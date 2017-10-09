---
title: "aaaRun des requêtes interactives sur un cluster Azure HDInsight Spark | Documents Microsoft"
description: "Démarrage rapide de HDInsight Spark sur comment toocreate un Apache Spark dans HDInsight de cluster."
keywords: "démarrage rapide spark,spark interactif,requête interactive,hdinsight spark,azure spark"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: nitinme
ms.openlocfilehash: 3864eba50eb3828a9ecb657ded88080e1974585f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="run-interactive-queries-on-an-hdinsight-spark-cluster"></a><span data-ttu-id="e4ef3-104">Exécuter des requêtes interactives sur un cluster HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="e4ef3-104">Run interactive queries on an HDInsight Spark cluster</span></span>

<span data-ttu-id="e4ef3-105">Dans cet article, vous utilisez un notebook bloc-notes toorun interactive Spark des requêtes SQL sur un cluster Spark.</span><span class="sxs-lookup"><span data-stu-id="e4ef3-105">In this article, you use a Jupyter notebook toorun interactive Spark SQL queries against a Spark cluster.</span></span> <span data-ttu-id="e4ef3-106">Bloc-notes jupyter est une application basée sur navigateur qui s’étend hello sur la console d’interactivité toohello Web.</span><span class="sxs-lookup"><span data-stu-id="e4ef3-106">Jupyter notebook is a browser-based application that extends hello console-based interactive experience toohello Web.</span></span> <span data-ttu-id="e4ef3-107">Pour plus d’informations, consultez [bloc-notes jupyter de hello](http://jupyter-notebook.readthedocs.io/en/latest/notebook.html).</span><span class="sxs-lookup"><span data-stu-id="e4ef3-107">For more information, see [hello Jupyter notebook](http://jupyter-notebook.readthedocs.io/en/latest/notebook.html).</span></span>

<span data-ttu-id="e4ef3-108">Pour ce didacticiel, vous utilisez hello **PySpark** noyau dans hello Notebook bloc-notes toorun une requête de Spark SQL interactive.</span><span class="sxs-lookup"><span data-stu-id="e4ef3-108">For this tutorial, you use hello **PySpark** kernel in hello Jupyter notebook toorun an interactive Spark SQL query.</span></span> <span data-ttu-id="e4ef3-109">Les blocs-notes Jupython des clusters HDInsight prennent également en charge deux autres noyaux - **PySpark3** et **Spark**.</span><span class="sxs-lookup"><span data-stu-id="e4ef3-109">Jupyter notebooks on HDInsight clusters also support two other kernels - **PySpark3** and **Spark**.</span></span> <span data-ttu-id="e4ef3-110">Pour plus d’informations sur les noyaux hello et hello les avantages de l’utilisation de **PySpark**, consultez [des clusters de noyaux de bloc-notes utilisez Notebook avec Apache Spark dans HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md).</span><span class="sxs-lookup"><span data-stu-id="e4ef3-110">For more information about hello kernels, and hello benefits of using **PySpark**, see [Use Jupyter notebook kernels with Apache Spark clusters in HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e4ef3-111">Composants requis</span><span class="sxs-lookup"><span data-stu-id="e4ef3-111">Prerequisites</span></span>

* <span data-ttu-id="e4ef3-112">**Un cluster Azure HDInsight Spark**.</span><span class="sxs-lookup"><span data-stu-id="e4ef3-112">**An Azure HDInsight Spark cluster**.</span></span> <span data-ttu-id="e4ef3-113">Pour obtenir des instructions, consultez [Créer un cluster Apache Spark dans Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="e4ef3-113">For instructions, see [Create an Apache Spark cluster in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="create-a-jupyter-notebook-toorun-interactive-queries"></a><span data-ttu-id="e4ef3-114">Créer un bloc-notes jupyter toorun des requêtes interactives</span><span class="sxs-lookup"><span data-stu-id="e4ef3-114">Create a Jupyter notebook toorun interactive queries</span></span>

<span data-ttu-id="e4ef3-115">toorun requêtes, nous utilisons des exemples de données qui est par défaut disponible dans le stockage hello associé hello cluster.</span><span class="sxs-lookup"><span data-stu-id="e4ef3-115">toorun queries, we use sample data that is by default available in hello storage associated with hello cluster.</span></span> <span data-ttu-id="e4ef3-116">Toutefois, vous devez d’abord charger ces données dans Spark comme une trame de données.</span><span class="sxs-lookup"><span data-stu-id="e4ef3-116">However, you must first load that data into Spark as a dataframe.</span></span> <span data-ttu-id="e4ef3-117">Une fois que vous avez hello trame de données, vous pouvez exécuter des requêtes sur ce dernier à l’aide du bloc-notes jupyter de hello.</span><span class="sxs-lookup"><span data-stu-id="e4ef3-117">Once you have hello dataframe, you can run queries on it using hello Jupyter notebook.</span></span> <span data-ttu-id="e4ef3-118">Dans cette section, vous examinez comment :</span><span class="sxs-lookup"><span data-stu-id="e4ef3-118">In this section, you look at how to:</span></span>

* <span data-ttu-id="e4ef3-119">Enregistrer un jeu d’exemple données comme une trame de données Spark.</span><span class="sxs-lookup"><span data-stu-id="e4ef3-119">Register a sample data set as a Spark dataframe.</span></span>
* <span data-ttu-id="e4ef3-120">Exécuter des requêtes sur la trame de données hello.</span><span class="sxs-lookup"><span data-stu-id="e4ef3-120">Run queries on hello dataframe.</span></span>

1. <span data-ttu-id="e4ef3-121">Ouvrez hello [portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="e4ef3-121">Open hello [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="e4ef3-122">Si vous avez choisi de tableau de bord toohello toopin hello cluster, cliquez sur hello en mosaïque de cluster à partir du Panneau de cluster hello du tableau de bord toolaunch hello.</span><span class="sxs-lookup"><span data-stu-id="e4ef3-122">If you opted toopin hello cluster toohello dashboard, click hello cluster tile from hello dashboard toolaunch hello cluster blade.</span></span>

    <span data-ttu-id="e4ef3-123">Si vous ne pas épinglez hello cluster toohello du tableau de bord, à partir du volet de gauche hello, cliquez sur **clusters HDInsight**, puis cliquez sur cluster hello vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="e4ef3-123">If you did not pin hello cluster toohello dashboard, from hello left pane, click **HDInsight clusters**, and then click hello cluster you created.</span></span>

3. <span data-ttu-id="e4ef3-124">À partir de **Liens rapides**, cliquez sur **Tableaux de bord de Cluster**, puis sur **Bloc-notes Jupyter**.</span><span class="sxs-lookup"><span data-stu-id="e4ef3-124">From **Quick links**, click **Cluster dashboards**, and then click **Jupyter Notebook**.</span></span> <span data-ttu-id="e4ef3-125">Si vous y êtes invité, entrez les informations d’identification du admin de hello pour le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="e4ef3-125">If prompted, enter hello admin credentials for hello cluster.</span></span>

   <span data-ttu-id="e4ef3-126">![Ouvrez Notebook bloc-notes toorun interactive Spark requête SQL](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-start-jupyter-interactive-spark-sql-query.png "la requête interactive Spark SQL Notebook ouvrir Bloc-notes toorun")</span><span class="sxs-lookup"><span data-stu-id="e4ef3-126">![Open Jupyter notebook toorun interactive Spark SQL query](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-start-jupyter-interactive-spark-sql-query.png "Open Jupyter notebook toorun interactive Spark SQL query")</span></span>

   > [!NOTE]
   > <span data-ttu-id="e4ef3-127">Vous pouvez également accéder bloc-notes jupyter de hello pour votre cluster en hello ouverture suivante d’URL dans votre navigateur.</span><span class="sxs-lookup"><span data-stu-id="e4ef3-127">You may also access hello Jupyter notebook for your cluster by opening hello following URL in your browser.</span></span> <span data-ttu-id="e4ef3-128">Remplacez **CLUSTERNAME** avec nom hello de votre cluster :</span><span class="sxs-lookup"><span data-stu-id="e4ef3-128">Replace **CLUSTERNAME** with hello name of your cluster:</span></span>
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >
3. <span data-ttu-id="e4ef3-129">Créez un bloc-notes.</span><span class="sxs-lookup"><span data-stu-id="e4ef3-129">Create a notebook.</span></span> <span data-ttu-id="e4ef3-130">Cliquez sur **Nouveau**, puis sur **PySpark**.</span><span class="sxs-lookup"><span data-stu-id="e4ef3-130">Click **New**, and then click **PySpark**.</span></span>

   <span data-ttu-id="e4ef3-131">![Créer une requête de Spark SQL interactive Notebook bloc-notes toorun](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-create-jupyter-interactive-Spark-SQL-query.png "créer une requête de Spark SQL Notebook bloc-notes toorun interactive")</span><span class="sxs-lookup"><span data-stu-id="e4ef3-131">![Create a Jupyter notebook toorun interactive Spark SQL query](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-create-jupyter-interactive-Spark-SQL-query.png "Create a Jupyter notebook toorun interactive Spark SQL query")</span></span>

   <span data-ttu-id="e4ef3-132">Un nouvel ordinateur portable est créé et ouvert avec le nom hello Untitled(Untitled.pynb).</span><span class="sxs-lookup"><span data-stu-id="e4ef3-132">A new notebook is created and opened with hello name Untitled(Untitled.pynb).</span></span>

4. <span data-ttu-id="e4ef3-133">Cliquez sur le nom du bloc-notes hello haut hello et entrez un nom convivial, si vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="e4ef3-133">Click hello notebook name at hello top, and enter a friendly name if you want.</span></span>

    <span data-ttu-id="e4ef3-134">![Fournissez un nom pour hello Jupter bloc-notes toorun Spark requêtes interactif de](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-jupyter-notebook-name.png "fournir un nom pour hello Jupter bloc-notes toorun interactive Spark requête à partir de")</span><span class="sxs-lookup"><span data-stu-id="e4ef3-134">![Provide a name for hello Jupter notebook toorun interactive Spark query from](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-jupyter-notebook-name.png "Provide a name for hello Jupter notebook toorun interactive Spark query from")</span></span>

5. <span data-ttu-id="e4ef3-135">Suit hello de coller le code dans une cellule vide, puis appuyez sur **MAJ + ENTRÉE** code hello de toorun.</span><span class="sxs-lookup"><span data-stu-id="e4ef3-135">Paste hello following code in an empty cell, and then press **SHIFT + ENTER** toorun hello code.</span></span> <span data-ttu-id="e4ef3-136">code de Hello importe des types hello requis pour ce scénario :</span><span class="sxs-lookup"><span data-stu-id="e4ef3-136">hello code imports hello types required for this scenario:</span></span>

        from pyspark.sql.types import *

    <span data-ttu-id="e4ef3-137">Étant donné que vous avez créé un ordinateur portable à l’aide de noyau de PySpark hello, il est inutile toocreate les contextes explicitement.</span><span class="sxs-lookup"><span data-stu-id="e4ef3-137">Because you created a notebook using hello PySpark kernel, you do not need toocreate any contexts explicitly.</span></span> <span data-ttu-id="e4ef3-138">contextes de Spark et Hive Hello sont créées automatiquement pour vous lors de l’exécution de la première cellule de code hello.</span><span class="sxs-lookup"><span data-stu-id="e4ef3-138">hello Spark and Hive contexts are automatically created for you when you run hello first code cell.</span></span>

    <span data-ttu-id="e4ef3-139">![État de la requête interactive Spark SQL](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-interactive-spark-query-status.png "État de la requête interactive Spark SQL")</span><span class="sxs-lookup"><span data-stu-id="e4ef3-139">![Status of interactive Spark SQL query](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-interactive-spark-query-status.png "Status of interactive Spark SQL query")</span></span>

    <span data-ttu-id="e4ef3-140">Chaque fois que vous exécutez une requête interactive dans le bloc-notes, le titre de la fenêtre de navigateur web affiche un **(occupé)** état, ainsi que le titre du bloc-notes hello.</span><span class="sxs-lookup"><span data-stu-id="e4ef3-140">Every time you run an interactive query in Jupyter, your web browser window title shows a **(Busy)** status along with hello notebook title.</span></span> <span data-ttu-id="e4ef3-141">Vous voyez également un toohello suivant cercle plein **PySpark** texte dans l’angle supérieur droit de hello.</span><span class="sxs-lookup"><span data-stu-id="e4ef3-141">You also see a solid circle next toohello **PySpark** text in hello top-right corner.</span></span> <span data-ttu-id="e4ef3-142">Une fois le travail de hello est terminé, il modifie tooa les cercle vide.</span><span class="sxs-lookup"><span data-stu-id="e4ef3-142">After hello job is completed, it changes tooa hollow circle.</span></span>

6. <span data-ttu-id="e4ef3-143">Avant de charger les données de salutation dans un cluster Spark, nous permettent de rechercher un instantané de celui-ci.</span><span class="sxs-lookup"><span data-stu-id="e4ef3-143">Before you load hello data into a Spark cluster, let us look a snapshot of it.</span></span> <span data-ttu-id="e4ef3-144">Hello exemples de données utilisés dans ce didacticiel sont disponibles dans un fichier CSV sur tous les clusters HDInsight Spark à **\HdiSamples\HdiSamples\SensorSampleData\hvac\hvac.csv**.</span><span class="sxs-lookup"><span data-stu-id="e4ef3-144">hello sample data used in this tutorial is available as a CSV file on all HDInsight Spark clusters at **\HdiSamples\HdiSamples\SensorSampleData\hvac\hvac.csv**.</span></span> <span data-ttu-id="e4ef3-145">les données de salutation capture les variations de température hello de bâtiment.</span><span class="sxs-lookup"><span data-stu-id="e4ef3-145">hello data captures hello temperature variations of a building.</span></span> <span data-ttu-id="e4ef3-146">Voici hello premières lignes de données de hello.</span><span class="sxs-lookup"><span data-stu-id="e4ef3-146">Here are hello first few rows of hello data.</span></span>

    <span data-ttu-id="e4ef3-147">![Instantané des données pour les requêtes Spark SQL interactives](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-sample-data-interactive-spark-sql-query.png "instantané des données pour les requêtes Spark SQL interactives")</span><span class="sxs-lookup"><span data-stu-id="e4ef3-147">![Snapshot of data for interactive Spark SQL query](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-sample-data-interactive-spark-sql-query.png "Snapshot of data for interactive Spark SQL query")</span></span>

6. <span data-ttu-id="e4ef3-148">Créer une trame de données et une table temporaire (**hvac**) en exécutant hello suivant de code.</span><span class="sxs-lookup"><span data-stu-id="e4ef3-148">Create a dataframe and a temporary table (**hvac**) by running hello following code.</span></span> <span data-ttu-id="e4ef3-149">Pour ce didacticiel, nous ne créez pas toutes les colonnes hello dans la table temporaire de hello en tant que colonnes comparées toohello dans des données CSV brutes hello.</span><span class="sxs-lookup"><span data-stu-id="e4ef3-149">For this tutorial, we do not create all hello columns in hello temporary table as compared toohello columns in hello raw CSV data.</span></span> 

        # Create an RDD from sample data
        hvacText = sc.textFile("wasbs:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

        # Create a schema for our data
        Entry = Row('Date', 'Time', 'TargetTemp', 'ActualTemp', 'BuildingID')

        # Parse hello data and create a schema
        hvacParts = hvacText.map(lambda s: s.split(',')).filter(lambda s: s[0] != 'Date')
        hvac = hvacParts.map(lambda p: Entry(str(p[0]), str(p[1]), int(p[2]), int(p[3]), int(p[6])))
        
        # Infer hello schema and create a table       
        hvacTable = sqlContext.createDataFrame(hvac)
        hvacTable.registerTempTable('hvactemptable')
        dfw = DataFrameWriter(hvacTable)
        dfw.saveAsTable('hvac')

7. <span data-ttu-id="e4ef3-150">Une fois que la table de hello est créée, exécuter des requêtes interactives sur les données de hello, utilisez hello suivant de code.</span><span class="sxs-lookup"><span data-stu-id="e4ef3-150">Once hello table is created, run interactive query on hello data, use hello following code.</span></span>

        %%sql
        SELECT buildingID, (targettemp - actualtemp) AS temp_diff, date FROM hvac WHERE date = \"6/1/13\"

   <span data-ttu-id="e4ef3-151">Étant donné que vous utilisez un noyau PySpark, vous pouvez maintenant directement exécuter une requête SQL interactive sur une table temporaire de hello **hvac** que vous avez créé à l’aide de hello `%%sql` magique.</span><span class="sxs-lookup"><span data-stu-id="e4ef3-151">Because you are using a PySpark kernel, you can now directly run an interactive SQL query on hello temporary table **hvac** that you created by using hello `%%sql` magic.</span></span> <span data-ttu-id="e4ef3-152">Pour plus d’informations sur hello `%%sql` magique et autres magics disponibles avec le noyau de PySpark hello, consultez [noyaux disponibles sur les ordinateurs portables de Notebook avec clusters Spark HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span><span class="sxs-lookup"><span data-stu-id="e4ef3-152">For more information about hello `%%sql` magic, and other magics available with hello PySpark kernel, see [Kernels available on Jupyter notebooks with Spark HDInsight clusters](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span></span>

   <span data-ttu-id="e4ef3-153">Hello suivant sortie tabulaire est affiché par défaut.</span><span class="sxs-lookup"><span data-stu-id="e4ef3-153">hello following tabular output is displayed by default.</span></span>

     <span data-ttu-id="e4ef3-154">![Sortie sous forme de tableau d’un résultat de requête interactive Spark](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-interactive-spark-query-result.png "Sortie sous forme de tableau d’un résultat de requête interactive Spark")</span><span class="sxs-lookup"><span data-stu-id="e4ef3-154">![Table output of interactive Spark query result](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-interactive-spark-query-result.png "Table output of interactive Spark query result")</span></span>

    <span data-ttu-id="e4ef3-155">Vous pouvez également afficher les résultats de hello dans les autres visualisations.</span><span class="sxs-lookup"><span data-stu-id="e4ef3-155">You can also see hello results in other visualizations as well.</span></span> <span data-ttu-id="e4ef3-156">Par exemple, un graphique en aires pour hello même sortie se présente comme suit de hello.</span><span class="sxs-lookup"><span data-stu-id="e4ef3-156">For example, an area graph for hello same output would look like hello following.</span></span>

    <span data-ttu-id="e4ef3-157">![Résultat de requête interactive Spark sous forme graphique](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-interactive-spark-query-result-area-chart.png "Résultat de requête interactive Spark sous forme graphique")</span><span class="sxs-lookup"><span data-stu-id="e4ef3-157">![Area graph of interactive Spark query result](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-interactive-spark-query-result-area-chart.png "Area graph of interactive Spark query result")</span></span>

9. <span data-ttu-id="e4ef3-158">Arrêt des ressources de cluster hello hello bloc-notes toorelease une fois que vous avez terminé d’exécuter l’application hello.</span><span class="sxs-lookup"><span data-stu-id="e4ef3-158">Shut down hello notebook toorelease hello cluster resources after you have finished running hello application.</span></span> <span data-ttu-id="e4ef3-159">toodo donc de hello **fichier** cliquez sur le menu d’un ordinateur portable hello, **fermer et s’arrêter**.</span><span class="sxs-lookup"><span data-stu-id="e4ef3-159">toodo so, from hello **File** menu on hello notebook, click **Close and Halt**.</span></span>

## <a name="next-step"></a><span data-ttu-id="e4ef3-160">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="e4ef3-160">Next step</span></span>

<span data-ttu-id="e4ef3-161">Dans cet article vous avez appris comment utiliser des requêtes interactives toorun dans Spark à l’aide du bloc-notes jupyter.</span><span class="sxs-lookup"><span data-stu-id="e4ef3-161">In this article you learned how toorun interactive queries in Spark using Jupyter notebook.</span></span> <span data-ttu-id="e4ef3-162">Avance suivant toosee article toohello, comment les données de salutation que vous avez enregistré dans Spark peuvent être extraites dans un outil analytique de BI telles que Power BI et de Tableau.</span><span class="sxs-lookup"><span data-stu-id="e4ef3-162">Advance toohello next article toosee how hello data you registered in Spark can be pulled into a BI analytics tool such as Power BI and Tableau.</span></span> 

> [!div class="nextstepaction"]
>[<span data-ttu-id="e4ef3-163">Spark BI utilisant des outils de visualisation de données avec Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="e4ef3-163">Spark BI using data visualization tools with Azure HDInsight</span></span>](hdinsight-apache-spark-use-bi-tools.md)




