---
title: "aaaAzure modèle de données d’Application Insights télémétrie - télémétrie des dépendances | Documents Microsoft"
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
ms.openlocfilehash: cd5ab7c61d3498e4aa2a0aa0c8b0d106a92912e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="dependency-telemetry-application-insights-data-model"></a><span data-ttu-id="de72a-103">Télémétrie des dépendances : modèle de données Application Insights</span><span class="sxs-lookup"><span data-stu-id="de72a-103">Dependency telemetry: Application Insights data model</span></span>

<span data-ttu-id="de72a-104">Télémétrie des dépendances (dans [Application Insights](app-insights-overview.md)) représente une interaction de composant hello analysé avec un composant distant tel que SQL ou un point de terminaison HTTP.</span><span class="sxs-lookup"><span data-stu-id="de72a-104">Dependency Telemetry (in [Application Insights](app-insights-overview.md)) represents an interaction of hello monitored component with a remote component such as SQL or an HTTP endpoint.</span></span>

## <a name="name"></a><span data-ttu-id="de72a-105">Nom</span><span class="sxs-lookup"><span data-stu-id="de72a-105">Name</span></span>

<span data-ttu-id="de72a-106">Nom de la commande hello démarrée avec cet appel de dépendance.</span><span class="sxs-lookup"><span data-stu-id="de72a-106">Name of hello command initiated with this dependency call.</span></span> <span data-ttu-id="de72a-107">Valeur de faible cardinalité.</span><span class="sxs-lookup"><span data-stu-id="de72a-107">Low cardinality value.</span></span> <span data-ttu-id="de72a-108">Exemples : nom de procédure stockée et modèle de chemin d’accès d’URL.</span><span class="sxs-lookup"><span data-stu-id="de72a-108">Examples are stored procedure name and URL path template.</span></span>

## <a name="id"></a><span data-ttu-id="de72a-109">ID</span><span class="sxs-lookup"><span data-stu-id="de72a-109">ID</span></span>

<span data-ttu-id="de72a-110">Identificateur d’une instance d’appel de dépendance.</span><span class="sxs-lookup"><span data-stu-id="de72a-110">Identifier of a dependency call instance.</span></span> <span data-ttu-id="de72a-111">Utilisé pour la corrélation par élément de données de télémétrie hello demande correspondant toothis dépendance appel.</span><span class="sxs-lookup"><span data-stu-id="de72a-111">Used for correlation with hello request telemetry item corresponding toothis dependency call.</span></span> <span data-ttu-id="de72a-112">Pour plus d’informations, consultez la page relative à la [corrélation](application-insights-correlation.md).</span><span class="sxs-lookup"><span data-stu-id="de72a-112">For more information, see [correlation](application-insights-correlation.md) page.</span></span>

## <a name="data"></a><span data-ttu-id="de72a-113">Données</span><span class="sxs-lookup"><span data-stu-id="de72a-113">Data</span></span>

<span data-ttu-id="de72a-114">Commande lancée par cet appel de dépendance.</span><span class="sxs-lookup"><span data-stu-id="de72a-114">Command initiated by this dependency call.</span></span> <span data-ttu-id="de72a-115">Exemples : instruction SQL et URL HTTP avec tous les paramètres de requête.</span><span class="sxs-lookup"><span data-stu-id="de72a-115">Examples are SQL statement and HTTP URL with all query parameters.</span></span>

## <a name="type"></a><span data-ttu-id="de72a-116">Type</span><span class="sxs-lookup"><span data-stu-id="de72a-116">Type</span></span>

<span data-ttu-id="de72a-117">Nom du type de dépendance.</span><span class="sxs-lookup"><span data-stu-id="de72a-117">Dependency type name.</span></span> <span data-ttu-id="de72a-118">Valeur de faible cardinalité pour le regroupement logique de dépendances et l’interprétation d’autres champs comme commandName et resultCode.</span><span class="sxs-lookup"><span data-stu-id="de72a-118">Low cardinality value for logical grouping of dependencies and interpretation of other fields like commandName and resultCode.</span></span> <span data-ttu-id="de72a-119">Exemples : SQL, table Azure et HTTP.</span><span class="sxs-lookup"><span data-stu-id="de72a-119">Examples are SQL, Azure table, and HTTP.</span></span>

## <a name="target"></a><span data-ttu-id="de72a-120">Cible</span><span class="sxs-lookup"><span data-stu-id="de72a-120">Target</span></span>

<span data-ttu-id="de72a-121">Site cible d’un appel de dépendance.</span><span class="sxs-lookup"><span data-stu-id="de72a-121">Target site of a dependency call.</span></span> <span data-ttu-id="de72a-122">Exemples : nom de serveur, adresse d’hôte.</span><span class="sxs-lookup"><span data-stu-id="de72a-122">Examples are server name, host address.</span></span> <span data-ttu-id="de72a-123">Pour plus d’informations, consultez la page relative à la [corrélation](application-insights-correlation.md).</span><span class="sxs-lookup"><span data-stu-id="de72a-123">For more information, see [correlation](application-insights-correlation.md) page.</span></span>

## <a name="duration"></a><span data-ttu-id="de72a-124">Durée</span><span class="sxs-lookup"><span data-stu-id="de72a-124">Duration</span></span>

<span data-ttu-id="de72a-125">Durée de la demande au format : `DD.HH:MM:SS.MMMMMM`.</span><span class="sxs-lookup"><span data-stu-id="de72a-125">Request duration in format: `DD.HH:MM:SS.MMMMMM`.</span></span> <span data-ttu-id="de72a-126">Doit être inférieure à `1000` jours.</span><span class="sxs-lookup"><span data-stu-id="de72a-126">Must be less than `1000` days.</span></span>

## <a name="result-code"></a><span data-ttu-id="de72a-127">Code de résultat</span><span class="sxs-lookup"><span data-stu-id="de72a-127">Result code</span></span>

<span data-ttu-id="de72a-128">Code de résultat d’un appel de dépendance.</span><span class="sxs-lookup"><span data-stu-id="de72a-128">Result code of a dependency call.</span></span> <span data-ttu-id="de72a-129">Exemples : code d’erreur SQL et code d’état HTTP.</span><span class="sxs-lookup"><span data-stu-id="de72a-129">Examples are SQL error code and HTTP status code.</span></span>

## <a name="success"></a><span data-ttu-id="de72a-130">Succès</span><span class="sxs-lookup"><span data-stu-id="de72a-130">Success</span></span>

<span data-ttu-id="de72a-131">Indication de la réussite ou non d’un appel.</span><span class="sxs-lookup"><span data-stu-id="de72a-131">Indication of successful or unsuccessful call.</span></span>

## <a name="custom-properties"></a><span data-ttu-id="de72a-132">Propriétés personnalisées</span><span class="sxs-lookup"><span data-stu-id="de72a-132">Custom properties</span></span>

[!INCLUDE [application-insights-data-model-properties](../../includes/application-insights-data-model-properties.md)]

## <a name="custom-measurements"></a><span data-ttu-id="de72a-133">Mesures personnalisées</span><span class="sxs-lookup"><span data-stu-id="de72a-133">Custom measurements</span></span>

[!INCLUDE [application-insights-data-model-measurements](../../includes/application-insights-data-model-measurements.md)]


## <a name="next-steps"></a><span data-ttu-id="de72a-134">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="de72a-134">Next steps</span></span>

- <span data-ttu-id="de72a-135">Configurez le suivi des dépendances pour [.NET](app-insights-asp-net-dependencies.md).</span><span class="sxs-lookup"><span data-stu-id="de72a-135">Set up dependency tracking for [.NET](app-insights-asp-net-dependencies.md).</span></span>
- <span data-ttu-id="de72a-136">Configurez le suivi des dépendances pour [Java](app-insights-java-agent.md).</span><span class="sxs-lookup"><span data-stu-id="de72a-136">Set up dependency tracking for [Java](app-insights-java-agent.md).</span></span>
- [<span data-ttu-id="de72a-137">Écrire des données de télémétrie des dépendances personnalisées</span><span class="sxs-lookup"><span data-stu-id="de72a-137">Write custom dependency telemetry</span></span>](app-insights-api-custom-events-metrics.md#trackdependency)
- <span data-ttu-id="de72a-138">Pour connaître les types et les modèles de données Application Insights, consultez [Modèle de données](application-insights-data-model.md).</span><span class="sxs-lookup"><span data-stu-id="de72a-138">See [data model](application-insights-data-model.md) for Application Insights types and data model.</span></span>
- <span data-ttu-id="de72a-139">Découvrez quelles [plateformes](app-insights-platforms.md) sont prises en charge par Application Insights.</span><span class="sxs-lookup"><span data-stu-id="de72a-139">Check out [platforms](app-insights-platforms.md) supported by Application Insights.</span></span>
