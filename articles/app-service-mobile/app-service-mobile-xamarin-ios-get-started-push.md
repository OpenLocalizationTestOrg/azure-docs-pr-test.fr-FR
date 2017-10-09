---
title: application aaaAdd push notifications tooyour Xamarin.iOS avec Azure App Service
description: "Découvrez comment toouse Azure App Service toosend push notifications tooyour Xamarin.iOS application"
services: app-service\mobile
documentationcenter: xamarin
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 2921214a-49f8-45e1-a306-a85ce21defca
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-ios
ms.devlang: dotnet
ms.topic: article
ms.date: 10/12/2016
ms.author: glenga
ms.openlocfilehash: 3e6439aee4f3fe0f60b9786d0bbfd74c4f5e52d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="add-push-notifications-tooyour-xamarinios-app"></a>Ajouter des notifications de push tooyour application Xamarin.iOS
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a>Vue d'ensemble
Dans ce didacticiel, vous allez ajouter toohello de notifications push [Xamarin.iOS de démarrage rapide](app-service-mobile-xamarin-ios-get-started.md) projet afin qu’une notification push est envoyée toohello périphérique chaque fois qu’un enregistrement est inséré.

Si vous n’utilisez pas hello téléchargé le projet de démarrage rapide de serveur, vous devez serez hello package d’extension de notification push. Consultez [fonctionne avec serveur principal de .NET hello SDK pour les applications mobiles Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) pour plus d’informations.

## <a name="prerequisites"></a>Composants requis
* Hello complète [Xamarin.iOS quickstart](app-service-mobile-xamarin-ios-get-started.md) didacticiel.
* Un appareil iOS physique. Notifications push ne sont pas pris en charge par le simulateur iOS de hello.

## <a name="register-hello-app-for-push-notifications-on-apples-developer-portal"></a>Inscrire l’application hello pour les notifications push sur le portail des développeurs d’Apple
[!INCLUDE [Enable Apple Push Notifications](../../includes/enable-apple-push-notifications.md)]

## <a name="configure-your-mobile-app-toosend-push-notifications"></a>Configurer les notifications de push de l’application Mobile toosend
[!INCLUDE [app-service-mobile-apns-configure-push](../../includes/app-service-mobile-apns-configure-push.md)]

## <a name="update-hello-server-project-toosend-push-notifications"></a>Mettre à jour des notifications push de hello serveur projet toosend
[!INCLUDE [app-service-mobile-update-server-project-for-push-template](../../includes/app-service-mobile-update-server-project-for-push-template.md)]

## <a name="configure-your-xamarinios-project"></a>Configurer votre projet Xamarin.iOS
[!INCLUDE [app-service-mobile-xamarin-ios-configure-project](../../includes/app-service-mobile-xamarin-ios-configure-project.md)]

## <a name="add-push-notifications-tooyour-app"></a>Ajouter une application de tooyour de notifications push
1. Dans **QSTodoService**, ajouter hello suivant propriété afin que **AppDelegate** peut acquérir les clients mobiles hello :
   
            public MobileServiceClient GetClient {
            get
            {
                return client;
            }
            private set
            {
                client = value;
            }
        }
2. Ajoutez hello suivant `using` haut de toohello d’instruction de hello **AppDelegate.cs** fichier.
   
        using Microsoft.WindowsAzure.MobileServices;
        using Newtonsoft.Json.Linq;
3. Dans **AppDelegate**, substituez hello **FinishedLaunching** événement :
   
        public override bool FinishedLaunching(UIApplication application, NSDictionary launchOptions)
        {
            // registers for push for iOS8
            var settings = UIUserNotificationSettings.GetSettingsForTypes(
                UIUserNotificationType.Alert
                | UIUserNotificationType.Badge
                | UIUserNotificationType.Sound,
                new NSSet());
   
            UIApplication.SharedApplication.RegisterUserNotificationSettings(settings);
            UIApplication.SharedApplication.RegisterForRemoteNotifications();
   
            return true;
        }
4. Dans hello du même fichier, remplacer hello **RegisteredForRemoteNotifications** événement. Dans ce code, vous vous inscrivez pour une notification de modèle simple qui est envoyée sur toutes les plateformes prises en charge par le serveur de hello.
   
    Pour plus d’informations sur les modèles avec Notification Hubs, consultez [Modèles](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md).

        public override void RegisteredForRemoteNotifications(UIApplication application, NSData deviceToken)
        {
            MobileServiceClient client = QSTodoService.DefaultService.GetClient;

            const string templateBodyAPNS = "{\"aps\":{\"alert\":\"$(messageParam)\"}}";

            JObject templates = new JObject();
            templates["genericMessage"] = new JObject
            {
                {"body", templateBodyAPNS}
            };

            // Register for push with your mobile app
            var push = client.GetPush();
            push.RegisterAsync(deviceToken, templates);
        }


1. Substituez ensuite hello **DidReceivedRemoteNotification** événement :
   
        public override void DidReceiveRemoteNotification (UIApplication application, NSDictionary userInfo, Action<UIBackgroundFetchResult> completionHandler)
        {
            NSDictionary aps = userInfo.ObjectForKey(new NSString("aps")) as NSDictionary;
   
            string alert = string.Empty;
            if (aps.ContainsKey(new NSString("alert")))
                alert = (aps [new NSString("alert")] as NSString).ToString();
   
            //show alert
            if (!string.IsNullOrEmpty(alert))
            {
                UIAlertView avAlert = new UIAlertView("Notification", alert, null, "OK", null);
                avAlert.Show();
            }
        }

Votre application est maintenant des notifications push de toosupport mis à jour.

## <a name="test"></a>Tester les notifications push dans votre application
1. Hello de presse **exécuter** projet de hello toobuild et démarrer l’application hello dans un appareil iOS, puis cliquez sur **OK** tooaccept les notifications push.
   
   > [!NOTE]
   > Vous devez accepter explicitement les notifications Push de votre application. Cette demande produit uniquement hello première fois que hello application s’exécute.
   > 
   > 
2. Dans l’application hello, une tâche, puis tapez Bonjour signe plu (**+**) icône.
3. Vérifiez qu’une notification est reçue, puis cliquez sur **OK** toodismiss hello notification.
4. Répétez l’étape 2 et fermer immédiatement hello app, puis vérifiez qu’une notification s’affiche.

Vous avez terminé ce didacticiel.

<!-- Images. -->

<!-- URLs. -->



