---
title: "Guide d’utilisation de PolyBase dans SQL Data Warehouse | Microsoft Docs"
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
ms.openlocfilehash: 6938b92d8e5b46d908dc5b2155bdfdc89bb1dc8c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="guide-for-using-polybase-in-sql-data-warehouse"></a><span data-ttu-id="4599b-103">Guide d'utilisation de PolyBase dans SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="4599b-103">Guide for using PolyBase in SQL Data Warehouse</span></span>
<span data-ttu-id="4599b-104">Ce guide fournit des informations pratiques pour l'utilisation de PolyBase dans SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="4599b-104">This guide gives practical information for using PolyBase in SQL Data Warehouse.</span></span>

<span data-ttu-id="4599b-105">Pour commencer, suivez le didacticiel [Charger des données avec PolyBase][Load data with PolyBase].</span><span class="sxs-lookup"><span data-stu-id="4599b-105">To get started, see the [Load data with PolyBase][Load data with PolyBase] tutorial.</span></span>

## <a name="rotating-storage-keys"></a><span data-ttu-id="4599b-106">Rotation des clés de stockage</span><span class="sxs-lookup"><span data-stu-id="4599b-106">Rotating storage keys</span></span>
<span data-ttu-id="4599b-107">De temps à autre, vous devez modifier la clé d'accès à votre stockage d'objets blob pour des raisons de sécurité.</span><span class="sxs-lookup"><span data-stu-id="4599b-107">From time to time you will want to change the access key to your blob storage for security reasons.</span></span>

<span data-ttu-id="4599b-108">La façon la plus élégante d’effectuer cette tâche consiste à suivre un processus appelé « rotation des clés ».</span><span class="sxs-lookup"><span data-stu-id="4599b-108">The most elegant way to perform this task is to follow a process known as "rotating the keys".</span></span> <span data-ttu-id="4599b-109">Vous avez peut-être remarqué que vous disposez de deux clés de stockage pour votre compte de stockage d'objets blob.</span><span class="sxs-lookup"><span data-stu-id="4599b-109">You may have noticed that you have two storage keys for your blob storage account.</span></span> <span data-ttu-id="4599b-110">Cela permet une transition.</span><span class="sxs-lookup"><span data-stu-id="4599b-110">This is so that you can transition</span></span>

<span data-ttu-id="4599b-111">La rotation de vos clés de compte de stockage Azure est un processus simple en trois étapes.</span><span class="sxs-lookup"><span data-stu-id="4599b-111">Rotating your Azure storage account keys is a simple three step process</span></span>

1. <span data-ttu-id="4599b-112">Créez le deuxième fichier d’informations d’identification de niveau base de données en fonction de la clé d'accès de stockage secondaire.</span><span class="sxs-lookup"><span data-stu-id="4599b-112">Create second database scoped credential based on the secondary storage access key</span></span>
2. <span data-ttu-id="4599b-113">Créez la deuxième source de données externe en fonction de ces nouvelles informations d'identification.</span><span class="sxs-lookup"><span data-stu-id="4599b-113">Create second external data source based off this new credential</span></span>
3. <span data-ttu-id="4599b-114">Supprimez et créez la ou les tables externes pointant vers la nouvelle source de données externes.</span><span class="sxs-lookup"><span data-stu-id="4599b-114">Drop and create the external table(s) pointing to the new external data source</span></span>

<span data-ttu-id="4599b-115">Lorsque vous avez migré toutes vos tables externes vers la nouvelle source de données externes, vous pouvez effectuer les tâches de nettoyage :</span><span class="sxs-lookup"><span data-stu-id="4599b-115">When you have migrated all your external tables to the new external data source then you can perform the clean up tasks:</span></span>

1. <span data-ttu-id="4599b-116">suppression de la première source de données externe ;</span><span class="sxs-lookup"><span data-stu-id="4599b-116">Drop first external data source</span></span>
2. <span data-ttu-id="4599b-117">suppression du premier fichier d’informations d’identification de niveau base de données en fonction de la clé d'accès de stockage secondaire ;</span><span class="sxs-lookup"><span data-stu-id="4599b-117">Drop first database scoped credential based on the primary storage access key</span></span>
3. <span data-ttu-id="4599b-118">connexion à Azure et régénération de la clé d'accès primaire, pour la prochaine fois.</span><span class="sxs-lookup"><span data-stu-id="4599b-118">Log into Azure and regenerate the primary access key ready for the next time</span></span>

## <a name="query-azure-blob-storage-data"></a><span data-ttu-id="4599b-119">Interroger des données de l’espace de stockage d’objets Blob Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="4599b-119">Query Azure blob storage data</span></span>
<span data-ttu-id="4599b-120">Les requêtes dirigées vers les tables externes utilisent le nom de table, comme s’il s’agissait d’une table relationnelle.</span><span class="sxs-lookup"><span data-stu-id="4599b-120">Queries against external tables simply use the table name as though it was a relational table.</span></span>

```sql
-- Query Azure storage resident data via external table.
SELECT * FROM [ext].[CarSensor_Data]
;
```

> [!NOTE]
> <span data-ttu-id="4599b-121">Une requête sur une table externe peut échouer avec l’erreur *« Requête abandonnée : le seuil de rejet maximal a été atteint lors de la lecture à partir d’une source externe »*.</span><span class="sxs-lookup"><span data-stu-id="4599b-121">A query on an external table can fail with the error *"Query aborted-- the maximum reject threshold was reached while reading from an external source"*.</span></span> <span data-ttu-id="4599b-122">Cela indique que vos données externes contiennent des enregistrements *à l’intégrité compromise* .</span><span class="sxs-lookup"><span data-stu-id="4599b-122">This indicates that your external data contains *dirty* records.</span></span> <span data-ttu-id="4599b-123">Un enregistrement de données est considéré comme « compromis » si les types de données / le nombre de colonnes réels ne correspondent pas aux définitions de colonne de la table externe ou si les données ne sont pas conformes au format de fichier externe spécifié.</span><span class="sxs-lookup"><span data-stu-id="4599b-123">A data record is considered 'dirty' if the actual data types/number of columns do not match the column definitions of the external table or if the data doesn't conform to the specified external file format.</span></span> <span data-ttu-id="4599b-124">Pour résoudre ce problème, assurez-vous que les définitions de format de votre table externe et de votre fichier externe sont correctes et que vos données externes sont conformes à ces définitions.</span><span class="sxs-lookup"><span data-stu-id="4599b-124">To fix this, ensure that your external table and external file format definitions are correct and your external data conforms to these definitions.</span></span> <span data-ttu-id="4599b-125">Dans le cas où un sous-ensemble d'enregistrements de données externes serait compromis, vous pouvez choisir de rejeter ces enregistrements pour vos requêtes en utilisant les options de rejet dans le DDL CREATE EXTERNAL TABLE.</span><span class="sxs-lookup"><span data-stu-id="4599b-125">In case a subset of external data records are dirty, you can choose to reject these records for your queries by using the reject options in CREATE EXTERNAL TABLE DDL.</span></span>
> 
> 

## <a name="load-data-from-azure-blob-storage"></a><span data-ttu-id="4599b-126">Charger des données à partir d’objets Blob Microsoft Azure Storage</span><span class="sxs-lookup"><span data-stu-id="4599b-126">Load data from Azure blob storage</span></span>
<span data-ttu-id="4599b-127">Dans cet exemple, les données des objets Blob Microsoft Azure Storage sont chargées dans la base de données SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="4599b-127">This example loads data from Azure blob storage to SQL Data Warehouse database.</span></span>

<span data-ttu-id="4599b-128">En stockant directement les données, vous éliminez l’intervalle de transfert de données associé aux requêtes.</span><span class="sxs-lookup"><span data-stu-id="4599b-128">Storing data directly removes the data transfer time for queries.</span></span> <span data-ttu-id="4599b-129">Le stockage des données avec un index columnstore multiplie jusqu’à dix fois les performances des requêtes d’analyse.</span><span class="sxs-lookup"><span data-stu-id="4599b-129">Storing data with a columnstore index improves query performance for analysis queries by up to 10x.</span></span>

<span data-ttu-id="4599b-130">Dans cet exemple, l’instruction CREATE TABLE AS SELECT est utilisée pour charger des données.</span><span class="sxs-lookup"><span data-stu-id="4599b-130">This example uses the CREATE TABLE AS SELECT statement to load data.</span></span> <span data-ttu-id="4599b-131">La nouvelle table hérite des colonnes désignées dans la requête.</span><span class="sxs-lookup"><span data-stu-id="4599b-131">The new table inherits the columns named in the query.</span></span> <span data-ttu-id="4599b-132">Elle hérite des types de données de ces colonnes à partir de la définition de table externe.</span><span class="sxs-lookup"><span data-stu-id="4599b-132">It inherits the data types of those columns from the external table definition.</span></span>

<span data-ttu-id="4599b-133">CREATE TABLE AS SELECT est une instruction Transact-SQL très performante qui charge les données en parallèle sur tous les nœuds de calcul de votre entrepôt SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="4599b-133">CREATE TABLE AS SELECT is a highly performant Transact-SQL statement that loads the data in parallel to all the compute nodes of your SQL Data Warehouse.</span></span>  <span data-ttu-id="4599b-134">Initialement développée pour le moteur MPP (Massively Parallel Processing) d’Analytics Platform System, elle est désormais disponible dans SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="4599b-134">It was originally developed for  the massively parallel processing (MPP) engine in Analytics Platform System and is now in SQL Data Warehouse.</span></span>

```sql
-- Load data from Azure blob storage to SQL Data Warehouse

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

<span data-ttu-id="4599b-135">Consultez [CREATE TABLE AS SELECT (Transact-SQL)][CREATE TABLE AS SELECT (Transact-SQL)].</span><span class="sxs-lookup"><span data-stu-id="4599b-135">See [CREATE TABLE AS SELECT (Transact-SQL)][CREATE TABLE AS SELECT (Transact-SQL)].</span></span>

## <a name="create-statistics-on-newly-loaded-data"></a><span data-ttu-id="4599b-136">Créer des statistiques sur des données nouvellement chargées</span><span class="sxs-lookup"><span data-stu-id="4599b-136">Create Statistics on newly loaded data</span></span>
<span data-ttu-id="4599b-137">Azure SQL Data Warehouse ne prend pas encore en charge les statistiques à création ou mise à jour automatique.</span><span class="sxs-lookup"><span data-stu-id="4599b-137">Azure SQL Data Warehouse does not yet support auto create or auto update statistics.</span></span>  <span data-ttu-id="4599b-138">Pour optimiser les performances de vos requêtes, il est important de créer les statistiques sur toutes les colonnes de toutes les tables après le premier chargement ou après toute modification substantielle dans les données.</span><span class="sxs-lookup"><span data-stu-id="4599b-138">In order to get the best performance from your queries, it's important that statistics be created on all columns of all tables after the first load or any substantial changes occur in the data.</span></span>  <span data-ttu-id="4599b-139">Pour obtenir une explication détaillée des statistiques, consultez la rubrique [Statistiques][Statistics] dans le groupe de rubriques sur le développement.</span><span class="sxs-lookup"><span data-stu-id="4599b-139">For a detailed explanation of statistics, see the [Statistics][Statistics] topic in the Develop group of topics.</span></span>  <span data-ttu-id="4599b-140">Voici un exemple rapide de la création de statistiques sur le tableau chargé dans cet exemple.</span><span class="sxs-lookup"><span data-stu-id="4599b-140">Below is a quick example of how to create statistics on the tabled loaded in this example.</span></span>

```sql
create statistics [SensorKey] on [Customer_Speed] ([SensorKey]);
create statistics [CustomerKey] on [Customer_Speed] ([CustomerKey]);
create statistics [GeographyKey] on [Customer_Speed] ([GeographyKey]);
create statistics [Speed] on [Customer_Speed] ([Speed]);
create statistics [YearMeasured] on [Customer_Speed] ([YearMeasured]);
```

## <a name="export-data-to-azure-blob-storage"></a><span data-ttu-id="4599b-141">Exportation de données vers le stockage d’objets blob Azure</span><span class="sxs-lookup"><span data-stu-id="4599b-141">Export data to Azure blob storage</span></span>
<span data-ttu-id="4599b-142">Cette section montre comment exporter les données de SQL Data Warehouse vers le stockage d’objets blob Azure.</span><span class="sxs-lookup"><span data-stu-id="4599b-142">This section shows how to export data from SQL Data Warehouse to Azure blob storage.</span></span> <span data-ttu-id="4599b-143">Cet exemple utilise CREATE EXTERNAL TABLE AS SELECT, une instruction Transact-SQL très performante, pour exporter les données en parallèle à partir de tous les nœuds de calcul.</span><span class="sxs-lookup"><span data-stu-id="4599b-143">This example uses CREATE EXTERNAL TABLE AS SELECT which is a highly performant Transact-SQL statement to export the data in parallel from all the compute nodes.</span></span>

<span data-ttu-id="4599b-144">L’exemple suivant crée une table externe Weblogs2014 à l’aide des définitions de colonne et des données de la table dbo.Weblogs.</span><span class="sxs-lookup"><span data-stu-id="4599b-144">The following example creates an external table Weblogs2014 using column definitions and data from dbo.Weblogs table.</span></span> <span data-ttu-id="4599b-145">La définition de la table externe est stockée dans SQL Data Warehouse et les résultats de l’instruction SELECT sont exportés vers le répertoire « /archive/log2014 » sous le conteneur d’objets blob spécifié par la source de données.</span><span class="sxs-lookup"><span data-stu-id="4599b-145">The external table definition is stored in SQL Data Warehouse and the results of the SELECT statement are exported to the "/archive/log2014/" directory under the blob container specified by the data source.</span></span> <span data-ttu-id="4599b-146">Les données sont exportées au format de fichier texte spécifié.</span><span class="sxs-lookup"><span data-stu-id="4599b-146">The data is exported in the specified text file format.</span></span>

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
## <a name="isolate-loading-users"></a><span data-ttu-id="4599b-147">Isoler les utilisateurs du chargement</span><span class="sxs-lookup"><span data-stu-id="4599b-147">Isolate Loading Users</span></span>
<span data-ttu-id="4599b-148">Il est souvent nécessaire d’avoir plusieurs utilisateurs qui peuvent charger des données dans un entrepôt de données SQL.</span><span class="sxs-lookup"><span data-stu-id="4599b-148">There is often a need to have multiple users that can load data into a SQL DW.</span></span> <span data-ttu-id="4599b-149">Étant donné que [CREATE TABLE AS SELECT (Transact-SQL)][CREATE TABLE AS SELECT (Transact-SQL)] nécessite des autorisations CONTROL de la base de données, vous obtenez plusieurs utilisateurs avec un accès au contrôle sur tous les schémas.</span><span class="sxs-lookup"><span data-stu-id="4599b-149">Because the [CREATE TABLE AS SELECT (Transact-SQL)][CREATE TABLE AS SELECT (Transact-SQL)] requires CONTROL permissions of the database, you will end up with multiple users with control access over all schemas.</span></span> <span data-ttu-id="4599b-150">Pour limiter ce problème, vous pouvez utiliser l’instruction DENY CONTROL.</span><span class="sxs-lookup"><span data-stu-id="4599b-150">To limit this, you can use the DENY CONTROL statement.</span></span>

<span data-ttu-id="4599b-151">Par exemple, les schémas de base de données schema_A pour le service A et schema_B pour le service B laissent les utilisateurs de base de données user_A et user_B être utilisateurs du chargement PolyBase dans les services A et B, respectivement.</span><span class="sxs-lookup"><span data-stu-id="4599b-151">Example: Consider database schemas schema_A for dept A, and schema_B for dept B Let database users user_A and user_B be users for PolyBase loading in dept A and B, respectively.</span></span> <span data-ttu-id="4599b-152">Ils ont tous deux reçu des autorisations de base de données CONTROL.</span><span class="sxs-lookup"><span data-stu-id="4599b-152">They both have been granted CONTROL database permissions.</span></span>
<span data-ttu-id="4599b-153">Les créateurs des schémas A et B verrouillent maintenant leurs schémas à l’aide de DENY :</span><span class="sxs-lookup"><span data-stu-id="4599b-153">The creators of schema A and B now lock down their schemas using DENY:</span></span>

```sql
   DENY CONTROL ON SCHEMA :: schema_A TO user_B;
   DENY CONTROL ON SCHEMA :: schema_B TO user_A;
```   
 <span data-ttu-id="4599b-154">Suite à cette opération, user_A et user_B ne doivent maintenant plus avoir accès au schéma de l’autre service.</span><span class="sxs-lookup"><span data-stu-id="4599b-154">With this, user_A and user_B should now be locked out from the other dept’s schema.</span></span>
 


## <a name="next-steps"></a><span data-ttu-id="4599b-155">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4599b-155">Next steps</span></span>
<span data-ttu-id="4599b-156">Pour en savoir plus sur le déplacement de données dans SQL Data Warehouse, consultez la [vue d’ensemble de la migration des données][data migration overview].</span><span class="sxs-lookup"><span data-stu-id="4599b-156">To learn more about moving data to SQL Data Warehouse, see the [data migration overview][data migration overview].</span></span>

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
