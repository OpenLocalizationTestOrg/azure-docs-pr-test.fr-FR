---
title: "Intégration du SDK iOS Azure Mobile Engagement | Microsoft Docs"
description: "Dernières mises à jour et procédures du Kit de développement logiciel (SDK) iOS pour Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 947ea44b-00c1-450f-9a3b-74437954dc56
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 07/17/2017
ms.author: piyushjo
ms.openlocfilehash: 01fdbb43c21ac6932e8462f4a6507fc63e50542d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-integrate-engagement-on-ios"></a><span data-ttu-id="46b20-103">Intégration d'Engagement sur iOS</span><span class="sxs-lookup"><span data-stu-id="46b20-103">How to Integrate Engagement on iOS</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="46b20-104">Windows Universal</span><span class="sxs-lookup"><span data-stu-id="46b20-104">Windows Universal</span></span>](mobile-engagement-windows-store-integrate-engagement.md)
> * [<span data-ttu-id="46b20-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="46b20-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md)
> * [<span data-ttu-id="46b20-106">iOS</span><span class="sxs-lookup"><span data-stu-id="46b20-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md)
> * [<span data-ttu-id="46b20-107">Android</span><span class="sxs-lookup"><span data-stu-id="46b20-107">Android</span></span>](mobile-engagement-android-integrate-engagement.md)
>
>

<span data-ttu-id="46b20-108">Cette procédure décrit la méthode la plus simple pour activer les fonctions d'analyse et de contrôle d'Engagement dans votre application iOS.</span><span class="sxs-lookup"><span data-stu-id="46b20-108">This procedure describes the simplest way to activate Engagement's Analytics and Monitoring functions in your iOS application.</span></span>

<span data-ttu-id="46b20-109">Le SDK Engagement requiert iOS 7 ou versions ultérieures et Xcode 8 ou versions ultérieures : la cible de déploiement de votre application doit être au moins iOS 7.</span><span class="sxs-lookup"><span data-stu-id="46b20-109">The Engagement SDK requires iOS7+ and Xcode 8+: the deployment target of your application must be at least iOS 7.</span></span>

> [!NOTE]
> <span data-ttu-id="46b20-110">Si vous dépendez vraiment de XCode 7, vous pouvez utiliser [iOS SDK Engagement v3.2.4](https://aka.ms/r6oouh).</span><span class="sxs-lookup"><span data-stu-id="46b20-110">If you really depend on XCode 7 then you may use the [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh).</span></span> <span data-ttu-id="46b20-111">Il existe un bogue connu concernant le module Reach de cette version précédente lorsqu’elle est exécutée sur des appareils iOS 10, consultez [l’intégration du module Reach](mobile-engagement-ios-integrate-engagement-reach.md) pour plus de détails.</span><span class="sxs-lookup"><span data-stu-id="46b20-111">There is a known bug on the Reach module of this previous version while running on iOS 10 devices see [the reach module integration](mobile-engagement-ios-integrate-engagement-reach.md) for more details.</span></span> <span data-ttu-id="46b20-112">Si vous choisissez d’utiliser le Kit de développement logiciel v3.2.4, ignorez l’importation de `UserNotifications.framework` à l’étape suivante.</span><span class="sxs-lookup"><span data-stu-id="46b20-112">If you choose to use the SDK v3.2.4 then just skip the `UserNotifications.framework` import in the next step.</span></span>
>
>

<span data-ttu-id="46b20-113">Les étapes suivantes permettent d'activer la génération des journaux nécessaires pour calculer toutes les statistiques concernant les utilisateurs, les sessions, les activités, les incidents et les informations techniques.</span><span class="sxs-lookup"><span data-stu-id="46b20-113">The following steps are enough to activate the report of logs needed to compute all statistics regarding Users, Sessions, Activities, Crashes and Technicals.</span></span> <span data-ttu-id="46b20-114">Le rapport des journaux nécessaire pour calculer d’autres statistiques telles que les événements, les erreurs et les tâches, doit être généré manuellement à l’aide de l’API Engagement (consultez la rubrique [Utilisation de l’API de balisage Mobile Engagement avancée dans vos applications iOS](mobile-engagement-ios-use-engagement-api.md) étant donné que ces statistiques dépendent de l’application.</span><span class="sxs-lookup"><span data-stu-id="46b20-114">The report of logs needed to compute other statistics like Events, Errors and Jobs must be done manually using the Engagement API  (see [How to use the advanced Mobile Engagement tagging API in your iOS app](mobile-engagement-ios-use-engagement-api.md) since these statistics are application dependent.</span></span>

## <a name="embed-the-engagement-sdk-into-your-ios-project"></a><span data-ttu-id="46b20-115">Incorporer le SDK Engagement à votre projet iOS</span><span class="sxs-lookup"><span data-stu-id="46b20-115">Embed the Engagement SDK into your iOS project</span></span>
* <span data-ttu-id="46b20-116">Télécharger le kit de développement logiciel (SDK) iOS [ici](http://aka.ms/qk2rnj).</span><span class="sxs-lookup"><span data-stu-id="46b20-116">Download the iOS SDK from [here](http://aka.ms/qk2rnj).</span></span>
* <span data-ttu-id="46b20-117">Ajoutez le SDK Engagement à votre projet iOS : dans Xcode, cliquez avec le bouton droit sur votre projet, puis sélectionnez **Ajouter des fichiers à...** et choisissez le dossier `EngagementSDK`.</span><span class="sxs-lookup"><span data-stu-id="46b20-117">Add the Engagement SDK to your iOS project: in Xcode, right click on your project and select **"Add files to ..."** and choose the `EngagementSDK` folder.</span></span>
* <span data-ttu-id="46b20-118">Engagement nécessite des infrastructures supplémentaires pour fonctionner : dans l'Explorateur de projets, ouvrez le volet de votre projet et sélectionnez la cible appropriée.</span><span class="sxs-lookup"><span data-stu-id="46b20-118">Engagement requires additional frameworks to work: in the project explorer, open your project pane and select the correct target.</span></span> <span data-ttu-id="46b20-119">Ouvrez ensuite l’onglet **«Build phases »** (Générer des phases) et, dans le menu **« Link Binary With Libraries »** (Liaisons binaires à des bibliothèques), ajoutez ces infrastructures :</span><span class="sxs-lookup"><span data-stu-id="46b20-119">Then, open the **"Build phases"** tab and in the **"Link Binary With Libraries"** menu, add these frameworks:</span></span>

  * <span data-ttu-id="46b20-120">`UserNotifications.framework` - définissez le lien comme `Optional`</span><span class="sxs-lookup"><span data-stu-id="46b20-120">`UserNotifications.framework` - set the link as `Optional`</span></span>
  * <span data-ttu-id="46b20-121">`AdSupport.framework` - définissez le lien comme `Optional`</span><span class="sxs-lookup"><span data-stu-id="46b20-121">`AdSupport.framework` - set the link as `Optional`</span></span>
  * `SystemConfiguration.framework`
  * `CoreTelephony.framework`
  * `CFNetwork.framework`
  * `CoreLocation.framework`
  * `libxml2.dylib`

> [!NOTE]
> <span data-ttu-id="46b20-122">L'infrastructure AdSupport peut être supprimée.</span><span class="sxs-lookup"><span data-stu-id="46b20-122">The AdSupport framework can be removed.</span></span> <span data-ttu-id="46b20-123">Engagement en a besoin pour collecter l'IDFA.</span><span class="sxs-lookup"><span data-stu-id="46b20-123">Engagement needs this framework to collect the IDFA.</span></span> <span data-ttu-id="46b20-124">Toutefois, il est possible de désactiver la collection de l’IDFA \<ios-sdk-engagement-idfa\> pour se conformer à la nouvelle politique d’Apple concernant cet ID.</span><span class="sxs-lookup"><span data-stu-id="46b20-124">However, IDFA collection can be disabled \<ios-sdk-engagement-idfa\> to comply with the new Apple policy regarding this ID.</span></span>
>
>

## <a name="initialize-the-engagement-sdk"></a><span data-ttu-id="46b20-125">Initialiser le SDK Engagement</span><span class="sxs-lookup"><span data-stu-id="46b20-125">Initialize the Engagement SDK</span></span>
<span data-ttu-id="46b20-126">Vous devez modifier votre délégué d'application :</span><span class="sxs-lookup"><span data-stu-id="46b20-126">You need to modify your Application Delegate:</span></span>

* <span data-ttu-id="46b20-127">En haut de votre fichier d'implémentation, importez l'agent Engagement :</span><span class="sxs-lookup"><span data-stu-id="46b20-127">At the top of your implementation file, import the Engagement agent:</span></span>

      [...]
      #import "EngagementAgent.h"
* <span data-ttu-id="46b20-128">Initialisez Engagement au sein de la méthode **applicationDidFinishLaunching:** ou **application:didFinishLaunchingWithOptions:** :</span><span class="sxs-lookup"><span data-stu-id="46b20-128">Initialize Engagement inside the method '**applicationDidFinishLaunching:**' or '**application:didFinishLaunchingWithOptions:**':</span></span>

      - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
      {
        [...]
        [EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}"];
        [...]
      }

## <a name="basic-reporting"></a><span data-ttu-id="46b20-129">Génération de rapports de base</span><span class="sxs-lookup"><span data-stu-id="46b20-129">Basic reporting</span></span>
### <a name="recommended-method-overload-your-uiviewcontroller-classes"></a><span data-ttu-id="46b20-130">Méthode recommandée : surchargez vos classes `UIViewController`</span><span class="sxs-lookup"><span data-stu-id="46b20-130">Recommended method: overload your `UIViewController` classes</span></span>
<span data-ttu-id="46b20-131">Pour activer le rapport de tous les journaux requis par Engagement pour calculer les statistiques relatives aux utilisateurs, aux sessions, aux activités, aux incidents et aux informations techniques, il vous suffit de faire hériter toutes vos `UIViewController`sous-classes des classes `EngagementViewController` (même règle pour `UITableViewController` -\> `EngagementTableViewController`).</span><span class="sxs-lookup"><span data-stu-id="46b20-131">In order to activate the report of all the logs required by Engagement to compute Users, Sessions, Activities, Crashes and Technical statistics, you can simply make all your `UIViewController` sub-classes inherit from the `EngagementViewController` classes (same rule for `UITableViewController` -\> `EngagementTableViewController`).</span></span>

<span data-ttu-id="46b20-132">**Sans Engagement :**</span><span class="sxs-lookup"><span data-stu-id="46b20-132">**Without Engagement :**</span></span>

    #import <UIKit/UIKit.h>

    @interface Tab1ViewController : UIViewController<UITextFieldDelegate> {
      UITextField* myTextField1;
      UITextField* myTextField2;
    }

    @property (nonatomic, retain) IBOutlet UITextField* myTextField1;
    @property (nonatomic, retain) IBOutlet UITextField* myTextField2;

<span data-ttu-id="46b20-133">**Avec Engagement :**</span><span class="sxs-lookup"><span data-stu-id="46b20-133">**With Engagement :**</span></span>

    #import <UIKit/UIKit.h>
    #import "EngagementViewController.h"

    @interface Tab1ViewController : EngagementViewController<UITextFieldDelegate> {
      UITextField* myTextField1;
      UITextField* myTextField2;
    }

    @property (nonatomic, retain) IBOutlet UITextField* myTextField1;
    @property (nonatomic, retain) IBOutlet UITextField* myTextField2;

### <a name="alternate-method-call-startactivity-manually"></a><span data-ttu-id="46b20-134">Autre méthode : appeler `startActivity()` manuellement</span><span class="sxs-lookup"><span data-stu-id="46b20-134">Alternate method: call `startActivity()` manually</span></span>
<span data-ttu-id="46b20-135">Si vous ne pouvez pas ou ne voulez pas surcharger vos classes `UIViewController`, vous pouvez démarrer vos activités en appelant directement les méthodes de `EngagementAgent`.</span><span class="sxs-lookup"><span data-stu-id="46b20-135">If you cannot or do not want to overload your `UIViewController` classes, you can instead start your activities by calling `EngagementAgent`'s methods directly.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="46b20-136">Le Kit de développement logiciel (SDK) iOS appelle automatiquement la méthode `endActivity()` à la fermeture de l'application.</span><span class="sxs-lookup"><span data-stu-id="46b20-136">The iOS SDK automatically calls the `endActivity()` method when the application is closed.</span></span> <span data-ttu-id="46b20-137">Ainsi, il est *FORTEMENT* recommandé d’appeler la méthode `startActivity` chaque fois que l’activité de l’utilisateur change et de ne *JAMAIS* appeler la méthode `endActivity`, étant donné que l’appel de cette méthode entraîne l’arrêt de la session en cours.</span><span class="sxs-lookup"><span data-stu-id="46b20-137">Thus, it is *HIGHLY* recommended to call the `startActivity` method whenever the activity of the user change, and to *NEVER* call the `endActivity` method, since calling this method forces the current session to be ended.</span></span>
>
>

## <a name="location-reporting"></a><span data-ttu-id="46b20-138">Rapports d'emplacement</span><span class="sxs-lookup"><span data-stu-id="46b20-138">Location reporting</span></span>
<span data-ttu-id="46b20-139">Les conditions du service Apple n'autorisent pas les applications à utiliser le suivi d'emplacement à des fins statistiques uniquement.</span><span class="sxs-lookup"><span data-stu-id="46b20-139">Apple terms of service do not allow applications to use location tracking for statistics purpose only.</span></span> <span data-ttu-id="46b20-140">Par conséquent, il est recommandé d'activer les rapports d'emplacement uniquement si votre application utilise également le suivi d'emplacement pour une autre raison.</span><span class="sxs-lookup"><span data-stu-id="46b20-140">Thus, it is recommended to enable location reports only if your application also use the location tracking for another reason.</span></span>

<span data-ttu-id="46b20-141">À compter d’iOS 8, vous devez fournir une description de la façon dont votre application utilise les services d’emplacement en définissant une chaîne pour la clé [NSLocationWhenInUseUsageDescription] ou [NSLocationAlwaysUsageDescription] dans le fichier Info.plist de votre application.</span><span class="sxs-lookup"><span data-stu-id="46b20-141">Starting with iOS 8, you must provide a description for how your app uses location services by setting a string for the key [NSLocationWhenInUseUsageDescription] or [NSLocationAlwaysUsageDescription] in your app's Info.plist file.</span></span> <span data-ttu-id="46b20-142">Si vous voulez signaler l'emplacement en arrière-plan avec Engagement, ajoutez la clé NSLocationAlwaysUsageDescription.</span><span class="sxs-lookup"><span data-stu-id="46b20-142">If you want to report location in the background with Engagement, add the key NSLocationAlwaysUsageDescription.</span></span> <span data-ttu-id="46b20-143">Dans tous les autres cas, ajoutez la clé NSLocationWhenInUseUsageDescription.</span><span class="sxs-lookup"><span data-stu-id="46b20-143">In all other cases, add the key NSLocationWhenInUseUsageDescription.</span></span> <span data-ttu-id="46b20-144">NSLocationAlwaysAndWhenInUseUsageDescription et NSLocationWhenInUseUsageDescription sont nécessaires pour rapporter l’emplacement en arrière-plan sur iOS 11.</span><span class="sxs-lookup"><span data-stu-id="46b20-144">Note that you need both NSLocationAlwaysAndWhenInUseUsageDescription and NSLocationWhenInUseUsageDescription to report background location on iOS 11.</span></span>

### <a name="lazy-area-location-reporting"></a><span data-ttu-id="46b20-145">Rapports d'emplacement de zone différé</span><span class="sxs-lookup"><span data-stu-id="46b20-145">Lazy area location reporting</span></span>
<span data-ttu-id="46b20-146">Le rapport d'emplacement de zone différé permet d'indiquer le pays, la région et la localité associés aux appareils.</span><span class="sxs-lookup"><span data-stu-id="46b20-146">Lazy area location reporting allows to report the country, region and locality associated to devices.</span></span> <span data-ttu-id="46b20-147">Ce type de rapport d'emplacement utilise uniquement des emplacements réseau (basés sur l'ID cellulaire ou le Wi-Fi).</span><span class="sxs-lookup"><span data-stu-id="46b20-147">This type of location reporting only uses network locations (based on Cell ID or WIFI).</span></span> <span data-ttu-id="46b20-148">La zone de l'appareil est signalée une fois maximum par session.</span><span class="sxs-lookup"><span data-stu-id="46b20-148">The device area is reported at most once per session.</span></span> <span data-ttu-id="46b20-149">Le GPS n'est jamais utilisé, ce type de rapport d'emplacement a donc très peu d'impact (pour ne pas dire aucun) sur la batterie.</span><span class="sxs-lookup"><span data-stu-id="46b20-149">The GPS is never used, and thus this type of location report has very few (not to say no) impact on the battery.</span></span>

<span data-ttu-id="46b20-150">Les zones signalées sont utilisées pour calculer des statistiques géographiques relatives aux utilisateurs, aux sessions, aux événements et aux erreurs.</span><span class="sxs-lookup"><span data-stu-id="46b20-150">Reported areas are used to compute geographic statistics about users, sessions, events and errors.</span></span> <span data-ttu-id="46b20-151">Elles peuvent également servir de critère dans les couvertures campagne.</span><span class="sxs-lookup"><span data-stu-id="46b20-151">They can also be used as criterion in Reach campaigns.</span></span> <span data-ttu-id="46b20-152">La dernière zone connue signalée pour un appareil peut être récupérée grâce à l' [API de l'appareil].</span><span class="sxs-lookup"><span data-stu-id="46b20-152">The last known area reported for a device can be retrieved thanks to the [Device API].</span></span>

<span data-ttu-id="46b20-153">Pour activer le rapport d'emplacement de zone différé, ajoutez la ligne suivante après l'initialisation de l'agent Engagement :</span><span class="sxs-lookup"><span data-stu-id="46b20-153">To enable lazy area location reporting, add the following line after initializing the Engagement agent:</span></span>

    - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
    {
      [...]
      [[EngagementAgent shared] setLazyAreaLocationReport:YES];
      [...]
    }

### <a name="real-time-location-reporting"></a><span data-ttu-id="46b20-154">Rapports d'emplacement en temps réel</span><span class="sxs-lookup"><span data-stu-id="46b20-154">Real time location reporting</span></span>
<span data-ttu-id="46b20-155">Le rapport d'emplacement en temps réel permet de signaler la latitude et la longitude associées aux appareils.</span><span class="sxs-lookup"><span data-stu-id="46b20-155">Real time location reporting allows to report the latitude and longitude associated to devices.</span></span> <span data-ttu-id="46b20-156">Par défaut, ce type de rapport d'emplacement utilise uniquement des emplacements réseau (basés sur l'ID cellulaire ou le Wi-Fi) et le rapport n'est actif que lorsque l'application s'exécute en premier plan (c'est-à-dire pendant une session).</span><span class="sxs-lookup"><span data-stu-id="46b20-156">By default, this type of location reporting only uses network locations (based on Cell ID or WIFI), and the reporting is only active when the application runs in foreground (i.e. during a session).</span></span>

<span data-ttu-id="46b20-157">Les emplacements en temps réel ne sont *PAS* utilisés pour calculer des statistiques.</span><span class="sxs-lookup"><span data-stu-id="46b20-157">Real time locations are *NOT* used to compute statistics.</span></span> <span data-ttu-id="46b20-158">Leur seul but est de permettre l’utilisation d’un critère de géorepérage en temps réel \<portée-public-gardiennage virtuel\> dans les campagnes Reach.</span><span class="sxs-lookup"><span data-stu-id="46b20-158">Their only purpose is to allow the use of real time geo-fencing \<Reach-Audience-geofencing\> criterion in Reach campaigns.</span></span>

<span data-ttu-id="46b20-159">Pour activer le rapport d'emplacement en temps réel, ajoutez la ligne suivante après l'initialisation de l'agent Engagement :</span><span class="sxs-lookup"><span data-stu-id="46b20-159">To enable real time location reporting, add the following line after initializing the Engagement agent:</span></span>

    [[EngagementAgent shared] setRealtimeLocationReport:YES];

#### <a name="gps-based-reporting"></a><span data-ttu-id="46b20-160">Rapports GPS</span><span class="sxs-lookup"><span data-stu-id="46b20-160">GPS based reporting</span></span>
<span data-ttu-id="46b20-161">Par défaut, le rapport d'emplacement en temps réel utilise uniquement des emplacements réseau.</span><span class="sxs-lookup"><span data-stu-id="46b20-161">By default, real time location reporting only uses network based locations.</span></span> <span data-ttu-id="46b20-162">Pour activer l'utilisation des emplacements GPS (qui sont beaucoup plus précis), ajoutez ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="46b20-162">To enable the use of GPS based locations (which are far more precise), add:</span></span>

    [[EngagementAgent shared] setFineRealtimeLocationReport:YES];

#### <a name="background-reporting"></a><span data-ttu-id="46b20-163">Rapports en arrière-plan</span><span class="sxs-lookup"><span data-stu-id="46b20-163">Background reporting</span></span>
<span data-ttu-id="46b20-164">Par défaut, le rapport d'emplacement en temps réel est uniquement actif quand l'application s'exécute en premier plan (c'est-à-dire pendant une session).</span><span class="sxs-lookup"><span data-stu-id="46b20-164">By default, real time location reporting is only active when the application runs in foreground (i.e. during a session).</span></span> <span data-ttu-id="46b20-165">Pour activer la création de rapports également en arrière-plan, ajoutez ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="46b20-165">To enable the reporting also in background, add:</span></span>

    [[EngagementAgent shared] setBackgroundRealtimeLocationReport:YES withLaunchOptions:launchOptions];

> [!NOTE]
> <span data-ttu-id="46b20-166">Quand l'application s'exécute en arrière-plan, seuls les emplacements réseau sont signalés, même si vous avez activé le GPS.</span><span class="sxs-lookup"><span data-stu-id="46b20-166">When the application runs in background, only network based locations are reported, even if you enabled the GPS.</span></span>
>
>

<span data-ttu-id="46b20-167">L'implémentation de cette fonction appelle [startMonitoringSignificantLocationChanges] quand votre application passe en arrière-plan.</span><span class="sxs-lookup"><span data-stu-id="46b20-167">Implementation of this function will call [startMonitoringSignificantLocationChanges] when your application goes into the background.</span></span> <span data-ttu-id="46b20-168">N'oubliez pas que votre application sera automatiquement relancée en arrière-plan en cas de nouvel événement d'emplacement.</span><span class="sxs-lookup"><span data-stu-id="46b20-168">Be aware that it will automatically relaunch your application into the background if a new location event arrives.</span></span>

## <a name="advanced-reporting"></a><span data-ttu-id="46b20-169">Génération de rapports avancés</span><span class="sxs-lookup"><span data-stu-id="46b20-169">Advanced reporting</span></span>
<span data-ttu-id="46b20-170">Éventuellement, si vous voulez signaler des événements, des erreurs et des tâches de l'application spécifiques, vous devez utiliser l'API Engagement par le biais des méthodes de la classe `EngagementAgent` .</span><span class="sxs-lookup"><span data-stu-id="46b20-170">Optionally, if you want to report application specific events, errors and jobs, you need to use the Engagement API through the methods of the `EngagementAgent` class.</span></span> <span data-ttu-id="46b20-171">Un objet de cette classe peut être récupéré en appelant la méthode statique `[EngagementAgent shared]` .</span><span class="sxs-lookup"><span data-stu-id="46b20-171">An object of this class can be retrieved by calling the `[EngagementAgent shared]` static method.</span></span>

<span data-ttu-id="46b20-172">L'API d'Engagement permet d'utiliser toutes les fonctionnalités avancées d'Engagement et est détaillé dans la procédure d’utilisation de l'API d'Engagement sur iOS (ainsi que dans la documentation technique de la classe `EngagementAgent` ).</span><span class="sxs-lookup"><span data-stu-id="46b20-172">The Engagement API allows to use all of Engagement's advanced capabilities and is detailed in the How to Use the Engagement API on iOS (as well as in the technical documentation of the `EngagementAgent` class).</span></span>

## <a name="disable-idfa-collection"></a><span data-ttu-id="46b20-173">Désactiver la collecte de l'IDFA</span><span class="sxs-lookup"><span data-stu-id="46b20-173">Disable IDFA collection</span></span>
<span data-ttu-id="46b20-174">Par défaut, Engagement utilise l' [IDFA] pour identifier un utilisateur de manière unique.</span><span class="sxs-lookup"><span data-stu-id="46b20-174">By default, Engagement will use the [IDFA] to uniquely identify a user.</span></span> <span data-ttu-id="46b20-175">Toutefois, si vous n'utilisez pas de publicités à un autre endroit dans l'application, cette dernière peut être rejetée par le processus de vérification de la boutique d'applications.</span><span class="sxs-lookup"><span data-stu-id="46b20-175">But if you’re not using advertising elsewhere in the app, you might be rejected by the App Store review process.</span></span> <span data-ttu-id="46b20-176">La collection de l'IDFA peut être désactivée en ajoutant la macro `ENGAGEMENT_DISABLE_IDFA` du préprocesseur dans votre fichier pch (ou dans le `Build Settings` de votre application).</span><span class="sxs-lookup"><span data-stu-id="46b20-176">IDFA collection can be disabled by adding the preprocessor macro `ENGAGEMENT_DISABLE_IDFA` in your pch file (or in the `Build Settings` of your application).</span></span> <span data-ttu-id="46b20-177">De cette façon, vous garantissez qu'il n'existe aucune référence à `ASIdentifierManager`, `advertisingIdentifier` ou `isAdvertisingTrackingEnabled` dans la génération de l'application.</span><span class="sxs-lookup"><span data-stu-id="46b20-177">This will ensure that there is no references to `ASIdentifierManager`, `advertisingIdentifier` or `isAdvertisingTrackingEnabled` in the application build.</span></span>

<span data-ttu-id="46b20-178">Intégration dans le fichier **prefix.pch** :</span><span class="sxs-lookup"><span data-stu-id="46b20-178">Integration in the **prefix.pch** file:</span></span>

    #define ENGAGEMENT_DISABLE_IDFA
    ...

<span data-ttu-id="46b20-179">Vous pouvez vérifier que la collecte d'IDFA est correctement désactivée dans votre application en consultant les journaux de test d'Engagement.</span><span class="sxs-lookup"><span data-stu-id="46b20-179">You can verify that the IDFA collection is properly disabled in your application by checking the Engagement test logs.</span></span> <span data-ttu-id="46b20-180">Consultez la documentation sur les tests d’intégration \<ios-sdk-engagement-test-idfa\> pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="46b20-180">See the Integration Test\<ios-sdk-engagement-test-idfa\> documentation for further information.</span></span>

## <a name="disable-log-reporting"></a><span data-ttu-id="46b20-181">Désactiver les rapports de suivi</span><span class="sxs-lookup"><span data-stu-id="46b20-181">Disable log reporting</span></span>
### <a name="using-a-method-call"></a><span data-ttu-id="46b20-182">En appelant une méthode</span><span class="sxs-lookup"><span data-stu-id="46b20-182">Using a method call</span></span>
<span data-ttu-id="46b20-183">Si vous voulez qu'Engagement arrête d'envoyer des journaux, vous pouvez appeler la méthode suivante :</span><span class="sxs-lookup"><span data-stu-id="46b20-183">If you want Engagement to stop sending logs, you can call:</span></span>

    [[EngagementAgent shared] setEnabled:NO];

<span data-ttu-id="46b20-184">Cet appel est persistant : il utilise `NSUserDefaults` pour stocker les informations.</span><span class="sxs-lookup"><span data-stu-id="46b20-184">This call is persistent: it uses `NSUserDefaults` to store the information.</span></span>

<span data-ttu-id="46b20-185">Vous pouvez activer à nouveau la création de rapports de journaux en appelant la même fonction avec `YES`.</span><span class="sxs-lookup"><span data-stu-id="46b20-185">You can enable log reporting again by calling the same function with `YES`.</span></span>

### <a name="integration-in-your-settings-bundle"></a><span data-ttu-id="46b20-186">Intégration dans votre groupe de paramètres</span><span class="sxs-lookup"><span data-stu-id="46b20-186">Integration in your settings bundle</span></span>
<span data-ttu-id="46b20-187">Au lieu d'appeler cette fonction, vous pouvez également intégrer ce paramètre directement dans votre fichier `Settings.bundle` existant.</span><span class="sxs-lookup"><span data-stu-id="46b20-187">Instead of calling this function, you can also integrate this setting directly in your existing `Settings.bundle` file.</span></span> <span data-ttu-id="46b20-188">La chaîne `engagement_agent_enabled` doit être utilisée comme identificateur de préférence et doit être associée à un bouton bascule (`PSToggleSwitchSpecifier`).</span><span class="sxs-lookup"><span data-stu-id="46b20-188">The string `engagement_agent_enabled` must be used as a the preference identifier and it must be associated to a toggle switch(`PSToggleSwitchSpecifier`).</span></span>

<span data-ttu-id="46b20-189">L'exemple suivant de `Settings.bundle` montre comment l'implémenter :</span><span class="sxs-lookup"><span data-stu-id="46b20-189">The following example of `Settings.bundle` shows how to implement it:</span></span>

    <dict>
        <key>PreferenceSpecifiers</key>
        <array>
            <dict>
                <key>DefaultValue</key>
                <true/>
                <key>Key</key>
                <string>engagement_agent_enabled</string>
                <key>Title</key>
                <string>Log reporting enabled</string>
                <key>Type</key>
                <string>PSToggleSwitchSpecifier</string>
            </dict>
        </array>
        <key>StringsTable</key>
        <string>Root</string>
    </dict>

<!-- URLs. -->
<span data-ttu-id="46b20-190">[API de l'appareil]: http://go.microsoft.com/?linkid=9876094</span><span class="sxs-lookup"><span data-stu-id="46b20-190">[Device API]: http://go.microsoft.com/?linkid=9876094</span></span>
<span data-ttu-id="46b20-191">[NSLocationWhenInUseUsageDescription]:https://developer.apple.com/library/prerelease/ios/documentation/General/Reference/InfoPlistKeyReference/Articles/CocoaKeys.html#//apple_ref/doc/uid/TP40009251-SW26</span><span class="sxs-lookup"><span data-stu-id="46b20-191">[NSLocationWhenInUseUsageDescription]:https://developer.apple.com/library/prerelease/ios/documentation/General/Reference/InfoPlistKeyReference/Articles/CocoaKeys.html#//apple_ref/doc/uid/TP40009251-SW26</span></span>
<span data-ttu-id="46b20-192">[NSLocationAlwaysUsageDescription]:https://developer.apple.com/library/prerelease/ios/documentation/General/Reference/InfoPlistKeyReference/Articles/CocoaKeys.html#//apple_ref/doc/uid/TP40009251-SW18</span><span class="sxs-lookup"><span data-stu-id="46b20-192">[NSLocationAlwaysUsageDescription]:https://developer.apple.com/library/prerelease/ios/documentation/General/Reference/InfoPlistKeyReference/Articles/CocoaKeys.html#//apple_ref/doc/uid/TP40009251-SW18</span></span>
<span data-ttu-id="46b20-193">[startMonitoringSignificantLocationChanges]:http://developer.apple.com/library/IOs/#documentation/CoreLocation/Reference/CLLocationManager_Class/CLLocationManager/CLLocationManager.html#//apple_ref/occ/instm/CLLocationManager/startMonitoringSignificantLocationChanges</span><span class="sxs-lookup"><span data-stu-id="46b20-193">[startMonitoringSignificantLocationChanges]:http://developer.apple.com/library/IOs/#documentation/CoreLocation/Reference/CLLocationManager_Class/CLLocationManager/CLLocationManager.html#//apple_ref/occ/instm/CLLocationManager/startMonitoringSignificantLocationChanges</span></span>
<span data-ttu-id="46b20-194">[IDFA]:https://developer.apple.com/library/ios/documentation/AdSupport/Reference/ASIdentifierManager_Ref/ASIdentifierManager.html#//apple_ref/occ/instp/ASIdentifierManager/advertisingIdentifier</span><span class="sxs-lookup"><span data-stu-id="46b20-194">[IDFA]:https://developer.apple.com/library/ios/documentation/AdSupport/Reference/ASIdentifierManager_Ref/ASIdentifierManager.html#//apple_ref/occ/instp/ASIdentifierManager/advertisingIdentifier</span></span>
