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
# <a name="develop-java-mapreduce-programs-for-hadoop-on-hdinsight"></a>Développer des programmes MapReduce Java pour Hadoop sur HDInsight

Découvrez comment toouse application de MapReduce Apache Maven toocreate basé sur un Java, puis exécutez-le avec Hadoop sur Azure HDInsight.

> [!NOTE]
> Cet exemple a été testé pour la dernière fois sur HDInsight 3.6.

## <a name="prerequisites"></a>Configuration requise

* [Java JDK](http://www.oracle.com/technetwork/java/javase/downloads/) 8 ou versions ultérieures (ou un équivalent, par exemple, OpenJDK).
    
    > [!NOTE]
    > HDInsight 3.4 et versions antérieures utilisent Java 7. HDInsight 3.5 et les versions ultérieures utilisent Java 8.

* [Apache Maven](http://maven.apache.org/)

## <a name="configure-development-environment"></a>Configurer l’environnement de développement

Hello variables d’environnement suivantes peuvent être définis lors de l’installation de Java et hello JDK. Toutefois, vous devez vérifier qu’ils existent et qu’ils contiennent des valeurs correctes de hello pour votre système.

* `JAVA_HOME`-doit pointer Active toohello où hello Java runtime environment (JRE) est installé. Par exemple, sur un système OS X, Unix ou Linux, il doit avoir une valeur similaire trop`/usr/lib/jvm/java-7-oracle`. Dans Windows, il aurait une valeur similaire trop`c:\Program Files (x86)\Java\jre1.7`

* `PATH`-doit contenir hello suivant des chemins d’accès :
  
  * `JAVA_HOME`(ou les chemins d’accès équivalents hello)

  * `JAVA_HOME\bin`(ou les chemins d’accès équivalents hello)

  * répertoire d’Hello installation Maven

## <a name="create-a-maven-project"></a>Création d’un projet Maven

1. À partir d’une session Terminal Server, ou de la ligne de commande dans votre environnement de développement, modifiez les répertoires toohello emplacement toostore ce projet.

2. Hello d’utilisation `mvn` commande, qui est installé avec Maven, hello toogenerate génération de modèles automatique pour le projet de hello.

   ```bash
   mvn archetype:generate -DgroupId=org.apache.hadoop.examples -DartifactId=wordcountjava -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
   ```

    > [!NOTE]
    > Si vous utilisez PowerShell, vous devez le placer hello `-D` paramètres dans des guillemets doubles.
    >
    > `mvn archetype:generate "-DgroupId=org.apache.hadoop.examples" "-DartifactId=wordcountjava" "-DarchetypeArtifactId=maven-archetype-quickstart" "-DinteractiveMode=false"`

    Cette commande crée un répertoire avec le nom hello spécifié par hello `artifactID` paramètre (**wordcountjava** dans cet exemple.) Ce répertoire contient hello éléments suivants :

   * `pom.xml`-hello [modèle d’objet projet (POM)](http://maven.apache.org/guides/introduction/introduction-to-the-pom.html) qui contient des informations et les détails de configuration utilisés projet hello de toobuild.

   * `src`-Active hello qui contient l’application hello.

3. Supprimer hello `src/test/java/org/apache/hadoop/examples/apptest.java` fichier. Il n’est pas utilisé dans cet exemple.

## <a name="add-dependencies"></a>Ajout de dépendances

1. Modifier hello `pom.xml` et ajoutez hello après le texte à l’intérieur de hello `<dependencies>` section :
   
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

    Cela définit les bibliothèques nécessaires (figurant dans &lt;artifactId\>) avec une version spécifique (figurant dans &lt;version\>). Au moment de la compilation, ces dépendances sont téléchargés à partir du référentiel de Maven hello par défaut. Vous pouvez utiliser hello [recherche de référentiel Maven](http://search.maven.org/#artifactdetails%7Corg.apache.hadoop%7Chadoop-mapreduce-examples%7C2.5.1%7Cjar) tooview plus.
   
    Hello `<scope>provided</scope>` indique Maven que ces dépendances ne doivent pas être empaquetés avec l’application hello, telles qu’elles sont fournies par le cluster HDInsight de hello au moment de l’exécution.

    > [!IMPORTANT]
    > version Hello utilisée doit correspondre à version hello de Hadoop présent sur votre cluster. Pour plus d’informations sur les versions, consultez hello [le contrôle de version HDInsight composant](hdinsight-component-versioning.md) document.

2. Ajouter hello suivant toohello `pom.xml` fichier. Ce texte doit être à l’intérieur de hello `<project>...</project>` dans le fichier de hello ; par exemple, entre les balises `</dependencies>` et `</project>`.

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

    plug-in première Hello configure hello [plug-in de la nuance Maven](http://maven.apache.org/plugins/maven-shade-plugin/), qui est utilisé toobuild un uberjar (parfois appelé un fatjar), qui contient les dépendances requises par l’application hello. Elle évite également de duplication de licences dans le package hello jar, ce qui peut entraîner des problèmes sur certains systèmes.

    plug-in de la deuxième Hello configure une version Java hello cible.

    > [!NOTE]
    > HDInsight 3.4 et versions antérieures utilisent Java 7. HDInsight 3.5 et les versions ultérieures utilisent Java 8.

3. Enregistrer hello `pom.xml` fichier.

## <a name="create-hello-mapreduce-application"></a>Créer l’application de MapReduce hello

1. Accédez toohello `wordcountjava/src/main/java/org/apache/hadoop/examples` hello active et de renommer `App.java` trop de fichiers`WordCount.java`.

2. Ouvrez hello `WordCount.java` de fichiers dans un éditeur de texte et remplacez contenu de hello hello suivant du texte :
   
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
   
    Nom du package avis hello est `org.apache.hadoop.examples` et le nom de la classe hello est `WordCount`. Vous utilisez ces noms lorsque vous soumettez une tâche MapReduce de hello.

3. Enregistrez le fichier de hello.

## <a name="build-hello-application"></a>Générez l’application hello

1. Modifier toohello `wordcountjava` active, si vous n’êtes pas déjà.

2. Utilisez hello toobuild fichier JAR contenant application hello du fichier de commande suivante :

   ```
   mvn clean package
   ```

    Cette commande nettoie les artefacts de build précédente, télécharge les dépendances n’ont pas déjà été installés, et puis génère et package hello d’application.

3. Une fois la commande hello se termine, hello `wordcountjava/target` répertoire contient un fichier nommé `wordcountjava-1.0-SNAPSHOT.jar`.
   
   > [!NOTE]
   > Hello `wordcountjava-1.0-SNAPSHOT.jar` fichier est un uberjar, qui contient non seulement le travail de WordCount hello, mais nécessite également les dépendances qui hello travail lors de l’exécution.

## <a id="upload"></a>Télécharger le fichier jar de hello

Utilisez hello suivant commande tooupload hello jar fichier toohello HDInsight nœud principal :

   ```bash
   scp target/wordcountjava-1.0-SNAPSHOT.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:
   ```

    Replace __USERNAME__ with your SSH user name for hello cluster. Replace __CLUSTERNAME__ with hello HDInsight cluster name.

Cette commande copie les fichiers hello à partir du nœud principal du toohello hello système local. Pour en savoir plus, voir [Utilisation de SSH avec Hadoop Linux sur HDInsight depuis Linux, Unix ou OS X](hdinsight-hadoop-linux-use-ssh-unix.md).

## <a name="run"></a>Exécuter la tâche MapReduce de hello sur Hadoop

1. Se connecter tooHDInsight à l’aide de SSH. Pour en savoir plus, voir [Utilisation de SSH avec Hadoop Linux sur HDInsight depuis Linux, Unix ou OS X](hdinsight-hadoop-linux-use-ssh-unix.md).

2. À partir de la session SSH hello, utilisez hello après application de commande toorun hello MapReduce :
   
   ```bash
   yarn jar wordcountjava-1.0-SNAPSHOT.jar org.apache.hadoop.examples.WordCount /example/data/gutenberg/davinci.txt /example/data/wordcountout
   ```
   
    Cette commande démarre hello WordCount MapReduce application. fichier d’entrée de Hello est `/example/data/gutenberg/davinci.txt`, et le répertoire de sortie hello est `/example/data/wordcountout`. Hello les fichier d’entrée et sortie sont stockées toohello du stockage par défaut pour le cluster de hello.

3. Une fois que hello est terminée, utilisez hello suivant des résultats des commandes de hello tooview :
   
   ```bash
   hdfs dfs -cat /example/data/wordcountout/*
   ```

    Vous devez recevoir une liste de mots et des nombres, avec toohello similaire de valeurs suivant du texte :
   
        zeal    1
        zelus   1
        zenith  2

## <a id="nextsteps"></a>Étapes suivantes

Dans ce document, vous avez appris comment toodevelop une tâche MapReduce de Java. Consultez hello suivant des documents pour les autres toowork manières avec HDInsight.

* [Utilisation de Hive avec HDInsight][hdinsight-use-hive]
* [Utilisation de Pig avec HDInsight][hdinsight-use-pig]
* [Utilisation de MapReduce avec HDInsight](hdinsight-use-mapreduce.md)

Pour plus d’informations, consultez également hello [centre de développement Java](https://azure.microsoft.com/develop/java/).

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

