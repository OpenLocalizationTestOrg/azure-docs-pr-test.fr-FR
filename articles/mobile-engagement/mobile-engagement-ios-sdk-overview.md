---
title: "aaaAzure Mobile Engagement iOS présentation du kit SDK | Documents Microsoft"
description: "Dernières mises à jour et procédures du Kit de développement logiciel (SDK) iOS pour Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 3a03bbd6-bcf8-436c-9775-5a8188629252
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 07/17/2017
ms.author: piyushjo
ms.openlocfilehash: 38f0da2f84df9c62f8fbca233bfda8b9936fdc0f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="ios-sdk-for-azure-mobile-engagement"></a><span data-ttu-id="3d3cb-103">Kit de développement logiciel (SDK) iOS pour Azure Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="3d3cb-103">iOS SDK for Azure Mobile Engagement</span></span>
<span data-ttu-id="3d3cb-104">Mise en route tooget tous les détails de hello sur la façon de toointegrate Azure Mobile Engagement dans une application iOS.</span><span class="sxs-lookup"><span data-stu-id="3d3cb-104">Start here tooget all hello details on how toointegrate Azure Mobile Engagement in an iOS App.</span></span> <span data-ttu-id="3d3cb-105">Si vous souhaitez que toogive il essayer en premier lieu, assurez-vous que vous faire nos [didacticiel de 15 minutes](mobile-engagement-ios-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="3d3cb-105">If you'd like toogive it a try first, make sure you do our [15 minutes tutorial](mobile-engagement-ios-get-started.md).</span></span>

<span data-ttu-id="3d3cb-106">Cliquez sur toosee hello [contenu du Kit de développement logiciel](mobile-engagement-ios-sdk-content.md)</span><span class="sxs-lookup"><span data-stu-id="3d3cb-106">Click toosee hello [SDK Content](mobile-engagement-ios-sdk-content.md)</span></span>

## <a name="integration-procedures"></a><span data-ttu-id="3d3cb-107">Procédures d'intégration</span><span class="sxs-lookup"><span data-stu-id="3d3cb-107">Integration procedures</span></span>
1. <span data-ttu-id="3d3cb-108">Démarrez ici : [comment toointegrate Mobile Engagement dans votre application iOS](mobile-engagement-ios-integrate-engagement.md)</span><span class="sxs-lookup"><span data-stu-id="3d3cb-108">Start here: [How toointegrate Mobile Engagement in your iOS app](mobile-engagement-ios-integrate-engagement.md)</span></span>
2. <span data-ttu-id="3d3cb-109">Pour les Notifications : [comment toointegrate portée (Notifications) dans votre application iOS](mobile-engagement-ios-integrate-engagement-reach.md)</span><span class="sxs-lookup"><span data-stu-id="3d3cb-109">For Notifications: [How toointegrate Reach (Notifications) in your iOS app](mobile-engagement-ios-integrate-engagement-reach.md)</span></span>
3. <span data-ttu-id="3d3cb-110">Implémentation d’un plan de la balise : [comment toouse hello avancé Mobile Engagement marquage API dans votre application iOS](mobile-engagement-ios-use-engagement-api.md)</span><span class="sxs-lookup"><span data-stu-id="3d3cb-110">Tag plan implementation: [How toouse hello advanced Mobile Engagement tagging API in your iOS app](mobile-engagement-ios-use-engagement-api.md)</span></span>

## <a name="release-notes"></a><span data-ttu-id="3d3cb-111">Notes de publication</span><span class="sxs-lookup"><span data-stu-id="3d3cb-111">Release notes</span></span>
### <a name="410-07172017"></a><span data-ttu-id="3d3cb-112">4.1.0 (07/17/2017)</span><span class="sxs-lookup"><span data-stu-id="3d3cb-112">4.1.0 (07/17/2017)</span></span>
* <span data-ttu-id="3d3cb-113">Correction des badges effacés en arrière-plan.</span><span class="sxs-lookup"><span data-stu-id="3d3cb-113">Fixed badges cleared in background.</span></span>
* <span data-ttu-id="3d3cb-114">Correction des avertissements sur XCode 9 à propos des API qui ne sont pas appelées dans la file d’attente principale.</span><span class="sxs-lookup"><span data-stu-id="3d3cb-114">Fixed warnings on XCode 9 about APIs not called in main queue.</span></span>
* <span data-ttu-id="3d3cb-115">Correction d’une fuite de mémoire dans les sondages Reach.</span><span class="sxs-lookup"><span data-stu-id="3d3cb-115">Fixed a memory leak in Reach polls.</span></span>
* <span data-ttu-id="3d3cb-116">Fin de la prise en charge d’iOS 6.X.</span><span class="sxs-lookup"><span data-stu-id="3d3cb-116">Dropped support for iOS 6.X.</span></span> <span data-ttu-id="3d3cb-117">À partir de cette cible de déploiement hello version de votre application doit être au moins iOS 7.</span><span class="sxs-lookup"><span data-stu-id="3d3cb-117">Starting from this version hello deployment target of your application must be at least iOS 7.</span></span>

<span data-ttu-id="3d3cb-118">Pour les versions antérieures, consultez hello [terminer les notes de publication](mobile-engagement-ios-release-notes.md)</span><span class="sxs-lookup"><span data-stu-id="3d3cb-118">For earlier version please see hello [complete release notes](mobile-engagement-ios-release-notes.md)</span></span>

## <a name="upgrade-procedures"></a><span data-ttu-id="3d3cb-119">Procédures de mise à niveau</span><span class="sxs-lookup"><span data-stu-id="3d3cb-119">Upgrade procedures</span></span>
<span data-ttu-id="3d3cb-120">Si vous avez déjà intégré une version antérieure d’implication dans votre application, vous avez hello tooconsider hello Kit de développement logiciel de la mise à niveau les points suivants.</span><span class="sxs-lookup"><span data-stu-id="3d3cb-120">If you already have integrated an older version of Engagement into your application, you have tooconsider hello following points when upgrading hello SDK.</span></span>

<span data-ttu-id="3d3cb-121">Vous avez peut-être toofollow plusieurs procédures issue de plusieurs versions de hello SDK Voir hello complète [mise à niveau des procédures](mobile-engagement-ios-upgrade-procedure.md).</span><span class="sxs-lookup"><span data-stu-id="3d3cb-121">You may have toofollow several procedures if you missed several versions of hello SDK see hello complete [Upgrade Procedures](mobile-engagement-ios-upgrade-procedure.md).</span></span>

<span data-ttu-id="3d3cb-122">Pour chaque nouvelle version du Kit de développement logiciel de hello vous devez d’abord remplacer (supprimer et importer de nouveau dans xcode) hello dossiers EngagementSDK et EngagementReach.</span><span class="sxs-lookup"><span data-stu-id="3d3cb-122">For each new version of hello SDK you must first replace (remove and re-import in xcode) hello EngagementSDK and EngagementReach folders.</span></span>

### <a name="from-300-too400"></a><span data-ttu-id="3d3cb-123">À partir de 3.0.0 too4.0.0</span><span class="sxs-lookup"><span data-stu-id="3d3cb-123">From 3.0.0 too4.0.0</span></span>
### <a name="xcode-8"></a><span data-ttu-id="3d3cb-124">XCode 8</span><span class="sxs-lookup"><span data-stu-id="3d3cb-124">XCode 8</span></span>
<span data-ttu-id="3d3cb-125">XCode 8 est obligatoire à partir de la version 4.0.0 Hello SDK.</span><span class="sxs-lookup"><span data-stu-id="3d3cb-125">XCode 8 is mandatory starting from version 4.0.0 of hello SDK.</span></span>

> [!NOTE]
> <span data-ttu-id="3d3cb-126">Si vous dépendez vraiment de XCode 7, vous pouvez utiliser hello [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh).</span><span class="sxs-lookup"><span data-stu-id="3d3cb-126">If you really depend on XCode 7 then you may use hello [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh).</span></span> <span data-ttu-id="3d3cb-127">Il existe un bogue connu sur le module de couverture hello de cette version précédente lors de l’exécution sur les appareils iOS 10 : notifications système ne sont pas activées.</span><span class="sxs-lookup"><span data-stu-id="3d3cb-127">There is a known bug on hello reach module of this previous version while running on iOS 10 devices:  system notifications are not actioned.</span></span> <span data-ttu-id="3d3cb-128">toofix avoir tooimplement hello déconseillé API `application:didReceiveRemoteNotification:` dans votre application déléguer comme suit :</span><span class="sxs-lookup"><span data-stu-id="3d3cb-128">toofix this you will have tooimplement hello deprecated API `application:didReceiveRemoteNotification:` in your app delegate as follows:</span></span>
>
>

    - (void)application:(UIApplication*)application
    didReceiveRemoteNotification:(NSDictionary*)userInfo
    {
        [[EngagementAgent shared] applicationDidReceiveRemoteNotification:userInfo fetchCompletionHandler:nil];
    }

> [!IMPORTANT]
> <span data-ttu-id="3d3cb-129">**Nous ne recommandons pas cette solution de contournement** : ce comportement peut changer dans une prochaine mise à niveau (même mineure) de la version iOS car cette API iOS est déconseillée.</span><span class="sxs-lookup"><span data-stu-id="3d3cb-129">**We do not recommend this workaround** as this behavior can change in any upcoming (even minor) iOS version upgrade because this iOS API is deprecated.</span></span> <span data-ttu-id="3d3cb-130">Vous devez basculer tooXCode 8 dès que possible.</span><span class="sxs-lookup"><span data-stu-id="3d3cb-130">You should switch tooXCode 8 as soon as possible.</span></span>
>
>

#### <a name="usernotifications-framework"></a><span data-ttu-id="3d3cb-131">Infrastructure UserNotifications</span><span class="sxs-lookup"><span data-stu-id="3d3cb-131">UserNotifications framework</span></span>
<span data-ttu-id="3d3cb-132">Vous devez tooadd hello `UserNotifications` framework dans les Phases de votre Build.</span><span class="sxs-lookup"><span data-stu-id="3d3cb-132">You need tooadd hello `UserNotifications` framework in your Build Phases.</span></span>

<span data-ttu-id="3d3cb-133">dans l’Explorateur de projets hello, ouvrir votre projet et sélectionnez cible hello.</span><span class="sxs-lookup"><span data-stu-id="3d3cb-133">in hello project explorer, open your project pane and select hello correct target.</span></span> <span data-ttu-id="3d3cb-134">Ensuite, ouvrez hello **« Build phases »** onglet et Bonjour **« Binaire avec des bibliothèques de liens »** menu, ajoutez framework `UserNotifications.framework` -définir un lien hello en tant que`Optional`</span><span class="sxs-lookup"><span data-stu-id="3d3cb-134">Then, open hello **"Build phases"** tab and in hello **"Link Binary With Libraries"** menu, add framework `UserNotifications.framework` - set hello link as `Optional`</span></span>

#### <a name="application-push-capability"></a><span data-ttu-id="3d3cb-135">Fonctionnalité push de l’application</span><span class="sxs-lookup"><span data-stu-id="3d3cb-135">Application push capability</span></span>
<span data-ttu-id="3d3cb-136">XCode 8 peut réinitialiser votre application push de capacité, vérifiez qu’il Bonjour `capability` onglet de votre cible sélectionné.</span><span class="sxs-lookup"><span data-stu-id="3d3cb-136">XCode 8 may reset your app push capability, please double check it in hello `capability` tab of your selected target.</span></span>

#### <a name="add-hello-new-ios-10-notification-registration-code"></a><span data-ttu-id="3d3cb-137">Ajouter du code d’enregistrement notification 10 iOS hello</span><span class="sxs-lookup"><span data-stu-id="3d3cb-137">Add hello new iOS 10 notification registration code</span></span>
<span data-ttu-id="3d3cb-138">Hello plus anciens code extrait tooregister application hello toonotifications fonctionne toujours, mais utilise les API déconseillées lors de l’exécution sur iOS 10.</span><span class="sxs-lookup"><span data-stu-id="3d3cb-138">hello older code snippet tooregister hello app toonotifications still works but is using deprecated APIs while running on iOS 10.</span></span>

<span data-ttu-id="3d3cb-139">Hello d’importation `User Notification` framework :</span><span class="sxs-lookup"><span data-stu-id="3d3cb-139">Import hello `User Notification` framework:</span></span>

        #import <UserNotifications/UserNotifications.h>

<span data-ttu-id="3d3cb-140">Dans la méthode `application:didFinishLaunchingWithOptions` de votre délégué d’application remplacez :</span><span class="sxs-lookup"><span data-stu-id="3d3cb-140">In your application delegate `application:didFinishLaunchingWithOptions` method replace:</span></span>

        if ([application respondsToSelector:@selector(registerUserNotificationSettings:)]) {
            [application registerUserNotificationSettings:[UIUserNotificationSettings settingsForTypes:(UIUserNotificationTypeBadge | UIUserNotificationTypeSound | UIUserNotificationTypeAlert) categories:nil]];
            [application registerForRemoteNotifications];
        }
        else {

            [application registerForRemoteNotificationTypes:(UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound | UIRemoteNotificationTypeAlert)];
        }

<span data-ttu-id="3d3cb-141">par :</span><span class="sxs-lookup"><span data-stu-id="3d3cb-141">by :</span></span>

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

#### <a name="resolve-unusernotificationcenter-delegate-conflicts"></a><span data-ttu-id="3d3cb-142">Résoudre les conflits de délégués UNUserNotificationCenter</span><span class="sxs-lookup"><span data-stu-id="3d3cb-142">Resolve UNUserNotificationCenter delegate conflicts</span></span>

<span data-ttu-id="3d3cb-143">*Si, ni votre application ni l’une des bibliothèques tierces n’implémente un `UNUserNotificationCenterDelegate`, vous pouvez ignorer cette partie.*</span><span class="sxs-lookup"><span data-stu-id="3d3cb-143">*If neither your application or one of your third party libraries implements a `UNUserNotificationCenterDelegate` then you can skip this part.*</span></span>

<span data-ttu-id="3d3cb-144">A `UNUserNotificationCenter` délégué est utilisé par le cycle de vie hello SDK toomonitor hello de notifications d’Engagement sur les appareils qui exécutent sur iOS ou supérieure à 10.</span><span class="sxs-lookup"><span data-stu-id="3d3cb-144">A `UNUserNotificationCenter` delegate is used by hello SDK toomonitor hello life cycle of Engagement notifications on devices running on iOS 10 or greater.</span></span> <span data-ttu-id="3d3cb-145">Hello SDK possède sa propre implémentation de hello `UNUserNotificationCenterDelegate` de protocole, mais il peut y avoir qu’un seul `UNUserNotificationCenter` déléguer par application.</span><span class="sxs-lookup"><span data-stu-id="3d3cb-145">hello SDK has its own implementation of hello `UNUserNotificationCenterDelegate` protocol but there can be only one `UNUserNotificationCenter` delegate per application.</span></span> <span data-ttu-id="3d3cb-146">Tout autre délégué ajouté toohello `UNUserNotificationCenter` objet est en conflit avec hello Engagement une.</span><span class="sxs-lookup"><span data-stu-id="3d3cb-146">Any other delegate added toohello `UNUserNotificationCenter` object will conflict with hello Engagement one.</span></span> <span data-ttu-id="3d3cb-147">Si hello SDK détecte le délégué de votre ou de plusieurs autres tiers alors qu’il n’utilise pas sa propre implémentation toogive vous une chance tooresolve hello est en conflit.</span><span class="sxs-lookup"><span data-stu-id="3d3cb-147">If hello SDK detects your or any other third party's delegate then it will not use its own implementation toogive you a chance tooresolve hello conflicts.</span></span> <span data-ttu-id="3d3cb-148">Vous devez tooadd hello Engagement logique tooyour possèdent des conflits de hello tooresolve délégué dans l’ordre.</span><span class="sxs-lookup"><span data-stu-id="3d3cb-148">You will have tooadd hello Engagement logic tooyour own delegate in order tooresolve hello conflicts.</span></span>

<span data-ttu-id="3d3cb-149">Il existe deux façons tooachieve cela.</span><span class="sxs-lookup"><span data-stu-id="3d3cb-149">There are two ways tooachieve this.</span></span>

<span data-ttu-id="3d3cb-150">Proposition de 1, simplement en transfert votre délégué appelle toohello SDK :</span><span class="sxs-lookup"><span data-stu-id="3d3cb-150">Proposal 1, simply by forwarding your delegate calls toohello SDK:</span></span>

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

<span data-ttu-id="3d3cb-151">Ou 2, en héritant de hello `AEUserNotificationHandler` classe</span><span class="sxs-lookup"><span data-stu-id="3d3cb-151">Or proposal 2, by inheriting from hello `AEUserNotificationHandler` class</span></span>

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
> <span data-ttu-id="3d3cb-152">Vous pouvez déterminer si une notification d’Engagement ou non, en passant son `userInfo` dictionnaire toohello Agent `isEngagementPushPayload:` méthode de classe.</span><span class="sxs-lookup"><span data-stu-id="3d3cb-152">You can determine whether a notification comes from Engagement or not by passing its `userInfo` dictionary toohello Agent `isEngagementPushPayload:` class method.</span></span>

<span data-ttu-id="3d3cb-153">Vérifiez que hello `UNUserNotificationCenter` délégué de l’objet a la valeur délégué tooyour dans soit hello `application:willFinishLaunchingWithOptions:` ou hello `application:didFinishLaunchingWithOptions:` méthode du délégué de votre application.</span><span class="sxs-lookup"><span data-stu-id="3d3cb-153">Make sure that hello `UNUserNotificationCenter` object's delegate is set tooyour delegate within either hello `application:willFinishLaunchingWithOptions:` or hello `application:didFinishLaunchingWithOptions:` method of your application delegate.</span></span>
<span data-ttu-id="3d3cb-154">Par exemple, si vous avez implémenté hello ci-dessus proposition 1 :</span><span class="sxs-lookup"><span data-stu-id="3d3cb-154">For instance, if you implemented hello above proposal 1:</span></span>

      - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
        // Any other code

        [UNUserNotificationCenter currentNotificationCenter].delegate = self;
        return YES;
      }
