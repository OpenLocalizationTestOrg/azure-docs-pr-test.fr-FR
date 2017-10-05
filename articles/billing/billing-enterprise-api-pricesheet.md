---
title: "API de facturation d’entreprise Azure - Grille tarifaire | Microsoft Docs"
description: "Découvrez les API de création de rapports qui permettent aux clients Azure en entreprise d’extraire leurs données de consommation par programmation."
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
ms.openlocfilehash: 2e7d6e883abe4cee13bc5f684baf2a1ea9c6c397
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="reporting-apis-for-enterprise-customers---price-sheet"></a><span data-ttu-id="96c58-103">API de création de rapports pour les clients en entreprise - Grille tarifaire</span><span class="sxs-lookup"><span data-stu-id="96c58-103">Reporting APIs for Enterprise customers - Price Sheet</span></span>

<span data-ttu-id="96c58-104">L’API Grille tarifaire fournit les tarifs applicables pour chaque compteur selon l’abonnement et la période de facturation donnés.</span><span class="sxs-lookup"><span data-stu-id="96c58-104">The Price Sheet API provides the applicable rate for each Meter for the given Enrollment and Billing Period.</span></span>

##<a name="request"></a><span data-ttu-id="96c58-105">Requête</span><span class="sxs-lookup"><span data-stu-id="96c58-105">Request</span></span>
<span data-ttu-id="96c58-106">Les propriétés d’en-tête communes qui doivent être ajoutées sont spécifiées [ici](billing-enterprise-api.md).</span><span class="sxs-lookup"><span data-stu-id="96c58-106">Common header properties that need to be added are specified [here](billing-enterprise-api.md).</span></span> <span data-ttu-id="96c58-107">Si aucune période de facturation n’est spécifiée, les données de la période de facturation en cours sont retournées.</span><span class="sxs-lookup"><span data-stu-id="96c58-107">If a billing period is not specified, then data for the current billing period is returned.</span></span>

|<span data-ttu-id="96c58-108">Méthode</span><span class="sxs-lookup"><span data-stu-id="96c58-108">Method</span></span> | <span data-ttu-id="96c58-109">URI de demande</span><span class="sxs-lookup"><span data-stu-id="96c58-109">Request URI</span></span>|
|-|-|
|<span data-ttu-id="96c58-110">GET</span><span class="sxs-lookup"><span data-stu-id="96c58-110">GET</span></span>|<span data-ttu-id="96c58-111">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/pricesheet</span><span class="sxs-lookup"><span data-stu-id="96c58-111">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/pricesheet</span></span>|
|<span data-ttu-id="96c58-112">GET</span><span class="sxs-lookup"><span data-stu-id="96c58-112">GET</span></span>|<span data-ttu-id="96c58-113">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingPeriods/{billingPeriod}/pricesheet</span><span class="sxs-lookup"><span data-stu-id="96c58-113">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingPeriods/{billingPeriod}/pricesheet</span></span>|

> [!Note]
> <span data-ttu-id="96c58-114">Pour utiliser la préversion de l’API, remplacez v2 par v1 dans l’URL ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="96c58-114">To use the preview version of API, replace v2 with v1 in the above URL.</span></span>
>

## <a name="response"></a><span data-ttu-id="96c58-115">Réponse</span><span class="sxs-lookup"><span data-stu-id="96c58-115">Response</span></span>

    
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
><span data-ttu-id="96c58-116">Si vous utilisez la préversion de l’API, le champ meterId n’est pas disponible.</span><span class="sxs-lookup"><span data-stu-id="96c58-116">If you are using the Preview API, meterId field is not available.</span></span>
>

<span data-ttu-id="96c58-117">**Définitions des propriétés de réponse**</span><span class="sxs-lookup"><span data-stu-id="96c58-117">**Response property definitions**</span></span>

|<span data-ttu-id="96c58-118">Nom de la propriété</span><span class="sxs-lookup"><span data-stu-id="96c58-118">Property Name</span></span>| <span data-ttu-id="96c58-119">Type</span><span class="sxs-lookup"><span data-stu-id="96c58-119">Type</span></span>| <span data-ttu-id="96c58-120">Description</span><span class="sxs-lookup"><span data-stu-id="96c58-120">Description</span></span>
|-|-|-|
|<span data-ttu-id="96c58-121">id</span><span class="sxs-lookup"><span data-stu-id="96c58-121">id</span></span>| <span data-ttu-id="96c58-122">chaîne</span><span class="sxs-lookup"><span data-stu-id="96c58-122">string</span></span>| <span data-ttu-id="96c58-123">ID unique qui représente un élément de grille tarifaire donné (compteur par période de facturation)</span><span class="sxs-lookup"><span data-stu-id="96c58-123">The unique Id that represents a particular PriceSheet item (meter by billing period)</span></span>|
|<span data-ttu-id="96c58-124">billingPeriodId</span><span class="sxs-lookup"><span data-stu-id="96c58-124">billingPeriodId</span></span>| <span data-ttu-id="96c58-125">chaîne</span><span class="sxs-lookup"><span data-stu-id="96c58-125">string</span></span>| <span data-ttu-id="96c58-126">ID unique qui représente une période de facturation donnée</span><span class="sxs-lookup"><span data-stu-id="96c58-126">The unique Id that represents a particular Billing period</span></span>|
|<span data-ttu-id="96c58-127">meterId</span><span class="sxs-lookup"><span data-stu-id="96c58-127">meterId</span></span>| <span data-ttu-id="96c58-128">chaîne</span><span class="sxs-lookup"><span data-stu-id="96c58-128">string</span></span>| <span data-ttu-id="96c58-129">Identificateur du compteur.</span><span class="sxs-lookup"><span data-stu-id="96c58-129">The identifier for the meter.</span></span> <span data-ttu-id="96c58-130">Il peut être mappé au meterId d’utilisation.</span><span class="sxs-lookup"><span data-stu-id="96c58-130">It can be mapped to the usage meterId.</span></span>|
|<span data-ttu-id="96c58-131">meterName</span><span class="sxs-lookup"><span data-stu-id="96c58-131">meterName</span></span>| <span data-ttu-id="96c58-132">chaîne</span><span class="sxs-lookup"><span data-stu-id="96c58-132">string</span></span>| <span data-ttu-id="96c58-133">Nom du compteur</span><span class="sxs-lookup"><span data-stu-id="96c58-133">The meter name</span></span>|
|<span data-ttu-id="96c58-134">unitOfMeasure</span><span class="sxs-lookup"><span data-stu-id="96c58-134">unitOfMeasure</span></span>| <span data-ttu-id="96c58-135">chaîne</span><span class="sxs-lookup"><span data-stu-id="96c58-135">string</span></span>| <span data-ttu-id="96c58-136">Unité de mesure pour mesurer le service</span><span class="sxs-lookup"><span data-stu-id="96c58-136">The Unit of Measure for measuring the service</span></span>|
|<span data-ttu-id="96c58-137">includedQuantity</span><span class="sxs-lookup"><span data-stu-id="96c58-137">includedQuantity</span></span>| <span data-ttu-id="96c58-138">décimal</span><span class="sxs-lookup"><span data-stu-id="96c58-138">decimal</span></span>| <span data-ttu-id="96c58-139">Quantité incluse</span><span class="sxs-lookup"><span data-stu-id="96c58-139">Quantity that is included</span></span> |
|<span data-ttu-id="96c58-140">partNumber</span><span class="sxs-lookup"><span data-stu-id="96c58-140">partNumber</span></span>| <span data-ttu-id="96c58-141">chaîne</span><span class="sxs-lookup"><span data-stu-id="96c58-141">string</span></span>| <span data-ttu-id="96c58-142">Numéro de référence associé au compteur</span><span class="sxs-lookup"><span data-stu-id="96c58-142">The part number associated with the Meter</span></span>|
|<span data-ttu-id="96c58-143">unitPrice</span><span class="sxs-lookup"><span data-stu-id="96c58-143">unitPrice</span></span>| <span data-ttu-id="96c58-144">décimal</span><span class="sxs-lookup"><span data-stu-id="96c58-144">decimal</span></span>| <span data-ttu-id="96c58-145">Prix unitaire du compteur</span><span class="sxs-lookup"><span data-stu-id="96c58-145">The unit price for the meter</span></span>|
|<span data-ttu-id="96c58-146">currencyCode</span><span class="sxs-lookup"><span data-stu-id="96c58-146">currencyCode</span></span>| <span data-ttu-id="96c58-147">chaîne</span><span class="sxs-lookup"><span data-stu-id="96c58-147">string</span></span>| <span data-ttu-id="96c58-148">Code de devise du prix unitaire</span><span class="sxs-lookup"><span data-stu-id="96c58-148">The currency code for the unitPrice</span></span>|
<br/>
## <a name="see-also"></a><span data-ttu-id="96c58-149">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="96c58-149">See also</span></span>

* [<span data-ttu-id="96c58-150">API Périodes de facturation</span><span class="sxs-lookup"><span data-stu-id="96c58-150">Billing Periods API</span></span>](billing-enterprise-api-billing-periods.md)

* [<span data-ttu-id="96c58-151">API Détails de l’utilisation</span><span class="sxs-lookup"><span data-stu-id="96c58-151">Usage Detail API</span></span>](billing-enterprise-api-usage-detail.md)

* [<span data-ttu-id="96c58-152">API Solde et résumé</span><span class="sxs-lookup"><span data-stu-id="96c58-152">Balance and Summary API</span></span>](billing-enterprise-api-balance-summary.md)

* [<span data-ttu-id="96c58-153">API Frais de la Place de marché</span><span class="sxs-lookup"><span data-stu-id="96c58-153">Marketplace Store Charge API</span></span>](billing-enterprise-api-marketplace-storecharge.md)
