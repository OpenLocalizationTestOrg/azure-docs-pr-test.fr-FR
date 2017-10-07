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
# <a name="run-hello-mapreduce-examples-included-in-hdinsight"></a>Exécuter les exemples de MapReduce hello inclus dans HDInsight

[!INCLUDE [samples-selector](../../includes/hdinsight-run-samples-selector.md)]

Découvrez comment obtenir des exemples toorun hello MapReduce inclus avec Hadoop dans HDInsight.

## <a name="prerequisites"></a>Composants requis

* **Un cluster HDInsight** : consultez la rubrique [Bien démarrer avec Hadoop avec Hive dans HDInsight sur Linux](hdinsight-hadoop-linux-tutorial-get-started.md)

    > [!IMPORTANT]
    > Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure. Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

* **Client SSH** : pour en savoir plus, voir [Utilisation de SSH avec Hadoop Linux sur HDInsight depuis Linux, Unix ou OS XH](hdinsight-hadoop-linux-use-ssh-unix.md).

## <a name="hello-mapreduce-examples"></a>exemples de MapReduce Hello

**Emplacement**: exemples de hello se trouvent sur hello cluster HDInsight à `/usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar`.

**Contenu**: hello suivant exemples contenu dans cette archive :

* `aggregatewordcount`: Un agrégat basé programme mapreduce qui compte les mots hello dans les fichiers d’entrée hello.
* `aggregatewordhist`: Un agrégat basé programme mapreduce qui calcule l’histogramme hello de mots hello dans les fichiers d’entrée hello.
* `bbp`: Un programme mapreduce qui utilise Bailey-Borwein-Plouffe toocompute exact de chiffres de Pi.
* `dbcount`: Un travail d’exemple qui compte les journaux de page d’affichage hello stockés dans une base de données.
* `distbbp`: Un programme mapreduce qui utilise une formule toocompute BBP-type exact des bits de Pi.
* `grep`: Un programme mapreduce qui compte hello correspond à des expressions régulières dans l’entrée de hello.
* `join` : un travail qui effectue une jonction sur des jeux de données triés, à partition égale.
* `multifilewc` : un travail qui compte les mots de plusieurs fichiers.
* `pentomino`: Une vignette mapreduce portant des solutions toofind programme toopentomino problèmes.
* `pi` : un programme mapreduce qui estime la valeur de Pi à l’aide de la méthode quasi Monte Carlo.
* `randomtextwriter` : un programme mapreduce qui écrit 10 Go de données textuelles aléatoires par nœud.
* `randomwriter` : un programme mapreduce qui écrit 10 Go de données aléatoires par nœud.
* `secondarysort`: Phase de réduire un exemple de définition d’un toohello secondaire du tri.
* `sort`: Un programme mapreduce qui trie des données hello écrites par hello d’écriture aléatoire.
* `sudoku` : un solveur de sudoku.
* `teragen`: Générer des données pour hello terasort.
* `terasort`: Exécutez hello terasort.
* `teravalidate` : vérification des résultats du programme terasort.
* `wordcount`: Un programme mapreduce qui compte les mots hello dans les fichiers d’entrée hello.
* `wordmean`: Un programme mapreduce qui compte la longueur moyenne de hello de mots hello dans les fichiers d’entrée hello.
* `wordmedian`: Un programme mapreduce qui compte la longueur de la médiane hello de mots hello dans les fichiers d’entrée hello.
* `wordstandarddeviation`: Un programme mapreduce qui compte écart hello de longueur hello de mots hello dans les fichiers d’entrée hello.

**Le code source**: code Source pour ces exemples est incluse sur hello cluster HDInsight à `/usr/hdp/2.2.4.9-1/hadoop/src/hadoop-mapreduce-project/hadoop-mapreduce-examples`.

> [!NOTE]
> Hello `2.2.4.9-1` Bonjour le chemin d’accès est la version hello Hello Hortonworks Data Platform pour le cluster HDInsight de hello et peut être différente pour votre cluster.

## <a name="run-hello-wordcount-example"></a>Exécuter l’exemple wordcount de hello

1. Se connecter tooHDInsight à l’aide de SSH. Pour en savoir plus, voir [Utilisation de SSH avec Hadoop Linux sur HDInsight depuis Linux, Unix ou OS X](hdinsight-hadoop-linux-use-ssh-unix.md).

2. À partir de hello `username@#######:~$` invite, utilisez hello suivant des exemples de commande toolist hello :

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar
    ```

    Cette commande génère une liste hello d’exemple à partir de la section précédente de hello de ce document.

3. La commande suivante de hello utilisation aide tooget sur un exemple spécifique. Dans ce cas, hello **wordcount** exemple :

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount
    ```

    Hello message suivant s’affiche :

        Usage: wordcount <in> [<in>...] <out>

    Ce message indique que vous pouvez fournir plusieurs chemins d’entrée pour les documents source hello. chemin d’accès de la dernière Hello est où la sortie de hello (nombre de mots dans des documents source hello) est stocké.

4. Utilisez hello suivant toocount tous les mots Bonjour blocs-notes de Leonardo Da Vinci, qui sont fournies comme exemples de données avec votre cluster :

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount /example/data/gutenberg/davinci.txt /example/data/davinciwordcount
    ```

    L’entrée de ce travail est lue à partir de `/example/data/gutenberg/davinci.txt`. La sortie de cet exemple est stockée dans `/example/data/davinciwordcount`. Les deux chemins d’accès sont situés sur le stockage par défaut pour le cluster hello, pas le système de fichiers local hello.

   > [!NOTE]
   > Comme indiqué dans l’aide de hello pour exemple wordcount de hello, vous pouvez également spécifier plusieurs fichiers d’entrée. Par exemple, `hadoop jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount /example/data/gutenberg/davinci.txt /example/data/gutenberg/ulysses.txt /example/data/twowordcount` compte les mots figurant dans les fichiers davinci.txt et ulysses.txt.

5. Une fois que hello est terminée, utilisez hello après la sortie de commande tooview hello :

    ```bash
    hdfs dfs -cat /example/data/davinciwordcount/*
    ```

    Cette commande concatène tous les fichiers de sortie hello produits par la tâche de hello. Il affiche la console de toohello sortie hello. Hello est similaire toohello suivant texte de sortie :

        zum     1
        zur     1
        zwanzig 1
        zweite  1

    Chaque ligne représente un mot et le nombre de fois où elle s’est produite dans hello les données d’entrée.

## <a name="hello-sudoku-example"></a>exemple de Sudoku Hello

[Sudoku](https://en.wikipedia.org/wiki/Sudoku) est un puzzle logique composé de 3 x 3 grilles. Certaines des cellules de grille de hello ont des nombres, tandis que d’autres sont vides, hello vise toosolve pour les cellules vides hello. lien précédent de Hello possède plus d’informations sur les puzzle hello, mais hello cet exemple vise toosolve pour les cellules vides hello. Par conséquent, notre entrée doit être un fichier qui se trouve dans hello suivant le format :

* Neuf lignes de neuf colonnes
* Chaque colonne peut contenir un nombre ou `?` (qui indique une cellule vide)
* Les cellules sont séparées par un espace

Il existe un certain tooconstruct moyen Sudoku jeux ; Vous ne pouvez pas répéter un nombre dans une colonne ou ligne. Il est un exemple sur un cluster HDInsight hello qui est correctement construit. Il se trouve dans `/usr/hdp/*/hadoop/src/hadoop-mapreduce-project/hadoop-mapreduce-examples/src/main/java/org/apache/hadoop/examples/dancing/puzzle1.dta` et contient hello suivant du texte :

    8 5 ? 3 9 ? ? ? ?
    ? ? 2 ? ? ? ? ? ?
    ? ? 6 ? 1 ? ? ? 2
    ? ? 4 ? ? 3 ? 5 9
    ? ? 8 9 ? 1 4 ? ?
    3 2 ? 4 ? ? 8 ? ?
    9 ? ? ? 8 ? 5 ? ?
    ? ? ? ? ? ? 2 ? ?
    ? ? ? ? 4 5 ? 7 8

Ce problème de l’exemple hello Sudoku exemple, par le biais de toorun utiliser hello la commande suivante :

```bash
yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar sudoku /usr/hdp/*/hadoop/src/hadoop-mapreduce-project/hadoop-mapreduce-examples/src/main/java/org/apache/hadoop/examples/dancing/puzzle1.dta
```

les résultats de Hello apparaissent toohello similaire après le texte :

    8 5 1 3 9 2 6 4 7
    4 3 2 6 7 8 1 9 5
    7 9 6 5 1 4 3 8 2
    6 1 4 8 2 3 7 5 9
    5 7 8 9 6 1 4 2 3
    3 2 9 4 5 7 8 1 6
    9 4 7 2 8 6 5 3 1
    1 8 5 7 3 9 2 6 4
    2 6 3 1 4 5 9 7 8

## <a name="pi--example"></a>Exemple de Pi (π)

exemple de pi Hello utilise une statistique (quasi Monte Carlo) valeur de hello tooestimate la méthode de pi. Les points sont placés de manière aléatoire dans un carré unitaire. carré de Hello contient également un cercle. probabilité que les points de hello se situent dans le cercle de hello Hello sont zone toohello égale de hello circle, pi/4. valeur Hello de pi peut être estimée à partir de la valeur hello de 4R. R est le ratio hello du nombre de hello de points à l’intérieur des hello cercle toohello nombre total de points qui se trouvent dans le carré de hello. exemple Hello plus grande hello de points utilisés, meilleure estimation de hello hello est.

Utilisez hello suivant toorun de commande de cet exemple. Cette commande utilise les 16 mappages avec la valeur hello 10 000 000 exemples chaque tooestimate pi :

```bash
yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar pi 16 10000000
```

Hello valeur retournée par cette commande est similaire trop**3.14159155000000000000**. Pour les références, hello 10 premières décimales de pi sont 3.1415926535.

## <a name="10-gb-greysort-example"></a>Exemple de Greysort de 10 Go

GraySort est un tri de benchmark. métrique de Hello est le taux de tri hello (to/minute) qui est effectué lors du tri de grandes quantités de données, généralement un 100 To minimum.

Cet exemple utilise seulement 10 Go de données afin de pouvoir être exécuté relativement rapidement. Il utilise des applications de MapReduce hello développées par Owen O'Malley et Arun Murthy. Ces applications a gagné banc d’essai de hello annuel (« daytona ») à usage général téraoctet tri en 2009, avec un taux de 0.578 to/min (100 To 173 minutes). Pour plus d’informations sur les autres tests de tri, consultez hello [Sortbenchmark](http://sortbenchmark.org/) site.

Cet exemple utilise trois ensembles de programmes MapReduce :

* **TeraGen**: MapReduce d’un programme qui génère des lignes de données toosort

* **TeraSort**: échantillonne les données d’entrée hello et utilise des données de hello MapReduce toosort dans un ordre total

    TeraSort est un tri MapReduce standard, à l’exception d’un partitionneur personnalisé. partitionneur de Hello utilise une liste triée des clés de n-1 échantillonnée qui définissent la plage de clés hello pour chaque réduire. En particulier, toutes les clés de ces exemples [i-1] < = clé < exemple [i] sont envoyés tooreduce i. Ce partitionneur garantit que les sorties hello de réduisent i est tous inférieur à réduire la sortie hello de i + 1.

* **TeraValidate**: MapReduce d’un programme qui valide cette sortie hello est trié globalement

    Il crée un mappage par fichier dans le répertoire de sortie hello, et chaque mappage garantit que chaque clé est inférieur ou égal toohello précédent. fonction de mappage Hello génère tout d’abord les enregistrements de hello et de la dernière clés de chaque fichier. réduire la fonction Hello garantit que hello première clé de fichier i est supérieure à celle hello dernière d’i-1 de fichier. Tous les problèmes sont signalés comme une sortie de hello réduire phase, avec des clés de hello qui sont en désordre.

Toogenerate des données, les étapes suivantes de hello utilisez trier, puis valider la sortie de hello :

1. Générer de 10 Go de données, ce qui correspond au stockage par défaut du cluster stockée toohello HDInsight à `/example/data/10GB-sort-input`:

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar teragen -Dmapred.map.tasks=50 100000000 /example/data/10GB-sort-input
    ```

    Hello `-Dmapred.map.tasks` indique le nombre toouse de tâches de mappage pour ce travail Hadoop. paramètres de Hello deux derniers indiquer hello travail toocreate 10 Go de données et toostore à `/example/data/10GB-sort-input`.

2. Utilisez hello commande toosort hello données suivantes :

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar terasort -Dmapred.map.tasks=50 -Dmapred.reduce.tasks=25 /example/data/10GB-sort-input /example/data/10GB-sort-output
    ```

    Hello `-Dmapred.reduce.tasks` indique Hadoop combien réduire toouse de tâches pour le travail de hello. paramètres de Hello deux derniers sont simplement hello entrée et les emplacements pour les données de sortie.

3. Utilisez hello toovalidate hello données est générées par le tri de hello suivantes :

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar teravalidate -Dmapred.map.tasks=50 -Dmapred.reduce.tasks=25 /example/data/10GB-sort-output /example/data/10GB-sort-validate
    ```

## <a name="next-steps"></a>Étapes suivantes

À partir de cet article, vous avez appris comment exemples de hello toorun inclus avec hello clusters HDInsight de basés sur Linux. Pour consulter des didacticiels sur l’utilisation de Pig, Hive et MapReduce hdinsight, consultez hello rubriques suivantes :

* [Utilisation de Pig avec Hadoop sur HDInsight][hdinsight-use-pig]
* [Utilisation de Hive avec Hadoop sur HDInsight][hdinsight-use-hive]
* [Utilisation de MapReduce avec Hadoop sur HDInsight][hdinsight-use-mapreduce]

[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md
[hdinsight-sdk-documentation]: https://msdn.microsoft.com/library/azure/dn479185.aspx

[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-introduction]: hdinsight-hadoop-introduction.md



[hdinsight-samples]: hdinsight-run-samples.md

[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md
