---
title: "données aaaFind avec des recherches de journaux dans Azure journal Analytique | Documents Microsoft"
description: "Recherches de journal vous toocombine et mettre en corrélation des données machine de plusieurs sources dans votre environnement."
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.assetid: 0d7b6712-1722-423b-a60f-05389cde3625
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: bwren
ms.openlocfilehash: 1161857a0027f05726492417362cb24a8fe21ef8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="find-data-using-log-searches-in-log-analytics"></a><span data-ttu-id="19e0a-103">Trouver des données avec les recherches de journaux dans Log Analytics</span><span class="sxs-lookup"><span data-stu-id="19e0a-103">Find data using log searches in Log Analytics</span></span>

>[!NOTE]
> <span data-ttu-id="19e0a-104">Cet article décrit les recherches de journal à l’aide du langage de requête en cours hello dans Analytique de journal.</span><span class="sxs-lookup"><span data-stu-id="19e0a-104">This article describes log searches using hello current query language in Log Analytics.</span></span>  <span data-ttu-id="19e0a-105">Si votre espace de travail a été mis à niveau toohello [Analytique de journal nouveau langage de requête](log-analytics-log-search-upgrade.md), puis vous devez faire référence trop[Understanding log recherche Analytique de journal (nouveau)](log-analytics-log-search-new.md).</span><span class="sxs-lookup"><span data-stu-id="19e0a-105">If your workspace has been upgraded toohello [new Log Analytics query language](log-analytics-log-search-upgrade.md), then you should refer too[Understanding log searches in Log Analytics (new)](log-analytics-log-search-new.md).</span></span>


<span data-ttu-id="19e0a-106">Au cœur de hello d’Analytique de journal est fonction de recherche de journal hello qui vous permet de toocombine et mettre en corrélation des données machine de plusieurs sources dans votre environnement.</span><span class="sxs-lookup"><span data-stu-id="19e0a-106">At hello core of Log Analytics is hello log search feature which allows you toocombine and correlate any machine data from multiple sources within your environment.</span></span> <span data-ttu-id="19e0a-107">Les solutions sont également alimentées par toobring de recherche de journal vous mesures cernant un domaine problématique en particulier.</span><span class="sxs-lookup"><span data-stu-id="19e0a-107">Solutions are also powered by log search toobring you metrics pivoted around a particular problem area.</span></span>

<span data-ttu-id="19e0a-108">Sur la page de recherche de hello, vous pouvez créer une requête, puis lorsque vous recherchez, vous pouvez filtrer les résultats de hello à l’aide de contrôles de facette.</span><span class="sxs-lookup"><span data-stu-id="19e0a-108">On hello Search page, you can create a query, and then when you search, you can filter hello results by using facet controls.</span></span> <span data-ttu-id="19e0a-109">Vous pouvez également créer des rapports, le filtrage et des requêtes avancées tootransform sur vos résultats.</span><span class="sxs-lookup"><span data-stu-id="19e0a-109">You can also create advanced queries tootransform, filter, and report on your results.</span></span>

<span data-ttu-id="19e0a-110">Les requêtes de recherche de journal courantes apparaissent dans la plupart des pages de solutions.</span><span class="sxs-lookup"><span data-stu-id="19e0a-110">Common log search queries appear on most solution pages.</span></span> <span data-ttu-id="19e0a-111">Dans l’ensemble de la console OMS hello, vous pouvez cliquer sur les vignettes ou Explorer les éléments tooother tooview plus d’informations sur l’élément de hello par à l’aide de la recherche de journal.</span><span class="sxs-lookup"><span data-stu-id="19e0a-111">Throughout hello OMS console, you can click tiles or drill in tooother items tooview details about hello item by using log search.</span></span>

<span data-ttu-id="19e0a-112">Dans ce didacticiel, nous examinerons exemples toocover toutes les notions de base hello lorsque vous utilisez la recherche de journal.</span><span class="sxs-lookup"><span data-stu-id="19e0a-112">In this tutorial, we'll walk through examples toocover all hello basics when you use log search.</span></span>

<span data-ttu-id="19e0a-113">Nous allons commencer par des exemples simples et pratiques, puis générez sur les afin que vous pouvez obtenir une compréhension pratique de cas d’utilisation sur le mode insights de hello toouse hello syntaxe tooextract à partir des données de hello.</span><span class="sxs-lookup"><span data-stu-id="19e0a-113">We'll start with simple, practical examples and then build on them so that you can get an understanding of practical use cases about how toouse hello syntax tooextract hello insights you want from hello data.</span></span>

<span data-ttu-id="19e0a-114">Une fois que vous êtes familiarisé avec les techniques de recherche, vous pouvez passer en revue hello [Analytique de journal journal référence de recherche](log-analytics-search-reference.md).</span><span class="sxs-lookup"><span data-stu-id="19e0a-114">After you've familiar with search techniques, you can review hello [Log Analytics log search reference](log-analytics-search-reference.md).</span></span>

## <a name="use-basic-filters"></a><span data-ttu-id="19e0a-115">Utilisation de filtres de base</span><span class="sxs-lookup"><span data-stu-id="19e0a-115">Use basic filters</span></span>
<span data-ttu-id="19e0a-116">Hello première tooknow est que hello première partie d’une requête de recherche, avant tout » | « caractère de barre verticale est toujours un *filtre*.</span><span class="sxs-lookup"><span data-stu-id="19e0a-116">hello first thing tooknow is that hello first part of a search query, before any "|" vertical pipe character, is always a *filter*.</span></span> <span data-ttu-id="19e0a-117">Vous pouvez la considérer comme une clause WHERE dans TSQL : elle détermine *que* sous-ensemble de toopull de données en dehors de la banque de données OMS hello.</span><span class="sxs-lookup"><span data-stu-id="19e0a-117">You can think of it as a WHERE clause in TSQL--it determines *what* subset of data toopull out of hello OMS data store.</span></span> <span data-ttu-id="19e0a-118">La recherche dans le magasin de données hello consiste principalement à préciser les caractéristiques hello de hello données tooextract, par conséquent, il est naturel qu’une requête commence avec la clause WHERE de hello.</span><span class="sxs-lookup"><span data-stu-id="19e0a-118">Searching in hello data store is largely about specifying hello characteristics of hello data that you want tooextract, so it is natural that a query would start with hello WHERE clause.</span></span>

<span data-ttu-id="19e0a-119">Hello filtres les plus simples que vous pouvez utiliser sont *mots clés*, tels que « error » ou « timeout » ou un nom d’ordinateur.</span><span class="sxs-lookup"><span data-stu-id="19e0a-119">hello most basic filters you can use are *keywords*, such as ‘error’ or ‘timeout’, or a computer name.</span></span> <span data-ttu-id="19e0a-120">Ces types de requêtes simples retournent généralement différentes formes de données au sein de hello même jeu de résultats.</span><span class="sxs-lookup"><span data-stu-id="19e0a-120">These types of simple queries generally return diverse shapes of data within hello same result set.</span></span> <span data-ttu-id="19e0a-121">Il s’agit, car le journal Analytique dispose de différents *types* des données dans le système de hello.</span><span class="sxs-lookup"><span data-stu-id="19e0a-121">This is because Log Analytics has different *types* of data in hello system.</span></span>

### <a name="tooconduct-a-simple-search"></a><span data-ttu-id="19e0a-122">tooconduct une recherche simple</span><span class="sxs-lookup"><span data-stu-id="19e0a-122">tooconduct a simple search</span></span>
1. <span data-ttu-id="19e0a-123">Dans le portail OMS : hello, cliquez sur **recherche de journal**.</span><span class="sxs-lookup"><span data-stu-id="19e0a-123">In hello OMS portal, click **Log Search**.</span></span>  
    <span data-ttu-id="19e0a-124">![Vignette Rechercher](./media/log-analytics-log-searches/oms-overview-log-search.png)</span><span class="sxs-lookup"><span data-stu-id="19e0a-124">![search tile](./media/log-analytics-log-searches/oms-overview-log-search.png)</span></span>
2. <span data-ttu-id="19e0a-125">Dans le champ de requête hello, tapez `error` puis cliquez sur **recherche**.</span><span class="sxs-lookup"><span data-stu-id="19e0a-125">In hello query field, type `error` and then click **Search**.</span></span>  
    <span data-ttu-id="19e0a-126">![Recherche d’erreur](./media/log-analytics-log-searches/oms-search-error.png)</span><span class="sxs-lookup"><span data-stu-id="19e0a-126">![search error](./media/log-analytics-log-searches/oms-search-error.png)</span></span>  
    <span data-ttu-id="19e0a-127">Par exemple, les requêtes hello pour `error` Bonjour image suivante a retourné 100 000 **événement** enregistrements (collectés par la gestion du journal), 18 **ConfigurationAlert** (générés par la Configuration des enregistrements Évaluation) et 12 **ConfigurationChange** enregistrements (capturés par le suivi des modifications de hello).</span><span class="sxs-lookup"><span data-stu-id="19e0a-127">For example, hello query for `error` in hello following image returned 100,000 **Event** records (collected by Log Management), 18 **ConfigurationAlert** records (generated by Configuration Assessment) and 12 **ConfigurationChange** records (captured by hello Change Tracking).</span></span>   
    <span data-ttu-id="19e0a-128">![Recherche de résultats](./media/log-analytics-log-searches/oms-search-results01.png)</span><span class="sxs-lookup"><span data-stu-id="19e0a-128">![search results](./media/log-analytics-log-searches/oms-search-results01.png)</span></span>  

<span data-ttu-id="19e0a-129">Ces filtres ne sont pas vraiment des classes/types d'objet.</span><span class="sxs-lookup"><span data-stu-id="19e0a-129">These filters are not really object types/classes.</span></span> <span data-ttu-id="19e0a-130">*Type* est simplement une balise ou une propriété ou une chaîne/nom/une catégorie, qui est attaché tooa donnée.</span><span class="sxs-lookup"><span data-stu-id="19e0a-130">*Type* is just a tag, or a property, or a string/name/category, that is attached tooa piece of data.</span></span> <span data-ttu-id="19e0a-131">Certains documents dans hello système sont marqués en tant que **Type : ConfigurationAlert** et certaines sont marqués en tant que **Type : Perf**, ou **Type : Event**, et ainsi de suite.</span><span class="sxs-lookup"><span data-stu-id="19e0a-131">Some documents in hello system are tagged as **Type:ConfigurationAlert** and some are tagged as **Type:Perf**, or **Type:Event**, and so on.</span></span> <span data-ttu-id="19e0a-132">Chaque résultat de recherche, document, enregistrement ou entrée affiche toutes les propriétés brutes hello et leurs valeurs pour chacun de ces éléments de données, et vous pouvez utiliser ces toospecify de noms de champ de filtre de hello lorsque vous souhaitez que seuls les enregistrements hello tooretrieve dont le champ de hello a cette donnée valeur.</span><span class="sxs-lookup"><span data-stu-id="19e0a-132">Each search result, document, record, or entry displays all hello raw properties and their values for each of those pieces of data, and you can use those field names toospecify in hello filter when you want tooretrieve only hello records where hello field has that given value.</span></span>

<span data-ttu-id="19e0a-133">Le *type* est simplement un champ que tous les enregistrements ont. Il n'est pas différent des autres champs.</span><span class="sxs-lookup"><span data-stu-id="19e0a-133">*Type* is really just a field that all records have, it is not different from any other field.</span></span> <span data-ttu-id="19e0a-134">Cela a été établi en fonction de valeur hello du champ de Type hello.</span><span class="sxs-lookup"><span data-stu-id="19e0a-134">This was established based on hello value of hello Type field.</span></span> <span data-ttu-id="19e0a-135">Cet enregistrement aura une autre forme.</span><span class="sxs-lookup"><span data-stu-id="19e0a-135">That record will have a different shape or form.</span></span> <span data-ttu-id="19e0a-136">Par ailleurs, **Type = Perf**, ou **Type = Event** est également hello syntaxe que vous avez besoin de toolearn tooquery pour les données de performances ou des événements.</span><span class="sxs-lookup"><span data-stu-id="19e0a-136">Incidentally, **Type=Perf**, or **Type=Event** is also hello syntax that you need toolearn tooquery for performance data or events.</span></span>

<span data-ttu-id="19e0a-137">Vous pouvez utiliser un signe deux-points ( :) ou un signe égal (=) après le nom du champ hello et avant la valeur de hello.</span><span class="sxs-lookup"><span data-stu-id="19e0a-137">You can use either a colon (:) or an equal sign (=) after hello field name and before hello value.</span></span> <span data-ttu-id="19e0a-138">**Type : Event** et **Type = Event** sont équivalentes dans un sens, vous pouvez choisir hello style qui vous convient.</span><span class="sxs-lookup"><span data-stu-id="19e0a-138">**Type:Event** and **Type=Event** are equivalent in meaning, you can choose hello style you prefer.</span></span>

<span data-ttu-id="19e0a-139">Par conséquent, si hello Type = Perf enregistrements ont un champ appelé « CounterName », puis vous pouvez écrire une requête qui ressemble à `Type=Perf CounterName="% Processor Time"`.</span><span class="sxs-lookup"><span data-stu-id="19e0a-139">So, if hello Type=Perf records have a field called 'CounterName', then you can write a query resembling `Type=Perf CounterName="% Processor Time"`.</span></span>

<span data-ttu-id="19e0a-140">Cela vous donnera des données de performances hello uniquement où le nom de compteur de performance hello est « % temps processeur ».</span><span class="sxs-lookup"><span data-stu-id="19e0a-140">This will give you only hello performance data where hello performance counter name is "% Processor Time".</span></span>

### <a name="toosearch-for-processor-time-performance-data"></a><span data-ttu-id="19e0a-141">toosearch pour les données de performance du temps processeur</span><span class="sxs-lookup"><span data-stu-id="19e0a-141">toosearch for processor time performance data</span></span>
* <span data-ttu-id="19e0a-142">Dans le champ de requête de recherche hello, tapez`Type=Perf CounterName="% Processor Time"`</span><span class="sxs-lookup"><span data-stu-id="19e0a-142">In hello search query field, type `Type=Perf CounterName="% Processor Time"`</span></span>

<span data-ttu-id="19e0a-143">Vous pouvez également être plus précis et utiliser **InstanceName = _ 'Total'** dans la requête de hello, qui est un compteur de performance Windows.</span><span class="sxs-lookup"><span data-stu-id="19e0a-143">You can also be more specific and use **InstanceName=_'Total'** in hello query, which is a Windows performance counter.</span></span> <span data-ttu-id="19e0a-144">Vous pouvez également sélectionner une facette et une autre valeur **field:value**.</span><span class="sxs-lookup"><span data-stu-id="19e0a-144">You can also select a facet and another **field:value**.</span></span> <span data-ttu-id="19e0a-145">Hello filtre est automatiquement ajouté tooyour filtre dans la barre de requête hello.</span><span class="sxs-lookup"><span data-stu-id="19e0a-145">hello filter is automatically added tooyour filter in hello query bar.</span></span> <span data-ttu-id="19e0a-146">Vous pouvez le voir dans hello suivant l’image.</span><span class="sxs-lookup"><span data-stu-id="19e0a-146">You can see this in hello following image.</span></span> <span data-ttu-id="19e0a-147">Il vous montre où tooclick tooadd **InstanceName : '_Total'** requête toohello sans avoir à taper quoi que ce soit.</span><span class="sxs-lookup"><span data-stu-id="19e0a-147">It shows you where tooclick tooadd **InstanceName:’_Total’** toohello query without typing anything.</span></span>

![Recherche de facette](./media/log-analytics-log-searches/oms-search-facet.png)

<span data-ttu-id="19e0a-149">Votre requête devient alors `Type=Perf CounterName="% Processor Time" InstanceName="_Total"`</span><span class="sxs-lookup"><span data-stu-id="19e0a-149">Your query now becomes `Type=Perf CounterName="% Processor Time" InstanceName="_Total"`</span></span>

<span data-ttu-id="19e0a-150">Dans cet exemple, vous n’avez pas toospecify **Type = Perf** tooget toothis résultat.</span><span class="sxs-lookup"><span data-stu-id="19e0a-150">In this example, you don't have toospecify **Type=Perf** tooget toothis result.</span></span> <span data-ttu-id="19e0a-151">Étant donné que hello champs CounterName et InstanceName existent uniquement pour les enregistrements de Type = Perf, requête de hello est suffisamment spécifique tooreturn hello mêmes résultats que hello une plus longue, précédente :</span><span class="sxs-lookup"><span data-stu-id="19e0a-151">Because hello fields CounterName and InstanceName only exist for records of Type=Perf, hello query is specific enough tooreturn hello same results as hello longer, previous one:</span></span>

```
CounterName="% Processor Time" InstanceName="_Total"
```

<span data-ttu-id="19e0a-152">C’est parce que tous les filtres de hello dans la requête de hello sont évalués comme étant dans *AND* entre eux.</span><span class="sxs-lookup"><span data-stu-id="19e0a-152">This is because all hello filters in hello query are evaluated as being in *AND* with each other.</span></span> <span data-ttu-id="19e0a-153">En réalité, hello plusieurs champs que vous ajoutez toohello critères, moins vous obtenez des résultats plus spécifiques et affinés.</span><span class="sxs-lookup"><span data-stu-id="19e0a-153">Effectively, hello more fields you add toohello criteria, you get less, more specific and refined results.</span></span>

<span data-ttu-id="19e0a-154">Par exemple, les requêtes hello `Type=Event EventLog="Windows PowerShell"` est identique trop`Type=Event AND EventLog="Windows PowerShell"`.</span><span class="sxs-lookup"><span data-stu-id="19e0a-154">For example, hello query `Type=Event EventLog="Windows PowerShell"` is identical too`Type=Event AND EventLog="Windows PowerShell"`.</span></span> <span data-ttu-id="19e0a-155">Il retourne tous les événements qui ont été enregistrés dans et collectés à partir du journal des événements Windows PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="19e0a-155">It returns all events that were logged in and collected from hello Windows PowerShell event log.</span></span> <span data-ttu-id="19e0a-156">Si vous ajoutez un filtre à plusieurs fois et en sélectionnant de manière répétée hello même facette, puis d’émettre hello est alors purement esthétique : il peut surcharger la barre de recherche hello, mais elle retourne toujours hello mêmes résultats, car l’opérateur AND implicite de hello est toujours.</span><span class="sxs-lookup"><span data-stu-id="19e0a-156">If you add a filter multiple times by repeatedly selecting hello same facet, then hello issue is purely cosmetic--it might clutter hello Search bar, but it still returns hello same results because hello implicit AND operator is always there.</span></span>

<span data-ttu-id="19e0a-157">Vous pouvez facilement inverser l’opérateur AND implicite de hello à l’aide d’un opérateur NOT explicite.</span><span class="sxs-lookup"><span data-stu-id="19e0a-157">You can easily reverse hello implicit AND operator by using a NOT operator explicitly.</span></span> <span data-ttu-id="19e0a-158">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="19e0a-158">For example:</span></span>

<span data-ttu-id="19e0a-159">`Type:Event NOT(EventLog:"Windows PowerShell")`ou son équivalent `Type=Event EventLog!="Windows PowerShell"` retourne tous les événements de tous les autres journaux qui ne sont pas hello Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="19e0a-159">`Type:Event NOT(EventLog:"Windows PowerShell")` or its equivalent `Type=Event EventLog!="Windows PowerShell"` return all events from all other logs that are NOT hello Windows PowerShell log.</span></span>

<span data-ttu-id="19e0a-160">Vous pouvez également utiliser un autre opérateur booléen tel que « OR ».</span><span class="sxs-lookup"><span data-stu-id="19e0a-160">Or, you can use other Boolean operator such as ‘OR’.</span></span> <span data-ttu-id="19e0a-161">Renvoie les enregistrements pour le hello le journal des événements est une Application ou un système de requête de suivante de Hello.</span><span class="sxs-lookup"><span data-stu-id="19e0a-161">hello following query returns records for which hello EventLog is either Application OR System.</span></span>

```
EventLog=Application OR EventLog=System
```

<span data-ttu-id="19e0a-162">À l’aide de hello au-dessus de requête, vous obtiendrez les entrées pour les journaux Bonjour même jeu de résultats.</span><span class="sxs-lookup"><span data-stu-id="19e0a-162">Using hello above query, you’ll get entries for both logs in hello same result set.</span></span>

<span data-ttu-id="19e0a-163">Toutefois, si vous supprimez hello ou en le laissant hello implicite AND en place, puis hello requête suivante ne produira pas de résultats, car il n’est pas une entrée de journal des événements qui appartient tooBOTH journaux.</span><span class="sxs-lookup"><span data-stu-id="19e0a-163">However, if you remove hello OR by leaving hello implicit AND in place, then hello following query will not produce any results because there isn’t an event log entry that belongs tooBOTH logs.</span></span> <span data-ttu-id="19e0a-164">Chaque entrée de journal des événements a été écrite tooonly un des deux journaux de hello.</span><span class="sxs-lookup"><span data-stu-id="19e0a-164">Each event log entry was written tooonly one of hello two logs.</span></span>

```
EventLog=Application EventLog=System
```


## <a name="use-additional-filters"></a><span data-ttu-id="19e0a-165">Utilisation de filtres supplémentaires</span><span class="sxs-lookup"><span data-stu-id="19e0a-165">Use additional filters</span></span>
<span data-ttu-id="19e0a-166">Hello requête suivante retourne les entrées pour les journaux d’événements 2 pour tous les ordinateurs hello qui ont envoyé des données.</span><span class="sxs-lookup"><span data-stu-id="19e0a-166">hello following query returns entries for 2 event logs for all hello computers that have sent data.</span></span>

```
EventLog=Application OR EventLog=System
```

![Recherche de résultats](./media/log-analytics-log-searches/oms-search-results03.png)

<span data-ttu-id="19e0a-168">La sélection d’un des champs de hello ou des filtres restreindra hello requête tooa ordinateur spécifique, en excluant tous les autres.</span><span class="sxs-lookup"><span data-stu-id="19e0a-168">Selecting one of hello fields or filters will narrow hello query tooa specific computer, excluding all other ones.</span></span> <span data-ttu-id="19e0a-169">requête obtenue de Hello peut se présenter comme suit de hello.</span><span class="sxs-lookup"><span data-stu-id="19e0a-169">hello resulting query would resemble hello following.</span></span>

```
EventLog=Application OR EventLog=System Computer=SERVER1.contoso.com
```

<span data-ttu-id="19e0a-170">Qui est équivalent toohello suivantes, en raison de hello opérateur and implicite.</span><span class="sxs-lookup"><span data-stu-id="19e0a-170">Which is equivalent toohello following, because of hello implicit AND.</span></span>

```
EventLog=Application OR EventLog=System AND Computer=SERVER1.contoso.com
```

<span data-ttu-id="19e0a-171">Chaque requête est évaluée dans hello suivant l’ordre explicite.</span><span class="sxs-lookup"><span data-stu-id="19e0a-171">Each query is evaluated in hello following explicit order.</span></span> <span data-ttu-id="19e0a-172">Parenthèse de hello Remarque.</span><span class="sxs-lookup"><span data-stu-id="19e0a-172">Note hello parenthesis.</span></span>

```
(EventLog=Application OR EventLog=System) AND Computer=SERVER1.contoso.com
```

<span data-ttu-id="19e0a-173">Comme champ hello du journal des événements, vous pouvez récupérer des données uniquement pour un ensemble d’ordinateurs spécifiques en ajoutant ou.</span><span class="sxs-lookup"><span data-stu-id="19e0a-173">Just like hello event log field, you can retrieve data only for a set of specific computers by adding OR.</span></span> <span data-ttu-id="19e0a-174">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="19e0a-174">For example:</span></span>

```
(EventLog=Application OR EventLog=System) AND (Computer=SERVER1.contoso.com OR Computer=SERVER2.contoso.com OR Computer=SERVER3.contoso.com)
```

<span data-ttu-id="19e0a-175">De même, cette hello après le retour de la requête **% temps processeur** pour hello sélectionné uniquement de deux ordinateurs.</span><span class="sxs-lookup"><span data-stu-id="19e0a-175">Similarly, this hello following query return **% CPU Time** for hello selected two computers only.</span></span>

```
CounterName="% Processor Time"  AND InstanceName="_Total" AND (Computer=SERVER1.contoso.com OR Computer=SERVER2.contoso.com)
```

### <a name="field-types"></a><span data-ttu-id="19e0a-176">Types de champ</span><span class="sxs-lookup"><span data-stu-id="19e0a-176">Field types</span></span>
<span data-ttu-id="19e0a-177">Lors de la création de filtres, vous devez comprendre les différences de hello à l’utilisation des différents types de champs retournés par les recherches de journal.</span><span class="sxs-lookup"><span data-stu-id="19e0a-177">When creating filters, you should understand hello differences in working with different types of fields returned by log searches.</span></span>

<span data-ttu-id="19e0a-178">Les **champs interrogeables** s’affichent en bleu dans les résultats de la recherche.</span><span class="sxs-lookup"><span data-stu-id="19e0a-178">**Searchable fields** show in blue in search results.</span></span>  <span data-ttu-id="19e0a-179">Vous pouvez utiliser les champs de recherche dans le champ de toohello spécifique de conditions de recherche tels que les suivants hello :</span><span class="sxs-lookup"><span data-stu-id="19e0a-179">You can use searchable fields in search conditions specific toohello field such as hello following:</span></span>

```
Type: Event EventLevelName: "Error"
Type: SecurityEvent Computer:Contains("contoso.com")
Type: Event EventLevelName IN {"Error","Warning"}
```

<span data-ttu-id="19e0a-180">Les **champs interrogeables en texte libre** s’affichent en gris dans les résultats de la recherche.</span><span class="sxs-lookup"><span data-stu-id="19e0a-180">**Free text searchable fields** are shown in grey in search results.</span></span>  <span data-ttu-id="19e0a-181">Ils ne peuvent pas être utilisés avec le champ de toohello spécifique de conditions de recherche telles que des champs de recherche.</span><span class="sxs-lookup"><span data-stu-id="19e0a-181">They cannot be used with search conditions specific toohello field like searchable fields.</span></span>  <span data-ttu-id="19e0a-182">Recherche uniquement lors d’une requête pour tous les champs tels que les suivants hello.</span><span class="sxs-lookup"><span data-stu-id="19e0a-182">They are only searched when performing a query across all fields such as hello following.</span></span>

```
"Error"
Type: Event "Exception"
```


### <a name="boolean-operators"></a><span data-ttu-id="19e0a-183">Opérateurs booléens</span><span class="sxs-lookup"><span data-stu-id="19e0a-183">Boolean operators</span></span>
<span data-ttu-id="19e0a-184">Avec les champs numériques et DateHeure, vous pouvez rechercher des valeurs à l’aide d’opérateurs *supérieur à*, *inférieur à* et *inférieur ou égal à*.</span><span class="sxs-lookup"><span data-stu-id="19e0a-184">With datetime and numeric fields, you can search for values using *greater than*, *lesser than*, and *lesser than or equal*.</span></span> <span data-ttu-id="19e0a-185">Vous pouvez utiliser des opérateurs simples tels que >, <>, =, < =, ! = dans la barre de recherche de requête hello.</span><span class="sxs-lookup"><span data-stu-id="19e0a-185">You can use simple operators such as >, < , >=, <= , != in hello query search bar.</span></span>

<span data-ttu-id="19e0a-186">Vous pouvez interroger un journal des événements spécifique pour une période spécifique.</span><span class="sxs-lookup"><span data-stu-id="19e0a-186">You can query a specific event log for a specific period of time.</span></span> <span data-ttu-id="19e0a-187">Par exemple, hello des dernières 24 heures est exprimé par hello expression mnémonique suivante.</span><span class="sxs-lookup"><span data-stu-id="19e0a-187">For example, hello last 24 hours is expressed with hello following mnemonic expression.</span></span>

```
EventLog=System TimeGenerated>NOW-24HOURS
```


#### <a name="toosearch-using-a-boolean-operator"></a><span data-ttu-id="19e0a-188">toosearch à l’aide d’un opérateur booléen</span><span class="sxs-lookup"><span data-stu-id="19e0a-188">toosearch using a boolean operator</span></span>
* <span data-ttu-id="19e0a-189">Dans le champ de requête de recherche hello, tapez`EventLog=System TimeGenerated>NOW-24HOURS`</span><span class="sxs-lookup"><span data-stu-id="19e0a-189">In hello search query field, type `EventLog=System TimeGenerated>NOW-24HOURS`</span></span>  
    <span data-ttu-id="19e0a-190">![Recherche avec des opérateurs boléens](./media/log-analytics-log-searches/oms-search-boolean.png)</span><span class="sxs-lookup"><span data-stu-id="19e0a-190">![search with boolean](./media/log-analytics-log-searches/oms-search-boolean.png)</span></span>

<span data-ttu-id="19e0a-191">Vous pouvez contrôler hello intervalle de temps sous forme graphique et la plupart du temps, vous pourriez toodo que, il n’y avantages tooincluding un filtre de temps directement dans la requête de hello.</span><span class="sxs-lookup"><span data-stu-id="19e0a-191">Although you can control hello time interval graphically, and most times you might want toodo that, there are advantages tooincluding a time filter directly into hello query.</span></span> <span data-ttu-id="19e0a-192">Par exemple, cela fonctionne très bien avec les tableaux de bord où vous pouvez remplacer le temps de hello pour chaque vignette, quel que soit hello *global* sélecteur d’heure sur la page du tableau de bord hello.</span><span class="sxs-lookup"><span data-stu-id="19e0a-192">For example, this works great with dashboards where you can override hello time for each tile, regardless of hello *global* time selector on hello dashboard page.</span></span> <span data-ttu-id="19e0a-193">Pour plus d'informations, consultez [Questions relatives au temps dans le tableau de bord](http://cloudadministrator.wordpress.com/2014/10/19/system-center-advisor-restarted-time-matters-in-dashboard-part-6/).</span><span class="sxs-lookup"><span data-stu-id="19e0a-193">For more information, see [Time Matters in Dashboard](http://cloudadministrator.wordpress.com/2014/10/19/system-center-advisor-restarted-time-matters-in-dashboard-part-6/).</span></span>

<span data-ttu-id="19e0a-194">Lorsque le filtrage par heure, gardez à l’esprit que vous obtenez des résultats pour hello *intersection* Hello deux périodes : celle spécifiée dans le portail OMS (S1) est hello hello et hello celui spécifié dans la requête de hello (S2).</span><span class="sxs-lookup"><span data-stu-id="19e0a-194">When filtering by time, keep in mind that you get results for hello *intersection* of hello two time periods: hello one specified in hello OMS portal (S1) and hello one specified in hello query (S2).</span></span>

![intersection](./media/log-analytics-log-searches/oms-search-intersection.png)

<span data-ttu-id="19e0a-196">Cela signifie que, si hello deux périodes ne se chevauchent, par exemple dans le portail OMS de hello où vous choisissez **cette semaine** et dans la requête hello où vous définissez **semaine dernière**, il n’existe aucune intersection et vous ne serez pas réception des résultats.</span><span class="sxs-lookup"><span data-stu-id="19e0a-196">This means, if hello time periods don’t intersect, for example in hello OMS portal where you choose **This week** and in hello query where you define **last week**, then there is no intersection and you won't receive any results.</span></span>

<span data-ttu-id="19e0a-197">Opérateurs de comparaison utilisés pour le champ TimeGenerated de hello sont également utiles dans d’autres situations.</span><span class="sxs-lookup"><span data-stu-id="19e0a-197">Comparison operators used for hello TimeGenerated field are also useful in other situations.</span></span> <span data-ttu-id="19e0a-198">Par exemple, avec des champs numériques.</span><span class="sxs-lookup"><span data-stu-id="19e0a-198">For example, with numeric fields.</span></span>

<span data-ttu-id="19e0a-199">Par exemple, étant donné que les alertes d’évaluation de la Configuration ont hello des valeurs de gravité suivantes :</span><span class="sxs-lookup"><span data-stu-id="19e0a-199">For example, given that Configuration Assessment’s alerts have hello following severity values:</span></span>

* <span data-ttu-id="19e0a-200">0 = Information</span><span class="sxs-lookup"><span data-stu-id="19e0a-200">0 = Information</span></span>
* <span data-ttu-id="19e0a-201">1 = Avertissement</span><span class="sxs-lookup"><span data-stu-id="19e0a-201">1 = Warning</span></span>
* <span data-ttu-id="19e0a-202">2 = Critique</span><span class="sxs-lookup"><span data-stu-id="19e0a-202">2 = Critical</span></span>

<span data-ttu-id="19e0a-203">Vous pouvez interroger pour les alertes d’avertissement et critiques et exclure également les alertes d’information avec hello suivant la requête :</span><span class="sxs-lookup"><span data-stu-id="19e0a-203">You can query for both warning and critical alerts and also exclude informational ones with hello following query:</span></span>

```
Type=ConfigurationAlert  Severity>=1
```


<span data-ttu-id="19e0a-204">Vous pouvez aussi utiliser des requêtes de plage de données.</span><span class="sxs-lookup"><span data-stu-id="19e0a-204">You can also use range queries.</span></span> <span data-ttu-id="19e0a-205">Cela signifie que vous pouvez fournir la plage de début et de fin de hello de valeurs dans une séquence.</span><span class="sxs-lookup"><span data-stu-id="19e0a-205">This means that you can provide hello beginning and end range of values in a sequence.</span></span> <span data-ttu-id="19e0a-206">Par exemple, si vous souhaitez que les événements du journal des événements Operations Manager hello où hello EventID est too2100 supérieur ou égal mais non supérieur à 2199, puis hello suivant la requête va alors les retourner.</span><span class="sxs-lookup"><span data-stu-id="19e0a-206">For example, if you want events from hello Operations Manager event log where hello EventID is greater than or equal too2100 but not greater than 2199, then hello following query would return them.</span></span>

```
Type=Event EventLog="Operations Manager" EventID:[2100..2199]
```


> [!NOTE]
> <span data-ttu-id="19e0a-207">syntaxe de plage de Hello vous devez utiliser est le séparateur field : value de deux-points ( :)) hello et *pas* hello égal signe (=).</span><span class="sxs-lookup"><span data-stu-id="19e0a-207">hello range syntax you must use is hello colon (:) field:value separator and *not* hello equal sign (=).</span></span> <span data-ttu-id="19e0a-208">Placez l’extrémité supérieure et inférieure de hello de plage de hello crochets et séparez-les par deux points (..).</span><span class="sxs-lookup"><span data-stu-id="19e0a-208">Enclose hello lower and upper end of hello range in square brackets and separate them with two periods (..).</span></span>
>
>

## <a name="manipulate-search-results"></a><span data-ttu-id="19e0a-209">Manipulation des résultats de la recherche</span><span class="sxs-lookup"><span data-stu-id="19e0a-209">Manipulate search results</span></span>
<span data-ttu-id="19e0a-210">Lorsque vous recherchez des données, vous souhaitez toorefine votre requête de recherche et avoir un bon niveau de contrôle sur les résultats hello.</span><span class="sxs-lookup"><span data-stu-id="19e0a-210">When you're searching for data, you'll want toorefine your search query and have a good level of control over hello results.</span></span> <span data-ttu-id="19e0a-211">Lorsque les résultats sont récupérés, vous pouvez appliquer des commandes tootransform les.</span><span class="sxs-lookup"><span data-stu-id="19e0a-211">When results are retrieved, you can apply commands tootransform them.</span></span>

<span data-ttu-id="19e0a-212">Commandes dans les recherches de journal Analytique *doit* suivre après hello barre verticale (|).</span><span class="sxs-lookup"><span data-stu-id="19e0a-212">Commands in Log Analytics searches *must* follow after hello vertical pipe character (|).</span></span> <span data-ttu-id="19e0a-213">Un filtre doit toujours être la première partie de hello de chaîne de requête.</span><span class="sxs-lookup"><span data-stu-id="19e0a-213">A filter must always be hello first part of a query string.</span></span> <span data-ttu-id="19e0a-214">Il définit le jeu de données hello avec lequel vous travaillez et « dirige ensuite « ces résultats dans une ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="19e0a-214">It defines hello data set you're working with and then "pipes" those results into a command.</span></span> <span data-ttu-id="19e0a-215">Vous pouvez ensuite utiliser des commandes supplémentaires hello canal tooadd.</span><span class="sxs-lookup"><span data-stu-id="19e0a-215">You can then use hello pipe tooadd additional commands.</span></span> <span data-ttu-id="19e0a-216">Il s’agit de pipeline de Windows PowerShell toohello relativement similaire.</span><span class="sxs-lookup"><span data-stu-id="19e0a-216">This is loosely similar toohello Windows PowerShell pipeline.</span></span>

<span data-ttu-id="19e0a-217">En règle générale, hello langage de recherche Analytique de journal tente de toomake de style et les instructions de PowerShell toofollow toohello similaire d’informatique informatique les avantages et courbe d’apprentissage tooease hello.</span><span class="sxs-lookup"><span data-stu-id="19e0a-217">In general, hello Log Analytics search language tries toofollow PowerShell style and guidelines toomake it similar toohello IT pros, and tooease hello learning curve.</span></span>

<span data-ttu-id="19e0a-218">Le nom des commandes est un verbe, ce qui vous permet de connaître facilement leur fonction.</span><span class="sxs-lookup"><span data-stu-id="19e0a-218">Commands have names of verbs so you can easily tell what they do.</span></span>  

### <a name="sort"></a><span data-ttu-id="19e0a-219">Trier</span><span class="sxs-lookup"><span data-stu-id="19e0a-219">Sort</span></span>
<span data-ttu-id="19e0a-220">commande de tri Hello vous permet de hello toodefine ordre par un ou plusieurs champs de tri.</span><span class="sxs-lookup"><span data-stu-id="19e0a-220">hello sort command allows you toodefine hello sorting order by one or multiple fields.</span></span> <span data-ttu-id="19e0a-221">Même si vous ne l'utilisez pas, un ordre de temps décroissant est appliqué par défaut.</span><span class="sxs-lookup"><span data-stu-id="19e0a-221">Even if you don’t use it, by default, a time descending order is enforced.</span></span> <span data-ttu-id="19e0a-222">les résultats les plus récents Hello sont toujours en haut de hello des résultats de recherche.</span><span class="sxs-lookup"><span data-stu-id="19e0a-222">hello most recent results are always at hello top of search results.</span></span> <span data-ttu-id="19e0a-223">Cela signifie que lorsque vous exécutez une recherche avec `Type=Event EventID=1234` , ce qui est réellement exécuté pour vous est :</span><span class="sxs-lookup"><span data-stu-id="19e0a-223">This means that when you run a search, with `Type=Event EventID=1234` what really is executed for you is:</span></span>

```
Type=Event EventID=1234 **| Sort TimeGenerated desc**
```

<span data-ttu-id="19e0a-224">C'est-à-dire, car il est de type hello d’expérience que vous connaissez avec les journaux.</span><span class="sxs-lookup"><span data-stu-id="19e0a-224">That's because it is hello type of experience you are familiar with in logs.</span></span> <span data-ttu-id="19e0a-225">Par exemple, dans hello Observateur d’événements Windows.</span><span class="sxs-lookup"><span data-stu-id="19e0a-225">For example, in hello Windows Event Viewer.</span></span>

<span data-ttu-id="19e0a-226">Vous pouvez utiliser le tri toochange hello moyen résultats sont retournés.</span><span class="sxs-lookup"><span data-stu-id="19e0a-226">You can use Sort toochange hello way results are returned.</span></span> <span data-ttu-id="19e0a-227">Hello exemples suivants montrent comment cela fonctionne.</span><span class="sxs-lookup"><span data-stu-id="19e0a-227">hello following examples show how this works.</span></span>

```
Type=Event EventID=1234 | Sort TimeGenerated asc
```

```
Type=Event EventID=1234 | Sort Computer asc
```

```
Type=Event EventID=1234 | Sort Computer asc,TimeGenerated desc
```


<span data-ttu-id="19e0a-228">Hello simples exemples ci-dessus vous montrent comment des commandes : elles modifient forme hello de résultats hello hello filtre retourné.</span><span class="sxs-lookup"><span data-stu-id="19e0a-228">hello simple examples above show you how commands work--they change hello shape of hello results that hello filter returned.</span></span>

### <a name="limit-and-top"></a><span data-ttu-id="19e0a-229">Limit et Top</span><span class="sxs-lookup"><span data-stu-id="19e0a-229">Limit and top</span></span>
<span data-ttu-id="19e0a-230">Une autre commande moins connue est LIMIT.</span><span class="sxs-lookup"><span data-stu-id="19e0a-230">Another less known command is LIMIT.</span></span> <span data-ttu-id="19e0a-231">Limit est un verbe similaire à PowerShell.</span><span class="sxs-lookup"><span data-stu-id="19e0a-231">Limit is a PowerShell-like verb.</span></span> <span data-ttu-id="19e0a-232">Limite est de commande TOP toohello fonctionnellement identique.</span><span class="sxs-lookup"><span data-stu-id="19e0a-232">Limit is functionally identical toohello TOP command.</span></span> <span data-ttu-id="19e0a-233">Hello requêtes suivantes retournent hello mêmes résultats.</span><span class="sxs-lookup"><span data-stu-id="19e0a-233">hello following queries return hello same results.</span></span>

```
Type=Event EventID=600 | Limit 1
```

```
Type=Event EventID=600 | Top 1
```


#### <a name="toosearch-using-top"></a><span data-ttu-id="19e0a-234">toosearch à l’aide de top</span><span class="sxs-lookup"><span data-stu-id="19e0a-234">toosearch using top</span></span>
* <span data-ttu-id="19e0a-235">Dans le champ de requête de recherche hello, tapez`Type=Event EventID=600 | Top 1` </span><span class="sxs-lookup"><span data-stu-id="19e0a-235">In hello search query field, type `Type=Event EventID=600 | Top 1` </span></span>  
    <span data-ttu-id="19e0a-236">![Recherche top](./media/log-analytics-log-searches/oms-search-top.png)</span><span class="sxs-lookup"><span data-stu-id="19e0a-236">![search top](./media/log-analytics-log-searches/oms-search-top.png)</span></span>

<span data-ttu-id="19e0a-237">Dans l’image hello ci-dessus, il existe 358 mille enregistrements avec EventID = 600.</span><span class="sxs-lookup"><span data-stu-id="19e0a-237">In hello image above, there are 358 thousand records with EventID=600.</span></span> <span data-ttu-id="19e0a-238">Hello des champs, les facettes et les filtres sur hello gauche toujours des informations sur les résultats de hello *par partie du filtre hello* de requête de hello, qui fait partie de hello avant une barre verticale.</span><span class="sxs-lookup"><span data-stu-id="19e0a-238">hello fields, facets, and filters on hello left always show information about hello results returned *by hello filter portion* of hello query, which is hello part before any pipe character.</span></span> <span data-ttu-id="19e0a-239">Hello **résultats** volet retourne uniquement le résultat de hello 1 plus récente, parce que l’exemple de commande hello a formé et transformé les résultats hello.</span><span class="sxs-lookup"><span data-stu-id="19e0a-239">hello **Results** pane only returns hello most recent 1 result, because hello example command shaped and transformed hello results.</span></span>

### <a name="select"></a><span data-ttu-id="19e0a-240">Sélectionnez</span><span class="sxs-lookup"><span data-stu-id="19e0a-240">Select</span></span>
<span data-ttu-id="19e0a-241">commande SELECT Hello se comporte comme Select-Object dans PowerShell.</span><span class="sxs-lookup"><span data-stu-id="19e0a-241">hello SELECT command behaves like Select-Object in PowerShell.</span></span> <span data-ttu-id="19e0a-242">Elle retourne des résultats filtrés qui n'ont pas toutes leurs propriétés d'origine.</span><span class="sxs-lookup"><span data-stu-id="19e0a-242">It returns filtered results that do not have all of their original properties.</span></span> <span data-ttu-id="19e0a-243">Au lieu de cela, elle sélectionne uniquement les propriétés de hello que vous spécifiez.</span><span class="sxs-lookup"><span data-stu-id="19e0a-243">Instead, it selects only hello properties that you specify.</span></span>

#### <a name="toorun-a-search-using-hello-select-command"></a><span data-ttu-id="19e0a-244">toorun une recherche à l’aide de la commande select hello</span><span class="sxs-lookup"><span data-stu-id="19e0a-244">toorun a search using hello select command</span></span>
1. <span data-ttu-id="19e0a-245">Dans Rechercher, tapez `Type=Event` puis cliquez sur **Rechercher**.</span><span class="sxs-lookup"><span data-stu-id="19e0a-245">In Search, type `Type=Event` and then click **Search**.</span></span>
2. <span data-ttu-id="19e0a-246">Cliquez sur **+ afficher plus** dans un des tooview de résultats hello toutes les propriétés de hello qui hello des résultats.</span><span class="sxs-lookup"><span data-stu-id="19e0a-246">Click **+ show more** in one of hello results tooview all hello properties that hello results have.</span></span>
3. <span data-ttu-id="19e0a-247">Sélectionnez certains d'entre eux explicitement et hello modifications de la requête trop`Type=Event | Select Computer,EventID,RenderedDescription`.</span><span class="sxs-lookup"><span data-stu-id="19e0a-247">Select some of those explicitly, and hello query changes too`Type=Event | Select Computer,EventID,RenderedDescription`.</span></span>  
    <span data-ttu-id="19e0a-248">![Recherche select](./media/log-analytics-log-searches/oms-search-select.png)</span><span class="sxs-lookup"><span data-stu-id="19e0a-248">![search select](./media/log-analytics-log-searches/oms-search-select.png)</span></span>

<span data-ttu-id="19e0a-249">Cette commande est particulièrement utile lorsque vous souhaitez que les résultats de recherche toocontrol et choisissez uniquement les parties de hello des données qui importent vraiment pour votre exploration et qui n’est pas souvent d’enregistrement complet de hello.</span><span class="sxs-lookup"><span data-stu-id="19e0a-249">This command is particularly useful when you want toocontrol search output and choose only hello portions of data that really matter for your exploration, which often isn’t hello full record.</span></span> <span data-ttu-id="19e0a-250">Elle est également utile lorsque des enregistrements de différents types présentent *certaines* propriétés communes, mais que leurs propriétés ne sont pas *toutes* communes.</span><span class="sxs-lookup"><span data-stu-id="19e0a-250">This is also useful when records of different types have *some* common properties, but not *all* of their properties are common.</span></span> <span data-ttu-id="19e0a-251">Base de données, vous pouvez générer des résultats qui ressemblent plus naturellement à une table ou fonctionnent bien lorsqu’exporté tooa un fichier CSV puis envoyés dans Excel.</span><span class="sxs-lookup"><span data-stu-id="19e0a-251">The, you can generate output that looks more naturally like a table, or work well when exported tooa CSV file and then massaged in Excel.</span></span>

## <a name="use-hello-measure-command"></a><span data-ttu-id="19e0a-252">Utilisez la commande de mesure hello</span><span class="sxs-lookup"><span data-stu-id="19e0a-252">Use hello measure command</span></span>
<span data-ttu-id="19e0a-253">MESURE est une des commandes plus polyvalentes hello dans les recherches de journal Analytique.</span><span class="sxs-lookup"><span data-stu-id="19e0a-253">MEASURE is one of hello most versatile commands in Log Analytics searches.</span></span> <span data-ttu-id="19e0a-254">Il vous permet de tooapply statistique *fonctions* tooyour données et agréger les résultats sont regroupés par champ donné.</span><span class="sxs-lookup"><span data-stu-id="19e0a-254">It allows you tooapply statistical *functions* tooyour data and aggregate results grouped by a given field.</span></span> <span data-ttu-id="19e0a-255">Il existe plusieurs fonctions statistiques qui prennent en charge Measure.</span><span class="sxs-lookup"><span data-stu-id="19e0a-255">There are multiple statistical functions that Measure supports.</span></span>

### <a name="measure-count"></a><span data-ttu-id="19e0a-256">La fonction count() de Measure</span><span class="sxs-lookup"><span data-stu-id="19e0a-256">Measure count()</span></span>
<span data-ttu-id="19e0a-257">Hello la première fonction statistique toowork, avec un des toounderstand la plus simple de hello est donc hello *count()* (fonction).</span><span class="sxs-lookup"><span data-stu-id="19e0a-257">hello first statistical function toowork with, and one of hello simplest toounderstand is hello *count()* function.</span></span>

<span data-ttu-id="19e0a-258">Les résultats d’une requête de recherche telle que `Type=Event`, affichent des filtres, également appelés facettes, sur hello gauche des résultats de recherche.</span><span class="sxs-lookup"><span data-stu-id="19e0a-258">Results from any search query such as `Type=Event`, show filters also called facets on hello left side of search results.</span></span> <span data-ttu-id="19e0a-259">Hello filtres montrent une distribution de valeurs pour les résultats hello un champ donné dans hello recherche exécutée.</span><span class="sxs-lookup"><span data-stu-id="19e0a-259">hello filters show a distribution of values by a given field for hello results in hello search executed.</span></span>

![Recherche measure count](./media/log-analytics-log-searches/oms-search-measure-count01.png)

<span data-ttu-id="19e0a-261">Par exemple, Bonjour image ci-dessus, vous verrez hello **ordinateur** champ qui montre que dans les événements de presque 739 mille hello dans les résultats de hello, sont des valeurs uniques et distinctes 68 pour hello **ordinateur** champ dans ces enregistrements.</span><span class="sxs-lookup"><span data-stu-id="19e0a-261">For example, in hello image above you'll see hello **Computer** field and it shows that within hello almost 739 thousand events in hello results, there are 68 unique and distinct values for hello **Computer** field in those records.</span></span> <span data-ttu-id="19e0a-262">vignette de Hello affiche uniquement hello top 5, qui sont hello 5 valeurs les plus courantes écrites dans hello **ordinateur** champs), triées par nombre hello de documents contenant cette valeur spécifique dans ce champ.</span><span class="sxs-lookup"><span data-stu-id="19e0a-262">hello tile only shows hello top 5, which are hello most common 5 values that are written in hello **Computer** fields), sorted by hello number of documents that contain that specific value in that field.</span></span> <span data-ttu-id="19e0a-263">Dans l’image de hello vous pouvez voir que, parmi ces événements presque 369 mille, 90 mille proviennent hello OpsInsights04.contoso.com ordinateur, des milliers de 83 à partir de l’ordinateur de DB03.contoso.com hello et ainsi de suite.</span><span class="sxs-lookup"><span data-stu-id="19e0a-263">In hello image you can see that – among those almost 369 thousand events – 90 thousand come from hello OpsInsights04.contoso.com computer, 83 thousand from hello DB03.contoso.com computer, and so on.</span></span>

<span data-ttu-id="19e0a-264">Que se passe-t-il si vous souhaitez toosee toutes les valeurs, étant donné que les mosaïques hello montre uniquement hello uniquement les 5 premières ?</span><span class="sxs-lookup"><span data-stu-id="19e0a-264">What if you want toosee all values, since hello tile only shows only hello top 5?</span></span>

<span data-ttu-id="19e0a-265">Qui est quelle mesure hello commande permet de faire avec la fonction count() de hello.</span><span class="sxs-lookup"><span data-stu-id="19e0a-265">That’s what hello measure command can do with hello count() function.</span></span> <span data-ttu-id="19e0a-266">Cette fonction n'utilise aucun paramètre.</span><span class="sxs-lookup"><span data-stu-id="19e0a-266">This function doesn't use any parameters.</span></span> <span data-ttu-id="19e0a-267">Vous spécifiez simplement le champ hello en fonction duquel vous voulez toogroup par : hello **ordinateur** champ dans ce cas :</span><span class="sxs-lookup"><span data-stu-id="19e0a-267">You just specify hello field by which you want toogroup by – hello **Computer** field in this case:</span></span>

`Type=Event | Measure count() by Computer`

![Recherche measure count](./media/log-analytics-log-searches/oms-search-measure-count-computer.png)

<span data-ttu-id="19e0a-269">Le champ **Computer** est toutefois simplement un champ utilisé *dans* chaque élément de données : aucune base de données relationnelle n’est impliquée, et il n’existe aucun objet **Computer**distinct nulle part.</span><span class="sxs-lookup"><span data-stu-id="19e0a-269">However, **Computer** is just a field used *in* each piece of data – there are no relational databases involved and there is no separate **Computer** object anywhere.</span></span> <span data-ttu-id="19e0a-270">Hello simplement les valeurs *dans* hello données peuvent décrire quelle entité a générées, ainsi que plusieurs autres caractéristiques et aspects des données de hello : hello donc terme *facette*.</span><span class="sxs-lookup"><span data-stu-id="19e0a-270">Just hello values *in* hello data can describe which entity generated them, and a number of other characteristics and aspects of hello data – hence hello term *facet*.</span></span> <span data-ttu-id="19e0a-271">Toutefois, vous pouvez également les regrouper par d'autres champs.</span><span class="sxs-lookup"><span data-stu-id="19e0a-271">However, you can just as well group by other fields.</span></span> <span data-ttu-id="19e0a-272">Étant donné que les résultats d’origine de hello de presque 739 milliers d’événements transmis dans la commande de mesure hello ont également un champ appelé **EventID**, vous pouvez appliquer hello même toogroup technique par ce champ et obtenir le nombre d’événements par ID d’événement :</span><span class="sxs-lookup"><span data-stu-id="19e0a-272">Because hello original results of almost 739 thousand events that are piped into hello measure command also have a field called **EventID**, you can apply hello same technique toogroup by that field and get a count of events by EventID:</span></span>

```
Type=Event | Measure count() by EventID
```

<span data-ttu-id="19e0a-273">Si vous n’êtes pas intéressé par nombre d’enregistrements réels hello qui contiennent une valeur spécifique, mais à la place si vous souhaitez seulement une liste de hello valeurs elles-mêmes, vous pouvez ajouter un *sélectionnez* à la fin de hello d’elle et sélectionnez simplement hello première colonne :</span><span class="sxs-lookup"><span data-stu-id="19e0a-273">If you're not interested in hello actual record count that contain a specific value, but instead if you only want a list of hello values themselves, you can add a *Select* command at hello end of it and just select hello first column:</span></span>

```
Type=Event | Measure count() by EventID | Select EventID
```

<span data-ttu-id="19e0a-274">Puis vous pouvez obtenir plus complexes et des résultats de tri hello dans requête de hello, ou vous pouvez aussi simplement cliquer sur les colonnes dans la grille de hello, hello.</span><span class="sxs-lookup"><span data-stu-id="19e0a-274">Then you can get more intricate and pre-sort hello results in hello query, or you can just click hello columns in hello grid, too.</span></span>

```
Type=Event | Measure count() by EventID | Select EventID | Sort EventID asc
```

#### <a name="toosearch-using-measure-count"></a><span data-ttu-id="19e0a-275">toosearch à l’aide de la mesure nombre</span><span class="sxs-lookup"><span data-stu-id="19e0a-275">toosearch using measure count</span></span>
* <span data-ttu-id="19e0a-276">Dans le champ de requête de recherche hello, tapez`Type=Event | Measure count() by EventID`</span><span class="sxs-lookup"><span data-stu-id="19e0a-276">In hello search query field, type `Type=Event | Measure count() by EventID`</span></span>
* <span data-ttu-id="19e0a-277">Ajouter `| Select EventID` fin toohello de requête de hello.</span><span class="sxs-lookup"><span data-stu-id="19e0a-277">Append `| Select EventID` toohello end of hello query.</span></span>
* <span data-ttu-id="19e0a-278">Enfin, ajoutez `| Sort EventID asc` fin toohello de requête de hello.</span><span class="sxs-lookup"><span data-stu-id="19e0a-278">Finally, append `| Sort EventID asc` toohello end of hello query.</span></span>

<span data-ttu-id="19e0a-279">Il existe quelques points importants toonotice et mettre en évidence :</span><span class="sxs-lookup"><span data-stu-id="19e0a-279">There are a couple important points toonotice and emphasize:</span></span>

<span data-ttu-id="19e0a-280">Tout d’abord, les résultats hello que vous voyez ne sont pas résultats bruts d’origine de hello plus.</span><span class="sxs-lookup"><span data-stu-id="19e0a-280">First, hello results you see are not hello original raw results anymore.</span></span> <span data-ttu-id="19e0a-281">Il s’agit en fait de résultats agrégés : autrement dit, des groupes de résultats.</span><span class="sxs-lookup"><span data-stu-id="19e0a-281">Instead, they are aggregated results – essentially groups of results.</span></span> <span data-ttu-id="19e0a-282">Ce n’est pas un problème, mais vous devez comprendre que vous interagissez avec une toute autre forme de données qui diffère de hello forme brute d’origine créée en volée hello en raison de la fonction d’agrégation ou statistique est utilisée hello.</span><span class="sxs-lookup"><span data-stu-id="19e0a-282">This isn't a problem, but you should understand that you're interacting with a very different shape of data that differs from hello original raw shape that gets created on hello fly as a result of hello aggregation/statistical function.</span></span>

<span data-ttu-id="19e0a-283">Ensuite, **mesurer le nombre** actuellement retourne hello uniquement les premiers résultats distincts 100.</span><span class="sxs-lookup"><span data-stu-id="19e0a-283">Second, **Measure count** currently returns only hello top 100 distinct results.</span></span> <span data-ttu-id="19e0a-284">Cette limite ne s’applique pas toohello autres fonctions statistiques.</span><span class="sxs-lookup"><span data-stu-id="19e0a-284">This limit does not apply toohello other statistical functions.</span></span> <span data-ttu-id="19e0a-285">Par conséquent, vous devez généralement toouse un toosearch premier filtre plus précis pour des éléments spécifiques avant d’appliquer measure count().</span><span class="sxs-lookup"><span data-stu-id="19e0a-285">So, you'll usually need toouse a more precise filter first toosearch for specific items before you apply measure count().</span></span>

## <a name="use-hello-max-and-min-functions-with-hello-measure-command"></a><span data-ttu-id="19e0a-286">Utilisez les fonctions min et max hello avec la commande de mesure hello</span><span class="sxs-lookup"><span data-stu-id="19e0a-286">Use hello max and min functions with hello measure command</span></span>
<span data-ttu-id="19e0a-287">Il existe plusieurs situations où les commandes **Measure Max()** et **Measure Min()** sont utiles.</span><span class="sxs-lookup"><span data-stu-id="19e0a-287">There are various scenarios where **Measure Max()** and **Measure Min()** are useful.</span></span> <span data-ttu-id="19e0a-288">Toutefois, étant donné que chaque fonction est l'opposé de l'autre, nous démontrerons la fonction Max() et vous pourrez ensuite tester vous-même la fonction Min().</span><span class="sxs-lookup"><span data-stu-id="19e0a-288">However, since each function is opposite of each other, we'll illustrate Max() and you can experiment with Min() on your own.</span></span>

<span data-ttu-id="19e0a-289">Si vous interrogez des événements de sécurité, ceux-ci ont une propriété **Level** qui peut varier.</span><span class="sxs-lookup"><span data-stu-id="19e0a-289">If you query for security events, they have a **Level** property that can vary.</span></span> <span data-ttu-id="19e0a-290">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="19e0a-290">For example:</span></span>

```
Type=SecurityEvent
```

![Recherche du début de la fonction measure count](./media/log-analytics-log-searches/oms-search-measure-max01.png)

<span data-ttu-id="19e0a-292">Si vous souhaitez que la valeur plus élevée tooview hello pour tous les de sécurité de hello événements à un même ordinateur, groupe hello par champ, vous pouvez utiliser</span><span class="sxs-lookup"><span data-stu-id="19e0a-292">If you want tooview hello highest value for all of hello security events given a common Computer, hello group by field, you can use</span></span>

```
Type=ConfigurationAlert | Measure Max(Level) by Computer
```

![Recherche l’ordinateur de la fonction measure max](./media/log-analytics-log-searches/oms-search-measure-max02.png)

<span data-ttu-id="19e0a-294">Il affichera que pour les ordinateurs hello ayant **niveau** enregistrements, la plupart d'entre eux ont au moins 8, le niveau nombreuses avaient un niveau de 16.</span><span class="sxs-lookup"><span data-stu-id="19e0a-294">It will display that for hello computers that had **Level** records, most of them have at least level 8, many had a level of 16.</span></span>

```
Type=ConfigurationAlert | Measure Max(Severity) by Computer
```

![Recherche l’ordinateur qui génère la valeur horaire measure max](./media/log-analytics-log-searches/oms-search-measure-max03.png)

<span data-ttu-id="19e0a-296">Cette fonction fonctionne bien avec les nombres, mais elle fonctionne également avec les champs DateHeure.</span><span class="sxs-lookup"><span data-stu-id="19e0a-296">This function works well with numbers, but it also works with DateTime fields.</span></span> <span data-ttu-id="19e0a-297">C’est le dernier toocheck utile pour hello ou plus récent horodatage pour tout type de données indexé pour chaque ordinateur.</span><span class="sxs-lookup"><span data-stu-id="19e0a-297">It is useful toocheck for hello last or most recent time stamp for any piece of data indexed for each computer.</span></span> <span data-ttu-id="19e0a-298">Par exemple : lorsque l’événement sécurité hello plus récent a été signalée pour chaque machine ?</span><span class="sxs-lookup"><span data-stu-id="19e0a-298">For example: When was hello most recent security event reported for each machine?</span></span>

```
Type=ConfigurationChange | Measure Max(TimeGenerated) by Computer
```

## <a name="use-hello-avg-function-with-hello-measure-command"></a><span data-ttu-id="19e0a-299">Utilisez avg, fonction hello avec la commande de mesure hello</span><span class="sxs-lookup"><span data-stu-id="19e0a-299">Use hello avg function with hello measure command</span></span>
<span data-ttu-id="19e0a-300">Hello fonction statistique Avg() utilisée avec measure vous permet de valeur moyenne de toocalculate hello pour un champ et groupe les résultats par hello même ou un autre champ.</span><span class="sxs-lookup"><span data-stu-id="19e0a-300">hello Avg() statistical function used with measure allows you toocalculate hello average value for some field, and group results by hello same or other field.</span></span> <span data-ttu-id="19e0a-301">Cela est utile dans de nombreux cas, pour les données de performances par exemple.</span><span class="sxs-lookup"><span data-stu-id="19e0a-301">This is useful in a variety of cases, such as performance data.</span></span>

<span data-ttu-id="19e0a-302">Nous allons commencer par les données de performances.</span><span class="sxs-lookup"><span data-stu-id="19e0a-302">We'll start with performance data.</span></span> <span data-ttu-id="19e0a-303">Remarque : OMS collecte actuellement les compteurs de performance pour les ordinateurs Windows et Linux.</span><span class="sxs-lookup"><span data-stu-id="19e0a-303">Note that OMS currently collects performance counters for both Windows and Linux machines.</span></span>

<span data-ttu-id="19e0a-304">toosearch pour *tous les* est de requête la plus simple hello des données de performances :</span><span class="sxs-lookup"><span data-stu-id="19e0a-304">toosearch for *all* performance data, hello most basic query is:</span></span>

```
Type=Perf
```

![Recherche du début de la fonction avg](./media/log-analytics-log-searches/oms-search-avg01.png)

<span data-ttu-id="19e0a-306">Hello première chose que vous remarquerez est qu’Analytique de journal vous montre trois perspectives : liste, qui vous montre ce qui montre les enregistrements réels hello derrière les graphiques hello ; Table, qui affiche une vue tabulaire des données de compteur de performance ; et les mesures, qui affiche des compteurs de performance de graphiques pour hello.</span><span class="sxs-lookup"><span data-stu-id="19e0a-306">hello first thing you'll notice is that Log Analytics shows you three perspectives: List, which shows you which shows hello actual records behind hello charts; Table, which shows a tabular view of performance counter data; and Metrics, which shows charts for hello performance counters.</span></span>

<span data-ttu-id="19e0a-307">Dans l’image hello ci-dessus, il existe deux ensembles de champs marqués qui indiquent les éléments suivants de hello :</span><span class="sxs-lookup"><span data-stu-id="19e0a-307">In hello image above, there are two sets of fields marked that indicate hello following:</span></span>

* <span data-ttu-id="19e0a-308">Hello premier jeu identifie le nom de compteur de Performance Windows, nom de l’objet et nom de l’Instance dans le filtre de requête hello.</span><span class="sxs-lookup"><span data-stu-id="19e0a-308">hello first set identifies Windows Performance Counter Name, Object Name, and Instance Name in hello query filter.</span></span> <span data-ttu-id="19e0a-309">Il s’agit des champs hello que vous utiliserez probablement le plus souvent en tant que facettes ou filtres.</span><span class="sxs-lookup"><span data-stu-id="19e0a-309">These are hello fields you probably will most commonly use as facets/filters</span></span>
* <span data-ttu-id="19e0a-310">**CounterValue** est hello la valeur réelle du compteur de hello.</span><span class="sxs-lookup"><span data-stu-id="19e0a-310">**CounterValue** is hello actual value of hello counter.</span></span> <span data-ttu-id="19e0a-311">Dans cet exemple, la valeur de hello est *75*.</span><span class="sxs-lookup"><span data-stu-id="19e0a-311">In this example, hello value is *75*.</span></span>
* <span data-ttu-id="19e0a-312">**TimeGenerated** a la valeur 12:51, au format 24 heures.</span><span class="sxs-lookup"><span data-stu-id="19e0a-312">**TimeGenerated** is 12:51, in 24-hour time format.</span></span>

<span data-ttu-id="19e0a-313">Voici une vue des mesures hello dans un graphique.</span><span class="sxs-lookup"><span data-stu-id="19e0a-313">Here's a view of hello metrics in a graph.</span></span>

![Recherche du début de la fonction avg](./media/log-analytics-log-searches/oms-search-avg02.png)

<span data-ttu-id="19e0a-315">Après la lecture sur la forme d’enregistrement hello des performances et après avoir lu sur d’autres techniques de recherche, vous pouvez utiliser measure Avg() tooaggregate ce type de données numériques.</span><span class="sxs-lookup"><span data-stu-id="19e0a-315">After reading about hello Perf record shape, and having read about other search techniques, you can use measure Avg() tooaggregate this type of numerical data.</span></span>

<span data-ttu-id="19e0a-316">Voici un exemple simple :</span><span class="sxs-lookup"><span data-stu-id="19e0a-316">Here's a simple example:</span></span>

```
Type=Perf  ObjectName:Processor  InstanceName:_Total  CounterName:"% Processor Time" | Measure Avg(CounterValue) by Computer
```

![Recherche de l’exemple de valeur de la fonction avg](./media/log-analytics-log-searches/oms-search-avg03.png)

<span data-ttu-id="19e0a-318">Dans cet exemple, vous sélectionnez le compteur de performance du temps processeur Total hello et moyenne par ordinateur.</span><span class="sxs-lookup"><span data-stu-id="19e0a-318">In this example, you select hello CPU Total Time performance counter and average by Computer.</span></span> <span data-ttu-id="19e0a-319">Si vous souhaitez toonarrow vers le bas votre hello tooonly de résultats 6 dernières heures, vous pouvez utiliser le contrôle de filtre de temps hello ou spécifiez dans votre requête, comme suit :</span><span class="sxs-lookup"><span data-stu-id="19e0a-319">If you want toonarrow down your results tooonly hello last 6 hours, you can either use hello time filter control or specify in your query as follows:</span></span>

```
Type=Perf  ObjectName:Processor  InstanceName:_Total  CounterName:"% Processor Time" TimeGenerated>NOW-6HOURS | Measure Avg(CounterValue) by Computer
```

### <a name="toosearch-using-hello-avg-function-with-hello-measure-command"></a><span data-ttu-id="19e0a-320">toosearch à l’aide de la fonction avg de hello avec la commande de mesure hello</span><span class="sxs-lookup"><span data-stu-id="19e0a-320">toosearch using hello avg function with hello measure command</span></span>
* <span data-ttu-id="19e0a-321">Dans la zone de requête de recherche hello, tapez `Type=Perf  ObjectName:Processor  InstanceName:_Total  CounterName:"% Processor Time" TimeGenerated>NOW-6HOURS | Measure Avg(CounterValue) by Computer`.</span><span class="sxs-lookup"><span data-stu-id="19e0a-321">In hello Search query box, type `Type=Perf  ObjectName:Processor  InstanceName:_Total  CounterName:"% Processor Time" TimeGenerated>NOW-6HOURS | Measure Avg(CounterValue) by Computer`.</span></span>

<span data-ttu-id="19e0a-322">Vous pouvez agréger et corréler les données *entre* plusieurs ordinateurs.</span><span class="sxs-lookup"><span data-stu-id="19e0a-322">You can aggregate and correlate data *across* computers.</span></span> <span data-ttu-id="19e0a-323">Par exemple, imaginez que vous avez un ensemble d’ordinateurs hôtes dans une sorte de batterie de serveurs où chaque nœud est égal tooany autre et il suffit de faire hello tous les même type de travail et le chargement doit être à peu près équilibrée.</span><span class="sxs-lookup"><span data-stu-id="19e0a-323">For example, imagine that you have a set of hosts in some sort of farm where each node is equal tooany other one and they just do all hello same type of work and load should be roughly balanced.</span></span> <span data-ttu-id="19e0a-324">Vous pouvez obtenir leurs compteurs qu'en une seule fois par hello suivante, interroge et obtenir des moyennes pour l’ensemble de la batterie hello.</span><span class="sxs-lookup"><span data-stu-id="19e0a-324">You could get their counters all in one go with hello following query and get averages for hello entire farm.</span></span> <span data-ttu-id="19e0a-325">Vous pouvez commencer en choisissant les ordinateurs hello avec hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="19e0a-325">You can start by choosing hello computers with hello following example:</span></span>

```
Type=Perf AND (Computer="AzureMktg01" OR Computer="AzureMktg02" OR Computer="AzureMktg03")
```

<span data-ttu-id="19e0a-326">Maintenant que vous avez des ordinateurs de hello, vous ne devez que tooselect deux indicateurs de performance clés (KPI) : l’utilisation du processeur et % d’espace disque libre.</span><span class="sxs-lookup"><span data-stu-id="19e0a-326">Now that you have hello computers, you also only want tooselect two key performance indicators (KPIs): % CPU Usage and % Free Disk Space.</span></span> <span data-ttu-id="19e0a-327">Par conséquent, cette partie de hello requête devient :</span><span class="sxs-lookup"><span data-stu-id="19e0a-327">So, that part of hello query becomes:</span></span>

```
Type=Perf InstanceName:_Total  ((ObjectName:Processor AND CounterName:"% Processor Time") OR (ObjectName="LogicalDisk" AND CounterName="% Free Space")) AND TimeGenerated>NOW-4HOURS
```

<span data-ttu-id="19e0a-328">Vous pouvez maintenant ajouter les compteurs et les ordinateurs avec hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="19e0a-328">Now you can add computers and counters with hello following example:</span></span>

```
Type=Perf InstanceName:_Total  ((ObjectName:Processor AND CounterName:"% Processor Time") OR (ObjectName="LogicalDisk" AND CounterName="% Free Space")) AND TimeGenerated>NOW-4HOURS AND (Computer="AzureMktg01" OR Computer="AzureMktg02" OR Computer="AzureMktg03")
```

<span data-ttu-id="19e0a-329">Étant donné que vous avez une sélection très spécifique, hello **mesurer Avg()** commande peut retourner hello moyenne non par ordinateur, mais dans la batterie de serveurs hello, simplement en effectuant un regroupement par CounterName.</span><span class="sxs-lookup"><span data-stu-id="19e0a-329">Because you have a very specific selection, hello **measure Avg()** command can return hello average not by computer, but across hello farm, simply by grouping by CounterName.</span></span> <span data-ttu-id="19e0a-330">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="19e0a-330">For example:</span></span>

```
Type=Perf  InstanceName:_Total  ((ObjectName:Processor AND CounterName:"% Processor Time") OR (ObjectName="LogicalDisk" AND CounterName="% Free Space")) AND TimeGenerated>NOW-4HOURS AND (Computer="AzureMktg01" OR Computer="AzureMktg02" OR Computer="AzureMktg03") | Measure Avg(CounterValue) by CounterName
```

<span data-ttu-id="19e0a-331">Cela vous donne une vue compacte utile de quelques indicateurs de performance clés de votre environnement.</span><span class="sxs-lookup"><span data-stu-id="19e0a-331">This gives you a useful compact view of a couple of your environment's KPIs.</span></span>

![Recherche du groupement de la fonction avg](./media/log-analytics-log-searches/oms-search-avg04.png)

<span data-ttu-id="19e0a-333">Vous pouvez facilement utiliser la requête de recherche hello dans un tableau de bord.</span><span class="sxs-lookup"><span data-stu-id="19e0a-333">You can easily use hello search query in a dashboard.</span></span> <span data-ttu-id="19e0a-334">Par exemple, vous Impossible d’enregistrer la requête de recherche hello et créer un tableau de bord à partir de celui-ci nommé *KPI de batterie de serveurs Web*.</span><span class="sxs-lookup"><span data-stu-id="19e0a-334">For example, you could save hello search query and create a dashboard from it named *Web Farm KPIs*.</span></span> <span data-ttu-id="19e0a-335">toolearn plus sur l’utilisation de tableaux de bord, consultez [créer un tableau de bord personnalisé dans le journal Analytique](log-analytics-dashboards.md).</span><span class="sxs-lookup"><span data-stu-id="19e0a-335">toolearn more about using dashboards, see [Create a custom dashboard in Log Analytics](log-analytics-dashboards.md).</span></span>

![Tableau de bord de recherche avg](./media/log-analytics-log-searches/oms-search-avg05.png)

### <a name="use-hello-sum-function-with-hello-measure-command"></a><span data-ttu-id="19e0a-337">Utilisez la fonction sum hello avec la commande de mesure hello</span><span class="sxs-lookup"><span data-stu-id="19e0a-337">Use hello sum function with hello measure command</span></span>
<span data-ttu-id="19e0a-338">la fonction sum Hello est fonctions tooother similaires de la commande de mesure hello.</span><span class="sxs-lookup"><span data-stu-id="19e0a-338">hello sum function is similar tooother functions of hello measure command.</span></span> <span data-ttu-id="19e0a-339">Vous pouvez voir un exemple sur la façon dont toouse hello fonction sum dans [recherche de journaux IIS W3C dans Microsoft Azure Operational Insights](http://blogs.msdn.com/b/dmuscett/archive/2014/09/20/w3c-iis-logs-search-in-system-center-advisor-limited-preview.aspx).</span><span class="sxs-lookup"><span data-stu-id="19e0a-339">You can see an example about how toouse hello sum function at [W3C IIS Logs Search in Microsoft Azure Operational Insights](http://blogs.msdn.com/b/dmuscett/archive/2014/09/20/w3c-iis-logs-search-in-system-center-advisor-limited-preview.aspx).</span></span>

<span data-ttu-id="19e0a-340">Vous pouvez utiliser les fonctions Max() et Min() avec des chaînes de nombres, de dates et heures, et de texte.</span><span class="sxs-lookup"><span data-stu-id="19e0a-340">You can use Max() and Min() with numbers, date times and text strings.</span></span> <span data-ttu-id="19e0a-341">Avec des chaînes de texte, elles sont triées par ordre alphabétique et vous pouvez obtenir la première et la dernière.</span><span class="sxs-lookup"><span data-stu-id="19e0a-341">With text strings, they are sorted alphabetically and you get first and last.</span></span>

<span data-ttu-id="19e0a-342">Toutefois, vous ne pouvez pas utiliser Sum() uniquement avec des champs numériques.</span><span class="sxs-lookup"><span data-stu-id="19e0a-342">However, you cannot use Sum() with anything other than numerical fields.</span></span> <span data-ttu-id="19e0a-343">Cela s’applique également tooAvg().</span><span class="sxs-lookup"><span data-stu-id="19e0a-343">This also applies tooAvg().</span></span>

### <a name="use-hello-percentile-function-with-hello-measure-command"></a><span data-ttu-id="19e0a-344">Utilisez la fonction de centile de hello avec la commande de mesure hello</span><span class="sxs-lookup"><span data-stu-id="19e0a-344">Use hello percentile function with hello measure command</span></span>
<span data-ttu-id="19e0a-345">fonction de centile Hello est similaire tooAvg() et Sum() dans que vous pouvez l’utiliser uniquement pour les champs numériques.</span><span class="sxs-lookup"><span data-stu-id="19e0a-345">hello percentile function is similar tooAvg() and Sum() in that you can only use it for numerical fields.</span></span> <span data-ttu-id="19e0a-346">Vous pouvez utiliser n’importe quel centile entre 1 too99 sur un champ numérique.</span><span class="sxs-lookup"><span data-stu-id="19e0a-346">You can use any percentile between 1 too99 on a numeric field.</span></span> <span data-ttu-id="19e0a-347">Vous pouvez également utiliser les deux commandes **percentile** et **pct**.</span><span class="sxs-lookup"><span data-stu-id="19e0a-347">You can also use both **percentile** and **pct** commands.</span></span> <span data-ttu-id="19e0a-348">Voici quelques exemples :</span><span class="sxs-lookup"><span data-stu-id="19e0a-348">Here are few examples:</span></span>  

```
Type:Perf CounterName:"DiskTransers/sec" |measure percentile95(CurrentValue) by Computer
```
```
Type:Perf ObjectName=LogicalDisk CounterName="Current Disk Queue Length" Computer="MyComputerName" | measure pct65(CurrentValue) by InstanceName
```

## <a name="use-hello-where-command"></a><span data-ttu-id="19e0a-349">Utiliser des commandes hello</span><span class="sxs-lookup"><span data-stu-id="19e0a-349">Use hello where command</span></span>
<span data-ttu-id="19e0a-350">Hello où commande fonctionne comme un filtre, mais elle peut être appliquée dans le filtre de hello pipeline toofurther agrégées des résultats qui ont été produits par une commande Measure – en tant que résultats tooraw opposés qui sont filtrés au début de hello d’une requête.</span><span class="sxs-lookup"><span data-stu-id="19e0a-350">hello where command works like a filter, but it can be applied in hello pipeline toofurther filter aggregated results that have been produced by a Measure command – as opposed tooraw results that are filtered at hello beginning of a query.</span></span>

<span data-ttu-id="19e0a-351">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="19e0a-351">For example:</span></span>

```
Type=Perf  CounterName="% Processor Time"  InstanceName="_Total" | Measure Avg(CounterValue) as AVGCPU by Computer
```

<span data-ttu-id="19e0a-352">Vous pouvez ajouter une autre barre verticale « | » caractères et hello où commande tooonly obtenir les ordinateurs dont l’UC moyenne est supérieure à 80 %, avec hello selon exemple :</span><span class="sxs-lookup"><span data-stu-id="19e0a-352">You can add another pipe "|" character and hello Where command tooonly get computers whose average CPU is above 80%, with hello following example:</span></span>

```
Type=Perf  CounterName="% Processor Time"  InstanceName="_Total" | Measure Avg(CounterValue) as AVGCPU by Computer | Where AVGCPU>80
```

<span data-ttu-id="19e0a-353">Si vous êtes familiarisé avec Microsoft System Center - Operations Manager, vous pouvez considérer hello où command pack d’administration.</span><span class="sxs-lookup"><span data-stu-id="19e0a-353">If you're familiar with Microsoft System Center - Operations Manager, you can think of hello where command in management pack terms.</span></span> <span data-ttu-id="19e0a-354">Si hello exemple était une règle, hello première partie de la requête de hello serait hello et la source de données hello où commande serait la détection de condition hello.</span><span class="sxs-lookup"><span data-stu-id="19e0a-354">If hello example were a rule, hello first part of hello query would be hello data source and hello where command would be hello condition detection.</span></span>

<span data-ttu-id="19e0a-355">Vous pouvez utiliser la requête de hello sous forme de vignette dans **mon tableau de bord**, comme un moniteur de tri, toosee lorsque les processeurs d’ordinateur sont surexploités.</span><span class="sxs-lookup"><span data-stu-id="19e0a-355">You can use hello query as a tile in **My Dashboard**, as a monitor of sorts, toosee when computer CPUs are over-utilized.</span></span> <span data-ttu-id="19e0a-356">toolearn savoir plus sur les tableaux de bord, consultez [créer un tableau de bord personnalisé dans le journal Analytique](log-analytics-dashboards.md).</span><span class="sxs-lookup"><span data-stu-id="19e0a-356">toolearn more about dashboards, see [Create a custom dashboard in Log Analytics](log-analytics-dashboards.md).</span></span> <span data-ttu-id="19e0a-357">Vous pouvez également créer et utiliser des tableaux de bord à l’aide d’application mobile hello.</span><span class="sxs-lookup"><span data-stu-id="19e0a-357">You can also create and use dashboards using hello mobile app.</span></span> <span data-ttu-id="19e0a-358">Pour plus d’informations, voir [Applications mobiles OMS](http://www.windowsphone.com/en-us/store/app/operational-insights/4823b935-83ce-466c-82bb-bd0a3f58d865).</span><span class="sxs-lookup"><span data-stu-id="19e0a-358">For more information, see [OMS Mobile App ](http://www.windowsphone.com/en-us/store/app/operational-insights/4823b935-83ce-466c-82bb-bd0a3f58d865).</span></span> <span data-ttu-id="19e0a-359">Dans hello bas des deux vignettes de hello suivant l’image, vous pouvez voir le moniteur de hello a affiché une liste et un nombre.</span><span class="sxs-lookup"><span data-stu-id="19e0a-359">In hello bottom two tiles of hello following image, you can see hello monitor displayed a list and as a number.</span></span> <span data-ttu-id="19e0a-360">Fondamentalement, vous souhaitez hello, toobe nombre zéro et toujours hello toobe liste vide.</span><span class="sxs-lookup"><span data-stu-id="19e0a-360">Essentially, you always want hello number toobe zero and hello list toobe empty.</span></span> <span data-ttu-id="19e0a-361">Dans le cas contraire, il indique une condition d'alerte.</span><span class="sxs-lookup"><span data-stu-id="19e0a-361">Otherwise, it indicates an alert condition.</span></span> <span data-ttu-id="19e0a-362">Si nécessaire, vous pouvez l’utiliser tootake examiner quels ordinateurs sont sous pression.</span><span class="sxs-lookup"><span data-stu-id="19e0a-362">If needed, you can use it tootake a look at which machines are under pressure.</span></span>

![Tableau de bord mobile](./media/log-analytics-log-searches/oms-search-mobile.png)

## <a name="use-hello-in-operator"></a><span data-ttu-id="19e0a-364">Utilisez hello in, opérateur</span><span class="sxs-lookup"><span data-stu-id="19e0a-364">Use hello in operator</span></span>
<span data-ttu-id="19e0a-365">Hello *IN* (opérateur), avec *NOT IN* vous permet de toouse sous-recherches, c'est-à-dire des recherches qui incluent une autre recherche en tant qu’argument.</span><span class="sxs-lookup"><span data-stu-id="19e0a-365">hello *IN* operator, along with *NOT IN* allows you toouse subsearches, which are searches that include another search as an argument.</span></span> <span data-ttu-id="19e0a-366">Elles sont contenues entre accolades {} à l’intérieur d’une autre recherche *principale* ou *externe*.</span><span class="sxs-lookup"><span data-stu-id="19e0a-366">They are contained in braces {} within another *primary* or *outer* search.</span></span> <span data-ttu-id="19e0a-367">Hello résultat d’une sous-recherche, souvent une liste de résultats distincts est ensuite utilisé en tant qu’argument dans sa recherche principale.</span><span class="sxs-lookup"><span data-stu-id="19e0a-367">hello result of a subsearch, often a list of distinct results, is then used as an argument in its primary search.</span></span>

<span data-ttu-id="19e0a-368">Vous pouvez utiliser des sous-recherches toomatch des sous-ensembles de vos données que vous ne pouvez pas décrire directement dans une expression de recherche, mais qui peut être généré à partir d’une recherche.</span><span class="sxs-lookup"><span data-stu-id="19e0a-368">You can use subsearches toomatch subsets of your data that you cannot describe directly in a search expression, but which can be generated from a search.</span></span> <span data-ttu-id="19e0a-369">Par exemple, si vous voulez intéressez à l’aide d’une recherche toofind tous les événements à partir de *ordinateurs mises à jour de sécurité manquantes*, vous devez toodesign une sous-recherche qui identifie d’abord *ordinateurs mises à jour de sécurité manquantes*  avant de rechercher les événements appartenant toothose hôtes.</span><span class="sxs-lookup"><span data-stu-id="19e0a-369">For example, if you’re interested in using one search toofind all events from *computers missing security updates*, then you need toodesign a subsearch that first identifies that *computers missing security updates* before it finds events belonging toothose hosts.</span></span>

<span data-ttu-id="19e0a-370">Ainsi, vous pouvez représenter *ordinateurs auxquels il manque requis des mises à jour de sécurité* avec hello suivant la requête :</span><span class="sxs-lookup"><span data-stu-id="19e0a-370">So, you could express *computers currently missing required security updates* with hello following query:</span></span>

```
Type:Update UpdateState=Needed Optional=false Classification="Security Updates" TimeGenerated>NOW-24HOURS | measure count() by Computer
```    

![Exemple de recherche avec l’opérateur IN](./media/log-analytics-log-searches/oms-search-in01-revised.png)

<span data-ttu-id="19e0a-372">Une fois que vous avez hello liste, vous pouvez utiliser hello recherche comme une liste de hello toofeed recherche interne des ordinateurs d’une recherche externe (principale) qui recherche les événements liés à ces ordinateurs.</span><span class="sxs-lookup"><span data-stu-id="19e0a-372">Once you have hello list, you can use hello search as an inner search toofeed hello list of computers into an outer (primary) search that will look for events for those computers.</span></span> <span data-ttu-id="19e0a-373">Pour cela, vous devez hello, recherche interne entre accolades et alimentez ses résultats sous forme de valeurs possibles pour un filtre/champ de recherche externe à hello à l’aide d’opérateur de hello dans.</span><span class="sxs-lookup"><span data-stu-id="19e0a-373">You do this by enclosing hello inner search in braces and feeding its results as possible values for a filter/field in hello outer search using hello IN operator.</span></span> <span data-ttu-id="19e0a-374">Hello requête ressemble à :</span><span class="sxs-lookup"><span data-stu-id="19e0a-374">hello query would resemble:</span></span>

```
Type=Event Computer IN {Type:Update UpdateState=Needed Optional=false Classification="Security Updates" TimeGenerated>NOW-24HOURS | measure count() by Computer}
```
![Exemple de recherche avec l’opérateur IN](./media/log-analytics-log-searches/oms-search-in02-revised.png)

<span data-ttu-id="19e0a-376">Temps de hello avis filtre utilisé dans la recherche interne de hello car hello évaluation des mises à jour du système prend également un instantané de tous les ordinateurs toutes les 24 heures.</span><span class="sxs-lookup"><span data-stu-id="19e0a-376">Also notice hello time filter used in hello inner search because hello System Update Assessment takes a snapshot of all computers every 24 hours.</span></span> <span data-ttu-id="19e0a-377">Faire en requête interne de hello plus léger et plus précise par recherche uniquement sur une journée.</span><span class="sxs-lookup"><span data-stu-id="19e0a-377">You can make hello inner query more lightweight and precise by only searching for a day.</span></span> <span data-ttu-id="19e0a-378">recherche externe de Hello utilise à la place sélection de temps hello dans l’interface utilisateur hello, récupérer les événements à partir de hello ces 7 derniers jours.</span><span class="sxs-lookup"><span data-stu-id="19e0a-378">hello outer search instead uses hello time selection in hello user interface, retrieving events from hello last 7 days.</span></span> <span data-ttu-id="19e0a-379">Consultez la page [Opérateurs booléens](#boolean-operators) pour plus d’informations sur les opérateurs de temps.</span><span class="sxs-lookup"><span data-stu-id="19e0a-379">See [Boolean operators](#boolean-operators) for more information about time operators.</span></span>

<span data-ttu-id="19e0a-380">Étant donné que vous vraiment à peine hello utiliser les résultats de recherche interne de hello comme valeur de filtre pour hello externe, vous pouvez toujours appliquer des commandes de recherche externe de hello.</span><span class="sxs-lookup"><span data-stu-id="19e0a-380">Because you really only use hello results of hello inner search as a filter value for hello outer one, you can still apply commands in hello outer search.</span></span> <span data-ttu-id="19e0a-381">Par exemple, vous pouvez toujours hello groupe au-dessus événements avec une autre commande measure :</span><span class="sxs-lookup"><span data-stu-id="19e0a-381">For example, you can still group hello above events with another measure command:</span></span>

```
Type=Event Computer IN {Type:Update UpdateState=Needed Optional=false Classification="Security Updates" TimeGenerated>NOW-24HOURS | measure count() by Computer} | measure count() by Source
```

![Exemple de recherche avec l’opérateur IN](./media/log-analytics-log-searches/oms-search-in03-revised.png)

<span data-ttu-id="19e0a-383">En règle générale, vous souhaitez tooexecute de votre requête interne rapidement car Analytique de journal a des délais d’expiration côté service pour et également tooreturn une petite quantité de résultats.</span><span class="sxs-lookup"><span data-stu-id="19e0a-383">Generally, you want your inner query tooexecute quickly because Log Analytics has service-side timeouts for it and also tooreturn a small amount of results.</span></span> <span data-ttu-id="19e0a-384">Si la requête interne de hello retourne plus de résultats, la liste des résultats hello est tronquée, ce qui peut amener hello recherche externe tooreturn des résultats incorrects.</span><span class="sxs-lookup"><span data-stu-id="19e0a-384">If hello inner query returns more results, hello result list gets truncated, which could potentially cause hello outer search tooreturn incorrect results.</span></span>

<span data-ttu-id="19e0a-385">Une autre règle est que la recherche interne hello doit tooprovide *agrégées* résultats.</span><span class="sxs-lookup"><span data-stu-id="19e0a-385">Another rule is that hello inner search currently needs tooprovide *aggregated* results.</span></span> <span data-ttu-id="19e0a-386">En d’autres termes, elle doit contenir une commande *measure* ; vous ne pouvez pour le moment pas alimenter les résultats bruts dans une recherche externe.</span><span class="sxs-lookup"><span data-stu-id="19e0a-386">In other words, it must contain a *measure* command; you cannot currently feed raw results into an outer search.</span></span>

<span data-ttu-id="19e0a-387">En outre, il peut y avoir qu’un seul opérateur IN, et il doit être hello dernier filtre de requête de hello.</span><span class="sxs-lookup"><span data-stu-id="19e0a-387">Also, there can be only one IN operator and it must be hello last filter in hello query.</span></span> <span data-ttu-id="19e0a-388">Plusieurs opérateurs IN ne peut pas être, ou cela essentiellement d’empêcher l’exécution de plusieurs sous-recherches : hello important point est que seule sub/recherche interne est possible pour chaque recherche externe.</span><span class="sxs-lookup"><span data-stu-id="19e0a-388">Multiple IN operators cannot be OR’d – this essentially prevents running multiple subsearches: hello important point is that only one sub/inner search is possible for each outer search.</span></span>

<span data-ttu-id="19e0a-389">Même avec ces limites, permet de nombreux types de recherche en corrélation et vous permet de toodefine toogroups quelque chose de similaire tels que les ordinateurs, les utilisateurs ou les fichiers, les champs hello dans vos données contiennent des.</span><span class="sxs-lookup"><span data-stu-id="19e0a-389">Even with these limits, IN enables many kinds of correlated searches, and allows you toodefine something similar toogroups such as computers, users, or files – whatever hello fields in your data contain.</span></span> <span data-ttu-id="19e0a-390">Voici des exemples supplémentaires :</span><span class="sxs-lookup"><span data-stu-id="19e0a-390">Here are more examples:</span></span>

<span data-ttu-id="19e0a-391">**Toutes les mises à jour manquantes sur des ordinateurs sur lesquels le paramètre de mise à jour automatique est désactivé**</span><span class="sxs-lookup"><span data-stu-id="19e0a-391">**All updates missing from computers where Automatic Update setting is disabled**</span></span>

```
Type=Update UpdateState=Needed Optional=false Computer IN {Type=UpdateSummary WindowsUpdateSetting=Manual | measure count() by Computer} | measure count() by KBID
```

<span data-ttu-id="19e0a-392">**Tous les événements d’erreur sur des ordinateurs exécutant SQL Server (où l’évaluation de SQL a été exécutée)**</span><span class="sxs-lookup"><span data-stu-id="19e0a-392">**All error events from computers running SQL Server (=where SQL Assessment has run)**</span></span>

```
Type=Event EventLevelName=error Computer IN {Type=SQLAssessmentRecommendation | measure count() by Computer}
```

<span data-ttu-id="19e0a-393">**Tous les événements de sécurité des ordinateurs qui sont des contrôleurs de domaine (où l’évaluation d’Active Directory a été exécutée)**</span><span class="sxs-lookup"><span data-stu-id="19e0a-393">**All security events from computers that are Domain Controllers (=where AD Assessment has run)**</span></span>

```
Type=SecurityEvent Computer IN { Type=ADAssessmentRecommendation | measure count() by Computer }
```

<span data-ttu-id="19e0a-394">**Qui autres comptes ont ouvert une session toohello mêmes ordinateurs où le compte BACONLAND\jochan a ouvert une session ?**</span><span class="sxs-lookup"><span data-stu-id="19e0a-394">**Which other accounts have logged on toohello same computers where account BACONLAND\jochan has logged on?**</span></span>

```
Type=SecurityEvent EventID=4624   Account!="BACONLAND\\jochan" Computer IN { Type=SecurityEvent EventID=4624   Account="BACONLAND\\jochan" | measure count() by Computer } | measure count() by Account
```

## <a name="use-hello-distinct-command"></a><span data-ttu-id="19e0a-395">Utilisez la commande distinctes hello</span><span class="sxs-lookup"><span data-stu-id="19e0a-395">Use hello distinct command</span></span>
<span data-ttu-id="19e0a-396">Comme le suggère le nom hello, cette commande fournit une liste de valeurs distinctes d’un champ.</span><span class="sxs-lookup"><span data-stu-id="19e0a-396">As hello name suggests, this command provides a list of distinct values for a field.</span></span> <span data-ttu-id="19e0a-397">Son utilisation est étonnamment simple mais cette commande s’avère très utile.</span><span class="sxs-lookup"><span data-stu-id="19e0a-397">It's surprisingly simple but quite useful.</span></span> <span data-ttu-id="19e0a-398">Hello que même résultat peut être obtenu avec la commande measure count() également, comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="19e0a-398">hello same could be achieved with measure count() command as well, as shown below.</span></span>

```
Type=Event | Measure count() by Computer
```

![Exemple de commande de recherche DISTINCT](./media/log-analytics-log-searches/oms-search-distinct01-revised.png)

<span data-ttu-id="19e0a-400">Toutefois, si vous êtes intéressé il suffit qu’une liste de valeurs distinctes et non par nombre de documents qui ont des valeurs qui hello, puis DISTINCT peut fournir tooread plus claire et plus facile de sortie et une syntaxe plus courte, comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="19e0a-400">However, if all you're interested in is just a list of distinct values and not hello count of documents that have that values, then DISTINCT can provide cleaner and easier tooread output, and shorter syntax, as shown below.</span></span>

```
Type=Event | Distinct Computer
```
![Exemple de commande de recherche DISTINCT](./media/log-analytics-log-searches/oms-search-distinct02-revised.png)

## <a name="use-hello-countdistinct-function-with-hello-measure-command"></a><span data-ttu-id="19e0a-402">Utiliser la fonction countdistinct de hello avec la commande de mesure hello</span><span class="sxs-lookup"><span data-stu-id="19e0a-402">Use hello countdistinct function with hello measure command</span></span>
<span data-ttu-id="19e0a-403">fonction countdistinct de Hello de hello nombre de valeurs distinctes dans chaque groupe.</span><span class="sxs-lookup"><span data-stu-id="19e0a-403">hello countdistinct function counts hello number of distinct values within each group.</span></span> <span data-ttu-id="19e0a-404">Par exemple, il peut être utilisé numéro de hello toocount d’ordinateurs uniques pour chaque Type de création de rapports :</span><span class="sxs-lookup"><span data-stu-id="19e0a-404">For example, it could be used toocount hello number of unique computers reporting for each Type:</span></span>

```
* | measure countdistinct(Computer) by Type
```

![OMS-countdistinct](./media/log-analytics-log-searches/oms-countdistinct.png)

## <a name="use-hello-measure-interval-command"></a><span data-ttu-id="19e0a-406">Utiliser la commande d’intervalle hello measure</span><span class="sxs-lookup"><span data-stu-id="19e0a-406">Use hello measure interval command</span></span>
<span data-ttu-id="19e0a-407">Grâce à la récupération des données de performance en quasi-temps réel, vous pouvez récupérer et visualiser des compteurs de performance dans Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="19e0a-407">With near real-time performance data collection, you can collect and visualize any performance counter in Log Analytics.</span></span> <span data-ttu-id="19e0a-408">Requête de hello simplement entrer **Type : Perf** retournera des milliers de graphiques de métriques en fonction du nombre de hello des compteurs et les serveurs dans votre environnement Analytique de journal.</span><span class="sxs-lookup"><span data-stu-id="19e0a-408">Simply entering hello query **Type:Perf** will return thousands of metric graphs based on hello number of counters and servers in your Log Analytics environment.</span></span> <span data-ttu-id="19e0a-409">Avec l’agrégation de mesure à la demande, vous pouvez examiner hello métriques globale dans votre environnement à un niveau élevé et une connaissance approfondie des données plus granulaires que nécessaire pour.</span><span class="sxs-lookup"><span data-stu-id="19e0a-409">With on-demand metric aggregation, you can look at hello overall metrics in your environment at a high level, and deep dive into more granular data as you need to.</span></span>

<span data-ttu-id="19e0a-410">Supposons que vous voulez tooknow hello moyenne du processeur sur tous vos ordinateurs.</span><span class="sxs-lookup"><span data-stu-id="19e0a-410">Let’s say that you want tooknow what is hello average CPU across all your computers.</span></span> <span data-ttu-id="19e0a-411">Examinant hello des UC moyenne pour tous les ordinateurs ne serait pas utile, car les résultats peuvent obtenir nivelés. toolook en plus de détails, vous pouvez regrouper vos résultats fois plus petits segments de la fenêtre, puis ouvrez dans une série chronologique dans différentes dimensions.</span><span class="sxs-lookup"><span data-stu-id="19e0a-411">Looking at hello average CPU for every computer might not be helpful because results may get smoothed out. toolook into more details, you can aggregate your result in a smaller time window chunks, and look into a time series across different dimensions.</span></span> <span data-ttu-id="19e0a-412">Par exemple, vous pouvez effectuer moyenne de toutes les heures hello d’utilisation du processeur sur tous vos ordinateurs comme suit :</span><span class="sxs-lookup"><span data-stu-id="19e0a-412">For example, you can perform hello hourly average of CPU usage across all your computers as follows:</span></span>

```
Type:Perf CounterName="% Processor Time" InstanceName="_Total" | measure avg(CounterValue) by Computer Interval 1HOUR
```

![intervalle moyen de mesure](./media/log-analytics-log-searches/oms-measure-avg-interval.png)

<span data-ttu-id="19e0a-414">Par défaut, ces résultats s’affichent dans un graphique interactif en courbes contenant plusieurs séries.</span><span class="sxs-lookup"><span data-stu-id="19e0a-414">By default these results will be displayed in a multi-series interactive line chart.</span></span>  <span data-ttu-id="19e0a-415">Ce graphique prend en charge le basculement entre séries (avec la remise à l’échelle de l’axe y), le zoom et le survol.</span><span class="sxs-lookup"><span data-stu-id="19e0a-415">This chart supports series toggling (with y-axis rescaling), zooming, and hovering.</span></span>  <span data-ttu-id="19e0a-416">option d’affichage de tableau de Hello est toujours disponible pour l’affichage des données brutes de hello si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="19e0a-416">hello table display option is still available for viewing hello raw data if necessary.</span></span>

<span data-ttu-id="19e0a-417">Vous pouvez également effectuer des regroupements sur d’autres champs.</span><span class="sxs-lookup"><span data-stu-id="19e0a-417">You can also group by other fields.</span></span> <span data-ttu-id="19e0a-418">Dans cet exemple, je regarde tous les compteurs de % hello pour un ordinateur spécifique et vous voulez tooknow Nouveautés de centiles de toutes les heures 70 hello de chaque compteur :</span><span class="sxs-lookup"><span data-stu-id="19e0a-418">In this example, I am looking at all hello % counters for one specific computer, and I want tooknow what is hello hourly 70 percentiles of every counter:</span></span>

```
Type:Perf Computer=beefpatty4 CounterName=%* InstanceName=_Total | measure percentile70(CounterValue) by CounterName Interval 1HOUR
```
<span data-ttu-id="19e0a-419">Une chose toonote est que ces requêtes ne sont pas limités tooperformance compteurs.</span><span class="sxs-lookup"><span data-stu-id="19e0a-419">One thing toonote is that these queries are not limited tooperformance counters.</span></span> <span data-ttu-id="19e0a-420">Vous pouvez les appliquer tooany métrique.</span><span class="sxs-lookup"><span data-stu-id="19e0a-420">You can apply them tooany metric.</span></span> <span data-ttu-id="19e0a-421">Dans cet exemple, j’examine les journaux IIS W3C.</span><span class="sxs-lookup"><span data-stu-id="19e0a-421">In this example, I’m looking at W3C IIS logs.</span></span> <span data-ttu-id="19e0a-422">Je veux tooknow quel est le temps maximal de hello que nécessaire sur un intervalle de 5 minutes pour le traitement de chaque demande :</span><span class="sxs-lookup"><span data-stu-id="19e0a-422">I want tooknow what is hello maximum time it takes over a 5-minute interval for processing each request:</span></span>

```
Type:W3CIISLog | measure max(TimeTaken) by csMethod Interval 5MINUTES
```

### <a name="use-multiple-aggregates-in-one-query"></a><span data-ttu-id="19e0a-423">Utilisation de plusieurs agrégats dans une même requête</span><span class="sxs-lookup"><span data-stu-id="19e0a-423">Use multiple aggregates in one query</span></span>
<span data-ttu-id="19e0a-424">Vous pouvez spécifier plusieurs clauses d’agrégation dans une commande measure.</span><span class="sxs-lookup"><span data-stu-id="19e0a-424">You can specify multiple aggregate clauses in a measure command.</span></span>  <span data-ttu-id="19e0a-425">Un alias indépendant peut être attribué à chacune d’entre elles.</span><span class="sxs-lookup"><span data-stu-id="19e0a-425">Each one can be aliased independently.</span></span>  <span data-ttu-id="19e0a-426">Si elle n’est pas fourni un hello alias qui résulte nom de champ sera fonction d’agrégation hello qui a été utilisée (par exemple, « avg(CounterValue) » pour avg(CounterValue)).</span><span class="sxs-lookup"><span data-stu-id="19e0a-426">If it is not given an alias hello resulting field name will be hello aggregate function that was used (i.e. "avg(CounterValue)" for avg(CounterValue)).</span></span>

 ```
Type=WireData | measure avg(ReceivedBytes), avg(SentBytes) by Direction interval 1hour
```
![OMS-multiaggregates1](./media/log-analytics-log-searches/oms-multiaggregates1.png)

<span data-ttu-id="19e0a-428">Voici un autre exemple :</span><span class="sxs-lookup"><span data-stu-id="19e0a-428">Here is another example:</span></span>

 ```
* | measure countdistinct(Computer) as Computers, count() as TotalRecords by Type
```


## <a name="next-steps"></a><span data-ttu-id="19e0a-429">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="19e0a-429">Next steps</span></span>
<span data-ttu-id="19e0a-430">Pour plus d’informations sur les recherches de journal, consultez les ressources suivantes :</span><span class="sxs-lookup"><span data-stu-id="19e0a-430">For additional information about log searches, see:</span></span>

* <span data-ttu-id="19e0a-431">Utilisez [les champs personnalisés dans le journal Analytique](log-analytics-custom-fields.md) tooextend des recherches de journaux.</span><span class="sxs-lookup"><span data-stu-id="19e0a-431">Use [Custom fields in Log Analytics](log-analytics-custom-fields.md) tooextend log searches.</span></span>
* <span data-ttu-id="19e0a-432">Hello de révision [Analytique de journal journal référence de recherche](log-analytics-search-reference.md) tooview tous les Hello recherche des champs et facettes disponibles dans le journal Analytique.</span><span class="sxs-lookup"><span data-stu-id="19e0a-432">Review hello [Log Analytics log search reference](log-analytics-search-reference.md) tooview all of hello search fields and facets available in Log Analytics.</span></span>
