---
title: "exemples d’aaaRun hello Hadoop dans HDInsight - Azure | Documents Microsoft"
description: "Découvrez comment utiliser le service Azure HDInsight de hello avec exemples hello fournis. Utilisez des scripts PowerShell qui exécutent des programmes MapReduce sur des clusters de données."
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: bf76d452-abb4-4210-87bd-a2067778c6ed
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: 544856a2cdfe5154cbd9bf1fb05db081af86cd46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="run-hadoop-mapreduce-samples-in-windows-based-hdinsight"></a>Exécution des exemples Hadoop MapReduce dans HDInsight basé sur Windows
[!INCLUDE [samples-selector](../../includes/hdinsight-run-samples-selector.md)]

Un ensemble d’exemples sont fournis toohelp vous commencer à exécuter les tâches MapReduce sur des clusters Hadoop à l’aide d’Azure HDInsight. Ces exemples sont rendus disponibles sur chaque hello HDInsight clusters managés que vous créez. Ces exemples en cours d’exécution vous familiariser avec les travaux de toorun d’applets de commande Azure PowerShell sur des clusters Hadoop.

* [**Nombre de mots**][hdinsight-sample-wordcount] : nombre d'occurrences de mots dans un fichier texte.
* [**Diffusion en continu les statistiques c#**][hdinsight-sample-csharp-streaming]: nombre d’occurrences d’un mot dans un fichier texte à l’aide hello interface de diffusion en continu Hadoop.
* [**Estimateur de pi**][hdinsight-sample-pi-estimator]: utilise une statistique (quasi Monte Carlo) valeur de hello tooestimate la méthode de pi.
* [**Graysort 10 Go**][hdinsight-sample-10gb-graysort] : exécute un programme GraySort généraliste sur un fichier de 10 Go à l’aide de HDInsight. Il existe trois travaux toorun : Teragen toogenerate hello des données, les données de salutation toosort Terasort et tooconfirm Teravalidate que les données de salutation ont été correctement triées.

> [!NOTE]
> Vous trouverez le code source de Hello Bonjour annexe.

Documentation supplémentaire beaucoup existe sur le web hello pour les technologies Hadoop, telles que la programmation de MapReduce de basée sur Java et de diffusion en continu et la documentation sur les applets de commande hello qui sont utilisés dans Windows PowerShell scripting. Pour plus d'informations sur ces ressources, consultez :

* [Développement de programmes MapReduce en Java pour Hadoop dans HDInsight](hdinsight-develop-deploy-java-mapreduce-linux.md)
* [Envoi de tâches Hadoop dans HDInsight](hdinsight-submit-hadoop-jobs-programmatically.md)
* [Introduction tooAzure HDInsight][hdinsight-introduction]

Aujourd'hui, de nombreuses personnes choisissent Hive et Pig par l’intermédiaire de MapReduce.  Pour plus d'informations, consultez les pages suivantes :

* [Utilisation d'Hive dans HDInsight](hdinsight-use-hive.md)
* [Utilisation de Pig dans HDInsight](hdinsight-use-pig.md)

**Conditions préalables**:

* **Un abonnement Azure**. Consultez la page [Obtention d’un essai gratuit d’Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* **Un cluster HDInsight**. Pour obtenir des instructions sur hello dans lequel ces clusters peuvent être créés de différentes manières, consultez [Hadoop de créer des clusters dans HDInsight](hdinsight-hadoop-provision-linux-clusters.md).
* **Un poste de travail sur lequel est installé Azure PowerShell**.

    > [!IMPORTANT]
    > La prise en charge de la gestion des ressources HDInsight par Azure PowerShell à l’aide d’Azure Service Manager est **déconseillée** ; elle sera supprimée le 1er janvier 2017. étapes de Hello dans ce document Utilisez hello nouvelles applets de commande HDInsight qui fonctionnent avec Azure Resource Manager.
    >
    > Suivez les étapes de hello dans [installer et configurer Azure PowerShell](/powershell/azureps-cmdlets-docs) tooinstall hello dernière version d’Azure PowerShell. Si vous avez des scripts qui toobe besoin modifié toouse hello nouvelles applets de commande qui fonctionnent avec Azure Resource Manager, consultez [des outils de migration tooAzure développement basé sur le Gestionnaire de ressources pour les clusters HDInsight](hdinsight-hadoop-development-using-azure-resource-manager.md).

## <a name="hdinsight-sample-wordcount"></a>Nombre de mots - Java
toosubmit un projet MapReduce, vous créez tout d’abord une définition de tâche MapReduce. Dans la définition de tâche hello, vous spécifiez le fichier jar de hello MapReduce programme et l’emplacement de hello du fichier jar hello, qui est **wasb:///example/jars/hadoop-mapreduce-examples.jar**hello nom de classe et hello arguments.  programme de Hello wordcount MapReduce accepte deux arguments : fichier de source de hello est utilisé toocount mots et l’emplacement de hello pour la sortie.

code source de Hello se trouve dans hello [annexe A](#apendix-a---the-word-count-MapReduce-program-in-java).

Pour la procédure hello du développement d’un MapReduce Java programme, voir - [programmes MapReduce de Java développer pour Hadoop dans HDInsight](hdinsight-develop-deploy-java-mapreduce-linux.md)

**toosubmit une tâche MapReduce du nombre word**

1. Ouvrez **Windows PowerShell ISE**. Pour obtenir des instructions, consultez la rubrique [Installation et configuration d'Azure PowerShell][powershell-install-configure].
2. Collez hello PowerShell script suivant :

    ```powershell
    $subscriptionName = "<Azure Subscription Name>"
    $resourceGroupName = "<Resource Group Name>"
    $clusterName = "<HDInsight cluster name>"             # HDInsight cluster name

    Select-AzureRmSubscription -SubscriptionName $subscriptionName

    # Define hello MapReduce job
    $mrJobDefinition = New-AzureRmHDInsightMapReduceJobDefinition `
                                -JarFile "wasb:///example/jars/hadoop-mapreduce-examples.jar" `
                                -ClassName "wordcount" `
                                -Arguments "wasb:///example/data/gutenberg/davinci.txt", "wasb:///example/data/WordCountOutput"

    # Submit hello job and wait for job completion
    $cred = Get-Credential -Message "Enter hello HDInsight cluster HTTP user credential:"
    $mrJob = Start-AzureRmHDInsightJob `
                        -ResourceGroupName $resourceGroupName `
                        -ClusterName $clusterName `
                        -HttpCredential $cred `
                        -JobDefinition $mrJobDefinition

    Wait-AzureRmHDInsightJob `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $clusterName `
        -HttpCredential $cred `
        -JobId $mrJob.JobId

    # Get hello job output
    $cluster = Get-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $clusterName
    $defaultStorageAccount = $cluster.DefaultStorageAccount -replace '.blob.core.windows.net'
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccount)[0].Value
    $defaultStorageContainer = $cluster.DefaultStorageContainer

    Get-AzureRmHDInsightJobOutput `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $clusterName `
        -HttpCredential $cred `
        -DefaultStorageAccountName $defaultStorageAccount `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -DefaultContainer $defaultStorageContainer  `
        -JobId $mrJob.JobId `
        -DisplayOutputType StandardError

    # Download hello job output toohello workstation
    $storageContext = New-AzureStorageContext -StorageAccountName $defaultStorageAccount -StorageAccountKey $defaultStorageAccountKey
    Get-AzureStorageBlobContent -Container $defaultStorageContainer -Blob example/data/WordCountOutput/part-r-00000 -Context $storageContext -Force

    # Display hello output file
    cat ./example/data/WordCountOutput/part-r-00000 | findstr "there"
    ```

    tâche MapReduce Hello génère un fichier nommé *partie-r-00000*, qui contient les mots et hello. script de Hello utilise hello **findstr** commande toolist tous hello mots qui contient *« there »*.
3. Définir hello tout d’abord trois variables et exécuter le script de hello.

## <a name="hdinsight-sample-csharp-streaming"></a>Nombre de mots - Diffusion en continu C#
Hadoop fournit une diffusion en continu tooMapReduce API, ce qui permet de vous mappez toowrite et fonctions dans les langages autres que Java.

> [!NOTE]
> les étapes de Hello dans ce didacticiel s’appliquent en fonction de tooWindows uniquement des clusters HDInsight. Pour obtenir un exemple de diffusion en continu pour les clusters HDInsight Linux, consultez la rubrique [Développement de programmes de diffusion en continu Python pour HDInsight](hdinsight-hadoop-streaming-python.md).

Exemple de hello, le Mappeur hello et réducteur de hello sont des fichiers exécutables lire l’entrée de hello à partir de [stdin] [ stdin-stdout-stderr] (ligne par ligne) et envoyer la sortie de hello trop[stdout] [stdin-stdout-stderr]. programme de Hello compte tous les mots hello dans le texte hello.

Quand un fichier exécutable est spécifié pour **mappeurs**, chaque tâche Mappeur lance hello exécutable en tant que processus distinct lorsque le Mappeur hello est initialisé. Hello Mappeur tâche s’exécute, il convertit son entrée dans les lignes et des flux hello lignes toohello [stdin] [ stdin-stdout-stderr] du processus de hello.

Bonjour pendant ce temps, le Mappeur hello collecte sortie orientée ligne de hello à partir de stdout hello du processus de hello. Il convertit chaque ligne dans une paire clé/valeur, qui est collectée en tant que sortie hello du mappeur de hello. Par défaut, préfixe hello d’une ligne vers le haut toohello premier caractère de tabulation est la clé de hello et reste hello hello hors de ligne (hello caractère de tabulation) est la valeur de hello. S’il n’existe aucun caractère de tabulation dans la ligne de hello, toute ligne est considérée comme clé de hello et hello la valeur est null.

Quand un fichier exécutable est spécifié pour **REDUCTEURS**, chaque tâche réducteur lance hello exécutable en tant que processus séparé réducteur de hello est initialisé. Hello réducteur tâche s’exécute, il convertit son paires clé/valeur d’entrée en lignes et flux de hello lignes toohello [stdin] [ stdin-stdout-stderr] du processus de hello.

Bonjour attendant, réducteur de hello collecte sortie orientée ligne de hello de hello [stdout] [ stdin-stdout-stderr] du processus de hello. Il convertit chaque paire clé/valeur de ligne tooa, qui est collecté en tant que sortie hello du réducteur de hello. Par défaut, préfixe hello d’une ligne vers le haut toohello premier caractère de tabulation est la clé de hello et reste hello hello hors de ligne (hello caractère de tabulation) est la valeur de hello.

**travail de nombre toosubmit c# diffusion word**

* Suivez la procédure hello dans [Word count - Java](#word-count-java)et remplacez-les par définition de la tâche hello hello ligne suivante :

    ```powershell
    $mrJobDefinition = New-AzureRmHDInsightStreamingMapReduceJobDefinition `
                            -Files "/example/apps/cat.exe","/example/apps/wc.exe" `
                            -Mapper "cat.exe" `
                            -Reducer "wc.exe" `
                            -InputPath "/example/data/gutenberg/davinci.txt" `
                            -OutputPath "/example/data/StreamingOutput/wc.txt"
    ```

    fichier de sortie Hello doit être :

        example/data/StreamingOutput/wc.txt/part-00000

## <a name="hdinsight-sample-pi-estimator"></a>Estimateur de la valeur de PI
Estimateur de pi Hello utilise une statistique (quasi Monte Carlo) valeur de hello tooestimate la méthode de pi. Points placés de manière aléatoire à l’intérieur d’une unité appartiennent carrée également au sein d’un cercle inscrit dans ce carré à une zone de toohello égal probabilité du cercle de hello, pi/4. valeur Hello de pi peut être estimée à partir de la valeur hello de 4R, où R est le ratio hello du nombre de hello de points à l’intérieur des hello cercle toohello nombre total de points qui se trouvent dans le carré de hello. exemple Hello plus grande hello de points utilisés, meilleure estimation de hello hello est.

script Hello fourni avec cet exemple soumettre un travail de jar Hadoop et est configuré de toorun avec une valeur 16 maps, chacun d’eux étant des points d’échantillon 10 millions de toocompute requis par les valeurs de paramètre hello. Ces paramètres, les valeurs peuvent être modifiées tooimprove hello estimé valeur pi. Pour référence, hello 10 premières décimales de pi sont 3.1415926535.

**toosubmit un travail estimateur de pi**

* Suivez la procédure hello dans [Word count - Java](#word-count-java)et remplacez-les par définition de la tâche hello hello ligne suivante :

    ```powershell
    $mrJobJobDefinition = New-AzureRmHDInsightMapReduceJobDefinition `
                                -JarFile "wasb:///example/jars/hadoop-mapreduce-examples.jar" `
                                -ClassName "pi" `
                                -Arguments "16", "10000000"
    ```

## <a name="hdinsight-sample-10gb-graysort"></a>GraySort 10 Go
Cet exemple utilise seulement 10 Go de données afin de pouvoir être exécuté relativement rapidement. Il utilise des applications de MapReduce hello développées par Owen O'Malley et Arun Murthy qui a gagné banc d’essai de hello annuel (« daytona ») à usage général téraoctet tri en 2009 avec un taux de 0.578 to/min (100 To 173 minutes). Pour plus d’informations sur les autres tests de tri, consultez hello [Sortbenchmark](http://sortbenchmark.org/) site.

Cet exemple utilise trois ensembles de programmes MapReduce :

1. **TeraGen** est un programme MapReduce que vous pouvez utiliser des lignes de hello toogenerate de toosort de données.
2. **TeraSort** échantillonne les données d’entrée hello et utilise des données de hello MapReduce toosort dans un ordre total. TeraSort est un tri standard de fonctions MapReduce, à l’exception d’un partitionneur personnalisé qui utilise une liste triée des clés de n-1 échantillonnée qui définissent la plage de clés hello pour chaque réduire. En particulier, toutes les clés de ces exemples [i-1] < = clé < exemple [i] sont envoyés tooreduce i. Cela garantit que les sorties hello de réduisent i est tous inférieur à réduire la sortie hello de i + 1.
3. **TeraValidate** est un programme MapReduce qui valide cette sortie hello est trié globalement. Il crée un mappage par fichier dans le répertoire de sortie hello, et chaque mappage garantit que chaque clé est inférieur ou égal toohello précédent. fonction de mappage Hello génère également des enregistrements de hello tout d’abord et réduisent la dernière clés de chaque fichier et hello fonction garantit que hello première clé de fichier i est supérieure à celle hello dernière d’i-1 de fichier. Tous les problèmes sont signalés comme sortie de hello réduire avec des clés de hello qui sont en désordre.

Hello d’entrée et le format de sortie, utilisé par toutes les applications de trois, lit et écrit des fichiers de texte hello dans le format correct de hello. réduire la sortie Hello Hello réplication paramétré too1, au lieu de la valeur par défaut de hello 3, car le concours de banc d’essai hello ne nécessite pas que les données de sortie hello répliquées sur les nœuds toomultiple.

Par exemple hello, chaque tooone correspondante des programmes de MapReduce hello décrites dans l’introduction de hello, trois tâches sont requises :

1. Générer des données pour le tri en exécutant hello hello **TeraGen** tâche MapReduce.
2. Trier les données de hello en exécutant hello **TeraSort** tâche MapReduce.
3. Vérifiez que les données de salutation ont été correctement triées en exécutant hello **TeraValidate** tâche MapReduce.

**travaux de hello toosubmit**

* Suivez la procédure hello dans [Word count - Java](#word-count-java), et utilisez hello suivant des définitions de travaux :

    ```powershell
    $teragen = New-AzureRmHDInsightMapReduceJobDefinition `
                                -JarFile "/example/jars/hadoop-mapreduce-examples.jar" `
                                -ClassName "teragen" `
                                -Arguments "-Dmapred.map.tasks=50", "100000000", "/example/data/10GB-sort-input"

    $terasort = New-AzureRmHDInsightMapReduceJobDefinition `
                                -JarFile "/example/jars/hadoop-mapreduce-examples.jar" `
                                -ClassName "terasort" `
                                -Arguments "-Dmapred.map.tasks=50", "-Dmapred.reduce.tasks=25", "/example/data/10GB-sort-input", "/example/data/10GB-sort-output"

    $teravalidate = New-AzureRmHDInsightMapReduceJobDefinition `
                                -JarFile "/example/jars/hadoop-mapreduce-examples.jar" `
                                -ClassName "teravalidate" `
                                -Arguments "-Dmapred.map.tasks=50", "-Dmapred.reduce.tasks=25", "/example/data/10GB-sort-output", "/example/data/10GB-sort-validate"
    ```

## <a name="next-steps"></a>Étapes suivantes
À partir de cet article et les articles hello dans chacun des exemples de hello, vous avez appris comment exemples de hello toorun inclus avec hello clusters HDInsight à l’aide d’Azure PowerShell. Pour consulter des didacticiels sur l’utilisation de Pig, Hive et MapReduce hdinsight, consultez hello rubriques suivantes :

* [Prise en main Hadoop avec ruche en cours d’utilisation de HDInsight tooanalyze combiné mobile][hdinsight-get-started]
* [Utilisation de Pig avec Hadoop sur HDInsight][hdinsight-use-pig]
* [Utilisation de Hive avec Hadoop sur HDInsight][hdinsight-use-hive]
* [Envoi de tâches Hadoop dans HDInsight][hdinsight-submit-jobs]
* [Documentation du Kit de développement logiciel (SDK) Azure HDInsight][hdinsight-sdk-documentation]

## <a name="appendix-a---hello-word-count-source-code"></a>Annexe A - hello code source de nombre Word

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

## <a name="appendix-b---hello-word-count-streaming-source-code"></a>Annexe B - statistiques hello diffusion en continu de code source
Hello MapReduce utilise application cat.exe de hello comme texte hello toostream mappage interface dans la console de hello et application de wc.exe hello hello réduire le nombre de hello interface toocount de mots qui sont transmis en continu à partir d’un document. Le Mappeur hello et du réducteur lire, ligne par ligne, à partir du flux d’entrée standard (stdin) hello et écrire en toohello des flux de sortie standard (stdout).

```csharp
// hello source code for hello cat.exe (Mapper).

using System;
using System.IO;

namespace cat
{
    class cat
    {
        static void Main(string[] args)
        {
            if (args.Length > 0)
            {
                Console.SetIn(new StreamReader(args[0]));
            }

            string line;
            char[] separators = { ' ', '\n'};
            while ((line = Console.ReadLine()) != null)
            {
                string[] words = line.Split(separators);
                foreach (var word in words)
                {
                    Console.WriteLine("{0}\t1", word);
                }
            }
        }
    }
}
```

Hello code mappeur dans hello cat.cs fichiers utilise un [StreamReader] [ streamreader] tooread les caractères de hello hello entrants flux toohello console, lequel écrit ensuite hello le flux de sortie standard de toohello de flux de données de l’objet avec hello statique [Console.Writeline] [ console-writeline] (méthode).

```csharp
// hello source code for wc.exe (Reducer) is:

using System;
using System.IO;
using System.Linq;
using System.Collections;

namespace wc
{
    class wc
    {
        static void Main(string[] args)
        {
            string line;

            if (args.Length > 0)
            {
                Console.SetIn(new StreamReader(args[0]));
            }

            Hashtable wordCount = new Hashtable();
            while ((line = Console.ReadLine()) != null)
            {
                string[] words = line.Split('\t');

                string key = words[0];

                if (wordCount.ContainsKey(key) == true)
                {
                    int n = Convert.ToInt32(wordCount[key]);
                    wordCount[key] = Convert.ToString(n + 1);
                }
                else
                {
                    wordCount[key] = words[1];
                }
            }
            foreach (var key in wordCount.Keys)
            {
                Console.WriteLine("{0} {1}", key, wordCount[key]);
            }
        }
    }
}
```

Hello code réducteur dans hello wc.cs fichiers utilise un [StreamReader] [ streamreader] tooread caractères de l’objet hello flux d’entrée standard qui ont été générées par le Mappeur cat.exe hello. Lorsqu’il lit les caractères hello avec hello [Console.Writeline] [ console-writeline] méthode instantanément hello en comptant les espaces et les caractères de fin de ligne à fin hello de chaque mot. Il écrit ensuite le flux de sortie standard hello toohello total par hello [Console.Writeline] [ console-writeline] (méthode).

## <a name="appendix-c---hello-pi-estimator-source-code"></a>Annexe C - hello code de Pi estimateur de la source
Estimateur de pi Hello code Java qui contient des fonctions de Mappeur et du réducteur hello n’est disponible pour l’inspection ci-dessous. programme de Mappeur Hello génère un nombre spécifié de points placés de manière aléatoire à l’intérieur d’un carré d’unité et puis dénombre hello de ces points sont à l’intérieur du cercle de hello. programme de réducteur Hello accumule points comptés par mappeurs de hello et évalue ensuite la valeur hello de pi de 4R formule hello, où R est le ratio hello du nombre de hello de points comptés dans hello cercle toohello nombre total de points qui se trouvent dans le carré de hello.

```java
/**
* Licensed toohello Apache Software Foundation (ASF) under one
* or more contributor license agreements. See hello NOTICE file
* distributed with this work for additional information
* regarding copyright ownership. hello ASF licenses this file
* tooyou under hello Apache License, Version 2.0 (the
* "License"); you may not use this file except in compliance
* with hello License. You may obtain a copy of hello License at
*
* http://www.apache.org/licenses/LICENSE-2.0
*
* Unless required by applicable law or agreed tooin writing, software
* distributed under hello License is distributed on an "AS IS" BASIS,
* WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or     implied.
* See hello License for hello specific language governing permissions and
* limitations under hello License.
*/

package org.apache.hadoop.examples;

import java.io.IOException;
import java.math.BigDecimal;
import java.util.Iterator;

import org.apache.hadoop.conf.Configured;
import org.apache.hadoop.fs.FileSystem;
import org.apache.hadoop.fs.Path;
import org.apache.hadoop.io.BooleanWritable;
import org.apache.hadoop.io.LongWritable;
import org.apache.hadoop.io.SequenceFile;
import org.apache.hadoop.io.Writable;
import org.apache.hadoop.io.WritableComparable;
import org.apache.hadoop.io.SequenceFile.CompressionType;
import org.apache.hadoop.mapred.FileInputFormat;
import org.apache.hadoop.mapred.FileOutputFormat;
import org.apache.hadoop.mapred.JobClient;
import org.apache.hadoop.mapred.JobConf;
import org.apache.hadoop.mapred.MapReduceBase;
import org.apache.hadoop.mapred.Mapper;
import org.apache.hadoop.mapred.OutputCollector;
import org.apache.hadoop.mapred.Reducer;
import org.apache.hadoop.mapred.Reporter;
import org.apache.hadoop.mapred.SequenceFileInputFormat;
import org.apache.hadoop.mapred.SequenceFileOutputFormat;
import org.apache.hadoop.util.Tool;
import org.apache.hadoop.util.ToolRunner;

//A Map-reduce program tooestimate hello value of Pi
//using quasi-Monte Carlo method.
//
//Mapper:
//Generate points in a unit square
//and then count points inside/outside of hello inscribed circle of hello square.
//
//Reducer:
//Accumulate points inside/outside results from hello mappers.
//Let numTotal = numInside + numOutside.
//hello fraction numInside/numTotal is a rational approximation of
//hello value (Area of hello circle)/(Area of hello square),
//where hello area of hello inscribed circle is Pi/4
//and hello area of unit square is 1.
//Then, Pi is estimated value toobe 4(numInside/numTotal).
//

public class PiEstimator extends Configured implements Tool {
//tmp directory for input/output
static private final Path TMP_DIR = new Path(
PiEstimator.class.getSimpleName() + "_TMP_3_141592654");

//2-dimensional Halton sequence {H(i)},
//where H(i) is a 2-dimensional point and i >= 1 is hello index.
//Halton sequence is used toogenerate sample points for Pi estimation.
private static class HaltonSequence {
// Bases
static final int[] P = {2, 3};
//Maximum number of digits allowed
static final int[] K = {63, 40};

private long index;
private double[] x;
private double[][] q;
private int[][] d;

//Initialize tooH(startindex),
//so hello sequence begins with H(startindex+1).
HaltonSequence(long startindex) {
index = startindex;
x = new double[K.length];
q = new double[K.length][];
d = new int[K.length][];
for(int i = 0; i < K.length; i++) {
q[i] = new double[K[i]];
d[i] = new int[K[i]];
}

for(int i = 0; i < K.length; i++) {
long k = index;
x[i] = 0;

for(int j = 0; j < K[i]; j++) {
q[i][j] = (j == 0? 1.0: q[i][j-1])/P[i];
d[i][j] = (int)(k % P[i]);
k = (k - d[i][j])/P[i];
x[i] += d[i][j] * q[i][j];
}
}
}

//Compute next point.
//Assume hello current point is H(index).
//Compute H(index+1).
//@return a 2-dimensional point with coordinates in [0,1)^2
double[] nextPoint() {
index++;
for(int i = 0; i < K.length; i++) {
for(int j = 0; j < K[i]; j++) {
d[i][j]++;
x[i] += q[i][j];
if (d[i][j] < P[i]) {
break;
}
d[i][j] = 0;
x[i] -= (j == 0? 1.0: q[i][j-1]);
}
}
return x;
}
}

//Mapper class for Pi estimation.
//Generate points in a unit square and then
//count points inside/outside of hello inscribed circle of hello square.
public static class PiMapper extends MapReduceBase
implements Mapper<LongWritable, LongWritable, BooleanWritable, LongWritable> {

//Map method.
//@param offset samples starting from hello (offset+1)th sample.
//@param size hello number of samples for this map
//@param out output {ture->numInside, false->numOutside}
//@param reporter
public void map(LongWritable offset,
LongWritable size,
OutputCollector<BooleanWritable, LongWritable> out,
Reporter reporter) throws IOException {

final HaltonSequence haltonsequence = new HaltonSequence(offset.get());
long numInside = 0L;
long numOutside = 0L;

for(long i = 0; i < size.get(); ) {
//generate points in a unit square
final double[] point = haltonsequence.nextPoint();

//count points inside/outside of hello inscribed circle of hello square
final double x = point[0] - 0.5;
final double y = point[1] - 0.5;
if (x*x + y*y > 0.25) {
numOutside++;
} else {
numInside++;
}

//report status
i++;
if (i % 1000 == 0) {
reporter.setStatus("Generated " + i + " samples.");
}
}

//output map results
out.collect(new BooleanWritable(true), new LongWritable(numInside));
out.collect(new BooleanWritable(false), new LongWritable(numOutside));
}
}

//Reducer class for Pi estimation.
//Accumulate points inside/outside results from hello mappers.
public static class PiReducer extends MapReduceBase
implements Reducer<BooleanWritable, LongWritable, WritableComparable<?>, Writable> {

private long numInside = 0;
private long numOutside = 0;
private JobConf conf; //configuration for accessing hello file system

//Store job configuration.
@Override
public void configure(JobConf job) {
conf = job;
}

// Accumulate number of points inside/outside results from hello mappers.
// @param isInside Is hello points inside?
// @param values An iterator tooa list of point counts
// @param output dummy, not used here.
// @param reporter

public void reduce(BooleanWritable isInside,
Iterator<LongWritable> values,
OutputCollector<WritableComparable<?>, Writable> output,
Reporter reporter) throws IOException {
if (isInside.get()) {
for(; values.hasNext(); numInside += values.next().get());
} else {
for(; values.hasNext(); numOutside += values.next().get());
}
}

//Reduce task done, write output tooa file.
@Override
public void close() throws IOException {
//write output tooa file
Path outDir = new Path(TMP_DIR, "out");
Path outFile = new Path(outDir, "reduce-out");
FileSystem fileSys = FileSystem.get(conf);
SequenceFile.Writer writer = SequenceFile.createWriter(fileSys, conf,
outFile, LongWritable.class, LongWritable.class,
CompressionType.NONE);
writer.append(new LongWritable(numInside), new LongWritable(numOutside));
writer.close();
}
}

//Run a map/reduce job for estimating Pi.
//@return hello estimated value of Pi.
public static BigDecimal estimate(int numMaps, long numPoints, JobConf jobConf
)
throws IOException {
//setup job conf
jobConf.setJobName(PiEstimator.class.getSimpleName());

jobConf.setInputFormat(SequenceFileInputFormat.class);

jobConf.setOutputKeyClass(BooleanWritable.class);
jobConf.setOutputValueClass(LongWritable.class);
jobConf.setOutputFormat(SequenceFileOutputFormat.class);

jobConf.setMapperClass(PiMapper.class);
jobConf.setNumMapTasks(numMaps);

jobConf.setReducerClass(PiReducer.class);
jobConf.setNumReduceTasks(1);

// turn off speculative execution, because DFS doesn't handle
// multiple writers toohello same file.
jobConf.setSpeculativeExecution(false);

//setup input/output directories
final Path inDir = new Path(TMP_DIR, "in");
final Path outDir = new Path(TMP_DIR, "out");
FileInputFormat.setInputPaths(jobConf, inDir);
FileOutputFormat.setOutputPath(jobConf, outDir);

final FileSystem fs = FileSystem.get(jobConf);
if (fs.exists(TMP_DIR)) {
throw new IOException("Tmp directory " + fs.makeQualified(TMP_DIR)
+ " already exists. Remove it first.");
}
if (!fs.mkdirs(inDir)) {
throw new IOException("Cannot create input directory " + inDir);
}

//generate an input file for each map task
try {
for(int i=0; i < numMaps; ++i) {
final Path file = new Path(inDir, "part"+i);
final LongWritable offset = new LongWritable(i * numPoints);
final LongWritable size = new LongWritable(numPoints);
final SequenceFile.Writer writer = SequenceFile.createWriter(
fs, jobConf, file,
LongWritable.class, LongWritable.class, CompressionType.NONE);
try {
writer.append(offset, size);
} finally {
writer.close();
}
System.out.println("Wrote input for Map #"+i);
}

//start a map/reduce job
System.out.println("Starting Job");
final long startTime = System.currentTimeMillis();
JobClient.runJob(jobConf);
final double duration = (System.currentTimeMillis() - startTime)/1000.0;
System.out.println("Job Finished in " + duration + " seconds");

//read outputs
Path inFile = new Path(outDir, "reduce-out");
LongWritable numInside = new LongWritable();
LongWritable numOutside = new LongWritable();
SequenceFile.Reader reader = new SequenceFile.Reader(fs, inFile, jobConf);
try {
reader.next(numInside, numOutside);
} finally {
reader.close();
}

//compute estimated value
return BigDecimal.valueOf(4).setScale(20)
.multiply(BigDecimal.valueOf(numInside.get()))
.divide(BigDecimal.valueOf(numMaps))
.divide(BigDecimal.valueOf(numPoints));
} finally {
fs.delete(TMP_DIR, true);
}
}

//Parse arguments and then runs a map/reduce job.
//Print output in standard out.
//@return a non-zero if there is an error. Otherwise, return 0.
public int run(String[] args) throws Exception {
if (args.length != 2) {
System.err.println("Usage: "+getClass().getName()+" <nMaps> <nSamples>");
ToolRunner.printGenericCommandUsage(System.err);
return -1;
}

final int nMaps = Integer.parseInt(args[0]);
final long nSamples = Long.parseLong(args[1]);

System.out.println("Number of Maps = " + nMaps);
System.out.println("Samples per Map = " + nSamples);

final JobConf jobConf = new JobConf(getConf(), getClass());
System.out.println("Estimated value of Pi is "
+ estimate(nMaps, nSamples, jobConf));
return 0;
}

//main method for running it as a stand alone command.
public static void main(String[] argv) throws Exception {
System.exit(ToolRunner.run(null, new PiEstimator(), argv));
}
}
```

## <a name="appendix-d---hello-10gb-graysort-source-code"></a>Annexe D - code de source graysort hello 10 Go
code Hello pour hello programme TeraSort MapReduce est présentée pour inspection dans cette section.

```java
/**
    * Licensed toohello Apache Software Foundation (ASF) under one
    * or more contributor license agreements.  See hello NOTICE file
    * distributed with this work for additional information
    * regarding copyright ownership.  hello ASF licenses this file
    * tooyou under hello Apache License, Version 2.0 (the
    * "License"); you may not use this file except in compliance
    * with hello License.  You may obtain a copy of hello License at
    *
    *     http://www.apache.org/licenses/LICENSE-2.0
    *
    * Unless required by applicable law or agreed tooin writing, software
    * distributed under hello License is distributed on an "AS IS" BASIS,
    * WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    * See hello License for hello specific language governing permissions and
    * limitations under hello License.
    */

package org.apache.hadoop.examples.terasort;

import java.io.IOException;
import java.io.PrintStream;
import java.net.URI;
import java.util.ArrayList;
import java.util.List;

import org.apache.commons.logging.Log;
import org.apache.commons.logging.LogFactory;
import org.apache.hadoop.conf.Configured;
import org.apache.hadoop.filecache.DistributedCache;
import org.apache.hadoop.fs.FileSystem;
import org.apache.hadoop.fs.Path;
import org.apache.hadoop.io.NullWritable;
import org.apache.hadoop.io.SequenceFile;
import org.apache.hadoop.io.Text;
import org.apache.hadoop.mapred.FileOutputFormat;
import org.apache.hadoop.mapred.JobClient;
import org.apache.hadoop.mapred.JobConf;
import org.apache.hadoop.mapred.Partitioner;
import org.apache.hadoop.util.Tool;
import org.apache.hadoop.util.ToolRunner;

/**
    * Generates hello sampled split points, launches hello job,
    * and waits for it toofinish.
    * <p>
    * toorun hello program:
    * <b>bin/hadoop jar hadoop-examples-*.jar terasort in-dir out-dir</b>
    */

public class TeraSort extends Configured implements Tool {
    private static final Log LOG = LogFactory.getLog(TeraSort.class);

    /**
    * A partitioner that splits text keys into roughly equal
    * partitions in a global sorted order.
    */

    static class TotalOrderPartitioner implements Partitioner<Text,Text>{
    private TrieNode trie;
    private Text[] splitPoints;

    /**
        * A generic trie node
        */
    static abstract class TrieNode {
        private int level;
        TrieNode(int level) {
        this.level = level;
        }
        abstract int findPartition(Text key);
        abstract void print(PrintStream strm) throws IOException;
        int getLevel() {
        return level;
        }
    }

    /**
        * An inner trie node that contains 256 children based on hello next
        * character.
        */
    static class InnerTrieNode extends TrieNode {
        private TrieNode[] child = new TrieNode[256];

        InnerTrieNode(int level) {
        super(level);
        }
        int findPartition(Text key) {
        int level = getLevel();
        if (key.getLength() <= level) {
            return child[0].findPartition(key);
        }
        return child[key.getBytes()[level]].findPartition(key);
        }
        void setChild(int idx, TrieNode child) {
        this.child[idx] = child;
        }
        void print(PrintStream strm) throws IOException {
        for(int ch=0; ch < 255; ++ch) {
            for(int i = 0; i < 2*getLevel(); ++i) {
            strm.print(' ');
            }
            strm.print(ch);
            strm.println(" ->");
            if (child[ch] != null) {
            child[ch].print(strm);
            }
        }
        }
    }

    /**
        * A leaf trie node that does string compares toofigure out where hello given
        * key belongs between lower..upper.
        */
    static class LeafTrieNode extends TrieNode {
        int lower;
        int upper;
        Text[] splitPoints;
        LeafTrieNode(int level, Text[] splitPoints, int lower, int upper) {
        super(level);
        this.splitPoints = splitPoints;
        this.lower = lower;
        this.upper = upper;
        }
        int findPartition(Text key) {
        for(int i=lower; i<upper; ++i) {
            if (splitPoints[i].compareTo(key) >= 0) {
            return i;
            }
        }
        return upper;
        }
        void print(PrintStream strm) throws IOException {
        for(int i = 0; i < 2*getLevel(); ++i) {
            strm.print(' ');
        }
        strm.print(lower);
        strm.print(", ");
        strm.println(upper);
        }
    }

    /**
        * Read hello cut points from hello given sequence file.
        * @param fs hello file system
        * @param p hello path tooread
        * @param job hello job config
        * @return hello strings toosplit hello partitions on
        * @throws IOException
        */
    private static Text[] readPartitions(FileSystem fs, Path p,
                                            JobConf job) throws IOException {
        SequenceFile.Reader reader = new SequenceFile.Reader(fs, p, job);
        List<Text> parts = new ArrayList<Text>();
        Text key = new Text();
        NullWritable value = NullWritable.get();
        while (reader.next(key, value)) {
        parts.add(key);
        key = new Text();
        }
        reader.close();
        return parts.toArray(new Text[parts.size()]);
    }

    /**
        * Given a sorted set of cut points, build a trie that will find hello correct
        * partition quickly.
        * @param splits hello list of cut points
        * @param lower hello lower bound of partitions 0..numPartitions-1
        * @param upper hello upper bound of partitions 0..numPartitions-1
        * @param prefix hello prefix that we have already checked against
        * @param maxDepth hello maximum depth we will build a trie for
        * @return hello trie node that will divide hello splits correctly
        */
    private static TrieNode buildTrie(Text[] splits, int lower, int upper,
                                        Text prefix, int maxDepth) {
        int depth = prefix.getLength();
        if (depth >= maxDepth || lower == upper) {
        return new LeafTrieNode(depth, splits, lower, upper);
        }
        InnerTrieNode result = new InnerTrieNode(depth);
        Text trial = new Text(prefix);
        // append an extra byte on toohello prefix
        trial.append(new byte[1], 0, 1);
        int currentBound = lower;
        for(int ch = 0; ch < 255; ++ch) {
        trial.getBytes()[depth] = (byte) (ch + 1);
        lower = currentBound;
        while (currentBound < upper) {
            if (splits[currentBound].compareTo(trial) >= 0) {
            break;
            }
            currentBound += 1;
        }
        trial.getBytes()[depth] = (byte) ch;
        result.child[ch] = buildTrie(splits, lower, currentBound, trial,
                                        maxDepth);
        }
        // pick up hello rest
        trial.getBytes()[depth] = 127;
        result.child[255] = buildTrie(splits, currentBound, upper, trial,
                                    maxDepth);
        return result;
    }

    public void configure(JobConf job) {
        try {
        FileSystem fs = FileSystem.getLocal(job);
        Path partFile = new Path(TeraInputFormat.PARTITION_FILENAME);
        splitPoints = readPartitions(fs, partFile, job);
        trie = buildTrie(splitPoints, 0, splitPoints.length, new Text(), 2);
        } catch (IOException ie) {
        throw new IllegalArgumentException("can't read paritions file", ie);
        }
    }

    public TotalOrderPartitioner() {
    }

    public int getPartition(Text key, Text value, int numPartitions) {
        return trie.findPartition(key);
    }

    }

    public int run(String[] args) throws Exception {
    LOG.info("starting");
    JobConf job = (JobConf) getConf();
    Path inputDir = new Path(args[0]);
    inputDir = inputDir.makeQualified(inputDir.getFileSystem(job));
    Path partitionFile = new Path(inputDir, TeraInputFormat.PARTITION_FILENAME);
    URI partitionUri = new URI(partitionFile.toString() +
                                "#" + TeraInputFormat.PARTITION_FILENAME);
    TeraInputFormat.setInputPaths(job, new Path(args[0]));
    FileOutputFormat.setOutputPath(job, new Path(args[1]));
    job.setJobName("TeraSort");
    job.setJarByClass(TeraSort.class);
    job.setOutputKeyClass(Text.class);
    job.setOutputValueClass(Text.class);
    job.setInputFormat(TeraInputFormat.class);
    job.setOutputFormat(TeraOutputFormat.class);
    job.setPartitionerClass(TotalOrderPartitioner.class);
    TeraInputFormat.writePartitionFile(job, partitionFile);
    DistributedCache.addCacheFile(partitionUri, job);
    DistributedCache.createSymlink(job);
    job.setInt("dfs.replication", 1);
    TeraOutputFormat.setFinalSync(job, true);
    JobClient.runJob(job);
    LOG.info("done");
    return 0;
    }

    /**
    * @param args
    */

    public static void main(String[] args) throws Exception {
    int res = ToolRunner.run(new JobConf(), new TeraSort(), args);
    System.exit(res);
    }
}
```

[hdinsight-sdk-documentation]: https://msdn.microsoft.com/library/azure/dn479185.aspx

[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-introduction]: hdinsight-hadoop-introduction.md

[powershell-install-configure]: /powershell/azureps-cmdlets-docs

[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md

[hdinsight-samples]: hdinsight-run-samples.md
[hdinsight-sample-10gb-graysort]: #hdinsight-sample-10gb-graysort
[hdinsight-sample-csharp-streaming]: #hdinsight-sample-csharp-streaming
[hdinsight-sample-pi-estimator]: #hdinsight-sample-pi-estimator
[hdinsight-sample-wordcount]: #hdinsight-sample-wordcount

[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md

[streamreader]: http://msdn.microsoft.com/library/system.io.streamreader.aspx
[console-writeline]: http://msdn.microsoft.com/library/system.console.writeline
[stdin-stdout-stderr]: https://msdn.microsoft.com/library/3x292kth.aspx
