---
title: aaaLocation Reporting pour Azure Mobile Engagement Android SDK
description: "Décrit comment emplacement tooconfigure reporting pour Azure Mobile Engagement Android SDK"
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
ms.openlocfilehash: c2cb097df2a77bee2d56ffe9509dc116548db408
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="location-reporting-for-azure-mobile-engagement-android-sdk"></a><span data-ttu-id="95d86-103">Génération de rapports d’emplacement pour le SDK Azure Mobile Engagement pour Android</span><span class="sxs-lookup"><span data-stu-id="95d86-103">Location Reporting for Azure Mobile Engagement Android SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="95d86-104">Android</span><span class="sxs-lookup"><span data-stu-id="95d86-104">Android</span></span>](mobile-engagement-android-integrate-engagement.md)
> 
> 

<span data-ttu-id="95d86-105">Cette rubrique décrit comment emplacement toodo reporting pour votre application Android.</span><span class="sxs-lookup"><span data-stu-id="95d86-105">This topic describes how toodo location reporting for your Android application.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="95d86-106">Composants requis</span><span class="sxs-lookup"><span data-stu-id="95d86-106">Prerequisites</span></span>
[!INCLUDE [Prereqs](../../includes/mobile-engagement-android-prereqs.md)]

## <a name="location-reporting"></a><span data-ttu-id="95d86-107">Rapports d'emplacement</span><span class="sxs-lookup"><span data-stu-id="95d86-107">Location reporting</span></span>
<span data-ttu-id="95d86-108">Si vous souhaitez toobe emplacements signalé, vous devez tooadd quelques lignes de configuration (entre hello `<application>` et `</application>` balises).</span><span class="sxs-lookup"><span data-stu-id="95d86-108">If you want locations toobe reported, you need tooadd a few lines of configuration (between hello `<application>` and `</application>` tags).</span></span>

### <a name="lazy-area-location-reporting"></a><span data-ttu-id="95d86-109">Rapports d'emplacement de zone différé</span><span class="sxs-lookup"><span data-stu-id="95d86-109">Lazy area location reporting</span></span>
<span data-ttu-id="95d86-110">Signalisation différée de zone emplacement permet de pays hello déclarant, région et localité associées aux périphériques.</span><span class="sxs-lookup"><span data-stu-id="95d86-110">Lazy area location reporting enables reporting hello country, region, and locality associated with devices.</span></span> <span data-ttu-id="95d86-111">Ce type de rapport d'emplacement utilise uniquement des emplacements réseau (basés sur l'ID cellulaire ou le Wi-Fi).</span><span class="sxs-lookup"><span data-stu-id="95d86-111">This type of location reporting only uses network locations (based on Cell ID or WIFI).</span></span> <span data-ttu-id="95d86-112">zone de Hello est signalée au maximum une fois par session.</span><span class="sxs-lookup"><span data-stu-id="95d86-112">hello device area is reported at most once per session.</span></span> <span data-ttu-id="95d86-113">Hello GPS n’est jamais utilisé, et par conséquent, ce type de rapport d’emplacement a un faible impact sur la batterie de hello.</span><span class="sxs-lookup"><span data-stu-id="95d86-113">hello GPS is never used, and thus this type of location report has low impact on hello battery.</span></span>

<span data-ttu-id="95d86-114">Les zones signalées sont géographique de toocompute utilisé des statistiques sur les utilisateurs, les sessions, les événements et les erreurs.</span><span class="sxs-lookup"><span data-stu-id="95d86-114">Reported areas are used toocompute geographic statistics about users, sessions, events, and errors.</span></span> <span data-ttu-id="95d86-115">Elles peuvent également servir de critère dans les couvertures campagne.</span><span class="sxs-lookup"><span data-stu-id="95d86-115">They can also be used as criterion in Reach campaigns.</span></span>

<span data-ttu-id="95d86-116">Vous activez d’emplacement de la zone différée reporting à l’aide de configuration hello mentionnée précédemment dans cette procédure :</span><span class="sxs-lookup"><span data-stu-id="95d86-116">You enable lazy area location reporting by using hello configuration previously mentioned in this procedure:</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setLazyAreaLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

<span data-ttu-id="95d86-117">Vous devez également toospecify une autorisation de l’emplacement.</span><span class="sxs-lookup"><span data-stu-id="95d86-117">You also need toospecify a location permission.</span></span> <span data-ttu-id="95d86-118">Ce code utilise l’autorisation ``COARSE`` :</span><span class="sxs-lookup"><span data-stu-id="95d86-118">This code uses ``COARSE`` permission:</span></span>

    <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>

<span data-ttu-id="95d86-119">Si votre application l’exige, vous pouvez utiliser ``ACCESS_FINE_LOCATION`` à la place.</span><span class="sxs-lookup"><span data-stu-id="95d86-119">If your app requires it, you can use ``ACCESS_FINE_LOCATION`` instead.</span></span>

### <a name="real-time-location-reporting"></a><span data-ttu-id="95d86-120">Rapports d'emplacement en temps réel</span><span class="sxs-lookup"><span data-stu-id="95d86-120">Real-time location reporting</span></span>
<span data-ttu-id="95d86-121">Signalisation de l’emplacement en temps réel permet de création de rapports latitude de hello et la longitude associées aux périphériques.</span><span class="sxs-lookup"><span data-stu-id="95d86-121">Real-time location reporting enables reporting hello latitude and longitude associated with devices.</span></span> <span data-ttu-id="95d86-122">Par défaut, ce type de rapport d'emplacement utilise uniquement des emplacements réseau, basés sur l'ID cellulaire ou le Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="95d86-122">By default, this type of location reporting only uses network locations, based on Cell ID or WIFI.</span></span> <span data-ttu-id="95d86-123">Hello reporting est uniquement active lorsque l’application hello s’exécute en premier plan (par exemple, pendant une session).</span><span class="sxs-lookup"><span data-stu-id="95d86-123">hello reporting is only active when hello application runs in foreground (for example, during a session).</span></span>

<span data-ttu-id="95d86-124">Emplacements en temps réel sont *pas* utilisé toocompute statistiques.</span><span class="sxs-lookup"><span data-stu-id="95d86-124">Real-time locations are *NOT* used toocompute statistics.</span></span> <span data-ttu-id="95d86-125">Leur utilisation de hello tooallow de délimitation géographique en temps réel ne sert que \<portée-public-géorepérage\> critère dans les campagnes Reach.</span><span class="sxs-lookup"><span data-stu-id="95d86-125">Their only purpose is tooallow hello use of real-time geo-fencing \<Reach-Audience-geofencing\> criterion in Reach campaigns.</span></span>

<span data-ttu-id="95d86-126">emplacement en temps réel de tooenable création de rapports, ajoutez une ligne de code toowhere permet de chaîne de connexion d’Engagement hello dans l’activité de lanceur hello.</span><span class="sxs-lookup"><span data-stu-id="95d86-126">tooenable real-time location reporting, add a line of code toowhere you set hello Engagement connection string in hello launcher activity.</span></span> <span data-ttu-id="95d86-127">résultat de Hello ressemble à hello suivantes :</span><span class="sxs-lookup"><span data-stu-id="95d86-127">hello result looks like hello following:</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

        You also need toospecify a location permission. This code uses ``COARSE`` permission:

            <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>

        If your app requires it, you can use ``ACCESS_FINE_LOCATION`` instead.

#### <a name="gps-based-reporting"></a><span data-ttu-id="95d86-128">Rapports GPS</span><span class="sxs-lookup"><span data-stu-id="95d86-128">GPS based reporting</span></span>
<span data-ttu-id="95d86-129">Par défaut, le rapport d'emplacement en temps réel utilise uniquement des emplacements réseau.</span><span class="sxs-lookup"><span data-stu-id="95d86-129">By default, real-time location reporting only uses network-based locations.</span></span> <span data-ttu-id="95d86-130">utiliser hello tooenable emplacements GPS, qui sont beaucoup plus précises, utiliser l’objet de configuration de hello :</span><span class="sxs-lookup"><span data-stu-id="95d86-130">tooenable hello use of GPS-based locations, which are far more precise, use hello configuration object:</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    engagementConfiguration.setFineRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

<span data-ttu-id="95d86-131">Vous devez également hello tooadd suivant l’autorisation si manquant :</span><span class="sxs-lookup"><span data-stu-id="95d86-131">You also need tooadd hello following permission if missing:</span></span>

    <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION"/>

#### <a name="background-reporting"></a><span data-ttu-id="95d86-132">Rapports en arrière-plan</span><span class="sxs-lookup"><span data-stu-id="95d86-132">Background reporting</span></span>
<span data-ttu-id="95d86-133">Par défaut, reporting sur l’emplacement en temps réel est uniquement active lorsque l’application hello s’exécute en premier plan (par exemple, pendant une session).</span><span class="sxs-lookup"><span data-stu-id="95d86-133">By default, real-time location reporting is only active when hello application runs in foreground (for example, during a session).</span></span> <span data-ttu-id="95d86-134">hello tooenable reporting également en arrière-plan, utilisez cet objet de configuration :</span><span class="sxs-lookup"><span data-stu-id="95d86-134">tooenable hello reporting also in background, use this configuration object:</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    engagementConfiguration.setBackgroundRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

> [!NOTE]
> <span data-ttu-id="95d86-135">Lors de l’application hello s’exécute en arrière-plan, seuls les emplacements réseau sont signalées, même si vous avez activé hello GPS.</span><span class="sxs-lookup"><span data-stu-id="95d86-135">When hello application runs in background, only network-based locations are reported, even if you enabled hello GPS.</span></span>
> 
> 

<span data-ttu-id="95d86-136">Si l’utilisateur de hello a redémarré à leur appareil, le rapport d’emplacement hello en arrière-plan est arrêté.</span><span class="sxs-lookup"><span data-stu-id="95d86-136">If hello user reboots their device, hello background location report is stopped.</span></span> <span data-ttu-id="95d86-137">toomake il redémarre automatiquement au moment du démarrage, ajoutez ce code.</span><span class="sxs-lookup"><span data-stu-id="95d86-137">toomake it automatically restart at boot time, add this code.</span></span>

    <receiver android:name="com.microsoft.azure.engagement.EngagementLocationBootReceiver"
           android:exported="false">
        <intent-filter>
            <action android:name="android.intent.action.BOOT_COMPLETED" />
        </intent-filter>
    </receiver>

<span data-ttu-id="95d86-138">Vous devez également hello tooadd suivant l’autorisation si manquant :</span><span class="sxs-lookup"><span data-stu-id="95d86-138">You also need tooadd hello following permission if missing:</span></span>

    <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />

## <a name="android-m-permissions"></a><span data-ttu-id="95d86-139">Autorisations Android M</span><span class="sxs-lookup"><span data-stu-id="95d86-139">Android M permissions</span></span>
<span data-ttu-id="95d86-140">À partir d’Android M, certaines autorisations sont gérées lors de l’exécution et nécessitent une approbation de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="95d86-140">Starting with Android M, some permissions are managed at runtime and need user approval.</span></span>

<span data-ttu-id="95d86-141">Si vous ciblez Android API de niveau 23, les autorisations d’exécution hello sont désactivées par défaut pour les nouvelles installations de l’application.</span><span class="sxs-lookup"><span data-stu-id="95d86-141">If you target Android API level 23, hello runtime permissions are turned off by default for new app installations.</span></span> <span data-ttu-id="95d86-142">Sinon, elles sont activées par défaut.</span><span class="sxs-lookup"><span data-stu-id="95d86-142">Otherwise they are turned on by default.</span></span>

<span data-ttu-id="95d86-143">Vous pouvez activer ou désactiver ces autorisations à partir du menu Paramètres de périphérique hello.</span><span class="sxs-lookup"><span data-stu-id="95d86-143">You can enable/disable those permissions from hello device settings menu.</span></span> <span data-ttu-id="95d86-144">Désactivation des autorisations à partir du menu du système hello arrête les processus d’arrière-plan hello d’application hello, qui est un comportement du système et n’a aucun impact sur la capacité tooreceive par émission de données en arrière-plan.</span><span class="sxs-lookup"><span data-stu-id="95d86-144">Turning off permissions from hello system menu kills hello background processes of hello application, which is a system behavior, and has no impact on ability tooreceive push in background.</span></span>

<span data-ttu-id="95d86-145">Dans le contexte de hello d’emplacement de Mobile Engagement reporting, les autorisations hello qui requièrent une approbation lors de l’exécution sont :</span><span class="sxs-lookup"><span data-stu-id="95d86-145">In hello context of Mobile Engagement location reporting, hello permissions that require approval at runtime are:</span></span>

* `ACCESS_COARSE_LOCATION`
* `ACCESS_FINE_LOCATION`

<span data-ttu-id="95d86-146">Demander des autorisations d’utilisateur hello à l’aide d’une boîte de dialogue système standard.</span><span class="sxs-lookup"><span data-stu-id="95d86-146">Request permissions from hello user using a standard system dialog.</span></span> <span data-ttu-id="95d86-147">Si l’utilisateur de hello approuve, indiquer ``EngagementAgent`` tootake modifier en compte en temps réel.</span><span class="sxs-lookup"><span data-stu-id="95d86-147">If hello user approves, tell ``EngagementAgent`` tootake that change into account in real-time.</span></span> <span data-ttu-id="95d86-148">Dans le cas contraire les modifications hello sont traité hello suivant temps hello lance hello application d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="95d86-148">Otherwise hello change is processed hello next time hello user launches hello application.</span></span>

<span data-ttu-id="95d86-149">Voici une toouse d’exemple de code dans une activité de vos autorisations toorequest d’application et le résultat de hello vers l’avant si positif trop``EngagementAgent``:</span><span class="sxs-lookup"><span data-stu-id="95d86-149">Here is a code sample toouse in an activity of your application toorequest permissions and forward hello result if positive too``EngagementAgent``:</span></span>

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
         * Request location permission, but this doesn't explain why it is needed toohello user.
         * hello standard Android documentation explains with more details how toodisplay a rationale activity tooexplain hello user why hello permission is needed in your application.
         * Putting COARSE vs FINE has no impact here, they are part of hello same group for runtime permission management.
         */
        if (checkSelfPermission(android.Manifest.permission.ACCESS_FINE_LOCATION) != PackageManager.PERMISSION_GRANTED)
          requestPermissions(new String[] { android.Manifest.permission.ACCESS_FINE_LOCATION }, 0);

      }
    }

    @Override
    public void onRequestPermissionsResult(int requestCode, String[] permissions, int[] grantResults)
    {
      /* Only a positive location permission update requires engagement agent refresh, hence hello request code matching from above function */
      if (requestCode == 0 && grantResults[0] == PackageManager.PERMISSION_GRANTED)
        getEngagementAgent().refreshPermissions();
    }
