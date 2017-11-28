---
title: "aaaMapReduce et Bureau à distance avec Hadoop dans HDInsight - Azure | Documents Microsoft"
description: "Découvrez comment toouse Bureau à distance tooconnect tooHadoop sur HDInsight et d’exécuter les tâches MapReduce."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 9d3a7b34-7def-4c2e-bb6c-52682d30dee8
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 01/12/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: bdbbcf59ca86dd1b170471aa9e12334a04c23667
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-mapreduce-in-hadoop-on-hdinsight-with-remote-desktop"></a><span data-ttu-id="898e0-103">Utilisation de MapReduce dans Hadoop sur HDInsight avec le Bureau à distance</span><span class="sxs-lookup"><span data-stu-id="898e0-103">Use MapReduce in Hadoop on HDInsight with Remote Desktop</span></span>
[!INCLUDE [mapreduce-selector](../../includes/hdinsight-selector-use-mapreduce.md)]

<span data-ttu-id="898e0-104">Dans cet article, vous découvrez comment tooconnect tooa Hadoop dans HDInsight cluster à l’aide de bureau à distance et puis exécutez les tâches MapReduce à l’aide des commandes de Hadoop hello.</span><span class="sxs-lookup"><span data-stu-id="898e0-104">In this article, you will learn how tooconnect tooa Hadoop on HDInsight cluster by using Remote Desktop and then run MapReduce jobs by using hello Hadoop command.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="898e0-105">Le Bureau à distance n’est disponible que sur les clusters HDInsight Windows.</span><span class="sxs-lookup"><span data-stu-id="898e0-105">Remote Desktop is only available on Windows-based HDInsight clusters.</span></span> <span data-ttu-id="898e0-106">Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure.</span><span class="sxs-lookup"><span data-stu-id="898e0-106">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="898e0-107">Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="898e0-107">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>
>
> <span data-ttu-id="898e0-108">Pour HDInsight 3.4 ou supérieure, consultez [MapReduce utilisation avec SSH](hdinsight-hadoop-use-mapreduce-ssh.md) pour plus d’informations sur la connexion de cluster HDInsight de toohello et l’exécution des tâches MapReduce.</span><span class="sxs-lookup"><span data-stu-id="898e0-108">For HDInsight 3.4 or greater, see [Use MapReduce with SSH](hdinsight-hadoop-use-mapreduce-ssh.md) for information on connecting toohello HDInsight cluster and running MapReduce jobs.</span></span>

## <span data-ttu-id="898e0-109"><a id="prereq"></a>Configuration requise</span><span class="sxs-lookup"><span data-stu-id="898e0-109"><a id="prereq"></a>Prerequisites</span></span>
<span data-ttu-id="898e0-110">toocomplete hello étapes décrites dans cet article, vous devez suivant de hello :</span><span class="sxs-lookup"><span data-stu-id="898e0-110">toocomplete hello steps in this article, you will need hello following:</span></span>

* <span data-ttu-id="898e0-111">un cluster HDInsight basé sur Windows (Hadoop sur HDInsight)</span><span class="sxs-lookup"><span data-stu-id="898e0-111">A Windows-based HDInsight (Hadoop on HDInsight) cluster</span></span>
* <span data-ttu-id="898e0-112">Un ordinateur client avec Windows 10, Windows 8 ou Windows 7</span><span class="sxs-lookup"><span data-stu-id="898e0-112">A client computer running Windows 10, Windows 8, or Windows 7</span></span>

## <span data-ttu-id="898e0-113"><a id="connect"></a>Connexion avec le Bureau à distance</span><span class="sxs-lookup"><span data-stu-id="898e0-113"><a id="connect"></a>Connect with Remote Desktop</span></span>
<span data-ttu-id="898e0-114">Activer le Bureau à distance pour le cluster HDInsight de hello, puis connecter tooit en suivant les instructions de hello sur [connecter clusters tooHDInsight à l’aide du protocole RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span><span class="sxs-lookup"><span data-stu-id="898e0-114">Enable Remote Desktop for hello HDInsight cluster, then connect tooit by following hello instructions at [Connect tooHDInsight clusters using RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span></span>

## <span data-ttu-id="898e0-115"><a id="hadoop"></a>Utilisez la commande de Hadoop hello</span><span class="sxs-lookup"><span data-stu-id="898e0-115"><a id="hadoop"></a>Use hello Hadoop command</span></span>
<span data-ttu-id="898e0-116">Lorsque vous êtes bureau toohello connecté pour le cluster HDInsight de hello, utilisez hello suivant les étapes toorun une tâche MapReduce à l’aide des commandes de Hadoop hello :</span><span class="sxs-lookup"><span data-stu-id="898e0-116">When you are connected toohello desktop for hello HDInsight cluster, use hello following steps toorun a MapReduce job by using hello Hadoop command:</span></span>

1. <span data-ttu-id="898e0-117">À partir du bureau de HDInsight hello, démarrer hello **ligne de commande Hadoop**.</span><span class="sxs-lookup"><span data-stu-id="898e0-117">From hello HDInsight desktop, start hello **Hadoop Command Line**.</span></span> <span data-ttu-id="898e0-118">Cette opération ouvre une nouvelle invite de commandes Bonjour **c:\apps\dist\hadoop-&lt;numéro de version >** active.</span><span class="sxs-lookup"><span data-stu-id="898e0-118">This opens a new command prompt in hello **c:\apps\dist\hadoop-&lt;version number>** directory.</span></span>

   > [!NOTE]
   > <span data-ttu-id="898e0-119">numéro de version Hello change à mesure que Hadoop est mis à jour.</span><span class="sxs-lookup"><span data-stu-id="898e0-119">hello version number changes as Hadoop is updated.</span></span> <span data-ttu-id="898e0-120">Hello **HADOOP_HOME** variable d’environnement peut être le chemin d’accès de toofind utilisé hello.</span><span class="sxs-lookup"><span data-stu-id="898e0-120">hello **HADOOP_HOME** environment variable can be used toofind hello path.</span></span> <span data-ttu-id="898e0-121">Par exemple, `cd %HADOOP_HOME%` répertoire Hadoop toohello modifications répertoires, sans que vous ayez un numéro de version tooknow hello.</span><span class="sxs-lookup"><span data-stu-id="898e0-121">For example, `cd %HADOOP_HOME%` changes directories toohello Hadoop directory, without requiring you tooknow hello version number.</span></span>
   >
   >
2. <span data-ttu-id="898e0-122">toouse hello **Hadoop** toorun un travail MapReduce d’exemple de commande, utilisez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="898e0-122">toouse hello **Hadoop** command toorun an example MapReduce job, use hello following command:</span></span>

        hadoop jar hadoop-mapreduce-examples.jar wordcount wasb:///example/data/gutenberg/davinci.txt wasb:///example/data/WordCountOutput

    <span data-ttu-id="898e0-123">Cela démarre hello **wordcount** (classe), qui est contenue dans hello **hadoop-mapreduce-Examples.jar** fichier hello répertoire en cours.</span><span class="sxs-lookup"><span data-stu-id="898e0-123">This starts hello **wordcount** class, which is contained in hello **hadoop-mapreduce-examples.jar** file in hello current directory.</span></span> <span data-ttu-id="898e0-124">En tant qu’entrée, elle utilise hello **wasb://example/data/gutenberg/davinci.txt** document et la sortie est stocké au niveau : **wasb : / / / exemple/données/WordCountOutput**.</span><span class="sxs-lookup"><span data-stu-id="898e0-124">As input, it uses hello **wasb://example/data/gutenberg/davinci.txt** document, and output is stored at: **wasb:///example/data/WordCountOutput**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="898e0-125">Pour plus d’informations sur ces données d’exemple de travail et hello MapReduce, consultez <a href="hdinsight-use-mapreduce.md">MapReduce utilisation dans HDInsight Hadoop</a>.</span><span class="sxs-lookup"><span data-stu-id="898e0-125">for more information about this MapReduce job and hello example data, see <a href="hdinsight-use-mapreduce.md">Use MapReduce in HDInsight Hadoop</a>.</span></span>
   >
   >
3. <span data-ttu-id="898e0-126">travail de Hello émet des détails comme il est traité, et il retourne des informations similaires qui suivent toohello fois hello terminée :</span><span class="sxs-lookup"><span data-stu-id="898e0-126">hello job emits details as it is processed, and it returns information similar toohello following when hello job is complete:</span></span>

        File Input Format Counters
        Bytes Read=1395666
        File Output Format Counters
        Bytes Written=337623
4. <span data-ttu-id="898e0-127">Lors de la tâche de hello est terminée, utilisez hello suivant des fichiers de sortie commande toolist hello stockés sur **wasb://example/data/WordCountOutput**:</span><span class="sxs-lookup"><span data-stu-id="898e0-127">When hello job is complete, use hello following command toolist hello output files stored at **wasb://example/data/WordCountOutput**:</span></span>

        hadoop fs -ls wasb:///example/data/WordCountOutput

    <span data-ttu-id="898e0-128">Cela devrait afficher deux fichiers, **_SUCCESS** et **part-r-00000**.</span><span class="sxs-lookup"><span data-stu-id="898e0-128">This should display two files, **_SUCCESS** and **part-r-00000**.</span></span> <span data-ttu-id="898e0-129">Hello **partie-r-00000** fichier contient la sortie de hello pour ce travail.</span><span class="sxs-lookup"><span data-stu-id="898e0-129">hello **part-r-00000** file contains hello output for this job.</span></span>

   > [!NOTE]
   > <span data-ttu-id="898e0-130">Certaines tâches MapReduce peuvent fractionner les résultats hello entre plusieurs **partie-r-###** fichiers.</span><span class="sxs-lookup"><span data-stu-id="898e0-130">Some MapReduce jobs may split hello results across multiple **part-r-#####** files.</span></span> <span data-ttu-id="898e0-131">Dans ce cas, utilisez hello ### suffixe d’ordre de hello tooindicate des fichiers de hello.</span><span class="sxs-lookup"><span data-stu-id="898e0-131">If so, use hello ##### suffix tooindicate hello order of hello files.</span></span>
   >
   >
5. <span data-ttu-id="898e0-132">tooview hello de sortie, utilisez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="898e0-132">tooview hello output, use hello following command:</span></span>

        hadoop fs -cat wasb:///example/data/WordCountOutput/part-r-00000

    <span data-ttu-id="898e0-133">Cela affiche une liste de mots hello contenus dans hello **wasb://example/data/gutenberg/davinci.txt** fichier, en même temps que le nombre de hello de chaque mot s’est produite.</span><span class="sxs-lookup"><span data-stu-id="898e0-133">This displays a list of hello words that are contained in hello **wasb://example/data/gutenberg/davinci.txt** file, along with hello number of times each word occured.</span></span> <span data-ttu-id="898e0-134">Hello Voici un exemple de données hello qui seront contenus dans le fichier de hello :</span><span class="sxs-lookup"><span data-stu-id="898e0-134">hello following is an example of hello data that will be contained in hello file:</span></span>

        wreathed        3
        wreathing       1
        wreaths         1
        wrecked         3
        wrenching       1
        wretched        6
        wriggling       1

## <span data-ttu-id="898e0-135"><a id="summary"></a>Résumé</span><span class="sxs-lookup"><span data-stu-id="898e0-135"><a id="summary"></a>Summary</span></span>
<span data-ttu-id="898e0-136">Comme vous pouvez le voir, hello Hadoop commande fournit un moyen simple de toorun tâches MapReduce sur un cluster HDInsight, puis la sortie de travail vue hello.</span><span class="sxs-lookup"><span data-stu-id="898e0-136">As you can see, hello Hadoop command provides an easy way toorun MapReduce jobs on an HDInsight cluster and then view hello job output.</span></span>

## <span data-ttu-id="898e0-137"><a id="nextsteps"></a>Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="898e0-137"><a id="nextsteps"></a>Next steps</span></span>
<span data-ttu-id="898e0-138">Pour obtenir des informations générales sur les tâches MapReduce dans HDInsight :</span><span class="sxs-lookup"><span data-stu-id="898e0-138">For general information about MapReduce jobs in HDInsight:</span></span>

* [<span data-ttu-id="898e0-139">Utilisation de MapReduce dans Hadoop HDInsight</span><span class="sxs-lookup"><span data-stu-id="898e0-139">Use MapReduce on HDInsight Hadoop</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="898e0-140">Pour plus d’informations sur d’autres méthodes de travail avec Hadoop sur HDInsight :</span><span class="sxs-lookup"><span data-stu-id="898e0-140">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="898e0-141">Utilisation de Hive avec Hadoop sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="898e0-141">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="898e0-142">Utilisation de Pig avec Hadoop sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="898e0-142">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
