---
title: "données aaaCopy entre Data Lake Store et de la base de données SQL Azure à l’aide de Sqoop | Documents Microsoft"
description: "Utiliser des données de toocopy Sqoop entre la base de données SQL Azure et Data Lake Store"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 3f914b2a-83cc-4950-b3f7-69c921851683
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: f58483455f0ebe9544673a1d5c5884f2721c800c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-between-data-lake-store-and-azure-sql-database-using-sqoop"></a><span data-ttu-id="75dd1-103">Copier des données entre Data Lake Store et une base de données SQL Azure à l’aide de Sqoop</span><span class="sxs-lookup"><span data-stu-id="75dd1-103">Copy data between Data Lake Store and Azure SQL database using Sqoop</span></span>
<span data-ttu-id="75dd1-104">Découvrez comment Apache Sqoop toouse tooimport et exporter des données entre la base de données SQL Azure et Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="75dd1-104">Learn how toouse Apache Sqoop tooimport and export data between Azure SQL Database and Data Lake Store.</span></span>

## <a name="what-is-sqoop"></a><span data-ttu-id="75dd1-105">Qu'est-ce que Sqoop ?</span><span class="sxs-lookup"><span data-stu-id="75dd1-105">What is Sqoop?</span></span>
<span data-ttu-id="75dd1-106">Les applications Big Data sont un choix naturel pour le traitement des données non structurées et semi-structurées, telles que les journaux et les fichiers.</span><span class="sxs-lookup"><span data-stu-id="75dd1-106">Big data applications are a natural choice for processing unstructured and semi-structured data, such as logs and files.</span></span> <span data-ttu-id="75dd1-107">Toutefois, il peut également être un besoin de données tooprocess structurées stockées dans les bases de données relationnelles.</span><span class="sxs-lookup"><span data-stu-id="75dd1-107">However, there may also be a need tooprocess structured data that is stored in relational databases.</span></span>

<span data-ttu-id="75dd1-108">[Apache Sqoop](https://sqoop.apache.org/docs/1.4.4/SqoopUserGuide.html) est un outil conçu de tootransfer des données entre les bases de données relationnelles et un référentiel de données volumineuses, tels que Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="75dd1-108">[Apache Sqoop](https://sqoop.apache.org/docs/1.4.4/SqoopUserGuide.html) is a tool designed tootransfer data between  relational databases and a big data repository, such as Data Lake Store.</span></span> <span data-ttu-id="75dd1-109">Vous pouvez l’utiliser tooimport des données à partir d’un système de gestion de base de données relationnelle (SGBDR) comme base de données SQL Azure dans Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="75dd1-109">You can use it tooimport data from a relational database management system (RDBMS) such as Azure SQL Database into Data Lake Store.</span></span> <span data-ttu-id="75dd1-110">Vous pouvez transformer et analyser les données hello à l’aide de charges de travail de données volumineuses et puis exporter les données de salutation dans un SGBDR.</span><span class="sxs-lookup"><span data-stu-id="75dd1-110">You can then transform and analyze hello data using big data workloads and then export hello data back into an RDBMS.</span></span> <span data-ttu-id="75dd1-111">Dans ce didacticiel, vous utilisez une base de données SQL Azure en tant que votre base de données relationnelle tooimport/exportation à partir de.</span><span class="sxs-lookup"><span data-stu-id="75dd1-111">In this tutorial, you use an Azure SQL Database as your relational database tooimport/export from.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="75dd1-112">Composants requis</span><span class="sxs-lookup"><span data-stu-id="75dd1-112">Prerequisites</span></span>
<span data-ttu-id="75dd1-113">Avant de commencer cet article, vous devez disposer de hello :</span><span class="sxs-lookup"><span data-stu-id="75dd1-113">Before you begin this article, you must have hello following:</span></span>

* <span data-ttu-id="75dd1-114">**Un abonnement Azure**.</span><span class="sxs-lookup"><span data-stu-id="75dd1-114">**An Azure subscription**.</span></span> <span data-ttu-id="75dd1-115">Consultez la page [Obtention d’un essai gratuit d’Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="75dd1-115">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="75dd1-116">**Un compte Azure Data Lake Store**.</span><span class="sxs-lookup"><span data-stu-id="75dd1-116">**An Azure Data Lake Store account**.</span></span> <span data-ttu-id="75dd1-117">Pour obtenir des instructions sur la façon de voir d’un seul, toocreate [prise en main Azure Data Lake Store](data-lake-store-get-started-portal.md)</span><span class="sxs-lookup"><span data-stu-id="75dd1-117">For instructions on how toocreate one, see [Get started with Azure Data Lake Store](data-lake-store-get-started-portal.md)</span></span>
* <span data-ttu-id="75dd1-118">**Cluster HDInsight Azure** avec accès tooa compte Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="75dd1-118">**Azure HDInsight cluster** with access tooa Data Lake Store account.</span></span> <span data-ttu-id="75dd1-119">Voir [Créer un cluster HDInsight avec Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="75dd1-119">See [Create an HDInsight cluster with Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md).</span></span> <span data-ttu-id="75dd1-120">Cet article suppose que vous disposez d’un cluster Linux HDInsight avec accès à Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="75dd1-120">This article assumes you have an HDInsight Linux cluster with Data Lake Store access.</span></span>
* <span data-ttu-id="75dd1-121">**Base de données SQL Azure**.</span><span class="sxs-lookup"><span data-stu-id="75dd1-121">**Azure SQL Database**.</span></span> <span data-ttu-id="75dd1-122">Pour obtenir des instructions sur la façon de voir d’un seul, toocreate [créer une base de données SQL Azure](../sql-database/sql-database-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="75dd1-122">For instructions on how toocreate one, see [Create an Azure SQL database](../sql-database/sql-database-get-started.md)</span></span>

## <a name="do-you-learn-fast-with-videos"></a><span data-ttu-id="75dd1-123">Les vidéos vous permettent-elles d’apprendre rapidement ?</span><span class="sxs-lookup"><span data-stu-id="75dd1-123">Do you learn fast with videos?</span></span>
<span data-ttu-id="75dd1-124">[Regardez cette vidéo](https://mix.office.com/watch/1butcdjxmu114) sur la façon de toocopy des données entre les objets BLOB de stockage Azure et à l’aide de DistCp Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="75dd1-124">[Watch this video](https://mix.office.com/watch/1butcdjxmu114) on how toocopy data between Azure Storage Blobs and Data Lake Store using DistCp.</span></span>

## <a name="create-sample-tables-in-hello-azure-sql-database"></a><span data-ttu-id="75dd1-125">Créer des exemples de tables Bonjour base de données SQL Azure</span><span class="sxs-lookup"><span data-stu-id="75dd1-125">Create sample tables in hello Azure SQL Database</span></span>
1. <span data-ttu-id="75dd1-126">toostart, créez deux exemples de tables dans hello de base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="75dd1-126">toostart with, create two sample tables in hello Azure SQL Database.</span></span> <span data-ttu-id="75dd1-127">Utilisez [SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md) ou Visual Studio tooconnect toohello base de données SQL Azure et puis hello d’exécution des requêtes suivantes.</span><span class="sxs-lookup"><span data-stu-id="75dd1-127">Use [SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md) or Visual Studio tooconnect toohello Azure SQL Database and then run hello following queries.</span></span>

    <span data-ttu-id="75dd1-128">**Créer Table1**</span><span class="sxs-lookup"><span data-stu-id="75dd1-128">**Create Table1**</span></span>

        CREATE TABLE [dbo].[Table1](
        [ID] [int] NOT NULL,
        [FName] [nvarchar](50) NOT NULL,
        [LName] [nvarchar](50) NOT NULL,
         CONSTRAINT [PK_Table_4] PRIMARY KEY CLUSTERED
            (
                   [ID] ASC
            )
        ) ON [PRIMARY]
        GO

    <span data-ttu-id="75dd1-129">**Créer Table2**</span><span class="sxs-lookup"><span data-stu-id="75dd1-129">**Create Table2**</span></span>

        CREATE TABLE [dbo].[Table2](
        [ID] [int] NOT NULL,
        [FName] [nvarchar](50) NOT NULL,
        [LName] [nvarchar](50) NOT NULL,
         CONSTRAINT [PK_Table_4] PRIMARY KEY CLUSTERED
            (
                   [ID] ASC
            )
        ) ON [PRIMARY]
        GO
2. <span data-ttu-id="75dd1-130">Dans **Table1**, ajoutez des exemples de données.</span><span class="sxs-lookup"><span data-stu-id="75dd1-130">In **Table1**, add some sample data.</span></span> <span data-ttu-id="75dd1-131">Laissez **Table2** vide.</span><span class="sxs-lookup"><span data-stu-id="75dd1-131">Leave **Table2** empty.</span></span> <span data-ttu-id="75dd1-132">Nous importerons des données de **Table1** dans Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="75dd1-132">We will import data from **Table1** into Data Lake Store.</span></span> <span data-ttu-id="75dd1-133">Ensuite, nous exporterons les données de Data Lake Store vers **Table2**.</span><span class="sxs-lookup"><span data-stu-id="75dd1-133">Then, we will export data from Data Lake Store into **Table2**.</span></span> <span data-ttu-id="75dd1-134">Exécutez hello suivant extrait de code.</span><span class="sxs-lookup"><span data-stu-id="75dd1-134">Run hello following snippet.</span></span>

        INSERT INTO [dbo].[Table1] VALUES (1,'Neal','Kell'), (2,'Lila','Fulton'), (3, 'Erna','Myers'), (4,'Annette','Simpson');


## <a name="use-sqoop-from-an-hdinsight-cluster-with-access-toodata-lake-store"></a><span data-ttu-id="75dd1-135">Sqoop d’utilisation d’un cluster HDInsight avec accès tooData Lake Store</span><span class="sxs-lookup"><span data-stu-id="75dd1-135">Use Sqoop from an HDInsight cluster with access tooData Lake Store</span></span>
<span data-ttu-id="75dd1-136">Un cluster HDInsight a déjà des packages de Sqoop hello disponibles.</span><span class="sxs-lookup"><span data-stu-id="75dd1-136">An HDInsight cluster already has hello Sqoop packages available.</span></span> <span data-ttu-id="75dd1-137">Si vous avez configuré le cluster HDInsight de hello toouse Data Lake Store en tant qu’un stockage supplémentaire, vous pouvez utiliser Sqoop (sans aucune modification de configuration) tooimport/exporter des données entre une base de données relationnelle (dans cet exemple, la base de données SQL Azure) et un magasin Data Lake Store compte.</span><span class="sxs-lookup"><span data-stu-id="75dd1-137">If you have configured hello HDInsight cluster toouse Data Lake Store as an additional storage, you can use Sqoop (without any configuration changes) tooimport/export data between a relational database (in this example, Azure SQL Database) and a Data Lake Store account.</span></span>

1. <span data-ttu-id="75dd1-138">Pour ce didacticiel, nous supposons que vous avez créé un cluster de Linux, vous devez utiliser SSH tooconnect toohello cluster.</span><span class="sxs-lookup"><span data-stu-id="75dd1-138">For this tutorial, we assume you created a Linux cluster so you should use SSH tooconnect toohello cluster.</span></span> <span data-ttu-id="75dd1-139">Consultez [Connect tooa HDInsight de basés sur Linux cluster](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="75dd1-139">See [Connect tooa Linux-based HDInsight cluster](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>
2. <span data-ttu-id="75dd1-140">Vérifiez si vous avez accès hello compte Data Lake Store à partir du cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="75dd1-140">Verify whether you can access hello Data Lake Store account from hello cluster.</span></span> <span data-ttu-id="75dd1-141">Exécutez hello de commande suivante à partir de l’invite de commandes hello SSH :</span><span class="sxs-lookup"><span data-stu-id="75dd1-141">Run hello following command from hello SSH prompt:</span></span>

        hdfs dfs -ls adl://<data_lake_store_account>.azuredatalakestore.net/

    <span data-ttu-id="75dd1-142">Il doit fournir une liste de fichiers/dossiers Bonjour compte Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="75dd1-142">This should provide a list of files/folders in hello Data Lake Store account.</span></span>

### <a name="import-data-from-azure-sql-database-into-data-lake-store"></a><span data-ttu-id="75dd1-143">Importer des données à partir d’Azure SQL Database dans Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="75dd1-143">Import data from Azure SQL Database into Data Lake Store</span></span>
1. <span data-ttu-id="75dd1-144">Accédez répertoire toohello où Sqoop packages sont disponibles.</span><span class="sxs-lookup"><span data-stu-id="75dd1-144">Navigate toohello directory where Sqoop packages are available.</span></span> <span data-ttu-id="75dd1-145">En règle générale, il s’agit de `/usr/hdp/<version>/sqoop/bin`.</span><span class="sxs-lookup"><span data-stu-id="75dd1-145">Typically, this will be at `/usr/hdp/<version>/sqoop/bin`.</span></span>
2. <span data-ttu-id="75dd1-146">Importer les données hello **Table1** dans hello compte Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="75dd1-146">Import hello data from **Table1** into hello Data Lake Store account.</span></span> <span data-ttu-id="75dd1-147">Utilisez hello selon la syntaxe :</span><span class="sxs-lookup"><span data-stu-id="75dd1-147">Use hello following syntax:</span></span>

        sqoop-import --connect "jdbc:sqlserver://<sql-database-server-name>.database.windows.net:1433;username=<username>@<sql-database-server-name>;password=<password>;database=<sql-database-name>" --table Table1 --target-dir adl://<data-lake-store-name>.azuredatalakestore.net/Sqoop/SqoopImportTable1

    <span data-ttu-id="75dd1-148">Notez que **nom-serveur-de base de données-sql** espace réservé représente le nom hello du serveur hello sur lequel la base de données SQL Azure hello s’exécute.</span><span class="sxs-lookup"><span data-stu-id="75dd1-148">Note that **sql-database-server-name** placeholder represents hello name of hello server where hello Azure SQL database is running.</span></span> <span data-ttu-id="75dd1-149">**nom de base de données SQL** espace réservé représente le nom de base de données réelle hello.</span><span class="sxs-lookup"><span data-stu-id="75dd1-149">**sql-database-name** placeholder represents hello actual database name.</span></span>

    <span data-ttu-id="75dd1-150">Par exemple,</span><span class="sxs-lookup"><span data-stu-id="75dd1-150">For example,</span></span>


        sqoop-import --connect "jdbc:sqlserver://mysqoopserver.database.windows.net:1433;username=nitinme@mysqoopserver;password=<password>;database=mysqoopdatabase" --table Table1 --target-dir adl://myadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1

1. <span data-ttu-id="75dd1-151">Vérifiez que hello données ont été transférées compte Data Lake Store de toohello.</span><span class="sxs-lookup"><span data-stu-id="75dd1-151">Verify that hello data has been transferred toohello Data Lake Store account.</span></span> <span data-ttu-id="75dd1-152">Exécutez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="75dd1-152">Run hello following command:</span></span>

        hdfs dfs -ls adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/

    <span data-ttu-id="75dd1-153">Vous devez voir hello suivant de sortie.</span><span class="sxs-lookup"><span data-stu-id="75dd1-153">You should see hello following output.</span></span>


        -rwxrwxrwx   0 sshuser hdfs          0 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/_SUCCESS
        -rwxrwxrwx   0 sshuser hdfs         12 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/part-m-00000
        -rwxrwxrwx   0 sshuser hdfs         14 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/part-m-00001
        -rwxrwxrwx   0 sshuser hdfs         13 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/part-m-00002
        -rwxrwxrwx   0 sshuser hdfs         18 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/part-m-00003

    <span data-ttu-id="75dd1-154">Chaque **partie-m -*** fichier correspond ligne tooa dans la table de source de hello, **Table1**.</span><span class="sxs-lookup"><span data-stu-id="75dd1-154">Each **part-m-*** file corresponds tooa row in hello source table, **Table1**.</span></span> <span data-ttu-id="75dd1-155">Vous pouvez afficher le contenu de hello partie hello - m-* tooverify de fichiers.</span><span class="sxs-lookup"><span data-stu-id="75dd1-155">You can view hello contents of hello part-m-* files tooverify.</span></span>


### <a name="export-data-from-data-lake-store-into-azure-sql-database"></a><span data-ttu-id="75dd1-156">Exporter les données de Data Lake Store dans la base de données SQL Azure</span><span class="sxs-lookup"><span data-stu-id="75dd1-156">Export data from Data Lake Store into Azure SQL Database</span></span>
1. <span data-ttu-id="75dd1-157">Exporter les données de hello de table vide Data Lake Store compte toohello, **Table2**, Bonjour base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="75dd1-157">Export hello data from Data Lake Store account toohello empty table, **Table2**, in hello Azure SQL Database.</span></span> <span data-ttu-id="75dd1-158">Utiliser la syntaxe de hello.</span><span class="sxs-lookup"><span data-stu-id="75dd1-158">Use hello following syntax.</span></span>

        sqoop-export --connect "jdbc:sqlserver://<sql-database-server-name>.database.windows.net:1433;username=<username>@<sql-database-server-name>;password=<password>;database=<sql-database-name>" --table Table2 --export-dir adl://<data-lake-store-name>.azuredatalakestore.net/Sqoop/SqoopImportTable1 --input-fields-terminated-by ","

    <span data-ttu-id="75dd1-159">Par exemple,</span><span class="sxs-lookup"><span data-stu-id="75dd1-159">For example,</span></span>


        sqoop-export --connect "jdbc:sqlserver://mysqoopserver.database.windows.net:1433;username=nitinme@mysqoopserver;password=<password>;database=mysqoopdatabase" --table Table2 --export-dir adl://myadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1 --input-fields-terminated-by ","

1. <span data-ttu-id="75dd1-160">Vérifiez que hello données a été téléchargée table de base de données SQL toohello.</span><span class="sxs-lookup"><span data-stu-id="75dd1-160">Verify that hello data was uploaded toohello SQL Database table.</span></span> <span data-ttu-id="75dd1-161">Utilisez [SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md) ou Visual Studio tooconnect toohello base de données SQL Azure et puis hello exécution suivant la requête.</span><span class="sxs-lookup"><span data-stu-id="75dd1-161">Use [SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md) or Visual Studio tooconnect toohello Azure SQL Database and then run hello following query.</span></span>

        SELECT * FROM TABLE2

    <span data-ttu-id="75dd1-162">Cela doit avoir hello suivant de sortie.</span><span class="sxs-lookup"><span data-stu-id="75dd1-162">This should have hello following output.</span></span>

         ID  FName   LName
        ------------------
        1    Neal    Kell
        2    Lila    Fulton
        3    Erna    Myers
        4    Annette    Simpson

## <a name="performance-considerations-while-using-sqoop"></a><span data-ttu-id="75dd1-163">Considérations de performances lors de l’utilisation de Sqoop</span><span class="sxs-lookup"><span data-stu-id="75dd1-163">Performance considerations while using Sqoop</span></span>

<span data-ttu-id="75dd1-164">Pour votre Sqoop de réglage des performances de la tâche toocopy data tooData Lake Store, consultez [document de performances Sqoop](https://blogs.msdn.microsoft.com/bigdatasupport/2015/02/17/sqoop-job-performance-tuning-in-hdinsight-hadoop/).</span><span class="sxs-lookup"><span data-stu-id="75dd1-164">For performance tuning your Sqoop job toocopy data tooData Lake Store, see [Sqoop performance document](https://blogs.msdn.microsoft.com/bigdatasupport/2015/02/17/sqoop-job-performance-tuning-in-hdinsight-hadoop/).</span></span>

## <a name="see-also"></a><span data-ttu-id="75dd1-165">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="75dd1-165">See also</span></span>
* [<span data-ttu-id="75dd1-166">Copier des données d’objets BLOB de stockage Azure tooData Lake Store</span><span class="sxs-lookup"><span data-stu-id="75dd1-166">Copy data from Azure Storage Blobs tooData Lake Store</span></span>](data-lake-store-copy-data-azure-storage-blob.md)
* [<span data-ttu-id="75dd1-167">Sécuriser les données dans Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="75dd1-167">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="75dd1-168">Utiliser Azure Data Lake Analytics avec Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="75dd1-168">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="75dd1-169">Utiliser Azure HDInsight avec Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="75dd1-169">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
