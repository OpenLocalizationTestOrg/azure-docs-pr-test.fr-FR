---
title: "aaaAzure modèle de données d’Application Insights télémétrie - métrique de télémétrie | Documents Microsoft"
description: "Modèle de données Application Insights pour la télémétrie des mesures"
services: application-insights
documentationcenter: .net
author: SergeyKanzhelev
manager: carmonm
ms.service: application-insights
ms.workload: TBD
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 04/25/2017
ms.author: bwren
ms.openlocfilehash: 005e218a8451007458185f1e457a20cee93fa630
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="metric-telemetry-application-insights-data-model"></a><span data-ttu-id="f0338-103">Télémétrie des mesure : modèle de données Application Insights</span><span class="sxs-lookup"><span data-stu-id="f0338-103">Metric telemetry: Application Insights data model</span></span>

<span data-ttu-id="f0338-104">Deux types de télémétrie des mesures sont prises en charge par [Application Insights](app-insights-overview.md) : la mesure unique et la mesure pré-agrégée.</span><span class="sxs-lookup"><span data-stu-id="f0338-104">There are two types of metric telemetry supported by [Application Insights](app-insights-overview.md): single measurement and pre-aggregated metric.</span></span> <span data-ttu-id="f0338-105">La mesure unique consiste simplement dans un nom et une valeur.</span><span class="sxs-lookup"><span data-stu-id="f0338-105">Single measurement is just a name and value.</span></span> <span data-ttu-id="f0338-106">Métrique agrégée au préalable spécifie la valeur minimale et maximale de la métrique de hello dans l’intervalle d’agrégation de hello et écart de celui-ci.</span><span class="sxs-lookup"><span data-stu-id="f0338-106">Pre-aggregated metric specifies minimum and maximum value of hello metric in hello aggregation interval and standard deviation of it.</span></span>

<span data-ttu-id="f0338-107">La télémétrie des mesures pré-agrégées suppose que cette période d’agrégation est d’une minute.</span><span class="sxs-lookup"><span data-stu-id="f0338-107">Pre-aggregated metric telemetry assumes that aggregation period was one minute.</span></span>

<span data-ttu-id="f0338-108">Plusieurs noms de mesure connus sont pris en charge par Application Insights.</span><span class="sxs-lookup"><span data-stu-id="f0338-108">There are several well-known metric names supported by Application Insights.</span></span> 

<span data-ttu-id="f0338-109">Système de représentation des mesures et compteurs de processus :</span><span class="sxs-lookup"><span data-stu-id="f0338-109">Metric representing system and process counters:</span></span>

| <span data-ttu-id="f0338-110">**Nom .NET**</span><span class="sxs-lookup"><span data-stu-id="f0338-110">**.NET name**</span></span>             | <span data-ttu-id="f0338-111">**Nom sans plateforme spécifiée**</span><span class="sxs-lookup"><span data-stu-id="f0338-111">**Platform agnostic name**</span></span> | <span data-ttu-id="f0338-112">**Nom d’API REST**</span><span class="sxs-lookup"><span data-stu-id="f0338-112">**REST API name**</span></span> | <span data-ttu-id="f0338-113">**Description**</span><span class="sxs-lookup"><span data-stu-id="f0338-113">**Description**</span></span>
| ------------------------- | -------------------------- | ----------------- | ---------------- 
| `\Processor(_Total)\% Processor Time` | <span data-ttu-id="f0338-114">Travail en cours...</span><span class="sxs-lookup"><span data-stu-id="f0338-114">Work in progress...</span></span> | [<span data-ttu-id="f0338-115">processorCpuPercentage</span><span class="sxs-lookup"><span data-stu-id="f0338-115">processorCpuPercentage</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FprocessorCpuPercentage) | <span data-ttu-id="f0338-116">nombre total de processeurs de l’ordinateur</span><span class="sxs-lookup"><span data-stu-id="f0338-116">total machine CPU</span></span>
| `\Memory\Available Bytes`                 | <span data-ttu-id="f0338-117">Travail en cours...</span><span class="sxs-lookup"><span data-stu-id="f0338-117">Work in progress...</span></span> | [<span data-ttu-id="f0338-118">memoryAvailableBytes</span><span class="sxs-lookup"><span data-stu-id="f0338-118">memoryAvailableBytes</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FmemoryAvailableBytes) | <span data-ttu-id="f0338-119">mémoire disponible sur le disque</span><span class="sxs-lookup"><span data-stu-id="f0338-119">memory available on disk</span></span>
| `\Process(??APP_WIN32_PROC??)\% Processor Time` | <span data-ttu-id="f0338-120">Travail en cours...</span><span class="sxs-lookup"><span data-stu-id="f0338-120">Work in progress...</span></span> | [<span data-ttu-id="f0338-121">processCpuPercentage</span><span class="sxs-lookup"><span data-stu-id="f0338-121">processCpuPercentage</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FprocessCpuPercentage) | <span data-ttu-id="f0338-122">UC du processus hello hébergeant l’application hello</span><span class="sxs-lookup"><span data-stu-id="f0338-122">CPU of hello process hosting hello application</span></span>
| `\Process(??APP_WIN32_PROC??)\Private Bytes`      | <span data-ttu-id="f0338-123">Travail en cours...</span><span class="sxs-lookup"><span data-stu-id="f0338-123">Work in progress...</span></span> | [<span data-ttu-id="f0338-124">processPrivateBytes</span><span class="sxs-lookup"><span data-stu-id="f0338-124">processPrivateBytes</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FprocessPrivateBytes) | <span data-ttu-id="f0338-125">mémoire utilisée par les processus hello hébergeant l’application hello</span><span class="sxs-lookup"><span data-stu-id="f0338-125">memory used by hello process hosting hello application</span></span>
| `\Process(??APP_WIN32_PROC??)\IO Data Bytes/sec` | <span data-ttu-id="f0338-126">Travail en cours...</span><span class="sxs-lookup"><span data-stu-id="f0338-126">Work in progress...</span></span> | [<span data-ttu-id="f0338-127">processIOBytesPerSecond</span><span class="sxs-lookup"><span data-stu-id="f0338-127">processIOBytesPerSecond</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FprocessIOBytesPerSecond) | <span data-ttu-id="f0338-128">taux d’opérations d’e/s s’exécute par processus hébergeant l’application hello</span><span class="sxs-lookup"><span data-stu-id="f0338-128">rate of I/O operations runs by process hosting hello application</span></span>
| `\ASP.NET Applications(??APP_W3SVC_PROC??)\Requests/Sec`             | <span data-ttu-id="f0338-129">Travail en cours...</span><span class="sxs-lookup"><span data-stu-id="f0338-129">Work in progress...</span></span> | [<span data-ttu-id="f0338-130">requestsPerSecond</span><span class="sxs-lookup"><span data-stu-id="f0338-130">requestsPerSecond</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FrequestsPerSecond) | <span data-ttu-id="f0338-131">fréquence des requêtes traitées par application</span><span class="sxs-lookup"><span data-stu-id="f0338-131">rate of requests processed by application</span></span> 
| `\.NET CLR Exceptions(??APP_CLR_PROC??)\# of Exceps Thrown / sec`    | <span data-ttu-id="f0338-132">Travail en cours...</span><span class="sxs-lookup"><span data-stu-id="f0338-132">Work in progress...</span></span> | [<span data-ttu-id="f0338-133">exceptionsPerSecond</span><span class="sxs-lookup"><span data-stu-id="f0338-133">exceptionsPerSecond</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FexceptionsPerSecond) | <span data-ttu-id="f0338-134">fréquence des exceptions levées par application</span><span class="sxs-lookup"><span data-stu-id="f0338-134">rate of exceptions thrown by application</span></span>
| `\ASP.NET Applications(??APP_W3SVC_PROC??)\Request Execution Time`   | <span data-ttu-id="f0338-135">Travail en cours...</span><span class="sxs-lookup"><span data-stu-id="f0338-135">Work in progress...</span></span> | [<span data-ttu-id="f0338-136">requestExecutionTime</span><span class="sxs-lookup"><span data-stu-id="f0338-136">requestExecutionTime</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FrequestExecutionTime) | <span data-ttu-id="f0338-137">durée d’exécution moyenne des requêtes</span><span class="sxs-lookup"><span data-stu-id="f0338-137">average requests execution time</span></span>
| `\ASP.NET Applications(??APP_W3SVC_PROC??)\Requests In Application Queue` | <span data-ttu-id="f0338-138">Travail en cours...</span><span class="sxs-lookup"><span data-stu-id="f0338-138">Work in progress...</span></span> | [<span data-ttu-id="f0338-139">requestsInQueue</span><span class="sxs-lookup"><span data-stu-id="f0338-139">requestsInQueue</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FrequestsInQueue) | <span data-ttu-id="f0338-140">nombre de demandes en attente de hello dans une file d’attente de traitement</span><span class="sxs-lookup"><span data-stu-id="f0338-140">number of requests waiting for hello processing in a queue</span></span>

## <a name="name"></a><span data-ttu-id="f0338-141">Nom</span><span class="sxs-lookup"><span data-stu-id="f0338-141">Name</span></span>

<span data-ttu-id="f0338-142">Nom de mesure de hello vous aimeriez toosee dans le portail Application Insights et l’interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="f0338-142">Name of hello metric you'd like toosee in Application Insights portal and UI.</span></span> 

## <a name="value"></a><span data-ttu-id="f0338-143">Valeur</span><span class="sxs-lookup"><span data-stu-id="f0338-143">Value</span></span>

<span data-ttu-id="f0338-144">Valeur unique pour la mesure.</span><span class="sxs-lookup"><span data-stu-id="f0338-144">Single value for measurement.</span></span> <span data-ttu-id="f0338-145">Somme des mesures individuelles pour l’agrégation de hello.</span><span class="sxs-lookup"><span data-stu-id="f0338-145">Sum of individual measurements for hello aggregation.</span></span>

## <a name="count"></a><span data-ttu-id="f0338-146">Nombre</span><span class="sxs-lookup"><span data-stu-id="f0338-146">Count</span></span>

<span data-ttu-id="f0338-147">Poids de la métrique de hello agrégées métrique.</span><span class="sxs-lookup"><span data-stu-id="f0338-147">Metric weight of hello aggregated metric.</span></span> <span data-ttu-id="f0338-148">Ne doit pas être défini pour une mesure.</span><span class="sxs-lookup"><span data-stu-id="f0338-148">Should not be set for a measurement.</span></span>

## <a name="min"></a><span data-ttu-id="f0338-149">Min</span><span class="sxs-lookup"><span data-stu-id="f0338-149">Min</span></span>

<span data-ttu-id="f0338-150">Valeur minimale de la métrique de hello agrégée.</span><span class="sxs-lookup"><span data-stu-id="f0338-150">Minimum value of hello aggregated metric.</span></span> <span data-ttu-id="f0338-151">Ne doit pas être défini pour une mesure.</span><span class="sxs-lookup"><span data-stu-id="f0338-151">Should not be set for a measurement.</span></span>

## <a name="max"></a><span data-ttu-id="f0338-152">max</span><span class="sxs-lookup"><span data-stu-id="f0338-152">Max</span></span>

<span data-ttu-id="f0338-153">Valeur maximale de la métrique de hello agrégée.</span><span class="sxs-lookup"><span data-stu-id="f0338-153">Maximum value of hello aggregated metric.</span></span> <span data-ttu-id="f0338-154">Ne doit pas être défini pour une mesure.</span><span class="sxs-lookup"><span data-stu-id="f0338-154">Should not be set for a measurement.</span></span>

## <a name="standard-deviation"></a><span data-ttu-id="f0338-155">Écart standard</span><span class="sxs-lookup"><span data-stu-id="f0338-155">Standard deviation</span></span>

<span data-ttu-id="f0338-156">Écart type de mesure de hello agrégée.</span><span class="sxs-lookup"><span data-stu-id="f0338-156">Standard deviation of hello aggregated metric.</span></span> <span data-ttu-id="f0338-157">Ne doit pas être défini pour une mesure.</span><span class="sxs-lookup"><span data-stu-id="f0338-157">Should not be set for a measurement.</span></span>

## <a name="custom-properties"></a><span data-ttu-id="f0338-158">Propriétés personnalisées</span><span class="sxs-lookup"><span data-stu-id="f0338-158">Custom properties</span></span>

[!INCLUDE [application-insights-data-model-properties](../../includes/application-insights-data-model-properties.md)]

## <a name="next-steps"></a><span data-ttu-id="f0338-159">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f0338-159">Next steps</span></span>

- <span data-ttu-id="f0338-160">Découvrez comment toouse [API Application Insights pour les événements personnalisés et les métriques](app-insights-api-custom-events-metrics.md#trackmetric).</span><span class="sxs-lookup"><span data-stu-id="f0338-160">Learn how toouse [Application Insights API for custom events and metrics](app-insights-api-custom-events-metrics.md#trackmetric).</span></span>
- <span data-ttu-id="f0338-161">Pour connaître les types et les modèles de données Application Insights, consultez [Modèle de données](application-insights-data-model.md).</span><span class="sxs-lookup"><span data-stu-id="f0338-161">See [data model](application-insights-data-model.md) for Application Insights types and data model.</span></span>
- <span data-ttu-id="f0338-162">Découvrez quelles [plateformes](app-insights-platforms.md) sont prises en charge par Application Insights.</span><span class="sxs-lookup"><span data-stu-id="f0338-162">Check out [platforms](app-insights-platforms.md) supported by Application Insights.</span></span>
