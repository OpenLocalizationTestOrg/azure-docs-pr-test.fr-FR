---
title: aaaMapReduce et la connexion SSH avec Hadoop dans HDInsight - Azure | Documents Microsoft
description: "Découvrez comment toouse SSH toorun MapReduce travaux à l’aide de Hadoop dans HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 844678ba-1e1f-4fda-b9ef-34df4035d547
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: 9626577687fc5cc119a39d65a9c45298f57f81c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-mapreduce-with-hadoop-on-hdinsight-with-ssh"></a><span data-ttu-id="94294-103">Utilisation de MapReduce avec Hadoop sur HDInsight avec SSH</span><span class="sxs-lookup"><span data-stu-id="94294-103">Use MapReduce with Hadoop on HDInsight with SSH</span></span>

[!INCLUDE [mapreduce-selector](../../includes/hdinsight-selector-use-mapreduce.md)]

<span data-ttu-id="94294-104">Découvrez comment toosubmit MapReduce travaux à partir d’un tooHDInsight de connexion Secure Shell (SSH).</span><span class="sxs-lookup"><span data-stu-id="94294-104">Learn how toosubmit MapReduce jobs from a Secure Shell (SSH) connection tooHDInsight.</span></span>

> [!NOTE]
> <span data-ttu-id="94294-105">Si vous êtes déjà familiarisé avec Hadoop basé sur Linux à l’aide de serveurs, mais vous tooHDInsight nouvelle, consultez [HDInsight de basés sur Linux conseils](hdinsight-hadoop-linux-information.md).</span><span class="sxs-lookup"><span data-stu-id="94294-105">If you are already familiar with using Linux-based Hadoop servers, but you are new tooHDInsight, see [Linux-based HDInsight tips](hdinsight-hadoop-linux-information.md).</span></span>

## <span data-ttu-id="94294-106"><a id="prereq"></a>Configuration requise</span><span class="sxs-lookup"><span data-stu-id="94294-106"><a id="prereq"></a>Prerequisites</span></span>

* <span data-ttu-id="94294-107">un cluster HDInsight basé sur Linux (Hadoop sur HDInsight)</span><span class="sxs-lookup"><span data-stu-id="94294-107">A Linux-based HDInsight (Hadoop on HDInsight) cluster</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="94294-108">Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure.</span><span class="sxs-lookup"><span data-stu-id="94294-108">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="94294-109">Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="94294-109">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="94294-110">Un client SSH.</span><span class="sxs-lookup"><span data-stu-id="94294-110">An SSH client.</span></span> <span data-ttu-id="94294-111">Pour en savoir plus, consultez [Utilisation de SSH avec HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="94294-111">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md)</span></span>

## <span data-ttu-id="94294-112"><a id="ssh"></a>Connexion avec SSH</span><span class="sxs-lookup"><span data-stu-id="94294-112"><a id="ssh"></a>Connect with SSH</span></span>

<span data-ttu-id="94294-113">Connectez le cluster toohello à l’aide de SSH.</span><span class="sxs-lookup"><span data-stu-id="94294-113">Connect toohello cluster using SSH.</span></span> <span data-ttu-id="94294-114">Par exemple, hello commande suivante connecte à cluster tooa nommé **myhdinsight**:</span><span class="sxs-lookup"><span data-stu-id="94294-114">For example, hello following command connects tooa cluster named **myhdinsight**:</span></span>

```bash
ssh admin@myhdinsight-ssh.azurehdinsight.net
```

<span data-ttu-id="94294-115">**Si vous utilisez un certificat de clé pour l’authentification SSH**, vous devrez peut-être emplacement de hello toospecify de clé privée de hello sur votre système client, par exemple :</span><span class="sxs-lookup"><span data-stu-id="94294-115">**If you use a certificate key for SSH authentication**, you may need toospecify hello location of hello private key on your client system, for example:</span></span>

```bash
ssh -i ~/mykey.key admin@myhdinsight-ssh.azurehdinsight.net
```

<span data-ttu-id="94294-116">**Si vous utilisez un mot de passe pour l’authentification SSH**, vous devez tooprovide hello un mot de passe lorsque vous y êtes invité.</span><span class="sxs-lookup"><span data-stu-id="94294-116">**If you use a password for SSH authentication**, you need tooprovide hello password when prompted.</span></span>

<span data-ttu-id="94294-117">Pour en savoir plus sur l’utilisation de SSH avec HDInsight, voir [Utilisation de SSH avec HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="94294-117">For more information on using SSH with HDInsight, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <span data-ttu-id="94294-118"><a id="hadoop"></a>Utilisation de commandes Hadoop</span><span class="sxs-lookup"><span data-stu-id="94294-118"><a id="hadoop"></a>Use Hadoop commands</span></span>

1. <span data-ttu-id="94294-119">Après que vous être connecté toohello HDInsight cluster, utilisez hello suivant commande toostart une tâche MapReduce :</span><span class="sxs-lookup"><span data-stu-id="94294-119">After you are connected toohello HDInsight cluster, use hello following command toostart a MapReduce job:</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount /example/data/gutenberg/davinci.txt /example/data/WordCountOutput
    ```

    <span data-ttu-id="94294-120">Cette commande démarre hello `wordcount` (classe), qui est contenue dans hello `hadoop-mapreduce-examples.jar` fichier.</span><span class="sxs-lookup"><span data-stu-id="94294-120">This command starts hello `wordcount` class, which is contained in hello `hadoop-mapreduce-examples.jar` file.</span></span> <span data-ttu-id="94294-121">Il utilise hello `/example/data/gutenberg/davinci.txt` document comme entrée et de sortie est stockée au niveau `/example/data/WordCountOutput`.</span><span class="sxs-lookup"><span data-stu-id="94294-121">It uses hello `/example/data/gutenberg/davinci.txt` document as input, and output is stored at `/example/data/WordCountOutput`.</span></span>

    > [!NOTE]
    > <span data-ttu-id="94294-122">Pour plus d’informations sur ces données d’exemple de travail et hello MapReduce, consultez [MapReduce utilisation dans Hadoop dans HDInsight](hdinsight-use-mapreduce.md).</span><span class="sxs-lookup"><span data-stu-id="94294-122">For more information about this MapReduce job and hello example data, see [Use MapReduce in Hadoop on HDInsight](hdinsight-use-mapreduce.md).</span></span>

2. <span data-ttu-id="94294-123">travail de Hello émet des détails comme il traite et il retourne des informations toohello similaire après le texte hello travail une fois :</span><span class="sxs-lookup"><span data-stu-id="94294-123">hello job emits details as it processes, and it returns information similar toohello following text when hello job completes:</span></span>

        File Input Format Counters
        Bytes Read=1395666
        File Output Format Counters
        Bytes Written=337623

3. <span data-ttu-id="94294-124">Lors de la tâche de hello est terminée, utilisez hello fichiers de sortie de commande toolist hello suivants :</span><span class="sxs-lookup"><span data-stu-id="94294-124">When hello job completes, use hello following command toolist hello output files:</span></span>

    ```bash
    hdfs dfs -ls /example/data/WordCountOutput
    ```

    <span data-ttu-id="94294-125">Cette commande affiche deux fichiers, `_SUCCESS` et `part-r-00000`.</span><span class="sxs-lookup"><span data-stu-id="94294-125">This command display two files, `_SUCCESS` and `part-r-00000`.</span></span> <span data-ttu-id="94294-126">Hello `part-r-00000` fichier contient la sortie de hello pour ce travail.</span><span class="sxs-lookup"><span data-stu-id="94294-126">hello `part-r-00000` file contains hello output for this job.</span></span>

    > [!NOTE]
    > <span data-ttu-id="94294-127">Certaines tâches MapReduce peuvent fractionner les résultats hello entre plusieurs **partie-r-###** fichiers.</span><span class="sxs-lookup"><span data-stu-id="94294-127">Some MapReduce jobs may split hello results across multiple **part-r-#####** files.</span></span> <span data-ttu-id="94294-128">Dans ce cas, utilisez hello ### suffixe d’ordre de hello tooindicate des fichiers de hello.</span><span class="sxs-lookup"><span data-stu-id="94294-128">If so, use hello ##### suffix tooindicate hello order of hello files.</span></span>

4. <span data-ttu-id="94294-129">tooview hello de sortie, utilisez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="94294-129">tooview hello output, use hello following command:</span></span>

    ```bash
    hdfs dfs -cat /example/data/WordCountOutput/part-r-00000
    ```

    <span data-ttu-id="94294-130">Cette commande affiche une liste de mots hello contenus Bonjour **wasb://example/data/gutenberg/davinci.txt** hello de fichiers et de nombre de fois où chaque mot s’est produite.</span><span class="sxs-lookup"><span data-stu-id="94294-130">This command displays a list of hello words that are contained in hello **wasb://example/data/gutenberg/davinci.txt** file and hello number of times each word occurred.</span></span> <span data-ttu-id="94294-131">Hello texte suivant est un exemple de données hello contenues dans le fichier de hello :</span><span class="sxs-lookup"><span data-stu-id="94294-131">hello following text is an example of hello data that is contained in hello file:</span></span>

        wreathed        3
        wreathing       1
        wreaths         1
        wrecked         3
        wrenching       1
        wretched        6
        wriggling       1

## <span data-ttu-id="94294-132"><a id="summary"></a>Résumé</span><span class="sxs-lookup"><span data-stu-id="94294-132"><a id="summary"></a>Summary</span></span>

<span data-ttu-id="94294-133">Comme vous pouvez le voir, les commandes de Hadoop fournissent un moyen simple de toorun tâches MapReduce dans un cluster HDInsight, puis la sortie de travail vue hello.</span><span class="sxs-lookup"><span data-stu-id="94294-133">As you can see, Hadoop commands provide an easy way toorun MapReduce jobs in an HDInsight cluster and then view hello job output.</span></span>

## <span data-ttu-id="94294-134"><a id="nextsteps"></a>Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="94294-134"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="94294-135">Pour obtenir des informations générales sur les tâches MapReduce dans HDInsight :</span><span class="sxs-lookup"><span data-stu-id="94294-135">For general information about MapReduce jobs in HDInsight:</span></span>

* [<span data-ttu-id="94294-136">Utilisation de MapReduce dans Hadoop HDInsight</span><span class="sxs-lookup"><span data-stu-id="94294-136">Use MapReduce on HDInsight Hadoop</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="94294-137">Pour plus d’informations sur d’autres méthodes de travail avec Hadoop sur HDInsight :</span><span class="sxs-lookup"><span data-stu-id="94294-137">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="94294-138">Utilisation de Hive avec Hadoop sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="94294-138">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="94294-139">Utilisation de Pig avec Hadoop sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="94294-139">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
