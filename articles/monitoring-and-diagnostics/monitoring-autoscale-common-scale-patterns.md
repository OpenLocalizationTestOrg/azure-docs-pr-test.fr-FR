---
title: "Vue d’ensemble des modèles courants de mise à l’échelle automatique | Microsoft Docs"
description: "Découvrez certains des modèles courants de mise à l’échelle automatique de vos ressources dans Azure."
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: d37d3fda-8ef1-477c-a360-a855b418de84
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/07/2017
ms.author: ancav
ms.openlocfilehash: fce51546e041c8989d813c3935e058c52b38ba77
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="overview-of-common-autoscale-patterns"></a><span data-ttu-id="43b63-103">Vue d’ensemble des modèles courants de mise à l’échelle automatique</span><span class="sxs-lookup"><span data-stu-id="43b63-103">Overview of common autoscale patterns</span></span>
<span data-ttu-id="43b63-104">Cet article décrit certains des modèles courants de mise à l’échelle de vos ressources dans Azure.</span><span class="sxs-lookup"><span data-stu-id="43b63-104">This article describes some of the common patterns to scale your resource in Azure.</span></span>

<span data-ttu-id="43b63-105">La mise à l’échelle automatique Azure Monitor s’applique uniquement aux jeux de mise à l’échelle de machine virtuelle, services cloud, plans App Service et environnements App Service.</span><span class="sxs-lookup"><span data-stu-id="43b63-105">Azure Monitor auto scale applies only to Virtual Machine Scale Sets (VMSS), cloud services, app service plans and app service environments.</span></span> 

# <a name="lets-get-started"></a><span data-ttu-id="43b63-106">Prise en main</span><span class="sxs-lookup"><span data-stu-id="43b63-106">Lets get started</span></span>

<span data-ttu-id="43b63-107">Cet article suppose que vous êtes familiarisé avec la mise à l’échelle automatique.</span><span class="sxs-lookup"><span data-stu-id="43b63-107">This article assumes that you are familiar with auto scale.</span></span> <span data-ttu-id="43b63-108">Vous pouvez [commencer ici à mettre à l’échelle votre ressource][1].</span><span class="sxs-lookup"><span data-stu-id="43b63-108">You can [get started here to scale your resource][1].</span></span> <span data-ttu-id="43b63-109">Voici quelques modèles de mise à l’échelle courants.</span><span class="sxs-lookup"><span data-stu-id="43b63-109">The following are some of the common scale patterns.</span></span>

## <a name="scale-based-on-cpu"></a><span data-ttu-id="43b63-110">Mise à l’échelle en fonction du processeur</span><span class="sxs-lookup"><span data-stu-id="43b63-110">Scale based on CPU</span></span>

<span data-ttu-id="43b63-111">Vous avez une application web (/VMSS/rôle de service cloud) et</span><span class="sxs-lookup"><span data-stu-id="43b63-111">You have a web app (/VMSS/cloud service role) and</span></span> 

- <span data-ttu-id="43b63-112">Vous souhaitez faire augmenter/diminuer les tailles d’instance sur la base du processeur.</span><span class="sxs-lookup"><span data-stu-id="43b63-112">You want to scale out/scale in based on CPU.</span></span>
- <span data-ttu-id="43b63-113">Vous souhaitez en outre vous assurer qu’il existe un nombre minimal d’instances.</span><span class="sxs-lookup"><span data-stu-id="43b63-113">Additionally, you want to ensure there is a minimum number of instances.</span></span> 
- <span data-ttu-id="43b63-114">Vous souhaitez aussi vous assurer que vous définissez une limite maximale pour le nombre d’instances, vers lequel vous pouvez faire évoluer.</span><span class="sxs-lookup"><span data-stu-id="43b63-114">Also, you want to ensure that you set a maximum limit to the number of instances you can scale to.</span></span>

![Mise à l’échelle en fonction du processeur][2]

## <a name="scale-differently-on-weekdays-vs-weekends"></a><span data-ttu-id="43b63-116">Mettre à l’échelle différemment durant les week-ends et jours de la semaine</span><span class="sxs-lookup"><span data-stu-id="43b63-116">Scale differently on weekdays vs weekends</span></span>

<span data-ttu-id="43b63-117">Vous avez une application web (/VMSS/rôle de service cloud) et</span><span class="sxs-lookup"><span data-stu-id="43b63-117">You have a web app (/VMSS/cloud service role) and</span></span>

- <span data-ttu-id="43b63-118">Vous voulez 3 instances par défaut (pour les jours de la semaine)</span><span class="sxs-lookup"><span data-stu-id="43b63-118">You want 3 instances by default (on weekdays)</span></span>
- <span data-ttu-id="43b63-119">Vous ne prévoyez le trafic lors des week-ends et, par conséquent, vous souhaitez réduire de 1 instance les week-ends.</span><span class="sxs-lookup"><span data-stu-id="43b63-119">You don't expect traffic on weekends and hence you want to scale down to 1 instance on weekends.</span></span>

![Mettre à l’échelle différemment durant les week-ends et jours de la semaine][3]

## <a name="scale-differently-during-holidays"></a><span data-ttu-id="43b63-121">Mettre à l’échelle différemment pendant les jours fériés</span><span class="sxs-lookup"><span data-stu-id="43b63-121">Scale differently during holidays</span></span>

<span data-ttu-id="43b63-122">Vous avez une application web (/VMSS/rôle de service cloud) et</span><span class="sxs-lookup"><span data-stu-id="43b63-122">You have a web app (/VMSS/cloud service role) and</span></span> 

- <span data-ttu-id="43b63-123">Vous souhaitez augmenter/diminuer la taille des instances en fonction de l’utilisation du processeur par défaut</span><span class="sxs-lookup"><span data-stu-id="43b63-123">You want to scale up/down based on CPU usage by default</span></span>
- <span data-ttu-id="43b63-124">Toutefois, pendant les vacances (ou des jours spécifiques qui sont importants pour votre entreprise), vous souhaitez remplacer les valeurs par défaut et avoir plus de capacité à votre disposition.</span><span class="sxs-lookup"><span data-stu-id="43b63-124">However, during holiday season (or specific days that are important for your business) you want to override the defaults and have more capacity at your disposal.</span></span>

![Mettre à l’échelle différemment lors des jours fériés][4]

## <a name="scale-based-on-custom-metric"></a><span data-ttu-id="43b63-126">Mise à l’échelle en fonction de métriques personnalisées</span><span class="sxs-lookup"><span data-stu-id="43b63-126">Scale based on custom metric</span></span>

<span data-ttu-id="43b63-127">Vous avez un site web frontal et un niveau d’API qui communique avec le serveur principal.</span><span class="sxs-lookup"><span data-stu-id="43b63-127">You have a web front end and a API tier that communicates with the backend.</span></span> 

- <span data-ttu-id="43b63-128">Vous souhaitez mettre à l’échelle le niveau API sur la base d’événements personnalisés sur le serveur frontal (exemple : vous souhaitez mettre à l’échelle de votre processus de validation en fonction du nombre d’éléments dans le panier d’achat)</span><span class="sxs-lookup"><span data-stu-id="43b63-128">You want to scale the API tier based on custom events in the front end (example: You want to scale your checkout process based on the number of items in the shopping cart)</span></span>

![Mise à l’échelle en fonction de métriques personnalisées][5]

<!--Reference-->
[1]: ./monitoring-autoscale-get-started.md
[2]: ./media/monitoring-autoscale-common-scale-patterns/scale-based-on-cpu.png
[3]: ./media/monitoring-autoscale-common-scale-patterns/weekday-weekend-scale.png
[4]: ./media/monitoring-autoscale-common-scale-patterns/holidays-scale.png
[5]: ./media/monitoring-autoscale-common-scale-patterns/custom-metric-scale.png