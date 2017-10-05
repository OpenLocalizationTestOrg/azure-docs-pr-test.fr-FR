---
title: Apache Spark Structured Streaming avec Kafka - Azure HDInsight | Documents Microsoft
description: "Découvrez comment utiliser la diffusion en continu Apache Spark (DStream) pour échanger des flux de données avec Apache Kafka. Dans cet exemple, vous diffusez des données à l’aide d’un bloc-notes Jupyter à partir de Spark sur HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: 
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/09/2017
ms.author: larryfr
ms.openlocfilehash: 02b49e13e8f54c3d55310f4d2b21c7e09c91fe81
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="use-spark-structured-streaming-with-kafka-preview-on-hdinsight"></a><span data-ttu-id="e496f-104">Utiliser Spark Structured Streaming avec Kafka (préversion) sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="e496f-104">Use Spark Structured Streaming with Kafka (preview) on HDInsight</span></span>

<span data-ttu-id="e496f-105">Découvrez comment utiliser Spark Structured Streaming pour lire des données à partir d’Apache Kafka sur Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e496f-105">Learn how to use Spark Structured Streaming to read data from Apache Kafka on Azure HDInsight.</span></span>

<span data-ttu-id="e496f-106">Spark Structured Streaming est un moteur de traitement de flux basé sur Spark SQL.</span><span class="sxs-lookup"><span data-stu-id="e496f-106">Spark structured streaming is a stream processing engine built on Spark SQL.</span></span> <span data-ttu-id="e496f-107">Il vous permet d’exprimer des calculs de diffusion en continu de la même façon que pour les calculs de lot sur les données statiques.</span><span class="sxs-lookup"><span data-stu-id="e496f-107">It allows you to express streaming computations the same as batch computation on static data.</span></span> <span data-ttu-id="e496f-108">Pour plus d’informations sur Structured Streaming, consultez le [Guide de programmation Structured Streaming [Alpha]](http://spark.apache.org/docs/2.1.0/structured-streaming-programming-guide.html) sur le site Apache.org.</span><span class="sxs-lookup"><span data-stu-id="e496f-108">For more information on Structured Streaming, see the [Structured Streaming Programming Guide [Alpha]](http://spark.apache.org/docs/2.1.0/structured-streaming-programming-guide.html) at Apache.org.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e496f-109">Cet exemple utilise Spark 2.1 sur HDInsight 3.6.</span><span class="sxs-lookup"><span data-stu-id="e496f-109">This example used Spark 2.1 on HDInsight 3.6.</span></span> <span data-ttu-id="e496f-110">Structured Streaming est considéré comme __alpha__ sur Spark 2.1.</span><span class="sxs-lookup"><span data-stu-id="e496f-110">Structured Streaming is considered __alpha__ on Spark 2.1.</span></span>
>
> <span data-ttu-id="e496f-111">Les étapes décrites dans ce document créent un groupe de ressources Azure qui contient à la fois un Spark sur HDInsight et un Kafka sur un cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e496f-111">The steps in this document create an Azure resource group that contains both a Spark on HDInsight and a Kafka on HDInsight cluster.</span></span> <span data-ttu-id="e496f-112">Ces clusters sont tous deux situés dans un réseau virtuel Azure, ce qui permet au cluster Spark de communiquer directement avec le cluster Kafka.</span><span class="sxs-lookup"><span data-stu-id="e496f-112">These clusters are both located within an Azure Virtual Network, which allows the Spark cluster to directly communicate with the Kafka cluster.</span></span>
>
> <span data-ttu-id="e496f-113">Lorsque vous avez terminé les étapes décrites dans ce document, n’oubliez pas de supprimer les clusters pour éviter les frais supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="e496f-113">When you are done with the steps in this document, remember to delete the clusters to avoid excess charges.</span></span>

## <a name="create-the-clusters"></a><span data-ttu-id="e496f-114">Création des clusters</span><span class="sxs-lookup"><span data-stu-id="e496f-114">Create the clusters</span></span>

<span data-ttu-id="e496f-115">Apache Kafka sur HDInsight ne donne pas accès aux répartiteurs Kafka via l’internet public.</span><span class="sxs-lookup"><span data-stu-id="e496f-115">Apache Kafka on HDInsight does not provide access to the Kafka brokers over the public internet.</span></span> <span data-ttu-id="e496f-116">Tout ce qui communique avec Kafka doit se trouver sur le même réseau virtuel Azure que les nœuds du cluster Kafka.</span><span class="sxs-lookup"><span data-stu-id="e496f-116">Anything that talks to Kafka must be in the same Azure virtual network as the nodes in the Kafka cluster.</span></span> <span data-ttu-id="e496f-117">Pour cet exemple, les clusters Kafka et Spark sont situés dans un réseau virtuel Azure.</span><span class="sxs-lookup"><span data-stu-id="e496f-117">For this example, both the Kafka and Spark clusters are located in an Azure virtual network.</span></span> <span data-ttu-id="e496f-118">Le diagramme suivant illustre le flux de communication entre les clusters :</span><span class="sxs-lookup"><span data-stu-id="e496f-118">The following diagram shows how communication flows between the clusters:</span></span>

![Diagramme des clusters Spark et Kafka dans un réseau virtuel Azure](./media/hdinsight-apache-spark-with-kafka/spark-kafka-vnet.png)

> [!NOTE]
> <span data-ttu-id="e496f-120">Le service Kafka est limité à la communication au sein du réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="e496f-120">The Kafka service is limited to communication within the virtual network.</span></span> <span data-ttu-id="e496f-121">L’accès aux autres services sur le cluster, tels que SSH et Ambari, se fait via Internet.</span><span class="sxs-lookup"><span data-stu-id="e496f-121">Other services on the cluster, such as SSH and Ambari, can be accessed over the internet.</span></span> <span data-ttu-id="e496f-122">Pour plus d’informations sur les ports publics disponibles avec HDInsight, consultez [Ports et URI utilisés par HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span><span class="sxs-lookup"><span data-stu-id="e496f-122">For more information on the public ports available with HDInsight, see [Ports and URIs used by HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span></span>

<span data-ttu-id="e496f-123">Même si vous pouvez créer un réseau virtuel Azure, et des clusters Kafka et Spark manuellement, il est plus facile d’utiliser un modèle Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="e496f-123">While you can create an Azure virtual network, Kafka, and Spark clusters manually, it's easier to use an Azure Resource Manager template.</span></span> <span data-ttu-id="e496f-124">Utilisez les étapes suivantes pour déployer un réseau virtuel Azure et des clusters Kafka et Spark sur votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="e496f-124">Use the following steps to deploy an Azure virtual network, Kafka, and Spark clusters to your Azure subscription.</span></span>

1. <span data-ttu-id="e496f-125">Utilisez le bouton suivant pour vous connecter à Azure et ouvrir le modèle dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="e496f-125">Use the following button to sign in to Azure and open the template in the Azure portal.</span></span>
    
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-kafka-spark-cluster-in-vnet-v4.1.json" target="_blank"><img src="./media/hdinsight-apache-spark-with-kafka/deploy-to-azure.png" alt="Deploy to Azure"></a>
    
    <span data-ttu-id="e496f-126">Le modèle Azure Resource Manager se trouve à l’adresse **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-spark-cluster-in-vnet-v4.1.json**.</span><span class="sxs-lookup"><span data-stu-id="e496f-126">The Azure Resource Manager template is located at **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-spark-cluster-in-vnet-v4.1.json**.</span></span>

    <span data-ttu-id="e496f-127">Ce modèle crée les ressources suivantes :</span><span class="sxs-lookup"><span data-stu-id="e496f-127">This template creates the following resources:</span></span>

    * <span data-ttu-id="e496f-128">Un cluster Kafka sur HDInsight 3.5.</span><span class="sxs-lookup"><span data-stu-id="e496f-128">A Kafka on HDInsight 3.5 cluster.</span></span>
    * <span data-ttu-id="e496f-129">Un cluster Spark sur HDInsight 3.6.</span><span class="sxs-lookup"><span data-stu-id="e496f-129">A Spark on HDInsight 3.6 cluster.</span></span>
    * <span data-ttu-id="e496f-130">Un réseau virtuel Azure, qui contient les clusters HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e496f-130">An Azure Virtual Network, which contains the HDInsight clusters.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="e496f-131">Le bloc-notes de diffusion en continu structurée utilisé dans cet exemple nécessite Spark sur HDInsight 3.6.</span><span class="sxs-lookup"><span data-stu-id="e496f-131">The structured streaming notebook used in this example requires Spark on HDInsight 3.6.</span></span> <span data-ttu-id="e496f-132">Si vous utilisez une version antérieure de Spark sur HDInsight, vous recevez des erreurs lors de l’utilisation du bloc-notes.</span><span class="sxs-lookup"><span data-stu-id="e496f-132">If you use an earlier version of Spark on HDInsight, you receive errors when using the notebook.</span></span>

2. <span data-ttu-id="e496f-133">Utilisez les informations suivantes pour remplir les entrées sur le panneau **déploiement personnalisé** :</span><span class="sxs-lookup"><span data-stu-id="e496f-133">Use the following information to populate the entries on the **Custom deployment** blade:</span></span>
   
    ![Déploiement HDInsight personnalisé](./media/hdinsight-apache-spark-with-kafka/parameters.png)
   
    * <span data-ttu-id="e496f-135">**Groupe de ressources** : créez un groupe de ressources ou sélectionnez-en un.</span><span class="sxs-lookup"><span data-stu-id="e496f-135">**Resource group**: Create a group or select an existing one.</span></span> <span data-ttu-id="e496f-136">Ce groupe contient le cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e496f-136">This group contains the HDInsight cluster.</span></span>

    * <span data-ttu-id="e496f-137">**Emplacement** : choisissez un emplacement proche de vous géographiquement.</span><span class="sxs-lookup"><span data-stu-id="e496f-137">**Location**: Select a location geographically close to you.</span></span>

    * <span data-ttu-id="e496f-138">**Nom de cluster de base** : cette valeur sera utilisée comme nom de base pour les clusters Spark et Kafka.</span><span class="sxs-lookup"><span data-stu-id="e496f-138">**Base Cluster Name**: This value is used as the base name for the Spark and Kafka clusters.</span></span> <span data-ttu-id="e496f-139">Par exemple, si vous entrez **hdi**, cela crée un cluster Spark nommé spark-hdi__ et un cluster Kafka nommé **kafka-hdi**.</span><span class="sxs-lookup"><span data-stu-id="e496f-139">For example, entering **hdi** creates a Spark cluster named spark-hdi__ and a Kafka cluster named **kafka-hdi**.</span></span>

    * <span data-ttu-id="e496f-140">**Nom d’utilisateur du cluster** : nom utilisateur Admin pour les clusters Spark et Kafka.</span><span class="sxs-lookup"><span data-stu-id="e496f-140">**Cluster Login User Name**: The admin user name for the Spark and Kafka clusters.</span></span>

    * <span data-ttu-id="e496f-141">**Mot de passe du cluster** : mot de passe utilisateur Admin pour les clusters Spark et Kafka.</span><span class="sxs-lookup"><span data-stu-id="e496f-141">**Cluster Login Password**: The admin user password for the Spark and Kafka clusters.</span></span>

    * <span data-ttu-id="e496f-142">**Nom d’utilisateur SSH** : utilisateur SSH permettant de créer des clusters Spark et Kafka.</span><span class="sxs-lookup"><span data-stu-id="e496f-142">**SSH User Name**: The SSH user to create for the Spark and Kafka clusters.</span></span>

    * <span data-ttu-id="e496f-143">**Mot de passe SSH** : mot de passe de l’utilisateur SSH pour les clusters Spark et Kafka.</span><span class="sxs-lookup"><span data-stu-id="e496f-143">**SSH Password**: The password for the SSH user for the Spark and Kafka clusters.</span></span>

3. <span data-ttu-id="e496f-144">Passez en revue les **termes et conditions**, puis cochez la case **J’accepte les termes et conditions mentionnés ci-dessus**.</span><span class="sxs-lookup"><span data-stu-id="e496f-144">Read the **Terms and Conditions**, and then select **I agree to the terms and conditions stated above**.</span></span>

4. <span data-ttu-id="e496f-145">Pour finir, cochez **Épingler au tableau de bord**, puis sélectionnez **Acheter**.</span><span class="sxs-lookup"><span data-stu-id="e496f-145">Finally, check **Pin to dashboard** and then select **Purchase**.</span></span> <span data-ttu-id="e496f-146">La création des clusters prend environ 20 minutes.</span><span class="sxs-lookup"><span data-stu-id="e496f-146">It takes about 20 minutes to create the clusters.</span></span>

<span data-ttu-id="e496f-147">Une fois que les ressources ont été créées, vous êtes redirigé vers le panneau du groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="e496f-147">Once the resources have been created, you are redirected to the resource group blade.</span></span>

![Volet du groupe de ressources pour les clusters et le réseau virtuel](./media/hdinsight-apache-spark-with-kafka/groupblade.png)

> [!IMPORTANT]
> <span data-ttu-id="e496f-149">Les noms des clusters HDInsight sont **spark-BASENAME** et **kafka-BASENAME**, où BASENAME est le nom que vous avez fourni pour le modèle.</span><span class="sxs-lookup"><span data-stu-id="e496f-149">Notice that the names of the HDInsight clusters are **spark-BASENAME** and **kafka-BASENAME**, where BASENAME is the name you provided to the template.</span></span> <span data-ttu-id="e496f-150">Vous utilisez ces noms dans les étapes ultérieures, lors de la connexion aux clusters.</span><span class="sxs-lookup"><span data-stu-id="e496f-150">You use these names in later steps when connecting to the clusters.</span></span>

## <a name="get-the-kafka-brokers"></a><span data-ttu-id="e496f-151">Obtenir les répartiteurs Kafka</span><span class="sxs-lookup"><span data-stu-id="e496f-151">Get the Kafka brokers</span></span>

<span data-ttu-id="e496f-152">Le code dans cet exemple se connecte aux hôtes répartiteurs Kafka dans le cluster Kafka.</span><span class="sxs-lookup"><span data-stu-id="e496f-152">The code in this example connects to the Kafka broker hosts in the Kafka cluster.</span></span> <span data-ttu-id="e496f-153">Pour rechercher les hôtes répartiteurs Kafka, utilisez l’exemple PowerShell ou Bash suivant :</span><span class="sxs-lookup"><span data-stu-id="e496f-153">To find the Kafka broker hosts, use the following PowerShell or Bash example:</span></span>

```powershell
$creds = Get-Credential -UserName "admin" -Message "Enter the HDInsight login"
$clusterName = Read-Host -Prompt "Enter the Kafka cluster name"
$resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/KAFKA/components/KAFKA_BROKER" `
    -Credential $creds
$respObj = ConvertFrom-Json $resp.Content
$brokerHosts = $respObj.host_components.HostRoles.host_name
($brokerHosts -join ":9092,") + ":9092"
```

```bash
curl -u admin:$PASSWORD -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/KAFKA/components/KAFKA_BROKER" | jq -r '["\(.host_components[].HostRoles.host_name):9092"] | join(",")'
```

> [!NOTE]
> <span data-ttu-id="e496f-154">Cet exemple s’attend à ce que `$PASSWORD` contienne le mot de passe pour la connexion au cluster et à ce que `$CLUSTERNAME` contienne le nom du cluster Kafka.</span><span class="sxs-lookup"><span data-stu-id="e496f-154">This example expects `$PASSWORD` to contain the password for the cluster login, and `$CLUSTERNAME` to contain the name of the Kafka cluster.</span></span>
>
> <span data-ttu-id="e496f-155">Cet exemple utilise l’utilitaire [jq](https://stedolan.github.io/jq/) pour analyser les données du document JSON.</span><span class="sxs-lookup"><span data-stu-id="e496f-155">This example uses the [jq](https://stedolan.github.io/jq/) utility to parse data out of the JSON document.</span></span>

<span data-ttu-id="e496f-156">Le résultat ressemble au texte suivant :</span><span class="sxs-lookup"><span data-stu-id="e496f-156">The output is similar to the following text:</span></span>

`wn0-kafka.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net:9092,wn1-kafka.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net:9092,wn2-kafka.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net:9092,wn3-kafka.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net:9092`

<span data-ttu-id="e496f-157">Notez ces informations car elles sont utilisées dans les sections suivantes de ce document.</span><span class="sxs-lookup"><span data-stu-id="e496f-157">Save this information, as it is used in the following sections of this document.</span></span>

## <a name="get-the-notebooks"></a><span data-ttu-id="e496f-158">Obtenir les blocs-notes</span><span class="sxs-lookup"><span data-stu-id="e496f-158">Get the notebooks</span></span>

<span data-ttu-id="e496f-159">Le code de l’exemple décrit dans ce document est disponible à l’adresse [https://github.com/Azure-Samples/hdinsight-spark-kafka-structured-streaming](https://github.com/Azure-Samples/hdinsight-spark-kafka-structured-streaming).</span><span class="sxs-lookup"><span data-stu-id="e496f-159">The code for the example described in this document is available at [https://github.com/Azure-Samples/hdinsight-spark-kafka-structured-streaming](https://github.com/Azure-Samples/hdinsight-spark-kafka-structured-streaming).</span></span>

## <a name="upload-the-notebooks"></a><span data-ttu-id="e496f-160">Charger les blocs-notes</span><span class="sxs-lookup"><span data-stu-id="e496f-160">Upload the notebooks</span></span>

<span data-ttu-id="e496f-161">Pour charger les blocs-notes à partir du projet vers votre cluster Spark sur HDInsight, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="e496f-161">Use the following steps to upload the notebooks from the project to your Spark on HDInsight cluster:</span></span>

1. <span data-ttu-id="e496f-162">Dans votre navigateur web, connectez-vous au bloc-notes Jupyter sur votre cluster Spark.</span><span class="sxs-lookup"><span data-stu-id="e496f-162">In your web browser, connect to the Jupyter notebook on your Spark cluster.</span></span> <span data-ttu-id="e496f-163">Dans l’URL suivante, remplacez `CLUSTERNAME` par le nom de votre cluster Kafka :</span><span class="sxs-lookup"><span data-stu-id="e496f-163">In the following URL, replace `CLUSTERNAME` with the name of your Kafka cluster:</span></span>

        https://CLUSTERNAME.azurehdinsight.net/jupyter

    <span data-ttu-id="e496f-164">Lorsque vous y êtes invité, entrez l’identifiant de connexion (admin) et le mot de passe du cluster utilisés lors de la création du cluster.</span><span class="sxs-lookup"><span data-stu-id="e496f-164">When prompted, enter the cluster login (admin) and password used when you created the cluster.</span></span>

2. <span data-ttu-id="e496f-165">Dans la partie supérieure droite de la page, utilisez le bouton __Charger__ pour charger le fichier __Stream-Tweets-To_Kafka.ipynb__ dans le cluster.</span><span class="sxs-lookup"><span data-stu-id="e496f-165">From the upper right side of the page, use the __Upload__ button to upload the __Stream-Tweets-To_Kafka.ipynb__ file to the cluster.</span></span> <span data-ttu-id="e496f-166">Sélectionnez __Ouvrir__ pour démarrer le chargement.</span><span class="sxs-lookup"><span data-stu-id="e496f-166">Select __Open__ to start the upload.</span></span>

    ![Utiliser le bouton Charger pour sélectionner et charger un bloc-notes](./media/hdinsight-apache-kafka-spark-structured-streaming/upload-button.png)

    ![Sélectionner le fichier KafkaStreaming.ipynb](./media/hdinsight-apache-kafka-spark-structured-streaming/select-notebook.png)

3. <span data-ttu-id="e496f-169">Recherchez l’entrée __Stream-Tweets-To_Kafka.ipynb__ dans la liste des blocs-notes, puis sélectionnez le bouton __Charger__ en regard de celle-ci.</span><span class="sxs-lookup"><span data-stu-id="e496f-169">Find the __Stream-Tweets-To_Kafka.ipynb__ entry in the list of notebooks, and select __Upload__ button beside it.</span></span>

    ![Utiliser le bouton Charger en regard de l’entrée KafkaStreaming.ipynb pour charger celle-ci vers le serveur de blocs-notes](./media/hdinsight-apache-kafka-spark-structured-streaming/upload-notebook.png)

4. <span data-ttu-id="e496f-171">Répétez les étapes 1 à 3 pour charger le bloc-notes __Spark-Structured-Streaming-From-Kafka.ipynb__.</span><span class="sxs-lookup"><span data-stu-id="e496f-171">Repeat steps 1-3 to load the __Spark-Structured-Streaming-From-Kafka.ipynb__ notebook.</span></span>

## <a name="load-tweets-into-kafka"></a><span data-ttu-id="e496f-172">Charger des tweets dans Kafka</span><span class="sxs-lookup"><span data-stu-id="e496f-172">Load tweets into Kafka</span></span>

<span data-ttu-id="e496f-173">Une fois que les fichiers ont été chargés, sélectionnez l’entrée __Stream-Tweets-To_Kafka.ipynb__ pour ouvrir le bloc-notes.</span><span class="sxs-lookup"><span data-stu-id="e496f-173">Once the files have been uploaded, select the __Stream-Tweets-To_Kafka.ipynb__ entry to open the notebook.</span></span> <span data-ttu-id="e496f-174">Suivez les étapes dans le bloc-notes pour charger des tweets dans Kafka.</span><span class="sxs-lookup"><span data-stu-id="e496f-174">Follow the steps in the notebook to load tweets into Kafka.</span></span>

## <a name="process-tweets-using-spark-structured-streaming"></a><span data-ttu-id="e496f-175">Traiter des tweets à l’aide de Spark Structured Streaming</span><span class="sxs-lookup"><span data-stu-id="e496f-175">Process tweets using Spark Structured Streaming</span></span>

<span data-ttu-id="e496f-176">Dans la page d’accueil du bloc-notes Jupyter, sélectionnez l’entrée __Spark-Structured-Streaming-From-Kafka.ipynb__.</span><span class="sxs-lookup"><span data-stu-id="e496f-176">From the Jupyter Notebook home page, select the __Spark-Structured-Streaming-From-Kafka.ipynb__ entry.</span></span> <span data-ttu-id="e496f-177">Suivez les étapes dans le bloc-notes pour charger des tweets à partir de Kafka à l’aide de Spark Structured Streaming.</span><span class="sxs-lookup"><span data-stu-id="e496f-177">Follow the steps in the notebook to load tweets from Kafka using Spark Structured Streaming.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e496f-178">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e496f-178">Next steps</span></span>

<span data-ttu-id="e496f-179">Maintenant que vous avez appris à utiliser Spark Structured Streaming, consultez les documents suivants pour en savoir plus sur l’utilisation de Spark et de Kafka :</span><span class="sxs-lookup"><span data-stu-id="e496f-179">Now that you have learned how to use Spark Structured Streaming, see the following documents to learn more about working with Spark and Kafka:</span></span>

* <span data-ttu-id="e496f-180">[Utilisation de la diffusion en continu Spark (DStream) avec Kafka](hdinsight-apache-spark-with-kafka.md).</span><span class="sxs-lookup"><span data-stu-id="e496f-180">[How to use Spark streaming (DStream) with Kafka](hdinsight-apache-spark-with-kafka.md).</span></span>
* [<span data-ttu-id="e496f-181">Prise en main du bloc-notes Jupyter et Spark sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="e496f-181">Start with Jupyter Notebook and Spark on HDInsight</span></span>](hdinsight-apache-spark-jupyter-spark-sql.md)