---
title: "Modèle de données de télémétrie d’Azure Application Insights : télémétrie des exceptions | Microsoft Docs"
description: "Modèle de données Application Insights pour la télémétrie des exceptions"
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
ms.openlocfilehash: 6b220b0cb6719bac606f599d657d08ab847c7590
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="exception-telemetry-application-insights-data-model"></a><span data-ttu-id="90679-103">Télémétrie des exceptions : modèle de données Application Insights</span><span class="sxs-lookup"><span data-stu-id="90679-103">Exception telemetry: Application Insights data model</span></span>

<span data-ttu-id="90679-104">Dans [Application Insights](app-insights-overview.md), une instance d’exception représente une exception prise en charge ou non prise en charge générée pendant l’exécution de l’application surveillée.</span><span class="sxs-lookup"><span data-stu-id="90679-104">In [Application Insights](app-insights-overview.md), an instance of Exception represents a handled or unhandled exception that occurred during execution of the monitored application.</span></span>

## <a name="problem-id"></a><span data-ttu-id="90679-105">ID du problème</span><span class="sxs-lookup"><span data-stu-id="90679-105">Problem Id</span></span>

<span data-ttu-id="90679-106">Identificateur indiquant à quel endroit du code l’exception a été levée.</span><span class="sxs-lookup"><span data-stu-id="90679-106">Identifier of where the exception was thrown in code.</span></span> <span data-ttu-id="90679-107">Utilisé pour le regroupement des exceptions.</span><span class="sxs-lookup"><span data-stu-id="90679-107">Used for exceptions grouping.</span></span> <span data-ttu-id="90679-108">Généralement, une combinaison de type d’exception et une fonction de la pile des appels.</span><span class="sxs-lookup"><span data-stu-id="90679-108">Typically a combination of exception type and a function from the call stack.</span></span>

<span data-ttu-id="90679-109">Longueur maximale : 1024 caractères</span><span class="sxs-lookup"><span data-stu-id="90679-109">Max length: 1024 characters</span></span>

## <a name="severity-level"></a><span data-ttu-id="90679-110">Niveau de gravité</span><span class="sxs-lookup"><span data-stu-id="90679-110">Severity level</span></span>

<span data-ttu-id="90679-111">Niveau de gravité de trace.</span><span class="sxs-lookup"><span data-stu-id="90679-111">Trace severity level.</span></span> <span data-ttu-id="90679-112">La valeur peut être `Verbose`, `Information`, `Warning`, `Error`, `Critical`.</span><span class="sxs-lookup"><span data-stu-id="90679-112">Value can be `Verbose`, `Information`, `Warning`, `Error`, `Critical`.</span></span>

## <a name="exception-details"></a><span data-ttu-id="90679-113">Détails de l’exception</span><span class="sxs-lookup"><span data-stu-id="90679-113">Exception details</span></span>

<span data-ttu-id="90679-114">(À développer)</span><span class="sxs-lookup"><span data-stu-id="90679-114">(To be extended)</span></span>

## <a name="custom-properties"></a><span data-ttu-id="90679-115">Propriétés personnalisées</span><span class="sxs-lookup"><span data-stu-id="90679-115">Custom properties</span></span>

[!INCLUDE [application-insights-data-model-properties](../../includes/application-insights-data-model-properties.md)]

## <a name="custom-measurements"></a><span data-ttu-id="90679-116">Mesures personnalisées</span><span class="sxs-lookup"><span data-stu-id="90679-116">Custom measurements</span></span>

[!INCLUDE [application-insights-data-model-measurements](../../includes/application-insights-data-model-measurements.md)]

## <a name="next-steps"></a><span data-ttu-id="90679-117">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="90679-117">Next steps</span></span>

- <span data-ttu-id="90679-118">Pour connaître les types et les modèles de données Application Insights, consultez [Modèle de données](application-insights-data-model.md).</span><span class="sxs-lookup"><span data-stu-id="90679-118">See [data model](application-insights-data-model.md) for Application Insights types and data model.</span></span>
- <span data-ttu-id="90679-119">Découvrez comment [diagnostiquer les exceptions dans vos applications web avec Application Insights](app-insights-asp-net-exceptions.md).</span><span class="sxs-lookup"><span data-stu-id="90679-119">Learn how to [diagnose exceptions in your web apps with Application Insights](app-insights-asp-net-exceptions.md).</span></span>
- <span data-ttu-id="90679-120">Découvrez quelles [plateformes](app-insights-platforms.md) sont prises en charge par Application Insights.</span><span class="sxs-lookup"><span data-stu-id="90679-120">Check out [platforms](app-insights-platforms.md) supported by Application Insights.</span></span>
