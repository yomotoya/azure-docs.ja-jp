---
title: Azure Database for MySQL の読み取りレプリカの作成と管理
description: このアーティクルでは、Azure CLI を使用して Azure Database for MySQL の読み取りレプリカを設定し、管理する方法について説明します。
author: ajlam
ms.author: andrela
ms.service: mysql
ms.topic: conceptual
ms.date: 05/28/2019
ms.openlocfilehash: ba8af55f7467e361136e4b0c57c97b4fa187cec0
ms.sourcegitcommit: 009334a842d08b1c83ee183b5830092e067f4374
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66304954"
---
# <a name="how-to-create-and-manage-read-replicas-in-azure-database-for-mysql-using-the-azure-cli"></a>Azure CLI を使用して Azure Database for MySQL の読み取りレプリカを作成し、管理する方法

この記事では、Azure CLI を使用して Azure Database for MySQL のマスターと同じ Azure リージョン内に読み取りレプリカを作成し、管理する方法を学びます。

> [!IMPORTANT]
> マスター サーバーと同じ Azure リージョン内、または選択した他の任意の Azure リージョン内に読み取りレプリカを作成できます。 リージョン間レプリケーションは、現在パブリック プレビュー段階です。

## <a name="prerequisites"></a>前提条件

- [Azure CLI 2.0 のインストール](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest)
- マスター サーバーとして使用される [Azure Database for MySQL サーバー ](quickstart-create-mysql-server-database-using-azure-portal.md)。 

> [!IMPORTANT]
> 読み取りレプリカ機能は、汎用とメモリ最適化のどちらかの価格レベルにおける Azure Database for MySQL サーバーにのみ使用可能です。 マスター サーバーがこれらの価格レベルのいずれかを確認します。

## <a name="create-a-read-replica"></a>読み取りレプリカを作成します

読み取りレプリカ サーバーは、次のコマンドを使用して作成できます。

```azurecli-interactive
az mysql server replica create --name mydemoreplicaserver --source-server mydemoserver --resource-group myresourcegroup
```

`az mysql server replica create` コマンドには、次のパラメーターが必要です。

| Setting | 値の例 | 説明  |
| --- | --- | --- |
| resource-group |  myresourcegroup |  レプリカ サーバーを作成するリソース グループ。  |
| name | mydemoreplicaserver | 作成する新しいレプリカ サーバーの名前。 |
| source-server | mydemoserver | レプリケート元の既存のマスター サーバーの名前または ID。 |

リージョンをまたがる読み取りレプリカを作成するには、`--location` パラメーターを使用します。 次の CLI の例では、米国西部にレプリカを作成します。

```azurecli-interactive
az mysql server replica create --name mydemoreplicaserver --source-server mydemoserver --resource-group myresourcegroup --location westus
```

> [!NOTE]
> マスターと同じサーバー構成で、読み取りレプリカが作成されます。 作成された後、レプリカ サーバーの構成を変更できます。 レプリカをマスターと維持できるようにするために、レプリカ サーバーの構成をマスターと同じかそれ以上の値にしておくようお勧めします。

## <a name="stop-replication-to-a-replica-server"></a>レプリカ サーバーへのレプリケーションを停止します。

> [!IMPORTANT]
> サーバーへのレプリケーションの停止は、元に戻すことができません。 マスターとレプリカの間のレプリケーションを停止すると、取り消すことができません。 レプリカ サーバーはスタンドアロン サーバーになり、読み取りと書き込みをサポートするようになります。 このサーバーをもう一度レプリカにすることはできません。

読み取りレプリカ サーバーへのレプリケーションは、次のコマンドを使用して停止できます。

```azurecli-interactive
az mysql server replica stop --name mydemoreplicaserver --resource-group myresourcegroup
```

`az mysql server replica stop` コマンドには、次のパラメーターが必要です。

| Setting | 値の例 | 説明  |
| --- | --- | --- |
| resource-group |  myresourcegroup |  レプリカ サーバーが存在するリソース グループ。  |
| name | mydemoreplicaserver | レプリケーションを停止するレプリカ サーバーの名前。 |

## <a name="delete-a-replica-server"></a>レプリカ サーバーを削除します

読み取りレプリカ サーバーの削除は、 **[az mysql server delete](/cli/azure/mysql/server)** コマンドを使用して行うことができます。

```azurecli-interactive
az mysql server delete --resource-group myresourcegroup --name mydemoreplicaserver
```

## <a name="delete-a-master-server"></a>マスター サーバーを削除します

> [!IMPORTANT]
> マスター サーバーを削除すると、すべてのレプリカ サーバーへのレプリケーションを停止し、マスター サーバー自体を削除します。 これでレプリカ サーバーは、読み取りと書き込みの両方をサポートするスタンドアロン サーバーになります。

マスター サーバーを削除するには、 **[az mysql server delete](/cli/azure/mysql/server)** コマンドを実行します。

```azurecli-interactive
az mysql server delete --resource-group myresourcegroup --name mydemoserver
```

## <a name="list-replicas-for-a-master-server"></a>マスター サーバーのレプリカを一覧表示する

特定のマスター サーバーのすべてのレプリカを表示するには、次のコマンドを実行します。 

```azurecli-interactive
az mysql server replica list --server-name mydemoserver --resource-group myresourcegroup
```

`az mysql server replica list` コマンドには、次のパラメーターが必要です。

| Setting | 値の例 | 説明  |
| --- | --- | --- |
| resource-group |  myresourcegroup |  レプリカ サーバーを作成するリソース グループ。  |
| server-name | mydemoserver | マスター サーバーの名前または ID。 |

## <a name="next-steps"></a>次の手順

- [レプリカの読み取り](concepts-read-replicas.md) の詳細を確認する
