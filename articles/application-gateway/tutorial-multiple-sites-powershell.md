---
title: 複数の Web サイトをホストするアプリケーション ゲートウェイの作成 - Azure PowerShell
description: Azure PowerShell を使用して、複数の Web サイトをホストするアプリケーション ゲートウェイを作成する方法について説明します。
services: application-gateway
author: vhorne
ms.service: application-gateway
ms.topic: tutorial
ms.workload: infrastructure-services
ms.date: 7/13/2018
ms.author: victorh
ms.custom: mvc
ms.openlocfilehash: 9309778ad173e0c2588fa8814b16c7026e9ae7ba
ms.sourcegitcommit: 1aefdf876c95bf6c07b12eb8c5fab98e92948000
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2019
ms.locfileid: "66729557"
---
# <a name="create-an-application-gateway-that-hosts-multiple-web-sites-using-azure-powershell"></a>Azure PowerShell を使用して、複数の Web サイトをホストするアプリケーション ゲートウェイを作成する

[アプリケーション ゲートウェイ](overview.md)を作成するときに、Azure PowerShell を使用して [複数の Web サイト](multiple-site-overview.md)のホスティングを構成できます。 このチュートリアルでは、仮想マシン スケール セットを使用してバックエンド アドレス プールを定義します。 その後、Web トラフィックがプール内の適切なサーバーに確実に到着するように、所有するドメインに基づいてリスナーと規則を構成します。 このチュートリアルでは、複数のドメインを所有していることを前提として、*www.contoso.com* と *www.fabrikam.com* の例を使用します。

このチュートリアルでは、以下の内容を学習します。

> [!div class="checklist"]
> * ネットワークのセットアップ
> * アプリケーション ゲートウェイの作成
> * バックエンド リスナーの作成
> * ルーティング規則の作成
> * バックエンド プールを含んだ仮想マシン スケール セットの作成
> * ドメインの CNAME レコードの作成

![マルチサイト ルーティングの例](./media/tutorial-multiple-sites-powershell/scenario.png)

Azure サブスクリプションをお持ちでない場合は、開始する前に [無料アカウント](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) を作成してください。

[!INCLUDE [updated-for-az](../../includes/updated-for-az.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

PowerShell をインストールしてローカルで使用する場合、このチュートリアルでは Azure PowerShell モジュール バージョン 1.0.0 以降が必要になります。 バージョンを確認するには、`Get-Module -ListAvailable Az` を実行します。 アップグレードする必要がある場合は、[Azure PowerShell モジュールのインストール](/powershell/azure/install-az-ps)に関するページを参照してください。 PowerShell をローカルで実行している場合、`Login-AzAccount` を実行して Azure との接続を作成することも必要です。

## <a name="create-a-resource-group"></a>リソース グループの作成

リソース グループとは、Azure リソースのデプロイと管理に使用する論理コンテナーです。 [New-AzResourceGroup](/powershell/module/az.resources/new-azresourcegroup) を使用して Azure リソース グループを作成します。  

```azurepowershell-interactive
New-AzResourceGroup -Name myResourceGroupAG -Location eastus
```

## <a name="create-network-resources"></a>ネットワーク リソースを作成する

[New-AzVirtualNetworkSubnetConfig](/powershell/module/az.network/new-azvirtualnetworksubnetconfig) を使用してサブネット構成を作成します。 [New-AzVirtualNetwork](/powershell/module/az.network/new-azvirtualnetwork) とサブネット構成を使用して仮想ネットワークを作成します。 最後に、[New-AzPublicIpAddress](/powershell/module/az.network/new-azpublicipaddress) を使用してパブリック IP アドレスを作成します。 こうしたリソースは、アプリケーション ゲートウェイとその関連リソースにネットワーク接続を提供するために使用されます。

```azurepowershell-interactive
$backendSubnetConfig = New-AzVirtualNetworkSubnetConfig `
  -Name myBackendSubnet `
  -AddressPrefix 10.0.1.0/24

$agSubnetConfig = New-AzVirtualNetworkSubnetConfig `
  -Name myAGSubnet `
  -AddressPrefix 10.0.2.0/24

$vnet = New-AzVirtualNetwork `
  -ResourceGroupName myResourceGroupAG `
  -Location eastus `
  -Name myVNet `
  -AddressPrefix 10.0.0.0/16 `
  -Subnet $backendSubnetConfig, $agSubnetConfig

$pip = New-AzPublicIpAddress `
  -ResourceGroupName myResourceGroupAG `
  -Location eastus `
  -Name myAGPublicIPAddress `
  -AllocationMethod Dynamic
```

## <a name="create-an-application-gateway"></a>アプリケーション ゲートウェイの作成

### <a name="create-the-ip-configurations-and-frontend-port"></a>IP 構成とフロントエンド ポートの作成

[New-AzApplicationGatewayIPConfiguration](/powershell/module/az.network/new-azapplicationgatewayipconfiguration) を使用して、前に作成したサブネットをアプリケーション ゲートウェイに関連付けます。 [New-AzApplicationGatewayFrontendIPConfig](/powershell/module/az.network/new-azapplicationgatewayfrontendipconfig) を使用して、パブリック IP アドレスをアプリケーション ゲートウェイに割り当てます。

```azurepowershell-interactive
$vnet = Get-AzVirtualNetwork `
  -ResourceGroupName myResourceGroupAG `
  -Name myVNet

$subnet=$vnet.Subnets[0]

$gipconfig = New-AzApplicationGatewayIPConfiguration `
  -Name myAGIPConfig `
  -Subnet $subnet

$fipconfig = New-AzApplicationGatewayFrontendIPConfig `
  -Name myAGFrontendIPConfig `
  -PublicIPAddress $pip

$frontendport = New-AzApplicationGatewayFrontendPort `
  -Name myFrontendPort `
  -Port 80
```

### <a name="create-the-backend-pools-and-settings"></a>バックエンド プールと設定の作成

[New-AzApplicationGatewayBackendAddressPool](/powershell/module/az.network/new-azapplicationgatewaybackendaddresspool) を使用して、アプリケーション ゲートウェイのために最初のバックエンド アドレス プールを作成します。 [New-AzApplicationGatewayBackendHttpSettings](/powershell/module/az.network/new-azapplicationgatewaybackendhttpsetting) を使用して、プールの設定を構成します。

```azurepowershell-interactive
$contosoPool = New-AzApplicationGatewayBackendAddressPool `
  -Name contosoPool

$fabrikamPool = New-AzApplicationGatewayBackendAddressPool `
  -Name fabrikamPool

$poolSettings = New-AzApplicationGatewayBackendHttpSettings `
  -Name myPoolSettings `
  -Port 80 `
  -Protocol Http `
  -CookieBasedAffinity Enabled `
  -RequestTimeout 120
```

### <a name="create-the-listeners-and-rules"></a>リスナーと規則の作成

アプリケーション ゲートウェイが適切にトラフィックをバックエンド アドレス プールにルーティングできるようにするには、リスナーが必要です。 このチュートリアルでは、2 つのドメインに対して 2 つのリスナーを作成します。 この例では、*www.contoso.com* と *www.fabrikam.com* のドメインに対してリスナーを作成しています。

前に作成したフロントエンド構成とフロントエンド ポートを指定して [New-AzApplicationGatewayHttpListener](/powershell/module/az.network/new-azapplicationgatewayhttplistener) を使用し、最初のリスナーを作成します。 着信トラフィックに使用するバックエンド プールをリスナーが判断するには、ルールが必要です。 [New-AzApplicationGatewayRequestRoutingRule](/powershell/module/az.network/new-azapplicationgatewayrequestroutingrule) を使用して、*contosoRule* という名前の基本ルールを作成します。

```azurepowershell-interactive
$contosolistener = New-AzApplicationGatewayHttpListener `
  -Name contosoListener `
  -Protocol Http `
  -FrontendIPConfiguration $fipconfig `
  -FrontendPort $frontendport `
  -HostName "www.contoso.com"

$fabrikamlistener = New-AzApplicationGatewayHttpListener `
  -Name fabrikamListener `
  -Protocol Http `
  -FrontendIPConfiguration $fipconfig `
  -FrontendPort $frontendport `
  -HostName "www.fabrikam.com"

$contosoRule = New-AzApplicationGatewayRequestRoutingRule `
  -Name contosoRule `
  -RuleType Basic `
  -HttpListener $contosoListener `
  -BackendAddressPool $contosoPool `
  -BackendHttpSettings $poolSettings

$fabrikamRule = New-AzApplicationGatewayRequestRoutingRule `
  -Name fabrikamRule `
  -RuleType Basic `
  -HttpListener $fabrikamListener `
  -BackendAddressPool $fabrikamPool `
  -BackendHttpSettings $poolSettings
```

### <a name="create-the-application-gateway"></a>アプリケーション ゲートウェイの作成

必要な関連リソースを作成したら、[New-AzApplicationGatewaySku](/powershell/module/az.network/new-azapplicationgatewaysku) を使用してアプリケーション ゲートウェイのパラメーターを指定し、[New-AzApplicationGateway](/powershell/module/az.network/new-azapplicationgateway) を使用してそれを作成します。

```azurepowershell-interactive
$sku = New-AzApplicationGatewaySku `
  -Name Standard_Medium `
  -Tier Standard `
  -Capacity 2

$appgw = New-AzApplicationGateway `
  -Name myAppGateway `
  -ResourceGroupName myResourceGroupAG `
  -Location eastus `
  -BackendAddressPools $contosoPool, $fabrikamPool `
  -BackendHttpSettingsCollection $poolSettings `
  -FrontendIpConfigurations $fipconfig `
  -GatewayIpConfigurations $gipconfig `
  -FrontendPorts $frontendport `
  -HttpListeners $contosoListener, $fabrikamListener `
  -RequestRoutingRules $contosoRule, $fabrikamRule `
  -Sku $sku
```

## <a name="create-virtual-machine-scale-sets"></a>仮想マシン スケール セットの作成

この例では、作成した 2 つのバックエンド プールをサポートする 2 つの仮想マシン スケール セットを作成します。 作成するスケール セットの名前は、*myvmss1* と *myvmss2* です。 各スケール セットには、IIS をインストールする 2 つの仮想マシン インスタンスが含まれています。 スケール セットは、IP 設定を構成するときにバックエンド プールに割り当てます。

```azurepowershell-interactive
$vnet = Get-AzVirtualNetwork `
  -ResourceGroupName myResourceGroupAG `
  -Name myVNet

$appgw = Get-AzApplicationGateway `
  -ResourceGroupName myResourceGroupAG `
  -Name myAppGateway

$contosoPool = Get-AzApplicationGatewayBackendAddressPool `
  -Name contosoPool `
  -ApplicationGateway $appgw

$fabrikamPool = Get-AzApplicationGatewayBackendAddressPool `
  -Name fabrikamPool `
  -ApplicationGateway $appgw

for ($i=1; $i -le 2; $i++)
{
  if ($i -eq 1) 
  {
    $poolId = $contosoPool.Id
  }
  if ($i -eq 2)
  {
    $poolId = $fabrikamPool.Id
  }

  $ipConfig = New-AzVmssIpConfig `
    -Name myVmssIPConfig$i `
    -SubnetId $vnet.Subnets[1].Id `
    -ApplicationGatewayBackendAddressPoolsId $poolId

  $vmssConfig = New-AzVmssConfig `
    -Location eastus `
    -SkuCapacity 2 `
    -SkuName Standard_DS2 `
    -UpgradePolicyMode Automatic

  Set-AzVmssStorageProfile $vmssConfig `
    -ImageReferencePublisher MicrosoftWindowsServer `
    -ImageReferenceOffer WindowsServer `
    -ImageReferenceSku 2016-Datacenter `
    -ImageReferenceVersion latest
    -OsDiskCreateOption FromImage

  Set-AzVmssOsProfile $vmssConfig `
    -AdminUsername azureuser `
    -AdminPassword "Azure123456!" `
    -ComputerNamePrefix myvmss$i

  Add-AzVmssNetworkInterfaceConfiguration `
    -VirtualMachineScaleSet $vmssConfig `
    -Name myVmssNetConfig$i `
    -Primary $true `
    -IPConfiguration $ipConfig

  New-AzVmss `
    -ResourceGroupName myResourceGroupAG `
    -Name myvmss$i `
    -VirtualMachineScaleSet $vmssConfig
}
```

### <a name="install-iis"></a>IIS のインストール

```azurepowershell-interactive
$publicSettings = @{ "fileUris" = (,"https://raw.githubusercontent.com/Azure/azure-docs-powershell-samples/master/application-gateway/iis/appgatewayurl.ps1"); 
  "commandToExecute" = "powershell -ExecutionPolicy Unrestricted -File appgatewayurl.ps1" }

for ($i=1; $i -le 2; $i++)
{
  $vmss = Get-AzVmss `
    -ResourceGroupName myResourceGroupAG `
    -VMScaleSetName myvmss$i

  Add-AzVmssExtension -VirtualMachineScaleSet $vmss `
    -Name "customScript" `
    -Publisher "Microsoft.Compute" `
    -Type "CustomScriptExtension" `
    -TypeHandlerVersion 1.8 `
    -Setting $publicSettings

  Update-AzVmss `
    -ResourceGroupName myResourceGroupAG `
    -Name myvmss$i `
    -VirtualMachineScaleSet $vmss
}
```

## <a name="create-cname-record-in-your-domain"></a>ドメインの CNAME レコードの作成

パブリック IP アドレスを使用してアプリケーション ゲートウェイを作成した後は、DNS アドレスを取得し、これを使用してドメインに CNAME レコードを作成できます。 [Get-AzPublicIPAddress](/powershell/module/az.network/get-azpublicipaddress) を使用して、アプリケーション ゲートウェイの DNS アドレスを取得できます。 DNSSettings の *fqdn* 値をコピーし、作成した CNAME レコードの値として使用します。 アプリケーション ゲートウェイを再起動すると VIP が変更される可能性があるため、A レコードの使用はお勧めしません。

```azurepowershell-interactive
Get-AzPublicIPAddress -ResourceGroupName myResourceGroupAG -Name myAGPublicIPAddress
```

## <a name="test-the-application-gateway"></a>アプリケーション ゲートウェイのテスト

ブラウザーのアドレス バーにドメイン名を入力します。 http://www.contoso.com など。

![アプリケーション ゲートウェイの contoso サイトをテストする](./media/tutorial-multiple-sites-powershell/application-gateway-iistest.png)

アドレスをもう 1 つのドメインに変更します。次の例のように表示されます。

![アプリケーション ゲートウェイの fabrikam サイトをテストする](./media/tutorial-multiple-sites-powershell/application-gateway-iistest2.png)

## <a name="clean-up-resources"></a>リソースのクリーンアップ

必要がなくなったら、[Remove-AzResourceGroup](/powershell/module/az.resources/remove-azresourcegroup) を使用して、リソース グループ、アプリケーション ゲートウェイ、およびすべての関連リソースを削除します。

```azurepowershell-interactive
Remove-AzResourceGroup -Name myResourceGroupAG
```

## <a name="next-steps"></a>次の手順

このチュートリアルでは、以下の内容を学習しました。

> [!div class="checklist"]
> * ネットワークのセットアップ
> * アプリケーション ゲートウェイの作成
> * バックエンド リスナーの作成
> * ルーティング規則の作成
> * バックエンド プールを含んだ仮想マシン スケール セットの作成
> * ドメインの CNAME レコードの作成

> [!div class="nextstepaction"]
> [URL パスベースのルーティング規則のあるアプリケーション ゲートウェイを作成する](./tutorial-url-route-powershell.md)
