---
title: "aaaMove données tooSQL Server sur une machine virtuelle Azure | Documents Microsoft"
description: "Déplacer des données à partir de fichiers plats ou d’un tooSQL de SQL Server sur site Server sur machine virtuelle Azure."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 2c9ef1d3-4f5c-4b1f-bf06-223646c8af06
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: 63e02158f9c99f4478c4eb1cde62c877983dcf27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-toosql-server-on-an-azure-virtual-machine"></a>Déplacer les données tooSQL Server sur une machine virtuelle Azure
Cette rubrique décrit les options de hello pour le déplacement des données de fichiers plats (formats CSV ou TSV) ou d’un tooSQL de SQL Server sur site Server sur une machine virtuelle Azure. Ces tâches pour les données mobile dans le cloud toohello font partie de hello processus de science des données équipe.

Pour une rubrique qui décrit les options de hello de déplacement tooan de données base de données SQL Azure pour l’apprentissage, consultez [déplacer les données tooan base de données SQL Azure pour Azure Machine Learning](machine-learning-data-science-move-sql-azure.md).

Hello **menu** ci-dessous tootopics des liens qui décrivent comment les données tooingest dans d’autres environnements cibles où les données de salutation peuvent être stockées et traitées au cours de hello processus de science des données équipe (TDSP).

[!INCLUDE [cap-ingest-data-selector](../../includes/cap-ingest-data-selector.md)]

Hello tableau suivant résume les options hello pour tooSQL déplacement des données serveur sur une machine virtuelle Azure.

| <b>SOURCE</b> | <b>DESTINATION : SQL Server dans les machines virtuelles Azure</b> |
| --- | --- |
| <b>Fichier plat</b> |1. <a href="#insert-tables-bcp">Utilitaire de copie en bloc à ligne de commande (BCP)</a><br> 2. <a href="#insert-tables-bulkquery">Requête SQL Bulk Insert</a><br> 3. <a href="#sql-builtin-utilities">Utilitaires graphiques intégrés dans SQL Server</a> |
| <b>Serveur SQL Server local</b> |1. <a href="#deploy-a-sql-server-database-to-a-microsoft-azure-vm-wizard">Déployer un Assistant de machine virtuelle Microsoft Azure de base de données SQL Server tooa</a><br> 2. <a href="#export-flat-file">Exporter tooa fichier plat</a><br> 3. <a href="#sql-migration">Assistant Migration de la base de données SQL</a> <br> 4. <a href="#sql-backup">Sauvegarde et restauration de base de données</a><br> |

Notez que ce document suppose que les commandes SQL sont exécutées à partir de SQL Server Management Studio ou Visual Studio Database Explorer.

> [!TIP]
> En guise d’alternative, vous pouvez utiliser [Azure Data Factory](https://azure.microsoft.com/services/data-factory/) toocreate et planifier un pipeline qui déplace les données tooa machine virtuelle SQL Server sur Azure. Pour plus d’informations, consultez [Copie de données avec Azure Data Factory (activité de copie)](../data-factory/data-factory-data-movement-activities.md)
>
>

## <a name="prereqs"></a>Configuration requise
Ce didacticiel part du principe que vous disposez de :

* Un **abonnement Azure**. Si vous n’avez pas d’abonnement, vous pouvez vous inscrire à un [essai gratuit](https://azure.microsoft.com/pricing/free-trial/).
* Un **compte de stockage Azure**. Vous allez utiliser un compte de stockage Azure pour stocker les données de hello dans ce didacticiel. Si vous n’avez pas un compte de stockage Azure, consultez hello [créer un compte de stockage](../storage/common/storage-create-storage-account.md#create-a-storage-account) l’article. Une fois que vous avez créé le compte de stockage hello, vous devez compte de hello tooobtain clé utilisé le stockage de hello tooaccess. Voir [Gérer vos clés d’accès de stockage](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys).
* Approvisionnement d’un **serveur SQL Server sur une machine virtuelle Azure**. Pour obtenir des instructions, consultez [Configurer une machine virtuelle Azure SQL Server comme serveur IPython Notebook pour des analyses avancées](machine-learning-data-science-setup-sql-server-virtual-machine.md).
* **Azure PowerShell** installé et configuré localement. Pour obtenir des instructions, consultez [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview).

## <a name="filesource_to_sqlonazurevm"></a>Déplacement des données à partir d’un tooSQL de source de fichier plat Server sur une machine virtuelle Azure
Si vos données sont dans un fichier plat (classée dans un format de ligne/colonne), il peut être déplacé tooSQL ordinateur de serveur virtuel sur Azure via hello méthodes suivantes :

1. [Utilitaire de copie en bloc à ligne de commande (BCP)](#insert-tables-bcp)
2. [Requête SQL Bulk Insert ](#insert-tables-bulkquery)
3. [Utilitaires graphiques intégrés dans SQL Server (Importation/Exportation, SSIS)](#sql-builtin-utilities)

### <a name="insert-tables-bcp"></a>Utilitaire de copie en bloc à ligne de commande (BCP)
BCP est un utilitaire de ligne de commande installé avec SQL Server et est un des données toomove hello plus rapide. Il fonctionne sur les trois variantes de SQL Server (instance SQL Server locale, SQL Azure et machine virtuelle SQL Server sur Azure).

> [!NOTE]
> **Où mes données doivent-elles se trouver pour BCP ?**  
> Il n’est pas obligatoire, les fichiers contenant des données sources situées sur le même ordinateur en tant que cible de hello SQL Server permet de transfert plus rapide (réseau vitesse vs disque local vitesse d’e/s) de hello. Vous pouvez déplacer la machine de toohello de données contenant les fichiers hello plat où SQL Server est installé à l’aide de la copie des fichiers divers outils tels que [AZCopy](../storage/common/storage-use-azcopy.md), [Azure Storage Explorer](http://storageexplorer.com/) ou copier/coller de windows via à distance Protocole bureau (RDP).
>
>

1. Assurez-vous que les tables de hello et de la base de données hello sont créées sur la base de données SQL Server hello cible. Voici un exemple de procédure toodo que l’utilisation de hello `Create Database` et `Create Table` commandes :

        CREATE DATABASE <database_name>

        CREATE TABLE <tablename>
        (
            <columnname1> <datatype> <constraint>,
            <columnname2> <datatype> <constraint>,
            <columnname3> <datatype> <constraint>
        )
2. Générer hello fichier de format qui décrit le schéma hello pour la table de hello en émettant hello de commande suivante à partir de hello de ligne de commande de l’ordinateur de hello où bcp est installé.

    `bcp dbname..tablename format nul -c -x -f exportformatfilename.xml -S servername\sqlinstance -T -t \t -r \n`
3. Permet d’insérer des données de hello dans base de données hello utilisant hello bcp commande comme suit. En supposant que hello SQL Server est installé sur le même ordinateur, cela devrait fonctionner à partir de hello de ligne de commande :

    `bcp dbname..tablename in datafilename.tsv -f exportformatfilename.xml -S servername\sqlinstancename -U username -P password -b block_size_to_move_in_single_attemp -t \t -r \n`

> **Optimisation BCP insère** , consultez l’article suivant de hello [« Recommandations pour l’optimisation de l’importation en bloc »](https://technet.microsoft.com/library/ms177445%28v=sql.105%29.aspx) toooptimize telle insère.
>
>

### <a name="insert-tables-bulkquery-parallel"></a>Parallélisation des insertions pour accélérer le déplacement des données
Si vous déplacez les données de salutation sont volumineuse, vous pouvez accélérer choses en exécutant simultanément plusieurs commandes BCP en parallèle dans un PowerShell Script.

> [!NOTE]
> **Données volumineuses Ingestion** pour les datasets et très grandes, le chargement des données toooptimize partitionner vos tables de base de données logiques et physiques à l’aide de plusieurs tables de groupes de fichiers et de la partition. Pour plus d’informations sur la création et le chargement des données toopartition tables, consultez [parallèle Tables de Partition charge SQL](machine-learning-data-science-parallel-load-sql-partitioned-tables.md).
>
>

Hello exemple de script PowerShell ci-dessous montrent les insertions parallèles à l’aide de bcp :

    $NO_OF_PARALLEL_JOBS=2

     Set-ExecutionPolicy RemoteSigned #set execution policy for hello script tooexecute
     # Define what each job does
       $ScriptBlock = {
           param($partitionnumber)

           #Explictly using SQL username password
           bcp database..tablename in datafile_path.csv -F 2 -f format_file_path.xml -U username@servername -S tcp:servername -P password -b block_size_to_move_in_single_attempt -t "," -r \n -o path_to_outputfile.$partitionnumber.txt

            #Trusted connection w.o username password (if you are using windows auth and are signed in with that credentials)
            #bcp database..tablename in datafile_path.csv -o path_to_outputfile.$partitionnumber.txt -h "TABLOCK" -F 2 -f format_file_path.xml  -T -b block_size_to_move_in_single_attempt -t "," -r \n
      }


    # Background processing of all partitions
    for ($i=1; $i -le $NO_OF_PARALLEL_JOBS; $i++)
    {
      Write-Debug "Submit loading partition # $i"
      Start-Job $ScriptBlock -Arg $i      
    }


    # Wait for it all toocomplete
    While (Get-Job -State "Running")
    {
      Start-Sleep 10
      Get-Job
    }

    # Getting hello information back from hello jobs
    Get-Job | Receive-Job
    Set-ExecutionPolicy Restricted #reset hello execution policy


### <a name="insert-tables-bulkquery"></a>Requête SQL Bulk Insert
[En bloc insérer une requête de SQL](https://msdn.microsoft.com/library/ms188365) peuvent être utilisés tooimport des données dans base de données hello à partir des fichiers de ligne/colonne basée (types de hello pris en charge sont traitées dans le[préparer des données pour l’exportation en bloc ou d’importation (SQL Server)](https://msdn.microsoft.com/library/ms188609)) rubrique.

Voici quelques exemples de requêtes Bulk Insert :  

1. Analyser vos données et définir des options personnalisées avant d’importer toomake que cette base de données SQL Server hello suppose hello même mettre en forme des champs spéciaux tels que des dates. Voici un exemple de comment format de date de hello tooset en tant qu’année-mois-jour (si vos données contiennent date hello au format de l’année-mois-jour) :

        SET DATEFORMAT ymd;    
2. Importez des données avec des instructions import en bloc :

        BULK INSERT <tablename>
        FROM    
        '<datafilename>'
        WITH
        (
        FirstRow=2,
        FIELDTERMINATOR =',', --this should be column separator in your data
        ROWTERMINATOR ='\n'   --this should be hello row separator in your data
        )

### <a name="sql-builtin-utilities"></a>Utilitaires intégrés dans SQL Server
Vous pouvez utiliser les données de tooimport de SQL Server Integration Services (SSIS) dans la machine virtuelle SQL Server sur Azure à partir d’un fichier plat.
SSIS est disponible dans deux environnements Studio. Pour en savoir plus, consultez l’article [Services d’intégration (SSIS) et environnements Studio](https://technet.microsoft.com/library/ms140028.aspx):

* Pour en savoir plus sur les outils SQL Server Data Tools, consultez l’article [Microsoft SQL Server Data Tools](https://msdn.microsoft.com/data/tools.aspx)  
* Pour plus d’informations sur l’Assistant Importation/exportation de hello, consultez [SQL Server Assistant Importation et exportation](https://msdn.microsoft.com/library/ms141209.aspx)

## <a name="sqlonprem_to_sqlonazurevm"></a>Déplacement des données de tooSQL de SQL Server sur site Server sur une machine virtuelle Azure
Vous pouvez également utiliser hello suivant des stratégies de migration :

1. [Déployer un Assistant de machine virtuelle Microsoft Azure de base de données SQL Server tooa](#deploy-a-sql-server-database-to-a-microsoft-azure-vm-wizard)
2. [TooFlat d’exportation de fichier](#export-flat-file)
3. [Assistant Migration de la base de données SQL](#sql-migration)
4. [Sauvegarde et restauration de base de données](#sql-backup)

Chacune de ces étapes est décrite ci-après :

### <a name="deploy-a-sql-server-database-tooa-microsoft-azure-vm-wizard"></a>Déployer un Assistant de machine virtuelle Microsoft Azure de base de données SQL Server tooa
Hello **déployer un Assistant de machine virtuelle Microsoft Azure de base de données SQL Server tooa** est un moyen simple et recommandée toomove des données d’un ordinateur local SQL Server instance tooSQL Server sur une machine virtuelle Azure. Pour obtenir des instructions détaillées ainsi en savoir plus sur d’autres alternatives, consultez [migrer une base de données de tooSQL Server sur une machine virtuelle Azure](../virtual-machines/windows/sql/virtual-machines-windows-migrate-sql.md).

### <a name="export-flat-file"></a>TooFlat d’exportation de fichier
Différentes méthodes peuvent être utilisées toobulk exporter des données à partir d’un ordinateur local SQL Server comme décrit dans hello [importation et exportation de données (SQL Server)](https://msdn.microsoft.com/library/ms175937.aspx) rubrique. Ce document couvre hello programme de copie en bloc (BCP) comme exemple. Une fois que les données sont exportées dans un fichier plat, il peut être importé tooanother SQL server à l’aide de l’importation en bloc.

1. Exporter les données de hello de tooa de SQL Server locale fichier à l’aide d’utilitaire hello comme suit

    `bcp dbname..tablename out datafile.tsv -S    servername\sqlinstancename -T -t \t -t \n -c`
2. Créer des base de données hello et une table de hello sur la machine virtuelle SQL Server sur Azure à l’aide de hello `create database` et `create table` pour le schéma de la table hello exporté à l’étape 1.
3. Créer un fichier de format pour décrire le schéma de la table de données hello importé/exporté hello. Détails du fichier de format hello sont décrites dans [créer un fichier de Format (SQL Server)](https://msdn.microsoft.com/library/ms191516.aspx).

    Génération du fichier de format BCP à partir d’en cours d’exécution lorsque hello des ordinateur SQL Server

        bcp dbname..tablename format nul -c -x -f exportformatfilename.xml -S servername\sqlinstance -T -t \t -r \n

    Génération du fichier de formation en cas d’exécution de BCP à distance sur une instance SQL Server

        bcp dbname..tablename format nul -c -x -f  exportformatfilename.xml  -U username@servername.database.windows.net -S tcp:servername -P password  --t \t -r \n
4. Utiliser une des méthodes de hello décrites dans la section [déplacement de données à partir de la Source de fichier](#filesource_to_sqlonazurevm) toomove les données de hello dans les fichiers plats tooa SQL Server.

### <a name="sql-migration"></a>Assistant Migration de la base de données SQL
[Assistant de Migration de base de données SQL Server](http://sqlazuremw.codeplex.com/) fournit un toomove de manière conviviale des données entre deux instances de SQL server. Il permet de schéma de données hello utilisateur toomap hello entre les sources et les tables de destination, choisissez les types de colonnes et différentes autres fonctionnalités. Il utilise la copie en bloc (BCP) dans les coulisses de hello. Une capture d’écran de hello Bienvenue dans l’écran de hello Migration de base de données SQL Assistant est indiqué ci-dessous.  

![Assistant Migration de SQL Server][2]

### <a name="sql-backup"></a>Sauvegarde et restauration de base de données
SQL Server prend en charge :

1. [Base de données principale et de restauration](https://msdn.microsoft.com/library/ms187048.aspx) (les deux tooa local fichier ou du fichier bacpac exportation tooblob) et [Applications de la couche données](https://msdn.microsoft.com/library/ee210546.aspx) (à l’aide du fichier bacpac).
2. Capacité toodirectly créer des machines virtuelles SQL Server sur Azure avec une base de données copiée ou la base de données SQL Azure existante copie tooan. Pour plus d’informations, consultez [hello d’utilisation Assistant copie de base de données](https://msdn.microsoft.com/library/ms188664.aspx).

Une capture d’écran de sauvegarde de base de données hello/restaurer les options à partir de SQL Server Management Studio est indiqué ci-dessous.

![Outil d’importation SQL Server][1]

## <a name="resources"></a>Ressources
[Migrer une base de données de tooSQL Server sur une machine virtuelle Azure](../virtual-machines/windows/sql/virtual-machines-windows-migrate-sql.md)

[Vue d’ensemble de SQL Server sur les machines virtuelles Azure](../virtual-machines/windows/sql/virtual-machines-windows-sql-server-iaas-overview.md)

[1]: ./media/machine-learning-data-science-move-sql-server-virtual-machine/sqlserver_builtin_utilities.png
[2]: ./media/machine-learning-data-science-move-sql-server-virtual-machine/database_migration_wizard.png
