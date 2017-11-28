---
title: "fonctions de fenêtre d’Analytique aaaIntroduction tooStream | Documents Microsoft"
description: "En savoir plus sur les fonctions de fenêtre trois hello dans le flux de données Analytique (bascule, récurrente, glissante)."
keywords: "fenêtre bascule, fenêtre glissante, fenêtre récurrente"
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 0d8d8717-5d23-43f0-b475-af078ab4627d
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 7fc36eb9afb2b28e2791d925d26923145eb38074
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toostream-analytics-window-functions"></a><span data-ttu-id="581d5-104">Fonctions de fenêtre d’Analytique tooStream introduction</span><span class="sxs-lookup"><span data-stu-id="581d5-104">Introduction tooStream Analytics Window functions</span></span>
<span data-ttu-id="581d5-105">En temps réel plusieurs scénarios de diffusion en continu, il est nécessaire tooperform des opérations uniquement sur les données hello contenues dans les fenêtres temporelles.</span><span class="sxs-lookup"><span data-stu-id="581d5-105">In many real time streaming scenarios, it is necessary tooperform operations only on hello data contained in temporal windows.</span></span> <span data-ttu-id="581d5-106">Prise en charge native pour les fonctions de fenêtrage est une fonctionnalité clé de l’Analytique de flux de données Azure qui déplace l’aiguille de hello sur la productivité des développeurs dans la création de tâches de traitement des flux de données complexes.</span><span class="sxs-lookup"><span data-stu-id="581d5-106">Native support for windowing functions is a key feature of Azure Stream Analytics that moves hello needle on developer productivity in authoring complex stream processing jobs.</span></span> <span data-ttu-id="581d5-107">Flux Analytique permet aux développeurs toouse [ **bascule**](https://msdn.microsoft.com/library/dn835055.aspx), [ **saut** ](https://msdn.microsoft.com/library/dn835041.aspx) et [ **décalé** ](https://msdn.microsoft.com/library/dn835051.aspx) windows tooperform temporelle les opérations de diffusion en continu de données.</span><span class="sxs-lookup"><span data-stu-id="581d5-107">Stream Analytics enables developers toouse [**Tumbling**](https://msdn.microsoft.com/library/dn835055.aspx), [**Hopping**](https://msdn.microsoft.com/library/dn835041.aspx) and [**Sliding**](https://msdn.microsoft.com/library/dn835051.aspx) windows tooperform temporal operations on streaming data.</span></span> <span data-ttu-id="581d5-108">Il est important de noter que tous les [fenêtre](https://msdn.microsoft.com/library/dn835019.aspx) opérations produit des résultats à hello **fin** de fenêtre hello.</span><span class="sxs-lookup"><span data-stu-id="581d5-108">It is worth noting that all [Window](https://msdn.microsoft.com/library/dn835019.aspx) operations output results at hello **end** of hello window.</span></span> <span data-ttu-id="581d5-109">sortie Hello de fenêtre hello sera un événement unique basé sur la fonction d’agrégation hello utilisée.</span><span class="sxs-lookup"><span data-stu-id="581d5-109">hello output of hello window will be single event based on hello aggregate function used.</span></span> <span data-ttu-id="581d5-110">événement de Hello aura hello horodatage de fin hello de fenêtre hello et toutes les fonctions de fenêtre sont définies avec une longueur fixe.</span><span class="sxs-lookup"><span data-stu-id="581d5-110">hello event will have hello time stamp of hello end of hello window and all Window functions are defined with a fixed length.</span></span> <span data-ttu-id="581d5-111">Enfin, il est important toonote que toutes les fonctions de fenêtre doivent être utilisées dans un [ **GROUP BY** ](https://msdn.microsoft.com/library/dn835023.aspx) clause.</span><span class="sxs-lookup"><span data-stu-id="581d5-111">Lastly it is important toonote that all Window functions should be used in a [**GROUP BY**](https://msdn.microsoft.com/library/dn835023.aspx) clause.</span></span>

![Concepts des fonctions de fenêtrage de Stream Analytics](media/stream-analytics-window-functions/stream-analytics-window-functions-conceptual.png)

## <a name="tumbling-window"></a><span data-ttu-id="581d5-113">Fenêtre bascule</span><span class="sxs-lookup"><span data-stu-id="581d5-113">Tumbling Window</span></span>
<span data-ttu-id="581d5-114">Fonctions de fenêtre bascule sont toosegment utilisé un flux de données en segments de temps distinctes et exécutent une fonction contre eux, comme l’exemple hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="581d5-114">Tumbling window functions are used toosegment a data stream into distinct time segments and perform a function against them, such as hello example below.</span></span> <span data-ttu-id="581d5-115">les principaux atouts de Hello d’une fenêtre bascule sont qu’ils répéter, ne se chevauchent pas et un événement ne peut pas appartenir toomore à une fenêtre bascule.</span><span class="sxs-lookup"><span data-stu-id="581d5-115">hello key differentiators of a Tumbling window are that they repeat, do not overlap and an event cannot belong toomore than one tumbling window.</span></span>

![Introduction aux fonctions de fenêtre bascule de Stream Analytics](media/stream-analytics-window-functions/stream-analytics-window-functions-tumbling-intro.png)

## <a name="hopping-window"></a><span data-ttu-id="581d5-117">Fenêtre récurrente</span><span class="sxs-lookup"><span data-stu-id="581d5-117">Hopping Window</span></span>
<span data-ttu-id="581d5-118">Les fonctions de fenêtre récurrente font des bonds d’une durée fixe dans le temps.</span><span class="sxs-lookup"><span data-stu-id="581d5-118">Hopping window functions hop forward in time by a fixed period.</span></span> <span data-ttu-id="581d5-119">Il peut être facilement toothink d'entre eux en tant que fenêtres bascules qui peuvent se chevaucher, les événements peuvent appartenir toomore à un jeu de résultats de la fenêtre saut.</span><span class="sxs-lookup"><span data-stu-id="581d5-119">It may be easy toothink of them as Tumbling windows that can overlap, so events can belong toomore than one Hopping window result set.</span></span> <span data-ttu-id="581d5-120">toomake une saut de fenêtre même hello comme une fenêtre bascule un spécifiez simplement toobe de taille de saut hello même hello en tant que taille de la fenêtre hello.</span><span class="sxs-lookup"><span data-stu-id="581d5-120">toomake a Hopping window hello same as a Tumbling window one would simply specify hello hop size toobe hello same as hello window size.</span></span> 

![Introduction aux fonctions de fenêtre récurrente de Stream Analytics](media/stream-analytics-window-functions/stream-analytics-window-functions-hopping-intro.png)

## <a name="sliding-window"></a><span data-ttu-id="581d5-122">Fenêtre glissante</span><span class="sxs-lookup"><span data-stu-id="581d5-122">Sliding Window</span></span>
<span data-ttu-id="581d5-123">Les fonctions de fenêtre glissante, à la différence des fenêtres bascules ou récurrentes, ne génèrent une sortie **que** lorsqu’un événement se produit.</span><span class="sxs-lookup"><span data-stu-id="581d5-123">Sliding window functions, unlike Tumbling or Hopping windows, produce an output **only**  when an event occurs.</span></span> <span data-ttu-id="581d5-124">Chaque fenêtre aura au moins un événement et fenêtre hello en permanence avance par un € (epsilon).</span><span class="sxs-lookup"><span data-stu-id="581d5-124">Every window will have at least one event and hello window continuously moves forward by an € (epsilon).</span></span> <span data-ttu-id="581d5-125">Comme les fenêtres récurrentes, les événements peuvent appartenir toomore à une fenêtre glissante.</span><span class="sxs-lookup"><span data-stu-id="581d5-125">Like Hopping Windows, events can belong toomore than one Sliding Window.</span></span>

![Introduction aux fonctions de fenêtre glissante de Stream Analytics](media/stream-analytics-window-functions/stream-analytics-window-functions-sliding-intro.png)

## <a name="getting-help-with-window-functions"></a><span data-ttu-id="581d5-127">Obtenir de l’aide sur les fonctions de fenêtrage</span><span class="sxs-lookup"><span data-stu-id="581d5-127">Getting help with Window functions</span></span>
<span data-ttu-id="581d5-128">Pour obtenir une assistance, essayez notre [forum Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="581d5-128">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="581d5-129">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="581d5-129">Next steps</span></span>
* [<span data-ttu-id="581d5-130">Introduction tooAzure Analytique de flux de données</span><span class="sxs-lookup"><span data-stu-id="581d5-130">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="581d5-131">Prise en main d’Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="581d5-131">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="581d5-132">Mise à l'échelle des travaux Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="581d5-132">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="581d5-133">Références sur le langage des requêtes d'Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="581d5-133">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="581d5-134">Références sur l’API REST de gestion d’Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="581d5-134">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

