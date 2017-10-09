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
# <a name="parallel-bulk-data-import-using-sql-partition-tables"></a>Importer des données en parallèle et en bloc à l’aide de tables de partition SQL
Ce document décrit le mode de partition des tables pour l’importation d’accélérée parallèle en bloc de base de données SQL Server de données tooa toobuild. Pour base de données volumineuses chargement/transfert tooa SQL, l’importation de données toohello base de données SQL et les requêtes suivantes peut être améliorée à l’aide de *Partitioned Tables et vues*. 

## <a name="create-a-new-database-and-a-set-of-filegroups"></a>Créer une base de données et un ensemble de groupes de fichiers
* [Créez une base de données](https://technet.microsoft.com/library/ms176061.aspx) (si elle n’existe pas).
* Ajouter la base de données toohello de groupes de fichiers de base de données qui contiendra les fichiers physiques hello partitionnée. Cela peut être fait avec [CREATE DATABASE](https://technet.microsoft.com/library/ms176061.aspx) si de nouveaux ou [ALTER DATABASE](https://msdn.microsoft.com/library/bb522682.aspx) si la base de données hello existe déjà.
* Ajoutez un ou plusieurs fichiers de base de données tooeach de fichiers (si nécessaire).
  
  > [!NOTE]
  > Spécifiez le groupe de fichiers hello cible qui contient les données de cette partition et hello physique de la base de données fichier nom (s) où les données du groupe de fichiers hello seront stockées.
  > 
  > 

Hello exemple suivant crée une nouvelle base de données avec trois groupes de fichiers autres que hello principal et les groupes de journaux, qui contient un fichier physique dans chacun. fichiers de base de données de Hello sont créés dans le dossier de données SQL Server par défaut hello, tel que configuré dans l’instance de SQL Server hello. Pour plus d’informations sur les emplacements de fichier par défaut hello, consultez [emplacements des fichiers pour la valeur par défaut et nommé d’Instances de SQL Server](https://msdn.microsoft.com/library/ms143547.aspx).

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

## <a name="create-a-partitioned-table"></a>Créer une table partitionnée
Créer une ou plusieurs tables partitionnées selon le schéma de données toohello, groupes de fichiers de base de données mappé toohello créé à l’étape précédente de hello. Lorsque les données sont importées en bloc toohello partitionné une ou plusieurs tables, les enregistrements sont répartis entre les groupes de fichiers hello selon le schéma de partition tooa, comme décrit ci-dessous.

**toocreate une table de partition, vous devez :**

* [Créer une fonction de partition](https://msdn.microsoft.com/library/ms187802.aspx) qui définit la plage des valeurs/limites toobe hello inclus dans chaque table de partition individuelle, par exemple, les partitions toolimit par mois (certains\_datetime\_champ) dans l’année hello 2013 :
  
        CREATE PARTITION FUNCTION <DatetimeFieldPFN>(<datetime_field>)  
        AS RANGE RIGHT FOR VALUES (
            '20130201', '20130301', '20130401',
            '20130501', '20130601', '20130701', '20130801',
            '20130901', '20131001', '20131101', '20131201' )
* [Créer un schéma de partition](https://msdn.microsoft.com/library/ms179854.aspx) qui mappe chaque plage de partition dans hello partition fonction tooa groupe de fichiers physique, par exemple :
  
        CREATE PARTITION SCHEME <DatetimeFieldPScheme> AS  
        PARTITION <DatetimeFieldPFN> too(
        <filegroup_1>, <filegroup_2>, <filegroup_3>, <filegroup_4>,
        <filegroup_5>, <filegroup_6>, <filegroup_7>, <filegroup_8>,
        <filegroup_9>, <filegroup_10>, <filegroup_11>, <filegroup_12> )
  
  plages de hello tooverify en vigueur dans chaque conséquente toohello fonction/schéma de partition, exécutez hello suivant la requête :
  
        SELECT psch.name as PartitionScheme,
            prng.value AS ParitionValue,
            prng.boundary_id AS BoundaryID
        FROM sys.partition_functions AS pfun
        INNER JOIN sys.partition_schemes psch ON pfun.function_id = psch.function_id
        INNER JOIN sys.partition_range_values prng ON prng.function_id=pfun.function_id
        WHERE pfun.name = <DatetimeFieldPFN>
* [Créer une table partitionnée](https://msdn.microsoft.com/library/ms174979.aspx)(s) en fonction du schéma de données tooyour et indiquer le champ de schéma et de contrainte de partition hello utilisé toopartition table de hello, par exemple :
  
        CREATE TABLE <table_name> ( [include schema definition here] )
        ON <TablePScheme>(<partition_field>)

Pour plus d’informations, consultez l’article [Créer des tables partitionnées et des index](https://msdn.microsoft.com/library/ms188730.aspx).

## <a name="bulk-import-hello-data-for-each-individual-partition-table"></a>Importer en bloc hello des données pour chaque table de partition individuelle
* Vous pouvez utiliser BCP, BULK INSERT ou d’autres méthodes telles que l’ [Assistant Migration SQL Server](http://sqlazuremw.codeplex.com/). exemple Hello fourni utilise la méthode BCP hello.
* [Modifier la base de données hello](https://msdn.microsoft.com/library/bb522682.aspx) transaction toochange schéma tooBULK_LOGGED toominimize surcharge de la journalisation, par exemple, d’enregistrement :
  
        ALTER DATABASE <database_name> SET RECOVERY BULK_LOGGED
* données tooexpedite du chargement, lancer des opérations d’importation en bloc hello en parallèle. Pour obtenir des conseils sur l’accélération de l’importation en bloc de volumes importants dans des bases de données SQL Server, consultez l’article [Charger 1 To en moins d’une heure](http://blogs.msdn.com/b/sqlcat/archive/2006/05/19/602142.aspx).

Hello script PowerShell suivant est un exemple parallèles de chargement de données à l’aide de BCP.

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


## <a name="create-indexes-toooptimize-joins-and-query-performance"></a>Créer des index toooptimize jointures et des performances des requêtes
* Si vous extraira les données pour la modélisation de plusieurs tables, créer des index sur les clés de jointure hello performance de la jointure tooimprove hello.
* [Créer des index](https://technet.microsoft.com/library/ms188783.aspx) (en cluster ou non cluster) ciblant hello même groupe de fichiers pour chaque partition, pour, par exemple :
  
        CREATE CLUSTERED INDEX <table_idx> ON <table_name>( [include index columns here] )
        ON <TablePScheme>(<partition)field>)
  ou
  
        CREATE INDEX <table_idx> ON <table_name>( [include index columns here] )
        ON <TablePScheme>(<partition)field>)
  
  > [!NOTE]
  > Vous pouvez choisir toocreate index hello avant l’importation des données de salutation en bloc. La création d’index avant l’importation en bloc ralentit le chargement des données hello.
  > 
  > 

## <a name="advanced-analytics-process-and-technology-in-action-example"></a>Exemple de processus d’analyse avancé et technologie en action
Pour obtenir un exemple de procédure pas à pas de bout en bout à l’aide de hello Cortana Analytique processus avec un jeu de données public, consultez [processus Analytique de Cortana en Action : à l’aide de SQL Server](machine-learning-data-science-process-sql-walkthrough.md).

