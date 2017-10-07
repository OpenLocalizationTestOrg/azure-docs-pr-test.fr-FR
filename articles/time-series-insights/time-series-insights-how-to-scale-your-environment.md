---
title: "aaaHow tooscale votre environnement Azure temps série Insights | Documents Microsoft"
description: "Ce didacticiel décrit comment tooscale votre environnement de la série de temps Azure Insights"
keywords: 
services: time-series-insights
documentationcenter: 
author: sandshadow
manager: almineev
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/19/2017
ms.author: edett
ms.openlocfilehash: 55eda388997589185bd34228762b95e182b228ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooscale-your-time-series-insights-environment"></a><span data-ttu-id="0b601-103">Comment tooscale votre environnement un aperçu en temps série</span><span class="sxs-lookup"><span data-stu-id="0b601-103">How tooscale your Time Series Insights environment</span></span>

<span data-ttu-id="0b601-104">Ce didacticiel décrit comment tooscale votre environnement Insights de série de temps.</span><span class="sxs-lookup"><span data-stu-id="0b601-104">This tutorial covers how tooscale your Time Series Insights environment.</span></span>

> [!NOTE]
> <span data-ttu-id="0b601-105">La mise à l’échelle sur différents types de référence n’est pas autorisée.</span><span class="sxs-lookup"><span data-stu-id="0b601-105">Scale up across sku types is not allowed.</span></span> <span data-ttu-id="0b601-106">Un environnement avec une référence S1 ne peut pas être converti en environnement S2.</span><span class="sxs-lookup"><span data-stu-id="0b601-106">An environment with a S1 Sku cannot be converted into an S2 environment.</span></span>

## <a name="s1-sku-ingress-rates-and-capacities"></a><span data-ttu-id="0b601-107">Capacités et débits d’entrée de la référence S1</span><span class="sxs-lookup"><span data-stu-id="0b601-107">S1 SKU ingress rates and capacities</span></span>

| <span data-ttu-id="0b601-108">Capacité de la référence S1</span><span class="sxs-lookup"><span data-stu-id="0b601-108">S1 SKU Capacity</span></span> | <span data-ttu-id="0b601-109">Débit d’entrée</span><span class="sxs-lookup"><span data-stu-id="0b601-109">Ingress Rate</span></span> | <span data-ttu-id="0b601-110">Capacité de stockage maximale</span><span class="sxs-lookup"><span data-stu-id="0b601-110">Maximum Storage Capacity</span></span>
| --- | --- | --- |
| <span data-ttu-id="0b601-111">1</span><span class="sxs-lookup"><span data-stu-id="0b601-111">1</span></span> | <span data-ttu-id="0b601-112">1 Go (1 million d’événements)</span><span class="sxs-lookup"><span data-stu-id="0b601-112">1 GB (1 million events)</span></span> | <span data-ttu-id="0b601-113">30 Go (30 millions d’événements) par mois</span><span class="sxs-lookup"><span data-stu-id="0b601-113">30 GB (30 million events) per month</span></span> |
| <span data-ttu-id="0b601-114">10</span><span class="sxs-lookup"><span data-stu-id="0b601-114">10</span></span> | <span data-ttu-id="0b601-115">10 Go (10 millions d’événements)</span><span class="sxs-lookup"><span data-stu-id="0b601-115">10 GB (10 million events)</span></span> | <span data-ttu-id="0b601-116">300 Go (300 millions d’événements) par mois</span><span class="sxs-lookup"><span data-stu-id="0b601-116">300 GB (300 million events) per month</span></span> |

## <a name="s2-sku-ingress-rates-and-capacities"></a><span data-ttu-id="0b601-117">Capacités et débits d’entrée de la référence S2</span><span class="sxs-lookup"><span data-stu-id="0b601-117">S2 SKU ingress rates and capacities</span></span>

| <span data-ttu-id="0b601-118">Capacité de la référence S2</span><span class="sxs-lookup"><span data-stu-id="0b601-118">S2 SKU Capacity</span></span> | <span data-ttu-id="0b601-119">Débit d’entrée</span><span class="sxs-lookup"><span data-stu-id="0b601-119">Ingress Rate</span></span> | <span data-ttu-id="0b601-120">Capacité de stockage maximale</span><span class="sxs-lookup"><span data-stu-id="0b601-120">Maximum Storage Capacity</span></span>
| --- | --- | --- |
| <span data-ttu-id="0b601-121">1</span><span class="sxs-lookup"><span data-stu-id="0b601-121">1</span></span> | <span data-ttu-id="0b601-122">10 Go (10 millions d’événements)</span><span class="sxs-lookup"><span data-stu-id="0b601-122">10 GB (10 million events)</span></span> | <span data-ttu-id="0b601-123">300 Go (300 millions d’événements) par mois</span><span class="sxs-lookup"><span data-stu-id="0b601-123">300 GB (300 million events) per month</span></span> |
| <span data-ttu-id="0b601-124">10</span><span class="sxs-lookup"><span data-stu-id="0b601-124">10</span></span> | <span data-ttu-id="0b601-125">100 Go (100 millions d’événements)</span><span class="sxs-lookup"><span data-stu-id="0b601-125">100 GB (100 million events)</span></span> | <span data-ttu-id="0b601-126">3 To (3 milliards d’événements) par mois</span><span class="sxs-lookup"><span data-stu-id="0b601-126">3 TB (3 billion events) per month</span></span> |

<span data-ttu-id="0b601-127">Les capacités sont mises à l’échelle de façon linéaire. Par conséquent, une référence S1 avec la capacité 2 prend en charge 2 Go (2 millions) d’événements par débit d’entrée par jour et 60 Go (60 millions d’événements) par mois.</span><span class="sxs-lookup"><span data-stu-id="0b601-127">Capacities scale linearly, so a S1 sku with capacity 2 supports 2 GB (2 million) events per day ingress rate and 60 GB (60 million events) per month.</span></span>

## <a name="changing-hello-capacity-of-your-environment"></a><span data-ttu-id="0b601-128">Modification de la capacité de hello de votre environnement</span><span class="sxs-lookup"><span data-stu-id="0b601-128">Changing hello capacity of your environment</span></span>

1. <span data-ttu-id="0b601-129">Bonjour portail Azure, sélectionnez hello environnement dont vous souhaitez toochange.</span><span class="sxs-lookup"><span data-stu-id="0b601-129">In hello Azure portal, select hello environment whose capacity you want toochange.</span></span>
1. <span data-ttu-id="0b601-130">Sous Paramètres, cliquez sur Configurer.</span><span class="sxs-lookup"><span data-stu-id="0b601-130">Under Settings, click Configure.</span></span>
1. <span data-ttu-id="0b601-131">Utilisez hello capacité curseur tooselect hello capacité qui répond aux exigences de hello pour vos tarifs en entrée et la capacité de stockage.</span><span class="sxs-lookup"><span data-stu-id="0b601-131">Use hello Capacity slider tooselect hello capacity that meets hello requirements for your ingress rates and storage capacity.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0b601-132">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0b601-132">Next steps</span></span>

* <span data-ttu-id="0b601-133">Vérifiez que la nouvelle capacité de hello est suffisante tooprevent de limitation.</span><span class="sxs-lookup"><span data-stu-id="0b601-133">Verify that hello new capacity is sufficient tooprevent throttling.</span></span> <span data-ttu-id="0b601-134">Pour plus d’informations, consultez hello *votre environnement peut être mise en route limitée* section [ici](time-series-insights-diagnose-and-solve-problems.md).</span><span class="sxs-lookup"><span data-stu-id="0b601-134">For more details, see hello *Your environment might be getting throttled* section [here](time-series-insights-diagnose-and-solve-problems.md).</span></span>
