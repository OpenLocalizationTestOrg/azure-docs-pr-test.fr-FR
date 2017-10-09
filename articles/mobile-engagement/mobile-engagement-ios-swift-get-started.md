---
title: "aaaGet main d’Azure Mobile Engagement pour iOS dans Swift | Documents Microsoft"
description: "Découvrez comment toouse Azure Mobile Engagement avec Analytique et les Notifications Push pour des applications iOS."
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 196c282d-6f2f-4cbc-aeee-6517c5ad866d
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: swift
ms.topic: hero-article
ms.date: 09/20/2016
ms.author: piyushjo
ms.openlocfilehash: 9a3841d305745f8b80c6b0c86aabe18e0c7c0e59
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-ios-apps-in-swift"></a>Prise en main d’Azure Mobile Engagement pour les applications iOS dans Swift
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

Cette rubrique vous montre comment toouse Azure Mobile Engagement toounderstand votre utilisation de l’application et l’envoi de notifications toosegmented utilisateurs tooan iOS application push.
Dans ce didacticiel, vous créez une application iOS vide qui collecte des données de base et reçoit des notifications push à l'aide du service APN (Apple Push Notification Service).

Ce didacticiel requiert hello qui suit :

* XCode 8, que vous pouvez installer depuis l’App Store de votre MAC
* Hello [Mobile Engagement iOS SDK]
* Le certificat de notification push (.p12) que vous pouvez obtenir dans votre Centre de développement Apple

> [!NOTE]
> Ce didacticiel utilise Swift version 3.0. 
> 
> 

Vous devez suivre ce didacticiel pour avoir accès à tous les autres didacticiels Mobile Engagement pour applications iOS.

> [!NOTE]
> toocomplete ce didacticiel, vous devez disposer d’un compte Azure actif. Si vous ne possédez pas de compte, vous pouvez créer un compte d'évaluation gratuit en quelques minutes. Pour plus d'informations, consultez la page [Version d'évaluation gratuite d'Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-ios-swift-get-started).
> 
> 

## <a id="setup-azme"></a>Configuration de Mobile Engagement pour votre application iOS
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <a id="connecting-app"></a>Se connecter à votre serveur principal d’application toohello Mobile Engagement
Ce didacticiel présente une « intégration de base », qui est hello minimal requis toocollect données et envoyer une notification push. Vous trouverez la documentation sur l’intégration complète Hello dans hello [intégration du Kit de développement logiciel iOS Mobile Engagement](mobile-engagement-ios-sdk-overview.md)

Nous allons créer une application de base avec l’intégration de hello XCode toodemonstrate :

### <a name="create-a-new-ios-project"></a>Création d’un projet iOS
[!INCLUDE [Create a new iOS Project](../../includes/mobile-engagement-create-new-ios-app.md)]

### <a name="connect-your-app-toomobile-engagement-backend"></a>Se connecter à votre serveur principal d’application tooMobile Engagement
1. Télécharger hello [Mobile Engagement iOS SDK]
2. Extraire hello. tar.gz fichier tooa dossier sur votre ordinateur
3. Cliquez avec le bouton droit sur le projet hello et sélectionnez « Ajouter des fichiers trop... »
   
    ![][1]
4. Exploration du dossier toohello où vous avez extrait hello SDK et sélectionnez hello `EngagementSDK` dossier puis appuyez sur OK.
   
    ![][2]
5. Ouvrez hello `Build Phases` onglet et Bonjour `Link Binary With Libraries` menu Ajouter des infrastructures de hello comme indiqué ci-dessous :
   
    ![][3]
6. Créer objectif C API un pontage en-tête toobe toouse en mesure de hello du Kit de développement en cliquant sur fichier > Nouveau > fichier > iOS > Source > fichier d’en-tête.
   
    ![][4]
7. Modifier les hello pontage en-tête fichier tooexpose Mobile Engagement Objective-C code tooyour code Swift, ajouter hello suivant importations :
   
        /* Mobile Engagement Agent */
        #import "AEModule.h"
        #import "AEPushMessage.h"
        #import "AEStorage.h"
        #import "EngagementAgent.h"
        #import "EngagementTableViewController.h"
        #import "EngagementViewController.h"
        #import "AEUserNotificationHandler.h"
        #import "AEIdfaProvider.h"
8. Sous paramètres de génération, vérifiez que hello en-tête de Objective-C Bridging paramètre sous du compilateur Swift - génération de Code de la build a un en-tête toothis de chemin d’accès. Voici un exemple de chemin d’accès : **$(SRCROOT)/MySuperApp/MySuperApp-Bridging-Header.h (selon le chemin d’accès de hello)**
   
   ![][6]
9. Revenir en arrière toohello portail Azure dans votre application *informations de connexion* page et copie hello la chaîne de connexion
   
   ![][5]
10. Collez maintenant la chaîne de connexion hello Bonjour `didFinishLaunchingWithOptions` déléguer
    
        func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplicationLaunchOptionsKey: Any]?) -> Bool
        {
              [...]
                EngagementAgent.init("Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}")
              [...]
        }

## <a id="monitor"></a>Activation de la surveillance en temps réel
Dans l’ordre toostart envoi de données et en garantissant que les utilisateurs de hello sont actifs, vous devez envoyer au moins un principal de Mobile Engagement toohello écran (activité).

1. Ouvrez hello **ViewController.swift** de fichier et remplacez la classe de base hello de **ViewController** toobe **EngagementViewController**:
   
    `class ViewController : EngagementViewController {`

## <a id="monitor"></a>Connexion d’application avec l’analyse en temps réel
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <a id="integrate-push"></a>Activation des notifications Push et de la messagerie intégrée à l’application
Mobile Engagement vous permet de toointeract et portée avec vos utilisateurs avec des Notifications Push et de la messagerie dans l’application dans le contexte de hello de campagnes. Ce module est appelé portée dans le portail Mobile Engagement de hello.
Hello sections suivantes va installer votre application tooreceive les.

### <a name="enable-your-app-tooreceive-silent-push-notifications"></a>Activer votre tooreceive d’application en mode silencieux des Notifications Push
[!INCLUDE [mobile-engagement-ios-silent-push](../../includes/mobile-engagement-ios-silent-push.md)]

### <a name="add-hello-reach-library-tooyour-project"></a>Ajouter un projet de hello portée bibliothèque tooyour
1. Cliquez avec le bouton droit sur votre projet
2. Sélectionnez `Add file too...`.
3. Exploration du dossier toohello où vous avez extrait hello SDK
4. Sélectionnez hello `EngagementReach` dossier
5. Cliquez sur Ajouter.
6. Modifiez les hello pontage d’en-tête du fichier tooexpose Mobile Engagement Objective-C atteindre les en-têtes et ajoutez les hello suivant importations :
   
        /* Mobile Engagement Reach */
        #import "AEAnnouncementViewController.h"
        #import "AEAutorotateView.h"
        #import "AEContentViewController.h"
        #import "AEDefaultAnnouncementViewController.h"
        #import "AEDefaultNotifier.h"
        #import "AEDefaultPollViewController.h"
        #import "AEInteractiveContent.h"
        #import "AENotificationView.h"
        #import "AENotifier.h"
        #import "AEPollViewController.h"
        #import "AEReachAbstractAnnouncement.h"
        #import "AEReachAnnouncement.h"
        #import "AEReachContent.h"
        #import "AEReachDataPush.h"
        #import "AEReachDataPushDelegate.h"
        #import "AEReachModule.h"
        #import "AEReachNotifAnnouncement.h"
        #import "AEReachPoll.h"
        #import "AEReachPollQuestion.h"
        #import "AEViewControllerUtil.h"
        #import "AEWebAnnouncementJsBridge.h"

### <a name="modify-your-application-delegate"></a>Modifier votre délégué d'Application
1. À l’intérieur hello `didFinishLaunchingWithOptions` - créer un module de couverture et passer en ligne de l’initialisation Engagement tooyour existante :
   
        func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplicationLaunchOptionsKey: Any]?) -> Bool 
        {
            let reach = AEReachModule.module(withNotificationIcon: UIImage(named:"icon.png")) as! AEReachModule
            EngagementAgent.init("Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}", modulesArray:[reach])
            [...]
            return true
        }

### <a name="enable-your-app-tooreceive-apns-push-notifications"></a>Activer votre tooreceive application APNS les Notifications Push
1. Ajouter hello suivant ligne toohello `didFinishLaunchingWithOptions` méthode :
   
        if #available(iOS 8.0, *)
        {
            if #available(iOS 10.0, *)
            {
                UNUserNotificationCenter.current().requestAuthorization(options: [.alert, .badge, .sound]) { (granted, error) in }
            }else
            {
                let settings = UIUserNotificationSettings(types: [.alert, .badge, .sound], categories: nil)
                application.registerUserNotificationSettings(settings)
            }
            application.registerForRemoteNotifications()
        }
        else
        {
            application.registerForRemoteNotifications(matching: [.alert, .badge, .sound])
        }
2. Ajouter hello `didRegisterForRemoteNotificationsWithDeviceToken` méthode comme suit :
   
        func application(_ application: UIApplication, didRegisterForRemoteNotificationsWithDeviceToken deviceToken: Data) {
            EngagementAgent.shared().registerDeviceToken(deviceToken)
        }
3. Ajouter hello `didReceiveRemoteNotification:fetchCompletionHandler:` méthode comme suit :
   
        func application(_ application: UIApplication, didReceiveRemoteNotification userInfo: [AnyHashable : Any], fetchCompletionHandler completionHandler: @escaping (UIBackgroundFetchResult) -> Void) {
            EngagementAgent.shared().applicationDidReceiveRemoteNotification(userInfo, fetchCompletionHandler:completionHandler)
        }

[!INCLUDE [mobile-engagement-ios-send-push-push](../../includes/mobile-engagement-ios-send-push.md)]

<!-- URLs. -->
[Mobile Engagement iOS SDK]: http://aka.ms/qk2rnj

<!-- Images. -->
[1]: ./media/mobile-engagement-ios-get-started/xcode-add-files.png
[2]: ./media/mobile-engagement-ios-get-started/xcode-select-engagement-sdk.png
[3]: ./media/mobile-engagement-ios-get-started/xcode-build-phases.png
[4]: ./media/mobile-engagement-ios-swift-get-started/add-header-file.png
[5]: ./media/mobile-engagement-ios-get-started/app-connection-info-page.png
[6]: ./media/mobile-engagement-ios-swift-get-started/add-bridging-header.png
