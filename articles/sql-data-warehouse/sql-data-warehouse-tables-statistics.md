---
title: "aaaManaging des statistiques sur les tables de l’entrepôt de données SQL | Documents Microsoft"
description: Prise en main des statistiques sur les tables dans Azure SQL Data Warehouse.
services: sql-data-warehouse
documentationcenter: NA
author: shivaniguptamsft
manager: jhubbard
editor: 
ms.assetid: faa1034d-314c-4f9d-af81-f5a9aedf33e4
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: tables
ms.date: 10/31/2016
ms.author: shigu;barbkess
ms.openlocfilehash: c9521dc47891f68d124e77a53e2e15d03275caaa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-statistics-on-tables-in-sql-data-warehouse"></a><span data-ttu-id="5dab6-103">Gestion des statistiques sur les tables dans SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="5dab6-103">Managing statistics on tables in SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="5dab6-104">[Vue d’ensemble][Overview]</span><span class="sxs-lookup"><span data-stu-id="5dab6-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="5dab6-105">[Types de données][Data Types]</span><span class="sxs-lookup"><span data-stu-id="5dab6-105">[Data Types][Data Types]</span></span>
> * <span data-ttu-id="5dab6-106">[Distribuer][Distribute]</span><span class="sxs-lookup"><span data-stu-id="5dab6-106">[Distribute][Distribute]</span></span>
> * <span data-ttu-id="5dab6-107">[Index][Index]</span><span class="sxs-lookup"><span data-stu-id="5dab6-107">[Index][Index]</span></span>
> * <span data-ttu-id="5dab6-108">[Partition][Partition]</span><span class="sxs-lookup"><span data-stu-id="5dab6-108">[Partition][Partition]</span></span>
> * <span data-ttu-id="5dab6-109">[Statistiques][Statistics]</span><span class="sxs-lookup"><span data-stu-id="5dab6-109">[Statistics][Statistics]</span></span>
> * <span data-ttu-id="5dab6-110">[Temporaire][Temporary]</span><span class="sxs-lookup"><span data-stu-id="5dab6-110">[Temporary][Temporary]</span></span>
> 
> 

<span data-ttu-id="5dab6-111">Hello plus SQL Data Warehouse connaît vos données, hello plus rapidement qu’il peut exécuter des requêtes sur vos données.</span><span class="sxs-lookup"><span data-stu-id="5dab6-111">hello more SQL Data Warehouse knows about your data, hello faster it can execute queries against your data.</span></span>  <span data-ttu-id="5dab6-112">Hello qui vous indiquent à SQL Data Warehouse sur vos données, consiste à collecter des statistiques sur vos données.</span><span class="sxs-lookup"><span data-stu-id="5dab6-112">hello way that you tell SQL Data Warehouse about your data, is by collecting statistics about your data.</span></span>  <span data-ttu-id="5dab6-113">Contenant des statistiques sur vos données est un des points les plus importants hello faire toooptimize vos requêtes.</span><span class="sxs-lookup"><span data-stu-id="5dab6-113">Having statistics on your data is one of hello most important things you can do toooptimize your queries.</span></span>  <span data-ttu-id="5dab6-114">Statistiques de ménager de l’entrepôt de données SQL hello meilleur plan pour vos requêtes.</span><span class="sxs-lookup"><span data-stu-id="5dab6-114">Statistics help SQL Data Warehouse create hello most optimal plan for your queries.</span></span>  <span data-ttu-id="5dab6-115">Il s’agit, car l’optimiseur fondés sur une requête de SQL Data Warehouse hello optimiseur est un coût.</span><span class="sxs-lookup"><span data-stu-id="5dab6-115">This is because hello SQL Data Warehouse query optimizer is a cost based optimizer.</span></span>  <span data-ttu-id="5dab6-116">Autrement dit, il compare le coût de hello de différents plans de requête et choisit ensuite le plan hello hello onéreux, qui doit également être plan hello qui exécutera hello plus rapide.</span><span class="sxs-lookup"><span data-stu-id="5dab6-116">That is, it compares hello cost of various query plans and then chooses hello plan with hello lowest cost, which should also be hello plan that will execute hello fastest.</span></span>

<span data-ttu-id="5dab6-117">Les statistiques peuvent être créées sur une colonne unique, sur plusieurs colonnes ou sur un index d’une table.</span><span class="sxs-lookup"><span data-stu-id="5dab6-117">Statistics can be created on a single column, multiple columns or on an index of a table.</span></span>  <span data-ttu-id="5dab6-118">Les statistiques sont stockées dans un histogramme qui capture la plage de hello et la sélectivité des valeurs.</span><span class="sxs-lookup"><span data-stu-id="5dab6-118">Statistics are stored in a histogram which captures hello range and selectivity of values.</span></span>  <span data-ttu-id="5dab6-119">Cela présente un intérêt particulier lors de l’optimiseur de hello doit tooevaluate jointures, GROUP BY, HAVING et une clause WHERE dans une requête.</span><span class="sxs-lookup"><span data-stu-id="5dab6-119">This is of particular interest when hello optimizer needs tooevaluate JOINs, GROUP BY, HAVING and WHERE clauses in a query.</span></span>  <span data-ttu-id="5dab6-120">Par exemple, si l’optimiseur hello que date hello vous filtrez dans votre requête retourne 1 ligne, il peut choisir un autre plan que si elle estimations qu’ils date vous ont sélectionné va renvoyer 1 million de lignes.</span><span class="sxs-lookup"><span data-stu-id="5dab6-120">For example, if hello optimizer estimates that hello date you are filtering in your query will return 1 row, it may choose a very different plan than if it estimates that they date you have selected will return 1 million rows.</span></span>  <span data-ttu-id="5dab6-121">Lors de la création de statistiques est extrêmement important, il est tout aussi important que les statistiques *précisément* refléter l’état actuel de hello de table de hello.</span><span class="sxs-lookup"><span data-stu-id="5dab6-121">While creating statistics is extremely important, it is equally important that statistics *accurately* reflect hello current state of hello table.</span></span>  <span data-ttu-id="5dab6-122">Des statistiques à jour permet de garantir qu’un plan correct est sélectionné par l’optimiseur de hello.</span><span class="sxs-lookup"><span data-stu-id="5dab6-122">Having up-to-date statistics ensures that a good plan is selected by hello optimizer.</span></span>  <span data-ttu-id="5dab6-123">plans de Hello créés par l’optimiseur de hello ne sont pas aussi bien que les statistiques hello sur vos données.</span><span class="sxs-lookup"><span data-stu-id="5dab6-123">hello plans created by hello optimizer are only as good as hello statistics on your data.</span></span>

<span data-ttu-id="5dab6-124">Hello processus de création et de mise à jour des statistiques est actuellement un processus manuel, mais est très simple toodo.</span><span class="sxs-lookup"><span data-stu-id="5dab6-124">hello process of creating and updating statistics is currently a manual process, but is very simple toodo.</span></span>  <span data-ttu-id="5dab6-125">Cela diffère de SQL Server qui crée et met à jour automatiquement les statistiques sur les colonnes uniques et les index.</span><span class="sxs-lookup"><span data-stu-id="5dab6-125">This is unlike SQL Server which automatically creates and updates statistics on single columns and indexes.</span></span>  <span data-ttu-id="5dab6-126">À l’aide des informations de hello ci-dessous, vous pouvez considérablement automatiser la gestion de hello de statistiques de hello sur vos données.</span><span class="sxs-lookup"><span data-stu-id="5dab6-126">By using hello information below, you can greatly automate hello management of hello statistics on your data.</span></span> 

## <a name="getting-started-with-statistics"></a><span data-ttu-id="5dab6-127">Prise en main des statistiques</span><span class="sxs-lookup"><span data-stu-id="5dab6-127">Getting started with statistics</span></span>
 <span data-ttu-id="5dab6-128">Les statistiques échantillonnées sur chaque colonne est un moyen simple de tooget début de la création des statistiques.</span><span class="sxs-lookup"><span data-stu-id="5dab6-128">Creating sampled statistics on every column is an easy way tooget started with statistics.</span></span>  <span data-ttu-id="5dab6-129">Dans la mesure où il est tout aussi important tookeep les statistiques à jour, une méthode plus classique peut être tooupdate vos statistiques tous les jours ou après chaque charge.</span><span class="sxs-lookup"><span data-stu-id="5dab6-129">Since it is equally important tookeep statistics up-to-date, a conservative approach may be tooupdate your statistics daily or after each load.</span></span> <span data-ttu-id="5dab6-130">Il existe toujours un compromis entre performances et hello coût toocreate et mise à jour des statistiques.</span><span class="sxs-lookup"><span data-stu-id="5dab6-130">There are always trade-offs between performance and hello cost toocreate and update statistics.</span></span>  <span data-ttu-id="5dab6-131">Si vous trouvez que cela prend trop de temps toomaintain toutes vos statistiques, vous souhaiterez peut-être toobe tootry plus sélective sur les colonnes qui possèdent des statistiques ou les colonnes doive souvent mises à jour.</span><span class="sxs-lookup"><span data-stu-id="5dab6-131">If you find it is taking too long toomaintain all of your statistics, you may want tootry toobe more selective about which columns have statistics or which columns need frequent updating.</span></span>  <span data-ttu-id="5dab6-132">Vous pourriez par exemple, les colonnes de date tooupdate tous les jours, comme les nouvelles valeurs peuvent être ajoutées au lieu d’après chaque charge.</span><span class="sxs-lookup"><span data-stu-id="5dab6-132">For example, you might want tooupdate date columns daily, as new values may be added rather than after every load.</span></span> <span data-ttu-id="5dab6-133">Là encore, vous bénéficierez hello plus avantageux en ayant des statistiques sur des colonnes impliquées dans les jointures, GROUP BY, HAVING et une clause WHERE.</span><span class="sxs-lookup"><span data-stu-id="5dab6-133">Again, you will gain hello most benefit by having statistics on columns involved in JOINs, GROUP BY, HAVING and WHERE clauses.</span></span>  <span data-ttu-id="5dab6-134">Si vous avez une table avec un grand nombre de colonnes qui sont utilisés uniquement dans hello SELECT (clause), ne permettent pas de statistiques sur ces colonnes et un peu plus tooidentify d’effort de dépense uniquement les colonnes hello où aidera à des statistiques, peuvent réduire hello temps toomaintain vos statistiques .</span><span class="sxs-lookup"><span data-stu-id="5dab6-134">If you have a table with a lot of columns which are only used in hello SELECT clause, statistics on these columns may not help, and spending a little more effort tooidentify only hello columns where statistics will help, can reduce hello time toomaintain your statistics.</span></span>

## <a name="multi-column-statistics"></a><span data-ttu-id="5dab6-135">Statistiques sur plusieurs colonnes</span><span class="sxs-lookup"><span data-stu-id="5dab6-135">Multi-column statistics</span></span>
<span data-ttu-id="5dab6-136">En outre toocreating des statistiques sur les colonnes uniques, vous découvrirez peut-être que vos requêtes bénéficient de statistiques de colonnes multiples.</span><span class="sxs-lookup"><span data-stu-id="5dab6-136">In addition toocreating statistics on single columns, you may find that your queries will benefit from multi-column statistics.</span></span>  <span data-ttu-id="5dab6-137">Les statistiques sur plusieurs colonnes sont des données créées sur un ensemble de colonnes.</span><span class="sxs-lookup"><span data-stu-id="5dab6-137">Multi-column statistics are statistics created on a list of columns.</span></span>  <span data-ttu-id="5dab6-138">Ils comprennent les statistiques de colonne unique sur la première colonne de hello dans la liste de hello, ainsi que certaines informations de corrélation entre les colonnes appelée densités.</span><span class="sxs-lookup"><span data-stu-id="5dab6-138">They include single column statistics on hello first column in hello list, plus some cross-column correlation information called densities.</span></span>  <span data-ttu-id="5dab6-139">Par exemple, si vous avez une table qui s’attache tooanother sur deux colonnes, vous souhaiterez peut-être que l’entrepôt de données SQL peut améliorer le plan de hello s’il comprend la relation hello entre deux colonnes.</span><span class="sxs-lookup"><span data-stu-id="5dab6-139">For example, if you have a table that joins tooanother on two columns, you may find that SQL Data Warehouse can better optimize hello plan if it understands hello relationship between two columns.</span></span>   <span data-ttu-id="5dab6-140">Les statistiques sur plusieurs colonnes peuvent améliorer les performances des requêtes lors de certaines opérations, comme les clauses « group by » et les associations composites.</span><span class="sxs-lookup"><span data-stu-id="5dab6-140">Multi-column statistics can improve query performance for some operations such as composite joins and group by.</span></span>

## <a name="updating-statistics"></a><span data-ttu-id="5dab6-141">Mettre à jour les statistiques</span><span class="sxs-lookup"><span data-stu-id="5dab6-141">Updating statistics</span></span>
<span data-ttu-id="5dab6-142">Mettre à jour les statistiques est une composante importante de votre routine de gestion des bases de données.</span><span class="sxs-lookup"><span data-stu-id="5dab6-142">Updating statistics is an important part of your database management routine.</span></span>  <span data-ttu-id="5dab6-143">Lors de la distribution de hello des données dans la base de données hello change, les statistiques doivent toobe mis à jour.</span><span class="sxs-lookup"><span data-stu-id="5dab6-143">When hello distribution of data in hello database changes, statistics need toobe updated.</span></span>  <span data-ttu-id="5dab6-144">Les statistiques obsolètes entraîne des performances de requête optimales de toosub.</span><span class="sxs-lookup"><span data-stu-id="5dab6-144">Out-of-date statistics will lead toosub-optimal query performance.</span></span>

<span data-ttu-id="5dab6-145">Une meilleure solution consiste tooupdate des statistiques sur les colonnes de date chaque jour lors de l’ajout de nouvelles dates.</span><span class="sxs-lookup"><span data-stu-id="5dab6-145">One best practice is tooupdate statistics on date columns each day as new dates are added.</span></span>  <span data-ttu-id="5dab6-146">Chaque heure nouvelle sont chargées dans l’entrepôt de données hello, nouvelles dates de la charge ou les dates de transaction sont ajoutés.</span><span class="sxs-lookup"><span data-stu-id="5dab6-146">Each time new rows are loaded into hello data warehouse, new load dates or transaction dates are added.</span></span> <span data-ttu-id="5dab6-147">Modifier la distribution des données hello et les rendre les statistiques hello obsolètes.</span><span class="sxs-lookup"><span data-stu-id="5dab6-147">These change hello data distribution and make hello statistics out-of-date.</span></span> <span data-ttu-id="5dab6-148">À l’inverse, statistiques sur une colonne « pays » dans une table customer peut-être jamais toobe mis à jour, comme la distribution hello de valeurs généralement ne change pas.</span><span class="sxs-lookup"><span data-stu-id="5dab6-148">Conversely, statistics on a country column in a customer table might never need toobe updated, as hello distribution of values doesn’t generally change.</span></span> <span data-ttu-id="5dab6-149">En supposant que la distribution de hello est constante entre les clients, ajout de nouveaux variation de la table toohello lignes ne va pas la distribution des données toochange hello.</span><span class="sxs-lookup"><span data-stu-id="5dab6-149">Assuming hello distribution is constant between customers, adding new rows toohello table variation isn't going toochange hello data distribution.</span></span> <span data-ttu-id="5dab6-150">Toutefois, si votre entrepôt de données contient uniquement un pays et que vous importez des données à partir d’un nouveau pays, ce qui entraîne des données à partir de plusieurs pays doit être stockées, vous définitivement devez tooupdate des statistiques sur la colonne « pays » de hello.</span><span class="sxs-lookup"><span data-stu-id="5dab6-150">However, if your data warehouse only contains one country and you bring in data from a new country, resulting in data from multiple countries being stored, then you definitely need tooupdate statistics on hello country column.</span></span>

<span data-ttu-id="5dab6-151">Un des hello première questions tooask cas de dépannage d’une requête, » sont des statistiques de hello à jour ? »</span><span class="sxs-lookup"><span data-stu-id="5dab6-151">One of hello first questions tooask when troubleshooting a query is, "Are hello statistics up-to-date?"</span></span>

<span data-ttu-id="5dab6-152">Cette question n’est pas un objet qui peuvent être satisfaites par âge hello de données de hello.</span><span class="sxs-lookup"><span data-stu-id="5dab6-152">This question is not one that can be answered by hello age of hello data.</span></span> <span data-ttu-id="5dab6-153">Un objet de statistiques toodate haut peut être très anciens si il n’y a eu aucune toohello matériel les données sous-jacentes.</span><span class="sxs-lookup"><span data-stu-id="5dab6-153">An up toodate statistics object could be very old if there's been no material change toohello underlying data.</span></span> <span data-ttu-id="5dab6-154">Lorsque nombre hello de lignes a sensiblement changé ou il existe une modification significative de la distribution de hello des valeurs pour une colonne donnée *puis* il s’agit des statistiques de temps de tooupdate.</span><span class="sxs-lookup"><span data-stu-id="5dab6-154">When hello number of rows has changed substantially or there is a material change in hello distribution of values for a given column *then* it's time tooupdate statistics.</span></span>  

<span data-ttu-id="5dab6-155">Pour référence, **SQL Server** (et non SQL Data Warehouse) met automatiquement à jour les statistiques dans les cas suivants :</span><span class="sxs-lookup"><span data-stu-id="5dab6-155">For reference, **SQL Server** (not SQL Data Warehouse) automatically updates statistics for these situations:</span></span>

* <span data-ttu-id="5dab6-156">Si vous avez des lignes nulles dans une table de hello, lorsque vous ajoutez des lignes, vous obtiendrez une mise à jour automatique des statistiques</span><span class="sxs-lookup"><span data-stu-id="5dab6-156">If you have zero rows in hello table, when you add rows, you’ll get an automatic update of statistics</span></span>
* <span data-ttu-id="5dab6-157">Lorsque vous ajoutez plus de 500 table tooa de lignes à compter moins de 500 lignes (par exemple, au démarrage de l’avoir 499 et ajoutez-les au total tooa lignes 500 999 lignes), vous obtiendrez une mise à jour automatique</span><span class="sxs-lookup"><span data-stu-id="5dab6-157">When you add more than 500 rows tooa table starting with less than 500 rows (e.g. at start you have 499 and then add 500 rows tooa total of 999 rows), you’ll get an automatic update</span></span> 
* <span data-ttu-id="5dab6-158">Une fois que vous êtes plus de 500 lignes avoir tooadd de 500 lignes supplémentaires + 20 % de la taille de hello de table de hello avant que vous verrez une mise à jour automatique des statistiques de hello de</span><span class="sxs-lookup"><span data-stu-id="5dab6-158">Once you’re over 500 rows you will have tooadd 500 additional rows + 20% of hello size of hello table before you’ll see an automatic update on hello stats</span></span>

<span data-ttu-id="5dab6-159">Comme il n’existe aucun toodetermine DMV si les données dans la table de hello ont changé dans la mesure où les mises à jour les statistiques de temps dernière hello, connaître l’ancienneté hello de vos statistiques peut vous permettent de partie de l’image de hello.</span><span class="sxs-lookup"><span data-stu-id="5dab6-159">Since there is no DMV toodetermine if data within hello table has changed since hello last time statistics were updated, knowing hello age of your statistics can provide you with part of hello picture.</span></span>  <span data-ttu-id="5dab6-160">Vous pouvez utiliser hello suivant toodetermine hello dernière vos statistiques de requête lorsque la mise à jour sur chaque table.</span><span class="sxs-lookup"><span data-stu-id="5dab6-160">You can use hello following query toodetermine hello last time your statistics where updated on each table.</span></span>  

> [!NOTE]
> <span data-ttu-id="5dab6-161">N’oubliez pas que s’il existe une modification significative de la distribution de hello des valeurs pour une colonne donnée, vous devez mettre à jour statistiques indépendamment hello dernière, qu'ils ont été mis à jour.</span><span class="sxs-lookup"><span data-stu-id="5dab6-161">Remember if there is a material change in hello distribution of values for a given column, you should update statistics regardless of hello last time they were updated.</span></span>  
> 
> 

```sql
SELECT
    sm.[name] AS [schema_name],
    tb.[name] AS [table_name],
    co.[name] AS [stats_column_name],
    st.[name] AS [stats_name],
    STATS_DATE(st.[object_id],st.[stats_id]) AS [stats_last_updated_date]
FROM
    sys.objects ob
    JOIN sys.stats st
        ON  ob.[object_id] = st.[object_id]
    JOIN sys.stats_columns sc    
        ON  st.[stats_id] = sc.[stats_id]
        AND st.[object_id] = sc.[object_id]
    JOIN sys.columns co    
        ON  sc.[column_id] = co.[column_id]
        AND sc.[object_id] = co.[object_id]
    JOIN sys.types  ty    
        ON  co.[user_type_id] = ty.[user_type_id]
    JOIN sys.tables tb    
        ON  co.[object_id] = tb.[object_id]
    JOIN sys.schemas sm    
        ON  tb.[schema_id] = sm.[schema_id]
WHERE
    st.[user_created] = 1;
```

<span data-ttu-id="5dab6-162">Par exemple, les statistiques des colonnes de date d’un entrepôt de données doivent souvent être mises à jour.</span><span class="sxs-lookup"><span data-stu-id="5dab6-162">Date columns in a data warehouse, for example, usually need frequent statistics updates.</span></span> <span data-ttu-id="5dab6-163">Chaque heure nouvelle sont chargées dans l’entrepôt de données hello, nouvelles dates de la charge ou les dates de transaction sont ajoutés.</span><span class="sxs-lookup"><span data-stu-id="5dab6-163">Each time new rows are loaded into hello data warehouse, new load dates or transaction dates are added.</span></span> <span data-ttu-id="5dab6-164">Modifier la distribution des données hello et les rendre les statistiques hello obsolètes.</span><span class="sxs-lookup"><span data-stu-id="5dab6-164">These change hello data distribution and make hello statistics out-of-date.</span></span>  <span data-ttu-id="5dab6-165">À l’inverse, des statistiques sur une colonne sexe sur une table ne peuvent jamais besoin toobe mis à jour.</span><span class="sxs-lookup"><span data-stu-id="5dab6-165">Conversely, statistics on a gender column on a customer table might never need toobe updated.</span></span> <span data-ttu-id="5dab6-166">En supposant que la distribution de hello est constante entre les clients, ajout de nouveaux variation de la table toohello lignes ne va pas la distribution des données toochange hello.</span><span class="sxs-lookup"><span data-stu-id="5dab6-166">Assuming hello distribution is constant between customers, adding new rows toohello table variation isn't going toochange hello data distribution.</span></span> <span data-ttu-id="5dab6-167">Toutefois, si votre entrepôt de données ne contient qu’un sexe et une nouvelle spécification entraîne plusieurs sexes, vous définitivement devez tooupdate des statistiques sur la colonne de genre hello.</span><span class="sxs-lookup"><span data-stu-id="5dab6-167">However, if your data warehouse only contains one gender and a new requirement results in multiple genders then you definitely need tooupdate statistics on hello gender column.</span></span>

<span data-ttu-id="5dab6-168">Pour en savoir plus, consultez la section [Statistiques][Statistics] de MSDN.</span><span class="sxs-lookup"><span data-stu-id="5dab6-168">For further explanation, see [Statistics][Statistics] on MSDN.</span></span>

## <a name="implementing-statistics-management"></a><span data-ttu-id="5dab6-169">Implémentation de fonctions de gestion des statistiques</span><span class="sxs-lookup"><span data-stu-id="5dab6-169">Implementing statistics management</span></span>
<span data-ttu-id="5dab6-170">Il est souvent une bonne idée tooextend votre tooensure processus mises à jour des statistiques au niveau de chargement des données hello fin du chargement de hello.</span><span class="sxs-lookup"><span data-stu-id="5dab6-170">It is often a good idea tooextend your data loading process tooensure that statistics are updated at hello end of hello load.</span></span> <span data-ttu-id="5dab6-171">chargement des données Hello est lorsque les tables changent plus souvent leur taille et/ou la répartition des valeurs.</span><span class="sxs-lookup"><span data-stu-id="5dab6-171">hello data load is when tables most frequently change their size and/or their distribution of values.</span></span> <span data-ttu-id="5dab6-172">Par conséquent, il s’agit d’un tooimplement emplacement logique des processus de gestion.</span><span class="sxs-lookup"><span data-stu-id="5dab6-172">Therefore, this is a logical place tooimplement some management processes.</span></span>

<span data-ttu-id="5dab6-173">Certains principes sont fournies ci-dessous pour mettre à jour vos statistiques au cours du processus de chargement hello :</span><span class="sxs-lookup"><span data-stu-id="5dab6-173">Some guiding principles are provided below for updating your statistics during hello load process:</span></span>

* <span data-ttu-id="5dab6-174">Assurez-vous que chaque table chargée présente au moins un objet de statistiques mis à jour.</span><span class="sxs-lookup"><span data-stu-id="5dab6-174">Ensure that each loaded table has at least one statistics object updated.</span></span> <span data-ttu-id="5dab6-175">Les tables cette hello mises à jour les informations de taille (nombre de lignes et le nombre de pages) dans le cadre de la mise à jour des statistiques de hello.</span><span class="sxs-lookup"><span data-stu-id="5dab6-175">This updates hello tables size (row count and page count) information as part of hello stats update.</span></span>
* <span data-ttu-id="5dab6-176">Concentrez-vous sur les colonnes participant aux clauses JOIN, GROUP BY, ORDER BY et DISTINCT.</span><span class="sxs-lookup"><span data-stu-id="5dab6-176">Focus on columns participating in JOIN, GROUP BY, ORDER BY and DISTINCT clauses</span></span>
* <span data-ttu-id="5dab6-177">Envisagez la mise à jour de « par ordre croissant de clé » des colonnes telles que les transactions plus fréquemment car ces valeurs ne seront pas inclus dans l’histogramme des statistiques de hello des dates.</span><span class="sxs-lookup"><span data-stu-id="5dab6-177">Consider updating "ascending key" columns such as transaction dates more frequently as these values will not be included in hello statistics histogram.</span></span>
* <span data-ttu-id="5dab6-178">Envisagez de mettre moins souvent à jour les colonnes de distribution statiques.</span><span class="sxs-lookup"><span data-stu-id="5dab6-178">Consider updating static distribution columns less frequently.</span></span>
* <span data-ttu-id="5dab6-179">N’oubliez pas que chaque objet de statistiques est mis à jour à son tour.</span><span class="sxs-lookup"><span data-stu-id="5dab6-179">Remember each statistic object is updated in series.</span></span> <span data-ttu-id="5dab6-180">L’implémentation de l’élément `UPDATE STATISTICS <TABLE_NAME>` peut ne pas suffire, notamment lorsque les tables sont volumineuses et incluent un grand nombre d’objets de statistiques.</span><span class="sxs-lookup"><span data-stu-id="5dab6-180">Simply implementing `UPDATE STATISTICS <TABLE_NAME>` may not be ideal - especially for wide tables with lots of statistics objects.</span></span>

> [!NOTE]
> <span data-ttu-id="5dab6-181">Pour plus d’informations sur [croissant clé] consultez toohello SQL Server 2014 livre blanc estimation de la cardinalité.</span><span class="sxs-lookup"><span data-stu-id="5dab6-181">For more details on [ascending key] please refer toohello SQL Server 2014 cardinality estimation model whitepaper.</span></span>
> 
> 

<span data-ttu-id="5dab6-182">Pour en savoir plus, consultez la section [Estimation de la cardinalité][Cardinality Estimation] de MSDN.</span><span class="sxs-lookup"><span data-stu-id="5dab6-182">For further explanation, see  [Cardinality Estimation][Cardinality Estimation] on MSDN.</span></span>

## <a name="examples-create-statistics"></a><span data-ttu-id="5dab6-183">Exemples de création de statistiques</span><span class="sxs-lookup"><span data-stu-id="5dab6-183">Examples: Create statistics</span></span>
<span data-ttu-id="5dab6-184">Ces exemples montrent comment toouse diverses options pour la création de statistiques.</span><span class="sxs-lookup"><span data-stu-id="5dab6-184">These examples show how toouse various options for creating statistics.</span></span> <span data-ttu-id="5dab6-185">options de Hello que vous utilisez pour chaque colonne dépendent de caractéristiques hello de vos données et comment hello colonne sera utilisée dans les requêtes.</span><span class="sxs-lookup"><span data-stu-id="5dab6-185">hello options that you use for each column depend on hello characteristics of your data and how hello column will be used in queries.</span></span>

### <a name="a-create-single-column-statistics-with-default-options"></a><span data-ttu-id="5dab6-186">R :</span><span class="sxs-lookup"><span data-stu-id="5dab6-186">A.</span></span> <span data-ttu-id="5dab6-187">Créer des statistiques sur une colonne en utilisant les options par défaut</span><span class="sxs-lookup"><span data-stu-id="5dab6-187">Create single-column statistics with default options</span></span>
<span data-ttu-id="5dab6-188">toocreate des statistiques sur une colonne, il suffit de fournir un nom pour l’objet de statistiques hello et hello de colonne de hello.</span><span class="sxs-lookup"><span data-stu-id="5dab6-188">toocreate statistics on a column, simply provide a name for hello statistics object and hello name of hello column.</span></span>

<span data-ttu-id="5dab6-189">Cette syntaxe utilise toutes les options par défaut de hello.</span><span class="sxs-lookup"><span data-stu-id="5dab6-189">This syntax uses all of hello default options.</span></span> <span data-ttu-id="5dab6-190">Par défaut, SQL Data Warehouse exemples 20 pour cent de la table de hello lorsqu’il crée des statistiques.</span><span class="sxs-lookup"><span data-stu-id="5dab6-190">By default, SQL Data Warehouse samples 20 percent of hello table when it creates statistics.</span></span>

```sql
CREATE STATISTICS [statistics_name] ON [schema_name].[table_name]([column_name]);
```

<span data-ttu-id="5dab6-191">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="5dab6-191">For example:</span></span>

```sql
CREATE STATISTICS col1_stats ON dbo.table1 (col1);
```

### <a name="b-create-single-column-statistics-by-examining-every-row"></a><span data-ttu-id="5dab6-192">B.</span><span class="sxs-lookup"><span data-stu-id="5dab6-192">B.</span></span> <span data-ttu-id="5dab6-193">Créer des statistiques sur plusieurs colonnes en examinant chaque ligne</span><span class="sxs-lookup"><span data-stu-id="5dab6-193">Create single-column statistics by examining every row</span></span>
<span data-ttu-id="5dab6-194">taux d’échantillonnage par défaut Hello de 20 % est suffisant pour la plupart des situations.</span><span class="sxs-lookup"><span data-stu-id="5dab6-194">hello default sampling rate of 20 percent is sufficient for most situations.</span></span> <span data-ttu-id="5dab6-195">Toutefois, vous pouvez ajuster les taux d’échantillonnage de hello.</span><span class="sxs-lookup"><span data-stu-id="5dab6-195">However, you can adjust hello sampling rate.</span></span>

<span data-ttu-id="5dab6-196">hello toosample complète de table, utilisez la syntaxe suivante :</span><span class="sxs-lookup"><span data-stu-id="5dab6-196">toosample hello full table, use this syntax:</span></span>

```sql
CREATE STATISTICS [statistics_name] ON [schema_name].[table_name]([column_name]) WITH FULLSCAN;
```

<span data-ttu-id="5dab6-197">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="5dab6-197">For example:</span></span>

```sql
CREATE STATISTICS col1_stats ON dbo.table1 (col1) WITH FULLSCAN;
```

### <a name="c-create-single-column-statistics-by-specifying-hello-sample-size"></a><span data-ttu-id="5dab6-198">C.</span><span class="sxs-lookup"><span data-stu-id="5dab6-198">C.</span></span> <span data-ttu-id="5dab6-199">Créer des statistiques de colonne unique en spécifiant la taille de l’exemple hello</span><span class="sxs-lookup"><span data-stu-id="5dab6-199">Create single-column statistics by specifying hello sample size</span></span>
<span data-ttu-id="5dab6-200">Vous pouvez également spécifier la taille de l’exemple hello sous forme de pourcentage :</span><span class="sxs-lookup"><span data-stu-id="5dab6-200">Alternatively, you can specify hello sample size as a percent:</span></span>

```sql
CREATE STATISTICS col1_stats ON dbo.table1 (col1) WITH SAMPLE = 50 PERCENT;
```

### <a name="d-create-single-column-statistics-on-only-some-of-hello-rows"></a><span data-ttu-id="5dab6-201">D.</span><span class="sxs-lookup"><span data-stu-id="5dab6-201">D.</span></span> <span data-ttu-id="5dab6-202">Créer des statistiques de colonne unique sur certaines lignes de hello</span><span class="sxs-lookup"><span data-stu-id="5dab6-202">Create single-column statistics on only some of hello rows</span></span>
<span data-ttu-id="5dab6-203">Une autre option, vous pouvez créer des statistiques sur une partie des lignes de hello dans votre table.</span><span class="sxs-lookup"><span data-stu-id="5dab6-203">Another option, you can create statistics on a portion of hello rows in your table.</span></span> <span data-ttu-id="5dab6-204">On parle alors de « statistiques filtrées ».</span><span class="sxs-lookup"><span data-stu-id="5dab6-204">This is called a filtered statistic.</span></span>

<span data-ttu-id="5dab6-205">Par exemple, vous pouvez utiliser les statistiques filtrées lorsque vous planifiez tooquery une partition spécifique d’une grande table partitionnée.</span><span class="sxs-lookup"><span data-stu-id="5dab6-205">For example, you could use filtered statistics when you plan tooquery a specific partition of a large partitioned table.</span></span> <span data-ttu-id="5dab6-206">En créant des statistiques sur hello uniquement les valeurs de partition, précision hello de statistiques de hello améliorer et par conséquent, améliorer les performances des requêtes.</span><span class="sxs-lookup"><span data-stu-id="5dab6-206">By creating statistics on only hello partition values, hello accuracy of hello statistics will improve, and therefore improve query performance.</span></span>

<span data-ttu-id="5dab6-207">Dans cet exemple, des statistiques sont créées sur une plage de valeurs.</span><span class="sxs-lookup"><span data-stu-id="5dab6-207">This example creates statistics on a range of values.</span></span> <span data-ttu-id="5dab6-208">les valeurs Hello peut être défini de plage de hello toomatch de valeurs dans une partition.</span><span class="sxs-lookup"><span data-stu-id="5dab6-208">hello values could easily be defined toomatch hello range of values in a partition.</span></span>

```sql
CREATE STATISTICS stats_col1 ON table1(col1) WHERE col1 > '2000101' AND col1 < '20001231';
```

> [!NOTE]
> <span data-ttu-id="5dab6-209">Pour hello tooconsider d’optimiseur de requête à l’aide de statistiques filtrées lorsqu’il choisit le plan de requête distribuée hello, requête de hello doit tenir dans la définition de hello hello d’objet de statistiques.</span><span class="sxs-lookup"><span data-stu-id="5dab6-209">For hello query optimizer tooconsider using filtered statistics when it chooses hello distributed query plan, hello query must fit inside hello definition of hello statistics object.</span></span> <span data-ttu-id="5dab6-210">À l’aide de hello précédent exemple, hello la requête où clause a besoin de valeurs de col1 toospecify entre 2000101 et 20001231.</span><span class="sxs-lookup"><span data-stu-id="5dab6-210">Using hello previous example, hello query's where clause needs toospecify col1 values between 2000101 and 20001231.</span></span>
> 
> 

### <a name="e-create-single-column-statistics-with-all-hello-options"></a><span data-ttu-id="5dab6-211">E.</span><span class="sxs-lookup"><span data-stu-id="5dab6-211">E.</span></span> <span data-ttu-id="5dab6-212">Créer des statistiques de colonne unique avec toutes les options de hello</span><span class="sxs-lookup"><span data-stu-id="5dab6-212">Create single-column statistics with all hello options</span></span>
<span data-ttu-id="5dab6-213">Vous pouvez, bien entendu, de combiner les options hello.</span><span class="sxs-lookup"><span data-stu-id="5dab6-213">You can, of course, combine hello options together.</span></span> <span data-ttu-id="5dab6-214">exemple Hello ci-dessous crée un objet de statistiques filtrées avec une taille d’échantillon personnalisé :</span><span class="sxs-lookup"><span data-stu-id="5dab6-214">hello example below creates a filtered statistics object with a custom sample size:</span></span>

```sql
CREATE STATISTICS stats_col1 ON table1 (col1) WHERE col1 > '2000101' AND col1 < '20001231' WITH SAMPLE = 50 PERCENT;
```

<span data-ttu-id="5dab6-215">Pour la référence complète de hello, consultez [CREATE STATISTICS] [ CREATE STATISTICS] sur MSDN.</span><span class="sxs-lookup"><span data-stu-id="5dab6-215">For hello full reference, see [CREATE STATISTICS][CREATE STATISTICS] on MSDN.</span></span>

### <a name="f-create-multi-column-statistics"></a><span data-ttu-id="5dab6-216">F.</span><span class="sxs-lookup"><span data-stu-id="5dab6-216">F.</span></span> <span data-ttu-id="5dab6-217">Créer des statistiques sur plusieurs colonnes</span><span class="sxs-lookup"><span data-stu-id="5dab6-217">Create multi-column statistics</span></span>
<span data-ttu-id="5dab6-218">toocreate un statistiques multicolonnes, simplement utiliser les exemples précédents hello, mais spécifier plus de colonnes.</span><span class="sxs-lookup"><span data-stu-id="5dab6-218">toocreate a multi-column statistics, simply use hello previous examples, but specify more columns.</span></span>

> [!NOTE]
> <span data-ttu-id="5dab6-219">Histogramme Hello, qui est utilisé tooestimate nombre de lignes dans le résultat de la requête hello, est uniquement disponible pour hello première colonne répertorié dans la définition de l’objet statistiques hello.</span><span class="sxs-lookup"><span data-stu-id="5dab6-219">hello histogram, which is used tooestimate number of rows in hello query result, is only available for hello first column listed in hello statistics object definition.</span></span>
> 
> 

<span data-ttu-id="5dab6-220">Dans cet exemple, histogramme de hello est sur *produit\_catégorie*.</span><span class="sxs-lookup"><span data-stu-id="5dab6-220">In this example, hello histogram is on *product\_category*.</span></span> <span data-ttu-id="5dab6-221">Les statistiques portant sur différentes colonnes sont calculées sur la base des éléments *product\_category* et *product\_sub_c\ategory* :</span><span class="sxs-lookup"><span data-stu-id="5dab6-221">Cross-column statistics are calculated on *product\_category* and *product\_sub_c\ategory*:</span></span>

```sql
CREATE STATISTICS stats_2cols ON table1 (product_category, product_sub_category) WHERE product_category > '2000101' AND product_category < '20001231' WITH SAMPLE = 50 PERCENT;
```

<span data-ttu-id="5dab6-222">Dans la mesure où il existe une corrélation entre *produit\_catégorie* et *produit\_sub\_catégorie*, un état à plusieurs colonne peut être utile si ces colonnes sont accessibles. à hello même temps.</span><span class="sxs-lookup"><span data-stu-id="5dab6-222">Since there is a correlation between *product\_category* and *product\_sub\_category*, a multi-column stat can be useful if these columns are accessed at hello same time.</span></span>

### <a name="g-create-statistics-on-all-hello-columns-in-a-table"></a><span data-ttu-id="5dab6-223">G.</span><span class="sxs-lookup"><span data-stu-id="5dab6-223">G.</span></span> <span data-ttu-id="5dab6-224">Créer des statistiques sur toutes les colonnes hello dans une table</span><span class="sxs-lookup"><span data-stu-id="5dab6-224">Create statistics on all hello columns in a table</span></span>
<span data-ttu-id="5dab6-225">Statistiques d’une façon toocreate sont tooissues les commandes CREATE STATISTICS après avoir créé la table de hello.</span><span class="sxs-lookup"><span data-stu-id="5dab6-225">One way toocreate statistics is tooissues CREATE STATISTICS commands after creating hello table.</span></span>

```sql
CREATE TABLE dbo.table1
(
   col1 int
,  col2 int
,  col3 int
)
WITH
  (
    CLUSTERED COLUMNSTORE INDEX
  )
;

CREATE STATISTICS stats_col1 on dbo.table1 (col1);
CREATE STATISTICS stats_col2 on dbo.table2 (col2);
CREATE STATISTICS stats_col3 on dbo.table3 (col3);
```

### <a name="h-use-a-stored-procedure-toocreate-statistics-on-all-columns-in-a-database"></a><span data-ttu-id="5dab6-226">H.</span><span class="sxs-lookup"><span data-stu-id="5dab6-226">H.</span></span> <span data-ttu-id="5dab6-227">Utilisez une statistiques toocreate de procédure stockée sur toutes les colonnes dans une base de données</span><span class="sxs-lookup"><span data-stu-id="5dab6-227">Use a stored procedure toocreate statistics on all columns in a database</span></span>
<span data-ttu-id="5dab6-228">Entrepôt de données SQL n’a pas un équivalent de la procédure stockée système trop [] de [sp_create_stats] dans SQL Server.</span><span class="sxs-lookup"><span data-stu-id="5dab6-228">SQL Data Warehouse does not have a system stored procedure equivalent too[sp_create_stats][] in SQL Server.</span></span> <span data-ttu-id="5dab6-229">Cette procédure stockée crée un objet de statistiques de colonne unique sur chaque colonne de base de données hello qui ne possède pas de statistiques.</span><span class="sxs-lookup"><span data-stu-id="5dab6-229">This stored procedure creates a single column statistics object on every column of hello database that doesn't already have statistics.</span></span>

<span data-ttu-id="5dab6-230">Cela vous aidera à commencer à concevoir votre base de données.</span><span class="sxs-lookup"><span data-stu-id="5dab6-230">This will help you get started with your database design.</span></span> <span data-ttu-id="5dab6-231">Pensez tooadapt libre il tooyour a besoin.</span><span class="sxs-lookup"><span data-stu-id="5dab6-231">Feel free tooadapt it tooyour needs.</span></span>

```sql
CREATE PROCEDURE    [dbo].[prc_sqldw_create_stats]
(   @create_type    tinyint -- 1 default 2 Fullscan 3 Sample
,   @sample_pct     tinyint
)
AS

IF @create_type NOT IN (1,2,3)
BEGIN
    THROW 151000,'Invalid value for @stats_type parameter. Valid range 1 (default), 2 (fullscan) or 3 (sample).',1;
END;

IF @sample_pct IS NULL
BEGIN;
    SET @sample_pct = 20;
END;

IF OBJECT_ID('tempdb..#stats_ddl') IS NOT NULL
BEGIN;
    DROP TABLE #stats_ddl;
END;

CREATE TABLE #stats_ddl
WITH    (   DISTRIBUTION    = HASH([seq_nmbr])
        ,   LOCATION        = USER_DB
        )
AS
WITH T
AS
(
SELECT      t.[name]                        AS [table_name]
,           s.[name]                        AS [table_schema_name]
,           c.[name]                        AS [column_name]
,           c.[column_id]                   AS [column_id]
,           t.[object_id]                   AS [object_id]
,           ROW_NUMBER()
            OVER(ORDER BY (SELECT NULL))    AS [seq_nmbr]
FROM        sys.[tables] t
JOIN        sys.[schemas] s         ON  t.[schema_id]       = s.[schema_id]
JOIN        sys.[columns] c         ON  t.[object_id]       = c.[object_id]
LEFT JOIN   sys.[stats_columns] l   ON  l.[object_id]       = c.[object_id]
                                    AND l.[column_id]       = c.[column_id]
                                    AND l.[stats_column_id] = 1
LEFT JOIN    sys.[external_tables] e    ON    e.[object_id]        = t.[object_id]
WHERE       l.[object_id] IS NULL
AND            e.[object_id] IS NULL -- not an external table
)
SELECT  [table_schema_name]
,       [table_name]
,       [column_name]
,       [column_id]
,       [object_id]
,       [seq_nmbr]
,       CASE @create_type
        WHEN 1
        THEN    CAST('CREATE STATISTICS '+QUOTENAME('stat_'+table_schema_name+ '_' + table_name + '_'+column_name)+' ON '+QUOTENAME(table_schema_name)+'.'+QUOTENAME(table_name)+'('+QUOTENAME(column_name)+')' AS VARCHAR(8000))
        WHEN 2
        THEN    CAST('CREATE STATISTICS '+QUOTENAME('stat_'+table_schema_name+ '_' + table_name + '_'+column_name)+' ON '+QUOTENAME(table_schema_name)+'.'+QUOTENAME(table_name)+'('+QUOTENAME(column_name)+') WITH FULLSCAN' AS VARCHAR(8000))
        WHEN 3
        THEN    CAST('CREATE STATISTICS '+QUOTENAME('stat_'+table_schema_name+ '_' + table_name + '_'+column_name)+' ON '+QUOTENAME(table_schema_name)+'.'+QUOTENAME(table_name)+'('+QUOTENAME(column_name)+') WITH SAMPLE '+@sample_pct+'PERCENT' AS VARCHAR(8000))
        END AS create_stat_ddl
FROM T
;

DECLARE @i INT              = 1
,       @t INT              = (SELECT COUNT(*) FROM #stats_ddl)
,       @s NVARCHAR(4000)   = N''
;

WHILE @i <= @t
BEGIN
    SET @s=(SELECT create_stat_ddl FROM #stats_ddl WHERE seq_nmbr = @i);

    PRINT @s
    EXEC sp_executesql @s
    SET @i+=1;
END

DROP TABLE #stats_ddl;
```

<span data-ttu-id="5dab6-232">toocreate des statistiques sur toutes les colonnes de table hello avec cette procédure, appelez simplement la procédure de hello.</span><span class="sxs-lookup"><span data-stu-id="5dab6-232">toocreate statistics on all columns in hello table with this procedure, simply call hello procedure.</span></span>

```sql
prc_sqldw_create_stats;
```

## <a name="examples-update-statistics"></a><span data-ttu-id="5dab6-233">Exemple de mise à jour des statistiques</span><span class="sxs-lookup"><span data-stu-id="5dab6-233">Examples: update statistics</span></span>
<span data-ttu-id="5dab6-234">statistiques de tooupdate, vous pouvez :</span><span class="sxs-lookup"><span data-stu-id="5dab6-234">tooupdate statistics, you can:</span></span>

1. <span data-ttu-id="5dab6-235">Mettez à jour un objet de statistiques.</span><span class="sxs-lookup"><span data-stu-id="5dab6-235">Update one statistics object.</span></span> <span data-ttu-id="5dab6-236">Spécifiez nom hello Hello vous souhaitez tooupdate de l’objet de statistiques.</span><span class="sxs-lookup"><span data-stu-id="5dab6-236">Specify hello name of hello statistics object you wish tooupdate.</span></span>
2. <span data-ttu-id="5dab6-237">Mettez à jour tous les objets de statistiques sur une table.</span><span class="sxs-lookup"><span data-stu-id="5dab6-237">Update all statistics objects on a table.</span></span> <span data-ttu-id="5dab6-238">Spécifiez nom hello de table hello au lieu d’un objet de statistiques spécifiques.</span><span class="sxs-lookup"><span data-stu-id="5dab6-238">Specify hello name of hello table instead of one specific statistics object.</span></span>

### <a name="a-update-one-specific-statistics-object"></a><span data-ttu-id="5dab6-239">R :</span><span class="sxs-lookup"><span data-stu-id="5dab6-239">A.</span></span> <span data-ttu-id="5dab6-240">Mettre à jour un objet de statistiques spécifique</span><span class="sxs-lookup"><span data-stu-id="5dab6-240">Update one specific statistics object</span></span>
<span data-ttu-id="5dab6-241">Utilisez hello suivant de syntaxe tooupdate un objet de statistiques spécifique :</span><span class="sxs-lookup"><span data-stu-id="5dab6-241">Use hello following syntax tooupdate a specific statistics object:</span></span>

```sql
UPDATE STATISTICS [schema_name].[table_name]([stat_name]);
```

<span data-ttu-id="5dab6-242">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="5dab6-242">For example:</span></span>

```sql
UPDATE STATISTICS [dbo].[table1] ([stats_col1]);
```

<span data-ttu-id="5dab6-243">En mettant à jour les objets de statistiques spécifique, vous pouvez réduire hello temps et des ressources requises toomanage des statistiques.</span><span class="sxs-lookup"><span data-stu-id="5dab6-243">By updating specific statistics objects, you can minimize hello time and resources required toomanage statistics.</span></span> <span data-ttu-id="5dab6-244">Cela requiert que certains considéré, bien que, toochoose hello meilleures statistiques objets tooupdate.</span><span class="sxs-lookup"><span data-stu-id="5dab6-244">This requires some thought, though, toochoose hello best statistics objects tooupdate.</span></span>

### <a name="b-update-all-statistics-on-a-table"></a><span data-ttu-id="5dab6-245">B.</span><span class="sxs-lookup"><span data-stu-id="5dab6-245">B.</span></span> <span data-ttu-id="5dab6-246">Mettre à jour tous les objets de statistiques dans une table</span><span class="sxs-lookup"><span data-stu-id="5dab6-246">Update all statistics on a table</span></span>
<span data-ttu-id="5dab6-247">Voici une méthode simple pour mettre à jour tous les objets de statistiques hello sur une table.</span><span class="sxs-lookup"><span data-stu-id="5dab6-247">This shows a simple method for updating all hello statistics objects on a table.</span></span>

```sql
UPDATE STATISTICS [schema_name].[table_name];
```

<span data-ttu-id="5dab6-248">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="5dab6-248">For example:</span></span>

```sql
UPDATE STATISTICS dbo.table1;
```

<span data-ttu-id="5dab6-249">Cette instruction est toouse facile.</span><span class="sxs-lookup"><span data-stu-id="5dab6-249">This statement is easy toouse.</span></span> <span data-ttu-id="5dab6-250">N’oubliez pas que cela met à jour toutes les statistiques sur la table de hello et par conséquent peut travailler plus qu’il n’est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="5dab6-250">Just remember this updates all statistics on hello table, and therefore might perform more work than is necessary.</span></span> <span data-ttu-id="5dab6-251">Si les performances hello ne sont pas un problème, cela est moyen plus simple et la plus complète hello tooguarantee statistiques sont à jour.</span><span class="sxs-lookup"><span data-stu-id="5dab6-251">If hello performance is not an issue, this is definitely hello easiest and most complete way tooguarantee statistics are up-to-date.</span></span>

> [!NOTE]
> <span data-ttu-id="5dab6-252">Lors de la mise à jour toutes les statistiques d’une table, l’entrepôt de données SQL est une table de hello toosample analyse pour chaque statistiques.</span><span class="sxs-lookup"><span data-stu-id="5dab6-252">When updating all statistics on a table, SQL Data Warehouse does a scan toosample hello table for each statistics.</span></span> <span data-ttu-id="5dab6-253">Si la table de hello est volumineuse, a le nombre de colonnes et de nombreuses statistiques, il peut être plus efficace tooupdate individuels des statistiques en fonction des besoins.</span><span class="sxs-lookup"><span data-stu-id="5dab6-253">If hello table is large, has many columns, and many statistics, it might be more efficient tooupdate individual statistics based on need.</span></span>
> 
> 

<span data-ttu-id="5dab6-254">Pour une implémentation d’un `UPDATE STATISTICS` procédure consultez hello [Tables temporaires] [ Temporary] l’article.</span><span class="sxs-lookup"><span data-stu-id="5dab6-254">For an implementation of an `UPDATE STATISTICS` procedure please see hello [Temporary Tables][Temporary] article.</span></span> <span data-ttu-id="5dab6-255">méthode d’implémentation Hello est légèrement différent toohello `CREATE STATISTICS` procédure ci-dessus, mais le résultat final de hello est hello identiques.</span><span class="sxs-lookup"><span data-stu-id="5dab6-255">hello implementation method is slightly different toohello `CREATE STATISTICS` procedure above but hello end result is hello same.</span></span>

<span data-ttu-id="5dab6-256">Pour la syntaxe complète de hello, consultez [Update Statistics] [ Update Statistics] sur MSDN.</span><span class="sxs-lookup"><span data-stu-id="5dab6-256">For hello full syntax, see [Update Statistics][Update Statistics] on MSDN.</span></span>

## <a name="statistics-metadata"></a><span data-ttu-id="5dab6-257">Métadonnées de statistiques</span><span class="sxs-lookup"><span data-stu-id="5dab6-257">Statistics metadata</span></span>
<span data-ttu-id="5dab6-258">Il existe plusieurs vue système et fonctions que vous pouvez utiliser toofind des informations sur les statistiques.</span><span class="sxs-lookup"><span data-stu-id="5dab6-258">There are several system view and functions that you can use toofind information about statistics.</span></span> <span data-ttu-id="5dab6-259">Par exemple, vous pouvez voir si un objet de statistiques sont obsolète à l’aide de hello statistiques-date fonction toosee lorsque les statistiques de dernière création ou mise à jour.</span><span class="sxs-lookup"><span data-stu-id="5dab6-259">For example, you can see if a statistics object might be out-of-date by using hello stats-date function toosee when statistics were last created or updated.</span></span>

### <a name="catalog-views-for-statistics"></a><span data-ttu-id="5dab6-260">Vues de catalogue des statistiques</span><span class="sxs-lookup"><span data-stu-id="5dab6-260">Catalog views for statistics</span></span>
<span data-ttu-id="5dab6-261">Ces vues système fournissent des informations sur les statistiques :</span><span class="sxs-lookup"><span data-stu-id="5dab6-261">These system views provide information about statistics:</span></span>

| <span data-ttu-id="5dab6-262">Vue de catalogue</span><span class="sxs-lookup"><span data-stu-id="5dab6-262">Catalog View</span></span> | <span data-ttu-id="5dab6-263">Description</span><span class="sxs-lookup"><span data-stu-id="5dab6-263">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="5dab6-264">[sys.columns][sys.columns]</span><span class="sxs-lookup"><span data-stu-id="5dab6-264">[sys.columns][sys.columns]</span></span> |<span data-ttu-id="5dab6-265">Une ligne pour chaque colonne.</span><span class="sxs-lookup"><span data-stu-id="5dab6-265">One row for each column.</span></span> |
| <span data-ttu-id="5dab6-266">[sys.objects][sys.objects]</span><span class="sxs-lookup"><span data-stu-id="5dab6-266">[sys.objects][sys.objects]</span></span> |<span data-ttu-id="5dab6-267">Une ligne pour chaque objet de base de données hello.</span><span class="sxs-lookup"><span data-stu-id="5dab6-267">One row for each object in hello database.</span></span> |
| <span data-ttu-id="5dab6-268">[sys.schemas][sys.schemas]</span><span class="sxs-lookup"><span data-stu-id="5dab6-268">[sys.schemas][sys.schemas]</span></span> |<span data-ttu-id="5dab6-269">Une ligne pour chaque schéma de base de données hello.</span><span class="sxs-lookup"><span data-stu-id="5dab6-269">One row for each schema in hello database.</span></span> |
| <span data-ttu-id="5dab6-270">[sys.stats][sys.stats]</span><span class="sxs-lookup"><span data-stu-id="5dab6-270">[sys.stats][sys.stats]</span></span> |<span data-ttu-id="5dab6-271">Une ligne pour chaque objet de statistiques.</span><span class="sxs-lookup"><span data-stu-id="5dab6-271">One row for each statistics object.</span></span> |
| <span data-ttu-id="5dab6-272">[sys.stats_columns][sys.stats_columns]</span><span class="sxs-lookup"><span data-stu-id="5dab6-272">[sys.stats_columns][sys.stats_columns]</span></span> |<span data-ttu-id="5dab6-273">Une ligne pour chaque colonne dans l’objet de statistiques hello.</span><span class="sxs-lookup"><span data-stu-id="5dab6-273">One row for each column in hello statistics object.</span></span> <span data-ttu-id="5dab6-274">Revient toosys.columns.</span><span class="sxs-lookup"><span data-stu-id="5dab6-274">Links back toosys.columns.</span></span> |
| <span data-ttu-id="5dab6-275">[sys.tables][sys.tables]</span><span class="sxs-lookup"><span data-stu-id="5dab6-275">[sys.tables][sys.tables]</span></span> |<span data-ttu-id="5dab6-276">Une ligne pour chaque table (y compris les tables externes).</span><span class="sxs-lookup"><span data-stu-id="5dab6-276">One row for each table (includes external tables).</span></span> |
| <span data-ttu-id="5dab6-277">[sys.table_types][sys.table_types]</span><span class="sxs-lookup"><span data-stu-id="5dab6-277">[sys.table_types][sys.table_types]</span></span> |<span data-ttu-id="5dab6-278">Une ligne pour chaque type de données.</span><span class="sxs-lookup"><span data-stu-id="5dab6-278">One row for each data type.</span></span> |

### <a name="system-functions-for-statistics"></a><span data-ttu-id="5dab6-279">Fonctions système relatives aux statistiques</span><span class="sxs-lookup"><span data-stu-id="5dab6-279">System functions for statistics</span></span>
<span data-ttu-id="5dab6-280">Ces fonctions système sont utiles lorsque vous gérez des statistiques :</span><span class="sxs-lookup"><span data-stu-id="5dab6-280">These system functions are useful for working with statistics:</span></span>

| <span data-ttu-id="5dab6-281">Fonction système</span><span class="sxs-lookup"><span data-stu-id="5dab6-281">System Function</span></span> | <span data-ttu-id="5dab6-282">Description</span><span class="sxs-lookup"><span data-stu-id="5dab6-282">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="5dab6-283">[STATS_DATE][STATS_DATE]</span><span class="sxs-lookup"><span data-stu-id="5dab6-283">[STATS_DATE][STATS_DATE]</span></span> |<span data-ttu-id="5dab6-284">Objet de statistiques hello date a été modifié.</span><span class="sxs-lookup"><span data-stu-id="5dab6-284">Date hello statistics object was last updated.</span></span> |
| <span data-ttu-id="5dab6-285">[DBCC SHOW_STATISTICS][DBCC SHOW_STATISTICS]</span><span class="sxs-lookup"><span data-stu-id="5dab6-285">[DBCC SHOW_STATISTICS][DBCC SHOW_STATISTICS]</span></span> |<span data-ttu-id="5dab6-286">Fournit des informations de résumé et détaillées sur la distribution des valeurs de hello comme comprise par l’objet de statistiques hello.</span><span class="sxs-lookup"><span data-stu-id="5dab6-286">Provides summary level and detailed information about hello distribution of values as understood by hello statistics object.</span></span> |

### <a name="combine-statistics-columns-and-functions-into-one-view"></a><span data-ttu-id="5dab6-287">Combiner des fonctions et des colonnes de statistiques en une seule vue</span><span class="sxs-lookup"><span data-stu-id="5dab6-287">Combine statistics columns and functions into one view</span></span>
<span data-ttu-id="5dab6-288">Cette vue affiche les colonnes liées ensemble toostatistics et les résultats à partir de la fonction de hello [STATS_DATE()] [].</span><span class="sxs-lookup"><span data-stu-id="5dab6-288">This view brings columns that relate toostatistics, and results from hello [STATS_DATE()][]function together.</span></span>

```sql
CREATE VIEW dbo.vstats_columns
AS
SELECT
        sm.[name]                           AS [schema_name]
,       tb.[name]                           AS [table_name]
,       st.[name]                           AS [stats_name]
,       st.[filter_definition]              AS [stats_filter_defiinition]
,       st.[has_filter]                     AS [stats_is_filtered]
,       STATS_DATE(st.[object_id],st.[stats_id])
                                            AS [stats_last_updated_date]
,       co.[name]                           AS [stats_column_name]
,       ty.[name]                           AS [column_type]
,       co.[max_length]                     AS [column_max_length]
,       co.[precision]                      AS [column_precision]
,       co.[scale]                          AS [column_scale]
,       co.[is_nullable]                    AS [column_is_nullable]
,       co.[collation_name]                 AS [column_collation_name]
,       QUOTENAME(sm.[name])+'.'+QUOTENAME(tb.[name])
                                            AS two_part_name
,       QUOTENAME(DB_NAME())+'.'+QUOTENAME(sm.[name])+'.'+QUOTENAME(tb.[name])
                                            AS three_part_name
FROM    sys.objects                         AS ob
JOIN    sys.stats           AS st ON    ob.[object_id]      = st.[object_id]
JOIN    sys.stats_columns   AS sc ON    st.[stats_id]       = sc.[stats_id]
                            AND         st.[object_id]      = sc.[object_id]
JOIN    sys.columns         AS co ON    sc.[column_id]      = co.[column_id]
                            AND         sc.[object_id]      = co.[object_id]
JOIN    sys.types           AS ty ON    co.[user_type_id]   = ty.[user_type_id]
JOIN    sys.tables          AS tb ON  co.[object_id]        = tb.[object_id]
JOIN    sys.schemas         AS sm ON  tb.[schema_id]        = sm.[schema_id]
WHERE   1=1
AND     st.[user_created] = 1
;
```

## <a name="dbcc-showstatistics-examples"></a><span data-ttu-id="5dab6-289">Exemples portant sur la fonction DBCC SHOW_STATISTICS()</span><span class="sxs-lookup"><span data-stu-id="5dab6-289">DBCC SHOW_STATISTICS() examples</span></span>
<span data-ttu-id="5dab6-290">DBCC SHOW_STATISTICS() affiche les données de hello contenues dans un objet de statistiques.</span><span class="sxs-lookup"><span data-stu-id="5dab6-290">DBCC SHOW_STATISTICS() shows hello data held within a statistics object.</span></span> <span data-ttu-id="5dab6-291">Ces données sont affichées en trois parties.</span><span class="sxs-lookup"><span data-stu-id="5dab6-291">This data comes in three parts.</span></span>

1. <span data-ttu-id="5dab6-292">En-tête</span><span class="sxs-lookup"><span data-stu-id="5dab6-292">Header</span></span>
2. <span data-ttu-id="5dab6-293">Vecteur de densité</span><span class="sxs-lookup"><span data-stu-id="5dab6-293">Density Vector</span></span>
3. <span data-ttu-id="5dab6-294">Histogramme</span><span class="sxs-lookup"><span data-stu-id="5dab6-294">Histogram</span></span>

<span data-ttu-id="5dab6-295">métadonnées d’en-tête Hello sur les statistiques de hello.</span><span class="sxs-lookup"><span data-stu-id="5dab6-295">hello header metadata about hello statistics.</span></span> <span data-ttu-id="5dab6-296">histogramme de Hello affiche la distribution hello des valeurs dans la première colonne clé hello hello d’objet de statistiques.</span><span class="sxs-lookup"><span data-stu-id="5dab6-296">hello histogram displays hello distribution of values in hello first key column of hello statistics object.</span></span> <span data-ttu-id="5dab6-297">vecteur de densité Hello mesure la corrélation entre les colonnes.</span><span class="sxs-lookup"><span data-stu-id="5dab6-297">hello density vector measures cross-column correlation.</span></span> <span data-ttu-id="5dab6-298">SQLDW calcule les estimations de cardinalité avec les données hello dans l’objet de statistiques hello.</span><span class="sxs-lookup"><span data-stu-id="5dab6-298">SQLDW computes cardinality estimates with any of hello data in hello statistics object.</span></span>

### <a name="show-header-density-and-histogram"></a><span data-ttu-id="5dab6-299">Afficher l’en-tête, la densité et l’histogramme</span><span class="sxs-lookup"><span data-stu-id="5dab6-299">Show header, density, and histogram</span></span>
<span data-ttu-id="5dab6-300">Cet exemple simple illustre les trois parties d’un objet de statistiques.</span><span class="sxs-lookup"><span data-stu-id="5dab6-300">This simple example shows all three parts of a statistics object.</span></span>

```sql
DBCC SHOW_STATISTICS([<schema_name>.<table_name>],<stats_name>)
```

<span data-ttu-id="5dab6-301">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="5dab6-301">For example:</span></span>

```sql
DBCC SHOW_STATISTICS (dbo.table1, stats_col1);
```

### <a name="show-one-or-more-parts-of-dbcc-showstatistics"></a><span data-ttu-id="5dab6-302">Afficher une ou plusieurs parties de la fonction DBCC SHOW_STATISTICS();</span><span class="sxs-lookup"><span data-stu-id="5dab6-302">Show one or more parts of DBCC SHOW_STATISTICS();</span></span>
<span data-ttu-id="5dab6-303">Si vous êtes uniquement intéressé par des composants spécifiques, utilisez hello `WITH` clause et spécifiez ce qui les parties que vous voulez toosee :</span><span class="sxs-lookup"><span data-stu-id="5dab6-303">If you are only interested in viewing specific parts, use hello `WITH` clause and specify which parts you want toosee:</span></span>

```sql
DBCC SHOW_STATISTICS([<schema_name>.<table_name>],<stats_name>) WITH stat_header, histogram, density_vector
```

<span data-ttu-id="5dab6-304">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="5dab6-304">For example:</span></span>

```sql
DBCC SHOW_STATISTICS (dbo.table1, stats_col1) WITH histogram, density_vector
```

## <a name="dbcc-showstatistics-differences"></a><span data-ttu-id="5dab6-305">Différences liées à la fonction DBCC SHOW_STATISTICS()</span><span class="sxs-lookup"><span data-stu-id="5dab6-305">DBCC SHOW_STATISTICS() differences</span></span>
<span data-ttu-id="5dab6-306">DBCC SHOW_STATISTICS() est plus strictement implémenté dans SQL Data Warehouse comparées tooSQL Server.</span><span class="sxs-lookup"><span data-stu-id="5dab6-306">DBCC SHOW_STATISTICS() is more strictly implemented in SQL Data Warehouse compared tooSQL Server.</span></span>

1. <span data-ttu-id="5dab6-307">Les fonctions non documentées ne sont pas prises en charge.</span><span class="sxs-lookup"><span data-stu-id="5dab6-307">Undocumented features are not supported</span></span>
2. <span data-ttu-id="5dab6-308">Impossible d’utiliser le paramètre « Stats_stream ».</span><span class="sxs-lookup"><span data-stu-id="5dab6-308">Cannot use Stats_stream</span></span>
3. <span data-ttu-id="5dab6-309">Impossible de joindre les résultats de sous-ensembles spécifiques de données de statistiques, par exemple : STAT_HEADER JOIN DENSITY_VECTOR.</span><span class="sxs-lookup"><span data-stu-id="5dab6-309">Cannot join results for specific subsets of statistics data e.g. (STAT_HEADER JOIN DENSITY_VECTOR)</span></span>
4. <span data-ttu-id="5dab6-310">L’élément NO_INFOMSGS ne peut pas être défini pour la suppression des messages.</span><span class="sxs-lookup"><span data-stu-id="5dab6-310">NO_INFOMSGS cannot be set for message suppression</span></span>
5. <span data-ttu-id="5dab6-311">Vous ne pouvez pas placer de crochets autour des noms de statistiques.</span><span class="sxs-lookup"><span data-stu-id="5dab6-311">Square brackets around statistics names cannot be used</span></span>
6. <span data-ttu-id="5dab6-312">Impossible d’utiliser les objets de statistiques de colonne noms tooidentify</span><span class="sxs-lookup"><span data-stu-id="5dab6-312">Cannot use column names tooidentify statistics objects</span></span>
7. <span data-ttu-id="5dab6-313">L’erreur personnalisée 2767 n’est pas prise en charge.</span><span class="sxs-lookup"><span data-stu-id="5dab6-313">Custom error 2767 is not supported</span></span>

## <a name="next-steps"></a><span data-ttu-id="5dab6-314">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="5dab6-314">Next steps</span></span>
<span data-ttu-id="5dab6-315">Pour en savoir plus, consultez la section [DBCC SHOW_STATISTICS][DBCC SHOW_STATISTICS] de MSDN.</span><span class="sxs-lookup"><span data-stu-id="5dab6-315">For more details, see [DBCC SHOW_STATISTICS][DBCC SHOW_STATISTICS] on MSDN.</span></span>  <span data-ttu-id="5dab6-316">toolearn, voir les articles hello sur [vue d’ensemble de la Table][Overview], [les Types de données de Table][Data Types], [distribution d’une Table] [ Distribute], [L’indexation d’une Table][Index], [partitionnement d’une Table] [ Partition] et [ Tables temporaires][Temporary].</span><span class="sxs-lookup"><span data-stu-id="5dab6-316">toolearn more, see hello articles on [Table Overview][Overview], [Table Data Types][Data Types], [Distributing a Table][Distribute], [Indexing a Table][Index],  [Partitioning a Table][Partition] and [Temporary Tables][Temporary].</span></span>  <span data-ttu-id="5dab6-317">Pour en savoir plus sur les meilleures pratiques, consultez [Meilleures pratiques relatives à SQL Data Warehouse][SQL Data Warehouse Best Practices].</span><span class="sxs-lookup"><span data-stu-id="5dab6-317">For more about best practices, see [SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices].</span></span>  

<!--Image references-->

<!--Article references-->
[Overview]: ./sql-data-warehouse-tables-overview.md
[Data Types]: ./sql-data-warehouse-tables-data-types.md
[Distribute]: ./sql-data-warehouse-tables-distribute.md
[Index]: ./sql-data-warehouse-tables-index.md
[Partition]: ./sql-data-warehouse-tables-partition.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md
[Temporary]: ./sql-data-warehouse-tables-temporary.md
[SQL Data Warehouse Best Practices]: ./sql-data-warehouse-best-practices.md

<!--MSDN references-->  
[Cardinality Estimation]: https://msdn.microsoft.com/library/dn600374.aspx
[CREATE STATISTICS]: https://msdn.microsoft.com/library/ms188038.aspx
[DBCC SHOW_STATISTICS]:https://msdn.microsoft.com/library/ms174384.aspx
[Statistics]: https://msdn.microsoft.com/library/ms190397.aspx
[STATS_DATE]: https://msdn.microsoft.com/library/ms190330.aspx
[sys.columns]: https://msdn.microsoft.com/library/ms176106.aspx
[sys.objects]: https://msdn.microsoft.com/library/ms190324.aspx
[sys.schemas]: https://msdn.microsoft.com/library/ms190324.aspx
[sys.stats]: https://msdn.microsoft.com/library/ms177623.aspx
[sys.stats_columns]: https://msdn.microsoft.com/library/ms187340.aspx
[sys.tables]: https://msdn.microsoft.com/library/ms187406.aspx
[sys.table_types]: https://msdn.microsoft.com/library/bb510623.aspx
[UPDATE STATISTICS]: https://msdn.microsoft.com/library/ms187348.aspx

<!--Other Web references-->  
