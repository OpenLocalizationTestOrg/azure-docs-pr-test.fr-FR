---
title: configuration aaaAdvanced pour Azure Mobile Engagement Android SDK
description: "Décrit les hello notamment hello manifeste Android avec le SDK Android Azure Mobile Engagement des options de configuration avancées"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 37d2c09a-86fa-473d-8987-c7e35a0eb3e8
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 10/04/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: 757abf362021fd018f444cae6305524623e77062
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-configuration-for-azure-mobile-engagement-android-sdk"></a><span data-ttu-id="7522c-103">Configuration avancée pour le SDK Android pour Azure Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="7522c-103">Advanced configuration for Azure Mobile Engagement Android SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="7522c-104">Windows universel</span><span class="sxs-lookup"><span data-stu-id="7522c-104">Universal Windows</span></span>](mobile-engagement-windows-store-advanced-configuration.md)
> * [<span data-ttu-id="7522c-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="7522c-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md)
> * [<span data-ttu-id="7522c-106">iOS</span><span class="sxs-lookup"><span data-stu-id="7522c-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md)
> * [<span data-ttu-id="7522c-107">Android</span><span class="sxs-lookup"><span data-stu-id="7522c-107">Android</span></span>](mobile-engagement-android-advanced-configuration.md)
>
>

<span data-ttu-id="7522c-108">Cette procédure décrit comment tooconfigure différentes options de configuration pour les applications Azure Mobile Engagement Android.</span><span class="sxs-lookup"><span data-stu-id="7522c-108">This procedure describes how tooconfigure various configuration options for Azure Mobile Engagement Android apps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7522c-109">Composants requis</span><span class="sxs-lookup"><span data-stu-id="7522c-109">Prerequisites</span></span>
[!INCLUDE [Prereqs](../../includes/mobile-engagement-android-prereqs.md)]

## <a name="permission-requirements"></a><span data-ttu-id="7522c-110">Autorisations requises</span><span class="sxs-lookup"><span data-stu-id="7522c-110">Permission Requirements</span></span>
<span data-ttu-id="7522c-111">Certaines options nécessitent des autorisations spécifiques qui sont répertoriées ici pour référence et en ligne dans la fonctionnalité spécifique de hello.</span><span class="sxs-lookup"><span data-stu-id="7522c-111">Some options require specific permissions, all of which are listed here for reference, and in-line in hello specific feature.</span></span> <span data-ttu-id="7522c-112">Ajoutez ces toohello autorisations AndroidManifest.xml de votre projet immédiatement avant ou après hello `<application>` balise.</span><span class="sxs-lookup"><span data-stu-id="7522c-112">Add these permissions toohello AndroidManifest.xml of your project immediately before or after hello `<application>` tag.</span></span>

<span data-ttu-id="7522c-113">code d’autorisation Hello doit toolook hello suivante, où vous renseignez autorisation appropriée de hello à partir de la table hello qui suit.</span><span class="sxs-lookup"><span data-stu-id="7522c-113">hello permission code needs toolook like hello following, where you fill in hello appropriate permission from hello table that follows.</span></span>

    <uses-permission android:name="android.permission.[specific permission]"/>


| <span data-ttu-id="7522c-114">Autorisation</span><span class="sxs-lookup"><span data-stu-id="7522c-114">Permission</span></span> | <span data-ttu-id="7522c-115">Quand l’utiliser</span><span class="sxs-lookup"><span data-stu-id="7522c-115">When used</span></span> |
| --- | --- |
| <span data-ttu-id="7522c-116">INTERNET</span><span class="sxs-lookup"><span data-stu-id="7522c-116">INTERNET</span></span> |<span data-ttu-id="7522c-117">Obligatoire.</span><span class="sxs-lookup"><span data-stu-id="7522c-117">Required.</span></span> <span data-ttu-id="7522c-118">Pour la génération de rapports de base</span><span class="sxs-lookup"><span data-stu-id="7522c-118">For basic reporting</span></span> |
| <span data-ttu-id="7522c-119">ACCESS_NETWORK_STATE</span><span class="sxs-lookup"><span data-stu-id="7522c-119">ACCESS_NETWORK_STATE</span></span> |<span data-ttu-id="7522c-120">Obligatoire.</span><span class="sxs-lookup"><span data-stu-id="7522c-120">Required.</span></span> <span data-ttu-id="7522c-121">Pour la génération de rapports de base</span><span class="sxs-lookup"><span data-stu-id="7522c-121">For basic reporting</span></span> |
| <span data-ttu-id="7522c-122">RECEIVE_BOOT_COMPLETED</span><span class="sxs-lookup"><span data-stu-id="7522c-122">RECEIVE_BOOT_COMPLETED</span></span> |<span data-ttu-id="7522c-123">Obligatoire.</span><span class="sxs-lookup"><span data-stu-id="7522c-123">Required.</span></span> <span data-ttu-id="7522c-124">tooshow centre de notifications hello après le redémarrage de l’appareil</span><span class="sxs-lookup"><span data-stu-id="7522c-124">tooshow up hello notifications center after device reboot</span></span> |
| <span data-ttu-id="7522c-125">WAKE_LOCK</span><span class="sxs-lookup"><span data-stu-id="7522c-125">WAKE_LOCK</span></span> |<span data-ttu-id="7522c-126">Recommandé.</span><span class="sxs-lookup"><span data-stu-id="7522c-126">Recommended.</span></span> <span data-ttu-id="7522c-127">Active la collecte de données quand vous utilisez le Wi-Fi ou quand l’écran est éteint</span><span class="sxs-lookup"><span data-stu-id="7522c-127">Enables collecting data when using WiFi or when screen is off</span></span> |
| <span data-ttu-id="7522c-128">VIBRATE</span><span class="sxs-lookup"><span data-stu-id="7522c-128">VIBRATE</span></span> |<span data-ttu-id="7522c-129">facultatif.</span><span class="sxs-lookup"><span data-stu-id="7522c-129">Optional.</span></span> <span data-ttu-id="7522c-130">Active la vibration lors de la réception des notifications</span><span class="sxs-lookup"><span data-stu-id="7522c-130">Enables vibration when notifications are received</span></span> |
| <span data-ttu-id="7522c-131">DOWNLOAD_WITHOUT_NOTIFICATION</span><span class="sxs-lookup"><span data-stu-id="7522c-131">DOWNLOAD_WITHOUT_NOTIFICATION</span></span> |<span data-ttu-id="7522c-132">facultatif.</span><span class="sxs-lookup"><span data-stu-id="7522c-132">Optional.</span></span> <span data-ttu-id="7522c-133">Active la Notification de la vue d’ensemble Android</span><span class="sxs-lookup"><span data-stu-id="7522c-133">Enables Android Big Picture Notification</span></span> |
| <span data-ttu-id="7522c-134">WRITE_EXTERNAL_STORAGE</span><span class="sxs-lookup"><span data-stu-id="7522c-134">WRITE_EXTERNAL_STORAGE</span></span> |<span data-ttu-id="7522c-135">facultatif.</span><span class="sxs-lookup"><span data-stu-id="7522c-135">Optional.</span></span> <span data-ttu-id="7522c-136">Active la Notification de la vue d’ensemble Android</span><span class="sxs-lookup"><span data-stu-id="7522c-136">Enables Android Big Picture Notification</span></span> |
| <span data-ttu-id="7522c-137">ACCESS_COARSE_LOCATION</span><span class="sxs-lookup"><span data-stu-id="7522c-137">ACCESS_COARSE_LOCATION</span></span> |<span data-ttu-id="7522c-138">facultatif.</span><span class="sxs-lookup"><span data-stu-id="7522c-138">Optional.</span></span> <span data-ttu-id="7522c-139">Active la génération de rapports d’emplacement en temps réel</span><span class="sxs-lookup"><span data-stu-id="7522c-139">Enables Real-time location reporting</span></span> |
| <span data-ttu-id="7522c-140">ACCESS_FINE_LOCATION</span><span class="sxs-lookup"><span data-stu-id="7522c-140">ACCESS_FINE_LOCATION</span></span> |<span data-ttu-id="7522c-141">facultatif.</span><span class="sxs-lookup"><span data-stu-id="7522c-141">Optional.</span></span> <span data-ttu-id="7522c-142">Active la génération de rapports sur l’emplacement GPS</span><span class="sxs-lookup"><span data-stu-id="7522c-142">Enables GPS-based location reporting</span></span> |

<span data-ttu-id="7522c-143">À partir d’Android M, [certaines autorisations sont gérées au moment de l’exécution](mobile-engagement-android-location-reporting.md#android-m-permissions).</span><span class="sxs-lookup"><span data-stu-id="7522c-143">Starting with Android M, [some permissions are managed at run time](mobile-engagement-android-location-reporting.md#android-m-permissions).</span></span>

<span data-ttu-id="7522c-144">Si vous utilisez déjà ``ACCESS_FINE_LOCATION``, vous avez tooalso utiliser ``ACCESS_COARSE_LOCATION``.</span><span class="sxs-lookup"><span data-stu-id="7522c-144">If you are already using ``ACCESS_FINE_LOCATION``, then you don't need tooalso use ``ACCESS_COARSE_LOCATION``.</span></span>

## <a name="android-manifest-configuration-options"></a><span data-ttu-id="7522c-145">Options de configuration de manifeste Android</span><span class="sxs-lookup"><span data-stu-id="7522c-145">Android Manifest configuration options</span></span>
### <a name="crash-report"></a><span data-ttu-id="7522c-146">Rapport d'incidents</span><span class="sxs-lookup"><span data-stu-id="7522c-146">Crash report</span></span>
<span data-ttu-id="7522c-147">rapports d’incidents toodisable, ajoutez le code entre hello `<application>` et `</application>` balises :</span><span class="sxs-lookup"><span data-stu-id="7522c-147">toodisable crash reports, add this code between hello `<application>` and `</application>` tags:</span></span>

    <meta-data android:name="engagement:reportCrash" android:value="false"/>

### <a name="burst-threshold"></a><span data-ttu-id="7522c-148">Seuil du mode rafale</span><span class="sxs-lookup"><span data-stu-id="7522c-148">Burst threshold</span></span>
<span data-ttu-id="7522c-149">Par défaut, les rapports de service d’Engagement hello journaux en temps réel.</span><span class="sxs-lookup"><span data-stu-id="7522c-149">By default, hello Engagement service reports logs in real time.</span></span> <span data-ttu-id="7522c-150">Si vos journaux d’état application varie fréquemment, il est mieux toobuffer hello journaux et tooreport à la fois à une base de temps réguliers (appelée « mode de croissance »).</span><span class="sxs-lookup"><span data-stu-id="7522c-150">If your application report logs vary frequently, it is better toobuffer hello logs and tooreport them all at once on a regular time base (called "burst mode").</span></span> <span data-ttu-id="7522c-151">toodo, ajoutez ce code entre hello `<application>` et `</application>` balises :</span><span class="sxs-lookup"><span data-stu-id="7522c-151">toodo so, add this code between hello `<application>` and `</application>` tags:</span></span>

    <meta-data android:name="engagement:burstThreshold" android:value="{interval between too bursts (in milliseconds)}"/>

<span data-ttu-id="7522c-152">Mode rafale augmente l’autonomie des batteries hello légèrement mais a un impact sur hello Engagement moniteur : durée des sessions et les travaux toute sont arrondis toohello rafale seuil (par conséquent, les sessions et les travaux plus court que le seuil de croissance hello n’est pas forcément visible).</span><span class="sxs-lookup"><span data-stu-id="7522c-152">Burst mode slightly increases hello battery life but has an impact on hello Engagement Monitor: all sessions and jobs duration are rounded toohello burst threshold (thus, sessions and jobs shorter than hello burst threshold may not be visible).</span></span> <span data-ttu-id="7522c-153">Votre seuil de rafale ne doit pas dépasser la valeur 30000 (30 s).</span><span class="sxs-lookup"><span data-stu-id="7522c-153">Your burst threshold should be no longer than 30000 (30s).</span></span>

### <a name="session-timeout"></a><span data-ttu-id="7522c-154">Délai d'expiration de session</span><span class="sxs-lookup"><span data-stu-id="7522c-154">Session timeout</span></span>
 <span data-ttu-id="7522c-155">Vous pouvez terminer une activité en appuyant sur les hello **accueil** ou **précédent** clé, par définition téléphone hello inactif ou passer à une autre application.</span><span class="sxs-lookup"><span data-stu-id="7522c-155">You can end an activity by pressing hello **Home** or **Back** key, by setting hello phone idle or by jumping into another application.</span></span> <span data-ttu-id="7522c-156">Par défaut, une session prend fin dix secondes après la fin de hello de sa dernière activité.</span><span class="sxs-lookup"><span data-stu-id="7522c-156">By default, a session is ended ten seconds after hello end of its last activity.</span></span> <span data-ttu-id="7522c-157">Cela permet d’éviter un fractionnement de session chaque utilisateur hello se termine et retourne toohello application rapidement, ce qui peut se produire lorsque l’utilisateur de hello sélectionne une image, vérifie une notification, un etc.. Vous souhaiterez toomodify ce paramètre.</span><span class="sxs-lookup"><span data-stu-id="7522c-157">This avoids a session split each time hello user exits and returns toohello application quickly, which can happen when hello user picks up an image, checks a notification, etc. You may want toomodify this parameter.</span></span> <span data-ttu-id="7522c-158">toodo, ajoutez ce code entre hello `<application>` et `</application>` balises :</span><span class="sxs-lookup"><span data-stu-id="7522c-158">toodo so, add this code between hello `<application>` and `</application>` tags:</span></span>

    <meta-data android:name="engagement:sessionTimeout" android:value="{session timeout (in milliseconds)}"/>

## <a name="disable-log-reporting"></a><span data-ttu-id="7522c-159">Désactiver les rapports de suivi</span><span class="sxs-lookup"><span data-stu-id="7522c-159">Disable log reporting</span></span>
### <a name="using-a-method-call"></a><span data-ttu-id="7522c-160">En appelant une méthode</span><span class="sxs-lookup"><span data-stu-id="7522c-160">Using a method call</span></span>
<span data-ttu-id="7522c-161">Si vous souhaitez toostop Engagement envoi de journaux, vous pouvez appeler :</span><span class="sxs-lookup"><span data-stu-id="7522c-161">If you want Engagement toostop sending logs, you can call:</span></span>

    EngagementAgent.getInstance(context).setEnabled(false);

<span data-ttu-id="7522c-162">Cet appel est persistant : il utilise un fichier de préférences partagées.</span><span class="sxs-lookup"><span data-stu-id="7522c-162">This call is persistent: it uses a shared preferences file.</span></span>

<span data-ttu-id="7522c-163">Si l’Engagement est active lorsque vous appelez cette fonction, il peut prendre une minute pour hello service toostop.</span><span class="sxs-lookup"><span data-stu-id="7522c-163">If Engagement is active when you call this function, it may take one minute for hello service toostop.</span></span> <span data-ttu-id="7522c-164">Toutefois, il ne sera pas lancer service hello en hello tous les prochaine fois que vous lancez application hello.</span><span class="sxs-lookup"><span data-stu-id="7522c-164">However it won't launch hello service at all hello next time you launch hello application.</span></span>

<span data-ttu-id="7522c-165">Vous pouvez activer le journal de création de rapports en appelant hello même fonction avec `true`.</span><span class="sxs-lookup"><span data-stu-id="7522c-165">You can enable log reporting again by calling hello same function with `true`.</span></span>

### <a name="integration-in-your-own-preferenceactivity"></a><span data-ttu-id="7522c-166">Intégration dans votre propre `PreferenceActivity`</span><span class="sxs-lookup"><span data-stu-id="7522c-166">Integration in your own `PreferenceActivity`</span></span>
<span data-ttu-id="7522c-167">Au lieu d'appeler cette fonction, vous pouvez également intégrer ce paramètre directement dans votre `PreferenceActivity`.</span><span class="sxs-lookup"><span data-stu-id="7522c-167">Instead of calling this function, you can also integrate this setting directly in your existing `PreferenceActivity`.</span></span>

<span data-ttu-id="7522c-168">Vous pouvez configurer toouse Engagement vos préférences de fichier (avec le mode souhaité de hello) de hello `AndroidManifest.xml` de fichiers avec `application meta-data`:</span><span class="sxs-lookup"><span data-stu-id="7522c-168">You can configure Engagement toouse your preferences file (with hello desired mode) in hello `AndroidManifest.xml` file with `application meta-data`:</span></span>

* <span data-ttu-id="7522c-169">Hello `engagement:agent:settings:name` clé désigne toodefine utilisé hello du fichier de préférences partagées hello.</span><span class="sxs-lookup"><span data-stu-id="7522c-169">hello `engagement:agent:settings:name` key is used toodefine hello name of hello shared preferences file.</span></span>
* <span data-ttu-id="7522c-170">Hello `engagement:agent:settings:mode` clé est en mode de hello toodefine utilisé du fichier de préférences partagées hello.</span><span class="sxs-lookup"><span data-stu-id="7522c-170">hello `engagement:agent:settings:mode` key is used toodefine hello mode of hello shared preferences file.</span></span> <span data-ttu-id="7522c-171">Utilisez hello même mode en tant que dans votre `PreferenceActivity`.</span><span class="sxs-lookup"><span data-stu-id="7522c-171">Use hello same mode as in your `PreferenceActivity`.</span></span> <span data-ttu-id="7522c-172">mode de Hello doit être passé en tant que nombre : Si vous utilisez une combinaison d’indicateurs de constantes dans votre code, vérifiez la valeur totale de hello.</span><span class="sxs-lookup"><span data-stu-id="7522c-172">hello mode must be passed as a number: if you are using a combination of constant flags in your code, check hello total value.</span></span>

<span data-ttu-id="7522c-173">Engagement toujours utilise hello `engagement:key` booléenne clé dans le fichier de préférences de hello pour gérer ce paramètre.</span><span class="sxs-lookup"><span data-stu-id="7522c-173">Engagement always uses hello `engagement:key` boolean key within hello preferences file for managing this setting.</span></span>

<span data-ttu-id="7522c-174">Hello selon l’exemple de `AndroidManifest.xml` affiche hello des valeurs par défaut :</span><span class="sxs-lookup"><span data-stu-id="7522c-174">hello following example of `AndroidManifest.xml` shows hello default values:</span></span>

    <application>
        [...]
        <meta-data
          android:name="engagement:agent:settings:name"
          android:value="engagement.agent" />
        <meta-data
          android:name="engagement:agent:settings:mode"
          android:value="0" />

<span data-ttu-id="7522c-175">Vous pouvez ensuite ajouter un `CheckBoxPreference` dans la disposition de préférence comme hello suivant un :</span><span class="sxs-lookup"><span data-stu-id="7522c-175">Then you can add a `CheckBoxPreference` in your preference layout like hello following one:</span></span>

    <CheckBoxPreference
      android:key="engagement:enabled"
      android:defaultValue="true"
      android:title="Use Engagement"
      android:summaryOn="Engagement is enabled."
      android:summaryOff="Engagement is disabled." />
