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
# <a name="get-started-with-azure-mobile-engagement-for-ios-apps-in-swift"></a><span data-ttu-id="e994a-103">Prise en main d’Azure Mobile Engagement pour les applications iOS dans Swift</span><span class="sxs-lookup"><span data-stu-id="e994a-103">Get Started with Azure Mobile Engagement for iOS Apps in Swift</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="e994a-104">Cette rubrique vous montre comment toouse Azure Mobile Engagement toounderstand votre utilisation de l’application et l’envoi de notifications toosegmented utilisateurs tooan iOS application push.</span><span class="sxs-lookup"><span data-stu-id="e994a-104">This topic shows you how toouse Azure Mobile Engagement toounderstand your app usage and send push notifications toosegmented users tooan iOS application.</span></span>
<span data-ttu-id="e994a-105">Dans ce didacticiel, vous créez une application iOS vide qui collecte des données de base et reçoit des notifications push à l'aide du service APN (Apple Push Notification Service).</span><span class="sxs-lookup"><span data-stu-id="e994a-105">In this tutorial, you create a blank iOS app that collects basic data and receives push notifications using Apple Push Notification System (APNS).</span></span>

<span data-ttu-id="e994a-106">Ce didacticiel requiert hello qui suit :</span><span class="sxs-lookup"><span data-stu-id="e994a-106">This tutorial requires hello following:</span></span>

* <span data-ttu-id="e994a-107">XCode 8, que vous pouvez installer depuis l’App Store de votre MAC</span><span class="sxs-lookup"><span data-stu-id="e994a-107">XCode 8, which you can install from your MAC App Store</span></span>
* <span data-ttu-id="e994a-108">Hello [Mobile Engagement iOS SDK]</span><span class="sxs-lookup"><span data-stu-id="e994a-108">hello [Mobile Engagement iOS SDK]</span></span>
* <span data-ttu-id="e994a-109">Le certificat de notification push (.p12) que vous pouvez obtenir dans votre Centre de développement Apple</span><span class="sxs-lookup"><span data-stu-id="e994a-109">Push notification certificate (.p12) that you can obtain on your Apple Dev Center</span></span>

> [!NOTE]
> <span data-ttu-id="e994a-110">Ce didacticiel utilise Swift version 3.0.</span><span class="sxs-lookup"><span data-stu-id="e994a-110">This tutorial uses Swift version 3.0.</span></span> 
> 
> 

<span data-ttu-id="e994a-111">Vous devez suivre ce didacticiel pour avoir accès à tous les autres didacticiels Mobile Engagement pour applications iOS.</span><span class="sxs-lookup"><span data-stu-id="e994a-111">Completing this tutorial is a prerequisite for all other Mobile Engagement tutorials for iOS apps.</span></span>

> [!NOTE]
> <span data-ttu-id="e994a-112">toocomplete ce didacticiel, vous devez disposer d’un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="e994a-112">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="e994a-113">Si vous ne possédez pas de compte, vous pouvez créer un compte d'évaluation gratuit en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="e994a-113">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="e994a-114">Pour plus d'informations, consultez la page [Version d'évaluation gratuite d'Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-ios-swift-get-started).</span><span class="sxs-lookup"><span data-stu-id="e994a-114">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-ios-swift-get-started).</span></span>
> 
> 

## <span data-ttu-id="e994a-115"><a id="setup-azme"></a>Configuration de Mobile Engagement pour votre application iOS</span><span class="sxs-lookup"><span data-stu-id="e994a-115"><a id="setup-azme"></a>Setup Mobile Engagement for your iOS app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="e994a-116"><a id="connecting-app"></a>Se connecter à votre serveur principal d’application toohello Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="e994a-116"><a id="connecting-app"></a>Connect your app toohello Mobile Engagement backend</span></span>
<span data-ttu-id="e994a-117">Ce didacticiel présente une « intégration de base », qui est hello minimal requis toocollect données et envoyer une notification push.</span><span class="sxs-lookup"><span data-stu-id="e994a-117">This tutorial presents a "basic integration", which is hello minimal set required toocollect data and send a push notification.</span></span> <span data-ttu-id="e994a-118">Vous trouverez la documentation sur l’intégration complète Hello dans hello [intégration du Kit de développement logiciel iOS Mobile Engagement](mobile-engagement-ios-sdk-overview.md)</span><span class="sxs-lookup"><span data-stu-id="e994a-118">hello complete integration documentation can be found in hello [Mobile Engagement iOS SDK integration](mobile-engagement-ios-sdk-overview.md)</span></span>

<span data-ttu-id="e994a-119">Nous allons créer une application de base avec l’intégration de hello XCode toodemonstrate :</span><span class="sxs-lookup"><span data-stu-id="e994a-119">We will create a basic app with XCode toodemonstrate hello integration:</span></span>

### <a name="create-a-new-ios-project"></a><span data-ttu-id="e994a-120">Création d’un projet iOS</span><span class="sxs-lookup"><span data-stu-id="e994a-120">Create a new iOS project</span></span>
[!INCLUDE [Create a new iOS Project](../../includes/mobile-engagement-create-new-ios-app.md)]

### <a name="connect-your-app-toomobile-engagement-backend"></a><span data-ttu-id="e994a-121">Se connecter à votre serveur principal d’application tooMobile Engagement</span><span class="sxs-lookup"><span data-stu-id="e994a-121">Connect your app tooMobile Engagement backend</span></span>
1. <span data-ttu-id="e994a-122">Télécharger hello [Mobile Engagement iOS SDK]</span><span class="sxs-lookup"><span data-stu-id="e994a-122">Download hello [Mobile Engagement iOS SDK]</span></span>
2. <span data-ttu-id="e994a-123">Extraire hello. tar.gz fichier tooa dossier sur votre ordinateur</span><span class="sxs-lookup"><span data-stu-id="e994a-123">Extract hello .tar.gz file tooa folder in your computer</span></span>
3. <span data-ttu-id="e994a-124">Cliquez avec le bouton droit sur le projet hello et sélectionnez « Ajouter des fichiers trop... »</span><span class="sxs-lookup"><span data-stu-id="e994a-124">Right click hello project and select "Add files too..."</span></span>
   
    ![][1]
4. <span data-ttu-id="e994a-125">Exploration du dossier toohello où vous avez extrait hello SDK et sélectionnez hello `EngagementSDK` dossier puis appuyez sur OK.</span><span class="sxs-lookup"><span data-stu-id="e994a-125">Navigate toohello folder where you extracted hello SDK and select hello `EngagementSDK` folder then press OK.</span></span>
   
    ![][2]
5. <span data-ttu-id="e994a-126">Ouvrez hello `Build Phases` onglet et Bonjour `Link Binary With Libraries` menu Ajouter des infrastructures de hello comme indiqué ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="e994a-126">Open hello `Build Phases` tab and in hello `Link Binary With Libraries` menu add hello frameworks as shown below:</span></span>
   
    ![][3]
6. <span data-ttu-id="e994a-127">Créer objectif C API un pontage en-tête toobe toouse en mesure de hello du Kit de développement en cliquant sur fichier > Nouveau > fichier > iOS > Source > fichier d’en-tête.</span><span class="sxs-lookup"><span data-stu-id="e994a-127">Create a Bridging header toobe able toouse hello SDK's Objective C APIs by choosing File > New > File > iOS > Source > Header File.</span></span>
   
    ![][4]
7. <span data-ttu-id="e994a-128">Modifier les hello pontage en-tête fichier tooexpose Mobile Engagement Objective-C code tooyour code Swift, ajouter hello suivant importations :</span><span class="sxs-lookup"><span data-stu-id="e994a-128">Edit hello bridging header file tooexpose Mobile Engagement Objective-C code tooyour Swift code, add hello following imports :</span></span>
   
        /* Mobile Engagement Agent */
        #import "AEModule.h"
        #import "AEPushMessage.h"
        #import "AEStorage.h"
        #import "EngagementAgent.h"
        #import "EngagementTableViewController.h"
        #import "EngagementViewController.h"
        #import "AEUserNotificationHandler.h"
        #import "AEIdfaProvider.h"
8. <span data-ttu-id="e994a-129">Sous paramètres de génération, vérifiez que hello en-tête de Objective-C Bridging paramètre sous du compilateur Swift - génération de Code de la build a un en-tête toothis de chemin d’accès.</span><span class="sxs-lookup"><span data-stu-id="e994a-129">Under Build Settings, make sure hello Objective-C Bridging Header build setting under Swift Compiler - Code Generation has a path toothis header.</span></span> <span data-ttu-id="e994a-130">Voici un exemple de chemin d’accès : **$(SRCROOT)/MySuperApp/MySuperApp-Bridging-Header.h (selon le chemin d’accès de hello)**</span><span class="sxs-lookup"><span data-stu-id="e994a-130">Here is a path example: **$(SRCROOT)/MySuperApp/MySuperApp-Bridging-Header.h (depending on hello path)**</span></span>
   
   ![][6]
9. <span data-ttu-id="e994a-131">Revenir en arrière toohello portail Azure dans votre application *informations de connexion* page et copie hello la chaîne de connexion</span><span class="sxs-lookup"><span data-stu-id="e994a-131">Go back toohello Azure portal in your app's *Connection Info* page and copy hello Connection String</span></span>
   
   ![][5]
10. <span data-ttu-id="e994a-132">Collez maintenant la chaîne de connexion hello Bonjour `didFinishLaunchingWithOptions` déléguer</span><span class="sxs-lookup"><span data-stu-id="e994a-132">Now paste hello connection string in hello `didFinishLaunchingWithOptions` delegate</span></span>
    
        func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplicationLaunchOptionsKey: Any]?) -> Bool
        {
              [...]
                EngagementAgent.init("Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}")
              [...]
        }

## <span data-ttu-id="e994a-133"><a id="monitor"></a>Activation de la surveillance en temps réel</span><span class="sxs-lookup"><span data-stu-id="e994a-133"><a id="monitor"></a>Enabling real-time monitoring</span></span>
<span data-ttu-id="e994a-134">Dans l’ordre toostart envoi de données et en garantissant que les utilisateurs de hello sont actifs, vous devez envoyer au moins un principal de Mobile Engagement toohello écran (activité).</span><span class="sxs-lookup"><span data-stu-id="e994a-134">In order toostart sending data and ensuring that hello users are active, you must send at least one screen (Activity) toohello Mobile Engagement backend.</span></span>

1. <span data-ttu-id="e994a-135">Ouvrez hello **ViewController.swift** de fichier et remplacez la classe de base hello de **ViewController** toobe **EngagementViewController**:</span><span class="sxs-lookup"><span data-stu-id="e994a-135">Open hello **ViewController.swift** file and replace hello base class of **ViewController** toobe **EngagementViewController**:</span></span>
   
    `class ViewController : EngagementViewController {`

## <span data-ttu-id="e994a-136"><a id="monitor"></a>Connexion d’application avec l’analyse en temps réel</span><span class="sxs-lookup"><span data-stu-id="e994a-136"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="e994a-137"><a id="integrate-push"></a>Activation des notifications Push et de la messagerie intégrée à l’application</span><span class="sxs-lookup"><span data-stu-id="e994a-137"><a id="integrate-push"></a>Enabling Push Notifications and in-app messaging</span></span>
<span data-ttu-id="e994a-138">Mobile Engagement vous permet de toointeract et portée avec vos utilisateurs avec des Notifications Push et de la messagerie dans l’application dans le contexte de hello de campagnes.</span><span class="sxs-lookup"><span data-stu-id="e994a-138">Mobile Engagement allows you toointeract and REACH with your users with Push Notifications and In-app Messaging in hello context of campaigns.</span></span> <span data-ttu-id="e994a-139">Ce module est appelé portée dans le portail Mobile Engagement de hello.</span><span class="sxs-lookup"><span data-stu-id="e994a-139">This module is called REACH in hello Mobile Engagement portal.</span></span>
<span data-ttu-id="e994a-140">Hello sections suivantes va installer votre application tooreceive les.</span><span class="sxs-lookup"><span data-stu-id="e994a-140">hello following sections will setup your app tooreceive them.</span></span>

### <a name="enable-your-app-tooreceive-silent-push-notifications"></a><span data-ttu-id="e994a-141">Activer votre tooreceive d’application en mode silencieux des Notifications Push</span><span class="sxs-lookup"><span data-stu-id="e994a-141">Enable your app tooreceive Silent Push Notifications</span></span>
[!INCLUDE [mobile-engagement-ios-silent-push](../../includes/mobile-engagement-ios-silent-push.md)]

### <a name="add-hello-reach-library-tooyour-project"></a><span data-ttu-id="e994a-142">Ajouter un projet de hello portée bibliothèque tooyour</span><span class="sxs-lookup"><span data-stu-id="e994a-142">Add hello Reach library tooyour project</span></span>
1. <span data-ttu-id="e994a-143">Cliquez avec le bouton droit sur votre projet</span><span class="sxs-lookup"><span data-stu-id="e994a-143">Right click your project</span></span>
2. <span data-ttu-id="e994a-144">Sélectionnez `Add file too...`.</span><span class="sxs-lookup"><span data-stu-id="e994a-144">Select `Add file too...`</span></span>
3. <span data-ttu-id="e994a-145">Exploration du dossier toohello où vous avez extrait hello SDK</span><span class="sxs-lookup"><span data-stu-id="e994a-145">Navigate toohello folder where you extracted hello SDK</span></span>
4. <span data-ttu-id="e994a-146">Sélectionnez hello `EngagementReach` dossier</span><span class="sxs-lookup"><span data-stu-id="e994a-146">Select hello `EngagementReach` folder</span></span>
5. <span data-ttu-id="e994a-147">Cliquez sur Ajouter.</span><span class="sxs-lookup"><span data-stu-id="e994a-147">Click Add</span></span>
6. <span data-ttu-id="e994a-148">Modifiez les hello pontage d’en-tête du fichier tooexpose Mobile Engagement Objective-C atteindre les en-têtes et ajoutez les hello suivant importations :</span><span class="sxs-lookup"><span data-stu-id="e994a-148">Edit hello bridging header file tooexpose Mobile Engagement Objective-C Reach headers and add hello following imports :</span></span>
   
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

### <a name="modify-your-application-delegate"></a><span data-ttu-id="e994a-149">Modifier votre délégué d'Application</span><span class="sxs-lookup"><span data-stu-id="e994a-149">Modify your Application Delegate</span></span>
1. <span data-ttu-id="e994a-150">À l’intérieur hello `didFinishLaunchingWithOptions` - créer un module de couverture et passer en ligne de l’initialisation Engagement tooyour existante :</span><span class="sxs-lookup"><span data-stu-id="e994a-150">Inside  hello `didFinishLaunchingWithOptions` -  create a reach module and pass it tooyour existing Engagement initialization line:</span></span>
   
        func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplicationLaunchOptionsKey: Any]?) -> Bool 
        {
            let reach = AEReachModule.module(withNotificationIcon: UIImage(named:"icon.png")) as! AEReachModule
            EngagementAgent.init("Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}", modulesArray:[reach])
            [...]
            return true
        }

### <a name="enable-your-app-tooreceive-apns-push-notifications"></a><span data-ttu-id="e994a-151">Activer votre tooreceive application APNS les Notifications Push</span><span class="sxs-lookup"><span data-stu-id="e994a-151">Enable your app tooreceive APNS Push Notifications</span></span>
1. <span data-ttu-id="e994a-152">Ajouter hello suivant ligne toohello `didFinishLaunchingWithOptions` méthode :</span><span class="sxs-lookup"><span data-stu-id="e994a-152">Add hello following line toohello `didFinishLaunchingWithOptions` method:</span></span>
   
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
2. <span data-ttu-id="e994a-153">Ajouter hello `didRegisterForRemoteNotificationsWithDeviceToken` méthode comme suit :</span><span class="sxs-lookup"><span data-stu-id="e994a-153">Add hello `didRegisterForRemoteNotificationsWithDeviceToken` method as follows:</span></span>
   
        func application(_ application: UIApplication, didRegisterForRemoteNotificationsWithDeviceToken deviceToken: Data) {
            EngagementAgent.shared().registerDeviceToken(deviceToken)
        }
3. <span data-ttu-id="e994a-154">Ajouter hello `didReceiveRemoteNotification:fetchCompletionHandler:` méthode comme suit :</span><span class="sxs-lookup"><span data-stu-id="e994a-154">Add hello `didReceiveRemoteNotification:fetchCompletionHandler:` method as follows:</span></span>
   
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
