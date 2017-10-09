---
title: "aaaAzure Mobile Engagement iOS intégration d’atteindre SDK | Documents Microsoft"
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
ms.openlocfilehash: 40c9bfbdb475ab0b97bdbc9cea798a59cb8a71ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toointegrate-engagement-reach-on-ios"></a><span data-ttu-id="4c006-103">Comment les tooIntegrate Engagement sur iOS</span><span class="sxs-lookup"><span data-stu-id="4c006-103">How tooIntegrate Engagement Reach on iOS</span></span>
<span data-ttu-id="4c006-104">Vous devez suivre la procédure d’intégration hello décrite dans hello [comment tooIntegrate Engagement sur iOS document](mobile-engagement-ios-integrate-engagement.md) avant de suivre ce guide.</span><span class="sxs-lookup"><span data-stu-id="4c006-104">You must follow hello integration procedure described in hello [How tooIntegrate Engagement on iOS document](mobile-engagement-ios-integrate-engagement.md) before following this guide.</span></span>

<span data-ttu-id="4c006-105">Cette documentation nécessite XCode 8.</span><span class="sxs-lookup"><span data-stu-id="4c006-105">This documentation requires XCode 8.</span></span> <span data-ttu-id="4c006-106">Si vous dépendez vraiment de XCode 7, vous pouvez utiliser hello [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh).</span><span class="sxs-lookup"><span data-stu-id="4c006-106">If you really depend on XCode 7 then you may use hello [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh).</span></span> <span data-ttu-id="4c006-107">Il existe un bogue connu concernant cette version précédente quand elle est exécutée sur des appareils iOS 10 : les notifications système ne sont pas activées.</span><span class="sxs-lookup"><span data-stu-id="4c006-107">There is a known bug on this previous version while running on iOS 10 devices:  system notifications are not actioned.</span></span> <span data-ttu-id="4c006-108">toofix avoir tooimplement hello déconseillé API `application:didReceiveRemoteNotification:` dans votre application déléguer comme suit :</span><span class="sxs-lookup"><span data-stu-id="4c006-108">toofix this you will have tooimplement hello deprecated API `application:didReceiveRemoteNotification:` in your app delegate as follows:</span></span>

    - (void)application:(UIApplication*)application
    didReceiveRemoteNotification:(NSDictionary*)userInfo
    {
        [[EngagementAgent shared] applicationDidReceiveRemoteNotification:userInfo fetchCompletionHandler:nil];
    }

> [!IMPORTANT]
> <span data-ttu-id="4c006-109">**Nous ne recommandons pas cette solution de contournement** : ce comportement peut changer dans une prochaine mise à niveau (même mineure) de la version iOS car cette API iOS est déconseillée.</span><span class="sxs-lookup"><span data-stu-id="4c006-109">**We do not recommend this workaround** as this behavior can change in any upcoming (even minor) iOS version upgrade because this iOS API is deprecated.</span></span> <span data-ttu-id="4c006-110">Vous devez basculer tooXCode 8 dès que possible.</span><span class="sxs-lookup"><span data-stu-id="4c006-110">You should switch tooXCode 8 as soon as possible.</span></span>
>
>

### <a name="enable-your-app-tooreceive-silent-push-notifications"></a><span data-ttu-id="4c006-111">Activer votre tooreceive d’application en mode silencieux des Notifications Push</span><span class="sxs-lookup"><span data-stu-id="4c006-111">Enable your app tooreceive Silent Push Notifications</span></span>
[!INCLUDE [mobile-engagement-ios-silent-push](../../includes/mobile-engagement-ios-silent-push.md)]

## <a name="integration-steps"></a><span data-ttu-id="4c006-112">Étapes d'intégration</span><span class="sxs-lookup"><span data-stu-id="4c006-112">Integration steps</span></span>
### <a name="embed-hello-engagement-reach-sdk-into-your-ios-project"></a><span data-ttu-id="4c006-113">Incorporer hello SDK Reach d’Engagement dans votre projet iOS</span><span class="sxs-lookup"><span data-stu-id="4c006-113">Embed hello Engagement Reach SDK into your iOS project</span></span>
* <span data-ttu-id="4c006-114">Ajouter le sdk de portée de hello dans votre projet Xcode.</span><span class="sxs-lookup"><span data-stu-id="4c006-114">Add hello Reach sdk in your Xcode project.</span></span> <span data-ttu-id="4c006-115">Dans Xcode, accédez trop**projet \> ajouter tooproject** et choisissez hello `EngagementReach` dossier.</span><span class="sxs-lookup"><span data-stu-id="4c006-115">In Xcode, go too**Project \> Add tooproject** and choose hello `EngagementReach` folder.</span></span>

### <a name="modify-your-application-delegate"></a><span data-ttu-id="4c006-116">Modifier votre délégué d'Application</span><span class="sxs-lookup"><span data-stu-id="4c006-116">Modify your Application Delegate</span></span>
* <span data-ttu-id="4c006-117">En hello en haut de votre fichier d’implémentation, importez le module d’Engagement atteindre hello :</span><span class="sxs-lookup"><span data-stu-id="4c006-117">At hello top of your implementation file, import hello Engagement Reach module:</span></span>

      [...]
      #import "AEReachModule.h"
* <span data-ttu-id="4c006-118">Dans la méthode `applicationDidFinishLaunching:` ou `application:didFinishLaunchingWithOptions:`, créez un module de portée et passer en ligne de l’initialisation Engagement tooyour existante :</span><span class="sxs-lookup"><span data-stu-id="4c006-118">Inside method `applicationDidFinishLaunching:` or `application:didFinishLaunchingWithOptions:`, create a reach module and pass it tooyour existing Engagement initialization line:</span></span>

      - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
        AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
        [EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}" modules:reach, nil];
        [...]

        return YES;
      }
* <span data-ttu-id="4c006-119">Modifier **'icon.png'** chaîne dont vous souhaitez définir comme l’icône de votre nom de l’image hello.</span><span class="sxs-lookup"><span data-stu-id="4c006-119">Modify **'icon.png'** string with hello image name you want as your notification icon.</span></span>
* <span data-ttu-id="4c006-120">Si vous souhaitez toouse hello option *valeur de badge mise à jour* dans les campagnes Reach ou si vous souhaitez que le push natif toouse \<format/Native de SaaS/portée API/campagne Push\> campagnes, vous devez laisser hello portée module gérer Hello badge icône lui-même (elle supprime automatiquement le badge d’application hello et également réinitialiser la valeur hello stockée par Engagement chaque fois qu’application hello est démarré ou foregrounded).</span><span class="sxs-lookup"><span data-stu-id="4c006-120">If you want toouse hello option *Update badge value* in Reach campaigns or if you want toouse native push \</SaaS/Reach API/Campaign format/Native Push\> campaigns, you must let hello Reach module manage hello badge icon itself (it will automatically clear hello application badge and also reset hello value stored by Engagement every time hello application is started or foregrounded).</span></span> <span data-ttu-id="4c006-121">Cela est fait en ajoutant hello ligne suivante après l’initialisation du module portée :</span><span class="sxs-lookup"><span data-stu-id="4c006-121">This is done by adding hello following line after Reach module initialization:</span></span>

      [reach setAutoBadgeEnabled:YES];
* <span data-ttu-id="4c006-122">Si vous souhaitez push de données de couverture toohandle, vous devez laisser votre délégué de l’Application est conforme toohello `AEReachDataPushDelegate` protocole.</span><span class="sxs-lookup"><span data-stu-id="4c006-122">If you want toohandle Reach data push, you must let your Application delegate conform toohello `AEReachDataPushDelegate` protocol.</span></span> <span data-ttu-id="4c006-123">Ajoutez hello ligne suivante après l’initialisation du module portée :</span><span class="sxs-lookup"><span data-stu-id="4c006-123">Add hello following line after Reach module initialization:</span></span>

      [reach setDataPushDelegate:self];
* <span data-ttu-id="4c006-124">Ensuite, vous pouvez implémenter les méthodes hello `onDataPushStringReceived:` et `onDataPushBase64ReceivedWithDecodedBody:andEncodedBody:` dans votre délégué d’application :</span><span class="sxs-lookup"><span data-stu-id="4c006-124">Then you can implement hello methods `onDataPushStringReceived:` and `onDataPushBase64ReceivedWithDecodedBody:andEncodedBody:` in your application delegate:</span></span>

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

### <a name="category"></a><span data-ttu-id="4c006-125">Catégorie</span><span class="sxs-lookup"><span data-stu-id="4c006-125">Category</span></span>
<span data-ttu-id="4c006-126">paramètre de catégorie Hello est facultatif lorsque vous créez une campagne de Push de données et permet de que vous toofilter données exécute un push.</span><span class="sxs-lookup"><span data-stu-id="4c006-126">hello category parameter is optional when you create a Data Push campaign and allows you toofilter data pushes.</span></span> <span data-ttu-id="4c006-127">Cela est utile si vous souhaitez que les différents types de toopush de `Base64` tooidentify de données et que vous souhaitez leur type avant de les analyser.</span><span class="sxs-lookup"><span data-stu-id="4c006-127">This is useful if you want toopush different kinds of `Base64` data and want tooidentify their type before parsing them.</span></span>

<span data-ttu-id="4c006-128">**Votre application est maintenant prêt tooreceive et affichage de contenu atteint !**</span><span class="sxs-lookup"><span data-stu-id="4c006-128">**Your application is now ready tooreceive and display reach contents!**</span></span>

## <a name="how-tooreceive-announcements-and-polls-at-any-time"></a><span data-ttu-id="4c006-129">Comment tooreceive annonces et les sondages à tout moment</span><span class="sxs-lookup"><span data-stu-id="4c006-129">How tooreceive announcements and polls at any time</span></span>
<span data-ttu-id="4c006-130">Engagement peut envoyer des notifications de portée aux utilisateurs finaux de tooyour à tout moment à l’aide de hello Apple Push Notification Service.</span><span class="sxs-lookup"><span data-stu-id="4c006-130">Engagement can send Reach notifications tooyour end users at any time by using hello Apple Push Notification Service.</span></span>

<span data-ttu-id="4c006-131">tooenable cette fonctionnalité, vous avez tooprepare votre application pour les notifications de push d’Apple et modifier votre délégué de l’application.</span><span class="sxs-lookup"><span data-stu-id="4c006-131">tooenable this functionality, you'll have tooprepare your application for Apple push notifications and modify your application delegate.</span></span>

### <a name="prepare-your-application-for-apple-push-notifications"></a><span data-ttu-id="4c006-132">Préparer votre application pour les notifications Push Apple</span><span class="sxs-lookup"><span data-stu-id="4c006-132">Prepare your application for Apple push notifications</span></span>
<span data-ttu-id="4c006-133">Suivez le guide de hello : [comment tooPrepare votre Application pour les Notifications Push Apple](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html#//apple_ref/doc/uid/TP40012582-CH26-SW6)</span><span class="sxs-lookup"><span data-stu-id="4c006-133">Please follow hello guide : [How tooPrepare your Application for Apple Push Notifications](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html#//apple_ref/doc/uid/TP40012582-CH26-SW6)</span></span>

### <a name="add-hello-necessary-client-code"></a><span data-ttu-id="4c006-134">Ajoutez le code du client nécessaire hello</span><span class="sxs-lookup"><span data-stu-id="4c006-134">Add hello necessary client code</span></span>
<span data-ttu-id="4c006-135">*À ce stade votre application doit avoir un certificat Apple push inscrit dans le serveur frontal de hello Engagement.*</span><span class="sxs-lookup"><span data-stu-id="4c006-135">*At this point your application should have a registered Apple push certificate in hello Engagement frontend.*</span></span>

<span data-ttu-id="4c006-136">Si elle n’est pas déjà fait, vous devez tooregister des notifications push tooreceive de votre application.</span><span class="sxs-lookup"><span data-stu-id="4c006-136">If it's not done already, you need tooregister your application tooreceive push notifications.</span></span>

* <span data-ttu-id="4c006-137">Hello d’importation `User Notification` framework :</span><span class="sxs-lookup"><span data-stu-id="4c006-137">Import hello `User Notification` framework:</span></span>

        #import <UserNotifications/UserNotifications.h>
* <span data-ttu-id="4c006-138">Ajouter hello ligne suivante au démarrage de votre application (en général, dans `application:didFinishLaunchingWithOptions:`) :</span><span class="sxs-lookup"><span data-stu-id="4c006-138">Add hello following line when your application starts (typically in `application:didFinishLaunchingWithOptions:`):</span></span>

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

<span data-ttu-id="4c006-139">Ensuite, vous devez le jeton du périphérique tooprovide tooEngagement hello retourné par les serveurs d’Apple.</span><span class="sxs-lookup"><span data-stu-id="4c006-139">Then, You need tooprovide tooEngagement hello device token returned by Apple servers.</span></span> <span data-ttu-id="4c006-140">Cette opération est effectuée dans la méthode hello nommé `application:didRegisterForRemoteNotificationsWithDeviceToken:` dans votre délégué d’application :</span><span class="sxs-lookup"><span data-stu-id="4c006-140">This is done in hello method named `application:didRegisterForRemoteNotificationsWithDeviceToken:` in your application delegate:</span></span>

    - (void)application:(UIApplication*)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData*)deviceToken
    {
        [[EngagementAgent shared] registerDeviceToken:deviceToken];
    }

<span data-ttu-id="4c006-141">Enfin, vous avez tooinform hello Engagement SDK lorsque votre application reçoit une notification à distance.</span><span class="sxs-lookup"><span data-stu-id="4c006-141">Finally, you have tooinform hello Engagement SDK when your application receives a remote notification.</span></span> <span data-ttu-id="4c006-142">toodo qui, appelez hello méthode `applicationDidReceiveRemoteNotification:fetchCompletionHandler:` dans votre délégué d’application :</span><span class="sxs-lookup"><span data-stu-id="4c006-142">toodo that, call hello method `applicationDidReceiveRemoteNotification:fetchCompletionHandler:` in your application delegate:</span></span>

    - (void)application:(UIApplication*)application didReceiveRemoteNotification:(NSDictionary*)userInfo fetchCompletionHandler:(void (^)(UIBackgroundFetchResult result))handler
    {
        [[EngagementAgent shared] applicationDidReceiveRemoteNotification:userInfo fetchCompletionHandler:handler];
    }

> [!IMPORTANT]
> <span data-ttu-id="4c006-143">Par défaut, l’Engagement atteindre contrôle hello completionHandler.</span><span class="sxs-lookup"><span data-stu-id="4c006-143">By default, Engagement Reach controls hello completionHandler.</span></span> <span data-ttu-id="4c006-144">Si vous souhaitez toomanually répondre toohello `handler` dans votre code, vous pouvez passer nil pour hello `handler` bloquer l’achèvement de hello argument et le contrôle vous-même.</span><span class="sxs-lookup"><span data-stu-id="4c006-144">If you want toomanually respond toohello `handler` block in your code, you can pass nil for hello `handler` argument and control hello completion block yourself.</span></span> <span data-ttu-id="4c006-145">Consultez hello `UIBackgroundFetchResult` type pour obtenir la liste des valeurs possibles.</span><span class="sxs-lookup"><span data-stu-id="4c006-145">See hello `UIBackgroundFetchResult` type for a list of possible values.</span></span>
>
>

### <a name="full-example"></a><span data-ttu-id="4c006-146">Exemple complet</span><span class="sxs-lookup"><span data-stu-id="4c006-146">Full example</span></span>
<span data-ttu-id="4c006-147">Voici un exemple complet d'intégration :</span><span class="sxs-lookup"><span data-stu-id="4c006-147">Here is a full example of integration:</span></span>

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

### <a name="resolve-unusernotificationcenter-delegate-conflicts"></a><span data-ttu-id="4c006-148">Résoudre les conflits de délégué UNUserNotificationCenter</span><span class="sxs-lookup"><span data-stu-id="4c006-148">Resolve UNUserNotificationCenter delegate conflicts</span></span>

<span data-ttu-id="4c006-149">*Si, ni votre application ni l’une des bibliothèques tierces n’implémente un `UNUserNotificationCenterDelegate`, vous pouvez ignorer cette partie.*</span><span class="sxs-lookup"><span data-stu-id="4c006-149">*If neither your application or one of your third party libraries implements a `UNUserNotificationCenterDelegate` then you can skip this part.*</span></span>

<span data-ttu-id="4c006-150">A `UNUserNotificationCenter` délégué est utilisé par le cycle de vie hello SDK toomonitor hello de notifications d’Engagement sur les appareils qui exécutent sur iOS ou supérieure à 10.</span><span class="sxs-lookup"><span data-stu-id="4c006-150">A `UNUserNotificationCenter` delegate is used by hello SDK toomonitor hello life cycle of Engagement notifications on devices running on iOS 10 or greater.</span></span> <span data-ttu-id="4c006-151">Hello SDK possède sa propre implémentation de hello `UNUserNotificationCenterDelegate` de protocole, mais il peut y avoir qu’un seul `UNUserNotificationCenter` déléguer par application.</span><span class="sxs-lookup"><span data-stu-id="4c006-151">hello SDK has its own implementation of hello `UNUserNotificationCenterDelegate` protocol but there can be only one `UNUserNotificationCenter` delegate per application.</span></span> <span data-ttu-id="4c006-152">Tout autre délégué ajouté toohello `UNUserNotificationCenter` objet est en conflit avec hello Engagement une.</span><span class="sxs-lookup"><span data-stu-id="4c006-152">Any other delegate added toohello `UNUserNotificationCenter` object will conflict with hello Engagement one.</span></span> <span data-ttu-id="4c006-153">Si hello SDK détecte le délégué de votre ou de plusieurs autres tiers alors qu’il n’utilise pas sa propre implémentation toogive vous une chance tooresolve hello est en conflit.</span><span class="sxs-lookup"><span data-stu-id="4c006-153">If hello SDK detects your or any other third party's delegate then it will not use its own implementation toogive you a chance tooresolve hello conflicts.</span></span> <span data-ttu-id="4c006-154">Vous devez tooadd hello Engagement logique tooyour possèdent des conflits de hello tooresolve délégué dans l’ordre.</span><span class="sxs-lookup"><span data-stu-id="4c006-154">You will have tooadd hello Engagement logic tooyour own delegate in order tooresolve hello conflicts.</span></span>

<span data-ttu-id="4c006-155">Il existe deux façons tooachieve cela.</span><span class="sxs-lookup"><span data-stu-id="4c006-155">There are two ways tooachieve this.</span></span>

<span data-ttu-id="4c006-156">Proposition de 1, simplement en transfert votre délégué appelle toohello SDK :</span><span class="sxs-lookup"><span data-stu-id="4c006-156">Proposal 1, simply by forwarding your delegate calls toohello SDK:</span></span>

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

<span data-ttu-id="4c006-157">Ou 2, en héritant de hello `AEUserNotificationHandler` classe</span><span class="sxs-lookup"><span data-stu-id="4c006-157">Or proposal 2, by inheriting from hello `AEUserNotificationHandler` class</span></span>

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
> <span data-ttu-id="4c006-158">Vous pouvez déterminer si une notification d’Engagement ou non, en passant son `userInfo` dictionnaire toohello Agent `isEngagementPushPayload:` méthode de classe.</span><span class="sxs-lookup"><span data-stu-id="4c006-158">You can determine whether a notification comes from Engagement or not by passing its `userInfo` dictionary toohello Agent `isEngagementPushPayload:` class method.</span></span>

<span data-ttu-id="4c006-159">Vérifiez que hello `UNUserNotificationCenter` délégué de l’objet a la valeur délégué tooyour dans soit hello `application:willFinishLaunchingWithOptions:` ou hello `application:didFinishLaunchingWithOptions:` méthode du délégué de votre application.</span><span class="sxs-lookup"><span data-stu-id="4c006-159">Make sure that hello `UNUserNotificationCenter` object's delegate is set tooyour delegate within either hello `application:willFinishLaunchingWithOptions:` or hello `application:didFinishLaunchingWithOptions:` method of your application delegate.</span></span>
<span data-ttu-id="4c006-160">Par exemple, si vous avez implémenté hello ci-dessus proposition 1 :</span><span class="sxs-lookup"><span data-stu-id="4c006-160">For instance, if you implemented hello above proposal 1:</span></span>

      - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
        // Any other code

        [UNUserNotificationCenter currentNotificationCenter].delegate = self;
        return YES;
      }

## <a name="how-toocustomize-campaigns"></a><span data-ttu-id="4c006-161">Comment les campagnes toocustomize</span><span class="sxs-lookup"><span data-stu-id="4c006-161">How toocustomize campaigns</span></span>
### <a name="notifications"></a><span data-ttu-id="4c006-162">Notifications</span><span class="sxs-lookup"><span data-stu-id="4c006-162">Notifications</span></span>
<span data-ttu-id="4c006-163">Il existe deux types de notifications : les notifications système et les notifications dans l'application.</span><span class="sxs-lookup"><span data-stu-id="4c006-163">There are two types of notifications: system and in-app notifications.</span></span>

<span data-ttu-id="4c006-164">Les notifications système sont gérées par iOS et ne peuvent pas être personnalisées.</span><span class="sxs-lookup"><span data-stu-id="4c006-164">System notifications are handled by iOS, and cannot be customized.</span></span>

<span data-ttu-id="4c006-165">Les notifications dans l’application sont constituées d’une vue qui est ajoutée dynamiquement toohello fenêtre d’application actuelle.</span><span class="sxs-lookup"><span data-stu-id="4c006-165">In-app notifications are made of a view that is dynamically added toohello current application window.</span></span> <span data-ttu-id="4c006-166">Il s'agit d'une superposition de notification.</span><span class="sxs-lookup"><span data-stu-id="4c006-166">This is called a notification overlay.</span></span> <span data-ttu-id="4c006-167">Superpositions de notification sont parfaites pour une intégration rapide car ils ne nécessitent pas vous toomodify n’importe quelle vue dans votre application.</span><span class="sxs-lookup"><span data-stu-id="4c006-167">Notification overlays are great for a fast integration because they does not require you toomodify any view in your application.</span></span>

#### <a name="layout"></a><span data-ttu-id="4c006-168">Disposition</span><span class="sxs-lookup"><span data-stu-id="4c006-168">Layout</span></span>
<span data-ttu-id="4c006-169">apparence hello toomodify vos notifications dans l’application, il suffit de modifier le fichier de hello `AENotificationView.xib` tooyour a besoin, tant que vous conservez les valeurs de balise hello et les types de sous-vues existant de hello.</span><span class="sxs-lookup"><span data-stu-id="4c006-169">toomodify hello look of your in-app notifications, you can simply modify hello file `AENotificationView.xib` tooyour needs, as long as you keep hello tag values and types of hello existing subviews.</span></span>

<span data-ttu-id="4c006-170">Par défaut, les notifications dans l’application sont présentées sous l’écran hello hello.</span><span class="sxs-lookup"><span data-stu-id="4c006-170">By default, in-app notifications are presented at hello bottom of hello screen.</span></span> <span data-ttu-id="4c006-171">Si vous préférez toodisplay en haut de hello de l’écran, modifier hello fourni `AENotificationView.xib` et modifiez hello `AutoSizing` propriété de vue principale de hello donc peuvent rester en haut hello de son super-vue.</span><span class="sxs-lookup"><span data-stu-id="4c006-171">If you prefer toodisplay them at hello top of screen, edit hello provided `AENotificationView.xib` and change hello `AutoSizing` property of hello main view so it can be kept at hello top of its superview.</span></span>

#### <a name="categories"></a><span data-ttu-id="4c006-172">Catégories</span><span class="sxs-lookup"><span data-stu-id="4c006-172">Categories</span></span>
<span data-ttu-id="4c006-173">Lorsque vous modifiez hello fourni mise en page, vous modifiez apparence hello toutes vos notifications.</span><span class="sxs-lookup"><span data-stu-id="4c006-173">When you modify hello provided layout, you modify hello look of all your notifications.</span></span> <span data-ttu-id="4c006-174">Les catégories permettent toodefine que différents ciblés recherche (et éventuellement des comportements) pour les notifications.</span><span class="sxs-lookup"><span data-stu-id="4c006-174">Categories allow you toodefine various targeted looks (possibly behaviors) for notifications.</span></span> <span data-ttu-id="4c006-175">Une catégorie peut être spécifiée lorsque vous créez une campagne Reach.</span><span class="sxs-lookup"><span data-stu-id="4c006-175">A category can be specified when you create a Reach campaign.</span></span> <span data-ttu-id="4c006-176">N'oubliez pas que les catégories vous permettent également de personnaliser les annonces et les sondages, décrits plus avant dans ce document.</span><span class="sxs-lookup"><span data-stu-id="4c006-176">Keep in mind that categories also let you customize announcements and polls, that is described later in this document.</span></span>

<span data-ttu-id="4c006-177">tooregister un gestionnaire de catégorie pour les notifications, vous devez tooadd un appel une fois hello atteindre le module est initialisé.</span><span class="sxs-lookup"><span data-stu-id="4c006-177">tooregister a category handler for your notifications, you need tooadd a call once hello reach module is initialized.</span></span>

    AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
    [reach registerNotifier:myNotifier forCategory:@"my_category"];
    ...

<span data-ttu-id="4c006-178">`myNotifier`doit être une instance d’un objet qui est conforme toohello protocole `AENotifier`.</span><span class="sxs-lookup"><span data-stu-id="4c006-178">`myNotifier` must be an instance of an object that conforms toohello protocol `AENotifier`.</span></span>

<span data-ttu-id="4c006-179">Vous pouvez implémenter des méthodes de protocole hello par vous-même ou vous pouvez choisir tooreimplement hello existants de la classe `AEDefaultNotifier` qui exécute déjà la plupart du travail de hello.</span><span class="sxs-lookup"><span data-stu-id="4c006-179">You can implement hello protocol methods by yourself or you can choose tooreimplement hello existing class `AEDefaultNotifier` which already performs most of hello work.</span></span>

<span data-ttu-id="4c006-180">Par exemple, si vous souhaitez un affichage des notifications tooredefine hello pour une catégorie spécifique, vous pouvez suivre cet exemple :</span><span class="sxs-lookup"><span data-stu-id="4c006-180">For example, if you want tooredefine hello notification view for a specific category, you can follow this example:</span></span>

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

<span data-ttu-id="4c006-181">Cet exemple simple de catégorie part du principe que vous possédez un fichier nommé `MyNotificationView.xib` dans votre offre groupée d'applications principale.</span><span class="sxs-lookup"><span data-stu-id="4c006-181">This simple example of category assume that you have a file named `MyNotificationView.xib` in your main application bundle.</span></span> <span data-ttu-id="4c006-182">Si la méthode hello n’est pas en mesure de toofind correspondante `.xib`Engagement génère un message dans la console hello et notification de hello n’apparaissent pas.</span><span class="sxs-lookup"><span data-stu-id="4c006-182">If hello method is not able toofind a corresponding `.xib`, hello notification will not be displayed and Engagement will output a message in hello console.</span></span>

<span data-ttu-id="4c006-183">fichier nib de Hello fournie doit respecter hello suivant les règles :</span><span class="sxs-lookup"><span data-stu-id="4c006-183">hello provided nib file should respect hello following rules:</span></span>

* <span data-ttu-id="4c006-184">Il doit contenir une seule vue.</span><span class="sxs-lookup"><span data-stu-id="4c006-184">It should only contain one view.</span></span>
* <span data-ttu-id="4c006-185">Sous-vues doivent être de hello même de type hello celles à l’intérieur de fichier nib de hello fourni nommé`AENotificationView.xib`</span><span class="sxs-lookup"><span data-stu-id="4c006-185">Subviews should be of hello same types as hello ones inside hello provided nib file named `AENotificationView.xib`</span></span>
* <span data-ttu-id="4c006-186">Sous-vues doivent avoir hello même balises comme celles à l’intérieur de fichier nib de hello fourni nommé hello`AENotificationView.xib`</span><span class="sxs-lookup"><span data-stu-id="4c006-186">Subviews should have hello same tags as hello ones inside hello provided nib file named `AENotificationView.xib`</span></span>

> [!TIP]
> <span data-ttu-id="4c006-187">Simplement copier le fichier nib hello fourni nommé `AENotificationView.xib`et commencer à travailler à partir de là.</span><span class="sxs-lookup"><span data-stu-id="4c006-187">Just copy hello provided nib file, named `AENotificationView.xib`, and start working from there.</span></span> <span data-ttu-id="4c006-188">Mais attention, hello vue à l’intérieur de ce fichier nib est associé toohello classe `AENotificationView`.</span><span class="sxs-lookup"><span data-stu-id="4c006-188">But be careful, hello view inside this nib file is associated toohello class `AENotificationView`.</span></span> <span data-ttu-id="4c006-189">Cette classe redéfini méthode hello `layoutSubViews` toomove et redimensionner ses sous-vues selon toocontext.</span><span class="sxs-lookup"><span data-stu-id="4c006-189">This class redefined hello method `layoutSubViews` toomove and resize its subviews according toocontext.</span></span> <span data-ttu-id="4c006-190">Vous souhaiterez peut-être tooreplace avec un `UIView` ou la classe d’affichage personnalisé pour vous.</span><span class="sxs-lookup"><span data-stu-id="4c006-190">You may want tooreplace it with an `UIView` or you custom view class.</span></span>
>
>

<span data-ttu-id="4c006-191">Si vous avez besoin d’une personnalisation plus approfondie de vos notifications (si vous souhaitez que pour l’instance tooload votre vue directement à partir de code de hello), il est recommandé de tootake examiner hello a fourni la documentation de code et de la classe source de `Protocol ReferencesDefaultNotifier` et `AENotifier`.</span><span class="sxs-lookup"><span data-stu-id="4c006-191">If you need deeper customization of your notifications(if you want for instance tooload your view directly from hello code), it is recommended tootake a look at hello provided source code and class documentation of `Protocol ReferencesDefaultNotifier` and `AENotifier`.</span></span>

<span data-ttu-id="4c006-192">Notez que vous pouvez utiliser hello même notifiant pour plusieurs catégories.</span><span class="sxs-lookup"><span data-stu-id="4c006-192">Note that you can use hello same notifier for multiple categories.</span></span>

<span data-ttu-id="4c006-193">Vous pouvez le notificateur de valeur par défaut hello également redéfini comme suit :</span><span class="sxs-lookup"><span data-stu-id="4c006-193">You can also redefined hello default notifier like this:</span></span>

    AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
    [reach registerNotifier:myNotifier forCategory:kAEReachDefaultCategory];

##### <a name="notification-handling"></a><span data-ttu-id="4c006-194">Gestion des notifications</span><span class="sxs-lookup"><span data-stu-id="4c006-194">Notification handling</span></span>
<span data-ttu-id="4c006-195">Lorsque vous utilisez la catégorie par défaut de hello, certaines méthodes de cycle de vie sont appelées sur hello `AEReachContent` tooreport des statistiques et mise à jour hello campagne l’état de l’objet :</span><span class="sxs-lookup"><span data-stu-id="4c006-195">When using hello default category, some life cycle methods are called on hello `AEReachContent` object tooreport statistics and update hello campaign state:</span></span>

* <span data-ttu-id="4c006-196">Lors de la notification de hello s’affiche dans l’application, hello `displayNotification` méthode est appelée (qui fournit des statistiques) par `AEReachModule` si `handleNotification:` retourne `YES`.</span><span class="sxs-lookup"><span data-stu-id="4c006-196">When hello notification is displayed in application, hello `displayNotification` method is called (which reports statistics) by `AEReachModule` if `handleNotification:` returns `YES`.</span></span>
* <span data-ttu-id="4c006-197">Si la notification de hello est fermée, hello `exitNotification` méthode est appelée, la statistique est signalée et campagnes suivants peuvent maintenant être traités.</span><span class="sxs-lookup"><span data-stu-id="4c006-197">If hello notification is dismissed, hello `exitNotification` method is called, statistic is reported and next campaigns can now be processed.</span></span>
* <span data-ttu-id="4c006-198">Cliquez sur la notification de hello `actionNotification` est appelée, la statistique est signalée et hello associé action est effectuée.</span><span class="sxs-lookup"><span data-stu-id="4c006-198">If hello notification is clicked, `actionNotification` is called, statistic is reported and hello associated action is performed.</span></span>

<span data-ttu-id="4c006-199">Si votre implémentation de `AENotifier` contournements hello le comportement par défaut, vous pouvez toocall ces méthodes de cycle de vie vous-même.</span><span class="sxs-lookup"><span data-stu-id="4c006-199">If your implementation of `AENotifier` bypasses hello default behavior, you have toocall these life cycle methods by yourself.</span></span> <span data-ttu-id="4c006-200">Hello suivant exemples illustre certains cas où le comportement par défaut de hello est ignorée :</span><span class="sxs-lookup"><span data-stu-id="4c006-200">hello following examples illustrate some cases where hello default behavior is bypassed:</span></span>

* <span data-ttu-id="4c006-201">Vous n'étendez pas `AEDefaultNotifier`, par exemple, vous avez implémenté la gestion des catégories à partir de zéro.</span><span class="sxs-lookup"><span data-stu-id="4c006-201">You don't extend `AEDefaultNotifier`, e.g. you implemented category handling from scratch.</span></span>
* <span data-ttu-id="4c006-202">Vous a substitué `prepareNotificationView:forContent:`, être d’au moins sûr toomap `onNotificationActioned` ou `onNotificationExited` tooone de vos contrôles U.I.</span><span class="sxs-lookup"><span data-stu-id="4c006-202">You overrode `prepareNotificationView:forContent:`, be sure toomap at least `onNotificationActioned` or `onNotificationExited` tooone of your U.I controls.</span></span>

> [!WARNING]
> <span data-ttu-id="4c006-203">Si `handleNotification:` lève une exception, hello contenu est supprimé et `drop` est appelé, cela est signalé dans les statistiques et campagnes suivants peuvent maintenant être traités.</span><span class="sxs-lookup"><span data-stu-id="4c006-203">If `handleNotification:` throws an exception, hello content is deleted and `drop` is called, this is reported in statistics and next campaigns can now be processed.</span></span>
>
>

#### <a name="include-notification-as-part-of-an-existing-view"></a><span data-ttu-id="4c006-204">Incluez des notifications dans le cadre d'une vue existante</span><span class="sxs-lookup"><span data-stu-id="4c006-204">Include notification as part of an existing view</span></span>
<span data-ttu-id="4c006-205">Les superpositions sont idéales pour une intégration rapide mais peuvent parfois ne pas être pratiques ou avoir des effets secondaires indésirables.</span><span class="sxs-lookup"><span data-stu-id="4c006-205">Overlays are great for a fast integration but can be sometimes not convenient, or can have unwanted side effects.</span></span>

<span data-ttu-id="4c006-206">Si vous n’êtes pas satisfait de système de superposition hello dans certains de vos affichages, vous pouvez le personnaliser pour ces vues.</span><span class="sxs-lookup"><span data-stu-id="4c006-206">If you're not satisfied with hello overlay system in some of your views, you can customize it for these views.</span></span>

<span data-ttu-id="4c006-207">Vous pouvez décider tooinclude à notre disposition de notification dans vos vues existantes.</span><span class="sxs-lookup"><span data-stu-id="4c006-207">You can decide tooinclude our notification layout in your existing views.</span></span> <span data-ttu-id="4c006-208">toodo il y a donc deux styles de mise en œuvre :</span><span class="sxs-lookup"><span data-stu-id="4c006-208">toodo so, there is two implementation styles:</span></span>

1. <span data-ttu-id="4c006-209">Ajouter l’affichage des notifications hello à l’aide du constructeur d’interface</span><span class="sxs-lookup"><span data-stu-id="4c006-209">Add hello notification view using interface builder</span></span>

   * <span data-ttu-id="4c006-210">Ouvrez *Interface Builder*</span><span class="sxs-lookup"><span data-stu-id="4c006-210">Open *Interface Builder*</span></span>
   * <span data-ttu-id="4c006-211">Placez un 320 x 60 (ou si vous êtes sur iPad 768 x 60) `UIView` où vous souhaitez hello notification tooappear</span><span class="sxs-lookup"><span data-stu-id="4c006-211">Place a 320x60 (or 768x60 if you are on iPad) `UIView` where you want hello notification tooappear</span></span>
   * <span data-ttu-id="4c006-212">La valeur hello balise pour cette vue trop : **36822491**</span><span class="sxs-lookup"><span data-stu-id="4c006-212">Set hello Tag value for this view too: **36822491**</span></span>
2. <span data-ttu-id="4c006-213">Ajouter la vue des notifications hello par programmation.</span><span class="sxs-lookup"><span data-stu-id="4c006-213">Add hello notification view programmatically.</span></span> <span data-ttu-id="4c006-214">Ajoutez simplement hello suivant code lorsque votre vue a été initialisée :</span><span class="sxs-lookup"><span data-stu-id="4c006-214">Just add hello following code when your view has been initialized:</span></span>

       UIView* notificationView = [[UIView alloc] initWithFrame:CGRectMake(0, 0, 320, 60)]; //Replace x and y coordinate values tooyour needs.
       notificationView.tag = NOTIFICATION_AREA_VIEW_TAG;
       [self.view addSubview:notificationView];

<span data-ttu-id="4c006-215">La macro `NOTIFICATION_AREA_VIEW_TAG` se trouve dans `AEDefaultNotifier.h`.</span><span class="sxs-lookup"><span data-stu-id="4c006-215">`NOTIFICATION_AREA_VIEW_TAG` macro can be found in `AEDefaultNotifier.h`.</span></span>

> [!NOTE]
> <span data-ttu-id="4c006-216">notificateur de valeur par défaut Hello détecte automatiquement cette mise en page de notification hello est inclus dans cette vue et n’ajoute pas d’un segment de recouvrement pour celle-ci.</span><span class="sxs-lookup"><span data-stu-id="4c006-216">hello default notifier automatically detects that hello notification layout is included in this view and will not add an overlay for it.</span></span>
>
>

### <a name="announcements-and-polls"></a><span data-ttu-id="4c006-217">Annonces et sondages</span><span class="sxs-lookup"><span data-stu-id="4c006-217">Announcements and polls</span></span>
#### <a name="layouts"></a><span data-ttu-id="4c006-218">Mises en forme</span><span class="sxs-lookup"><span data-stu-id="4c006-218">Layouts</span></span>
<span data-ttu-id="4c006-219">Vous pouvez modifier les fichiers hello `AEDefaultAnnouncementView.xib` et `AEDefaultPollView.xib` tant que vous conservez les valeurs de balise hello et les types de sous-vues existant de hello.</span><span class="sxs-lookup"><span data-stu-id="4c006-219">You can modify hello files `AEDefaultAnnouncementView.xib` and `AEDefaultPollView.xib` as long as you keep hello tag values and types of hello existing subviews.</span></span>

#### <a name="categories"></a><span data-ttu-id="4c006-220">Catégories</span><span class="sxs-lookup"><span data-stu-id="4c006-220">Categories</span></span>
##### <a name="alternate-layouts"></a><span data-ttu-id="4c006-221">Autres dispositions</span><span class="sxs-lookup"><span data-stu-id="4c006-221">Alternate layouts</span></span>
<span data-ttu-id="4c006-222">Telles que les notifications, catégorie de la campagne hello peut être utilisé toohave des formes différentes vos annonces et les interroge.</span><span class="sxs-lookup"><span data-stu-id="4c006-222">Like notifications, hello campaign's category can be used toohave alternate layouts for your announcements and polls.</span></span>

<span data-ttu-id="4c006-223">toocreate une catégorie pour une annonce, vous devez étendre **AEAnnouncementViewController** et l’inscrire une fois le module de couverture hello a été initialisé :</span><span class="sxs-lookup"><span data-stu-id="4c006-223">toocreate a category for an announcement, you must extend **AEAnnouncementViewController** and register it once hello reach module has been initialized:</span></span>

    AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
    [reach registerAnnouncementController:[MyCustomAnnouncementViewController class] forCategory:@"my_category"];

> [!NOTE]
> <span data-ttu-id="4c006-224">Chaque fois un utilisateur clique sur une notification pour une annonce avec la catégorie de hello « mon\_catégorie », votre contrôleur d’affichage inscrits (dans ce cas `MyCustomAnnouncementViewController`) sera initialisé en appelant la méthode hello `initWithAnnouncement:` et affichage de hello sera fenêtre d’application actuelle toohello ajouté.</span><span class="sxs-lookup"><span data-stu-id="4c006-224">Each time a user will click on a notification for an announcement with hello category "my\_category", your registered view controller (in that case `MyCustomAnnouncementViewController`) will be initialized by calling hello method `initWithAnnouncement:` and hello view will be added toohello current application window.</span></span>
>
>

<span data-ttu-id="4c006-225">Dans votre implémentation de hello `AEAnnouncementViewController` classe que vous aurez une propriété de hello tooread `announcement` tooinitialize votre sous-vues.</span><span class="sxs-lookup"><span data-stu-id="4c006-225">In your implementation of hello `AEAnnouncementViewController` class you will have tooread hello property `announcement` tooinitialize your subviews.</span></span> <span data-ttu-id="4c006-226">Considérez l’exemple hello ci-dessous, où deux étiquettes sont initialisés à l’aide de `title` et `body` propriétés Hello `AEReachAnnouncement` classe :</span><span class="sxs-lookup"><span data-stu-id="4c006-226">Consider hello example below, where two labels are initialized using `title` and `body` properties of hello `AEReachAnnouncement` class:</span></span>

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

<span data-ttu-id="4c006-227">Si vous ne souhaitez pas vos vues tooload par vous-même mais que vous souhaitiez simplement la disposition de vue annonce tooreuse hello par défaut, vous pouvez simplement mettre le contrôleur de votre affichage personnalisé étend la classe hello fourni `AEDefaultAnnouncementViewController`.</span><span class="sxs-lookup"><span data-stu-id="4c006-227">If you don't want tooload your views by yourself but you just want tooreuse hello default announcement view layout, you can simply make your custom view controller extends hello provided class `AEDefaultAnnouncementViewController`.</span></span> <span data-ttu-id="4c006-228">Dans ce cas, en double fichier nib de hello `AEDefaultAnnouncementView.xib` et renommez-la peut être chargé par le contrôleur de votre affichage personnalisé (pour un contrôleur nommé `CustomAnnouncementViewController`, vous devez appeler votre fichier nib `CustomAnnouncementView.xib`).</span><span class="sxs-lookup"><span data-stu-id="4c006-228">In that case, duplicate hello nib file `AEDefaultAnnouncementView.xib` and rename it so it can be loaded by your custom view controller (for a controller named `CustomAnnouncementViewController`, you should call your nib file `CustomAnnouncementView.xib`).</span></span>

<span data-ttu-id="4c006-229">catégorie de par défaut hello tooreplace des annonces, inscrire simplement votre contrôleur de vue personnalisée pour la catégorie hello définie dans `kAEReachDefaultCategory`:</span><span class="sxs-lookup"><span data-stu-id="4c006-229">tooreplace hello default category of announcements, simply register your custom view controller for hello category defined in `kAEReachDefaultCategory`:</span></span>

    [reach registerAnnouncementController:[MyCustomAnnouncementViewController class] forCategory:kAEReachDefaultCategory];

<span data-ttu-id="4c006-230">Interroge peut être personnalisée hello identique :</span><span class="sxs-lookup"><span data-stu-id="4c006-230">Polls can be customized hello same way :</span></span>

    AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
    [reach registerPollController:[MyCustomPollViewController class] forCategory:@"my_category"];

<span data-ttu-id="4c006-231">Cette fois-ci, le hello fourni `MyCustomPollViewController` doit étendre `AEPollViewController`.</span><span class="sxs-lookup"><span data-stu-id="4c006-231">This time, hello provided `MyCustomPollViewController` must extend `AEPollViewController`.</span></span> <span data-ttu-id="4c006-232">Ou vous pouvez choisir tooextend à partir du contrôleur hello par défaut : `AEDefaultPollViewController`.</span><span class="sxs-lookup"><span data-stu-id="4c006-232">Or you can choose tooextend from hello default controller: `AEDefaultPollViewController`.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4c006-233">N’oubliez pas toocall soit `action` (`submitAnswers:` pour l’affichage des contrôleurs de sondage personnalisé) ou `exit` avant le contrôleur d’affichage hello est fermée.</span><span class="sxs-lookup"><span data-stu-id="4c006-233">Don't forget toocall either `action` (`submitAnswers:` for custom poll view controllers) or `exit` method before hello view controller is dismissed.</span></span> <span data-ttu-id="4c006-234">Sinon, les statistiques ne seront pas envoyées (autrement dit, aucune analytique sur une campagne de hello) et plus de campagnes important suivant ne seront pas informés qu’après le redémarrage du processus d’application hello.</span><span class="sxs-lookup"><span data-stu-id="4c006-234">Otherwise, statistics won't be sent (i.e. no analytics on hello campaign) and more importantly next campaigns will not be notified until hello application process is restarted.</span></span>
>
>

##### <a name="implementation-example"></a><span data-ttu-id="4c006-235">Exemple d'implémentation</span><span class="sxs-lookup"><span data-stu-id="4c006-235">Implementation example</span></span>
<span data-ttu-id="4c006-236">Dans cette implémentation, vue d’annonce personnalisée hello est chargé à partir d’un fichier xib externe.</span><span class="sxs-lookup"><span data-stu-id="4c006-236">In this implementation hello custom announcement view is loaded from an external xib file.</span></span>

<span data-ttu-id="4c006-237">Comme pour la personnalisation de la notification avancés, il est recommandé toolook au code source de hello d’implémentation standard de hello.</span><span class="sxs-lookup"><span data-stu-id="4c006-237">Like for advanced notification customization, it is recommended toolook at hello source code of hello standard implementation.</span></span>

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
