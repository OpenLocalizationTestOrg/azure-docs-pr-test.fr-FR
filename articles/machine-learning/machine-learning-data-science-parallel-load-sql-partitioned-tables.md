---
title: "Créer et optimiser des tables pour une importation en parallèle rapide des données dans un serveur SQL Server sur une machine virtuelle Azure | Microsoft Docs"
description: "Importer des données en parallèle et en bloc à l’aide de tables de partition SQL"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: ff90fdb0-5bc7-49e8-aee7-678b54f901c8
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: bradsev
ms.openlocfilehash: aae4e4f59e76bf48b00a2ee92aedd7d5643ba91a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="parallel-bulk-data-import-using-sql-partition-tables"></a><span data-ttu-id="aa9a6-103">Importer des données en parallèle et en bloc à l’aide de tables de partition SQL</span><span class="sxs-lookup"><span data-stu-id="aa9a6-103">Parallel Bulk Data Import Using SQL Partition Tables</span></span>
<span data-ttu-id="aa9a6-104">Ce document décrit comment créer une ou plusieurs tables partitionnées pour importer des données rapidement, en parallèle et en bloc dans une base de données SQL Server.</span><span class="sxs-lookup"><span data-stu-id="aa9a6-104">This document describes how to build partitioned tables for fast parallel bulk importing of data to a SQL Server database.</span></span> <span data-ttu-id="aa9a6-105">Dans le cas d’un chargement ou d’un transfert volumineux dans une base de données SQL, les *vues et tables partitionnées*permettent d’améliorer l’importation des données et le traitement des requêtes.</span><span class="sxs-lookup"><span data-stu-id="aa9a6-105">For big data loading/transfer to a SQL database, importing data to the SQL DB and subsequent queries can be improved by using *Partitioned Tables and Views*.</span></span> 

## <a name="create-a-new-database-and-a-set-of-filegroups"></a><span data-ttu-id="aa9a6-106">Créer une base de données et un ensemble de groupes de fichiers</span><span class="sxs-lookup"><span data-stu-id="aa9a6-106">Create a new database and a set of filegroups</span></span>
* <span data-ttu-id="aa9a6-107">[Créez une base de données](https://technet.microsoft.com/library/ms176061.aspx) (si elle n’existe pas).</span><span class="sxs-lookup"><span data-stu-id="aa9a6-107">[Create a new database](https://technet.microsoft.com/library/ms176061.aspx), if it doesn't exist already.</span></span>
* <span data-ttu-id="aa9a6-108">Ajoutez des groupes de fichiers de base de données à la base de données qui contiendra les fichiers physiques partitionnés. Pour cette opération, utilisez [CREATE DATABASE](https://technet.microsoft.com/library/ms176061.aspx) si la base de données n’existe pas ou [ALTER DATABASE](https://msdn.microsoft.com/library/bb522682.aspx) si elle existe.</span><span class="sxs-lookup"><span data-stu-id="aa9a6-108">Add database filegroups to the database which will hold the partitioned physical files.This can be done with [CREATE DATABASE](https://technet.microsoft.com/library/ms176061.aspx) if new or [ALTER DATABASE](https://msdn.microsoft.com/library/bb522682.aspx) if the database exists already.</span></span>
* <span data-ttu-id="aa9a6-109">Ajoutez un ou plusieurs fichiers (selon le cas) dans chaque groupe de fichiers de base de données.</span><span class="sxs-lookup"><span data-stu-id="aa9a6-109">Add one or more files (as needed) to each database filegroup.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="aa9a6-110">Spécifiez le groupe de fichiers cible qui contiennent les données de cette partition, ainsi que le nom du ou des fichiers physiques de base de données qui stockeront les données du groupe de fichiers.</span><span class="sxs-lookup"><span data-stu-id="aa9a6-110">Specify the target filegroup which holds data for this partition and the physical database file name(s) where the filegroup data will be stored.</span></span>
  > 
  > 

<span data-ttu-id="aa9a6-111">L’exemple suivant crée une base de données avec trois groupes de fichiers autres que le groupe principal et le groupe de journalisation, chacun contenant un fichier physique</span><span class="sxs-lookup"><span data-stu-id="aa9a6-111">The following example creates a new database with three filegroups other than the primary and log groups, containing one physical file in each.</span></span> <span data-ttu-id="aa9a6-112">Les fichiers de la base de données sont créés dans le dossier de données SQL Server par défaut configuré dans l’instance SQL Server.</span><span class="sxs-lookup"><span data-stu-id="aa9a6-112">The database files are created in the default SQL Server Data folder, as configured in the SQL Server instance.</span></span> <span data-ttu-id="aa9a6-113">Pour plus d’informations sur les emplacements par défaut des fichiers, consultez l’article [Emplacement des fichiers pour les instances par défaut et nommées de SQL Server](https://msdn.microsoft.com/library/ms143547.aspx).</span><span class="sxs-lookup"><span data-stu-id="aa9a6-113">For more information about the default file locations, see [File Locations for Default and Named Instances of SQL Server](https://msdn.microsoft.com/library/ms143547.aspx).</span></span>

    DECLARE @data_path nvarchar(256);
    SET @data_path = (SELECT SUBSTRING(physical_name, 1, CHARINDEX(N'master.mdf', LOWER(physical_name)) - 1)
      FROM master.sys.master_files
      WHERE database_id = 1 AND file_id = 1);

    EXECUTE ('
        CREATE DATABASE <database_name>
         ON  PRIMARY 
        ( NAME = ''Primary'', FILENAME = ''' + @data_path + '<primary_file_name>.mdf'', SIZE = 4096KB , FILEGROWTH = 1024KB ), 
         FILEGROUP [filegroup_1] 
        ( NAME = ''FileGroup1'', FILENAME = ''' + @data_path + '<file_name_1>.ndf'' , SIZE = 4096KB , FILEGROWTH = 1024KB ), 
         FILEGROUP [filegroup_2] 
        ( NAME = ''FileGroup1'', FILENAME = ''' + @data_path + '<file_name_2>.ndf'' , SIZE = 4096KB , FILEGROWTH = 1024KB ), 
         FILEGROUP [filegroup_3] 
        ( NAME = ''FileGroup1'', FILENAME = ''' + @data_path + '<file_name>.ndf'' , SIZE = 102400KB , FILEGROWTH = 10240KB ), 
         LOG ON 
        ( NAME = ''LogFileGroup'', FILENAME = ''' + @data_path + '<log_file_name>.ldf'' , SIZE = 1024KB , FILEGROWTH = 10%)
    ')

## <a name="create-a-partitioned-table"></a><span data-ttu-id="aa9a6-114">Créer une table partitionnée</span><span class="sxs-lookup"><span data-stu-id="aa9a6-114">Create a partitioned table</span></span>
<span data-ttu-id="aa9a6-115">Créez une ou plusieurs tables partitionnées, selon le schéma de données, et mappez-les aux groupes de fichiers de base de données créés à l’étape précédente.</span><span class="sxs-lookup"><span data-stu-id="aa9a6-115">Create partitioned table(s) according to the data schema, mapped to the database filegroups created in the previous step.</span></span> <span data-ttu-id="aa9a6-116">Une fois les données importées en bloc dans la ou les tables partitionnées, les enregistrements sont répartis dans les groupes de fichiers selon un schéma de partition, comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="aa9a6-116">When data is bulk imported to the partitioned table(s), records will be distributed among the filegroups according to a partition scheme, as described below.</span></span>

<span data-ttu-id="aa9a6-117">**Pour créer une table de partition, vous devez :**</span><span class="sxs-lookup"><span data-stu-id="aa9a6-117">**To create a partition table, you need to:**</span></span>

* <span data-ttu-id="aa9a6-118">[Créer une fonction de partition](https://msdn.microsoft.com/library/ms187802.aspx) qui définit la plage de valeurs/limites à inclure dans chaque table de partition, par exemple, pour limiter les partitions mensuelles (some\_datetime\_field) de l’année 2013 :</span><span class="sxs-lookup"><span data-stu-id="aa9a6-118">[Create a partition function](https://msdn.microsoft.com/library/ms187802.aspx) which defines the range of values/boundaries to be included in each individual partition table, e.g., to limit partitions by month(some\_datetime\_field) in the year 2013:</span></span>
  
        CREATE PARTITION FUNCTION <DatetimeFieldPFN>(<datetime_field>)  
        AS RANGE RIGHT FOR VALUES (
            '20130201', '20130301', '20130401',
            '20130501', '20130601', '20130701', '20130801',
            '20130901', '20131001', '20131101', '20131201' )
* <span data-ttu-id="aa9a6-119">[Créer un schéma de partition](https://msdn.microsoft.com/library/ms179854.aspx) qui mappe chaque plage de la fonction de partition à un groupe de fichiers physique, par exemple :</span><span class="sxs-lookup"><span data-stu-id="aa9a6-119">[Create a partition scheme](https://msdn.microsoft.com/library/ms179854.aspx) which maps each partition range in the partition function to a physical filegroup, e.g.:</span></span>
  
        CREATE PARTITION SCHEME <DatetimeFieldPScheme> AS  
        PARTITION <DatetimeFieldPFN> TO (
        <filegroup_1>, <filegroup_2>, <filegroup_3>, <filegroup_4>,
        <filegroup_5>, <filegroup_6>, <filegroup_7>, <filegroup_8>,
        <filegroup_9>, <filegroup_10>, <filegroup_11>, <filegroup_12> )
  
  <span data-ttu-id="aa9a6-120">pour vérifier les plages de chaque partition selon la fonction et le schéma, exécutez la requête suivante :</span><span class="sxs-lookup"><span data-stu-id="aa9a6-120">To verify the ranges in effect in each partition according to the function/scheme, run the following query:</span></span>
  
        SELECT psch.name as PartitionScheme,
            prng.value AS ParitionValue,
            prng.boundary_id AS BoundaryID
        FROM sys.partition_functions AS pfun
        INNER JOIN sys.partition_schemes psch ON pfun.function_id = psch.function_id
        INNER JOIN sys.partition_range_values prng ON prng.function_id=pfun.function_id
        WHERE pfun.name = <DatetimeFieldPFN>
* <span data-ttu-id="aa9a6-121">[Créer une ou plusieurs tables partitionnées](https://msdn.microsoft.com/library/ms174979.aspx)selon votre schéma de données, puis spécifiez le schéma de partition et le champ de contrainte utilisé pour partitionner la table, par exemple :</span><span class="sxs-lookup"><span data-stu-id="aa9a6-121">[Create partitioned table](https://msdn.microsoft.com/library/ms174979.aspx)(s) according to your data schema, and specify the partition scheme and constraint field used to partition the table, e.g.:</span></span>
  
        CREATE TABLE <table_name> ( [include schema definition here] )
        ON <TablePScheme>(<partition_field>)

<span data-ttu-id="aa9a6-122">Pour plus d’informations, consultez l’article [Créer des tables partitionnées et des index](https://msdn.microsoft.com/library/ms188730.aspx).</span><span class="sxs-lookup"><span data-stu-id="aa9a6-122">For more information, see [Create Partitioned Tables and Indexes](https://msdn.microsoft.com/library/ms188730.aspx).</span></span>

## <a name="bulk-import-the-data-for-each-individual-partition-table"></a><span data-ttu-id="aa9a6-123">Importer les données en bloc dans chaque table de partition</span><span class="sxs-lookup"><span data-stu-id="aa9a6-123">Bulk import the data for each individual partition table</span></span>
* <span data-ttu-id="aa9a6-124">Vous pouvez utiliser BCP, BULK INSERT ou d’autres méthodes telles que l’ [Assistant Migration SQL Server](http://sqlazuremw.codeplex.com/).</span><span class="sxs-lookup"><span data-stu-id="aa9a6-124">You may use BCP, BULK INSERT, or other methods such as [SQL Server Migration Wizard](http://sqlazuremw.codeplex.com/).</span></span> <span data-ttu-id="aa9a6-125">L’exemple fourni utilise la méthode BCP.</span><span class="sxs-lookup"><span data-stu-id="aa9a6-125">The example provided uses the BCP method.</span></span>
* <span data-ttu-id="aa9a6-126">[Modifiez la base de données](https://msdn.microsoft.com/library/bb522682.aspx) en remplaçant le schéma de journalisation des transactions par BULK_LOGGED pour minimiser le temps de traitement de la journalisation, par exemple :</span><span class="sxs-lookup"><span data-stu-id="aa9a6-126">[Alter the database](https://msdn.microsoft.com/library/bb522682.aspx) to change transaction logging scheme to BULK_LOGGED to minimize overhead of logging, e.g.:</span></span>
  
        ALTER DATABASE <database_name> SET RECOVERY BULK_LOGGED
* <span data-ttu-id="aa9a6-127">Pour accélérer le chargement des données, lancez plusieurs importations en bloc en parallèle.</span><span class="sxs-lookup"><span data-stu-id="aa9a6-127">To expedite data loading, launch the bulk import operations in parallel.</span></span> <span data-ttu-id="aa9a6-128">Pour obtenir des conseils sur l’accélération de l’importation en bloc de volumes importants dans des bases de données SQL Server, consultez l’article [Charger 1 To en moins d’une heure](http://blogs.msdn.com/b/sqlcat/archive/2006/05/19/602142.aspx).</span><span class="sxs-lookup"><span data-stu-id="aa9a6-128">For tips on expediting bulk importing of big data into SQL Server databases, see [Load 1TB in less than 1 hour](http://blogs.msdn.com/b/sqlcat/archive/2006/05/19/602142.aspx).</span></span>

<span data-ttu-id="aa9a6-129">Le script PowerShell suivant est un exemple de chargement de données en parallèle avec BCP.</span><span class="sxs-lookup"><span data-stu-id="aa9a6-129">The following PowerShell script is an example of parallel data loading using BCP.</span></span>

    # Set database name, input data directory, and output log directory
    # This example loads comma-separated input data files
    # The example assumes the partitioned data files are named as <base_file_name>_<partition_number>.csv
    # Assumes the input data files include a header line. Loading starts at line number 2.

    $dbname = "<database_name>"
    $indir  = "<path_to_data_files>"
    $logdir = "<path_to_log_directory>"

    # Select authentication mode
    $sqlauth = 0

    # For SQL authentication, set the server and user credentials
    $sqlusr = "<user@server>"
    $server = "<tcp:serverdns>"
    $pass   = "<password>"

    # Set number of partitions per table - Should match the number of input data files per table
    $numofparts = <number_of_partitions>

    # Set table name to be loaded, basename of input data files, input format file, and number of partitions
    $tbname = "<table_name>"
    $basename = "<base_input_data_filename_no_extension>"
    $fmtfile = "<full_path_to_format_file>"

    # Create log directory if it does not exist
    New-Item -ErrorAction Ignore -ItemType directory -Path $logdir

    # BCP example using Windows authentication
    $ScriptBlock1 = {
       param($dbname, $tbname, $basename, $fmtfile, $indir, $logdir, $num)
       bcp ($dbname + ".." + $tbname) in ($indir + "\" + $basename + "_" + $num + ".csv") -o ($logdir + "\" + $tbname + "_" + $num + ".txt") -h "TABLOCK" -F 2 -C "RAW" -f ($fmtfile) -T -b 2500 -t "," -r \n
    }

    # BCP example using SQL authentication
    $ScriptBlock2 = {
       param($dbname, $tbname, $basename, $fmtfile, $indir, $logdir, $num, $sqlusr, $server, $pass)
       bcp ($dbname + ".." + $tbname) in ($indir + "\" + $basename + "_" + $num + ".csv") -o ($logdir + "\" + $tbname + "_" + $num + ".txt") -h "TABLOCK" -F 2 -C "RAW" -f ($fmtfile) -U $sqlusr -S $server -P $pass -b 2500 -t "," -r \n
    }

    # Background processing of all partitions
    for ($i=1; $i -le $numofparts; $i++)
    {
       Write-Output "Submit loading trip and fare partitions # $i"
       if ($sqlauth -eq 0) {
          # Use Windows authentication
          Start-Job -ScriptBlock $ScriptBlock1 -Arg ($dbname, $tbname, $basename, $fmtfile, $indir, $logdir, $i)
       } 
       else {
          # Use SQL authentication
          Start-Job -ScriptBlock $ScriptBlock2 -Arg ($dbname, $tbname, $basename, $fmtfile, $indir, $logdir, $i, $sqlusr, $server, $pass)
       }
    }

    Get-Job

    # Optional - Wait till all jobs complete and report date and time
    date
    While (Get-Job -State "Running") { Start-Sleep 10 }
    date


## <a name="create-indexes-to-optimize-joins-and-query-performance"></a><span data-ttu-id="aa9a6-130">Créer des index pour optimiser les jointures et le traitement des requêtes</span><span class="sxs-lookup"><span data-stu-id="aa9a6-130">Create indexes to optimize joins and query performance</span></span>
* <span data-ttu-id="aa9a6-131">Si vous extrayez des données de plusieurs tables à des fins de modélisation, créez des index sur les clés de jointure pour améliorer les performances des jointures.</span><span class="sxs-lookup"><span data-stu-id="aa9a6-131">If you will extract data for modeling from multiple tables, create indexes on the join keys to improve the join performance.</span></span>
* <span data-ttu-id="aa9a6-132">[Créez des index](https://technet.microsoft.com/library/ms188783.aspx) (clusterisés ou non) ciblant le même groupe de fichiers de chaque partition, par exemple :</span><span class="sxs-lookup"><span data-stu-id="aa9a6-132">[Create indexes](https://technet.microsoft.com/library/ms188783.aspx) (clustered or non-clustered) targeting the same filegroup for each partition, for e.g.:</span></span>
  
        CREATE CLUSTERED INDEX <table_idx> ON <table_name>( [include index columns here] )
        ON <TablePScheme>(<partition)field>)
  <span data-ttu-id="aa9a6-133">ou</span><span class="sxs-lookup"><span data-stu-id="aa9a6-133">or,</span></span>
  
        CREATE INDEX <table_idx> ON <table_name>( [include index columns here] )
        ON <TablePScheme>(<partition)field>)
  
  > [!NOTE]
  > <span data-ttu-id="aa9a6-134">Vous pouvez créer les index avant d’importer les données en bloc.</span><span class="sxs-lookup"><span data-stu-id="aa9a6-134">You may choose to create the indexes before bulk importing the data.</span></span> <span data-ttu-id="aa9a6-135">Mais la création des index avant l’opération d’importation ralentira le chargement des données.</span><span class="sxs-lookup"><span data-stu-id="aa9a6-135">Index creation before bulk importing will slow down the data loading.</span></span>
  > 
  > 

## <a name="advanced-analytics-process-and-technology-in-action-example"></a><span data-ttu-id="aa9a6-136">Exemple de processus d’analyse avancé et technologie en action</span><span class="sxs-lookup"><span data-stu-id="aa9a6-136">Advanced Analytics Process and Technology in Action Example</span></span>
<span data-ttu-id="aa9a6-137">Pour obtenir un exemple de procédure pas à pas complet utilisant le processus Cortana Analytics avec un jeu de données public, consultez [Processus Cortana Analytics en action : utilisation de SQL Server](machine-learning-data-science-process-sql-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="aa9a6-137">For an end-to-end walkthrough example using the Cortana Analytics Process with a public dataset, see [Cortana Analytics Process in Action: using SQL Server](machine-learning-data-science-process-sql-walkthrough.md).</span></span>

