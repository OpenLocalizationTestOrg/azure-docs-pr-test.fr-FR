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
# <a name="move-data-toosql-server-on-an-azure-virtual-machine"></a><span data-ttu-id="3d18e-103">Déplacer les données tooSQL Server sur une machine virtuelle Azure</span><span class="sxs-lookup"><span data-stu-id="3d18e-103">Move data tooSQL Server on an Azure virtual machine</span></span>
<span data-ttu-id="3d18e-104">Cette rubrique décrit les options de hello pour le déplacement des données de fichiers plats (formats CSV ou TSV) ou d’un tooSQL de SQL Server sur site Server sur une machine virtuelle Azure.</span><span class="sxs-lookup"><span data-stu-id="3d18e-104">This topic outlines hello options for moving data either from flat files (CSV or TSV formats) or from an on-premises SQL Server tooSQL Server on an Azure virtual machine.</span></span> <span data-ttu-id="3d18e-105">Ces tâches pour les données mobile dans le cloud toohello font partie de hello processus de science des données équipe.</span><span class="sxs-lookup"><span data-stu-id="3d18e-105">These tasks for moving data toohello cloud are part of hello Team Data Science Process.</span></span>

<span data-ttu-id="3d18e-106">Pour une rubrique qui décrit les options de hello de déplacement tooan de données base de données SQL Azure pour l’apprentissage, consultez [déplacer les données tooan base de données SQL Azure pour Azure Machine Learning](machine-learning-data-science-move-sql-azure.md).</span><span class="sxs-lookup"><span data-stu-id="3d18e-106">For a topic that outlines hello options for moving data tooan Azure SQL Database for Machine Learning, see [Move data tooan Azure SQL Database for Azure Machine Learning](machine-learning-data-science-move-sql-azure.md).</span></span>

<span data-ttu-id="3d18e-107">Hello **menu** ci-dessous tootopics des liens qui décrivent comment les données tooingest dans d’autres environnements cibles où les données de salutation peuvent être stockées et traitées au cours de hello processus de science des données équipe (TDSP).</span><span class="sxs-lookup"><span data-stu-id="3d18e-107">hello **menu** below links tootopics that describe how tooingest data into other target environments where hello data can be stored and processed during hello Team Data Science Process (TDSP).</span></span>

[!INCLUDE [cap-ingest-data-selector](../../includes/cap-ingest-data-selector.md)]

<span data-ttu-id="3d18e-108">Hello tableau suivant résume les options hello pour tooSQL déplacement des données serveur sur une machine virtuelle Azure.</span><span class="sxs-lookup"><span data-stu-id="3d18e-108">hello following table summarizes hello options for moving data tooSQL Server on an Azure virtual machine.</span></span>

| <span data-ttu-id="3d18e-109"><b>SOURCE</b></span><span class="sxs-lookup"><span data-stu-id="3d18e-109"><b>SOURCE</b></span></span> | <span data-ttu-id="3d18e-110"><b>DESTINATION : SQL Server dans les machines virtuelles Azure</b></span><span class="sxs-lookup"><span data-stu-id="3d18e-110"><b>DESTINATION: SQL Server on Azure VM</b></span></span> |
| --- | --- |
| <span data-ttu-id="3d18e-111"><b>Fichier plat</b></span><span class="sxs-lookup"><span data-stu-id="3d18e-111"><b>Flat File</b></span></span> |<span data-ttu-id="3d18e-112">1. <a href="#insert-tables-bcp">Utilitaire de copie en bloc à ligne de commande (BCP)</a></span><span class="sxs-lookup"><span data-stu-id="3d18e-112">1. <a href="#insert-tables-bcp">Command-line bulk copy utility (BCP) </a></span></span><br> <span data-ttu-id="3d18e-113">2. <a href="#insert-tables-bulkquery">Requête SQL Bulk Insert</a></span><span class="sxs-lookup"><span data-stu-id="3d18e-113">2. <a href="#insert-tables-bulkquery">Bulk Insert SQL Query </a></span></span><br> <span data-ttu-id="3d18e-114">3. <a href="#sql-builtin-utilities">Utilitaires graphiques intégrés dans SQL Server</a></span><span class="sxs-lookup"><span data-stu-id="3d18e-114">3. <a href="#sql-builtin-utilities">Graphical Built-in Utilities in SQL Server</a></span></span> |
| <span data-ttu-id="3d18e-115"><b>Serveur SQL Server local</b></span><span class="sxs-lookup"><span data-stu-id="3d18e-115"><b>On-Premises SQL Server</b></span></span> |<span data-ttu-id="3d18e-116">1. <a href="#deploy-a-sql-server-database-to-a-microsoft-azure-vm-wizard">Déployer un Assistant de machine virtuelle Microsoft Azure de base de données SQL Server tooa</a></span><span class="sxs-lookup"><span data-stu-id="3d18e-116">1. <a href="#deploy-a-sql-server-database-to-a-microsoft-azure-vm-wizard">Deploy a SQL Server Database tooa Microsoft Azure VM wizard</a></span></span><br> <span data-ttu-id="3d18e-117">2. <a href="#export-flat-file">Exporter tooa fichier plat</a></span><span class="sxs-lookup"><span data-stu-id="3d18e-117">2. <a href="#export-flat-file">Export tooa flat File </a></span></span><br> <span data-ttu-id="3d18e-118">3. <a href="#sql-migration">Assistant Migration de la base de données SQL</a></span><span class="sxs-lookup"><span data-stu-id="3d18e-118">3. <a href="#sql-migration">SQL Database Migration Wizard </a></span></span> <br> <span data-ttu-id="3d18e-119">4. <a href="#sql-backup">Sauvegarde et restauration de base de données</a></span><span class="sxs-lookup"><span data-stu-id="3d18e-119">4. <a href="#sql-backup">Database back up and restore </a></span></span><br> |

<span data-ttu-id="3d18e-120">Notez que ce document suppose que les commandes SQL sont exécutées à partir de SQL Server Management Studio ou Visual Studio Database Explorer.</span><span class="sxs-lookup"><span data-stu-id="3d18e-120">Note that this document assumes that SQL commands are executed from SQL Server Management Studio or Visual Studio Database Explorer.</span></span>

> [!TIP]
> <span data-ttu-id="3d18e-121">En guise d’alternative, vous pouvez utiliser [Azure Data Factory](https://azure.microsoft.com/services/data-factory/) toocreate et planifier un pipeline qui déplace les données tooa machine virtuelle SQL Server sur Azure.</span><span class="sxs-lookup"><span data-stu-id="3d18e-121">As an alternative, you can use [Azure Data Factory](https://azure.microsoft.com/services/data-factory/) toocreate and schedule a pipeline that will move data tooa SQL Server VM on Azure.</span></span> <span data-ttu-id="3d18e-122">Pour plus d’informations, consultez [Copie de données avec Azure Data Factory (activité de copie)](../data-factory/data-factory-data-movement-activities.md)</span><span class="sxs-lookup"><span data-stu-id="3d18e-122">For more information, see [Copy data with Azure Data Factory (Copy Activity)](../data-factory/data-factory-data-movement-activities.md).</span></span>
>
>

## <span data-ttu-id="3d18e-123"><a name="prereqs"></a>Configuration requise</span><span class="sxs-lookup"><span data-stu-id="3d18e-123"><a name="prereqs"></a>Prerequisites</span></span>
<span data-ttu-id="3d18e-124">Ce didacticiel part du principe que vous disposez de :</span><span class="sxs-lookup"><span data-stu-id="3d18e-124">This tutorial assumes you have:</span></span>

* <span data-ttu-id="3d18e-125">Un **abonnement Azure**.</span><span class="sxs-lookup"><span data-stu-id="3d18e-125">An **Azure subscription**.</span></span> <span data-ttu-id="3d18e-126">Si vous n’avez pas d’abonnement, vous pouvez vous inscrire à un [essai gratuit](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3d18e-126">If you do not have a subscription, you can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="3d18e-127">Un **compte de stockage Azure**.</span><span class="sxs-lookup"><span data-stu-id="3d18e-127">An **Azure storage account**.</span></span> <span data-ttu-id="3d18e-128">Vous allez utiliser un compte de stockage Azure pour stocker les données de hello dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="3d18e-128">You will use an Azure storage account for storing hello data in this tutorial.</span></span> <span data-ttu-id="3d18e-129">Si vous n’avez pas un compte de stockage Azure, consultez hello [créer un compte de stockage](../storage/common/storage-create-storage-account.md#create-a-storage-account) l’article.</span><span class="sxs-lookup"><span data-stu-id="3d18e-129">If you don't have an Azure storage account, see hello [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) article.</span></span> <span data-ttu-id="3d18e-130">Une fois que vous avez créé le compte de stockage hello, vous devez compte de hello tooobtain clé utilisé le stockage de hello tooaccess.</span><span class="sxs-lookup"><span data-stu-id="3d18e-130">After you have created hello storage account, you will need tooobtain hello account key used tooaccess hello storage.</span></span> <span data-ttu-id="3d18e-131">Voir [Gérer vos clés d’accès de stockage](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys).</span><span class="sxs-lookup"><span data-stu-id="3d18e-131">See [Manage your storage access keys](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys).</span></span>
* <span data-ttu-id="3d18e-132">Approvisionnement d’un **serveur SQL Server sur une machine virtuelle Azure**.</span><span class="sxs-lookup"><span data-stu-id="3d18e-132">Provisioned **SQL Server on an Azure VM**.</span></span> <span data-ttu-id="3d18e-133">Pour obtenir des instructions, consultez [Configurer une machine virtuelle Azure SQL Server comme serveur IPython Notebook pour des analyses avancées](machine-learning-data-science-setup-sql-server-virtual-machine.md).</span><span class="sxs-lookup"><span data-stu-id="3d18e-133">For instructions, see [Set up an Azure SQL Server virtual machine as an IPython Notebook server for advanced analytics](machine-learning-data-science-setup-sql-server-virtual-machine.md).</span></span>
* <span data-ttu-id="3d18e-134">**Azure PowerShell** installé et configuré localement.</span><span class="sxs-lookup"><span data-stu-id="3d18e-134">Installed and configured **Azure PowerShell** locally.</span></span> <span data-ttu-id="3d18e-135">Pour obtenir des instructions, consultez [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="3d18e-135">For instructions, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <span data-ttu-id="3d18e-136"><a name="filesource_to_sqlonazurevm"></a>Déplacement des données à partir d’un tooSQL de source de fichier plat Server sur une machine virtuelle Azure</span><span class="sxs-lookup"><span data-stu-id="3d18e-136"><a name="filesource_to_sqlonazurevm"></a> Moving data from a flat file source tooSQL Server on an Azure VM</span></span>
<span data-ttu-id="3d18e-137">Si vos données sont dans un fichier plat (classée dans un format de ligne/colonne), il peut être déplacé tooSQL ordinateur de serveur virtuel sur Azure via hello méthodes suivantes :</span><span class="sxs-lookup"><span data-stu-id="3d18e-137">If your data is in a flat file (arranged in a row/column format), it can be moved tooSQL Server VM on Azure via hello following methods:</span></span>

1. [<span data-ttu-id="3d18e-138">Utilitaire de copie en bloc à ligne de commande (BCP)</span><span class="sxs-lookup"><span data-stu-id="3d18e-138">Command-line bulk copy utility (BCP)</span></span>](#insert-tables-bcp)
2. [<span data-ttu-id="3d18e-139">Requête SQL Bulk Insert </span><span class="sxs-lookup"><span data-stu-id="3d18e-139">Bulk Insert SQL Query </span></span>](#insert-tables-bulkquery)
3. [<span data-ttu-id="3d18e-140">Utilitaires graphiques intégrés dans SQL Server (Importation/Exportation, SSIS)</span><span class="sxs-lookup"><span data-stu-id="3d18e-140">Graphical Built-in Utilities in SQL Server (Import/Export, SSIS)</span></span>](#sql-builtin-utilities)

### <span data-ttu-id="3d18e-141"><a name="insert-tables-bcp"></a>Utilitaire de copie en bloc à ligne de commande (BCP)</span><span class="sxs-lookup"><span data-stu-id="3d18e-141"><a name="insert-tables-bcp"></a>Command-line bulk copy utility (BCP)</span></span>
<span data-ttu-id="3d18e-142">BCP est un utilitaire de ligne de commande installé avec SQL Server et est un des données toomove hello plus rapide.</span><span class="sxs-lookup"><span data-stu-id="3d18e-142">BCP is a command-line utility installed with SQL Server and is one of hello quickest ways toomove data.</span></span> <span data-ttu-id="3d18e-143">Il fonctionne sur les trois variantes de SQL Server (instance SQL Server locale, SQL Azure et machine virtuelle SQL Server sur Azure).</span><span class="sxs-lookup"><span data-stu-id="3d18e-143">It works across all three SQL Server variants (On-premises SQL Server, SQL Azure and SQL Server VM on Azure).</span></span>

> [!NOTE]
> <span data-ttu-id="3d18e-144">**Où mes données doivent-elles se trouver pour BCP ?**</span><span class="sxs-lookup"><span data-stu-id="3d18e-144">**Where should my data be for BCP?**</span></span>  
> <span data-ttu-id="3d18e-145">Il n’est pas obligatoire, les fichiers contenant des données sources situées sur le même ordinateur en tant que cible de hello SQL Server permet de transfert plus rapide (réseau vitesse vs disque local vitesse d’e/s) de hello.</span><span class="sxs-lookup"><span data-stu-id="3d18e-145">While it is not required, having files containing source data located on hello same machine as hello target SQL Server allows for faster transfers (network speed vs local disk IO speed).</span></span> <span data-ttu-id="3d18e-146">Vous pouvez déplacer la machine de toohello de données contenant les fichiers hello plat où SQL Server est installé à l’aide de la copie des fichiers divers outils tels que [AZCopy](../storage/common/storage-use-azcopy.md), [Azure Storage Explorer](http://storageexplorer.com/) ou copier/coller de windows via à distance Protocole bureau (RDP).</span><span class="sxs-lookup"><span data-stu-id="3d18e-146">You can move hello flat files containing data toohello machine where SQL Server is installed using various file copying tools such as [AZCopy](../storage/common/storage-use-azcopy.md), [Azure Storage Explorer](http://storageexplorer.com/) or windows copy/paste via Remote Desktop Protocol (RDP).</span></span>
>
>

1. <span data-ttu-id="3d18e-147">Assurez-vous que les tables de hello et de la base de données hello sont créées sur la base de données SQL Server hello cible.</span><span class="sxs-lookup"><span data-stu-id="3d18e-147">Ensure that hello database and hello tables are created on hello target SQL Server database.</span></span> <span data-ttu-id="3d18e-148">Voici un exemple de procédure toodo que l’utilisation de hello `Create Database` et `Create Table` commandes :</span><span class="sxs-lookup"><span data-stu-id="3d18e-148">Here is an example of how toodo that using hello `Create Database` and `Create Table` commands:</span></span>

        CREATE DATABASE <database_name>

        CREATE TABLE <tablename>
        (
            <columnname1> <datatype> <constraint>,
            <columnname2> <datatype> <constraint>,
            <columnname3> <datatype> <constraint>
        )
2. <span data-ttu-id="3d18e-149">Générer hello fichier de format qui décrit le schéma hello pour la table de hello en émettant hello de commande suivante à partir de hello de ligne de commande de l’ordinateur de hello où bcp est installé.</span><span class="sxs-lookup"><span data-stu-id="3d18e-149">Generate hello format file that describes hello schema for hello table by issuing hello following command from hello command-line of hello machine where bcp is installed.</span></span>

    `bcp dbname..tablename format nul -c -x -f exportformatfilename.xml -S servername\sqlinstance -T -t \t -r \n`
3. <span data-ttu-id="3d18e-150">Permet d’insérer des données de hello dans base de données hello utilisant hello bcp commande comme suit.</span><span class="sxs-lookup"><span data-stu-id="3d18e-150">Insert hello data into hello database using hello bcp command as follows.</span></span> <span data-ttu-id="3d18e-151">En supposant que hello SQL Server est installé sur le même ordinateur, cela devrait fonctionner à partir de hello de ligne de commande :</span><span class="sxs-lookup"><span data-stu-id="3d18e-151">This should work from hello command-line assuming that hello SQL Server is installed on same machine:</span></span>

    `bcp dbname..tablename in datafilename.tsv -f exportformatfilename.xml -S servername\sqlinstancename -U username -P password -b block_size_to_move_in_single_attemp -t \t -r \n`

> <span data-ttu-id="3d18e-152">**Optimisation BCP insère** , consultez l’article suivant de hello [« Recommandations pour l’optimisation de l’importation en bloc »](https://technet.microsoft.com/library/ms177445%28v=sql.105%29.aspx) toooptimize telle insère.</span><span class="sxs-lookup"><span data-stu-id="3d18e-152">**Optimizing BCP Inserts** Please refer hello following article ['Guidelines for Optimizing Bulk Import'](https://technet.microsoft.com/library/ms177445%28v=sql.105%29.aspx) toooptimize such inserts.</span></span>
>
>

### <span data-ttu-id="3d18e-153"><a name="insert-tables-bulkquery-parallel"></a>Parallélisation des insertions pour accélérer le déplacement des données</span><span class="sxs-lookup"><span data-stu-id="3d18e-153"><a name="insert-tables-bulkquery-parallel"></a>Parallelizing Inserts for Faster Data Movement</span></span>
<span data-ttu-id="3d18e-154">Si vous déplacez les données de salutation sont volumineuse, vous pouvez accélérer choses en exécutant simultanément plusieurs commandes BCP en parallèle dans un PowerShell Script.</span><span class="sxs-lookup"><span data-stu-id="3d18e-154">If hello data you are moving is large, you can speed things up by simultaneously executing multiple BCP commands in parallel in a PowerShell Script.</span></span>

> [!NOTE]
> <span data-ttu-id="3d18e-155">**Données volumineuses Ingestion** pour les datasets et très grandes, le chargement des données toooptimize partitionner vos tables de base de données logiques et physiques à l’aide de plusieurs tables de groupes de fichiers et de la partition.</span><span class="sxs-lookup"><span data-stu-id="3d18e-155">**Big data Ingestion** toooptimize data loading for large and very large datasets, partition your logical and physical database tables using multiple filegroups and partition tables.</span></span> <span data-ttu-id="3d18e-156">Pour plus d’informations sur la création et le chargement des données toopartition tables, consultez [parallèle Tables de Partition charge SQL](machine-learning-data-science-parallel-load-sql-partitioned-tables.md).</span><span class="sxs-lookup"><span data-stu-id="3d18e-156">For more information about creating and loading data toopartition tables, see [Parallel Load SQL Partition Tables](machine-learning-data-science-parallel-load-sql-partitioned-tables.md).</span></span>
>
>

<span data-ttu-id="3d18e-157">Hello exemple de script PowerShell ci-dessous montrent les insertions parallèles à l’aide de bcp :</span><span class="sxs-lookup"><span data-stu-id="3d18e-157">hello sample PowerShell script below demonstrate parallel inserts using bcp:</span></span>

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


### <span data-ttu-id="3d18e-158"><a name="insert-tables-bulkquery"></a>Requête SQL Bulk Insert</span><span class="sxs-lookup"><span data-stu-id="3d18e-158"><a name="insert-tables-bulkquery"></a>Bulk Insert SQL Query</span></span>
<span data-ttu-id="3d18e-159">[En bloc insérer une requête de SQL](https://msdn.microsoft.com/library/ms188365) peuvent être utilisés tooimport des données dans base de données hello à partir des fichiers de ligne/colonne basée (types de hello pris en charge sont traitées dans le[préparer des données pour l’exportation en bloc ou d’importation (SQL Server)](https://msdn.microsoft.com/library/ms188609)) rubrique.</span><span class="sxs-lookup"><span data-stu-id="3d18e-159">[Bulk Insert SQL Query](https://msdn.microsoft.com/library/ms188365) can be used tooimport data into hello database from row/column based files (hello supported types are covered in the[Prepare Data for Bulk Export or Import (SQL Server)](https://msdn.microsoft.com/library/ms188609)) topic.</span></span>

<span data-ttu-id="3d18e-160">Voici quelques exemples de requêtes Bulk Insert :</span><span class="sxs-lookup"><span data-stu-id="3d18e-160">Here are some sample commands for Bulk Insert are as below:</span></span>  

1. <span data-ttu-id="3d18e-161">Analyser vos données et définir des options personnalisées avant d’importer toomake que cette base de données SQL Server hello suppose hello même mettre en forme des champs spéciaux tels que des dates.</span><span class="sxs-lookup"><span data-stu-id="3d18e-161">Analyze your data and set any custom options before importing toomake sure that hello SQL Server database assumes hello same format for any special fields such as dates.</span></span> <span data-ttu-id="3d18e-162">Voici un exemple de comment format de date de hello tooset en tant qu’année-mois-jour (si vos données contiennent date hello au format de l’année-mois-jour) :</span><span class="sxs-lookup"><span data-stu-id="3d18e-162">Here is an example of how tooset hello date format as year-month-day (if your data contains hello date in year-month-day format):</span></span>

        SET DATEFORMAT ymd;    
2. <span data-ttu-id="3d18e-163">Importez des données avec des instructions import en bloc :</span><span class="sxs-lookup"><span data-stu-id="3d18e-163">Import data using bulk import statements:</span></span>

        BULK INSERT <tablename>
        FROM    
        '<datafilename>'
        WITH
        (
        FirstRow=2,
        FIELDTERMINATOR =',', --this should be column separator in your data
        ROWTERMINATOR ='\n'   --this should be hello row separator in your data
        )

### <span data-ttu-id="3d18e-164"><a name="sql-builtin-utilities"></a>Utilitaires intégrés dans SQL Server</span><span class="sxs-lookup"><span data-stu-id="3d18e-164"><a name="sql-builtin-utilities"></a>Built-in Utilities in SQL Server</span></span>
<span data-ttu-id="3d18e-165">Vous pouvez utiliser les données de tooimport de SQL Server Integration Services (SSIS) dans la machine virtuelle SQL Server sur Azure à partir d’un fichier plat.</span><span class="sxs-lookup"><span data-stu-id="3d18e-165">You can use SQL Server Integrations Services (SSIS) tooimport data into SQL Server VM on Azure from a flat file.</span></span>
<span data-ttu-id="3d18e-166">SSIS est disponible dans deux environnements Studio.</span><span class="sxs-lookup"><span data-stu-id="3d18e-166">SSIS is available in two studio environments.</span></span> <span data-ttu-id="3d18e-167">Pour en savoir plus, consultez l’article [Services d’intégration (SSIS) et environnements Studio](https://technet.microsoft.com/library/ms140028.aspx):</span><span class="sxs-lookup"><span data-stu-id="3d18e-167">For details, see [Integration Services (SSIS) and Studio Environments](https://technet.microsoft.com/library/ms140028.aspx):</span></span>

* <span data-ttu-id="3d18e-168">Pour en savoir plus sur les outils SQL Server Data Tools, consultez l’article [Microsoft SQL Server Data Tools](https://msdn.microsoft.com/data/tools.aspx)</span><span class="sxs-lookup"><span data-stu-id="3d18e-168">For details on SQL Server Data Tools, see [Microsoft SQL Server Data Tools](https://msdn.microsoft.com/data/tools.aspx)</span></span>  
* <span data-ttu-id="3d18e-169">Pour plus d’informations sur l’Assistant Importation/exportation de hello, consultez [SQL Server Assistant Importation et exportation](https://msdn.microsoft.com/library/ms141209.aspx)</span><span class="sxs-lookup"><span data-stu-id="3d18e-169">For details on hello Import/Export Wizard, see [SQL Server Import and Export Wizard](https://msdn.microsoft.com/library/ms141209.aspx)</span></span>

## <span data-ttu-id="3d18e-170"><a name="sqlonprem_to_sqlonazurevm"></a>Déplacement des données de tooSQL de SQL Server sur site Server sur une machine virtuelle Azure</span><span class="sxs-lookup"><span data-stu-id="3d18e-170"><a name="sqlonprem_to_sqlonazurevm"></a>Moving Data from on-premises SQL Server tooSQL Server on an Azure VM</span></span>
<span data-ttu-id="3d18e-171">Vous pouvez également utiliser hello suivant des stratégies de migration :</span><span class="sxs-lookup"><span data-stu-id="3d18e-171">You can also use hello following migration strategies:</span></span>

1. [<span data-ttu-id="3d18e-172">Déployer un Assistant de machine virtuelle Microsoft Azure de base de données SQL Server tooa</span><span class="sxs-lookup"><span data-stu-id="3d18e-172">Deploy a SQL Server Database tooa Microsoft Azure VM wizard</span></span>](#deploy-a-sql-server-database-to-a-microsoft-azure-vm-wizard)
2. [<span data-ttu-id="3d18e-173">TooFlat d’exportation de fichier</span><span class="sxs-lookup"><span data-stu-id="3d18e-173">Export tooFlat File</span></span>](#export-flat-file)
3. [<span data-ttu-id="3d18e-174">Assistant Migration de la base de données SQL</span><span class="sxs-lookup"><span data-stu-id="3d18e-174">SQL Database Migration Wizard</span></span>](#sql-migration)
4. [<span data-ttu-id="3d18e-175">Sauvegarde et restauration de base de données</span><span class="sxs-lookup"><span data-stu-id="3d18e-175">Database back up and restore</span></span>](#sql-backup)

<span data-ttu-id="3d18e-176">Chacune de ces étapes est décrite ci-après :</span><span class="sxs-lookup"><span data-stu-id="3d18e-176">We describe each of these below:</span></span>

### <a name="deploy-a-sql-server-database-tooa-microsoft-azure-vm-wizard"></a><span data-ttu-id="3d18e-177">Déployer un Assistant de machine virtuelle Microsoft Azure de base de données SQL Server tooa</span><span class="sxs-lookup"><span data-stu-id="3d18e-177">Deploy a SQL Server Database tooa Microsoft Azure VM wizard</span></span>
<span data-ttu-id="3d18e-178">Hello **déployer un Assistant de machine virtuelle Microsoft Azure de base de données SQL Server tooa** est un moyen simple et recommandée toomove des données d’un ordinateur local SQL Server instance tooSQL Server sur une machine virtuelle Azure.</span><span class="sxs-lookup"><span data-stu-id="3d18e-178">hello **Deploy a SQL Server Database tooa Microsoft Azure VM wizard** is a simple and recommended way toomove data from an on-premises SQL Server instance tooSQL Server on an Azure VM.</span></span> <span data-ttu-id="3d18e-179">Pour obtenir des instructions détaillées ainsi en savoir plus sur d’autres alternatives, consultez [migrer une base de données de tooSQL Server sur une machine virtuelle Azure](../virtual-machines/windows/sql/virtual-machines-windows-migrate-sql.md).</span><span class="sxs-lookup"><span data-stu-id="3d18e-179">For detailed steps as well as a discussion of other alternatives, see [Migrate a database tooSQL Server on an Azure VM](../virtual-machines/windows/sql/virtual-machines-windows-migrate-sql.md).</span></span>

### <span data-ttu-id="3d18e-180"><a name="export-flat-file"></a>TooFlat d’exportation de fichier</span><span class="sxs-lookup"><span data-stu-id="3d18e-180"><a name="export-flat-file"></a>Export tooFlat File</span></span>
<span data-ttu-id="3d18e-181">Différentes méthodes peuvent être utilisées toobulk exporter des données à partir d’un ordinateur local SQL Server comme décrit dans hello [importation et exportation de données (SQL Server)](https://msdn.microsoft.com/library/ms175937.aspx) rubrique.</span><span class="sxs-lookup"><span data-stu-id="3d18e-181">Various methods can be used toobulk export data from an On-Premises SQL Server as documented in hello [Bulk Import and Export of Data (SQL Server)](https://msdn.microsoft.com/library/ms175937.aspx) topic.</span></span> <span data-ttu-id="3d18e-182">Ce document couvre hello programme de copie en bloc (BCP) comme exemple.</span><span class="sxs-lookup"><span data-stu-id="3d18e-182">This document will cover hello Bulk Copy Program (BCP) as an example.</span></span> <span data-ttu-id="3d18e-183">Une fois que les données sont exportées dans un fichier plat, il peut être importé tooanother SQL server à l’aide de l’importation en bloc.</span><span class="sxs-lookup"><span data-stu-id="3d18e-183">Once data is exported into a flat file, it can be imported tooanother SQL server using bulk import.</span></span>

1. <span data-ttu-id="3d18e-184">Exporter les données de hello de tooa de SQL Server locale fichier à l’aide d’utilitaire hello comme suit</span><span class="sxs-lookup"><span data-stu-id="3d18e-184">Export hello data from on-premises SQL Server tooa File using hello bcp utility as follows</span></span>

    `bcp dbname..tablename out datafile.tsv -S    servername\sqlinstancename -T -t \t -t \n -c`
2. <span data-ttu-id="3d18e-185">Créer des base de données hello et une table de hello sur la machine virtuelle SQL Server sur Azure à l’aide de hello `create database` et `create table` pour le schéma de la table hello exporté à l’étape 1.</span><span class="sxs-lookup"><span data-stu-id="3d18e-185">Create hello database and hello table on SQL Server VM on Azure using hello `create database` and `create table` for hello table schema exported in step 1.</span></span>
3. <span data-ttu-id="3d18e-186">Créer un fichier de format pour décrire le schéma de la table de données hello importé/exporté hello.</span><span class="sxs-lookup"><span data-stu-id="3d18e-186">Create a format file for describing hello table schema of hello data being exported/imported.</span></span> <span data-ttu-id="3d18e-187">Détails du fichier de format hello sont décrites dans [créer un fichier de Format (SQL Server)](https://msdn.microsoft.com/library/ms191516.aspx).</span><span class="sxs-lookup"><span data-stu-id="3d18e-187">Details of hello format file are described in [Create a Format File (SQL Server)](https://msdn.microsoft.com/library/ms191516.aspx).</span></span>

    <span data-ttu-id="3d18e-188">Génération du fichier de format BCP à partir d’en cours d’exécution lorsque hello des ordinateur SQL Server</span><span class="sxs-lookup"><span data-stu-id="3d18e-188">Format file generation when running BCP from hello SQL Server machine</span></span>

        bcp dbname..tablename format nul -c -x -f exportformatfilename.xml -S servername\sqlinstance -T -t \t -r \n

    <span data-ttu-id="3d18e-189">Génération du fichier de formation en cas d’exécution de BCP à distance sur une instance SQL Server</span><span class="sxs-lookup"><span data-stu-id="3d18e-189">Format file generation when running BCP remotely against a SQL Server</span></span>

        bcp dbname..tablename format nul -c -x -f  exportformatfilename.xml  -U username@servername.database.windows.net -S tcp:servername -P password  --t \t -r \n
4. <span data-ttu-id="3d18e-190">Utiliser une des méthodes de hello décrites dans la section [déplacement de données à partir de la Source de fichier](#filesource_to_sqlonazurevm) toomove les données de hello dans les fichiers plats tooa SQL Server.</span><span class="sxs-lookup"><span data-stu-id="3d18e-190">Use any of hello methods described in section [Moving Data from File Source](#filesource_to_sqlonazurevm) toomove hello data in flat files tooa SQL Server.</span></span>

### <span data-ttu-id="3d18e-191"><a name="sql-migration"></a>Assistant Migration de la base de données SQL</span><span class="sxs-lookup"><span data-stu-id="3d18e-191"><a name="sql-migration"></a>SQL Database Migration Wizard</span></span>
<span data-ttu-id="3d18e-192">[Assistant de Migration de base de données SQL Server](http://sqlazuremw.codeplex.com/) fournit un toomove de manière conviviale des données entre deux instances de SQL server.</span><span class="sxs-lookup"><span data-stu-id="3d18e-192">[SQL Server Database Migration Wizard](http://sqlazuremw.codeplex.com/) provides a user-friendly way toomove data between two SQL server instances.</span></span> <span data-ttu-id="3d18e-193">Il permet de schéma de données hello utilisateur toomap hello entre les sources et les tables de destination, choisissez les types de colonnes et différentes autres fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="3d18e-193">It allows hello user toomap hello data schema between sources and destination tables, choose column types and various other functionalities.</span></span> <span data-ttu-id="3d18e-194">Il utilise la copie en bloc (BCP) dans les coulisses de hello.</span><span class="sxs-lookup"><span data-stu-id="3d18e-194">It uses bulk copy (BCP) under hello covers.</span></span> <span data-ttu-id="3d18e-195">Une capture d’écran de hello Bienvenue dans l’écran de hello Migration de base de données SQL Assistant est indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="3d18e-195">A screenshot of hello welcome screen for hello SQL Database Migration wizard is shown below.</span></span>  

![Assistant Migration de SQL Server][2]

### <span data-ttu-id="3d18e-197"><a name="sql-backup"></a>Sauvegarde et restauration de base de données</span><span class="sxs-lookup"><span data-stu-id="3d18e-197"><a name="sql-backup"></a>Database back up and restore</span></span>
<span data-ttu-id="3d18e-198">SQL Server prend en charge :</span><span class="sxs-lookup"><span data-stu-id="3d18e-198">SQL Server supports:</span></span>

1. <span data-ttu-id="3d18e-199">[Base de données principale et de restauration](https://msdn.microsoft.com/library/ms187048.aspx) (les deux tooa local fichier ou du fichier bacpac exportation tooblob) et [Applications de la couche données](https://msdn.microsoft.com/library/ee210546.aspx) (à l’aide du fichier bacpac).</span><span class="sxs-lookup"><span data-stu-id="3d18e-199">[Database back up and restore functionality](https://msdn.microsoft.com/library/ms187048.aspx) (both tooa local file or bacpac export tooblob) and [Data Tier Applications](https://msdn.microsoft.com/library/ee210546.aspx) (using bacpac).</span></span>
2. <span data-ttu-id="3d18e-200">Capacité toodirectly créer des machines virtuelles SQL Server sur Azure avec une base de données copiée ou la base de données SQL Azure existante copie tooan.</span><span class="sxs-lookup"><span data-stu-id="3d18e-200">Ability toodirectly create SQL Server VMs on Azure with a copied database or copy tooan existing SQL Azure database.</span></span> <span data-ttu-id="3d18e-201">Pour plus d’informations, consultez [hello d’utilisation Assistant copie de base de données](https://msdn.microsoft.com/library/ms188664.aspx).</span><span class="sxs-lookup"><span data-stu-id="3d18e-201">For more details, see [Use hello Copy Database Wizard](https://msdn.microsoft.com/library/ms188664.aspx).</span></span>

<span data-ttu-id="3d18e-202">Une capture d’écran de sauvegarde de base de données hello/restaurer les options à partir de SQL Server Management Studio est indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="3d18e-202">A screenshot of hello Database back up/restore options from SQL Server Management Studio is shown below.</span></span>

![Outil d’importation SQL Server][1]

## <a name="resources"></a><span data-ttu-id="3d18e-204">Ressources</span><span class="sxs-lookup"><span data-stu-id="3d18e-204">Resources</span></span>
[<span data-ttu-id="3d18e-205">Migrer une base de données de tooSQL Server sur une machine virtuelle Azure</span><span class="sxs-lookup"><span data-stu-id="3d18e-205">Migrate a Database tooSQL Server on an Azure VM</span></span>](../virtual-machines/windows/sql/virtual-machines-windows-migrate-sql.md)

[<span data-ttu-id="3d18e-206">Vue d’ensemble de SQL Server sur les machines virtuelles Azure</span><span class="sxs-lookup"><span data-stu-id="3d18e-206">SQL Server on Azure Virtual Machines overview</span></span>](../virtual-machines/windows/sql/virtual-machines-windows-sql-server-iaas-overview.md)

[1]: ./media/machine-learning-data-science-move-sql-server-virtual-machine/sqlserver_builtin_utilities.png
[2]: ./media/machine-learning-data-science-move-sql-server-virtual-machine/database_migration_wizard.png
