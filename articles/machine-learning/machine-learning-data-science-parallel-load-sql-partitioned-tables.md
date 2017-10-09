---
title: "aaaBuild et optimiser des tables pour l’importation parallèle rapide des données dans un serveur SQL Server sur une machine virtuelle Azure | Documents Microsoft"
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
ms.openlocfilehash: ab748c47348ec6ca3b98ba39e27181bba5d36fc0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="parallel-bulk-data-import-using-sql-partition-tables"></a><span data-ttu-id="df38d-103">Importer des données en parallèle et en bloc à l’aide de tables de partition SQL</span><span class="sxs-lookup"><span data-stu-id="df38d-103">Parallel Bulk Data Import Using SQL Partition Tables</span></span>
<span data-ttu-id="df38d-104">Ce document décrit le mode de partition des tables pour l’importation d’accélérée parallèle en bloc de base de données SQL Server de données tooa toobuild.</span><span class="sxs-lookup"><span data-stu-id="df38d-104">This document describes how toobuild partitioned tables for fast parallel bulk importing of data tooa SQL Server database.</span></span> <span data-ttu-id="df38d-105">Pour base de données volumineuses chargement/transfert tooa SQL, l’importation de données toohello base de données SQL et les requêtes suivantes peut être améliorée à l’aide de *Partitioned Tables et vues*.</span><span class="sxs-lookup"><span data-stu-id="df38d-105">For big data loading/transfer tooa SQL database, importing data toohello SQL DB and subsequent queries can be improved by using *Partitioned Tables and Views*.</span></span> 

## <a name="create-a-new-database-and-a-set-of-filegroups"></a><span data-ttu-id="df38d-106">Créer une base de données et un ensemble de groupes de fichiers</span><span class="sxs-lookup"><span data-stu-id="df38d-106">Create a new database and a set of filegroups</span></span>
* <span data-ttu-id="df38d-107">[Créez une base de données](https://technet.microsoft.com/library/ms176061.aspx) (si elle n’existe pas).</span><span class="sxs-lookup"><span data-stu-id="df38d-107">[Create a new database](https://technet.microsoft.com/library/ms176061.aspx), if it doesn't exist already.</span></span>
* <span data-ttu-id="df38d-108">Ajouter la base de données toohello de groupes de fichiers de base de données qui contiendra les fichiers physiques hello partitionnée. Cela peut être fait avec [CREATE DATABASE](https://technet.microsoft.com/library/ms176061.aspx) si de nouveaux ou [ALTER DATABASE](https://msdn.microsoft.com/library/bb522682.aspx) si la base de données hello existe déjà.</span><span class="sxs-lookup"><span data-stu-id="df38d-108">Add database filegroups toohello database which will hold hello partitioned physical files.This can be done with [CREATE DATABASE](https://technet.microsoft.com/library/ms176061.aspx) if new or [ALTER DATABASE](https://msdn.microsoft.com/library/bb522682.aspx) if hello database exists already.</span></span>
* <span data-ttu-id="df38d-109">Ajoutez un ou plusieurs fichiers de base de données tooeach de fichiers (si nécessaire).</span><span class="sxs-lookup"><span data-stu-id="df38d-109">Add one or more files (as needed) tooeach database filegroup.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="df38d-110">Spécifiez le groupe de fichiers hello cible qui contient les données de cette partition et hello physique de la base de données fichier nom (s) où les données du groupe de fichiers hello seront stockées.</span><span class="sxs-lookup"><span data-stu-id="df38d-110">Specify hello target filegroup which holds data for this partition and hello physical database file name(s) where hello filegroup data will be stored.</span></span>
  > 
  > 

<span data-ttu-id="df38d-111">Hello exemple suivant crée une nouvelle base de données avec trois groupes de fichiers autres que hello principal et les groupes de journaux, qui contient un fichier physique dans chacun.</span><span class="sxs-lookup"><span data-stu-id="df38d-111">hello following example creates a new database with three filegroups other than hello primary and log groups, containing one physical file in each.</span></span> <span data-ttu-id="df38d-112">fichiers de base de données de Hello sont créés dans le dossier de données SQL Server par défaut hello, tel que configuré dans l’instance de SQL Server hello.</span><span class="sxs-lookup"><span data-stu-id="df38d-112">hello database files are created in hello default SQL Server Data folder, as configured in hello SQL Server instance.</span></span> <span data-ttu-id="df38d-113">Pour plus d’informations sur les emplacements de fichier par défaut hello, consultez [emplacements des fichiers pour la valeur par défaut et nommé d’Instances de SQL Server](https://msdn.microsoft.com/library/ms143547.aspx).</span><span class="sxs-lookup"><span data-stu-id="df38d-113">For more information about hello default file locations, see [File Locations for Default and Named Instances of SQL Server](https://msdn.microsoft.com/library/ms143547.aspx).</span></span>

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

## <a name="create-a-partitioned-table"></a><span data-ttu-id="df38d-114">Créer une table partitionnée</span><span class="sxs-lookup"><span data-stu-id="df38d-114">Create a partitioned table</span></span>
<span data-ttu-id="df38d-115">Créer une ou plusieurs tables partitionnées selon le schéma de données toohello, groupes de fichiers de base de données mappé toohello créé à l’étape précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="df38d-115">Create partitioned table(s) according toohello data schema, mapped toohello database filegroups created in hello previous step.</span></span> <span data-ttu-id="df38d-116">Lorsque les données sont importées en bloc toohello partitionné une ou plusieurs tables, les enregistrements sont répartis entre les groupes de fichiers hello selon le schéma de partition tooa, comme décrit ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="df38d-116">When data is bulk imported toohello partitioned table(s), records will be distributed among hello filegroups according tooa partition scheme, as described below.</span></span>

<span data-ttu-id="df38d-117">**toocreate une table de partition, vous devez :**</span><span class="sxs-lookup"><span data-stu-id="df38d-117">**toocreate a partition table, you need to:**</span></span>

* <span data-ttu-id="df38d-118">[Créer une fonction de partition](https://msdn.microsoft.com/library/ms187802.aspx) qui définit la plage des valeurs/limites toobe hello inclus dans chaque table de partition individuelle, par exemple, les partitions toolimit par mois (certains\_datetime\_champ) dans l’année hello 2013 :</span><span class="sxs-lookup"><span data-stu-id="df38d-118">[Create a partition function](https://msdn.microsoft.com/library/ms187802.aspx) which defines hello range of values/boundaries toobe included in each individual partition table, e.g., toolimit partitions by month(some\_datetime\_field) in hello year 2013:</span></span>
  
        CREATE PARTITION FUNCTION <DatetimeFieldPFN>(<datetime_field>)  
        AS RANGE RIGHT FOR VALUES (
            '20130201', '20130301', '20130401',
            '20130501', '20130601', '20130701', '20130801',
            '20130901', '20131001', '20131101', '20131201' )
* <span data-ttu-id="df38d-119">[Créer un schéma de partition](https://msdn.microsoft.com/library/ms179854.aspx) qui mappe chaque plage de partition dans hello partition fonction tooa groupe de fichiers physique, par exemple :</span><span class="sxs-lookup"><span data-stu-id="df38d-119">[Create a partition scheme](https://msdn.microsoft.com/library/ms179854.aspx) which maps each partition range in hello partition function tooa physical filegroup, e.g.:</span></span>
  
        CREATE PARTITION SCHEME <DatetimeFieldPScheme> AS  
        PARTITION <DatetimeFieldPFN> too(
        <filegroup_1>, <filegroup_2>, <filegroup_3>, <filegroup_4>,
        <filegroup_5>, <filegroup_6>, <filegroup_7>, <filegroup_8>,
        <filegroup_9>, <filegroup_10>, <filegroup_11>, <filegroup_12> )
  
  <span data-ttu-id="df38d-120">plages de hello tooverify en vigueur dans chaque conséquente toohello fonction/schéma de partition, exécutez hello suivant la requête :</span><span class="sxs-lookup"><span data-stu-id="df38d-120">tooverify hello ranges in effect in each partition according toohello function/scheme, run hello following query:</span></span>
  
        SELECT psch.name as PartitionScheme,
            prng.value AS ParitionValue,
            prng.boundary_id AS BoundaryID
        FROM sys.partition_functions AS pfun
        INNER JOIN sys.partition_schemes psch ON pfun.function_id = psch.function_id
        INNER JOIN sys.partition_range_values prng ON prng.function_id=pfun.function_id
        WHERE pfun.name = <DatetimeFieldPFN>
* <span data-ttu-id="df38d-121">[Créer une table partitionnée](https://msdn.microsoft.com/library/ms174979.aspx)(s) en fonction du schéma de données tooyour et indiquer le champ de schéma et de contrainte de partition hello utilisé toopartition table de hello, par exemple :</span><span class="sxs-lookup"><span data-stu-id="df38d-121">[Create partitioned table](https://msdn.microsoft.com/library/ms174979.aspx)(s) according tooyour data schema, and specify hello partition scheme and constraint field used toopartition hello table, e.g.:</span></span>
  
        CREATE TABLE <table_name> ( [include schema definition here] )
        ON <TablePScheme>(<partition_field>)

<span data-ttu-id="df38d-122">Pour plus d’informations, consultez l’article [Créer des tables partitionnées et des index](https://msdn.microsoft.com/library/ms188730.aspx).</span><span class="sxs-lookup"><span data-stu-id="df38d-122">For more information, see [Create Partitioned Tables and Indexes](https://msdn.microsoft.com/library/ms188730.aspx).</span></span>

## <a name="bulk-import-hello-data-for-each-individual-partition-table"></a><span data-ttu-id="df38d-123">Importer en bloc hello des données pour chaque table de partition individuelle</span><span class="sxs-lookup"><span data-stu-id="df38d-123">Bulk import hello data for each individual partition table</span></span>
* <span data-ttu-id="df38d-124">Vous pouvez utiliser BCP, BULK INSERT ou d’autres méthodes telles que l’ [Assistant Migration SQL Server](http://sqlazuremw.codeplex.com/).</span><span class="sxs-lookup"><span data-stu-id="df38d-124">You may use BCP, BULK INSERT, or other methods such as [SQL Server Migration Wizard](http://sqlazuremw.codeplex.com/).</span></span> <span data-ttu-id="df38d-125">exemple Hello fourni utilise la méthode BCP hello.</span><span class="sxs-lookup"><span data-stu-id="df38d-125">hello example provided uses hello BCP method.</span></span>
* <span data-ttu-id="df38d-126">[Modifier la base de données hello](https://msdn.microsoft.com/library/bb522682.aspx) transaction toochange schéma tooBULK_LOGGED toominimize surcharge de la journalisation, par exemple, d’enregistrement :</span><span class="sxs-lookup"><span data-stu-id="df38d-126">[Alter hello database](https://msdn.microsoft.com/library/bb522682.aspx) toochange transaction logging scheme tooBULK_LOGGED toominimize overhead of logging, e.g.:</span></span>
  
        ALTER DATABASE <database_name> SET RECOVERY BULK_LOGGED
* <span data-ttu-id="df38d-127">données tooexpedite du chargement, lancer des opérations d’importation en bloc hello en parallèle.</span><span class="sxs-lookup"><span data-stu-id="df38d-127">tooexpedite data loading, launch hello bulk import operations in parallel.</span></span> <span data-ttu-id="df38d-128">Pour obtenir des conseils sur l’accélération de l’importation en bloc de volumes importants dans des bases de données SQL Server, consultez l’article [Charger 1 To en moins d’une heure](http://blogs.msdn.com/b/sqlcat/archive/2006/05/19/602142.aspx).</span><span class="sxs-lookup"><span data-stu-id="df38d-128">For tips on expediting bulk importing of big data into SQL Server databases, see [Load 1TB in less than 1 hour](http://blogs.msdn.com/b/sqlcat/archive/2006/05/19/602142.aspx).</span></span>

<span data-ttu-id="df38d-129">Hello script PowerShell suivant est un exemple parallèles de chargement de données à l’aide de BCP.</span><span class="sxs-lookup"><span data-stu-id="df38d-129">hello following PowerShell script is an example of parallel data loading using BCP.</span></span>

    # Set database name, input data directory, and output log directory
    # This example loads comma-separated input data files
    # hello example assumes hello partitioned data files are named as <base_file_name>_<partition_number>.csv
    # Assumes hello input data files include a header line. Loading starts at line number 2.

    $dbname = "<database_name>"
    $indir  = "<path_to_data_files>"
    $logdir = "<path_to_log_directory>"

    # Select authentication mode
    $sqlauth = 0

    # For SQL authentication, set hello server and user credentials
    $sqlusr = "<user@server>"
    $server = "<tcp:serverdns>"
    $pass   = "<password>"

    # Set number of partitions per table - Should match hello number of input data files per table
    $numofparts = <number_of_partitions>

    # Set table name toobe loaded, basename of input data files, input format file, and number of partitions
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


## <a name="create-indexes-toooptimize-joins-and-query-performance"></a><span data-ttu-id="df38d-130">Créer des index toooptimize jointures et des performances des requêtes</span><span class="sxs-lookup"><span data-stu-id="df38d-130">Create indexes toooptimize joins and query performance</span></span>
* <span data-ttu-id="df38d-131">Si vous extraira les données pour la modélisation de plusieurs tables, créer des index sur les clés de jointure hello performance de la jointure tooimprove hello.</span><span class="sxs-lookup"><span data-stu-id="df38d-131">If you will extract data for modeling from multiple tables, create indexes on hello join keys tooimprove hello join performance.</span></span>
* <span data-ttu-id="df38d-132">[Créer des index](https://technet.microsoft.com/library/ms188783.aspx) (en cluster ou non cluster) ciblant hello même groupe de fichiers pour chaque partition, pour, par exemple :</span><span class="sxs-lookup"><span data-stu-id="df38d-132">[Create indexes](https://technet.microsoft.com/library/ms188783.aspx) (clustered or non-clustered) targeting hello same filegroup for each partition, for e.g.:</span></span>
  
        CREATE CLUSTERED INDEX <table_idx> ON <table_name>( [include index columns here] )
        ON <TablePScheme>(<partition)field>)
  <span data-ttu-id="df38d-133">ou</span><span class="sxs-lookup"><span data-stu-id="df38d-133">or,</span></span>
  
        CREATE INDEX <table_idx> ON <table_name>( [include index columns here] )
        ON <TablePScheme>(<partition)field>)
  
  > [!NOTE]
  > <span data-ttu-id="df38d-134">Vous pouvez choisir toocreate index hello avant l’importation des données de salutation en bloc.</span><span class="sxs-lookup"><span data-stu-id="df38d-134">You may choose toocreate hello indexes before bulk importing hello data.</span></span> <span data-ttu-id="df38d-135">La création d’index avant l’importation en bloc ralentit le chargement des données hello.</span><span class="sxs-lookup"><span data-stu-id="df38d-135">Index creation before bulk importing will slow down hello data loading.</span></span>
  > 
  > 

## <a name="advanced-analytics-process-and-technology-in-action-example"></a><span data-ttu-id="df38d-136">Exemple de processus d’analyse avancé et technologie en action</span><span class="sxs-lookup"><span data-stu-id="df38d-136">Advanced Analytics Process and Technology in Action Example</span></span>
<span data-ttu-id="df38d-137">Pour obtenir un exemple de procédure pas à pas de bout en bout à l’aide de hello Cortana Analytique processus avec un jeu de données public, consultez [processus Analytique de Cortana en Action : à l’aide de SQL Server](machine-learning-data-science-process-sql-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="df38d-137">For an end-to-end walkthrough example using hello Cortana Analytics Process with a public dataset, see [Cortana Analytics Process in Action: using SQL Server](machine-learning-data-science-process-sql-walkthrough.md).</span></span>

