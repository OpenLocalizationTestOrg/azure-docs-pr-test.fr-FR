---
title: aaaAzure Mobile Engagement iOS Notes de publication SDK | Documents Microsoft
description: "Dernières mises à jour et procédures du Kit de développement logiciel (SDK) iOS pour Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: a43ff0f6-90d5-4b3c-8d7a-a1db21bc776b
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 07/17/2017
ms.author: piyushjo
ms.openlocfilehash: ae29d200ebb1784357b29edbd1f66b71df0778cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-mobile-engagement-ios-sdk-release-notes"></a><span data-ttu-id="b8702-103">Notes de publication du Kit de développement logiciel (SDK) Azure Mobile Engagement pour iOS</span><span class="sxs-lookup"><span data-stu-id="b8702-103">Azure Mobile Engagement iOS SDK release notes</span></span>

## <a name="410-07172017"></a><span data-ttu-id="b8702-104">4.1.0 (07/17/2017)</span><span class="sxs-lookup"><span data-stu-id="b8702-104">4.1.0 (07/17/2017)</span></span>
* <span data-ttu-id="b8702-105">Correction des badges effacés en arrière-plan.</span><span class="sxs-lookup"><span data-stu-id="b8702-105">Fixed badges cleared in background.</span></span>
* <span data-ttu-id="b8702-106">Correction des avertissements sur XCode 9 à propos des API qui ne sont pas appelées dans la file d’attente principale.</span><span class="sxs-lookup"><span data-stu-id="b8702-106">Fixed warnings on XCode 9 about APIs not called in main queue.</span></span>
* <span data-ttu-id="b8702-107">Correction d’une fuite de mémoire dans les sondages Reach.</span><span class="sxs-lookup"><span data-stu-id="b8702-107">Fixed a memory leak in Reach polls.</span></span>
* <span data-ttu-id="b8702-108">Fin de la prise en charge d’iOS 6.X.</span><span class="sxs-lookup"><span data-stu-id="b8702-108">Dropped support for iOS 6.X.</span></span> <span data-ttu-id="b8702-109">À partir de cette cible de déploiement hello version de votre application doit être au moins iOS 7.</span><span class="sxs-lookup"><span data-stu-id="b8702-109">Starting from this version hello deployment target of your application must be at least iOS 7.</span></span>

## <a name="401-12132016"></a><span data-ttu-id="b8702-110">4.0.1 (13/12/2016)</span><span class="sxs-lookup"><span data-stu-id="b8702-110">4.0.1 (12/13/2016)</span></span>
* <span data-ttu-id="b8702-111">Amélioration de la remise de journaux en arrière-plan.</span><span class="sxs-lookup"><span data-stu-id="b8702-111">Improved log delivery in background.</span></span>

## <a name="400-09122016"></a><span data-ttu-id="b8702-112">4.0.0 (09/12/2016)</span><span class="sxs-lookup"><span data-stu-id="b8702-112">4.0.0 (09/12/2016)</span></span>
* <span data-ttu-id="b8702-113">Résolution de la notification non affichée sur les appareils iOS 10.</span><span class="sxs-lookup"><span data-stu-id="b8702-113">Fixed notification not actioned on iOS 10 devices.</span></span>
* <span data-ttu-id="b8702-114">Utilisation de XCode 7 déconseillée.</span><span class="sxs-lookup"><span data-stu-id="b8702-114">Deprecate XCode 7.</span></span>

## <a name="324-06302016"></a><span data-ttu-id="b8702-115">3.2.4 (30/06/2016)</span><span class="sxs-lookup"><span data-stu-id="b8702-115">3.2.4 (06/30/2016)</span></span>
* <span data-ttu-id="b8702-116">Agrégation fixe entre les journaux techniques et les autres journaux.</span><span class="sxs-lookup"><span data-stu-id="b8702-116">Fixed aggregation between technical logs and other logs.</span></span>

## <a name="323-06072016"></a><span data-ttu-id="b8702-117">3.2.3 (07/06/2016)</span><span class="sxs-lookup"><span data-stu-id="b8702-117">3.2.3 (06/07/2016)</span></span>
* <span data-ttu-id="b8702-118">Bogue hello fixe dans lequel les commentaires de remise ne sont pas signalée lors de l’application est dans l’arrière-plan de hello.</span><span class="sxs-lookup"><span data-stu-id="b8702-118">Fixed hello bug where delivery feedback is not reported when app is in hello background.</span></span>
* <span data-ttu-id="b8702-119">Hello optimisé envoi de journaux techniques.</span><span class="sxs-lookup"><span data-stu-id="b8702-119">Optimized hello sending of technical logs.</span></span>

## <a name="322-04072016"></a><span data-ttu-id="b8702-120">3.2.2 (04/07/2016)</span><span class="sxs-lookup"><span data-stu-id="b8702-120">3.2.2 (04/07/2016)</span></span>
* <span data-ttu-id="b8702-121">Bogue d’annulation de demande HTTP conduisant parfois toocrash.</span><span class="sxs-lookup"><span data-stu-id="b8702-121">Fixed bug on HTTP request cancellation which sometimes leads toocrash.</span></span>

## <a name="321-12112015"></a><span data-ttu-id="b8702-122">3.2.1 (12/11/2015)</span><span class="sxs-lookup"><span data-stu-id="b8702-122">3.2.1 (12/11/2015)</span></span>
* <span data-ttu-id="b8702-123">Délai fixe hello lorsqu’une nouvelle instance de l’application est déclenchée par une notification avec des liens profonds</span><span class="sxs-lookup"><span data-stu-id="b8702-123">Fixed hello delay when a new app instance is triggered by a notification with deep links</span></span>

## <a name="320-10082015"></a><span data-ttu-id="b8702-124">3.2.0 (10/08/2015)</span><span class="sxs-lookup"><span data-stu-id="b8702-124">3.2.0 (10/08/2015)</span></span>
* <span data-ttu-id="b8702-125">Activé Bitcode dans toomake du Kit de développement logiciel hello elle fonctionne avec **Xcode 7**.</span><span class="sxs-lookup"><span data-stu-id="b8702-125">Enabled Bitcode in hello SDK toomake it work with **Xcode 7**.</span></span>
* <span data-ttu-id="b8702-126">Bogues résolus relatives des notifications de l’application de tooin.</span><span class="sxs-lookup"><span data-stu-id="b8702-126">Fixed bugs related tooin-app notifications.</span></span>
* <span data-ttu-id="b8702-127">Rendu les notifications dans l’application hello plus fiable en cas de batterie faible et d’autres cas de figure.</span><span class="sxs-lookup"><span data-stu-id="b8702-127">Made hello in-app notifications more reliable in case of low battery and other such scenarios.</span></span>
* <span data-ttu-id="b8702-128">Suppression des journaux de console supplémentaires générés par la bibliothèque tierce.</span><span class="sxs-lookup"><span data-stu-id="b8702-128">Removed extra console logs generated by 3rd party library.</span></span>

## <a name="310-08262015"></a><span data-ttu-id="b8702-129">3.1.0 (26/08/2015)</span><span class="sxs-lookup"><span data-stu-id="b8702-129">3.1.0 (08/26/2015)</span></span>
* <span data-ttu-id="b8702-130">Résolution d’un bogue de compatibilité iOS 9 avec une bibliothèque tierce.</span><span class="sxs-lookup"><span data-stu-id="b8702-130">Fix iOS 9 compatibility bug with a third party library.</span></span> <span data-ttu-id="b8702-131">Ce bogue provoquait des blocages pendant l’envoi des résultats des sondages, d’informations sur l’application ou de données supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="b8702-131">It was causing crashes while sending polls results, application information or extra data.</span></span>

## <a name="300-06192015"></a><span data-ttu-id="b8702-132">3.0.0 (19/06/2015)</span><span class="sxs-lookup"><span data-stu-id="b8702-132">3.0.0 (06/19/2015)</span></span>
* <span data-ttu-id="b8702-133">Mobile Engagement utilise des notifications Push Silent.</span><span class="sxs-lookup"><span data-stu-id="b8702-133">Mobile Engagement uses Silent Push Notifications.</span></span>
* <span data-ttu-id="b8702-134">Prise en charge d’iOS 4.X abandonnée.</span><span class="sxs-lookup"><span data-stu-id="b8702-134">Dropped support for iOS 4.X.</span></span> <span data-ttu-id="b8702-135">À partir de cette cible de déploiement hello version de votre application doit être au moins iOS 6.</span><span class="sxs-lookup"><span data-stu-id="b8702-135">Starting from this version hello deployment target of your application must be at least iOS 6.</span></span>

## <a name="220-05212015"></a><span data-ttu-id="b8702-136">2.2.0 (21/05/2015)</span><span class="sxs-lookup"><span data-stu-id="b8702-136">2.2.0 (05/21/2015)</span></span>
* <span data-ttu-id="b8702-137">id de périphérique Mobile Engagement Hello pour les appareils < iOS 6 est désormais basée sur un GUID généré au moment de l’installation.</span><span class="sxs-lookup"><span data-stu-id="b8702-137">hello Mobile Engagement device id for devices < iOS 6 is now based on a GUID generated at installation time.</span></span>

## <a name="210-04242015"></a><span data-ttu-id="b8702-138">2.1.0 (24/04/2015)</span><span class="sxs-lookup"><span data-stu-id="b8702-138">2.1.0 (04/24/2015)</span></span>
* <span data-ttu-id="b8702-139">Compatibilité Swift ajoutée.</span><span class="sxs-lookup"><span data-stu-id="b8702-139">Added Swift compatibility.</span></span>
* <span data-ttu-id="b8702-140">Lorsque vous cliquez sur une notification, action hello QU'URL est désormais exécutée droite après que l’application hello est ouvert.</span><span class="sxs-lookup"><span data-stu-id="b8702-140">When clicking on a notification, hello action URL is now executed right after hello application is opened.</span></span>
* <span data-ttu-id="b8702-141">Ajout du fichier d'en-tête manquant dans le package du Kit de développement logiciel (SDK).</span><span class="sxs-lookup"><span data-stu-id="b8702-141">Added missing header file in SDK package.</span></span>
* <span data-ttu-id="b8702-142">Correction d’un problème lors de la reporter d’incident hello Mobile Engagement a été désactivée.</span><span class="sxs-lookup"><span data-stu-id="b8702-142">Fixed an issue when hello Mobile Engagement crash reporter was disabled.</span></span>

## <a name="200-02172015"></a><span data-ttu-id="b8702-143">2.0.0 (17/02/2015)</span><span class="sxs-lookup"><span data-stu-id="b8702-143">2.0.0 (02/17/2015)</span></span>
* <span data-ttu-id="b8702-144">Version initiale d'Azure Engagement Mobile</span><span class="sxs-lookup"><span data-stu-id="b8702-144">Initial Release of Azure Mobile Engagement</span></span>
* <span data-ttu-id="b8702-145">La configuration d'appId/sdkKey est remplacée par une configuration de chaîne de connexion.</span><span class="sxs-lookup"><span data-stu-id="b8702-145">appId/sdkKey configuration is replaced by a connection string configuration.</span></span>
* <span data-ttu-id="b8702-146">Supprimé API toosend et recevoir des messages XMPP arbitraires à partir des entités XMPP arbitraires.</span><span class="sxs-lookup"><span data-stu-id="b8702-146">Removed API toosend and receive arbitrary XMPP messages from arbitrary XMPP entities.</span></span>
* <span data-ttu-id="b8702-147">Supprimé toosend d’API et de recevoir des messages entre les appareils.</span><span class="sxs-lookup"><span data-stu-id="b8702-147">Removed API toosend and receive messages between devices.</span></span>
* <span data-ttu-id="b8702-148">Améliorations de sécurité.</span><span class="sxs-lookup"><span data-stu-id="b8702-148">Security improvements.</span></span>
* <span data-ttu-id="b8702-149">Suppression du suivi SmartAd.</span><span class="sxs-lookup"><span data-stu-id="b8702-149">SmartAd tracking removed.</span></span>
