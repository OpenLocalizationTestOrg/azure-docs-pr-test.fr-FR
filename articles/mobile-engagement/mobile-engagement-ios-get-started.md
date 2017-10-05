---
title: "Bien démarrer avec Azure Mobile Engagement pour iOS en Objective C | Microsoft Docs"
description: "Découvrez comment utiliser Azure Mobile Engagement avec les analyses et les notifications push pour les applications iOS."
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
ms.openlocfilehash: 1b87a2ebb35b31ee3d3139ecead6267e62eb1033
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-ios-apps-in-objective-c"></a><span data-ttu-id="906a3-103">Prise en main d’Azure Mobile Engagement pour les applications iOS dans Objective C</span><span class="sxs-lookup"><span data-stu-id="906a3-103">Get Started with Azure Mobile Engagement for iOS apps in Objective C</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="906a3-104">Cette rubrique indique comment utiliser Azure Mobile Engagement pour comprendre l’utilisation de votre application et envoyer des notifications push à un segment d’utilisateurs d’une application iOS.</span><span class="sxs-lookup"><span data-stu-id="906a3-104">This topic shows you how to use Azure Mobile Engagement to understand your app usage and send push notifications to segmented users to an iOS application.</span></span>
<span data-ttu-id="906a3-105">Dans ce didacticiel, vous créez une application iOS vide qui collecte des données de base et reçoit des notifications push à l'aide du service APN (Apple Push Notification Service).</span><span class="sxs-lookup"><span data-stu-id="906a3-105">In this tutorial, you create a blank iOS app that collects basic data and receives push notifications using Apple Push Notification System (APNS).</span></span>

<span data-ttu-id="906a3-106">Ce didacticiel requiert les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="906a3-106">This tutorial requires the following:</span></span>

* <span data-ttu-id="906a3-107">XCode 8, que vous pouvez installer depuis l’App Store de votre MAC</span><span class="sxs-lookup"><span data-stu-id="906a3-107">XCode 8, which you can install from your MAC App Store</span></span>
* <span data-ttu-id="906a3-108">Le [kit de développement logiciel (SDK) iOS Mobile Engagement]</span><span class="sxs-lookup"><span data-stu-id="906a3-108">the [Mobile Engagement iOS SDK]</span></span>

<span data-ttu-id="906a3-109">Vous devez suivre ce didacticiel pour avoir accès à tous les autres didacticiels Mobile Engagement pour applications iOS.</span><span class="sxs-lookup"><span data-stu-id="906a3-109">Completing this tutorial is a prerequisite for all other Mobile Engagement tutorials for iOS apps.</span></span>

> [!NOTE]
> <span data-ttu-id="906a3-110">Pour suivre ce didacticiel, vous avez besoin d'un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="906a3-110">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="906a3-111">Si vous ne possédez pas de compte, vous pouvez créer un compte d'évaluation gratuit en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="906a3-111">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="906a3-112">Pour plus d'informations, consultez la page [Version d'évaluation gratuite d'Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-ios-get-started).</span><span class="sxs-lookup"><span data-stu-id="906a3-112">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-ios-get-started).</span></span>
>
>

## <span data-ttu-id="906a3-113"><a id="setup-azme"></a>Configuration de Mobile Engagement pour votre application iOS</span><span class="sxs-lookup"><span data-stu-id="906a3-113"><a id="setup-azme"></a>Setup Mobile Engagement for your iOS app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="906a3-114"><a id="connecting-app"></a>Connexion de votre application au serveur principal Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="906a3-114"><a id="connecting-app"></a>Connect your app to the Mobile Engagement backend</span></span>
<span data-ttu-id="906a3-115">Ce didacticiel aborde l'intégration de base qui correspond aux éléments nécessaires à la collection de données et à l'envoi de notifications push.</span><span class="sxs-lookup"><span data-stu-id="906a3-115">This tutorial presents a "basic integration", which is the minimal set required to collect data and send a push notification.</span></span> <span data-ttu-id="906a3-116">Vous trouverez la documentation complète sur l’intégration dans [Intégration du Kit de développement logiciel (SDK) iOS Mobile Engagement](mobile-engagement-ios-sdk-overview.md)</span><span class="sxs-lookup"><span data-stu-id="906a3-116">The complete integration documentation can be found in the [Mobile Engagement iOS SDK integration](mobile-engagement-ios-sdk-overview.md)</span></span>

<span data-ttu-id="906a3-117">Nous allons créer une application de base à l’aide de XCode afin d’illustrer l’intégration :</span><span class="sxs-lookup"><span data-stu-id="906a3-117">We will create a basic app with XCode to demonstrate the integration.</span></span>

### <a name="create-a-new-ios-project"></a><span data-ttu-id="906a3-118">Création d’un projet iOS</span><span class="sxs-lookup"><span data-stu-id="906a3-118">Create a new iOS project</span></span>
[!INCLUDE [Create a new iOS Project](../../includes/mobile-engagement-create-new-ios-app.md)]

### <a name="connect-your-app-to-the-mobile-engagement-backend"></a><span data-ttu-id="906a3-119">Connexion de votre application au serveur principal Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="906a3-119">Connect your app to the Mobile Engagement backend</span></span>
1. <span data-ttu-id="906a3-120">Téléchargez le [kit de développement logiciel (SDK) iOS Mobile Engagement]</span><span class="sxs-lookup"><span data-stu-id="906a3-120">Download the [Mobile Engagement iOS SDK].</span></span>
2. <span data-ttu-id="906a3-121">Décompressez le fichier .tar.gz dans un dossier de votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="906a3-121">Extract the .tar.gz file to a folder in your computer.</span></span>
3. <span data-ttu-id="906a3-122">Cliquez avec le bouton droit sur le projet, puis sélectionnez **Add files to**.</span><span class="sxs-lookup"><span data-stu-id="906a3-122">Right-click the project, and then select **Add files to**.</span></span>

    ![][1]
4. <span data-ttu-id="906a3-123">Accédez au dossier dans lequel vous avez extrait le kit de développement logiciel (SDK), sélectionnez le dossier `EngagementSDK`, cliquez sur **Options** dans le coin inférieur gauche et assurez-vous que la case **Copier les éléments si besoin** et la case correspondant à votre cible sont cochées, puis appuyez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="906a3-123">Navigate to the folder where you extracted the SDK, select the `EngagementSDK` folder, click **Options** on the bottom left corner and make sure that the checkbox **Copy items if needed** and the checkbox for your target are checked then press **OK**.</span></span>

    ![][2]
5. <span data-ttu-id="906a3-124">Ouvrez l’onglet **Build Phases** (Générer des phases), puis, dans le menu **Liaisons binaires à des bibliothèques**, ajoutez les infrastructures comme indiqué ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="906a3-124">Open the **Build Phases** tab, and in the **Link Binary With Libraries** menu, add the frameworks as shown below:</span></span>

    ![][3]
6. <span data-ttu-id="906a3-125">De retour sur le portail Azure, dans la page **Informations de connexion** de votre application, copiez la chaîne de connexion.</span><span class="sxs-lookup"><span data-stu-id="906a3-125">Go back to the Azure portal in your app's **Connection Info** page and copy the connection string.</span></span>

    ![][4]
7. <span data-ttu-id="906a3-126">Dans le fichier **AppDelegate.m** , ajoutez la ligne de code suivante.</span><span class="sxs-lookup"><span data-stu-id="906a3-126">Add the following line of code in your **AppDelegate.m** file.</span></span>

        #import "EngagementAgent.h"
8. <span data-ttu-id="906a3-127">Collez la chaîne de connexion dans le délégué `didFinishLaunchingWithOptions`</span><span class="sxs-lookup"><span data-stu-id="906a3-127">Now paste the connection string in the `didFinishLaunchingWithOptions` delegate.</span></span>

        - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
        {
              [...]   
              [EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}"];
              [...]
        }
9. <span data-ttu-id="906a3-128">`setTestLogEnabled` est une instruction facultative qui active les journaux du Kit de développement logiciel (SDK) pour vous permettre d’identifier des problèmes.</span><span class="sxs-lookup"><span data-stu-id="906a3-128">`setTestLogEnabled` is an optional statement which enables SDK logs for you to identify issues.</span></span>

## <span data-ttu-id="906a3-129"><a id="monitor"></a>Activation de l’analyse en temps réel</span><span class="sxs-lookup"><span data-stu-id="906a3-129"><a id="monitor"></a>Enable real-time monitoring</span></span>
<span data-ttu-id="906a3-130">Pour commencer à envoyer des données et vous assurer que les utilisateurs sont actifs, vous devez envoyer au moins un écran (activité) au serveur principal Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="906a3-130">In order to start sending data and ensuring that the users are active, you must send at least one screen (Activity) to the Mobile Engagement backend.</span></span>

1. <span data-ttu-id="906a3-131">Ouvrez le fichier **ViewController.h** et importez l’élément **EngagementViewController.h** :</span><span class="sxs-lookup"><span data-stu-id="906a3-131">Open the **ViewController.h** file and import **EngagementViewController.h**:</span></span>

    `#import "EngagementViewController.h"`
2. <span data-ttu-id="906a3-132">Remplacez maintenant la super classe de l’interface **ViewController** par `EngagementViewController` :</span><span class="sxs-lookup"><span data-stu-id="906a3-132">Now replace the super class of the **ViewController** interface by `EngagementViewController`:</span></span>

    `@interface ViewController : EngagementViewController`

## <span data-ttu-id="906a3-133"><a id="monitor"></a>Connexion d’application avec l’analyse en temps réel</span><span class="sxs-lookup"><span data-stu-id="906a3-133"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="906a3-134"><a id="integrate-push"></a>Activation des notifications push et de la messagerie in-app</span><span class="sxs-lookup"><span data-stu-id="906a3-134"><a id="integrate-push"></a>Enable push notifications and in-app messaging</span></span>
<span data-ttu-id="906a3-135">Mobile Engagement vous permet d’interagir et d’atteindre vos utilisateurs et REACH à l’aide de notifications push et de la messagerie in-app, dans le cadre d’une campagne.</span><span class="sxs-lookup"><span data-stu-id="906a3-135">Mobile Engagement allows you to interact with your users and REACH with push notifications and in-app messaging in the context of campaigns.</span></span> <span data-ttu-id="906a3-136">Ce module s'appelle Couverture dans le portail Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="906a3-136">This module is called REACH in the Mobile Engagement portal.</span></span>
<span data-ttu-id="906a3-137">Les sections suivantes vous permettent de configurer votre application pour la réception.</span><span class="sxs-lookup"><span data-stu-id="906a3-137">The following sections set up your app to receive them.</span></span>

### <a name="enable-your-app-to-receive-silent-push-notifications"></a><span data-ttu-id="906a3-138">Activer votre application pour recevoir des notifications push Silent</span><span class="sxs-lookup"><span data-stu-id="906a3-138">Enable your app to receive Silent Push Notifications</span></span>
[!INCLUDE [mobile-engagement-ios-silent-push](../../includes/mobile-engagement-ios-silent-push.md)]

### <a name="add-the-reach-library-to-your-project"></a><span data-ttu-id="906a3-139">Ajoutez la bibliothèque du module Couverture à votre projet</span><span class="sxs-lookup"><span data-stu-id="906a3-139">Add the Reach library to your project</span></span>
1. <span data-ttu-id="906a3-140">Cliquez avec le bouton droit sur votre projet.</span><span class="sxs-lookup"><span data-stu-id="906a3-140">Right-click your project.</span></span>
2. <span data-ttu-id="906a3-141">Sélectionnez **Add file to**.</span><span class="sxs-lookup"><span data-stu-id="906a3-141">Select **Add file to**.</span></span>
3. <span data-ttu-id="906a3-142">Accédez au dossier dans lequel vous avez extrait le SDK.</span><span class="sxs-lookup"><span data-stu-id="906a3-142">Navigate to the folder where you extracted the SDK.</span></span>
4. <span data-ttu-id="906a3-143">Sélectionnez le dossier `EngagementReach` .</span><span class="sxs-lookup"><span data-stu-id="906a3-143">Select the `EngagementReach` folder.</span></span>
5. <span data-ttu-id="906a3-144">Cliquez sur **Add**.</span><span class="sxs-lookup"><span data-stu-id="906a3-144">Click **Add**.</span></span>

### <a name="modify-your-application-delegate"></a><span data-ttu-id="906a3-145">Modifier votre délégué d'Application</span><span class="sxs-lookup"><span data-stu-id="906a3-145">Modify your Application Delegate</span></span>
1. <span data-ttu-id="906a3-146">Dans le fichier **AppDeletegate.m** , importez le module Couverture d'Engagement.</span><span class="sxs-lookup"><span data-stu-id="906a3-146">Back in **AppDeletegate.m** file, import the Engagement Reach module.</span></span>

        #import "AEReachModule.h"
        #import <UserNotifications/UserNotifications.h>
2. <span data-ttu-id="906a3-147">Dans la méthode `application:didFinishLaunchingWithOptions` , créez un module Couverture et passez-le à votre ligne d’initialisation Engagement existante :</span><span class="sxs-lookup"><span data-stu-id="906a3-147">Inside the `application:didFinishLaunchingWithOptions` method, create a Reach module and pass it to your existing Engagement initialization line:</span></span>

        - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
            AEReachModule * reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
            [EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}" modules:reach, nil];
            [...]
            return YES;
        }

### <a name="enable-your-app-to-receive-apns-push-notifications"></a><span data-ttu-id="906a3-148">Activez votre application pour recevoir des notifications push du service APN</span><span class="sxs-lookup"><span data-stu-id="906a3-148">Enable your app to receive APNS Push Notifications</span></span>
1. <span data-ttu-id="906a3-149">Ajoutez la ligne suivante à la méthode `application:didFinishLaunchingWithOptions` :</span><span class="sxs-lookup"><span data-stu-id="906a3-149">Add the following line to the `application:didFinishLaunchingWithOptions` method:</span></span>

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
2. <span data-ttu-id="906a3-150">Ajoutez la méthode `application:didRegisterForRemoteNotificationsWithDeviceToken` comme suit :</span><span class="sxs-lookup"><span data-stu-id="906a3-150">Add the `application:didRegisterForRemoteNotificationsWithDeviceToken` method as follows:</span></span>

        - (void)application:(UIApplication *)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken
        {
             [[EngagementAgent shared] registerDeviceToken:deviceToken];
            NSLog(@"Registered Token: %@", deviceToken);
        }
3. <span data-ttu-id="906a3-151">Ajoutez la méthode `didFailToRegisterForRemoteNotificationsWithError` comme suit :</span><span class="sxs-lookup"><span data-stu-id="906a3-151">Add the `didFailToRegisterForRemoteNotificationsWithError` method as follows:</span></span>

        - (void)application:(UIApplication*)application didFailToRegisterForRemoteNotificationsWithError:(NSError*)error
        {
           NSLog(@"Failed to get token, error: %@", error);
        }
4. <span data-ttu-id="906a3-152">Ajoutez la méthode `didReceiveRemoteNotification:fetchCompletionHandler` comme suit :</span><span class="sxs-lookup"><span data-stu-id="906a3-152">Add the `didReceiveRemoteNotification:fetchCompletionHandler` method as follows:</span></span>

        - (void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo fetchCompletionHandler:(void (^)(UIBackgroundFetchResult result))handler
        {
            [[EngagementAgent shared] applicationDidReceiveRemoteNotification:userInfo fetchCompletionHandler:handler];
        }

[!INCLUDE [mobile-engagement-ios-send-push-push](../../includes/mobile-engagement-ios-send-push.md)]

<!-- URLs. -->
<span data-ttu-id="906a3-153">[kit de développement logiciel (SDK) iOS Mobile Engagement]: http://aka.ms/qk2rnj</span><span class="sxs-lookup"><span data-stu-id="906a3-153">[Mobile Engagement iOS SDK]: http://aka.ms/qk2rnj</span></span>

<!-- Images. -->
[1]: ./media/mobile-engagement-ios-get-started/xcode-add-files.png
[2]: ./media/mobile-engagement-ios-get-started/xcode-select-engagement-sdk.png
[3]: ./media/mobile-engagement-ios-get-started/xcode-build-phases.png
[4]: ./media/mobile-engagement-ios-get-started/app-connection-info-page.png
