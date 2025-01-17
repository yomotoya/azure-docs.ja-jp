---
title: Azure IoT Edge のモジュールを開発する | Microsoft Docs
description: ランタイムおよび IoT Hub と通信できる Azure IoT Edge 用のカスタム モジュールを開発する
author: kgremban
manager: philmea
ms.author: kgremban
ms.date: 02/25/2019
ms.topic: conceptual
ms.service: iot-edge
services: iot-edge
ms.custom: seodec18
ms.openlocfilehash: 5285490ca1a27494cbcd3ea3d6527b78c7d38c8c
ms.sourcegitcommit: 3ced637c8f1f24256dd6ac8e180fff62a444b03c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/17/2019
ms.locfileid: "65833430"
---
# <a name="develop-your-own-iot-edge-modules"></a>独自の IoT Edge モジュールを開発する

Azure IoT Edge モジュールでは、他の Azure サービスに接続し、大規模なクラウド データ パイプラインに関与することができます。 この記事では、IoT Edge ランタイムと IoT Hub、したがって Azure クラウドの残りの部分とも通信するモジュールを開発する方法について説明します。 

## <a name="iot-edge-runtime-environment"></a>IoT Edge ランタイム環境
IoT Edge ランタイムでは、複数のIoT Edge モジュールの機能を統合し、IoT Edge デバイス上に展開するためのインフラストラクチャが提供されます。 簡単に言えば、ユーザーは任意のプログラムを IoT Edge モジュールとしてパッケージ化することができます。 ただし、IoT Edge の通信機能や管理機能を活用するには、モジュールで実行されるプログラムが、IoT Edge ランタイムに統合されたローカル IoT Edge ハブに接続できる必要があります。

## <a name="using-the-iot-edge-hub"></a>IoT Edge ハブの使用
IoT Edge ハブでは、2 つの主要機能が提供されます。 IoT Hub へのプロキシと、ローカル通信です。

### <a name="iot-hub-primitives"></a>IoT Hub プリミティブ
IoT Hub では、次のような意味で、モジュール インスタンスがデバイスのようなものとして見なされます。

* [デバイス ツイン](../iot-hub/iot-hub-devguide-device-twins.md)、およびそのデバイスの他のモジュール ツインとは区別されて分離された、モジュール ツインがある。
* [device-to-cloud メッセージ](../iot-hub/iot-hub-devguide-messaging.md)を送信できる。
* その ID で明確に対象とされた[ダイレクト メソッド](../iot-hub/iot-hub-devguide-direct-methods.md)を受け取ることができる。

現在のところ、モジュールでは、クラウドからデバイスへのメッセージを受信したり、ファイルのアップロード機能を使用することはできません。

モジュールを作成する際には、[Azure IoT Device SDK](../iot-hub/iot-hub-devguide-sdks.md) を使用して IoT Edge ハブに接続し、デバイス アプリケーションで IoT Hub を使用する場合と同様に、上記の機能を使用することができます。違うのは、アプリケーション バックエンドから、デバイス ID ではなくモジュール ID を参照する必要があるという点だけです。

### <a name="device-to-cloud-messages"></a>デバイスからクラウドへのメッセージ
デバイスからクラウドへのメッセージの複雑な処理を可能にするため、IoT Edge ハブでは、モジュール間、およびモジュールと IoT Hub 間での、メッセージの宣言型ルーティングが提供されます。 宣言型ルーティングによって、モジュールは他のモジュールによって送信されたメッセージをインターセプトして処理し、それらを複雑なパイプラインに伝達できるようになります。 詳細については、[モジュールのデプロイと IoT Edge へのルートの確立](module-composition.md)に関する記事をご覧ください。

通常の IoT Hub デバイス アプリケーションとは違い、IoT Edge モジュールでは、ローカルの IoT Edge ハブによってプロキシされている、デバイスからクラウドへのメッセージを受信し、それらを処理することができます。

IoT Edge ハブでは、[配置マニフェスト](module-composition.md)に関するページで説明されている宣言型のルートに基づいて、メッセージをモジュールに伝達します。 IoT Edge モジュールの開発時には、メッセージ ハンドラーを設定してこれらのメッセージを受信できます。

ルートの作成を簡略化するため、IoT Edge では、モジュールの*入力* エンドポイントと*出力* エンドポイントの概念が追加されています。 モジュールは、自身にルーティングされたすべての D2C メッセージ (デバイスからクラウドへのメッセージ) を、入力を指定することなく受信したり、出力を指定することなく、D2C メッセージ送信することができます。 ただし、明示的な入力と出力を使用したほうが、ルーティング ルールがわかりやすくなります。 

最後に、Edge ハブによって処理された D2C メッセージには、次のシステム プロパティを使用してスタンプが付けられます。

| プロパティ | 説明 |
| -------- | ----------- |
| $connectionDeviceId | メッセージを送信したクライアントのデバイス ID |
| $connectionModuleId | メッセージを送信したモジュールのモジュール ID |
| $inputName | このメッセージを受信した入力。 空の場合もあります。 |
| $outputName | メッセージを送信するために使用された出力。 空の場合もあります。 |

### <a name="connecting-to-iot-edge-hub-from-a-module"></a>モジュールから IoT Edge ハブへの接続
モジュールからローカル IoT Edge ハブに接続するには、2 つの手順が必要です。 
1. アプリケーションで ModuleClient インスタンスを作成します。
2. そのデバイスの IoT Edge ハブによって提示された証明書がアプリケーションによって受け入れられることを確認します。

ModuleClient インスタンスを作成し、デバイスで実行されている IoT Edge ハブにモジュールを接続します。これは、DeviceClient インスタンスで IoT デバイスを IoT Hub に接続する方法と似ています。 ModuleClient クラスとその通信方法に関する詳細については、優先する SDK 言語 ([C# ](https://docs.microsoft.com/dotnet/api/microsoft.azure.devices.client.moduleclient?view=azure-dotnet)、[C および Python](https://docs.microsoft.com/azure/iot-hub/iot-c-sdk-ref/iothub-module-client-h)、[Java](https://docs.microsoft.com/java/api/com.microsoft.azure.sdk.iot.device.moduleclient?view=azure-java-stable)、[Node.js](https://docs.microsoft.com/javascript/api/azure-iot-device/moduleclient?view=azure-node-latest)) の API リファレンスを参照してください。


## <a name="next-steps"></a>次の手順

[IoT Edge のための開発およびテスト環境の準備](development-environment.md)

[Visual Studio を使用して IoT Edge 用の C# モジュールを開発する](how-to-visual-studio-develop-module.md)

[Visual Studio Code を使用して IoT Edge 用のモジュールを開発する](how-to-vs-code-develop-module.md)

