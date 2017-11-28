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
# <a name="use-mapreduce-in-hadoop-on-hdinsight"></a><span data-ttu-id="6d9bb-103">Utilisation de MapReduce sur Hadoop sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="6d9bb-103">Use MapReduce in Hadoop on HDInsight</span></span>

<span data-ttu-id="6d9bb-104">Découvrez comment toorun MapReduce travaux sur les clusters HDInsight.</span><span class="sxs-lookup"><span data-stu-id="6d9bb-104">Learn how toorun MapReduce jobs on HDInsight clusters.</span></span> <span data-ttu-id="6d9bb-105">Utilisez hello suivant hello toodiscover de table que MapReduce peut être utilisé avec HDInsight de différentes manières :</span><span class="sxs-lookup"><span data-stu-id="6d9bb-105">Use hello following table toodiscover hello various ways that MapReduce can be used with HDInsight:</span></span>

| <span data-ttu-id="6d9bb-106">**Élément à utiliser...**</span><span class="sxs-lookup"><span data-stu-id="6d9bb-106">**Use this**...</span></span> | <span data-ttu-id="6d9bb-107">**.. .toodo cela**</span><span class="sxs-lookup"><span data-stu-id="6d9bb-107">**...toodo this**</span></span> | <span data-ttu-id="6d9bb-108">...avec ce **système d’exploitation cluster**</span><span class="sxs-lookup"><span data-stu-id="6d9bb-108">...with this **cluster operating system**</span></span> | <span data-ttu-id="6d9bb-109">...depuis ce **système d’exploitation cluster**</span><span class="sxs-lookup"><span data-stu-id="6d9bb-109">...from this **client operating system**</span></span> |
|:--- |:--- |:--- |:--- |
| [<span data-ttu-id="6d9bb-110">SSH</span><span class="sxs-lookup"><span data-stu-id="6d9bb-110">SSH</span></span>](hdinsight-hadoop-use-mapreduce-ssh.md) |<span data-ttu-id="6d9bb-111">Utiliser la commande de Hadoop hello via **SSH**</span><span class="sxs-lookup"><span data-stu-id="6d9bb-111">Use hello Hadoop command through **SSH**</span></span> |<span data-ttu-id="6d9bb-112">Linux</span><span class="sxs-lookup"><span data-stu-id="6d9bb-112">Linux</span></span> |<span data-ttu-id="6d9bb-113">Linux, Unix, Mac OS X ou Windows</span><span class="sxs-lookup"><span data-stu-id="6d9bb-113">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="6d9bb-114">REST</span><span class="sxs-lookup"><span data-stu-id="6d9bb-114">REST</span></span>](hdinsight-hadoop-use-mapreduce-curl.md) |<span data-ttu-id="6d9bb-115">Envoi de la tâche de hello à distance à l’aide de **reste** (exemples utilisent cURL)</span><span class="sxs-lookup"><span data-stu-id="6d9bb-115">Submit hello job remotely by using **REST** (examples use cURL)</span></span> |<span data-ttu-id="6d9bb-116">Linux ou Windows</span><span class="sxs-lookup"><span data-stu-id="6d9bb-116">Linux or Windows</span></span> |<span data-ttu-id="6d9bb-117">Linux, Unix, Mac OS X ou Windows</span><span class="sxs-lookup"><span data-stu-id="6d9bb-117">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="6d9bb-118">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="6d9bb-118">Windows PowerShell</span></span>](hdinsight-hadoop-use-mapreduce-powershell.md) |<span data-ttu-id="6d9bb-119">Envoi de la tâche de hello à distance à l’aide de **Windows PowerShell**</span><span class="sxs-lookup"><span data-stu-id="6d9bb-119">Submit hello job remotely by using **Windows PowerShell**</span></span> |<span data-ttu-id="6d9bb-120">Linux ou Windows</span><span class="sxs-lookup"><span data-stu-id="6d9bb-120">Linux or Windows</span></span> |<span data-ttu-id="6d9bb-121">Windows</span><span class="sxs-lookup"><span data-stu-id="6d9bb-121">Windows</span></span> |
| <span data-ttu-id="6d9bb-122">[Bureau à distance](hdinsight-hadoop-use-mapreduce-remote-desktop.md) (HDInsight 3.2 et 3.3)</span><span class="sxs-lookup"><span data-stu-id="6d9bb-122">[Remote Desktop](hdinsight-hadoop-use-mapreduce-remote-desktop.md) (HDInsight 3.2 and 3.3)</span></span> |<span data-ttu-id="6d9bb-123">Utiliser la commande de Hadoop hello via **Bureau à distance**</span><span class="sxs-lookup"><span data-stu-id="6d9bb-123">Use hello Hadoop command through **Remote Desktop**</span></span> |<span data-ttu-id="6d9bb-124">Windows</span><span class="sxs-lookup"><span data-stu-id="6d9bb-124">Windows</span></span> |<span data-ttu-id="6d9bb-125">Windows</span><span class="sxs-lookup"><span data-stu-id="6d9bb-125">Windows</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="6d9bb-126">Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure.</span><span class="sxs-lookup"><span data-stu-id="6d9bb-126">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="6d9bb-127">Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="6d9bb-127">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <span data-ttu-id="6d9bb-128"><a id="whatis"></a>Qu’est-ce que MapReduce ?</span><span class="sxs-lookup"><span data-stu-id="6d9bb-128"><a id="whatis"></a>What is MapReduce</span></span>

<span data-ttu-id="6d9bb-129">Hadoop MapReduce est une infrastructure logicielle qui permet d'écrire des tâches traitant d'importantes quantités de données.</span><span class="sxs-lookup"><span data-stu-id="6d9bb-129">Hadoop MapReduce is a software framework for writing jobs that process vast amounts of data.</span></span> <span data-ttu-id="6d9bb-130">Données d’entrée sont divisées en segments indépendants, qui sont ensuite traitées en parallèle sur les nœuds hello dans votre cluster.</span><span class="sxs-lookup"><span data-stu-id="6d9bb-130">Input data is split into independent chunks, which are then processed in parallel across hello nodes in your cluster.</span></span> <span data-ttu-id="6d9bb-131">Une tâche MapReduce se compose de deux fonctions :</span><span class="sxs-lookup"><span data-stu-id="6d9bb-131">A MapReduce job consists of two functions:</span></span>

* <span data-ttu-id="6d9bb-132">**Mappeur**: il consomme les données d'entrée, les analyse (généralement avec les opérations de tri et de filtre) et émet des tuples (paires clé-valeur)</span><span class="sxs-lookup"><span data-stu-id="6d9bb-132">**Mapper**: Consumes input data, analyzes it (usually with filter and sorting operations), and emits tuples (key-value pairs)</span></span>

* <span data-ttu-id="6d9bb-133">**RÉDUCTEUR**: consomme des tuples émis par le mappeur de hello et effectue une opération de synthèse qui crée un résultat plus petit, combiné à partir de données de mappeur de hello</span><span class="sxs-lookup"><span data-stu-id="6d9bb-133">**Reducer**: Consumes tuples emitted by hello Mapper and performs a summary operation that creates a smaller, combined result from hello Mapper data</span></span>

<span data-ttu-id="6d9bb-134">Un exemple de tâche MapReduce base word count est illustré dans hello suivant schéma :</span><span class="sxs-lookup"><span data-stu-id="6d9bb-134">A basic word count MapReduce job example is illustrated in hello following diagram:</span></span>

![HDI.WordCountDiagram][image-hdi-wordcountdiagram]

<span data-ttu-id="6d9bb-136">sortie Hello de ce travail est un nombre du nombre de fois où chaque mot s’est produite dans le texte hello qui ont été analysée.</span><span class="sxs-lookup"><span data-stu-id="6d9bb-136">hello output of this job is a count of how many times each word occurred in hello text that was analyzed.</span></span>

* <span data-ttu-id="6d9bb-137">le Mappeur Hello prend chaque ligne hello texte d’entrée en tant qu’entrée et la décompose en mots.</span><span class="sxs-lookup"><span data-stu-id="6d9bb-137">hello mapper takes each line from hello input text as an input and breaks it into words.</span></span> <span data-ttu-id="6d9bb-138">Il émet une clé/valeur paire chaque fois qu’un mot se produit de word de hello est suivie par un 1.</span><span class="sxs-lookup"><span data-stu-id="6d9bb-138">It emits a key/value pair each time a word occurs of hello word is followed by a 1.</span></span> <span data-ttu-id="6d9bb-139">sortie de Hello est triée avant de l’envoyer tooreducer.</span><span class="sxs-lookup"><span data-stu-id="6d9bb-139">hello output is sorted before sending it tooreducer.</span></span>
* <span data-ttu-id="6d9bb-140">Réducteur de Hello additionne ces nombres individuels pour chaque mot et émet une paire clé/valeur unique qui contient le mot hello suivi par somme hello de ses occurrences.</span><span class="sxs-lookup"><span data-stu-id="6d9bb-140">hello reducer sums these individual counts for each word and emits a single key/value pair that contains hello word followed by hello sum of its occurrences.</span></span>

<span data-ttu-id="6d9bb-141">MapReduce peut être implémenté dans plusieurs langues.</span><span class="sxs-lookup"><span data-stu-id="6d9bb-141">MapReduce can be implemented in various languages.</span></span> <span data-ttu-id="6d9bb-142">Java est l’implémentation la plus courante hello et est utilisé à titre de démonstration dans ce document.</span><span class="sxs-lookup"><span data-stu-id="6d9bb-142">Java is hello most common implementation, and is used for demonstration purposes in this document.</span></span>

## <a name="development-languages"></a><span data-ttu-id="6d9bb-143">Langues de développement</span><span class="sxs-lookup"><span data-stu-id="6d9bb-143">Development languages</span></span>

<span data-ttu-id="6d9bb-144">Langages ou des infrastructures qui sont basés sur Java et hello Machine virtuelle peut être exécuté directement comme une tâche MapReduce.</span><span class="sxs-lookup"><span data-stu-id="6d9bb-144">Languages or frameworks that are based on Java and hello Java Virtual Machine can be ran directly as a MapReduce job.</span></span> <span data-ttu-id="6d9bb-145">exemple Hello utilisé dans ce document est une application Java MapReduce.</span><span class="sxs-lookup"><span data-stu-id="6d9bb-145">hello example used in this document is a Java MapReduce application.</span></span> <span data-ttu-id="6d9bb-146">Les langages autres que Java, comme C#, Python ou des exécutables autonomes, doivent utiliser la diffusion en continu Hadoop.</span><span class="sxs-lookup"><span data-stu-id="6d9bb-146">Non-Java languages, such as C#, Python, or standalone executables, must use Hadoop streaming.</span></span>

<span data-ttu-id="6d9bb-147">Diffusion en continu Hadoop communique avec le Mappeur hello et du réducteur STDIN et STDOUT.</span><span class="sxs-lookup"><span data-stu-id="6d9bb-147">Hadoop streaming communicates with hello mapper and reducer over STDIN and STDOUT.</span></span> <span data-ttu-id="6d9bb-148">Réducteur de mappeur de hello lire les données une ligne à la fois de STDIN et écrire hello sortie tooSTDOUT.</span><span class="sxs-lookup"><span data-stu-id="6d9bb-148">hello mapper and reducer read data a line at a time from STDIN, and write hello output tooSTDOUT.</span></span> <span data-ttu-id="6d9bb-149">Chaque ligne de lecture ou émis par réducteur et le Mappeur hello doit être au format hello d’une paire clé/valeur séparée par un caractère de tabulation :</span><span class="sxs-lookup"><span data-stu-id="6d9bb-149">Each line read or emitted by hello mapper and reducer must be in hello format of a key/value pair, delimited by a tab character:</span></span>

    [key]/t[value]

<span data-ttu-id="6d9bb-150">Pour plus d’informations, consultez [Diffusion en continu Hadoop](http://hadoop.apache.org/docs/r1.2.1/streaming.html).</span><span class="sxs-lookup"><span data-stu-id="6d9bb-150">For more information, see [Hadoop Streaming](http://hadoop.apache.org/docs/r1.2.1/streaming.html).</span></span>

<span data-ttu-id="6d9bb-151">Pour obtenir des exemples d’utilisation de diffusion en continu hdinsight Hadoop, consultez hello suivant des documents :</span><span class="sxs-lookup"><span data-stu-id="6d9bb-151">For examples of using Hadoop streaming with HDInsight, see hello following documents:</span></span>

* [<span data-ttu-id="6d9bb-152">Développement de tâches MapReduce C#</span><span class="sxs-lookup"><span data-stu-id="6d9bb-152">Develop C# MapReduce jobs</span></span>](hdinsight-hadoop-dotnet-csharp-mapreduce-streaming.md)

* [<span data-ttu-id="6d9bb-153">Développement de tâches MapReduce Python</span><span class="sxs-lookup"><span data-stu-id="6d9bb-153">Develop Python MapReduce jobs</span></span>](hdinsight-hadoop-streaming-python.md)

## <span data-ttu-id="6d9bb-154"><a id="data"></a>Exemple de données</span><span class="sxs-lookup"><span data-stu-id="6d9bb-154"><a id="data"></a>Example data</span></span>

<span data-ttu-id="6d9bb-155">HDInsight fournit différents jeux de données d’exemple, qui sont stockées dans hello `/example/data` et `/HdiSamples` active.</span><span class="sxs-lookup"><span data-stu-id="6d9bb-155">HDInsight provides various example data sets, which are stored in hello `/example/data` and `/HdiSamples` directory.</span></span> <span data-ttu-id="6d9bb-156">Ces répertoires sont dans le stockage par défaut hello pour votre cluster.</span><span class="sxs-lookup"><span data-stu-id="6d9bb-156">These directories are in hello default storage for your cluster.</span></span> <span data-ttu-id="6d9bb-157">Dans ce document, nous utilisons hello `/example/data/gutenberg/davinci.txt` fichier.</span><span class="sxs-lookup"><span data-stu-id="6d9bb-157">In this document, we use hello `/example/data/gutenberg/davinci.txt` file.</span></span> <span data-ttu-id="6d9bb-158">Ce fichier contient des blocs-notes hello de Leonardo Da Vinci.</span><span class="sxs-lookup"><span data-stu-id="6d9bb-158">This file contains hello notebooks of Leonardo Da Vinci.</span></span>

## <span data-ttu-id="6d9bb-159"><a id="job"></a>Exemple MapReduce</span><span class="sxs-lookup"><span data-stu-id="6d9bb-159"><a id="job"></a>Example MapReduce</span></span>

<span data-ttu-id="6d9bb-160">Un exemple d’application de comptage de mots MapReduce est inclus dans votre cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="6d9bb-160">An example MapReduce word count application is included with your HDInsight cluster.</span></span> <span data-ttu-id="6d9bb-161">Cet exemple se trouve dans `/example/jars/hadoop-mapreduce-examples.jar` sur le stockage par défaut hello pour votre cluster.</span><span class="sxs-lookup"><span data-stu-id="6d9bb-161">This example is located at `/example/jars/hadoop-mapreduce-examples.jar` on hello default storage for your cluster.</span></span>

<span data-ttu-id="6d9bb-162">Hello suivant le code Java est source de hello Hello application MapReduce contenue dans hello `hadoop-mapreduce-examples.jar` fichier :</span><span class="sxs-lookup"><span data-stu-id="6d9bb-162">hello following Java code is hello source of hello MapReduce application contained in hello `hadoop-mapreduce-examples.jar` file:</span></span>

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

<span data-ttu-id="6d9bb-163">Pour obtenir des instructions toowrite vos propres applications MapReduce, consultez hello suivant des documents :</span><span class="sxs-lookup"><span data-stu-id="6d9bb-163">For instructions toowrite your own MapReduce applications, see hello following documents:</span></span>

* [<span data-ttu-id="6d9bb-164">Développement d’applications MapReduce en Java pour HDInsight</span><span class="sxs-lookup"><span data-stu-id="6d9bb-164">Develop Java MapReduce applications for HDInsight</span></span>](hdinsight-develop-deploy-java-mapreduce-linux.md)

* [<span data-ttu-id="6d9bb-165">Développement d’applications MapReduce en Python pour HDInsight</span><span class="sxs-lookup"><span data-stu-id="6d9bb-165">Develop Python MapReduce applications for HDInsight</span></span>](hdinsight-hadoop-streaming-python.md)

## <span data-ttu-id="6d9bb-166"><a id="run"></a>Exécutez hello MapReduce</span><span class="sxs-lookup"><span data-stu-id="6d9bb-166"><a id="run"></a>Run hello MapReduce</span></span>

<span data-ttu-id="6d9bb-167">HDInsight peut exécuter des tâches HiveQL de différentes manières.</span><span class="sxs-lookup"><span data-stu-id="6d9bb-167">HDInsight can run HiveQL jobs by using various methods.</span></span> <span data-ttu-id="6d9bb-168">Utilisez hello suivant toodecide table quelle méthode vous consiste, puis suivez le lien hello pour une procédure pas à pas.</span><span class="sxs-lookup"><span data-stu-id="6d9bb-168">Use hello following table toodecide which method is right for you, then follow hello link for a walkthrough.</span></span>

| <span data-ttu-id="6d9bb-169">**Élément à utiliser...**</span><span class="sxs-lookup"><span data-stu-id="6d9bb-169">**Use this**...</span></span> | <span data-ttu-id="6d9bb-170">**.. .toodo cela**</span><span class="sxs-lookup"><span data-stu-id="6d9bb-170">**...toodo this**</span></span> | <span data-ttu-id="6d9bb-171">...avec ce **système d’exploitation cluster**</span><span class="sxs-lookup"><span data-stu-id="6d9bb-171">...with this **cluster operating system**</span></span> | <span data-ttu-id="6d9bb-172">...depuis ce **système d’exploitation cluster**</span><span class="sxs-lookup"><span data-stu-id="6d9bb-172">...from this **client operating system**</span></span> |
|:--- |:--- |:--- |:--- |
| [<span data-ttu-id="6d9bb-173">SSH</span><span class="sxs-lookup"><span data-stu-id="6d9bb-173">SSH</span></span>](hdinsight-hadoop-use-mapreduce-ssh.md) |<span data-ttu-id="6d9bb-174">Utiliser la commande de Hadoop hello via **SSH**</span><span class="sxs-lookup"><span data-stu-id="6d9bb-174">Use hello Hadoop command through **SSH**</span></span> |<span data-ttu-id="6d9bb-175">Linux</span><span class="sxs-lookup"><span data-stu-id="6d9bb-175">Linux</span></span> |<span data-ttu-id="6d9bb-176">Linux, Unix, Mac OS X ou Windows</span><span class="sxs-lookup"><span data-stu-id="6d9bb-176">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="6d9bb-177">Curl</span><span class="sxs-lookup"><span data-stu-id="6d9bb-177">Curl</span></span>](hdinsight-hadoop-use-mapreduce-curl.md) |<span data-ttu-id="6d9bb-178">Envoi de la tâche de hello à distance à l’aide de **REST**</span><span class="sxs-lookup"><span data-stu-id="6d9bb-178">Submit hello job remotely by using **REST**</span></span> |<span data-ttu-id="6d9bb-179">Linux ou Windows</span><span class="sxs-lookup"><span data-stu-id="6d9bb-179">Linux or Windows</span></span> |<span data-ttu-id="6d9bb-180">Linux, Unix, Mac OS X ou Windows</span><span class="sxs-lookup"><span data-stu-id="6d9bb-180">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="6d9bb-181">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="6d9bb-181">Windows PowerShell</span></span>](hdinsight-hadoop-use-mapreduce-powershell.md) |<span data-ttu-id="6d9bb-182">Envoi de la tâche de hello à distance à l’aide de **Windows PowerShell**</span><span class="sxs-lookup"><span data-stu-id="6d9bb-182">Submit hello job remotely by using **Windows PowerShell**</span></span> |<span data-ttu-id="6d9bb-183">Linux ou Windows</span><span class="sxs-lookup"><span data-stu-id="6d9bb-183">Linux or Windows</span></span> |<span data-ttu-id="6d9bb-184">Windows</span><span class="sxs-lookup"><span data-stu-id="6d9bb-184">Windows</span></span> |
| <span data-ttu-id="6d9bb-185">[Bureau à distance](hdinsight-hadoop-use-mapreduce-remote-desktop.md) (HDInsight 3.2 et 3.3)</span><span class="sxs-lookup"><span data-stu-id="6d9bb-185">[Remote Desktop](hdinsight-hadoop-use-mapreduce-remote-desktop.md) (HDInsight 3.2 and 3.3)</span></span> |<span data-ttu-id="6d9bb-186">Utiliser la commande de Hadoop hello via **Bureau à distance**</span><span class="sxs-lookup"><span data-stu-id="6d9bb-186">Use hello Hadoop command through **Remote Desktop**</span></span> |<span data-ttu-id="6d9bb-187">Windows</span><span class="sxs-lookup"><span data-stu-id="6d9bb-187">Windows</span></span> |<span data-ttu-id="6d9bb-188">Windows</span><span class="sxs-lookup"><span data-stu-id="6d9bb-188">Windows</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="6d9bb-189">Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure.</span><span class="sxs-lookup"><span data-stu-id="6d9bb-189">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="6d9bb-190">Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="6d9bb-190">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <span data-ttu-id="6d9bb-191"><a id="nextsteps"></a>Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6d9bb-191"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="6d9bb-192">toolearn en savoir plus sur l’utilisation des données dans HDInsight, consultez hello suivant des documents :</span><span class="sxs-lookup"><span data-stu-id="6d9bb-192">toolearn more about working with data in HDInsight, see hello following documents:</span></span>

* [<span data-ttu-id="6d9bb-193">Développement de programmes MapReduce en Java pour HDInsight</span><span class="sxs-lookup"><span data-stu-id="6d9bb-193">Develop Java MapReduce programs for HDInsight</span></span>](hdinsight-develop-deploy-java-mapreduce-linux.md)

* [<span data-ttu-id="6d9bb-194">Développement de programmes MapReduce de diffusion en continu Python pour HDInsight</span><span class="sxs-lookup"><span data-stu-id="6d9bb-194">Develop Python streaming MapReduce programs for HDInsight</span></span>](hdinsight-hadoop-streaming-python.md)

* [<span data-ttu-id="6d9bb-195">Développement de tâches MapReduce Scalding avec Apache Hadoop dans HDInsight</span><span class="sxs-lookup"><span data-stu-id="6d9bb-195">Develop Scalding MapReduce jobs with Apache Hadoop on HDInsight</span></span>](hdinsight-hadoop-mapreduce-scalding.md)

* <span data-ttu-id="6d9bb-196">[Utilisation de Hive avec HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="6d9bb-196">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>

* <span data-ttu-id="6d9bb-197">[Utilisation de Pig avec HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="6d9bb-197">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>


[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-develop-mapreduce-jobs]: hdinsight-develop-deploy-java-mapreduce-linux.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md


[powershell-install-configure]: /powershell/azureps-cmdlets-docs

[image-hdi-wordcountdiagram]: ./media/hdinsight-use-mapreduce/HDI.WordCountDiagram.gif
