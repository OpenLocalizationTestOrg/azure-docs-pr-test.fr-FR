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
# <a name="enterprise-push-architectural-guidance"></a>Guide architectural des notifications Push d’entreprise
Aujourd'hui, les entreprises sont progressivement mobiles, la création d’applications mobiles pour les utilisateurs finals (externe) ou des employés de hello (internes). Ils ont des systèmes principaux existant en place qu’il s’agisse de grands systèmes ou certaines applications métier qui doivent être intégrées dans hello architecture de l’application mobile. Ce guide aborderons toodo la meilleure façon de cette intégration recommander des scénarios de toocommon solution possible.

Une exigence fréquente est pour l’envoi des utilisateurs de toohello de notification via leurs applications mobiles par émission de données lorsqu’un événement d’intérêt se produit dans les systèmes back-end hello. Par exemple, un client de la banque qui a des application bancaire de la banque hello sur son iPhone veut toobe notifié lorsqu’un débit est fait au-dessus d’un certain montant à partir de son compte ou un intranet où un employé à partir du service finance disposant d’une application de l’approbation de budget sur son Windows Phone veut toobe averti lorsqu’il reçoit une demande d’approbation.

Hello bancaires ou le traitement de l’approbation est probablement toobe effectuée dans un système principal qui doit lancer un utilisateur de toohello par émission de données. Il peut y avoir plusieurs principaux de ce systèmes, ce qui doivent générer tous les hello même type de push de tooimplement logique lorsqu’un événement déclenche une notification. complexité Hello ici se trouve dans l’intégration de plusieurs systèmes principaux ainsi que d’un système de transmission unique où hello les utilisateurs finaux peuvent se sont abonnées toodifferent notifications et il peut même être plusieurs applications mobiles, par exemple dans les cas de hello d’intranet des applications mobiles où une application mobile veulent tooreceive des notifications à partir de plusieurs de ces systèmes de serveur principal. les systèmes back-end Hello ne connaissez pas ou n’a besoin tooknow de sémantique/technologie push d’une solution courante ici traditionnellement toointroduce un composant qui interroge les systèmes principaux de hello pour tous les événements d’intérêt et est chargé d’envoyer des messages de type push hello toohello client.
Ici, nous aborderons une solution plus efficace à l’aide d’Azure Service Bus - modèle de rubrique / d’abonnement qui réduit la complexité de hello lors de la solution de hello évolutive.

Voici architecture générale d’hello de solution de hello (généralisée avec plusieurs applications mobiles, mais également applicables lorsqu’il y a qu’une seule application mobile)

## <a name="architecture"></a>Architecture
![][1]

information de clé Hello dans ce diagramme architectural est Bus des services Azure qui fournit un modèle de programmation les rubriques/abonnements (au plus [programmation de Service Bus Pub/Sub]). récepteur de Hello, qui est dans ce cas, les principaux de Mobile hello (généralement [Service Mobile Azure], qui va déclencher un push toohello des applications mobiles) ne pas recevoir des messages directement à partir de systèmes principaux de hello, mais au lieu de cela, nous avons un couche d’abstraction intermédiaire fournie par [Azure Service Bus] permet aux messages de tooreceive backend mobile à partir d’un ou plusieurs systèmes back-end. Une rubrique Service Bus doit toobe créé pour chacune des systèmes principaux hello par exemple, compte, h, Finance qui sont essentiellement « rubriques » d’intérêt qui va lancer toobe de messages envoyé en tant que notification push. les systèmes back-end Hello enverra les messages des rubriques de toothese. Un service principal Mobile peuvent s’abonner tooone ou plusieurs de ces rubriques en créant un abonnement Service Bus. Cela donnera droit hello backend mobile tooreceive une notification à partir de son système principal correspondant hello. Backend mobile continue toolisten pour les messages sur leurs abonnements et dès qu’un message arrive, il reprend et l’envoie en tant que le hub de notification tooits de notification. Concentrateurs de notification puis remet finalement application mobile du toohello message hello. Composants clés de hello toosummarize, nous avons :

1. les systèmes principaux (systèmes métiers/hérités)
   * Crée une rubrique Service Bus
   * Envoie un message
2. Serveur principal mobile
   * Crée l’abonnement au service
   * Reçoit le message (du système principal)
   * Envoie la notification des tooclients (via le concentrateur de Notification Azure)
3. Application mobile
   * Reçoit et affiche une notification

### <a name="benefits"></a>Avantages :
1. Hello découplage entre l’expéditeur (systèmes back-end) et du récepteur de hello (application/service mobile via un concentrateur de Notification) permet à des systèmes back-end supplémentaires en cours d’intégration en apportant les modifications.
2. Cela facilite également le scénario hello dans plusieurs applications mobiles étant en mesure de tooreceive des événements à partir d’un ou plusieurs systèmes back-end.  

## <a name="sample"></a>Exemple :
### <a name="prerequisites"></a>Composants requis
Vous devez effectuer hello suivant toofamiliarize didacticiels avec les concepts de hello, ainsi que les étapes de création et de configuration courantes :

1. [programmation de Service Bus Pub/Sub] -cette rubrique explique comment détails hello de travailler avec des rubriques/abonnements Service Bus, toocreate un espace de noms toocontain rubriques/abonnements, comment toosend & recevoir des messages à partir de celles-ci.
2. [Concentrateurs de notification - didacticiel Windows universel] -ce qui explique comment tooset configurer une application du Windows Store et utiliser Notification Hubs tooregister et recevoir des notifications.

### <a name="sample-code"></a>Exemple de code
Hello exemple de code complet est disponible à l’adresse [exemples de concentrateur de Notification]. Il est divisé en trois composants :

1. **EnterprisePushBackendSystem**
   
    a. Ce projet utilise hello *WindowsAzure.ServiceBus* package Nuget et est basée sur [programmation de Service Bus Pub/Sub].
   
    b. Il s’agit d’un simple c# console application toosimulate un système métier qui lance hello toobe de message remis toohello des applications mobiles.
   
        static void Main(string[] args)
        {
            string connectionString =
                CloudConfigurationManager.GetSetting("Microsoft.ServiceBus.ConnectionString");
   
            // Create hello topic where we will send notifications
            CreateTopic(connectionString);
   
            // Send message
            SendMessage(connectionString);
        }
   
    c. `CreateTopic`est la rubrique Service Bus toocreate utilisé hello où nous enverra les messages.
   
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
   
    d. `SendMessage`est utilisé toosend hello messages toothis rubrique Service Bus. Ici, nous envoyons simplement un ensemble de la rubrique de toohello des messages aléatoires régulièrement fins hello de l’exemple hello. Normalement, un système principal envoie des messages lorsqu’un événement se produit.
   
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
2. **ReceiveAndSendNotification**
   
    a. Ce projet utilise hello *WindowsAzure.ServiceBus* et *Microsoft.Web.WebJobs.Publish* Nuget packages et est basée sur [programmation de Service Bus Pub/Sub].
   
    b. Il s’agit d’une autre application de console c# lequel nous allons exécuter en tant qu’un [la tâche Web Azure] , car il a toorun en permanence toolisten pour les messages à partir des systèmes métier/principal de hello. Cela fera partie de votre serveur principal Mobile.
   
        static void Main(string[] args)
        {
            string connectionString =
                     CloudConfigurationManager.GetSetting("Microsoft.ServiceBus.ConnectionString");
   
            // Create hello subscription which will receive messages
            CreateSubscription(connectionString);
   
            // Receive message
            ReceiveMessageAndSendNotification(connectionString);
        }
   
    c. `CreateSubscription`est un abonnement de Bus de Service pour la rubrique de hello toocreate utilisé où son système principal hello enverra les messages. Selon le scénario d’entreprise hello, ce composant créera un ou plusieurs abonnements rubriques toocorresponding (par exemple, certaines peuvent recevoir les messages à partir du système des ressources humaines, certains à partir de système de Finance et ainsi de suite)
   
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
   
    d. ReceiveMessageAndSendNotification est le message de type hello tooread utilisé à partir de la rubrique hello à l’aide de son abonnement et si hello lecture réussit puis élaborer une toohello de toobe envoyé de notification (dans l’exemple de scénario hello une notification toast native de Windows) mobile application à l’aide de Azure Notification Hubs.
   
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
   
    e. Pour la publication en tant qu’un **WebJob**, cliquez avec le bouton droit sur la solution hello dans Visual Studio et sélectionnez **publier en tant que tâche Web**
   
    ![][2]
   
    f. Sélectionnez votre profil de publication et créer un nouveau site Web de Azure s’il n’existe déjà qui va héberger cette tâche Web et une fois que du site Web hello puis **publier**.
   
    ![][3]
   
    g. Configurer hello toobe de tâche « Exécuter en continu » de sorte que lorsque vous ouvrez une session dans toohello [portail classique Azure] vous devez voir quelque chose comme hello ci-après :
   
    ![][4]
3. **EnterprisePushMobileApp**
   
    a. Il s’agit d’une application du Windows Store qui reçoivent des notifications toast à partir de l’exécution de la tâche Web hello dans le cadre de votre serveur principal Mobile et l’afficher. Elle repose sur [Concentrateurs de notification - didacticiel Windows universel].  
   
    b. Assurez-vous que votre application est activé tooreceive des notifications de toast.
   
    c. Vérifiez que hello suivant le code d’enregistrement de concentrateurs de Notification est appelée à hello application démarrent (après le remplacement hello *HubName* et *DefaultListenSharedAccessSignature*:
   
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

### <a name="running-sample"></a>Exemple d’exécution :
1. Assurez-vous que votre tâche Web est en cours d’exécution avec succès et planifié trop « exécuter en continu ».
2. Exécutez hello **EnterprisePushMobileApp** démarrer hello application du Windows Store.
3. Exécutez hello **EnterprisePushBackendSystem** application console qui simule hello LoB principal et commencer l’envoi des messages et des notifications de toast apparaissant hello suivante doit s’afficher :
   
    ![][5]
4. messages Hello ont été envoyés à l’origine des rubriques de Bus tooService qui était en cours d’analyse par abonnements Service Bus dans votre projet Web. Une fois qu’un message a été reçu, une notification a été créée et envoyée toohello des applications mobiles. Vous pouvez consulter hello ouvre une tâche Web tooconfirm hello traitement lorsque vous passez toohello lien de journaux dans [portail classique Azure] pour votre tâche Web :
   
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
