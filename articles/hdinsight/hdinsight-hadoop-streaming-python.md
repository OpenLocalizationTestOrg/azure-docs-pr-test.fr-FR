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
# <a name="develop-python-streaming-mapreduce-programs-for-hdinsight"></a>Développer des programmes MapReduce de diffusion en continu Python pour HDInsight

Découvrez comment toouse Python dans les opérations MapReduce de diffusion en continu. Hadoop fournit une API de diffusion en continu pour MapReduce qui permet de vous mappez toowrite et réduire les fonctions dans les langages autres que Java. Bonjour étapes de ce document implémentent hello carte et réduisent les composants de Python.

## <a name="prerequisites"></a>Composants requis

* Un cluster Hadoop Linux sur HDInsight

  > [!IMPORTANT]
  > étapes de Hello dans ce document nécessitent un cluster HDInsight qui utilise Linux. Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure. Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

* Un éditeur de texte

  > [!IMPORTANT]
  > éditeur de texte Hello doit utiliser LF comme fin de ligne hello. À l’aide d’une fin de ligne de CRLF provoque des erreurs lors de l’exécution du travail MapReduce de hello sur les clusters HDInsight de basés sur Linux.

* Hello `ssh` et `scp` commandes, ou [Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview?view=azurermps-3.8.0)

## <a name="word-count"></a>Nombre de mots

Cet exemple illustre un nombre de mots de base dans un mappeur et un réducteur Python. le Mappeur Hello sauts de phrases en mots individuels et réducteur de hello agrège les mots hello et nombres de sortie de hello tooproduce.

Hello suivant organigramme illustre ce qui se produit lors du mappage de hello et réduire les phases.

![illustration du processus de mapreduce hello](./media/hdinsight-hadoop-streaming-python/HDI.WordCountDiagram.png)

## <a name="streaming-mapreduce"></a>Diffusion en continu de MapReduce

Hadoop vous permet de toospecify un fichier qui contient le mappage de hello et réduire la logique utilisée par une tâche. exigences spécifiques Hello hello mapper et réduire logique sont :

* **D’entrée**: hello de mappage et de réduire les composants doivent lire les données d’entrée de STDIN.
* **Sortie**: hello de mappage et de réduire les composants doivent écrire tooSTDOUT de données de sortie.
* **Format de données**: données hello consommées et le produit doivent être une paire clé/valeur, séparée par un caractère de tabulation.

Python peut gérer facilement ces exigences à l’aide de hello `sys` tooread de module de STDIN et d’utiliser `print` tooprint tooSTDOUT. Hello tâche restante est simplement mise en forme les données de salutation avec un onglet (`\t`) caractère entre hello clé et la valeur.

## <a name="create-hello-mapper-and-reducer"></a>Créer réducteur et le Mappeur hello

1. Créez un fichier nommé `mapper.py` et utilisez hello suivant le code en tant que contenu de hello :

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

2. Créez un fichier nommé **reducer.py** et utilisez hello suivant le code en tant que contenu de hello :

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

## <a name="run-using-powershell"></a>Exécuter à l’aide de PowerShell

tooensure que vos fichiers ont les fins de ligne droite de hello, hello utilisez PowerShell script suivant :

[!code-powershell[main](../../powershell_scripts/hdinsight/streaming-python/streaming-python.ps1?range=138-140)]

Utilisez hello PowerShell script tooupload hello fichiers suivants, exécuter la tâche de hello et afficher la sortie de hello :

[!code-powershell[main](../../powershell_scripts/hdinsight/streaming-python/streaming-python.ps1?range=5-134)]

## <a name="run-from-an-ssh-session"></a>Exécution à partir d’une session SSH

1. À partir de votre environnement de développement, de hello le même répertoire que `mapper.py` et `reducer.py` fichiers, utilisez hello de commande suivante :

    ```bash
    scp mapper.py reducer.py username@clustername-ssh.azurehdinsight.net:
    ```

    Remplacez `username` avec le nom d’utilisateur SSH hello pour votre cluster, et `clustername` avec le nom hello de votre cluster.

    Cette commande copie les fichiers hello à partir du nœud principal du toohello hello système local.

    > [!NOTE]
    > Si vous avez utilisé un toosecure de mot de passe de votre compte SSH, vous êtes invité pour un mot de passe hello. Si vous avez utilisé une clé SSH, vous avez peut-être toouse hello `-i` clé privée des toohello de chemin d’accès au paramètre et hello. Par exemple, `scp -i /path/to/private/key mapper.py reducer.py username@clustername-ssh.azurehdinsight.net:`.

2. Se connecter toohello cluster à l’aide de SSH :

    ```bash
    ssh username@clustername-ssh.azurehdinsight.net`
    ```

    Pour en savoir plus, consultez [Utilisation de SSH avec HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

3. REDUCER.py et tooensure hello mapper.py ont hello corriger les fins de ligne, utilisez hello suivant de commandes :

    ```bash
    perl -pi -e 's/\r\n/\n/g' mapper.py
    perl -pi -e 's/\r\n/\n/g' reducer.py
    ```

4. Utilisez hello suivant la tâche de commande toostart hello MapReduce.

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-streaming.jar -files mapper.py,reducer.py -mapper mapper.py -reducer reducer.py -input /example/data/gutenberg/davinci.txt -output /example/wordcountout
    ```

    Cette commande a hello composants suivants :

   * **hadoop-streaming.jar**: utilisé lors de l’exécution d’opérations de diffusion en contenu MapReduce. Il interagit Hadoop avec code MapReduce externe hello que vous fournissez.

   * **-fichiers**: ajoute hello spécifié travail MapReduce de toohello des fichiers.

   * **-Mappeur**: Hadoop indique quel fichier toouse comme hello mappeur.

   * **-RÉDUCTEUR**: Hadoop indique quel fichier toouse comme hello du réducteur.

   * **-d’entrée**: fichier d’entrée hello que nous devons compter les mots à partir de.

   * **-sortie**: répertoire hello hello de sortie est écrite dans.

    Comme la tâche MapReduce de hello fonctionne, les processus de hello s’affiche sous forme de pourcentages.

        15/02/05 19:01:04 INFO mapreduce.Job:  map 0% reduce 0%    15/02/05 19:01:16 INFO mapreduce.Job:  map 100% reduce 0%    15/02/05 19:01:27 INFO mapreduce.Job:  map 100% reduce 100%


5. tooview hello de sortie, utilisez hello de commande suivante :

    ```bash
    hdfs dfs -text /example/wordcountout/part-00000
    ```

    Cette commande affiche une liste de mots et le nombre de fois word de hello s’est produite.

## <a name="next-steps"></a>Étapes suivantes

Maintenant que vous avez appris comment toouse MapRedcue de diffusion en continu des travaux avec HDInsight, utilisez hello suivant les liens tooexplore autres toowork manières avec Azure HDInsight.

* [Utilisation de Hive avec HDInsight](hdinsight-use-hive.md)
* [Utilisation de Pig avec HDInsight](hdinsight-use-pig.md)
* [Utilisation des tâches MapReduce avec HDInsight](hdinsight-use-mapreduce.md)
