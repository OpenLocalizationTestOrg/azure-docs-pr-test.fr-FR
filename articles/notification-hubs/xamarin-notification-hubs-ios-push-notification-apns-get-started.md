---
title: aaaiOS des Notifications Push avec Notification Hubs pour les applications Xamarin | Documents Microsoft
description: "Dans ce didacticiel, vous découvrez comment toouse Azure Notification Hubs toosend push application iOS de notifications tooa Xamarin."
services: notification-hubs
keywords: notifications push iOS, messages push, notifications push, envoi de messages
documentationcenter: xamarin
author: ysxu
manager: erikre
editor: 
ms.assetid: 4d4dfd42-c5a5-4360-9d70-7812f96924d2
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-ios
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 8db60338047dd53074b4d3d4bb127aa6d9f13a25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="ios-push-notifications-with-notification-hubs-for-xamarin-apps"></a>Notifications Push iOS à l’aide des hubs de notification pour applications Xamarin
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a>Vue d'ensemble
> [!IMPORTANT]
> toocomplete ce didacticiel, vous devez disposer d’un compte Azure actif. Si vous ne possédez pas de compte, vous pouvez créer un compte d'évaluation gratuit en quelques minutes. Pour plus d'informations, consultez la page [Version d'évaluation gratuite d'Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fpartner-xamarin-notification-hubs-ios-get-started).
> 
> 

Ce didacticiel vous montre comment toouse Azure Notification Hubs toosend push application iOS de tooan des notifications.
Vous allez créer une application Xamarin.iOS vide qui reçoit des notifications push à l’aide de hello [services de notifications Push Apple (APN)](https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/APNSOverview.html). Lorsque vous avez terminé, vous serez en mesure de toouse votre toobroadcast de concentrateur de notification push des appareils de hello notifications tooall votre application en cours d’exécution. Hello code terminé est disponible dans hello [NotificationHubs application] [ GitHub] exemple.

Ce didacticiel illustre un scénario diffusion de messages hello simple push avec Notification Hubs.

## <a name="prerequisites"></a>Composants requis
Ce didacticiel requiert hello qui suit :

* [Xcode 6.0][Install Xcode]
* Un appareil compatible iOS 7.0 (ou version ultérieure)
* Un abonnement au programme pour développeurs iOS
* [Xamarin Studio]
  
  > [!NOTE]
  > En raison de la configuration requise pour les notifications de push iOS, vous devez déployer et tester l’application d’exemple hello sur un appareil physique iOS (iPhone ou iPad) au lieu de dans le simulateur de hello.
  > 
  > 

Vous devez suivre ce didacticiel avant de pouvoir suivre tous les autres didacticiels dédiés aux hubs de notification pour applications Xamarin iOS.

[!INCLUDE [Notification Hubs Enable Apple Push Notifications](../../includes/notification-hubs-enable-apple-push-notifications.md)]

## <a name="configure-your-notification-hub"></a>Configuration de votre hub de notification
Cette section présente la création d’un concentrateur de notification et de configuration de l’authentification avec APNS à l’aide de hello **.p12** : certificat push que vous avez créé. Si vous voulez toouse un concentrateur de notification que vous avez déjà créé, vous pouvez ignorer toostep 5.

[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="7">

<li>

<p>Comme nous voulons tooconfigure hello APNS connexion, hello portail Azure, ouvrir les paramètres de Notification Hub, ande cliquez sur <b>Notification Services</b>, puis cliquez sur hello <b>Apple (APN)</b> élément de liste de hello. Une fois terminé, cliquez sur <b>télécharger un certificat</b> et sélectionnez hello <b>.p12</b> certificat que vous avez exporté précédemment, ainsi que d’un mot de passe hello pour les certificats hello.</p>

<p>Assurez-vous que tooselect <b>Sandbox</b> mode étant donné que vous allez envoyer par émission de données des messages dans un environnement de développement. Utilisez uniquement hello <b>Production</b> paramètre si vous souhaitez toousers de notifications push toosend qui ont déjà acheté votre application à partir du magasin de hello.</p>
</li>
</ol>
&emsp;&emsp;![](./media/notification-hubs-ios-get-started/notification-hubs-apns.png)

&emsp;&emsp;![](./media/notification-hubs-ios-get-started/notification-hubs-sandbox.png)

Votre concentrateur de notification est maintenant configuré toowork avec APNS, et vous avez tooregister de chaînes de connexion hello votre application et envoyez des notifications push.

## <a name="connect-your-app-toohello-notification-hub"></a>Se connecter à votre hub de notification d’application toohello
#### <a name="create-a-new-project"></a>Création d'un projet
1. Dans Xamarin Studio, créez un projet iOS et sélectionnez hello **API unifiée** > **Application vue unique** modèle.
   
     ![Xamarin Studio - Sélectionner le type d’application][31]
2. Ajouter un composant de messagerie Azure toohello référence. Bonjour vue de solutions, cliquez sur hello **composants** dossier de votre projet et choisissez **obtenir plusieurs composants**. Recherchez hello **messagerie Azure** composant et ajoutez le projet tooyour hello.
3. Dans **AppDelegate.cs**, ajoutez hello qui suit à l’aide d’instruction :
   
        using WindowsAzure.Messaging;
4. Déclarez une instance de **SBNotificationHub**:
   
        private SBNotificationHub Hub { get; set; }
5. Créer un **Constants.cs** classe avec hello suivant variables :
   
        // Azure app-specific connection string and hub path
        public const string ConnectionString = "<Azure connection string>";
        public const string NotificationHubPath = "<Azure hub path>";
6. Dans **AppDelegate.cs**, mettre à jour **FinishedLaunching()** suivant de hello toomatch :
   
        public override bool FinishedLaunching(UIApplication application, NSDictionary launchOptions)
        {
            if (UIDevice.CurrentDevice.CheckSystemVersion (8, 0)) {
                var pushSettings = UIUserNotificationSettings.GetSettingsForTypes (
                       UIUserNotificationType.Alert | UIUserNotificationType.Badge | UIUserNotificationType.Sound,
                       new NSSet ());
   
                UIApplication.SharedApplication.RegisterUserNotificationSettings (pushSettings);
                UIApplication.SharedApplication.RegisterForRemoteNotifications ();
            } else {
                UIRemoteNotificationType notificationTypes = UIRemoteNotificationType.Alert | UIRemoteNotificationType.Badge | UIRemoteNotificationType.Sound;
                UIApplication.SharedApplication.RegisterForRemoteNotificationTypes (notificationTypes);
            }
   
            return true;
        }
7. Remplacer hello **RegisteredForRemoteNotifications()** méthode dans **AppDelegate.cs**:
   
        public override void RegisteredForRemoteNotifications(UIApplication application, NSData deviceToken)
        {
            Hub = new SBNotificationHub(Constants.ConnectionString, Constants.NotificationHubPath);
   
            Hub.UnregisterAllAsync (deviceToken, (error) => {
                if (error != null)
                {
                    Console.WriteLine("Error calling Unregister: {0}", error.ToString());
                    return;
                }
   
                NSSet tags = null; // create tags if you want
                Hub.RegisterNativeAsync(deviceToken, tags, (errorCallback) => {
                    if (errorCallback != null)
                        Console.WriteLine("RegisterNativeAsync error: " + errorCallback.ToString());
                });
            });
        }
8. Remplacer hello **ReceivedRemoteNotification()** méthode dans **AppDelegate.cs**:
   
        public override void ReceivedRemoteNotification(UIApplication application, NSDictionary userInfo)
        {
            ProcessNotification(userInfo, false);
        }
9. Créer hello **ProcessNotification()** méthode dans **AppDelegate.cs**:
   
        void ProcessNotification(NSDictionary options, bool fromFinishedLaunching)
        {
            // Check toosee if hello dictionary has hello aps key.  This is hello notification payload you would have sent
            if (null != options && options.ContainsKey(new NSString("aps")))
            {
                //Get hello aps dictionary
                NSDictionary aps = options.ObjectForKey(new NSString("aps")) as NSDictionary;
   
                string alert = string.Empty;
   
                //Extract hello alert text
                // NOTE: If you're using hello simple alert by just specifying
                // "  aps:{alert:"alert msg here"}  ", this will work fine.
                // But if you're using a complex alert with Localization keys, etc.,
                // your "alert" object from hello aps dictionary will be another NSDictionary.
                // Basically hello JSON gets dumped right into a NSDictionary,
                // so keep that in mind.
                if (aps.ContainsKey(new NSString("alert")))
                    alert = (aps [new NSString("alert")] as NSString).ToString();
   
                //If this came from hello ReceivedRemoteNotification while hello app was running,
                // we of course need toomanually process things like hello sound, badge, and alert.
                if (!fromFinishedLaunching)
                {
                    //Manually show an alert
                    if (!string.IsNullOrEmpty(alert))
                    {
                        UIAlertView avAlert = new UIAlertView("Notification", alert, null, "OK", null);
                        avAlert.Show();
                    }
                }
            }
        }
   
   > [!NOTE]
   > Vous pouvez choisir toooverride **FailedToRegisterForRemoteNotifications()** toohandle cas d’aucune connexion réseau. Cela est particulièrement important lorsque les utilisateur hello peuvent démarrer votre application en mode hors connexion (par exemple, avion) et que vous souhaitez push toohandle application tooyour spécifique de scénarios de messagerie.
   > 
   > 
10. Exécutez l’application hello sur votre appareil.

## <a name="sending-push-notifications"></a>Envoi de notifications Push
Vous pouvez tester de recevoir des notifications push dans votre application en envoyant des notifications Bonjour [Azure Portal] via hello **envoi Test** fonctionnalité Bonjour **dépannage** ensemble d’outils, à droite dans la page hello notification hub, comme indiqué dans l’écran hello ci-dessous.

![](./media/notification-hubs-ios-get-started/notification-hubs-test-send.png)

Les notifications Push sont normalement envoyées via un service principal tel que Mobile Services ou ASP.NET à l’aide d’une bibliothèque compatible. Vous pouvez également utiliser hello API REST directement toosend push des messages si une bibliothèque n’est pas disponible dans votre scénario. 

Dans ce didacticiel, nous plus de simplicité et simplement montrent le test de votre application cliente en envoyant des notifications à l’aide de hello SDK .NET pour les concentrateurs de notification dans une application console à la place d’un service principal. Nous vous recommandons de hello [utiliser Notification Hubs toopush notifications toousers](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) didacticiel en tant qu’étape suivante de hello pour envoyer des notifications à partir d’un serveur principal d’ASP.NET. Toutefois, hello méthodes suivantes peut servir pour envoyer des notifications :

* **Interface REST**: vous pouvez prendre en charge les notifications push sur toute plateforme principale à l’aide de hello [interface REST](http://msdn.microsoft.com/library/windowsazure/dn223264.aspx).
* **Kit de développement logiciel Microsoft Azure Notification Hubs .NET**: Bonjour Gestionnaire de Package Nuget pour Visual Studio, exécutez [Install-Package Microsoft.Azure.NotificationHubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).
* **Node.js** : [comment toouse concentrateurs de Notification à partir de Node.js](notification-hubs-nodejs-push-notification-tutorial.md).

**Applications mobiles**: pour obtenir un exemple de notifications toosend à partir d’un serveur principal Azure App Service Mobile Apps intégré avec Notification Hubs, consultez [ajouter push notifications tooyour application mobile](../app-service-mobile/app-service-mobile-ios-get-started-push.md).

* **Java / PHP**: pour obtenir un exemple de comment toosend les notifications push à l’aide de hello API REST, consultez « Comment toouse concentrateurs de Notification à partir de Java/PHP » ([Java](notification-hubs-java-push-notification-tutorial.md) | [PHP](notification-hubs-php-push-notification-tutorial.md)).

#### <a name="optional-send-push-notifications-from-a-net-console-app"></a>(Facultatif) Envoi de notifications Push à partir d’une application de console .NET
Dans cette section, nous allons envoyer des notifications Push à l’aide d’une simple application de console .NET. Pour des raisons de hello de cet exemple, nous changeons environnement de développement Windows tooa qui a déjà installé Visual Studio.

1. Dans Visual Studio, créez une application de console Visual C# :
   
       ![Visual Studio - Create a new console application][213]
2. Dans Visual Studio, cliquez successivement sur **Outils**, **Gestionnaire de package NuGet** et **Console du gestionnaire de package**.
   
    console du Gestionnaire de package Hello doit apparaître bas toohello ancrée de votre espace de travail de Visual Studio.
3. Dans la fenêtre de Console du Gestionnaire de Package de hello, définissez hello **projet par défaut** tooyour nouveau projet d’application console et puis, dans la fenêtre de console hello, exécutez hello de commande suivante :
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    Cette opération ajoute une référence de toohello Azure Notification Hubs SDK à l’aide de hello <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">package NuGet de concentrateurs Microsoft.Azure.Notification</a>.
   
    ![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-package-manager.png)
4. Ouvrez hello `Program.cs` et ajoutez les suivant hello `using` instruction, garantissant que nous pouvons utiliser les classes Azure et des fonctions dans votre classe principale :
   
        using Microsoft.Azure.NotificationHubs;
5. Dans votre `Program` de classe, ajoutez hello suivant (méthode) (n’oubliez pas tooreplace hello **chaîne de connexion** et **nom de hub**) :
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
            var alert = "{\"aps\":{\"alert\":\"Hello from .NET!\"}}";
            await hub.SendAppleNativeNotificationAsync(alert);
        }
6. Ajouter hello suivant des lignes dans votre `Main` méthode :
   
         SendNotificationAsync();
         Console.ReadLine();
7. Appuyez sur la touche application de hello toorun clé hello F5. En quelques secondes, une notification Push devrait s’afficher sur votre appareil. Si vous utilisez le Wi-Fi ou un réseau cellulaire de données, assurez-vous que vous avez une connexion internet active sur l’appareil de hello.

Vous pouvez trouver toutes les charges utiles de possibles hello Bonjour Apple [Local et le Guide de programmation de Notification Push].

#### <a name="optional-send-notifications-from-a-mobile-service"></a>(Facultatif) Envoi de notifications depuis un service mobile
Dans cette section, nous allons envoyer des notifications Push à l’aide d’un service mobile via un script de nœud.

toosend une notification à l’aide d’un service mobile, procédez comme [prise en main des Services mobiles], puis :

1. Connectez-vous à toohello [portail classique Azure], puis sélectionnez votre service mobile.
2. Sélectionnez hello **planificateur** onglet en haut de hello.
   
       ![Azure Classic Portal - Scheduler][215]
3. Créez un travail planifié, insérez un nom, puis sélectionnez **On demand**.
   
       ![Azure Classic Portal - Create new job][216]
4. Lorsque le travail de hello est créé, cliquez sur le nom de la tâche hello. Puis cliquez sur hello **Script** onglet sur la barre supérieure de hello.
5. Insérez hello script à l’intérieur de votre fonction Planificateur suivant. Rendre des espaces réservés de hello tooreplace vraiment avec votre notification hub hello et nom de chaîne de connexion pour *DefaultFullSharedAccessSignature* que vous avez obtenu précédemment. Cliquez sur **Enregistrer**.
   
        var azure = require('azure');
        var notificationHubService = azure.createNotificationHubService('<Hubname>', '<SAS Full access >');
        notificationHubService.apns.send(
            null,
            {"aps":
                {
                  "alert": "Hello from Mobile Services!"
                }
            },
            function (error)
            {
                if (!error) {
                    console.warn("Notification successful");
                }
            }
        );
6. Cliquez sur **exécuter une fois** sur la barre inférieure de hello. Vous devez recevoir une alerte sur votre appareil.

## <a name="next-steps"></a>Étapes suivantes
Dans cet exemple simple, vous diffusées tooall de notifications push à vos appareils iOS. Dans l’ordre tootarget des utilisateurs spécifiques, consultez le didacticiel de toohello [utiliser Notification Hubs toopush notifications toousers]. Si vous souhaitez toosegment vos utilisateurs en groupes d’intérêt, vous pouvez lire [toosend utiliser Notification Hubs actualités]. En savoir plus sur la façon toouse Notification Hubs dans [des conseils de concentrateurs de Notification] et Bonjour [iOS de concentrateurs de Notification procédure-toofor].

<!-- Images. -->

[213]: ./media/partner-xamarin-notification-hubs-ios-get-started/notification-hub-create-console-app.png

[215]: ./media/partner-xamarin-notification-hubs-ios-get-started/notification-hub-scheduler1.png
[216]: ./media/partner-xamarin-notification-hubs-ios-get-started/notification-hub-scheduler2.png


[31]: ./media/partner-xamarin-notification-hubs-ios-get-started/notification-hub-create-ios-app.png




<!-- URLs. -->
[Mobile Services iOS SDK]: http://go.microsoft.com/fwLink/?LinkID=266533
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253

[prise en main des Services mobiles]: /develop/mobile/tutorials/get-started-xamarin-ios
[portail classique Azure]: https://manage.windowsazure.com/
[des conseils de concentrateurs de Notification]: http://msdn.microsoft.com/library/jj927170.aspx
[iOS de concentrateurs de Notification procédure-toofor]: http://msdn.microsoft.com/library/jj927168.aspx
[Install Xcode]: https://go.microsoft.com/fwLink/p/?LinkID=266532
[iOS Provisioning Portal]: http://go.microsoft.com/fwlink/p/?LinkId=272456

[utiliser Notification Hubs toopush notifications toousers]: /manage/services/notification-hubs/notify-users-aspnet
[toosend utiliser Notification Hubs actualités]: /manage/services/notification-hubs/breaking-news-dotnet

[Local et le Guide de programmation de Notification Push]:https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/HandlingRemoteNotifications.html#//apple_ref/doc/uid/TP40008194-CH6-SW1
[Apple Push Notification Service]: http://go.microsoft.com/fwlink/p/?LinkId=272584

[Azure Mobile Services Component]: http://components.xamarin.com/view/azure-mobile-services/
[GitHub]: http://go.microsoft.com/fwlink/p/?LinkId=331329
[Xamarin Studio]: http://xamarin.com/download
[WindowsAzure.Messaging]: https://github.com/infosupport/WindowsAzure.Messaging.iOS
[Azure Portal]: https://portal.azure.com
