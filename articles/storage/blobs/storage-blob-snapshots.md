---
title: "aaaCreate un instantané en lecture seule d’un objet blob dans le stockage Azure | Documents Microsoft"
description: "Découvrez comment toocreate un instantané d’un tooback d’objets blob des données blob à un moment donné dans le temps. Comprendre comment les instantanés sont facturés et toouse les frais de capacité toominimize."
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 3710705d-e127-4b01-8d0f-29853fb06d0d
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/11/2017
ms.author: marsma
ms.openlocfilehash: 57f2e76b8899b8a513688bf148dd13673141d5bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-blob-snapshot"></a>Création d’un instantané d’objet blob

Un instantané est une version en lecture seule d'un objet blob capturé à un instant donné. Les captures instantanées sont utiles pour la sauvegarde des objets blob. Une fois créé, un instantané peut être lu, copié ou supprimé, mais pas modifié.

Un instantané d’un objet blob est l’objet blob de base tooits identiques, à l’exception de cet objet blob hello URI a un **DateTime** valeur ajoutée temps hello toohello blob URI tooindicate à quels hello instantané a été pris. Par exemple, si une page d’objets blob URI est `http://storagesample.core.blob.windows.net/mydrives/myvhd`, hello instantané URI est trop similaire`http://storagesample.core.blob.windows.net/mydrives/myvhd?snapshot=2011-03-09T01:42:34.9360000Z`.

> [!NOTE]
> Tous les instantanés de partagent les URI hello base de l’objet blob. Hello seule distinction entre l’objet blob de base hello et instantané d’hello est hello ajouté **DateTime** valeur.
>

Un objet blob peut avoir plusieurs instantanés. Les instantanés sont conservés jusqu’à ce qu’ils soient explicitement supprimés. Un instantané ne peut pas être conservé plus longtemps que son objet blob de base. Vous pouvez énumérer les instantanés hello associés tootrack d’objet blob de base hello vos instantanés actuels.

Lorsque vous créez un instantané d’un objet blob, hello des propriétés de système de l’objet blob est des mêmes valeurs instantané toohello copiés avec hello. Hello base métadonnées d’objet blob sont également copié toohello snapshot, sauf si vous spécifiez des métadonnées distincts pour hello d’instantané lors de sa création.

Des baux associés d’objet blob de base hello n’affectent pas l’instantané d’hello. Vous ne pouvez pas acquérir de bail pour un instantané.

Un fichier de disque dur virtuel est utilisé toostore hello plus d’informations en cours et l’état d’un disque de machine virtuelle. Vous pouvez détacher un disque à partir de hello machine virtuelle ou arrêter hello machine virtuelle et puis prendre un instantané de son fichier de disque dur virtuel. Vous pouvez utiliser ce fichier de capture instantanée ultérieure tooretrieve hello disque dur virtuel du fichier à ce stade dans le temps et recréer hello machine virtuelle.

Si le chiffrement de Service de stockage (SSE) est activée pour le compte de stockage hello dans le hello blob réside, puis toutes les captures instantanées prises de cet objet blob seront chiffrées au repos.

## <a name="create-a-snapshot"></a>Créer un instantané
Hello exemple de code suivant montre comment un instantané à l’aide de toocreate hello [bibliothèque cliente de stockage Azure pour .NET](https://www.nuget.org/packages/WindowsAzure.Storage/). Cet exemple spécifie des métadonnées supplémentaires pour la capture instantanée de hello lors de sa création.

```csharp
private static async Task CreateBlockBlobSnapshot(CloudBlobContainer container)
{
    // Create a new block blob in hello container.
    CloudBlockBlob baseBlob = container.GetBlockBlobReference("sample-base-blob.txt");

    // Add blob metadata.
    baseBlob.Metadata.Add("ApproxBlobCreatedDate", DateTime.UtcNow.ToString());

    try
    {
        // Upload hello blob toocreate it, with its metadata.
        await baseBlob.UploadTextAsync(string.Format("Base blob: {0}", baseBlob.Uri.ToString()));

        // Sleep 5 seconds.
        System.Threading.Thread.Sleep(5000);

        // Create a snapshot of hello base blob.
        // Specify metadata at hello time that hello snapshot is created toospecify unique metadata for hello snapshot.
        // If no metadata is specified when hello snapshot is created, hello base blob's metadata is copied toohello snapshot.
        Dictionary<string, string> metadata = new Dictionary<string, string>();
        metadata.Add("ApproxSnapshotCreatedDate", DateTime.UtcNow.ToString());
        await baseBlob.CreateSnapshotAsync(metadata, null, null, null);
    }
    catch (StorageException e)
    {
        Console.WriteLine(e.Message);
        Console.ReadLine();
        throw;
    }
}
```

## <a name="copy-snapshots"></a>Copie d'instantanés
Les opérations de copie impliquant des objets blob et des instantanés respectent les règles suivantes :

* Vous pouvez copier un instantané sur son objet blob de base. En promouvant la position toohello instantané d’objet blob de base hello, vous pouvez restaurer une version antérieure d’un objet blob. Hello d’instantané est conservé, mais l’objet blob de base hello est remplacée par une copie accessible en écriture de l’instantané d’hello.
* Vous pouvez copier un objet blob de destination instantané tooa avec un nom différent. objet blob de destination qui en résulte Hello est un objet blob accessible en écriture et pas un instantané.
* Lorsqu’un objet blob source est copié, les instantanés de l’objet blob source de hello ne sont pas copiés toohello destination. Lorsqu’un objet blob de destination est remplacé par une copie, tous les instantanés associés d’objet blob de destination d’origine hello restent intacts.
* Lorsque vous créez un instantané d’un objet blob de blocs, liste des blocs validés de l’objet blob de hello est également copié toohello instantané. Les blocs non validés ne sont pas copiés.

## <a name="specify-an-access-condition"></a>Spécification d'une condition d'accès
Lorsque vous appelez [CreateSnapshotAsync][dotnet_CreateSnapshotAsync], vous pouvez spécifier une condition d’accès afin que hello instantané est créé uniquement si une condition est remplie. toospecify une condition d’accès, utilisez hello [AccessCondition] [ dotnet_AccessCondition] paramètre. Si hello spécifié la condition n’est pas remplie, hello instantané n’est créé et hello service Blob retourne le code d’état [HTTPStatusCode][dotnet_HTTPStatusCode]. Ne.

## <a name="delete-snapshots"></a>Suppression d'instantanés
Impossible de supprimer un objet blob avec des instantanés, sauf si hello instantanés sont également supprimés. Vous pouvez supprimer un instantané individuel, ou spécifier que toutes les captures instantanées supprimée lorsque l’objet blob source de hello est supprimé. Si vous essayez de toodelete un objet blob qui a toujours des captures instantanées, une erreur se produit.

Hello suivant exemple de code montre comment toodelete un objet blob et ses instantanés dans .NET, où `blockBlob` est un objet de type [CloudBlockBlob][dotnet_CloudBlockBlob]:

```csharp
await blockBlob.DeleteIfExistsAsync(DeleteSnapshotsOption.IncludeSnapshots, null, null, null);
```

## <a name="snapshots-with-azure-premium-storage"></a>Instantanés avec Azure Premium Storage
Lors de l’utilisation des instantanés de stockage Premium, hello suivant les règles s’appliquent :

* nombre maximal de Hello d’instantanés par l’objet blob de pages dans un compte de stockage premium est 100. Si cette limite est dépassée, hello opération Snapshot Blob renvoie le code d’erreur 409 (`SnapshotCountExceeded`).
* Vous pouvez prendre un instantané d’un objet blob de pages dans un compte de stockage premium toutes les 10 minutes. Si ce taux est dépassé, hello opération Snapshot Blob renvoie le code d’erreur 409 (`SnapshotOperationRateExceeded`).
* tooread un instantané, vous pouvez utiliser toocopy opération de copie d’objets Blob hello objet blob de pages tooanother instantané dans le compte de hello. objet blob de destination Hello pour l’opération de copie hello ne doit pas avoir tous les instantanés existants. Si le blob de destination hello ne dispose pas des captures instantanées, puis hello opération Copy Blob renvoie le code d’erreur 409 (`SnapshotsPresent`).

## <a name="return-hello-absolute-uri-tooa-snapshot"></a>Instantané tooa URI absolu de retour hello
Cet exemple de code c# crée une capture instantanée et écrit hello URI absolu pour l’emplacement principal de hello.

```csharp
//Create hello blob service client object.
const string ConnectionString = "DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key";

CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConnectionString);
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

//Get a reference tooa container.
CloudBlobContainer container = blobClient.GetContainerReference("sample-container");
container.CreateIfNotExists();

//Get a reference tooa blob.
CloudBlockBlob blob = container.GetBlockBlobReference("sampleblob.txt");
blob.UploadText("This is a blob.");

//Create a snapshot of hello blob and write out its primary URI.
CloudBlockBlob blobSnapshot = blob.CreateSnapshot();
Console.WriteLine(blobSnapshot.SnapshotQualifiedStorageUri.PrimaryUri);
```

## <a name="understand-how-snapshots-accrue-charges"></a>Présentation des frais liés aux instantanés
Création d’un instantané, qui est une copie en lecture seule d’un objet blob, peut entraîner un compte de tooyour de frais de stockage des données supplémentaires. Lorsque vous concevez votre application, il est important toobe prenant en charge de la façon dont ces frais peuvent accumuler afin que vous pouvez réduire les coûts.

### <a name="important-billing-considerations"></a>Considérations importantes relatives à la facturation
Hello suivant liste inclut les points clés tooconsider lors de la création d’un instantané.

* Votre compte de stockage entraîne des frais pour les blocs uniques ou des pages, qu’ils soient dans l’objet blob de hello ou hello instantané. Votre compte n’entraîne pas de frais supplémentaires pour les instantanés associés à un objet blob jusqu'à ce que vous mettez à jour blob hello sur lequel ils sont basés. Une fois que vous mettez à jour d’objet blob de base hello, il diffère de ses instantanés. Dans ce cas, vous êtes facturé pour hello blocs ou pages uniques dans chaque objet blob ou un instantané.
* Quand vous remplacez un bloc au sein d’un objet blob de bloc, ce bloc est ensuite facturé comme un bloc unique. Cela est vrai même si le bloc de hello a hello même ID de bloc et hello même des données tel qu’il est dans l’instantané d’hello. Une fois que le bloc de hello est validée, elle diffère de son homologue dans tous les instantanés et vous serez facturé pour ses données. Hello que va de même pour une page dans un objet blob de pages est mis à jour avec des données identiques.
* Remplacement d’un objet blob de blocs en appelant hello [UploadFromFile][dotnet_UploadFromFile], [UploadText][dotnet_UploadText], [UploadFromStream] [ dotnet_UploadFromStream], ou [UploadFromByteArray] [ dotnet_UploadFromByteArray] méthode remplace tous les blocs dans l’objet blob de hello. Si vous disposez d’un instantané associé à cet objet blob, tous les blocs dans l’objet blob de base hello et instantané différents, et vous serez facturé pour tous les blocs hello dans les deux objets BLOB. Cela est vrai même si les données de salutation dans l’objet blob de base hello et l’instantané hello restent identiques.
* Hello service Blob Azure n’est pas un toodetermine signifie que si deux blocs contiennent des données identiques. Chaque bloc est téléchargé et validé est traité comme uniques, même si elle a hello des mêmes données et hello même bloquer le code. Les coûts pour les blocs uniques, il est important tooconsider, entraînant la mise à jour d’un objet blob qui a un instantané dans les blocs uniques supplémentaires et des frais supplémentaires.

### <a name="minimize-cost-with-snapshot-management"></a>Réduire les coûts grâce à la gestion des captures instantanées

Nous vous recommandons de la gestion de vos instantanés avec précaution tooavoid des frais supplémentaires. Vous pouvez suivre ces meilleures pratiques toohelp réduire les coûts de hello induites par le stockage de vos instantanés hello :

* Supprimer et recréer les instantanés associés à un objet blob lorsque vous mettez à jour les objets blob hello, même si vous mettez à jour avec des données identiques, sauf si la conception de votre application nécessite que vous conservez des instantanés. En supprimant et en recréant les instantanés de l’objet blob de hello, vous pouvez vous assurer que les instantanés et les objets blob de hello divergences.
* Si vous gardez les instantanés d’un objet blob, évitez d’appeler [UploadFromFile][dotnet_UploadFromFile], [UploadText][dotnet_UploadText], [ UploadFromStream][dotnet_UploadFromStream], ou [UploadFromByteArray] [ dotnet_UploadFromByteArray] objet blob de tooupdate hello. Ces méthodes remplacent tous les blocs hello dans l’objet blob de hello, à l’origine de votre objet blob de base et ses toodiverge instantanés considérablement. Au lieu de cela, les mises à jour hello plus petit nombre possible de blocs à l’aide de hello [PutBlock] [ dotnet_PutBlock] et [PutBlockList] [ dotnet_PutBlockList] méthodes.

### <a name="snapshot-billing-scenarios"></a>Scénarios de facturation d’instantanés
Hello les scénarios suivants illustrent l’augmentation des coûts pour un objet blob de blocs et de ses instantanés.

**Scénario 1**

Dans le scénario 1, objet blob de base hello n'a pas été mis à jour une fois l’instantané hello, frais sont donc calculés uniquement pour les blocs uniques 1, 2 et 3.

![Ressources Azure Storage](./media/storage-blob-snapshots/storage-blob-snapshots-billing-scenario-1.png)

**Scénario 2**

Dans le scénario 2, objet blob de base hello a été mis à jour, mais les instantanés hello ne sont pas. Le bloc 3 a été mis à jour et bien qu’il contienne hello les mêmes données et hello même ID, il est non hello même bloc 3 de l’instantané d’hello. Par conséquent, le compte de hello est facturé pour quatre blocs.

![Ressources Azure Storage](./media/storage-blob-snapshots/storage-blob-snapshots-billing-scenario-2.png)

**Scénario 3**

Dans le scénario 3, objet blob de base hello a été mis à jour, mais les instantanés hello ne sont pas. Le bloc 3 a été remplacé par le bloc 4 dans l’objet blob de base hello, mais l’instantané d’hello reflète toujours le bloc 3. Par conséquent, le compte de hello est facturé pour quatre blocs.

![Ressources Azure Storage](./media/storage-blob-snapshots/storage-blob-snapshots-billing-scenario-3.png)

**Scénario 4**

Dans le scénario 4, objet blob de base hello a été complètement mis à jour et ne contient aucun de ses blocs d’origine. Par conséquent, compte de hello est facturé pour toutes les huit blocs uniques. Ce scénario peut se produire si vous utilisez une méthode de mise à jour comme [UploadFromFile][dotnet_UploadFromFile], [UploadText][dotnet_UploadText], [ UploadFromStream][dotnet_UploadFromStream], ou [UploadFromByteArray][dotnet_UploadFromByteArray], car ces méthodes remplacent tout contenu hello d’un objet blob.

![Ressources Azure Storage](./media/storage-blob-snapshots/storage-blob-snapshots-billing-scenario-4.png)

## <a name="next-steps"></a>Étapes suivantes

* Vous trouverez plus d’informations sur l’utilisation des captures instantanées de disque de machine virtuelle (VM) dans [Sauvegarder les disques de machines virtuelles Azure non gérés avec des captures instantanées incrémentielles](../../virtual-machines/windows/incremental-snapshots.md)

* Pour obtenir des exemples de code supplémentaires d’utilisation du Stockage Blob, consultez [Exemples de code Azure](https://azure.microsoft.com/documentation/samples/?service=storage&term=blob). Vous pouvez télécharger un exemple d’application et exécutez-le ou parcourir le code hello sur GitHub.

[dotnet_AccessCondition]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.accesscondition.aspx
[dotnet_CloudBlockBlob]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblockblob.aspx
[dotnet_CreateSnapshotAsync]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblockblob.createsnapshotasync.aspx
[dotnet_HTTPStatusCode]: https://msdn.microsoft.com/library/system.net.httpstatuscode(v=vs.110).aspx
[dotnet_PutBlockList]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblockblob.putblocklist.aspx
[dotnet_PutBlock]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblockblob.putblock.aspx
[dotnet_UploadFromByteArray]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblockblob.uploadfrombytearray.aspx
[dotnet_UploadFromFile]: https://msdn.microsoft.com/library/azure/mt705654.aspx
[dotnet_UploadFromStream]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblockblob.uploadfromstream.aspx
[dotnet_UploadText]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblockblob.uploadtext.aspx