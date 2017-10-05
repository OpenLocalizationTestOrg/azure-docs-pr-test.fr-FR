---
title: "Développer des travaux MapReduce de diffusion en continu Python avec HDInsight - Azure | Documents Microsoft"
description: "Découvrez comment utiliser Python dans des travaux MapReduce de diffusion en continu. Hadoop fournit une API de diffusion en continu pour MapReduce pour l’écriture dans des langages autres que Java."
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
ms.openlocfilehash: b86605c49291a99f49c4b2841d46324cfd0db56d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="develop-python-streaming-mapreduce-programs-for-hdinsight"></a><span data-ttu-id="5dd31-104">Développer des programmes MapReduce de diffusion en continu Python pour HDInsight</span><span class="sxs-lookup"><span data-stu-id="5dd31-104">Develop Python streaming MapReduce programs for HDInsight</span></span>

<span data-ttu-id="5dd31-105">Découvrez comment utiliser Python dans des opérations MapReduce de diffusion en continu.</span><span class="sxs-lookup"><span data-stu-id="5dd31-105">Learn how to use Python in streaming MapReduce operations.</span></span> <span data-ttu-id="5dd31-106">Hadoop fournit une API de diffusion en continu pour MapReduce qui vous permet d'écrire des fonctions de mappage et de réduction dans d'autres langages que Java.</span><span class="sxs-lookup"><span data-stu-id="5dd31-106">Hadoop provides a streaming API for MapReduce that enables you to write map and reduce functions in languages other than Java.</span></span> <span data-ttu-id="5dd31-107">Les étapes décrites dans ce document implémentent les composants de mappage et de réduction dans Python.</span><span class="sxs-lookup"><span data-stu-id="5dd31-107">The steps in this document implement the Map and Reduce components in Python.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5dd31-108">Composants requis</span><span class="sxs-lookup"><span data-stu-id="5dd31-108">Prerequisites</span></span>

* <span data-ttu-id="5dd31-109">Un cluster Hadoop Linux sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="5dd31-109">A Linux-based Hadoop on HDInsight cluster</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="5dd31-110">Les étapes décrites dans ce document nécessitent un cluster HDInsight utilisant Linux.</span><span class="sxs-lookup"><span data-stu-id="5dd31-110">The steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="5dd31-111">Linux est le seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure.</span><span class="sxs-lookup"><span data-stu-id="5dd31-111">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="5dd31-112">Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="5dd31-112">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="5dd31-113">Un éditeur de texte</span><span class="sxs-lookup"><span data-stu-id="5dd31-113">A text editor</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="5dd31-114">L’éditeur de texte doit utiliser LF comme caractère de fin de ligne.</span><span class="sxs-lookup"><span data-stu-id="5dd31-114">The text editor must use LF as the line ending.</span></span> <span data-ttu-id="5dd31-115">L’utilisation d’une fin de ligne du CRLF génère des erreurs lors de l’exécution de la tâche MapReduce dans les clusters HDInsight sous Linux.</span><span class="sxs-lookup"><span data-stu-id="5dd31-115">Using a line ending of CRLF causes errors when running the MapReduce job on Linux-based HDInsight clusters.</span></span>

* <span data-ttu-id="5dd31-116">Les commandes `ssh` et `scp` ou [Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview?view=azurermps-3.8.0)</span><span class="sxs-lookup"><span data-stu-id="5dd31-116">The `ssh` and `scp` commands, or [Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview?view=azurermps-3.8.0)</span></span>

## <a name="word-count"></a><span data-ttu-id="5dd31-117">Nombre de mots</span><span class="sxs-lookup"><span data-stu-id="5dd31-117">Word count</span></span>

<span data-ttu-id="5dd31-118">Cet exemple illustre un nombre de mots de base dans un mappeur et un réducteur Python.</span><span class="sxs-lookup"><span data-stu-id="5dd31-118">This example is a basic word count implemented in a python a mapper and reducer.</span></span> <span data-ttu-id="5dd31-119">Le mappeur sépare les phrases en mots individuels, et le raccord de réduction rassemble les mots et les nombres pour produire la sortie.</span><span class="sxs-lookup"><span data-stu-id="5dd31-119">The mapper breaks sentences into individual words, and the reducer aggregates the words and counts to produce the output.</span></span>

<span data-ttu-id="5dd31-120">L’organigramme suivant illustre ce qui se passe durant les phases de mappage et de réduction.</span><span class="sxs-lookup"><span data-stu-id="5dd31-120">The following flowchart illustrates what happens during the map and reduce phases.</span></span>

![illustration du processus mapreduce](./media/hdinsight-hadoop-streaming-python/HDI.WordCountDiagram.png)

## <a name="streaming-mapreduce"></a><span data-ttu-id="5dd31-122">Diffusion en continu de MapReduce</span><span class="sxs-lookup"><span data-stu-id="5dd31-122">Streaming MapReduce</span></span>

<span data-ttu-id="5dd31-123">Hadoop vous permet de spécifier un fichier qui dispose de la logique de mappage et de réduction utilisée par un travail.</span><span class="sxs-lookup"><span data-stu-id="5dd31-123">Hadoop allows you to specify a file that contains the map and reduce logic that is used by a job.</span></span> <span data-ttu-id="5dd31-124">Parmi les exigences spécifiques de mappage et de réduction, on retrouve les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="5dd31-124">The specific requirements for the map and reduce logic are:</span></span>

* <span data-ttu-id="5dd31-125">**Entrée**: les composants de mappage et de réduction doivent lire les données d’entrée depuis STDIN.</span><span class="sxs-lookup"><span data-stu-id="5dd31-125">**Input**: The map and reduce components must read input data from STDIN.</span></span>
* <span data-ttu-id="5dd31-126">**Sortie**: les composants de mappage et de réduction doivent écrire les données de sortie vers STDOUT.</span><span class="sxs-lookup"><span data-stu-id="5dd31-126">**Output**: The map and reduce components must write output data to STDOUT.</span></span>
* <span data-ttu-id="5dd31-127">**Format de données**: les données consommées et produites doivent représenter une paire clé/valeur, séparée par un caractère de tabulation.</span><span class="sxs-lookup"><span data-stu-id="5dd31-127">**Data format**: The data consumed and produced must be a key/value pair, separated by a tab character.</span></span>

<span data-ttu-id="5dd31-128">Python peut facilement gérer ces exigences en utilisant le module `sys` pour lire depuis STDIN et utiliser `print` pour imprimer vers STDOUT.</span><span class="sxs-lookup"><span data-stu-id="5dd31-128">Python can easily handle these requirements by using the `sys` module to read from STDIN and using `print` to print to STDOUT.</span></span> <span data-ttu-id="5dd31-129">Le travail restant consiste à disposer un caractère de tabulation (`\t`) entre la clé et la valeur pour vous permettre d’effectuer, si vous le souhaitez, le formatage de ces données.</span><span class="sxs-lookup"><span data-stu-id="5dd31-129">The remaining task is simply formatting the data with a tab (`\t`) character between the key and value.</span></span>

## <a name="create-the-mapper-and-reducer"></a><span data-ttu-id="5dd31-130">Création du mappeur et du raccord de réduction</span><span class="sxs-lookup"><span data-stu-id="5dd31-130">Create the mapper and reducer</span></span>

1. <span data-ttu-id="5dd31-131">Créez un fichier nommé `mapper.py` et utilisez le code suivant comme contenu :</span><span class="sxs-lookup"><span data-stu-id="5dd31-131">Create a file named `mapper.py` and use the following code as the content:</span></span>

   ```python
   #!/usr/bin/env python

   # Use the sys module
   import sys

   # 'file' in this case is STDIN
   def read_input(file):
       # Split each line into words
       for line in file:
           yield line.split()

   def main(separator='\t'):
       # Read the data using read_input
       data = read_input(sys.stdin)
       # Process each word returned from read_input
       for words in data:
           # Process each word
           for word in words:
               # Write to STDOUT
               print '%s%s%d' % (word, separator, 1)

   if __name__ == "__main__":
       main()
   ```

2. <span data-ttu-id="5dd31-132">Créez un fichier nommé **reducer.py** et utilisez le code suivant comme contenu :</span><span class="sxs-lookup"><span data-stu-id="5dd31-132">Create a file named **reducer.py** and use the following code as the content:</span></span>

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
           # Strip out the separator character
           yield line.rstrip().split(separator, 1)

   def main(separator='\t'):
       # Read the data using read_mapper_output
       data = read_mapper_output(sys.stdin, separator=separator)
       # Group words and counts into 'group'
       #   Since MapReduce is a distributed process, each word
       #   may have multiple counts. 'group' will have all counts
       #   which can be retrieved using the word as the key.
       for current_word, group in groupby(data, itemgetter(0)):
           try:
               # For each word, pull the count(s) for the word
               #   from 'group' and create a total count
               total_count = sum(int(count) for current_word, count in group)
               # Write to stdout
               print "%s%s%d" % (current_word, separator, total_count)
           except ValueError:
               # Count was not a number, so do nothing
               pass

   if __name__ == "__main__":
       main()
   ```

## <a name="run-using-powershell"></a><span data-ttu-id="5dd31-133">Exécuter à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="5dd31-133">Run using PowerShell</span></span>

<span data-ttu-id="5dd31-134">Pour vous assurer que vos fichiers ont le droit de modifier les fins de ligne, utilisez le script PowerShell suivant :</span><span class="sxs-lookup"><span data-stu-id="5dd31-134">To ensure that your files have the right line endings, use the following PowerShell script:</span></span>

<span data-ttu-id="5dd31-135">[!code-powershell[main](../../powershell_scripts/hdinsight/streaming-python/streaming-python.ps1?range=138-140)]</span><span class="sxs-lookup"><span data-stu-id="5dd31-135">[!code-powershell[main](../../powershell_scripts/hdinsight/streaming-python/streaming-python.ps1?range=138-140)]</span></span>

<span data-ttu-id="5dd31-136">Utilisez le script PowerShell suivant pour charger les fichiers, exécuter la tâche et afficher le résultat :</span><span class="sxs-lookup"><span data-stu-id="5dd31-136">Use the following PowerShell script to upload the files, run the job, and view the output:</span></span>

<span data-ttu-id="5dd31-137">[!code-powershell[main](../../powershell_scripts/hdinsight/streaming-python/streaming-python.ps1?range=5-134)]</span><span class="sxs-lookup"><span data-stu-id="5dd31-137">[!code-powershell[main](../../powershell_scripts/hdinsight/streaming-python/streaming-python.ps1?range=5-134)]</span></span>

## <a name="run-from-an-ssh-session"></a><span data-ttu-id="5dd31-138">Exécution à partir d’une session SSH</span><span class="sxs-lookup"><span data-stu-id="5dd31-138">Run from an SSH session</span></span>

1. <span data-ttu-id="5dd31-139">À partir de votre environnement de développement, dans le même répertoire que `mapper.py` et `reducer.py`, utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="5dd31-139">From your development environment, in the same directory as `mapper.py` and `reducer.py` files, use the following command:</span></span>

    ```bash
    scp mapper.py reducer.py username@clustername-ssh.azurehdinsight.net:
    ```

    <span data-ttu-id="5dd31-140">Remplacez `username` par le nom d’utilisateur SSH de votre cluster, et remplacez `clustername` par le nom de votre cluster.</span><span class="sxs-lookup"><span data-stu-id="5dd31-140">Replace `username` with the SSH user name for your cluster, and `clustername` with the name of your cluster.</span></span>

    <span data-ttu-id="5dd31-141">Avec cette commande, les fichiers du système local sont copiés dans le nœud principal.</span><span class="sxs-lookup"><span data-stu-id="5dd31-141">This command copies the files from the local system to the head node.</span></span>

    > [!NOTE]
    > <span data-ttu-id="5dd31-142">Si vous utilisez un mot de passe pour sécuriser votre compte SSH, vous êtes invité à le saisir.</span><span class="sxs-lookup"><span data-stu-id="5dd31-142">If you used a password to secure your SSH account, you are prompted for the password.</span></span> <span data-ttu-id="5dd31-143">Si vous utilisez une clé SSH, vous devrez peut-être utiliser le paramètre `-i` et le chemin d'accès à la clé privée.</span><span class="sxs-lookup"><span data-stu-id="5dd31-143">If you used an SSH key, you may have to use the `-i` parameter and the path to the private key.</span></span> <span data-ttu-id="5dd31-144">Par exemple, `scp -i /path/to/private/key mapper.py reducer.py username@clustername-ssh.azurehdinsight.net:`.</span><span class="sxs-lookup"><span data-stu-id="5dd31-144">For example, `scp -i /path/to/private/key mapper.py reducer.py username@clustername-ssh.azurehdinsight.net:`.</span></span>

2. <span data-ttu-id="5dd31-145">Connectez-vous au cluster à l’aide de SSH :</span><span class="sxs-lookup"><span data-stu-id="5dd31-145">Connect to the cluster by using SSH:</span></span>

    ```bash
    ssh username@clustername-ssh.azurehdinsight.net`
    ```

    <span data-ttu-id="5dd31-146">Pour en savoir plus, consultez [Utilisation de SSH avec HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="5dd31-146">For more information on, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

3. <span data-ttu-id="5dd31-147">Pour garantir que les fichiers mapper.py et reducer.py ont des fins de ligne correctes, utilisez les commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="5dd31-147">To ensure the mapper.py and reducer.py have the correct line endings, use the following commands:</span></span>

    ```bash
    perl -pi -e 's/\r\n/\n/g' mapper.py
    perl -pi -e 's/\r\n/\n/g' reducer.py
    ```

4. <span data-ttu-id="5dd31-148">Exécutez la commande suivante pour démarrer la tâche MapReduce :</span><span class="sxs-lookup"><span data-stu-id="5dd31-148">Use the following command to start the MapReduce job.</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-streaming.jar -files mapper.py,reducer.py -mapper mapper.py -reducer reducer.py -input /example/data/gutenberg/davinci.txt -output /example/wordcountout
    ```

    <span data-ttu-id="5dd31-149">Cette commande dispose des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="5dd31-149">This command has the following parts:</span></span>

   * <span data-ttu-id="5dd31-150">**hadoop-streaming.jar**: utilisé lors de l’exécution d’opérations de diffusion en contenu MapReduce.</span><span class="sxs-lookup"><span data-stu-id="5dd31-150">**hadoop-streaming.jar**: Used when performing streaming MapReduce operations.</span></span> <span data-ttu-id="5dd31-151">Il établit un lien entre Hadoop et le code externe MapReduce que vous fournissez</span><span class="sxs-lookup"><span data-stu-id="5dd31-151">It interfaces Hadoop with the external MapReduce code you provide.</span></span>

   * <span data-ttu-id="5dd31-152">**-files** : ajoute les fichiers spécifiés à la tâche MapReduce.</span><span class="sxs-lookup"><span data-stu-id="5dd31-152">**-files**: Adds the specified files to the MapReduce job.</span></span>

   * <span data-ttu-id="5dd31-153">**-mapper**: indique à Hadoop quel fichier doit être utilisé comme mappeur.</span><span class="sxs-lookup"><span data-stu-id="5dd31-153">**-mapper**: Tells Hadoop which file to use as the mapper.</span></span>

   * <span data-ttu-id="5dd31-154">**-reducer**: indique à Hadoop quel fichier doit être utilisé comme raccord de réduction.</span><span class="sxs-lookup"><span data-stu-id="5dd31-154">**-reducer**: Tells Hadoop which file to use as the reducer.</span></span>

   * <span data-ttu-id="5dd31-155">**-input**: le fichier d’entrée à partir duquel nous devrions compter les mots.</span><span class="sxs-lookup"><span data-stu-id="5dd31-155">**-input**: The input file that we should count words from.</span></span>

   * <span data-ttu-id="5dd31-156">**-output** : le répertoire sur lequel le résultat est écrit.</span><span class="sxs-lookup"><span data-stu-id="5dd31-156">**-output**: The directory that the output is written to.</span></span>

    <span data-ttu-id="5dd31-157">La tâche MapReduce fonctionne et le processus s’affiche sous forme de pourcentages.</span><span class="sxs-lookup"><span data-stu-id="5dd31-157">As the MapReduce job works, the process is displayed as percentages.</span></span>

        <span data-ttu-id="5dd31-158">15/02/05 19:01:04 INFO mapreduce.Job:  map 0% reduce 0%    15/02/05 19:01:16 INFO mapreduce.Job:  map 100% reduce 0%    15/02/05 19:01:27 INFO mapreduce.Job:  map 100% reduce 100%</span><span class="sxs-lookup"><span data-stu-id="5dd31-158">15/02/05 19:01:04 INFO mapreduce.Job:  map 0% reduce 0%    15/02/05 19:01:16 INFO mapreduce.Job:  map 100% reduce 0%    15/02/05 19:01:27 INFO mapreduce.Job:  map 100% reduce 100%</span></span>


5. <span data-ttu-id="5dd31-159">Pour afficher la sortie, utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="5dd31-159">To view the output, use the following command:</span></span>

    ```bash
    hdfs dfs -text /example/wordcountout/part-00000
    ```

    <span data-ttu-id="5dd31-160">Cette commande affiche une liste des mots et le nombre de fois où ils apparaissent.</span><span class="sxs-lookup"><span data-stu-id="5dd31-160">This command displays a list of words and how many times the word occurred.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5dd31-161">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="5dd31-161">Next steps</span></span>

<span data-ttu-id="5dd31-162">Maintenant que vous avez découvert comment utiliser des travaux de diffusion en continu MapReduce avec HDInsight, cliquez sur les liens suivants pour explorer d’autres façons d’utiliser Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5dd31-162">Now that you have learned how to use streaming MapRedcue jobs with HDInsight, use the following links to explore other ways to work with Azure HDInsight.</span></span>

* [<span data-ttu-id="5dd31-163">Utilisation de Hive avec HDInsight</span><span class="sxs-lookup"><span data-stu-id="5dd31-163">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="5dd31-164">Utilisation de Pig avec HDInsight</span><span class="sxs-lookup"><span data-stu-id="5dd31-164">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="5dd31-165">Utilisation des tâches MapReduce avec HDInsight</span><span class="sxs-lookup"><span data-stu-id="5dd31-165">Use MapReduce jobs with HDInsight</span></span>](hdinsight-use-mapreduce.md)
