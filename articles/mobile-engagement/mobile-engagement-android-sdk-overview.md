---
title: "Intégration du SDK Android pour Azure Mobile Engagement"
description: "Décrit comment intégrer le SDK Azure Mobile Engagement dans les applications Android"
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
ms.openlocfilehash: 35935e911f1f17989beb71978396c6d1b7d601d6
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="android-sdk-integration-for-azure-mobile-engagement"></a><span data-ttu-id="fab2d-103">Intégration du SDK Android pour Azure Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="fab2d-103">Android SDK Integration for Azure Mobile Engagement</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="fab2d-104">Windows universel</span><span class="sxs-lookup"><span data-stu-id="fab2d-104">Universal Windows</span></span>](mobile-engagement-windows-store-sdk-overview.md)
> * [<span data-ttu-id="fab2d-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="fab2d-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-sdk-overview.md)
> * [<span data-ttu-id="fab2d-106">iOS</span><span class="sxs-lookup"><span data-stu-id="fab2d-106">iOS</span></span>](mobile-engagement-ios-sdk-overview.md)
> * [<span data-ttu-id="fab2d-107">Android</span><span class="sxs-lookup"><span data-stu-id="fab2d-107">Android</span></span>](mobile-engagement-android-sdk-overview.md)
> 
> 

<span data-ttu-id="fab2d-108">Ce document décrit toutes les options d’intégration et de configuration disponibles pour le SDK Azure Mobile Engagement pour Android.</span><span class="sxs-lookup"><span data-stu-id="fab2d-108">This document describes all the integration and configuration options available for Azure Mobile Engagement Android SDK.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fab2d-109">Composants requis</span><span class="sxs-lookup"><span data-stu-id="fab2d-109">Prerequisites</span></span>
[!INCLUDE [Prereqs](../../includes/mobile-engagement-android-prereqs.md)]

## <a name="advanced-features"></a><span data-ttu-id="fab2d-110">Fonctionnalités avancées</span><span class="sxs-lookup"><span data-stu-id="fab2d-110">Advanced Features</span></span>
### <a name="reporting-features"></a><span data-ttu-id="fab2d-111">Fonctionnalités de génération de rapports</span><span class="sxs-lookup"><span data-stu-id="fab2d-111">Reporting Features</span></span>
<span data-ttu-id="fab2d-112">Vous pouvez ajouter les fonctionnalités suivantes :</span><span class="sxs-lookup"><span data-stu-id="fab2d-112">You can add these features:</span></span>

1. [<span data-ttu-id="fab2d-113">Options de génération de rapports avancés</span><span class="sxs-lookup"><span data-stu-id="fab2d-113">Advanced reporting options</span></span>](mobile-engagement-android-advanced-reporting.md)
2. [<span data-ttu-id="fab2d-114">Options de génération de rapports d’emplacement</span><span class="sxs-lookup"><span data-stu-id="fab2d-114">Location Reporting options</span></span>](mobile-engagement-android-location-reporting.md)
3. [<span data-ttu-id="fab2d-115">Options de configuration avancées</span><span class="sxs-lookup"><span data-stu-id="fab2d-115">Advanced Configuration options</span></span>](mobile-engagement-android-advanced-configuration.md)

### <a name="notifications"></a><span data-ttu-id="fab2d-116">Notifications :</span><span class="sxs-lookup"><span data-stu-id="fab2d-116">Notifications:</span></span>
[<span data-ttu-id="fab2d-117">comment intégrer le module Couverture (notifications) à votre application Android</span><span class="sxs-lookup"><span data-stu-id="fab2d-117">How to integrate Reach (Notifications) in your Android app</span></span>](mobile-engagement-android-integrate-engagement-reach.md)

1. <span data-ttu-id="fab2d-118">Google Cloud Messaging (GCM) : [comment intégrer GCM à Mobile Engagement](mobile-engagement-android-gcm-integrate.md)</span><span class="sxs-lookup"><span data-stu-id="fab2d-118">Google Cloud Messaging (GCM): [How to Integrate GCM with Mobile Engagement](mobile-engagement-android-gcm-integrate.md)</span></span>
2. <span data-ttu-id="fab2d-119">Amazon Device Messaging (ADM) : [comment intégrer ADM à Mobile Engagement](mobile-engagement-android-adm-integrate.md)</span><span class="sxs-lookup"><span data-stu-id="fab2d-119">Amazon Device Messaging (ADM): [How to Integrate ADM with Mobile Engagement](mobile-engagement-android-adm-integrate.md)</span></span>

### <a name="tag-plan-implementation"></a><span data-ttu-id="fab2d-120">Implémentation du plan de balise :</span><span class="sxs-lookup"><span data-stu-id="fab2d-120">Tag plan implementation:</span></span>
[<span data-ttu-id="fab2d-121">comment utiliser l'API de balisage avancée de Mobile Engagement dans votre application Android</span><span class="sxs-lookup"><span data-stu-id="fab2d-121">How to use the advanced Mobile Engagement tagging API in your Android app</span></span>](mobile-engagement-android-use-engagement-api.md)

## <a name="release-notes"></a><span data-ttu-id="fab2d-122">Notes de publication</span><span class="sxs-lookup"><span data-stu-id="fab2d-122">Release notes</span></span>

### <a name="431-07172017"></a><span data-ttu-id="fab2d-123">4.3.1 (07/17/2017)</span><span class="sxs-lookup"><span data-stu-id="fab2d-123">4.3.1 (07/17/2017)</span></span>
* <span data-ttu-id="fab2d-124">Résolution d’un incident rare lors de l’appel de `EngagementAgentUtils.isInDedicatedEngagementProcess`, également utilisée par la classe `EngagementApplication`.</span><span class="sxs-lookup"><span data-stu-id="fab2d-124">Fix a crash that could rarely happen when calling `EngagementAgentUtils.isInDedicatedEngagementProcess`, which is also used by the `EngagementApplication` class.</span></span>

### <a name="430-06272017"></a><span data-ttu-id="fab2d-125">4.3.0 (06/27/2017)</span><span class="sxs-lookup"><span data-stu-id="fab2d-125">4.3.0 (06/27/2017)</span></span>
* <span data-ttu-id="fab2d-126">Prise en charge Android 8 (les versions précédentes du Kit de développement logiciel ne fonctionnent pas sur Android 8).</span><span class="sxs-lookup"><span data-stu-id="fab2d-126">Android 8 support (previous versions of the SDK will not work on Android 8).</span></span>
* <span data-ttu-id="fab2d-127">Aucune autre dépendance sur la bibliothèque de prise en charge.</span><span class="sxs-lookup"><span data-stu-id="fab2d-127">No more dependency on support library.</span></span>
* <span data-ttu-id="fab2d-128">Supprimez la classe `EngagementFragmentActivity`.</span><span class="sxs-lookup"><span data-stu-id="fab2d-128">Remove `EngagementFragmentActivity` class.</span></span>
* <span data-ttu-id="fab2d-129">En raison des [limites d’exécution en arrière-plan](https://developer.android.com/preview/features/background.html) sur Android 8, les journaux en arrière-plan peuvent être retardés jusqu’à ce que l’utilisateur interagisse avec l’appareil. Cela entraîne un retard des statistiques **Remis** et **Notification système (affichée dans la barre de notification)** de la campagne push si l’appareil est en veille (la notification sera toujours affichée, sonnera et vibrera en temps réel sans problème).</span><span class="sxs-lookup"><span data-stu-id="fab2d-129">Due to [Background Execution Limits](https://developer.android.com/preview/features/background.html) on Android 8, logs in background might be delayed until the user interacts with the device, this will have an impact on Push Campaign **Delivered** and **System notification displayed** statistics being delayed if the device was sleeping (the notification will still be displayed, will ring and vibrate in real time without issues).</span></span>
* <span data-ttu-id="fab2d-130">En raison des [limites d’exécution en arrière-plan](https://developer.android.com/preview/features/background-location-limits.html), l’emplacement en arrière-plan en temps réel ne sera pas fréquemment mis à jour sur Android 8.</span><span class="sxs-lookup"><span data-stu-id="fab2d-130">Due to [Background Location Limits](https://developer.android.com/preview/features/background-location-limits.html), the real time location in background will not be updated frequently on Android 8.</span></span>

<span data-ttu-id="fab2d-131">Pour toutes les versions, consultez les [notes de publication complètes](mobile-engagement-android-release-notes.md).</span><span class="sxs-lookup"><span data-stu-id="fab2d-131">For all versions, see the [complete release notes](mobile-engagement-android-release-notes.md).</span></span>

## <a name="upgrade-procedures"></a><span data-ttu-id="fab2d-132">Procédures de mise à niveau</span><span class="sxs-lookup"><span data-stu-id="fab2d-132">Upgrade procedures</span></span>
<span data-ttu-id="fab2d-133">Si vous avez déjà intégré une version plus ancienne de notre kit de développement logiciel (SDK) dans votre application, consultez [Procédures de mise à niveau](mobile-engagement-android-upgrade-procedure.md).</span><span class="sxs-lookup"><span data-stu-id="fab2d-133">If you already have integrated an older version of our SDK into your application, consult [Upgrade Procedures](mobile-engagement-android-upgrade-procedure.md).</span></span>

