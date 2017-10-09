---
title: portail de recherche de journal aaaUsing hello dans Analytique de journal Azure | Documents Microsoft
description: "Cet article inclut un didacticiel décrivant comment toocreate recherches de journal et analyser les données stockées dans votre espace de travail Analytique des journaux à l’aide du portail de recherche de journal hello.  didacticiel de Hello inclut en cours d’exécution des requêtes simples tooreturn différents types de données et analyse des résultats."
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
ms.openlocfilehash: 2e6633d548bb508edc0c650d11d2c32fc6ee536c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-log-searches-in-azure-log-analytics-using-hello-log-search-portal"></a><span data-ttu-id="51557-104">Créer des recherches de journal dans Azure Analytique de journal à l’aide du portail de recherche de journal hello</span><span class="sxs-lookup"><span data-stu-id="51557-104">Create log searches in Azure Log Analytics using hello Log Search portal</span></span>

> [!NOTE]
> <span data-ttu-id="51557-105">Cet article décrit le portail de recherche de journal hello dans Azure Analytique de journal à l’aide du nouveau langage de requête hello.</span><span class="sxs-lookup"><span data-stu-id="51557-105">This article describes hello Log Search portal in Azure Log Analytics using hello new query language.</span></span>  <span data-ttu-id="51557-106">Vous pouvez en savoir plus sur le nouveau langage de hello et obtenir hello procédure tooupgrade votre espace de travail à [mise à niveau de votre recherche de journal toonew espace de travail Analytique des journaux Azure](log-analytics-log-search-upgrade.md).</span><span class="sxs-lookup"><span data-stu-id="51557-106">You can learn more about hello new language and get hello procedure tooupgrade your workspace at [Upgrade your Azure Log Analytics workspace toonew log search](log-analytics-log-search-upgrade.md).</span></span>  
>
> <span data-ttu-id="51557-107">Si votre espace de travail n’a pas été mis à niveau toohello nouveau langage de requête, vous devez faire référence trop[trouver des données à l’aide de recherches de journal dans le journal Analytique](log-analytics-log-searches.md) pour plus d’informations sur la version actuelle de hello du portail de recherche de journal hello.</span><span class="sxs-lookup"><span data-stu-id="51557-107">If your workspace hasn't been upgraded toohello new query language, you should refer too[Find data using log searches in Log Analytics](log-analytics-log-searches.md) for information on hello current version of hello Log Search portal.</span></span>

<span data-ttu-id="51557-108">Cet article inclut un didacticiel décrivant comment toocreate recherches de journal et analyser les données stockées dans votre espace de travail Analytique des journaux à l’aide du portail de recherche de journal hello.</span><span class="sxs-lookup"><span data-stu-id="51557-108">This article includes a tutorial that describes how toocreate log searches and analyze data stored in your Log Analytics workspace using hello Log Search portal.</span></span>  <span data-ttu-id="51557-109">didacticiel de Hello inclut en cours d’exécution des requêtes simples tooreturn différents types de données et analyse des résultats.</span><span class="sxs-lookup"><span data-stu-id="51557-109">hello tutorial includes running some simple queries tooreturn different types of data and analyzing results.</span></span>  <span data-ttu-id="51557-110">Il se concentre sur les fonctionnalités dans le portail de recherche de journal hello pour modifier la requête de hello plutôt que de modifier directement.</span><span class="sxs-lookup"><span data-stu-id="51557-110">It focuses on features in hello Log Search portal for modifying hello query rather than modifying it directly.</span></span>  <span data-ttu-id="51557-111">Pour plus d’informations sur la modification directe de requête de hello, consultez hello [référence du langage de requête](https://go.microsoft.com/fwlink/?linkid=856079).</span><span class="sxs-lookup"><span data-stu-id="51557-111">For details on directly editing hello query, see hello [Query Language reference](https://go.microsoft.com/fwlink/?linkid=856079).</span></span>

<span data-ttu-id="51557-112">recherche toocreate dans portail d’Analytique de Advanced hello au lieu du portail de recherche de journal hello, consultez [prise en main de hello Analytique Portal](https://go.microsoft.com/fwlink/?linkid=856587).</span><span class="sxs-lookup"><span data-stu-id="51557-112">toocreate searches in hello Advanced Analytics portal instead of hello Log Search portal, see [Getting Started with hello Analytics Portal](https://go.microsoft.com/fwlink/?linkid=856587).</span></span>  <span data-ttu-id="51557-113">Les deux portails utilisent hello requête même langage tooaccess hello des mêmes données dans l’espace de travail hello Analytique de journal.</span><span class="sxs-lookup"><span data-stu-id="51557-113">Both portals use hello same query language tooaccess hello same data in hello Log Analytics workspace.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="51557-114">Composants requis</span><span class="sxs-lookup"><span data-stu-id="51557-114">Prerequisites</span></span>
<span data-ttu-id="51557-115">Ce didacticiel suppose que vous disposez déjà d’un espace de travail Analytique de journal au moins une source connectée qui génère des données pour hello requêtes tooanalyze.</span><span class="sxs-lookup"><span data-stu-id="51557-115">This tutorial assumes that you already have a Log Analytics workspace with at least one connected source that generates data for hello queries tooanalyze.</span></span>  

- <span data-ttu-id="51557-116">Si vous n’avez pas un espace de travail, vous pouvez créer un gratuitement à l’aide de la procédure hello sur [prise en main avec un espace de travail Analytique de journal](log-analytics-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="51557-116">If you don't have a workspace, you can create a free one using hello procedure at [Get started with a Log Analytics workspace](log-analytics-get-started.md).</span></span>
- <span data-ttu-id="51557-117">Se connecter au moins un [agent Windows](log-analytics-windows-agents.md) ou un [agent Linux](log-analytics-linux-agents.md) toohello espace de travail.</span><span class="sxs-lookup"><span data-stu-id="51557-117">Connect least one [Windows agent](log-analytics-windows-agents.md) or one [Linux agent](log-analytics-linux-agents.md) toohello workspace.</span></span>  

## <a name="open-hello-log-search-portal"></a><span data-ttu-id="51557-118">Portail de recherche de journal hello ouvert</span><span class="sxs-lookup"><span data-stu-id="51557-118">Open hello Log Search portal</span></span>
<span data-ttu-id="51557-119">Commencez par ouvrir le portail de recherche de journal hello.</span><span class="sxs-lookup"><span data-stu-id="51557-119">Start by opening hello Log Search portal.</span></span>  <span data-ttu-id="51557-120">Vous pouvez y accéder dans hello portail Azure ou du portail OMS hello.</span><span class="sxs-lookup"><span data-stu-id="51557-120">You can access it in either hello Azure portal or hello OMS portal.</span></span>

1. <span data-ttu-id="51557-121">Ouvrez hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="51557-121">Open hello Azure portal.</span></span>
2. <span data-ttu-id="51557-122">Accédez tooLog Analytique et sélectionnez votre espace de travail.</span><span class="sxs-lookup"><span data-stu-id="51557-122">Navigate tooLog Analytics and select your workspace.</span></span>
3. <span data-ttu-id="51557-123">Sélectionnez **recherche de journal** toostay Bonjour Azure portal ou lancez hello du portail OMS en sélectionnant **portail OMS** , puis sur le bouton de recherche de journal hello.</span><span class="sxs-lookup"><span data-stu-id="51557-123">Either select **Log Search** toostay in hello Azure portal or launch hello OMS portal by selecting **OMS Portal** and then clicking hello Log Search button.</span></span>

![Bouton Recherche dans les journaux](media/log-analytics-log-search-log-search-portal/log-search-button.png)

## <a name="create-a-simple-search"></a><span data-ttu-id="51557-125">Créer une recherche simple</span><span class="sxs-lookup"><span data-stu-id="51557-125">Create a simple search</span></span>
<span data-ttu-id="51557-126">tooretrieve moyen le plus rapide de Hello toowork de certaines données avec est une requête simple qui retourne tous les enregistrements dans la table.</span><span class="sxs-lookup"><span data-stu-id="51557-126">hello quickest way tooretrieve some data toowork with is a simple query that returns all records in table.</span></span>  <span data-ttu-id="51557-127">Si vous disposez d’un espace de travail Windows ou Linux clients tooyour connecté, puis vous allez ont des données dans hello soit des événements (Windows) ou une table de Syslog (Linux).</span><span class="sxs-lookup"><span data-stu-id="51557-127">If you have any Windows or Linux clients connected tooyour workspace, then you'll have data in either hello Event (Windows) or Syslog (Linux) table.</span></span>

<span data-ttu-id="51557-128">Tapez une Bonjour suite de requêtes dans la zone de recherche hello et cliquez sur le bouton de recherche hello.</span><span class="sxs-lookup"><span data-stu-id="51557-128">Type one hello following queries in hello search box and click hello search button.</span></span>  

```
Event
```
```
Syslog
```

<span data-ttu-id="51557-129">Données sont retournées dans l’affichage de liste par défaut hello, et vous pouvez voir le nombre total d’enregistrements retournés.</span><span class="sxs-lookup"><span data-stu-id="51557-129">Data is returned in hello default list view, and you can see how many total records were returned.</span></span>

![Requête simple](media/log-analytics-log-search-log-search-portal/log-search-portal-01.png)

<span data-ttu-id="51557-131">Uniquement hello premier quelques propriétés de chaque enregistrement sont affichées.</span><span class="sxs-lookup"><span data-stu-id="51557-131">Only hello first few properties of each record are displayed.</span></span>  <span data-ttu-id="51557-132">Cliquez sur **afficher plus** toodisplay toutes les propriétés pour un enregistrement particulier.</span><span class="sxs-lookup"><span data-stu-id="51557-132">Click **show more** toodisplay all properties for a particular record.</span></span>

![Détails des enregistrements](media/log-analytics-log-search-log-search-portal/log-search-portal-02.png)

## <a name="set-hello-time-scope"></a><span data-ttu-id="51557-134">Définir l’étendue de temps hello</span><span class="sxs-lookup"><span data-stu-id="51557-134">Set hello time scope</span></span>
<span data-ttu-id="51557-135">Chaque enregistrement collecté par Analytique de journal a un **TimeGenerated** propriété contenant hello date et heure de cet enregistrement hello a été créé.</span><span class="sxs-lookup"><span data-stu-id="51557-135">Every record collected by Log Analytics has a **TimeGenerated** property that contains hello date and time that hello record was created.</span></span>  <span data-ttu-id="51557-136">Une requête dans le portail de recherche de journal hello retourne uniquement les enregistrements avec un **TimeGenerated** étendue hello temps qui s’affiche sur hello à gauche de l’écran hello.</span><span class="sxs-lookup"><span data-stu-id="51557-136">A query in hello Log Search portal only returns records with a **TimeGenerated** within hello time scope that's displayed on hello left side of hello screen.</span></span>  

<span data-ttu-id="51557-137">Vous pouvez modifier le filtre d’heure hello en sélectionnant la liste déroulante de hello ou en modifiant le curseur de hello.</span><span class="sxs-lookup"><span data-stu-id="51557-137">You can change hello time filter either by selecting hello dropdown or by modifying hello slider.</span></span>  <span data-ttu-id="51557-138">curseur de Hello affiche un graphique à barres qui affiche hello de nombre relatif des enregistrements pour chaque segment de temps au sein de la plage de hello.</span><span class="sxs-lookup"><span data-stu-id="51557-138">hello slider displays a bar graph that shows hello relative number of records for each time segment within hello range.</span></span>  <span data-ttu-id="51557-139">Ce segment varie en fonction de la plage de hello.</span><span class="sxs-lookup"><span data-stu-id="51557-139">This segment will vary depending on hello range.</span></span>

<span data-ttu-id="51557-140">étendue de temps par défaut Hello est **1 jour**.</span><span class="sxs-lookup"><span data-stu-id="51557-140">hello default time scope is **1 day**.</span></span>  <span data-ttu-id="51557-141">Modifiez cette valeur trop**7 jours**, et hello le nombre total d’enregistrements doit augmenter.</span><span class="sxs-lookup"><span data-stu-id="51557-141">Change this value too**7 days**, and hello total number of records should increase.</span></span>

![Période](media/log-analytics-log-search-log-search-portal/log-search-portal-03.png)

## <a name="filter-results-of-hello-query"></a><span data-ttu-id="51557-143">Filtrer les résultats de requête de hello</span><span class="sxs-lookup"><span data-stu-id="51557-143">Filter results of hello query</span></span>
<span data-ttu-id="51557-144">Sur hello à gauche de l’écran hello est le volet de filtre hello qui vous permet de tooadd filtrage toohello requête sans le modifier directement.</span><span class="sxs-lookup"><span data-stu-id="51557-144">On hello left side of hello screen is hello filter pane which allows you tooadd filtering toohello query without modifying it directly.</span></span>  <span data-ttu-id="51557-145">Plusieurs propriétés de hello les enregistrements retournés sont affichées avec leurs dix premières valeurs avec leur nombre d’enregistrements.</span><span class="sxs-lookup"><span data-stu-id="51557-145">Several properties of hello records returned are displayed with their top ten values with their record count.</span></span>

<span data-ttu-id="51557-146">Si vous travaillez avec **événement**, sélectionnez hello case à cocher l’ensuite trop**erreur** sous **valeur EVENTLEVELNAME**.</span><span class="sxs-lookup"><span data-stu-id="51557-146">If you're working with **Event**, select hello checkbox next too**Error** under **EVENTLEVELNAME**.</span></span>   <span data-ttu-id="51557-147">Si vous travaillez avec **Syslog**, sélectionnez hello case à cocher l’ensuite trop**err** sous **SEVERITYLEVEL**.</span><span class="sxs-lookup"><span data-stu-id="51557-147">If you're working with **Syslog**, select hello checkbox next too**err** under **SEVERITYLEVEL**.</span></span>  <span data-ttu-id="51557-148">Cela modifie la requête hello tooone Hello suivant toolimit hello tooerror événements des résultats.</span><span class="sxs-lookup"><span data-stu-id="51557-148">This changes hello query tooone of hello following toolimit hello results tooerror events.</span></span>

```
Event | where (EventLevelName == "Error")
```
```
Syslog | where (SeverityLevel == "err")
```

![Filtrer](media/log-analytics-log-search-log-search-portal/log-search-portal-04.png)

<span data-ttu-id="51557-150">Volet de filtre toohello ajouter propriétés en sélectionnant **ajouter toofilters** à partir du menu de propriété hello sur l’un des enregistrements de hello.</span><span class="sxs-lookup"><span data-stu-id="51557-150">Add properties toohello filter pane by selecting **Add toofilters** from hello property menu on one of hello records.</span></span>

![Toofilter menu Ajouter](media/log-analytics-log-search-log-search-portal/log-search-portal-02a.png)

<span data-ttu-id="51557-152">Vous pouvez définir hello même filtre en sélectionnant **filtre** à partir du menu de propriété hello pour un enregistrement avec la valeur de hello souhaité toofilter.</span><span class="sxs-lookup"><span data-stu-id="51557-152">You can set hello same filter by selecting **Filter** from hello property menu for a record with hello value you want toofilter.</span></span>  

<span data-ttu-id="51557-153">Il vous suffit hello **filtre** option pour les propriétés par leur nom en bleu.</span><span class="sxs-lookup"><span data-stu-id="51557-153">You only have hello **Filter** option for properties with their name in blue.</span></span>  <span data-ttu-id="51557-154">Il s’agit de champs *dans lesquels une recherche peut être effectuée* et qui sont indexés pour les conditions de recherche.</span><span class="sxs-lookup"><span data-stu-id="51557-154">These are *searchable* fields which are indexed for search conditions.</span></span>  <span data-ttu-id="51557-155">Les champs en gris sont *libérer des recherches de texte* les champs qui ont uniquement des hello **afficher les références** option.</span><span class="sxs-lookup"><span data-stu-id="51557-155">Fields in grey are *free text searchable* fields which only have hello **Show references** option.</span></span>  <span data-ttu-id="51557-156">Cette option retourne les enregistrements qui ont cette valeur dans une propriété quelconque.</span><span class="sxs-lookup"><span data-stu-id="51557-156">This option returns records that have that value in any property.</span></span>

![Menu Filtrer](media/log-analytics-log-search-log-search-portal/log-search-portal-01a.png)

<span data-ttu-id="51557-158">Vous pouvez regrouper les résultats de hello sur une seule propriété en sélectionnant hello **regrouper par** option dans le menu d’enregistrement hello.</span><span class="sxs-lookup"><span data-stu-id="51557-158">You can group hello results on a single property by selecting hello **Group by** option in hello record menu.</span></span>  <span data-ttu-id="51557-159">Cette opération ajoute une [résumer](https://docs.loganalytics.io/docs/Language-Reference/Tabular-operators/summarize-operator) requête tooyour opérateur qui affiche les résultats de hello dans un graphique.</span><span class="sxs-lookup"><span data-stu-id="51557-159">This will add a [summarize](https://docs.loganalytics.io/docs/Language-Reference/Tabular-operators/summarize-operator) operator tooyour query that displays hello results in a chart.</span></span>  <span data-ttu-id="51557-160">Vous pouvez regrouper sur plus d’une propriété, mais vous devez alors requête de hello tooedit directement.</span><span class="sxs-lookup"><span data-stu-id="51557-160">You can group on more than one property, but you would need tooedit hello query directly.</span></span>  <span data-ttu-id="51557-161">Sélectionnez Bonjour menu enregistrement suivant hello Bonjour **ordinateur** et sélectionnez **Group by « Computer »**.</span><span class="sxs-lookup"><span data-stu-id="51557-161">Select hello record menu next hello hello **Computer** property and select **Group by 'Computer'**.</span></span>  

![Regrouper par ordinateur](media/log-analytics-log-search-log-search-portal/log-search-portal-10.png)

## <a name="work-with-results"></a><span data-ttu-id="51557-163">Utiliser les résultats</span><span class="sxs-lookup"><span data-stu-id="51557-163">Work with results</span></span>
<span data-ttu-id="51557-164">portail de recherche de journal Hello possède un large éventail de fonctionnalités pour l’utilisation des résultats hello d’une requête.</span><span class="sxs-lookup"><span data-stu-id="51557-164">hello Log Search portal has a variety of features for working with hello results of a query.</span></span>  <span data-ttu-id="51557-165">Vous pouvez trier, filtrer et regrouper des données de hello de tooanalyze de résultats sans modifier la requête réelle de hello.</span><span class="sxs-lookup"><span data-stu-id="51557-165">You can sort, filter, and group results tooanalyze hello data without modifying hello actual query.</span></span>  <span data-ttu-id="51557-166">Les résultats d’une requête ne sont pas triés par défaut.</span><span class="sxs-lookup"><span data-stu-id="51557-166">Results of a query are not sorted by default.</span></span>

<span data-ttu-id="51557-167">les données de salutation tooview sous forme de table qui fournit des options supplémentaires pour le filtrage et le tri, cliquez sur **Table**.</span><span class="sxs-lookup"><span data-stu-id="51557-167">tooview hello data in table form which provides additional options for filtering and sorting, click **Table**.</span></span>  

![Vue Table](media/log-analytics-log-search-log-search-portal/log-search-portal-05.png)

<span data-ttu-id="51557-169">Cliquez sur la flèche de hello par un enregistrement tooview les détails hello pour cet enregistrement.</span><span class="sxs-lookup"><span data-stu-id="51557-169">Click hello arrow by a record tooview hello details for that record.</span></span>

![Trier les résultats](media/log-analytics-log-search-log-search-portal/log-search-portal-06.png)

<span data-ttu-id="51557-171">Pour trier sur un champ, cliquez sur son en-tête de colonne.</span><span class="sxs-lookup"><span data-stu-id="51557-171">Sort on any field by clicking on its column header.</span></span>

![Trier les résultats](media/log-analytics-log-search-log-search-portal/log-search-portal-07.png)

<span data-ttu-id="51557-173">Filtrer les résultats de hello sur une valeur spécifique dans la colonne de hello en cliquant sur le bouton Filtrer hello et en fournissant une condition de filtre.</span><span class="sxs-lookup"><span data-stu-id="51557-173">Filter hello results on a specific value in hello column by clicking hello filter button and providing a filter condition.</span></span>

![Filtrer les résultats](media/log-analytics-log-search-log-search-portal/log-search-portal-08.png)

<span data-ttu-id="51557-175">Regrouper sur une colonne en faisant glisser en haut de toohello des en-tête de colonne des résultats de hello.</span><span class="sxs-lookup"><span data-stu-id="51557-175">Group on a column by dragging its column header toohello top of hello results.</span></span>  <span data-ttu-id="51557-176">Vous pouvez regrouper plusieurs champs en faisant glisser plusieurs colonnes toohello haut.</span><span class="sxs-lookup"><span data-stu-id="51557-176">You can group on multiple fields by dragging multiple columns toohello top.</span></span>

![Regrouper les résultats](media/log-analytics-log-search-log-search-portal/log-search-portal-09.png)



## <a name="work-with-performance-data"></a><span data-ttu-id="51557-178">Utiliser des données de performances</span><span class="sxs-lookup"><span data-stu-id="51557-178">Work with performance data</span></span>
<span data-ttu-id="51557-179">Données de performances pour les agents Windows et Linux sont stockées dans hello Analytique de journal espace de travail hello **Perf** table.</span><span class="sxs-lookup"><span data-stu-id="51557-179">Performance data for both Windows and Linux agents is stored in hello Log Analytics workspace in hello **Perf** table.</span></span>  <span data-ttu-id="51557-180">Les enregistrements de performances ressemblent aux autres enregistrements, et nous pouvons écrire une requête simple qui retourne tous les enregistrements de performances, tout comme avec les événements.</span><span class="sxs-lookup"><span data-stu-id="51557-180">Performance records look just like any other record, and we can write a simple query that returns all performance records just like with events.</span></span>

```
Perf
```

![Données de performances](media/log-analytics-log-search-log-search-portal/log-search-portal-11.png)

<span data-ttu-id="51557-182">Retourner plusieurs millions d’enregistrements pour tous les objets de performances et compteurs n’est cependant pas très utile.</span><span class="sxs-lookup"><span data-stu-id="51557-182">Returning millions of records for all performance objects and counters though isn't very useful.</span></span>  <span data-ttu-id="51557-183">Vous pouvez utiliser hello mêmes méthodes que vous utilisés au-dessus de données de hello toofilter ou simplement taper hello suivante de requête directement dans la zone de recherche de journal hello.</span><span class="sxs-lookup"><span data-stu-id="51557-183">You can use hello same methods you used above toofilter hello data or just type hello following query directly into hello log search box.</span></span>  <span data-ttu-id="51557-184">Cela retourne uniquement les enregistrements d’utilisation des processeurs pour les ordinateurs Windows et Linux.</span><span class="sxs-lookup"><span data-stu-id="51557-184">This returns only processor utilization records for both Windows and Linux computers.</span></span>

```
Perf | where (ObjectName == "Processor")  | where (CounterName == "% Processor Time")
```

![Utilisation des processeurs](media/log-analytics-log-search-log-search-portal/log-search-portal-12.png)

<span data-ttu-id="51557-186">Cela limite hello données tooa des compteurs de performance, mais il reste ne placer dans un formulaire qui est particulièrement utile.</span><span class="sxs-lookup"><span data-stu-id="51557-186">This limits hello data tooa particular counter, but it still doesn't put it in a form that's particularly useful.</span></span>  <span data-ttu-id="51557-187">Vous pouvez afficher les données de salutation dans un graphique en courbes, mais devez toogroup par ordinateur et TimeGenerated.</span><span class="sxs-lookup"><span data-stu-id="51557-187">You can display hello data in a line chart, but first need toogroup it by Computer and TimeGenerated.</span></span>  <span data-ttu-id="51557-188">toogroup sur plusieurs champs, vous devez les requêtes de hello toomodify directement, par conséquent, de modifier toohello éléments suivants de la requête hello.</span><span class="sxs-lookup"><span data-stu-id="51557-188">toogroup on multiple fields, you need toomodify hello query directly, so modify hello query toohello following.</span></span>  <span data-ttu-id="51557-189">Cette méthode utilise hello [avg](https://docs.loganalytics.io/docs/Language-Reference/Aggregation-functions/avg()) fonction hello **CounterValue** valeur moyenne de propriété toocalculate hello sur chaque heure.</span><span class="sxs-lookup"><span data-stu-id="51557-189">This uses hello [avg](https://docs.loganalytics.io/docs/Language-Reference/Aggregation-functions/avg()) function on hello **CounterValue** property toocalculate hello average value over each hour.</span></span>

```
Perf  | where (ObjectName == "Processor")  | where (CounterName == "% Processor Time") | summarize avg(CounterValue) by Computer, TimeGenerated
```

![Graphique de données de performances](media/log-analytics-log-search-log-search-portal/log-search-portal-13.png)

<span data-ttu-id="51557-191">Maintenant que les données de salutation sont regroupées convenablement, vous pouvez l’afficher dans un graphique visual en ajoutant hello [restituer](https://docs.loganalytics.io/docs/Language-Reference/Tabular-operators/render-operator) opérateur.</span><span class="sxs-lookup"><span data-stu-id="51557-191">Now that hello data is suitably grouped, you can display it in a visual chart by adding hello [render](https://docs.loganalytics.io/docs/Language-Reference/Tabular-operators/render-operator) operator.</span></span>  

```
Perf  | where (ObjectName == "Processor")  | where (CounterName == "% Processor Time") | summarize avg(CounterValue) by Computer, TimeGenerated | render timechart
```

![Graphique en courbes](media/log-analytics-log-search-log-search-portal/log-search-portal-14.png)

## <a name="next-steps"></a><span data-ttu-id="51557-193">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="51557-193">Next steps</span></span>

- <span data-ttu-id="51557-194">En savoir plus sur le langage de requête Analytique de journal hello à [prise en main de hello Analytique Portal](https://go.microsoft.com/fwlink/?linkid=856079).</span><span class="sxs-lookup"><span data-stu-id="51557-194">Learn more about hello Log Analytics query language at [Getting Started with hello Analytics Portal](https://go.microsoft.com/fwlink/?linkid=856079).</span></span>
- <span data-ttu-id="51557-195">Suivre un didacticiel à l’aide de hello [portal d’Analytique de Advanced](https://go.microsoft.com/fwlink/?linkid=856587) qui vous permet de toorun hello même des requêtes et des accès hello des mêmes données en tant que portail de recherche de journal hello.</span><span class="sxs-lookup"><span data-stu-id="51557-195">Walk through a tutorial using hello [Advanced Analytics portal](https://go.microsoft.com/fwlink/?linkid=856587) which allows you toorun hello same queries and access hello same data as hello Log Search portal.</span></span>
