---
title: "Modèle de données de télémétrie d’Azure Application Insights : télémétrie des événements | Microsoft Docs"
description: "Modèle de données Application Insights pour la télémétrie des événements"
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
ms.openlocfilehash: 422e193ae10938954602a6ef8c49fd47f473bc01
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="event-telemetry-application-insights-data-model"></a><span data-ttu-id="4450a-103">Télémétrie des événements : modèle de données Application Insights</span><span class="sxs-lookup"><span data-stu-id="4450a-103">Event telemetry: Application Insights data model</span></span>

<span data-ttu-id="4450a-104">Vous pouvez créer des éléments de télémétrie (dans [Application Insights](app-insights-overview.md)) pour représenter un événement qui s’est produit dans votre application.</span><span class="sxs-lookup"><span data-stu-id="4450a-104">You can create event telemetry items (in [Application Insights](app-insights-overview.md)) to represent an event that occurred in your application.</span></span> <span data-ttu-id="4450a-105">En général, il s’agit d’une interaction utilisateur comme un clic sur un bouton ou une validation de commande.</span><span class="sxs-lookup"><span data-stu-id="4450a-105">Typically it is a user interaction such as button click or order checkout.</span></span> <span data-ttu-id="4450a-106">Il peut aussi s’agir d’un événement lié au cycle de vie de l’application, comme une initialisation ou une mise à jour de configuration.</span><span class="sxs-lookup"><span data-stu-id="4450a-106">It can also be an application life cycle event like initialization or configuration update.</span></span> 

<span data-ttu-id="4450a-107">Sur le plan sémantique, les événements ne sont pas forcément corrélés aux requêtes.</span><span class="sxs-lookup"><span data-stu-id="4450a-107">Semantically, events may or may not be correlated to requests.</span></span> <span data-ttu-id="4450a-108">Toutefois, si la télémétrie des événements est utilisée correctement, elle est plus importante que les requêtes ou les traces.</span><span class="sxs-lookup"><span data-stu-id="4450a-108">However, if used properly, event telemetry is more important than requests or traces.</span></span> <span data-ttu-id="4450a-109">Les événements représentent la télémétrie métier et doivent faire l’objet d’un [échantillonnage](app-insights-api-filtering-sampling.md) distinct, moins agressif.</span><span class="sxs-lookup"><span data-stu-id="4450a-109">Events represent business telemetry and should be a subject to separate, less aggressive [sampling](app-insights-api-filtering-sampling.md).</span></span>

## <a name="name"></a><span data-ttu-id="4450a-110">Nom</span><span class="sxs-lookup"><span data-stu-id="4450a-110">Name</span></span>

<span data-ttu-id="4450a-111">Nom de l’événement.</span><span class="sxs-lookup"><span data-stu-id="4450a-111">Event name.</span></span> <span data-ttu-id="4450a-112">Pour permettre le regroupement approprié et des mesures utiles, limitez votre application afin qu’elle génère un petit nombre de noms d’événements distincts.</span><span class="sxs-lookup"><span data-stu-id="4450a-112">To allow proper grouping and useful metrics, restrict your application so that it generates a small number of separate event names.</span></span> <span data-ttu-id="4450a-113">Par exemple, n’utilisez pas un nom distinct pour chaque instance générée d’un événement.</span><span class="sxs-lookup"><span data-stu-id="4450a-113">For example, don't use a separate name for each generated instance of an event.</span></span>

<span data-ttu-id="4450a-114">Longueur maximale : 512 caractères</span><span class="sxs-lookup"><span data-stu-id="4450a-114">Max length: 512 characters</span></span>

## <a name="custom-properties"></a><span data-ttu-id="4450a-115">Propriétés personnalisées</span><span class="sxs-lookup"><span data-stu-id="4450a-115">Custom properties</span></span>

[!INCLUDE [application-insights-data-model-properties](../../includes/application-insights-data-model-properties.md)]

## <a name="custom-measurements"></a><span data-ttu-id="4450a-116">Mesures personnalisées</span><span class="sxs-lookup"><span data-stu-id="4450a-116">Custom measurements</span></span>

[!INCLUDE [application-insights-data-model-measurements](../../includes/application-insights-data-model-measurements.md)]

## <a name="next-steps"></a><span data-ttu-id="4450a-117">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4450a-117">Next steps</span></span>

- <span data-ttu-id="4450a-118">Pour connaître les types et les modèles de données Application Insights, consultez [Modèle de données](application-insights-data-model.md).</span><span class="sxs-lookup"><span data-stu-id="4450a-118">See [data model](application-insights-data-model.md) for Application Insights types and data model.</span></span>
- [<span data-ttu-id="4450a-119">Écrire des données de télémétrie d’événement personnalisées</span><span class="sxs-lookup"><span data-stu-id="4450a-119">Write custom event telemetry</span></span>](app-insights-api-custom-events-metrics.md#trackevent)
- <span data-ttu-id="4450a-120">Découvrez quelles [plateformes](app-insights-platforms.md) sont prises en charge par Application Insights.</span><span class="sxs-lookup"><span data-stu-id="4450a-120">Check out [platforms](app-insights-platforms.md) supported by Application Insights.</span></span>
