---
title: "aaaGet main du stockage de file d’attente Azure à l’aide de .NET | Documents Microsoft"
description: "Les files d’attente Azure fournissent une messagerie asynchrone fiable entre les composants d’application. Le cloud permet de messagerie votre tooscale de composants d’application indépendamment."
services: storage
documentationcenter: .net
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: c0f82537-a613-4f01-b2ed-fc82e5eea2a7
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 03/27/2017
ms.author: robinsh
ms.openlocfilehash: 36bbb40189a301cddbc2ded92d0623fa5e093eb1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-queue-storage-using-net"></a>Prise en main du stockage de files d’attente Azure à l’aide de .NET
[!INCLUDE [storage-selector-queue-include](../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-check-out-samples-dotnet](../../includes/storage-check-out-samples-dotnet.md)]

## <a name="overview"></a>Vue d'ensemble
Le stockage de files d’attente Azure fournit une messagerie cloud entre les composants d’application. Lors de la conception d'applications pour la mise à l'échelle, des composants d'application sont souvent découplés, de sorte qu'ils peuvent être mis à l'échelle indépendamment. Stockage de file d’attente fournit une messagerie asynchrone pour la communication entre les composants d’application, qu’elles s’exécutent dans le cloud hello, sur le bureau de hello, sur un serveur local ou sur un appareil mobile. Le stockage de files d’attente prend également en charge la gestion des tâches asynchrones et la création des flux de travail de processus.

### <a name="about-this-tutorial"></a>À propos de ce didacticiel
Ce didacticiel montre comment le code toowrite .NET pour les scénarios courants lors de l’utilisation du stockage de file d’attente Azure. Les scénarios traités sont les suivants : création et suppression de files d’attente, et ajout, lecture et suppression des messages de file d’attente.

**Estimation du temps toocomplete :** 45 minutes

**Configuration requise :**

* [Microsoft Visual Studio](https://www.visualstudio.com/downloads/)
* [Bibliothèque cliente Azure Storage pour .NET](https://www.nuget.org/packages/WindowsAzure.Storage/)
* [Gestionnaire de configuration Azure pour .NET](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/)
* Un [compte de stockage Azure](storage-create-storage-account.md#create-a-storage-account)

[!INCLUDE [storage-dotnet-client-library-version-include](../../includes/storage-dotnet-client-library-version-include.md)]

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

[!INCLUDE [storage-development-environment-include](../../includes/storage-development-environment-include.md)]

### <a name="add-using-directives"></a>Ajouter des directives d’utilisation
Ajoutez hello suivant `using` haut toohello de directives de hello `Program.cs` fichier :

```csharp
using Microsoft.Azure; // Namespace for CloudConfigurationManager
using Microsoft.WindowsAzure.Storage; // Namespace for CloudStorageAccount
using Microsoft.WindowsAzure.Storage.Queue; // Namespace for Queue storage types
```

### <a name="parse-hello-connection-string"></a>Analyser la chaîne de connexion hello
[!INCLUDE [storage-cloud-configuration-manager-include](../../includes/storage-cloud-configuration-manager-include.md)]

### <a name="create-hello-queue-service-client"></a>Créer le client du service de file d’attente hello
Hello **CloudQueueClient** classe permet de vous tooretrieve les files d’attente stockés dans le stockage de file d’attente. Voici un moyen toocreate hello service client :

```csharp
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
```
    
Vous êtes maintenant code prêt toowrite qui lit les données à partir d’et écrit le stockage des données tooQueue.

## <a name="create-a-queue"></a>Création d’une file d’attente
Cet exemple montre comment toocreate une file d’attente si elle n’existe pas déjà :

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference tooa container.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Create hello queue if it doesn't already exist
queue.CreateIfNotExists();
```

## <a name="insert-a-message-into-a-queue"></a>Insertion d'un message dans une file d'attente
tooinsert un message dans une file d’attente existante, commencez par créer un **CloudQueueMessage**. Ensuite, appelez hello **AddMessage** (méthode). Un **CloudQueueMessage** peut être créé à partir d’une chaîne (au format UTF-8) ou d’un tableau **d’octets**. Voici le code qui crée une file d’attente (s’il n’existe pas) et le message de type hello insertions « Hello, World » :

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference tooa queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Create hello queue if it doesn't already exist.
queue.CreateIfNotExists();

// Create a message and add it toohello queue.
CloudQueueMessage message = new CloudQueueMessage("Hello, World");
queue.AddMessage(message);
```

## <a name="peek-at-hello-next-message"></a>Lire des message de type hello suivant
Vous pouvez lire de message hello devant hello une file d’attente sans le supprimer de la file d’attente hello en appelant hello **PeekMessage** (méthode).

```csharp
// Retrieve storage account from connection string
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello queue client
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference tooa queue
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Peek at hello next message
CloudQueueMessage peekedMessage = queue.PeekMessage();

// Display message.
Console.WriteLine(peekedMessage.AsString);
```

## <a name="change-hello-contents-of-a-queued-message"></a>Modifier le contenu de hello d’un message en file d’attente
Vous pouvez modifier le contenu de hello d’un message en place dans la file d’attente hello. Si le message représente une tâche de travail, vous pouvez utiliser cette fonctionnalité de tooupdate l’état de tâche hello. Hello suivant code met à jour le message de file d’attente hello avec le nouveau contenu et jeux hello tooextend de délai d’attente de visibilité un autre 60 secondes. Cela enregistre l’état hello du travail associé au message de type hello, ainsi que les clients hello un autre toocontinue minute travaillant sur un message de type hello. Vous pouvez utiliser ce flux de travail à plusieurs étapes de tootrack technique sur les messages de la file d’attente, sans avoir toostart sur du début de hello si une étape de traitement échoue en raison de l’erreur toohardware ou logicielle. En règle générale, vous conservez ainsi un nombre de tentatives, et si hello message est retentée plusieurs  *n*  fois, vous le supprimez. Cela protège du déclenchement d'une erreur d'application par un message chaque fois qu'il est traité.

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference tooa queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Get hello message from hello queue and update hello message contents.
CloudQueueMessage message = queue.GetMessage();
message.SetMessageContent("Updated contents.");
queue.UpdateMessage(message,
    TimeSpan.FromSeconds(60.0),  // Make it invisible for another 60 seconds.
    MessageUpdateFields.Content | MessageUpdateFields.Visibility);
```

## <a name="de-queue-hello-next-message"></a>File d’attente message de type hello suivant
Votre code enlève un message d'une file d'attente en deux étapes. Lorsque vous appelez **GetMessage**, vous obtenez un message de type hello suivante dans une file d’attente. Un message retourné à partir de **GetMessage** devient invisible tooany tout autre code de la lecture de messages à partir de cette file d’attente. Par défaut, ce message reste invisible pendant 30 secondes. toofinish lors de la suppression du message de salutation à partir de la file d’attente hello, vous devez également appeler **DeleteMessage**. Ce processus en deux étapes de la suppression d’un message garantit que si votre code échoue tooprocess qu'un message en raison de la défaillance toohardware ou logiciel, une autre instance de votre code peut obtenir hello même message puis réessayez. Votre code appelle **DeleteMessage** juste après le message de salutation a été traité.

```csharp
// Retrieve storage account from connection string
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello queue client
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference tooa queue
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Get hello next message
CloudQueueMessage retrievedMessage = queue.GetMessage();

//Process hello message in less than 30 seconds, and then delete hello message
queue.DeleteMessage(retrievedMessage);
```

## <a name="use-async-await-pattern-with-common-queue-storage-apis"></a>Utiliser le modèle Async-Await avec les API de stockage de files d’attente communes
Cet exemple montre comment hello toouse Async-Await de modèle avec l’API de stockage de file d’attente commun. exemple Hello appelle la version asynchrone de hello de chacune des hello donné des méthodes, comme indiqué par hello *Async* suffixe de chaque méthode. Lorsqu’une méthode async est utilisée, hello async-await modèle suspend l’exécution locale jusqu'à ce que la fin de l’appel hello. Ce comportement permet à toodo de thread actuel hello autre travail, ce qui permet d’éviter les goulots d’étranglement et améliore la réactivité globale de votre application de hello. Pour plus d’informations sur l’utilisation de hello modèle Async-Await dans .NET consultez [Async et Await (c# et Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx)

```csharp
// Create hello queue if it doesn't already exist
if(await queue.CreateIfNotExistsAsync())
{
    Console.WriteLine("Queue '{0}' Created", queue.Name);
}
else
{
    Console.WriteLine("Queue '{0}' Exists", queue.Name);
}

// Create a message tooput in hello queue
CloudQueueMessage cloudQueueMessage = new CloudQueueMessage("My message");

// Async enqueue hello message
await queue.AddMessageAsync(cloudQueueMessage);
Console.WriteLine("Message added");

// Async dequeue hello message
CloudQueueMessage retrievedMessage = await queue.GetMessageAsync();
Console.WriteLine("Retrieved message with content '{0}'", retrievedMessage.AsString);

// Async delete hello message
await queue.DeleteMessageAsync(retrievedMessage);
Console.WriteLine("Deleted message");
```
    
## <a name="leverage-additional-options-for-de-queuing-messages"></a>Utilisation d’options supplémentaires pour l’enlèvement des messages
Il existe deux façons de personnaliser l'extraction des messages à partir d'une file d'attente.
Tout d’abord, vous pouvez obtenir un lot de messages (haut too32). Ensuite, vous pouvez définir un délai d’attente de l’invisibilité plus ou moins longtemps, ce qui permet de votre code plus ou moins toofully temps traitent chaque message. code Hello suivant utilise le **GetMessages** messages tooget 20 de méthode dans un seul appel. Ensuite, il traite chaque message à l'aide d'une boucle **foreach** . Il définit également hello invisibilité délai d’expiration toofive minutes pour chaque message. Notez que hello 5 minutes démarre pour tous les messages à hello même moment, après que les 5 minutes se sont écoulées depuis l’appel de hello trop**GetMessages**, tous les messages qui n’ont pas été supprimés devient visibles à nouveau.

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference tooa queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

foreach (CloudQueueMessage message in queue.GetMessages(20, TimeSpan.FromMinutes(5)))
{
    // Process all messages in less than 5 minutes, deleting each message after processing.
    queue.DeleteMessage(message);
}
```

## <a name="get-hello-queue-length"></a>Obtenir la longueur de file d’attente hello
Vous pouvez obtenir une estimation du nombre de hello de messages dans une file d’attente. Le **FetchAttributes** méthode vous demande de service de file d’attente hello pour récupérer les attributs de file d’attente hello, y compris le nombre de messages hello. Hello **ApproximateMessageCount** propriété renvoie hello dernière valeur récupérée par le **FetchAttributes** (méthode), sans avoir à contacter le service de file d’attente hello.

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference tooa queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Fetch hello queue attributes.
queue.FetchAttributes();

// Retrieve hello cached approximate message count.
int? cachedMessageCount = queue.ApproximateMessageCount;

// Display number of messages.
Console.WriteLine("Number of messages in queue: " + cachedMessageCount);
```

## <a name="delete-a-queue"></a>Suppression d'une file d'attente
toodelete une file d’attente et tous les messages hello qu’il contient, appelez le **supprimer** méthode sur un objet de file d’attente hello.

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference tooa queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Delete hello queue.
queue.Delete();
```
    

## <a name="next-steps"></a>Étapes suivantes
Maintenant que vous avez appris les notions de base de hello de stockage de la file d’attente, suivez ces toolearn des liens sur les tâches de stockage plus complexes.

* Afficher la documentation de référence de service de file d’attente hello pour plus d’informations sur les API disponibles :
  * [Référence de la bibliothèque cliente de stockage pour .NET](http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409)
  * [Référence d’API REST](http://msdn.microsoft.com/library/azure/dd179355)
* En savoir plus toosimplify hello code que vous écrivez est comment toowork avec le stockage Azure à l’aide de hello [Kit de développement logiciel Azure WebJobs](../app-service-web/websites-dotnet-webjobs-sdk.md).
* Permet d’afficher plusieurs toolearn de repères de fonctionnalité sur les options supplémentaires pour le stockage des données dans Azure.
  * [Prise en main le stockage de Table Azure à l’aide de .NET](storage-dotnet-how-to-use-tables.md) toostore des données structurées.
  * [Prise en main le stockage Blob Azure à l’aide de .NET](storage-dotnet-how-to-use-blobs.md) toostore des données non structurées.
  * [Se connecter tooSQL de base de données à l’aide de .NET (c#)](../sql-database/sql-database-develop-dotnet-simple.md) toostore des données relationnelles.

[Download and install hello Azure SDK for .NET]: /develop/net/
[.NET client library reference]: http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409
[Creating a Azure Project in Visual Studio]: http://msdn.microsoft.com/library/azure/ee405487.aspx
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
[OData]: http://nuget.org/packages/Microsoft.Data.OData/5.0.2
[Edm]: http://nuget.org/packages/Microsoft.Data.Edm/5.0.2
[Spatial]: http://nuget.org/packages/System.Spatial/5.0.2
