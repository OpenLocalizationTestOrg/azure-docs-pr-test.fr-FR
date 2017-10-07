---
title: aaaAzure Notification Hubs Secure Push.
description: "Découvrez comment toosend sécurisée des notifications push dans Azure. Exemples de code écrits en c# à l’aide des API .NET de hello."
documentationcenter: windows
author: ysxu
manager: erikre
editor: 
services: notification-hubs
ms.assetid: 5aef50f4-80b3-460e-a9a7-7435001273bd
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: windows
ms.devlang: dotnet
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: b6fe16c96d28d75ff698278409fb012472ba6396
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-notification-hubs-secure-push"></a>Notifications Push sécurisées avec Azure Notification Hubs
> [!div class="op_single_selector"]
> * [Windows Universal](notification-hubs-aspnet-backend-windows-dotnet-wns-secure-push-notification.md)
> * [iOS](notification-hubs-aspnet-backend-ios-push-apple-apns-secure-notification.md)
> * [Android](notification-hubs-aspnet-backend-android-secure-google-gcm-push-notification.md)
> 
> 

## <a name="overview"></a>Vue d'ensemble
Prise en charge des notifications push dans Microsoft Azure vous permet de tooaccess une infrastructure push facile à utiliser, multiplateforme, à grande échelle, ce qui simplifie considérablement l’implémentation hello de notifications push pour les applications consommateur et d’entreprise mobile plateformes.

En raison de contraintes de sécurité ou tooregulatory, une application peut parfois tooinclude quelque chose dans la notification hello ne peut pas être transmis au moyen de l’infrastructure de notification push standard hello. Ce didacticiel explique comment tooachieve hello la même expérience en envoyant des informations sensibles via une connexion sécurisée, authentifiée entre le périphérique de hello client et serveur principal d’application hello.

À un niveau élevé, les flux hello sont comme suit :

1. Hello serveur principal d’application :
   * stocke la charge utile sécurisée dans la base de données principale ;
   * Envoie un ID hello de cet appareil toohello de notification (aucune information sécurisée est envoyée).
2. application Hello sur périphérique hello, lors de la réception de notification de hello :
   * Appareil de Hello contacte hello principal demande hello sécurisé charge utile.
   * application Hello peut afficher la charge utile de hello en tant que notification sur l’appareil de hello.

Il est important de toonote que Bonjour précédant le flux (et, dans ce didacticiel), nous supposons que cet appareil hello stocke un jeton d’authentification dans le stockage local, une fois hello utilisateur se connecte. Cela garantit une expérience entièrement transparente, comme périphérique de hello peut récupérer de données de la notification hello sécurisé à l’aide de ce jeton. Si votre application n’enregistre pas les jetons d’authentification sur l’appareil de hello, ou si ces jetons peuvent avoir expiré, hello application d’appareil, à la réception de notification de hello doit afficher une notification générique invitant hello utilisateur toolaunch hello application. application Hello puis authentifie l’utilisateur de hello et montre la charge utile de notification hello.

Ce didacticiel de Push de sécuriser montre comment toosend une notification push en toute sécurité. didacticiel de Hello s’appuie sur hello [avertir les utilisateurs](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md) (didacticiel), donc vous devez effectuer les étapes de hello tout d’abord dans ce didacticiel.

> [!NOTE]
> Ce didacticiel part du principe que vous avez créé et configuré votre hub de notification comme décrit dans [Prise en main de Notification Hubs (Windows Store)](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md).
> Notez également que Windows Phone 8.1 nécessite des informations d’identification Windows (pas Windows Phone) et que les tâches en arrière-plan ne fonctionnent pas sur Windows Phone 8.0 ou Silverlight 8.1. Pour les applications du Windows Store, vous pouvez recevoir des notifications via une tâche en arrière-plan uniquement si l’application hello est activé d’écran de verrouillage (cliquez sur la case à cocher hello Bonjour Appmanifest).
> 
> 

[!INCLUDE [notification-hubs-aspnet-backend-securepush](../../includes/notification-hubs-aspnet-backend-securepush.md)]

## <a name="modify-hello-windows-phone-project"></a>Modifier hello projet du Windows Phone
1. Bonjour **NotifyUserWindowsPhone** de projet, ajoutez hello suivant la tâche en arrière-plan de la poussée du code tooApp.xaml.cs tooregister hello. Ajouter hello suivant la ligne de code à fin hello Hello `OnLaunched()` méthode :
   
        RegisterBackgroundTask();
2. Toujours dans App.xaml.cs, ajoutez hello suivant code immédiatement après hello `OnLaunched()` méthode :
   
        private async void RegisterBackgroundTask()
        {
            if (!Windows.ApplicationModel.Background.BackgroundTaskRegistration.AllTasks.Any(i => i.Value.Name == "PushBackgroundTask"))
            {
                var result = await BackgroundExecutionManager.RequestAccessAsync();
                var builder = new BackgroundTaskBuilder();
   
                builder.Name = "PushBackgroundTask";
                builder.TaskEntryPoint = typeof(PushBackgroundComponent.PushBackgroundTask).FullName;
                builder.SetTrigger(new Windows.ApplicationModel.Background.PushNotificationTrigger());
                BackgroundTaskRegistration task = builder.Register();
            }
        }
3. Ajoutez hello suit `using` instructions haut hello du fichier de App.xaml.cs hello :
   
        using Windows.Networking.PushNotifications;
        using Windows.ApplicationModel.Background;
4. À partir de hello **fichier** menu dans Visual Studio, cliquez sur **Enregistrer tout**.

## <a name="create-hello-push-background-component"></a>Créer hello pousser le composant en arrière-plan
étape suivante de Hello est le composant toocreate hello par émission de données en arrière-plan.

1. Dans l’Explorateur de solutions, cliquez sur nœud de niveau supérieur hello de solution de hello (**Solution SecurePush** dans ce cas), puis cliquez sur **ajouter**, puis cliquez sur **nouveau projet**.
2. Développez **Applications du Windows Store** et cliquez sur **Applications Windows Phone**, puis sur **Composant Windows Runtime (Windows Phone)**. Projet de hello nom **PushBackgroundComponent**, puis cliquez sur **OK** projet hello de toocreate.
   
    ![][12]
3. Dans l’Explorateur de solutions, cliquez sur hello **PushBackgroundComponent (8.1 de Windows Phone)** de projet, puis cliquez sur **ajouter**, puis cliquez sur **classe**. Nommez la nouvelle classe de hello **PushBackgroundTask.cs**. Cliquez sur **ajouter** classe hello de toogenerate.
4. Remplacez hello tout contenu de hello **PushBackgroundComponent** définition d’espace de noms avec hello suivant de code, en remplaçant les espaces réservés de hello `{back-end endpoint}` avec point de terminaison principal hello obtenue lors du déploiement de votre principal :
   
        public sealed class Notification
            {
                public int Id { get; set; }
                public string Payload { get; set; }
                public bool Read { get; set; }
            }
   
            public sealed class PushBackgroundTask : IBackgroundTask
            {
                private string GET_URL = "{back-end endpoint}/api/notifications/";
   
                async void IBackgroundTask.Run(IBackgroundTaskInstance taskInstance)
                {
                    // Store hello content received from hello notification so it can be retrieved from hello UI.
                    RawNotification raw = (RawNotification)taskInstance.TriggerDetails;
                    var notificationId = raw.Content;
   
                    // retrieve content
                    BackgroundTaskDeferral deferral = taskInstance.GetDeferral();
                    var httpClient = new HttpClient();
                    var settings = ApplicationData.Current.LocalSettings.Values;
                    httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Basic", (string)settings["AuthenticationToken"]);
   
                    var notificationString = await httpClient.GetStringAsync(GET_URL + notificationId);
   
                    var notification = JsonConvert.DeserializeObject<Notification>(notificationString);
   
                    ShowToast(notification);
   
                    deferral.Complete();
                }
   
                private void ShowToast(Notification notification)
                {
                    ToastTemplateType toastTemplate = ToastTemplateType.ToastText01;
                    XmlDocument toastXml = ToastNotificationManager.GetTemplateContent(toastTemplate);
                    XmlNodeList toastTextElements = toastXml.GetElementsByTagName("text");
                    toastTextElements[0].AppendChild(toastXml.CreateTextNode(notification.Payload));
                    ToastNotification toast = new ToastNotification(toastXml);
                    ToastNotificationManager.CreateToastNotifier().Show(toast);
                }
            }
5. Dans l’Explorateur de solutions, cliquez sur hello **PushBackgroundComponent (8.1 de Windows Phone)** de projet, puis cliquez sur **gérer les Packages NuGet**.
6. Dans la partie gauche hello, cliquez sur **Online**.
7. Bonjour **recherche** , tapez **Http Client**.
8. Dans la liste des résultats hello, cliquez sur **Microsoft HTTP Client Libraries**, puis cliquez sur **installer**. Terminer l’installation de hello.
9. Dans hello NuGet **recherche** , tapez **Json.net**. Installer hello **Json.NET** package, puis sur fenêtre du Gestionnaire de Package NuGet hello fermer.
10. Ajoutez hello suivant `using` instructions haut hello hello **PushBackgroundTask.cs** fichier :
    
        using Windows.ApplicationModel.Background;
        using Windows.Networking.PushNotifications;
        using System.Net.Http;
        using Windows.Storage;
        using System.Net.Http.Headers;
        using Newtonsoft.Json;
        using Windows.UI.Notifications;
        using Windows.Data.Xml.Dom;
11. Dans l’Explorateur de solutions, Bonjour **NotifyUserWindowsPhone (8.1 de Windows Phone)** de projet, cliquez sur **références**, puis cliquez sur **ajouter une référence...** . Dans la boîte de dialogue Gestionnaire de références hello, hello case à cocher ensuite trop**PushBackgroundComponent**, puis cliquez sur **OK**.
12. Dans l’Explorateur de solutions, double-cliquez sur **Package.appxmanifest** Bonjour **NotifyUserWindowsPhone (8.1 de Windows Phone)** projet. Sous **Notifications**, définissez **compatible Toast** trop**Oui**.
    
    ![][3]
13. Toujours dans **Package.appxmanifest**, cliquez sur hello **déclarations** menu haut hello. Bonjour **déclarations disponibles** liste déroulante, cliquez sur **les tâches en arrière-plan**, puis cliquez sur **ajouter**.
14. Dans **Package.appxmanifest**, sous **Propriétés**, cochez **Notification Push**.
15. Dans **Package.appxmanifest**, sous **paramètres de l’application**, type **PushBackgroundComponent.PushBackgroundTask** Bonjour **Point d’entrée** champ.
    
    ![][13]
16. À partir de hello **fichier** menu, cliquez sur **Enregistrer tout**.

## <a name="run-hello-application"></a>Exécutez hello Application
toorun hello application, procédez comme hello suivant :

1. Dans Visual Studio, exécutez hello **AppBackend** application d’API Web. Une page web ASP.NET s'affiche.
2. Dans Visual Studio, exécutez hello **NotifyUserWindowsPhone (8.1 de Windows Phone)** application du Windows Phone. émulateur Windows Phone de Hello s’exécute et charge application hello automatiquement.
3. Bonjour **NotifyUserWindowsPhone** application d’interface utilisateur, entrez un nom d’utilisateur et un mot de passe. Il peuvent être n’importe quelle chaîne, mais ils doivent être hello la même valeur.
4. Bonjour **NotifyUserWindowsPhone** application d’interface utilisateur, cliquez sur **connectez-vous et inscrivez**. Cliquez ensuite sur **Send push**.

[3]: ./media/notification-hubs-aspnet-backend-windows-dotnet-secure-push/notification-hubs-secure-push3.png
[12]: ./media/notification-hubs-aspnet-backend-windows-dotnet-secure-push/notification-hubs-secure-push12.png
[13]: ./media/notification-hubs-aspnet-backend-windows-dotnet-secure-push/notification-hubs-secure-push13.png
