---
title: "aaaAzure intégration du Kit de développement logiciel Android Mobile Engagement"
description: "Dernières mises à jour et procédures du SDK Android pour Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: a5487793-1a12-4f6c-a1cf-587c5a671e6b
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 4f79936ea0fa6102023dec2b4682032a4a81fa9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toointegrate-engagement-on-android"></a><span data-ttu-id="a2c9a-103">Comment tooIntegrate Engagement sur Android</span><span class="sxs-lookup"><span data-stu-id="a2c9a-103">How tooIntegrate Engagement on Android</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a2c9a-104">Windows Universal</span><span class="sxs-lookup"><span data-stu-id="a2c9a-104">Windows Universal</span></span>](mobile-engagement-windows-store-integrate-engagement.md)
> * [<span data-ttu-id="a2c9a-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="a2c9a-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md)
> * [<span data-ttu-id="a2c9a-106">iOS</span><span class="sxs-lookup"><span data-stu-id="a2c9a-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md)
> * [<span data-ttu-id="a2c9a-107">Android</span><span class="sxs-lookup"><span data-stu-id="a2c9a-107">Android</span></span>](mobile-engagement-android-integrate-engagement.md)
> 
> 

<span data-ttu-id="a2c9a-108">Cette procédure décrit Analytique et surveillance de votre application Android hello la plus simple façon tooactivate Engagement.</span><span class="sxs-lookup"><span data-stu-id="a2c9a-108">This procedure describes hello simplest way tooactivate Engagement's Analytics and Monitoring functions in your Android application.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a2c9a-109">Le niveau minimum de l'API SDK Android doit être égal ou supérieur à 10 (Android 2.3.3 ou version ultérieure).</span><span class="sxs-lookup"><span data-stu-id="a2c9a-109">Your minimum Android SDK API level must be 10 or higher (Android 2.3.3 or higher).</span></span>
> 
> 

<span data-ttu-id="a2c9a-110">Hello suit est que suffisamment rapport hello tooactivates journaux nécessaires toocompute toutes les statistiques concernant les utilisateurs, Sessions, activités, blocages et Technicals.</span><span class="sxs-lookup"><span data-stu-id="a2c9a-110">hello following steps are enough tooactivates hello report of logs needed toocompute all statistics regarding Users, Sessions, Activities, Crashes and Technicals.</span></span> <span data-ttu-id="a2c9a-111">rapport Hello de journaux nécessaires toocompute autres statistiques telles que les événements, les erreurs et les tâches doivent être effectués manuellement à l’aide des API de l’Engagement de hello (consultez [comment toouse hello avancé Mobile Engagement marquage API dans votre Android](mobile-engagement-android-use-engagement-api.md) depuis ces les statistiques sont dépend de l’application.</span><span class="sxs-lookup"><span data-stu-id="a2c9a-111">hello report of logs needed toocompute other statistics like Events, Errors and Jobs must be done manually using hello Engagement API (see [How toouse hello advanced Mobile Engagement tagging API in your Android](mobile-engagement-android-use-engagement-api.md) since these statistics are application dependent.</span></span>

## <a name="embed-hello-engagement-sdk-and-service-into-your-android-project"></a><span data-ttu-id="a2c9a-112">Incorporer hello Engagement SDK et service dans votre projet Android</span><span class="sxs-lookup"><span data-stu-id="a2c9a-112">Embed hello Engagement SDK and service into your Android project</span></span>
<span data-ttu-id="a2c9a-113">Téléchargement hello du SDK Android à partir de [ici](https://aka.ms/vq9mfn) obtenir `mobile-engagement-VERSION.jar` et placez-les dans hello `libs` dossier de votre projet Android (créer le dossier de bibliothèques hello s’il n’existe pas encore).</span><span class="sxs-lookup"><span data-stu-id="a2c9a-113">Download hello Android SDK from [here](https://aka.ms/vq9mfn) Get `mobile-engagement-VERSION.jar` and put them into hello `libs` folder of your Android project (create hello libs folder if it does not exist yet).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a2c9a-114">Si vous générez votre package d’application avec ProGuard, vous devez tookeep certaines classes.</span><span class="sxs-lookup"><span data-stu-id="a2c9a-114">If you build your application package with ProGuard, you need tookeep some classes.</span></span> <span data-ttu-id="a2c9a-115">Vous pouvez utiliser hello suivant extrait de configuration :</span><span class="sxs-lookup"><span data-stu-id="a2c9a-115">You can use hello following configuration snippet:</span></span>
> 
> <span data-ttu-id="a2c9a-116">-keep public class * extends android.os.IInterface -keep class com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity$EngagementReachContentJS {</span><span class="sxs-lookup"><span data-stu-id="a2c9a-116">-keep public class * extends android.os.IInterface -keep class com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity$EngagementReachContentJS {</span></span>
> 
> <span data-ttu-id="a2c9a-117"><methods>; }</span><span class="sxs-lookup"><span data-stu-id="a2c9a-117"><methods>; }</span></span>
> 
> 

<span data-ttu-id="a2c9a-118">Spécifiez votre chaîne de connexion Engagement en appelant hello suivant de méthode dans l’activité de lanceur hello :</span><span class="sxs-lookup"><span data-stu-id="a2c9a-118">Specify your Engagement connection string by calling hello following method in hello launcher activity:</span></span>

            EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
            engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
            EngagementAgent.getInstance(this).init(engagementConfiguration);

<span data-ttu-id="a2c9a-119">chaîne de connexion Hello pour votre application s’affiche sur le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="a2c9a-119">hello connection string for your application is displayed on Azure Portal.</span></span>

* <span data-ttu-id="a2c9a-120">Si manquant, ajouter hello Android autorisations suivantes (avant hello `<application>` étiquette) :</span><span class="sxs-lookup"><span data-stu-id="a2c9a-120">If missing, add hello following Android permissions (before hello `<application>` tag):</span></span>
  
          <uses-permission android:name="android.permission.INTERNET"/>
          <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
* <span data-ttu-id="a2c9a-121">Ajouter hello après section (entre hello `<application>` et `</application>` balises) :</span><span class="sxs-lookup"><span data-stu-id="a2c9a-121">Add hello following section (between hello `<application>` and `</application>` tags):</span></span>
  
          <service
            android:name="com.microsoft.azure.engagement.service.EngagementService"
            android:exported="false"
            android:label="<Your application name>Service"
            android:process=":Engagement"/>
* <span data-ttu-id="a2c9a-122">Modification `<Your application name>` par nom hello de votre application.</span><span class="sxs-lookup"><span data-stu-id="a2c9a-122">Change `<Your application name>` by hello name of your application.</span></span>

> [!TIP]
> <span data-ttu-id="a2c9a-123">Hello `android:label` attribut permet de vous toochoose hello nom de service de l’Engagement de hello tel qu’il apparaîtra aux utilisateurs finaux toohello sur l’écran hello « Services en cours d’exécution » de leur téléphone.</span><span class="sxs-lookup"><span data-stu-id="a2c9a-123">hello `android:label` attribute allows you toochoose hello name of hello Engagement service as it will appear toohello end-users in hello "Running services" screen of their phone.</span></span> <span data-ttu-id="a2c9a-124">Il est recommandé de cet attribut tooset trop`"<Your application name>Service"` (par exemple, `"AcmeFunGameService"`).</span><span class="sxs-lookup"><span data-stu-id="a2c9a-124">It is recommended tooset this attribute too`"<Your application name>Service"` (e.g. `"AcmeFunGameService"`).</span></span>
> 
> 

<span data-ttu-id="a2c9a-125">En spécifiant hello `android:process` attribut garantit que ce service de l’Engagement hello s’exécute dans son propre processus (en cours d’exécution Engagement Bonjour même processus que votre application permettront à votre thread principal / l’interface utilisateur potentiellement moins sensible).</span><span class="sxs-lookup"><span data-stu-id="a2c9a-125">Specifying hello `android:process` attribute ensures that hello Engagement service will run in its own process (running Engagement in hello same process as your application will make your main/UI thread potentially less responsive).</span></span>

> [!NOTE]
> <span data-ttu-id="a2c9a-126">Tout code que vous placez dans `Application.onCreate()` et autres rappels de l’application seront exécutés pour les processus de tous les votre application, y compris le service d’Engagement hello.</span><span class="sxs-lookup"><span data-stu-id="a2c9a-126">Any code you place in `Application.onCreate()` and other application callbacks will be run for all your application's processes, including hello Engagement service.</span></span> <span data-ttu-id="a2c9a-127">Elle peut avoir des effets secondaires indésirables (par exemple, les allocations de mémoire inutiles et les threads de processus, les récepteurs de diffusion en double ou les services d’Engagement hello).</span><span class="sxs-lookup"><span data-stu-id="a2c9a-127">It may have unwanted side effects (like unneeded memory allocations and threads in hello Engagement's process, duplicate broadcast receivers or services).</span></span>
> 
> 

<span data-ttu-id="a2c9a-128">Si vous substituez `Application.onCreate()`, il est hello tooadd recommandée suivante extrait de code au début de hello de votre `Application.onCreate()` fonction :</span><span class="sxs-lookup"><span data-stu-id="a2c9a-128">If you override `Application.onCreate()`, it's recommended tooadd hello following code snippet at hello beginning of your `Application.onCreate()` function:</span></span>

             public void onCreate()
             {
               if (EngagementAgentUtils.isInDedicatedEngagementProcess(this))
                 return;

               ... Your code...
             }

<span data-ttu-id="a2c9a-129">Vous pouvez effectuer hello même chose pour `Application.onTerminate()`, `Application.onLowMemory()` et `Application.onConfigurationChanged(...)`.</span><span class="sxs-lookup"><span data-stu-id="a2c9a-129">You can do hello same thing for `Application.onTerminate()`, `Application.onLowMemory()` and `Application.onConfigurationChanged(...)`.</span></span>

<span data-ttu-id="a2c9a-130">Vous pouvez également étendre `EngagementApplication` au lieu de l’extension `Application`: hello rappel `Application.onCreate()` hello vérification de processus et les appels `Application.onApplicationProcessCreate()` uniquement si le processus actuel de hello n’est pas hello un hello Engagement service d’hébergement, hello mêmes règles s’appliquent pour Bonjour autres rappels.</span><span class="sxs-lookup"><span data-stu-id="a2c9a-130">You can also extend `EngagementApplication` instead of extending `Application`: hello callback `Application.onCreate()` does hello process check and calls `Application.onApplicationProcessCreate()` only if hello current process is not hello one hosting hello Engagement service, hello same rules apply for hello other callbacks.</span></span>

## <a name="basic-reporting"></a><span data-ttu-id="a2c9a-131">Génération de rapports de base</span><span class="sxs-lookup"><span data-stu-id="a2c9a-131">Basic reporting</span></span>
### <a name="recommended-method-overload-your-activity-classes"></a><span data-ttu-id="a2c9a-132">Méthode recommandée : surchargez vos classes `Activity`</span><span class="sxs-lookup"><span data-stu-id="a2c9a-132">Recommended method: overload your `Activity` classes</span></span>
<span data-ttu-id="a2c9a-133">Dans le rapport de hello order tooactivate de tous les journaux hello requis par Engagement toocompute utilisateurs, Sessions, activités, blocages et statistiques, il vous suffit toomake tous vos `*Activity` sous-classes héritent hello correspondant `Engagement*Activity` classes (par exemple, si votre activité hérité étend `ListActivity`, assurez-vous qu’il étend `EngagementListActivity`).</span><span class="sxs-lookup"><span data-stu-id="a2c9a-133">In order tooactivate hello report of all hello logs required by Engagement toocompute Users, Sessions, Activities, Crashes and Technical statistics, you just have toomake all your `*Activity` sub-classes inherit from hello corresponding `Engagement*Activity` classes (e.g. if your legacy activity extends `ListActivity`, make it extends `EngagementListActivity`).</span></span>

<span data-ttu-id="a2c9a-134">**Sans Engagement :**</span><span class="sxs-lookup"><span data-stu-id="a2c9a-134">**Without Engagement :**</span></span>

            package com.company.myapp;

            import android.app.Activity;
            import android.os.Bundle;

            public class MyApp extends Activity
            {
              @Override
              public void onCreate(Bundle savedInstanceState)
              {
                super.onCreate(savedInstanceState);
                setContentView(R.layout.main);
              }
            }

<span data-ttu-id="a2c9a-135">**Avec Engagement :**</span><span class="sxs-lookup"><span data-stu-id="a2c9a-135">**With Engagement :**</span></span>

            package com.company.myapp;

            import com.microsoft.azure.engagement.activity.EngagementActivity;
            import android.os.Bundle;

            public class MyApp extends EngagementActivity
            {
              @Override
              public void onCreate(Bundle savedInstanceState)
              {
                super.onCreate(savedInstanceState);
                setContentView(R.layout.main);
              }
            }

> [!IMPORTANT]
> <span data-ttu-id="a2c9a-136">Lorsque vous utilisez `EngagementListActivity` ou `EngagementExpandableListActivity`, assurez-vous que tout appel trop`requestWindowFeature(...);` est effectuée avant l’appel de hello trop`super.onCreate(...);`, sinon un incident se produit.</span><span class="sxs-lookup"><span data-stu-id="a2c9a-136">When using `EngagementListActivity` or `EngagementExpandableListActivity`, make sure any call too`requestWindowFeature(...);` is made before hello call too`super.onCreate(...);`, otherwise a crash will occur.</span></span>
> 
> 

<span data-ttu-id="a2c9a-137">Vous pouvez trouver ces classes Bonjour `src` dossier, puis les copier dans votre projet.</span><span class="sxs-lookup"><span data-stu-id="a2c9a-137">You can find these classes in hello `src` folder, and can copy them into your project.</span></span> <span data-ttu-id="a2c9a-138">classes de Hello figurent également dans hello **JavaDoc**.</span><span class="sxs-lookup"><span data-stu-id="a2c9a-138">hello classes are also in hello **JavaDoc**.</span></span>

### <a name="alternate-method-call-startactivity-and-endactivity-manually"></a><span data-ttu-id="a2c9a-139">Méthode alternative : appelez `startActivity()` et `endActivity()` manuellement</span><span class="sxs-lookup"><span data-stu-id="a2c9a-139">Alternate method: call `startActivity()` and `endActivity()` manually</span></span>
<span data-ttu-id="a2c9a-140">Si vous ne pouvez pas ou ne souhaitez pas que toooverload votre `Activity` classes, vous pouvez à la place de début et de fin de vos activités en appelant `EngagementAgent`de méthodes directement.</span><span class="sxs-lookup"><span data-stu-id="a2c9a-140">If you cannot or do not want toooverload your `Activity` classes, you can instead start and end your activities by calling `EngagementAgent`'s methods directly.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a2c9a-141">Hello du SDK Android n’appelle jamais hello `endActivity()` méthode, même lorsque l’application hello est fermée (sur Android, les applications sont en fait jamais fermées).</span><span class="sxs-lookup"><span data-stu-id="a2c9a-141">hello Android SDK never calls hello `endActivity()` method, even when hello application is closed (on Android, applications are actually never closed).</span></span> <span data-ttu-id="a2c9a-142">Par conséquent, il est *hautement* recommandé toocall hello `startActivity()` méthode Bonjour `onResume` rappel de *tous les* vos activités et hello `endActivity()` méthode Bonjour `onPause()` rappel de *tous les* vos activités.</span><span class="sxs-lookup"><span data-stu-id="a2c9a-142">Thus, it is *HIGHLY* recommended toocall hello `startActivity()` method in hello `onResume` callback of *ALL* your activities, and hello `endActivity()` method in hello `onPause()` callback of *ALL* your activities.</span></span> <span data-ttu-id="a2c9a-143">Il s’agit de toobe moyen hello uniquement assurer que les sessions ne seront pas divulguées.</span><span class="sxs-lookup"><span data-stu-id="a2c9a-143">This is hello only way toobe sure that sessions will not be leaked.</span></span> <span data-ttu-id="a2c9a-144">Si une session est perdue, hello service d’Engagement sera déconnecté jamais hello Engagement principal (étant donné que le service de hello reste connecté en tant qu’une session est en attente).</span><span class="sxs-lookup"><span data-stu-id="a2c9a-144">If a session is leaked, hello Engagement service will never disconnect from hello Engagement backend (since hello service stays connected as long as a session is pending).</span></span>
> 
> 

<span data-ttu-id="a2c9a-145">Voici un exemple :</span><span class="sxs-lookup"><span data-stu-id="a2c9a-145">Here is an example:</span></span>

            public class MyActivity extends Some3rdPartyActivity
            {
              @Override
              protected void onResume()
              {
                super.onResume();
                String activityNameOnEngagement = EngagementAgentUtils.buildEngagementActivityName(getClass()); // Uses short class name and removes "Activity" at hello end.
                EngagementAgent.getInstance(this).startActivity(this, activityNameOnEngagement, null);
              }

              @Override
              protected void onPause()
              {
                super.onPause();
                EngagementAgent.getInstance(this).endActivity();
              }
            }

<span data-ttu-id="a2c9a-146">Cette toohello très similaire exemple `EngagementActivity` classe et ses variantes, dont le code source est fourni dans hello `src` dossier.</span><span class="sxs-lookup"><span data-stu-id="a2c9a-146">This example very similiar toohello `EngagementActivity` class and its variants, whose source code is provided in hello `src` folder.</span></span>

## <a name="test"></a><span data-ttu-id="a2c9a-147">Test</span><span class="sxs-lookup"><span data-stu-id="a2c9a-147">Test</span></span>
<span data-ttu-id="a2c9a-148">Veuillez vérifier maintenant votre intégration en exécutant votre application mobile dans un émulateur ou un appareil et en vérifiant qu’il enregistre une session sur l’onglet de surveillance hello.</span><span class="sxs-lookup"><span data-stu-id="a2c9a-148">Now please verify your integration by running your mobile app in an emulator or device and verifying that it registers a session on hello Monitor tab.</span></span>

<span data-ttu-id="a2c9a-149">les sections suivantes Hello sont facultatifs.</span><span class="sxs-lookup"><span data-stu-id="a2c9a-149">hello next sections are optional.</span></span>

## <a name="location-reporting"></a><span data-ttu-id="a2c9a-150">Rapports d'emplacement</span><span class="sxs-lookup"><span data-stu-id="a2c9a-150">Location reporting</span></span>
<span data-ttu-id="a2c9a-151">Si vous souhaitez toobe emplacements signalé, vous devez tooadd quelques lignes de configuration (entre hello `<application>` et `</application>` balises).</span><span class="sxs-lookup"><span data-stu-id="a2c9a-151">If you want locations toobe reported, you need tooadd a few lines of configuration (between hello `<application>` and `</application>` tags).</span></span>

### <a name="lazy-area-location-reporting"></a><span data-ttu-id="a2c9a-152">Rapports d'emplacement de zone différé</span><span class="sxs-lookup"><span data-stu-id="a2c9a-152">Lazy area location reporting</span></span>
<span data-ttu-id="a2c9a-153">Signalisation différée de zone emplacement permet tooreport hello pays, la région et localité associés toodevices.</span><span class="sxs-lookup"><span data-stu-id="a2c9a-153">Lazy area location reporting allows tooreport hello country, region and locality associated toodevices.</span></span> <span data-ttu-id="a2c9a-154">Ce type de rapport d'emplacement utilise uniquement des emplacements réseau (basés sur l'ID cellulaire ou le Wi-Fi).</span><span class="sxs-lookup"><span data-stu-id="a2c9a-154">This type of location reporting only uses network locations (based on Cell ID or WIFI).</span></span> <span data-ttu-id="a2c9a-155">zone de Hello est signalée au maximum une fois par session.</span><span class="sxs-lookup"><span data-stu-id="a2c9a-155">hello device area is reported at most once per session.</span></span> <span data-ttu-id="a2c9a-156">Hello GPS n’est jamais utilisé, et par conséquent, ce type de rapport de l’emplacement a très peu (pas toosay aucune) impact sur la batterie de hello.</span><span class="sxs-lookup"><span data-stu-id="a2c9a-156">hello GPS is never used, and thus this type of location report has very few (not toosay no) impact on hello battery.</span></span>

<span data-ttu-id="a2c9a-157">Les zones signalés sont utilisés toocompute des statistiques géographique sur les utilisateurs, des sessions, des événements et des erreurs.</span><span class="sxs-lookup"><span data-stu-id="a2c9a-157">Reported areas are used toocompute geographic statistics about users, sessions, events and errors.</span></span> <span data-ttu-id="a2c9a-158">Elles peuvent également servir de critère dans les couvertures campagne.</span><span class="sxs-lookup"><span data-stu-id="a2c9a-158">They can also be used as criterion in Reach campaigns.</span></span>

<span data-ttu-id="a2c9a-159">emplacement de la zone différée tooenable reporting, vous pouvez le faire à l’aide de configuration hello mentionnée précédemment dans cette procédure :</span><span class="sxs-lookup"><span data-stu-id="a2c9a-159">tooenable lazy area location reporting, you can do it by using hello configuration previously mentioned in this procedure :</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setLazyAreaLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

<span data-ttu-id="a2c9a-160">Vous devez également hello tooadd suivant l’autorisation si manquant :</span><span class="sxs-lookup"><span data-stu-id="a2c9a-160">You also need tooadd hello following permission if missing:</span></span>

            <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>

<span data-ttu-id="a2c9a-161">Ou vous pouvez continuer à utiliser ``ACCESS_FINE_LOCATION`` si vous l’utilisez déjà dans votre application.</span><span class="sxs-lookup"><span data-stu-id="a2c9a-161">Or you can keep using ``ACCESS_FINE_LOCATION`` if you already use it in your application.</span></span>

### <a name="real-time-location-reporting"></a><span data-ttu-id="a2c9a-162">Rapports d'emplacement en temps réel</span><span class="sxs-lookup"><span data-stu-id="a2c9a-162">Real time location reporting</span></span>
<span data-ttu-id="a2c9a-163">Signalisation de l’emplacement en temps réel permet de latitude de hello tooreport et longitude associés toodevices.</span><span class="sxs-lookup"><span data-stu-id="a2c9a-163">Real time location reporting allows tooreport hello latitude and longitude associated toodevices.</span></span> <span data-ttu-id="a2c9a-164">Par défaut, ce type d’emplacement reporting utilise uniquement des emplacements réseau (basés sur l’ID de la cellule ou Wi-Fi), et hello reporting est uniquement active lorsque l’application hello s’exécute en premier plan (par exemple, lors d’une session).</span><span class="sxs-lookup"><span data-stu-id="a2c9a-164">By default, this type of location reporting only uses network locations (based on Cell ID or WIFI), and hello reporting is only active when hello application runs in foreground (i.e. during a session).</span></span>

<span data-ttu-id="a2c9a-165">Les emplacements en temps réel sont *pas* utilisé toocompute statistiques.</span><span class="sxs-lookup"><span data-stu-id="a2c9a-165">Real time locations are *NOT* used toocompute statistics.</span></span> <span data-ttu-id="a2c9a-166">Leur utilisation de hello tooallow de délimitation géographique en temps réel ne sert que \<portée-public-géorepérage\> critère dans les campagnes Reach.</span><span class="sxs-lookup"><span data-stu-id="a2c9a-166">Their only purpose is tooallow hello use of real time geo-fencing \<Reach-Audience-geofencing\> criterion in Reach campaigns.</span></span>

<span data-ttu-id="a2c9a-167">emplacement en temps réel du tooenable reporting, vous pouvez le faire à l’aide de configuration hello mentionnée précédemment dans cette procédure :</span><span class="sxs-lookup"><span data-stu-id="a2c9a-167">tooenable real time location reporting, you can do it by using hello configuration previously mentioned in this procedure :</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

<span data-ttu-id="a2c9a-168">Vous devez également hello tooadd suivant l’autorisation si manquant :</span><span class="sxs-lookup"><span data-stu-id="a2c9a-168">You also need tooadd hello following permission if missing:</span></span>

            <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>

<span data-ttu-id="a2c9a-169">Ou vous pouvez continuer à utiliser ``ACCESS_FINE_LOCATION`` si vous l’utilisez déjà dans votre application.</span><span class="sxs-lookup"><span data-stu-id="a2c9a-169">Or you can keep using ``ACCESS_FINE_LOCATION`` if you already use it in your application.</span></span>

#### <a name="gps-based-reporting"></a><span data-ttu-id="a2c9a-170">Rapports GPS</span><span class="sxs-lookup"><span data-stu-id="a2c9a-170">GPS based reporting</span></span>
<span data-ttu-id="a2c9a-171">Par défaut, le rapport d'emplacement en temps réel utilise uniquement des emplacements réseau.</span><span class="sxs-lookup"><span data-stu-id="a2c9a-171">By default, real time location reporting only uses network based locations.</span></span> <span data-ttu-id="a2c9a-172">utiliser hello tooenable GPS en fonction des emplacements (qui sont beaucoup plus précises), utilisez l’objet de configuration hello :</span><span class="sxs-lookup"><span data-stu-id="a2c9a-172">tooenable hello use of GPS based locations (which are far more precise), use hello configuration object:</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    engagementConfiguration.setFineRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

<span data-ttu-id="a2c9a-173">Vous devez également hello tooadd suivant l’autorisation si manquant :</span><span class="sxs-lookup"><span data-stu-id="a2c9a-173">You also need tooadd hello following permission if missing:</span></span>

            <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION"/>

#### <a name="background-reporting"></a><span data-ttu-id="a2c9a-174">Rapports en arrière-plan</span><span class="sxs-lookup"><span data-stu-id="a2c9a-174">Background reporting</span></span>
<span data-ttu-id="a2c9a-175">Par défaut, reporting en temps réel sur l’emplacement est uniquement active lorsque l’application hello s’exécute en premier plan (par exemple, lors d’une session).</span><span class="sxs-lookup"><span data-stu-id="a2c9a-175">By default, real time location reporting is only active when hello application runs in foreground (i.e. during a session).</span></span> <span data-ttu-id="a2c9a-176">hello tooenable reporting également en arrière-plan, utilisez hello configuration objet :</span><span class="sxs-lookup"><span data-stu-id="a2c9a-176">tooenable hello reporting also in background, use hello configuration object:</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    engagementConfiguration.setBackgroundRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

> [!NOTE]
> <span data-ttu-id="a2c9a-177">Lors de l’application hello s’exécute en arrière-plan, seuls les emplacements réseau sont signalées, même si vous avez activé hello GPS.</span><span class="sxs-lookup"><span data-stu-id="a2c9a-177">When hello application runs in background, only network based locations are reported, even if you enabled hello GPS.</span></span>
> 
> 

<span data-ttu-id="a2c9a-178">rapport d’emplacement Hello en arrière-plan sera arrêté si l’utilisateur de hello redémarre son appareil, vous pouvez ajouter cette toomake il redémarre automatiquement au moment du démarrage :</span><span class="sxs-lookup"><span data-stu-id="a2c9a-178">hello background location report will be stopped if hello user reboots its device, you can add this toomake it automatically restart at boot time:</span></span>

            <receiver android:name="com.microsoft.azure.engagement.EngagementLocationBootReceiver"
               android:exported="false">
               <intent-filter>
                  <action android:name="android.intent.action.BOOT_COMPLETED" />
               </intent-filter>
            </receiver>

<span data-ttu-id="a2c9a-179">Vous devez également hello tooadd suivant l’autorisation si manquant :</span><span class="sxs-lookup"><span data-stu-id="a2c9a-179">You also need tooadd hello following permission if missing:</span></span>

            <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />

### <a name="android-m-permissions"></a><span data-ttu-id="a2c9a-180">Autorisations Android M</span><span class="sxs-lookup"><span data-stu-id="a2c9a-180">Android M permissions</span></span>
<span data-ttu-id="a2c9a-181">À partir d’Android M, certaines autorisations sont gérées lors de l’exécution et nécessitent une approbation de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="a2c9a-181">Starting with Android M, some permissions are managed at runtime and needs user approval.</span></span>

<span data-ttu-id="a2c9a-182">autorisations d’exécution Hello seront désactivées par défaut pour les nouvelles installations de l’application si vous ciblez l’API Android de niveau 23.</span><span class="sxs-lookup"><span data-stu-id="a2c9a-182">hello runtime permissions will be turned off by default for new app installations if you target Android API level 23.</span></span> <span data-ttu-id="a2c9a-183">Sinon, elles seront activées par défaut.</span><span class="sxs-lookup"><span data-stu-id="a2c9a-183">Otherwise it will be turned on by default.</span></span>

<span data-ttu-id="a2c9a-184">utilisateur de Hello peut activer ou désactiver ces autorisations à partir du menu Paramètres de périphérique hello.</span><span class="sxs-lookup"><span data-stu-id="a2c9a-184">hello user can enable/disable those permissions from hello device settings menu.</span></span> <span data-ttu-id="a2c9a-185">Désactivation des autorisations à partir du menu système arrête les processus d’arrière-plan de l’application hello, ceci est un comportement du système et n’a aucun impact sur la capacité tooreceive par émission de données en arrière-plan.</span><span class="sxs-lookup"><span data-stu-id="a2c9a-185">Turning off permissions from system menu kills background processes of hello application, this is a system behavior and has no impact on ability tooreceive push in background.</span></span>

<span data-ttu-id="a2c9a-186">Dans le contexte de hello de Mobile Engagement, autorisations hello qui requièrent une approbation lors de l’exécution sont :</span><span class="sxs-lookup"><span data-stu-id="a2c9a-186">In hello context of Mobile Engagement, hello permissions that require approval at runtime are:</span></span>

* `ACCESS_COARSE_LOCATION`
* `ACCESS_FINE_LOCATION`
* <span data-ttu-id="a2c9a-187">`WRITE_EXTERNAL_STORAGE` (uniquement lors du ciblage de niveau d’API Android 23 pour cet élément)</span><span class="sxs-lookup"><span data-stu-id="a2c9a-187">`WRITE_EXTERNAL_STORAGE` (only when targeting Android API level 23 for this one)</span></span>

<span data-ttu-id="a2c9a-188">un stockage externe Hello est utilisé uniquement pour la fonctionnalité de vue d’ensemble de portée.</span><span class="sxs-lookup"><span data-stu-id="a2c9a-188">hello external storage is used only for Reach big picture feature.</span></span> <span data-ttu-id="a2c9a-189">Si vous trouvez demandant aux utilisateurs de cette autorisation toobe interruption de service, vous pouvez le supprimer si vous l’avez utilisé seulement pour Mobile Engagement, mais au coût hello de désactiver la fonctionnalité de vue d’ensemble.</span><span class="sxs-lookup"><span data-stu-id="a2c9a-189">If you find asking users this permission toobe disruptive, you can remove it if you used it only for Mobile Engagement but at hello cost of disabling big picture feature.</span></span>

<span data-ttu-id="a2c9a-190">Pour les fonctionnalités d’emplacement hello, vous devez demander toouser d’autorisations à l’aide d’une boîte de dialogue système standard.</span><span class="sxs-lookup"><span data-stu-id="a2c9a-190">For hello location features, you should request permissions toouser using a standard system dialog.</span></span> <span data-ttu-id="a2c9a-191">Si l’utilisateur de hello approuve, vous devez tootell ``EngagementAgent`` tootake modifier en compte en temps réel (modification de hello sinon sera traité hello suivant temps hello utilisateur lance hello application).</span><span class="sxs-lookup"><span data-stu-id="a2c9a-191">If hello user approves, you need tootell ``EngagementAgent`` tootake that change into account in real time (otherwise hello change will be processed hello next time hello user launches hello application).</span></span>

<span data-ttu-id="a2c9a-192">Voici une toouse d’exemple de code dans une activité de vos autorisations toorequest d’application et le résultat de hello vers l’avant si positif trop``EngagementAgent``:</span><span class="sxs-lookup"><span data-stu-id="a2c9a-192">Here is a code sample toouse in an activity of your application toorequest permissions and forward hello result if positive too``EngagementAgent``:</span></span>

    @Override
    public void onCreate(Bundle savedInstanceState)
    {
      /* Other code... */

      /* Request permissions */
      requestPermissions();
    }

    @TargetApi(Build.VERSION_CODES.M)
    private void requestPermissions()
    {
      /* Avoid crashing if not on Android M */
      if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.M)
      {
        /*
         * Request location permission, but this won't explain why it is needed toohello user.
         * hello standard Android documentation explains with more details how toodisplay a rationale activity tooexplain hello user why hello permission is needed in your application.
         * Putting COARSE vs FINE has no impact here, they are part of hello same group for runtime permission management.
         */
        if (checkSelfPermission(android.Manifest.permission.ACCESS_FINE_LOCATION) != PackageManager.PERMISSION_GRANTED)
          requestPermissions(new String[] { android.Manifest.permission.ACCESS_FINE_LOCATION }, 0);

        /* Only if you want tookeep features using external storage */
        if (checkSelfPermission(android.Manifest.permission.WRITE_EXTERNAL_STORAGE) != PackageManager.PERMISSION_GRANTED)
          requestPermissions(new String[] { android.Manifest.permission.WRITE_EXTERNAL_STORAGE }, 1);
      }
    }

    @Override
    public void onRequestPermissionsResult(int requestCode, String[] permissions, int[] grantResults)
    {
      /* Only a positive location permission update requires engagement agent refresh, hence hello request code matching from above function */
      if (requestCode == 0 && grantResults[0] == PackageManager.PERMISSION_GRANTED)
        getEngagementAgent().refreshPermissions();
    }

## <a name="advanced-reporting"></a><span data-ttu-id="a2c9a-193">Génération de rapports avancés</span><span class="sxs-lookup"><span data-stu-id="a2c9a-193">Advanced reporting</span></span>
<span data-ttu-id="a2c9a-194">Si vous le souhaitez, si vous souhaitez tooreport les événements d’application spécifique, les erreurs et les tâches, vous devez toouse hello Engagement API via les méthodes hello Hello `EngagementAgent` classe.</span><span class="sxs-lookup"><span data-stu-id="a2c9a-194">Optionally, if you want tooreport application specific events, errors and jobs, you need toouse hello Engagement API through hello methods of hello `EngagementAgent` class.</span></span> <span data-ttu-id="a2c9a-195">Un objet de cette classe permettre être récupérés en appelant hello `EngagementAgent.getInstance()` méthode statique.</span><span class="sxs-lookup"><span data-stu-id="a2c9a-195">An object of this class can be retreived by calling hello `EngagementAgent.getInstance()` static method.</span></span>

<span data-ttu-id="a2c9a-196">permet de toouse toutes les fonctionnalités avancées d’Engagement Hello Engagement API et est détaillée dans hello comment tooUse l’API d’Engagement sur Android (ainsi que dans la documentation technique de hello Hello `EngagementAgent` classe).</span><span class="sxs-lookup"><span data-stu-id="a2c9a-196">hello Engagement API allows toouse all of Engagement's advanced capabilities and is detailed in hello How tooUse the Engagement API on Android (as well as in hello technical documentation of hello `EngagementAgent` class).</span></span>

## <a name="advanced-configuration-in-androidmanifestxml"></a><span data-ttu-id="a2c9a-197">Configuration avancée (dans AndroidManifest.xml)</span><span class="sxs-lookup"><span data-stu-id="a2c9a-197">Advanced configuration (in AndroidManifest.xml)</span></span>
### <a name="wake-locks"></a><span data-ttu-id="a2c9a-198">Verrous d'activation</span><span class="sxs-lookup"><span data-stu-id="a2c9a-198">Wake locks</span></span>
<span data-ttu-id="a2c9a-199">Si vous souhaitez toobe assurer que les statistiques sont envoyées en temps réel lors de l’utilisation du Wi-Fi ou dans l’écran hello est désactivé, ajoutez hello suivant autorisation facultatif :</span><span class="sxs-lookup"><span data-stu-id="a2c9a-199">If you want toobe sure that statistics are sent in real time when using Wifi or when hello screen is off, add hello following optional permission:</span></span>

            <uses-permission android:name="android.permission.WAKE_LOCK"/>

### <a name="crash-report"></a><span data-ttu-id="a2c9a-200">Rapport d'incidents</span><span class="sxs-lookup"><span data-stu-id="a2c9a-200">Crash report</span></span>
<span data-ttu-id="a2c9a-201">Si vous souhaitez que les rapports d’incidents toodisable, ajoutez ceci (entre hello `<application>` et `</application>` balises) :</span><span class="sxs-lookup"><span data-stu-id="a2c9a-201">If you want toodisable crash reports, add this (between hello `<application>` and `</application>` tags):</span></span>

            <meta-data android:name="engagement:reportCrash" android:value="false"/>

### <a name="burst-threshold"></a><span data-ttu-id="a2c9a-202">Seuil du mode rafale</span><span class="sxs-lookup"><span data-stu-id="a2c9a-202">Burst threshold</span></span>
<span data-ttu-id="a2c9a-203">Par défaut, les rapports de service d’Engagement hello journaux en temps réel.</span><span class="sxs-lookup"><span data-stu-id="a2c9a-203">By default, hello Engagement service reports logs in real time.</span></span> <span data-ttu-id="a2c9a-204">Si votre application rapports journaux très fréquemment, il est mieux toobuffer hello journaux et tooreport à la fois à une base de temps réguliers (appelée hello « mode de croissance »).</span><span class="sxs-lookup"><span data-stu-id="a2c9a-204">If your application reports logs very frequently, it is better toobuffer hello logs and tooreport them all at once on a regular time base (this is called hello "burst mode").</span></span> <span data-ttu-id="a2c9a-205">toodo, ajoutez ceci (entre hello `<application>` et `</application>` balises) :</span><span class="sxs-lookup"><span data-stu-id="a2c9a-205">toodo so, add this (between hello `<application>` and `</application>` tags):</span></span>

            <meta-data android:name="engagement:burstThreshold" android:value="{interval between too bursts (in milliseconds)}"/>

<span data-ttu-id="a2c9a-206">Hello mode rafale légèrement augmenter la batterie de hello vie mais n’a un impact sur hello Engagement moniteur : toutes les sessions et les travaux seront arrondies toohello rafale seuil (par conséquent, les sessions et les travaux plus court que le seuil de croissance hello n’est pas forcément visible).</span><span class="sxs-lookup"><span data-stu-id="a2c9a-206">hello burst mode slightly increase hello battery life but has an impact on hello Engagement Monitor: all sessions and jobs duration will be rounded toohello burst threshold (thus, sessions and jobs shorter than hello burst threshold may not be visible).</span></span> <span data-ttu-id="a2c9a-207">Il est recommandé de toouse un seuil de croissance n’est plus à 30000 (30 s).</span><span class="sxs-lookup"><span data-stu-id="a2c9a-207">It is recommended toouse a burst threshold no longer than 30000 (30s).</span></span>

### <a name="session-timeout"></a><span data-ttu-id="a2c9a-208">Délai d'expiration de session</span><span class="sxs-lookup"><span data-stu-id="a2c9a-208">Session timeout</span></span>
<span data-ttu-id="a2c9a-209">Par défaut, une session est 10 s terminée après la fin de hello de sa dernière activité (qui se produit en appuyant sur le hello accueil ou sauvegardez la clé, par définition téléphone hello inactif ou passer à une autre application généralement).</span><span class="sxs-lookup"><span data-stu-id="a2c9a-209">By default, a session is ended 10s after hello end of its last activity (which usually occurs by pressing hello Home or Back key, by setting hello phone idle or by jumping into another application).</span></span> <span data-ttu-id="a2c9a-210">Il s’agit de tooavoid un fractionnement de session chaque utilisateur hello quitter et revenir toohello application très rapidement (qui peut se produire lorsqu’il chercher une image, vérifier une notification, etc..).</span><span class="sxs-lookup"><span data-stu-id="a2c9a-210">This is tooavoid a session split each time hello user exit and return toohello application very quickly (which can happen when he pick up a image, check a notification, etc.).</span></span> <span data-ttu-id="a2c9a-211">Vous souhaiterez toomodify ce paramètre.</span><span class="sxs-lookup"><span data-stu-id="a2c9a-211">You may want toomodify this parameter.</span></span> <span data-ttu-id="a2c9a-212">toodo, ajoutez ceci (entre hello `<application>` et `</application>` balises) :</span><span class="sxs-lookup"><span data-stu-id="a2c9a-212">toodo so, add this (between hello `<application>` and `</application>` tags):</span></span>

            <meta-data android:name="engagement:sessionTimeout" android:value="{session timeout (in milliseconds)}"/>

## <a name="disable-log-reporting"></a><span data-ttu-id="a2c9a-213">Désactiver les rapports de suivi</span><span class="sxs-lookup"><span data-stu-id="a2c9a-213">Disable log reporting</span></span>
### <a name="using-a-method-call"></a><span data-ttu-id="a2c9a-214">En appelant une méthode</span><span class="sxs-lookup"><span data-stu-id="a2c9a-214">Using a method call</span></span>
<span data-ttu-id="a2c9a-215">Si vous souhaitez toostop Engagement envoi de journaux, vous pouvez appeler :</span><span class="sxs-lookup"><span data-stu-id="a2c9a-215">If you want Engagement toostop sending logs, you can call:</span></span>

            EngagementAgent.getInstance(context).setEnabled(false);

<span data-ttu-id="a2c9a-216">Cet appel est persistant : il utilise un fichier de préférences partagées.</span><span class="sxs-lookup"><span data-stu-id="a2c9a-216">This call is persistent: it uses a shared preferences file.</span></span>

<span data-ttu-id="a2c9a-217">Si l’Engagement est active lorsque vous appelez cette fonction, peut prendre une minute pour hello service toostop.</span><span class="sxs-lookup"><span data-stu-id="a2c9a-217">If Engagement is active when you call this function, it may take 1 minute for hello service toostop.</span></span> <span data-ttu-id="a2c9a-218">Toutefois, il ne sera pas lancer service hello en hello tous les prochaine fois que vous lancez application hello.</span><span class="sxs-lookup"><span data-stu-id="a2c9a-218">However it won't launch hello service at all hello next time you launch hello application.</span></span>

<span data-ttu-id="a2c9a-219">Vous pouvez activer le journal de création de rapports en appelant hello même fonction avec `true`.</span><span class="sxs-lookup"><span data-stu-id="a2c9a-219">You can enable log reporting again by calling hello same function with `true`.</span></span>

### <a name="integration-in-your-own-preferenceactivity"></a><span data-ttu-id="a2c9a-220">Intégration dans votre propre `PreferenceActivity`</span><span class="sxs-lookup"><span data-stu-id="a2c9a-220">Integration in your own `PreferenceActivity`</span></span>
<span data-ttu-id="a2c9a-221">Au lieu d'appeler cette fonction, vous pouvez également intégrer ce paramètre directement dans votre `PreferenceActivity`.</span><span class="sxs-lookup"><span data-stu-id="a2c9a-221">Instead of calling this function, you can also integrate this setting directly in your existing `PreferenceActivity`.</span></span>

<span data-ttu-id="a2c9a-222">Vous pouvez configurer toouse Engagement vos préférences de fichier (avec le mode souhaité de hello) de hello `AndroidManifest.xml` de fichiers avec `application meta-data`:</span><span class="sxs-lookup"><span data-stu-id="a2c9a-222">You can configure Engagement toouse your preferences file (with hello desired mode) in hello `AndroidManifest.xml` file with `application meta-data`:</span></span>

* <span data-ttu-id="a2c9a-223">Hello `engagement:agent:settings:name` clé désigne toodefine utilisé hello du fichier de préférences partagées hello.</span><span class="sxs-lookup"><span data-stu-id="a2c9a-223">hello `engagement:agent:settings:name` key is used toodefine hello name of hello shared preferences file.</span></span>
* <span data-ttu-id="a2c9a-224">Hello `engagement:agent:settings:mode` clé est en mode de hello toodefine utilisé du fichier de préférences partagées hello, vous devez utiliser hello même mode comme dans votre `PreferenceActivity`.</span><span class="sxs-lookup"><span data-stu-id="a2c9a-224">hello `engagement:agent:settings:mode` key is used toodefine hello mode of hello shared preferences file, you should use hello same mode as in your `PreferenceActivity`.</span></span> <span data-ttu-id="a2c9a-225">mode de Hello doit être passé en tant que nombre : Si vous utilisez une combinaison d’indicateurs de constantes dans votre code, vérifiez la valeur totale de hello.</span><span class="sxs-lookup"><span data-stu-id="a2c9a-225">hello mode must be passed as a number: if you are using a combination of constant flags in your code, check hello total value.</span></span>

<span data-ttu-id="a2c9a-226">Engagement de toujours utiliser hello `engagement:key` booléenne clé dans le fichier de préférences de hello pour gérer ce paramètre.</span><span class="sxs-lookup"><span data-stu-id="a2c9a-226">Engagement always use hello `engagement:key` boolean key within hello preferences file for managing this setting.</span></span>

<span data-ttu-id="a2c9a-227">Hello selon l’exemple de `AndroidManifest.xml` affiche hello des valeurs par défaut :</span><span class="sxs-lookup"><span data-stu-id="a2c9a-227">hello following example of `AndroidManifest.xml` shows hello default values:</span></span>

            <application>
                [...]
                <meta-data
                  android:name="engagement:agent:settings:name"
                  android:value="engagement.agent" />
                <meta-data
                  android:name="engagement:agent:settings:mode"
                  android:value="0" />

<span data-ttu-id="a2c9a-228">Vous pouvez ensuite ajouter un `CheckBoxPreference` dans la disposition de préférence comme hello suivant un :</span><span class="sxs-lookup"><span data-stu-id="a2c9a-228">Then you can add a `CheckBoxPreference` in your preference layout like hello following one:</span></span>

            <CheckBoxPreference
              android:key="engagement:enabled"
              android:defaultValue="true"
              android:title="Use Engagement"
              android:summaryOn="Engagement is enabled."
              android:summaryOff="Engagement is disabled." />

<!-- URLs. -->
[Device API]: http://go.microsoft.com/?linkid=9876094
