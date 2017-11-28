---
title: "aaaNotification concentrateurs - Architecture Push d’entreprise"
description: "Aide sur l’utilisation d’Azure Notification Hubs dans un environnement d’entreprise"
services: notification-hubs
documentationcenter: 
author: ysxu
manager: erikre
editor: 
ms.assetid: 903023e9-9347-442a-924b-663af85e05c6
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: c3afb83de1ba0882bf99e10f38cca40cb42d07a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="enterprise-push-architectural-guidance"></a><span data-ttu-id="400da-103">Guide architectural des notifications Push d’entreprise</span><span class="sxs-lookup"><span data-stu-id="400da-103">Enterprise push architectural guidance</span></span>
<span data-ttu-id="400da-104">Aujourd'hui, les entreprises sont progressivement mobiles, la création d’applications mobiles pour les utilisateurs finals (externe) ou des employés de hello (internes).</span><span class="sxs-lookup"><span data-stu-id="400da-104">Enterprises today are gradually moving towards creating mobile applications for either their end users (external) or for hello employees (internal).</span></span> <span data-ttu-id="400da-105">Ils ont des systèmes principaux existant en place qu’il s’agisse de grands systèmes ou certaines applications métier qui doivent être intégrées dans hello architecture de l’application mobile.</span><span class="sxs-lookup"><span data-stu-id="400da-105">They have existing backend systems in place be it mainframes or some LoB applications which must be integrated into hello mobile application architecture.</span></span> <span data-ttu-id="400da-106">Ce guide aborderons toodo la meilleure façon de cette intégration recommander des scénarios de toocommon solution possible.</span><span class="sxs-lookup"><span data-stu-id="400da-106">This guide will talk about how best toodo this integration recommending possible solution toocommon scenarios.</span></span>

<span data-ttu-id="400da-107">Une exigence fréquente est pour l’envoi des utilisateurs de toohello de notification via leurs applications mobiles par émission de données lorsqu’un événement d’intérêt se produit dans les systèmes back-end hello.</span><span class="sxs-lookup"><span data-stu-id="400da-107">A frequent requirement is for sending push notification toohello users through their mobile application when an event of interest occurs in hello backend systems.</span></span> <span data-ttu-id="400da-108">Par exemple,</span><span class="sxs-lookup"><span data-stu-id="400da-108">E.g.</span></span> <span data-ttu-id="400da-109">un client de la banque qui a des application bancaire de la banque hello sur son iPhone veut toobe notifié lorsqu’un débit est fait au-dessus d’un certain montant à partir de son compte ou un intranet où un employé à partir du service finance disposant d’une application de l’approbation de budget sur son Windows Phone veut toobe averti lorsqu’il reçoit une demande d’approbation.</span><span class="sxs-lookup"><span data-stu-id="400da-109">a bank customer who has hello bank's banking app on her iPhone wants toobe notified when a debit is made above a certain amount from her account or an intranet scenario where an employee from finance department who has a budget approval app on his Windows Phone wants toobe notified when he gets an approval request.</span></span>

<span data-ttu-id="400da-110">Hello bancaires ou le traitement de l’approbation est probablement toobe effectuée dans un système principal qui doit lancer un utilisateur de toohello par émission de données.</span><span class="sxs-lookup"><span data-stu-id="400da-110">hello bank account or approval processing is likely toobe done in some backend system which must initiate a push toohello user.</span></span> <span data-ttu-id="400da-111">Il peut y avoir plusieurs principaux de ce systèmes, ce qui doivent générer tous les hello même type de push de tooimplement logique lorsqu’un événement déclenche une notification.</span><span class="sxs-lookup"><span data-stu-id="400da-111">There may be multiple such backend systems which must all build hello same kind of logic tooimplement push when an event triggers a notification.</span></span> <span data-ttu-id="400da-112">complexité Hello ici se trouve dans l’intégration de plusieurs systèmes principaux ainsi que d’un système de transmission unique où hello les utilisateurs finaux peuvent se sont abonnées toodifferent notifications et il peut même être plusieurs applications mobiles, par exemple dans les cas de hello d’intranet des applications mobiles où une application mobile veulent tooreceive des notifications à partir de plusieurs de ces systèmes de serveur principal.</span><span class="sxs-lookup"><span data-stu-id="400da-112">hello complexity here lies in integrating several backend systems together with a single push system where hello end users may have subscribed toodifferent notifications and there may even be multiple mobile applications e.g. in hello case of intranet mobile apps where one mobile application may want tooreceive notifications from multiple such backend systems.</span></span> <span data-ttu-id="400da-113">les systèmes back-end Hello ne connaissez pas ou n’a besoin tooknow de sémantique/technologie push d’une solution courante ici traditionnellement toointroduce un composant qui interroge les systèmes principaux de hello pour tous les événements d’intérêt et est chargé d’envoyer des messages de type push hello toohello client.</span><span class="sxs-lookup"><span data-stu-id="400da-113">hello backend systems do not know or need tooknow of push semantics/technology so a common solution here traditionally has been toointroduce a component which polls hello backend systems for any events of interest and is responsible for sending hello push messages toohello client.</span></span>
<span data-ttu-id="400da-114">Ici, nous aborderons une solution plus efficace à l’aide d’Azure Service Bus - modèle de rubrique / d’abonnement qui réduit la complexité de hello lors de la solution de hello évolutive.</span><span class="sxs-lookup"><span data-stu-id="400da-114">Here we will talk about an even better solution using Azure Service Bus - Topic/Subscription model which will reduce hello complexity while making hello solution scalable.</span></span>

<span data-ttu-id="400da-115">Voici architecture générale d’hello de solution de hello (généralisée avec plusieurs applications mobiles, mais également applicables lorsqu’il y a qu’une seule application mobile)</span><span class="sxs-lookup"><span data-stu-id="400da-115">Here is hello general architecture of hello solution (generalized with multiple mobile apps but equally applicable when there is only one mobile app)</span></span>

## <a name="architecture"></a><span data-ttu-id="400da-116">Architecture</span><span class="sxs-lookup"><span data-stu-id="400da-116">Architecture</span></span>
![][1]

<span data-ttu-id="400da-117">information de clé Hello dans ce diagramme architectural est Bus des services Azure qui fournit un modèle de programmation les rubriques/abonnements (au plus [programmation de Service Bus Pub/Sub]).</span><span class="sxs-lookup"><span data-stu-id="400da-117">hello key piece in this architectural diagram is Azure Service Bus which provides a topics/subscriptions programming model (more on it at [Service Bus Pub/Sub programming]).</span></span> <span data-ttu-id="400da-118">récepteur de Hello, qui est dans ce cas, les principaux de Mobile hello (généralement [Service Mobile Azure], qui va déclencher un push toohello des applications mobiles) ne pas recevoir des messages directement à partir de systèmes principaux de hello, mais au lieu de cela, nous avons un couche d’abstraction intermédiaire fournie par [Azure Service Bus] permet aux messages de tooreceive backend mobile à partir d’un ou plusieurs systèmes back-end.</span><span class="sxs-lookup"><span data-stu-id="400da-118">hello receiver, which in this case, is hello Mobile backend (typically [Azure Mobile Service], which will initiate a push toohello mobile apps) does not receive messages directly from hello backend systems but instead we have an intermediate abstraction layer provided by [Azure Service Bus] which enables mobile backend tooreceive messages from one or more backend systems.</span></span> <span data-ttu-id="400da-119">Une rubrique Service Bus doit toobe créé pour chacune des systèmes principaux hello par exemple, compte, h, Finance qui sont essentiellement « rubriques » d’intérêt qui va lancer toobe de messages envoyé en tant que notification push.</span><span class="sxs-lookup"><span data-stu-id="400da-119">A Service Bus Topic needs toobe created for each of hello backend systems e.g. Account, HR, Finance which are basically "topics" of interest which will initiate messages toobe sent as push notification.</span></span> <span data-ttu-id="400da-120">les systèmes back-end Hello enverra les messages des rubriques de toothese.</span><span class="sxs-lookup"><span data-stu-id="400da-120">hello backend systems will send messages toothese topics.</span></span> <span data-ttu-id="400da-121">Un service principal Mobile peuvent s’abonner tooone ou plusieurs de ces rubriques en créant un abonnement Service Bus.</span><span class="sxs-lookup"><span data-stu-id="400da-121">A Mobile Backend can subscribe tooone or more such topics by creating a Service Bus subscription.</span></span> <span data-ttu-id="400da-122">Cela donnera droit hello backend mobile tooreceive une notification à partir de son système principal correspondant hello.</span><span class="sxs-lookup"><span data-stu-id="400da-122">This will entitle hello mobile backend tooreceive a notification from hello corresponding backend system.</span></span> <span data-ttu-id="400da-123">Backend mobile continue toolisten pour les messages sur leurs abonnements et dès qu’un message arrive, il reprend et l’envoie en tant que le hub de notification tooits de notification.</span><span class="sxs-lookup"><span data-stu-id="400da-123">Mobile backend continues toolisten for messages on their subscriptions and as soon as a message arrives, it turns back and sends it as notification tooits notification hub.</span></span> <span data-ttu-id="400da-124">Concentrateurs de notification puis remet finalement application mobile du toohello message hello.</span><span class="sxs-lookup"><span data-stu-id="400da-124">Notification hubs then eventually delivers hello message toohello mobile app.</span></span> <span data-ttu-id="400da-125">Composants clés de hello toosummarize, nous avons :</span><span class="sxs-lookup"><span data-stu-id="400da-125">So toosummarize hello key components, we have:</span></span>

1. <span data-ttu-id="400da-126">les systèmes principaux (systèmes métiers/hérités)</span><span class="sxs-lookup"><span data-stu-id="400da-126">Backend systems (LoB/Legacy systems)</span></span>
   * <span data-ttu-id="400da-127">Crée une rubrique Service Bus</span><span class="sxs-lookup"><span data-stu-id="400da-127">Creates Service Bus Topic</span></span>
   * <span data-ttu-id="400da-128">Envoie un message</span><span class="sxs-lookup"><span data-stu-id="400da-128">Sends Message</span></span>
2. <span data-ttu-id="400da-129">Serveur principal mobile</span><span class="sxs-lookup"><span data-stu-id="400da-129">Mobile backend</span></span>
   * <span data-ttu-id="400da-130">Crée l’abonnement au service</span><span class="sxs-lookup"><span data-stu-id="400da-130">Creates Service Subscription</span></span>
   * <span data-ttu-id="400da-131">Reçoit le message (du système principal)</span><span class="sxs-lookup"><span data-stu-id="400da-131">Receives Message (from Backend system)</span></span>
   * <span data-ttu-id="400da-132">Envoie la notification des tooclients (via le concentrateur de Notification Azure)</span><span class="sxs-lookup"><span data-stu-id="400da-132">Sends notification tooclients (via Azure Notification Hub)</span></span>
3. <span data-ttu-id="400da-133">Application mobile</span><span class="sxs-lookup"><span data-stu-id="400da-133">Mobile Application</span></span>
   * <span data-ttu-id="400da-134">Reçoit et affiche une notification</span><span class="sxs-lookup"><span data-stu-id="400da-134">Receives and display notification</span></span>

### <a name="benefits"></a><span data-ttu-id="400da-135">Avantages :</span><span class="sxs-lookup"><span data-stu-id="400da-135">Benefits:</span></span>
1. <span data-ttu-id="400da-136">Hello découplage entre l’expéditeur (systèmes back-end) et du récepteur de hello (application/service mobile via un concentrateur de Notification) permet à des systèmes back-end supplémentaires en cours d’intégration en apportant les modifications.</span><span class="sxs-lookup"><span data-stu-id="400da-136">hello decoupling between hello receiver (mobile app/service via Notification Hub) and sender (backend systems) enables additional backend systems being integrated with minimal change.</span></span>
2. <span data-ttu-id="400da-137">Cela facilite également le scénario hello dans plusieurs applications mobiles étant en mesure de tooreceive des événements à partir d’un ou plusieurs systèmes back-end.</span><span class="sxs-lookup"><span data-stu-id="400da-137">This also makes hello scenario of multiple mobile apps being able tooreceive events from one or more backend systems.</span></span>  

## <a name="sample"></a><span data-ttu-id="400da-138">Exemple :</span><span class="sxs-lookup"><span data-stu-id="400da-138">Sample:</span></span>
### <a name="prerequisites"></a><span data-ttu-id="400da-139">Composants requis</span><span class="sxs-lookup"><span data-stu-id="400da-139">Prerequisites</span></span>
<span data-ttu-id="400da-140">Vous devez effectuer hello suivant toofamiliarize didacticiels avec les concepts de hello, ainsi que les étapes de création et de configuration courantes :</span><span class="sxs-lookup"><span data-stu-id="400da-140">You should complete hello following tutorials toofamiliarize with hello concepts as well as common creation & configuration steps:</span></span>

1. <span data-ttu-id="400da-141">[programmation de Service Bus Pub/Sub] -cette rubrique explique comment détails hello de travailler avec des rubriques/abonnements Service Bus, toocreate un espace de noms toocontain rubriques/abonnements, comment toosend & recevoir des messages à partir de celles-ci.</span><span class="sxs-lookup"><span data-stu-id="400da-141">[Service Bus Pub/Sub programming] - This explains hello details of working with Service Bus Topics/Subscriptions, how toocreate a namespace toocontain topics/subscriptions, how toosend & receive messages from them.</span></span>
2. <span data-ttu-id="400da-142">[Concentrateurs de notification - didacticiel Windows universel] -ce qui explique comment tooset configurer une application du Windows Store et utiliser Notification Hubs tooregister et recevoir des notifications.</span><span class="sxs-lookup"><span data-stu-id="400da-142">[Notification Hubs - Windows Universal tutorial] - This explains how tooset up a Windows Store app and use Notification Hubs tooregister and then receive notifications.</span></span>

### <a name="sample-code"></a><span data-ttu-id="400da-143">Exemple de code</span><span class="sxs-lookup"><span data-stu-id="400da-143">Sample code</span></span>
<span data-ttu-id="400da-144">Hello exemple de code complet est disponible à l’adresse [exemples de concentrateur de Notification].</span><span class="sxs-lookup"><span data-stu-id="400da-144">hello full sample code is available at [Notification Hub Samples].</span></span> <span data-ttu-id="400da-145">Il est divisé en trois composants :</span><span class="sxs-lookup"><span data-stu-id="400da-145">It is split into three components:</span></span>

1. <span data-ttu-id="400da-146">**EnterprisePushBackendSystem**</span><span class="sxs-lookup"><span data-stu-id="400da-146">**EnterprisePushBackendSystem**</span></span>
   
    <span data-ttu-id="400da-147">a.</span><span class="sxs-lookup"><span data-stu-id="400da-147">a.</span></span> <span data-ttu-id="400da-148">Ce projet utilise hello *WindowsAzure.ServiceBus* package Nuget et est basée sur [programmation de Service Bus Pub/Sub].</span><span class="sxs-lookup"><span data-stu-id="400da-148">This project uses hello *WindowsAzure.ServiceBus* Nuget package and is  based on [Service Bus Pub/Sub programming].</span></span>
   
    <span data-ttu-id="400da-149">b.</span><span class="sxs-lookup"><span data-stu-id="400da-149">b.</span></span> <span data-ttu-id="400da-150">Il s’agit d’un simple c# console application toosimulate un système métier qui lance hello toobe de message remis toohello des applications mobiles.</span><span class="sxs-lookup"><span data-stu-id="400da-150">This is a simple C# console app toosimulate an LoB system which initiates hello message toobe delivered toohello mobile app.</span></span>
   
        static void Main(string[] args)
        {
            string connectionString =
                CloudConfigurationManager.GetSetting("Microsoft.ServiceBus.ConnectionString");
   
            // Create hello topic where we will send notifications
            CreateTopic(connectionString);
   
            // Send message
            SendMessage(connectionString);
        }
   
    <span data-ttu-id="400da-151">c.</span><span class="sxs-lookup"><span data-stu-id="400da-151">c.</span></span> <span data-ttu-id="400da-152">`CreateTopic`est la rubrique Service Bus toocreate utilisé hello où nous enverra les messages.</span><span class="sxs-lookup"><span data-stu-id="400da-152">`CreateTopic` is used toocreate hello Service Bus topic where we will send messages.</span></span>
   
        public static void CreateTopic(string connectionString)
        {
            // Create hello topic if it does not exist already
   
            var namespaceManager =
                NamespaceManager.CreateFromConnectionString(connectionString);
   
            if (!namespaceManager.TopicExists(sampleTopic))
            {
                namespaceManager.CreateTopic(sampleTopic);
            }
        }
   
    <span data-ttu-id="400da-153">d.</span><span class="sxs-lookup"><span data-stu-id="400da-153">d.</span></span> <span data-ttu-id="400da-154">`SendMessage`est utilisé toosend hello messages toothis rubrique Service Bus.</span><span class="sxs-lookup"><span data-stu-id="400da-154">`SendMessage` is used toosend hello messages toothis Service Bus Topic.</span></span> <span data-ttu-id="400da-155">Ici, nous envoyons simplement un ensemble de la rubrique de toohello des messages aléatoires régulièrement fins hello de l’exemple hello.</span><span class="sxs-lookup"><span data-stu-id="400da-155">Here we are simply sending a set of random messages toohello topic periodically for hello purpose of hello sample.</span></span> <span data-ttu-id="400da-156">Normalement, un système principal envoie des messages lorsqu’un événement se produit.</span><span class="sxs-lookup"><span data-stu-id="400da-156">Normally there will be a backend system which will send messages when an event occurs.</span></span>
   
        public static void SendMessage(string connectionString)
        {
            TopicClient client =
                TopicClient.CreateFromConnectionString(connectionString, sampleTopic);
   
            // Sends random messages every 10 seconds toohello topic
            string[] messages =
            {
                "Employee Id '{0}' has joined.",
                "Employee Id '{0}' has left.",
                "Employee Id '{0}' has switched tooa different team."
            };
   
            while (true)
            {
                Random rnd = new Random();
                string employeeId = rnd.Next(10000, 99999).ToString();
                string notification = String.Format(messages[rnd.Next(0,messages.Length)], employeeId);
   
                // Send Notification
                BrokeredMessage message = new BrokeredMessage(notification);
                client.Send(message);
   
                Console.WriteLine("{0} Message sent - '{1}'", DateTime.Now, notification);
   
                System.Threading.Thread.Sleep(new TimeSpan(0, 0, 10));
            }
        }
2. <span data-ttu-id="400da-157">**ReceiveAndSendNotification**</span><span class="sxs-lookup"><span data-stu-id="400da-157">**ReceiveAndSendNotification**</span></span>
   
    <span data-ttu-id="400da-158">a.</span><span class="sxs-lookup"><span data-stu-id="400da-158">a.</span></span> <span data-ttu-id="400da-159">Ce projet utilise hello *WindowsAzure.ServiceBus* et *Microsoft.Web.WebJobs.Publish* Nuget packages et est basée sur [programmation de Service Bus Pub/Sub].</span><span class="sxs-lookup"><span data-stu-id="400da-159">This project uses hello *WindowsAzure.ServiceBus* and *Microsoft.Web.WebJobs.Publish* Nuget packages and is based on [Service Bus Pub/Sub programming].</span></span>
   
    <span data-ttu-id="400da-160">b.</span><span class="sxs-lookup"><span data-stu-id="400da-160">b.</span></span> <span data-ttu-id="400da-161">Il s’agit d’une autre application de console c# lequel nous allons exécuter en tant qu’un [la tâche Web Azure] , car il a toorun en permanence toolisten pour les messages à partir des systèmes métier/principal de hello.</span><span class="sxs-lookup"><span data-stu-id="400da-161">This is another C# console app which we will run as an [Azure WebJob] since it has toorun continuously toolisten for messages from hello LoB/backend systems.</span></span> <span data-ttu-id="400da-162">Cela fera partie de votre serveur principal Mobile.</span><span class="sxs-lookup"><span data-stu-id="400da-162">This will be part of your Mobile backend.</span></span>
   
        static void Main(string[] args)
        {
            string connectionString =
                     CloudConfigurationManager.GetSetting("Microsoft.ServiceBus.ConnectionString");
   
            // Create hello subscription which will receive messages
            CreateSubscription(connectionString);
   
            // Receive message
            ReceiveMessageAndSendNotification(connectionString);
        }
   
    <span data-ttu-id="400da-163">c.</span><span class="sxs-lookup"><span data-stu-id="400da-163">c.</span></span> <span data-ttu-id="400da-164">`CreateSubscription`est un abonnement de Bus de Service pour la rubrique de hello toocreate utilisé où son système principal hello enverra les messages.</span><span class="sxs-lookup"><span data-stu-id="400da-164">`CreateSubscription` is used toocreate a Service Bus subscription for hello topic where hello backend system will send messages.</span></span> <span data-ttu-id="400da-165">Selon le scénario d’entreprise hello, ce composant créera un ou plusieurs abonnements rubriques toocorresponding (par exemple, certaines peuvent recevoir les messages à partir du système des ressources humaines, certains à partir de système de Finance et ainsi de suite)</span><span class="sxs-lookup"><span data-stu-id="400da-165">Depending on hello business scenario, this component will create one or more subscriptions toocorresponding topics (e.g. some may be receiving messages from HR system, some from Finance system, and so on)</span></span>
   
        static void CreateSubscription(string connectionString)
        {
            // Create hello subscription if it does not exist already
            var namespaceManager =
                NamespaceManager.CreateFromConnectionString(connectionString);
   
            if (!namespaceManager.SubscriptionExists(sampleTopic, sampleSubscription))
            {
                namespaceManager.CreateSubscription(sampleTopic, sampleSubscription);
            }
        }
   
    <span data-ttu-id="400da-166">d.</span><span class="sxs-lookup"><span data-stu-id="400da-166">d.</span></span> <span data-ttu-id="400da-167">ReceiveMessageAndSendNotification est le message de type hello tooread utilisé à partir de la rubrique hello à l’aide de son abonnement et si hello lecture réussit puis élaborer une toohello de toobe envoyé de notification (dans l’exemple de scénario hello une notification toast native de Windows) mobile application à l’aide de Azure Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="400da-167">ReceiveMessageAndSendNotification is used tooread hello message from hello topic using its subscription and if hello read is successful then craft a notification (in hello sample scenario a Windows native toast notification) toobe sent toohello mobile application using Azure Notification Hubs.</span></span>
   
        static void ReceiveMessageAndSendNotification(string connectionString)
        {
            // Initialize hello Notification Hub
            string hubConnectionString = CloudConfigurationManager.GetSetting
                    ("Microsoft.NotificationHub.ConnectionString");
            hub = NotificationHubClient.CreateClientFromConnectionString
                    (hubConnectionString, "enterprisepushservicehub");
   
            SubscriptionClient Client =
                SubscriptionClient.CreateFromConnectionString
                        (connectionString, sampleTopic, sampleSubscription);
   
            Client.Receive();
   
            // Continuously process messages received from hello subscription
            while (true)
            {
                BrokeredMessage message = Client.Receive();
                var toastMessage = @"<toast><visual><binding template=""ToastText01""><text id=""1"">{messagepayload}</text></binding></visual></toast>";
   
                if (message != null)
                {
                    try
                    {
                        Console.WriteLine(message.MessageId);
                        Console.WriteLine(message.SequenceNumber);
                        string messageBody = message.GetBody<string>();
                        Console.WriteLine("Body: " + messageBody + "\n");
   
                        toastMessage = toastMessage.Replace("{messagepayload}", messageBody);
                        SendNotificationAsync(toastMessage);
   
                        // Remove message from subscription
                        message.Complete();
                    }
                    catch (Exception)
                    {
                        // Indicate a problem, unlock message in subscription
                        message.Abandon();
                    }
                }
            }
        }
        static async void SendNotificationAsync(string message)
        {
            await hub.SendWindowsNativeNotificationAsync(message);
        }
   
    <span data-ttu-id="400da-168">e.</span><span class="sxs-lookup"><span data-stu-id="400da-168">e.</span></span> <span data-ttu-id="400da-169">Pour la publication en tant qu’un **WebJob**, cliquez avec le bouton droit sur la solution hello dans Visual Studio et sélectionnez **publier en tant que tâche Web**</span><span class="sxs-lookup"><span data-stu-id="400da-169">For publishing this as a **WebJob**, right click on hello solution in Visual Studio and select **Publish as WebJob**</span></span>
   
    ![][2]
   
    <span data-ttu-id="400da-170">f.</span><span class="sxs-lookup"><span data-stu-id="400da-170">f.</span></span> <span data-ttu-id="400da-171">Sélectionnez votre profil de publication et créer un nouveau site Web de Azure s’il n’existe déjà qui va héberger cette tâche Web et une fois que du site Web hello puis **publier**.</span><span class="sxs-lookup"><span data-stu-id="400da-171">Select your publishing profile and create a new Azure WebSite if it doesnt exist already which will host this WebJob and once you have hello WebSite then **Publish**.</span></span>
   
    ![][3]
   
    <span data-ttu-id="400da-172">g.</span><span class="sxs-lookup"><span data-stu-id="400da-172">g.</span></span> <span data-ttu-id="400da-173">Configurer hello toobe de tâche « Exécuter en continu » de sorte que lorsque vous ouvrez une session dans toohello [portail classique Azure] vous devez voir quelque chose comme hello ci-après :</span><span class="sxs-lookup"><span data-stu-id="400da-173">Configure hello job toobe "Run Continuously" so that when you log in toohello [Azure Classic Portal] you should see something like hello following:</span></span>
   
    ![][4]
3. <span data-ttu-id="400da-174">**EnterprisePushMobileApp**</span><span class="sxs-lookup"><span data-stu-id="400da-174">**EnterprisePushMobileApp**</span></span>
   
    <span data-ttu-id="400da-175">a.</span><span class="sxs-lookup"><span data-stu-id="400da-175">a.</span></span> <span data-ttu-id="400da-176">Il s’agit d’une application du Windows Store qui reçoivent des notifications toast à partir de l’exécution de la tâche Web hello dans le cadre de votre serveur principal Mobile et l’afficher.</span><span class="sxs-lookup"><span data-stu-id="400da-176">This is a Windows Store application which will receive toast notifications from hello WebJob running as part of your Mobile backend and display it.</span></span> <span data-ttu-id="400da-177">Elle repose sur [Concentrateurs de notification - didacticiel Windows universel].</span><span class="sxs-lookup"><span data-stu-id="400da-177">This is based on [Notification Hubs - Windows Universal tutorial].</span></span>  
   
    <span data-ttu-id="400da-178">b.</span><span class="sxs-lookup"><span data-stu-id="400da-178">b.</span></span> <span data-ttu-id="400da-179">Assurez-vous que votre application est activé tooreceive des notifications de toast.</span><span class="sxs-lookup"><span data-stu-id="400da-179">Ensure that your application is enabled tooreceive toast notifications.</span></span>
   
    <span data-ttu-id="400da-180">c.</span><span class="sxs-lookup"><span data-stu-id="400da-180">c.</span></span> <span data-ttu-id="400da-181">Vérifiez que hello suivant le code d’enregistrement de concentrateurs de Notification est appelée à hello application démarrent (après le remplacement hello *HubName* et *DefaultListenSharedAccessSignature*:</span><span class="sxs-lookup"><span data-stu-id="400da-181">Ensure that hello following Notification Hubs registration code is being called at hello App start up (after replacing hello *HubName* and *DefaultListenSharedAccessSignature*:</span></span>
   
        private async void InitNotificationsAsync()
        {
            var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();
   
            var hub = new NotificationHub("[HubName]", "[DefaultListenSharedAccessSignature]");
            var result = await hub.RegisterNativeAsync(channel.Uri);
   
            // Displays hello registration ID so you know it was successful
            if (result.RegistrationId != null)
            {
                var dialog = new MessageDialog("Registration successful: " + result.RegistrationId);
                dialog.Commands.Add(new UICommand("OK"));
                await dialog.ShowAsync();
            }
        }

### <a name="running-sample"></a><span data-ttu-id="400da-182">Exemple d’exécution :</span><span class="sxs-lookup"><span data-stu-id="400da-182">Running sample:</span></span>
1. <span data-ttu-id="400da-183">Assurez-vous que votre tâche Web est en cours d’exécution avec succès et planifié trop « exécuter en continu ».</span><span class="sxs-lookup"><span data-stu-id="400da-183">Ensure that your WebJob is running successfully and scheduled too"Run Continuously".</span></span>
2. <span data-ttu-id="400da-184">Exécutez hello **EnterprisePushMobileApp** démarrer hello application du Windows Store.</span><span class="sxs-lookup"><span data-stu-id="400da-184">Run hello **EnterprisePushMobileApp** which will start hello Windows Store app.</span></span>
3. <span data-ttu-id="400da-185">Exécutez hello **EnterprisePushBackendSystem** application console qui simule hello LoB principal et commencer l’envoi des messages et des notifications de toast apparaissant hello suivante doit s’afficher :</span><span class="sxs-lookup"><span data-stu-id="400da-185">Run hello **EnterprisePushBackendSystem** console application which will simulate hello LoB backend and will start sending messages and you should see toast notifications appearing like hello following:</span></span>
   
    ![][5]
4. <span data-ttu-id="400da-186">messages Hello ont été envoyés à l’origine des rubriques de Bus tooService qui était en cours d’analyse par abonnements Service Bus dans votre projet Web.</span><span class="sxs-lookup"><span data-stu-id="400da-186">hello messages were originally sent tooService Bus topics which was being monitored by Service Bus subscriptions in your Web Job.</span></span> <span data-ttu-id="400da-187">Une fois qu’un message a été reçu, une notification a été créée et envoyée toohello des applications mobiles.</span><span class="sxs-lookup"><span data-stu-id="400da-187">Once a message was received, a notification was created and sent toohello mobile app.</span></span> <span data-ttu-id="400da-188">Vous pouvez consulter hello ouvre une tâche Web tooconfirm hello traitement lorsque vous passez toohello lien de journaux dans [portail classique Azure] pour votre tâche Web :</span><span class="sxs-lookup"><span data-stu-id="400da-188">You can look through hello WebJob logs tooconfirm hello processing when you go toohello Logs link in [Azure Classic Portal] for your Web Job:</span></span>
   
    ![][6]

<!-- Images -->
[1]: ./media/notification-hubs-enterprise-push-architecture/architecture.png
[2]: ./media/notification-hubs-enterprise-push-architecture/WebJobsContextMenu.png
[3]: ./media/notification-hubs-enterprise-push-architecture/PublishAsWebJob.png
[4]: ./media/notification-hubs-enterprise-push-architecture/WebJob.png
[5]: ./media/notification-hubs-enterprise-push-architecture/Notifications.png
[6]: ./media/notification-hubs-enterprise-push-architecture/WebJobsLog.png

<!-- Links -->
[exemples de concentrateur de Notification]: https://github.com/Azure/azure-notificationhubs-samples
[Service Mobile Azure]: http://azure.microsoft.com/documentation/services/mobile-services/
[Azure Service Bus]: http://azure.microsoft.com/documentation/articles/fundamentals-service-bus-hybrid-solutions/
[programmation de Service Bus Pub/Sub]: http://azure.microsoft.com/documentation/articles/service-bus-dotnet-how-to-use-topics-subscriptions/
[la tâche Web Azure]: http://azure.microsoft.com/documentation/articles/web-sites-create-web-jobs/
[Concentrateurs de notification - didacticiel Windows universel]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-store-dotnet-get-started/
[portail classique Azure]: https://manage.windowsazure.com/
