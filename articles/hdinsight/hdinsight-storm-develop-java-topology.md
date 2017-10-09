---
title: aaaApache renverser exemple de topologie Java - Azure HDInsight | Documents Microsoft
description: "Découvrez comment les topologies d’Apache Storm toocreate dans Java en créant un mot exemple compter topologie."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
keywords: apache storm,exemple apache storm,storm java,exemple de topologie storm
ms.assetid: a8838f29-9c08-4fd9-99ef-26655d1bf6d7
ms.service: hdinsight
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/07/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive,hdiseo17may2017
ms.openlocfilehash: 54fa9dc3c93ddad83ac861f3101f50f80117d804
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-apache-storm-topology-in-java"></a>Créer une topologie Apache Storm en Java

Découvrez comment toocreate une topologie basée sur Java d’Apache Storm. Vous créez une topologie Storm qui implémente une application de comptage de mots. Vous utilisez Maven toobuild et package hello le projet. Ensuite, vous allez apprendre comment l’à l’aide de topologie toodefine hello hello framework de Flux.

> [!NOTE]
> infrastructure de Flux Hello est disponible dans Storm 0.10.0 ou version ultérieure. Storm 0.10.0 est disponible avec HDInsight 3.3 et 3.4.

Après avoir effectué les étapes de hello dans ce document, vous pouvez déployer hello topologie tooApache Storm sur HDInsight.

> [!NOTE]
> Une version complète d’exemples de topologie Storm hello créé dans ce document est disponible à l’adresse [https://github.com/Azure-Samples/hdinsight-java-storm-wordcount](https://github.com/Azure-Samples/hdinsight-java-storm-wordcount).

## <a name="prerequisites"></a>Composants requis

* [Kit de développeur Java (JDK) version 7](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html)

* [Maven (https://maven.apache.org/download.cgi)](https://maven.apache.org/download.cgi): Maven est un système de génération de projet pour les projets Java.

* Un éditeur de texte ou IDE.

## <a name="configure-environment-variables"></a>Configuration des variables d’environnement

Hello variables d’environnement suivantes peuvent être définis lors de l’installation de Java et hello JDK. Toutefois, vous devez vérifier qu’ils existent et qu’ils contiennent des valeurs correctes de hello pour votre système.

* **JAVA_HOME** -doit pointer Active toohello où hello Java runtime environment (JRE) est installé. Par exemple, dans une distribution Unix ou Linux, il doit avoir une valeur similaire trop`/usr/lib/jvm/java-7-oracle`. Dans Windows, il aurait une valeur similaire trop`c:\Program Files (x86)\Java\jre1.7`

* **Chemin d’accès** -doit contenir hello suivant des chemins d’accès :

  * **JAVA_HOME** (ou les chemins d’accès équivalents hello)

  * **JAVA_HOME\bin** (ou les chemins d’accès équivalents hello)

  * répertoire d’Hello installation Maven

## <a name="create-a-maven-project"></a>Création d’un projet Maven

À partir de la ligne de commande hello, utilisez hello commande suivante toocreate un projet Maven nommé **WordCount**:

```bash
mvn archetype:generate -DarchetypeArtifactId=maven-archetype-quickstart -DgroupId=com.microsoft.example -DartifactId=WordCount -DinteractiveMode=false
```

> [!NOTE]
> Si vous utilisez PowerShell, vous devez placer les paramètres `-D` entre guillemets doubles.
>
> `mvn archetype:generate "-DarchetypeArtifactId=maven-archetype-quickstart" "-DgroupId=com.microsoft.example" "-DartifactId=WordCount" "-DinteractiveMode=false"`

Cette commande crée un répertoire nommé `WordCount` à l’emplacement actuel de hello, qui contient un projet de base Maven. Hello `WordCount` répertoire contient hello éléments suivants :

* `pom.xml`: Contient les paramètres de projet de Maven hello.
* `src\main\java\com\microsoft\example` : contient votre code d’application.
* `src\test\java\com\microsoft\example` : contient des tests pour votre application. 

### <a name="remove-hello-generated-example-code"></a>Supprimer l’exemple de code hello généré

Supprimer les fichiers d’application hello et de test de hello généré :

* **src\test\java\com\microsoft\example\AppTest.java**
* **src\main\java\com\microsoft\example\App.java**

## <a name="add-maven-repositories"></a>Ajouter des référentiels Maven

HDInsight est basée sur hello Hortonworks Data Platform (HDP), nous vous recommandons d’à l’aide des dépendances de toodownload référentiel hello Hortonworks pour vos projets d’Apache Storm. Bonjour __pom.xml__ , ajoutez hello XML suivant après hello `<url>http://maven.apache.org</url>` ligne :

```xml
<repositories>
    <repository>
        <releases>
            <enabled>true</enabled>
            <updatePolicy>always</updatePolicy>
            <checksumPolicy>warn</checksumPolicy>
        </releases>
        <snapshots>
            <enabled>false</enabled>
            <updatePolicy>never</updatePolicy>
            <checksumPolicy>fail</checksumPolicy>
        </snapshots>
        <id>HDPReleases</id>
        <name>HDP Releases</name>
        <url>http://repo.hortonworks.com/content/repositories/releases/</url>
        <layout>default</layout>
    </repository>
    <repository>
        <releases>
            <enabled>true</enabled>
            <updatePolicy>always</updatePolicy>
            <checksumPolicy>warn</checksumPolicy>
        </releases>
        <snapshots>
            <enabled>false</enabled>
            <updatePolicy>never</updatePolicy>
            <checksumPolicy>fail</checksumPolicy>
        </snapshots>
        <id>HDPJetty</id>
        <name>Hadoop Jetty</name>
        <url>http://repo.hortonworks.com/content/repositories/jetty-hadoop/</url>
        <layout>default</layout>
    </repository>
</repositories>
```

## <a name="add-properties"></a>Ajout de propriétés

Maven vous permet de valeurs au niveau du projet de toodefine appelées propriétés. Bonjour __pom.xml__, ajouter hello après le texte après hello `</repositories>` ligne :

```xml
<properties>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    <!--
    This is a version of Storm from hello Hortonworks repository that is compatible with HDInsight.
    -->
    <storm.version>1.0.1.2.5.3.0-37</storm.version>
</properties>
```

Vous pouvez maintenant utiliser cette valeur dans d’autres sections de hello `pom.xml`. Par exemple, lors de la spécification de version hello des composants de Storm, vous pouvez utiliser `${storm.version}` au lieu de manière irréversible une valeur.

## <a name="add-dependencies"></a>Ajout de dépendances

Ajoutez une dépendance pour les composants Storm. Ouvrez hello `pom.xml` et ajoutez hello suivant code Bonjour `<dependencies>` section :

```xml
<dependency>
    <groupId>org.apache.storm</groupId>
    <artifactId>storm-core</artifactId>
    <version>${storm.version}</version>
    <!-- keep storm out of hello jar-with-dependencies -->
    <scope>provided</scope>
</dependency>
```

Au moment de la compilation, Maven utilise cette toolook informations `storm-core` dans le référentiel de Maven hello. Il recherche tout d’abord dans le référentiel hello sur votre ordinateur local. Si les fichiers hello ne sont pas, Maven les télécharge à partir du référentiel de Maven publique hello et les stocke dans le référentiel local de hello.

> [!NOTE]
> Hello d’avis `<scope>provided</scope>` ligne dans cette section. Ce paramètre indique à Maven tooexclude **storm cœur** à partir de tous les fichiers JAR créés, car elle est fournie par le système de hello.

## <a name="build-configuration"></a>Configuration de build

Plug-ins de Maven autoriser étapes de build toocustomize hello du projet de hello. Par exemple, comment le projet de hello est compilé ou comment toopackage dans un fichier JAR. Ouvrez hello `pom.xml` et ajoutez hello suivant code directement au-dessus hello `</project>` ligne.

```xml
<build>
    <plugins>
    </plugins>
    <resources>
    </resources>
</build>
```

Cette section est tooadd utilisé plug-ins, les ressources et les autres options de configuration de build. Pour des informations complètes de hello **pom.xml** de fichiers, consultez [http://maven.apache.org/pom.html](http://maven.apache.org/pom.html).

### <a name="add-plug-ins"></a>Ajout de plug-ins

Pour les topologies d’Apache Storm implémentées en Java, hello [plug-in de Maven Exec](http://www.mojohaus.org/exec-maven-plugin/) est utile car elle vous permet de tooeasily exécuter topologie de hello localement dans votre environnement de développement. Ajouter hello suivant toohello `<plugins>` section Hello `pom.xml` fichier plug-in de tooinclude hello Exec Maven :

```xml
<plugin>
    <groupId>org.codehaus.mojo</groupId>
    <artifactId>exec-maven-plugin</artifactId>
    <version>1.4.0</version>
    <executions>
    <execution>
    <goals>
        <goal>exec</goal>
    </goals>
    </execution>
    </executions>
    <configuration>
    <executable>java</executable>
    <includeProjectDependencies>true</includeProjectDependencies>
    <includePluginDependencies>false</includePluginDependencies>
    <classpathScope>compile</classpathScope>
    <mainClass>${storm.topology}</mainClass>
    <cleanupDaemonThreads>false</cleanupDaemonThreads> 
    </configuration>
</plugin>
```

Un autre utile plug-in est hello [le plug-in du compilateur Apache Maven](http://maven.apache.org/plugins/maven-compiler-plugin/), qui est utilisé toochange options de compilation. modifications de Hello hello version Java Maven utilise pour la source de hello et la cible de votre application.

* Pour HDInsight __3.4 ou une version antérieure__, définissez hello source et cible Java version too__1.7__.

* Pour HDInsight __3.5__, définissez hello source et cible Java version too__1.8__.

Ajouter hello suit texte Bonjour `<plugins>` section Hello `pom.xml` fichier plug-in de tooinclude hello Apache Maven compilateur. Cet exemple spécifie 1.8, afin de la version de HDInsight cible hello est 3.5.

```xml
<plugin>
    <groupId>org.apache.maven.plugins</groupId>
    <artifactId>maven-compiler-plugin</artifactId>
    <version>3.3</version>
    <configuration>
    <source>1.8</source>
    <target>1.8</target>
    </configuration>
</plugin>
```

### <a name="configure-resources"></a>Configuration des ressources

section de ressources Hello vous permet de ressources de non code tooinclude tels que les fichiers de configuration requis par les composants dans une topologie de hello. Pour cet exemple, ajoutez hello suit texte Bonjour `<resources>` section Hello ' pom.xml fichier.

```xml
<resource>
    <directory>${basedir}/resources</directory>
    <filtering>false</filtering>
    <includes>
        <include>log4j2.xml</include>
    </includes>
</resource>
```

Cet exemple ajoute le répertoire des ressources hello dans racine hello du projet de hello (`${basedir}`) en tant qu’emplacement qui contient des ressources et inclut le fichier hello nommé `log4j2.xml`. Ce fichier est utilisé tooconfigure quelles informations sont enregistrées par la topologie de hello.

## <a name="create-hello-topology"></a>Créer la topologie de hello

Une topologie Apache Storm basée sur Java comprend trois composants que vous devez créer (ou référencer) en tant que dépendance.

* **Becs verseurs amovibles**: lit les sources de données externes et émet des flux de données dans la topologie de hello.

* **Les bolts**: effectuent le traitement des flux de données émis par les spouts ou les autres bolts et émettent un ou plusieurs flux.

* **Topologie**: définit le mode hello becs verseurs amovibles et boulons sont organisées et fournit un point d’entrée hello pour la topologie de hello.

### <a name="create-hello-spout"></a>Créer les bec hello

configuration tooreduce pour des sources de données externes, hello suivant bec émet simplement des phrases aléatoires. Il s’agit d’une version modifiée d’un bec qui est fourni avec hello [exemples de Storm-Starter](https://github.com/apache/storm/blob/0.10.x-branch/examples/storm-starter/src/jvm/storm/starter).

> [!NOTE]
> Pour obtenir un exemple d’un bec qui lit à partir d’une source de données externes, consultez une des hello exemple suivant :
>
> * [TwitterSampleSpout](https://github.com/apache/storm/blob/0.10.x-branch/examples/storm-starter/src/jvm/storm/starter/spout/TwitterSampleSpout.java): un exemple de spout qui lit à partir de Twitter
> * [Storm-Kafka](https://github.com/apache/storm/tree/0.10.x-branch/external/storm-kafka): un spout qui lit à partir de Kafka

Pour un bec hello, créez un fichier nommé `RandomSentenceSpout.java` Bonjour `src\main\java\com\microsoft\example` hello active et l’utilisation suivante du code Java en tant que contenu de hello :

```java
package com.microsoft.example;

import org.apache.storm.spout.SpoutOutputCollector;
import org.apache.storm.task.TopologyContext;
import org.apache.storm.topology.OutputFieldsDeclarer;
import org.apache.storm.topology.base.BaseRichSpout;
import org.apache.storm.tuple.Fields;
import org.apache.storm.tuple.Values;
import org.apache.storm.utils.Utils;

import java.util.Map;
import java.util.Random;

//This spout randomly emits sentences
public class RandomSentenceSpout extends BaseRichSpout {
  //Collector used tooemit output
  SpoutOutputCollector _collector;
  //Used toogenerate a random number
  Random _rand;

  //Open is called when an instance of hello class is created
  @Override
  public void open(Map conf, TopologyContext context, SpoutOutputCollector collector) {
  //Set hello instance collector toohello one passed in
    _collector = collector;
    //For randomness
    _rand = new Random();
  }

  //Emit data toohello stream
  @Override
  public void nextTuple() {
  //Sleep for a bit
    Utils.sleep(100);
    //hello sentences that are randomly emitted
    String[] sentences = new String[]{ "hello cow jumped over hello moon", "an apple a day keeps hello doctor away",
        "four score and seven years ago", "snow white and hello seven dwarfs", "i am at two with nature" };
    //Randomly pick a sentence
    String sentence = sentences[_rand.nextInt(sentences.length)];
    //Emit hello sentence
    _collector.emit(new Values(sentence));
  }

  //Ack is not implemented since this is a basic example
  @Override
  public void ack(Object id) {
  }

  //Fail is not implemented since this is a basic example
  @Override
  public void fail(Object id) {
  }

  //Declare hello output fields. In this case, an sentence
  @Override
  public void declareOutputFields(OutputFieldsDeclarer declarer) {
    declarer.declare(new Fields("sentence"));
  }
}
```

> [!NOTE]
> Bien que cette topologie n'utilise qu’un seul bec, d’autres peuvent en avoir plusieurs ce flux de données à partir de différentes sources dans une topologie de hello.

### <a name="create-hello-bolts"></a>Créer hello boulons

Boulons gèrent le traitement des données hello. Cette topologie utilise deux bolts :

* **SplitSentence**: fractionne les phrases hello émis par **RandomSentenceSpout** en mots individuels.

* **WordCount**: compte le nombre d’occurrences de chaque mot.

> [!NOTE]
> Boulons faire quoi que ce soit, par exemple, le calcul, persistance ou communiquer avec les composants tooexternal.

Créez deux nouveaux fichiers, `SplitSentence.java` et `WordCount.java` Bonjour `src\main\java\com\microsoft\example` active. Utilisez hello après le texte en tant que contenu hello pour les fichiers de hello :

#### <a name="splitsentence"></a>SplitSentence

```java
package com.microsoft.example;

import java.text.BreakIterator;

import org.apache.storm.topology.BasicOutputCollector;
import org.apache.storm.topology.OutputFieldsDeclarer;
import org.apache.storm.topology.base.BaseBasicBolt;
import org.apache.storm.tuple.Fields;
import org.apache.storm.tuple.Tuple;
import org.apache.storm.tuple.Values;

//There are a variety of bolt types. In this case, use BaseBasicBolt
public class SplitSentence extends BaseBasicBolt {

  //Execute is called tooprocess tuples
  @Override
  public void execute(Tuple tuple, BasicOutputCollector collector) {
    //Get hello sentence content from hello tuple
    String sentence = tuple.getString(0);
    //An iterator tooget each word
    BreakIterator boundary=BreakIterator.getWordInstance();
    //Give hello iterator hello sentence
    boundary.setText(sentence);
    //Find hello beginning first word
    int start=boundary.first();
    //Iterate over each word and emit it toohello output stream
    for (int end=boundary.next(); end != BreakIterator.DONE; start=end, end=boundary.next()) {
      //get hello word
      String word=sentence.substring(start,end);
      //If a word is whitespace characters, replace it with empty
      word=word.replaceAll("\\s+","");
      //if it's an actual word, emit it
      if (!word.equals("")) {
        collector.emit(new Values(word));
      }
    }
  }

  //Declare that emitted tuples contain a word field
  @Override
  public void declareOutputFields(OutputFieldsDeclarer declarer) {
    declarer.declare(new Fields("word"));
  }
}
```

#### <a name="wordcount"></a>WordCount

```java
package com.microsoft.example;

import java.util.HashMap;
import java.util.Map;
import java.util.Iterator;

import org.apache.storm.Constants;
import org.apache.storm.topology.BasicOutputCollector;
import org.apache.storm.topology.OutputFieldsDeclarer;
import org.apache.storm.topology.base.BaseBasicBolt;
import org.apache.storm.tuple.Fields;
import org.apache.storm.tuple.Tuple;
import org.apache.storm.tuple.Values;
import org.apache.storm.Config;

// For logging
import org.apache.logging.log4j.Logger;
import org.apache.logging.log4j.LogManager;

//There are a variety of bolt types. In this case, use BaseBasicBolt
public class WordCount extends BaseBasicBolt {
  //Create logger for this class
  private static final Logger logger = LogManager.getLogger(WordCount.class);
  //For holding words and counts
  Map<String, Integer> counts = new HashMap<String, Integer>();
  //How often tooemit a count of words
  private Integer emitFrequency;

  // Default constructor
  public WordCount() {
      emitFrequency=5; // Default too60 seconds
  }

  // Constructor that sets emit frequency
  public WordCount(Integer frequency) {
      emitFrequency=frequency;
  }

  //Configure frequency of tick tuples for this bolt
  //This delivers a 'tick' tuple on a specific interval,
  //which is used tootrigger certain actions
  @Override
  public Map<String, Object> getComponentConfiguration() {
      Config conf = new Config();
      conf.put(Config.TOPOLOGY_TICK_TUPLE_FREQ_SECS, emitFrequency);
      return conf;
  }

  //execute is called tooprocess tuples
  @Override
  public void execute(Tuple tuple, BasicOutputCollector collector) {
    //If it's a tick tuple, emit all words and counts
    if(tuple.getSourceComponent().equals(Constants.SYSTEM_COMPONENT_ID)
            && tuple.getSourceStreamId().equals(Constants.SYSTEM_TICK_STREAM_ID)) {
      for(String word : counts.keySet()) {
        Integer count = counts.get(word);
        collector.emit(new Values(word, count));
        logger.info("Emitting a count of " + count + " for word " + word);
      }
    } else {
      //Get hello word contents from hello tuple
      String word = tuple.getString(0);
      //Have we counted any already?
      Integer count = counts.get(word);
      if (count == null)
        count = 0;
      //Increment hello count and store it
      count++;
      counts.put(word, count);
    }
  }

  //Declare that this emits a tuple containing two fields; word and count
  @Override
  public void declareOutputFields(OutputFieldsDeclarer declarer) {
    declarer.declare(new Fields("word", "count"));
  }
}
```

### <a name="define-hello-topology"></a>Définir la topologie de hello

topologie de Hello lie becs verseurs de hello et boulons ensemble dans un graphique, qui définit comment les données circulent entre les composants de hello. Il fournit également des indications de parallélisme Storm utilise lors de la création d’instances des composants hello au sein du cluster de hello.

Hello image suivante est un schéma de base de graphique de hello des composants pour cette topologie.

![hello d’affichage de diagramme becs verseurs amovibles et boulons arrangement](./media/hdinsight-storm-develop-java-topology/wordcount-topology.png)

tooimplement hello topologie, créez un fichier nommé `WordCountTopology.java` Bonjour `src\main\java\com\microsoft\example` active. Utilisez hello suivant le code Java en tant que contenu hello du fichier de hello :

```java
package com.microsoft.example;

import org.apache.storm.Config;
import org.apache.storm.LocalCluster;
import org.apache.storm.StormSubmitter;
import org.apache.storm.topology.TopologyBuilder;
import org.apache.storm.tuple.Fields;

import com.microsoft.example.RandomSentenceSpout;

public class WordCountTopology {

  //Entry point for hello topology
  public static void main(String[] args) throws Exception {
  //Used toobuild hello topology
    TopologyBuilder builder = new TopologyBuilder();
    //Add hello spout, with a name of 'spout'
    //and parallelism hint of 5 executors
    builder.setSpout("spout", new RandomSentenceSpout(), 5);
    //Add hello SplitSentence bolt, with a name of 'split'
    //and parallelism hint of 8 executors
    //shufflegrouping subscribes toohello spout, and equally distributes
    //tuples (sentences) across instances of hello SplitSentence bolt
    builder.setBolt("split", new SplitSentence(), 8).shuffleGrouping("spout");
    //Add hello counter, with a name of 'count'
    //and parallelism hint of 12 executors
    //fieldsgrouping subscribes toohello split bolt, and
    //ensures that hello same word is sent toohello same instance (group by field 'word')
    builder.setBolt("count", new WordCount(), 12).fieldsGrouping("split", new Fields("word"));

    //new configuration
    Config conf = new Config();
    //Set toofalse toodisable debug information when
    // running in production on a cluster
    conf.setDebug(false);

    //If there are arguments, we are running on a cluster
    if (args != null && args.length > 0) {
      //parallelism hint tooset hello number of workers
      conf.setNumWorkers(3);
      //submit hello topology
      StormSubmitter.submitTopology(args[0], conf, builder.createTopology());
    }
    //Otherwise, we are running locally
    else {
      //Cap hello maximum number of executors that can be spawned
      //for a component too3
      conf.setMaxTaskParallelism(3);
      //LocalCluster is used toorun locally
      LocalCluster cluster = new LocalCluster();
      //submit hello topology
      cluster.submitTopology("word-count", conf, builder.createTopology());
      //sleep
      Thread.sleep(10000);
      //shut down hello cluster
      cluster.shutdown();
    }
  }
}
```

### <a name="configure-logging"></a>Configuration de la journalisation

Storm utilise Apache Log4j toolog informations. Si vous ne configurez pas la journalisation, la topologie de hello émet des informations de diagnostic. toocontrol éléments enregistrés, créez un fichier nommé `log4j2.xml` Bonjour `resources` active. Utilisez hello XML suivant comme contenu hello du fichier de hello.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Configuration>
<Appenders>
    <Console name="STDOUT" target="SYSTEM_OUT">
        <PatternLayout pattern="%d{HH:mm:ss} [%t] %-5level %logger{36} - %msg%n"/>
    </Console>
</Appenders>
<Loggers>
    <Logger name="com.microsoft.example" level="trace" additivity="false">
        <AppenderRef ref="STDOUT"/>
    </Logger>
    <Root level="error">
        <Appender-Ref ref="STDOUT"/>
    </Root>
</Loggers>
</Configuration>
```

Ce code XML configure un nouvel enregistreur d’événements pour hello `com.microsoft.example` (classe), qui inclut les composants hello dans cet exemple de topologie. niveau de Hello a la valeur tootrace pour cet enregistreur d’événements, qui capture toutes les informations de journalisation émises par les composants dans cette topologie.

Hello `<Root level="error">` section configure le niveau de journalisation racine du hello (pas dans tous les éléments `com.microsoft.example`) les informations sur l’erreur du journal tooonly.

Pour plus d’informations sur la configuration de la journalisation pour Log4j, consultez [http://logging.apache.org/log4j/2.x/manual/configuration.html](http://logging.apache.org/log4j/2.x/manual/configuration.html).

> [!NOTE]
> Storm version 0.10.0 et ultérieure utilisent Log4j 2.x. Les versions antérieures de Storm utilisaient Log4j 1.x, qui utilisait un autre format pour la configuration du journal. Pour plus d’informations sur la configuration antérieure hello, consultez [http://wiki.apache.org/logging-log4j/Log4jXmlFormat](http://wiki.apache.org/logging-log4j/Log4jXmlFormat).

## <a name="test-hello-topology-locally"></a>Topologie de hello test localement

Après avoir enregistré les fichiers hello, utilisez hello suivant topologie commande tootest hello localement.

```bash
mvn compile exec:java -Dstorm.topology=com.microsoft.example.WordCountTopology
```

En cours d’exécution, la topologie de hello affiche des informations de démarrage. Hello texte suivant est un exemple de sortie de nombre hello word :

    17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 56 for word snow
    17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 56 for word white
    17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 112 for word seven
    17:33:27 [Thread-16-count] INFO  com.microsoft.example.WordCount - Emitting a count of 195 for word the
    17:33:27 [Thread-30-count] INFO  com.microsoft.example.WordCount - Emitting a count of 113 for word and
    17:33:27 [Thread-30-count] INFO  com.microsoft.example.WordCount - Emitting a count of 57 for word dwarfs
    17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 57 for word snow

Cet exemple de journal indique le mot hello ' et ' a été émis 113 fois. Hello nombre continue toogo des tant que la topologie de hello s’exécute, car les bec hello émet en continu hello même phrase.

Il existe un intervalle de 5 secondes entre l’émission des mots et les décomptes. Hello **WordCount** composant est configuré tooonly émettre des informations lors de l’arrivée d’un tuple de la graduation. Il demande que tuples de graduation soient remis uniquement toutes les cinq secondes.

## <a name="convert-hello-topology-tooflux"></a>Convertir hello topologie tooFlux

Flux est une nouvelle infrastructure disponible avec Storm 0.10.0 et versions ultérieure, ce qui vous permet de configuration tooseparate à partir de l’implémentation. Vos composants sont toujours définies dans Java, mais la topologie de hello est définie à l’aide d’un fichier YAML. Vous pouvez empaqueter une définition de la topologie par défaut avec votre projet, ou utiliser un fichier autonome lors de l’envoi de topologie de hello. Lors de la soumission hello topologie tooStorm, vous pouvez utiliser les valeurs de toopopulate de fichiers de configuration ou les variables d’environnement dans la définition de la topologie YAML de hello.

fichier YAML Hello définit toouse de composants hello pour la topologie de hello et hello des flux de données entre eux. Vous pouvez inclure un fichier YAML en tant que partie du fichier jar de hello, ou vous pouvez utiliser un fichier YAML externe.

Pour plus d’informations sur Flux, voir [Infrastructure Flux (https://storm.apache.org/releases/0.10.0/flux.html)](https://storm.apache.org/releases/0.10.0/flux.html).

> [!WARNING]
> Échéance tooa [bogue (https://issues.apache.org/jira/browse/STORM-2055)](https://issues.apache.org/jira/browse/STORM-2055) Storm 1.0.1, vous devrez peut-être tooinstall un [environnement de développement Storm](https://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html) toorun les topologies de Flux localement.

1. Déplacer hello `WordCountTopology.java` fichier de projet de hello. Auparavant, ce fichier définis de topologie de hello, mais n’est pas nécessaire avec le Flux.

2. Bonjour `resources` répertoire, créez un fichier nommé `topology.yaml`. Utilisez hello après le texte en tant que contenu hello de ce fichier.

        name: "wordcount"       # friendly name for hello topology
        
        config:                 # Topology configuration
        topology.workers: 1     # Hint for hello number of workers toocreate
        
        spouts:                 # Spout definitions
        - id: "sentence-spout"
            className: "com.microsoft.example.RandomSentenceSpout"
            parallelism: 1      # parallelism hint
        
        bolts:                  # Bolt definitions
        - id: "splitter-bolt"
            className: "com.microsoft.example.SplitSentence"
            parallelism: 1
         
        - id: "counter-bolt"
            className: "com.microsoft.example.WordCount"
            constructorArgs:
                - 10
            parallelism: 1
        
        streams:                # Stream definitions
            - name: "Spout --> Splitter" # name isn't used (placeholder for logging, UI, etc.)
            from: "sentence-spout"       # hello stream emitter
            to: "splitter-bolt"          # hello stream consumer
            grouping:                    # Grouping type
                type: SHUFFLE
          
            - name: "Splitter -> Counter"
            from: "splitter-bolt"
            to: "counter-bolt"
            grouping:
            type: FIELDS
                args: ["word"]           # field(s) toogroup on

3. Rendre hello suit les modifications toohello `pom.xml` fichier.
   
   * Ajouter hello suivant nouvelle dépendance Bonjour `<dependencies>` section :
     
        ```xml
        <!-- Add a dependency on hello Flux framework -->
        <dependency>
            <groupId>org.apache.storm</groupId>
            <artifactId>flux-core</artifactId>
            <version>${storm.version}</version>
        </dependency>
        ```
   * Ajouter hello suivant plug-in toohello `<plugins>` section. Ce plug-in gère la création d’un package (fichier jar) hello pour le projet de hello et applique certains tooFlux spécifique de transformations lors de la création de package de hello.
     
        ```xml
        <!-- build an uber jar -->
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-shade-plugin</artifactId>
            <version>2.3</version>
            <configuration>
                <transformers>
                    <!-- Keep us from getting a "can't overwrite file error" -->
                    <transformer implementation="org.apache.maven.plugins.shade.resource.ApacheLicenseResourceTransformer" />
                    <transformer implementation="org.apache.maven.plugins.shade.resource.ServicesResourceTransformer" />
                    <!-- We're using Flux, so refer tooit as main -->
                    <transformer implementation="org.apache.maven.plugins.shade.resource.ManifestResourceTransformer">
                        <mainClass>org.apache.storm.flux.Flux</mainClass>
                    </transformer>
                </transformers>
                <!-- Keep us from getting a bad signature error -->
                <filters>
                    <filter>
                        <artifact>*:*</artifact>
                        <excludes>
                            <exclude>META-INF/*.SF</exclude>
                            <exclude>META-INF/*.DSA</exclude>
                            <exclude>META-INF/*.RSA</exclude>
                        </excludes>
                    </filter>
                </filters>
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
        ```

   * Bonjour **exec-maven plug-in** `<configuration>` section, modifiez la valeur hello pour `<mainClass>` trop`org.apache.storm.flux.Flux`. Ce paramètre permet de toohandle du Flux en cours d’exécution topologie de hello localement dans le développement.

   * Bonjour `<resources>` section, ajoutez hello suivant toohello `<includes>`. Ce code XML inclut un fichier YAML hello qui définit la topologie de hello en tant que partie du projet de hello.

        ```xml
        <include>topology.yaml</include>
        ```

## <a name="test-hello-flux-topology-locally"></a>Topologie de flux hello test localement

1. Utilisez hello suivant toocompile et exécuter la topologie de Flux de hello à l’aide de Maven :

    ```bash
    mvn compile exec:java -Dexec.args="--local -R /topology.yaml"
    ```

    Si vous utilisez PowerShell, utilisez hello de commande suivante :

    ```bash
    mvn compile exec:java "-Dexec.args=--local -R /topology.yaml"
    ```

    > [!WARNING]
    > Si votre topologie utilise des bits Storm 1.0.1, cette commande échoue. Cet échec est dû à [https://issues.apache.org/jira/browse/STORM-2055](https://issues.apache.org/jira/browse/STORM-2055). Au lieu de cela, [installer Storm dans votre environnement de développement](http://storm.apache.org/releases/0.10.0/Setting-up-development-environment.html) et hello d’utiliser les informations suivantes.

    Si vous avez [installé Storm dans votre environnement de développement](http://storm.apache.org/releases/0.10.0/Setting-up-development-environment.html), vous pouvez utiliser hello suivant à la place les commandes :

    ```bash
    mvn compile package
    storm jar target/WordCount-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local -R /topology.yaml
    ```

    Hello `--local` paramètre exécute la topologie de hello en mode local sur votre environnement de développement. Hello `-R /topology.yaml` paramètre utilise hello `topology.yaml` ressource de fichier à partir de la topologie de hello jar fichier toodefine hello.

    En cours d’exécution, la topologie de hello affiche des informations de démarrage. Hello suivant le texte est un exemple de sortie de hello :

        17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 56 for word snow
        17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 56 for word white
        17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 112 for word seven
        17:33:27 [Thread-16-count] INFO  com.microsoft.example.WordCount - Emitting a count of 195 for word the
        17:33:27 [Thread-30-count] INFO  com.microsoft.example.WordCount - Emitting a count of 113 for word and
        17:33:27 [Thread-30-count] INFO  com.microsoft.example.WordCount - Emitting a count of 57 for word dwarfs

    Il existe un délai de 10 secondes entre chaque lot d’informations enregistrées.

2. Effectuer une copie de hello `topology.yaml` fichier de projet de hello. Nouveau fichier de nom hello `newtopology.yaml`. Bonjour `newtopology.yaml` de fichiers, Rechercher suivant de hello section et modifier la valeur hello `10` trop`5`. Compte de cet intervalle de hello modification modifications entre l’émission de lots de word à partir de too5 de 10 secondes.

    ```yaml
    - id: "counter-bolt"
    className: "com.microsoft.example.WordCount"
    constructorArgs:
    - 5
    parallelism: 1
    ```yaml

3. toorun hello topology, use hello following command:

    ```bash
    mvn exec:java -Dexec.args="--local /path/to/newtopology.yaml"
    ```

    Ou, si vous avez Storm dans votre environnement de développement :

    ```bash
    storm jar target/WordCount-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local /path/to/newtopology.yaml
    ```

    Hello de modification `/path/to/newtopology.yaml` toohello chemin d’accès toohello newtopology.yaml fichier créé à l’étape précédente de hello. Cette commande utilise hello newtopology.yaml en tant que définition de la topologie hello. Étant donné que nous n’avez pas incluses hello `compile` paramètre, Maven utilise hello version de hello projet créé dans les étapes précédentes.

    Une fois hello topologie démarre, vous devez remarquer que heure hello entre les traitements émis a changé de valeur hello tooreflect newtopology.yaml. Par conséquent, vous pouvez voir que vous pouvez modifier votre configuration via un fichier YAML sans avoir de topologie de hello toorecompile.

Pour plus d’informations sur d’autres fonctionnalités de l’infrastructure de Flux hello, consultez [Flux (https://storm.apache.org/releases/0.10.0/flux.html)](https://storm.apache.org/releases/0.10.0/flux.html).

## <a name="trident"></a>Trident

Trident est une abstraction de haut niveau fournie par Storm. Il prend en charge le traitement avec état. Hello principal avantage de Trident est qu’il peut garantir que chaque message qui entre dans la topologie de hello est traitée qu’une seule fois. Sans utilisation de Trident, votre topologie peut uniquement garantir que les messages sont traités au moins une fois. Il existe aussi d'autres différences, comme les composants intégrés pouvant être utilisés, plutôt que de créer des bolts. Les Bolts sont remplacés par des composants moins génériques, tels que des filtres, des projections et des fonctions.

Les applications Trident peuvent être créées à l’aide de projets Maven. Vous utilisez hello même étapes présenté plus haut dans cet article : uniquement le code hello est différent. Trident également (actuellement) sont inutilisables avec l’infrastructure de Flux hello.

Pour plus d’informations sur Trident, consultez hello [présentation de l’API Trident](http://storm.apache.org/documentation/Trident-API-Overview.html).

Pour obtenir un exemple d’application Trident, consultez les [Rubriques de tendances Twitter avec Apache Storm sur HDInsight](hdinsight-storm-twitter-trending.md).

## <a name="next-steps"></a>Étapes suivantes

Vous avez appris comment toocreate une topologie Storm à l’aide de Java. Apprenez maintenant à effectuer les actions suivantes :

* [Déploiement et gestion des topologies Apache Storm sur HDInsight](hdinsight-storm-deploy-monitor-topology.md)

* [Développement de topologies C# pour Apache Storm dans HDInsight à l'aide de Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md)

Vous trouverez davantage d’exemples de topologies Storm en vous rendant sur [Exemples de topologies Storm sur HDInsight](hdinsight-storm-example-topology.md).

