---
title: "aaaUse données de tooanalyze Apache Spark dans Azure Data Lake Store | Documents Microsoft"
description: "Exécuter des travaux de Spark tooanalyze les données stockées dans Azure Data Lake Store"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 1f174323-c17b-428c-903d-04f0e272784c
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 3b7f628f7a8114d2ca6f3f9219ce107905f1c818
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hdinsight-spark-cluster-tooanalyze-data-in-data-lake-store"></a><span data-ttu-id="dcfdc-103">Utiliser des données tooanalyze du cluster HDInsight Spark dans Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="dcfdc-103">Use HDInsight Spark cluster tooanalyze data in Data Lake Store</span></span>

<span data-ttu-id="dcfdc-104">Dans ce didacticiel, vous utilisez bloc-notes jupyter disponible avec HDInsight Spark clusters toorun une tâche qui lit des données à partir d’un compte Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="dcfdc-104">In this tutorial, you use Jupyter notebook available with HDInsight Spark clusters toorun a job that reads data from a Data Lake Store account.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dcfdc-105">Composants requis</span><span class="sxs-lookup"><span data-stu-id="dcfdc-105">Prerequisites</span></span>

* <span data-ttu-id="dcfdc-106">Compte Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="dcfdc-106">Azure Data Lake Store account.</span></span> <span data-ttu-id="dcfdc-107">Suivez les instructions de hello à [prise en main Azure Data Lake Store à l’aide de hello Azure Portal](../data-lake-store/data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="dcfdc-107">Follow hello instructions at [Get started with Azure Data Lake Store using hello Azure Portal](../data-lake-store/data-lake-store-get-started-portal.md).</span></span>

* <span data-ttu-id="dcfdc-108">Cluster Azure HDInsight Spark avec Data Lake Store comme système de stockage.</span><span class="sxs-lookup"><span data-stu-id="dcfdc-108">Azure HDInsight Spark cluster with Data Lake Store as storage.</span></span> <span data-ttu-id="dcfdc-109">Suivez les instructions de hello à [créer un cluster HDInsight à l’aide du portail Azure Data Lake Store](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="dcfdc-109">Follow hello instructions at [Create an HDInsight cluster with Data Lake Store using Azure Portal](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span>

    
## <a name="prepare-hello-data"></a><span data-ttu-id="dcfdc-110">Préparer les données de salutation</span><span class="sxs-lookup"><span data-stu-id="dcfdc-110">Prepare hello data</span></span>

> [!NOTE]
> <span data-ttu-id="dcfdc-111">Il est inutile tooperform cette étape si vous avez créé le cluster HDInsight de hello avec Data Lake Store en tant que stockage de la valeur par défaut.</span><span class="sxs-lookup"><span data-stu-id="dcfdc-111">You do not need tooperform this step if you have created hello HDInsight cluster with Data Lake Store as default storage.</span></span> <span data-ttu-id="dcfdc-112">processus de création de cluster Hello ajoute quelques exemples de données dans le compte Data Lake Store hello que vous spécifiez lors de la création du cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="dcfdc-112">hello cluster creation processes adds some sample data in hello Data Lake Store account that you specify while creating hello cluster.</span></span> <span data-ttu-id="dcfdc-113">Ignorer la section de toohello [cluster utilisez HDInsight Spark avec Data Lake Store](#use-an-hdinsight-spark-cluster-with-data-lake-store).</span><span class="sxs-lookup"><span data-stu-id="dcfdc-113">Skip toohello section [Use HDInsight Spark cluster with Data Lake Store](#use-an-hdinsight-spark-cluster-with-data-lake-store).</span></span>
>
>

<span data-ttu-id="dcfdc-114">Si vous avez créé un cluster HDInsight avec Data Lake Store en tant qu’objet Blob de stockage Azure en tant que stockage par défaut et de stockage supplémentaire, vous devez tout d’abord copier sur certaines toohello de données exemple compte Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="dcfdc-114">If you created an HDInsight cluster with Data Lake Store as additional storage and Azure Storage Blob as default storage, you should first copy over some sample data toohello Data Lake Store account.</span></span> <span data-ttu-id="dcfdc-115">Vous pouvez utiliser les exemples de données hello de hello qu'objet Blob de stockage Azure associée au cluster HDInsight de hello.</span><span class="sxs-lookup"><span data-stu-id="dcfdc-115">You can use hello sample data from hello Azure Storage Blob associated with hello HDInsight cluster.</span></span> <span data-ttu-id="dcfdc-116">Vous pouvez utiliser hello [ADLCopy outil](http://aka.ms/downloadadlcopy) toodo donc.</span><span class="sxs-lookup"><span data-stu-id="dcfdc-116">You can use hello [ADLCopy tool](http://aka.ms/downloadadlcopy) toodo so.</span></span> <span data-ttu-id="dcfdc-117">Téléchargez et installez l’outil de hello à partir du lien de hello.</span><span class="sxs-lookup"><span data-stu-id="dcfdc-117">Download and install hello tool from hello link.</span></span>

1. <span data-ttu-id="dcfdc-118">Ouvrez une invite de commandes et accédez répertoire toohello où AdlCopy est installé, généralement `%HOMEPATH%\Documents\adlcopy`.</span><span class="sxs-lookup"><span data-stu-id="dcfdc-118">Open a command prompt and navigate toohello directory where AdlCopy is installed, typically `%HOMEPATH%\Documents\adlcopy`.</span></span>

2. <span data-ttu-id="dcfdc-119">Exécutez hello suivant commande toocopy un blob spécifique de hello source conteneur tooa Data Lake Store :</span><span class="sxs-lookup"><span data-stu-id="dcfdc-119">Run hello following command toocopy a specific blob from hello source container tooa Data Lake Store:</span></span>

        AdlCopy /source https://<source_account>.blob.core.windows.net/<source_container>/<blob name> /dest swebhdfs://<dest_adls_account>.azuredatalakestore.net/<dest_folder>/ /sourcekey <storage_account_key_for_storage_container>

    <span data-ttu-id="dcfdc-120">Hello de copie **HVAC.csv** exemples de données de fichiers au **/HdiSamples/HdiSamples/SensorSampleData/hvac/** toohello compte Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="dcfdc-120">Copy hello **HVAC.csv** sample data file at **/HdiSamples/HdiSamples/SensorSampleData/hvac/** toohello Azure Data Lake Store account.</span></span> <span data-ttu-id="dcfdc-121">extrait de code Hello doit ressembler à :</span><span class="sxs-lookup"><span data-stu-id="dcfdc-121">hello code snippet should look like:</span></span>

        AdlCopy /Source https://mydatastore.blob.core.windows.net/mysparkcluster/HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv /dest swebhdfs://mydatalakestore.azuredatalakestore.net/hvac/ /sourcekey uJUfvD6cEvhfLoBae2yyQf8t9/BpbWZ4XoYj4kAS5Jf40pZaMNf0q6a8yqTxktwVgRED4vPHeh/50iS9atS5LQ==

   > [!WARNING]
   > <span data-ttu-id="dcfdc-122">Vérifiez que hello de fichier et les noms de chemin d’accès sont en majuscules de hello.</span><span class="sxs-lookup"><span data-stu-id="dcfdc-122">Make sure you hello file and path names are in hello proper case.</span></span>
   >
   >
3. <span data-ttu-id="dcfdc-123">Vous serez invité à tooenter informations d’identification hello pour hello abonnement Azure sous lequel vous avez à votre compte Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="dcfdc-123">You will be prompted tooenter hello credentials for hello Azure subscription under which you have your Data Lake Store account.</span></span> <span data-ttu-id="dcfdc-124">Vous découvrez une sortie similaire toohello :</span><span class="sxs-lookup"><span data-stu-id="dcfdc-124">You will see an output similar toohello following:</span></span>

        Initializing Copy.
        Copy Started.
        100% data copied.
        Copy Completed. 1 file copied.

    <span data-ttu-id="dcfdc-125">fichier de données Hello (**HVAC.csv**) doivent être copiées dans un dossier **/hvac** Bonjour compte Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="dcfdc-125">hello data file (**HVAC.csv**) will be copied under a folder **/hvac** in hello Data Lake Store account.</span></span>

## <a name="use-an-hdinsight-spark-cluster-with-data-lake-store"></a><span data-ttu-id="dcfdc-126">Utiliser un cluster HDInsight Spark avec Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="dcfdc-126">Use an HDInsight Spark cluster with Data Lake Store</span></span>

1. <span data-ttu-id="dcfdc-127">À partir de hello [Azure Portal](https://portal.azure.com/), à partir du tableau d’accueil hello, cliquez sur la vignette hello pour votre cluster Spark (si vous avez épinglé il toohello tableau d’accueil).</span><span class="sxs-lookup"><span data-stu-id="dcfdc-127">From hello [Azure Portal](https://portal.azure.com/), from hello startboard, click hello tile for your Spark cluster (if you pinned it toohello startboard).</span></span> <span data-ttu-id="dcfdc-128">Vous pouvez également naviguer cluster tooyour sous **parcourir tous les** > **Clusters HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="dcfdc-128">You can also navigate tooyour cluster under **Browse All** > **HDInsight Clusters**.</span></span>

2. <span data-ttu-id="dcfdc-129">Dans le panneau de cluster Spark hello, cliquez sur **liens rapides**, puis à partir de hello **tableau de bord de Cluster** panneau, cliquez sur **bloc-notes Jupyter**.</span><span class="sxs-lookup"><span data-stu-id="dcfdc-129">From hello Spark cluster blade, click **Quick Links**, and then from hello **Cluster Dashboard** blade, click **Jupyter Notebook**.</span></span> <span data-ttu-id="dcfdc-130">Si vous y êtes invité, entrez les informations d’identification du admin de hello pour le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="dcfdc-130">If prompted, enter hello admin credentials for hello cluster.</span></span>

   > [!NOTE]
   > <span data-ttu-id="dcfdc-131">Vous pouvez également atteindre hello bloc-notes Jupyter pour votre cluster en hello ouverture suivante d’URL dans votre navigateur.</span><span class="sxs-lookup"><span data-stu-id="dcfdc-131">You may also reach hello Jupyter Notebook for your cluster by opening hello following URL in your browser.</span></span> <span data-ttu-id="dcfdc-132">Remplacez **CLUSTERNAME** avec nom hello de votre cluster :</span><span class="sxs-lookup"><span data-stu-id="dcfdc-132">Replace **CLUSTERNAME** with hello name of your cluster:</span></span>
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >

3. <span data-ttu-id="dcfdc-133">Créer un nouveau bloc-notes.</span><span class="sxs-lookup"><span data-stu-id="dcfdc-133">Create a new notebook.</span></span> <span data-ttu-id="dcfdc-134">Cliquez sur **Nouveau**, puis sur **PySpark**.</span><span class="sxs-lookup"><span data-stu-id="dcfdc-134">Click **New**, and then click **PySpark**.</span></span>

    <span data-ttu-id="dcfdc-135">![Créer un bloc-notes Jupyter](./media/hdinsight-apache-spark-use-with-data-lake-store/hdinsight-create-jupyter-notebook.png "Créer un bloc-notes Jupyter")</span><span class="sxs-lookup"><span data-stu-id="dcfdc-135">![Create a new Jupyter notebook](./media/hdinsight-apache-spark-use-with-data-lake-store/hdinsight-create-jupyter-notebook.png "Create a new Jupyter notebook")</span></span>

4. <span data-ttu-id="dcfdc-136">Étant donné que vous avez créé un ordinateur portable à l’aide de noyau de PySpark hello, il est inutile toocreate les contextes explicitement.</span><span class="sxs-lookup"><span data-stu-id="dcfdc-136">Because you created a notebook using hello PySpark kernel, you do not need toocreate any contexts explicitly.</span></span> <span data-ttu-id="dcfdc-137">contextes de Spark et Hive Hello seront automatiquement créés pour vous lors de l’exécution de la première cellule de code hello.</span><span class="sxs-lookup"><span data-stu-id="dcfdc-137">hello Spark and Hive contexts will be automatically created for you when you run hello first code cell.</span></span> <span data-ttu-id="dcfdc-138">Vous pouvez commencer par importer les types hello requis pour ce scénario.</span><span class="sxs-lookup"><span data-stu-id="dcfdc-138">You can start by importing hello types required for this scenario.</span></span> <span data-ttu-id="dcfdc-139">toodo coller donc hello suivant extrait de code dans une cellule appuyez sur **MAJ + ENTRÉE**.</span><span class="sxs-lookup"><span data-stu-id="dcfdc-139">toodo so, paste hello following code snippet in a cell and press **SHIFT + ENTER**.</span></span>

        from pyspark.sql.types import *

    <span data-ttu-id="dcfdc-140">Chaque fois que vous exécutez une tâche dans le bloc-notes, titre de la fenêtre de navigateur web affichera un **(occupé)** état, ainsi que le titre du bloc-notes hello.</span><span class="sxs-lookup"><span data-stu-id="dcfdc-140">Every time you run a job in Jupyter, your web browser window title will show a **(Busy)** status along with hello notebook title.</span></span> <span data-ttu-id="dcfdc-141">Vous verrez également une toohello suivant cercle plein **PySpark** texte dans l’angle supérieur droit de hello.</span><span class="sxs-lookup"><span data-stu-id="dcfdc-141">You will also see a solid circle next toohello **PySpark** text in hello top-right corner.</span></span> <span data-ttu-id="dcfdc-142">Une fois le travail de hello est terminé, cela modifiera le cercle vide de tooa.</span><span class="sxs-lookup"><span data-stu-id="dcfdc-142">After hello job is completed, this will change tooa hollow circle.</span></span>

     <span data-ttu-id="dcfdc-143">![État d’une tâche de bloc-notes Jupyter](./media/hdinsight-apache-spark-use-with-data-lake-store/hdinsight-jupyter-job-status.png "État d’une tâche de bloc-notes Jupyter")</span><span class="sxs-lookup"><span data-stu-id="dcfdc-143">![Status of a Jupyter notebook job](./media/hdinsight-apache-spark-use-with-data-lake-store/hdinsight-jupyter-job-status.png "Status of a Jupyter notebook job")</span></span>

5. <span data-ttu-id="dcfdc-144">Charger des exemples de données dans une table temporaire à l’aide de hello **HVAC.csv** fichier que vous avez copié le compte Data Lake Store de toohello.</span><span class="sxs-lookup"><span data-stu-id="dcfdc-144">Load sample data into a temporary table using hello **HVAC.csv** file you copied toohello Data Lake Store account.</span></span> <span data-ttu-id="dcfdc-145">Vous pouvez accéder aux hello hello Data Lake Store nom du compte hello suivant le modèle d’URL.</span><span class="sxs-lookup"><span data-stu-id="dcfdc-145">You can access hello data in hello Data Lake Store account using hello following URL pattern.</span></span>

    * <span data-ttu-id="dcfdc-146">Si vous avez Data Lake Store en tant que stockage par défaut, HVAC.csv sera à toohello similaire de hello chemin d’accès suivant l’URL :</span><span class="sxs-lookup"><span data-stu-id="dcfdc-146">If you have Data Lake Store as default storage, HVAC.csv will be at hello path similar toohello following URL:</span></span>

            adl://<data_lake_store_name>.azuredatalakestore.net/<cluster_root>/HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv

        <span data-ttu-id="dcfdc-147">Ou bien, vous pouvez également utiliser un format raccourci tel que suivant de hello :</span><span class="sxs-lookup"><span data-stu-id="dcfdc-147">Or, you could also use a shortened format such as hello following:</span></span>

            adl:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv

    * <span data-ttu-id="dcfdc-148">Si vous avez Data Lake Store en tant que stockage supplémentaire, HVAC.csv sera à hello emplacement où vous avez copié, telles que :</span><span class="sxs-lookup"><span data-stu-id="dcfdc-148">If you have Data Lake Store as additional storage, HVAC.csv will be at hello location where you copied it, such as:</span></span>

            adl://<data_lake_store_name>.azuredatalakestore.net/<path_to_file>

     <span data-ttu-id="dcfdc-149">Dans une cellule vide, hello coller suivant l’exemple de code, remplacez **MYDATALAKESTORE** avec votre nom de compte Data Lake Store, puis appuyez sur **MAJ + ENTRÉE**.</span><span class="sxs-lookup"><span data-stu-id="dcfdc-149">In an empty cell, paste hello following code example, replace **MYDATALAKESTORE** with your Data Lake Store account name, and press **SHIFT + ENTER**.</span></span> <span data-ttu-id="dcfdc-150">Cet exemple de code enregistre les données de salutation dans une table temporaire nommée **hvac**.</span><span class="sxs-lookup"><span data-stu-id="dcfdc-150">This code example registers hello data into a temporary table called **hvac**.</span></span>

            # Load hello data. hello path below assumes Data Lake Store is default storage for hello Spark cluster
            hvacText = sc.textFile("adl://MYDATALAKESTORE.azuredatalakestore.net/cluster/mysparkcluster/HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

            # Create hello schema
            hvacSchema = StructType([StructField("date", StringType(), False),StructField("time", StringType(), False),StructField("targettemp", IntegerType(), False),StructField("actualtemp", IntegerType(), False),StructField("buildingID", StringType(), False)])

            # Parse hello data in hvacText
            hvac = hvacText.map(lambda s: s.split(",")).filter(lambda s: s[0] != "Date").map(lambda s:(str(s[0]), str(s[1]), int(s[2]), int(s[3]), str(s[6]) ))

            # Create a data frame
            hvacdf = sqlContext.createDataFrame(hvac,hvacSchema)

            # Register hello data fram as a table toorun queries against
            hvacdf.registerTempTable("hvac")

6. <span data-ttu-id="dcfdc-151">Étant donné que vous utilisez un noyau PySpark, vous pouvez maintenant directement exécuter une requête SQL sur une table temporaire de hello **hvac** que vous venez de créer à l’aide de hello `%%sql` magique.</span><span class="sxs-lookup"><span data-stu-id="dcfdc-151">Because you are using a PySpark kernel, you can now directly run a SQL query on hello temporary table **hvac** that you just created by using hello `%%sql` magic.</span></span> <span data-ttu-id="dcfdc-152">Pour plus d’informations sur hello `%%sql` magic, ainsi que d’autres magics disponibles avec le noyau de PySpark hello, consultez [noyaux disponibles sur les ordinateurs portables de Notebook avec clusters Spark HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span><span class="sxs-lookup"><span data-stu-id="dcfdc-152">For more information about hello `%%sql` magic, as well as other magics available with hello PySpark kernel, see [Kernels available on Jupyter notebooks with Spark HDInsight clusters](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span></span>

        %%sql
        SELECT buildingID, (targettemp - actualtemp) AS temp_diff, date FROM hvac WHERE date = \"6/1/13\"

7. <span data-ttu-id="dcfdc-153">Une fois que hello tâche terminée avec succès, hello suivant sortie tabulaire est affiché par défaut.</span><span class="sxs-lookup"><span data-stu-id="dcfdc-153">Once hello job is completed successfully, hello following tabular output is displayed by default.</span></span>

      <span data-ttu-id="dcfdc-154">![Table de sortie des résultats de la requête](./media/hdinsight-apache-spark-use-with-data-lake-store/jupyter-tabular-output.png "Table de sortie des résultats de la requête")</span><span class="sxs-lookup"><span data-stu-id="dcfdc-154">![Table output of query result](./media/hdinsight-apache-spark-use-with-data-lake-store/jupyter-tabular-output.png "Table output of query result")</span></span>

     <span data-ttu-id="dcfdc-155">Vous pouvez également afficher les résultats de hello dans les autres visualisations.</span><span class="sxs-lookup"><span data-stu-id="dcfdc-155">You can also see hello results in other visualizations as well.</span></span> <span data-ttu-id="dcfdc-156">Par exemple, un graphique en aires pour hello même sortie se présente comme suit de hello.</span><span class="sxs-lookup"><span data-stu-id="dcfdc-156">For example, an area graph for hello same output would look like hello following.</span></span>

     <span data-ttu-id="dcfdc-157">![Graphique en aires des résultats de la requête](./media/hdinsight-apache-spark-use-with-data-lake-store/jupyter-area-output.png "Graphique en aires des résultats de la requête")</span><span class="sxs-lookup"><span data-stu-id="dcfdc-157">![Area graph of query result](./media/hdinsight-apache-spark-use-with-data-lake-store/jupyter-area-output.png "Area graph of query result")</span></span>

8. <span data-ttu-id="dcfdc-158">Une fois que vous avez terminé d’exécuter l’application hello, vous devez le ressources hello toorelease arrêt hello bloc-notes.</span><span class="sxs-lookup"><span data-stu-id="dcfdc-158">After you have finished running hello application, you should shutdown hello notebook toorelease hello resources.</span></span> <span data-ttu-id="dcfdc-159">toodo donc de hello **fichier** cliquez sur le menu d’un ordinateur portable hello, **fermer et s’arrêter**.</span><span class="sxs-lookup"><span data-stu-id="dcfdc-159">toodo so, from hello **File** menu on hello notebook, click **Close and Halt**.</span></span> <span data-ttu-id="dcfdc-160">Cette s’arrête et le bloc-notes de fermer hello.</span><span class="sxs-lookup"><span data-stu-id="dcfdc-160">This will shutdown and close hello notebook.</span></span>


## <a name="next-steps"></a><span data-ttu-id="dcfdc-161">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="dcfdc-161">Next steps</span></span>

* [<span data-ttu-id="dcfdc-162">Créer un toorun d’application de Scala autonome sur un cluster d’Apache Spark</span><span class="sxs-lookup"><span data-stu-id="dcfdc-162">Create a standalone Scala application toorun on Apache Spark cluster</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="dcfdc-163">Utilisez les outils HDInsight dans la boîte à outils Azure pour les applications Spark cluster HDInsight Spark Linux IntelliJ toocreate</span><span class="sxs-lookup"><span data-stu-id="dcfdc-163">Use HDInsight Tools in Azure Toolkit for IntelliJ toocreate Spark applications for HDInsight Spark Linux cluster</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="dcfdc-164">Utilisez les outils HDInsight dans la boîte à outils Azure pour les applications de Spark toocreate Eclipse pour le cluster HDInsight Spark Linux</span><span class="sxs-lookup"><span data-stu-id="dcfdc-164">Use HDInsight Tools in Azure Toolkit for Eclipse toocreate Spark applications for HDInsight Spark Linux cluster</span></span>](hdinsight-apache-spark-eclipse-tool-plugin.md)
