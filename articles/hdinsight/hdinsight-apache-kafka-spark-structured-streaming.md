---
title: "aaaApache structurées Spark diffusion en continu avec Kafka - Azure HDInsight | Documents Microsoft"
description: "Découvrez comment toouse Apache Spark diffusion en continu (DStream) tooget données dans ou hors d’Apache Kafka. Dans cet exemple, vous diffusez des données à l’aide d’un bloc-notes Jupyter à partir de Spark sur HDInsight."
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
ms.openlocfilehash: 0837e8fc5ea314e644daed029d596feeb2b02c68
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-spark-structured-streaming-with-kafka-preview-on-hdinsight"></a><span data-ttu-id="4594a-104">Utiliser Spark Structured Streaming avec Kafka (préversion) sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="4594a-104">Use Spark Structured Streaming with Kafka (preview) on HDInsight</span></span>

<span data-ttu-id="4594a-105">Découvrez comment toouse Spark structurée de diffusion en continu des données de tooread de Kafka Apache sur Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4594a-105">Learn how toouse Spark Structured Streaming tooread data from Apache Kafka on Azure HDInsight.</span></span>

<span data-ttu-id="4594a-106">Spark Structured Streaming est un moteur de traitement de flux basé sur Spark SQL.</span><span class="sxs-lookup"><span data-stu-id="4594a-106">Spark structured streaming is a stream processing engine built on Spark SQL.</span></span> <span data-ttu-id="4594a-107">Il permet de que vous calculs de diffusion en continu tooexpress hello identique au calcul du lot sur les données statiques.</span><span class="sxs-lookup"><span data-stu-id="4594a-107">It allows you tooexpress streaming computations hello same as batch computation on static data.</span></span> <span data-ttu-id="4594a-108">Pour plus d’informations sur la diffusion en continu structuré, consultez hello [structurées de diffusion en continu Guide de programmation [Alpha]](http://spark.apache.org/docs/2.1.0/structured-streaming-programming-guide.html) sur le site Apache.org.</span><span class="sxs-lookup"><span data-stu-id="4594a-108">For more information on Structured Streaming, see hello [Structured Streaming Programming Guide [Alpha]](http://spark.apache.org/docs/2.1.0/structured-streaming-programming-guide.html) at Apache.org.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4594a-109">Cet exemple utilise Spark 2.1 sur HDInsight 3.6.</span><span class="sxs-lookup"><span data-stu-id="4594a-109">This example used Spark 2.1 on HDInsight 3.6.</span></span> <span data-ttu-id="4594a-110">Structured Streaming est considéré comme __alpha__ sur Spark 2.1.</span><span class="sxs-lookup"><span data-stu-id="4594a-110">Structured Streaming is considered __alpha__ on Spark 2.1.</span></span>
>
> <span data-ttu-id="4594a-111">étapes Hello dans ce document créent un groupe de ressources Azure qui contient à la fois un Spark sur HDInsight et un Kafka sur le cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4594a-111">hello steps in this document create an Azure resource group that contains both a Spark on HDInsight and a Kafka on HDInsight cluster.</span></span> <span data-ttu-id="4594a-112">Ces clusters sont situés dans un réseau virtuel Azure, ce qui permet de hello toodirectly de cluster Spark communiquent avec hello cluster de Kafka.</span><span class="sxs-lookup"><span data-stu-id="4594a-112">These clusters are both located within an Azure Virtual Network, which allows hello Spark cluster toodirectly communicate with hello Kafka cluster.</span></span>
>
> <span data-ttu-id="4594a-113">Lorsque vous avez terminé les étapes hello dans ce document, n’oubliez pas de frais supplémentaires de toodelete hello clusters tooavoid.</span><span class="sxs-lookup"><span data-stu-id="4594a-113">When you are done with hello steps in this document, remember toodelete hello clusters tooavoid excess charges.</span></span>

## <a name="create-hello-clusters"></a><span data-ttu-id="4594a-114">Créer des clusters de hello</span><span class="sxs-lookup"><span data-stu-id="4594a-114">Create hello clusters</span></span>

<span data-ttu-id="4594a-115">Kafka Apache sur HDInsight ne fournit pas d’accès toohello Kafka courtiers sur hello internet public.</span><span class="sxs-lookup"><span data-stu-id="4594a-115">Apache Kafka on HDInsight does not provide access toohello Kafka brokers over hello public internet.</span></span> <span data-ttu-id="4594a-116">Tout ce qui tooKafka doit se trouver dans des entretiens hello même réseau virtuel Azure en tant que nœuds hello dans hello cluster de Kafka.</span><span class="sxs-lookup"><span data-stu-id="4594a-116">Anything that talks tooKafka must be in hello same Azure virtual network as hello nodes in hello Kafka cluster.</span></span> <span data-ttu-id="4594a-117">Pour cet exemple, hello Kafka et les clusters Spark se trouvent dans un réseau virtuel Azure.</span><span class="sxs-lookup"><span data-stu-id="4594a-117">For this example, both hello Kafka and Spark clusters are located in an Azure virtual network.</span></span> <span data-ttu-id="4594a-118">Hello diagramme suivant illustre le flux de communication entre les clusters hello :</span><span class="sxs-lookup"><span data-stu-id="4594a-118">hello following diagram shows how communication flows between hello clusters:</span></span>

![Diagramme des clusters Spark et Kafka dans un réseau virtuel Azure](./media/hdinsight-apache-spark-with-kafka/spark-kafka-vnet.png)

> [!NOTE]
> <span data-ttu-id="4594a-120">Hello service de Kafka est toocommunication limitée dans le réseau virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="4594a-120">hello Kafka service is limited toocommunication within hello virtual network.</span></span> <span data-ttu-id="4594a-121">Autres services sur un cluster de hello, tels que SSH et Ambari, sont accessibles via hello internet.</span><span class="sxs-lookup"><span data-stu-id="4594a-121">Other services on hello cluster, such as SSH and Ambari, can be accessed over hello internet.</span></span> <span data-ttu-id="4594a-122">Pour plus d’informations sur les ports publics de hello disponibles avec HDInsight, consultez [Ports et URI utilisé par HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span><span class="sxs-lookup"><span data-stu-id="4594a-122">For more information on hello public ports available with HDInsight, see [Ports and URIs used by HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span></span>

<span data-ttu-id="4594a-123">Si vous pouvez créer un réseau virtuel Azure, Kafka et Spark clusters manuellement, il est plus facile toouse un modèle Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="4594a-123">While you can create an Azure virtual network, Kafka, and Spark clusters manually, it's easier toouse an Azure Resource Manager template.</span></span> <span data-ttu-id="4594a-124">Toodeploy un réseau virtuel Azure, Kafka, les étapes suivantes de hello utilisation et Spark clusters tooyour abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="4594a-124">Use hello following steps toodeploy an Azure virtual network, Kafka, and Spark clusters tooyour Azure subscription.</span></span>

1. <span data-ttu-id="4594a-125">Utilisez hello suivant toosign bouton dans tooAzure et modèle ouvert hello Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="4594a-125">Use hello following button toosign in tooAzure and open hello template in hello Azure portal.</span></span>
    
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-kafka-spark-cluster-in-vnet-v4.1.json" target="_blank"><img src="./media/hdinsight-apache-spark-with-kafka/deploy-to-azure.png" alt="Deploy tooAzure"></a>
    
    <span data-ttu-id="4594a-126">Hello modèle Azure Resource Manager se trouve dans **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-spark-cluster-in-vnet-v4.1.json**.</span><span class="sxs-lookup"><span data-stu-id="4594a-126">hello Azure Resource Manager template is located at **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-spark-cluster-in-vnet-v4.1.json**.</span></span>

    <span data-ttu-id="4594a-127">Ce modèle crée hello suivant des ressources :</span><span class="sxs-lookup"><span data-stu-id="4594a-127">This template creates hello following resources:</span></span>

    * <span data-ttu-id="4594a-128">Un cluster Kafka sur HDInsight 3.5.</span><span class="sxs-lookup"><span data-stu-id="4594a-128">A Kafka on HDInsight 3.5 cluster.</span></span>
    * <span data-ttu-id="4594a-129">Un cluster Spark sur HDInsight 3.6.</span><span class="sxs-lookup"><span data-stu-id="4594a-129">A Spark on HDInsight 3.6 cluster.</span></span>
    * <span data-ttu-id="4594a-130">Un réseau virtuel Azure, qui contient des clusters HDInsight de hello.</span><span class="sxs-lookup"><span data-stu-id="4594a-130">An Azure Virtual Network, which contains hello HDInsight clusters.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="4594a-131">bloc-notes diffusion en continu structuré Hello utilisé dans cet exemple nécessite Spark sur HDInsight 3.6.</span><span class="sxs-lookup"><span data-stu-id="4594a-131">hello structured streaming notebook used in this example requires Spark on HDInsight 3.6.</span></span> <span data-ttu-id="4594a-132">Si vous utilisez une version antérieure de Spark sur HDInsight, vous recevez des erreurs lorsque vous utilisez le bloc-notes de hello.</span><span class="sxs-lookup"><span data-stu-id="4594a-132">If you use an earlier version of Spark on HDInsight, you receive errors when using hello notebook.</span></span>

2. <span data-ttu-id="4594a-133">Hello utilisation suivant des entrées d’information toopopulate hello de hello **les déploiement personnalisé** panneau :</span><span class="sxs-lookup"><span data-stu-id="4594a-133">Use hello following information toopopulate hello entries on hello **Custom deployment** blade:</span></span>
   
    ![Déploiement HDInsight personnalisé](./media/hdinsight-apache-spark-with-kafka/parameters.png)
   
    * <span data-ttu-id="4594a-135">**Groupe de ressources** : créez un groupe de ressources ou sélectionnez-en un.</span><span class="sxs-lookup"><span data-stu-id="4594a-135">**Resource group**: Create a group or select an existing one.</span></span> <span data-ttu-id="4594a-136">Ce groupe contient un cluster HDInsight de hello.</span><span class="sxs-lookup"><span data-stu-id="4594a-136">This group contains hello HDInsight cluster.</span></span>

    * <span data-ttu-id="4594a-137">**Emplacement**: sélectionnez un tooyou géographiquement fermer d’emplacement.</span><span class="sxs-lookup"><span data-stu-id="4594a-137">**Location**: Select a location geographically close tooyou.</span></span>

    * <span data-ttu-id="4594a-138">**Nom du Cluster de base**: cette valeur est utilisée comme nom de base hello pour les clusters de Spark et Kafka hello.</span><span class="sxs-lookup"><span data-stu-id="4594a-138">**Base Cluster Name**: This value is used as hello base name for hello Spark and Kafka clusters.</span></span> <span data-ttu-id="4594a-139">Par exemple, si vous entrez **hdi**, cela crée un cluster Spark nommé spark-hdi__ et un cluster Kafka nommé **kafka-hdi**.</span><span class="sxs-lookup"><span data-stu-id="4594a-139">For example, entering **hdi** creates a Spark cluster named spark-hdi__ and a Kafka cluster named **kafka-hdi**.</span></span>

    * <span data-ttu-id="4594a-140">**Nom d’utilisateur de cluster**: nom d’utilisateur admin hello pour les clusters de Spark et Kafka hello.</span><span class="sxs-lookup"><span data-stu-id="4594a-140">**Cluster Login User Name**: hello admin user name for hello Spark and Kafka clusters.</span></span>

    * <span data-ttu-id="4594a-141">**Mot de passe de connexion cluster**: hello mot de passe administrateur pour les clusters de Spark et Kafka hello.</span><span class="sxs-lookup"><span data-stu-id="4594a-141">**Cluster Login Password**: hello admin user password for hello Spark and Kafka clusters.</span></span>

    * <span data-ttu-id="4594a-142">**Nom d’utilisateur SSH**: hello toocreate d’utilisateur SSH pour les clusters de Spark et Kafka hello.</span><span class="sxs-lookup"><span data-stu-id="4594a-142">**SSH User Name**: hello SSH user toocreate for hello Spark and Kafka clusters.</span></span>

    * <span data-ttu-id="4594a-143">**Mot de passe SSH**: mot de passe de hello pour hello SSH pour les clusters de Spark et Kafka hello.</span><span class="sxs-lookup"><span data-stu-id="4594a-143">**SSH Password**: hello password for hello SSH user for hello Spark and Kafka clusters.</span></span>

3. <span data-ttu-id="4594a-144">Hello de lecture **termes et Conditions**, puis sélectionnez **J’accepte les termes du contrat de toohello et conditions susmentionnées**.</span><span class="sxs-lookup"><span data-stu-id="4594a-144">Read hello **Terms and Conditions**, and then select **I agree toohello terms and conditions stated above**.</span></span>

4. <span data-ttu-id="4594a-145">Enfin, recherchez **code confidentiel toodashboard** , puis sélectionnez **bon**.</span><span class="sxs-lookup"><span data-stu-id="4594a-145">Finally, check **Pin toodashboard** and then select **Purchase**.</span></span> <span data-ttu-id="4594a-146">Il prend environ 20 minutes toocreate les clusters hello.</span><span class="sxs-lookup"><span data-stu-id="4594a-146">It takes about 20 minutes toocreate hello clusters.</span></span>

<span data-ttu-id="4594a-147">Une fois que les ressources hello ont été créées, vous êtes panneau des ressources de groupe toohello redirigé.</span><span class="sxs-lookup"><span data-stu-id="4594a-147">Once hello resources have been created, you are redirected toohello resource group blade.</span></span>

![Panneau des ressources de groupe de réseau virtuel de hello et des clusters](./media/hdinsight-apache-spark-with-kafka/groupblade.png)

> [!IMPORTANT]
> <span data-ttu-id="4594a-149">Notez que les noms de hello des clusters HDInsight de hello sont **spark-BASENAME** et **kafka-BASENAME**, où BASENAME est nom hello toohello modèle fourni.</span><span class="sxs-lookup"><span data-stu-id="4594a-149">Notice that hello names of hello HDInsight clusters are **spark-BASENAME** and **kafka-BASENAME**, where BASENAME is hello name you provided toohello template.</span></span> <span data-ttu-id="4594a-150">Vous utilisez ces noms dans les étapes suivantes lors de la connexion toohello clusters.</span><span class="sxs-lookup"><span data-stu-id="4594a-150">You use these names in later steps when connecting toohello clusters.</span></span>

## <a name="get-hello-kafka-brokers"></a><span data-ttu-id="4594a-151">Obtenir hello Kafka courtiers</span><span class="sxs-lookup"><span data-stu-id="4594a-151">Get hello Kafka brokers</span></span>

<span data-ttu-id="4594a-152">Hello code dans cet exemple connecte toohello Kafka hôtes Bonjour cluster de Kafka du service broker.</span><span class="sxs-lookup"><span data-stu-id="4594a-152">hello code in this example connects toohello Kafka broker hosts in hello Kafka cluster.</span></span> <span data-ttu-id="4594a-153">toofind hello hôtes de service broker Kafka, utilisez hello PowerShell ou Bash l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="4594a-153">toofind hello Kafka broker hosts, use hello following PowerShell or Bash example:</span></span>

```powershell
$creds = Get-Credential -UserName "admin" -Message "Enter hello HDInsight login"
$clusterName = Read-Host -Prompt "Enter hello Kafka cluster name"
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
> <span data-ttu-id="4594a-154">Cet exemple attend `$PASSWORD` toocontain hello mot de passe au cluster de hello, et `$CLUSTERNAME` nom de hello toocontain Hello cluster de Kafka.</span><span class="sxs-lookup"><span data-stu-id="4594a-154">This example expects `$PASSWORD` toocontain hello password for hello cluster login, and `$CLUSTERNAME` toocontain hello name of hello Kafka cluster.</span></span>
>
> <span data-ttu-id="4594a-155">Cet exemple utilise hello [jq](https://stedolan.github.io/jq/) données tooparse utilitaire de document JSON de hello.</span><span class="sxs-lookup"><span data-stu-id="4594a-155">This example uses hello [jq](https://stedolan.github.io/jq/) utility tooparse data out of hello JSON document.</span></span>

<span data-ttu-id="4594a-156">Hello est similaire toohello suivant texte de sortie :</span><span class="sxs-lookup"><span data-stu-id="4594a-156">hello output is similar toohello following text:</span></span>

`wn0-kafka.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net:9092,wn1-kafka.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net:9092,wn2-kafka.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net:9092,wn3-kafka.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net:9092`

<span data-ttu-id="4594a-157">Enregistrez ces informations, car il est utilisé dans les sections suivantes de ce document de hello.</span><span class="sxs-lookup"><span data-stu-id="4594a-157">Save this information, as it is used in hello following sections of this document.</span></span>

## <a name="get-hello-notebooks"></a><span data-ttu-id="4594a-158">Obtenir les blocs-notes hello</span><span class="sxs-lookup"><span data-stu-id="4594a-158">Get hello notebooks</span></span>

<span data-ttu-id="4594a-159">code Hello pour exemple hello décrite dans ce document est disponible à l’adresse [https://github.com/Azure-Samples/hdinsight-spark-kafka-structured-streaming](https://github.com/Azure-Samples/hdinsight-spark-kafka-structured-streaming).</span><span class="sxs-lookup"><span data-stu-id="4594a-159">hello code for hello example described in this document is available at [https://github.com/Azure-Samples/hdinsight-spark-kafka-structured-streaming](https://github.com/Azure-Samples/hdinsight-spark-kafka-structured-streaming).</span></span>

## <a name="upload-hello-notebooks"></a><span data-ttu-id="4594a-160">Télécharger les blocs-notes hello</span><span class="sxs-lookup"><span data-stu-id="4594a-160">Upload hello notebooks</span></span>

<span data-ttu-id="4594a-161">Utilisez hello étapes suivantes blocs-notes de hello tooupload de hello projet tooyour Spark sur le cluster HDInsight :</span><span class="sxs-lookup"><span data-stu-id="4594a-161">Use hello following steps tooupload hello notebooks from hello project tooyour Spark on HDInsight cluster:</span></span>

1. <span data-ttu-id="4594a-162">Dans votre navigateur web, connectez-vous toohello bloc-notes jupyter sur votre cluster Spark.</span><span class="sxs-lookup"><span data-stu-id="4594a-162">In your web browser, connect toohello Jupyter notebook on your Spark cluster.</span></span> <span data-ttu-id="4594a-163">Bonjour suivant URL, remplacez `CLUSTERNAME` par nom hello de votre cluster Kafka :</span><span class="sxs-lookup"><span data-stu-id="4594a-163">In hello following URL, replace `CLUSTERNAME` with hello name of your Kafka cluster:</span></span>

        https://CLUSTERNAME.azurehdinsight.net/jupyter

    <span data-ttu-id="4594a-164">Lorsque vous y êtes invité, entrez la connexion de cluster hello (admin) et le mot de passe utilisé lors de la création de cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="4594a-164">When prompted, enter hello cluster login (admin) and password used when you created hello cluster.</span></span>

2. <span data-ttu-id="4594a-165">À partir de hello coin supérieur droit de la page de hello, utilisez hello __télécharger__ hello tooupload de bouton __flux-Tweets-To_Kafka.ipynb__ toohello de fichiers.</span><span class="sxs-lookup"><span data-stu-id="4594a-165">From hello upper right side of hello page, use hello __Upload__ button tooupload hello __Stream-Tweets-To_Kafka.ipynb__ file toohello cluster.</span></span> <span data-ttu-id="4594a-166">Sélectionnez __ouvrir__ téléchargement de hello toostart.</span><span class="sxs-lookup"><span data-stu-id="4594a-166">Select __Open__ toostart hello upload.</span></span>

    ![Utilisez tooselect de bouton de téléchargement hello et télécharger un ordinateur portable](./media/hdinsight-apache-kafka-spark-structured-streaming/upload-button.png)

    ![Sélectionnez le fichier de KafkaStreaming.ipynb hello](./media/hdinsight-apache-kafka-spark-structured-streaming/select-notebook.png)

3. <span data-ttu-id="4594a-169">Recherche hello __flux-Tweets-To_Kafka.ipynb__ entrée dans la liste hello de blocs-notes et sélectionnez __télécharger__ bouton à côté de lui.</span><span class="sxs-lookup"><span data-stu-id="4594a-169">Find hello __Stream-Tweets-To_Kafka.ipynb__ entry in hello list of notebooks, and select __Upload__ button beside it.</span></span>

    ![Téléchargement de hello utilisez bouton en regard de tooupload d’entrée hello KafkaStreaming.ipynb il serveur bloc-notes de toohello](./media/hdinsight-apache-kafka-spark-structured-streaming/upload-notebook.png)

4. <span data-ttu-id="4594a-171">Répétez les étapes hello tooload de 1 à 3 __Spark-structuré-diffusion en continu-de-Kafka.ipynb__ bloc-notes.</span><span class="sxs-lookup"><span data-stu-id="4594a-171">Repeat steps 1-3 tooload hello __Spark-Structured-Streaming-From-Kafka.ipynb__ notebook.</span></span>

## <a name="load-tweets-into-kafka"></a><span data-ttu-id="4594a-172">Charger des tweets dans Kafka</span><span class="sxs-lookup"><span data-stu-id="4594a-172">Load tweets into Kafka</span></span>

<span data-ttu-id="4594a-173">Une fois que les fichiers hello ont été téléchargés, sélectionnez hello __flux-Tweets-To_Kafka.ipynb__ bloc-notes de hello tooopen entrée.</span><span class="sxs-lookup"><span data-stu-id="4594a-173">Once hello files have been uploaded, select hello __Stream-Tweets-To_Kafka.ipynb__ entry tooopen hello notebook.</span></span> <span data-ttu-id="4594a-174">Suivez les étapes de hello de hello bloc-notes tooload tweets dans Kafka.</span><span class="sxs-lookup"><span data-stu-id="4594a-174">Follow hello steps in hello notebook tooload tweets into Kafka.</span></span>

## <a name="process-tweets-using-spark-structured-streaming"></a><span data-ttu-id="4594a-175">Traiter des tweets à l’aide de Spark Structured Streaming</span><span class="sxs-lookup"><span data-stu-id="4594a-175">Process tweets using Spark Structured Streaming</span></span>

<span data-ttu-id="4594a-176">À partir de hello bloc-notes Jupyter page d’accueil, sélectionnez hello __Spark-structuré-diffusion en continu-de-Kafka.ipynb__ entrée.</span><span class="sxs-lookup"><span data-stu-id="4594a-176">From hello Jupyter Notebook home page, select hello __Spark-Structured-Streaming-From-Kafka.ipynb__ entry.</span></span> <span data-ttu-id="4594a-177">Suivez les étapes de hello de hello bloc-notes tooload tweets de Kafka à l’aide de Spark structurée de diffusion en continu.</span><span class="sxs-lookup"><span data-stu-id="4594a-177">Follow hello steps in hello notebook tooload tweets from Kafka using Spark Structured Streaming.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4594a-178">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4594a-178">Next steps</span></span>

<span data-ttu-id="4594a-179">Maintenant que vous avez appris comment toouse Spark structurées en continu, consultez hello suivant toolearn documents plus sur l’utilisation de Spark et Kafka :</span><span class="sxs-lookup"><span data-stu-id="4594a-179">Now that you have learned how toouse Spark Structured Streaming, see hello following documents toolearn more about working with Spark and Kafka:</span></span>

* <span data-ttu-id="4594a-180">[Comment toouse au service de diffusion en continu (DStream) avec Kafka](hdinsight-apache-spark-with-kafka.md).</span><span class="sxs-lookup"><span data-stu-id="4594a-180">[How toouse Spark streaming (DStream) with Kafka](hdinsight-apache-spark-with-kafka.md).</span></span>
* [<span data-ttu-id="4594a-181">Prise en main du bloc-notes Jupyter et Spark sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="4594a-181">Start with Jupyter Notebook and Spark on HDInsight</span></span>](hdinsight-apache-spark-jupyter-spark-sql.md)