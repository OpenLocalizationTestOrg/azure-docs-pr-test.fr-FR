---
title: "aaaApache Storm écrire tooStorage/Data Lake Store - Azure HDInsight | Documents Microsoft"
description: "Découvrez comment toouse hello stockage de toohello compatible HDFS Apache Storm toowrite pour HDInsight. Azure Storage ou Azure Data Lake Store fournir un stockage hello HDFS-comptabile pour HDInsight. Ce document et hello exemple associé, montrent comment les composants de HdfsBolt hello peuvent être des toowrite utilisé toohello du stockage par défaut d’une tempête sur le cluster HDInsight."
services: hdinsight
documentationcenter: na
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 1df98653-a6c8-4662-a8c6-5d288fc4f3a6
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/19/2017
ms.author: larryfr
ms.openlocfilehash: d76159a9ecd1be18e519511cfdb3bcfd18ae4d33
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="write-toohdfs-from-apache-storm-on-hdinsight"></a>Écrire des tooHDFS à partir d’Apache Storm sur HDInsight

Découvrez comment toouse Storm toowrite données toohello stockage de HDFS compatibles utilisé par Apache Storm sur HDInsight. HDInsight peut utiliser à la fois le stockage Azure et Azure Data Lake comme stockage compatible HDFS. Storm fournit un [HdfsBolt](http://storm.apache.org/releases/1.1.0/javadocs/org/apache/storm/hdfs/bolt/HdfsBolt.html) composant qui écrit des données tooHDFS. Ce document fournit des informations sur l’écriture de type tooeither de stockage à partir de hello HdfsBolt. 

> [!IMPORTANT]
> exemple Hello topologie utilisée dans ce document s’appuie sur les composants qui sont inclus avec Storm sur HDInsight. Vous devrez peut-être toowork modification avec Azure Data Lake Store lorsqu’il est utilisé avec les autres clusters Apache Storm.

## <a name="get-hello-code"></a>Obtenir le code de hello

projet Hello contenant cette topologie est disponible en téléchargement à partir de [https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store](https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store).

toocompile ce projet, vous devez hello configuration pour votre environnement de développement suivante :

* [Java JDK 1.8](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) ou version ultérieure. HDInsight 3.5 ou les versions ultérieures requièrent Java 8.

* [Maven 3.x](https://maven.apache.org/download.cgi)

Hello variables d’environnement suivantes peuvent être définis lors de l’installation de Java et hello JDK sur votre station de travail de développement. Toutefois, vous devez vérifier qu’ils existent et qu’ils contiennent des valeurs correctes de hello pour votre système.

* `JAVA_HOME`-doit pointer toohello répertoire où hello JDK est installé.
* `PATH`-doit contenir hello suivant des chemins d’accès :
  
    * `JAVA_HOME`(ou les chemins d’accès équivalents hello).
    * `JAVA_HOME\bin`(ou les chemins d’accès équivalents hello).
    * répertoire de Hello où Maven est installé.

## <a name="how-toouse-hello-hdfsbolt-with-hdinsight"></a>Comment toouse hello HdfsBolt avec HDInsight

> [!IMPORTANT]
> Avant d’utiliser hello HdfsBolt avec Storm sur HDInsight, vous devez d’abord utiliser un fichier de script action toocopy requis jar dans hello `extpath` de Storm. Pour plus d’informations, consultez hello [cluster hello de configurer](#configure) section.

Hello HdfsBolt utilise le schéma de fichier hello que vous fournissiez toounderstand comment toowrite tooHDFS. Hdinsight, utilisez une des hello suivant des schémas :

* `wasb://` : avec un compte de stockage Azure.
* `adl://` : avec Azure Data Lake Store.

Hello tableau suivant fournit des exemples d’utilisation de fichiers de schéma de hello pour différents scénarios :

| Schéma | Remarques |
| ----- | ----- |
| `wasb:///` | compte de stockage par défaut Hello est un conteneur d’objets blob dans un compte de stockage Azure |
| `adl:///` | compte de stockage par défaut Hello est un répertoire dans Azure Data Lake Store. Lors de la création du cluster, spécifiez hello répertoire dans Data Lake Store est la racine HDFS du cluster hello hello. Par exemple, hello `/clusters/myclustername/` active. |
| `wasb://CONTAINER@ACCOUNT.blob.core.windows.net/` | Compte de stockage Azure (supplémentaires) de celle par défaut associé hello cluster. |
| `adl://STORENAME/` | racine Hello hello utilisé par le cluster de hello Data Lake Store. Ce modèle vous permet de tooaccess les données qui se trouve en dehors du répertoire hello qui contient le système de fichiers du cluster hello. |

Pour plus d’informations, consultez hello [HdfsBolt](http://storm.apache.org/releases/1.1.0/javadocs/org/apache/storm/hdfs/bolt/HdfsBolt.html) référence sur le site Apache.org.

### <a name="example-configuration"></a>Exemple de configuration

Hello YAML suivant est un extrait de hello `resources/writetohdfs.yaml` fichier inclus dans l’exemple de hello. Ce fichier définit la topologie de Storm hello à l’aide de hello [Flux](https://storm.apache.org/releases/1.1.0/flux.html) framework d’Apache Storm.

```yaml
components:
  - id: "syncPolicy"
    className: "org.apache.storm.hdfs.bolt.sync.CountSyncPolicy"
    constructorArgs:
      - 1000

  - id: "rotationPolicy"
    className: "org.apache.storm.hdfs.bolt.rotation.NoRotationPolicy"

  - id: "fileNameFormat"
    className: "org.apache.storm.hdfs.bolt.format.DefaultFileNameFormat"
    configMethods:
      - name: "withPath"
        args: ["${hdfs.write.dir}"]
      - name: "withExtension"
        args: [".txt"]

  - id: "recordFormat"
    className: "org.apache.storm.hdfs.bolt.format.DelimitedRecordFormat"
    configMethods:
      - name: "withFieldDelimiter"
        args: ["|"]

# spout definitions
spouts:
  - id: "tick-spout"
    className: "com.microsoft.example.TickSpout"
    parallelism: 1


# bolt definitions
bolts:
  - id: "hdfs-bolt"
    className: "org.apache.storm.hdfs.bolt.HdfsBolt"
    configMethods:
      - name: "withConfigKey"
        args: ["hdfs.config"]
      - name: "withFsUrl"
        args: ["${hdfs.url}"]
      - name: "withFileNameFormat"
        args: [ref: "fileNameFormat"]
      - name: "withRecordFormat"
        args: [ref: "recordFormat"]
      - name: "withRotationPolicy"
        args: [ref: "rotationPolicy"]
      - name: "withSyncPolicy"
        args: [ref: "syncPolicy"]
```

Cette YAML définit hello éléments suivants :

* `syncPolicy`: Définit lorsque les fichiers système de fichiers toohello de synchronisé/vidés. Dans cet exemple, tous les 1 000 tuples.
* `fileNameFormat`: Définit hello chemin d’accès et nom du modèle toouse lors de l’écriture de fichiers. Dans cet exemple, le chemin d’accès hello est fourni lors de l’exécution à l’aide d’un filtre et l’extension de fichier hello est `.txt`.
* `recordFormat`: Définit le format interne de hello de fichiers hello écrits. Dans cet exemple, les champs sont délimités par hello `|` caractère.
* `rotationPolicy`: Définit quand les fichiers toorotate. Dans cet exemple, aucune rotation n’est effectuée.
* `hdfs-bolt`: Utilise hello composants précédentes en tant que paramètres de configuration pour hello `HdfsBolt` classe.

Pour plus d’informations sur l’infrastructure de Flux hello, consultez [https://storm.apache.org/releases/1.1.0/flux.html](https://storm.apache.org/releases/1.1.0/flux.html).

## <a name="configure-hello-cluster"></a>Configurer le cluster de hello

Par défaut, Storm sur HDInsight n’inclut pas les composants hello que HdfsBolt utilise toocommunicate avec le stockage Azure ou Data Lake Store dans le chemin de classe de Storm. Le script suivant de hello d’utilisation action tooadd toohello de ces composants `extlib` répertoire de Storm sur votre cluster :

| URI de script | Nœuds tooapply à | Paramètres || `https://000aarperiscus.blob.core.windows.net/certs/stormextlib.sh` | Nimbus, superviseur | None |

Pour plus d’informations sur l’utilisation de ce script avec votre cluster, consultez hello [HDInsight de personnaliser des clusters à l’aide des actions de script](./hdinsight-hadoop-customize-cluster-linux.md) document.

## <a name="build-and-package-hello-topology"></a>Générez et Empaquetez la topologie de hello

1. Télécharger le projet d’exemple hello à partir de [https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store ](https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store) tooyour les environnement de développement.

2. À partir d’une invite de commandes, Terminal Server ou la session d’interpréteur de commandes, modification de répertoires toohello racine hello téléchargé le projet. toobuild et package hello topologie, utiliser hello commande suivante :
   
        mvn compile package
   
    Une fois la génération de hello et l’empaquetage terminée, il existe un nouveau répertoire nommé `target`, qui contient un fichier nommé `StormToHdfs-1.0-SNAPSHOT.jar`. Ce fichier contient la topologie de hello compilé.

## <a name="deploy-and-run-hello-topology"></a>Déployer et exécuter la topologie de hello

1. Utilisez hello suivant du cluster HDInsight de commande toocopy hello topologie toohello. Remplacez **utilisateur** avec le nom d’utilisateur SSH hello que vous avez utilisé lors de la création du cluster de hello. Remplacez **CLUSTERNAME** avec nom hello du cluster de hello.
   
        scp target\StormToHdfs-1.0-SNAPSHOT.jar USER@CLUSTERNAME-ssh.azurehdinsight.net:StormToHdfs1.0-SNAPSHOT.jar
   
    Lorsque vous y êtes invité, spécifiez hello mot de passe lors de la création d’utilisateur SSH hello pour le cluster de hello. Si vous avez utilisé une clé publique au lieu d’un mot de passe, vous devrez peut-être toouse hello `-i` paramètre toospecify hello chemin d’accès toohello correspondant à une clé privée.
   
   > [!NOTE]
   > Pour en savoir plus sur l’utilisation de `scp` avec HDInsight, voir [Utiliser SSH avec Hadoop - Azure HDInsight](./hdinsight-hadoop-linux-use-ssh-unix.md).

2. Une fois le téléchargement de hello terminé, utilisez hello suivant tooconnect toohello HDInsight cluster à l’aide de SSH. Remplacez **utilisateur** avec le nom d’utilisateur SSH hello que vous avez utilisé lors de la création du cluster de hello. Remplacez **CLUSTERNAME** avec nom hello du cluster de hello.
   
        ssh USER@CLUSTERNAME-ssh.azurehdinsight.net
   
    Lorsque vous y êtes invité, spécifiez hello mot de passe lors de la création d’utilisateur SSH hello pour le cluster de hello. Si vous avez utilisé une clé publique au lieu d’un mot de passe, vous devrez peut-être toouse hello `-i` paramètre toospecify hello chemin d’accès toohello correspondant à une clé privée.
   
   Pour en savoir plus, voir [Utilisation de SSH avec Hadoop Linux sur HDInsight depuis Linux, Unix ou OS X](hdinsight-hadoop-linux-use-ssh-unix.md).

3. Une fois connecté, utilisez hello commande suivante toocreate un fichier nommé `dev.properties`:

        nano dev.properties

4. Hello utilisation après le texte en tant que contenu hello Hello `dev.properties` fichier :

        hdfs.write.dir: /stormdata/
        hdfs.url: wasb:///

    > [!IMPORTANT]
    > Cet exemple suppose que votre cluster utilise un compte de stockage Azure en tant que stockage par défaut de hello. Si votre cluster utilise Azure Data Lake Store, utilisez `hdfs.url: adl:///` à la place.
    
    fichier de hello toosave, utilisez __Ctrl + X__, puis __Y__et enfin __entrée__. Hello dans ce fichier valeur hello Data Lake store URL et le nom du répertoire hello que les données sont écrites dans.

3. Utilisez hello suivant la topologie de commande toostart hello :
   
        storm jar StormToHdfs-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /writetohdfs.yaml --filter dev.properties

    Cette commande démarre la topologie hello à l’aide du framework de Flux hello en le soumettant à nœud de Nimbus toohello du cluster de hello. topologie de Hello est définie par hello `writetohdfs.yaml` fichier inclus dans le fichier jar de hello. Hello `dev.properties` fichier est passé en tant que filtre et les valeurs hello contenues dans le fichier de hello sont lues par la topologie de hello.

## <a name="view-output-data"></a>Affichage des données de sortie

les données de salutation tooview, utilisez hello de commande suivante :

    hdfs dfs -ls /stormdata/

Une liste de fichiers hello créés par cette topologie s’affiche.

Hello liste suivante est un exemple de données hello retournées par les commandes précédentes hello :

    Found 30 items
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-0-1488568403092.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-1-1488568404567.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-10-1488568408678.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-11-1488568411636.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-12-1488568411884.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-13-1488568412603.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-14-1488568415055.txt

## <a name="stop-hello-topology"></a>Arrêter la topologie de hello

Les topologies Storm exécuter jusqu'à l’arrêt, ou cluster de hello est supprimé. toostop hello topologie, utilisez hello de commande suivante :

    storm kill hdfswriter

## <a name="delete-your-cluster"></a>Supprimer votre cluster

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a>Étapes suivantes

Maintenant que vous avez appris comment toouse Storm toowrite tooAzure stockage et Azure Data Lake Store, découvrir les autres [renverser exemples pour HDInsight](hdinsight-storm-example-topology.md).

