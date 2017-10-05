---
title: "Recevoir des événements d’Azure Event Hubs avec .Net Standard | Microsoft Docs"
description: "Prise en main de la réception des messages avec EventProcessorHost dans .NET Standard"
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/27/2017
ms.author: sethm
ms.openlocfilehash: cc62792dad0284f9514664795fdfb32e94a85943
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-receiving-messages-with-the-event-processor-host-in-net-standard"></a><span data-ttu-id="1690a-103">Bien démarrer avec la réception de messages à l’aide de l’hôte du processeur d’événements dans .NET Standard</span><span class="sxs-lookup"><span data-stu-id="1690a-103">Get started receiving messages with the Event Processor Host in .NET Standard</span></span>

> [!NOTE]
> <span data-ttu-id="1690a-104">Cet exemple est disponible sur [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver).</span><span class="sxs-lookup"><span data-stu-id="1690a-104">This sample is available on [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver).</span></span>

<span data-ttu-id="1690a-105">Ce didacticiel explique comment écrire une application console .NET Core qui reçoit des messages d’un concentrateur d’événements à l’aide d’**EventProcessorHost**.</span><span class="sxs-lookup"><span data-stu-id="1690a-105">This tutorial shows how to write a .NET Core console application that receives messages from an event hub by using **EventProcessorHost**.</span></span> <span data-ttu-id="1690a-106">Vous pouvez exécuter la solution [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver) telle quelle, en remplaçant les chaînes par vos valeurs de compte de stockage et de concentrateur d’événements.</span><span class="sxs-lookup"><span data-stu-id="1690a-106">You can run the [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver) solution as-is, replacing the strings with your event hub and storage account values.</span></span> <span data-ttu-id="1690a-107">Ou vous pouvez suivre les étapes de ce didacticiel pour créer les vôtres.</span><span class="sxs-lookup"><span data-stu-id="1690a-107">Or you can follow the steps in this tutorial to create your own.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1690a-108">Composants requis</span><span class="sxs-lookup"><span data-stu-id="1690a-108">Prerequisites</span></span>

* <span data-ttu-id="1690a-109">[Microsoft Visual Studio 2015 ou 2017](http://www.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="1690a-109">[Microsoft Visual Studio 2015 or 2017](http://www.visualstudio.com).</span></span> <span data-ttu-id="1690a-110">Les exemples de ce didacticiel utilisent Visual Studio 2017, mais Visual Studio 2015 est également pris en charge.</span><span class="sxs-lookup"><span data-stu-id="1690a-110">The examples in this tutorial use Visual Studio 2017, but Visual Studio 2015 is also supported.</span></span>
* <span data-ttu-id="1690a-111">[Outils Visual Studio 2015 ou 2017 .NET Core](http://www.microsoft.com/net/core).</span><span class="sxs-lookup"><span data-stu-id="1690a-111">[.NET Core Visual Studio 2015 or 2017 tools](http://www.microsoft.com/net/core).</span></span>
* <span data-ttu-id="1690a-112">Un abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="1690a-112">An Azure subscription.</span></span>
* <span data-ttu-id="1690a-113">Un espace de noms Azure Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="1690a-113">An Azure Event Hubs namespace.</span></span>
* <span data-ttu-id="1690a-114">Un compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="1690a-114">An Azure storage account.</span></span>

## <a name="create-an-event-hubs-namespace-and-an-event-hub"></a><span data-ttu-id="1690a-115">Création d’un espace de noms Event Hubs et d’un concentrateur d’événements</span><span class="sxs-lookup"><span data-stu-id="1690a-115">Create an Event Hubs namespace and an event hub</span></span>  

<span data-ttu-id="1690a-116">La première étape consiste à utiliser le [portail Azure](https://portal.azure.com) pour créer un espace de noms de type Event Hubs et obtenir les informations de gestion nécessaires à votre application pour communiquer avec le concentrateur d’événements.</span><span class="sxs-lookup"><span data-stu-id="1690a-116">The first step is to use the [Azure portal](https://portal.azure.com) to create a namespace for the Event Hubs type, and obtain the management credentials that your application needs to communicate with the event hub.</span></span> <span data-ttu-id="1690a-117">Pour créer un espace de noms et un concentrateur d’événements, suivez la procédure décrite dans [cet article](event-hubs-create.md), puis passez aux étapes suivantes.</span><span class="sxs-lookup"><span data-stu-id="1690a-117">To create a namespace and event hub, follow the procedure in [this article](event-hubs-create.md), and then proceed with the following steps.</span></span>  

## <a name="create-an-azure-storage-account"></a><span data-ttu-id="1690a-118">Création d'un compte de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="1690a-118">Create an Azure storage account</span></span>  

1. <span data-ttu-id="1690a-119">Connectez-vous au [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="1690a-119">Sign in to the [Azure portal](https://portal.azure.com).</span></span>  
2. <span data-ttu-id="1690a-120">Dans le panneau de navigation gauche du portail, cliquez sur **Nouveau**, puis sur **Données** et sur **Compte de stockage**.</span><span class="sxs-lookup"><span data-stu-id="1690a-120">In the left navigation pane of the portal, click **New**, click **Storage**, and then click **Storage Account**.</span></span>  
3. <span data-ttu-id="1690a-121">Renseignez les champs dans le panneau de compte de stockage, puis cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="1690a-121">Complete the fields in the storage account blade, and then click **Create**.</span></span>

    ![Créer un compte de stockage][1]

4. <span data-ttu-id="1690a-123">Après l’affichage du message **Déploiements réussis**, cliquez sur le nom du nouveau compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="1690a-123">After you see the **Deployments Succeeded** message, click the name of the new storage account.</span></span> <span data-ttu-id="1690a-124">Dans le panneau **Bases**, cliquez sur **Objets blob**.</span><span class="sxs-lookup"><span data-stu-id="1690a-124">In the **Essentials** blade, click **Blobs**.</span></span> <span data-ttu-id="1690a-125">Quand le panneau **Service Blob** s’ouvre, cliquez sur **+ Conteneur** en haut.</span><span class="sxs-lookup"><span data-stu-id="1690a-125">When the **Blob service** blade opens, click **+ Container** at the top.</span></span> <span data-ttu-id="1690a-126">Nommez le conteneur, puis fermez le panneau **Service Blob**.</span><span class="sxs-lookup"><span data-stu-id="1690a-126">Give the container a name, and then close the **Blob service** blade.</span></span>  
5. <span data-ttu-id="1690a-127">Cliquez sur **Clés d’accès** dans le panneau de gauche, puis copiez le nom du conteneur de stockage, le compte de stockage et la valeur de **key1**.</span><span class="sxs-lookup"><span data-stu-id="1690a-127">Click **Access keys** in the left blade and copy the name of the storage container, the storage account, and the value of **key1**.</span></span> <span data-ttu-id="1690a-128">Enregistrez ces valeurs dans le Bloc-notes ou un autre emplacement temporaire.</span><span class="sxs-lookup"><span data-stu-id="1690a-128">Save these values to Notepad or some other temporary location.</span></span>  

## <a name="create-a-console-application"></a><span data-ttu-id="1690a-129">Création d’une application console</span><span class="sxs-lookup"><span data-stu-id="1690a-129">Create a console application</span></span>

<span data-ttu-id="1690a-130">Démarrez Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1690a-130">Start Visual Studio.</span></span> <span data-ttu-id="1690a-131">Dans le menu **Fichier**, cliquez sur **Nouveau**, puis sur **Projet**.</span><span class="sxs-lookup"><span data-stu-id="1690a-131">From the **File** menu, click **New**, and then click **Project**.</span></span> <span data-ttu-id="1690a-132">Créez une application console .NET Core.</span><span class="sxs-lookup"><span data-stu-id="1690a-132">Create a .NET Core console application.</span></span>

![Nouveau projet][2]

## <a name="add-the-event-hubs-nuget-package"></a><span data-ttu-id="1690a-134">Ajout du package NuGet Event Hubs</span><span class="sxs-lookup"><span data-stu-id="1690a-134">Add the Event Hubs NuGet package</span></span>

<span data-ttu-id="1690a-135">Ajoutez les packages NuGet de bibliothèque standard .NET [`Microsoft.Azure.EventHubs`](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/) et [`Microsoft.Azure.EventHubs.Processor`](https://www.nuget.org/packages/Microsoft.Azure.EventHubs.Processor/) à votre projet en procédant comme suit :</span><span class="sxs-lookup"><span data-stu-id="1690a-135">Add the [`Microsoft.Azure.EventHubs`](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/) and [`Microsoft.Azure.EventHubs.Processor`](https://www.nuget.org/packages/Microsoft.Azure.EventHubs.Processor/) .NET Standard library NuGet packages to your project by following these steps:</span></span> 

1. <span data-ttu-id="1690a-136">Cliquez avec le bouton droit sur le projet créé et sélectionnez **Gérer les packages NuGet**.</span><span class="sxs-lookup"><span data-stu-id="1690a-136">Right-click the newly created project and select **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="1690a-137">Cliquez sur l’onglet **Parcourir**, puis recherchez « Microsoft.Azure.EventHubs » et sélectionnez le package **Microsoft.Azure.EventHubs**.</span><span class="sxs-lookup"><span data-stu-id="1690a-137">Click the **Browse** tab, then search for "Microsoft.Azure.EventHubs" and select the **Microsoft.Azure.EventHubs** package.</span></span> <span data-ttu-id="1690a-138">Cliquez sur **Installer** pour terminer l’installation, puis fermez cette boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="1690a-138">Click **Install** to complete the installation, then close this dialog box.</span></span>
3. <span data-ttu-id="1690a-139">Répétez les étapes 1 et 2 et installez le package **Microsoft.Azure.EventHubs.Processor**.</span><span class="sxs-lookup"><span data-stu-id="1690a-139">Repeat steps 1 and 2, and install the **Microsoft.Azure.EventHubs.Processor** package.</span></span>

## <a name="implement-the-ieventprocessor-interface"></a><span data-ttu-id="1690a-140">Implémentation de l’interface IEventProcessor</span><span class="sxs-lookup"><span data-stu-id="1690a-140">Implement the IEventProcessor interface</span></span>

1. <span data-ttu-id="1690a-141">Dans l’Explorateur de solutions, cliquez sur **Ajouter**, puis sur **Classe**.</span><span class="sxs-lookup"><span data-stu-id="1690a-141">In Solution Explorer, right-click the project, click **Add**, and then click **Class**.</span></span> <span data-ttu-id="1690a-142">Nommez la nouvelle classe **SimpleEventProcessor**.</span><span class="sxs-lookup"><span data-stu-id="1690a-142">Name the new class **SimpleEventProcessor**.</span></span>

2. <span data-ttu-id="1690a-143">Ouvrez le fichier SimpleEventProcessor.cs et ajoutez les instructions `using` suivantes au début du fichier.</span><span class="sxs-lookup"><span data-stu-id="1690a-143">Open the SimpleEventProcessor.cs file and add the following `using` statements to the top of the file.</span></span>

    ```csharp
    using Microsoft.Azure.EventHubs;
    using Microsoft.Azure.EventHubs.Processor;
    using System.Threading.Tasks;
    ```

3. <span data-ttu-id="1690a-144">Implémentez l’interface `IEventProcessor`.</span><span class="sxs-lookup"><span data-stu-id="1690a-144">Implement the `IEventProcessor` interface.</span></span> <span data-ttu-id="1690a-145">Remplacez tout le contenu de la classe `SimpleEventProcessor` par le code suivant :</span><span class="sxs-lookup"><span data-stu-id="1690a-145">Replace the entire contents of the `SimpleEventProcessor` class with the following code:</span></span>

    ```csharp
    public class SimpleEventProcessor : IEventProcessor
    {
        public Task CloseAsync(PartitionContext context, CloseReason reason)
        {
            Console.WriteLine($"Processor Shutting Down. Partition '{context.PartitionId}', Reason: '{reason}'.");
            return Task.CompletedTask;
        }

        public Task OpenAsync(PartitionContext context)
        {
            Console.WriteLine($"SimpleEventProcessor initialized. Partition: '{context.PartitionId}'");
            return Task.CompletedTask;
        }

        public Task ProcessErrorAsync(PartitionContext context, Exception error)
        {
            Console.WriteLine($"Error on Partition: {context.PartitionId}, Error: {error.Message}");
            return Task.CompletedTask;
        }

        public Task ProcessEventsAsync(PartitionContext context, IEnumerable<EventData> messages)
        {
            foreach (var eventData in messages)
            {
                var data = Encoding.UTF8.GetString(eventData.Body.Array, eventData.Body.Offset, eventData.Body.Count);
                Console.WriteLine($"Message received. Partition: '{context.PartitionId}', Data: '{data}'");
            }

            return context.CheckpointAsync();
        }
    }
    ```

## <a name="write-a-main-console-method-that-uses-the-simpleeventprocessor-class-to-receive-messages"></a><span data-ttu-id="1690a-146">Écrire une méthode de console qui utilise la classe SimpleEventProcessor pour recevoir des messages</span><span class="sxs-lookup"><span data-stu-id="1690a-146">Write a main console method that uses the SimpleEventProcessor class to receive messages</span></span>

1. <span data-ttu-id="1690a-147">Ajoutez les instructions `using` ci-après en haut du fichier Program.cs.</span><span class="sxs-lookup"><span data-stu-id="1690a-147">Add the following `using` statements to the top of the Program.cs file.</span></span>

    ```csharp
    using Microsoft.Azure.EventHubs;
    using Microsoft.Azure.EventHubs.Processor;
    using System.Threading.Tasks;
    ```

2. <span data-ttu-id="1690a-148">Ajoutez des constantes à la classe `Program` pour la chaîne de connexion du concentrateur d’événements, le nom du concentrateur d’événements, le nom du conteneur de compte de stockage, le nom du compte de stockage et la clé du compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="1690a-148">Add constants to the `Program` class for the event hub connection string, event hub name, storage account container name, storage account name, and storage account key.</span></span> <span data-ttu-id="1690a-149">Ajoutez le code suivant, en remplaçant les espaces réservés par les valeurs correspondantes.</span><span class="sxs-lookup"><span data-stu-id="1690a-149">Add the following code, replacing the placeholders with their corresponding values.</span></span>

    ```csharp
    private const string EhConnectionString = "{Event Hubs connection string}";
    private const string EhEntityPath = "{Event Hub path/name}";
    private const string StorageContainerName = "{Storage account container name}";
    private const string StorageAccountName = "{Storage account name}";
    private const string StorageAccountKey = "{Storage account key}";

    private static readonly string StorageConnectionString = string.Format("DefaultEndpointsProtocol=https;AccountName={0};AccountKey={1}", StorageAccountName, StorageAccountKey);
    ```   

3. <span data-ttu-id="1690a-150">Ajoutez une nouvelle méthode nommée `MainAsync` à la classe `Program`, comme suit :</span><span class="sxs-lookup"><span data-stu-id="1690a-150">Add a new method named `MainAsync` to the `Program` class, as follows:</span></span>

    ```csharp
    private static async Task MainAsync(string[] args)
    {
        Console.WriteLine("Registering EventProcessor...");

        var eventProcessorHost = new EventProcessorHost(
            EhEntityPath,
            PartitionReceiver.DefaultConsumerGroupName,
            EhConnectionString,
            StorageConnectionString,
            StorageContainerName);

        // Registers the Event Processor Host and starts receiving messages
        await eventProcessorHost.RegisterEventProcessorAsync<SimpleEventProcessor>();

        Console.WriteLine("Receiving. Press ENTER to stop worker.");
        Console.ReadLine();

        // Disposes of the Event Processor Host
        await eventProcessorHost.UnregisterEventProcessorAsync();
    }
    ```

3. <span data-ttu-id="1690a-151">Ajoutez la ligne de code suivante à la méthode `Main` :</span><span class="sxs-lookup"><span data-stu-id="1690a-151">Add the following line of code to the `Main` method:</span></span>

    ```csharp
    MainAsync(args).GetAwaiter().GetResult();
    ```

    <span data-ttu-id="1690a-152">Voici à quoi doit ressembler votre fichier Program.cs :</span><span class="sxs-lookup"><span data-stu-id="1690a-152">Here is what your Program.cs file should look like:</span></span>

    ```csharp
    namespace SampleEphReceiver
    {

        public class Program
        {
            private const string EhConnectionString = "{Event Hubs connection string}";
            private const string EhEntityPath = "{Event Hub path/name}";
            private const string StorageContainerName = "{Storage account container name}";
            private const string StorageAccountName = "{Storage account name}";
            private const string StorageAccountKey = "{Storage account key}";

            private static readonly string StorageConnectionString = string.Format("DefaultEndpointsProtocol=https;AccountName={0};AccountKey={1}", StorageAccountName, StorageAccountKey);

            public static void Main(string[] args)
            {
                MainAsync(args).GetAwaiter().GetResult();
            }

            private static async Task MainAsync(string[] args)
            {
                Console.WriteLine("Registering EventProcessor...");

                var eventProcessorHost = new EventProcessorHost(
                    EhEntityPath,
                    PartitionReceiver.DefaultConsumerGroupName,
                    EhConnectionString,
                    StorageConnectionString,
                    StorageContainerName);

                // Registers the Event Processor Host and starts receiving messages
                await eventProcessorHost.RegisterEventProcessorAsync<SimpleEventProcessor>();

                Console.WriteLine("Receiving. Press ENTER to stop worker.");
                Console.ReadLine();

                // Disposes of the Event Processor Host
                await eventProcessorHost.UnregisterEventProcessorAsync();
            }
        }
    }
    ```

4. <span data-ttu-id="1690a-153">Exécutez le programme et assurez-vous qu’il n’y a aucune erreur.</span><span class="sxs-lookup"><span data-stu-id="1690a-153">Run the program, and ensure that there are no errors.</span></span>

<span data-ttu-id="1690a-154">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="1690a-154">Congratulations!</span></span> <span data-ttu-id="1690a-155">Vous recevez maintenant les messages d’un concentrateur d’événements à l’aide de l’hôte du processeur d’événements.</span><span class="sxs-lookup"><span data-stu-id="1690a-155">You have now received messages from an event hub by using the Event Processor Host.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1690a-156">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1690a-156">Next steps</span></span>
<span data-ttu-id="1690a-157">Vous pouvez en apprendre plus sur Event Hubs en consultant les liens suivants :</span><span class="sxs-lookup"><span data-stu-id="1690a-157">You can learn more about Event Hubs by visiting the following links:</span></span>

* [<span data-ttu-id="1690a-158">Vue d’ensemble des hubs d’événements</span><span class="sxs-lookup"><span data-stu-id="1690a-158">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="1690a-159">Créer un concentrateur d’événements</span><span class="sxs-lookup"><span data-stu-id="1690a-159">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="1690a-160">FAQ sur les hubs d'événements</span><span class="sxs-lookup"><span data-stu-id="1690a-160">Event Hubs FAQ</span></span>](event-hubs-faq.md)

[1]: ./media/event-hubs-dotnet-standard-getstarted-receive-eph/event-hubs-python1.png
[2]: ./media/event-hubs-dotnet-standard-getstarted-receive-eph/netcore.png
