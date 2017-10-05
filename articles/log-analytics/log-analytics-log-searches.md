---
title: "Recherche de données à l’aide de recherches de journal dans Azure Log Analytics | Microsoft Docs"
description: "Les recherches de journal vous permettent de combiner et de mettre en corrélation toutes les données de l’ordinateur à partir de plusieurs sources dans votre environnement."
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
ms.openlocfilehash: bf237a837297cb8f1ab3a3340139133adcd2b244
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="find-data-using-log-searches-in-log-analytics"></a><span data-ttu-id="f0a89-103">Trouver des données avec les recherches de journaux dans Log Analytics</span><span class="sxs-lookup"><span data-stu-id="f0a89-103">Find data using log searches in Log Analytics</span></span>

>[!NOTE]
> <span data-ttu-id="f0a89-104">Cet article détaille les recherches de journaux via le langage de requête actuel dans Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="f0a89-104">This article describes log searches using the current query language in Log Analytics.</span></span>  <span data-ttu-id="f0a89-105">Si vous avez mis à niveau votre espace de travail vers le [nouveau langage de requête dans Log Analytics](log-analytics-log-search-upgrade.md), voir [Comprendre les recherches de journaux dans Log Analytics (nouveau)](log-analytics-log-search-new.md).</span><span class="sxs-lookup"><span data-stu-id="f0a89-105">If your workspace has been upgraded to the [new Log Analytics query language](log-analytics-log-search-upgrade.md), then you should refer to [Understanding log searches in Log Analytics (new)](log-analytics-log-search-new.md).</span></span>


<span data-ttu-id="f0a89-106">La fonctionnalité de recherche de journal se trouve au cœur de Log Analytics et vous permet de combiner et de mettre en corrélation des données machine de plusieurs sources dans votre environnement.</span><span class="sxs-lookup"><span data-stu-id="f0a89-106">At the core of Log Analytics is the log search feature which allows you to combine and correlate any machine data from multiple sources within your environment.</span></span> <span data-ttu-id="f0a89-107">Des solutions sont également alimentées par la recherche de journal pour vous proposer des mesures cernant un domaine problématique en particulier.</span><span class="sxs-lookup"><span data-stu-id="f0a89-107">Solutions are also powered by log search to bring you metrics pivoted around a particular problem area.</span></span>

<span data-ttu-id="f0a89-108">Sur la page Recherche, vous pouvez créer une requête, puis lorsque vous effectuez une recherche, vous pouvez filtrer les résultats en utilisant des contrôles de facette.</span><span class="sxs-lookup"><span data-stu-id="f0a89-108">On the Search page, you can create a query, and then when you search, you can filter the results by using facet controls.</span></span> <span data-ttu-id="f0a89-109">Vous pouvez également créer des requêtes avancées pour la transformation, le filtrage et les rapports relatifs aux résultats.</span><span class="sxs-lookup"><span data-stu-id="f0a89-109">You can also create advanced queries to transform, filter, and report on your results.</span></span>

<span data-ttu-id="f0a89-110">Les requêtes de recherche de journal courantes apparaissent dans la plupart des pages de solutions.</span><span class="sxs-lookup"><span data-stu-id="f0a89-110">Common log search queries appear on most solution pages.</span></span> <span data-ttu-id="f0a89-111">Vous pouvez cliquer sur les vignettes ou explorer d’autres éléments dans l’ensemble de la console OMS afin d’afficher les détails de l’élément à l’aide de la recherche de journal.</span><span class="sxs-lookup"><span data-stu-id="f0a89-111">Throughout the OMS console, you can click tiles or drill in to other items to view details about the item by using log search.</span></span>

<span data-ttu-id="f0a89-112">Dans ce didacticiel, nous examinerons des exemples afin de couvrir toutes les notions de base dont vous avez besoin lorsque vous utilisez la recherche de journal.</span><span class="sxs-lookup"><span data-stu-id="f0a89-112">In this tutorial, we'll walk through examples to cover all the basics when you use log search.</span></span>

<span data-ttu-id="f0a89-113">Nous allons commencer par des exemples simples et pratiques, puis nous développerons à partir de ceux-ci pour vous permettre d’avoir une compréhension pratique de l’utilisation de la syntaxe pour extraire les informations dont vous avez besoin à partir des données.</span><span class="sxs-lookup"><span data-stu-id="f0a89-113">We'll start with simple, practical examples and then build on them so that you can get an understanding of practical use cases about how to use the syntax to extract the insights you want from the data.</span></span>

<span data-ttu-id="f0a89-114">Une fois que vous êtes familiarisé avec les techniques de recherche, vous pouvez consulter les [informations de référence sur la recherche de journal Log Analytics](log-analytics-search-reference.md).</span><span class="sxs-lookup"><span data-stu-id="f0a89-114">After you've familiar with search techniques, you can review the [Log Analytics log search reference](log-analytics-search-reference.md).</span></span>

## <a name="use-basic-filters"></a><span data-ttu-id="f0a89-115">Utilisation de filtres de base</span><span class="sxs-lookup"><span data-stu-id="f0a89-115">Use basic filters</span></span>
<span data-ttu-id="f0a89-116">La première chose à savoir est que la première partie d’une requête de recherche avant un caractère de barre verticale « | » est toujours un *filtre*.</span><span class="sxs-lookup"><span data-stu-id="f0a89-116">The first thing to know is that the first part of a search query, before any "|" vertical pipe character, is always a *filter*.</span></span> <span data-ttu-id="f0a89-117">Considérez-la comme une clause WHERE dans TSQL : elle détermine *quel* sous-ensemble de données doit être extrait du magasin de données OMS.</span><span class="sxs-lookup"><span data-stu-id="f0a89-117">You can think of it as a WHERE clause in TSQL--it determines *what* subset of data to pull out of the OMS data store.</span></span> <span data-ttu-id="f0a89-118">La recherche dans un magasin de données consiste principalement à préciser les caractéristiques de données que vous souhaitez extraire ; il est donc naturel qu’une requête commence par la clause WHERE.</span><span class="sxs-lookup"><span data-stu-id="f0a89-118">Searching in the data store is largely about specifying the characteristics of the data that you want to extract, so it is natural that a query would start with the WHERE clause.</span></span>

<span data-ttu-id="f0a89-119">Les filtres les plus simples que vous pouvez utiliser sont des *mots clés*tels que « error » ou « timeout » ou un nom d'ordinateur.</span><span class="sxs-lookup"><span data-stu-id="f0a89-119">The most basic filters you can use are *keywords*, such as ‘error’ or ‘timeout’, or a computer name.</span></span> <span data-ttu-id="f0a89-120">Ces types de requêtes simples retournent généralement différentes formes de données dans le même jeu de résultats.</span><span class="sxs-lookup"><span data-stu-id="f0a89-120">These types of simple queries generally return diverse shapes of data within the same result set.</span></span> <span data-ttu-id="f0a89-121">Cela est dû au fait que Log Analytics dispose de différents *types* de données dans le système.</span><span class="sxs-lookup"><span data-stu-id="f0a89-121">This is because Log Analytics has different *types* of data in the system.</span></span>

### <a name="to-conduct-a-simple-search"></a><span data-ttu-id="f0a89-122">Pour effectuer une recherche simple</span><span class="sxs-lookup"><span data-stu-id="f0a89-122">To conduct a simple search</span></span>
1. <span data-ttu-id="f0a89-123">Dans le portail OMS, cliquez sur **Recherche de journal**.</span><span class="sxs-lookup"><span data-stu-id="f0a89-123">In the OMS portal, click **Log Search**.</span></span>  
    <span data-ttu-id="f0a89-124">![Vignette Rechercher](./media/log-analytics-log-searches/oms-overview-log-search.png)</span><span class="sxs-lookup"><span data-stu-id="f0a89-124">![search tile](./media/log-analytics-log-searches/oms-overview-log-search.png)</span></span>
2. <span data-ttu-id="f0a89-125">Dans le champ de requête, tapez `error` puis cliquez sur **Rechercher**.</span><span class="sxs-lookup"><span data-stu-id="f0a89-125">In the query field, type `error` and then click **Search**.</span></span>  
    <span data-ttu-id="f0a89-126">![Recherche d’erreur](./media/log-analytics-log-searches/oms-search-error.png)</span><span class="sxs-lookup"><span data-stu-id="f0a89-126">![search error](./media/log-analytics-log-searches/oms-search-error.png)</span></span>  
    <span data-ttu-id="f0a89-127">Par exemple, la requête pour `error` dans l’image suivante a retourné 100 000 enregistrements **Événement** (collectés par la gestion des journaux), 18 enregistrements **ConfigurationAlert** (générés par l’évaluation de la configuration), et 12 enregistrements **ConfigurationChange** (capturés par le suivi des modifications). </span><span class="sxs-lookup"><span data-stu-id="f0a89-127">For example, the query for `error` in the following image returned 100,000 **Event** records (collected by Log Management), 18 **ConfigurationAlert** records (generated by Configuration Assessment) and 12 **ConfigurationChange** records (captured by the Change Tracking).</span></span>   
    <span data-ttu-id="f0a89-128">![Recherche de résultats](./media/log-analytics-log-searches/oms-search-results01.png)</span><span class="sxs-lookup"><span data-stu-id="f0a89-128">![search results](./media/log-analytics-log-searches/oms-search-results01.png)</span></span>  

<span data-ttu-id="f0a89-129">Ces filtres ne sont pas vraiment des classes/types d'objet.</span><span class="sxs-lookup"><span data-stu-id="f0a89-129">These filters are not really object types/classes.</span></span> <span data-ttu-id="f0a89-130">*Type* est simplement une balise, une propriété ou une chaîne/un nom/une catégorie associés à un élément de données.</span><span class="sxs-lookup"><span data-stu-id="f0a89-130">*Type* is just a tag, or a property, or a string/name/category, that is attached to a piece of data.</span></span> <span data-ttu-id="f0a89-131">Certains documents dans le système sont balisés en tant que **Type:ConfigurationAlert**, d’autres en tant que **Type:Perf** ou **Type:Event**, et ainsi de suite.</span><span class="sxs-lookup"><span data-stu-id="f0a89-131">Some documents in the system are tagged as **Type:ConfigurationAlert** and some are tagged as **Type:Perf**, or **Type:Event**, and so on.</span></span> <span data-ttu-id="f0a89-132">Chaque résultat de recherche, document, enregistrement ou entrée affiche toutes les propriétés brutes et leurs valeurs pour chacun de ces éléments de données. Vous pouvez utiliser ces noms de champs pour préciser dans le filtre lorsque vous souhaitez récupérer uniquement les enregistrements dont le champ a cette valeur donnée.</span><span class="sxs-lookup"><span data-stu-id="f0a89-132">Each search result, document, record, or entry displays all the raw properties and their values for each of those pieces of data, and you can use those field names to specify in the filter when you want to retrieve only the records where the field has that given value.</span></span>

<span data-ttu-id="f0a89-133">Le *type* est simplement un champ que tous les enregistrements ont. Il n'est pas différent des autres champs.</span><span class="sxs-lookup"><span data-stu-id="f0a89-133">*Type* is really just a field that all records have, it is not different from any other field.</span></span> <span data-ttu-id="f0a89-134">Cela a été établi suivant la valeur du champ Type.</span><span class="sxs-lookup"><span data-stu-id="f0a89-134">This was established based on the value of the Type field.</span></span> <span data-ttu-id="f0a89-135">Cet enregistrement aura une autre forme.</span><span class="sxs-lookup"><span data-stu-id="f0a89-135">That record will have a different shape or form.</span></span> <span data-ttu-id="f0a89-136">À ce propos, **Type=Perf** ou **Type=Event** constituent également la syntaxe dont vous avez besoin pour apprendre à interroger des données ou événements de performances.</span><span class="sxs-lookup"><span data-stu-id="f0a89-136">Incidentally, **Type=Perf**, or **Type=Event** is also the syntax that you need to learn to query for performance data or events.</span></span>

<span data-ttu-id="f0a89-137">Vous pouvez utiliser les deux-points (:) ou le signe égal (=) après le nom du champ et avant la valeur.</span><span class="sxs-lookup"><span data-stu-id="f0a89-137">You can use either a colon (:) or an equal sign (=) after the field name and before the value.</span></span> <span data-ttu-id="f0a89-138">Les notations **Type:Event** et **Type=Event** ont la même signification. Vous pouvez donc choisir le style qui vous convient.</span><span class="sxs-lookup"><span data-stu-id="f0a89-138">**Type:Event** and **Type=Event** are equivalent in meaning, you can choose the style you prefer.</span></span>

<span data-ttu-id="f0a89-139">Ainsi, si les enregistrements Type=Perf ont un champ appelé « CounterName », vous pouvez alors écrire une requête qui ressemble à `Type=Perf CounterName="% Processor Time"`.</span><span class="sxs-lookup"><span data-stu-id="f0a89-139">So, if the Type=Perf records have a field called 'CounterName', then you can write a query resembling `Type=Perf CounterName="% Processor Time"`.</span></span>

<span data-ttu-id="f0a89-140">Vous obtiendrez uniquement les données de performances où le nom du compteur de performance est « % Processor Time ».</span><span class="sxs-lookup"><span data-stu-id="f0a89-140">This will give you only the performance data where the performance counter name is "% Processor Time".</span></span>

### <a name="to-search-for-processor-time-performance-data"></a><span data-ttu-id="f0a89-141">Pour rechercher des données de performance de temps du processeur</span><span class="sxs-lookup"><span data-stu-id="f0a89-141">To search for processor time performance data</span></span>
* <span data-ttu-id="f0a89-142">Dans le champ de requête de recherche, tapez `Type=Perf CounterName="% Processor Time"`</span><span class="sxs-lookup"><span data-stu-id="f0a89-142">In the search query field, type `Type=Perf CounterName="% Processor Time"`</span></span>

<span data-ttu-id="f0a89-143">Vous pouvez également être plus précis et utiliser **InstanceName=_’Total’** dans la requête, qui est un compteur de performances Windows.</span><span class="sxs-lookup"><span data-stu-id="f0a89-143">You can also be more specific and use **InstanceName=_'Total'** in the query, which is a Windows performance counter.</span></span> <span data-ttu-id="f0a89-144">Vous pouvez également sélectionner une facette et une autre valeur **field:value**.</span><span class="sxs-lookup"><span data-stu-id="f0a89-144">You can also select a facet and another **field:value**.</span></span> <span data-ttu-id="f0a89-145">Ce filtre est automatiquement ajouté à votre filtre dans la barre de requête.</span><span class="sxs-lookup"><span data-stu-id="f0a89-145">The filter is automatically added to your filter in the query bar.</span></span> <span data-ttu-id="f0a89-146">Vous pouvez le voir dans l'image suivante.</span><span class="sxs-lookup"><span data-stu-id="f0a89-146">You can see this in the following image.</span></span> <span data-ttu-id="f0a89-147">Elle indique où cliquer pour ajouter **InstanceName:’_Total’** à la requête sans devoir taper quoi que ce soit.</span><span class="sxs-lookup"><span data-stu-id="f0a89-147">It shows you where to click to add **InstanceName:’_Total’** to the query without typing anything.</span></span>

![Recherche de facette](./media/log-analytics-log-searches/oms-search-facet.png)

<span data-ttu-id="f0a89-149">Votre requête devient alors `Type=Perf CounterName="% Processor Time" InstanceName="_Total"`</span><span class="sxs-lookup"><span data-stu-id="f0a89-149">Your query now becomes `Type=Perf CounterName="% Processor Time" InstanceName="_Total"`</span></span>

<span data-ttu-id="f0a89-150">Dans cet exemple, vous n’êtes pas obligé de spécifier **Type=Perf** pour obtenir ce résultat.</span><span class="sxs-lookup"><span data-stu-id="f0a89-150">In this example, you don't have to specify **Type=Perf** to get to this result.</span></span> <span data-ttu-id="f0a89-151">Étant donné que les champs CounterName et InstanceName existent uniquement pour les enregistrements de Type=Perf, la requête est suffisamment spécifique pour retourner les mêmes résultats que le résultat précédent plus long :</span><span class="sxs-lookup"><span data-stu-id="f0a89-151">Because the fields CounterName and InstanceName only exist for records of Type=Perf, the query is specific enough to return the same results as the longer, previous one:</span></span>

```
CounterName="% Processor Time" InstanceName="_Total"
```

<span data-ttu-id="f0a89-152">Cela est dû au fait que tous les filtres dans la requête sont évalués comme étant dans chacun d’eux *ET* entre eux.</span><span class="sxs-lookup"><span data-stu-id="f0a89-152">This is because all the filters in the query are evaluated as being in *AND* with each other.</span></span> <span data-ttu-id="f0a89-153">En effet, plus vous ajoutez des champs aux critères, moins vous obtenez des résultats plus spécifiques et affinés.</span><span class="sxs-lookup"><span data-stu-id="f0a89-153">Effectively, the more fields you add to the criteria, you get less, more specific and refined results.</span></span>

<span data-ttu-id="f0a89-154">Par exemple, la requête `Type=Event EventLog="Windows PowerShell"` est identique à `Type=Event AND EventLog="Windows PowerShell"`.</span><span class="sxs-lookup"><span data-stu-id="f0a89-154">For example, the query `Type=Event EventLog="Windows PowerShell"` is identical to `Type=Event AND EventLog="Windows PowerShell"`.</span></span> <span data-ttu-id="f0a89-155">Elle retourne tous les événements qui ont été enregistrés dans et collectés à partir du journal des événements Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f0a89-155">It returns all events that were logged in and collected from the Windows PowerShell event log.</span></span> <span data-ttu-id="f0a89-156">Si vous ajoutez un filtre plusieurs fois en sélectionnant de manière répétée la même facette, le problème est alors purement esthétique : il peut surcharger la barre de recherche, mais il retourne toujours les mêmes résultats, car l'opérateur AND implicite est toujours présent.</span><span class="sxs-lookup"><span data-stu-id="f0a89-156">If you add a filter multiple times by repeatedly selecting the same facet, then the issue is purely cosmetic--it might clutter the Search bar, but it still returns the same results because the implicit AND operator is always there.</span></span>

<span data-ttu-id="f0a89-157">Vous pouvez facilement inverser l'opérateur AND implicite à l'aide d'un opérateur NOT explicite.</span><span class="sxs-lookup"><span data-stu-id="f0a89-157">You can easily reverse the implicit AND operator by using a NOT operator explicitly.</span></span> <span data-ttu-id="f0a89-158">Par exemple : </span><span class="sxs-lookup"><span data-stu-id="f0a89-158">For example:</span></span>

<span data-ttu-id="f0a89-159">`Type:Event NOT(EventLog:"Windows PowerShell")` ou son équivalent `Type=Event EventLog!="Windows PowerShell"` retournent tous les événements de tous les autres journaux qui ne sont PAS le journal Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f0a89-159">`Type:Event NOT(EventLog:"Windows PowerShell")` or its equivalent `Type=Event EventLog!="Windows PowerShell"` return all events from all other logs that are NOT the Windows PowerShell log.</span></span>

<span data-ttu-id="f0a89-160">Vous pouvez également utiliser un autre opérateur booléen tel que « OR ».</span><span class="sxs-lookup"><span data-stu-id="f0a89-160">Or, you can use other Boolean operator such as ‘OR’.</span></span> <span data-ttu-id="f0a89-161">La requête suivante retourne les enregistrements pour lesquels le journal des événements est une application OU un système.</span><span class="sxs-lookup"><span data-stu-id="f0a89-161">The following query returns records for which the EventLog is either Application OR System.</span></span>

```
EventLog=Application OR EventLog=System
```

<span data-ttu-id="f0a89-162">À l'aide de la requête ci-dessus, vous obtiendrez les entrées pour les journaux dans le même jeu de résultats.</span><span class="sxs-lookup"><span data-stu-id="f0a89-162">Using the above query, you’ll get entries for both logs in the same result set.</span></span>

<span data-ttu-id="f0a89-163">Cependant, si vous supprimez l'opérateur OR en laissant l’opérateur implicite AND en place, la requête suivante ne produira pas de résultats car aucune entrée du journal des événements n’appartient aux DEUX journaux.</span><span class="sxs-lookup"><span data-stu-id="f0a89-163">However, if you remove the OR by leaving the implicit AND in place, then the following query will not produce any results because there isn’t an event log entry that belongs to BOTH logs.</span></span> <span data-ttu-id="f0a89-164">Chaque entrée de journal des événements a été écrite pour seulement un des deux journaux.</span><span class="sxs-lookup"><span data-stu-id="f0a89-164">Each event log entry was written to only one of the two logs.</span></span>

```
EventLog=Application EventLog=System
```


## <a name="use-additional-filters"></a><span data-ttu-id="f0a89-165">Utilisation de filtres supplémentaires</span><span class="sxs-lookup"><span data-stu-id="f0a89-165">Use additional filters</span></span>
<span data-ttu-id="f0a89-166">La requête suivante retourne les entrées pour deux journaux des événements pour tous les ordinateurs qui ont envoyé des données.</span><span class="sxs-lookup"><span data-stu-id="f0a89-166">The following query returns entries for 2 event logs for all the computers that have sent data.</span></span>

```
EventLog=Application OR EventLog=System
```

![Recherche de résultats](./media/log-analytics-log-searches/oms-search-results03.png)

<span data-ttu-id="f0a89-168">La sélection de l'un des champs ou des filtres restreindra la requête pour un ordinateur spécifique, en excluant tous les autres.</span><span class="sxs-lookup"><span data-stu-id="f0a89-168">Selecting one of the fields or filters will narrow the query to a specific computer, excluding all other ones.</span></span> <span data-ttu-id="f0a89-169">La requête obtenue peut se présenter comme suit.</span><span class="sxs-lookup"><span data-stu-id="f0a89-169">The resulting query would resemble the following.</span></span>

```
EventLog=Application OR EventLog=System Computer=SERVER1.contoso.com
```

<span data-ttu-id="f0a89-170">Ce qui revient à la commande suivante, en raison de l'opérateur AND implicite.</span><span class="sxs-lookup"><span data-stu-id="f0a89-170">Which is equivalent to the following, because of the implicit AND.</span></span>

```
EventLog=Application OR EventLog=System AND Computer=SERVER1.contoso.com
```

<span data-ttu-id="f0a89-171">Chaque requête est évaluée dans l'ordre explicite suivant.</span><span class="sxs-lookup"><span data-stu-id="f0a89-171">Each query is evaluated in the following explicit order.</span></span> <span data-ttu-id="f0a89-172">Notez la parenthèse.</span><span class="sxs-lookup"><span data-stu-id="f0a89-172">Note the parenthesis.</span></span>

```
(EventLog=Application OR EventLog=System) AND Computer=SERVER1.contoso.com
```

<span data-ttu-id="f0a89-173">Comme le champ du journal des événements, vous pouvez récupérer des données uniquement pour un ensemble d'ordinateurs spécifiques en ajoutant OR.</span><span class="sxs-lookup"><span data-stu-id="f0a89-173">Just like the event log field, you can retrieve data only for a set of specific computers by adding OR.</span></span> <span data-ttu-id="f0a89-174">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="f0a89-174">For example:</span></span>

```
(EventLog=Application OR EventLog=System) AND (Computer=SERVER1.contoso.com OR Computer=SERVER2.contoso.com OR Computer=SERVER3.contoso.com)
```

<span data-ttu-id="f0a89-175">De même, cette requête suivante retourne le **pourcentage de temps processeur** uniquement pour les deux ordinateurs sélectionnés.</span><span class="sxs-lookup"><span data-stu-id="f0a89-175">Similarly, this the following query return **% CPU Time** for the selected two computers only.</span></span>

```
CounterName="% Processor Time"  AND InstanceName="_Total" AND (Computer=SERVER1.contoso.com OR Computer=SERVER2.contoso.com)
```

### <a name="field-types"></a><span data-ttu-id="f0a89-176">Types de champ</span><span class="sxs-lookup"><span data-stu-id="f0a89-176">Field types</span></span>
<span data-ttu-id="f0a89-177">Lorsque vous créez des filtres, vous devez comprendre les différences entre les types de champs retournés par les recherches dans les journaux.</span><span class="sxs-lookup"><span data-stu-id="f0a89-177">When creating filters, you should understand the differences in working with different types of fields returned by log searches.</span></span>

<span data-ttu-id="f0a89-178">Les **champs interrogeables** s’affichent en bleu dans les résultats de la recherche.</span><span class="sxs-lookup"><span data-stu-id="f0a89-178">**Searchable fields** show in blue in search results.</span></span>  <span data-ttu-id="f0a89-179">Vous pouvez les utiliser dans des conditions de recherche propres au champ, par exemple :</span><span class="sxs-lookup"><span data-stu-id="f0a89-179">You can use searchable fields in search conditions specific to the field such as the following:</span></span>

```
Type: Event EventLevelName: "Error"
Type: SecurityEvent Computer:Contains("contoso.com")
Type: Event EventLevelName IN {"Error","Warning"}
```

<span data-ttu-id="f0a89-180">Les **champs interrogeables en texte libre** s’affichent en gris dans les résultats de la recherche.</span><span class="sxs-lookup"><span data-stu-id="f0a89-180">**Free text searchable fields** are shown in grey in search results.</span></span>  <span data-ttu-id="f0a89-181">Ils ne peuvent pas être utilisés avec des conditions de recherche propres au champ, à la différence des champs interrogeables.</span><span class="sxs-lookup"><span data-stu-id="f0a89-181">They cannot be used with search conditions specific to the field like searchable fields.</span></span>  <span data-ttu-id="f0a89-182">Ils ne sont interrogeables que dans le cadre de requêtes portant sur tous les champs, comme ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="f0a89-182">They are only searched when performing a query across all fields such as the following.</span></span>

```
"Error"
Type: Event "Exception"
```


### <a name="boolean-operators"></a><span data-ttu-id="f0a89-183">Opérateurs booléens</span><span class="sxs-lookup"><span data-stu-id="f0a89-183">Boolean operators</span></span>
<span data-ttu-id="f0a89-184">Avec les champs numériques et DateHeure, vous pouvez rechercher des valeurs à l’aide d’opérateurs *supérieur à*, *inférieur à* et *inférieur ou égal à*.</span><span class="sxs-lookup"><span data-stu-id="f0a89-184">With datetime and numeric fields, you can search for values using *greater than*, *lesser than*, and *lesser than or equal*.</span></span> <span data-ttu-id="f0a89-185">Vous pouvez utiliser des opérateurs simples tels que >, <, >=, <=, != dans la barre de recherche de requête.</span><span class="sxs-lookup"><span data-stu-id="f0a89-185">You can use simple operators such as >, < , >=, <= , != in the query search bar.</span></span>

<span data-ttu-id="f0a89-186">Vous pouvez interroger un journal des événements spécifique pour une période spécifique.</span><span class="sxs-lookup"><span data-stu-id="f0a89-186">You can query a specific event log for a specific period of time.</span></span> <span data-ttu-id="f0a89-187">Par exemple, l’expression mnémonique suivante permet d’exprimer les dernières 24 heures.</span><span class="sxs-lookup"><span data-stu-id="f0a89-187">For example, the last 24 hours is expressed with the following mnemonic expression.</span></span>

```
EventLog=System TimeGenerated>NOW-24HOURS
```


#### <a name="to-search-using-a-boolean-operator"></a><span data-ttu-id="f0a89-188">Pour effectuer une recherche à l'aide d'un opérateur booléen</span><span class="sxs-lookup"><span data-stu-id="f0a89-188">To search using a boolean operator</span></span>
* <span data-ttu-id="f0a89-189">Dans le champ de requête de recherche, tapez `EventLog=System TimeGenerated>NOW-24HOURS`</span><span class="sxs-lookup"><span data-stu-id="f0a89-189">In the search query field, type `EventLog=System TimeGenerated>NOW-24HOURS`</span></span>  
    <span data-ttu-id="f0a89-190">![Recherche avec des opérateurs booléens](./media/log-analytics-log-searches/oms-search-boolean.png)</span><span class="sxs-lookup"><span data-stu-id="f0a89-190">![search with boolean](./media/log-analytics-log-searches/oms-search-boolean.png)</span></span>

<span data-ttu-id="f0a89-191">Bien que vous puissiez contrôler graphiquement l'intervalle de temps, et nous vous invitons à faire cela la plupart du temps, l’ajout d’un filtre de temps directement dans la requête présente certains avantages.</span><span class="sxs-lookup"><span data-stu-id="f0a89-191">Although you can control the time interval graphically, and most times you might want to do that, there are advantages to including a time filter directly into the query.</span></span> <span data-ttu-id="f0a89-192">Par exemple, cela fonctionne très bien avec les tableaux de bord qui vous permettent de remplacer le temps pour chaque vignette, quel que soit le sélecteur de temps *global* sur la page du tableau de bord.</span><span class="sxs-lookup"><span data-stu-id="f0a89-192">For example, this works great with dashboards where you can override the time for each tile, regardless of the *global* time selector on the dashboard page.</span></span> <span data-ttu-id="f0a89-193">Pour plus d'informations, consultez [Questions relatives au temps dans le tableau de bord](http://cloudadministrator.wordpress.com/2014/10/19/system-center-advisor-restarted-time-matters-in-dashboard-part-6/).</span><span class="sxs-lookup"><span data-stu-id="f0a89-193">For more information, see [Time Matters in Dashboard](http://cloudadministrator.wordpress.com/2014/10/19/system-center-advisor-restarted-time-matters-in-dashboard-part-6/).</span></span>

<span data-ttu-id="f0a89-194">Lors du filtrage par heure, n’oubliez pas que vous obtenez des résultats pour l’ *intersection* des deux périodes : celle indiquée dans le portail OMS (S1) et celle indiquée dans la requête (S2).</span><span class="sxs-lookup"><span data-stu-id="f0a89-194">When filtering by time, keep in mind that you get results for the *intersection* of the two time periods: the one specified in the OMS portal (S1) and the one specified in the query (S2).</span></span>

![intersection](./media/log-analytics-log-searches/oms-search-intersection.png)

<span data-ttu-id="f0a89-196">Cela signifie que, si les périodes ne présentent pas d’intersection, par exemple, dans le portail OMS où vous choisissez **Cette semaine** et dans la requête où vous précisez la **semaine dernière**, il n’y a pas d’intersection et vous ne recevez aucun résultat.</span><span class="sxs-lookup"><span data-stu-id="f0a89-196">This means, if the time periods don’t intersect, for example in the OMS portal where you choose **This week** and in the query where you define **last week**, then there is no intersection and you won't receive any results.</span></span>

<span data-ttu-id="f0a89-197">Les opérateurs de comparaison utilisés pour le champ TimeGenerated sont également utiles dans d'autres situations.</span><span class="sxs-lookup"><span data-stu-id="f0a89-197">Comparison operators used for the TimeGenerated field are also useful in other situations.</span></span> <span data-ttu-id="f0a89-198">Par exemple, avec des champs numériques.</span><span class="sxs-lookup"><span data-stu-id="f0a89-198">For example, with numeric fields.</span></span>

<span data-ttu-id="f0a89-199">Par exemple, étant donné que les alertes d'évaluation de configuration ont les valeurs de gravité suivantes :</span><span class="sxs-lookup"><span data-stu-id="f0a89-199">For example, given that Configuration Assessment’s alerts have the following severity values:</span></span>

* <span data-ttu-id="f0a89-200">0 = Information</span><span class="sxs-lookup"><span data-stu-id="f0a89-200">0 = Information</span></span>
* <span data-ttu-id="f0a89-201">1 = Avertissement</span><span class="sxs-lookup"><span data-stu-id="f0a89-201">1 = Warning</span></span>
* <span data-ttu-id="f0a89-202">2 = Critique</span><span class="sxs-lookup"><span data-stu-id="f0a89-202">2 = Critical</span></span>

<span data-ttu-id="f0a89-203">Vous pouvez interroger pour les alertes d’avertissements et les alertes critiques et exclure également les alertes d'information avec la requête suivante :</span><span class="sxs-lookup"><span data-stu-id="f0a89-203">You can query for both warning and critical alerts and also exclude informational ones with the following query:</span></span>

```
Type=ConfigurationAlert  Severity>=1
```


<span data-ttu-id="f0a89-204">Vous pouvez aussi utiliser des requêtes de plage de données.</span><span class="sxs-lookup"><span data-stu-id="f0a89-204">You can also use range queries.</span></span> <span data-ttu-id="f0a89-205">Cela signifie que vous pouvez fournir la plage de valeurs de début et de fin dans une séquence.</span><span class="sxs-lookup"><span data-stu-id="f0a89-205">This means that you can provide the beginning and end range of values in a sequence.</span></span> <span data-ttu-id="f0a89-206">Par exemple, si vous souhaitez obtenir des événements du journal des événements Operations Manager où l'ID de l’événement est supérieur ou égal à 2100 mais inférieur ou égal à 2199, la requête suivante va alors les retourner.</span><span class="sxs-lookup"><span data-stu-id="f0a89-206">For example, if you want events from the Operations Manager event log where the EventID is greater than or equal to 2100 but not greater than 2199, then the following query would return them.</span></span>

```
Type=Event EventLog="Operations Manager" EventID:[2100..2199]
```


> [!NOTE]
> <span data-ttu-id="f0a89-207">La syntaxe de plage de données que vous devez utiliser est le séparateur field:value avec les deux-points (:) field:value et *non* le signe égal (=).</span><span class="sxs-lookup"><span data-stu-id="f0a89-207">The range syntax you must use is the colon (:) field:value separator and *not* the equal sign (=).</span></span> <span data-ttu-id="f0a89-208">Ajoutez l’extrémité supérieure et inférieure de la plage de données entre crochets et séparez-les par deux points (..).</span><span class="sxs-lookup"><span data-stu-id="f0a89-208">Enclose the lower and upper end of the range in square brackets and separate them with two periods (..).</span></span>
>
>

## <a name="manipulate-search-results"></a><span data-ttu-id="f0a89-209">Manipulation des résultats de la recherche</span><span class="sxs-lookup"><span data-stu-id="f0a89-209">Manipulate search results</span></span>
<span data-ttu-id="f0a89-210">Lorsque vous recherchez des données, vous devez affiner votre requête de recherche et avoir un bon niveau de contrôle sur les résultats.</span><span class="sxs-lookup"><span data-stu-id="f0a89-210">When you're searching for data, you'll want to refine your search query and have a good level of control over the results.</span></span> <span data-ttu-id="f0a89-211">Lorsque les résultats sont récupérés, vous pouvez appliquer des commandes pour les transformer.</span><span class="sxs-lookup"><span data-stu-id="f0a89-211">When results are retrieved, you can apply commands to transform them.</span></span>

<span data-ttu-id="f0a89-212">Les commandes dans les recherches de Log Analytics *doivent* se trouver après la barre verticale (|).</span><span class="sxs-lookup"><span data-stu-id="f0a89-212">Commands in Log Analytics searches *must* follow after the vertical pipe character (|).</span></span> <span data-ttu-id="f0a89-213">La première partie d'une chaîne de requête doit toujours être un filtre.</span><span class="sxs-lookup"><span data-stu-id="f0a89-213">A filter must always be the first part of a query string.</span></span> <span data-ttu-id="f0a89-214">Celui-ci définit le jeu de données avec lequel vous travaillez, puis il envoie ces résultats dans une commande.</span><span class="sxs-lookup"><span data-stu-id="f0a89-214">It defines the data set you're working with and then "pipes" those results into a command.</span></span> <span data-ttu-id="f0a89-215">Vous pouvez ensuite utiliser ce pipe pour ajouter des commandes supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="f0a89-215">You can then use the pipe to add additional commands.</span></span> <span data-ttu-id="f0a89-216">Cela est relativement similaire au pipeline Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f0a89-216">This is loosely similar to the Windows PowerShell pipeline.</span></span>

<span data-ttu-id="f0a89-217">En général, le langage de recherche de Log Analytics tente de respecter le style et les instructions PowerShell de manière à ce qu’ils soient similaires à ceux des professionnels de l’informatique et pour faciliter cette étape de l’apprentissage.</span><span class="sxs-lookup"><span data-stu-id="f0a89-217">In general, the Log Analytics search language tries to follow PowerShell style and guidelines to make it similar to the IT pros, and to ease the learning curve.</span></span>

<span data-ttu-id="f0a89-218">Le nom des commandes est un verbe, ce qui vous permet de connaître facilement leur fonction.</span><span class="sxs-lookup"><span data-stu-id="f0a89-218">Commands have names of verbs so you can easily tell what they do.</span></span>  

### <a name="sort"></a><span data-ttu-id="f0a89-219">Trier</span><span class="sxs-lookup"><span data-stu-id="f0a89-219">Sort</span></span>
<span data-ttu-id="f0a89-220">La commande de tri vous permet de définir l'ordre de tri avec un ou plusieurs champs.</span><span class="sxs-lookup"><span data-stu-id="f0a89-220">The sort command allows you to define the sorting order by one or multiple fields.</span></span> <span data-ttu-id="f0a89-221">Même si vous ne l'utilisez pas, un ordre de temps décroissant est appliqué par défaut.</span><span class="sxs-lookup"><span data-stu-id="f0a89-221">Even if you don’t use it, by default, a time descending order is enforced.</span></span> <span data-ttu-id="f0a89-222">Les résultats les plus récents sont toujours en haut des résultats de recherche.</span><span class="sxs-lookup"><span data-stu-id="f0a89-222">The most recent results are always at the top of search results.</span></span> <span data-ttu-id="f0a89-223">Cela signifie que lorsque vous exécutez une recherche avec `Type=Event EventID=1234` , ce qui est réellement exécuté pour vous est :</span><span class="sxs-lookup"><span data-stu-id="f0a89-223">This means that when you run a search, with `Type=Event EventID=1234` what really is executed for you is:</span></span>

```
Type=Event EventID=1234 **| Sort TimeGenerated desc**
```

<span data-ttu-id="f0a89-224">C’est parce qu’il s’agit du type d'expérience que vous connaissez avec les journaux.</span><span class="sxs-lookup"><span data-stu-id="f0a89-224">That's because it is the type of experience you are familiar with in logs.</span></span> <span data-ttu-id="f0a89-225">Par exemple, dans l'observateur d'événements Windows.</span><span class="sxs-lookup"><span data-stu-id="f0a89-225">For example, in the Windows Event Viewer.</span></span>

<span data-ttu-id="f0a89-226">Vous pouvez utiliser la fonction Sort pour modifier la façon dont les résultats sont retournés.</span><span class="sxs-lookup"><span data-stu-id="f0a89-226">You can use Sort to change the way results are returned.</span></span> <span data-ttu-id="f0a89-227">Les exemples suivants illustrent son fonctionnement.</span><span class="sxs-lookup"><span data-stu-id="f0a89-227">The following examples show how this works.</span></span>

```
Type=Event EventID=1234 | Sort TimeGenerated asc
```

```
Type=Event EventID=1234 | Sort Computer asc
```

```
Type=Event EventID=1234 | Sort Computer asc,TimeGenerated desc
```


<span data-ttu-id="f0a89-228">Ces simples exemples ci-dessus vous montrent le fonctionnement des commandes : elles modifient la forme des résultats que le filtre a retournés.</span><span class="sxs-lookup"><span data-stu-id="f0a89-228">The simple examples above show you how commands work--they change the shape of the results that the filter returned.</span></span>

### <a name="limit-and-top"></a><span data-ttu-id="f0a89-229">Limit et Top</span><span class="sxs-lookup"><span data-stu-id="f0a89-229">Limit and top</span></span>
<span data-ttu-id="f0a89-230">Une autre commande moins connue est LIMIT.</span><span class="sxs-lookup"><span data-stu-id="f0a89-230">Another less known command is LIMIT.</span></span> <span data-ttu-id="f0a89-231">Limit est un verbe similaire à PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f0a89-231">Limit is a PowerShell-like verb.</span></span> <span data-ttu-id="f0a89-232">Limit a la même fonction que la commande TOP.</span><span class="sxs-lookup"><span data-stu-id="f0a89-232">Limit is functionally identical to the TOP command.</span></span> <span data-ttu-id="f0a89-233">Les requêtes suivantes retournent les mêmes résultats.</span><span class="sxs-lookup"><span data-stu-id="f0a89-233">The following queries return the same results.</span></span>

```
Type=Event EventID=600 | Limit 1
```

```
Type=Event EventID=600 | Top 1
```


#### <a name="to-search-using-top"></a><span data-ttu-id="f0a89-234">Pour effectuer une recherche à l'aide de Top</span><span class="sxs-lookup"><span data-stu-id="f0a89-234">To search using top</span></span>
* <span data-ttu-id="f0a89-235">Dans le champ de requête de recherche, tapez `Type=Event EventID=600 | Top 1` .</span><span class="sxs-lookup"><span data-stu-id="f0a89-235">In the search query field, type `Type=Event EventID=600 | Top 1` </span></span>  
    <span data-ttu-id="f0a89-236">![Recherche top](./media/log-analytics-log-searches/oms-search-top.png)</span><span class="sxs-lookup"><span data-stu-id="f0a89-236">![search top](./media/log-analytics-log-searches/oms-search-top.png)</span></span>

<span data-ttu-id="f0a89-237">Dans l’image ci-dessus, il existe des 358 000 enregistrements avec l’EventID=600.</span><span class="sxs-lookup"><span data-stu-id="f0a89-237">In the image above, there are 358 thousand records with EventID=600.</span></span> <span data-ttu-id="f0a89-238">Les champs, les facettes et les filtres sur la gauche affichent toujours des informations sur les résultats retournés *par la partie du filtre* de la requête, qui est la partie située avant une barre verticale.</span><span class="sxs-lookup"><span data-stu-id="f0a89-238">The fields, facets, and filters on the left always show information about the results returned *by the filter portion* of the query, which is the part before any pipe character.</span></span> <span data-ttu-id="f0a89-239">Le panneau **Résultats** retourne uniquement le résultat le plus récent car l’exemple de commande a formé et transformé les résultats.</span><span class="sxs-lookup"><span data-stu-id="f0a89-239">The **Results** pane only returns the most recent 1 result, because the example command shaped and transformed the results.</span></span>

### <a name="select"></a><span data-ttu-id="f0a89-240">Sélectionnez</span><span class="sxs-lookup"><span data-stu-id="f0a89-240">Select</span></span>
<span data-ttu-id="f0a89-241">La commande SELECT agit comme Select-Object dans PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f0a89-241">The SELECT command behaves like Select-Object in PowerShell.</span></span> <span data-ttu-id="f0a89-242">Elle retourne des résultats filtrés qui n'ont pas toutes leurs propriétés d'origine.</span><span class="sxs-lookup"><span data-stu-id="f0a89-242">It returns filtered results that do not have all of their original properties.</span></span> <span data-ttu-id="f0a89-243">Au lieu de cela, elle sélectionne uniquement les propriétés que vous avez spécifiées.</span><span class="sxs-lookup"><span data-stu-id="f0a89-243">Instead, it selects only the properties that you specify.</span></span>

#### <a name="to-run-a-search-using-the-select-command"></a><span data-ttu-id="f0a89-244">Pour exécuter une recherche à l'aide de la commande select</span><span class="sxs-lookup"><span data-stu-id="f0a89-244">To run a search using the select command</span></span>
1. <span data-ttu-id="f0a89-245">Dans Rechercher, tapez `Type=Event` puis cliquez sur **Rechercher**.</span><span class="sxs-lookup"><span data-stu-id="f0a89-245">In Search, type `Type=Event` and then click **Search**.</span></span>
2. <span data-ttu-id="f0a89-246">Cliquez sur **+ Afficher plus** dans un des résultats pour afficher toutes les propriétés dont disposent les résultats.</span><span class="sxs-lookup"><span data-stu-id="f0a89-246">Click **+ show more** in one of the results to view all the properties that the results have.</span></span>
3. <span data-ttu-id="f0a89-247">Sélectionnez certains d’entre eux de façon explicite ; la requête devient alors `Type=Event | Select Computer,EventID,RenderedDescription`.</span><span class="sxs-lookup"><span data-stu-id="f0a89-247">Select some of those explicitly, and the query changes to `Type=Event | Select Computer,EventID,RenderedDescription`.</span></span>  
    <span data-ttu-id="f0a89-248">![Recherche select](./media/log-analytics-log-searches/oms-search-select.png)</span><span class="sxs-lookup"><span data-stu-id="f0a89-248">![search select](./media/log-analytics-log-searches/oms-search-select.png)</span></span>

<span data-ttu-id="f0a89-249">Il s’agit d’une commande particulièrement utile pour contrôler les résultats de recherche et choisir uniquement des portions de données qui importent vraiment pour l’exploration et qui, bien souvent, ne correspondent pas à la totalité de l’enregistrement.</span><span class="sxs-lookup"><span data-stu-id="f0a89-249">This command is particularly useful when you want to control search output and choose only the portions of data that really matter for your exploration, which often isn’t the full record.</span></span> <span data-ttu-id="f0a89-250">Elle est également utile lorsque des enregistrements de différents types présentent *certaines* propriétés communes, mais que leurs propriétés ne sont pas *toutes* communes.</span><span class="sxs-lookup"><span data-stu-id="f0a89-250">This is also useful when records of different types have *some* common properties, but not *all* of their properties are common.</span></span> <span data-ttu-id="f0a89-251">Vous pouvez générer des résultats qui ressemblent plus naturellement à une table ou fonctionnent bien lorsqu’ils sont exportés vers un fichier CSV puis envoyés dans Excel.</span><span class="sxs-lookup"><span data-stu-id="f0a89-251">The, you can generate output that looks more naturally like a table, or work well when exported to a CSV file and then massaged in Excel.</span></span>

## <a name="use-the-measure-command"></a><span data-ttu-id="f0a89-252">Utilisation de la commande measure</span><span class="sxs-lookup"><span data-stu-id="f0a89-252">Use the measure command</span></span>
<span data-ttu-id="f0a89-253">MEASURE est une des commandes les plus polyvalentes dans les recherches de Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="f0a89-253">MEASURE is one of the most versatile commands in Log Analytics searches.</span></span> <span data-ttu-id="f0a89-254">Elle vous permet d'appliquer des *fonctions* statistiques à vos données et de regrouper des résultats par champ donné.</span><span class="sxs-lookup"><span data-stu-id="f0a89-254">It allows you to apply statistical *functions* to your data and aggregate results grouped by a given field.</span></span> <span data-ttu-id="f0a89-255">Il existe plusieurs fonctions statistiques qui prennent en charge Measure.</span><span class="sxs-lookup"><span data-stu-id="f0a89-255">There are multiple statistical functions that Measure supports.</span></span>

### <a name="measure-count"></a><span data-ttu-id="f0a89-256">La fonction count() de Measure</span><span class="sxs-lookup"><span data-stu-id="f0a89-256">Measure count()</span></span>
<span data-ttu-id="f0a89-257">La première fonction statistique à utiliser et la plus simple à comprendre est la fonction *count()* .</span><span class="sxs-lookup"><span data-stu-id="f0a89-257">The first statistical function to work with, and one of the simplest to understand is the *count()* function.</span></span>

<span data-ttu-id="f0a89-258">Les résultats d'une requête de recherche telle que `Type=Event`, affichent des filtres, également appelés facettes, sur le côté gauche des résultats de la recherche.</span><span class="sxs-lookup"><span data-stu-id="f0a89-258">Results from any search query such as `Type=Event`, show filters also called facets on the left side of search results.</span></span> <span data-ttu-id="f0a89-259">Les filtres montrent une distribution de valeurs pour un champ donné dans les résultats de la recherche effectuée.</span><span class="sxs-lookup"><span data-stu-id="f0a89-259">The filters show a distribution of values by a given field for the results in the search executed.</span></span>

![Recherche measure count](./media/log-analytics-log-searches/oms-search-measure-count01.png)

<span data-ttu-id="f0a89-261">Par exemple, dans l’image ci-dessus, vous voyez le champ **Computer**. L’image montre que, parmi les près de 739 000 événements figurant dans les résultats, 68 contiennent des valeurs uniques et distinctes dans le champ **Computer**.</span><span class="sxs-lookup"><span data-stu-id="f0a89-261">For example, in the image above you'll see the **Computer** field and it shows that within the almost 739 thousand events in the results, there are 68 unique and distinct values for the **Computer** field in those records.</span></span> <span data-ttu-id="f0a89-262">La vignette affiche uniquement les 5 premières, qui sont les 5 valeurs les plus courantes écrites dans le champ **Ordinateur** , triées par nombre de documents contenant cette valeur spécifique dans ce champ.</span><span class="sxs-lookup"><span data-stu-id="f0a89-262">The tile only shows the top 5, which are the most common 5 values that are written in the **Computer** fields), sorted by the number of documents that contain that specific value in that field.</span></span> <span data-ttu-id="f0a89-263">L’image montre que, parmi ces près de 369 000 événements, 90 000 proviennent de l’ordinateur OpsInsights04.contoso.com, 83 0000 de l’ordinateur DB03.contoso.com, et ainsi de suite.</span><span class="sxs-lookup"><span data-stu-id="f0a89-263">In the image you can see that – among those almost 369 thousand events – 90 thousand come from the OpsInsights04.contoso.com computer, 83 thousand from the DB03.contoso.com computer, and so on.</span></span>

<span data-ttu-id="f0a89-264">Comment faire si vous souhaitez voir toutes les valeurs, étant donné que la vignette ne montre que les 5 premières ?</span><span class="sxs-lookup"><span data-stu-id="f0a89-264">What if you want to see all values, since the tile only shows only the top 5?</span></span>

<span data-ttu-id="f0a89-265">C'est ce que la commande Measure permet de faire avec la fonction count().</span><span class="sxs-lookup"><span data-stu-id="f0a89-265">That’s what the measure command can do with the count() function.</span></span> <span data-ttu-id="f0a89-266">Cette fonction n'utilise aucun paramètre.</span><span class="sxs-lookup"><span data-stu-id="f0a89-266">This function doesn't use any parameters.</span></span> <span data-ttu-id="f0a89-267">Vous spécifiez simplement le champ par lequel vous voulez regrouper – le champ **Ordinateur** dans ce cas :</span><span class="sxs-lookup"><span data-stu-id="f0a89-267">You just specify the field by which you want to group by – the **Computer** field in this case:</span></span>

`Type=Event | Measure count() by Computer`

![Recherche measure count](./media/log-analytics-log-searches/oms-search-measure-count-computer.png)

<span data-ttu-id="f0a89-269">Le champ **Computer** est toutefois simplement un champ utilisé *dans* chaque élément de données : aucune base de données relationnelle n’est impliquée, et il n’existe aucun objet **Computer**distinct nulle part.</span><span class="sxs-lookup"><span data-stu-id="f0a89-269">However, **Computer** is just a field used *in* each piece of data – there are no relational databases involved and there is no separate **Computer** object anywhere.</span></span> <span data-ttu-id="f0a89-270">Simplement, les valeurs *dans* les données peuvent décrire l’entité qui les a générées, ainsi qu’un certain nombre d’autres caractéristiques et aspects des données, d’où le terme *facette*.</span><span class="sxs-lookup"><span data-stu-id="f0a89-270">Just the values *in* the data can describe which entity generated them, and a number of other characteristics and aspects of the data – hence the term *facet*.</span></span> <span data-ttu-id="f0a89-271">Toutefois, vous pouvez également les regrouper par d'autres champs.</span><span class="sxs-lookup"><span data-stu-id="f0a89-271">However, you can just as well group by other fields.</span></span> <span data-ttu-id="f0a89-272">Étant donné que les résultats d’origine des près de 739 000 événements canalisés dans la commande Measure ont également un champ nommé **EventID**, vous pouvez appliquer la même technique pour regrouper par ce champ et obtenir un nombre d’événements par EventID :</span><span class="sxs-lookup"><span data-stu-id="f0a89-272">Because the original results of almost 739 thousand events that are piped into the measure command also have a field called **EventID**, you can apply the same technique to group by that field and get a count of events by EventID:</span></span>

```
Type=Event | Measure count() by EventID
```

<span data-ttu-id="f0a89-273">Si vous n'êtes pas intéressé par le nombre d'enregistrements réels qui contiennent une valeur spécifique, mais que vous souhaitez seulement une liste de valeurs elles-mêmes, vous pouvez ajouter une commande *Sélect* à la fin de celle-ci et simplement sélectionner la première colonne :</span><span class="sxs-lookup"><span data-stu-id="f0a89-273">If you're not interested in the actual record count that contain a specific value, but instead if you only want a list of the values themselves, you can add a *Select* command at the end of it and just select the first column:</span></span>

```
Type=Event | Measure count() by EventID | Select EventID
```

<span data-ttu-id="f0a89-274">Vous pouvez ensuite obtenir des résultats de requête plus complexes et les trier, ou vous pouvez aussi simplement cliquer sur les colonnes dans la grille.</span><span class="sxs-lookup"><span data-stu-id="f0a89-274">Then you can get more intricate and pre-sort the results in the query, or you can just click the columns in the grid, too.</span></span>

```
Type=Event | Measure count() by EventID | Select EventID | Sort EventID asc
```

#### <a name="to-search-using-measure-count"></a><span data-ttu-id="f0a89-275">Pour effectuer une recherche à l'aide de measure count</span><span class="sxs-lookup"><span data-stu-id="f0a89-275">To search using measure count</span></span>
* <span data-ttu-id="f0a89-276">Dans le champ de requête de recherche, tapez `Type=Event | Measure count() by EventID`</span><span class="sxs-lookup"><span data-stu-id="f0a89-276">In the search query field, type `Type=Event | Measure count() by EventID`</span></span>
* <span data-ttu-id="f0a89-277">Ajoutez `| Select EventID` à la fin de la requête.</span><span class="sxs-lookup"><span data-stu-id="f0a89-277">Append `| Select EventID` to the end of the query.</span></span>
* <span data-ttu-id="f0a89-278">Enfin, ajoutez `| Sort EventID asc` à la fin de la requête.</span><span class="sxs-lookup"><span data-stu-id="f0a89-278">Finally, append `| Sort EventID asc` to the end of the query.</span></span>

<span data-ttu-id="f0a89-279">Il est important de comprendre et de mettre en évidence certains points essentiels :</span><span class="sxs-lookup"><span data-stu-id="f0a89-279">There are a couple important points to notice and emphasize:</span></span>

<span data-ttu-id="f0a89-280">Tout d'abord, les résultats que vous voyez ne sont plus les résultats bruts d'origine.</span><span class="sxs-lookup"><span data-stu-id="f0a89-280">First, the results you see are not the original raw results anymore.</span></span> <span data-ttu-id="f0a89-281">Il s’agit en fait de résultats agrégés : autrement dit, des groupes de résultats.</span><span class="sxs-lookup"><span data-stu-id="f0a89-281">Instead, they are aggregated results – essentially groups of results.</span></span> <span data-ttu-id="f0a89-282">Cela n'est pas un problème, mais vous devez comprendre que vous interagissez avec une toute autre forme de données qui diffère de la forme brute d'origine créée en cours de route lorsque la fonction d'agrégation ou statistique est utilisée.</span><span class="sxs-lookup"><span data-stu-id="f0a89-282">This isn't a problem, but you should understand that you're interacting with a very different shape of data that differs from the original raw shape that gets created on the fly as a result of the aggregation/statistical function.</span></span>

<span data-ttu-id="f0a89-283">Ensuite, la fonction **Measure count** ne retourne pour le moment que les 100 premiers résultats distincts.</span><span class="sxs-lookup"><span data-stu-id="f0a89-283">Second, **Measure count** currently returns only the top 100 distinct results.</span></span> <span data-ttu-id="f0a89-284">Cette limite ne s'applique pas aux autres fonctions statistiques.</span><span class="sxs-lookup"><span data-stu-id="f0a89-284">This limit does not apply to the other statistical functions.</span></span> <span data-ttu-id="f0a89-285">Par conséquent, vous devez généralement utiliser d’abord un filtre plus précis pour rechercher des éléments spécifiques avant d'appliquer measure count().</span><span class="sxs-lookup"><span data-stu-id="f0a89-285">So, you'll usually need to use a more precise filter first to search for specific items before you apply measure count().</span></span>

## <a name="use-the-max-and-min-functions-with-the-measure-command"></a><span data-ttu-id="f0a89-286">Utilisation des fonctions min et max avec la commande measure</span><span class="sxs-lookup"><span data-stu-id="f0a89-286">Use the max and min functions with the measure command</span></span>
<span data-ttu-id="f0a89-287">Il existe plusieurs situations où les commandes **Measure Max()** et **Measure Min()** sont utiles.</span><span class="sxs-lookup"><span data-stu-id="f0a89-287">There are various scenarios where **Measure Max()** and **Measure Min()** are useful.</span></span> <span data-ttu-id="f0a89-288">Toutefois, étant donné que chaque fonction est l'opposé de l'autre, nous démontrerons la fonction Max() et vous pourrez ensuite tester vous-même la fonction Min().</span><span class="sxs-lookup"><span data-stu-id="f0a89-288">However, since each function is opposite of each other, we'll illustrate Max() and you can experiment with Min() on your own.</span></span>

<span data-ttu-id="f0a89-289">Si vous interrogez des événements de sécurité, ceux-ci ont une propriété **Level** qui peut varier.</span><span class="sxs-lookup"><span data-stu-id="f0a89-289">If you query for security events, they have a **Level** property that can vary.</span></span> <span data-ttu-id="f0a89-290">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="f0a89-290">For example:</span></span>

```
Type=SecurityEvent
```

![Recherche du début de la fonction measure count](./media/log-analytics-log-searches/oms-search-measure-max01.png)

<span data-ttu-id="f0a89-292">Si vous souhaitez afficher la valeur la plus élevée de toutes les alertes de sécurité pour un ordinateur commun donné, puis les grouper par champ, vous pouvez utiliser la syntaxe suivante :</span><span class="sxs-lookup"><span data-stu-id="f0a89-292">If you want to view the highest value for all of the security events given a common Computer, the group by field, you can use</span></span>

```
Type=ConfigurationAlert | Measure Max(Level) by Computer
```

![Recherche l’ordinateur de la fonction measure max](./media/log-analytics-log-searches/oms-search-measure-max02.png)

<span data-ttu-id="f0a89-294">Elle indique que, pour les ordinateurs ayant des enregistrements **Level**, la plupart ont au moins le niveau 8, et un grand nombre ont le niveau 16.</span><span class="sxs-lookup"><span data-stu-id="f0a89-294">It will display that for the computers that had **Level** records, most of them have at least level 8, many had a level of 16.</span></span>

```
Type=ConfigurationAlert | Measure Max(Severity) by Computer
```

![Recherche l’ordinateur qui génère la valeur horaire measure max](./media/log-analytics-log-searches/oms-search-measure-max03.png)

<span data-ttu-id="f0a89-296">Cette fonction fonctionne bien avec les nombres, mais elle fonctionne également avec les champs DateHeure.</span><span class="sxs-lookup"><span data-stu-id="f0a89-296">This function works well with numbers, but it also works with DateTime fields.</span></span> <span data-ttu-id="f0a89-297">Il est utile de vérifier l'horodatage de la dernière heure ou de l’heure la plus récente pour tout type de données indexé pour chaque ordinateur.</span><span class="sxs-lookup"><span data-stu-id="f0a89-297">It is useful to check for the last or most recent time stamp for any piece of data indexed for each computer.</span></span> <span data-ttu-id="f0a89-298">Par exemple : quand l’événement de sécurité plus récent a-t-il été signalé pour chaque ordinateur ?</span><span class="sxs-lookup"><span data-stu-id="f0a89-298">For example: When was the most recent security event reported for each machine?</span></span>

```
Type=ConfigurationChange | Measure Max(TimeGenerated) by Computer
```

## <a name="use-the-avg-function-with-the-measure-command"></a><span data-ttu-id="f0a89-299">Utilisation de la fonction avg avec la commande measure</span><span class="sxs-lookup"><span data-stu-id="f0a89-299">Use the avg function with the measure command</span></span>
<span data-ttu-id="f0a89-300">La fonction statistique Avg() utilisée avec measure vous permet de calculer la valeur moyenne pour un champ et de grouper les résultats selon ce même champ ou un autre.</span><span class="sxs-lookup"><span data-stu-id="f0a89-300">The Avg() statistical function used with measure allows you to calculate the average value for some field, and group results by the same or other field.</span></span> <span data-ttu-id="f0a89-301">Cela est utile dans de nombreux cas, pour les données de performances par exemple.</span><span class="sxs-lookup"><span data-stu-id="f0a89-301">This is useful in a variety of cases, such as performance data.</span></span>

<span data-ttu-id="f0a89-302">Nous allons commencer par les données de performances.</span><span class="sxs-lookup"><span data-stu-id="f0a89-302">We'll start with performance data.</span></span> <span data-ttu-id="f0a89-303">Remarque : OMS collecte actuellement les compteurs de performance pour les ordinateurs Windows et Linux.</span><span class="sxs-lookup"><span data-stu-id="f0a89-303">Note that OMS currently collects performance counters for both Windows and Linux machines.</span></span>

<span data-ttu-id="f0a89-304">Pour rechercher *toutes* les données de performances, la requête la plus simple est :</span><span class="sxs-lookup"><span data-stu-id="f0a89-304">To search for *all* performance data, the most basic query is:</span></span>

```
Type=Perf
```

![Recherche du début de la fonction avg](./media/log-analytics-log-searches/oms-search-avg01.png)

<span data-ttu-id="f0a89-306">La première chose que vous pouvez remarquer est que Log Analytics présente trois perspectives : Liste, qui montre les enregistrements réels sous-jacents aux graphiques ; Table, qui montre une vue tabulaire des données d’un compteur de performances ; et Mesures, qui montre des graphiques pour les compteurs de performances.</span><span class="sxs-lookup"><span data-stu-id="f0a89-306">The first thing you'll notice is that Log Analytics shows you three perspectives: List, which shows you which shows the actual records behind the charts; Table, which shows a tabular view of performance counter data; and Metrics, which shows charts for the performance counters.</span></span>

<span data-ttu-id="f0a89-307">Dans l'image ci-dessus, il existe deux ensembles de champs marqués qui indiquent les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="f0a89-307">In the image above, there are two sets of fields marked that indicate the following:</span></span>

* <span data-ttu-id="f0a89-308">Le premier jeu identifie le nom du compteur de performances Windows, le nom de l’objet et le nom de l’instance dans le filtre de la requête.</span><span class="sxs-lookup"><span data-stu-id="f0a89-308">The first set identifies Windows Performance Counter Name, Object Name, and Instance Name in the query filter.</span></span> <span data-ttu-id="f0a89-309">Il s’agit des champs que vous utiliserez probablement le plus souvent en tant que facettes ou filtres.</span><span class="sxs-lookup"><span data-stu-id="f0a89-309">These are the fields you probably will most commonly use as facets/filters</span></span>
* <span data-ttu-id="f0a89-310">**CounterValue** est la valeur réelle du compteur.</span><span class="sxs-lookup"><span data-stu-id="f0a89-310">**CounterValue** is the actual value of the counter.</span></span> <span data-ttu-id="f0a89-311">Dans cet exemple, la valeur est *75*.</span><span class="sxs-lookup"><span data-stu-id="f0a89-311">In this example, the value is *75*.</span></span>
* <span data-ttu-id="f0a89-312">**TimeGenerated** a la valeur 12:51, au format 24 heures.</span><span class="sxs-lookup"><span data-stu-id="f0a89-312">**TimeGenerated** is 12:51, in 24-hour time format.</span></span>

<span data-ttu-id="f0a89-313">Voici une vue des mesures dans un graphique.</span><span class="sxs-lookup"><span data-stu-id="f0a89-313">Here's a view of the metrics in a graph.</span></span>

![Recherche du début de la fonction avg](./media/log-analytics-log-searches/oms-search-avg02.png)

<span data-ttu-id="f0a89-315">Après avoir lu ce qui concerne la forme d’enregistrement Perf et ce qui concerne d’autres techniques de recherche, vous pouvez utiliser measure Avg() pour agréger ce type de données numériques.</span><span class="sxs-lookup"><span data-stu-id="f0a89-315">After reading about the Perf record shape, and having read about other search techniques, you can use measure Avg() to aggregate this type of numerical data.</span></span>

<span data-ttu-id="f0a89-316">Voici un exemple simple :</span><span class="sxs-lookup"><span data-stu-id="f0a89-316">Here's a simple example:</span></span>

```
Type=Perf  ObjectName:Processor  InstanceName:_Total  CounterName:"% Processor Time" | Measure Avg(CounterValue) by Computer
```

![Recherche de l’exemple de valeur de la fonction avg](./media/log-analytics-log-searches/oms-search-avg03.png)

<span data-ttu-id="f0a89-318">Dans cet exemple, vous sélectionnez le compteur de performance du temps processeur total et la moyenne par ordinateur.</span><span class="sxs-lookup"><span data-stu-id="f0a89-318">In this example, you select the CPU Total Time performance counter and average by Computer.</span></span> <span data-ttu-id="f0a89-319">Si vous souhaitez restreindre les résultats aux 6 dernières heures, vous pouvez utiliser le contrôle de filtre de temps ou ajouter une mention spéciale à votre requête, comme suit :</span><span class="sxs-lookup"><span data-stu-id="f0a89-319">If you want to narrow down your results to only the last 6 hours, you can either use the time filter control or specify in your query as follows:</span></span>

```
Type=Perf  ObjectName:Processor  InstanceName:_Total  CounterName:"% Processor Time" TimeGenerated>NOW-6HOURS | Measure Avg(CounterValue) by Computer
```

### <a name="to-search-using-the-avg-function-with-the-measure-command"></a><span data-ttu-id="f0a89-320">Rechercher à l’aide de la fonction avg avec la commande measure</span><span class="sxs-lookup"><span data-stu-id="f0a89-320">To search using the avg function with the measure command</span></span>
* <span data-ttu-id="f0a89-321">Dans le champ de requête de recherche, tapez `Type=Perf  ObjectName:Processor  InstanceName:_Total  CounterName:"% Processor Time" TimeGenerated>NOW-6HOURS | Measure Avg(CounterValue) by Computer`.</span><span class="sxs-lookup"><span data-stu-id="f0a89-321">In the Search query box, type `Type=Perf  ObjectName:Processor  InstanceName:_Total  CounterName:"% Processor Time" TimeGenerated>NOW-6HOURS | Measure Avg(CounterValue) by Computer`.</span></span>

<span data-ttu-id="f0a89-322">Vous pouvez agréger et corréler les données *entre* plusieurs ordinateurs.</span><span class="sxs-lookup"><span data-stu-id="f0a89-322">You can aggregate and correlate data *across* computers.</span></span> <span data-ttu-id="f0a89-323">Par exemple, imaginez que vous disposez d'un ensemble d'hôtes dans une sorte de batterie de serveurs où chaque nœud est égal à n'importe quel autre et ils effectuent simplement le même type de travail et la charge doit être à peu près équilibrée.</span><span class="sxs-lookup"><span data-stu-id="f0a89-323">For example, imagine that you have a set of hosts in some sort of farm where each node is equal to any other one and they just do all the same type of work and load should be roughly balanced.</span></span> <span data-ttu-id="f0a89-324">Vous pouvez obtenir leurs compteurs en une seule fois avec la requête suivante et obtenir des moyennes pour l’ensemble de la batterie.</span><span class="sxs-lookup"><span data-stu-id="f0a89-324">You could get their counters all in one go with the following query and get averages for the entire farm.</span></span> <span data-ttu-id="f0a89-325">Vous pouvez commencer en choisissant les ordinateurs avec l'exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="f0a89-325">You can start by choosing the computers with the following example:</span></span>

```
Type=Perf AND (Computer="AzureMktg01" OR Computer="AzureMktg02" OR Computer="AzureMktg03")
```

<span data-ttu-id="f0a89-326">Maintenant que vous avez les ordinateurs, vous ne devez sélectionner que deux indicateurs de performance clés (KPI) : le pourcentage d’utilisation du processeur et le pourcentage d’espace disque disponible.</span><span class="sxs-lookup"><span data-stu-id="f0a89-326">Now that you have the computers, you also only want to select two key performance indicators (KPIs): % CPU Usage and % Free Disk Space.</span></span> <span data-ttu-id="f0a89-327">Par conséquent, cette partie de la requête devient :</span><span class="sxs-lookup"><span data-stu-id="f0a89-327">So, that part of the query becomes:</span></span>

```
Type=Perf InstanceName:_Total  ((ObjectName:Processor AND CounterName:"% Processor Time") OR (ObjectName="LogicalDisk" AND CounterName="% Free Space")) AND TimeGenerated>NOW-4HOURS
```

<span data-ttu-id="f0a89-328">Vous pouvez maintenant ajouter des ordinateurs et des compteurs avec l'exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="f0a89-328">Now you can add computers and counters with the following example:</span></span>

```
Type=Perf InstanceName:_Total  ((ObjectName:Processor AND CounterName:"% Processor Time") OR (ObjectName="LogicalDisk" AND CounterName="% Free Space")) AND TimeGenerated>NOW-4HOURS AND (Computer="AzureMktg01" OR Computer="AzureMktg02" OR Computer="AzureMktg03")
```

<span data-ttu-id="f0a89-329">Étant donné que vous avez une sélection très spécifique, la commande **measure Avg()** peut retourner la moyenne non par ordinateur mais pour l’ensemble de la batterie de serveurs, simplement en effectuant un regroupement par CounterName.</span><span class="sxs-lookup"><span data-stu-id="f0a89-329">Because you have a very specific selection, the **measure Avg()** command can return the average not by computer, but across the farm, simply by grouping by CounterName.</span></span> <span data-ttu-id="f0a89-330">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="f0a89-330">For example:</span></span>

```
Type=Perf  InstanceName:_Total  ((ObjectName:Processor AND CounterName:"% Processor Time") OR (ObjectName="LogicalDisk" AND CounterName="% Free Space")) AND TimeGenerated>NOW-4HOURS AND (Computer="AzureMktg01" OR Computer="AzureMktg02" OR Computer="AzureMktg03") | Measure Avg(CounterValue) by CounterName
```

<span data-ttu-id="f0a89-331">Cela vous donne une vue compacte utile de quelques indicateurs de performance clés de votre environnement.</span><span class="sxs-lookup"><span data-stu-id="f0a89-331">This gives you a useful compact view of a couple of your environment's KPIs.</span></span>

![Recherche du groupement de la fonction avg](./media/log-analytics-log-searches/oms-search-avg04.png)

<span data-ttu-id="f0a89-333">Vous pouvez facilement utiliser la requête de recherche dans un tableau de bord.</span><span class="sxs-lookup"><span data-stu-id="f0a89-333">You can easily use the search query in a dashboard.</span></span> <span data-ttu-id="f0a89-334">Par exemple, vous pouvez enregistrer la requête de recherche, puis créer un tableau de bord à partir de celle-ci, nommé *Indicateurs de performance clés (KPI) de batterie de serveurs web*.</span><span class="sxs-lookup"><span data-stu-id="f0a89-334">For example, you could save the search query and create a dashboard from it named *Web Farm KPIs*.</span></span> <span data-ttu-id="f0a89-335">Pour en savoir plus sur l’utilisation de tableaux de bord, consultez [Créer un tableau de bord personnalisé dans Log Analytics](log-analytics-dashboards.md).</span><span class="sxs-lookup"><span data-stu-id="f0a89-335">To learn more about using dashboards, see [Create a custom dashboard in Log Analytics](log-analytics-dashboards.md).</span></span>

![Tableau de bord de recherche avg](./media/log-analytics-log-searches/oms-search-avg05.png)

### <a name="use-the-sum-function-with-the-measure-command"></a><span data-ttu-id="f0a89-337">Utilisation de la fonction sum avec la commande measure</span><span class="sxs-lookup"><span data-stu-id="f0a89-337">Use the sum function with the measure command</span></span>
<span data-ttu-id="f0a89-338">La fonction sum est similaire à d'autres fonctions de la commande measure.</span><span class="sxs-lookup"><span data-stu-id="f0a89-338">The sum function is similar to other functions of the measure command.</span></span> <span data-ttu-id="f0a89-339">Vous pouvez voir un exemple sur la façon d'utiliser la fonction sum dans [Recherche de journaux IIS W3C dans Microsoft Azure Operational Insights](http://blogs.msdn.com/b/dmuscett/archive/2014/09/20/w3c-iis-logs-search-in-system-center-advisor-limited-preview.aspx).</span><span class="sxs-lookup"><span data-stu-id="f0a89-339">You can see an example about how to use the sum function at [W3C IIS Logs Search in Microsoft Azure Operational Insights](http://blogs.msdn.com/b/dmuscett/archive/2014/09/20/w3c-iis-logs-search-in-system-center-advisor-limited-preview.aspx).</span></span>

<span data-ttu-id="f0a89-340">Vous pouvez utiliser les fonctions Max() et Min() avec des chaînes de nombres, de dates et heures, et de texte.</span><span class="sxs-lookup"><span data-stu-id="f0a89-340">You can use Max() and Min() with numbers, date times and text strings.</span></span> <span data-ttu-id="f0a89-341">Avec des chaînes de texte, elles sont triées par ordre alphabétique et vous pouvez obtenir la première et la dernière.</span><span class="sxs-lookup"><span data-stu-id="f0a89-341">With text strings, they are sorted alphabetically and you get first and last.</span></span>

<span data-ttu-id="f0a89-342">Toutefois, vous ne pouvez pas utiliser Sum() uniquement avec des champs numériques.</span><span class="sxs-lookup"><span data-stu-id="f0a89-342">However, you cannot use Sum() with anything other than numerical fields.</span></span> <span data-ttu-id="f0a89-343">Cela vaut également pour la fonction Avg().</span><span class="sxs-lookup"><span data-stu-id="f0a89-343">This also applies to Avg().</span></span>

### <a name="use-the-percentile-function-with-the-measure-command"></a><span data-ttu-id="f0a89-344">Utilisation de la fonction percentile avec la commande measure</span><span class="sxs-lookup"><span data-stu-id="f0a89-344">Use the percentile function with the measure command</span></span>
<span data-ttu-id="f0a89-345">La fonction percentile est similaire à Avg() et Sum() dans la mesure où vous pouvez l’utiliser uniquement pour les champs numériques.</span><span class="sxs-lookup"><span data-stu-id="f0a89-345">The percentile function is similar to Avg() and Sum() in that you can only use it for numerical fields.</span></span> <span data-ttu-id="f0a89-346">Vous pouvez utiliser n’importe quel pourcentage entre 1 et 99 sur un champ numérique.</span><span class="sxs-lookup"><span data-stu-id="f0a89-346">You can use any percentile between 1 to 99 on a numeric field.</span></span> <span data-ttu-id="f0a89-347">Vous pouvez également utiliser les deux commandes **percentile** et **pct**.</span><span class="sxs-lookup"><span data-stu-id="f0a89-347">You can also use both **percentile** and **pct** commands.</span></span> <span data-ttu-id="f0a89-348">Voici quelques exemples :</span><span class="sxs-lookup"><span data-stu-id="f0a89-348">Here are few examples:</span></span>  

```
Type:Perf CounterName:"DiskTransers/sec" |measure percentile95(CurrentValue) by Computer
```
```
Type:Perf ObjectName=LogicalDisk CounterName="Current Disk Queue Length" Computer="MyComputerName" | measure pct65(CurrentValue) by InstanceName
```

## <a name="use-the-where-command"></a><span data-ttu-id="f0a89-349">Utilisation de la commande where</span><span class="sxs-lookup"><span data-stu-id="f0a89-349">Use the where command</span></span>
<span data-ttu-id="f0a89-350">La commande where fonctionne comme un filtre, mais elle peut être appliquée dans le pipeline pour filtrer davantage les résultats agrégés résultant d’une commande Measure – au lieu des résultats bruts qui sont filtrés au début d'une requête.</span><span class="sxs-lookup"><span data-stu-id="f0a89-350">The where command works like a filter, but it can be applied in the pipeline to further filter aggregated results that have been produced by a Measure command – as opposed to raw results that are filtered at the beginning of a query.</span></span>

<span data-ttu-id="f0a89-351">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="f0a89-351">For example:</span></span>

```
Type=Perf  CounterName="% Processor Time"  InstanceName="_Total" | Measure Avg(CounterValue) as AVGCPU by Computer
```

<span data-ttu-id="f0a89-352">Vous pouvez ajouter une autre barre verticale « | » et la commande Where pour obtenir uniquement les ordinateurs dont la moyenne du processeur est supérieure à 80 %, avec l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="f0a89-352">You can add another pipe "|" character and the Where command to only get computers whose average CPU is above 80%, with the following example:</span></span>

```
Type=Perf  CounterName="% Processor Time"  InstanceName="_Total" | Measure Avg(CounterValue) as AVGCPU by Computer | Where AVGCPU>80
```

<span data-ttu-id="f0a89-353">Si vous êtes familiarisé avec Microsoft System Center - Operations Manager, vous pouvez considérer la commande where comme un pack d’administration.</span><span class="sxs-lookup"><span data-stu-id="f0a89-353">If you're familiar with Microsoft System Center - Operations Manager, you can think of the where command in management pack terms.</span></span> <span data-ttu-id="f0a89-354">S'il l'exemple était une règle, la première partie de la requête serait la source de données et la commande where serait la détection de condition.</span><span class="sxs-lookup"><span data-stu-id="f0a89-354">If the example were a rule, the first part of the query would be the data source and the where command would be the condition detection.</span></span>

<span data-ttu-id="f0a89-355">Vous pouvez utiliser la requête sous forme de vignette dans **Mon tableau de bord**, comme un moniteur de tri, afin de voir à quel moment les processeurs de l'ordinateur sont surexploités.</span><span class="sxs-lookup"><span data-stu-id="f0a89-355">You can use the query as a tile in **My Dashboard**, as a monitor of sorts, to see when computer CPUs are over-utilized.</span></span> <span data-ttu-id="f0a89-356">Pour en savoir plus sur les tableaux de bord, consultez [Créer un tableau de bord personnalisé dans Log Analytics](log-analytics-dashboards.md).</span><span class="sxs-lookup"><span data-stu-id="f0a89-356">To learn more about dashboards, see [Create a custom dashboard in Log Analytics](log-analytics-dashboards.md).</span></span> <span data-ttu-id="f0a89-357">Vous pouvez également créer et utiliser des tableaux de bord à l'aide de l'application mobile.</span><span class="sxs-lookup"><span data-stu-id="f0a89-357">You can also create and use dashboards using the mobile app.</span></span> <span data-ttu-id="f0a89-358">Pour plus d’informations, voir [Applications mobiles OMS](http://www.windowsphone.com/en-us/store/app/operational-insights/4823b935-83ce-466c-82bb-bd0a3f58d865).</span><span class="sxs-lookup"><span data-stu-id="f0a89-358">For more information, see [OMS Mobile App ](http://www.windowsphone.com/en-us/store/app/operational-insights/4823b935-83ce-466c-82bb-bd0a3f58d865).</span></span> <span data-ttu-id="f0a89-359">En bas des deux vignettes de l'image suivante, vous pouvez voir que le moniteur a affiché une liste et un nombre.</span><span class="sxs-lookup"><span data-stu-id="f0a89-359">In the bottom two tiles of the following image, you can see the monitor displayed a list and as a number.</span></span> <span data-ttu-id="f0a89-360">Essentiellement, le nombre doit toujours être zéro et la liste doit toujours être vide.</span><span class="sxs-lookup"><span data-stu-id="f0a89-360">Essentially, you always want the number to be zero and the list to be empty.</span></span> <span data-ttu-id="f0a89-361">Dans le cas contraire, il indique une condition d'alerte.</span><span class="sxs-lookup"><span data-stu-id="f0a89-361">Otherwise, it indicates an alert condition.</span></span> <span data-ttu-id="f0a89-362">Au besoin, vous pouvez l'utiliser pour voir quels ordinateurs sont sous pression.</span><span class="sxs-lookup"><span data-stu-id="f0a89-362">If needed, you can use it to take a look at which machines are under pressure.</span></span>

![Tableau de bord mobile](./media/log-analytics-log-searches/oms-search-mobile.png)

## <a name="use-the-in-operator"></a><span data-ttu-id="f0a89-364">Utilisation de l’opérateur in</span><span class="sxs-lookup"><span data-stu-id="f0a89-364">Use the in operator</span></span>
<span data-ttu-id="f0a89-365">Les opérateurs *IN* et *NOT IN* vous permettent d’effectuer des sous-recherches, c’est-à-dire des recherches incluant une autre recherche en tant qu’argument.</span><span class="sxs-lookup"><span data-stu-id="f0a89-365">The *IN* operator, along with *NOT IN* allows you to use subsearches, which are searches that include another search as an argument.</span></span> <span data-ttu-id="f0a89-366">Elles sont contenues entre accolades {} à l’intérieur d’une autre recherche *principale* ou *externe*.</span><span class="sxs-lookup"><span data-stu-id="f0a89-366">They are contained in braces {} within another *primary* or *outer* search.</span></span> <span data-ttu-id="f0a89-367">Le résultat d’une sous-recherche, souvent une liste de résultats distincts, sert ensuite d’argument pour la recherche principale.</span><span class="sxs-lookup"><span data-stu-id="f0a89-367">The result of a subsearch, often a list of distinct results, is then used as an argument in its primary search.</span></span>

<span data-ttu-id="f0a89-368">Vous pouvez utiliser les sous-recherches pour faire correspondre des sous-ensembles de données que vous ne pouvez pas décrire directement dans une expression de recherche, mais qui peuvent être générés à partir d’une recherche.</span><span class="sxs-lookup"><span data-stu-id="f0a89-368">You can use subsearches to match subsets of your data that you cannot describe directly in a search expression, but which can be generated from a search.</span></span> <span data-ttu-id="f0a89-369">Par exemple, si vous souhaitez utiliser une recherche pour trouver tous les événements survenus sur des *ordinateurs auxquels manquent des mises à jour de sécurité*, vous devez concevoir une sous-recherche qui identifie d’abord les *ordinateurs auxquels manquent des mises à jour de sécurité*, avant de rechercher des événements associés à ces hôtes.</span><span class="sxs-lookup"><span data-stu-id="f0a89-369">For example, if you’re interested in using one search to find all events from *computers missing security updates*, then you need to design a subsearch that first identifies that *computers missing security updates* before it finds events belonging to those hosts.</span></span>

<span data-ttu-id="f0a89-370">Par conséquent, vous pouvez définir les *ordinateurs ayant actuellement des mises à jour de sécurité obligatoires manquantes* avec la requête suivante :</span><span class="sxs-lookup"><span data-stu-id="f0a89-370">So, you could express *computers currently missing required security updates* with the following query:</span></span>

```
Type:Update UpdateState=Needed Optional=false Classification="Security Updates" TimeGenerated>NOW-24HOURS | measure count() by Computer
```    

![Exemple de recherche avec l’opérateur IN](./media/log-analytics-log-searches/oms-search-in01-revised.png)

<span data-ttu-id="f0a89-372">Une fois la liste en votre possession, vous pouvez utiliser la recherche comme recherche interne pour alimenter la liste des ordinateurs dans une recherche externe (principale) qui recherchera les événements correspondant à ces ordinateurs.</span><span class="sxs-lookup"><span data-stu-id="f0a89-372">Once you have the list, you can use the search as an inner search to feed the list of computers into an outer (primary) search that will look for events for those computers.</span></span> <span data-ttu-id="f0a89-373">Pour cela, incluez la recherche interne dans des accolades et indiquez ses résultats en tant que valeurs possibles pour un filtre/champ dans la recherche externe à l’aide de l’opérateur IN.</span><span class="sxs-lookup"><span data-stu-id="f0a89-373">You do this by enclosing the inner search in braces and feeding its results as possible values for a filter/field in the outer search using the IN operator.</span></span> <span data-ttu-id="f0a89-374">La requête se présente comme suit :</span><span class="sxs-lookup"><span data-stu-id="f0a89-374">The query would resemble:</span></span>

```
Type=Event Computer IN {Type:Update UpdateState=Needed Optional=false Classification="Security Updates" TimeGenerated>NOW-24HOURS | measure count() by Computer}
```
![Exemple de recherche avec l’opérateur IN](./media/log-analytics-log-searches/oms-search-in02-revised.png)

<span data-ttu-id="f0a89-376">Notez également le filtre de temps utilisé dans la recherche interne, car l’évaluation des mises à jour du système prend un instantané de tous les ordinateurs toutes les 24 heures.</span><span class="sxs-lookup"><span data-stu-id="f0a89-376">Also notice the time filter used in the inner search because the System Update Assessment takes a snapshot of all computers every 24 hours.</span></span> <span data-ttu-id="f0a89-377">Vous pouvez rendre la requête interne plus légère et plus précise en recherchant uniquement une journée.</span><span class="sxs-lookup"><span data-stu-id="f0a89-377">You can make the inner query more lightweight and precise by only searching for a day.</span></span> <span data-ttu-id="f0a89-378">La recherche externe utilise pour sa part la sélection de temps de l’interface utilisateur, en récupérant les événements des 7 derniers jours.</span><span class="sxs-lookup"><span data-stu-id="f0a89-378">The outer search instead uses the time selection in the user interface, retrieving events from the last 7 days.</span></span> <span data-ttu-id="f0a89-379">Consultez la page [Opérateurs booléens](#boolean-operators) pour plus d’informations sur les opérateurs de temps.</span><span class="sxs-lookup"><span data-stu-id="f0a89-379">See [Boolean operators](#boolean-operators) for more information about time operators.</span></span>

<span data-ttu-id="f0a89-380">Étant donné que vous utilisez uniquement les résultats de la recherche interne comme valeurs de filtre pour la recherche externe, vous pouvez toujours appliquer des commandes à la recherche externe.</span><span class="sxs-lookup"><span data-stu-id="f0a89-380">Because you really only use the results of the inner search as a filter value for the outer one, you can still apply commands in the outer search.</span></span> <span data-ttu-id="f0a89-381">Par exemple, vous pouvez toujours regrouper les événements ci-dessus avec une autre commande measure :</span><span class="sxs-lookup"><span data-stu-id="f0a89-381">For example, you can still group the above events with another measure command:</span></span>

```
Type=Event Computer IN {Type:Update UpdateState=Needed Optional=false Classification="Security Updates" TimeGenerated>NOW-24HOURS | measure count() by Computer} | measure count() by Source
```

![Exemple de recherche avec l’opérateur IN](./media/log-analytics-log-searches/oms-search-in03-revised.png)

<span data-ttu-id="f0a89-383">En règle générale, vous souhaitez que la requête interne s’exécute rapidement, car elle nécessite des délais d’attente côté service dans Log Analytics, et qu’elle renvoie un nombre de résultats limité.</span><span class="sxs-lookup"><span data-stu-id="f0a89-383">Generally, you want your inner query to execute quickly because Log Analytics has service-side timeouts for it and also to return a small amount of results.</span></span> <span data-ttu-id="f0a89-384">Si la requête interne renvoie trop de résultats, la liste des résultats est tronquée, ce qui peut provoquer un renvoi de résultats incorrects de la part de la recherche externe.</span><span class="sxs-lookup"><span data-stu-id="f0a89-384">If the inner query returns more results, the result list gets truncated, which could potentially cause the outer search to return incorrect results.</span></span>

<span data-ttu-id="f0a89-385">Une autre règle est que la recherche interne doit actuellement fournir des résultats *agrégés* .</span><span class="sxs-lookup"><span data-stu-id="f0a89-385">Another rule is that the inner search currently needs to provide *aggregated* results.</span></span> <span data-ttu-id="f0a89-386">En d’autres termes, elle doit contenir une commande *measure* ; vous ne pouvez pour le moment pas alimenter les résultats bruts dans une recherche externe.</span><span class="sxs-lookup"><span data-stu-id="f0a89-386">In other words, it must contain a *measure* command; you cannot currently feed raw results into an outer search.</span></span>

<span data-ttu-id="f0a89-387">En outre, il ne peut y avoir qu’un seul opérateur IN et il doit être le dernier filtre de la requête.</span><span class="sxs-lookup"><span data-stu-id="f0a89-387">Also, there can be only one IN operator and it must be the last filter in the query.</span></span> <span data-ttu-id="f0a89-388">Il est impossible de relier plusieurs opérateurs IN par un opérateur OR, dans la mesure où cela empêche l’exécution de plusieurs sous-recherches : il est important de noter qu’une seule sous-recherche/recherche interne est possible pour chaque recherche externe.</span><span class="sxs-lookup"><span data-stu-id="f0a89-388">Multiple IN operators cannot be OR’d – this essentially prevents running multiple subsearches: the important point is that only one sub/inner search is possible for each outer search.</span></span>

<span data-ttu-id="f0a89-389">Malgré ces limites, l’opérateur IN permet de nombreux types de recherches corrélées et vous permet de définir des éléments similaires aux groupes tels que les ordinateurs, les utilisateurs ou les fichiers, quels que soient les champs contenus dans vos données.</span><span class="sxs-lookup"><span data-stu-id="f0a89-389">Even with these limits, IN enables many kinds of correlated searches, and allows you to define something similar to groups such as computers, users, or files – whatever the fields in your data contain.</span></span> <span data-ttu-id="f0a89-390">Voici des exemples supplémentaires :</span><span class="sxs-lookup"><span data-stu-id="f0a89-390">Here are more examples:</span></span>

<span data-ttu-id="f0a89-391">**Toutes les mises à jour manquantes sur des ordinateurs sur lesquels le paramètre de mise à jour automatique est désactivé**</span><span class="sxs-lookup"><span data-stu-id="f0a89-391">**All updates missing from computers where Automatic Update setting is disabled**</span></span>

```
Type=Update UpdateState=Needed Optional=false Computer IN {Type=UpdateSummary WindowsUpdateSetting=Manual | measure count() by Computer} | measure count() by KBID
```

<span data-ttu-id="f0a89-392">**Tous les événements d’erreur sur des ordinateurs exécutant SQL Server (où l’évaluation de SQL a été exécutée)**</span><span class="sxs-lookup"><span data-stu-id="f0a89-392">**All error events from computers running SQL Server (=where SQL Assessment has run)**</span></span>

```
Type=Event EventLevelName=error Computer IN {Type=SQLAssessmentRecommendation | measure count() by Computer}
```

<span data-ttu-id="f0a89-393">**Tous les événements de sécurité des ordinateurs qui sont des contrôleurs de domaine (où l’évaluation d’Active Directory a été exécutée)**</span><span class="sxs-lookup"><span data-stu-id="f0a89-393">**All security events from computers that are Domain Controllers (=where AD Assessment has run)**</span></span>

```
Type=SecurityEvent Computer IN { Type=ADAssessmentRecommendation | measure count() by Computer }
```

<span data-ttu-id="f0a89-394">**Quels autres comptes ont ouvert une session sur les ordinateurs auxquels le compte BACONLAND\jochan s’est connecté ?**</span><span class="sxs-lookup"><span data-stu-id="f0a89-394">**Which other accounts have logged on to the same computers where account BACONLAND\jochan has logged on?**</span></span>

```
Type=SecurityEvent EventID=4624   Account!="BACONLAND\\jochan" Computer IN { Type=SecurityEvent EventID=4624   Account="BACONLAND\\jochan" | measure count() by Computer } | measure count() by Account
```

## <a name="use-the-distinct-command"></a><span data-ttu-id="f0a89-395">Utilisation de la commande distinct</span><span class="sxs-lookup"><span data-stu-id="f0a89-395">Use the distinct command</span></span>
<span data-ttu-id="f0a89-396">Comme son nom l’indique, cette commande fournit une liste de valeurs distinctes pour un champ.</span><span class="sxs-lookup"><span data-stu-id="f0a89-396">As the name suggests, this command provides a list of distinct values for a field.</span></span> <span data-ttu-id="f0a89-397">Son utilisation est étonnamment simple mais cette commande s’avère très utile.</span><span class="sxs-lookup"><span data-stu-id="f0a89-397">It's surprisingly simple but quite useful.</span></span> <span data-ttu-id="f0a89-398">Vous pouvez obtenir le même résultat avec la commande measure count(), comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="f0a89-398">The same could be achieved with measure count() command as well, as shown below.</span></span>

```
Type=Event | Measure count() by Computer
```

![Exemple de commande de recherche DISTINCT](./media/log-analytics-log-searches/oms-search-distinct01-revised.png)

<span data-ttu-id="f0a89-400">Toutefois, si vous souhaitez simplement obtenir une liste de valeurs distinctes sans le nombre de documents qui ont ces valeurs, la commande DISTINCT vous permet de bénéficier d’un résultat plus clair et plus facile à lire, ainsi que d’une syntaxe plus courte, comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="f0a89-400">However, if all you're interested in is just a list of distinct values and not the count of documents that have that values, then DISTINCT can provide cleaner and easier to read output, and shorter syntax, as shown below.</span></span>

```
Type=Event | Distinct Computer
```
![Exemple de commande de recherche DISTINCT](./media/log-analytics-log-searches/oms-search-distinct02-revised.png)

## <a name="use-the-countdistinct-function-with-the-measure-command"></a><span data-ttu-id="f0a89-402">Utilisation de la fonction countdistinct avec la commande measure</span><span class="sxs-lookup"><span data-stu-id="f0a89-402">Use the countdistinct function with the measure command</span></span>
<span data-ttu-id="f0a89-403">La fonction countdistinct compte le nombre de valeurs distinctes dans chaque groupe.</span><span class="sxs-lookup"><span data-stu-id="f0a89-403">The countdistinct function counts the number of distinct values within each group.</span></span> <span data-ttu-id="f0a89-404">Par exemple, elle peut servir à compter le nombre d’ordinateurs uniques correspondant à chaque Type :</span><span class="sxs-lookup"><span data-stu-id="f0a89-404">For example, it could be used to count the number of unique computers reporting for each Type:</span></span>

```
* | measure countdistinct(Computer) by Type
```

![OMS-countdistinct](./media/log-analytics-log-searches/oms-countdistinct.png)

## <a name="use-the-measure-interval-command"></a><span data-ttu-id="f0a89-406">Utilisation de la commande measure interval</span><span class="sxs-lookup"><span data-stu-id="f0a89-406">Use the measure interval command</span></span>
<span data-ttu-id="f0a89-407">Grâce à la récupération des données de performance en quasi-temps réel, vous pouvez récupérer et visualiser des compteurs de performance dans Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="f0a89-407">With near real-time performance data collection, you can collect and visualize any performance counter in Log Analytics.</span></span> <span data-ttu-id="f0a89-408">En saisissant simplement la requête **Type:Perf** , vous obtiendrez des milliers de graphiques de mesure basés sur le nombre de compteurs et de serveurs de votre environnement Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="f0a89-408">Simply entering the query **Type:Perf** will return thousands of metric graphs based on the number of counters and servers in your Log Analytics environment.</span></span> <span data-ttu-id="f0a89-409">Grâce à l’agrégation des mesures à la demande, vous pouvez consulter les mesures globales dans votre environnement à un niveau élevé, et analyser en profondeur des données plus granulaires lorsque c’est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="f0a89-409">With on-demand metric aggregation, you can look at the overall metrics in your environment at a high level, and deep dive into more granular data as you need to.</span></span>

<span data-ttu-id="f0a89-410">Supposons que vous souhaitiez connaître l’utilisation moyenne du processeur sur tous vos ordinateurs.</span><span class="sxs-lookup"><span data-stu-id="f0a89-410">Let’s say that you want to know what is the average CPU across all your computers.</span></span> <span data-ttu-id="f0a89-411">Examiner l’utilisation moyenne du processeur pour chaque ordinateur peut ne pas être représentatif car les résultats risquent d’être lissés.</span><span class="sxs-lookup"><span data-stu-id="f0a89-411">Looking at the average CPU for every computer might not be helpful because results may get smoothed out.</span></span> <span data-ttu-id="f0a89-412">Pour une analyse plus détaillée, vous pouvez regrouper vos résultats dans des segments temporels plus courts, puis analysez une série chronologique dans différentes dimensions.</span><span class="sxs-lookup"><span data-stu-id="f0a89-412">To look into more details, you can aggregate your result in a smaller time window chunks, and look into a time series across different dimensions.</span></span> <span data-ttu-id="f0a89-413">Par exemple, vous pouvez effectuer la moyenne horaire de l’utilisation du processeur sur tous vos ordinateurs comme suit :</span><span class="sxs-lookup"><span data-stu-id="f0a89-413">For example, you can perform the hourly average of CPU usage across all your computers as follows:</span></span>

```
Type:Perf CounterName="% Processor Time" InstanceName="_Total" | measure avg(CounterValue) by Computer Interval 1HOUR
```

![intervalle moyen de mesure](./media/log-analytics-log-searches/oms-measure-avg-interval.png)

<span data-ttu-id="f0a89-415">Par défaut, ces résultats s’affichent dans un graphique interactif en courbes contenant plusieurs séries.</span><span class="sxs-lookup"><span data-stu-id="f0a89-415">By default these results will be displayed in a multi-series interactive line chart.</span></span>  <span data-ttu-id="f0a89-416">Ce graphique prend en charge le basculement entre séries (avec la remise à l’échelle de l’axe y), le zoom et le survol.</span><span class="sxs-lookup"><span data-stu-id="f0a89-416">This chart supports series toggling (with y-axis rescaling), zooming, and hovering.</span></span>  <span data-ttu-id="f0a89-417">L’option d’affichage de tableau reste disponible pour l’affichage des données brutes si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="f0a89-417">The table display option is still available for viewing the raw data if necessary.</span></span>

<span data-ttu-id="f0a89-418">Vous pouvez également effectuer des regroupements sur d’autres champs.</span><span class="sxs-lookup"><span data-stu-id="f0a89-418">You can also group by other fields.</span></span> <span data-ttu-id="f0a89-419">Dans cet exemple, j’examine tous les compteurs en % pour un ordinateur spécifique, et je souhaite connaître le 70e centile horaire de chaque compteur :</span><span class="sxs-lookup"><span data-stu-id="f0a89-419">In this example, I am looking at all the % counters for one specific computer, and I want to know what is the hourly 70 percentiles of every counter:</span></span>

```
Type:Perf Computer=beefpatty4 CounterName=%* InstanceName=_Total | measure percentile70(CounterValue) by CounterName Interval 1HOUR
```
<span data-ttu-id="f0a89-420">Il est à noter que ces requêtes ne sont pas limitées aux compteurs de performance.</span><span class="sxs-lookup"><span data-stu-id="f0a89-420">One thing to note is that these queries are not limited to performance counters.</span></span> <span data-ttu-id="f0a89-421">Vous pouvez les appliquer à toute mesure.</span><span class="sxs-lookup"><span data-stu-id="f0a89-421">You can apply them to any metric.</span></span> <span data-ttu-id="f0a89-422">Dans cet exemple, j’examine les journaux IIS W3C.</span><span class="sxs-lookup"><span data-stu-id="f0a89-422">In this example, I’m looking at W3C IIS logs.</span></span> <span data-ttu-id="f0a89-423">Je voudrais savoir quel est le temps maximal nécessaire, sur un intervalle de 5 minutes, pour traiter chaque demande :</span><span class="sxs-lookup"><span data-stu-id="f0a89-423">I want to know what is the maximum time it takes over a 5-minute interval for processing each request:</span></span>

```
Type:W3CIISLog | measure max(TimeTaken) by csMethod Interval 5MINUTES
```

### <a name="use-multiple-aggregates-in-one-query"></a><span data-ttu-id="f0a89-424">Utilisation de plusieurs agrégats dans une même requête</span><span class="sxs-lookup"><span data-stu-id="f0a89-424">Use multiple aggregates in one query</span></span>
<span data-ttu-id="f0a89-425">Vous pouvez spécifier plusieurs clauses d’agrégation dans une commande measure.</span><span class="sxs-lookup"><span data-stu-id="f0a89-425">You can specify multiple aggregate clauses in a measure command.</span></span>  <span data-ttu-id="f0a89-426">Un alias indépendant peut être attribué à chacune d’entre elles.</span><span class="sxs-lookup"><span data-stu-id="f0a89-426">Each one can be aliased independently.</span></span>  <span data-ttu-id="f0a89-427">Si aucun alias n’est donné, le nom du champ résultant correspondra à la fonction d’agrégation utilisée (par exemple, « avg(CounterValue) » pour avg(CounterValue)).</span><span class="sxs-lookup"><span data-stu-id="f0a89-427">If it is not given an alias the resulting field name will be the aggregate function that was used (i.e. "avg(CounterValue)" for avg(CounterValue)).</span></span>

 ```
Type=WireData | measure avg(ReceivedBytes), avg(SentBytes) by Direction interval 1hour
```
![OMS-multiaggregates1](./media/log-analytics-log-searches/oms-multiaggregates1.png)

<span data-ttu-id="f0a89-429">Voici un autre exemple :</span><span class="sxs-lookup"><span data-stu-id="f0a89-429">Here is another example:</span></span>

 ```
* | measure countdistinct(Computer) as Computers, count() as TotalRecords by Type
```


## <a name="next-steps"></a><span data-ttu-id="f0a89-430">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f0a89-430">Next steps</span></span>
<span data-ttu-id="f0a89-431">Pour plus d’informations sur les recherches de journal, consultez les ressources suivantes :</span><span class="sxs-lookup"><span data-stu-id="f0a89-431">For additional information about log searches, see:</span></span>

* <span data-ttu-id="f0a89-432">Utilisez [Champs personnalisés dans Log Analytics](log-analytics-custom-fields.md) pour étendre les recherches de journal.</span><span class="sxs-lookup"><span data-stu-id="f0a89-432">Use [Custom fields in Log Analytics](log-analytics-custom-fields.md) to extend log searches.</span></span>
* <span data-ttu-id="f0a89-433">Pour connaître tous les champs de recherche et facettes disponibles dans Log Analytics, consultez les [informations de référence sur la recherche de journal avec Log Analytics](log-analytics-search-reference.md) .</span><span class="sxs-lookup"><span data-stu-id="f0a89-433">Review the [Log Analytics log search reference](log-analytics-search-reference.md) to view all of the search fields and facets available in Log Analytics.</span></span>
