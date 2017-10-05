---
title: "Intégration du SDK Android d'Azure Mobile Engagement"
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
ms.openlocfilehash: 1f047f93fa8bc852b28c86e91d0c007a94fb4299
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="upgrade-procedures"></a><span data-ttu-id="0a622-103">Procédures de mise à niveau</span><span class="sxs-lookup"><span data-stu-id="0a622-103">Upgrade procedures</span></span>
<span data-ttu-id="0a622-104">Si vous avez déjà intégré une ancienne version de notre SDK à votre application, tenez compte des points suivants avant de procéder à la mise à niveau du SDK.</span><span class="sxs-lookup"><span data-stu-id="0a622-104">If you already have integrated an older version of our SDK into your application, you have to consider the following points when upgrading the SDK.</span></span>

<span data-ttu-id="0a622-105">Vous devrez peut-être suivre quelques procédures si vous avez manqué plusieurs versions du kit SDK.</span><span class="sxs-lookup"><span data-stu-id="0a622-105">You may have to follow several procedures if you missed several versions of the SDK.</span></span> <span data-ttu-id="0a622-106">Par exemple, si vous migrez de la version 1.4.0 vers 1.6.0, vous devez tout d'abord suivre la procédure « Migration de 1.4.0 vers 1.5.0 », puis la procédure « Migration de 1.5.0 vers 1.6.0 ».</span><span class="sxs-lookup"><span data-stu-id="0a622-106">For example if you migrate from 1.4.0 to 1.6.0 you have to first follow the "from 1.4.0 to 1.5.0" procedure then the "from 1.5.0 to 1.6.0" procedure.</span></span>

<span data-ttu-id="0a622-107">Quelle que soit la version que vous mettez à niveau, vous devez remplacer `mobile-engagement-VERSION.jar` .</span><span class="sxs-lookup"><span data-stu-id="0a622-107">Whatever the version you upgrade from, you have to replace the `mobile-engagement-VERSION.jar` with the new one.</span></span>

## <a name="from-420-to-421"></a><span data-ttu-id="0a622-108">Migration de 4.2.0 vers 4.2.1</span><span class="sxs-lookup"><span data-stu-id="0a622-108">From 4.2.0 to 4.2.1</span></span>
<span data-ttu-id="0a622-109">Vous pouvez effectuer cette étape sur n’importe quelle version du SDK. Il s’agit d’une amélioration de sécurité quand vous intégrez des activités Reach.</span><span class="sxs-lookup"><span data-stu-id="0a622-109">This step can actually be done on any version of the SDK, its a security improvement when you integrate Reach activities.</span></span>

<span data-ttu-id="0a622-110">Vous devez maintenant ajouter `exported="false"` à toutes les activités Reach.</span><span class="sxs-lookup"><span data-stu-id="0a622-110">You should now add `exported="false"` to all Reach activities.</span></span>

<span data-ttu-id="0a622-111">Les activités Reach doivent maintenant ressembler à ceci sur votre `AndroidManifest.xml`:</span><span class="sxs-lookup"><span data-stu-id="0a622-111">Reach activities should now look like this on your `AndroidManifest.xml`:</span></span>

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

## <a name="from-400-to-410"></a><span data-ttu-id="0a622-112">Migration de 4.0.0 vers 4.1.0</span><span class="sxs-lookup"><span data-stu-id="0a622-112">From 4.0.0 to 4.1.0</span></span>
<span data-ttu-id="0a622-113">Le SDK gère maintenant un nouveau modèle d’autorisation à partir d’Android M.</span><span class="sxs-lookup"><span data-stu-id="0a622-113">The SDK now handle new permission model from Android M.</span></span>

<span data-ttu-id="0a622-114">Si vous utilisez des fonctionnalités de localisation ou des notifications BigPicture, veuillez lire [cette section](mobile-engagement-android-integrate-engagement.md#android-m-permissions).</span><span class="sxs-lookup"><span data-stu-id="0a622-114">If you use location features or big picture notifications please read [this section](mobile-engagement-android-integrate-engagement.md#android-m-permissions).</span></span>

<span data-ttu-id="0a622-115">Outre le nouveau modèle d’autorisation, nous prenons désormais en charge les fonctionnalités de localisation lors de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="0a622-115">In addition to the new permission model, we now support configuring location features at runtime.</span></span>
<span data-ttu-id="0a622-116">Nous sommes toujours compatibles avec les paramètres du manifeste pour la localisation, mais ils sont à présent obsolètes.</span><span class="sxs-lookup"><span data-stu-id="0a622-116">We are still compatible with the manifest parameters for location but it's now deprecated.</span></span> <span data-ttu-id="0a622-117">Pour utiliser la configuration lors de l’exécution, supprimez les sections suivantes à partir de votre ``AndroidManifest.xml``:</span><span class="sxs-lookup"><span data-stu-id="0a622-117">To use runtime configuration, remove the following sections from your ``AndroidManifest.xml``:</span></span>

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

<span data-ttu-id="0a622-118">et lisez [cette procédure mise à jour](mobile-engagement-android-integrate-engagement.md#location-reporting) pour utiliser à la place une configuration lors de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="0a622-118">and read [this updated procedure](mobile-engagement-android-integrate-engagement.md#location-reporting) to use runtime configuration instead.</span></span>

## <a name="from-300-to-400"></a><span data-ttu-id="0a622-119">Migration de 3.0.0 vers 4.0.0</span><span class="sxs-lookup"><span data-stu-id="0a622-119">From 3.0.0 to 4.0.0</span></span>
### <a name="native-push"></a><span data-ttu-id="0a622-120">Native Push</span><span class="sxs-lookup"><span data-stu-id="0a622-120">Native push</span></span>
<span data-ttu-id="0a622-121">Native Push (GCM/ADM) est désormais également utilisé pour les notifications dans l’application. Vous devez donc configurer les informations d’identification Native Push pour tout type de campagne push.</span><span class="sxs-lookup"><span data-stu-id="0a622-121">Native push (GCM/ADM) is now also used for in app notifications so you must configure the native push credentials for any type of push campaign.</span></span>

<span data-ttu-id="0a622-122">Si ce n’est déjà fait, suivez [cette procédure](mobile-engagement-android-integrate-engagement-reach.md#native-push).</span><span class="sxs-lookup"><span data-stu-id="0a622-122">If not already done please follow [this procedure](mobile-engagement-android-integrate-engagement-reach.md#native-push).</span></span>

### <a name="androidmanifestxml"></a><span data-ttu-id="0a622-123">AndroidManifest.xml</span><span class="sxs-lookup"><span data-stu-id="0a622-123">AndroidManifest.xml</span></span>
<span data-ttu-id="0a622-124">L’intégrationReach a été modifiée dans ``AndroidManifest.xml``.</span><span class="sxs-lookup"><span data-stu-id="0a622-124">Reach integration has been modified in ``AndroidManifest.xml``.</span></span>

<span data-ttu-id="0a622-125">Remplacez ceci :</span><span class="sxs-lookup"><span data-stu-id="0a622-125">Replace this:</span></span>

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

<span data-ttu-id="0a622-126">par</span><span class="sxs-lookup"><span data-stu-id="0a622-126">By</span></span>

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

<span data-ttu-id="0a622-127">Il se peut désormais qu’un écran de chargement s’affiche lorsque vous cliquez sur une annonce (avec texte/contenu web) ou sur une interrogation.</span><span class="sxs-lookup"><span data-stu-id="0a622-127">There is possibly a loading screen now when you click on an announcement (with text/web content) or a poll.</span></span>
<span data-ttu-id="0a622-128">Vous devez ajouter ceci pour que les campagnes fonctionnent dans la version 4.0.0 :</span><span class="sxs-lookup"><span data-stu-id="0a622-128">You have to add this for those campaigns to work in 4.0.0:</span></span>

    <activity
      android:name="com.microsoft.azure.engagement.reach.activity.EngagementLoadingActivity"
      android:theme="@android:style/Theme.Dialog">
      <intent-filter>
        <action android:name="com.microsoft.azure.engagement.reach.intent.action.LOADING"/>
        <category android:name="android.intent.category.DEFAULT"/>
      </intent-filter>
    </activity>

### <a name="resources"></a><span data-ttu-id="0a622-129">Ressources</span><span class="sxs-lookup"><span data-stu-id="0a622-129">Resources</span></span>
<span data-ttu-id="0a622-130">Intégrez le nouveau fichier `res/layout/engagement_loading.xml` dans votre projet.</span><span class="sxs-lookup"><span data-stu-id="0a622-130">Embed the new `res/layout/engagement_loading.xml` file into your project.</span></span>

## <a name="from-240-to-300"></a><span data-ttu-id="0a622-131">Migration de 2.4.0 vers 3.0.0</span><span class="sxs-lookup"><span data-stu-id="0a622-131">From 2.4.0 to 3.0.0</span></span>
<span data-ttu-id="0a622-132">La section qui suit décrit comment migrer une intégration du SDK à partir du service Capptain offert par Capptain SAS dans une application reposant sur Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="0a622-132">The following describes how to migrate an SDK integration from the Capptain service offered by Capptain SAS into an app powered by Azure Mobile Engagement.</span></span> <span data-ttu-id="0a622-133">Si vous migrez à partir d'une version antérieure, consultez le site web de Capptain pour migrer tout d'abord vers 2.4.0, puis appliquez la procédure suivante.</span><span class="sxs-lookup"><span data-stu-id="0a622-133">If you are migrating from an earlier version, please consult the Capptain web site to migrate to 2.4.0 first and then apply the following procedure.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0a622-134">Capptain et Mobile Engagement ne sont pas les mêmes services et la procédure décrite ci-dessous explique uniquement comment migrer l'application cliente.</span><span class="sxs-lookup"><span data-stu-id="0a622-134">Capptain and Mobile Engagement are not the same services, and the procedure given below only highlights how to migrate the client app.</span></span> <span data-ttu-id="0a622-135">La migration du SDK dans l'application ne migre PAS vos données des serveurs Capptain vers les serveurs Mobile Engagement .</span><span class="sxs-lookup"><span data-stu-id="0a622-135">Migrating the SDK in the app will NOT migrate your data from the Capptain servers to the Mobile Engagement servers.</span></span>
> 
> 

### <a name="jar-file"></a><span data-ttu-id="0a622-136">Fichier JAR</span><span class="sxs-lookup"><span data-stu-id="0a622-136">JAR file</span></span>
<span data-ttu-id="0a622-137">Remplacez `capptain.jar` par `mobile-engagement-VERSION.jar` dans votre dossier `libs`.</span><span class="sxs-lookup"><span data-stu-id="0a622-137">Replace `capptain.jar` by `mobile-engagement-VERSION.jar` in your `libs` folder.</span></span>

### <a name="resource-files"></a><span data-ttu-id="0a622-138">Fichiers de ressources</span><span class="sxs-lookup"><span data-stu-id="0a622-138">Resource files</span></span>
<span data-ttu-id="0a622-139">Chaque fichier de ressources fourni (précédé de `capptain_`) doit être remplacé par un nouveau (précédé de `engagement_`).</span><span class="sxs-lookup"><span data-stu-id="0a622-139">Every resource file that we provided (prefixed by `capptain_`) has to be replaced by the new ones (prefixed with `engagement_`).</span></span>

<span data-ttu-id="0a622-140">Si vous avez personnalisé ces fichiers, vous devez réappliquer vos modifications aux nouveaux fichiers, **tous les identificateurs dans les fichiers de ressources ont également été renommés**.</span><span class="sxs-lookup"><span data-stu-id="0a622-140">If you customized those files, you have to re-apply your customization on the new files, **all the identifiers in the resource files have also been renamed**.</span></span>

### <a name="application-id"></a><span data-ttu-id="0a622-141">ID de l'application</span><span class="sxs-lookup"><span data-stu-id="0a622-141">Application ID</span></span>
<span data-ttu-id="0a622-142">Engagement utilise désormais une chaîne de connexion pour configurer les identificateurs du SDK tels que l'identificateur d'application.</span><span class="sxs-lookup"><span data-stu-id="0a622-142">Now Engagement uses a connection string to configure the SDK identifiers such as the application identifier.</span></span>

<span data-ttu-id="0a622-143">Vous devez utiliser la méthode `EngagementAgent.init` dans l'activité de votre programme de lancement comme suit :</span><span class="sxs-lookup"><span data-stu-id="0a622-143">You have to use `EngagementAgent.init` method in your launcher activity like this:</span></span>

            EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
            engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
            EngagementAgent.getInstance(this).init(engagementConfiguration);

<span data-ttu-id="0a622-144">La chaîne de connexion de votre application est affichée sur le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="0a622-144">The connection string for your application is displayed on Azure Portal.</span></span>

<span data-ttu-id="0a622-145">Supprimez tous les appels vers `CapptainAgent.configure`, car `EngagementAgent.init` remplace cette méthode.</span><span class="sxs-lookup"><span data-stu-id="0a622-145">Please remove any call to `CapptainAgent.configure` as `EngagementAgent.init` replaces that method.</span></span>

<span data-ttu-id="0a622-146">`appId` ne peut plus être configuré avec `AndroidManifest.xml`.</span><span class="sxs-lookup"><span data-stu-id="0a622-146">The `appId` can no longer be configured using `AndroidManifest.xml`.</span></span>

<span data-ttu-id="0a622-147">Supprimez cette section de votre `AndroidManifest.xml` si elle existe :</span><span class="sxs-lookup"><span data-stu-id="0a622-147">Please remove this section from your `AndroidManifest.xml` if you have it:</span></span>

            <meta-data android:name="capptain:appId" android:value="<YOUR_APPID>"/>

### <a name="java-api"></a><span data-ttu-id="0a622-148">API Java</span><span class="sxs-lookup"><span data-stu-id="0a622-148">Java API</span></span>
<span data-ttu-id="0a622-149">Chaque appel vers n'importe quelle classe Java de notre SDK doit être renommé, par exemple, `CapptainAgent.getInstance(this)` doit être renommé en `EngagementAgent.getInstance(this)`, `extends CapptainActivity` doit être renommé en `extends EngagementActivity`, etc.</span><span class="sxs-lookup"><span data-stu-id="0a622-149">Every call to any Java class of our SDK has to be renamed; for example, `CapptainAgent.getInstance(this)` must be renamed `EngagementAgent.getInstance(this)`, `extends CapptainActivity` must be renamed `extends EngagementActivity` etc...</span></span>

<span data-ttu-id="0a622-150">Si vous avez effectué l'intégration avec les fichiers de préférences de l'agent par défaut, le nom du fichier par défaut est désormais `engagement.agent`, et la clé est `engagement:agent`.</span><span class="sxs-lookup"><span data-stu-id="0a622-150">If you were integrated with default agent preference files, the default file name is now `engagement.agent` and the key is `engagement:agent`.</span></span>

<span data-ttu-id="0a622-151">Quand vous créez des annonces web, le binder Javascript est maintenant `engagementReachContent`.</span><span class="sxs-lookup"><span data-stu-id="0a622-151">When creating web announcements, the Javascript binder is now `engagementReachContent`.</span></span>

### <a name="androidmanifestxml"></a><span data-ttu-id="0a622-152">AndroidManifest.xml</span><span class="sxs-lookup"><span data-stu-id="0a622-152">AndroidManifest.xml</span></span>
<span data-ttu-id="0a622-153">De nombreuses modifications ont été apportées, le service n'est plus partagé et vous ne pouvez plus exporter un grand nombre de destinataires.</span><span class="sxs-lookup"><span data-stu-id="0a622-153">A lot of changes happened there, the service is not shared anymore, and a lot of receivers are not exportable anymore.</span></span>

<span data-ttu-id="0a622-154">La déclaration du service est plus simple, vous supprimez le filtre intent et toutes les métadonnées qu'il contient, et ajoutez `exportable=false`.</span><span class="sxs-lookup"><span data-stu-id="0a622-154">The service declaration is now simpler; remove the intent filter and all meta-data inside it, and add `exportable=false`.</span></span>

<span data-ttu-id="0a622-155">En outre, tous les éléments sont renommés pour utiliser Engagement.</span><span class="sxs-lookup"><span data-stu-id="0a622-155">Plus everything is renamed to use engagement.</span></span>

<span data-ttu-id="0a622-156">Vous devez obtenir quelque chose similaire à ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="0a622-156">It now looks like:</span></span>

            <service
              android:name="com.microsoft.azure.engagement.service.EngagementService"
              android:exported="false"
              android:label="<Your application name>Service"
              android:process=":Engagement"/>

<span data-ttu-id="0a622-157">Pour l'activation des journaux de tests, les métadonnées ont été déplacées dans la balise application et renommées :</span><span class="sxs-lookup"><span data-stu-id="0a622-157">When you want to enable test logs, the meta-data has now been moved to the application tag and has been renamed:</span></span>

            <application>

              <meta-data android:name="engagement:log:test" android:value="true" />

              <service/>

            </application>

<span data-ttu-id="0a622-158">Toutes les autres métadonnées ont simplement été renommées, en voici la liste complète (renommez uniquement celles que vous utilisez) :</span><span class="sxs-lookup"><span data-stu-id="0a622-158">All other meta-data have just been renamed, here is the full list (of course rename only the ones you use):</span></span>

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

<span data-ttu-id="0a622-159">Le suivi de Google Play et SmartAd a été supprimé du SDK, il vous suffit le supprimer sans le remplacer :</span><span class="sxs-lookup"><span data-stu-id="0a622-159">Google Play and SmartAd tracking has been removed from SDK you just have to remove this without replacement:</span></span>

            <meta-data 
                android:name="capptain:track:installReferrerForwardList"
                android:value="com.class1,com.class2"/>
            <meta-data
                android:name="capptain:track:adservers"
                android:value="smartad" />

<span data-ttu-id="0a622-160">Les activités Reach sont maintenant déclarées comme suit :</span><span class="sxs-lookup"><span data-stu-id="0a622-160">The Reach activities are now declared like this:</span></span>

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

<span data-ttu-id="0a622-161">Si vous avez personnalisé des activités Reach, vous devez simplement remplacer les actions intent par `com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT` ou `com.microsoft.azure.engagement.reach.intent.action.POLL`.</span><span class="sxs-lookup"><span data-stu-id="0a622-161">If you have custom Reach activities, you need only to change the intent actions to match either `com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT` or `com.microsoft.azure.engagement.reach.intent.action.POLL`.</span></span>

<span data-ttu-id="0a622-162">Les récepteurs de diffusion ont été renommés, et nous ajoutons maintenant `exported=false`.</span><span class="sxs-lookup"><span data-stu-id="0a622-162">The broadcast receivers have been renamed, plus we now add `exported=false`.</span></span> <span data-ttu-id="0a622-163">Voici la liste complète des récepteurs avec la nouvelle spécification, (renommez uniquement ceux que vous utilisez) :</span><span class="sxs-lookup"><span data-stu-id="0a622-163">Here is the full list of the receivers with the new specification, (of course rename only the ones you use):</span></span>

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

<span data-ttu-id="0a622-164">Le récepteur de suivi a été supprimé, par conséquent, vous devez supprimer cette section :</span><span class="sxs-lookup"><span data-stu-id="0a622-164">Tracking receiver has been removed, so you have to remove this section:</span></span>

          <receiver android:name="com.ubikod.capptain.android.sdk.track.CapptainTrackReceiver">
            <intent-filter>
              <action android:name="com.ubikod.capptain.intent.action.APPID_GOT" />
              <!-- possibly <action android:name="com.android.vending.INSTALL_REFERRER" /> -->
            </intent-filter>
          </receiver>

<span data-ttu-id="0a622-165">Notez que la déclaration de votre implémentation du récepteur de diffusion **EngagementMessageReceiver** a changé dans `AndroidManifest.xml`.</span><span class="sxs-lookup"><span data-stu-id="0a622-165">Note that the declaration of your implementation of the broadcast receiver **EngagementMessageReceiver** has changed in the `AndroidManifest.xml`.</span></span> <span data-ttu-id="0a622-166">En effet, l'API permettant d'envoyer et de supprimer des messages XMPP arbitraires d'entités XMPP arbitraires, et l'API permettant d'envoyer et de recevoir des messages entre appareils ont été supprimées.</span><span class="sxs-lookup"><span data-stu-id="0a622-166">This is because the API to send and remove arbitrary XMPP messages from arbitrary XMPP entities and the API to send and receive messages between devices have been removed.</span></span> <span data-ttu-id="0a622-167">Par conséquent, vous devez également supprimer les rappels suivants de votre implémentation de **EngagementMessageReceiver** :</span><span class="sxs-lookup"><span data-stu-id="0a622-167">Thus, you have also to delete the following callbacks from your **EngagementMessageReceiver** implementation :</span></span>

            protected void onDeviceMessageReceived(android.content.Context context, java.lang.String deviceId, java.lang.String payload)

<span data-ttu-id="0a622-168">and</span><span class="sxs-lookup"><span data-stu-id="0a622-168">and</span></span>

            protected void onXMPPMessageReceived(android.content.Context context, android.os.Bundle message)

<span data-ttu-id="0a622-169">puis supprimez tout appel sur **EngagementAgent** dans :</span><span class="sxs-lookup"><span data-stu-id="0a622-169">then delete any call on **EngagementAgent** for :</span></span>

            sendMessageToDevice(java.lang.String deviceId, java.lang.String payload, java.lang.String packageName)

<span data-ttu-id="0a622-170">and</span><span class="sxs-lookup"><span data-stu-id="0a622-170">and</span></span>

            sendXMPPMessage(android.os.Bundle msg)

### <a name="proguard"></a><span data-ttu-id="0a622-171">Proguard</span><span class="sxs-lookup"><span data-stu-id="0a622-171">Proguard</span></span>
<span data-ttu-id="0a622-172">La configuration de Proguard peut être affectée par le changement de nom, les règles ressemblent maintenant à ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="0a622-172">Proguard configuration can be impacted by rebranding, the rules are now looking like:</span></span>

            -dontwarn android.**
            -keep class android.support.v4.** { *; }

            -keep public class * extends android.os.IInterface
            -keep class com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity$EngagementReachContentJS {
              <methods>;
            }

