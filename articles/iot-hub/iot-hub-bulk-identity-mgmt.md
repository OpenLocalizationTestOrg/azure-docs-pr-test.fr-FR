---
title: "exportation d’aaaImport des identités d’appareil Azure IoT Hub | Documents Microsoft"
description: "Comment toouse hello Azure IoT service SDK tooperform opérations contre hello identité Registre tooimport en bloc et exporter les identités des appareils. Opérations d’importation permettent de toocreate, mise à jour et suppression des identités de périphérique en bloc."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 2ade1494-45ea-46a7-ade7-cf6e11ce62da
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/03/2017
ms.author: dobett
ms.openlocfilehash: b67777d381e03de05d9c007b5ce6bdaf15bbb8f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-your-iot-hub-device-identities-in-bulk"></a><span data-ttu-id="2ea79-104">Gestion de vos identités d’appareil IoT Hub en bloc</span><span class="sxs-lookup"><span data-stu-id="2ea79-104">Manage your IoT Hub device identities in bulk</span></span>

<span data-ttu-id="2ea79-105">Chaque hub IoT a un registre d’identité que vous pouvez utiliser les ressources de chaque appareil toocreate dans le service hello.</span><span class="sxs-lookup"><span data-stu-id="2ea79-105">Each IoT hub has an identity registry you can use toocreate per-device resources in hello service.</span></span> <span data-ttu-id="2ea79-106">Registre des identités Hello vous permet également de points de terminaison toocontrol accès toohello périphérique.</span><span class="sxs-lookup"><span data-stu-id="2ea79-106">hello identity registry also enables you toocontrol access toohello device-facing endpoints.</span></span> <span data-ttu-id="2ea79-107">Cet article décrit comment les identités d’appareil tooimport et d’exportation dans en bloc tooand à partir d’un registre d’identité.</span><span class="sxs-lookup"><span data-stu-id="2ea79-107">This article describes how tooimport and export device identities in bulk tooand from an identity registry.</span></span>

<span data-ttu-id="2ea79-108">Opérations d’importation et d’exportation ont lieu dans le contexte de hello de *travaux* qui vous permettent des opérations de service tooexecute en bloc par rapport à un hub IoT.</span><span class="sxs-lookup"><span data-stu-id="2ea79-108">Import and export operations take place in hello context of *Jobs* that enable you tooexecute bulk service operations against an IoT hub.</span></span>

<span data-ttu-id="2ea79-109">Hello **RegistryManager** classe inclut hello **ExportDevicesAsync** et **ImportDevicesAsync** les méthodes qui utilisent hello **travail** Framework.</span><span class="sxs-lookup"><span data-stu-id="2ea79-109">hello **RegistryManager** class includes hello **ExportDevicesAsync** and **ImportDevicesAsync** methods that use hello **Job** framework.</span></span> <span data-ttu-id="2ea79-110">Ces méthodes permettent de tooexport, importation et synchroniser l’intégralité de hello de Registre des identités un hub IoT.</span><span class="sxs-lookup"><span data-stu-id="2ea79-110">These methods enable you tooexport, import, and synchronize hello entirety of an IoT hub identity registry.</span></span>

## <a name="what-are-jobs"></a><span data-ttu-id="2ea79-111">Que sont les tâches ?</span><span class="sxs-lookup"><span data-stu-id="2ea79-111">What are jobs?</span></span>

<span data-ttu-id="2ea79-112">Les opérations de Registre identité utilisent hello **travail** système lorsque hello opération :</span><span class="sxs-lookup"><span data-stu-id="2ea79-112">Identity registry operations use hello **Job** system when hello operation:</span></span>

* <span data-ttu-id="2ea79-113">A une durée d’exécution peut être longue comparée toostandard opérations d’exécution.</span><span class="sxs-lookup"><span data-stu-id="2ea79-113">Has a potentially long execution time compared toostandard run-time operations.</span></span>
* <span data-ttu-id="2ea79-114">Retourne une grande quantité d’utilisateur toohello de données.</span><span class="sxs-lookup"><span data-stu-id="2ea79-114">Returns a large amount of data toohello user.</span></span>

<span data-ttu-id="2ea79-115">Au lieu d’un seul appel d’API en attente ou de blocage sur le résultat de hello d’opération de hello, opération de hello crée de façon asynchrone un **travail** pour ce hub IoT.</span><span class="sxs-lookup"><span data-stu-id="2ea79-115">Instead of a single API call waiting or blocking on hello result of hello operation, hello operation asynchronously creates a **Job** for that IoT hub.</span></span> <span data-ttu-id="2ea79-116">opération de Hello, puis retourne immédiatement un **JobProperties** objet.</span><span class="sxs-lookup"><span data-stu-id="2ea79-116">hello operation then immediately returns a **JobProperties** object.</span></span>

<span data-ttu-id="2ea79-117">Hello suivant c# de code extrait de code montre comment toocreate un travail d’exportation :</span><span class="sxs-lookup"><span data-stu-id="2ea79-117">hello following C# code snippet shows how toocreate an export job:</span></span>

```csharp
// Call an export job on hello IoT Hub tooretrieve all devices
JobProperties exportJob = await registryManager.ExportDevicesAsync(containerSasUri, false);
```

> [!NOTE]
> <span data-ttu-id="2ea79-118">toouse hello **RegistryManager** de classe dans votre code c#, ajoutez hello **Microsoft.Azure.Devices** projet tooyour de package NuGet.</span><span class="sxs-lookup"><span data-stu-id="2ea79-118">toouse hello **RegistryManager** class in your C# code, add hello **Microsoft.Azure.Devices** NuGet package tooyour project.</span></span> <span data-ttu-id="2ea79-119">Hello **RegistryManager** classe se trouve dans hello **Microsoft.Azure.Devices** espace de noms.</span><span class="sxs-lookup"><span data-stu-id="2ea79-119">hello **RegistryManager** class is in hello **Microsoft.Azure.Devices** namespace.</span></span>

<span data-ttu-id="2ea79-120">Vous pouvez utiliser hello **RegistryManager** classe état de hello tooquery Hello **travail** à l’aide de hello retourné **JobProperties** métadonnées.</span><span class="sxs-lookup"><span data-stu-id="2ea79-120">You can use hello **RegistryManager** class tooquery hello state of hello **Job** using hello returned **JobProperties** metadata.</span></span>

<span data-ttu-id="2ea79-121">Hello extrait de code c# suivant montre comment toopoll toosee de toutes les cinq secondes si hello la tâche est terminée :</span><span class="sxs-lookup"><span data-stu-id="2ea79-121">hello following C# code snippet shows how toopoll every five seconds toosee if hello job has finished executing:</span></span>

```csharp
// Wait until job is finished
while(true)
{
  exportJob = await registryManager.GetJobAsync(exportJob.JobId);
  if (exportJob.Status == JobStatus.Completed || 
      exportJob.Status == JobStatus.Failed ||
      exportJob.Status == JobStatus.Cancelled)
  {
    // Job has finished executing
    break;
  }

  await Task.Delay(TimeSpan.FromSeconds(5));
}
```

## <a name="export-devices"></a><span data-ttu-id="2ea79-122">Exporter des appareils</span><span class="sxs-lookup"><span data-stu-id="2ea79-122">Export devices</span></span>

<span data-ttu-id="2ea79-123">Hello d’utilisation **ExportDevicesAsync** intégralité de hello méthode tooexport d’un tooan de Registre IoT hub identité [Azure Storage](../storage/index.md) conteneur d’objets blob à l’aide un [Signature d’accès partagé](../storage/common/storage-security-guide.md#data-plane-security).</span><span class="sxs-lookup"><span data-stu-id="2ea79-123">Use hello **ExportDevicesAsync** method tooexport hello entirety of an IoT hub identity registry tooan [Azure Storage](../storage/index.md) blob container using a [Shared Access Signature](../storage/common/storage-security-guide.md#data-plane-security).</span></span>

<span data-ttu-id="2ea79-124">Cette méthode vous permet de toocreate les sauvegardes fiable de vos informations de périphérique dans un conteneur d’objets blob que vous contrôlez.</span><span class="sxs-lookup"><span data-stu-id="2ea79-124">This method enables you toocreate reliable backups of your device information in a blob container that you control.</span></span>

<span data-ttu-id="2ea79-125">Hello **ExportDevicesAsync** méthode requiert deux paramètres :</span><span class="sxs-lookup"><span data-stu-id="2ea79-125">hello **ExportDevicesAsync** method requires two parameters:</span></span>

* <span data-ttu-id="2ea79-126">Une *chaîne* qui contient l’URI d’un conteneur d’objets blob.</span><span class="sxs-lookup"><span data-stu-id="2ea79-126">A *string* that contains a URI of a blob container.</span></span> <span data-ttu-id="2ea79-127">Cet URI doit contenir un jeton SAS qui accorde un accès en écriture toohello conteneur.</span><span class="sxs-lookup"><span data-stu-id="2ea79-127">This URI must contain a SAS token that grants write access toohello container.</span></span> <span data-ttu-id="2ea79-128">Hello crée un objet blob de blocs dans ces conteneur toostore hello sérialisé exporter périphérique des données.</span><span class="sxs-lookup"><span data-stu-id="2ea79-128">hello job creates a block blob in this container toostore hello serialized export device data.</span></span> <span data-ttu-id="2ea79-129">un jeton SAS Hello doit inclure ces autorisations :</span><span class="sxs-lookup"><span data-stu-id="2ea79-129">hello SAS token must include these permissions:</span></span>

   ```csharp
   SharedAccessBlobPermissions.Write | SharedAccessBlobPermissions.Read | SharedAccessBlobPermissions.Delete
   ```

* <span data-ttu-id="2ea79-130">A *booléenne* qui indique si vous souhaitez tooexclude clés d’authentification à partir de vos données d’exportation.</span><span class="sxs-lookup"><span data-stu-id="2ea79-130">A *boolean* that indicates if you want tooexclude authentication keys from your export data.</span></span> <span data-ttu-id="2ea79-131">Si la valeur est **false**, des clés d’authentification sont incluses dans la sortie d’exportation.</span><span class="sxs-lookup"><span data-stu-id="2ea79-131">If **false**, authentication keys are included in export output.</span></span> <span data-ttu-id="2ea79-132">Dans le cas contraire, les clés sont exportées sous forme de valeur **null**.</span><span class="sxs-lookup"><span data-stu-id="2ea79-132">Otherwise, keys are exported as **null**.</span></span>

<span data-ttu-id="2ea79-133">Hello extrait de code c# suivant montre comment tooinitiate un travail d’exportation qui inclut des clés de l’authentification d’appareil Bonjour exporter des données et puis interroger fin :</span><span class="sxs-lookup"><span data-stu-id="2ea79-133">hello following C# code snippet shows how tooinitiate an export job that includes device authentication keys in hello export data and then poll for completion:</span></span>

```csharp
// Call an export job on hello IoT Hub tooretrieve all devices
JobProperties exportJob = await registryManager.ExportDevicesAsync(containerSasUri, false);

// Wait until job is finished
while(true)
{
    exportJob = await registryManager.GetJobAsync(exportJob.JobId);
    if (exportJob.Status == JobStatus.Completed || 
        exportJob.Status == JobStatus.Failed ||
        exportJob.Status == JobStatus.Cancelled)
    {
    // Job has finished executing
    break;
    }

    await Task.Delay(TimeSpan.FromSeconds(5));
}
```

<span data-ttu-id="2ea79-134">Hello travail stocke sa sortie dans un conteneur d’objets blob hello fourni en tant qu’objet blob de blocs avec le nom de hello **devices.txt**.</span><span class="sxs-lookup"><span data-stu-id="2ea79-134">hello job stores its output in hello provided blob container as a block blob with hello name **devices.txt**.</span></span> <span data-ttu-id="2ea79-135">les données de sortie Hello se comprennent de données de l’appareil sérialisé au format JSON, avec un périphérique par ligne.</span><span class="sxs-lookup"><span data-stu-id="2ea79-135">hello output data consists of JSON serialized device data, with one device per line.</span></span>

<span data-ttu-id="2ea79-136">Hello suivant montre les données de sortie hello :</span><span class="sxs-lookup"><span data-stu-id="2ea79-136">hello following example shows hello output data:</span></span>

```json
{"id":"Device1","eTag":"MA==","status":"enabled","authentication":{"symmetricKey":{"primaryKey":"abc=","secondaryKey":"def="}}}
{"id":"Device2","eTag":"MA==","status":"enabled","authentication":{"symmetricKey":{"primaryKey":"abc=","secondaryKey":"def="}}}
{"id":"Device3","eTag":"MA==","status":"disabled","authentication":{"symmetricKey":{"primaryKey":"abc=","secondaryKey":"def="}}}
{"id":"Device4","eTag":"MA==","status":"disabled","authentication":{"symmetricKey":{"primaryKey":"abc=","secondaryKey":"def="}}}
{"id":"Device5","eTag":"MA==","status":"enabled","authentication":{"symmetricKey":{"primaryKey":"abc=","secondaryKey":"def="}}}
```

Si un périphérique comporte des données de double, données de double hello sont également exportées avec les données de l’appareil hello. Hello suivant montre ce format. <span data-ttu-id="2ea79-139">Toutes les données de ligne de « twinETag » hello jusqu'à la fin de hello sont les données double.</span><span class="sxs-lookup"><span data-stu-id="2ea79-139">All data from hello "twinETag" line until hello end are twin data.</span></span>

```json
{
   "id":"export-6d84f075-0",
   "eTag":"MQ==",
   "status":"enabled",
   "statusReason":"firstUpdate",
   "authentication":null,
   "twinETag":"AAAAAAAAAAI=",
   "tags":{
      "Location":"LivingRoom"
   },
   "properties":{
      "desired":{
         "Thermostat":{
            "Temperature":75.1,
            "Unit":"F"
         },
         "$metadata":{
            "$lastUpdated":"2017-03-09T18:30:52.3167248Z",
            "$lastUpdatedVersion":2,
            "Thermostat":{
               "$lastUpdated":"2017-03-09T18:30:52.3167248Z",
               "$lastUpdatedVersion":2,
               "Temperature":{
                  "$lastUpdated":"2017-03-09T18:30:52.3167248Z",
                  "$lastUpdatedVersion":2
               },
               "Unit":{
                  "$lastUpdated":"2017-03-09T18:30:52.3167248Z",
                  "$lastUpdatedVersion":2
               }
            }
         },
         "$version":2
      },
      "reported":{
         "$metadata":{
            "$lastUpdated":"2017-03-09T18:30:51.1309437Z"
         },
         "$version":1
      }
   }
}
```

<span data-ttu-id="2ea79-140">Si vous devez accéder aux données toothis dans du code, vous pouvez facilement désérialiser ces données à l’aide de hello **ExportImportDevice** classe.</span><span class="sxs-lookup"><span data-stu-id="2ea79-140">If you need access toothis data in code, you can easily deserialize this data using hello **ExportImportDevice** class.</span></span> <span data-ttu-id="2ea79-141">Hello extrait de code c# suivant montre comment les informations de périphérique tooread qui a été précédemment exportées tooa objet blob de blocs :</span><span class="sxs-lookup"><span data-stu-id="2ea79-141">hello following C# code snippet shows how tooread device information that was previously exported tooa block blob:</span></span>

```csharp
var exportedDevices = new List<ExportImportDevice>();

using (var streamReader = new StreamReader(await blob.OpenReadAsync(AccessCondition.GenerateIfExistsCondition(), null, null), Encoding.UTF8))
{
  while (streamReader.Peek() != -1)
  {
    string line = await streamReader.ReadLineAsync();
    var device = JsonConvert.DeserializeObject<ExportImportDevice>(line);
    exportedDevices.Add(device);
  }
}
```

> [!NOTE]
> <span data-ttu-id="2ea79-142">Vous pouvez également utiliser hello **GetDevicesAsync** méthode Hello **RegistryManager** classe toofetch une liste de vos appareils.</span><span class="sxs-lookup"><span data-stu-id="2ea79-142">You can also use hello **GetDevicesAsync** method of hello **RegistryManager** class toofetch a list of your devices.</span></span> <span data-ttu-id="2ea79-143">Toutefois, cette approche a une valeur maximale de 1000 nombre hello d’objets de périphérique qui sont retournées.</span><span class="sxs-lookup"><span data-stu-id="2ea79-143">However, this approach has a hard cap of 1000 on hello number of device objects that are returned.</span></span> <span data-ttu-id="2ea79-144">Hello attendu de cas d’utilisation de hello **GetDevicesAsync** méthode est pour le débogage de tooaid de scénarios de développement et n’est pas recommandée pour les charges de production.</span><span class="sxs-lookup"><span data-stu-id="2ea79-144">hello expected use case for hello **GetDevicesAsync** method is for development scenarios tooaid debugging and is not recommended for production workloads.</span></span>

## <a name="import-devices"></a><span data-ttu-id="2ea79-145">Importer des appareils</span><span class="sxs-lookup"><span data-stu-id="2ea79-145">Import devices</span></span>

<span data-ttu-id="2ea79-146">Hello **ImportDevicesAsync** méthode Bonjour **RegistryManager** classe vous permet d’opérations d’importation et synchronisation d’en bloc dans un registre des identités IoT hub tooperform.</span><span class="sxs-lookup"><span data-stu-id="2ea79-146">hello **ImportDevicesAsync** method in hello **RegistryManager** class enables you tooperform bulk import and synchronization operations in an IoT hub identity registry.</span></span> <span data-ttu-id="2ea79-147">Comme hello **ExportDevicesAsync** (méthode), hello **ImportDevicesAsync** méthode utilise hello **travail** framework.</span><span class="sxs-lookup"><span data-stu-id="2ea79-147">Like hello **ExportDevicesAsync** method, hello **ImportDevicesAsync** method uses hello **Job** framework.</span></span>

<span data-ttu-id="2ea79-148">Prendre en charge à l’aide de hello **ImportDevicesAsync** (méthode), car dans Ajout tooprovisioning nouveaux appareils dans votre Registre des identités, il peut également mettre à jour et supprimer des périphériques existants.</span><span class="sxs-lookup"><span data-stu-id="2ea79-148">Take care using hello **ImportDevicesAsync** method because in addition tooprovisioning new devices in your identity registry, it can also update and delete existing devices.</span></span>

> [!WARNING]
> <span data-ttu-id="2ea79-149">Il est impossible d’annuler une opération d’importation.</span><span class="sxs-lookup"><span data-stu-id="2ea79-149">An import operation cannot be undone.</span></span> <span data-ttu-id="2ea79-150">Toujours sauvegarder vos données existantes à l’aide de hello **ExportDevicesAsync** conteneur d’objets blob méthode tooanother avant d’apporter en bloc modifie le Registre des identités tooyour.</span><span class="sxs-lookup"><span data-stu-id="2ea79-150">Always back up your existing data using hello **ExportDevicesAsync** method tooanother blob container before you make bulk changes tooyour identity registry.</span></span>

<span data-ttu-id="2ea79-151">Hello **ImportDevicesAsync** méthode accepte deux paramètres :</span><span class="sxs-lookup"><span data-stu-id="2ea79-151">hello **ImportDevicesAsync** method takes two parameters:</span></span>

* <span data-ttu-id="2ea79-152">A *chaîne* qui contient l’URI d’un [Azure Storage](../storage/index.md) toouse conteneur comme des objets blob *d’entrée* toohello travail.</span><span class="sxs-lookup"><span data-stu-id="2ea79-152">A *string* that contains a URI of an [Azure Storage](../storage/index.md) blob container toouse as *input* toohello job.</span></span> <span data-ttu-id="2ea79-153">Cet URI doit contenir un jeton SAS qui accorde l’accès en lecture toohello conteneur.</span><span class="sxs-lookup"><span data-stu-id="2ea79-153">This URI must contain a SAS token that grants read access toohello container.</span></span> <span data-ttu-id="2ea79-154">Ce conteneur doit contenir un objet blob avec le nom de hello **devices.txt** qui contient tooimport de données de périphérique hello sérialisé dans le Registre de votre identité.</span><span class="sxs-lookup"><span data-stu-id="2ea79-154">This container must contain a blob with hello name **devices.txt** that contains hello serialized device data tooimport into your identity registry.</span></span> <span data-ttu-id="2ea79-155">Hello importer des données doivent contenir des informations de périphérique Bonjour même format JSON que hello **ExportImportDevice** travail utilise lorsqu’il crée un **devices.txt** blob.</span><span class="sxs-lookup"><span data-stu-id="2ea79-155">hello import data must contain device information in hello same JSON format that hello **ExportImportDevice** job uses when it creates a **devices.txt** blob.</span></span> <span data-ttu-id="2ea79-156">un jeton SAS Hello doit inclure ces autorisations :</span><span class="sxs-lookup"><span data-stu-id="2ea79-156">hello SAS token must include these permissions:</span></span>

   ```csharp
   SharedAccessBlobPermissions.Read
   ```
* <span data-ttu-id="2ea79-157">A *chaîne* qui contient l’URI d’un [Azure Storage](https://azure.microsoft.com/documentation/services/storage/) toouse conteneur comme des objets blob *sortie* à partir de la tâche de hello.</span><span class="sxs-lookup"><span data-stu-id="2ea79-157">A *string* that contains a URI of an [Azure Storage](https://azure.microsoft.com/documentation/services/storage/) blob container toouse as *output* from hello job.</span></span> <span data-ttu-id="2ea79-158">Hello travail crée un objet blob de blocs dans ce conteneur toostore aucune information d’erreur de l’importation de hello terminée **travail**.</span><span class="sxs-lookup"><span data-stu-id="2ea79-158">hello job creates a block blob in this container toostore any error information from hello completed import **Job**.</span></span> <span data-ttu-id="2ea79-159">un jeton SAS Hello doit inclure ces autorisations :</span><span class="sxs-lookup"><span data-stu-id="2ea79-159">hello SAS token must include these permissions:</span></span>

   ```csharp
   SharedAccessBlobPermissions.Write | SharedAccessBlobPermissions.Read | SharedAccessBlobPermissions.Delete
   ```

> [!NOTE]
> <span data-ttu-id="2ea79-160">paramètres de Hello deux peuvent pointer toohello même conteneur d’objets blob.</span><span class="sxs-lookup"><span data-stu-id="2ea79-160">hello two parameters can point toohello same blob container.</span></span> <span data-ttu-id="2ea79-161">les paramètres distincts Hello activent simplement plus de contrôle sur vos données en tant que conteneur de sortie hello nécessite des autorisations supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="2ea79-161">hello separate parameters simply enable more control over your data as hello output container requires additional permissions.</span></span>

<span data-ttu-id="2ea79-162">Hello suivant c# de code extrait de code montre comment tooinitiate un travail d’importation :</span><span class="sxs-lookup"><span data-stu-id="2ea79-162">hello following C# code snippet shows how tooinitiate an import job:</span></span>

```csharp
JobProperties importJob = await registryManager.ImportDevicesAsync(containerSasUri, containerSasUri);
```

<span data-ttu-id="2ea79-163">Cette méthode peut également être données hello tooimport utilisé double du périphérique hello.</span><span class="sxs-lookup"><span data-stu-id="2ea79-163">This method can also be used tooimport hello data for hello device twin.</span></span> <span data-ttu-id="2ea79-164">format Hello hello d’entrée de données est hello même en tant que format hello illustré hello **ExportDevicesAsync** section.</span><span class="sxs-lookup"><span data-stu-id="2ea79-164">hello format for hello data input is hello same as hello format shown in hello **ExportDevicesAsync** section.</span></span> <span data-ttu-id="2ea79-165">De cette façon, vous pouvez réimporter les données de hello exportée.</span><span class="sxs-lookup"><span data-stu-id="2ea79-165">In this way, you can reimport hello exported data.</span></span> <span data-ttu-id="2ea79-166">Hello **$metadata** est facultatif.</span><span class="sxs-lookup"><span data-stu-id="2ea79-166">hello **$metadata** is optional.</span></span>

## <a name="import-behavior"></a><span data-ttu-id="2ea79-167">Comportement d’importation</span><span class="sxs-lookup"><span data-stu-id="2ea79-167">Import behavior</span></span>

<span data-ttu-id="2ea79-168">Vous pouvez utiliser hello **ImportDevicesAsync** suivant de méthode tooperform hello en bloc des opérations dans le Registre de votre identité :</span><span class="sxs-lookup"><span data-stu-id="2ea79-168">You can use hello **ImportDevicesAsync** method tooperform hello following bulk operations in your identity registry:</span></span>

* <span data-ttu-id="2ea79-169">Inscription en bloc de nouveaux appareils</span><span class="sxs-lookup"><span data-stu-id="2ea79-169">Bulk registration of new devices</span></span>
* <span data-ttu-id="2ea79-170">Suppression en bloc d’appareils existants</span><span class="sxs-lookup"><span data-stu-id="2ea79-170">Bulk deletions of existing devices</span></span>
* <span data-ttu-id="2ea79-171">Modifications d’état en bloc (activer ou désactiver des appareils)</span><span class="sxs-lookup"><span data-stu-id="2ea79-171">Bulk status changes (enable or disable devices)</span></span>
* <span data-ttu-id="2ea79-172">Attribution en bloc de nouvelles clés d’authentification d’appareils</span><span class="sxs-lookup"><span data-stu-id="2ea79-172">Bulk assignment of new device authentication keys</span></span>
* <span data-ttu-id="2ea79-173">Auto-régénération en bloc des clés d’authentification d’appareils</span><span class="sxs-lookup"><span data-stu-id="2ea79-173">Bulk auto-regeneration of device authentication keys</span></span>
* <span data-ttu-id="2ea79-174">Mise à jour en bloc de données de représentation</span><span class="sxs-lookup"><span data-stu-id="2ea79-174">Bulk update of twin data</span></span>

<span data-ttu-id="2ea79-175">Vous pouvez effectuer n’importe quelle combinaison de hello précédant les opérations dans un seul **ImportDevicesAsync** appeler.</span><span class="sxs-lookup"><span data-stu-id="2ea79-175">You can perform any combination of hello preceding operations within a single **ImportDevicesAsync** call.</span></span> <span data-ttu-id="2ea79-176">Par exemple, vous pouvez inscrire de nouveaux périphériques et supprimer ou mettre à jour des périphériques existants à hello même temps.</span><span class="sxs-lookup"><span data-stu-id="2ea79-176">For example, you can register new devices and delete or update existing devices at hello same time.</span></span> <span data-ttu-id="2ea79-177">Lorsqu’il est utilisé avec hello **ExportDevicesAsync** (méthode), vous pouvez entièrement migrer tous vos appareils à partir d’un tooanother de hub IoT.</span><span class="sxs-lookup"><span data-stu-id="2ea79-177">When used along with hello **ExportDevicesAsync** method, you can completely migrate all your devices from one IoT hub tooanother.</span></span>

<span data-ttu-id="2ea79-178">Si le fichier d’importation hello inclut les métadonnées de double, ces métadonnées remplacent les métadonnées existantes du double hello.</span><span class="sxs-lookup"><span data-stu-id="2ea79-178">If hello import file includes twin metadata, then this metadata overwrites hello existing twin metadata.</span></span> <span data-ttu-id="2ea79-179">Si le fichier d’importation hello n’inclut pas de métadonnées de double, puis uniquement hello `lastUpdateTime` métadonnées sont mis à jour à l’aide de hello heure actuelle.</span><span class="sxs-lookup"><span data-stu-id="2ea79-179">If hello import file does not include twin metadata, then only hello `lastUpdateTime` metadata is updated using hello current time.</span></span>

<span data-ttu-id="2ea79-180">Hello utilisation facultative **importMode** propriété dans les données de sérialisation hello pour chaque périphérique toocontrol hello importation processus par périphérique.</span><span class="sxs-lookup"><span data-stu-id="2ea79-180">Use hello optional **importMode** property in hello import serialization data for each device toocontrol hello import process per-device.</span></span> <span data-ttu-id="2ea79-181">Hello **importMode** propriété a hello options suivantes :</span><span class="sxs-lookup"><span data-stu-id="2ea79-181">hello **importMode** property has hello following options:</span></span>

| <span data-ttu-id="2ea79-182">importMode</span><span class="sxs-lookup"><span data-stu-id="2ea79-182">importMode</span></span> | <span data-ttu-id="2ea79-183">Description</span><span class="sxs-lookup"><span data-stu-id="2ea79-183">Description</span></span> |
| --- | --- |
| <span data-ttu-id="2ea79-184">**createOrUpdate**</span><span class="sxs-lookup"><span data-stu-id="2ea79-184">**createOrUpdate**</span></span> |<span data-ttu-id="2ea79-185">Si un appareil avec hello spécifié n’existe pas **id**, il est nouvellement inscrit.</span><span class="sxs-lookup"><span data-stu-id="2ea79-185">If a device does not exist with hello specified **id**, it is newly registered.</span></span> <br/><span data-ttu-id="2ea79-186">Si l’appareil de hello existe déjà, informations existantes sont remplacées par hello a fourni des données d’entrée sans se soucier des toohello **ETag** valeur.</span><span class="sxs-lookup"><span data-stu-id="2ea79-186">If hello device already exists, existing information is overwritten with hello provided input data without regard toohello **ETag** value.</span></span> <br> <span data-ttu-id="2ea79-187">utilisateur de Hello peut éventuellement spécifier des données de double en même temps que les données de l’appareil hello.</span><span class="sxs-lookup"><span data-stu-id="2ea79-187">hello user can optionally specify twin data along with hello device data.</span></span> <span data-ttu-id="2ea79-188">etag du double Hello si spécifié, est traitée indépendamment de l’etag de l’appareil hello.</span><span class="sxs-lookup"><span data-stu-id="2ea79-188">hello twin’s etag, if specified, is processed independently from hello device’s etag.</span></span> <span data-ttu-id="2ea79-189">S’il existe une incompatibilité avec les etag du double hello existant, une erreur est consignée toohello du journal.</span><span class="sxs-lookup"><span data-stu-id="2ea79-189">If there is a mismatch with hello existing twin’s etag, an error is written toohello log file.</span></span> |
| <span data-ttu-id="2ea79-190">**create**</span><span class="sxs-lookup"><span data-stu-id="2ea79-190">**create**</span></span> |<span data-ttu-id="2ea79-191">Si un appareil avec hello spécifié n’existe pas **id**, il est nouvellement inscrit.</span><span class="sxs-lookup"><span data-stu-id="2ea79-191">If a device does not exist with hello specified **id**, it is newly registered.</span></span> <br/><span data-ttu-id="2ea79-192">Si l’appareil de hello existe déjà, une erreur est consignée toohello du journal.</span><span class="sxs-lookup"><span data-stu-id="2ea79-192">If hello device already exists, an error is written toohello log file.</span></span> <br> <span data-ttu-id="2ea79-193">utilisateur de Hello peut éventuellement spécifier des données de double en même temps que les données de l’appareil hello.</span><span class="sxs-lookup"><span data-stu-id="2ea79-193">hello user can optionally specify twin data along with hello device data.</span></span> <span data-ttu-id="2ea79-194">etag du double Hello si spécifié, est traitée indépendamment de l’etag de l’appareil hello.</span><span class="sxs-lookup"><span data-stu-id="2ea79-194">hello twin’s etag, if specified, is processed independently from hello device’s etag.</span></span> <span data-ttu-id="2ea79-195">S’il existe une incompatibilité avec les etag du double hello existant, une erreur est consignée toohello du journal.</span><span class="sxs-lookup"><span data-stu-id="2ea79-195">If there is a mismatch with hello existing twin’s etag, an error is written toohello log file.</span></span> |
| <span data-ttu-id="2ea79-196">**update**</span><span class="sxs-lookup"><span data-stu-id="2ea79-196">**update**</span></span> |<span data-ttu-id="2ea79-197">Si un appareil existe déjà avec hello spécifié **id**, les informations existantes sont remplacées par hello a fourni des données d’entrée sans se soucier des toohello **ETag** valeur.</span><span class="sxs-lookup"><span data-stu-id="2ea79-197">If a device already exists with hello specified **id**, existing information is overwritten with hello provided input data without regard toohello **ETag** value.</span></span> <br/><span data-ttu-id="2ea79-198">Si l’appareil de hello n’existe pas, une erreur est consignée toohello du journal.</span><span class="sxs-lookup"><span data-stu-id="2ea79-198">If hello device does not exist, an error is written toohello log file.</span></span> |
| <span data-ttu-id="2ea79-199">**updateIfMatchETag**</span><span class="sxs-lookup"><span data-stu-id="2ea79-199">**updateIfMatchETag**</span></span> |<span data-ttu-id="2ea79-200">Si un appareil existe déjà avec hello spécifié **id**, les informations existantes sont remplacées par hello a fourni des données d’entrée uniquement s’il existe un **ETag** correspondent.</span><span class="sxs-lookup"><span data-stu-id="2ea79-200">If a device already exists with hello specified **id**, existing information is overwritten with hello provided input data only if there is an **ETag** match.</span></span> <br/><span data-ttu-id="2ea79-201">Si l’appareil de hello n’existe pas, une erreur est consignée toohello du journal.</span><span class="sxs-lookup"><span data-stu-id="2ea79-201">If hello device does not exist, an error is written toohello log file.</span></span> <br/><span data-ttu-id="2ea79-202">S’il existe un **ETag** incompatibilité, une erreur est consignée toohello du journal.</span><span class="sxs-lookup"><span data-stu-id="2ea79-202">If there is an **ETag** mismatch, an error is written toohello log file.</span></span> |
| <span data-ttu-id="2ea79-203">**createOrUpdateIfMatchETag**</span><span class="sxs-lookup"><span data-stu-id="2ea79-203">**createOrUpdateIfMatchETag**</span></span> |<span data-ttu-id="2ea79-204">Si un appareil avec hello spécifié n’existe pas **id**, il est nouvellement inscrit.</span><span class="sxs-lookup"><span data-stu-id="2ea79-204">If a device does not exist with hello specified **id**, it is newly registered.</span></span> <br/><span data-ttu-id="2ea79-205">Si l’appareil de hello existe déjà, informations existantes sont remplacées par hello a fourni des données d’entrée uniquement s’il existe un **ETag** correspondent.</span><span class="sxs-lookup"><span data-stu-id="2ea79-205">If hello device already exists, existing information is overwritten with hello provided input data only if there is an **ETag** match.</span></span> <br/><span data-ttu-id="2ea79-206">S’il existe un **ETag** incompatibilité, une erreur est consignée toohello du journal.</span><span class="sxs-lookup"><span data-stu-id="2ea79-206">If there is an **ETag** mismatch, an error is written toohello log file.</span></span> <br> <span data-ttu-id="2ea79-207">utilisateur de Hello peut éventuellement spécifier des données de double en même temps que les données de l’appareil hello.</span><span class="sxs-lookup"><span data-stu-id="2ea79-207">hello user can optionally specify twin data along with hello device data.</span></span> <span data-ttu-id="2ea79-208">etag du double Hello si spécifié, est traitée indépendamment de l’etag de l’appareil hello.</span><span class="sxs-lookup"><span data-stu-id="2ea79-208">hello twin’s etag, if specified, is processed independently from hello device’s etag.</span></span> <span data-ttu-id="2ea79-209">S’il existe une incompatibilité avec les etag du double hello existant, une erreur est consignée toohello du journal.</span><span class="sxs-lookup"><span data-stu-id="2ea79-209">If there is a mismatch with hello existing twin’s etag, an error is written toohello log file.</span></span> |
| <span data-ttu-id="2ea79-210">**delete**</span><span class="sxs-lookup"><span data-stu-id="2ea79-210">**delete**</span></span> |<span data-ttu-id="2ea79-211">Si un appareil existe déjà avec hello spécifié **id**, il est supprimé sans se soucier des toohello **ETag** valeur.</span><span class="sxs-lookup"><span data-stu-id="2ea79-211">If a device already exists with hello specified **id**, it is deleted without regard toohello **ETag** value.</span></span> <br/><span data-ttu-id="2ea79-212">Si l’appareil de hello n’existe pas, une erreur est consignée toohello du journal.</span><span class="sxs-lookup"><span data-stu-id="2ea79-212">If hello device does not exist, an error is written toohello log file.</span></span> |
| <span data-ttu-id="2ea79-213">**deleteIfMatchETag**</span><span class="sxs-lookup"><span data-stu-id="2ea79-213">**deleteIfMatchETag**</span></span> |<span data-ttu-id="2ea79-214">Si un appareil existe déjà avec hello spécifié **id**, il est supprimé uniquement s’il existe un **ETag** correspondent.</span><span class="sxs-lookup"><span data-stu-id="2ea79-214">If a device already exists with hello specified **id**, it is deleted only if there is an **ETag** match.</span></span> <span data-ttu-id="2ea79-215">Si l’appareil de hello n’existe pas, une erreur est consignée toohello du journal.</span><span class="sxs-lookup"><span data-stu-id="2ea79-215">If hello device does not exist, an error is written toohello log file.</span></span> <br/><span data-ttu-id="2ea79-216">S’il existe une non-correspondance d’ETag, une erreur est consignée toohello du journal.</span><span class="sxs-lookup"><span data-stu-id="2ea79-216">If there is an ETag mismatch, an error is written toohello log file.</span></span> |

> [!NOTE]
> <span data-ttu-id="2ea79-217">Si les données de sérialisation hello ne définissent pas explicitement un **importMode** indicateur pour un périphérique, la valeur par défaut trop**createOrUpdate** hello lors de l’opération d’importation.</span><span class="sxs-lookup"><span data-stu-id="2ea79-217">If hello serialization data does not explicitly define an **importMode** flag for a device, it defaults too**createOrUpdate** during hello import operation.</span></span>

## <a name="import-devices-example--bulk-device-provisioning"></a><span data-ttu-id="2ea79-218">Exemple d’importation d’appareils : approvisionnement d’appareils en bloc</span><span class="sxs-lookup"><span data-stu-id="2ea79-218">Import devices example – bulk device provisioning</span></span>

<span data-ttu-id="2ea79-219">Hello exemple de code c# suivant illustre comment toogenerate plusieurs identités d’appareil qui :</span><span class="sxs-lookup"><span data-stu-id="2ea79-219">hello following C# code sample illustrates how toogenerate multiple device identities that:</span></span>

* <span data-ttu-id="2ea79-220">Comprennent des clés d’authentification.</span><span class="sxs-lookup"><span data-stu-id="2ea79-220">Include authentication keys.</span></span>
* <span data-ttu-id="2ea79-221">Cet objet blob de blocs appareil informations tooa d’écriture.</span><span class="sxs-lookup"><span data-stu-id="2ea79-221">Write that device information tooa block blob.</span></span>
* <span data-ttu-id="2ea79-222">Importer des appareils hello dans le Registre des identités hello.</span><span class="sxs-lookup"><span data-stu-id="2ea79-222">Import hello devices into hello identity registry.</span></span>

```csharp
// Provision 1,000 more devices
var serializedDevices = new List<string>();

for (var i = 0; i < 1000; i++)
{
  // Create a new ExportImportDevice
  // CryptoKeyGenerator is in hello Microsoft.Azure.Devices.Common namespace
  var deviceToAdd = new ExportImportDevice()
  {
    Id = Guid.NewGuid().ToString(),
    Status = DeviceStatus.Enabled,
    Authentication = new AuthenticationMechanism()
    {
      SymmetricKey = new SymmetricKey()
      {
        PrimaryKey = CryptoKeyGenerator.GenerateKey(32),
        SecondaryKey = CryptoKeyGenerator.GenerateKey(32)
      }
    },
    ImportMode = ImportMode.Create
  };

  // Add device toohello list
  serializedDevices.Add(JsonConvert.SerializeObject(deviceToAdd));
}

// Write hello list toohello blob
var sb = new StringBuilder();
serializedDevices.ForEach(serializedDevice => sb.AppendLine(serializedDevice));
await blob.DeleteIfExistsAsync();

using (CloudBlobStream stream = await blob.OpenWriteAsync())
{
  byte[] bytes = Encoding.UTF8.GetBytes(sb.ToString());
  for (var i = 0; i < bytes.Length; i += 500)
  {
    int length = Math.Min(bytes.Length - i, 500);
    await stream.WriteAsync(bytes, i, length);
  }
}

// Call import using hello blob tooadd new devices
// Log information related toohello job is written toohello same container
// This normally takes 1 minute per 100 devices
JobProperties importJob = await registryManager.ImportDevicesAsync(containerSasUri, containerSasUri);

// Wait until job is finished
while(true)
{
  importJob = await registryManager.GetJobAsync(importJob.JobId);
  if (importJob.Status == JobStatus.Completed || 
      importJob.Status == JobStatus.Failed ||
      importJob.Status == JobStatus.Cancelled)
  {
    // Job has finished executing
    break;
  }

  await Task.Delay(TimeSpan.FromSeconds(5));
}
```

## <a name="import-devices-example--bulk-deletion"></a><span data-ttu-id="2ea79-223">Exemple d’importation d’appareils : suppression en bloc</span><span class="sxs-lookup"><span data-stu-id="2ea79-223">Import devices example – bulk deletion</span></span>

<span data-ttu-id="2ea79-224">Hello exemple de code suivant montre comment les appareils hello toodelete de que vous avez ajouté à l’aide hello exemple de code précédent :</span><span class="sxs-lookup"><span data-stu-id="2ea79-224">hello following code sample shows you how toodelete hello devices you added using hello previous code sample:</span></span>

```csharp
// Step 1: Update each device's ImportMode toobe Delete
sb = new StringBuilder();
serializedDevices.ForEach(serializedDevice =>
{
  // Deserialize back tooan ExportImportDevice
  var device = JsonConvert.DeserializeObject<ExportImportDevice>(serializedDevice);

  // Update property
  device.ImportMode = ImportMode.Delete;

  // Re-serialize
  sb.AppendLine(JsonConvert.SerializeObject(device));
});

// Step 2: Write hello new import data back toohello block blob
await blob.DeleteIfExistsAsync();
using (CloudBlobStream stream = await blob.OpenWriteAsync())
{
  byte[] bytes = Encoding.UTF8.GetBytes(sb.ToString());
  for (var i = 0; i < bytes.Length; i += 500)
  {
    int length = Math.Min(bytes.Length - i, 500);
    await stream.WriteAsync(bytes, i, length);
  }
}

// Step 3: Call import using hello same blob toodelete all devices
importJob = await registryManager.ImportDevicesAsync(containerSasUri, containerSasUri);

// Wait until job is finished
while(true)
{
  importJob = await registryManager.GetJobAsync(importJob.JobId);
  if (importJob.Status == JobStatus.Completed || 
      importJob.Status == JobStatus.Failed ||
      importJob.Status == JobStatus.Cancelled)
  {
    // Job has finished executing
    break;
  }

  await Task.Delay(TimeSpan.FromSeconds(5));
}
```

## <a name="get-hello-container-sas-uri"></a><span data-ttu-id="2ea79-225">Obtenir le conteneur de hello URI SAS</span><span class="sxs-lookup"><span data-stu-id="2ea79-225">Get hello container SAS URI</span></span>

<span data-ttu-id="2ea79-226">Hello exemple de code suivant vous montre comment toogenerate un [URI SAS](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md) en lecture, écriture et suppression des autorisations pour un conteneur d’objets blob :</span><span class="sxs-lookup"><span data-stu-id="2ea79-226">hello following code sample shows you how toogenerate a [SAS URI](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md) with read, write, and delete permissions for a blob container:</span></span>

```csharp
static string GetContainerSasUri(CloudBlobContainer container)
{
  // Set hello expiry time and permissions for hello container.
  // In this case no start time is specified, so the
  // shared access signature becomes valid immediately.
  var sasConstraints = new SharedAccessBlobPolicy();
  sasConstraints.SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24);
  sasConstraints.Permissions = 
    SharedAccessBlobPermissions.Write | 
    SharedAccessBlobPermissions.Read | 
    SharedAccessBlobPermissions.Delete;

  // Generate hello shared access signature on hello container,
  // setting hello constraints directly on hello signature.
  string sasContainerToken = container.GetSharedAccessSignature(sasConstraints);

  // Return hello URI string for hello container,
  // including hello SAS token.
  return container.Uri + sasContainerToken;
}
```

## <a name="next-steps"></a><span data-ttu-id="2ea79-227">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="2ea79-227">Next steps</span></span>

<span data-ttu-id="2ea79-228">Dans cet article, vous avez appris comment tooperform en bloc des opérations sur le Registre des identités hello dans un hub IoT.</span><span class="sxs-lookup"><span data-stu-id="2ea79-228">In this article, you learned how tooperform bulk operations against hello identity registry in an IoT hub.</span></span> <span data-ttu-id="2ea79-229">Suivez ces liens de toolearn plus d’informations sur la gestion de Azure IoT Hub :</span><span class="sxs-lookup"><span data-stu-id="2ea79-229">Follow these links toolearn more about managing Azure IoT Hub:</span></span>

* <span data-ttu-id="2ea79-230">[Métriques d’IoT Hub][lnk-metrics]</span><span class="sxs-lookup"><span data-stu-id="2ea79-230">[IoT Hub metrics][lnk-metrics]</span></span>
* <span data-ttu-id="2ea79-231">[Surveillance des opérations][lnk-monitor]</span><span class="sxs-lookup"><span data-stu-id="2ea79-231">[Operations monitoring][lnk-monitor]</span></span>

<span data-ttu-id="2ea79-232">toofurther Explorez les fonctionnalités de hello d’IoT Hub, consultez :</span><span class="sxs-lookup"><span data-stu-id="2ea79-232">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="2ea79-233">[Guide du développeur IoT Hub][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="2ea79-233">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="2ea79-234">[Simulation d’un appareil avec IoT Edge][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="2ea79-234">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>

[lnk-metrics]: iot-hub-metrics.md
[lnk-monitor]: iot-hub-operations-monitoring.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
