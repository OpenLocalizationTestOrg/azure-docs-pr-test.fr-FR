---
title: "Écriture Apache Storm dans le stockage/Data Lake Store - Azure HDInsight | Microsoft Docs"
description: "Découvrez comment utiliser Apache Storm pour écrire dans le stockage compatible HDFS pour HDInsight. Le stockage Azure ou Azure Data Lake Store fournissent un stockage compatible HDFS pour HDInsight. Ce document et l’exemple associé illustrent la manière dont le composant HdfsBolt peut être utilisé pour écrire dans le stockage par défaut d’un cluster Storm dans un cluster HDInsight."
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
ms.openlocfilehash: 10dc8789e8f4a2b27fd3a4c6fec2ab28c674170a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="write-to-hdfs-from-apache-storm-on-hdinsight"></a><span data-ttu-id="34def-105">Écrire dans un stockage HDFS à partir d’Apache Storm sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="34def-105">Write to HDFS from Apache Storm on HDInsight</span></span>

<span data-ttu-id="34def-106">Découvrez comment utiliser Storm pour écrire des données dans le stockage compatible HDFS utilisé par Apache Storm sur HDInsight.</span><span class="sxs-lookup"><span data-stu-id="34def-106">Learn how to use Storm to write data to the HDFS-compatible storage used by Apache Storm on HDInsight.</span></span> <span data-ttu-id="34def-107">HDInsight peut utiliser à la fois le stockage Azure et Azure Data Lake comme stockage compatible HDFS.</span><span class="sxs-lookup"><span data-stu-id="34def-107">HDInsight can use both Azure Storage and Azure Data Lake store as HDFS-comptabile storage.</span></span> <span data-ttu-id="34def-108">Storm fournit un composant [HdfsBolt](http://storm.apache.org/releases/1.1.0/javadocs/org/apache/storm/hdfs/bolt/HdfsBolt.html) qui écrit des données dans le stockage HDFS.</span><span class="sxs-lookup"><span data-stu-id="34def-108">Storm provides an [HdfsBolt](http://storm.apache.org/releases/1.1.0/javadocs/org/apache/storm/hdfs/bolt/HdfsBolt.html) component that writes data to HDFS.</span></span> <span data-ttu-id="34def-109">Ce document fournit des informations sur l’écriture dans ces deux types de stockages à partir du composant HdfsBolt.</span><span class="sxs-lookup"><span data-stu-id="34def-109">This document provides information on writing to either type of storage from the HdfsBolt.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="34def-110">L’exemple de topologie utilisé dans ce document s’appuie sur les composants inclus avec Storm sur HDInsight.</span><span class="sxs-lookup"><span data-stu-id="34def-110">The example topology used in this document relies on components that are included with Storm on HDInsight.</span></span> <span data-ttu-id="34def-111">Il faudra peut-être le modifier pour qu’il fonctionne avec Azure Data Lake Store en cas d’utilisation avec d’autres clusters Apache Storm.</span><span class="sxs-lookup"><span data-stu-id="34def-111">It may require modification to work with Azure Data Lake Store when used with other Apache Storm clusters.</span></span>

## <a name="get-the-code"></a><span data-ttu-id="34def-112">Obtenir le code</span><span class="sxs-lookup"><span data-stu-id="34def-112">Get the code</span></span>

<span data-ttu-id="34def-113">Le projet contenant cette topologie est disponible en téléchargement à partir de [https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store](https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store).</span><span class="sxs-lookup"><span data-stu-id="34def-113">The project containing this topology is available as a download from [https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store](https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store).</span></span>

<span data-ttu-id="34def-114">Pour compiler ce projet, utilisez la configuration suivante dans votre environnement de développement :</span><span class="sxs-lookup"><span data-stu-id="34def-114">To compile this project, you need the following configuration for your development environment:</span></span>

* <span data-ttu-id="34def-115">[Java JDK 1.8](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="34def-115">[Java JDK 1.8](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) or higher.</span></span> <span data-ttu-id="34def-116">HDInsight 3.5 ou les versions ultérieures requièrent Java 8.</span><span class="sxs-lookup"><span data-stu-id="34def-116">HDInsight 3.5 or higher require Java 8.</span></span>

* [<span data-ttu-id="34def-117">Maven 3.x</span><span class="sxs-lookup"><span data-stu-id="34def-117">Maven 3.x</span></span>](https://maven.apache.org/download.cgi)

<span data-ttu-id="34def-118">Les variables d’environnement suivantes peuvent être définies lors de l’installation de Java et du Kit de développeur Java (JDK) sur votre station de travail de développement.</span><span class="sxs-lookup"><span data-stu-id="34def-118">The following environment variables may be set when you install Java and the JDK on your development workstation.</span></span> <span data-ttu-id="34def-119">Toutefois, vous devez vérifier qu’elles existent et qu’elles contiennent les valeurs correctes pour votre système.</span><span class="sxs-lookup"><span data-stu-id="34def-119">However, you should check that they exist and that they contain the correct values for your system.</span></span>

* <span data-ttu-id="34def-120">`JAVA_HOME` : doit pointer vers le répertoire d’installation du Kit de développeur Java (JDK).</span><span class="sxs-lookup"><span data-stu-id="34def-120">`JAVA_HOME` - should point to the directory where the JDK is installed.</span></span>
* <span data-ttu-id="34def-121">`PATH` : doit contenir les chemins d’accès suivants :</span><span class="sxs-lookup"><span data-stu-id="34def-121">`PATH` - should contain the following paths:</span></span>
  
    * <span data-ttu-id="34def-122">`JAVA_HOME` (ou le chemin équivalent).</span><span class="sxs-lookup"><span data-stu-id="34def-122">`JAVA_HOME` (or the equivalent path).</span></span>
    * <span data-ttu-id="34def-123">`JAVA_HOME\bin` (ou le chemin équivalent).</span><span class="sxs-lookup"><span data-stu-id="34def-123">`JAVA_HOME\bin` (or the equivalent path).</span></span>
    * <span data-ttu-id="34def-124">Le répertoire d’installation de Maven.</span><span class="sxs-lookup"><span data-stu-id="34def-124">The directory where Maven is installed.</span></span>

## <a name="how-to-use-the-hdfsbolt-with-hdinsight"></a><span data-ttu-id="34def-125">Comment utiliser le composant HdfsBolt avec HDInsight</span><span class="sxs-lookup"><span data-stu-id="34def-125">How to use the HdfsBolt with HDInsight</span></span>

> [!IMPORTANT]
> <span data-ttu-id="34def-126">Avant de vous servir du composant HdfsBolt avec Storm sur HDInsight, vous devez utiliser une action de script pour copier les fichiers jar requis à l’emplacement `extpath` de Storm.</span><span class="sxs-lookup"><span data-stu-id="34def-126">Before using the HdfsBolt with Storm on HDInsight, you must first use a script action to copy required jar files into the `extpath` for Storm.</span></span> <span data-ttu-id="34def-127">Pour plus d’informations, consultez la section [Configurer le cluster](#configure).</span><span class="sxs-lookup"><span data-stu-id="34def-127">For more information, see the [Configure the cluster](#configure) section.</span></span>

<span data-ttu-id="34def-128">Le composant HdfsBolt utilise le schéma de fichier que vous fournissez pour savoir comment écrire dans le stockage HDFS.</span><span class="sxs-lookup"><span data-stu-id="34def-128">The HdfsBolt uses the file scheme that you provide to understand how to write to HDFS.</span></span> <span data-ttu-id="34def-129">Avec HDInsight, utilisez l’un des schémas suivants :</span><span class="sxs-lookup"><span data-stu-id="34def-129">With HDInsight, use one of the following schemes:</span></span>

* <span data-ttu-id="34def-130">`wasb://` : avec un compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="34def-130">`wasb://`: Used with an Azure Storage account.</span></span>
* <span data-ttu-id="34def-131">`adl://` : avec Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="34def-131">`adl://`: Used with Azure Data Lake Store.</span></span>

<span data-ttu-id="34def-132">Le tableau suivant fournit des exemples d’utilisation du schéma de fichier dans différents scénarios :</span><span class="sxs-lookup"><span data-stu-id="34def-132">The following table provides examples of using the file scheme for different scenarios:</span></span>

| <span data-ttu-id="34def-133">Schéma</span><span class="sxs-lookup"><span data-stu-id="34def-133">Scheme</span></span> | <span data-ttu-id="34def-134">Remarques</span><span class="sxs-lookup"><span data-stu-id="34def-134">Notes</span></span> |
| ----- | ----- |
| `wasb:///` | <span data-ttu-id="34def-135">Le compte de stockage par défaut est un conteneur d’objets blob dans un compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="34def-135">The default storage account is a blob container in an Azure Storage account</span></span> |
| `adl:///` | <span data-ttu-id="34def-136">Le compte de stockage par défaut est un répertoire dans Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="34def-136">The default storage account is a directory in Azure Data Lake Store.</span></span> <span data-ttu-id="34def-137">Lors de la création du cluster, vous spécifiez le répertoire Data Lake Store qui sera la racine du stockage HDFS du cluster.</span><span class="sxs-lookup"><span data-stu-id="34def-137">During cluster creation, you specify the directory in Data Lake Store that is the root of the cluster's HDFS.</span></span> <span data-ttu-id="34def-138">Par exemple, le répertoire `/clusters/myclustername/`.</span><span class="sxs-lookup"><span data-stu-id="34def-138">For example, the `/clusters/myclustername/` directory.</span></span> |
| `wasb://CONTAINER@ACCOUNT.blob.core.windows.net/` | <span data-ttu-id="34def-139">Un compte de stockage Azure différent du compte par défaut (compte supplémentaire) associé au cluster.</span><span class="sxs-lookup"><span data-stu-id="34def-139">A non-default (additional) Azure storage account associated with the cluster.</span></span> |
| `adl://STORENAME/` | <span data-ttu-id="34def-140">La racine du compte Data Lake Store utilisé par le cluster.</span><span class="sxs-lookup"><span data-stu-id="34def-140">The root of the Data Lake Store used by the cluster.</span></span> <span data-ttu-id="34def-141">Ce schéma vous permet d’accéder aux données qui se trouvent en dehors du répertoire qui contient le système de fichiers du cluster.</span><span class="sxs-lookup"><span data-stu-id="34def-141">This scheme allows you to access data that is located outside the directory that contains the cluster file system.</span></span> |

<span data-ttu-id="34def-142">Pour plus d’informations, consultez la documentation de référence [HdfsBolt](http://storm.apache.org/releases/1.1.0/javadocs/org/apache/storm/hdfs/bolt/HdfsBolt.html) sur le site Apache.org.</span><span class="sxs-lookup"><span data-stu-id="34def-142">For more information, see the [HdfsBolt](http://storm.apache.org/releases/1.1.0/javadocs/org/apache/storm/hdfs/bolt/HdfsBolt.html) reference at Apache.org.</span></span>

### <a name="example-configuration"></a><span data-ttu-id="34def-143">Exemple de configuration</span><span class="sxs-lookup"><span data-stu-id="34def-143">Example configuration</span></span>

<span data-ttu-id="34def-144">Le code YAML suivant est un extrait du fichier `resources/writetohdfs.yaml` inclus dans cet exemple.</span><span class="sxs-lookup"><span data-stu-id="34def-144">The following YAML is an excerpt from the `resources/writetohdfs.yaml` file included in the example.</span></span> <span data-ttu-id="34def-145">Ce fichier définit la topologie de Storm à l’aide du framework [Flux](https://storm.apache.org/releases/1.1.0/flux.html) pour Apache Storm.</span><span class="sxs-lookup"><span data-stu-id="34def-145">This file defines the Storm topology using the [Flux](https://storm.apache.org/releases/1.1.0/flux.html) framework for Apache Storm.</span></span>

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

<span data-ttu-id="34def-146">Ce code YAML définit les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="34def-146">This YAML defines the following items:</span></span>

* <span data-ttu-id="34def-147">`syncPolicy` : définit quand les fichiers sont synchronisés/vidés sur le système de fichiers.</span><span class="sxs-lookup"><span data-stu-id="34def-147">`syncPolicy`: Defines when files are synched/flushed to the file system.</span></span> <span data-ttu-id="34def-148">Dans cet exemple, tous les 1 000 tuples.</span><span class="sxs-lookup"><span data-stu-id="34def-148">In this example, every 1000 tuples.</span></span>
* <span data-ttu-id="34def-149">`fileNameFormat` : définit le modèle de chemin d’accès et de nom de fichier à utiliser lors de l’écriture de fichiers.</span><span class="sxs-lookup"><span data-stu-id="34def-149">`fileNameFormat`: Defines the path and file name pattern to use when writing files.</span></span> <span data-ttu-id="34def-150">Dans cet exemple, le chemin d’accès est fourni au moment de l’exécution à l’aide d’un filtre, avec l’extension de fichier `.txt`.</span><span class="sxs-lookup"><span data-stu-id="34def-150">In this example, the path is provided at runtime using a filter, and the file extension is `.txt`.</span></span>
* <span data-ttu-id="34def-151">`recordFormat` : définit le format interne des fichiers écrits.</span><span class="sxs-lookup"><span data-stu-id="34def-151">`recordFormat`: Defines the internal format of the files written.</span></span> <span data-ttu-id="34def-152">Dans cet exemple, les champs sont délimités par le caractère `|`.</span><span class="sxs-lookup"><span data-stu-id="34def-152">In this example, fields are delimited by the `|` character.</span></span>
* <span data-ttu-id="34def-153">`rotationPolicy` : définit le moment de rotation des fichiers.</span><span class="sxs-lookup"><span data-stu-id="34def-153">`rotationPolicy`: Defines when to rotate files.</span></span> <span data-ttu-id="34def-154">Dans cet exemple, aucune rotation n’est effectuée.</span><span class="sxs-lookup"><span data-stu-id="34def-154">In this example, no rotation is performed.</span></span>
* <span data-ttu-id="34def-155">`hdfs-bolt` : utilise les composants précédents comme paramètres de configuration pour la classe `HdfsBolt`.</span><span class="sxs-lookup"><span data-stu-id="34def-155">`hdfs-bolt`: Uses the previous components as configuration parameters for the `HdfsBolt` class.</span></span>

<span data-ttu-id="34def-156">Pour plus d’informations sur le framework Flux, consultez la page [https://storm.apache.org/releases/1.1.0/flux.html](https://storm.apache.org/releases/1.1.0/flux.html).</span><span class="sxs-lookup"><span data-stu-id="34def-156">For more information on the Flux framework, see [https://storm.apache.org/releases/1.1.0/flux.html](https://storm.apache.org/releases/1.1.0/flux.html).</span></span>

## <a name="configure-the-cluster"></a><span data-ttu-id="34def-157">Configurer le cluster</span><span class="sxs-lookup"><span data-stu-id="34def-157">Configure the cluster</span></span>

<span data-ttu-id="34def-158">Par défaut, Storm sur HDInsight n’inclut pas les composants utilisés par HdfsBolt pour communiquer avec le stockage Azure ou Data Lake Store dans le chemin de classe du cluster Storm.</span><span class="sxs-lookup"><span data-stu-id="34def-158">By default, Storm on HDInsight does not include the components that HdfsBolt uses to communicate with Azure Storage or Data Lake Store in Storm's classpath.</span></span> <span data-ttu-id="34def-159">Utilisez l’action de script suivante pour ajouter ces composants au répertoire `extlib` de Storm sur votre cluster :</span><span class="sxs-lookup"><span data-stu-id="34def-159">Use the following script action to add these components to the `extlib` directory for Storm on your cluster:</span></span>

<span data-ttu-id="34def-160">| URI du script | Nœuds sur lesquels l’appliquer | Paramètres | | `https://000aarperiscus.blob.core.windows.net/certs/stormextlib.sh` | Nimbus, Supervisor | None |</span><span class="sxs-lookup"><span data-stu-id="34def-160">| Script URI | Nodes to apply it to| Parameters | | `https://000aarperiscus.blob.core.windows.net/certs/stormextlib.sh` | Nimbus, Supervisor | None |</span></span>

<span data-ttu-id="34def-161">Pour plus d’informations sur l’utilisation de ce script avec votre cluster, consultez le document [Personnalisation de clusters HDInsight basés sur Linux à l’aide d'une action de script](./hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="34def-161">For information on using this script with your cluster, see the [Customize HDInsight clusters using script actions](./hdinsight-hadoop-customize-cluster-linux.md) document.</span></span>

## <a name="build-and-package-the-topology"></a><span data-ttu-id="34def-162">Génération et empaquetage de la topologie</span><span class="sxs-lookup"><span data-stu-id="34def-162">Build and package the topology</span></span>

1. <span data-ttu-id="34def-163">Téléchargez l’exemple de projet à partir de [https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store ](https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store) dans votre environnement de développement.</span><span class="sxs-lookup"><span data-stu-id="34def-163">Download the example project from [https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store ](https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store) to your development environment.</span></span>

2. <span data-ttu-id="34def-164">À partir d’une invite de commandes, d’un terminal ou d’une session shell, modifiez les répertoires à la racine du projet téléchargé.</span><span class="sxs-lookup"><span data-stu-id="34def-164">From a command prompt, terminal, or shell session, change directories to the root of the downloaded project.</span></span> <span data-ttu-id="34def-165">Pour générer et empaqueter la topologie, utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="34def-165">To build and package the topology, use the following command:</span></span>
   
        mvn compile package
   
    <span data-ttu-id="34def-166">Une fois la génération et l’empaquetage terminés, vous obtenez un répertoire nommé `target`, qui contient un fichier `StormToHdfs-1.0-SNAPSHOT.jar`.</span><span class="sxs-lookup"><span data-stu-id="34def-166">Once the build and packaging completes, there is a new directory named `target`, that contains a file named `StormToHdfs-1.0-SNAPSHOT.jar`.</span></span> <span data-ttu-id="34def-167">Ce fichier contient la topologie compilée.</span><span class="sxs-lookup"><span data-stu-id="34def-167">This file contains the compiled topology.</span></span>

## <a name="deploy-and-run-the-topology"></a><span data-ttu-id="34def-168">Déployer et exécuter la topologie</span><span class="sxs-lookup"><span data-stu-id="34def-168">Deploy and run the topology</span></span>

1. <span data-ttu-id="34def-169">Utilisez la commande suivante pour copier la topologie sur le cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="34def-169">Use the following command to copy the topology to the HDInsight cluster.</span></span> <span data-ttu-id="34def-170">Remplacez **USER** par le nom d’utilisateur SSH que vous avez utilisé lors de la création du cluster.</span><span class="sxs-lookup"><span data-stu-id="34def-170">Replace **USER** with the SSH user name you used when creating the cluster.</span></span> <span data-ttu-id="34def-171">Remplacez **CLUSTERNAME** par le nom de votre cluster.</span><span class="sxs-lookup"><span data-stu-id="34def-171">Replace **CLUSTERNAME** with the name of the cluster.</span></span>
   
        scp target\StormToHdfs-1.0-SNAPSHOT.jar USER@CLUSTERNAME-ssh.azurehdinsight.net:StormToHdfs1.0-SNAPSHOT.jar
   
    <span data-ttu-id="34def-172">À l’invite, saisissez le mot de passe que vous avez utilisé lors de la création de l’utilisateur SSH du cluster.</span><span class="sxs-lookup"><span data-stu-id="34def-172">When prompted, enter the password used when creating the SSH user for the cluster.</span></span> <span data-ttu-id="34def-173">Si vous utilisez une clé publique au lieu d’un mot de passe, vous devrez peut-être utiliser le paramètre `-i` pour spécifier le chemin d’accès à la clé privée correspondante.</span><span class="sxs-lookup"><span data-stu-id="34def-173">If you used a public key instead of a password, you may need to use the `-i` parameter to specify the path to the matching private key.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="34def-174">Pour en savoir plus sur l’utilisation de `scp` avec HDInsight, voir [Utiliser SSH avec Hadoop - Azure HDInsight](./hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="34def-174">For more information on using `scp` with HDInsight, see [Use SSH with HDInsight](./hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="34def-175">Une fois le téléchargement terminé, utilisez les éléments suivants pour vous connecter au cluster HDInsight à l’aide de SSH.</span><span class="sxs-lookup"><span data-stu-id="34def-175">Once the upload completes, use the following to connect to the HDInsight cluster using SSH.</span></span> <span data-ttu-id="34def-176">Remplacez **USER** par le nom d’utilisateur SSH que vous avez utilisé lors de la création du cluster.</span><span class="sxs-lookup"><span data-stu-id="34def-176">Replace **USER** with the SSH user name you used when creating the cluster.</span></span> <span data-ttu-id="34def-177">Remplacez **CLUSTERNAME** par le nom de votre cluster.</span><span class="sxs-lookup"><span data-stu-id="34def-177">Replace **CLUSTERNAME** with the name of the cluster.</span></span>
   
        ssh USER@CLUSTERNAME-ssh.azurehdinsight.net
   
    <span data-ttu-id="34def-178">À l’invite, saisissez le mot de passe que vous avez utilisé lors de la création de l’utilisateur SSH du cluster.</span><span class="sxs-lookup"><span data-stu-id="34def-178">When prompted, enter the password used when creating the SSH user for the cluster.</span></span> <span data-ttu-id="34def-179">Si vous utilisez une clé publique au lieu d’un mot de passe, vous devrez peut-être utiliser le paramètre `-i` pour spécifier le chemin d’accès à la clé privée correspondante.</span><span class="sxs-lookup"><span data-stu-id="34def-179">If you used a public key instead of a password, you may need to use the `-i` parameter to specify the path to the matching private key.</span></span>
   
   <span data-ttu-id="34def-180">Pour en savoir plus, voir [Utilisation de SSH avec Hadoop Linux sur HDInsight depuis Linux, Unix ou OS X](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="34def-180">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

3. <span data-ttu-id="34def-181">Une fois connecté, utilisez la commande suivante pour créer un fichier nommé `dev.properties` :</span><span class="sxs-lookup"><span data-stu-id="34def-181">Once connected, use the following command to create a file named `dev.properties`:</span></span>

        nano dev.properties

4. <span data-ttu-id="34def-182">Utilisez les données suivantes comme contenu du fichier `dev.properties` :</span><span class="sxs-lookup"><span data-stu-id="34def-182">Use the following text as the contents of the `dev.properties` file:</span></span>

        hdfs.write.dir: /stormdata/
        hdfs.url: wasb:///

    > [!IMPORTANT]
    > <span data-ttu-id="34def-183">Cet exemple suppose que votre cluster utilise un compte de stockage Azure pour le stockage par défaut.</span><span class="sxs-lookup"><span data-stu-id="34def-183">This example assumes that your cluster uses an Azure Storage account as the default storage.</span></span> <span data-ttu-id="34def-184">Si votre cluster utilise Azure Data Lake Store, utilisez `hdfs.url: adl:///` à la place.</span><span class="sxs-lookup"><span data-stu-id="34def-184">If your cluster uses Azure Data Lake Store, use `hdfs.url: adl:///` instead.</span></span>
    
    <span data-ttu-id="34def-185">Pour enregistrer le fichier, use __Ctrl + X__, puis __Y__, et enfin __Entrée__.</span><span class="sxs-lookup"><span data-stu-id="34def-185">To save the file, use __Ctrl + X__, then __Y__, and finally __Enter__.</span></span> <span data-ttu-id="34def-186">Les valeurs dans ce fichier définissent l’URL de Data Lake Store et le nom du répertoire où sont écrites les données.</span><span class="sxs-lookup"><span data-stu-id="34def-186">The values in this file set the Data Lake store URL and the directory name that data is written to.</span></span>

3. <span data-ttu-id="34def-187">Utilisez la commande suivante pour démarrer la topologie :</span><span class="sxs-lookup"><span data-stu-id="34def-187">Use the following command to start the topology:</span></span>
   
        storm jar StormToHdfs-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /writetohdfs.yaml --filter dev.properties

    <span data-ttu-id="34def-188">Cette commande démarre la topologie à partir du framework Flux en le soumettant au nœud Nimbus du cluster.</span><span class="sxs-lookup"><span data-stu-id="34def-188">This command starts the topology using the Flux framework by submitting it to the Nimbus node of the cluster.</span></span> <span data-ttu-id="34def-189">La topologie est définie par le fichier `writetohdfs.yaml` inclus dans le fichier jar.</span><span class="sxs-lookup"><span data-stu-id="34def-189">The topology is defined by the `writetohdfs.yaml` file included in the jar.</span></span> <span data-ttu-id="34def-190">Le fichier `dev.properties` est transféré en tant que filtre et les valeurs qu’il contient sont lues par la topologie.</span><span class="sxs-lookup"><span data-stu-id="34def-190">The `dev.properties` file is passed as a filter, and the values contained in the file are read by the topology.</span></span>

## <a name="view-output-data"></a><span data-ttu-id="34def-191">Affichage des données de sortie</span><span class="sxs-lookup"><span data-stu-id="34def-191">View output data</span></span>

<span data-ttu-id="34def-192">Pour afficher les données, utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="34def-192">To view the data, use the following command:</span></span>

    hdfs dfs -ls /stormdata/

<span data-ttu-id="34def-193">Une liste des fichiers créés par cette topologie s’affiche.</span><span class="sxs-lookup"><span data-stu-id="34def-193">A list of the files created by this topology is displayed.</span></span>

<span data-ttu-id="34def-194">La liste suivante est un exemple des données retournées par les commandes précédentes :</span><span class="sxs-lookup"><span data-stu-id="34def-194">The following list is an example of the data retuned by the previous commands:</span></span>

    Found 30 items
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-0-1488568403092.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-1-1488568404567.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-10-1488568408678.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-11-1488568411636.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-12-1488568411884.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-13-1488568412603.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-14-1488568415055.txt

## <a name="stop-the-topology"></a><span data-ttu-id="34def-195">Arrêt de la topologie</span><span class="sxs-lookup"><span data-stu-id="34def-195">Stop the topology</span></span>

<span data-ttu-id="34def-196">Les topologies Storm s’exécutent jusqu’à ce qu’elles soient arrêtées ou que le cluster soit supprimé.</span><span class="sxs-lookup"><span data-stu-id="34def-196">Storm topologies run until stopped, or the cluster is deleted.</span></span> <span data-ttu-id="34def-197">Pour arrêter la topologie, utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="34def-197">To stop the topology, use the following command:</span></span>

    storm kill hdfswriter

## <a name="delete-your-cluster"></a><span data-ttu-id="34def-198">Supprimer votre cluster</span><span class="sxs-lookup"><span data-stu-id="34def-198">Delete your cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a><span data-ttu-id="34def-199">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="34def-199">Next steps</span></span>

<span data-ttu-id="34def-200">Maintenant que vous avez appris à utiliser Storm pour écrire dans le stockage Azure et Azure Data Lake Store, découvrez d’autres [exemples Storm pour HDInsight](hdinsight-storm-example-topology.md).</span><span class="sxs-lookup"><span data-stu-id="34def-200">Now that you have learned how to use Storm to write to Azure Storage and Azure Data Lake Store, discover other [Storm examples for HDInsight](hdinsight-storm-example-topology.md).</span></span>

