---
title: "aaaGet main d’Azure Mobile Engagement pour iOS dans Objective C | Documents Microsoft"
description: "Découvrez comment toouse Azure Mobile Engagement avec analytique et des notifications push pour les applications iOS."
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 117b5742-522b-41de-98c5-f432da2d98f8
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: hero-article
ms.date: 07/17/2017
ms.author: piyushjo
ms.openlocfilehash: 51a5013f23d2d04a7b9b30c83b47017898b2bb00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-ios-apps-in-objective-c"></a><span data-ttu-id="fc805-103">Prise en main d’Azure Mobile Engagement pour les applications iOS dans Objective C</span><span class="sxs-lookup"><span data-stu-id="fc805-103">Get Started with Azure Mobile Engagement for iOS apps in Objective C</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="fc805-104">Cette rubrique vous montre comment toouse Azure Mobile Engagement toounderstand votre utilisation de l’application et l’envoi de notifications toosegmented utilisateurs tooan iOS application push.</span><span class="sxs-lookup"><span data-stu-id="fc805-104">This topic shows you how toouse Azure Mobile Engagement toounderstand your app usage and send push notifications toosegmented users tooan iOS application.</span></span>
<span data-ttu-id="fc805-105">Dans ce didacticiel, vous créez une application iOS vide qui collecte des données de base et reçoit des notifications push à l'aide du service APN (Apple Push Notification Service).</span><span class="sxs-lookup"><span data-stu-id="fc805-105">In this tutorial, you create a blank iOS app that collects basic data and receives push notifications using Apple Push Notification System (APNS).</span></span>

<span data-ttu-id="fc805-106">Ce didacticiel requiert hello qui suit :</span><span class="sxs-lookup"><span data-stu-id="fc805-106">This tutorial requires hello following:</span></span>

* <span data-ttu-id="fc805-107">XCode 8, que vous pouvez installer depuis l’App Store de votre MAC</span><span class="sxs-lookup"><span data-stu-id="fc805-107">XCode 8, which you can install from your MAC App Store</span></span>
* <span data-ttu-id="fc805-108">Hello [Mobile Engagement iOS SDK]</span><span class="sxs-lookup"><span data-stu-id="fc805-108">hello [Mobile Engagement iOS SDK]</span></span>

<span data-ttu-id="fc805-109">Vous devez suivre ce didacticiel pour avoir accès à tous les autres didacticiels Mobile Engagement pour applications iOS.</span><span class="sxs-lookup"><span data-stu-id="fc805-109">Completing this tutorial is a prerequisite for all other Mobile Engagement tutorials for iOS apps.</span></span>

> [!NOTE]
> <span data-ttu-id="fc805-110">toocomplete ce didacticiel, vous devez disposer d’un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="fc805-110">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="fc805-111">Si vous ne possédez pas de compte, vous pouvez créer un compte d'évaluation gratuit en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="fc805-111">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="fc805-112">Pour plus d'informations, consultez la page [Version d'évaluation gratuite d'Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-ios-get-started).</span><span class="sxs-lookup"><span data-stu-id="fc805-112">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-ios-get-started).</span></span>
>
>

## <span data-ttu-id="fc805-113"><a id="setup-azme"></a>Configuration de Mobile Engagement pour votre application iOS</span><span class="sxs-lookup"><span data-stu-id="fc805-113"><a id="setup-azme"></a>Setup Mobile Engagement for your iOS app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="fc805-114"><a id="connecting-app"></a>Se connecter à votre serveur principal d’application toohello Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="fc805-114"><a id="connecting-app"></a>Connect your app toohello Mobile Engagement backend</span></span>
<span data-ttu-id="fc805-115">Ce didacticiel présente une « intégration de base », qui est hello minimal requis toocollect données et envoyer une notification push.</span><span class="sxs-lookup"><span data-stu-id="fc805-115">This tutorial presents a "basic integration", which is hello minimal set required toocollect data and send a push notification.</span></span> <span data-ttu-id="fc805-116">Vous trouverez la documentation sur l’intégration complète Hello dans hello [intégration du Kit de développement logiciel iOS Mobile Engagement](mobile-engagement-ios-sdk-overview.md)</span><span class="sxs-lookup"><span data-stu-id="fc805-116">hello complete integration documentation can be found in hello [Mobile Engagement iOS SDK integration](mobile-engagement-ios-sdk-overview.md)</span></span>

<span data-ttu-id="fc805-117">Nous allons créer une application de base avec l’intégration de hello toodemonstrate XCode.</span><span class="sxs-lookup"><span data-stu-id="fc805-117">We will create a basic app with XCode toodemonstrate hello integration.</span></span>

### <a name="create-a-new-ios-project"></a><span data-ttu-id="fc805-118">Création d’un projet iOS</span><span class="sxs-lookup"><span data-stu-id="fc805-118">Create a new iOS project</span></span>
[!INCLUDE [Create a new iOS Project](../../includes/mobile-engagement-create-new-ios-app.md)]

### <a name="connect-your-app-toohello-mobile-engagement-backend"></a><span data-ttu-id="fc805-119">Se connecter à votre serveur principal d’application toohello Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="fc805-119">Connect your app toohello Mobile Engagement backend</span></span>
1. <span data-ttu-id="fc805-120">Télécharger hello [Mobile Engagement iOS SDK].</span><span class="sxs-lookup"><span data-stu-id="fc805-120">Download hello [Mobile Engagement iOS SDK].</span></span>
2. <span data-ttu-id="fc805-121">Extraire hello. tar.gz fichier tooa dossier sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="fc805-121">Extract hello .tar.gz file tooa folder in your computer.</span></span>
3. <span data-ttu-id="fc805-122">Projet de hello d’avec le bouton droit et sélectionnez **ajouter des fichiers à**.</span><span class="sxs-lookup"><span data-stu-id="fc805-122">Right-click hello project, and then select **Add files to**.</span></span>

    ![][1]
4. <span data-ttu-id="fc805-123">Exploration du dossier toohello où vous avez extrait hello SDK, sélectionnez hello `EngagementSDK` dossier, cliquez sur **Options** hello coin inférieur gauche et assurez-vous que cette case à cocher hello **copier des éléments si nécessaire** et hello case à cocher pour votre cible sont cochées, puis appuyez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="fc805-123">Navigate toohello folder where you extracted hello SDK, select hello `EngagementSDK` folder, click **Options** on hello bottom left corner and make sure that hello checkbox **Copy items if needed** and hello checkbox for your target are checked then press **OK**.</span></span>

    ![][2]
5. <span data-ttu-id="fc805-124">Ouvrez hello **générer les Phases** onglet et Bonjour **binaire avec des bibliothèques de liens** menu, ajouter des infrastructures de hello comme indiqué ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="fc805-124">Open hello **Build Phases** tab, and in hello **Link Binary With Libraries** menu, add hello frameworks as shown below:</span></span>

    ![][3]
6. <span data-ttu-id="fc805-125">Revenir en arrière toohello portail Azure dans votre application **informations de connexion** page et copie la chaîne de connexion hello.</span><span class="sxs-lookup"><span data-stu-id="fc805-125">Go back toohello Azure portal in your app's **Connection Info** page and copy hello connection string.</span></span>

    ![][4]
7. <span data-ttu-id="fc805-126">Ajouter hello suivant la ligne de code dans votre **AppDelegate.m** fichier.</span><span class="sxs-lookup"><span data-stu-id="fc805-126">Add hello following line of code in your **AppDelegate.m** file.</span></span>

        #import "EngagementAgent.h"
8. <span data-ttu-id="fc805-127">Collez maintenant la chaîne de connexion hello Bonjour `didFinishLaunchingWithOptions` déléguer.</span><span class="sxs-lookup"><span data-stu-id="fc805-127">Now paste hello connection string in hello `didFinishLaunchingWithOptions` delegate.</span></span>

        - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
        {
              [...]   
              [EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}"];
              [...]
        }
9. <span data-ttu-id="fc805-128">`setTestLogEnabled`est une instruction facultative qui active les journaux du Kit de développement logiciel pour vous tooidentify problèmes.</span><span class="sxs-lookup"><span data-stu-id="fc805-128">`setTestLogEnabled` is an optional statement which enables SDK logs for you tooidentify issues.</span></span>

## <span data-ttu-id="fc805-129"><a id="monitor"></a>Activation de l’analyse en temps réel</span><span class="sxs-lookup"><span data-stu-id="fc805-129"><a id="monitor"></a>Enable real-time monitoring</span></span>
<span data-ttu-id="fc805-130">Dans l’ordre toostart envoi de données et en garantissant que les utilisateurs de hello sont actifs, vous devez envoyer au moins un principal de Mobile Engagement toohello écran (activité).</span><span class="sxs-lookup"><span data-stu-id="fc805-130">In order toostart sending data and ensuring that hello users are active, you must send at least one screen (Activity) toohello Mobile Engagement backend.</span></span>

1. <span data-ttu-id="fc805-131">Ouvrez hello **ViewController.h** de fichier et importer **EngagementViewController.h**:</span><span class="sxs-lookup"><span data-stu-id="fc805-131">Open hello **ViewController.h** file and import **EngagementViewController.h**:</span></span>

    `#import "EngagementViewController.h"`
2. <span data-ttu-id="fc805-132">Maintenant remplacer superclasse de hello Hello **ViewController** par l’interface `EngagementViewController`:</span><span class="sxs-lookup"><span data-stu-id="fc805-132">Now replace hello super class of hello **ViewController** interface by `EngagementViewController`:</span></span>

    `@interface ViewController : EngagementViewController`

## <span data-ttu-id="fc805-133"><a id="monitor"></a>Connexion d’application avec l’analyse en temps réel</span><span class="sxs-lookup"><span data-stu-id="fc805-133"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="fc805-134"><a id="integrate-push"></a>Activation des notifications push et de la messagerie in-app</span><span class="sxs-lookup"><span data-stu-id="fc805-134"><a id="integrate-push"></a>Enable push notifications and in-app messaging</span></span>
<span data-ttu-id="fc805-135">Mobile Engagement vous permet de toointeract avec vos utilisateurs et portée avec des notifications push et les messages dans le contexte de hello de campagnes dans l’application.</span><span class="sxs-lookup"><span data-stu-id="fc805-135">Mobile Engagement allows you toointeract with your users and REACH with push notifications and in-app messaging in hello context of campaigns.</span></span> <span data-ttu-id="fc805-136">Ce module est appelé portée dans le portail Mobile Engagement de hello.</span><span class="sxs-lookup"><span data-stu-id="fc805-136">This module is called REACH in hello Mobile Engagement portal.</span></span>
<span data-ttu-id="fc805-137">Hello sections suivantes configurer votre application tooreceive les.</span><span class="sxs-lookup"><span data-stu-id="fc805-137">hello following sections set up your app tooreceive them.</span></span>

### <a name="enable-your-app-tooreceive-silent-push-notifications"></a><span data-ttu-id="fc805-138">Activer votre tooreceive d’application en mode silencieux des Notifications Push</span><span class="sxs-lookup"><span data-stu-id="fc805-138">Enable your app tooreceive Silent Push Notifications</span></span>
[!INCLUDE [mobile-engagement-ios-silent-push](../../includes/mobile-engagement-ios-silent-push.md)]

### <a name="add-hello-reach-library-tooyour-project"></a><span data-ttu-id="fc805-139">Ajouter un projet de hello portée bibliothèque tooyour</span><span class="sxs-lookup"><span data-stu-id="fc805-139">Add hello Reach library tooyour project</span></span>
1. <span data-ttu-id="fc805-140">Cliquez avec le bouton droit sur votre projet.</span><span class="sxs-lookup"><span data-stu-id="fc805-140">Right-click your project.</span></span>
2. <span data-ttu-id="fc805-141">Sélectionnez **Add file to**.</span><span class="sxs-lookup"><span data-stu-id="fc805-141">Select **Add file to**.</span></span>
3. <span data-ttu-id="fc805-142">Parcourir le dossier toohello où vous avez extrait hello SDK.</span><span class="sxs-lookup"><span data-stu-id="fc805-142">Navigate toohello folder where you extracted hello SDK.</span></span>
4. <span data-ttu-id="fc805-143">Sélectionnez hello `EngagementReach` dossier.</span><span class="sxs-lookup"><span data-stu-id="fc805-143">Select hello `EngagementReach` folder.</span></span>
5. <span data-ttu-id="fc805-144">Cliquez sur **Add**.</span><span class="sxs-lookup"><span data-stu-id="fc805-144">Click **Add**.</span></span>

### <a name="modify-your-application-delegate"></a><span data-ttu-id="fc805-145">Modifier votre délégué d'Application</span><span class="sxs-lookup"><span data-stu-id="fc805-145">Modify your Application Delegate</span></span>
1. <span data-ttu-id="fc805-146">Dans les **AppDeletegate.m** de fichiers, importez le module d’Engagement atteindre hello.</span><span class="sxs-lookup"><span data-stu-id="fc805-146">Back in **AppDeletegate.m** file, import hello Engagement Reach module.</span></span>

        #import "AEReachModule.h"
        #import <UserNotifications/UserNotifications.h>
2. <span data-ttu-id="fc805-147">À l’intérieur hello `application:didFinishLaunchingWithOptions` (méthode), créer un module de couverture et passer en ligne de l’initialisation Engagement tooyour existante :</span><span class="sxs-lookup"><span data-stu-id="fc805-147">Inside hello `application:didFinishLaunchingWithOptions` method, create a Reach module and pass it tooyour existing Engagement initialization line:</span></span>

        - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
            AEReachModule * reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
            [EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}" modules:reach, nil];
            [...]
            return YES;
        }

### <a name="enable-your-app-tooreceive-apns-push-notifications"></a><span data-ttu-id="fc805-148">Activer votre tooreceive application APNS les Notifications Push</span><span class="sxs-lookup"><span data-stu-id="fc805-148">Enable your app tooreceive APNS Push Notifications</span></span>
1. <span data-ttu-id="fc805-149">Ajouter hello suivant ligne toohello `application:didFinishLaunchingWithOptions` méthode :</span><span class="sxs-lookup"><span data-stu-id="fc805-149">Add hello following line toohello `application:didFinishLaunchingWithOptions` method:</span></span>

        if (NSFoundationVersionNumber >= NSFoundationVersionNumber_iOS_8_0)
        {
            if (NSFoundationVersionNumber > NSFoundationVersionNumber_iOS_9_x_Max)
            {
                [UNUserNotificationCenter.currentNotificationCenter requestAuthorizationWithOptions:(UNAuthorizationOptionBadge | UNAuthorizationOptionSound | UNAuthorizationOptionAlert) completionHandler:^(BOOL granted, NSError * _Nullable error) {}];
            }else
            {
                [application registerUserNotificationSettings:[UIUserNotificationSettings settingsForTypes:(UIUserNotificationTypeBadge | UIUserNotificationTypeSound | UIUserNotificationTypeAlert)   categories:nil]];
            }
            [application registerForRemoteNotifications];
        }
        else
        {
            [application registerForRemoteNotificationTypes:(UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound | UIRemoteNotificationTypeAlert)];
        }
2. <span data-ttu-id="fc805-150">Ajouter hello `application:didRegisterForRemoteNotificationsWithDeviceToken` méthode comme suit :</span><span class="sxs-lookup"><span data-stu-id="fc805-150">Add hello `application:didRegisterForRemoteNotificationsWithDeviceToken` method as follows:</span></span>

        - (void)application:(UIApplication *)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken
        {
             [[EngagementAgent shared] registerDeviceToken:deviceToken];
            NSLog(@"Registered Token: %@", deviceToken);
        }
3. <span data-ttu-id="fc805-151">Ajouter hello `didFailToRegisterForRemoteNotificationsWithError` méthode comme suit :</span><span class="sxs-lookup"><span data-stu-id="fc805-151">Add hello `didFailToRegisterForRemoteNotificationsWithError` method as follows:</span></span>

        - (void)application:(UIApplication*)application didFailToRegisterForRemoteNotificationsWithError:(NSError*)error
        {
           NSLog(@"Failed tooget token, error: %@", error);
        }
4. <span data-ttu-id="fc805-152">Ajouter hello `didReceiveRemoteNotification:fetchCompletionHandler` méthode comme suit :</span><span class="sxs-lookup"><span data-stu-id="fc805-152">Add hello `didReceiveRemoteNotification:fetchCompletionHandler` method as follows:</span></span>

        - (void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo fetchCompletionHandler:(void (^)(UIBackgroundFetchResult result))handler
        {
            [[EngagementAgent shared] applicationDidReceiveRemoteNotification:userInfo fetchCompletionHandler:handler];
        }

[!INCLUDE [mobile-engagement-ios-send-push-push](../../includes/mobile-engagement-ios-send-push.md)]

<!-- URLs. -->
[Mobile Engagement iOS SDK]: http://aka.ms/qk2rnj

<!-- Images. -->
[1]: ./media/mobile-engagement-ios-get-started/xcode-add-files.png
[2]: ./media/mobile-engagement-ios-get-started/xcode-select-engagement-sdk.png
[3]: ./media/mobile-engagement-ios-get-started/xcode-build-phases.png
[4]: ./media/mobile-engagement-ios-get-started/app-connection-info-page.png
