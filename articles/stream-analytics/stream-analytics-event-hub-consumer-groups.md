---
title: "aaaDebug Analytique de flux de données Azure avec les récepteurs du hub d’événements | Documents Microsoft"
description: "Meilleures pratiques pour considérer les groupes de consommateurs Event Hubs dans Stream Analytics."
keywords: "limite de hub d’événement, groupe de consommateurs"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 04/20/2017
ms.author: jeffstok
ms.openlocfilehash: 89821e6273151de43b5e42d907e547c939e24824
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="debug-azure-stream-analytics-with-event-hub-receivers"></a><span data-ttu-id="82e1d-104">Déboguer Azure Stream Analytics avec des destinataires de hub d’événement</span><span class="sxs-lookup"><span data-stu-id="82e1d-104">Debug Azure Stream Analytics with event hub receivers</span></span>

<span data-ttu-id="82e1d-105">Vous pouvez utiliser Azure Event Hubs Azure flux Analytique tooingest ou sortie des données à partir d’un travail.</span><span class="sxs-lookup"><span data-stu-id="82e1d-105">You can use Azure Event Hubs in Azure Stream Analytics tooingest or output data from a job.</span></span> <span data-ttu-id="82e1d-106">Il est recommandé pour l’utilisation des concentrateurs d’événements toouse plusieurs groupes de consommateurs, l’extensibilité de projet tooensure.</span><span class="sxs-lookup"><span data-stu-id="82e1d-106">A best practice for using Event Hubs is toouse multiple consumer groups, tooensure job scalability.</span></span> <span data-ttu-id="82e1d-107">L’une des raisons sont que nombre hello de lecteurs dans la tâche de flux de données Analytique hello pour une entrée spécifique affecte un nombre hello de lecteurs dans un groupe de consommateurs unique.</span><span class="sxs-lookup"><span data-stu-id="82e1d-107">One reason is that hello number of readers in hello Stream Analytics job for a specific input affects hello number of readers in a single consumer group.</span></span> <span data-ttu-id="82e1d-108">nombre précis de Hello de récepteurs est basé sur les détails d’implémentation interne pour la logique de topologie de montée en puissance parallèle hello.</span><span class="sxs-lookup"><span data-stu-id="82e1d-108">hello precise number of receivers is based on internal implementation details for hello scale-out topology logic.</span></span> <span data-ttu-id="82e1d-109">nombre de Hello de récepteurs n’est pas exposé en externe.</span><span class="sxs-lookup"><span data-stu-id="82e1d-109">hello number of receivers is not exposed externally.</span></span> <span data-ttu-id="82e1d-110">nombre de Hello de lecteurs peut changer à l’heure de début de tâche hello ou mises à niveau de la tâche.</span><span class="sxs-lookup"><span data-stu-id="82e1d-110">hello number of readers can change either at hello job start time or during job upgrades.</span></span>

> [!NOTE]
> <span data-ttu-id="82e1d-111">Quand un nombre de lecteurs hello change pendant une mise à niveau de la tâche, avertissements temporaires sont écrits tooaudit journaux.</span><span class="sxs-lookup"><span data-stu-id="82e1d-111">When hello number of readers changes during a job upgrade, transient warnings are written tooaudit logs.</span></span> <span data-ttu-id="82e1d-112">Les travaux Stream Analytics récupèrent automatiquement de ces problèmes temporaires.</span><span class="sxs-lookup"><span data-stu-id="82e1d-112">Stream Analytics jobs automatically recover from these transient issues.</span></span>

## <a name="number-of-readers-per-partition-exceeds-event-hubs-limit-of-five"></a><span data-ttu-id="82e1d-113">Le nombre de lecteurs par partition dépasse la limite de 5 définie dans Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="82e1d-113">Number of readers per partition exceeds Event Hubs limit of five</span></span>

<span data-ttu-id="82e1d-114">Les scénarios dans le hello nombre de lecteurs par partition dépasse la limite de concentrateurs d’événements hello de cinq hello suivants :</span><span class="sxs-lookup"><span data-stu-id="82e1d-114">Scenarios in which hello number of readers per partition exceeds hello Event Hubs limit of five include hello following:</span></span>

* <span data-ttu-id="82e1d-115">Plusieurs instructions SELECT : Si vous utilisez plusieurs instructions SELECT qui font référence trop**même** concentrateur d’événements d’entrée, chaque instruction SELECT entraîne une nouvelle toobe de récepteur créé.</span><span class="sxs-lookup"><span data-stu-id="82e1d-115">Multiple SELECT statements: If you use multiple SELECT statements that refer too**same** event hub input, each SELECT statement causes a new receiver toobe created.</span></span>
* <span data-ttu-id="82e1d-116">UNION : Lorsque vous utilisez une UNION, il est possible de toohave plusieurs entrées qui font référence toohello **même** groupe hub et consommateur d’événements.</span><span class="sxs-lookup"><span data-stu-id="82e1d-116">UNION: When you use a UNION, it's possible toohave multiple inputs that refer toohello **same** event hub and consumer group.</span></span>
* <span data-ttu-id="82e1d-117">Une jointure RÉFLEXIVE : Lorsque vous utilisez une opération de jointure de libre-service, il est possible de toorefer toohello **même** concentrateur d’événements plusieurs fois.</span><span class="sxs-lookup"><span data-stu-id="82e1d-117">SELF JOIN: When you use a SELF JOIN operation, it's possible toorefer toohello **same** event hub multiple times.</span></span>

## <a name="solution"></a><span data-ttu-id="82e1d-118">Solution</span><span class="sxs-lookup"><span data-stu-id="82e1d-118">Solution</span></span>

<span data-ttu-id="82e1d-119">Hello meilleures pratiques suivantes peuvent aider à atténuer les Bonjour nombre de lecteurs par partition dépasse la limite de concentrateurs d’événements hello de cinq des scénarios.</span><span class="sxs-lookup"><span data-stu-id="82e1d-119">hello following best practices can help mitigate scenarios in which hello number of readers per partition exceeds hello Event Hubs limit of five.</span></span>

### <a name="split-your-query-into-multiple-steps-by-using-a-with-clause"></a><span data-ttu-id="82e1d-120">Fractionner votre requête en plusieurs étapes à l’aide d’une clause WITH</span><span class="sxs-lookup"><span data-stu-id="82e1d-120">Split your query into multiple steps by using a WITH clause</span></span>

<span data-ttu-id="82e1d-121">clause WITH de Hello spécifie un jeu de résultats nommé temporaire qui peut être référencé par une clause FROM de la requête de hello.</span><span class="sxs-lookup"><span data-stu-id="82e1d-121">hello WITH clause specifies a temporary named result set that can be referenced by a FROM clause in hello query.</span></span> <span data-ttu-id="82e1d-122">Vous définissez la clause WITH de hello dans la portée de l’exécution de hello d’une instruction SELECT unique.</span><span class="sxs-lookup"><span data-stu-id="82e1d-122">You define hello WITH clause in hello execution scope of a single SELECT statement.</span></span>

<span data-ttu-id="82e1d-123">Par exemple, au lieu de cette requête :</span><span class="sxs-lookup"><span data-stu-id="82e1d-123">For example, instead of this query:</span></span>

```
SELECT foo 
INTO output1
FROM inputEventHub

SELECT bar
INTO output2
FROM inputEventHub 
…
```

<span data-ttu-id="82e1d-124">Utilisez cette requête :</span><span class="sxs-lookup"><span data-stu-id="82e1d-124">Use this query:</span></span>

```
WITH input (
   SELECT * FROM inputEventHub
) as data

SELECT foo
INTO output1
FROM data

SELECT bar
INTO output2
FROM data
…
```

### <a name="ensure-that-inputs-bind-toodifferent-consumer-groups"></a><span data-ttu-id="82e1d-125">Assurez-vous que les entrées lient des groupes de consommateurs toodifferent</span><span class="sxs-lookup"><span data-stu-id="82e1d-125">Ensure that inputs bind toodifferent consumer groups</span></span>

<span data-ttu-id="82e1d-126">Pour les requêtes dans laquelle au moins trois entrées sont connecté toohello même consommateur de concentrateurs d’événements, créer des groupes de consommateurs distincts.</span><span class="sxs-lookup"><span data-stu-id="82e1d-126">For queries in which three or more inputs are connected toohello same Event Hubs consumer group, create separate consumer groups.</span></span> <span data-ttu-id="82e1d-127">Cela requiert la création d’entrées de flux de données Analytique supplémentaires hello.</span><span class="sxs-lookup"><span data-stu-id="82e1d-127">This requires hello creation of additional Stream Analytics inputs.</span></span>


## <a name="get-help"></a><span data-ttu-id="82e1d-128">Obtenir de l’aide</span><span class="sxs-lookup"><span data-stu-id="82e1d-128">Get help</span></span>
<span data-ttu-id="82e1d-129">Pour une assistance supplémentaire, essayez notre [forum Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="82e1d-129">For additional assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="82e1d-130">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="82e1d-130">Next steps</span></span>
* [<span data-ttu-id="82e1d-131">Introduction tooStream Analytique</span><span class="sxs-lookup"><span data-stu-id="82e1d-131">Introduction tooStream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="82e1d-132">Prise en main de Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="82e1d-132">Get started with Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="82e1d-133">Mise à l’échelle des travaux Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="82e1d-133">Scale Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="82e1d-134">Informations de référence sur le langage de requête Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="82e1d-134">Stream Analytics query language reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="82e1d-135">Références sur l’API REST de gestion de Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="82e1d-135">Stream Analytics management REST API reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
