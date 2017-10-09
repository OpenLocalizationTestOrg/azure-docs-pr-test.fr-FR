---
title: "aaaGuide pour l’utilisation de PolyBase dans SQL Data Warehouse | Documents Microsoft"
description: "Instructions et recommandations relatives à l'utilisation de PolyBase dans les scénarios SQL Data Warehouse."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: barbkess
editor: 
ms.assetid: 4757fce1-96b3-48ea-8a51-be1385705f9f
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 6/5/2016
ms.custom: loading
ms.author: cakarst;barbkess
ms.openlocfilehash: b05e4c5d528f2fe1c60d6855b5333065f0c908ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="guide-for-using-polybase-in-sql-data-warehouse"></a><span data-ttu-id="55f01-103">Guide d'utilisation de PolyBase dans SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="55f01-103">Guide for using PolyBase in SQL Data Warehouse</span></span>
<span data-ttu-id="55f01-104">Ce guide fournit des informations pratiques pour l'utilisation de PolyBase dans SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="55f01-104">This guide gives practical information for using PolyBase in SQL Data Warehouse.</span></span>

<span data-ttu-id="55f01-105">tooget démarré, consultez hello [charger des données avec PolyBase] [ Load data with PolyBase] didacticiel.</span><span class="sxs-lookup"><span data-stu-id="55f01-105">tooget started, see hello [Load data with PolyBase][Load data with PolyBase] tutorial.</span></span>

## <a name="rotating-storage-keys"></a><span data-ttu-id="55f01-106">Rotation des clés de stockage</span><span class="sxs-lookup"><span data-stu-id="55f01-106">Rotating storage keys</span></span>
<span data-ttu-id="55f01-107">À partir de tootime de temps, vous devez le stockage blob tooyour clé toochange hello accès pour des raisons de sécurité.</span><span class="sxs-lookup"><span data-stu-id="55f01-107">From time tootime you will want toochange hello access key tooyour blob storage for security reasons.</span></span>

<span data-ttu-id="55f01-108">Bonjour tooperform de façon plus élégante que cette tâche est toofollow un processus appelé « rotation des clés de hello ».</span><span class="sxs-lookup"><span data-stu-id="55f01-108">hello most elegant way tooperform this task is toofollow a process known as "rotating hello keys".</span></span> <span data-ttu-id="55f01-109">Vous avez peut-être remarqué que vous disposez de deux clés de stockage pour votre compte de stockage d'objets blob.</span><span class="sxs-lookup"><span data-stu-id="55f01-109">You may have noticed that you have two storage keys for your blob storage account.</span></span> <span data-ttu-id="55f01-110">Cela permet une transition.</span><span class="sxs-lookup"><span data-stu-id="55f01-110">This is so that you can transition</span></span>

<span data-ttu-id="55f01-111">La rotation de vos clés de compte de stockage Azure est un processus simple en trois étapes.</span><span class="sxs-lookup"><span data-stu-id="55f01-111">Rotating your Azure storage account keys is a simple three step process</span></span>

1. <span data-ttu-id="55f01-112">Créer le deuxième information d’identification de la portée de la base de données en fonction de la clé d’accès de stockage secondaire de hello</span><span class="sxs-lookup"><span data-stu-id="55f01-112">Create second database scoped credential based on hello secondary storage access key</span></span>
2. <span data-ttu-id="55f01-113">Créez la deuxième source de données externe en fonction de ces nouvelles informations d'identification.</span><span class="sxs-lookup"><span data-stu-id="55f01-113">Create second external data source based off this new credential</span></span>
3. <span data-ttu-id="55f01-114">Supprimez et recréez les tables externes hello pointant vers la nouvelle source de données externe toohello</span><span class="sxs-lookup"><span data-stu-id="55f01-114">Drop and create hello external table(s) pointing toohello new external data source</span></span>

<span data-ttu-id="55f01-115">Lorsque vous avez migré toutes les tables externes toohello nouvelle source de données externe que vous pouvez effectuer hello nettoyer des tâches :</span><span class="sxs-lookup"><span data-stu-id="55f01-115">When you have migrated all your external tables toohello new external data source then you can perform hello clean up tasks:</span></span>

1. <span data-ttu-id="55f01-116">suppression de la première source de données externe ;</span><span class="sxs-lookup"><span data-stu-id="55f01-116">Drop first external data source</span></span>
2. <span data-ttu-id="55f01-117">Première base de données de la suppression d’une étendue d’informations d’identification en fonction de la clé d’accès de stockage principal de hello</span><span class="sxs-lookup"><span data-stu-id="55f01-117">Drop first database scoped credential based on hello primary storage access key</span></span>
3. <span data-ttu-id="55f01-118">Connectez-vous à Azure et régénérer la clé d’accès primaire hello prête pour hello prochaine</span><span class="sxs-lookup"><span data-stu-id="55f01-118">Log into Azure and regenerate hello primary access key ready for hello next time</span></span>

## <a name="query-azure-blob-storage-data"></a><span data-ttu-id="55f01-119">Interroger des données de l’espace de stockage d’objets Blob Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="55f01-119">Query Azure blob storage data</span></span>
<span data-ttu-id="55f01-120">Requêtes sur des tables externes utilisent simplement le nom de la table hello comme s’il s’agissait d’une table relationnelle.</span><span class="sxs-lookup"><span data-stu-id="55f01-120">Queries against external tables simply use hello table name as though it was a relational table.</span></span>

```sql
-- Query Azure storage resident data via external table.
SELECT * FROM [ext].[CarSensor_Data]
;
```

> [!NOTE]
> <span data-ttu-id="55f01-121">Une requête sur une table externe peut échouer avec l’erreur de hello *« requête abandonnée : seuil de rejet maximal hello a été atteinte lors de la lecture à partir d’une source externe »*.</span><span class="sxs-lookup"><span data-stu-id="55f01-121">A query on an external table can fail with hello error *"Query aborted-- hello maximum reject threshold was reached while reading from an external source"*.</span></span> <span data-ttu-id="55f01-122">Cela indique que vos données externes contiennent des enregistrements *à l’intégrité compromise* .</span><span class="sxs-lookup"><span data-stu-id="55f01-122">This indicates that your external data contains *dirty* records.</span></span> <span data-ttu-id="55f01-123">Un enregistrement de données est considérée comme « dirty » si les types de données réelles hello/nombre de colonnes ne correspondent pas les définitions des colonnes d’une table externe hello hello ou si les données de salutation n’est pas conforme toohello externe format spécifiés.</span><span class="sxs-lookup"><span data-stu-id="55f01-123">A data record is considered 'dirty' if hello actual data types/number of columns do not match hello column definitions of hello external table or if hello data doesn't conform toohello specified external file format.</span></span> <span data-ttu-id="55f01-124">toofix, assurez-vous que votre table externe et les définitions de format de fichier externe sont correctes et que vos données externes est conforme à des définitions de toothese.</span><span class="sxs-lookup"><span data-stu-id="55f01-124">toofix this, ensure that your external table and external file format definitions are correct and your external data conforms toothese definitions.</span></span> <span data-ttu-id="55f01-125">Au cas où un sous-ensemble d’enregistrements de données externes sont incorrectes, vous pouvez choisir tooreject ces enregistrements de vos requêtes à l’aide des options de rejet hello dans DDL créer la TABLE externe.</span><span class="sxs-lookup"><span data-stu-id="55f01-125">In case a subset of external data records are dirty, you can choose tooreject these records for your queries by using hello reject options in CREATE EXTERNAL TABLE DDL.</span></span>
> 
> 

## <a name="load-data-from-azure-blob-storage"></a><span data-ttu-id="55f01-126">Charger des données à partir d’objets Blob Microsoft Azure Storage</span><span class="sxs-lookup"><span data-stu-id="55f01-126">Load data from Azure blob storage</span></span>
<span data-ttu-id="55f01-127">Cet exemple charge des données à partir de la base de données du Data Warehouse tooSQL stockage blob Azure.</span><span class="sxs-lookup"><span data-stu-id="55f01-127">This example loads data from Azure blob storage tooSQL Data Warehouse database.</span></span>

<span data-ttu-id="55f01-128">Le stockage des données directement supprime les temps de transfert de données hello pour les requêtes.</span><span class="sxs-lookup"><span data-stu-id="55f01-128">Storing data directly removes hello data transfer time for queries.</span></span> <span data-ttu-id="55f01-129">Le stockage des données avec un index columnstore améliore les performances des requêtes d’analyse par des too10x.</span><span class="sxs-lookup"><span data-stu-id="55f01-129">Storing data with a columnstore index improves query performance for analysis queries by up too10x.</span></span>

<span data-ttu-id="55f01-130">Cet exemple utilise des données de tooload instruction CREATE TABLE AS SELECT hello.</span><span class="sxs-lookup"><span data-stu-id="55f01-130">This example uses hello CREATE TABLE AS SELECT statement tooload data.</span></span> <span data-ttu-id="55f01-131">nouvelle table de Hello hérite des colonnes hello nommées dans la requête de hello.</span><span class="sxs-lookup"><span data-stu-id="55f01-131">hello new table inherits hello columns named in hello query.</span></span> <span data-ttu-id="55f01-132">Il hérite des types de données hello de ces colonnes de définition de la table externe hello.</span><span class="sxs-lookup"><span data-stu-id="55f01-132">It inherits hello data types of those columns from hello external table definition.</span></span>

<span data-ttu-id="55f01-133">CREATE TABLE AS SELECT est une très performantes instruction Transact-SQL qui charge des données hello tooall parallèle Bonjour les nœuds de votre entrepôt de données SQL.</span><span class="sxs-lookup"><span data-stu-id="55f01-133">CREATE TABLE AS SELECT is a highly performant Transact-SQL statement that loads hello data in parallel tooall hello compute nodes of your SQL Data Warehouse.</span></span>  <span data-ttu-id="55f01-134">Il a été développé pour le moteur de traitement parallèle massif (MPP) hello dans le système de plateforme Analytique et est désormais dans l’entrepôt de données SQL.</span><span class="sxs-lookup"><span data-stu-id="55f01-134">It was originally developed for  hello massively parallel processing (MPP) engine in Analytics Platform System and is now in SQL Data Warehouse.</span></span>

```sql
-- Load data from Azure blob storage tooSQL Data Warehouse

CREATE TABLE [dbo].[Customer_Speed]
WITH
(   
    CLUSTERED COLUMNSTORE INDEX
,    DISTRIBUTION = HASH([CarSensor_Data].[CustomerKey])
)
AS
SELECT *
FROM   [ext].[CarSensor_Data]
;
```

<span data-ttu-id="55f01-135">Consultez [CREATE TABLE AS SELECT (Transact-SQL)][CREATE TABLE AS SELECT (Transact-SQL)].</span><span class="sxs-lookup"><span data-stu-id="55f01-135">See [CREATE TABLE AS SELECT (Transact-SQL)][CREATE TABLE AS SELECT (Transact-SQL)].</span></span>

## <a name="create-statistics-on-newly-loaded-data"></a><span data-ttu-id="55f01-136">Créer des statistiques sur des données nouvellement chargées</span><span class="sxs-lookup"><span data-stu-id="55f01-136">Create Statistics on newly loaded data</span></span>
<span data-ttu-id="55f01-137">Azure SQL Data Warehouse ne prend pas encore en charge les statistiques à création ou mise à jour automatique.</span><span class="sxs-lookup"><span data-stu-id="55f01-137">Azure SQL Data Warehouse does not yet support auto create or auto update statistics.</span></span>  <span data-ttu-id="55f01-138">Dans l’ordre tooget hello optimiser les performances de vos requêtes, il est important que créer des statistiques sur toutes les colonnes de toutes les tables après le premier chargement de hello ou toutes les modifications importantes se produisent dans les données de salutation.</span><span class="sxs-lookup"><span data-stu-id="55f01-138">In order tooget hello best performance from your queries, it's important that statistics be created on all columns of all tables after hello first load or any substantial changes occur in hello data.</span></span>  <span data-ttu-id="55f01-139">Pour obtenir une explication détaillée des statistiques, consultez hello [statistiques] [ Statistics] rubrique dans le groupe de développement hello de rubriques.</span><span class="sxs-lookup"><span data-stu-id="55f01-139">For a detailed explanation of statistics, see hello [Statistics][Statistics] topic in hello Develop group of topics.</span></span>  <span data-ttu-id="55f01-140">Voici un exemple rapide de la façon dont les statistiques toocreate sur hello déposée chargement dans cet exemple.</span><span class="sxs-lookup"><span data-stu-id="55f01-140">Below is a quick example of how toocreate statistics on hello tabled loaded in this example.</span></span>

```sql
create statistics [SensorKey] on [Customer_Speed] ([SensorKey]);
create statistics [CustomerKey] on [Customer_Speed] ([CustomerKey]);
create statistics [GeographyKey] on [Customer_Speed] ([GeographyKey]);
create statistics [Speed] on [Customer_Speed] ([Speed]);
create statistics [YearMeasured] on [Customer_Speed] ([YearMeasured]);
```

## <a name="export-data-tooazure-blob-storage"></a><span data-ttu-id="55f01-141">Exporter le stockage d’objets blob de données tooAzure</span><span class="sxs-lookup"><span data-stu-id="55f01-141">Export data tooAzure blob storage</span></span>
<span data-ttu-id="55f01-142">Cette section montre comment tooexport des données à partir de l’entrepôt de données SQL tooAzure stockage d’objets blob.</span><span class="sxs-lookup"><span data-stu-id="55f01-142">This section shows how tooexport data from SQL Data Warehouse tooAzure blob storage.</span></span> <span data-ttu-id="55f01-143">Cet exemple utilise CREATE EXTERNAL TABLE AS SELECT qui est un hautement performant Transact-SQL instruction tooexport hello de données en parallèle à partir de tous les nœuds de calcul hello.</span><span class="sxs-lookup"><span data-stu-id="55f01-143">This example uses CREATE EXTERNAL TABLE AS SELECT which is a highly performant Transact-SQL statement tooexport hello data in parallel from all hello compute nodes.</span></span>

<span data-ttu-id="55f01-144">Hello exemple suivant crée une table externe Weblogs2014 à l’aide des définitions de colonne et les données à partir de dbo. Table des blogs.</span><span class="sxs-lookup"><span data-stu-id="55f01-144">hello following example creates an external table Weblogs2014 using column definitions and data from dbo.Weblogs table.</span></span> <span data-ttu-id="55f01-145">définition de la table externe Hello est stockée dans l’entrepôt de données SQL et les résultats de hello d’instruction SELECT de hello sont exportée toohello répertoire « / archive/log2014 / » sous le conteneur d’objets blob hello spécifié par la source de données hello.</span><span class="sxs-lookup"><span data-stu-id="55f01-145">hello external table definition is stored in SQL Data Warehouse and hello results of hello SELECT statement are exported toohello "/archive/log2014/" directory under hello blob container specified by hello data source.</span></span> <span data-ttu-id="55f01-146">les données de Hello sont exportées au format de fichier texte hello.</span><span class="sxs-lookup"><span data-stu-id="55f01-146">hello data is exported in hello specified text file format.</span></span>

```sql
CREATE EXTERNAL TABLE Weblogs2014 WITH
(
    LOCATION='/archive/log2014/',
    DATA_SOURCE=azure_storage,
    FILE_FORMAT=text_file_format
)
AS
SELECT
    Uri,
    DateRequested
FROM
    dbo.Weblogs
WHERE
    1=1
    AND DateRequested > '12/31/2013'
    AND DateRequested < '01/01/2015';
```
## <a name="isolate-loading-users"></a><span data-ttu-id="55f01-147">Isoler les utilisateurs du chargement</span><span class="sxs-lookup"><span data-stu-id="55f01-147">Isolate Loading Users</span></span>
<span data-ttu-id="55f01-148">Il existe souvent un toohave besoin de plusieurs utilisateurs qui peuvent charger des données dans un entrepôt de données SQL.</span><span class="sxs-lookup"><span data-stu-id="55f01-148">There is often a need toohave multiple users that can load data into a SQL DW.</span></span> <span data-ttu-id="55f01-149">Étant donné que hello [CREATE TABLE AS SELECT (Transact-SQL)] [ CREATE TABLE AS SELECT (Transact-SQL)] nécessite des autorisations de contrôle de base de données hello, vous obtiendrez avec plusieurs utilisateurs à contrôler l’accès sur tous les schémas.</span><span class="sxs-lookup"><span data-stu-id="55f01-149">Because hello [CREATE TABLE AS SELECT (Transact-SQL)][CREATE TABLE AS SELECT (Transact-SQL)] requires CONTROL permissions of hello database, you will end up with multiple users with control access over all schemas.</span></span> <span data-ttu-id="55f01-150">toolimit, vous pouvez utiliser d’instruction de contrôle de refuser hello.</span><span class="sxs-lookup"><span data-stu-id="55f01-150">toolimit this, you can use hello DENY CONTROL statement.</span></span>

<span data-ttu-id="55f01-151">Par exemple, les schémas de base de données schema_A pour le service A et schema_B pour le service B laissent les utilisateurs de base de données user_A et user_B être utilisateurs du chargement PolyBase dans les services A et B, respectivement.</span><span class="sxs-lookup"><span data-stu-id="55f01-151">Example: Consider database schemas schema_A for dept A, and schema_B for dept B Let database users user_A and user_B be users for PolyBase loading in dept A and B, respectively.</span></span> <span data-ttu-id="55f01-152">Ils ont tous deux reçu des autorisations de base de données CONTROL.</span><span class="sxs-lookup"><span data-stu-id="55f01-152">They both have been granted CONTROL database permissions.</span></span>
<span data-ttu-id="55f01-153">créateurs Hello du schéma A et B désormais verrouiller leurs schémas à l’aide de refus :</span><span class="sxs-lookup"><span data-stu-id="55f01-153">hello creators of schema A and B now lock down their schemas using DENY:</span></span>

```sql
   DENY CONTROL ON SCHEMA :: schema_A toouser_B;
   DENY CONTROL ON SCHEMA :: schema_B toouser_A;
```   
 <span data-ttu-id="55f01-154">Avec cette option, ce dernier et user_B doivent maintenant être verrouillée de hello les schémas d’autres sociétés.</span><span class="sxs-lookup"><span data-stu-id="55f01-154">With this, user_A and user_B should now be locked out from hello other dept’s schema.</span></span>
 


## <a name="next-steps"></a><span data-ttu-id="55f01-155">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="55f01-155">Next steps</span></span>
<span data-ttu-id="55f01-156">toolearn en savoir plus sur mobile tooSQL données entrepôt de données, consultez hello [vue d’ensemble de la migration de données][data migration overview].</span><span class="sxs-lookup"><span data-stu-id="55f01-156">toolearn more about moving data tooSQL Data Warehouse, see hello [data migration overview][data migration overview].</span></span>

<!--Image references-->

<!--Article references-->
[Load data with bcp]: ./sql-data-warehouse-load-with-bcp.md
[Load data with PolyBase]: ./sql-data-warehouse-get-started-load-with-polybase.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md
[data migration overview]: ./sql-data-warehouse-overview-migrate.md

<!--MSDN references-->
[supported source/sink]: https://msdn.microsoft.com/library/dn894007.aspx
[copy activity]: https://msdn.microsoft.com/library/dn835035.aspx
[SQL Server destination adapter]: https://msdn.microsoft.com/library/ms141095.aspx
[SSIS]: https://msdn.microsoft.com/library/ms141026.aspx

[CREATE EXTERNAL DATA SOURCE (Transact-SQL)]: https://msdn.microsoft.com/library/dn935022.aspx
[CREATE EXTERNAL FILE FORMAT (Transact-SQL)]: https://msdn.microsoft.com/library/dn935026.aspx
[CREATE EXTERNAL TABLE (Transact-SQL)]: https://msdn.microsoft.com/library/dn935021.aspx

[DROP EXTERNAL DATA SOURCE (Transact-SQL)]: https://msdn.microsoft.com/library/mt146367.aspx
[DROP EXTERNAL FILE FORMAT (Transact-SQL)]: https://msdn.microsoft.com/library/mt146379.aspx
[DROP EXTERNAL TABLE (Transact-SQL)]: https://msdn.microsoft.com/library/mt130698.aspx

[CREATE TABLE AS SELECT (Transact-SQL)]: https://msdn.microsoft.com/library/mt204041.aspx
[INSERT...SELECT (Transact-SQL)]: https://msdn.microsoft.com/library/ms174335.aspx
[CREATE MASTER KEY (Transact-SQL)]: https://msdn.microsoft.com/library/ms174382.aspx
[CREATE CREDENTIAL (Transact-SQL)]: https://msdn.microsoft.com/library/ms189522.aspx
[CREATE DATABASE SCOPED CREDENTIAL (Transact-SQL)]: https://msdn.microsoft.com/library/mt270260.aspx
[DROP CREDENTIAL (Transact-SQL)]: https://msdn.microsoft.com/library/ms189450.aspx

<!-- External Links -->
