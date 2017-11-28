---
title: "aaaAzure Mobile Engagement iOS intégration SDK | Documents Microsoft"
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
ms.openlocfilehash: 66ce34efabede7d882caa8a91431a8df71e4fb59
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toointegrate-engagement-on-ios"></a><span data-ttu-id="d49a9-103">Comment tooIntegrate Engagement sur iOS</span><span class="sxs-lookup"><span data-stu-id="d49a9-103">How tooIntegrate Engagement on iOS</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d49a9-104">Windows Universal</span><span class="sxs-lookup"><span data-stu-id="d49a9-104">Windows Universal</span></span>](mobile-engagement-windows-store-integrate-engagement.md)
> * [<span data-ttu-id="d49a9-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="d49a9-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md)
> * [<span data-ttu-id="d49a9-106">iOS</span><span class="sxs-lookup"><span data-stu-id="d49a9-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md)
> * [<span data-ttu-id="d49a9-107">Android</span><span class="sxs-lookup"><span data-stu-id="d49a9-107">Android</span></span>](mobile-engagement-android-integrate-engagement.md)
>
>

<span data-ttu-id="d49a9-108">Cette procédure décrit hello la plus simple façon tooactivate Engagement Analytique et fonctions dans votre application iOS de surveillance.</span><span class="sxs-lookup"><span data-stu-id="d49a9-108">This procedure describes hello simplest way tooactivate Engagement's Analytics and Monitoring functions in your iOS application.</span></span>

<span data-ttu-id="d49a9-109">Hello Engagement SDK nécessite iOS7 + et Xcode 8 + : cible de déploiement hello de votre application doit être au moins iOS 7.</span><span class="sxs-lookup"><span data-stu-id="d49a9-109">hello Engagement SDK requires iOS7+ and Xcode 8+: hello deployment target of your application must be at least iOS 7.</span></span>

> [!NOTE]
> <span data-ttu-id="d49a9-110">Si vous dépendez vraiment de XCode 7, vous pouvez utiliser hello [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh).</span><span class="sxs-lookup"><span data-stu-id="d49a9-110">If you really depend on XCode 7 then you may use hello [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh).</span></span> <span data-ttu-id="d49a9-111">Il existe un bogue connu sur le module de couverture hello de cette version précédente lors de l’exécution sur des appareils iOS 10, consultez [hello portée module intégration](mobile-engagement-ios-integrate-engagement-reach.md) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="d49a9-111">There is a known bug on hello Reach module of this previous version while running on iOS 10 devices see [hello reach module integration](mobile-engagement-ios-integrate-engagement-reach.md) for more details.</span></span> <span data-ttu-id="d49a9-112">Si vous choisissez toouse hello SDK v3.2.4 ignorer hello `UserNotifications.framework` importer à l’étape suivante de hello.</span><span class="sxs-lookup"><span data-stu-id="d49a9-112">If you choose toouse hello SDK v3.2.4 then just skip hello `UserNotifications.framework` import in hello next step.</span></span>
>
>

<span data-ttu-id="d49a9-113">Hello suit est que suffisamment rapport hello tooactivate journaux nécessaires toocompute toutes les statistiques concernant les utilisateurs, Sessions, activités, blocages et Technicals.</span><span class="sxs-lookup"><span data-stu-id="d49a9-113">hello following steps are enough tooactivate hello report of logs needed toocompute all statistics regarding Users, Sessions, Activities, Crashes and Technicals.</span></span> <span data-ttu-id="d49a9-114">rapport Hello de journaux nécessaires toocompute autres statistiques telles que les événements, les erreurs et les tâches doivent être effectués manuellement à l’aide des API de l’Engagement de hello (consultez [comment toouse hello avancé Mobile Engagement marquage API dans votre application iOS](mobile-engagement-ios-use-engagement-api.md) depuis ces statistiques dépendent de l’application.</span><span class="sxs-lookup"><span data-stu-id="d49a9-114">hello report of logs needed toocompute other statistics like Events, Errors and Jobs must be done manually using hello Engagement API  (see [How toouse hello advanced Mobile Engagement tagging API in your iOS app](mobile-engagement-ios-use-engagement-api.md) since these statistics are application dependent.</span></span>

## <a name="embed-hello-engagement-sdk-into-your-ios-project"></a><span data-ttu-id="d49a9-115">Incorporer hello Engagement SDK dans votre projet iOS</span><span class="sxs-lookup"><span data-stu-id="d49a9-115">Embed hello Engagement SDK into your iOS project</span></span>
* <span data-ttu-id="d49a9-116">Télécharger le SDK de hello iOS à partir de [ici](http://aka.ms/qk2rnj).</span><span class="sxs-lookup"><span data-stu-id="d49a9-116">Download hello iOS SDK from [here](http://aka.ms/qk2rnj).</span></span>
* <span data-ttu-id="d49a9-117">Le projet iOS tooyour ajouter hello Engagement SDK : dans Xcode, un clic droit sur votre projet, puis sélectionnez **« ajouter des fichiers trop... »** et choisissez hello `EngagementSDK` dossier.</span><span class="sxs-lookup"><span data-stu-id="d49a9-117">Add hello Engagement SDK tooyour iOS project: in Xcode, right click on your project and select **"Add files too..."** and choose hello `EngagementSDK` folder.</span></span>
* <span data-ttu-id="d49a9-118">Engagement requiert des infrastructures supplémentaires toowork : hello Explorateur de projets, ouvrir votre projet et sélectionnez hello cible correct.</span><span class="sxs-lookup"><span data-stu-id="d49a9-118">Engagement requires additional frameworks toowork: in hello project explorer, open your project pane and select hello correct target.</span></span> <span data-ttu-id="d49a9-119">Ensuite, ouvrez hello **« Build phases »** onglet et Bonjour **« Binaire avec des bibliothèques de liens »** menu, ajoutez ces infrastructures :</span><span class="sxs-lookup"><span data-stu-id="d49a9-119">Then, open hello **"Build phases"** tab and in hello **"Link Binary With Libraries"** menu, add these frameworks:</span></span>

  * <span data-ttu-id="d49a9-120">`UserNotifications.framework`-définir un lien hello en tant que`Optional`</span><span class="sxs-lookup"><span data-stu-id="d49a9-120">`UserNotifications.framework` - set hello link as `Optional`</span></span>
  * <span data-ttu-id="d49a9-121">`AdSupport.framework`-définir un lien hello en tant que`Optional`</span><span class="sxs-lookup"><span data-stu-id="d49a9-121">`AdSupport.framework` - set hello link as `Optional`</span></span>
  * `SystemConfiguration.framework`
  * `CoreTelephony.framework`
  * `CFNetwork.framework`
  * `CoreLocation.framework`
  * `libxml2.dylib`

> [!NOTE]
> <span data-ttu-id="d49a9-122">infrastructure de AdSupport Hello peut être supprimée.</span><span class="sxs-lookup"><span data-stu-id="d49a9-122">hello AdSupport framework can be removed.</span></span> <span data-ttu-id="d49a9-123">Engagement doit cette hello de toocollect framework IDFA.</span><span class="sxs-lookup"><span data-stu-id="d49a9-123">Engagement needs this framework toocollect hello IDFA.</span></span> <span data-ttu-id="d49a9-124">Toutefois, la collection de IDFA peut être désactivée \<ios-sdk-engagement-idfa\> toocomply avec hello nouvelle Apple stratégie en matière de ce code.</span><span class="sxs-lookup"><span data-stu-id="d49a9-124">However, IDFA collection can be disabled \<ios-sdk-engagement-idfa\> toocomply with hello new Apple policy regarding this ID.</span></span>
>
>

## <a name="initialize-hello-engagement-sdk"></a><span data-ttu-id="d49a9-125">Initialiser hello Engagement SDK</span><span class="sxs-lookup"><span data-stu-id="d49a9-125">Initialize hello Engagement SDK</span></span>
<span data-ttu-id="d49a9-126">Vous devez toomodify votre délégué de l’Application :</span><span class="sxs-lookup"><span data-stu-id="d49a9-126">You need toomodify your Application Delegate:</span></span>

* <span data-ttu-id="d49a9-127">En hello en haut de votre fichier d’implémentation, importez l’agent de hello Engagement :</span><span class="sxs-lookup"><span data-stu-id="d49a9-127">At hello top of your implementation file, import hello Engagement agent:</span></span>

      [...]
      #import "EngagementAgent.h"
* <span data-ttu-id="d49a9-128">Initialiser l’Engagement au sein de la méthode hello '**applicationDidFinishLaunching :**'ou'**application : didFinishLaunchingWithOptions :**» :</span><span class="sxs-lookup"><span data-stu-id="d49a9-128">Initialize Engagement inside hello method '**applicationDidFinishLaunching:**' or '**application:didFinishLaunchingWithOptions:**':</span></span>

      - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
      {
        [...]
        [EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}"];
        [...]
      }

## <a name="basic-reporting"></a><span data-ttu-id="d49a9-129">Génération de rapports de base</span><span class="sxs-lookup"><span data-stu-id="d49a9-129">Basic reporting</span></span>
### <a name="recommended-method-overload-your-uiviewcontroller-classes"></a><span data-ttu-id="d49a9-130">Méthode recommandée : surchargez vos classes `UIViewController`</span><span class="sxs-lookup"><span data-stu-id="d49a9-130">Recommended method: overload your `UIViewController` classes</span></span>
<span data-ttu-id="d49a9-131">Dans le rapport de hello order tooactivate de tous les journaux hello requis par Engagement toocompute utilisateurs, Sessions, activités, blocages et statistiques, vous pouvez simplement mettre tous les votre `UIViewController` sous-classes héritent hello `EngagementViewController` (même règle de classes pour `UITableViewController`  - \> `EngagementTableViewController`).</span><span class="sxs-lookup"><span data-stu-id="d49a9-131">In order tooactivate hello report of all hello logs required by Engagement toocompute Users, Sessions, Activities, Crashes and Technical statistics, you can simply make all your `UIViewController` sub-classes inherit from hello `EngagementViewController` classes (same rule for `UITableViewController` -\> `EngagementTableViewController`).</span></span>

<span data-ttu-id="d49a9-132">**Sans Engagement :**</span><span class="sxs-lookup"><span data-stu-id="d49a9-132">**Without Engagement :**</span></span>

    #import <UIKit/UIKit.h>

    @interface Tab1ViewController : UIViewController<UITextFieldDelegate> {
      UITextField* myTextField1;
      UITextField* myTextField2;
    }

    @property (nonatomic, retain) IBOutlet UITextField* myTextField1;
    @property (nonatomic, retain) IBOutlet UITextField* myTextField2;

<span data-ttu-id="d49a9-133">**Avec Engagement :**</span><span class="sxs-lookup"><span data-stu-id="d49a9-133">**With Engagement :**</span></span>

    #import <UIKit/UIKit.h>
    #import "EngagementViewController.h"

    @interface Tab1ViewController : EngagementViewController<UITextFieldDelegate> {
      UITextField* myTextField1;
      UITextField* myTextField2;
    }

    @property (nonatomic, retain) IBOutlet UITextField* myTextField1;
    @property (nonatomic, retain) IBOutlet UITextField* myTextField2;

### <a name="alternate-method-call-startactivity-manually"></a><span data-ttu-id="d49a9-134">Autre méthode : appeler `startActivity()` manuellement</span><span class="sxs-lookup"><span data-stu-id="d49a9-134">Alternate method: call `startActivity()` manually</span></span>
<span data-ttu-id="d49a9-135">Si vous ne pouvez pas ou ne souhaitez pas que toooverload votre `UIViewController` classes, vous pouvez démarrer à la place de vos activités en appelant `EngagementAgent`de méthodes directement.</span><span class="sxs-lookup"><span data-stu-id="d49a9-135">If you cannot or do not want toooverload your `UIViewController` classes, you can instead start your activities by calling `EngagementAgent`'s methods directly.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d49a9-136">Hello, iOS SDK appelle automatiquement hello `endActivity()` méthode lors de l’application hello est fermée.</span><span class="sxs-lookup"><span data-stu-id="d49a9-136">hello iOS SDK automatically calls hello `endActivity()` method when hello application is closed.</span></span> <span data-ttu-id="d49a9-137">Par conséquent, il est *hautement* recommandé toocall hello `startActivity` méthode chaque fois que l’activité hello d’utilisateur de hello modifier et trop*jamais* appel hello `endActivity` méthode, depuis l’appel de cette méthode force Bonjour toobe de session en cours s’est terminée.</span><span class="sxs-lookup"><span data-stu-id="d49a9-137">Thus, it is *HIGHLY* recommended toocall hello `startActivity` method whenever hello activity of hello user change, and too*NEVER* call hello `endActivity` method, since calling this method forces hello current session toobe ended.</span></span>
>
>

## <a name="location-reporting"></a><span data-ttu-id="d49a9-138">Rapports d'emplacement</span><span class="sxs-lookup"><span data-stu-id="d49a9-138">Location reporting</span></span>
<span data-ttu-id="d49a9-139">Conditions d’utilisation de Apple n’autorisent pas les applications emplacement toouse suivi uniquement à des fins de statistiques.</span><span class="sxs-lookup"><span data-stu-id="d49a9-139">Apple terms of service do not allow applications toouse location tracking for statistics purpose only.</span></span> <span data-ttu-id="d49a9-140">Par conséquent, il est recommandé de tooenable emplacement rapports uniquement si votre application utilise également hello suivi d’emplacement pour une autre raison.</span><span class="sxs-lookup"><span data-stu-id="d49a9-140">Thus, it is recommended tooenable location reports only if your application also use hello location tracking for another reason.</span></span>

<span data-ttu-id="d49a9-141">À compter d’iOS 8, vous devez fournir une description de votre application utilise les services d’emplacement en définissant une chaîne de clé de hello [NSLocationWhenInUseUsageDescription] ou [NSLocationAlwaysUsageDescription]dans le fichier Info.plist de votre application.</span><span class="sxs-lookup"><span data-stu-id="d49a9-141">Starting with iOS 8, you must provide a description for how your app uses location services by setting a string for hello key [NSLocationWhenInUseUsageDescription] or [NSLocationAlwaysUsageDescription] in your app's Info.plist file.</span></span> <span data-ttu-id="d49a9-142">Si vous souhaitez emplacement tooreport en arrière-plan hello avec Engagement, ajoutez la clé de hello NSLocationAlwaysUsageDescription.</span><span class="sxs-lookup"><span data-stu-id="d49a9-142">If you want tooreport location in hello background with Engagement, add hello key NSLocationAlwaysUsageDescription.</span></span> <span data-ttu-id="d49a9-143">Dans tous les autres cas, ajoutez la clé de hello NSLocationWhenInUseUsageDescription.</span><span class="sxs-lookup"><span data-stu-id="d49a9-143">In all other cases, add hello key NSLocationWhenInUseUsageDescription.</span></span> <span data-ttu-id="d49a9-144">Notez que vous avez besoin d’emplacement d’arrière-plan tooreport NSLocationAlwaysAndWhenInUseUsageDescription et NSLocationWhenInUseUsageDescription sur iOS 11.</span><span class="sxs-lookup"><span data-stu-id="d49a9-144">Note that you need both NSLocationAlwaysAndWhenInUseUsageDescription and NSLocationWhenInUseUsageDescription tooreport background location on iOS 11.</span></span>

### <a name="lazy-area-location-reporting"></a><span data-ttu-id="d49a9-145">Rapports d'emplacement de zone différé</span><span class="sxs-lookup"><span data-stu-id="d49a9-145">Lazy area location reporting</span></span>
<span data-ttu-id="d49a9-146">Signalisation différée de zone emplacement permet tooreport hello pays, la région et localité associés toodevices.</span><span class="sxs-lookup"><span data-stu-id="d49a9-146">Lazy area location reporting allows tooreport hello country, region and locality associated toodevices.</span></span> <span data-ttu-id="d49a9-147">Ce type de rapport d'emplacement utilise uniquement des emplacements réseau (basés sur l'ID cellulaire ou le Wi-Fi).</span><span class="sxs-lookup"><span data-stu-id="d49a9-147">This type of location reporting only uses network locations (based on Cell ID or WIFI).</span></span> <span data-ttu-id="d49a9-148">zone de Hello est signalée au maximum une fois par session.</span><span class="sxs-lookup"><span data-stu-id="d49a9-148">hello device area is reported at most once per session.</span></span> <span data-ttu-id="d49a9-149">Hello GPS n’est jamais utilisé, et par conséquent, ce type de rapport de l’emplacement a très peu (pas toosay aucune) impact sur la batterie de hello.</span><span class="sxs-lookup"><span data-stu-id="d49a9-149">hello GPS is never used, and thus this type of location report has very few (not toosay no) impact on hello battery.</span></span>

<span data-ttu-id="d49a9-150">Les zones signalés sont utilisés toocompute des statistiques géographique sur les utilisateurs, des sessions, des événements et des erreurs.</span><span class="sxs-lookup"><span data-stu-id="d49a9-150">Reported areas are used toocompute geographic statistics about users, sessions, events and errors.</span></span> <span data-ttu-id="d49a9-151">Elles peuvent également servir de critère dans les couvertures campagne.</span><span class="sxs-lookup"><span data-stu-id="d49a9-151">They can also be used as criterion in Reach campaigns.</span></span> <span data-ttu-id="d49a9-152">Hello dernière connue zone signalé pour un périphérique peut être récupérée Merci toohello [Device API].</span><span class="sxs-lookup"><span data-stu-id="d49a9-152">hello last known area reported for a device can be retrieved thanks toohello [Device API].</span></span>

<span data-ttu-id="d49a9-153">emplacement de zone différée tooenable reporting, ajoutez hello ligne suivante après l’initialisation de l’agent de hello Engagement :</span><span class="sxs-lookup"><span data-stu-id="d49a9-153">tooenable lazy area location reporting, add hello following line after initializing hello Engagement agent:</span></span>

    - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
    {
      [...]
      [[EngagementAgent shared] setLazyAreaLocationReport:YES];
      [...]
    }

### <a name="real-time-location-reporting"></a><span data-ttu-id="d49a9-154">Rapports d'emplacement en temps réel</span><span class="sxs-lookup"><span data-stu-id="d49a9-154">Real time location reporting</span></span>
<span data-ttu-id="d49a9-155">Signalisation de l’emplacement en temps réel permet de latitude de hello tooreport et longitude associés toodevices.</span><span class="sxs-lookup"><span data-stu-id="d49a9-155">Real time location reporting allows tooreport hello latitude and longitude associated toodevices.</span></span> <span data-ttu-id="d49a9-156">Par défaut, ce type d’emplacement reporting utilise uniquement des emplacements réseau (basés sur l’ID de la cellule ou Wi-Fi), et hello reporting est uniquement active lorsque l’application hello s’exécute en premier plan (par exemple, lors d’une session).</span><span class="sxs-lookup"><span data-stu-id="d49a9-156">By default, this type of location reporting only uses network locations (based on Cell ID or WIFI), and hello reporting is only active when hello application runs in foreground (i.e. during a session).</span></span>

<span data-ttu-id="d49a9-157">Les emplacements en temps réel sont *pas* utilisé toocompute statistiques.</span><span class="sxs-lookup"><span data-stu-id="d49a9-157">Real time locations are *NOT* used toocompute statistics.</span></span> <span data-ttu-id="d49a9-158">Leur utilisation de hello tooallow de délimitation géographique en temps réel ne sert que \<portée-public-géorepérage\> critère dans les campagnes Reach.</span><span class="sxs-lookup"><span data-stu-id="d49a9-158">Their only purpose is tooallow hello use of real time geo-fencing \<Reach-Audience-geofencing\> criterion in Reach campaigns.</span></span>

<span data-ttu-id="d49a9-159">emplacement en temps réel de tooenable création de rapports, ajoutez hello ligne suivante après l’initialisation de l’agent de hello Engagement :</span><span class="sxs-lookup"><span data-stu-id="d49a9-159">tooenable real time location reporting, add hello following line after initializing hello Engagement agent:</span></span>

    [[EngagementAgent shared] setRealtimeLocationReport:YES];

#### <a name="gps-based-reporting"></a><span data-ttu-id="d49a9-160">Rapports GPS</span><span class="sxs-lookup"><span data-stu-id="d49a9-160">GPS based reporting</span></span>
<span data-ttu-id="d49a9-161">Par défaut, le rapport d'emplacement en temps réel utilise uniquement des emplacements réseau.</span><span class="sxs-lookup"><span data-stu-id="d49a9-161">By default, real time location reporting only uses network based locations.</span></span> <span data-ttu-id="d49a9-162">utilisation de hello tooenable de GPS en fonction des emplacements (qui sont beaucoup plus précises), ajoutez :</span><span class="sxs-lookup"><span data-stu-id="d49a9-162">tooenable hello use of GPS based locations (which are far more precise), add:</span></span>

    [[EngagementAgent shared] setFineRealtimeLocationReport:YES];

#### <a name="background-reporting"></a><span data-ttu-id="d49a9-163">Rapports en arrière-plan</span><span class="sxs-lookup"><span data-stu-id="d49a9-163">Background reporting</span></span>
<span data-ttu-id="d49a9-164">Par défaut, reporting en temps réel sur l’emplacement est uniquement active lorsque l’application hello s’exécute en premier plan (par exemple, lors d’une session).</span><span class="sxs-lookup"><span data-stu-id="d49a9-164">By default, real time location reporting is only active when hello application runs in foreground (i.e. during a session).</span></span> <span data-ttu-id="d49a9-165">hello tooenable reporting également en arrière-plan, ajoutez :</span><span class="sxs-lookup"><span data-stu-id="d49a9-165">tooenable hello reporting also in background, add:</span></span>

    [[EngagementAgent shared] setBackgroundRealtimeLocationReport:YES withLaunchOptions:launchOptions];

> [!NOTE]
> <span data-ttu-id="d49a9-166">Lors de l’application hello s’exécute en arrière-plan, seuls les emplacements réseau sont signalées, même si vous avez activé hello GPS.</span><span class="sxs-lookup"><span data-stu-id="d49a9-166">When hello application runs in background, only network based locations are reported, even if you enabled hello GPS.</span></span>
>
>

<span data-ttu-id="d49a9-167">Implémentation de cette fonction appelle [startMonitoringSignificantLocationChanges] lorsque votre application passe en arrière-plan de hello.</span><span class="sxs-lookup"><span data-stu-id="d49a9-167">Implementation of this function will call [startMonitoringSignificantLocationChanges] when your application goes into hello background.</span></span> <span data-ttu-id="d49a9-168">N’oubliez pas qu’il sera automatiquement relancer votre application en arrière-plan de hello si l’arrivée d’un nouvel événement d’emplacement.</span><span class="sxs-lookup"><span data-stu-id="d49a9-168">Be aware that it will automatically relaunch your application into hello background if a new location event arrives.</span></span>

## <a name="advanced-reporting"></a><span data-ttu-id="d49a9-169">Génération de rapports avancés</span><span class="sxs-lookup"><span data-stu-id="d49a9-169">Advanced reporting</span></span>
<span data-ttu-id="d49a9-170">Si vous le souhaitez, si vous souhaitez tooreport les événements d’application spécifique, les erreurs et les tâches, vous devez toouse hello Engagement API via les méthodes hello Hello `EngagementAgent` classe.</span><span class="sxs-lookup"><span data-stu-id="d49a9-170">Optionally, if you want tooreport application specific events, errors and jobs, you need toouse hello Engagement API through hello methods of hello `EngagementAgent` class.</span></span> <span data-ttu-id="d49a9-171">Un objet de cette classe peut être récupéré en appelant hello `[EngagementAgent shared]` méthode statique.</span><span class="sxs-lookup"><span data-stu-id="d49a9-171">An object of this class can be retrieved by calling hello `[EngagementAgent shared]` static method.</span></span>

<span data-ttu-id="d49a9-172">permet de toouse toutes les fonctionnalités avancées d’Engagement Hello Engagement API et est détaillée dans hello comment tooUse l’API d’Engagement sur iOS (ainsi que dans la documentation technique de hello Hello `EngagementAgent` classe).</span><span class="sxs-lookup"><span data-stu-id="d49a9-172">hello Engagement API allows toouse all of Engagement's advanced capabilities and is detailed in hello How tooUse the Engagement API on iOS (as well as in hello technical documentation of hello `EngagementAgent` class).</span></span>

## <a name="disable-idfa-collection"></a><span data-ttu-id="d49a9-173">Désactiver la collecte de l'IDFA</span><span class="sxs-lookup"><span data-stu-id="d49a9-173">Disable IDFA collection</span></span>
<span data-ttu-id="d49a9-174">Par défaut, Engagement utilisera hello [IDFA] toouniquely identifier un utilisateur.</span><span class="sxs-lookup"><span data-stu-id="d49a9-174">By default, Engagement will use hello [IDFA] toouniquely identify a user.</span></span> <span data-ttu-id="d49a9-175">Mais si vous n’utilisez pas de publication ailleurs dans l’application hello, vous pourrez être rejetée par le processus de révision App Store de hello.</span><span class="sxs-lookup"><span data-stu-id="d49a9-175">But if you’re not using advertising elsewhere in hello app, you might be rejected by hello App Store review process.</span></span> <span data-ttu-id="d49a9-176">Collection de IDFA peut être désactivée en ajoutant la macro de préprocesseur hello `ENGAGEMENT_DISABLE_IDFA` dans votre fichier pch (ou Bonjour `Build Settings` de votre application).</span><span class="sxs-lookup"><span data-stu-id="d49a9-176">IDFA collection can be disabled by adding hello preprocessor macro `ENGAGEMENT_DISABLE_IDFA` in your pch file (or in hello `Build Settings` of your application).</span></span> <span data-ttu-id="d49a9-177">Cela permet de garantir qu’il n’existe aucune référence trop`ASIdentifierManager`, `advertisingIdentifier` ou `isAdvertisingTrackingEnabled` dans la build d’application hello.</span><span class="sxs-lookup"><span data-stu-id="d49a9-177">This will ensure that there is no references too`ASIdentifierManager`, `advertisingIdentifier` or `isAdvertisingTrackingEnabled` in hello application build.</span></span>

<span data-ttu-id="d49a9-178">Intégration dans hello **prefix.pch** fichier :</span><span class="sxs-lookup"><span data-stu-id="d49a9-178">Integration in hello **prefix.pch** file:</span></span>

    #define ENGAGEMENT_DISABLE_IDFA
    ...

<span data-ttu-id="d49a9-179">Vous pouvez vérifier que collection IDFA de hello est correctement désactivée dans votre application en vérifiant les journaux des tests hello Engagement.</span><span class="sxs-lookup"><span data-stu-id="d49a9-179">You can verify that hello IDFA collection is properly disabled in your application by checking hello Engagement test logs.</span></span> <span data-ttu-id="d49a9-180">Consultez hello des tests d’intégration\<idfa du test engagement ios sdk\> documentation pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="d49a9-180">See hello Integration Test\<ios-sdk-engagement-test-idfa\> documentation for further information.</span></span>

## <a name="disable-log-reporting"></a><span data-ttu-id="d49a9-181">Désactiver les rapports de suivi</span><span class="sxs-lookup"><span data-stu-id="d49a9-181">Disable log reporting</span></span>
### <a name="using-a-method-call"></a><span data-ttu-id="d49a9-182">En appelant une méthode</span><span class="sxs-lookup"><span data-stu-id="d49a9-182">Using a method call</span></span>
<span data-ttu-id="d49a9-183">Si vous souhaitez toostop Engagement envoi de journaux, vous pouvez appeler :</span><span class="sxs-lookup"><span data-stu-id="d49a9-183">If you want Engagement toostop sending logs, you can call:</span></span>

    [[EngagementAgent shared] setEnabled:NO];

<span data-ttu-id="d49a9-184">Cet appel est persistant : il utilise `NSUserDefaults` plus d’informations toostore hello.</span><span class="sxs-lookup"><span data-stu-id="d49a9-184">This call is persistent: it uses `NSUserDefaults` toostore hello information.</span></span>

<span data-ttu-id="d49a9-185">Vous pouvez activer le journal de création de rapports en appelant hello même fonction avec `YES`.</span><span class="sxs-lookup"><span data-stu-id="d49a9-185">You can enable log reporting again by calling hello same function with `YES`.</span></span>

### <a name="integration-in-your-settings-bundle"></a><span data-ttu-id="d49a9-186">Intégration dans votre groupe de paramètres</span><span class="sxs-lookup"><span data-stu-id="d49a9-186">Integration in your settings bundle</span></span>
<span data-ttu-id="d49a9-187">Au lieu d'appeler cette fonction, vous pouvez également intégrer ce paramètre directement dans votre fichier `Settings.bundle` existant.</span><span class="sxs-lookup"><span data-stu-id="d49a9-187">Instead of calling this function, you can also integrate this setting directly in your existing `Settings.bundle` file.</span></span> <span data-ttu-id="d49a9-188">Hello chaîne `engagement_agent_enabled` doit être utilisé comme un identificateur de préférence hello et il doivent être associé tooa bouton bascule (`PSToggleSwitchSpecifier`).</span><span class="sxs-lookup"><span data-stu-id="d49a9-188">hello string `engagement_agent_enabled` must be used as a hello preference identifier and it must be associated tooa toggle switch(`PSToggleSwitchSpecifier`).</span></span>

<span data-ttu-id="d49a9-189">Hello selon l’exemple de `Settings.bundle` montre comment tooimplement il :</span><span class="sxs-lookup"><span data-stu-id="d49a9-189">hello following example of `Settings.bundle` shows how tooimplement it:</span></span>

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
[Device API]: http://go.microsoft.com/?linkid=9876094
[NSLocationWhenInUseUsageDescription]:https://developer.apple.com/library/prerelease/ios/documentation/General/Reference/InfoPlistKeyReference/Articles/CocoaKeys.html#//apple_ref/doc/uid/TP40009251-SW26
[NSLocationAlwaysUsageDescription]:https://developer.apple.com/library/prerelease/ios/documentation/General/Reference/InfoPlistKeyReference/Articles/CocoaKeys.html#//apple_ref/doc/uid/TP40009251-SW18
[startMonitoringSignificantLocationChanges]:http://developer.apple.com/library/IOs/#documentation/CoreLocation/Reference/CLLocationManager_Class/CLLocationManager/CLLocationManager.html#//apple_ref/occ/instm/CLLocationManager/startMonitoringSignificantLocationChanges
[IDFA]:https://developer.apple.com/library/ios/documentation/AdSupport/Reference/ASIdentifierManager_Ref/ASIdentifierManager.html#//apple_ref/occ/instp/ASIdentifierManager/advertisingIdentifier
