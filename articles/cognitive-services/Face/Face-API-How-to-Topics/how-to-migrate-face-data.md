---
title: サブスクリプション間で顔データを移行する - Face API
titleSuffix: Azure Cognitive Services
description: このガイドでは、保存した顔データをある Face API サブスクリプションから別の Face API サブスクリプションに移行する方法について説明します。
services: cognitive-services
author: lewlu
manager: cgronlun
ms.service: cognitive-services
ms.subservice: face-api
ms.topic: conceptual
ms.date: 02/01/2019
ms.author: lewlu
ms.openlocfilehash: 702aed12860c090e83b997e6b56d56e06b416568
ms.sourcegitcommit: 67625c53d466c7b04993e995a0d5f87acf7da121
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/20/2019
ms.locfileid: "65913796"
---
# <a name="migrate-your-face-data-to-a-different-face-subscription"></a>顔データを別の Face サブスクリプションに移行する

このガイドでは、顔データ (顔と一緒に保存したPersonGroup オブジェクトなど) を別の Azure Cognitive Services Face API サブスクリプションに移動する方法について説明します。 データを移動するには、スナップショット機能を使用します。 これにより、運用を移行または拡張するときに、PersonGroup または FaceList オブジェクトを繰り返し構築およびトレーニングする必要がなくなります。 たとえば、無料試用版サブスクリプションを使用して PersonGroup オブジェクトを作成し、それを有料サブスクリプションに移行することが必要になる場合があります。 または、大規模なエンタープライズ運用のためにリージョン間で顔データを同期することが必要な場合もあります。

この同じ移行戦略は、LargePersonGroup オブジェクトと LargeFaceList オブジェクトにも適用されます。 このガイドの概念についてよくわからない場合は、「[顔認識の概念](../concepts/face-recognition.md)」ガイドにあるそれらの定義を参照してください。 このガイドでは、C# と共に Face API .NET クライアント ライブラリを使用しています。

## <a name="prerequisites"></a>前提条件

次のものが必要です。

- 2 つの Face API サブスクリプション キー (1 つは既存のデータがあり、もう 1 つは移行先)。 Face API サービスをサブスクライブし、キーを取得するには、[Cognitive Services アカウントの作成](https://docs.microsoft.com/azure/cognitive-services/cognitive-services-apis-create-account)に関するページの手順に従ってください。
- ターゲット サブスクリプションに対応する Face API サブスクリプション ID の文字列。 これを見つけるには、Azure portal で **[概要]** を選択します。 
- [Visual Studio 2015 または 2017](https://www.visualstudio.com/downloads/) の任意のエディション。

## <a name="create-the-visual-studio-project"></a>Visual Studio プロジェクトの作成

このガイドでは、顔データの移行を実行するために簡単なコンソール アプリを使用します。 完全な実装については、GitHub の [Face API のスナップショット サンプル](https://github.com/Azure-Samples/cognitive-services-dotnet-sdk-samples/tree/master/app-samples/FaceApiSnapshotSample/FaceApiSnapshotSample)に関するページを参照してください。

1. Visual Studio で、新しいコンソール アプリ .NET Framework プロジェクトを作成します。 これに **FaceApiSnapshotSample** という名前を付けます。
1. 必須の NuGet パッケージを入手します。 ソリューション エクスプローラーで目的のプロジェクトを右クリックし、 **[NuGet パッケージの管理]** を選択します。 **[参照]** タブを選択し、 **[プレリリースを含める]** を選択します。 次のパッケージを検索してインストールします。
    - [Microsoft.Azure.CognitiveServices.Vision.Face 2.3.0-preview](https://www.nuget.org/packages/Microsoft.Azure.CognitiveServices.Vision.Face/2.2.0-preview)

## <a name="create-face-clients"></a>顔クライアントを作成する

*Program.cs* の **Main** メソッドで、ソース サブスクリプション用とターゲット サブスクリプション用の 2 つの [FaceClient](https://docs.microsoft.com/dotnet/api/microsoft.azure.cognitiveservices.vision.face.faceclient?view=azure-dotnet) インスタンスを作成します。 この例では、東アジア リージョンの Face サブスクリプションをソースとして使用し、米国西部サブスクリプションをターゲットとして使用します。 この例で、Azure リージョン間でデータを移行する方法について説明します。 サブスクリプションが異なるリージョンにある場合は、`Endpoint` 文字列を変更してください。

```csharp
var FaceClientEastAsia = new FaceClient(new ApiKeyServiceClientCredentials("<East Asia Subscription Key>"))
    {
        Endpoint = "https://southeastasia.api.cognitive.microsoft.com/>"
    };

var FaceClientWestUS = new FaceClient(new ApiKeyServiceClientCredentials("<West US Subscription Key>"))
    {
        Endpoint = "https://westus.api.cognitive.microsoft.com/"
    };
```

ソース サブスクリプションとターゲット サブスクリプションのサブスクリプション キー値とエンドポイント URL を入力します。


## <a name="prepare-a-persongroup-for-migration"></a>移行のために PersonGroup を準備する

ターゲット サブスクリプションに移行するには、ソース サブスクリプションの PersonGroup の ID が必要です。 PersonGroup オブジェクトの一覧を取得するには、[PersonGroupOperationsExtensions.ListAsync](https://docs.microsoft.com/dotnet/api/microsoft.azure.cognitiveservices.vision.face.persongroupoperationsextensions.listasync?view=azure-dotnet) メソッドを使用します。 次に、[PersonGroup.PersonGroupId](https://docs.microsoft.com/dotnet/api/microsoft.azure.cognitiveservices.vision.face.models.persongroup.persongroupid?view=azure-dotnet#Microsoft_Azure_CognitiveServices_Vision_Face_Models_PersonGroup_PersonGroupId) プロパティを取得します。 このプロセスは、実際の PersonGroup オブジェクトによって変わります。 このガイドでは、ソースの PersonGroup ID は `personGroupId` に格納されます。

> [!NOTE]
> [サンプル コード](https://github.com/Azure-Samples/cognitive-services-dotnet-sdk-samples/tree/master/app-samples/FaceApiSnapshotSample/FaceApiSnapshotSample)は、移行する新しい PersonGroup を作成してトレーニングします。 ほとんどの場合は、使用する PersonGroup が既に存在するはずです。

## <a name="take-a-snapshot-of-a-persongroup"></a>PersonGroup のスナップショットを作成する

スナップショットは、特定の Face データ型のための一時的なリモート ストレージです。 これは、あるサブスクリプションから別のサブスクリプションにデータをコピーするための一種のクリップボードとして機能します。 最初に、ソース サブスクリプション内のデータのスナップショットを作成します。 次に、これをターゲット サブスクリプション内の新しいデータ オブジェクトに適用します。

ソース サブスクリプションの FaceClient インスタンスを使用して、PersonGroup のスナップショットを作成します。 PersonGroup ID とターゲット サブスクリプションの ID を指定して [TakeAsync](https://docs.microsoft.com/dotnet/api/microsoft.azure.cognitiveservices.vision.face.snapshotoperationsextensions.takeasync?view=azure-dotnet) を使用します。 複数のターゲット サブスクリプションがある場合は、それらを 3 つ目のパラメーターで配列エントリとして追加します。

```csharp
var takeSnapshotResult = await FaceClientEastAsia.Snapshot.TakeAsync(
    SnapshotObjectType.PersonGroup,
    personGroupId,
    new[] { "<Azure West US Subscription ID>" /* Put other IDs here, if multiple target subscriptions wanted */ });
```

> [!NOTE]
> スナップショットを作成して適用するプロセスで、ソースまたはターゲットの PersonGroup または FaceList への通常の呼び出しが中断されることはありません。 ソース オブジェクトを変更する複数の呼び出し (たとえば、[FaceList 管理の呼び出し](https://docs.microsoft.com/dotnet/api/microsoft.azure.cognitiveservices.vision.face.facelistoperations?view=azure-dotnet)や [PersonGroup トレーニング](https://docs.microsoft.com/dotnet/api/microsoft.azure.cognitiveservices.vision.face.persongroupoperations?view=azure-dotnet)の呼び出しなど) を同時に行わないでください。 スナップショット操作がそれらの操作の前または後に実行されたり、エラーが発生したりする可能性があります。

## <a name="retrieve-the-snapshot-id"></a>スナップショット ID を取得する

スナップショットを作成するために使用するメソッドは非同期であるため、その完了を待つ必要があります。 スナップショットの操作を取り消すことはできません。 このコードで、`WaitForOperation` メソッドは非同期呼び出しを監視します。 これは 100 ミリ秒ごとに状態を確認します。 操作が完了したら、`OperationLocation` フィールドを解析して操作 ID を取得します。 

```csharp
var takeOperationId = Guid.Parse(takeSnapshotResult.OperationLocation.Split('/')[2]);
var operationStatus = await WaitForOperation(FaceClientEastAsia, takeOperationId);
```

一般的な `OperationLocation` の値は次のようになります。

```csharp
"/operations/a63a3bdd-a1db-4d05-87b8-dbad6850062a"
```

`WaitForOperation` ヘルパー メソッドは次のとおりです。

```csharp
/// <summary>
/// Waits for the take/apply operation to complete and returns the final operation status.
/// </summary>
/// <returns>The final operation status.</returns>
private static async Task<OperationStatus> WaitForOperation(IFaceClient client, Guid operationId)
{
    OperationStatus operationStatus = null;
    do
    {
        if (operationStatus != null)
        {
            Thread.Sleep(TimeSpan.FromMilliseconds(100));
        }

        // Get the status of the operation.
        operationStatus = await client.Snapshot.GetOperationStatusAsync(operationId);

        Console.WriteLine($"Operation Status: {operationStatus.Status}");
    }
    while (operationStatus.Status != OperationStatusType.Succeeded
            && operationStatus.Status != OperationStatusType.Failed);

    return operationStatus;
}
```

操作状態が `Succeeded` と表示されたら、返された OperationStatus インスタンスの `ResourceLocation` フィールドを解析してスナップショット ID を取得します。

```csharp
var snapshotId = Guid.Parse(operationStatus.ResourceLocation.Split('/')[2]);
```

一般的な `resourceLocation` の値は次のようになります。

```csharp
"/snapshots/e58b3f08-1e8b-4165-81df-aa9858f233dc"
```

## <a name="apply-a-snapshot-to-a-target-subscription"></a>ターゲット サブスクリプションにスナップショットを適用する

次に、ランダムに生成された ID を使用して、ターゲット サブスクリプションに新しい PersonGroup を作成します。 その後、ターゲット サブスクリプションの FaceClient インスタンスを使用して、スナップショットをこの PersonGroup に適用します。 スナップショット ID と新しい PersonGroup ID を渡します。

```csharp
var newPersonGroupId = Guid.NewGuid().ToString();
var applySnapshotResult = await FaceClientWestUS.Snapshot.ApplyAsync(snapshotId, newPersonGroupId);
```


> [!NOTE]
> Snapshot オブジェクトは 48 時間のみ有効です。 スナップショットは、すぐにデータ移行に使用する予定がある場合にのみ作成してください。

スナップショットの適用要求で、別の操作 ID が返されます。 この ID を取得するには、返された applySnapshotResult インスタンスの `OperationLocation` フィールドを解析します。 

```csharp
var applyOperationId = Guid.Parse(applySnapshotResult.OperationLocation.Split('/')[2]);
```

スナップショットの適用プロセスも非同期なので、この場合も `WaitForOperation` を使用して完了するまで待ちます。

```csharp
operationStatus = await WaitForOperation(FaceClientWestUS, applyOperationId);
```

## <a name="test-the-data-migration"></a>データ移行をテストする

スナップショットを適用すると、ターゲット サブスクリプションの新しい PersonGroup に元の顔データが設定されます。 既定では、トレーニングの結果もコピーされます。 新しい PersonGroup は、再トレーニングを実行しなくても顔識別の呼び出しに対する準備ができています。

データ移行をテストするには、以下の操作を実行し、コンソールに出力された結果を比較します。

```csharp
await DisplayPersonGroup(FaceClientEastAsia, personGroupId);
await IdentifyInPersonGroup(FaceClientEastAsia, personGroupId);

await DisplayPersonGroup(FaceClientWestUS, newPersonGroupId);
// No need to retrain the person group before identification,
// training results are copied by snapshot as well.
await IdentifyInPersonGroup(FaceClientWestUS, newPersonGroupId);
```

以下のヘルパー メソッドを使用します。

```csharp
private static async Task DisplayPersonGroup(IFaceClient client, string personGroupId)
{
    var personGroup = await client.PersonGroup.GetAsync(personGroupId);
    Console.WriteLine("Person Group:");
    Console.WriteLine(JsonConvert.SerializeObject(personGroup));

    // List persons.
    var persons = await client.PersonGroupPerson.ListAsync(personGroupId);

    foreach (var person in persons)
    {
        Console.WriteLine(JsonConvert.SerializeObject(person));
    }

    Console.WriteLine();
}
```

```csharp
private static async Task IdentifyInPersonGroup(IFaceClient client, string personGroupId)
{
    using (var fileStream = new FileStream("data\\PersonGroup\\Daughter\\Daughter1.jpg", FileMode.Open, FileAccess.Read))
    {
        var detectedFaces = await client.Face.DetectWithStreamAsync(fileStream);

        var result = await client.Face.IdentifyAsync(detectedFaces.Select(face => face.FaceId.Value).ToList(), personGroupId);
        Console.WriteLine("Test identify against PersonGroup");
        Console.WriteLine(JsonConvert.SerializeObject(result));
        Console.WriteLine();
    }
}
```

これで、ターゲット サブスクリプションで新しい PersonGroup を使用できるようになります。 

今後ターゲットの PersonGroup を改めて更新するには、スナップショットを受け取るために新しい PersonGroup を作成します。 これを行うには、このガイドの手順に従います。 1 つの PersonGroup オブジェクトには 1 つのスナップショットを 1 回のみ適用できます。

## <a name="clean-up-resources"></a>リソースのクリーンアップ

顔データの移行が完了したら、スナップショット オブジェクトを手動で削除します。

```csharp
await FaceClientEastAsia.Snapshot.DeleteAsync(snapshotId);
```

## <a name="next-steps"></a>次の手順

次に、関連する API リファレンス ドキュメントを参照するか、スナップショット機能を使用するサンプル アプリを調べるか、またはハウツー ガイドに従って、ここで説明されているその他の API 操作の使用を開始してください。

- [スナップショット リファレンス ドキュメント (.NET SDK)](https://docs.microsoft.com/dotnet/api/microsoft.azure.cognitiveservices.vision.face.snapshotoperations?view=azure-dotnet)
- [Face API のスナップショット サンプル](https://github.com/Azure-Samples/cognitive-services-dotnet-sdk-samples/tree/master/app-samples/FaceApiSnapshotSample/FaceApiSnapshotSample)
- [顔を追加する](how-to-add-faces.md)
- [画像内の顔を検出する](HowtoDetectFacesinImage.md)
- [画像内の顔を識別する](HowtoIdentifyFacesinImage.md)
