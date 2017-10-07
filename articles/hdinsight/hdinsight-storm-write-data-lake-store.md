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
# <a name="write-toohdfs-from-apache-storm-on-hdinsight"></a><span data-ttu-id="4c4d3-105">Écrire des tooHDFS à partir d’Apache Storm sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="4c4d3-105">Write tooHDFS from Apache Storm on HDInsight</span></span>

<span data-ttu-id="4c4d3-106">Découvrez comment toouse Storm toowrite données toohello stockage de HDFS compatibles utilisé par Apache Storm sur HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4c4d3-106">Learn how toouse Storm toowrite data toohello HDFS-compatible storage used by Apache Storm on HDInsight.</span></span> <span data-ttu-id="4c4d3-107">HDInsight peut utiliser à la fois le stockage Azure et Azure Data Lake comme stockage compatible HDFS.</span><span class="sxs-lookup"><span data-stu-id="4c4d3-107">HDInsight can use both Azure Storage and Azure Data Lake store as HDFS-comptabile storage.</span></span> <span data-ttu-id="4c4d3-108">Storm fournit un [HdfsBolt](http://storm.apache.org/releases/1.1.0/javadocs/org/apache/storm/hdfs/bolt/HdfsBolt.html) composant qui écrit des données tooHDFS.</span><span class="sxs-lookup"><span data-stu-id="4c4d3-108">Storm provides an [HdfsBolt](http://storm.apache.org/releases/1.1.0/javadocs/org/apache/storm/hdfs/bolt/HdfsBolt.html) component that writes data tooHDFS.</span></span> <span data-ttu-id="4c4d3-109">Ce document fournit des informations sur l’écriture de type tooeither de stockage à partir de hello HdfsBolt.</span><span class="sxs-lookup"><span data-stu-id="4c4d3-109">This document provides information on writing tooeither type of storage from hello HdfsBolt.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="4c4d3-110">exemple Hello topologie utilisée dans ce document s’appuie sur les composants qui sont inclus avec Storm sur HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4c4d3-110">hello example topology used in this document relies on components that are included with Storm on HDInsight.</span></span> <span data-ttu-id="4c4d3-111">Vous devrez peut-être toowork modification avec Azure Data Lake Store lorsqu’il est utilisé avec les autres clusters Apache Storm.</span><span class="sxs-lookup"><span data-stu-id="4c4d3-111">It may require modification toowork with Azure Data Lake Store when used with other Apache Storm clusters.</span></span>

## <a name="get-hello-code"></a><span data-ttu-id="4c4d3-112">Obtenir le code de hello</span><span class="sxs-lookup"><span data-stu-id="4c4d3-112">Get hello code</span></span>

<span data-ttu-id="4c4d3-113">projet Hello contenant cette topologie est disponible en téléchargement à partir de [https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store](https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store).</span><span class="sxs-lookup"><span data-stu-id="4c4d3-113">hello project containing this topology is available as a download from [https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store](https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store).</span></span>

<span data-ttu-id="4c4d3-114">toocompile ce projet, vous devez hello configuration pour votre environnement de développement suivante :</span><span class="sxs-lookup"><span data-stu-id="4c4d3-114">toocompile this project, you need hello following configuration for your development environment:</span></span>

* <span data-ttu-id="4c4d3-115">[Java JDK 1.8](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="4c4d3-115">[Java JDK 1.8](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) or higher.</span></span> <span data-ttu-id="4c4d3-116">HDInsight 3.5 ou les versions ultérieures requièrent Java 8.</span><span class="sxs-lookup"><span data-stu-id="4c4d3-116">HDInsight 3.5 or higher require Java 8.</span></span>

* [<span data-ttu-id="4c4d3-117">Maven 3.x</span><span class="sxs-lookup"><span data-stu-id="4c4d3-117">Maven 3.x</span></span>](https://maven.apache.org/download.cgi)

<span data-ttu-id="4c4d3-118">Hello variables d’environnement suivantes peuvent être définis lors de l’installation de Java et hello JDK sur votre station de travail de développement.</span><span class="sxs-lookup"><span data-stu-id="4c4d3-118">hello following environment variables may be set when you install Java and hello JDK on your development workstation.</span></span> <span data-ttu-id="4c4d3-119">Toutefois, vous devez vérifier qu’ils existent et qu’ils contiennent des valeurs correctes de hello pour votre système.</span><span class="sxs-lookup"><span data-stu-id="4c4d3-119">However, you should check that they exist and that they contain hello correct values for your system.</span></span>

* <span data-ttu-id="4c4d3-120">`JAVA_HOME`-doit pointer toohello répertoire où hello JDK est installé.</span><span class="sxs-lookup"><span data-stu-id="4c4d3-120">`JAVA_HOME` - should point toohello directory where hello JDK is installed.</span></span>
* <span data-ttu-id="4c4d3-121">`PATH`-doit contenir hello suivant des chemins d’accès :</span><span class="sxs-lookup"><span data-stu-id="4c4d3-121">`PATH` - should contain hello following paths:</span></span>
  
    * <span data-ttu-id="4c4d3-122">`JAVA_HOME`(ou les chemins d’accès équivalents hello).</span><span class="sxs-lookup"><span data-stu-id="4c4d3-122">`JAVA_HOME` (or hello equivalent path).</span></span>
    * <span data-ttu-id="4c4d3-123">`JAVA_HOME\bin`(ou les chemins d’accès équivalents hello).</span><span class="sxs-lookup"><span data-stu-id="4c4d3-123">`JAVA_HOME\bin` (or hello equivalent path).</span></span>
    * <span data-ttu-id="4c4d3-124">répertoire de Hello où Maven est installé.</span><span class="sxs-lookup"><span data-stu-id="4c4d3-124">hello directory where Maven is installed.</span></span>

## <a name="how-toouse-hello-hdfsbolt-with-hdinsight"></a><span data-ttu-id="4c4d3-125">Comment toouse hello HdfsBolt avec HDInsight</span><span class="sxs-lookup"><span data-stu-id="4c4d3-125">How toouse hello HdfsBolt with HDInsight</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4c4d3-126">Avant d’utiliser hello HdfsBolt avec Storm sur HDInsight, vous devez d’abord utiliser un fichier de script action toocopy requis jar dans hello `extpath` de Storm.</span><span class="sxs-lookup"><span data-stu-id="4c4d3-126">Before using hello HdfsBolt with Storm on HDInsight, you must first use a script action toocopy required jar files into hello `extpath` for Storm.</span></span> <span data-ttu-id="4c4d3-127">Pour plus d’informations, consultez hello [cluster hello de configurer](#configure) section.</span><span class="sxs-lookup"><span data-stu-id="4c4d3-127">For more information, see hello [Configure hello cluster](#configure) section.</span></span>

<span data-ttu-id="4c4d3-128">Hello HdfsBolt utilise le schéma de fichier hello que vous fournissiez toounderstand comment toowrite tooHDFS.</span><span class="sxs-lookup"><span data-stu-id="4c4d3-128">hello HdfsBolt uses hello file scheme that you provide toounderstand how toowrite tooHDFS.</span></span> <span data-ttu-id="4c4d3-129">Hdinsight, utilisez une des hello suivant des schémas :</span><span class="sxs-lookup"><span data-stu-id="4c4d3-129">With HDInsight, use one of hello following schemes:</span></span>

* <span data-ttu-id="4c4d3-130">`wasb://` : avec un compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="4c4d3-130">`wasb://`: Used with an Azure Storage account.</span></span>
* <span data-ttu-id="4c4d3-131">`adl://` : avec Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="4c4d3-131">`adl://`: Used with Azure Data Lake Store.</span></span>

<span data-ttu-id="4c4d3-132">Hello tableau suivant fournit des exemples d’utilisation de fichiers de schéma de hello pour différents scénarios :</span><span class="sxs-lookup"><span data-stu-id="4c4d3-132">hello following table provides examples of using hello file scheme for different scenarios:</span></span>

| <span data-ttu-id="4c4d3-133">Schéma</span><span class="sxs-lookup"><span data-stu-id="4c4d3-133">Scheme</span></span> | <span data-ttu-id="4c4d3-134">Remarques</span><span class="sxs-lookup"><span data-stu-id="4c4d3-134">Notes</span></span> |
| ----- | ----- |
| `wasb:///` | <span data-ttu-id="4c4d3-135">compte de stockage par défaut Hello est un conteneur d’objets blob dans un compte de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="4c4d3-135">hello default storage account is a blob container in an Azure Storage account</span></span> |
| `adl:///` | <span data-ttu-id="4c4d3-136">compte de stockage par défaut Hello est un répertoire dans Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="4c4d3-136">hello default storage account is a directory in Azure Data Lake Store.</span></span> <span data-ttu-id="4c4d3-137">Lors de la création du cluster, spécifiez hello répertoire dans Data Lake Store est la racine HDFS du cluster hello hello.</span><span class="sxs-lookup"><span data-stu-id="4c4d3-137">During cluster creation, you specify hello directory in Data Lake Store that is hello root of hello cluster's HDFS.</span></span> <span data-ttu-id="4c4d3-138">Par exemple, hello `/clusters/myclustername/` active.</span><span class="sxs-lookup"><span data-stu-id="4c4d3-138">For example, hello `/clusters/myclustername/` directory.</span></span> |
| `wasb://CONTAINER@ACCOUNT.blob.core.windows.net/` | <span data-ttu-id="4c4d3-139">Compte de stockage Azure (supplémentaires) de celle par défaut associé hello cluster.</span><span class="sxs-lookup"><span data-stu-id="4c4d3-139">A non-default (additional) Azure storage account associated with hello cluster.</span></span> |
| `adl://STORENAME/` | <span data-ttu-id="4c4d3-140">racine Hello hello utilisé par le cluster de hello Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="4c4d3-140">hello root of hello Data Lake Store used by hello cluster.</span></span> <span data-ttu-id="4c4d3-141">Ce modèle vous permet de tooaccess les données qui se trouve en dehors du répertoire hello qui contient le système de fichiers du cluster hello.</span><span class="sxs-lookup"><span data-stu-id="4c4d3-141">This scheme allows you tooaccess data that is located outside hello directory that contains hello cluster file system.</span></span> |

<span data-ttu-id="4c4d3-142">Pour plus d’informations, consultez hello [HdfsBolt](http://storm.apache.org/releases/1.1.0/javadocs/org/apache/storm/hdfs/bolt/HdfsBolt.html) référence sur le site Apache.org.</span><span class="sxs-lookup"><span data-stu-id="4c4d3-142">For more information, see hello [HdfsBolt](http://storm.apache.org/releases/1.1.0/javadocs/org/apache/storm/hdfs/bolt/HdfsBolt.html) reference at Apache.org.</span></span>

### <a name="example-configuration"></a><span data-ttu-id="4c4d3-143">Exemple de configuration</span><span class="sxs-lookup"><span data-stu-id="4c4d3-143">Example configuration</span></span>

<span data-ttu-id="4c4d3-144">Hello YAML suivant est un extrait de hello `resources/writetohdfs.yaml` fichier inclus dans l’exemple de hello.</span><span class="sxs-lookup"><span data-stu-id="4c4d3-144">hello following YAML is an excerpt from hello `resources/writetohdfs.yaml` file included in hello example.</span></span> <span data-ttu-id="4c4d3-145">Ce fichier définit la topologie de Storm hello à l’aide de hello [Flux](https://storm.apache.org/releases/1.1.0/flux.html) framework d’Apache Storm.</span><span class="sxs-lookup"><span data-stu-id="4c4d3-145">This file defines hello Storm topology using hello [Flux](https://storm.apache.org/releases/1.1.0/flux.html) framework for Apache Storm.</span></span>

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

<span data-ttu-id="4c4d3-146">Cette YAML définit hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="4c4d3-146">This YAML defines hello following items:</span></span>

* <span data-ttu-id="4c4d3-147">`syncPolicy`: Définit lorsque les fichiers système de fichiers toohello de synchronisé/vidés.</span><span class="sxs-lookup"><span data-stu-id="4c4d3-147">`syncPolicy`: Defines when files are synched/flushed toohello file system.</span></span> <span data-ttu-id="4c4d3-148">Dans cet exemple, tous les 1 000 tuples.</span><span class="sxs-lookup"><span data-stu-id="4c4d3-148">In this example, every 1000 tuples.</span></span>
* <span data-ttu-id="4c4d3-149">`fileNameFormat`: Définit hello chemin d’accès et nom du modèle toouse lors de l’écriture de fichiers.</span><span class="sxs-lookup"><span data-stu-id="4c4d3-149">`fileNameFormat`: Defines hello path and file name pattern toouse when writing files.</span></span> <span data-ttu-id="4c4d3-150">Dans cet exemple, le chemin d’accès hello est fourni lors de l’exécution à l’aide d’un filtre et l’extension de fichier hello est `.txt`.</span><span class="sxs-lookup"><span data-stu-id="4c4d3-150">In this example, hello path is provided at runtime using a filter, and hello file extension is `.txt`.</span></span>
* <span data-ttu-id="4c4d3-151">`recordFormat`: Définit le format interne de hello de fichiers hello écrits.</span><span class="sxs-lookup"><span data-stu-id="4c4d3-151">`recordFormat`: Defines hello internal format of hello files written.</span></span> <span data-ttu-id="4c4d3-152">Dans cet exemple, les champs sont délimités par hello `|` caractère.</span><span class="sxs-lookup"><span data-stu-id="4c4d3-152">In this example, fields are delimited by hello `|` character.</span></span>
* <span data-ttu-id="4c4d3-153">`rotationPolicy`: Définit quand les fichiers toorotate.</span><span class="sxs-lookup"><span data-stu-id="4c4d3-153">`rotationPolicy`: Defines when toorotate files.</span></span> <span data-ttu-id="4c4d3-154">Dans cet exemple, aucune rotation n’est effectuée.</span><span class="sxs-lookup"><span data-stu-id="4c4d3-154">In this example, no rotation is performed.</span></span>
* <span data-ttu-id="4c4d3-155">`hdfs-bolt`: Utilise hello composants précédentes en tant que paramètres de configuration pour hello `HdfsBolt` classe.</span><span class="sxs-lookup"><span data-stu-id="4c4d3-155">`hdfs-bolt`: Uses hello previous components as configuration parameters for hello `HdfsBolt` class.</span></span>

<span data-ttu-id="4c4d3-156">Pour plus d’informations sur l’infrastructure de Flux hello, consultez [https://storm.apache.org/releases/1.1.0/flux.html](https://storm.apache.org/releases/1.1.0/flux.html).</span><span class="sxs-lookup"><span data-stu-id="4c4d3-156">For more information on hello Flux framework, see [https://storm.apache.org/releases/1.1.0/flux.html](https://storm.apache.org/releases/1.1.0/flux.html).</span></span>

## <a name="configure-hello-cluster"></a><span data-ttu-id="4c4d3-157">Configurer le cluster de hello</span><span class="sxs-lookup"><span data-stu-id="4c4d3-157">Configure hello cluster</span></span>

<span data-ttu-id="4c4d3-158">Par défaut, Storm sur HDInsight n’inclut pas les composants hello que HdfsBolt utilise toocommunicate avec le stockage Azure ou Data Lake Store dans le chemin de classe de Storm.</span><span class="sxs-lookup"><span data-stu-id="4c4d3-158">By default, Storm on HDInsight does not include hello components that HdfsBolt uses toocommunicate with Azure Storage or Data Lake Store in Storm's classpath.</span></span> <span data-ttu-id="4c4d3-159">Le script suivant de hello d’utilisation action tooadd toohello de ces composants `extlib` répertoire de Storm sur votre cluster :</span><span class="sxs-lookup"><span data-stu-id="4c4d3-159">Use hello following script action tooadd these components toohello `extlib` directory for Storm on your cluster:</span></span>

<span data-ttu-id="4c4d3-160">| URI de script | Nœuds tooapply à | Paramètres || `https://000aarperiscus.blob.core.windows.net/certs/stormextlib.sh` | Nimbus, superviseur | None |</span><span class="sxs-lookup"><span data-stu-id="4c4d3-160">| Script URI | Nodes tooapply it to| Parameters | | `https://000aarperiscus.blob.core.windows.net/certs/stormextlib.sh` | Nimbus, Supervisor | None |</span></span>

<span data-ttu-id="4c4d3-161">Pour plus d’informations sur l’utilisation de ce script avec votre cluster, consultez hello [HDInsight de personnaliser des clusters à l’aide des actions de script](./hdinsight-hadoop-customize-cluster-linux.md) document.</span><span class="sxs-lookup"><span data-stu-id="4c4d3-161">For information on using this script with your cluster, see hello [Customize HDInsight clusters using script actions](./hdinsight-hadoop-customize-cluster-linux.md) document.</span></span>

## <a name="build-and-package-hello-topology"></a><span data-ttu-id="4c4d3-162">Générez et Empaquetez la topologie de hello</span><span class="sxs-lookup"><span data-stu-id="4c4d3-162">Build and package hello topology</span></span>

1. <span data-ttu-id="4c4d3-163">Télécharger le projet d’exemple hello à partir de [https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store ](https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store) tooyour les environnement de développement.</span><span class="sxs-lookup"><span data-stu-id="4c4d3-163">Download hello example project from [https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store ](https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store) tooyour development environment.</span></span>

2. <span data-ttu-id="4c4d3-164">À partir d’une invite de commandes, Terminal Server ou la session d’interpréteur de commandes, modification de répertoires toohello racine hello téléchargé le projet.</span><span class="sxs-lookup"><span data-stu-id="4c4d3-164">From a command prompt, terminal, or shell session, change directories toohello root of hello downloaded project.</span></span> <span data-ttu-id="4c4d3-165">toobuild et package hello topologie, utiliser hello commande suivante :</span><span class="sxs-lookup"><span data-stu-id="4c4d3-165">toobuild and package hello topology, use hello following command:</span></span>
   
        mvn compile package
   
    <span data-ttu-id="4c4d3-166">Une fois la génération de hello et l’empaquetage terminée, il existe un nouveau répertoire nommé `target`, qui contient un fichier nommé `StormToHdfs-1.0-SNAPSHOT.jar`.</span><span class="sxs-lookup"><span data-stu-id="4c4d3-166">Once hello build and packaging completes, there is a new directory named `target`, that contains a file named `StormToHdfs-1.0-SNAPSHOT.jar`.</span></span> <span data-ttu-id="4c4d3-167">Ce fichier contient la topologie de hello compilé.</span><span class="sxs-lookup"><span data-stu-id="4c4d3-167">This file contains hello compiled topology.</span></span>

## <a name="deploy-and-run-hello-topology"></a><span data-ttu-id="4c4d3-168">Déployer et exécuter la topologie de hello</span><span class="sxs-lookup"><span data-stu-id="4c4d3-168">Deploy and run hello topology</span></span>

1. <span data-ttu-id="4c4d3-169">Utilisez hello suivant du cluster HDInsight de commande toocopy hello topologie toohello.</span><span class="sxs-lookup"><span data-stu-id="4c4d3-169">Use hello following command toocopy hello topology toohello HDInsight cluster.</span></span> <span data-ttu-id="4c4d3-170">Remplacez **utilisateur** avec le nom d’utilisateur SSH hello que vous avez utilisé lors de la création du cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="4c4d3-170">Replace **USER** with hello SSH user name you used when creating hello cluster.</span></span> <span data-ttu-id="4c4d3-171">Remplacez **CLUSTERNAME** avec nom hello du cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="4c4d3-171">Replace **CLUSTERNAME** with hello name of hello cluster.</span></span>
   
        scp target\StormToHdfs-1.0-SNAPSHOT.jar USER@CLUSTERNAME-ssh.azurehdinsight.net:StormToHdfs1.0-SNAPSHOT.jar
   
    <span data-ttu-id="4c4d3-172">Lorsque vous y êtes invité, spécifiez hello mot de passe lors de la création d’utilisateur SSH hello pour le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="4c4d3-172">When prompted, enter hello password used when creating hello SSH user for hello cluster.</span></span> <span data-ttu-id="4c4d3-173">Si vous avez utilisé une clé publique au lieu d’un mot de passe, vous devrez peut-être toouse hello `-i` paramètre toospecify hello chemin d’accès toohello correspondant à une clé privée.</span><span class="sxs-lookup"><span data-stu-id="4c4d3-173">If you used a public key instead of a password, you may need toouse hello `-i` parameter toospecify hello path toohello matching private key.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="4c4d3-174">Pour en savoir plus sur l’utilisation de `scp` avec HDInsight, voir [Utiliser SSH avec Hadoop - Azure HDInsight](./hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="4c4d3-174">For more information on using `scp` with HDInsight, see [Use SSH with HDInsight](./hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="4c4d3-175">Une fois le téléchargement de hello terminé, utilisez hello suivant tooconnect toohello HDInsight cluster à l’aide de SSH.</span><span class="sxs-lookup"><span data-stu-id="4c4d3-175">Once hello upload completes, use hello following tooconnect toohello HDInsight cluster using SSH.</span></span> <span data-ttu-id="4c4d3-176">Remplacez **utilisateur** avec le nom d’utilisateur SSH hello que vous avez utilisé lors de la création du cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="4c4d3-176">Replace **USER** with hello SSH user name you used when creating hello cluster.</span></span> <span data-ttu-id="4c4d3-177">Remplacez **CLUSTERNAME** avec nom hello du cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="4c4d3-177">Replace **CLUSTERNAME** with hello name of hello cluster.</span></span>
   
        ssh USER@CLUSTERNAME-ssh.azurehdinsight.net
   
    <span data-ttu-id="4c4d3-178">Lorsque vous y êtes invité, spécifiez hello mot de passe lors de la création d’utilisateur SSH hello pour le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="4c4d3-178">When prompted, enter hello password used when creating hello SSH user for hello cluster.</span></span> <span data-ttu-id="4c4d3-179">Si vous avez utilisé une clé publique au lieu d’un mot de passe, vous devrez peut-être toouse hello `-i` paramètre toospecify hello chemin d’accès toohello correspondant à une clé privée.</span><span class="sxs-lookup"><span data-stu-id="4c4d3-179">If you used a public key instead of a password, you may need toouse hello `-i` parameter toospecify hello path toohello matching private key.</span></span>
   
   <span data-ttu-id="4c4d3-180">Pour en savoir plus, voir [Utilisation de SSH avec Hadoop Linux sur HDInsight depuis Linux, Unix ou OS X](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="4c4d3-180">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

3. <span data-ttu-id="4c4d3-181">Une fois connecté, utilisez hello commande suivante toocreate un fichier nommé `dev.properties`:</span><span class="sxs-lookup"><span data-stu-id="4c4d3-181">Once connected, use hello following command toocreate a file named `dev.properties`:</span></span>

        nano dev.properties

4. <span data-ttu-id="4c4d3-182">Hello utilisation après le texte en tant que contenu hello Hello `dev.properties` fichier :</span><span class="sxs-lookup"><span data-stu-id="4c4d3-182">Use hello following text as hello contents of hello `dev.properties` file:</span></span>

        hdfs.write.dir: /stormdata/
        hdfs.url: wasb:///

    > [!IMPORTANT]
    > <span data-ttu-id="4c4d3-183">Cet exemple suppose que votre cluster utilise un compte de stockage Azure en tant que stockage par défaut de hello.</span><span class="sxs-lookup"><span data-stu-id="4c4d3-183">This example assumes that your cluster uses an Azure Storage account as hello default storage.</span></span> <span data-ttu-id="4c4d3-184">Si votre cluster utilise Azure Data Lake Store, utilisez `hdfs.url: adl:///` à la place.</span><span class="sxs-lookup"><span data-stu-id="4c4d3-184">If your cluster uses Azure Data Lake Store, use `hdfs.url: adl:///` instead.</span></span>
    
    <span data-ttu-id="4c4d3-185">fichier de hello toosave, utilisez __Ctrl + X__, puis __Y__et enfin __entrée__.</span><span class="sxs-lookup"><span data-stu-id="4c4d3-185">toosave hello file, use __Ctrl + X__, then __Y__, and finally __Enter__.</span></span> <span data-ttu-id="4c4d3-186">Hello dans ce fichier valeur hello Data Lake store URL et le nom du répertoire hello que les données sont écrites dans.</span><span class="sxs-lookup"><span data-stu-id="4c4d3-186">hello values in this file set hello Data Lake store URL and hello directory name that data is written to.</span></span>

3. <span data-ttu-id="4c4d3-187">Utilisez hello suivant la topologie de commande toostart hello :</span><span class="sxs-lookup"><span data-stu-id="4c4d3-187">Use hello following command toostart hello topology:</span></span>
   
        storm jar StormToHdfs-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /writetohdfs.yaml --filter dev.properties

    <span data-ttu-id="4c4d3-188">Cette commande démarre la topologie hello à l’aide du framework de Flux hello en le soumettant à nœud de Nimbus toohello du cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="4c4d3-188">This command starts hello topology using hello Flux framework by submitting it toohello Nimbus node of hello cluster.</span></span> <span data-ttu-id="4c4d3-189">topologie de Hello est définie par hello `writetohdfs.yaml` fichier inclus dans le fichier jar de hello.</span><span class="sxs-lookup"><span data-stu-id="4c4d3-189">hello topology is defined by hello `writetohdfs.yaml` file included in hello jar.</span></span> <span data-ttu-id="4c4d3-190">Hello `dev.properties` fichier est passé en tant que filtre et les valeurs hello contenues dans le fichier de hello sont lues par la topologie de hello.</span><span class="sxs-lookup"><span data-stu-id="4c4d3-190">hello `dev.properties` file is passed as a filter, and hello values contained in hello file are read by hello topology.</span></span>

## <a name="view-output-data"></a><span data-ttu-id="4c4d3-191">Affichage des données de sortie</span><span class="sxs-lookup"><span data-stu-id="4c4d3-191">View output data</span></span>

<span data-ttu-id="4c4d3-192">les données de salutation tooview, utilisez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="4c4d3-192">tooview hello data, use hello following command:</span></span>

    hdfs dfs -ls /stormdata/

<span data-ttu-id="4c4d3-193">Une liste de fichiers hello créés par cette topologie s’affiche.</span><span class="sxs-lookup"><span data-stu-id="4c4d3-193">A list of hello files created by this topology is displayed.</span></span>

<span data-ttu-id="4c4d3-194">Hello liste suivante est un exemple de données hello retournées par les commandes précédentes hello :</span><span class="sxs-lookup"><span data-stu-id="4c4d3-194">hello following list is an example of hello data retuned by hello previous commands:</span></span>

    Found 30 items
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-0-1488568403092.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-1-1488568404567.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-10-1488568408678.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-11-1488568411636.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-12-1488568411884.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-13-1488568412603.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-14-1488568415055.txt

## <a name="stop-hello-topology"></a><span data-ttu-id="4c4d3-195">Arrêter la topologie de hello</span><span class="sxs-lookup"><span data-stu-id="4c4d3-195">Stop hello topology</span></span>

<span data-ttu-id="4c4d3-196">Les topologies Storm exécuter jusqu'à l’arrêt, ou cluster de hello est supprimé.</span><span class="sxs-lookup"><span data-stu-id="4c4d3-196">Storm topologies run until stopped, or hello cluster is deleted.</span></span> <span data-ttu-id="4c4d3-197">toostop hello topologie, utilisez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="4c4d3-197">toostop hello topology, use hello following command:</span></span>

    storm kill hdfswriter

## <a name="delete-your-cluster"></a><span data-ttu-id="4c4d3-198">Supprimer votre cluster</span><span class="sxs-lookup"><span data-stu-id="4c4d3-198">Delete your cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a><span data-ttu-id="4c4d3-199">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4c4d3-199">Next steps</span></span>

<span data-ttu-id="4c4d3-200">Maintenant que vous avez appris comment toouse Storm toowrite tooAzure stockage et Azure Data Lake Store, découvrir les autres [renverser exemples pour HDInsight](hdinsight-storm-example-topology.md).</span><span class="sxs-lookup"><span data-stu-id="4c4d3-200">Now that you have learned how toouse Storm toowrite tooAzure Storage and Azure Data Lake Store, discover other [Storm examples for HDInsight](hdinsight-storm-example-topology.md).</span></span>

