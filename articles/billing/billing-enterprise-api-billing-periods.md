---
title: "aaaAzure API Enterprise sur la facturation - périodes de facturation | Documents Microsoft"
description: "Découvrez hello API de Reporting qui permettent aux données de consommation de toopull clients entreprise Azure par programme."
services: 
documentationcenter: 
author: aedwin
manager: aedwin
editor: 
tags: billing
ms.assetid: 3e817b43-0696-400c-a02e-47b7817f9b77
ms.service: billing
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: billing
ms.date: 04/25/2017
ms.author: aedwin
ms.openlocfilehash: d4e17f25b22729a7f213306fb019ee0dbeca87ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="reporting-apis-for-enterprise-customers---billing-periods"></a><span data-ttu-id="3db01-103">API de création de rapports pour les clients Enterprise : périodes de facturation</span><span class="sxs-lookup"><span data-stu-id="3db01-103">Reporting APIs for Enterprise customers - Billing Periods</span></span>

<span data-ttu-id="3db01-104">Hello API de périodes de facturation retourne une liste de facturation des périodes qui contiennent des données de consommation pour hello spécifiée d’inscription dans l’ordre chronologique inverse.</span><span class="sxs-lookup"><span data-stu-id="3db01-104">hello Billing Periods API returns a list of billing periods that have consumption data for hello specified Enrollment in reverse chronological order.</span></span> <span data-ttu-id="3db01-105">Chaque période contient une propriété pointant itinéraire d’API toohello pour hello quatre ensembles de données - BalanceSummary, UsageDetails, les frais de Marktplace et PriceSheet.</span><span class="sxs-lookup"><span data-stu-id="3db01-105">Each Period contains a property pointing toohello API route for hello four sets of data - BalanceSummary, UsageDetails, Marktplace Charges, and PriceSheet.</span></span> <span data-ttu-id="3db01-106">Si la période de hello n’a pas de données, la propriété correspondante de hello est null.</span><span class="sxs-lookup"><span data-stu-id="3db01-106">If hello period does not have data, hello corresponding property is null.</span></span> 


##<a name="request"></a><span data-ttu-id="3db01-107">Demande</span><span class="sxs-lookup"><span data-stu-id="3db01-107">Request</span></span> 
<span data-ttu-id="3db01-108">Propriétés d’en-tête commun nécessitant toobe ajouté sont spécifiées [ici](billing-enterprise-api.md).</span><span class="sxs-lookup"><span data-stu-id="3db01-108">Common header properties that need toobe added are specified [here](billing-enterprise-api.md).</span></span> 

|<span data-ttu-id="3db01-109">Méthode</span><span class="sxs-lookup"><span data-stu-id="3db01-109">Method</span></span> | <span data-ttu-id="3db01-110">URI de demande</span><span class="sxs-lookup"><span data-stu-id="3db01-110">Request URI</span></span>|
|-|-|
|<span data-ttu-id="3db01-111">GET</span><span class="sxs-lookup"><span data-stu-id="3db01-111">GET</span></span>| <span data-ttu-id="3db01-112">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingperiods</span><span class="sxs-lookup"><span data-stu-id="3db01-112">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingperiods</span></span>|

> [!Note]
> <span data-ttu-id="3db01-113">version d’évaluation hello toouse de l’API, remplacez v2 v1 Bonjour au-dessus des URL.</span><span class="sxs-lookup"><span data-stu-id="3db01-113">toouse hello preview version of API, replace v2 with v1 in hello above URL.</span></span>
>

## <a name="response"></a><span data-ttu-id="3db01-114">Réponse</span><span class="sxs-lookup"><span data-stu-id="3db01-114">Response</span></span>
 
    
    
      [
            {
                "billingPeriodId": "201704",
                "billingStart": "2017-04-01T00:00:00Z",
                "billingEnd": "2017-04-30T11:59:59Z",
                "balanceSummary": "/v1/enrollments/100/billingperiods/201704/balancesummary",
                "usageDetails": "/v1/enrollments/100/billingperiods/201704/usagedetails",
                "marketplaceCharges": "/v1/enrollments/100/billingperiods/201704/marketplacecharges",
                "priceSheet": "/v1/enrollments/100/billingperiods/201704/pricesheet"
            },          
            ....
      ]
    

<span data-ttu-id="3db01-115">**Définitions des propriétés de réponse**</span><span class="sxs-lookup"><span data-stu-id="3db01-115">**Response property definitions**</span></span>

|<span data-ttu-id="3db01-116">Nom de la propriété</span><span class="sxs-lookup"><span data-stu-id="3db01-116">Property Name</span></span>| <span data-ttu-id="3db01-117">Type</span><span class="sxs-lookup"><span data-stu-id="3db01-117">Type</span></span>| <span data-ttu-id="3db01-118">Description</span><span class="sxs-lookup"><span data-stu-id="3db01-118">Description</span></span>
|-|-|-|
|<span data-ttu-id="3db01-119">billingPeriodId</span><span class="sxs-lookup"><span data-stu-id="3db01-119">billingPeriodId</span></span>| <span data-ttu-id="3db01-120">string</span><span class="sxs-lookup"><span data-stu-id="3db01-120">string</span></span>| <span data-ttu-id="3db01-121">Hello Id unique qui représente une période de facturation particulière</span><span class="sxs-lookup"><span data-stu-id="3db01-121">hello unique Id that represents a particular Billing period</span></span>|
|<span data-ttu-id="3db01-122">billingStart</span><span class="sxs-lookup"><span data-stu-id="3db01-122">billingStart</span></span>| <span data-ttu-id="3db01-123">datetime</span><span class="sxs-lookup"><span data-stu-id="3db01-123">datetime</span></span>| <span data-ttu-id="3db01-124">Chaîne ISO 8601 représentant la date de début de la période de hello</span><span class="sxs-lookup"><span data-stu-id="3db01-124">ISO 8601 string representing hello period start date</span></span>|
|<span data-ttu-id="3db01-125">billingEnd</span><span class="sxs-lookup"><span data-stu-id="3db01-125">billingEnd</span></span>| <span data-ttu-id="3db01-126">datetime</span><span class="sxs-lookup"><span data-stu-id="3db01-126">datetime</span></span>| <span data-ttu-id="3db01-127">Chaîne ISO 8601 représentant la date de fin de la période de hello</span><span class="sxs-lookup"><span data-stu-id="3db01-127">ISO 8601 string representing hello period end date</span></span>|
|<span data-ttu-id="3db01-128">balanceSummary</span><span class="sxs-lookup"><span data-stu-id="3db01-128">balanceSummary</span></span>| <span data-ttu-id="3db01-129">string</span><span class="sxs-lookup"><span data-stu-id="3db01-129">string</span></span>| <span data-ttu-id="3db01-130">chemin d’accès URL Hello qui achemine les données de résumé de solde toohello pour cette période</span><span class="sxs-lookup"><span data-stu-id="3db01-130">hello URL path that routes toohello Balance Summary data for this period</span></span>|
|<span data-ttu-id="3db01-131">usageDetails</span><span class="sxs-lookup"><span data-stu-id="3db01-131">usageDetails</span></span>| <span data-ttu-id="3db01-132">string</span><span class="sxs-lookup"><span data-stu-id="3db01-132">string</span></span>| <span data-ttu-id="3db01-133">chemin d’accès URL Hello qui achemine les données des détails d’utilisation de toohello pour cette période</span><span class="sxs-lookup"><span data-stu-id="3db01-133">hello URL path that routes toohello Usage Details data for this period</span></span>|
|<span data-ttu-id="3db01-134">marketplaceCharges</span><span class="sxs-lookup"><span data-stu-id="3db01-134">marketplaceCharges</span></span>| <span data-ttu-id="3db01-135">string</span><span class="sxs-lookup"><span data-stu-id="3db01-135">string</span></span>| <span data-ttu-id="3db01-136">chemin d’accès URL Hello qui achemine les données de frais Marketplace toohello pour cette période</span><span class="sxs-lookup"><span data-stu-id="3db01-136">hello URL path that routes toohello Marketplace Charges data for this period</span></span>|
|<span data-ttu-id="3db01-137">priceSheet</span><span class="sxs-lookup"><span data-stu-id="3db01-137">priceSheet</span></span>| <span data-ttu-id="3db01-138">string</span><span class="sxs-lookup"><span data-stu-id="3db01-138">string</span></span>| <span data-ttu-id="3db01-139">chemin d’accès URL Hello qui achemine les données de PriceSheet toohello pour cette période</span><span class="sxs-lookup"><span data-stu-id="3db01-139">hello URL path that routes toohello PriceSheet data for this period</span></span>|

<br/>
## <a name="see-also"></a><span data-ttu-id="3db01-140">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="3db01-140">See also</span></span>

* [<span data-ttu-id="3db01-141">API Solde et résumé</span><span class="sxs-lookup"><span data-stu-id="3db01-141">Balance and Summary API</span></span>](billing-enterprise-api-balance-summary.md)

* [<span data-ttu-id="3db01-142">API Détails de l’utilisation</span><span class="sxs-lookup"><span data-stu-id="3db01-142">Usage Detail API</span></span>](billing-enterprise-api-usage-detail.md) 

* [<span data-ttu-id="3db01-143">API Frais de la Place de marché</span><span class="sxs-lookup"><span data-stu-id="3db01-143">Marketplace Store Charge API</span></span>](billing-enterprise-api-marketplace-storecharge.md) 

* [<span data-ttu-id="3db01-144">API Grille tarifaire</span><span class="sxs-lookup"><span data-stu-id="3db01-144">Price Sheet API</span></span>](billing-enterprise-api-pricesheet.md)