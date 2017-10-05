---
title: Utiliser une diffusion en continu Apache Spark avec Kafka - Azure HDInsight | Documents Microsoft
description: "Découvrez comment utiliser Apache Spark pour diffuser des données vers ou depuis Apache Kafka à l’aide de DStreams. Dans cet exemple, vous diffusez des données à l’aide d’un bloc-notes Jupyter à partir de Spark sur HDInsight."
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
ms.openlocfilehash: 81fa319f6fb94bdabacd8f68d14b9a1063a9749a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="apache-spark-streaming-dstream-example-with-kafka-preview-on-hdinsight"></a><span data-ttu-id="79af0-105">Exemple Apache Spark Streaming (DStream) avec Kafka (aperçu) sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="79af0-105">Apache Spark streaming (DStream) example with Kafka (preview) on HDInsight</span></span>

<span data-ttu-id="79af0-106">Découvrez comment utiliser Apache Spark pour diffuser des données vers ou depuis Apache Kafka à l’aide de DStreams.</span><span class="sxs-lookup"><span data-stu-id="79af0-106">Learn how to use Spark Apache Spark to stream data into or out of Apache Kafka on HDInsight using DStreams.</span></span> <span data-ttu-id="79af0-107">Cet exemple utilise un bloc-notes jupyter qui s’exécute sur le cluster Spark.</span><span class="sxs-lookup"><span data-stu-id="79af0-107">This example uses a Jupyter notebook that runs on the Spark cluster.</span></span>
> [!NOTE]
> <span data-ttu-id="79af0-108">Les étapes décrites dans ce document créent un groupe de ressources Azure qui contient à la fois un Spark sur HDInsight et un Kafka sur un cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="79af0-108">The steps in this document create an Azure resource group that contains both a Spark on HDInsight and a Kafka on HDInsight cluster.</span></span> <span data-ttu-id="79af0-109">Ces clusters sont tous deux situés dans un réseau virtuel Azure, ce qui permet au cluster Spark de communiquer directement avec le cluster Kafka.</span><span class="sxs-lookup"><span data-stu-id="79af0-109">These clusters are both located within an Azure Virtual Network, which allows the Spark cluster to directly communicate with the Kafka cluster.</span></span>
>
> <span data-ttu-id="79af0-110">Lorsque vous avez terminé les étapes décrites dans ce document, n’oubliez pas de supprimer les clusters pour éviter les frais supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="79af0-110">When you are done with the steps in this document, remember to delete the clusters to avoid excess charges.</span></span>

## <a name="create-the-clusters"></a><span data-ttu-id="79af0-111">Création des clusters</span><span class="sxs-lookup"><span data-stu-id="79af0-111">Create the clusters</span></span>

<span data-ttu-id="79af0-112">Apache Kafka sur HDInsight ne donne pas accès aux répartiteurs Kafka via l’internet public.</span><span class="sxs-lookup"><span data-stu-id="79af0-112">Apache Kafka on HDInsight does not provide access to the Kafka brokers over the public internet.</span></span> <span data-ttu-id="79af0-113">Tout ce qui communique avec Kafka doit se trouver sur le même réseau virtuel Azure que les nœuds du cluster Kafka.</span><span class="sxs-lookup"><span data-stu-id="79af0-113">Anything that talks to Kafka must be in the same Azure virtual network as the nodes in the Kafka cluster.</span></span> <span data-ttu-id="79af0-114">Pour cet exemple, les clusters Kafka et Spark sont situés dans un réseau virtuel Azure.</span><span class="sxs-lookup"><span data-stu-id="79af0-114">For this example, both the Kafka and Spark clusters are located in an Azure virtual network.</span></span> <span data-ttu-id="79af0-115">Le diagramme suivant illustre le flux de communication entre les clusters :</span><span class="sxs-lookup"><span data-stu-id="79af0-115">The following diagram shows how communication flows between the clusters:</span></span>

![Diagramme des clusters Spark et Kafka dans un réseau virtuel Azure](./media/hdinsight-apache-spark-with-kafka/spark-kafka-vnet.png)

> [!NOTE]
> <span data-ttu-id="79af0-117">Bien que Kafka soit lui-même limité à la communication au sein du réseau virtuel, d’autres services sur le cluster comme SSH et Ambari sont accessibles sur Internet.</span><span class="sxs-lookup"><span data-stu-id="79af0-117">Though Kafka itself is limited to communication within the virtual network, other services on the cluster such as SSH and Ambari can be accessed over the internet.</span></span> <span data-ttu-id="79af0-118">Pour plus d’informations sur les ports publics disponibles avec HDInsight, consultez [Ports et URI utilisés par HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span><span class="sxs-lookup"><span data-stu-id="79af0-118">For more information on the public ports available with HDInsight, see [Ports and URIs used by HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span></span>

<span data-ttu-id="79af0-119">Même si vous pouvez créer un réseau virtuel Azure, et des clusters Kafka et Spark manuellement, il est plus facile d’utiliser un modèle Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="79af0-119">While you can create an Azure virtual network, Kafka, and Spark clusters manually, it's easier to use an Azure Resource Manager template.</span></span> <span data-ttu-id="79af0-120">Utilisez les étapes suivantes pour déployer un réseau virtuel Azure et des clusters Kafka et Spark sur votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="79af0-120">Use the following steps to deploy an Azure virtual network, Kafka, and Spark clusters to your Azure subscription.</span></span>

1. <span data-ttu-id="79af0-121">Utilisez le bouton suivant pour vous connecter à Azure et ouvrir le modèle dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="79af0-121">Use the following button to sign in to Azure and open the template in the Azure portal.</span></span>
    
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-kafka-spark-cluster-in-vnet-v2.1.json" target="_blank"><img src="./media/hdinsight-apache-spark-with-kafka/deploy-to-azure.png" alt="Deploy to Azure"></a>
    
    <span data-ttu-id="79af0-122">Le modèle Azure Resource Manager se trouve à l’adresse **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-spark-cluster-in-vnet-v2.1.json**.</span><span class="sxs-lookup"><span data-stu-id="79af0-122">The Azure Resource Manager template is located at **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-spark-cluster-in-vnet-v2.1.json**.</span></span>

    > [!WARNING]
    > <span data-ttu-id="79af0-123">Pour garantir la disponibilité de Kafka sur HDInsight, votre cluster doit contenir au moins trois nœuds Worker.</span><span class="sxs-lookup"><span data-stu-id="79af0-123">To guarantee availability of Kafka on HDInsight, your cluster must contain at least three worker nodes.</span></span> <span data-ttu-id="79af0-124">Ce modèle crée un cluster Kafka qui contient trois nœuds de travail.</span><span class="sxs-lookup"><span data-stu-id="79af0-124">This template creates a Kafka cluster that contains three worker nodes.</span></span>

    <span data-ttu-id="79af0-125">Ce modèle crée un cluster HDInsight 3.6 pour Kafka et Spark.</span><span class="sxs-lookup"><span data-stu-id="79af0-125">This template creates an HDInsight 3.6 cluster for both Kafka and Spark.</span></span>

2. <span data-ttu-id="79af0-126">Utilisez les informations suivantes pour remplir les entrées sur le panneau **déploiement personnalisé** :</span><span class="sxs-lookup"><span data-stu-id="79af0-126">Use the following information to populate the entries on the **Custom deployment** blade:</span></span>
   
    ![Déploiement HDInsight personnalisé](./media/hdinsight-apache-spark-with-kafka/parameters.png)
   
    * <span data-ttu-id="79af0-128">**Groupe de ressources** : créez un groupe de ressources ou sélectionnez-en un.</span><span class="sxs-lookup"><span data-stu-id="79af0-128">**Resource group**: Create a group or select an existing one.</span></span> <span data-ttu-id="79af0-129">Ce groupe contient le cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="79af0-129">This group contains the HDInsight cluster.</span></span>

    * <span data-ttu-id="79af0-130">**Emplacement** : choisissez un emplacement proche de vous géographiquement.</span><span class="sxs-lookup"><span data-stu-id="79af0-130">**Location**: Select a location geographically close to you.</span></span>

    * <span data-ttu-id="79af0-131">**Nom de cluster de base** : cette valeur sera utilisée comme nom de base pour les clusters Spark et Kafka.</span><span class="sxs-lookup"><span data-stu-id="79af0-131">**Base Cluster Name**: This value is used as the base name for the Spark and Kafka clusters.</span></span> <span data-ttu-id="79af0-132">Par exemple, si vous entrez **hdi**, cela crée un cluster Spark nommé spark-hdi__ et un cluster Kafka nommé **kafka-hdi**.</span><span class="sxs-lookup"><span data-stu-id="79af0-132">For example, entering **hdi** creates a Spark cluster named spark-hdi__ and a Kafka cluster named **kafka-hdi**.</span></span>

    * <span data-ttu-id="79af0-133">**Nom d’utilisateur du cluster** : nom utilisateur Admin pour les clusters Spark et Kafka.</span><span class="sxs-lookup"><span data-stu-id="79af0-133">**Cluster Login User Name**: The admin user name for the Spark and Kafka clusters.</span></span>

    * <span data-ttu-id="79af0-134">**Mot de passe du cluster** : mot de passe utilisateur Admin pour les clusters Spark et Kafka.</span><span class="sxs-lookup"><span data-stu-id="79af0-134">**Cluster Login Password**: The admin user password for the Spark and Kafka clusters.</span></span>

    * <span data-ttu-id="79af0-135">**Nom d’utilisateur SSH** : utilisateur SSH permettant de créer des clusters Spark et Kafka.</span><span class="sxs-lookup"><span data-stu-id="79af0-135">**SSH User Name**: The SSH user to create for the Spark and Kafka clusters.</span></span>

    * <span data-ttu-id="79af0-136">**Mot de passe SSH** : mot de passe de l’utilisateur SSH pour les clusters Spark et Kafka.</span><span class="sxs-lookup"><span data-stu-id="79af0-136">**SSH Password**: The password for the SSH user for the Spark and Kafka clusters.</span></span>

3. <span data-ttu-id="79af0-137">Passez en revue les **termes et conditions**, puis cochez la case **J’accepte les termes et conditions mentionnés ci-dessus**.</span><span class="sxs-lookup"><span data-stu-id="79af0-137">Read the **Terms and Conditions**, and then select **I agree to the terms and conditions stated above**.</span></span>

4. <span data-ttu-id="79af0-138">Pour finir, cochez **Épingler au tableau de bord**, puis sélectionnez **Acheter**.</span><span class="sxs-lookup"><span data-stu-id="79af0-138">Finally, check **Pin to dashboard** and then select **Purchase**.</span></span> <span data-ttu-id="79af0-139">La création des clusters prend environ 20 minutes.</span><span class="sxs-lookup"><span data-stu-id="79af0-139">It takes about 20 minutes to create the clusters.</span></span>

<span data-ttu-id="79af0-140">Une fois les ressources créées, vous êtes redirigé vers un panneau pour le groupe de ressources contenant les clusters et le tableau de bord Web.</span><span class="sxs-lookup"><span data-stu-id="79af0-140">Once the resources have been created, you are redirected to a blade for the resource group that contains the clusters and web dashboard.</span></span>

![Volet du groupe de ressources pour les clusters et le réseau virtuel](./media/hdinsight-apache-spark-with-kafka/groupblade.png)

> [!IMPORTANT]
> <span data-ttu-id="79af0-142">Les noms des clusters HDInsight sont **spark-BASENAME** et **kafka-BASENAME**, où BASENAME est le nom que vous avez fourni pour le modèle.</span><span class="sxs-lookup"><span data-stu-id="79af0-142">Notice that the names of the HDInsight clusters are **spark-BASENAME** and **kafka-BASENAME**, where BASENAME is the name you provided to the template.</span></span> <span data-ttu-id="79af0-143">Vous utilisez ces noms dans les étapes ultérieures, lors de la connexion aux clusters.</span><span class="sxs-lookup"><span data-stu-id="79af0-143">You use these names in later steps when connecting to the clusters.</span></span>

## <a name="use-the-notebooks"></a><span data-ttu-id="79af0-144">Obtenir les blocs-notes</span><span class="sxs-lookup"><span data-stu-id="79af0-144">Use the notebooks</span></span>

<span data-ttu-id="79af0-145">Le code de l’exemple décrit dans ce document est disponible à l’adresse [https://github.com/Azure-Samples/hdinsight-spark-scala-kafka](https://github.com/Azure-Samples/hdinsight-spark-scala-kafka).</span><span class="sxs-lookup"><span data-stu-id="79af0-145">The code for the example described in this document is available at [https://github.com/Azure-Samples/hdinsight-spark-scala-kafka](https://github.com/Azure-Samples/hdinsight-spark-scala-kafka).</span></span>

<span data-ttu-id="79af0-146">Suivez les étapes du fichier `README.md` pour terminer cet exemple.</span><span class="sxs-lookup"><span data-stu-id="79af0-146">Follow the steps in the `README.md` file to complete this example.</span></span>

## <a name="delete-the-cluster"></a><span data-ttu-id="79af0-147">Suppression du cluster</span><span class="sxs-lookup"><span data-stu-id="79af0-147">Delete the cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="79af0-148">Étant donné que les étapes décrites dans ce document créent deux clusters dans le même groupe de ressources Azure, vous pouvez supprimer le groupe de ressources du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="79af0-148">Since the steps in this document create both clusters in the same Azure resource group, you can delete the resource group in the Azure portal.</span></span> <span data-ttu-id="79af0-149">La suppression de ce groupe supprime toutes les ressources créées par la suite dans ce document, le réseau virtuel Azure et le compte de stockage utilisé par les clusters.</span><span class="sxs-lookup"><span data-stu-id="79af0-149">Deleting the group removes all resources created by following this document, the Azure Virtual Network, and storage account used by the clusters.</span></span>

## <a name="next-steps"></a><span data-ttu-id="79af0-150">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="79af0-150">Next steps</span></span>

<span data-ttu-id="79af0-151">Dans ce document, vous avez appris à utiliser Spark pour lire et écrire dans Kafka.</span><span class="sxs-lookup"><span data-stu-id="79af0-151">In this example, you learned how to use Spark to read and write to Kafka.</span></span> <span data-ttu-id="79af0-152">Utilisez les liens suivants pour découvrir d’autres façons de travailler avec Kafka :</span><span class="sxs-lookup"><span data-stu-id="79af0-152">Use the following links to discover other ways to work with Kafka:</span></span>

* [<span data-ttu-id="79af0-153">Prise en main d’Apache Kafka sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="79af0-153">Get started with Apache Kafka on HDInsight</span></span>](hdinsight-apache-kafka-get-started.md)
* [<span data-ttu-id="79af0-154">Utilisation de MirrorMaker pour créer un réplica de Kafka sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="79af0-154">Use MirrorMaker to create a replica of Kafka on HDInsight</span></span>](hdinsight-apache-kafka-mirroring.md)
* [<span data-ttu-id="79af0-155">Utilisation d’Apache Storm avec Kafka sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="79af0-155">Use Apache Storm with Kafka on HDInsight</span></span>](hdinsight-apache-storm-with-kafka.md)

