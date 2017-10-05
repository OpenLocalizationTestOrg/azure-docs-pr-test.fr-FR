---
title: "Procédure de mise à niveau du SDK iOS Azure Mobile Engagement | Microsoft Docs"
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
ms.openlocfilehash: 37c7f133d079186f828d58cabce0d2a259efd085
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="upgrade-procedures"></a><span data-ttu-id="d045f-103">Procédures de mise à niveau</span><span class="sxs-lookup"><span data-stu-id="d045f-103">Upgrade procedures</span></span>
<span data-ttu-id="d045f-104">Si vous avez déjà intégré une version antérieure d'Engagement dans votre application, vous devez prendre en compte les points suivants lors de la mise à niveau du Kit de développement logiciel.</span><span class="sxs-lookup"><span data-stu-id="d045f-104">If you already have integrated an older version of Engagement into your application, you have to consider the following points when upgrading the SDK.</span></span>

<span data-ttu-id="d045f-105">Pour chaque nouvelle version du Kit de développement logiciel, vous devez d'abord remplacer (supprimer et importer de nouveau dans xcode) les dossiers EngagementSDK et EngagementReach.</span><span class="sxs-lookup"><span data-stu-id="d045f-105">For each new version of the SDK you must first replace (remove and re-import in xcode) the EngagementSDK and EngagementReach folders.</span></span>

## <a name="from-300-to-400"></a><span data-ttu-id="d045f-106">Migration de 3.0.0 vers 4.0.0</span><span class="sxs-lookup"><span data-stu-id="d045f-106">From 3.0.0 to 4.0.0</span></span>
### <a name="xcode-8"></a><span data-ttu-id="d045f-107">XCode 8</span><span class="sxs-lookup"><span data-stu-id="d045f-107">XCode 8</span></span>
<span data-ttu-id="d045f-108">XCode 8 est obligatoire à partir de la version 4.0.0 du SDK.</span><span class="sxs-lookup"><span data-stu-id="d045f-108">XCode 8 is mandatory starting from version 4.0.0 of the SDK.</span></span>

> [!NOTE]
> <span data-ttu-id="d045f-109">Si vous dépendez vraiment de XCode 7, vous pouvez utiliser [iOS SDK Engagement v3.2.4](https://aka.ms/r6oouh).</span><span class="sxs-lookup"><span data-stu-id="d045f-109">If you really depend on XCode 7 then you may use the [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh).</span></span> <span data-ttu-id="d045f-110">Il existe un bogue connu concernant le module Reach de cette version précédente quand elle est exécutée sur des appareils iOS 10 : les notifications système ne sont pas activées.</span><span class="sxs-lookup"><span data-stu-id="d045f-110">There is a known bug on the reach module of this previous version while running on iOS 10 devices:  system notifications are not actioned.</span></span> <span data-ttu-id="d045f-111">Pour corriger ce problème, vous devez implémenter l’API déconseillée `application:didReceiveRemoteNotification:` dans votre délégué d’application comme suit :</span><span class="sxs-lookup"><span data-stu-id="d045f-111">To fix this you will have to implement the deprecated API `application:didReceiveRemoteNotification:` in your app delegate as follows:</span></span>
> 
> 

    - (void)application:(UIApplication*)application
    didReceiveRemoteNotification:(NSDictionary*)userInfo
    {
        [[EngagementAgent shared] applicationDidReceiveRemoteNotification:userInfo fetchCompletionHandler:nil];
    }

> [!IMPORTANT]
> <span data-ttu-id="d045f-112">**Nous ne recommandons pas cette solution de contournement** : ce comportement peut changer dans une prochaine mise à niveau (même mineure) de la version iOS car cette API iOS est déconseillée.</span><span class="sxs-lookup"><span data-stu-id="d045f-112">**We do not recommend this workaround** as this behavior can change in any upcoming (even minor) iOS version upgrade because this iOS API is deprecated.</span></span> <span data-ttu-id="d045f-113">Vous devriez passer à XCode 8 dès que possible.</span><span class="sxs-lookup"><span data-stu-id="d045f-113">You should switch to XCode 8 as soon as possible.</span></span>
> 
> 

### <a name="usernotifications-framework"></a><span data-ttu-id="d045f-114">Infrastructure UserNotifications</span><span class="sxs-lookup"><span data-stu-id="d045f-114">UserNotifications framework</span></span>
<span data-ttu-id="d045f-115">Vous devez ajouter l’infrastructure `UserNotifications` à votre onglet Build Phases.</span><span class="sxs-lookup"><span data-stu-id="d045f-115">You need to add the `UserNotifications` framework in your Build Phases.</span></span>

<span data-ttu-id="d045f-116">Dans l'Explorateur de projets, ouvrez le volet de votre projet et sélectionnez la cible appropriée.</span><span class="sxs-lookup"><span data-stu-id="d045f-116">in the project explorer, open your project pane and select the correct target.</span></span> <span data-ttu-id="d045f-117">Ouvrez ensuite l’onglet **« Build phases »** et, dans le menu **« Link Binary With Libraries »**, ajoutez l’infrastructure `UserNotifications.framework` - définissez le lien comme étant `Optional`</span><span class="sxs-lookup"><span data-stu-id="d045f-117">Then, open the **"Build phases"** tab and in the **"Link Binary With Libraries"** menu, add framework `UserNotifications.framework` - set the link as `Optional`</span></span>

### <a name="application-push-capability"></a><span data-ttu-id="d045f-118">Fonctionnalité push de l’application</span><span class="sxs-lookup"><span data-stu-id="d045f-118">Application push capability</span></span>
<span data-ttu-id="d045f-119">XCode 8 peut réinitialiser la fonctionnalité push de votre application : vérifiez ce point dans l’onglet `capability` de votre cible sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="d045f-119">XCode 8 may reset your app push capability, please double check it in the `capability` tab of your selected target.</span></span>

### <a name="add-the-new-ios-10-notification-registration-code"></a><span data-ttu-id="d045f-120">Ajoutez le nouveau code d’inscription aux notifications iOS 10</span><span class="sxs-lookup"><span data-stu-id="d045f-120">Add the new iOS 10 notification registration code</span></span>
<span data-ttu-id="d045f-121">L’extrait de code plus ancien permettant d’inscrire l’application aux notifications fonctionne toujours, mais utilise des API déconseillées avec IOS 10.</span><span class="sxs-lookup"><span data-stu-id="d045f-121">The older code snippet to register the app to notifications still works but is using deprecated APIs while running on iOS 10.</span></span>

<span data-ttu-id="d045f-122">Importez l’infrastructure de `User Notification` :</span><span class="sxs-lookup"><span data-stu-id="d045f-122">Import the `User Notification` framework:</span></span>

        #import <UserNotifications/UserNotifications.h> 

<span data-ttu-id="d045f-123">Dans la méthode `application:didFinishLaunchingWithOptions` de votre délégué d’application remplacez :</span><span class="sxs-lookup"><span data-stu-id="d045f-123">In your application delegate `application:didFinishLaunchingWithOptions` method replace:</span></span>

    if ([application respondsToSelector:@selector(registerUserNotificationSettings:)]) {
        [application registerUserNotificationSettings:[UIUserNotificationSettings settingsForTypes:(UIUserNotificationTypeBadge | UIUserNotificationTypeSound | UIUserNotificationTypeAlert) categories:nil]];
        [application registerForRemoteNotifications];
    }
    else {

        [application registerForRemoteNotificationTypes:(UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound | UIRemoteNotificationTypeAlert)];
    }

<span data-ttu-id="d045f-124">par :</span><span class="sxs-lookup"><span data-stu-id="d045f-124">by :</span></span>

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

### <a name="resolve-unusernotificationcenter-delegate-conflicts"></a><span data-ttu-id="d045f-125">Résoudre les conflits de délégués UNUserNotificationCenter</span><span class="sxs-lookup"><span data-stu-id="d045f-125">Resolve UNUserNotificationCenter delegate conflicts</span></span>

<span data-ttu-id="d045f-126">*Si, ni votre application ni l’une des bibliothèques tierces n’implémente un `UNUserNotificationCenterDelegate`, vous pouvez ignorer cette partie.*</span><span class="sxs-lookup"><span data-stu-id="d045f-126">*If neither your application or one of your third party libraries implements a `UNUserNotificationCenterDelegate` then you can skip this part.*</span></span>

<span data-ttu-id="d045f-127">Un délégué `UNUserNotificationCenter` est utilisé par le Kit de développement logiciel (SDK) pour surveiller le cycle de vie des notifications Engagement sur les appareils iOS 10 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="d045f-127">A `UNUserNotificationCenter` delegate is used by the SDK to monitor the life cycle of Engagement notifications on devices running on iOS 10 or greater.</span></span> <span data-ttu-id="d045f-128">Le Kit de développement logiciel (SDK) a sa propre implémentation du protocole `UNUserNotificationCenterDelegate`, mais il ne peut y avoir qu’un seul délégué `UNUserNotificationCenter` par application.</span><span class="sxs-lookup"><span data-stu-id="d045f-128">The SDK has its own implementation of the `UNUserNotificationCenterDelegate` protocol but there can be only one `UNUserNotificationCenter` delegate per application.</span></span> <span data-ttu-id="d045f-129">Tout autre délégué ajouté à l’objet `UNUserNotificationCenter` est en conflit avec celui d’Engagement.</span><span class="sxs-lookup"><span data-stu-id="d045f-129">Any other delegate added to the `UNUserNotificationCenter` object will conflict with the Engagement one.</span></span> <span data-ttu-id="d045f-130">Si le Kit de développement logiciel (SDK) détecte votre délégué ou un délégué tiers, il n’utilisera pas sa propre implémentation pour vous permettre de résoudre les conflits.</span><span class="sxs-lookup"><span data-stu-id="d045f-130">If the SDK detects your or any other third party's delegate then it will not use its own implementation to give you a chance to resolve the conflicts.</span></span> <span data-ttu-id="d045f-131">Vous devrez ajouter la logique d’Engagement à votre propre délégué afin de résoudre les conflits.</span><span class="sxs-lookup"><span data-stu-id="d045f-131">You will have to add the Engagement logic to your own delegate in order to resolve the conflicts.</span></span>

<span data-ttu-id="d045f-132">Il existe deux moyens de parvenir à cet objectif.</span><span class="sxs-lookup"><span data-stu-id="d045f-132">There are two ways to achieve this.</span></span>

<span data-ttu-id="d045f-133">1re méthode : en transférant les appels de votre délégué au kit de développement logiciel (SDK).</span><span class="sxs-lookup"><span data-stu-id="d045f-133">Proposal 1, simply by forwarding your delegate calls to the SDK:</span></span>

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

<span data-ttu-id="d045f-134">2e méthode : en héritant de la classe `AEUserNotificationHandler`</span><span class="sxs-lookup"><span data-stu-id="d045f-134">Or proposal 2, by inheriting from the `AEUserNotificationHandler` class</span></span>

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
> <span data-ttu-id="d045f-135">Vous pouvez déterminer si une notification provient ou non d’Engagement en passant son dictionnaire `userInfo` à la méthode de classe `isEngagementPushPayload:` de l’agent.</span><span class="sxs-lookup"><span data-stu-id="d045f-135">You can determine whether a notification comes from Engagement or not by passing its `userInfo` dictionary to the Agent `isEngagementPushPayload:` class method.</span></span>

<span data-ttu-id="d045f-136">Assurez-vous que le délégué de l’objet `UNUserNotificationCenter` est paramétré en fonction de votre délégué, grâce à la méthode `application:willFinishLaunchingWithOptions:` ou `application:didFinishLaunchingWithOptions:` de votre délégué d’application.</span><span class="sxs-lookup"><span data-stu-id="d045f-136">Make sure that the `UNUserNotificationCenter` object's delegate is set to your delegate within either the `application:willFinishLaunchingWithOptions:` or the `application:didFinishLaunchingWithOptions:` method of your application delegate.</span></span>
<span data-ttu-id="d045f-137">Par exemple, si vous avez implémenté la méthode 1 ci-dessus :</span><span class="sxs-lookup"><span data-stu-id="d045f-137">For instance, if you implemented the above proposal 1:</span></span>

      - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
        // Any other code
  
        [UNUserNotificationCenter currentNotificationCenter].delegate = self;
        return YES;
      }

## <a name="from-200-to-300"></a><span data-ttu-id="d045f-138">Migration de 2.0.0 vers 3.0.0</span><span class="sxs-lookup"><span data-stu-id="d045f-138">From 2.0.0 to 3.0.0</span></span>
<span data-ttu-id="d045f-139">Prise en charge d’iOS 4.X abandonnée.</span><span class="sxs-lookup"><span data-stu-id="d045f-139">Dropped support for iOS 4.X.</span></span> <span data-ttu-id="d045f-140">À partir de cette version, la cible de déploiement de votre application doit être au moins iOS 6.</span><span class="sxs-lookup"><span data-stu-id="d045f-140">Starting from this version the deployment target of your application must be at least iOS 6.</span></span>

<span data-ttu-id="d045f-141">Si vous utilisez Reach dans votre application, vous devez ajouter la valeur `remote-notification` au tableau `UIBackgroundModes` dans votre fichier Info.plist pour recevoir des notifications à distance.</span><span class="sxs-lookup"><span data-stu-id="d045f-141">If you are using Reach in your application, you must add `remote-notification` value to the `UIBackgroundModes` array in your Info.plist file in order to receive remote notifications.</span></span>

<span data-ttu-id="d045f-142">La méthode `application:didReceiveRemoteNotification:` doit être remplacée par `application:didReceiveRemoteNotification:fetchCompletionHandler:` dans votre délégué d’application.</span><span class="sxs-lookup"><span data-stu-id="d045f-142">The method `application:didReceiveRemoteNotification:` needs to be replaced by `application:didReceiveRemoteNotification:fetchCompletionHandler:` in your application delegate.</span></span>

<span data-ttu-id="d045f-143">« AEPushDelegate.h » est une interface déconseillée et vous devez supprimer toutes les références.</span><span class="sxs-lookup"><span data-stu-id="d045f-143">"AEPushDelegate.h" is deprecated interface and you need to remove all references.</span></span> <span data-ttu-id="d045f-144">Cela inclut notamment la suppression `[[EngagementAgent shared] setPushDelegate:self]` et les méthodes de délégation depuis votre délégué d’application :</span><span class="sxs-lookup"><span data-stu-id="d045f-144">This includes removing `[[EngagementAgent shared] setPushDelegate:self]` and the delegate methods from your application delegate:</span></span>

    -(void)willRetrieveLaunchMessage;
    -(void)didFailToRetrieveLaunchMessage;
    -(void)didReceiveLaunchMessage:(AEPushMessage*)launchMessage;

## <a name="from-1160-to-200"></a><span data-ttu-id="d045f-145">De 1.16.0 à 2.0.0</span><span class="sxs-lookup"><span data-stu-id="d045f-145">From 1.16.0 to 2.0.0</span></span>
<span data-ttu-id="d045f-146">La section qui suit décrit comment migrer une intégration du SDK à partir du service Capptain offert par Capptain SAS dans une application reposant sur Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="d045f-146">The following describes how to migrate an SDK integration from the Capptain service offered by Capptain SAS into an app powered by Azure Mobile Engagement.</span></span>
<span data-ttu-id="d045f-147">Si vous effectuez une migration depuis une version antérieure, veuillez d’abord consulter le site web Capptain pour effectuer une migration vers la version 1.16, puis appliquer la procédure suivante.</span><span class="sxs-lookup"><span data-stu-id="d045f-147">If you are migrating from an earlier version, please consult the Capptain web site to migrate to 1.16 first then apply the following procedure.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d045f-148">Capptain et Engagement Mobile ne sont pas les mêmes services et la procédure décrite ci-dessous explique uniquement comment migrer l'application cliente.</span><span class="sxs-lookup"><span data-stu-id="d045f-148">Capptain and Mobile Engagement are not the same services and the procedure given below only highlights how to migrate the client app.</span></span> <span data-ttu-id="d045f-149">La migration du SDK dans l'application ne migre PAS vos données des serveurs Capptain vers les serveurs Engagement Mobile.</span><span class="sxs-lookup"><span data-stu-id="d045f-149">Migrating the SDK in the app will NOT migrate your data from the Capptain servers to the Mobile Engagement servers</span></span>
> 
> 

### <a name="agent"></a><span data-ttu-id="d045f-150">Agent</span><span class="sxs-lookup"><span data-stu-id="d045f-150">Agent</span></span>
<span data-ttu-id="d045f-151">La méthode `registerApp:` a été remplacée par la nouvelle méthode `init:`.</span><span class="sxs-lookup"><span data-stu-id="d045f-151">The method `registerApp:` has been replaced by the new method `init:`.</span></span> <span data-ttu-id="d045f-152">Votre délégué d'application doit être mis à jour en conséquence et utiliser la chaîne de connexion :</span><span class="sxs-lookup"><span data-stu-id="d045f-152">Your application delegate must be updated accordingly and use connection string:</span></span>

            - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
            {
              [...]
              [EngagementAgent init:@"YOUR_CONNECTION_STRING"];
              [...]
            }

<span data-ttu-id="d045f-153">Le suivi SmartAd a été supprimé du Kit de développement logiciel (SDK). Vous devez seulement supprimer toutes les instances de la classe `AETrackModule`</span><span class="sxs-lookup"><span data-stu-id="d045f-153">SmartAd tracking has been removed from SDK you just have to remove all instances of `AETrackModule` class</span></span>

### <a name="class-name-changes"></a><span data-ttu-id="d045f-154">Modifications de nom de classe</span><span class="sxs-lookup"><span data-stu-id="d045f-154">Class Name Changes</span></span>
<span data-ttu-id="d045f-155">Dans le cadre du repositionnement, quelques classes/noms de fichiers doivent être modifiés.</span><span class="sxs-lookup"><span data-stu-id="d045f-155">As part of the rebranding, there are couple of class/file names that need to be changed.</span></span>

<span data-ttu-id="d045f-156">Toutes les classes avec le préfixe « CP » sont renommées avec le préfixe « AE ».</span><span class="sxs-lookup"><span data-stu-id="d045f-156">All classes prefixed with "CP" are renamed with "AE" prefix.</span></span>

<span data-ttu-id="d045f-157">Exemple :</span><span class="sxs-lookup"><span data-stu-id="d045f-157">Example:</span></span>

* <span data-ttu-id="d045f-158">`CPModule.h` est renommé `AEModule.h`.</span><span class="sxs-lookup"><span data-stu-id="d045f-158">`CPModule.h` is renamed to `AEModule.h`.</span></span>

<span data-ttu-id="d045f-159">Toutes les classes avec le préfixe « Capptain » sont renommées avec le préfixe « Engagement ».</span><span class="sxs-lookup"><span data-stu-id="d045f-159">All classes prefixed with "Capptain" are renamed with "Engagement" prefix.</span></span>

<span data-ttu-id="d045f-160">Exemples :</span><span class="sxs-lookup"><span data-stu-id="d045f-160">Examples:</span></span>

* <span data-ttu-id="d045f-161">La classe `CapptainAgent` est renommée `EngagementAgent`.</span><span class="sxs-lookup"><span data-stu-id="d045f-161">The class `CapptainAgent` is renamed to `EngagementAgent`.</span></span>
* <span data-ttu-id="d045f-162">La classe `CapptainTableViewController` est renommée `EngagementTableViewController`.</span><span class="sxs-lookup"><span data-stu-id="d045f-162">The class `CapptainTableViewController` is renamed to `EngagementTableViewController`.</span></span>
* <span data-ttu-id="d045f-163">La classe `CapptainUtils` est renommée `EngagementUtils`.</span><span class="sxs-lookup"><span data-stu-id="d045f-163">The class `CapptainUtils` is renamed to `EngagementUtils`.</span></span>
* <span data-ttu-id="d045f-164">La classe `CapptainViewController` est renommée `EngagementViewController`.</span><span class="sxs-lookup"><span data-stu-id="d045f-164">The class `CapptainViewController` is renamed to `EngagementViewController`.</span></span>

