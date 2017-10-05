---
title: "Intégration du SDK Android d'Azure Mobile Engagement"
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
ms.openlocfilehash: 35bd92e52b7a02f58620a03156902f9f91be57ae
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-integrate-engagement-on-android"></a><span data-ttu-id="25b48-103">Comment intégrer Engagement à Android</span><span class="sxs-lookup"><span data-stu-id="25b48-103">How to Integrate Engagement on Android</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="25b48-104">Windows Universal</span><span class="sxs-lookup"><span data-stu-id="25b48-104">Windows Universal</span></span>](mobile-engagement-windows-store-integrate-engagement.md)
> * [<span data-ttu-id="25b48-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="25b48-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md)
> * [<span data-ttu-id="25b48-106">iOS</span><span class="sxs-lookup"><span data-stu-id="25b48-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md)
> * [<span data-ttu-id="25b48-107">Android</span><span class="sxs-lookup"><span data-stu-id="25b48-107">Android</span></span>](mobile-engagement-android-integrate-engagement.md)
> 
> 

<span data-ttu-id="25b48-108">Cette procédure décrit la méthode la plus simple pour activer les fonctions d'analyse et de surveillance dans votre application Android.</span><span class="sxs-lookup"><span data-stu-id="25b48-108">This procedure describes the simplest way to activate Engagement's Analytics and Monitoring functions in your Android application.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="25b48-109">Le niveau minimum de l'API SDK Android doit être égal ou supérieur à 10 (Android 2.3.3 ou version ultérieure).</span><span class="sxs-lookup"><span data-stu-id="25b48-109">Your minimum Android SDK API level must be 10 or higher (Android 2.3.3 or higher).</span></span>
> 
> 

<span data-ttu-id="25b48-110">Les étapes suivantes suffisent à activer la création de journaux nécessaires au calcul de l'ensemble des statistiques concernant les utilisateurs, les sessions, les activités, les incidents et les éléments techniques.</span><span class="sxs-lookup"><span data-stu-id="25b48-110">The following steps are enough to activates the report of logs needed to compute all statistics regarding Users, Sessions, Activities, Crashes and Technicals.</span></span> <span data-ttu-id="25b48-111">Le rapport des journaux nécessaire pour calculer d'autres statistiques telles que les événements, les erreurs et les tâches, doit être généré manuellement à l'aide de l'API Engagement (consultez la rubrique [Utilisation de l'API de balisage Mobile Engagement avancé dans votre Android](mobile-engagement-android-use-engagement-api.md) étant donné que ces statistiques dépendent de l'application.</span><span class="sxs-lookup"><span data-stu-id="25b48-111">The report of logs needed to compute other statistics like Events, Errors and Jobs must be done manually using the Engagement API (see [How to use the advanced Mobile Engagement tagging API in your Android](mobile-engagement-android-use-engagement-api.md) since these statistics are application dependent.</span></span>

## <a name="embed-the-engagement-sdk-and-service-into-your-android-project"></a><span data-ttu-id="25b48-112">Intégrer le SDK et le service Engagement à un projet Android</span><span class="sxs-lookup"><span data-stu-id="25b48-112">Embed the Engagement SDK and service into your Android project</span></span>
<span data-ttu-id="25b48-113">Téléchargez le Kit de développement logiciel (SDK) Android [ici](https://aka.ms/vq9mfn) Récupérez `mobile-engagement-VERSION.jar` et placez-les dans le dossier `libs` de votre projet Android (créez le dossier de la bibliothèque si celui-ci n’existe pas).</span><span class="sxs-lookup"><span data-stu-id="25b48-113">Download the Android SDK from [here](https://aka.ms/vq9mfn) Get `mobile-engagement-VERSION.jar` and put them into the `libs` folder of your Android project (create the libs folder if it does not exist yet).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="25b48-114">Si vous générez votre package d'application avec ProGuard, vous devez conserver certaines classes.</span><span class="sxs-lookup"><span data-stu-id="25b48-114">If you build your application package with ProGuard, you need to keep some classes.</span></span> <span data-ttu-id="25b48-115">Vous pouvez utiliser l'extrait de configuration suivant :</span><span class="sxs-lookup"><span data-stu-id="25b48-115">You can use the following configuration snippet:</span></span>
> 
> <span data-ttu-id="25b48-116">-keep public class * extends android.os.IInterface -keep class com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity$EngagementReachContentJS {</span><span class="sxs-lookup"><span data-stu-id="25b48-116">-keep public class * extends android.os.IInterface -keep class com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity$EngagementReachContentJS {</span></span>
> 
> <span data-ttu-id="25b48-117"><methods>; }</span><span class="sxs-lookup"><span data-stu-id="25b48-117"><methods>; }</span></span>
> 
> 

<span data-ttu-id="25b48-118">Spécifiez votre chaîne de connexion Engagement en appelant la méthode suivante dans l'activité du programme de lancement :</span><span class="sxs-lookup"><span data-stu-id="25b48-118">Specify your Engagement connection string by calling the following method in the launcher activity:</span></span>

            EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
            engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
            EngagementAgent.getInstance(this).init(engagementConfiguration);

<span data-ttu-id="25b48-119">La chaîne de connexion de votre application est affichée sur le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="25b48-119">The connection string for your application is displayed on Azure Portal.</span></span>

* <span data-ttu-id="25b48-120">Si ce n'est pas le cas, ajoutez les autorisations Android suivantes (avant la balise `<application>`) :</span><span class="sxs-lookup"><span data-stu-id="25b48-120">If missing, add the following Android permissions (before the `<application>` tag):</span></span>
  
          <uses-permission android:name="android.permission.INTERNET"/>
          <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
* <span data-ttu-id="25b48-121">Ajoutez la section suivante (entre les balises `<application>` et `</application>`) :</span><span class="sxs-lookup"><span data-stu-id="25b48-121">Add the following section (between the `<application>` and `</application>` tags):</span></span>
  
          <service
            android:name="com.microsoft.azure.engagement.service.EngagementService"
            android:exported="false"
            android:label="<Your application name>Service"
            android:process=":Engagement"/>
* <span data-ttu-id="25b48-122">Remplacez `<Your application name>` par le nom de votre application.</span><span class="sxs-lookup"><span data-stu-id="25b48-122">Change `<Your application name>` by the name of your application.</span></span>

> [!TIP]
> <span data-ttu-id="25b48-123">La clé `android:label` vous permet de choisir le nom du service Engagement tel qu'il apparaîtra aux utilisateurs finaux dans l'écran Services en cours d'exécution de leur téléphone.</span><span class="sxs-lookup"><span data-stu-id="25b48-123">The `android:label` attribute allows you to choose the name of the Engagement service as it will appear to the end-users in the "Running services" screen of their phone.</span></span> <span data-ttu-id="25b48-124">Il est recommandé de définir cet attribut sur `"<Your application name>Service"` (par exemple `"AcmeFunGameService"`).</span><span class="sxs-lookup"><span data-stu-id="25b48-124">It is recommended to set this attribute to `"<Your application name>Service"` (e.g. `"AcmeFunGameService"`).</span></span>
> 
> 

<span data-ttu-id="25b48-125">La spécification de l'attribut `android:process` permet au service Engagement d'être exécuté dans le cadre de son propre processus (l'exécution d'Engagement dans le même processus que votre application peut rendre votre thread principal/d'interface utilisateur moins réactif).</span><span class="sxs-lookup"><span data-stu-id="25b48-125">Specifying the `android:process` attribute ensures that the Engagement service will run in its own process (running Engagement in the same process as your application will make your main/UI thread potentially less responsive).</span></span>

> [!NOTE]
> <span data-ttu-id="25b48-126">Tout code que vous placez dans `Application.onCreate()` et autres rappels d'application sera exécuté pour l'ensemble des processus de votre application, y compris le service Engagement.</span><span class="sxs-lookup"><span data-stu-id="25b48-126">Any code you place in `Application.onCreate()` and other application callbacks will be run for all your application's processes, including the Engagement service.</span></span> <span data-ttu-id="25b48-127">Cela peut avoir des effets indésirables (tels que des allocations de mémoire et des threads inutiles dans le processus Engagement, ou des récepteurs ou services de diffusion en double).</span><span class="sxs-lookup"><span data-stu-id="25b48-127">It may have unwanted side effects (like unneeded memory allocations and threads in the Engagement's process, duplicate broadcast receivers or services).</span></span>
> 
> 

<span data-ttu-id="25b48-128">Si vous remplacez `Application.onCreate()`, il est recommandé d'ajouter l'extrait de code suivant au début de la fonction `Application.onCreate()` :</span><span class="sxs-lookup"><span data-stu-id="25b48-128">If you override `Application.onCreate()`, it's recommended to add the following code snippet at the beginning of your `Application.onCreate()` function:</span></span>

             public void onCreate()
             {
               if (EngagementAgentUtils.isInDedicatedEngagementProcess(this))
                 return;

               ... Your code...
             }

<span data-ttu-id="25b48-129">Vous pouvez faire la même chose pour `Application.onTerminate()`, `Application.onLowMemory()` et `Application.onConfigurationChanged(...)`.</span><span class="sxs-lookup"><span data-stu-id="25b48-129">You can do the same thing for `Application.onTerminate()`, `Application.onLowMemory()` and `Application.onConfigurationChanged(...)`.</span></span>

<span data-ttu-id="25b48-130">Vous pouvez également étendre `EngagementApplication` au lieu d'étendre `Application` : le rappel `Application.onCreate()` effectue la vérification du processus et appelle `Application.onApplicationProcessCreate()` uniquement si le processus actuel n'est pas celui qui héberge le service Engagement. Les mêmes règles s'appliquent pour les autres rappels.</span><span class="sxs-lookup"><span data-stu-id="25b48-130">You can also extend `EngagementApplication` instead of extending `Application`: the callback `Application.onCreate()` does the process check and calls `Application.onApplicationProcessCreate()` only if the current process is not the one hosting the Engagement service, the same rules apply for the other callbacks.</span></span>

## <a name="basic-reporting"></a><span data-ttu-id="25b48-131">Génération de rapports de base</span><span class="sxs-lookup"><span data-stu-id="25b48-131">Basic reporting</span></span>
### <a name="recommended-method-overload-your-activity-classes"></a><span data-ttu-id="25b48-132">Méthode recommandée : surchargez vos classes `Activity`</span><span class="sxs-lookup"><span data-stu-id="25b48-132">Recommended method: overload your `Activity` classes</span></span>
<span data-ttu-id="25b48-133">Pour activer la création d'un rapport à partir de tous les journaux nécessaires à Engagement pour calculer les statistiques relatives aux utilisateurs, aux sessions, aux activités, aux incidents et aux éléments techniques, il vous suffit de faire hériter toutes les sous-classes `*Activity` des classes `Engagement*Activity` correspondantes (par exemple, si votre activité héritée étend `ListActivity`, assurez-vous qu'elle étend `EngagementListActivity`).</span><span class="sxs-lookup"><span data-stu-id="25b48-133">In order to activate the report of all the logs required by Engagement to compute Users, Sessions, Activities, Crashes and Technical statistics, you just have to make all your `*Activity` sub-classes inherit from the corresponding `Engagement*Activity` classes (e.g. if your legacy activity extends `ListActivity`, make it extends `EngagementListActivity`).</span></span>

<span data-ttu-id="25b48-134">**Sans Engagement :**</span><span class="sxs-lookup"><span data-stu-id="25b48-134">**Without Engagement :**</span></span>

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

<span data-ttu-id="25b48-135">**Avec Engagement :**</span><span class="sxs-lookup"><span data-stu-id="25b48-135">**With Engagement :**</span></span>

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
> <span data-ttu-id="25b48-136">Lorsque vous utilisez `EngagementListActivity` ou `EngagementExpandableListActivity`, assurez-vous que tout appel à `requestWindowFeature(...);` est effectué avant l'appel à `super.onCreate(...);`. Dans le cas contraire, un incident se produira.</span><span class="sxs-lookup"><span data-stu-id="25b48-136">When using `EngagementListActivity` or `EngagementExpandableListActivity`, make sure any call to `requestWindowFeature(...);` is made before the call to `super.onCreate(...);`, otherwise a crash will occur.</span></span>
> 
> 

<span data-ttu-id="25b48-137">Vous trouverez ces classes dans le dossier `src`. Vous pourrez les copier dans votre projet.</span><span class="sxs-lookup"><span data-stu-id="25b48-137">You can find these classes in the `src` folder, and can copy them into your project.</span></span> <span data-ttu-id="25b48-138">Les classes se trouvent également dans **JavaDoc**.</span><span class="sxs-lookup"><span data-stu-id="25b48-138">The classes are also in the **JavaDoc**.</span></span>

### <a name="alternate-method-call-startactivity-and-endactivity-manually"></a><span data-ttu-id="25b48-139">Méthode alternative : appelez `startActivity()` et `endActivity()` manuellement</span><span class="sxs-lookup"><span data-stu-id="25b48-139">Alternate method: call `startActivity()` and `endActivity()` manually</span></span>
<span data-ttu-id="25b48-140">Si vous ne pouvez pas ou ne voulez pas surcharger vos classes `Activity`, vous pouvez démarrer et terminer vos activités en appelant les méthodes `EngagementAgent` directement.</span><span class="sxs-lookup"><span data-stu-id="25b48-140">If you cannot or do not want to overload your `Activity` classes, you can instead start and end your activities by calling `EngagementAgent`'s methods directly.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="25b48-141">Le Kit de développement logiciel (SDK) Android n'appelle jamais la méthode `endActivity()`, même quand l'application est fermée (sur Android, les applications ne sont en fait jamais fermées).</span><span class="sxs-lookup"><span data-stu-id="25b48-141">The Android SDK never calls the `endActivity()` method, even when the application is closed (on Android, applications are actually never closed).</span></span> <span data-ttu-id="25b48-142">Il est donc *FORTEMENT* recommandé d’appeler la méthode `startActivity()` dans le rappel `onResume` de *TOUTES* vos activités, et la méthode `endActivity()` dans le rappel `onPause()` de *TOUTES* vos activités.</span><span class="sxs-lookup"><span data-stu-id="25b48-142">Thus, it is *HIGHLY* recommended to call the `startActivity()` method in the `onResume` callback of *ALL* your activities, and the `endActivity()` method in the `onPause()` callback of *ALL* your activities.</span></span> <span data-ttu-id="25b48-143">Il s'agit de la seule façon d'empêcher la fuite de sessions.</span><span class="sxs-lookup"><span data-stu-id="25b48-143">This is the only way to be sure that sessions will not be leaked.</span></span> <span data-ttu-id="25b48-144">Dans le cas d'une fuite de session, le service Engagement n'est jamais déconnecté du serveur principal d'Engagement (étant donné que le service reste connecté tant qu'une session est en cours).</span><span class="sxs-lookup"><span data-stu-id="25b48-144">If a session is leaked, the Engagement service will never disconnect from the Engagement backend (since the service stays connected as long as a session is pending).</span></span>
> 
> 

<span data-ttu-id="25b48-145">Voici un exemple :</span><span class="sxs-lookup"><span data-stu-id="25b48-145">Here is an example:</span></span>

            public class MyActivity extends Some3rdPartyActivity
            {
              @Override
              protected void onResume()
              {
                super.onResume();
                String activityNameOnEngagement = EngagementAgentUtils.buildEngagementActivityName(getClass()); // Uses short class name and removes "Activity" at the end.
                EngagementAgent.getInstance(this).startActivity(this, activityNameOnEngagement, null);
              }

              @Override
              protected void onPause()
              {
                super.onPause();
                EngagementAgent.getInstance(this).endActivity();
              }
            }

<span data-ttu-id="25b48-146">Cet exemple est très similaire à la classe `EngagementActivity` et à ses variantes, dont le code source est fourni dans le dossier `src`.</span><span class="sxs-lookup"><span data-stu-id="25b48-146">This example very similiar to the `EngagementActivity` class and its variants, whose source code is provided in the `src` folder.</span></span>

## <a name="test"></a><span data-ttu-id="25b48-147">Test</span><span class="sxs-lookup"><span data-stu-id="25b48-147">Test</span></span>
<span data-ttu-id="25b48-148">Maintenant, vérifiez votre intégration en exécutant votre application mobile dans un émulateur ou sur un appareil et en vérifiant qu'elle inscrit une session sur l'onglet Surveiller.</span><span class="sxs-lookup"><span data-stu-id="25b48-148">Now please verify your integration by running your mobile app in an emulator or device and verifying that it registers a session on the Monitor tab.</span></span>

<span data-ttu-id="25b48-149">Les sections suivantes sont facultatives.</span><span class="sxs-lookup"><span data-stu-id="25b48-149">The next sections are optional.</span></span>

## <a name="location-reporting"></a><span data-ttu-id="25b48-150">Rapports d'emplacement</span><span class="sxs-lookup"><span data-stu-id="25b48-150">Location reporting</span></span>
<span data-ttu-id="25b48-151">Si vous souhaitez créer des rapports concernant les emplacements, vous devez ajouter quelques lignes de configuration (entre les balises `<application>` et `</application>`).</span><span class="sxs-lookup"><span data-stu-id="25b48-151">If you want locations to be reported, you need to add a few lines of configuration (between the `<application>` and `</application>` tags).</span></span>

### <a name="lazy-area-location-reporting"></a><span data-ttu-id="25b48-152">Rapports d'emplacement de zone différé</span><span class="sxs-lookup"><span data-stu-id="25b48-152">Lazy area location reporting</span></span>
<span data-ttu-id="25b48-153">Le rapport d'emplacement de zone différé permet d'indiquer le pays, la région et la localité associés aux appareils.</span><span class="sxs-lookup"><span data-stu-id="25b48-153">Lazy area location reporting allows to report the country, region and locality associated to devices.</span></span> <span data-ttu-id="25b48-154">Ce type de rapport d'emplacement utilise uniquement des emplacements réseau (basés sur l'ID cellulaire ou le Wi-Fi).</span><span class="sxs-lookup"><span data-stu-id="25b48-154">This type of location reporting only uses network locations (based on Cell ID or WIFI).</span></span> <span data-ttu-id="25b48-155">La zone de l'appareil est signalée une fois maximum par session.</span><span class="sxs-lookup"><span data-stu-id="25b48-155">The device area is reported at most once per session.</span></span> <span data-ttu-id="25b48-156">Le GPS n'est jamais utilisé, ce type de rapport d'emplacement a donc très peu d'impact (pour ne pas dire aucun) sur la batterie.</span><span class="sxs-lookup"><span data-stu-id="25b48-156">The GPS is never used, and thus this type of location report has very few (not to say no) impact on the battery.</span></span>

<span data-ttu-id="25b48-157">Les zones signalées sont utilisées pour calculer des statistiques géographiques relatives aux utilisateurs, aux sessions, aux événements et aux erreurs.</span><span class="sxs-lookup"><span data-stu-id="25b48-157">Reported areas are used to compute geographic statistics about users, sessions, events and errors.</span></span> <span data-ttu-id="25b48-158">Elles peuvent également servir de critère dans les couvertures campagne.</span><span class="sxs-lookup"><span data-stu-id="25b48-158">They can also be used as criterion in Reach campaigns.</span></span>

<span data-ttu-id="25b48-159">Pour activer le service de localisation de zone différé, vous pouvez utiliser la configuration précédemment mentionnée dans cette procédure :</span><span class="sxs-lookup"><span data-stu-id="25b48-159">To enable lazy area location reporting, you can do it by using the configuration previously mentioned in this procedure :</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setLazyAreaLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

<span data-ttu-id="25b48-160">Vous devez également ajouter l'autorisation suivante si elle manque :</span><span class="sxs-lookup"><span data-stu-id="25b48-160">You also need to add the following permission if missing:</span></span>

            <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>

<span data-ttu-id="25b48-161">Ou vous pouvez continuer à utiliser ``ACCESS_FINE_LOCATION`` si vous l’utilisez déjà dans votre application.</span><span class="sxs-lookup"><span data-stu-id="25b48-161">Or you can keep using ``ACCESS_FINE_LOCATION`` if you already use it in your application.</span></span>

### <a name="real-time-location-reporting"></a><span data-ttu-id="25b48-162">Rapports d'emplacement en temps réel</span><span class="sxs-lookup"><span data-stu-id="25b48-162">Real time location reporting</span></span>
<span data-ttu-id="25b48-163">Le rapport d'emplacement en temps réel permet de signaler la latitude et la longitude associées aux appareils.</span><span class="sxs-lookup"><span data-stu-id="25b48-163">Real time location reporting allows to report the latitude and longitude associated to devices.</span></span> <span data-ttu-id="25b48-164">Par défaut, ce type de rapport d'emplacement utilise uniquement des emplacements réseau (basés sur l'ID cellulaire ou le Wi-Fi) et le rapport n'est actif que lorsque l'application s'exécute en premier plan (c'est-à-dire pendant une session).</span><span class="sxs-lookup"><span data-stu-id="25b48-164">By default, this type of location reporting only uses network locations (based on Cell ID or WIFI), and the reporting is only active when the application runs in foreground (i.e. during a session).</span></span>

<span data-ttu-id="25b48-165">Les emplacements en temps réel ne sont *PAS* utilisés pour calculer des statistiques.</span><span class="sxs-lookup"><span data-stu-id="25b48-165">Real time locations are *NOT* used to compute statistics.</span></span> <span data-ttu-id="25b48-166">Leur seul but est de permettre l’utilisation d’un critère de géorepérage en temps réel \<Reach-Audience-geofencing\> dans les campagnes Reach.</span><span class="sxs-lookup"><span data-stu-id="25b48-166">Their only purpose is to allow the use of real time geo-fencing \<Reach-Audience-geofencing\> criterion in Reach campaigns.</span></span>

<span data-ttu-id="25b48-167">Pour activer le service de localisation de zone en temps réel, vous pouvez utiliser la configuration précédemment mentionnée dans cette procédure :</span><span class="sxs-lookup"><span data-stu-id="25b48-167">To enable real time location reporting, you can do it by using the configuration previously mentioned in this procedure :</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

<span data-ttu-id="25b48-168">Vous devez également ajouter l'autorisation suivante si elle manque :</span><span class="sxs-lookup"><span data-stu-id="25b48-168">You also need to add the following permission if missing:</span></span>

            <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>

<span data-ttu-id="25b48-169">Ou vous pouvez continuer à utiliser ``ACCESS_FINE_LOCATION`` si vous l’utilisez déjà dans votre application.</span><span class="sxs-lookup"><span data-stu-id="25b48-169">Or you can keep using ``ACCESS_FINE_LOCATION`` if you already use it in your application.</span></span>

#### <a name="gps-based-reporting"></a><span data-ttu-id="25b48-170">Rapports GPS</span><span class="sxs-lookup"><span data-stu-id="25b48-170">GPS based reporting</span></span>
<span data-ttu-id="25b48-171">Par défaut, le rapport d'emplacement en temps réel utilise uniquement des emplacements réseau.</span><span class="sxs-lookup"><span data-stu-id="25b48-171">By default, real time location reporting only uses network based locations.</span></span> <span data-ttu-id="25b48-172">Pour activer l’utilisation des localisations GPS (beaucoup plus précises), utilisez l’objet de configuration suivant :</span><span class="sxs-lookup"><span data-stu-id="25b48-172">To enable the use of GPS based locations (which are far more precise), use the configuration object:</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    engagementConfiguration.setFineRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

<span data-ttu-id="25b48-173">Vous devez également ajouter l'autorisation suivante si elle manque :</span><span class="sxs-lookup"><span data-stu-id="25b48-173">You also need to add the following permission if missing:</span></span>

            <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION"/>

#### <a name="background-reporting"></a><span data-ttu-id="25b48-174">Rapports en arrière-plan</span><span class="sxs-lookup"><span data-stu-id="25b48-174">Background reporting</span></span>
<span data-ttu-id="25b48-175">Par défaut, le rapport d'emplacement en temps réel est uniquement actif quand l'application s'exécute en premier plan (c'est-à-dire pendant une session).</span><span class="sxs-lookup"><span data-stu-id="25b48-175">By default, real time location reporting is only active when the application runs in foreground (i.e. during a session).</span></span> <span data-ttu-id="25b48-176">Pour activer la création de rapports également en arrière-plan, utilisez l’objet de configuration suivant :</span><span class="sxs-lookup"><span data-stu-id="25b48-176">To enable the reporting also in background, use the configuration object:</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    engagementConfiguration.setBackgroundRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

> [!NOTE]
> <span data-ttu-id="25b48-177">Quand l'application s'exécute en arrière-plan, seuls les emplacements réseau sont signalés, même si vous avez activé le GPS.</span><span class="sxs-lookup"><span data-stu-id="25b48-177">When the application runs in background, only network based locations are reported, even if you enabled the GPS.</span></span>
> 
> 

<span data-ttu-id="25b48-178">Le rapport d'emplacement en arrière-plan sera arrêté si l'utilisateur redémarre son appareil. Pour configurer un redémarrage automatique au moment du démarrage, ajoutez ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="25b48-178">The background location report will be stopped if the user reboots its device, you can add this to make it automatically restart at boot time:</span></span>

            <receiver android:name="com.microsoft.azure.engagement.EngagementLocationBootReceiver"
               android:exported="false">
               <intent-filter>
                  <action android:name="android.intent.action.BOOT_COMPLETED" />
               </intent-filter>
            </receiver>

<span data-ttu-id="25b48-179">Vous devez également ajouter l'autorisation suivante si elle manque :</span><span class="sxs-lookup"><span data-stu-id="25b48-179">You also need to add the following permission if missing:</span></span>

            <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />

### <a name="android-m-permissions"></a><span data-ttu-id="25b48-180">Autorisations Android M</span><span class="sxs-lookup"><span data-stu-id="25b48-180">Android M permissions</span></span>
<span data-ttu-id="25b48-181">À partir d’Android M, certaines autorisations sont gérées lors de l’exécution et nécessitent une approbation de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="25b48-181">Starting with Android M, some permissions are managed at runtime and needs user approval.</span></span>

<span data-ttu-id="25b48-182">Les autorisations d’exécution seront désactivées par défaut pour les nouvelles installations d’application si vous ciblez le niveau d’API Android 23.</span><span class="sxs-lookup"><span data-stu-id="25b48-182">The runtime permissions will be turned off by default for new app installations if you target Android API level 23.</span></span> <span data-ttu-id="25b48-183">Sinon, elles seront activées par défaut.</span><span class="sxs-lookup"><span data-stu-id="25b48-183">Otherwise it will be turned on by default.</span></span>

<span data-ttu-id="25b48-184">L’utilisateur peut activer/désactiver ces autorisations dans le menu des paramètres de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="25b48-184">The user can enable/disable those permissions from the device settings menu.</span></span> <span data-ttu-id="25b48-185">La désactivation des autorisations à partir du menu système arrête les processus en arrière-plan de l’application. Il s’agit d’un comportement du système qui n’a aucune incidence sur la capacité à recevoir des notifications en arrière-plan.</span><span class="sxs-lookup"><span data-stu-id="25b48-185">Turning off permissions from system menu kills background processes of the application, this is a system behavior and has no impact on ability to receive push in background.</span></span>

<span data-ttu-id="25b48-186">Dans le cadre de la stratégie Mobile Engagement, les autorisations qui requièrent une approbation au moment de l’exécution sont :</span><span class="sxs-lookup"><span data-stu-id="25b48-186">In the context of Mobile Engagement, the permissions that require approval at runtime are:</span></span>

* `ACCESS_COARSE_LOCATION`
* `ACCESS_FINE_LOCATION`
* <span data-ttu-id="25b48-187">`WRITE_EXTERNAL_STORAGE` (uniquement lors du ciblage de niveau d’API Android 23 pour cet élément)</span><span class="sxs-lookup"><span data-stu-id="25b48-187">`WRITE_EXTERNAL_STORAGE` (only when targeting Android API level 23 for this one)</span></span>

<span data-ttu-id="25b48-188">Le stockage externe est utilisé uniquement pour la fonctionnalité Reach BigPicture.</span><span class="sxs-lookup"><span data-stu-id="25b48-188">The external storage is used only for Reach big picture feature.</span></span> <span data-ttu-id="25b48-189">Si vous estimez que demander cette autorisation aux utilisateurs est un élément trop perturbateur, vous pouvez le supprimer si vous l’avez utilisé uniquement pour Mobile Engagement, au détriment de la fonctionnalité BigPicture qui sera alors désactivée.</span><span class="sxs-lookup"><span data-stu-id="25b48-189">If you find asking users this permission to be disruptive, you can remove it if you used it only for Mobile Engagement but at the cost of disabling big picture feature.</span></span>

<span data-ttu-id="25b48-190">Pour les fonctionnalités de localisation, vous devez demander les autorisations à l’utilisateur via une boîte de dialogue système standard.</span><span class="sxs-lookup"><span data-stu-id="25b48-190">For the location features, you should request permissions to user using a standard system dialog.</span></span> <span data-ttu-id="25b48-191">Si l’utilisateur approuve, vous devez indiquer à ``EngagementAgent`` de prendre enc ompte cette modification en temps réel (sinon, la modification sera traitée au prochain lancement de l’application par l’utilisateur).</span><span class="sxs-lookup"><span data-stu-id="25b48-191">If the user approves, you need to tell ``EngagementAgent`` to take that change into account in real time (otherwise the change will be processed the next time the user launches the application).</span></span>

<span data-ttu-id="25b48-192">Voici un exemple de code à utiliser dans une activité de votre application pour demander des autorisations et transmettre le résultat, si positif, à ``EngagementAgent``:</span><span class="sxs-lookup"><span data-stu-id="25b48-192">Here is a code sample to use in an activity of your application to request permissions and forward the result if positive to ``EngagementAgent``:</span></span>

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
         * Request location permission, but this won't explain why it is needed to the user.
         * The standard Android documentation explains with more details how to display a rationale activity to explain the user why the permission is needed in your application.
         * Putting COARSE vs FINE has no impact here, they are part of the same group for runtime permission management.
         */
        if (checkSelfPermission(android.Manifest.permission.ACCESS_FINE_LOCATION) != PackageManager.PERMISSION_GRANTED)
          requestPermissions(new String[] { android.Manifest.permission.ACCESS_FINE_LOCATION }, 0);

        /* Only if you want to keep features using external storage */
        if (checkSelfPermission(android.Manifest.permission.WRITE_EXTERNAL_STORAGE) != PackageManager.PERMISSION_GRANTED)
          requestPermissions(new String[] { android.Manifest.permission.WRITE_EXTERNAL_STORAGE }, 1);
      }
    }

    @Override
    public void onRequestPermissionsResult(int requestCode, String[] permissions, int[] grantResults)
    {
      /* Only a positive location permission update requires engagement agent refresh, hence the request code matching from above function */
      if (requestCode == 0 && grantResults[0] == PackageManager.PERMISSION_GRANTED)
        getEngagementAgent().refreshPermissions();
    }

## <a name="advanced-reporting"></a><span data-ttu-id="25b48-193">Génération de rapports avancés</span><span class="sxs-lookup"><span data-stu-id="25b48-193">Advanced reporting</span></span>
<span data-ttu-id="25b48-194">Éventuellement, si vous voulez signaler des événements, des erreurs et des tâches de l'application spécifiques, vous devez utiliser l'API Engagement par le biais des méthodes de la classe `EngagementAgent` .</span><span class="sxs-lookup"><span data-stu-id="25b48-194">Optionally, if you want to report application specific events, errors and jobs, you need to use the Engagement API through the methods of the `EngagementAgent` class.</span></span> <span data-ttu-id="25b48-195">Un objet de cette classe peut être récupéré en appelant la méthode statique `EngagementAgent.getInstance()` .</span><span class="sxs-lookup"><span data-stu-id="25b48-195">An object of this class can be retreived by calling the `EngagementAgent.getInstance()` static method.</span></span>

<span data-ttu-id="25b48-196">L'API d'Engagement permet d'utiliser toutes les fonctionnalités avancées d'Engagement. Elle est détaillée dans la procédure d'utilisation de l'API d'Engagement sur Android (ainsi que dans la documentation technique de la classe `EngagementAgent`).</span><span class="sxs-lookup"><span data-stu-id="25b48-196">The Engagement API allows to use all of Engagement's advanced capabilities and is detailed in the How to Use the Engagement API on Android (as well as in the technical documentation of the `EngagementAgent` class).</span></span>

## <a name="advanced-configuration-in-androidmanifestxml"></a><span data-ttu-id="25b48-197">Configuration avancée (dans AndroidManifest.xml)</span><span class="sxs-lookup"><span data-stu-id="25b48-197">Advanced configuration (in AndroidManifest.xml)</span></span>
### <a name="wake-locks"></a><span data-ttu-id="25b48-198">Verrous d'activation</span><span class="sxs-lookup"><span data-stu-id="25b48-198">Wake locks</span></span>
<span data-ttu-id="25b48-199">Si vous voulez être sûr que les statistiques soient envoyées en temps réel quand vous utilisez le Wi-Fi ou quand l'écran est désactivé, ajoutez l'autorisation facultative suivante :</span><span class="sxs-lookup"><span data-stu-id="25b48-199">If you want to be sure that statistics are sent in real time when using Wifi or when the screen is off, add the following optional permission:</span></span>

            <uses-permission android:name="android.permission.WAKE_LOCK"/>

### <a name="crash-report"></a><span data-ttu-id="25b48-200">Rapport d'incidents</span><span class="sxs-lookup"><span data-stu-id="25b48-200">Crash report</span></span>
<span data-ttu-id="25b48-201">Si vous voulez désactiver les rapports d'incidents, ajoutez ce qui suit (entre les balises `<application>` et `</application>`) :</span><span class="sxs-lookup"><span data-stu-id="25b48-201">If you want to disable crash reports, add this (between the `<application>` and `</application>` tags):</span></span>

            <meta-data android:name="engagement:reportCrash" android:value="false"/>

### <a name="burst-threshold"></a><span data-ttu-id="25b48-202">Seuil du mode rafale</span><span class="sxs-lookup"><span data-stu-id="25b48-202">Burst threshold</span></span>
<span data-ttu-id="25b48-203">Par défaut, le service Engagement génère des journaux en temps réel.</span><span class="sxs-lookup"><span data-stu-id="25b48-203">By default, the Engagement service reports logs in real time.</span></span> <span data-ttu-id="25b48-204">Si votre application crée des journaux très fréquemment, il est préférable de les mettre en mémoire tampon et de les rassembler dans un rapport à intervalle régulier (on parle dans ce cas de « mode rafale »).</span><span class="sxs-lookup"><span data-stu-id="25b48-204">If your application reports logs very frequently, it is better to buffer the logs and to report them all at once on a regular time base (this is called the "burst mode").</span></span> <span data-ttu-id="25b48-205">Pour cela, ajoutez ce qui suit (entre les balises `<application>` et `</application>`) :</span><span class="sxs-lookup"><span data-stu-id="25b48-205">To do so, add this (between the `<application>` and `</application>` tags):</span></span>

            <meta-data android:name="engagement:burstThreshold" android:value="{interval between too bursts (in milliseconds)}"/>

<span data-ttu-id="25b48-206">Le mode rafale accroît légèrement l'autonomie de la batterie, mais il affecte aussi Engagement Monitor. En effet, la durée des sessions et des tâches est arrondie au seuil de rafale (les sessions et les tâches plus courtes que le seuil de rafale ne sont donc pas visibles).</span><span class="sxs-lookup"><span data-stu-id="25b48-206">The burst mode slightly increase the battery life but has an impact on the Engagement Monitor: all sessions and jobs duration will be rounded to the burst threshold (thus, sessions and jobs shorter than the burst threshold may not be visible).</span></span> <span data-ttu-id="25b48-207">Il est recommandé d'utiliser un seuil de rafale inférieur à 30 000 (30 s).</span><span class="sxs-lookup"><span data-stu-id="25b48-207">It is recommended to use a burst threshold no longer than 30000 (30s).</span></span>

### <a name="session-timeout"></a><span data-ttu-id="25b48-208">Délai d'expiration de session</span><span class="sxs-lookup"><span data-stu-id="25b48-208">Session timeout</span></span>
<span data-ttu-id="25b48-209">Par défaut, une session est terminée dans les 10 s qui suivent la fin de la dernière activité (ce qui se produit généralement quand vous appuyez sur la touche Accueil ou Retour, quand vous mettez le téléphone en mode veille ou quand vous passez à une autre application).</span><span class="sxs-lookup"><span data-stu-id="25b48-209">By default, a session is ended 10s after the end of its last activity (which usually occurs by pressing the Home or Back key, by setting the phone idle or by jumping into another application).</span></span> <span data-ttu-id="25b48-210">Cela permet d'éviter un fractionnement de session chaque fois que l'utilisateur quitte une application puis la rouvre très rapidement (ce qui peut se produire quand il ouvre une image ou une notification, etc.).</span><span class="sxs-lookup"><span data-stu-id="25b48-210">This is to avoid a session split each time the user exit and return to the application very quickly (which can happen when he pick up a image, check a notification, etc.).</span></span> <span data-ttu-id="25b48-211">Il est possible de modifier ce paramètre.</span><span class="sxs-lookup"><span data-stu-id="25b48-211">You may want to modify this parameter.</span></span> <span data-ttu-id="25b48-212">Pour cela, ajoutez ce qui suit (entre les balises `<application>` et `</application>`) :</span><span class="sxs-lookup"><span data-stu-id="25b48-212">To do so, add this (between the `<application>` and `</application>` tags):</span></span>

            <meta-data android:name="engagement:sessionTimeout" android:value="{session timeout (in milliseconds)}"/>

## <a name="disable-log-reporting"></a><span data-ttu-id="25b48-213">Désactiver les rapports de suivi</span><span class="sxs-lookup"><span data-stu-id="25b48-213">Disable log reporting</span></span>
### <a name="using-a-method-call"></a><span data-ttu-id="25b48-214">En appelant une méthode</span><span class="sxs-lookup"><span data-stu-id="25b48-214">Using a method call</span></span>
<span data-ttu-id="25b48-215">Si vous voulez qu'Engagement arrête d'envoyer des journaux, vous pouvez appeler la méthode suivante :</span><span class="sxs-lookup"><span data-stu-id="25b48-215">If you want Engagement to stop sending logs, you can call:</span></span>

            EngagementAgent.getInstance(context).setEnabled(false);

<span data-ttu-id="25b48-216">Cet appel est persistant : il utilise un fichier de préférences partagées.</span><span class="sxs-lookup"><span data-stu-id="25b48-216">This call is persistent: it uses a shared preferences file.</span></span>

<span data-ttu-id="25b48-217">Si le contrat est actif quand vous appelez cette fonction, l'arrêt du service peut prendre une minute.</span><span class="sxs-lookup"><span data-stu-id="25b48-217">If Engagement is active when you call this function, it may take 1 minute for the service to stop.</span></span> <span data-ttu-id="25b48-218">Toutefois, le service ne sera pas lancé la prochaine fois que vous lancerez l'application.</span><span class="sxs-lookup"><span data-stu-id="25b48-218">However it won't launch the service at all the next time you launch the application.</span></span>

<span data-ttu-id="25b48-219">Vous pouvez activer à nouveau la création de rapports de journaux en appelant la même fonction avec `true`.</span><span class="sxs-lookup"><span data-stu-id="25b48-219">You can enable log reporting again by calling the same function with `true`.</span></span>

### <a name="integration-in-your-own-preferenceactivity"></a><span data-ttu-id="25b48-220">Intégration dans votre propre `PreferenceActivity`</span><span class="sxs-lookup"><span data-stu-id="25b48-220">Integration in your own `PreferenceActivity`</span></span>
<span data-ttu-id="25b48-221">Au lieu d'appeler cette fonction, vous pouvez également intégrer ce paramètre directement dans votre `PreferenceActivity`.</span><span class="sxs-lookup"><span data-stu-id="25b48-221">Instead of calling this function, you can also integrate this setting directly in your existing `PreferenceActivity`.</span></span>

<span data-ttu-id="25b48-222">Vous pouvez configurer Engagement pour qu'il utilise votre fichier de préférences (avec le mode souhaité) dans le fichier `AndroidManifest.xml` avec `application meta-data` :</span><span class="sxs-lookup"><span data-stu-id="25b48-222">You can configure Engagement to use your preferences file (with the desired mode) in the `AndroidManifest.xml` file with `application meta-data`:</span></span>

* <span data-ttu-id="25b48-223">La clé `engagement:agent:settings:name` est utilisée pour définir le nom du fichier de préférences partagées.</span><span class="sxs-lookup"><span data-stu-id="25b48-223">The `engagement:agent:settings:name` key is used to define the name of the shared preferences file.</span></span>
* <span data-ttu-id="25b48-224">La clé `engagement:agent:settings:mode` est utilisée pour définir le mode du fichier de préférences partagées. Vous devez utiliser le même mode que dans votre `PreferenceActivity`.</span><span class="sxs-lookup"><span data-stu-id="25b48-224">The `engagement:agent:settings:mode` key is used to define the mode of the shared preferences file, you should use the same mode as in your `PreferenceActivity`.</span></span> <span data-ttu-id="25b48-225">Le mode doit être passé comme un nombre. Si vous utilisez une combinaison d'indicateurs de constante dans votre code, vérifiez la valeur totale.</span><span class="sxs-lookup"><span data-stu-id="25b48-225">The mode must be passed as a number: if you are using a combination of constant flags in your code, check the total value.</span></span>

<span data-ttu-id="25b48-226">Engagement utilise toujours la clé booléenne `engagement:key` dans le fichier de préférences pour la gestion de ce paramètre.</span><span class="sxs-lookup"><span data-stu-id="25b48-226">Engagement always use the `engagement:key` boolean key within the preferences file for managing this setting.</span></span>

<span data-ttu-id="25b48-227">L'exemple de suivant de `AndroidManifest.xml` montre les valeurs par défaut :</span><span class="sxs-lookup"><span data-stu-id="25b48-227">The following example of `AndroidManifest.xml` shows the default values:</span></span>

            <application>
                [...]
                <meta-data
                  android:name="engagement:agent:settings:name"
                  android:value="engagement.agent" />
                <meta-data
                  android:name="engagement:agent:settings:mode"
                  android:value="0" />

<span data-ttu-id="25b48-228">Vous pouvez ensuite ajouter un `CheckBoxPreference` dans votre disposition préférée, comme celle qui suit :</span><span class="sxs-lookup"><span data-stu-id="25b48-228">Then you can add a `CheckBoxPreference` in your preference layout like the following one:</span></span>

            <CheckBoxPreference
              android:key="engagement:enabled"
              android:defaultValue="true"
              android:title="Use Engagement"
              android:summaryOn="Engagement is enabled."
              android:summaryOff="Engagement is disabled." />

<!-- URLs. -->
[Device API]: http://go.microsoft.com/?linkid=9876094
