---
title: "événements d’aaaReceive de concentrateurs d’événements Azure à l’aide de .NET Standard | Documents Microsoft"
description: "Commencer à recevoir des messages avec hello EventProcessorHost dans .NET Standard"
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
ms.openlocfilehash: c3983f2668ac8f65522e44a1609dfd2eed31b7d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-receiving-messages-with-hello-event-processor-host-in-net-standard"></a><span data-ttu-id="50e4a-103">Commencer à recevoir des messages avec hello processeur d’événements hôte dans .NET Standard</span><span class="sxs-lookup"><span data-stu-id="50e4a-103">Get started receiving messages with hello Event Processor Host in .NET Standard</span></span>

> [!NOTE]
> <span data-ttu-id="50e4a-104">Cet exemple est disponible sur [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver).</span><span class="sxs-lookup"><span data-stu-id="50e4a-104">This sample is available on [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver).</span></span>

<span data-ttu-id="50e4a-105">Ce didacticiel montre comment toowrite un .NET Core console application qui reçoit des messages à partir d’un concentrateur d’événements à l’aide de **EventProcessorHost**.</span><span class="sxs-lookup"><span data-stu-id="50e4a-105">This tutorial shows how toowrite a .NET Core console application that receives messages from an event hub by using **EventProcessorHost**.</span></span> <span data-ttu-id="50e4a-106">Vous pouvez exécuter hello [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver) solution en tant que-, remplace les chaînes hello avec vos valeurs de compte événement concentrateur et de stockage.</span><span class="sxs-lookup"><span data-stu-id="50e4a-106">You can run hello [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver) solution as-is, replacing hello strings with your event hub and storage account values.</span></span> <span data-ttu-id="50e4a-107">Vous pouvez également suivre hello étapes de ce didacticiel toocreate votre propre.</span><span class="sxs-lookup"><span data-stu-id="50e4a-107">Or you can follow hello steps in this tutorial toocreate your own.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="50e4a-108">Composants requis</span><span class="sxs-lookup"><span data-stu-id="50e4a-108">Prerequisites</span></span>

* <span data-ttu-id="50e4a-109">[Microsoft Visual Studio 2015 ou 2017](http://www.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="50e4a-109">[Microsoft Visual Studio 2015 or 2017](http://www.visualstudio.com).</span></span> <span data-ttu-id="50e4a-110">exemples de Hello dans ce didacticiel, utilisez Visual Studio 2017, mais Visual Studio 2015 est également pris en charge.</span><span class="sxs-lookup"><span data-stu-id="50e4a-110">hello examples in this tutorial use Visual Studio 2017, but Visual Studio 2015 is also supported.</span></span>
* <span data-ttu-id="50e4a-111">[Outils Visual Studio 2015 ou 2017 .NET Core](http://www.microsoft.com/net/core).</span><span class="sxs-lookup"><span data-stu-id="50e4a-111">[.NET Core Visual Studio 2015 or 2017 tools](http://www.microsoft.com/net/core).</span></span>
* <span data-ttu-id="50e4a-112">Un abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="50e4a-112">An Azure subscription.</span></span>
* <span data-ttu-id="50e4a-113">Un espace de noms Azure Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="50e4a-113">An Azure Event Hubs namespace.</span></span>
* <span data-ttu-id="50e4a-114">Un compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="50e4a-114">An Azure storage account.</span></span>

## <a name="create-an-event-hubs-namespace-and-an-event-hub"></a><span data-ttu-id="50e4a-115">Création d’un espace de noms Event Hubs et d’un concentrateur d’événements</span><span class="sxs-lookup"><span data-stu-id="50e4a-115">Create an Event Hubs namespace and an event hub</span></span>  

<span data-ttu-id="50e4a-116">première étape de Hello est toouse hello [portail Azure](https://portal.azure.com) toocreate un espace de noms pour hello concentrateurs d’événements de type et obtenir des informations d’identification de gestion que votre application doit toocommunicate avec un concentrateur d’événements hello hello.</span><span class="sxs-lookup"><span data-stu-id="50e4a-116">hello first step is toouse hello [Azure portal](https://portal.azure.com) toocreate a namespace for hello Event Hubs type, and obtain hello management credentials that your application needs toocommunicate with hello event hub.</span></span> <span data-ttu-id="50e4a-117">toocreate un espace de noms et le concentrateur d’événements, suivez la procédure hello dans [cet article](event-hubs-create.md), puis poursuivez hello comme suit.</span><span class="sxs-lookup"><span data-stu-id="50e4a-117">toocreate a namespace and event hub, follow hello procedure in [this article](event-hubs-create.md), and then proceed with hello following steps.</span></span>  

## <a name="create-an-azure-storage-account"></a><span data-ttu-id="50e4a-118">Création d'un compte de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="50e4a-118">Create an Azure storage account</span></span>  

1. <span data-ttu-id="50e4a-119">Connectez-vous à toohello [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="50e4a-119">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>  
2. <span data-ttu-id="50e4a-120">Dans le volet de navigation gauche hello du portail de hello, cliquez sur **nouveau**, cliquez sur **stockage**, puis cliquez sur **compte de stockage**.</span><span class="sxs-lookup"><span data-stu-id="50e4a-120">In hello left navigation pane of hello portal, click **New**, click **Storage**, and then click **Storage Account**.</span></span>  
3. <span data-ttu-id="50e4a-121">Renseignez les champs hello dans le panneau de compte de stockage hello, puis cliquez sur **créer**.</span><span class="sxs-lookup"><span data-stu-id="50e4a-121">Complete hello fields in hello storage account blade, and then click **Create**.</span></span>

    ![Créer un compte de stockage][1]

4. <span data-ttu-id="50e4a-123">Une fois que vous consultez hello **a réussi des déploiements** , cliquez sur le nom de hello du nouveau compte de stockage hello.</span><span class="sxs-lookup"><span data-stu-id="50e4a-123">After you see hello **Deployments Succeeded** message, click hello name of hello new storage account.</span></span> <span data-ttu-id="50e4a-124">Bonjour **Essentials** panneau, cliquez sur **BLOB**.</span><span class="sxs-lookup"><span data-stu-id="50e4a-124">In hello **Essentials** blade, click **Blobs**.</span></span> <span data-ttu-id="50e4a-125">Hello lorsque **service Blob** panneau s’ouvre, cliquez sur **+ conteneur** haut hello.</span><span class="sxs-lookup"><span data-stu-id="50e4a-125">When hello **Blob service** blade opens, click **+ Container** at hello top.</span></span> <span data-ttu-id="50e4a-126">Donnez un nom à conteneur de hello et fermez hello **service Blob** panneau.</span><span class="sxs-lookup"><span data-stu-id="50e4a-126">Give hello container a name, and then close hello **Blob service** blade.</span></span>  
5. <span data-ttu-id="50e4a-127">Cliquez sur **clés d’accès** dans hello gauche lame et copie hello le nom du conteneur de stockage hello et valeur hello du compte de stockage hello **key1**.</span><span class="sxs-lookup"><span data-stu-id="50e4a-127">Click **Access keys** in hello left blade and copy hello name of hello storage container, hello storage account, and hello value of **key1**.</span></span> <span data-ttu-id="50e4a-128">Enregistrez ces tooNotepad de valeurs ou un autre emplacement temporaire.</span><span class="sxs-lookup"><span data-stu-id="50e4a-128">Save these values tooNotepad or some other temporary location.</span></span>  

## <a name="create-a-console-application"></a><span data-ttu-id="50e4a-129">Création d’une application console</span><span class="sxs-lookup"><span data-stu-id="50e4a-129">Create a console application</span></span>

<span data-ttu-id="50e4a-130">Démarrez Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="50e4a-130">Start Visual Studio.</span></span> <span data-ttu-id="50e4a-131">À partir de hello **fichier** menu, cliquez sur **nouveau**, puis cliquez sur **projet**.</span><span class="sxs-lookup"><span data-stu-id="50e4a-131">From hello **File** menu, click **New**, and then click **Project**.</span></span> <span data-ttu-id="50e4a-132">Créez une application console .NET Core.</span><span class="sxs-lookup"><span data-stu-id="50e4a-132">Create a .NET Core console application.</span></span>

![Nouveau projet][2]

## <a name="add-hello-event-hubs-nuget-package"></a><span data-ttu-id="50e4a-134">Ajouter un package NuGet de concentrateurs d’événements de hello</span><span class="sxs-lookup"><span data-stu-id="50e4a-134">Add hello Event Hubs NuGet package</span></span>

<span data-ttu-id="50e4a-135">Ajouter hello [ `Microsoft.Azure.EventHubs` ](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/) et [ `Microsoft.Azure.EventHubs.Processor` ](https://www.nuget.org/packages/Microsoft.Azure.EventHubs.Processor/) .NET Standard NuGet packages tooyour projet de bibliothèque d’en procédant comme suit :</span><span class="sxs-lookup"><span data-stu-id="50e4a-135">Add hello [`Microsoft.Azure.EventHubs`](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/) and [`Microsoft.Azure.EventHubs.Processor`](https://www.nuget.org/packages/Microsoft.Azure.EventHubs.Processor/) .NET Standard library NuGet packages tooyour project by following these steps:</span></span> 

1. <span data-ttu-id="50e4a-136">Avec le bouton droit de projet de hello nouvellement créé et sélectionnez **gérer les Packages NuGet**.</span><span class="sxs-lookup"><span data-stu-id="50e4a-136">Right-click hello newly created project and select **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="50e4a-137">Cliquez sur hello **Parcourir** tab, puis recherchez « Microsoft.Azure.EventHubs » et sélectionnez hello **Microsoft.Azure.EventHubs** package.</span><span class="sxs-lookup"><span data-stu-id="50e4a-137">Click hello **Browse** tab, then search for "Microsoft.Azure.EventHubs" and select hello **Microsoft.Azure.EventHubs** package.</span></span> <span data-ttu-id="50e4a-138">Cliquez sur **installer** toocomplete hello installation, puis fermez cette boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="50e4a-138">Click **Install** toocomplete hello installation, then close this dialog box.</span></span>
3. <span data-ttu-id="50e4a-139">Répétez les étapes 1 et 2 et installer hello **Microsoft.Azure.EventHubs.Processor** package.</span><span class="sxs-lookup"><span data-stu-id="50e4a-139">Repeat steps 1 and 2, and install hello **Microsoft.Azure.EventHubs.Processor** package.</span></span>

## <a name="implement-hello-ieventprocessor-interface"></a><span data-ttu-id="50e4a-140">Implémenter l’interface IEventProcessor hello</span><span class="sxs-lookup"><span data-stu-id="50e4a-140">Implement hello IEventProcessor interface</span></span>

1. <span data-ttu-id="50e4a-141">Dans l’Explorateur de solutions, projets de hello avec le bouton droit, cliquez sur **ajouter**, puis cliquez sur **classe**.</span><span class="sxs-lookup"><span data-stu-id="50e4a-141">In Solution Explorer, right-click hello project, click **Add**, and then click **Class**.</span></span> <span data-ttu-id="50e4a-142">Nommez la nouvelle classe de hello **SimpleEventProcessor**.</span><span class="sxs-lookup"><span data-stu-id="50e4a-142">Name hello new class **SimpleEventProcessor**.</span></span>

2. <span data-ttu-id="50e4a-143">Ouvrez le fichier de SimpleEventProcessor.cs hello et ajoutez hello suit `using` haut de toohello instructions du fichier de hello.</span><span class="sxs-lookup"><span data-stu-id="50e4a-143">Open hello SimpleEventProcessor.cs file and add hello following `using` statements toohello top of hello file.</span></span>

    ```csharp
    using Microsoft.Azure.EventHubs;
    using Microsoft.Azure.EventHubs.Processor;
    using System.Threading.Tasks;
    ```

3. <span data-ttu-id="50e4a-144">Hello d’implémenter `IEventProcessor` interface.</span><span class="sxs-lookup"><span data-stu-id="50e4a-144">Implement hello `IEventProcessor` interface.</span></span> <span data-ttu-id="50e4a-145">Remplacez hello tout contenu de hello `SimpleEventProcessor` classe avec hello suivant de code :</span><span class="sxs-lookup"><span data-stu-id="50e4a-145">Replace hello entire contents of hello `SimpleEventProcessor` class with hello following code:</span></span>

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

## <a name="write-a-main-console-method-that-uses-hello-simpleeventprocessor-class-tooreceive-messages"></a><span data-ttu-id="50e4a-146">Écrivez une méthode de console principal qui utilise les messages de salutation SimpleEventProcessor classe tooreceive</span><span class="sxs-lookup"><span data-stu-id="50e4a-146">Write a main console method that uses hello SimpleEventProcessor class tooreceive messages</span></span>

1. <span data-ttu-id="50e4a-147">Ajoutez hello suit `using` haut de toohello instructions du fichier Program.cs de hello.</span><span class="sxs-lookup"><span data-stu-id="50e4a-147">Add hello following `using` statements toohello top of hello Program.cs file.</span></span>

    ```csharp
    using Microsoft.Azure.EventHubs;
    using Microsoft.Azure.EventHubs.Processor;
    using System.Threading.Tasks;
    ```

2. <span data-ttu-id="50e4a-148">Ajouter des constantes toohello `Program` classe pour la chaîne de connexion du concentrateur hello événement, nom de hub d’événements, nom de conteneur de compte de stockage, nom de compte de stockage et clé de compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="50e4a-148">Add constants toohello `Program` class for hello event hub connection string, event hub name, storage account container name, storage account name, and storage account key.</span></span> <span data-ttu-id="50e4a-149">Ajoutez hello suivant de code, le remplacement des espaces réservés de hello avec leurs valeurs correspondantes.</span><span class="sxs-lookup"><span data-stu-id="50e4a-149">Add hello following code, replacing hello placeholders with their corresponding values.</span></span>

    ```csharp
    private const string EhConnectionString = "{Event Hubs connection string}";
    private const string EhEntityPath = "{Event Hub path/name}";
    private const string StorageContainerName = "{Storage account container name}";
    private const string StorageAccountName = "{Storage account name}";
    private const string StorageAccountKey = "{Storage account key}";

    private static readonly string StorageConnectionString = string.Format("DefaultEndpointsProtocol=https;AccountName={0};AccountKey={1}", StorageAccountName, StorageAccountKey);
    ```   

3. <span data-ttu-id="50e4a-150">Ajoutez une nouvelle méthode nommée `MainAsync` toohello `Program` de classe, comme suit :</span><span class="sxs-lookup"><span data-stu-id="50e4a-150">Add a new method named `MainAsync` toohello `Program` class, as follows:</span></span>

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

        // Registers hello Event Processor Host and starts receiving messages
        await eventProcessorHost.RegisterEventProcessorAsync<SimpleEventProcessor>();

        Console.WriteLine("Receiving. Press ENTER toostop worker.");
        Console.ReadLine();

        // Disposes of hello Event Processor Host
        await eventProcessorHost.UnregisterEventProcessorAsync();
    }
    ```

3. <span data-ttu-id="50e4a-151">Ajouter hello suivant la ligne de code toohello `Main` méthode :</span><span class="sxs-lookup"><span data-stu-id="50e4a-151">Add hello following line of code toohello `Main` method:</span></span>

    ```csharp
    MainAsync(args).GetAwaiter().GetResult();
    ```

    <span data-ttu-id="50e4a-152">Voici à quoi doit ressembler votre fichier Program.cs :</span><span class="sxs-lookup"><span data-stu-id="50e4a-152">Here is what your Program.cs file should look like:</span></span>

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

                // Registers hello Event Processor Host and starts receiving messages
                await eventProcessorHost.RegisterEventProcessorAsync<SimpleEventProcessor>();

                Console.WriteLine("Receiving. Press ENTER toostop worker.");
                Console.ReadLine();

                // Disposes of hello Event Processor Host
                await eventProcessorHost.UnregisterEventProcessorAsync();
            }
        }
    }
    ```

4. <span data-ttu-id="50e4a-153">Exécuter le programme de hello et vérifiez qu’il n’y a aucune erreur.</span><span class="sxs-lookup"><span data-stu-id="50e4a-153">Run hello program, and ensure that there are no errors.</span></span>

<span data-ttu-id="50e4a-154">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="50e4a-154">Congratulations!</span></span> <span data-ttu-id="50e4a-155">Vous avez désormais reçu des messages à partir d’un concentrateur d’événements à l’aide de hello processeur d’événements hôte.</span><span class="sxs-lookup"><span data-stu-id="50e4a-155">You have now received messages from an event hub by using hello Event Processor Host.</span></span>

## <a name="next-steps"></a><span data-ttu-id="50e4a-156">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="50e4a-156">Next steps</span></span>
<span data-ttu-id="50e4a-157">Vous pouvez plus d’informations sur les concentrateurs d’événements en visitant hello suivant liens :</span><span class="sxs-lookup"><span data-stu-id="50e4a-157">You can learn more about Event Hubs by visiting hello following links:</span></span>

* [<span data-ttu-id="50e4a-158">Vue d’ensemble des hubs d’événements</span><span class="sxs-lookup"><span data-stu-id="50e4a-158">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="50e4a-159">Créer un concentrateur d’événements</span><span class="sxs-lookup"><span data-stu-id="50e4a-159">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="50e4a-160">FAQ sur les hubs d'événements</span><span class="sxs-lookup"><span data-stu-id="50e4a-160">Event Hubs FAQ</span></span>](event-hubs-faq.md)

[1]: ./media/event-hubs-dotnet-standard-getstarted-receive-eph/event-hubs-python1.png
[2]: ./media/event-hubs-dotnet-standard-getstarted-receive-eph/netcore.png
