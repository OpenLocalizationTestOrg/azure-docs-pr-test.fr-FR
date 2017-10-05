---
title: MapReduce avec Hadoop sur HDInsight | Microsoft Docs
description: "Apprenez à exécuter des tâches MapReduce sur Hadoop dans des clusters HDInsight."
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
ms.openlocfilehash: df8ac578a56de72df667b1fa7f90f981c79d9999
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="use-mapreduce-in-hadoop-on-hdinsight"></a><span data-ttu-id="ef3fa-103">Utilisation de MapReduce sur Hadoop sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="ef3fa-103">Use MapReduce in Hadoop on HDInsight</span></span>

<span data-ttu-id="ef3fa-104">Apprenez à exécuter des tâches MapReduce sur des clusters HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ef3fa-104">Learn how to run MapReduce jobs on HDInsight clusters.</span></span> <span data-ttu-id="ef3fa-105">Utilisez le tableau suivant pour découvrir les différentes façons d’utiliser MapReduce avec HDInsight :</span><span class="sxs-lookup"><span data-stu-id="ef3fa-105">Use the following table to discover the various ways that MapReduce can be used with HDInsight:</span></span>

| <span data-ttu-id="ef3fa-106">**Élément à utiliser...**</span><span class="sxs-lookup"><span data-stu-id="ef3fa-106">**Use this**...</span></span> | <span data-ttu-id="ef3fa-107">**...pour faire cela**</span><span class="sxs-lookup"><span data-stu-id="ef3fa-107">**...to do this**</span></span> | <span data-ttu-id="ef3fa-108">...avec ce **système d’exploitation cluster**</span><span class="sxs-lookup"><span data-stu-id="ef3fa-108">...with this **cluster operating system**</span></span> | <span data-ttu-id="ef3fa-109">...depuis ce **système d’exploitation cluster**</span><span class="sxs-lookup"><span data-stu-id="ef3fa-109">...from this **client operating system**</span></span> |
|:--- |:--- |:--- |:--- |
| [<span data-ttu-id="ef3fa-110">SSH</span><span class="sxs-lookup"><span data-stu-id="ef3fa-110">SSH</span></span>](hdinsight-hadoop-use-mapreduce-ssh.md) |<span data-ttu-id="ef3fa-111">Utilisation de la commande Hadoop via **SSH**</span><span class="sxs-lookup"><span data-stu-id="ef3fa-111">Use the Hadoop command through **SSH**</span></span> |<span data-ttu-id="ef3fa-112">Linux</span><span class="sxs-lookup"><span data-stu-id="ef3fa-112">Linux</span></span> |<span data-ttu-id="ef3fa-113">Linux, Unix, Mac OS X ou Windows</span><span class="sxs-lookup"><span data-stu-id="ef3fa-113">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="ef3fa-114">REST</span><span class="sxs-lookup"><span data-stu-id="ef3fa-114">REST</span></span>](hdinsight-hadoop-use-mapreduce-curl.md) |<span data-ttu-id="ef3fa-115">Envoyer la tâche à distance à l’aide de **REST** (dans les exemples, cURL est utilisé)</span><span class="sxs-lookup"><span data-stu-id="ef3fa-115">Submit the job remotely by using **REST** (examples use cURL)</span></span> |<span data-ttu-id="ef3fa-116">Linux ou Windows</span><span class="sxs-lookup"><span data-stu-id="ef3fa-116">Linux or Windows</span></span> |<span data-ttu-id="ef3fa-117">Linux, Unix, Mac OS X ou Windows</span><span class="sxs-lookup"><span data-stu-id="ef3fa-117">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="ef3fa-118">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="ef3fa-118">Windows PowerShell</span></span>](hdinsight-hadoop-use-mapreduce-powershell.md) |<span data-ttu-id="ef3fa-119">Envoyer la tâche à distance à l'aide de **Windows PowerShell**</span><span class="sxs-lookup"><span data-stu-id="ef3fa-119">Submit the job remotely by using **Windows PowerShell**</span></span> |<span data-ttu-id="ef3fa-120">Linux ou Windows</span><span class="sxs-lookup"><span data-stu-id="ef3fa-120">Linux or Windows</span></span> |<span data-ttu-id="ef3fa-121">Windows</span><span class="sxs-lookup"><span data-stu-id="ef3fa-121">Windows</span></span> |
| <span data-ttu-id="ef3fa-122">[Bureau à distance](hdinsight-hadoop-use-mapreduce-remote-desktop.md) (HDInsight 3.2 et 3.3)</span><span class="sxs-lookup"><span data-stu-id="ef3fa-122">[Remote Desktop](hdinsight-hadoop-use-mapreduce-remote-desktop.md) (HDInsight 3.2 and 3.3)</span></span> |<span data-ttu-id="ef3fa-123">Utilisation de la commande Hadoop via le **bureau à distance**</span><span class="sxs-lookup"><span data-stu-id="ef3fa-123">Use the Hadoop command through **Remote Desktop**</span></span> |<span data-ttu-id="ef3fa-124">Windows</span><span class="sxs-lookup"><span data-stu-id="ef3fa-124">Windows</span></span> |<span data-ttu-id="ef3fa-125">Windows</span><span class="sxs-lookup"><span data-stu-id="ef3fa-125">Windows</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="ef3fa-126">Linux est le seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure.</span><span class="sxs-lookup"><span data-stu-id="ef3fa-126">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="ef3fa-127">Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="ef3fa-127">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <span data-ttu-id="ef3fa-128"><a id="whatis"></a>Qu’est-ce que MapReduce ?</span><span class="sxs-lookup"><span data-stu-id="ef3fa-128"><a id="whatis"></a>What is MapReduce</span></span>

<span data-ttu-id="ef3fa-129">Hadoop MapReduce est une infrastructure logicielle qui permet d'écrire des tâches traitant d'importantes quantités de données.</span><span class="sxs-lookup"><span data-stu-id="ef3fa-129">Hadoop MapReduce is a software framework for writing jobs that process vast amounts of data.</span></span> <span data-ttu-id="ef3fa-130">Les données d'entrée sont divisées en blocs indépendants, qui sont ensuite traitées en parallèle sur les nœuds de votre cluster.</span><span class="sxs-lookup"><span data-stu-id="ef3fa-130">Input data is split into independent chunks, which are then processed in parallel across the nodes in your cluster.</span></span> <span data-ttu-id="ef3fa-131">Une tâche MapReduce se compose de deux fonctions :</span><span class="sxs-lookup"><span data-stu-id="ef3fa-131">A MapReduce job consists of two functions:</span></span>

* <span data-ttu-id="ef3fa-132">**Mappeur**: il consomme les données d'entrée, les analyse (généralement avec les opérations de tri et de filtre) et émet des tuples (paires clé-valeur)</span><span class="sxs-lookup"><span data-stu-id="ef3fa-132">**Mapper**: Consumes input data, analyzes it (usually with filter and sorting operations), and emits tuples (key-value pairs)</span></span>

* <span data-ttu-id="ef3fa-133">**Raccord de réduction**: il consomme les tuples émis par le Mappeur et effectue une opération de synthèse qui crée un résultat plus petit, combiné à partir des données du Mappeur</span><span class="sxs-lookup"><span data-stu-id="ef3fa-133">**Reducer**: Consumes tuples emitted by the Mapper and performs a summary operation that creates a smaller, combined result from the Mapper data</span></span>

<span data-ttu-id="ef3fa-134">Un exemple de tâche MapReduce de comptage de mots de base est illustré dans le diagramme suivant :</span><span class="sxs-lookup"><span data-stu-id="ef3fa-134">A basic word count MapReduce job example is illustrated in the following diagram:</span></span>

![HDI.WordCountDiagram][image-hdi-wordcountdiagram]

<span data-ttu-id="ef3fa-136">Le résultat de cette tâche indique le nombre d’occurrences de chaque mot dans le texte qui a été analysé.</span><span class="sxs-lookup"><span data-stu-id="ef3fa-136">The output of this job is a count of how many times each word occurred in the text that was analyzed.</span></span>

* <span data-ttu-id="ef3fa-137">Le mappeur prend chaque ligne du texte saisi en tant qu'entrée, et la divise en mots.</span><span class="sxs-lookup"><span data-stu-id="ef3fa-137">The mapper takes each line from the input text as an input and breaks it into words.</span></span> <span data-ttu-id="ef3fa-138">Il émet une paire clé/valeur pour chaque occurrence de mot ou si le mot est suivi d’un 1.</span><span class="sxs-lookup"><span data-stu-id="ef3fa-138">It emits a key/value pair each time a word occurs of the word is followed by a 1.</span></span> <span data-ttu-id="ef3fa-139">Le résultat est trié avant d'être envoyé au raccord de réduction.</span><span class="sxs-lookup"><span data-stu-id="ef3fa-139">The output is sorted before sending it to reducer.</span></span>
* <span data-ttu-id="ef3fa-140">Ce dernier calcule la somme du compte de mots, puis émet une seule paire clé/valeur contenant le mot défini, suivi par la somme de ses occurrences.</span><span class="sxs-lookup"><span data-stu-id="ef3fa-140">The reducer sums these individual counts for each word and emits a single key/value pair that contains the word followed by the sum of its occurrences.</span></span>

<span data-ttu-id="ef3fa-141">MapReduce peut être implémenté dans plusieurs langues.</span><span class="sxs-lookup"><span data-stu-id="ef3fa-141">MapReduce can be implemented in various languages.</span></span> <span data-ttu-id="ef3fa-142">Java est l'implémentation la plus courante. Ce langage est utilisé à titre d’exemple dans ce document.</span><span class="sxs-lookup"><span data-stu-id="ef3fa-142">Java is the most common implementation, and is used for demonstration purposes in this document.</span></span>

## <a name="development-languages"></a><span data-ttu-id="ef3fa-143">Langues de développement</span><span class="sxs-lookup"><span data-stu-id="ef3fa-143">Development languages</span></span>

<span data-ttu-id="ef3fa-144">Les langages ou infrastructures basés sur Java et la Machine virtuelle Java peuvent être exécutés directement comme une tâche MapReduce.</span><span class="sxs-lookup"><span data-stu-id="ef3fa-144">Languages or frameworks that are based on Java and the Java Virtual Machine can be ran directly as a MapReduce job.</span></span> <span data-ttu-id="ef3fa-145">L’exemple utilisé dans ce document est une application Java MapReduce.</span><span class="sxs-lookup"><span data-stu-id="ef3fa-145">The example used in this document is a Java MapReduce application.</span></span> <span data-ttu-id="ef3fa-146">Les langages autres que Java, comme C#, Python ou des exécutables autonomes, doivent utiliser la diffusion en continu Hadoop.</span><span class="sxs-lookup"><span data-stu-id="ef3fa-146">Non-Java languages, such as C#, Python, or standalone executables, must use Hadoop streaming.</span></span>

<span data-ttu-id="ef3fa-147">La diffusion en continu Hadoop communique avec le mappeur et le raccord de réduction via STDIN et STDOUT.</span><span class="sxs-lookup"><span data-stu-id="ef3fa-147">Hadoop streaming communicates with the mapper and reducer over STDIN and STDOUT.</span></span> <span data-ttu-id="ef3fa-148">Le mappeur et le raccord de réduction lisent les données ligne par ligne depuis STDIN et écrivent la sortie dans STDOUT.</span><span class="sxs-lookup"><span data-stu-id="ef3fa-148">The mapper and reducer read data a line at a time from STDIN, and write the output to STDOUT.</span></span> <span data-ttu-id="ef3fa-149">Chaque ligne lue ou émise par le mappeur et le raccord de réduction doit être au format d’une paire clé / valeur, délimitée par un caractère de tabulation :</span><span class="sxs-lookup"><span data-stu-id="ef3fa-149">Each line read or emitted by the mapper and reducer must be in the format of a key/value pair, delimited by a tab character:</span></span>

    [key]/t[value]

<span data-ttu-id="ef3fa-150">Pour plus d’informations, consultez [Diffusion en continu Hadoop](http://hadoop.apache.org/docs/r1.2.1/streaming.html).</span><span class="sxs-lookup"><span data-stu-id="ef3fa-150">For more information, see [Hadoop Streaming](http://hadoop.apache.org/docs/r1.2.1/streaming.html).</span></span>

<span data-ttu-id="ef3fa-151">Pour obtenir des exemples d’utilisation de diffusion en continu Hadoop avec HDInsight, consultez les documents suivants :</span><span class="sxs-lookup"><span data-stu-id="ef3fa-151">For examples of using Hadoop streaming with HDInsight, see the following documents:</span></span>

* [<span data-ttu-id="ef3fa-152">Développement de tâches MapReduce C#</span><span class="sxs-lookup"><span data-stu-id="ef3fa-152">Develop C# MapReduce jobs</span></span>](hdinsight-hadoop-dotnet-csharp-mapreduce-streaming.md)

* [<span data-ttu-id="ef3fa-153">Développement de tâches MapReduce Python</span><span class="sxs-lookup"><span data-stu-id="ef3fa-153">Develop Python MapReduce jobs</span></span>](hdinsight-hadoop-streaming-python.md)

## <span data-ttu-id="ef3fa-154"><a id="data"></a>Exemple de données</span><span class="sxs-lookup"><span data-stu-id="ef3fa-154"><a id="data"></a>Example data</span></span>

<span data-ttu-id="ef3fa-155">HDInsight propose différents exemples de jeux de données, qui sont stockés dans les répertoires `/example/data` et `/HdiSamples`.</span><span class="sxs-lookup"><span data-stu-id="ef3fa-155">HDInsight provides various example data sets, which are stored in the `/example/data` and `/HdiSamples` directory.</span></span> <span data-ttu-id="ef3fa-156">Ces répertoires sont disponibles dans le stockage par défaut de votre cluster.</span><span class="sxs-lookup"><span data-stu-id="ef3fa-156">These directories are in the default storage for your cluster.</span></span> <span data-ttu-id="ef3fa-157">Dans ce document, nous utilisons le fichier `/example/data/gutenberg/davinci.txt`.</span><span class="sxs-lookup"><span data-stu-id="ef3fa-157">In this document, we use the `/example/data/gutenberg/davinci.txt` file.</span></span> <span data-ttu-id="ef3fa-158">Ce fichier contient les carnets de Léonard De Vinci.</span><span class="sxs-lookup"><span data-stu-id="ef3fa-158">This file contains the notebooks of Leonardo Da Vinci.</span></span>

## <span data-ttu-id="ef3fa-159"><a id="job"></a>Exemple MapReduce</span><span class="sxs-lookup"><span data-stu-id="ef3fa-159"><a id="job"></a>Example MapReduce</span></span>

<span data-ttu-id="ef3fa-160">Un exemple d’application de comptage de mots MapReduce est inclus dans votre cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ef3fa-160">An example MapReduce word count application is included with your HDInsight cluster.</span></span> <span data-ttu-id="ef3fa-161">Cet exemple se trouve dans `/example/jars/hadoop-mapreduce-examples.jar` sur le stockage par défaut pour votre cluster.</span><span class="sxs-lookup"><span data-stu-id="ef3fa-161">This example is located at `/example/jars/hadoop-mapreduce-examples.jar` on the default storage for your cluster.</span></span>

<span data-ttu-id="ef3fa-162">Le code Java suivant est la source de l’application MapReduce contenue dans le fichier `hadoop-mapreduce-examples.jar` :</span><span class="sxs-lookup"><span data-stu-id="ef3fa-162">The following Java code is the source of the MapReduce application contained in the `hadoop-mapreduce-examples.jar` file:</span></span>

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

<span data-ttu-id="ef3fa-163">Pour savoir comment écrire vos propres applications MapReduce, consultez les documents suivants :</span><span class="sxs-lookup"><span data-stu-id="ef3fa-163">For instructions to write your own MapReduce applications, see the following documents:</span></span>

* [<span data-ttu-id="ef3fa-164">Développement d’applications MapReduce en Java pour HDInsight</span><span class="sxs-lookup"><span data-stu-id="ef3fa-164">Develop Java MapReduce applications for HDInsight</span></span>](hdinsight-develop-deploy-java-mapreduce-linux.md)

* [<span data-ttu-id="ef3fa-165">Développement d’applications MapReduce en Python pour HDInsight</span><span class="sxs-lookup"><span data-stu-id="ef3fa-165">Develop Python MapReduce applications for HDInsight</span></span>](hdinsight-hadoop-streaming-python.md)

## <span data-ttu-id="ef3fa-166"><a id="run"></a>Exécution de la tâche MapReduce</span><span class="sxs-lookup"><span data-stu-id="ef3fa-166"><a id="run"></a>Run the MapReduce</span></span>

<span data-ttu-id="ef3fa-167">HDInsight peut exécuter des tâches HiveQL de différentes manières.</span><span class="sxs-lookup"><span data-stu-id="ef3fa-167">HDInsight can run HiveQL jobs by using various methods.</span></span> <span data-ttu-id="ef3fa-168">Utilisez la table suivante pour choisir la méthode qui vous convient, puis cliquez sur le lien pour obtenir une présentation détaillée.</span><span class="sxs-lookup"><span data-stu-id="ef3fa-168">Use the following table to decide which method is right for you, then follow the link for a walkthrough.</span></span>

| <span data-ttu-id="ef3fa-169">**Élément à utiliser...**</span><span class="sxs-lookup"><span data-stu-id="ef3fa-169">**Use this**...</span></span> | <span data-ttu-id="ef3fa-170">**...pour faire cela**</span><span class="sxs-lookup"><span data-stu-id="ef3fa-170">**...to do this**</span></span> | <span data-ttu-id="ef3fa-171">...avec ce **système d’exploitation cluster**</span><span class="sxs-lookup"><span data-stu-id="ef3fa-171">...with this **cluster operating system**</span></span> | <span data-ttu-id="ef3fa-172">...depuis ce **système d’exploitation cluster**</span><span class="sxs-lookup"><span data-stu-id="ef3fa-172">...from this **client operating system**</span></span> |
|:--- |:--- |:--- |:--- |
| [<span data-ttu-id="ef3fa-173">SSH</span><span class="sxs-lookup"><span data-stu-id="ef3fa-173">SSH</span></span>](hdinsight-hadoop-use-mapreduce-ssh.md) |<span data-ttu-id="ef3fa-174">Utilisation de la commande Hadoop via **SSH**</span><span class="sxs-lookup"><span data-stu-id="ef3fa-174">Use the Hadoop command through **SSH**</span></span> |<span data-ttu-id="ef3fa-175">Linux</span><span class="sxs-lookup"><span data-stu-id="ef3fa-175">Linux</span></span> |<span data-ttu-id="ef3fa-176">Linux, Unix, Mac OS X ou Windows</span><span class="sxs-lookup"><span data-stu-id="ef3fa-176">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="ef3fa-177">Curl</span><span class="sxs-lookup"><span data-stu-id="ef3fa-177">Curl</span></span>](hdinsight-hadoop-use-mapreduce-curl.md) |<span data-ttu-id="ef3fa-178">Envoyer la tâche à distance à l'aide de **REST**</span><span class="sxs-lookup"><span data-stu-id="ef3fa-178">Submit the job remotely by using **REST**</span></span> |<span data-ttu-id="ef3fa-179">Linux ou Windows</span><span class="sxs-lookup"><span data-stu-id="ef3fa-179">Linux or Windows</span></span> |<span data-ttu-id="ef3fa-180">Linux, Unix, Mac OS X ou Windows</span><span class="sxs-lookup"><span data-stu-id="ef3fa-180">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="ef3fa-181">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="ef3fa-181">Windows PowerShell</span></span>](hdinsight-hadoop-use-mapreduce-powershell.md) |<span data-ttu-id="ef3fa-182">Envoyer la tâche à distance à l'aide de **Windows PowerShell**</span><span class="sxs-lookup"><span data-stu-id="ef3fa-182">Submit the job remotely by using **Windows PowerShell**</span></span> |<span data-ttu-id="ef3fa-183">Linux ou Windows</span><span class="sxs-lookup"><span data-stu-id="ef3fa-183">Linux or Windows</span></span> |<span data-ttu-id="ef3fa-184">Windows</span><span class="sxs-lookup"><span data-stu-id="ef3fa-184">Windows</span></span> |
| <span data-ttu-id="ef3fa-185">[Bureau à distance](hdinsight-hadoop-use-mapreduce-remote-desktop.md) (HDInsight 3.2 et 3.3)</span><span class="sxs-lookup"><span data-stu-id="ef3fa-185">[Remote Desktop](hdinsight-hadoop-use-mapreduce-remote-desktop.md) (HDInsight 3.2 and 3.3)</span></span> |<span data-ttu-id="ef3fa-186">Utilisation de la commande Hadoop via le **bureau à distance**</span><span class="sxs-lookup"><span data-stu-id="ef3fa-186">Use the Hadoop command through **Remote Desktop**</span></span> |<span data-ttu-id="ef3fa-187">Windows</span><span class="sxs-lookup"><span data-stu-id="ef3fa-187">Windows</span></span> |<span data-ttu-id="ef3fa-188">Windows</span><span class="sxs-lookup"><span data-stu-id="ef3fa-188">Windows</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="ef3fa-189">Linux est le seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure.</span><span class="sxs-lookup"><span data-stu-id="ef3fa-189">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="ef3fa-190">Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="ef3fa-190">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <span data-ttu-id="ef3fa-191"><a id="nextsteps"></a>Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ef3fa-191"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="ef3fa-192">Pour savoir comment utiliser les données dans HDInsight, consultez les documents suivants :</span><span class="sxs-lookup"><span data-stu-id="ef3fa-192">To learn more about working with data in HDInsight, see the following documents:</span></span>

* [<span data-ttu-id="ef3fa-193">Développement de programmes MapReduce en Java pour HDInsight</span><span class="sxs-lookup"><span data-stu-id="ef3fa-193">Develop Java MapReduce programs for HDInsight</span></span>](hdinsight-develop-deploy-java-mapreduce-linux.md)

* [<span data-ttu-id="ef3fa-194">Développement de programmes MapReduce de diffusion en continu Python pour HDInsight</span><span class="sxs-lookup"><span data-stu-id="ef3fa-194">Develop Python streaming MapReduce programs for HDInsight</span></span>](hdinsight-hadoop-streaming-python.md)

* [<span data-ttu-id="ef3fa-195">Développement de tâches MapReduce Scalding avec Apache Hadoop dans HDInsight</span><span class="sxs-lookup"><span data-stu-id="ef3fa-195">Develop Scalding MapReduce jobs with Apache Hadoop on HDInsight</span></span>](hdinsight-hadoop-mapreduce-scalding.md)

* <span data-ttu-id="ef3fa-196">[Utilisation de Hive avec HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="ef3fa-196">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>

* <span data-ttu-id="ef3fa-197">[Utilisation de Pig avec HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="ef3fa-197">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>


[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-develop-mapreduce-jobs]: hdinsight-develop-deploy-java-mapreduce-linux.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md


[powershell-install-configure]: /powershell/azureps-cmdlets-docs

[image-hdi-wordcountdiagram]: ./media/hdinsight-use-mapreduce/HDI.WordCountDiagram.gif
