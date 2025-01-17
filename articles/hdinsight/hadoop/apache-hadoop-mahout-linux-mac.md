---
title: Apache Mahout と HDInsight を使用してリコメンデーションを生成する (SSH) - Azure
description: Apache Mahout 機械学習ライブラリを使用して HDInsight (Hadoop) で映画のリコメンデーションを生成する方法について説明します。
author: hrasheed-msft
ms.author: hrasheed
ms.reviewer: jasonh
ms.service: hdinsight
ms.custom: hdinsightactive
ms.topic: conceptual
ms.date: 04/24/2019
ms.openlocfilehash: d566b57ae12520b9eee26334a67d2e10c05f8040
ms.sourcegitcommit: 44a85a2ed288f484cc3cdf71d9b51bc0be64cc33
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2019
ms.locfileid: "64709090"
---
# <a name="generate-movie-recommendations-by-using-apache-mahout-with-linux-based-apache-hadoop-in-hdinsight-ssh"></a>HDInsight 上の Apache Mahout と Linux ベースの Hadoop を使用して映画のリコメンデーションを生成する (SSH)

[!INCLUDE [mahout-selector](../../../includes/hdinsight-selector-mahout.md)]

[Apache Mahout](https://mahout.apache.org) 機械学習ライブラリを使用して Azure HDInsight で映画のリコメンデーションを生成する方法について説明します。

Mahout は、Apache Hadoop の[機械学習](https://en.wikipedia.org/wiki/Machine_learning)ライブラリの 1 つです。 Mahout には、フィルター処理、分類、クラスタリングなどデータを処理するためのアルゴリズムが含まれています。 この記事では、リコメンデーション エンジンを使用し、友人たちが鑑賞した映画に基づいて映画のリコメンデーションを生成します。

## <a name="prerequisites"></a>前提条件

* HDInsight の Apache Hadoop クラスター。 [Linux での HDInsight の概要](./apache-hadoop-linux-tutorial-get-started.md)に関するページを参照してください。

* SSH クライアント 詳細については、[SSH を使用して HDInsight (Apache Hadoop) に接続する方法](../hdinsight-hadoop-linux-use-ssh-unix.md)に関するページを参照してください。

## <a name="apache-mahout-versioning"></a>Apache Mahout のバージョン

HDInsight に含まれる Mahout のバージョンについて詳しくは、[HDInsight のバージョンと Apache Hadoop コンポーネント](../hdinsight-component-versioning.md)に関する記事を参照してください。

## <a name="recommendations"></a>リコメンデーションについて

Mahout で提供される機能の 1 つが、リコメンデーション エンジンです。 データは、`userID`、`itemId`、`prefValue` (項目に対する嗜好) の形式で受け付けられます。 Mahout では、共起分析を実行して、*ある項目を嗜好するユーザーが他の項目も嗜好する*ということを判断できます。 次に Mahout は、項目の嗜好が似ているユーザーを特定します。これはリコメンデーションの作成に使用できます。

映画のデータを使用したシンプルなワークフローの例を次に示します。

* **共起**: Joe、Alice、Bob は全員、好きな映画として "*Star Wars (スター ウォーズ)* "、"*The Empire Strikes Back (帝国の逆襲)* "、"*Return of the Jedi (ジェダイの帰還)* " を挙げました。 Mahout では、これらの映画のいずれかを好きなユーザーが他の 2 作品も好きであると判断します。

* **共起**: Bob と Alice は "*The Phantom Menace (ファントム メナス)* "、"*Attack of the Clones (クローンの攻撃)* "、"*Revenge of the Sith (シスの復讐)* " も好きな映画として選びました。 Mahout では、この例の最初の 3 作品を好きなユーザーがこれらの 3 作品も好きであると判断します。

* **類似性のレコメンデーション**: Joe は、この例の最初の 3 作品を好きな映画として選びました。Mahout では、嗜好が似ている他のユーザーが好きな映画の中で、Joe がまだ観ていない映画を調べます (好み/順位)。 この場合、Mahout では、「*The Phantom Menace (ファントム メナス)* 」、「*Attack of the Clones (クローンの攻撃)* 」、「*Revenge of the Sith (シスの復讐)* 」を推薦します。

### <a name="understanding-the-data"></a>データの説明

[GroupLens Research](https://grouplens.org/datasets/movielens/) では利便性を高めるために、Mahout と互換性のある形式で映画の評価データを提供します。 このデータは、クラスターの既定の記憶域 ( `/HdiSamples/HdiSamples/MahoutMovieData`) にあります。

`moviedb.txt` と `user-ratings.txt` という 2 つのファイルがあります。 `user-ratings.txt` ファイルは分析時に使用されます。 `moviedb.txt` ファイルは、結果を表示するときにわかりやすいテキストを提供するために使用されます。

user-ratings.txt に含まれているデータの構造は `userID`、`movieID`、`userRating`、および `timestamp` です。これは、各ユーザーによって映画に対してどれだけ高い評価が付けられているか示しています。 次にデータの例を示します。

    196    242    3    881250949
    186    302    3    891717742
    22     377    1    878887116
    244    51     2    880606923
    166    346    1    886397596

## <a name="run-the-analysis"></a>分析を実行する

クラスターに SSH で接続してから、次のコマンドを使用してリコメンデーション ジョブを実行します。

```bash
mahout recommenditembased -s SIMILARITY_COOCCURRENCE -i /HdiSamples/HdiSamples/MahoutMovieData/user-ratings.txt -o /example/data/mahoutout --tempDir /temp/mahouttemp
```

> [!NOTE]  
> ジョブが完了するまでに数分かかる場合があり、複数の MapReduce ジョブを実行することがあります。

## <a name="view-the-output"></a>出力を表示する

1. ジョブが完了したら、次のコマンドを使用して、生成された出力を表示します。

    ```bash
    hdfs dfs -text /example/data/mahoutout/part-r-00000
    ```

    出力は次のようになります。

        1    [234:5.0,347:5.0,237:5.0,47:5.0,282:5.0,275:5.0,88:5.0,515:5.0,514:5.0,121:5.0]
        2    [282:5.0,210:5.0,237:5.0,234:5.0,347:5.0,121:5.0,258:5.0,515:5.0,462:5.0,79:5.0]
        3    [284:5.0,285:4.828125,508:4.7543354,845:4.75,319:4.705128,124:4.7045455,150:4.6938777,311:4.6769233,248:4.65625,272:4.649266]
        4    [690:5.0,12:5.0,234:5.0,275:5.0,121:5.0,255:5.0,237:5.0,895:5.0,282:5.0,117:5.0]

    最初の列は `userID`です。 "[" と "]" に含まれる値は `movieId`:`recommendationScore` です。

2. 出力を moviedb.txt と共に使用して、よりわかりやすくリコメンデーションを表示できます。 最初に、次のコマンドを使用して、ファイルをローカルにコピーします。

    ```bash
    hdfs dfs -get /example/data/mahoutout/part-r-00000 recommendations.txt
    hdfs dfs -get /HdiSamples/HdiSamples/MahoutMovieData/* .
    ```

    これにより、出力データが、現在のディレクトリの **recommendations.txt** という名前のファイルにコピーされます。また、映画データ ファイルもコピーされます。

3. 次のコマンドを使用し、リコメンデーション出力のデータの映画の名前を検索する Python スクリプトを作成します。

    ```bash
    nano show_recommendations.py
    ```

    エディターが開いたら、ファイルの内容として次のテキストを使用します。

   ```python
   #!/usr/bin/env python

   import sys

   if len(sys.argv) != 5:
        print "Arguments: userId userDataFilename movieFilename recommendationFilename"
        sys.exit(1)

   userId, userDataFilename, movieFilename, recommendationFilename = sys.argv[1:]

   print "Reading Movies Descriptions"
   movieFile = open(movieFilename)
   movieById = {}
   for line in movieFile:
       tokens = line.split("|")
       movieById[tokens[0]] = tokens[1:]
   movieFile.close()

   print "Reading Rated Movies"
   userDataFile = open(userDataFilename)
   ratedMovieIds = []
   for line in userDataFile:
       tokens = line.split("\t")
       if tokens[0] == userId:
           ratedMovieIds.append((tokens[1],tokens[2]))
   userDataFile.close()

   print "Reading Recommendations"
   recommendationFile = open(recommendationFilename)
   recommendations = []
   for line in recommendationFile:
       tokens = line.split("\t")
       if tokens[0] == userId:
           movieIdAndScores = tokens[1].strip("[]\n").split(",")
           recommendations = [ movieIdAndScore.split(":") for movieIdAndScore in movieIdAndScores ]
           break
   recommendationFile.close()

   print "Rated Movies"
   print "------------------------"
   for movieId, rating in ratedMovieIds:
       print "%s, rating=%s" % (movieById[movieId][0], rating)
   print "------------------------"

   print "Recommended Movies"
   print "------------------------"
   for movieId, score in recommendations:
       print "%s, score=%s" % (movieById[movieId][0], score)
   print "------------------------"
   ```

    **Ctrl-X**、**Y**、**Enter** の順に押して、データを保存します。

4. Python スクリプトを実行します。 次のコマンドは、すべてのファイルがダウンロードされているディレクトリにいることが前提となっています。

    ```bash
    python show_recommendations.py 4 user-ratings.txt moviedb.txt recommendations.txt
    ```

    このコマンドは、ユーザー ID 4 に対して生成されたリコメンデーションを表示します。

   * **user-ratings.txt** ファイルを使用して、ユーザーが評価した映画を取得します。

   * **moviedb.txt** ファイルを使用して、映画の名前を取得します。

   * **recommendations.txt** を使用して、このユーザーの映画のリコメンデーションを取得します。

     このコマンドの出力は次のテキストのように表示されます。

       Seven Years in Tibet (1997), score=5.0   Indiana Jones and the Last Crusade (1989), score=5.0   Jaws (1975), score=5.0   Sense and Sensibility (1995), score=5.0   Independence Day (ID4) (1996), score=5.0   My Best Friend's Wedding (1997), score=5.0   Jerry Maguire (1996), score=5.0   Scream 2 (1997), score=5.0   Time to Kill, A (1996), score=5.0

## <a name="delete-temporary-data"></a>一時データを削除する

Mahout ジョブは、ジョブの処理中に作成された一時データを削除しません。 このサンプル ジョブでは `--tempDir` パラメーターを指定し、一時ファイルを特定のパスに分離して簡単に削除できるようにしています。 一時ファイルを削除するには、次のコマンドを使用します。

```bash
hdfs dfs -rm -f -r /temp/mahouttemp
```

> [!WARNING]  
> コマンドを再実行する場合、出力ディレクトリも削除する必要があります。 このディレクトリを削除するには、次を使用します。
>
> `hdfs dfs -rm -f -r /example/data/mahoutout`


## <a name="next-steps"></a>次の手順

ここまで、Mahout の使用方法を学習し、HDInsight でデータを操作するその他の方法を確認してきました。

* [HDInsight での Apache Hive の使用](hdinsight-use-hive.md)
* [HDInsight での Apache Pig の使用](hdinsight-use-pig.md)
* [HDInsight での MapReduce の使用](hdinsight-use-mapreduce.md)