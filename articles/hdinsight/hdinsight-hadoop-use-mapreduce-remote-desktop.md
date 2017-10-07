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
# <a name="use-mapreduce-in-hadoop-on-hdinsight-with-remote-desktop"></a>Utilisation de MapReduce dans Hadoop sur HDInsight avec le Bureau à distance
[!INCLUDE [mapreduce-selector](../../includes/hdinsight-selector-use-mapreduce.md)]

Dans cet article, vous découvrez comment tooconnect tooa Hadoop dans HDInsight cluster à l’aide de bureau à distance et puis exécutez les tâches MapReduce à l’aide des commandes de Hadoop hello.

> [!IMPORTANT]
> Le Bureau à distance n’est disponible que sur les clusters HDInsight Windows. Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure. Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).
>
> Pour HDInsight 3.4 ou supérieure, consultez [MapReduce utilisation avec SSH](hdinsight-hadoop-use-mapreduce-ssh.md) pour plus d’informations sur la connexion de cluster HDInsight de toohello et l’exécution des tâches MapReduce.

## <a id="prereq"></a>Configuration requise
toocomplete hello étapes décrites dans cet article, vous devez suivant de hello :

* un cluster HDInsight basé sur Windows (Hadoop sur HDInsight)
* Un ordinateur client avec Windows 10, Windows 8 ou Windows 7

## <a id="connect"></a>Connexion avec le Bureau à distance
Activer le Bureau à distance pour le cluster HDInsight de hello, puis connecter tooit en suivant les instructions de hello sur [connecter clusters tooHDInsight à l’aide du protocole RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).

## <a id="hadoop"></a>Utilisez la commande de Hadoop hello
Lorsque vous êtes bureau toohello connecté pour le cluster HDInsight de hello, utilisez hello suivant les étapes toorun une tâche MapReduce à l’aide des commandes de Hadoop hello :

1. À partir du bureau de HDInsight hello, démarrer hello **ligne de commande Hadoop**. Cette opération ouvre une nouvelle invite de commandes Bonjour **c:\apps\dist\hadoop-&lt;numéro de version >** active.

   > [!NOTE]
   > numéro de version Hello change à mesure que Hadoop est mis à jour. Hello **HADOOP_HOME** variable d’environnement peut être le chemin d’accès de toofind utilisé hello. Par exemple, `cd %HADOOP_HOME%` répertoire Hadoop toohello modifications répertoires, sans que vous ayez un numéro de version tooknow hello.
   >
   >
2. toouse hello **Hadoop** toorun un travail MapReduce d’exemple de commande, utilisez hello de commande suivante :

        hadoop jar hadoop-mapreduce-examples.jar wordcount wasb:///example/data/gutenberg/davinci.txt wasb:///example/data/WordCountOutput

    Cela démarre hello **wordcount** (classe), qui est contenue dans hello **hadoop-mapreduce-Examples.jar** fichier hello répertoire en cours. En tant qu’entrée, elle utilise hello **wasb://example/data/gutenberg/davinci.txt** document et la sortie est stocké au niveau : **wasb : / / / exemple/données/WordCountOutput**.

   > [!NOTE]
   > Pour plus d’informations sur ces données d’exemple de travail et hello MapReduce, consultez <a href="hdinsight-use-mapreduce.md">MapReduce utilisation dans HDInsight Hadoop</a>.
   >
   >
3. travail de Hello émet des détails comme il est traité, et il retourne des informations similaires qui suivent toohello fois hello terminée :

        File Input Format Counters
        Bytes Read=1395666
        File Output Format Counters
        Bytes Written=337623
4. Lors de la tâche de hello est terminée, utilisez hello suivant des fichiers de sortie commande toolist hello stockés sur **wasb://example/data/WordCountOutput**:

        hadoop fs -ls wasb:///example/data/WordCountOutput

    Cela devrait afficher deux fichiers, **_SUCCESS** et **part-r-00000**. Hello **partie-r-00000** fichier contient la sortie de hello pour ce travail.

   > [!NOTE]
   > Certaines tâches MapReduce peuvent fractionner les résultats hello entre plusieurs **partie-r-###** fichiers. Dans ce cas, utilisez hello ### suffixe d’ordre de hello tooindicate des fichiers de hello.
   >
   >
5. tooview hello de sortie, utilisez hello de commande suivante :

        hadoop fs -cat wasb:///example/data/WordCountOutput/part-r-00000

    Cela affiche une liste de mots hello contenus dans hello **wasb://example/data/gutenberg/davinci.txt** fichier, en même temps que le nombre de hello de chaque mot s’est produite. Hello Voici un exemple de données hello qui seront contenus dans le fichier de hello :

        wreathed        3
        wreathing       1
        wreaths         1
        wrecked         3
        wrenching       1
        wretched        6
        wriggling       1

## <a id="summary"></a>Résumé
Comme vous pouvez le voir, hello Hadoop commande fournit un moyen simple de toorun tâches MapReduce sur un cluster HDInsight, puis la sortie de travail vue hello.

## <a id="nextsteps"></a>Étapes suivantes
Pour obtenir des informations générales sur les tâches MapReduce dans HDInsight :

* [Utilisation de MapReduce dans Hadoop HDInsight](hdinsight-use-mapreduce.md)

Pour plus d’informations sur d’autres méthodes de travail avec Hadoop sur HDInsight :

* [Utilisation de Hive avec Hadoop sur HDInsight](hdinsight-use-hive.md)
* [Utilisation de Pig avec Hadoop sur HDInsight](hdinsight-use-pig.md)
