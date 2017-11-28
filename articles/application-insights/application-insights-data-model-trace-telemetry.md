---
title: "Modèle de données de télémétrie d’Azure Application Insights : télémétrie des traces | Microsoft Docs"
description: "Modèle de données Application Insights pour la télémétrie des traces"
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
ms.openlocfilehash: e1da0d6a6fbd9ca5486936c326ade667d7b01006
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="trace-telemetry-application-insights-data-model"></a><span data-ttu-id="a710c-103">Télémétrie des traces : modèle de données Application Insights</span><span class="sxs-lookup"><span data-stu-id="a710c-103">Trace telemetry: Application Insights data model</span></span>

<span data-ttu-id="a710c-104">La télémétrie des traces (dans [Application Insights](app-insights-overview.md)) représente des instructions de traces de type `printf` qui font l’objet de recherches textuelles.</span><span class="sxs-lookup"><span data-stu-id="a710c-104">Trace telemetry (in [Application Insights](app-insights-overview.md)) represents `printf` style trace statements that are text-searched.</span></span> <span data-ttu-id="a710c-105">`Log4Net`, `NLog` et les autres entrées de fichier journal de type texte sont converties en instances de ce type.</span><span class="sxs-lookup"><span data-stu-id="a710c-105">`Log4Net`, `NLog`, and other text-based log file entries are translated into instances of this type.</span></span> <span data-ttu-id="a710c-106">La trace ne comporte pas de mesures comme l’extensibilité.</span><span class="sxs-lookup"><span data-stu-id="a710c-106">The trace does not have measurements as an extensibility.</span></span>

## <a name="message"></a><span data-ttu-id="a710c-107">Message</span><span class="sxs-lookup"><span data-stu-id="a710c-107">Message</span></span>

<span data-ttu-id="a710c-108">Message de trace.</span><span class="sxs-lookup"><span data-stu-id="a710c-108">Trace message.</span></span>

<span data-ttu-id="a710c-109">Longueur maximale : 32768 caractères</span><span class="sxs-lookup"><span data-stu-id="a710c-109">Max length: 32768 characters</span></span>

## <a name="severity-level"></a><span data-ttu-id="a710c-110">Niveau de gravité</span><span class="sxs-lookup"><span data-stu-id="a710c-110">Severity level</span></span>

<span data-ttu-id="a710c-111">Niveau de gravité de trace.</span><span class="sxs-lookup"><span data-stu-id="a710c-111">Trace severity level.</span></span> <span data-ttu-id="a710c-112">La valeur peut être `Verbose`, `Information`, `Warning`, `Error`, `Critical`.</span><span class="sxs-lookup"><span data-stu-id="a710c-112">Value can be `Verbose`, `Information`, `Warning`, `Error`, `Critical`.</span></span>

## <a name="custom-properties"></a><span data-ttu-id="a710c-113">Propriétés personnalisées</span><span class="sxs-lookup"><span data-stu-id="a710c-113">Custom properties</span></span>

[!INCLUDE [application-insights-data-model-properties](../../includes/application-insights-data-model-properties.md)]

## <a name="next-steps"></a><span data-ttu-id="a710c-114">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a710c-114">Next steps</span></span>

- <span data-ttu-id="a710c-115">[Exploration des journaux .NET dans Application Insights](app-insights-asp-net-trace-logs.md).</span><span class="sxs-lookup"><span data-stu-id="a710c-115">[Explore .NET trace logs in Application Insights](app-insights-asp-net-trace-logs.md).</span></span>
- <span data-ttu-id="a710c-116">[Exploration du suivi des journaux Java dans Application Insights](app-insights-java-trace-logs.md).</span><span class="sxs-lookup"><span data-stu-id="a710c-116">[Explore Java trace logs in Application Insights](app-insights-java-trace-logs.md).</span></span>
- <span data-ttu-id="a710c-117">Pour connaître les types et les modèles de données Application Insights, consultez [Modèle de données](application-insights-data-model.md).</span><span class="sxs-lookup"><span data-stu-id="a710c-117">See [data model](application-insights-data-model.md) for Application Insights types and data model.</span></span>
- [<span data-ttu-id="a710c-118">Écrire des données de télémétrie de trace personnalisées</span><span class="sxs-lookup"><span data-stu-id="a710c-118">Write custom trace telemetry</span></span>](app-insights-api-custom-events-metrics.md#tracktrace)
- <span data-ttu-id="a710c-119">Découvrez quelles [plateformes](app-insights-platforms.md) sont prises en charge par Application Insights.</span><span class="sxs-lookup"><span data-stu-id="a710c-119">Check out [platforms](app-insights-platforms.md) supported by Application Insights.</span></span>