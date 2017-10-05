---
title: MapReduce et la connexion SSH avec Hadoop dans HDInsight - Azure | Documents Microsoft
description: "Apprenez à utiliser le protocole SSH pour exécuter des tâches MapReduce avec Hadoop sur HDInsight."
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
ms.openlocfilehash: eaf6278f97cd5ddd7e049ff4745181f39d7949a0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="use-mapreduce-with-hadoop-on-hdinsight-with-ssh"></a><span data-ttu-id="d9f56-103">Utilisation de MapReduce avec Hadoop sur HDInsight avec SSH</span><span class="sxs-lookup"><span data-stu-id="d9f56-103">Use MapReduce with Hadoop on HDInsight with SSH</span></span>

[!INCLUDE [mapreduce-selector](../../includes/hdinsight-selector-use-mapreduce.md)]

<span data-ttu-id="d9f56-104">Découvrez comment soumettre des tâches MapReduce à partir d’une connexion SSH (Secure Shell) vers HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d9f56-104">Learn how to submit MapReduce jobs from a Secure Shell (SSH) connection to HDInsight.</span></span>

> [!NOTE]
> <span data-ttu-id="d9f56-105">Si vous êtes déjà familiarisé avec l’utilisation de serveurs Hadoop sur Linux, mais pas avec HDInsight, consultez la rubrique [Informations sur l’utilisation de HDInsight sur Linux](hdinsight-hadoop-linux-information.md).</span><span class="sxs-lookup"><span data-stu-id="d9f56-105">If you are already familiar with using Linux-based Hadoop servers, but you are new to HDInsight, see [Linux-based HDInsight tips](hdinsight-hadoop-linux-information.md).</span></span>

## <span data-ttu-id="d9f56-106"><a id="prereq"></a>Configuration requise</span><span class="sxs-lookup"><span data-stu-id="d9f56-106"><a id="prereq"></a>Prerequisites</span></span>

* <span data-ttu-id="d9f56-107">un cluster HDInsight basé sur Linux (Hadoop sur HDInsight)</span><span class="sxs-lookup"><span data-stu-id="d9f56-107">A Linux-based HDInsight (Hadoop on HDInsight) cluster</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="d9f56-108">Linux est le seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure.</span><span class="sxs-lookup"><span data-stu-id="d9f56-108">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="d9f56-109">Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="d9f56-109">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="d9f56-110">Un client SSH.</span><span class="sxs-lookup"><span data-stu-id="d9f56-110">An SSH client.</span></span> <span data-ttu-id="d9f56-111">Pour en savoir plus, consultez [Utilisation de SSH avec HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="d9f56-111">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md)</span></span>

## <span data-ttu-id="d9f56-112"><a id="ssh"></a>Connexion avec SSH</span><span class="sxs-lookup"><span data-stu-id="d9f56-112"><a id="ssh"></a>Connect with SSH</span></span>

<span data-ttu-id="d9f56-113">Connectez-vous au cluster à l'aide de SSH.</span><span class="sxs-lookup"><span data-stu-id="d9f56-113">Connect to the cluster using SSH.</span></span> <span data-ttu-id="d9f56-114">Par exemple, la commande suivante permet de se connecter à un cluster nommé **myhdinsight** :</span><span class="sxs-lookup"><span data-stu-id="d9f56-114">For example, the following command connects to a cluster named **myhdinsight**:</span></span>

```bash
ssh admin@myhdinsight-ssh.azurehdinsight.net
```

<span data-ttu-id="d9f56-115">**Si vous utilisez une clé de certificat pour l’authentification SSH** vous devrez peut-être spécifier l’emplacement de la clé privée sur votre système client, par exemple :</span><span class="sxs-lookup"><span data-stu-id="d9f56-115">**If you use a certificate key for SSH authentication**, you may need to specify the location of the private key on your client system, for example:</span></span>

```bash
ssh -i ~/mykey.key admin@myhdinsight-ssh.azurehdinsight.net
```

<span data-ttu-id="d9f56-116">**Si vous utilisez un mot de passe pour l’authentification SSH**, vous devez fournir le mot de passe lorsque vous y êtes invité.</span><span class="sxs-lookup"><span data-stu-id="d9f56-116">**If you use a password for SSH authentication**, you need to provide the password when prompted.</span></span>

<span data-ttu-id="d9f56-117">Pour en savoir plus sur l’utilisation de SSH avec HDInsight, voir [Utilisation de SSH avec HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="d9f56-117">For more information on using SSH with HDInsight, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <span data-ttu-id="d9f56-118"><a id="hadoop"></a>Utilisation de commandes Hadoop</span><span class="sxs-lookup"><span data-stu-id="d9f56-118"><a id="hadoop"></a>Use Hadoop commands</span></span>

1. <span data-ttu-id="d9f56-119">Une fois connecté au cluster HDInsight, utilisez la commande suivante pour lancer une tâche MapReduce :</span><span class="sxs-lookup"><span data-stu-id="d9f56-119">After you are connected to the HDInsight cluster, use the following command to start a MapReduce job:</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount /example/data/gutenberg/davinci.txt /example/data/WordCountOutput
    ```

    <span data-ttu-id="d9f56-120">Cette commande démarre la classe `wordcount`, qui est contenue dans le fichier `hadoop-mapreduce-examples.jar`.</span><span class="sxs-lookup"><span data-stu-id="d9f56-120">This command starts the `wordcount` class, which is contained in the `hadoop-mapreduce-examples.jar` file.</span></span> <span data-ttu-id="d9f56-121">Il utilise le document `/example/data/gutenberg/davinci.txt` comme entrée. La sortie est stockée dans `/example/data/WordCountOutput`.</span><span class="sxs-lookup"><span data-stu-id="d9f56-121">It uses the `/example/data/gutenberg/davinci.txt` document as input, and output is stored at `/example/data/WordCountOutput`.</span></span>

    > [!NOTE]
    > <span data-ttu-id="d9f56-122">Pour plus d’informations sur cette tâche MapReduce et sur les exemples de données, consultez la rubrique [Utilisation de MapReduce dans Hadoop sur HDInsight](hdinsight-use-mapreduce.md).</span><span class="sxs-lookup"><span data-stu-id="d9f56-122">For more information about this MapReduce job and the example data, see [Use MapReduce in Hadoop on HDInsight](hdinsight-use-mapreduce.md).</span></span>

2. <span data-ttu-id="d9f56-123">La tâche émet des informations lors de son traitement, avant de renvoyer des informations semblables au texte suivant lorsqu’elle est terminée :</span><span class="sxs-lookup"><span data-stu-id="d9f56-123">The job emits details as it processes, and it returns information similar to the following text when the job completes:</span></span>

        File Input Format Counters
        Bytes Read=1395666
        File Output Format Counters
        Bytes Written=337623

3. <span data-ttu-id="d9f56-124">Une fois la tâche terminée, utilisez la commande suivante pour afficher les fichiers sortants :</span><span class="sxs-lookup"><span data-stu-id="d9f56-124">When the job completes, use the following command to list the output files:</span></span>

    ```bash
    hdfs dfs -ls /example/data/WordCountOutput
    ```

    <span data-ttu-id="d9f56-125">Cette commande affiche deux fichiers, `_SUCCESS` et `part-r-00000`.</span><span class="sxs-lookup"><span data-stu-id="d9f56-125">This command display two files, `_SUCCESS` and `part-r-00000`.</span></span> <span data-ttu-id="d9f56-126">Le fichier `part-r-00000` contient le résultat pour cette tâche.</span><span class="sxs-lookup"><span data-stu-id="d9f56-126">The `part-r-00000` file contains the output for this job.</span></span>

    > [!NOTE]
    > <span data-ttu-id="d9f56-127">Certaines tâches MapReduce peuvent fractionner les résultats sur plusieurs fichiers **part-r-#####** .</span><span class="sxs-lookup"><span data-stu-id="d9f56-127">Some MapReduce jobs may split the results across multiple **part-r-#####** files.</span></span> <span data-ttu-id="d9f56-128">Dans ce cas, utilisez le suffixe ##### pour indiquer l’ordre des fichiers.</span><span class="sxs-lookup"><span data-stu-id="d9f56-128">If so, use the ##### suffix to indicate the order of the files.</span></span>

4. <span data-ttu-id="d9f56-129">Pour afficher la sortie, utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="d9f56-129">To view the output, use the following command:</span></span>

    ```bash
    hdfs dfs -cat /example/data/WordCountOutput/part-r-00000
    ```

    <span data-ttu-id="d9f56-130">Cette commande affiche une liste des mots contenus dans le fichier **wasb://example/data/gutenberg/davinci.txt**, ainsi que le nombre d’occurrences de chaque mot.</span><span class="sxs-lookup"><span data-stu-id="d9f56-130">This command displays a list of the words that are contained in the **wasb://example/data/gutenberg/davinci.txt** file and the number of times each word occurred.</span></span> <span data-ttu-id="d9f56-131">Le texte suivant est un exemple des données contenues dans le fichier :</span><span class="sxs-lookup"><span data-stu-id="d9f56-131">The following text is an example of the data that is contained in the file:</span></span>

        wreathed        3
        wreathing       1
        wreaths         1
        wrecked         3
        wrenching       1
        wretched        6
        wriggling       1

## <span data-ttu-id="d9f56-132"><a id="summary"></a>Résumé</span><span class="sxs-lookup"><span data-stu-id="d9f56-132"><a id="summary"></a>Summary</span></span>

<span data-ttu-id="d9f56-133">Comme vous pouvez le voir, les commandes Hadoop fournissent un moyen facile pour exécuter des tâches MapReduce sur un cluster HDInsight avant d’afficher le résultat de la tâche.</span><span class="sxs-lookup"><span data-stu-id="d9f56-133">As you can see, Hadoop commands provide an easy way to run MapReduce jobs in an HDInsight cluster and then view the job output.</span></span>

## <span data-ttu-id="d9f56-134"><a id="nextsteps"></a>Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d9f56-134"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="d9f56-135">Pour obtenir des informations générales sur les tâches MapReduce dans HDInsight :</span><span class="sxs-lookup"><span data-stu-id="d9f56-135">For general information about MapReduce jobs in HDInsight:</span></span>

* [<span data-ttu-id="d9f56-136">Utilisation de MapReduce dans Hadoop HDInsight</span><span class="sxs-lookup"><span data-stu-id="d9f56-136">Use MapReduce on HDInsight Hadoop</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="d9f56-137">Pour plus d’informations sur d’autres méthodes de travail avec Hadoop sur HDInsight :</span><span class="sxs-lookup"><span data-stu-id="d9f56-137">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="d9f56-138">Utilisation de Hive avec Hadoop sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="d9f56-138">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="d9f56-139">Utilisation de Pig avec Hadoop sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="d9f56-139">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
