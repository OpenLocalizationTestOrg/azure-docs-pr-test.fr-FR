---
title: "données aaaLoad à partir de SQL Server dans Azure SQL Data Warehouse (bcp) | Documents Microsoft"
description: "Pour une taille de données de petite taille, utilise les données tooexport de bcp à partir de fichiers tooflat de SQL Server et importer des données hello directement dans l’entrepôt de données SQL Azure."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: jhubbard
editor: 
ms.assetid: f87d8d7c-8276-43c5-90e7-d4ccc0e3a224
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: a03b5403d123e8814ae73a7cce8e6851c8b264a6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-from-sql-server-into-azure-sql-data-warehouse-flat-files"></a><span data-ttu-id="84b3b-103">Charger des données à partir de SQL Server dans Azure SQL Data Warehouse (fichiers plats)</span><span class="sxs-lookup"><span data-stu-id="84b3b-103">Load data from SQL Server into Azure SQL Data Warehouse (flat files)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="84b3b-104">SSIS</span><span class="sxs-lookup"><span data-stu-id="84b3b-104">SSIS</span></span>](sql-data-warehouse-load-from-sql-server-with-integration-services.md)
> * [<span data-ttu-id="84b3b-105">PolyBase</span><span class="sxs-lookup"><span data-stu-id="84b3b-105">PolyBase</span></span>](sql-data-warehouse-load-from-sql-server-with-polybase.md)
> * [<span data-ttu-id="84b3b-106">bcp</span><span class="sxs-lookup"><span data-stu-id="84b3b-106">bcp</span></span>](sql-data-warehouse-load-from-sql-server-with-bcp.md)
> 
> 

<span data-ttu-id="84b3b-107">Pour les petits jeux de données, vous pouvez utiliser utilitaire de ligne de commande bcp hello tooexport des données à partir de SQL Server et puis de le charger directement tooAzure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="84b3b-107">For small data sets, you can use hello bcp command-line utility tooexport data from SQL Server and then load it directly tooAzure SQL Data Warehouse.</span></span>

<span data-ttu-id="84b3b-108">Dans ce didacticiel, nous allons utiliser bcp pour :</span><span class="sxs-lookup"><span data-stu-id="84b3b-108">In this tutorial, you will use bcp to:</span></span>

* <span data-ttu-id="84b3b-109">Exportez une table à partir de SQL Server à l’aide de bcp hello commande (ou créer un exemple simple de fichier)</span><span class="sxs-lookup"><span data-stu-id="84b3b-109">Export a table from from SQL Server by using hello bcp out command (or create a simple sample file)</span></span>
* <span data-ttu-id="84b3b-110">Table hello d’importation à partir d’un fichier plat de tooSQL l’entrepôt de données.</span><span class="sxs-lookup"><span data-stu-id="84b3b-110">Import hello table from a flat file tooSQL Data Warehouse.</span></span>
* <span data-ttu-id="84b3b-111">Créer des statistiques sur les données de salutation chargée.</span><span class="sxs-lookup"><span data-stu-id="84b3b-111">Create statistics on hello loaded data.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Loading-data-into-Azure-SQL-Data-Warehouse-with-BCP/player]
> 
> 

## <a name="before-you-begin"></a><span data-ttu-id="84b3b-112">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="84b3b-112">Before you begin</span></span>
### <a name="prerequisites"></a><span data-ttu-id="84b3b-113">Composants requis</span><span class="sxs-lookup"><span data-stu-id="84b3b-113">Prerequisites</span></span>
<span data-ttu-id="84b3b-114">toostep dans ce didacticiel, vous devez :</span><span class="sxs-lookup"><span data-stu-id="84b3b-114">toostep through this tutorial, you need:</span></span>

* <span data-ttu-id="84b3b-115">Base de données SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="84b3b-115">A SQL Data Warehouse database</span></span>
* <span data-ttu-id="84b3b-116">utilitaire de ligne de commande de Hello bcp installé</span><span class="sxs-lookup"><span data-stu-id="84b3b-116">hello bcp command-line utility installed</span></span>
* <span data-ttu-id="84b3b-117">utilitaire de ligne de commande de Hello sqlcmd installé</span><span class="sxs-lookup"><span data-stu-id="84b3b-117">hello sqlcmd command-line utility installed</span></span>

<span data-ttu-id="84b3b-118">Vous pouvez télécharger les utilitaires bcp et sqlcmd hello hello [Microsoft Download Center][Microsoft Download Center].</span><span class="sxs-lookup"><span data-stu-id="84b3b-118">You can download hello bcp and sqlcmd utilities from hello [Microsoft Download Center][Microsoft Download Center].</span></span>

### <a name="data-in-ascii-or-utf-16-format"></a><span data-ttu-id="84b3b-119">Données au format ASCII ou UTF-16</span><span class="sxs-lookup"><span data-stu-id="84b3b-119">Data in ASCII or UTF-16 format</span></span>
<span data-ttu-id="84b3b-120">Si vous essayez de ce didacticiel avec vos propres données, vos données doivent toouse hello ASCII ou UTF-16 encodage bcp ne prenant pas en charge UTF-8.</span><span class="sxs-lookup"><span data-stu-id="84b3b-120">If you are trying this tutorial with your own data, your data needs toouse hello ASCII or UTF-16 encoding since bcp does not support UTF-8.</span></span> 

<span data-ttu-id="84b3b-121">PolyBase prend en charge UTF-8, mais pas UTF-16 pour l’instant.</span><span class="sxs-lookup"><span data-stu-id="84b3b-121">PolyBase supports UTF-8 but doesn't yet support UTF-16.</span></span> <span data-ttu-id="84b3b-122">Notez que si vous souhaitez que bcp toocombine avec PolyBase vous devez tootransform hello données tooUTF-8 après son exportation à partir de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="84b3b-122">Note that if you want toocombine bcp with PolyBase you will need tootransform hello data tooUTF-8 after it is exported from SQL Server.</span></span> 

## <a name="1-create-a-destination-table"></a><span data-ttu-id="84b3b-123">1. Créer une table de destination</span><span class="sxs-lookup"><span data-stu-id="84b3b-123">1. Create a destination table</span></span>
<span data-ttu-id="84b3b-124">Définir une table dans l’entrepôt de données SQL qui sera la table de destination hello pour la charge hello.</span><span class="sxs-lookup"><span data-stu-id="84b3b-124">Define a table in SQL Data Warehouse that will be hello destination table for hello load.</span></span> <span data-ttu-id="84b3b-125">les colonnes dans la table de hello Hello doivent correspondre toohello des données dans chaque ligne de votre fichier de données.</span><span class="sxs-lookup"><span data-stu-id="84b3b-125">hello columns in hello table must correspond toohello data in each row of your data file.</span></span>

<span data-ttu-id="84b3b-126">toocreate une table, ouvrez une invite de commandes et utilisez sqlcmd.exe hello de toorun commande suivante :</span><span class="sxs-lookup"><span data-stu-id="84b3b-126">toocreate a table, open a command prompt and use sqlcmd.exe toorun hello following command:</span></span>

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "
    CREATE TABLE DimDate2
    (
        DateId INT NOT NULL,
        CalendarQuarter TINYINT NOT NULL,
        FiscalQuarter TINYINT NOT NULL
    )
    WITH
    (
        CLUSTERED COLUMNSTORE INDEX,
        DISTRIBUTION = ROUND_ROBIN
    );
"
```


## <a name="2-create-a-source-data-file"></a><span data-ttu-id="84b3b-127">2. Créer un fichier de données source</span><span class="sxs-lookup"><span data-stu-id="84b3b-127">2. Create a source data file</span></span>
<span data-ttu-id="84b3b-128">Ouvrez le bloc-notes, puis copiez hello après des lignes de données dans un nouveau fichier texte, puis enregistrez ce fichier tooyour répertoire temp local, C:\Temp\DimDate2.txt.</span><span class="sxs-lookup"><span data-stu-id="84b3b-128">Open Notepad and copy hello following lines of data into a new text file and then save this file tooyour local temp directory, C:\Temp\DimDate2.txt.</span></span> <span data-ttu-id="84b3b-129">Ces données sont au format ASCII.</span><span class="sxs-lookup"><span data-stu-id="84b3b-129">This data is in ASCII format.</span></span>

```
20150301,1,3
20150501,2,4
20151001,4,2
20150201,1,3
20151201,4,2
20150801,3,1
20150601,2,4
20151101,4,2
20150401,2,4
20150701,3,1
20150901,3,1
20150101,1,3
```

<span data-ttu-id="84b3b-130">(Facultatif) tooexport vos propres données à partir d’une base de données SQL Server, ouvrez une invite de commandes et exécutez hello commande suivante.</span><span class="sxs-lookup"><span data-stu-id="84b3b-130">(Optional) tooexport your own data from a SQL Server database, open a command prompt and run hello following command.</span></span> <span data-ttu-id="84b3b-131">Remplacez TableName, ServerName, DatabaseName, Username et Password par vos propres informations.</span><span class="sxs-lookup"><span data-stu-id="84b3b-131">Replace TableName, ServerName, DatabaseName, Username, and Password with your own information.</span></span>

```sql
bcp <TableName> out C:\Temp\DimDate2_export.txt -S <ServerName> -d <DatabaseName> -U <Username> -P <Password> -q -c -t ','
```



## <a name="3-load-hello-data"></a><span data-ttu-id="84b3b-132">3. Charger des données hello</span><span class="sxs-lookup"><span data-stu-id="84b3b-132">3. Load hello data</span></span>
<span data-ttu-id="84b3b-133">les données de salutation tooload, ouvrez une invite de commandes et exécutez les hello commande suivante, en remplaçant les valeurs hello pour le nom du serveur, nom de base de données, nom d’utilisateur et mot de passe avec vos propres informations.</span><span class="sxs-lookup"><span data-stu-id="84b3b-133">tooload hello data, open a command prompt and run hello following command, replacing hello values for Server Name, Database name, Username, and Password with your own information.</span></span>

```sql
bcp DimDate2 in C:\Temp\DimDate2.txt -S <ServerName> -d <DatabaseName> -U <Username> -P <password> -q -c -t  ','
```

<span data-ttu-id="84b3b-134">Utilisez cette commande hello tooverify données a été correctement chargées.</span><span class="sxs-lookup"><span data-stu-id="84b3b-134">Use this command tooverify hello data was loaded properly</span></span>

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "SELECT * FROM DimDate2 ORDER BY 1;"
```

<span data-ttu-id="84b3b-135">résultats de Hello doivent ressembler à ceci :</span><span class="sxs-lookup"><span data-stu-id="84b3b-135">hello results should look like this:</span></span>

| <span data-ttu-id="84b3b-136">DateId</span><span class="sxs-lookup"><span data-stu-id="84b3b-136">DateId</span></span> | <span data-ttu-id="84b3b-137">CalendarQuarter</span><span class="sxs-lookup"><span data-stu-id="84b3b-137">CalendarQuarter</span></span> | <span data-ttu-id="84b3b-138">FiscalQuarter</span><span class="sxs-lookup"><span data-stu-id="84b3b-138">FiscalQuarter</span></span> |
| --- | --- | --- |
| <span data-ttu-id="84b3b-139">20150101</span><span class="sxs-lookup"><span data-stu-id="84b3b-139">20150101</span></span> |<span data-ttu-id="84b3b-140">1</span><span class="sxs-lookup"><span data-stu-id="84b3b-140">1</span></span> |<span data-ttu-id="84b3b-141">3</span><span class="sxs-lookup"><span data-stu-id="84b3b-141">3</span></span> |
| <span data-ttu-id="84b3b-142">20150201</span><span class="sxs-lookup"><span data-stu-id="84b3b-142">20150201</span></span> |<span data-ttu-id="84b3b-143">1</span><span class="sxs-lookup"><span data-stu-id="84b3b-143">1</span></span> |<span data-ttu-id="84b3b-144">3</span><span class="sxs-lookup"><span data-stu-id="84b3b-144">3</span></span> |
| <span data-ttu-id="84b3b-145">20150301</span><span class="sxs-lookup"><span data-stu-id="84b3b-145">20150301</span></span> |<span data-ttu-id="84b3b-146">1</span><span class="sxs-lookup"><span data-stu-id="84b3b-146">1</span></span> |<span data-ttu-id="84b3b-147">3</span><span class="sxs-lookup"><span data-stu-id="84b3b-147">3</span></span> |
| <span data-ttu-id="84b3b-148">20150401</span><span class="sxs-lookup"><span data-stu-id="84b3b-148">20150401</span></span> |<span data-ttu-id="84b3b-149">2</span><span class="sxs-lookup"><span data-stu-id="84b3b-149">2</span></span> |<span data-ttu-id="84b3b-150">4</span><span class="sxs-lookup"><span data-stu-id="84b3b-150">4</span></span> |
| <span data-ttu-id="84b3b-151">20150501</span><span class="sxs-lookup"><span data-stu-id="84b3b-151">20150501</span></span> |<span data-ttu-id="84b3b-152">2</span><span class="sxs-lookup"><span data-stu-id="84b3b-152">2</span></span> |<span data-ttu-id="84b3b-153">4</span><span class="sxs-lookup"><span data-stu-id="84b3b-153">4</span></span> |
| <span data-ttu-id="84b3b-154">20150601</span><span class="sxs-lookup"><span data-stu-id="84b3b-154">20150601</span></span> |<span data-ttu-id="84b3b-155">2</span><span class="sxs-lookup"><span data-stu-id="84b3b-155">2</span></span> |<span data-ttu-id="84b3b-156">4</span><span class="sxs-lookup"><span data-stu-id="84b3b-156">4</span></span> |
| <span data-ttu-id="84b3b-157">20150701</span><span class="sxs-lookup"><span data-stu-id="84b3b-157">20150701</span></span> |<span data-ttu-id="84b3b-158">3</span><span class="sxs-lookup"><span data-stu-id="84b3b-158">3</span></span> |<span data-ttu-id="84b3b-159">1</span><span class="sxs-lookup"><span data-stu-id="84b3b-159">1</span></span> |
| <span data-ttu-id="84b3b-160">20150801</span><span class="sxs-lookup"><span data-stu-id="84b3b-160">20150801</span></span> |<span data-ttu-id="84b3b-161">3</span><span class="sxs-lookup"><span data-stu-id="84b3b-161">3</span></span> |<span data-ttu-id="84b3b-162">1</span><span class="sxs-lookup"><span data-stu-id="84b3b-162">1</span></span> |
| <span data-ttu-id="84b3b-163">20150801</span><span class="sxs-lookup"><span data-stu-id="84b3b-163">20150801</span></span> |<span data-ttu-id="84b3b-164">3</span><span class="sxs-lookup"><span data-stu-id="84b3b-164">3</span></span> |<span data-ttu-id="84b3b-165">1</span><span class="sxs-lookup"><span data-stu-id="84b3b-165">1</span></span> |
| <span data-ttu-id="84b3b-166">20151001</span><span class="sxs-lookup"><span data-stu-id="84b3b-166">20151001</span></span> |<span data-ttu-id="84b3b-167">4</span><span class="sxs-lookup"><span data-stu-id="84b3b-167">4</span></span> |<span data-ttu-id="84b3b-168">2</span><span class="sxs-lookup"><span data-stu-id="84b3b-168">2</span></span> |
| <span data-ttu-id="84b3b-169">20151101</span><span class="sxs-lookup"><span data-stu-id="84b3b-169">20151101</span></span> |<span data-ttu-id="84b3b-170">4</span><span class="sxs-lookup"><span data-stu-id="84b3b-170">4</span></span> |<span data-ttu-id="84b3b-171">2</span><span class="sxs-lookup"><span data-stu-id="84b3b-171">2</span></span> |
| <span data-ttu-id="84b3b-172">20151201</span><span class="sxs-lookup"><span data-stu-id="84b3b-172">20151201</span></span> |<span data-ttu-id="84b3b-173">4</span><span class="sxs-lookup"><span data-stu-id="84b3b-173">4</span></span> |<span data-ttu-id="84b3b-174">2</span><span class="sxs-lookup"><span data-stu-id="84b3b-174">2</span></span> |

## <a name="4-create-statistics"></a><span data-ttu-id="84b3b-175">4. Create statistics</span><span class="sxs-lookup"><span data-stu-id="84b3b-175">4. Create statistics</span></span>
<span data-ttu-id="84b3b-176">SQL Data Warehouse ne prend pas encore en charge les statistiques à création ou mise à jour automatique.</span><span class="sxs-lookup"><span data-stu-id="84b3b-176">SQL Data Warehouse does not yet support auto-create or auto-update statistics.</span></span> <span data-ttu-id="84b3b-177">tooget hello meilleures performances des requêtes, il est important toocreate des statistiques sur toutes les colonnes de toutes les tables après le premier chargement de hello ou toutes les modifications importantes se produisent dans les données de salutation.</span><span class="sxs-lookup"><span data-stu-id="84b3b-177">tooget hello best query performance, it's important toocreate statistics on all columns of all tables after hello first load or after any substantial changes occur in hello data.</span></span> <span data-ttu-id="84b3b-178">Pour obtenir une explication détaillée des statistiques, consultez [Statistiques][Statistics].</span><span class="sxs-lookup"><span data-stu-id="84b3b-178">For a detailed explanation of statistics, see [Statistics][Statistics].</span></span> 

<span data-ttu-id="84b3b-179">La commande suivante d’exécution hello toocreate des statistiques sur la table qui vient d’être chargée.</span><span class="sxs-lookup"><span data-stu-id="84b3b-179">Run hello following command toocreate statistics on your newly loaded table.</span></span>

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "
    create statistics [DateId] on [DimDate2] ([DateId]);
    create statistics [CalendarQuarter] on [DimDate2] ([CalendarQuarter]);
    create statistics [FiscalQuarter] on [DimDate2] ([FiscalQuarter]);
"
```

## <a name="5-export-data-from-sql-data-warehouse"></a><span data-ttu-id="84b3b-180">5. Exporter des données de SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="84b3b-180">5. Export data from SQL Data Warehouse</span></span>
<span data-ttu-id="84b3b-181">Pour vous amuser, vous pouvez exporter les données de hello chargée hors de l’entrepôt de données SQL.</span><span class="sxs-lookup"><span data-stu-id="84b3b-181">For fun, you can export hello data that you just loaded back out of SQL Data Warehouse.</span></span>  <span data-ttu-id="84b3b-182">tooexport de commande Hello est exactement hello identique à l’exportation à partir de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="84b3b-182">hello command tooexport is exactly hello same as exporting from SQL Server.</span></span>

<span data-ttu-id="84b3b-183">Toutefois, il est d’une différence dans les résultats de hello.</span><span class="sxs-lookup"><span data-stu-id="84b3b-183">However, there is a difference in hello results.</span></span> <span data-ttu-id="84b3b-184">Étant donné que les données de salutation sont stockées dans des emplacements distribués au sein de l’entrepôt de données SQL, lorsque vous exportez des données de chaque nœud de calcul écrit fichier de sortie toohello de données.</span><span class="sxs-lookup"><span data-stu-id="84b3b-184">Since hello data is stored in distributed locations within SQL Data Warehouse, when you export data each Compute node writes it data toohello output file.</span></span> <span data-ttu-id="84b3b-185">commande Hello de données hello dans le fichier de sortie hello est probablement toobe autre que l’ordre de hello de données hello dans le fichier d’entrée de hello.</span><span class="sxs-lookup"><span data-stu-id="84b3b-185">hello order of hello data in hello output file is likely toobe different than hello order of hello data in hello input file.</span></span>

### <a name="export-a-table-and-compare-exported-results"></a><span data-ttu-id="84b3b-186">Exporter une table et comparer les résultats exportés</span><span class="sxs-lookup"><span data-stu-id="84b3b-186">Export a table and compare exported results</span></span>
<span data-ttu-id="84b3b-187">toosee hello données exportées, ouvrez une invite de commandes et exécuter cette commande à l’aide de vos propres paramètres.</span><span class="sxs-lookup"><span data-stu-id="84b3b-187">toosee hello exported data, open a command prompt and run this command using your own parameters.</span></span> <span data-ttu-id="84b3b-188">Nom_serveur est le nom hello de votre serveur de SQL Azure logiques.</span><span class="sxs-lookup"><span data-stu-id="84b3b-188">ServerName is hello name of your Azure logical SQL Server.</span></span>

```sql
bcp DimDate2 out C:\Temp\DimDate2_export.txt -S <Server Name> -d <Database Name> -U <Username> -P <password> -q -c -t ','
```
<span data-ttu-id="84b3b-189">Vous pouvez vérifier hello données a été correctement exportées en ouvrant le fichier hello.</span><span class="sxs-lookup"><span data-stu-id="84b3b-189">You can verify hello data was exported correctly by opening hello new file.</span></span> <span data-ttu-id="84b3b-190">données Hello dans le fichier de hello doivent correspondre au texte hello ci-dessous, mais il seront probablement être triées dans un ordre différent :</span><span class="sxs-lookup"><span data-stu-id="84b3b-190">hello data in hello file should match hello text below, but will likely be sorted in a different order:</span></span>

```
20150301,1,3
20150501,2,4
20151001,4,2
20150201,1,3
20151201,4,2
20150801,3,1
20150601,2,4
20151101,4,2
20150401,2,4
20150701,3,1
20150901,3,1
20150101,1,3
```

### <a name="export-hello-results-of-a-query"></a><span data-ttu-id="84b3b-191">Exporter les résultats d’une requête hello</span><span class="sxs-lookup"><span data-stu-id="84b3b-191">Export hello results of a query</span></span>
<span data-ttu-id="84b3b-192">Vous pouvez utiliser hello **queryout** fonction des résultats de hello bcp tooexport d’une requête plutôt que d’exporter la totalité de la table hello.</span><span class="sxs-lookup"><span data-stu-id="84b3b-192">You can use hello **queryout** function of bcp tooexport hello results of a query instead of exporting hello entire table.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="84b3b-193">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="84b3b-193">Next steps</span></span>
<span data-ttu-id="84b3b-194">Pour accéder à une vue d’ensemble du chargement, consultez [Charger des données dans SQL Data Warehouse][Load data into SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="84b3b-194">For an overview of loading, see [Load data into SQL Data Warehouse][Load data into SQL Data Warehouse].</span></span>
<span data-ttu-id="84b3b-195">Pour obtenir des conseils supplémentaires en matière de développement, consultez l’article [Vue d’ensemble sur le développement SQL Data Warehouse][SQL Data Warehouse development overview].</span><span class="sxs-lookup"><span data-stu-id="84b3b-195">For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>
<span data-ttu-id="84b3b-196">Pour plus d’informations sur la création d’une table sur SQL Data Warehouse, consultez [Vue d’ensemble des tables][Table Overview] ou la syntaxe [CREATE TABLE][CREATE TABLE syntax].</span><span class="sxs-lookup"><span data-stu-id="84b3b-196">See [Table Overview][Table Overview] or [CREATE TABLE syntax][CREATE TABLE syntax] for more information about creating a table on SQL Data Warehouse.</span></span>

<!--Image references-->

<!--Article references-->

[Load data into SQL Data Warehouse]: ./sql-data-warehouse-overview-load.md
[SQL Data Warehouse development overview]: ./sql-data-warehouse-overview-develop.md
[Table Overview]: ./sql-data-warehouse-tables-overview.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md

<!--MSDN references-->
[bcp]: https://msdn.microsoft.com/library/ms162802.aspx
[CREATE TABLE syntax]: https://msdn.microsoft.com/library/mt203953.aspx

<!--Other Web references-->
[Microsoft Download Center]: https://www.microsoft.com/download/details.aspx?id=36433
