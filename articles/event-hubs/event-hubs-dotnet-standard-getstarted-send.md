---
title: "Envoyer des événements vers Azure Event Hubs avec .NET Standard | Microsoft Docs"
description: "Prise en main de l’envoi d’événements vers Event Hubs dans .NET Standard"
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
ms.openlocfilehash: 8af9d70965c1c9ad8c49b7d2bb04244fc207058d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-sending-messages-to-azure-event-hubs-in-net-standard"></a><span data-ttu-id="f0f09-103">Bien démarrer avec l’envoi de messages vers Azure Event Hubs dans .NET Standard</span><span class="sxs-lookup"><span data-stu-id="f0f09-103">Get started sending messages to Azure Event Hubs in .NET Standard</span></span>

> [!NOTE]
> <span data-ttu-id="f0f09-104">Cet exemple est disponible sur [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender).</span><span class="sxs-lookup"><span data-stu-id="f0f09-104">This sample is available on [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender).</span></span>

<span data-ttu-id="f0f09-105">Ce didacticiel montre comment écrire une application console .NET Core qui envoie un jeu de messages à un concentrateur d’événements.</span><span class="sxs-lookup"><span data-stu-id="f0f09-105">This tutorial shows how to write a .NET Core console application that sends a set of messages to an event hub.</span></span> <span data-ttu-id="f0f09-106">Vous pouvez exécuter la solution [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender), en remplaçant les chaînes `EhConnectionString` et `EhEntityPath` par vos valeurs de concentrateur d’événements.</span><span class="sxs-lookup"><span data-stu-id="f0f09-106">You can run the [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender) solution as-is, replacing the `EhConnectionString` and `EhEntityPath` strings with your event hub values.</span></span> <span data-ttu-id="f0f09-107">Ou vous pouvez suivre les étapes de ce didacticiel pour créer les vôtres.</span><span class="sxs-lookup"><span data-stu-id="f0f09-107">Or you can follow the steps in this tutorial to create your own.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f0f09-108">Composants requis</span><span class="sxs-lookup"><span data-stu-id="f0f09-108">Prerequisites</span></span>

* <span data-ttu-id="f0f09-109">[Microsoft Visual Studio 2015 ou 2017](http://www.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="f0f09-109">[Microsoft Visual Studio 2015 or 2017](http://www.visualstudio.com).</span></span> <span data-ttu-id="f0f09-110">Les exemples de ce didacticiel utilisent Visual Studio 2017, mais Visual Studio 2015 est également pris en charge.</span><span class="sxs-lookup"><span data-stu-id="f0f09-110">The examples in this tutorial use Visual Studio 2017, but Visual Studio 2015 is also supported.</span></span>
* <span data-ttu-id="f0f09-111">[Outils Visual Studio 2015 ou 2017 .NET Core](http://www.microsoft.com/net/core).</span><span class="sxs-lookup"><span data-stu-id="f0f09-111">[.NET Core Visual Studio 2015 or 2017 tools](http://www.microsoft.com/net/core).</span></span>
* <span data-ttu-id="f0f09-112">Un abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="f0f09-112">An Azure subscription.</span></span>
* <span data-ttu-id="f0f09-113">Un espace de noms de concentrateur d’événements.</span><span class="sxs-lookup"><span data-stu-id="f0f09-113">An event hub namespace.</span></span>

<span data-ttu-id="f0f09-114">Pour envoyer des messages à un concentrateur d’événements, nous allons utiliser Visual Studio pour écrire une application console C#.</span><span class="sxs-lookup"><span data-stu-id="f0f09-114">To send messages to an event hub, we will use Visual Studio to write a C# console application.</span></span>

## <a name="create-an-event-hubs-namespace-and-an-event-hub"></a><span data-ttu-id="f0f09-115">Création d’un espace de noms Event Hubs et d’un concentrateur d’événements</span><span class="sxs-lookup"><span data-stu-id="f0f09-115">Create an Event Hubs namespace and an event hub</span></span>

<span data-ttu-id="f0f09-116">La première étape consiste à utiliser le [portail Azure](https://portal.azure.com) pour créer un espace de noms de type concentrateur d’événements et obtenir les informations de gestion nécessaires à votre application pour communiquer avec le concentrateur d’événements.</span><span class="sxs-lookup"><span data-stu-id="f0f09-116">The first step is to use the [Azure portal](https://portal.azure.com) to create a namespace for the event hub type, and obtain the management credentials that your application needs to communicate with the event hub.</span></span> <span data-ttu-id="f0f09-117">Pour créer un espace de noms et un concentrateur d’événements, suivez la procédure décrite dans [cet article](event-hubs-create.md), puis passez aux étapes suivantes.</span><span class="sxs-lookup"><span data-stu-id="f0f09-117">To create a namespace and an event hub, follow the procedure in [this article](event-hubs-create.md), and then proceed with the following steps.</span></span>

## <a name="create-a-console-application"></a><span data-ttu-id="f0f09-118">Création d’une application console</span><span class="sxs-lookup"><span data-stu-id="f0f09-118">Create a console application</span></span>

<span data-ttu-id="f0f09-119">Démarrez Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f0f09-119">Start Visual Studio.</span></span> <span data-ttu-id="f0f09-120">Dans le menu **Fichier**, cliquez sur **Nouveau**, puis sur **Projet**.</span><span class="sxs-lookup"><span data-stu-id="f0f09-120">From the **File** menu, click **New**, and then click **Project**.</span></span> <span data-ttu-id="f0f09-121">Créez une application console .NET Core.</span><span class="sxs-lookup"><span data-stu-id="f0f09-121">Create a .NET Core console application.</span></span>

![Nouveau projet][1]

## <a name="add-the-event-hubs-nuget-package"></a><span data-ttu-id="f0f09-123">Ajout du package NuGet Event Hubs</span><span class="sxs-lookup"><span data-stu-id="f0f09-123">Add the Event Hubs NuGet package</span></span>

<span data-ttu-id="f0f09-124">Ajoutez le package NuGet de bibliothèque standard .NET [`Microsoft.Azure.EventHubs`](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/) à votre projet en procédant comme suit :</span><span class="sxs-lookup"><span data-stu-id="f0f09-124">Add the [`Microsoft.Azure.EventHubs`](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/) .NET Standard library NuGet package to your project by following these steps:</span></span> 

1. <span data-ttu-id="f0f09-125">Cliquez avec le bouton droit sur le projet créé et sélectionnez **Gérer les packages NuGet**.</span><span class="sxs-lookup"><span data-stu-id="f0f09-125">Right-click the newly created project and select **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="f0f09-126">Cliquez sur l’onglet **Parcourir**, puis recherchez « Microsoft.Azure.EventHubs » et sélectionnez le package **Microsoft.Azure.EventHubs**.</span><span class="sxs-lookup"><span data-stu-id="f0f09-126">Click the **Browse** tab, then search for "Microsoft.Azure.EventHubs" and select the **Microsoft.Azure.EventHubs** package.</span></span> <span data-ttu-id="f0f09-127">Cliquez sur **Installer** pour terminer l’installation, puis fermez cette boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="f0f09-127">Click **Install** to complete the installation, then close this dialog box.</span></span>

## <a name="write-some-code-to-send-messages-to-the-event-hub"></a><span data-ttu-id="f0f09-128">Écriture de code pour envoyer des messages à un concentrateur d’événements</span><span class="sxs-lookup"><span data-stu-id="f0f09-128">Write some code to send messages to the event hub</span></span>

1. <span data-ttu-id="f0f09-129">Ajoutez les instructions `using` ci-après en haut du fichier Program.cs.</span><span class="sxs-lookup"><span data-stu-id="f0f09-129">Add the following `using` statements to the top of the Program.cs file.</span></span>

    ```csharp
    using Microsoft.Azure.EventHubs;
    using System.Text;
    using System.Threading.Tasks;
    ```

2. <span data-ttu-id="f0f09-130">Ajoutez des constantes à la classe `Program` pour le chemin de l’entité et la chaîne de connexion Event Hubs (nom du concentrateur d’événements individuel).</span><span class="sxs-lookup"><span data-stu-id="f0f09-130">Add constants to the `Program` class for the Event Hubs connection string and entity path (individual event hub name).</span></span> <span data-ttu-id="f0f09-131">Remplacez les espaces réservés entre crochets par les valeurs appropriées obtenues lors de la création du concentrateur d’événements.</span><span class="sxs-lookup"><span data-stu-id="f0f09-131">Replace the placeholders in brackets with the proper values that were obtained when creating the event hub.</span></span>

    ```csharp
    private static EventHubClient eventHubClient;
    private const string EhConnectionString = "{Event Hubs connection string}";
    private const string EhEntityPath = "{Event Hub path/name}";
    ```

3. <span data-ttu-id="f0f09-132">Ajoutez une nouvelle méthode nommée `MainAsync` à la classe `Program`, comme suit :</span><span class="sxs-lookup"><span data-stu-id="f0f09-132">Add a new method named `MainAsync` to the `Program` class, as follows:</span></span>

    ```csharp
    private static async Task MainAsync(string[] args)
    {
        // Creates an EventHubsConnectionStringBuilder object from the connection string, and sets the EntityPath.
        // Typically, the connection string should have the entity path in it, but for the sake of this simple scenario
        // we are using the connection string from the namespace.
        var connectionStringBuilder = new EventHubsConnectionStringBuilder(EhConnectionString)
        {
            EntityPath = EhEntityPath
        };

        eventHubClient = EventHubClient.CreateFromConnectionString(connectionStringBuilder.ToString());

        await SendMessagesToEventHub(100);

        await eventHubClient.CloseAsync();

        Console.WriteLine("Press ENTER to exit.");
        Console.ReadLine();
    }
    ```

4. <span data-ttu-id="f0f09-133">Ajoutez une nouvelle méthode nommée `SendMessagesToEventHub` à la classe `Program`, comme suit :</span><span class="sxs-lookup"><span data-stu-id="f0f09-133">Add a new method named `SendMessagesToEventHub` to the `Program` class, as follows:</span></span>

    ```csharp
    // Creates an event hub client and sends 100 messages to the event hub.
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

5. <span data-ttu-id="f0f09-134">Ajoutez le code suivant à la méthode `Main` dans la classe `Program`.</span><span class="sxs-lookup"><span data-stu-id="f0f09-134">Add the following code to the `Main` method in the `Program` class.</span></span>

    ```csharp
    MainAsync(args).GetAwaiter().GetResult();
    ```

   <span data-ttu-id="f0f09-135">Voici à quoi doit ressembler votre fichier Program.cs.</span><span class="sxs-lookup"><span data-stu-id="f0f09-135">Here is what your Program.cs should look like.</span></span>

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
                // Creates an EventHubsConnectionStringBuilder object from the connection string, and sets the EntityPath.
                // Typically, the connection string should have the entity path in it, but for the sake of this simple scenario
                // we are using the connection string from the namespace.
                var connectionStringBuilder = new EventHubsConnectionStringBuilder(EhConnectionString)
                {
                    EntityPath = EhEntityPath
                };

                eventHubClient = EventHubClient.CreateFromConnectionString(connectionStringBuilder.ToString());

                await SendMessagesToEventHub(100);

                await eventHubClient.CloseAsync();

                Console.WriteLine("Press ENTER to exit.");
                Console.ReadLine();
            }

            // Creates an event hub client and sends 100 messages to the event hub.
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

6. <span data-ttu-id="f0f09-136">Exécutez le programme et assurez-vous qu’il n’y a aucune erreur.</span><span class="sxs-lookup"><span data-stu-id="f0f09-136">Run the program, and ensure that there are no errors.</span></span>

<span data-ttu-id="f0f09-137">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="f0f09-137">Congratulations!</span></span> <span data-ttu-id="f0f09-138">Vous venez d’envoyer des messages à un concentrateur d’événements.</span><span class="sxs-lookup"><span data-stu-id="f0f09-138">You have now sent messages to an event hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f0f09-139">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f0f09-139">Next steps</span></span>
<span data-ttu-id="f0f09-140">Vous pouvez en apprendre plus sur Event Hubs en consultant les liens suivants :</span><span class="sxs-lookup"><span data-stu-id="f0f09-140">You can learn more about Event Hubs by visiting the following links:</span></span>

* [<span data-ttu-id="f0f09-141">Recevoir des événements d’Event Hubs</span><span class="sxs-lookup"><span data-stu-id="f0f09-141">Receive events from Event Hubs</span></span>](event-hubs-dotnet-standard-getstarted-receive-eph.md)
* [<span data-ttu-id="f0f09-142">Vue d’ensemble des hubs d’événements</span><span class="sxs-lookup"><span data-stu-id="f0f09-142">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="f0f09-143">Créer un concentrateur d’événements</span><span class="sxs-lookup"><span data-stu-id="f0f09-143">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="f0f09-144">FAQ sur les hubs d'événements</span><span class="sxs-lookup"><span data-stu-id="f0f09-144">Event Hubs FAQ</span></span>](event-hubs-faq.md)

[1]: ./media/event-hubs-dotnet-standard-getstarted-send/netcore.png
