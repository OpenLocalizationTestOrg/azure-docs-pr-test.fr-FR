---
title: aaaApache Sqoop avec Hadoop - Azure HDInsight | Documents Microsoft
description: "Découvrez comment toouse Apache Sqoop tooimport et exportation entre Hadoop dans HDInsight et d’une base de données SQL Azure."
editor: cgronlun
manager: jhubbard
services: hdinsight
documentationcenter: 
author: Blackmist
tags: azure-portal
keywords: hadoop sqoop, sqoop
ms.assetid: 303649a5-4be5-4933-bf1d-4b232083c354
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: larryfr
ms.openlocfilehash: b256285659bbcf18ff05e220ccdf51c21eb8fbf7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-apache-sqoop-tooimport-and-export-data-between-hadoop-on-hdinsight-and-sql-database"></a><span data-ttu-id="8f4b9-104">Utilisez Apache Sqoop tooimport et exporter des données entre Hadoop dans HDInsight et de la base de données SQL</span><span class="sxs-lookup"><span data-stu-id="8f4b9-104">Use Apache Sqoop tooimport and export data between Hadoop on HDInsight and SQL Database</span></span>

[!INCLUDE [sqoop-selector](../../includes/hdinsight-selector-use-sqoop.md)]

<span data-ttu-id="8f4b9-105">Découvrez comment toouse Apache Sqoop tooimport et exportation entre un Hadoop de cluster Azure HDInsight et de la base de données de base de données SQL Azure ou Microsoft SQL Server.</span><span class="sxs-lookup"><span data-stu-id="8f4b9-105">Learn how toouse Apache Sqoop tooimport and export between a Hadoop cluster in Azure HDInsight and Azure SQL Database or Microsoft SQL Server database.</span></span> <span data-ttu-id="8f4b9-106">Hello les étapes dans cette hello d’utilisation de document `sqoop` commande directement à partir de nœud principal de hello du cluster Hadoop de hello.</span><span class="sxs-lookup"><span data-stu-id="8f4b9-106">hello steps in this document use hello `sqoop` command directly from hello headnode of hello Hadoop cluster.</span></span> <span data-ttu-id="8f4b9-107">Vous utilisez le nœud principal de SSH tooconnect toohello et exécutez des commandes hello dans ce document.</span><span class="sxs-lookup"><span data-stu-id="8f4b9-107">You use SSH tooconnect toohello head node and run hello commands in this document.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8f4b9-108">Hello étapes décrites dans ce document fonctionnent uniquement avec les clusters HDInsight qui utilisent Linux.</span><span class="sxs-lookup"><span data-stu-id="8f4b9-108">hello steps in this document only work with HDInsight clusters that use Linux.</span></span> <span data-ttu-id="8f4b9-109">Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure.</span><span class="sxs-lookup"><span data-stu-id="8f4b9-109">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="8f4b9-110">Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="8f4b9-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="install-freetds"></a><span data-ttu-id="8f4b9-111">Installer FreeTDS</span><span class="sxs-lookup"><span data-stu-id="8f4b9-111">Install FreeTDS</span></span>

1. <span data-ttu-id="8f4b9-112">Utiliser SSH tooconnect toohello HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="8f4b9-112">Use SSH tooconnect toohello HDInsight cluster.</span></span> <span data-ttu-id="8f4b9-113">Par exemple, hello commande suivante connecte toohello le nœud principal principal d’un cluster nommé `mycluster`:</span><span class="sxs-lookup"><span data-stu-id="8f4b9-113">For example, hello following command connects toohello primary headnode of a cluster named `mycluster`:</span></span>

    ```bash
    ssh CLUSTERNAME-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="8f4b9-114">Pour en savoir plus, voir [Utilisation de SSH avec Hadoop Linux sur HDInsight depuis Linux, Unix ou OS X](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="8f4b9-114">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="8f4b9-115">Utilisez hello suivant commande tooinstall FreeTDS :</span><span class="sxs-lookup"><span data-stu-id="8f4b9-115">Use hello following command tooinstall FreeTDS:</span></span>

    ```bash
    sudo apt --assume-yes install freetds-dev freetds-bin
    ```

    <span data-ttu-id="8f4b9-116">FreeTDS est utilisé dans plusieurs étapes de tooconnect tooSQL de base de données.</span><span class="sxs-lookup"><span data-stu-id="8f4b9-116">FreeTDS is used in several steps tooconnect tooSQL Database.</span></span>

## <a name="create-hello-table-in-sql-database"></a><span data-ttu-id="8f4b9-117">Créer la table de hello dans la base de données SQL</span><span class="sxs-lookup"><span data-stu-id="8f4b9-117">Create hello table in SQL Database</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8f4b9-118">Si vous utilisez un cluster HDInsight de hello et base de données SQL créée dans [créer le cluster et la base de données SQL](hdinsight-use-sqoop.md), ignorez les étapes hello dans cette section.</span><span class="sxs-lookup"><span data-stu-id="8f4b9-118">If you are using hello HDInsight cluster and SQL Database created in [Create cluster and SQL database](hdinsight-use-sqoop.md), skip hello steps in this section.</span></span> <span data-ttu-id="8f4b9-119">Hello base de données et la table ont été créées comme partie de hello étapes Bonjour [créer le cluster et la base de données SQL](hdinsight-use-sqoop.md) document.</span><span class="sxs-lookup"><span data-stu-id="8f4b9-119">hello database and table were created as part of hello steps in hello [Create cluster and SQL database](hdinsight-use-sqoop.md) document.</span></span>

1. <span data-ttu-id="8f4b9-120">À partir de la session SSH de hello, utilisez hello suivant du serveur de base de données SQL de commande tooconnect toohello.</span><span class="sxs-lookup"><span data-stu-id="8f4b9-120">From hello SSH session, use hello following command tooconnect toohello SQL Database server.</span></span>

        TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P <adminPassword> -p 1433 -D sqooptest

    <span data-ttu-id="8f4b9-121">Vous recevez toohello similaire de sortie suivant du texte :</span><span class="sxs-lookup"><span data-stu-id="8f4b9-121">You receive output similar toohello following text:</span></span>

        locale is "en_US.UTF-8"
        locale charset is "UTF-8"
        using default charset "UTF-8"
        Default database being set toosqooptest
        1>

2. <span data-ttu-id="8f4b9-122">À hello `1>` invite, entrez hello suivant la requête :</span><span class="sxs-lookup"><span data-stu-id="8f4b9-122">At hello `1>` prompt, enter hello following query:</span></span>

    ```sql
    CREATE TABLE [dbo].[mobiledata](
    [clientid] [nvarchar](50),
    [querytime] [nvarchar](50),
    [market] [nvarchar](50),
    [deviceplatform] [nvarchar](50),
    [devicemake] [nvarchar](50),
    [devicemodel] [nvarchar](50),
    [state] [nvarchar](50),
    [country] [nvarchar](50),
    [querydwelltime] [float],
    [sessionid] [bigint],
    [sessionpagevieworder] [bigint])
    GO
    CREATE CLUSTERED INDEX mobiledata_clustered_index on mobiledata(clientid)
    GO
    ```

    <span data-ttu-id="8f4b9-123">Hello lorsque `GO` instruction est entrée, les instructions précédentes hello sont évaluées.</span><span class="sxs-lookup"><span data-stu-id="8f4b9-123">When hello `GO` statement is entered, hello previous statements are evaluated.</span></span> <span data-ttu-id="8f4b9-124">Tout d’abord, hello **mobiledata** table est créée, puis un index cluster est ajouté tooit (requis par la base de données SQL).</span><span class="sxs-lookup"><span data-stu-id="8f4b9-124">First, hello **mobiledata** table is created, then a clustered index is added tooit (required by SQL Database.)</span></span>

    <span data-ttu-id="8f4b9-125">Hello utilisation suivant tooverify de requête qui hello table a été créé :</span><span class="sxs-lookup"><span data-stu-id="8f4b9-125">Use hello following query tooverify that hello table has been created:</span></span>

    ```sql
    SELECT * FROM information_schema.tables
    GO
    ```

    <span data-ttu-id="8f4b9-126">Vous consultez toohello similaire de sortie suivant du texte :</span><span class="sxs-lookup"><span data-stu-id="8f4b9-126">You see output similar toohello following text:</span></span>

        TABLE_CATALOG   TABLE_SCHEMA    TABLE_NAME      TABLE_TYPE
        sqooptest       dbo     mobiledata      BASE TABLE

3. <span data-ttu-id="8f4b9-127">Entrez `exit` à hello `1>` tooexit hello tsql utilitaire d’invite.</span><span class="sxs-lookup"><span data-stu-id="8f4b9-127">Enter `exit` at hello `1>` prompt tooexit hello tsql utility.</span></span>

## <a name="sqoop-export"></a><span data-ttu-id="8f4b9-128">Exportation de Sqoop</span><span class="sxs-lookup"><span data-stu-id="8f4b9-128">Sqoop export</span></span>

1. <span data-ttu-id="8f4b9-129">Cluster de toohello connexion hello SSH, utilisez hello suivant tooverify commande que Sqoop peut voir votre base de données SQL :</span><span class="sxs-lookup"><span data-stu-id="8f4b9-129">From hello SSH connection toohello cluster, use hello following command tooverify that Sqoop can see your SQL Database:</span></span>

    ```bash
    sqoop list-databases --connect jdbc:sqlserver://<serverName>.database.windows.net:1433 --username <adminLogin> -P
    ```
    <span data-ttu-id="8f4b9-130">Lorsque vous y êtes invité, entrez le mot de passe de hello pour la connexion de base de données SQL hello.</span><span class="sxs-lookup"><span data-stu-id="8f4b9-130">When prompted, enter hello password for hello SQL Database login.</span></span>

    <span data-ttu-id="8f4b9-131">Cette commande renvoie une liste des bases de données, y compris hello **sqooptest** base de données que vous avez créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="8f4b9-131">This command returns a list of databases, including hello **sqooptest** database that you created earlier.</span></span>

2. <span data-ttu-id="8f4b9-132">données tooexport **hivesampletable** toohello **mobiledata** table, utilisez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="8f4b9-132">tooexport data from **hivesampletable** toohello **mobiledata** table, use hello following command:</span></span>

    ```bash
    sqoop export --connect 'jdbc:sqlserver://<serverName>.database.windows.net:1433;database=sqooptest' --username <adminLogin> -P --table 'mobiledata' --export-dir 'wasb:///hive/warehouse/hivesampletable' --fields-terminated-by '\t' -m 1
    ```

    <span data-ttu-id="8f4b9-133">Cette commande ordonne à Sqoop tooconnect toohello **sqooptest** base de données.</span><span class="sxs-lookup"><span data-stu-id="8f4b9-133">This command instructs Sqoop tooconnect toohello **sqooptest** database.</span></span> <span data-ttu-id="8f4b9-134">Sqoop exporte ensuite les données à partir de **wasb : / / / hive/entrepôt/hivesampletable** toohello **mobiledata** table.</span><span class="sxs-lookup"><span data-stu-id="8f4b9-134">Sqoop then exports data from **wasb:///hive/warehouse/hivesampletable** toohello **mobiledata** table.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="8f4b9-135">Utilisez `wasb:///` si le stockage par défaut de hello pour votre cluster est un compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="8f4b9-135">Use `wasb:///` if hello default storage for your cluster is an Azure Storage account.</span></span> <span data-ttu-id="8f4b9-136">Utilisez `adl:///` s’il s’agit d’un Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="8f4b9-136">Use `adl:///` if it is an Azure Data Lake Store.</span></span>

3. <span data-ttu-id="8f4b9-137">Après la commande hello, utilisez hello suivant commande tooconnect toohello de base de données à l’aide de TSQL :</span><span class="sxs-lookup"><span data-stu-id="8f4b9-137">After hello command completes, use hello following command tooconnect toohello database using TSQL:</span></span>

    ```bash
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P -p 1433 -D sqooptest
    ```

    <span data-ttu-id="8f4b9-138">Une fois connecté, hello utilisation suivant les instructions tooverify qui hello de données a été exporté toohello **mobiledata** table :</span><span class="sxs-lookup"><span data-stu-id="8f4b9-138">Once connected, use hello following statements tooverify that hello data was exported toohello **mobiledata** table:</span></span>

    ```sql
    SET ROWCOUNT 50;
    SELECT * FROM mobiledata
    GO
    ```

    <span data-ttu-id="8f4b9-139">Vous devez voir une liste de données de table de hello.</span><span class="sxs-lookup"><span data-stu-id="8f4b9-139">You should see a listing of data in hello table.</span></span> <span data-ttu-id="8f4b9-140">Type `exit` utilitaire de tooexit hello tsql.</span><span class="sxs-lookup"><span data-stu-id="8f4b9-140">Type `exit` tooexit hello tsql utility.</span></span>

## <a name="sqoop-import"></a><span data-ttu-id="8f4b9-141">Importation de Sqoop</span><span class="sxs-lookup"><span data-stu-id="8f4b9-141">Sqoop import</span></span>

1. <span data-ttu-id="8f4b9-142">Suivant de hello utilisez commande tooimport des données à partir de hello **mobiledata** table dans la base de données SQL, toohello **wasb : / / / didacticiels/usesqoop/importeddata** répertoire HDInsight :</span><span class="sxs-lookup"><span data-stu-id="8f4b9-142">Use hello following command tooimport data from hello **mobiledata** table in SQL Database, toohello **wasb:///tutorials/usesqoop/importeddata** directory on HDInsight:</span></span>

    ```bash
    sqoop import --connect 'jdbc:sqlserver://<serverName>.database.windows.net:1433;database=sqooptest' --username <adminLogin> --password <adminPassword> --table 'mobiledata' --target-dir 'wasb:///tutorials/usesqoop/importeddata' --fields-terminated-by '\t' --lines-terminated-by '\n' -m 1
    ```

    <span data-ttu-id="8f4b9-143">champs de Hello dans les données de salutation sont séparés par un caractère de tabulation et les lignes hello sont terminent par un caractère de nouvelle ligne.</span><span class="sxs-lookup"><span data-stu-id="8f4b9-143">hello fields in hello data are separated by a tab character, and hello lines are terminated by a new-line character.</span></span>

2. <span data-ttu-id="8f4b9-144">Une fois l’importation de hello terminée, utilisez hello suivant toolist commande données hello dans le répertoire hello :</span><span class="sxs-lookup"><span data-stu-id="8f4b9-144">Once hello import has completed, use hello following command toolist out hello data in hello new directory:</span></span>

    ```bash
    hdfs dfs -text /tutorials/usesqoop/importeddata/part-m-00000
    ```

## <a name="using-sql-server"></a><span data-ttu-id="8f4b9-145">Utilisation de SQL Server</span><span class="sxs-lookup"><span data-stu-id="8f4b9-145">Using SQL Server</span></span>

<span data-ttu-id="8f4b9-146">Vous pouvez également utiliser Sqoop tooimport et exporter des données à partir de SQL Server, dans votre centre de données ou sur une Machine virtuelle hébergée dans Azure.</span><span class="sxs-lookup"><span data-stu-id="8f4b9-146">You can also use Sqoop tooimport and export data from SQL Server, either in your data center or on a Virtual Machine hosted in Azure.</span></span> <span data-ttu-id="8f4b9-147">Hello les différences entre l’utilisation de la base de données SQL et SQL Server sont :</span><span class="sxs-lookup"><span data-stu-id="8f4b9-147">hello differences between using SQL Database and SQL Server are:</span></span>

* <span data-ttu-id="8f4b9-148">HDInsight et SQL Server doit être sur hello même réseau virtuel Azure.</span><span class="sxs-lookup"><span data-stu-id="8f4b9-148">Both HDInsight and SQL Server must be on hello same Azure Virtual Network.</span></span>

    <span data-ttu-id="8f4b9-149">Pour obtenir un exemple, consultez hello [réseau de se connecter de HDInsight tooyour local](./connect-on-premises-network.md) document.</span><span class="sxs-lookup"><span data-stu-id="8f4b9-149">For an example, see hello [Connect HDInsight tooyour on-premises network](./connect-on-premises-network.md) document.</span></span>

    <span data-ttu-id="8f4b9-150">Pour plus d’informations sur l’utilisation de HDInsight avec un réseau virtuel Azure, consultez hello [HDInsight d’étendre avec un réseau virtuel Azure](hdinsight-extend-hadoop-virtual-network.md) document.</span><span class="sxs-lookup"><span data-stu-id="8f4b9-150">For more information on using HDInsight with an Azure Virtual Network, see hello [Extend HDInsight with Azure Virtual Network](hdinsight-extend-hadoop-virtual-network.md) document.</span></span> <span data-ttu-id="8f4b9-151">Pour plus d’informations sur un réseau virtuel Azure, consultez hello [présentation du réseau virtuel](../virtual-network/virtual-networks-overview.md) document.</span><span class="sxs-lookup"><span data-stu-id="8f4b9-151">For more information on Azure Virtual Network, see hello [Virtual Network Overview](../virtual-network/virtual-networks-overview.md) document.</span></span>

* <span data-ttu-id="8f4b9-152">SQL Server doit être configuré tooallow l’authentification SQL.</span><span class="sxs-lookup"><span data-stu-id="8f4b9-152">SQL Server must be configured tooallow SQL authentication.</span></span> <span data-ttu-id="8f4b9-153">Pour plus d’informations, consultez hello [choisir un Mode d’authentification](https://msdn.microsoft.com/ms144284.aspx) document.</span><span class="sxs-lookup"><span data-stu-id="8f4b9-153">For more information, see hello [Choose an Authentication Mode](https://msdn.microsoft.com/ms144284.aspx) document.</span></span>

* <span data-ttu-id="8f4b9-154">Vous pouvez avoir des connexions à distance du tooaccept tooconfigure SQL Server.</span><span class="sxs-lookup"><span data-stu-id="8f4b9-154">You may have tooconfigure SQL Server tooaccept remote connections.</span></span> <span data-ttu-id="8f4b9-155">Pour plus d’informations, consultez hello [moteur de base de toohello de connexion tootroubleshoot SQL Server](http://social.technet.microsoft.com/wiki/contents/articles/2102.how-to-troubleshoot-connecting-to-the-sql-server-database-engine.aspx) document.</span><span class="sxs-lookup"><span data-stu-id="8f4b9-155">For more information, see hello [How tootroubleshoot connecting toohello SQL Server database engine](http://social.technet.microsoft.com/wiki/contents/articles/2102.how-to-troubleshoot-connecting-to-the-sql-server-database-engine.aspx) document.</span></span>

* <span data-ttu-id="8f4b9-156">Créer hello **sqooptest** base de données dans SQL Server à l’aide d’un utilitaire tel que **SQL Server Management Studio** ou **tsql**.</span><span class="sxs-lookup"><span data-stu-id="8f4b9-156">Create hello **sqooptest** database in SQL Server using a utility such as **SQL Server Management Studio** or **tsql**.</span></span> <span data-ttu-id="8f4b9-157">étapes de Hello pour l’utilisation de hello CLI d’Azure fonctionnent uniquement pour la base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="8f4b9-157">hello steps for using hello Azure CLI only work for Azure SQL Database.</span></span>

    <span data-ttu-id="8f4b9-158">Hello utilisation suivant hello de toocreate d’instructions Transact-SQL **mobiledata** table :</span><span class="sxs-lookup"><span data-stu-id="8f4b9-158">Use hello following Transact-SQL statements toocreate hello **mobiledata** table:</span></span>

    ```sql
    CREATE TABLE [dbo].[mobiledata](
    [clientid] [nvarchar](50),
    [querytime] [nvarchar](50),
    [market] [nvarchar](50),
    [deviceplatform] [nvarchar](50),
    [devicemake] [nvarchar](50),
    [devicemodel] [nvarchar](50),
    [state] [nvarchar](50),
    [country] [nvarchar](50),
    [querydwelltime] [float],
    [sessionid] [bigint],
    [sessionpagevieworder] [bigint])
    ```

* <span data-ttu-id="8f4b9-159">Lors de la connexion toohello SQL Server à partir de HDInsight, vous avez peut-être l’adresse IP toouse hello hello SQL Server.</span><span class="sxs-lookup"><span data-stu-id="8f4b9-159">When connecting toohello SQL Server from HDInsight, you may have toouse hello IP address of hello SQL Server.</span></span> <span data-ttu-id="8f4b9-160">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="8f4b9-160">For example:</span></span>

    ```bash
    sqoop import --connect 'jdbc:sqlserver://10.0.1.1:1433;database=sqooptest' --username <adminLogin> --password <adminPassword> --table 'mobiledata' --target-dir 'wasb:///tutorials/usesqoop/importeddata' --fields-terminated-by '\t' --lines-terminated-by '\n' -m 1
    ```

## <a name="limitations"></a><span data-ttu-id="8f4b9-161">Limites</span><span class="sxs-lookup"><span data-stu-id="8f4b9-161">Limitations</span></span>

* <span data-ttu-id="8f4b9-162">L’exportation en bloc - basés sur Linux avec un HDInsight, hello Sqoop connecteur utilisé tooexport données tooMicrosoft SQL Server ou base de données SQL Azure ne prend actuellement pas en charge les insertions en bloc.</span><span class="sxs-lookup"><span data-stu-id="8f4b9-162">Bulk export - With Linux-based HDInsight, hello Sqoop connector used tooexport data tooMicrosoft SQL Server or Azure SQL Database does not currently support bulk inserts.</span></span>

* <span data-ttu-id="8f4b9-163">Le traitement par lot - Hdinsight basés sur Linux, lorsque vous utilisez hello `-batch` commutateur lorsque vous effectuez des insertions, Sqoop effectue plusieurs insertions au lieu de traitement par lot des opérations d’insertion hello.</span><span class="sxs-lookup"><span data-stu-id="8f4b9-163">Batching - With Linux-based HDInsight, When using hello `-batch` switch when performing inserts, Sqoop makes multiple inserts instead of batching hello insert operations.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8f4b9-164">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="8f4b9-164">Next steps</span></span>

<span data-ttu-id="8f4b9-165">Maintenant que vous avez appris comment toouse Sqoop.</span><span class="sxs-lookup"><span data-stu-id="8f4b9-165">Now you have learned how toouse Sqoop.</span></span> <span data-ttu-id="8f4b9-166">toolearn, voir :</span><span class="sxs-lookup"><span data-stu-id="8f4b9-166">toolearn more, see:</span></span>

* <span data-ttu-id="8f4b9-167">[Utilisation d’Oozie avec HDInsight][hdinsight-use-oozie] : utilisez l’action Sqoop dans un workflow Oozie.</span><span class="sxs-lookup"><span data-stu-id="8f4b9-167">[Use Oozie with HDInsight][hdinsight-use-oozie]: Use Sqoop action in an Oozie workflow.</span></span>
* <span data-ttu-id="8f4b9-168">[Analyser des données de retard de vol avec HDInsight][hdinsight-analyze-flight-data]: utiliser la ruche de vol de tooanalyze retarder des données et ensuite utiliser la base de données Sqoop tooexport données tooan SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="8f4b9-168">[Analyze flight delay data using HDInsight][hdinsight-analyze-flight-data]: Use Hive tooanalyze flight delay data, and then use Sqoop tooexport data tooan Azure SQL database.</span></span>
* <span data-ttu-id="8f4b9-169">[Télécharger des données tooHDInsight][hdinsight-upload-data]: trouver d’autres méthodes pour le téléchargement des données tooHDInsight/Azure Blob storage.</span><span class="sxs-lookup"><span data-stu-id="8f4b9-169">[Upload data tooHDInsight][hdinsight-upload-data]: Find other methods for uploading data tooHDInsight/Azure Blob storage.</span></span>

[hdinsight-versions]:  hdinsight-component-versioning.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-storage]: ../hdinsight-hadoop-use-blob-storage.md
[hdinsight-analyze-flight-data]: hdinsight-analyze-flight-delay-data.md
[hdinsight-use-oozie]: hdinsight-use-oozie.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md

[sqldatabase-get-started]: ../sql-database-get-started.md
[sqldatabase-create-configue]: ../sql-database-create-configure.md

[powershell-start]: http://technet.microsoft.com/library/hh847889.aspx
[powershell-install]: /powershell/azureps-cmdlets-docs
[powershell-script]: http://technet.microsoft.com/library/ee176949.aspx

[sqoop-user-guide-1.4.4]: https://sqoop.apache.org/docs/1.4.4/SqoopUserGuide.html
