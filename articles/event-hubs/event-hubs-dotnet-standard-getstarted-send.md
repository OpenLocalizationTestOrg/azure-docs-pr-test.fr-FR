---
title: "aaaSend événements tooAzure concentrateurs d’événements à l’aide de .NET Standard | Documents Microsoft"
description: "Prise en main de l’envoi d’événements tooEvent concentrateurs dans .NET Standard"
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
ms.openlocfilehash: caa9747a8a72aa8e7aea1348a116f6e4b406460e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-sending-messages-tooazure-event-hubs-in-net-standard"></a><span data-ttu-id="36c8b-103">Commencer l’envoi de messages tooAzure concentrateurs d’événements dans .NET Standard</span><span class="sxs-lookup"><span data-stu-id="36c8b-103">Get started sending messages tooAzure Event Hubs in .NET Standard</span></span>

> [!NOTE]
> <span data-ttu-id="36c8b-104">Cet exemple est disponible sur [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender).</span><span class="sxs-lookup"><span data-stu-id="36c8b-104">This sample is available on [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender).</span></span>

<span data-ttu-id="36c8b-105">Ce didacticiel montre comment toowrite une application console .NET Core qui envoie un ensemble de messages tooan concentrateur d’événements.</span><span class="sxs-lookup"><span data-stu-id="36c8b-105">This tutorial shows how toowrite a .NET Core console application that sends a set of messages tooan event hub.</span></span> <span data-ttu-id="36c8b-106">Vous pouvez exécuter hello [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender) solution en tant que-remplacer hello `EhConnectionString` et `EhEntityPath` de chaînes avec vos valeurs de concentrateur d’événements.</span><span class="sxs-lookup"><span data-stu-id="36c8b-106">You can run hello [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender) solution as-is, replacing hello `EhConnectionString` and `EhEntityPath` strings with your event hub values.</span></span> <span data-ttu-id="36c8b-107">Vous pouvez également suivre hello étapes de ce didacticiel toocreate votre propre.</span><span class="sxs-lookup"><span data-stu-id="36c8b-107">Or you can follow hello steps in this tutorial toocreate your own.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="36c8b-108">Composants requis</span><span class="sxs-lookup"><span data-stu-id="36c8b-108">Prerequisites</span></span>

* <span data-ttu-id="36c8b-109">[Microsoft Visual Studio 2015 ou 2017](http://www.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="36c8b-109">[Microsoft Visual Studio 2015 or 2017](http://www.visualstudio.com).</span></span> <span data-ttu-id="36c8b-110">exemples de Hello dans ce didacticiel, utilisez Visual Studio 2017, mais Visual Studio 2015 est également pris en charge.</span><span class="sxs-lookup"><span data-stu-id="36c8b-110">hello examples in this tutorial use Visual Studio 2017, but Visual Studio 2015 is also supported.</span></span>
* <span data-ttu-id="36c8b-111">[Outils Visual Studio 2015 ou 2017 .NET Core](http://www.microsoft.com/net/core).</span><span class="sxs-lookup"><span data-stu-id="36c8b-111">[.NET Core Visual Studio 2015 or 2017 tools](http://www.microsoft.com/net/core).</span></span>
* <span data-ttu-id="36c8b-112">Un abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="36c8b-112">An Azure subscription.</span></span>
* <span data-ttu-id="36c8b-113">Un espace de noms de concentrateur d’événements.</span><span class="sxs-lookup"><span data-stu-id="36c8b-113">An event hub namespace.</span></span>

<span data-ttu-id="36c8b-114">concentrateur d’événements toosend messages tooan, nous allons utiliser Visual Studio toowrite une application console c#.</span><span class="sxs-lookup"><span data-stu-id="36c8b-114">toosend messages tooan event hub, we will use Visual Studio toowrite a C# console application.</span></span>

## <a name="create-an-event-hubs-namespace-and-an-event-hub"></a><span data-ttu-id="36c8b-115">Création d’un espace de noms Event Hubs et d’un concentrateur d’événements</span><span class="sxs-lookup"><span data-stu-id="36c8b-115">Create an Event Hubs namespace and an event hub</span></span>

<span data-ttu-id="36c8b-116">première étape de Hello est toouse hello [portail Azure](https://portal.azure.com) toocreate un espace de noms pour le type de concentrateur d’événements hello et obtenir des informations d’identification de gestion que votre application doit toocommunicate avec un concentrateur d’événements hello hello.</span><span class="sxs-lookup"><span data-stu-id="36c8b-116">hello first step is toouse hello [Azure portal](https://portal.azure.com) toocreate a namespace for hello event hub type, and obtain hello management credentials that your application needs toocommunicate with hello event hub.</span></span> <span data-ttu-id="36c8b-117">toocreate un espace de noms et d’un concentrateur d’événements, suivez la procédure hello dans [cet article](event-hubs-create.md), puis poursuivez hello comme suit.</span><span class="sxs-lookup"><span data-stu-id="36c8b-117">toocreate a namespace and an event hub, follow hello procedure in [this article](event-hubs-create.md), and then proceed with hello following steps.</span></span>

## <a name="create-a-console-application"></a><span data-ttu-id="36c8b-118">Création d’une application console</span><span class="sxs-lookup"><span data-stu-id="36c8b-118">Create a console application</span></span>

<span data-ttu-id="36c8b-119">Démarrez Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="36c8b-119">Start Visual Studio.</span></span> <span data-ttu-id="36c8b-120">À partir de hello **fichier** menu, cliquez sur **nouveau**, puis cliquez sur **projet**.</span><span class="sxs-lookup"><span data-stu-id="36c8b-120">From hello **File** menu, click **New**, and then click **Project**.</span></span> <span data-ttu-id="36c8b-121">Créez une application console .NET Core.</span><span class="sxs-lookup"><span data-stu-id="36c8b-121">Create a .NET Core console application.</span></span>

![Nouveau projet][1]

## <a name="add-hello-event-hubs-nuget-package"></a><span data-ttu-id="36c8b-123">Ajouter un package NuGet de concentrateurs d’événements de hello</span><span class="sxs-lookup"><span data-stu-id="36c8b-123">Add hello Event Hubs NuGet package</span></span>

<span data-ttu-id="36c8b-124">Ajouter hello [ `Microsoft.Azure.EventHubs` ](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/) .NET Standard bibliothèque NuGet package tooyour projet en procédant comme suit :</span><span class="sxs-lookup"><span data-stu-id="36c8b-124">Add hello [`Microsoft.Azure.EventHubs`](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/) .NET Standard library NuGet package tooyour project by following these steps:</span></span> 

1. <span data-ttu-id="36c8b-125">Avec le bouton droit de projet de hello nouvellement créé et sélectionnez **gérer les Packages NuGet**.</span><span class="sxs-lookup"><span data-stu-id="36c8b-125">Right-click hello newly created project and select **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="36c8b-126">Cliquez sur hello **Parcourir** tab, puis recherchez « Microsoft.Azure.EventHubs » et sélectionnez hello **Microsoft.Azure.EventHubs** package.</span><span class="sxs-lookup"><span data-stu-id="36c8b-126">Click hello **Browse** tab, then search for "Microsoft.Azure.EventHubs" and select hello **Microsoft.Azure.EventHubs** package.</span></span> <span data-ttu-id="36c8b-127">Cliquez sur **installer** toocomplete hello installation, puis fermez cette boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="36c8b-127">Click **Install** toocomplete hello installation, then close this dialog box.</span></span>

## <a name="write-some-code-toosend-messages-toohello-event-hub"></a><span data-ttu-id="36c8b-128">Écrire certaines concentrateur d’événements toohello messages code toosend</span><span class="sxs-lookup"><span data-stu-id="36c8b-128">Write some code toosend messages toohello event hub</span></span>

1. <span data-ttu-id="36c8b-129">Ajoutez hello suit `using` haut de toohello instructions du fichier Program.cs de hello.</span><span class="sxs-lookup"><span data-stu-id="36c8b-129">Add hello following `using` statements toohello top of hello Program.cs file.</span></span>

    ```csharp
    using Microsoft.Azure.EventHubs;
    using System.Text;
    using System.Threading.Tasks;
    ```

2. <span data-ttu-id="36c8b-130">Ajouter des constantes toohello `Program` classe hello concentrateurs d’événements connexion entité et la chaîne de chemin d’accès (nom du concentrateur d’événements).</span><span class="sxs-lookup"><span data-stu-id="36c8b-130">Add constants toohello `Program` class for hello Event Hubs connection string and entity path (individual event hub name).</span></span> <span data-ttu-id="36c8b-131">Remplacez les espaces réservés de hello entre crochets avec les valeurs appropriées hello qui ont été obtenus lors de la création du concentrateur d’événements hello.</span><span class="sxs-lookup"><span data-stu-id="36c8b-131">Replace hello placeholders in brackets with hello proper values that were obtained when creating hello event hub.</span></span>

    ```csharp
    private static EventHubClient eventHubClient;
    private const string EhConnectionString = "{Event Hubs connection string}";
    private const string EhEntityPath = "{Event Hub path/name}";
    ```

3. <span data-ttu-id="36c8b-132">Ajoutez une nouvelle méthode nommée `MainAsync` toohello `Program` de classe, comme suit :</span><span class="sxs-lookup"><span data-stu-id="36c8b-132">Add a new method named `MainAsync` toohello `Program` class, as follows:</span></span>

    ```csharp
    private static async Task MainAsync(string[] args)
    {
        // Creates an EventHubsConnectionStringBuilder object from hello connection string, and sets hello EntityPath.
        // Typically, hello connection string should have hello entity path in it, but for hello sake of this simple scenario
        // we are using hello connection string from hello namespace.
        var connectionStringBuilder = new EventHubsConnectionStringBuilder(EhConnectionString)
        {
            EntityPath = EhEntityPath
        };

        eventHubClient = EventHubClient.CreateFromConnectionString(connectionStringBuilder.ToString());

        await SendMessagesToEventHub(100);

        await eventHubClient.CloseAsync();

        Console.WriteLine("Press ENTER tooexit.");
        Console.ReadLine();
    }
    ```

4. <span data-ttu-id="36c8b-133">Ajoutez une nouvelle méthode nommée `SendMessagesToEventHub` toohello `Program` de classe, comme suit :</span><span class="sxs-lookup"><span data-stu-id="36c8b-133">Add a new method named `SendMessagesToEventHub` toohello `Program` class, as follows:</span></span>

    ```csharp
    // Creates an event hub client and sends 100 messages toohello event hub.
    private static async Task SendMessagesToEventHub(int numMessagesToSend)
    {
        for (var i = 0; i < numMessagesToSend; i++)
        {
            try
            {
                var message = $"Message {i}";
                Console.WriteLine($"Sending message: {message}");
                await eventHubClient.SendAsync(new EventData(Encoding.UTF8.GetBytes(message)));
            }
            catch (Exception exception)
            {
                Console.WriteLine($"{DateTime.Now} > Exception: {exception.Message}");
            }

            await Task.Delay(10);
        }

        Console.WriteLine($"{numMessagesToSend} messages sent.");
    }
    ```

5. <span data-ttu-id="36c8b-134">Ajouter hello suivant code toohello `Main` méthode Bonjour `Program` classe.</span><span class="sxs-lookup"><span data-stu-id="36c8b-134">Add hello following code toohello `Main` method in hello `Program` class.</span></span>

    ```csharp
    MainAsync(args).GetAwaiter().GetResult();
    ```

   <span data-ttu-id="36c8b-135">Voici à quoi doit ressembler votre fichier Program.cs.</span><span class="sxs-lookup"><span data-stu-id="36c8b-135">Here is what your Program.cs should look like.</span></span>

    ```csharp
    namespace SampleSender
    {
        using System;
        using System.Text;
        using System.Threading.Tasks;
        using Microsoft.Azure.EventHubs;

        public class Program
        {
            private static EventHubClient eventHubClient;
            private const string EhConnectionString = "{Event Hubs connection string}";
            private const string EhEntityPath = "{Event Hub path/name}";

            public static void Main(string[] args)
            {
                MainAsync(args).GetAwaiter().GetResult();
            }

            private static async Task MainAsync(string[] args)
            {
                // Creates an EventHubsConnectionStringBuilder object from hello connection string, and sets hello EntityPath.
                // Typically, hello connection string should have hello entity path in it, but for hello sake of this simple scenario
                // we are using hello connection string from hello namespace.
                var connectionStringBuilder = new EventHubsConnectionStringBuilder(EhConnectionString)
                {
                    EntityPath = EhEntityPath
                };

                eventHubClient = EventHubClient.CreateFromConnectionString(connectionStringBuilder.ToString());

                await SendMessagesToEventHub(100);

                await eventHubClient.CloseAsync();

                Console.WriteLine("Press ENTER tooexit.");
                Console.ReadLine();
            }

            // Creates an event hub client and sends 100 messages toohello event hub.
            private static async Task SendMessagesToEventHub(int numMessagesToSend)
            {
                for (var i = 0; i < numMessagesToSend; i++)
                {
                    try
                    {
                        var message = $"Message {i}";
                        Console.WriteLine($"Sending message: {message}");
                        await eventHubClient.SendAsync(new EventData(Encoding.UTF8.GetBytes(message)));
                    }
                    catch (Exception exception)
                    {
                        Console.WriteLine($"{DateTime.Now} > Exception: {exception.Message}");
                    }

                    await Task.Delay(10);
                }

                Console.WriteLine($"{numMessagesToSend} messages sent.");
            }
        }
    }
    ```

6. <span data-ttu-id="36c8b-136">Exécuter le programme de hello et vérifiez qu’il n’y a aucune erreur.</span><span class="sxs-lookup"><span data-stu-id="36c8b-136">Run hello program, and ensure that there are no errors.</span></span>

<span data-ttu-id="36c8b-137">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="36c8b-137">Congratulations!</span></span> <span data-ttu-id="36c8b-138">Vous avez maintenant envoyé concentrateur d’événements tooan messages.</span><span class="sxs-lookup"><span data-stu-id="36c8b-138">You have now sent messages tooan event hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="36c8b-139">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="36c8b-139">Next steps</span></span>
<span data-ttu-id="36c8b-140">Vous pouvez plus d’informations sur les concentrateurs d’événements en visitant hello suivant liens :</span><span class="sxs-lookup"><span data-stu-id="36c8b-140">You can learn more about Event Hubs by visiting hello following links:</span></span>

* [<span data-ttu-id="36c8b-141">Recevoir des événements d’Event Hubs</span><span class="sxs-lookup"><span data-stu-id="36c8b-141">Receive events from Event Hubs</span></span>](event-hubs-dotnet-standard-getstarted-receive-eph.md)
* [<span data-ttu-id="36c8b-142">Vue d’ensemble des hubs d’événements</span><span class="sxs-lookup"><span data-stu-id="36c8b-142">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="36c8b-143">Créer un concentrateur d’événements</span><span class="sxs-lookup"><span data-stu-id="36c8b-143">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="36c8b-144">FAQ sur les hubs d'événements</span><span class="sxs-lookup"><span data-stu-id="36c8b-144">Event Hubs FAQ</span></span>](event-hubs-faq.md)

[1]: ./media/event-hubs-dotnet-standard-getstarted-send/netcore.png
