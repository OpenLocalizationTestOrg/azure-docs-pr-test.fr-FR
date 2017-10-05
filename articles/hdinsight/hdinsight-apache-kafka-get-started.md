---
title: "Démarrer avec Apache Kafka - Azure HDInsight | Microsoft Docs"
description: "Découvrez comment créer un cluster Apache Kafka sur Azure HDInsight. Découvrez comment créer des rubriques, des abonnés et des consommateurs."
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
ms.openlocfilehash: 03e6996f0f44e04978080b3bd267e924f342b7fc
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="start-with-apache-kafka-preview-on-hdinsight"></a><span data-ttu-id="80e05-104">Démarrer avec Apache Kafka (version préliminaire) sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="80e05-104">Start with Apache Kafka (preview) on HDInsight</span></span>

<span data-ttu-id="80e05-105">Découvrez comment créer et utiliser un cluster [Apache Kafka](https://kafka.apache.org) sur Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="80e05-105">Learn how to create and use an [Apache Kafka](https://kafka.apache.org) cluster on Azure HDInsight.</span></span> <span data-ttu-id="80e05-106">Kafka est une plateforme de diffusion en continu distribuée open source, disponible avec HDInsight.</span><span class="sxs-lookup"><span data-stu-id="80e05-106">Kafka is an open-source, distributed streaming platform that is available with HDInsight.</span></span> <span data-ttu-id="80e05-107">Elle est souvent utilisée comme répartiteur de messages, car elle fournit des fonctionnalités similaires à une file d’attente de messages de publication/d’abonnement.</span><span class="sxs-lookup"><span data-stu-id="80e05-107">It is often used as a message broker, as it provides functionality similar to a publish-subscribe message queue.</span></span>

> [!NOTE]
> <span data-ttu-id="80e05-108">Il existe actuellement deux versions de Kafka disponibles avec HDInsight ; 0.9.0 (HDInsight 3.4) et 0.10.0 (HDInsight 3.5 et 3.6).</span><span class="sxs-lookup"><span data-stu-id="80e05-108">There are currently two versions of Kafka available with HDInsight; 0.9.0 (HDInsight 3.4) and 0.10.0 (HDInsight 3.5 and 3.6).</span></span> <span data-ttu-id="80e05-109">Les étapes décrites dans ce document supposent que vous utilisez Kafka sur HDInsight 3.6.</span><span class="sxs-lookup"><span data-stu-id="80e05-109">The steps in this document assume that you are using Kafka on HDInsight 3.6.</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="create-a-kafka-cluster"></a><span data-ttu-id="80e05-110">Création d’un cluster Kafka</span><span class="sxs-lookup"><span data-stu-id="80e05-110">Create a Kafka cluster</span></span>

<span data-ttu-id="80e05-111">Utilisez les étapes suivantes pour créer un Kafka sur un cluster HDInsight :</span><span class="sxs-lookup"><span data-stu-id="80e05-111">Use the following steps to create a Kafka on HDInsight cluster:</span></span>

1. <span data-ttu-id="80e05-112">À partir du [portail Azure](https://portal.azure.com), sélectionnez **+ et Nouveau**, **Intelligence et analyse**, puis **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="80e05-112">From the [Azure portal](https://portal.azure.com), select **+ NEW**, **Intelligence + Analytics**, and then select **HDInsight**.</span></span>
   
    ![Création d'un cluster HDInsight](./media/hdinsight-apache-kafka-get-started/create-hdinsight.png)

2. <span data-ttu-id="80e05-114">À partir du panneau **Informations de base**, entrez les informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="80e05-114">From **Basics**, enter the following information:</span></span>

    * <span data-ttu-id="80e05-115">**Nom du cluster** : nom du cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="80e05-115">**Cluster Name**: The name of the HDInsight cluster.</span></span>
    * <span data-ttu-id="80e05-116">**Abonnement** : sélectionnez l'abonnement souhaité.</span><span class="sxs-lookup"><span data-stu-id="80e05-116">**Subscription**: Select the subscription to use.</span></span>
    * <span data-ttu-id="80e05-117">**Nom d’utilisateur de connexion du cluster** et **Mot de passe de connexion du cluster** : les informations de connexion lors de l’accès au cluster sur HTTPS.</span><span class="sxs-lookup"><span data-stu-id="80e05-117">**Cluster login username** and **Cluster login password**: The login when accessing the cluster over HTTPS.</span></span> <span data-ttu-id="80e05-118">Vous utilisez ces informations d’identification pour accéder aux services tels que l’interface utilisateur Ambari Web ou l’API REST.</span><span class="sxs-lookup"><span data-stu-id="80e05-118">You use these credentials to access services such as the Ambari Web UI or REST API.</span></span>
    * <span data-ttu-id="80e05-119">**Nom d’utilisateur Secure Shell (SSH)** : information de connexion utilisée lors de l’accès au cluster sur SSH.</span><span class="sxs-lookup"><span data-stu-id="80e05-119">**Secure Shell (SSH) username**: The login used when accessing the cluster over SSH.</span></span> <span data-ttu-id="80e05-120">Par défaut, le mot de passe est le même que le mot de passe de connexion de cluster.</span><span class="sxs-lookup"><span data-stu-id="80e05-120">By default the password is the same as the cluster login password.</span></span>
    * <span data-ttu-id="80e05-121">**Groupe de ressources** : groupe de ressources dans lequel créer le cluster.</span><span class="sxs-lookup"><span data-stu-id="80e05-121">**Resource Group**: The resource group to create the cluster in.</span></span>
    * <span data-ttu-id="80e05-122">**Emplacement** : la région Azure dans laquelle créer le cluster.</span><span class="sxs-lookup"><span data-stu-id="80e05-122">**Location**: The Azure region to create the cluster in.</span></span>
   
 ![Sélectionnez un abonnement](./media/hdinsight-apache-kafka-get-started/hdinsight-basic-configuration.png)

3. <span data-ttu-id="80e05-124">Sélectionnez le **Type de cluster**, puis définissez les valeurs suivantes sur le panneau **Configuration du cluster** :</span><span class="sxs-lookup"><span data-stu-id="80e05-124">Select **Cluster type**, and then set the following values from **Cluster configuration**:</span></span>
   
    * <span data-ttu-id="80e05-125">**Type de cluster** : Kafka</span><span class="sxs-lookup"><span data-stu-id="80e05-125">**Cluster Type**: Kafka</span></span>

    * <span data-ttu-id="80e05-126">**Version** : Kafka 0.10.0 (HDI 3.6)</span><span class="sxs-lookup"><span data-stu-id="80e05-126">**Version**: Kafka 0.10.0 (HDI 3.6)</span></span>

    * <span data-ttu-id="80e05-127">**Niveau cluster** : standard</span><span class="sxs-lookup"><span data-stu-id="80e05-127">**Cluster Tier**: Standard</span></span>
     
 <span data-ttu-id="80e05-128">Enfin, utilisez le bouton **Sélectionner** pour enregistrer les paramètres.</span><span class="sxs-lookup"><span data-stu-id="80e05-128">Finally, use the **Select** button to save settings.</span></span>
     
 ![Sélectionner un type de cluster](./media/hdinsight-apache-kafka-get-started/set-hdinsight-cluster-type.png)

4. <span data-ttu-id="80e05-130">Après avoir sélectionné le type de cluster, utilisez le bouton __Sélectionner__ pour définir le type de cluster.</span><span class="sxs-lookup"><span data-stu-id="80e05-130">After selecting the cluster type, use the __Select__ button to set the cluster type.</span></span> <span data-ttu-id="80e05-131">Ensuite, utilisez le bouton __Suivant__ bouton pour terminer la configuration de base.</span><span class="sxs-lookup"><span data-stu-id="80e05-131">Next, use the __Next__ button to finish basic configuration.</span></span>

5. <span data-ttu-id="80e05-132">À partir du panneau **Stockage**, sélectionnez ou créez un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="80e05-132">From **Storage**, select or create a Storage account.</span></span> <span data-ttu-id="80e05-133">Concernant les étapes de ce document, laissez les autres champs sur leurs valeurs par défaut.</span><span class="sxs-lookup"><span data-stu-id="80e05-133">For the steps in this document, leave the other fields at the default values.</span></span> <span data-ttu-id="80e05-134">Utilisez le bouton __Suivant__ pour enregistrer la configuration de stockage.</span><span class="sxs-lookup"><span data-stu-id="80e05-134">Use the __Next__ button to save storage configuration.</span></span>

    ![Définir les paramètres de compte de stockage pour HDInsight](./media/hdinsight-apache-kafka-get-started/set-hdinsight-storage-account.png)

6. <span data-ttu-id="80e05-136">Dans le panneau __Applications (facultatif)__, sélectionnez __Suivant__ pour continuer.</span><span class="sxs-lookup"><span data-stu-id="80e05-136">From __Applications (optional)__, select __Next__ to continue.</span></span> <span data-ttu-id="80e05-137">Cet exemple ne requiert aucune application.</span><span class="sxs-lookup"><span data-stu-id="80e05-137">No applications are required for this example.</span></span>

7. <span data-ttu-id="80e05-138">Dans le panneau __Taille du cluster__, sélectionnez __Suivant__ pour continuer.</span><span class="sxs-lookup"><span data-stu-id="80e05-138">From __Cluster size__, select __Next__ to continue.</span></span>

    > [!WARNING]
    > <span data-ttu-id="80e05-139">Pour garantir la disponibilité de Kafka sur HDInsight, votre cluster doit contenir au moins trois nœuds Worker.</span><span class="sxs-lookup"><span data-stu-id="80e05-139">To guarantee availability of Kafka on HDInsight, your cluster must contain at least three worker nodes.</span></span>

    ![Définir la taille du cluster Kafka](./media/hdinsight-apache-kafka-get-started/kafka-cluster-size.png)

    > [!NOTE]
    > <span data-ttu-id="80e05-141">L’entrée relative aux **disques par nœud Worker** détermine l’extensibilité de Kafka sur HDInsight.</span><span class="sxs-lookup"><span data-stu-id="80e05-141">The **disks per worker node** entry controls the scalability of Kafka on HDInsight.</span></span> <span data-ttu-id="80e05-142">Pour plus d’informations, consultez l’article [Configurer le stockage et l’extensibilité pour Apache Kafka sur HDInsight](hdinsight-apache-kafka-scalability.md).</span><span class="sxs-lookup"><span data-stu-id="80e05-142">For more information, see [Configure storage and scalability of Kafka on HDInsight](hdinsight-apache-kafka-scalability.md).</span></span>

8. <span data-ttu-id="80e05-143">Dans le panneau __Paramètres avancés__, sélectionnez __Suivant__ pour continuer.</span><span class="sxs-lookup"><span data-stu-id="80e05-143">From __Advanced settings__, select __Next__ to continue.</span></span>

9. <span data-ttu-id="80e05-144">Dans le panneau **Résumé**, passez en revue la configuration du cluster.</span><span class="sxs-lookup"><span data-stu-id="80e05-144">From the **Summary**, review the configuration for the cluster.</span></span> <span data-ttu-id="80e05-145">Utilisez les liens __Modifier__ pour modifier les éventuels paramètres incorrects.</span><span class="sxs-lookup"><span data-stu-id="80e05-145">Use the __Edit__ links to change any settings that are incorrect.</span></span> <span data-ttu-id="80e05-146">Pour finir, cliquez sur le bouton __Créer__ pour créer le cluster.</span><span class="sxs-lookup"><span data-stu-id="80e05-146">Finally, use the__Create__ button to create the cluster.</span></span>
   
    ![Résumé de la configuration du cluster](./media/hdinsight-apache-kafka-get-started/hdinsight-configuration-summary.png)
   
    > [!NOTE]
    > <span data-ttu-id="80e05-148">La création du cluster peut prendre jusqu’à 20 minutes.</span><span class="sxs-lookup"><span data-stu-id="80e05-148">It can take up to 20 minutes to create the cluster.</span></span>

## <a name="connect-to-the-cluster"></a><span data-ttu-id="80e05-149">Connexion au cluster</span><span class="sxs-lookup"><span data-stu-id="80e05-149">Connect to the cluster</span></span>

> [!IMPORTANT]
> <span data-ttu-id="80e05-150">Lorsque vous effectuez les étapes suivantes, vous devez utiliser un client SSH.</span><span class="sxs-lookup"><span data-stu-id="80e05-150">When performing the following steps, you must use an SSH client.</span></span> <span data-ttu-id="80e05-151">Pour plus d’informations, consultez le document [Utiliser SSH avec HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="80e05-151">For more information, see the [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

<span data-ttu-id="80e05-152">À partir de votre client, utilisez SSH pour la connexion au cluster :</span><span class="sxs-lookup"><span data-stu-id="80e05-152">From your client, use SSH to connect to the cluster:</span></span>

```ssh SSHUSER@CLUSTERNAME-ssh.azurehdinsight.net```

<span data-ttu-id="80e05-153">Remplacez **SSHUSER** par le nom d’utilisateur SSH que vous avez fourni lors de la création du cluster.</span><span class="sxs-lookup"><span data-stu-id="80e05-153">Replace **SSHUSER** with the SSH username you provided during cluster creation.</span></span> <span data-ttu-id="80e05-154">Remplacez **CLUSTERNAME** par le nom de votre cluster.</span><span class="sxs-lookup"><span data-stu-id="80e05-154">Replace **CLUSTERNAME** with the name of the cluster.</span></span>

<span data-ttu-id="80e05-155">Lorsque vous y êtes invité, entrez le mot de passe utilisé pour le compte SSH.</span><span class="sxs-lookup"><span data-stu-id="80e05-155">When prompted, enter the password you used for the SSH account.</span></span>

<span data-ttu-id="80e05-156">Pour en savoir plus, voir [Utilisation de SSH avec HDInsight (Hadoop) depuis Bash (l’interpréteur de commande) sur Windows 10, Linux, Unix ou OS X](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="80e05-156">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <span data-ttu-id="80e05-157"><a id="getkafkainfo"></a>Obtention des informations sur Zookeeper et l’hôte du répartiteur</span><span class="sxs-lookup"><span data-stu-id="80e05-157"><a id="getkafkainfo"></a>Get the Zookeeper and Broker host information</span></span>

<span data-ttu-id="80e05-158">Lorsque vous travaillez avec Kafka, vous devez connaître deux valeurs d’hôte : les hôtes *Zookeeper* et de *répartiteur*.</span><span class="sxs-lookup"><span data-stu-id="80e05-158">When working with Kafka, you must know two host values; the *Zookeeper* hosts and the *Broker* hosts.</span></span> <span data-ttu-id="80e05-159">Ces hôtes sont utilisés avec l’API Kafka et la plupart des utilitaires fournis avec Kafka.</span><span class="sxs-lookup"><span data-stu-id="80e05-159">These hosts are used with the Kafka API and many of the utilities that ship with Kafka.</span></span>

<span data-ttu-id="80e05-160">Utilisez les étapes suivantes pour créer des variables d’environnement contenant des informations sur l’hôte.</span><span class="sxs-lookup"><span data-stu-id="80e05-160">Use the following steps to create environment variables that contain the host information.</span></span> <span data-ttu-id="80e05-161">Ces variables d’environnement sont utilisées dans les étapes de ce document.</span><span class="sxs-lookup"><span data-stu-id="80e05-161">These environment variables are used in the steps in this document.</span></span>

1. <span data-ttu-id="80e05-162">À partir d’une connexion SSH avec le cluster, utilisez la commande suivante pour installer l’utilitaire `jq`.</span><span class="sxs-lookup"><span data-stu-id="80e05-162">From an SSH connection to the cluster, use the following command to install the `jq` utility.</span></span> <span data-ttu-id="80e05-163">Cet utilitaire est utilisé pour analyser des documents JSON et est utile lors de la récupération des informations sur l’hôte du répartiteur :</span><span class="sxs-lookup"><span data-stu-id="80e05-163">This utility is used to parse JSON documents, and is useful in retrieving the broker host information:</span></span>
   
    ```bash
    sudo apt -y install jq
    ```

2. <span data-ttu-id="80e05-164">Pour définir les variables d’environnement avec les informations récupérées à partir d’Ambari, utilisez les commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="80e05-164">To set the environment variables with information retrieved from Ambari, use the following commands:</span></span>

    ```bash
    CLUSTERNAME='your cluster name'
    PASSWORD='your cluster password'
    export KAFKAZKHOSTS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/ZOOKEEPER/components/ZOOKEEPER_SERVER | jq -r '["\(.host_components[].HostRoles.host_name):2181"] | join(",")' | cut -d',' -f1,2`

    export KAFKABROKERS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/KAFKA/components/KAFKA_BROKER | jq -r '["\(.host_components[].HostRoles.host_name):9092"] | join(",")' | cut -d',' -f1,2`

    echo '$KAFKAZKHOSTS='$KAFKAZKHOSTS
    echo '$KAFKABROKERS='$KAFKABROKERS
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="80e05-165">Définissez `CLUSTERNAME=` sur le nom du cluster Kafka.</span><span class="sxs-lookup"><span data-stu-id="80e05-165">Set `CLUSTERNAME=` to the name of the Kafka cluster.</span></span> <span data-ttu-id="80e05-166">Définissez `PASSWORD=` sur le mot de passe de connexion (admin) que vous avez utilisé lors de la création du cluster.</span><span class="sxs-lookup"><span data-stu-id="80e05-166">Set `PASSWORD=` to the login (admin) password you used when creating the cluster.</span></span>

    <span data-ttu-id="80e05-167">Le texte suivant constitue un exemple du contenu de `$KAFKAZKHOSTS` :</span><span class="sxs-lookup"><span data-stu-id="80e05-167">The following text is an example of the contents of `$KAFKAZKHOSTS`:</span></span>
   
    `zk0-kafka.eahjefxxp1netdbyklgqj5y1ud.ex.internal.cloudapp.net:2181,zk2-kafka.eahjefxxp1netdbyklgqj5y1ud.ex.internal.cloudapp.net:2181`
   
    <span data-ttu-id="80e05-168">Le texte suivant constitue un exemple du contenu de `$KAFKABROKERS` :</span><span class="sxs-lookup"><span data-stu-id="80e05-168">The following text is an example of the contents of `$KAFKABROKERS`:</span></span>
   
    `wn1-kafka.eahjefxxp1netdbyklgqj5y1ud.cx.internal.cloudapp.net:9092,wn0-kafka.eahjefxxp1netdbyklgqj5y1ud.cx.internal.cloudapp.net:9092`

    > [!NOTE]
    > <span data-ttu-id="80e05-169">La commande `cut` sert à couper la liste des ordinateurs hôtes en deux entrées d’hôte.</span><span class="sxs-lookup"><span data-stu-id="80e05-169">The `cut` command is used to trim the list of hosts to two host entries.</span></span> <span data-ttu-id="80e05-170">Vous n’avez pas besoin de fournir la liste complète des hôtes lors de la création d’un consommateur ou d’un producteur Kafka.</span><span class="sxs-lookup"><span data-stu-id="80e05-170">You do not need to provide the full list of hosts when creating a Kafka consumer or producer.</span></span>
   
    > [!WARNING]
    > <span data-ttu-id="80e05-171">Les informations renvoyées par cette session ne sont pas toujours précises.</span><span class="sxs-lookup"><span data-stu-id="80e05-171">Do not rely on the information returned from this session to always be accurate.</span></span> <span data-ttu-id="80e05-172">Si vous redimensionnez le cluster, de nouveaux répartiteurs sont ajoutés ou supprimés.</span><span class="sxs-lookup"><span data-stu-id="80e05-172">If you scale the cluster, new brokers are added or removed.</span></span> <span data-ttu-id="80e05-173">Si une défaillance se produit et si un nœud est remplacé, le nom d’hôte du nœud peut changer.</span><span class="sxs-lookup"><span data-stu-id="80e05-173">If a failure occurs and a node is replaced, the host name for the node may change.</span></span>
    >
    > <span data-ttu-id="80e05-174">Vous devez récupérer les informations des hôtes Zookeeper et du répartiteur peu de temps avant de les utiliser pour vous assurer de leur validité.</span><span class="sxs-lookup"><span data-stu-id="80e05-174">You should retrieve the Zookeeper and broker hosts information shortly before you use it to ensure you have valid information.</span></span>

## <a name="create-a-topic"></a><span data-ttu-id="80e05-175">Création d'une rubrique</span><span class="sxs-lookup"><span data-stu-id="80e05-175">Create a topic</span></span>

<span data-ttu-id="80e05-176">Kafka stocke les flux de données dans des catégories appelées *rubriques*.</span><span class="sxs-lookup"><span data-stu-id="80e05-176">Kafka stores streams of data in categories called *topics*.</span></span> <span data-ttu-id="80e05-177">À partir d’une connexion SSH à un nœud principal de cluster, utilisez un script fourni avec Kafka pour créer une rubrique :</span><span class="sxs-lookup"><span data-stu-id="80e05-177">From An SSH connection to a cluster headnode, use a script provided with Kafka to create a topic:</span></span>

```bash
/usr/hdp/current/kafka-broker/bin/kafka-topics.sh --create --replication-factor 3 --partitions 8 --topic test --zookeeper $KAFKAZKHOSTS
```

<span data-ttu-id="80e05-178">Cette commande se connecte à Zookeeper en utilisant les informations d’hôte stockées dans `$KAFKAZKHOSTS`, puis crée une rubrique Kafka nommée **test**.</span><span class="sxs-lookup"><span data-stu-id="80e05-178">This command connects to Zookeeper using the host information stored in `$KAFKAZKHOSTS`, and then create Kafka topic named **test**.</span></span> <span data-ttu-id="80e05-179">Vous pouvez vérifier que la rubrique a été créée à l’aide du script suivant pour répertorier les rubriques :</span><span class="sxs-lookup"><span data-stu-id="80e05-179">You can verify that the topic was created by using the following script to list topics:</span></span>

```bash
/usr/hdp/current/kafka-broker/bin/kafka-topics.sh --list --zookeeper $KAFKAZKHOSTS
```

<span data-ttu-id="80e05-180">La sortie de cette commande répertorie les rubriques Kafka, contenant la rubrique **test**.</span><span class="sxs-lookup"><span data-stu-id="80e05-180">The output of this command lists Kafka topics, which contains the **test** topic.</span></span>

## <a name="produce-and-consume-records"></a><span data-ttu-id="80e05-181">Produire et consommer des enregistrements</span><span class="sxs-lookup"><span data-stu-id="80e05-181">Produce and consume records</span></span>

<span data-ttu-id="80e05-182">Kafka stocke les *enregistrements* dans des rubriques.</span><span class="sxs-lookup"><span data-stu-id="80e05-182">Kafka stores *records* in topics.</span></span> <span data-ttu-id="80e05-183">Les enregistrements sont produits par des *producteurs*, et utilisés par des *consommateurs*.</span><span class="sxs-lookup"><span data-stu-id="80e05-183">Records are produced by *producers*, and consumed by *consumers*.</span></span> <span data-ttu-id="80e05-184">Les producteurs récupèrent des enregistrements à partir des *répartiteurs* Kafka.</span><span class="sxs-lookup"><span data-stu-id="80e05-184">Producers retrieve records from Kafka *brokers*.</span></span> <span data-ttu-id="80e05-185">Chaque nœud Worker dans votre cluster HDInsight est un répartiteur Kafka.</span><span class="sxs-lookup"><span data-stu-id="80e05-185">Each worker node in your HDInsight cluster is a Kafka broker.</span></span>

<span data-ttu-id="80e05-186">Pour stocker les enregistrements dans la rubrique test créée précédemment, puis les lire à l’aide d’un consommateur, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="80e05-186">Use the following steps to store records into the test topic you created earlier, and then read them using a consumer:</span></span>

1. <span data-ttu-id="80e05-187">À partir de la session SSH, utilisez un script fourni avec Kafka pour écrire des enregistrements dans la rubrique :</span><span class="sxs-lookup"><span data-stu-id="80e05-187">From the SSH session, use a script provided with Kafka to write records to the topic:</span></span>
   
    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-console-producer.sh --broker-list $KAFKABROKERS --topic test
    ```
   
    <span data-ttu-id="80e05-188">L’invite ne s’affichera plus après cette commande.</span><span class="sxs-lookup"><span data-stu-id="80e05-188">You are not returned to the prompt after this command.</span></span> <span data-ttu-id="80e05-189">À la place, tapez quelques messages de texte, puis utilisez la combinaison **Ctrl + C** pour arrêter l’envoi à la rubrique.</span><span class="sxs-lookup"><span data-stu-id="80e05-189">Instead, type a few text messages and then use **Ctrl + C** to stop sending to the topic.</span></span> <span data-ttu-id="80e05-190">Chaque ligne est envoyée en tant qu’enregistrement distinct.</span><span class="sxs-lookup"><span data-stu-id="80e05-190">Each line is sent as a separate record.</span></span>

2. <span data-ttu-id="80e05-191">Utilisez un script fourni avec Kafka pour lire les enregistrements à partir de la rubrique :</span><span class="sxs-lookup"><span data-stu-id="80e05-191">Use a script provided with Kafka to read records from the topic:</span></span>
   
    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-console-consumer.sh --bootstrap-server $KAFKABROKERS --topic test --from-beginning
    ```
   
    <span data-ttu-id="80e05-192">Cette commande permet de récupérer les enregistrements à partir de la rubrique et de les afficher.</span><span class="sxs-lookup"><span data-stu-id="80e05-192">This command retrieves the records from the topic and displays them.</span></span> <span data-ttu-id="80e05-193">L’utilisation de `--from-beginning` indique au consommateur de démarrer à partir du début du flux, de manière à récupérer tous les enregistrements.</span><span class="sxs-lookup"><span data-stu-id="80e05-193">Using `--from-beginning` tells the consumer to start from the beginning of the stream, so all records are retrieved.</span></span>

3. <span data-ttu-id="80e05-194">Utilisez la combinaison __Ctrl + C__ pour arrêter le consommateur.</span><span class="sxs-lookup"><span data-stu-id="80e05-194">Use __Ctrl + C__ to stop the consumer.</span></span>

## <a name="producer-and-consumer-api"></a><span data-ttu-id="80e05-195">API de producteur et de consommateur</span><span class="sxs-lookup"><span data-stu-id="80e05-195">Producer and consumer API</span></span>

<span data-ttu-id="80e05-196">Vous pouvez également produire et consommer des enregistrements par programme à l’aide des [API Kafka](http://kafka.apache.org/documentation#api).</span><span class="sxs-lookup"><span data-stu-id="80e05-196">You can also programmatically produce and consume records using the [Kafka APIs](http://kafka.apache.org/documentation#api).</span></span> <span data-ttu-id="80e05-197">Pour générer un producteur et un consommateur Java, suivez les étapes suivantes à partir de votre environnement de développement.</span><span class="sxs-lookup"><span data-stu-id="80e05-197">To build a Java producer and consumer, use the following steps from your development environment.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="80e05-198">Les composants suivants doivent être installés dans votre environnement de développement :</span><span class="sxs-lookup"><span data-stu-id="80e05-198">You must have the following components installed in your development environment:</span></span>
>
> * <span data-ttu-id="80e05-199">[Java JDK 8](http://www.oracle.com/technetwork/java/javase/downloads/index.html), ou un équivalent, par exemple, OpenJDK.</span><span class="sxs-lookup"><span data-stu-id="80e05-199">[Java JDK 8](http://www.oracle.com/technetwork/java/javase/downloads/index.html) or an equivalent, such as OpenJDK.</span></span>
>
> * [<span data-ttu-id="80e05-200">Apache Maven</span><span class="sxs-lookup"><span data-stu-id="80e05-200">Apache Maven</span></span>](http://maven.apache.org/)
>
> * <span data-ttu-id="80e05-201">Un client SSH et la commande `scp`.</span><span class="sxs-lookup"><span data-stu-id="80e05-201">An SSH client and the `scp` command.</span></span> <span data-ttu-id="80e05-202">Pour plus d’informations, consultez le document [Utiliser SSH avec HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="80e05-202">For more information, see the [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

1. <span data-ttu-id="80e05-203">Téléchargez les exemples à partir de [https://github.com/Azure-Samples/hdinsight-kafka-java-get-started](https://github.com/Azure-Samples/hdinsight-kafka-java-get-started).</span><span class="sxs-lookup"><span data-stu-id="80e05-203">Download the examples from [https://github.com/Azure-Samples/hdinsight-kafka-java-get-started](https://github.com/Azure-Samples/hdinsight-kafka-java-get-started).</span></span> <span data-ttu-id="80e05-204">Pour l’exemple de producteur/consommateur, utilisez le projet dans le répertoire `Producer-Consumer`.</span><span class="sxs-lookup"><span data-stu-id="80e05-204">For the producer/consumer example, use the project in the `Producer-Consumer` directory.</span></span> <span data-ttu-id="80e05-205">Il contient les classes suivantes :</span><span class="sxs-lookup"><span data-stu-id="80e05-205">This example contains the following classes:</span></span>
   
    * <span data-ttu-id="80e05-206">**Exécuter** : démarre le consommateur ou le producteur.</span><span class="sxs-lookup"><span data-stu-id="80e05-206">**Run** - starts either the consumer or producer.</span></span>

    * <span data-ttu-id="80e05-207">**Producer** : stocke 1 000 000 d’enregistrements dans la rubrique.</span><span class="sxs-lookup"><span data-stu-id="80e05-207">**Producer** - stores 1,000,000 records to the topic.</span></span>

    * <span data-ttu-id="80e05-208">**Consumer** : lit les enregistrements à partir de la rubrique.</span><span class="sxs-lookup"><span data-stu-id="80e05-208">**Consumer** - reads records from the topic.</span></span>

2. <span data-ttu-id="80e05-209">Pour créer un package jar, modifiez les répertoires d’accès à l’emplacement du répertoire `Producer-Consumer` de l’exemple, puis utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="80e05-209">To create a jar package, change directories to the location of the `Producer-Consumer` directory and use the following command:</span></span>

    ```
    mvn clean package
    ```

    <span data-ttu-id="80e05-210">Cette commande crée un répertoire nommé `target`, qui contient un fichier nommé `kafka-producer-consumer-1.0-SNAPSHOT.jar`.</span><span class="sxs-lookup"><span data-stu-id="80e05-210">This command creates a directory named `target`, that contains a file named `kafka-producer-consumer-1.0-SNAPSHOT.jar`.</span></span>

3. <span data-ttu-id="80e05-211">Utilisez les commandes suivantes pour copier le fichier `kafka-producer-consumer-1.0-SNAPSHOT.jar` dans votre cluster HDInsight :</span><span class="sxs-lookup"><span data-stu-id="80e05-211">Use the following commands to copy the `kafka-producer-consumer-1.0-SNAPSHOT.jar` file to your HDInsight cluster:</span></span>
   
    ```bash
    scp ./target/kafka-producer-consumer-1.0-SNAPSHOT.jar SSHUSER@CLUSTERNAME-ssh.azurehdinsight.net:kafka-producer-consumer.jar
    ```
   
    <span data-ttu-id="80e05-212">Remplacez **SSHUSER** par l’utilisateur SSH pour votre cluster, et remplacez **CLUSTERNAME** par le nom de votre cluster.</span><span class="sxs-lookup"><span data-stu-id="80e05-212">Replace **SSHUSER** with the SSH user for your cluster, and replace **CLUSTERNAME** with the name of your cluster.</span></span> <span data-ttu-id="80e05-213">Lorsque vous y êtes invité, entrez le mot de passe de l’utilisateur SSH.</span><span class="sxs-lookup"><span data-stu-id="80e05-213">When prompted enter the password for the SSH user.</span></span>

4. <span data-ttu-id="80e05-214">Une fois que la commande `scp` a fini de copier le fichier, connectez-vous au cluster à l’aide de SSH.</span><span class="sxs-lookup"><span data-stu-id="80e05-214">Once the `scp` command finishes copying the file, connect to the cluster using SSH.</span></span> <span data-ttu-id="80e05-215">Utilisez la commande suivante pour écrire des enregistrements dans la rubrique de test :</span><span class="sxs-lookup"><span data-stu-id="80e05-215">Use the following command to write records to the test topic:</span></span>

    ```bash
    java -jar kafka-producer-consumer.jar producer $KAFKABROKERS
    ```

5. <span data-ttu-id="80e05-216">Une fois le processus terminé, utilisez la commande suivante pour lire à partir de la rubrique :</span><span class="sxs-lookup"><span data-stu-id="80e05-216">Once the process has finished, use the following command to read from the topic:</span></span>
   
    ```bash
    java -jar kafka-producer-consumer.jar consumer $KAFKABROKERS
    ```
   
    <span data-ttu-id="80e05-217">Les enregistrements lus et le nombre d’enregistrements s’affichent.</span><span class="sxs-lookup"><span data-stu-id="80e05-217">The records read, along with a count of records, is displayed.</span></span> <span data-ttu-id="80e05-218">Il est possible qu’un peu plus de 1 000 000 d’enregistrements soient consignés, car vous avez envoyé plusieurs enregistrements à la rubrique à l’aide d’un script dans une étape précédente.</span><span class="sxs-lookup"><span data-stu-id="80e05-218">You may see a few more than 1,000,000 logged as you sent several records to the topic using a script in an earlier step.</span></span>

6. <span data-ttu-id="80e05-219">Utilisez __Ctrl + C__ pour quitter le consommateur.</span><span class="sxs-lookup"><span data-stu-id="80e05-219">Use __Ctrl + C__ to exit the consumer.</span></span>

### <a name="multiple-consumers"></a><span data-ttu-id="80e05-220">Consommateurs multiples</span><span class="sxs-lookup"><span data-stu-id="80e05-220">Multiple consumers</span></span>

<span data-ttu-id="80e05-221">Les consommateurs Kafka utilisent un groupe de consommateurs lors de la lecture des enregistrements.</span><span class="sxs-lookup"><span data-stu-id="80e05-221">Kafka consumers use a consumer group when reading records.</span></span> <span data-ttu-id="80e05-222">L’utilisation du même groupe avec plusieurs consommateurs permet des lectures à charge équilibrée à partir d’une rubrique.</span><span class="sxs-lookup"><span data-stu-id="80e05-222">Using the same group with multiple consumers results in load balanced reads from a topic.</span></span> <span data-ttu-id="80e05-223">Chaque consommateur dans le groupe reçoit une partie des enregistrements.</span><span class="sxs-lookup"><span data-stu-id="80e05-223">Each consumer in the group receives a portion of the records.</span></span> <span data-ttu-id="80e05-224">Pour voir ce processus en action, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="80e05-224">To see this process in action, use the following steps:</span></span>

1. <span data-ttu-id="80e05-225">Ouvrez une nouvelle session SSH vers le cluster, afin de disposer de deux sessions.</span><span class="sxs-lookup"><span data-stu-id="80e05-225">Open a new SSH session to the cluster, so that you have two of them.</span></span> <span data-ttu-id="80e05-226">Dans chaque session, utilisez les éléments suivants pour démarrer un consommateur avec le même ID de groupe de consommateurs :</span><span class="sxs-lookup"><span data-stu-id="80e05-226">In each session, use the following to start a consumer with the same consumer group ID:</span></span>
   
    ```bash
    java -jar kafka-producer-consumer.jar consumer $KAFKABROKERS mygroup
    ```

    <span data-ttu-id="80e05-227">Cette commande démarre un consommateur à l’aide de l’ID de groupe `mygroup`.</span><span class="sxs-lookup"><span data-stu-id="80e05-227">This command starts a consumer using the group ID `mygroup`.</span></span>

    > [!NOTE]
    > <span data-ttu-id="80e05-228">Utilisez les commandes dans la section [Obtention des informations sur Zookeeper et l’hôte du répartiteur](#getkafkainfo) pour définir `$KAFKABROKERS` pour cette session SSH.</span><span class="sxs-lookup"><span data-stu-id="80e05-228">Use the commands in the [Get the Zookeeper and Broker host information](#getkafkainfo) section to set `$KAFKABROKERS` for this SSH session.</span></span>

2. <span data-ttu-id="80e05-229">Observez chaque session compter les enregistrements reçus de la rubrique.</span><span class="sxs-lookup"><span data-stu-id="80e05-229">Watch as each session counts the records it receives from the topic.</span></span> <span data-ttu-id="80e05-230">Le total des deux sessions doit être identique à celui reçu précédemment à partir d’un seul consommateur.</span><span class="sxs-lookup"><span data-stu-id="80e05-230">The total of both sessions should be the same as you received previously from one consumer.</span></span>

<span data-ttu-id="80e05-231">La consommation par les clients au sein du même groupe est gérée par le biais des partitions de la rubrique.</span><span class="sxs-lookup"><span data-stu-id="80e05-231">Consumption by clients within the same group is handled through the partitions for the topic.</span></span> <span data-ttu-id="80e05-232">Pour la rubrique `test` créée précédemment, il y a huit partitions.</span><span class="sxs-lookup"><span data-stu-id="80e05-232">For the `test` topic created earlier, it has eight partitions.</span></span> <span data-ttu-id="80e05-233">Si vous ouvrez huit sessions SSH et lancez un consommateur dans toutes les sessions, chaque consommateur lit les enregistrements à partir d’une seule partition de la rubrique.</span><span class="sxs-lookup"><span data-stu-id="80e05-233">If you open eight SSH sessions and launch a consumer in all sessions, each consumer reads records from a single partition for the topic.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="80e05-234">Il ne peut pas y avoir plus d’instances de consommateurs dans un groupe de consommateurs que de partitions.</span><span class="sxs-lookup"><span data-stu-id="80e05-234">There cannot be more consumer instances in a consumer group than partitions.</span></span> <span data-ttu-id="80e05-235">Dans cet exemple, un groupe de consommateurs peut contenir jusqu’à huit consommateurs puisque c’est le nombre de partitions de la rubrique.</span><span class="sxs-lookup"><span data-stu-id="80e05-235">In this example, one consumer group can contain up to eight consumers since that is the number of partitions in the topic.</span></span> <span data-ttu-id="80e05-236">Vous pouvez également disposer de plusieurs groupes de consommateurs, chacun ne dépassant pas huit consommateurs.</span><span class="sxs-lookup"><span data-stu-id="80e05-236">Or you can have multiple consumer groups, each with no more than eight consumers.</span></span>

<span data-ttu-id="80e05-237">Les enregistrements stockés dans Kafka sont stockés dans l’ordre de réception dans une partition.</span><span class="sxs-lookup"><span data-stu-id="80e05-237">Records stored in Kafka are stored in the order they are received within a partition.</span></span> <span data-ttu-id="80e05-238">Pour obtenir la livraison chronologique des enregistrements *dans une partition*, créez un groupe de consommateurs où le nombre d’instances de consommateurs correspond au nombre de partitions.</span><span class="sxs-lookup"><span data-stu-id="80e05-238">To achieve in-ordered delivery for records *within a partition*, create a consumer group where the number of consumer instances matches the number of partitions.</span></span> <span data-ttu-id="80e05-239">Pour obtenir la livraison chronologique des enregistrements *dans la rubrique*, créez un groupe de consommateurs avec une seule instance de consommateur.</span><span class="sxs-lookup"><span data-stu-id="80e05-239">To achieve in-ordered delivery for records *within the topic*, create a consumer group with only one consumer instance.</span></span>

## <a name="streaming-api"></a><span data-ttu-id="80e05-240">API de diffusion en continu</span><span class="sxs-lookup"><span data-stu-id="80e05-240">Streaming API</span></span>

<span data-ttu-id="80e05-241">L’API de diffusion en continu a été ajoutée à Kafka dans la version 0.10.0 ; les versions antérieures s’appuient sur Apache Spark ou Storm pour le traitement des flux de données.</span><span class="sxs-lookup"><span data-stu-id="80e05-241">The streaming API was added to Kafka in version 0.10.0; earlier versions rely on Apache Spark or Storm for stream processing.</span></span>

1. <span data-ttu-id="80e05-242">Si ce n’est pas déjà fait, téléchargez les exemples de [https://github.com/Azure-Samples/hdinsight-kafka-java-get-started](https://github.com/Azure-Samples/hdinsight-kafka-java-get-started) dans votre environnement de développement.</span><span class="sxs-lookup"><span data-stu-id="80e05-242">If you haven't already done so, download the examples from [https://github.com/Azure-Samples/hdinsight-kafka-java-get-started](https://github.com/Azure-Samples/hdinsight-kafka-java-get-started) to your development environment.</span></span> <span data-ttu-id="80e05-243">Pour l’exemple de diffusion en continu, utilisez le projet dans le répertoire `streaming`.</span><span class="sxs-lookup"><span data-stu-id="80e05-243">For the streaming example, use the project in the `streaming` directory.</span></span>
   
    <span data-ttu-id="80e05-244">Ce projet contient uniquement une classe, `Stream`, qui lit les enregistrements à partir de la rubrique `test` créée précédemment.</span><span class="sxs-lookup"><span data-stu-id="80e05-244">This project contains only one class, `Stream`, which reads records from the `test` topic created previously.</span></span> <span data-ttu-id="80e05-245">Il compte les mots lus et émet chaque mot et quantité dans une rubrique nommée `wordcounts`.</span><span class="sxs-lookup"><span data-stu-id="80e05-245">It counts the words read, and emits each word and count to a topic named `wordcounts`.</span></span> <span data-ttu-id="80e05-246">La rubrique `wordcounts` est créée dans une étape ultérieure de cette section.</span><span class="sxs-lookup"><span data-stu-id="80e05-246">The `wordcounts` topic is created in a later step in this section.</span></span>

2. <span data-ttu-id="80e05-247">À partir de la ligne de commande dans votre environnement de développement, modifiez les répertoires d’accès à l’emplacement du répertoire `Streaming`, puis utilisez la commande suivante pour créer un package jar :</span><span class="sxs-lookup"><span data-stu-id="80e05-247">From the command line in your development environment, change directories to the location of the `Streaming` directory, and then use the following command to create a jar package:</span></span>

    ```bash
    mvn clean package
    ```

    <span data-ttu-id="80e05-248">Cette commande crée un répertoire nommé `target`, qui contient un fichier nommé `kafka-streaming-1.0-SNAPSHOT.jar`.</span><span class="sxs-lookup"><span data-stu-id="80e05-248">This command creates a directory named `target`, which contains a file named `kafka-streaming-1.0-SNAPSHOT.jar`.</span></span>

3. <span data-ttu-id="80e05-249">Utilisez les commandes suivantes pour copier le fichier `kafka-streaming-1.0-SNAPSHOT.jar` dans votre cluster HDInsight :</span><span class="sxs-lookup"><span data-stu-id="80e05-249">Use the following commands to copy the `kafka-streaming-1.0-SNAPSHOT.jar` file to your HDInsight cluster:</span></span>
   
    ```bash
    scp ./target/kafka-streaming-1.0-SNAPSHOT.jar SSHUSER@CLUSTERNAME-ssh.azurehdinsight.net:kafka-streaming.jar
    ```
   
    <span data-ttu-id="80e05-250">Remplacez **SSHUSER** par l’utilisateur SSH pour votre cluster, et remplacez **CLUSTERNAME** par le nom de votre cluster.</span><span class="sxs-lookup"><span data-stu-id="80e05-250">Replace **SSHUSER** with the SSH user for your cluster, and replace **CLUSTERNAME** with the name of your cluster.</span></span> <span data-ttu-id="80e05-251">Lorsque vous y êtes invité, entrez le mot de passe de l’utilisateur SSH.</span><span class="sxs-lookup"><span data-stu-id="80e05-251">When prompted enter the password for the SSH user.</span></span>

4. <span data-ttu-id="80e05-252">Une fois que la commande `scp` a fini de copier le fichier, connectez-vous au cluster à l’aide de SSH, puis utilisez la commande suivante pour créer la rubrique `wordcounts` :</span><span class="sxs-lookup"><span data-stu-id="80e05-252">Once the `scp` command finishes copying the file, connect to the cluster using SSH, and then use the following command to create the `wordcounts` topic:</span></span>

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --create --replication-factor 3 --partitions 8 --topic wordcounts --zookeeper $KAFKAZKHOSTS
    ```

5. <span data-ttu-id="80e05-253">Ensuite, démarrez le processus de diffusion en continu à l’aide de la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="80e05-253">Next, start the streaming process by using the following command:</span></span>
   
    ```bash
    java -jar kafka-streaming.jar $KAFKABROKERS $KAFKAZKHOSTS 2>/dev/null &
    ```
   
    <span data-ttu-id="80e05-254">Cette commande démarre le processus de diffusion en continu en arrière-plan.</span><span class="sxs-lookup"><span data-stu-id="80e05-254">This command starts the streaming process in the background.</span></span>

6. <span data-ttu-id="80e05-255">Utilisez la commande suivante pour envoyer des messages à la rubrique `test`.</span><span class="sxs-lookup"><span data-stu-id="80e05-255">Use the following command to send messages to the `test` topic.</span></span> <span data-ttu-id="80e05-256">Ces messages sont traités par l’exemple de diffusion en continu :</span><span class="sxs-lookup"><span data-stu-id="80e05-256">These messages are processed by the streaming example:</span></span>
   
    ```bash
    java -jar kafka-producer-consumer.jar producer $KAFKABROKERS &>/dev/null &
    ```

7. <span data-ttu-id="80e05-257">Utilisez la commande suivante pour afficher la sortie écrite dans la rubrique `wordcounts` par le processus de diffusion en continu :</span><span class="sxs-lookup"><span data-stu-id="80e05-257">Use the following command to view the output that is written to the `wordcounts` topic by the streaming process:</span></span>
   
    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-console-consumer.sh --bootstrap-server $KAFKABROKERS --topic wordcounts --from-beginning --formatter kafka.tools.DefaultMessageFormatter --property print.key=true --property key.deserializer=org.apache.kafka.common.serialization.StringDeserializer --property value.deserializer=org.apache.kafka.common.serialization.LongDeserializer
    ```
   
    > [!NOTE]
    > <span data-ttu-id="80e05-258">Pour afficher les données, vous devez indiquer au consommateur d’imprimer la clé et le désérialiseur à utiliser pour la clé et la valeur.</span><span class="sxs-lookup"><span data-stu-id="80e05-258">To view the data, you must tell the consumer to print the key and the deserializer to use for the key and value.</span></span> <span data-ttu-id="80e05-259">Le nom de la clé est le mot, et la valeur de clé contient le nombre.</span><span class="sxs-lookup"><span data-stu-id="80e05-259">The key name is the word, and the key value contains the count.</span></span>
   
    <span data-ttu-id="80e05-260">Le résultat ressemble au texte suivant :</span><span class="sxs-lookup"><span data-stu-id="80e05-260">The output is similar to the following text:</span></span>
   
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
    > <span data-ttu-id="80e05-261">Le nombre augmente à chaque fois qu’un mot est rencontré.</span><span class="sxs-lookup"><span data-stu-id="80e05-261">The count increments each time a word is encountered.</span></span>

7. <span data-ttu-id="80e05-262">Utilisez la combinaison __Ctrl + C__ pour quitter le client, puis utilisez la commande `fg` pour passer la tâche de diffusion en continu de l’arrière-plan au premier plan.</span><span class="sxs-lookup"><span data-stu-id="80e05-262">Use the __Ctrl + C__ to exit the consumer, then use the `fg` command to bring the streaming background task back to the foreground.</span></span> <span data-ttu-id="80e05-263">Utilisez la combinaison __Ctrl + C__ pour le quitter également.</span><span class="sxs-lookup"><span data-stu-id="80e05-263">Use __Ctrl + C__ to exit it also.</span></span>

## <a name="delete-the-cluster"></a><span data-ttu-id="80e05-264">Suppression du cluster</span><span class="sxs-lookup"><span data-stu-id="80e05-264">Delete the cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="troubleshoot"></a><span data-ttu-id="80e05-265">Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="80e05-265">Troubleshoot</span></span>

<span data-ttu-id="80e05-266">Si vous rencontrez des problèmes lors de la création de clusters HDInsight, reportez-vous aux [exigences de contrôle d’accès](hdinsight-administer-use-portal-linux.md#create-clusters).</span><span class="sxs-lookup"><span data-stu-id="80e05-266">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="80e05-267">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="80e05-267">Next steps</span></span>

<span data-ttu-id="80e05-268">Dans ce document, vous avez appris les bases de l’utilisation d’Apache Kafka sur HDInsight.</span><span class="sxs-lookup"><span data-stu-id="80e05-268">In this document, you have learned the basics of working with Apache Kafka on HDInsight.</span></span> <span data-ttu-id="80e05-269">Consultez les articles suivants pour en savoir plus sur l’utilisation de Kafka :</span><span class="sxs-lookup"><span data-stu-id="80e05-269">Use the following to learn more about working with Kafka:</span></span>

* [<span data-ttu-id="80e05-270">Garantir une haute disponibilité de vos données avec Apache Kafka sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="80e05-270">Ensure high availability of your data with Kafka on HDInsight</span></span>](hdinsight-apache-kafka-high-availability.md)
* [<span data-ttu-id="80e05-271">Configurer le stockage et l’extensibilité pour Apache Kafka sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="80e05-271">Increase scalability by configuring managed disks with Kafka on HDInsight</span></span>](hdinsight-apache-kafka-scalability.md)
* <span data-ttu-id="80e05-272">[Documentation Apache Kafka](http://kafka.apache.org/documentation.html) à l’adresse kafka.apache.org.</span><span class="sxs-lookup"><span data-stu-id="80e05-272">[Apache Kafka documentation](http://kafka.apache.org/documentation.html) at kafka.apache.org.</span></span>
* [<span data-ttu-id="80e05-273">Utilisation de MirrorMaker pour créer un réplica de Kafka sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="80e05-273">Use MirrorMaker to create a replica of Kafka on HDInsight</span></span>](hdinsight-apache-kafka-mirroring.md)
* <span data-ttu-id="80e05-274">[Use Apache Storm with Kafka on HDInsight](hdinsight-apache-storm-with-kafka.md) (Utilisation d’Apache Storm avec Kafka sur HDInsight)</span><span class="sxs-lookup"><span data-stu-id="80e05-274">[Use Apache Storm with Kafka on HDInsight](hdinsight-apache-storm-with-kafka.md)</span></span>
* <span data-ttu-id="80e05-275">[Use Apache Spark with Kafka on HDInsight](hdinsight-apache-spark-with-kafka.md) (Utilisation d’Apache Spark avec Kafka sur HDInsight)</span><span class="sxs-lookup"><span data-stu-id="80e05-275">[Use Apache Spark with Kafka on HDInsight](hdinsight-apache-spark-with-kafka.md)</span></span>
* <span data-ttu-id="80e05-276">[Connect to Kafka through an Azure Virtual Network](hdinsight-apache-kafka-connect-vpn-gateway.md) (Se connecter à Kafka via un réseau virtuel Azure)</span><span class="sxs-lookup"><span data-stu-id="80e05-276">[Connect to Kafka through an Azure Virtual Network](hdinsight-apache-kafka-connect-vpn-gateway.md)</span></span>
