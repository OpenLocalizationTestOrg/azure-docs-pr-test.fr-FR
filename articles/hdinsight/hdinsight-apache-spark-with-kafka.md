---
title: aaaApache Spark diffusion en continu avec Kafka - Azure HDInsight | Documents Microsoft
description: "Découvrez comment toouse Spark Apache Spark toostream de données dans ou hors Kafka Apache à l’aide de DStreams. Dans cet exemple, vous diffusez des données à l’aide d’un bloc-notes Jupyter à partir de Spark sur HDInsight."
keywords: exemple kafka, zookeeper kafka, kafka de diffusion spark, exemple kafka de diffusion spark
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: dd8f53c1-bdee-4921-b683-3be4c46c2039
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: 
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/13/2017
ms.author: larryfr
ms.openlocfilehash: f48b37aadafa4979cd27af68e8417db6acc8a0e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="apache-spark-streaming-dstream-example-with-kafka-preview-on-hdinsight"></a><span data-ttu-id="645f3-105">Exemple Apache Spark Streaming (DStream) avec Kafka (aperçu) sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="645f3-105">Apache Spark streaming (DStream) example with Kafka (preview) on HDInsight</span></span>

<span data-ttu-id="645f3-106">Découvrez comment toouse Spark Apache Spark toostream de données dans ou hors Kafka Apache sur HDInsight à l’aide de DStreams.</span><span class="sxs-lookup"><span data-stu-id="645f3-106">Learn how toouse Spark Apache Spark toostream data into or out of Apache Kafka on HDInsight using DStreams.</span></span> <span data-ttu-id="645f3-107">Cet exemple utilise un bloc-notes jupyter qui s’exécute sur un cluster de Spark hello.</span><span class="sxs-lookup"><span data-stu-id="645f3-107">This example uses a Jupyter notebook that runs on hello Spark cluster.</span></span>
> [!NOTE]
> <span data-ttu-id="645f3-108">étapes Hello dans ce document créent un groupe de ressources Azure qui contient à la fois un Spark sur HDInsight et un Kafka sur le cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="645f3-108">hello steps in this document create an Azure resource group that contains both a Spark on HDInsight and a Kafka on HDInsight cluster.</span></span> <span data-ttu-id="645f3-109">Ces clusters sont situés dans un réseau virtuel Azure, ce qui permet de hello toodirectly de cluster Spark communiquent avec hello cluster de Kafka.</span><span class="sxs-lookup"><span data-stu-id="645f3-109">These clusters are both located within an Azure Virtual Network, which allows hello Spark cluster toodirectly communicate with hello Kafka cluster.</span></span>
>
> <span data-ttu-id="645f3-110">Lorsque vous avez terminé les étapes hello dans ce document, n’oubliez pas de frais supplémentaires de toodelete hello clusters tooavoid.</span><span class="sxs-lookup"><span data-stu-id="645f3-110">When you are done with hello steps in this document, remember toodelete hello clusters tooavoid excess charges.</span></span>

## <a name="create-hello-clusters"></a><span data-ttu-id="645f3-111">Créer des clusters de hello</span><span class="sxs-lookup"><span data-stu-id="645f3-111">Create hello clusters</span></span>

<span data-ttu-id="645f3-112">Kafka Apache sur HDInsight ne fournit pas d’accès toohello Kafka courtiers sur hello internet public.</span><span class="sxs-lookup"><span data-stu-id="645f3-112">Apache Kafka on HDInsight does not provide access toohello Kafka brokers over hello public internet.</span></span> <span data-ttu-id="645f3-113">Tout ce qui tooKafka doit se trouver dans des entretiens hello même réseau virtuel Azure en tant que nœuds hello dans hello cluster de Kafka.</span><span class="sxs-lookup"><span data-stu-id="645f3-113">Anything that talks tooKafka must be in hello same Azure virtual network as hello nodes in hello Kafka cluster.</span></span> <span data-ttu-id="645f3-114">Pour cet exemple, hello Kafka et les clusters Spark se trouvent dans un réseau virtuel Azure.</span><span class="sxs-lookup"><span data-stu-id="645f3-114">For this example, both hello Kafka and Spark clusters are located in an Azure virtual network.</span></span> <span data-ttu-id="645f3-115">Hello diagramme suivant illustre le flux de communication entre les clusters hello :</span><span class="sxs-lookup"><span data-stu-id="645f3-115">hello following diagram shows how communication flows between hello clusters:</span></span>

![Diagramme des clusters Spark et Kafka dans un réseau virtuel Azure](./media/hdinsight-apache-spark-with-kafka/spark-kafka-vnet.png)

> [!NOTE]
> <span data-ttu-id="645f3-117">Bien que Kafka proprement dit est limitée toocommunication au sein du réseau virtuel de hello, autres services sur un cluster de hello hello tels que SSH et Ambari est accessible via internet.</span><span class="sxs-lookup"><span data-stu-id="645f3-117">Though Kafka itself is limited toocommunication within hello virtual network, other services on hello cluster such as SSH and Ambari can be accessed over hello internet.</span></span> <span data-ttu-id="645f3-118">Pour plus d’informations sur les ports publics de hello disponibles avec HDInsight, consultez [Ports et URI utilisé par HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span><span class="sxs-lookup"><span data-stu-id="645f3-118">For more information on hello public ports available with HDInsight, see [Ports and URIs used by HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span></span>

<span data-ttu-id="645f3-119">Si vous pouvez créer un réseau virtuel Azure, Kafka et Spark clusters manuellement, il est plus facile toouse un modèle Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="645f3-119">While you can create an Azure virtual network, Kafka, and Spark clusters manually, it's easier toouse an Azure Resource Manager template.</span></span> <span data-ttu-id="645f3-120">Toodeploy un réseau virtuel Azure, Kafka, les étapes suivantes de hello utilisation et Spark clusters tooyour abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="645f3-120">Use hello following steps toodeploy an Azure virtual network, Kafka, and Spark clusters tooyour Azure subscription.</span></span>

1. <span data-ttu-id="645f3-121">Utilisez hello suivant toosign bouton dans tooAzure et modèle ouvert hello Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="645f3-121">Use hello following button toosign in tooAzure and open hello template in hello Azure portal.</span></span>
    
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-kafka-spark-cluster-in-vnet-v2.1.json" target="_blank"><img src="./media/hdinsight-apache-spark-with-kafka/deploy-to-azure.png" alt="Deploy tooAzure"></a>
    
    <span data-ttu-id="645f3-122">Hello modèle Azure Resource Manager se trouve dans **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-spark-cluster-in-vnet-v2.1.json**.</span><span class="sxs-lookup"><span data-stu-id="645f3-122">hello Azure Resource Manager template is located at **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-spark-cluster-in-vnet-v2.1.json**.</span></span>

    > [!WARNING]
    > <span data-ttu-id="645f3-123">disponibilité tooguarantee de Kafka sur HDInsight, votre cluster doit contenir au moins trois nœuds de travail.</span><span class="sxs-lookup"><span data-stu-id="645f3-123">tooguarantee availability of Kafka on HDInsight, your cluster must contain at least three worker nodes.</span></span> <span data-ttu-id="645f3-124">Ce modèle crée un cluster Kafka qui contient trois nœuds Worker.</span><span class="sxs-lookup"><span data-stu-id="645f3-124">This template creates a Kafka cluster that contains three worker nodes.</span></span>

    <span data-ttu-id="645f3-125">Ce modèle crée un cluster HDInsight 3.6 pour Kafka et Spark.</span><span class="sxs-lookup"><span data-stu-id="645f3-125">This template creates an HDInsight 3.6 cluster for both Kafka and Spark.</span></span>

2. <span data-ttu-id="645f3-126">Hello utilisation suivant des entrées d’information toopopulate hello de hello **les déploiement personnalisé** panneau :</span><span class="sxs-lookup"><span data-stu-id="645f3-126">Use hello following information toopopulate hello entries on hello **Custom deployment** blade:</span></span>
   
    ![Déploiement HDInsight personnalisé](./media/hdinsight-apache-spark-with-kafka/parameters.png)
   
    * <span data-ttu-id="645f3-128">**Groupe de ressources** : créez un groupe de ressources ou sélectionnez-en un.</span><span class="sxs-lookup"><span data-stu-id="645f3-128">**Resource group**: Create a group or select an existing one.</span></span> <span data-ttu-id="645f3-129">Ce groupe contient un cluster HDInsight de hello.</span><span class="sxs-lookup"><span data-stu-id="645f3-129">This group contains hello HDInsight cluster.</span></span>

    * <span data-ttu-id="645f3-130">**Emplacement**: sélectionnez un tooyou géographiquement fermer d’emplacement.</span><span class="sxs-lookup"><span data-stu-id="645f3-130">**Location**: Select a location geographically close tooyou.</span></span>

    * <span data-ttu-id="645f3-131">**Nom du Cluster de base**: cette valeur est utilisée comme nom de base hello pour les clusters de Spark et Kafka hello.</span><span class="sxs-lookup"><span data-stu-id="645f3-131">**Base Cluster Name**: This value is used as hello base name for hello Spark and Kafka clusters.</span></span> <span data-ttu-id="645f3-132">Par exemple, si vous entrez **hdi**, cela crée un cluster Spark nommé spark-hdi__ et un cluster Kafka nommé **kafka-hdi**.</span><span class="sxs-lookup"><span data-stu-id="645f3-132">For example, entering **hdi** creates a Spark cluster named spark-hdi__ and a Kafka cluster named **kafka-hdi**.</span></span>

    * <span data-ttu-id="645f3-133">**Nom d’utilisateur de cluster**: nom d’utilisateur admin hello pour les clusters de Spark et Kafka hello.</span><span class="sxs-lookup"><span data-stu-id="645f3-133">**Cluster Login User Name**: hello admin user name for hello Spark and Kafka clusters.</span></span>

    * <span data-ttu-id="645f3-134">**Mot de passe de connexion cluster**: hello mot de passe administrateur pour les clusters de Spark et Kafka hello.</span><span class="sxs-lookup"><span data-stu-id="645f3-134">**Cluster Login Password**: hello admin user password for hello Spark and Kafka clusters.</span></span>

    * <span data-ttu-id="645f3-135">**Nom d’utilisateur SSH**: hello toocreate d’utilisateur SSH pour les clusters de Spark et Kafka hello.</span><span class="sxs-lookup"><span data-stu-id="645f3-135">**SSH User Name**: hello SSH user toocreate for hello Spark and Kafka clusters.</span></span>

    * <span data-ttu-id="645f3-136">**Mot de passe SSH**: mot de passe de hello pour hello SSH pour les clusters de Spark et Kafka hello.</span><span class="sxs-lookup"><span data-stu-id="645f3-136">**SSH Password**: hello password for hello SSH user for hello Spark and Kafka clusters.</span></span>

3. <span data-ttu-id="645f3-137">Hello de lecture **termes et Conditions**, puis sélectionnez **J’accepte les termes du contrat de toohello et conditions susmentionnées**.</span><span class="sxs-lookup"><span data-stu-id="645f3-137">Read hello **Terms and Conditions**, and then select **I agree toohello terms and conditions stated above**.</span></span>

4. <span data-ttu-id="645f3-138">Enfin, recherchez **code confidentiel toodashboard** , puis sélectionnez **bon**.</span><span class="sxs-lookup"><span data-stu-id="645f3-138">Finally, check **Pin toodashboard** and then select **Purchase**.</span></span> <span data-ttu-id="645f3-139">Il prend environ 20 minutes toocreate les clusters hello.</span><span class="sxs-lookup"><span data-stu-id="645f3-139">It takes about 20 minutes toocreate hello clusters.</span></span>

<span data-ttu-id="645f3-140">Une fois que les ressources hello ont été créées, vous êtes panneau tooa redirigé hello groupe de ressources qui contient des clusters de hello et tableau de bord web.</span><span class="sxs-lookup"><span data-stu-id="645f3-140">Once hello resources have been created, you are redirected tooa blade for hello resource group that contains hello clusters and web dashboard.</span></span>

![Panneau des ressources de groupe de réseau virtuel de hello et des clusters](./media/hdinsight-apache-spark-with-kafka/groupblade.png)

> [!IMPORTANT]
> <span data-ttu-id="645f3-142">Notez que les noms de hello des clusters HDInsight de hello sont **spark-BASENAME** et **kafka-BASENAME**, où BASENAME est nom hello toohello modèle fourni.</span><span class="sxs-lookup"><span data-stu-id="645f3-142">Notice that hello names of hello HDInsight clusters are **spark-BASENAME** and **kafka-BASENAME**, where BASENAME is hello name you provided toohello template.</span></span> <span data-ttu-id="645f3-143">Vous utilisez ces noms dans les étapes suivantes lors de la connexion toohello clusters.</span><span class="sxs-lookup"><span data-stu-id="645f3-143">You use these names in later steps when connecting toohello clusters.</span></span>

## <a name="use-hello-notebooks"></a><span data-ttu-id="645f3-144">Utilisez les blocs-notes hello</span><span class="sxs-lookup"><span data-stu-id="645f3-144">Use hello notebooks</span></span>

<span data-ttu-id="645f3-145">code Hello pour exemple hello décrite dans ce document est disponible à l’adresse [https://github.com/Azure-Samples/hdinsight-spark-scala-kafka](https://github.com/Azure-Samples/hdinsight-spark-scala-kafka).</span><span class="sxs-lookup"><span data-stu-id="645f3-145">hello code for hello example described in this document is available at [https://github.com/Azure-Samples/hdinsight-spark-scala-kafka](https://github.com/Azure-Samples/hdinsight-spark-scala-kafka).</span></span>

<span data-ttu-id="645f3-146">Suivez les étapes de hello Bonjour `README.md` toocomplete de fichiers de cet exemple.</span><span class="sxs-lookup"><span data-stu-id="645f3-146">Follow hello steps in hello `README.md` file toocomplete this example.</span></span>

## <a name="delete-hello-cluster"></a><span data-ttu-id="645f3-147">Supprimer le cluster de hello</span><span class="sxs-lookup"><span data-stu-id="645f3-147">Delete hello cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="645f3-148">Étant donné que les étapes de hello dans ce document vous allez créer deux clusters dans hello même groupe de ressources Azure, vous pouvez supprimer le groupe de ressources hello Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="645f3-148">Since hello steps in this document create both clusters in hello same Azure resource group, you can delete hello resource group in hello Azure portal.</span></span> <span data-ttu-id="645f3-149">Suppression du groupe hello supprime toutes les ressources créées en suivant ce document, hello réseau virtuel Azure et compte de stockage utilisé par les clusters de hello.</span><span class="sxs-lookup"><span data-stu-id="645f3-149">Deleting hello group removes all resources created by following this document, hello Azure Virtual Network, and storage account used by hello clusters.</span></span>

## <a name="next-steps"></a><span data-ttu-id="645f3-150">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="645f3-150">Next steps</span></span>

<span data-ttu-id="645f3-151">Dans cet exemple, vous avez appris comment toouse nouvelles tooread et tooKafka d’écriture.</span><span class="sxs-lookup"><span data-stu-id="645f3-151">In this example, you learned how toouse Spark tooread and write tooKafka.</span></span> <span data-ttu-id="645f3-152">Utilisez des autres façons toowork hello suivant les liens toodiscover avec Kafka :</span><span class="sxs-lookup"><span data-stu-id="645f3-152">Use hello following links toodiscover other ways toowork with Kafka:</span></span>

* [<span data-ttu-id="645f3-153">Prise en main d’Apache Kafka sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="645f3-153">Get started with Apache Kafka on HDInsight</span></span>](hdinsight-apache-kafka-get-started.md)
* [<span data-ttu-id="645f3-154">Utilisez MirrorMaker toocreate un réplica de Kafka sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="645f3-154">Use MirrorMaker toocreate a replica of Kafka on HDInsight</span></span>](hdinsight-apache-kafka-mirroring.md)
* [<span data-ttu-id="645f3-155">Utilisation d’Apache Storm avec Kafka sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="645f3-155">Use Apache Storm with Kafka on HDInsight</span></span>](hdinsight-apache-storm-with-kafka.md)

