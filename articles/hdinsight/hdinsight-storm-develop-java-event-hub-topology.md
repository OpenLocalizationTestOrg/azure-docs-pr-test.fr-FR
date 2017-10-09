---
title: "les événements de concentrateurs d’événements avec Storm sur HDInsight à l’aide de Java aaaProcess | Documents Microsoft"
description: "Découvrez comment tooprocess données concentrateurs d’événements avec une topologie Java Storm créé avec Maven."
services: hdinsight,notification hubs
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 453fa7b0-c8a6-413e-8747-3ac3b71bed86
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/13/2017
ms.author: larryfr
ms.openlocfilehash: 6506f5bc8f6ab0e29350c071a3f84433382038e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="process-events-from-azure-event-hubs-with-storm-on-hdinsight-java"></a>Traitement des événements Azure Event Hubs avec Storm sur HDInsight (Java)

Découvrez comment toouse Azure Event Hubs avec Storm sur HDInsight. Cet exemple utilise des composants basés sur Java tooread et écrire les données dans Azure Event Hubs.

Les concentrateurs d’événements Azure vous permet de tooprocess de gros volumes de données à partir de sites Web, des applications et des périphériques. Hello bec de concentrateur d’événements rend facile toouse Apache renverser sur HDInsight tooanalyze ces données en temps réel. Vous pouvez également écrire des données tooEvent concentrateurs à partir de Storm à l’aide de hello boulon de concentrateurs d’événements.

## <a name="prerequisites"></a>Composants requis

* Un cluster Apache Storm sur HDInsight version 3.6. Pour plus d’informations, voir [Prise en main de Storm sur HDInsight](hdinsight-apache-storm-tutorial-get-started-linux.md).

    > [!IMPORTANT]
    > Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure. Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

* Un [hub d’événements Azure](../event-hubs/event-hubs-csharp-ephcs-getstarted.md).

* [Kit de développeur Java (JDK) Oracle version 8](http://www.oracle.com/technetwork/java/javase/downloads/index.html) ou un équivalent, par exemple, [OpenJDK](http://openjdk.java.net/).

* [Maven](https://maven.apache.org/download.cgi) : Maven est un système de génération de projet pour les projets Java.

* Un éditeur de texte ou un environnement de développement intégré (IDE).

    > [!NOTE]
    > Votre éditeur ou IDE peut avoir des fonctionnalités spécifiques pour l’utilisation avec Maven, qui ne sont pas traitées dans ce document. Pour plus d’informations sur les fonctionnalités de hello de votre environnement d’édition, consultez la documentation hello pour produit hello que vous utilisez.

    * Un client SSH. Pour en savoir plus, voir [Utilisation de SSH avec Hadoop Linux sur HDInsight depuis Linux, Unix ou OS X](hdinsight-hadoop-linux-use-ssh-unix.md).

* Hello `ssh` et `scp` commandes. Il s’agit de cluster de HDInsight utilisé toocopy fichiers toohello. Sous Windows, vous pouvez les obtenir via Bash dans Windows 10.

## <a name="understanding-hello-example"></a>Exemple hello de présentation

Hello [hdinsight-java-storm-eventhub](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub) exemple contient deux topologies :

Hello `resources/writer.yaml` topologie écrit des données aléatoires tooan concentrateur d’événements Azure. les données de salutation sont générées par hello `DeviceSpout` composant, et est une valeur de l’appareil et un ID de périphérique aléatoire. Ainsi, elles simulent certains matériels qui émettent un ID de chaîne et une valeur numérique.

Les trois `resources/reader.yaml` topologie lit des données à partir du concentrateur d’événements (écrites par EventHubWriter, les données hello) analyse les données JSON de hello et ouvre une session hello `deviceId` et `deviceValue` données.

les données de salutation sont mise en forme comme un document JSON avant d’être écrite tooEvent Hub et lors de la lecture par le lecteur de hello il est analysé en dehors de JSON et dans des tuples. format JSON Hello est comme suit :

    { "deviceId": "unique identifier", "deviceValue": some value }

### <a name="project-configuration"></a>Configuration du projet

Hello `POM.xml` fichier contient des informations de configuration pour ce projet Maven. intéressantes Hello sont :

#### <a name="event-hub-components"></a>Composants Event Hub

composant de Hello qui lit et écrit les concentrateurs d’événements tooAzure se trouve dans hello [HDInsight référentiel](https://github.com/hdinsight/mvn-rep). Hello suivants sections Bonjour `POM.xml` composants hello du chargement de fichiers à partir de ce référentiel

```xml
<repositories>
    <repository>
        <id>hdinsight-examples</id>
        <url>http://raw.github.com/hdinsight/mvn-repo/master</url>
    </repository>
</repositories>
```

#### <a name="hello-eventhubs-storm-spout-dependency"></a>Hello bec de Storm EventHubs de dépendance

```xml
<dependency>
    <groupId>com.microsoft</groupId>
    <artifactId>eventhubs</artifactId>
    <version>${storm.eventhub.version}</version>
</dependency>
```

Ce code xml définit une dépendance pour le package hello eventhubs, qui contient à la fois un bec pour lire à partir de concentrateurs d’événements et un éclair pour l’écriture de tooit.

```xml
</source>
    <target>1.8</target>
    </configuration>
</plugin>
```

Ce code xml configure la sortie du toogenerate hello projet Java 8, qui est utilisé par HDInsight 3.5 ou version ultérieure.

#### <a name="hello-maven-shade-plugin"></a>Hello maven-ton plug-in

```xml
<!-- build an uber jar -->
<plugin>
<groupId>org.apache.maven.plugins</groupId>
<artifactId>maven-shade-plugin</artifactId>
<version>2.3</version>
<configuration>
    <transformers>
    <!-- Keep us from getting a can't overwrite file error -->
    <transformer implementation="org.apache.maven.plugins.shade.resource.ApacheLicenseResourceTransformer"/>
    <transformer implementation="org.apache.maven.plugins.shade.resource.ServicesResourceTransformer"/>
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

Ce code xml configure la sortie de hello hello solution toopackage dans un fichier jar générale. jar de Hello contient le code de projet hello et les dépendances requises. Il est également utilisé pour :

* Renommez les fichiers de licence pour les dépendances de hello.
* Exclure les sécurités/signatures.
* Vérifiez que plusieurs implémentations de hello même interface sont fusionnées en une seule entrée.

Ces paramètres de configuration évitent les erreurs au moment de l’exécution.

#### <a name="topology-definitions"></a>Définitions de topologie

Cet exemple utilise hello [Flux](https://storm.apache.org/releases/1.1.0/flux.html) framework. Cette infrastructure utilise les topologies hello YAML toodefine. Hello le principal avantage est que vous n’êtes pas dur codage topologie hello dans le code Java. Définition de hello étant YAML, vous pouvez le modifier avant de soumettre la topologie de hello, sans avoir à toorecompile tous les éléments.

__writer.yaml__ :

```yaml
---
# Topology that reads from Event Hubs
name: "eventhubwriter"

components:
  # Configure hello Event Hub spout
  - id: "eventhubbolt-config"
    className: "org.apache.storm.eventhubs.bolt.EventHubBoltConfig"
    constructorArgs:
      # These are populated from hello .properties file when hello topology is started
      - "${eventhub.write.policy.name}"
      - "${eventhub.write.policy.key}"
      - "${eventhub.namespace}"
      - "servicebus.windows.net"
      - "${eventhub.name}"

spouts:
  - id: "device-emulator-spout"
    className: "com.microsoft.example.DeviceSpout"
    parallelism: ${eventhub.partitions}

bolts:
  - id: "eventhub-bolt"
    className: "org.apache.storm.eventhubs.bolt.EventHubBolt"
    constructorArgs:
      - ref: "eventhubbolt-config" # config declared in components section
    # parallelism hint. This should be hello same as hello number of partitions for your Event Hub, so we read it from hello dev.properties file passed at run time.
    parallelism: ${eventhub.partitions}

  # Log information
  - id: "log-bolt"
    className: "org.apache.storm.flux.wrappers.bolts.LogInfoBolt"
    parallelism: 1

# How data flows through hello components
streams:
  - name: "spout -> eventhub" # just a string used for logging
    from: "device-emulator-spout"
    to: "eventhub-bolt"
    grouping:
        type: SHUFFLE

  - name: "spout -> logger"
    from: "device-emulator-spout"
    to: "log-bolt"
    grouping:
        type: SHUFFLE
```

__reader.yaml__ :

```yaml
---
# Topology that reads from Event Hubs
name: "eventhubreader"

components:
  # Configure hello Event Hub spout
  - id: "eventhubspout-config"
    className: "org.apache.storm.eventhubs.spout.EventHubSpoutConfig"
    constructorArgs:
      # These are populated from hello .properties file when hello topology is started
      - "${eventhub.read.policy.name}"
      - "${eventhub.read.policy.key}"
      - "${eventhub.namespace}"
      - "${eventhub.name}"
      - ${eventhub.partitions}

spouts:
  - id: "eventhub-spout"
    className: "org.apache.storm.eventhubs.spout.EventHubSpout"
    constructorArgs:
      - ref: "eventhubspout-config" # config declared in components section
    # parallelism hint. This should be hello same as hello number of partitions for your Event Hub, so we read it from hello dev.properties file passed at run time.
    parallelism: ${eventhub.partitions}

bolts:
  # Log information
  - id: "log-bolt"
    className: "org.apache.storm.flux.wrappers.bolts.LogInfoBolt"
    parallelism: 1

  # Parses from JSON into tuples
  - id: "parser-bolt"
    className: "com.microsoft.example.ParserBolt"
    parallelism: ${eventhub.partitions}

# How data flows through hello components
streams:
  - name: "spout -> parser" # just a string used for logging
    from: "eventhub-spout"
    to: "parser-bolt"
    grouping:
        type: SHUFFLE

  - name: "parser -> log-bolt"
    from: "parser-bolt"
    to: "log-bolt"
    grouping:
        type: SHUFFLE
```

#### <a name="tell-hello-topology-about-event-hub"></a>Topologie de hello dire de concentrateur d’événements

Au moment de l’exécution, hello `dev.properties` fichier est utilisé toopass hello concentrateur d’événements configuration toohello topologie. Hello exemple suivant est contenu par défaut de hello du fichier de hello :

```yaml
eventhub.write.policy.name: writer
eventhub.write.policy.key: your_key_here
eventhub.read.policy.name: reader
eventhub.read.policy.key: your_key_here
eventhub.namespace: your_namespace_here
eventhub.name: storm
eventhub.partitions: 2
```

## <a name="configure-environment-variables"></a>Configuration des variables d’environnement

Hello variables d’environnement suivantes peuvent être définis lors de l’installation de Java et hello JDK sur votre station de travail de développement. Toutefois, vous devez vérifier qu’ils existent et qu’ils contiennent des valeurs correctes de hello pour votre système.

* **JAVA_HOME** -doit pointer Active toohello où hello Java runtime environment (JRE) est installé. Par exemple, dans une distribution Unix ou Linux, il doit avoir une valeur similaire trop`/usr/lib/jvm/java-7-oracle`. Dans Windows, il aurait une valeur similaire trop`c:\Program Files (x86)\Java\jre1.7`
* **Chemin d’accès** -doit contenir hello suivant des chemins d’accès :

  * **JAVA_HOME** (ou les chemins d’accès équivalents hello)
  * **JAVA_HOME\bin** (ou les chemins d’accès équivalents hello)
  * répertoire d’Hello installation Maven

## <a name="configure-event-hub"></a>Configuration du hub d'événements

Concentrateurs d’événements est la source de données de hello pour cet exemple. Utilisez hello suivant les étapes toocreate un concentrateur d’événements.

1. À partir de hello [portail classique Azure](https://manage.windowsazure.com), sélectionnez **nouveau** > **Service Bus** > **concentrateur d’événements**  >  **Création personnalisée**.

2. Sur hello **ajouter un concentrateur d’événements** écran, entrez un **nom de Hub d’événements**. Sélectionnez hello **région** toocreate hello concentrateur, puis créer un espace de noms ou sélectionnez-en un existant. Enfin, cliquez sur hello **flèche** toocontinue.

    ![page 1 de l’assistant](./media/hdinsight-storm-develop-csharp-event-hub-topology/wiz1.png)

   > [!NOTE]
   > Sélectionnez hello même **emplacement** comme votre Storm sur HDInsight serveur tooreduce latence et les coûts.

3. Sur hello **concentrateur d’événements configurer** écran, entrez hello **nombre de Partition** et **rétention des messages** valeurs. Pour cet exemple, entrez 10 pour le nombre de partitions et 1 pour la conservation des messages. Notez le nombre de partitions hello, car vous avez besoin de cette valeur ultérieurement.

    ![page 2 de l’assistant](./media/hdinsight-storm-develop-csharp-event-hub-topology/wiz2.png)

4. Une fois le concentrateur d’événements hello a été créé, sélectionnez hello espace de noms, sélectionnez **concentrateurs d’événements**, puis sélectionnez le concentrateur d’événements hello que vous avez créé précédemment.
5. Sélectionnez **configurer**, puis créez deux nouvelles stratégies d’accès à l’aide de hello informations suivantes :

    <table>
    <tr><th>Nom</th><th>Autorisations</th></tr>
    <tr><td>Writer</td><td>Envoyer</td></tr>
    <tr><td>Lecteur</td><td>Écouter</td></tr>
    </table>

    Après avoir créé des autorisations de hello, sélectionnez hello **enregistrer** icône bas hello de page de hello. Ces stratégies d’accès partagé sont utilisé tooread et écrire tooEvent Hub.

    ![stratégies](./media/hdinsight-storm-develop-csharp-event-hub-topology/policy.png)

6. Après avoir enregistré les stratégies hello, utilisez hello **Générateur de clés d’accès partagé** bas hello de clé hello page tooretrieve hello hello **writer** et **lecteur** stratégies. Enregistrez ces clés.

## <a name="download-and-build-hello-project"></a>Télécharger et générer le projet de hello

1. Télécharger le projet de hello à partir de GitHub : [hdinsight-java-storm-eventhub](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub). Vous pouvez télécharger le package hello sous la forme d’une archive zip, ou utilisez [git](https://git-scm.com/) tooclone le projet hello local.

2. Modifier hello `dev.properties` fichier de configuration hello pour votre concentrateur d’événements.

3. Utilisez hello suivant du projet de hello toobuild et le package :

        mvn package

    Cette commande télécharge les dépendances nécessaires, builds, et puis packages hello projet. sortie de Hello est stockée dans hello **/target** répertoire comme **EventHubExample-1.0-SNAPSHOT.jar**.

## <a name="test-locally"></a>Tester les topologies localement

Étant donné que ces topologies uniquement lire et écrire tooEvent Hubs, vous pouvez les tester localement si vous avez un [environnement de développement Storm](http://storm.apache.org/releases/current/Setting-up-development-environment.html). Utilisez hello suivant toorun étapes localement dans l’environnement de développement hello :

1. Enregistreur de hello, exécutez :

        storm jar EventHubExample-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local -R /writer.yaml --filter dev.properties

2. Lecteur de hello, exécutez :

        storm jar EventHubExample-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local -R /reader.yaml --filter dev.properties

> [!TIP]
> * `--local`: Topologie hello exécution en mode local (non distribuées).
> * `-R /writer.yaml`: Charger la définition de la topologie hello de hello `resources` empaquetées dans le fichier jar de hello. Si la topologie de hello est un fichier sur le système de fichiers local hello, spécifiez tooit de chemin d’accès hello comme dernier paramètre de hello.
> * `--filter dev.properties`: Utilisez contenu hello de `dev.properties` toofill dans les valeurs hello dans les définitions de topologie hello. Par exemple, `${eventhub.read.policy.name}`.

Sortie est journalisée toohello console s’exécute en local. Utilisez __Ctrl + C__ topologie de hello toostop.

## <a name="deploy-hello-topologies"></a>Déployer des topologies de hello

1. Utilisez SCP toocopy hello jar package tooyour cluster HDInsight. Remplacez le nom d’utilisateur à utilisateur SSH hello pour votre cluster. Remplacez CLUSTERNAME nom hello de votre cluster HDInsight :

        scp ./target/EventHubExample-1.0-SNAPSHOT.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:.

    Si vous avez utilisé un mot de passe pour votre compte SSH, vous êtes un mot de passe hello tooenter demandées. Si vous avez utilisé une clé SSH avec compte de hello, vous devrez peut-être toouse hello `-i` paramètre toospecify hello chemin d’accès toohello fichier de clé. Par exemple, `scp -i ~/.ssh/id_rsa ./target/EventHubExample-1.0-SNAPSHOT.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:.`

    Cette commande copie hello fichier toohello répertoire de base de votre utilisateur SSH sur le cluster de hello.

2. Une fois le téléchargement du fichier hello a terminé, utilisez le cluster HDInsight SSH tooconnect toohello. Remplacez **nom d’utilisateur** nom hello de votre connexion SSH. Remplacez **CLUSTERNAME** par le nom de votre cluster HDInsight :

        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net

    > [!NOTE]
    > Si vous avez utilisé un mot de passe pour votre compte SSH, vous êtes un mot de passe hello tooenter demandées. Si vous avez utilisé une clé SSH avec compte de hello, vous devrez peut-être toouse hello `-i` paramètre toospecify hello chemin d’accès toohello fichier de clé. Hello exemple suivant charge hello la clé privée `~/.ssh/id_rsa`:
    >
    > `ssh -i ~/.ssh/id_rsa USERNAME@CLUSTERNAME-ssh.azurehdinsight.net`

3. Utilisez hello suivant des topologies de commande toostart hello :

        storm jar EventHubExample-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /writer.yaml --filter dev.properties
        storm jar EventHubExample-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /reader.yaml --filter dev.properties

    > [!TIP]
    > * `--remote`: Soumet hello topologie toohello service Nimbus, ce qui démarre sur les nœuds de cluster de hello travail de hello.

4. les données tooview hello connecté, accédez à toohttps://CLUSTERNAME.azurehdinsight.net/stormui, où __CLUSTERNAME__ hello désigne votre cluster HDInsight. Sélectionnez les topologies hello et Descendre toohello composants. Sélectionnez hello __port__ entrée pour une instance d’un composant de tooview a enregistré des informations.

5. Utilisez hello suivant des topologies de hello toostop de commandes :

        storm kill reader
        storm kill writer

## <a name="delete-your-cluster"></a>Supprimer votre cluster

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a>Étapes suivantes

* [Exemples de topologies pour Storm dans HDInsight](hdinsight-storm-example-topology.md)
