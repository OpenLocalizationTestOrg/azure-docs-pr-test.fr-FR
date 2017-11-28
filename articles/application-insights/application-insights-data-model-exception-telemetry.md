---
title: "aaaAzure modèle de données d’Application Insights télémétrie - télémétrie des exceptions | Documents Microsoft"
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
ms.openlocfilehash: 4c2b7d1ac3816d5623db9a35819a48a68a13a9cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="exception-telemetry-application-insights-data-model"></a><span data-ttu-id="addeb-103">Télémétrie des exceptions : modèle de données Application Insights</span><span class="sxs-lookup"><span data-stu-id="addeb-103">Exception telemetry: Application Insights data model</span></span>

<span data-ttu-id="addeb-104">Dans [Application Insights](app-insights-overview.md), une instance d’Exception représente une exception gérée ou non gérée s’est produite lors de l’exécution de l’application hello analysé.</span><span class="sxs-lookup"><span data-stu-id="addeb-104">In [Application Insights](app-insights-overview.md), an instance of Exception represents a handled or unhandled exception that occurred during execution of hello monitored application.</span></span>

## <a name="problem-id"></a><span data-ttu-id="addeb-105">ID du problème</span><span class="sxs-lookup"><span data-stu-id="addeb-105">Problem Id</span></span>

<span data-ttu-id="addeb-106">Identificateur d’où l’exception de hello a été levée dans le code.</span><span class="sxs-lookup"><span data-stu-id="addeb-106">Identifier of where hello exception was thrown in code.</span></span> <span data-ttu-id="addeb-107">Utilisé pour le regroupement des exceptions.</span><span class="sxs-lookup"><span data-stu-id="addeb-107">Used for exceptions grouping.</span></span> <span data-ttu-id="addeb-108">En règle générale, une combinaison de type d’exception et une fonction à partir de la pile des appels hello.</span><span class="sxs-lookup"><span data-stu-id="addeb-108">Typically a combination of exception type and a function from hello call stack.</span></span>

<span data-ttu-id="addeb-109">Longueur maximale : 1024 caractères</span><span class="sxs-lookup"><span data-stu-id="addeb-109">Max length: 1024 characters</span></span>

## <a name="severity-level"></a><span data-ttu-id="addeb-110">Niveau de gravité</span><span class="sxs-lookup"><span data-stu-id="addeb-110">Severity level</span></span>

<span data-ttu-id="addeb-111">Niveau de gravité de trace.</span><span class="sxs-lookup"><span data-stu-id="addeb-111">Trace severity level.</span></span> <span data-ttu-id="addeb-112">La valeur peut être `Verbose`, `Information`, `Warning`, `Error`, `Critical`.</span><span class="sxs-lookup"><span data-stu-id="addeb-112">Value can be `Verbose`, `Information`, `Warning`, `Error`, `Critical`.</span></span>

## <a name="exception-details"></a><span data-ttu-id="addeb-113">Détails de l’exception</span><span class="sxs-lookup"><span data-stu-id="addeb-113">Exception details</span></span>

<span data-ttu-id="addeb-114">(toobe étendu)</span><span class="sxs-lookup"><span data-stu-id="addeb-114">(toobe extended)</span></span>

## <a name="custom-properties"></a><span data-ttu-id="addeb-115">Propriétés personnalisées</span><span class="sxs-lookup"><span data-stu-id="addeb-115">Custom properties</span></span>

[!INCLUDE [application-insights-data-model-properties](../../includes/application-insights-data-model-properties.md)]

## <a name="custom-measurements"></a><span data-ttu-id="addeb-116">Mesures personnalisées</span><span class="sxs-lookup"><span data-stu-id="addeb-116">Custom measurements</span></span>

[!INCLUDE [application-insights-data-model-measurements](../../includes/application-insights-data-model-measurements.md)]

## <a name="next-steps"></a><span data-ttu-id="addeb-117">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="addeb-117">Next steps</span></span>

- <span data-ttu-id="addeb-118">Pour connaître les types et les modèles de données Application Insights, consultez [Modèle de données](application-insights-data-model.md).</span><span class="sxs-lookup"><span data-stu-id="addeb-118">See [data model](application-insights-data-model.md) for Application Insights types and data model.</span></span>
- <span data-ttu-id="addeb-119">Découvrez comment trop[diagnostiquer des exceptions dans vos applications web avec Application Insights](app-insights-asp-net-exceptions.md).</span><span class="sxs-lookup"><span data-stu-id="addeb-119">Learn how too[diagnose exceptions in your web apps with Application Insights](app-insights-asp-net-exceptions.md).</span></span>
- <span data-ttu-id="addeb-120">Découvrez quelles [plateformes](app-insights-platforms.md) sont prises en charge par Application Insights.</span><span class="sxs-lookup"><span data-stu-id="addeb-120">Check out [platforms](app-insights-platforms.md) supported by Application Insights.</span></span>
