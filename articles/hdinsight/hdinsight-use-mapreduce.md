---
title: aaaMapReduce avec Hadoop dans HDInsight | Documents Microsoft
description: "Découvrez comment toorun MapReduce travaux sur Hadoop dans des clusters HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 7f321501-d62c-4ffc-b5d6-102ecba6dd76
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/26/2017
ms.author: larryfr
ms.openlocfilehash: 0cf7ad0e6769e678be64f9e4ec8ed7a214ab7af2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-mapreduce-in-hadoop-on-hdinsight"></a>Utilisation de MapReduce sur Hadoop sur HDInsight

Découvrez comment toorun MapReduce travaux sur les clusters HDInsight. Utilisez hello suivant hello toodiscover de table que MapReduce peut être utilisé avec HDInsight de différentes manières :

| **Élément à utiliser...** | **.. .toodo cela** | ...avec ce **système d’exploitation cluster** | ...depuis ce **système d’exploitation cluster** |
|:--- |:--- |:--- |:--- |
| [SSH](hdinsight-hadoop-use-mapreduce-ssh.md) |Utiliser la commande de Hadoop hello via **SSH** |Linux |Linux, Unix, Mac OS X ou Windows |
| [REST](hdinsight-hadoop-use-mapreduce-curl.md) |Envoi de la tâche de hello à distance à l’aide de **reste** (exemples utilisent cURL) |Linux ou Windows |Linux, Unix, Mac OS X ou Windows |
| [Windows PowerShell](hdinsight-hadoop-use-mapreduce-powershell.md) |Envoi de la tâche de hello à distance à l’aide de **Windows PowerShell** |Linux ou Windows |Windows |
| [Bureau à distance](hdinsight-hadoop-use-mapreduce-remote-desktop.md) (HDInsight 3.2 et 3.3) |Utiliser la commande de Hadoop hello via **Bureau à distance** |Windows |Windows |

> [!IMPORTANT]
> Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure. Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

## <a id="whatis"></a>Qu’est-ce que MapReduce ?

Hadoop MapReduce est une infrastructure logicielle qui permet d'écrire des tâches traitant d'importantes quantités de données. Données d’entrée sont divisées en segments indépendants, qui sont ensuite traitées en parallèle sur les nœuds hello dans votre cluster. Une tâche MapReduce se compose de deux fonctions :

* **Mappeur**: il consomme les données d'entrée, les analyse (généralement avec les opérations de tri et de filtre) et émet des tuples (paires clé-valeur)

* **RÉDUCTEUR**: consomme des tuples émis par le mappeur de hello et effectue une opération de synthèse qui crée un résultat plus petit, combiné à partir de données de mappeur de hello

Un exemple de tâche MapReduce base word count est illustré dans hello suivant schéma :

![HDI.WordCountDiagram][image-hdi-wordcountdiagram]

sortie Hello de ce travail est un nombre du nombre de fois où chaque mot s’est produite dans le texte hello qui ont été analysée.

* le Mappeur Hello prend chaque ligne hello texte d’entrée en tant qu’entrée et la décompose en mots. Il émet une clé/valeur paire chaque fois qu’un mot se produit de word de hello est suivie par un 1. sortie de Hello est triée avant de l’envoyer tooreducer.
* Réducteur de Hello additionne ces nombres individuels pour chaque mot et émet une paire clé/valeur unique qui contient le mot hello suivi par somme hello de ses occurrences.

MapReduce peut être implémenté dans plusieurs langues. Java est l’implémentation la plus courante hello et est utilisé à titre de démonstration dans ce document.

## <a name="development-languages"></a>Langues de développement

Langages ou des infrastructures qui sont basés sur Java et hello Machine virtuelle peut être exécuté directement comme une tâche MapReduce. exemple Hello utilisé dans ce document est une application Java MapReduce. Les langages autres que Java, comme C#, Python ou des exécutables autonomes, doivent utiliser la diffusion en continu Hadoop.

Diffusion en continu Hadoop communique avec le Mappeur hello et du réducteur STDIN et STDOUT. Réducteur de mappeur de hello lire les données une ligne à la fois de STDIN et écrire hello sortie tooSTDOUT. Chaque ligne de lecture ou émis par réducteur et le Mappeur hello doit être au format hello d’une paire clé/valeur séparée par un caractère de tabulation :

    [key]/t[value]

Pour plus d’informations, consultez [Diffusion en continu Hadoop](http://hadoop.apache.org/docs/r1.2.1/streaming.html).

Pour obtenir des exemples d’utilisation de diffusion en continu hdinsight Hadoop, consultez hello suivant des documents :

* [Développement de tâches MapReduce C#](hdinsight-hadoop-dotnet-csharp-mapreduce-streaming.md)

* [Développement de tâches MapReduce Python](hdinsight-hadoop-streaming-python.md)

## <a id="data"></a>Exemple de données

HDInsight fournit différents jeux de données d’exemple, qui sont stockées dans hello `/example/data` et `/HdiSamples` active. Ces répertoires sont dans le stockage par défaut hello pour votre cluster. Dans ce document, nous utilisons hello `/example/data/gutenberg/davinci.txt` fichier. Ce fichier contient des blocs-notes hello de Leonardo Da Vinci.

## <a id="job"></a>Exemple MapReduce

Un exemple d’application de comptage de mots MapReduce est inclus dans votre cluster HDInsight. Cet exemple se trouve dans `/example/jars/hadoop-mapreduce-examples.jar` sur le stockage par défaut hello pour votre cluster.

Hello suivant le code Java est source de hello Hello application MapReduce contenue dans hello `hadoop-mapreduce-examples.jar` fichier :

```java
package org.apache.hadoop.examples;

import java.io.IOException;
import java.util.StringTokenizer;

import org.apache.hadoop.conf.Configuration;
import org.apache.hadoop.fs.Path;
import org.apache.hadoop.io.IntWritable;
import org.apache.hadoop.io.Text;
import org.apache.hadoop.mapreduce.Job;
import org.apache.hadoop.mapreduce.Mapper;
import org.apache.hadoop.mapreduce.Reducer;
import org.apache.hadoop.mapreduce.lib.input.FileInputFormat;
import org.apache.hadoop.mapreduce.lib.output.FileOutputFormat;
import org.apache.hadoop.util.GenericOptionsParser;

public class WordCount {

    public static class TokenizerMapper
        extends Mapper<Object, Text, Text, IntWritable>{

    private final static IntWritable one = new IntWritable(1);
    private Text word = new Text();

    public void map(Object key, Text value, Context context
                    ) throws IOException, InterruptedException {
        StringTokenizer itr = new StringTokenizer(value.toString());
        while (itr.hasMoreTokens()) {
        word.set(itr.nextToken());
        context.write(word, one);
        }
    }
    }

    public static class IntSumReducer
        extends Reducer<Text,IntWritable,Text,IntWritable> {
    private IntWritable result = new IntWritable();

    public void reduce(Text key, Iterable<IntWritable> values,
                        Context context
                        ) throws IOException, InterruptedException {
        int sum = 0;
        for (IntWritable val : values) {
        sum += val.get();
        }
        result.set(sum);
        context.write(key, result);
    }
    }

    public static void main(String[] args) throws Exception {
    Configuration conf = new Configuration();
    String[] otherArgs = new GenericOptionsParser(conf, args).getRemainingArgs();
    if (otherArgs.length != 2) {
        System.err.println("Usage: wordcount <in> <out>");
        System.exit(2);
    }
    Job job = new Job(conf, "word count");
    job.setJarByClass(WordCount.class);
    job.setMapperClass(TokenizerMapper.class);
    job.setCombinerClass(IntSumReducer.class);
    job.setReducerClass(IntSumReducer.class);
    job.setOutputKeyClass(Text.class);
    job.setOutputValueClass(IntWritable.class);
    FileInputFormat.addInputPath(job, new Path(otherArgs[0]));
    FileOutputFormat.setOutputPath(job, new Path(otherArgs[1]));
    System.exit(job.waitForCompletion(true) ? 0 : 1);
    }
}
```

Pour obtenir des instructions toowrite vos propres applications MapReduce, consultez hello suivant des documents :

* [Développement d’applications MapReduce en Java pour HDInsight](hdinsight-develop-deploy-java-mapreduce-linux.md)

* [Développement d’applications MapReduce en Python pour HDInsight](hdinsight-hadoop-streaming-python.md)

## <a id="run"></a>Exécutez hello MapReduce

HDInsight peut exécuter des tâches HiveQL de différentes manières. Utilisez hello suivant toodecide table quelle méthode vous consiste, puis suivez le lien hello pour une procédure pas à pas.

| **Élément à utiliser...** | **.. .toodo cela** | ...avec ce **système d’exploitation cluster** | ...depuis ce **système d’exploitation cluster** |
|:--- |:--- |:--- |:--- |
| [SSH](hdinsight-hadoop-use-mapreduce-ssh.md) |Utiliser la commande de Hadoop hello via **SSH** |Linux |Linux, Unix, Mac OS X ou Windows |
| [Curl](hdinsight-hadoop-use-mapreduce-curl.md) |Envoi de la tâche de hello à distance à l’aide de **REST** |Linux ou Windows |Linux, Unix, Mac OS X ou Windows |
| [Windows PowerShell](hdinsight-hadoop-use-mapreduce-powershell.md) |Envoi de la tâche de hello à distance à l’aide de **Windows PowerShell** |Linux ou Windows |Windows |
| [Bureau à distance](hdinsight-hadoop-use-mapreduce-remote-desktop.md) (HDInsight 3.2 et 3.3) |Utiliser la commande de Hadoop hello via **Bureau à distance** |Windows |Windows |

> [!IMPORTANT]
> Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure. Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

## <a id="nextsteps"></a>Étapes suivantes

toolearn en savoir plus sur l’utilisation des données dans HDInsight, consultez hello suivant des documents :

* [Développement de programmes MapReduce en Java pour HDInsight](hdinsight-develop-deploy-java-mapreduce-linux.md)

* [Développement de programmes MapReduce de diffusion en continu Python pour HDInsight](hdinsight-hadoop-streaming-python.md)

* [Développement de tâches MapReduce Scalding avec Apache Hadoop dans HDInsight](hdinsight-hadoop-mapreduce-scalding.md)

* [Utilisation de Hive avec HDInsight][hdinsight-use-hive]

* [Utilisation de Pig avec HDInsight][hdinsight-use-pig]


[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-develop-mapreduce-jobs]: hdinsight-develop-deploy-java-mapreduce-linux.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md


[powershell-install-configure]: /powershell/azureps-cmdlets-docs

[image-hdi-wordcountdiagram]: ./media/hdinsight-use-mapreduce/HDI.WordCountDiagram.gif
