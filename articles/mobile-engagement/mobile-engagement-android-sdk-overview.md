---
title: "aaaAndroid intégration du Kit de développement logiciel pour Azure Mobile Engagement"
description: "Décrit comment toointegrate Kit de développement logiciel Azure Mobile Engagement dans des applications Android"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: a91ed04f-f3ce-4692-a6dd-b56a28d7dee8
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 07/17/2017
ms.author: piyushjo;ricksal
ms.openlocfilehash: 0c63bfaf673abbda7ea498390f8282c43e2fb8df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="android-sdk-integration-for-azure-mobile-engagement"></a><span data-ttu-id="41561-103">Intégration du SDK Android pour Azure Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="41561-103">Android SDK Integration for Azure Mobile Engagement</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="41561-104">Windows universel</span><span class="sxs-lookup"><span data-stu-id="41561-104">Universal Windows</span></span>](mobile-engagement-windows-store-sdk-overview.md)
> * [<span data-ttu-id="41561-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="41561-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-sdk-overview.md)
> * [<span data-ttu-id="41561-106">iOS</span><span class="sxs-lookup"><span data-stu-id="41561-106">iOS</span></span>](mobile-engagement-ios-sdk-overview.md)
> * [<span data-ttu-id="41561-107">Android</span><span class="sxs-lookup"><span data-stu-id="41561-107">Android</span></span>](mobile-engagement-android-sdk-overview.md)
> 
> 

<span data-ttu-id="41561-108">Ce document décrit tous les hello intégration et configuration options disponibles pour Azure Mobile Engagement Android SDK.</span><span class="sxs-lookup"><span data-stu-id="41561-108">This document describes all hello integration and configuration options available for Azure Mobile Engagement Android SDK.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="41561-109">Composants requis</span><span class="sxs-lookup"><span data-stu-id="41561-109">Prerequisites</span></span>
[!INCLUDE [Prereqs](../../includes/mobile-engagement-android-prereqs.md)]

## <a name="advanced-features"></a><span data-ttu-id="41561-110">Fonctionnalités avancées</span><span class="sxs-lookup"><span data-stu-id="41561-110">Advanced Features</span></span>
### <a name="reporting-features"></a><span data-ttu-id="41561-111">Fonctionnalités de génération de rapports</span><span class="sxs-lookup"><span data-stu-id="41561-111">Reporting Features</span></span>
<span data-ttu-id="41561-112">Vous pouvez ajouter les fonctionnalités suivantes :</span><span class="sxs-lookup"><span data-stu-id="41561-112">You can add these features:</span></span>

1. [<span data-ttu-id="41561-113">Options de génération de rapports avancés</span><span class="sxs-lookup"><span data-stu-id="41561-113">Advanced reporting options</span></span>](mobile-engagement-android-advanced-reporting.md)
2. [<span data-ttu-id="41561-114">Options de génération de rapports d’emplacement</span><span class="sxs-lookup"><span data-stu-id="41561-114">Location Reporting options</span></span>](mobile-engagement-android-location-reporting.md)
3. [<span data-ttu-id="41561-115">Options de configuration avancées</span><span class="sxs-lookup"><span data-stu-id="41561-115">Advanced Configuration options</span></span>](mobile-engagement-android-advanced-configuration.md)

### <a name="notifications"></a><span data-ttu-id="41561-116">Notifications :</span><span class="sxs-lookup"><span data-stu-id="41561-116">Notifications:</span></span>
[<span data-ttu-id="41561-117">Comment toointegrate portée (Notifications) dans votre application Android</span><span class="sxs-lookup"><span data-stu-id="41561-117">How toointegrate Reach (Notifications) in your Android app</span></span>](mobile-engagement-android-integrate-engagement-reach.md)

1. <span data-ttu-id="41561-118">Google Cloud Messaging (GCM) : [comment tooIntegrate GCM avec Mobile Engagement](mobile-engagement-android-gcm-integrate.md)</span><span class="sxs-lookup"><span data-stu-id="41561-118">Google Cloud Messaging (GCM): [How tooIntegrate GCM with Mobile Engagement](mobile-engagement-android-gcm-integrate.md)</span></span>
2. <span data-ttu-id="41561-119">Messagerie d’appareil Amazon (ADM) : [comment tooIntegrate ADM avec Mobile Engagement](mobile-engagement-android-adm-integrate.md)</span><span class="sxs-lookup"><span data-stu-id="41561-119">Amazon Device Messaging (ADM): [How tooIntegrate ADM with Mobile Engagement](mobile-engagement-android-adm-integrate.md)</span></span>

### <a name="tag-plan-implementation"></a><span data-ttu-id="41561-120">Implémentation du plan de balise :</span><span class="sxs-lookup"><span data-stu-id="41561-120">Tag plan implementation:</span></span>
[<span data-ttu-id="41561-121">Comment toouse hello avancé Mobile Engagement marquage API dans votre application Android</span><span class="sxs-lookup"><span data-stu-id="41561-121">How toouse hello advanced Mobile Engagement tagging API in your Android app</span></span>](mobile-engagement-android-use-engagement-api.md)

## <a name="release-notes"></a><span data-ttu-id="41561-122">Notes de publication</span><span class="sxs-lookup"><span data-stu-id="41561-122">Release notes</span></span>

### <a name="431-07172017"></a><span data-ttu-id="41561-123">4.3.1 (07/17/2017)</span><span class="sxs-lookup"><span data-stu-id="41561-123">4.3.1 (07/17/2017)</span></span>
* <span data-ttu-id="41561-124">Résoudre un incident peut se produire rarement lors de l’appel `EngagementAgentUtils.isInDedicatedEngagementProcess`, qui est également utilisé par hello `EngagementApplication` classe.</span><span class="sxs-lookup"><span data-stu-id="41561-124">Fix a crash that could rarely happen when calling `EngagementAgentUtils.isInDedicatedEngagementProcess`, which is also used by hello `EngagementApplication` class.</span></span>

### <a name="430-06272017"></a><span data-ttu-id="41561-125">4.3.0 (06/27/2017)</span><span class="sxs-lookup"><span data-stu-id="41561-125">4.3.0 (06/27/2017)</span></span>
* <span data-ttu-id="41561-126">Android 8 prise en charge (versions précédentes de hello SDK ne fonctionnera pas sur Android 8).</span><span class="sxs-lookup"><span data-stu-id="41561-126">Android 8 support (previous versions of hello SDK will not work on Android 8).</span></span>
* <span data-ttu-id="41561-127">Aucune autre dépendance sur la bibliothèque de prise en charge.</span><span class="sxs-lookup"><span data-stu-id="41561-127">No more dependency on support library.</span></span>
* <span data-ttu-id="41561-128">Supprimez la classe `EngagementFragmentActivity`.</span><span class="sxs-lookup"><span data-stu-id="41561-128">Remove `EngagementFragmentActivity` class.</span></span>
* <span data-ttu-id="41561-129">Échéance trop[limites de l’exécution en arrière-plan](https://developer.android.com/preview/features/background.html) sur 8 Android, les journaux en arrière-plan peuvent être retardées jusqu'à ce que l’utilisateur de hello interagit avec les appareils hello, cela aura un impact sur les campagnes de Push **remis** et **Notification système affichée** statistiques retardées si l’appareil de hello était en état de veille (hello notification restent affichée, est en anneau et faire vibrer en temps réel sans problème).</span><span class="sxs-lookup"><span data-stu-id="41561-129">Due too[Background Execution Limits](https://developer.android.com/preview/features/background.html) on Android 8, logs in background might be delayed until hello user interacts with hello device, this will have an impact on Push Campaign **Delivered** and **System notification displayed** statistics being delayed if hello device was sleeping (hello notification will still be displayed, will ring and vibrate in real time without issues).</span></span>
* <span data-ttu-id="41561-130">Échéance trop[arrière-plan emplacement limites](https://developer.android.com/preview/features/background-location-limits.html), emplacement en temps réel de hello en arrière-plan se verra pas fréquemment sur 8 Android.</span><span class="sxs-lookup"><span data-stu-id="41561-130">Due too[Background Location Limits](https://developer.android.com/preview/features/background-location-limits.html), hello real time location in background will not be updated frequently on Android 8.</span></span>

<span data-ttu-id="41561-131">Pour toutes les versions, consultez hello [terminer les notes de publication](mobile-engagement-android-release-notes.md).</span><span class="sxs-lookup"><span data-stu-id="41561-131">For all versions, see hello [complete release notes](mobile-engagement-android-release-notes.md).</span></span>

## <a name="upgrade-procedures"></a><span data-ttu-id="41561-132">Procédures de mise à niveau</span><span class="sxs-lookup"><span data-stu-id="41561-132">Upgrade procedures</span></span>
<span data-ttu-id="41561-133">Si vous avez déjà intégré une version plus ancienne de notre kit de développement logiciel (SDK) dans votre application, consultez [Procédures de mise à niveau](mobile-engagement-android-upgrade-procedure.md).</span><span class="sxs-lookup"><span data-stu-id="41561-133">If you already have integrated an older version of our SDK into your application, consult [Upgrade Procedures](mobile-engagement-android-upgrade-procedure.md).</span></span>

