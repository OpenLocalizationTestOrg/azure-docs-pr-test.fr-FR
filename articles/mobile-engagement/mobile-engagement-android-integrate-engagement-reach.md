---
title: "aaaAzure intégration du Kit de développement logiciel Android Mobile Engagement"
description: "Dernières mises à jour et procédures du SDK Android pour Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 9ec3fab3-35ec-458e-bf41-6cdd69e3fa44
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 06/27/2016
ms.author: piyushjo
ms.openlocfilehash: 4ab6143771bdc0758a548abb529d6bde98fc0e4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toointegrate-engagement-reach-on-android"></a><span data-ttu-id="39c7b-103">Comment les tooIntegrate Engagement sur Android</span><span class="sxs-lookup"><span data-stu-id="39c7b-103">How tooIntegrate Engagement Reach on Android</span></span>
> [!IMPORTANT]
> <span data-ttu-id="39c7b-104">Vous devez suivre la procédure d’intégration hello décrite dans hello comment tooIntegrate Engagement sur Android document avant de suivre ce guide.</span><span class="sxs-lookup"><span data-stu-id="39c7b-104">You must follow hello integration procedure described in hello How tooIntegrate Engagement on Android document before following this guide.</span></span>
> 
> 

## <a name="standard-integration"></a><span data-ttu-id="39c7b-105">Intégration standard</span><span class="sxs-lookup"><span data-stu-id="39c7b-105">Standard integration</span></span>

<span data-ttu-id="39c7b-106">Copiez les fichiers de ressources de portée de hello SDK dans votre projet :</span><span class="sxs-lookup"><span data-stu-id="39c7b-106">Copy Reach resource files from hello SDK in your project :</span></span>

* <span data-ttu-id="39c7b-107">Copiez les fichiers hello hello `res/layout` dossier fourni avec le Kit de développement logiciel de hello en hello `res/layout` dossier de votre application.</span><span class="sxs-lookup"><span data-stu-id="39c7b-107">Copy hello files from hello `res/layout` folder delivered with hello SDK into hello `res/layout` folder of your application.</span></span>
* <span data-ttu-id="39c7b-108">Copiez les fichiers hello hello `res/drawable` dossier fourni avec le Kit de développement logiciel de hello en hello `res/drawable` dossier de votre application.</span><span class="sxs-lookup"><span data-stu-id="39c7b-108">Copy hello files from hello `res/drawable` folder delivered with hello SDK into hello `res/drawable` folder of your application.</span></span>

<span data-ttu-id="39c7b-109">Modifiez le fichier `AndroidManifest.xml` :</span><span class="sxs-lookup"><span data-stu-id="39c7b-109">Edit your `AndroidManifest.xml` file:</span></span>

* <span data-ttu-id="39c7b-110">Ajouter hello après section (entre hello `<application>` et `</application>` balises) :</span><span class="sxs-lookup"><span data-stu-id="39c7b-110">Add hello following section (between hello `<application>` and `</application>` tags):</span></span>
  
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
          <receiver android:name="com.microsoft.azure.engagement.reach.EngagementReachReceiver" android:exported="false">
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
* <span data-ttu-id="39c7b-111">Vous avez besoin de cette autorisation tooreplay système les notifications qui n’étaient pas activés au démarrage (sinon ils seront conservés sur le disque, mais ne s’affiche plus, vous devez tooinclude cela).</span><span class="sxs-lookup"><span data-stu-id="39c7b-111">You need this permission tooreplay system notifications that were not clicked at boot (otherwise they will be kept on disk but won't be displayed anymore, you really have tooinclude this).</span></span>
  
          <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />
* <span data-ttu-id="39c7b-112">Spécifier une icône utilisée pour les notifications (à la fois dans l’application et ceux de système) en copiant et en modifiant les hello après section (entre hello `<application>` et `</application>` balises) :</span><span class="sxs-lookup"><span data-stu-id="39c7b-112">Specify an icon used for notifications (both in app and system ones) by copying and editing hello following section (between hello `<application>` and `</application>` tags):</span></span>
  
          <meta-data android:name="engagement:reach:notification:icon" android:value="<name_of_icon_WITHOUT_file_extension_and_WITHOUT_'@drawable/'>" />

> [!IMPORTANT]
> <span data-ttu-id="39c7b-113">Cette section est **obligatoire** si vous prévoyez d'utiliser les notifications système lors de la création de campagnes de couverture.</span><span class="sxs-lookup"><span data-stu-id="39c7b-113">This section is **mandatory** if you plan on using system notifications when creating Reach campaigns.</span></span> <span data-ttu-id="39c7b-114">Android empêche les notifications système sans icône de s'afficher.</span><span class="sxs-lookup"><span data-stu-id="39c7b-114">Android prevents system notifications without icons from being shown.</span></span> <span data-ttu-id="39c7b-115">Si vous omettez cette section, vos utilisateurs finaux seront donc pas en mesure de tooreceive les.</span><span class="sxs-lookup"><span data-stu-id="39c7b-115">So if you omit this section, your end users will not be able tooreceive them.</span></span>
> 
> 

* <span data-ttu-id="39c7b-116">Si vous créez des campagnes avec les notifications système à l’aide de la vue d’ensemble, vous devez hello tooadd les autorisations suivantes (après hello `</application>` balise) si manquant :</span><span class="sxs-lookup"><span data-stu-id="39c7b-116">If you create campaigns with system notifications using big picture, you need tooadd hello following permissions (after hello `</application>` tag) if missing:</span></span>
  
          <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
          <uses-permission android:name="android.permission.DOWNLOAD_WITHOUT_NOTIFICATION"/>
  
  * <span data-ttu-id="39c7b-117">Sur Android M et si votre application cible un niveau d’API Android 23 ou supérieur, l’autorisation ``WRITE_EXTERNAL_STORAGE`` nécessite l’approbation de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="39c7b-117">On Android M and if your application targets Android API level 23 or greater, ``WRITE_EXTERNAL_STORAGE`` permission requires user approval.</span></span> <span data-ttu-id="39c7b-118">Veuillez lire [cette section](mobile-engagement-android-integrate-engagement.md#android-m-permissions).</span><span class="sxs-lookup"><span data-stu-id="39c7b-118">Please read [this section](mobile-engagement-android-integrate-engagement.md#android-m-permissions).</span></span>
* <span data-ttu-id="39c7b-119">Pour les notifications système que vous pouvez également spécifier dans hello atteindre campagne si l’appareil de hello doit sonner et/ou faire vibrer.</span><span class="sxs-lookup"><span data-stu-id="39c7b-119">For system notifications you can also specify in hello Reach campaign if hello device should ring and/or vibrate.</span></span> <span data-ttu-id="39c7b-120">Pour qu’il toowork, que vous avez toomake que vous avez déclaré hello suivant d’autorisation (après hello `</application>` étiquette) :</span><span class="sxs-lookup"><span data-stu-id="39c7b-120">For it toowork, you have toomake sure you declared hello following permission (after hello `</application>` tag):</span></span>
  
          <uses-permission android:name="android.permission.VIBRATE" />
  
  <span data-ttu-id="39c7b-121">Sans cette autorisation, Android empêche les notifications système est affichée si vous avez coché anneau de hello ou hello faire vibrer option dans le Gestionnaire d’atteindre une campagne hello.</span><span class="sxs-lookup"><span data-stu-id="39c7b-121">Without this permission, Android prevents system notifications from being shown if you checked hello ring or hello vibrate option in hello Reach Campaign manager.</span></span>

## <a name="native-push"></a><span data-ttu-id="39c7b-122">Native Push</span><span class="sxs-lookup"><span data-stu-id="39c7b-122">Native Push</span></span>
<span data-ttu-id="39c7b-123">Maintenant que vous avez configuré le module de couverture, vous devez tooconfigure push natif toobe tooreceive en mesure de hello campagnes marketing sur les appareils hello.</span><span class="sxs-lookup"><span data-stu-id="39c7b-123">Now that you configured Reach module, you need tooconfigure native push toobe able tooreceive hello campaigns on hello device.</span></span>

<span data-ttu-id="39c7b-124">Nous prenons en charge les deux services sur Android :</span><span class="sxs-lookup"><span data-stu-id="39c7b-124">We support two services on Android:</span></span>

* <span data-ttu-id="39c7b-125">Les appareils Google Play : utilisez [messagerie Cloud Google] par hello suivant [comment tooIntegrate GCM avec Engagement guide](mobile-engagement-android-gcm-integrate.md) guide.</span><span class="sxs-lookup"><span data-stu-id="39c7b-125">Google Play devices: Use [Google Cloud Messaging] by following hello [How tooIntegrate GCM with Engagement guide](mobile-engagement-android-gcm-integrate.md) guide.</span></span>
* <span data-ttu-id="39c7b-126">Les appareils Amazon : utilisez [Amazon Device Messaging] par hello suivant [comment tooIntegrate ADM avec Engagement guide](mobile-engagement-android-adm-integrate.md) guide.</span><span class="sxs-lookup"><span data-stu-id="39c7b-126">Amazon devices: Use [Amazon Device Messaging] by following hello [How tooIntegrate ADM with Engagement guide](mobile-engagement-android-adm-integrate.md) guide.</span></span>

<span data-ttu-id="39c7b-127">Si vous souhaitez tootarget appareils Amazon et Google Play, ses toohave possible tout son contenu 1 AndroidManifest.xml/APK pour le développement.</span><span class="sxs-lookup"><span data-stu-id="39c7b-127">If you want tootarget both Amazon and Google Play devices, its possible toohave everything inside 1 AndroidManifest.xml/APK for development.</span></span> <span data-ttu-id="39c7b-128">Mais lorsque vous soumettez tooAmazon, ils peuvent rejeter votre application s’ils trouvent le code GCM.</span><span class="sxs-lookup"><span data-stu-id="39c7b-128">But when submitting tooAmazon, they may reject your application if they find GCM code.</span></span>

<span data-ttu-id="39c7b-129">Dans ce cas, vous devrez utiliser plusieurs fichiers APK.</span><span class="sxs-lookup"><span data-stu-id="39c7b-129">You should use multiple APKs in that case.</span></span>

<span data-ttu-id="39c7b-130">**Votre application est maintenant prêt tooreceive et affichage atteint campagnes !**</span><span class="sxs-lookup"><span data-stu-id="39c7b-130">**Your application is now ready tooreceive and display reach campaigns!**</span></span>

## <a name="how-toohandle-data-push"></a><span data-ttu-id="39c7b-131">Comment les données toohandle push</span><span class="sxs-lookup"><span data-stu-id="39c7b-131">How toohandle data push</span></span>
### <a name="integration"></a><span data-ttu-id="39c7b-132">Intégration</span><span class="sxs-lookup"><span data-stu-id="39c7b-132">Integration</span></span>
<span data-ttu-id="39c7b-133">Si vous souhaitez que votre application toobe en mesure d’exécute un push de tooreceive les données de couverture, que vous avez toocreate une sous-classe de `com.microsoft.azure.engagement.reach.EngagementReachDataPushReceiver` et référencez-la dans hello `AndroidManifest.xml` fichier (entre hello `<application>` et/ou `</application>` balises) :</span><span class="sxs-lookup"><span data-stu-id="39c7b-133">If you want your application toobe able tooreceive Reach data pushes, you have toocreate a sub-class of `com.microsoft.azure.engagement.reach.EngagementReachDataPushReceiver` and reference it in hello `AndroidManifest.xml` file (between hello `<application>` and/or `</application>` tags):</span></span>

            <receiver android:name="<your_sub_class_of_com.microsoft.azure.engagement.reach.EngagementReachDataPushReceiver>"
              android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.DATA_PUSH" />
              </intent-filter>
            </receiver>

<span data-ttu-id="39c7b-134">Vous pouvez remplacer hello `onDataPushStringReceived` et `onDataPushBase64Received` rappels.</span><span class="sxs-lookup"><span data-stu-id="39c7b-134">Then you can override hello `onDataPushStringReceived` and `onDataPushBase64Received` callbacks.</span></span> <span data-ttu-id="39c7b-135">Voici un exemple :</span><span class="sxs-lookup"><span data-stu-id="39c7b-135">Here is an example:</span></span>

            public class MyDataPushReceiver extends EngagementReachDataPushReceiver
            {
              @Override
              protected Boolean onDataPushStringReceived(Context context, String category, String body)
              {
                Log.d("tmp", "String data push message received: " + body);
                return true;
              }

              @Override
              protected Boolean onDataPushBase64Received(Context context, String category, byte[] decodedBody, String encodedBody)
              {
                Log.d("tmp", "Base64 data push message received: " + encodedBody);
                // Do something useful with decodedBody like updating an image view
                return true;
              }
            }

### <a name="category"></a><span data-ttu-id="39c7b-136">Catégorie</span><span class="sxs-lookup"><span data-stu-id="39c7b-136">Category</span></span>
<span data-ttu-id="39c7b-137">paramètre de catégorie Hello est facultatif lorsque vous créez une campagne de Push de données et permet de que vous toofilter données exécute un push.</span><span class="sxs-lookup"><span data-stu-id="39c7b-137">hello category parameter is optional when you create a Data Push campaign and allows you toofilter data pushes.</span></span> <span data-ttu-id="39c7b-138">Cela est utile si vous avez plusieurs récepteurs de diffusion la gestion des différents types de push de données, ou si vous souhaitez toopush différents types de `Base64` tooidentify de données et que vous souhaitez leur type avant de les analyser.</span><span class="sxs-lookup"><span data-stu-id="39c7b-138">This is useful if you have several broadcast receivers handling different types of data pushes, or if you want toopush different kinds of `Base64` data and want tooidentify their type before parsing them.</span></span>

### <a name="callbacks-return-parameter"></a><span data-ttu-id="39c7b-139">Paramètre de retour des rappels</span><span class="sxs-lookup"><span data-stu-id="39c7b-139">Callbacks' return parameter</span></span>
<span data-ttu-id="39c7b-140">Voici quelques recommandations tooproperly handle hello paramètre de retour de `onDataPushStringReceived` et `onDataPushBase64Received`:</span><span class="sxs-lookup"><span data-stu-id="39c7b-140">Here are some guidelines tooproperly handle hello return parameter of `onDataPushStringReceived` and `onDataPushBase64Received`:</span></span>

* <span data-ttu-id="39c7b-141">Un récepteur de diffusion doit retourner `null` dans le rappel hello si elles ne savent pas comment toohandle données push.</span><span class="sxs-lookup"><span data-stu-id="39c7b-141">A broadcast receiver should return `null` in hello callback if it does not know how toohandle a data push.</span></span> <span data-ttu-id="39c7b-142">Vous devez utiliser hello catégorie toodetermine si votre récepteur de diffusion doit gérer la transmission de données hello ou non.</span><span class="sxs-lookup"><span data-stu-id="39c7b-142">You should use hello category toodetermine whether your broadcast receiver should handle hello data push or not.</span></span>
* <span data-ttu-id="39c7b-143">Un récepteur de diffusion hello doit retourner `true` dans le rappel hello si ce dernier accepte push de données hello.</span><span class="sxs-lookup"><span data-stu-id="39c7b-143">One of hello broadcast receiver should return `true` in hello callback if it accepts hello data push.</span></span>
* <span data-ttu-id="39c7b-144">Un récepteur de diffusion hello doit retourner `false` dans le rappel hello s’il reconnaît le push de données hello, mais il ignore pour une raison quelconque.</span><span class="sxs-lookup"><span data-stu-id="39c7b-144">One of hello broadcast receiver should return `false` in hello callback if it recognizes hello data push, but discards it for whatever reason.</span></span> <span data-ttu-id="39c7b-145">Par exemple, retourner `false` lorsque les données de salutation reçue ne sont pas valides.</span><span class="sxs-lookup"><span data-stu-id="39c7b-145">For example, return `false` when hello received data is invalid.</span></span>
* <span data-ttu-id="39c7b-146">Si une diffusion récepteur retourne `true` tandis que l’autre un retourne `false` pour hello même push de données, le comportement de hello n’est pas défini, vous devez le faire jamais.</span><span class="sxs-lookup"><span data-stu-id="39c7b-146">If one broadcast receiver returns `true` while another one returns `false` for hello same data push, hello behavior is undefined, you should never do that.</span></span>

<span data-ttu-id="39c7b-147">type de retour Hello est utilisé uniquement pour les statistiques de couverture hello :</span><span class="sxs-lookup"><span data-stu-id="39c7b-147">hello return type is used only for hello Reach statistics:</span></span>

* <span data-ttu-id="39c7b-148">`Replied`est incrémenté si un des récepteurs de diffusion hello renvoyées `true` ou `false`.</span><span class="sxs-lookup"><span data-stu-id="39c7b-148">`Replied` is incremented if one of hello broadcast receivers returned either `true` or `false`.</span></span>
* <span data-ttu-id="39c7b-149">`Actioned`est incrémenté uniquement si un des hello diffusion récepteurs retournés `true`.</span><span class="sxs-lookup"><span data-stu-id="39c7b-149">`Actioned` is incremented only if one of hello broadcast receivers returned `true`.</span></span>

## <a name="how-toocustomize-campaigns"></a><span data-ttu-id="39c7b-150">Comment les campagnes toocustomize</span><span class="sxs-lookup"><span data-stu-id="39c7b-150">How toocustomize campaigns</span></span>
<span data-ttu-id="39c7b-151">toocustomize campagnes, vous pouvez modifier les présentations hello Bonjour SDK Reach.</span><span class="sxs-lookup"><span data-stu-id="39c7b-151">toocustomize campaigns, you can modify hello layouts provided in hello Reach SDK.</span></span>

<span data-ttu-id="39c7b-152">Vous devez conserver tous les identificateurs hello sont utilisées dans les dispositions de hello et maintenir des types hello de vues hello qui utilisent un identificateur, en particulier pour les affichages de texte et image.</span><span class="sxs-lookup"><span data-stu-id="39c7b-152">You should keep all hello identifiers used in hello layouts and keep hello types of hello views that use an identifier, especially for text views and image views.</span></span> <span data-ttu-id="39c7b-153">Certaines vues sont toohide uniquement utilisé ou affichent les zones de leur type peut être modifié.</span><span class="sxs-lookup"><span data-stu-id="39c7b-153">Some views are just used toohide or show areas so their type may be changed.</span></span> <span data-ttu-id="39c7b-154">Vérifiez le code source de hello si vous envisagez de type hello de toochange d’une vue dans les dispositions de hello fourni.</span><span class="sxs-lookup"><span data-stu-id="39c7b-154">Please check hello source code if you intend toochange hello type of a view in hello provided layouts.</span></span>

### <a name="notifications"></a><span data-ttu-id="39c7b-155">Notifications</span><span class="sxs-lookup"><span data-stu-id="39c7b-155">Notifications</span></span>
<span data-ttu-id="39c7b-156">Il existe deux types de notifications : les notifications système et les notifications dans l'application qui utilisent des fichiers de disposition différents.</span><span class="sxs-lookup"><span data-stu-id="39c7b-156">There are two types of notifications: system and in-app notifications which use different layout files.</span></span>

#### <a name="system-notifications"></a><span data-ttu-id="39c7b-157">Notifications système</span><span class="sxs-lookup"><span data-stu-id="39c7b-157">System notifications</span></span>
<span data-ttu-id="39c7b-158">les notifications système toocustomize vous devez toouse hello **catégories**.</span><span class="sxs-lookup"><span data-stu-id="39c7b-158">toocustomize system notifications you need toouse hello **categories**.</span></span> <span data-ttu-id="39c7b-159">Vous pouvez passer trop[catégories](#categories).</span><span class="sxs-lookup"><span data-stu-id="39c7b-159">You can jump too[Categories](#categories).</span></span>

#### <a name="in-app-notifications"></a><span data-ttu-id="39c7b-160">Notifications dans l'application</span><span class="sxs-lookup"><span data-stu-id="39c7b-160">In-app notifications</span></span>
<span data-ttu-id="39c7b-161">Par défaut, une notification dans l’application est une vue qui est la méthode Android toohello ajoutées de manière dynamique actuelle activité utilisateur interface Merci toohello `addContentView()`.</span><span class="sxs-lookup"><span data-stu-id="39c7b-161">By default, an in-app notification is a view that is dynamically added toohello current activity user interface thanks toohello Android method `addContentView()`.</span></span> <span data-ttu-id="39c7b-162">Il s'agit d'une superposition de notification.</span><span class="sxs-lookup"><span data-stu-id="39c7b-162">This is called a notification overlay.</span></span> <span data-ttu-id="39c7b-163">Superpositions de notification sont parfaites pour une intégration rapide, car ils ne nécessitent pas vous toomodify toute disposition dans votre application.</span><span class="sxs-lookup"><span data-stu-id="39c7b-163">Notification overlays are great for a fast integration because they do not require you toomodify any layout in your application.</span></span>

<span data-ttu-id="39c7b-164">apparence hello toomodify votre superpositions de notification, il suffit de modifier le fichier de hello `engagement_notification_area.xml` tooyour a besoin.</span><span class="sxs-lookup"><span data-stu-id="39c7b-164">toomodify hello look of your notification overlays, you can simply modify hello file `engagement_notification_area.xml` tooyour needs.</span></span>

> [!NOTE]
> <span data-ttu-id="39c7b-165">fichier de Hello `engagement_notification_overlay.xml` est celui utilisé toocreate hello du segment de recouvrement de la notification, elle inclut les fichiers hello `engagement_notification_area.xml`.</span><span class="sxs-lookup"><span data-stu-id="39c7b-165">hello file `engagement_notification_overlay.xml` is hello one that is used toocreate a notification overlay, it includes hello file `engagement_notification_area.xml`.</span></span> <span data-ttu-id="39c7b-166">Vous pouvez également personnaliser toosuit (par exemple pour positionner la zone de notification hello dans un segment de recouvrement hello) de vos besoins.</span><span class="sxs-lookup"><span data-stu-id="39c7b-166">You can also customize it toosuit your needs (such as for positioning hello notification area within hello overlay).</span></span>
> 
> 

##### <a name="include-notification-layout-as-part-of-an-activity-layout"></a><span data-ttu-id="39c7b-167">Inclure une disposition de notification dans une disposition d'activité</span><span class="sxs-lookup"><span data-stu-id="39c7b-167">Include notification layout as part of an activity layout</span></span>
<span data-ttu-id="39c7b-168">Les superpositions sont idéales pour une intégration rapide, mais peuvent être gênantes ou avoir des effets indésirables dans certains cas.</span><span class="sxs-lookup"><span data-stu-id="39c7b-168">Overlays are great for a fast integration but can be inconvenient or have side effects in special cases.</span></span> <span data-ttu-id="39c7b-169">Hello superposition système peut être personnalisé à un niveau d’activité, rendant les effets secondaires tooprevent facile pour les activités spéciales.</span><span class="sxs-lookup"><span data-stu-id="39c7b-169">hello overlay system can be customized at an activity level, making it easy tooprevent side effects for special activities.</span></span>

<span data-ttu-id="39c7b-170">Vous pouvez décider tooinclude à notre disposition de notification dans votre toohello Merci d’existant disposition Android **incluent** instruction.</span><span class="sxs-lookup"><span data-stu-id="39c7b-170">You can decide tooinclude our notification layout in your existing layout thanks toohello Android **include** statement.</span></span> <span data-ttu-id="39c7b-171">Hello Voici un exemple d’une modification `ListActivity` disposition contenant simplement un `ListView`.</span><span class="sxs-lookup"><span data-stu-id="39c7b-171">hello following is an example of a modified `ListActivity` layout containing just a `ListView`.</span></span>

<span data-ttu-id="39c7b-172">**Avant l'intégration d'Engagement :**</span><span class="sxs-lookup"><span data-stu-id="39c7b-172">**Before Engagement integration :**</span></span>

            <?xml version="1.0" encoding="utf-8"?>
            <ListView
              xmlns:android="http://schemas.android.com/apk/res/android"
              android:id="@android:id/list"
              android:layout_width="fill_parent"
              android:layout_height="fill_parent" />

<span data-ttu-id="39c7b-173">**Après l'intégration d'Engagement :**</span><span class="sxs-lookup"><span data-stu-id="39c7b-173">**After Engagement integration :**</span></span>

            <?xml version="1.0" encoding="utf-8"?>
            <LinearLayout
              xmlns:android="http://schemas.android.com/apk/res/android"
              android:orientation="vertical"
              android:layout_width="fill_parent"
              android:layout_height="fill_parent">

              <ListView
                android:id="@android:id/list"
                android:layout_width="fill_parent"
                android:layout_height="fill_parent"
                android:layout_weight="1" />

              <include layout="@layout/engagement_notification_area" />

            </LinearLayout>

<span data-ttu-id="39c7b-174">Dans cet exemple, nous avons ajouté un conteneur parent car mise hello utilisé un affichage de liste en tant qu’élément de niveau supérieur hello.</span><span class="sxs-lookup"><span data-stu-id="39c7b-174">In this example we added a parent container since hello original layout used a list view as hello top level element.</span></span> <span data-ttu-id="39c7b-175">Nous avons également ajouté `android:layout_weight="1"` tooadd en mesure de toobe une vue au-dessous d’un affichage de liste configurés avec `android:layout_height="fill_parent"`.</span><span class="sxs-lookup"><span data-stu-id="39c7b-175">We also added `android:layout_weight="1"` toobe able tooadd a view below a list view configured with `android:layout_height="fill_parent"`.</span></span>

<span data-ttu-id="39c7b-176">Hello SDK Reach d’Engagement détecte automatiquement cette mise en page de notification hello est inclus dans cette activité et n’ajoute pas d’un segment de recouvrement pour cette activité.</span><span class="sxs-lookup"><span data-stu-id="39c7b-176">hello Engagement Reach SDK automatically detects that hello notification layout is included in this activity and will not add an overlay for this activity.</span></span>

> [!TIP]
> <span data-ttu-id="39c7b-177">Si vous utilisez un ListActivity dans votre application, un segment de recouvrement portée visible vous empêcheront les éléments tooclicked réaction en mode hello plus.</span><span class="sxs-lookup"><span data-stu-id="39c7b-177">If you use a ListActivity in your application, a visible Reach overlay will prevent you from reacting tooclicked items in hello list view anymore.</span></span> <span data-ttu-id="39c7b-178">Il s'agit d'un problème connu.</span><span class="sxs-lookup"><span data-stu-id="39c7b-178">This is a known issue.</span></span> <span data-ttu-id="39c7b-179">toowork résoudre ce problème, nous vous suggérons tooembed hello notification mise en page dans votre propre disposition de liste d’activités, comme dans l’exemple précédent hello.</span><span class="sxs-lookup"><span data-stu-id="39c7b-179">toowork around this problem we suggest you tooembed hello notification layout in your own list activity layout like in hello previous sample.</span></span>
> 
> 

##### <a name="disabling-application-notification-per-activity"></a><span data-ttu-id="39c7b-180">Désactivation des notifications d'application par activité</span><span class="sxs-lookup"><span data-stu-id="39c7b-180">Disabling application notification per activity</span></span>
<span data-ttu-id="39c7b-181">Si vous ne souhaitez pas hello superposition toobe ajouté tooyour activité, et si vous n’incluez pas mise en page de notification hello dans votre propre mise en page, vous pouvez désactiver la superposition hello pour cette activité Bonjour `AndroidManifest.xml` en ajoutant un `meta-data` section comme dans les éléments suivants de hello exemple :</span><span class="sxs-lookup"><span data-stu-id="39c7b-181">If you don't want hello overlay toobe added tooyour activity, and if you don't include hello notification layout in your own layout, you can disable hello overlay for this activity in hello `AndroidManifest.xml` by adding a `meta-data` section like in hello following example:</span></span>

            <activity android:name="SplashScreenActivity">
              <meta-data android:name="engagement:notification:overlay" android:value="false"/>
            </activity>

#### <span data-ttu-id="39c7b-182"><a name="categories"></a> Catégories</span><span class="sxs-lookup"><span data-stu-id="39c7b-182"><a name="categories"></a> Categories</span></span>
<span data-ttu-id="39c7b-183">Lorsque vous modifiez hello fourni mises en page, vous modifiez apparence hello toutes vos notifications.</span><span class="sxs-lookup"><span data-stu-id="39c7b-183">When you modify hello provided layouts, you modify hello look of all your notifications.</span></span> <span data-ttu-id="39c7b-184">Les catégories permettent toodefine que différents ciblés recherche (et éventuellement des comportements) pour les notifications.</span><span class="sxs-lookup"><span data-stu-id="39c7b-184">Categories allow you toodefine various targeted looks (possibly behaviors) for notifications.</span></span> <span data-ttu-id="39c7b-185">Une catégorie peut être spécifiée lorsque vous créez une campagne Reach.</span><span class="sxs-lookup"><span data-stu-id="39c7b-185">A category can be specified when you create a Reach campaign.</span></span> <span data-ttu-id="39c7b-186">N'oubliez pas que les catégories vous permettent également de personnaliser les annonces et les sondages, décrits plus avant dans ce document.</span><span class="sxs-lookup"><span data-stu-id="39c7b-186">Keep in mind that categories also let you customize announcements and polls, that is described later in this document.</span></span>

<span data-ttu-id="39c7b-187">tooregister un gestionnaire de catégorie pour les notifications, vous devez tooadd un appel lorsque l’application hello est initialisée.</span><span class="sxs-lookup"><span data-stu-id="39c7b-187">tooregister a category handler for your notifications, you need tooadd a call when hello application is initialized.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="39c7b-188">Veuillez lire avertissement hello sur hello android : traiter l’attribut \<android-sdk-engagement-process\> Bonjour comment tooIntegrate Engagement sur la rubrique Android avant de continuer.</span><span class="sxs-lookup"><span data-stu-id="39c7b-188">Please read hello warning about hello android:process attribute \<android-sdk-engagement-process\> in hello How tooIntegrate Engagement on Android topic before proceeding.</span></span>
> 
> 

<span data-ttu-id="39c7b-189">Hello exemple suivant suppose que vous les avertissement précédent hello d’accusé de réception et que vous utilisez une sous-classe de `EngagementApplication`:</span><span class="sxs-lookup"><span data-stu-id="39c7b-189">hello following example assumes you acknowledged hello previous warning and use a sub-class of `EngagementApplication`:</span></span>

            public class MyApplication extends EngagementApplication
            {
              @Override
              protected void onApplicationProcessCreate()
              {
                // [...] other init
                EngagementReachAgent reachAgent = EngagementReachAgent.getInstance(this);
                reachAgent.registerNotifier(new MyNotifier(this), "myCategory");
              }
            }

<span data-ttu-id="39c7b-190">Hello `MyNotifier` objet est mise en oeuvre de hello du Gestionnaire de catégorie de notification hello.</span><span class="sxs-lookup"><span data-stu-id="39c7b-190">hello `MyNotifier` object is hello implementation of hello notification category handler.</span></span> <span data-ttu-id="39c7b-191">Il s’agit d’une mise en œuvre de hello `EngagementNotifier` interface ou une sous-classe de l’implémentation par défaut de hello : `EngagementDefaultNotifier`.</span><span class="sxs-lookup"><span data-stu-id="39c7b-191">It is either an implementation of hello `EngagementNotifier` interface or a sub class of hello default implementation: `EngagementDefaultNotifier`.</span></span>

<span data-ttu-id="39c7b-192">Notez que hello même notifiant peut gérer plusieurs catégories, vous pouvez les enregistrer comme suit :</span><span class="sxs-lookup"><span data-stu-id="39c7b-192">Note that hello same notifier can handle several categories, you can register them like this:</span></span>

            reachAgent.registerNotifier(new MyNotifier(this), "myCategory", "myAnotherCategory");

<span data-ttu-id="39c7b-193">tooreplace hello catégorie l’implémentation par défaut, vous pouvez inscrire votre implémentation comme Bonjour l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="39c7b-193">tooreplace hello default category implementation, you can register your implementation like in hello following example:</span></span>

            public class MyApplication extends EngagementApplication
            {
              @Override
              protected void onApplicationProcessCreate()
              {
                // [...] other init
                EngagementReachAgent reachAgent = EngagementReachAgent.getInstance(this);
                reachAgent.registerNotifier(new MyNotifier(this), Intent.CATEGORY_DEFAULT); // "android.intent.category.DEFAULT"
              }
            }

<span data-ttu-id="39c7b-194">catégorie de Hello actuelle utilisée dans un gestionnaire est passé en tant que paramètre dans la plupart des méthodes que vous pouvez substituer dans `EngagementDefaultNotifier`.</span><span class="sxs-lookup"><span data-stu-id="39c7b-194">hello current category used in a handler is passed as a parameter in most methods you can override in `EngagementDefaultNotifier`.</span></span>

<span data-ttu-id="39c7b-195">Elle est passée en tant que paramètre `String` ou indirectement dans un objet `EngagementReachContent` ayant une méthode `getCategory()`.</span><span class="sxs-lookup"><span data-stu-id="39c7b-195">It is passed either as a `String` parameter or indirectly in a `EngagementReachContent` object which has a `getCategory()` method.</span></span>

<span data-ttu-id="39c7b-196">Vous pouvez modifier la plupart des processus de création de notification hello en redéfinissant les méthodes sur `EngagementDefaultNotifier`, pour une personnalisation plus avancée sentir libre tootake un coup de œil à la documentation technique hello et au code source de hello.</span><span class="sxs-lookup"><span data-stu-id="39c7b-196">You can change most of hello notification creation process by redefining methods on `EngagementDefaultNotifier`, for more advanced customization feel free tootake a look at hello technical documentation and at hello source code.</span></span>

##### <a name="in-app-notifications"></a><span data-ttu-id="39c7b-197">Notifications dans l'application</span><span class="sxs-lookup"><span data-stu-id="39c7b-197">In-app notifications</span></span>
<span data-ttu-id="39c7b-198">Si vous souhaitez simplement toouse différentes dispositions pour une catégorie spécifique, vous pouvez implémenter cela comme hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="39c7b-198">If you just want toouse alternate layouts for a specific category, you can implement this as in hello following example:</span></span>

            public class MyNotifier extends EngagementDefaultNotifier
            {
              public MyNotifier(Context context)
              {
                super(context);
              }

              @Override
              protected int getOverlayLayoutId(String category)
              {
                return R.layout.my_notification_overlay;
              }


              @Override
              public Integer getOverlayViewId(String category)
              {
                return R.id.my_notification_overlay;
              }

              @Override
              public Integer getInAppAreaId(String category)
              {
                return R.id.my_notification_area;
              }
            }

<span data-ttu-id="39c7b-199">**Exemple de `my_notification_overlay.xml` :**</span><span class="sxs-lookup"><span data-stu-id="39c7b-199">**Example of `my_notification_overlay.xml` :**</span></span>

            <?xml version="1.0" encoding="utf-8"?>
            <RelativeLayout
              xmlns:android="http://schemas.android.com/apk/res/android"
              android:id="@+id/my_notification_overlay"
              android:layout_width="fill_parent"
              android:layout_height="fill_parent">

              <include layout="@layout/my_notification_area" />

            </RelativeLayout>

<span data-ttu-id="39c7b-200">Comme vous pouvez le voir, identificateur d’affichage superposition hello est différent de celui standard de hello un.</span><span class="sxs-lookup"><span data-stu-id="39c7b-200">As you can see, hello overlay view identifier is different than hello standard one.</span></span> <span data-ttu-id="39c7b-201">Il est important que chaque disposition utilise un identificateur unique pour les superpositions.</span><span class="sxs-lookup"><span data-stu-id="39c7b-201">It is important that each layout use a unique identifier for overlays.</span></span>

<span data-ttu-id="39c7b-202">**Exemple de `my_notification_area.xml` :**</span><span class="sxs-lookup"><span data-stu-id="39c7b-202">**Example of `my_notification_area.xml` :**</span></span>

            <?xml version="1.0" encoding="utf-8"?>
            <merge
              xmlns:android="http://schemas.android.com/apk/res/android"
              android:layout_width="fill_parent"
              android:layout_height="fill_parent">

              <RelativeLayout
                android:id="@+id/my_notification_area"
                android:layout_width="fill_parent"
                android:layout_height="64dp"
                android:layout_alignParentTop="true"
                android:background="#B000">

                <LinearLayout
                  android:orientation="horizontal"
                  android:layout_width="fill_parent"
                  android:layout_height="fill_parent"
                  android:gravity="center_vertical">

                  <ImageView
                    android:id="@+id/engagement_notification_icon"
                    android:layout_width="48dp"
                    android:layout_height="48dp" />

                  <LinearLayout
                    android:id="@+id/engagement_notification_text"
                    android:orientation="vertical"
                    android:layout_width="fill_parent"
                    android:layout_height="fill_parent"
                    android:layout_weight="1"
                    android:gravity="center_vertical">

                    <TextView
                      android:id="@+id/engagement_notification_title"
                      android:layout_width="fill_parent"
                      android:layout_height="wrap_content"
                      android:singleLine="true"
                      android:ellipsize="end"
                      android:textAppearance="@android:style/TextAppearance.Medium" />

                    <TextView
                      android:id="@+id/engagement_notification_message"
                      android:layout_width="fill_parent"
                      android:layout_height="wrap_content"
                      android:maxLines="2"
                      android:ellipsize="end"
                      android:textAppearance="@android:style/TextAppearance.Small" />

                  </LinearLayout>

                  <ImageView
                    android:id="@+id/engagement_notification_image"
                    android:layout_width="wrap_content"
                    android:layout_height="fill_parent"
                    android:adjustViewBounds="true" />

                  <ImageButton
                    android:id="@+id/engagement_notification_close_area"
                    android:visibility="invisible"
                    android:layout_width="wrap_content"
                    android:layout_height="fill_parent"
                    android:src="@android:drawable/btn_dialog"
                    android:background="#0F00" />

                </LinearLayout>

                <ImageButton
                  android:id="@+id/engagement_notification_close"
                  android:layout_width="wrap_content"
                  android:layout_height="fill_parent"
                  android:layout_alignParentRight="true"
                  android:src="@android:drawable/btn_dialog"
                  android:background="#0F00" />

              </RelativeLayout>

            </merge>

<span data-ttu-id="39c7b-203">Comme vous pouvez le voir, identificateur de vue de zone de notification hello est différente de celle standard de hello un.</span><span class="sxs-lookup"><span data-stu-id="39c7b-203">As you can see, hello notification area view identifier is different than hello standard one.</span></span> <span data-ttu-id="39c7b-204">Il est important que chaque disposition utilise un identificateur unique pour les zones de notification.</span><span class="sxs-lookup"><span data-stu-id="39c7b-204">It is important that each layout uses a unique identifier for notification areas.</span></span>

<span data-ttu-id="39c7b-205">Cet exemple simple de la catégorie rend l’application (ou dans l’application) des notifications affichées en haut de hello d’écran hello.</span><span class="sxs-lookup"><span data-stu-id="39c7b-205">This simple example of category makes application (or in-app) notifications displayed at hello top of hello screen.</span></span> <span data-ttu-id="39c7b-206">Nous n’a pas changé les identificateurs standard hello utilisés dans la zone de notification hello lui-même.</span><span class="sxs-lookup"><span data-stu-id="39c7b-206">We did not change hello standard identifiers used in hello notification area itself.</span></span>

<span data-ttu-id="39c7b-207">Si vous souhaitez toochange que vous avez tooredefine hello `EngagementDefaultNotifier.prepareInAppArea` (méthode).</span><span class="sxs-lookup"><span data-stu-id="39c7b-207">If you want toochange that, you have tooredefine hello `EngagementDefaultNotifier.prepareInAppArea` method.</span></span> <span data-ttu-id="39c7b-208">Il est recommandé de toolook à la documentation technique hello et au code source de hello de `EngagementNotifier` et `EngagementDefaultNotifier` si vous souhaitez que ce niveau de personnalisation avancée.</span><span class="sxs-lookup"><span data-stu-id="39c7b-208">It's recommended toolook at hello technical documentation and at hello source code of `EngagementNotifier` and `EngagementDefaultNotifier` if you want this level of advanced customization.</span></span>

##### <a name="system-notifications"></a><span data-ttu-id="39c7b-209">Notifications système</span><span class="sxs-lookup"><span data-stu-id="39c7b-209">System notifications</span></span>
<span data-ttu-id="39c7b-210">En étendant `EngagementDefaultNotifier`, vous pouvez remplacer `onNotificationPrepared` notification hello tooalter qui a été préparée par l’implémentation par défaut de hello.</span><span class="sxs-lookup"><span data-stu-id="39c7b-210">By extending `EngagementDefaultNotifier`, you can override `onNotificationPrepared` tooalter hello notification that was prepared by hello default implementation.</span></span>

<span data-ttu-id="39c7b-211">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="39c7b-211">For example:</span></span>

            @Override
            protected boolean onNotificationPrepared(Notification notification, EngagementReachInteractiveContent content)
              throws RuntimeException
            {
              if ("ongoing".equals(content.getCategory()))
                notification.flags |= Notification.FLAG_ONGOING_EVENT;
              return true;
            }

<span data-ttu-id="39c7b-212">Cet exemple montre une notification du système pour un contenu affiché sous la forme d’un événement en cours lors de la catégorie « en cours » hello est utilisée.</span><span class="sxs-lookup"><span data-stu-id="39c7b-212">This example makes a system notification for a content being displayed as an ongoing event when hello "ongoing" category is used.</span></span>

<span data-ttu-id="39c7b-213">Si vous souhaitez toobuild hello `Notification` de l’objet à partir de zéro, vous pouvez retourner `false` toohello méthode et appel `notify` vous-même sur hello `NotificationManager`.</span><span class="sxs-lookup"><span data-stu-id="39c7b-213">If you want toobuild hello `Notification` object from scratch, you can return `false` toohello method and call `notify` yourself on hello `NotificationManager`.</span></span> <span data-ttu-id="39c7b-214">Dans ce cas, il est important de conserver un `contentIntent`, un `deleteIntent` et hello identificateur de notification utilisé par `EngagementReachReceiver`.</span><span class="sxs-lookup"><span data-stu-id="39c7b-214">In that case it's important that you keep a `contentIntent`, a `deleteIntent` and hello notification identifier used by `EngagementReachReceiver`.</span></span>

<span data-ttu-id="39c7b-215">Voici un exemple correct d'une telle implémentation :</span><span class="sxs-lookup"><span data-stu-id="39c7b-215">Here is a correct example of such an implementation:</span></span>

            @Override
            protected boolean onNotificationPrepared(Notification notification, EngagementReachInteractiveContent content) throws RuntimeException
            {
              /* Required fields */
              NotificationCompat.Builder builder = new NotificationCompat.Builder(mContext)
                .setSmallIcon(notification.icon)              // icon is mandatory
                .setContentIntent(notification.contentIntent) // keep content intent
                .setDeleteIntent(notification.deleteIntent);  // keep delete intent

              /* Your customization */
              // builder.set...

              /* Dismiss option can be managed only after build */
              Notification myNotification = builder.build();
              if (!content.isNotificationCloseable())
                myNotification.flags |= Notification.FLAG_NO_CLEAR;

              /* Notify here instead of super class */
              NotificationManager manager = (NotificationManager) mContext.getSystemService(Context.NOTIFICATION_SERVICE);
              manager.notify(getNotificationId(content), myNotification); // notice hello call tooget hello right identifier

              /* Return false, we notify ourselves */
              return false;
            }

##### <a name="notification-only-announcements"></a><span data-ttu-id="39c7b-216">Annonces avec notifications uniquement</span><span class="sxs-lookup"><span data-stu-id="39c7b-216">Notification only announcements</span></span>
<span data-ttu-id="39c7b-217">Hello Hello, cliquez sur une notification annonce uniquement peut être personnalisé en substituant `EngagementDefaultNotifier.onNotifAnnouncementIntentPrepared` hello toomodify préparée `Intent`.</span><span class="sxs-lookup"><span data-stu-id="39c7b-217">hello management of hello click on a notification only announcement can be customized by overriding `EngagementDefaultNotifier.onNotifAnnouncementIntentPrepared` toomodify hello prepared `Intent`.</span></span> <span data-ttu-id="39c7b-218">À l’aide de cette méthode vous permet des indicateurs de hello tootune facilement.</span><span class="sxs-lookup"><span data-stu-id="39c7b-218">Using this method allows you tootune hello flags easily.</span></span>

<span data-ttu-id="39c7b-219">Par exemple tooadd hello `SINGLE_TOP` indicateur :</span><span class="sxs-lookup"><span data-stu-id="39c7b-219">For example tooadd hello `SINGLE_TOP` flag:</span></span>

            @Override
            protected Intent onNotifAnnouncementIntentPrepared(EngagementNotifAnnouncement notifAnnouncement,
              Intent intent)
            {
              intent.addFlags(Intent.FLAG_ACTIVITY_SINGLE_TOP);
              return intent;
            }

<span data-ttu-id="39c7b-220">Pour les utilisateurs d’Engagement hérités, notez que les notifications système sans intervention de l’URL maintenant lance application hello si elle était en arrière-plan, cette méthode peut être appelée avec une annonce sans URL de l’action.</span><span class="sxs-lookup"><span data-stu-id="39c7b-220">For legacy Engagement users, please note that system notifications without action URL now launches hello application if it was in background, so this method can be called with an announcement without action URL.</span></span> <span data-ttu-id="39c7b-221">Vous devez envisager que lors de la personnalisation d’intention de hello.</span><span class="sxs-lookup"><span data-stu-id="39c7b-221">You should consider that when customizing hello intent.</span></span>

<span data-ttu-id="39c7b-222">Vous pouvez également implémenter `EngagementNotifier.executeNotifAnnouncementAction` à partir de zéro.</span><span class="sxs-lookup"><span data-stu-id="39c7b-222">You can also implement `EngagementNotifier.executeNotifAnnouncementAction` from scratch.</span></span>

##### <a name="notification-life-cycle"></a><span data-ttu-id="39c7b-223">Cycle de vie des notifications</span><span class="sxs-lookup"><span data-stu-id="39c7b-223">Notification life cycle</span></span>
<span data-ttu-id="39c7b-224">Lorsque vous utilisez la catégorie par défaut de hello, certaines méthodes de cycle de vie sont appelées sur hello `EngagementReachInteractiveContent` tooreport des statistiques et mise à jour hello campagne l’état de l’objet :</span><span class="sxs-lookup"><span data-stu-id="39c7b-224">When using hello default category, some life cycle methods are called on hello `EngagementReachInteractiveContent` object tooreport statistics and update hello campaign state:</span></span>

* <span data-ttu-id="39c7b-225">Lors de la notification de hello est affichée dans l’application ou placée dans la barre d’état hello, hello `displayNotification` méthode est appelée (qui fournit des statistiques) par `EngagementReachAgent` si `handleNotification` retourne `true`.</span><span class="sxs-lookup"><span data-stu-id="39c7b-225">When hello notification is displayed in application or put in hello status bar, hello `displayNotification` method is called (which reports statistics) by `EngagementReachAgent` if `handleNotification` returns `true`.</span></span>
* <span data-ttu-id="39c7b-226">Si la notification de hello est fermée, hello `exitNotification` méthode est appelée, la statistique est signalée et campagnes suivants peuvent maintenant être traités.</span><span class="sxs-lookup"><span data-stu-id="39c7b-226">If hello notification is dismissed, hello `exitNotification` method is called, statistic is reported and next campaigns can now be processed.</span></span>
* <span data-ttu-id="39c7b-227">Cliquez sur la notification de hello `actionNotification` est appelée, la statistique est signalée et l’intention de hello associé est lancée.</span><span class="sxs-lookup"><span data-stu-id="39c7b-227">If hello notification is clicked, `actionNotification` is called, statistic is reported and hello associated intent is launched.</span></span>

<span data-ttu-id="39c7b-228">Si votre implémentation de `EngagementNotifier` contournements hello le comportement par défaut, vous pouvez toocall ces méthodes de cycle de vie vous-même.</span><span class="sxs-lookup"><span data-stu-id="39c7b-228">If your implementation of `EngagementNotifier` bypasses hello default behavior, you have toocall these life cycle methods by yourself.</span></span> <span data-ttu-id="39c7b-229">Hello suivant exemples illustre certains cas où le comportement par défaut de hello est ignorée :</span><span class="sxs-lookup"><span data-stu-id="39c7b-229">hello following examples illustrate some cases where hello default behavior is bypassed:</span></span>

* <span data-ttu-id="39c7b-230">Vous n'étendez pas `EngagementDefaultNotifier`, par exemple, vous avez implémenté la gestion des catégories à partir de zéro.</span><span class="sxs-lookup"><span data-stu-id="39c7b-230">You don't extend `EngagementDefaultNotifier`, e.g. you implemented category handling from scratch.</span></span>
* <span data-ttu-id="39c7b-231">Pour les notifications système, vous a substitué hello `onNotificationPrepared` et vous avez modifié `contentIntent` ou `deleteIntent` Bonjour `Notification` objet.</span><span class="sxs-lookup"><span data-stu-id="39c7b-231">For system notifications, you overrode hello `onNotificationPrepared` and you modified `contentIntent` or `deleteIntent` in hello `Notification` object.</span></span>
* <span data-ttu-id="39c7b-232">Pour les notifications dans l’application, vous se `prepareInAppArea`, être d’au moins sûr toomap `actionNotification` tooone de vos contrôles U.I.</span><span class="sxs-lookup"><span data-stu-id="39c7b-232">For in-app notifications, you overrode `prepareInAppArea`, be sure toomap at least `actionNotification` tooone of your U.I controls.</span></span>

> [!NOTE]
> <span data-ttu-id="39c7b-233">Si `handleNotification` lève une exception, hello contenu est supprimé et `dropContent` est appelée.</span><span class="sxs-lookup"><span data-stu-id="39c7b-233">If `handleNotification` throws an exception, hello content is deleted and `dropContent` is called.</span></span> <span data-ttu-id="39c7b-234">Ceci est signalé dans les statistiques et les campagnes suivantes peuvent être traitées.</span><span class="sxs-lookup"><span data-stu-id="39c7b-234">This is reported in statistics and next campaigns can now be processed.</span></span>
> 
> 

### <a name="announcements-and-polls"></a><span data-ttu-id="39c7b-235">Annonces et sondages</span><span class="sxs-lookup"><span data-stu-id="39c7b-235">Announcements and polls</span></span>
#### <a name="layouts"></a><span data-ttu-id="39c7b-236">Mises en forme</span><span class="sxs-lookup"><span data-stu-id="39c7b-236">Layouts</span></span>
<span data-ttu-id="39c7b-237">Vous pouvez modifier hello `engagement_text_announcement.xml`, `engagement_web_announcement.xml` et `engagement_poll.xml` toocustomize texte annonces, des annonces de web et des interrogations de fichiers.</span><span class="sxs-lookup"><span data-stu-id="39c7b-237">You can modify hello `engagement_text_announcement.xml`, `engagement_web_announcement.xml` and `engagement_poll.xml` files toocustomize text announcements, web announcements and polls.</span></span>

<span data-ttu-id="39c7b-238">Ces fichiers partagent deux dispositions courantes pour la zone de titre hello et zone de bouton hello.</span><span class="sxs-lookup"><span data-stu-id="39c7b-238">These files share two common layouts for hello title area and hello button area.</span></span> <span data-ttu-id="39c7b-239">mise en page Hello pour le titre de hello est `engagement_content_title.xml` et utilise hello éponyme fichier drawable pour l’arrière-plan de hello.</span><span class="sxs-lookup"><span data-stu-id="39c7b-239">hello layout for hello title is `engagement_content_title.xml` and uses hello eponymous drawable file for hello background.</span></span> <span data-ttu-id="39c7b-240">Hello la disposition des boutons d’action et quitter hello est `engagement_button_bar.xml` et utilise hello éponyme fichier drawable pour l’arrière-plan de hello.</span><span class="sxs-lookup"><span data-stu-id="39c7b-240">hello layout for hello action and exit buttons is `engagement_button_bar.xml` and uses hello eponymous drawable file for hello background.</span></span>

<span data-ttu-id="39c7b-241">Dans un sondage, hello mise en page de question et de leur choix est dynamiquement à l’aide de plusieurs fois hello `engagement_question.xml` fichier de disposition pour les questions de hello et hello `engagement_choice.xml` fichier pour les choix de hello.</span><span class="sxs-lookup"><span data-stu-id="39c7b-241">In a poll, hello question layout and their choices are dynamically inflated using several times hello `engagement_question.xml` layout file for hello questions and hello `engagement_choice.xml` file for hello choices.</span></span>

#### <a name="categories"></a><span data-ttu-id="39c7b-242">Catégories</span><span class="sxs-lookup"><span data-stu-id="39c7b-242">Categories</span></span>
##### <a name="alternate-layouts"></a><span data-ttu-id="39c7b-243">Autres dispositions</span><span class="sxs-lookup"><span data-stu-id="39c7b-243">Alternate layouts</span></span>
<span data-ttu-id="39c7b-244">Telles que les notifications, catégorie de la campagne hello peut être utilisé toohave des formes différentes vos annonces et les interroge.</span><span class="sxs-lookup"><span data-stu-id="39c7b-244">Like notifications, hello campaign's category can be used toohave alternate layouts for your announcements and polls.</span></span>

<span data-ttu-id="39c7b-245">Par exemple, de le toocreate une catégorie pour une annonce de texte, vous pouvez étendre `EngagementTextAnnouncementActivity` et à le référencer hello `AndroidManifest.xml` fichier :</span><span class="sxs-lookup"><span data-stu-id="39c7b-245">For example, toocreate a category for a text announcement, you can extend `EngagementTextAnnouncementActivity` and reference it hello `AndroidManifest.xml` file:</span></span>

            <activity android:name="com.your_company.MyCustomTextAnnouncementActivity">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
                <category android:name="my_category" />
                <data android:mimeType="text/plain" />
              </intent-filter>
            </activity>

<span data-ttu-id="39c7b-246">Notez cette catégorie hello dans l’intention de hello sert de filtre de différence de hello toomake avec une activité d’annonce hello par défaut.</span><span class="sxs-lookup"><span data-stu-id="39c7b-246">Note that hello category in hello intent filter is used toomake hello difference with hello default announcement activity.</span></span>

<span data-ttu-id="39c7b-247">Hello SDK Reach utilise hello intention tooresolve hello droite l’activité du système pour une catégorie spécifique et qu’il revient de catégorie par défaut de hello en cas d’échec de la résolution de hello.</span><span class="sxs-lookup"><span data-stu-id="39c7b-247">hello Reach SDK uses hello intent system tooresolve hello right activity for a specific category and it falls back on hello default category if hello resolution failed.</span></span>

<span data-ttu-id="39c7b-248">Vous devez tooimplement `MyCustomTextAnnouncementActivity`, si vous venez laquelle toochange hello présentation (mais conservez hello même afficher les identificateurs), vous avez simplement classe hello toodefine, telles que Bonjour l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="39c7b-248">Then you have tooimplement `MyCustomTextAnnouncementActivity`, if you just want toochange hello layout (but keep hello same view identifiers), you just have toodefine hello class like in hello following example:</span></span>

            public class MyCustomTextAnnouncementActivity extends EngagementTextAnnouncementActivity
            {
              @Override
              protected String getLayoutName()
              {
                return "my_text_announcement";  // tell super class toouse R.layout.my_text_announcement
              }
            }

<span data-ttu-id="39c7b-249">catégorie de par défaut hello tooreplace des annonces de texte, remplacez simplement `android:name="com.microsoft.azure.engagement.reach.activity.EngagementTextAnnouncementActivity"` par votre implémentation.</span><span class="sxs-lookup"><span data-stu-id="39c7b-249">tooreplace hello default category of text announcements, simply replace `android:name="com.microsoft.azure.engagement.reach.activity.EngagementTextAnnouncementActivity"` by your implementation.</span></span>

<span data-ttu-id="39c7b-250">Les annonces web et les sondages peuvent être personnalisés de la même manière.</span><span class="sxs-lookup"><span data-stu-id="39c7b-250">Web announcements and polls can be customized in a similar fashion.</span></span>

<span data-ttu-id="39c7b-251">Les annonces de web, vous pouvez étendre `EngagementWebAnnouncementActivity` et déclarer votre activité Bonjour `AndroidManifest.xml` comme Bonjour l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="39c7b-251">For web announcements you can extend `EngagementWebAnnouncementActivity` and declare your activity in hello `AndroidManifest.xml` like in hello following example:</span></span>

            <activity android:name="com.your_company.MyCustomWebAnnouncementActivity">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
                <category android:name="my_category" />
                <data android:mimeType="text/html" />    <!-- only difference with text announcements in hello intent is hello data mime type -->
              </intent-filter>
            </activity>

<span data-ttu-id="39c7b-252">Pour les sondages, vous pouvez étendre `EngagementPollActivity` et déclarer votre hello en `AndroidManifest.xml` comme Bonjour l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="39c7b-252">For polls you can extend `EngagementPollActivity` and declare your in hello `AndroidManifest.xml` like in hello following example:</span></span>

            <activity android:name="com.your_company.MyCustomPollActivity">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.POLL"/>
                <category android:name="my_category" />
              </intent-filter>
            </activity>

##### <a name="implementation-from-scratch"></a><span data-ttu-id="39c7b-253">Implémentation à partir de zéro</span><span class="sxs-lookup"><span data-stu-id="39c7b-253">Implementation from scratch</span></span>
<span data-ttu-id="39c7b-254">Vous pouvez implémenter des catégories pour vos activités d’annonce (et d’interrogation) sans étendre un des hello `Engagement*Activity` classes fournies par hello SDK Reach.</span><span class="sxs-lookup"><span data-stu-id="39c7b-254">You can implement categories for your announcement (and poll) activities without extending one of hello `Engagement*Activity` classes provided by hello Reach SDK.</span></span> <span data-ttu-id="39c7b-255">Cela est utile par exemple si vous souhaitez toodefine une disposition qui n’utilise pas de hello même vues comme les dispositions standard hello.</span><span class="sxs-lookup"><span data-stu-id="39c7b-255">This is useful for example if you want toodefine a layout that does not use hello same views as hello standard layouts.</span></span>

<span data-ttu-id="39c7b-256">Comme pour la personnalisation de la notification avancés, il est recommandé toolook au code source de hello d’implémentation standard de hello.</span><span class="sxs-lookup"><span data-stu-id="39c7b-256">Like for advanced notification customization, it is recommended toolook at hello source code of hello standard implementation.</span></span>

<span data-ttu-id="39c7b-257">Voici certains tookeep choses à l’esprit : portée lancera activité hello avec un mode spécifique (filtre intention toohello correspondant) ainsi que d’un paramètre supplémentaire qui est l’identificateur de contenu hello.</span><span class="sxs-lookup"><span data-stu-id="39c7b-257">Here are some things tookeep in mind: Reach will launch hello activity with a specific intent (corresponding toohello intent filter) plus an extra parameter which is hello content identifier.</span></span>

<span data-ttu-id="39c7b-258">objet contenu tooretrieve hello qui contiennent des champs hello vous avez spécifié lorsque hello de création de la campagne sur le site web de hello vous pouvez procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="39c7b-258">tooretrieve hello content object which contain hello fields you specified when creating hello campaign on hello web site you can do this:</span></span>

            public class MyCustomTextAnnouncement extends EngagementActivity
            {
              private EngagementAnnouncement mContent;

              @Override
              protected void onCreate(Bundle savedInstanceState)
              {
                super.onCreate(savedInstanceState);

                /* Get content */
                mContent = EngagementReachAgent.getInstance(this).getContent(getIntent());
                if (mContent == null)
                {
                  /* If problem with content, exit */
                  finish();
                  return;
                }

                setContentView(R.layout.my_text_announcement);

                /* Configure views by querying fields on mContent */
                // ...
              }
            }

<span data-ttu-id="39c7b-259">Pour les statistiques, vous devez signaler l’affichage du contenu de hello dans hello `onResume` événement :</span><span class="sxs-lookup"><span data-stu-id="39c7b-259">For statistics, you should report hello content is displayed in hello `onResume` event:</span></span>

            @Override
            protected void onResume()
            {
             /* Mark hello content displayed */
             mContent.displayContent(this);
             super.onResume();
            }

<span data-ttu-id="39c7b-260">Ensuite, n’oubliez pas toocall soit `actionContent(this)` ou `exitContent(this)` sur l’objet de contenu hello avant l’activité hello passe en arrière-plan.</span><span class="sxs-lookup"><span data-stu-id="39c7b-260">Then, don't forget toocall either `actionContent(this)` or `exitContent(this)` on hello content object before hello activity goes into background.</span></span>

<span data-ttu-id="39c7b-261">Si vous n’appelez pas soit `actionContent` ou `exitContent`, les statistiques ne seront pas envoyées (autrement dit, aucune analytique sur une campagne de hello) et plus important encore, hello campagnes suivants ne seront pas informés qu’après le redémarrage du processus d’application hello.</span><span class="sxs-lookup"><span data-stu-id="39c7b-261">If you don't call either `actionContent` or `exitContent`, statistics won't be sent (i.e. no analytics on hello campaign) and more importantly, hello next campaigns will not be notified until hello application process is restarted.</span></span>

<span data-ttu-id="39c7b-262">L’orientation ou autres modifications de configuration peut prendre de toodetermine difficile de code hello activité hello passe en arrière-plan ou non, hello rend implémentation standard que contenu de hello est signalé comme quitté si l’utilisateur de hello quitte activité hello (soit en en appuyant sur `HOME` ou `BACK`), mais pas si hello orientation change.</span><span class="sxs-lookup"><span data-stu-id="39c7b-262">Orientation or other configuration changes can make hello code tricky toodetermine whether hello activity goes into background or not, hello standard implementation makes sure hello content is reported as exited if hello user leaves hello activity (either by pressing `HOME` or `BACK`) but not if hello orientation changes.</span></span>

<span data-ttu-id="39c7b-263">Ici est hello intéressantes dans hello implémentation :</span><span class="sxs-lookup"><span data-stu-id="39c7b-263">Here is hello interesting part of hello implementation:</span></span>

            @Override
            protected void onUserLeaveHint()
            {
              finish();
            }

            @Override
            protected void onPause()
            {
              if (isFinishing() && mContent != null)
              {
                /*
                 * Exit content on exit, this is has no effect if another process method has already been
                 * called so we don't have toocheck anything here.
                 */
                mContent.exitContent(this);
              }
              super.onPause();
            }

<span data-ttu-id="39c7b-264">Comme vous pouvez le voir, si vous avez appelé `actionContent(this)` puis terminé l’activité hello, `exitContent(this)` peut être appelée en toute sécurité sans avoir aucun effet.</span><span class="sxs-lookup"><span data-stu-id="39c7b-264">As you can see, if you called `actionContent(this)` then finished hello activity, `exitContent(this)` can be safely called without having any effect.</span></span>

[here]:http://developer.android.com/tools/extras/support-library.html#Downloading
[messagerie Cloud Google]:http://developer.android.com/guide/google/gcm/index.html
[Amazon Device Messaging]:https://developer.amazon.com/sdk/adm.html
