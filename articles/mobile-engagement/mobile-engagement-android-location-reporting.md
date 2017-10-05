---
title: "Génération de rapports d’emplacement pour le SDK Azure Mobile Engagement pour Android"
description: "Décrit comment configurer la génération de rapports d’emplacement pour le SDK Azure Mobile Engagement pour Android"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 6cab5ed1-b767-46ac-9f0b-48a4e249d88c
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 08/12/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: 777d5719cce505b55dfb61c91dcac7e713b077a9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="location-reporting-for-azure-mobile-engagement-android-sdk"></a><span data-ttu-id="67a26-103">Génération de rapports d’emplacement pour le SDK Azure Mobile Engagement pour Android</span><span class="sxs-lookup"><span data-stu-id="67a26-103">Location Reporting for Azure Mobile Engagement Android SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="67a26-104">Android</span><span class="sxs-lookup"><span data-stu-id="67a26-104">Android</span></span>](mobile-engagement-android-integrate-engagement.md)
> 
> 

<span data-ttu-id="67a26-105">Cette rubrique explique comment générer des rapports d’emplacement pour votre application Android.</span><span class="sxs-lookup"><span data-stu-id="67a26-105">This topic describes how to do location reporting for your Android application.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="67a26-106">Composants requis</span><span class="sxs-lookup"><span data-stu-id="67a26-106">Prerequisites</span></span>
[!INCLUDE [Prereqs](../../includes/mobile-engagement-android-prereqs.md)]

## <a name="location-reporting"></a><span data-ttu-id="67a26-107">Rapports d'emplacement</span><span class="sxs-lookup"><span data-stu-id="67a26-107">Location reporting</span></span>
<span data-ttu-id="67a26-108">Si vous souhaitez créer des rapports concernant les emplacements, vous devez ajouter quelques lignes de configuration (entre les balises `<application>` et `</application>`).</span><span class="sxs-lookup"><span data-stu-id="67a26-108">If you want locations to be reported, you need to add a few lines of configuration (between the `<application>` and `</application>` tags).</span></span>

### <a name="lazy-area-location-reporting"></a><span data-ttu-id="67a26-109">Rapports d'emplacement de zone différé</span><span class="sxs-lookup"><span data-stu-id="67a26-109">Lazy area location reporting</span></span>
<span data-ttu-id="67a26-110">Le rapport d'emplacement de zone différé permet d'indiquer le pays, la région et la localité associés aux appareils.</span><span class="sxs-lookup"><span data-stu-id="67a26-110">Lazy area location reporting enables reporting the country, region, and locality associated with devices.</span></span> <span data-ttu-id="67a26-111">Ce type de rapport d'emplacement utilise uniquement des emplacements réseau (basés sur l'ID cellulaire ou le Wi-Fi).</span><span class="sxs-lookup"><span data-stu-id="67a26-111">This type of location reporting only uses network locations (based on Cell ID or WIFI).</span></span> <span data-ttu-id="67a26-112">La zone de l'appareil est signalée une fois maximum par session.</span><span class="sxs-lookup"><span data-stu-id="67a26-112">The device area is reported at most once per session.</span></span> <span data-ttu-id="67a26-113">Le GPS n'est jamais utilisé, ce type de rapport d'emplacement a donc peu d'impact sur la batterie.</span><span class="sxs-lookup"><span data-stu-id="67a26-113">The GPS is never used, and thus this type of location report has low impact on the battery.</span></span>

<span data-ttu-id="67a26-114">Les zones signalées sont utilisées pour calculer des statistiques géographiques relatives aux utilisateurs, aux sessions, aux événements et aux erreurs.</span><span class="sxs-lookup"><span data-stu-id="67a26-114">Reported areas are used to compute geographic statistics about users, sessions, events, and errors.</span></span> <span data-ttu-id="67a26-115">Elles peuvent également servir de critère dans les couvertures campagne.</span><span class="sxs-lookup"><span data-stu-id="67a26-115">They can also be used as criterion in Reach campaigns.</span></span>

<span data-ttu-id="67a26-116">Vous activez le service de localisation de zone différé à l’aide de la configuration précédemment mentionnée dans cette procédure :</span><span class="sxs-lookup"><span data-stu-id="67a26-116">You enable lazy area location reporting by using the configuration previously mentioned in this procedure:</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setLazyAreaLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

<span data-ttu-id="67a26-117">Vous devez également spécifier une autorisation d’emplacement.</span><span class="sxs-lookup"><span data-stu-id="67a26-117">You also need to specify a location permission.</span></span> <span data-ttu-id="67a26-118">Ce code utilise l’autorisation ``COARSE`` :</span><span class="sxs-lookup"><span data-stu-id="67a26-118">This code uses ``COARSE`` permission:</span></span>

    <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>

<span data-ttu-id="67a26-119">Si votre application l’exige, vous pouvez utiliser ``ACCESS_FINE_LOCATION`` à la place.</span><span class="sxs-lookup"><span data-stu-id="67a26-119">If your app requires it, you can use ``ACCESS_FINE_LOCATION`` instead.</span></span>

### <a name="real-time-location-reporting"></a><span data-ttu-id="67a26-120">Rapports d'emplacement en temps réel</span><span class="sxs-lookup"><span data-stu-id="67a26-120">Real-time location reporting</span></span>
<span data-ttu-id="67a26-121">Le rapport d'emplacement en temps réel permet de signaler la latitude et la longitude associées aux appareils.</span><span class="sxs-lookup"><span data-stu-id="67a26-121">Real-time location reporting enables reporting the latitude and longitude associated with devices.</span></span> <span data-ttu-id="67a26-122">Par défaut, ce type de rapport d'emplacement utilise uniquement des emplacements réseau, basés sur l'ID cellulaire ou le Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="67a26-122">By default, this type of location reporting only uses network locations, based on Cell ID or WIFI.</span></span> <span data-ttu-id="67a26-123">Le rapport est uniquement actif quand l'application s'exécute en premier plan (c'est-à-dire pendant une session).</span><span class="sxs-lookup"><span data-stu-id="67a26-123">The reporting is only active when the application runs in foreground (for example, during a session).</span></span>

<span data-ttu-id="67a26-124">Les emplacements en temps réel ne sont *PAS* utilisés pour calculer des statistiques.</span><span class="sxs-lookup"><span data-stu-id="67a26-124">Real-time locations are *NOT* used to compute statistics.</span></span> <span data-ttu-id="67a26-125">Leur seul but est de permettre l’utilisation d’un critère de géorepérage en temps réel \<portée-public-gardiennage virtuel\> dans les campagnes Reach.</span><span class="sxs-lookup"><span data-stu-id="67a26-125">Their only purpose is to allow the use of real-time geo-fencing \<Reach-Audience-geofencing\> criterion in Reach campaigns.</span></span>

<span data-ttu-id="67a26-126">Pour activer les rapports d’emplacement en temps réel, ajoutez une ligne de code à l’endroit où vous définissez la chaîne de connexion Engagement dans l’activité du programme de lancement.</span><span class="sxs-lookup"><span data-stu-id="67a26-126">To enable real-time location reporting, add a line of code to where you set the Engagement connection string in the launcher activity.</span></span> <span data-ttu-id="67a26-127">Le résultat se présente comme suit :</span><span class="sxs-lookup"><span data-stu-id="67a26-127">The result looks like the following:</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

        You also need to specify a location permission. This code uses ``COARSE`` permission:

            <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>

        If your app requires it, you can use ``ACCESS_FINE_LOCATION`` instead.

#### <a name="gps-based-reporting"></a><span data-ttu-id="67a26-128">Rapports GPS</span><span class="sxs-lookup"><span data-stu-id="67a26-128">GPS based reporting</span></span>
<span data-ttu-id="67a26-129">Par défaut, le rapport d'emplacement en temps réel utilise uniquement des emplacements réseau.</span><span class="sxs-lookup"><span data-stu-id="67a26-129">By default, real-time location reporting only uses network-based locations.</span></span> <span data-ttu-id="67a26-130">Pour activer l’utilisation des localisations GPS (beaucoup plus précises), utilisez l’objet de configuration suivant :</span><span class="sxs-lookup"><span data-stu-id="67a26-130">To enable the use of GPS-based locations, which are far more precise, use the configuration object:</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    engagementConfiguration.setFineRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

<span data-ttu-id="67a26-131">Vous devez également ajouter l'autorisation suivante si elle manque :</span><span class="sxs-lookup"><span data-stu-id="67a26-131">You also need to add the following permission if missing:</span></span>

    <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION"/>

#### <a name="background-reporting"></a><span data-ttu-id="67a26-132">Rapports en arrière-plan</span><span class="sxs-lookup"><span data-stu-id="67a26-132">Background reporting</span></span>
<span data-ttu-id="67a26-133">Par défaut, le rapport d'emplacement en temps réel est uniquement actif quand l'application s'exécute en premier plan (pendant une session par exemple).</span><span class="sxs-lookup"><span data-stu-id="67a26-133">By default, real-time location reporting is only active when the application runs in foreground (for example, during a session).</span></span> <span data-ttu-id="67a26-134">Pour activer la génération de rapports également en arrière-plan, utilisez l’objet de configuration suivant :</span><span class="sxs-lookup"><span data-stu-id="67a26-134">To enable the reporting also in background, use this configuration object:</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    engagementConfiguration.setBackgroundRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

> [!NOTE]
> <span data-ttu-id="67a26-135">Quand l'application s'exécute en arrière-plan, seuls les emplacements réseau sont signalés, même si vous avez activé le GPS.</span><span class="sxs-lookup"><span data-stu-id="67a26-135">When the application runs in background, only network-based locations are reported, even if you enabled the GPS.</span></span>
> 
> 

<span data-ttu-id="67a26-136">Si l’utilisateur redémarre son appareil, le rapport d’emplacement en arrière-plan est arrêté.</span><span class="sxs-lookup"><span data-stu-id="67a26-136">If the user reboots their device, the background location report is stopped.</span></span> <span data-ttu-id="67a26-137">Pour qu’il redémarre automatiquement au démarrage, ajoutez ce code.</span><span class="sxs-lookup"><span data-stu-id="67a26-137">To make it automatically restart at boot time, add this code.</span></span>

    <receiver android:name="com.microsoft.azure.engagement.EngagementLocationBootReceiver"
           android:exported="false">
        <intent-filter>
            <action android:name="android.intent.action.BOOT_COMPLETED" />
        </intent-filter>
    </receiver>

<span data-ttu-id="67a26-138">Vous devez également ajouter l'autorisation suivante si elle manque :</span><span class="sxs-lookup"><span data-stu-id="67a26-138">You also need to add the following permission if missing:</span></span>

    <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />

## <a name="android-m-permissions"></a><span data-ttu-id="67a26-139">Autorisations Android M</span><span class="sxs-lookup"><span data-stu-id="67a26-139">Android M permissions</span></span>
<span data-ttu-id="67a26-140">À partir d’Android M, certaines autorisations sont gérées lors de l’exécution et nécessitent une approbation de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="67a26-140">Starting with Android M, some permissions are managed at runtime and need user approval.</span></span>

<span data-ttu-id="67a26-141">Si vous ciblez le niveau d’API Android 23, les autorisations d’exécution sont désactivées par défaut pour les nouvelles installations d’application.</span><span class="sxs-lookup"><span data-stu-id="67a26-141">If you target Android API level 23, the runtime permissions are turned off by default for new app installations.</span></span> <span data-ttu-id="67a26-142">Sinon, elles sont activées par défaut.</span><span class="sxs-lookup"><span data-stu-id="67a26-142">Otherwise they are turned on by default.</span></span>

<span data-ttu-id="67a26-143">Vous pouvez activer/désactiver ces autorisations dans le menu des paramètres de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="67a26-143">You can enable/disable those permissions from the device settings menu.</span></span> <span data-ttu-id="67a26-144">La désactivation des autorisations à partir du menu système arrête les processus en arrière-plan de l’application. Il s’agit d’un comportement du système qui n’a aucune incidence sur la capacité à recevoir des notifications en arrière-plan.</span><span class="sxs-lookup"><span data-stu-id="67a26-144">Turning off permissions from the system menu kills the background processes of the application, which is a system behavior, and has no impact on ability to receive push in background.</span></span>

<span data-ttu-id="67a26-145">Dans le cadre de la génération de rapports d’emplacement Mobile Engagement, les autorisations qui requièrent une approbation au moment de l’exécution sont :</span><span class="sxs-lookup"><span data-stu-id="67a26-145">In the context of Mobile Engagement location reporting, the permissions that require approval at runtime are:</span></span>

* `ACCESS_COARSE_LOCATION`
* `ACCESS_FINE_LOCATION`

<span data-ttu-id="67a26-146">Demandez les autorisations à l’utilisateur via une boîte de dialogue système standard.</span><span class="sxs-lookup"><span data-stu-id="67a26-146">Request permissions from the user using a standard system dialog.</span></span> <span data-ttu-id="67a26-147">Si l’utilisateur approuve, indiquez à ``EngagementAgent`` de prendre en compte cette modification en temps réel.</span><span class="sxs-lookup"><span data-stu-id="67a26-147">If the user approves, tell ``EngagementAgent`` to take that change into account in real-time.</span></span> <span data-ttu-id="67a26-148">Sinon, la modification est traitée la prochaine fois que l’utilisateur lance l’application.</span><span class="sxs-lookup"><span data-stu-id="67a26-148">Otherwise the change is processed the next time the user launches the application.</span></span>

<span data-ttu-id="67a26-149">Voici un exemple de code à utiliser dans une activité de votre application pour demander des autorisations et transmettre le résultat, si positif, à ``EngagementAgent``:</span><span class="sxs-lookup"><span data-stu-id="67a26-149">Here is a code sample to use in an activity of your application to request permissions and forward the result if positive to ``EngagementAgent``:</span></span>

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
         * Request location permission, but this doesn't explain why it is needed to the user.
         * The standard Android documentation explains with more details how to display a rationale activity to explain the user why the permission is needed in your application.
         * Putting COARSE vs FINE has no impact here, they are part of the same group for runtime permission management.
         */
        if (checkSelfPermission(android.Manifest.permission.ACCESS_FINE_LOCATION) != PackageManager.PERMISSION_GRANTED)
          requestPermissions(new String[] { android.Manifest.permission.ACCESS_FINE_LOCATION }, 0);

      }
    }

    @Override
    public void onRequestPermissionsResult(int requestCode, String[] permissions, int[] grantResults)
    {
      /* Only a positive location permission update requires engagement agent refresh, hence the request code matching from above function */
      if (requestCode == 0 && grantResults[0] == PackageManager.PERMISSION_GRANTED)
        getEngagementAgent().refreshPermissions();
    }
