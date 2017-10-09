---
title: "aaaGet main d’Azure Mobile Engagement pour Xamarin.iOS"
description: "Découvrez comment toouse Azure Mobile Engagement avec Analytique et les Notifications Push pour les applications de Xamarin.iOS."
services: mobile-engagement
documentationcenter: xamarin
author: piyushjo
manager: erikre
editor: 
ms.assetid: 0448209e-fff6-47bd-985c-2cf074bac12f
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-ios
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 02340a744753dcc5cd1b6888a5fa87628be47b68
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-xamarinios-apps"></a>Prise en main d’Azure Mobile Engagement pour les applications Xamarin.iOS
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

Cette rubrique vous montre comment toouse Azure Mobile Engagement toounderstand votre utilisation de l’application et l’envoi push notifications toosegmented les utilisateurs dans une application Xamarin.iOS.
Dans ce didacticiel, vous allez créer une application Xamarin.iOS vide qui collecte des données de base et reçoit des notifications Push à l’aide du service APN (Apple Push Notification).

> [!NOTE]
> Hello Azure Mobile Engagement service mars 2018 est retirée et est actuellement que les clients tooexisting disponibles. Pour plus d’informations, consultez [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).

Ce didacticiel requiert hello qui suit :

* [Xamarin Studio](http://xamarin.com/studio). Vous pouvez également utiliser Visual Studio avec Xamarin, mais ce didacticiel utilise Xamarin Studio. Pour obtenir des instructions sur l’installation, consultez la page [Configuration et installation pour Visual Studio et Xamarin](https://msdn.microsoft.com/library/mt613162.aspx). 
* [Kit de développement logiciel (SDK) Mobile Engagement pour Xamarin](https://www.nuget.org/packages/Microsoft.Azure.Engagement.Xamarin/)

> [!NOTE]
> toocomplete ce didacticiel, vous devez disposer d’un compte Azure actif. Si vous ne possédez pas de compte, vous pouvez créer un compte d'évaluation gratuit en quelques minutes. Pour plus d'informations, consultez la page [Version d'évaluation gratuite d'Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-xamarin-ios-get-started).
> 
> 

## <a id="setup-azme"></a>Configuration de Mobile Engagement pour votre application iOS
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <a id="connecting-app"></a>Se connecter à votre serveur principal d’application toohello Mobile Engagement
Ce didacticiel présente une « intégration de base « hello minimale définie les données de toocollect requis et envoyer une notification push.

Nous allons créer une application de base avec l’intégration de hello toodemonstrate Xamarin :

### <a name="create-a-new-xamarinios-project"></a>Créer un projet Xamarin.iOS
1. Démarrez Xamarin Studio. Accédez trop**fichier** -> **nouveau** -> **Solution** 
   
    ![][1]
2. Sélectionnez **application vue unique**, assurez-vous que la langue hello sélectionné est **c#** puis cliquez sur **suivant**.
   
    ![][2]
3. Renseignez hello **nom de l’application** et hello **identifiant d’organisation** puis cliquez sur **suivant**. 
   
    ![][3]
   
   > [!IMPORTANT]
   > Vérifiez que hello publication que vous utilisez finalement toodeploy que votre application iOS utilise un ID d’application qui correspond à exactement avec hello identificateur de lot que vous avez ici. 
   > 
   > 
4. Hello de mise à jour **nom du projet**, **nom de la Solution** et **emplacement** si nécessaire et cliquez sur **créer**.
   
    ![][4]

Xamarin Studio créera une application de démonstration hello dans lequel nous intégrera Mobile Engagement. 

### <a name="connect-your-app-toomobile-engagement-backend"></a>Se connecter à votre serveur principal d’application tooMobile Engagement
1. Cliquez avec le bouton droit sur hello **Packages** dossier dans windows de Solution hello et sélectionnez **ajouter des Packages en cours...**
   
    ![][5]
2. Recherchez hello **Microsoft Azure Mobile Engagement Xamarin SDK** et ajoutez-le tooyour solution.  
   
    ![][6]
3. Ouvrez **AppDelegate.cs** et ajoutez hello qui suit à l’aide d’instruction :
   
        using Microsoft.Azure.Engagement.Xamarin;
4. Bonjour **FinishedLaunching** (méthode), ajouter hello après la connexion de hello tooinitialize avec le serveur principal Mobile Engagement. Assurez-vous que tooadd votre **ConnectionString**. Ce code utilise également un fantôme **NotificationIcon** qui est ajouté par hello Mobile Engagement Kit de développement logiciel que vous pouvez tooreplace. 
   
        EngagementConfiguration config = new EngagementConfiguration {
                        ConnectionString = "YourConnectionStringFromAzurePortal",
                        NotificationIcon = UIImage.FromBundle("close")
                    };
        EngagementAgent.Init (config);

## <a id="monitor"></a>Activation de la surveillance en temps réel
Dans l’ordre toostart envoi de données et en garantissant hello utilisateurs sont actifs, vous devez envoyer au moins un écran toohello Mobile Engagement principal.

1. Ouvrez **ViewController.cs** et ajoutez hello qui suit à l’aide d’instruction :
   
        using Microsoft.Azure.Engagement.Xamarin;
2. Remplacez la classe hello à partir de laquelle `ViewController` hérite `UIViewController` trop`EngagementViewController`. 

## <a id="monitor"></a>Connexion d’application avec l’analyse en temps réel
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <a id="integrate-push"></a>Activation des notifications push et de la messagerie in-app
Mobile Engagement vous permet de toointeract avec vos utilisateurs et portée avec des notifications push et les messages dans le contexte de hello de campagnes dans l’application. Ce module est appelé portée dans le portail Mobile Engagement de hello.
Hello sections suivantes configurer votre application tooreceive les.

### <a name="modify-your-application-delegate"></a>Modifier votre délégué d'Application
1. Ouvrez hello **AppDelegate.cs** et ajoutez hello qui suit à l’aide d’instruction :
   
        using System; 
2. Maintenant, à l’intérieur hello `FinishedLaunching` (méthode), ajouter hello suivant tooregister pour les messages envoyés après`EngagementAgent.init(...)`
   
        if (UIDevice.CurrentDevice.CheckSystemVersion(8,0))
        {
            var pushSettings = UIUserNotificationSettings.GetSettingsForTypes (
                (UIUserNotificationType.Badge |
                    UIUserNotificationType.Sound |
                    UIUserNotificationType.Alert),
                null);
            UIApplication.SharedApplication.RegisterUserNotificationSettings (pushSettings);
            UIApplication.SharedApplication.RegisterForRemoteNotifications ();
        }
        else
        {
            UIApplication.SharedApplication.RegisterForRemoteNotificationTypes (
                UIRemoteNotificationType.Badge |
                UIRemoteNotificationType.Sound |
                UIRemoteNotificationType.Alert);
        }
3. Enfin - mettre à jour ou ajouter hello méthodes suivantes :
   
        public override void DidReceiveRemoteNotification (UIApplication application, NSDictionary userInfo, 
            Action<UIBackgroundFetchResult> completionHandler)
        {
            EngagementAgent.ApplicationDidReceiveRemoteNotification(userInfo, completionHandler);
        }
   
        public override void RegisteredForRemoteNotifications (UIApplication application, NSData deviceToken)
        {
            // Register device token on Engagement
            EngagementAgent.RegisterDeviceToken(deviceToken);
        }
   
        public override void FailedToRegisterForRemoteNotifications(UIApplication application, NSError error)
        {
            Console.WriteLine("Failed tooregister for remote notifications: Error '{0}'", error);
        }
4. Dans votre **Info.plist** de fichiers dans la solution de hello, vérifiez que hello **identificateur de lot** correspond au hello **ID d’application** vous avez dans votre profil de configuration Bonjour Apple Dev Centre. 
   
    ![][7]
5. Dans hello même **Info.plist** de fichiers, assurez-vous que vous avez vérifié hello **activer les Modes d’arrière-plan** et **des Notifications à distance**. 
   
     ![][8]
6. Exécutez l’application hello sur périphérique hello que vous avez associé à ce profil de publication. 

[!INCLUDE [mobile-engagement-ios-send-push-push](../../includes/mobile-engagement-ios-send-push.md)]

<!-- Images. -->
[1]: ./media/mobile-engagement-xamarin-ios-get-started/new-solution.png
[2]: ./media/mobile-engagement-xamarin-ios-get-started/app-type.png
[3]: ./media/mobile-engagement-xamarin-ios-get-started/configure-project-name.png
[4]: ./media/mobile-engagement-xamarin-ios-get-started/configure-project-confirm.png
[5]: ./media/mobile-engagement-xamarin-ios-get-started/add-nuget.png
[6]: ./media/mobile-engagement-xamarin-ios-get-started/add-nuget-azme.png
[7]: ./media/mobile-engagement-xamarin-ios-get-started/info-plist-confirm-bundle.png
[8]: ./media/mobile-engagement-xamarin-ios-get-started/info-plist-configure-push.png
