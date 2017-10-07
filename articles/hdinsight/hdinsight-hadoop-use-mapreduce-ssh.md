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
# <a name="use-mapreduce-with-hadoop-on-hdinsight-with-ssh"></a>Utilisation de MapReduce avec Hadoop sur HDInsight avec SSH

[!INCLUDE [mapreduce-selector](../../includes/hdinsight-selector-use-mapreduce.md)]

Découvrez comment toosubmit MapReduce travaux à partir d’un tooHDInsight de connexion Secure Shell (SSH).

> [!NOTE]
> Si vous êtes déjà familiarisé avec Hadoop basé sur Linux à l’aide de serveurs, mais vous tooHDInsight nouvelle, consultez [HDInsight de basés sur Linux conseils](hdinsight-hadoop-linux-information.md).

## <a id="prereq"></a>Configuration requise

* un cluster HDInsight basé sur Linux (Hadoop sur HDInsight)

  > [!IMPORTANT]
  > Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure. Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

* Un client SSH. Pour en savoir plus, consultez [Utilisation de SSH avec HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

## <a id="ssh"></a>Connexion avec SSH

Connectez le cluster toohello à l’aide de SSH. Par exemple, hello commande suivante connecte à cluster tooa nommé **myhdinsight**:

```bash
ssh admin@myhdinsight-ssh.azurehdinsight.net
```

**Si vous utilisez un certificat de clé pour l’authentification SSH**, vous devrez peut-être emplacement de hello toospecify de clé privée de hello sur votre système client, par exemple :

```bash
ssh -i ~/mykey.key admin@myhdinsight-ssh.azurehdinsight.net
```

**Si vous utilisez un mot de passe pour l’authentification SSH**, vous devez tooprovide hello un mot de passe lorsque vous y êtes invité.

Pour en savoir plus sur l’utilisation de SSH avec HDInsight, voir [Utilisation de SSH avec HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

## <a id="hadoop"></a>Utilisation de commandes Hadoop

1. Après que vous être connecté toohello HDInsight cluster, utilisez hello suivant commande toostart une tâche MapReduce :

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount /example/data/gutenberg/davinci.txt /example/data/WordCountOutput
    ```

    Cette commande démarre hello `wordcount` (classe), qui est contenue dans hello `hadoop-mapreduce-examples.jar` fichier. Il utilise hello `/example/data/gutenberg/davinci.txt` document comme entrée et de sortie est stockée au niveau `/example/data/WordCountOutput`.

    > [!NOTE]
    > Pour plus d’informations sur ces données d’exemple de travail et hello MapReduce, consultez [MapReduce utilisation dans Hadoop dans HDInsight](hdinsight-use-mapreduce.md).

2. travail de Hello émet des détails comme il traite et il retourne des informations toohello similaire après le texte hello travail une fois :

        File Input Format Counters
        Bytes Read=1395666
        File Output Format Counters
        Bytes Written=337623

3. Lors de la tâche de hello est terminée, utilisez hello fichiers de sortie de commande toolist hello suivants :

    ```bash
    hdfs dfs -ls /example/data/WordCountOutput
    ```

    Cette commande affiche deux fichiers, `_SUCCESS` et `part-r-00000`. Hello `part-r-00000` fichier contient la sortie de hello pour ce travail.

    > [!NOTE]
    > Certaines tâches MapReduce peuvent fractionner les résultats hello entre plusieurs **partie-r-###** fichiers. Dans ce cas, utilisez hello ### suffixe d’ordre de hello tooindicate des fichiers de hello.

4. tooview hello de sortie, utilisez hello de commande suivante :

    ```bash
    hdfs dfs -cat /example/data/WordCountOutput/part-r-00000
    ```

    Cette commande affiche une liste de mots hello contenus Bonjour **wasb://example/data/gutenberg/davinci.txt** hello de fichiers et de nombre de fois où chaque mot s’est produite. Hello texte suivant est un exemple de données hello contenues dans le fichier de hello :

        wreathed        3
        wreathing       1
        wreaths         1
        wrecked         3
        wrenching       1
        wretched        6
        wriggling       1

## <a id="summary"></a>Résumé

Comme vous pouvez le voir, les commandes de Hadoop fournissent un moyen simple de toorun tâches MapReduce dans un cluster HDInsight, puis la sortie de travail vue hello.

## <a id="nextsteps"></a>Étapes suivantes

Pour obtenir des informations générales sur les tâches MapReduce dans HDInsight :

* [Utilisation de MapReduce dans Hadoop HDInsight](hdinsight-use-mapreduce.md)

Pour plus d’informations sur d’autres méthodes de travail avec Hadoop sur HDInsight :

* [Utilisation de Hive avec Hadoop sur HDInsight](hdinsight-use-hive.md)
* [Utilisation de Pig avec Hadoop sur HDInsight](hdinsight-use-pig.md)
