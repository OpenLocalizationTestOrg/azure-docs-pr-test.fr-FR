---
title: aaaStart avec Apache Kafka - Azure HDInsight | Documents Microsoft
description: "Découvrez comment toocreate un Kafka Apache cluster sur Azure HDInsight. Découvrez comment toocreate consommateurs, rubriques et les abonnés."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 43585abf-bec1-4322-adde-6db21de98d7f
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: 
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/14/2017
ms.author: larryfr
ms.openlocfilehash: b93299d88dc2cf9a9764662509308ff75fd74474
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="start-with-apache-kafka-preview-on-hdinsight"></a><span data-ttu-id="b132a-104">Démarrer avec Apache Kafka (version préliminaire) sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="b132a-104">Start with Apache Kafka (preview) on HDInsight</span></span>

<span data-ttu-id="b132a-105">Découvrez comment toocreate et utiliser une [Apache Kafka](https://kafka.apache.org) cluster sur Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b132a-105">Learn how toocreate and use an [Apache Kafka](https://kafka.apache.org) cluster on Azure HDInsight.</span></span> <span data-ttu-id="b132a-106">Kafka est une plateforme de diffusion en continu distribuée open source, disponible avec HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b132a-106">Kafka is an open-source, distributed streaming platform that is available with HDInsight.</span></span> <span data-ttu-id="b132a-107">Il est souvent utilisé comme un courtier de messages, car il fournit des fonctionnalités similaires tooa publication-abonnement file d’attente.</span><span class="sxs-lookup"><span data-stu-id="b132a-107">It is often used as a message broker, as it provides functionality similar tooa publish-subscribe message queue.</span></span>

> [!NOTE]
> <span data-ttu-id="b132a-108">Il existe actuellement deux versions de Kafka disponibles avec HDInsight ; 0.9.0 (HDInsight 3.4) et 0.10.0 (HDInsight 3.5 et 3.6).</span><span class="sxs-lookup"><span data-stu-id="b132a-108">There are currently two versions of Kafka available with HDInsight; 0.9.0 (HDInsight 3.4) and 0.10.0 (HDInsight 3.5 and 3.6).</span></span> <span data-ttu-id="b132a-109">étapes de Hello dans ce document supposent que vous utilisez Kafka sur HDInsight 3.6.</span><span class="sxs-lookup"><span data-stu-id="b132a-109">hello steps in this document assume that you are using Kafka on HDInsight 3.6.</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="create-a-kafka-cluster"></a><span data-ttu-id="b132a-110">Création d’un cluster Kafka</span><span class="sxs-lookup"><span data-stu-id="b132a-110">Create a Kafka cluster</span></span>

<span data-ttu-id="b132a-111">Utilisez hello suivant les étapes toocreate un Kafka de cluster HDInsight :</span><span class="sxs-lookup"><span data-stu-id="b132a-111">Use hello following steps toocreate a Kafka on HDInsight cluster:</span></span>

1. <span data-ttu-id="b132a-112">À partir de hello [portail Azure](https://portal.azure.com), sélectionnez **+ nouveau**, **Intelligence + Analytique**, puis sélectionnez **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="b132a-112">From hello [Azure portal](https://portal.azure.com), select **+ NEW**, **Intelligence + Analytics**, and then select **HDInsight**.</span></span>
   
    ![Création d'un cluster HDInsight](./media/hdinsight-apache-kafka-get-started/create-hdinsight.png)

2. <span data-ttu-id="b132a-114">À partir de **notions de base**, entrez hello informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="b132a-114">From **Basics**, enter hello following information:</span></span>

    * <span data-ttu-id="b132a-115">**Nom du cluster**: nom hello du cluster HDInsight de hello.</span><span class="sxs-lookup"><span data-stu-id="b132a-115">**Cluster Name**: hello name of hello HDInsight cluster.</span></span>
    * <span data-ttu-id="b132a-116">**Abonnement**: sélectionnez hello abonnement toouse.</span><span class="sxs-lookup"><span data-stu-id="b132a-116">**Subscription**: Select hello subscription toouse.</span></span>
    * <span data-ttu-id="b132a-117">**Nom d’utilisateur de cluster** et **mot de passe de connexion Cluster**: connexion hello lors de l’accès de cluster de hello via le protocole HTTPS.</span><span class="sxs-lookup"><span data-stu-id="b132a-117">**Cluster login username** and **Cluster login password**: hello login when accessing hello cluster over HTTPS.</span></span> <span data-ttu-id="b132a-118">Vous utilisez ces services de tooaccess des informations d’identification telles que hello l’interface utilisateur de Ambari Web ou l’API REST.</span><span class="sxs-lookup"><span data-stu-id="b132a-118">You use these credentials tooaccess services such as hello Ambari Web UI or REST API.</span></span>
    * <span data-ttu-id="b132a-119">**Secure Shell (SSH) username**: connexion hello utilisée lors de l’accès de cluster de hello via SSH.</span><span class="sxs-lookup"><span data-stu-id="b132a-119">**Secure Shell (SSH) username**: hello login used when accessing hello cluster over SSH.</span></span> <span data-ttu-id="b132a-120">Par défaut, un mot de passe hello est hello identique au mot de passe de connexion hello cluster.</span><span class="sxs-lookup"><span data-stu-id="b132a-120">By default hello password is hello same as hello cluster login password.</span></span>
    * <span data-ttu-id="b132a-121">**Groupe de ressources**: hello ressource groupe toocreate hello cluster.</span><span class="sxs-lookup"><span data-stu-id="b132a-121">**Resource Group**: hello resource group toocreate hello cluster in.</span></span>
    * <span data-ttu-id="b132a-122">**Emplacement**: hello région Azure toocreate hello cluster.</span><span class="sxs-lookup"><span data-stu-id="b132a-122">**Location**: hello Azure region toocreate hello cluster in.</span></span>
   
 ![Sélectionnez un abonnement](./media/hdinsight-apache-kafka-get-started/hdinsight-basic-configuration.png)

3. <span data-ttu-id="b132a-124">Sélectionnez **Cluster type**, puis en suivant hello du jeu de valeurs à partir de **configuration de Cluster**:</span><span class="sxs-lookup"><span data-stu-id="b132a-124">Select **Cluster type**, and then set hello following values from **Cluster configuration**:</span></span>
   
    * <span data-ttu-id="b132a-125">**Type de cluster** : Kafka</span><span class="sxs-lookup"><span data-stu-id="b132a-125">**Cluster Type**: Kafka</span></span>

    * <span data-ttu-id="b132a-126">**Version** : Kafka 0.10.0 (HDI 3.6)</span><span class="sxs-lookup"><span data-stu-id="b132a-126">**Version**: Kafka 0.10.0 (HDI 3.6)</span></span>

    * <span data-ttu-id="b132a-127">**Niveau cluster** : standard</span><span class="sxs-lookup"><span data-stu-id="b132a-127">**Cluster Tier**: Standard</span></span>
     
 <span data-ttu-id="b132a-128">Enfin, utilisez hello **sélectionnez** bouton toosave paramètres.</span><span class="sxs-lookup"><span data-stu-id="b132a-128">Finally, use hello **Select** button toosave settings.</span></span>
     
 ![Sélectionner un type de cluster](./media/hdinsight-apache-kafka-get-started/set-hdinsight-cluster-type.png)

4. <span data-ttu-id="b132a-130">Après avoir sélectionné le type de cluster hello, utilisez hello __sélectionnez__ tooset hello cluster type de bouton.</span><span class="sxs-lookup"><span data-stu-id="b132a-130">After selecting hello cluster type, use hello __Select__ button tooset hello cluster type.</span></span> <span data-ttu-id="b132a-131">Ensuite, utilisez hello __suivant__ configuration de base de toofinish de bouton.</span><span class="sxs-lookup"><span data-stu-id="b132a-131">Next, use hello __Next__ button toofinish basic configuration.</span></span>

5. <span data-ttu-id="b132a-132">À partir du panneau **Stockage**, sélectionnez ou créez un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="b132a-132">From **Storage**, select or create a Storage account.</span></span> <span data-ttu-id="b132a-133">Pour connaître les étapes hello dans ce document, laissez hello autres champs à des valeurs par défaut hello.</span><span class="sxs-lookup"><span data-stu-id="b132a-133">For hello steps in this document, leave hello other fields at hello default values.</span></span> <span data-ttu-id="b132a-134">Hello d’utilisation __suivant__ configuration du stockage toosave bouton.</span><span class="sxs-lookup"><span data-stu-id="b132a-134">Use hello __Next__ button toosave storage configuration.</span></span>

    ![Définir les paramètres de compte de stockage hello pour HDInsight](./media/hdinsight-apache-kafka-get-started/set-hdinsight-storage-account.png)

6. <span data-ttu-id="b132a-136">À partir de __(facultatives) les Applications__, sélectionnez __suivant__ toocontinue.</span><span class="sxs-lookup"><span data-stu-id="b132a-136">From __Applications (optional)__, select __Next__ toocontinue.</span></span> <span data-ttu-id="b132a-137">Cet exemple ne requiert aucune application.</span><span class="sxs-lookup"><span data-stu-id="b132a-137">No applications are required for this example.</span></span>

7. <span data-ttu-id="b132a-138">À partir de __taille de Cluster__, sélectionnez __suivant__ toocontinue.</span><span class="sxs-lookup"><span data-stu-id="b132a-138">From __Cluster size__, select __Next__ toocontinue.</span></span>

    > [!WARNING]
    > <span data-ttu-id="b132a-139">disponibilité tooguarantee de Kafka sur HDInsight, votre cluster doit contenir au moins trois nœuds de travail.</span><span class="sxs-lookup"><span data-stu-id="b132a-139">tooguarantee availability of Kafka on HDInsight, your cluster must contain at least three worker nodes.</span></span>

    ![Ensemble hello taille de cluster Kafka](./media/hdinsight-apache-kafka-get-started/kafka-cluster-size.png)

    > [!NOTE]
    > <span data-ttu-id="b132a-141">Hello **disques par nœud de travail** contrôles d’entrée hello l’évolutivité de Kafka sur HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b132a-141">hello **disks per worker node** entry controls hello scalability of Kafka on HDInsight.</span></span> <span data-ttu-id="b132a-142">Pour plus d’informations, consultez l’article [Configurer le stockage et l’extensibilité pour Apache Kafka sur HDInsight](hdinsight-apache-kafka-scalability.md).</span><span class="sxs-lookup"><span data-stu-id="b132a-142">For more information, see [Configure storage and scalability of Kafka on HDInsight](hdinsight-apache-kafka-scalability.md).</span></span>

8. <span data-ttu-id="b132a-143">À partir de __paramètres avancés__, sélectionnez __suivant__ toocontinue.</span><span class="sxs-lookup"><span data-stu-id="b132a-143">From __Advanced settings__, select __Next__ toocontinue.</span></span>

9. <span data-ttu-id="b132a-144">À partir de hello **Résumé**, passez en revue la configuration hello pour le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="b132a-144">From hello **Summary**, review hello configuration for hello cluster.</span></span> <span data-ttu-id="b132a-145">Hello d’utilisation __modifier__ lie toochange tous les paramètres sont incorrects.</span><span class="sxs-lookup"><span data-stu-id="b132a-145">Use hello __Edit__ links toochange any settings that are incorrect.</span></span> <span data-ttu-id="b132a-146">Enfin, utilisez le cluster de hello toocreate the__Create__ bouton.</span><span class="sxs-lookup"><span data-stu-id="b132a-146">Finally, use the__Create__ button toocreate hello cluster.</span></span>
   
    ![Résumé de la configuration du cluster](./media/hdinsight-apache-kafka-get-started/hdinsight-configuration-summary.png)
   
    > [!NOTE]
    > <span data-ttu-id="b132a-148">Il peut prendre jusqu'à cluster de hello toocreate too20 minutes.</span><span class="sxs-lookup"><span data-stu-id="b132a-148">It can take up too20 minutes toocreate hello cluster.</span></span>

## <a name="connect-toohello-cluster"></a><span data-ttu-id="b132a-149">Se connecter toohello cluster</span><span class="sxs-lookup"><span data-stu-id="b132a-149">Connect toohello cluster</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b132a-150">Lorsque vous effectuez hello comme suit, vous devez utiliser un client SSH.</span><span class="sxs-lookup"><span data-stu-id="b132a-150">When performing hello following steps, you must use an SSH client.</span></span> <span data-ttu-id="b132a-151">Pour plus d’informations, consultez hello [utilisation de SSH avec HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span><span class="sxs-lookup"><span data-stu-id="b132a-151">For more information, see hello [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

<span data-ttu-id="b132a-152">À partir de votre client, utilisez SSH tooconnect toohello cluster :</span><span class="sxs-lookup"><span data-stu-id="b132a-152">From your client, use SSH tooconnect toohello cluster:</span></span>

```ssh SSHUSER@CLUSTERNAME-ssh.azurehdinsight.net```

<span data-ttu-id="b132a-153">Remplacez **SSHUSER** avec nom d’utilisateur SSH de hello vous avez fourni pendant la création du cluster.</span><span class="sxs-lookup"><span data-stu-id="b132a-153">Replace **SSHUSER** with hello SSH username you provided during cluster creation.</span></span> <span data-ttu-id="b132a-154">Remplacez **CLUSTERNAME** avec nom hello du cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="b132a-154">Replace **CLUSTERNAME** with hello name of hello cluster.</span></span>

<span data-ttu-id="b132a-155">Lorsque vous y êtes invité, entrez mot de passe hello utilisé pour hello SSH compte.</span><span class="sxs-lookup"><span data-stu-id="b132a-155">When prompted, enter hello password you used for hello SSH account.</span></span>

<span data-ttu-id="b132a-156">Pour en savoir plus, voir [Utilisation de SSH avec HDInsight (Hadoop) depuis Bash (l’interpréteur de commande) sur Windows 10, Linux, Unix ou OS X](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="b132a-156">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <span data-ttu-id="b132a-157"><a id="getkafkainfo"></a>Obtenir hello soigneur et service Broker pour les informations sur l’hôte</span><span class="sxs-lookup"><span data-stu-id="b132a-157"><a id="getkafkainfo"></a>Get hello Zookeeper and Broker host information</span></span>

<span data-ttu-id="b132a-158">Lorsque vous utilisez Kafka, vous devez connaître les deux valeurs de l’hôte ; Hello *soigneur* hôtes et hello *Broker* hôtes.</span><span class="sxs-lookup"><span data-stu-id="b132a-158">When working with Kafka, you must know two host values; hello *Zookeeper* hosts and hello *Broker* hosts.</span></span> <span data-ttu-id="b132a-159">Ces hôtes sont utilisés avec hello Kafka API et la plupart des utilitaires hello fournis avec Kafka.</span><span class="sxs-lookup"><span data-stu-id="b132a-159">These hosts are used with hello Kafka API and many of hello utilities that ship with Kafka.</span></span>

<span data-ttu-id="b132a-160">Utilisez hello suivant des variables d’environnement toocreate étapes qui contiennent des informations sur l’hôte hello.</span><span class="sxs-lookup"><span data-stu-id="b132a-160">Use hello following steps toocreate environment variables that contain hello host information.</span></span> <span data-ttu-id="b132a-161">Ces variables d’environnement sont utilisés dans les étapes de hello dans ce document.</span><span class="sxs-lookup"><span data-stu-id="b132a-161">These environment variables are used in hello steps in this document.</span></span>

1. <span data-ttu-id="b132a-162">À partir d’un cluster de toohello connexion SSH, suivant de hello utilisez commande tooinstall hello `jq` utilitaire.</span><span class="sxs-lookup"><span data-stu-id="b132a-162">From an SSH connection toohello cluster, use hello following command tooinstall hello `jq` utility.</span></span> <span data-ttu-id="b132a-163">Cet utilitaire est utilisé tooparse documents JSON et est utile lors de la récupération des informations sur l’hôte service broker hello :</span><span class="sxs-lookup"><span data-stu-id="b132a-163">This utility is used tooparse JSON documents, and is useful in retrieving hello broker host information:</span></span>
   
    ```bash
    sudo apt -y install jq
    ```

2. <span data-ttu-id="b132a-164">variables d’environnement hello tooset avec des informations extraites de Ambari, hello utilisation suivant de commandes :</span><span class="sxs-lookup"><span data-stu-id="b132a-164">tooset hello environment variables with information retrieved from Ambari, use hello following commands:</span></span>

    ```bash
    CLUSTERNAME='your cluster name'
    PASSWORD='your cluster password'
    export KAFKAZKHOSTS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/ZOOKEEPER/components/ZOOKEEPER_SERVER | jq -r '["\(.host_components[].HostRoles.host_name):2181"] | join(",")' | cut -d',' -f1,2`

    export KAFKABROKERS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/KAFKA/components/KAFKA_BROKER | jq -r '["\(.host_components[].HostRoles.host_name):9092"] | join(",")' | cut -d',' -f1,2`

    echo '$KAFKAZKHOSTS='$KAFKAZKHOSTS
    echo '$KAFKABROKERS='$KAFKABROKERS
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="b132a-165">Définissez `CLUSTERNAME=` nom toohello Hello cluster de Kafka.</span><span class="sxs-lookup"><span data-stu-id="b132a-165">Set `CLUSTERNAME=` toohello name of hello Kafka cluster.</span></span> <span data-ttu-id="b132a-166">Définissez `PASSWORD=` toohello mot de passe de connexion (admin) vous avez utilisé lors de la création du cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="b132a-166">Set `PASSWORD=` toohello login (admin) password you used when creating hello cluster.</span></span>

    <span data-ttu-id="b132a-167">Hello texte suivant est un exemple de contenu hello de `$KAFKAZKHOSTS`:</span><span class="sxs-lookup"><span data-stu-id="b132a-167">hello following text is an example of hello contents of `$KAFKAZKHOSTS`:</span></span>
   
    `zk0-kafka.eahjefxxp1netdbyklgqj5y1ud.ex.internal.cloudapp.net:2181,zk2-kafka.eahjefxxp1netdbyklgqj5y1ud.ex.internal.cloudapp.net:2181`
   
    <span data-ttu-id="b132a-168">Hello texte suivant est un exemple de contenu hello de `$KAFKABROKERS`:</span><span class="sxs-lookup"><span data-stu-id="b132a-168">hello following text is an example of hello contents of `$KAFKABROKERS`:</span></span>
   
    `wn1-kafka.eahjefxxp1netdbyklgqj5y1ud.cx.internal.cloudapp.net:9092,wn0-kafka.eahjefxxp1netdbyklgqj5y1ud.cx.internal.cloudapp.net:9092`

    > [!NOTE]
    > <span data-ttu-id="b132a-169">Hello `cut` commande est la liste de hello de tootrim utilisé des entrées d’hôte tootwo hôtes.</span><span class="sxs-lookup"><span data-stu-id="b132a-169">hello `cut` command is used tootrim hello list of hosts tootwo host entries.</span></span> <span data-ttu-id="b132a-170">Vous n’avez pas besoin de tooprovide hello la liste complète des ordinateurs hôtes lors de la création d’un consommateur de Kafka ou le producteur.</span><span class="sxs-lookup"><span data-stu-id="b132a-170">You do not need tooprovide hello full list of hosts when creating a Kafka consumer or producer.</span></span>
   
    > [!WARNING]
    > <span data-ttu-id="b132a-171">Ne comptez pas sur les informations de hello retournées à partir de cette session tooalways être précis.</span><span class="sxs-lookup"><span data-stu-id="b132a-171">Do not rely on hello information returned from this session tooalways be accurate.</span></span> <span data-ttu-id="b132a-172">Si vous redimensionnez le cluster de hello, nouveau courtiers sont ajoutés ou supprimés.</span><span class="sxs-lookup"><span data-stu-id="b132a-172">If you scale hello cluster, new brokers are added or removed.</span></span> <span data-ttu-id="b132a-173">Si une défaillance se produit et un nœud est remplacé, le nom d’hôte hello pour le nœud de hello peut changer.</span><span class="sxs-lookup"><span data-stu-id="b132a-173">If a failure occurs and a node is replaced, hello host name for hello node may change.</span></span>
    >
    > <span data-ttu-id="b132a-174">Vous devez récupérer hello soigneur et service Broker pour les informations sur les hôtes dans quelques instants avant de l’utiliser tooensure que vous disposez des informations valides.</span><span class="sxs-lookup"><span data-stu-id="b132a-174">You should retrieve hello Zookeeper and broker hosts information shortly before you use it tooensure you have valid information.</span></span>

## <a name="create-a-topic"></a><span data-ttu-id="b132a-175">Création d'une rubrique</span><span class="sxs-lookup"><span data-stu-id="b132a-175">Create a topic</span></span>

<span data-ttu-id="b132a-176">Kafka stocke les flux de données dans des catégories appelées *rubriques*.</span><span class="sxs-lookup"><span data-stu-id="b132a-176">Kafka stores streams of data in categories called *topics*.</span></span> <span data-ttu-id="b132a-177">À partir de SSH une connexion tooa cluster nœud principal, utilisez un script fourni avec Kafka toocreate une rubrique :</span><span class="sxs-lookup"><span data-stu-id="b132a-177">From An SSH connection tooa cluster headnode, use a script provided with Kafka toocreate a topic:</span></span>

```bash
/usr/hdp/current/kafka-broker/bin/kafka-topics.sh --create --replication-factor 3 --partitions 8 --topic test --zookeeper $KAFKAZKHOSTS
```

<span data-ttu-id="b132a-178">Cette commande connecte à l’aide des informations sur l’hôte hello stockées dans des tooZookeeper `$KAFKAZKHOSTS`, puis créer la rubrique Kafka nommée **test**.</span><span class="sxs-lookup"><span data-stu-id="b132a-178">This command connects tooZookeeper using hello host information stored in `$KAFKAZKHOSTS`, and then create Kafka topic named **test**.</span></span> <span data-ttu-id="b132a-179">Vous pouvez vérifier que cette rubrique hello a été créée à l’aide de hello script toolist rubriques suivantes :</span><span class="sxs-lookup"><span data-stu-id="b132a-179">You can verify that hello topic was created by using hello following script toolist topics:</span></span>

```bash
/usr/hdp/current/kafka-broker/bin/kafka-topics.sh --list --zookeeper $KAFKAZKHOSTS
```

<span data-ttu-id="b132a-180">Hello sortie de cette commande répertorie les rubriques Kafka, qui contient hello **test** rubrique.</span><span class="sxs-lookup"><span data-stu-id="b132a-180">hello output of this command lists Kafka topics, which contains hello **test** topic.</span></span>

## <a name="produce-and-consume-records"></a><span data-ttu-id="b132a-181">Produire et consommer des enregistrements</span><span class="sxs-lookup"><span data-stu-id="b132a-181">Produce and consume records</span></span>

<span data-ttu-id="b132a-182">Kafka stocke les *enregistrements* dans des rubriques.</span><span class="sxs-lookup"><span data-stu-id="b132a-182">Kafka stores *records* in topics.</span></span> <span data-ttu-id="b132a-183">Les enregistrements sont produits par des *producteurs*, et utilisés par des *consommateurs*.</span><span class="sxs-lookup"><span data-stu-id="b132a-183">Records are produced by *producers*, and consumed by *consumers*.</span></span> <span data-ttu-id="b132a-184">Les producteurs récupèrent des enregistrements à partir des *répartiteurs* Kafka.</span><span class="sxs-lookup"><span data-stu-id="b132a-184">Producers retrieve records from Kafka *brokers*.</span></span> <span data-ttu-id="b132a-185">Chaque nœud Worker dans votre cluster HDInsight est un répartiteur Kafka.</span><span class="sxs-lookup"><span data-stu-id="b132a-185">Each worker node in your HDInsight cluster is a Kafka broker.</span></span>

<span data-ttu-id="b132a-186">Utilisez hello suivant les étapes toostore enregistrements dans la rubrique de test hello vous créé précédemment, puis les lire à l’aide d’un consommateur :</span><span class="sxs-lookup"><span data-stu-id="b132a-186">Use hello following steps toostore records into hello test topic you created earlier, and then read them using a consumer:</span></span>

1. <span data-ttu-id="b132a-187">À partir de la session SSH hello, utiliser un script fourni avec la rubrique de toohello Kafka toowrite enregistrements :</span><span class="sxs-lookup"><span data-stu-id="b132a-187">From hello SSH session, use a script provided with Kafka toowrite records toohello topic:</span></span>
   
    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-console-producer.sh --broker-list $KAFKABROKERS --topic test
    ```
   
    <span data-ttu-id="b132a-188">Vous ne sont pas retournés toohello invite après cette commande.</span><span class="sxs-lookup"><span data-stu-id="b132a-188">You are not returned toohello prompt after this command.</span></span> <span data-ttu-id="b132a-189">Au lieu de cela, tapez quelques messages texte, puis utilisez **Ctrl + C** toostop envoi toohello rubrique.</span><span class="sxs-lookup"><span data-stu-id="b132a-189">Instead, type a few text messages and then use **Ctrl + C** toostop sending toohello topic.</span></span> <span data-ttu-id="b132a-190">Chaque ligne est envoyée en tant qu’enregistrement distinct.</span><span class="sxs-lookup"><span data-stu-id="b132a-190">Each line is sent as a separate record.</span></span>

2. <span data-ttu-id="b132a-191">Utiliser un script fourni avec les enregistrements de tooread Kafka à partir de la rubrique de hello :</span><span class="sxs-lookup"><span data-stu-id="b132a-191">Use a script provided with Kafka tooread records from hello topic:</span></span>
   
    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-console-consumer.sh --bootstrap-server $KAFKABROKERS --topic test --from-beginning
    ```
   
    <span data-ttu-id="b132a-192">Cette commande récupère les enregistrements hello à partir de la rubrique de hello et les affiche.</span><span class="sxs-lookup"><span data-stu-id="b132a-192">This command retrieves hello records from hello topic and displays them.</span></span> <span data-ttu-id="b132a-193">À l’aide de `--from-beginning` indique hello consommateur toostart à partir du début de hello du flux de hello, tous les enregistrements sont extraits.</span><span class="sxs-lookup"><span data-stu-id="b132a-193">Using `--from-beginning` tells hello consumer toostart from hello beginning of hello stream, so all records are retrieved.</span></span>

3. <span data-ttu-id="b132a-194">Utilisez __Ctrl + C__ consommateur de hello toostop.</span><span class="sxs-lookup"><span data-stu-id="b132a-194">Use __Ctrl + C__ toostop hello consumer.</span></span>

## <a name="producer-and-consumer-api"></a><span data-ttu-id="b132a-195">API de producteur et de consommateur</span><span class="sxs-lookup"><span data-stu-id="b132a-195">Producer and consumer API</span></span>

<span data-ttu-id="b132a-196">Vous pouvez également programmer produire et consommer des enregistrements à l’aide de hello [Kafka API](http://kafka.apache.org/documentation#api).</span><span class="sxs-lookup"><span data-stu-id="b132a-196">You can also programmatically produce and consume records using hello [Kafka APIs](http://kafka.apache.org/documentation#api).</span></span> <span data-ttu-id="b132a-197">toobuild un producteur de Java et le consommateur, utilisez hello comme suit à partir de votre environnement de développement.</span><span class="sxs-lookup"><span data-stu-id="b132a-197">toobuild a Java producer and consumer, use hello following steps from your development environment.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b132a-198">Vous devez avoir hello suivant des composants installés dans votre environnement de développement :</span><span class="sxs-lookup"><span data-stu-id="b132a-198">You must have hello following components installed in your development environment:</span></span>
>
> * <span data-ttu-id="b132a-199">[Java JDK 8](http://www.oracle.com/technetwork/java/javase/downloads/index.html), ou un équivalent, par exemple, OpenJDK.</span><span class="sxs-lookup"><span data-stu-id="b132a-199">[Java JDK 8](http://www.oracle.com/technetwork/java/javase/downloads/index.html) or an equivalent, such as OpenJDK.</span></span>
>
> * [<span data-ttu-id="b132a-200">Apache Maven</span><span class="sxs-lookup"><span data-stu-id="b132a-200">Apache Maven</span></span>](http://maven.apache.org/)
>
> * <span data-ttu-id="b132a-201">Un client SSH et les hello `scp` commande.</span><span class="sxs-lookup"><span data-stu-id="b132a-201">An SSH client and hello `scp` command.</span></span> <span data-ttu-id="b132a-202">Pour plus d’informations, consultez hello [utilisation de SSH avec HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span><span class="sxs-lookup"><span data-stu-id="b132a-202">For more information, see hello [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

1. <span data-ttu-id="b132a-203">Télécharger les exemples de hello de [https://github.com/Azure-Samples/hdinsight-kafka-java-get-started](https://github.com/Azure-Samples/hdinsight-kafka-java-get-started).</span><span class="sxs-lookup"><span data-stu-id="b132a-203">Download hello examples from [https://github.com/Azure-Samples/hdinsight-kafka-java-get-started](https://github.com/Azure-Samples/hdinsight-kafka-java-get-started).</span></span> <span data-ttu-id="b132a-204">Par exemple de producteur/consommateur hello, utilisez project de hello Bonjour `Producer-Consumer` active.</span><span class="sxs-lookup"><span data-stu-id="b132a-204">For hello producer/consumer example, use hello project in hello `Producer-Consumer` directory.</span></span> <span data-ttu-id="b132a-205">Cet exemple contient hello classes suivantes :</span><span class="sxs-lookup"><span data-stu-id="b132a-205">This example contains hello following classes:</span></span>
   
    * <span data-ttu-id="b132a-206">**Exécutez** -démarre le consommateur de hello ou le producteur.</span><span class="sxs-lookup"><span data-stu-id="b132a-206">**Run** - starts either hello consumer or producer.</span></span>

    * <span data-ttu-id="b132a-207">**Producteur** -magasins 1 000 000 enregistrements toohello rubrique.</span><span class="sxs-lookup"><span data-stu-id="b132a-207">**Producer** - stores 1,000,000 records toohello topic.</span></span>

    * <span data-ttu-id="b132a-208">**Consommateur** -lit les enregistrements à partir de la rubrique de hello.</span><span class="sxs-lookup"><span data-stu-id="b132a-208">**Consumer** - reads records from hello topic.</span></span>

2. <span data-ttu-id="b132a-209">toocreate un package jar, répertoires toohello de déplacer hello `Producer-Consumer` active et l’utilisation hello commande suivante :</span><span class="sxs-lookup"><span data-stu-id="b132a-209">toocreate a jar package, change directories toohello location of hello `Producer-Consumer` directory and use hello following command:</span></span>

    ```
    mvn clean package
    ```

    <span data-ttu-id="b132a-210">Cette commande crée un répertoire nommé `target`, qui contient un fichier nommé `kafka-producer-consumer-1.0-SNAPSHOT.jar`.</span><span class="sxs-lookup"><span data-stu-id="b132a-210">This command creates a directory named `target`, that contains a file named `kafka-producer-consumer-1.0-SNAPSHOT.jar`.</span></span>

3. <span data-ttu-id="b132a-211">Toocopy hello des commandes suivantes de hello utilisation `kafka-producer-consumer-1.0-SNAPSHOT.jar` HDInsight tooyour de fichiers :</span><span class="sxs-lookup"><span data-stu-id="b132a-211">Use hello following commands toocopy hello `kafka-producer-consumer-1.0-SNAPSHOT.jar` file tooyour HDInsight cluster:</span></span>
   
    ```bash
    scp ./target/kafka-producer-consumer-1.0-SNAPSHOT.jar SSHUSER@CLUSTERNAME-ssh.azurehdinsight.net:kafka-producer-consumer.jar
    ```
   
    <span data-ttu-id="b132a-212">Remplacez **SSHUSER** avec l’utilisateur SSH hello pour votre cluster, puis remplacez **CLUSTERNAME** avec nom hello de votre cluster.</span><span class="sxs-lookup"><span data-stu-id="b132a-212">Replace **SSHUSER** with hello SSH user for your cluster, and replace **CLUSTERNAME** with hello name of your cluster.</span></span> <span data-ttu-id="b132a-213">Lorsque vous y êtes invité entrez hello le mot de passe utilisateur SSH hello.</span><span class="sxs-lookup"><span data-stu-id="b132a-213">When prompted enter hello password for hello SSH user.</span></span>

4. <span data-ttu-id="b132a-214">Une fois hello `scp` commande a fini de copier le fichier de hello, connectez le cluster de toohello à l’aide de SSH.</span><span class="sxs-lookup"><span data-stu-id="b132a-214">Once hello `scp` command finishes copying hello file, connect toohello cluster using SSH.</span></span> <span data-ttu-id="b132a-215">Utilisez hello commande toowrite enregistrements toohello test rubrique suivante :</span><span class="sxs-lookup"><span data-stu-id="b132a-215">Use hello following command toowrite records toohello test topic:</span></span>

    ```bash
    java -jar kafka-producer-consumer.jar producer $KAFKABROKERS
    ```

5. <span data-ttu-id="b132a-216">Une fois que hello est terminée, utilisez hello suivant tooread de commande à partir de la rubrique de hello :</span><span class="sxs-lookup"><span data-stu-id="b132a-216">Once hello process has finished, use hello following command tooread from hello topic:</span></span>
   
    ```bash
    java -jar kafka-producer-consumer.jar consumer $KAFKABROKERS
    ```
   
    <span data-ttu-id="b132a-217">enregistrements Hello lire, ainsi que d’un nombre d’enregistrements, s’affiche.</span><span class="sxs-lookup"><span data-stu-id="b132a-217">hello records read, along with a count of records, is displayed.</span></span> <span data-ttu-id="b132a-218">Vous pouvez voir quelques exemples plus de 1 000 000 connecté comme vous avez envoyé la rubrique de toohello plusieurs enregistrements à l’aide d’un script dans une étape antérieure.</span><span class="sxs-lookup"><span data-stu-id="b132a-218">You may see a few more than 1,000,000 logged as you sent several records toohello topic using a script in an earlier step.</span></span>

6. <span data-ttu-id="b132a-219">Utilisez __Ctrl + C__ consommateur de hello tooexit.</span><span class="sxs-lookup"><span data-stu-id="b132a-219">Use __Ctrl + C__ tooexit hello consumer.</span></span>

### <a name="multiple-consumers"></a><span data-ttu-id="b132a-220">Consommateurs multiples</span><span class="sxs-lookup"><span data-stu-id="b132a-220">Multiple consumers</span></span>

<span data-ttu-id="b132a-221">Les consommateurs Kafka utilisent un groupe de consommateurs lors de la lecture des enregistrements.</span><span class="sxs-lookup"><span data-stu-id="b132a-221">Kafka consumers use a consumer group when reading records.</span></span> <span data-ttu-id="b132a-222">À l’aide de hello de groupe avec plusieurs consommateurs entraîne charge équilibrée lectures à partir d’une rubrique.</span><span class="sxs-lookup"><span data-stu-id="b132a-222">Using hello same group with multiple consumers results in load balanced reads from a topic.</span></span> <span data-ttu-id="b132a-223">Chaque consommateur dans le groupe de hello reçoit une partie des enregistrements de hello.</span><span class="sxs-lookup"><span data-stu-id="b132a-223">Each consumer in hello group receives a portion of hello records.</span></span> <span data-ttu-id="b132a-224">toosee étapes de ce processus en action, hello utilisation suivant :</span><span class="sxs-lookup"><span data-stu-id="b132a-224">toosee this process in action, use hello following steps:</span></span>

1. <span data-ttu-id="b132a-225">Ouvrez un nouveau cluster de toohello de session SSH, afin que vous ayez deux d'entre eux.</span><span class="sxs-lookup"><span data-stu-id="b132a-225">Open a new SSH session toohello cluster, so that you have two of them.</span></span> <span data-ttu-id="b132a-226">Dans chaque session, utilisez hello suivant toostart un consommateur avec hello même ID de groupe de consommateurs :</span><span class="sxs-lookup"><span data-stu-id="b132a-226">In each session, use hello following toostart a consumer with hello same consumer group ID:</span></span>
   
    ```bash
    java -jar kafka-producer-consumer.jar consumer $KAFKABROKERS mygroup
    ```

    <span data-ttu-id="b132a-227">Cette commande démarre un consommateur à l’aide des ID de groupe hello `mygroup`.</span><span class="sxs-lookup"><span data-stu-id="b132a-227">This command starts a consumer using hello group ID `mygroup`.</span></span>

    > [!NOTE]
    > <span data-ttu-id="b132a-228">Utilisez les commandes hello hello [obtenir hello soigneur et service Broker pour les informations sur l’hôte](#getkafkainfo) section tooset `$KAFKABROKERS` pour cette session SSH.</span><span class="sxs-lookup"><span data-stu-id="b132a-228">Use hello commands in hello [Get hello Zookeeper and Broker host information](#getkafkainfo) section tooset `$KAFKABROKERS` for this SSH session.</span></span>

2. <span data-ttu-id="b132a-229">Observez comment chaque enregistrements de hello de nombres de session qu’il reçoit à partir de la rubrique de hello.</span><span class="sxs-lookup"><span data-stu-id="b132a-229">Watch as each session counts hello records it receives from hello topic.</span></span> <span data-ttu-id="b132a-230">total Hello de deux sessions doit être hello même que vous avez reçu précédemment à partir d’un seul client.</span><span class="sxs-lookup"><span data-stu-id="b132a-230">hello total of both sessions should be hello same as you received previously from one consumer.</span></span>

<span data-ttu-id="b132a-231">Consommation par des clients dans le même groupe est géré par le biais des partitions pour une rubrique de hello hello de hello.</span><span class="sxs-lookup"><span data-stu-id="b132a-231">Consumption by clients within hello same group is handled through hello partitions for hello topic.</span></span> <span data-ttu-id="b132a-232">Pourquoi `test` rubrique créée précédemment, il a huit partitions.</span><span class="sxs-lookup"><span data-stu-id="b132a-232">For hello `test` topic created earlier, it has eight partitions.</span></span> <span data-ttu-id="b132a-233">Si vous ouvrez huit sessions SSH et lancez un consommateur de toutes les sessions, chaque consommateur lit les enregistrements à partir d’une seule partition pour une rubrique de hello.</span><span class="sxs-lookup"><span data-stu-id="b132a-233">If you open eight SSH sessions and launch a consumer in all sessions, each consumer reads records from a single partition for hello topic.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b132a-234">Il ne peut pas y avoir plus d’instances de consommateurs dans un groupe de consommateurs que de partitions.</span><span class="sxs-lookup"><span data-stu-id="b132a-234">There cannot be more consumer instances in a consumer group than partitions.</span></span> <span data-ttu-id="b132a-235">Dans cet exemple, un groupe de consommateurs peut contenir des consommateurs de tooeight puisque c’est le nombre de hello de partitions dans la rubrique de hello.</span><span class="sxs-lookup"><span data-stu-id="b132a-235">In this example, one consumer group can contain up tooeight consumers since that is hello number of partitions in hello topic.</span></span> <span data-ttu-id="b132a-236">Vous pouvez également disposer de plusieurs groupes de consommateurs, chacun ne dépassant pas huit consommateurs.</span><span class="sxs-lookup"><span data-stu-id="b132a-236">Or you can have multiple consumer groups, each with no more than eight consumers.</span></span>

<span data-ttu-id="b132a-237">Enregistrements stockés dans Kafka sont stockées dans l’ordre de hello qu’ils sont reçus au sein d’une partition.</span><span class="sxs-lookup"><span data-stu-id="b132a-237">Records stored in Kafka are stored in hello order they are received within a partition.</span></span> <span data-ttu-id="b132a-238">tooachieve dans-livraison chronologique des messages pour les enregistrements *au sein d’une partition*, créez un groupe de consommateurs où hello nombre d’instances de consommateur correspond au nombre de hello de partitions.</span><span class="sxs-lookup"><span data-stu-id="b132a-238">tooachieve in-ordered delivery for records *within a partition*, create a consumer group where hello number of consumer instances matches hello number of partitions.</span></span> <span data-ttu-id="b132a-239">tooachieve dans-livraison chronologique des messages pour les enregistrements *au sein de la rubrique de hello*, créez un groupe de consommateurs avec une instance de consommateur qu’un seul.</span><span class="sxs-lookup"><span data-stu-id="b132a-239">tooachieve in-ordered delivery for records *within hello topic*, create a consumer group with only one consumer instance.</span></span>

## <a name="streaming-api"></a><span data-ttu-id="b132a-240">API de diffusion en continu</span><span class="sxs-lookup"><span data-stu-id="b132a-240">Streaming API</span></span>

<span data-ttu-id="b132a-241">Hello API de diffusion en continu a été ajoutée tooKafka dans la version 0.10.0 ; les versions antérieures s’appuient sur Apache Spark ou Storm pour le traitement de flux de données.</span><span class="sxs-lookup"><span data-stu-id="b132a-241">hello streaming API was added tooKafka in version 0.10.0; earlier versions rely on Apache Spark or Storm for stream processing.</span></span>

1. <span data-ttu-id="b132a-242">Si vous n’avez pas déjà fait, téléchargez les exemples hello à partir de [https://github.com/Azure-Samples/hdinsight-kafka-java-get-started](https://github.com/Azure-Samples/hdinsight-kafka-java-get-started) tooyour les environnement de développement.</span><span class="sxs-lookup"><span data-stu-id="b132a-242">If you haven't already done so, download hello examples from [https://github.com/Azure-Samples/hdinsight-kafka-java-get-started](https://github.com/Azure-Samples/hdinsight-kafka-java-get-started) tooyour development environment.</span></span> <span data-ttu-id="b132a-243">Pour un exemple de diffusion en continu de hello, utilisez project de hello Bonjour `streaming` active.</span><span class="sxs-lookup"><span data-stu-id="b132a-243">For hello streaming example, use hello project in hello `streaming` directory.</span></span>
   
    <span data-ttu-id="b132a-244">Ce projet contient une seule classe, `Stream`, qui lit les enregistrements d’hello `test` rubrique créée précédemment.</span><span class="sxs-lookup"><span data-stu-id="b132a-244">This project contains only one class, `Stream`, which reads records from hello `test` topic created previously.</span></span> <span data-ttu-id="b132a-245">Elle compte mots hello lire et émet chaque rubrique tooa word et nombre nommée `wordcounts`.</span><span class="sxs-lookup"><span data-stu-id="b132a-245">It counts hello words read, and emits each word and count tooa topic named `wordcounts`.</span></span> <span data-ttu-id="b132a-246">Hello `wordcounts` rubrique est créée dans une étape ultérieure de cette section.</span><span class="sxs-lookup"><span data-stu-id="b132a-246">hello `wordcounts` topic is created in a later step in this section.</span></span>

2. <span data-ttu-id="b132a-247">À partir de la ligne de commande hello dans votre environnement de développement, modifier l’emplacement de toohello répertoires de hello `Streaming` répertoire, puis hello utilisation suivant commande toocreate un package jar :</span><span class="sxs-lookup"><span data-stu-id="b132a-247">From hello command line in your development environment, change directories toohello location of hello `Streaming` directory, and then use hello following command toocreate a jar package:</span></span>

    ```bash
    mvn clean package
    ```

    <span data-ttu-id="b132a-248">Cette commande crée un répertoire nommé `target`, qui contient un fichier nommé `kafka-streaming-1.0-SNAPSHOT.jar`.</span><span class="sxs-lookup"><span data-stu-id="b132a-248">This command creates a directory named `target`, which contains a file named `kafka-streaming-1.0-SNAPSHOT.jar`.</span></span>

3. <span data-ttu-id="b132a-249">Toocopy hello des commandes suivantes de hello utilisation `kafka-streaming-1.0-SNAPSHOT.jar` HDInsight tooyour de fichiers :</span><span class="sxs-lookup"><span data-stu-id="b132a-249">Use hello following commands toocopy hello `kafka-streaming-1.0-SNAPSHOT.jar` file tooyour HDInsight cluster:</span></span>
   
    ```bash
    scp ./target/kafka-streaming-1.0-SNAPSHOT.jar SSHUSER@CLUSTERNAME-ssh.azurehdinsight.net:kafka-streaming.jar
    ```
   
    <span data-ttu-id="b132a-250">Remplacez **SSHUSER** avec l’utilisateur SSH hello pour votre cluster, puis remplacez **CLUSTERNAME** avec nom hello de votre cluster.</span><span class="sxs-lookup"><span data-stu-id="b132a-250">Replace **SSHUSER** with hello SSH user for your cluster, and replace **CLUSTERNAME** with hello name of your cluster.</span></span> <span data-ttu-id="b132a-251">Lorsque vous y êtes invité entrez hello le mot de passe utilisateur SSH hello.</span><span class="sxs-lookup"><span data-stu-id="b132a-251">When prompted enter hello password for hello SSH user.</span></span>

4. <span data-ttu-id="b132a-252">Une fois hello `scp` commande a fini de copier le fichier de hello, connectez le cluster de toohello à l’aide de SSH et l’utiliser hello suivant commande toocreate hello `wordcounts` rubrique :</span><span class="sxs-lookup"><span data-stu-id="b132a-252">Once hello `scp` command finishes copying hello file, connect toohello cluster using SSH, and then use hello following command toocreate hello `wordcounts` topic:</span></span>

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --create --replication-factor 3 --partitions 8 --topic wordcounts --zookeeper $KAFKAZKHOSTS
    ```

5. <span data-ttu-id="b132a-253">Ensuite, démarrez hello processus de diffusion en continu à l’aide de hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="b132a-253">Next, start hello streaming process by using hello following command:</span></span>
   
    ```bash
    java -jar kafka-streaming.jar $KAFKABROKERS $KAFKAZKHOSTS 2>/dev/null &
    ```
   
    <span data-ttu-id="b132a-254">Cette commande démarre hello processus en arrière-plan de hello de diffusion en continu.</span><span class="sxs-lookup"><span data-stu-id="b132a-254">This command starts hello streaming process in hello background.</span></span>

6. <span data-ttu-id="b132a-255">Suivant de hello utilisez commande toosend messages toohello `test` rubrique.</span><span class="sxs-lookup"><span data-stu-id="b132a-255">Use hello following command toosend messages toohello `test` topic.</span></span> <span data-ttu-id="b132a-256">Ces messages sont traités par hello exemple de diffusion en continu :</span><span class="sxs-lookup"><span data-stu-id="b132a-256">These messages are processed by hello streaming example:</span></span>
   
    ```bash
    java -jar kafka-producer-consumer.jar producer $KAFKABROKERS &>/dev/null &
    ```

7. <span data-ttu-id="b132a-257">Hello d’utilisation après la sortie de la commande tooview hello écrit toohello `wordcounts` rubrique par hello processus de diffusion en continu :</span><span class="sxs-lookup"><span data-stu-id="b132a-257">Use hello following command tooview hello output that is written toohello `wordcounts` topic by hello streaming process:</span></span>
   
    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-console-consumer.sh --bootstrap-server $KAFKABROKERS --topic wordcounts --from-beginning --formatter kafka.tools.DefaultMessageFormatter --property print.key=true --property key.deserializer=org.apache.kafka.common.serialization.StringDeserializer --property value.deserializer=org.apache.kafka.common.serialization.LongDeserializer
    ```
   
    > [!NOTE]
    > <span data-ttu-id="b132a-258">les données de salutation tooview, vous devez indiquer à hello tooprint hello clé et toouse de désérialiseur hello pour hello clé et la valeur.</span><span class="sxs-lookup"><span data-stu-id="b132a-258">tooview hello data, you must tell hello consumer tooprint hello key and hello deserializer toouse for hello key and value.</span></span> <span data-ttu-id="b132a-259">nom de la clé Hello est word de hello et valeur de clé hello contient le nombre de hello.</span><span class="sxs-lookup"><span data-stu-id="b132a-259">hello key name is hello word, and hello key value contains hello count.</span></span>
   
    <span data-ttu-id="b132a-260">Hello est similaire toohello suivant texte de sortie :</span><span class="sxs-lookup"><span data-stu-id="b132a-260">hello output is similar toohello following text:</span></span>
   
        dwarfs  13635
        ago     13664
        snow    13636
        dwarfs  13636
        ago     13665
        a       13803
        ago     13666
        a       13804
        ago     13667
        ago     13668
        jumped  13640
        jumped  13641
        a       13805
        snow    13637
   
    > [!NOTE]
    > <span data-ttu-id="b132a-261">nombre de Hello est incrémenté à chaque fois un mot est rencontré.</span><span class="sxs-lookup"><span data-stu-id="b132a-261">hello count increments each time a word is encountered.</span></span>

7. <span data-ttu-id="b132a-262">Utilisez hello __Ctrl + C__ tooexit hello consommateur, puis utilisez hello `fg` commande toobring hello au premier plan de diffusion en continu en arrière-plan tâche toohello précédent.</span><span class="sxs-lookup"><span data-stu-id="b132a-262">Use hello __Ctrl + C__ tooexit hello consumer, then use hello `fg` command toobring hello streaming background task back toohello foreground.</span></span> <span data-ttu-id="b132a-263">Utilisez __Ctrl + C__ tooexit il également.</span><span class="sxs-lookup"><span data-stu-id="b132a-263">Use __Ctrl + C__ tooexit it also.</span></span>

## <a name="delete-hello-cluster"></a><span data-ttu-id="b132a-264">Supprimer le cluster de hello</span><span class="sxs-lookup"><span data-stu-id="b132a-264">Delete hello cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="troubleshoot"></a><span data-ttu-id="b132a-265">Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="b132a-265">Troubleshoot</span></span>

<span data-ttu-id="b132a-266">Si vous rencontrez des problèmes lors de la création de clusters HDInsight, reportez-vous aux [exigences de contrôle d’accès](hdinsight-administer-use-portal-linux.md#create-clusters).</span><span class="sxs-lookup"><span data-stu-id="b132a-266">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b132a-267">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b132a-267">Next steps</span></span>

<span data-ttu-id="b132a-268">Dans ce document, vous avez appris les notions de base de hello de l’utilisation de Kafka Apache sur HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b132a-268">In this document, you have learned hello basics of working with Apache Kafka on HDInsight.</span></span> <span data-ttu-id="b132a-269">Utilisez hello suivant toolearn plus sur l’utilisation de Kafka :</span><span class="sxs-lookup"><span data-stu-id="b132a-269">Use hello following toolearn more about working with Kafka:</span></span>

* [<span data-ttu-id="b132a-270">Garantir une haute disponibilité de vos données avec Apache Kafka sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="b132a-270">Ensure high availability of your data with Kafka on HDInsight</span></span>](hdinsight-apache-kafka-high-availability.md)
* [<span data-ttu-id="b132a-271">Configurer le stockage et l’extensibilité pour Apache Kafka sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="b132a-271">Increase scalability by configuring managed disks with Kafka on HDInsight</span></span>](hdinsight-apache-kafka-scalability.md)
* <span data-ttu-id="b132a-272">[Documentation Apache Kafka](http://kafka.apache.org/documentation.html) à l’adresse kafka.apache.org.</span><span class="sxs-lookup"><span data-stu-id="b132a-272">[Apache Kafka documentation](http://kafka.apache.org/documentation.html) at kafka.apache.org.</span></span>
* [<span data-ttu-id="b132a-273">Utilisez MirrorMaker toocreate un réplica de Kafka sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="b132a-273">Use MirrorMaker toocreate a replica of Kafka on HDInsight</span></span>](hdinsight-apache-kafka-mirroring.md)
* [<span data-ttu-id="b132a-274">Utilisation d’Apache Storm avec Kafka sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="b132a-274">Use Apache Storm with Kafka on HDInsight</span></span>](hdinsight-apache-storm-with-kafka.md)
* <span data-ttu-id="b132a-275">[Use Apache Spark with Kafka on HDInsight](hdinsight-apache-spark-with-kafka.md) (Utilisation d’Apache Spark avec Kafka sur HDInsight)</span><span class="sxs-lookup"><span data-stu-id="b132a-275">[Use Apache Spark with Kafka on HDInsight](hdinsight-apache-spark-with-kafka.md)</span></span>
* [<span data-ttu-id="b132a-276">Se connecter tooKafka via un réseau virtuel Azure</span><span class="sxs-lookup"><span data-stu-id="b132a-276">Connect tooKafka through an Azure Virtual Network</span></span>](hdinsight-apache-kafka-connect-vpn-gateway.md)
