---
title: "journaux du site Web aaaAnalyze avec les bibliothèques de Python dans Spark - Azure | Documents Microsoft"
description: "Ce bloc-notes montre comment enregistrer les données à l’aide d’une bibliothèque personnalisée avec Spark sur Azure HDInsight tooanalyze."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 8c61c70f-fe7f-4f0f-a4ab-0cccee5668c9
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 29e4308b2a359aee6d69494a98307d4da07f7909
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-website-logs-using-a-custom-python-library-with-spark-cluster-on-hdinsight"></a><span data-ttu-id="faa0d-103">Analyser des journaux de site web en utilisant une bibliothèque Python personnalisée avec un cluster Spark sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="faa0d-103">Analyze website logs using a custom Python library with Spark cluster on HDInsight</span></span>

<span data-ttu-id="faa0d-104">Ce bloc-notes montre comment enregistrer les données à l’aide d’une bibliothèque personnalisée avec Spark sur HDInsight tooanalyze.</span><span class="sxs-lookup"><span data-stu-id="faa0d-104">This notebook demonstrates how tooanalyze log data using a custom library with Spark on HDInsight.</span></span> <span data-ttu-id="faa0d-105">Hello personnalisé, nous utilisons est une bibliothèque Python appelé **iislogparser.py**.</span><span class="sxs-lookup"><span data-stu-id="faa0d-105">hello custom library we use is a Python library called **iislogparser.py**.</span></span>

> [!TIP]
> <span data-ttu-id="faa0d-106">Ce didacticiel est également disponible en tant que bloc-notes Jupyter sur un cluster Spark (Linux) que vous créez dans HDInsight.</span><span class="sxs-lookup"><span data-stu-id="faa0d-106">This tutorial is also available as a Jupyter notebook on a Spark (Linux) cluster that you create in HDInsight.</span></span> <span data-ttu-id="faa0d-107">expérience de bloc-notes Hello vous permet d’exécuter des extraits de code hello Python à partir de l’ordinateur portable hello lui-même.</span><span class="sxs-lookup"><span data-stu-id="faa0d-107">hello notebook experience lets you run hello Python snippets from hello notebook itself.</span></span> <span data-ttu-id="faa0d-108">didacticiel de hello tooperform à partir d’un ordinateur portable, créez un cluster Spark, lancer un bloc-notes jupyter (`https://CLUSTERNAME.azurehdinsight.net/jupyter`), puis exécutez bloc-notes de hello **analyser les journaux avec Spark à l’aide d’un library.ipynb personnalisé** sous hello  **PySpark** dossier.</span><span class="sxs-lookup"><span data-stu-id="faa0d-108">tooperform hello tutorial from within a notebook, create a Spark cluster, launch a Jupyter notebook (`https://CLUSTERNAME.azurehdinsight.net/jupyter`), and then run hello notebook **Analyze logs with Spark using a custom library.ipynb** under hello **PySpark** folder.</span></span>
>
>

<span data-ttu-id="faa0d-109">**Configuration requise :**</span><span class="sxs-lookup"><span data-stu-id="faa0d-109">**Prerequisites:**</span></span>

<span data-ttu-id="faa0d-110">Vous devez disposer de hello :</span><span class="sxs-lookup"><span data-stu-id="faa0d-110">You must have hello following:</span></span>

* <span data-ttu-id="faa0d-111">Un abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="faa0d-111">An Azure subscription.</span></span> <span data-ttu-id="faa0d-112">Consultez la page [Obtention d’un essai gratuit d’Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="faa0d-112">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

* <span data-ttu-id="faa0d-113">Un cluster Apache Spark sur HDInsight.</span><span class="sxs-lookup"><span data-stu-id="faa0d-113">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="faa0d-114">Pour obtenir des instructions, consultez [Création de clusters Apache Spark dans Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="faa0d-114">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="save-raw-data-as-an-rdd"></a><span data-ttu-id="faa0d-115">Enregistrer des données brutes en tant que RDD</span><span class="sxs-lookup"><span data-stu-id="faa0d-115">Save raw data as an RDD</span></span>
<span data-ttu-id="faa0d-116">Dans cette section, nous utilisons hello [Notebook](https://jupyter.org) bloc-notes associé à un cluster d’Apache Spark dans HDInsight travaux toorun traiter vos données d’exemple brut et l’enregistrer en tant qu’une table Hive.</span><span class="sxs-lookup"><span data-stu-id="faa0d-116">In this section, we use hello [Jupyter](https://jupyter.org) notebook associated with an Apache Spark cluster in HDInsight toorun jobs that process your raw sample data and save it as a Hive table.</span></span> <span data-ttu-id="faa0d-117">données d’exemple Hello sont un fichier .csv (hvac.csv) disponible sur tous les clusters par défaut.</span><span class="sxs-lookup"><span data-stu-id="faa0d-117">hello sample data is a .csv file (hvac.csv) available on all clusters by default.</span></span>

<span data-ttu-id="faa0d-118">Une fois que vos données sont enregistrées dans une table Hive, nous se connecte dans la section suivante de hello table Hive de toohello à l’aide des outils de BI tels que Power BI et de Tableau.</span><span class="sxs-lookup"><span data-stu-id="faa0d-118">Once your data is saved as a Hive table, in hello next section we will connect toohello Hive table using BI tools such as Power BI and Tableau.</span></span>

1. <span data-ttu-id="faa0d-119">À partir de hello [portail Azure](https://portal.azure.com/), à partir du tableau d’accueil hello, cliquez sur la vignette hello pour votre cluster Spark (si vous avez épinglé il toohello tableau d’accueil).</span><span class="sxs-lookup"><span data-stu-id="faa0d-119">From hello [Azure portal](https://portal.azure.com/), from hello startboard, click hello tile for your Spark cluster (if you pinned it toohello startboard).</span></span> <span data-ttu-id="faa0d-120">Vous pouvez également naviguer cluster tooyour sous **parcourir tous les** > **Clusters HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="faa0d-120">You can also navigate tooyour cluster under **Browse All** > **HDInsight Clusters**.</span></span>   
2. <span data-ttu-id="faa0d-121">Dans le panneau de cluster Spark hello, cliquez sur **tableau de bord de Cluster**, puis cliquez sur **bloc-notes Jupyter**.</span><span class="sxs-lookup"><span data-stu-id="faa0d-121">From hello Spark cluster blade, click **Cluster Dashboard**, and then click **Jupyter Notebook**.</span></span> <span data-ttu-id="faa0d-122">Si vous y êtes invité, entrez les informations d’identification du admin de hello pour le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="faa0d-122">If prompted, enter hello admin credentials for hello cluster.</span></span>

   > [!NOTE]
   > <span data-ttu-id="faa0d-123">Vous pouvez également atteindre hello bloc-notes Jupyter pour votre cluster en hello ouverture suivante d’URL dans votre navigateur.</span><span class="sxs-lookup"><span data-stu-id="faa0d-123">You may also reach hello Jupyter Notebook for your cluster by opening hello following URL in your browser.</span></span> <span data-ttu-id="faa0d-124">Remplacez **CLUSTERNAME** avec nom hello de votre cluster :</span><span class="sxs-lookup"><span data-stu-id="faa0d-124">Replace **CLUSTERNAME** with hello name of your cluster:</span></span>
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >
3. <span data-ttu-id="faa0d-125">Créer un nouveau bloc-notes.</span><span class="sxs-lookup"><span data-stu-id="faa0d-125">Create a new notebook.</span></span> <span data-ttu-id="faa0d-126">Cliquez sur **Nouveau**, puis sur **PySpark**.</span><span class="sxs-lookup"><span data-stu-id="faa0d-126">Click **New**, and then click **PySpark**.</span></span>

    <span data-ttu-id="faa0d-127">![Créer un bloc-notes Jupyter](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-create-jupyter-notebook.png "Créer un bloc-notes Jupyter")</span><span class="sxs-lookup"><span data-stu-id="faa0d-127">![Create a new Jupyter notebook](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-create-jupyter-notebook.png "Create a new Jupyter notebook")</span></span>
4. <span data-ttu-id="faa0d-128">Un nouvel ordinateur portable est créé et ouvert avec le nom hello Untitled.pynb.</span><span class="sxs-lookup"><span data-stu-id="faa0d-128">A new notebook is created and opened with hello name Untitled.pynb.</span></span> <span data-ttu-id="faa0d-129">Cliquez sur le nom du bloc-notes hello haut hello et entrez un nom convivial.</span><span class="sxs-lookup"><span data-stu-id="faa0d-129">Click hello notebook name at hello top, and enter a friendly name.</span></span>

    <span data-ttu-id="faa0d-130">![Fournissez un nom pour l’ordinateur portable de hello](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-name-jupyter-notebook.png "fournir un nom d’ordinateur portable de hello")</span><span class="sxs-lookup"><span data-stu-id="faa0d-130">![Provide a name for hello notebook](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-name-jupyter-notebook.png "Provide a name for hello notebook")</span></span>
5. <span data-ttu-id="faa0d-131">Étant donné que vous avez créé un ordinateur portable à l’aide de noyau de PySpark hello, il est inutile toocreate les contextes explicitement.</span><span class="sxs-lookup"><span data-stu-id="faa0d-131">Because you created a notebook using hello PySpark kernel, you do not need toocreate any contexts explicitly.</span></span> <span data-ttu-id="faa0d-132">contextes de Spark et Hive Hello seront automatiquement créés pour vous lors de l’exécution de la première cellule de code hello.</span><span class="sxs-lookup"><span data-stu-id="faa0d-132">hello Spark and Hive contexts will be automatically created for you when you run hello first code cell.</span></span> <span data-ttu-id="faa0d-133">Vous pouvez commencer par importer les types hello qui sont requis pour ce scénario.</span><span class="sxs-lookup"><span data-stu-id="faa0d-133">You can start by importing hello types that are required for this scenario.</span></span> <span data-ttu-id="faa0d-134">Collez hello suivant extrait dans une cellule vide, puis appuyez sur **MAJ + ENTRÉE**.</span><span class="sxs-lookup"><span data-stu-id="faa0d-134">Paste hello following snippet in an empty cell, and then press **SHIFT + ENTER**.</span></span>

        from pyspark.sql import Row
        from pyspark.sql.types import *


1. <span data-ttu-id="faa0d-135">Créer un RDD à l’aide des données de journal exemple hello déjà disponibles sur le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="faa0d-135">Create an RDD using hello sample log data already available on hello cluster.</span></span> <span data-ttu-id="faa0d-136">Vous pouvez accéder aux hello hello compte de stockage par défaut associé au cluster hello à **\HdiSamples\HdiSamples\WebsiteLogSampleData\SampleLog\909f2b.log**.</span><span class="sxs-lookup"><span data-stu-id="faa0d-136">You can access hello data in hello default storage account associated with hello cluster at **\HdiSamples\HdiSamples\WebsiteLogSampleData\SampleLog\909f2b.log**.</span></span>

        logs = sc.textFile('wasb:///HdiSamples/HdiSamples/WebsiteLogSampleData/SampleLog/909f2b.log')


1. <span data-ttu-id="faa0d-137">Récupérer qu'un exemple de journal défini tooverify cette étape précédente hello s’est terminée correctement.</span><span class="sxs-lookup"><span data-stu-id="faa0d-137">Retrieve a sample log set tooverify that hello previous step completed successfully.</span></span>

        logs.take(5)

    <span data-ttu-id="faa0d-138">Vous devez voir s’afficher une sortie similaire toohello :</span><span class="sxs-lookup"><span data-stu-id="faa0d-138">You should see an output similar toohello following:</span></span>

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        [u'#Software: Microsoft Internet Information Services 8.0',
         u'#Fields: date time s-sitename cs-method cs-uri-stem cs-uri-query s-port cs-username c-ip cs(User-Agent) cs(Cookie) cs(Referer) cs-host sc-status sc-substatus sc-win32-status sc-bytes cs-bytes time-taken',
         u'2014-01-01 02:01:09 SAMPLEWEBSITE GET /blogposts/mvc4/step2.png X-ARR-LOG-ID=2ec4b8ad-3cf0-4442-93ab-837317ece6a1 80 - 1.54.23.196 Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36 - http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx www.sample.com 200 0 0 53175 871 46',
         u'2014-01-01 02:01:09 SAMPLEWEBSITE GET /blogposts/mvc4/step3.png X-ARR-LOG-ID=9eace870-2f49-4efd-b204-0d170da46b4a 80 - 1.54.23.196 Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36 - http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx www.sample.com 200 0 0 51237 871 32',
         u'2014-01-01 02:01:09 SAMPLEWEBSITE GET /blogposts/mvc4/step4.png X-ARR-LOG-ID=4bea5b3d-8ac9-46c9-9b8c-ec3e9500cbea 80 - 1.54.23.196 Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36 - http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx www.sample.com 200 0 0 72177 871 47']

## <a name="analyze-log-data-using-a-custom-python-library"></a><span data-ttu-id="faa0d-139">Analysez les données de journal à l'aide d'une bibliothèque Python personnalisée</span><span class="sxs-lookup"><span data-stu-id="faa0d-139">Analyze log data using a custom Python library</span></span>
1. <span data-ttu-id="faa0d-140">Dans la sortie de hello ci-dessus, hello premier deux lignes incluent des informations d’en-tête hello et chaque ligne restante correspond au schéma de hello décrit dans cet en-tête.</span><span class="sxs-lookup"><span data-stu-id="faa0d-140">In hello output above, hello first couple lines include hello header information and each remaining line matches hello schema described in that header.</span></span> <span data-ttu-id="faa0d-141">L’analyse de tels journaux peut s’avérer complexe.</span><span class="sxs-lookup"><span data-stu-id="faa0d-141">Parsing such logs could be complicated.</span></span> <span data-ttu-id="faa0d-142">Par conséquent, nous utilisons une bibliothèque Python personnalisée (**iislogparser.py**) qui facilite beaucoup l'analyse de tels journaux.</span><span class="sxs-lookup"><span data-stu-id="faa0d-142">So, we use a custom Python library (**iislogparser.py**) that makes parsing such logs much easier.</span></span> <span data-ttu-id="faa0d-143">Par défaut, cette bibliothèque est incluse avec votre cluster Spark sur HDInsight dans **/HdiSamples/HdiSamples/WebsiteLogSampleData/iislogparser.py**.</span><span class="sxs-lookup"><span data-stu-id="faa0d-143">By default, this library is included with your Spark cluster on HDInsight at **/HdiSamples/HdiSamples/WebsiteLogSampleData/iislogparser.py**.</span></span>

    <span data-ttu-id="faa0d-144">Toutefois, cette bibliothèque n’est pas Bonjour `PYTHONPATH` donc nous ne pouvons pas l’utiliser à l’aide d’une instruction d’importation comme `import iislogparser`.</span><span class="sxs-lookup"><span data-stu-id="faa0d-144">However, this library is not in hello `PYTHONPATH` so we cannot use it by using an import statement like `import iislogparser`.</span></span> <span data-ttu-id="faa0d-145">toouse cette bibliothèque, nous devons distribuer de nœuds de travail tooall hello.</span><span class="sxs-lookup"><span data-stu-id="faa0d-145">toouse this library, we must distribute it tooall hello worker nodes.</span></span> <span data-ttu-id="faa0d-146">Exécutez hello suivant extrait de code.</span><span class="sxs-lookup"><span data-stu-id="faa0d-146">Run hello following snippet.</span></span>

        sc.addPyFile('wasb:///HdiSamples/HdiSamples/WebsiteLogSampleData/iislogparser.py')


1. <span data-ttu-id="faa0d-147">`iislogparser`Fournit une fonction `parse_log_line` qui retourne `None` si une ligne de journal est une ligne d’en-tête et retourne une instance de hello `LogLine` classe s’il rencontre une ligne de journal.</span><span class="sxs-lookup"><span data-stu-id="faa0d-147">`iislogparser` provides a function `parse_log_line` that returns `None` if a log line is a header row, and returns an instance of hello `LogLine` class if it encounters a log line.</span></span> <span data-ttu-id="faa0d-148">Hello d’utilisation `LogLine` tooextract de la classe hello uniquement les lignes de journal à partir de hello RDD :</span><span class="sxs-lookup"><span data-stu-id="faa0d-148">Use hello `LogLine` class tooextract only hello log lines from hello RDD:</span></span>

        def parse_line(l):
            import iislogparser
            return iislogparser.parse_log_line(l)
        logLines = logs.map(parse_line).filter(lambda p: p is not None).cache()
2. <span data-ttu-id="faa0d-149">Récupérer quelques lignes extraites du journal tooverify qui hello étape s’est terminée avec succès.</span><span class="sxs-lookup"><span data-stu-id="faa0d-149">Retrieve a couple of extracted log lines tooverify that hello step completed successfully.</span></span>

       logLines.take(2)

   <span data-ttu-id="faa0d-150">sortie de Hello sont similaires toohello suivants :</span><span class="sxs-lookup"><span data-stu-id="faa0d-150">hello output should be similar toohello following:</span></span>

       # -----------------
       # THIS IS AN OUTPUT
       # -----------------

       [2014-01-01 02:01:09 SAMPLEWEBSITE GET /blogposts/mvc4/step2.png X-ARR-LOG-ID=2ec4b8ad-3cf0-4442-93ab-837317ece6a1 80 - 1.54.23.196 Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36 - http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx www.sample.com 200 0 0 53175 871 46,
        2014-01-01 02:01:09 SAMPLEWEBSITE GET /blogposts/mvc4/step3.png X-ARR-LOG-ID=9eace870-2f49-4efd-b204-0d170da46b4a 80 - 1.54.23.196 Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36 - http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx www.sample.com 200 0 0 51237 871 32]
3. <span data-ttu-id="faa0d-151">Hello `LogLine` (classe), à son tour, a des méthodes utiles, tels que `is_error()`, qui indique si une entrée de journal a un code d’erreur.</span><span class="sxs-lookup"><span data-stu-id="faa0d-151">hello `LogLine` class, in turn, has some useful methods, like `is_error()`, which returns whether a log entry has an error code.</span></span> <span data-ttu-id="faa0d-152">Utiliser ce numéro de hello toocompute des erreurs de lignes du journal hello extrait et puis journal tous les hello erreurs tooa différents.</span><span class="sxs-lookup"><span data-stu-id="faa0d-152">Use this toocompute hello number of errors in hello extracted log lines, and then log all hello errors tooa different file.</span></span>

       errors = logLines.filter(lambda p: p.is_error())
       numLines = logLines.count()
       numErrors = errors.count()
       print 'There are', numErrors, 'errors and', numLines, 'log entries'
       errors.map(lambda p: str(p)).saveAsTextFile('wasb:///HdiSamples/HdiSamples/WebsiteLogSampleData/SampleLog/909f2b-2.log')

   <span data-ttu-id="faa0d-153">Vous devez voir une sortie semblable à hello suivante :</span><span class="sxs-lookup"><span data-stu-id="faa0d-153">You should see an output like hello following:</span></span>

       # -----------------
       # THIS IS AN OUTPUT
       # -----------------

       There are 30 errors and 646 log entries
4. <span data-ttu-id="faa0d-154">Vous pouvez également utiliser **Matplotlib** tooconstruct une visualisation des données de hello.</span><span class="sxs-lookup"><span data-stu-id="faa0d-154">You can also use **Matplotlib** tooconstruct a visualization of hello data.</span></span> <span data-ttu-id="faa0d-155">Par exemple, si vous souhaitez la cause de hello tooisolate de requêtes qui s’exécutent pendant une longue période, vous pourriez fichiers hello toofind prenant hello la plupart des tooserve de temps en moyenne.</span><span class="sxs-lookup"><span data-stu-id="faa0d-155">For example, if you want tooisolate hello cause of requests that run for a long time, you might want toofind hello files that take hello most time tooserve on average.</span></span>
   <span data-ttu-id="faa0d-156">extrait de code Hello ci-dessous récupère hello top 25 ressources qui a nécessité la plupart des temps tooserve une demande.</span><span class="sxs-lookup"><span data-stu-id="faa0d-156">hello snippet below retrieves hello top 25 resources that took most time tooserve a request.</span></span>

       def avgTimeTakenByKey(rdd):
           return rdd.combineByKey(lambda line: (line.time_taken, 1),
                                   lambda x, line: (x[0] + line.time_taken, x[1] + 1),
                                   lambda x, y: (x[0] + y[0], x[1] + y[1]))\
                     .map(lambda x: (x[0], float(x[1][0]) / float(x[1][1])))

       avgTimeTakenByKey(logLines.map(lambda p: (p.cs_uri_stem, p))).top(25, lambda x: x[1])

   <span data-ttu-id="faa0d-157">Vous devez voir une sortie semblable à hello suivante :</span><span class="sxs-lookup"><span data-stu-id="faa0d-157">You should see an output like hello following:</span></span>

       # -----------------
       # THIS IS AN OUTPUT
       # -----------------

       [(u'/blogposts/mvc4/step13.png', 197.5),
        (u'/blogposts/mvc2/step10.jpg', 179.5),
        (u'/blogposts/extractusercontrol/step5.png', 170.0),
        (u'/blogposts/mvc4/step8.png', 159.0),
        (u'/blogposts/mvcrouting/step22.jpg', 155.0),
        (u'/blogposts/mvcrouting/step3.jpg', 152.0),
        (u'/blogposts/linqsproc1/step16.jpg', 138.75),
        (u'/blogposts/linqsproc1/step26.jpg', 137.33333333333334),
        (u'/blogposts/vs2008javascript/step10.jpg', 127.0),
        (u'/blogposts/nested/step2.jpg', 126.0),
        (u'/blogposts/adminpack/step1.png', 124.0),
        (u'/BlogPosts/datalistpaging/step2.png', 118.0),
        (u'/blogposts/mvc4/step35.png', 117.0),
        (u'/blogposts/mvcrouting/step2.jpg', 116.5),
        (u'/blogposts/aboutme/basketball.jpg', 109.0),
        (u'/blogposts/anonymoustypes/step11.jpg', 109.0),
        (u'/blogposts/mvc4/step12.png', 106.0),
        (u'/blogposts/linq8/step0.jpg', 105.5),
        (u'/blogposts/mvc2/step18.jpg', 104.0),
        (u'/blogposts/mvc2/step11.jpg', 104.0),
        (u'/blogposts/mvcrouting/step1.jpg', 104.0),
        (u'/blogposts/extractusercontrol/step1.png', 103.0),
        (u'/blogposts/sqlvideos/sqlvideos.jpg', 102.0),
        (u'/blogposts/mvcrouting/step21.jpg', 101.0),
        (u'/blogposts/mvc4/step1.png', 98.0)]
5. <span data-ttu-id="faa0d-158">Vous pouvez également présenter ces informations sous forme de hello du tracé.</span><span class="sxs-lookup"><span data-stu-id="faa0d-158">You can also present this information in hello form of plot.</span></span> <span data-ttu-id="faa0d-159">Une première étape toocreate un tracé, faites-le nous tout d’abord créer une table temporaire **AverageTime**.</span><span class="sxs-lookup"><span data-stu-id="faa0d-159">As a first step toocreate a plot, let us first create a temporary table **AverageTime**.</span></span> <span data-ttu-id="faa0d-160">Bonjour Bonjour de groupes de table ouvre une session en temps toosee s’il y a des pics d’activité inhabituelle latence à un moment donné.</span><span class="sxs-lookup"><span data-stu-id="faa0d-160">hello table groups hello logs by time toosee if there were any unusual latency spikes at any particular time.</span></span>

       avgTimeTakenByMinute = avgTimeTakenByKey(logLines.map(lambda p: (p.datetime.minute, p))).sortByKey()
       schema = StructType([StructField('Minutes', IntegerType(), True),
                            StructField('Time', FloatType(), True)])

       avgTimeTakenByMinuteDF = sqlContext.createDataFrame(avgTimeTakenByMinute, schema)
       avgTimeTakenByMinuteDF.registerTempTable('AverageTime')
6. <span data-ttu-id="faa0d-161">Vous pouvez ensuite exécuter hello suivant tooget de requête SQL tous les enregistrements de hello Bonjour **AverageTime** table.</span><span class="sxs-lookup"><span data-stu-id="faa0d-161">You can then run hello following SQL query tooget all hello records in hello **AverageTime** table.</span></span>

       %%sql -o averagetime
       SELECT * FROM AverageTime

   <span data-ttu-id="faa0d-162">Hello `%%sql` magique suivie `-o averagetime` garantit que sortie hello de requête de hello est rendu persistant localement sur le serveur de Notebook hello (généralement hello nœud principal du cluster de hello).</span><span class="sxs-lookup"><span data-stu-id="faa0d-162">hello `%%sql` magic followed by `-o averagetime` ensures that hello output of hello query is persisted locally on hello Jupyter server (typically hello headnode of hello cluster).</span></span> <span data-ttu-id="faa0d-163">sortie de Hello est conservée en tant qu’un [Pandas](http://pandas.pydata.org/) nom spécifié de trame de données avec hello **averagetime**.</span><span class="sxs-lookup"><span data-stu-id="faa0d-163">hello output is persisted as a [Pandas](http://pandas.pydata.org/) dataframe with hello specified name **averagetime**.</span></span>

   <span data-ttu-id="faa0d-164">Vous devez voir une sortie semblable à hello suivante :</span><span class="sxs-lookup"><span data-stu-id="faa0d-164">You should see an output like hello following:</span></span>

   <span data-ttu-id="faa0d-165">![Résultat de la requête SQL](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-jupyter-sql-qyery-output.png "Résultat de la requête SQL")</span><span class="sxs-lookup"><span data-stu-id="faa0d-165">![SQL query output](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-jupyter-sql-qyery-output.png "SQL query output")</span></span>

   <span data-ttu-id="faa0d-166">Pour plus d’informations sur hello `%%sql` magic, voir [paramètres pris en charge par hello %% sql magic](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span><span class="sxs-lookup"><span data-stu-id="faa0d-166">For more information about hello `%%sql` magic, see [Parameters supported with hello %%sql magic](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span></span>
7. <span data-ttu-id="faa0d-167">Vous pouvez maintenant utiliser Matplotlib, une bibliothèque utilisée tooconstruct une visualisation des données, toocreate un tracé.</span><span class="sxs-lookup"><span data-stu-id="faa0d-167">You can now use Matplotlib, a library used tooconstruct visualization of data, toocreate a plot.</span></span> <span data-ttu-id="faa0d-168">Étant donné que le traçage de hello doit être créé à partir de hello localement persistantes **averagetime** trame de données, l’extrait de code hello doit commencer par hello `%%local` magique.</span><span class="sxs-lookup"><span data-stu-id="faa0d-168">Because hello plot must be created from hello locally persisted **averagetime** dataframe, hello code snippet must begin with hello `%%local` magic.</span></span> <span data-ttu-id="faa0d-169">Cela garantit que le code de hello est exécuté localement sur le serveur de Notebook hello.</span><span class="sxs-lookup"><span data-stu-id="faa0d-169">This ensures that hello code is run locally on hello Jupyter server.</span></span>

       %%local
       %matplotlib inline
       import matplotlib.pyplot as plt

       plt.plot(averagetime['Minutes'], averagetime['Time'], marker='o', linestyle='--')
       plt.xlabel('Time (min)')
       plt.ylabel('Average time taken for request (ms)')

   <span data-ttu-id="faa0d-170">Vous devez voir une sortie semblable à hello suivante :</span><span class="sxs-lookup"><span data-stu-id="faa0d-170">You should see an output like hello following:</span></span>

   <span data-ttu-id="faa0d-171">![Résultat Matplotlib](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-apache-spark-web-log-analysis-plot.png "Résultat Matplotlib")</span><span class="sxs-lookup"><span data-stu-id="faa0d-171">![Matplotlib output](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-apache-spark-web-log-analysis-plot.png "Matplotlib output")</span></span>
8. <span data-ttu-id="faa0d-172">Une fois que vous avez terminé d’exécuter l’application hello, vous devez le ressources hello toorelease arrêt hello bloc-notes.</span><span class="sxs-lookup"><span data-stu-id="faa0d-172">After you have finished running hello application, you should shutdown hello notebook toorelease hello resources.</span></span> <span data-ttu-id="faa0d-173">toodo donc de hello **fichier** cliquez sur le menu d’un ordinateur portable hello, **fermer et s’arrêter**.</span><span class="sxs-lookup"><span data-stu-id="faa0d-173">toodo so, from hello **File** menu on hello notebook, click **Close and Halt**.</span></span> <span data-ttu-id="faa0d-174">Cette s’arrête et le bloc-notes de fermer hello.</span><span class="sxs-lookup"><span data-stu-id="faa0d-174">This will shutdown and close hello notebook.</span></span>

## <span data-ttu-id="faa0d-175"><a name="seealso"></a>Voir aussi</span><span class="sxs-lookup"><span data-stu-id="faa0d-175"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="faa0d-176">Vue d’ensemble : Apache Spark sur Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="faa0d-176">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="faa0d-177">Scénarios</span><span class="sxs-lookup"><span data-stu-id="faa0d-177">Scenarios</span></span>
* [<span data-ttu-id="faa0d-178">Spark avec BI : effectuez une analyse interactive des données à l’aide de Spark dans HDInsight avec des outils BI</span><span class="sxs-lookup"><span data-stu-id="faa0d-178">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="faa0d-179">Spark avec Machine Learning : utilisez Spark dans HDInsight pour l’analyse de la température des bâtiments à l’aide des données des systèmes HVAC</span><span class="sxs-lookup"><span data-stu-id="faa0d-179">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="faa0d-180">Spark avec Machine Learning : Spark utilisation dans résultats de l’inspection alimentaires toopredict HDInsight</span><span class="sxs-lookup"><span data-stu-id="faa0d-180">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="faa0d-181">Streaming Spark : Utiliser Spark dans HDInsight pour créer des applications de diffusion en continu en temps réel</span><span class="sxs-lookup"><span data-stu-id="faa0d-181">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="faa0d-182">Création et exécution d’applications</span><span class="sxs-lookup"><span data-stu-id="faa0d-182">Create and run applications</span></span>
* [<span data-ttu-id="faa0d-183">Créer une application autonome avec Scala</span><span class="sxs-lookup"><span data-stu-id="faa0d-183">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="faa0d-184">Exécuter des tâches à distance avec Livy sur un cluster Spark</span><span class="sxs-lookup"><span data-stu-id="faa0d-184">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="faa0d-185">Outils et extensions</span><span class="sxs-lookup"><span data-stu-id="faa0d-185">Tools and extensions</span></span>
* [<span data-ttu-id="faa0d-186">Utiliser le plug-in des outils HDInsight pour IntelliJ idée toocreate et soumettre des applications de Spark Scala</span><span class="sxs-lookup"><span data-stu-id="faa0d-186">Use HDInsight Tools Plugin for IntelliJ IDEA toocreate and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="faa0d-187">Utiliser des plug-in des outils HDInsight pour les applications de Spark toodebug IntelliJ idée à distance</span><span class="sxs-lookup"><span data-stu-id="faa0d-187">Use HDInsight Tools Plugin for IntelliJ IDEA toodebug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="faa0d-188">Utiliser des bloc-notes Zeppelin avec un cluster Spark sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="faa0d-188">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="faa0d-189">Noyaux disponibles pour le bloc-notes Jupyter dans un cluster Spark pour HDInsight</span><span class="sxs-lookup"><span data-stu-id="faa0d-189">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="faa0d-190">Utiliser des packages externes avec les blocs-notes Jupyter</span><span class="sxs-lookup"><span data-stu-id="faa0d-190">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="faa0d-191">Installer Notebook sur votre ordinateur et vous connecter tooan cluster HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="faa0d-191">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="faa0d-192">Gestion des ressources</span><span class="sxs-lookup"><span data-stu-id="faa0d-192">Manage resources</span></span>
* [<span data-ttu-id="faa0d-193">Gérer les ressources de cluster d’Apache Spark hello dans Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="faa0d-193">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="faa0d-194">Track and debug jobs running on an Apache Spark cluster in HDInsight (Suivi et débogage des tâches en cours d’exécution sur un cluster Apache Spark dans HDInsight)</span><span class="sxs-lookup"><span data-stu-id="faa0d-194">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)
