---
title: Utiliser le blocs-notes Zeppelin avec un cluster Apache Spark sur HDInsight | Microsoft Docs
description: "Instructions détaillées sur l’utilisation des blocs-notes Zeppelin avec les clusters Apache Spark sur Azure HDInsight."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: df489d70-7788-4efa-a089-e5e5006421e2
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 7fe5e3ec68e82945b972d2dd44f2cc3b8cf395d1
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="use-zeppelin-notebooks-with-apache-spark-cluster-on-azure-hdinsight"></a><span data-ttu-id="3c418-103">Utiliser des blocs-notes Zeppelin avec un cluster Apache Spark sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="3c418-103">Use Zeppelin notebooks with Apache Spark cluster on Azure HDInsight</span></span>

<span data-ttu-id="3c418-104">Les clusters HDInsight Spark incluent des blocs-notes Zeppelin que vous pouvez utiliser pour exécuter des tâches Spark.</span><span class="sxs-lookup"><span data-stu-id="3c418-104">HDInsight Spark clusters include Zeppelin notebooks that you can use to run Spark jobs.</span></span> <span data-ttu-id="3c418-105">Dans cet article, vous allez apprendre à utiliser le bloc-notes Zeppelin sur un cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="3c418-105">In this article, you learn how to use the Zeppelin notebook on an HDInsight cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="3c418-106">Les blocs-notes Zeppelin sont disponibles uniquement pour Spark 1.6.3 sur HDInsight 3.5 et Spark 2.1.0 sur HDInsight 3.6.</span><span class="sxs-lookup"><span data-stu-id="3c418-106">Zeppelin notebooks are available only for Spark 1.6.3 on HDInsight 3.5 and Spark 2.1.0 on HDInsight 3.6.</span></span>
>

<span data-ttu-id="3c418-107">**Configuration requise :**</span><span class="sxs-lookup"><span data-stu-id="3c418-107">**Prerequisites:**</span></span>

* <span data-ttu-id="3c418-108">Un abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="3c418-108">An Azure subscription.</span></span> <span data-ttu-id="3c418-109">Consultez la page [Obtention d’un essai gratuit d’Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="3c418-109">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="3c418-110">Un cluster Apache Spark sur HDInsight.</span><span class="sxs-lookup"><span data-stu-id="3c418-110">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="3c418-111">Pour obtenir des instructions, consultez [Création de clusters Apache Spark dans Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="3c418-111">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="launch-a-zeppelin-notebook"></a><span data-ttu-id="3c418-112">Lancement d’un bloc-notes Zeppelin</span><span class="sxs-lookup"><span data-stu-id="3c418-112">Launch a Zeppelin notebook</span></span>
1. <span data-ttu-id="3c418-113">Dans le panneau du cluster Spark, cliquez sur **Tableau de bord du cluster**, puis sur **Bloc-notes Zeppelin**.</span><span class="sxs-lookup"><span data-stu-id="3c418-113">From the Spark cluster blade, click **Cluster Dashboard**, and then click **Zeppelin Notebook**.</span></span> <span data-ttu-id="3c418-114">Si vous y êtes invité, entrez les informations d’identification d’administrateur pour le cluster.</span><span class="sxs-lookup"><span data-stu-id="3c418-114">If prompted, enter the admin credentials for the cluster.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="3c418-115">Vous pouvez également atteindre le bloc-notes Zeppelin pour votre cluster en ouvrant l'URL suivante dans votre navigateur.</span><span class="sxs-lookup"><span data-stu-id="3c418-115">You may also reach the Zeppelin Notebook for your cluster by opening the following URL in your browser.</span></span> <span data-ttu-id="3c418-116">Remplacez **CLUSTERNAME** par le nom de votre cluster.</span><span class="sxs-lookup"><span data-stu-id="3c418-116">Replace **CLUSTERNAME** with the name of your cluster:</span></span>
   > 
   > `https://CLUSTERNAME.azurehdinsight.net/zeppelin`
   > 
   > 
2. <span data-ttu-id="3c418-117">Créer un nouveau bloc-notes.</span><span class="sxs-lookup"><span data-stu-id="3c418-117">Create a new notebook.</span></span> <span data-ttu-id="3c418-118">Dans le volet d'en-tête, cliquez sur **Bloc-notes**, puis sur **Créer une note**.</span><span class="sxs-lookup"><span data-stu-id="3c418-118">From the header pane, click **Notebook**, and then click **Create New Note**.</span></span>
   
    <span data-ttu-id="3c418-119">![Créer un nouveau bloc-notes Zeppelin](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-create-zeppelin-notebook.png "Créer un nouveau bloc-notes Zeppelin")</span><span class="sxs-lookup"><span data-stu-id="3c418-119">![Create a new Zeppelin notebook](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-create-zeppelin-notebook.png "Create a new Zeppelin notebook")</span></span>
   
    <span data-ttu-id="3c418-120">Entrez un nom pour le bloc-notes, puis cliquez sur **Créer une note**.</span><span class="sxs-lookup"><span data-stu-id="3c418-120">Enter a name for the notebook, and then click **Create Note**.</span></span>
3. <span data-ttu-id="3c418-121">Vérifiez également que l’en-tête du bloc-notes indique un état connecté.</span><span class="sxs-lookup"><span data-stu-id="3c418-121">Also, make sure the notebook header shows a connected status.</span></span> <span data-ttu-id="3c418-122">Il est indiqué par un point vert dans le coin supérieur droit.</span><span class="sxs-lookup"><span data-stu-id="3c418-122">It is denoted by a green dot in the top-right corner.</span></span>
   
    <span data-ttu-id="3c418-123">![État du bloc-notes Zeppelin](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-connected.png "État du bloc-notes Zeppelin")</span><span class="sxs-lookup"><span data-stu-id="3c418-123">![Zeppelin notebook status](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-connected.png "Zeppelin notebook status")</span></span>
4. <span data-ttu-id="3c418-124">Chargez un exemple de données dans une table temporaire.</span><span class="sxs-lookup"><span data-stu-id="3c418-124">Load sample data into a temporary table.</span></span> <span data-ttu-id="3c418-125">Lorsque vous créez un cluster Spark dans HDInsight, l’exemple de fichier de données **hvac.csv** est copié vers le compte de stockage associé dans **\HdiSamples\SensorSampleData\hvac**.</span><span class="sxs-lookup"><span data-stu-id="3c418-125">When you create a Spark cluster in HDInsight, the sample data file, **hvac.csv**, is copied to the associated storage account under **\HdiSamples\SensorSampleData\hvac**.</span></span>
   
    <span data-ttu-id="3c418-126">Collez l’extrait suivant dans le paragraphe vide créé par défaut dans le nouveau bloc-notes.</span><span class="sxs-lookup"><span data-stu-id="3c418-126">In the empty paragraph that is created by default in the new notebook, paste the following snippet.</span></span>
   
        %livy.spark
        //The above magic instructs Zeppelin to use the Livy Scala interpreter
   
        // Create an RDD using the default Spark context, sc
        val hvacText = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")
   
        // Define a schema
        case class Hvac(date: String, time: String, targettemp: Integer, actualtemp: Integer, buildingID: String)
   
        // Map the values in the .csv file to the schema
        val hvac = hvacText.map(s => s.split(",")).filter(s => s(0) != "Date").map(
            s => Hvac(s(0), 
                    s(1),
                    s(2).toInt,
                    s(3).toInt,
                    s(6)
            )
        ).toDF()
   
        // Register as a temporary table called "hvac"
        hvac.registerTempTable("hvac")
   
    <span data-ttu-id="3c418-127">Appuyez sur **MAJ + ENTRÉE** ou cliquez sur le bouton **Lire** pour que le paragraphe exécute l'extrait de code.</span><span class="sxs-lookup"><span data-stu-id="3c418-127">Press **SHIFT + ENTER** or click the **Play** button for the paragraph to run the snippet.</span></span> <span data-ttu-id="3c418-128">L’état indiqué dans le coin supérieur droit du paragraphe doit progresser de READY, PENDING, RUNNING à FINISHED.</span><span class="sxs-lookup"><span data-stu-id="3c418-128">The status on the right-corner of the paragraph should progress from READY, PENDING, RUNNING to FINISHED.</span></span> <span data-ttu-id="3c418-129">Le résultat s’affiche au bas du même paragraphe.</span><span class="sxs-lookup"><span data-stu-id="3c418-129">The output shows up at the bottom of the same paragraph.</span></span> <span data-ttu-id="3c418-130">La capture d’écran ressemble à ceci :</span><span class="sxs-lookup"><span data-stu-id="3c418-130">The screenshot looks like the following:</span></span>
   
    <span data-ttu-id="3c418-131">![Créer une table temporaire à partir de données brutes](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-load-data.png "Créer une table temporaire à partir de données brutes")</span><span class="sxs-lookup"><span data-stu-id="3c418-131">![Create a temporary table from raw data](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-load-data.png "Create a temporary table from raw data")</span></span>
   
    <span data-ttu-id="3c418-132">Vous pouvez également indiquer un titre pour chaque paragraphe.</span><span class="sxs-lookup"><span data-stu-id="3c418-132">You can also provide a title to each paragraph.</span></span> <span data-ttu-id="3c418-133">Dans le coin droit, cliquez sur l’icône **Settings**, puis sur **Show title**.</span><span class="sxs-lookup"><span data-stu-id="3c418-133">From the right-hand corner, click the **Settings** icon, and then click **Show title**.</span></span>
5. <span data-ttu-id="3c418-134">Vous pouvez maintenant exécuter des instructions Spark SQL dans la table **hvac** .</span><span class="sxs-lookup"><span data-stu-id="3c418-134">You can now run Spark SQL statements on the **hvac** table.</span></span> <span data-ttu-id="3c418-135">Collez la requête suivante dans un nouveau paragraphe.</span><span class="sxs-lookup"><span data-stu-id="3c418-135">Paste the following query in a new paragraph.</span></span> <span data-ttu-id="3c418-136">La requête récupère l’ID de bâtiment et la différence entre les températures cibles et réelles pour chaque bâtiment à une date donnée.</span><span class="sxs-lookup"><span data-stu-id="3c418-136">The query retrieves the building ID and the difference between the target and actual temperatures for each building on a given date.</span></span> <span data-ttu-id="3c418-137">Appuyez sur **MAJ + ENTRÉE**.</span><span class="sxs-lookup"><span data-stu-id="3c418-137">Press **SHIFT + ENTER**.</span></span>
   
        %sql
        select buildingID, (targettemp - actualtemp) as temp_diff, date from hvac where date = "6/1/13" 
   
    <span data-ttu-id="3c418-138">L’instruction **%sql** du début demande au bloc-notes d’utiliser l’interpréteur Livy Scala.</span><span class="sxs-lookup"><span data-stu-id="3c418-138">The **%sql** statement at the beginning tells the notebook to use the Livy Scala interpreter.</span></span>
   
    <span data-ttu-id="3c418-139">La capture d’écran qui suit présente le résultat.</span><span class="sxs-lookup"><span data-stu-id="3c418-139">The following screenshot shows the output.</span></span>
   
    <span data-ttu-id="3c418-140">![Exécuter une instruction Spark SQL à l’aide du bloc-notes](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-spark-query-1.png "Exécuter une instruction Spark SQL à l’aide du bloc-notes")</span><span class="sxs-lookup"><span data-stu-id="3c418-140">![Run a Spark SQL statement using the notebook](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-spark-query-1.png "Run a Spark SQL statement using the notebook")</span></span>
   
     <span data-ttu-id="3c418-141">Cliquez sur les options d’affichage (mis en exergue dans un rectangle) pour basculer entre les différentes représentations du même résultat.</span><span class="sxs-lookup"><span data-stu-id="3c418-141">Click the display options (highlighted in rectangle) to switch between different representations for the same output.</span></span> <span data-ttu-id="3c418-142">Cliquez sur **Paramètres** pour choisir ce qui constitue la clé et les valeurs dans le résultat.</span><span class="sxs-lookup"><span data-stu-id="3c418-142">Click **Settings** to choose what consitutes the key and values in the output.</span></span> <span data-ttu-id="3c418-143">La capture d'écran ci-dessus utilise la clé **buildingID** et la moyenne **temp_diff** comme valeur.</span><span class="sxs-lookup"><span data-stu-id="3c418-143">The screen capture above uses **buildingID** as the key and the average of **temp_diff** as the value.</span></span>
6. <span data-ttu-id="3c418-144">Vous pouvez également exécuter des instructions Spark SQL à l’aide de variables dans la requête.</span><span class="sxs-lookup"><span data-stu-id="3c418-144">You can also run Spark SQL statements using variables in the query.</span></span> <span data-ttu-id="3c418-145">L’extrait suivant montre comment définir la variable **Temp**dans la requête avec les valeurs possibles d’interrogation.</span><span class="sxs-lookup"><span data-stu-id="3c418-145">The next snippet shows how to define a variable, **Temp**, in the query with the possible values you want to query with.</span></span> <span data-ttu-id="3c418-146">Lors de la première exécution de la requête, une liste déroulante est automatiquement renseignée avec les valeurs que vous avez spécifiées pour la variable.</span><span class="sxs-lookup"><span data-stu-id="3c418-146">When you first run the query, a drop-down is automatically populated with the values you specified for the variable.</span></span>
   
        %sql
        select buildingID, date, targettemp, (targettemp - actualtemp) as temp_diff from hvac where targettemp > "${Temp = 65,65|75|85}" 
   
    <span data-ttu-id="3c418-147">Collez cet extrait dans un nouveau paragraphe, puis appuyez sur **MAJ + ENTRÉE**.</span><span class="sxs-lookup"><span data-stu-id="3c418-147">Paste this snippet in a new paragraph and press **SHIFT + ENTER**.</span></span> <span data-ttu-id="3c418-148">La capture d’écran qui suit présente le résultat.</span><span class="sxs-lookup"><span data-stu-id="3c418-148">The following screenshot shows the output.</span></span>
   
    <span data-ttu-id="3c418-149">![Exécuter une instruction Spark SQL à l’aide du bloc-notes](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-spark-query-2.png "Exécuter une instruction Spark SQL à l’aide du bloc-notes")</span><span class="sxs-lookup"><span data-stu-id="3c418-149">![Run a Spark SQL statement using the notebook](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-spark-query-2.png "Run a Spark SQL statement using the notebook")</span></span>
   
    <span data-ttu-id="3c418-150">Pour les requêtes suivantes, vous pouvez sélectionner une nouvelle valeur dans la liste déroulante et réexécuter la requête.</span><span class="sxs-lookup"><span data-stu-id="3c418-150">For subsequent queries, you can select a new value from the drop-down and run the query again.</span></span> <span data-ttu-id="3c418-151">Cliquez sur **Paramètres** pour choisir ce qui constitue la clé et les valeurs dans le résultat.</span><span class="sxs-lookup"><span data-stu-id="3c418-151">Click **Settings** to choose what consitutes the key and values in the output.</span></span> <span data-ttu-id="3c418-152">La capture d'écran ci-dessus utilise la clé **buildingID**, la moyenne **temp_diff** comme valeur, et le groupe **targettemp**.</span><span class="sxs-lookup"><span data-stu-id="3c418-152">The screen capture above uses **buildingID** as the key, the average of **temp_diff** as the value, and **targettemp** as the group.</span></span>
7. <span data-ttu-id="3c418-153">Redémarrez l’interpréteur Livy pour quitter l’application.</span><span class="sxs-lookup"><span data-stu-id="3c418-153">Restart the Livy interpreter to exit the application.</span></span> <span data-ttu-id="3c418-154">Pour ce faire, ouvrez les paramètres de l’interpréteur en cliquant sur le nom d’utilisateur connecté dans le coin supérieur droit, puis cliquez sur **Interpreter** (Interpréteur).</span><span class="sxs-lookup"><span data-stu-id="3c418-154">To do so, open interpreter settings by clicking the logged in user name from the top-right corner, and then click **Interpreter**.</span></span>
   
    <span data-ttu-id="3c418-155">![Lancer l’interpréteur](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Sortie Hive")</span><span class="sxs-lookup"><span data-stu-id="3c418-155">![Launch interpreter](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Hive output")</span></span>
8. <span data-ttu-id="3c418-156">Accédez aux paramètres d’interpréteur Livy, puis cliquez sur **Redémarrer**.</span><span class="sxs-lookup"><span data-stu-id="3c418-156">Scroll to Livy interpreter settings and then click **Restart**.</span></span>
   
    <span data-ttu-id="3c418-157">![Redémarrer l’interpréteur Livy](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-restart-interpreter.png "Redémarrer l’interpréteur Zeppelin")</span><span class="sxs-lookup"><span data-stu-id="3c418-157">![Restart the Livy intepreter](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-restart-interpreter.png "Restart the Zeppelin intepreter")</span></span>

## <a name="how-do-i-use-external-packages-with-the-notebook"></a><span data-ttu-id="3c418-158">Comment utiliser des packages externes avec le bloc-notes ?</span><span class="sxs-lookup"><span data-stu-id="3c418-158">How do I use external packages with the notebook?</span></span>
<span data-ttu-id="3c418-159">Vous pouvez configurer le bloc-notes Zeppelin dans un cluster Apache Spark sur HDInsight (Linux) pour utiliser des packages externes bénéficiant de la contribution de la communauté, qui ne sont pas inclus dans le cluster.</span><span class="sxs-lookup"><span data-stu-id="3c418-159">You can configure the Zeppelin notebook in Apache Spark cluster on HDInsight (Linux) to use external, community-contributed packages that are not included out-of-the-box in the cluster.</span></span> <span data-ttu-id="3c418-160">Vous pouvez rechercher le [référentiel Maven](http://search.maven.org/) pour obtenir la liste complète des packages disponibles.</span><span class="sxs-lookup"><span data-stu-id="3c418-160">You can search the [Maven repository](http://search.maven.org/) for the complete list of packages that are available.</span></span> <span data-ttu-id="3c418-161">Vous pouvez également obtenir une liste des packages disponibles à partir d’autres sources.</span><span class="sxs-lookup"><span data-stu-id="3c418-161">You can also get a list of available packages from other sources.</span></span> <span data-ttu-id="3c418-162">Par exemple, une liste complète des packages bénéficiant de la contribution de la communauté est disponible sur le site [Spark Packages](http://spark-packages.org/)(Packages Spark).</span><span class="sxs-lookup"><span data-stu-id="3c418-162">For example, a complete list of community-contributed packages is available at [Spark Packages](http://spark-packages.org/).</span></span>

<span data-ttu-id="3c418-163">Dans cet article, vous allez apprendre à utiliser le package [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) avec le bloc-notes Jupyter.</span><span class="sxs-lookup"><span data-stu-id="3c418-163">In this article, you will see how to use the [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) package with the Jupyter notebook.</span></span>

1. <span data-ttu-id="3c418-164">Ouvrez les paramètres de l’interpréteur.</span><span class="sxs-lookup"><span data-stu-id="3c418-164">Open interpreter settings.</span></span> <span data-ttu-id="3c418-165">Dans le coin supérieur droit, cliquez sur le nom d’utilisateur connecté, puis cliquez sur **Interpreter** (Interpréteur).</span><span class="sxs-lookup"><span data-stu-id="3c418-165">From the top-right corner, click the logged in user name, and then click **Interpreter**.</span></span>
   
    <span data-ttu-id="3c418-166">![Lancer l’interpréteur](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Sortie Hive")</span><span class="sxs-lookup"><span data-stu-id="3c418-166">![Launch interpreter](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Hive output")</span></span>
2. <span data-ttu-id="3c418-167">Accédez aux paramètres d’interpréteur Livy, puis cliquez sur **Modifier**.</span><span class="sxs-lookup"><span data-stu-id="3c418-167">Scroll to Livy interpreter settings and then click **Edit**.</span></span>
   
    <span data-ttu-id="3c418-168">![Modifier les paramètres de l’interpréteur](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-use-external-package-1.png "Modifier les paramètres de l’interpréteur")</span><span class="sxs-lookup"><span data-stu-id="3c418-168">![Change interpreter settings](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-use-external-package-1.png "Change interpreter settings")</span></span>
3. <span data-ttu-id="3c418-169">Ajoutez une nouvelle clé, appelée **livy.spark.jars.packages** et définissez sa valeur au format `group:id:version`.</span><span class="sxs-lookup"><span data-stu-id="3c418-169">Add a new key, called **livy.spark.jars.packages** and set its value in the format `group:id:version`.</span></span> <span data-ttu-id="3c418-170">Par conséquent, si vous souhaitez utiliser le package [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar), vous devez définir la valeur de la clé sur `com.databricks:spark-csv_2.10:1.4.0`.</span><span class="sxs-lookup"><span data-stu-id="3c418-170">So, if you want to use the [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) package, you must set the value of the key to `com.databricks:spark-csv_2.10:1.4.0`.</span></span>
   
    <span data-ttu-id="3c418-171">![Modifier les paramètres de l’interpréteur](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-use-external-package-2.png "Modifier les paramètres de l’interpréteur")</span><span class="sxs-lookup"><span data-stu-id="3c418-171">![Change interpreter settings](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-use-external-package-2.png "Change interpreter settings")</span></span>
   
    <span data-ttu-id="3c418-172">Cliquez sur **Enregistrer**, puis redémarrez l’interpréteur Livy.</span><span class="sxs-lookup"><span data-stu-id="3c418-172">Click **Save** and then restart the Livy interpreter.</span></span>
4. <span data-ttu-id="3c418-173">**Conseil** : si vous souhaitez savoir comment atteindre la valeur de la clé entrée ci-dessus, lisez ce qui suit.</span><span class="sxs-lookup"><span data-stu-id="3c418-173">**Tip**: If you want to understand how to arrive at the value of the key entered above, here's how.</span></span>
   
    <span data-ttu-id="3c418-174">a.</span><span class="sxs-lookup"><span data-stu-id="3c418-174">a.</span></span> <span data-ttu-id="3c418-175">Recherchez le package dans le référentiel Maven.</span><span class="sxs-lookup"><span data-stu-id="3c418-175">Locate the package in the Maven Repository.</span></span> <span data-ttu-id="3c418-176">Dans ce didacticiel, nous avons utilisé [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar).</span><span class="sxs-lookup"><span data-stu-id="3c418-176">For this tutorial, we used [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar).</span></span>
   
    <span data-ttu-id="3c418-177">b.</span><span class="sxs-lookup"><span data-stu-id="3c418-177">b.</span></span> <span data-ttu-id="3c418-178">À partir du référentiel, rassemblez les valeurs pour **GroupId**, **ArtifactId** et **Version**.</span><span class="sxs-lookup"><span data-stu-id="3c418-178">From the repository, gather the values for **GroupId**, **ArtifactId**, and **Version**.</span></span>
   
    <span data-ttu-id="3c418-179">![Utiliser des packages externes avec le bloc-notes Jupyter](./media/hdinsight-apache-spark-zeppelin-notebook/use-external-packages-with-jupyter.png "Utiliser des packages externes avec le bloc-notes Jupyter")</span><span class="sxs-lookup"><span data-stu-id="3c418-179">![Use external packages with Jupyter notebook](./media/hdinsight-apache-spark-zeppelin-notebook/use-external-packages-with-jupyter.png "Use external packages with Jupyter notebook")</span></span>
   
    <span data-ttu-id="3c418-180">c.</span><span class="sxs-lookup"><span data-stu-id="3c418-180">c.</span></span> <span data-ttu-id="3c418-181">Concaténez les trois valeurs séparées par deux-points (**:**).</span><span class="sxs-lookup"><span data-stu-id="3c418-181">Concatenate the three values, separated by a colon (**:**).</span></span>
   
        com.databricks:spark-csv_2.10:1.4.0

## <a name="where-are-the-zeppelin-notebooks-saved"></a><span data-ttu-id="3c418-182">Où les blocs-notes Zeppelin sont-ils enregistrés ?</span><span class="sxs-lookup"><span data-stu-id="3c418-182">Where are the Zeppelin notebooks saved?</span></span>
<span data-ttu-id="3c418-183">Les blocs-notes Zeppelin sont enregistrés dans les nœuds principaux du cluster.</span><span class="sxs-lookup"><span data-stu-id="3c418-183">The Zeppelin notebooks are saved to the cluster headnodes.</span></span> <span data-ttu-id="3c418-184">Par conséquent, si vous supprimez le cluster, les blocs-notes seront aussi supprimés.</span><span class="sxs-lookup"><span data-stu-id="3c418-184">So, if you delete the cluster, the notebooks will be deleted as well.</span></span> <span data-ttu-id="3c418-185">Si vous souhaitez conserver vos blocs-notes pour une utilisation ultérieure sur les autres clusters, vous devez les exporter après avoir terminé l’exécution des tâches.</span><span class="sxs-lookup"><span data-stu-id="3c418-185">If you want to preserve your notebooks for later use on other clusters, you must export them after you have finished running the jobs.</span></span> <span data-ttu-id="3c418-186">Pour exporter un bloc-notes, cliquez sur l’icône **Exporter** comme illustré dans l’image ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="3c418-186">To export a notebook, click the **Export** icon as shown in the image below.</span></span>

<span data-ttu-id="3c418-187">![Télécharger le bloc-notes](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-download-notebook.png "Télécharger le bloc-notes")</span><span class="sxs-lookup"><span data-stu-id="3c418-187">![Download notebook](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-download-notebook.png "Download the notebook")</span></span>

<span data-ttu-id="3c418-188">Cela permet d’enregistrer le bloc-notes en tant que fichier JSON dans l’emplacement de téléchargement.</span><span class="sxs-lookup"><span data-stu-id="3c418-188">This saves the notebook as a JSON file in your download location.</span></span>

## <a name="livy-session-management"></a><span data-ttu-id="3c418-189">Gestion des sessions Livy</span><span class="sxs-lookup"><span data-stu-id="3c418-189">Livy session management</span></span>
<span data-ttu-id="3c418-190">Lorsque vous exécutez le premier paragraphe de code dans votre bloc-notes Zeppelin, une nouvelle session Livy est créée dans votre cluster HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="3c418-190">When you run the first code paragraph in your Zeppelin notebook, a new Livy session is created in your HDInsight Spark cluster.</span></span> <span data-ttu-id="3c418-191">Cette session est partagée par tous les blocs-notes Zeppelin que vous créerez par la suite.</span><span class="sxs-lookup"><span data-stu-id="3c418-191">This session is shared across all Zeppelin notebooks that you subsequently create.</span></span> <span data-ttu-id="3c418-192">Si, pour une raison quelconque, la session Livy est arrêtée (redémarrage de cluster, etc.), vous ne serez pas en mesure d’exécuter de tâches à partir du bloc-notes Zeppelin.</span><span class="sxs-lookup"><span data-stu-id="3c418-192">If for some reason the Livy session is killed (cluster reboot, etc.), you will not be able to run jobs from the Zeppelin notebook.</span></span>

<span data-ttu-id="3c418-193">Dans ce cas, vous devez effectuer les étapes suivantes avant de commencer à exécuter des tâches à partir d’un bloc-notes Zeppelin.</span><span class="sxs-lookup"><span data-stu-id="3c418-193">In such a case, you must perform the following steps before you can start running jobs from a Zeppelin notebook.</span></span> 

1. <span data-ttu-id="3c418-194">Redémarrez l’interpréteur Livy à partir du bloc-notes Zeppelin.</span><span class="sxs-lookup"><span data-stu-id="3c418-194">Restart the Livy interpreter from the Zeppelin notebook.</span></span> <span data-ttu-id="3c418-195">Pour ce faire, ouvrez les paramètres de l’interpréteur en cliquant sur le nom d’utilisateur connecté dans le coin supérieur droit, puis cliquez sur **Interpreter** (Interpréteur).</span><span class="sxs-lookup"><span data-stu-id="3c418-195">To do so, open interpreter settings by clicking the logged in user name from the top-right corner, and then click **Interpreter**.</span></span>
   
    <span data-ttu-id="3c418-196">![Lancer l’interpréteur](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Sortie Hive")</span><span class="sxs-lookup"><span data-stu-id="3c418-196">![Launch interpreter](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Hive output")</span></span>
2. <span data-ttu-id="3c418-197">Accédez aux paramètres d’interpréteur Livy, puis cliquez sur **Redémarrer**.</span><span class="sxs-lookup"><span data-stu-id="3c418-197">Scroll to Livy interpreter settings and then click **Restart**.</span></span>
   
    <span data-ttu-id="3c418-198">![Redémarrer l’interpréteur Livy](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-restart-interpreter.png "Redémarrer l’interpréteur Zeppelin")</span><span class="sxs-lookup"><span data-stu-id="3c418-198">![Restart the Livy intepreter](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-restart-interpreter.png "Restart the Zeppelin intepreter")</span></span>
3. <span data-ttu-id="3c418-199">Exécutez une cellule de code à partir d’un bloc-notes Zeppelin existant.</span><span class="sxs-lookup"><span data-stu-id="3c418-199">Run a code cell from an existing Zeppelin notebook.</span></span> <span data-ttu-id="3c418-200">Cela crée une session Livy dans le cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="3c418-200">This creates a new Livy session in the HDInsight cluster.</span></span>

## <span data-ttu-id="3c418-201"><a name="seealso"></a>Voir aussi</span><span class="sxs-lookup"><span data-stu-id="3c418-201"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="3c418-202">Vue d’ensemble : Apache Spark sur Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="3c418-202">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="3c418-203">Scénarios</span><span class="sxs-lookup"><span data-stu-id="3c418-203">Scenarios</span></span>
* [<span data-ttu-id="3c418-204">Spark avec BI : effectuez une analyse interactive des données à l’aide de Spark dans HDInsight avec des outils BI</span><span class="sxs-lookup"><span data-stu-id="3c418-204">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="3c418-205">Spark avec Machine Learning : Utiliser Spark dans HDInsight pour l’analyse de la température de bâtiments à l’aide de données HVAC</span><span class="sxs-lookup"><span data-stu-id="3c418-205">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="3c418-206">Spark avec Machine Learning : Utiliser Spark dans HDInsight pour prédire les résultats de l’inspection des aliments</span><span class="sxs-lookup"><span data-stu-id="3c418-206">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="3c418-207">Streaming Spark : Utiliser Spark dans HDInsight pour créer des applications de diffusion en continu en temps réel</span><span class="sxs-lookup"><span data-stu-id="3c418-207">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="3c418-208">Analyse des journaux de site web à l’aide de Spark dans HDInsight</span><span class="sxs-lookup"><span data-stu-id="3c418-208">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="3c418-209">Créer et exécuter des applications</span><span class="sxs-lookup"><span data-stu-id="3c418-209">Create and run applications</span></span>
* [<span data-ttu-id="3c418-210">Créer une application autonome avec Scala</span><span class="sxs-lookup"><span data-stu-id="3c418-210">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="3c418-211">Exécuter des tâches à distance avec Livy sur un cluster Spark</span><span class="sxs-lookup"><span data-stu-id="3c418-211">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="3c418-212">Outils et extensions</span><span class="sxs-lookup"><span data-stu-id="3c418-212">Tools and extensions</span></span>
* [<span data-ttu-id="3c418-213">Utilisez le plugin d’outils HDInsight pour IntelliJ IDEA pour créer et soumettre des applications Spark Scala</span><span class="sxs-lookup"><span data-stu-id="3c418-213">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applicatons</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="3c418-214">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely (Utiliser le plug-in Outils HDInsight pour IntelliJ IDEA pour déboguer des applications Spark à distance)</span><span class="sxs-lookup"><span data-stu-id="3c418-214">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="3c418-215">Noyaux disponibles pour le bloc-notes Jupyter dans un cluster Spark pour HDInsight</span><span class="sxs-lookup"><span data-stu-id="3c418-215">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="3c418-216">Utiliser des packages externes avec les blocs-notes Jupyter</span><span class="sxs-lookup"><span data-stu-id="3c418-216">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="3c418-217">Install Jupyter on your computer and connect to an HDInsight Spark cluster (Installer Jupyter sur un ordinateur et se connecter au cluster Spark sur HDInsight)</span><span class="sxs-lookup"><span data-stu-id="3c418-217">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="3c418-218">Gestion des ressources</span><span class="sxs-lookup"><span data-stu-id="3c418-218">Manage resources</span></span>
* [<span data-ttu-id="3c418-219">Gérer les ressources du cluster Apache Spark dans Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="3c418-219">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="3c418-220">Suivi et débogage des tâches en cours d’exécution sur un cluster Apache Spark dans HDInsight</span><span class="sxs-lookup"><span data-stu-id="3c418-220">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md 







