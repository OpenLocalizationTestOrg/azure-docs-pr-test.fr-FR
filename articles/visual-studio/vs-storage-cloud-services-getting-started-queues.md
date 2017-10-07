---
title: "aaaGet démarré avec Visual Studio et le stockage de file d’attente des services connectés (services de cloud computing) | Documents Microsoft"
description: "Comment tooget démarrer l’utilisation du stockage de file d’attente Azure dans un projet de service cloud dans Visual Studio une fois la connexion de compte de stockage tooa à l’aide de Visual Studio services connectés"
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: da587aac-5e64-4e9a-8405-44cc1924881d
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: kraigb
ms.openlocfilehash: 1e90eeb826131cadca90dcb720c931fff5fedcb7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-queue-storage-and-visual-studio-connected-services-cloud-services-projects"></a>Prise en main du stockage de files d'attente Azure et des services connectés Visual Studio (projets services cloud)
[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a>Vue d'ensemble
Cet article décrit comment tooget démarrer l’utilisation du stockage de file d’attente Azure dans Visual Studio après avoir créé ou référencé un compte de stockage Azure dans un projet de services cloud à l’aide de Visual Studio de hello **ajouter des Services connectés** boîte de dialogue .

Nous allons vous montrer comment toocreate une file d’attente dans le code. Nous allons également vous montrer comment tooperform basic file d’attente des opérations, telles que l’ajout, modification, lecture et suppression des messages de file d’attente. les exemples de Hello sont écrits en code c# et utilisez hello [bibliothèque cliente Microsoft Azure Storage pour .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).

Hello **ajouter des Services connectés** opération installe hello approprié NuGet packages tooaccess stockage Azure dans votre projet et ajoute la chaîne de connexion hello pour hello du compte de stockage tooyour les fichiers de configuration de projet.

* Pour plus d’informations sur l’utilisation de files d’attente dans le code, consultez [Prise en main du stockage de files d’attente Azure à l’aide de .NET](../storage/queues/storage-dotnet-how-to-use-queues.md) .
* Pour des informations générales sur Azure Storage, consultez la [documentation relative au stockage](https://azure.microsoft.com/documentation/services/storage/) .
* Pour des informations générales sur les services cloud Azure, consultez la [documentation des services cloud](https://azure.microsoft.com/documentation/services/cloud-services/) .
* Pour plus d’informations sur la programmation des applications ASP.NET, consultez la page [ASP.NET](http://www.asp.net) .

Stockage de file d’attente Azure est un service pour stocker un grand nombre de messages qui sont accessibles à partir de n’importe où dans le monde hello via des appels authentifiés à l’aide de HTTP ou HTTPS. Un message de la file d’attente unique peut être de taille too64 Ko, et une file d’attente peut contenir des millions de messages, des limites de capacité totale de toohello d’un compte de stockage.

## <a name="access-queues-in-code"></a>Accéder à des files d’attente dans le code
tooaccess files d’attente dans les projets Visual Studio Cloud Services, vous devez suivant de hello tooinclude fichier source tooany c# éléments accéder au stockage de file d’attente Azure.

1. Assurez-vous que les déclarations d’espace de noms hello haut hello du fichier de hello c# incluent ces **à l’aide de** instructions.
   
        using Microsoft.Framework.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Queue;
2. Obtenez un objet **CloudStorageAccount** qui représente les informations de votre compte de stockage. Hello utilisation suivant tooget de code hello votre chaîne de connexion de stockage et les informations de compte de stockage à partir de la configuration du service Azure hello.
   
         CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
           CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
3. Obtenir un **CloudQueueClient** tooreference objets de file d’attente hello dans votre compte de stockage de l’objet.  
   
        // Create hello queue client.
        CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
4. Obtenir un **CloudQueue** tooreference une file d’attente spécifique de l’objet.
   
        // Get a reference tooa queue named "messageQueue"
        CloudQueue messageQueue = queueClient.GetQueueReference("messageQueue");

**Remarque :** utilisent les hello ci-dessus code devant les code hello dans hello suivant des exemples.

## <a name="create-a-queue-in-code"></a>Créer une file d’attente dans le code
file d’attente de hello toocreate dans le code, ajoutez simplement un appel trop**CreateIfNotExists**.

    // Create hello CloudQueue if it does not exist
    messageQueue.CreateIfNotExists();

## <a name="add-a-message-tooa-queue"></a>Ajouter une file d’attente de messages tooa
tooinsert un message dans une file d’attente existante, créer un nouveau **CloudQueueMessage** objet, puis appel hello **AddMessage** (méthode).

Un objet **CloudQueueMessage** peut être créé à partir d'une chaîne (au format UTF-8) ou d'un tableau d'octets.

Voici un exemple qui insère des message de type hello « Hello, World ».

    // Create a message and add it toohello queue.
    CloudQueueMessage message = new CloudQueueMessage("Hello, World");
    messageQueue.AddMessage(message);

## <a name="read-a-message-in-a-queue"></a>Lire un message dans une file d’attente
Vous pouvez lire de message hello devant hello une file d’attente sans le supprimer de la file d’attente hello en appelant hello **PeekMessage** (méthode).

    // Peek at hello next message
    CloudQueueMessage peekedMessage = messageQueue.PeekMessage();

## <a name="read-and-remove-a-message-in-a-queue"></a>Lire et supprimer un message dans une file d’attente
Votre code permet de supprimer (retirer) un message d'une file d'attente en deux étapes.

1. Appelez **GetMessage** tooget message suivant dans une file d’attente de type hello. Un message retourné à partir de **GetMessage** devient invisible tooany tout autre code de la lecture de messages à partir de cette file d’attente. Par défaut, ce message reste invisible pendant 30 secondes.
2. toofinish suppression de message de type hello à partir de la file d’attente hello, appelez **DeleteMessage**.

Ce processus en deux étapes de la suppression d’un message garantit que si votre code échoue tooprocess qu'un message en raison de la défaillance toohardware ou logiciel, une autre instance de votre code peut obtenir hello même message puis réessayez. code Hello suivant appelle **DeleteMessage** juste après le message de salutation a été traité.

    // Get hello next message in hello queue.
    CloudQueueMessage retrievedMessage = messageQueue.GetMessage();

    // Process hello message in less than 30 seconds

    // Then delete hello message.
    await messageQueue.DeleteMessage(retrievedMessage);


## <a name="use-additional-options-tooprocess-and-remove-queue-messages"></a>Utilisez les options supplémentaires tooprocess et supprimer les messages de la file d’attente
Il existe deux façons de personnaliser l'extraction des messages à partir d'une file d'attente.

* Vous pouvez obtenir un lot de messages (haut too32).
* Vous pouvez définir un délai d’attente de l’invisibilité plus ou moins longtemps, ce qui permet de votre code plus ou moins toofully temps traitent chaque message. code Hello suivant utilise le **GetMessages** messages tooget 20 de méthode dans un seul appel. Ensuite, il traite chaque message à l'aide d'une boucle **foreach** . Il définit également hello invisibilité délai d’expiration toofive minutes pour chaque message. Notez que hello 5 minutes démarre pour tous les messages à hello même moment, après que les 5 minutes se sont écoulées depuis l’appel de hello trop**GetMessages**, tous les messages qui n’ont pas été supprimés devient visibles à nouveau.

Voici un exemple :

    foreach (CloudQueueMessage message in messageQueue.GetMessages(20, TimeSpan.FromMinutes(5)))
    {
        // Process all messages in less than 5 minutes, deleting each message after processing.

        // Then delete hello message after processing
        messageQueue.DeleteMessage(message);

    }

## <a name="get-hello-queue-length"></a>Obtenir la longueur de file d’attente hello
Vous pouvez obtenir une estimation du nombre de hello de messages dans une file d’attente. Le **FetchAttributes** méthode vous demande de service de file d’attente hello pour récupérer les attributs de file d’attente hello, y compris le nombre de messages hello. Hello **ApproximateMethodCount** propriété renvoie hello dernière valeur récupérée par le **FetchAttributes** (méthode), sans avoir à contacter le service de file d’attente hello.

    // Fetch hello queue attributes.
    messageQueue.FetchAttributes();

    // Retrieve hello cached approximate message count.
    int? cachedMessageCount = messageQueue.ApproximateMessageCount;

    // Display number of messages.
    Console.WriteLine("Number of messages in queue: " + cachedMessageCount);

## <a name="use-hello-async-await-pattern-with-common-azure-queue-apis"></a>Utilisez hello Async-Await un modèle avec l’API de file d’attente Azure courantes
Cet exemple montre comment hello toouse Async-Await de modèle avec l’API de file d’attente Azure courantes. exemple Hello appelle la version asynchrone de hello de chacune des hello donné des méthodes, ceci peut être observé par hello **Async** après correction de chaque méthode. Quand une méthode async est utilisé hello async-await modèle suspend l’exécution locale jusqu'à ce que la fin de l’appel hello. Ce comportement permet à toodo de thread actuel hello autre travail qui permet d’éviter les goulots d’étranglement et améliore la réactivité globale de votre application de hello. Pour plus d’informations sur l’utilisation de hello modèle Async-Await dans .NET consultez [Async et Await (c# et Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx)

    // Create a message tooput in hello queue
    CloudQueueMessage cloudQueueMessage = new CloudQueueMessage("My message");

    // Add hello message asynchronously
    await messageQueue.AddMessageAsync(cloudQueueMessage);
    Console.WriteLine("Message added");

    // Async dequeue hello message
    CloudQueueMessage retrievedMessage = await messageQueue.GetMessageAsync();
    Console.WriteLine("Retrieved message with content '{0}'", retrievedMessage.AsString);

    // Delete hello message asynchronously
    await messageQueue.DeleteMessageAsync(retrievedMessage);
    Console.WriteLine("Deleted message");

## <a name="delete-a-queue"></a>Suppression d'une file d'attente
toodelete une file d’attente et tous les messages hello qu’il contient, appel hello **supprimer** méthode sur un objet de file d’attente hello.

    // Delete hello queue.
    messageQueue.Delete();

## <a name="next-steps"></a>Étapes suivantes
[!INCLUDE [vs-storage-dotnet-queues-next-steps](../../includes/vs-storage-dotnet-queues-next-steps.md)]

