---
title: Azure Dev Space を操作する場合のシークレットを管理する方法
titleSuffix: Azure Dev Spaces
services: azure-dev-spaces
ms.service: azure-dev-spaces
author: zr-msft
ms.author: zarhoads
ms.date: 05/11/2018
ms.topic: conceptual
description: Azure のコンテナーとマイクロサービスを使用した迅速な Kubernetes 開発
keywords: Docker, Kubernetes, Azure, AKS, Azure Container Service, コンテナー
ms.openlocfilehash: 8ee50289083b12b7b2abd3b9ece2c8de345df9fe
ms.sourcegitcommit: 16cb78a0766f9b3efbaf12426519ddab2774b815
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/17/2019
ms.locfileid: "65851429"
---
# <a name="how-to-manage-secrets-when-working-with-an-azure-dev-space"></a>Azure Dev Space を操作する場合のシークレットを管理する方法

サービスで、データベースやその他のセキュリティ保護された Azure サービスなどの特定のパスワード、接続文字列、およびその他のシークレットが必要になることがあります。 構成ファイルにこれらのシークレットの値を設定して、コードで環境変数としてそれらを使用できるようにすることができます。  これらは、シークレットのセキュリティを損なわないように注意して扱う必要があります。

Azure Dev Spaces では、シークレットを格納するための 2 つの推奨されるオプションが用意されています。values.dev.yaml ファイル内と azds.yaml にインラインで直接格納する方法です。 values.yaml にシークレットを格納することはお勧めしません。
 
## <a name="method-1-valuesdevyaml"></a>方法 1: values.dev.yaml
1. Azure Dev Spaces 用に有効にされているプロジェクトで VS Code を開きます。
2. 既存の _azds.yaml_ と同じフォルダーに、_values.dev.yaml_ という名前のファイルを追加し、次の例のように秘密鍵と値を定義します。

    ```yaml
    secrets:
      redis:
        port: "6380"
        host: "contosodevredis.redis.cache.windows.net"
        key: "secretkeyhere"
    ```
     
3. _azds.yaml_ は、_values.dev.yaml_ ファイルが存在する場合はそれを既に参照しています。 別のファイル名が好みの場合は、install.values セクションを更新します。

    ```yaml
    install:
      values:
      - values.dev.yaml?
      - secrets.dev.yaml?
    ```
 
4. 次の例のように、環境変数としてこれらのシークレットを参照するようにサービス コードを変更します。

    ```
    var redisPort = process.env.REDIS_PORT
    var host = process.env.REDIS_HOST
    var theKey = process.env.REDIS_KEY
    ```
    
5. クラスターで実行されているサービスをこれらの変更で更新します。 コマンド ラインで、次のコマンドを実行します。

    ```
    azds up
    ```
 
6. (省略可能) コマンド ラインから、これらのシークレットが作成されたことを確認します。

      ```
      kubectl get secret --namespace default -o yaml 
      ```

7. _values.dev.yaml_ を _.gitignore_ ファイルに追加して、ソース管理でシークレットがコミットされないようにします。
 
 
## <a name="method-2-inline-directly-in-azdsyaml"></a>方法 2:azds.yaml にインラインで直接
1.  _Azds.yaml_ で、yaml セクションの configurations/develop/install の下にシークレットを設定します。 ここにシークレット値を直接入力できますが、_azds.yaml_ はソース管理にチェックインされるため、お勧めしません。 代わりに、"$PLACEHOLDER" 構文を使用してプレース ホルダーを追加します。

    ```yaml
    configurations:
      develop:
        ...
        install:
          set:
            secrets:
              redis:
                port: "$REDIS_PORT"
                host: "$REDIS_HOST"
                key: "$REDIS_KEY"
    ```
     
2.  _azds.yaml_ ファイルと同じフォルダーに _.env_ ファイルを作成します。 標準の key=value 表記を使用してシークレットを入力します。 _.env_ ファイルをソース管理にコミットしないでください。 (Git ベースのバージョン管理システムでソース管理から除外するには、それを _.gitignore_ ファイルに追加します)。次の例は、 _.env_ ファイルを示しています。

    ```
    REDIS_PORT=3333
    REDIS_HOST=myredishost
    REDIS_KEY=myrediskey
    ```
2.  次の例のように、コードで、これらのシークレットを参照するようにサービス ソース コードを変更します。

    ```
    var redisPort = process.env.REDIS_PORT
    var host = process.env.REDIS_HOST
    var theKey = process.env.REDIS_KEY
    ```
 
3.  クラスターで実行されているサービスをこれらの変更で更新します。 コマンド ラインで、次のコマンドを実行します。

    ```
    azds up
    ```

4.  (省略可能) Kubectl からシークレットを表示します。

    ```
    kubectl get secret --namespace default -o yaml
    ```

## <a name="next-steps"></a>次の手順

これらの方法によって、データベース、Azure Cache for Redis に安全に接続したり、セキュリティ保護された Azure サービスにアクセスしたりできます。
 
