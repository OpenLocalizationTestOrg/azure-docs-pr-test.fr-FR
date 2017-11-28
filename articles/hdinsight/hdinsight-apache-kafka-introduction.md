---
title: "Présentation d’Apache Kafka sur HDInsight - Azure | Microsoft Docs"
description: "Découvrez Apache Kafka sur HDInsight : Présentation, fonctionnalités et exemples et informations de prise en main."
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
ms.openlocfilehash: 1976c52bd7fa56bb07104e205ab3699b2dfa4c50
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="introducing-apache-kafka-on-hdinsight-preview"></a><span data-ttu-id="f837f-103">Présentation d’Apache Kafka sur HDInsight (version préliminaire)</span><span class="sxs-lookup"><span data-stu-id="f837f-103">Introducing Apache Kafka on HDInsight (preview)</span></span>

<span data-ttu-id="f837f-104">[Apache Kafka](https://kafka.apache.org) est une plateforme de diffusion en continu distribuée open source qui permet de générer des pipelines de données et des applications de diffusion en continu en temps réel.</span><span class="sxs-lookup"><span data-stu-id="f837f-104">[Apache Kafka](https://kafka.apache.org) is an open-source distributed streaming platform that can be used to build real-time streaming data pipelines and applications.</span></span> <span data-ttu-id="f837f-105">Kafka fournit également des fonctionnalités de courtier de messages semblables à une file d’attente, où vous pouvez publier et vous abonner aux flux de données nommés.</span><span class="sxs-lookup"><span data-stu-id="f837f-105">Kafka also provides message broker functionality similar to a message queue, where you can publish and subscribe to named data streams.</span></span> <span data-ttu-id="f837f-106">Kafka sur HDInsight vous offre un service géré, hautement évolutif et hautement disponible dans le cloud Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="f837f-106">Kafka on HDInsight provides you with a managed, highly scalable, and highly available service in the Microsoft Azure cloud.</span></span>

## <a name="why-use-kafka-on-hdinsight"></a><span data-ttu-id="f837f-107">Pourquoi utiliser Kafka sur HDInsight ?</span><span class="sxs-lookup"><span data-stu-id="f837f-107">Why use Kafka on HDInsight?</span></span>

<span data-ttu-id="f837f-108">Kafka fournit les fonctionnalités suivantes :</span><span class="sxs-lookup"><span data-stu-id="f837f-108">Kafka provides the following features:</span></span>

* <span data-ttu-id="f837f-109">Modèle de messagerie de publication/abonnement : Kafka fournit une API de producteur pour la publication des enregistrements dans un sujet Kafka.</span><span class="sxs-lookup"><span data-stu-id="f837f-109">Publish-subscribe messaging pattern: Kafka provides a Producer API for publishing records to a Kafka topic.</span></span> <span data-ttu-id="f837f-110">L’API de consommateur est utilisée lors de l’abonnement à un sujet.</span><span class="sxs-lookup"><span data-stu-id="f837f-110">The Consumer API is used when subscribing to a topic.</span></span>

* <span data-ttu-id="f837f-111">Traitement des flux : Kafka est souvent utilisé avec Apache Storm ou Spark pour le traitement des flux en temps réel.</span><span class="sxs-lookup"><span data-stu-id="f837f-111">Stream processing: Kafka is often used with Apache Storm or Spark for real-time stream processing.</span></span> <span data-ttu-id="f837f-112">Kafka 0.10.0.0 (HDInsight version 3.5) a introduit une API de diffusion en continu qui vous permet de créer des solutions de diffusion en continu sans Storm ni Spark.</span><span class="sxs-lookup"><span data-stu-id="f837f-112">Kafka 0.10.0.0 (HDInsight version 3.5) introduced a streaming API that allows you to build streaming solutions without requiring Storm or Spark.</span></span>

* <span data-ttu-id="f837f-113">Évolution horizontale : Kafka partitionne les flux de données entre les nœuds du cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f837f-113">Horizontal scale: Kafka partitions streams across the nodes in the HDInsight cluster.</span></span> <span data-ttu-id="f837f-114">Les processus consommateur peuvent être associés à des partitions individuelles pour fournir un équilibrage de charge lors de l’utilisation des enregistrements.</span><span class="sxs-lookup"><span data-stu-id="f837f-114">Consumer processes can be associated with individual partitions to provide load balancing when consuming records.</span></span>

* <span data-ttu-id="f837f-115">Livraison chronologique : dans chaque partition, les enregistrements sont stockés dans le flux de données dans l’ordre de réception.</span><span class="sxs-lookup"><span data-stu-id="f837f-115">In-order delivery: Within each partition, records are stored in the stream in the order that they were received.</span></span> <span data-ttu-id="f837f-116">En associant un processus consommateur par partition, vous pouvez garantir que les enregistrements sont traités dans l’ordre.</span><span class="sxs-lookup"><span data-stu-id="f837f-116">By associating one consumer process per partition, you can guarantee that records are processed in-order.</span></span>

* <span data-ttu-id="f837f-117">Tolérance de pannes : les partitions peuvent être répliquées entre les nœuds pour fournir une tolérance de pannes.</span><span class="sxs-lookup"><span data-stu-id="f837f-117">Fault-tolerant: Partitions can be replicated between nodes to provide fault tolerance.</span></span>

* <span data-ttu-id="f837f-118">Intégration à Azure Managed Disks : Managed Disks disques offre une mise à l’échelle et un débit supérieurs pour les disques utilisés par les machines virtuelles du cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f837f-118">Integration with Azure Managed Disks: Managed disks provides higher scale and throughput for the disks used by the virtual machines in the HDInsight cluster.</span></span>

    <span data-ttu-id="f837f-119">Les disques gérés sont activés par défaut pour Kafka sur HDInsight, et le nombre de disques utilisés par le nœud peut être configuré lors de la création de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f837f-119">Managed disks are enabled by default for Kafka on HDInsight, and the number of disks used per node can be configured during HDInsight creation.</span></span> <span data-ttu-id="f837f-120">Pour plus d’informations sur les disques gérés, consultez [Azure Managed Disks](../virtual-machines/windows/managed-disks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f837f-120">For more information on managed disks, see [Azure Managed Disks](../virtual-machines/windows/managed-disks-overview.md).</span></span>

    <span data-ttu-id="f837f-121">Pour plus d’informations sur la configuration des disques gérés avec Kafka sur HDInsight, consultez [Increase scalability of Kafka on HDInsight](hdinsight-apache-kafka-scalability.md) (Augmenter l’évolutivité de Kafka sur HDInsight).</span><span class="sxs-lookup"><span data-stu-id="f837f-121">For information on configuring managed disks with Kafka on HDInsight, see [Increase scalability of Kafka on HDInsight](hdinsight-apache-kafka-scalability.md).</span></span>

## <a name="use-cases"></a><span data-ttu-id="f837f-122">Cas d'utilisation</span><span class="sxs-lookup"><span data-stu-id="f837f-122">Use cases</span></span>

* <span data-ttu-id="f837f-123">**Messagerie** : dans la mesure où Kafka prend en charge le modèle de messagerie publication/abonnement, il est souvent utilisé comme courtier de messages.</span><span class="sxs-lookup"><span data-stu-id="f837f-123">**Messaging**: Since it supports the publish-subscribe message pattern, Kafka is often used as a message broker.</span></span>

* <span data-ttu-id="f837f-124">**Suivi des activités** : étant donné que Kafka fournit la journalisation dans l’ordre des enregistrements, il peut être utilisé pour effectuer le suivi et recréer des activités.</span><span class="sxs-lookup"><span data-stu-id="f837f-124">**Activity tracking**: Since Kafka provides in-order logging of records, it can be used to track and re-create activities.</span></span> <span data-ttu-id="f837f-125">Par exemple, les actions de l’utilisateur sur un site web ou dans une application.</span><span class="sxs-lookup"><span data-stu-id="f837f-125">For example, user actions on a web site or within an application.</span></span>

* <span data-ttu-id="f837f-126">**Agrégation** : avec le traitement de flux de données, vous pouvez agréger des informations à partir de différents flux afin de combiner et de centraliser les informations dans des données opérationnelles.</span><span class="sxs-lookup"><span data-stu-id="f837f-126">**Aggregation**: Using stream processing, you can aggregate information from different streams to combine and centralize the information into operational data.</span></span>

* <span data-ttu-id="f837f-127">**Transformation** : avec le traitement de flux de données, vous pouvez combiner et enrichir les données à partir de plusieurs rubriques d’entrée dans une ou plusieurs rubriques de sortie.</span><span class="sxs-lookup"><span data-stu-id="f837f-127">**Transformation**: Using stream processing, you can combine and enrich data from multiple input topics into one or more output topics.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f837f-128">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f837f-128">Next steps</span></span>

<span data-ttu-id="f837f-129">Cliquez sur les liens suivants pour apprendre à utiliser Apache Kafka sur HDInsight :</span><span class="sxs-lookup"><span data-stu-id="f837f-129">Use the following links to learn how to use Apache Kafka on HDInsight:</span></span>

* [<span data-ttu-id="f837f-130">Prise en main de Kafka sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="f837f-130">Get started with Kafka on HDInsight</span></span>](hdinsight-apache-kafka-get-started.md)

* [<span data-ttu-id="f837f-131">Utilisation de MirrorMaker pour créer un réplica de Kafka sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="f837f-131">Use MirrorMaker to create a replica of Kafka on HDInsight</span></span>](hdinsight-apache-kafka-mirroring.md)

* <span data-ttu-id="f837f-132">[Use Apache Storm with Kafka on HDInsight](hdinsight-apache-storm-with-kafka.md) (Utilisation d’Apache Storm avec Kafka sur HDInsight)</span><span class="sxs-lookup"><span data-stu-id="f837f-132">[Use Apache Storm with Kafka on HDInsight](hdinsight-apache-storm-with-kafka.md)</span></span>

* <span data-ttu-id="f837f-133">[Use Apache Spark with Kafka on HDInsight](hdinsight-apache-spark-with-kafka.md) (Utilisation d’Apache Spark avec Kafka sur HDInsight)</span><span class="sxs-lookup"><span data-stu-id="f837f-133">[Use Apache Spark with Kafka on HDInsight](hdinsight-apache-spark-with-kafka.md)</span></span>

* <span data-ttu-id="f837f-134">[Connect to Kafka through an Azure Virtual Network](hdinsight-apache-kafka-connect-vpn-gateway.md) (Se connecter à Kafka via un réseau virtuel Azure)</span><span class="sxs-lookup"><span data-stu-id="f837f-134">[Connect to Kafka through an Azure Virtual Network](hdinsight-apache-kafka-connect-vpn-gateway.md)</span></span>