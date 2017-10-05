---
title: "Intégration du SDK Android d'Azure Mobile Engagement"
description: "Dernières mises à jour et procédures du SDK Android pour Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 585341f9-3f39-459a-af42-864e400a0128
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 07/17/2017
ms.author: piyushjo
ms.openlocfilehash: c179c39a43da0aa35e945acceacbf27fe8e328f3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="release-notes"></a><span data-ttu-id="97c5c-103">Notes de publication</span><span class="sxs-lookup"><span data-stu-id="97c5c-103">Release notes</span></span>

## <a name="431-07172017"></a><span data-ttu-id="97c5c-104">4.3.1 (07/17/2017)</span><span class="sxs-lookup"><span data-stu-id="97c5c-104">4.3.1 (07/17/2017)</span></span>
* <span data-ttu-id="97c5c-105">Résolution d’un incident rare lors de l’appel de `EngagementAgentUtils.isInDedicatedEngagementProcess`, également utilisée par la classe `EngagementApplication`.</span><span class="sxs-lookup"><span data-stu-id="97c5c-105">Fix a crash that could rarely happen when calling `EngagementAgentUtils.isInDedicatedEngagementProcess`, which is also used by the `EngagementApplication` class.</span></span>

## <a name="430-06272017"></a><span data-ttu-id="97c5c-106">4.3.0 (06/27/2017)</span><span class="sxs-lookup"><span data-stu-id="97c5c-106">4.3.0 (06/27/2017)</span></span>
* <span data-ttu-id="97c5c-107">Prise en charge Android 8 (les versions précédentes du Kit de développement logiciel ne fonctionnent pas sur Android 8).</span><span class="sxs-lookup"><span data-stu-id="97c5c-107">Android 8 support (previous versions of the SDK will not work on Android 8).</span></span>
* <span data-ttu-id="97c5c-108">Aucune autre dépendance sur la bibliothèque de prise en charge.</span><span class="sxs-lookup"><span data-stu-id="97c5c-108">No more dependency on support library.</span></span>
* <span data-ttu-id="97c5c-109">Supprimez la classe `EngagementFragmentActivity`.</span><span class="sxs-lookup"><span data-stu-id="97c5c-109">Remove `EngagementFragmentActivity` class.</span></span>
* <span data-ttu-id="97c5c-110">En raison des [limites d’exécution en arrière-plan](https://developer.android.com/preview/features/background.html) sur Android 8, les journaux en arrière-plan peuvent être retardés jusqu’à ce que l’utilisateur interagisse avec l’appareil. Cela entraîne un retard des statistiques **Remis** et **Notification système (affichée dans la barre de notification)** de la campagne push si l’appareil est en veille (la notification sera toujours affichée, sonnera et vibrera en temps réel sans problème).</span><span class="sxs-lookup"><span data-stu-id="97c5c-110">Due to [Background Execution Limits](https://developer.android.com/preview/features/background.html) on Android 8, logs in background might be delayed until the user interacts with the device, this will have an impact on Push Campaign **Delivered** and **System notification displayed** statistics being delayed if the device was sleeping (the notification will still be displayed, will ring and vibrate in real time without issues).</span></span>
* <span data-ttu-id="97c5c-111">En raison des [limites d’exécution en arrière-plan](https://developer.android.com/preview/features/background-location-limits.html), l’emplacement en arrière-plan en temps réel ne sera pas fréquemment mis à jour sur Android 8.</span><span class="sxs-lookup"><span data-stu-id="97c5c-111">Due to [Background Location Limits](https://developer.android.com/preview/features/background-location-limits.html), the real time location in background will not be updated frequently on Android 8.</span></span>

## <a name="424-03302017"></a><span data-ttu-id="97c5c-112">4.2.4 (03/30/2017)</span><span class="sxs-lookup"><span data-stu-id="97c5c-112">4.2.4 (03/30/2017)</span></span>
* <span data-ttu-id="97c5c-113">Résolution du problème des couleurs du texte de notification dans l’application sur Android 7, qui deviennent identiques à celles des versions antérieures d’Android.</span><span class="sxs-lookup"><span data-stu-id="97c5c-113">Fix in-app notification text colors on Android 7 to be the same as older Android versions.</span></span>

## <a name="423-08102016"></a><span data-ttu-id="97c5c-114">4.2.3 (08/10/2016)</span><span class="sxs-lookup"><span data-stu-id="97c5c-114">4.2.3 (08/10/2016)</span></span>
* <span data-ttu-id="97c5c-115">Plus aucun verrou Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="97c5c-115">No more WIFI lock.</span></span>
* <span data-ttu-id="97c5c-116">Résolution d'un blocage lors de l’appel de getDeviceId avant init (bogue introduit dans 4.2.0).</span><span class="sxs-lookup"><span data-stu-id="97c5c-116">Fix a deadlock when calling getDeviceId before init (bug introduced in 4.2.0).</span></span>

## <a name="422-05172016"></a><span data-ttu-id="97c5c-117">4.2.2 (05/17/2016)</span><span class="sxs-lookup"><span data-stu-id="97c5c-117">4.2.2 (05/17/2016)</span></span>
* <span data-ttu-id="97c5c-118">Améliorations de la stabilité.</span><span class="sxs-lookup"><span data-stu-id="97c5c-118">Stability improvements.</span></span>

## <a name="421-05102016"></a><span data-ttu-id="97c5c-119">4.2.1 (05/10/2016)</span><span class="sxs-lookup"><span data-stu-id="97c5c-119">4.2.1 (05/10/2016)</span></span>
* <span data-ttu-id="97c5c-120">Sécurité : Désactivation de l’accès aux fichiers locaux dans les vues web.</span><span class="sxs-lookup"><span data-stu-id="97c5c-120">Security: disable web view local file access.</span></span>
* <span data-ttu-id="97c5c-121">Sécurité : Suppression de la classe `EngagementPreferenceActivity` qui étend la classe `PreferenceActivity` obsolète et non sécurisée.</span><span class="sxs-lookup"><span data-stu-id="97c5c-121">Security: remove `EngagementPreferenceActivity` class that extends obsolete and unsecure `PreferenceActivity` class.</span></span>
* <span data-ttu-id="97c5c-122">Sécurité : Les activités Reach sont maintenant documentées pour utiliser `exported="false"`. Vous pouvez aussi utiliser cet indicateur dans les versions précédentes du SDK.</span><span class="sxs-lookup"><span data-stu-id="97c5c-122">Security: reach activities are now documented to use `exported="false"`, this flag can also be used in previous SDK versions.</span></span>

## <a name="420-03112016"></a><span data-ttu-id="97c5c-123">4.2.0 (03/11/2016)</span><span class="sxs-lookup"><span data-stu-id="97c5c-123">4.2.0 (03/11/2016)</span></span>
* <span data-ttu-id="97c5c-124">Le Kit de développement logiciel (SDK) est désormais sous licence MIT.</span><span class="sxs-lookup"><span data-stu-id="97c5c-124">The SDK is now licensed under MIT.</span></span>
* <span data-ttu-id="97c5c-125">Autorise la spécification d’un identificateur d’appareil personnalisé au moment de l’initialisation du Kit de développement logiciel (SDK).</span><span class="sxs-lookup"><span data-stu-id="97c5c-125">Allow specifying a custom device identifier at SDK initialization time.</span></span>

## <a name="415-02012016"></a><span data-ttu-id="97c5c-126">4.1.5 (01/02/2016)</span><span class="sxs-lookup"><span data-stu-id="97c5c-126">4.1.5 (02/01/2016)</span></span>
* <span data-ttu-id="97c5c-127">Améliorations de la stabilité.</span><span class="sxs-lookup"><span data-stu-id="97c5c-127">Stability improvements.</span></span>

## <a name="414-01262016"></a><span data-ttu-id="97c5c-128">4.1.4 (26/01/2016)</span><span class="sxs-lookup"><span data-stu-id="97c5c-128">4.1.4 (01/26/2016)</span></span>
* <span data-ttu-id="97c5c-129">Améliorations de la stabilité.</span><span class="sxs-lookup"><span data-stu-id="97c5c-129">Stability improvements.</span></span>

## <a name="413-1292015"></a><span data-ttu-id="97c5c-130">4.1.3 (12/9/2015)</span><span class="sxs-lookup"><span data-stu-id="97c5c-130">4.1.3 (12/9/2015)</span></span>
* <span data-ttu-id="97c5c-131">Améliorations de la stabilité.</span><span class="sxs-lookup"><span data-stu-id="97c5c-131">Stability improvements.</span></span>

## <a name="412-11252015"></a><span data-ttu-id="97c5c-132">4.1.2 (25/11/2015)</span><span class="sxs-lookup"><span data-stu-id="97c5c-132">4.1.2 (11/25/2015)</span></span>
* <span data-ttu-id="97c5c-133">Améliorations de la stabilité.</span><span class="sxs-lookup"><span data-stu-id="97c5c-133">Stability improvements.</span></span>

## <a name="411-11042015"></a><span data-ttu-id="97c5c-134">4.1.1 (11/04/2015)</span><span class="sxs-lookup"><span data-stu-id="97c5c-134">4.1.1 (11/04/2015)</span></span>
* <span data-ttu-id="97c5c-135">Améliorations de la stabilité.</span><span class="sxs-lookup"><span data-stu-id="97c5c-135">Stability improvements.</span></span>

## <a name="410-08252015"></a><span data-ttu-id="97c5c-136">4.1.0 (25/08/2015)</span><span class="sxs-lookup"><span data-stu-id="97c5c-136">4.1.0 (08/25/2015)</span></span>
* <span data-ttu-id="97c5c-137">Gestion du nouveau modèle d’autorisation pour Android M.</span><span class="sxs-lookup"><span data-stu-id="97c5c-137">Handle new permission model for Android M.</span></span>
* <span data-ttu-id="97c5c-138">Vous pouvez désormais configurer les fonctionnalités de localisation lors de l’exécution au lieu d’utiliser `AndroidManifest.xml`.</span><span class="sxs-lookup"><span data-stu-id="97c5c-138">Can now configure location features at runtime instead of using  `AndroidManifest.xml`.</span></span>
* <span data-ttu-id="97c5c-139">Résolution d’un bogue d’autorisation : si vous utilisez `ACCESS_FINE_LOCATION`, `ACCESS_COARSE_LOCATION` n’est plus nécessaire.</span><span class="sxs-lookup"><span data-stu-id="97c5c-139">Fix a permission bug: if you use `ACCESS_FINE_LOCATION`, then `ACCESS_COARSE_LOCATION` is not needed anymore.</span></span>
* <span data-ttu-id="97c5c-140">Améliorations de la stabilité.</span><span class="sxs-lookup"><span data-stu-id="97c5c-140">Stability improvements.</span></span>

## <a name="400-07062015"></a><span data-ttu-id="97c5c-141">4.0.0 (06/07/2015)</span><span class="sxs-lookup"><span data-stu-id="97c5c-141">4.0.0 (07/06/2015)</span></span>
* <span data-ttu-id="97c5c-142">Modifications de protocole interne pour rendre les analyses et la diffusion plus fiables.</span><span class="sxs-lookup"><span data-stu-id="97c5c-142">Internal protocol changes to make analytics and push more reliable.</span></span>
* <span data-ttu-id="97c5c-143">Native Push (GCM/ADM) est désormais également utilisé pour les notifications dans l’application. Vous devez donc configurer les informations d’identification Native Push pour tout type de campagne push.</span><span class="sxs-lookup"><span data-stu-id="97c5c-143">Native push (GCM/ADM) is now also used for in app notifications so you must configure the native push credentials for any type of push campaign.</span></span>
* <span data-ttu-id="97c5c-144">Correction de la notification de la vue d’ensemble : elle ne s’affichait que 10 s après avoir été transmise.</span><span class="sxs-lookup"><span data-stu-id="97c5c-144">Fix big picture notification: they were displayed only 10s after being pushed.</span></span>
* <span data-ttu-id="97c5c-145">Résolution d’un bogue dans l’affichage web : un clic sur un lien exécutait également l’URL de l’action par défaut.</span><span class="sxs-lookup"><span data-stu-id="97c5c-145">Fix a bug in web view: clicking on a link was also executing the default action URL.</span></span>
* <span data-ttu-id="97c5c-146">Résolution d’un blocage rare lié à la gestion du stockage local.</span><span class="sxs-lookup"><span data-stu-id="97c5c-146">Fix a rare crash related to local storage management.</span></span>
* <span data-ttu-id="97c5c-147">Correction de la gestion des chaînes de configuration dynamique.</span><span class="sxs-lookup"><span data-stu-id="97c5c-147">Fix dynamic configuration string management.</span></span>
* <span data-ttu-id="97c5c-148">Mise à jour du CLUF.</span><span class="sxs-lookup"><span data-stu-id="97c5c-148">Update EULA.</span></span>

## <a name="300-02172015"></a><span data-ttu-id="97c5c-149">3.0.0 (17/02/2015)</span><span class="sxs-lookup"><span data-stu-id="97c5c-149">3.0.0 (02/17/2015)</span></span>
* <span data-ttu-id="97c5c-150">Version initiale d'Azure Engagement Mobile</span><span class="sxs-lookup"><span data-stu-id="97c5c-150">Initial Release of Azure Mobile Engagement</span></span>
* <span data-ttu-id="97c5c-151">La configuration d'appId est remplacée par la configuration d'une chaîne de connexion.</span><span class="sxs-lookup"><span data-stu-id="97c5c-151">appId configuration is replaced by a connection string configuration.</span></span>
* <span data-ttu-id="97c5c-152">Suppression de l'API pour envoyer et recevoir des messages XMPP arbitraires d'entités XMPP arbitraires.</span><span class="sxs-lookup"><span data-stu-id="97c5c-152">Removed API to send and receive arbitrary XMPP messages from arbitrary XMPP entities.</span></span>
* <span data-ttu-id="97c5c-153">Suppression de l'API pour envoyer et recevoir des messages entre appareils.</span><span class="sxs-lookup"><span data-stu-id="97c5c-153">Removed API to send and receive messages between devices.</span></span>
* <span data-ttu-id="97c5c-154">Améliorations de sécurité.</span><span class="sxs-lookup"><span data-stu-id="97c5c-154">Security improvements.</span></span>
* <span data-ttu-id="97c5c-155">Suppression du suivi de Google Play et SmartAd.</span><span class="sxs-lookup"><span data-stu-id="97c5c-155">Google Play and SmartAd tracking removed.</span></span>

