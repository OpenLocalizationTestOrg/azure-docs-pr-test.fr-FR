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
# <a name="get-started-with-service-bus-topics"></a><span data-ttu-id="fbaf7-103">Prise en main des rubriques Service Bus</span><span class="sxs-lookup"><span data-stu-id="fbaf7-103">Get started with Service Bus topics</span></span>

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

## <a name="what-will-be-accomplished"></a><span data-ttu-id="fbaf7-104">Les opérations que nous allons effectuer</span><span class="sxs-lookup"><span data-stu-id="fbaf7-104">What will be accomplished</span></span>

<span data-ttu-id="fbaf7-105">Ce didacticiel couvre hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="fbaf7-105">This tutorial covers hello following steps:</span></span>

1. <span data-ttu-id="fbaf7-106">Créer un espace de noms Service Bus, à l’aide de hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="fbaf7-106">Create a Service Bus namespace, using hello Azure portal.</span></span>
2. <span data-ttu-id="fbaf7-107">Créez une rubrique Service Bus, à l’aide de hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="fbaf7-107">Create a Service Bus topic, using hello Azure portal.</span></span>
3. <span data-ttu-id="fbaf7-108">Créer une abonnement toothat la rubrique Service Bus, à l’aide de hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="fbaf7-108">Create a Service Bus subscription toothat topic, using hello Azure portal.</span></span>
4. <span data-ttu-id="fbaf7-109">Écrire un toosend d’application console une rubrique toohello de message.</span><span class="sxs-lookup"><span data-stu-id="fbaf7-109">Write a console application toosend a message toohello topic.</span></span>
5. <span data-ttu-id="fbaf7-110">Écrire un tooreceive d’application console qu’un message d’abonnement de hello.</span><span class="sxs-lookup"><span data-stu-id="fbaf7-110">Write a console application tooreceive that message from hello subscription.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fbaf7-111">Composants requis</span><span class="sxs-lookup"><span data-stu-id="fbaf7-111">Prerequisites</span></span>

1. <span data-ttu-id="fbaf7-112">[Visual Studio 2015 ou une version ultérieure](http://www.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="fbaf7-112">[Visual Studio 2015 or higher](http://www.visualstudio.com).</span></span> <span data-ttu-id="fbaf7-113">exemples de Hello dans ce didacticiel utilisent Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="fbaf7-113">hello examples in this tutorial use Visual Studio 2017.</span></span>
2. <span data-ttu-id="fbaf7-114">Un abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="fbaf7-114">An Azure subscription.</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="1-create-a-namespace-using-hello-azure-portal"></a><span data-ttu-id="fbaf7-115">1. Créer un espace de noms à l’aide de hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="fbaf7-115">1. Create a namespace using hello Azure portal</span></span>

<span data-ttu-id="fbaf7-116">Si vous avez déjà créé un espace de noms de messagerie Service Bus, raccourcis toohello [créer une rubrique à l’aide de hello portail Azure](#2-create-a-topic-using-the-azure-portal) section.</span><span class="sxs-lookup"><span data-stu-id="fbaf7-116">If you have already created a Service Bus Messaging namespace, jump toohello [Create a topic using hello Azure portal](#2-create-a-topic-using-the-azure-portal) section.</span></span>

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="2-create-a-topic-using-hello-azure-portal"></a><span data-ttu-id="fbaf7-117">2. Créez une rubrique à l’aide de hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="fbaf7-117">2. Create a topic using hello Azure portal</span></span>

1. <span data-ttu-id="fbaf7-118">Ouvrez une session sur toohello [portail Azure][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="fbaf7-118">Log on toohello [Azure portal][azure-portal].</span></span>
2. <span data-ttu-id="fbaf7-119">Dans le volet de navigation gauche hello du portail de hello, cliquez sur **Service Bus** (si vous ne voyez pas **Service Bus**, cliquez sur **davantage de services**).</span><span class="sxs-lookup"><span data-stu-id="fbaf7-119">In hello left navigation pane of hello portal, click **Service Bus** (if you don't see **Service Bus**, click **More services**).</span></span>
3. <span data-ttu-id="fbaf7-120">Cliquez sur hello espace de noms dans lequel vous souhaitez que rubrique de hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="fbaf7-120">Click hello namespace in which you would like toocreate hello topic.</span></span> <span data-ttu-id="fbaf7-121">Panneau de vue d’ensemble d’espace de noms Hello s’affiche :</span><span class="sxs-lookup"><span data-stu-id="fbaf7-121">hello namespace overview blade appears:</span></span>
   
    ![Création d'une rubrique][createtopic1]
4. <span data-ttu-id="fbaf7-123">Bonjour **espace de noms Service Bus** panneau, cliquez sur **rubriques**, puis cliquez sur **ajouter rubrique**.</span><span class="sxs-lookup"><span data-stu-id="fbaf7-123">In hello **Service Bus namespace** blade, click **Topics**, then click **Add topic**.</span></span>
   
    ![Sélectionnez les rubriques][createtopic2]
5. <span data-ttu-id="fbaf7-125">Entrez un nom pour la rubrique de hello et décochez hello **activer leur partitionnement** option.</span><span class="sxs-lookup"><span data-stu-id="fbaf7-125">Enter a name for hello topic, and uncheck hello **Enable partitioning** option.</span></span> <span data-ttu-id="fbaf7-126">Laissez hello autres options avec leurs valeurs par défaut.</span><span class="sxs-lookup"><span data-stu-id="fbaf7-126">Leave hello other options with their default values.</span></span>
   
    ![Sélectionner Nouveau][createtopic3]
6. <span data-ttu-id="fbaf7-128">Au bas de hello du Panneau de hello, cliquez sur **créer**.</span><span class="sxs-lookup"><span data-stu-id="fbaf7-128">At hello bottom of hello blade, click **Create**.</span></span>

## <a name="3-create-a-subscription-toohello-topic"></a><span data-ttu-id="fbaf7-129">3. Créer une rubrique toohello d’abonnement</span><span class="sxs-lookup"><span data-stu-id="fbaf7-129">3. Create a subscription toohello topic</span></span>

1. <span data-ttu-id="fbaf7-130">Dans le volet du portail de ressources hello, cliquez sur espace de noms hello créé à l’étape 1, puis cliquez sur le nom de rubrique hello créé à l’étape 2.</span><span class="sxs-lookup"><span data-stu-id="fbaf7-130">In hello portal resources pane, click hello namespace you created in step 1, then click name of hello topic you created in step 2.</span></span>
2. <span data-ttu-id="fbaf7-131">Top hello du volet de présentation hello, cliquez sur hello plus se connecter ensuite trop**abonnement** tooadd une rubrique toothis d’abonnement.</span><span class="sxs-lookup"><span data-stu-id="fbaf7-131">A hello top of hello overview pane, click hello plus sign next too**Subscription** tooadd a subscription toothis topic.</span></span>

    ![Créer un abonnement][createtopic4]

3. <span data-ttu-id="fbaf7-133">Entrez un nom pour l’abonnement de hello.</span><span class="sxs-lookup"><span data-stu-id="fbaf7-133">Enter a name for hello subscription.</span></span> <span data-ttu-id="fbaf7-134">Laissez hello autres options avec leurs valeurs par défaut.</span><span class="sxs-lookup"><span data-stu-id="fbaf7-134">Leave hello other options with their default values.</span></span>

## <a name="4-send-messages-toohello-topic"></a><span data-ttu-id="fbaf7-135">4. Rubrique toohello de messages d’envoi</span><span class="sxs-lookup"><span data-stu-id="fbaf7-135">4. Send messages toohello topic</span></span>

<span data-ttu-id="fbaf7-136">rubrique de toohello toosend messages, nous écrire une application console c# à l’aide de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="fbaf7-136">toosend messages toohello topic, we write a C# console application using Visual Studio.</span></span>

### <a name="create-a-console-application"></a><span data-ttu-id="fbaf7-137">Création d’une application console</span><span class="sxs-lookup"><span data-stu-id="fbaf7-137">Create a console application</span></span>

<span data-ttu-id="fbaf7-138">Ouvrez Visual Studio et créez un projet **Application de console (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="fbaf7-138">Launch Visual Studio and create a new **Console app (.NET Framework)** project.</span></span>

### <a name="add-hello-service-bus-nuget-package"></a><span data-ttu-id="fbaf7-139">Ajoutez le package NuGet Service Bus de hello</span><span class="sxs-lookup"><span data-stu-id="fbaf7-139">Add hello Service Bus NuGet package</span></span>

1. <span data-ttu-id="fbaf7-140">Avec le bouton droit de projet de hello nouvellement créé et sélectionnez **gérer les Packages NuGet**.</span><span class="sxs-lookup"><span data-stu-id="fbaf7-140">Right-click hello newly created project and select **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="fbaf7-141">Cliquez sur hello **Parcourir** onglet, recherchez **Microsoft Azure Service Bus**, puis sélectionnez hello **WindowsAzure.ServiceBus** élément.</span><span class="sxs-lookup"><span data-stu-id="fbaf7-141">Click hello **Browse** tab, search for **Microsoft Azure Service Bus**, and then select hello **WindowsAzure.ServiceBus** item.</span></span> <span data-ttu-id="fbaf7-142">Cliquez sur **installer** toocomplete hello installation, puis fermez cette boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="fbaf7-142">Click **Install** toocomplete hello installation, then close this dialog box.</span></span>
   
    ![Sélectionner un package NuGet][nuget-pkg]

### <a name="write-some-code-toosend-a-message-toohello-topic"></a><span data-ttu-id="fbaf7-144">Écrire certaines toosend code une rubrique toohello de message</span><span class="sxs-lookup"><span data-stu-id="fbaf7-144">Write some code toosend a message toohello topic</span></span>

1. <span data-ttu-id="fbaf7-145">Ajoutez hello suit `using` haut de toohello instruction du fichier Program.cs de hello.</span><span class="sxs-lookup"><span data-stu-id="fbaf7-145">Add hello following `using` statement toohello top of hello Program.cs file.</span></span>
   
    ```csharp
    using Microsoft.ServiceBus.Messaging;
    ```
2. <span data-ttu-id="fbaf7-146">Ajouter hello suivant code toohello `Main` (méthode).</span><span class="sxs-lookup"><span data-stu-id="fbaf7-146">Add hello following code toohello `Main` method.</span></span> <span data-ttu-id="fbaf7-147">Ensemble hello `connectionString` que vous avez obtenu lors de la création d’espace de noms hello et définir de chaîne de connexion de la variable toohello `topicName` toohello nom que vous avez utilisé lors de la création de la rubrique hello.</span><span class="sxs-lookup"><span data-stu-id="fbaf7-147">Set hello `connectionString` variable toohello connection string that you obtained when creating hello namespace, and set `topicName` toohello name that you used when creating hello topic.</span></span>
   
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
   
    <span data-ttu-id="fbaf7-148">Voici à quoi doit ressembler votre fichier Program.cs.</span><span class="sxs-lookup"><span data-stu-id="fbaf7-148">Here is what your Program.cs file should look like.</span></span>
   
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
3. <span data-ttu-id="fbaf7-149">Exécuter le programme de hello et vérifier hello portail Azure : cliquez sur nom hello de votre rubrique dans l’espace de noms hello **vue d’ensemble** panneau.</span><span class="sxs-lookup"><span data-stu-id="fbaf7-149">Run hello program, and check hello Azure portal: click hello name of your topic in hello namespace **Overview** blade.</span></span> <span data-ttu-id="fbaf7-150">rubrique de Hello **Essentials** panneau s’affiche.</span><span class="sxs-lookup"><span data-stu-id="fbaf7-150">hello topic **Essentials** blade is displayed.</span></span> <span data-ttu-id="fbaf7-151">Dans les abonnements hello répertoriés bas hello du Panneau de hello, notez que hello **nombre de messages** valeur pour chaque abonnement doit maintenant être 1.</span><span class="sxs-lookup"><span data-stu-id="fbaf7-151">In hello subscription(s) listed near hello bottom of hello blade, notice that hello **Message Count** value for each subscription should now be 1.</span></span> <span data-ttu-id="fbaf7-152">Chaque fois que vous exécutez l’application d’expédition hello sans récupérer les messages de type hello (comme décrit dans la section suivante de hello), cette valeur augmente de 1.</span><span class="sxs-lookup"><span data-stu-id="fbaf7-152">Each time you run hello sender application without retrieving hello messages (as described in hello next section), this value increases by 1.</span></span> <span data-ttu-id="fbaf7-153">Notez également que taille actuelle de hello Hello d’incréments hello rubrique **actuel** valeur sur hello **Essentials** panneau chaque fois application hello ajoute un message toohello rubrique / d’abonnement.</span><span class="sxs-lookup"><span data-stu-id="fbaf7-153">Also note that hello current size of hello topic increments hello **Current** value on hello **Essentials** blade each time hello app adds a message toohello topic/subscription.</span></span>
   
      ![Taille des messages][topic-message]

## <a name="5-receive-messages-from-hello-subscription"></a><span data-ttu-id="fbaf7-155">5. Recevoir des messages à partir de l’abonnement de hello</span><span class="sxs-lookup"><span data-stu-id="fbaf7-155">5. Receive messages from hello subscription</span></span>

1. <span data-ttu-id="fbaf7-156">hello tooreceive ou les messages que vous venez d’envoyer, créer une nouvelle application console et ajouter un package NuGet Service Bus toohello référence, l’application expéditeur précédente toohello similaire.</span><span class="sxs-lookup"><span data-stu-id="fbaf7-156">tooreceive hello message or messages you just sent, create a new console application and add a reference toohello Service Bus NuGet package, similar toohello previous sender application.</span></span>
2. <span data-ttu-id="fbaf7-157">Ajoutez hello suit `using` haut de toohello instruction du fichier Program.cs de hello.</span><span class="sxs-lookup"><span data-stu-id="fbaf7-157">Add hello following `using` statement toohello top of hello Program.cs file.</span></span>
   
    ```csharp
    using Microsoft.ServiceBus.Messaging;
    ```
3. <span data-ttu-id="fbaf7-158">Ajouter hello suivant code toohello `Main` (méthode).</span><span class="sxs-lookup"><span data-stu-id="fbaf7-158">Add hello following code toohello `Main` method.</span></span> <span data-ttu-id="fbaf7-159">Ensemble hello `connectionString` vous obtenu lors de la création d’espace de noms hello et définir de chaîne de connexion de la variable toohello `topicName` toohello nom que vous avez utilisé lors de la création de la rubrique hello.</span><span class="sxs-lookup"><span data-stu-id="fbaf7-159">Set hello `connectionString` variable toohello connection string you obtained when creating hello namespace, and set `topicName` toohello name that you used when creating hello topic.</span></span>
   
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
   
    <span data-ttu-id="fbaf7-160">Voici à quoi doit ressembler votre fichier Program.cs :</span><span class="sxs-lookup"><span data-stu-id="fbaf7-160">Here is what your Program.cs file should look like:</span></span>
   
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
4. <span data-ttu-id="fbaf7-161">Exécuter le programme de hello et vérifiez de nouveau portail de hello.</span><span class="sxs-lookup"><span data-stu-id="fbaf7-161">Run hello program, and check hello portal again.</span></span> <span data-ttu-id="fbaf7-162">Notez que hello **nombre de messages** et **actuel** les valeurs sont désormais 0.</span><span class="sxs-lookup"><span data-stu-id="fbaf7-162">Notice that hello **Message Count** and **Current** values are now 0.</span></span>
   
    ![Longueur de la rubrique][topic-message-receive]

<span data-ttu-id="fbaf7-164">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="fbaf7-164">Congratulations!</span></span> <span data-ttu-id="fbaf7-165">Vous avez créé une rubrique et un abonnement, envoyé un message et reçu ce message.</span><span class="sxs-lookup"><span data-stu-id="fbaf7-165">You have now created a topic and subscription, sent a message, and received that message.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fbaf7-166">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="fbaf7-166">Next steps</span></span>

<span data-ttu-id="fbaf7-167">Découvrez notre [référentiel GitHub avec des exemples](https://github.com/Azure/azure-service-bus/tree/master/samples) qui illustrent certaines hello plus avancés des fonctionnalités de messagerie Service Bus.</span><span class="sxs-lookup"><span data-stu-id="fbaf7-167">Check out our [GitHub repository with samples](https://github.com/Azure/azure-service-bus/tree/master/samples) that demonstrate some of hello more advanced features of Service Bus messaging.</span></span>

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
