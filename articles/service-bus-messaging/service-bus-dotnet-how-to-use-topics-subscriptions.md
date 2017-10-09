---
title: "aaaGet a démarré avec des rubriques et abonnements Azure Service Bus | Documents Microsoft"
description: "Écrivez une application console C# qui utilise les rubriques et les abonnements de messageries Service Bus."
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: service-bus-messaging
ms.devlang: tbd
ms.topic: hero-article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 06/30/2017
ms.author: sethm
ms.openlocfilehash: 619d602599d97ecff2ded0681a383b19f1a8b7ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-service-bus-topics"></a>Prise en main des rubriques Service Bus

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

## <a name="what-will-be-accomplished"></a>Les opérations que nous allons effectuer

Ce didacticiel couvre hello comme suit :

1. Créer un espace de noms Service Bus, à l’aide de hello portail Azure.
2. Créez une rubrique Service Bus, à l’aide de hello portail Azure.
3. Créer une abonnement toothat la rubrique Service Bus, à l’aide de hello portail Azure.
4. Écrire un toosend d’application console une rubrique toohello de message.
5. Écrire un tooreceive d’application console qu’un message d’abonnement de hello.

## <a name="prerequisites"></a>Composants requis

1. [Visual Studio 2015 ou une version ultérieure](http://www.visualstudio.com). exemples de Hello dans ce didacticiel utilisent Visual Studio 2017.
2. Un abonnement Azure.

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="1-create-a-namespace-using-hello-azure-portal"></a>1. Créer un espace de noms à l’aide de hello portail Azure

Si vous avez déjà créé un espace de noms de messagerie Service Bus, raccourcis toohello [créer une rubrique à l’aide de hello portail Azure](#2-create-a-topic-using-the-azure-portal) section.

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="2-create-a-topic-using-hello-azure-portal"></a>2. Créez une rubrique à l’aide de hello portail Azure

1. Ouvrez une session sur toohello [portail Azure][azure-portal].
2. Dans le volet de navigation gauche hello du portail de hello, cliquez sur **Service Bus** (si vous ne voyez pas **Service Bus**, cliquez sur **davantage de services**).
3. Cliquez sur hello espace de noms dans lequel vous souhaitez que rubrique de hello toocreate. Panneau de vue d’ensemble d’espace de noms Hello s’affiche :
   
    ![Création d'une rubrique][createtopic1]
4. Bonjour **espace de noms Service Bus** panneau, cliquez sur **rubriques**, puis cliquez sur **ajouter rubrique**.
   
    ![Sélectionnez les rubriques][createtopic2]
5. Entrez un nom pour la rubrique de hello et décochez hello **activer leur partitionnement** option. Laissez hello autres options avec leurs valeurs par défaut.
   
    ![Sélectionner Nouveau][createtopic3]
6. Au bas de hello du Panneau de hello, cliquez sur **créer**.

## <a name="3-create-a-subscription-toohello-topic"></a>3. Créer une rubrique toohello d’abonnement

1. Dans le volet du portail de ressources hello, cliquez sur espace de noms hello créé à l’étape 1, puis cliquez sur le nom de rubrique hello créé à l’étape 2.
2. Top hello du volet de présentation hello, cliquez sur hello plus se connecter ensuite trop**abonnement** tooadd une rubrique toothis d’abonnement.

    ![Créer un abonnement][createtopic4]

3. Entrez un nom pour l’abonnement de hello. Laissez hello autres options avec leurs valeurs par défaut.

## <a name="4-send-messages-toohello-topic"></a>4. Rubrique toohello de messages d’envoi

rubrique de toohello toosend messages, nous écrire une application console c# à l’aide de Visual Studio.

### <a name="create-a-console-application"></a>Création d’une application console

Ouvrez Visual Studio et créez un projet **Application de console (.NET Framework)**.

### <a name="add-hello-service-bus-nuget-package"></a>Ajoutez le package NuGet Service Bus de hello

1. Avec le bouton droit de projet de hello nouvellement créé et sélectionnez **gérer les Packages NuGet**.
2. Cliquez sur hello **Parcourir** onglet, recherchez **Microsoft Azure Service Bus**, puis sélectionnez hello **WindowsAzure.ServiceBus** élément. Cliquez sur **installer** toocomplete hello installation, puis fermez cette boîte de dialogue.
   
    ![Sélectionner un package NuGet][nuget-pkg]

### <a name="write-some-code-toosend-a-message-toohello-topic"></a>Écrire certaines toosend code une rubrique toohello de message

1. Ajoutez hello suit `using` haut de toohello instruction du fichier Program.cs de hello.
   
    ```csharp
    using Microsoft.ServiceBus.Messaging;
    ```
2. Ajouter hello suivant code toohello `Main` (méthode). Ensemble hello `connectionString` que vous avez obtenu lors de la création d’espace de noms hello et définir de chaîne de connexion de la variable toohello `topicName` toohello nom que vous avez utilisé lors de la création de la rubrique hello.
   
    ```csharp
    var connectionString = "<your connection string>";
    var topicName = "<your topic name>";
   
    var client = TopicClient.CreateFromConnectionString(connectionString, topicName);
    var message = new BrokeredMessage("This is a test message!");

    Console.WriteLine(String.Format("Message body: {0}", message.GetBody<String>()));
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

    namespace tsend
    {
        class Program
        {
            static void Main(string[] args)
            {
                var connectionString = "Endpoint=sb://<your namespace>.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=<your key>";
                var topicName = "<your topic name>";

                var client = TopicClient.CreateFromConnectionString(connectionString, topicName);
                var message = new BrokeredMessage("This is a test message!");

                Console.WriteLine(String.Format("Message body: {0}", message.GetBody<String>()));
                Console.WriteLine(String.Format("Message id: {0}", message.MessageId));

                client.Send(message);

                Console.WriteLine("Message successfully sent! Press ENTER tooexit program");
                Console.ReadLine();
            }
        }
    }
    ```
3. Exécuter le programme de hello et vérifier hello portail Azure : cliquez sur nom hello de votre rubrique dans l’espace de noms hello **vue d’ensemble** panneau. rubrique de Hello **Essentials** panneau s’affiche. Dans les abonnements hello répertoriés bas hello du Panneau de hello, notez que hello **nombre de messages** valeur pour chaque abonnement doit maintenant être 1. Chaque fois que vous exécutez l’application d’expédition hello sans récupérer les messages de type hello (comme décrit dans la section suivante de hello), cette valeur augmente de 1. Notez également que taille actuelle de hello Hello d’incréments hello rubrique **actuel** valeur sur hello **Essentials** panneau chaque fois application hello ajoute un message toohello rubrique / d’abonnement.
   
      ![Taille des messages][topic-message]

## <a name="5-receive-messages-from-hello-subscription"></a>5. Recevoir des messages à partir de l’abonnement de hello

1. hello tooreceive ou les messages que vous venez d’envoyer, créer une nouvelle application console et ajouter un package NuGet Service Bus toohello référence, l’application expéditeur précédente toohello similaire.
2. Ajoutez hello suit `using` haut de toohello instruction du fichier Program.cs de hello.
   
    ```csharp
    using Microsoft.ServiceBus.Messaging;
    ```
3. Ajouter hello suivant code toohello `Main` (méthode). Ensemble hello `connectionString` vous obtenu lors de la création d’espace de noms hello et définir de chaîne de connexion de la variable toohello `topicName` toohello nom que vous avez utilisé lors de la création de la rubrique hello.
   
    ```csharp
    var connectionString = "<your connection string>";
    var topicName = "<your topic name>";
   
    var client = SubscriptionClient.CreateFromConnectionString(connectionString, topicName, "<your subscription name>");
   
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
   
    namespace GettingStartedWithTopics
    {
      class Program
      {
        static void Main(string[] args)
        {
          var connectionString = "Endpoint=sb://<your namespace>.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=<your key>";;
          var topicName = "<your topic name>";
   
          var client = SubscriptionClient.CreateFromConnectionString(connectionString, topicName, "<your subscription name>");
   
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
4. Exécuter le programme de hello et vérifiez de nouveau portail de hello. Notez que hello **nombre de messages** et **actuel** les valeurs sont désormais 0.
   
    ![Longueur de la rubrique][topic-message-receive]

Félicitations ! Vous avez créé une rubrique et un abonnement, envoyé un message et reçu ce message.

## <a name="next-steps"></a>Étapes suivantes

Découvrez notre [référentiel GitHub avec des exemples](https://github.com/Azure/azure-service-bus/tree/master/samples) qui illustrent certaines hello plus avancés des fonctionnalités de messagerie Service Bus.

<!--Image references-->

[nuget-pkg]: ./media/service-bus-dotnet-how-to-use-topics-subscriptions/nuget-package.png
[topic-message]: ./media/service-bus-dotnet-how-to-use-topics-subscriptions/topic-message.png
[topic-message-receive]: ./media/service-bus-dotnet-how-to-use-topics-subscriptions/topic-message-receive.png
[createtopic1]: ./media/service-bus-dotnet-how-to-use-topics-subscriptions/create-topic1.png
[createtopic2]: ./media/service-bus-dotnet-how-to-use-topics-subscriptions/create-topic2.png
[createtopic3]: ./media/service-bus-dotnet-how-to-use-topics-subscriptions/create-topic3.png
[createtopic4]: ./media/service-bus-dotnet-how-to-use-topics-subscriptions/create-topic4.png
[github-samples]: https://github.com/Azure-Samples/azure-servicebus-messaging-samples
[azure-portal]: https://portal.azure.com
