---
title: "aaaAzure API d’entreprise facturation - PriceSheet | Documents Microsoft"
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
ms.openlocfilehash: 4cfe694c63fba266d117054b046d9caacb3b7197
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="reporting-apis-for-enterprise-customers---price-sheet"></a><span data-ttu-id="19285-103">API de création de rapports pour les clients en entreprise - Grille tarifaire</span><span class="sxs-lookup"><span data-stu-id="19285-103">Reporting APIs for Enterprise customers - Price Sheet</span></span>

<span data-ttu-id="19285-104">Hello API de feuille de prix fournit les taux applicable hello pour chacun des compteurs pour hello donné d’inscription et la période de facturation.</span><span class="sxs-lookup"><span data-stu-id="19285-104">hello Price Sheet API provides hello applicable rate for each Meter for hello given Enrollment and Billing Period.</span></span>

##<a name="request"></a><span data-ttu-id="19285-105">Demande</span><span class="sxs-lookup"><span data-stu-id="19285-105">Request</span></span>
<span data-ttu-id="19285-106">Propriétés d’en-tête commun nécessitant toobe ajouté sont spécifiées [ici](billing-enterprise-api.md).</span><span class="sxs-lookup"><span data-stu-id="19285-106">Common header properties that need toobe added are specified [here](billing-enterprise-api.md).</span></span> <span data-ttu-id="19285-107">Si une période de facturation n’est pas spécifiée, puis les données de facturation actuel de hello période sont retournées.</span><span class="sxs-lookup"><span data-stu-id="19285-107">If a billing period is not specified, then data for hello current billing period is returned.</span></span>

|<span data-ttu-id="19285-108">Méthode</span><span class="sxs-lookup"><span data-stu-id="19285-108">Method</span></span> | <span data-ttu-id="19285-109">URI de demande</span><span class="sxs-lookup"><span data-stu-id="19285-109">Request URI</span></span>|
|-|-|
|<span data-ttu-id="19285-110">GET</span><span class="sxs-lookup"><span data-stu-id="19285-110">GET</span></span>|<span data-ttu-id="19285-111">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/pricesheet</span><span class="sxs-lookup"><span data-stu-id="19285-111">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/pricesheet</span></span>|
|<span data-ttu-id="19285-112">GET</span><span class="sxs-lookup"><span data-stu-id="19285-112">GET</span></span>|<span data-ttu-id="19285-113">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingPeriods/{billingPeriod}/pricesheet</span><span class="sxs-lookup"><span data-stu-id="19285-113">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingPeriods/{billingPeriod}/pricesheet</span></span>|

> [!Note]
> <span data-ttu-id="19285-114">version d’évaluation hello toouse de l’API, remplacez v2 v1 Bonjour au-dessus des URL.</span><span class="sxs-lookup"><span data-stu-id="19285-114">toouse hello preview version of API, replace v2 with v1 in hello above URL.</span></span>
>

## <a name="response"></a><span data-ttu-id="19285-115">Réponse</span><span class="sxs-lookup"><span data-stu-id="19285-115">Response</span></span>

    
        [
            {
                "id": "enrollments/57354989/billingperiods/201601/products/343/pricesheets",
                "billingPeriodId": "201704",
                "meterId": "dc210ecb-97e8-4522-8134-2385494233c0",
                "meterName": "A1 VM",
                "unitOfMeasure": "100 Hours",
                "includedQuantity": 0,
                "partNumber": "N7H-00015",
                "unitPrice": 0.00,
                "currencyCode": "USD"
            },
            {
                "id": "enrollments/57354989/billingperiods/201601/products/2884/pricesheets",
                "billingPeriodId": "201404",
                "meterId": "dc210ecb-97e8-4522-8134-5385494233c0",
                "meterName": "Locally Redundant Storage Premium Storage - Snapshots - AU East",
                "unitOfMeasure": "100 GB",
                "includedQuantity": 0,
                "partNumber": "N9H-00402",
                "unitPrice": 0.00,
                "currencyCode": "USD"
            },
            ...
        ]
    

> [!Note]
><span data-ttu-id="19285-116">Si vous utilisez hello API d’aperçu, le champ d’ID de jauge n’est pas disponible.</span><span class="sxs-lookup"><span data-stu-id="19285-116">If you are using hello Preview API, meterId field is not available.</span></span>
>

<span data-ttu-id="19285-117">**Définitions des propriétés de réponse**</span><span class="sxs-lookup"><span data-stu-id="19285-117">**Response property definitions**</span></span>

|<span data-ttu-id="19285-118">Nom de la propriété</span><span class="sxs-lookup"><span data-stu-id="19285-118">Property Name</span></span>| <span data-ttu-id="19285-119">Type</span><span class="sxs-lookup"><span data-stu-id="19285-119">Type</span></span>| <span data-ttu-id="19285-120">Description</span><span class="sxs-lookup"><span data-stu-id="19285-120">Description</span></span>
|-|-|-|
|<span data-ttu-id="19285-121">id</span><span class="sxs-lookup"><span data-stu-id="19285-121">id</span></span>| <span data-ttu-id="19285-122">string</span><span class="sxs-lookup"><span data-stu-id="19285-122">string</span></span>| <span data-ttu-id="19285-123">Hello Id unique qui représente un élément particulier de PriceSheet (compteur par période de facturation)</span><span class="sxs-lookup"><span data-stu-id="19285-123">hello unique Id that represents a particular PriceSheet item (meter by billing period)</span></span>|
|<span data-ttu-id="19285-124">billingPeriodId</span><span class="sxs-lookup"><span data-stu-id="19285-124">billingPeriodId</span></span>| <span data-ttu-id="19285-125">string</span><span class="sxs-lookup"><span data-stu-id="19285-125">string</span></span>| <span data-ttu-id="19285-126">Hello Id unique qui représente une période de facturation particulière</span><span class="sxs-lookup"><span data-stu-id="19285-126">hello unique Id that represents a particular Billing period</span></span>|
|<span data-ttu-id="19285-127">meterId</span><span class="sxs-lookup"><span data-stu-id="19285-127">meterId</span></span>| <span data-ttu-id="19285-128">string</span><span class="sxs-lookup"><span data-stu-id="19285-128">string</span></span>| <span data-ttu-id="19285-129">Identificateur Hello pour le compteur de hello.</span><span class="sxs-lookup"><span data-stu-id="19285-129">hello identifier for hello meter.</span></span> <span data-ttu-id="19285-130">Il peut être mappé toohello utilisation de l’ID de jauge.</span><span class="sxs-lookup"><span data-stu-id="19285-130">It can be mapped toohello usage meterId.</span></span>|
|<span data-ttu-id="19285-131">meterName</span><span class="sxs-lookup"><span data-stu-id="19285-131">meterName</span></span>| <span data-ttu-id="19285-132">string</span><span class="sxs-lookup"><span data-stu-id="19285-132">string</span></span>| <span data-ttu-id="19285-133">nom de compteur Hello</span><span class="sxs-lookup"><span data-stu-id="19285-133">hello meter name</span></span>|
|<span data-ttu-id="19285-134">unitOfMeasure</span><span class="sxs-lookup"><span data-stu-id="19285-134">unitOfMeasure</span></span>| <span data-ttu-id="19285-135">string</span><span class="sxs-lookup"><span data-stu-id="19285-135">string</span></span>| <span data-ttu-id="19285-136">Hello unité de mesure de service de hello</span><span class="sxs-lookup"><span data-stu-id="19285-136">hello Unit of Measure for measuring hello service</span></span>|
|<span data-ttu-id="19285-137">includedQuantity</span><span class="sxs-lookup"><span data-stu-id="19285-137">includedQuantity</span></span>| <span data-ttu-id="19285-138">décimal</span><span class="sxs-lookup"><span data-stu-id="19285-138">decimal</span></span>| <span data-ttu-id="19285-139">Quantité incluse</span><span class="sxs-lookup"><span data-stu-id="19285-139">Quantity that is included</span></span> |
|<span data-ttu-id="19285-140">partNumber</span><span class="sxs-lookup"><span data-stu-id="19285-140">partNumber</span></span>| <span data-ttu-id="19285-141">string</span><span class="sxs-lookup"><span data-stu-id="19285-141">string</span></span>| <span data-ttu-id="19285-142">numéro de référence Hello associé hello compteur</span><span class="sxs-lookup"><span data-stu-id="19285-142">hello part number associated with hello Meter</span></span>|
|<span data-ttu-id="19285-143">unitPrice</span><span class="sxs-lookup"><span data-stu-id="19285-143">unitPrice</span></span>| <span data-ttu-id="19285-144">Décimal</span><span class="sxs-lookup"><span data-stu-id="19285-144">decimal</span></span>| <span data-ttu-id="19285-145">prix unitaire Hello pour le compteur de hello</span><span class="sxs-lookup"><span data-stu-id="19285-145">hello unit price for hello meter</span></span>|
|<span data-ttu-id="19285-146">currencyCode</span><span class="sxs-lookup"><span data-stu-id="19285-146">currencyCode</span></span>| <span data-ttu-id="19285-147">string</span><span class="sxs-lookup"><span data-stu-id="19285-147">string</span></span>| <span data-ttu-id="19285-148">code de devise Hello hello UnitPrice</span><span class="sxs-lookup"><span data-stu-id="19285-148">hello currency code for hello unitPrice</span></span>|
<br/>
## <a name="see-also"></a><span data-ttu-id="19285-149">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="19285-149">See also</span></span>

* [<span data-ttu-id="19285-150">API Périodes de facturation</span><span class="sxs-lookup"><span data-stu-id="19285-150">Billing Periods API</span></span>](billing-enterprise-api-billing-periods.md)

* [<span data-ttu-id="19285-151">API Détails de l’utilisation</span><span class="sxs-lookup"><span data-stu-id="19285-151">Usage Detail API</span></span>](billing-enterprise-api-usage-detail.md)

* [<span data-ttu-id="19285-152">API Solde et résumé</span><span class="sxs-lookup"><span data-stu-id="19285-152">Balance and Summary API</span></span>](billing-enterprise-api-balance-summary.md)

* [<span data-ttu-id="19285-153">API Frais de la Place de marché</span><span class="sxs-lookup"><span data-stu-id="19285-153">Marketplace Store Charge API</span></span>](billing-enterprise-api-marketplace-storecharge.md)
