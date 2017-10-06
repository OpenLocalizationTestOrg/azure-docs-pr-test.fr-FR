---
title: aaaAzure de facturation des API Enterprise | Documents Microsoft
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
ms.openlocfilehash: 017cecc57ad6bdeb402b5d9d57fc95df9b033a42
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-reporting-apis-for-enterprise-customers"></a><span data-ttu-id="7688c-103">Vue d’ensemble des API de création de rapports pour les clients Enterprise</span><span class="sxs-lookup"><span data-stu-id="7688c-103">Overview of Reporting APIs for Enterprise customers</span></span>
<span data-ttu-id="7688c-104">Hello Reporting API permettent la consommation de Azure d’entreprise clients tooprogrammatically par extraction de données et les données de facturation dans les outils d’analyse de données par défaut.</span><span class="sxs-lookup"><span data-stu-id="7688c-104">hello Reporting APIs enable Enterprise Azure customers tooprogrammatically pull consumption and billing data into preferred data analysis tools.</span></span> 

## <a name="enabling-data-access-toohello-api"></a><span data-ttu-id="7688c-105">L’activation des API de toohello d’accès aux données</span><span class="sxs-lookup"><span data-stu-id="7688c-105">Enabling data access toohello API</span></span>
* <span data-ttu-id="7688c-106">**Générer ou de récupérer la clé d’API de hello** API de création de rapports - journal toohello Enterprise portal et suivez hello didacticiel sous aide -.</span><span class="sxs-lookup"><span data-stu-id="7688c-106">**Generate or retrieve hello API key** - Log in toohello Enterprise portal and follow hello tutorial under Help - Reporting APIs.</span></span> <span data-ttu-id="7688c-107">première section de Hello sous cet article d’aide explique comment la clé hello API toogenerate ou récupérer pour hello spécifiée d’inscription.</span><span class="sxs-lookup"><span data-stu-id="7688c-107">hello first section under this help article explains how toogenerate or retrieve hello API key for hello specified enrollment.</span></span>
* <span data-ttu-id="7688c-108">**Passe des clés Bonjour API** -clé de hello API doit toobe passé pour chaque appel d’authentification et autorisation.</span><span class="sxs-lookup"><span data-stu-id="7688c-108">**Passing keys in hello API** - hello API key needs toobe passed for each call for Authentication and Authorization.</span></span> <span data-ttu-id="7688c-109">la propriété suivante Hello doit toobe toohello HTTP en-têtes</span><span class="sxs-lookup"><span data-stu-id="7688c-109">hello following property needs toobe toohello HTTP headers</span></span>

|<span data-ttu-id="7688c-110">Clé d’en-tête de demande</span><span class="sxs-lookup"><span data-stu-id="7688c-110">Request Header Key</span></span> | <span data-ttu-id="7688c-111">Valeur</span><span class="sxs-lookup"><span data-stu-id="7688c-111">Value</span></span>|
|-|-|
|<span data-ttu-id="7688c-112">Autorisation</span><span class="sxs-lookup"><span data-stu-id="7688c-112">Authorization</span></span>| <span data-ttu-id="7688c-113">Spécifiez la valeur de hello dans ce format : **PORTEUR {API_KEY}**</span><span class="sxs-lookup"><span data-stu-id="7688c-113">Specify hello value in this format: **bearer {API_KEY}**</span></span> <br/> <span data-ttu-id="7688c-114">Exemple : porteur eyr... 09</span><span class="sxs-lookup"><span data-stu-id="7688c-114">Example: bearer eyr....09</span></span>|

## <a name="consumption-apis"></a><span data-ttu-id="7688c-115">API de consommation</span><span class="sxs-lookup"><span data-stu-id="7688c-115">Consumption APIs</span></span>
<span data-ttu-id="7688c-116">Il existe un point de terminaison Swagger [ici](https://consumption.azure.com/swagger/ui/index) pour hello API décrites dessous de laquelle doit activer les introspection facile de hello API et du client de toogenerate hello capacité kits de développement logiciel à l’aide de [AutoRest](https://github.com/Azure/AutoRest) ou [ Swagger CodeGen](http://swagger.io/swagger-codegen/).</span><span class="sxs-lookup"><span data-stu-id="7688c-116">A Swagger endpoint is available [here](https://consumption.azure.com/swagger/ui/index) for hello APIs described below which should enable easy introspection of hello API and hello ability toogenerate client SDKs using [AutoRest](https://github.com/Azure/AutoRest) or [Swagger CodeGen](http://swagger.io/swagger-codegen/).</span></span> <span data-ttu-id="7688c-117">À compter du 1er mai 2014, ces données sont disponibles via cette API.</span><span class="sxs-lookup"><span data-stu-id="7688c-117">Data beginning May 1, 2014 is available through this API.</span></span> 

* <span data-ttu-id="7688c-118">**Solde et résumé** - hello [solde et API Résumé](billing-enterprise-api-balance-summary.md) offre un résumé de tous les mois d’informations sur les soldes, nouveaux achats, des frais de service Azure Marketplace, ajustements et frais de dépassement.</span><span class="sxs-lookup"><span data-stu-id="7688c-118">**Balance and Summary** - hello [Balance and Summary API](billing-enterprise-api-balance-summary.md) offers a monthly summary of information on balances, new purchases, Azure Marketplace service charges, adjustments and overage charges.</span></span>

* <span data-ttu-id="7688c-119">**Détails d’utilisation** - hello [API des détails d’utilisation](billing-enterprise-api-usage-detail.md) offre une analyse quotidienne des quantités consommées et frais estimés par une inscription.</span><span class="sxs-lookup"><span data-stu-id="7688c-119">**Usage Details** - hello [Usage Detail API](billing-enterprise-api-usage-detail.md) offers a daily breakdown of consumed quantities and estimated charges by an Enrollment.</span></span> <span data-ttu-id="7688c-120">résultat de Hello inclut également des informations sur les instances, les compteurs et les services.</span><span class="sxs-lookup"><span data-stu-id="7688c-120">hello result also includes information on instances, meters and departments.</span></span> <span data-ttu-id="7688c-121">Hello API peut être interrogée par période de facturation ou par un début spécifiée et la date de fin.</span><span class="sxs-lookup"><span data-stu-id="7688c-121">hello API can be queried by Billing period or by a specified start and end date.</span></span> 

* <span data-ttu-id="7688c-122">**Les frais Marketplace magasin** - hello [API du magasin de frais Marketplace](billing-enterprise-api-marketplace-storecharge.md) retourne répartition de frais hello basée sur l’utilisation de marketplace par jour pour hello spécifié la période de facturation ou les dates de début et de fin (frais d’une seule fois ne sont pas inclus) .</span><span class="sxs-lookup"><span data-stu-id="7688c-122">**Marketplace Store Charge** - hello [Marketplace Store Charge API](billing-enterprise-api-marketplace-storecharge.md) returns hello usage-based marketplace charges breakdown by day for hello specified Billing Period or start and end dates (one time fees are not included).</span></span>

* <span data-ttu-id="7688c-123">**Table de tarification** - hello [API de feuille de prix](billing-enterprise-api-pricesheet.md) fournit les taux applicable hello pour chacun des compteurs pour hello donné d’inscription et la période de facturation.</span><span class="sxs-lookup"><span data-stu-id="7688c-123">**Price Sheet** - hello [Price Sheet API](billing-enterprise-api-pricesheet.md) provides hello applicable rate for each Meter for hello given Enrollment and Billing Period.</span></span> 

## <a name="helper-apis"></a><span data-ttu-id="7688c-124">API d’assistance</span><span class="sxs-lookup"><span data-stu-id="7688c-124">Helper APIs</span></span>
 <span data-ttu-id="7688c-125">**Liste des périodes de facturation** - hello [API de périodes de facturation](billing-enterprise-api-billing-periods.md) retourne une liste de facturation des périodes qui ont des données de consommation pour hello spécifié d’inscription dans l’ordre chronologique inverse.</span><span class="sxs-lookup"><span data-stu-id="7688c-125">**List Billing Periods** - hello [Billing Periods API](billing-enterprise-api-billing-periods.md) returns a list of billing periods that have consumption data for hello specified Enrollment in reverse chronological order.</span></span> <span data-ttu-id="7688c-126">Chaque période contient une propriété pointant itinéraire d’API toohello pour hello quatre ensembles de données - BalanceSummary, UsageDetails, frais Marketplace et table de tarification.</span><span class="sxs-lookup"><span data-stu-id="7688c-126">Each Period contains a property pointing toohello API route for hello four sets of data - BalanceSummary, UsageDetails, Marketplace Charges, and Price Sheet.</span></span>


## <a name="api-response-codes"></a><span data-ttu-id="7688c-127">Codes de réponse HTTP</span><span class="sxs-lookup"><span data-stu-id="7688c-127">API Response Codes</span></span>  
|<span data-ttu-id="7688c-128">Code du statut de réponse</span><span class="sxs-lookup"><span data-stu-id="7688c-128">Response Status Code</span></span>|<span data-ttu-id="7688c-129">Message</span><span class="sxs-lookup"><span data-stu-id="7688c-129">Message</span></span>|<span data-ttu-id="7688c-130">Description</span><span class="sxs-lookup"><span data-stu-id="7688c-130">Description</span></span>|
|-|-|-|
|<span data-ttu-id="7688c-131">200</span><span class="sxs-lookup"><span data-stu-id="7688c-131">200</span></span>| <span data-ttu-id="7688c-132">OK</span><span class="sxs-lookup"><span data-stu-id="7688c-132">OK</span></span>|<span data-ttu-id="7688c-133">Aucune erreur</span><span class="sxs-lookup"><span data-stu-id="7688c-133">No error</span></span>|
|<span data-ttu-id="7688c-134">401</span><span class="sxs-lookup"><span data-stu-id="7688c-134">401</span></span>| <span data-ttu-id="7688c-135">Non autorisé</span><span class="sxs-lookup"><span data-stu-id="7688c-135">Unauthorized</span></span>| <span data-ttu-id="7688c-136">Clé API introuvable, non valide, expirée, etc.</span><span class="sxs-lookup"><span data-stu-id="7688c-136">API Key not found, Invalid, Expired etc.</span></span>|
|<span data-ttu-id="7688c-137">404</span><span class="sxs-lookup"><span data-stu-id="7688c-137">404</span></span>| <span data-ttu-id="7688c-138">Non disponible</span><span class="sxs-lookup"><span data-stu-id="7688c-138">Unavailable</span></span>| <span data-ttu-id="7688c-139">Point de terminaison de rapport introuvable</span><span class="sxs-lookup"><span data-stu-id="7688c-139">Report endpoint not found</span></span>|
|<span data-ttu-id="7688c-140">400</span><span class="sxs-lookup"><span data-stu-id="7688c-140">400</span></span>| <span data-ttu-id="7688c-141">Demande incorrecte</span><span class="sxs-lookup"><span data-stu-id="7688c-141">Bad Request</span></span>| <span data-ttu-id="7688c-142">Paramètres non valides : plages de dates, nombres de Contrats Entreprise (EA), etc.</span><span class="sxs-lookup"><span data-stu-id="7688c-142">Invalid params – Date ranges, EA numbers etc.</span></span>|
|<span data-ttu-id="7688c-143">500</span><span class="sxs-lookup"><span data-stu-id="7688c-143">500</span></span>| <span data-ttu-id="7688c-144">Erreur de serveur</span><span class="sxs-lookup"><span data-stu-id="7688c-144">Server Error</span></span>| <span data-ttu-id="7688c-145">Erreur inattendue lors du traitement de la demande</span><span class="sxs-lookup"><span data-stu-id="7688c-145">Unexoected error processing request</span></span>| 









