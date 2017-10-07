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
# <a name="manage-your-iot-hub-device-identities-in-bulk"></a>Gestion de vos identités d’appareil IoT Hub en bloc

Chaque hub IoT a un registre d’identité que vous pouvez utiliser les ressources de chaque appareil toocreate dans le service hello. Registre des identités Hello vous permet également de points de terminaison toocontrol accès toohello périphérique. Cet article décrit comment les identités d’appareil tooimport et d’exportation dans en bloc tooand à partir d’un registre d’identité.

Opérations d’importation et d’exportation ont lieu dans le contexte de hello de *travaux* qui vous permettent des opérations de service tooexecute en bloc par rapport à un hub IoT.

Hello **RegistryManager** classe inclut hello **ExportDevicesAsync** et **ImportDevicesAsync** les méthodes qui utilisent hello **travail** Framework. Ces méthodes permettent de tooexport, importation et synchroniser l’intégralité de hello de Registre des identités un hub IoT.

## <a name="what-are-jobs"></a>Que sont les tâches ?

Les opérations de Registre identité utilisent hello **travail** système lorsque hello opération :

* A une durée d’exécution peut être longue comparée toostandard opérations d’exécution.
* Retourne une grande quantité d’utilisateur toohello de données.

Au lieu d’un seul appel d’API en attente ou de blocage sur le résultat de hello d’opération de hello, opération de hello crée de façon asynchrone un **travail** pour ce hub IoT. opération de Hello, puis retourne immédiatement un **JobProperties** objet.

Hello suivant c# de code extrait de code montre comment toocreate un travail d’exportation :

```csharp
// Call an export job on hello IoT Hub tooretrieve all devices
JobProperties exportJob = await registryManager.ExportDevicesAsync(containerSasUri, false);
```

> [!NOTE]
> toouse hello **RegistryManager** de classe dans votre code c#, ajoutez hello **Microsoft.Azure.Devices** projet tooyour de package NuGet. Hello **RegistryManager** classe se trouve dans hello **Microsoft.Azure.Devices** espace de noms.

Vous pouvez utiliser hello **RegistryManager** classe état de hello tooquery Hello **travail** à l’aide de hello retourné **JobProperties** métadonnées.

Hello extrait de code c# suivant montre comment toopoll toosee de toutes les cinq secondes si hello la tâche est terminée :

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

## <a name="export-devices"></a>Exporter des appareils

Hello d’utilisation **ExportDevicesAsync** intégralité de hello méthode tooexport d’un tooan de Registre IoT hub identité [Azure Storage](../storage/index.md) conteneur d’objets blob à l’aide un [Signature d’accès partagé](../storage/common/storage-security-guide.md#data-plane-security).

Cette méthode vous permet de toocreate les sauvegardes fiable de vos informations de périphérique dans un conteneur d’objets blob que vous contrôlez.

Hello **ExportDevicesAsync** méthode requiert deux paramètres :

* Une *chaîne* qui contient l’URI d’un conteneur d’objets blob. Cet URI doit contenir un jeton SAS qui accorde un accès en écriture toohello conteneur. Hello crée un objet blob de blocs dans ces conteneur toostore hello sérialisé exporter périphérique des données. un jeton SAS Hello doit inclure ces autorisations :

   ```csharp
   SharedAccessBlobPermissions.Write | SharedAccessBlobPermissions.Read | SharedAccessBlobPermissions.Delete
   ```

* A *booléenne* qui indique si vous souhaitez tooexclude clés d’authentification à partir de vos données d’exportation. Si la valeur est **false**, des clés d’authentification sont incluses dans la sortie d’exportation. Dans le cas contraire, les clés sont exportées sous forme de valeur **null**.

Hello extrait de code c# suivant montre comment tooinitiate un travail d’exportation qui inclut des clés de l’authentification d’appareil Bonjour exporter des données et puis interroger fin :

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

Hello travail stocke sa sortie dans un conteneur d’objets blob hello fourni en tant qu’objet blob de blocs avec le nom de hello **devices.txt**. les données de sortie Hello se comprennent de données de l’appareil sérialisé au format JSON, avec un périphérique par ligne.

Hello suivant montre les données de sortie hello :

```json
{"id":"Device1","eTag":"MA==","status":"enabled","authentication":{"symmetricKey":{"primaryKey":"abc=","secondaryKey":"def="}}}
{"id":"Device2","eTag":"MA==","status":"enabled","authentication":{"symmetricKey":{"primaryKey":"abc=","secondaryKey":"def="}}}
{"id":"Device3","eTag":"MA==","status":"disabled","authentication":{"symmetricKey":{"primaryKey":"abc=","secondaryKey":"def="}}}
{"id":"Device4","eTag":"MA==","status":"disabled","authentication":{"symmetricKey":{"primaryKey":"abc=","secondaryKey":"def="}}}
{"id":"Device5","eTag":"MA==","status":"enabled","authentication":{"symmetricKey":{"primaryKey":"abc=","secondaryKey":"def="}}}
```

Si un périphérique comporte des données de double, données de double hello sont également exportées avec les données de l’appareil hello. Hello suivant montre ce format. Toutes les données de ligne de « twinETag » hello jusqu'à la fin de hello sont les données double.

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

Si vous devez accéder aux données toothis dans du code, vous pouvez facilement désérialiser ces données à l’aide de hello **ExportImportDevice** classe. Hello extrait de code c# suivant montre comment les informations de périphérique tooread qui a été précédemment exportées tooa objet blob de blocs :

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
> Vous pouvez également utiliser hello **GetDevicesAsync** méthode Hello **RegistryManager** classe toofetch une liste de vos appareils. Toutefois, cette approche a une valeur maximale de 1000 nombre hello d’objets de périphérique qui sont retournées. Hello attendu de cas d’utilisation de hello **GetDevicesAsync** méthode est pour le débogage de tooaid de scénarios de développement et n’est pas recommandée pour les charges de production.

## <a name="import-devices"></a>Importer des appareils

Hello **ImportDevicesAsync** méthode Bonjour **RegistryManager** classe vous permet d’opérations d’importation et synchronisation d’en bloc dans un registre des identités IoT hub tooperform. Comme hello **ExportDevicesAsync** (méthode), hello **ImportDevicesAsync** méthode utilise hello **travail** framework.

Prendre en charge à l’aide de hello **ImportDevicesAsync** (méthode), car dans Ajout tooprovisioning nouveaux appareils dans votre Registre des identités, il peut également mettre à jour et supprimer des périphériques existants.

> [!WARNING]
> Il est impossible d’annuler une opération d’importation. Toujours sauvegarder vos données existantes à l’aide de hello **ExportDevicesAsync** conteneur d’objets blob méthode tooanother avant d’apporter en bloc modifie le Registre des identités tooyour.

Hello **ImportDevicesAsync** méthode accepte deux paramètres :

* A *chaîne* qui contient l’URI d’un [Azure Storage](../storage/index.md) toouse conteneur comme des objets blob *d’entrée* toohello travail. Cet URI doit contenir un jeton SAS qui accorde l’accès en lecture toohello conteneur. Ce conteneur doit contenir un objet blob avec le nom de hello **devices.txt** qui contient tooimport de données de périphérique hello sérialisé dans le Registre de votre identité. Hello importer des données doivent contenir des informations de périphérique Bonjour même format JSON que hello **ExportImportDevice** travail utilise lorsqu’il crée un **devices.txt** blob. un jeton SAS Hello doit inclure ces autorisations :

   ```csharp
   SharedAccessBlobPermissions.Read
   ```
* A *chaîne* qui contient l’URI d’un [Azure Storage](https://azure.microsoft.com/documentation/services/storage/) toouse conteneur comme des objets blob *sortie* à partir de la tâche de hello. Hello travail crée un objet blob de blocs dans ce conteneur toostore aucune information d’erreur de l’importation de hello terminée **travail**. un jeton SAS Hello doit inclure ces autorisations :

   ```csharp
   SharedAccessBlobPermissions.Write | SharedAccessBlobPermissions.Read | SharedAccessBlobPermissions.Delete
   ```

> [!NOTE]
> paramètres de Hello deux peuvent pointer toohello même conteneur d’objets blob. les paramètres distincts Hello activent simplement plus de contrôle sur vos données en tant que conteneur de sortie hello nécessite des autorisations supplémentaires.

Hello suivant c# de code extrait de code montre comment tooinitiate un travail d’importation :

```csharp
JobProperties importJob = await registryManager.ImportDevicesAsync(containerSasUri, containerSasUri);
```

Cette méthode peut également être données hello tooimport utilisé double du périphérique hello. format Hello hello d’entrée de données est hello même en tant que format hello illustré hello **ExportDevicesAsync** section. De cette façon, vous pouvez réimporter les données de hello exportée. Hello **$metadata** est facultatif.

## <a name="import-behavior"></a>Comportement d’importation

Vous pouvez utiliser hello **ImportDevicesAsync** suivant de méthode tooperform hello en bloc des opérations dans le Registre de votre identité :

* Inscription en bloc de nouveaux appareils
* Suppression en bloc d’appareils existants
* Modifications d’état en bloc (activer ou désactiver des appareils)
* Attribution en bloc de nouvelles clés d’authentification d’appareils
* Auto-régénération en bloc des clés d’authentification d’appareils
* Mise à jour en bloc de données de représentation

Vous pouvez effectuer n’importe quelle combinaison de hello précédant les opérations dans un seul **ImportDevicesAsync** appeler. Par exemple, vous pouvez inscrire de nouveaux périphériques et supprimer ou mettre à jour des périphériques existants à hello même temps. Lorsqu’il est utilisé avec hello **ExportDevicesAsync** (méthode), vous pouvez entièrement migrer tous vos appareils à partir d’un tooanother de hub IoT.

Si le fichier d’importation hello inclut les métadonnées de double, ces métadonnées remplacent les métadonnées existantes du double hello. Si le fichier d’importation hello n’inclut pas de métadonnées de double, puis uniquement hello `lastUpdateTime` métadonnées sont mis à jour à l’aide de hello heure actuelle.

Hello utilisation facultative **importMode** propriété dans les données de sérialisation hello pour chaque périphérique toocontrol hello importation processus par périphérique. Hello **importMode** propriété a hello options suivantes :

| importMode | Description |
| --- | --- |
| **createOrUpdate** |Si un appareil avec hello spécifié n’existe pas **id**, il est nouvellement inscrit. <br/>Si l’appareil de hello existe déjà, informations existantes sont remplacées par hello a fourni des données d’entrée sans se soucier des toohello **ETag** valeur. <br> utilisateur de Hello peut éventuellement spécifier des données de double en même temps que les données de l’appareil hello. etag du double Hello si spécifié, est traitée indépendamment de l’etag de l’appareil hello. S’il existe une incompatibilité avec les etag du double hello existant, une erreur est consignée toohello du journal. |
| **create** |Si un appareil avec hello spécifié n’existe pas **id**, il est nouvellement inscrit. <br/>Si l’appareil de hello existe déjà, une erreur est consignée toohello du journal. <br> utilisateur de Hello peut éventuellement spécifier des données de double en même temps que les données de l’appareil hello. etag du double Hello si spécifié, est traitée indépendamment de l’etag de l’appareil hello. S’il existe une incompatibilité avec les etag du double hello existant, une erreur est consignée toohello du journal. |
| **update** |Si un appareil existe déjà avec hello spécifié **id**, les informations existantes sont remplacées par hello a fourni des données d’entrée sans se soucier des toohello **ETag** valeur. <br/>Si l’appareil de hello n’existe pas, une erreur est consignée toohello du journal. |
| **updateIfMatchETag** |Si un appareil existe déjà avec hello spécifié **id**, les informations existantes sont remplacées par hello a fourni des données d’entrée uniquement s’il existe un **ETag** correspondent. <br/>Si l’appareil de hello n’existe pas, une erreur est consignée toohello du journal. <br/>S’il existe un **ETag** incompatibilité, une erreur est consignée toohello du journal. |
| **createOrUpdateIfMatchETag** |Si un appareil avec hello spécifié n’existe pas **id**, il est nouvellement inscrit. <br/>Si l’appareil de hello existe déjà, informations existantes sont remplacées par hello a fourni des données d’entrée uniquement s’il existe un **ETag** correspondent. <br/>S’il existe un **ETag** incompatibilité, une erreur est consignée toohello du journal. <br> utilisateur de Hello peut éventuellement spécifier des données de double en même temps que les données de l’appareil hello. etag du double Hello si spécifié, est traitée indépendamment de l’etag de l’appareil hello. S’il existe une incompatibilité avec les etag du double hello existant, une erreur est consignée toohello du journal. |
| **delete** |Si un appareil existe déjà avec hello spécifié **id**, il est supprimé sans se soucier des toohello **ETag** valeur. <br/>Si l’appareil de hello n’existe pas, une erreur est consignée toohello du journal. |
| **deleteIfMatchETag** |Si un appareil existe déjà avec hello spécifié **id**, il est supprimé uniquement s’il existe un **ETag** correspondent. Si l’appareil de hello n’existe pas, une erreur est consignée toohello du journal. <br/>S’il existe une non-correspondance d’ETag, une erreur est consignée toohello du journal. |

> [!NOTE]
> Si les données de sérialisation hello ne définissent pas explicitement un **importMode** indicateur pour un périphérique, la valeur par défaut trop**createOrUpdate** hello lors de l’opération d’importation.

## <a name="import-devices-example--bulk-device-provisioning"></a>Exemple d’importation d’appareils : approvisionnement d’appareils en bloc

Hello exemple de code c# suivant illustre comment toogenerate plusieurs identités d’appareil qui :

* Comprennent des clés d’authentification.
* Cet objet blob de blocs appareil informations tooa d’écriture.
* Importer des appareils hello dans le Registre des identités hello.

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

## <a name="import-devices-example--bulk-deletion"></a>Exemple d’importation d’appareils : suppression en bloc

Hello exemple de code suivant montre comment les appareils hello toodelete de que vous avez ajouté à l’aide hello exemple de code précédent :

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

## <a name="get-hello-container-sas-uri"></a>Obtenir le conteneur de hello URI SAS

Hello exemple de code suivant vous montre comment toogenerate un [URI SAS](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md) en lecture, écriture et suppression des autorisations pour un conteneur d’objets blob :

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

## <a name="next-steps"></a>Étapes suivantes

Dans cet article, vous avez appris comment tooperform en bloc des opérations sur le Registre des identités hello dans un hub IoT. Suivez ces liens de toolearn plus d’informations sur la gestion de Azure IoT Hub :

* [Métriques d’IoT Hub][lnk-metrics]
* [Surveillance des opérations][lnk-monitor]

toofurther Explorez les fonctionnalités de hello d’IoT Hub, consultez :

* [Guide du développeur IoT Hub][lnk-devguide]
* [Simulation d’un appareil avec IoT Edge][lnk-iotedge]

[lnk-metrics]: iot-hub-metrics.md
[lnk-monitor]: iot-hub-operations-monitoring.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
