---
title: "Copier des données entre Data Lake Store et une base de données SQL Azure à l’aide de Sqoop | Microsoft Docs"
description: "Utiliser Sqoop pour copier des données entre Azure SQL Database et Data Lake Store"
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
ms.openlocfilehash: 53bf33f6027f1f365bd92251490d5c851fb83f8b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="copy-data-between-data-lake-store-and-azure-sql-database-using-sqoop"></a><span data-ttu-id="999e1-103">Copier des données entre Data Lake Store et une base de données SQL Azure à l’aide de Sqoop</span><span class="sxs-lookup"><span data-stu-id="999e1-103">Copy data between Data Lake Store and Azure SQL database using Sqoop</span></span>
<span data-ttu-id="999e1-104">Découvrez comment utiliser Apache Sqoop pour importer et exporter des données entre Azure SQL Database et Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="999e1-104">Learn how to use Apache Sqoop to import and export data between Azure SQL Database and Data Lake Store.</span></span>

## <a name="what-is-sqoop"></a><span data-ttu-id="999e1-105">Qu'est-ce que Sqoop ?</span><span class="sxs-lookup"><span data-stu-id="999e1-105">What is Sqoop?</span></span>
<span data-ttu-id="999e1-106">Les applications Big Data sont un choix naturel pour le traitement des données non structurées et semi-structurées, telles que les journaux et les fichiers.</span><span class="sxs-lookup"><span data-stu-id="999e1-106">Big data applications are a natural choice for processing unstructured and semi-structured data, such as logs and files.</span></span> <span data-ttu-id="999e1-107">Toutefois, il peut également être nécessaire de traiter des données structurées stockées dans des bases de données relationnelles.</span><span class="sxs-lookup"><span data-stu-id="999e1-107">However, there may also be a need to process structured data that is stored in relational databases.</span></span>

<span data-ttu-id="999e1-108">[Apache Sqoop](https://sqoop.apache.org/docs/1.4.4/SqoopUserGuide.html) est un outil conçu pour transférer des données entre des bases de données relationnelles et un référentiel Big Data, par exemple Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="999e1-108">[Apache Sqoop](https://sqoop.apache.org/docs/1.4.4/SqoopUserGuide.html) is a tool designed to transfer data between  relational databases and a big data repository, such as Data Lake Store.</span></span> <span data-ttu-id="999e1-109">Vous pouvez l’utiliser pour importer des données à partir d’un système de gestion de base de données relationnelle (SGBDR), comme Azure SQL Database, dans Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="999e1-109">You can use it to import data from a relational database management system (RDBMS) such as Azure SQL Database into Data Lake Store.</span></span> <span data-ttu-id="999e1-110">Vous pouvez ensuite transformer et analyser les données à l’aide de charges de travail Big Data, puis exporter les données dans un SGBDR.</span><span class="sxs-lookup"><span data-stu-id="999e1-110">You can then transform and analyze the data using big data workloads and then export the data back into an RDBMS.</span></span> <span data-ttu-id="999e1-111">Dans ce didacticiel, vous utilisez une base de données SQL Azure comme base de données relationnelle pour les opérations d’importation et d’exportation.</span><span class="sxs-lookup"><span data-stu-id="999e1-111">In this tutorial, you use an Azure SQL Database as your relational database to import/export from.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="999e1-112">Composants requis</span><span class="sxs-lookup"><span data-stu-id="999e1-112">Prerequisites</span></span>
<span data-ttu-id="999e1-113">Avant de commencer cet article, vous devez disposer des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="999e1-113">Before you begin this article, you must have the following:</span></span>

* <span data-ttu-id="999e1-114">**Un abonnement Azure**.</span><span class="sxs-lookup"><span data-stu-id="999e1-114">**An Azure subscription**.</span></span> <span data-ttu-id="999e1-115">Consultez la page [Obtention d’un essai gratuit d’Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="999e1-115">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="999e1-116">**Un compte Azure Data Lake Store**.</span><span class="sxs-lookup"><span data-stu-id="999e1-116">**An Azure Data Lake Store account**.</span></span> <span data-ttu-id="999e1-117">Pour savoir comment en créer un, consultez [Prise en main d'Azure Data Lake Store](data-lake-store-get-started-portal.md)</span><span class="sxs-lookup"><span data-stu-id="999e1-117">For instructions on how to create one, see [Get started with Azure Data Lake Store](data-lake-store-get-started-portal.md)</span></span>
* <span data-ttu-id="999e1-118">**Cluster Azure HDInsight** ayant accès à un compte Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="999e1-118">**Azure HDInsight cluster** with access to a Data Lake Store account.</span></span> <span data-ttu-id="999e1-119">Voir [Créer un cluster HDInsight avec Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="999e1-119">See [Create an HDInsight cluster with Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md).</span></span> <span data-ttu-id="999e1-120">Cet article suppose que vous disposez d’un cluster Linux HDInsight avec accès à Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="999e1-120">This article assumes you have an HDInsight Linux cluster with Data Lake Store access.</span></span>
* <span data-ttu-id="999e1-121">**Base de données SQL Azure**.</span><span class="sxs-lookup"><span data-stu-id="999e1-121">**Azure SQL Database**.</span></span> <span data-ttu-id="999e1-122">Pour savoir comment en créer un, consultez [Créer une base de données SQL Azure](../sql-database/sql-database-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="999e1-122">For instructions on how to create one, see [Create an Azure SQL database](../sql-database/sql-database-get-started.md)</span></span>

## <a name="do-you-learn-fast-with-videos"></a><span data-ttu-id="999e1-123">Les vidéos vous permettent-elles d’apprendre rapidement ?</span><span class="sxs-lookup"><span data-stu-id="999e1-123">Do you learn fast with videos?</span></span>
<span data-ttu-id="999e1-124">[Regardez cette vidéo](https://mix.office.com/watch/1butcdjxmu114) pour savoir comment copier des données entre des objets blob Azure Storage et Data Lake Store à l’aide de DistCp.</span><span class="sxs-lookup"><span data-stu-id="999e1-124">[Watch this video](https://mix.office.com/watch/1butcdjxmu114) on how to copy data between Azure Storage Blobs and Data Lake Store using DistCp.</span></span>

## <a name="create-sample-tables-in-the-azure-sql-database"></a><span data-ttu-id="999e1-125">Créer des exemples de tables dans la base de données SQL Azure</span><span class="sxs-lookup"><span data-stu-id="999e1-125">Create sample tables in the Azure SQL Database</span></span>
1. <span data-ttu-id="999e1-126">Pour commencer, créez deux exemples de tables dans la base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="999e1-126">To start with, create two sample tables in the Azure SQL Database.</span></span> <span data-ttu-id="999e1-127">Utilisez [SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md) ou Visual Studio pour vous connecter à la base de données SQL Azure, puis exécutez les requêtes suivantes.</span><span class="sxs-lookup"><span data-stu-id="999e1-127">Use [SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md) or Visual Studio to connect to the Azure SQL Database and then run the following queries.</span></span>

    <span data-ttu-id="999e1-128">**Créer Table1**</span><span class="sxs-lookup"><span data-stu-id="999e1-128">**Create Table1**</span></span>

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

    <span data-ttu-id="999e1-129">**Créer Table2**</span><span class="sxs-lookup"><span data-stu-id="999e1-129">**Create Table2**</span></span>

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
2. <span data-ttu-id="999e1-130">Dans **Table1**, ajoutez des exemples de données.</span><span class="sxs-lookup"><span data-stu-id="999e1-130">In **Table1**, add some sample data.</span></span> <span data-ttu-id="999e1-131">Laissez **Table2** vide.</span><span class="sxs-lookup"><span data-stu-id="999e1-131">Leave **Table2** empty.</span></span> <span data-ttu-id="999e1-132">Nous importerons des données de **Table1** dans Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="999e1-132">We will import data from **Table1** into Data Lake Store.</span></span> <span data-ttu-id="999e1-133">Ensuite, nous exporterons les données de Data Lake Store vers **Table2**.</span><span class="sxs-lookup"><span data-stu-id="999e1-133">Then, we will export data from Data Lake Store into **Table2**.</span></span> <span data-ttu-id="999e1-134">Exécutez l'extrait de code suivant.</span><span class="sxs-lookup"><span data-stu-id="999e1-134">Run the following snippet.</span></span>

        INSERT INTO [dbo].[Table1] VALUES (1,'Neal','Kell'), (2,'Lila','Fulton'), (3, 'Erna','Myers'), (4,'Annette','Simpson');


## <a name="use-sqoop-from-an-hdinsight-cluster-with-access-to-data-lake-store"></a><span data-ttu-id="999e1-135">Utiliser Sqoop à partir d’un cluster HDInsight avec accès à Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="999e1-135">Use Sqoop from an HDInsight cluster with access to Data Lake Store</span></span>
<span data-ttu-id="999e1-136">Un cluster HDInsight dispose déjà des packages Sqoop.</span><span class="sxs-lookup"><span data-stu-id="999e1-136">An HDInsight cluster already has the Sqoop packages available.</span></span> <span data-ttu-id="999e1-137">Si vous avez configuré le cluster HDInsight pour utiliser un Data Lake Store comme un espace de stockage supplémentaire, vous pouvez utiliser Sqoop (sans aucune modification de configuration) pour importer/exporter des données entre une base de données relationnelle (dans cet exemple, Azure SQL Database) et un compte Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="999e1-137">If you have configured the HDInsight cluster to use Data Lake Store as an additional storage, you can use Sqoop (without any configuration changes) to import/export data between a relational database (in this example, Azure SQL Database) and a Data Lake Store account.</span></span>

1. <span data-ttu-id="999e1-138">Pour ce didacticiel, nous supposons que vous avez créé un cluster Linux ; vous devez donc utiliser SSH pour vous connecter au cluster.</span><span class="sxs-lookup"><span data-stu-id="999e1-138">For this tutorial, we assume you created a Linux cluster so you should use SSH to connect to the cluster.</span></span> <span data-ttu-id="999e1-139">Consultez [Connexion à un cluster HDInsight sous Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="999e1-139">See [Connect to a Linux-based HDInsight cluster](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>
2. <span data-ttu-id="999e1-140">Vérifiez si vous pouvez accéder au compte Data Lake Store à partir du cluster.</span><span class="sxs-lookup"><span data-stu-id="999e1-140">Verify whether you can access the Data Lake Store account from the cluster.</span></span> <span data-ttu-id="999e1-141">Exécutez la commande suivante depuis une invite SSH :</span><span class="sxs-lookup"><span data-stu-id="999e1-141">Run the following command from the SSH prompt:</span></span>

        hdfs dfs -ls adl://<data_lake_store_account>.azuredatalakestore.net/

    <span data-ttu-id="999e1-142">Vous devriez accéder à une liste des fichiers/dossiers contenus dans le compte Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="999e1-142">This should provide a list of files/folders in the Data Lake Store account.</span></span>

### <a name="import-data-from-azure-sql-database-into-data-lake-store"></a><span data-ttu-id="999e1-143">Importer des données à partir d’Azure SQL Database dans Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="999e1-143">Import data from Azure SQL Database into Data Lake Store</span></span>
1. <span data-ttu-id="999e1-144">Accédez au répertoire dans lequel se trouvent les packages Sqoop.</span><span class="sxs-lookup"><span data-stu-id="999e1-144">Navigate to the directory where Sqoop packages are available.</span></span> <span data-ttu-id="999e1-145">En règle générale, il s’agit de `/usr/hdp/<version>/sqoop/bin`.</span><span class="sxs-lookup"><span data-stu-id="999e1-145">Typically, this will be at `/usr/hdp/<version>/sqoop/bin`.</span></span>
2. <span data-ttu-id="999e1-146">Importez les données de **Table1** dans le compte Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="999e1-146">Import the data from **Table1** into the Data Lake Store account.</span></span> <span data-ttu-id="999e1-147">Utilisez la syntaxe suivante :</span><span class="sxs-lookup"><span data-stu-id="999e1-147">Use the following syntax:</span></span>

        sqoop-import --connect "jdbc:sqlserver://<sql-database-server-name>.database.windows.net:1433;username=<username>@<sql-database-server-name>;password=<password>;database=<sql-database-name>" --table Table1 --target-dir adl://<data-lake-store-name>.azuredatalakestore.net/Sqoop/SqoopImportTable1

    <span data-ttu-id="999e1-148">Notez que l’espace réservé **sql-database-server-name** représente le nom du serveur sur lequel s’exécute la base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="999e1-148">Note that **sql-database-server-name** placeholder represents the name of the server where the Azure SQL database is running.</span></span> <span data-ttu-id="999e1-149">L’espace réservé **sql-database-name** désigne le nom de la base de données.</span><span class="sxs-lookup"><span data-stu-id="999e1-149">**sql-database-name** placeholder represents the actual database name.</span></span>

    <span data-ttu-id="999e1-150">Par exemple,</span><span class="sxs-lookup"><span data-stu-id="999e1-150">For example,</span></span>


        sqoop-import --connect "jdbc:sqlserver://mysqoopserver.database.windows.net:1433;username=nitinme@mysqoopserver;password=<password>;database=mysqoopdatabase" --table Table1 --target-dir adl://myadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1

1. <span data-ttu-id="999e1-151">Vérifiez que les données ont été transférées vers le compte Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="999e1-151">Verify that the data has been transferred to the Data Lake Store account.</span></span> <span data-ttu-id="999e1-152">Exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="999e1-152">Run the following command:</span></span>

        hdfs dfs -ls adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/

    <span data-ttu-id="999e1-153">La sortie suivante s'affiche.</span><span class="sxs-lookup"><span data-stu-id="999e1-153">You should see the following output.</span></span>


        -rwxrwxrwx   0 sshuser hdfs          0 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/_SUCCESS
        -rwxrwxrwx   0 sshuser hdfs         12 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/part-m-00000
        -rwxrwxrwx   0 sshuser hdfs         14 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/part-m-00001
        -rwxrwxrwx   0 sshuser hdfs         13 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/part-m-00002
        -rwxrwxrwx   0 sshuser hdfs         18 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/part-m-00003

    <span data-ttu-id="999e1-154">Chaque fichier **part-m-*** correspond à une ligne dans la table source **Table1**.</span><span class="sxs-lookup"><span data-stu-id="999e1-154">Each **part-m-*** file corresponds to a row in the source table, **Table1**.</span></span> <span data-ttu-id="999e1-155">Vous pouvez afficher le contenu des fichiers part-m-* à vérifier.</span><span class="sxs-lookup"><span data-stu-id="999e1-155">You can view the contents of the part-m-* files to verify.</span></span>


### <a name="export-data-from-data-lake-store-into-azure-sql-database"></a><span data-ttu-id="999e1-156">Exporter les données de Data Lake Store dans la base de données SQL Azure</span><span class="sxs-lookup"><span data-stu-id="999e1-156">Export data from Data Lake Store into Azure SQL Database</span></span>
1. <span data-ttu-id="999e1-157">Exportez les données du compte Data Lake Store vers la table vide, **Table2**, dans la base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="999e1-157">Export the data from Data Lake Store account to the empty table, **Table2**, in the Azure SQL Database.</span></span> <span data-ttu-id="999e1-158">Utilisez la syntaxe suivante.</span><span class="sxs-lookup"><span data-stu-id="999e1-158">Use the following syntax.</span></span>

        sqoop-export --connect "jdbc:sqlserver://<sql-database-server-name>.database.windows.net:1433;username=<username>@<sql-database-server-name>;password=<password>;database=<sql-database-name>" --table Table2 --export-dir adl://<data-lake-store-name>.azuredatalakestore.net/Sqoop/SqoopImportTable1 --input-fields-terminated-by ","

    <span data-ttu-id="999e1-159">Par exemple,</span><span class="sxs-lookup"><span data-stu-id="999e1-159">For example,</span></span>


        sqoop-export --connect "jdbc:sqlserver://mysqoopserver.database.windows.net:1433;username=nitinme@mysqoopserver;password=<password>;database=mysqoopdatabase" --table Table2 --export-dir adl://myadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1 --input-fields-terminated-by ","

1. <span data-ttu-id="999e1-160">Vérifiez que les données ont été chargées sur la table de la base de données SQL.</span><span class="sxs-lookup"><span data-stu-id="999e1-160">Verify that the data was uploaded to the SQL Database table.</span></span> <span data-ttu-id="999e1-161">Utilisez [SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md) ou Visual Studio pour vous connecter à la base de données SQL Azure, puis exécutez la requête suivante.</span><span class="sxs-lookup"><span data-stu-id="999e1-161">Use [SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md) or Visual Studio to connect to the Azure SQL Database and then run the following query.</span></span>

        SELECT * FROM TABLE2

    <span data-ttu-id="999e1-162">Vous devriez obtenir le résultat suivant.</span><span class="sxs-lookup"><span data-stu-id="999e1-162">This should have the following output.</span></span>

         ID  FName   LName
        ------------------
        1    Neal    Kell
        2    Lila    Fulton
        3    Erna    Myers
        4    Annette    Simpson

## <a name="performance-considerations-while-using-sqoop"></a><span data-ttu-id="999e1-163">Considérations de performances lors de l’utilisation de Sqoop</span><span class="sxs-lookup"><span data-stu-id="999e1-163">Performance considerations while using Sqoop</span></span>

<span data-ttu-id="999e1-164">Pour optimiser les performances de votre tâche Sqoop pour copier des données vers Data Lake Store, consultez le [document de performance Sqoop](https://blogs.msdn.microsoft.com/bigdatasupport/2015/02/17/sqoop-job-performance-tuning-in-hdinsight-hadoop/).</span><span class="sxs-lookup"><span data-stu-id="999e1-164">For performance tuning your Sqoop job to copy data to Data Lake Store, see [Sqoop performance document](https://blogs.msdn.microsoft.com/bigdatasupport/2015/02/17/sqoop-job-performance-tuning-in-hdinsight-hadoop/).</span></span>

## <a name="see-also"></a><span data-ttu-id="999e1-165">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="999e1-165">See also</span></span>
* [<span data-ttu-id="999e1-166">Copier des données d’objets blob Azure Storage vers Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="999e1-166">Copy data from Azure Storage Blobs to Data Lake Store</span></span>](data-lake-store-copy-data-azure-storage-blob.md)
* [<span data-ttu-id="999e1-167">Sécuriser les données dans Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="999e1-167">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="999e1-168">Utiliser Azure Data Lake Analytics avec Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="999e1-168">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="999e1-169">Utiliser Azure HDInsight avec Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="999e1-169">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
