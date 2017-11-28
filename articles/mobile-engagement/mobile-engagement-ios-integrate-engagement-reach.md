---
title: "Intégration Reach du SDK iOS Azure Mobile Engagement | Microsoft Docs"
description: "Dernières mises à jour et procédures du Kit de développement logiciel (SDK) iOS pour Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 1f5f5857-867c-40c5-9d76-675a343a0296
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 12/13/2016
ms.author: piyushjo
ms.openlocfilehash: ba74e0c442ac10f096d465f989e03d2ceae8cd88
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-integrate-engagement-reach-on-ios"></a><span data-ttu-id="f7f3b-103">Comment intégrer Engagement Reach sur iOS</span><span class="sxs-lookup"><span data-stu-id="f7f3b-103">How to Integrate Engagement Reach on iOS</span></span>
<span data-ttu-id="f7f3b-104">Vous devez suivre la procédure d'intégration décrite dans la procédure [Intégration d'Engagement sur un document iOS](mobile-engagement-ios-integrate-engagement.md) avant de suivre ce guide.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-104">You must follow the integration procedure described in the [How to Integrate Engagement on iOS document](mobile-engagement-ios-integrate-engagement.md) before following this guide.</span></span>

<span data-ttu-id="f7f3b-105">Cette documentation nécessite XCode 8.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-105">This documentation requires XCode 8.</span></span> <span data-ttu-id="f7f3b-106">Si vous dépendez vraiment de XCode 7, vous pouvez utiliser [iOS SDK Engagement v3.2.4](https://aka.ms/r6oouh).</span><span class="sxs-lookup"><span data-stu-id="f7f3b-106">If you really depend on XCode 7 then you may use the [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh).</span></span> <span data-ttu-id="f7f3b-107">Il existe un bogue connu concernant cette version précédente quand elle est exécutée sur des appareils iOS 10 : les notifications système ne sont pas activées.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-107">There is a known bug on this previous version while running on iOS 10 devices:  system notifications are not actioned.</span></span> <span data-ttu-id="f7f3b-108">Pour corriger ce problème, vous devez implémenter l’API déconseillée `application:didReceiveRemoteNotification:` dans votre délégué d’application comme suit :</span><span class="sxs-lookup"><span data-stu-id="f7f3b-108">To fix this you will have to implement the deprecated API `application:didReceiveRemoteNotification:` in your app delegate as follows:</span></span>

    - (void)application:(UIApplication*)application
    didReceiveRemoteNotification:(NSDictionary*)userInfo
    {
        [[EngagementAgent shared] applicationDidReceiveRemoteNotification:userInfo fetchCompletionHandler:nil];
    }

> [!IMPORTANT]
> <span data-ttu-id="f7f3b-109">**Nous ne recommandons pas cette solution de contournement** : ce comportement peut changer dans une prochaine mise à niveau (même mineure) de la version iOS car cette API iOS est déconseillée.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-109">**We do not recommend this workaround** as this behavior can change in any upcoming (even minor) iOS version upgrade because this iOS API is deprecated.</span></span> <span data-ttu-id="f7f3b-110">Vous devriez passer à XCode 8 dès que possible.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-110">You should switch to XCode 8 as soon as possible.</span></span>
>
>

### <a name="enable-your-app-to-receive-silent-push-notifications"></a><span data-ttu-id="f7f3b-111">Activer votre application pour recevoir des notifications Push Silent</span><span class="sxs-lookup"><span data-stu-id="f7f3b-111">Enable your app to receive Silent Push Notifications</span></span>
[!INCLUDE [mobile-engagement-ios-silent-push](../../includes/mobile-engagement-ios-silent-push.md)]

## <a name="integration-steps"></a><span data-ttu-id="f7f3b-112">Étapes d'intégration</span><span class="sxs-lookup"><span data-stu-id="f7f3b-112">Integration steps</span></span>
### <a name="embed-the-engagement-reach-sdk-into-your-ios-project"></a><span data-ttu-id="f7f3b-113">Incorporez le Kit de développement logiciel (SDK) Engagement Reach dans votre projet iOS</span><span class="sxs-lookup"><span data-stu-id="f7f3b-113">Embed the Engagement Reach SDK into your iOS project</span></span>
* <span data-ttu-id="f7f3b-114">Ajoutez le Kit de développement logiciel (SDK) Reach dans votre projet Xcode.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-114">Add the Reach sdk in your Xcode project.</span></span> <span data-ttu-id="f7f3b-115">Dans Xcode, accédez à **Projet \> Ajouter au projet** et choisissez le dossier `EngagementReach`.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-115">In Xcode, go to **Project \> Add to project** and choose the `EngagementReach` folder.</span></span>

### <a name="modify-your-application-delegate"></a><span data-ttu-id="f7f3b-116">Modifier votre délégué d'Application</span><span class="sxs-lookup"><span data-stu-id="f7f3b-116">Modify your Application Delegate</span></span>
* <span data-ttu-id="f7f3b-117">En haut de votre fichier d'implémentation, importez le module Engagement Reach :</span><span class="sxs-lookup"><span data-stu-id="f7f3b-117">At the top of your implementation file, import the Engagement Reach module:</span></span>

      [...]
      #import "AEReachModule.h"
* <span data-ttu-id="f7f3b-118">Dans la méthode `applicationDidFinishLaunching:` ou `application:didFinishLaunchingWithOptions:`, créez un module Reach et transmettez-le à la ligne d'initialisation d’Engagement existante :</span><span class="sxs-lookup"><span data-stu-id="f7f3b-118">Inside method `applicationDidFinishLaunching:` or `application:didFinishLaunchingWithOptions:`, create a reach module and pass it to your existing Engagement initialization line:</span></span>

      - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
        AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
        [EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}" modules:reach, nil];
        [...]

        return YES;
      }
* <span data-ttu-id="f7f3b-119">Modifiez la chaîne **icon.png** avec le nom de l'image que vous souhaitez en tant qu'icône de notification.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-119">Modify **'icon.png'** string with the image name you want as your notification icon.</span></span>
* <span data-ttu-id="f7f3b-120">Si vous voulez utiliser l’option *Update badge value*dans des campagnes Reach ou si vous voulez utiliser des campagnes \<</SaaS/Reach API/Campaign format/Native Push>\> de type Push natives, vous devez laisser le module Reach gérer l’icône de badge lui-même (il efface automatiquement le badge de l’application et réinitialise également la valeur stockée par Engagement lors de chaque démarrage ou mise au premier plan de l’application).</span><span class="sxs-lookup"><span data-stu-id="f7f3b-120">If you want to use the option *Update badge value* in Reach campaigns or if you want to use native push \</SaaS/Reach API/Campaign format/Native Push\> campaigns, you must let the Reach module manage the badge icon itself (it will automatically clear the application badge and also reset the value stored by Engagement every time the application is started or foregrounded).</span></span> <span data-ttu-id="f7f3b-121">Pour cela, ajoutez la ligne suivante après l'initialisation de module Reach :</span><span class="sxs-lookup"><span data-stu-id="f7f3b-121">This is done by adding the following line after Reach module initialization:</span></span>

      [reach setAutoBadgeEnabled:YES];
* <span data-ttu-id="f7f3b-122">Si vous souhaitez gérer le Push des données Reach, vous devez laisser votre délégué d'application se conformer au protocole `AEReachDataPushDelegate` .</span><span class="sxs-lookup"><span data-stu-id="f7f3b-122">If you want to handle Reach data push, you must let your Application delegate conform to the `AEReachDataPushDelegate` protocol.</span></span> <span data-ttu-id="f7f3b-123">Ajoutez la ligne suivante après l'initialisation de module Reach :</span><span class="sxs-lookup"><span data-stu-id="f7f3b-123">Add the following line after Reach module initialization:</span></span>

      [reach setDataPushDelegate:self];
* <span data-ttu-id="f7f3b-124">Vous pourrez ensuite implémenter les méthodes `onDataPushStringReceived:` et `onDataPushBase64ReceivedWithDecodedBody:andEncodedBody:` dans votre délégué d'application :</span><span class="sxs-lookup"><span data-stu-id="f7f3b-124">Then you can implement the methods `onDataPushStringReceived:` and `onDataPushBase64ReceivedWithDecodedBody:andEncodedBody:` in your application delegate:</span></span>

      -(BOOL)didReceiveStringDataPushWithCategory:(NSString*)category body:(NSString*)body
      {
         NSLog(@"String data push message with category <%@> received: %@", category, body);
         return YES;
      }

      -(BOOL)didReceiveBase64DataPushWithCategory:(NSString*)category decodedBody:(NSData *)decodedBody encodedBody:(NSString *)encodedBody
      {
         NSLog(@"Base64 data push message with category <%@> received: %@", category, encodedBody);
         // Do something useful with decodedBody like updating an image view
         return YES;
      }

### <a name="category"></a><span data-ttu-id="f7f3b-125">Catégorie</span><span class="sxs-lookup"><span data-stu-id="f7f3b-125">Category</span></span>
<span data-ttu-id="f7f3b-126">Le paramètre de catégorie est facultatif lorsque vous créez une campagne d'envoi de données (push) et vous permet de filtrer les envois de données.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-126">The category parameter is optional when you create a Data Push campaign and allows you to filter data pushes.</span></span> <span data-ttu-id="f7f3b-127">Cela s’avère utile si vous souhaitez effectuer une transmission de type push pour différents types de données `Base64` et que vous souhaitez identifier leur type avant de les analyser.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-127">This is useful if you want to push different kinds of `Base64` data and want to identify their type before parsing them.</span></span>

<span data-ttu-id="f7f3b-128">**Votre application est prête à recevoir et à afficher des contenus Reach !**</span><span class="sxs-lookup"><span data-stu-id="f7f3b-128">**Your application is now ready to receive and display reach contents!**</span></span>

## <a name="how-to-receive-announcements-and-polls-at-any-time"></a><span data-ttu-id="f7f3b-129">Réception des annonces et des sondages à tout moment</span><span class="sxs-lookup"><span data-stu-id="f7f3b-129">How to receive announcements and polls at any time</span></span>
<span data-ttu-id="f7f3b-130">Engagement peut envoyer des notifications Reach à vos utilisateurs finaux à tout moment en utilisant le Service de Notifications Push Apple.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-130">Engagement can send Reach notifications to your end users at any time by using the Apple Push Notification Service.</span></span>

<span data-ttu-id="f7f3b-131">Pour activer cette fonctionnalité, vous devrez préparer votre application pour les notifications Push Apple et modifier votre délégué d'application.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-131">To enable this functionality, you'll have to prepare your application for Apple push notifications and modify your application delegate.</span></span>

### <a name="prepare-your-application-for-apple-push-notifications"></a><span data-ttu-id="f7f3b-132">Préparer votre application pour les notifications Push Apple</span><span class="sxs-lookup"><span data-stu-id="f7f3b-132">Prepare your application for Apple push notifications</span></span>
<span data-ttu-id="f7f3b-133">Veuillez suivre le guide [Préparation de votre Application pour les notifications Push Apple](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html#//apple_ref/doc/uid/TP40012582-CH26-SW6)</span><span class="sxs-lookup"><span data-stu-id="f7f3b-133">Please follow the guide : [How to Prepare your Application for Apple Push Notifications](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html#//apple_ref/doc/uid/TP40012582-CH26-SW6)</span></span>

### <a name="add-the-necessary-client-code"></a><span data-ttu-id="f7f3b-134">Ajoutez le code client nécessaire</span><span class="sxs-lookup"><span data-stu-id="f7f3b-134">Add the necessary client code</span></span>
<span data-ttu-id="f7f3b-135">*À ce stade, votre application doit avoir un certificat Push Apple enregistré dans le serveur frontal d'Engagement.*</span><span class="sxs-lookup"><span data-stu-id="f7f3b-135">*At this point your application should have a registered Apple push certificate in the Engagement frontend.*</span></span>

<span data-ttu-id="f7f3b-136">Si ce n'est pas encore le cas, vous devez inscrire votre application afin de recevoir des notifications push.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-136">If it's not done already, you need to register your application to receive push notifications.</span></span>

* <span data-ttu-id="f7f3b-137">Importez l’infrastructure de `User Notification` :</span><span class="sxs-lookup"><span data-stu-id="f7f3b-137">Import the `User Notification` framework:</span></span>

        #import <UserNotifications/UserNotifications.h>
* <span data-ttu-id="f7f3b-138">Ajoutez la ligne suivante au démarrage de votre application (en général, dans `application:didFinishLaunchingWithOptions:`) :</span><span class="sxs-lookup"><span data-stu-id="f7f3b-138">Add the following line when your application starts (typically in `application:didFinishLaunchingWithOptions:`):</span></span>

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

<span data-ttu-id="f7f3b-139">Ensuite, vous devez fournir à Engagement le jeton de périphérique retourné par les serveurs Apple.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-139">Then, You need to provide to Engagement the device token returned by Apple servers.</span></span> <span data-ttu-id="f7f3b-140">Cette opération est effectuée dans la méthode appelée `application:didRegisterForRemoteNotificationsWithDeviceToken:` dans votre délégué d'application :</span><span class="sxs-lookup"><span data-stu-id="f7f3b-140">This is done in the method named `application:didRegisterForRemoteNotificationsWithDeviceToken:` in your application delegate:</span></span>

    - (void)application:(UIApplication*)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData*)deviceToken
    {
        [[EngagementAgent shared] registerDeviceToken:deviceToken];
    }

<span data-ttu-id="f7f3b-141">Enfin, vous devez informer le Kit de développement logiciel (SDK) Engagement lorsque votre application reçoit une notification à distance.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-141">Finally, you have to inform the Engagement SDK when your application receives a remote notification.</span></span> <span data-ttu-id="f7f3b-142">Pour cela, appelez la méthode `applicationDidReceiveRemoteNotification:fetchCompletionHandler:` dans votre délégué d'application :</span><span class="sxs-lookup"><span data-stu-id="f7f3b-142">To do that, call the method `applicationDidReceiveRemoteNotification:fetchCompletionHandler:` in your application delegate:</span></span>

    - (void)application:(UIApplication*)application didReceiveRemoteNotification:(NSDictionary*)userInfo fetchCompletionHandler:(void (^)(UIBackgroundFetchResult result))handler
    {
        [[EngagementAgent shared] applicationDidReceiveRemoteNotification:userInfo fetchCompletionHandler:handler];
    }

> [!IMPORTANT]
> <span data-ttu-id="f7f3b-143">Par défaut, Engagement Reach contrôle le completionHandler.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-143">By default, Engagement Reach controls the completionHandler.</span></span> <span data-ttu-id="f7f3b-144">Si vous souhaitez répondre manuellement au bloc `handler` de votre code, vous pouvez utiliser nil pour l’argument `handler` et contrôler le bloc de fin vous-même.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-144">If you want to manually respond to the `handler` block in your code, you can pass nil for the `handler` argument and control the completion block yourself.</span></span> <span data-ttu-id="f7f3b-145">Consultez le type `UIBackgroundFetchResult` d'une liste de valeurs possibles.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-145">See the `UIBackgroundFetchResult` type for a list of possible values.</span></span>
>
>

### <a name="full-example"></a><span data-ttu-id="f7f3b-146">Exemple complet</span><span class="sxs-lookup"><span data-stu-id="f7f3b-146">Full example</span></span>
<span data-ttu-id="f7f3b-147">Voici un exemple complet d'intégration :</span><span class="sxs-lookup"><span data-stu-id="f7f3b-147">Here is a full example of integration:</span></span>

    #pragma mark -
    #pragma mark Application lifecycle

    - (BOOL)application:(UIApplication*)application didFinishLaunchingWithOptions:(NSDictionary*)launchOptions
    {
      /* Reach module */
      AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
      [reach setAutoBadgeEnabled:YES];

      /* Engagement initialization */
      [EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}" modules:reach, nil];
      [[EngagementAgent shared] setPushDelegate:self];

      /* Views */
      [window addSubview:[tabBarController view]];
      [window makeKeyAndVisible];

      [application registerForRemoteNotificationTypes:UIRemoteNotificationTypeAlert|UIRemoteNotificationTypeBadge|UIRemoteNotificationTypeSound];
      return YES;
    }

    - (void)application:(UIApplication*)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData*)deviceToken
    {
      [[EngagementAgent shared] registerDeviceToken:deviceToken];
    }

    - (void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo fetchCompletionHandler:(void (^)(UIBackgroundFetchResult result))handler
    {
        [[EngagementAgent shared] applicationDidReceiveRemoteNotification:userInfo fetchCompletionHandler:handler];
    }

### <a name="resolve-unusernotificationcenter-delegate-conflicts"></a><span data-ttu-id="f7f3b-148">Résoudre les conflits de délégué UNUserNotificationCenter</span><span class="sxs-lookup"><span data-stu-id="f7f3b-148">Resolve UNUserNotificationCenter delegate conflicts</span></span>

<span data-ttu-id="f7f3b-149">*Si, ni votre application ni l’une des bibliothèques tierces n’implémente un `UNUserNotificationCenterDelegate`, vous pouvez ignorer cette partie.*</span><span class="sxs-lookup"><span data-stu-id="f7f3b-149">*If neither your application or one of your third party libraries implements a `UNUserNotificationCenterDelegate` then you can skip this part.*</span></span>

<span data-ttu-id="f7f3b-150">Un délégué `UNUserNotificationCenter` est utilisé par le Kit de développement logiciel (SDK) pour surveiller le cycle de vie des notifications Engagement sur les appareils iOS 10 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-150">A `UNUserNotificationCenter` delegate is used by the SDK to monitor the life cycle of Engagement notifications on devices running on iOS 10 or greater.</span></span> <span data-ttu-id="f7f3b-151">Le Kit de développement logiciel (SDK) a sa propre implémentation du protocole `UNUserNotificationCenterDelegate`, mais il ne peut y avoir qu’un seul délégué `UNUserNotificationCenter` par application.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-151">The SDK has its own implementation of the `UNUserNotificationCenterDelegate` protocol but there can be only one `UNUserNotificationCenter` delegate per application.</span></span> <span data-ttu-id="f7f3b-152">Tout autre délégué ajouté à l’objet `UNUserNotificationCenter` est en conflit avec celui d’Engagement.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-152">Any other delegate added to the `UNUserNotificationCenter` object will conflict with the Engagement one.</span></span> <span data-ttu-id="f7f3b-153">Si le Kit de développement logiciel (SDK) détecte votre délégué ou un délégué tiers, il n’utilisera pas sa propre implémentation pour vous permettre de résoudre les conflits.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-153">If the SDK detects your or any other third party's delegate then it will not use its own implementation to give you a chance to resolve the conflicts.</span></span> <span data-ttu-id="f7f3b-154">Vous devrez ajouter la logique d’Engagement à votre propre délégué afin de résoudre les conflits.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-154">You will have to add the Engagement logic to your own delegate in order to resolve the conflicts.</span></span>

<span data-ttu-id="f7f3b-155">Il existe deux moyens de parvenir à cet objectif.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-155">There are two ways to achieve this.</span></span>

<span data-ttu-id="f7f3b-156">1re méthode : en transférant les appels de votre délégué au kit de développement logiciel (SDK).</span><span class="sxs-lookup"><span data-stu-id="f7f3b-156">Proposal 1, simply by forwarding your delegate calls to the SDK:</span></span>

    #import <UIKit/UIKit.h>
    #import "EngagementAgent.h"
    #import <UserNotifications/UserNotifications.h>


    @interface MyAppDelegate : NSObject <UIApplicationDelegate, UNUserNotificationCenterDelegate>
    @end

    @implementation MyAppDelegate

    - (void)userNotificationCenter:(UNUserNotificationCenter *)center willPresentNotification:(UNNotification *)notification withCompletionHandler:(void (^)(UNNotificationPresentationOptions options))completionHandler
    {
      // Your own logic.

      [[EngagementAgent shared] userNotificationCenterWillPresentNotification:notification withCompletionHandler:completionHandler]
    }

    - (void)userNotificationCenter:(UNUserNotificationCenter *)center didReceiveNotificationResponse:(UNNotificationResponse *)response withCompletionHandler:(void(^)())completionHandler
    {
      // Your own logic.

      [[EngagementAgent shared] userNotificationCenterDidReceiveNotificationResponse:response withCompletionHandler:completionHandler]
    }
    @end

<span data-ttu-id="f7f3b-157">2e méthode : en héritant de la classe `AEUserNotificationHandler`</span><span class="sxs-lookup"><span data-stu-id="f7f3b-157">Or proposal 2, by inheriting from the `AEUserNotificationHandler` class</span></span>

    #import "AEUserNotificationHandler.h"
    #import "EngagementAgent.h"

    @interface CustomUserNotificationHandler :AEUserNotificationHandler
    @end

    @implementation CustomUserNotificationHandler

    - (void)userNotificationCenter:(UNUserNotificationCenter *)center willPresentNotification:(UNNotification *)notification withCompletionHandler:(void (^)(UNNotificationPresentationOptions options))completionHandler
    {
      // Your own logic.

      [super userNotificationCenter:center willPresentNotification:notification withCompletionHandler:completionHandler];
    }

    - (void)userNotificationCenter:(UNUserNotificationCenter *)center didReceiveNotificationResponse: UNNotificationResponse *)response withCompletionHandler:(void(^)())completionHandler
    {
      // Your own logic.

      [super userNotificationCenter:center didReceiveNotificationResponse:response withCompletionHandler:completionHandler];
    }

    @end

> [!NOTE]
> <span data-ttu-id="f7f3b-158">Vous pouvez déterminer si une notification provient ou non d’Engagement en passant son dictionnaire `userInfo` à la méthode de classe `isEngagementPushPayload:` de l’agent.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-158">You can determine whether a notification comes from Engagement or not by passing its `userInfo` dictionary to the Agent `isEngagementPushPayload:` class method.</span></span>

<span data-ttu-id="f7f3b-159">Assurez-vous que le délégué de l’objet `UNUserNotificationCenter` est paramétré en fonction de votre délégué, grâce à la méthode `application:willFinishLaunchingWithOptions:` ou `application:didFinishLaunchingWithOptions:` de votre délégué d’application.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-159">Make sure that the `UNUserNotificationCenter` object's delegate is set to your delegate within either the `application:willFinishLaunchingWithOptions:` or the `application:didFinishLaunchingWithOptions:` method of your application delegate.</span></span>
<span data-ttu-id="f7f3b-160">Par exemple, si vous avez implémenté la méthode 1 ci-dessus :</span><span class="sxs-lookup"><span data-stu-id="f7f3b-160">For instance, if you implemented the above proposal 1:</span></span>

      - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
        // Any other code

        [UNUserNotificationCenter currentNotificationCenter].delegate = self;
        return YES;
      }

## <a name="how-to-customize-campaigns"></a><span data-ttu-id="f7f3b-161">Personnalisation des campagnes marketing</span><span class="sxs-lookup"><span data-stu-id="f7f3b-161">How to customize campaigns</span></span>
### <a name="notifications"></a><span data-ttu-id="f7f3b-162">Notifications</span><span class="sxs-lookup"><span data-stu-id="f7f3b-162">Notifications</span></span>
<span data-ttu-id="f7f3b-163">Il existe deux types de notifications : les notifications système et les notifications dans l'application.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-163">There are two types of notifications: system and in-app notifications.</span></span>

<span data-ttu-id="f7f3b-164">Les notifications système sont gérées par iOS et ne peuvent pas être personnalisées.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-164">System notifications are handled by iOS, and cannot be customized.</span></span>

<span data-ttu-id="f7f3b-165">Les notifications dans l'application sont constituées d'une vue qui est ajoutée dynamiquement à la fenêtre de l'application actuelle.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-165">In-app notifications are made of a view that is dynamically added to the current application window.</span></span> <span data-ttu-id="f7f3b-166">Il s'agit d'une superposition de notification.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-166">This is called a notification overlay.</span></span> <span data-ttu-id="f7f3b-167">Les superpositions de notification sont idéales pour une intégration rapide car vous n'avez pas à modifier les vues dans votre application.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-167">Notification overlays are great for a fast integration because they does not require you to modify any view in your application.</span></span>

#### <a name="layout"></a><span data-ttu-id="f7f3b-168">Disposition</span><span class="sxs-lookup"><span data-stu-id="f7f3b-168">Layout</span></span>
<span data-ttu-id="f7f3b-169">Pour modifier l'apparence de vos notifications dans l'application, il vous suffit de modifier le fichier `AENotificationView.xib` pour l'adapter à vos besoins, en veillant à conserver les valeurs des balises et les types de sous-vues existantes.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-169">To modify the look of your in-app notifications, you can simply modify the file `AENotificationView.xib` to your needs, as long as you keep the tag values and types of the existing subviews.</span></span>

<span data-ttu-id="f7f3b-170">Par défaut, les notifications dans l'application se trouvent en bas de l'écran.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-170">By default, in-app notifications are presented at the bottom of the screen.</span></span> <span data-ttu-id="f7f3b-171">Si vous préférez les afficher en haut de l'écran, modifiez le `AENotificationView.xib` fourni et modifiez la propriété `AutoSizing` de la vue principale afin qu'elle puisse être conservée en haut de sa superview.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-171">If you prefer to display them at the top of screen, edit the provided `AENotificationView.xib` and change the `AutoSizing` property of the main view so it can be kept at the top of its superview.</span></span>

#### <a name="categories"></a><span data-ttu-id="f7f3b-172">Catégories</span><span class="sxs-lookup"><span data-stu-id="f7f3b-172">Categories</span></span>
<span data-ttu-id="f7f3b-173">Lorsque vous modifiez la disposition fournie, vous modifiez l'apparence de toutes vos notifications.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-173">When you modify the provided layout, you modify the look of all your notifications.</span></span> <span data-ttu-id="f7f3b-174">Les catégories permettent de définir diverses recherches ciblées (et éventuellement des comportements) pour les notifications.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-174">Categories allow you to define various targeted looks (possibly behaviors) for notifications.</span></span> <span data-ttu-id="f7f3b-175">Une catégorie peut être spécifiée lorsque vous créez une campagne Reach.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-175">A category can be specified when you create a Reach campaign.</span></span> <span data-ttu-id="f7f3b-176">N'oubliez pas que les catégories vous permettent également de personnaliser les annonces et les sondages, décrits plus avant dans ce document.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-176">Keep in mind that categories also let you customize announcements and polls, that is described later in this document.</span></span>

<span data-ttu-id="f7f3b-177">Pour inscrire un gestionnaire de catégorie pour vos notifications, vous devez ajouter un appel lorsque le module Reach est initialisé.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-177">To register a category handler for your notifications, you need to add a call once the reach module is initialized.</span></span>

    AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
    [reach registerNotifier:myNotifier forCategory:@"my_category"];
    ...

<span data-ttu-id="f7f3b-178">`myNotifier` doit être une instance d'un objet qui est conforme au protocole `AENotifier`.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-178">`myNotifier` must be an instance of an object that conforms to the protocol `AENotifier`.</span></span>

<span data-ttu-id="f7f3b-179">Vous pouvez implémenter les méthodes de protocole vous-même ou choisir d'implémenter à nouveau la classe `AEDefaultNotifier` existante qui effectue déjà l'essentiel du travail.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-179">You can implement the protocol methods by yourself or you can choose to reimplement the existing class `AEDefaultNotifier` which already performs most of the work.</span></span>

<span data-ttu-id="f7f3b-180">Par exemple, si vous souhaitez redéfinir la vue de notification pour une catégorie spécifique, vous pouvez suivre cet exemple :</span><span class="sxs-lookup"><span data-stu-id="f7f3b-180">For example, if you want to redefine the notification view for a specific category, you can follow this example:</span></span>

    #import "AEDefaultNotifier.h"
    #import "AENotificationView.h"
    @interface MyNotifier : AEDefaultNotifier
    @end

    @implementation MyNotifier

    -(NSString*)nibNameForCategory:(NSString*)category
    {
      return "MyNotificationView";
    }

    @end

<span data-ttu-id="f7f3b-181">Cet exemple simple de catégorie part du principe que vous possédez un fichier nommé `MyNotificationView.xib` dans votre offre groupée d'applications principale.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-181">This simple example of category assume that you have a file named `MyNotificationView.xib` in your main application bundle.</span></span> <span data-ttu-id="f7f3b-182">Si la méthode n'est pas en mesure de trouver un `.xib`correspondant, la notification ne s'affichera pas et Engagement générera un message dans la console.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-182">If the method is not able to find a corresponding `.xib`, the notification will not be displayed and Engagement will output a message in the console.</span></span>

<span data-ttu-id="f7f3b-183">Le fichier nib fourni doit respecter les règles suivantes :</span><span class="sxs-lookup"><span data-stu-id="f7f3b-183">The provided nib file should respect the following rules:</span></span>

* <span data-ttu-id="f7f3b-184">Il doit contenir une seule vue.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-184">It should only contain one view.</span></span>
* <span data-ttu-id="f7f3b-185">Les sous-vues doivent être du même type que celles qui se trouvent dans le fichier nib fourni nommé `AENotificationView.xib`</span><span class="sxs-lookup"><span data-stu-id="f7f3b-185">Subviews should be of the same types as the ones inside the provided nib file named `AENotificationView.xib`</span></span>
* <span data-ttu-id="f7f3b-186">Les sous-vues doivent comporter les mêmes balises que celles qui se trouvent dans le fichier nib nommé `AENotificationView.xib`</span><span class="sxs-lookup"><span data-stu-id="f7f3b-186">Subviews should have the same tags as the ones inside the provided nib file named `AENotificationView.xib`</span></span>

> [!TIP]
> <span data-ttu-id="f7f3b-187">Copiez simplement le fichier nib fourni, nommé `AENotificationView.xib`, puis commencez à travailler.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-187">Just copy the provided nib file, named `AENotificationView.xib`, and start working from there.</span></span> <span data-ttu-id="f7f3b-188">Attention, la vue à l'intérieur de ce fichier nib est associée à la classe `AENotificationView`.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-188">But be careful, the view inside this nib file is associated to the class `AENotificationView`.</span></span> <span data-ttu-id="f7f3b-189">Cette classe a redéfini la méthode `layoutSubViews` pour déplacer et redimensionner ses sous-vues en fonction du contexte.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-189">This class redefined the method `layoutSubViews` to move and resize its subviews according to context.</span></span> <span data-ttu-id="f7f3b-190">Vous avez peut-être besoin de la remplacer par une `UIView` ou votre classe de vue personnalisée.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-190">You may want to replace it with an `UIView` or you custom view class.</span></span>
>
>

<span data-ttu-id="f7f3b-191">Si vous avez besoin de personnaliser davantage vos notifications (si vous souhaitez par exemple charger votre vue directement à partir du code), il est recommandé d'examiner le code source et la documentation de classe fournis de `Protocol ReferencesDefaultNotifier` et `AENotifier`.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-191">If you need deeper customization of your notifications(if you want for instance to load your view directly from the code), it is recommended to take a look at the provided source code and class documentation of `Protocol ReferencesDefaultNotifier` and `AENotifier`.</span></span>

<span data-ttu-id="f7f3b-192">Notez que vous pouvez utiliser le même notificateur pour plusieurs catégories.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-192">Note that you can use the same notifier for multiple categories.</span></span>

<span data-ttu-id="f7f3b-193">Vous pouvez également redéfinir le notificateur par défaut comme suit :</span><span class="sxs-lookup"><span data-stu-id="f7f3b-193">You can also redefined the default notifier like this:</span></span>

    AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
    [reach registerNotifier:myNotifier forCategory:kAEReachDefaultCategory];

##### <a name="notification-handling"></a><span data-ttu-id="f7f3b-194">Gestion des notifications</span><span class="sxs-lookup"><span data-stu-id="f7f3b-194">Notification handling</span></span>
<span data-ttu-id="f7f3b-195">Lorsque vous utilisez la catégorie par défaut, certaines méthodes de cycle de vie sont appelées sur l'objet `AEReachContent` pour communiquer les statistiques et mettre à jour l'état de la campagne :</span><span class="sxs-lookup"><span data-stu-id="f7f3b-195">When using the default category, some life cycle methods are called on the `AEReachContent` object to report statistics and update the campaign state:</span></span>

* <span data-ttu-id="f7f3b-196">Lorsque la notification est affichée dans l'application, la méthode `displayNotification` (qui fournit des statistiques) est appelée par `AEReachModule` si `handleNotification:` renvoie `YES`.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-196">When the notification is displayed in application, the `displayNotification` method is called (which reports statistics) by `AEReachModule` if `handleNotification:` returns `YES`.</span></span>
* <span data-ttu-id="f7f3b-197">Si la notification est ignorée, la méthode `exitNotification` est appelée, les statistiques sont signalées et les campagnes suivantes peuvent alors être traitées.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-197">If the notification is dismissed, the `exitNotification` method is called, statistic is reported and next campaigns can now be processed.</span></span>
* <span data-ttu-id="f7f3b-198">En cas de clic sur la notification, `actionNotification` est appelée, les statistiques sont signalées et l'action associée est effectuée.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-198">If the notification is clicked, `actionNotification` is called, statistic is reported and the associated action is performed.</span></span>

<span data-ttu-id="f7f3b-199">Si votre implémentation de `AENotifier` contourne le comportement par défaut, vous devez appeler ces méthodes de cycle de vie vous-même.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-199">If your implementation of `AENotifier` bypasses the default behavior, you have to call these life cycle methods by yourself.</span></span> <span data-ttu-id="f7f3b-200">Les exemples suivants illustrent certains cas dans lesquels le comportement par défaut est ignoré :</span><span class="sxs-lookup"><span data-stu-id="f7f3b-200">The following examples illustrate some cases where the default behavior is bypassed:</span></span>

* <span data-ttu-id="f7f3b-201">Vous n'étendez pas `AEDefaultNotifier`, par exemple, vous avez implémenté la gestion des catégories à partir de zéro.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-201">You don't extend `AEDefaultNotifier`, e.g. you implemented category handling from scratch.</span></span>
* <span data-ttu-id="f7f3b-202">Vous avez substitué `prepareNotificationView:forContent:`, veillez à mapper au moins `onNotificationActioned` ou `onNotificationExited` sur l'un des contrôles de votre interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-202">You overrode `prepareNotificationView:forContent:`, be sure to map at least `onNotificationActioned` or `onNotificationExited` to one of your U.I controls.</span></span>

> [!WARNING]
> <span data-ttu-id="f7f3b-203">Si `handleNotification:` lève une exception, le contenu est supprimé et `drop` est appelé. Cela est signalé dans les statistiques et les campagnes suivantes peuvent maintenant être traitées.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-203">If `handleNotification:` throws an exception, the content is deleted and `drop` is called, this is reported in statistics and next campaigns can now be processed.</span></span>
>
>

#### <a name="include-notification-as-part-of-an-existing-view"></a><span data-ttu-id="f7f3b-204">Incluez des notifications dans le cadre d'une vue existante</span><span class="sxs-lookup"><span data-stu-id="f7f3b-204">Include notification as part of an existing view</span></span>
<span data-ttu-id="f7f3b-205">Les superpositions sont idéales pour une intégration rapide mais peuvent parfois ne pas être pratiques ou avoir des effets secondaires indésirables.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-205">Overlays are great for a fast integration but can be sometimes not convenient, or can have unwanted side effects.</span></span>

<span data-ttu-id="f7f3b-206">Si vous n'êtes pas satisfait du système de superposition de certains de vos affichages, vous pouvez le personnaliser pour ces affichages.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-206">If you're not satisfied with the overlay system in some of your views, you can customize it for these views.</span></span>

<span data-ttu-id="f7f3b-207">Vous pouvez décider d'inclure notre disposition de notifications dans vos affichages existants.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-207">You can decide to include our notification layout in your existing views.</span></span> <span data-ttu-id="f7f3b-208">Pour ce faire, il existe deux styles de mise en œuvre :</span><span class="sxs-lookup"><span data-stu-id="f7f3b-208">To do so, there is two implementation styles:</span></span>

1. <span data-ttu-id="f7f3b-209">Ajouter l'affichage de notification à l'aide d'Interface Builder</span><span class="sxs-lookup"><span data-stu-id="f7f3b-209">Add the notification view using interface builder</span></span>

   * <span data-ttu-id="f7f3b-210">Ouvrez *Interface Builder*</span><span class="sxs-lookup"><span data-stu-id="f7f3b-210">Open *Interface Builder*</span></span>
   * <span data-ttu-id="f7f3b-211">Placez un `UIView` 320 x 60 (ou 768 x 60 si vous êtes sur iPad) à l'endroit où vous souhaitez voir apparaître la notification</span><span class="sxs-lookup"><span data-stu-id="f7f3b-211">Place a 320x60 (or 768x60 if you are on iPad) `UIView` where you want the notification to appear</span></span>
   * <span data-ttu-id="f7f3b-212">Définissez la valeur de balise pour cette vue sur : **36822491**</span><span class="sxs-lookup"><span data-stu-id="f7f3b-212">Set the Tag value for this view to : **36822491**</span></span>
2. <span data-ttu-id="f7f3b-213">Ajoutez par programme l'affichage de notification.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-213">Add the notification view programmatically.</span></span> <span data-ttu-id="f7f3b-214">Ajoutez simplement le code suivant lors de l'initialisation de votre affichage :</span><span class="sxs-lookup"><span data-stu-id="f7f3b-214">Just add the following code when your view has been initialized:</span></span>

       UIView* notificationView = [[UIView alloc] initWithFrame:CGRectMake(0, 0, 320, 60)]; //Replace x and y coordinate values to your needs.
       notificationView.tag = NOTIFICATION_AREA_VIEW_TAG;
       [self.view addSubview:notificationView];

<span data-ttu-id="f7f3b-215">La macro `NOTIFICATION_AREA_VIEW_TAG` se trouve dans `AEDefaultNotifier.h`.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-215">`NOTIFICATION_AREA_VIEW_TAG` macro can be found in `AEDefaultNotifier.h`.</span></span>

> [!NOTE]
> <span data-ttu-id="f7f3b-216">Le notificateur par défaut détecte automatiquement que la disposition de notification est incluse dans cet affichage et nr lui ajoute pas de superposition.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-216">The default notifier automatically detects that the notification layout is included in this view and will not add an overlay for it.</span></span>
>
>

### <a name="announcements-and-polls"></a><span data-ttu-id="f7f3b-217">Annonces et sondages</span><span class="sxs-lookup"><span data-stu-id="f7f3b-217">Announcements and polls</span></span>
#### <a name="layouts"></a><span data-ttu-id="f7f3b-218">Mises en forme</span><span class="sxs-lookup"><span data-stu-id="f7f3b-218">Layouts</span></span>
<span data-ttu-id="f7f3b-219">Vous pouvez modifier les fichiers `AEDefaultAnnouncementView.xib` et `AEDefaultPollView.xib` tant que vous conservez les valeurs des balises et les types de sous-vues existantes.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-219">You can modify the files `AEDefaultAnnouncementView.xib` and `AEDefaultPollView.xib` as long as you keep the tag values and types of the existing subviews.</span></span>

#### <a name="categories"></a><span data-ttu-id="f7f3b-220">Catégories</span><span class="sxs-lookup"><span data-stu-id="f7f3b-220">Categories</span></span>
##### <a name="alternate-layouts"></a><span data-ttu-id="f7f3b-221">Autres dispositions</span><span class="sxs-lookup"><span data-stu-id="f7f3b-221">Alternate layouts</span></span>
<span data-ttu-id="f7f3b-222">Telles que les notifications, catégorie de la campagne peut être utilisée pour que les autres dispositions pour vos annonces et les sondages.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-222">Like notifications, the campaign's category can be used to have alternate layouts for your announcements and polls.</span></span>

<span data-ttu-id="f7f3b-223">Pour créer une catégorie d'annonce, vous devez étendre **AEAnnouncementViewController** et l'enregistrer lorsque le module Reach a été initialisé :</span><span class="sxs-lookup"><span data-stu-id="f7f3b-223">To create a category for an announcement, you must extend **AEAnnouncementViewController** and register it once the reach module has been initialized:</span></span>

    AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
    [reach registerAnnouncementController:[MyCustomAnnouncementViewController class] forCategory:@"my_category"];

> [!NOTE]
> <span data-ttu-id="f7f3b-224">Chaque fois qu’un utilisateur clique sur une notification pour une annonce avec la catégorie « my\_category », votre contrôleur d’affichage inscrit (dans ce cas, `MyCustomAnnouncementViewController`) est initialisé en appelant la méthode `initWithAnnouncement:` et l’affichage est ajouté à la fenêtre de l’application actuelle.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-224">Each time a user will click on a notification for an announcement with the category "my\_category", your registered view controller (in that case `MyCustomAnnouncementViewController`) will be initialized by calling the method `initWithAnnouncement:` and the view will be added to the current application window.</span></span>
>
>

<span data-ttu-id="f7f3b-225">Dans votre implémentation de la classe `AEAnnouncementViewController`, vous devez lire la propriété `announcement` pour initialiser vos sous-vues.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-225">In your implementation of the `AEAnnouncementViewController` class you will have to read the property `announcement` to initialize your subviews.</span></span> <span data-ttu-id="f7f3b-226">Prenons l'exemple ci-dessous, dans lequel deux étiquettes sont initialisées à l'aide des propriétés `title` et `body` de la classe `AEReachAnnouncement` :</span><span class="sxs-lookup"><span data-stu-id="f7f3b-226">Consider the example below, where two labels are initialized using `title` and `body` properties of the `AEReachAnnouncement` class:</span></span>

    -(void)loadView
    {
        [super loadView];

        UILabel* titleLabel = [[UILabel alloc] initWithFrame:CGRectMake(10, 20, 300, 60)];
        titleLabel.font = [UIFont systemFontOfSize:32.0];
        titleLabel.text = self.announcement.title;

        UILabel* bodyLabel = [[UILabel alloc] initWithFrame:CGRectMake(10, 20, 300, 60)];
        bodyLabel.font = [UIFont systemFontOfSize:24.0];
        bodyLabel.text = self.announcement.body;

        [self.view addSubview:titleLabel];
        [self.view addSubview:bodyLabel];
    }

<span data-ttu-id="f7f3b-227">Si vous ne souhaitez pas charger vos affichages vous-même, mais que vous souhaitez simplement réutiliser la disposition de l'affichage des annonces par défaut, il vous suffit de faire en sorte que votre contrôleur d'affichage personnalisé étende la classe fournie `AEDefaultAnnouncementViewController`.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-227">If you don't want to load your views by yourself but you just want to reuse the default announcement view layout, you can simply make your custom view controller extends the provided class `AEDefaultAnnouncementViewController`.</span></span> <span data-ttu-id="f7f3b-228">Dans ce cas, dupliquez le fichier nib `AEDefaultAnnouncementView.xib` et renommez-le afin qu'il puisse être chargé par votre contrôleur d'affichage personnalisé (pour un contrôleur nommé `CustomAnnouncementViewController`, vous devez appeler votre fichier nib `CustomAnnouncementView.xib`).</span><span class="sxs-lookup"><span data-stu-id="f7f3b-228">In that case, duplicate the nib file `AEDefaultAnnouncementView.xib` and rename it so it can be loaded by your custom view controller (for a controller named `CustomAnnouncementViewController`, you should call your nib file `CustomAnnouncementView.xib`).</span></span>

<span data-ttu-id="f7f3b-229">Pour remplacer la catégorie par défaut des annonces, il vous suffit d'enregistrer votre contrôleur d'affichage personnalisé pour la catégorie définie dans `kAEReachDefaultCategory`:</span><span class="sxs-lookup"><span data-stu-id="f7f3b-229">To replace the default category of announcements, simply register your custom view controller for the category defined in `kAEReachDefaultCategory`:</span></span>

    [reach registerAnnouncementController:[MyCustomAnnouncementViewController class] forCategory:kAEReachDefaultCategory];

<span data-ttu-id="f7f3b-230">Les sondages peuvent être personnalisés de la même manière :</span><span class="sxs-lookup"><span data-stu-id="f7f3b-230">Polls can be customized the same way :</span></span>

    AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
    [reach registerPollController:[MyCustomPollViewController class] forCategory:@"my_category"];

<span data-ttu-id="f7f3b-231">Cette fois, les `MyCustomPollViewController` fournis doivent étendre `AEPollViewController`.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-231">This time, the provided `MyCustomPollViewController` must extend `AEPollViewController`.</span></span> <span data-ttu-id="f7f3b-232">Vous pouvez également choisir d'étendre à partir du contrôleur par défaut : `AEDefaultPollViewController`.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-232">Or you can choose to extend from the default controller: `AEDefaultPollViewController`.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f7f3b-233">N'oubliez pas d'appeler `action` (`submitAnswers:` pour les contrôleurs d'affichage personnalisé de sondage) ou la méthode `exit` avant que le contrôleur d'affichage ne soit ignoré.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-233">Don't forget to call either `action` (`submitAnswers:` for custom poll view controllers) or `exit` method before the view controller is dismissed.</span></span> <span data-ttu-id="f7f3b-234">Dans le cas contraire, les statistiques ne seront pas envoyées (c'est-à-dire aucune analyse de la campagne) et surtout, les campagnes suivantes ne recevront pas de notification avant que le processus de l'application soit redémarré.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-234">Otherwise, statistics won't be sent (i.e. no analytics on the campaign) and more importantly next campaigns will not be notified until the application process is restarted.</span></span>
>
>

##### <a name="implementation-example"></a><span data-ttu-id="f7f3b-235">Exemple d'implémentation</span><span class="sxs-lookup"><span data-stu-id="f7f3b-235">Implementation example</span></span>
<span data-ttu-id="f7f3b-236">Dans cette implémentation, l'affichage d'annonces personnalisé est chargé à partir d'un fichier xib externe.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-236">In this implementation the custom announcement view is loaded from an external xib file.</span></span>

<span data-ttu-id="f7f3b-237">Comme pour la personnalisation de notification avancée, il est recommandé d'examiner le code source de l'implémentation standard.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-237">Like for advanced notification customization, it is recommended to look at the source code of the standard implementation.</span></span>

`CustomAnnouncementViewController.h`

    //Interface
    @interface CustomAnnouncementViewController : AEAnnouncementViewController {
      UILabel* titleLabel;
      UITextView* descTextView;
      UIWebView* htmlWebView;
      UIButton* okButton;
      UIButton* cancelButton;
    }

    @property (nonatomic, retain) IBOutlet UILabel* titleLabel;
    @property (nonatomic, retain) IBOutlet UITextView* descTextView;
    @property (nonatomic, retain) IBOutlet UIWebView* htmlWebView;
    @property (nonatomic, retain) IBOutlet UIButton* okButton;
    @property (nonatomic, retain) IBOutlet UIButton* cancelButton;

    -(IBAction)okButtonClicked:(id)sender;
    -(IBAction)cancelButtonClicked:(id)sender;

`CustomAnnouncementViewController.m`

    //Implementation
    @implementation CustomAnnouncementViewController
    @synthesize titleLabel;
    @synthesize descTextView;
    @synthesize htmlWebView;
    @synthesize okButton;
    @synthesize cancelButton;

    -(id)initWithAnnouncement:(AEReachAnnouncement*)anAnnouncement
    {
      self = [super initWithNibName:@"CustomAnnouncementViewController" bundle:nil];
      if (self != nil) {
        self.announcement = anAnnouncement;
      }
      return self;
    }

    - (void) dealloc
    {
      [titleLabel release];
      [descTextView release];
      [htmlWebView release];
      [okButton release];
      [cancelButton release];
      [super dealloc];
    }

    - (void)viewDidLoad {
      [super viewDidLoad];

      /* Init announcement title */
      titleLabel.text = self.announcement.title;

      /* Init announcement body */
      if(self.announcement.type == AEAnnouncementTypeHtml)
      {
        titleLabel.hidden = YES;
        htmlWebView.hidden = NO;
        [htmlWebView loadHTMLString:self.announcement.body baseURL:[NSURL URLWithString:@"http://localhost/"]];
      }
      else
      {
        titleLabel.hidden = NO;
        htmlWebView.hidden = YES;
        descTextView.text = self.announcement.body;
      }

      /* Set action button label */
      if([self.announcement.actionLabel length] > 0)
        [okButton setTitle:self.announcement.actionLabel forState:UIControlStateNormal];

      /* Set exit button label */
      if([self.announcement.exitLabel length] > 0)
        [cancelButton setTitle:self.announcement.exitLabel forState:UIControlStateNormal];
    }

    #pragma mark Actions

    -(IBAction)okButtonClicked:(id)sender
    {
        [self action];
    }

    -(IBAction)cancelButtonClicked:(id)sender
    {
        [self exit];
    }

    @end
