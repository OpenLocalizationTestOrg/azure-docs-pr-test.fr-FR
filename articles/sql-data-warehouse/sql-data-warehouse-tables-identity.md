---
title: "aaaCreate des clés de substitution à l’aide d’identité | Documents Microsoft"
description: "Découvrez comment clés de substitution de toocreate toouse identité sur les tables."
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: faa1034d-314c-4f9d-af81-f5a9aedf33e4
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 06/13/2017
ms.author: jrj;barbkess
ms.openlocfilehash: 502cdd2b510b229b2a19c1f78b11862a7386ae3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-surrogate-keys-by-using-identity"></a><span data-ttu-id="e50c8-103">Créer des clés de substitution à l’aide d’IDENTITY</span><span class="sxs-lookup"><span data-stu-id="e50c8-103">Create surrogate keys by using IDENTITY</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="e50c8-104">[Vue d’ensemble][Overview]</span><span class="sxs-lookup"><span data-stu-id="e50c8-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="e50c8-105">[Types de données][Data Types]</span><span class="sxs-lookup"><span data-stu-id="e50c8-105">[Data types][Data Types]</span></span>
> * <span data-ttu-id="e50c8-106">[Distribuer][Distribute]</span><span class="sxs-lookup"><span data-stu-id="e50c8-106">[Distribute][Distribute]</span></span>
> * <span data-ttu-id="e50c8-107">[Index][Index]</span><span class="sxs-lookup"><span data-stu-id="e50c8-107">[Index][Index]</span></span>
> * <span data-ttu-id="e50c8-108">[Partition][Partition]</span><span class="sxs-lookup"><span data-stu-id="e50c8-108">[Partition][Partition]</span></span>
> * <span data-ttu-id="e50c8-109">[Statistiques][Statistics]</span><span class="sxs-lookup"><span data-stu-id="e50c8-109">[Statistics][Statistics]</span></span>
> * <span data-ttu-id="e50c8-110">[Temporaire][Temporary]</span><span class="sxs-lookup"><span data-stu-id="e50c8-110">[Temporary][Temporary]</span></span>
> * <span data-ttu-id="e50c8-111">[Identité][Identity]</span><span class="sxs-lookup"><span data-stu-id="e50c8-111">[Identity][Identity]</span></span>
> 
> 

<span data-ttu-id="e50c8-112">Nombreux modélisateurs de données tels que les clés de substitution toocreate sur leurs tables lorsqu’ils conçoivent des modèles de l’entrepôt de données.</span><span class="sxs-lookup"><span data-stu-id="e50c8-112">Many data modelers like toocreate surrogate keys on their tables when they design data warehouse models.</span></span> <span data-ttu-id="e50c8-113">Vous pouvez utiliser tooachieve de propriété d’identité hello cet objectif simple et efficace sans affecter les performances de chargement.</span><span class="sxs-lookup"><span data-stu-id="e50c8-113">You can use hello IDENTITY property tooachieve this goal simply and effectively without affecting load performance.</span></span> 

## <a name="get-started-with-identity"></a><span data-ttu-id="e50c8-114">Prise en main d’IDENTITY</span><span class="sxs-lookup"><span data-stu-id="e50c8-114">Get started with IDENTITY</span></span>
<span data-ttu-id="e50c8-115">Vous pouvez définir un tableau comme propriété d’identité hello lorsque vous créez hello table à l’aide de la syntaxe similaire toohello après l’instruction :</span><span class="sxs-lookup"><span data-stu-id="e50c8-115">You can define a table as having hello IDENTITY property when you first create hello table by using syntax that is similar toohello following statement:</span></span>

```sql
CREATE TABLE dbo.T1
(   C1 INT IDENTITY(1,1) NOT NULL
,   C2 INT NULL
)
WITH
(   DISTRIBUTION = HASH(C2)
,   CLUSTERED COLUMNSTORE INDEX
)
;
```

<span data-ttu-id="e50c8-116">Vous pouvez ensuite utiliser `INSERT..SELECT` table de hello toopopulate.</span><span class="sxs-lookup"><span data-stu-id="e50c8-116">You can then use `INSERT..SELECT` toopopulate hello table.</span></span>

## <a name="behavior"></a><span data-ttu-id="e50c8-117">Comportement</span><span class="sxs-lookup"><span data-stu-id="e50c8-117">Behavior</span></span>
<span data-ttu-id="e50c8-118">Hello, propriété d’identité est conçue tooscale out entre toutes les distributions hello dans l’entrepôt de données hello sans affecter les performances de chargement.</span><span class="sxs-lookup"><span data-stu-id="e50c8-118">hello IDENTITY property is designed tooscale out across all hello distributions in hello data warehouse without affecting load performance.</span></span> <span data-ttu-id="e50c8-119">Par conséquent, l’implémentation hello d’identité est adaptée pour atteindre ces objectifs.</span><span class="sxs-lookup"><span data-stu-id="e50c8-119">Therefore, hello implementation of IDENTITY is oriented toward achieving these goals.</span></span> <span data-ttu-id="e50c8-120">Cette section met en évidence les nuances hello de hello implémentation toohelp vous comprendre de façon plus complète.</span><span class="sxs-lookup"><span data-stu-id="e50c8-120">This section highlights hello nuances of hello implementation toohelp you understand them more fully.</span></span>  

### <a name="allocation-of-values"></a><span data-ttu-id="e50c8-121">Allocation de valeurs</span><span class="sxs-lookup"><span data-stu-id="e50c8-121">Allocation of values</span></span>
<span data-ttu-id="e50c8-122">Hello propriété IDENTITY ne garantit pas l’ordre hello dans le hello les valeurs de substitution sont allouées, qui reflète le comportement hello de SQL Server et la base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="e50c8-122">hello IDENTITY property doesn't guarantee hello order in which hello surrogate values are allocated, which reflects hello behavior of SQL Server and Azure SQL Database.</span></span> <span data-ttu-id="e50c8-123">Toutefois, dans l’entrepôt de données SQL Azure, absence de hello d’une garantie plus marquée.</span><span class="sxs-lookup"><span data-stu-id="e50c8-123">However, in Azure SQL Data Warehouse, hello absence of a guarantee is more pronounced.</span></span> 

<span data-ttu-id="e50c8-124">Bonjour à l’exemple suivant est une illustration :</span><span class="sxs-lookup"><span data-stu-id="e50c8-124">hello following example is an illustration:</span></span>

```sql
CREATE TABLE dbo.T1
(   C1 INT IDENTITY(1,1)    NOT NULL
,   C2 VARCHAR(30)              NULL
)
WITH
(   DISTRIBUTION = HASH(C2)
,   CLUSTERED COLUMNSTORE INDEX
)
;

INSERT INTO dbo.T1
VALUES (NULL);

INSERT INTO dbo.T1
VALUES (NULL);

SELECT *
FROM dbo.T1;

DBCC PDW_SHOWSPACEUSED('dbo.T1');
```

<span data-ttu-id="e50c8-125">Bonjour précédent exemple, deux lignes étant récupérées de distribution 1.</span><span class="sxs-lookup"><span data-stu-id="e50c8-125">In hello preceding example, two rows landed in distribution 1.</span></span> <span data-ttu-id="e50c8-126">première ligne de Hello a la valeur de substitution de hello de 1 dans la colonne `C1`, et hello deuxième ligne a la valeur de substitution hello 61.</span><span class="sxs-lookup"><span data-stu-id="e50c8-126">hello first row has hello surrogate value of 1 in column `C1`, and hello second row has hello surrogate value of 61.</span></span> <span data-ttu-id="e50c8-127">Ces deux valeurs ont été créés par hello propriété d’identité.</span><span class="sxs-lookup"><span data-stu-id="e50c8-127">Both of these values were generated by hello IDENTITY property.</span></span> <span data-ttu-id="e50c8-128">Toutefois, l’allocation des valeurs de hello hello n’est pas contigue.</span><span class="sxs-lookup"><span data-stu-id="e50c8-128">However, hello allocation of hello values is not contiguous.</span></span> <span data-ttu-id="e50c8-129">Ce comportement est normal.</span><span class="sxs-lookup"><span data-stu-id="e50c8-129">This behavior is by design.</span></span>

### <a name="skewed-data"></a><span data-ttu-id="e50c8-130">Données décalées</span><span class="sxs-lookup"><span data-stu-id="e50c8-130">Skewed data</span></span> 
<span data-ttu-id="e50c8-131">plage de Hello de valeurs pour le type de données hello sont répartis uniformément entre les distributions de hello.</span><span class="sxs-lookup"><span data-stu-id="e50c8-131">hello range of values for hello data type are spread evenly across hello distributions.</span></span> <span data-ttu-id="e50c8-132">Si une table distribuée est données rétrécies, puis hello plage de valeurs de type de données toohello disponibles peut être épuisée prématurément.</span><span class="sxs-lookup"><span data-stu-id="e50c8-132">If a distributed table suffers from skewed data, then hello range of values available toohello datatype can be exhausted prematurely.</span></span> <span data-ttu-id="e50c8-133">Par exemple, si toutes les données hello se termine dans une seule distribution, puis table de hello a effectivement accès tooonly-un sixième de valeurs hello hello du type de données.</span><span class="sxs-lookup"><span data-stu-id="e50c8-133">For example, if all hello data ends up in a single distribution, then effectively hello table has access tooonly one-sixtieth of hello values of hello data type.</span></span> <span data-ttu-id="e50c8-134">Pour cette raison, hello propriété d’identité est limitée trop`INT` et `BIGINT` uniquement des types de données.</span><span class="sxs-lookup"><span data-stu-id="e50c8-134">For this reason, hello IDENTITY property is limited too`INT` and `BIGINT` data types only.</span></span>

### <a name="selectinto"></a><span data-ttu-id="e50c8-135">SELECT .. INTO</span><span class="sxs-lookup"><span data-stu-id="e50c8-135">SELECT..INTO</span></span>
<span data-ttu-id="e50c8-136">Lorsqu’une colonne d’identité existante est sélectionnée dans une nouvelle table, hello nouvelle colonne hérite de propriété d’identité hello, sauf si une des hello conditions suivantes est vraie :</span><span class="sxs-lookup"><span data-stu-id="e50c8-136">When an existing IDENTITY column is selected into a new table, hello new column inherits hello IDENTITY property, unless one of hello following conditions is true:</span></span>
- <span data-ttu-id="e50c8-137">instruction SELECT de Hello contient une jointure.</span><span class="sxs-lookup"><span data-stu-id="e50c8-137">hello SELECT statement contains a join.</span></span>
- <span data-ttu-id="e50c8-138">Plusieurs instructions SELECT sont jointes à l’aide d’UNION.</span><span class="sxs-lookup"><span data-stu-id="e50c8-138">Multiple SELECT statements are joined by using UNION.</span></span>
- <span data-ttu-id="e50c8-139">colonne d’identité Hello est répertorié plusieurs fois dans la liste de sélection hello.</span><span class="sxs-lookup"><span data-stu-id="e50c8-139">hello IDENTITY column is listed more than one time in hello SELECT list.</span></span>
- <span data-ttu-id="e50c8-140">colonne d’identité Hello fait partie d’une expression.</span><span class="sxs-lookup"><span data-stu-id="e50c8-140">hello IDENTITY column is part of an expression.</span></span>
    
<span data-ttu-id="e50c8-141">Si l’une de ces conditions est true, les colonnes hello sont créé NOT NULL au lieu d’hériter de la propriété IDENTITY hello.</span><span class="sxs-lookup"><span data-stu-id="e50c8-141">If any one of these conditions is true, hello column is created NOT NULL instead of inheriting hello IDENTITY property.</span></span>

### <a name="create-table-as-select"></a><span data-ttu-id="e50c8-142">CREATE TABLE AS SELECT</span><span class="sxs-lookup"><span data-stu-id="e50c8-142">CREATE TABLE AS SELECT</span></span>
<span data-ttu-id="e50c8-143">CREATE TABLE AS sélectionnez (SACT) suit hello même comportement SQL Server est documentée pour sélectionnez... DANS.</span><span class="sxs-lookup"><span data-stu-id="e50c8-143">CREATE TABLE AS SELECT (CTAS) follows hello same SQL Server behavior that's documented for SELECT..INTO.</span></span> <span data-ttu-id="e50c8-144">Toutefois, vous ne pouvez pas spécifier une propriété d’identité dans la définition de colonne hello Hello `CREATE TABLE` dans le cadre de l’instruction de hello.</span><span class="sxs-lookup"><span data-stu-id="e50c8-144">However, you can't specify an IDENTITY property in hello column definition of hello `CREATE TABLE` part of hello statement.</span></span> <span data-ttu-id="e50c8-145">Vous ne pouvez pas utiliser fonction d’identité hello Bonjour `SELECT` dans le cadre du hello SACT.</span><span class="sxs-lookup"><span data-stu-id="e50c8-145">You also can't use hello IDENTITY function in hello `SELECT` part of hello CTAS.</span></span> <span data-ttu-id="e50c8-146">toopopulate une table, vous devez toouse `CREATE TABLE` suivi de la table de hello toodefine `INSERT..SELECT` toopopulate il.</span><span class="sxs-lookup"><span data-stu-id="e50c8-146">toopopulate a table, you need toouse `CREATE TABLE` toodefine hello table followed by `INSERT..SELECT` toopopulate it.</span></span>

## <a name="explicitly-insert-values-into-an-identity-column"></a><span data-ttu-id="e50c8-147">Insérer explicitement des valeurs dans une colonne IDENTITY</span><span class="sxs-lookup"><span data-stu-id="e50c8-147">Explicitly insert values into an IDENTITY column</span></span> 
<span data-ttu-id="e50c8-148">SQL Data Warehouse prend en charge la syntaxe `SET IDENTITY_INSERT <your table> ON|OFF`.</span><span class="sxs-lookup"><span data-stu-id="e50c8-148">SQL Data Warehouse supports `SET IDENTITY_INSERT <your table> ON|OFF` syntax.</span></span> <span data-ttu-id="e50c8-149">Vous pouvez utiliser ce syntaxe tooexplicitly insérer les valeurs dans la colonne d’identité hello.</span><span class="sxs-lookup"><span data-stu-id="e50c8-149">You can use this syntax tooexplicitly insert values into hello IDENTITY column.</span></span>

<span data-ttu-id="e50c8-150">Nombreux modélisateurs de données comme négatif prédéfinis de toouse des valeurs pour certaines lignes dans les dimensions.</span><span class="sxs-lookup"><span data-stu-id="e50c8-150">Many data modelers like toouse predefined negative values for certain rows in their dimensions.</span></span> <span data-ttu-id="e50c8-151">Il est un exemple hello -1 ou la ligne « membre inconnu ».</span><span class="sxs-lookup"><span data-stu-id="e50c8-151">An example is hello -1 or "unknown member" row.</span></span> 

<span data-ttu-id="e50c8-152">accéder au script Hello suivant montre comment tooexplicitly ajouter cette ligne à l’aide de SET IDENTITY_INSERT :</span><span class="sxs-lookup"><span data-stu-id="e50c8-152">hello next script shows how tooexplicitly add this row by using SET IDENTITY_INSERT:</span></span>

```sql
SET IDENTITY_INSERT dbo.T1 ON;

INSERT INTO dbo.T1
(   C1
,   C2
)
VALUES (-1,'UNKNOWN')
;

SET IDENTITY_INSERT dbo.T1 OFF;

SELECT  *
FROM    dbo.T1
;
```    

## <a name="load-data-into-a-table-with-identity"></a><span data-ttu-id="e50c8-153">Charger des données dans une table avec IDENTITY</span><span class="sxs-lookup"><span data-stu-id="e50c8-153">Load data into a table with IDENTITY</span></span>

<span data-ttu-id="e50c8-154">Hello la présence de hello propriété d’identité a un code de chargement de données tooyour implications.</span><span class="sxs-lookup"><span data-stu-id="e50c8-154">hello presence of hello IDENTITY property has some implications tooyour data-loading code.</span></span> <span data-ttu-id="e50c8-155">Cette section met en évidence certains modèles de base pour charger des données dans les tables à l’aide d’IDENTITY.</span><span class="sxs-lookup"><span data-stu-id="e50c8-155">This section highlights some basic patterns for loading data into tables by using IDENTITY.</span></span> 

### <a name="load-data-with-polybase"></a><span data-ttu-id="e50c8-156">Charger des données avec PolyBase</span><span class="sxs-lookup"><span data-stu-id="e50c8-156">Load data with PolyBase</span></span>
<span data-ttu-id="e50c8-157">données tooload dans une table et générer une clé de substitution à l’aide d’identité, créer la table de hello et utiliser l’instruction INSERT... SELECT ou INSERT... VALEURS tooperform hello charge.</span><span class="sxs-lookup"><span data-stu-id="e50c8-157">tooload data into a table and generate a surrogate key by using IDENTITY, create hello table and then use INSERT..SELECT or INSERT..VALUES tooperform hello load.</span></span>

<span data-ttu-id="e50c8-158">Hello exemple suivant met en évidence du modèle de base hello :</span><span class="sxs-lookup"><span data-stu-id="e50c8-158">hello following example highlights hello basic pattern:</span></span>
 
```sql
--CREATE TABLE with IDENTITY
CREATE TABLE dbo.T1
(   C1 INT IDENTITY(1,1)
,   C2 VARCHAR(30)
)
WITH
(   DISTRIBUTION = HASH(C2)
,   CLUSTERED COLUMNSTORE INDEX
)
;

--Use INSERT..SELECT toopopulate hello table from an external table
INSERT INTO dbo.T1
(C2)
SELECT  C2
FROM    ext.T1
;

SELECT  *
FROM    dbo.T1
;

DBCC PDW_SHOWSPACEUSED('dbo.T1');
```

> [!NOTE] 
> <span data-ttu-id="e50c8-159">Il n’est pas possible de toouse `CREATE TABLE AS SELECT` actuellement lors du chargement des données dans une table comportant une colonne d’identité.</span><span class="sxs-lookup"><span data-stu-id="e50c8-159">It's not possible toouse `CREATE TABLE AS SELECT` currently when loading data into a table with an IDENTITY column.</span></span>
> 

<span data-ttu-id="e50c8-160">Pour plus d’informations sur le chargement de données à l’aide d’outil de programme (BCP) copie hello en bloc, consultez hello suivant des articles :</span><span class="sxs-lookup"><span data-stu-id="e50c8-160">For more information on loading data by using hello bulk copy program (BCP) tool, see hello following articles:</span></span>

- <span data-ttu-id="e50c8-161">[Charger avec PolyBase][]</span><span class="sxs-lookup"><span data-stu-id="e50c8-161">[Load with PolyBase][]</span></span>
- <span data-ttu-id="e50c8-162">[Meilleures pratiques pour PolyBase][]</span><span class="sxs-lookup"><span data-stu-id="e50c8-162">[PolyBase best practices][]</span></span>

### <a name="load-data-with-bcp"></a><span data-ttu-id="e50c8-163">Chargement des données avec BCP</span><span class="sxs-lookup"><span data-stu-id="e50c8-163">Load data with BCP</span></span>
<span data-ttu-id="e50c8-164">BCP est un outil de ligne de commande que vous pouvez utiliser les données de tooload dans SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="e50c8-164">BCP is a command-line tool that you can use tooload data into SQL Data Warehouse.</span></span> <span data-ttu-id="e50c8-165">Un de ses paramètres (-E) contrôles hello le comportement de l’utilitaire BCP lors du chargement des données dans une table avec une colonne d’identité.</span><span class="sxs-lookup"><span data-stu-id="e50c8-165">One of its parameters (-E) controls hello behavior of BCP when loading data into a table with an IDENTITY column.</span></span> 

<span data-ttu-id="e50c8-166">Si -E est spécifiée, les valeurs hello stockées dans le fichier d’entrée de hello pour la colonne de hello avec l’identité sont conservés.</span><span class="sxs-lookup"><span data-stu-id="e50c8-166">When -E is specified, hello values held in hello input file for hello column with IDENTITY are retained.</span></span> <span data-ttu-id="e50c8-167">Si -E est *pas* spécifié, les valeurs hello dans cette colonne sont ignorées.</span><span class="sxs-lookup"><span data-stu-id="e50c8-167">If -E is *not* specified, then hello values in this column are ignored.</span></span> <span data-ttu-id="e50c8-168">Si la colonne d’identité hello n’est pas inclus, puis les données de salutation sont chargées normalement.</span><span class="sxs-lookup"><span data-stu-id="e50c8-168">If hello identity column is not included, then hello data is loaded as normal.</span></span> <span data-ttu-id="e50c8-169">les valeurs Hello sont générées en fonction de stratégie de toohello incrément et la valeur initiale de la propriété de hello.</span><span class="sxs-lookup"><span data-stu-id="e50c8-169">hello values are generated according toohello increment and seed policy of hello property.</span></span>

<span data-ttu-id="e50c8-170">Pour plus d’informations sur le chargement de données à l’aide de BCP, consultez hello suivant des articles :</span><span class="sxs-lookup"><span data-stu-id="e50c8-170">For more information on loading data by using BCP, see hello following articles:</span></span>

- <span data-ttu-id="e50c8-171">[Charger avec BCP][]</span><span class="sxs-lookup"><span data-stu-id="e50c8-171">[Load with BCP][]</span></span>
- <span data-ttu-id="e50c8-172">[BCP dans MSDN][]</span><span class="sxs-lookup"><span data-stu-id="e50c8-172">[BCP in MSDN][]</span></span>

## <a name="catalog-views"></a><span data-ttu-id="e50c8-173">Affichages catalogue</span><span class="sxs-lookup"><span data-stu-id="e50c8-173">Catalog views</span></span>
<span data-ttu-id="e50c8-174">Entrepôt de données SQL prend en charge hello `sys.identity_columns` vue de catalogue.</span><span class="sxs-lookup"><span data-stu-id="e50c8-174">SQL Data Warehouse supports hello `sys.identity_columns` catalog view.</span></span> <span data-ttu-id="e50c8-175">Cette vue peut être utilisé tooidentify une colonne ayant la propriété d’identité hello.</span><span class="sxs-lookup"><span data-stu-id="e50c8-175">This view can be used tooidentify a column that has hello IDENTITY property.</span></span>

<span data-ttu-id="e50c8-176">toohelp vous mieux le schéma de base de données hello, cet exemple montre comment toointegrate `sys.identity_columns` avec d’autres vues de catalogue système :</span><span class="sxs-lookup"><span data-stu-id="e50c8-176">toohelp you better understand hello database schema, this example shows how toointegrate `sys.identity_columns` with other system catalog views:</span></span>

```sql
SELECT  sm.name
,       tb.name
,       co.name
,       CASE WHEN ic.column_id IS NOT NULL
             THEN 1
        ELSE 0
        END AS is_identity 
FROM        sys.schemas AS sm
JOIN        sys.tables  AS tb           ON  sm.schema_id = tb.schema_id
JOIN        sys.columns AS co           ON  tb.object_id = co.object_id
LEFT JOIN   sys.identity_columns AS ic  ON  co.object_id = ic.object_id
                                        AND co.column_id = ic.column_id
WHERE   sm.name = 'dbo'
AND     tb.name = 'T1'
;
```

## <a name="limitations"></a><span data-ttu-id="e50c8-177">Limites</span><span class="sxs-lookup"><span data-stu-id="e50c8-177">Limitations</span></span>
<span data-ttu-id="e50c8-178">Hello, propriété d’identité ne peut pas être utilisée dans hello les scénarios suivants :</span><span class="sxs-lookup"><span data-stu-id="e50c8-178">hello IDENTITY property can't be used in hello following scenarios:</span></span>
- <span data-ttu-id="e50c8-179">Où le type de données de colonne hello n’est pas INT ou BIGINT</span><span class="sxs-lookup"><span data-stu-id="e50c8-179">Where hello column data type is not INT or BIGINT</span></span>
- <span data-ttu-id="e50c8-180">Où hello colonne est également hello distribution clé</span><span class="sxs-lookup"><span data-stu-id="e50c8-180">Where hello column is also hello distribution key</span></span>
- <span data-ttu-id="e50c8-181">Où la table de hello est une table externe</span><span class="sxs-lookup"><span data-stu-id="e50c8-181">Where hello table is an external table</span></span> 

<span data-ttu-id="e50c8-182">Hello suivant des fonctions connexes n’est pas pris en charge dans SQL Data Warehouse :</span><span class="sxs-lookup"><span data-stu-id="e50c8-182">hello following related functions are not supported in SQL Data Warehouse:</span></span>

- <span data-ttu-id="e50c8-183">[IDENTITY()][]</span><span class="sxs-lookup"><span data-stu-id="e50c8-183">[IDENTITY()][]</span></span>
- <span data-ttu-id="e50c8-184">[@@IDENTITY][]</span><span class="sxs-lookup"><span data-stu-id="e50c8-184">[@@IDENTITY][]</span></span>
- <span data-ttu-id="e50c8-185">[SCOPE_IDENTITY][]</span><span class="sxs-lookup"><span data-stu-id="e50c8-185">[SCOPE_IDENTITY][]</span></span>
- <span data-ttu-id="e50c8-186">[IDENT_CURRENT][]</span><span class="sxs-lookup"><span data-stu-id="e50c8-186">[IDENT_CURRENT][]</span></span>
- <span data-ttu-id="e50c8-187">[IDENT_INCR][]</span><span class="sxs-lookup"><span data-stu-id="e50c8-187">[IDENT_INCR][]</span></span>
- <span data-ttu-id="e50c8-188">[IDENT_SEED][]</span><span class="sxs-lookup"><span data-stu-id="e50c8-188">[IDENT_SEED][]</span></span>
- <span data-ttu-id="e50c8-189">[DBCC CHECK_IDENT()][]</span><span class="sxs-lookup"><span data-stu-id="e50c8-189">[DBCC CHECK_IDENT()][]</span></span>

## <a name="tasks"></a><span data-ttu-id="e50c8-190">Tâches</span><span class="sxs-lookup"><span data-stu-id="e50c8-190">Tasks</span></span>

<span data-ttu-id="e50c8-191">Cette section fournit un exemple de code vous pouvez utiliser des tâches courantes de tooperform lorsque vous travaillez avec des colonnes d’identité.</span><span class="sxs-lookup"><span data-stu-id="e50c8-191">This section provides some sample code you can use tooperform common tasks when you work with IDENTITY columns.</span></span>

> [!NOTE] 
> <span data-ttu-id="e50c8-192">Colonne C1 est hello identité Bonjour toutes les tâches suivantes.</span><span class="sxs-lookup"><span data-stu-id="e50c8-192">Column C1 is hello IDENTITY in all hello following tasks.</span></span>
> 
 
### <a name="find-hello-highest-allocated-value-for-a-table"></a><span data-ttu-id="e50c8-193">Rechercher la valeur de la plus élevée de hello allouée pour une table</span><span class="sxs-lookup"><span data-stu-id="e50c8-193">Find hello highest allocated value for a table</span></span>
<span data-ttu-id="e50c8-194">Hello d’utilisation `MAX()` toodetermine hello valeur la plus élevée allouée pour une table distribuée de fonction :</span><span class="sxs-lookup"><span data-stu-id="e50c8-194">Use hello `MAX()` function toodetermine hello highest value allocated for a distributed table:</span></span>

```sql
SELECT  MAX(C1)
FROM    dbo.T1
``` 

### <a name="find-hello-seed-and-increment-for-hello-identity-property"></a><span data-ttu-id="e50c8-195">Recherchez hello départ et incrément hello propriété d’identité</span><span class="sxs-lookup"><span data-stu-id="e50c8-195">Find hello seed and increment for hello IDENTITY property</span></span>
<span data-ttu-id="e50c8-196">Vous pouvez utiliser hello catalogue vues toodiscover hello incrément et la valeur initiale configuration valeurs d’identité pour une table à l’aide de hello suivant la requête :</span><span class="sxs-lookup"><span data-stu-id="e50c8-196">You can use hello catalog views toodiscover hello identity increment and seed configuration values for a table by using hello following query:</span></span> 

```sql
SELECT  sm.name
,       tb.name
,       co.name
,       ic.seed_value
,       ic.increment_value 
FROM        sys.schemas AS sm
JOIN        sys.tables  AS tb           ON  sm.schema_id = tb.schema_id
JOIN        sys.columns AS co           ON  tb.object_id = co.object_id
JOIN        sys.identity_columns AS ic  ON  co.object_id = ic.object_id
                                        AND co.column_id = ic.column_id
WHERE   sm.name = 'dbo'
AND     tb.name = 'T1'
;
```

## <a name="next-steps"></a><span data-ttu-id="e50c8-197">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e50c8-197">Next steps</span></span>

* <span data-ttu-id="e50c8-198">toolearn plus sur le développement des tables, consultez [vue d’ensemble de la Table][Overview], [des types de données de Table][Data Types], [distribuer une table] [ Distribute], [Une table d’index][Index], [partitionner une table][Partition], et [ Tables temporaires][Temporary].</span><span class="sxs-lookup"><span data-stu-id="e50c8-198">toolearn more about developing tables, see [Table overview][Overview], [Table data types][Data Types], [Distribute a table][Distribute], [Index a table][Index], [Partition a table][Partition], and [Temporary tables][Temporary].</span></span> 
* <span data-ttu-id="e50c8-199">Pour plus d’informations sur les bonnes pratiques, consultez [Bonnes pratiques pour SQL Data Warehouse][SQL Data Warehouse Best Practices].</span><span class="sxs-lookup"><span data-stu-id="e50c8-199">For more information about best practices, see [SQL Data Warehouse best practices][SQL Data Warehouse Best Practices].</span></span>  

<!--Image references-->

<!--Article references-->
[Overview]: ./sql-data-warehouse-tables-overview.md
[Data Types]: ./sql-data-warehouse-tables-data-types.md
[Distribute]: ./sql-data-warehouse-tables-distribute.md
[Index]: ./sql-data-warehouse-tables-index.md
[Partition]: ./sql-data-warehouse-tables-partition.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md
[Temporary]: ./sql-data-warehouse-tables-temporary.md
[Identity]: ./sql-data-warehouse-tables-identity.md
[SQL Data Warehouse Best Practices]: ./sql-data-warehouse-best-practices.md

[Charger avec BCP]: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-load-with-bcp/
[Charger avec PolyBase]: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-load-from-azure-blob-storage-with-polybase/
[Meilleures pratiques pour PolyBase]: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-load-polybase-guide/


<!--MSDN references-->
[Identity property]: https://msdn.microsoft.com/library/ms186775.aspx
[sys.identity_columns]: https://msdn.microsoft.com/library/ms187334.aspx
[IDENTITY()]: https://msdn.microsoft.com/library/ms189838.aspx
[@@IDENTITY]: https://msdn.microsoft.com/library/ms187342.aspx
[SCOPE_IDENTITY]: https://msdn.microsoft.com/library/ms190315.aspx
[IDENT_CURRENT]: https://msdn.microsoft.com/library/ms175098.aspx
[IDENT_INCR]: https://msdn.microsoft.com/library/ms189795.aspx
[IDENT_SEED]: https://msdn.microsoft.com/library/ms189834.aspx
[DBCC CHECK_IDENT()]: https://msdn.microsoft.com/library/ms176057.aspx

[BCP dans MSDN]: https://msdn.microsoft.com/library/ms162802.aspx
  

<!--Other Web references-->  
