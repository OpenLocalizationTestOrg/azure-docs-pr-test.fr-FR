---
title: aaaCreate MapReduce Java pour Hadoop - Azure HDInsight | Documents Microsoft
description: "Découvrez comment toouse application de MapReduce Apache Maven toocreate basé sur un Java, puis exécutez-le avec Hadoop sur Azure HDInsight."
services: hdinsight
editor: cgronlun
manager: jhubbard
author: Blackmist
documentationcenter: 
tags: azure-portal
ms.assetid: 9ee6384c-cb61-4087-8273-fb53fa27c1c3
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 08/07/2017
ms.author: larryfr
ms.openlocfilehash: 903a57a482395f7da79002188399a4d6288ff0af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="develop-java-mapreduce-programs-for-hadoop-on-hdinsight"></a><span data-ttu-id="5ade8-103">Développer des programmes MapReduce Java pour Hadoop sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="5ade8-103">Develop Java MapReduce programs for Hadoop on HDInsight</span></span>

<span data-ttu-id="5ade8-104">Découvrez comment toouse application de MapReduce Apache Maven toocreate basé sur un Java, puis exécutez-le avec Hadoop sur Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5ade8-104">Learn how toouse Apache Maven toocreate a Java-based MapReduce application, then run it with Hadoop on Azure HDInsight.</span></span>

> [!NOTE]
> <span data-ttu-id="5ade8-105">Cet exemple a été testé pour la dernière fois sur HDInsight 3.6.</span><span class="sxs-lookup"><span data-stu-id="5ade8-105">This example was most recently tested on HDInsight 3.6.</span></span>

## <span data-ttu-id="5ade8-106"><a name="prerequisites"></a>Configuration requise</span><span class="sxs-lookup"><span data-stu-id="5ade8-106"><a name="prerequisites"></a>Prerequisites</span></span>

* <span data-ttu-id="5ade8-107">[Java JDK](http://www.oracle.com/technetwork/java/javase/downloads/) 8 ou versions ultérieures (ou un équivalent, par exemple, OpenJDK).</span><span class="sxs-lookup"><span data-stu-id="5ade8-107">[Java JDK](http://www.oracle.com/technetwork/java/javase/downloads/) 8 or later (or an equivalent, such as OpenJDK).</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="5ade8-108">HDInsight 3.4 et versions antérieures utilisent Java 7.</span><span class="sxs-lookup"><span data-stu-id="5ade8-108">HDInsight versions 3.4 and earlier use Java 7.</span></span> <span data-ttu-id="5ade8-109">HDInsight 3.5 et les versions ultérieures utilisent Java 8.</span><span class="sxs-lookup"><span data-stu-id="5ade8-109">HDInsight 3.5 and greater uses Java 8.</span></span>

* [<span data-ttu-id="5ade8-110">Apache Maven</span><span class="sxs-lookup"><span data-stu-id="5ade8-110">Apache Maven</span></span>](http://maven.apache.org/)

## <a name="configure-development-environment"></a><span data-ttu-id="5ade8-111">Configurer l’environnement de développement</span><span class="sxs-lookup"><span data-stu-id="5ade8-111">Configure development environment</span></span>

<span data-ttu-id="5ade8-112">Hello variables d’environnement suivantes peuvent être définis lors de l’installation de Java et hello JDK.</span><span class="sxs-lookup"><span data-stu-id="5ade8-112">hello following environment variables may be set when you install Java and hello JDK.</span></span> <span data-ttu-id="5ade8-113">Toutefois, vous devez vérifier qu’ils existent et qu’ils contiennent des valeurs correctes de hello pour votre système.</span><span class="sxs-lookup"><span data-stu-id="5ade8-113">However, you should check that they exist and that they contain hello correct values for your system.</span></span>

* <span data-ttu-id="5ade8-114">`JAVA_HOME`-doit pointer Active toohello où hello Java runtime environment (JRE) est installé.</span><span class="sxs-lookup"><span data-stu-id="5ade8-114">`JAVA_HOME` - should point toohello directory where hello Java runtime environment (JRE) is installed.</span></span> <span data-ttu-id="5ade8-115">Par exemple, sur un système OS X, Unix ou Linux, il doit avoir une valeur similaire trop`/usr/lib/jvm/java-7-oracle`.</span><span class="sxs-lookup"><span data-stu-id="5ade8-115">For example, on an OS X, Unix or Linux system, it should have a value similar too`/usr/lib/jvm/java-7-oracle`.</span></span> <span data-ttu-id="5ade8-116">Dans Windows, il aurait une valeur similaire trop`c:\Program Files (x86)\Java\jre1.7`</span><span class="sxs-lookup"><span data-stu-id="5ade8-116">In Windows, it would have a value similar too`c:\Program Files (x86)\Java\jre1.7`</span></span>

* <span data-ttu-id="5ade8-117">`PATH`-doit contenir hello suivant des chemins d’accès :</span><span class="sxs-lookup"><span data-stu-id="5ade8-117">`PATH` - should contain hello following paths:</span></span>
  
  * <span data-ttu-id="5ade8-118">`JAVA_HOME`(ou les chemins d’accès équivalents hello)</span><span class="sxs-lookup"><span data-stu-id="5ade8-118">`JAVA_HOME` (or hello equivalent path)</span></span>

  * <span data-ttu-id="5ade8-119">`JAVA_HOME\bin`(ou les chemins d’accès équivalents hello)</span><span class="sxs-lookup"><span data-stu-id="5ade8-119">`JAVA_HOME\bin` (or hello equivalent path)</span></span>

  * <span data-ttu-id="5ade8-120">répertoire d’Hello installation Maven</span><span class="sxs-lookup"><span data-stu-id="5ade8-120">hello directory where Maven is installed</span></span>

## <a name="create-a-maven-project"></a><span data-ttu-id="5ade8-121">Création d’un projet Maven</span><span class="sxs-lookup"><span data-stu-id="5ade8-121">Create a Maven project</span></span>

1. <span data-ttu-id="5ade8-122">À partir d’une session Terminal Server, ou de la ligne de commande dans votre environnement de développement, modifiez les répertoires toohello emplacement toostore ce projet.</span><span class="sxs-lookup"><span data-stu-id="5ade8-122">From a terminal session, or command line in your development environment, change directories toohello location you want toostore this project.</span></span>

2. <span data-ttu-id="5ade8-123">Hello d’utilisation `mvn` commande, qui est installé avec Maven, hello toogenerate génération de modèles automatique pour le projet de hello.</span><span class="sxs-lookup"><span data-stu-id="5ade8-123">Use hello `mvn` command, which is installed with Maven, toogenerate hello scaffolding for hello project.</span></span>

   ```bash
   mvn archetype:generate -DgroupId=org.apache.hadoop.examples -DartifactId=wordcountjava -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
   ```

    > [!NOTE]
    > <span data-ttu-id="5ade8-124">Si vous utilisez PowerShell, vous devez le placer hello `-D` paramètres dans des guillemets doubles.</span><span class="sxs-lookup"><span data-stu-id="5ade8-124">If you are using PowerShell, you must enclose hello `-D` parameters in double quotes.</span></span>
    >
    > `mvn archetype:generate "-DgroupId=org.apache.hadoop.examples" "-DartifactId=wordcountjava" "-DarchetypeArtifactId=maven-archetype-quickstart" "-DinteractiveMode=false"`

    <span data-ttu-id="5ade8-125">Cette commande crée un répertoire avec le nom hello spécifié par hello `artifactID` paramètre (**wordcountjava** dans cet exemple.) Ce répertoire contient hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="5ade8-125">This command creates a directory with hello name specified by hello `artifactID` parameter (**wordcountjava** in this example.) This directory contains hello following items:</span></span>

   * <span data-ttu-id="5ade8-126">`pom.xml`-hello [modèle d’objet projet (POM)](http://maven.apache.org/guides/introduction/introduction-to-the-pom.html) qui contient des informations et les détails de configuration utilisés projet hello de toobuild.</span><span class="sxs-lookup"><span data-stu-id="5ade8-126">`pom.xml` - hello [Project Object Model (POM)](http://maven.apache.org/guides/introduction/introduction-to-the-pom.html) that contains information and configuration details used toobuild hello project.</span></span>

   * <span data-ttu-id="5ade8-127">`src`-Active hello qui contient l’application hello.</span><span class="sxs-lookup"><span data-stu-id="5ade8-127">`src` - hello directory that contains hello application.</span></span>

3. <span data-ttu-id="5ade8-128">Supprimer hello `src/test/java/org/apache/hadoop/examples/apptest.java` fichier.</span><span class="sxs-lookup"><span data-stu-id="5ade8-128">Delete hello `src/test/java/org/apache/hadoop/examples/apptest.java` file.</span></span> <span data-ttu-id="5ade8-129">Il n’est pas utilisé dans cet exemple.</span><span class="sxs-lookup"><span data-stu-id="5ade8-129">It is not used in this example.</span></span>

## <a name="add-dependencies"></a><span data-ttu-id="5ade8-130">Ajout de dépendances</span><span class="sxs-lookup"><span data-stu-id="5ade8-130">Add dependencies</span></span>

1. <span data-ttu-id="5ade8-131">Modifier hello `pom.xml` et ajoutez hello après le texte à l’intérieur de hello `<dependencies>` section :</span><span class="sxs-lookup"><span data-stu-id="5ade8-131">Edit hello `pom.xml` file and add hello following text inside hello `<dependencies>` section:</span></span>
   
   ```xml
    <dependency>
        <groupId>org.apache.hadoop</groupId>
        <artifactId>hadoop-mapreduce-examples</artifactId>
        <version>2.7.3</version>
        <scope>provided</scope>
    </dependency>
    <dependency>
        <groupId>org.apache.hadoop</groupId>
        <artifactId>hadoop-mapreduce-client-common</artifactId>
        <version>2.7.3</version>
        <scope>provided</scope>
    </dependency>
    <dependency>
        <groupId>org.apache.hadoop</groupId>
        <artifactId>hadoop-common</artifactId>
        <version>2.7.3</version>
        <scope>provided</scope>
    </dependency>
   ```

    <span data-ttu-id="5ade8-132">Cela définit les bibliothèques nécessaires (figurant dans &lt;artifactId\>) avec une version spécifique (figurant dans &lt;version\>).</span><span class="sxs-lookup"><span data-stu-id="5ade8-132">This defines required libraries (listed within &lt;artifactId\>) with a specific version (listed within &lt;version\>).</span></span> <span data-ttu-id="5ade8-133">Au moment de la compilation, ces dépendances sont téléchargés à partir du référentiel de Maven hello par défaut.</span><span class="sxs-lookup"><span data-stu-id="5ade8-133">At compile time, these dependencies are downloaded from hello default Maven repository.</span></span> <span data-ttu-id="5ade8-134">Vous pouvez utiliser hello [recherche de référentiel Maven](http://search.maven.org/#artifactdetails%7Corg.apache.hadoop%7Chadoop-mapreduce-examples%7C2.5.1%7Cjar) tooview plus.</span><span class="sxs-lookup"><span data-stu-id="5ade8-134">You can use hello [Maven repository search](http://search.maven.org/#artifactdetails%7Corg.apache.hadoop%7Chadoop-mapreduce-examples%7C2.5.1%7Cjar) tooview more.</span></span>
   
    <span data-ttu-id="5ade8-135">Hello `<scope>provided</scope>` indique Maven que ces dépendances ne doivent pas être empaquetés avec l’application hello, telles qu’elles sont fournies par le cluster HDInsight de hello au moment de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="5ade8-135">hello `<scope>provided</scope>` tells Maven that these dependencies should not be packaged with hello application, as they are provided by hello HDInsight cluster at run-time.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="5ade8-136">version Hello utilisée doit correspondre à version hello de Hadoop présent sur votre cluster.</span><span class="sxs-lookup"><span data-stu-id="5ade8-136">hello version used should match hello version of Hadoop present on your cluster.</span></span> <span data-ttu-id="5ade8-137">Pour plus d’informations sur les versions, consultez hello [le contrôle de version HDInsight composant](hdinsight-component-versioning.md) document.</span><span class="sxs-lookup"><span data-stu-id="5ade8-137">For more information on versions, see hello [HDInsight component versioning](hdinsight-component-versioning.md) document.</span></span>

2. <span data-ttu-id="5ade8-138">Ajouter hello suivant toohello `pom.xml` fichier.</span><span class="sxs-lookup"><span data-stu-id="5ade8-138">Add hello following toohello `pom.xml` file.</span></span> <span data-ttu-id="5ade8-139">Ce texte doit être à l’intérieur de hello `<project>...</project>` dans le fichier de hello ; par exemple, entre les balises `</dependencies>` et `</project>`.</span><span class="sxs-lookup"><span data-stu-id="5ade8-139">This text must be inside hello `<project>...</project>` tags in hello file; for example, between `</dependencies>` and `</project>`.</span></span>

   ```xml
    <build>
        <plugins>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-shade-plugin</artifactId>
            <version>2.3</version>
            <configuration>
            <transformers>
                <transformer implementation="org.apache.maven.plugins.shade.resource.ApacheLicenseResourceTransformer">
                </transformer>
            </transformers>
            </configuration>
            <executions>
            <execution>
                <phase>package</phase>
                    <goals>
                    <goal>shade</goal>
                    </goals>
            </execution>
            </executions>
            </plugin>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-compiler-plugin</artifactId>
            <version>3.6.1</version>
            <configuration>
            <source>1.8</source>
            <target>1.8</target>
            </configuration>
        </plugin>
        </plugins>
    </build>
   ```

    <span data-ttu-id="5ade8-140">plug-in première Hello configure hello [plug-in de la nuance Maven](http://maven.apache.org/plugins/maven-shade-plugin/), qui est utilisé toobuild un uberjar (parfois appelé un fatjar), qui contient les dépendances requises par l’application hello.</span><span class="sxs-lookup"><span data-stu-id="5ade8-140">hello first plugin configures hello [Maven Shade Plugin](http://maven.apache.org/plugins/maven-shade-plugin/), which is used toobuild an uberjar (sometimes called a fatjar), which contains dependencies required by hello application.</span></span> <span data-ttu-id="5ade8-141">Elle évite également de duplication de licences dans le package hello jar, ce qui peut entraîner des problèmes sur certains systèmes.</span><span class="sxs-lookup"><span data-stu-id="5ade8-141">It also prevents duplication of licenses within hello jar package, which can cause problems on some systems.</span></span>

    <span data-ttu-id="5ade8-142">plug-in de la deuxième Hello configure une version Java hello cible.</span><span class="sxs-lookup"><span data-stu-id="5ade8-142">hello second plugin configures hello target Java version.</span></span>

    > [!NOTE]
    > <span data-ttu-id="5ade8-143">HDInsight 3.4 et versions antérieures utilisent Java 7.</span><span class="sxs-lookup"><span data-stu-id="5ade8-143">HDInsight 3.4 and earlier use Java 7.</span></span> <span data-ttu-id="5ade8-144">HDInsight 3.5 et les versions ultérieures utilisent Java 8.</span><span class="sxs-lookup"><span data-stu-id="5ade8-144">HDInsight 3.5 and greater uses Java 8.</span></span>

3. <span data-ttu-id="5ade8-145">Enregistrer hello `pom.xml` fichier.</span><span class="sxs-lookup"><span data-stu-id="5ade8-145">Save hello `pom.xml` file.</span></span>

## <a name="create-hello-mapreduce-application"></a><span data-ttu-id="5ade8-146">Créer l’application de MapReduce hello</span><span class="sxs-lookup"><span data-stu-id="5ade8-146">Create hello MapReduce application</span></span>

1. <span data-ttu-id="5ade8-147">Accédez toohello `wordcountjava/src/main/java/org/apache/hadoop/examples` hello active et de renommer `App.java` trop de fichiers`WordCount.java`.</span><span class="sxs-lookup"><span data-stu-id="5ade8-147">Go toohello `wordcountjava/src/main/java/org/apache/hadoop/examples` directory and rename hello `App.java` file too`WordCount.java`.</span></span>

2. <span data-ttu-id="5ade8-148">Ouvrez hello `WordCount.java` de fichiers dans un éditeur de texte et remplacez contenu de hello hello suivant du texte :</span><span class="sxs-lookup"><span data-stu-id="5ade8-148">Open hello `WordCount.java` file in a text editor and replace hello contents with hello following text:</span></span>
   
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
   
    <span data-ttu-id="5ade8-149">Nom du package avis hello est `org.apache.hadoop.examples` et le nom de la classe hello est `WordCount`.</span><span class="sxs-lookup"><span data-stu-id="5ade8-149">Notice hello package name is `org.apache.hadoop.examples` and hello class name is `WordCount`.</span></span> <span data-ttu-id="5ade8-150">Vous utilisez ces noms lorsque vous soumettez une tâche MapReduce de hello.</span><span class="sxs-lookup"><span data-stu-id="5ade8-150">You use these names when you submit hello MapReduce job.</span></span>

3. <span data-ttu-id="5ade8-151">Enregistrez le fichier de hello.</span><span class="sxs-lookup"><span data-stu-id="5ade8-151">Save hello file.</span></span>

## <a name="build-hello-application"></a><span data-ttu-id="5ade8-152">Générez l’application hello</span><span class="sxs-lookup"><span data-stu-id="5ade8-152">Build hello application</span></span>

1. <span data-ttu-id="5ade8-153">Modifier toohello `wordcountjava` active, si vous n’êtes pas déjà.</span><span class="sxs-lookup"><span data-stu-id="5ade8-153">Change toohello `wordcountjava` directory, if you are not already there.</span></span>

2. <span data-ttu-id="5ade8-154">Utilisez hello toobuild fichier JAR contenant application hello du fichier de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="5ade8-154">Use hello following command toobuild a JAR file containing hello application:</span></span>

   ```
   mvn clean package
   ```

    <span data-ttu-id="5ade8-155">Cette commande nettoie les artefacts de build précédente, télécharge les dépendances n’ont pas déjà été installés, et puis génère et package hello d’application.</span><span class="sxs-lookup"><span data-stu-id="5ade8-155">This command cleans any previous build artifacts, downloads any dependencies that have not already been installed, and then builds and package hello application.</span></span>

3. <span data-ttu-id="5ade8-156">Une fois la commande hello se termine, hello `wordcountjava/target` répertoire contient un fichier nommé `wordcountjava-1.0-SNAPSHOT.jar`.</span><span class="sxs-lookup"><span data-stu-id="5ade8-156">Once hello command finishes, hello `wordcountjava/target` directory contains a file named `wordcountjava-1.0-SNAPSHOT.jar`.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="5ade8-157">Hello `wordcountjava-1.0-SNAPSHOT.jar` fichier est un uberjar, qui contient non seulement le travail de WordCount hello, mais nécessite également les dépendances qui hello travail lors de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="5ade8-157">hello `wordcountjava-1.0-SNAPSHOT.jar` file is an uberjar, which contains not only hello WordCount job, but also dependencies that hello job requires at runtime.</span></span>

## <span data-ttu-id="5ade8-158"><a id="upload"></a>Télécharger le fichier jar de hello</span><span class="sxs-lookup"><span data-stu-id="5ade8-158"><a id="upload"></a>Upload hello jar</span></span>

<span data-ttu-id="5ade8-159">Utilisez hello suivant commande tooupload hello jar fichier toohello HDInsight nœud principal :</span><span class="sxs-lookup"><span data-stu-id="5ade8-159">Use hello following command tooupload hello jar file toohello HDInsight headnode:</span></span>

   ```bash
   scp target/wordcountjava-1.0-SNAPSHOT.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:
   ```

    Replace __USERNAME__ with your SSH user name for hello cluster. Replace __CLUSTERNAME__ with hello HDInsight cluster name.

<span data-ttu-id="5ade8-160">Cette commande copie les fichiers hello à partir du nœud principal du toohello hello système local.</span><span class="sxs-lookup"><span data-stu-id="5ade8-160">This command copies hello files from hello local system toohello head node.</span></span> <span data-ttu-id="5ade8-161">Pour en savoir plus, voir [Utilisation de SSH avec Hadoop Linux sur HDInsight depuis Linux, Unix ou OS X](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="5ade8-161">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <span data-ttu-id="5ade8-162"><a name="run"></a>Exécuter la tâche MapReduce de hello sur Hadoop</span><span class="sxs-lookup"><span data-stu-id="5ade8-162"><a name="run"></a>Run hello MapReduce job on Hadoop</span></span>

1. <span data-ttu-id="5ade8-163">Se connecter tooHDInsight à l’aide de SSH.</span><span class="sxs-lookup"><span data-stu-id="5ade8-163">Connect tooHDInsight using SSH.</span></span> <span data-ttu-id="5ade8-164">Pour en savoir plus, voir [Utilisation de SSH avec Hadoop Linux sur HDInsight depuis Linux, Unix ou OS X](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="5ade8-164">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="5ade8-165">À partir de la session SSH hello, utilisez hello après application de commande toorun hello MapReduce :</span><span class="sxs-lookup"><span data-stu-id="5ade8-165">From hello SSH session, use hello following command toorun hello MapReduce application:</span></span>
   
   ```bash
   yarn jar wordcountjava-1.0-SNAPSHOT.jar org.apache.hadoop.examples.WordCount /example/data/gutenberg/davinci.txt /example/data/wordcountout
   ```
   
    <span data-ttu-id="5ade8-166">Cette commande démarre hello WordCount MapReduce application.</span><span class="sxs-lookup"><span data-stu-id="5ade8-166">This command starts hello WordCount MapReduce application.</span></span> <span data-ttu-id="5ade8-167">fichier d’entrée de Hello est `/example/data/gutenberg/davinci.txt`, et le répertoire de sortie hello est `/example/data/wordcountout`.</span><span class="sxs-lookup"><span data-stu-id="5ade8-167">hello input file is `/example/data/gutenberg/davinci.txt`, and hello output directory is `/example/data/wordcountout`.</span></span> <span data-ttu-id="5ade8-168">Hello les fichier d’entrée et sortie sont stockées toohello du stockage par défaut pour le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="5ade8-168">Both hello input file and output are stored toohello default storage for hello cluster.</span></span>

3. <span data-ttu-id="5ade8-169">Une fois que hello est terminée, utilisez hello suivant des résultats des commandes de hello tooview :</span><span class="sxs-lookup"><span data-stu-id="5ade8-169">Once hello job completes, use hello following command tooview hello results:</span></span>
   
   ```bash
   hdfs dfs -cat /example/data/wordcountout/*
   ```

    <span data-ttu-id="5ade8-170">Vous devez recevoir une liste de mots et des nombres, avec toohello similaire de valeurs suivant du texte :</span><span class="sxs-lookup"><span data-stu-id="5ade8-170">You should receive a list of words and counts, with values similar toohello following text:</span></span>
   
        zeal    1
        zelus   1
        zenith  2

## <span data-ttu-id="5ade8-171"><a id="nextsteps"></a>Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="5ade8-171"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="5ade8-172">Dans ce document, vous avez appris comment toodevelop une tâche MapReduce de Java.</span><span class="sxs-lookup"><span data-stu-id="5ade8-172">In this document, you have learned how toodevelop a Java MapReduce job.</span></span> <span data-ttu-id="5ade8-173">Consultez hello suivant des documents pour les autres toowork manières avec HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5ade8-173">See hello following documents for other ways toowork with HDInsight.</span></span>

* <span data-ttu-id="5ade8-174">[Utilisation de Hive avec HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="5ade8-174">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="5ade8-175">[Utilisation de Pig avec HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="5ade8-175">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* [<span data-ttu-id="5ade8-176">Utilisation de MapReduce avec HDInsight</span><span class="sxs-lookup"><span data-stu-id="5ade8-176">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="5ade8-177">Pour plus d’informations, consultez également hello [centre de développement Java](https://azure.microsoft.com/develop/java/).</span><span class="sxs-lookup"><span data-stu-id="5ade8-177">For more information, see also hello [Java Developer Center](https://azure.microsoft.com/develop/java/).</span></span>

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[hdinsight-use-sqoop]: hdinsight-use-sqoop.md
[hdinsight-ODBC]: hdinsight-connect-excel-hive-ODBC-driver.md
[hdinsight-power-query]: hdinsight-connect-excel-power-query.md

[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-admin-powershell]: hdinsight-administer-use-powershell.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md
[hdinsight-power-query]: hdinsight-connect-excel-power-query.md

[powershell-PSCredential]: http://social.technet.microsoft.com/wiki/contents/articles/4546.working-with-passwords-secure-strings-and-credentials-in-windows-powershell.aspx

