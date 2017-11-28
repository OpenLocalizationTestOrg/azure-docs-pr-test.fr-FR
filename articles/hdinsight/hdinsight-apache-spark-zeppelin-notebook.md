---
title: cluster de blocs-notes de Zeppelin aaaUse avec Apache Spark sur Azure HDInsight | Documents Microsoft
description: "Obtenir des instructions détaillées sur comment les clusters blocs-notes de Zeppelin toouse avec Apache Spark sur Azure HDInsight."
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
ms.openlocfilehash: 3ab479cfccc7fd38a9bf6a9fb4f5928beec8ff7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-zeppelin-notebooks-with-apache-spark-cluster-on-azure-hdinsight"></a><span data-ttu-id="83cc7-103">Utiliser des blocs-notes Zeppelin avec un cluster Apache Spark sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="83cc7-103">Use Zeppelin notebooks with Apache Spark cluster on Azure HDInsight</span></span>

<span data-ttu-id="83cc7-104">Les clusters HDInsight Spark incluent les blocs-notes Zeppelin que vous pouvez utiliser les travaux de Spark toorun.</span><span class="sxs-lookup"><span data-stu-id="83cc7-104">HDInsight Spark clusters include Zeppelin notebooks that you can use toorun Spark jobs.</span></span> <span data-ttu-id="83cc7-105">Dans cet article, vous découvrez comment toouse hello bloc-notes Zeppelin sur un cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="83cc7-105">In this article, you learn how toouse hello Zeppelin notebook on an HDInsight cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="83cc7-106">Les blocs-notes Zeppelin sont disponibles uniquement pour Spark 1.6.3 sur HDInsight 3.5 et Spark 2.1.0 sur HDInsight 3.6.</span><span class="sxs-lookup"><span data-stu-id="83cc7-106">Zeppelin notebooks are available only for Spark 1.6.3 on HDInsight 3.5 and Spark 2.1.0 on HDInsight 3.6.</span></span>
>

<span data-ttu-id="83cc7-107">**Configuration requise :**</span><span class="sxs-lookup"><span data-stu-id="83cc7-107">**Prerequisites:**</span></span>

* <span data-ttu-id="83cc7-108">Un abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="83cc7-108">An Azure subscription.</span></span> <span data-ttu-id="83cc7-109">Consultez la page [Obtention d’un essai gratuit d’Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="83cc7-109">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="83cc7-110">Un cluster Apache Spark sur HDInsight.</span><span class="sxs-lookup"><span data-stu-id="83cc7-110">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="83cc7-111">Pour obtenir des instructions, consultez [Création de clusters Apache Spark dans Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="83cc7-111">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="launch-a-zeppelin-notebook"></a><span data-ttu-id="83cc7-112">Lancement d’un bloc-notes Zeppelin</span><span class="sxs-lookup"><span data-stu-id="83cc7-112">Launch a Zeppelin notebook</span></span>
1. <span data-ttu-id="83cc7-113">Dans le panneau de cluster Spark hello, cliquez sur **tableau de bord de Cluster**, puis cliquez sur **Zeppelin bloc-notes**.</span><span class="sxs-lookup"><span data-stu-id="83cc7-113">From hello Spark cluster blade, click **Cluster Dashboard**, and then click **Zeppelin Notebook**.</span></span> <span data-ttu-id="83cc7-114">Si vous y êtes invité, entrez les informations d’identification du admin de hello pour le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="83cc7-114">If prompted, enter hello admin credentials for hello cluster.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="83cc7-115">Vous pouvez également atteindre hello Zeppelin bloc-notes pour votre cluster en hello ouverture suivante d’URL dans votre navigateur.</span><span class="sxs-lookup"><span data-stu-id="83cc7-115">You may also reach hello Zeppelin Notebook for your cluster by opening hello following URL in your browser.</span></span> <span data-ttu-id="83cc7-116">Remplacez **CLUSTERNAME** avec nom hello de votre cluster :</span><span class="sxs-lookup"><span data-stu-id="83cc7-116">Replace **CLUSTERNAME** with hello name of your cluster:</span></span>
   > 
   > `https://CLUSTERNAME.azurehdinsight.net/zeppelin`
   > 
   > 
2. <span data-ttu-id="83cc7-117">Créer un nouveau bloc-notes.</span><span class="sxs-lookup"><span data-stu-id="83cc7-117">Create a new notebook.</span></span> <span data-ttu-id="83cc7-118">Dans le volet d’en-tête hello, cliquez sur **bloc-notes**, puis cliquez sur **créer une Note**.</span><span class="sxs-lookup"><span data-stu-id="83cc7-118">From hello header pane, click **Notebook**, and then click **Create New Note**.</span></span>
   
    <span data-ttu-id="83cc7-119">![Créer un nouveau bloc-notes Zeppelin](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-create-zeppelin-notebook.png "Créer un nouveau bloc-notes Zeppelin")</span><span class="sxs-lookup"><span data-stu-id="83cc7-119">![Create a new Zeppelin notebook](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-create-zeppelin-notebook.png "Create a new Zeppelin notebook")</span></span>
   
    <span data-ttu-id="83cc7-120">Entrez un nom pour l’ordinateur portable de hello, puis cliquez sur **créer une Note**.</span><span class="sxs-lookup"><span data-stu-id="83cc7-120">Enter a name for hello notebook, and then click **Create Note**.</span></span>
3. <span data-ttu-id="83cc7-121">Assurez-vous également que les en-tête de bloc-notes hello présente l’état connecté.</span><span class="sxs-lookup"><span data-stu-id="83cc7-121">Also, make sure hello notebook header shows a connected status.</span></span> <span data-ttu-id="83cc7-122">Il est indiqué par un point vert dans le coin supérieur droit de hello.</span><span class="sxs-lookup"><span data-stu-id="83cc7-122">It is denoted by a green dot in hello top-right corner.</span></span>
   
    <span data-ttu-id="83cc7-123">![État du bloc-notes Zeppelin](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-connected.png "État du bloc-notes Zeppelin")</span><span class="sxs-lookup"><span data-stu-id="83cc7-123">![Zeppelin notebook status](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-connected.png "Zeppelin notebook status")</span></span>
4. <span data-ttu-id="83cc7-124">Chargez un exemple de données dans une table temporaire.</span><span class="sxs-lookup"><span data-stu-id="83cc7-124">Load sample data into a temporary table.</span></span> <span data-ttu-id="83cc7-125">Lorsque vous créez un cluster Spark dans HDInsight, le fichier de données d’exemple hello, **hvac.csv**, est le compte de stockage toohello copié associée sous **\HdiSamples\SensorSampleData\hvac**.</span><span class="sxs-lookup"><span data-stu-id="83cc7-125">When you create a Spark cluster in HDInsight, hello sample data file, **hvac.csv**, is copied toohello associated storage account under **\HdiSamples\SensorSampleData\hvac**.</span></span>
   
    <span data-ttu-id="83cc7-126">Dans hello paragraphe vide qui est créé par défaut dans le bloc-notes hello, collez hello suivant extrait de code.</span><span class="sxs-lookup"><span data-stu-id="83cc7-126">In hello empty paragraph that is created by default in hello new notebook, paste hello following snippet.</span></span>
   
        %livy.spark
        //hello above magic instructs Zeppelin toouse hello Livy Scala interpreter
   
        // Create an RDD using hello default Spark context, sc
        val hvacText = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")
   
        // Define a schema
        case class Hvac(date: String, time: String, targettemp: Integer, actualtemp: Integer, buildingID: String)
   
        // Map hello values in hello .csv file toohello schema
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
   
    <span data-ttu-id="83cc7-127">Appuyez sur **MAJ + ENTRÉE** ou cliquez sur hello **lire** bouton pour l’extrait de code hello paragraphe toorun hello.</span><span class="sxs-lookup"><span data-stu-id="83cc7-127">Press **SHIFT + ENTER** or click hello **Play** button for hello paragraph toorun hello snippet.</span></span> <span data-ttu-id="83cc7-128">état Hello sur la droite hello du paragraphe de hello doit progression prêt, en attente, en cours d’exécution tooFINISHED.</span><span class="sxs-lookup"><span data-stu-id="83cc7-128">hello status on hello right-corner of hello paragraph should progress from READY, PENDING, RUNNING tooFINISHED.</span></span> <span data-ttu-id="83cc7-129">sortie de Hello s’affiche en bas de hello Hello même paragraph.</span><span class="sxs-lookup"><span data-stu-id="83cc7-129">hello output shows up at hello bottom of hello same paragraph.</span></span> <span data-ttu-id="83cc7-130">capture d’écran de Hello ressemble à hello suivantes :</span><span class="sxs-lookup"><span data-stu-id="83cc7-130">hello screenshot looks like hello following:</span></span>
   
    <span data-ttu-id="83cc7-131">![Créer une table temporaire à partir de données brutes](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-load-data.png "Créer une table temporaire à partir de données brutes")</span><span class="sxs-lookup"><span data-stu-id="83cc7-131">![Create a temporary table from raw data](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-load-data.png "Create a temporary table from raw data")</span></span>
   
    <span data-ttu-id="83cc7-132">Vous pouvez également fournir un paragraphe tooeach de titre.</span><span class="sxs-lookup"><span data-stu-id="83cc7-132">You can also provide a title tooeach paragraph.</span></span> <span data-ttu-id="83cc7-133">À partir de l’angle supérieur droit de hello, cliquez sur hello **paramètres** icône, puis cliquez sur **afficher le titre**.</span><span class="sxs-lookup"><span data-stu-id="83cc7-133">From hello right-hand corner, click hello **Settings** icon, and then click **Show title**.</span></span>
5. <span data-ttu-id="83cc7-134">Vous pouvez désormais exécuter des instructions SQL de Spark sur hello **hvac** table.</span><span class="sxs-lookup"><span data-stu-id="83cc7-134">You can now run Spark SQL statements on hello **hvac** table.</span></span> <span data-ttu-id="83cc7-135">Collez hello suivant la requête dans un nouveau paragraphe.</span><span class="sxs-lookup"><span data-stu-id="83cc7-135">Paste hello following query in a new paragraph.</span></span> <span data-ttu-id="83cc7-136">requête de Hello récupère les ID de génération hello et différence hello entre la cible de hello et températures réels pour chaque génération sur une date donnée.</span><span class="sxs-lookup"><span data-stu-id="83cc7-136">hello query retrieves hello building ID and hello difference between hello target and actual temperatures for each building on a given date.</span></span> <span data-ttu-id="83cc7-137">Appuyez sur **MAJ + ENTRÉE**.</span><span class="sxs-lookup"><span data-stu-id="83cc7-137">Press **SHIFT + ENTER**.</span></span>
   
        %sql
        select buildingID, (targettemp - actualtemp) as temp_diff, date from hvac where date = "6/1/13" 
   
    <span data-ttu-id="83cc7-138">Hello **% sql** instruction au début de hello indique à l’interpréteur de Livy Scala hello bloc-notes toouse hello.</span><span class="sxs-lookup"><span data-stu-id="83cc7-138">hello **%sql** statement at hello beginning tells hello notebook toouse hello Livy Scala interpreter.</span></span>
   
    <span data-ttu-id="83cc7-139">Hello capture d’écran suivante montre la sortie de hello.</span><span class="sxs-lookup"><span data-stu-id="83cc7-139">hello following screenshot shows hello output.</span></span>
   
    <span data-ttu-id="83cc7-140">![Exécuter une instruction Spark SQL à l’aide du bloc-notes de hello](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-spark-query-1.png "exécuter une instruction Spark SQL à l’aide du bloc-notes de hello")</span><span class="sxs-lookup"><span data-stu-id="83cc7-140">![Run a Spark SQL statement using hello notebook](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-spark-query-1.png "Run a Spark SQL statement using hello notebook")</span></span>
   
     <span data-ttu-id="83cc7-141">Cliquez sur hello affichage options (rectangle surligné en) tooswitch entre différentes représentations pour hello même sortie.</span><span class="sxs-lookup"><span data-stu-id="83cc7-141">Click hello display options (highlighted in rectangle) tooswitch between different representations for hello same output.</span></span> <span data-ttu-id="83cc7-142">Cliquez sur **paramètres** toochoose quel constitue hello clé et les valeurs de sortie de hello.</span><span class="sxs-lookup"><span data-stu-id="83cc7-142">Click **Settings** toochoose what consitutes hello key and values in hello output.</span></span> <span data-ttu-id="83cc7-143">capture d’écran ci-dessus utilise de Hello **buildingID** en tant que clé de hello et moyenne hello de **temp_diff** en tant que valeur de hello.</span><span class="sxs-lookup"><span data-stu-id="83cc7-143">hello screen capture above uses **buildingID** as hello key and hello average of **temp_diff** as hello value.</span></span>
6. <span data-ttu-id="83cc7-144">Vous pouvez également exécuter des instructions de Spark SQL à l’aide de variables de requête de hello.</span><span class="sxs-lookup"><span data-stu-id="83cc7-144">You can also run Spark SQL statements using variables in hello query.</span></span> <span data-ttu-id="83cc7-145">Hello suivante extrait de code montre comment toodefine une variable, **Temp**, dans la requête de hello avec les valeurs possibles de hello souhaité tooquery avec.</span><span class="sxs-lookup"><span data-stu-id="83cc7-145">hello next snippet shows how toodefine a variable, **Temp**, in hello query with hello possible values you want tooquery with.</span></span> <span data-ttu-id="83cc7-146">Lors de la première exécution de requête de hello, une liste déroulante est automatiquement remplie avec les valeurs hello que vous avez spécifié pour la variable de hello.</span><span class="sxs-lookup"><span data-stu-id="83cc7-146">When you first run hello query, a drop-down is automatically populated with hello values you specified for hello variable.</span></span>
   
        %sql
        select buildingID, date, targettemp, (targettemp - actualtemp) as temp_diff from hvac where targettemp > "${Temp = 65,65|75|85}" 
   
    <span data-ttu-id="83cc7-147">Collez cet extrait dans un nouveau paragraphe, puis appuyez sur **MAJ + ENTRÉE**.</span><span class="sxs-lookup"><span data-stu-id="83cc7-147">Paste this snippet in a new paragraph and press **SHIFT + ENTER**.</span></span> <span data-ttu-id="83cc7-148">Hello capture d’écran suivante montre la sortie de hello.</span><span class="sxs-lookup"><span data-stu-id="83cc7-148">hello following screenshot shows hello output.</span></span>
   
    <span data-ttu-id="83cc7-149">![Exécuter une instruction Spark SQL à l’aide du bloc-notes de hello](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-spark-query-2.png "exécuter une instruction Spark SQL à l’aide du bloc-notes de hello")</span><span class="sxs-lookup"><span data-stu-id="83cc7-149">![Run a Spark SQL statement using hello notebook](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-spark-query-2.png "Run a Spark SQL statement using hello notebook")</span></span>
   
    <span data-ttu-id="83cc7-150">Pour les requêtes suivantes, vous pouvez sélectionner une nouvelle valeur à partir de déroulante hello et réexécutez la requête de hello.</span><span class="sxs-lookup"><span data-stu-id="83cc7-150">For subsequent queries, you can select a new value from hello drop-down and run hello query again.</span></span> <span data-ttu-id="83cc7-151">Cliquez sur **paramètres** toochoose quel constitue hello clé et les valeurs de sortie de hello.</span><span class="sxs-lookup"><span data-stu-id="83cc7-151">Click **Settings** toochoose what consitutes hello key and values in hello output.</span></span> <span data-ttu-id="83cc7-152">Hello capture d’écran ci-dessus utilise **buildingID** en tant que clé de hello, hello moyenne de **temp_diff** en tant que valeur hello et **targettemp** en tant que groupe de hello.</span><span class="sxs-lookup"><span data-stu-id="83cc7-152">hello screen capture above uses **buildingID** as hello key, hello average of **temp_diff** as hello value, and **targettemp** as hello group.</span></span>
7. <span data-ttu-id="83cc7-153">Redémarrez hello application hello de Livy interpréteur tooexit.</span><span class="sxs-lookup"><span data-stu-id="83cc7-153">Restart hello Livy interpreter tooexit hello application.</span></span> <span data-ttu-id="83cc7-154">toodo, ouvrez Paramètres de l’interpréteur en cliquant sur hello consigné dans le nom d’utilisateur à partir de l’angle supérieur droit de hello, puis cliquez sur **interpréteur**.</span><span class="sxs-lookup"><span data-stu-id="83cc7-154">toodo so, open interpreter settings by clicking hello logged in user name from hello top-right corner, and then click **Interpreter**.</span></span>
   
    <span data-ttu-id="83cc7-155">![Lancer l’interpréteur](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Sortie Hive")</span><span class="sxs-lookup"><span data-stu-id="83cc7-155">![Launch interpreter](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Hive output")</span></span>
8. <span data-ttu-id="83cc7-156">Faites défiler les paramètres d’interpréteur tooLivy, puis cliquez sur **redémarrer**.</span><span class="sxs-lookup"><span data-stu-id="83cc7-156">Scroll tooLivy interpreter settings and then click **Restart**.</span></span>
   
    <span data-ttu-id="83cc7-157">![Redémarrez hello Livy intepreter](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-restart-interpreter.png "redémarrer hello Zeppelin intepreter")</span><span class="sxs-lookup"><span data-stu-id="83cc7-157">![Restart hello Livy intepreter](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-restart-interpreter.png "Restart hello Zeppelin intepreter")</span></span>

## <a name="how-do-i-use-external-packages-with-hello-notebook"></a><span data-ttu-id="83cc7-158">Utilisation des packages externes avec l’ordinateur portable de hello</span><span class="sxs-lookup"><span data-stu-id="83cc7-158">How do I use external packages with hello notebook?</span></span>
<span data-ttu-id="83cc7-159">Vous pouvez configurer le bloc-notes de Zeppelin hello cluster Apache Spark sur HDInsight (Linux) toouse externe conçu par la Communauté de packages, qui ne sont pas inclus out-of-the-box dans un cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="83cc7-159">You can configure hello Zeppelin notebook in Apache Spark cluster on HDInsight (Linux) toouse external, community-contributed packages that are not included out-of-the-box in hello cluster.</span></span> <span data-ttu-id="83cc7-160">Vous pouvez rechercher hello [référentiel de Maven](http://search.maven.org/) pour la liste complète des packages disponibles hello.</span><span class="sxs-lookup"><span data-stu-id="83cc7-160">You can search hello [Maven repository](http://search.maven.org/) for hello complete list of packages that are available.</span></span> <span data-ttu-id="83cc7-161">Vous pouvez également obtenir une liste des packages disponibles à partir d’autres sources.</span><span class="sxs-lookup"><span data-stu-id="83cc7-161">You can also get a list of available packages from other sources.</span></span> <span data-ttu-id="83cc7-162">Par exemple, une liste complète des packages bénéficiant de la contribution de la communauté est disponible sur le site [Spark Packages](http://spark-packages.org/)(Packages Spark).</span><span class="sxs-lookup"><span data-stu-id="83cc7-162">For example, a complete list of community-contributed packages is available at [Spark Packages](http://spark-packages.org/).</span></span>

<span data-ttu-id="83cc7-163">Dans cet article, vous verrez comment toouse hello [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) package avec un bloc-notes jupyter de hello.</span><span class="sxs-lookup"><span data-stu-id="83cc7-163">In this article, you will see how toouse hello [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) package with hello Jupyter notebook.</span></span>

1. <span data-ttu-id="83cc7-164">Ouvrez les paramètres de l’interpréteur.</span><span class="sxs-lookup"><span data-stu-id="83cc7-164">Open interpreter settings.</span></span> <span data-ttu-id="83cc7-165">Hello en haut à droite, cliquez sur hello consigné dans le nom d’utilisateur, puis cliquez sur **interpréteur**.</span><span class="sxs-lookup"><span data-stu-id="83cc7-165">From hello top-right corner, click hello logged in user name, and then click **Interpreter**.</span></span>
   
    <span data-ttu-id="83cc7-166">![Lancer l’interpréteur](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Sortie Hive")</span><span class="sxs-lookup"><span data-stu-id="83cc7-166">![Launch interpreter](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Hive output")</span></span>
2. <span data-ttu-id="83cc7-167">Faites défiler les paramètres d’interpréteur tooLivy, puis cliquez sur **modifier**.</span><span class="sxs-lookup"><span data-stu-id="83cc7-167">Scroll tooLivy interpreter settings and then click **Edit**.</span></span>
   
    <span data-ttu-id="83cc7-168">![Modifier les paramètres de l’interpréteur](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-use-external-package-1.png "Modifier les paramètres de l’interpréteur")</span><span class="sxs-lookup"><span data-stu-id="83cc7-168">![Change interpreter settings](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-use-external-package-1.png "Change interpreter settings")</span></span>
3. <span data-ttu-id="83cc7-169">Ajoutez une nouvelle clé, appelée **livy.spark.jars.packages** et définissez sa valeur au format de hello `group:id:version`.</span><span class="sxs-lookup"><span data-stu-id="83cc7-169">Add a new key, called **livy.spark.jars.packages** and set its value in hello format `group:id:version`.</span></span> <span data-ttu-id="83cc7-170">Par conséquent, si vous souhaitez toouse hello [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) package, vous devez définir les valeur hello de clé de hello trop`com.databricks:spark-csv_2.10:1.4.0`.</span><span class="sxs-lookup"><span data-stu-id="83cc7-170">So, if you want toouse hello [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) package, you must set hello value of hello key too`com.databricks:spark-csv_2.10:1.4.0`.</span></span>
   
    <span data-ttu-id="83cc7-171">![Modifier les paramètres de l’interpréteur](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-use-external-package-2.png "Modifier les paramètres de l’interpréteur")</span><span class="sxs-lookup"><span data-stu-id="83cc7-171">![Change interpreter settings](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-use-external-package-2.png "Change interpreter settings")</span></span>
   
    <span data-ttu-id="83cc7-172">Cliquez sur **enregistrer** , puis redémarrez hello interpréteur de Livy.</span><span class="sxs-lookup"><span data-stu-id="83cc7-172">Click **Save** and then restart hello Livy interpreter.</span></span>
4. <span data-ttu-id="83cc7-173">**Conseil**: Si vous souhaitez toounderstand comment tooarrive à la valeur de clé de hello d’hello entré ci-dessus, voici comment.</span><span class="sxs-lookup"><span data-stu-id="83cc7-173">**Tip**: If you want toounderstand how tooarrive at hello value of hello key entered above, here's how.</span></span>
   
    <span data-ttu-id="83cc7-174">a.</span><span class="sxs-lookup"><span data-stu-id="83cc7-174">a.</span></span> <span data-ttu-id="83cc7-175">Recherchez le package de hello Bonjour Maven référentiel.</span><span class="sxs-lookup"><span data-stu-id="83cc7-175">Locate hello package in hello Maven Repository.</span></span> <span data-ttu-id="83cc7-176">Dans ce didacticiel, nous avons utilisé [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar).</span><span class="sxs-lookup"><span data-stu-id="83cc7-176">For this tutorial, we used [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar).</span></span>
   
    <span data-ttu-id="83cc7-177">b.</span><span class="sxs-lookup"><span data-stu-id="83cc7-177">b.</span></span> <span data-ttu-id="83cc7-178">À partir de référentiel de hello, collectez les valeurs hello pour **GroupId**, **ArtifactId**, et **Version**.</span><span class="sxs-lookup"><span data-stu-id="83cc7-178">From hello repository, gather hello values for **GroupId**, **ArtifactId**, and **Version**.</span></span>
   
    <span data-ttu-id="83cc7-179">![Utiliser des packages externes avec le bloc-notes Jupyter](./media/hdinsight-apache-spark-zeppelin-notebook/use-external-packages-with-jupyter.png "Utiliser des packages externes avec le bloc-notes Jupyter")</span><span class="sxs-lookup"><span data-stu-id="83cc7-179">![Use external packages with Jupyter notebook](./media/hdinsight-apache-spark-zeppelin-notebook/use-external-packages-with-jupyter.png "Use external packages with Jupyter notebook")</span></span>
   
    <span data-ttu-id="83cc7-180">c.</span><span class="sxs-lookup"><span data-stu-id="83cc7-180">c.</span></span> <span data-ttu-id="83cc7-181">Concaténer des valeurs hello trois, séparés par un signe deux-points (**:**).</span><span class="sxs-lookup"><span data-stu-id="83cc7-181">Concatenate hello three values, separated by a colon (**:**).</span></span>
   
        com.databricks:spark-csv_2.10:1.4.0

## <a name="where-are-hello-zeppelin-notebooks-saved"></a><span data-ttu-id="83cc7-182">Où est hello blocs-notes Zeppelin enregistrées ?</span><span class="sxs-lookup"><span data-stu-id="83cc7-182">Where are hello Zeppelin notebooks saved?</span></span>
<span data-ttu-id="83cc7-183">ordinateurs portables de Hello Zeppelin sont enregistrés toohello cluster headnodes.</span><span class="sxs-lookup"><span data-stu-id="83cc7-183">hello Zeppelin notebooks are saved toohello cluster headnodes.</span></span> <span data-ttu-id="83cc7-184">Par conséquent, si vous supprimez le cluster de hello, les blocs-notes hello seront également supprimés.</span><span class="sxs-lookup"><span data-stu-id="83cc7-184">So, if you delete hello cluster, hello notebooks will be deleted as well.</span></span> <span data-ttu-id="83cc7-185">Si vous souhaitez toopreserve à vos blocs-notes et pour une utilisation ultérieure sur les autres clusters, vous devez les exporter une fois que vous avez terminé l’exécution des travaux de hello.</span><span class="sxs-lookup"><span data-stu-id="83cc7-185">If you want toopreserve your notebooks for later use on other clusters, you must export them after you have finished running hello jobs.</span></span> <span data-ttu-id="83cc7-186">tooexport un bloc-notes, cliquez sur hello **exporter** icône comme illustré dans l’image hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="83cc7-186">tooexport a notebook, click hello **Export** icon as shown in hello image below.</span></span>

<span data-ttu-id="83cc7-187">![Télécharger le bloc-notes](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-download-notebook.png "bloc-notes hello de téléchargement")</span><span class="sxs-lookup"><span data-stu-id="83cc7-187">![Download notebook](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-download-notebook.png "Download hello notebook")</span></span>

<span data-ttu-id="83cc7-188">Cela enregistre bloc-notes de hello sous la forme d’un fichier JSON dans l’emplacement de téléchargement.</span><span class="sxs-lookup"><span data-stu-id="83cc7-188">This saves hello notebook as a JSON file in your download location.</span></span>

## <a name="livy-session-management"></a><span data-ttu-id="83cc7-189">Gestion des sessions Livy</span><span class="sxs-lookup"><span data-stu-id="83cc7-189">Livy session management</span></span>
<span data-ttu-id="83cc7-190">Lorsque vous exécutez le premier paragraphe de code hello dans votre ordinateur portable Zeppelin, une nouvelle session Livy est créée dans votre cluster HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="83cc7-190">When you run hello first code paragraph in your Zeppelin notebook, a new Livy session is created in your HDInsight Spark cluster.</span></span> <span data-ttu-id="83cc7-191">Cette session est partagée par tous les blocs-notes Zeppelin que vous créerez par la suite.</span><span class="sxs-lookup"><span data-stu-id="83cc7-191">This session is shared across all Zeppelin notebooks that you subsequently create.</span></span> <span data-ttu-id="83cc7-192">If pour certains hello raison Livy session est arrêtée (redémarrage de cluster, etc.), vous ne serez pas toorun en mesure des travaux à partir de l’ordinateur portable de Zeppelin hello.</span><span class="sxs-lookup"><span data-stu-id="83cc7-192">If for some reason hello Livy session is killed (cluster reboot, etc.), you will not be able toorun jobs from hello Zeppelin notebook.</span></span>

<span data-ttu-id="83cc7-193">Dans ce cas, vous devez effectuer hello comme suit avant de commencer l’exécution des travaux à partir d’un ordinateur portable Zeppelin.</span><span class="sxs-lookup"><span data-stu-id="83cc7-193">In such a case, you must perform hello following steps before you can start running jobs from a Zeppelin notebook.</span></span> 

1. <span data-ttu-id="83cc7-194">Redémarrez hello interpréteur Livy à partir de l’ordinateur portable de Zeppelin hello.</span><span class="sxs-lookup"><span data-stu-id="83cc7-194">Restart hello Livy interpreter from hello Zeppelin notebook.</span></span> <span data-ttu-id="83cc7-195">toodo, ouvrez Paramètres de l’interpréteur en cliquant sur hello consigné dans le nom d’utilisateur à partir de l’angle supérieur droit de hello, puis cliquez sur **interpréteur**.</span><span class="sxs-lookup"><span data-stu-id="83cc7-195">toodo so, open interpreter settings by clicking hello logged in user name from hello top-right corner, and then click **Interpreter**.</span></span>
   
    <span data-ttu-id="83cc7-196">![Lancer l’interpréteur](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Sortie Hive")</span><span class="sxs-lookup"><span data-stu-id="83cc7-196">![Launch interpreter](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Hive output")</span></span>
2. <span data-ttu-id="83cc7-197">Faites défiler les paramètres d’interpréteur tooLivy, puis cliquez sur **redémarrer**.</span><span class="sxs-lookup"><span data-stu-id="83cc7-197">Scroll tooLivy interpreter settings and then click **Restart**.</span></span>
   
    <span data-ttu-id="83cc7-198">![Redémarrez hello Livy intepreter](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-restart-interpreter.png "redémarrer hello Zeppelin intepreter")</span><span class="sxs-lookup"><span data-stu-id="83cc7-198">![Restart hello Livy intepreter](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-restart-interpreter.png "Restart hello Zeppelin intepreter")</span></span>
3. <span data-ttu-id="83cc7-199">Exécutez une cellule de code à partir d’un bloc-notes Zeppelin existant.</span><span class="sxs-lookup"><span data-stu-id="83cc7-199">Run a code cell from an existing Zeppelin notebook.</span></span> <span data-ttu-id="83cc7-200">Cette opération crée une nouvelle session Livy dans le cluster HDInsight de hello.</span><span class="sxs-lookup"><span data-stu-id="83cc7-200">This creates a new Livy session in hello HDInsight cluster.</span></span>

## <span data-ttu-id="83cc7-201"><a name="seealso"></a>Voir aussi</span><span class="sxs-lookup"><span data-stu-id="83cc7-201"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="83cc7-202">Vue d’ensemble : Apache Spark sur Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="83cc7-202">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="83cc7-203">Scénarios</span><span class="sxs-lookup"><span data-stu-id="83cc7-203">Scenarios</span></span>
* [<span data-ttu-id="83cc7-204">Spark avec BI : effectuez une analyse interactive des données à l’aide de Spark dans HDInsight avec des outils BI</span><span class="sxs-lookup"><span data-stu-id="83cc7-204">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="83cc7-205">Spark avec Machine Learning : utilisez Spark dans HDInsight pour l’analyse de la température des bâtiments à l’aide des données des systèmes HVAC</span><span class="sxs-lookup"><span data-stu-id="83cc7-205">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="83cc7-206">Spark avec Machine Learning : Spark utilisation dans résultats de l’inspection alimentaires toopredict HDInsight</span><span class="sxs-lookup"><span data-stu-id="83cc7-206">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="83cc7-207">Streaming Spark : Utiliser Spark dans HDInsight pour créer des applications de diffusion en continu en temps réel</span><span class="sxs-lookup"><span data-stu-id="83cc7-207">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="83cc7-208">Analyse des journaux de site web à l’aide de Spark dans HDInsight</span><span class="sxs-lookup"><span data-stu-id="83cc7-208">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="83cc7-209">Créer et exécuter des applications</span><span class="sxs-lookup"><span data-stu-id="83cc7-209">Create and run applications</span></span>
* [<span data-ttu-id="83cc7-210">Créer une application autonome avec Scala</span><span class="sxs-lookup"><span data-stu-id="83cc7-210">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="83cc7-211">Exécuter des tâches à distance avec Livy sur un cluster Spark</span><span class="sxs-lookup"><span data-stu-id="83cc7-211">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="83cc7-212">Outils et extensions</span><span class="sxs-lookup"><span data-stu-id="83cc7-212">Tools and extensions</span></span>
* [<span data-ttu-id="83cc7-213">Utiliser le plug-in des outils HDInsight pour IntelliJ idée toocreate et soumettre des applications les plus importantes Spark Scala</span><span class="sxs-lookup"><span data-stu-id="83cc7-213">Use HDInsight Tools Plugin for IntelliJ IDEA toocreate and submit Spark Scala applicatons</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="83cc7-214">Utiliser des plug-in des outils HDInsight pour les applications de Spark toodebug IntelliJ idée à distance</span><span class="sxs-lookup"><span data-stu-id="83cc7-214">Use HDInsight Tools Plugin for IntelliJ IDEA toodebug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="83cc7-215">Noyaux disponibles pour le bloc-notes Jupyter dans un cluster Spark pour HDInsight</span><span class="sxs-lookup"><span data-stu-id="83cc7-215">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="83cc7-216">Utiliser des packages externes avec les blocs-notes Jupyter</span><span class="sxs-lookup"><span data-stu-id="83cc7-216">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="83cc7-217">Installer Notebook sur votre ordinateur et vous connecter tooan cluster HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="83cc7-217">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="83cc7-218">Gestion des ressources</span><span class="sxs-lookup"><span data-stu-id="83cc7-218">Manage resources</span></span>
* [<span data-ttu-id="83cc7-219">Gérer les ressources de cluster d’Apache Spark hello dans Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="83cc7-219">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="83cc7-220">Track and debug jobs running on an Apache Spark cluster in HDInsight (Suivi et débogage des tâches en cours d’exécution sur un cluster Apache Spark dans HDInsight)</span><span class="sxs-lookup"><span data-stu-id="83cc7-220">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md 







