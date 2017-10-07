---
title: exemples de Hadoop MapReduce aaaRun sur HDInsight - Azure | Documents Microsoft
description: "Bien démarrer avec des exemples MapReduce dans des fichiers jar inclus dans HDInsight. Utilisez SSH tooconnect toohello cluster, puis utilisez les travaux d’exemple hello Hadoop commande toorun."
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
ms.openlocfilehash: 7a16bbd51eb17570fcaa3b1e0f5990fa889c106a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="run-hello-mapreduce-examples-included-in-hdinsight"></a><span data-ttu-id="bd5cb-105">Exécuter les exemples de MapReduce hello inclus dans HDInsight</span><span class="sxs-lookup"><span data-stu-id="bd5cb-105">Run hello MapReduce examples included in HDInsight</span></span>

[!INCLUDE [samples-selector](../../includes/hdinsight-run-samples-selector.md)]

<span data-ttu-id="bd5cb-106">Découvrez comment obtenir des exemples toorun hello MapReduce inclus avec Hadoop dans HDInsight.</span><span class="sxs-lookup"><span data-stu-id="bd5cb-106">Learn how toorun hello MapReduce examples included with Hadoop on HDInsight.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bd5cb-107">Composants requis</span><span class="sxs-lookup"><span data-stu-id="bd5cb-107">Prerequisites</span></span>

* <span data-ttu-id="bd5cb-108">**Un cluster HDInsight** : consultez la rubrique [Bien démarrer avec Hadoop avec Hive dans HDInsight sur Linux](hdinsight-hadoop-linux-tutorial-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="bd5cb-108">**An HDInsight cluster**: See [Get started using Hadoop with Hive in HDInsight on Linux](hdinsight-hadoop-linux-tutorial-get-started.md)</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="bd5cb-109">Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure.</span><span class="sxs-lookup"><span data-stu-id="bd5cb-109">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="bd5cb-110">Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="bd5cb-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="bd5cb-111">**Client SSH** : pour en savoir plus, voir [Utilisation de SSH avec Hadoop Linux sur HDInsight depuis Linux, Unix ou OS XH](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="bd5cb-111">**An SSH client**: For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <a name="hello-mapreduce-examples"></a><span data-ttu-id="bd5cb-112">exemples de MapReduce Hello</span><span class="sxs-lookup"><span data-stu-id="bd5cb-112">hello MapReduce examples</span></span>

<span data-ttu-id="bd5cb-113">**Emplacement**: exemples de hello se trouvent sur hello cluster HDInsight à `/usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar`.</span><span class="sxs-lookup"><span data-stu-id="bd5cb-113">**Location**: hello samples are located on hello HDInsight cluster at `/usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar`.</span></span>

<span data-ttu-id="bd5cb-114">**Contenu**: hello suivant exemples contenu dans cette archive :</span><span class="sxs-lookup"><span data-stu-id="bd5cb-114">**Contents**: hello following samples are contained in this archive:</span></span>

* <span data-ttu-id="bd5cb-115">`aggregatewordcount`: Un agrégat basé programme mapreduce qui compte les mots hello dans les fichiers d’entrée hello.</span><span class="sxs-lookup"><span data-stu-id="bd5cb-115">`aggregatewordcount`: An Aggregate based mapreduce program that counts hello words in hello input files.</span></span>
* <span data-ttu-id="bd5cb-116">`aggregatewordhist`: Un agrégat basé programme mapreduce qui calcule l’histogramme hello de mots hello dans les fichiers d’entrée hello.</span><span class="sxs-lookup"><span data-stu-id="bd5cb-116">`aggregatewordhist`: An Aggregate based mapreduce program that computes hello histogram of hello words in hello input files.</span></span>
* <span data-ttu-id="bd5cb-117">`bbp`: Un programme mapreduce qui utilise Bailey-Borwein-Plouffe toocompute exact de chiffres de Pi.</span><span class="sxs-lookup"><span data-stu-id="bd5cb-117">`bbp`: A mapreduce program that uses Bailey-Borwein-Plouffe toocompute exact digits of Pi.</span></span>
* <span data-ttu-id="bd5cb-118">`dbcount`: Un travail d’exemple qui compte les journaux de page d’affichage hello stockés dans une base de données.</span><span class="sxs-lookup"><span data-stu-id="bd5cb-118">`dbcount`: An example job that counts hello pageview logs stored in a database.</span></span>
* <span data-ttu-id="bd5cb-119">`distbbp`: Un programme mapreduce qui utilise une formule toocompute BBP-type exact des bits de Pi.</span><span class="sxs-lookup"><span data-stu-id="bd5cb-119">`distbbp`: A mapreduce program that uses a BBP-type formula toocompute exact bits of Pi.</span></span>
* <span data-ttu-id="bd5cb-120">`grep`: Un programme mapreduce qui compte hello correspond à des expressions régulières dans l’entrée de hello.</span><span class="sxs-lookup"><span data-stu-id="bd5cb-120">`grep`: A mapreduce program that counts hello matches of a regex in hello input.</span></span>
* <span data-ttu-id="bd5cb-121">`join` : un travail qui effectue une jonction sur des jeux de données triés, à partition égale.</span><span class="sxs-lookup"><span data-stu-id="bd5cb-121">`join`: A job that performs a join over sorted, equally partitioned datasets.</span></span>
* <span data-ttu-id="bd5cb-122">`multifilewc` : un travail qui compte les mots de plusieurs fichiers.</span><span class="sxs-lookup"><span data-stu-id="bd5cb-122">`multifilewc`: A job that counts words from several files.</span></span>
* <span data-ttu-id="bd5cb-123">`pentomino`: Une vignette mapreduce portant des solutions toofind programme toopentomino problèmes.</span><span class="sxs-lookup"><span data-stu-id="bd5cb-123">`pentomino`: A mapreduce tile laying program toofind solutions toopentomino problems.</span></span>
* <span data-ttu-id="bd5cb-124">`pi` : un programme mapreduce qui estime la valeur de Pi à l’aide de la méthode quasi Monte Carlo.</span><span class="sxs-lookup"><span data-stu-id="bd5cb-124">`pi`: A mapreduce program that estimates Pi using a quasi-Monte Carlo method.</span></span>
* <span data-ttu-id="bd5cb-125">`randomtextwriter` : un programme mapreduce qui écrit 10 Go de données textuelles aléatoires par nœud.</span><span class="sxs-lookup"><span data-stu-id="bd5cb-125">`randomtextwriter`: A mapreduce program that writes 10 GB of random textual data per node.</span></span>
* <span data-ttu-id="bd5cb-126">`randomwriter` : un programme mapreduce qui écrit 10 Go de données aléatoires par nœud.</span><span class="sxs-lookup"><span data-stu-id="bd5cb-126">`randomwriter`: A mapreduce program that writes 10 GB of random data per node.</span></span>
* <span data-ttu-id="bd5cb-127">`secondarysort`: Phase de réduire un exemple de définition d’un toohello secondaire du tri.</span><span class="sxs-lookup"><span data-stu-id="bd5cb-127">`secondarysort`: An example defining a secondary sort toohello reduce phase.</span></span>
* <span data-ttu-id="bd5cb-128">`sort`: Un programme mapreduce qui trie des données hello écrites par hello d’écriture aléatoire.</span><span class="sxs-lookup"><span data-stu-id="bd5cb-128">`sort`: A mapreduce program that sorts hello data written by hello random writer.</span></span>
* <span data-ttu-id="bd5cb-129">`sudoku` : un solveur de sudoku.</span><span class="sxs-lookup"><span data-stu-id="bd5cb-129">`sudoku`: A sudoku solver.</span></span>
* <span data-ttu-id="bd5cb-130">`teragen`: Générer des données pour hello terasort.</span><span class="sxs-lookup"><span data-stu-id="bd5cb-130">`teragen`: Generate data for hello terasort.</span></span>
* <span data-ttu-id="bd5cb-131">`terasort`: Exécutez hello terasort.</span><span class="sxs-lookup"><span data-stu-id="bd5cb-131">`terasort`: Run hello terasort.</span></span>
* <span data-ttu-id="bd5cb-132">`teravalidate` : vérification des résultats du programme terasort.</span><span class="sxs-lookup"><span data-stu-id="bd5cb-132">`teravalidate`: Checking results of terasort.</span></span>
* <span data-ttu-id="bd5cb-133">`wordcount`: Un programme mapreduce qui compte les mots hello dans les fichiers d’entrée hello.</span><span class="sxs-lookup"><span data-stu-id="bd5cb-133">`wordcount`: A mapreduce program that counts hello words in hello input files.</span></span>
* <span data-ttu-id="bd5cb-134">`wordmean`: Un programme mapreduce qui compte la longueur moyenne de hello de mots hello dans les fichiers d’entrée hello.</span><span class="sxs-lookup"><span data-stu-id="bd5cb-134">`wordmean`: A mapreduce program that counts hello average length of hello words in hello input files.</span></span>
* <span data-ttu-id="bd5cb-135">`wordmedian`: Un programme mapreduce qui compte la longueur de la médiane hello de mots hello dans les fichiers d’entrée hello.</span><span class="sxs-lookup"><span data-stu-id="bd5cb-135">`wordmedian`: A mapreduce program that counts hello median length of hello words in hello input files.</span></span>
* <span data-ttu-id="bd5cb-136">`wordstandarddeviation`: Un programme mapreduce qui compte écart hello de longueur hello de mots hello dans les fichiers d’entrée hello.</span><span class="sxs-lookup"><span data-stu-id="bd5cb-136">`wordstandarddeviation`: A mapreduce program that counts hello standard deviation of hello length of hello words in hello input files.</span></span>

<span data-ttu-id="bd5cb-137">**Le code source**: code Source pour ces exemples est incluse sur hello cluster HDInsight à `/usr/hdp/2.2.4.9-1/hadoop/src/hadoop-mapreduce-project/hadoop-mapreduce-examples`.</span><span class="sxs-lookup"><span data-stu-id="bd5cb-137">**Source code**: Source code for these samples is included on hello HDInsight cluster at `/usr/hdp/2.2.4.9-1/hadoop/src/hadoop-mapreduce-project/hadoop-mapreduce-examples`.</span></span>

> [!NOTE]
> <span data-ttu-id="bd5cb-138">Hello `2.2.4.9-1` Bonjour le chemin d’accès est la version hello Hello Hortonworks Data Platform pour le cluster HDInsight de hello et peut être différente pour votre cluster.</span><span class="sxs-lookup"><span data-stu-id="bd5cb-138">hello `2.2.4.9-1` in hello path is hello version of hello Hortonworks Data Platform for hello HDInsight cluster, and may be different for your cluster.</span></span>

## <a name="run-hello-wordcount-example"></a><span data-ttu-id="bd5cb-139">Exécuter l’exemple wordcount de hello</span><span class="sxs-lookup"><span data-stu-id="bd5cb-139">Run hello wordcount example</span></span>

1. <span data-ttu-id="bd5cb-140">Se connecter tooHDInsight à l’aide de SSH.</span><span class="sxs-lookup"><span data-stu-id="bd5cb-140">Connect tooHDInsight using SSH.</span></span> <span data-ttu-id="bd5cb-141">Pour en savoir plus, voir [Utilisation de SSH avec Hadoop Linux sur HDInsight depuis Linux, Unix ou OS X](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="bd5cb-141">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="bd5cb-142">À partir de hello `username@#######:~$` invite, utilisez hello suivant des exemples de commande toolist hello :</span><span class="sxs-lookup"><span data-stu-id="bd5cb-142">From hello `username@#######:~$` prompt, use hello following command toolist hello samples:</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar
    ```

    <span data-ttu-id="bd5cb-143">Cette commande génère une liste hello d’exemple à partir de la section précédente de hello de ce document.</span><span class="sxs-lookup"><span data-stu-id="bd5cb-143">This command generates hello list of sample from hello previous section of this document.</span></span>

3. <span data-ttu-id="bd5cb-144">La commande suivante de hello utilisation aide tooget sur un exemple spécifique.</span><span class="sxs-lookup"><span data-stu-id="bd5cb-144">Use hello following command tooget help on a specific sample.</span></span> <span data-ttu-id="bd5cb-145">Dans ce cas, hello **wordcount** exemple :</span><span class="sxs-lookup"><span data-stu-id="bd5cb-145">In this case, hello **wordcount** sample:</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount
    ```

    <span data-ttu-id="bd5cb-146">Hello message suivant s’affiche :</span><span class="sxs-lookup"><span data-stu-id="bd5cb-146">You receive hello following message:</span></span>

        Usage: wordcount <in> [<in>...] <out>

    <span data-ttu-id="bd5cb-147">Ce message indique que vous pouvez fournir plusieurs chemins d’entrée pour les documents source hello.</span><span class="sxs-lookup"><span data-stu-id="bd5cb-147">This message indicates that you can provide several input paths for hello source documents.</span></span> <span data-ttu-id="bd5cb-148">chemin d’accès de la dernière Hello est où la sortie de hello (nombre de mots dans des documents source hello) est stocké.</span><span class="sxs-lookup"><span data-stu-id="bd5cb-148">hello final path is where hello output (count of words in hello source documents) is stored.</span></span>

4. <span data-ttu-id="bd5cb-149">Utilisez hello suivant toocount tous les mots Bonjour blocs-notes de Leonardo Da Vinci, qui sont fournies comme exemples de données avec votre cluster :</span><span class="sxs-lookup"><span data-stu-id="bd5cb-149">Use hello following toocount all words in hello Notebooks of Leonardo Da Vinci, which are provided as sample data with your cluster:</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount /example/data/gutenberg/davinci.txt /example/data/davinciwordcount
    ```

    <span data-ttu-id="bd5cb-150">L’entrée de ce travail est lue à partir de `/example/data/gutenberg/davinci.txt`.</span><span class="sxs-lookup"><span data-stu-id="bd5cb-150">Input for this job is read from `/example/data/gutenberg/davinci.txt`.</span></span> <span data-ttu-id="bd5cb-151">La sortie de cet exemple est stockée dans `/example/data/davinciwordcount`.</span><span class="sxs-lookup"><span data-stu-id="bd5cb-151">Output for this example is stored in `/example/data/davinciwordcount`.</span></span> <span data-ttu-id="bd5cb-152">Les deux chemins d’accès sont situés sur le stockage par défaut pour le cluster hello, pas le système de fichiers local hello.</span><span class="sxs-lookup"><span data-stu-id="bd5cb-152">Both paths are located on default storage for hello cluster, not hello local file system.</span></span>

   > [!NOTE]
   > <span data-ttu-id="bd5cb-153">Comme indiqué dans l’aide de hello pour exemple wordcount de hello, vous pouvez également spécifier plusieurs fichiers d’entrée.</span><span class="sxs-lookup"><span data-stu-id="bd5cb-153">As noted in hello help for hello wordcount sample, you could also specify multiple input files.</span></span> <span data-ttu-id="bd5cb-154">Par exemple, `hadoop jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount /example/data/gutenberg/davinci.txt /example/data/gutenberg/ulysses.txt /example/data/twowordcount` compte les mots figurant dans les fichiers davinci.txt et ulysses.txt.</span><span class="sxs-lookup"><span data-stu-id="bd5cb-154">For example, `hadoop jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount /example/data/gutenberg/davinci.txt /example/data/gutenberg/ulysses.txt /example/data/twowordcount` would count words in both davinci.txt and ulysses.txt.</span></span>

5. <span data-ttu-id="bd5cb-155">Une fois que hello est terminée, utilisez hello après la sortie de commande tooview hello :</span><span class="sxs-lookup"><span data-stu-id="bd5cb-155">Once hello job completes, use hello following command tooview hello output:</span></span>

    ```bash
    hdfs dfs -cat /example/data/davinciwordcount/*
    ```

    <span data-ttu-id="bd5cb-156">Cette commande concatène tous les fichiers de sortie hello produits par la tâche de hello.</span><span class="sxs-lookup"><span data-stu-id="bd5cb-156">This command concatenates all hello output files produced by hello job.</span></span> <span data-ttu-id="bd5cb-157">Il affiche la console de toohello sortie hello.</span><span class="sxs-lookup"><span data-stu-id="bd5cb-157">It displays hello output toohello console.</span></span> <span data-ttu-id="bd5cb-158">Hello est similaire toohello suivant texte de sortie :</span><span class="sxs-lookup"><span data-stu-id="bd5cb-158">hello output is similar toohello following text:</span></span>

        zum     1
        zur     1
        zwanzig 1
        zweite  1

    <span data-ttu-id="bd5cb-159">Chaque ligne représente un mot et le nombre de fois où elle s’est produite dans hello les données d’entrée.</span><span class="sxs-lookup"><span data-stu-id="bd5cb-159">Each line represents a word and how many times it occurred in hello input data.</span></span>

## <a name="hello-sudoku-example"></a><span data-ttu-id="bd5cb-160">exemple de Sudoku Hello</span><span class="sxs-lookup"><span data-stu-id="bd5cb-160">hello Sudoku example</span></span>

<span data-ttu-id="bd5cb-161">[Sudoku](https://en.wikipedia.org/wiki/Sudoku) est un puzzle logique composé de 3 x 3 grilles.</span><span class="sxs-lookup"><span data-stu-id="bd5cb-161">[Sudoku](https://en.wikipedia.org/wiki/Sudoku) is a logic puzzle made up of nine 3x3 grids.</span></span> <span data-ttu-id="bd5cb-162">Certaines des cellules de grille de hello ont des nombres, tandis que d’autres sont vides, hello vise toosolve pour les cellules vides hello.</span><span class="sxs-lookup"><span data-stu-id="bd5cb-162">Some cells in hello grid have numbers, while others are blank, and hello goal is toosolve for hello blank cells.</span></span> <span data-ttu-id="bd5cb-163">lien précédent de Hello possède plus d’informations sur les puzzle hello, mais hello cet exemple vise toosolve pour les cellules vides hello.</span><span class="sxs-lookup"><span data-stu-id="bd5cb-163">hello previous link has more information on hello puzzle, but hello purpose of this sample is toosolve for hello blank cells.</span></span> <span data-ttu-id="bd5cb-164">Par conséquent, notre entrée doit être un fichier qui se trouve dans hello suivant le format :</span><span class="sxs-lookup"><span data-stu-id="bd5cb-164">So our input should be a file that is in hello following format:</span></span>

* <span data-ttu-id="bd5cb-165">Neuf lignes de neuf colonnes</span><span class="sxs-lookup"><span data-stu-id="bd5cb-165">Nine rows of nine columns</span></span>
* <span data-ttu-id="bd5cb-166">Chaque colonne peut contenir un nombre ou `?` (qui indique une cellule vide)</span><span class="sxs-lookup"><span data-stu-id="bd5cb-166">Each column can contain either a number or `?` (which indicates a blank cell)</span></span>
* <span data-ttu-id="bd5cb-167">Les cellules sont séparées par un espace</span><span class="sxs-lookup"><span data-stu-id="bd5cb-167">Cells are separated by a space</span></span>

<span data-ttu-id="bd5cb-168">Il existe un certain tooconstruct moyen Sudoku jeux ; Vous ne pouvez pas répéter un nombre dans une colonne ou ligne.</span><span class="sxs-lookup"><span data-stu-id="bd5cb-168">There is a certain way tooconstruct Sudoku puzzles; you can't repeat a number in a column or row.</span></span> <span data-ttu-id="bd5cb-169">Il est un exemple sur un cluster HDInsight hello qui est correctement construit.</span><span class="sxs-lookup"><span data-stu-id="bd5cb-169">There's an example on hello HDInsight cluster that is properly constructed.</span></span> <span data-ttu-id="bd5cb-170">Il se trouve dans `/usr/hdp/*/hadoop/src/hadoop-mapreduce-project/hadoop-mapreduce-examples/src/main/java/org/apache/hadoop/examples/dancing/puzzle1.dta` et contient hello suivant du texte :</span><span class="sxs-lookup"><span data-stu-id="bd5cb-170">It is located at `/usr/hdp/*/hadoop/src/hadoop-mapreduce-project/hadoop-mapreduce-examples/src/main/java/org/apache/hadoop/examples/dancing/puzzle1.dta` and contains hello following text:</span></span>

    8 5 ? 3 9 ? ? ? ?
    ? ? 2 ? ? ? ? ? ?
    ? ? 6 ? 1 ? ? ? 2
    ? ? 4 ? ? 3 ? 5 9
    ? ? 8 9 ? 1 4 ? ?
    3 2 ? 4 ? ? 8 ? ?
    9 ? ? ? 8 ? 5 ? ?
    ? ? ? ? ? ? 2 ? ?
    ? ? ? ? 4 5 ? 7 8

<span data-ttu-id="bd5cb-171">Ce problème de l’exemple hello Sudoku exemple, par le biais de toorun utiliser hello la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="bd5cb-171">toorun this example problem through hello Sudoku example, use hello following command:</span></span>

```bash
yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar sudoku /usr/hdp/*/hadoop/src/hadoop-mapreduce-project/hadoop-mapreduce-examples/src/main/java/org/apache/hadoop/examples/dancing/puzzle1.dta
```

<span data-ttu-id="bd5cb-172">les résultats de Hello apparaissent toohello similaire après le texte :</span><span class="sxs-lookup"><span data-stu-id="bd5cb-172">hello results appear similar toohello following text:</span></span>

    8 5 1 3 9 2 6 4 7
    4 3 2 6 7 8 1 9 5
    7 9 6 5 1 4 3 8 2
    6 1 4 8 2 3 7 5 9
    5 7 8 9 6 1 4 2 3
    3 2 9 4 5 7 8 1 6
    9 4 7 2 8 6 5 3 1
    1 8 5 7 3 9 2 6 4
    2 6 3 1 4 5 9 7 8

## <a name="pi--example"></a><span data-ttu-id="bd5cb-173">Exemple de Pi (π)</span><span class="sxs-lookup"><span data-stu-id="bd5cb-173">Pi (π) example</span></span>

<span data-ttu-id="bd5cb-174">exemple de pi Hello utilise une statistique (quasi Monte Carlo) valeur de hello tooestimate la méthode de pi.</span><span class="sxs-lookup"><span data-stu-id="bd5cb-174">hello pi sample uses a statistical (quasi-Monte Carlo) method tooestimate hello value of pi.</span></span> <span data-ttu-id="bd5cb-175">Les points sont placés de manière aléatoire dans un carré unitaire.</span><span class="sxs-lookup"><span data-stu-id="bd5cb-175">Points are placed at random in a unit square.</span></span> <span data-ttu-id="bd5cb-176">carré de Hello contient également un cercle.</span><span class="sxs-lookup"><span data-stu-id="bd5cb-176">hello square also contains a circle.</span></span> <span data-ttu-id="bd5cb-177">probabilité que les points de hello se situent dans le cercle de hello Hello sont zone toohello égale de hello circle, pi/4.</span><span class="sxs-lookup"><span data-stu-id="bd5cb-177">hello probability that hello points fall within hello circle are equal toohello area of hello circle, pi/4.</span></span> <span data-ttu-id="bd5cb-178">valeur Hello de pi peut être estimée à partir de la valeur hello de 4R.</span><span class="sxs-lookup"><span data-stu-id="bd5cb-178">hello value of pi can be estimated from hello value of 4R.</span></span> <span data-ttu-id="bd5cb-179">R est le ratio hello du nombre de hello de points à l’intérieur des hello cercle toohello nombre total de points qui se trouvent dans le carré de hello.</span><span class="sxs-lookup"><span data-stu-id="bd5cb-179">R is hello ratio of hello number of points that are inside hello circle toohello total number of points that are within hello square.</span></span> <span data-ttu-id="bd5cb-180">exemple Hello plus grande hello de points utilisés, meilleure estimation de hello hello est.</span><span class="sxs-lookup"><span data-stu-id="bd5cb-180">hello larger hello sample of points used, hello better hello estimate is.</span></span>

<span data-ttu-id="bd5cb-181">Utilisez hello suivant toorun de commande de cet exemple.</span><span class="sxs-lookup"><span data-stu-id="bd5cb-181">Use hello following command toorun this sample.</span></span> <span data-ttu-id="bd5cb-182">Cette commande utilise les 16 mappages avec la valeur hello 10 000 000 exemples chaque tooestimate pi :</span><span class="sxs-lookup"><span data-stu-id="bd5cb-182">This command uses 16 maps with 10,000,000 samples each tooestimate hello value of pi:</span></span>

```bash
yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar pi 16 10000000
```

<span data-ttu-id="bd5cb-183">Hello valeur retournée par cette commande est similaire trop**3.14159155000000000000**.</span><span class="sxs-lookup"><span data-stu-id="bd5cb-183">hello value returned by this command is similar too**3.14159155000000000000**.</span></span> <span data-ttu-id="bd5cb-184">Pour les références, hello 10 premières décimales de pi sont 3.1415926535.</span><span class="sxs-lookup"><span data-stu-id="bd5cb-184">For references, hello first 10 decimal places of pi are 3.1415926535.</span></span>

## <a name="10-gb-greysort-example"></a><span data-ttu-id="bd5cb-185">Exemple de Greysort de 10 Go</span><span class="sxs-lookup"><span data-stu-id="bd5cb-185">10 GB Greysort example</span></span>

<span data-ttu-id="bd5cb-186">GraySort est un tri de benchmark.</span><span class="sxs-lookup"><span data-stu-id="bd5cb-186">GraySort is a benchmark sort.</span></span> <span data-ttu-id="bd5cb-187">métrique de Hello est le taux de tri hello (to/minute) qui est effectué lors du tri de grandes quantités de données, généralement un 100 To minimum.</span><span class="sxs-lookup"><span data-stu-id="bd5cb-187">hello metric is hello sort rate (TB/minute) that is achieved while sorting large amounts of data, usually a 100 TB minimum.</span></span>

<span data-ttu-id="bd5cb-188">Cet exemple utilise seulement 10 Go de données afin de pouvoir être exécuté relativement rapidement.</span><span class="sxs-lookup"><span data-stu-id="bd5cb-188">This sample uses a modest 10 GB of data so that it can be run relatively quickly.</span></span> <span data-ttu-id="bd5cb-189">Il utilise des applications de MapReduce hello développées par Owen O'Malley et Arun Murthy.</span><span class="sxs-lookup"><span data-stu-id="bd5cb-189">It uses hello MapReduce applications developed by Owen O'Malley and Arun Murthy.</span></span> <span data-ttu-id="bd5cb-190">Ces applications a gagné banc d’essai de hello annuel (« daytona ») à usage général téraoctet tri en 2009, avec un taux de 0.578 to/min (100 To 173 minutes).</span><span class="sxs-lookup"><span data-stu-id="bd5cb-190">These applications won hello annual general-purpose ("daytona") terabyte sort benchmark in 2009, with a rate of 0.578 TB/min (100 TB in 173 minutes).</span></span> <span data-ttu-id="bd5cb-191">Pour plus d’informations sur les autres tests de tri, consultez hello [Sortbenchmark](http://sortbenchmark.org/) site.</span><span class="sxs-lookup"><span data-stu-id="bd5cb-191">For more information on this and other sorting benchmarks, see hello [Sortbenchmark](http://sortbenchmark.org/) site.</span></span>

<span data-ttu-id="bd5cb-192">Cet exemple utilise trois ensembles de programmes MapReduce :</span><span class="sxs-lookup"><span data-stu-id="bd5cb-192">This sample uses three sets of MapReduce programs:</span></span>

* <span data-ttu-id="bd5cb-193">**TeraGen**: MapReduce d’un programme qui génère des lignes de données toosort</span><span class="sxs-lookup"><span data-stu-id="bd5cb-193">**TeraGen**: A MapReduce program that generates rows of data toosort</span></span>

* <span data-ttu-id="bd5cb-194">**TeraSort**: échantillonne les données d’entrée hello et utilise des données de hello MapReduce toosort dans un ordre total</span><span class="sxs-lookup"><span data-stu-id="bd5cb-194">**TeraSort**: Samples hello input data and uses MapReduce toosort hello data into a total order</span></span>

    <span data-ttu-id="bd5cb-195">TeraSort est un tri MapReduce standard, à l’exception d’un partitionneur personnalisé.</span><span class="sxs-lookup"><span data-stu-id="bd5cb-195">TeraSort is a standard MapReduce sort, except for a custom partitioner.</span></span> <span data-ttu-id="bd5cb-196">partitionneur de Hello utilise une liste triée des clés de n-1 échantillonnée qui définissent la plage de clés hello pour chaque réduire.</span><span class="sxs-lookup"><span data-stu-id="bd5cb-196">hello partitioner uses a sorted list of N-1 sampled keys that define hello key range for each reduce.</span></span> <span data-ttu-id="bd5cb-197">En particulier, toutes les clés de ces exemples [i-1] < = clé < exemple [i] sont envoyés tooreduce i.</span><span class="sxs-lookup"><span data-stu-id="bd5cb-197">In particular, all keys such that sample[i-1] <= key < sample[i] are sent tooreduce i.</span></span> <span data-ttu-id="bd5cb-198">Ce partitionneur garantit que les sorties hello de réduisent i est tous inférieur à réduire la sortie hello de i + 1.</span><span class="sxs-lookup"><span data-stu-id="bd5cb-198">This partitioner guarantees that hello outputs of reduce i are all less than hello output of reduce i+1.</span></span>

* <span data-ttu-id="bd5cb-199">**TeraValidate**: MapReduce d’un programme qui valide cette sortie hello est trié globalement</span><span class="sxs-lookup"><span data-stu-id="bd5cb-199">**TeraValidate**: A MapReduce program that validates that hello output is globally sorted</span></span>

    <span data-ttu-id="bd5cb-200">Il crée un mappage par fichier dans le répertoire de sortie hello, et chaque mappage garantit que chaque clé est inférieur ou égal toohello précédent.</span><span class="sxs-lookup"><span data-stu-id="bd5cb-200">It creates one map per file in hello output directory, and each map ensures that each key is less than or equal toohello previous one.</span></span> <span data-ttu-id="bd5cb-201">fonction de mappage Hello génère tout d’abord les enregistrements de hello et de la dernière clés de chaque fichier.</span><span class="sxs-lookup"><span data-stu-id="bd5cb-201">hello map function generates records of hello first and last keys of each file.</span></span> <span data-ttu-id="bd5cb-202">réduire la fonction Hello garantit que hello première clé de fichier i est supérieure à celle hello dernière d’i-1 de fichier.</span><span class="sxs-lookup"><span data-stu-id="bd5cb-202">hello reduce function ensures that hello first key of file i is greater than hello last key of file i-1.</span></span> <span data-ttu-id="bd5cb-203">Tous les problèmes sont signalés comme une sortie de hello réduire phase, avec des clés de hello qui sont en désordre.</span><span class="sxs-lookup"><span data-stu-id="bd5cb-203">Any problems are reported as an output of hello reduce phase, with hello keys that are out of order.</span></span>

<span data-ttu-id="bd5cb-204">Toogenerate des données, les étapes suivantes de hello utilisez trier, puis valider la sortie de hello :</span><span class="sxs-lookup"><span data-stu-id="bd5cb-204">Use hello following steps toogenerate data, sort, and then validate hello output:</span></span>

1. <span data-ttu-id="bd5cb-205">Générer de 10 Go de données, ce qui correspond au stockage par défaut du cluster stockée toohello HDInsight à `/example/data/10GB-sort-input`:</span><span class="sxs-lookup"><span data-stu-id="bd5cb-205">Generate 10 GB of data, which is stored toohello HDInsight cluster's default storage at `/example/data/10GB-sort-input`:</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar teragen -Dmapred.map.tasks=50 100000000 /example/data/10GB-sort-input
    ```

    <span data-ttu-id="bd5cb-206">Hello `-Dmapred.map.tasks` indique le nombre toouse de tâches de mappage pour ce travail Hadoop.</span><span class="sxs-lookup"><span data-stu-id="bd5cb-206">hello `-Dmapred.map.tasks` tells Hadoop how many map tasks toouse for this job.</span></span> <span data-ttu-id="bd5cb-207">paramètres de Hello deux derniers indiquer hello travail toocreate 10 Go de données et toostore à `/example/data/10GB-sort-input`.</span><span class="sxs-lookup"><span data-stu-id="bd5cb-207">hello final two parameters instruct hello job toocreate 10 GB of data and toostore it at `/example/data/10GB-sort-input`.</span></span>

2. <span data-ttu-id="bd5cb-208">Utilisez hello commande toosort hello données suivantes :</span><span class="sxs-lookup"><span data-stu-id="bd5cb-208">Use hello following command toosort hello data:</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar terasort -Dmapred.map.tasks=50 -Dmapred.reduce.tasks=25 /example/data/10GB-sort-input /example/data/10GB-sort-output
    ```

    <span data-ttu-id="bd5cb-209">Hello `-Dmapred.reduce.tasks` indique Hadoop combien réduire toouse de tâches pour le travail de hello.</span><span class="sxs-lookup"><span data-stu-id="bd5cb-209">hello `-Dmapred.reduce.tasks` tells Hadoop how many reduce tasks toouse for hello job.</span></span> <span data-ttu-id="bd5cb-210">paramètres de Hello deux derniers sont simplement hello entrée et les emplacements pour les données de sortie.</span><span class="sxs-lookup"><span data-stu-id="bd5cb-210">hello final two parameters are just hello input and output locations for data.</span></span>

3. <span data-ttu-id="bd5cb-211">Utilisez hello toovalidate hello données est générées par le tri de hello suivantes :</span><span class="sxs-lookup"><span data-stu-id="bd5cb-211">Use hello following toovalidate hello data generated by hello sort:</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar teravalidate -Dmapred.map.tasks=50 -Dmapred.reduce.tasks=25 /example/data/10GB-sort-output /example/data/10GB-sort-validate
    ```

## <a name="next-steps"></a><span data-ttu-id="bd5cb-212">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="bd5cb-212">Next steps</span></span>

<span data-ttu-id="bd5cb-213">À partir de cet article, vous avez appris comment exemples de hello toorun inclus avec hello clusters HDInsight de basés sur Linux.</span><span class="sxs-lookup"><span data-stu-id="bd5cb-213">From this article, you learned how toorun hello samples included with hello Linux-based HDInsight clusters.</span></span> <span data-ttu-id="bd5cb-214">Pour consulter des didacticiels sur l’utilisation de Pig, Hive et MapReduce hdinsight, consultez hello rubriques suivantes :</span><span class="sxs-lookup"><span data-stu-id="bd5cb-214">For tutorials about using Pig, Hive, and MapReduce with HDInsight, see hello following topics:</span></span>

* <span data-ttu-id="bd5cb-215">[Utilisation de Pig avec Hadoop sur HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="bd5cb-215">[Use Pig with Hadoop on HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="bd5cb-216">[Utilisation de Hive avec Hadoop sur HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="bd5cb-216">[Use Hive with Hadoop on HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="bd5cb-217">[Utilisation de MapReduce avec Hadoop sur HDInsight][hdinsight-use-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="bd5cb-217">[Use MapReduce with Hadoop on HDInsight][hdinsight-use-mapreduce]</span></span>

[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md
[hdinsight-sdk-documentation]: https://msdn.microsoft.com/library/azure/dn479185.aspx

[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-introduction]: hdinsight-hadoop-introduction.md



[hdinsight-samples]: hdinsight-run-samples.md

[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md
