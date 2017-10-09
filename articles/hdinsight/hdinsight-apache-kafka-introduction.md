---
title: "Présentation d’aaaAn tooApache Kafka sur HDInsight - Azure | Documents Microsoft"
description: "En savoir plus sur Kafka Apache sur HDInsight : ce qu’il est, ce qu’il fait et où les exemples toofind et la prise en main des informations."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: f284b6e3-5f3b-4a50-b455-917e77588069
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/15/2017
ms.author: larryfr
ms.openlocfilehash: 1bc198d4cf93a4682030d4fa5f71030f49ad64be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="introducing-apache-kafka-on-hdinsight-preview"></a><span data-ttu-id="c7d03-103">Présentation d’Apache Kafka sur HDInsight (version préliminaire)</span><span class="sxs-lookup"><span data-stu-id="c7d03-103">Introducing Apache Kafka on HDInsight (preview)</span></span>

<span data-ttu-id="c7d03-104">[Apache Kafka](https://kafka.apache.org) est une plate-forme de diffusion en continu distribuée open source qui peut être utilisé toobuild en temps réel de diffusion en continu des pipelines de données et applications.</span><span class="sxs-lookup"><span data-stu-id="c7d03-104">[Apache Kafka](https://kafka.apache.org) is an open-source distributed streaming platform that can be used toobuild real-time streaming data pipelines and applications.</span></span> <span data-ttu-id="c7d03-105">Kafka fournit également des fonctionnalités similaires tooa file d’attente, où vous pouvez publier et s’abonner à des flux de données toonamed courtier de messages.</span><span class="sxs-lookup"><span data-stu-id="c7d03-105">Kafka also provides message broker functionality similar tooa message queue, where you can publish and subscribe toonamed data streams.</span></span> <span data-ttu-id="c7d03-106">Kafka sur HDInsight vous offre un service géré, évolutif et hautement disponible dans le cloud de Microsoft Azure hello.</span><span class="sxs-lookup"><span data-stu-id="c7d03-106">Kafka on HDInsight provides you with a managed, highly scalable, and highly available service in hello Microsoft Azure cloud.</span></span>

## <a name="why-use-kafka-on-hdinsight"></a><span data-ttu-id="c7d03-107">Pourquoi utiliser Kafka sur HDInsight ?</span><span class="sxs-lookup"><span data-stu-id="c7d03-107">Why use Kafka on HDInsight?</span></span>

<span data-ttu-id="c7d03-108">Kafka fournit hello suivant de fonctionnalités :</span><span class="sxs-lookup"><span data-stu-id="c7d03-108">Kafka provides hello following features:</span></span>

* <span data-ttu-id="c7d03-109">Modèle de messagerie de publication / abonnement : Kafka fournit une API de production pour la publication des enregistrements tooa rubrique de Kafka.</span><span class="sxs-lookup"><span data-stu-id="c7d03-109">Publish-subscribe messaging pattern: Kafka provides a Producer API for publishing records tooa Kafka topic.</span></span> <span data-ttu-id="c7d03-110">Hello consommateur API est utilisée lors de l’abonnement tooa rubrique.</span><span class="sxs-lookup"><span data-stu-id="c7d03-110">hello Consumer API is used when subscribing tooa topic.</span></span>

* <span data-ttu-id="c7d03-111">Traitement des flux : Kafka est souvent utilisé avec Apache Storm ou Spark pour le traitement des flux en temps réel.</span><span class="sxs-lookup"><span data-stu-id="c7d03-111">Stream processing: Kafka is often used with Apache Storm or Spark for real-time stream processing.</span></span> <span data-ttu-id="c7d03-112">Kafka 0.10.0.0 (HDInsight version 3.5) a introduit une API de diffusion en continu qui vous permet de toobuild solutions de diffusion en continu sans Storm ou Spark.</span><span class="sxs-lookup"><span data-stu-id="c7d03-112">Kafka 0.10.0.0 (HDInsight version 3.5) introduced a streaming API that allows you toobuild streaming solutions without requiring Storm or Spark.</span></span>

* <span data-ttu-id="c7d03-113">Échelle horizontale : Kafka partitionne les flux de données entre les nœuds de hello dans le cluster HDInsight de hello.</span><span class="sxs-lookup"><span data-stu-id="c7d03-113">Horizontal scale: Kafka partitions streams across hello nodes in hello HDInsight cluster.</span></span> <span data-ttu-id="c7d03-114">Processus de consommateur peuvent être associés à des partitions individuelles tooprovide l’équilibrage de charge lors de l’utilisation des enregistrements.</span><span class="sxs-lookup"><span data-stu-id="c7d03-114">Consumer processes can be associated with individual partitions tooprovide load balancing when consuming records.</span></span>

* <span data-ttu-id="c7d03-115">Commande livraison : au sein de chaque partition, les enregistrements sont stockés dans le flux hello dans l’ordre de hello qu’ils ont été reçus.</span><span class="sxs-lookup"><span data-stu-id="c7d03-115">In-order delivery: Within each partition, records are stored in hello stream in hello order that they were received.</span></span> <span data-ttu-id="c7d03-116">En associant un processus consommateur par partition, vous pouvez garantir que les enregistrements sont traités dans l’ordre.</span><span class="sxs-lookup"><span data-stu-id="c7d03-116">By associating one consumer process per partition, you can guarantee that records are processed in-order.</span></span>

* <span data-ttu-id="c7d03-117">À tolérance de pannes : Les Partitions peuvent être répliquées entre une tolérance de panne tooprovide nœuds.</span><span class="sxs-lookup"><span data-stu-id="c7d03-117">Fault-tolerant: Partitions can be replicated between nodes tooprovide fault tolerance.</span></span>

* <span data-ttu-id="c7d03-118">Intégration avec des disques gérés Azure : managé disques fournit plus élevé de débit et de mise à l’échelle pour les disques hello utilisés par les ordinateurs virtuels de hello dans le cluster HDInsight de hello.</span><span class="sxs-lookup"><span data-stu-id="c7d03-118">Integration with Azure Managed Disks: Managed disks provides higher scale and throughput for hello disks used by hello virtual machines in hello HDInsight cluster.</span></span>

    <span data-ttu-id="c7d03-119">Disques gérés sont activées par défaut pour Kafka sur HDInsight et nombre de hello de disques utilisés par le nœud peut être configuré lors de la création de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c7d03-119">Managed disks are enabled by default for Kafka on HDInsight, and hello number of disks used per node can be configured during HDInsight creation.</span></span> <span data-ttu-id="c7d03-120">Pour plus d’informations sur les disques gérés, consultez [Azure Managed Disks](../virtual-machines/windows/managed-disks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c7d03-120">For more information on managed disks, see [Azure Managed Disks](../virtual-machines/windows/managed-disks-overview.md).</span></span>

    <span data-ttu-id="c7d03-121">Pour plus d’informations sur la configuration des disques gérés avec Kafka sur HDInsight, consultez [Increase scalability of Kafka on HDInsight](hdinsight-apache-kafka-scalability.md) (Augmenter l’évolutivité de Kafka sur HDInsight).</span><span class="sxs-lookup"><span data-stu-id="c7d03-121">For information on configuring managed disks with Kafka on HDInsight, see [Increase scalability of Kafka on HDInsight](hdinsight-apache-kafka-scalability.md).</span></span>

## <a name="use-cases"></a><span data-ttu-id="c7d03-122">Cas d'utilisation</span><span class="sxs-lookup"><span data-stu-id="c7d03-122">Use cases</span></span>

* <span data-ttu-id="c7d03-123">**Messagerie**: car il prend en charge hello publication-abonnement de modèle de message, Kafka est souvent utilisé comme un courtier de messages.</span><span class="sxs-lookup"><span data-stu-id="c7d03-123">**Messaging**: Since it supports hello publish-subscribe message pattern, Kafka is often used as a message broker.</span></span>

* <span data-ttu-id="c7d03-124">**Suivi des activités**: étant donné que Kafka fournit la journalisation dans l’ordre des enregistrements, peut être utilisé tootrack et recréer les activités.</span><span class="sxs-lookup"><span data-stu-id="c7d03-124">**Activity tracking**: Since Kafka provides in-order logging of records, it can be used tootrack and re-create activities.</span></span> <span data-ttu-id="c7d03-125">Par exemple, les actions de l’utilisateur sur un site web ou dans une application.</span><span class="sxs-lookup"><span data-stu-id="c7d03-125">For example, user actions on a web site or within an application.</span></span>

* <span data-ttu-id="c7d03-126">**Agrégation**: à l’aide du traitement de flux de données, vous pouvez agréger des informations à partir de différents flux toocombine et centraliser des informations hello dans les données opérationnelles.</span><span class="sxs-lookup"><span data-stu-id="c7d03-126">**Aggregation**: Using stream processing, you can aggregate information from different streams toocombine and centralize hello information into operational data.</span></span>

* <span data-ttu-id="c7d03-127">**Transformation** : avec le traitement de flux de données, vous pouvez combiner et enrichir les données à partir de plusieurs rubriques d’entrée dans une ou plusieurs rubriques de sortie.</span><span class="sxs-lookup"><span data-stu-id="c7d03-127">**Transformation**: Using stream processing, you can combine and enrich data from multiple input topics into one or more output topics.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c7d03-128">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c7d03-128">Next steps</span></span>

<span data-ttu-id="c7d03-129">Toolearn de la façon dont liens suivants de hello utilisation toouse Kafka Apache sur HDInsight :</span><span class="sxs-lookup"><span data-stu-id="c7d03-129">Use hello following links toolearn how toouse Apache Kafka on HDInsight:</span></span>

* [<span data-ttu-id="c7d03-130">Prise en main de Kafka sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="c7d03-130">Get started with Kafka on HDInsight</span></span>](hdinsight-apache-kafka-get-started.md)

* [<span data-ttu-id="c7d03-131">Utilisez MirrorMaker toocreate un réplica de Kafka sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="c7d03-131">Use MirrorMaker toocreate a replica of Kafka on HDInsight</span></span>](hdinsight-apache-kafka-mirroring.md)

* [<span data-ttu-id="c7d03-132">Utilisation d’Apache Storm avec Kafka sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="c7d03-132">Use Apache Storm with Kafka on HDInsight</span></span>](hdinsight-apache-storm-with-kafka.md)

* <span data-ttu-id="c7d03-133">[Use Apache Spark with Kafka on HDInsight](hdinsight-apache-spark-with-kafka.md) (Utilisation d’Apache Spark avec Kafka sur HDInsight)</span><span class="sxs-lookup"><span data-stu-id="c7d03-133">[Use Apache Spark with Kafka on HDInsight](hdinsight-apache-spark-with-kafka.md)</span></span>

* [<span data-ttu-id="c7d03-134">Se connecter tooKafka via un réseau virtuel Azure</span><span class="sxs-lookup"><span data-stu-id="c7d03-134">Connect tooKafka through an Azure Virtual Network</span></span>](hdinsight-apache-kafka-connect-vpn-gateway.md)
