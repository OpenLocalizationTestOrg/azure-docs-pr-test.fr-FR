---
title: "Prise en main du stockage de files d’attente Azure à l’aide de .NET | Microsoft Docs"
description: "Les files d’attente Azure fournissent une messagerie asynchrone fiable entre les composants d’application. La messagerie cloud permet de mettre à l’échelle vos composants d’application indépendamment."
services: storage
documentationcenter: .net
author: tamram
manager: timlt
editor: tysonn
ms.assetid: c0f82537-a613-4f01-b2ed-fc82e5eea2a7
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 03/27/2017
ms.author: tamram
ms.openlocfilehash: 00c737205c8970bf3cd3036b8bfa653c962949d0
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/11/2017
---
# <a name="get-started-with-azure-queue-storage-using-net"></a>Prise en main du stockage de files d’attente Azure à l’aide de .NET
[!INCLUDE [storage-selector-queue-include](../../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-check-out-samples-dotnet](../../../includes/storage-check-out-samples-dotnet.md)]

## <a name="overview"></a>Vue d'ensemble
Le stockage de files d’attente Azure fournit une messagerie cloud entre les composants d’application. Lors de la conception d'applications pour la mise à l'échelle, des composants d'application sont souvent découplés, de sorte qu'ils peuvent être mis à l'échelle indépendamment. Le stockage de files d’attente offre une messagerie asynchrone pour la communication entre les composants d’application, qu’ils soient exécutés dans le cloud, sur le bureau, sur un serveur local ou sur un appareil mobile. Le stockage de files d’attente prend également en charge la gestion des tâches asynchrones et la création des flux de travail de processus.

### <a name="about-this-tutorial"></a>À propos de ce didacticiel
Ce didacticiel montre comment écrire du code .NET pour des scénarios courants d’utilisation du stockage de files d’attente Azure. Les scénarios traités sont les suivants : création et suppression de files d’attente, et ajout, lecture et suppression des messages de file d’attente.

**Durée estimée :** 45 minutes

**Configuration requise :**

* [Microsoft Visual Studio](https://www.visualstudio.com/downloads/)
* [Bibliothèque cliente Azure Storage pour .NET](https://www.nuget.org/packages/WindowsAzure.Storage/)
* [Gestionnaire de configuration Azure pour .NET](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/)
* Un [compte de stockage Azure](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json#create-a-storage-account)

[!INCLUDE [storage-dotnet-client-library-version-include](../../../includes/storage-dotnet-client-library-version-include.md)]

[!INCLUDE [storage-queue-concepts-include](../../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

[!INCLUDE [storage-development-environment-include](../../../includes/storage-development-environment-include.md)]

### <a name="add-using-directives"></a>Ajouter des directives d’utilisation
Ajoutez les directives `using` suivantes au fichier `Program.cs` :

```csharp
using Microsoft.Azure; // Namespace for CloudConfigurationManager
using Microsoft.WindowsAzure.Storage; // Namespace for CloudStorageAccount
using Microsoft.WindowsAzure.Storage.Queue; // Namespace for Queue storage types
```

### <a name="parse-the-connection-string"></a>Analyse de la chaîne de connexion
[!INCLUDE [storage-cloud-configuration-manager-include](../../../includes/storage-cloud-configuration-manager-include.md)]

### <a name="create-the-queue-service-client"></a>Création du client du service Queue
La classe **CloudQueueClient** vous permet de récupérer des files d’attente stockées dans Queue Storage. Voici un moyen de créer le client du service :

```csharp
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
```
    
Vous êtes maintenant prêt à écrire du code qui lit et écrit des données dans le Queue Storage.

## <a name="create-a-queue"></a>Création d’une file d’attente
Cet exemple montre comment créer une file d’attente, si elle n’existe pas encore :

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference to a container.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Create the queue if it doesn't already exist
queue.CreateIfNotExists();
```

## <a name="insert-a-message-into-a-queue"></a>Insertion d'un message dans une file d'attente
Pour insérer un message dans une file d'attente existante, commencez par créer un **CloudQueueMessage**. Appelez ensuite la méthode **AddMessage** . Un **CloudQueueMessage** peut être créé à partir d’une chaîne (au format UTF-8) ou d’un tableau **d’octets**. Voici le code qui crée une file d'attente (si elle n'existe pas) et insère le message « Hello, World » :

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference to a queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Create the queue if it doesn't already exist.
queue.CreateIfNotExists();

// Create a message and add it to the queue.
CloudQueueMessage message = new CloudQueueMessage("Hello, World");
queue.AddMessage(message);
```

## <a name="peek-at-the-next-message"></a>Lecture furtive du message suivant
Vous pouvez lire furtivement le message au début de la file d'attente sans l'enlever de la file d'attente en appelant la méthode **PeekMessage** .

```csharp
// Retrieve storage account from connection string
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the queue client
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference to a queue
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Peek at the next message
CloudQueueMessage peekedMessage = queue.PeekMessage();

// Display message.
Console.WriteLine(peekedMessage.AsString);
```

## <a name="change-the-contents-of-a-queued-message"></a>Modification du contenu d'un message en file d'attente
Vous pouvez modifier le contenu d'un message placé dans la file d'attente. Si le message représente une tâche, vous pouvez utiliser cette fonctionnalité pour mettre à jour l'état de la tâche. Le code suivant met à jour le message de la file d'attente avec un nouveau contenu et ajoute 60 secondes au délai d'expiration de la visibilité. Cette opération enregistre l'état de la tâche associée au message et accorde une minute supplémentaire au client pour traiter le message. Vous pouvez utiliser cette technique pour suivre des flux de travail à plusieurs étapes sur les messages de file d'attente, sans devoir reprendre du début si une étape du traitement échoue à cause d'une défaillance matérielle ou logicielle. Normalement, vous conservez aussi un nombre de nouvelles tentatives et si le message est retenté plus de *n* fois, vous le supprimez. Cela protège du déclenchement d'une erreur d'application par un message chaque fois qu'il est traité.

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference to a queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Get the message from the queue and update the message contents.
CloudQueueMessage message = queue.GetMessage();
message.SetMessageContent("Updated contents.");
queue.UpdateMessage(message,
    TimeSpan.FromSeconds(60.0),  // Make it invisible for another 60 seconds.
    MessageUpdateFields.Content | MessageUpdateFields.Visibility);
```

## <a name="de-queue-the-next-message"></a>Enlèvement du message suivant de la file d'attente
Votre code enlève un message d'une file d'attente en deux étapes. Lorsque vous appelez **GetMessage**, vous obtenez le message suivant dans une file d'attente. Un message renvoyé par **GetMessage** devient invisible par les autres codes lisant les messages de cette file d'attente. Par défaut, ce message reste invisible pendant 30 secondes. Pour finaliser la suppression du message de la file d'attente, vous devez aussi appeler **DeleteMessage**. Ce processus de suppression d'un message en deux étapes garantit que, si votre code ne parvient pas à traiter un message à cause d'une défaillance matérielle ou logicielle, une autre instance de votre code peut obtenir le même message et réessayer. Votre code appelle **DeleteMessage** juste après le traitement du message.

```csharp
// Retrieve storage account from connection string
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the queue client
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference to a queue
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Get the next message
CloudQueueMessage retrievedMessage = queue.GetMessage();

//Process the message in less than 30 seconds, and then delete the message
queue.DeleteMessage(retrievedMessage);
```

## <a name="use-async-await-pattern-with-common-queue-storage-apis"></a>Utiliser le modèle Async-Await avec les API de stockage de files d’attente communes
Cet exemple décrit comment utiliser le modèle Async-Await avec les API de stockage de files d’attente communes. L’exemple appelle la version asynchrone de chacune des méthodes spécifiées, comme l’indique le suffixe *Async* de chaque méthode. Quand une méthode asynchrone est utilisée, le modèle Async-Await suspend l’exécution locale jusqu’à la fin de l’appel. Ce comportement permet au thread actuel d’effectuer d’autres tâches afin d’éviter les goulots d’étranglement au niveau des performances et d’améliorer la réactivité globale de votre application. Pour plus d’informations sur l’utilisation du modèle Async-Await dans .NET, consultez l’article [Programmation asynchrone avec Async et Await (C# et Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx)

```csharp
// Create the queue if it doesn't already exist
if(await queue.CreateIfNotExistsAsync())
{
    Console.WriteLine("Queue '{0}' Created", queue.Name);
}
else
{
    Console.WriteLine("Queue '{0}' Exists", queue.Name);
}

// Create a message to put in the queue
CloudQueueMessage cloudQueueMessage = new CloudQueueMessage("My message");

// Async enqueue the message
await queue.AddMessageAsync(cloudQueueMessage);
Console.WriteLine("Message added");

// Async dequeue the message
CloudQueueMessage retrievedMessage = await queue.GetMessageAsync();
Console.WriteLine("Retrieved message with content '{0}'", retrievedMessage.AsString);

// Async delete the message
await queue.DeleteMessageAsync(retrievedMessage);
Console.WriteLine("Deleted message");
```
    
## <a name="leverage-additional-options-for-de-queuing-messages"></a>Utilisation d’options supplémentaires pour l’enlèvement des messages
Il existe deux façons de personnaliser l'extraction des messages à partir d'une file d'attente.
Premièrement, vous pouvez obtenir un lot de messages (jusqu'à 32). Deuxièmement, vous pouvez définir un délai d'expiration de l'invisibilité plus long ou plus court afin d'accorder à votre code plus ou moins de temps pour traiter complètement chaque message. L'exemple de code suivant utilise la méthode **GetMessages** pour obtenir 20 messages en un appel. Ensuite, il traite chaque message à l'aide d'une boucle **foreach** . Il définit également le délai d'expiration de l'invisibilité sur cinq minutes pour chaque message. Notez que le délai de 5 minutes démarre en même temps pour tous les messages, donc une fois les 5 minutes écoulées après l'appel de **GetMessages**, tous les messages n'ayant pas été supprimés redeviennent visibles.

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference to a queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

foreach (CloudQueueMessage message in queue.GetMessages(20, TimeSpan.FromMinutes(5)))
{
    // Process all messages in less than 5 minutes, deleting each message after processing.
    queue.DeleteMessage(message);
}
```

## <a name="get-the-queue-length"></a>Obtention de la longueur de la file d'attente
Vous pouvez obtenir une estimation du nombre de messages dans une file d'attente. La méthode **FetchAttributes** demande au service de files d'attente d'extraire les attributs de la file d'attente, y compris le nombre de messages. La propriété **ApproximateMessageCount** renvoie la dernière valeur extraite par la méthode **FetchAttributes**, sans appeler le service de files d’attente.

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference to a queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Fetch the queue attributes.
queue.FetchAttributes();

// Retrieve the cached approximate message count.
int? cachedMessageCount = queue.ApproximateMessageCount;

// Display number of messages.
Console.WriteLine("Number of messages in queue: " + cachedMessageCount);
```

## <a name="delete-a-queue"></a>Suppression d'une file d'attente
Pour supprimer une file d'attente et tous les messages qu'elle contient, appelez la méthode **Delete** sur l'objet file d'attente.

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference to a queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Delete the queue.
queue.Delete();
```
    

## <a name="next-steps"></a>Étapes suivantes
Maintenant que vous connaissez les bases du stockage des files d'attente, consultez les liens suivants pour apprendre à exécuter les tâches de stockage plus complexes.

* Pour plus d'informations sur les API disponibles, consultez la documentation de référence des services de files d'attente :
  * [Référence de la bibliothèque cliente de stockage pour .NET](http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409)
  * [Référence d’API REST](http://msdn.microsoft.com/library/azure/dd179355)
* Découvrez comment simplifier le code que vous écrivez avec Azure Storage, à l’aide du [Kit de développement logiciel (SDK) Azure WebJobs](https://github.com/Azure/azure-webjobs-sdk/wiki).
* Pour plus d’informations sur les autres options de stockage de données dans Azure, consultez d’autres guides de fonctionnalités.
  * [Prise en main du stockage de tables Azure à l’aide de .NET](../../cosmos-db/table-storage-how-to-use-dotnet.md) pour le stockage de données structurées.
  * [Prise en main d’Azure Blob Storage à l’aide de .NET](../blobs/storage-dotnet-how-to-use-blobs.md) pour le stockage de données non structurées.
  * [Connexion à SQL Database à l’aide de .NET (C#)](../../sql-database/sql-database-connect-query-dotnet-core.md) pour stocker des données relationnelles.

[Download and install the Azure SDK for .NET]: /develop/net/
[.NET client library reference]: http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409
[Creating a Azure Project in Visual Studio]: http://msdn.microsoft.com/library/azure/ee405487.aspx
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
[OData]: http://nuget.org/packages/Microsoft.Data.OData/5.0.2
[Edm]: http://nuget.org/packages/Microsoft.Data.Edm/5.0.2
[Spatial]: http://nuget.org/packages/System.Spatial/5.0.2
