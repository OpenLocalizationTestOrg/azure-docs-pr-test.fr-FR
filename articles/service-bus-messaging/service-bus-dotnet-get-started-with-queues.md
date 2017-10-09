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
# <a name="get-started-with-service-bus-queues"></a><span data-ttu-id="55794-103">Prise en main des files d’attente Service Bus</span><span class="sxs-lookup"><span data-stu-id="55794-103">Get started with Service Bus queues</span></span>
[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

## <a name="what-will-be-accomplished"></a><span data-ttu-id="55794-104">Les opérations que nous allons effectuer</span><span class="sxs-lookup"><span data-stu-id="55794-104">What will be accomplished</span></span>
<span data-ttu-id="55794-105">Ce didacticiel couvre hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="55794-105">This tutorial covers hello following steps:</span></span>

1. <span data-ttu-id="55794-106">Créer un espace de noms Service Bus, à l’aide de hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="55794-106">Create a Service Bus namespace, using hello Azure portal.</span></span>
2. <span data-ttu-id="55794-107">Créer une file d’attente Service Bus, à l’aide de hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="55794-107">Create a Service Bus queue, using hello Azure portal.</span></span>
3. <span data-ttu-id="55794-108">Écrire un toosend d’application console à un message.</span><span class="sxs-lookup"><span data-stu-id="55794-108">Write a console application toosend a message.</span></span>
4. <span data-ttu-id="55794-109">Écrire des messages envoyés à l’étape précédente de hello un Bonjour de tooreceive d’application console.</span><span class="sxs-lookup"><span data-stu-id="55794-109">Write a console application tooreceive hello messages sent in hello previous step.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="55794-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="55794-110">Prerequisites</span></span>
1. <span data-ttu-id="55794-111">[Visual Studio 2015 ou une version ultérieure](http://www.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="55794-111">[Visual Studio 2015 or higher](http://www.visualstudio.com).</span></span> <span data-ttu-id="55794-112">exemples de Hello dans ce didacticiel utilisent Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="55794-112">hello examples in this tutorial use Visual Studio 2017.</span></span>
2. <span data-ttu-id="55794-113">Un abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="55794-113">An Azure subscription.</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="1-create-a-namespace-using-hello-azure-portal"></a><span data-ttu-id="55794-114">1. Créer un espace de noms à l’aide de hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="55794-114">1. Create a namespace using hello Azure portal</span></span>
<span data-ttu-id="55794-115">Si vous avez déjà créé un espace de noms de messagerie Service Bus, raccourcis toohello [créer une file d’attente à l’aide de hello portail Azure](#2-create-a-queue-using-the-azure-portal) section.</span><span class="sxs-lookup"><span data-stu-id="55794-115">If you've already created a Service Bus Messaging namespace, jump toohello [Create a queue using hello Azure portal](#2-create-a-queue-using-the-azure-portal) section.</span></span>

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="2-create-a-queue-using-hello-azure-portal"></a><span data-ttu-id="55794-116">2. Créer une file d’attente à l’aide de hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="55794-116">2. Create a queue using hello Azure portal</span></span>
<span data-ttu-id="55794-117">Si vous avez déjà créé une file d’attente Service Bus, raccourcis toohello [file d’attente de toohello de messages envoi](#3-send-messages-to-the-queue) section.</span><span class="sxs-lookup"><span data-stu-id="55794-117">If you have already created a Service Bus queue, jump toohello [Send messages toohello queue](#3-send-messages-to-the-queue) section.</span></span>

[!INCLUDE [service-bus-create-queue-portal](../../includes/service-bus-create-queue-portal.md)]

## <a name="3-send-messages-toohello-queue"></a><span data-ttu-id="55794-118">3. Envoyer la file d’attente de messages toohello</span><span class="sxs-lookup"><span data-stu-id="55794-118">3. Send messages toohello queue</span></span>
<span data-ttu-id="55794-119">file d’attente toosend messages toohello, nous écrire une application console c# à l’aide de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="55794-119">toosend messages toohello queue, we write a C# console application using Visual Studio.</span></span>

### <a name="create-a-console-application"></a><span data-ttu-id="55794-120">Création d’une application console</span><span class="sxs-lookup"><span data-stu-id="55794-120">Create a console application</span></span>

<span data-ttu-id="55794-121">Ouvrez Visual Studio et créez un projet **Application de console (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="55794-121">Launch Visual Studio and create a new **Console app (.NET Framework)** project.</span></span>

### <a name="add-hello-service-bus-nuget-package"></a><span data-ttu-id="55794-122">Ajoutez le package NuGet Service Bus de hello</span><span class="sxs-lookup"><span data-stu-id="55794-122">Add hello Service Bus NuGet package</span></span>
1. <span data-ttu-id="55794-123">Avec le bouton droit de projet de hello nouvellement créé et sélectionnez **gérer les Packages NuGet**.</span><span class="sxs-lookup"><span data-stu-id="55794-123">Right-click hello newly created project and select **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="55794-124">Cliquez sur hello **Parcourir** onglet, recherchez **Microsoft Azure Service Bus**, puis sélectionnez hello **WindowsAzure.ServiceBus** élément.</span><span class="sxs-lookup"><span data-stu-id="55794-124">Click hello **Browse** tab, search for **Microsoft Azure Service Bus**, and then select hello **WindowsAzure.ServiceBus** item.</span></span> <span data-ttu-id="55794-125">Cliquez sur **installer** toocomplete hello installation, puis fermez cette boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="55794-125">Click **Install** toocomplete hello installation, then close this dialog box.</span></span>
   
    ![Sélectionner un package NuGet][nuget-pkg]

### <a name="write-some-code-toosend-a-message-toohello-queue"></a><span data-ttu-id="55794-127">Écrire certaines toosend code une file d’attente de messages toohello</span><span class="sxs-lookup"><span data-stu-id="55794-127">Write some code toosend a message toohello queue</span></span>
1. <span data-ttu-id="55794-128">Ajoutez hello suit `using` haut de toohello instruction du fichier Program.cs de hello.</span><span class="sxs-lookup"><span data-stu-id="55794-128">Add hello following `using` statement toohello top of hello Program.cs file.</span></span>
   
    ```csharp
    using Microsoft.ServiceBus.Messaging;
    ```
2. <span data-ttu-id="55794-129">Ajouter hello suivant code toohello `Main` (méthode).</span><span class="sxs-lookup"><span data-stu-id="55794-129">Add hello following code toohello `Main` method.</span></span> <span data-ttu-id="55794-130">Ensemble hello `connectionString` que vous avez obtenu lors de la création d’espace de noms hello et définir de chaîne de connexion de la variable toohello `queueName` nom de file d’attente toohello que vous avez utilisé lors de la création de file d’attente hello.</span><span class="sxs-lookup"><span data-stu-id="55794-130">Set hello `connectionString` variable toohello connection string that you obtained when creating hello namespace, and set `queueName` toohello queue name that you used when creating hello queue.</span></span>
   
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
   
    <span data-ttu-id="55794-131">Voici à quoi doit ressembler votre fichier Program.cs.</span><span class="sxs-lookup"><span data-stu-id="55794-131">Here is what your Program.cs file should look like.</span></span>
   
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
3. <span data-ttu-id="55794-132">Exécuter le programme de hello et vérifier hello portail Azure : cliquez sur nom hello de votre file d’attente dans l’espace de noms hello **vue d’ensemble** panneau.</span><span class="sxs-lookup"><span data-stu-id="55794-132">Run hello program, and check hello Azure portal: click hello name of your queue in hello namespace **Overview** blade.</span></span> <span data-ttu-id="55794-133">file d’attente Hello **Essentials** panneau s’affiche.</span><span class="sxs-lookup"><span data-stu-id="55794-133">hello queue **Essentials** blade is displayed.</span></span> <span data-ttu-id="55794-134">Notez que hello **nombre de messages actifs** valeur doit maintenant être 1.</span><span class="sxs-lookup"><span data-stu-id="55794-134">Notice that hello **Active Message Count** value should now be 1.</span></span> <span data-ttu-id="55794-135">Chaque fois que vous exécutez l’application d’expédition hello sans récupérer les messages de type hello, cette valeur augmente de 1.</span><span class="sxs-lookup"><span data-stu-id="55794-135">Each time you run hello sender application without retrieving hello messages, this value increases by 1.</span></span> <span data-ttu-id="55794-136">Notez que taille actuelle de hello de file d’attente hello incrémente chaque application hello de temps ajoute également une file d’attente de message toohello.</span><span class="sxs-lookup"><span data-stu-id="55794-136">Also note that hello current size of hello queue increments each time hello app adds a message toohello queue.</span></span>
   
      ![Taille des messages][queue-message]

## <a name="4-receive-messages-from-hello-queue"></a><span data-ttu-id="55794-138">4. Recevoir des messages à partir de la file d’attente hello</span><span class="sxs-lookup"><span data-stu-id="55794-138">4. Receive messages from hello queue</span></span>

1. <span data-ttu-id="55794-139">messages de type hello tooreceive vous venez d’envoyer, créer une nouvelle application console et ajouter un package NuGet Service Bus toohello référence, l’application expéditeur précédente toohello similaire.</span><span class="sxs-lookup"><span data-stu-id="55794-139">tooreceive hello messages you just sent, create a new console application and add a reference toohello Service Bus NuGet package, similar toohello previous sender application.</span></span>
2. <span data-ttu-id="55794-140">Ajoutez hello suit `using` haut de toohello instruction du fichier Program.cs de hello.</span><span class="sxs-lookup"><span data-stu-id="55794-140">Add hello following `using` statement toohello top of hello Program.cs file.</span></span>
   
    ```csharp
    using Microsoft.ServiceBus.Messaging;
    ```
3. <span data-ttu-id="55794-141">Ajouter hello suivant code toohello `Main` (méthode).</span><span class="sxs-lookup"><span data-stu-id="55794-141">Add hello following code toohello `Main` method.</span></span> <span data-ttu-id="55794-142">Ensemble hello `connectionString` chaîne de connexion toohello variable qui a été obtenu lors de la création d’espace de noms hello et définir `queueName` nom de file d’attente toohello que vous avez utilisé lors de la création de file d’attente hello.</span><span class="sxs-lookup"><span data-stu-id="55794-142">Set hello `connectionString` variable toohello connection string that was obtained when creating hello namespace, and set `queueName` toohello queue name that you used when creating hello queue.</span></span>
   
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
   
    <span data-ttu-id="55794-143">Voici à quoi doit ressembler votre fichier Program.cs :</span><span class="sxs-lookup"><span data-stu-id="55794-143">Here is what your Program.cs file should look like:</span></span>
   
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
4. <span data-ttu-id="55794-144">Exécuter le programme de hello et vérifiez de nouveau portail de hello.</span><span class="sxs-lookup"><span data-stu-id="55794-144">Run hello program, and check hello portal again.</span></span> <span data-ttu-id="55794-145">Notez que hello **nombre de messages actifs** et **actuel** les valeurs sont désormais 0.</span><span class="sxs-lookup"><span data-stu-id="55794-145">Notice that hello **Active Message Count** and **Current** values are now 0.</span></span>
   
    ![Longueur de la file d’attente][queue-message-receive]

<span data-ttu-id="55794-147">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="55794-147">Congratulations!</span></span> <span data-ttu-id="55794-148">Vous avez maintenant créé une file d’attente, envoyé un message et reçu un message.</span><span class="sxs-lookup"><span data-stu-id="55794-148">You have now created a queue, sent a message, and received a message.</span></span>

## <a name="next-steps"></a><span data-ttu-id="55794-149">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="55794-149">Next steps</span></span>

<span data-ttu-id="55794-150">Découvrez notre [référentiel GitHub avec des exemples](https://github.com/Azure/azure-service-bus/tree/master/samples) qui illustrent certaines hello plus avancés des fonctionnalités de messagerie Service Bus.</span><span class="sxs-lookup"><span data-stu-id="55794-150">Check out our [GitHub repository with samples](https://github.com/Azure/azure-service-bus/tree/master/samples) that demonstrate some of hello more advanced features of Service Bus messaging.</span></span>

<!--Image references-->

[nuget-pkg]: ./media/service-bus-dotnet-get-started-with-queues/nuget-package.png
[queue-message]: ./media/service-bus-dotnet-get-started-with-queues/queue-message.png
[queue-message-receive]: ./media/service-bus-dotnet-get-started-with-queues/queue-message-receive.png
[github-samples]: https://github.com/Azure-Samples/azure-servicebus-messaging-samples
