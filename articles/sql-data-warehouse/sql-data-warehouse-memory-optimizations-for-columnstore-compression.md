---
title: "performances de l’index columnstore aaaImprove dans SQL Azure | Documents Microsoft"
description: "Réduire les besoins en mémoire ou augmentez hello mémoire disponible toomaximize hello nombre de lignes de qu'un index columnstore compresse dans chaque groupe de lignes."
services: sql-data-warehouse
documentationcenter: NA
author: shivaniguptamsft
manager: jhubbard
editor: 
ms.assetid: ef170f39-ae24-4b04-af76-53bb4c4d16d3
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: performance
ms.date: 6/2/2017
ms.author: shigu;barbkess
ms.openlocfilehash: 2c5a68435aa200236a2dc8538aa4638b52a59093
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="maximizing-rowgroup-quality-for-columnstore"></a><span data-ttu-id="9c987-103">Optimiser la qualité du rowgroup pour columnstore</span><span class="sxs-lookup"><span data-stu-id="9c987-103">Maximizing rowgroup quality for columnstore</span></span>

<span data-ttu-id="9c987-104">Qualité de Rowgroup est déterminée par le nombre de hello de lignes dans un groupe de lignes.</span><span class="sxs-lookup"><span data-stu-id="9c987-104">Rowgroup quality is determined by hello number of rows in a rowgroup.</span></span> <span data-ttu-id="9c987-105">Réduire les besoins en mémoire ou augmentez hello mémoire disponible toomaximize hello nombre de lignes de qu'un index columnstore compresse dans chaque groupe de lignes.</span><span class="sxs-lookup"><span data-stu-id="9c987-105">Reduce memory requirements or increase hello available memory toomaximize hello number of rows a columnstore index compresses into each rowgroup.</span></span>  <span data-ttu-id="9c987-106">Utilisez ces modes tooimprove de taux de compression et les performances des requêtes pour les index columnstore.</span><span class="sxs-lookup"><span data-stu-id="9c987-106">Use these methods tooimprove compression rates and query performance for columnstore indexes.</span></span>

## <a name="why-hello-rowgroup-size-matters"></a><span data-ttu-id="9c987-107">Importance de la taille de rowgroup hello</span><span class="sxs-lookup"><span data-stu-id="9c987-107">Why hello rowgroup size matters</span></span>
<span data-ttu-id="9c987-108">Dans la mesure où un index columnstore analyse une table en analysant les segments de colonne de rowgroups individuels, optimiser le nombre de hello de lignes dans chaque groupe de lignes améliore les performances de requête.</span><span class="sxs-lookup"><span data-stu-id="9c987-108">Since a columnstore index scans a table by scanning column segments of individual rowgroups, maximizing hello number of rows in each rowgroup enhances query performance.</span></span> <span data-ttu-id="9c987-109">Lorsque rowgroups ont un grand nombre de lignes, la compression des données permet d’améliorer ce qui signifie qu'est moins tooread de données à partir du disque.</span><span class="sxs-lookup"><span data-stu-id="9c987-109">When rowgroups have a high number of rows, data compression improves which means there is less data tooread from disk.</span></span>

<span data-ttu-id="9c987-110">Pour plus d’informations sur les rowgroups, voir [Description des index columnstore](https://msdn.microsoft.com/library/gg492088.aspx).</span><span class="sxs-lookup"><span data-stu-id="9c987-110">For more information about rowgroups, see [Columnstore Indexes Guide](https://msdn.microsoft.com/library/gg492088.aspx).</span></span>

## <a name="target-size-for-rowgroups"></a><span data-ttu-id="9c987-111">Taille cible des rowgroups</span><span class="sxs-lookup"><span data-stu-id="9c987-111">Target size for rowgroups</span></span>
<span data-ttu-id="9c987-112">Pour de meilleures performances de requête, hello vise nombre de hello toomaximize de lignes par rowgroup dans un index columnstore.</span><span class="sxs-lookup"><span data-stu-id="9c987-112">For best query performance, hello goal is toomaximize hello number of rows per rowgroup in a columnstore index.</span></span> <span data-ttu-id="9c987-113">Un rowgroup peut compter au maximum 1 048 576 lignes.</span><span class="sxs-lookup"><span data-stu-id="9c987-113">A rowgroup can have a maximum of 1,048,576 rows.</span></span> <span data-ttu-id="9c987-114">Son toonot OK ont un nombre maximal de hello de lignes par rowgroup.</span><span class="sxs-lookup"><span data-stu-id="9c987-114">It's okay toonot have hello maximum number of rows per rowgroup.</span></span> <span data-ttu-id="9c987-115">Les index columnstore produisent de bonnes performances quand les rowgroups comprennent au moins 100 000 lignes.</span><span class="sxs-lookup"><span data-stu-id="9c987-115">Columnstore indexes achieve good performance when rowgroups have at least 100,000 rows.</span></span>

## <a name="rowgroups-can-get-trimmed-during-compression"></a><span data-ttu-id="9c987-116">Des rowgroups peuvent être découpés en cours de compression</span><span class="sxs-lookup"><span data-stu-id="9c987-116">Rowgroups can get trimmed during compression</span></span>

<span data-ttu-id="9c987-117">Pendant une reconstruction d’index en bloc charge ou columnstore, parfois, il n’est pas assez toocompress disponible mémoire que tous hello désignés pour chaque groupe de lignes.</span><span class="sxs-lookup"><span data-stu-id="9c987-117">During a bulk load or columnstore index rebuild, sometimes there isn't enough memory available toocompress all hello rows designated for each rowgroup.</span></span> <span data-ttu-id="9c987-118">En cas de sollicitation de la mémoire, les index columnstore trim tailles de rowgroup hello compression dans hello columnstore permettre fonctionner.</span><span class="sxs-lookup"><span data-stu-id="9c987-118">When there is memory pressure, columnstore indexes trim hello rowgroup sizes so compression into hello columnstore can succeed.</span></span> 

<span data-ttu-id="9c987-119">Lorsqu’il existe des lignes toocompress au moins 10 000 de mémoire insuffisante dans chaque groupe de lignes, SQL Data Warehouse génère une erreur.</span><span class="sxs-lookup"><span data-stu-id="9c987-119">When there is insufficient memory toocompress at least 10,000 rows into each rowgroup, SQL Data Warehouse generates an error.</span></span>

<span data-ttu-id="9c987-120">Pour plus d’informations sur le chargement en masse, voir [Chargement de données d’index columnstore](https://msdn.microsoft.com/en-us/library/dn935008.aspx#Bulk load into a clustered columnstore index).</span><span class="sxs-lookup"><span data-stu-id="9c987-120">For more information on bulk loading, see [Bulk load into a clustered columnstore index](https://msdn.microsoft.com/en-us/library/dn935008.aspx#Bulk load into a clustered columnstore index).</span></span>

## <a name="how-toomonitor-rowgroup-quality"></a><span data-ttu-id="9c987-121">La qualité de rowgroup toomonitor</span><span class="sxs-lookup"><span data-stu-id="9c987-121">How toomonitor rowgroup quality</span></span>

<span data-ttu-id="9c987-122">Il existe une vue de gestion dynamique (sys.dm_pdw_nodes_db_column_store_row_group_physical_stats) qui expose des informations utiles telles que le nombre de lignes dans les rowgroups et hello motif pour la troncature s’il a été de découpage.</span><span class="sxs-lookup"><span data-stu-id="9c987-122">There is a DMV (sys.dm_pdw_nodes_db_column_store_row_group_physical_stats) that exposes useful information such as number of rows in rowgroups and hello reason for trimming if there was trimming.</span></span> <span data-ttu-id="9c987-123">Vous pouvez créer des ces informations de tooget DMV hello suivant vue comme un moyen pratique de tooquery sur la suppression du groupe de lignes.</span><span class="sxs-lookup"><span data-stu-id="9c987-123">You can create hello following view as a handy way tooquery this DMV tooget information on rowgroup trimming.</span></span>

```sql
create view dbo.vCS_rg_physical_stats
as 
with cte
as
(
select   tb.[name]                    AS [logical_table_name]
,        rg.[row_group_id]            AS [row_group_id]
,        rg.[state]                   AS [state]
,        rg.[state_desc]              AS [state_desc]
,        rg.[total_rows]              AS [total_rows]
,        rg.[trim_reason_desc]        AS trim_reason_desc
,        mp.[physical_name]           AS physical_name
FROM    sys.[schemas] sm
JOIN    sys.[tables] tb               ON  sm.[schema_id]          = tb.[schema_id]                             
JOIN    sys.[pdw_table_mappings] mp   ON  tb.[object_id]          = mp.[object_id]
JOIN    sys.[pdw_nodes_tables] nt     ON  nt.[name]               = mp.[physical_name]
JOIN    sys.[dm_pdw_nodes_db_column_store_row_group_physical_stats] rg      ON  rg.[object_id]     = nt.[object_id]
                                                                            AND rg.[pdw_node_id]   = nt.[pdw_node_id]
                                        AND rg.[distribution_id]    = nt.[distribution_id]                                          
)
select *
from cte;
```

<span data-ttu-id="9c987-124">Hello trim_reason_desc indique si le groupe de lignes hello a été tronqué (trim_reason_desc = NO_TRIM implique aucune suppression, et groupe de lignes est de qualité optimale).</span><span class="sxs-lookup"><span data-stu-id="9c987-124">hello trim_reason_desc tells whether hello rowgroup was trimmed(trim_reason_desc = NO_TRIM implies there was no trimming and row group is of optimal quality).</span></span> <span data-ttu-id="9c987-125">Hello raisons trim suivantes indiquent suppression prématurée de hello rowgroup :</span><span class="sxs-lookup"><span data-stu-id="9c987-125">hello following trim reasons indicate premature trimming of hello rowgroup:</span></span>
- <span data-ttu-id="9c987-126">Chargement en masse : C’est pourquoi découpage est utilisé lorsque le traitement entrant de hello de lignes pour la charge hello était inférieur à 1 million de lignes.</span><span class="sxs-lookup"><span data-stu-id="9c987-126">BULKLOAD: This trim reason is used when hello incoming batch of rows for hello load had less than 1 million rows.</span></span> <span data-ttu-id="9c987-127">moteur de Hello créera des groupes de lignes compressés si supérieur à 100 000 lignes insérées (comme tooinserting exécutée dans le magasin de delta hello) mais des jeux hello tooBULKLOAD de découpage raison.</span><span class="sxs-lookup"><span data-stu-id="9c987-127">hello engine will create compressed row groups if there are greater than 100,000 rows being inserted (as opposed tooinserting into hello delta store) but sets hello trim reason tooBULKLOAD.</span></span> <span data-ttu-id="9c987-128">Dans ce scénario, envisagez d’augmenter votre tooaccumulate de fenêtre de charge de traitement par lots plusieurs lignes.</span><span class="sxs-lookup"><span data-stu-id="9c987-128">In this scenario, consider increasing your batch load window tooaccumulate more rows.</span></span> <span data-ttu-id="9c987-129">En outre, réévaluez votre tooensure schéma partitionnement, il n’est pas trop granulaire que les groupes de lignes ne peut pas couvrir les limites de partition.</span><span class="sxs-lookup"><span data-stu-id="9c987-129">Also, reevaluate your partitioning scheme tooensure it is not too granular as row groups cannot span partition boundaries.</span></span>
- <span data-ttu-id="9c987-130">MEMORY_LIMITATION : toocreate des groupes de lignes avec 1 million de lignes, une certaine quantité de mémoire de travail est requis par le moteur de hello.</span><span class="sxs-lookup"><span data-stu-id="9c987-130">MEMORY_LIMITATION: toocreate row groups with 1 million rows, a certain amount of working memory is required by hello engine.</span></span> <span data-ttu-id="9c987-131">Lorsque la mémoire disponible de hello du chargement de session est inférieur au nombre requis de hello mémoire de travail, les groupes de lignes obtient supprimés prématurément.</span><span class="sxs-lookup"><span data-stu-id="9c987-131">When available memory of hello loading session is less than hello required working memory, row groups get prematurely trimmed.</span></span> <span data-ttu-id="9c987-132">Hello les sections suivantes explique comment tooestimate mémoire requise et allouer davantage de mémoire.</span><span class="sxs-lookup"><span data-stu-id="9c987-132">hello following sections explain how tooestimate memory required and allocate more memory.</span></span>
- <span data-ttu-id="9c987-133">DICTIONARY_SIZE : cette raison indique qu’un rowgroup a été découpé car il contenant au moins une colonne de chaîne avec des chaînes de cardinalité large et/ou haute.</span><span class="sxs-lookup"><span data-stu-id="9c987-133">DICTIONARY_SIZE: This trim reason indicates that rowgroup trimming occurred because there was at least one string column with wide and/or high cardinality strings.</span></span> <span data-ttu-id="9c987-134">taille de dictionnaire Hello est limitée too16 Mo en mémoire et une fois cette limite atteinte groupe de lignes hello est compressé.</span><span class="sxs-lookup"><span data-stu-id="9c987-134">hello dictionary size is limited too16 MB in memory and once this limit is reached hello row group is compressed.</span></span> <span data-ttu-id="9c987-135">Si vous n’exécutez pas dans ce cas, envisagez d’isoler les colonnes problématique hello dans une table distincte.</span><span class="sxs-lookup"><span data-stu-id="9c987-135">If you do run into this situation, consider isolating hello problematic column into a separate table.</span></span>

## <a name="how-tooestimate-memory-requirements"></a><span data-ttu-id="9c987-136">Comment tooestimate mémoire requise</span><span class="sxs-lookup"><span data-stu-id="9c987-136">How tooestimate memory requirements</span></span>

<!--
tooview an estimate of hello memory requirements toocompress a rowgroup of maximum size into a columnstore index, download and run hello view [dbo.vCS_mon_mem_grant](). This view shows hello size of hello memory grant that a rowgroup requires for compression in toohello columnstore.
-->

<span data-ttu-id="9c987-137">un rowgroup Hello maximale de mémoire requise toocompress est d’environ</span><span class="sxs-lookup"><span data-stu-id="9c987-137">hello maximum required memory toocompress one rowgroup is approximately</span></span>

- <span data-ttu-id="9c987-138">72 Mo +</span><span class="sxs-lookup"><span data-stu-id="9c987-138">72 MB +</span></span>
- <span data-ttu-id="9c987-139">\#lignes \*\#colonnes \* 8 octets +</span><span class="sxs-lookup"><span data-stu-id="9c987-139">\#rows \* \#columns \* 8 bytes +</span></span>
- <span data-ttu-id="9c987-140">\#lignes \*\#colonnes de chaîne courte \* 32 octets +</span><span class="sxs-lookup"><span data-stu-id="9c987-140">\#rows \* \#short-string-columns \* 32 bytes +</span></span>
- <span data-ttu-id="9c987-141">\#colonnes de chaîne longue \* 16 Mo pour le dictionnaire de compression</span><span class="sxs-lookup"><span data-stu-id="9c987-141">\#long-string-columns \* 16 MB for compression dictionary</span></span>

<span data-ttu-id="9c987-142">où les colonnes de chaîne courte utilisent des données de type chaîne <= 32 octets, et les colonnes de chaîne longueur utilisent des données de type chaîne > 32 octets.</span><span class="sxs-lookup"><span data-stu-id="9c987-142">where short-string-columns use string data types of <= 32 bytes and long-string-columns use string data types of > 32 bytes.</span></span>

<span data-ttu-id="9c987-143">Les chaînes longues sont compressés avec une méthode de compression conçue pour la compression de texte.</span><span class="sxs-lookup"><span data-stu-id="9c987-143">Long strings are compressed with a compression method designed for compressing text.</span></span> <span data-ttu-id="9c987-144">Cette méthode de compression utilise un *dictionnaire* toostore les modèles de texte.</span><span class="sxs-lookup"><span data-stu-id="9c987-144">This compression method uses a *dictionary* toostore text patterns.</span></span> <span data-ttu-id="9c987-145">taille maximale de Hello d’un dictionnaire est de 16 Mo.</span><span class="sxs-lookup"><span data-stu-id="9c987-145">hello maximum size of a dictionary is 16 MB.</span></span> <span data-ttu-id="9c987-146">Il est uniquement un dictionnaire pour chaque colonne de chaîne longue de hello rowgroup.</span><span class="sxs-lookup"><span data-stu-id="9c987-146">There is only one dictionary for each long string column in hello rowgroup.</span></span>

<span data-ttu-id="9c987-147">Pour une présentation détaillée des besoins en mémoire de columnstore, voir la vidéo [Mise à l’échelle d’Azure SQL Data Warehouse : configuration et instructions](https://myignite.microsoft.com/videos/14822).</span><span class="sxs-lookup"><span data-stu-id="9c987-147">For an in-depth discussion of columnstore memory requirements, see the video [Azure SQL Data Warehouse scaling: configuration and guidance](https://myignite.microsoft.com/videos/14822).</span></span>

## <a name="ways-tooreduce-memory-requirements"></a><span data-ttu-id="9c987-148">Besoins en mémoire façons tooreduce</span><span class="sxs-lookup"><span data-stu-id="9c987-148">Ways tooreduce memory requirements</span></span>

<span data-ttu-id="9c987-149">Utilisez hello suivant les exigences de mémoire techniques tooreduce hello pour compresser les rowgroups dans les index columnstore.</span><span class="sxs-lookup"><span data-stu-id="9c987-149">Use hello following techniques tooreduce hello memory requirements for compressing rowgroups into columnstore indexes.</span></span>

### <a name="use-fewer-columns"></a><span data-ttu-id="9c987-150">Utiliser moins de colonnes</span><span class="sxs-lookup"><span data-stu-id="9c987-150">Use fewer columns</span></span>
<span data-ttu-id="9c987-151">Si possible, concevez table hello avec moins de colonnes.</span><span class="sxs-lookup"><span data-stu-id="9c987-151">If possible, design hello table with fewer columns.</span></span> <span data-ttu-id="9c987-152">Quand un rowgroup est compressé dans hello columnstore, index columnstore de hello compresse chaque segment de colonne séparément.</span><span class="sxs-lookup"><span data-stu-id="9c987-152">When a rowgroup is compressed into hello columnstore, hello columnstore index compresses each column segment separately.</span></span> <span data-ttu-id="9c987-153">Par conséquent hello besoins en mémoire toocompress un rowgroup augmenter en tant que nombre hello de colonnes.</span><span class="sxs-lookup"><span data-stu-id="9c987-153">Therefore hello memory requirements toocompress a rowgroup increase as hello number of columns increases.</span></span>


### <a name="use-fewer-string-columns"></a><span data-ttu-id="9c987-154">Utiliser moins de colonnes de chaîne</span><span class="sxs-lookup"><span data-stu-id="9c987-154">Use fewer string columns</span></span>
<span data-ttu-id="9c987-155">Les colonnes de données de type chaîne nécessitent davantage de mémoire que les données de type nombre et date.</span><span class="sxs-lookup"><span data-stu-id="9c987-155">Columns of string data types require more memory than numeric and date data types.</span></span> <span data-ttu-id="9c987-156">tooreduce besoins en mémoire, envisagez de supprimer des colonnes de type chaîne à partir des tables de faits et en les plaçant dans les tables de dimension plus petites.</span><span class="sxs-lookup"><span data-stu-id="9c987-156">tooreduce memory requirements, consider removing string columns from fact tables and putting them in smaller dimension tables.</span></span>

<span data-ttu-id="9c987-157">Besoins en mémoire supplémentaires pour la compression de chaîne :</span><span class="sxs-lookup"><span data-stu-id="9c987-157">Additional memory requirements for string compression:</span></span>

- <span data-ttu-id="9c987-158">Types de données de chaîne des caractères de too32 peuvent nécessiter 32 octets supplémentaires par valeur.</span><span class="sxs-lookup"><span data-stu-id="9c987-158">String data types up too32 characters can require 32 additional bytes per value.</span></span>
- <span data-ttu-id="9c987-159">Les données de type chaîne comprenant plus de 32 caractères sont compressées à l’aide de méthodes de dictionnaire.</span><span class="sxs-lookup"><span data-stu-id="9c987-159">String data types with more than 32 characters are compressed using dictionary methods.</span></span>  <span data-ttu-id="9c987-160">Chaque colonne dans le groupe de lignes hello peut nécessiter la dictionnaire tooan supplémentaires 16 Mo toobuild hello.</span><span class="sxs-lookup"><span data-stu-id="9c987-160">Each column in hello rowgroup can require up tooan additional 16 MB toobuild hello dictionary.</span></span>

### <a name="avoid-over-partitioning"></a><span data-ttu-id="9c987-161">Éviter un partitionnement excessif</span><span class="sxs-lookup"><span data-stu-id="9c987-161">Avoid over-partitioning</span></span>

<span data-ttu-id="9c987-162">Les index columnstore créent un ou plusieurs rowgroups par partition.</span><span class="sxs-lookup"><span data-stu-id="9c987-162">Columnstore indexes create one or more rowgroups per partition.</span></span> <span data-ttu-id="9c987-163">Dans l’entrepôt de données SQL, nombre hello de partitions augmente rapidement, car les données de salutation sont distribuées et chaque point de distribution est partitionnée.</span><span class="sxs-lookup"><span data-stu-id="9c987-163">In SQL Data Warehouse, hello number of partitions grows quickly because hello data is distributed and each distribution is partitioned.</span></span> <span data-ttu-id="9c987-164">Si la table de hello a trop de partitions, il peut-être pas suffisamment rowgroups de hello toofill lignes.</span><span class="sxs-lookup"><span data-stu-id="9c987-164">If hello table has too many partitions, there might not be enough rows toofill hello rowgroups.</span></span> <span data-ttu-id="9c987-165">manque de Hello de lignes ne crée pas de sollicitation de la mémoire lors de la compression, mais elle entraîne toorowgroups que ne pas atteindre les meilleures performances des requêtes columnstore hello.</span><span class="sxs-lookup"><span data-stu-id="9c987-165">hello lack of rows does not create memory pressure during compression, but it leads toorowgroups that do not achieve hello best columnstore query performance.</span></span>

<span data-ttu-id="9c987-166">Une autre raison tooavoid remplacer le partitionnement est une mémoire système de traitement pour le chargement de lignes dans un index columnstore sur une table partitionnée.</span><span class="sxs-lookup"><span data-stu-id="9c987-166">Another reason tooavoid over-partitioning is there is a memory overhead for loading rows into a columnstore index on a partitioned table.</span></span> <span data-ttu-id="9c987-167">Lors d’un chargement, le nombre de partitions pourrait recevoir des lignes entrantes hello, qui sont conservées en mémoire jusqu'à ce que chaque partition possède suffisamment toobe lignes compressé.</span><span class="sxs-lookup"><span data-stu-id="9c987-167">During a load, many partitions could receive hello incoming rows, which are held in memory until each partition has enough rows toobe compressed.</span></span> <span data-ttu-id="9c987-168">Un trop grand nombre de partitions entraîne une sollicitation supplémentaire de la mémoire.</span><span class="sxs-lookup"><span data-stu-id="9c987-168">Having too many partitions creates additional memory pressure.</span></span>

### <a name="simplify-hello-load-query"></a><span data-ttu-id="9c987-169">Simplifiez la requête de charge hello</span><span class="sxs-lookup"><span data-stu-id="9c987-169">Simplify hello load query</span></span>

<span data-ttu-id="9c987-170">base de données Hello partage hello allocation de mémoire pour une requête parmi tous les opérateurs hello dans la requête de hello.</span><span class="sxs-lookup"><span data-stu-id="9c987-170">hello database shares hello memory grant for a query among all hello operators in hello query.</span></span> <span data-ttu-id="9c987-171">Lorsqu’une requête de charge contient des tris complexes et les jointures, mémoire hello disponible pour la compression est réduite.</span><span class="sxs-lookup"><span data-stu-id="9c987-171">When a load query has complex sorts and joins, hello memory available for compression is reduced.</span></span>

<span data-ttu-id="9c987-172">Concevoir hello charge requête toofocus uniquement lors du chargement de requête de hello.</span><span class="sxs-lookup"><span data-stu-id="9c987-172">Design hello load query toofocus only on loading hello query.</span></span> <span data-ttu-id="9c987-173">Si vous avez besoin de transformations toorun sur les données de salutation, exécutez-les distinct à partir de la requête de charge hello.</span><span class="sxs-lookup"><span data-stu-id="9c987-173">If you need toorun transformations on hello data, run them separate from hello load query.</span></span> <span data-ttu-id="9c987-174">Par exemple, stocker des données hello dans une table de segment de mémoire, exécuter des transformations de hello et chargez ensuite hello table intermédiaire dans un index columnstore hello.</span><span class="sxs-lookup"><span data-stu-id="9c987-174">For example, stage hello data in a heap table, run hello transformations, and then load hello staging table into hello columnstore index.</span></span> <span data-ttu-id="9c987-175">Vous pouvez également charger en premier les données hello et ensuite utiliser les données de salutation MPP système tootransform hello.</span><span class="sxs-lookup"><span data-stu-id="9c987-175">You can also load hello data first and then use hello MPP system tootransform hello data.</span></span>

### <a name="adjust-maxdop"></a><span data-ttu-id="9c987-176">Ajuster MAXDOP</span><span class="sxs-lookup"><span data-stu-id="9c987-176">Adjust MAXDOP</span></span>

<span data-ttu-id="9c987-177">Chaque point de distribution compresse les rowgroups dans columnstore hello en parallèle lorsque plusieurs cœurs de processeur est disponible par la distribution.</span><span class="sxs-lookup"><span data-stu-id="9c987-177">Each distribution compresses rowgroups into hello columnstore in parallel when there is more than one CPU core available per distribution.</span></span> <span data-ttu-id="9c987-178">parallélisme de Hello nécessite des ressources de mémoire supplémentaire, qui peuvent provoquer une sollicitation de la toomemory et de la suppression du groupe de lignes.</span><span class="sxs-lookup"><span data-stu-id="9c987-178">hello parallelism requires additional memory resources, which can lead toomemory pressure and rowgroup trimming.</span></span>

<span data-ttu-id="9c987-179">tooreduce la sollicitation de la mémoire, vous pouvez utiliser hello MAXDOP requête indicateur tooforce hello charge opération toorun en mode série au sein de chaque point de distribution.</span><span class="sxs-lookup"><span data-stu-id="9c987-179">tooreduce memory pressure, you can use hello MAXDOP query hint tooforce hello load operation toorun in serial mode within each distribution.</span></span>

```
CREATE TABLE MyFactSalesQuota
WITH (DISTRIBUTION = ROUND_ROBIN)
AS SELECT * FROM FactSalesQUota
OPTION (MAXDOP 1);
```

## <a name="ways-tooallocate-more-memory"></a><span data-ttu-id="9c987-180">Méthodes tooallocate plus de mémoire</span><span class="sxs-lookup"><span data-stu-id="9c987-180">Ways tooallocate more memory</span></span>

<span data-ttu-id="9c987-181">Classe de ressource utilisateur hello et de taille des DWU déterminent la quantité de mémoire est disponible pour une requête utilisateur.</span><span class="sxs-lookup"><span data-stu-id="9c987-181">DWU size and hello user resource class together determine how much memory is available for a user query.</span></span> <span data-ttu-id="9c987-182">allocation de mémoire de hello de tooincrease pour une requête de charge, vous pouvez augmenter le nombre de hello de Dwu ou augmenter la classe de ressource hello.</span><span class="sxs-lookup"><span data-stu-id="9c987-182">tooincrease hello memory grant for a load query, you can either increase hello number of DWUs or increase hello resource class.</span></span>

- <span data-ttu-id="9c987-183">tooincrease hello Dwu, consultez [comment faire évoluer performances ?](sql-data-warehouse-manage-compute-overview.md#scale-compute)</span><span class="sxs-lookup"><span data-stu-id="9c987-183">tooincrease hello DWUs, see [How do I scale performance?](sql-data-warehouse-manage-compute-overview.md#scale-compute)</span></span>
- <span data-ttu-id="9c987-184">classe de ressource toochange hello pour une requête, consultez [modifier un exemple de classe de ressource utilisateur](sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example).</span><span class="sxs-lookup"><span data-stu-id="9c987-184">toochange hello resource class for a query, see [Change a user resource class example](sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example).</span></span>

<span data-ttu-id="9c987-185">Par exemple, sur DWU 100, un utilisateur dans la classe de ressource hello smallrc peut utiliser 100 Mo de mémoire pour chaque point de distribution.</span><span class="sxs-lookup"><span data-stu-id="9c987-185">For example, on DWU 100 a user in hello smallrc resource class can use 100 MB of memory for each distribution.</span></span> <span data-ttu-id="9c987-186">Pour plus d’informations hello, consultez [l’accès concurrentiel dans SQL Data Warehouse](sql-data-warehouse-develop-concurrency.md).</span><span class="sxs-lookup"><span data-stu-id="9c987-186">For hello details, see [Concurrency in SQL Data Warehouse](sql-data-warehouse-develop-concurrency.md).</span></span>

<span data-ttu-id="9c987-187">Supposons que vous déterminez que vous avez besoin de 700 Mo de tailles de mémoire tooget rowgroup de haute qualité.</span><span class="sxs-lookup"><span data-stu-id="9c987-187">Suppose you determine that you need 700 MB of memory tooget high-quality rowgroup sizes.</span></span> <span data-ttu-id="9c987-188">Ces exemples montrent comment vous pouvez exécuter la requête de charge hello avec suffisamment de mémoire.</span><span class="sxs-lookup"><span data-stu-id="9c987-188">These examples show how you can run hello load query with enough memory.</span></span>

- <span data-ttu-id="9c987-189">En utilisant DWU 1000 et mediumrc, votre allocation de mémoire est de 800 Mo.</span><span class="sxs-lookup"><span data-stu-id="9c987-189">Using DWU 1000 and mediumrc, your memory grant is 800 MB</span></span>
- <span data-ttu-id="9c987-190">En utilisant DWU 600 et largerc, votre allocation de mémoire est de 800 Mo.</span><span class="sxs-lookup"><span data-stu-id="9c987-190">Using DWU 600 and largerc, your memory grant is 800 MB.</span></span>


## <a name="next-steps"></a><span data-ttu-id="9c987-191">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="9c987-191">Next steps</span></span>

<span data-ttu-id="9c987-192">toofind performances tooimprove manières dans l’entrepôt de données SQL, consultez hello [vue d’ensemble des performances](sql-data-warehouse-overview-manage-user-queries.md).</span><span class="sxs-lookup"><span data-stu-id="9c987-192">toofind more ways tooimprove performance in SQL Data Warehouse, see hello [Performance overview](sql-data-warehouse-overview-manage-user-queries.md).</span></span>

<!--Image references-->

<!--Article references-->


<!--MSDN references-->

<!--Other Web references-->
