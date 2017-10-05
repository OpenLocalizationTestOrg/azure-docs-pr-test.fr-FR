---
title: Utilisation du portail Recherche dans les journaux dans Azure Log Analytics | Microsoft Docs
description: "Cet article contient un didacticiel qui explique comment créer des recherches dans les journaux et analyser les données stockées dans votre espace de travail Log Analytics à l’aide du portail Recherche dans les journaux.  Le didacticiel comprend des requêtes simples qui retournent différents types de données et une description des résultats des analyses."
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/23/2017
ms.author: bwren
ms.openlocfilehash: 6fc556ceb34cde26d5f3789a2397cdaa34b0b84d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="create-log-searches-in-azure-log-analytics-using-the-log-search-portal"></a><span data-ttu-id="bbd46-104">Créer des recherches dans les journaux dans Azure Log Analytics à l’aide du portail Recherche dans les journaux</span><span class="sxs-lookup"><span data-stu-id="bbd46-104">Create log searches in Azure Log Analytics using the Log Search portal</span></span>

> [!NOTE]
> <span data-ttu-id="bbd46-105">Cet article décrit le portail Recherche dans les journaux dans Azure Log Analytics avec le nouveau langage de requête.</span><span class="sxs-lookup"><span data-stu-id="bbd46-105">This article describes the Log Search portal in Azure Log Analytics using the new query language.</span></span>  <span data-ttu-id="bbd46-106">Pour en savoir plus sur le nouveau langage et connaître la procédure de mise à niveau de votre espace de travail, consultez [Mettre à niveau votre espace de travail Azure Log Analytics avec la nouvelle recherche dans les journaux](log-analytics-log-search-upgrade.md).</span><span class="sxs-lookup"><span data-stu-id="bbd46-106">You can learn more about the new language and get the procedure to upgrade your workspace at [Upgrade your Azure Log Analytics workspace to new log search](log-analytics-log-search-upgrade.md).</span></span>  
>
> <span data-ttu-id="bbd46-107">Si votre espace de travail n’a pas été mis à niveau avec le nouveau langage de requête, consultez [Rechercher des données avec les recherches dans les journaux dans Log Analytics](log-analytics-log-searches.md) pour plus d’informations sur la version actuelle du portail Recherche dans les journaux.</span><span class="sxs-lookup"><span data-stu-id="bbd46-107">If your workspace hasn't been upgraded to the new query language, you should refer to [Find data using log searches in Log Analytics](log-analytics-log-searches.md) for information on the current version of the Log Search portal.</span></span>

<span data-ttu-id="bbd46-108">Cet article contient un didacticiel qui explique comment créer des recherches dans les journaux et analyser les données stockées dans votre espace de travail Log Analytics à l’aide du portail Recherche dans les journaux.</span><span class="sxs-lookup"><span data-stu-id="bbd46-108">This article includes a tutorial that describes how to create log searches and analyze data stored in your Log Analytics workspace using the Log Search portal.</span></span>  <span data-ttu-id="bbd46-109">Le didacticiel comprend des requêtes simples qui retournent différents types de données et une description des résultats des analyses.</span><span class="sxs-lookup"><span data-stu-id="bbd46-109">The tutorial includes running some simple queries to return different types of data and analyzing results.</span></span>  <span data-ttu-id="bbd46-110">Il est axé sur les fonctionnalités du portail Recherche dans les journaux qui permettent de modifier la requête, plutôt que de la modifier directement.</span><span class="sxs-lookup"><span data-stu-id="bbd46-110">It focuses on features in the Log Search portal for modifying the query rather than modifying it directly.</span></span>  <span data-ttu-id="bbd46-111">Pour plus d’informations sur la modification directe de la requête, consultez les [informations de référence sur le langage de requête](https://go.microsoft.com/fwlink/?linkid=856079).</span><span class="sxs-lookup"><span data-stu-id="bbd46-111">For details on directly editing the query, see the [Query Language reference](https://go.microsoft.com/fwlink/?linkid=856079).</span></span>

<span data-ttu-id="bbd46-112">Pour créer des recherches dans le portail Advanced Analytics plutôt que dans le portail Recherche dans les journaux, consultez [Getting Started with the Analytics Portal](https://go.microsoft.com/fwlink/?linkid=856587) (Bien démarrer avec le portail Analytics).</span><span class="sxs-lookup"><span data-stu-id="bbd46-112">To create searches in the Advanced Analytics portal instead of the Log Search portal, see [Getting Started with the Analytics Portal](https://go.microsoft.com/fwlink/?linkid=856587).</span></span>  <span data-ttu-id="bbd46-113">Les deux portails utilisent le même langage de requête pour accéder aux mêmes données dans l’espace de travail Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="bbd46-113">Both portals use the same query language to access the same data in the Log Analytics workspace.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bbd46-114">Prérequis</span><span class="sxs-lookup"><span data-stu-id="bbd46-114">Prerequisites</span></span>
<span data-ttu-id="bbd46-115">Ce didacticiel part du principe que vous disposez déjà d’un espace de travail Log Analytics avec au moins une source connectée qui génère des données pour les requêtes à analyser.</span><span class="sxs-lookup"><span data-stu-id="bbd46-115">This tutorial assumes that you already have a Log Analytics workspace with at least one connected source that generates data for the queries to analyze.</span></span>  

- <span data-ttu-id="bbd46-116">Si vous n’avez pas d’espace de travail, vous pouvez en créer un gratuitement à l’aide de la procédure décrite dans [Prise en main d’un espace de travail Log Analytics](log-analytics-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="bbd46-116">If you don't have a workspace, you can create a free one using the procedure at [Get started with a Log Analytics workspace](log-analytics-get-started.md).</span></span>
- <span data-ttu-id="bbd46-117">Connectez au moins un [agent Windows](log-analytics-windows-agents.md) ou un [agent Linux](log-analytics-linux-agents.md) à l’espace de travail.</span><span class="sxs-lookup"><span data-stu-id="bbd46-117">Connect least one [Windows agent](log-analytics-windows-agents.md) or one [Linux agent](log-analytics-linux-agents.md) to the workspace.</span></span>  

## <a name="open-the-log-search-portal"></a><span data-ttu-id="bbd46-118">Ouvrir le portail Recherche dans les journaux</span><span class="sxs-lookup"><span data-stu-id="bbd46-118">Open the Log Search portal</span></span>
<span data-ttu-id="bbd46-119">Commencez par ouvrir le portail Recherche dans les journaux.</span><span class="sxs-lookup"><span data-stu-id="bbd46-119">Start by opening the Log Search portal.</span></span>  <span data-ttu-id="bbd46-120">Vous pouvez y accéder dans le portail Azure ou le portail OMS.</span><span class="sxs-lookup"><span data-stu-id="bbd46-120">You can access it in either the Azure portal or the OMS portal.</span></span>

1. <span data-ttu-id="bbd46-121">Ouvrez le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="bbd46-121">Open the Azure portal.</span></span>
2. <span data-ttu-id="bbd46-122">Accédez à Log Analytics et sélectionnez votre espace de travail.</span><span class="sxs-lookup"><span data-stu-id="bbd46-122">Navigate to Log Analytics and select your workspace.</span></span>
3. <span data-ttu-id="bbd46-123">Sélectionnez **Recherche dans les journaux** pour rester dans le portail Azure ou lancez le portail OMS en sélectionnant **Portail OMS** puis en cliquant sur le bouton Recherche dans les journaux.</span><span class="sxs-lookup"><span data-stu-id="bbd46-123">Either select **Log Search** to stay in the Azure portal or launch the OMS portal by selecting **OMS Portal** and then clicking the Log Search button.</span></span>

![Bouton Recherche dans les journaux](media/log-analytics-log-search-log-search-portal/log-search-button.png)

## <a name="create-a-simple-search"></a><span data-ttu-id="bbd46-125">Créer une recherche simple</span><span class="sxs-lookup"><span data-stu-id="bbd46-125">Create a simple search</span></span>
<span data-ttu-id="bbd46-126">Le moyen le plus rapide de récupérer des données à utiliser consiste à faire appel à une requête simple qui retourne tous les enregistrements d’une table.</span><span class="sxs-lookup"><span data-stu-id="bbd46-126">The quickest way to retrieve some data to work with is a simple query that returns all records in table.</span></span>  <span data-ttu-id="bbd46-127">Si vous avez des clients Windows ou Linux connectés à votre espace de travail, vous aurez des données dans la table Event (Windows) ou Syslog (Linux).</span><span class="sxs-lookup"><span data-stu-id="bbd46-127">If you have any Windows or Linux clients connected to your workspace, then you'll have data in either the Event (Windows) or Syslog (Linux) table.</span></span>

<span data-ttu-id="bbd46-128">Tapez l’une des requêtes suivantes dans la zone de recherche, puis cliquez sur le bouton de recherche.</span><span class="sxs-lookup"><span data-stu-id="bbd46-128">Type one the following queries in the search box and click the search button.</span></span>  

```
Event
```
```
Syslog
```

<span data-ttu-id="bbd46-129">Les données sont retournées dans la vue Liste par défaut, et vous pouvez voir le nombre total d’enregistrements retournés.</span><span class="sxs-lookup"><span data-stu-id="bbd46-129">Data is returned in the default list view, and you can see how many total records were returned.</span></span>

![Requête simple](media/log-analytics-log-search-log-search-portal/log-search-portal-01.png)

<span data-ttu-id="bbd46-131">Seules les premières propriétés de chaque enregistrement sont affichées.</span><span class="sxs-lookup"><span data-stu-id="bbd46-131">Only the first few properties of each record are displayed.</span></span>  <span data-ttu-id="bbd46-132">Cliquez sur **afficher plus** pour afficher toutes les propriétés d’un enregistrement.</span><span class="sxs-lookup"><span data-stu-id="bbd46-132">Click **show more** to display all properties for a particular record.</span></span>

![Détails des enregistrements](media/log-analytics-log-search-log-search-portal/log-search-portal-02.png)

## <a name="set-the-time-scope"></a><span data-ttu-id="bbd46-134">Définir la période</span><span class="sxs-lookup"><span data-stu-id="bbd46-134">Set the time scope</span></span>
<span data-ttu-id="bbd46-135">Chaque enregistrement recueilli par Log Analytics a une propriété **TimeGenerated** qui contient la date et l’heure de création de l’enregistrement.</span><span class="sxs-lookup"><span data-stu-id="bbd46-135">Every record collected by Log Analytics has a **TimeGenerated** property that contains the date and time that the record was created.</span></span>  <span data-ttu-id="bbd46-136">Une requête dans le portail Recherche dans les journaux retourne uniquement les enregistrements dont la propriété **TimeGenerated** se trouve dans la période affichée sur le côté gauche de l’écran.</span><span class="sxs-lookup"><span data-stu-id="bbd46-136">A query in the Log Search portal only returns records with a **TimeGenerated** within the time scope that's displayed on the left side of the screen.</span></span>  

<span data-ttu-id="bbd46-137">Vous pouvez changer le filtre temporel en sélectionnant la liste déroulante ou en modifiant le curseur.</span><span class="sxs-lookup"><span data-stu-id="bbd46-137">You can change the time filter either by selecting the dropdown or by modifying the slider.</span></span>  <span data-ttu-id="bbd46-138">Le curseur affiche un graphique à barres qui indique le nombre relatif d’enregistrements pour chaque segment de temps dans la plage.</span><span class="sxs-lookup"><span data-stu-id="bbd46-138">The slider displays a bar graph that shows the relative number of records for each time segment within the range.</span></span>  <span data-ttu-id="bbd46-139">Ce segment varie en fonction de la plage.</span><span class="sxs-lookup"><span data-stu-id="bbd46-139">This segment will vary depending on the range.</span></span>

<span data-ttu-id="bbd46-140">La période par défaut est **1 jour**.</span><span class="sxs-lookup"><span data-stu-id="bbd46-140">The default time scope is **1 day**.</span></span>  <span data-ttu-id="bbd46-141">Remplacez cette valeur par **7 jours**. Le nombre total d’enregistrements devrait alors augmenter.</span><span class="sxs-lookup"><span data-stu-id="bbd46-141">Change this value to **7 days**, and the total number of records should increase.</span></span>

![Période](media/log-analytics-log-search-log-search-portal/log-search-portal-03.png)

## <a name="filter-results-of-the-query"></a><span data-ttu-id="bbd46-143">Filtrer les résultats de la requête</span><span class="sxs-lookup"><span data-stu-id="bbd46-143">Filter results of the query</span></span>
<span data-ttu-id="bbd46-144">Sur le côté gauche de l’écran se trouve le volet de filtre, qui vous permet d’ajouter un filtrage à la requête sans la modifier directement.</span><span class="sxs-lookup"><span data-stu-id="bbd46-144">On the left side of the screen is the filter pane which allows you to add filtering to the query without modifying it directly.</span></span>  <span data-ttu-id="bbd46-145">Plusieurs propriétés des enregistrements retournés sont affichées, avec leurs dix premières valeurs et le nombre d’enregistrements.</span><span class="sxs-lookup"><span data-stu-id="bbd46-145">Several properties of the records returned are displayed with their top ten values with their record count.</span></span>

<span data-ttu-id="bbd46-146">Si vous travaillez avec **Event**, cochez la case en regard de **Error** sous **EVENTLEVELNAME**.</span><span class="sxs-lookup"><span data-stu-id="bbd46-146">If you're working with **Event**, select the checkbox next to **Error** under **EVENTLEVELNAME**.</span></span>   <span data-ttu-id="bbd46-147">Si vous travaillez avec **Syslog**, cochez la case en regard de **err** sous **SEVERITYLEVEL**.</span><span class="sxs-lookup"><span data-stu-id="bbd46-147">If you're working with **Syslog**, select the checkbox next to **err** under **SEVERITYLEVEL**.</span></span>  <span data-ttu-id="bbd46-148">Cela remplace la requête par l’une des suivantes, afin de limiter les résultats aux événements d’erreur.</span><span class="sxs-lookup"><span data-stu-id="bbd46-148">This changes the query to one of the following to limit the results to error events.</span></span>

```
Event | where (EventLevelName == "Error")
```
```
Syslog | where (SeverityLevel == "err")
```

![Filtre](media/log-analytics-log-search-log-search-portal/log-search-portal-04.png)

<span data-ttu-id="bbd46-150">Ajoutez des propriétés au volet de filtre en sélectionnant **Ajouter aux filtres** dans le menu de propriété sur l’un des enregistrements.</span><span class="sxs-lookup"><span data-stu-id="bbd46-150">Add properties to the filter pane by selecting **Add to filters** from the property menu on one of the records.</span></span>

![Menu Ajouter au filtre](media/log-analytics-log-search-log-search-portal/log-search-portal-02a.png)

<span data-ttu-id="bbd46-152">Vous pouvez définir le même filtre en sélectionnant **Filtrer** dans le menu de propriété d’un enregistrement avec la valeur que vous souhaitez filtrer.</span><span class="sxs-lookup"><span data-stu-id="bbd46-152">You can set the same filter by selecting **Filter** from the property menu for a record with the value you want to filter.</span></span>  

<span data-ttu-id="bbd46-153">L’option **Filtrer** est visible uniquement pour les propriétés dont le nom est en bleu.</span><span class="sxs-lookup"><span data-stu-id="bbd46-153">You only have the **Filter** option for properties with their name in blue.</span></span>  <span data-ttu-id="bbd46-154">Il s’agit de champs *dans lesquels une recherche peut être effectuée* et qui sont indexés pour les conditions de recherche.</span><span class="sxs-lookup"><span data-stu-id="bbd46-154">These are *searchable* fields which are indexed for search conditions.</span></span>  <span data-ttu-id="bbd46-155">Les champs en gris sont des champs *dans lesquels une recherche en texte libre peut être effectuée*. Ils ont uniquement l’option **Afficher les références**.</span><span class="sxs-lookup"><span data-stu-id="bbd46-155">Fields in grey are *free text searchable* fields which only have the **Show references** option.</span></span>  <span data-ttu-id="bbd46-156">Cette option retourne les enregistrements qui ont cette valeur dans une propriété quelconque.</span><span class="sxs-lookup"><span data-stu-id="bbd46-156">This option returns records that have that value in any property.</span></span>

![Menu Filtrer](media/log-analytics-log-search-log-search-portal/log-search-portal-01a.png)

<span data-ttu-id="bbd46-158">Vous pouvez regrouper les résultats sur une propriété unique en sélectionnant l’option **Regrouper par** dans le menu d’enregistrement.</span><span class="sxs-lookup"><span data-stu-id="bbd46-158">You can group the results on a single property by selecting the **Group by** option in the record menu.</span></span>  <span data-ttu-id="bbd46-159">Cette opération ajoute un opérateur [summarize](https://docs.loganalytics.io/docs/Language-Reference/Tabular-operators/summarize-operator) à votre requête qui affiche les résultats dans un graphique.</span><span class="sxs-lookup"><span data-stu-id="bbd46-159">This will add a [summarize](https://docs.loganalytics.io/docs/Language-Reference/Tabular-operators/summarize-operator) operator to your query that displays the results in a chart.</span></span>  <span data-ttu-id="bbd46-160">Vous pouvez regrouper sur plusieurs propriétés, mais vous devrez modifier la requête directement.</span><span class="sxs-lookup"><span data-stu-id="bbd46-160">You can group on more than one property, but you would need to edit the query directly.</span></span>  <span data-ttu-id="bbd46-161">Sélectionnez le menu d’enregistrement à côté de la propriété **Computer** et sélectionnez **Regrouper par « Computer »**.</span><span class="sxs-lookup"><span data-stu-id="bbd46-161">Select the record menu next the the **Computer** property and select **Group by 'Computer'**.</span></span>  

![Regrouper par ordinateur](media/log-analytics-log-search-log-search-portal/log-search-portal-10.png)

## <a name="work-with-results"></a><span data-ttu-id="bbd46-163">Utiliser les résultats</span><span class="sxs-lookup"><span data-stu-id="bbd46-163">Work with results</span></span>
<span data-ttu-id="bbd46-164">Le portail Recherche dans les journaux offre un large éventail de fonctionnalités pour utiliser les résultats d’une requête.</span><span class="sxs-lookup"><span data-stu-id="bbd46-164">The Log Search portal has a variety of features for working with the results of a query.</span></span>  <span data-ttu-id="bbd46-165">Vous pouvez trier, filtrer et regrouper les résultats pour analyser les données sans modifier la requête proprement dite.</span><span class="sxs-lookup"><span data-stu-id="bbd46-165">You can sort, filter, and group results to analyze the data without modifying the actual query.</span></span>  <span data-ttu-id="bbd46-166">Les résultats d’une requête ne sont pas triés par défaut.</span><span class="sxs-lookup"><span data-stu-id="bbd46-166">Results of a query are not sorted by default.</span></span>

<span data-ttu-id="bbd46-167">Pour afficher les données sous forme de table qui fournit des options supplémentaires pour le filtrage et le tri, cliquez sur **Table**.</span><span class="sxs-lookup"><span data-stu-id="bbd46-167">To view the data in table form which provides additional options for filtering and sorting, click **Table**.</span></span>  

![Vue Table](media/log-analytics-log-search-log-search-portal/log-search-portal-05.png)

<span data-ttu-id="bbd46-169">Cliquez sur la flèche en regard d’un enregistrement pour afficher les détails de cet enregistrement.</span><span class="sxs-lookup"><span data-stu-id="bbd46-169">Click the arrow by a record to view the details for that record.</span></span>

![Trier les résultats](media/log-analytics-log-search-log-search-portal/log-search-portal-06.png)

<span data-ttu-id="bbd46-171">Pour trier sur un champ, cliquez sur son en-tête de colonne.</span><span class="sxs-lookup"><span data-stu-id="bbd46-171">Sort on any field by clicking on its column header.</span></span>

![Trier les résultats](media/log-analytics-log-search-log-search-portal/log-search-portal-07.png)

<span data-ttu-id="bbd46-173">Pour filtrer les résultats sur une valeur spécifique dans la colonne, cliquez sur le bouton de filtre et spécifiez une condition de filtre.</span><span class="sxs-lookup"><span data-stu-id="bbd46-173">Filter the results on a specific value in the column by clicking the filter button and providing a filter condition.</span></span>

![Filtrer les résultats](media/log-analytics-log-search-log-search-portal/log-search-portal-08.png)

<span data-ttu-id="bbd46-175">Pour regrouper sur une colonne, faites glisser son en-tête en haut des résultats.</span><span class="sxs-lookup"><span data-stu-id="bbd46-175">Group on a column by dragging its column header to the top of the results.</span></span>  <span data-ttu-id="bbd46-176">Vous pouvez regrouper sur plusieurs champs en faisant glisser plusieurs colonnes vers le haut.</span><span class="sxs-lookup"><span data-stu-id="bbd46-176">You can group on multiple fields by dragging multiple columns to the top.</span></span>

![Regrouper les résultats](media/log-analytics-log-search-log-search-portal/log-search-portal-09.png)



## <a name="work-with-performance-data"></a><span data-ttu-id="bbd46-178">Utiliser des données de performances</span><span class="sxs-lookup"><span data-stu-id="bbd46-178">Work with performance data</span></span>
<span data-ttu-id="bbd46-179">Les données de performances pour les agents Windows et Linux sont stockées dans l’espace de travail Log Analytics dans la table **Perf**.</span><span class="sxs-lookup"><span data-stu-id="bbd46-179">Performance data for both Windows and Linux agents is stored in the Log Analytics workspace in the **Perf** table.</span></span>  <span data-ttu-id="bbd46-180">Les enregistrements de performances ressemblent aux autres enregistrements, et nous pouvons écrire une requête simple qui retourne tous les enregistrements de performances, tout comme avec les événements.</span><span class="sxs-lookup"><span data-stu-id="bbd46-180">Performance records look just like any other record, and we can write a simple query that returns all performance records just like with events.</span></span>

```
Perf
```

![Données de performances](media/log-analytics-log-search-log-search-portal/log-search-portal-11.png)

<span data-ttu-id="bbd46-182">Retourner plusieurs millions d’enregistrements pour tous les objets de performances et compteurs n’est cependant pas très utile.</span><span class="sxs-lookup"><span data-stu-id="bbd46-182">Returning millions of records for all performance objects and counters though isn't very useful.</span></span>  <span data-ttu-id="bbd46-183">Vous pouvez appliquer les mêmes méthodes que ci-dessus pour filtrer les données, ou simplement taper la requête suivante directement dans la zone de recherche dans les journaux.</span><span class="sxs-lookup"><span data-stu-id="bbd46-183">You can use the same methods you used above to filter the data or just type the following query directly into the log search box.</span></span>  <span data-ttu-id="bbd46-184">Cela retourne uniquement les enregistrements d’utilisation des processeurs pour les ordinateurs Windows et Linux.</span><span class="sxs-lookup"><span data-stu-id="bbd46-184">This returns only processor utilization records for both Windows and Linux computers.</span></span>

```
Perf | where (ObjectName == "Processor")  | where (CounterName == "% Processor Time")
```

![Utilisation des processeurs](media/log-analytics-log-search-log-search-portal/log-search-portal-12.png)

<span data-ttu-id="bbd46-186">Cela limite les données à un compteur spécifique, mais sous une forme qui n’est encore pas particulièrement utile.</span><span class="sxs-lookup"><span data-stu-id="bbd46-186">This limits the data to a particular counter, but it still doesn't put it in a form that's particularly useful.</span></span>  <span data-ttu-id="bbd46-187">Vous pouvez afficher les données dans un graphique en courbes, mais vous devez d’abord les regrouper par Computer et TimeGenerated.</span><span class="sxs-lookup"><span data-stu-id="bbd46-187">You can display the data in a line chart, but first need to group it by Computer and TimeGenerated.</span></span>  <span data-ttu-id="bbd46-188">Pour regrouper sur plusieurs champs, vous devez modifier la requête directement, comme suit.</span><span class="sxs-lookup"><span data-stu-id="bbd46-188">To group on multiple fields, you need to modify the query directly, so modify the query to the following.</span></span>  <span data-ttu-id="bbd46-189">Cette requête utilise la fonction [avg](https://docs.loganalytics.io/docs/Language-Reference/Aggregation-functions/avg()) sur la propriété **CounterValue** pour calculer la valeur moyenne durant chaque heure.</span><span class="sxs-lookup"><span data-stu-id="bbd46-189">This uses the [avg](https://docs.loganalytics.io/docs/Language-Reference/Aggregation-functions/avg()) function on the **CounterValue** property to calculate the average value over each hour.</span></span>

```
Perf  | where (ObjectName == "Processor")  | where (CounterName == "% Processor Time") | summarize avg(CounterValue) by Computer, TimeGenerated
```

![Graphique de données de performances](media/log-analytics-log-search-log-search-portal/log-search-portal-13.png)

<span data-ttu-id="bbd46-191">Maintenant que les données sont regroupées convenablement, vous pouvez les afficher dans un graphique en ajoutant l’opérateur [render](https://docs.loganalytics.io/docs/Language-Reference/Tabular-operators/render-operator).</span><span class="sxs-lookup"><span data-stu-id="bbd46-191">Now that the data is suitably grouped, you can display it in a visual chart by adding the [render](https://docs.loganalytics.io/docs/Language-Reference/Tabular-operators/render-operator) operator.</span></span>  

```
Perf  | where (ObjectName == "Processor")  | where (CounterName == "% Processor Time") | summarize avg(CounterValue) by Computer, TimeGenerated | render timechart
```

![Graphique en courbes](media/log-analytics-log-search-log-search-portal/log-search-portal-14.png)

## <a name="next-steps"></a><span data-ttu-id="bbd46-193">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="bbd46-193">Next steps</span></span>

- <span data-ttu-id="bbd46-194">Pour en savoir plus sur le langage de requête Log Analytics, consultez [Getting Started with the Analytics Portal](https://go.microsoft.com/fwlink/?linkid=856079) (Bien démarrer avec le portail Analytics).</span><span class="sxs-lookup"><span data-stu-id="bbd46-194">Learn more about the Log Analytics query language at [Getting Started with the Analytics Portal](https://go.microsoft.com/fwlink/?linkid=856079).</span></span>
- <span data-ttu-id="bbd46-195">Suivez un didacticiel à l’aide du [portail Advanced Analytics](https://go.microsoft.com/fwlink/?linkid=856587) pour exécuter les mêmes requêtes et accéder aux mêmes données que le portail Recherche dans les journaux.</span><span class="sxs-lookup"><span data-stu-id="bbd46-195">Walk through a tutorial using the [Advanced Analytics portal](https://go.microsoft.com/fwlink/?linkid=856587) which allows you to run the same queries and access the same data as the Log Search portal.</span></span>
