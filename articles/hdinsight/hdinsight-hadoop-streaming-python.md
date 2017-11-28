---
title: travaux de Python MapReduce de diffusion en continu aaaDevelop hdinsight - Azure | Documents Microsoft
description: "Découvrez comment toouse Python dans les tâches MapReduce de diffusion en continu. Hadoop fournit une API de diffusion en continu pour MapReduce pour l’écriture dans des langages autres que Java."
services: hdinsight
keyword: mapreduce python,python map reduce,python mapreduce
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 7631d8d9-98ae-42ec-b9ec-ee3cf7e57fb3
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: a6ae3ba650b665ecc5839a4ddf5282f8ccfb6bd6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="develop-python-streaming-mapreduce-programs-for-hdinsight"></a><span data-ttu-id="7bb26-104">Développer des programmes MapReduce de diffusion en continu Python pour HDInsight</span><span class="sxs-lookup"><span data-stu-id="7bb26-104">Develop Python streaming MapReduce programs for HDInsight</span></span>

<span data-ttu-id="7bb26-105">Découvrez comment toouse Python dans les opérations MapReduce de diffusion en continu.</span><span class="sxs-lookup"><span data-stu-id="7bb26-105">Learn how toouse Python in streaming MapReduce operations.</span></span> <span data-ttu-id="7bb26-106">Hadoop fournit une API de diffusion en continu pour MapReduce qui permet de vous mappez toowrite et réduire les fonctions dans les langages autres que Java.</span><span class="sxs-lookup"><span data-stu-id="7bb26-106">Hadoop provides a streaming API for MapReduce that enables you toowrite map and reduce functions in languages other than Java.</span></span> <span data-ttu-id="7bb26-107">Bonjour étapes de ce document implémentent hello carte et réduisent les composants de Python.</span><span class="sxs-lookup"><span data-stu-id="7bb26-107">hello steps in this document implement hello Map and Reduce components in Python.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7bb26-108">Composants requis</span><span class="sxs-lookup"><span data-stu-id="7bb26-108">Prerequisites</span></span>

* <span data-ttu-id="7bb26-109">Un cluster Hadoop Linux sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="7bb26-109">A Linux-based Hadoop on HDInsight cluster</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="7bb26-110">étapes de Hello dans ce document nécessitent un cluster HDInsight qui utilise Linux.</span><span class="sxs-lookup"><span data-stu-id="7bb26-110">hello steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="7bb26-111">Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure.</span><span class="sxs-lookup"><span data-stu-id="7bb26-111">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="7bb26-112">Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="7bb26-112">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="7bb26-113">Un éditeur de texte</span><span class="sxs-lookup"><span data-stu-id="7bb26-113">A text editor</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="7bb26-114">éditeur de texte Hello doit utiliser LF comme fin de ligne hello.</span><span class="sxs-lookup"><span data-stu-id="7bb26-114">hello text editor must use LF as hello line ending.</span></span> <span data-ttu-id="7bb26-115">À l’aide d’une fin de ligne de CRLF provoque des erreurs lors de l’exécution du travail MapReduce de hello sur les clusters HDInsight de basés sur Linux.</span><span class="sxs-lookup"><span data-stu-id="7bb26-115">Using a line ending of CRLF causes errors when running hello MapReduce job on Linux-based HDInsight clusters.</span></span>

* <span data-ttu-id="7bb26-116">Hello `ssh` et `scp` commandes, ou [Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview?view=azurermps-3.8.0)</span><span class="sxs-lookup"><span data-stu-id="7bb26-116">hello `ssh` and `scp` commands, or [Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview?view=azurermps-3.8.0)</span></span>

## <a name="word-count"></a><span data-ttu-id="7bb26-117">Nombre de mots</span><span class="sxs-lookup"><span data-stu-id="7bb26-117">Word count</span></span>

<span data-ttu-id="7bb26-118">Cet exemple illustre un nombre de mots de base dans un mappeur et un réducteur Python.</span><span class="sxs-lookup"><span data-stu-id="7bb26-118">This example is a basic word count implemented in a python a mapper and reducer.</span></span> <span data-ttu-id="7bb26-119">le Mappeur Hello sauts de phrases en mots individuels et réducteur de hello agrège les mots hello et nombres de sortie de hello tooproduce.</span><span class="sxs-lookup"><span data-stu-id="7bb26-119">hello mapper breaks sentences into individual words, and hello reducer aggregates hello words and counts tooproduce hello output.</span></span>

<span data-ttu-id="7bb26-120">Hello suivant organigramme illustre ce qui se produit lors du mappage de hello et réduire les phases.</span><span class="sxs-lookup"><span data-stu-id="7bb26-120">hello following flowchart illustrates what happens during hello map and reduce phases.</span></span>

![illustration du processus de mapreduce hello](./media/hdinsight-hadoop-streaming-python/HDI.WordCountDiagram.png)

## <a name="streaming-mapreduce"></a><span data-ttu-id="7bb26-122">Diffusion en continu de MapReduce</span><span class="sxs-lookup"><span data-stu-id="7bb26-122">Streaming MapReduce</span></span>

<span data-ttu-id="7bb26-123">Hadoop vous permet de toospecify un fichier qui contient le mappage de hello et réduire la logique utilisée par une tâche.</span><span class="sxs-lookup"><span data-stu-id="7bb26-123">Hadoop allows you toospecify a file that contains hello map and reduce logic that is used by a job.</span></span> <span data-ttu-id="7bb26-124">exigences spécifiques Hello hello mapper et réduire logique sont :</span><span class="sxs-lookup"><span data-stu-id="7bb26-124">hello specific requirements for hello map and reduce logic are:</span></span>

* <span data-ttu-id="7bb26-125">**D’entrée**: hello de mappage et de réduire les composants doivent lire les données d’entrée de STDIN.</span><span class="sxs-lookup"><span data-stu-id="7bb26-125">**Input**: hello map and reduce components must read input data from STDIN.</span></span>
* <span data-ttu-id="7bb26-126">**Sortie**: hello de mappage et de réduire les composants doivent écrire tooSTDOUT de données de sortie.</span><span class="sxs-lookup"><span data-stu-id="7bb26-126">**Output**: hello map and reduce components must write output data tooSTDOUT.</span></span>
* <span data-ttu-id="7bb26-127">**Format de données**: données hello consommées et le produit doivent être une paire clé/valeur, séparée par un caractère de tabulation.</span><span class="sxs-lookup"><span data-stu-id="7bb26-127">**Data format**: hello data consumed and produced must be a key/value pair, separated by a tab character.</span></span>

<span data-ttu-id="7bb26-128">Python peut gérer facilement ces exigences à l’aide de hello `sys` tooread de module de STDIN et d’utiliser `print` tooprint tooSTDOUT.</span><span class="sxs-lookup"><span data-stu-id="7bb26-128">Python can easily handle these requirements by using hello `sys` module tooread from STDIN and using `print` tooprint tooSTDOUT.</span></span> <span data-ttu-id="7bb26-129">Hello tâche restante est simplement mise en forme les données de salutation avec un onglet (`\t`) caractère entre hello clé et la valeur.</span><span class="sxs-lookup"><span data-stu-id="7bb26-129">hello remaining task is simply formatting hello data with a tab (`\t`) character between hello key and value.</span></span>

## <a name="create-hello-mapper-and-reducer"></a><span data-ttu-id="7bb26-130">Créer réducteur et le Mappeur hello</span><span class="sxs-lookup"><span data-stu-id="7bb26-130">Create hello mapper and reducer</span></span>

1. <span data-ttu-id="7bb26-131">Créez un fichier nommé `mapper.py` et utilisez hello suivant le code en tant que contenu de hello :</span><span class="sxs-lookup"><span data-stu-id="7bb26-131">Create a file named `mapper.py` and use hello following code as hello content:</span></span>

   ```python
   #!/usr/bin/env python

   # Use hello sys module
   import sys

   # 'file' in this case is STDIN
   def read_input(file):
       # Split each line into words
       for line in file:
           yield line.split()

   def main(separator='\t'):
       # Read hello data using read_input
       data = read_input(sys.stdin)
       # Process each word returned from read_input
       for words in data:
           # Process each word
           for word in words:
               # Write tooSTDOUT
               print '%s%s%d' % (word, separator, 1)

   if __name__ == "__main__":
       main()
   ```

2. <span data-ttu-id="7bb26-132">Créez un fichier nommé **reducer.py** et utilisez hello suivant le code en tant que contenu de hello :</span><span class="sxs-lookup"><span data-stu-id="7bb26-132">Create a file named **reducer.py** and use hello following code as hello content:</span></span>

   ```python
   #!/usr/bin/env python

   # import modules
   from itertools import groupby
   from operator import itemgetter
   import sys

   # 'file' in this case is STDIN
   def read_mapper_output(file, separator='\t'):
       # Go through each line
       for line in file:
           # Strip out hello separator character
           yield line.rstrip().split(separator, 1)

   def main(separator='\t'):
       # Read hello data using read_mapper_output
       data = read_mapper_output(sys.stdin, separator=separator)
       # Group words and counts into 'group'
       #   Since MapReduce is a distributed process, each word
       #   may have multiple counts. 'group' will have all counts
       #   which can be retrieved using hello word as hello key.
       for current_word, group in groupby(data, itemgetter(0)):
           try:
               # For each word, pull hello count(s) for hello word
               #   from 'group' and create a total count
               total_count = sum(int(count) for current_word, count in group)
               # Write toostdout
               print "%s%s%d" % (current_word, separator, total_count)
           except ValueError:
               # Count was not a number, so do nothing
               pass

   if __name__ == "__main__":
       main()
   ```

## <a name="run-using-powershell"></a><span data-ttu-id="7bb26-133">Exécuter à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="7bb26-133">Run using PowerShell</span></span>

<span data-ttu-id="7bb26-134">tooensure que vos fichiers ont les fins de ligne droite de hello, hello utilisez PowerShell script suivant :</span><span class="sxs-lookup"><span data-stu-id="7bb26-134">tooensure that your files have hello right line endings, use hello following PowerShell script:</span></span>

[!code-powershell[main](../../powershell_scripts/hdinsight/streaming-python/streaming-python.ps1?range=138-140)]

<span data-ttu-id="7bb26-135">Utilisez hello PowerShell script tooupload hello fichiers suivants, exécuter la tâche de hello et afficher la sortie de hello :</span><span class="sxs-lookup"><span data-stu-id="7bb26-135">Use hello following PowerShell script tooupload hello files, run hello job, and view hello output:</span></span>

[!code-powershell[main](../../powershell_scripts/hdinsight/streaming-python/streaming-python.ps1?range=5-134)]

## <a name="run-from-an-ssh-session"></a><span data-ttu-id="7bb26-136">Exécution à partir d’une session SSH</span><span class="sxs-lookup"><span data-stu-id="7bb26-136">Run from an SSH session</span></span>

1. <span data-ttu-id="7bb26-137">À partir de votre environnement de développement, de hello le même répertoire que `mapper.py` et `reducer.py` fichiers, utilisez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="7bb26-137">From your development environment, in hello same directory as `mapper.py` and `reducer.py` files, use hello following command:</span></span>

    ```bash
    scp mapper.py reducer.py username@clustername-ssh.azurehdinsight.net:
    ```

    <span data-ttu-id="7bb26-138">Remplacez `username` avec le nom d’utilisateur SSH hello pour votre cluster, et `clustername` avec le nom hello de votre cluster.</span><span class="sxs-lookup"><span data-stu-id="7bb26-138">Replace `username` with hello SSH user name for your cluster, and `clustername` with hello name of your cluster.</span></span>

    <span data-ttu-id="7bb26-139">Cette commande copie les fichiers hello à partir du nœud principal du toohello hello système local.</span><span class="sxs-lookup"><span data-stu-id="7bb26-139">This command copies hello files from hello local system toohello head node.</span></span>

    > [!NOTE]
    > <span data-ttu-id="7bb26-140">Si vous avez utilisé un toosecure de mot de passe de votre compte SSH, vous êtes invité pour un mot de passe hello.</span><span class="sxs-lookup"><span data-stu-id="7bb26-140">If you used a password toosecure your SSH account, you are prompted for hello password.</span></span> <span data-ttu-id="7bb26-141">Si vous avez utilisé une clé SSH, vous avez peut-être toouse hello `-i` clé privée des toohello de chemin d’accès au paramètre et hello.</span><span class="sxs-lookup"><span data-stu-id="7bb26-141">If you used an SSH key, you may have toouse hello `-i` parameter and hello path toohello private key.</span></span> <span data-ttu-id="7bb26-142">Par exemple, `scp -i /path/to/private/key mapper.py reducer.py username@clustername-ssh.azurehdinsight.net:`.</span><span class="sxs-lookup"><span data-stu-id="7bb26-142">For example, `scp -i /path/to/private/key mapper.py reducer.py username@clustername-ssh.azurehdinsight.net:`.</span></span>

2. <span data-ttu-id="7bb26-143">Se connecter toohello cluster à l’aide de SSH :</span><span class="sxs-lookup"><span data-stu-id="7bb26-143">Connect toohello cluster by using SSH:</span></span>

    ```bash
    ssh username@clustername-ssh.azurehdinsight.net`
    ```

    <span data-ttu-id="7bb26-144">Pour en savoir plus, consultez [Utilisation de SSH avec HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="7bb26-144">For more information on, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

3. <span data-ttu-id="7bb26-145">REDUCER.py et tooensure hello mapper.py ont hello corriger les fins de ligne, utilisez hello suivant de commandes :</span><span class="sxs-lookup"><span data-stu-id="7bb26-145">tooensure hello mapper.py and reducer.py have hello correct line endings, use hello following commands:</span></span>

    ```bash
    perl -pi -e 's/\r\n/\n/g' mapper.py
    perl -pi -e 's/\r\n/\n/g' reducer.py
    ```

4. <span data-ttu-id="7bb26-146">Utilisez hello suivant la tâche de commande toostart hello MapReduce.</span><span class="sxs-lookup"><span data-stu-id="7bb26-146">Use hello following command toostart hello MapReduce job.</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-streaming.jar -files mapper.py,reducer.py -mapper mapper.py -reducer reducer.py -input /example/data/gutenberg/davinci.txt -output /example/wordcountout
    ```

    <span data-ttu-id="7bb26-147">Cette commande a hello composants suivants :</span><span class="sxs-lookup"><span data-stu-id="7bb26-147">This command has hello following parts:</span></span>

   * <span data-ttu-id="7bb26-148">**hadoop-streaming.jar**: utilisé lors de l’exécution d’opérations de diffusion en contenu MapReduce.</span><span class="sxs-lookup"><span data-stu-id="7bb26-148">**hadoop-streaming.jar**: Used when performing streaming MapReduce operations.</span></span> <span data-ttu-id="7bb26-149">Il interagit Hadoop avec code MapReduce externe hello que vous fournissez.</span><span class="sxs-lookup"><span data-stu-id="7bb26-149">It interfaces Hadoop with hello external MapReduce code you provide.</span></span>

   * <span data-ttu-id="7bb26-150">**-fichiers**: ajoute hello spécifié travail MapReduce de toohello des fichiers.</span><span class="sxs-lookup"><span data-stu-id="7bb26-150">**-files**: Adds hello specified files toohello MapReduce job.</span></span>

   * <span data-ttu-id="7bb26-151">**-Mappeur**: Hadoop indique quel fichier toouse comme hello mappeur.</span><span class="sxs-lookup"><span data-stu-id="7bb26-151">**-mapper**: Tells Hadoop which file toouse as hello mapper.</span></span>

   * <span data-ttu-id="7bb26-152">**-RÉDUCTEUR**: Hadoop indique quel fichier toouse comme hello du réducteur.</span><span class="sxs-lookup"><span data-stu-id="7bb26-152">**-reducer**: Tells Hadoop which file toouse as hello reducer.</span></span>

   * <span data-ttu-id="7bb26-153">**-d’entrée**: fichier d’entrée hello que nous devons compter les mots à partir de.</span><span class="sxs-lookup"><span data-stu-id="7bb26-153">**-input**: hello input file that we should count words from.</span></span>

   * <span data-ttu-id="7bb26-154">**-sortie**: répertoire hello hello de sortie est écrite dans.</span><span class="sxs-lookup"><span data-stu-id="7bb26-154">**-output**: hello directory that hello output is written to.</span></span>

    <span data-ttu-id="7bb26-155">Comme la tâche MapReduce de hello fonctionne, les processus de hello s’affiche sous forme de pourcentages.</span><span class="sxs-lookup"><span data-stu-id="7bb26-155">As hello MapReduce job works, hello process is displayed as percentages.</span></span>

        <span data-ttu-id="7bb26-156">15/02/05 19:01:04 INFO mapreduce.Job:  map 0% reduce 0%    15/02/05 19:01:16 INFO mapreduce.Job:  map 100% reduce 0%    15/02/05 19:01:27 INFO mapreduce.Job:  map 100% reduce 100%</span><span class="sxs-lookup"><span data-stu-id="7bb26-156">15/02/05 19:01:04 INFO mapreduce.Job:  map 0% reduce 0%    15/02/05 19:01:16 INFO mapreduce.Job:  map 100% reduce 0%    15/02/05 19:01:27 INFO mapreduce.Job:  map 100% reduce 100%</span></span>


5. <span data-ttu-id="7bb26-157">tooview hello de sortie, utilisez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="7bb26-157">tooview hello output, use hello following command:</span></span>

    ```bash
    hdfs dfs -text /example/wordcountout/part-00000
    ```

    <span data-ttu-id="7bb26-158">Cette commande affiche une liste de mots et le nombre de fois word de hello s’est produite.</span><span class="sxs-lookup"><span data-stu-id="7bb26-158">This command displays a list of words and how many times hello word occurred.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7bb26-159">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="7bb26-159">Next steps</span></span>

<span data-ttu-id="7bb26-160">Maintenant que vous avez appris comment toouse MapRedcue de diffusion en continu des travaux avec HDInsight, utilisez hello suivant les liens tooexplore autres toowork manières avec Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7bb26-160">Now that you have learned how toouse streaming MapRedcue jobs with HDInsight, use hello following links tooexplore other ways toowork with Azure HDInsight.</span></span>

* [<span data-ttu-id="7bb26-161">Utilisation de Hive avec HDInsight</span><span class="sxs-lookup"><span data-stu-id="7bb26-161">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="7bb26-162">Utilisation de Pig avec HDInsight</span><span class="sxs-lookup"><span data-stu-id="7bb26-162">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="7bb26-163">Utilisation des tâches MapReduce avec HDInsight</span><span class="sxs-lookup"><span data-stu-id="7bb26-163">Use MapReduce jobs with HDInsight</span></span>](hdinsight-use-mapreduce.md)
