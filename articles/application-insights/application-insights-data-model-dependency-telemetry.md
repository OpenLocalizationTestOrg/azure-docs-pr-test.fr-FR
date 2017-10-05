---
title: "Modèle de données de télémétrie d’Azure Application Insights : télémétrie des dépendances | Microsoft Docs"
description: "Modèle de données Application Insights pour la télémétrie des dépendances"
services: application-insights
documentationcenter: .net
author: SergeyKanzhelev
manager: carmonm
ms.service: application-insights
ms.workload: TBD
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 04/17/2017
ms.author: bwren
ms.openlocfilehash: 2e97c3f951f46c32802aea543b93d5ab1bb76228
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="dependency-telemetry-application-insights-data-model"></a><span data-ttu-id="6f138-103">Télémétrie des dépendances : modèle de données Application Insights</span><span class="sxs-lookup"><span data-stu-id="6f138-103">Dependency telemetry: Application Insights data model</span></span>

<span data-ttu-id="6f138-104">La télémétrie des dépendances (dans [Application Insights](app-insights-overview.md)) représente une interaction du composant surveillé avec un composant distant tel que SQL ou un point de terminaison HTTP.</span><span class="sxs-lookup"><span data-stu-id="6f138-104">Dependency Telemetry (in [Application Insights](app-insights-overview.md)) represents an interaction of the monitored component with a remote component such as SQL or an HTTP endpoint.</span></span>

## <a name="name"></a><span data-ttu-id="6f138-105">Nom</span><span class="sxs-lookup"><span data-stu-id="6f138-105">Name</span></span>

<span data-ttu-id="6f138-106">Nom de la commande lancée par cet appel de dépendance.</span><span class="sxs-lookup"><span data-stu-id="6f138-106">Name of the command initiated with this dependency call.</span></span> <span data-ttu-id="6f138-107">Valeur de faible cardinalité.</span><span class="sxs-lookup"><span data-stu-id="6f138-107">Low cardinality value.</span></span> <span data-ttu-id="6f138-108">Exemples : nom de procédure stockée et modèle de chemin d’accès d’URL.</span><span class="sxs-lookup"><span data-stu-id="6f138-108">Examples are stored procedure name and URL path template.</span></span>

## <a name="id"></a><span data-ttu-id="6f138-109">ID</span><span class="sxs-lookup"><span data-stu-id="6f138-109">ID</span></span>

<span data-ttu-id="6f138-110">Identificateur d’une instance d’appel de dépendance.</span><span class="sxs-lookup"><span data-stu-id="6f138-110">Identifier of a dependency call instance.</span></span> <span data-ttu-id="6f138-111">Utilisé pour la corrélation avec l’élément de télémétrie de demande correspondant à cet appel de dépendance.</span><span class="sxs-lookup"><span data-stu-id="6f138-111">Used for correlation with the request telemetry item corresponding to this dependency call.</span></span> <span data-ttu-id="6f138-112">Pour plus d’informations, consultez la page relative à la [corrélation](application-insights-correlation.md).</span><span class="sxs-lookup"><span data-stu-id="6f138-112">For more information, see [correlation](application-insights-correlation.md) page.</span></span>

## <a name="data"></a><span data-ttu-id="6f138-113">Données</span><span class="sxs-lookup"><span data-stu-id="6f138-113">Data</span></span>

<span data-ttu-id="6f138-114">Commande lancée par cet appel de dépendance.</span><span class="sxs-lookup"><span data-stu-id="6f138-114">Command initiated by this dependency call.</span></span> <span data-ttu-id="6f138-115">Exemples : instruction SQL et URL HTTP avec tous les paramètres de requête.</span><span class="sxs-lookup"><span data-stu-id="6f138-115">Examples are SQL statement and HTTP URL with all query parameters.</span></span>

## <a name="type"></a><span data-ttu-id="6f138-116">Type</span><span class="sxs-lookup"><span data-stu-id="6f138-116">Type</span></span>

<span data-ttu-id="6f138-117">Nom du type de dépendance.</span><span class="sxs-lookup"><span data-stu-id="6f138-117">Dependency type name.</span></span> <span data-ttu-id="6f138-118">Valeur de faible cardinalité pour le regroupement logique de dépendances et l’interprétation d’autres champs comme commandName et resultCode.</span><span class="sxs-lookup"><span data-stu-id="6f138-118">Low cardinality value for logical grouping of dependencies and interpretation of other fields like commandName and resultCode.</span></span> <span data-ttu-id="6f138-119">Exemples : SQL, table Azure et HTTP.</span><span class="sxs-lookup"><span data-stu-id="6f138-119">Examples are SQL, Azure table, and HTTP.</span></span>

## <a name="target"></a><span data-ttu-id="6f138-120">Cible</span><span class="sxs-lookup"><span data-stu-id="6f138-120">Target</span></span>

<span data-ttu-id="6f138-121">Site cible d’un appel de dépendance.</span><span class="sxs-lookup"><span data-stu-id="6f138-121">Target site of a dependency call.</span></span> <span data-ttu-id="6f138-122">Exemples : nom de serveur, adresse d’hôte.</span><span class="sxs-lookup"><span data-stu-id="6f138-122">Examples are server name, host address.</span></span> <span data-ttu-id="6f138-123">Pour plus d’informations, consultez la page relative à la [corrélation](application-insights-correlation.md).</span><span class="sxs-lookup"><span data-stu-id="6f138-123">For more information, see [correlation](application-insights-correlation.md) page.</span></span>

## <a name="duration"></a><span data-ttu-id="6f138-124">Durée</span><span class="sxs-lookup"><span data-stu-id="6f138-124">Duration</span></span>

<span data-ttu-id="6f138-125">Durée de la demande au format : `DD.HH:MM:SS.MMMMMM`.</span><span class="sxs-lookup"><span data-stu-id="6f138-125">Request duration in format: `DD.HH:MM:SS.MMMMMM`.</span></span> <span data-ttu-id="6f138-126">Doit être inférieure à `1000` jours.</span><span class="sxs-lookup"><span data-stu-id="6f138-126">Must be less than `1000` days.</span></span>

## <a name="result-code"></a><span data-ttu-id="6f138-127">Code de résultat</span><span class="sxs-lookup"><span data-stu-id="6f138-127">Result code</span></span>

<span data-ttu-id="6f138-128">Code de résultat d’un appel de dépendance.</span><span class="sxs-lookup"><span data-stu-id="6f138-128">Result code of a dependency call.</span></span> <span data-ttu-id="6f138-129">Exemples : code d’erreur SQL et code d’état HTTP.</span><span class="sxs-lookup"><span data-stu-id="6f138-129">Examples are SQL error code and HTTP status code.</span></span>

## <a name="success"></a><span data-ttu-id="6f138-130">Succès</span><span class="sxs-lookup"><span data-stu-id="6f138-130">Success</span></span>

<span data-ttu-id="6f138-131">Indication de la réussite ou non d’un appel.</span><span class="sxs-lookup"><span data-stu-id="6f138-131">Indication of successful or unsuccessful call.</span></span>

## <a name="custom-properties"></a><span data-ttu-id="6f138-132">Propriétés personnalisées</span><span class="sxs-lookup"><span data-stu-id="6f138-132">Custom properties</span></span>

[!INCLUDE [application-insights-data-model-properties](../../includes/application-insights-data-model-properties.md)]

## <a name="custom-measurements"></a><span data-ttu-id="6f138-133">Mesures personnalisées</span><span class="sxs-lookup"><span data-stu-id="6f138-133">Custom measurements</span></span>

[!INCLUDE [application-insights-data-model-measurements](../../includes/application-insights-data-model-measurements.md)]


## <a name="next-steps"></a><span data-ttu-id="6f138-134">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6f138-134">Next steps</span></span>

- <span data-ttu-id="6f138-135">Configurez le suivi des dépendances pour [.NET](app-insights-asp-net-dependencies.md).</span><span class="sxs-lookup"><span data-stu-id="6f138-135">Set up dependency tracking for [.NET](app-insights-asp-net-dependencies.md).</span></span>
- <span data-ttu-id="6f138-136">Configurez le suivi des dépendances pour [Java](app-insights-java-agent.md).</span><span class="sxs-lookup"><span data-stu-id="6f138-136">Set up dependency tracking for [Java](app-insights-java-agent.md).</span></span>
- [<span data-ttu-id="6f138-137">Écrire des données de télémétrie des dépendances personnalisées</span><span class="sxs-lookup"><span data-stu-id="6f138-137">Write custom dependency telemetry</span></span>](app-insights-api-custom-events-metrics.md#trackdependency)
- <span data-ttu-id="6f138-138">Pour connaître les types et les modèles de données Application Insights, consultez [Modèle de données](application-insights-data-model.md).</span><span class="sxs-lookup"><span data-stu-id="6f138-138">See [data model](application-insights-data-model.md) for Application Insights types and data model.</span></span>
- <span data-ttu-id="6f138-139">Découvrez quelles [plateformes](app-insights-platforms.md) sont prises en charge par Application Insights.</span><span class="sxs-lookup"><span data-stu-id="6f138-139">Check out [platforms](app-insights-platforms.md) supported by Application Insights.</span></span>
