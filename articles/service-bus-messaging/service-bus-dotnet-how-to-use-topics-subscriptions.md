---
title: Prise en main des rubriques et abonnements Azure Service Bus | Microsoft Docs
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
ms.openlocfilehash: 9401ada519f600b0d2817f06a396e16607a24129
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-service-bus-topics"></a><span data-ttu-id="25458-103">Prise en main des rubriques Service Bus</span><span class="sxs-lookup"><span data-stu-id="25458-103">Get started with Service Bus topics</span></span>

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

## <a name="what-will-be-accomplished"></a><span data-ttu-id="25458-104">Les opérations que nous allons effectuer</span><span class="sxs-lookup"><span data-stu-id="25458-104">What will be accomplished</span></span>

<span data-ttu-id="25458-105">Ce didacticiel couvre les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="25458-105">This tutorial covers the following steps:</span></span>

1. <span data-ttu-id="25458-106">Créer un espace de noms Service Bus à l’aide du Portail Azure.</span><span class="sxs-lookup"><span data-stu-id="25458-106">Create a Service Bus namespace, using the Azure portal.</span></span>
2. <span data-ttu-id="25458-107">Créer une rubrique Service Bus à l’aide du Portail Azure.</span><span class="sxs-lookup"><span data-stu-id="25458-107">Create a Service Bus topic, using the Azure portal.</span></span>
3. <span data-ttu-id="25458-108">Créer un abonnement Service Bus vers cette rubrique à l’aide du Portail Azure.</span><span class="sxs-lookup"><span data-stu-id="25458-108">Create a Service Bus subscription to that topic, using the Azure portal.</span></span>
4. <span data-ttu-id="25458-109">Écrire une application de console pour envoyer un message vers la rubrique.</span><span class="sxs-lookup"><span data-stu-id="25458-109">Write a console application to send a message to the topic.</span></span>
5. <span data-ttu-id="25458-110">Écrivez une application console pour recevoir ce message depuis l’abonnement.</span><span class="sxs-lookup"><span data-stu-id="25458-110">Write a console application to receive that message from the subscription.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="25458-111">Composants requis</span><span class="sxs-lookup"><span data-stu-id="25458-111">Prerequisites</span></span>

1. <span data-ttu-id="25458-112">[Visual Studio 2015 ou une version ultérieure](http://www.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="25458-112">[Visual Studio 2015 or higher](http://www.visualstudio.com).</span></span> <span data-ttu-id="25458-113">Les exemples de ce didacticiel utilisent Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="25458-113">The examples in this tutorial use Visual Studio 2017.</span></span>
2. <span data-ttu-id="25458-114">Un abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="25458-114">An Azure subscription.</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="1-create-a-namespace-using-the-azure-portal"></a><span data-ttu-id="25458-115">1. Créer un espace de noms à l’aide du Portail Azure</span><span class="sxs-lookup"><span data-stu-id="25458-115">1. Create a namespace using the Azure portal</span></span>

<span data-ttu-id="25458-116">Si vous avez déjà créé un espace de noms Service Bus Messaging, passez directement à la section [Créer une rubrique à l’aide du portail Azure](#2-create-a-topic-using-the-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="25458-116">If you have already created a Service Bus Messaging namespace, jump to the [Create a topic using the Azure portal](#2-create-a-topic-using-the-azure-portal) section.</span></span>

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="2-create-a-topic-using-the-azure-portal"></a><span data-ttu-id="25458-117">2. Créer une rubrique à l’aide du Portail Azure</span><span class="sxs-lookup"><span data-stu-id="25458-117">2. Create a topic using the Azure portal</span></span>

1. <span data-ttu-id="25458-118">Connectez-vous au [portail Azure][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="25458-118">Log on to the [Azure portal][azure-portal].</span></span>
2. <span data-ttu-id="25458-119">Dans le volet de navigation gauche du portail, cliquez sur **Service Bus** (si vous ne voyez pas **Service Bus**, cliquez sur **Plus de services**).</span><span class="sxs-lookup"><span data-stu-id="25458-119">In the left navigation pane of the portal, click **Service Bus** (if you don't see **Service Bus**, click **More services**).</span></span>
3. <span data-ttu-id="25458-120">Cliquez sur l’espace de noms dans lequel vous souhaitez créer la rubrique.</span><span class="sxs-lookup"><span data-stu-id="25458-120">Click the namespace in which you would like to create the topic.</span></span> <span data-ttu-id="25458-121">Le panneau de vue d’ensemble d’espace de noms s’affiche :</span><span class="sxs-lookup"><span data-stu-id="25458-121">The namespace overview blade appears:</span></span>
   
    ![Création d'une rubrique][createtopic1]
4. <span data-ttu-id="25458-123">Dans le panneau de **l’espace de noms Service Bus**, sélectionnez **Rubriques**, puis cliquez sur **Ajouter une rubrique**.</span><span class="sxs-lookup"><span data-stu-id="25458-123">In the **Service Bus namespace** blade, click **Topics**, then click **Add topic**.</span></span>
   
    ![Sélectionnez les rubriques][createtopic2]
5. <span data-ttu-id="25458-125">Entrez un nom pour la rubrique et désélectionnez l’option **Activer le partitionnement**.</span><span class="sxs-lookup"><span data-stu-id="25458-125">Enter a name for the topic, and uncheck the **Enable partitioning** option.</span></span> <span data-ttu-id="25458-126">Conservez les valeurs par défaut des autres options.</span><span class="sxs-lookup"><span data-stu-id="25458-126">Leave the other options with their default values.</span></span>
   
    ![Sélectionner Nouveau][createtopic3]
6. <span data-ttu-id="25458-128">Au bas du panneau, cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="25458-128">At the bottom of the blade, click **Create**.</span></span>

## <a name="3-create-a-subscription-to-the-topic"></a><span data-ttu-id="25458-129">3. Créer un abonnement à la rubrique</span><span class="sxs-lookup"><span data-stu-id="25458-129">3. Create a subscription to the topic</span></span>

1. <span data-ttu-id="25458-130">Dans le volet ressources du portail, cliquez sur l’espace de noms que vous avez créé à l’étape 1, puis cliquez sur le nom de la rubrique que vous avez créée à l’étape 2.</span><span class="sxs-lookup"><span data-stu-id="25458-130">In the portal resources pane, click the namespace you created in step 1, then click name of the topic you created in step 2.</span></span>
2. <span data-ttu-id="25458-131">Sur la partie supérieure du volet Vue d’ensemble, cliquez sur le signe plus à côté de l’option **Abonnement** pour ajouter un abonnement à cette rubrique.</span><span class="sxs-lookup"><span data-stu-id="25458-131">A the top of the overview pane, click the plus sign next to **Subscription** to add a subscription to this topic.</span></span>

    ![Créer un abonnement][createtopic4]

3. <span data-ttu-id="25458-133">Entrez un nom pour l’abonnement.</span><span class="sxs-lookup"><span data-stu-id="25458-133">Enter a name for the subscription.</span></span> <span data-ttu-id="25458-134">Conservez les valeurs par défaut des autres options.</span><span class="sxs-lookup"><span data-stu-id="25458-134">Leave the other options with their default values.</span></span>

## <a name="4-send-messages-to-the-topic"></a><span data-ttu-id="25458-135">4. Envoyez des messages à la rubrique</span><span class="sxs-lookup"><span data-stu-id="25458-135">4. Send messages to the topic</span></span>

<span data-ttu-id="25458-136">Pour envoyer des messages vers la rubrique, nous écrivons une application de console C# à l’aide de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="25458-136">To send messages to the topic, we write a C# console application using Visual Studio.</span></span>

### <a name="create-a-console-application"></a><span data-ttu-id="25458-137">Création d’une application console</span><span class="sxs-lookup"><span data-stu-id="25458-137">Create a console application</span></span>

<span data-ttu-id="25458-138">Ouvrez Visual Studio et créez un projet **Application de console (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="25458-138">Launch Visual Studio and create a new **Console app (.NET Framework)** project.</span></span>

### <a name="add-the-service-bus-nuget-package"></a><span data-ttu-id="25458-139">Ajout du package NuGet Service Bus</span><span class="sxs-lookup"><span data-stu-id="25458-139">Add the Service Bus NuGet package</span></span>

1. <span data-ttu-id="25458-140">Cliquez avec le bouton droit sur le projet créé et sélectionnez **Gérer les packages NuGet**.</span><span class="sxs-lookup"><span data-stu-id="25458-140">Right-click the newly created project and select **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="25458-141">Cliquez sur l’onglet **Parcourir**, recherchez **Microsoft Azure Service Bus**, puis sélectionnez l’élément **WindowsAzure.ServiceBus**.</span><span class="sxs-lookup"><span data-stu-id="25458-141">Click the **Browse** tab, search for **Microsoft Azure Service Bus**, and then select the **WindowsAzure.ServiceBus** item.</span></span> <span data-ttu-id="25458-142">Cliquez sur **Installer** pour terminer l’installation, puis fermez cette boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="25458-142">Click **Install** to complete the installation, then close this dialog box.</span></span>
   
    ![Sélectionner un package NuGet][nuget-pkg]

### <a name="write-some-code-to-send-a-message-to-the-topic"></a><span data-ttu-id="25458-144">Écrire du code pour envoyer un message vers la rubrique</span><span class="sxs-lookup"><span data-stu-id="25458-144">Write some code to send a message to the topic</span></span>

1. <span data-ttu-id="25458-145">Ajoutez l’instruction `using` suivante au début du fichier Program.cs.</span><span class="sxs-lookup"><span data-stu-id="25458-145">Add the following `using` statement to the top of the Program.cs file.</span></span>
   
    ```csharp
    using Microsoft.ServiceBus.Messaging;
    ```
2. <span data-ttu-id="25458-146">Ajoutez le code suivant à la méthode `Main` .</span><span class="sxs-lookup"><span data-stu-id="25458-146">Add the following code to the `Main` method.</span></span> <span data-ttu-id="25458-147">Configurez la variable `connectionString` en tant que chaîne de connexion obtenue lors de la création de l’espace de noms, puis configurez `topicName` en tant que nom utilisé lors de la création de la rubrique.</span><span class="sxs-lookup"><span data-stu-id="25458-147">Set the `connectionString` variable to the connection string that you obtained when creating the namespace, and set `topicName` to the name that you used when creating the topic.</span></span>
   
    ```csharp
    var connectionString = "<your connection string>";
    var topicName = "<your topic name>";
   
    var client = TopicClient.CreateFromConnectionString(connectionString, topicName);
    var message = new BrokeredMessage("This is a test message!");

    Console.WriteLine(String.Format("Message body: {0}", message.GetBody<String>()));
    Console.WriteLine(String.Format("Message id: {0}", message.MessageId));

    client.Send(message);

    Console.WriteLine("Message successfully sent! Press ENTER to exit program");
    Console.ReadLine();
    ```
   
    <span data-ttu-id="25458-148">Voici à quoi doit ressembler votre fichier Program.cs.</span><span class="sxs-lookup"><span data-stu-id="25458-148">Here is what your Program.cs file should look like.</span></span>
   
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

                Console.WriteLine("Message successfully sent! Press ENTER to exit program");
                Console.ReadLine();
            }
        }
    }
    ```
3. <span data-ttu-id="25458-149">Exécutez le programme et consultez le portail Azure : cliquez sur le nom de votre rubrique dans le panneau de l’espace de noms **Vue d’ensemble**.</span><span class="sxs-lookup"><span data-stu-id="25458-149">Run the program, and check the Azure portal: click the name of your topic in the namespace **Overview** blade.</span></span> <span data-ttu-id="25458-150">Le panneau de rubrique **Fondamentaux** est affiché.</span><span class="sxs-lookup"><span data-stu-id="25458-150">The topic **Essentials** blade is displayed.</span></span> <span data-ttu-id="25458-151">Dans les abonnements répertoriés au bas du panneau, notez que la valeur **Nombre de messages** de chaque abonnement doit désormais être égale à 1.</span><span class="sxs-lookup"><span data-stu-id="25458-151">In the subscription(s) listed near the bottom of the blade, notice that the **Message Count** value for each subscription should now be 1.</span></span> <span data-ttu-id="25458-152">Chaque fois que vous exécutez l’application de l’expéditeur sans récupérer les messages (tel que décrit que la section suivante), cette valeur augmente de 1.</span><span class="sxs-lookup"><span data-stu-id="25458-152">Each time you run the sender application without retrieving the messages (as described in the next section), this value increases by 1.</span></span> <span data-ttu-id="25458-153">Notez également que la taille actuelle de la rubrique incrémente la valeur **Actuel** sur le panneau **Fondamentaux** chaque fois que l’application ajoute un message à la rubrique/l’abonnement.</span><span class="sxs-lookup"><span data-stu-id="25458-153">Also note that the current size of the topic increments the **Current** value on the **Essentials** blade each time the app adds a message to the topic/subscription.</span></span>
   
      ![Taille des messages][topic-message]

## <a name="5-receive-messages-from-the-subscription"></a><span data-ttu-id="25458-155">5. Réception des messages de l’abonnement</span><span class="sxs-lookup"><span data-stu-id="25458-155">5. Receive messages from the subscription</span></span>

1. <span data-ttu-id="25458-156">Pour recevoir le ou les messages que vous venez d’envoyer, créez une application console et ajoutez une référence au package NuGet Service Bus, identique à l’application de l’expéditeur précédente.</span><span class="sxs-lookup"><span data-stu-id="25458-156">To receive the message or messages you just sent, create a new console application and add a reference to the Service Bus NuGet package, similar to the previous sender application.</span></span>
2. <span data-ttu-id="25458-157">Ajoutez l’instruction `using` suivante au début du fichier Program.cs.</span><span class="sxs-lookup"><span data-stu-id="25458-157">Add the following `using` statement to the top of the Program.cs file.</span></span>
   
    ```csharp
    using Microsoft.ServiceBus.Messaging;
    ```
3. <span data-ttu-id="25458-158">Ajoutez le code suivant à la méthode `Main` .</span><span class="sxs-lookup"><span data-stu-id="25458-158">Add the following code to the `Main` method.</span></span> <span data-ttu-id="25458-159">Configurez la variable `connectionString` en tant que chaîne de connexion obtenue lors de la création de l’espace de noms, puis configurez `topicName` en tant que nom utilisé lors de la création de la rubrique.</span><span class="sxs-lookup"><span data-stu-id="25458-159">Set the `connectionString` variable to the connection string you obtained when creating the namespace, and set `topicName` to the name that you used when creating the topic.</span></span>
   
    ```csharp
    var connectionString = "<your connection string>";
    var topicName = "<your topic name>";
   
    var client = SubscriptionClient.CreateFromConnectionString(connectionString, topicName, "<your subscription name>");
   
    client.OnMessage(message =>
    {
      Console.WriteLine(String.Format("Message body: {0}", message.GetBody<String>()));
      Console.WriteLine(String.Format("Message id: {0}", message.MessageId));
    });
   
    Console.WriteLine("Press ENTER to exit program");
    Console.ReadLine();
    ```
   
    <span data-ttu-id="25458-160">Voici à quoi doit ressembler votre fichier Program.cs :</span><span class="sxs-lookup"><span data-stu-id="25458-160">Here is what your Program.cs file should look like:</span></span>
   
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

          Console.WriteLine("Press ENTER to exit program");   
          Console.ReadLine();
        }
      }
    }
    ```
4. <span data-ttu-id="25458-161">Réexécutez le programme et vérifiez le portail.</span><span class="sxs-lookup"><span data-stu-id="25458-161">Run the program, and check the portal again.</span></span> <span data-ttu-id="25458-162">Notez que les valeurs **Nombre de messages** et **Actuel** sont à présent de 0.</span><span class="sxs-lookup"><span data-stu-id="25458-162">Notice that the **Message Count** and **Current** values are now 0.</span></span>
   
    ![Longueur de la rubrique][topic-message-receive]

<span data-ttu-id="25458-164">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="25458-164">Congratulations!</span></span> <span data-ttu-id="25458-165">Vous avez créé une rubrique et un abonnement, envoyé un message et reçu ce message.</span><span class="sxs-lookup"><span data-stu-id="25458-165">You have now created a topic and subscription, sent a message, and received that message.</span></span>

## <a name="next-steps"></a><span data-ttu-id="25458-166">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="25458-166">Next steps</span></span>

<span data-ttu-id="25458-167">Consultez les [référentiels GitHub accompagnés d’exemples](https://github.com/Azure/azure-service-bus/tree/master/samples) qui illustrent certaines des fonctionnalités les plus avancées de la messagerie Service Bus.</span><span class="sxs-lookup"><span data-stu-id="25458-167">Check out our [GitHub repository with samples](https://github.com/Azure/azure-service-bus/tree/master/samples) that demonstrate some of the more advanced features of Service Bus messaging.</span></span>

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
