---
title: "Importer/exporter des identités d’appareil Azure IoT Hub | Microsoft Docs"
description: "Utilisation du Kit de développement logiciel (SDK) de service Azure IoT pour effectuer des opérations en bloc dans le registre des identités pour importer et exporter les identités des appareils. Les opérations d’importation vous permettent de créer, de mettre à jour et de supprimer des identités d’appareils en bloc."
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
ms.openlocfilehash: ad2c6d585eef5450f7f0912ffa4753fe80d86b37
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="manage-your-iot-hub-device-identities-in-bulk"></a><span data-ttu-id="4ea00-104">Gestion de vos identités d’appareil IoT Hub en bloc</span><span class="sxs-lookup"><span data-stu-id="4ea00-104">Manage your IoT Hub device identities in bulk</span></span>

<span data-ttu-id="4ea00-105">Chaque IoT Hub a un registre des identités que vous pouvez utiliser pour créer des ressources par appareil dans le service.</span><span class="sxs-lookup"><span data-stu-id="4ea00-105">Each IoT hub has an identity registry you can use to create per-device resources in the service.</span></span> <span data-ttu-id="4ea00-106">Le registre des identités vous permet également de contrôler l’accès aux points de terminaison orientés appareil.</span><span class="sxs-lookup"><span data-stu-id="4ea00-106">The identity registry also enables you to control access to the device-facing endpoints.</span></span> <span data-ttu-id="4ea00-107">Cet article explique comment importer et exporter les identités des appareils en bloc vers et à partir d’un registre des identités.</span><span class="sxs-lookup"><span data-stu-id="4ea00-107">This article describes how to import and export device identities in bulk to and from an identity registry.</span></span>

<span data-ttu-id="4ea00-108">Les opérations d’importation et d’exportation se déroulent dans le cadre de *Tâches* , qui vous permettent d’exécuter des opérations de service en bloc par rapport à un IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="4ea00-108">Import and export operations take place in the context of *Jobs* that enable you to execute bulk service operations against an IoT hub.</span></span>

<span data-ttu-id="4ea00-109">La classe **RegistryManager** comprend les méthodes **ExportDevicesAsync** et **ImportDevicesAsync**, qui utilisent l’infrastructure des **tâches**.</span><span class="sxs-lookup"><span data-stu-id="4ea00-109">The **RegistryManager** class includes the **ExportDevicesAsync** and **ImportDevicesAsync** methods that use the **Job** framework.</span></span> <span data-ttu-id="4ea00-110">Ces méthodes vous permettent d’exporter, d’importer et de synchroniser l’intégralité d’un registre des identités IoT hub.</span><span class="sxs-lookup"><span data-stu-id="4ea00-110">These methods enable you to export, import, and synchronize the entirety of an IoT hub identity registry.</span></span>

## <a name="what-are-jobs"></a><span data-ttu-id="4ea00-111">Que sont les tâches ?</span><span class="sxs-lookup"><span data-stu-id="4ea00-111">What are jobs?</span></span>

<span data-ttu-id="4ea00-112">Les opérations de registre des identités utilisent le système de **tâches** lorsque l’opération :</span><span class="sxs-lookup"><span data-stu-id="4ea00-112">Identity registry operations use the **Job** system when the operation:</span></span>

* <span data-ttu-id="4ea00-113">a un temps d’exécution potentiellement long par rapport à une opération d’exécution standard.</span><span class="sxs-lookup"><span data-stu-id="4ea00-113">Has a potentially long execution time compared to standard run-time operations.</span></span>
* <span data-ttu-id="4ea00-114">renvoie une grande quantité de données à l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="4ea00-114">Returns a large amount of data to the user.</span></span>

<span data-ttu-id="4ea00-115">Au lieu d’avoir un seul appel d’API en attente ou qui se bloque sur le résultat de l’opération, l’opération crée de façon asynchrone un **travail** pour cet IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="4ea00-115">Instead of a single API call waiting or blocking on the result of the operation, the operation asynchronously creates a **Job** for that IoT hub.</span></span> <span data-ttu-id="4ea00-116">L’opération renvoie alors immédiatement un objet **JobProperties**.</span><span class="sxs-lookup"><span data-stu-id="4ea00-116">The operation then immediately returns a **JobProperties** object.</span></span>

<span data-ttu-id="4ea00-117">L’extrait de code C# suivant indique comment créer une tâche d’exportation :</span><span class="sxs-lookup"><span data-stu-id="4ea00-117">The following C# code snippet shows how to create an export job:</span></span>

```csharp
// Call an export job on the IoT Hub to retrieve all devices
JobProperties exportJob = await registryManager.ExportDevicesAsync(containerSasUri, false);
```

> [!NOTE]
> <span data-ttu-id="4ea00-118">Pour utiliser la classe **RegistryManager** dans votre code C#, ajoutez le package NuGet **Microsoft.Azure.Devices** à votre projet.</span><span class="sxs-lookup"><span data-stu-id="4ea00-118">To use the **RegistryManager** class in your C# code, add the **Microsoft.Azure.Devices** NuGet package to your project.</span></span> <span data-ttu-id="4ea00-119">La classe **RegistryManager** se trouve dans l’espace de noms **Microsoft.Azure.Devices**.</span><span class="sxs-lookup"><span data-stu-id="4ea00-119">The **RegistryManager** class is in the **Microsoft.Azure.Devices** namespace.</span></span>

<span data-ttu-id="4ea00-120">Vous pouvez utiliser la classe **RegistryManager** pour interroger l’état de la **tâche** à l’aide des métadonnées **JobProperties** retournées.</span><span class="sxs-lookup"><span data-stu-id="4ea00-120">You can use the **RegistryManager** class to query the state of the **Job** using the returned **JobProperties** metadata.</span></span>

<span data-ttu-id="4ea00-121">L’extrait de code C# suivant indique comment envoyer des interrogations toutes les cinq secondes pour voir si la tâche a terminé son exécution :</span><span class="sxs-lookup"><span data-stu-id="4ea00-121">The following C# code snippet shows how to poll every five seconds to see if the job has finished executing:</span></span>

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

## <a name="export-devices"></a><span data-ttu-id="4ea00-122">Exporter des appareils</span><span class="sxs-lookup"><span data-stu-id="4ea00-122">Export devices</span></span>

<span data-ttu-id="4ea00-123">Utilisez la méthode **ExportDevicesAsync** pour exporter l’intégralité d’un registre des identités IoT Hub vers un conteneur d’objets blob [Azure Storage](../storage/index.md) à l’aide d’une [signature d’accès partagé](../storage/common/storage-security-guide.md#data-plane-security).</span><span class="sxs-lookup"><span data-stu-id="4ea00-123">Use the **ExportDevicesAsync** method to export the entirety of an IoT hub identity registry to an [Azure Storage](../storage/index.md) blob container using a [Shared Access Signature](../storage/common/storage-security-guide.md#data-plane-security).</span></span>

<span data-ttu-id="4ea00-124">Cette méthode vous permet de créer des sauvegardes fiables de vos informations d’appareil dans un conteneur d’objets blob que vous contrôlez.</span><span class="sxs-lookup"><span data-stu-id="4ea00-124">This method enables you to create reliable backups of your device information in a blob container that you control.</span></span>

<span data-ttu-id="4ea00-125">La méthode **ExportDevicesAsync** requiert deux paramètres :</span><span class="sxs-lookup"><span data-stu-id="4ea00-125">The **ExportDevicesAsync** method requires two parameters:</span></span>

* <span data-ttu-id="4ea00-126">Une *chaîne* qui contient l’URI d’un conteneur d’objets blob.</span><span class="sxs-lookup"><span data-stu-id="4ea00-126">A *string* that contains a URI of a blob container.</span></span> <span data-ttu-id="4ea00-127">Cet URI doit contenir un jeton SAP, qui accorde l’accès en écriture au conteneur.</span><span class="sxs-lookup"><span data-stu-id="4ea00-127">This URI must contain a SAS token that grants write access to the container.</span></span> <span data-ttu-id="4ea00-128">La tâche crée un objet blob de blocs dans ce conteneur pour stocker les données d’exportation d’appareil sérialisées.</span><span class="sxs-lookup"><span data-stu-id="4ea00-128">The job creates a block blob in this container to store the serialized export device data.</span></span> <span data-ttu-id="4ea00-129">Le jeton SAP doit inclure ces autorisations :</span><span class="sxs-lookup"><span data-stu-id="4ea00-129">The SAS token must include these permissions:</span></span>

   ```csharp
   SharedAccessBlobPermissions.Write | SharedAccessBlobPermissions.Read | SharedAccessBlobPermissions.Delete
   ```

* <span data-ttu-id="4ea00-130">Un *booléen* qui indique si vous souhaitez exclure les clés d’authentification de vos données d’exportation.</span><span class="sxs-lookup"><span data-stu-id="4ea00-130">A *boolean* that indicates if you want to exclude authentication keys from your export data.</span></span> <span data-ttu-id="4ea00-131">Si la valeur est **false**, des clés d’authentification sont incluses dans la sortie d’exportation.</span><span class="sxs-lookup"><span data-stu-id="4ea00-131">If **false**, authentication keys are included in export output.</span></span> <span data-ttu-id="4ea00-132">Dans le cas contraire, les clés sont exportées sous forme de valeur **null**.</span><span class="sxs-lookup"><span data-stu-id="4ea00-132">Otherwise, keys are exported as **null**.</span></span>

<span data-ttu-id="4ea00-133">L’extrait de code C# suivant montre comment lancer une tâche d’exportation qui inclut des clés d’authentification de l’appareil dans les données d’exportation, puis comment interroger l’exécution :</span><span class="sxs-lookup"><span data-stu-id="4ea00-133">The following C# code snippet shows how to initiate an export job that includes device authentication keys in the export data and then poll for completion:</span></span>

```csharp
// Call an export job on the IoT Hub to retrieve all devices
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

<span data-ttu-id="4ea00-134">La tâche stocke sa sortie dans le conteneur d’objets blob fourni en tant qu’objet blob de blocs portant le nom **devices.txt**.</span><span class="sxs-lookup"><span data-stu-id="4ea00-134">The job stores its output in the provided blob container as a block blob with the name **devices.txt**.</span></span> <span data-ttu-id="4ea00-135">Les données de sortie consistent en des données d’appareil JSON sérialisées, avec un appareil par ligne.</span><span class="sxs-lookup"><span data-stu-id="4ea00-135">The output data consists of JSON serialized device data, with one device per line.</span></span>

<span data-ttu-id="4ea00-136">L’exemple ci-après illustre les données de sortie :</span><span class="sxs-lookup"><span data-stu-id="4ea00-136">The following example shows the output data:</span></span>

```json
{"id":"Device1","eTag":"MA==","status":"enabled","authentication":{"symmetricKey":{"primaryKey":"abc=","secondaryKey":"def="}}}
{"id":"Device2","eTag":"MA==","status":"enabled","authentication":{"symmetricKey":{"primaryKey":"abc=","secondaryKey":"def="}}}
{"id":"Device3","eTag":"MA==","status":"disabled","authentication":{"symmetricKey":{"primaryKey":"abc=","secondaryKey":"def="}}}
{"id":"Device4","eTag":"MA==","status":"disabled","authentication":{"symmetricKey":{"primaryKey":"abc=","secondaryKey":"def="}}}
{"id":"Device5","eTag":"MA==","status":"enabled","authentication":{"symmetricKey":{"primaryKey":"abc=","secondaryKey":"def="}}}
```

Si un appareil comporte des données de représentation, elles sont également exportées avec les données de l’appareil. L’exemple ci-après illustre ce format. <span data-ttu-id="4ea00-139">Toutes les données à partir de la ligne « twinETag » jusqu'à la fin sont des données de représentation.</span><span class="sxs-lookup"><span data-stu-id="4ea00-139">All data from the "twinETag" line until the end are twin data.</span></span>

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

<span data-ttu-id="4ea00-140">Si vous avez besoin d’accéder à ces données sous forme de code, vous pouvez facilement désérialiser ces données à l’aide de la classe **ExportImportDevice** .</span><span class="sxs-lookup"><span data-stu-id="4ea00-140">If you need access to this data in code, you can easily deserialize this data using the **ExportImportDevice** class.</span></span> <span data-ttu-id="4ea00-141">L’extrait de code C# suivant montre comment lire les informations d’appareil qui ont été exportées précédemment vers un objet blob de bloc :</span><span class="sxs-lookup"><span data-stu-id="4ea00-141">The following C# code snippet shows how to read device information that was previously exported to a block blob:</span></span>

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
> <span data-ttu-id="4ea00-142">Vous pouvez également utiliser la méthode **GetDevicesAsync** de la classe **RegistryManager** pour extraire une liste de vos appareils.</span><span class="sxs-lookup"><span data-stu-id="4ea00-142">You can also use the **GetDevicesAsync** method of the **RegistryManager** class to fetch a list of your devices.</span></span> <span data-ttu-id="4ea00-143">Toutefois, cette approche a une capacité stricte de 1 000 en ce qui concerne le nombre d’objets d’appareil renvoyés.</span><span class="sxs-lookup"><span data-stu-id="4ea00-143">However, this approach has a hard cap of 1000 on the number of device objects that are returned.</span></span> <span data-ttu-id="4ea00-144">La méthode **GetDevicesAsync** est surtout envisagée pour l’aide au débogage lors de scénarios de développement. Elle n’est pas recommandée pour les charges de travail de production.</span><span class="sxs-lookup"><span data-stu-id="4ea00-144">The expected use case for the **GetDevicesAsync** method is for development scenarios to aid debugging and is not recommended for production workloads.</span></span>

## <a name="import-devices"></a><span data-ttu-id="4ea00-145">Importer des appareils</span><span class="sxs-lookup"><span data-stu-id="4ea00-145">Import devices</span></span>

<span data-ttu-id="4ea00-146">La méthode **ImportDevicesAsync** de la classe **RegistryManager** vous permet d’effectuer des opérations d’importation et de synchronisation en bloc dans un registre des identités IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="4ea00-146">The **ImportDevicesAsync** method in the **RegistryManager** class enables you to perform bulk import and synchronization operations in an IoT hub identity registry.</span></span> <span data-ttu-id="4ea00-147">À la manière de la méthode **ExportDevicesAsync**, la méthode **ImportDevicesAsync** utilise l’infrastructure de **Tâches**.</span><span class="sxs-lookup"><span data-stu-id="4ea00-147">Like the **ExportDevicesAsync** method, the **ImportDevicesAsync** method uses the **Job** framework.</span></span>

<span data-ttu-id="4ea00-148">Faites attention lors de l’utilisation de la méthode **ImportDevicesAsync**. Celle-ci peut, en plus d’approvisionner de nouveaux appareils dans le registre des identités, mettre à jour et supprimer des appareils existants.</span><span class="sxs-lookup"><span data-stu-id="4ea00-148">Take care using the **ImportDevicesAsync** method because in addition to provisioning new devices in your identity registry, it can also update and delete existing devices.</span></span>

> [!WARNING]
> <span data-ttu-id="4ea00-149">Il est impossible d’annuler une opération d’importation.</span><span class="sxs-lookup"><span data-stu-id="4ea00-149">An import operation cannot be undone.</span></span> <span data-ttu-id="4ea00-150">Sauvegardez toujours vos données existantes vers un autre conteneur d’objets blob, à l’aide de la méthode **ExportDevicesAsync**, avant de faire des modifications en bloc dans le registre des identités.</span><span class="sxs-lookup"><span data-stu-id="4ea00-150">Always back up your existing data using the **ExportDevicesAsync** method to another blob container before you make bulk changes to your identity registry.</span></span>

<span data-ttu-id="4ea00-151">La méthode **ImportDevicesAsync** requiert deux paramètres :</span><span class="sxs-lookup"><span data-stu-id="4ea00-151">The **ImportDevicesAsync** method takes two parameters:</span></span>

* <span data-ttu-id="4ea00-152">Une *chaîne* qui contient l’URI d’un conteneur d’objets blob [Azure Storage](../storage/index.md) à utiliser comme *entrée* de la tâche.</span><span class="sxs-lookup"><span data-stu-id="4ea00-152">A *string* that contains a URI of an [Azure Storage](../storage/index.md) blob container to use as *input* to the job.</span></span> <span data-ttu-id="4ea00-153">Cet URI doit contenir un jeton SAP qui accorde l’accès en lecture au conteneur.</span><span class="sxs-lookup"><span data-stu-id="4ea00-153">This URI must contain a SAS token that grants read access to the container.</span></span> <span data-ttu-id="4ea00-154">Ce conteneur doit inclure un objet blob du nom de **devices.txt** contenant les données d’appareil sérialisées pour importation dans le registre des identités.</span><span class="sxs-lookup"><span data-stu-id="4ea00-154">This container must contain a blob with the name **devices.txt** that contains the serialized device data to import into your identity registry.</span></span> <span data-ttu-id="4ea00-155">Les données d’importation doivent contenir des informations sur l’appareil au même format JSON que celui utilisé par la tâche **ExportImportDevice** lors de la création d’un objet blob **devices.txt**.</span><span class="sxs-lookup"><span data-stu-id="4ea00-155">The import data must contain device information in the same JSON format that the **ExportImportDevice** job uses when it creates a **devices.txt** blob.</span></span> <span data-ttu-id="4ea00-156">Le jeton SAP doit inclure ces autorisations :</span><span class="sxs-lookup"><span data-stu-id="4ea00-156">The SAS token must include these permissions:</span></span>

   ```csharp
   SharedAccessBlobPermissions.Read
   ```
* <span data-ttu-id="4ea00-157">Une *chaîne* qui contient l’URI d’un conteneur d’objets blob [Azure Storage](https://azure.microsoft.com/documentation/services/storage/) à utiliser comme *sortie* de la tâche.</span><span class="sxs-lookup"><span data-stu-id="4ea00-157">A *string* that contains a URI of an [Azure Storage](https://azure.microsoft.com/documentation/services/storage/) blob container to use as *output* from the job.</span></span> <span data-ttu-id="4ea00-158">La tâche crée un objet blob de blocs dans ce conteneur pour stocker toute information d’erreur à partir de la **tâche**d’importation terminée.</span><span class="sxs-lookup"><span data-stu-id="4ea00-158">The job creates a block blob in this container to store any error information from the completed import **Job**.</span></span> <span data-ttu-id="4ea00-159">Le jeton SAP doit inclure ces autorisations :</span><span class="sxs-lookup"><span data-stu-id="4ea00-159">The SAS token must include these permissions:</span></span>

   ```csharp
   SharedAccessBlobPermissions.Write | SharedAccessBlobPermissions.Read | SharedAccessBlobPermissions.Delete
   ```

> [!NOTE]
> <span data-ttu-id="4ea00-160">Les deux paramètres peuvent pointer vers le même conteneur d’objets blob.</span><span class="sxs-lookup"><span data-stu-id="4ea00-160">The two parameters can point to the same blob container.</span></span> <span data-ttu-id="4ea00-161">Les paramètres distincts permettent simplement davantage de contrôle sur vos données, étant donné que le conteneur de sortie requiert des autorisations supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="4ea00-161">The separate parameters simply enable more control over your data as the output container requires additional permissions.</span></span>

<span data-ttu-id="4ea00-162">L’extrait de code C# suivant indique comment créer une tâche d’importation :</span><span class="sxs-lookup"><span data-stu-id="4ea00-162">The following C# code snippet shows how to initiate an import job:</span></span>

```csharp
JobProperties importJob = await registryManager.ImportDevicesAsync(containerSasUri, containerSasUri);
```

<span data-ttu-id="4ea00-163">Cette méthode peut également être utilisée pour importer les données pour la représentation de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="4ea00-163">This method can also be used to import the data for the device twin.</span></span> <span data-ttu-id="4ea00-164">Le format des données d’entrée est le même que celui indiqué dans la section **ExportDevicesAsync**.</span><span class="sxs-lookup"><span data-stu-id="4ea00-164">The format for the data input is the same as the format shown in the **ExportDevicesAsync** section.</span></span> <span data-ttu-id="4ea00-165">De cette façon, vous pouvez réimporter les données exportées.</span><span class="sxs-lookup"><span data-stu-id="4ea00-165">In this way, you can reimport the exported data.</span></span> <span data-ttu-id="4ea00-166">Le **$metadata** est facultatif.</span><span class="sxs-lookup"><span data-stu-id="4ea00-166">The **$metadata** is optional.</span></span>

## <a name="import-behavior"></a><span data-ttu-id="4ea00-167">Comportement d’importation</span><span class="sxs-lookup"><span data-stu-id="4ea00-167">Import behavior</span></span>

<span data-ttu-id="4ea00-168">Vous pouvez utiliser la méthode **ImportDevicesAsync** pour effectuer les opérations en bloc suivantes dans le registre des identités :</span><span class="sxs-lookup"><span data-stu-id="4ea00-168">You can use the **ImportDevicesAsync** method to perform the following bulk operations in your identity registry:</span></span>

* <span data-ttu-id="4ea00-169">Inscription en bloc de nouveaux appareils</span><span class="sxs-lookup"><span data-stu-id="4ea00-169">Bulk registration of new devices</span></span>
* <span data-ttu-id="4ea00-170">Suppression en bloc d’appareils existants</span><span class="sxs-lookup"><span data-stu-id="4ea00-170">Bulk deletions of existing devices</span></span>
* <span data-ttu-id="4ea00-171">Modifications d’état en bloc (activer ou désactiver des appareils)</span><span class="sxs-lookup"><span data-stu-id="4ea00-171">Bulk status changes (enable or disable devices)</span></span>
* <span data-ttu-id="4ea00-172">Attribution en bloc de nouvelles clés d’authentification d’appareils</span><span class="sxs-lookup"><span data-stu-id="4ea00-172">Bulk assignment of new device authentication keys</span></span>
* <span data-ttu-id="4ea00-173">Auto-régénération en bloc des clés d’authentification d’appareils</span><span class="sxs-lookup"><span data-stu-id="4ea00-173">Bulk auto-regeneration of device authentication keys</span></span>
* <span data-ttu-id="4ea00-174">Mise à jour en bloc de données de représentation</span><span class="sxs-lookup"><span data-stu-id="4ea00-174">Bulk update of twin data</span></span>

<span data-ttu-id="4ea00-175">Vous pouvez effectuer n’importe quelle combinaison des opérations précédentes en un seul appel **ImportDevicesAsync** .</span><span class="sxs-lookup"><span data-stu-id="4ea00-175">You can perform any combination of the preceding operations within a single **ImportDevicesAsync** call.</span></span> <span data-ttu-id="4ea00-176">Vous pouvez, par exemple, inscrire de nouveaux appareils, tout en supprimant ou mettant à jour des appareils existants.</span><span class="sxs-lookup"><span data-stu-id="4ea00-176">For example, you can register new devices and delete or update existing devices at the same time.</span></span> <span data-ttu-id="4ea00-177">Lorsqu’il est utilisé avec la méthode **ExportDevicesAsync** , tous les appareils peuvent être migrés complètement à partir d’un IoT Hub vers un autre.</span><span class="sxs-lookup"><span data-stu-id="4ea00-177">When used along with the **ExportDevicesAsync** method, you can completely migrate all your devices from one IoT hub to another.</span></span>

<span data-ttu-id="4ea00-178">Si le fichier d’importation inclut les métadonnées de représentation, ces métadonnées remplacent les métadonnées de représentation existantes.</span><span class="sxs-lookup"><span data-stu-id="4ea00-178">If the import file includes twin metadata, then this metadata overwrites the existing twin metadata.</span></span> <span data-ttu-id="4ea00-179">Si le fichier d’importation n’inclut pas les métadonnées de représentation, seules les métadonnées `lastUpdateTime` sont mises à jour avec l’heure actuelle.</span><span class="sxs-lookup"><span data-stu-id="4ea00-179">If the import file does not include twin metadata, then only the `lastUpdateTime` metadata is updated using the current time.</span></span>

<span data-ttu-id="4ea00-180">Vous pouvez contrôler le processus d’importation par appareil en utilisant la propriété facultative **importMode** dans les données d’importation sérialisées pour chaque appareil.</span><span class="sxs-lookup"><span data-stu-id="4ea00-180">Use the optional **importMode** property in the import serialization data for each device to control the import process per-device.</span></span> <span data-ttu-id="4ea00-181">La propriété **importMode** propose les options suivantes :</span><span class="sxs-lookup"><span data-stu-id="4ea00-181">The **importMode** property has the following options:</span></span>

| <span data-ttu-id="4ea00-182">importMode</span><span class="sxs-lookup"><span data-stu-id="4ea00-182">importMode</span></span> | <span data-ttu-id="4ea00-183">Description</span><span class="sxs-lookup"><span data-stu-id="4ea00-183">Description</span></span> |
| --- | --- |
| <span data-ttu-id="4ea00-184">**createOrUpdate**</span><span class="sxs-lookup"><span data-stu-id="4ea00-184">**createOrUpdate**</span></span> |<span data-ttu-id="4ea00-185">Si un appareil n’existe pas avec l’ **ID**spécifié, ce dernier a été inscrit récemment.</span><span class="sxs-lookup"><span data-stu-id="4ea00-185">If a device does not exist with the specified **id**, it is newly registered.</span></span> <br/><span data-ttu-id="4ea00-186">Si l’appareil existe déjà, les informations existantes sont remplacées par les données d’entrée fournies, sans tenir compte de la valeur **ETag** .</span><span class="sxs-lookup"><span data-stu-id="4ea00-186">If the device already exists, existing information is overwritten with the provided input data without regard to the **ETag** value.</span></span> <br> <span data-ttu-id="4ea00-187">L’utilisateur peut éventuellement spécifier des données de représentation avec les données de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="4ea00-187">The user can optionally specify twin data along with the device data.</span></span> <span data-ttu-id="4ea00-188">L’etag de la représentation, si elle est spécifiée, est traitée indépendamment de l’etag de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="4ea00-188">The twin’s etag, if specified, is processed independently from the device’s etag.</span></span> <span data-ttu-id="4ea00-189">S’il existe une incompatibilité avec l’etag existant de la représentation, une erreur est consignée dans le fichier journal.</span><span class="sxs-lookup"><span data-stu-id="4ea00-189">If there is a mismatch with the existing twin’s etag, an error is written to the log file.</span></span> |
| <span data-ttu-id="4ea00-190">**create**</span><span class="sxs-lookup"><span data-stu-id="4ea00-190">**create**</span></span> |<span data-ttu-id="4ea00-191">Si un appareil n’existe pas avec l’ **ID**spécifié, ce dernier a été inscrit récemment.</span><span class="sxs-lookup"><span data-stu-id="4ea00-191">If a device does not exist with the specified **id**, it is newly registered.</span></span> <br/><span data-ttu-id="4ea00-192">Si l’appareil existe déjà, une erreur est consignée dans le fichier journal.</span><span class="sxs-lookup"><span data-stu-id="4ea00-192">If the device already exists, an error is written to the log file.</span></span> <br> <span data-ttu-id="4ea00-193">L’utilisateur peut éventuellement spécifier des données de représentation avec les données de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="4ea00-193">The user can optionally specify twin data along with the device data.</span></span> <span data-ttu-id="4ea00-194">L’etag de la représentation, si elle est spécifiée, est traitée indépendamment de l’etag de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="4ea00-194">The twin’s etag, if specified, is processed independently from the device’s etag.</span></span> <span data-ttu-id="4ea00-195">S’il existe une incompatibilité avec l’etag existant de la représentation, une erreur est consignée dans le fichier journal.</span><span class="sxs-lookup"><span data-stu-id="4ea00-195">If there is a mismatch with the existing twin’s etag, an error is written to the log file.</span></span> |
| <span data-ttu-id="4ea00-196">**update**</span><span class="sxs-lookup"><span data-stu-id="4ea00-196">**update**</span></span> |<span data-ttu-id="4ea00-197">Si un appareil avec **l’ID** spécifié existe déjà, les informations existantes sont remplacées par les données d’entrée fournies, sans tenir compte de la valeur **ETag**.</span><span class="sxs-lookup"><span data-stu-id="4ea00-197">If a device already exists with the specified **id**, existing information is overwritten with the provided input data without regard to the **ETag** value.</span></span> <br/><span data-ttu-id="4ea00-198">Si l’appareil n’existe pas, une erreur est consignée dans le fichier journal.</span><span class="sxs-lookup"><span data-stu-id="4ea00-198">If the device does not exist, an error is written to the log file.</span></span> |
| <span data-ttu-id="4ea00-199">**updateIfMatchETag**</span><span class="sxs-lookup"><span data-stu-id="4ea00-199">**updateIfMatchETag**</span></span> |<span data-ttu-id="4ea00-200">Si un appareil avec **l’ID** spécifié existe déjà, les informations existantes sont remplacées par les données d’entrée fournies, mais uniquement si la valeur **ETag** correspond.</span><span class="sxs-lookup"><span data-stu-id="4ea00-200">If a device already exists with the specified **id**, existing information is overwritten with the provided input data only if there is an **ETag** match.</span></span> <br/><span data-ttu-id="4ea00-201">Si l’appareil n’existe pas, une erreur est consignée dans le fichier journal.</span><span class="sxs-lookup"><span data-stu-id="4ea00-201">If the device does not exist, an error is written to the log file.</span></span> <br/><span data-ttu-id="4ea00-202">En cas d’incompatibilité de valeur **ETag** , une erreur est consignée dans le fichier journal.</span><span class="sxs-lookup"><span data-stu-id="4ea00-202">If there is an **ETag** mismatch, an error is written to the log file.</span></span> |
| <span data-ttu-id="4ea00-203">**createOrUpdateIfMatchETag**</span><span class="sxs-lookup"><span data-stu-id="4ea00-203">**createOrUpdateIfMatchETag**</span></span> |<span data-ttu-id="4ea00-204">Si un appareil n’existe pas avec l’ **ID**spécifié, ce dernier a été inscrit récemment.</span><span class="sxs-lookup"><span data-stu-id="4ea00-204">If a device does not exist with the specified **id**, it is newly registered.</span></span> <br/><span data-ttu-id="4ea00-205">Si un appareil existe déjà, les informations existantes sont remplacées par les données d’entrée fournies, mais uniquement si la valeur **ETag** correspond.</span><span class="sxs-lookup"><span data-stu-id="4ea00-205">If the device already exists, existing information is overwritten with the provided input data only if there is an **ETag** match.</span></span> <br/><span data-ttu-id="4ea00-206">En cas d’incompatibilité de valeur **ETag** , une erreur est consignée dans le fichier journal.</span><span class="sxs-lookup"><span data-stu-id="4ea00-206">If there is an **ETag** mismatch, an error is written to the log file.</span></span> <br> <span data-ttu-id="4ea00-207">L’utilisateur peut éventuellement spécifier des données de représentation avec les données de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="4ea00-207">The user can optionally specify twin data along with the device data.</span></span> <span data-ttu-id="4ea00-208">L’etag de la représentation, si elle est spécifiée, est traitée indépendamment de l’etag de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="4ea00-208">The twin’s etag, if specified, is processed independently from the device’s etag.</span></span> <span data-ttu-id="4ea00-209">S’il existe une incompatibilité avec l’etag existant de la représentation, une erreur est consignée dans le fichier journal.</span><span class="sxs-lookup"><span data-stu-id="4ea00-209">If there is a mismatch with the existing twin’s etag, an error is written to the log file.</span></span> |
| <span data-ttu-id="4ea00-210">**delete**</span><span class="sxs-lookup"><span data-stu-id="4ea00-210">**delete**</span></span> |<span data-ttu-id="4ea00-211">Si un appareil avec **l’ID** spécifié existe déjà, il est supprimé sans tenir compte de la valeur **ETag**.</span><span class="sxs-lookup"><span data-stu-id="4ea00-211">If a device already exists with the specified **id**, it is deleted without regard to the **ETag** value.</span></span> <br/><span data-ttu-id="4ea00-212">Si l’appareil n’existe pas, une erreur est consignée dans le fichier journal.</span><span class="sxs-lookup"><span data-stu-id="4ea00-212">If the device does not exist, an error is written to the log file.</span></span> |
| <span data-ttu-id="4ea00-213">**deleteIfMatchETag**</span><span class="sxs-lookup"><span data-stu-id="4ea00-213">**deleteIfMatchETag**</span></span> |<span data-ttu-id="4ea00-214">Si un appareil avec **l’ID** spécifié existe déjà, il est supprimé, mais uniquement si la valeur **ETag** correspond.</span><span class="sxs-lookup"><span data-stu-id="4ea00-214">If a device already exists with the specified **id**, it is deleted only if there is an **ETag** match.</span></span> <span data-ttu-id="4ea00-215">Si l’appareil n’existe pas, une erreur est consignée dans le fichier journal.</span><span class="sxs-lookup"><span data-stu-id="4ea00-215">If the device does not exist, an error is written to the log file.</span></span> <br/><span data-ttu-id="4ea00-216">En cas d’incompatibilité de valeur ETag, une erreur est consignée dans le fichier journal.</span><span class="sxs-lookup"><span data-stu-id="4ea00-216">If there is an ETag mismatch, an error is written to the log file.</span></span> |

> [!NOTE]
> <span data-ttu-id="4ea00-217">Si les données de sérialisation ne définissent pas explicitement un indicateur **importMode** pour un appareil donné, sa valeur par défaut sera **createOrUpdate** pendant l’opération d’importation.</span><span class="sxs-lookup"><span data-stu-id="4ea00-217">If the serialization data does not explicitly define an **importMode** flag for a device, it defaults to **createOrUpdate** during the import operation.</span></span>

## <a name="import-devices-example--bulk-device-provisioning"></a><span data-ttu-id="4ea00-218">Exemple d’importation d’appareils : approvisionnement d’appareils en bloc</span><span class="sxs-lookup"><span data-stu-id="4ea00-218">Import devices example – bulk device provisioning</span></span>

<span data-ttu-id="4ea00-219">L’exemple de code C# suivant illustre comment générer plusieurs identités d’appareil qui :</span><span class="sxs-lookup"><span data-stu-id="4ea00-219">The following C# code sample illustrates how to generate multiple device identities that:</span></span>

* <span data-ttu-id="4ea00-220">Comprennent des clés d’authentification.</span><span class="sxs-lookup"><span data-stu-id="4ea00-220">Include authentication keys.</span></span>
* <span data-ttu-id="4ea00-221">Écrivent ces informations d’appareil sur un objet blob de blocs.</span><span class="sxs-lookup"><span data-stu-id="4ea00-221">Write that device information to a block blob.</span></span>
* <span data-ttu-id="4ea00-222">Importent les appareils dans le registre des identités.</span><span class="sxs-lookup"><span data-stu-id="4ea00-222">Import the devices into the identity registry.</span></span>

```csharp
// Provision 1,000 more devices
var serializedDevices = new List<string>();

for (var i = 0; i < 1000; i++)
{
  // Create a new ExportImportDevice
  // CryptoKeyGenerator is in the Microsoft.Azure.Devices.Common namespace
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

  // Add device to the list
  serializedDevices.Add(JsonConvert.SerializeObject(deviceToAdd));
}

// Write the list to the blob
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

// Call import using the blob to add new devices
// Log information related to the job is written to the same container
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

## <a name="import-devices-example--bulk-deletion"></a><span data-ttu-id="4ea00-223">Exemple d’importation d’appareils : suppression en bloc</span><span class="sxs-lookup"><span data-stu-id="4ea00-223">Import devices example – bulk deletion</span></span>

<span data-ttu-id="4ea00-224">L’exemple de code suivant montre comment supprimer les appareils ajoutés à l’aide de l’exemple de code précédent :</span><span class="sxs-lookup"><span data-stu-id="4ea00-224">The following code sample shows you how to delete the devices you added using the previous code sample:</span></span>

```csharp
// Step 1: Update each device's ImportMode to be Delete
sb = new StringBuilder();
serializedDevices.ForEach(serializedDevice =>
{
  // Deserialize back to an ExportImportDevice
  var device = JsonConvert.DeserializeObject<ExportImportDevice>(serializedDevice);

  // Update property
  device.ImportMode = ImportMode.Delete;

  // Re-serialize
  sb.AppendLine(JsonConvert.SerializeObject(device));
});

// Step 2: Write the new import data back to the block blob
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

// Step 3: Call import using the same blob to delete all devices
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

## <a name="get-the-container-sas-uri"></a><span data-ttu-id="4ea00-225">Obtenir l’URI SAS du conteneur</span><span class="sxs-lookup"><span data-stu-id="4ea00-225">Get the container SAS URI</span></span>

<span data-ttu-id="4ea00-226">L’exemple de code suivant montre comment générer un [URI de SAP](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md) avec des autorisations de lecture, d’écriture et de suppression pour un conteneur d’objets blob :</span><span class="sxs-lookup"><span data-stu-id="4ea00-226">The following code sample shows you how to generate a [SAS URI](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md) with read, write, and delete permissions for a blob container:</span></span>

```csharp
static string GetContainerSasUri(CloudBlobContainer container)
{
  // Set the expiry time and permissions for the container.
  // In this case no start time is specified, so the
  // shared access signature becomes valid immediately.
  var sasConstraints = new SharedAccessBlobPolicy();
  sasConstraints.SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24);
  sasConstraints.Permissions = 
    SharedAccessBlobPermissions.Write | 
    SharedAccessBlobPermissions.Read | 
    SharedAccessBlobPermissions.Delete;

  // Generate the shared access signature on the container,
  // setting the constraints directly on the signature.
  string sasContainerToken = container.GetSharedAccessSignature(sasConstraints);

  // Return the URI string for the container,
  // including the SAS token.
  return container.Uri + sasContainerToken;
}
```

## <a name="next-steps"></a><span data-ttu-id="4ea00-227">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4ea00-227">Next steps</span></span>

<span data-ttu-id="4ea00-228">Dans cet article, vous avez appris comment effectuer des opérations en bloc dans le registre des identités dans un IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="4ea00-228">In this article, you learned how to perform bulk operations against the identity registry in an IoT hub.</span></span> <span data-ttu-id="4ea00-229">Suivez ces liens pour en savoir plus sur la gestion de Azure IoT Hub :</span><span class="sxs-lookup"><span data-stu-id="4ea00-229">Follow these links to learn more about managing Azure IoT Hub:</span></span>

* <span data-ttu-id="4ea00-230">[Métriques d’IoT Hub][lnk-metrics]</span><span class="sxs-lookup"><span data-stu-id="4ea00-230">[IoT Hub metrics][lnk-metrics]</span></span>
* <span data-ttu-id="4ea00-231">[Surveillance des opérations][lnk-monitor]</span><span class="sxs-lookup"><span data-stu-id="4ea00-231">[Operations monitoring][lnk-monitor]</span></span>

<span data-ttu-id="4ea00-232">Pour explorer davantage les capacités de IoT Hub, consultez :</span><span class="sxs-lookup"><span data-stu-id="4ea00-232">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="4ea00-233">[Guide du développeur IoT Hub][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="4ea00-233">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="4ea00-234">[Simulation d’un appareil avec IoT Edge][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="4ea00-234">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>

[lnk-metrics]: iot-hub-metrics.md
[lnk-monitor]: iot-hub-operations-monitoring.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
