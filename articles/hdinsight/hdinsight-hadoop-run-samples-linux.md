---
title: "Exécuter des exemples MapReduce Hadoop dans HDInsight - Azure | Documents Microsoft"
description: "Bien démarrer avec des exemples MapReduce dans des fichiers jar inclus dans HDInsight. Utilisez le protocole SSH pour vous connecter au cluster, puis utilisez la commande Hadoop pour exécuter des exemples de travaux."
keywords: exemple de fichier jar Hadoop, exemples de fichiers jar hadoop, exemples mapreduce hadoop, exemples mapreduce
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: e1d2a0b9-1659-4fab-921e-4a8990cbb30a
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: larryfr
ms.openlocfilehash: 447c07f869ff9a2a2a00089248be98e6729d6dc4
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="run-the-mapreduce-examples-included-in-hdinsight"></a><span data-ttu-id="54a9e-105">Exécuter les exemples MapReduce inclus dans HDInsight</span><span class="sxs-lookup"><span data-stu-id="54a9e-105">Run the MapReduce examples included in HDInsight</span></span>

[!INCLUDE [samples-selector](../../includes/hdinsight-run-samples-selector.md)]

<span data-ttu-id="54a9e-106">Découvrez comment exécuter les exemples MapReduce inclus à Hadoop dans HDInsight.</span><span class="sxs-lookup"><span data-stu-id="54a9e-106">Learn how to run the MapReduce examples included with Hadoop on HDInsight.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="54a9e-107">Composants requis</span><span class="sxs-lookup"><span data-stu-id="54a9e-107">Prerequisites</span></span>

* <span data-ttu-id="54a9e-108">**Un cluster HDInsight** : consultez la rubrique [Bien démarrer avec Hadoop avec Hive dans HDInsight sur Linux](hdinsight-hadoop-linux-tutorial-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="54a9e-108">**An HDInsight cluster**: See [Get started using Hadoop with Hive in HDInsight on Linux](hdinsight-hadoop-linux-tutorial-get-started.md)</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="54a9e-109">Linux est le seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure.</span><span class="sxs-lookup"><span data-stu-id="54a9e-109">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="54a9e-110">Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="54a9e-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="54a9e-111">**Client SSH** : pour en savoir plus, voir [Utilisation de SSH avec Hadoop Linux sur HDInsight depuis Linux, Unix ou OS XH](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="54a9e-111">**An SSH client**: For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <a name="the-mapreduce-examples"></a><span data-ttu-id="54a9e-112">Exemples MapReduce</span><span class="sxs-lookup"><span data-stu-id="54a9e-112">The MapReduce examples</span></span>

<span data-ttu-id="54a9e-113">**Emplacement** : les exemples se trouvent sur le cluster HDInsight à l’emplacement `/usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar`.</span><span class="sxs-lookup"><span data-stu-id="54a9e-113">**Location**: The samples are located on the HDInsight cluster at `/usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar`.</span></span>

<span data-ttu-id="54a9e-114">**Contenu**: les exemples suivants sont contenus dans cette archive :</span><span class="sxs-lookup"><span data-stu-id="54a9e-114">**Contents**: The following samples are contained in this archive:</span></span>

* <span data-ttu-id="54a9e-115">`aggregatewordcount` : un programme mapreduce basé sur une agrégation qui compte les mots contenus dans les fichiers d’entrée.</span><span class="sxs-lookup"><span data-stu-id="54a9e-115">`aggregatewordcount`: An Aggregate based mapreduce program that counts the words in the input files.</span></span>
* <span data-ttu-id="54a9e-116">`aggregatewordhist` : un programme mapreduce basé sur une agrégation qui calcule l’histogramme des mots contenus dans les fichiers d’entrée.</span><span class="sxs-lookup"><span data-stu-id="54a9e-116">`aggregatewordhist`: An Aggregate based mapreduce program that computes the histogram of the words in the input files.</span></span>
* <span data-ttu-id="54a9e-117">`bbp`: Un programme mapreduce qui utilise Bailey-Borwein-Plouffe pour calculer les chiffres exacts de Pi.</span><span class="sxs-lookup"><span data-stu-id="54a9e-117">`bbp`: A mapreduce program that uses Bailey-Borwein-Plouffe to compute exact digits of Pi.</span></span>
* <span data-ttu-id="54a9e-118">`dbcount` : un exemple de travail qui compte les journaux d’affichage de pages stockés dans une base de données.</span><span class="sxs-lookup"><span data-stu-id="54a9e-118">`dbcount`: An example job that counts the pageview logs stored in a database.</span></span>
* <span data-ttu-id="54a9e-119">`distbbp` : un programme mapreduce qui utilise une formule de type BBP pour calculer le nombre exact de bits de Pi.</span><span class="sxs-lookup"><span data-stu-id="54a9e-119">`distbbp`: A mapreduce program that uses a BBP-type formula to compute exact bits of Pi.</span></span>
* <span data-ttu-id="54a9e-120">`grep` : un programme mapreduce qui compte les correspondances regex dans l’entrée.</span><span class="sxs-lookup"><span data-stu-id="54a9e-120">`grep`: A mapreduce program that counts the matches of a regex in the input.</span></span>
* <span data-ttu-id="54a9e-121">`join` : un travail qui effectue une jonction sur des jeux de données triés, à partition égale.</span><span class="sxs-lookup"><span data-stu-id="54a9e-121">`join`: A job that performs a join over sorted, equally partitioned datasets.</span></span>
* <span data-ttu-id="54a9e-122">`multifilewc` : un travail qui compte les mots de plusieurs fichiers.</span><span class="sxs-lookup"><span data-stu-id="54a9e-122">`multifilewc`: A job that counts words from several files.</span></span>
* <span data-ttu-id="54a9e-123">`pentomino` : un programme mapreduce de disposition de vignettes permettant de trouver des solutions aux problèmes posés par les pentominos.</span><span class="sxs-lookup"><span data-stu-id="54a9e-123">`pentomino`: A mapreduce tile laying program to find solutions to pentomino problems.</span></span>
* <span data-ttu-id="54a9e-124">`pi` : un programme mapreduce qui estime la valeur de Pi à l’aide de la méthode quasi Monte Carlo.</span><span class="sxs-lookup"><span data-stu-id="54a9e-124">`pi`: A mapreduce program that estimates Pi using a quasi-Monte Carlo method.</span></span>
* <span data-ttu-id="54a9e-125">`randomtextwriter` : un programme mapreduce qui écrit 10 Go de données textuelles aléatoires par nœud.</span><span class="sxs-lookup"><span data-stu-id="54a9e-125">`randomtextwriter`: A mapreduce program that writes 10 GB of random textual data per node.</span></span>
* <span data-ttu-id="54a9e-126">`randomwriter` : un programme mapreduce qui écrit 10 Go de données aléatoires par nœud.</span><span class="sxs-lookup"><span data-stu-id="54a9e-126">`randomwriter`: A mapreduce program that writes 10 GB of random data per node.</span></span>
* <span data-ttu-id="54a9e-127">`secondarysort` : un exemple définissant un tri secondaire lors de la phase de réduction.</span><span class="sxs-lookup"><span data-stu-id="54a9e-127">`secondarysort`: An example defining a secondary sort to the reduce phase.</span></span>
* <span data-ttu-id="54a9e-128">`sort` : un programme mapreduce qui trie les données écrites par l’enregistreur aléatoire.</span><span class="sxs-lookup"><span data-stu-id="54a9e-128">`sort`: A mapreduce program that sorts the data written by the random writer.</span></span>
* <span data-ttu-id="54a9e-129">`sudoku` : un solveur de sudoku.</span><span class="sxs-lookup"><span data-stu-id="54a9e-129">`sudoku`: A sudoku solver.</span></span>
* <span data-ttu-id="54a9e-130">`teragen` : générateur de données pour le programme terasort.</span><span class="sxs-lookup"><span data-stu-id="54a9e-130">`teragen`: Generate data for the terasort.</span></span>
* <span data-ttu-id="54a9e-131">`terasort` : exécution du terasort.</span><span class="sxs-lookup"><span data-stu-id="54a9e-131">`terasort`: Run the terasort.</span></span>
* <span data-ttu-id="54a9e-132">`teravalidate` : vérification des résultats du programme terasort.</span><span class="sxs-lookup"><span data-stu-id="54a9e-132">`teravalidate`: Checking results of terasort.</span></span>
* <span data-ttu-id="54a9e-133">`wordcount` : un programme mapreduce qui compte les mots contenus dans les fichiers d’entrée.</span><span class="sxs-lookup"><span data-stu-id="54a9e-133">`wordcount`: A mapreduce program that counts the words in the input files.</span></span>
* <span data-ttu-id="54a9e-134">`wordmean` : un programme mapreduce qui compte la longueur moyenne des mots contenus dans les fichiers d’entrée.</span><span class="sxs-lookup"><span data-stu-id="54a9e-134">`wordmean`: A mapreduce program that counts the average length of the words in the input files.</span></span>
* <span data-ttu-id="54a9e-135">`wordmedian` : un programme mapreduce qui compte la longueur moyenne des mots contenus dans les fichiers d’entrée.</span><span class="sxs-lookup"><span data-stu-id="54a9e-135">`wordmedian`: A mapreduce program that counts the median length of the words in the input files.</span></span>
* <span data-ttu-id="54a9e-136">`wordstandarddeviation` : un programme mapreduce qui compte l’écart type de la longueur des mots contenus dans les fichiers d’entrée.</span><span class="sxs-lookup"><span data-stu-id="54a9e-136">`wordstandarddeviation`: A mapreduce program that counts the standard deviation of the length of the words in the input files.</span></span>

<span data-ttu-id="54a9e-137">**Code source** : le code source de ces exemples est inclus dans le cluster HDInsight à l’emplacement `/usr/hdp/2.2.4.9-1/hadoop/src/hadoop-mapreduce-project/hadoop-mapreduce-examples`.</span><span class="sxs-lookup"><span data-stu-id="54a9e-137">**Source code**: Source code for these samples is included on the HDInsight cluster at `/usr/hdp/2.2.4.9-1/hadoop/src/hadoop-mapreduce-project/hadoop-mapreduce-examples`.</span></span>

> [!NOTE]
> <span data-ttu-id="54a9e-138">Dans le chemin d’accès, `2.2.4.9-1` représente la version de la plateforme de données Hortonworks du cluster HDInsight ; elle peut différer pour votre cluster.</span><span class="sxs-lookup"><span data-stu-id="54a9e-138">The `2.2.4.9-1` in the path is the version of the Hortonworks Data Platform for the HDInsight cluster, and may be different for your cluster.</span></span>

## <a name="run-the-wordcount-example"></a><span data-ttu-id="54a9e-139">Exécuter l’exemple wordcount</span><span class="sxs-lookup"><span data-stu-id="54a9e-139">Run the wordcount example</span></span>

1. <span data-ttu-id="54a9e-140">Connectez-vous à HDInsight à l’aide de SSH.</span><span class="sxs-lookup"><span data-stu-id="54a9e-140">Connect to HDInsight using SSH.</span></span> <span data-ttu-id="54a9e-141">Pour en savoir plus, voir [Utilisation de SSH avec Hadoop Linux sur HDInsight depuis Linux, Unix ou OS X](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="54a9e-141">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="54a9e-142">À l’invite `username@#######:~$` , utilisez la commande suivante pour répertorier les exemples :</span><span class="sxs-lookup"><span data-stu-id="54a9e-142">From the `username@#######:~$` prompt, use the following command to list the samples:</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar
    ```

    <span data-ttu-id="54a9e-143">Cette commande génère la liste des exemples de la section précédente de ce document.</span><span class="sxs-lookup"><span data-stu-id="54a9e-143">This command generates the list of sample from the previous section of this document.</span></span>

3. <span data-ttu-id="54a9e-144">Utilisez la commande suivante pour obtenir de l’aide sur un exemple spécifique.</span><span class="sxs-lookup"><span data-stu-id="54a9e-144">Use the following command to get help on a specific sample.</span></span> <span data-ttu-id="54a9e-145">Dans ce cas, l’exemple **wordcount** :</span><span class="sxs-lookup"><span data-stu-id="54a9e-145">In this case, the **wordcount** sample:</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount
    ```

    <span data-ttu-id="54a9e-146">Le message suivant s’affiche :</span><span class="sxs-lookup"><span data-stu-id="54a9e-146">You receive the following message:</span></span>

        Usage: wordcount <in> [<in>...] <out>

    <span data-ttu-id="54a9e-147">Ce message indique que vous pouvez fournir plusieurs chemins d’accès d’entrée pour les documents sources.</span><span class="sxs-lookup"><span data-stu-id="54a9e-147">This message indicates that you can provide several input paths for the source documents.</span></span> <span data-ttu-id="54a9e-148">Le chemin d’accès final correspond à l’emplacement de stockage de la sortie (nombre de mots dans les documents sources).</span><span class="sxs-lookup"><span data-stu-id="54a9e-148">The final path is where the output (count of words in the source documents) is stored.</span></span>

4. <span data-ttu-id="54a9e-149">Pour compter tous les mots figurant dans les carnets de Léonard De Vinci qui sont fournis comme exemples de données avec votre cluster, utilisez les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="54a9e-149">Use the following to count all words in the Notebooks of Leonardo Da Vinci, which are provided as sample data with your cluster:</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount /example/data/gutenberg/davinci.txt /example/data/davinciwordcount
    ```

    <span data-ttu-id="54a9e-150">L’entrée de ce travail est lue à partir de `/example/data/gutenberg/davinci.txt`.</span><span class="sxs-lookup"><span data-stu-id="54a9e-150">Input for this job is read from `/example/data/gutenberg/davinci.txt`.</span></span> <span data-ttu-id="54a9e-151">La sortie de cet exemple est stockée dans `/example/data/davinciwordcount`.</span><span class="sxs-lookup"><span data-stu-id="54a9e-151">Output for this example is stored in `/example/data/davinciwordcount`.</span></span> <span data-ttu-id="54a9e-152">Les deux chemins d’accès sont situés sur le stockage par défaut du cluster, et non du système de fichiers local.</span><span class="sxs-lookup"><span data-stu-id="54a9e-152">Both paths are located on default storage for the cluster, not the local file system.</span></span>

   > [!NOTE]
   > <span data-ttu-id="54a9e-153">Comme indiqué dans l’aide de l’exemple wordcount, vous pouvez également spécifier plusieurs fichiers d’entrée.</span><span class="sxs-lookup"><span data-stu-id="54a9e-153">As noted in the help for the wordcount sample, you could also specify multiple input files.</span></span> <span data-ttu-id="54a9e-154">Par exemple, `hadoop jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount /example/data/gutenberg/davinci.txt /example/data/gutenberg/ulysses.txt /example/data/twowordcount` compte les mots figurant dans les fichiers davinci.txt et ulysses.txt.</span><span class="sxs-lookup"><span data-stu-id="54a9e-154">For example, `hadoop jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount /example/data/gutenberg/davinci.txt /example/data/gutenberg/ulysses.txt /example/data/twowordcount` would count words in both davinci.txt and ulysses.txt.</span></span>

5. <span data-ttu-id="54a9e-155">Une fois la tâche terminée, utilisez la commande suivante pour afficher le résultat généré :</span><span class="sxs-lookup"><span data-stu-id="54a9e-155">Once the job completes, use the following command to view the output:</span></span>

    ```bash
    hdfs dfs -cat /example/data/davinciwordcount/*
    ```

    <span data-ttu-id="54a9e-156">Cette commande concatène tous les fichiers de sortie générés par le travail.</span><span class="sxs-lookup"><span data-stu-id="54a9e-156">This command concatenates all the output files produced by the job.</span></span> <span data-ttu-id="54a9e-157">Elle affiche la sortie dans la console.</span><span class="sxs-lookup"><span data-stu-id="54a9e-157">It displays the output to the console.</span></span> <span data-ttu-id="54a9e-158">Le résultat ressemble au texte suivant :</span><span class="sxs-lookup"><span data-stu-id="54a9e-158">The output is similar to the following text:</span></span>

        zum     1
        zur     1
        zwanzig 1
        zweite  1

    <span data-ttu-id="54a9e-159">Chaque ligne représente un mot et le nombre d’occurrences dans les données d’entrée.</span><span class="sxs-lookup"><span data-stu-id="54a9e-159">Each line represents a word and how many times it occurred in the input data.</span></span>

## <a name="the-sudoku-example"></a><span data-ttu-id="54a9e-160">L’exemple de Sudoku</span><span class="sxs-lookup"><span data-stu-id="54a9e-160">The Sudoku example</span></span>

<span data-ttu-id="54a9e-161">[Sudoku](https://en.wikipedia.org/wiki/Sudoku) est un puzzle logique composé de 3 x 3 grilles.</span><span class="sxs-lookup"><span data-stu-id="54a9e-161">[Sudoku](https://en.wikipedia.org/wiki/Sudoku) is a logic puzzle made up of nine 3x3 grids.</span></span> <span data-ttu-id="54a9e-162">Certaines cellules de la grille comportent des numéros, tandis que d’autres sont vides, l’objectif consiste à résoudre les cellules vides.</span><span class="sxs-lookup"><span data-stu-id="54a9e-162">Some cells in the grid have numbers, while others are blank, and the goal is to solve for the blank cells.</span></span> <span data-ttu-id="54a9e-163">Le lien précédent comporte davantage d’informations sur le casse-tête, mais l’objectif de cet exemple consiste à résoudre les cellules vides.</span><span class="sxs-lookup"><span data-stu-id="54a9e-163">The previous link has more information on the puzzle, but the purpose of this sample is to solve for the blank cells.</span></span> <span data-ttu-id="54a9e-164">Par conséquent, notre entrée doit être un fichier au format suivant :</span><span class="sxs-lookup"><span data-stu-id="54a9e-164">So our input should be a file that is in the following format:</span></span>

* <span data-ttu-id="54a9e-165">Neuf lignes de neuf colonnes</span><span class="sxs-lookup"><span data-stu-id="54a9e-165">Nine rows of nine columns</span></span>
* <span data-ttu-id="54a9e-166">Chaque colonne peut contenir un nombre ou `?` (qui indique une cellule vide)</span><span class="sxs-lookup"><span data-stu-id="54a9e-166">Each column can contain either a number or `?` (which indicates a blank cell)</span></span>
* <span data-ttu-id="54a9e-167">Les cellules sont séparées par un espace</span><span class="sxs-lookup"><span data-stu-id="54a9e-167">Cells are separated by a space</span></span>

<span data-ttu-id="54a9e-168">La façon de construire des puzzles Sudoku est particulière dans la mesure où vous ne pouvez pas répéter un nombre dans une colonne ou une ligne.</span><span class="sxs-lookup"><span data-stu-id="54a9e-168">There is a certain way to construct Sudoku puzzles; you can't repeat a number in a column or row.</span></span> <span data-ttu-id="54a9e-169">Il existe un exemple sur le cluster HDInsight qui est construit correctement.</span><span class="sxs-lookup"><span data-stu-id="54a9e-169">There's an example on the HDInsight cluster that is properly constructed.</span></span> <span data-ttu-id="54a9e-170">Il se trouve dans `/usr/hdp/*/hadoop/src/hadoop-mapreduce-project/hadoop-mapreduce-examples/src/main/java/org/apache/hadoop/examples/dancing/puzzle1.dta` et contient le texte suivant :</span><span class="sxs-lookup"><span data-stu-id="54a9e-170">It is located at `/usr/hdp/*/hadoop/src/hadoop-mapreduce-project/hadoop-mapreduce-examples/src/main/java/org/apache/hadoop/examples/dancing/puzzle1.dta` and contains the following text:</span></span>

    8 5 ? 3 9 ? ? ? ?
    ? ? 2 ? ? ? ? ? ?
    ? ? 6 ? 1 ? ? ? 2
    ? ? 4 ? ? 3 ? 5 9
    ? ? 8 9 ? 1 4 ? ?
    3 2 ? 4 ? ? 8 ? ?
    9 ? ? ? 8 ? 5 ? ?
    ? ? ? ? ? ? 2 ? ?
    ? ? ? ? 4 5 ? 7 8

<span data-ttu-id="54a9e-171">Pour exécuter cet exemple de problème dans l’exemple de Sudoku, utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="54a9e-171">To run this example problem through the Sudoku example, use the following command:</span></span>

```bash
yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar sudoku /usr/hdp/*/hadoop/src/hadoop-mapreduce-project/hadoop-mapreduce-examples/src/main/java/org/apache/hadoop/examples/dancing/puzzle1.dta
```

<span data-ttu-id="54a9e-172">Les résultats sont les suivants :</span><span class="sxs-lookup"><span data-stu-id="54a9e-172">The results appear similar to the following text:</span></span>

    8 5 1 3 9 2 6 4 7
    4 3 2 6 7 8 1 9 5
    7 9 6 5 1 4 3 8 2
    6 1 4 8 2 3 7 5 9
    5 7 8 9 6 1 4 2 3
    3 2 9 4 5 7 8 1 6
    9 4 7 2 8 6 5 3 1
    1 8 5 7 3 9 2 6 4
    2 6 3 1 4 5 9 7 8

## <a name="pi--example"></a><span data-ttu-id="54a9e-173">Exemple de Pi (π)</span><span class="sxs-lookup"><span data-stu-id="54a9e-173">Pi (π) example</span></span>

<span data-ttu-id="54a9e-174">L’exemple de Pi utilise une méthode statistique (quasi-Monte-Carlo) pour estimer la valeur de Pi.</span><span class="sxs-lookup"><span data-stu-id="54a9e-174">The pi sample uses a statistical (quasi-Monte Carlo) method to estimate the value of pi.</span></span> <span data-ttu-id="54a9e-175">Les points sont placés de manière aléatoire dans un carré unitaire.</span><span class="sxs-lookup"><span data-stu-id="54a9e-175">Points are placed at random in a unit square.</span></span> <span data-ttu-id="54a9e-176">Le carré contient également un cercle.</span><span class="sxs-lookup"><span data-stu-id="54a9e-176">The square also contains a circle.</span></span> <span data-ttu-id="54a9e-177">La probabilité que les points tombent dans le cercle est égale à l’aire du cercle, pi/4.</span><span class="sxs-lookup"><span data-stu-id="54a9e-177">The probability that the points fall within the circle are equal to the area of the circle, pi/4.</span></span> <span data-ttu-id="54a9e-178">La valeur de pi peut être estimée à partir de la valeur de 4R.</span><span class="sxs-lookup"><span data-stu-id="54a9e-178">The value of pi can be estimated from the value of 4R.</span></span> <span data-ttu-id="54a9e-179">R est le rapport entre le nombre de points situés à l’intérieur du cercle et le nombre total de points situés à l’intérieur du carré.</span><span class="sxs-lookup"><span data-stu-id="54a9e-179">R is the ratio of the number of points that are inside the circle to the total number of points that are within the square.</span></span> <span data-ttu-id="54a9e-180">Plus l'échantillon de points est grand, plus l'estimation est précise.</span><span class="sxs-lookup"><span data-stu-id="54a9e-180">The larger the sample of points used, the better the estimate is.</span></span>

<span data-ttu-id="54a9e-181">Utilisez la commande suivante pour exécuter cet exemple :</span><span class="sxs-lookup"><span data-stu-id="54a9e-181">Use the following command to run this sample.</span></span> <span data-ttu-id="54a9e-182">Cette commande utilise 16 mappages, avec pour chacun 10 000 000 exemples, pour estimer la valeur de Pi :</span><span class="sxs-lookup"><span data-stu-id="54a9e-182">This command uses 16 maps with 10,000,000 samples each to estimate the value of pi:</span></span>

```bash
yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar pi 16 10000000
```

<span data-ttu-id="54a9e-183">La valeur retournée par cette commande doit être semblable à **3,14159155000000000000**.</span><span class="sxs-lookup"><span data-stu-id="54a9e-183">The value returned by this command is similar to **3.14159155000000000000**.</span></span> <span data-ttu-id="54a9e-184">Pour référence, voici les 10 chiffres de Pi après la virgule : 3,1415926535.</span><span class="sxs-lookup"><span data-stu-id="54a9e-184">For references, the first 10 decimal places of pi are 3.1415926535.</span></span>

## <a name="10-gb-greysort-example"></a><span data-ttu-id="54a9e-185">Exemple de Greysort de 10 Go</span><span class="sxs-lookup"><span data-stu-id="54a9e-185">10 GB Greysort example</span></span>

<span data-ttu-id="54a9e-186">GraySort est un tri de benchmark.</span><span class="sxs-lookup"><span data-stu-id="54a9e-186">GraySort is a benchmark sort.</span></span> <span data-ttu-id="54a9e-187">La mesure est le taux de tri (To/minute) obtenu lors du tri de très grandes quantités de données, en général au minimum 100 To.</span><span class="sxs-lookup"><span data-stu-id="54a9e-187">The metric is the sort rate (TB/minute) that is achieved while sorting large amounts of data, usually a 100 TB minimum.</span></span>

<span data-ttu-id="54a9e-188">Cet exemple utilise seulement 10 Go de données afin de pouvoir être exécuté relativement rapidement.</span><span class="sxs-lookup"><span data-stu-id="54a9e-188">This sample uses a modest 10 GB of data so that it can be run relatively quickly.</span></span> <span data-ttu-id="54a9e-189">Il utilise les applications MapReduce développées par Owen O'Malley et Arun Murthy.</span><span class="sxs-lookup"><span data-stu-id="54a9e-189">It uses the MapReduce applications developed by Owen O'Malley and Arun Murthy.</span></span> <span data-ttu-id="54a9e-190">Ces applications ont remporté en 2009 le benchmark du tri de téraoctets (« daytona ») annuel universel général avec un taux de 0,578 To/min (100 To en 173 minutes).</span><span class="sxs-lookup"><span data-stu-id="54a9e-190">These applications won the annual general-purpose ("daytona") terabyte sort benchmark in 2009, with a rate of 0.578 TB/min (100 TB in 173 minutes).</span></span> <span data-ttu-id="54a9e-191">Pour plus d'informations à ce sujet et sur d'autres benchmarks de tri, consultez le site [Sortbenchmark](http://sortbenchmark.org/) .</span><span class="sxs-lookup"><span data-stu-id="54a9e-191">For more information on this and other sorting benchmarks, see the [Sortbenchmark](http://sortbenchmark.org/) site.</span></span>

<span data-ttu-id="54a9e-192">Cet exemple utilise trois ensembles de programmes MapReduce :</span><span class="sxs-lookup"><span data-stu-id="54a9e-192">This sample uses three sets of MapReduce programs:</span></span>

* <span data-ttu-id="54a9e-193">**TeraGen**: programme MapReduce qui génère des lignes de données à trier</span><span class="sxs-lookup"><span data-stu-id="54a9e-193">**TeraGen**: A MapReduce program that generates rows of data to sort</span></span>

* <span data-ttu-id="54a9e-194">**TeraSort**: échantillonne les données d'entrée et utilise MapReduce pour trier les données en une commande totale.</span><span class="sxs-lookup"><span data-stu-id="54a9e-194">**TeraSort**: Samples the input data and uses MapReduce to sort the data into a total order</span></span>

    <span data-ttu-id="54a9e-195">TeraSort est un tri MapReduce standard, à l’exception d’un partitionneur personnalisé.</span><span class="sxs-lookup"><span data-stu-id="54a9e-195">TeraSort is a standard MapReduce sort, except for a custom partitioner.</span></span> <span data-ttu-id="54a9e-196">Le partitionneur utilise une liste triée des clés N-1 échantillonnée qui définissent la plage de clés pour chaque réduction.</span><span class="sxs-lookup"><span data-stu-id="54a9e-196">The partitioner uses a sorted list of N-1 sampled keys that define the key range for each reduce.</span></span> <span data-ttu-id="54a9e-197">Plus particulièrement, toutes les clés semblables à cet échantillon [i-1] <= key < sample[i] sont envoyées pour réduire i.</span><span class="sxs-lookup"><span data-stu-id="54a9e-197">In particular, all keys such that sample[i-1] <= key < sample[i] are sent to reduce i.</span></span> <span data-ttu-id="54a9e-198">Le partitionneur garantit que les sorties de réduction i sont toutes inférieures aux sorties de réduction i+1.</span><span class="sxs-lookup"><span data-stu-id="54a9e-198">This partitioner guarantees that the outputs of reduce i are all less than the output of reduce i+1.</span></span>

* <span data-ttu-id="54a9e-199">**TeraValidate**: programme MapReduce qui valide le tri global de la sortie</span><span class="sxs-lookup"><span data-stu-id="54a9e-199">**TeraValidate**: A MapReduce program that validates that the output is globally sorted</span></span>

    <span data-ttu-id="54a9e-200">Il crée un mappage par fichier dans le répertoire de sortie et chaque mappage assure que chaque clé est inférieure ou égale à la précédente.</span><span class="sxs-lookup"><span data-stu-id="54a9e-200">It creates one map per file in the output directory, and each map ensures that each key is less than or equal to the previous one.</span></span> <span data-ttu-id="54a9e-201">La fonction de mappage génère des enregistrements de la première et de la dernière clés de chaque fichier.</span><span class="sxs-lookup"><span data-stu-id="54a9e-201">The map function generates records of the first and last keys of each file.</span></span> <span data-ttu-id="54a9e-202">La fonction de réduction veille à ce que la première clé du fichier i soit supérieure à la dernière clé du fichier i-1.</span><span class="sxs-lookup"><span data-stu-id="54a9e-202">The reduce function ensures that the first key of file i is greater than the last key of file i-1.</span></span> <span data-ttu-id="54a9e-203">Un problème est signalé comme une sortie de la phase de réduction avec les clés dans le désordre.</span><span class="sxs-lookup"><span data-stu-id="54a9e-203">Any problems are reported as an output of the reduce phase, with the keys that are out of order.</span></span>

<span data-ttu-id="54a9e-204">Utilisez les étapes suivantes pour générer des données, trier, puis valider la sortie :</span><span class="sxs-lookup"><span data-stu-id="54a9e-204">Use the following steps to generate data, sort, and then validate the output:</span></span>

1. <span data-ttu-id="54a9e-205">Générez 10 Go de données, qui sont stockées dans le stockage par défaut du cluster HDInsight à l’emplacement `/example/data/10GB-sort-input` :</span><span class="sxs-lookup"><span data-stu-id="54a9e-205">Generate 10 GB of data, which is stored to the HDInsight cluster's default storage at `/example/data/10GB-sort-input`:</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar teragen -Dmapred.map.tasks=50 100000000 /example/data/10GB-sort-input
    ```

    <span data-ttu-id="54a9e-206">`-Dmapred.map.tasks` indique à Hadoop le nombre de tâches de mappage à utiliser pour cette tâche.</span><span class="sxs-lookup"><span data-stu-id="54a9e-206">The `-Dmapred.map.tasks` tells Hadoop how many map tasks to use for this job.</span></span> <span data-ttu-id="54a9e-207">Les deux derniers paramètres demandent au travail de créer 10 Go de données et de les stocker sous `/example/data/10GB-sort-input`.</span><span class="sxs-lookup"><span data-stu-id="54a9e-207">The final two parameters instruct the job to create 10 GB of data and to store it at `/example/data/10GB-sort-input`.</span></span>

2. <span data-ttu-id="54a9e-208">Exécutez la commande suivante pour trier les données :</span><span class="sxs-lookup"><span data-stu-id="54a9e-208">Use the following command to sort the data:</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar terasort -Dmapred.map.tasks=50 -Dmapred.reduce.tasks=25 /example/data/10GB-sort-input /example/data/10GB-sort-output
    ```

    <span data-ttu-id="54a9e-209">`-Dmapred.reduce.tasks` indique à Hadoop le nombre de tâches de réduction à utiliser pour cette tâche.</span><span class="sxs-lookup"><span data-stu-id="54a9e-209">The `-Dmapred.reduce.tasks` tells Hadoop how many reduce tasks to use for the job.</span></span> <span data-ttu-id="54a9e-210">Les deux derniers paramètres sont simplement les emplacements d’entrée et de sortie des données.</span><span class="sxs-lookup"><span data-stu-id="54a9e-210">The final two parameters are just the input and output locations for data.</span></span>

3. <span data-ttu-id="54a9e-211">Pour valider les données générées par le tri, utilisez les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="54a9e-211">Use the following to validate the data generated by the sort:</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar teravalidate -Dmapred.map.tasks=50 -Dmapred.reduce.tasks=25 /example/data/10GB-sort-output /example/data/10GB-sort-validate
    ```

## <a name="next-steps"></a><span data-ttu-id="54a9e-212">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="54a9e-212">Next steps</span></span>

<span data-ttu-id="54a9e-213">Dans cet article, vous avez appris à exécuter les exemples inclus avec les clusters HDInsight sous Linux.</span><span class="sxs-lookup"><span data-stu-id="54a9e-213">From this article, you learned how to run the samples included with the Linux-based HDInsight clusters.</span></span> <span data-ttu-id="54a9e-214">Pour des didacticiels sur l’utilisation de Pig, Hive et MapReduce avec HDInsight, consultez les rubriques suivantes :</span><span class="sxs-lookup"><span data-stu-id="54a9e-214">For tutorials about using Pig, Hive, and MapReduce with HDInsight, see the following topics:</span></span>

* <span data-ttu-id="54a9e-215">[Utilisation de Pig avec Hadoop sur HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="54a9e-215">[Use Pig with Hadoop on HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="54a9e-216">[Utilisation de Hive avec Hadoop sur HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="54a9e-216">[Use Hive with Hadoop on HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="54a9e-217">[Utilisation de MapReduce avec Hadoop sur HDInsight][hdinsight-use-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="54a9e-217">[Use MapReduce with Hadoop on HDInsight][hdinsight-use-mapreduce]</span></span>

[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md
[hdinsight-sdk-documentation]: https://msdn.microsoft.com/library/azure/dn479185.aspx

[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-introduction]: hdinsight-hadoop-introduction.md



[hdinsight-samples]: hdinsight-run-samples.md

[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md
