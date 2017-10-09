---
title: "aaaSend événements tooAzure concentrateurs d’événements à l’aide de hello .NET Framework | Documents Microsoft"
description: "Prise en main de l’envoi d’événements concentrateurs tooEvent à l’aide de hello .NET Framework"
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
ms.openlocfilehash: 05514546a6094096e4a3c800db058190076de80a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="send-events-tooazure-event-hubs-using-hello-net-framework"></a><span data-ttu-id="c3698-103">Envoyer des événements de concentrateurs d’événements tooAzure à l’aide de hello .NET Framework</span><span class="sxs-lookup"><span data-stu-id="c3698-103">Send events tooAzure Event Hubs using hello .NET Framework</span></span>

## <a name="introduction"></a><span data-ttu-id="c3698-104">Introduction</span><span class="sxs-lookup"><span data-stu-id="c3698-104">Introduction</span></span>

<span data-ttu-id="c3698-105">Event Hubs constitue un service qui traite de grandes quantités de données d'événement (télémétrie) à partir de périphériques et d'applications connectés.</span><span class="sxs-lookup"><span data-stu-id="c3698-105">Event Hubs is a service that processes large amounts of event data (telemetry) from connected devices and applications.</span></span> <span data-ttu-id="c3698-106">Après avoir recueilli les données aux concentrateurs d’événements, vous pouvez stocker les données de salutation à l’aide d’un cluster de stockage ou transformer à l’aide d’un fournisseur de l’analytique en temps réel.</span><span class="sxs-lookup"><span data-stu-id="c3698-106">After you collect data into Event Hubs, you can store hello data using a storage cluster or transform it using a real-time analytics provider.</span></span> <span data-ttu-id="c3698-107">Cette fonctionnalité de collecte et de traitement des événements à grande échelle est un composant clé des architectures d’application moderne, y compris hello Internet of Things (IoT).</span><span class="sxs-lookup"><span data-stu-id="c3698-107">This large-scale event collection and processing capability is a key component of modern application architectures including hello Internet of Things (IoT).</span></span>

<span data-ttu-id="c3698-108">Ce didacticiel montre comment toouse hello [portail Azure](https://portal.azure.com) toocreate un concentrateur d’événements.</span><span class="sxs-lookup"><span data-stu-id="c3698-108">This tutorial shows how toouse hello [Azure portal](https://portal.azure.com) toocreate an event hub.</span></span> <span data-ttu-id="c3698-109">Il montre également comment le concentrateur d’événements toosend événements tooan à l’aide d’une application console écrite en c# à l’aide de hello .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="c3698-109">It also shows how toosend events tooan event hub using a console application written in C# using hello .NET Framework.</span></span> <span data-ttu-id="c3698-110">événements de tooreceive à l’aide de hello .NET Framework, consultez hello [recevoir des événements à l’aide de .NET Framework de hello](event-hubs-dotnet-framework-getstarted-receive-eph.md) article, ou cliquez sur hello réception langue dans la table de gauche hello du contenu.</span><span class="sxs-lookup"><span data-stu-id="c3698-110">tooreceive events using hello .NET Framework, see hello [Receive events using hello .NET Framework](event-hubs-dotnet-framework-getstarted-receive-eph.md) article, or click hello appropriate receiving language in hello left-hand table of contents.</span></span>

<span data-ttu-id="c3698-111">toocomplete ce didacticiel, vous devez hello suivant des conditions préalables :</span><span class="sxs-lookup"><span data-stu-id="c3698-111">toocomplete this tutorial, you need hello following prerequisites:</span></span>

* <span data-ttu-id="c3698-112">[Microsoft Visual Studio 2015 ou une version ultérieure](http://visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="c3698-112">[Microsoft Visual Studio 2015 or higher](http://visualstudio.com).</span></span> <span data-ttu-id="c3698-113">captures d’écran Hello dans ce didacticiel utilisent Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="c3698-113">hello screen shots in this tutorial use Visual Studio 2017.</span></span>
* <span data-ttu-id="c3698-114">Un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="c3698-114">An active Azure account.</span></span> <span data-ttu-id="c3698-115">Si vous n’en avez pas, vous pouvez créer un compte gratuit en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="c3698-115">If you don't have one, you can create a free account in just a couple of minutes.</span></span> <span data-ttu-id="c3698-116">Pour plus d'informations, consultez la page [Version d'évaluation gratuite d'Azure](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="c3698-116">For details, see [Azure Free Trial](https://azure.microsoft.com/free/).</span></span>

## <a name="create-an-event-hubs-namespace-and-an-event-hub"></a><span data-ttu-id="c3698-117">Création d’un espace de noms Event Hubs et d’un concentrateur d’événements</span><span class="sxs-lookup"><span data-stu-id="c3698-117">Create an Event Hubs namespace and an event hub</span></span>

<span data-ttu-id="c3698-118">première étape de Hello est toouse hello [portail Azure](https://portal.azure.com) toocreate un espace de noms de concentrateurs d’événements de type et obtenir des informations d’identification d’administration votre application doit toocommunicate avec un concentrateur d’événements hello hello.</span><span class="sxs-lookup"><span data-stu-id="c3698-118">hello first step is toouse hello [Azure portal](https://portal.azure.com) toocreate a namespace of type Event Hubs, and obtain hello management credentials your application needs toocommunicate with hello event hub.</span></span> <span data-ttu-id="c3698-119">toocreate un espace de noms et le concentrateur d’événements, suivez la procédure hello dans [cet article](event-hubs-create.md), puis poursuivez hello suivant les étapes de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="c3698-119">toocreate a namespace and event hub, follow hello procedure in [this article](event-hubs-create.md), then proceed with hello following steps in this tutorial.</span></span>

## <a name="create-a-sender-console-application"></a><span data-ttu-id="c3698-120">Créer une application de console d’expéditeur</span><span class="sxs-lookup"><span data-stu-id="c3698-120">Create a sender console application</span></span>

<span data-ttu-id="c3698-121">Dans cette section, vous allez écrire une application de console Windows qui envoie le concentrateur d’événements événements tooyour.</span><span class="sxs-lookup"><span data-stu-id="c3698-121">In this section, you'll write a Windows console app that sends events tooyour event hub.</span></span>

1. <span data-ttu-id="c3698-122">Dans Visual Studio, créez un nouveau projet d’application de bureau Visual c# à l’aide de hello **Application Console** modèle de projet.</span><span class="sxs-lookup"><span data-stu-id="c3698-122">In Visual Studio, create a new Visual C# Desktop App project using hello **Console Application** project template.</span></span> <span data-ttu-id="c3698-123">Projet de hello nom **expéditeur**.</span><span class="sxs-lookup"><span data-stu-id="c3698-123">Name hello project **Sender**.</span></span>
   
    ![](./media/event-hubs-dotnet-framework-getstarted-send/create-sender-csharp1.png)
2. <span data-ttu-id="c3698-124">Dans l’Explorateur de solutions, cliquez sur hello **expéditeur** de projet, puis cliquez sur **gérer les Packages NuGet pour la Solution**.</span><span class="sxs-lookup"><span data-stu-id="c3698-124">In Solution Explorer, right-click hello **Sender** project, and then click **Manage NuGet Packages for Solution**.</span></span> 
3. <span data-ttu-id="c3698-125">Cliquez sur hello **Parcourir** onglet, puis recherchez `Microsoft Azure Service Bus`.</span><span class="sxs-lookup"><span data-stu-id="c3698-125">Click hello **Browse** tab, then search for `Microsoft Azure Service Bus`.</span></span> <span data-ttu-id="c3698-126">Cliquez sur **installer**et acceptez les conditions d’utilisation de hello.</span><span class="sxs-lookup"><span data-stu-id="c3698-126">Click **Install**, and accept hello terms of use.</span></span> 
   
    ![](./media/event-hubs-dotnet-framework-getstarted-send/create-sender-csharp2.png)
   
    <span data-ttu-id="c3698-127">Visual Studio télécharge, installe et ajoute une référence toohello [package NuGet de bibliothèque Azure Service Bus](https://www.nuget.org/packages/WindowsAzure.ServiceBus).</span><span class="sxs-lookup"><span data-stu-id="c3698-127">Visual Studio downloads, installs, and adds a reference toohello [Azure Service Bus library NuGet package](https://www.nuget.org/packages/WindowsAzure.ServiceBus).</span></span>
4. <span data-ttu-id="c3698-128">Ajoutez hello suivant `using` instructions haut hello hello **Program.cs** fichier :</span><span class="sxs-lookup"><span data-stu-id="c3698-128">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>
   
  ```csharp
  using System.Threading;
  using Microsoft.ServiceBus.Messaging;
  ```
5. <span data-ttu-id="c3698-129">Ajouter hello suivant champs toohello **programme** (classe), en remplaçant les valeurs d’espace réservé hello avec nom hello du concentrateur d’événements hello vous avez créé dans la section précédente de hello et chaîne de connexion au niveau de l’espace de noms hello vous avez enregistré précédemment.</span><span class="sxs-lookup"><span data-stu-id="c3698-129">Add hello following fields toohello **Program** class, substituting hello placeholder values with hello name of hello event hub you created in hello previous section, and hello namespace-level connection string you saved previously.</span></span>
   
  ```csharp
  static string eventHubName = "{Event Hub name}";
  static string connectionString = "{send connection string}";
  ```
6. <span data-ttu-id="c3698-130">Ajouter hello suivant de méthode toohello **programme** classe :</span><span class="sxs-lookup"><span data-stu-id="c3698-130">Add hello following method toohello **Program** class:</span></span>
   
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
   
  <span data-ttu-id="c3698-131">Cette méthode envoie en permanence le concentrateur d’événements événements tooyour dans un délai de 200 ms.</span><span class="sxs-lookup"><span data-stu-id="c3698-131">This method continuously sends events tooyour event hub with a 200-ms delay.</span></span>
7. <span data-ttu-id="c3698-132">Enfin, ajoutez hello suivant lignes toohello **Main** méthode :</span><span class="sxs-lookup"><span data-stu-id="c3698-132">Finally, add hello following lines toohello **Main** method:</span></span>
   
  ```csharp
  Console.WriteLine("Press Ctrl-C toostop hello sender process");
  Console.WriteLine("Press Enter toostart now");
  Console.ReadLine();
  SendingRandomMessages();
  ```
8. <span data-ttu-id="c3698-133">Exécuter le programme de hello et vérifiez qu’il n’y a aucune erreur.</span><span class="sxs-lookup"><span data-stu-id="c3698-133">Run hello program, and ensure that there are no errors.</span></span>
  
<span data-ttu-id="c3698-134">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="c3698-134">Congratulations!</span></span> <span data-ttu-id="c3698-135">Vous avez maintenant envoyé concentrateur d’événements tooan messages.</span><span class="sxs-lookup"><span data-stu-id="c3698-135">You have now sent messages tooan event hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c3698-136">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c3698-136">Next steps</span></span>
<span data-ttu-id="c3698-137">Maintenant que vous avez créé une application opérationnelle qui crée un concentrateur d’événements et envoie les données, vous pouvez déplacer sur toohello les scénarios suivants :</span><span class="sxs-lookup"><span data-stu-id="c3698-137">Now that you've built a working application that creates an event hub and sends data, you can move on toohello following scenarios:</span></span>

* [<span data-ttu-id="c3698-138">Recevoir des événements à l’aide de hello processeur d’événements hôte</span><span class="sxs-lookup"><span data-stu-id="c3698-138">Receive events using hello Event Processor Host</span></span>](event-hubs-dotnet-framework-getstarted-receive-eph.md)
* [<span data-ttu-id="c3698-139">Informations de référence de l’hôte du processeur d’événements</span><span class="sxs-lookup"><span data-stu-id="c3698-139">Event Processor Host reference</span></span>](/dotnet/api/microsoft.servicebus.messaging.eventprocessorhost)
* [<span data-ttu-id="c3698-140">Vue d’ensemble des hubs d’événements</span><span class="sxs-lookup"><span data-stu-id="c3698-140">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)

<!-- Images. -->
[19]: ./media/event-hubs-csharp-ephcs-getstarted/create-eh-proj1.png
[20]: ./media/event-hubs-csharp-ephcs-getstarted/create-eh-proj2.png
[21]: ./media/event-hubs-csharp-ephcs-getstarted/run-csharp-ephcs1.png
[22]: ./media/event-hubs-csharp-ephcs-getstarted/run-csharp-ephcs2.png

