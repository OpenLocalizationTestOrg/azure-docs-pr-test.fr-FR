---
title: "Utilisation d’Apache Kafka avec Storm sur HDInsight - Azure | Microsoft Docs"
description: "Apache Kafka est installé avec Apache Storm sur HDInsight. Apprenez à écrire sur Kafka et lire à partir de celui-ci, et utiliser les composants KafkaBolt et KafkaSpout fournis avec Storm. Découvrez également comment utiliser l’infrastructure Flux pour définir et envoyer des topologies Storm."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: e4941329-1580-4cd8-b82e-a2258802c1a7
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/21/2017
ms.author: larryfr
ms.openlocfilehash: e8895ef3c11aea48513e4060a20f5f49b11fc961
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="use-apache-kafka-preview-with-storm-on-hdinsight"></a><span data-ttu-id="4c1a2-105">Utilisation d’Apache Kafka (version préliminaire) avec Storm sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="4c1a2-105">Use Apache Kafka (preview) with Storm on HDInsight</span></span>

<span data-ttu-id="4c1a2-106">Découvrez comment utiliser Apache Storm pour lire et écrire dans Apache Kafka.</span><span class="sxs-lookup"><span data-stu-id="4c1a2-106">Learn how to use Apache Storm to read from and write to Apache Kafka.</span></span> <span data-ttu-id="4c1a2-107">Cet exemple montre également comment enregistrer des données d’une topologie Storm dans un système de fichiers compatible HDFS utilisé par HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4c1a2-107">This example also demonstrates how to save data from a Storm topology to the HDFS-compatible file system used by HDInsight.</span></span>

> [!NOTE]
> <span data-ttu-id="4c1a2-108">Les étapes décrites dans ce document créent un groupe de ressources Azure qui contient à la fois un Storm sur HDInsight et un Kafka sur un cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4c1a2-108">The steps in this document create an Azure resource group that contains both a Storm on HDInsight and a Kafka on HDInsight cluster.</span></span> <span data-ttu-id="4c1a2-109">Ces clusters sont tous deux situés dans un réseau virtuel Azure, ce qui permet au cluster Storm de communiquer directement avec le cluster Kafka.</span><span class="sxs-lookup"><span data-stu-id="4c1a2-109">These clusters are both located within an Azure Virtual Network, which allows the Storm cluster to directly communicate with the Kafka cluster.</span></span>
> 
> <span data-ttu-id="4c1a2-110">Lorsque vous avez terminé les étapes décrites dans ce document, n’oubliez pas de supprimer les clusters pour éviter les frais supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="4c1a2-110">When you are done with the steps in this document, remember to delete the clusters to avoid excess charges.</span></span>

## <a name="get-the-code"></a><span data-ttu-id="4c1a2-111">Obtenir le code</span><span class="sxs-lookup"><span data-stu-id="4c1a2-111">Get the code</span></span>

<span data-ttu-id="4c1a2-112">Le code de l’exemple utilisé dans ce document est disponible à l’adresse [https://github.com/Azure-Samples/hdinsight-storm-java-kafka](https://github.com/Azure-Samples/hdinsight-storm-java-kafka).</span><span class="sxs-lookup"><span data-stu-id="4c1a2-112">The code for the example used in this document is available at [https://github.com/Azure-Samples/hdinsight-storm-java-kafka](https://github.com/Azure-Samples/hdinsight-storm-java-kafka).</span></span>

<span data-ttu-id="4c1a2-113">Pour compiler ce projet, la configuration de votre environnement de développement doit être la suivante :</span><span class="sxs-lookup"><span data-stu-id="4c1a2-113">To compile this project, you need the following configuration for your development environment:</span></span>

* <span data-ttu-id="4c1a2-114">[Java JDK 1.8](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="4c1a2-114">[Java JDK 1.8](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) or higher.</span></span> <span data-ttu-id="4c1a2-115">HDInsight 3.5 ou les versions ultérieures requièrent Java 8.</span><span class="sxs-lookup"><span data-stu-id="4c1a2-115">HDInsight 3.5 or higher require Java 8.</span></span>

* [<span data-ttu-id="4c1a2-116">Maven 3.x</span><span class="sxs-lookup"><span data-stu-id="4c1a2-116">Maven 3.x</span></span>](https://maven.apache.org/download.cgi)

* <span data-ttu-id="4c1a2-117">Un client SSH (vous avez besoin des commandes `ssh` et `scp`) : pour plus d’informations, voir [Utilisation de SSH avec HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="4c1a2-117">An SSH client (you need the `ssh` and `scp` commands) - For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

* <span data-ttu-id="4c1a2-118">Un éditeur de texte ou IDE.</span><span class="sxs-lookup"><span data-stu-id="4c1a2-118">A text editor or IDE.</span></span>

<span data-ttu-id="4c1a2-119">Les variables d’environnement suivantes peuvent être définies lors de l’installation de Java et du Kit de développeur Java (JDK) sur votre station de travail de développement.</span><span class="sxs-lookup"><span data-stu-id="4c1a2-119">The following environment variables may be set when you install Java and the JDK on your development workstation.</span></span> <span data-ttu-id="4c1a2-120">Toutefois, vous devez vérifier qu’elles existent et qu’elles contiennent les valeurs correctes pour votre système.</span><span class="sxs-lookup"><span data-stu-id="4c1a2-120">However, you should check that they exist and that they contain the correct values for your system.</span></span>

* <span data-ttu-id="4c1a2-121">`JAVA_HOME` : doit pointer vers le répertoire d’installation du Kit de développeur Java (JDK).</span><span class="sxs-lookup"><span data-stu-id="4c1a2-121">`JAVA_HOME` - should point to the directory where the JDK is installed.</span></span>
* <span data-ttu-id="4c1a2-122">`PATH` : doit contenir les chemins d’accès suivants :</span><span class="sxs-lookup"><span data-stu-id="4c1a2-122">`PATH` - should contain the following paths:</span></span>
  
    * <span data-ttu-id="4c1a2-123">`JAVA_HOME` (ou le chemin équivalent).</span><span class="sxs-lookup"><span data-stu-id="4c1a2-123">`JAVA_HOME` (or the equivalent path).</span></span>
    * <span data-ttu-id="4c1a2-124">`JAVA_HOME\bin` (ou le chemin équivalent).</span><span class="sxs-lookup"><span data-stu-id="4c1a2-124">`JAVA_HOME\bin` (or the equivalent path).</span></span>
    * <span data-ttu-id="4c1a2-125">Répertoire d’installation de Maven.</span><span class="sxs-lookup"><span data-stu-id="4c1a2-125">The directory where Maven is installed.</span></span>

## <a name="create-the-clusters"></a><span data-ttu-id="4c1a2-126">Création des clusters</span><span class="sxs-lookup"><span data-stu-id="4c1a2-126">Create the clusters</span></span>

<span data-ttu-id="4c1a2-127">Apache Kafka sur HDInsight ne donne pas accès aux répartiteurs Kafka via l’internet public.</span><span class="sxs-lookup"><span data-stu-id="4c1a2-127">Apache Kafka on HDInsight does not provide access to the Kafka brokers over the public internet.</span></span> <span data-ttu-id="4c1a2-128">Tout ce qui communique avec Kafka doit se trouver sur le même réseau virtuel Azure que les nœuds du cluster Kafka.</span><span class="sxs-lookup"><span data-stu-id="4c1a2-128">Anything that talks to Kafka must be in the same Azure virtual network as the nodes in the Kafka cluster.</span></span> <span data-ttu-id="4c1a2-129">Pour cet exemple, les clusters Kafka et Storm sont situés dans un réseau virtuel Azure.</span><span class="sxs-lookup"><span data-stu-id="4c1a2-129">For this example, both the Kafka and Storm clusters are located in an Azure virtual network.</span></span> <span data-ttu-id="4c1a2-130">Le diagramme suivant illustre le flux de communication entre les clusters :</span><span class="sxs-lookup"><span data-stu-id="4c1a2-130">The following diagram shows how communication flows between the clusters:</span></span>

![Diagramme des clusters Storm et Kafka dans un réseau virtuel Azure](./media/hdinsight-apache-storm-with-kafka/storm-kafka-vnet.png)

> [!NOTE]
> <span data-ttu-id="4c1a2-132">Les autres services sur le cluster, tels que SSH et Ambari, sont accessibles via Internet.</span><span class="sxs-lookup"><span data-stu-id="4c1a2-132">Other services on the cluster such as SSH and Ambari can be accessed over the internet.</span></span> <span data-ttu-id="4c1a2-133">Pour plus d’informations sur les ports publics disponibles avec HDInsight, consultez [Ports et URI utilisés par HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span><span class="sxs-lookup"><span data-stu-id="4c1a2-133">For more information on the public ports available with HDInsight, see [Ports and URIs used by HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span></span>

<span data-ttu-id="4c1a2-134">Même si vous pouvez créer un réseau virtuel Azure, et des clusters Kafka et Storm manuellement, il est plus facile d’utiliser un modèle Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="4c1a2-134">While you can create an Azure virtual network, Kafka, and Storm clusters manually, it's easier to use an Azure Resource Manager template.</span></span> <span data-ttu-id="4c1a2-135">Utilisez les étapes suivantes pour déployer un réseau virtuel Azure et des clusters Kafka et Storm sur votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="4c1a2-135">Use the following steps to deploy an Azure virtual network, Kafka, and Storm clusters to your Azure subscription.</span></span>

1. <span data-ttu-id="4c1a2-136">Utilisez le bouton suivant pour vous connecter à Azure et ouvrir le modèle dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="4c1a2-136">Use the following button to sign in to Azure and open the template in the Azure portal.</span></span>
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-kafka-storm-cluster-in-vnet-v2.json" target="_blank"><img src="./media/hdinsight-apache-storm-with-kafka/deploy-to-azure.png" alt="Deploy to Azure"></a>
   
    <span data-ttu-id="4c1a2-137">Le modèle Azure Resource Manager se trouve à l’adresse **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-storm-cluster-in-vnet-v1.json**.</span><span class="sxs-lookup"><span data-stu-id="4c1a2-137">The Azure Resource Manager template is located at **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-storm-cluster-in-vnet-v1.json**.</span></span> <span data-ttu-id="4c1a2-138">Il crée les ressources suivantes :</span><span class="sxs-lookup"><span data-stu-id="4c1a2-138">It creates the following resources:</span></span>
    
    * <span data-ttu-id="4c1a2-139">Groupe de ressources Azure</span><span class="sxs-lookup"><span data-stu-id="4c1a2-139">Azure resource group</span></span>
    * <span data-ttu-id="4c1a2-140">Réseau virtuel Azure</span><span class="sxs-lookup"><span data-stu-id="4c1a2-140">Azure Virtual Network</span></span>
    * <span data-ttu-id="4c1a2-141">Compte de Stockage Azure</span><span class="sxs-lookup"><span data-stu-id="4c1a2-141">Azure Storage account</span></span>
    * <span data-ttu-id="4c1a2-142">Kafka sur HDInsight version 3.6 (trois nœuds worker)</span><span class="sxs-lookup"><span data-stu-id="4c1a2-142">Kafka on HDInsight version 3.6 (three worker nodes)</span></span>
    * <span data-ttu-id="4c1a2-143">Storm sur HDInsight version 3.6 (trois nœuds worker)</span><span class="sxs-lookup"><span data-stu-id="4c1a2-143">Storm on HDInsight version 3.6 (three worker nodes)</span></span>

  > [!WARNING]
  > <span data-ttu-id="4c1a2-144">Pour garantir la disponibilité de Kafka sur HDInsight, votre cluster doit contenir au moins trois nœuds Worker.</span><span class="sxs-lookup"><span data-stu-id="4c1a2-144">To guarantee availability of Kafka on HDInsight, your cluster must contain at least three worker nodes.</span></span> <span data-ttu-id="4c1a2-145">Ce modèle crée un cluster Kafka qui contient trois nœuds Worker.</span><span class="sxs-lookup"><span data-stu-id="4c1a2-145">This template creates a Kafka cluster that contains three worker nodes.</span></span>

2. <span data-ttu-id="4c1a2-146">Utilisez les instructions suivantes pour remplir les entrées sur le panneau **déploiement personnalisé** :</span><span class="sxs-lookup"><span data-stu-id="4c1a2-146">Use the following guidance to populate the entries on the **Custom deployment** blade:</span></span>
   
    ![Déploiement HDInsight personnalisé](./media/hdinsight-apache-storm-with-kafka/parameters.png)

    * <span data-ttu-id="4c1a2-148">**Groupe de ressources** : créez un groupe de ressources ou sélectionnez-en un.</span><span class="sxs-lookup"><span data-stu-id="4c1a2-148">**Resource group**: Create a group or select an existing one.</span></span> <span data-ttu-id="4c1a2-149">Ce groupe contient le cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4c1a2-149">This group contains the HDInsight cluster.</span></span>
   
    * <span data-ttu-id="4c1a2-150">**Emplacement** : choisissez un emplacement proche de vous géographiquement.</span><span class="sxs-lookup"><span data-stu-id="4c1a2-150">**Location**: Select a location geographically close to you.</span></span>

    * <span data-ttu-id="4c1a2-151">**Nom de cluster de base** : cette valeur sera utilisée comme nom de base pour les clusters Storm et HBase.</span><span class="sxs-lookup"><span data-stu-id="4c1a2-151">**Base Cluster Name**: This value is used as the base name for the Storm and Kafka clusters.</span></span> <span data-ttu-id="4c1a2-152">Par exemple, si vous entrez **hdi**, cela crée un cluster Storm nommé **storm-hdi** et un cluster Kafka nommé **kafka-hdi**.</span><span class="sxs-lookup"><span data-stu-id="4c1a2-152">For example, entering **hdi** creates a Storm cluster named **storm-hdi** and a Kafka cluster named **kafka-hdi**.</span></span>
   
    * <span data-ttu-id="4c1a2-153">**Nom d’utilisateur du cluster** : nom utilisateur Admin pour les clusters Storm et Kafka.</span><span class="sxs-lookup"><span data-stu-id="4c1a2-153">**Cluster Login User Name**: The admin user name for the Storm and Kafka clusters.</span></span>
   
    * <span data-ttu-id="4c1a2-154">**Mot de passe du cluster** : mot de passe utilisateur Admin pour les clusters Storm et Kafka.</span><span class="sxs-lookup"><span data-stu-id="4c1a2-154">**Cluster Login Password**: The admin user password for the Storm and Kafka clusters.</span></span>
    
    * <span data-ttu-id="4c1a2-155">**Nom d’utilisateur SSH** : utilisateur SSH permettant de créer des clusters Storm et Kafka.</span><span class="sxs-lookup"><span data-stu-id="4c1a2-155">**SSH User Name**: The SSH user to create for the Storm and Kafka clusters.</span></span>
    
    * <span data-ttu-id="4c1a2-156">**Mot de passe SSH** : mot de passe de l’utilisateur SSH pour les clusters Storm et Kafka.</span><span class="sxs-lookup"><span data-stu-id="4c1a2-156">**SSH Password**: The password for the SSH user for the Storm and Kafka clusters.</span></span>

3. <span data-ttu-id="4c1a2-157">Passez en revue les **termes et conditions**, puis cochez la case **J’accepte les termes et conditions mentionnés ci-dessus**.</span><span class="sxs-lookup"><span data-stu-id="4c1a2-157">Read the **Terms and Conditions**, and then select **I agree to the terms and conditions stated above**.</span></span>

4. <span data-ttu-id="4c1a2-158">Pour finir, cochez **Épingler au tableau de bord**, puis sélectionnez **Acheter**.</span><span class="sxs-lookup"><span data-stu-id="4c1a2-158">Finally, check **Pin to dashboard** and then select **Purchase**.</span></span> <span data-ttu-id="4c1a2-159">La création des clusters prend environ 20 minutes.</span><span class="sxs-lookup"><span data-stu-id="4c1a2-159">It takes about 20 minutes to create the clusters.</span></span>

<span data-ttu-id="4c1a2-160">Une fois les ressources créées, le panneau du groupe de ressources s’affiche.</span><span class="sxs-lookup"><span data-stu-id="4c1a2-160">Once the resources have been created, the blade for the resource group is displayed.</span></span>

![Volet du groupe de ressources pour les clusters et le réseau virtuel](./media/hdinsight-apache-storm-with-kafka/groupblade.png)

> [!IMPORTANT]
> <span data-ttu-id="4c1a2-162">Les noms des clusters HDInsight sont **storm-BASENAME** et **kafka-BASENAME**, où BASENAME est le nom que vous avez fourni pour le modèle.</span><span class="sxs-lookup"><span data-stu-id="4c1a2-162">Notice that the names of the HDInsight clusters are **storm-BASENAME** and **kafka-BASENAME**, where BASENAME is the name you provided to the template.</span></span> <span data-ttu-id="4c1a2-163">Vous utilisez ces noms dans les étapes ultérieures, lors de la connexion aux clusters.</span><span class="sxs-lookup"><span data-stu-id="4c1a2-163">You use these names in later steps when connecting to the clusters.</span></span>

## <a name="understanding-the-code"></a><span data-ttu-id="4c1a2-164">Présentation du code</span><span class="sxs-lookup"><span data-stu-id="4c1a2-164">Understanding the code</span></span>

<span data-ttu-id="4c1a2-165">Ce projet contient deux topologies :</span><span class="sxs-lookup"><span data-stu-id="4c1a2-165">This project contains two topologies:</span></span>

* <span data-ttu-id="4c1a2-166">**KafkaWriter** : définie par le fichier **writer.yaml**, cette topologie écrit des phrases aléatoires dans Kafka en utilisant le KafkaBolt fourni avec Apache Storm.</span><span class="sxs-lookup"><span data-stu-id="4c1a2-166">**KafkaWriter**: Defined by the **writer.yaml** file, this topology writes random sentences to Kafka using the KafkaBolt provided with Apache Storm.</span></span>

    <span data-ttu-id="4c1a2-167">Cette topologie utilise un composant **SentenceSpout** personnalisé pour générer des phrases aléatoires.</span><span class="sxs-lookup"><span data-stu-id="4c1a2-167">This topology uses a custom **SentenceSpout** component to generate random sentences.</span></span>

* <span data-ttu-id="4c1a2-168">**KafkaReader** : définie par le fichier **reader.yaml**, cette topologie lit les données à partir de Kafka à l’aide du KafkaSpout fourni avec Apache Storm, puis écrit les données dans stdout.</span><span class="sxs-lookup"><span data-stu-id="4c1a2-168">**KafkaReader**: Defined by the **reader.yaml** file, this topology reads data from Kafka using the KafkaSpout provided with Apache Storm, then logs the data to stdout.</span></span>

    <span data-ttu-id="4c1a2-169">Cette topologie utilise le Storm HdfsBolt pour écrire des données dans le stockage par défaut pour le cluster Storm.</span><span class="sxs-lookup"><span data-stu-id="4c1a2-169">This topology uses the Storm HdfsBolt to write data to default storage for the Storm cluster.</span></span>
### <a name="flux"></a><span data-ttu-id="4c1a2-170">Flux</span><span class="sxs-lookup"><span data-stu-id="4c1a2-170">Flux</span></span>

<span data-ttu-id="4c1a2-171">Les topologies sont définies à l’aide de [Flux](https://storm.apache.org/releases/1.1.0/flux.html).</span><span class="sxs-lookup"><span data-stu-id="4c1a2-171">The topologies are defined using [Flux](https://storm.apache.org/releases/1.1.0/flux.html).</span></span> <span data-ttu-id="4c1a2-172">Flux a été introduit dans Storm 0.10.x et vous permet de séparer la configuration de topologie du code.</span><span class="sxs-lookup"><span data-stu-id="4c1a2-172">Flux was introduced in Storm 0.10.x and allows you to separate the topology configuration from the code.</span></span> <span data-ttu-id="4c1a2-173">Pour les topologies qui utilisent l’infrastructure Flux, la topologie est définie dans un fichier YAML.</span><span class="sxs-lookup"><span data-stu-id="4c1a2-173">For Topologies that use the Flux framework, the topology is defined in a YAML file.</span></span> <span data-ttu-id="4c1a2-174">Le fichier YAML peut être inclus dans le cadre de la topologie.</span><span class="sxs-lookup"><span data-stu-id="4c1a2-174">The YAML file can be included as part of the topology.</span></span> <span data-ttu-id="4c1a2-175">Il peut également s’agir d’un fichier autonome utilisé lorsque vous envoyez la topologie.</span><span class="sxs-lookup"><span data-stu-id="4c1a2-175">It can also be a standalone file used when you submit the topology.</span></span> <span data-ttu-id="4c1a2-176">Flux prend également en charge la substitution des variables au moment de l’exécution, ce qui est utilisé dans cet exemple.</span><span class="sxs-lookup"><span data-stu-id="4c1a2-176">Flux also supports variable substitution at run-time, which is used in this example.</span></span>

<span data-ttu-id="4c1a2-177">Les paramètres suivants sont définis au moment de l’exécution pour les topologies suivantes :</span><span class="sxs-lookup"><span data-stu-id="4c1a2-177">The following parameters are set at run time for these topologies:</span></span>

* <span data-ttu-id="4c1a2-178">`${kafka.topic}` : nom de la rubrique Kafka dans laquelle les topologies lisent et écrivent.</span><span class="sxs-lookup"><span data-stu-id="4c1a2-178">`${kafka.topic}`: The name of the Kafka topic that the topologies read/write to.</span></span>

* <span data-ttu-id="4c1a2-179">`${kafka.broker.hosts}` : hôtes sur lesquels les répartiteurs Kafka s’exécutent.</span><span class="sxs-lookup"><span data-stu-id="4c1a2-179">`${kafka.broker.hosts}`: The hosts that the Kafka brokers run on.</span></span> <span data-ttu-id="4c1a2-180">Les informations sur les répartiteurs sont utilisées par le KafkaBolt lors de l’écriture sur Kafka.</span><span class="sxs-lookup"><span data-stu-id="4c1a2-180">The broker information is used by the KafkaBolt when writing to Kafka.</span></span>

* <span data-ttu-id="4c1a2-181">`${kafka.zookeeper.hosts}`: hôtes sur lesquels Zookeeper s’exécute dans le cluster Kafka.</span><span class="sxs-lookup"><span data-stu-id="4c1a2-181">`${kafka.zookeeper.hosts}`: The hosts that Zookeeper runs on in the Kafka cluster.</span></span>

<span data-ttu-id="4c1a2-182">Pour plus d’informations sur les topologies Flux, voir la page [https://storm.apache.org/releases/1.1.0/flux.html](https://storm.apache.org/releases/1.1.0/flux.html).</span><span class="sxs-lookup"><span data-stu-id="4c1a2-182">For more information on Flux topologies, see [https://storm.apache.org/releases/1.1.0/flux.html](https://storm.apache.org/releases/1.1.0/flux.html).</span></span>

## <a name="download-and-compile-the-project"></a><span data-ttu-id="4c1a2-183">Téléchargez et compilez le projet</span><span class="sxs-lookup"><span data-stu-id="4c1a2-183">Download and compile the project</span></span>

1. <span data-ttu-id="4c1a2-184">Dans votre environnement de développement, téléchargez le projet sur [https://github.com/Azure-Samples/hdinsight-storm-java-kafka](https://github.com/Azure-Samples/hdinsight-storm-java-kafka), ouvrez une interface de ligne de commande et accédez à l’emplacement auquel vous avez téléchargé le projet.</span><span class="sxs-lookup"><span data-stu-id="4c1a2-184">On your development environment, download the project from [https://github.com/Azure-Samples/hdinsight-storm-java-kafka](https://github.com/Azure-Samples/hdinsight-storm-java-kafka), open a command-line, and change directories to the location that you downloaded the project.</span></span>

2. <span data-ttu-id="4c1a2-185">À partir du répertoire **hdinsight-storm-java-kafka**, utilisez la commande suivante pour compiler le projet et créer un package de déploiement :</span><span class="sxs-lookup"><span data-stu-id="4c1a2-185">From the **hdinsight-storm-java-kafka** directory, use the following command to compile the project and create a package for deployment:</span></span>

  ```bash
  mvn clean package
  ```

    <span data-ttu-id="4c1a2-186">Le processus de création de package crée un fichier nommé `KafkaTopology-1.0-SNAPSHOT.jar` dans le répertoire `target`.</span><span class="sxs-lookup"><span data-stu-id="4c1a2-186">The package process creates a file named `KafkaTopology-1.0-SNAPSHOT.jar` in the `target` directory.</span></span>

3. <span data-ttu-id="4c1a2-187">Utilisez la commande suivante pour copier le package sur votre Storm dans votre cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4c1a2-187">Use the following commands to copy the package to your Storm on HDInsight cluster.</span></span> <span data-ttu-id="4c1a2-188">Remplacez **USERNAME** par le nom d’utilisateur SSH pour le cluster.</span><span class="sxs-lookup"><span data-stu-id="4c1a2-188">Replace **USERNAME** with the SSH user name for the cluster.</span></span> <span data-ttu-id="4c1a2-189">Remplacez **BASENAME** par le nom de base que vous avez utilisé lors de la création du cluster.</span><span class="sxs-lookup"><span data-stu-id="4c1a2-189">Replace **BASENAME** with the base name you used when creating the cluster.</span></span>

  ```bash
  scp ./target/KafkaTopology-1.0-SNAPSHOT.jar USERNAME@storm-BASENAME-ssh.azurehdinsight.net:KafkaTopology-1.0-SNAPSHOT.jar
  ```

    <span data-ttu-id="4c1a2-190">À l'invite, saisissez le mot de passe que vous avez utilisé lors de la création du cluster.</span><span class="sxs-lookup"><span data-stu-id="4c1a2-190">When prompted, enter the password you used when creating the clusters.</span></span>

## <a name="configure-the-topology"></a><span data-ttu-id="4c1a2-191">Configurer la topologie</span><span class="sxs-lookup"><span data-stu-id="4c1a2-191">Configure the topology</span></span>

1. <span data-ttu-id="4c1a2-192">Pour découvrir les hôtes du répartiteur Kafka, utilisez l’une des méthodes suivantes :</span><span class="sxs-lookup"><span data-stu-id="4c1a2-192">Use one of the following methods to discover the Kafka broker hosts:</span></span>

    ```powershell
    $creds = Get-Credential -UserName "admin" -Message "Enter the HDInsight login"
    $clusterName = Read-Host -Prompt "Enter the Kafka cluster name"
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/KAFKA/components/KAFKA_BROKER" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $brokerHosts = $respObj.host_components.HostRoles.host_name[0..1]
    ($brokerHosts -join ":9092,") + ":9092"
    ```

    ```bash
    curl -su admin -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/KAFKA/components/KAFKA_BROKER" | jq -r '["\(.host_components[].HostRoles.host_name):9092"] | join(",")' | cut -d',' -f1,2
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="4c1a2-193">L’exemple de Bash suppose que `$CLUSTERNAME` contient le nom du cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4c1a2-193">The Bash example assumes that `$CLUSTERNAME` contains the name of the HDInsight cluster.</span></span> <span data-ttu-id="4c1a2-194">Il suppose également que [jq](https://stedolan.github.io/jq/) est installé.</span><span class="sxs-lookup"><span data-stu-id="4c1a2-194">It also assumes that [jq](https://stedolan.github.io/jq/) is installed.</span></span> <span data-ttu-id="4c1a2-195">Lorsque vous y êtes invité, entrez le mot de passe du compte de connexion au cluster.</span><span class="sxs-lookup"><span data-stu-id="4c1a2-195">When prompted, enter the password for the cluster login account.</span></span>

    <span data-ttu-id="4c1a2-196">Les informations renvoyées sont similaire au texte suivant :</span><span class="sxs-lookup"><span data-stu-id="4c1a2-196">The value returned is similar to the following text:</span></span>

        wn0-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:9092,wn1-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:9092

    > [!IMPORTANT]
    > <span data-ttu-id="4c1a2-197">Votre cluster pouvant disposer de plus de deux hôtes de répartiteur, il n’est pas nécessaire de fournir une liste complète des hôtes aux clients.</span><span class="sxs-lookup"><span data-stu-id="4c1a2-197">While there may be more than two broker hosts for your cluster, you do not need to provide a full list of all hosts to clients.</span></span> <span data-ttu-id="4c1a2-198">Un ou deux sont suffisants.</span><span class="sxs-lookup"><span data-stu-id="4c1a2-198">One or two is enough.</span></span>

2. <span data-ttu-id="4c1a2-199">Pour découvrir les hôtes du Zookeeper Kafka, utilisez l’une des méthodes suivantes :</span><span class="sxs-lookup"><span data-stu-id="4c1a2-199">Use one of the following methods to discover the Kafka Zookeeper hosts:</span></span>

    ```powershell
    $creds = Get-Credential -UserName "admin" -Message "Enter the HDInsight login"
    $clusterName = Read-Host -Prompt "Enter the Kafka cluster name"
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/ZOOKEEPER/components/ZOOKEEPER_SERVER" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $zookeeperHosts = $respObj.host_components.HostRoles.host_name[0..1]
    ($zookeeperHosts -join ":2181,") + ":2181"
    ```

    ```bash
    curl -su admin -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/ZOOKEEPER/components/ZOOKEEPER_SERVER" | jq -r '["\(.host_components[].HostRoles.host_name):2181"] | join(",")' | cut -d',' -f1,2
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="4c1a2-200">L’exemple de Bash suppose que `$CLUSTERNAME` contient le nom du cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4c1a2-200">The Bash example assumes that `$CLUSTERNAME` contains the name of the HDInsight cluster.</span></span> <span data-ttu-id="4c1a2-201">Il suppose également que [jq](https://stedolan.github.io/jq/) est installé.</span><span class="sxs-lookup"><span data-stu-id="4c1a2-201">It also assumes that [jq](https://stedolan.github.io/jq/) is installed.</span></span> <span data-ttu-id="4c1a2-202">Lorsque vous y êtes invité, entrez le mot de passe du compte de connexion au cluster.</span><span class="sxs-lookup"><span data-stu-id="4c1a2-202">When prompted, enter the password for the cluster login account.</span></span>

    <span data-ttu-id="4c1a2-203">Les informations renvoyées sont similaire au texte suivant :</span><span class="sxs-lookup"><span data-stu-id="4c1a2-203">The value returned is similar to the following text:</span></span>

        zk0-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:2181,zk2-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:2181

    > [!IMPORTANT]
    > <span data-ttu-id="4c1a2-204">Puisqu’il existe plus de deux nœuds Zookeeper, il n’est pas nécessaire de fournir une liste complète des hôtes aux clients.</span><span class="sxs-lookup"><span data-stu-id="4c1a2-204">While there are more than two Zookeeper nodes, you do not need to provide a full list of all hosts to clients.</span></span> <span data-ttu-id="4c1a2-205">Un ou deux sont suffisants.</span><span class="sxs-lookup"><span data-stu-id="4c1a2-205">One or two is enough.</span></span>

    <span data-ttu-id="4c1a2-206">Enregistrez cette valeur, car vous l’utiliserez plus tard.</span><span class="sxs-lookup"><span data-stu-id="4c1a2-206">Save this value, as it is used later.</span></span>

3. <span data-ttu-id="4c1a2-207">Modifiez le fichier `dev.properties` à la racine du projet.</span><span class="sxs-lookup"><span data-stu-id="4c1a2-207">Edit the `dev.properties` file in the root of the project.</span></span> <span data-ttu-id="4c1a2-208">Ajoutez les informations des hôtes Répartiteur et Zookeeper aux lignes correspondantes dans ce fichier.</span><span class="sxs-lookup"><span data-stu-id="4c1a2-208">Add the Broker and Zookeeper hosts information to the matching lines in this file.</span></span> <span data-ttu-id="4c1a2-209">L’exemple suivant est configuré à l’aide des exemples de valeurs de l’étape précédente :</span><span class="sxs-lookup"><span data-stu-id="4c1a2-209">The following example is configured using the sample values from the previous steps:</span></span>

        kafka.zookeeper.hosts: zk0-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:2181,zk2-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:2181
        kafka.broker.hosts: wn0-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:9092,wn1-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:9092
        kafka.topic: stormtopic

4. <span data-ttu-id="4c1a2-210">Enregistrez le fichier `dev.properties`, puis utilisez la commande suivante pour le charger sur le cluster Storm :</span><span class="sxs-lookup"><span data-stu-id="4c1a2-210">Save the `dev.properties` file and then use the following command to upload it to the Storm cluster:</span></span>

     ```bash
    scp dev.properties USERNAME@storm-BASENAME-ssh.azurehdinsight.net:KafkaTopology-1.0-SNAPSHOT.jar
    ```

    <span data-ttu-id="4c1a2-211">Remplacez **USERNAME** par le nom d’utilisateur SSH pour le cluster.</span><span class="sxs-lookup"><span data-stu-id="4c1a2-211">Replace **USERNAME** with the SSH user name for the cluster.</span></span> <span data-ttu-id="4c1a2-212">Remplacez **BASENAME** par le nom de base que vous avez utilisé lors de la création du cluster.</span><span class="sxs-lookup"><span data-stu-id="4c1a2-212">Replace **BASENAME** with the base name you used when creating the cluster.</span></span>

## <a name="start-the-writer"></a><span data-ttu-id="4c1a2-213">Démarrer l’enregistreur</span><span class="sxs-lookup"><span data-stu-id="4c1a2-213">Start the writer</span></span>

1. <span data-ttu-id="4c1a2-214">Utilisez ce qui suit pour vous connecter au cluster Storm à l’aide de SSH.</span><span class="sxs-lookup"><span data-stu-id="4c1a2-214">Use the following to connect to the Storm cluster using SSH.</span></span> <span data-ttu-id="4c1a2-215">Remplacez **USERNAME** par le nom d’utilisateur SSH que vous avez utilisé lors de la création du cluster.</span><span class="sxs-lookup"><span data-stu-id="4c1a2-215">Replace **USERNAME** with the SSH user name used when creating the cluster.</span></span> <span data-ttu-id="4c1a2-216">Remplacez **BASENAME** par le nom de base que vous avez utilisé lors de la création du cluster.</span><span class="sxs-lookup"><span data-stu-id="4c1a2-216">Replace **BASENAME** with the base name used when creating the cluster.</span></span>

  ```bash
  ssh USERNAME@storm-BASENAME-ssh.azurehdinsight.net
  ```

    <span data-ttu-id="4c1a2-217">À l'invite, saisissez le mot de passe que vous avez utilisé lors de la création du cluster.</span><span class="sxs-lookup"><span data-stu-id="4c1a2-217">When prompted, enter the password you used when creating the clusters.</span></span>
   
    <span data-ttu-id="4c1a2-218">Pour en savoir plus, voir [Utilisation de SSH avec HDInsight (Hadoop) depuis Bash (l’interpréteur de commande) sur Windows 10, Linux, Unix ou OS X](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="4c1a2-218">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="4c1a2-219">À partir de la connexion SSH, utilisez la commande suivante pour créer la rubrique Kafka utilisée par la topologie :</span><span class="sxs-lookup"><span data-stu-id="4c1a2-219">From the SSH connection, use the following command to create the Kafka topic used by the topology:</span></span>

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --create --replication-factor 3 --partitions 8 --topic stormtopic --zookeeper $KAFKAZKHOSTS
    ```

    <span data-ttu-id="4c1a2-220">Remplacez `$KAFKAZKHOSTS` par les informations de l’hôte Zookeeper que vous avez récupérées dans la section précédente.</span><span class="sxs-lookup"><span data-stu-id="4c1a2-220">Replace `$KAFKAZKHOSTS` with the Zookeeper host information you retrieved in the previous section.</span></span>

2. <span data-ttu-id="4c1a2-221">Dans la connexion SSH sur le cluster Storm, utilisez la commande suivante pour démarrer la topologie d’enregistreur :</span><span class="sxs-lookup"><span data-stu-id="4c1a2-221">From the SSH connection to the Storm cluster, use the following command to start the writer topology:</span></span>

    ```bash
    storm jar KafkaTopology-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /writer.yaml --filter dev.properties
    ```

    <span data-ttu-id="4c1a2-222">Les paramètres utilisés avec cette commande sont les suivants :</span><span class="sxs-lookup"><span data-stu-id="4c1a2-222">The parameters used with this command are:</span></span>

    * <span data-ttu-id="4c1a2-223">`org.apache.storm.flux.Flux` : utilisez Flux pour configurer et exécuter cette topologie.</span><span class="sxs-lookup"><span data-stu-id="4c1a2-223">`org.apache.storm.flux.Flux`: Use Flux to configure and run this topology.</span></span>

    * <span data-ttu-id="4c1a2-224">`--remote` : envoyez la topologie à Nimbus.</span><span class="sxs-lookup"><span data-stu-id="4c1a2-224">`--remote`: Submit the topology to Nimbus.</span></span> <span data-ttu-id="4c1a2-225">La topologie est distribuée sur les nœuds de travail dans le cluster.</span><span class="sxs-lookup"><span data-stu-id="4c1a2-225">The topology is distributed across the worker nodes in the cluster.</span></span>

    * <span data-ttu-id="4c1a2-226">`-R /writer.yaml` : utilisez le fichier `writer.yaml` pour configurer la topologie.</span><span class="sxs-lookup"><span data-stu-id="4c1a2-226">`-R /writer.yaml`: Use the `writer.yaml` file to configure the topology.</span></span> <span data-ttu-id="4c1a2-227">`-R` indique que cette ressource est incluse dans le fichier jar.</span><span class="sxs-lookup"><span data-stu-id="4c1a2-227">`-R` indicates that this resource is included in the jar file.</span></span> <span data-ttu-id="4c1a2-228">Il se trouve à la racine du fichier jar, donc `/writer.yaml` est le chemin d’accès à celui-ci.</span><span class="sxs-lookup"><span data-stu-id="4c1a2-228">It's in the root of the jar, so `/writer.yaml` is the path to it.</span></span>

    * <span data-ttu-id="4c1a2-229">`--filter` : complétez les entrées de la topologie `writer.yaml` à l’aide des valeurs figurant dans le fichier `dev.properties`.</span><span class="sxs-lookup"><span data-stu-id="4c1a2-229">`--filter`: Populate entries in the `writer.yaml` topology using values in the `dev.properties` file.</span></span> <span data-ttu-id="4c1a2-230">Par exemple, la valeur de l’entrée `kafka.topic` dans le fichier est utilisée pour remplacer l’entrée `${kafka.topic}` dans la définition de la topologie.</span><span class="sxs-lookup"><span data-stu-id="4c1a2-230">For example, the value of the `kafka.topic` entry in the file is used to replace the `${kafka.topic}` entry in the topology definition.</span></span>

5. <span data-ttu-id="4c1a2-231">Après démarrage de la topologie, utilisez la commande suivante pour vérifier qu’elle écrit les données dans la rubrique Kafka :</span><span class="sxs-lookup"><span data-stu-id="4c1a2-231">Once the topology has started, use the following command to verify that it is writing data to the Kafka topic:</span></span>

  ```bash
  /usr/hdp/current/kafka-broker/bin/kafka-console-consumer.sh --zookeeper $KAFKAZKHOSTS --from-beginning --topic stormtopic
  ```

    <span data-ttu-id="4c1a2-232">Remplacez `$KAFKAZKHOSTS` par les informations de l’hôte Zookeeper que vous avez récupérées dans la section précédente.</span><span class="sxs-lookup"><span data-stu-id="4c1a2-232">Replace `$KAFKAZKHOSTS` with the Zookeeper host information you retrieved in the previous section.</span></span>

    <span data-ttu-id="4c1a2-233">Cette commande utilise un script fourni avec Kafka pour surveiller la rubrique.</span><span class="sxs-lookup"><span data-stu-id="4c1a2-233">This command uses a script shipped with Kafka to monitor the topic.</span></span> <span data-ttu-id="4c1a2-234">Après quelques instants, elle doit commencer à retourner des phrases aléatoires qui ont été écrites dans la rubrique.</span><span class="sxs-lookup"><span data-stu-id="4c1a2-234">After a moment, it should start returning random sentences that have been written to the topic.</span></span> <span data-ttu-id="4c1a2-235">Le résultat ressemble à l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="4c1a2-235">The output is similar to the following example:</span></span>

        i am at two with nature             
        an apple a day keeps the doctor away
        snow white and the seven dwarfs     
        the cow jumped over the moon        
        an apple a day keeps the doctor away
        an apple a day keeps the doctor away
        the cow jumped over the moon        
        an apple a day keeps the doctor away
        an apple a day keeps the doctor away
        four score and seven years ago      
        snow white and the seven dwarfs     
        snow white and the seven dwarfs     
        i am at two with nature             
        an apple a day keeps the doctor away

    <span data-ttu-id="4c1a2-236">Pour arrêter le script, utilisez les touches Ctrl + C.</span><span class="sxs-lookup"><span data-stu-id="4c1a2-236">Use Ctrl+c to stop the script.</span></span>

## <a name="start-the-reader"></a><span data-ttu-id="4c1a2-237">Démarrer le lecteur</span><span class="sxs-lookup"><span data-stu-id="4c1a2-237">Start the reader</span></span>

1. <span data-ttu-id="4c1a2-238">Dans la session SSH sur le cluster Storm, utilisez la commande suivante pour démarrer la topologie de lecteur :</span><span class="sxs-lookup"><span data-stu-id="4c1a2-238">From the SSH session to the Storm cluster, use the following command to start the reader topology:</span></span>

  ```bash
  storm jar KafkaTopology-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /reader.yaml --filter dev.properties
  ```

2. <span data-ttu-id="4c1a2-239">Une fois que la topologie commence, ouvrez l’interface utilisateur Storm.</span><span class="sxs-lookup"><span data-stu-id="4c1a2-239">Once the topology starts, open the Storm UI.</span></span> <span data-ttu-id="4c1a2-240">Cette interface utilisateur web est située dans https://storm-BASENAME.azurehdinsight.net/stormui.</span><span class="sxs-lookup"><span data-stu-id="4c1a2-240">This web UI is located at https://storm-BASENAME.azurehdinsight.net/stormui.</span></span> <span data-ttu-id="4c1a2-241">Remplacez __BASENAME__ par le nom de base que vous avez utilisé lors de la création du cluster.</span><span class="sxs-lookup"><span data-stu-id="4c1a2-241">Replace __BASENAME__ with the base name used when the cluster was created.</span></span> 

    <span data-ttu-id="4c1a2-242">Lorsque vous y êtes invité, utilisez le nom d’utilisateur administrateur (par défaut `admin`) et le mot de passe utilisés lors de la création du cluster.</span><span class="sxs-lookup"><span data-stu-id="4c1a2-242">When prompted, use the admin login name (default, `admin`) and password used when the cluster was created.</span></span> <span data-ttu-id="4c1a2-243">Vous voyez s’afficher une page web similaire à l’image suivante :</span><span class="sxs-lookup"><span data-stu-id="4c1a2-243">You see a web page similar to the following image:</span></span>

    ![Interface utilisateur de Storm](./media/hdinsight-apache-storm-with-kafka/stormui.png)

3. <span data-ttu-id="4c1a2-245">Dans l’interface utilisateur de Storm, sélectionnez le lien __kafka-lecteur__ dans la section __Résumé de la topologie__ pour afficher des informations sur la topologie __kafka-reader__.</span><span class="sxs-lookup"><span data-stu-id="4c1a2-245">From the Storm UI, select the __kafka-reader__ link in the __Topology Summary__ section to display information about the __kafka-reader__ topology.</span></span>

    ![Section Résumé de topologie l'interface utilisateur web de Storm](./media/hdinsight-apache-storm-with-kafka/topology-summary.png)

4. <span data-ttu-id="4c1a2-247">Pour afficher des informations sur les instances du composant logger-bolt, sélectionnez le lien __logger-bolt__ dans la section __Bolts (All time)__.</span><span class="sxs-lookup"><span data-stu-id="4c1a2-247">To display information about the instances of the logger-bolt component, select the __logger-bolt__ link in the __Bolts (All time)__ section.</span></span>

    ![Lien logger-bolt dans la section bolts](./media/hdinsight-apache-storm-with-kafka/bolts.png)

5. <span data-ttu-id="4c1a2-249">Dans la section __Executors__, sélectionnez un lien dans la colonne __Port__ pour afficher des informations de journalisation sur cette instance du composant.</span><span class="sxs-lookup"><span data-stu-id="4c1a2-249">In the __Executors__ section, select a link in the __Port__ column to display logging information about this instance of the component.</span></span>

    ![Exécuteurs de lien](./media/hdinsight-apache-storm-with-kafka/executors.png)

    <span data-ttu-id="4c1a2-251">Le journal contient un journal des données lues à partir de la rubrique Kafka.</span><span class="sxs-lookup"><span data-stu-id="4c1a2-251">The log contains a log of the data read from the Kafka topic.</span></span> <span data-ttu-id="4c1a2-252">Les informations dans le journal sont similaires à ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="4c1a2-252">The information in the log is similar to the following text:</span></span>

        2016-11-04 17:47:14.907 c.m.e.LoggerBolt [INFO] Received data: four score and seven years ago
        2016-11-04 17:47:14.907 STDIO [INFO] the cow jumped over the moon
        2016-11-04 17:47:14.908 c.m.e.LoggerBolt [INFO] Received data: the cow jumped over the moon
        2016-11-04 17:47:14.911 STDIO [INFO] snow white and the seven dwarfs
        2016-11-04 17:47:14.911 c.m.e.LoggerBolt [INFO] Received data: snow white and the seven dwarfs
        2016-11-04 17:47:14.932 STDIO [INFO] snow white and the seven dwarfs
        2016-11-04 17:47:14.932 c.m.e.LoggerBolt [INFO] Received data: snow white and the seven dwarfs
        2016-11-04 17:47:14.969 STDIO [INFO] an apple a day keeps the doctor away
        2016-11-04 17:47:14.970 c.m.e.LoggerBolt [INFO] Received data: an apple a day keeps the doctor away

## <a name="stop-the-topologies"></a><span data-ttu-id="4c1a2-253">Arrêt des topologies</span><span class="sxs-lookup"><span data-stu-id="4c1a2-253">Stop the topologies</span></span>

<span data-ttu-id="4c1a2-254">Dans une session SSH sur le cluster Storm, utilisez la commande suivante pour arrêter les topologies Storm :</span><span class="sxs-lookup"><span data-stu-id="4c1a2-254">From an SSH session to the Storm cluster, use the following commands to stop the Storm topologies:</span></span>

  ```bash
  storm kill kafka-writer
  storm kill kafka-reader
  ```

## <a name="delete-the-cluster"></a><span data-ttu-id="4c1a2-255">Suppression du cluster</span><span class="sxs-lookup"><span data-stu-id="4c1a2-255">Delete the cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="4c1a2-256">Étant donné que les étapes décrites dans ce document créent deux clusters dans le même groupe de ressources Azure, vous pouvez supprimer le groupe de ressources du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="4c1a2-256">Since the steps in this document create both clusters in the same Azure resource group, you can delete the resource group in the Azure portal.</span></span> <span data-ttu-id="4c1a2-257">La suppression du groupe de ressources a pour effet de supprimer toutes les ressources créées en suivant les étapes décrites dans ce document.</span><span class="sxs-lookup"><span data-stu-id="4c1a2-257">Deleting the resource group removes all resources created by following this document.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4c1a2-258">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4c1a2-258">Next steps</span></span>

<span data-ttu-id="4c1a2-259">Pour plus d’exemples de topologies qui peuvent être utilisées avec Storm sur HDInsight, consultez [Exemples de topologies et composants Storm](hdinsight-storm-example-topology.md).</span><span class="sxs-lookup"><span data-stu-id="4c1a2-259">For more example topologies that can be used with Storm on HDInsight, see [Example Storm topologies and components](hdinsight-storm-example-topology.md).</span></span>

<span data-ttu-id="4c1a2-260">Pour plus d’informations sur le déploiement et la surveillance des topologies sur HDInsight Linux, consultez [Déploiement et gestion des topologies Apache Storm sur HDInsight Linux](hdinsight-storm-deploy-monitor-topology-linux.md)</span><span class="sxs-lookup"><span data-stu-id="4c1a2-260">For information on deploying and monitoring topologies on Linux-based HDInsight, see [Deploy and manage Apache Storm topologies on Linux-based HDInsight](hdinsight-storm-deploy-monitor-topology-linux.md)</span></span>