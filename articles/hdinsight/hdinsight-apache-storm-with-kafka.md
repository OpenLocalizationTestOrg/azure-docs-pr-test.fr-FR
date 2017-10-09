---
title: aaaUse Kafka Apache avec Storm sur HDInsight - Azure | Documents Microsoft
description: "Apache Kafka est installé avec Apache Storm sur HDInsight. Découvrez comment toowrite tooKafka, puis lisez à partir de celui-ci, à l’aide de hello KafkaBolt et KafkaSpout des composants fournis avec Storm. Également apprendre comment toouse hello Flux framework toodefine et soumettre des topologies de Storm."
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
ms.openlocfilehash: 95701f51dfdf6f1a859dcde96d7053df4f21701f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-apache-kafka-preview-with-storm-on-hdinsight"></a><span data-ttu-id="724a1-105">Utilisation d’Apache Kafka (version préliminaire) avec Storm sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="724a1-105">Use Apache Kafka (preview) with Storm on HDInsight</span></span>

<span data-ttu-id="724a1-106">Découvrez comment tooread d’Apache Storm toouse à partir d’et d’écriture tooApache Kafka.</span><span class="sxs-lookup"><span data-stu-id="724a1-106">Learn how toouse Apache Storm tooread from and write tooApache Kafka.</span></span> <span data-ttu-id="724a1-107">Cet exemple montre également comment toosave des données à partir d’un toohello de topologie Storm compatible HDFS fichier système utilisé par HDInsight.</span><span class="sxs-lookup"><span data-stu-id="724a1-107">This example also demonstrates how toosave data from a Storm topology toohello HDFS-compatible file system used by HDInsight.</span></span>

> [!NOTE]
> <span data-ttu-id="724a1-108">étapes Hello dans ce document créent un groupe de ressources Azure qui contient à la fois une tempête sur HDInsight et un Kafka sur le cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="724a1-108">hello steps in this document create an Azure resource group that contains both a Storm on HDInsight and a Kafka on HDInsight cluster.</span></span> <span data-ttu-id="724a1-109">Ces clusters sont situés dans un réseau virtuel Azure, ce qui permet de hello Storm cluster toodirectly communiquent avec hello cluster de Kafka.</span><span class="sxs-lookup"><span data-stu-id="724a1-109">These clusters are both located within an Azure Virtual Network, which allows hello Storm cluster toodirectly communicate with hello Kafka cluster.</span></span>
> 
> <span data-ttu-id="724a1-110">Lorsque vous avez terminé les étapes hello dans ce document, n’oubliez pas de frais supplémentaires de toodelete hello clusters tooavoid.</span><span class="sxs-lookup"><span data-stu-id="724a1-110">When you are done with hello steps in this document, remember toodelete hello clusters tooavoid excess charges.</span></span>

## <a name="get-hello-code"></a><span data-ttu-id="724a1-111">Obtenir le code de hello</span><span class="sxs-lookup"><span data-stu-id="724a1-111">Get hello code</span></span>

<span data-ttu-id="724a1-112">code Hello pour exemple hello utilisé dans ce document est disponible à l’adresse [https://github.com/Azure-Samples/hdinsight-storm-java-kafka](https://github.com/Azure-Samples/hdinsight-storm-java-kafka).</span><span class="sxs-lookup"><span data-stu-id="724a1-112">hello code for hello example used in this document is available at [https://github.com/Azure-Samples/hdinsight-storm-java-kafka](https://github.com/Azure-Samples/hdinsight-storm-java-kafka).</span></span>

<span data-ttu-id="724a1-113">toocompile ce projet, vous devez hello configuration pour votre environnement de développement suivante :</span><span class="sxs-lookup"><span data-stu-id="724a1-113">toocompile this project, you need hello following configuration for your development environment:</span></span>

* <span data-ttu-id="724a1-114">[Java JDK 1.8](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="724a1-114">[Java JDK 1.8](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) or higher.</span></span> <span data-ttu-id="724a1-115">HDInsight 3.5 ou les versions ultérieures requièrent Java 8.</span><span class="sxs-lookup"><span data-stu-id="724a1-115">HDInsight 3.5 or higher require Java 8.</span></span>

* [<span data-ttu-id="724a1-116">Maven 3.x</span><span class="sxs-lookup"><span data-stu-id="724a1-116">Maven 3.x</span></span>](https://maven.apache.org/download.cgi)

* <span data-ttu-id="724a1-117">Un client SSH (vous devez hello `ssh` et `scp` commandes) - pour plus d’informations, consultez [utilisation de SSH avec HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="724a1-117">An SSH client (you need hello `ssh` and `scp` commands) - For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

* <span data-ttu-id="724a1-118">Un éditeur de texte ou IDE.</span><span class="sxs-lookup"><span data-stu-id="724a1-118">A text editor or IDE.</span></span>

<span data-ttu-id="724a1-119">Hello variables d’environnement suivantes peuvent être définis lors de l’installation de Java et hello JDK sur votre station de travail de développement.</span><span class="sxs-lookup"><span data-stu-id="724a1-119">hello following environment variables may be set when you install Java and hello JDK on your development workstation.</span></span> <span data-ttu-id="724a1-120">Toutefois, vous devez vérifier qu’ils existent et qu’ils contiennent des valeurs correctes de hello pour votre système.</span><span class="sxs-lookup"><span data-stu-id="724a1-120">However, you should check that they exist and that they contain hello correct values for your system.</span></span>

* <span data-ttu-id="724a1-121">`JAVA_HOME`-doit pointer toohello répertoire où hello JDK est installé.</span><span class="sxs-lookup"><span data-stu-id="724a1-121">`JAVA_HOME` - should point toohello directory where hello JDK is installed.</span></span>
* <span data-ttu-id="724a1-122">`PATH`-doit contenir hello suivant des chemins d’accès :</span><span class="sxs-lookup"><span data-stu-id="724a1-122">`PATH` - should contain hello following paths:</span></span>
  
    * <span data-ttu-id="724a1-123">`JAVA_HOME`(ou les chemins d’accès équivalents hello).</span><span class="sxs-lookup"><span data-stu-id="724a1-123">`JAVA_HOME` (or hello equivalent path).</span></span>
    * <span data-ttu-id="724a1-124">`JAVA_HOME\bin`(ou les chemins d’accès équivalents hello).</span><span class="sxs-lookup"><span data-stu-id="724a1-124">`JAVA_HOME\bin` (or hello equivalent path).</span></span>
    * <span data-ttu-id="724a1-125">répertoire de Hello où Maven est installé.</span><span class="sxs-lookup"><span data-stu-id="724a1-125">hello directory where Maven is installed.</span></span>

## <a name="create-hello-clusters"></a><span data-ttu-id="724a1-126">Créer des clusters de hello</span><span class="sxs-lookup"><span data-stu-id="724a1-126">Create hello clusters</span></span>

<span data-ttu-id="724a1-127">Kafka Apache sur HDInsight ne fournit pas d’accès toohello Kafka courtiers sur hello internet public.</span><span class="sxs-lookup"><span data-stu-id="724a1-127">Apache Kafka on HDInsight does not provide access toohello Kafka brokers over hello public internet.</span></span> <span data-ttu-id="724a1-128">Tout ce qui tooKafka doit se trouver dans des entretiens hello même réseau virtuel Azure en tant que nœuds hello dans hello cluster de Kafka.</span><span class="sxs-lookup"><span data-stu-id="724a1-128">Anything that talks tooKafka must be in hello same Azure virtual network as hello nodes in hello Kafka cluster.</span></span> <span data-ttu-id="724a1-129">Pour cet exemple, hello Kafka et les clusters Storm se trouvent dans un réseau virtuel Azure.</span><span class="sxs-lookup"><span data-stu-id="724a1-129">For this example, both hello Kafka and Storm clusters are located in an Azure virtual network.</span></span> <span data-ttu-id="724a1-130">Hello diagramme suivant illustre le flux de communication entre les clusters hello :</span><span class="sxs-lookup"><span data-stu-id="724a1-130">hello following diagram shows how communication flows between hello clusters:</span></span>

![Diagramme des clusters Storm et Kafka dans un réseau virtuel Azure](./media/hdinsight-apache-storm-with-kafka/storm-kafka-vnet.png)

> [!NOTE]
> <span data-ttu-id="724a1-132">Autres services sur un cluster de hello tels que SSH et Ambari sont accessibles via hello internet.</span><span class="sxs-lookup"><span data-stu-id="724a1-132">Other services on hello cluster such as SSH and Ambari can be accessed over hello internet.</span></span> <span data-ttu-id="724a1-133">Pour plus d’informations sur les ports publics de hello disponibles avec HDInsight, consultez [Ports et URI utilisé par HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span><span class="sxs-lookup"><span data-stu-id="724a1-133">For more information on hello public ports available with HDInsight, see [Ports and URIs used by HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span></span>

<span data-ttu-id="724a1-134">Tandis que vous pouvez créer un réseau virtuel Azure, Kafka, Storm clusters manuellement, il est plus facile toouse un modèle Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="724a1-134">While you can create an Azure virtual network, Kafka, and Storm clusters manually, it's easier toouse an Azure Resource Manager template.</span></span> <span data-ttu-id="724a1-135">Toodeploy un réseau virtuel Azure, Kafka, les étapes suivantes de hello utilisation et Storm clusters tooyour abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="724a1-135">Use hello following steps toodeploy an Azure virtual network, Kafka, and Storm clusters tooyour Azure subscription.</span></span>

1. <span data-ttu-id="724a1-136">Utilisez hello suivant toosign bouton dans tooAzure et modèle ouvert hello Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="724a1-136">Use hello following button toosign in tooAzure and open hello template in hello Azure portal.</span></span>
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-kafka-storm-cluster-in-vnet-v2.json" target="_blank"><img src="./media/hdinsight-apache-storm-with-kafka/deploy-to-azure.png" alt="Deploy tooAzure"></a>
   
    <span data-ttu-id="724a1-137">Hello modèle Azure Resource Manager se trouve dans **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-storm-cluster-in-vnet-v1.json**.</span><span class="sxs-lookup"><span data-stu-id="724a1-137">hello Azure Resource Manager template is located at **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-storm-cluster-in-vnet-v1.json**.</span></span> <span data-ttu-id="724a1-138">Il crée hello suivant des ressources :</span><span class="sxs-lookup"><span data-stu-id="724a1-138">It creates hello following resources:</span></span>
    
    * <span data-ttu-id="724a1-139">Groupe de ressources Azure</span><span class="sxs-lookup"><span data-stu-id="724a1-139">Azure resource group</span></span>
    * <span data-ttu-id="724a1-140">Réseau virtuel Azure</span><span class="sxs-lookup"><span data-stu-id="724a1-140">Azure Virtual Network</span></span>
    * <span data-ttu-id="724a1-141">Compte de Stockage Azure</span><span class="sxs-lookup"><span data-stu-id="724a1-141">Azure Storage account</span></span>
    * <span data-ttu-id="724a1-142">Kafka sur HDInsight version 3.6 (trois nœuds worker)</span><span class="sxs-lookup"><span data-stu-id="724a1-142">Kafka on HDInsight version 3.6 (three worker nodes)</span></span>
    * <span data-ttu-id="724a1-143">Storm sur HDInsight version 3.6 (trois nœuds worker)</span><span class="sxs-lookup"><span data-stu-id="724a1-143">Storm on HDInsight version 3.6 (three worker nodes)</span></span>

  > [!WARNING]
  > <span data-ttu-id="724a1-144">disponibilité tooguarantee de Kafka sur HDInsight, votre cluster doit contenir au moins trois nœuds de travail.</span><span class="sxs-lookup"><span data-stu-id="724a1-144">tooguarantee availability of Kafka on HDInsight, your cluster must contain at least three worker nodes.</span></span> <span data-ttu-id="724a1-145">Ce modèle crée un cluster Kafka qui contient trois nœuds Worker.</span><span class="sxs-lookup"><span data-stu-id="724a1-145">This template creates a Kafka cluster that contains three worker nodes.</span></span>

2. <span data-ttu-id="724a1-146">Hello utilisation suivant des entrées de hello toopopulate des conseils de hello **les déploiement personnalisé** panneau :</span><span class="sxs-lookup"><span data-stu-id="724a1-146">Use hello following guidance toopopulate hello entries on hello **Custom deployment** blade:</span></span>
   
    ![Déploiement HDInsight personnalisé](./media/hdinsight-apache-storm-with-kafka/parameters.png)

    * <span data-ttu-id="724a1-148">**Groupe de ressources** : créez un groupe de ressources ou sélectionnez-en un.</span><span class="sxs-lookup"><span data-stu-id="724a1-148">**Resource group**: Create a group or select an existing one.</span></span> <span data-ttu-id="724a1-149">Ce groupe contient un cluster HDInsight de hello.</span><span class="sxs-lookup"><span data-stu-id="724a1-149">This group contains hello HDInsight cluster.</span></span>
   
    * <span data-ttu-id="724a1-150">**Emplacement**: sélectionnez un tooyou géographiquement fermer d’emplacement.</span><span class="sxs-lookup"><span data-stu-id="724a1-150">**Location**: Select a location geographically close tooyou.</span></span>

    * <span data-ttu-id="724a1-151">**Nom du Cluster de base**: cette valeur est utilisée comme nom de base hello pour les clusters de Storm et Kafka hello.</span><span class="sxs-lookup"><span data-stu-id="724a1-151">**Base Cluster Name**: This value is used as hello base name for hello Storm and Kafka clusters.</span></span> <span data-ttu-id="724a1-152">Par exemple, si vous entrez **hdi**, cela crée un cluster Storm nommé **storm-hdi** et un cluster Kafka nommé **kafka-hdi**.</span><span class="sxs-lookup"><span data-stu-id="724a1-152">For example, entering **hdi** creates a Storm cluster named **storm-hdi** and a Kafka cluster named **kafka-hdi**.</span></span>
   
    * <span data-ttu-id="724a1-153">**Nom d’utilisateur de cluster**: nom d’utilisateur admin hello pour les clusters de Storm et Kafka hello.</span><span class="sxs-lookup"><span data-stu-id="724a1-153">**Cluster Login User Name**: hello admin user name for hello Storm and Kafka clusters.</span></span>
   
    * <span data-ttu-id="724a1-154">**Mot de passe de connexion cluster**: hello mot de passe administrateur pour les clusters de Storm et Kafka hello.</span><span class="sxs-lookup"><span data-stu-id="724a1-154">**Cluster Login Password**: hello admin user password for hello Storm and Kafka clusters.</span></span>
    
    * <span data-ttu-id="724a1-155">**Nom d’utilisateur SSH**: hello toocreate d’utilisateur SSH pour les clusters de Storm et Kafka hello.</span><span class="sxs-lookup"><span data-stu-id="724a1-155">**SSH User Name**: hello SSH user toocreate for hello Storm and Kafka clusters.</span></span>
    
    * <span data-ttu-id="724a1-156">**Mot de passe SSH**: mot de passe de hello pour hello SSH pour les clusters de Storm et Kafka hello.</span><span class="sxs-lookup"><span data-stu-id="724a1-156">**SSH Password**: hello password for hello SSH user for hello Storm and Kafka clusters.</span></span>

3. <span data-ttu-id="724a1-157">Hello de lecture **termes et Conditions**, puis sélectionnez **J’accepte les termes du contrat de toohello et conditions susmentionnées**.</span><span class="sxs-lookup"><span data-stu-id="724a1-157">Read hello **Terms and Conditions**, and then select **I agree toohello terms and conditions stated above**.</span></span>

4. <span data-ttu-id="724a1-158">Enfin, recherchez **code confidentiel toodashboard** , puis sélectionnez **bon**.</span><span class="sxs-lookup"><span data-stu-id="724a1-158">Finally, check **Pin toodashboard** and then select **Purchase**.</span></span> <span data-ttu-id="724a1-159">Il prend environ 20 minutes toocreate les clusters hello.</span><span class="sxs-lookup"><span data-stu-id="724a1-159">It takes about 20 minutes toocreate hello clusters.</span></span>

<span data-ttu-id="724a1-160">Une fois que les ressources hello ont été créées, panneau hello pour le groupe de ressources hello s’affiche.</span><span class="sxs-lookup"><span data-stu-id="724a1-160">Once hello resources have been created, hello blade for hello resource group is displayed.</span></span>

![Panneau des ressources de groupe de réseau virtuel de hello et des clusters](./media/hdinsight-apache-storm-with-kafka/groupblade.png)

> [!IMPORTANT]
> <span data-ttu-id="724a1-162">Notez que les noms de hello des clusters HDInsight de hello sont **storm-BASENAME** et **kafka-BASENAME**, où BASENAME est nom hello toohello modèle fourni.</span><span class="sxs-lookup"><span data-stu-id="724a1-162">Notice that hello names of hello HDInsight clusters are **storm-BASENAME** and **kafka-BASENAME**, where BASENAME is hello name you provided toohello template.</span></span> <span data-ttu-id="724a1-163">Vous utilisez ces noms dans les étapes suivantes lors de la connexion toohello clusters.</span><span class="sxs-lookup"><span data-stu-id="724a1-163">You use these names in later steps when connecting toohello clusters.</span></span>

## <a name="understanding-hello-code"></a><span data-ttu-id="724a1-164">Description du code hello</span><span class="sxs-lookup"><span data-stu-id="724a1-164">Understanding hello code</span></span>

<span data-ttu-id="724a1-165">Ce projet contient deux topologies :</span><span class="sxs-lookup"><span data-stu-id="724a1-165">This project contains two topologies:</span></span>

* <span data-ttu-id="724a1-166">**KafkaWriter**: défini par hello **writer.yaml** fichier, écrit de cette topologie tooKafka phrases aléatoire à l’aide de hello KafkaBolt fourni avec Apache Storm.</span><span class="sxs-lookup"><span data-stu-id="724a1-166">**KafkaWriter**: Defined by hello **writer.yaml** file, this topology writes random sentences tooKafka using hello KafkaBolt provided with Apache Storm.</span></span>

    <span data-ttu-id="724a1-167">Cette topologie utilise personnalisé **SentenceSpout** phrases aléatoire toogenerate de composant.</span><span class="sxs-lookup"><span data-stu-id="724a1-167">This topology uses a custom **SentenceSpout** component toogenerate random sentences.</span></span>

* <span data-ttu-id="724a1-168">**KafkaReader**: défini par hello **reader.yaml** fichier, cette topologie lit les données à partir de Kafka à l’aide de hello KafkaSpout fourni avec Apache Storm, puis journaux hello toostdout de données.</span><span class="sxs-lookup"><span data-stu-id="724a1-168">**KafkaReader**: Defined by hello **reader.yaml** file, this topology reads data from Kafka using hello KafkaSpout provided with Apache Storm, then logs hello data toostdout.</span></span>

    <span data-ttu-id="724a1-169">Cette topologie utilise stockage toodefault hello Storm HdfsBolt toowrite pour le cluster de Storm hello.</span><span class="sxs-lookup"><span data-stu-id="724a1-169">This topology uses hello Storm HdfsBolt toowrite data toodefault storage for hello Storm cluster.</span></span>
### <a name="flux"></a><span data-ttu-id="724a1-170">Flux</span><span class="sxs-lookup"><span data-stu-id="724a1-170">Flux</span></span>

<span data-ttu-id="724a1-171">topologies de Hello sont définis à l’aide de [Flux](https://storm.apache.org/releases/1.1.0/flux.html).</span><span class="sxs-lookup"><span data-stu-id="724a1-171">hello topologies are defined using [Flux](https://storm.apache.org/releases/1.1.0/flux.html).</span></span> <span data-ttu-id="724a1-172">Flux a été introduite dans renverser 0.10.x et vous permet de configuration de la topologie hello tooseparate à partir du code hello.</span><span class="sxs-lookup"><span data-stu-id="724a1-172">Flux was introduced in Storm 0.10.x and allows you tooseparate hello topology configuration from hello code.</span></span> <span data-ttu-id="724a1-173">Pour les Topologies qui utilisent l’infrastructure de Flux hello, topologie de hello est défini dans un fichier YAML.</span><span class="sxs-lookup"><span data-stu-id="724a1-173">For Topologies that use hello Flux framework, hello topology is defined in a YAML file.</span></span> <span data-ttu-id="724a1-174">fichier YAML Hello peut être inclus dans le cadre de la topologie de hello.</span><span class="sxs-lookup"><span data-stu-id="724a1-174">hello YAML file can be included as part of hello topology.</span></span> <span data-ttu-id="724a1-175">Il peut également être un fichier autonome utilisé lorsque vous soumettez une topologie de hello.</span><span class="sxs-lookup"><span data-stu-id="724a1-175">It can also be a standalone file used when you submit hello topology.</span></span> <span data-ttu-id="724a1-176">Flux prend également en charge la substitution des variables au moment de l’exécution, ce qui est utilisé dans cet exemple.</span><span class="sxs-lookup"><span data-stu-id="724a1-176">Flux also supports variable substitution at run-time, which is used in this example.</span></span>

<span data-ttu-id="724a1-177">Hello paramètres suivants sont définies au moment de l’exécution de ces topologies :</span><span class="sxs-lookup"><span data-stu-id="724a1-177">hello following parameters are set at run time for these topologies:</span></span>

* <span data-ttu-id="724a1-178">`${kafka.topic}`: nom hello Hello Kafka rubrique topologies de hello en lecture/écriture à.</span><span class="sxs-lookup"><span data-stu-id="724a1-178">`${kafka.topic}`: hello name of hello Kafka topic that hello topologies read/write to.</span></span>

* <span data-ttu-id="724a1-179">`${kafka.broker.hosts}`: hello héberge ce hello Kafka fournit s’exécutent sur.</span><span class="sxs-lookup"><span data-stu-id="724a1-179">`${kafka.broker.hosts}`: hello hosts that hello Kafka brokers run on.</span></span> <span data-ttu-id="724a1-180">informations de service broker Hello sont utilisées par hello KafkaBolt lors de l’écriture de tooKafka.</span><span class="sxs-lookup"><span data-stu-id="724a1-180">hello broker information is used by hello KafkaBolt when writing tooKafka.</span></span>

* <span data-ttu-id="724a1-181">`${kafka.zookeeper.hosts}`: hôtes hello soigneur s’exécute dans hello cluster de Kafka.</span><span class="sxs-lookup"><span data-stu-id="724a1-181">`${kafka.zookeeper.hosts}`: hello hosts that Zookeeper runs on in hello Kafka cluster.</span></span>

<span data-ttu-id="724a1-182">Pour plus d’informations sur les topologies Flux, voir la page [https://storm.apache.org/releases/1.1.0/flux.html](https://storm.apache.org/releases/1.1.0/flux.html).</span><span class="sxs-lookup"><span data-stu-id="724a1-182">For more information on Flux topologies, see [https://storm.apache.org/releases/1.1.0/flux.html](https://storm.apache.org/releases/1.1.0/flux.html).</span></span>

## <a name="download-and-compile-hello-project"></a><span data-ttu-id="724a1-183">Télécharger et compilez le projet de hello</span><span class="sxs-lookup"><span data-stu-id="724a1-183">Download and compile hello project</span></span>

1. <span data-ttu-id="724a1-184">Sur votre environnement de développement, télécharger le projet à partir de hello [https://github.com/Azure-Samples/hdinsight-storm-java-kafka](https://github.com/Azure-Samples/hdinsight-storm-java-kafka), ouvrez une ligne de commande et modifier l’emplacement de toohello répertoires que vous avez téléchargé le projet de hello.</span><span class="sxs-lookup"><span data-stu-id="724a1-184">On your development environment, download hello project from [https://github.com/Azure-Samples/hdinsight-storm-java-kafka](https://github.com/Azure-Samples/hdinsight-storm-java-kafka), open a command-line, and change directories toohello location that you downloaded hello project.</span></span>

2. <span data-ttu-id="724a1-185">À partir de hello **hdinsight-storm-java-kafka** répertoire, suivante de hello utilisation projet hello de toocompile de commande et créer un package de déploiement :</span><span class="sxs-lookup"><span data-stu-id="724a1-185">From hello **hdinsight-storm-java-kafka** directory, use hello following command toocompile hello project and create a package for deployment:</span></span>

  ```bash
  mvn clean package
  ```

    <span data-ttu-id="724a1-186">processus du package Hello crée un fichier nommé `KafkaTopology-1.0-SNAPSHOT.jar` Bonjour `target` active.</span><span class="sxs-lookup"><span data-stu-id="724a1-186">hello package process creates a file named `KafkaTopology-1.0-SNAPSHOT.jar` in hello `target` directory.</span></span>

3. <span data-ttu-id="724a1-187">Utilisez hello suivant de commandes toocopy hello package tooyour tempête de cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="724a1-187">Use hello following commands toocopy hello package tooyour Storm on HDInsight cluster.</span></span> <span data-ttu-id="724a1-188">Remplacez **nom d’utilisateur** avec le nom d’utilisateur SSH hello pour le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="724a1-188">Replace **USERNAME** with hello SSH user name for hello cluster.</span></span> <span data-ttu-id="724a1-189">Remplacez **BASENAME** avec le nom de base hello que vous avez utilisé lors de la création du cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="724a1-189">Replace **BASENAME** with hello base name you used when creating hello cluster.</span></span>

  ```bash
  scp ./target/KafkaTopology-1.0-SNAPSHOT.jar USERNAME@storm-BASENAME-ssh.azurehdinsight.net:KafkaTopology-1.0-SNAPSHOT.jar
  ```

    <span data-ttu-id="724a1-190">Lorsque vous y êtes invité, entrez le mot de passe hello utilisé lors de la création de clusters de hello.</span><span class="sxs-lookup"><span data-stu-id="724a1-190">When prompted, enter hello password you used when creating hello clusters.</span></span>

## <a name="configure-hello-topology"></a><span data-ttu-id="724a1-191">Configurer la topologie de hello</span><span class="sxs-lookup"><span data-stu-id="724a1-191">Configure hello topology</span></span>

1. <span data-ttu-id="724a1-192">Utilisez une des hello suivant les méthodes toodiscover hello hôtes de service broker Kafka :</span><span class="sxs-lookup"><span data-stu-id="724a1-192">Use one of hello following methods toodiscover hello Kafka broker hosts:</span></span>

    ```powershell
    $creds = Get-Credential -UserName "admin" -Message "Enter hello HDInsight login"
    $clusterName = Read-Host -Prompt "Enter hello Kafka cluster name"
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
    > <span data-ttu-id="724a1-193">Hello Bash exemple suppose que `$CLUSTERNAME` contient le nom hello du cluster HDInsight de hello.</span><span class="sxs-lookup"><span data-stu-id="724a1-193">hello Bash example assumes that `$CLUSTERNAME` contains hello name of hello HDInsight cluster.</span></span> <span data-ttu-id="724a1-194">Il suppose également que [jq](https://stedolan.github.io/jq/) est installé.</span><span class="sxs-lookup"><span data-stu-id="724a1-194">It also assumes that [jq](https://stedolan.github.io/jq/) is installed.</span></span> <span data-ttu-id="724a1-195">Lorsque vous y êtes invité, entrez le mot de passe de hello hello cluster compte de connexion.</span><span class="sxs-lookup"><span data-stu-id="724a1-195">When prompted, enter hello password for hello cluster login account.</span></span>

    <span data-ttu-id="724a1-196">valeur de Hello retournée est similaire toohello suivant du texte :</span><span class="sxs-lookup"><span data-stu-id="724a1-196">hello value returned is similar toohello following text:</span></span>

        wn0-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:9092,wn1-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:9092

    > [!IMPORTANT]
    > <span data-ttu-id="724a1-197">Il peut être plus de deux hôtes de service broker pour votre cluster, il est inutile tooprovide une liste complète de tous les hôtes tooclients.</span><span class="sxs-lookup"><span data-stu-id="724a1-197">While there may be more than two broker hosts for your cluster, you do not need tooprovide a full list of all hosts tooclients.</span></span> <span data-ttu-id="724a1-198">Un ou deux sont suffisants.</span><span class="sxs-lookup"><span data-stu-id="724a1-198">One or two is enough.</span></span>

2. <span data-ttu-id="724a1-199">Utilisez une des hello suivant les ordinateurs hôtes de méthodes toodiscover hello Kafka soigneur :</span><span class="sxs-lookup"><span data-stu-id="724a1-199">Use one of hello following methods toodiscover hello Kafka Zookeeper hosts:</span></span>

    ```powershell
    $creds = Get-Credential -UserName "admin" -Message "Enter hello HDInsight login"
    $clusterName = Read-Host -Prompt "Enter hello Kafka cluster name"
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
    > <span data-ttu-id="724a1-200">Hello Bash exemple suppose que `$CLUSTERNAME` contient le nom hello du cluster HDInsight de hello.</span><span class="sxs-lookup"><span data-stu-id="724a1-200">hello Bash example assumes that `$CLUSTERNAME` contains hello name of hello HDInsight cluster.</span></span> <span data-ttu-id="724a1-201">Il suppose également que [jq](https://stedolan.github.io/jq/) est installé.</span><span class="sxs-lookup"><span data-stu-id="724a1-201">It also assumes that [jq](https://stedolan.github.io/jq/) is installed.</span></span> <span data-ttu-id="724a1-202">Lorsque vous y êtes invité, entrez le mot de passe de hello hello cluster compte de connexion.</span><span class="sxs-lookup"><span data-stu-id="724a1-202">When prompted, enter hello password for hello cluster login account.</span></span>

    <span data-ttu-id="724a1-203">valeur de Hello retournée est similaire toohello suivant du texte :</span><span class="sxs-lookup"><span data-stu-id="724a1-203">hello value returned is similar toohello following text:</span></span>

        zk0-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:2181,zk2-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:2181

    > [!IMPORTANT]
    > <span data-ttu-id="724a1-204">Lorsqu’il y a plus de deux nœuds soigneur, il est inutile tooprovide une liste complète de tous les hôtes tooclients.</span><span class="sxs-lookup"><span data-stu-id="724a1-204">While there are more than two Zookeeper nodes, you do not need tooprovide a full list of all hosts tooclients.</span></span> <span data-ttu-id="724a1-205">Un ou deux sont suffisants.</span><span class="sxs-lookup"><span data-stu-id="724a1-205">One or two is enough.</span></span>

    <span data-ttu-id="724a1-206">Enregistrez cette valeur, car vous l’utiliserez plus tard.</span><span class="sxs-lookup"><span data-stu-id="724a1-206">Save this value, as it is used later.</span></span>

3. <span data-ttu-id="724a1-207">Modifier hello `dev.properties` dans fichier hello la racine du projet de hello.</span><span class="sxs-lookup"><span data-stu-id="724a1-207">Edit hello `dev.properties` file in hello root of hello project.</span></span> <span data-ttu-id="724a1-208">Ajoutez hello Broker et les lignes correspondantes de soigneur hôtes informations toohello dans ce fichier.</span><span class="sxs-lookup"><span data-stu-id="724a1-208">Add hello Broker and Zookeeper hosts information toohello matching lines in this file.</span></span> <span data-ttu-id="724a1-209">Hello suivant configuré avec les valeurs d’exemple hello des étapes précédentes de hello :</span><span class="sxs-lookup"><span data-stu-id="724a1-209">hello following example is configured using hello sample values from hello previous steps:</span></span>

        kafka.zookeeper.hosts: zk0-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:2181,zk2-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:2181
        kafka.broker.hosts: wn0-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:9092,wn1-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:9092
        kafka.topic: stormtopic

4. <span data-ttu-id="724a1-210">Enregistrer hello `dev.properties` fichier, puis utiliser hello suivant tooupload de commande de cluster de Storm toohello :</span><span class="sxs-lookup"><span data-stu-id="724a1-210">Save hello `dev.properties` file and then use hello following command tooupload it toohello Storm cluster:</span></span>

     ```bash
    scp dev.properties USERNAME@storm-BASENAME-ssh.azurehdinsight.net:KafkaTopology-1.0-SNAPSHOT.jar
    ```

    <span data-ttu-id="724a1-211">Remplacez **nom d’utilisateur** avec le nom d’utilisateur SSH hello pour le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="724a1-211">Replace **USERNAME** with hello SSH user name for hello cluster.</span></span> <span data-ttu-id="724a1-212">Remplacez **BASENAME** avec le nom de base hello que vous avez utilisé lors de la création du cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="724a1-212">Replace **BASENAME** with hello base name you used when creating hello cluster.</span></span>

## <a name="start-hello-writer"></a><span data-ttu-id="724a1-213">Démarrer l’enregistreur de hello</span><span class="sxs-lookup"><span data-stu-id="724a1-213">Start hello writer</span></span>

1. <span data-ttu-id="724a1-214">Utilisez hello suivant cluster Storm de tooconnect toohello à l’aide de SSH.</span><span class="sxs-lookup"><span data-stu-id="724a1-214">Use hello following tooconnect toohello Storm cluster using SSH.</span></span> <span data-ttu-id="724a1-215">Remplacez **nom d’utilisateur** par nom d’utilisateur SSH hello utilisé lors de la création du cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="724a1-215">Replace **USERNAME** with hello SSH user name used when creating hello cluster.</span></span> <span data-ttu-id="724a1-216">Remplacez **BASENAME** par nom de base hello utilisé lors de la création du cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="724a1-216">Replace **BASENAME** with hello base name used when creating hello cluster.</span></span>

  ```bash
  ssh USERNAME@storm-BASENAME-ssh.azurehdinsight.net
  ```

    <span data-ttu-id="724a1-217">Lorsque vous y êtes invité, entrez le mot de passe hello utilisé lors de la création de clusters de hello.</span><span class="sxs-lookup"><span data-stu-id="724a1-217">When prompted, enter hello password you used when creating hello clusters.</span></span>
   
    <span data-ttu-id="724a1-218">Pour en savoir plus, voir [Utilisation de SSH avec HDInsight (Hadoop) depuis Bash (l’interpréteur de commande) sur Windows 10, Linux, Unix ou OS X](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="724a1-218">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="724a1-219">À partir de hello connexion SSH, utilisez hello suivant commande toocreate hello rubrique Kafka utilisé par la topologie de hello :</span><span class="sxs-lookup"><span data-stu-id="724a1-219">From hello SSH connection, use hello following command toocreate hello Kafka topic used by hello topology:</span></span>

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --create --replication-factor 3 --partitions 8 --topic stormtopic --zookeeper $KAFKAZKHOSTS
    ```

    <span data-ttu-id="724a1-220">Remplacez `$KAFKAZKHOSTS` par hello soigneur héberger les informations que vous avez récupéré dans la section précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="724a1-220">Replace `$KAFKAZKHOSTS` with hello Zookeeper host information you retrieved in hello previous section.</span></span>

2. <span data-ttu-id="724a1-221">À partir de cluster de Storm toohello hello SSH connexion, utilisez hello suivant la topologie d’enregistreur commande toostart hello :</span><span class="sxs-lookup"><span data-stu-id="724a1-221">From hello SSH connection toohello Storm cluster, use hello following command toostart hello writer topology:</span></span>

    ```bash
    storm jar KafkaTopology-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /writer.yaml --filter dev.properties
    ```

    <span data-ttu-id="724a1-222">paramètres de Hello utilisés avec cette commande sont :</span><span class="sxs-lookup"><span data-stu-id="724a1-222">hello parameters used with this command are:</span></span>

    * <span data-ttu-id="724a1-223">`org.apache.storm.flux.Flux`: Utilisez des Flux tooconfigure et exécuter cette topologie.</span><span class="sxs-lookup"><span data-stu-id="724a1-223">`org.apache.storm.flux.Flux`: Use Flux tooconfigure and run this topology.</span></span>

    * <span data-ttu-id="724a1-224">`--remote`: Envoyez hello topologie tooNimbus.</span><span class="sxs-lookup"><span data-stu-id="724a1-224">`--remote`: Submit hello topology tooNimbus.</span></span> <span data-ttu-id="724a1-225">topologie de Hello est réparti entre les nœuds de cluster de hello travail de hello.</span><span class="sxs-lookup"><span data-stu-id="724a1-225">hello topology is distributed across hello worker nodes in hello cluster.</span></span>

    * <span data-ttu-id="724a1-226">`-R /writer.yaml`: Hello d’utilisation `writer.yaml` topologie de hello tooconfigure de fichiers.</span><span class="sxs-lookup"><span data-stu-id="724a1-226">`-R /writer.yaml`: Use hello `writer.yaml` file tooconfigure hello topology.</span></span> <span data-ttu-id="724a1-227">`-R`Indique que cette ressource est incluse dans le fichier jar hello.</span><span class="sxs-lookup"><span data-stu-id="724a1-227">`-R` indicates that this resource is included in hello jar file.</span></span> <span data-ttu-id="724a1-228">Il est donc dans racine hello JAR de hello, `/writer.yaml` est tooit de chemin d’accès hello.</span><span class="sxs-lookup"><span data-stu-id="724a1-228">It's in hello root of hello jar, so `/writer.yaml` is hello path tooit.</span></span>

    * <span data-ttu-id="724a1-229">`--filter`: Remplir les entrées de hello `writer.yaml` topologie à l’aide de valeurs Bonjour `dev.properties` fichier.</span><span class="sxs-lookup"><span data-stu-id="724a1-229">`--filter`: Populate entries in hello `writer.yaml` topology using values in hello `dev.properties` file.</span></span> <span data-ttu-id="724a1-230">Par exemple, hello valeur Hello `kafka.topic` entrée dans le fichier de hello est utilisé tooreplace hello `${kafka.topic}` entrée dans la définition de la topologie hello.</span><span class="sxs-lookup"><span data-stu-id="724a1-230">For example, hello value of hello `kafka.topic` entry in hello file is used tooreplace hello `${kafka.topic}` entry in hello topology definition.</span></span>

5. <span data-ttu-id="724a1-231">Une fois que la topologie de hello a démarré, utilisez hello suivant tooverify commande que qu’elle écrit des données toohello rubrique de Kafka :</span><span class="sxs-lookup"><span data-stu-id="724a1-231">Once hello topology has started, use hello following command tooverify that it is writing data toohello Kafka topic:</span></span>

  ```bash
  /usr/hdp/current/kafka-broker/bin/kafka-console-consumer.sh --zookeeper $KAFKAZKHOSTS --from-beginning --topic stormtopic
  ```

    <span data-ttu-id="724a1-232">Remplacez `$KAFKAZKHOSTS` par hello soigneur héberger les informations que vous avez récupéré dans la section précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="724a1-232">Replace `$KAFKAZKHOSTS` with hello Zookeeper host information you retrieved in hello previous section.</span></span>

    <span data-ttu-id="724a1-233">Cette commande utilise un script inclu dans la rubrique de Kafka toomonitor hello.</span><span class="sxs-lookup"><span data-stu-id="724a1-233">This command uses a script shipped with Kafka toomonitor hello topic.</span></span> <span data-ttu-id="724a1-234">Après quelques instants, il doit commence à renvoyer des phrases aléatoires qui ont été écrits toohello rubrique.</span><span class="sxs-lookup"><span data-stu-id="724a1-234">After a moment, it should start returning random sentences that have been written toohello topic.</span></span> <span data-ttu-id="724a1-235">Hello la sortie est similaire toohello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="724a1-235">hello output is similar toohello following example:</span></span>

        i am at two with nature             
        an apple a day keeps hello doctor away
        snow white and hello seven dwarfs     
        hello cow jumped over hello moon        
        an apple a day keeps hello doctor away
        an apple a day keeps hello doctor away
        hello cow jumped over hello moon        
        an apple a day keeps hello doctor away
        an apple a day keeps hello doctor away
        four score and seven years ago      
        snow white and hello seven dwarfs     
        snow white and hello seven dwarfs     
        i am at two with nature             
        an apple a day keeps hello doctor away

    <span data-ttu-id="724a1-236">Utilisez Ctrl + script de hello toostop c.</span><span class="sxs-lookup"><span data-stu-id="724a1-236">Use Ctrl+c toostop hello script.</span></span>

## <a name="start-hello-reader"></a><span data-ttu-id="724a1-237">Démarrer le lecteur de hello</span><span class="sxs-lookup"><span data-stu-id="724a1-237">Start hello reader</span></span>

1. <span data-ttu-id="724a1-238">À partir de cluster de Storm toohello hello SSH session, utilisez hello suivant la topologie du lecteur de commande toostart hello :</span><span class="sxs-lookup"><span data-stu-id="724a1-238">From hello SSH session toohello Storm cluster, use hello following command toostart hello reader topology:</span></span>

  ```bash
  storm jar KafkaTopology-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /reader.yaml --filter dev.properties
  ```

2. <span data-ttu-id="724a1-239">Une fois que la topologie de hello démarre, ouvrez hello Storm UI.</span><span class="sxs-lookup"><span data-stu-id="724a1-239">Once hello topology starts, open hello Storm UI.</span></span> <span data-ttu-id="724a1-240">Cette interface utilisateur web est située dans https://storm-BASENAME.azurehdinsight.net/stormui.</span><span class="sxs-lookup"><span data-stu-id="724a1-240">This web UI is located at https://storm-BASENAME.azurehdinsight.net/stormui.</span></span> <span data-ttu-id="724a1-241">Remplacez __BASENAME__ par nom de base hello utilisé lors de la création de cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="724a1-241">Replace __BASENAME__ with hello base name used when hello cluster was created.</span></span> 

    <span data-ttu-id="724a1-242">Lorsque vous y êtes invité, utilisez le nom de connexion d’administrateur hello (valeur par défaut, `admin`) et le mot de passe utilisé lors de la création de cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="724a1-242">When prompted, use hello admin login name (default, `admin`) and password used when hello cluster was created.</span></span> <span data-ttu-id="724a1-243">Vous voyez un toohello similaire de page web suivant image :</span><span class="sxs-lookup"><span data-stu-id="724a1-243">You see a web page similar toohello following image:</span></span>

    ![Interface utilisateur de Storm](./media/hdinsight-apache-storm-with-kafka/stormui.png)

3. <span data-ttu-id="724a1-245">À partir de l’interface utilisateur tempête de hello, sélectionnez hello __kafka-lecteur__ lien Bonjour __récapitulatif de la topologie__ section toodisplay informations hello __kafka-lecteur__ topologie.</span><span class="sxs-lookup"><span data-stu-id="724a1-245">From hello Storm UI, select hello __kafka-reader__ link in hello __Topology Summary__ section toodisplay information about hello __kafka-reader__ topology.</span></span>

    ![Section de résumé de topologie de l’interface utilisateur web de Storm hello](./media/hdinsight-apache-storm-with-kafka/topology-summary.png)

4. <span data-ttu-id="724a1-247">toodisplay plus d’informations sur les instances du composant de journal-éclair hello, sélectionnez hello hello __éclair de l’enregistreur d’événements__ lien Bonjour __boulons (tout temps)__ section.</span><span class="sxs-lookup"><span data-stu-id="724a1-247">toodisplay information about hello instances of hello logger-bolt component, select hello __logger-bolt__ link in hello __Bolts (All time)__ section.</span></span>

    ![Lien d’éclair de l’enregistreur d’événements dans la section de boulons hello](./media/hdinsight-apache-storm-with-kafka/bolts.png)

5. <span data-ttu-id="724a1-249">Bonjour __exécuteurs__ , sélectionnez un lien dans hello __Port__ les informations de journalisation toodisplay de colonne sur cette instance du composant de hello.</span><span class="sxs-lookup"><span data-stu-id="724a1-249">In hello __Executors__ section, select a link in hello __Port__ column toodisplay logging information about this instance of hello component.</span></span>

    ![Exécuteurs de lien](./media/hdinsight-apache-storm-with-kafka/executors.png)

    <span data-ttu-id="724a1-251">journal de Hello contient un journal des données de hello lues à partir de la rubrique de Kafka de hello.</span><span class="sxs-lookup"><span data-stu-id="724a1-251">hello log contains a log of hello data read from hello Kafka topic.</span></span> <span data-ttu-id="724a1-252">informations Hello dans le journal de hello sont similaire toohello suivant du texte :</span><span class="sxs-lookup"><span data-stu-id="724a1-252">hello information in hello log is similar toohello following text:</span></span>

        2016-11-04 17:47:14.907 c.m.e.LoggerBolt [INFO] Received data: four score and seven years ago
        2016-11-04 17:47:14.907 STDIO [INFO] hello cow jumped over hello moon
        2016-11-04 17:47:14.908 c.m.e.LoggerBolt [INFO] Received data: hello cow jumped over hello moon
        2016-11-04 17:47:14.911 STDIO [INFO] snow white and hello seven dwarfs
        2016-11-04 17:47:14.911 c.m.e.LoggerBolt [INFO] Received data: snow white and hello seven dwarfs
        2016-11-04 17:47:14.932 STDIO [INFO] snow white and hello seven dwarfs
        2016-11-04 17:47:14.932 c.m.e.LoggerBolt [INFO] Received data: snow white and hello seven dwarfs
        2016-11-04 17:47:14.969 STDIO [INFO] an apple a day keeps hello doctor away
        2016-11-04 17:47:14.970 c.m.e.LoggerBolt [INFO] Received data: an apple a day keeps hello doctor away

## <a name="stop-hello-topologies"></a><span data-ttu-id="724a1-253">Arrêter les topologies hello</span><span class="sxs-lookup"><span data-stu-id="724a1-253">Stop hello topologies</span></span>

<span data-ttu-id="724a1-254">À partir d’un cluster Storm SSH session toohello, utilisez hello suivant des topologies de commandes toostop hello Storm :</span><span class="sxs-lookup"><span data-stu-id="724a1-254">From an SSH session toohello Storm cluster, use hello following commands toostop hello Storm topologies:</span></span>

  ```bash
  storm kill kafka-writer
  storm kill kafka-reader
  ```

## <a name="delete-hello-cluster"></a><span data-ttu-id="724a1-255">Supprimer le cluster de hello</span><span class="sxs-lookup"><span data-stu-id="724a1-255">Delete hello cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="724a1-256">Étant donné que les étapes de hello dans ce document vous allez créer deux clusters dans hello même groupe de ressources Azure, vous pouvez supprimer le groupe de ressources hello Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="724a1-256">Since hello steps in this document create both clusters in hello same Azure resource group, you can delete hello resource group in hello Azure portal.</span></span> <span data-ttu-id="724a1-257">Groupe de ressources hello suppression supprime toutes les ressources créées en suivant ce document.</span><span class="sxs-lookup"><span data-stu-id="724a1-257">Deleting hello resource group removes all resources created by following this document.</span></span>

## <a name="next-steps"></a><span data-ttu-id="724a1-258">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="724a1-258">Next steps</span></span>

<span data-ttu-id="724a1-259">Pour plus d’exemples de topologies qui peuvent être utilisées avec Storm sur HDInsight, consultez [Exemples de topologies et composants Storm](hdinsight-storm-example-topology.md).</span><span class="sxs-lookup"><span data-stu-id="724a1-259">For more example topologies that can be used with Storm on HDInsight, see [Example Storm topologies and components](hdinsight-storm-example-topology.md).</span></span>

<span data-ttu-id="724a1-260">Pour plus d’informations sur le déploiement et la surveillance des topologies sur HDInsight Linux, consultez [Déploiement et gestion des topologies Apache Storm sur HDInsight Linux](hdinsight-storm-deploy-monitor-topology-linux.md)</span><span class="sxs-lookup"><span data-stu-id="724a1-260">For information on deploying and monitoring topologies on Linux-based HDInsight, see [Deploy and manage Apache Storm topologies on Linux-based HDInsight](hdinsight-storm-deploy-monitor-topology-linux.md)</span></span>