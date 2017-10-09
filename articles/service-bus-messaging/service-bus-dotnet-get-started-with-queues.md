---
title: "aaaGet démarré avec les files d’attente Azure Service Bus | Documents Microsoft"
description: "Écrire une application console C# qui utilise les files d’attente de messagerie Service Bus."
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 68a34c00-5600-43f6-bbcc-fea599d500da
ms.service: service-bus-messaging
ms.devlang: tbd
ms.topic: hero-article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 06/26/2017
ms.author: sethm
ms.openlocfilehash: eaa362ab0eabd2427977398c1deab5dc00105ae9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-service-bus-queues"></a>Prise en main des files d’attente Service Bus
[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

## <a name="what-will-be-accomplished"></a>Les opérations que nous allons effectuer
Ce didacticiel couvre hello comme suit :

1. Créer un espace de noms Service Bus, à l’aide de hello portail Azure.
2. Créer une file d’attente Service Bus, à l’aide de hello portail Azure.
3. Écrire un toosend d’application console à un message.
4. Écrire des messages envoyés à l’étape précédente de hello un Bonjour de tooreceive d’application console.

## <a name="prerequisites"></a>Composants requis
1. [Visual Studio 2015 ou une version ultérieure](http://www.visualstudio.com). exemples de Hello dans ce didacticiel utilisent Visual Studio 2017.
2. Un abonnement Azure.

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="1-create-a-namespace-using-hello-azure-portal"></a>1. Créer un espace de noms à l’aide de hello portail Azure
Si vous avez déjà créé un espace de noms de messagerie Service Bus, raccourcis toohello [créer une file d’attente à l’aide de hello portail Azure](#2-create-a-queue-using-the-azure-portal) section.

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="2-create-a-queue-using-hello-azure-portal"></a>2. Créer une file d’attente à l’aide de hello portail Azure
Si vous avez déjà créé une file d’attente Service Bus, raccourcis toohello [file d’attente de toohello de messages envoi](#3-send-messages-to-the-queue) section.

[!INCLUDE [service-bus-create-queue-portal](../../includes/service-bus-create-queue-portal.md)]

## <a name="3-send-messages-toohello-queue"></a>3. Envoyer la file d’attente de messages toohello
file d’attente toosend messages toohello, nous écrire une application console c# à l’aide de Visual Studio.

### <a name="create-a-console-application"></a>Création d’une application console

Ouvrez Visual Studio et créez un projet **Application de console (.NET Framework)**.

### <a name="add-hello-service-bus-nuget-package"></a>Ajoutez le package NuGet Service Bus de hello
1. Avec le bouton droit de projet de hello nouvellement créé et sélectionnez **gérer les Packages NuGet**.
2. Cliquez sur hello **Parcourir** onglet, recherchez **Microsoft Azure Service Bus**, puis sélectionnez hello **WindowsAzure.ServiceBus** élément. Cliquez sur **installer** toocomplete hello installation, puis fermez cette boîte de dialogue.
   
    ![Sélectionner un package NuGet][nuget-pkg]

### <a name="write-some-code-toosend-a-message-toohello-queue"></a>Écrire certaines toosend code une file d’attente de messages toohello
1. Ajoutez hello suit `using` haut de toohello instruction du fichier Program.cs de hello.
   
    ```csharp
    using Microsoft.ServiceBus.Messaging;
    ```
2. Ajouter hello suivant code toohello `Main` (méthode). Ensemble hello `connectionString` que vous avez obtenu lors de la création d’espace de noms hello et définir de chaîne de connexion de la variable toohello `queueName` nom de file d’attente toohello que vous avez utilisé lors de la création de file d’attente hello.
   
    ```csharp
    var connectionString = "<your connection string>";
    var queueName = "<your queue name>";
   
    var client = QueueClient.CreateFromConnectionString(connectionString, queueName);
    var message = new BrokeredMessage("This is a test message!");

    Console.WriteLine(String.Format("Message id: {0}", message.MessageId));

    client.Send(message);

    Console.WriteLine("Message successfully sent! Press ENTER tooexit program");
    Console.ReadLine();
    ```
   
    Voici à quoi doit ressembler votre fichier Program.cs.
   
    ```csharp
    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Text;
    using System.Threading.Tasks;
    using Microsoft.ServiceBus.Messaging;

    namespace qsend
    {
        class Program
        {
            static void Main(string[] args)
            {
                var connectionString = "Endpoint=sb://<your namespace>.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=<your key>";
                var queueName = "<your queue name>";

                var client = QueueClient.CreateFromConnectionString(connectionString, queueName);
                var message = new BrokeredMessage("This is a test message!");

                Console.WriteLine(String.Format("Message id: {0}", message.MessageId));

                client.Send(message);

                Console.WriteLine("Message successfully sent! Press ENTER tooexit program");
                Console.ReadLine();
            }
        }
    }
    ```
3. Exécuter le programme de hello et vérifier hello portail Azure : cliquez sur nom hello de votre file d’attente dans l’espace de noms hello **vue d’ensemble** panneau. file d’attente Hello **Essentials** panneau s’affiche. Notez que hello **nombre de messages actifs** valeur doit maintenant être 1. Chaque fois que vous exécutez l’application d’expédition hello sans récupérer les messages de type hello, cette valeur augmente de 1. Notez que taille actuelle de hello de file d’attente hello incrémente chaque application hello de temps ajoute également une file d’attente de message toohello.
   
      ![Taille des messages][queue-message]

## <a name="4-receive-messages-from-hello-queue"></a>4. Recevoir des messages à partir de la file d’attente hello

1. messages de type hello tooreceive vous venez d’envoyer, créer une nouvelle application console et ajouter un package NuGet Service Bus toohello référence, l’application expéditeur précédente toohello similaire.
2. Ajoutez hello suit `using` haut de toohello instruction du fichier Program.cs de hello.
   
    ```csharp
    using Microsoft.ServiceBus.Messaging;
    ```
3. Ajouter hello suivant code toohello `Main` (méthode). Ensemble hello `connectionString` chaîne de connexion toohello variable qui a été obtenu lors de la création d’espace de noms hello et définir `queueName` nom de file d’attente toohello que vous avez utilisé lors de la création de file d’attente hello.
   
    ```csharp
    var connectionString = "<your connection string>";
    var queueName = "<your queue name>";
   
    var client = QueueClient.CreateFromConnectionString(connectionString, queueName);
   
    client.OnMessage(message =>
    {
      Console.WriteLine(String.Format("Message body: {0}", message.GetBody<String>()));
      Console.WriteLine(String.Format("Message id: {0}", message.MessageId));
    });
   
    Console.WriteLine("Press ENTER tooexit program");
    Console.ReadLine();
    ```
   
    Voici à quoi doit ressembler votre fichier Program.cs :
   
    ```csharp
    using System;
    using Microsoft.ServiceBus.Messaging;
   
    namespace GettingStartedWithQueues
    {
      class Program
      {
        static void Main(string[] args)
        {
          var connectionString = "Endpoint=sb://<your namespace>.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=<your key>";;
          var queueName = "<your queue name>";
   
          var client = QueueClient.CreateFromConnectionString(connectionString, queueName);
   
          client.OnMessage(message =>
          {
            Console.WriteLine(String.Format("Message body: {0}", message.GetBody<String>()));
            Console.WriteLine(String.Format("Message id: {0}", message.MessageId));
          });

          Console.WriteLine("Press ENTER tooexit program");   
          Console.ReadLine();
        }
      }
    }
    ```
4. Exécuter le programme de hello et vérifiez de nouveau portail de hello. Notez que hello **nombre de messages actifs** et **actuel** les valeurs sont désormais 0.
   
    ![Longueur de la file d’attente][queue-message-receive]

Félicitations ! Vous avez maintenant créé une file d’attente, envoyé un message et reçu un message.

## <a name="next-steps"></a>Étapes suivantes

Découvrez notre [référentiel GitHub avec des exemples](https://github.com/Azure/azure-service-bus/tree/master/samples) qui illustrent certaines hello plus avancés des fonctionnalités de messagerie Service Bus.

<!--Image references-->

[nuget-pkg]: ./media/service-bus-dotnet-get-started-with-queues/nuget-package.png
[queue-message]: ./media/service-bus-dotnet-get-started-with-queues/queue-message.png
[queue-message-receive]: ./media/service-bus-dotnet-get-started-with-queues/queue-message-receive.png
[github-samples]: https://github.com/Azure-Samples/azure-servicebus-messaging-samples
