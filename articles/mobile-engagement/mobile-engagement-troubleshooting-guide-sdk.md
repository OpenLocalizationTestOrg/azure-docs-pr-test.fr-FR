---
title: aaaAzure Mobile Engagement Troubleshooting Guide - SDK
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
ms.openlocfilehash: 1c082b81d898f4bdb47b8efe6cfbacfd83fe9279
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-guide-for-sdk-integration-issues"></a><span data-ttu-id="1f382-103">Guide de dépannage pour les problèmes d’intégration du Kit de développement logiciel (SDK)</span><span class="sxs-lookup"><span data-stu-id="1f382-103">Troubleshooting guide for SDK integration issues</span></span>
<span data-ttu-id="1f382-104">Hello Voici les problèmes possibles, que vous pouvez rencontrer avec l’intégration de Azure Mobile Engagement dans votre application.</span><span class="sxs-lookup"><span data-stu-id="1f382-104">hello following are possible issues you may encounter with how Azure Mobile Engagement integrates into your application.</span></span>

## <a name="sdk-issues-discovered-by-a-failure-in-another-area-of-your-application"></a><span data-ttu-id="1f382-105">Problèmes du Kit de développement logiciel (SDK) découverts par un échec dans une autre partie de votre application</span><span class="sxs-lookup"><span data-stu-id="1f382-105">SDK issues discovered by a failure in another area of your application</span></span>
### <a name="issue"></a><span data-ttu-id="1f382-106">Problème</span><span class="sxs-lookup"><span data-stu-id="1f382-106">Issue</span></span>
* <span data-ttu-id="1f382-107">Échec de la collecte de données de l'interface utilisateur (dans Analyse, Surveillance, Segmentation ou Tableaux de bord).</span><span class="sxs-lookup"><span data-stu-id="1f382-107">UI data collection failure (in Analytics, Monitoring, Segmentation, or Dashboards).</span></span>
* <span data-ttu-id="1f382-108">Échec push (push ne fonctionne pas dans l'application, en dehors de l'application, ou les deux).</span><span class="sxs-lookup"><span data-stu-id="1f382-108">Push Failures (Pushes don't work in app, out of app, or both).</span></span>
* <span data-ttu-id="1f382-109">Échecs de composants avancés (le suivi, la géolocalisation ou les push spécifiques à une plateforme ne fonctionnent pas).</span><span class="sxs-lookup"><span data-stu-id="1f382-109">Advanced Feature Failures (Tracking, Geolocation, or platform specific Pushes don’t work).</span></span>
* <span data-ttu-id="1f382-110">Échecs d'API (les API échouent souvent en mode silencieux sans afficher de message d'erreur).</span><span class="sxs-lookup"><span data-stu-id="1f382-110">API Failures (APIs fail often silently without error messages).</span></span>
* <span data-ttu-id="1f382-111">Défaillances du service (aucun élément d'Azure Mobile Engagement ne fonctionne avec votre application).</span><span class="sxs-lookup"><span data-stu-id="1f382-111">Service Failures (none of Azure Mobile Engagement works for your application).</span></span>

### <a name="causes"></a><span data-ttu-id="1f382-112">Causes</span><span class="sxs-lookup"><span data-stu-id="1f382-112">Causes</span></span>
* <span data-ttu-id="1f382-113">La plupart des problèmes nécessitant toobe résolu par hello Azure Mobile Engagement SDK sera découvert par un échec dans votre application (par exemple, un échec de collecte des données de l’interface utilisateur, Échec de transmission, Échec de la fonctionnalité avancée, Échec de l’API, Application tombe en panne ou service apparent panne).</span><span class="sxs-lookup"><span data-stu-id="1f382-113">Most issues that need toobe resolved with hello Azure Mobile Engagement SDK will be discovered by a failure in your application (such as a UI data collection failure, push failure, advanced feature failure, API failure, Application crashes, or apparent service outage).</span></span>  
* <span data-ttu-id="1f382-114">Si une fonctionnalité particulière d’Azure Mobile Engagement n’a jamais travaillé dans votre application avant, vous devez l’intégration toocomplete hello.</span><span class="sxs-lookup"><span data-stu-id="1f382-114">If a particular feature of Azure Mobile Engagement has never worked in your app before, you will need toocomplete hello integration.</span></span> 
* <span data-ttu-id="1f382-115">Si une fonctionnalité particulière d’Azure Mobile Engagement a été fonctionne et s’est arrêté, vous devrez peut-être tooupgrade toohello la dernière version avec hello Kit de développement logiciel Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="1f382-115">If a particular feature of Azure Mobile Engagement was working and stopped, you may need tooupgrade toohello last version with hello Azure Mobile Engagement SDK.</span></span> <span data-ttu-id="1f382-116">N’oubliez pas qu’il existe une autre version du Kit de développement logiciel Azure Mobile Engagement de hello pour chaque plateforme prise en charge par Azure Mobile Engagement (Android, iOS, Windows et Windows Phone).</span><span class="sxs-lookup"><span data-stu-id="1f382-116">Remember that there is a different version of hello Azure Mobile Engagement SDK for each platform supported by Azure Mobile Engagement (Android, iOS, Windows, and Windows Phone).</span></span>

#### <a name="sdk-integration"></a><span data-ttu-id="1f382-117">Intégration du Kit de développement logiciel (SDK)</span><span class="sxs-lookup"><span data-stu-id="1f382-117">SDK Integration</span></span>
* <span data-ttu-id="1f382-118">Azure Mobile Engagement n'est pas correctement intégré dans le Kit de développement logiciel (Analyse).</span><span class="sxs-lookup"><span data-stu-id="1f382-118">Azure Mobile Engagement not correctly integrated in SDK (Analytics).</span></span>
* <span data-ttu-id="1f382-119">Reach n'est pas correctement intégré dans le Kit de développement logiciel (push dans l'application et en dehors de l'application).</span><span class="sxs-lookup"><span data-stu-id="1f382-119">Reach not correctly integrated in SDK (In App and Out of App Pushes).</span></span>
* <span data-ttu-id="1f382-120">Certificat expiré ou PROD et DEV incorrects (iOS uniquement).</span><span class="sxs-lookup"><span data-stu-id="1f382-120">Certificate expired or incorrect PROD vs. DEV (iOS only).</span></span>
* <span data-ttu-id="1f382-121">GCM ou ADM n'est pas correctement intégré dans le Kit de développement logiciel (Android uniquement - Push spécifique au service).</span><span class="sxs-lookup"><span data-stu-id="1f382-121">GCM or ADM not correctly integrated in SDK (Android only - Service Specific Pushes).</span></span>
* <span data-ttu-id="1f382-122">Le suivi n'est pas correctement intégré dans le Kit de développement logiciel (installer le suivi de magasin).</span><span class="sxs-lookup"><span data-stu-id="1f382-122">Tracking not correctly integrated in SDK (Install store tracking).</span></span>
* <span data-ttu-id="1f382-123">Intégration incorrecte de l'emplacement tardif ou de l'emplacement GPS dans le Kit de développement logiciel (ciblage par emplacement géographique).</span><span class="sxs-lookup"><span data-stu-id="1f382-123">Lazy Location or GPS Location not correctly integrated in SDK (Targeting by geo-location).</span></span>

<span data-ttu-id="1f382-124">**Voir aussi :**</span><span class="sxs-lookup"><span data-stu-id="1f382-124">**See also:**</span></span>

* <span data-ttu-id="1f382-125">[Documentation du Kit de développement logiciel (SDK) - Guide d’intégration][Link 5]</span><span class="sxs-lookup"><span data-stu-id="1f382-125">[SDK Documentation - Integration Guides][Link 5]</span></span> 
* <span data-ttu-id="1f382-126">[Guide de résolution des problèmes - Push][Link 23]</span><span class="sxs-lookup"><span data-stu-id="1f382-126">[Troubleshooting Guide - Push][Link 23]</span></span>

#### <a name="sdk-upgrade"></a><span data-ttu-id="1f382-127">Mise à niveau du Kit de développement logiciel (SDK) :</span><span class="sxs-lookup"><span data-stu-id="1f382-127">SDK Upgrade</span></span>
* <span data-ttu-id="1f382-128">Peut-être des problèmes de tooresolve tooupgrade Kit de développement logiciel avec les versions antérieures du Kit de développement logiciel (souvent connexes toonewer versions de système d’exploitation du périphérique hello) de hello.</span><span class="sxs-lookup"><span data-stu-id="1f382-128">Need tooupgrade SDK tooresolve issues with older versions of hello SDK (often related toonewer versions of hello device OS).</span></span>
* <span data-ttu-id="1f382-129">Désinstallez toutes les versions précédentes de votre application à partir de votre appareil et réinstallez la version la plus récente de votre application hello, hello réinscrire votre ID d’appareil à partir de tooconfirm de l’interface utilisateur de Azure Mobile Engagement hello que votre appareil utilise la version la plus récente de votre application hello.</span><span class="sxs-lookup"><span data-stu-id="1f382-129">Uninstall all previous versions of your app from your device and reinstall hello newest version of your app, hello re-register your Device ID from hello Azure Mobile Engagement UI tooconfirm that your device is using hello newest version of your app.</span></span>

<span data-ttu-id="1f382-130">**Voir aussi :**</span><span class="sxs-lookup"><span data-stu-id="1f382-130">**See also:**</span></span>

* [<span data-ttu-id="1f382-131">Documentation du Kit de développement logiciel (SDK) - Notes de publication</span><span class="sxs-lookup"><span data-stu-id="1f382-131">SDK Documentation - Release Notes</span></span>](http://go.microsoft.com/fwlink/?LinkId= 525554) 
* [<span data-ttu-id="1f382-132">Documentation du Kit de développement logiciel - Guides de mise à niveau</span><span class="sxs-lookup"><span data-stu-id="1f382-132">SDK Documentation - Upgrade Guides</span></span>](http://go.microsoft.com/fwlink/?LinkId= 525554)

#### <a name="sdk-other"></a><span data-ttu-id="1f382-133">Kit de développement logiciel (SDK), autres :</span><span class="sxs-lookup"><span data-stu-id="1f382-133">SDK Other</span></span>
* <span data-ttu-id="1f382-134">Erreurs dans le manifeste d’Application « AndroidManifest.xml » peuvent entraîner Azure Mobile Engagement pas toowork (Android uniquement).</span><span class="sxs-lookup"><span data-stu-id="1f382-134">Errors in Application Manifest "AndroidManifest.xml" can cause Azure Mobile Engagement not toowork (Android only).</span></span>
* <span data-ttu-id="1f382-135">Un problème courant avec l’intégration du Kit de développement logiciel et l’utilisation de l’API est tooconfuse hello clé du SDK et hello clé API.</span><span class="sxs-lookup"><span data-stu-id="1f382-135">A common issue with SDK integration and API usage is tooconfuse hello SDK Key and hello API Key.</span></span>

<span data-ttu-id="1f382-136">**Voir aussi :**</span><span class="sxs-lookup"><span data-stu-id="1f382-136">**See also:**</span></span>

* <span data-ttu-id="1f382-137">[Concepts - Glossaire][Link 6]</span><span class="sxs-lookup"><span data-stu-id="1f382-137">[Concepts - Glossary][Link 6]</span></span>

## <a name="advanced-coding-issues"></a><span data-ttu-id="1f382-138">Problèmes de codage avancé</span><span class="sxs-lookup"><span data-stu-id="1f382-138">Advanced coding issues</span></span>
### <a name="issue"></a><span data-ttu-id="1f382-139">Problème</span><span class="sxs-lookup"><span data-stu-id="1f382-139">Issue</span></span>
* <span data-ttu-id="1f382-140">Le code de plate-forme spécifique pas directement liées tooAzure que Mobile Engagement peut entraîner des problèmes sur iOS, Android et Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="1f382-140">Platform specific code not directly related tooAzure Mobile Engagement can cause issues on iOS, Android, and Windows Phone.</span></span>

### <a name="causes"></a><span data-ttu-id="1f382-141">Causes</span><span class="sxs-lookup"><span data-stu-id="1f382-141">Causes</span></span>
* <span data-ttu-id="1f382-142">Nombreux avancée des problèmes de codage avec Azure Mobile Engagement sont provoquées par la plateforme écrite de manière incorrecte un code spécifique pas directement liées tooAzure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="1f382-142">Many advanced coding issues with Azure Mobile Engagement are caused by improperly written platform specific code not directly related tooAzure Mobile Engagement.</span></span> <span data-ttu-id="1f382-143">Vous devez tooconsult documentation spécifique toohello plate-forme de que développement pour de plus documentation de Mobile Engagement tooAzure (Android, iOS, Web, Windows et Windows Phone).</span><span class="sxs-lookup"><span data-stu-id="1f382-143">You will need tooconsult documentation specific toohello platform you are developing for in addition tooAzure Mobile Engagement documentation (Android, iOS, Web, Windows, and Windows Phone).</span></span>
* <span data-ttu-id="1f382-144">Configurez pas correctement les « catégories », empêche la liaison à partir d’un emplacement de tooanother de notification à l’intérieur ou en dehors de l’application hello (Android uniquement).</span><span class="sxs-lookup"><span data-stu-id="1f382-144">Not correctly configuring "categories", prevents linking from a notification tooanother location either inside or outside of hello app (Android only).</span></span> 
* <span data-ttu-id="1f382-145">Vous ne définissez ne pas « UIKit.framework » trop « facultatif » dans votre code iOS, affiche un « Symbole introuvable » ou se bloque sur les anciens appareils iOS (iOS uniquement).</span><span class="sxs-lookup"><span data-stu-id="1f382-145">Not setting "UIKit.framework" too"optional" in your iOS code, shows a "Symbol not found error" and/or crashes on older iOS devices (iOS only).</span></span>
* <span data-ttu-id="1f382-146">Les certificats expirés ou n’est pas correctement à l’aide de hello développement ou la version de production du certificat de hello, push de causes émet (iOS uniquement).</span><span class="sxs-lookup"><span data-stu-id="1f382-146">Expired certificates or not correctly using hello DEV or Prod version of hello cert, causes push issues (iOS only).</span></span>
* <span data-ttu-id="1f382-147">Il existe certains plate-forme limitations inhérentes tooa Azure Mobile Engagement ne peut pas contrôler (par exemple, le fonctionne de centre de système hello pour hors de l’application exécute un push dans Android et iOS).</span><span class="sxs-lookup"><span data-stu-id="1f382-147">There are some limitations inherent tooa platform that Azure Mobile Engagement can't control (like how hello system center works for out of app pushes in Android and iOS).</span></span>
* <span data-ttu-id="1f382-148">Azure Mobile Engagement publie une liste complète des packages de hello interne utilisé par Azure Mobile Engagement pour iOS et Android à titre de référence.</span><span class="sxs-lookup"><span data-stu-id="1f382-148">Azure Mobile Engagement publishes a full list of hello internal packages used by Azure Mobile Engagement for iOS and Android for reference.</span></span> <span data-ttu-id="1f382-149">Gardez à l’esprit que certaines fonctionnalités d’Azure Mobile Engagement sont plateforme toohello spécifique (Android, iOS, Web, Windows et Windows Phone).</span><span class="sxs-lookup"><span data-stu-id="1f382-149">Keep in mind that some features of Azure Mobile Engagement are specific toohello platform (Android, iOS, Web, Windows, and Windows Phone).</span></span>

### <a name="see-also"></a><span data-ttu-id="1f382-150">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="1f382-150">See also</span></span>
* <span data-ttu-id="1f382-151">[Guide de résolution des problèmes - Push][Link 23]</span><span class="sxs-lookup"><span data-stu-id="1f382-151">[Troubleshooting Guide - Push][Link 23]</span></span> 
* <span data-ttu-id="1f382-152">[Documentation du Kit de développement logiciel (SDK) - Notes de publication][Link 5]</span><span class="sxs-lookup"><span data-stu-id="1f382-152">[SDK Documentation - Release Notes][Link 5]</span></span>
* <span data-ttu-id="1f382-153">[Documentation du Kit de développement logiciel (SDK) - Guides de mise à niveau][Link 5]</span><span class="sxs-lookup"><span data-stu-id="1f382-153">[SDK Documentation - Upgrade Guides][Link 5]</span></span>

## <a name="application-crashes"></a><span data-ttu-id="1f382-154">Blocage de l’application</span><span class="sxs-lookup"><span data-stu-id="1f382-154">Application crashes</span></span>
### <a name="issue"></a><span data-ttu-id="1f382-155">Problème</span><span class="sxs-lookup"><span data-stu-id="1f382-155">Issue</span></span>
* <span data-ttu-id="1f382-156">Votre application se bloque sur l’appareil des utilisateurs finaux hello.</span><span class="sxs-lookup"><span data-stu-id="1f382-156">Your application crashes on hello end users' device.</span></span>

### <a name="causes"></a><span data-ttu-id="1f382-157">Causes</span><span class="sxs-lookup"><span data-stu-id="1f382-157">Causes</span></span>
* <span data-ttu-id="1f382-158">Les informations de blocage peuvent être consultées dans hello *Analytique UI* ou hello *Analytique API*</span><span class="sxs-lookup"><span data-stu-id="1f382-158">Crash information can be viewed in hello *Analytics UI* or hello *Analytics API*</span></span>
* <span data-ttu-id="1f382-159">Vous pouvez trouver hello ID de périphérique de votre appareil de test et prendre hello même action qui a provoqué toocrash de votre application pour un utilisateur final de toohelp identifier la cause hello de votre incident.</span><span class="sxs-lookup"><span data-stu-id="1f382-159">You can find hello Device ID of your test device and take hello same action that caused your application toocrash for an end user toohelp identify hello cause of your crash.</span></span>
* <span data-ttu-id="1f382-160">Problèmes connus avec hello Kit de développement logiciel Azure Mobile Engagement qui provoquent des applications toocrash sont parfois résolus en mettant à niveau de la version la plus récente du Kit de développement logiciel de hello toohello.</span><span class="sxs-lookup"><span data-stu-id="1f382-160">Known issues with hello Azure Mobile Engagement SDK that cause applications toocrash are sometimes resolved by upgrading toohello latest version of hello SDK.</span></span> <span data-ttu-id="1f382-161">Assurez-vous que toocheck hello notes de publication sur votre plateforme lorsque vous recherchez des pannes.</span><span class="sxs-lookup"><span data-stu-id="1f382-161">Make sure toocheck hello release notes about your platform when investigating crashes.</span></span>

### <a name="see-also"></a><span data-ttu-id="1f382-162">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="1f382-162">See also</span></span>
* <span data-ttu-id="1f382-163">[Documentation du Kit de développement logiciel (SDK) - Notes de publication][Link 5]</span><span class="sxs-lookup"><span data-stu-id="1f382-163">[SDK Documentation - Release Notes][Link 5]</span></span>
* <span data-ttu-id="1f382-164">[Documentation du Kit de développement logiciel (SDK) - Guides de mise à niveau][Link 5]</span><span class="sxs-lookup"><span data-stu-id="1f382-164">[SDK Documentation - Upgrade Guides][Link 5]</span></span>

## <a name="app-store-upload-failures"></a><span data-ttu-id="1f382-165">Échecs de téléchargement App Store</span><span class="sxs-lookup"><span data-stu-id="1f382-165">App store upload failures</span></span>
### <a name="issue"></a><span data-ttu-id="1f382-166">Problème</span><span class="sxs-lookup"><span data-stu-id="1f382-166">Issue</span></span>
* <span data-ttu-id="1f382-167">Erreurs liées toouploading hello dernière version de votre application tooApple, Google ou magasin de l’application Windows hello.</span><span class="sxs-lookup"><span data-stu-id="1f382-167">Errors related toouploading hello latest version of your app tooApple, Google, or hello Windows App store.</span></span>

### <a name="causes"></a><span data-ttu-id="1f382-168">Causes</span><span class="sxs-lookup"><span data-stu-id="1f382-168">Causes</span></span>
* <span data-ttu-id="1f382-169">Application stocke parfois bloquer des applications avec certaines fonctionnalités activées (par exemple hello Apple Store empêche utilisation hello de IDFV d’applications dans le magasin de hello et magasin de GooglePlay hello hello partage des informations entre les applications de l’application).</span><span class="sxs-lookup"><span data-stu-id="1f382-169">App stores sometimes block apps with certain features enabled (e.g. hello Apple Store prevents hello use of IDFV in apps in hello store and hello GooglePlay store prevents hello sharing of application information between apps).</span></span> 
* <span data-ttu-id="1f382-170">Vérifiez que les notes de publication hello sur votre plateforme et la version actuelle du Kit de développement logiciel de hello si vous avez des difficultés à télécharger un magasin d’applications toohello.</span><span class="sxs-lookup"><span data-stu-id="1f382-170">Make sure that you check hello release notes about your platform and current version of hello SDK if you have difficulty uploading an app toohello store.</span></span>

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

