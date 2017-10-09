---
title: "rubriques d’Apache Kafka aaaMirror - Azure HDInsight | Documents Microsoft"
description: "Découvrez comment la mise en miroir de Kafka toouse Apache de fonctionnalité toomaintain un réplica d’un Kafka sur le cluster HDInsight en cluster secondaire tooa de rubriques de mise en miroir."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 015d276e-f678-4f2b-9572-75553c56625b
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/13/2017
ms.author: larryfr
ms.openlocfilehash: 5ace0251d7402d4d7d9b28726e253ce7091a87ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-mirrormaker-tooreplicate-apache-kafka-topics-with-kafka-on-hdinsight-preview"></a><span data-ttu-id="299b7-103">Utilisez les rubriques d’Apache Kafka MirrorMaker tooreplicate avec Kafka sur HDInsight (version préliminaire)</span><span class="sxs-lookup"><span data-stu-id="299b7-103">Use MirrorMaker tooreplicate Apache Kafka topics with Kafka on HDInsight (preview)</span></span>

<span data-ttu-id="299b7-104">Découvrez comment toouse Apache Kafka de mise en miroir de fonctionnalité tooreplicate rubriques tooa secondaire de cluster.</span><span class="sxs-lookup"><span data-stu-id="299b7-104">Learn how toouse Apache Kafka's mirroring feature tooreplicate topics tooa secondary cluster.</span></span> <span data-ttu-id="299b7-105">Mise en miroir peut être exécuté comme un processus continu, ou en tant que méthode de migration, utilisé par intermittence tooanother de données à partir d’un cluster.</span><span class="sxs-lookup"><span data-stu-id="299b7-105">Mirroring can be ran as a continuous process, or used intermittently as a method of migrating data from one cluster tooanother.</span></span>

<span data-ttu-id="299b7-106">Dans cet exemple, la mise en miroir est rubriques tooreplicate utilisé entre deux clusters HDInsight.</span><span class="sxs-lookup"><span data-stu-id="299b7-106">In this example, mirroring is used tooreplicate topics between two HDInsight clusters.</span></span> <span data-ttu-id="299b7-107">Les deux clusters se trouvant dans un réseau virtuel Azure Bonjour même région.</span><span class="sxs-lookup"><span data-stu-id="299b7-107">Both clusters are in an Azure Virtual Network in hello same region.</span></span>

> [!WARNING]
> <span data-ttu-id="299b7-108">Mise en miroir ne doit pas être considéré comme un moyen tooachieve une tolérance de pannes.</span><span class="sxs-lookup"><span data-stu-id="299b7-108">Mirroring should not be considered as a means tooachieve fault-tolerance.</span></span> <span data-ttu-id="299b7-109">tooitems de décalage Hello au sein d’une rubrique sont différentes entre les clusters sources et de destination de hello, pour les clients ne peuvent pas utiliser de manière interchangeable hello deux.</span><span class="sxs-lookup"><span data-stu-id="299b7-109">hello offset tooitems within a topic are different between hello source and destination clusters, so clients cannot use hello two interchangeably.</span></span>
>
> <span data-ttu-id="299b7-110">Si vous êtes inquiet de la tolérance de panne, vous devez définir la réplication pour les rubriques hello dans votre cluster.</span><span class="sxs-lookup"><span data-stu-id="299b7-110">If you are concerned about fault tolerance, you should set replication for hello topics within your cluster.</span></span> <span data-ttu-id="299b7-111">Pour plus d’informations, consultez [Prise en main de Kafka sur HDInsight](hdinsight-apache-kafka-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="299b7-111">For more information, see [Get started with Kafka on HDInsight](hdinsight-apache-kafka-get-started.md).</span></span>

## <a name="how-kafka-mirroring-works"></a><span data-ttu-id="299b7-112">Fonctionne de la mise en miroir Kafka</span><span class="sxs-lookup"><span data-stu-id="299b7-112">How Kafka mirroring works</span></span>

<span data-ttu-id="299b7-113">Fonctionnement de la mise en miroir à l’aide de hello MirrorMaker outil (partie de Apache Kafka) tooconsume des enregistrements à partir des rubriques sur le cluster source de hello, puis créez une copie locale sur le cluster de destination hello.</span><span class="sxs-lookup"><span data-stu-id="299b7-113">Mirroring works by using hello MirrorMaker tool (part of Apache Kafka) tooconsume records from topics on hello source cluster and then create a local copy on hello destination cluster.</span></span> <span data-ttu-id="299b7-114">MirrorMaker utilise un (ou plusieurs) *consommateurs* lus à partir du cluster source hello et un *producteur* qui écrit du cluster de toohello local (destination).</span><span class="sxs-lookup"><span data-stu-id="299b7-114">MirrorMaker uses one (or more) *consumers* that read from hello source cluster, and a *producer* that writes toohello local (destination) cluster.</span></span>

<span data-ttu-id="299b7-115">Hello suivant schéma illustre le processus de mise en miroir hello :</span><span class="sxs-lookup"><span data-stu-id="299b7-115">hello following diagram illustrates hello Mirroring process:</span></span>

![Diagramme de processus de mise en miroir de hello](./media/hdinsight-apache-kafka-mirroring/kafka-mirroring.png)

<span data-ttu-id="299b7-117">Kafka Apache sur HDInsight ne fournit pas d’accès toohello service de Kafka sur hello internet public.</span><span class="sxs-lookup"><span data-stu-id="299b7-117">Apache Kafka on HDInsight does not provide access toohello Kafka service over hello public internet.</span></span> <span data-ttu-id="299b7-118">Les producteurs Kafka ou qu’ils doivent être Bonjour même réseau virtuel Azure en tant que nœuds hello Bonjour cluster de Kafka.</span><span class="sxs-lookup"><span data-stu-id="299b7-118">Kafka producers or consumers must be in hello same Azure virtual network as hello nodes in hello Kafka cluster.</span></span> <span data-ttu-id="299b7-119">Pour cet exemple, hello source de Kafka et clusters de destination se trouvent dans un réseau virtuel Azure.</span><span class="sxs-lookup"><span data-stu-id="299b7-119">For this example, both hello Kafka source and destination clusters are located in an Azure virtual network.</span></span> <span data-ttu-id="299b7-120">Hello diagramme suivant illustre le flux de communication entre les clusters hello :</span><span class="sxs-lookup"><span data-stu-id="299b7-120">hello following diagram shows how communication flows between hello clusters:</span></span>

![Diagramme du cluster source et du cluster de destination Kafka dans un réseau virtuel Azure](./media/hdinsight-apache-kafka-mirroring/spark-kafka-vnet.png)

<span data-ttu-id="299b7-122">les clusters sources et de destination Hello peuvent être différents dans nombre hello des nœuds et des partitions, et les décalages dans les rubriques hello diffèrent également.</span><span class="sxs-lookup"><span data-stu-id="299b7-122">hello source and destination clusters can be different in hello number of nodes and partitions, and offsets within hello topics are different also.</span></span> <span data-ttu-id="299b7-123">Mise en miroir de conserve la valeur de clé de hello qui est utilisé pour le partitionnement, afin de l’ordre d’enregistrement est conservé sur une base par clé.</span><span class="sxs-lookup"><span data-stu-id="299b7-123">Mirroring maintains hello key value that is used for partitioning, so record order is preserved on a per-key basis.</span></span>

### <a name="mirroring-across-network-boundaries"></a><span data-ttu-id="299b7-124">Mise en miroir au-delà des limites réseau</span><span class="sxs-lookup"><span data-stu-id="299b7-124">Mirroring across network boundaries</span></span>

<span data-ttu-id="299b7-125">Si vous devez toomirror entre Kafka des clusters sur différents réseaux, il existe des hello suivant des considérations supplémentaires :</span><span class="sxs-lookup"><span data-stu-id="299b7-125">If you need toomirror between Kafka clusters in different networks, there are hello following additional considerations:</span></span>

* <span data-ttu-id="299b7-126">**Passerelles**: les réseaux hello doivent être en mesure de toocommunicate à hello au niveau du TCPIP.</span><span class="sxs-lookup"><span data-stu-id="299b7-126">**Gateways**: hello networks must be able toocommunicate at hello TCPIP level.</span></span>

* <span data-ttu-id="299b7-127">**La résolution de noms**: hello Kafka des clusters dans chaque réseau doit être en mesure de tooconnect tooeach autres à l’aide de noms d’hôte.</span><span class="sxs-lookup"><span data-stu-id="299b7-127">**Name resolution**: hello Kafka clusters in each network must be able tooconnect tooeach other by using hostnames.</span></span> <span data-ttu-id="299b7-128">Cette opération peut nécessiter un serveur de système DNS (Domain Name) de chaque réseau est configuré tooforward demandes toohello autres réseaux.</span><span class="sxs-lookup"><span data-stu-id="299b7-128">This may require a Domain Name System (DNS) server in each network that is configured tooforward requests toohello other networks.</span></span>

    <span data-ttu-id="299b7-129">Lors de la création d’un réseau virtuel Azure, au lieu d’utiliser hello qu'automatique DNS fourni avec le réseau de hello, vous devez spécifier une personnalisé DNS server hello adresse IP et de serveur de hello.</span><span class="sxs-lookup"><span data-stu-id="299b7-129">When creating an Azure Virtual Network, instead of using hello automatic DNS provided with hello network, you must specify a custom DNS server and hello IP address for hello server.</span></span> <span data-ttu-id="299b7-130">Après hello que réseau virtuel a été créé, vous devez ensuite créer une Machine virtuelle Azure qui utilise cette adresse IP, puis installer et configurer le logiciel DNS sur celui-ci.</span><span class="sxs-lookup"><span data-stu-id="299b7-130">After hello Virtual Network has been created, you must then create an Azure Virtual Machine that uses that IP address, then install and configure DNS software on it.</span></span>

    > [!WARNING]
    > <span data-ttu-id="299b7-131">Créez et configurez un serveur DNS personnalisé hello avant d’installer HDInsight dans hello réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="299b7-131">Create and configure hello custom DNS server before installing HDInsight into hello Virtual Network.</span></span> <span data-ttu-id="299b7-132">Il n’existe aucune configuration supplémentaire requise pour le serveur DNS HDInsight toouse hello sont configuré pour hello réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="299b7-132">There is no additional configuration required for HDInsight toouse hello DNS server configured for hello Virtual Network.</span></span>

<span data-ttu-id="299b7-133">Pour plus d’informations sur la connexion de deux réseaux virtuels Azure, consultez [Configurer une connexion de réseau virtuel à réseau virtuel](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="299b7-133">For more information on connecting two Azure Virtual Networks, see [Configure a VNet-to-VNet connection](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md).</span></span>

## <a name="create-kafka-clusters"></a><span data-ttu-id="299b7-134">Création de clusters Kafka</span><span class="sxs-lookup"><span data-stu-id="299b7-134">Create Kafka clusters</span></span>

<span data-ttu-id="299b7-135">Pendant que vous pouvez créer un réseau virtuel Azure et Kafka clusters manuellement, il est plus facile toouse un modèle Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="299b7-135">While you can create an Azure virtual network and Kafka clusters manually, it's easier toouse an Azure Resource Manager template.</span></span> <span data-ttu-id="299b7-136">Utilisez hello suivant les étapes toodeploy un réseau virtuel Azure et deux tooyour de clusters Kafka abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="299b7-136">Use hello following steps toodeploy an Azure virtual network and two Kafka clusters tooyour Azure subscription.</span></span>

1. <span data-ttu-id="299b7-137">Utilisez hello suivant toosign bouton dans tooAzure et modèle ouvert hello Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="299b7-137">Use hello following button toosign in tooAzure and open hello template in hello Azure portal.</span></span>
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json" target="_blank"><img src="./media/hdinsight-apache-kafka-mirroring/deploy-to-azure.png" alt="Deploy tooAzure"></a>
   
    <span data-ttu-id="299b7-138">Hello modèle Azure Resource Manager se trouve dans **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json**.</span><span class="sxs-lookup"><span data-stu-id="299b7-138">hello Azure Resource Manager template is located at **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json**.</span></span>

    > [!WARNING]
    > <span data-ttu-id="299b7-139">disponibilité tooguarantee de Kafka sur HDInsight, votre cluster doit contenir au moins trois nœuds de travail.</span><span class="sxs-lookup"><span data-stu-id="299b7-139">tooguarantee availability of Kafka on HDInsight, your cluster must contain at least three worker nodes.</span></span> <span data-ttu-id="299b7-140">Ce modèle crée un cluster Kafka qui contient trois nœuds Worker.</span><span class="sxs-lookup"><span data-stu-id="299b7-140">This template creates a Kafka cluster that contains three worker nodes.</span></span>

2. <span data-ttu-id="299b7-141">Hello utilisation suivant des entrées d’information toopopulate hello de hello **les déploiement personnalisé** panneau :</span><span class="sxs-lookup"><span data-stu-id="299b7-141">Use hello following information toopopulate hello entries on hello **Custom deployment** blade:</span></span>
    
    ![Déploiement HDInsight personnalisé](./media/hdinsight-apache-kafka-mirroring/parameters.png)
    
    * <span data-ttu-id="299b7-143">**Groupe de ressources** : créez un groupe de ressources ou sélectionnez-en un.</span><span class="sxs-lookup"><span data-stu-id="299b7-143">**Resource group**: Create a group or select an existing one.</span></span> <span data-ttu-id="299b7-144">Ce groupe contient un cluster HDInsight de hello.</span><span class="sxs-lookup"><span data-stu-id="299b7-144">This group contains hello HDInsight cluster.</span></span>

    * <span data-ttu-id="299b7-145">**Emplacement**: sélectionnez un tooyou géographiquement fermer d’emplacement.</span><span class="sxs-lookup"><span data-stu-id="299b7-145">**Location**: Select a location geographically close tooyou.</span></span>
     
    * <span data-ttu-id="299b7-146">**Nom du Cluster de base**: cette valeur est utilisée comme nom de base hello pour hello Kafka clusters.</span><span class="sxs-lookup"><span data-stu-id="299b7-146">**Base Cluster Name**: This value is used as hello base name for hello Kafka clusters.</span></span> <span data-ttu-id="299b7-147">Par exemple, l’entrée de **hdi** crée des clusters nommés **source-hdi** et **dest-hdi**.</span><span class="sxs-lookup"><span data-stu-id="299b7-147">For example, entering **hdi** creates clusters named **source-hdi** and **dest-hdi**.</span></span>

    * <span data-ttu-id="299b7-148">**Nom d’utilisateur de cluster**: clusters de Kafka nom d’utilisateur admin hello pour hello source et de destination.</span><span class="sxs-lookup"><span data-stu-id="299b7-148">**Cluster Login User Name**: hello admin user name for hello source and destination Kafka clusters.</span></span>

    * <span data-ttu-id="299b7-149">**Mot de passe de connexion cluster**: les clusters Kafka hello mot de passe administrateur pour hello source et de destination.</span><span class="sxs-lookup"><span data-stu-id="299b7-149">**Cluster Login Password**: hello admin user password for hello source and destination Kafka clusters.</span></span>

    * <span data-ttu-id="299b7-150">**Nom d’utilisateur SSH**: les clusters Kafka hello SSH utilisateur toocreate pour hello source et de destination.</span><span class="sxs-lookup"><span data-stu-id="299b7-150">**SSH User Name**: hello SSH user toocreate for hello source and destination Kafka clusters.</span></span>

    * <span data-ttu-id="299b7-151">**Mot de passe SSH**: clusters de Kafka de mot de passe de hello pour hello SSH pour hello source et de destination.</span><span class="sxs-lookup"><span data-stu-id="299b7-151">**SSH Password**: hello password for hello SSH user for hello source and destination Kafka clusters.</span></span>

3. <span data-ttu-id="299b7-152">Hello de lecture **termes et Conditions**, puis sélectionnez **J’accepte les termes du contrat de toohello et conditions susmentionnées**.</span><span class="sxs-lookup"><span data-stu-id="299b7-152">Read hello **Terms and Conditions**, and then select **I agree toohello terms and conditions stated above**.</span></span>

4. <span data-ttu-id="299b7-153">Enfin, recherchez **code confidentiel toodashboard** , puis sélectionnez **bon**.</span><span class="sxs-lookup"><span data-stu-id="299b7-153">Finally, check **Pin toodashboard** and then select **Purchase**.</span></span> <span data-ttu-id="299b7-154">Il prend environ 20 minutes toocreate les clusters hello.</span><span class="sxs-lookup"><span data-stu-id="299b7-154">It takes about 20 minutes toocreate hello clusters.</span></span>

<span data-ttu-id="299b7-155">Une fois que les ressources hello ont été créées, vous êtes panneau tooa redirigé hello groupe de ressources qui contient des clusters de hello et tableau de bord web.</span><span class="sxs-lookup"><span data-stu-id="299b7-155">Once hello resources have been created, you are redirected tooa blade for hello resource group that contains hello clusters and web dashboard.</span></span>

![Panneau des ressources de groupe de réseau virtuel de hello et des clusters](./media/hdinsight-apache-kafka-mirroring/groupblade.png)

> [!IMPORTANT]
> <span data-ttu-id="299b7-157">Notez que les noms de hello des clusters HDInsight de hello sont **source-BASENAME** et **dest-BASENAME**, où BASENAME est nom hello toohello modèle fourni.</span><span class="sxs-lookup"><span data-stu-id="299b7-157">Notice that hello names of hello HDInsight clusters are **source-BASENAME** and **dest-BASENAME**, where BASENAME is hello name you provided toohello template.</span></span> <span data-ttu-id="299b7-158">Vous utilisez ces noms dans les étapes suivantes lors de la connexion toohello clusters.</span><span class="sxs-lookup"><span data-stu-id="299b7-158">You use these names in later steps when connecting toohello clusters.</span></span>

## <a name="create-topics"></a><span data-ttu-id="299b7-159">Création de sujets</span><span class="sxs-lookup"><span data-stu-id="299b7-159">Create topics</span></span>

1. <span data-ttu-id="299b7-160">Se connecter toohello **source** cluster à l’aide de SSH :</span><span class="sxs-lookup"><span data-stu-id="299b7-160">Connect toohello **source** cluster using SSH:</span></span>

    ```bash
    ssh sshuser@source-BASENAME-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="299b7-161">Remplacez **sshuser** avec nom d’utilisateur SSH hello utilisé lors de la création du cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="299b7-161">Replace **sshuser** with hello SSH user name used when creating hello cluster.</span></span> <span data-ttu-id="299b7-162">Remplacez **BASENAME** par nom de base hello utilisé lors de la création du cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="299b7-162">Replace **BASENAME** with hello base name used when creating hello cluster.</span></span>

    <span data-ttu-id="299b7-163">Pour en savoir plus, voir [Utilisation de SSH avec HDInsight (Hadoop) depuis Bash (l’interpréteur de commande) sur Windows 10, Linux, Unix ou OS X](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="299b7-163">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="299b7-164">Suivant de hello utilisez commandes toofind hello soigneur ordinateurs hôtes pour du cluster source hello :</span><span class="sxs-lookup"><span data-stu-id="299b7-164">Use hello following commands toofind hello Zookeeper hosts for hello source cluster:</span></span>

    ```bash
    # Install jq if it is not installed
    sudo apt -y install jq
    # get hello zookeeper hosts for hello source cluster
    export SOURCE_ZKHOSTS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/ZOOKEEPER/components/ZOOKEEPER_SERVER | jq -r '["\(.host_components[].HostRoles.host_name):2181"] | join(",")' | cut -d',' -f1,2`
    
    Replace `$PASSWORD` with hello password for hello cluster.

    Replace `$CLUSTERNAME` with hello name of hello source cluster.

3. toocreate a topic named `testtopic`, use hello following command:

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --create --replication-factor 2 --partitions 8 --topic testtopic --zookeeper $SOURCE_ZKHOSTS
    ```

3. <span data-ttu-id="299b7-165">Hello utilisation suivant tooverify de commande qui hello rubrique a été créé :</span><span class="sxs-lookup"><span data-stu-id="299b7-165">Use hello following command tooverify that hello topic was created:</span></span>

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --list --zookeeper $SOURCE_ZKHOSTS
    ```

    <span data-ttu-id="299b7-166">réponse de Hello contient `testtopic`.</span><span class="sxs-lookup"><span data-stu-id="299b7-166">hello response contains `testtopic`.</span></span>

4. <span data-ttu-id="299b7-167">Hello utilisation suivant tooview hello soigneur informations sur l’hôte pour ce (hello **source**) cluster :</span><span class="sxs-lookup"><span data-stu-id="299b7-167">Use hello following tooview hello Zookeeper host information for this (hello **source**) cluster:</span></span>

    ```bash
    echo $SOURCE_ZKHOSTS
    ```

    <span data-ttu-id="299b7-168">Cet exemple renvoie toohello similaire à informations suivant le texte :</span><span class="sxs-lookup"><span data-stu-id="299b7-168">This returns information similar toohello following text:</span></span>

    `zk0-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:2181,zk1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:2181`

    <span data-ttu-id="299b7-169">Enregistrez ces informations.</span><span class="sxs-lookup"><span data-stu-id="299b7-169">Save this information.</span></span> <span data-ttu-id="299b7-170">Il est utilisé dans la section suivante de hello.</span><span class="sxs-lookup"><span data-stu-id="299b7-170">It is used in hello next section.</span></span>

## <a name="configure-mirroring"></a><span data-ttu-id="299b7-171">Configuration de la mise en miroir</span><span class="sxs-lookup"><span data-stu-id="299b7-171">Configure mirroring</span></span>

1. <span data-ttu-id="299b7-172">Se connecter toohello **destination** cluster à l’aide d’une autre session SSH :</span><span class="sxs-lookup"><span data-stu-id="299b7-172">Connect toohello **destination** cluster using a different SSH session:</span></span>

    ```bash
    ssh sshuser@dest-BASENAME-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="299b7-173">Remplacez **sshuser** avec nom d’utilisateur SSH hello utilisé lors de la création du cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="299b7-173">Replace **sshuser** with hello SSH user name used when creating hello cluster.</span></span> <span data-ttu-id="299b7-174">Remplacez **BASENAME** par nom de base hello utilisé lors de la création du cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="299b7-174">Replace **BASENAME** with hello base name used when creating hello cluster.</span></span>

    <span data-ttu-id="299b7-175">Pour en savoir plus, voir [Utilisation de SSH avec HDInsight (Hadoop) depuis Bash (l’interpréteur de commande) sur Windows 10, Linux, Unix ou OS X](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="299b7-175">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="299b7-176">Suivant de hello utilisez commande toocreate un `consumer.properties` décrivant comment toocommunicate avec hello **source** cluster :</span><span class="sxs-lookup"><span data-stu-id="299b7-176">Use hello following command toocreate a `consumer.properties` file that describes how toocommunicate with hello **source** cluster:</span></span>

    ```bash
    nano consumer.properties
    ```

    <span data-ttu-id="299b7-177">Hello utilisation après le texte en tant que contenu hello Hello `consumer.properties` fichier :</span><span class="sxs-lookup"><span data-stu-id="299b7-177">Use hello following text as hello contents of hello `consumer.properties` file:</span></span>

    ```yaml
    zookeeper.connect=SOURCE_ZKHOSTS
    group.id=mirrorgroup
    ```

    <span data-ttu-id="299b7-178">Remplacez **SOURCE_ZKHOSTS** avec hello soigneur héberge les informations à partir de hello **source** cluster.</span><span class="sxs-lookup"><span data-stu-id="299b7-178">Replace **SOURCE_ZKHOSTS** with hello Zookeeper hosts information from hello **source** cluster.</span></span>

    <span data-ttu-id="299b7-179">Ce fichier décrit hello consommateur informations toouse lors de la lecture à partir de la source de hello cluster de Kafka.</span><span class="sxs-lookup"><span data-stu-id="299b7-179">This file describes hello consumer information toouse when reading from hello source Kafka cluster.</span></span> <span data-ttu-id="299b7-180">Pour plus d’informations sur la configuration du consommateur, consultez [Consumer Configs](https://kafka.apache.org/documentation#consumerconfigs) (Configurations de consommateur) sur kafka.apache.org.</span><span class="sxs-lookup"><span data-stu-id="299b7-180">For more information consumer configuration, see [Consumer Configs](https://kafka.apache.org/documentation#consumerconfigs) at kafka.apache.org.</span></span>

    <span data-ttu-id="299b7-181">fichier de hello toosave, utilisez **Ctrl + X**, **Y**, puis **entrée**.</span><span class="sxs-lookup"><span data-stu-id="299b7-181">toosave hello file, use **Ctrl + X**, **Y**, and then **Enter**.</span></span>

3. <span data-ttu-id="299b7-182">Avant de configurer le producteur hello qui communique avec le cluster de destination hello, vous devez trouver hello broker hôtes pour hello **destination** cluster.</span><span class="sxs-lookup"><span data-stu-id="299b7-182">Before configuring hello producer that communicates with hello destination cluster, you must find hello broker hosts for hello **destination** cluster.</span></span> <span data-ttu-id="299b7-183">Utilisez hello suivant de commandes tooretrieve ces informations :</span><span class="sxs-lookup"><span data-stu-id="299b7-183">Use hello following commands tooretrieve this information:</span></span>

    ```bash
    sudo apt -y install jq
    DEST_BROKERHOSTS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/KAFKA/components/KAFKA_BROKER | jq -r '["\(.host_components[].HostRoles.host_name):9092"] | join(",")' | cut -d',' -f1,2`
    echo $DEST_BROKERHOSTS
    ```

    <span data-ttu-id="299b7-184">Remplacez `$PASSWORD` avec le mot de passe du compte (administrateur) hello connexion pour le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="299b7-184">Replace `$PASSWORD` with hello login account (admin) password for hello cluster.</span></span>

    <span data-ttu-id="299b7-185">Remplacez `$CLUSTERNAME` par nom de hello du cluster de destination hello.</span><span class="sxs-lookup"><span data-stu-id="299b7-185">Replace `$CLUSTERNAME` with hello name of hello destination cluster.</span></span>

    <span data-ttu-id="299b7-186">Ces commandes retournent des informations similaires toohello qui suivent :</span><span class="sxs-lookup"><span data-stu-id="299b7-186">These commands return information similar toohello following:</span></span>

        wn0-dest.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn1-dest.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092

4. <span data-ttu-id="299b7-187">Hello utilisation suivant toocreate un `producer.properties` décrivant comment toocommunicate avec hello **destination** cluster :</span><span class="sxs-lookup"><span data-stu-id="299b7-187">Use hello following toocreate a `producer.properties` file that describes how toocommunicate with hello **destination** cluster:</span></span>

    ```bash
    nano producer.properties
    ```

    <span data-ttu-id="299b7-188">Hello utilisation après le texte en tant que contenu hello Hello `producer.properties` fichier :</span><span class="sxs-lookup"><span data-stu-id="299b7-188">Use hello following text as hello contents of hello `producer.properties` file:</span></span>

    ```yaml
    bootstrap.servers=DEST_BROKERS
    compression.type=none
    ```

    <span data-ttu-id="299b7-189">Remplacez **DEST_BROKERS** avec les informations de service broker hello à partir de l’étape précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="299b7-189">Replace **DEST_BROKERS** with hello broker information from hello previous step.</span></span>

    <span data-ttu-id="299b7-190">Pour plus d’informations sur la configuration du producteur, consultez [Producer Configs](https://kafka.apache.org/documentation#producerconfigs) (Configurations de producteur) sur kafka.apache.org.</span><span class="sxs-lookup"><span data-stu-id="299b7-190">For more information producer configuration, see [Producer Configs](https://kafka.apache.org/documentation#producerconfigs) at kafka.apache.org.</span></span>

## <a name="start-mirrormaker"></a><span data-ttu-id="299b7-191">Lancement de MirrorMaker</span><span class="sxs-lookup"><span data-stu-id="299b7-191">Start MirrorMaker</span></span>

1. <span data-ttu-id="299b7-192">À partir de hello SSH connexion toohello **destination** de cluster, utilisez hello suivant commande toostart hello MirrorMaker processus :</span><span class="sxs-lookup"><span data-stu-id="299b7-192">From hello SSH connection toohello **destination** cluster, use hello following command toostart hello MirrorMaker process:</span></span>

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-run-class.sh kafka.tools.MirrorMaker --consumer.config consumer.properties --producer.config producer.properties --whitelist testtopic --num.streams 4
    ```

    <span data-ttu-id="299b7-193">paramètres Hello utilisés dans cet exemple sont :</span><span class="sxs-lookup"><span data-stu-id="299b7-193">hello parameters used in this example are:</span></span>

    * <span data-ttu-id="299b7-194">**--consumer.config**: Spécifie le fichier hello qui contient les propriétés de consommateur.</span><span class="sxs-lookup"><span data-stu-id="299b7-194">**--consumer.config**: Specifies hello file that contains consumer properties.</span></span> <span data-ttu-id="299b7-195">Ces propriétés sont utilisée toocreate un consommateur qui lit à partir de hello *source* cluster de Kafka.</span><span class="sxs-lookup"><span data-stu-id="299b7-195">These properties are used toocreate a consumer that reads from hello *source* Kafka cluster.</span></span>

    * <span data-ttu-id="299b7-196">**--producer.config**: Spécifie le fichier hello qui contient les propriétés de producteur.</span><span class="sxs-lookup"><span data-stu-id="299b7-196">**--producer.config**: Specifies hello file that contains producer properties.</span></span> <span data-ttu-id="299b7-197">Ces propriétés sont utilisée toocreate un producteur qui écrit toohello *destination* cluster de Kafka.</span><span class="sxs-lookup"><span data-stu-id="299b7-197">These properties are used toocreate a producer that writes toohello *destination* Kafka cluster.</span></span>

    * <span data-ttu-id="299b7-198">**liste blanche--**: une liste de rubriques MirrorMaker réplique de hello source cluster toohello de destination.</span><span class="sxs-lookup"><span data-stu-id="299b7-198">**--whitelist**: A list of topics that MirrorMaker replicates from hello source cluster toohello destination.</span></span>

    * <span data-ttu-id="299b7-199">**--num.streams**: hello nombre de toocreate de threads de consommateur.</span><span class="sxs-lookup"><span data-stu-id="299b7-199">**--num.streams**: hello number of consumer threads toocreate.</span></span>

 <span data-ttu-id="299b7-200">Au démarrage, MirrorMaker retourne toohello similaire à informations suivant le texte :</span><span class="sxs-lookup"><span data-stu-id="299b7-200">On startup, MirrorMaker returns information similar toohello following text:</span></span>

    ```json
    {metadata.broker.list=wn1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn0-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092, request.timeout.ms=30000, client.id=mirror-group-3, security.protocol=PLAINTEXT}{metadata.broker.list=wn1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn0-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092, request.timeout.ms=30000, client.id=mirror-group-0, security.protocol=PLAINTEXT}
    metadata.broker.list=wn1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn0-kafka.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092, request.timeout.ms=30000, client.id=mirror-group-2, security.protocol=PLAINTEXT}
    metadata.broker.list=wn1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn0-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092, request.timeout.ms=30000, client.id=mirror-group-1, security.protocol=PLAINTEXT}
    ```

2. <span data-ttu-id="299b7-201">À partir de hello SSH connexion toohello **source** de cluster, utilisez hello suivant commande toostart un producteur et rubrique toohello de messages d’envoi :</span><span class="sxs-lookup"><span data-stu-id="299b7-201">From hello SSH connection toohello **source** cluster, use hello following command toostart a producer and send messages toohello topic:</span></span>

    ```bash
    SOURCE_BROKERHOSTS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/KAFKA/components/KAFKA_BROKER | jq -r '["\(.host_components[].HostRoles.host_name):9092"] | join(",")' | cut -d',' -f1,2`
    /usr/hdp/current/kafka-broker/bin/kafka-console-producer.sh --broker-list $SOURCE_BROKERHOSTS --topic testtopic
    ```

    <span data-ttu-id="299b7-202">Remplacez `$PASSWORD` avec un mot de passe de connexion (admin) pour le cluster source de hello hello.</span><span class="sxs-lookup"><span data-stu-id="299b7-202">Replace `$PASSWORD` with hello login (admin) password for hello source cluster.</span></span>

    <span data-ttu-id="299b7-203">Remplacez `$CLUSTERNAME` par nom de hello du cluster de source de hello.</span><span class="sxs-lookup"><span data-stu-id="299b7-203">Replace `$CLUSTERNAME` with hello name of hello source cluster.</span></span>

     <span data-ttu-id="299b7-204">Lorsque vous arrivez sur une ligne vide avec un curseur, tapez quelques messages texte.</span><span class="sxs-lookup"><span data-stu-id="299b7-204">When you arrive at a blank line with a cursor, type in a few text messages.</span></span> <span data-ttu-id="299b7-205">Ceux-ci sont envoyés toohello rubrique sur hello **source** cluster.</span><span class="sxs-lookup"><span data-stu-id="299b7-205">These are sent toohello topic on hello **source** cluster.</span></span> <span data-ttu-id="299b7-206">Lorsque vous avez terminé, utilisez **Ctrl + C** processus de producteur tooend hello.</span><span class="sxs-lookup"><span data-stu-id="299b7-206">When done, use **Ctrl + C** tooend hello producer process.</span></span>

3. <span data-ttu-id="299b7-207">À partir de hello SSH connexion toohello **destination** de cluster, utilisez **Ctrl + C** tooend hello MirrorMaker processus.</span><span class="sxs-lookup"><span data-stu-id="299b7-207">From hello SSH connection toohello **destination** cluster, use **Ctrl + C** tooend hello MirrorMaker process.</span></span> <span data-ttu-id="299b7-208">Puis suit de hello utilisez commandes tooverify que hello `testtopic` rubrique a été créée, et que les données de la rubrique de hello a été répliquée toothis miroir :</span><span class="sxs-lookup"><span data-stu-id="299b7-208">Then use hello following commands tooverify that hello `testtopic` topic was created, and that data in hello topic was replicated toothis mirror:</span></span>

    ```bash
    DEST_ZKHOSTS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/ZOOKEEPER/components/ZOOKEEPER_SERVER | jq -r '["\(.host_components[].HostRoles.host_name):2181"] | join(",")' | cut -d',' -f1,2`
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --list --zookeeper $DEST_ZKHOSTS
    /usr/hdp/current/kafka-broker/bin/kafka-console-consumer.sh --zookeeper $DEST_ZKHOSTS --topic testtopic --from-beginning
    ```

    <span data-ttu-id="299b7-209">Remplacez `$PASSWORD` avec un mot de passe de connexion (admin) pour le cluster de destination hello hello.</span><span class="sxs-lookup"><span data-stu-id="299b7-209">Replace `$PASSWORD` with hello login (admin) password for hello destination cluster.</span></span>

    <span data-ttu-id="299b7-210">Remplacez `$CLUSTERNAME` par nom de hello du cluster de destination hello.</span><span class="sxs-lookup"><span data-stu-id="299b7-210">Replace `$CLUSTERNAME` with hello name of hello destination cluster.</span></span>

    <span data-ttu-id="299b7-211">Hello la liste des rubriques inclut désormais `testtopic`, qui est créé lorsque MirrorMaster reflète rubrique hello hello source cluster toohello de destination.</span><span class="sxs-lookup"><span data-stu-id="299b7-211">hello list of topics now includes `testtopic`, which is created when MirrorMaster mirrors hello topic from hello source cluster toohello destination.</span></span> <span data-ttu-id="299b7-212">messages Hello récupérées à partir de la rubrique de hello sont hello entré sur le cluster de hello source identique.</span><span class="sxs-lookup"><span data-stu-id="299b7-212">hello messages retrieved from hello topic are hello same as entered on hello source cluster.</span></span>

## <a name="delete-hello-cluster"></a><span data-ttu-id="299b7-213">Supprimer le cluster de hello</span><span class="sxs-lookup"><span data-stu-id="299b7-213">Delete hello cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="299b7-214">Étant donné que les étapes de hello dans ce document vous allez créer deux clusters dans hello même groupe de ressources Azure, vous pouvez supprimer le groupe de ressources hello Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="299b7-214">Since hello steps in this document create both clusters in hello same Azure resource group, you can delete hello resource group in hello Azure portal.</span></span> <span data-ttu-id="299b7-215">Groupe de ressources hello suppression supprime toutes les ressources créées en suivant ce document, hello réseau virtuel Azure et compte de stockage utilisé par les clusters de hello.</span><span class="sxs-lookup"><span data-stu-id="299b7-215">Deleting hello resource group removes all resources created by following this document, hello Azure Virtual Network, and storage account used by hello clusters.</span></span>

## <a name="next-steps"></a><span data-ttu-id="299b7-216">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="299b7-216">Next Steps</span></span>

<span data-ttu-id="299b7-217">Dans ce document, vous avez appris comment toouse MirrorMaker toocreate un réplica d’un Kafka cluster.</span><span class="sxs-lookup"><span data-stu-id="299b7-217">In this document, you learned how toouse MirrorMaker toocreate a replica of a Kafka cluster.</span></span> <span data-ttu-id="299b7-218">Utilisez des autres façons toowork hello suivant les liens toodiscover avec Kafka :</span><span class="sxs-lookup"><span data-stu-id="299b7-218">Use hello following links toodiscover other ways toowork with Kafka:</span></span>

* <span data-ttu-id="299b7-219">[Documentation d’Apache Kafka MirrorMaker](https://cwiki.apache.org/confluence/pages/viewpage.action?pageId=27846330) sur cwiki.apache.org.</span><span class="sxs-lookup"><span data-stu-id="299b7-219">[Apache Kafka MirrorMaker documentation](https://cwiki.apache.org/confluence/pages/viewpage.action?pageId=27846330) at cwiki.apache.org.</span></span>
* [<span data-ttu-id="299b7-220">Prise en main d’Apache Kafka sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="299b7-220">Get started with Apache Kafka on HDInsight</span></span>](hdinsight-apache-kafka-get-started.md)
* <span data-ttu-id="299b7-221">[Use Apache Spark with Kafka on HDInsight](hdinsight-apache-spark-with-kafka.md) (Utilisation d’Apache Spark avec Kafka sur HDInsight)</span><span class="sxs-lookup"><span data-stu-id="299b7-221">[Use Apache Spark with Kafka on HDInsight](hdinsight-apache-spark-with-kafka.md)</span></span>
* [<span data-ttu-id="299b7-222">Utilisation d’Apache Storm avec Kafka sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="299b7-222">Use Apache Storm with Kafka on HDInsight</span></span>](hdinsight-apache-storm-with-kafka.md)
* [<span data-ttu-id="299b7-223">Se connecter tooKafka via un réseau virtuel Azure</span><span class="sxs-lookup"><span data-stu-id="299b7-223">Connect tooKafka through an Azure Virtual Network</span></span>](hdinsight-apache-kafka-connect-vpn-gateway.md)
