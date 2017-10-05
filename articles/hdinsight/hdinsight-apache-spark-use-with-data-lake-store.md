---
title: "Utiliser Apache Spark pour analyser les données Azure Data Lake Store | Microsoft Docs"
description: "Exécuter des travaux Spark pour analyser des données stockées dans Azure Data Lake Store"
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
ms.openlocfilehash: 66f115c4f348ccaeb8855568ba1ad50faa442173
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="use-hdinsight-spark-cluster-to-analyze-data-in-data-lake-store"></a><span data-ttu-id="1845a-103">Utiliser le cluster HDInsight Spark pour analyser les données dans Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="1845a-103">Use HDInsight Spark cluster to analyze data in Data Lake Store</span></span>

<span data-ttu-id="1845a-104">Dans ce didacticiel, vous utilisez le bloc-notes Jupyter disponible avec les clusters HDInsight Spark pour exécuter un travail qui lit les données à partir d’un compte Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="1845a-104">In this tutorial, you use Jupyter notebook available with HDInsight Spark clusters to run a job that reads data from a Data Lake Store account.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1845a-105">Composants requis</span><span class="sxs-lookup"><span data-stu-id="1845a-105">Prerequisites</span></span>

* <span data-ttu-id="1845a-106">Compte Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="1845a-106">Azure Data Lake Store account.</span></span> <span data-ttu-id="1845a-107">Suivez les instructions de [Prise en main d'Azure Data Lake Store avec le portail Azure](../data-lake-store/data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="1845a-107">Follow the instructions at [Get started with Azure Data Lake Store using the Azure Portal](../data-lake-store/data-lake-store-get-started-portal.md).</span></span>

* <span data-ttu-id="1845a-108">Cluster Azure HDInsight Spark avec Data Lake Store comme système de stockage.</span><span class="sxs-lookup"><span data-stu-id="1845a-108">Azure HDInsight Spark cluster with Data Lake Store as storage.</span></span> <span data-ttu-id="1845a-109">SUivez les instructions énoncées dans la section [Créer un cluster HDInsight avec Data Lake Store à l’aide du portail Azure](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="1845a-109">Follow the instructions at [Create an HDInsight cluster with Data Lake Store using Azure Portal](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span>

    
## <a name="prepare-the-data"></a><span data-ttu-id="1845a-110">Préparation des données</span><span class="sxs-lookup"><span data-stu-id="1845a-110">Prepare the data</span></span>

> [!NOTE]
> <span data-ttu-id="1845a-111">Vous n’avez pas besoin de suivre cette étape si vous avez créé le cluster HDInsight avec Data Lake Store comme stockage par défaut.</span><span class="sxs-lookup"><span data-stu-id="1845a-111">You do not need to perform this step if you have created the HDInsight cluster with Data Lake Store as default storage.</span></span> <span data-ttu-id="1845a-112">Les processus de création de cluster ajoutent quelques exemples de données dans le compte Data Lake Store spécifié durant la création du cluster.</span><span class="sxs-lookup"><span data-stu-id="1845a-112">The cluster creation processes adds some sample data in the Data Lake Store account that you specify while creating the cluster.</span></span> <span data-ttu-id="1845a-113">Passez à la section [Utilisation du cluster Azure HDInsight Spark avec Data Lake Store](#use-an-hdinsight-spark-cluster-with-data-lake-store).</span><span class="sxs-lookup"><span data-stu-id="1845a-113">Skip to the section [Use HDInsight Spark cluster with Data Lake Store](#use-an-hdinsight-spark-cluster-with-data-lake-store).</span></span>
>
>

<span data-ttu-id="1845a-114">Si vous avez créé un cluster HDInsight avec Data Lake Store en tant que stockage supplémentaire et Azure Storage Blob comme stockage par défaut, vous devez dans un premier temps copier quelques exemples de données sur le compte Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="1845a-114">If you created an HDInsight cluster with Data Lake Store as additional storage and Azure Storage Blob as default storage, you should first copy over some sample data to the Data Lake Store account.</span></span> <span data-ttu-id="1845a-115">Vous pouvez utiliser les exemples de données de l’instance Azure Storage Blob associée au cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1845a-115">You can use the sample data from the Azure Storage Blob associated with the HDInsight cluster.</span></span> <span data-ttu-id="1845a-116">Vous pouvez utiliser [l’outil ADLCopy](http://aka.ms/downloadadlcopy) pour cette opération.</span><span class="sxs-lookup"><span data-stu-id="1845a-116">You can use the [ADLCopy tool](http://aka.ms/downloadadlcopy) to do so.</span></span> <span data-ttu-id="1845a-117">Téléchargez et installez l’outil à l’aide du lien.</span><span class="sxs-lookup"><span data-stu-id="1845a-117">Download and install the tool from the link.</span></span>

1. <span data-ttu-id="1845a-118">Ouvrez une invite de commandes et accédez au répertoire où vous avez installé AdlCopy, généralement `%HOMEPATH%\Documents\adlcopy`.</span><span class="sxs-lookup"><span data-stu-id="1845a-118">Open a command prompt and navigate to the directory where AdlCopy is installed, typically `%HOMEPATH%\Documents\adlcopy`.</span></span>

2. <span data-ttu-id="1845a-119">Exécutez la commande suivante pour copier un objet blob spécifique du conteneur source vers Data Lake Store :</span><span class="sxs-lookup"><span data-stu-id="1845a-119">Run the following command to copy a specific blob from the source container to a Data Lake Store:</span></span>

        AdlCopy /source https://<source_account>.blob.core.windows.net/<source_container>/<blob name> /dest swebhdfs://<dest_adls_account>.azuredatalakestore.net/<dest_folder>/ /sourcekey <storage_account_key_for_storage_container>

    <span data-ttu-id="1845a-120">Copiez le fichier d’exemple de données **HVAC.csv** de l’emplacement **/HdiSamples/HdiSamples/SensorSampleData/hvac/** sur le compte Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="1845a-120">Copy the **HVAC.csv** sample data file at **/HdiSamples/HdiSamples/SensorSampleData/hvac/** to the Azure Data Lake Store account.</span></span> <span data-ttu-id="1845a-121">L’extrait de code doit ressembler à ceci :</span><span class="sxs-lookup"><span data-stu-id="1845a-121">The code snippet should look like:</span></span>

        AdlCopy /Source https://mydatastore.blob.core.windows.net/mysparkcluster/HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv /dest swebhdfs://mydatalakestore.azuredatalakestore.net/hvac/ /sourcekey uJUfvD6cEvhfLoBae2yyQf8t9/BpbWZ4XoYj4kAS5Jf40pZaMNf0q6a8yqTxktwVgRED4vPHeh/50iS9atS5LQ==

   > [!WARNING]
   > <span data-ttu-id="1845a-122">Assurez-vous que la casse des noms de fichiers et du chemin est correcte.</span><span class="sxs-lookup"><span data-stu-id="1845a-122">Make sure you the file and path names are in the proper case.</span></span>
   >
   >
3. <span data-ttu-id="1845a-123">Vous êtes invité à entrer les informations d’identification de l’abonnement Azure sous lequel vous disposez d’un compte Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="1845a-123">You will be prompted to enter the credentials for the Azure subscription under which you have your Data Lake Store account.</span></span> <span data-ttu-id="1845a-124">Vous devez voir une sortie similaire à ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="1845a-124">You will see an output similar to the following:</span></span>

        Initializing Copy.
        Copy Started.
        100% data copied.
        Copy Completed. 1 file copied.

    <span data-ttu-id="1845a-125">Le fichier de données (**HVAC.csv**) sera copié dans un dossier **/hvac** du compte Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="1845a-125">The data file (**HVAC.csv**) will be copied under a folder **/hvac** in the Data Lake Store account.</span></span>

## <a name="use-an-hdinsight-spark-cluster-with-data-lake-store"></a><span data-ttu-id="1845a-126">Utiliser un cluster HDInsight Spark avec Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="1845a-126">Use an HDInsight Spark cluster with Data Lake Store</span></span>

1. <span data-ttu-id="1845a-127">Dans le tableau d’accueil du [portail Azure](https://portal.azure.com/), cliquez sur la vignette de votre cluster Spark (si vous l’avez épinglé au tableau d’accueil).</span><span class="sxs-lookup"><span data-stu-id="1845a-127">From the [Azure Portal](https://portal.azure.com/), from the startboard, click the tile for your Spark cluster (if you pinned it to the startboard).</span></span> <span data-ttu-id="1845a-128">Vous pouvez également accéder à votre cluster sous **Parcourir tout** > **Clusters HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="1845a-128">You can also navigate to your cluster under **Browse All** > **HDInsight Clusters**.</span></span>

2. <span data-ttu-id="1845a-129">Dans le panneau du cluster Spark, cliquez sur **Liens rapides**, puis dans le panneau **Tableau de bord du cluster**, cliquez sur **Bloc-notes Jupyter**.</span><span class="sxs-lookup"><span data-stu-id="1845a-129">From the Spark cluster blade, click **Quick Links**, and then from the **Cluster Dashboard** blade, click **Jupyter Notebook**.</span></span> <span data-ttu-id="1845a-130">Si vous y êtes invité, entrez les informations d’identification d’administrateur pour le cluster.</span><span class="sxs-lookup"><span data-stu-id="1845a-130">If prompted, enter the admin credentials for the cluster.</span></span>

   > [!NOTE]
   > <span data-ttu-id="1845a-131">Vous pouvez également atteindre le bloc-notes Jupyter pour votre cluster en ouvrant l'URL suivante dans votre navigateur.</span><span class="sxs-lookup"><span data-stu-id="1845a-131">You may also reach the Jupyter Notebook for your cluster by opening the following URL in your browser.</span></span> <span data-ttu-id="1845a-132">Remplacez **CLUSTERNAME** par le nom de votre cluster.</span><span class="sxs-lookup"><span data-stu-id="1845a-132">Replace **CLUSTERNAME** with the name of your cluster:</span></span>
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >

3. <span data-ttu-id="1845a-133">Créer un nouveau bloc-notes.</span><span class="sxs-lookup"><span data-stu-id="1845a-133">Create a new notebook.</span></span> <span data-ttu-id="1845a-134">Cliquez sur **Nouveau**, puis sur **PySpark**.</span><span class="sxs-lookup"><span data-stu-id="1845a-134">Click **New**, and then click **PySpark**.</span></span>

    <span data-ttu-id="1845a-135">![Créer un bloc-notes Jupyter](./media/hdinsight-apache-spark-use-with-data-lake-store/hdinsight-create-jupyter-notebook.png "Créer un bloc-notes Jupyter")</span><span class="sxs-lookup"><span data-stu-id="1845a-135">![Create a new Jupyter notebook](./media/hdinsight-apache-spark-use-with-data-lake-store/hdinsight-create-jupyter-notebook.png "Create a new Jupyter notebook")</span></span>

4. <span data-ttu-id="1845a-136">Comme vous avez créé un bloc-notes à l’aide du noyau PySpark, il est inutile de créer des contextes explicitement.</span><span class="sxs-lookup"><span data-stu-id="1845a-136">Because you created a notebook using the PySpark kernel, you do not need to create any contexts explicitly.</span></span> <span data-ttu-id="1845a-137">Les contextes Spark et Hive sont automatiquement créés pour vous lorsque vous exécutez la première cellule de code.</span><span class="sxs-lookup"><span data-stu-id="1845a-137">The Spark and Hive contexts will be automatically created for you when you run the first code cell.</span></span> <span data-ttu-id="1845a-138">Vous pouvez commencer par importer les types requis pour ce scénario.</span><span class="sxs-lookup"><span data-stu-id="1845a-138">You can start by importing the types required for this scenario.</span></span> <span data-ttu-id="1845a-139">Pour cela, collez l’extrait de code suivant dans une cellule vide, puis appuyez sur **MAJ + ENTRÉE**.</span><span class="sxs-lookup"><span data-stu-id="1845a-139">To do so, paste the following code snippet in a cell and press **SHIFT + ENTER**.</span></span>

        from pyspark.sql.types import *

    <span data-ttu-id="1845a-140">À chaque exécution d’une tâche dans Jupyter, le titre de la fenêtre du navigateur web affiche l’état **(Occupé)** ainsi que le titre du bloc-notes.</span><span class="sxs-lookup"><span data-stu-id="1845a-140">Every time you run a job in Jupyter, your web browser window title will show a **(Busy)** status along with the notebook title.</span></span> <span data-ttu-id="1845a-141">Un cercle plein s’affiche également en regard du texte **PySpark** dans le coin supérieur droit.</span><span class="sxs-lookup"><span data-stu-id="1845a-141">You will also see a solid circle next to the **PySpark** text in the top-right corner.</span></span> <span data-ttu-id="1845a-142">Une fois le travail terminé, ce cercle est remplacé par un cercle vide.</span><span class="sxs-lookup"><span data-stu-id="1845a-142">After the job is completed, this will change to a hollow circle.</span></span>

     <span data-ttu-id="1845a-143">![État d’une tâche de bloc-notes Jupyter](./media/hdinsight-apache-spark-use-with-data-lake-store/hdinsight-jupyter-job-status.png "État d’une tâche de bloc-notes Jupyter")</span><span class="sxs-lookup"><span data-stu-id="1845a-143">![Status of a Jupyter notebook job](./media/hdinsight-apache-spark-use-with-data-lake-store/hdinsight-jupyter-job-status.png "Status of a Jupyter notebook job")</span></span>

5. <span data-ttu-id="1845a-144">Chargez des exemples de données dans une table temporaire à l’aide du fichier **HVAC.csv** que vous avez copié dans le compte Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="1845a-144">Load sample data into a temporary table using the **HVAC.csv** file you copied to the Data Lake Store account.</span></span> <span data-ttu-id="1845a-145">Vous pouvez accéder aux données du compte Data Lake Store à l’aide du modèle d’URL suivant.</span><span class="sxs-lookup"><span data-stu-id="1845a-145">You can access the data in the Data Lake Store account using the following URL pattern.</span></span>

    * <span data-ttu-id="1845a-146">Si vous disposez de Data Lake Store en tant que stockage par défaut, le fichier HVAC.csv sera sur un chemin d’accès similaire à l’URL suivante :</span><span class="sxs-lookup"><span data-stu-id="1845a-146">If you have Data Lake Store as default storage, HVAC.csv will be at the path similar to the following URL:</span></span>

            adl://<data_lake_store_name>.azuredatalakestore.net/<cluster_root>/HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv

        <span data-ttu-id="1845a-147">Vous pouvez également utiliser un format abrégé comme les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="1845a-147">Or, you could also use a shortened format such as the following:</span></span>

            adl:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv

    * <span data-ttu-id="1845a-148">Si vous disposez de Data Lake Store en tant que stockage supplémentaire, le fichier HVAC.csv sera à l’emplacement où vous l’avez copié, comme :</span><span class="sxs-lookup"><span data-stu-id="1845a-148">If you have Data Lake Store as additional storage, HVAC.csv will be at the location where you copied it, such as:</span></span>

            adl://<data_lake_store_name>.azuredatalakestore.net/<path_to_file>

     <span data-ttu-id="1845a-149">Dans une cellule vide, collez l’exemple de code suivant, remplacez **MYDATALAKESTORE** par votre nom de compte Data Lake Store, puis appuyez sur **Maj+ Entrée**.</span><span class="sxs-lookup"><span data-stu-id="1845a-149">In an empty cell, paste the following code example, replace **MYDATALAKESTORE** with your Data Lake Store account name, and press **SHIFT + ENTER**.</span></span> <span data-ttu-id="1845a-150">Cet exemple de code enregistre les données dans une table temporaire appelée **hvac**.</span><span class="sxs-lookup"><span data-stu-id="1845a-150">This code example registers the data into a temporary table called **hvac**.</span></span>

            # Load the data. The path below assumes Data Lake Store is default storage for the Spark cluster
            hvacText = sc.textFile("adl://MYDATALAKESTORE.azuredatalakestore.net/cluster/mysparkcluster/HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

            # Create the schema
            hvacSchema = StructType([StructField("date", StringType(), False),StructField("time", StringType(), False),StructField("targettemp", IntegerType(), False),StructField("actualtemp", IntegerType(), False),StructField("buildingID", StringType(), False)])

            # Parse the data in hvacText
            hvac = hvacText.map(lambda s: s.split(",")).filter(lambda s: s[0] != "Date").map(lambda s:(str(s[0]), str(s[1]), int(s[2]), int(s[3]), str(s[6]) ))

            # Create a data frame
            hvacdf = sqlContext.createDataFrame(hvac,hvacSchema)

            # Register the data fram as a table to run queries against
            hvacdf.registerTempTable("hvac")

6. <span data-ttu-id="1845a-151">Étant donné que vous utilisez un noyau PySpark, vous pouvez maintenant exécuter directement une requête SQL sur la table temporaire **hvac** que vous venez de créer à l’aide de la méthode magique `%%sql`.</span><span class="sxs-lookup"><span data-stu-id="1845a-151">Because you are using a PySpark kernel, you can now directly run a SQL query on the temporary table **hvac** that you just created by using the `%%sql` magic.</span></span> <span data-ttu-id="1845a-152">Pour plus d’informations sur la méthode magique `%%sql` , ainsi que les autres méthodes magiques disponibles avec le noyau PySpark, consultez [Noyaux disponibles sur les blocs-notes Jupyter avec clusters Spark HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span><span class="sxs-lookup"><span data-stu-id="1845a-152">For more information about the `%%sql` magic, as well as other magics available with the PySpark kernel, see [Kernels available on Jupyter notebooks with Spark HDInsight clusters](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span></span>

        %%sql
        SELECT buildingID, (targettemp - actualtemp) AS temp_diff, date FROM hvac WHERE date = \"6/1/13\"

7. <span data-ttu-id="1845a-153">Une fois le travail terminé, le résultat tabulaire suivant s’affiche par défaut.</span><span class="sxs-lookup"><span data-stu-id="1845a-153">Once the job is completed successfully, the following tabular output is displayed by default.</span></span>

      <span data-ttu-id="1845a-154">![Table de sortie des résultats de la requête](./media/hdinsight-apache-spark-use-with-data-lake-store/jupyter-tabular-output.png "Table de sortie des résultats de la requête")</span><span class="sxs-lookup"><span data-stu-id="1845a-154">![Table output of query result](./media/hdinsight-apache-spark-use-with-data-lake-store/jupyter-tabular-output.png "Table output of query result")</span></span>

     <span data-ttu-id="1845a-155">Vous pouvez également voir les résultats dans d’autres visualisations.</span><span class="sxs-lookup"><span data-stu-id="1845a-155">You can also see the results in other visualizations as well.</span></span> <span data-ttu-id="1845a-156">Par exemple, un graphique en aires pour le même résultat se présenterait comme suit.</span><span class="sxs-lookup"><span data-stu-id="1845a-156">For example, an area graph for the same output would look like the following.</span></span>

     <span data-ttu-id="1845a-157">![Graphique en aires des résultats de la requête](./media/hdinsight-apache-spark-use-with-data-lake-store/jupyter-area-output.png "Graphique en aires des résultats de la requête")</span><span class="sxs-lookup"><span data-stu-id="1845a-157">![Area graph of query result](./media/hdinsight-apache-spark-use-with-data-lake-store/jupyter-area-output.png "Area graph of query result")</span></span>

8. <span data-ttu-id="1845a-158">Une fois l’exécution de l’application terminée, arrêtez le bloc-notes pour libérer les ressources.</span><span class="sxs-lookup"><span data-stu-id="1845a-158">After you have finished running the application, you should shutdown the notebook to release the resources.</span></span> <span data-ttu-id="1845a-159">Pour ce faire, dans le menu **Fichier** du bloc-notes, cliquez sur **Fermer et arrêter**.</span><span class="sxs-lookup"><span data-stu-id="1845a-159">To do so, from the **File** menu on the notebook, click **Close and Halt**.</span></span> <span data-ttu-id="1845a-160">Cette opération permet d’arrêter et de fermer le bloc-notes.</span><span class="sxs-lookup"><span data-stu-id="1845a-160">This will shutdown and close the notebook.</span></span>


## <a name="next-steps"></a><span data-ttu-id="1845a-161">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1845a-161">Next steps</span></span>

* [<span data-ttu-id="1845a-162">Créer une application Scala autonome à exécuter sur le cluster Apache Spark</span><span class="sxs-lookup"><span data-stu-id="1845a-162">Create a standalone Scala application to run on Apache Spark cluster</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="1845a-163">Utiliser HDInsight Tools dans le kit de ressources Azure pour IntelliJ afin de créer des applications Spark pour un cluster Linux HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="1845a-163">Use HDInsight Tools in Azure Toolkit for IntelliJ to create Spark applications for HDInsight Spark Linux cluster</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="1845a-164">Utiliser HDInsight Tools dans le kit de ressources Azure pour Eclipse afin de créer des applications Spark pour un cluster Linux HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="1845a-164">Use HDInsight Tools in Azure Toolkit for Eclipse to create Spark applications for HDInsight Spark Linux cluster</span></span>](hdinsight-apache-spark-eclipse-tool-plugin.md)
