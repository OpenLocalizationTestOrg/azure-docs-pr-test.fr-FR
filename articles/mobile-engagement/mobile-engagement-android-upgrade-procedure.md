---
title: "aaaAzure intégration du Kit de développement logiciel Android Mobile Engagement"
description: "Dernières mises à jour et procédures du SDK Android pour Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 11618586-c709-49ca-bcd8-745323ff1af6
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: df5c82812fe0a242eaa5df8c906030237215b7eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-procedures"></a><span data-ttu-id="79ffb-103">Procédures de mise à niveau</span><span class="sxs-lookup"><span data-stu-id="79ffb-103">Upgrade procedures</span></span>
<span data-ttu-id="79ffb-104">Si vous avez déjà intégré une ancienne version de notre kit de développement logiciel dans votre application, vous avez hello tooconsider hello Kit de développement logiciel de la mise à niveau les points suivants.</span><span class="sxs-lookup"><span data-stu-id="79ffb-104">If you already have integrated an older version of our SDK into your application, you have tooconsider hello following points when upgrading hello SDK.</span></span>

<span data-ttu-id="79ffb-105">Vous avez peut-être toofollow plusieurs procédures issue de plusieurs versions du Kit de développement logiciel de hello.</span><span class="sxs-lookup"><span data-stu-id="79ffb-105">You may have toofollow several procedures if you missed several versions of hello SDK.</span></span> <span data-ttu-id="79ffb-106">Par exemple, si vous migrez à partir de 1.4.0 too1.6.0 que vous avez toofirst suivez hello » à partir de 1.4.0 too1.5.0 « procédure puis hello » à partir de 1.5.0 too1.6.0 » procédure.</span><span class="sxs-lookup"><span data-stu-id="79ffb-106">For example if you migrate from 1.4.0 too1.6.0 you have toofirst follow hello "from 1.4.0 too1.5.0" procedure then hello "from 1.5.0 too1.6.0" procedure.</span></span>

<span data-ttu-id="79ffb-107">Version hello vous mettez à niveau, vous avez tooreplace hello `mobile-engagement-VERSION.jar` avec hello nouveau.</span><span class="sxs-lookup"><span data-stu-id="79ffb-107">Whatever hello version you upgrade from, you have tooreplace hello `mobile-engagement-VERSION.jar` with hello new one.</span></span>

## <a name="from-420-too421"></a><span data-ttu-id="79ffb-108">À partir de 4.2.0 too4.2.1</span><span class="sxs-lookup"><span data-stu-id="79ffb-108">From 4.2.0 too4.2.1</span></span>
<span data-ttu-id="79ffb-109">Cette étape peut effectivement être effectuée sur n’importe quelle version du Kit de développement logiciel de hello, il s’agit d’une amélioration de la sécurité lorsque vous intégrez les activités de portée.</span><span class="sxs-lookup"><span data-stu-id="79ffb-109">This step can actually be done on any version of hello SDK, its a security improvement when you integrate Reach activities.</span></span>

<span data-ttu-id="79ffb-110">Vous devez maintenant ajouter `exported="false"` tooall portée activités.</span><span class="sxs-lookup"><span data-stu-id="79ffb-110">You should now add `exported="false"` tooall Reach activities.</span></span>

<span data-ttu-id="79ffb-111">Les activités Reach doivent maintenant ressembler à ceci sur votre `AndroidManifest.xml`:</span><span class="sxs-lookup"><span data-stu-id="79ffb-111">Reach activities should now look like this on your `AndroidManifest.xml`:</span></span>

            <activity android:name="com.microsoft.azure.engagement.reach.activity.EngagementTextAnnouncementActivity" android:theme="@android:style/Theme.Light" android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
                <category android:name="android.intent.category.DEFAULT" />
                <data android:mimeType="text/plain" />
              </intent-filter>
            </activity>
            <activity android:name="com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity" android:theme="@android:style/Theme.Light" android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
                <category android:name="android.intent.category.DEFAULT" />
                <data android:mimeType="text/html" />
              </intent-filter>
            </activity>
            <activity android:name="com.microsoft.azure.engagement.reach.activity.EngagementPollActivity" android:theme="@android:style/Theme.Light" android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.POLL"/>
                <category android:name="android.intent.category.DEFAULT" />
              </intent-filter>
            </activity>
            <activity android:name="com.microsoft.azure.engagement.reach.activity.EngagementLoadingActivity" android:theme="@android:style/Theme.Dialog" android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.LOADING"/>
                <category android:name="android.intent.category.DEFAULT"/>
              </intent-filter>
            </activity>

## <a name="from-400-too410"></a><span data-ttu-id="79ffb-112">À partir de 4.0.0 too4.1.0</span><span class="sxs-lookup"><span data-stu-id="79ffb-112">From 4.0.0 too4.1.0</span></span>
<span data-ttu-id="79ffb-113">Hello SDK maintenant handle nouveau modèle d’autorisation à partir d’Android M.</span><span class="sxs-lookup"><span data-stu-id="79ffb-113">hello SDK now handle new permission model from Android M.</span></span>

<span data-ttu-id="79ffb-114">Si vous utilisez des fonctionnalités de localisation ou des notifications BigPicture, veuillez lire [cette section](mobile-engagement-android-integrate-engagement.md#android-m-permissions).</span><span class="sxs-lookup"><span data-stu-id="79ffb-114">If you use location features or big picture notifications please read [this section](mobile-engagement-android-integrate-engagement.md#android-m-permissions).</span></span>

<span data-ttu-id="79ffb-115">En outre toohello nouveau modèle d’autorisation, nous prennent désormais en charge la configuration des fonctionnalités de l’emplacement lors de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="79ffb-115">In addition toohello new permission model, we now support configuring location features at runtime.</span></span>
<span data-ttu-id="79ffb-116">Nous sommes toujours compatibles avec les paramètres de manifeste hello pour l’emplacement, mais il est désormais déconseillée.</span><span class="sxs-lookup"><span data-stu-id="79ffb-116">We are still compatible with hello manifest parameters for location but it's now deprecated.</span></span> <span data-ttu-id="79ffb-117">sections de suivantes de hello de suppression toouse configuration d’exécution, à partir de votre ``AndroidManifest.xml``:</span><span class="sxs-lookup"><span data-stu-id="79ffb-117">toouse runtime configuration, remove hello following sections from your ``AndroidManifest.xml``:</span></span>

    <meta-data
      android:name="engagement:locationReport:lazyArea"
      android:value="true"/>
    <meta-data
      android:name="engagement:locationReport:realTime"
      android:value="true"/>
    <meta-data
      android:name="engagement:locationReport:realTime:background"
      android:value="true"/>
    <meta-data
      android:name="engagement:locationReport:realTime:fine"
      android:value="true"/>

<span data-ttu-id="79ffb-118">et lecture [cette procédure de mise à jour](mobile-engagement-android-integrate-engagement.md#location-reporting) toouse configuration d’exécution à la place.</span><span class="sxs-lookup"><span data-stu-id="79ffb-118">and read [this updated procedure](mobile-engagement-android-integrate-engagement.md#location-reporting) toouse runtime configuration instead.</span></span>

## <a name="from-300-too400"></a><span data-ttu-id="79ffb-119">À partir de 3.0.0 too4.0.0</span><span class="sxs-lookup"><span data-stu-id="79ffb-119">From 3.0.0 too4.0.0</span></span>
### <a name="native-push"></a><span data-ttu-id="79ffb-120">Native Push</span><span class="sxs-lookup"><span data-stu-id="79ffb-120">Native push</span></span>
<span data-ttu-id="79ffb-121">Push natif (GCM/ADM) est désormais également utilisé pour des notifications de l’application vous devez configurer les informations d’identification de push natif hello pour n’importe quel type de campagne push.</span><span class="sxs-lookup"><span data-stu-id="79ffb-121">Native push (GCM/ADM) is now also used for in app notifications so you must configure hello native push credentials for any type of push campaign.</span></span>

<span data-ttu-id="79ffb-122">Si ce n’est déjà fait, suivez [cette procédure](mobile-engagement-android-integrate-engagement-reach.md#native-push).</span><span class="sxs-lookup"><span data-stu-id="79ffb-122">If not already done please follow [this procedure](mobile-engagement-android-integrate-engagement-reach.md#native-push).</span></span>

### <a name="androidmanifestxml"></a><span data-ttu-id="79ffb-123">AndroidManifest.xml</span><span class="sxs-lookup"><span data-stu-id="79ffb-123">AndroidManifest.xml</span></span>
<span data-ttu-id="79ffb-124">L’intégrationReach a été modifiée dans ``AndroidManifest.xml``.</span><span class="sxs-lookup"><span data-stu-id="79ffb-124">Reach integration has been modified in ``AndroidManifest.xml``.</span></span>

<span data-ttu-id="79ffb-125">Remplacez ceci :</span><span class="sxs-lookup"><span data-stu-id="79ffb-125">Replace this:</span></span>

    <receiver
      android:name="com.microsoft.azure.engagement.reach.EngagementReachReceiver"
      android:exported="false">
      <intent-filter>
        <action android:name="android.intent.action.BOOT_COMPLETED"/>
        <action android:name="com.microsoft.azure.engagement.intent.action.AGENT_CREATED"/>
        <action android:name="com.microsoft.azure.engagement.intent.action.MESSAGE"/>
        <action android:name="com.microsoft.azure.engagement.reach.intent.action.ACTION_NOTIFICATION"/>
        <action android:name="com.microsoft.azure.engagement.reach.intent.action.EXIT_NOTIFICATION"/>
        <action android:name="android.intent.action.DOWNLOAD_COMPLETE"/>
        <action android:name="com.microsoft.azure.engagement.reach.intent.action.DOWNLOAD_TIMEOUT"/>
      </intent-filter>
    </receiver>

<span data-ttu-id="79ffb-126">par</span><span class="sxs-lookup"><span data-stu-id="79ffb-126">By</span></span>

    <receiver
      android:name="com.microsoft.azure.engagement.reach.EngagementReachReceiver"
      android:exported="false">
      <intent-filter>
        <action android:name="android.intent.action.BOOT_COMPLETED"/>
        <action android:name="com.microsoft.azure.engagement.intent.action.AGENT_CREATED"/>
        <action android:name="com.microsoft.azure.engagement.intent.action.MESSAGE"/>
        <action android:name="com.microsoft.azure.engagement.reach.intent.action.ACTION_NOTIFICATION"/>
        <action android:name="com.microsoft.azure.engagement.reach.intent.action.EXIT_NOTIFICATION"/>
        <action android:name="com.microsoft.azure.engagement.reach.intent.action.DOWNLOAD_TIMEOUT"/>
      </intent-filter>
    </receiver>
    <receiver android:name="com.microsoft.azure.engagement.reach.EngagementReachDownloadReceiver">
      <intent-filter>
        <action android:name="android.intent.action.DOWNLOAD_COMPLETE"/>
      </intent-filter>
    </receiver>

<span data-ttu-id="79ffb-127">Il se peut désormais qu’un écran de chargement s’affiche lorsque vous cliquez sur une annonce (avec texte/contenu web) ou sur une interrogation.</span><span class="sxs-lookup"><span data-stu-id="79ffb-127">There is possibly a loading screen now when you click on an announcement (with text/web content) or a poll.</span></span>
<span data-ttu-id="79ffb-128">Vous avez tooadd cela pour ces toowork campagnes dans 4.0.0 :</span><span class="sxs-lookup"><span data-stu-id="79ffb-128">You have tooadd this for those campaigns toowork in 4.0.0:</span></span>

    <activity
      android:name="com.microsoft.azure.engagement.reach.activity.EngagementLoadingActivity"
      android:theme="@android:style/Theme.Dialog">
      <intent-filter>
        <action android:name="com.microsoft.azure.engagement.reach.intent.action.LOADING"/>
        <category android:name="android.intent.category.DEFAULT"/>
      </intent-filter>
    </activity>

### <a name="resources"></a><span data-ttu-id="79ffb-129">Ressources</span><span class="sxs-lookup"><span data-stu-id="79ffb-129">Resources</span></span>
<span data-ttu-id="79ffb-130">Incorporer hello nouvelle `res/layout/engagement_loading.xml` fichier dans votre projet.</span><span class="sxs-lookup"><span data-stu-id="79ffb-130">Embed hello new `res/layout/engagement_loading.xml` file into your project.</span></span>

## <a name="from-240-too300"></a><span data-ttu-id="79ffb-131">À partir de 2.4.0 too3.0.0</span><span class="sxs-lookup"><span data-stu-id="79ffb-131">From 2.4.0 too3.0.0</span></span>
<span data-ttu-id="79ffb-132">Hello suivante décrit comment toomigrate une intégration du Kit de développement logiciel de hello Capptain service offert par Capptain SAS dans une application grâce à Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="79ffb-132">hello following describes how toomigrate an SDK integration from hello Capptain service offered by Capptain SAS into an app powered by Azure Mobile Engagement.</span></span> <span data-ttu-id="79ffb-133">Si vous effectuez une migration à partir d’une version antérieure, consultez hello Capptain site web toomigrate too2.4.0 tout d’abord, puis appliquez hello suivant la procédure.</span><span class="sxs-lookup"><span data-stu-id="79ffb-133">If you are migrating from an earlier version, please consult hello Capptain web site toomigrate too2.4.0 first and then apply hello following procedure.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="79ffb-134">Capptain Mobile Engagement sont des services mêmes pas hello et hello la procédure décrite ci-dessous met en évidence uniquement comment toomigrate hello application cliente.</span><span class="sxs-lookup"><span data-stu-id="79ffb-134">Capptain and Mobile Engagement are not hello same services, and hello procedure given below only highlights how toomigrate hello client app.</span></span> <span data-ttu-id="79ffb-135">Migration hello SDK dans l’application hello ne sera pas migré vos données à partir de serveurs de hello Capptain serveurs toohello Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="79ffb-135">Migrating hello SDK in hello app will NOT migrate your data from hello Capptain servers toohello Mobile Engagement servers.</span></span>
> 
> 

### <a name="jar-file"></a><span data-ttu-id="79ffb-136">Fichier JAR</span><span class="sxs-lookup"><span data-stu-id="79ffb-136">JAR file</span></span>
<span data-ttu-id="79ffb-137">Remplacez `capptain.jar` par `mobile-engagement-VERSION.jar` dans votre dossier `libs`.</span><span class="sxs-lookup"><span data-stu-id="79ffb-137">Replace `capptain.jar` by `mobile-engagement-VERSION.jar` in your `libs` folder.</span></span>

### <a name="resource-files"></a><span data-ttu-id="79ffb-138">Fichiers de ressources</span><span class="sxs-lookup"><span data-stu-id="79ffb-138">Resource files</span></span>
<span data-ttu-id="79ffb-139">Chaque fichier de ressources que nous avons fournis (précédé `capptain_`) a toobe remplacé par hello nouveaux (avec le préfixe `engagement_`).</span><span class="sxs-lookup"><span data-stu-id="79ffb-139">Every resource file that we provided (prefixed by `capptain_`) has toobe replaced by hello new ones (prefixed with `engagement_`).</span></span>

<span data-ttu-id="79ffb-140">Si vous avez personnalisé ces fichiers, vous avez toore-appliquer votre personnalisation sur les nouveaux fichiers de hello, **tous les identificateurs hello dans les fichiers de ressources hello ont également été renommés**.</span><span class="sxs-lookup"><span data-stu-id="79ffb-140">If you customized those files, you have toore-apply your customization on hello new files, **all hello identifiers in hello resource files have also been renamed**.</span></span>

### <a name="application-id"></a><span data-ttu-id="79ffb-141">ID de l'application</span><span class="sxs-lookup"><span data-stu-id="79ffb-141">Application ID</span></span>
<span data-ttu-id="79ffb-142">Engagement utilise désormais une connexion chaîne tooconfigure hello Kit de développement logiciel des identificateurs comme identificateur de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="79ffb-142">Now Engagement uses a connection string tooconfigure hello SDK identifiers such as hello application identifier.</span></span>

<span data-ttu-id="79ffb-143">Vous avez toouse `EngagementAgent.init` méthode dans votre activité Lanceur comme suit :</span><span class="sxs-lookup"><span data-stu-id="79ffb-143">You have toouse `EngagementAgent.init` method in your launcher activity like this:</span></span>

            EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
            engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
            EngagementAgent.getInstance(this).init(engagementConfiguration);

<span data-ttu-id="79ffb-144">chaîne de connexion Hello pour votre application s’affiche sur le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="79ffb-144">hello connection string for your application is displayed on Azure Portal.</span></span>

<span data-ttu-id="79ffb-145">Veuillez supprimer n’importe quel appel trop`CapptainAgent.configure` comme `EngagementAgent.init` remplace cette méthode.</span><span class="sxs-lookup"><span data-stu-id="79ffb-145">Please remove any call too`CapptainAgent.configure` as `EngagementAgent.init` replaces that method.</span></span>

<span data-ttu-id="79ffb-146">Hello `appId` ne peuvent plus être configurées à l’aide de `AndroidManifest.xml`.</span><span class="sxs-lookup"><span data-stu-id="79ffb-146">hello `appId` can no longer be configured using `AndroidManifest.xml`.</span></span>

<span data-ttu-id="79ffb-147">Supprimez cette section de votre `AndroidManifest.xml` si elle existe :</span><span class="sxs-lookup"><span data-stu-id="79ffb-147">Please remove this section from your `AndroidManifest.xml` if you have it:</span></span>

            <meta-data android:name="capptain:appId" android:value="<YOUR_APPID>"/>

### <a name="java-api"></a><span data-ttu-id="79ffb-148">API Java</span><span class="sxs-lookup"><span data-stu-id="79ffb-148">Java API</span></span>
<span data-ttu-id="79ffb-149">Chaque classe Java de notre kit de développement logiciel de tooany appel a toobe renommé ; par exemple, `CapptainAgent.getInstance(this)` doit être renommé `EngagementAgent.getInstance(this)`, `extends CapptainActivity` doit être renommé `extends EngagementActivity` etc....</span><span class="sxs-lookup"><span data-stu-id="79ffb-149">Every call tooany Java class of our SDK has toobe renamed; for example, `CapptainAgent.getInstance(this)` must be renamed `EngagementAgent.getInstance(this)`, `extends CapptainActivity` must be renamed `extends EngagementActivity` etc...</span></span>

<span data-ttu-id="79ffb-150">Si vous ont été intégrées dans les fichiers de préférence de l’agent par défaut, le nom de fichier par défaut hello est désormais `engagement.agent` et clé de hello est `engagement:agent`.</span><span class="sxs-lookup"><span data-stu-id="79ffb-150">If you were integrated with default agent preference files, hello default file name is now `engagement.agent` and hello key is `engagement:agent`.</span></span>

<span data-ttu-id="79ffb-151">Lorsque vous créez des annonces de web, hello Javascript binder est désormais `engagementReachContent`.</span><span class="sxs-lookup"><span data-stu-id="79ffb-151">When creating web announcements, hello Javascript binder is now `engagementReachContent`.</span></span>

### <a name="androidmanifestxml"></a><span data-ttu-id="79ffb-152">AndroidManifest.xml</span><span class="sxs-lookup"><span data-stu-id="79ffb-152">AndroidManifest.xml</span></span>
<span data-ttu-id="79ffb-153">De nombreuses modifications s’est-il passé et service de hello n’est pas partagé plus un grand nombre de récepteurs ne sont plus exportable.</span><span class="sxs-lookup"><span data-stu-id="79ffb-153">A lot of changes happened there, hello service is not shared anymore, and a lot of receivers are not exportable anymore.</span></span>

<span data-ttu-id="79ffb-154">déclaration du service Hello est désormais plus simple. Supprimez le filtre intention de hello et toutes les métadonnées qu’il contient et ajoutez `exportable=false`.</span><span class="sxs-lookup"><span data-stu-id="79ffb-154">hello service declaration is now simpler; remove hello intent filter and all meta-data inside it, and add `exportable=false`.</span></span>

<span data-ttu-id="79ffb-155">De plus, tous les éléments sont renommé toouse engagement.</span><span class="sxs-lookup"><span data-stu-id="79ffb-155">Plus everything is renamed toouse engagement.</span></span>

<span data-ttu-id="79ffb-156">Vous devez obtenir quelque chose similaire à ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="79ffb-156">It now looks like:</span></span>

            <service
              android:name="com.microsoft.azure.engagement.service.EngagementService"
              android:exported="false"
              android:label="<Your application name>Service"
              android:process=":Engagement"/>

<span data-ttu-id="79ffb-157">Lorsque vous souhaitez que les journaux des tests tooenable, hello métadonnées ont été déplacés de balise de l’application toohello et a été renommé :</span><span class="sxs-lookup"><span data-stu-id="79ffb-157">When you want tooenable test logs, hello meta-data has now been moved toohello application tag and has been renamed:</span></span>

            <application>

              <meta-data android:name="engagement:log:test" android:value="true" />

              <service/>

            </application>

<span data-ttu-id="79ffb-158">Toutes les autres métadonnées ont simplement été renommées, voici la liste complète de hello (bien entendu renommer uniquement hello celles que vous utilisez) :</span><span class="sxs-lookup"><span data-stu-id="79ffb-158">All other meta-data have just been renamed, here is hello full list (of course rename only hello ones you use):</span></span>

            <meta-data
              android:name="engagement:reportCrash"
              android:value="true"/>
            <meta-data
              android:name="engagement:sessionTimeout"
              android:value="10000"/>
            <meta-data
              android:name="engagement:burstThreshold"
              android:value="0"/>
            <meta-data
              android:name="engagement:connection:delay"
              android:value="0"/>
            <meta-data
              android:name="engagement:locationReport:lazyArea"
              android:value="false"/>
            <meta-data
              android:name="engagement:locationReport:realTime"
              android:value="false"/>
            <meta-data
              android:name="engagement:locationReport:realTime:background"
              android:value="false"/>
            <meta-data
              android:name="engagement:locationReport:realTime:fine"
              android:value="false"/>
            <meta-data
              android:name="engagement:agent:settings:name"
              android:value="engagement.agent"/>
            <meta-data
              android:name="engagement:agent:settings:mode"
              android:value="0"/>
            <meta-data
              android:name="engagement:gcm:sender"
              android:value="<YOUR_PROJECT_NUMBER>\n"/>
            <meta-data
              android:name="engagement:adm:register"
              android:value="true"/>
            <meta-data
              android:name="engagement:reach:notification:icon"
              android:value="<DRAWABLE_NAME_WITHOUT_EXTENSION>"/>

            <activity android:name="SomeActivityWithoutReachOverlay">
              <meta-data
                android:name="engagement:notification:overlay"
                android:value="false"/>
            </activity>

<span data-ttu-id="79ffb-159">Suivi de Google Play et SmartAd a été supprimé à partir du Kit de développement logiciel vous devez tooremove cela sans remplacement :</span><span class="sxs-lookup"><span data-stu-id="79ffb-159">Google Play and SmartAd tracking has been removed from SDK you just have tooremove this without replacement:</span></span>

            <meta-data 
                android:name="capptain:track:installReferrerForwardList"
                android:value="com.class1,com.class2"/>
            <meta-data
                android:name="capptain:track:adservers"
                android:value="smartad" />

<span data-ttu-id="79ffb-160">activités de portée Hello sont désormais déclarées comme suit :</span><span class="sxs-lookup"><span data-stu-id="79ffb-160">hello Reach activities are now declared like this:</span></span>

            <activity
              android:name="com.microsoft.azure.engagement.reach.activity.EngagementTextAnnouncementActivity"
              android:theme="@android:style/Theme.Light">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
                <category android:name="android.intent.category.DEFAULT"/>
                <data android:mimeType="text/plain"/>
              </intent-filter>
            </activity>
            <activity
              android:name="com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity"
              android:theme="@android:style/Theme.Light">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
                <category android:name="android.intent.category.DEFAULT"/>
                <data android:mimeType="text/html"/>
              </intent-filter>
            </activity>
            <activity
              android:name="com.microsoft.azure.engagement.reach.activity.EngagementPollActivity"
              android:theme="@android:style/Theme.Light">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.POLL"/>
                <category android:name="android.intent.category.DEFAULT"/>
              </intent-filter>
            </activity>

<span data-ttu-id="79ffb-161">Si vous avez des activités personnalisées de portée, vous devez soit uniquement toochange hello actions intention toomatch `com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT` ou `com.microsoft.azure.engagement.reach.intent.action.POLL`.</span><span class="sxs-lookup"><span data-stu-id="79ffb-161">If you have custom Reach activities, you need only toochange hello intent actions toomatch either `com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT` or `com.microsoft.azure.engagement.reach.intent.action.POLL`.</span></span>

<span data-ttu-id="79ffb-162">Hello récepteurs de diffusion ont été renommés, ainsi que nous ajoutons maintenant `exported=false`.</span><span class="sxs-lookup"><span data-stu-id="79ffb-162">hello broadcast receivers have been renamed, plus we now add `exported=false`.</span></span> <span data-ttu-id="79ffb-163">Voici la liste complète de hello de récepteurs hello avec nouvelle spécification hello, (bien entendu renommer uniquement hello celles que vous utilisez) :</span><span class="sxs-lookup"><span data-stu-id="79ffb-163">Here is hello full list of hello receivers with hello new specification, (of course rename only hello ones you use):</span></span>

            <receiver android:name="com.microsoft.azure.engagement.reach.EngagementReachReceiver"
              android:exported="false">
              <intent-filter>
                <action android:name="android.intent.action.BOOT_COMPLETED"/>
                <action android:name="com.microsoft.azure.engagement.intent.action.AGENT_CREATED"/>
                <action android:name="com.microsoft.azure.engagement.intent.action.MESSAGE"/>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ACTION_NOTIFICATION"/>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.EXIT_NOTIFICATION"/>
                <action android:name="android.intent.action.DOWNLOAD_COMPLETE"/>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.DOWNLOAD_TIMEOUT"/>
              </intent-filter>
            </receiver>

            <receiver android:name="com.microsoft.azure.engagement.gcm.EngagementGCMEnabler"
              android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.intent.action.APPID_GOT" />
              </intent-filter>
            </receiver>

            <receiver
              android:name="com.microsoft.azure.engagement.gcm.EngagementGCMReceiver"
              android:permission="com.google.android.c2dm.permission.SEND">
              <intent-filter>
                <action android:name="com.google.android.c2dm.intent.REGISTRATION"/>
                <action android:name="com.google.android.c2dm.intent.RECEIVE"/>
                <category android:name="<your_package_name>"/>
              </intent-filter>
            </receiver>

            <receiver android:name="com.microsoft.azure.engagement.adm.EngagementADMEnabler"
              android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.intent.action.APPID_GOT"/>
              </intent-filter>
            </receiver>

            <receiver
              android:name="com.microsoft.azure.engagement.adm.EngagementADMReceiver"
              android:permission="com.amazon.device.messaging.permission.SEND">
              <intent-filter>
                <action android:name="com.amazon.device.messaging.intent.REGISTRATION"/>
                <action android:name="com.amazon.device.messaging.intent.RECEIVE"/>
                <category android:name="<your_package_name>"/>
              </intent-filter>
            </receiver>

            <receiver android:name="<your_sub_class_of_com.microsoft.azure.engagement.reach.EngagementReachDataPushReceiver>"
              android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.DATA_PUSH" />
              </intent-filter>
            </receiver>

            <receiver android:name="com.microsoft.azure.engagement.EngagementLocationBootReceiver"
               android:exported="false">
               <intent-filter>
                  <action android:name="android.intent.action.BOOT_COMPLETED" />
               </intent-filter>
            </receiver>

            <receiver android:name="<your_sub_class_of_com.microsoft.azure.engagement.EngagementConnectionReceiver.java>"
              android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.intent.action.CONNECTED"/>
                <action android:name="com.microsoft.azure.engagement.intent.action.DISCONNECTED"/>
              </intent-filter>
            </receiver>

            <receiver
              android:name="<your_sub_class_of_com.microsoft.azure.engagement.EngagementMessageReceiver.java>"
              android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.MESSAGE"/>
              </intent-filter>
            </receiver>

<span data-ttu-id="79ffb-164">Récepteur de suivi a été supprimé, afin que vous ayez tooremove de cette section :</span><span class="sxs-lookup"><span data-stu-id="79ffb-164">Tracking receiver has been removed, so you have tooremove this section:</span></span>

          <receiver android:name="com.ubikod.capptain.android.sdk.track.CapptainTrackReceiver">
            <intent-filter>
              <action android:name="com.ubikod.capptain.intent.action.APPID_GOT" />
              <!-- possibly <action android:name="com.android.vending.INSTALL_REFERRER" /> -->
            </intent-filter>
          </receiver>

<span data-ttu-id="79ffb-165">Notez que le récepteur de diffusion déclaration hello de votre implémentation de hello **EngagementMessageReceiver** a été modifié dans hello `AndroidManifest.xml`.</span><span class="sxs-lookup"><span data-stu-id="79ffb-165">Note that hello declaration of your implementation of hello broadcast receiver **EngagementMessageReceiver** has changed in hello `AndroidManifest.xml`.</span></span> <span data-ttu-id="79ffb-166">En effet, messages hello API toosend et remove XMPP arbitraire à partir des entités XMPP arbitraires et hello API toosend et recevoir des messages entre les appareils ont été supprimées.</span><span class="sxs-lookup"><span data-stu-id="79ffb-166">This is because hello API toosend and remove arbitrary XMPP messages from arbitrary XMPP entities and hello API toosend and receive messages between devices have been removed.</span></span> <span data-ttu-id="79ffb-167">Par conséquent, vous avez également hello toodelete suivant des rappels à partir de votre **EngagementMessageReceiver** implémentation :</span><span class="sxs-lookup"><span data-stu-id="79ffb-167">Thus, you have also toodelete hello following callbacks from your **EngagementMessageReceiver** implementation :</span></span>

            protected void onDeviceMessageReceived(android.content.Context context, java.lang.String deviceId, java.lang.String payload)

<span data-ttu-id="79ffb-168">and</span><span class="sxs-lookup"><span data-stu-id="79ffb-168">and</span></span>

            protected void onXMPPMessageReceived(android.content.Context context, android.os.Bundle message)

<span data-ttu-id="79ffb-169">puis supprimez tout appel sur **EngagementAgent** dans :</span><span class="sxs-lookup"><span data-stu-id="79ffb-169">then delete any call on **EngagementAgent** for :</span></span>

            sendMessageToDevice(java.lang.String deviceId, java.lang.String payload, java.lang.String packageName)

<span data-ttu-id="79ffb-170">and</span><span class="sxs-lookup"><span data-stu-id="79ffb-170">and</span></span>

            sendXMPPMessage(android.os.Bundle msg)

### <a name="proguard"></a><span data-ttu-id="79ffb-171">Proguard</span><span class="sxs-lookup"><span data-stu-id="79ffb-171">Proguard</span></span>
<span data-ttu-id="79ffb-172">Configuration proguard peut être touchée par repositionnement, hello règles sont désormais similaire à :</span><span class="sxs-lookup"><span data-stu-id="79ffb-172">Proguard configuration can be impacted by rebranding, hello rules are now looking like:</span></span>

            -dontwarn android.**
            -keep class android.support.v4.** { *; }

            -keep public class * extends android.os.IInterface
            -keep class com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity$EngagementReachContentJS {
              <methods>;
            }

