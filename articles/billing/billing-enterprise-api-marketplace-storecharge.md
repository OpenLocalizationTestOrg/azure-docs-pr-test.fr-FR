---
title: "aaaAzure API d’entreprise facturation - frais Marketplace | Documents Microsoft"
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
ms.openlocfilehash: cdf2836b52df06a4bf5ed71a476fe33662c5363c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="reporting-apis-for-enterprise-customers---marketplace-store-charge"></a><span data-ttu-id="0562c-103">API de création de rapports pour les clients Enterprise - Marketplace Store Charge</span><span class="sxs-lookup"><span data-stu-id="0562c-103">Reporting APIs for Enterprise customers - Marketplace Store Charge</span></span>

<span data-ttu-id="0562c-104">Hello Marketplace magasin frais API retourne hello basée sur l’utilisation de marketplace frais répartition par jour pour hello spécifié la période de facturation ou les dates de début et de fin (frais d’une seule fois ne sont pas inclus).</span><span class="sxs-lookup"><span data-stu-id="0562c-104">hello Marketplace Store Charge API returns hello usage-based marketplace charges breakdown by day for hello specified Billing Period or start and end dates (one time fees are not included).</span></span>

##<a name="request"></a><span data-ttu-id="0562c-105">Demande</span><span class="sxs-lookup"><span data-stu-id="0562c-105">Request</span></span> 
<span data-ttu-id="0562c-106">Propriétés d’en-tête commun nécessitant toobe ajouté sont spécifiées [ici](billing-enterprise-api.md).</span><span class="sxs-lookup"><span data-stu-id="0562c-106">Common header properties that need toobe added are specified [here](billing-enterprise-api.md).</span></span> <span data-ttu-id="0562c-107">Si une période de facturation n’est pas spécifiée, puis les données de facturation actuel de hello période sont retournées.</span><span class="sxs-lookup"><span data-stu-id="0562c-107">If a billing period is not specified, then data for hello current billing period is returned.</span></span> <span data-ttu-id="0562c-108">Plages d’heure personnalisé peuvent être spécifiés avec le début de hello et les paramètres de date sont précis hello format AAAA-MM-JJ, hello maximale prise en charge est comprise entre 36 mois de fin.</span><span class="sxs-lookup"><span data-stu-id="0562c-108">Custom time ranges can be specified with hello start and end date parameters that are in hello format yyyy-MM-dd, hello maximum supported time range is 36 months.</span></span>  

|<span data-ttu-id="0562c-109">Méthode</span><span class="sxs-lookup"><span data-stu-id="0562c-109">Method</span></span> | <span data-ttu-id="0562c-110">URI de demande</span><span class="sxs-lookup"><span data-stu-id="0562c-110">Request URI</span></span>|
|-|-|
|<span data-ttu-id="0562c-111">GET</span><span class="sxs-lookup"><span data-stu-id="0562c-111">GET</span></span>|<span data-ttu-id="0562c-112">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/marketplacecharges</span><span class="sxs-lookup"><span data-stu-id="0562c-112">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/marketplacecharges</span></span>|
|<span data-ttu-id="0562c-113">GET</span><span class="sxs-lookup"><span data-stu-id="0562c-113">GET</span></span>|<span data-ttu-id="0562c-114">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingPeriods/{billingPeriod}/marketplacecharges</span><span class="sxs-lookup"><span data-stu-id="0562c-114">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingPeriods/{billingPeriod}/marketplacecharges</span></span>|
|<span data-ttu-id="0562c-115">GET</span><span class="sxs-lookup"><span data-stu-id="0562c-115">GET</span></span>|<span data-ttu-id="0562c-116">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/marketplacechargesbycustomdate?startTime=2017-01-01&endTime=2017-01-10</span><span class="sxs-lookup"><span data-stu-id="0562c-116">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/marketplacechargesbycustomdate?startTime=2017-01-01&endTime=2017-01-10</span></span>|

> [!Note]
> <span data-ttu-id="0562c-117">version d’évaluation hello toouse de l’API, remplacez v2 v1 Bonjour au-dessus des URL.</span><span class="sxs-lookup"><span data-stu-id="0562c-117">toouse hello preview version of API, replace v2 with v1 in hello above URL.</span></span>
>

## <a name="response"></a><span data-ttu-id="0562c-118">Réponse</span><span class="sxs-lookup"><span data-stu-id="0562c-118">Response</span></span>
 
    
        [
            {
                "id": "id",
                "subscriptionGuid": "00000000-0000-0000-0000-000000000000",
                "subscriptionName": "subName",
                "meterId": "2core",
                "usageStartDate": "2015-09-17T00:00:00Z",
                "usageEndDate": "2015-09-17T23:59:59Z",
                "offerName": "Virtual LoadMaster™ (VLM) for Azure",
                "resourceGroup": "Res group",
                "instanceId": "id",
                "additionalInfo": "{\"ImageType\":null,\"ServiceType\":\"Medium\"}",
                "tags": "",
                "orderNumber": "order",
                "unitOfMeasure": "",
                "costCenter": "100",
                "accountId": 100,
                "accountName": "Account Name",
                "accountOwnerId": "account@live.com",
                "departmentId": 101,
                "departmentName": "Department 1",
                "publisherName": "Publisher 1",
                "planName": "Plan name",
                "consumedQuantity": 1.15,
                "resourceRate": 0.1,
                "extendedCost": 1.11
            },
            ...
        ]
    

<span data-ttu-id="0562c-119">**Définitions des propriétés de réponse**</span><span class="sxs-lookup"><span data-stu-id="0562c-119">**Response property definitions**</span></span>

|<span data-ttu-id="0562c-120">Nom de la propriété</span><span class="sxs-lookup"><span data-stu-id="0562c-120">Property Name</span></span>| <span data-ttu-id="0562c-121">Type</span><span class="sxs-lookup"><span data-stu-id="0562c-121">Type</span></span>| <span data-ttu-id="0562c-122">Description</span><span class="sxs-lookup"><span data-stu-id="0562c-122">Description</span></span>
|-|-|-|
|<span data-ttu-id="0562c-123">id</span><span class="sxs-lookup"><span data-stu-id="0562c-123">id</span></span>|<span data-ttu-id="0562c-124">string</span><span class="sxs-lookup"><span data-stu-id="0562c-124">string</span></span>|<span data-ttu-id="0562c-125">Id unique de l’élément de frais marketplace hello</span><span class="sxs-lookup"><span data-stu-id="0562c-125">Unique Id for hello marketplace charge item</span></span>|
|<span data-ttu-id="0562c-126">subscriptionGuid</span><span class="sxs-lookup"><span data-stu-id="0562c-126">subscriptionGuid</span></span>|<span data-ttu-id="0562c-127">Guid</span><span class="sxs-lookup"><span data-stu-id="0562c-127">Guid</span></span>|<span data-ttu-id="0562c-128">Hello Guid de l’abonnement</span><span class="sxs-lookup"><span data-stu-id="0562c-128">hello Subscription Guid</span></span>|
|<span data-ttu-id="0562c-129">subscriptionName</span><span class="sxs-lookup"><span data-stu-id="0562c-129">subscriptionName</span></span>|<span data-ttu-id="0562c-130">string</span><span class="sxs-lookup"><span data-stu-id="0562c-130">string</span></span>|<span data-ttu-id="0562c-131">Nom de l’abonnement de Hello</span><span class="sxs-lookup"><span data-stu-id="0562c-131">hello Subscription Name</span></span>|
|<span data-ttu-id="0562c-132">meterId</span><span class="sxs-lookup"><span data-stu-id="0562c-132">meterId</span></span>|<span data-ttu-id="0562c-133">string</span><span class="sxs-lookup"><span data-stu-id="0562c-133">string</span></span>|<span data-ttu-id="0562c-134">ID de hello émis compteur</span><span class="sxs-lookup"><span data-stu-id="0562c-134">Id for hello emitted Meter</span></span>|
|<span data-ttu-id="0562c-135">usageStartDate</span><span class="sxs-lookup"><span data-stu-id="0562c-135">usageStartDate</span></span>|<span data-ttu-id="0562c-136">DateTime</span><span class="sxs-lookup"><span data-stu-id="0562c-136">DateTime</span></span>|<span data-ttu-id="0562c-137">Heure de début de l’enregistrement de l’utilisation de hello</span><span class="sxs-lookup"><span data-stu-id="0562c-137">Start time for hello usage record</span></span>|
|<span data-ttu-id="0562c-138">usageEndDate</span><span class="sxs-lookup"><span data-stu-id="0562c-138">usageEndDate</span></span>|<span data-ttu-id="0562c-139">DateTime</span><span class="sxs-lookup"><span data-stu-id="0562c-139">DateTime</span></span>|<span data-ttu-id="0562c-140">Heure de fin de l’enregistrement de l’utilisation de hello</span><span class="sxs-lookup"><span data-stu-id="0562c-140">End time for hello usage record</span></span>|
|<span data-ttu-id="0562c-141">offerName</span><span class="sxs-lookup"><span data-stu-id="0562c-141">offerName</span></span>|<span data-ttu-id="0562c-142">string</span><span class="sxs-lookup"><span data-stu-id="0562c-142">string</span></span>|<span data-ttu-id="0562c-143">nom de l’offre Hello</span><span class="sxs-lookup"><span data-stu-id="0562c-143">hello Offer name</span></span>|
|<span data-ttu-id="0562c-144">resourceGroup</span><span class="sxs-lookup"><span data-stu-id="0562c-144">resourceGroup</span></span>|<span data-ttu-id="0562c-145">string</span><span class="sxs-lookup"><span data-stu-id="0562c-145">string</span></span>|<span data-ttu-id="0562c-146">ressource de Hello groupe</span><span class="sxs-lookup"><span data-stu-id="0562c-146">hello resource Group</span></span>|
|<span data-ttu-id="0562c-147">instanceId</span><span class="sxs-lookup"><span data-stu-id="0562c-147">instanceId</span></span>|<span data-ttu-id="0562c-148">string</span><span class="sxs-lookup"><span data-stu-id="0562c-148">string</span></span>|<span data-ttu-id="0562c-149">ID de l’instance</span><span class="sxs-lookup"><span data-stu-id="0562c-149">Instance Id</span></span>|
|<span data-ttu-id="0562c-150">additionalInfo</span><span class="sxs-lookup"><span data-stu-id="0562c-150">additionalInfo</span></span>|<span data-ttu-id="0562c-151">string</span><span class="sxs-lookup"><span data-stu-id="0562c-151">string</span></span>|<span data-ttu-id="0562c-152">Chaîne JSON avec informations supplémentaires</span><span class="sxs-lookup"><span data-stu-id="0562c-152">Additional info JSON string</span></span>|
|<span data-ttu-id="0562c-153">tags</span><span class="sxs-lookup"><span data-stu-id="0562c-153">tags</span></span>|<span data-ttu-id="0562c-154">string</span><span class="sxs-lookup"><span data-stu-id="0562c-154">string</span></span>|<span data-ttu-id="0562c-155">Chaîne JSON de balise</span><span class="sxs-lookup"><span data-stu-id="0562c-155">Tag JSON string</span></span>|
|<span data-ttu-id="0562c-156">orderNumber</span><span class="sxs-lookup"><span data-stu-id="0562c-156">orderNumber</span></span>|<span data-ttu-id="0562c-157">string</span><span class="sxs-lookup"><span data-stu-id="0562c-157">string</span></span>|<span data-ttu-id="0562c-158">numéro de commande Hello</span><span class="sxs-lookup"><span data-stu-id="0562c-158">hello order number</span></span>|
|<span data-ttu-id="0562c-159">unitOfMeasure</span><span class="sxs-lookup"><span data-stu-id="0562c-159">unitOfMeasure</span></span>|<span data-ttu-id="0562c-160">string</span><span class="sxs-lookup"><span data-stu-id="0562c-160">string</span></span>|<span data-ttu-id="0562c-161">Unité de mesure pour le compteur de hello</span><span class="sxs-lookup"><span data-stu-id="0562c-161">Unit of measure for hello meter</span></span>|
|<span data-ttu-id="0562c-162">costCenter</span><span class="sxs-lookup"><span data-stu-id="0562c-162">costCenter</span></span>|<span data-ttu-id="0562c-163">string</span><span class="sxs-lookup"><span data-stu-id="0562c-163">string</span></span>|<span data-ttu-id="0562c-164">Centre de coût de Hello</span><span class="sxs-lookup"><span data-stu-id="0562c-164">hello cost center</span></span>|
|<span data-ttu-id="0562c-165">accountId</span><span class="sxs-lookup"><span data-stu-id="0562c-165">accountId</span></span>|<span data-ttu-id="0562c-166">int</span><span class="sxs-lookup"><span data-stu-id="0562c-166">int</span></span>|<span data-ttu-id="0562c-167">compte Hello Id</span><span class="sxs-lookup"><span data-stu-id="0562c-167">hello account Id</span></span>|
|<span data-ttu-id="0562c-168">accountName</span><span class="sxs-lookup"><span data-stu-id="0562c-168">accountName</span></span>|<span data-ttu-id="0562c-169">string</span><span class="sxs-lookup"><span data-stu-id="0562c-169">string</span></span> |<span data-ttu-id="0562c-170">Nom du compte de Hello</span><span class="sxs-lookup"><span data-stu-id="0562c-170">hello Account Name</span></span>|
|<span data-ttu-id="0562c-171">accountOwnerId</span><span class="sxs-lookup"><span data-stu-id="0562c-171">accountOwnerId</span></span>|<span data-ttu-id="0562c-172">string</span><span class="sxs-lookup"><span data-stu-id="0562c-172">string</span></span>|<span data-ttu-id="0562c-173">Hello Id de propriétaire de compte</span><span class="sxs-lookup"><span data-stu-id="0562c-173">hello Account Owner Id</span></span>|
|<span data-ttu-id="0562c-174">departmentId</span><span class="sxs-lookup"><span data-stu-id="0562c-174">departmentId</span></span>|<span data-ttu-id="0562c-175">int</span><span class="sxs-lookup"><span data-stu-id="0562c-175">int</span></span>|<span data-ttu-id="0562c-176">service Hello Id</span><span class="sxs-lookup"><span data-stu-id="0562c-176">hello department Id</span></span>|
|<span data-ttu-id="0562c-177">departmentName</span><span class="sxs-lookup"><span data-stu-id="0562c-177">departmentName</span></span>|<span data-ttu-id="0562c-178">string</span><span class="sxs-lookup"><span data-stu-id="0562c-178">string</span></span>|<span data-ttu-id="0562c-179">nom du service informatique Hello</span><span class="sxs-lookup"><span data-stu-id="0562c-179">hello department name</span></span>|
|<span data-ttu-id="0562c-180">publisherName</span><span class="sxs-lookup"><span data-stu-id="0562c-180">publisherName</span></span>|<span data-ttu-id="0562c-181">string</span><span class="sxs-lookup"><span data-stu-id="0562c-181">string</span></span>|<span data-ttu-id="0562c-182">nom de l’éditeur Hello</span><span class="sxs-lookup"><span data-stu-id="0562c-182">hello publisher name</span></span>|
|<span data-ttu-id="0562c-183">planName</span><span class="sxs-lookup"><span data-stu-id="0562c-183">planName</span></span>|<span data-ttu-id="0562c-184">string</span><span class="sxs-lookup"><span data-stu-id="0562c-184">string</span></span>|<span data-ttu-id="0562c-185">nom du Plan Hello</span><span class="sxs-lookup"><span data-stu-id="0562c-185">hello Plan name</span></span>|
|<span data-ttu-id="0562c-186">consumedQuantity</span><span class="sxs-lookup"><span data-stu-id="0562c-186">consumedQuantity</span></span>|<span data-ttu-id="0562c-187">Décimal</span><span class="sxs-lookup"><span data-stu-id="0562c-187">decimal</span></span>|<span data-ttu-id="0562c-188">Quantité consommée pendant cette période</span><span class="sxs-lookup"><span data-stu-id="0562c-188">Consumed Quantity during this time period</span></span>|
|<span data-ttu-id="0562c-189">resourceRate</span><span class="sxs-lookup"><span data-stu-id="0562c-189">resourceRate</span></span>|<span data-ttu-id="0562c-190">Décimal</span><span class="sxs-lookup"><span data-stu-id="0562c-190">decimal</span></span>|<span data-ttu-id="0562c-191">Prix unitaire pour le compteur de hello</span><span class="sxs-lookup"><span data-stu-id="0562c-191">Unit price for hello meter</span></span>|
|<span data-ttu-id="0562c-192">extendedCost</span><span class="sxs-lookup"><span data-stu-id="0562c-192">extendedCost</span></span>|<span data-ttu-id="0562c-193">Décimal</span><span class="sxs-lookup"><span data-stu-id="0562c-193">decimal</span></span>|<span data-ttu-id="0562c-194">Estimation des frais en fonction de la quantité consommée et du coût global</span><span class="sxs-lookup"><span data-stu-id="0562c-194">Estimated charge based on Consumed Quantity and Extended cost</span></span>|
<br/>
## <a name="see-also"></a><span data-ttu-id="0562c-195">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="0562c-195">See also</span></span>

* [<span data-ttu-id="0562c-196">API Périodes de facturation</span><span class="sxs-lookup"><span data-stu-id="0562c-196">Billing Periods API</span></span>](billing-enterprise-api-billing-periods.md)

* [<span data-ttu-id="0562c-197">API Détails de l’utilisation</span><span class="sxs-lookup"><span data-stu-id="0562c-197">Usage Detail API</span></span>](billing-enterprise-api-usage-detail.md) 

* [<span data-ttu-id="0562c-198">API Solde et résumé</span><span class="sxs-lookup"><span data-stu-id="0562c-198">Balance and Summary API</span></span>](billing-enterprise-api-balance-summary.md)

* [<span data-ttu-id="0562c-199">API Grille tarifaire</span><span class="sxs-lookup"><span data-stu-id="0562c-199">Price Sheet API</span></span>](billing-enterprise-api-pricesheet.md)