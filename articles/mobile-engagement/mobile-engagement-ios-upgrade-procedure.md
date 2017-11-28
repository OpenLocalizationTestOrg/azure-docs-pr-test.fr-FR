---
title: "aaaAzure Mobile Engagement iOS procédure de mise à niveau de SDK | Documents Microsoft"
description: "Dernières mises à jour et procédures du Kit de développement logiciel (SDK) iOS pour Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 72a9e493-3f14-4e52-b6e2-0490fd04b184
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 12/13/2016
ms.author: piyushjo
ms.openlocfilehash: 5a81bcaaec72aec665b3334e6400d520454d56a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-procedures"></a><span data-ttu-id="40d4a-103">Procédures de mise à niveau</span><span class="sxs-lookup"><span data-stu-id="40d4a-103">Upgrade procedures</span></span>
<span data-ttu-id="40d4a-104">Si vous avez déjà intégré une version antérieure d’implication dans votre application, vous avez hello tooconsider hello Kit de développement logiciel de la mise à niveau les points suivants.</span><span class="sxs-lookup"><span data-stu-id="40d4a-104">If you already have integrated an older version of Engagement into your application, you have tooconsider hello following points when upgrading hello SDK.</span></span>

<span data-ttu-id="40d4a-105">Pour chaque nouvelle version du Kit de développement logiciel de hello vous devez d’abord remplacer (supprimer et importer de nouveau dans xcode) hello dossiers EngagementSDK et EngagementReach.</span><span class="sxs-lookup"><span data-stu-id="40d4a-105">For each new version of hello SDK you must first replace (remove and re-import in xcode) hello EngagementSDK and EngagementReach folders.</span></span>

## <a name="from-300-too400"></a><span data-ttu-id="40d4a-106">À partir de 3.0.0 too4.0.0</span><span class="sxs-lookup"><span data-stu-id="40d4a-106">From 3.0.0 too4.0.0</span></span>
### <a name="xcode-8"></a><span data-ttu-id="40d4a-107">XCode 8</span><span class="sxs-lookup"><span data-stu-id="40d4a-107">XCode 8</span></span>
<span data-ttu-id="40d4a-108">XCode 8 est obligatoire à partir de la version 4.0.0 Hello SDK.</span><span class="sxs-lookup"><span data-stu-id="40d4a-108">XCode 8 is mandatory starting from version 4.0.0 of hello SDK.</span></span>

> [!NOTE]
> <span data-ttu-id="40d4a-109">Si vous dépendez vraiment de XCode 7, vous pouvez utiliser hello [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh).</span><span class="sxs-lookup"><span data-stu-id="40d4a-109">If you really depend on XCode 7 then you may use hello [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh).</span></span> <span data-ttu-id="40d4a-110">Il existe un bogue connu sur le module de couverture hello de cette version précédente lors de l’exécution sur les appareils iOS 10 : notifications système ne sont pas activées.</span><span class="sxs-lookup"><span data-stu-id="40d4a-110">There is a known bug on hello reach module of this previous version while running on iOS 10 devices:  system notifications are not actioned.</span></span> <span data-ttu-id="40d4a-111">toofix avoir tooimplement hello déconseillé API `application:didReceiveRemoteNotification:` dans votre application déléguer comme suit :</span><span class="sxs-lookup"><span data-stu-id="40d4a-111">toofix this you will have tooimplement hello deprecated API `application:didReceiveRemoteNotification:` in your app delegate as follows:</span></span>
> 
> 

    - (void)application:(UIApplication*)application
    didReceiveRemoteNotification:(NSDictionary*)userInfo
    {
        [[EngagementAgent shared] applicationDidReceiveRemoteNotification:userInfo fetchCompletionHandler:nil];
    }

> [!IMPORTANT]
> <span data-ttu-id="40d4a-112">**Nous ne recommandons pas cette solution de contournement** : ce comportement peut changer dans une prochaine mise à niveau (même mineure) de la version iOS car cette API iOS est déconseillée.</span><span class="sxs-lookup"><span data-stu-id="40d4a-112">**We do not recommend this workaround** as this behavior can change in any upcoming (even minor) iOS version upgrade because this iOS API is deprecated.</span></span> <span data-ttu-id="40d4a-113">Vous devez basculer tooXCode 8 dès que possible.</span><span class="sxs-lookup"><span data-stu-id="40d4a-113">You should switch tooXCode 8 as soon as possible.</span></span>
> 
> 

### <a name="usernotifications-framework"></a><span data-ttu-id="40d4a-114">Infrastructure UserNotifications</span><span class="sxs-lookup"><span data-stu-id="40d4a-114">UserNotifications framework</span></span>
<span data-ttu-id="40d4a-115">Vous devez tooadd hello `UserNotifications` framework dans les Phases de votre Build.</span><span class="sxs-lookup"><span data-stu-id="40d4a-115">You need tooadd hello `UserNotifications` framework in your Build Phases.</span></span>

<span data-ttu-id="40d4a-116">dans l’Explorateur de projets hello, ouvrir votre projet et sélectionnez cible hello.</span><span class="sxs-lookup"><span data-stu-id="40d4a-116">in hello project explorer, open your project pane and select hello correct target.</span></span> <span data-ttu-id="40d4a-117">Ensuite, ouvrez hello **« Build phases »** onglet et Bonjour **« Binaire avec des bibliothèques de liens »** menu, ajoutez framework `UserNotifications.framework` -définir un lien hello en tant que`Optional`</span><span class="sxs-lookup"><span data-stu-id="40d4a-117">Then, open hello **"Build phases"** tab and in hello **"Link Binary With Libraries"** menu, add framework `UserNotifications.framework` - set hello link as `Optional`</span></span>

### <a name="application-push-capability"></a><span data-ttu-id="40d4a-118">Fonctionnalité push de l’application</span><span class="sxs-lookup"><span data-stu-id="40d4a-118">Application push capability</span></span>
<span data-ttu-id="40d4a-119">XCode 8 peut réinitialiser votre application push de capacité, vérifiez qu’il Bonjour `capability` onglet de votre cible sélectionné.</span><span class="sxs-lookup"><span data-stu-id="40d4a-119">XCode 8 may reset your app push capability, please double check it in hello `capability` tab of your selected target.</span></span>

### <a name="add-hello-new-ios-10-notification-registration-code"></a><span data-ttu-id="40d4a-120">Ajouter du code d’enregistrement notification 10 iOS hello</span><span class="sxs-lookup"><span data-stu-id="40d4a-120">Add hello new iOS 10 notification registration code</span></span>
<span data-ttu-id="40d4a-121">Hello plus anciens code extrait tooregister application hello toonotifications fonctionne toujours, mais utilise les API déconseillées lors de l’exécution sur iOS 10.</span><span class="sxs-lookup"><span data-stu-id="40d4a-121">hello older code snippet tooregister hello app toonotifications still works but is using deprecated APIs while running on iOS 10.</span></span>

<span data-ttu-id="40d4a-122">Hello d’importation `User Notification` framework :</span><span class="sxs-lookup"><span data-stu-id="40d4a-122">Import hello `User Notification` framework:</span></span>

        #import <UserNotifications/UserNotifications.h> 

<span data-ttu-id="40d4a-123">Dans la méthode `application:didFinishLaunchingWithOptions` de votre délégué d’application remplacez :</span><span class="sxs-lookup"><span data-stu-id="40d4a-123">In your application delegate `application:didFinishLaunchingWithOptions` method replace:</span></span>

    if ([application respondsToSelector:@selector(registerUserNotificationSettings:)]) {
        [application registerUserNotificationSettings:[UIUserNotificationSettings settingsForTypes:(UIUserNotificationTypeBadge | UIUserNotificationTypeSound | UIUserNotificationTypeAlert) categories:nil]];
        [application registerForRemoteNotifications];
    }
    else {

        [application registerForRemoteNotificationTypes:(UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound | UIRemoteNotificationTypeAlert)];
    }

<span data-ttu-id="40d4a-124">par :</span><span class="sxs-lookup"><span data-stu-id="40d4a-124">by :</span></span>

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

### <a name="resolve-unusernotificationcenter-delegate-conflicts"></a><span data-ttu-id="40d4a-125">Résoudre les conflits de délégués UNUserNotificationCenter</span><span class="sxs-lookup"><span data-stu-id="40d4a-125">Resolve UNUserNotificationCenter delegate conflicts</span></span>

<span data-ttu-id="40d4a-126">*Si, ni votre application ni l’une des bibliothèques tierces n’implémente un `UNUserNotificationCenterDelegate`, vous pouvez ignorer cette partie.*</span><span class="sxs-lookup"><span data-stu-id="40d4a-126">*If neither your application or one of your third party libraries implements a `UNUserNotificationCenterDelegate` then you can skip this part.*</span></span>

<span data-ttu-id="40d4a-127">A `UNUserNotificationCenter` délégué est utilisé par le cycle de vie hello SDK toomonitor hello de notifications d’Engagement sur les appareils qui exécutent sur iOS ou supérieure à 10.</span><span class="sxs-lookup"><span data-stu-id="40d4a-127">A `UNUserNotificationCenter` delegate is used by hello SDK toomonitor hello life cycle of Engagement notifications on devices running on iOS 10 or greater.</span></span> <span data-ttu-id="40d4a-128">Hello SDK possède sa propre implémentation de hello `UNUserNotificationCenterDelegate` de protocole, mais il peut y avoir qu’un seul `UNUserNotificationCenter` déléguer par application.</span><span class="sxs-lookup"><span data-stu-id="40d4a-128">hello SDK has its own implementation of hello `UNUserNotificationCenterDelegate` protocol but there can be only one `UNUserNotificationCenter` delegate per application.</span></span> <span data-ttu-id="40d4a-129">Tout autre délégué ajouté toohello `UNUserNotificationCenter` objet est en conflit avec hello Engagement une.</span><span class="sxs-lookup"><span data-stu-id="40d4a-129">Any other delegate added toohello `UNUserNotificationCenter` object will conflict with hello Engagement one.</span></span> <span data-ttu-id="40d4a-130">Si hello SDK détecte le délégué de votre ou de plusieurs autres tiers alors qu’il n’utilise pas sa propre implémentation toogive vous une chance tooresolve hello est en conflit.</span><span class="sxs-lookup"><span data-stu-id="40d4a-130">If hello SDK detects your or any other third party's delegate then it will not use its own implementation toogive you a chance tooresolve hello conflicts.</span></span> <span data-ttu-id="40d4a-131">Vous devez tooadd hello Engagement logique tooyour possèdent des conflits de hello tooresolve délégué dans l’ordre.</span><span class="sxs-lookup"><span data-stu-id="40d4a-131">You will have tooadd hello Engagement logic tooyour own delegate in order tooresolve hello conflicts.</span></span>

<span data-ttu-id="40d4a-132">Il existe deux façons tooachieve cela.</span><span class="sxs-lookup"><span data-stu-id="40d4a-132">There are two ways tooachieve this.</span></span>

<span data-ttu-id="40d4a-133">Proposition de 1, simplement en transfert votre délégué appelle toohello SDK :</span><span class="sxs-lookup"><span data-stu-id="40d4a-133">Proposal 1, simply by forwarding your delegate calls toohello SDK:</span></span>

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

<span data-ttu-id="40d4a-134">Ou 2, en héritant de hello `AEUserNotificationHandler` classe</span><span class="sxs-lookup"><span data-stu-id="40d4a-134">Or proposal 2, by inheriting from hello `AEUserNotificationHandler` class</span></span>

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
> <span data-ttu-id="40d4a-135">Vous pouvez déterminer si une notification d’Engagement ou non, en passant son `userInfo` dictionnaire toohello Agent `isEngagementPushPayload:` méthode de classe.</span><span class="sxs-lookup"><span data-stu-id="40d4a-135">You can determine whether a notification comes from Engagement or not by passing its `userInfo` dictionary toohello Agent `isEngagementPushPayload:` class method.</span></span>

<span data-ttu-id="40d4a-136">Vérifiez que hello `UNUserNotificationCenter` délégué de l’objet a la valeur délégué tooyour dans soit hello `application:willFinishLaunchingWithOptions:` ou hello `application:didFinishLaunchingWithOptions:` méthode du délégué de votre application.</span><span class="sxs-lookup"><span data-stu-id="40d4a-136">Make sure that hello `UNUserNotificationCenter` object's delegate is set tooyour delegate within either hello `application:willFinishLaunchingWithOptions:` or hello `application:didFinishLaunchingWithOptions:` method of your application delegate.</span></span>
<span data-ttu-id="40d4a-137">Par exemple, si vous avez implémenté hello ci-dessus proposition 1 :</span><span class="sxs-lookup"><span data-stu-id="40d4a-137">For instance, if you implemented hello above proposal 1:</span></span>

      - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
        // Any other code
  
        [UNUserNotificationCenter currentNotificationCenter].delegate = self;
        return YES;
      }

## <a name="from-200-too300"></a><span data-ttu-id="40d4a-138">À partir de 2.0.0 too3.0.0</span><span class="sxs-lookup"><span data-stu-id="40d4a-138">From 2.0.0 too3.0.0</span></span>
<span data-ttu-id="40d4a-139">Prise en charge d’iOS 4.X abandonnée.</span><span class="sxs-lookup"><span data-stu-id="40d4a-139">Dropped support for iOS 4.X.</span></span> <span data-ttu-id="40d4a-140">À partir de cette cible de déploiement hello version de votre application doit être au moins iOS 6.</span><span class="sxs-lookup"><span data-stu-id="40d4a-140">Starting from this version hello deployment target of your application must be at least iOS 6.</span></span>

<span data-ttu-id="40d4a-141">Si vous utilisez la portée de votre application, vous devez ajouter `remote-notification` valeur toohello `UIBackgroundModes` tableau dans votre fichier Info.plist dans les notifications de commande tooreceive à distance.</span><span class="sxs-lookup"><span data-stu-id="40d4a-141">If you are using Reach in your application, you must add `remote-notification` value toohello `UIBackgroundModes` array in your Info.plist file in order tooreceive remote notifications.</span></span>

<span data-ttu-id="40d4a-142">Hello méthode `application:didReceiveRemoteNotification:` doit toobe remplacé par `application:didReceiveRemoteNotification:fetchCompletionHandler:` dans votre délégué de l’application.</span><span class="sxs-lookup"><span data-stu-id="40d4a-142">hello method `application:didReceiveRemoteNotification:` needs toobe replaced by `application:didReceiveRemoteNotification:fetchCompletionHandler:` in your application delegate.</span></span>

<span data-ttu-id="40d4a-143">« AEPushDelegate.h » est déconseillée interface et que vous devez tooremove toutes les références.</span><span class="sxs-lookup"><span data-stu-id="40d4a-143">"AEPushDelegate.h" is deprecated interface and you need tooremove all references.</span></span> <span data-ttu-id="40d4a-144">Cela inclut la suppression `[[EngagementAgent shared] setPushDelegate:self]` et hello déléguer des méthodes à partir de votre délégué de l’application :</span><span class="sxs-lookup"><span data-stu-id="40d4a-144">This includes removing `[[EngagementAgent shared] setPushDelegate:self]` and hello delegate methods from your application delegate:</span></span>

    -(void)willRetrieveLaunchMessage;
    -(void)didFailToRetrieveLaunchMessage;
    -(void)didReceiveLaunchMessage:(AEPushMessage*)launchMessage;

## <a name="from-1160-too200"></a><span data-ttu-id="40d4a-145">À partir de 1.16.0 too2.0.0</span><span class="sxs-lookup"><span data-stu-id="40d4a-145">From 1.16.0 too2.0.0</span></span>
<span data-ttu-id="40d4a-146">Hello suivante décrit comment toomigrate une intégration du Kit de développement logiciel de hello Capptain service offert par Capptain SAS dans une application grâce à Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="40d4a-146">hello following describes how toomigrate an SDK integration from hello Capptain service offered by Capptain SAS into an app powered by Azure Mobile Engagement.</span></span>
<span data-ttu-id="40d4a-147">Si vous effectuez une migration à partir d’une version antérieure, consultez hello Capptain site web toomigrate too1.16 tout d’abord, puis appliquer hello suivant la procédure.</span><span class="sxs-lookup"><span data-stu-id="40d4a-147">If you are migrating from an earlier version, please consult hello Capptain web site toomigrate too1.16 first then apply hello following procedure.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="40d4a-148">Capptain et Mobile Engagement sont hello pas les mêmes services et procédure hello fourni ci-dessous uniquement met en évidence comment toomigrate hello application cliente.</span><span class="sxs-lookup"><span data-stu-id="40d4a-148">Capptain and Mobile Engagement are not hello same services and hello procedure given below only highlights how toomigrate hello client app.</span></span> <span data-ttu-id="40d4a-149">Migration hello SDK dans l’application hello ne fait pas migrer vos données des hello Capptain toohello Mobile Engagement serveurs</span><span class="sxs-lookup"><span data-stu-id="40d4a-149">Migrating hello SDK in hello app will NOT migrate your data from hello Capptain servers toohello Mobile Engagement servers</span></span>
> 
> 

### <a name="agent"></a><span data-ttu-id="40d4a-150">Agent</span><span class="sxs-lookup"><span data-stu-id="40d4a-150">Agent</span></span>
<span data-ttu-id="40d4a-151">Hello méthode `registerApp:` a été remplacée par la nouvelle méthode de hello `init:`.</span><span class="sxs-lookup"><span data-stu-id="40d4a-151">hello method `registerApp:` has been replaced by hello new method `init:`.</span></span> <span data-ttu-id="40d4a-152">Votre délégué d'application doit être mis à jour en conséquence et utiliser la chaîne de connexion :</span><span class="sxs-lookup"><span data-stu-id="40d4a-152">Your application delegate must be updated accordingly and use connection string:</span></span>

            - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
            {
              [...]
              [EngagementAgent init:@"YOUR_CONNECTION_STRING"];
              [...]
            }

<span data-ttu-id="40d4a-153">Suivi de SmartAd a été supprimé à partir du Kit de développement logiciel vous devez tooremove toutes les instances de `AETrackModule` classe</span><span class="sxs-lookup"><span data-stu-id="40d4a-153">SmartAd tracking has been removed from SDK you just have tooremove all instances of `AETrackModule` class</span></span>

### <a name="class-name-changes"></a><span data-ttu-id="40d4a-154">Modifications de nom de classe</span><span class="sxs-lookup"><span data-stu-id="40d4a-154">Class Name Changes</span></span>
<span data-ttu-id="40d4a-155">Dans le cadre de hello repositionnement, il existe deux classe/des noms de fichiers qui doivent toobe modifié.</span><span class="sxs-lookup"><span data-stu-id="40d4a-155">As part of hello rebranding, there are couple of class/file names that need toobe changed.</span></span>

<span data-ttu-id="40d4a-156">Toutes les classes avec le préfixe « CP » sont renommées avec le préfixe « AE ».</span><span class="sxs-lookup"><span data-stu-id="40d4a-156">All classes prefixed with "CP" are renamed with "AE" prefix.</span></span>

<span data-ttu-id="40d4a-157">Exemple :</span><span class="sxs-lookup"><span data-stu-id="40d4a-157">Example:</span></span>

* <span data-ttu-id="40d4a-158">`CPModule.h`est renommé trop`AEModule.h`.</span><span class="sxs-lookup"><span data-stu-id="40d4a-158">`CPModule.h` is renamed too`AEModule.h`.</span></span>

<span data-ttu-id="40d4a-159">Toutes les classes avec le préfixe « Capptain » sont renommées avec le préfixe « Engagement ».</span><span class="sxs-lookup"><span data-stu-id="40d4a-159">All classes prefixed with "Capptain" are renamed with "Engagement" prefix.</span></span>

<span data-ttu-id="40d4a-160">Exemples :</span><span class="sxs-lookup"><span data-stu-id="40d4a-160">Examples:</span></span>

* <span data-ttu-id="40d4a-161">Hello classe `CapptainAgent` est renommé trop`EngagementAgent`.</span><span class="sxs-lookup"><span data-stu-id="40d4a-161">hello class `CapptainAgent` is renamed too`EngagementAgent`.</span></span>
* <span data-ttu-id="40d4a-162">Hello classe `CapptainTableViewController` est renommé trop`EngagementTableViewController`.</span><span class="sxs-lookup"><span data-stu-id="40d4a-162">hello class `CapptainTableViewController` is renamed too`EngagementTableViewController`.</span></span>
* <span data-ttu-id="40d4a-163">Hello classe `CapptainUtils` est renommé trop`EngagementUtils`.</span><span class="sxs-lookup"><span data-stu-id="40d4a-163">hello class `CapptainUtils` is renamed too`EngagementUtils`.</span></span>
* <span data-ttu-id="40d4a-164">Hello classe `CapptainViewController` est renommé trop`EngagementViewController`.</span><span class="sxs-lookup"><span data-stu-id="40d4a-164">hello class `CapptainViewController` is renamed too`EngagementViewController`.</span></span>

