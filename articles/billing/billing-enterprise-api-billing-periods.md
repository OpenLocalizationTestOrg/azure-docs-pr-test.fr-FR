---
title: "API de facturation Azure Enterprise - Périodes de facturation | Microsoft Docs"
description: "En savoir plus sur les API de création de rapports qui permettent aux clients d’Azure Enterprise d’extraire leurs données de consommation par programme."
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
ms.openlocfilehash: c6880b79189e0683387a7aafbd6fa4805b3b42ef
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="reporting-apis-for-enterprise-customers---billing-periods"></a><span data-ttu-id="d0dd6-103">API de création de rapports pour les clients Enterprise : périodes de facturation</span><span class="sxs-lookup"><span data-stu-id="d0dd6-103">Reporting APIs for Enterprise customers - Billing Periods</span></span>

<span data-ttu-id="d0dd6-104">L’API Périodes de facturation renvoie une liste des périodes de facturation contenant les données de consommation pour l’abonnement indiqué, par ordre chronologique inverse.</span><span class="sxs-lookup"><span data-stu-id="d0dd6-104">The Billing Periods API returns a list of billing periods that have consumption data for the specified Enrollment in reverse chronological order.</span></span> <span data-ttu-id="d0dd6-105">Chaque période contient une propriété qui pointe vers l’API Route (Itinéraire) pour les quatre ensembles de données : BalanceSummary (Solde et résumé), UsageDetails (Détails d’utilisation), Marketplace Charges (Frais de la Place de marché) et PriceSheet (Grille tarifaire).</span><span class="sxs-lookup"><span data-stu-id="d0dd6-105">Each Period contains a property pointing to the API route for the four sets of data - BalanceSummary, UsageDetails, Marktplace Charges, and PriceSheet.</span></span> <span data-ttu-id="d0dd6-106">Si la période n’a pas de données, la propriété correspondante est Null.</span><span class="sxs-lookup"><span data-stu-id="d0dd6-106">If the period does not have data, the corresponding property is null.</span></span> 


##<a name="request"></a><span data-ttu-id="d0dd6-107">Requête</span><span class="sxs-lookup"><span data-stu-id="d0dd6-107">Request</span></span> 
<span data-ttu-id="d0dd6-108">Les propriétés d’en-tête communes qui doivent être ajoutées sont spécifiées [ici](billing-enterprise-api.md).</span><span class="sxs-lookup"><span data-stu-id="d0dd6-108">Common header properties that need to be added are specified [here](billing-enterprise-api.md).</span></span> 

|<span data-ttu-id="d0dd6-109">Méthode</span><span class="sxs-lookup"><span data-stu-id="d0dd6-109">Method</span></span> | <span data-ttu-id="d0dd6-110">URI de demande</span><span class="sxs-lookup"><span data-stu-id="d0dd6-110">Request URI</span></span>|
|-|-|
|<span data-ttu-id="d0dd6-111">GET</span><span class="sxs-lookup"><span data-stu-id="d0dd6-111">GET</span></span>| <span data-ttu-id="d0dd6-112">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingperiods</span><span class="sxs-lookup"><span data-stu-id="d0dd6-112">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingperiods</span></span>|

> [!Note]
> <span data-ttu-id="d0dd6-113">Pour utiliser la version d’évaluation de l’API, remplacez v2 par v1 dans l’URL ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="d0dd6-113">To use the preview version of API, replace v2 with v1 in the above URL.</span></span>
>

## <a name="response"></a><span data-ttu-id="d0dd6-114">Réponse</span><span class="sxs-lookup"><span data-stu-id="d0dd6-114">Response</span></span>
 
    
    
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
    

<span data-ttu-id="d0dd6-115">**Définitions des propriétés de réponse**</span><span class="sxs-lookup"><span data-stu-id="d0dd6-115">**Response property definitions**</span></span>

|<span data-ttu-id="d0dd6-116">Nom de la propriété</span><span class="sxs-lookup"><span data-stu-id="d0dd6-116">Property Name</span></span>| <span data-ttu-id="d0dd6-117">Type</span><span class="sxs-lookup"><span data-stu-id="d0dd6-117">Type</span></span>| <span data-ttu-id="d0dd6-118">Description</span><span class="sxs-lookup"><span data-stu-id="d0dd6-118">Description</span></span>
|-|-|-|
|<span data-ttu-id="d0dd6-119">billingPeriodId</span><span class="sxs-lookup"><span data-stu-id="d0dd6-119">billingPeriodId</span></span>| <span data-ttu-id="d0dd6-120">chaîne</span><span class="sxs-lookup"><span data-stu-id="d0dd6-120">string</span></span>| <span data-ttu-id="d0dd6-121">ID unique qui représente une période de facturation donnée</span><span class="sxs-lookup"><span data-stu-id="d0dd6-121">The unique Id that represents a particular Billing period</span></span>|
|<span data-ttu-id="d0dd6-122">billingStart</span><span class="sxs-lookup"><span data-stu-id="d0dd6-122">billingStart</span></span>| <span data-ttu-id="d0dd6-123">datetime</span><span class="sxs-lookup"><span data-stu-id="d0dd6-123">datetime</span></span>| <span data-ttu-id="d0dd6-124">Chaîne ISO 8601 représentant la date de début de la période</span><span class="sxs-lookup"><span data-stu-id="d0dd6-124">ISO 8601 string representing the period start date</span></span>|
|<span data-ttu-id="d0dd6-125">billingEnd</span><span class="sxs-lookup"><span data-stu-id="d0dd6-125">billingEnd</span></span>| <span data-ttu-id="d0dd6-126">datetime</span><span class="sxs-lookup"><span data-stu-id="d0dd6-126">datetime</span></span>| <span data-ttu-id="d0dd6-127">Chaîne ISO 8601 représentant la date de fin de la période</span><span class="sxs-lookup"><span data-stu-id="d0dd6-127">ISO 8601 string representing the period end date</span></span>|
|<span data-ttu-id="d0dd6-128">balanceSummary</span><span class="sxs-lookup"><span data-stu-id="d0dd6-128">balanceSummary</span></span>| <span data-ttu-id="d0dd6-129">string</span><span class="sxs-lookup"><span data-stu-id="d0dd6-129">string</span></span>| <span data-ttu-id="d0dd6-130">Chemin d’accès d’URL qui route vers les données de résumé de solde pour cette période</span><span class="sxs-lookup"><span data-stu-id="d0dd6-130">The URL path that routes to the Balance Summary data for this period</span></span>|
|<span data-ttu-id="d0dd6-131">usageDetails</span><span class="sxs-lookup"><span data-stu-id="d0dd6-131">usageDetails</span></span>| <span data-ttu-id="d0dd6-132">string</span><span class="sxs-lookup"><span data-stu-id="d0dd6-132">string</span></span>| <span data-ttu-id="d0dd6-133">Chemin d’accès d’URL qui route vers les données de détails d’utilisation pour cette période</span><span class="sxs-lookup"><span data-stu-id="d0dd6-133">The URL path that routes to the Usage Details data for this period</span></span>|
|<span data-ttu-id="d0dd6-134">marketplaceCharges</span><span class="sxs-lookup"><span data-stu-id="d0dd6-134">marketplaceCharges</span></span>| <span data-ttu-id="d0dd6-135">string</span><span class="sxs-lookup"><span data-stu-id="d0dd6-135">string</span></span>| <span data-ttu-id="d0dd6-136">Chemin d’accès d’URL qui route vers les données de frais de Place de marché pour cette période</span><span class="sxs-lookup"><span data-stu-id="d0dd6-136">The URL path that routes to the Marketplace Charges data for this period</span></span>|
|<span data-ttu-id="d0dd6-137">priceSheet</span><span class="sxs-lookup"><span data-stu-id="d0dd6-137">priceSheet</span></span>| <span data-ttu-id="d0dd6-138">string</span><span class="sxs-lookup"><span data-stu-id="d0dd6-138">string</span></span>| <span data-ttu-id="d0dd6-139">Chemin d’accès d’URL qui route vers les données de grille tarifaire pour cette période</span><span class="sxs-lookup"><span data-stu-id="d0dd6-139">The URL path that routes to the PriceSheet data for this period</span></span>|

<br/>
## <a name="see-also"></a><span data-ttu-id="d0dd6-140">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="d0dd6-140">See also</span></span>

* [<span data-ttu-id="d0dd6-141">API Solde et résumé</span><span class="sxs-lookup"><span data-stu-id="d0dd6-141">Balance and Summary API</span></span>](billing-enterprise-api-balance-summary.md)

* [<span data-ttu-id="d0dd6-142">API Détails de l’utilisation</span><span class="sxs-lookup"><span data-stu-id="d0dd6-142">Usage Detail API</span></span>](billing-enterprise-api-usage-detail.md) 

* [<span data-ttu-id="d0dd6-143">API Frais de la Place de marché</span><span class="sxs-lookup"><span data-stu-id="d0dd6-143">Marketplace Store Charge API</span></span>](billing-enterprise-api-marketplace-storecharge.md) 

* [<span data-ttu-id="d0dd6-144">API Grille tarifaire</span><span class="sxs-lookup"><span data-stu-id="d0dd6-144">Price Sheet API</span></span>](billing-enterprise-api-pricesheet.md)