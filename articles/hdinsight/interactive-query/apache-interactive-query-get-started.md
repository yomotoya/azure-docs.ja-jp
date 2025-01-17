---
title: Azure HDInsight での対話型クエリの使用
description: HDInsight での対話型クエリ (Hive LLAP) の使用方法について説明します。
ms.service: hdinsight
author: hrasheed-msft
ms.author: hrasheed
ms.reviewer: jasonh
ms.custom: hdinsightactive
ms.topic: conceptual
ms.date: 05/07/2019
ms.openlocfilehash: db36bbf6e20f9fab2f9a99f59be7a088e8f208e1
ms.sourcegitcommit: 36c50860e75d86f0d0e2be9e3213ffa9a06f4150
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/16/2019
ms.locfileid: "65800922"
---
# <a name="use-interactive-query-with-hdinsight"></a>HDInsight での対話型クエリの使用
対話型クエリ (別名 Apache Hive LLAP または [Low Latency Analytical Processing](https://cwiki.apache.org/confluence/display/Hive/LLAP)) は、Azure HDInsight の[クラスターの一種](../hdinsight-hadoop-provision-linux-clusters.md#cluster-types)です。 対話型クエリではインメモリ キャッシュがサポートされるため、Apache Hive クエリの速度と対話性が向上します。

[!INCLUDE [hdinsight-price-change](../../../includes/hdinsight-enhancements.md)] 

対話型クエリ クラスターは、Apache Hadoop クラスターとは異なり、 Hive サービスのみが含まれます。 

> [!NOTE]  
> 対話型クエリ クラスター内の Hive サービスには、Apache Ambari Hive View、Beeline、および Microsoft Hive Open Database Connectivity ドライバー (Hive ODBC) からのみアクセスできます。 Hive コンソール、Templeton、Azure クラシック CLI、Azure PowerShell からはアクセスできません。 

## <a name="create-an-interactive-query-cluster"></a>対話型クエリ クラスターの作成
HDInsight クラスターの作成について詳しくは、[HDInsight 内での Apache Hadoop クラスターの作成](../hdinsight-hadoop-provision-linux-clusters.md)に関する記事をご覧ください。 対話型クエリのクラスターの種類を選択します。

## <a name="execute-apache-hive-queries-from-interactive-query"></a>対話型クエリから Apache Hive クエリを実行する
Hive クエリを実行するには、次のオプションがあります。

* Microsoft Power BI を使用する

    [Azure HDInsight 上の Power BI を使用した対話型クエリの Apache Hive データの視覚化](./apache-hadoop-connect-hive-power-bi-directquery.md)に関する記事をご覧ください。[Azure HDInsight 上の Power BI を使用したビッグ データの視覚化](../hadoop/apache-hadoop-connect-hive-power-bi.md)に関する記事をご覧ください。

* Visual Studio を使用する

    [Data Lake Tools for Visual Studio を使用した Azure HDInsight への接続と Apache Hive クエリの実行](../hadoop/apache-hadoop-visual-studio-tools-get-started.md#run-interactive-apache-hive-queries)に関するページをご覧ください。

* Visual Studio Code を使用する

    [Apache Hive、LLAP、pySpark に Visual Studio Code を使用する](../hdinsight-for-vscode.md)方法に関する記事を参照してください。
* Apache Ambari Hive ビューを使用して Apache Hive を実行する。
  
    [Azure HDInsight 上の Apache Hadoop で Apache Hive ビューを使用する](../hadoop/apache-hadoop-use-hive-ambari-view.md)方法に関する記事をご覧ください。

* Beeline を使用して Apache Hive を実行する。
  
    [Beeline による HDInsight 上の Apache Hive と Apache Hadoop の使用](../hadoop/apache-hadoop-use-hive-beeline.md)に関する記事をご覧ください。
  
    Beeline はヘッド ノードまたは空のエッジ ノードから使用できます。 空のエッジ ノードから Beeline を使用することをお勧めします。 空のエッジ ノードを使って HDInsight クラスターを作成する方法の詳細については、「[HDInsight での空のエッジ ノードの使用](../hdinsight-apps-use-edge-node.md)」を参照してください。
* Hive ODBC を使用して Apache Hive を実行する。
  
    [Microsoft Hive ODBC ドライバーを使用した Excel から Apache Hadoop への接続](../hadoop/apache-hadoop-connect-excel-hive-odbc-driver.md)に関するページをご覧ください。

Java Database Connectivity (JDBC) 接続文字列は次の方法で調べることができます。

1. `https://<cluster name>.AzureHDInsight.net` という URL を使用して Apache Ambari にサインインします。
2. 左側のメニューで **[Hive]** を選択します。
3. URL をコピーするには、クリップボード アイコンを選択します。
   
   ![HDInsight Hadoop 対話型クエリ LLAP JDBC](./media/apache-interactive-query-get-started/hdinsight-hadoop-use-interactive-hive-jdbc.png)

## <a name="next-steps"></a>次の手順

* [HDInsight で対話型クエリ クラスターを作成する](../hdinsight-hadoop-provision-linux-clusters.md)方法を学ぶ。
* [Azure HDInsight の Power BI でビッグ データを視覚化する](../hadoop/apache-hadoop-connect-hive-power-bi.md)方法を学ぶ。
* [Azure HDInsight で Apache Zeppelin を使用して Apache Hive クエリを実行する](../interactive-query/hdinsight-connect-hive-zeppelin.md)方法を学ぶ。
* [Data Lake Tools for Visual Studio を使用して Apache Hive クエリを実行する](../hadoop/apache-hadoop-visual-studio-tools-get-started.md#run-interactive-apache-hive-queries)方法を学ぶ。
* [HDInsight Tools for Visual Studio Code を使用する](../hdinsight-for-vscode.md)方法を学ぶ。
* [HDInsight 上の Apache Hadoop で Apache Hive ビューを使用する](../hadoop/apache-hadoop-use-hive-ambari-view.md)方法を学ぶ
* [Beeline を使用して HDInsight 内で Apache Hive クエリを実行する](../hadoop/apache-hadoop-use-hive-beeline.md)方法を学ぶ。
* [Microsoft Hive ODBC ドライバーを使用して Excel から Apache Hadoop に接続する](../hadoop/apache-hadoop-connect-excel-hive-odbc-driver.md)方法を学ぶ。

