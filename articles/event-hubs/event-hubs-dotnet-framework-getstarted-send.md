---
title: "Envoyer des événements vers les hubs d’événements Azure avec .NET Framework | Microsoft Docs"
description: "Prise en main de l’envoi d’événements vers les hubs d’événements avec .NET Framework"
services: event-hubs
documentationcenter: 
author: sethmanheim
manager: timlt
editor: 
ms.assetid: c4974bd3-2a79-48a1-aa3b-8ee2d6655b28
ms.service: event-hubs
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/12/2017
ms.author: sethm
ms.openlocfilehash: 4eb0e7bcc14722010121c2a5945509d6ed736f4f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="send-events-to-azure-event-hubs-using-the-net-framework"></a><span data-ttu-id="476ec-103">Envoyer des événements vers les hubs d’événements Azure avec .NET Framework</span><span class="sxs-lookup"><span data-stu-id="476ec-103">Send events to Azure Event Hubs using the .NET Framework</span></span>

## <a name="introduction"></a><span data-ttu-id="476ec-104">Introduction</span><span class="sxs-lookup"><span data-stu-id="476ec-104">Introduction</span></span>

<span data-ttu-id="476ec-105">Event Hubs constitue un service qui traite de grandes quantités de données d'événement (télémétrie) à partir de périphériques et d'applications connectés.</span><span class="sxs-lookup"><span data-stu-id="476ec-105">Event Hubs is a service that processes large amounts of event data (telemetry) from connected devices and applications.</span></span> <span data-ttu-id="476ec-106">Après avoir collecté des données dans les concentrateurs d’événements, vous pouvez les stocker à l’aide d’un cluster de stockage ou les transformer à l’aide d’un fournisseur d’analyses en temps réel.</span><span class="sxs-lookup"><span data-stu-id="476ec-106">After you collect data into Event Hubs, you can store the data using a storage cluster or transform it using a real-time analytics provider.</span></span> <span data-ttu-id="476ec-107">Cette fonctionnalité de collecte et de traitement d’événements à grande échelle représente un élément clé des architectures d’applications modernes, notamment l’Internet des objets (IoT).</span><span class="sxs-lookup"><span data-stu-id="476ec-107">This large-scale event collection and processing capability is a key component of modern application architectures including the Internet of Things (IoT).</span></span>

<span data-ttu-id="476ec-108">Ce didacticiel montre comment utiliser le [portail Azure](https://portal.azure.com) pour créer un concentrateur d’événements.</span><span class="sxs-lookup"><span data-stu-id="476ec-108">This tutorial shows how to use the [Azure portal](https://portal.azure.com) to create an event hub.</span></span> <span data-ttu-id="476ec-109">Il montre également comment envoyer des événements vers un concentrateur d’événements à l’aide d’une application de console écrite en C# avec .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="476ec-109">It also shows how to send events to an event hub using a console application written in C# using the .NET Framework.</span></span> <span data-ttu-id="476ec-110">Pour recevoir des événements avec .NET Framework, consultez l’article [Recevoir des événements avec .NET Framework](event-hubs-dotnet-framework-getstarted-receive-eph.md) ou cliquez sur le langage de réception approprié dans le sommaire à gauche.</span><span class="sxs-lookup"><span data-stu-id="476ec-110">To receive events using the .NET Framework, see the [Receive events using the .NET Framework](event-hubs-dotnet-framework-getstarted-receive-eph.md) article, or click the appropriate receiving language in the left-hand table of contents.</span></span>

<span data-ttu-id="476ec-111">Pour effectuer ce didacticiel, vous avez besoin de ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="476ec-111">To complete this tutorial, you need the following prerequisites:</span></span>

* <span data-ttu-id="476ec-112">[Microsoft Visual Studio 2015 ou une version ultérieure](http://visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="476ec-112">[Microsoft Visual Studio 2015 or higher](http://visualstudio.com).</span></span> <span data-ttu-id="476ec-113">Les captures d’écran de ce didacticiel utilisent Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="476ec-113">The screen shots in this tutorial use Visual Studio 2017.</span></span>
* <span data-ttu-id="476ec-114">Un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="476ec-114">An active Azure account.</span></span> <span data-ttu-id="476ec-115">Si vous n’en avez pas, vous pouvez créer un compte gratuit en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="476ec-115">If you don't have one, you can create a free account in just a couple of minutes.</span></span> <span data-ttu-id="476ec-116">Pour plus d'informations, consultez la page [Version d'évaluation gratuite d'Azure](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="476ec-116">For details, see [Azure Free Trial](https://azure.microsoft.com/free/).</span></span>

## <a name="create-an-event-hubs-namespace-and-an-event-hub"></a><span data-ttu-id="476ec-117">Création d’un espace de noms Event Hubs et d’un concentrateur d’événements</span><span class="sxs-lookup"><span data-stu-id="476ec-117">Create an Event Hubs namespace and an event hub</span></span>

<span data-ttu-id="476ec-118">La première étape consiste à utiliser le [portail Azure](https://portal.azure.com) pour créer un espace de noms de type Event Hubs et obtenir les informations de gestion nécessaires à votre application pour communiquer avec le concentrateur d’événements.</span><span class="sxs-lookup"><span data-stu-id="476ec-118">The first step is to use the [Azure portal](https://portal.azure.com) to create a namespace of type Event Hubs, and obtain the management credentials your application needs to communicate with the event hub.</span></span> <span data-ttu-id="476ec-119">Pour créer un espace de noms et un concentrateur d’événements, suivez la procédure décrite dans [cet article](event-hubs-create.md), puis passez aux étapes suivantes de ce didactiel.</span><span class="sxs-lookup"><span data-stu-id="476ec-119">To create a namespace and event hub, follow the procedure in [this article](event-hubs-create.md), then proceed with the following steps in this tutorial.</span></span>

## <a name="create-a-sender-console-application"></a><span data-ttu-id="476ec-120">Créer une application de console d’expéditeur</span><span class="sxs-lookup"><span data-stu-id="476ec-120">Create a sender console application</span></span>

<span data-ttu-id="476ec-121">Dans cette section, vous allez écrire une application console Windows pour envoyer des événements à votre concentrateur d’événements.</span><span class="sxs-lookup"><span data-stu-id="476ec-121">In this section, you'll write a Windows console app that sends events to your event hub.</span></span>

1. <span data-ttu-id="476ec-122">Dans Visual Studio, créez un projet d'application de bureau Visual C# à l'aide du modèle de projet d' **application de console** .</span><span class="sxs-lookup"><span data-stu-id="476ec-122">In Visual Studio, create a new Visual C# Desktop App project using the **Console Application** project template.</span></span> <span data-ttu-id="476ec-123">Nommez le projet **Sender**.</span><span class="sxs-lookup"><span data-stu-id="476ec-123">Name the project **Sender**.</span></span>
   
    ![](./media/event-hubs-dotnet-framework-getstarted-send/create-sender-csharp1.png)
2. <span data-ttu-id="476ec-124">Dans l’Explorateur de solutions, cliquez avec le bouton droit sur le projet **Expéditeur**, puis cliquez sur **Gérer les packages NuGet pour la solution...**.</span><span class="sxs-lookup"><span data-stu-id="476ec-124">In Solution Explorer, right-click the **Sender** project, and then click **Manage NuGet Packages for Solution**.</span></span> 
3. <span data-ttu-id="476ec-125">Cliquez sur l’onglet **Parcourir**, puis recherchez `Microsoft Azure Service Bus`.</span><span class="sxs-lookup"><span data-stu-id="476ec-125">Click the **Browse** tab, then search for `Microsoft Azure Service Bus`.</span></span> <span data-ttu-id="476ec-126">Cliquez sur **Installer**et acceptez les conditions d’utilisation.</span><span class="sxs-lookup"><span data-stu-id="476ec-126">Click **Install**, and accept the terms of use.</span></span> 
   
    ![](./media/event-hubs-dotnet-framework-getstarted-send/create-sender-csharp2.png)
   
    <span data-ttu-id="476ec-127">Visual Studio lance le téléchargement, l’installation et ajoute une référence au [Package NuGet Azure Service Bus](https://www.nuget.org/packages/WindowsAzure.ServiceBus).</span><span class="sxs-lookup"><span data-stu-id="476ec-127">Visual Studio downloads, installs, and adds a reference to the [Azure Service Bus library NuGet package](https://www.nuget.org/packages/WindowsAzure.ServiceBus).</span></span>
4. <span data-ttu-id="476ec-128">Ajoutez les instructions `using` suivantes en haut du fichier **Program.cs** :</span><span class="sxs-lookup"><span data-stu-id="476ec-128">Add the following `using` statements at the top of the **Program.cs** file:</span></span>
   
  ```csharp
  using System.Threading;
  using Microsoft.ServiceBus.Messaging;
  ```
5. <span data-ttu-id="476ec-129">Ajoutez les champs suivants à la classe **Program** , en remplaçant les valeurs par le nom du concentrateur d’événements que vous avez créé dans la section précédente et par la chaîne de connexion au niveau de l’espace de noms, enregistrée précédemment.</span><span class="sxs-lookup"><span data-stu-id="476ec-129">Add the following fields to the **Program** class, substituting the placeholder values with the name of the event hub you created in the previous section, and the namespace-level connection string you saved previously.</span></span>
   
  ```csharp
  static string eventHubName = "{Event Hub name}";
  static string connectionString = "{send connection string}";
  ```
6. <span data-ttu-id="476ec-130">Ajoutez la méthode suivante à la classe **Program** :</span><span class="sxs-lookup"><span data-stu-id="476ec-130">Add the following method to the **Program** class:</span></span>
   
  ```csharp
  static void SendingRandomMessages()
  {
      var eventHubClient = EventHubClient.CreateFromConnectionString(connectionString, eventHubName);
      while (true)
      {
          try
          {
              var message = Guid.NewGuid().ToString();
              Console.WriteLine("{0} > Sending message: {1}", DateTime.Now, message);
              eventHubClient.Send(new EventData(Encoding.UTF8.GetBytes(message)));
          }
          catch (Exception exception)
          {
              Console.ForegroundColor = ConsoleColor.Red;
              Console.WriteLine("{0} > Exception: {1}", DateTime.Now, exception.Message);
              Console.ResetColor();
          }
   
          Thread.Sleep(200);
      }
  }
  ```
   
  <span data-ttu-id="476ec-131">Cette méthode envoie en continu les événements à votre concentrateur d’événements avec un délai de 200 ms.</span><span class="sxs-lookup"><span data-stu-id="476ec-131">This method continuously sends events to your event hub with a 200-ms delay.</span></span>
7. <span data-ttu-id="476ec-132">Enfin, ajoutez les lignes suivantes à la méthode **Main** :</span><span class="sxs-lookup"><span data-stu-id="476ec-132">Finally, add the following lines to the **Main** method:</span></span>
   
  ```csharp
  Console.WriteLine("Press Ctrl-C to stop the sender process");
  Console.WriteLine("Press Enter to start now");
  Console.ReadLine();
  SendingRandomMessages();
  ```
8. <span data-ttu-id="476ec-133">Exécutez le programme et assurez-vous qu’il n’y a aucune erreur.</span><span class="sxs-lookup"><span data-stu-id="476ec-133">Run the program, and ensure that there are no errors.</span></span>
  
<span data-ttu-id="476ec-134">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="476ec-134">Congratulations!</span></span> <span data-ttu-id="476ec-135">Vous venez d’envoyer des messages à un concentrateur d’événements.</span><span class="sxs-lookup"><span data-stu-id="476ec-135">You have now sent messages to an event hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="476ec-136">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="476ec-136">Next steps</span></span>
<span data-ttu-id="476ec-137">Vous avez conçu une application opérationnelle qui crée un concentrateur d’événements et envoie des données. Vous pouvez à présent passer aux scénarios suivants :</span><span class="sxs-lookup"><span data-stu-id="476ec-137">Now that you've built a working application that creates an event hub and sends data, you can move on to the following scenarios:</span></span>

* [<span data-ttu-id="476ec-138">Recevoir des événements avec l’hôte du processeur d’événements</span><span class="sxs-lookup"><span data-stu-id="476ec-138">Receive events using the Event Processor Host</span></span>](event-hubs-dotnet-framework-getstarted-receive-eph.md)
* [<span data-ttu-id="476ec-139">Informations de référence de l’hôte du processeur d’événements</span><span class="sxs-lookup"><span data-stu-id="476ec-139">Event Processor Host reference</span></span>](/dotnet/api/microsoft.servicebus.messaging.eventprocessorhost)
* [<span data-ttu-id="476ec-140">Vue d’ensemble des hubs d’événements</span><span class="sxs-lookup"><span data-stu-id="476ec-140">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)

<!-- Images. -->
[19]: ./media/event-hubs-csharp-ephcs-getstarted/create-eh-proj1.png
[20]: ./media/event-hubs-csharp-ephcs-getstarted/create-eh-proj2.png
[21]: ./media/event-hubs-csharp-ephcs-getstarted/run-csharp-ephcs1.png
[22]: ./media/event-hubs-csharp-ephcs-getstarted/run-csharp-ephcs2.png

