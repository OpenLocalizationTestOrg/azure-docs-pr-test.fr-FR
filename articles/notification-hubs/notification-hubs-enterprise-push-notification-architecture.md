---
title: "Notification Hubs - Architecture Push d’entreprise"
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
ms.openlocfilehash: ae7c1c9644ecfe7fe4ad6e332cc0683a3b5df22f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="enterprise-push-architectural-guidance"></a><span data-ttu-id="b40bc-103">Guide architectural des notifications Push d’entreprise</span><span class="sxs-lookup"><span data-stu-id="b40bc-103">Enterprise push architectural guidance</span></span>
<span data-ttu-id="b40bc-104">Les entreprises se tournent aujourd’hui progressivement vers la création d’applications mobiles pour leurs clients (externes) ou leurs collaborateurs (internes).</span><span class="sxs-lookup"><span data-stu-id="b40bc-104">Enterprises today are gradually moving towards creating mobile applications for either their end users (external) or for the employees (internal).</span></span> <span data-ttu-id="b40bc-105">Ils disposent de systèmes principaux, qu’il s’agisse de grands systèmes ou de certaines applications métiers, qui doivent être intégrés à l’architecture de l’application mobile.</span><span class="sxs-lookup"><span data-stu-id="b40bc-105">They have existing backend systems in place be it mainframes or some LoB applications which must be integrated into the mobile application architecture.</span></span> <span data-ttu-id="b40bc-106">Ce guide vous présente comment réussir au mieux cette intégration, en recommandant des solutions possibles pour les scénarios habituels.</span><span class="sxs-lookup"><span data-stu-id="b40bc-106">This guide will talk about how best to do this integration recommending possible solution to common scenarios.</span></span>

<span data-ttu-id="b40bc-107">Une exigence fréquente est l’envoi de notifications Push aux utilisateurs via leurs applications mobiles, lorsqu’un événement se produit dans les systèmes principaux.</span><span class="sxs-lookup"><span data-stu-id="b40bc-107">A frequent requirement is for sending push notification to the users through their mobile application when an event of interest occurs in the backend systems.</span></span> <span data-ttu-id="b40bc-108">Par exemple,</span><span class="sxs-lookup"><span data-stu-id="b40bc-108">E.g.</span></span> <span data-ttu-id="b40bc-109">un client d’une banque disposant d’une application bancaire sur son iPhone souhaite être averti lorsque son compte est débité d’un montant supérieur à un seuil défini ou un scénario intranet dans lequel un employé du service financier disposant d’une application d’approbation du budget sur son téléphone Windows Phone souhaite être averti lorsqu’il reçoit une demande d’approbation.</span><span class="sxs-lookup"><span data-stu-id="b40bc-109">a bank customer who has the bank's banking app on her iPhone wants to be notified when a debit is made above a certain amount from her account or an intranet scenario where an employee from finance department who has a budget approval app on his Windows Phone wants to be notified when he gets an approval request.</span></span>

<span data-ttu-id="b40bc-110">Le traitement des comptes bancaires ou des approbations sont généralement effectués dans un système principal, qui doit envoyer une notification Push à l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="b40bc-110">The bank account or approval processing is likely to be done in some backend system which must initiate a push to the user.</span></span> <span data-ttu-id="b40bc-111">Il peut y avoir plusieurs systèmes principaux qui doivent tous générer le même genre de logique afin d’implémenter une notification Push lorsqu’un événement la déclenche.</span><span class="sxs-lookup"><span data-stu-id="b40bc-111">There may be multiple such backend systems which must all build the same kind of logic to implement push when an event triggers a notification.</span></span> <span data-ttu-id="b40bc-112">Ici, la complexité réside dans l’intégration de plusieurs systèmes principaux avec un système Push unique où les utilisateurs peuvent être abonnés à différentes notifications et même peut-être à plusieurs applications mobiles, par exemple dans le cas d’applications mobiles intranet où une application mobile peut recevoir des notifications à partir de plusieurs systèmes principaux.</span><span class="sxs-lookup"><span data-stu-id="b40bc-112">The complexity here lies in integrating several backend systems together with a single push system where the end users may have subscribed to different notifications and there may even be multiple mobile applications e.g. in the case of intranet mobile apps where one mobile application may want to receive notifications from multiple such backend systems.</span></span> <span data-ttu-id="b40bc-113">Les systèmes principaux n’ont pas besoin de connaître une technologie ou une sémantique Push. Une solution courante a donc généralement été d’introduire un composant qui interroge les systèmes principaux pour tout événement vous intéressant et qui est chargé d’envoyer les messages Push au client.</span><span class="sxs-lookup"><span data-stu-id="b40bc-113">The backend systems do not know or need to know of push semantics/technology so a common solution here traditionally has been to introduce a component which polls the backend systems for any events of interest and is responsible for sending the push messages to the client.</span></span>
<span data-ttu-id="b40bc-114">Nous présenterons ici une solution encore plus efficace qui s’appuie sur le modèle Azure Service Bus - Rubrique/abonnement et réduit la complexité tout en rendant la solution évolutive.</span><span class="sxs-lookup"><span data-stu-id="b40bc-114">Here we will talk about an even better solution using Azure Service Bus - Topic/Subscription model which will reduce the complexity while making the solution scalable.</span></span>

<span data-ttu-id="b40bc-115">Voici l’architecture générale de la solution (généralisée pour plusieurs applications mobiles mais également applicable lorsqu’il n’y a qu’une seule application mobile)</span><span class="sxs-lookup"><span data-stu-id="b40bc-115">Here is the general architecture of the solution (generalized with multiple mobile apps but equally applicable when there is only one mobile app)</span></span>

## <a name="architecture"></a><span data-ttu-id="b40bc-116">Architecture</span><span class="sxs-lookup"><span data-stu-id="b40bc-116">Architecture</span></span>
![][1]

<span data-ttu-id="b40bc-117">L'élément clé de ce diagramme architectural est Azure Service Bus, qui fournit un modèle de programmation des rubriques/abonnements (la page [programmation Service Bus Pub/Sub]apporte plus d'informations à ce sujet).</span><span class="sxs-lookup"><span data-stu-id="b40bc-117">The key piece in this architectural diagram is Azure Service Bus which provides a topics/subscriptions programming model (more on it at [Service Bus Pub/Sub programming]).</span></span> <span data-ttu-id="b40bc-118">Le récepteur, dans ce cas le serveur principal Mobile (généralement [Azure Mobile Service], qui initie une notification Push vers les applications mobiles), ne reçoit pas les messages directement à partir des systèmes principaux, mais, au lieu de cela, il existe une couche d’abstraction intermédiaire fournie par [Azure Service Bus] qui permet au serveur mobile principal de recevoir des messages à partir d’un ou plusieurs systèmes principaux.</span><span class="sxs-lookup"><span data-stu-id="b40bc-118">The receiver, which in this case, is the Mobile backend (typically [Azure Mobile Service], which will initiate a push to the mobile apps) does not receive messages directly from the backend systems but instead we have an intermediate abstraction layer provided by [Azure Service Bus] which enables mobile backend to receive messages from one or more backend systems.</span></span> <span data-ttu-id="b40bc-119">Une rubrique Service Bus doit être créée pour chacun des systèmes principaux, par exemple Comptabilité, RH, Finance, qui sont essentiellement des « rubriques » d’intérêt qui génèrent des messages à envoyer en tant que notification Push.</span><span class="sxs-lookup"><span data-stu-id="b40bc-119">A Service Bus Topic needs to be created for each of the backend systems e.g. Account, HR, Finance which are basically "topics" of interest which will initiate messages to be sent as push notification.</span></span> <span data-ttu-id="b40bc-120">Les systèmes principaux envoient les messages à ces rubriques.</span><span class="sxs-lookup"><span data-stu-id="b40bc-120">The backend systems will send messages to these topics.</span></span> <span data-ttu-id="b40bc-121">Un service principal Mobile peut s’abonner à une ou plusieurs de ces rubriques en créant un abonnement Service Bus.</span><span class="sxs-lookup"><span data-stu-id="b40bc-121">A Mobile Backend can subscribe to one or more such topics by creating a Service Bus subscription.</span></span> <span data-ttu-id="b40bc-122">Cela autorisera le serveur principal mobile à recevoir une notification du système principal correspondant.</span><span class="sxs-lookup"><span data-stu-id="b40bc-122">This will entitle the mobile backend to receive a notification from the corresponding backend system.</span></span> <span data-ttu-id="b40bc-123">Le serveur principal mobile continue à écouter les messages sur ses abonnements et dès qu’un message arrive, il le reprend et l’envoie sous forme de notification à son hub de notification.</span><span class="sxs-lookup"><span data-stu-id="b40bc-123">Mobile backend continues to listen for messages on their subscriptions and as soon as a message arrives, it turns back and sends it as notification to its notification hub.</span></span> <span data-ttu-id="b40bc-124">Pour finir, les hubs de notification remettent ensuite le message à l’application mobile.</span><span class="sxs-lookup"><span data-stu-id="b40bc-124">Notification hubs then eventually delivers the message to the mobile app.</span></span> <span data-ttu-id="b40bc-125">Pour résumer, les composants clés sont donc :</span><span class="sxs-lookup"><span data-stu-id="b40bc-125">So to summarize the key components, we have:</span></span>

1. <span data-ttu-id="b40bc-126">les systèmes principaux (systèmes métiers/hérités)</span><span class="sxs-lookup"><span data-stu-id="b40bc-126">Backend systems (LoB/Legacy systems)</span></span>
   * <span data-ttu-id="b40bc-127">Crée une rubrique Service Bus</span><span class="sxs-lookup"><span data-stu-id="b40bc-127">Creates Service Bus Topic</span></span>
   * <span data-ttu-id="b40bc-128">Envoie un message</span><span class="sxs-lookup"><span data-stu-id="b40bc-128">Sends Message</span></span>
2. <span data-ttu-id="b40bc-129">Serveur principal mobile</span><span class="sxs-lookup"><span data-stu-id="b40bc-129">Mobile backend</span></span>
   * <span data-ttu-id="b40bc-130">Crée l’abonnement au service</span><span class="sxs-lookup"><span data-stu-id="b40bc-130">Creates Service Subscription</span></span>
   * <span data-ttu-id="b40bc-131">Reçoit le message (du système principal)</span><span class="sxs-lookup"><span data-stu-id="b40bc-131">Receives Message (from Backend system)</span></span>
   * <span data-ttu-id="b40bc-132">Envoie une notification aux clients (via Azure Notification Hub)</span><span class="sxs-lookup"><span data-stu-id="b40bc-132">Sends notification to clients (via Azure Notification Hub)</span></span>
3. <span data-ttu-id="b40bc-133">Application mobile</span><span class="sxs-lookup"><span data-stu-id="b40bc-133">Mobile Application</span></span>
   * <span data-ttu-id="b40bc-134">Reçoit et affiche une notification</span><span class="sxs-lookup"><span data-stu-id="b40bc-134">Receives and display notification</span></span>

### <a name="benefits"></a><span data-ttu-id="b40bc-135">Avantages :</span><span class="sxs-lookup"><span data-stu-id="b40bc-135">Benefits:</span></span>
1. <span data-ttu-id="b40bc-136">Le découplage entre l’expéditeur (les systèmes principaux) et le récepteur (application/service mobile via Notification Hub) permet à des systèmes principaux supplémentaires d’être intégrés, et ce avec un minimum de modifications.</span><span class="sxs-lookup"><span data-stu-id="b40bc-136">The decoupling between the receiver (mobile app/service via Notification Hub) and sender (backend systems) enables additional backend systems being integrated with minimal change.</span></span>
2. <span data-ttu-id="b40bc-137">Cela permet également à plusieurs applications mobiles de recevoir des événements à partir d’un ou plusieurs systèmes principaux.</span><span class="sxs-lookup"><span data-stu-id="b40bc-137">This also makes the scenario of multiple mobile apps being able to receive events from one or more backend systems.</span></span>  

## <a name="sample"></a><span data-ttu-id="b40bc-138">Exemple :</span><span class="sxs-lookup"><span data-stu-id="b40bc-138">Sample:</span></span>
### <a name="prerequisites"></a><span data-ttu-id="b40bc-139">Composants requis</span><span class="sxs-lookup"><span data-stu-id="b40bc-139">Prerequisites</span></span>
<span data-ttu-id="b40bc-140">Vous devez suivre les didacticiels suivants pour vous familiariser avec les concepts et les étapes habituelles de création et de configuration :</span><span class="sxs-lookup"><span data-stu-id="b40bc-140">You should complete the following tutorials to familiarize with the concepts as well as common creation & configuration steps:</span></span>

1. <span data-ttu-id="b40bc-141">[programmation Service Bus Pub/Sub] : ce didacticiel explique en détail comment utiliser des rubriques/abonnements Service Bus, comment créer un espace de noms pour contenir des rubriques/abonnements et comment envoyer et recevoir des messages à partir de ces rubriques/abonnements.</span><span class="sxs-lookup"><span data-stu-id="b40bc-141">[Service Bus Pub/Sub programming] - This explains the details of working with Service Bus Topics/Subscriptions, how to create a namespace to contain topics/subscriptions, how to send & receive messages from them.</span></span>
2. <span data-ttu-id="b40bc-142">[Notification Hubs : didacticiel Windows Universal] : cette rubrique explique comment configurer une application Windows Store et Notification Hubs pour vous inscrire et recevoir des notifications.</span><span class="sxs-lookup"><span data-stu-id="b40bc-142">[Notification Hubs - Windows Universal tutorial] - This explains how to set up a Windows Store app and use Notification Hubs to register and then receive notifications.</span></span>

### <a name="sample-code"></a><span data-ttu-id="b40bc-143">Exemple de code</span><span class="sxs-lookup"><span data-stu-id="b40bc-143">Sample code</span></span>
<span data-ttu-id="b40bc-144">L'exemple de code complet est disponible dans la page [Exemples de Notification Hub].</span><span class="sxs-lookup"><span data-stu-id="b40bc-144">The full sample code is available at [Notification Hub Samples].</span></span> <span data-ttu-id="b40bc-145">Il est divisé en trois composants :</span><span class="sxs-lookup"><span data-stu-id="b40bc-145">It is split into three components:</span></span>

1. <span data-ttu-id="b40bc-146">**EnterprisePushBackendSystem**</span><span class="sxs-lookup"><span data-stu-id="b40bc-146">**EnterprisePushBackendSystem**</span></span>
   
    <span data-ttu-id="b40bc-147">a.</span><span class="sxs-lookup"><span data-stu-id="b40bc-147">a.</span></span> <span data-ttu-id="b40bc-148">Ce projet utilise le package NuGet *WindowsAzure.ServiceBus*. Il repose sur la [programmation Service Bus Pub/Sub].</span><span class="sxs-lookup"><span data-stu-id="b40bc-148">This project uses the *WindowsAzure.ServiceBus* Nuget package and is  based on [Service Bus Pub/Sub programming].</span></span>
   
    <span data-ttu-id="b40bc-149">b.</span><span class="sxs-lookup"><span data-stu-id="b40bc-149">b.</span></span> <span data-ttu-id="b40bc-150">Il s’agit d’une console d’application C# simple pour simuler un système métier qui lance le message à remettre à l’application mobile.</span><span class="sxs-lookup"><span data-stu-id="b40bc-150">This is a simple C# console app to simulate an LoB system which initiates the message to be delivered to the mobile app.</span></span>
   
        static void Main(string[] args)
        {
            string connectionString =
                CloudConfigurationManager.GetSetting("Microsoft.ServiceBus.ConnectionString");
   
            // Create the topic where we will send notifications
            CreateTopic(connectionString);
   
            // Send message
            SendMessage(connectionString);
        }
   
    <span data-ttu-id="b40bc-151">c.</span><span class="sxs-lookup"><span data-stu-id="b40bc-151">c.</span></span> <span data-ttu-id="b40bc-152">`CreateTopic` permet de créer la rubrique Service Bus où nous enverrons les messages.</span><span class="sxs-lookup"><span data-stu-id="b40bc-152">`CreateTopic` is used to create the Service Bus topic where we will send messages.</span></span>
   
        public static void CreateTopic(string connectionString)
        {
            // Create the topic if it does not exist already
   
            var namespaceManager =
                NamespaceManager.CreateFromConnectionString(connectionString);
   
            if (!namespaceManager.TopicExists(sampleTopic))
            {
                namespaceManager.CreateTopic(sampleTopic);
            }
        }
   
    <span data-ttu-id="b40bc-153">d.</span><span class="sxs-lookup"><span data-stu-id="b40bc-153">d.</span></span> <span data-ttu-id="b40bc-154">`SendMessage` est utilisé pour envoyer les messages à cette rubrique Service Bus.</span><span class="sxs-lookup"><span data-stu-id="b40bc-154">`SendMessage` is used to send the messages to this Service Bus Topic.</span></span> <span data-ttu-id="b40bc-155">Dans le cadre de l’exemple, nous nous contentons d’envoyer périodiquement un ensemble de messages aléatoires à la rubrique.</span><span class="sxs-lookup"><span data-stu-id="b40bc-155">Here we are simply sending a set of random messages to the topic periodically for the purpose of the sample.</span></span> <span data-ttu-id="b40bc-156">Normalement, un système principal envoie des messages lorsqu’un événement se produit.</span><span class="sxs-lookup"><span data-stu-id="b40bc-156">Normally there will be a backend system which will send messages when an event occurs.</span></span>
   
        public static void SendMessage(string connectionString)
        {
            TopicClient client =
                TopicClient.CreateFromConnectionString(connectionString, sampleTopic);
   
            // Sends random messages every 10 seconds to the topic
            string[] messages =
            {
                "Employee Id '{0}' has joined.",
                "Employee Id '{0}' has left.",
                "Employee Id '{0}' has switched to a different team."
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
2. <span data-ttu-id="b40bc-157">**ReceiveAndSendNotification**</span><span class="sxs-lookup"><span data-stu-id="b40bc-157">**ReceiveAndSendNotification**</span></span>
   
    <span data-ttu-id="b40bc-158">a.</span><span class="sxs-lookup"><span data-stu-id="b40bc-158">a.</span></span> <span data-ttu-id="b40bc-159">Ce projet utilise les packages NuGet *WindowsAzure.ServiceBus* et *Microsoft.Web.WebJobs.Publish*. Il repose sur la [programmation Service Bus Pub/Sub].</span><span class="sxs-lookup"><span data-stu-id="b40bc-159">This project uses the *WindowsAzure.ServiceBus* and *Microsoft.Web.WebJobs.Publish* Nuget packages and is based on [Service Bus Pub/Sub programming].</span></span>
   
    <span data-ttu-id="b40bc-160">b.</span><span class="sxs-lookup"><span data-stu-id="b40bc-160">b.</span></span> <span data-ttu-id="b40bc-161">Il s'agit d'une autre application de console C# qui s'exécutera comme une [tâche web Azure] , étant donné qu'elle doit s'exécuter en continu pour écouter les messages des systèmes métiers/principaux.</span><span class="sxs-lookup"><span data-stu-id="b40bc-161">This is another C# console app which we will run as an [Azure WebJob] since it has to run continuously to listen for messages from the LoB/backend systems.</span></span> <span data-ttu-id="b40bc-162">Cela fera partie de votre serveur principal Mobile.</span><span class="sxs-lookup"><span data-stu-id="b40bc-162">This will be part of your Mobile backend.</span></span>
   
        static void Main(string[] args)
        {
            string connectionString =
                     CloudConfigurationManager.GetSetting("Microsoft.ServiceBus.ConnectionString");
   
            // Create the subscription which will receive messages
            CreateSubscription(connectionString);
   
            // Receive message
            ReceiveMessageAndSendNotification(connectionString);
        }
   
    <span data-ttu-id="b40bc-163">c.</span><span class="sxs-lookup"><span data-stu-id="b40bc-163">c.</span></span> <span data-ttu-id="b40bc-164">`CreateSubscription` permet de créer un abonnement Service Bus pour la rubrique où le système principal enverra les messages.</span><span class="sxs-lookup"><span data-stu-id="b40bc-164">`CreateSubscription` is used to create a Service Bus subscription for the topic where the backend system will send messages.</span></span> <span data-ttu-id="b40bc-165">Selon le scénario commercial, ce composant créera un ou plusieurs abonnements aux rubriques correspondantes (par exemple, certains peuvent recevoir les messages du système de RH, du système des Finances, etc.)</span><span class="sxs-lookup"><span data-stu-id="b40bc-165">Depending on the business scenario, this component will create one or more subscriptions to corresponding topics (e.g. some may be receiving messages from HR system, some from Finance system, and so on)</span></span>
   
        static void CreateSubscription(string connectionString)
        {
            // Create the subscription if it does not exist already
            var namespaceManager =
                NamespaceManager.CreateFromConnectionString(connectionString);
   
            if (!namespaceManager.SubscriptionExists(sampleTopic, sampleSubscription))
            {
                namespaceManager.CreateSubscription(sampleTopic, sampleSubscription);
            }
        }
   
    <span data-ttu-id="b40bc-166">d.</span><span class="sxs-lookup"><span data-stu-id="b40bc-166">d.</span></span> <span data-ttu-id="b40bc-167">ReceiveMessageAndSendNotification est utilisée pour lire le message dans la rubrique en utilisant son abonnement et, si la lecture réussit, pour créer une notification (dans notre exemple, une notification toast native Windows) à envoyer à l’application mobile à l’aide d’Azure Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="b40bc-167">ReceiveMessageAndSendNotification is used to read the message from the topic using its subscription and if the read is successful then craft a notification (in the sample scenario a Windows native toast notification) to be sent to the mobile application using Azure Notification Hubs.</span></span>
   
        static void ReceiveMessageAndSendNotification(string connectionString)
        {
            // Initialize the Notification Hub
            string hubConnectionString = CloudConfigurationManager.GetSetting
                    ("Microsoft.NotificationHub.ConnectionString");
            hub = NotificationHubClient.CreateClientFromConnectionString
                    (hubConnectionString, "enterprisepushservicehub");
   
            SubscriptionClient Client =
                SubscriptionClient.CreateFromConnectionString
                        (connectionString, sampleTopic, sampleSubscription);
   
            Client.Receive();
   
            // Continuously process messages received from the subscription
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
   
    <span data-ttu-id="b40bc-168">e.</span><span class="sxs-lookup"><span data-stu-id="b40bc-168">e.</span></span> <span data-ttu-id="b40bc-169">Pour publier ceci sous forme de **travail web**, cliquez avec le bouton droit sur la solution dans Visual Studio et sélectionnez **Publier en tant que travail web**</span><span class="sxs-lookup"><span data-stu-id="b40bc-169">For publishing this as a **WebJob**, right click on the solution in Visual Studio and select **Publish as WebJob**</span></span>
   
    ![][2]
   
    <span data-ttu-id="b40bc-170">f.</span><span class="sxs-lookup"><span data-stu-id="b40bc-170">f.</span></span> <span data-ttu-id="b40bc-171">Sélectionnez votre profil de publication et créez un site web Azure s’il n’existe pas déjà : il hébergera ce travail web. Quand vous disposez du site web, utilisez **Publier**.</span><span class="sxs-lookup"><span data-stu-id="b40bc-171">Select your publishing profile and create a new Azure WebSite if it doesnt exist already which will host this WebJob and once you have the WebSite then **Publish**.</span></span>
   
    ![][3]
   
    <span data-ttu-id="b40bc-172">g.</span><span class="sxs-lookup"><span data-stu-id="b40bc-172">g.</span></span> <span data-ttu-id="b40bc-173">Configurez le travail sur « Exécuter en continu ». Ainsi, quand vous vous connectez au [Portail Azure Classic], vous devriez voir ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="b40bc-173">Configure the job to be "Run Continuously" so that when you log in to the [Azure Classic Portal] you should see something like the following:</span></span>
   
    ![][4]
3. <span data-ttu-id="b40bc-174">**EnterprisePushMobileApp**</span><span class="sxs-lookup"><span data-stu-id="b40bc-174">**EnterprisePushMobileApp**</span></span>
   
    <span data-ttu-id="b40bc-175">a.</span><span class="sxs-lookup"><span data-stu-id="b40bc-175">a.</span></span> <span data-ttu-id="b40bc-176">Il s’agit d’une application Windows Store qui reçoit des notifications toast du WebJob en cours d’exécution dans le cadre de votre serveur principal Mobile et les affiche.</span><span class="sxs-lookup"><span data-stu-id="b40bc-176">This is a Windows Store application which will receive toast notifications from the WebJob running as part of your Mobile backend and display it.</span></span> <span data-ttu-id="b40bc-177">Elle repose sur [Notification Hubs : didacticiel Windows Universal].</span><span class="sxs-lookup"><span data-stu-id="b40bc-177">This is based on [Notification Hubs - Windows Universal tutorial].</span></span>  
   
    <span data-ttu-id="b40bc-178">b.</span><span class="sxs-lookup"><span data-stu-id="b40bc-178">b.</span></span> <span data-ttu-id="b40bc-179">Assurez-vous que la réception des notifications toast est activée dans votre application.</span><span class="sxs-lookup"><span data-stu-id="b40bc-179">Ensure that your application is enabled to receive toast notifications.</span></span>
   
    <span data-ttu-id="b40bc-180">c.</span><span class="sxs-lookup"><span data-stu-id="b40bc-180">c.</span></span> <span data-ttu-id="b40bc-181">Assurez-vous que le code d’inscription suivant de Notification Hubs est appelé au démarrage de l’application (après avoir remplacé *HubName* et *DefaultListenSharedAccessSignature*) :</span><span class="sxs-lookup"><span data-stu-id="b40bc-181">Ensure that the following Notification Hubs registration code is being called at the App start up (after replacing the *HubName* and *DefaultListenSharedAccessSignature*:</span></span>
   
        private async void InitNotificationsAsync()
        {
            var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();
   
            var hub = new NotificationHub("[HubName]", "[DefaultListenSharedAccessSignature]");
            var result = await hub.RegisterNativeAsync(channel.Uri);
   
            // Displays the registration ID so you know it was successful
            if (result.RegistrationId != null)
            {
                var dialog = new MessageDialog("Registration successful: " + result.RegistrationId);
                dialog.Commands.Add(new UICommand("OK"));
                await dialog.ShowAsync();
            }
        }

### <a name="running-sample"></a><span data-ttu-id="b40bc-182">Exemple d’exécution :</span><span class="sxs-lookup"><span data-stu-id="b40bc-182">Running sample:</span></span>
1. <span data-ttu-id="b40bc-183">Assurez-vous que votre WebJob est exécuté avec succès et planifié pour s’« Exécuter en continu ».</span><span class="sxs-lookup"><span data-stu-id="b40bc-183">Ensure that your WebJob is running successfully and scheduled to "Run Continuously".</span></span>
2. <span data-ttu-id="b40bc-184">Exécutez **EnterprisePushMobileApp** , qui lancera l'application Windows Store.</span><span class="sxs-lookup"><span data-stu-id="b40bc-184">Run the **EnterprisePushMobileApp** which will start the Windows Store app.</span></span>
3. <span data-ttu-id="b40bc-185">Exécutez l’application console **EnterprisePushBackendSystem** qui simule le serveur principal métier et enverra des messages. Vous devez voir apparaître des notifications toast similaires à celles-ci :</span><span class="sxs-lookup"><span data-stu-id="b40bc-185">Run the **EnterprisePushBackendSystem** console application which will simulate the LoB backend and will start sending messages and you should see toast notifications appearing like the following:</span></span>
   
    ![][5]
4. <span data-ttu-id="b40bc-186">Les messages ont été envoyés aux rubriques Service Bus qui ont été analysées par les abonnements Service Bus dans votre tâche Web.</span><span class="sxs-lookup"><span data-stu-id="b40bc-186">The messages were originally sent to Service Bus topics which was being monitored by Service Bus subscriptions in your Web Job.</span></span> <span data-ttu-id="b40bc-187">Lors de la réception d’un message, une notification a été créée et envoyée à l’application mobile.</span><span class="sxs-lookup"><span data-stu-id="b40bc-187">Once a message was received, a notification was created and sent to the mobile app.</span></span> <span data-ttu-id="b40bc-188">Vous pouvez consulter les journaux WebJob pour confirmer le traitement quand vous accédez au lien Journaux dans le [Portail Azure Classic] pour votre tâche Web :</span><span class="sxs-lookup"><span data-stu-id="b40bc-188">You can look through the WebJob logs to confirm the processing when you go to the Logs link in [Azure Classic Portal] for your Web Job:</span></span>
   
    ![][6]

<!-- Images -->
[1]: ./media/notification-hubs-enterprise-push-architecture/architecture.png
[2]: ./media/notification-hubs-enterprise-push-architecture/WebJobsContextMenu.png
[3]: ./media/notification-hubs-enterprise-push-architecture/PublishAsWebJob.png
[4]: ./media/notification-hubs-enterprise-push-architecture/WebJob.png
[5]: ./media/notification-hubs-enterprise-push-architecture/Notifications.png
[6]: ./media/notification-hubs-enterprise-push-architecture/WebJobsLog.png

<!-- Links -->
<span data-ttu-id="b40bc-189">[Exemples de Notification Hub]: https://github.com/Azure/azure-notificationhubs-samples</span><span class="sxs-lookup"><span data-stu-id="b40bc-189">[Notification Hub Samples]: https://github.com/Azure/azure-notificationhubs-samples</span></span>
<span data-ttu-id="b40bc-190">[Azure Mobile Service]: http://azure.microsoft.com/documentation/services/mobile-services/</span><span class="sxs-lookup"><span data-stu-id="b40bc-190">[Azure Mobile Service]: http://azure.microsoft.com/documentation/services/mobile-services/</span></span>
<span data-ttu-id="b40bc-191">[Azure Service Bus]: http://azure.microsoft.com/documentation/articles/fundamentals-service-bus-hybrid-solutions/</span><span class="sxs-lookup"><span data-stu-id="b40bc-191">[Azure Service Bus]: http://azure.microsoft.com/documentation/articles/fundamentals-service-bus-hybrid-solutions/</span></span>
<span data-ttu-id="b40bc-192">[programmation Service Bus Pub/Sub]: http://azure.microsoft.com/documentation/articles/service-bus-dotnet-how-to-use-topics-subscriptions/</span><span class="sxs-lookup"><span data-stu-id="b40bc-192">[Service Bus Pub/Sub programming]: http://azure.microsoft.com/documentation/articles/service-bus-dotnet-how-to-use-topics-subscriptions/</span></span>
<span data-ttu-id="b40bc-193">[tâche web Azure]: http://azure.microsoft.com/documentation/articles/web-sites-create-web-jobs/</span><span class="sxs-lookup"><span data-stu-id="b40bc-193">[Azure WebJob]: http://azure.microsoft.com/documentation/articles/web-sites-create-web-jobs/</span></span>
<span data-ttu-id="b40bc-194">[Notification Hubs : didacticiel Windows Universal]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-store-dotnet-get-started/</span><span class="sxs-lookup"><span data-stu-id="b40bc-194">[Notification Hubs - Windows Universal tutorial]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-store-dotnet-get-started/</span></span>
<span data-ttu-id="b40bc-195">[Portail Azure Classic]: https://manage.windowsazure.com/</span><span class="sxs-lookup"><span data-stu-id="b40bc-195">[Azure Classic Portal]: https://manage.windowsazure.com/</span></span>
