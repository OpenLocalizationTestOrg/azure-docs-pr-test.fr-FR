---
title: "aaaOverview des modèles de mise à l’échelle courants | Documents Microsoft"
description: "Découvrez que certaines hello courantes modèles tooauto l’échelle vos ressources dans Azure."
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
ms.openlocfilehash: fc5bd97852e0af01aa32940c99721ab8e21033ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-common-autoscale-patterns"></a><span data-ttu-id="17566-103">Vue d’ensemble des modèles courants de mise à l’échelle automatique</span><span class="sxs-lookup"><span data-stu-id="17566-103">Overview of common autoscale patterns</span></span>
<span data-ttu-id="17566-104">Cet article décrit certaines des hello courantes modèles tooscale vos ressources dans Azure.</span><span class="sxs-lookup"><span data-stu-id="17566-104">This article describes some of hello common patterns tooscale your resource in Azure.</span></span>

<span data-ttu-id="17566-105">Azure à l’échelle automatique analyse s’applique uniquement tooVirtual jeux de mise à l’échelle de Machine (mise), services de cloud computing, les plans de service d’application et les environnements app service.</span><span class="sxs-lookup"><span data-stu-id="17566-105">Azure Monitor auto scale applies only tooVirtual Machine Scale Sets (VMSS), cloud services, app service plans and app service environments.</span></span> 

# <a name="lets-get-started"></a><span data-ttu-id="17566-106">Prise en main</span><span class="sxs-lookup"><span data-stu-id="17566-106">Lets get started</span></span>

<span data-ttu-id="17566-107">Cet article suppose que vous êtes familiarisé avec la mise à l’échelle automatique.</span><span class="sxs-lookup"><span data-stu-id="17566-107">This article assumes that you are familiar with auto scale.</span></span> <span data-ttu-id="17566-108">Vous pouvez [obtenir tooscale ici démarré votre ressource][1].</span><span class="sxs-lookup"><span data-stu-id="17566-108">You can [get started here tooscale your resource][1].</span></span> <span data-ttu-id="17566-109">Hello Voici quelques-uns des modèles de mise à l’échelle hello courants.</span><span class="sxs-lookup"><span data-stu-id="17566-109">hello following are some of hello common scale patterns.</span></span>

## <a name="scale-based-on-cpu"></a><span data-ttu-id="17566-110">Mise à l’échelle en fonction du processeur</span><span class="sxs-lookup"><span data-stu-id="17566-110">Scale based on CPU</span></span>

<span data-ttu-id="17566-111">Vous avez une application web (/VMSS/rôle de service cloud) et</span><span class="sxs-lookup"><span data-stu-id="17566-111">You have a web app (/VMSS/cloud service role) and</span></span> 

- <span data-ttu-id="17566-112">Vous souhaitez tooscale hors/mise à l’échelle en fonction de processeur.</span><span class="sxs-lookup"><span data-stu-id="17566-112">You want tooscale out/scale in based on CPU.</span></span>
- <span data-ttu-id="17566-113">En outre, vous souhaitez que tooensure est un nombre minimal d’instances.</span><span class="sxs-lookup"><span data-stu-id="17566-113">Additionally, you want tooensure there is a minimum number of instances.</span></span> 
- <span data-ttu-id="17566-114">En outre, vous souhaitez tooensure que vous définissez un nombre de toohello le nombre maximal d’instances, à que vous pouvez faire évoluer.</span><span class="sxs-lookup"><span data-stu-id="17566-114">Also, you want tooensure that you set a maximum limit toohello number of instances you can scale to.</span></span>

![Mise à l’échelle en fonction du processeur][2]

## <a name="scale-differently-on-weekdays-vs-weekends"></a><span data-ttu-id="17566-116">Mettre à l’échelle différemment durant les week-ends et jours de la semaine</span><span class="sxs-lookup"><span data-stu-id="17566-116">Scale differently on weekdays vs weekends</span></span>

<span data-ttu-id="17566-117">Vous avez une application web (/VMSS/rôle de service cloud) et</span><span class="sxs-lookup"><span data-stu-id="17566-117">You have a web app (/VMSS/cloud service role) and</span></span>

- <span data-ttu-id="17566-118">Vous voulez 3 instances par défaut (pour les jours de la semaine)</span><span class="sxs-lookup"><span data-stu-id="17566-118">You want 3 instances by default (on weekdays)</span></span>
- <span data-ttu-id="17566-119">Vous ne prévoyez pas le trafic sur les week-ends, et par conséquent, vous souhaitez tooscale too1 instance vers le bas sur les week-ends.</span><span class="sxs-lookup"><span data-stu-id="17566-119">You don't expect traffic on weekends and hence you want tooscale down too1 instance on weekends.</span></span>

![Mettre à l’échelle différemment durant les week-ends et jours de la semaine][3]

## <a name="scale-differently-during-holidays"></a><span data-ttu-id="17566-121">Mettre à l’échelle différemment pendant les jours fériés</span><span class="sxs-lookup"><span data-stu-id="17566-121">Scale differently during holidays</span></span>

<span data-ttu-id="17566-122">Vous avez une application web (/VMSS/rôle de service cloud) et</span><span class="sxs-lookup"><span data-stu-id="17566-122">You have a web app (/VMSS/cloud service role) and</span></span> 

- <span data-ttu-id="17566-123">Vous souhaitez tooscale haut/bas en fonction de l’utilisation du processeur par défaut</span><span class="sxs-lookup"><span data-stu-id="17566-123">You want tooscale up/down based on CPU usage by default</span></span>
- <span data-ttu-id="17566-124">Toutefois, pendant la saison (ou des jours spécifiques qui sont importants pour votre entreprise) vous toooverride, hello par défaut et souhaitez davantage de capacité à votre disposition.</span><span class="sxs-lookup"><span data-stu-id="17566-124">However, during holiday season (or specific days that are important for your business) you want toooverride hello defaults and have more capacity at your disposal.</span></span>

![Mettre à l’échelle différemment lors des jours fériés][4]

## <a name="scale-based-on-custom-metric"></a><span data-ttu-id="17566-126">Mise à l’échelle en fonction de métriques personnalisées</span><span class="sxs-lookup"><span data-stu-id="17566-126">Scale based on custom metric</span></span>

<span data-ttu-id="17566-127">Vous avez un serveur web frontal et un niveau d’API qui communique avec le serveur principal hello.</span><span class="sxs-lookup"><span data-stu-id="17566-127">You have a web front end and a API tier that communicates with hello backend.</span></span> 

- <span data-ttu-id="17566-128">Vous souhaitez que le niveau de hello API tooscale basé sur des événements personnalisés dans frontal hello (exemple : vous souhaitez tooscale votre processus de validation basé sur le nombre de hello d’éléments de panier d’achat de hello)</span><span class="sxs-lookup"><span data-stu-id="17566-128">You want tooscale hello API tier based on custom events in hello front end (example: You want tooscale your checkout process based on hello number of items in hello shopping cart)</span></span>

![Mise à l’échelle en fonction de métriques personnalisées][5]

<!--Reference-->
[1]: ./monitoring-autoscale-get-started.md
[2]: ./media/monitoring-autoscale-common-scale-patterns/scale-based-on-cpu.png
[3]: ./media/monitoring-autoscale-common-scale-patterns/weekday-weekend-scale.png
[4]: ./media/monitoring-autoscale-common-scale-patterns/holidays-scale.png
[5]: ./media/monitoring-autoscale-common-scale-patterns/custom-metric-scale.png