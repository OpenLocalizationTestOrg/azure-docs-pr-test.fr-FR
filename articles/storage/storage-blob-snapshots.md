---
title: "Création d’un instantané en lecture seule d’un objet blob dans le stockage Azure | Microsoft Docs"
description: "Apprenez à créer un instantané d’un objet blob pour sauvegarder ses données à un moment donné. Découvrez comment les instantanés sont facturés et comment les utiliser pour réduire les frais de capacité."
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
ms.openlocfilehash: 6ebb77f4ec5f1887e5c55bf1c8c64224a9233654
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-blob-snapshot"></a><span data-ttu-id="a0a71-104">Création d’un instantané d’objet blob</span><span class="sxs-lookup"><span data-stu-id="a0a71-104">Create a blob snapshot</span></span>

<span data-ttu-id="a0a71-105">Un instantané est une version en lecture seule d'un objet blob capturé à un instant donné.</span><span class="sxs-lookup"><span data-stu-id="a0a71-105">A snapshot is a read-only version of a blob that's taken at a point in time.</span></span> <span data-ttu-id="a0a71-106">Les captures instantanées sont utiles pour la sauvegarde des objets blob.</span><span class="sxs-lookup"><span data-stu-id="a0a71-106">Snapshots are useful for backing up blobs.</span></span> <span data-ttu-id="a0a71-107">Une fois créé, un instantané peut être lu, copié ou supprimé, mais pas modifié.</span><span class="sxs-lookup"><span data-stu-id="a0a71-107">After you create a snapshot, you can read, copy, or delete it, but you cannot modify it.</span></span>

<span data-ttu-id="a0a71-108">Un instantané d’un objet blob est identique à l’objet blob de base, à la différence que l’URI de l’objet blob a une valeur **DateTime** à la fin qui indique l’heure à laquelle l’instantané a été pris.</span><span class="sxs-lookup"><span data-stu-id="a0a71-108">A snapshot of a blob is identical to its base blob, except that the blob URI has a **DateTime** value appended to the blob URI to indicate the time at which the snapshot was taken.</span></span> <span data-ttu-id="a0a71-109">Par exemple, si l’URI de l’objet blob de pages est `http://storagesample.core.blob.windows.net/mydrives/myvhd`, l’URI de l’instantané est du type `http://storagesample.core.blob.windows.net/mydrives/myvhd?snapshot=2011-03-09T01:42:34.9360000Z`.</span><span class="sxs-lookup"><span data-stu-id="a0a71-109">For example, if a page blob URI is `http://storagesample.core.blob.windows.net/mydrives/myvhd`, the snapshot URI is similar to `http://storagesample.core.blob.windows.net/mydrives/myvhd?snapshot=2011-03-09T01:42:34.9360000Z`.</span></span>

> [!NOTE]
> <span data-ttu-id="a0a71-110">Tous les instantanés partagent l’URI de l’objet blob de base.</span><span class="sxs-lookup"><span data-stu-id="a0a71-110">All snapshots share the base blob's URI.</span></span> <span data-ttu-id="a0a71-111">La seule distinction entre l’objet blob de base et l’instantané est la valeur **DateTime** ajoutée à la fin.</span><span class="sxs-lookup"><span data-stu-id="a0a71-111">The only distinction between the base blob and the snapshot is the appended **DateTime** value.</span></span>
>

<span data-ttu-id="a0a71-112">Un objet blob peut avoir plusieurs instantanés.</span><span class="sxs-lookup"><span data-stu-id="a0a71-112">A blob can have any number of snapshots.</span></span> <span data-ttu-id="a0a71-113">Les instantanés sont conservés jusqu’à ce qu’ils soient explicitement supprimés.</span><span class="sxs-lookup"><span data-stu-id="a0a71-113">Snapshots persist until they are explicitly deleted.</span></span> <span data-ttu-id="a0a71-114">Un instantané ne peut pas être conservé plus longtemps que son objet blob de base.</span><span class="sxs-lookup"><span data-stu-id="a0a71-114">A snapshot cannot outlive its base blob.</span></span> <span data-ttu-id="a0a71-115">Vous pouvez énumérer les instantanés associés à l’objet blob de base pour effectuer le suivi de vos instantanés actuels.</span><span class="sxs-lookup"><span data-stu-id="a0a71-115">You can enumerate the snapshots associated with the base blob to track your current snapshots.</span></span>

<span data-ttu-id="a0a71-116">Lorsque vous créez un instantané d’un objet blob, les propriétés système de l’objet blob sont copiées dans l’instantané avec les mêmes valeurs.</span><span class="sxs-lookup"><span data-stu-id="a0a71-116">When you create a snapshot of a blob, the blob's system properties are copied to the snapshot with the same values.</span></span> <span data-ttu-id="a0a71-117">Les métadonnées de l’objet blob de base sont également copiées dans l’instantané, sauf si vous spécifiez des métadonnées distinctes pour l’instantané lorsque vous le créez.</span><span class="sxs-lookup"><span data-stu-id="a0a71-117">The base blob's metadata is also copied to the snapshot, unless you specify separate metadata for the snapshot when you create it.</span></span>

<span data-ttu-id="a0a71-118">Aucun bail associé à l’objet blob de base n’a d’incidence sur l’instantané.</span><span class="sxs-lookup"><span data-stu-id="a0a71-118">Any leases associated with the base blob do not affect the snapshot.</span></span> <span data-ttu-id="a0a71-119">Vous ne pouvez pas acquérir de bail pour un instantané.</span><span class="sxs-lookup"><span data-stu-id="a0a71-119">You cannot acquire a lease on a snapshot.</span></span>

<span data-ttu-id="a0a71-120">Un fichier de disque dur virtuel est utilisé pour stocker les informations et l’état actuels d’un disque de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="a0a71-120">A VHD file is used to store the current information and status for a VM disk.</span></span> <span data-ttu-id="a0a71-121">Vous pouvez détacher un disque de la machine virtuelle ou arrêter la machine virtuelle, puis prendre une capture instantanée de son fichier de disque dur virtuel.</span><span class="sxs-lookup"><span data-stu-id="a0a71-121">You can detach a disk from within the VM or shut down the VM, and then take a snapshot of its VHD file.</span></span> <span data-ttu-id="a0a71-122">Vous pourrez par la suite utiliser ce fichier de capture instantanée pour récupérer le fichier de disque dur virtuel à ce moment précis et recréer la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="a0a71-122">You can use that snapshot file later to retrieve the VHD file at that point in time and recreate the VM.</span></span>

<span data-ttu-id="a0a71-123">Si le chiffrement du service de stockage (SSE) est activé pour le compte de stockage dans lequel réside l’objet blob, toutes les captures instantanées de cet objet blob seront chiffrées au repos.</span><span class="sxs-lookup"><span data-stu-id="a0a71-123">If Storage Service Encryption (SSE) is enabled for the storage account in which the blob resides, then any snapshots taken of that blob will be encrypted at rest.</span></span>

## <a name="create-a-snapshot"></a><span data-ttu-id="a0a71-124">Créer un instantané</span><span class="sxs-lookup"><span data-stu-id="a0a71-124">Create a snapshot</span></span>
<span data-ttu-id="a0a71-125">L’exemple de code suivant montre comment créer une capture instantanée à l’aide de la [bibliothèque cliente de stockage Azure pour .NET](https://www.nuget.org/packages/WindowsAzure.Storage/).</span><span class="sxs-lookup"><span data-stu-id="a0a71-125">The following code example shows how to create a snapshot by using the [Azure Storage Client Library for .NET](https://www.nuget.org/packages/WindowsAzure.Storage/).</span></span> <span data-ttu-id="a0a71-126">Cet exemple spécifie des métadonnées supplémentaires pour la capture instantanée lors de sa création.</span><span class="sxs-lookup"><span data-stu-id="a0a71-126">This example specifies additional metadata for the snapshot when it is created.</span></span>

```csharp
private static async Task CreateBlockBlobSnapshot(CloudBlobContainer container)
{
    // Create a new block blob in the container.
    CloudBlockBlob baseBlob = container.GetBlockBlobReference("sample-base-blob.txt");

    // Add blob metadata.
    baseBlob.Metadata.Add("ApproxBlobCreatedDate", DateTime.UtcNow.ToString());

    try
    {
        // Upload the blob to create it, with its metadata.
        await baseBlob.UploadTextAsync(string.Format("Base blob: {0}", baseBlob.Uri.ToString()));

        // Sleep 5 seconds.
        System.Threading.Thread.Sleep(5000);

        // Create a snapshot of the base blob.
        // Specify metadata at the time that the snapshot is created to specify unique metadata for the snapshot.
        // If no metadata is specified when the snapshot is created, the base blob's metadata is copied to the snapshot.
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

## <a name="copy-snapshots"></a><span data-ttu-id="a0a71-127">Copie d'instantanés</span><span class="sxs-lookup"><span data-stu-id="a0a71-127">Copy snapshots</span></span>
<span data-ttu-id="a0a71-128">Les opérations de copie impliquant des objets blob et des instantanés respectent les règles suivantes :</span><span class="sxs-lookup"><span data-stu-id="a0a71-128">Copy operations involving blobs and snapshots follow these rules:</span></span>

* <span data-ttu-id="a0a71-129">Vous pouvez copier un instantané sur son objet blob de base.</span><span class="sxs-lookup"><span data-stu-id="a0a71-129">You can copy a snapshot over its base blob.</span></span> <span data-ttu-id="a0a71-130">En plaçant un instantané à la place d'un objet blob de base, vous pouvez restaurer une version antérieure de l’objet blob.</span><span class="sxs-lookup"><span data-stu-id="a0a71-130">By promoting a snapshot to the position of the base blob, you can restore an earlier version of a blob.</span></span> <span data-ttu-id="a0a71-131">L’instantané est conservé, mais l’objet blob de base est remplacé par une copie accessible en écriture de l’instantané.</span><span class="sxs-lookup"><span data-stu-id="a0a71-131">The snapshot remains, but the base blob is overwritten with a writable copy of the snapshot.</span></span>
* <span data-ttu-id="a0a71-132">Vous pouvez copier un instantané sur un objet blob de destination avec un nom différent.</span><span class="sxs-lookup"><span data-stu-id="a0a71-132">You can copy a snapshot to a destination blob with a different name.</span></span> <span data-ttu-id="a0a71-133">L’objet blob de destination qui en découle est modifiable et n’est pas un instantané.</span><span class="sxs-lookup"><span data-stu-id="a0a71-133">The resulting destination blob is a writable blob and not a snapshot.</span></span>
* <span data-ttu-id="a0a71-134">Quand un objet blob source est copié, ses instantanés ne sont pas copiés dans la destination.</span><span class="sxs-lookup"><span data-stu-id="a0a71-134">When a source blob is copied, any snapshots of the source blob are not copied to the destination.</span></span> <span data-ttu-id="a0a71-135">Quand un objet blob de destination est remplacé par une copie, tous les instantanés associés à l’objet blob de destination d’origine restent intacts.</span><span class="sxs-lookup"><span data-stu-id="a0a71-135">When a destination blob is overwritten with a copy, any snapshots associated with the original destination blob remain intact.</span></span>
* <span data-ttu-id="a0a71-136">Quand vous créez un instantané d'un objet blob de blocs, la liste des blocs validés de l'objet blob est également copiée dans l'instantané.</span><span class="sxs-lookup"><span data-stu-id="a0a71-136">When you create a snapshot of a block blob, the blob's committed block list is also copied to the snapshot.</span></span> <span data-ttu-id="a0a71-137">Les blocs non validés ne sont pas copiés.</span><span class="sxs-lookup"><span data-stu-id="a0a71-137">Any uncommitted blocks are not copied.</span></span>

## <a name="specify-an-access-condition"></a><span data-ttu-id="a0a71-138">Spécification d'une condition d'accès</span><span class="sxs-lookup"><span data-stu-id="a0a71-138">Specify an access condition</span></span>
<span data-ttu-id="a0a71-139">Lorsque vous appelez [CreateSnapshotAsync][dotnet_CreateSnapshotAsync], vous pouvez spécifier une condition d’accès pour que la capture instantanée ne soit créée que si la condition est remplie.</span><span class="sxs-lookup"><span data-stu-id="a0a71-139">When you call [CreateSnapshotAsync][dotnet_CreateSnapshotAsync], you can specify an access condition so that the snapshot is created only if a condition is met.</span></span> <span data-ttu-id="a0a71-140">Pour spécifier une condition d’accès, utilisez le paramètre [AccessCondition][dotnet_AccessCondition].</span><span class="sxs-lookup"><span data-stu-id="a0a71-140">To specify an access condition, use the [AccessCondition][dotnet_AccessCondition] parameter.</span></span> <span data-ttu-id="a0a71-141">Si la condition spécifiée n’est pas remplie, la capture instantanée n’est pas créée et le service Blob retourne le code d’état [HTTPStatusCode][dotnet_HTTPStatusCode].PreconditionFailed.</span><span class="sxs-lookup"><span data-stu-id="a0a71-141">If the specified condition is not met, the snapshot is not created, and the Blob service returns status code [HTTPStatusCode][dotnet_HTTPStatusCode].PreconditionFailed.</span></span>

## <a name="delete-snapshots"></a><span data-ttu-id="a0a71-142">Suppression d'instantanés</span><span class="sxs-lookup"><span data-stu-id="a0a71-142">Delete snapshots</span></span>
<span data-ttu-id="a0a71-143">Un objet blob auquel sont associées des captures instantanées ne peut pas être supprimé, à moins de supprimer aussi les captures instantanées.</span><span class="sxs-lookup"><span data-stu-id="a0a71-143">You can't delete a blob with snapshots unless the snapshots are also deleted.</span></span> <span data-ttu-id="a0a71-144">Vous pouvez supprimer un instantané individuellement, ou spécifier que tous les instantanés doivent être supprimés lors de la suppression de l’objet blob source.</span><span class="sxs-lookup"><span data-stu-id="a0a71-144">You can delete a snapshot individually, or specify that all snapshots be deleted when the source blob is deleted.</span></span> <span data-ttu-id="a0a71-145">Si vous essayez de supprimer un objet blob auquel des instantanés sont encore associés, une erreur se produit.</span><span class="sxs-lookup"><span data-stu-id="a0a71-145">If you attempt to delete a blob that still has snapshots, an error results.</span></span>

<span data-ttu-id="a0a71-146">L’exemple de code suivant montre comment supprimer un objet blob et ses captures instantanées dans .NET, où `blockBlob` est un objet de type [CloudBlockBlob][dotnet_CloudBlockBlob] :</span><span class="sxs-lookup"><span data-stu-id="a0a71-146">The following code example shows how to delete a blob and its snapshots in .NET, where `blockBlob` is an object of type [CloudBlockBlob][dotnet_CloudBlockBlob]:</span></span>

```csharp
await blockBlob.DeleteIfExistsAsync(DeleteSnapshotsOption.IncludeSnapshots, null, null, null);
```

## <a name="snapshots-with-azure-premium-storage"></a><span data-ttu-id="a0a71-147">Instantanés avec Azure Premium Storage</span><span class="sxs-lookup"><span data-stu-id="a0a71-147">Snapshots with Azure Premium Storage</span></span>
<span data-ttu-id="a0a71-148">Lorsque vous utilisez des captures instantanées avec le stockage Premium, les règles suivantes s’appliquent :</span><span class="sxs-lookup"><span data-stu-id="a0a71-148">When using snapshots with Premium Storage, the following rules apply:</span></span>

* <span data-ttu-id="a0a71-149">Le nombre maximum d’instantanés par objet blob de pages dans un compte de stockage premium est 100.</span><span class="sxs-lookup"><span data-stu-id="a0a71-149">The maximum number of snapshots per page blob in a premium storage account is 100.</span></span> <span data-ttu-id="a0a71-150">Si vous dépassez cette limite, l’opération de capture instantanée d’objet blob retourne le code d’erreur 409 (`SnapshotCountExceeded`).</span><span class="sxs-lookup"><span data-stu-id="a0a71-150">If that limit is exceeded, the Snapshot Blob operation returns error code 409 (`SnapshotCountExceeded`).</span></span>
* <span data-ttu-id="a0a71-151">Vous pouvez prendre un instantané d’un objet blob de pages dans un compte de stockage premium toutes les 10 minutes.</span><span class="sxs-lookup"><span data-stu-id="a0a71-151">You can take a snapshot of a page blob in a premium storage account once every 10 minutes.</span></span> <span data-ttu-id="a0a71-152">Si vous dépassez ce taux, l’opération de capture instantanée d’objet blob retourne le code d’erreur 409 (`SnapshotOperationRateExceeded`).</span><span class="sxs-lookup"><span data-stu-id="a0a71-152">If that rate is exceeded, the Snapshot Blob operation returns error code 409 (`SnapshotOperationRateExceeded`).</span></span>
* <span data-ttu-id="a0a71-153">Pour lire un instantané, vous pouvez utiliser l’opération Copy Blob pour copier un instantané vers un autre objet blob de pages dans le compte.</span><span class="sxs-lookup"><span data-stu-id="a0a71-153">To read a snapshot, you can use the Copy Blob operation to copy a snapshot to another page blob in the account.</span></span> <span data-ttu-id="a0a71-154">L’objet blob de destination pour l'opération de copie ne doit pas avoir d'instantanés.</span><span class="sxs-lookup"><span data-stu-id="a0a71-154">The destination blob for the copy operation must not have any existing snapshots.</span></span> <span data-ttu-id="a0a71-155">Si l’objet blob de destination a des captures instantanées, l’opération Copy Blob retourne le code d’erreur 409 (`SnapshotsPresent`).</span><span class="sxs-lookup"><span data-stu-id="a0a71-155">If the destination blob does have snapshots, then the Copy Blob operation returns error code 409 (`SnapshotsPresent`).</span></span>

## <a name="return-the-absolute-uri-to-a-snapshot"></a><span data-ttu-id="a0a71-156">Renvoi de l'URI absolu d'un instantané</span><span class="sxs-lookup"><span data-stu-id="a0a71-156">Return the absolute URI to a snapshot</span></span>
<span data-ttu-id="a0a71-157">Cet exemple de code C# crée un instantané et écrit l’URI absolu de l’emplacement principal.</span><span class="sxs-lookup"><span data-stu-id="a0a71-157">This C# code example creates a snapshot and writes out the absolute URI for the primary location.</span></span>

```csharp
//Create the blob service client object.
const string ConnectionString = "DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key";

CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConnectionString);
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

//Get a reference to a container.
CloudBlobContainer container = blobClient.GetContainerReference("sample-container");
container.CreateIfNotExists();

//Get a reference to a blob.
CloudBlockBlob blob = container.GetBlockBlobReference("sampleblob.txt");
blob.UploadText("This is a blob.");

//Create a snapshot of the blob and write out its primary URI.
CloudBlockBlob blobSnapshot = blob.CreateSnapshot();
Console.WriteLine(blobSnapshot.SnapshotQualifiedStorageUri.PrimaryUri);
```

## <a name="understand-how-snapshots-accrue-charges"></a><span data-ttu-id="a0a71-158">Présentation des frais liés aux instantanés</span><span class="sxs-lookup"><span data-stu-id="a0a71-158">Understand how snapshots accrue charges</span></span>
<span data-ttu-id="a0a71-159">La création d’un instantané, c’est-à-dire d’une copie en lecture seule d’un objet blob, peut entraîner des frais de stockage de données supplémentaires pour votre compte.</span><span class="sxs-lookup"><span data-stu-id="a0a71-159">Creating a snapshot, which is a read-only copy of a blob, can result in additional data storage charges to your account.</span></span> <span data-ttu-id="a0a71-160">Lors de la conception de votre application, il est important de savoir comment ces frais peuvent s’accumuler pour pouvoir réduire les coûts.</span><span class="sxs-lookup"><span data-stu-id="a0a71-160">When designing your application, it is important to be aware of how these charges might accrue so that you can minimize costs.</span></span>

### <a name="important-billing-considerations"></a><span data-ttu-id="a0a71-161">Considérations importantes relatives à la facturation</span><span class="sxs-lookup"><span data-stu-id="a0a71-161">Important billing considerations</span></span>
<span data-ttu-id="a0a71-162">La liste suivante contient des points clés à prendre en compte lors de la création d’un instantané.</span><span class="sxs-lookup"><span data-stu-id="a0a71-162">The following list includes key points to consider when creating a snapshot.</span></span>

* <span data-ttu-id="a0a71-163">Des frais s’appliquent à votre compte de stockage pour des pages ou des blocs uniques, qu’ils soient dans l’objet blob ou dans l’instantané.</span><span class="sxs-lookup"><span data-stu-id="a0a71-163">Your storage account incurs charges for unique blocks or pages, whether they are in the blob or in the snapshot.</span></span> <span data-ttu-id="a0a71-164">Aucuns frais supplémentaires ne sont imputés à votre compte pour les instantanés associés à un objet blob tant que vous n'avez pas mis à jour l’objet blob sur lequel ils sont basés.</span><span class="sxs-lookup"><span data-stu-id="a0a71-164">Your account does not incur additional charges for snapshots associated with a blob until you update the blob on which they are based.</span></span> <span data-ttu-id="a0a71-165">Une fois que vous avez mis à jour l’objet blob de base, il diffère de ses instantanés.</span><span class="sxs-lookup"><span data-stu-id="a0a71-165">After you update the base blob, it diverges from its snapshots.</span></span> <span data-ttu-id="a0a71-166">Dans ce cas, vous êtes facturé pour les blocs ou pages uniques de chaque objet blob ou instantané.</span><span class="sxs-lookup"><span data-stu-id="a0a71-166">When this happens, you are charged for the unique blocks or pages in each blob or snapshot.</span></span>
* <span data-ttu-id="a0a71-167">Quand vous remplacez un bloc au sein d’un objet blob de bloc, ce bloc est ensuite facturé comme un bloc unique.</span><span class="sxs-lookup"><span data-stu-id="a0a71-167">When you replace a block within a block blob, that block is subsequently charged as a unique block.</span></span> <span data-ttu-id="a0a71-168">Cela est vrai même si le bloc a le même ID de bloc et les mêmes données que dans l'instantané.</span><span class="sxs-lookup"><span data-stu-id="a0a71-168">This is true even if the block has the same block ID and the same data as it has in the snapshot.</span></span> <span data-ttu-id="a0a71-169">Une fois le bloc revalidé, il diffère de son homologue dans tous les instantanés et vous serez facturé pour ses données.</span><span class="sxs-lookup"><span data-stu-id="a0a71-169">After the block is committed again, it diverges from its counterpart in any snapshot, and you will be charged for its data.</span></span> <span data-ttu-id="a0a71-170">Il en va de même pour une page dans un objet blob de pages qui est mise à jour avec des données identiques.</span><span class="sxs-lookup"><span data-stu-id="a0a71-170">The same holds true for a page in a page blob that's updated with identical data.</span></span>
* <span data-ttu-id="a0a71-171">Le remplacement d’un objet blob de blocs en appelant la méthode [UploadFromFile][dotnet_UploadFromFile], [UploadText][dotnet_UploadText], [UploadFromStream][dotnet_UploadFromStream] ou [UploadFromByteArray][dotnet_UploadFromByteArray] remplace tous les blocs de l’objet blob.</span><span class="sxs-lookup"><span data-stu-id="a0a71-171">Replacing a block blob by calling the [UploadFromFile][dotnet_UploadFromFile], [UploadText][dotnet_UploadText], [UploadFromStream][dotnet_UploadFromStream], or [UploadFromByteArray][dotnet_UploadFromByteArray] method replaces all blocks in the blob.</span></span> <span data-ttu-id="a0a71-172">Si vous avez une capture instantanée associée à cet objet blob, tous les blocs dans l’objet blob de base et la capture instantanée seront désormais différents et vous serez facturé pour tous les blocs des deux objets blob.</span><span class="sxs-lookup"><span data-stu-id="a0a71-172">If you have a snapshot associated with that blob, all blocks in the base blob and snapshot now diverge, and you will be charged for all the blocks in both blobs.</span></span> <span data-ttu-id="a0a71-173">Cela est vrai même si les données de l’objet blob de base et l’instantané restent identiques.</span><span class="sxs-lookup"><span data-stu-id="a0a71-173">This is true even if the data in the base blob and the snapshot remain identical.</span></span>
* <span data-ttu-id="a0a71-174">Le service blob Azure ne dispose d'aucun moyen pour déterminer si deux blocs contiennent des données identiques.</span><span class="sxs-lookup"><span data-stu-id="a0a71-174">The Azure Blob service does not have a means to determine whether two blocks contain identical data.</span></span> <span data-ttu-id="a0a71-175">Chaque bloc qui est téléchargé et validé est traité comme étant unique, même s’il a les mêmes données et le même ID de bloc.</span><span class="sxs-lookup"><span data-stu-id="a0a71-175">Each block that is uploaded and committed is treated as unique, even if it has the same data and the same block ID.</span></span> <span data-ttu-id="a0a71-176">Comme des frais sont applicables aux blocs uniques, il est important de savoir que la mise à jour d’un objet blob qui a une capture instantanée entraîne la création de blocs uniques supplémentaires et donc des frais supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="a0a71-176">Because charges accrue for unique blocks, it's important to consider that updating a blob that has a snapshot results in additional unique blocks and additional charges.</span></span>

### <a name="minimize-cost-with-snapshot-management"></a><span data-ttu-id="a0a71-177">Réduire les coûts grâce à la gestion des captures instantanées</span><span class="sxs-lookup"><span data-stu-id="a0a71-177">Minimize cost with snapshot management</span></span>

<span data-ttu-id="a0a71-178">Nous vous recommandons de gérer vos captures instantanées avec soin pour éviter des frais supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="a0a71-178">We recommend managing your snapshots carefully to avoid extra charges.</span></span> <span data-ttu-id="a0a71-179">Vous pouvez suivre ces meilleures pratiques pour réduire les coûts liés au stockage de vos captures instantanées :</span><span class="sxs-lookup"><span data-stu-id="a0a71-179">You can follow these best practices to help minimize the costs incurred by the storage of your snapshots:</span></span>

* <span data-ttu-id="a0a71-180">Supprimez et recréez les instantanés associés à un objet blob chaque fois que vous mettez à jour l'objet blob, même si vous le mettez à jour avec des données identiques, sauf si la conception de votre application exige de tenir à jour des instantanés.</span><span class="sxs-lookup"><span data-stu-id="a0a71-180">Delete and re-create snapshots associated with a blob whenever you update the blob, even if you are updating with identical data, unless your application design requires that you maintain snapshots.</span></span> <span data-ttu-id="a0a71-181">En supprimant et en recréant les captures instantanées de l’objet blob, vous pouvez vous assurer que l’objet blob et les captures instantanées ne diffèrent pas.</span><span class="sxs-lookup"><span data-stu-id="a0a71-181">By deleting and re-creating the blob's snapshots, you can ensure that the blob and snapshots do not diverge.</span></span>
* <span data-ttu-id="a0a71-182">Si vous tenez à jour des captures instantanées d’un objet blob, évitez d’appeler [UploadFromFile][dotnet_UploadFromFile], [UploadText][dotnet_UploadText], [UploadFromStream][dotnet_UploadFromStream] ou [UploadFromByteArray][dotnet_UploadFromByteArray] pour mettre à jour l’objet blob.</span><span class="sxs-lookup"><span data-stu-id="a0a71-182">If you are maintaining snapshots for a blob, avoid calling [UploadFromFile][dotnet_UploadFromFile], [UploadText][dotnet_UploadText], [UploadFromStream][dotnet_UploadFromStream], or [UploadFromByteArray][dotnet_UploadFromByteArray] to update the blob.</span></span> <span data-ttu-id="a0a71-183">Ces méthodes remplacent tous les blocs dans l’objet blob. Ainsi, votre objet blob de base et vos captures instantanées diffèrent de façon significative.</span><span class="sxs-lookup"><span data-stu-id="a0a71-183">These methods replace all of the blocks in the blob, causing your base blob and its snapshots to diverge significantly.</span></span> <span data-ttu-id="a0a71-184">Mettez plutôt à jour le moins de blocs possible en utilisant les méthodes [PutBlock][dotnet_PutBlock] et [PutBlockList][dotnet_PutBlockList].</span><span class="sxs-lookup"><span data-stu-id="a0a71-184">Instead, update the fewest possible number of blocks by using the [PutBlock][dotnet_PutBlock] and [PutBlockList][dotnet_PutBlockList] methods.</span></span>

### <a name="snapshot-billing-scenarios"></a><span data-ttu-id="a0a71-185">Scénarios de facturation d’instantanés</span><span class="sxs-lookup"><span data-stu-id="a0a71-185">Snapshot billing scenarios</span></span>
<span data-ttu-id="a0a71-186">Les scénarios suivants illustrent l’accumulation des coûts pour un objet blob de blocs et ses instantanés.</span><span class="sxs-lookup"><span data-stu-id="a0a71-186">The following scenarios demonstrate how charges accrue for a block blob and its snapshots.</span></span>

<span data-ttu-id="a0a71-187">**Scénario 1**</span><span class="sxs-lookup"><span data-stu-id="a0a71-187">**Scenario 1**</span></span>

<span data-ttu-id="a0a71-188">Dans le scénario 1, l'objet blob de base n'a pas été mis à jour depuis la capture de l'instantané. Des frais sont donc applicables uniquement pour les blocs uniques 1, 2 et 3.</span><span class="sxs-lookup"><span data-stu-id="a0a71-188">In scenario 1, the base blob has not been updated after the snapshot was taken, so charges are incurred only for unique blocks 1, 2, and 3.</span></span>

![Ressources Azure Storage](./media/storage-blob-snapshots/storage-blob-snapshots-billing-scenario-1.png)

<span data-ttu-id="a0a71-190">**Scénario 2**</span><span class="sxs-lookup"><span data-stu-id="a0a71-190">**Scenario 2**</span></span>

<span data-ttu-id="a0a71-191">Dans le scénario 2, l'objet blob de base a été mis à jour, mais pas l'instantané.</span><span class="sxs-lookup"><span data-stu-id="a0a71-191">In scenario 2, the base blob has been updated, but the snapshot has not.</span></span> <span data-ttu-id="a0a71-192">Le bloc 3 a été mis à jour, et bien qu’il contienne les mêmes données et le même ID, il est différent du bloc 3 de l’instantané.</span><span class="sxs-lookup"><span data-stu-id="a0a71-192">Block 3 was updated, and even though it contains the same data and the same ID, it is not the same as block 3 in the snapshot.</span></span> <span data-ttu-id="a0a71-193">Par conséquent, des frais pour quatre blocs sont facturés au compte.</span><span class="sxs-lookup"><span data-stu-id="a0a71-193">As a result, the account is charged for four blocks.</span></span>

![Ressources Azure Storage](./media/storage-blob-snapshots/storage-blob-snapshots-billing-scenario-2.png)

<span data-ttu-id="a0a71-195">**Scénario 3**</span><span class="sxs-lookup"><span data-stu-id="a0a71-195">**Scenario 3**</span></span>

<span data-ttu-id="a0a71-196">Dans le scénario 3, l'objet blob de base a été mis à jour, mais pas l'instantané.</span><span class="sxs-lookup"><span data-stu-id="a0a71-196">In scenario 3, the base blob has been updated, but the snapshot has not.</span></span> <span data-ttu-id="a0a71-197">Le bloc 3 a été remplacé par le bloc 4 dans l’objet blob de base, mais l’instantané reflète toujours le bloc 3.</span><span class="sxs-lookup"><span data-stu-id="a0a71-197">Block 3 was replaced with block 4 in the base blob, but the snapshot still reflects block 3.</span></span> <span data-ttu-id="a0a71-198">Par conséquent, des frais pour quatre blocs sont facturés au compte.</span><span class="sxs-lookup"><span data-stu-id="a0a71-198">As a result, the account is charged for four blocks.</span></span>

![Ressources Azure Storage](./media/storage-blob-snapshots/storage-blob-snapshots-billing-scenario-3.png)

<span data-ttu-id="a0a71-200">**Scénario 4**</span><span class="sxs-lookup"><span data-stu-id="a0a71-200">**Scenario 4**</span></span>

<span data-ttu-id="a0a71-201">Dans le scénario 4, l'objet blob de base a été complètement mis à jour et ne contient aucun de ses blocs d'origine.</span><span class="sxs-lookup"><span data-stu-id="a0a71-201">In scenario 4, the base blob has been completely updated and contains none of its original blocks.</span></span> <span data-ttu-id="a0a71-202">Par conséquent, des frais pour les huit blocs uniques sont facturés au compte.</span><span class="sxs-lookup"><span data-stu-id="a0a71-202">As a result, the account is charged for all eight unique blocks.</span></span> <span data-ttu-id="a0a71-203">Ce scénario peut se produire si vous utilisez une méthode de mise à jour [UploadFromFile][dotnet_UploadFromFile], [UploadText][dotnet_UploadText], [UploadFromStream][dotnet_UploadFromStream] ou [UploadFromByteArray][dotnet_UploadFromByteArray], car ces méthodes remplacent tout le contenu d’un objet blob.</span><span class="sxs-lookup"><span data-stu-id="a0a71-203">This scenario can occur if you are using an update method such as [UploadFromFile][dotnet_UploadFromFile], [UploadText][dotnet_UploadText], [UploadFromStream][dotnet_UploadFromStream], or [UploadFromByteArray][dotnet_UploadFromByteArray], because these methods replace all of the contents of a blob.</span></span>

![Ressources Azure Storage](./media/storage-blob-snapshots/storage-blob-snapshots-billing-scenario-4.png)

## <a name="next-steps"></a><span data-ttu-id="a0a71-205">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a0a71-205">Next steps</span></span>

* <span data-ttu-id="a0a71-206">Vous trouverez plus d’informations sur l’utilisation des captures instantanées de disque de machine virtuelle (VM) dans [Sauvegarder les disques de machines virtuelles Azure non gérés avec des captures instantanées incrémentielles](storage-incremental-snapshots.md)</span><span class="sxs-lookup"><span data-stu-id="a0a71-206">You can find more information about working with virtual machine (VM) disk snapshots in [Back up Azure unmanaged VM disks with incremental snapshots](storage-incremental-snapshots.md)</span></span>

* <span data-ttu-id="a0a71-207">Pour obtenir des exemples de code supplémentaires d’utilisation du Stockage Blob, consultez [Exemples de code Azure](https://azure.microsoft.com/documentation/samples/?service=storage&term=blob).</span><span class="sxs-lookup"><span data-stu-id="a0a71-207">For additional code examples using Blob storage, see [Azure Code Samples](https://azure.microsoft.com/documentation/samples/?service=storage&term=blob).</span></span> <span data-ttu-id="a0a71-208">Vous pouvez télécharger un exemple d’application et l’exécuter ou parcourir le code sur GitHub.</span><span class="sxs-lookup"><span data-stu-id="a0a71-208">You can download a sample application and run it, or browse the code on GitHub.</span></span>

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