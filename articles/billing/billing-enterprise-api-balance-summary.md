---
title: "aaaAzure API d’entreprise facturation - solde et résumé | Documents Microsoft"
description: "En savoir plus sur l’utilisation de facturation d’Azure et RateCard APIs, qui sont utilisés tooprovide connaître la consommation des ressources Azure et les tendances."
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
ms.openlocfilehash: b031de2c347e5abeacd11743cc96024434518918
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="reporting-apis-for-enterprise-customers---balance-and-summary"></a><span data-ttu-id="c5d27-103">API de création de rapports pour les clients Enterprise - Balance and Summary</span><span class="sxs-lookup"><span data-stu-id="c5d27-103">Reporting APIs for Enterprise customers - Balance and Summary</span></span>

<span data-ttu-id="c5d27-104">Hello solde et résumé API offre un résumé mensuel d’informations sur les soldes, nouveaux achats, des frais de service Azure Marketplace, ajustements et frais de dépassement.</span><span class="sxs-lookup"><span data-stu-id="c5d27-104">hello Balance and Summary API offers a monthly summary of information on balances, new purchases, Azure Marketplace service charges, adjustments, and overage charges.</span></span>


##<a name="request"></a><span data-ttu-id="c5d27-105">Demande</span><span class="sxs-lookup"><span data-stu-id="c5d27-105">Request</span></span> 
<span data-ttu-id="c5d27-106">Propriétés d’en-tête commun nécessitant toobe ajouté sont spécifiées [ici](billing-enterprise-api.md).</span><span class="sxs-lookup"><span data-stu-id="c5d27-106">Common header properties that need toobe added are specified [here](billing-enterprise-api.md).</span></span> <span data-ttu-id="c5d27-107">Si une période de facturation n’est pas spécifiée, puis les données de facturation actuel de hello période sont retournées.</span><span class="sxs-lookup"><span data-stu-id="c5d27-107">If a billing period is not specified, then data for hello current billing period is returned.</span></span>

|<span data-ttu-id="c5d27-108">Méthode</span><span class="sxs-lookup"><span data-stu-id="c5d27-108">Method</span></span> | <span data-ttu-id="c5d27-109">URI de demande</span><span class="sxs-lookup"><span data-stu-id="c5d27-109">Request URI</span></span>|
|-|-|
|<span data-ttu-id="c5d27-110">GET</span><span class="sxs-lookup"><span data-stu-id="c5d27-110">GET</span></span>| <span data-ttu-id="c5d27-111">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/balancesummary</span><span class="sxs-lookup"><span data-stu-id="c5d27-111">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/balancesummary</span></span>|
|<span data-ttu-id="c5d27-112">GET</span><span class="sxs-lookup"><span data-stu-id="c5d27-112">GET</span></span>| <span data-ttu-id="c5d27-113">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingPeriods/{billingPeriod}/balancesummary</span><span class="sxs-lookup"><span data-stu-id="c5d27-113">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingPeriods/{billingPeriod}/balancesummary</span></span>|

> [!Note]
> <span data-ttu-id="c5d27-114">version d’évaluation hello toouse de l’API, remplacez v2 v1 Bonjour au-dessus des URL.</span><span class="sxs-lookup"><span data-stu-id="c5d27-114">toouse hello preview version of API, replace v2 with v1 in hello above URL.</span></span>
>

## <a name="response"></a><span data-ttu-id="c5d27-115">Réponse</span><span class="sxs-lookup"><span data-stu-id="c5d27-115">Response</span></span>

        {
            "id": "enrollments/100/billingperiods/201507/balancesummaries",
            "billingPeriodId": 201507,
            "currencyCode": "USD",
            "beginningBalance": 0,
            "endingBalance": 1.1,
            "newPurchases": 1,
            "adjustments": 1.1,
            "utilized": 1.1,
            "serviceOverage": 1,
            "chargesBilledSeparately": 1,
            "totalOverage": 1,
            "totalUsage": 1.1,
            "azureMarketplaceServiceCharges": 1,
            "newPurchasesDetails": [
                {
                "name": "",
                "value": 1
                }
            ],
            "adjustmentDetails": [
                {
                "name": "Promo Credit",
                "value": 1.1
                },
                {
                "name": "SIE Credit",
                "value": 1.0
                }
            ]
        }


<span data-ttu-id="c5d27-116">**Définitions des propriétés de réponse**</span><span class="sxs-lookup"><span data-stu-id="c5d27-116">**Response property definitions**</span></span>

|<span data-ttu-id="c5d27-117">Nom de la propriété</span><span class="sxs-lookup"><span data-stu-id="c5d27-117">Property Name</span></span>| <span data-ttu-id="c5d27-118">Type</span><span class="sxs-lookup"><span data-stu-id="c5d27-118">Type</span></span>| <span data-ttu-id="c5d27-119">Description</span><span class="sxs-lookup"><span data-stu-id="c5d27-119">Description</span></span>
|-|-|-|
|<span data-ttu-id="c5d27-120">id</span><span class="sxs-lookup"><span data-stu-id="c5d27-120">id</span></span>|<span data-ttu-id="c5d27-121">string</span><span class="sxs-lookup"><span data-stu-id="c5d27-121">string</span></span>|<span data-ttu-id="c5d27-122">Hello Id unique pour une période de facturation donnée et l’inscription</span><span class="sxs-lookup"><span data-stu-id="c5d27-122">hello unique Id for a specific billing period and enrollment</span></span>|
|<span data-ttu-id="c5d27-123">billingPeriodId</span><span class="sxs-lookup"><span data-stu-id="c5d27-123">billingPeriodId</span></span>|<span data-ttu-id="c5d27-124">string</span><span class="sxs-lookup"><span data-stu-id="c5d27-124">string</span></span> |<span data-ttu-id="c5d27-125">Hello Id période de facturation</span><span class="sxs-lookup"><span data-stu-id="c5d27-125">hello billing period Id</span></span>|
|<span data-ttu-id="c5d27-126">currencyCode</span><span class="sxs-lookup"><span data-stu-id="c5d27-126">currencyCode</span></span>|<span data-ttu-id="c5d27-127">string</span><span class="sxs-lookup"><span data-stu-id="c5d27-127">string</span></span> |<span data-ttu-id="c5d27-128">code de devise Hello</span><span class="sxs-lookup"><span data-stu-id="c5d27-128">hello currency code</span></span>|
|<span data-ttu-id="c5d27-129">beginningBalance</span><span class="sxs-lookup"><span data-stu-id="c5d27-129">beginningBalance</span></span>|<span data-ttu-id="c5d27-130">Décimal</span><span class="sxs-lookup"><span data-stu-id="c5d27-130">decimal</span></span>| <span data-ttu-id="c5d27-131">Solde de début Hello pour la période de facturation hello</span><span class="sxs-lookup"><span data-stu-id="c5d27-131">hello beginning balance for hello billing period</span></span>|
|<span data-ttu-id="c5d27-132">endingBalance</span><span class="sxs-lookup"><span data-stu-id="c5d27-132">endingBalance</span></span>|<span data-ttu-id="c5d27-133">Décimal</span><span class="sxs-lookup"><span data-stu-id="c5d27-133">decimal</span></span>| <span data-ttu-id="c5d27-134">Hello solde de fin pour la période de facturation hello (pour les périodes ouvertes que cela sera mise à jour tous les jours)</span><span class="sxs-lookup"><span data-stu-id="c5d27-134">hello ending balance for hello billing period (for open periods this will be updated daily)</span></span>|
|<span data-ttu-id="c5d27-135">newPurchases</span><span class="sxs-lookup"><span data-stu-id="c5d27-135">newPurchases</span></span>|<span data-ttu-id="c5d27-136">Décimal</span><span class="sxs-lookup"><span data-stu-id="c5d27-136">decimal</span></span>| <span data-ttu-id="c5d27-137">Montant total des nouveaux achats</span><span class="sxs-lookup"><span data-stu-id="c5d27-137">Total new purchase amount</span></span>|
|<span data-ttu-id="c5d27-138">adjustments</span><span class="sxs-lookup"><span data-stu-id="c5d27-138">adjustments</span></span>|<span data-ttu-id="c5d27-139">Décimal</span><span class="sxs-lookup"><span data-stu-id="c5d27-139">decimal</span></span>| <span data-ttu-id="c5d27-140">Montant total d’ajustement</span><span class="sxs-lookup"><span data-stu-id="c5d27-140">Total adjustment amount</span></span>|
|<span data-ttu-id="c5d27-141">utilized</span><span class="sxs-lookup"><span data-stu-id="c5d27-141">utilized</span></span>|<span data-ttu-id="c5d27-142">Décimal</span><span class="sxs-lookup"><span data-stu-id="c5d27-142">decimal</span></span>| <span data-ttu-id="c5d27-143">Utilisation totale par de l’engagement</span><span class="sxs-lookup"><span data-stu-id="c5d27-143">Total Commitment usage</span></span>|
|<span data-ttu-id="c5d27-144">serviceOverage</span><span class="sxs-lookup"><span data-stu-id="c5d27-144">serviceOverage</span></span>|<span data-ttu-id="c5d27-145">Décimal</span><span class="sxs-lookup"><span data-stu-id="c5d27-145">decimal</span></span>| <span data-ttu-id="c5d27-146">Dépassement des services Azure</span><span class="sxs-lookup"><span data-stu-id="c5d27-146">Overage for Azure services</span></span>|
|<span data-ttu-id="c5d27-147">chargesBilledSeparately</span><span class="sxs-lookup"><span data-stu-id="c5d27-147">chargesBilledSeparately</span></span>|<span data-ttu-id="c5d27-148">Décimal</span><span class="sxs-lookup"><span data-stu-id="c5d27-148">decimal</span></span>| <span data-ttu-id="c5d27-149">Frais facturés séparément</span><span class="sxs-lookup"><span data-stu-id="c5d27-149">Charges Billed separately</span></span>|
|<span data-ttu-id="c5d27-150">totalOverage</span><span class="sxs-lookup"><span data-stu-id="c5d27-150">totalOverage</span></span>|<span data-ttu-id="c5d27-151">Décimal</span><span class="sxs-lookup"><span data-stu-id="c5d27-151">decimal</span></span>| <span data-ttu-id="c5d27-152">serviceOverage + chargesBilledSeparately</span><span class="sxs-lookup"><span data-stu-id="c5d27-152">serviceOverage + chargesBilledSeparately</span></span>|
|<span data-ttu-id="c5d27-153">totalUsage</span><span class="sxs-lookup"><span data-stu-id="c5d27-153">totalUsage</span></span>|<span data-ttu-id="c5d27-154">Décimal</span><span class="sxs-lookup"><span data-stu-id="c5d27-154">decimal</span></span>| <span data-ttu-id="c5d27-155">Engagement de service Azure + total du dépassement</span><span class="sxs-lookup"><span data-stu-id="c5d27-155">Azure service commitment + total Overage</span></span>|
|<span data-ttu-id="c5d27-156">azureMarketplaceServiceCharges</span><span class="sxs-lookup"><span data-stu-id="c5d27-156">azureMarketplaceServiceCharges</span></span>|<span data-ttu-id="c5d27-157">Décimal</span><span class="sxs-lookup"><span data-stu-id="c5d27-157">decimal</span></span>| <span data-ttu-id="c5d27-158">Total des frais pour la Place de marché Azure</span><span class="sxs-lookup"><span data-stu-id="c5d27-158">Total charges for Azure Marketplace</span></span>|
|<span data-ttu-id="c5d27-159">newPurchasesDetails</span><span class="sxs-lookup"><span data-stu-id="c5d27-159">newPurchasesDetails</span></span>|<span data-ttu-id="c5d27-160">Tableau de chaînes JSON de paires nom/valeur</span><span class="sxs-lookup"><span data-stu-id="c5d27-160">JSON string array of Name Value pairs</span></span>|<span data-ttu-id="c5d27-161">Liste de nouveaux achats</span><span class="sxs-lookup"><span data-stu-id="c5d27-161">List of new purchases</span></span>|
|<span data-ttu-id="c5d27-162">adjustmentDetails</span><span class="sxs-lookup"><span data-stu-id="c5d27-162">adjustmentDetails</span></span>|<span data-ttu-id="c5d27-163">Tableau de chaînes JSON de paires nom/valeur</span><span class="sxs-lookup"><span data-stu-id="c5d27-163">JSON string array of Name Value pairs</span></span>|<span data-ttu-id="c5d27-164">Liste d’ajustements (crédit de promotion, crédit SIE, etc.)</span><span class="sxs-lookup"><span data-stu-id="c5d27-164">List of Adjustments (Promo credit, SIE credit etc.)</span></span> |


<br/>
## <a name="see-also"></a><span data-ttu-id="c5d27-165">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="c5d27-165">See also</span></span>

* [<span data-ttu-id="c5d27-166">API Périodes de facturation</span><span class="sxs-lookup"><span data-stu-id="c5d27-166">Billing Periods API</span></span>](billing-enterprise-api-billing-periods.md)

* [<span data-ttu-id="c5d27-167">API Détails de l’utilisation</span><span class="sxs-lookup"><span data-stu-id="c5d27-167">Usage Detail API</span></span>](billing-enterprise-api-usage-detail.md) 

* [<span data-ttu-id="c5d27-168">API Frais de la Place de marché</span><span class="sxs-lookup"><span data-stu-id="c5d27-168">Marketplace Store Charge API</span></span>](billing-enterprise-api-marketplace-storecharge.md) 

* [<span data-ttu-id="c5d27-169">API Grille tarifaire</span><span class="sxs-lookup"><span data-stu-id="c5d27-169">Price Sheet API</span></span>](billing-enterprise-api-pricesheet.md)