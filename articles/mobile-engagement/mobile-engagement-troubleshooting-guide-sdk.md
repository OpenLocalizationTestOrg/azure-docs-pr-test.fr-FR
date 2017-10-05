---
title: "Guide de dépannage d’Azure Mobile Engagement - Kit de développement logiciel (SDK)"
description: "Résolution des problèmes d’intégration du Kit de développement logiciel (SDK) dans Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: de265cf1-2f88-43ef-8616-156ada5be7b6
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 4d9d6165deb4bd0c65f1841aa7c457363a1f2865
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting-guide-for-sdk-integration-issues"></a><span data-ttu-id="d017a-103">Guide de dépannage pour les problèmes d’intégration du Kit de développement logiciel (SDK)</span><span class="sxs-lookup"><span data-stu-id="d017a-103">Troubleshooting guide for SDK integration issues</span></span>
<span data-ttu-id="d017a-104">Les éléments suivants sont des problèmes potentiels liés à la façon dont Azure Mobile Engagement s’intègre dans votre application.</span><span class="sxs-lookup"><span data-stu-id="d017a-104">The following are possible issues you may encounter with how Azure Mobile Engagement integrates into your application.</span></span>

## <a name="sdk-issues-discovered-by-a-failure-in-another-area-of-your-application"></a><span data-ttu-id="d017a-105">Problèmes du Kit de développement logiciel (SDK) découverts par un échec dans une autre partie de votre application</span><span class="sxs-lookup"><span data-stu-id="d017a-105">SDK issues discovered by a failure in another area of your application</span></span>
### <a name="issue"></a><span data-ttu-id="d017a-106">Problème</span><span class="sxs-lookup"><span data-stu-id="d017a-106">Issue</span></span>
* <span data-ttu-id="d017a-107">Échec de la collecte de données de l'interface utilisateur (dans Analyse, Surveillance, Segmentation ou Tableaux de bord).</span><span class="sxs-lookup"><span data-stu-id="d017a-107">UI data collection failure (in Analytics, Monitoring, Segmentation, or Dashboards).</span></span>
* <span data-ttu-id="d017a-108">Échec push (push ne fonctionne pas dans l'application, en dehors de l'application, ou les deux).</span><span class="sxs-lookup"><span data-stu-id="d017a-108">Push Failures (Pushes don't work in app, out of app, or both).</span></span>
* <span data-ttu-id="d017a-109">Échecs de composants avancés (le suivi, la géolocalisation ou les push spécifiques à une plateforme ne fonctionnent pas).</span><span class="sxs-lookup"><span data-stu-id="d017a-109">Advanced Feature Failures (Tracking, Geolocation, or platform specific Pushes don’t work).</span></span>
* <span data-ttu-id="d017a-110">Échecs d'API (les API échouent souvent en mode silencieux sans afficher de message d'erreur).</span><span class="sxs-lookup"><span data-stu-id="d017a-110">API Failures (APIs fail often silently without error messages).</span></span>
* <span data-ttu-id="d017a-111">Défaillances du service (aucun élément d'Azure Mobile Engagement ne fonctionne avec votre application).</span><span class="sxs-lookup"><span data-stu-id="d017a-111">Service Failures (none of Azure Mobile Engagement works for your application).</span></span>

### <a name="causes"></a><span data-ttu-id="d017a-112">Causes</span><span class="sxs-lookup"><span data-stu-id="d017a-112">Causes</span></span>
* <span data-ttu-id="d017a-113">La plupart des problèmes qui doivent être résolus avec le Kit de développement logiciel Azure Mobile Engagement sera découvert par un échec dans votre application (par exemple, un échec de collecte des données de l'interface utilisateur, Échec de transmission, Échec de la fonctionnalité avancée, Échec de l'API, Application tombe en panne ou interruption de service apparente).</span><span class="sxs-lookup"><span data-stu-id="d017a-113">Most issues that need to be resolved with the Azure Mobile Engagement SDK will be discovered by a failure in your application (such as a UI data collection failure, push failure, advanced feature failure, API failure, Application crashes, or apparent service outage).</span></span>  
* <span data-ttu-id="d017a-114">Si une fonctionnalité particulière d'Azure Mobile Engagement n'a jamais fonctionné dans votre application auparavant, vous devez terminer l'intégration.</span><span class="sxs-lookup"><span data-stu-id="d017a-114">If a particular feature of Azure Mobile Engagement has never worked in your app before, you will need to complete the integration.</span></span> 
* <span data-ttu-id="d017a-115">Si une fonctionnalité particulière de l'Engagement Mobile Azure fonctionnait et arrêté, vous devrez peut-être mettre à niveau vers la dernière version avec l'Engagement de Mobile Azure SDK.</span><span class="sxs-lookup"><span data-stu-id="d017a-115">If a particular feature of Azure Mobile Engagement was working and stopped, you may need to upgrade to the last version with the Azure Mobile Engagement SDK.</span></span> <span data-ttu-id="d017a-116">N’oubliez pas qu’il existe une autre version du Kit de développement logiciel (SDK) d’Azure Mobile Engagement pour chaque plateforme prise en charge par Azure Mobile Engagement (Android, iOS, Windows et Windows Phone).</span><span class="sxs-lookup"><span data-stu-id="d017a-116">Remember that there is a different version of the Azure Mobile Engagement SDK for each platform supported by Azure Mobile Engagement (Android, iOS, Windows, and Windows Phone).</span></span>

#### <a name="sdk-integration"></a><span data-ttu-id="d017a-117">Intégration du Kit de développement logiciel (SDK)</span><span class="sxs-lookup"><span data-stu-id="d017a-117">SDK Integration</span></span>
* <span data-ttu-id="d017a-118">Azure Mobile Engagement n'est pas correctement intégré dans le Kit de développement logiciel (Analyse).</span><span class="sxs-lookup"><span data-stu-id="d017a-118">Azure Mobile Engagement not correctly integrated in SDK (Analytics).</span></span>
* <span data-ttu-id="d017a-119">Reach n'est pas correctement intégré dans le Kit de développement logiciel (push dans l'application et en dehors de l'application).</span><span class="sxs-lookup"><span data-stu-id="d017a-119">Reach not correctly integrated in SDK (In App and Out of App Pushes).</span></span>
* <span data-ttu-id="d017a-120">Certificat expiré ou PROD et DEV incorrects (iOS uniquement).</span><span class="sxs-lookup"><span data-stu-id="d017a-120">Certificate expired or incorrect PROD vs. DEV (iOS only).</span></span>
* <span data-ttu-id="d017a-121">GCM ou ADM n'est pas correctement intégré dans le Kit de développement logiciel (Android uniquement - Push spécifique au service).</span><span class="sxs-lookup"><span data-stu-id="d017a-121">GCM or ADM not correctly integrated in SDK (Android only - Service Specific Pushes).</span></span>
* <span data-ttu-id="d017a-122">Le suivi n'est pas correctement intégré dans le Kit de développement logiciel (installer le suivi de magasin).</span><span class="sxs-lookup"><span data-stu-id="d017a-122">Tracking not correctly integrated in SDK (Install store tracking).</span></span>
* <span data-ttu-id="d017a-123">Intégration incorrecte de l'emplacement tardif ou de l'emplacement GPS dans le Kit de développement logiciel (ciblage par emplacement géographique).</span><span class="sxs-lookup"><span data-stu-id="d017a-123">Lazy Location or GPS Location not correctly integrated in SDK (Targeting by geo-location).</span></span>

<span data-ttu-id="d017a-124">**Voir aussi :**</span><span class="sxs-lookup"><span data-stu-id="d017a-124">**See also:**</span></span>

* <span data-ttu-id="d017a-125">[Documentation du Kit de développement logiciel (SDK) - Guide d’intégration][Link 5]</span><span class="sxs-lookup"><span data-stu-id="d017a-125">[SDK Documentation - Integration Guides][Link 5]</span></span> 
* <span data-ttu-id="d017a-126">[Guide de résolution des problèmes - Push][Link 23]</span><span class="sxs-lookup"><span data-stu-id="d017a-126">[Troubleshooting Guide - Push][Link 23]</span></span>

#### <a name="sdk-upgrade"></a><span data-ttu-id="d017a-127">Mise à niveau du Kit de développement logiciel (SDK) :</span><span class="sxs-lookup"><span data-stu-id="d017a-127">SDK Upgrade</span></span>
* <span data-ttu-id="d017a-128">Vous devez mettre à niveau le Kit de développement logiciel pour résoudre des problèmes des versions antérieures du Kit de développement logiciel (souvent liés à des versions plus récentes du système d'exploitation du périphérique).</span><span class="sxs-lookup"><span data-stu-id="d017a-128">Need to upgrade SDK to resolve issues with older versions of the SDK (often related to newer versions of the device OS).</span></span>
* <span data-ttu-id="d017a-129">Désinstallez toutes les versions précédentes de votre application de votre appareil et réinstallez la version la plus récente de votre application, réenregistrez votre ID de périphérique à partir de l'interface utilisateur d'Azure Mobile Engagement pour confirmer que votre appareil utilise la version la plus récente de votre application.</span><span class="sxs-lookup"><span data-stu-id="d017a-129">Uninstall all previous versions of your app from your device and reinstall the newest version of your app, the re-register your Device ID from the Azure Mobile Engagement UI to confirm that your device is using the newest version of your app.</span></span>

<span data-ttu-id="d017a-130">**Voir aussi :**</span><span class="sxs-lookup"><span data-stu-id="d017a-130">**See also:**</span></span>

* [<span data-ttu-id="d017a-131">Documentation du Kit de développement logiciel (SDK) - Notes de publication</span><span class="sxs-lookup"><span data-stu-id="d017a-131">SDK Documentation - Release Notes</span></span>](http://go.microsoft.com/fwlink/?LinkId= 525554) 
* [<span data-ttu-id="d017a-132">Documentation du Kit de développement logiciel - Guides de mise à niveau</span><span class="sxs-lookup"><span data-stu-id="d017a-132">SDK Documentation - Upgrade Guides</span></span>](http://go.microsoft.com/fwlink/?LinkId= 525554)

#### <a name="sdk-other"></a><span data-ttu-id="d017a-133">Kit de développement logiciel (SDK), autres :</span><span class="sxs-lookup"><span data-stu-id="d017a-133">SDK Other</span></span>
* <span data-ttu-id="d017a-134">Des erreurs dans le manifeste d'application « AndroidManifest.xml » peuvent empêcher Azure Mobile Engagement de fonctionner (Android uniquement).</span><span class="sxs-lookup"><span data-stu-id="d017a-134">Errors in Application Manifest "AndroidManifest.xml" can cause Azure Mobile Engagement not to work (Android only).</span></span>
* <span data-ttu-id="d017a-135">Un autre problème courant avec l’intégration du Kit de développement logiciel (SDK) et l’utilisation de l’API est la confusion entre la clé du Kit de développement logiciel et la clé d’API.</span><span class="sxs-lookup"><span data-stu-id="d017a-135">A common issue with SDK integration and API usage is to confuse the SDK Key and the API Key.</span></span>

<span data-ttu-id="d017a-136">**Voir aussi :**</span><span class="sxs-lookup"><span data-stu-id="d017a-136">**See also:**</span></span>

* <span data-ttu-id="d017a-137">[Concepts - Glossaire][Link 6]</span><span class="sxs-lookup"><span data-stu-id="d017a-137">[Concepts - Glossary][Link 6]</span></span>

## <a name="advanced-coding-issues"></a><span data-ttu-id="d017a-138">Problèmes de codage avancé</span><span class="sxs-lookup"><span data-stu-id="d017a-138">Advanced coding issues</span></span>
### <a name="issue"></a><span data-ttu-id="d017a-139">Problème</span><span class="sxs-lookup"><span data-stu-id="d017a-139">Issue</span></span>
* <span data-ttu-id="d017a-140">Le code spécifique de plate-forme pas directement lié à Azure Mobile Engagement peut provoquer des problèmes sur iOS, Android et Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="d017a-140">Platform specific code not directly related to Azure Mobile Engagement can cause issues on iOS, Android, and Windows Phone.</span></span>

### <a name="causes"></a><span data-ttu-id="d017a-141">Causes</span><span class="sxs-lookup"><span data-stu-id="d017a-141">Causes</span></span>
* <span data-ttu-id="d017a-142">Beaucoup avancée des problèmes de codage avec Azure Mobile Engagement sont provoquées par le code spécifique de plate-forme mal écrit pas directement lié à l'Engagement de Mobile Azure.</span><span class="sxs-lookup"><span data-stu-id="d017a-142">Many advanced coding issues with Azure Mobile Engagement are caused by improperly written platform specific code not directly related to Azure Mobile Engagement.</span></span> <span data-ttu-id="d017a-143">Outre la documentation d'Azure Mobile Engagement, vous devez consulter la documentation spécifique à la plateforme sur laquelle vous développez (Android, iOS, Web, Windows et Windows Phone).</span><span class="sxs-lookup"><span data-stu-id="d017a-143">You will need to consult documentation specific to the platform you are developing for in addition to Azure Mobile Engagement documentation (Android, iOS, Web, Windows, and Windows Phone).</span></span>
* <span data-ttu-id="d017a-144">Ne pas configurer correctement « categories » empêche de lier une notification à un autre emplacement à l'intérieur ou en dehors de l'application (Android uniquement).</span><span class="sxs-lookup"><span data-stu-id="d017a-144">Not correctly configuring "categories", prevents linking from a notification to another location either inside or outside of the app (Android only).</span></span> 
* <span data-ttu-id="d017a-145">Ne pas définir « UIKit.framework » sur « facultatif » dans votre code iOS affiche un « Symbole erreur introuvable » et/ou des blocages sur les anciens périphériques iOS (iOS uniquement).</span><span class="sxs-lookup"><span data-stu-id="d017a-145">Not setting "UIKit.framework" to "optional" in your iOS code, shows a "Symbol not found error" and/or crashes on older iOS devices (iOS only).</span></span>
* <span data-ttu-id="d017a-146">Les certificats expirés ou qui ne sont pas correctement configurés à l'aide de la version de développement ou de production Prod du certificat, provoquent des problèmes push (iOS uniquement).</span><span class="sxs-lookup"><span data-stu-id="d017a-146">Expired certificates or not correctly using the DEV or Prod version of the cert, causes push issues (iOS only).</span></span>
* <span data-ttu-id="d017a-147">Il existe certaines limitations inhérentes à une plateforme qu'Azure Mobile Engagement n'est pas en mesure de contrôler (par exemple le fonctionnement de system center pour les push en dehors de l'application dans Android et iOS).</span><span class="sxs-lookup"><span data-stu-id="d017a-147">There are some limitations inherent to a platform that Azure Mobile Engagement can't control (like how the system center works for out of app pushes in Android and iOS).</span></span>
* <span data-ttu-id="d017a-148">Azure Mobile Engagement publie une liste complète des packages internes utilisé par Azure Mobile Engagement pour iOS et Android à des fins de référence.</span><span class="sxs-lookup"><span data-stu-id="d017a-148">Azure Mobile Engagement publishes a full list of the internal packages used by Azure Mobile Engagement for iOS and Android for reference.</span></span> <span data-ttu-id="d017a-149">N'oubliez pas que certaines fonctionnalités d'Azure Mobile Engagement sont spécifiques à la plate-forme (Android, iOS, Web, Windows et Windows Phone).</span><span class="sxs-lookup"><span data-stu-id="d017a-149">Keep in mind that some features of Azure Mobile Engagement are specific to the platform (Android, iOS, Web, Windows, and Windows Phone).</span></span>

### <a name="see-also"></a><span data-ttu-id="d017a-150">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="d017a-150">See also</span></span>
* <span data-ttu-id="d017a-151">[Guide de résolution des problèmes - Push][Link 23]</span><span class="sxs-lookup"><span data-stu-id="d017a-151">[Troubleshooting Guide - Push][Link 23]</span></span> 
* <span data-ttu-id="d017a-152">[Documentation du Kit de développement logiciel (SDK) - Notes de publication][Link 5]</span><span class="sxs-lookup"><span data-stu-id="d017a-152">[SDK Documentation - Release Notes][Link 5]</span></span>
* <span data-ttu-id="d017a-153">[Documentation du Kit de développement logiciel (SDK) - Guides de mise à niveau][Link 5]</span><span class="sxs-lookup"><span data-stu-id="d017a-153">[SDK Documentation - Upgrade Guides][Link 5]</span></span>

## <a name="application-crashes"></a><span data-ttu-id="d017a-154">Blocage de l’application</span><span class="sxs-lookup"><span data-stu-id="d017a-154">Application crashes</span></span>
### <a name="issue"></a><span data-ttu-id="d017a-155">Problème</span><span class="sxs-lookup"><span data-stu-id="d017a-155">Issue</span></span>
* <span data-ttu-id="d017a-156">Votre application se bloque sur un périphérique de l'utilisateur final.</span><span class="sxs-lookup"><span data-stu-id="d017a-156">Your application crashes on the end users' device.</span></span>

### <a name="causes"></a><span data-ttu-id="d017a-157">Causes</span><span class="sxs-lookup"><span data-stu-id="d017a-157">Causes</span></span>
* <span data-ttu-id="d017a-158">Les informations de blocage peuvent être consultées dans *l’interface utilisateur d’analyse* ou *l’API d’analyse*.</span><span class="sxs-lookup"><span data-stu-id="d017a-158">Crash information can be viewed in the *Analytics UI* or the *Analytics API*</span></span>
* <span data-ttu-id="d017a-159">Vous pouvez trouver l'ID de périphérique de votre périphérique de test et exécuter l'action à l'origine du blocage de votre application chez un utilisateur final afin d'identifier la cause de l'incident.</span><span class="sxs-lookup"><span data-stu-id="d017a-159">You can find the Device ID of your test device and take the same action that caused your application to crash for an end user to help identify the cause of your crash.</span></span>
* <span data-ttu-id="d017a-160">Les problèmes connus avec le Kit de développement logiciel (SDK) Mobile Azure Engagement qui provoquent le blocage des applications sont parfois résolus par la mise à niveau vers la dernière version du Kit de développement logiciel.</span><span class="sxs-lookup"><span data-stu-id="d017a-160">Known issues with the Azure Mobile Engagement SDK that cause applications to crash are sometimes resolved by upgrading to the latest version of the SDK.</span></span> <span data-ttu-id="d017a-161">Par conséquent, veillez à vérifier les notes de publication de votre plateforme quand vous recherchez la cause d’un blocage.</span><span class="sxs-lookup"><span data-stu-id="d017a-161">Make sure to check the release notes about your platform when investigating crashes.</span></span>

### <a name="see-also"></a><span data-ttu-id="d017a-162">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="d017a-162">See also</span></span>
* <span data-ttu-id="d017a-163">[Documentation du Kit de développement logiciel (SDK) - Notes de publication][Link 5]</span><span class="sxs-lookup"><span data-stu-id="d017a-163">[SDK Documentation - Release Notes][Link 5]</span></span>
* <span data-ttu-id="d017a-164">[Documentation du Kit de développement logiciel (SDK) - Guides de mise à niveau][Link 5]</span><span class="sxs-lookup"><span data-stu-id="d017a-164">[SDK Documentation - Upgrade Guides][Link 5]</span></span>

## <a name="app-store-upload-failures"></a><span data-ttu-id="d017a-165">Échecs de téléchargement App Store</span><span class="sxs-lookup"><span data-stu-id="d017a-165">App store upload failures</span></span>
### <a name="issue"></a><span data-ttu-id="d017a-166">Problème</span><span class="sxs-lookup"><span data-stu-id="d017a-166">Issue</span></span>
* <span data-ttu-id="d017a-167">Les erreurs liées au téléchargement de la dernière version de votre application dans Apple, Google ou le magasin d’applications Windows.</span><span class="sxs-lookup"><span data-stu-id="d017a-167">Errors related to uploading the latest version of your app to Apple, Google, or the Windows App store.</span></span>

### <a name="causes"></a><span data-ttu-id="d017a-168">Causes</span><span class="sxs-lookup"><span data-stu-id="d017a-168">Causes</span></span>
* <span data-ttu-id="d017a-169">Le magasin d’applications Windows bloque parfois les applications avec certaines fonctionnalités activées (l’Apple Store empêche l’utilisation de IDFV dans les applications du magasin et le magasin GooglePlay empêche le partage d’informations d’application entre les applications).</span><span class="sxs-lookup"><span data-stu-id="d017a-169">App stores sometimes block apps with certain features enabled (e.g. the Apple Store prevents the use of IDFV in apps in the store and the GooglePlay store prevents the sharing of application information between apps).</span></span> 
* <span data-ttu-id="d017a-170">Veillez à consulter les notes de publication sur votre plateforme et la version actuelle du SDK si vous avez des difficultés à télécharger une application dans le magasin.</span><span class="sxs-lookup"><span data-stu-id="d017a-170">Make sure that you check the release notes about your platform and current version of the SDK if you have difficulty uploading an app to the store.</span></span>

<!--Link references-->
[Link 1]: mobile-engagement-user-interface.md
[Link 2]: mobile-engagement-troubleshooting-guide.md
[Link 3]: mobile-engagement-how-tos.md
[Link 4]: http://go.microsoft.com/fwlink/?LinkID=525553
[Link 5]: http://go.microsoft.com/fwlink/?LinkID=525554
[Link 6]: http://go.microsoft.com/fwlink/?LinkId=525555
[Link 7]: https://account.windowsazure.com/PreviewFeatures
[Link 8]: https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=azuremobileengagement
[Link 9]: http://azure.microsoft.com/en-us/services/mobile-engagement/
[Link 10]: http://azure.microsoft.com/en-us/documentation/services/mobile-engagement/
[Link 11]: http://azure.microsoft.com/en-us/pricing/details/mobile-engagement/
[Link 12]: mobile-engagement-user-interface-navigation.md
[Link 13]: mobile-engagement-user-interface-home.md
[Link 14]: mobile-engagement-user-interface-my-account.md
[Link 15]: mobile-engagement-user-interface-analytics.md
[Link 16]: mobile-engagement-user-interface-monitor.md
[Link 17]: mobile-engagement-user-interface-reach.md
[Link 18]: mobile-engagement-user-interface-segments.md
[Link 19]: mobile-engagement-user-interface-dashboard.md
[Link 20]: mobile-engagement-user-interface-settings.md
[Link 21]: mobile-engagement-troubleshooting-guide-analytics.md
[Link 22]: mobile-engagement-troubleshooting-guide-apis.md
[Link 23]: mobile-engagement-troubleshooting-guide-push-reach.md
[Link 24]: mobile-engagement-troubleshooting-guide-service.md
[Link 25]: mobile-engagement-troubleshooting-guide-sdk.md
[Link 26]: mobile-engagement-troubleshooting-guide-sr-info.md
[Link 27]: mobile-engagement-user-interface-reach-campaign.md
[Link 28]: mobile-engagement-user-interface-reach-criterion.md
[Link 29]: mobile-engagement-user-interface-reach-content.md

