---
title: "Haute disponibilité avec Apache Kafka - Azure HDInsight | Microsoft Docs"
description: "Découvrez comment garantir une haute disponibilité avec Apache Kafka sur Azure HDInsight. Apprenez à rééquilibrer les réplicas de partition dans Kafka afin qu’ils soient répartis sur différents domaines d’erreur dans la région Azure qui contient HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: 
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/26/2017
ms.author: larryfr
ms.openlocfilehash: f8164d1c3483b28e5f2abcc8035da78880daec1e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="high-availability-of-your-data-with-apache-kafka-preview-on-hdinsight"></a><span data-ttu-id="7e946-104">Haute disponibilité de vos données avec Apache Kafka (version préliminaire) sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="7e946-104">High availability of your data with Apache Kafka (preview) on HDInsight</span></span>

<span data-ttu-id="7e946-105">Découvrez comment configurer des réplicas de partition pour les rubriques Kafka afin de tirer parti de la configuration de rack matériel sous-jacent.</span><span class="sxs-lookup"><span data-stu-id="7e946-105">Learn how to configure partition replicas for Kafka topics to take advantage of underlying hardware rack configuration.</span></span> <span data-ttu-id="7e946-106">Cette configuration garantit la disponibilité des données stockées dans Kafka Apache sur HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7e946-106">This configuration ensures the availability of data stored in Apache Kafka on HDInsight.</span></span>

## <a name="fault-and-update-domains-with-kafka"></a><span data-ttu-id="7e946-107">Domaines d’erreur et de mise à jour avec Kafka</span><span class="sxs-lookup"><span data-stu-id="7e946-107">Fault and update domains with Kafka</span></span>

<span data-ttu-id="7e946-108">Un domaine d’erreur est un regroupement logique de matériel sous-jacent dans un datacenter Azure.</span><span class="sxs-lookup"><span data-stu-id="7e946-108">A fault domain is a logical grouping of underlying hardware in an Azure data center.</span></span> <span data-ttu-id="7e946-109">Chaque domaine d’erreur partage une source d’alimentation et un commutateur réseau communs.</span><span class="sxs-lookup"><span data-stu-id="7e946-109">Each fault domain shares a common power source and network switch.</span></span> <span data-ttu-id="7e946-110">Les ordinateurs virtuels et les disques gérés mettant en œuvre les nœuds au sein d’un cluster HDInsight sont répartis dans ces domaines d’erreur.</span><span class="sxs-lookup"><span data-stu-id="7e946-110">The virtual machines and managed disks that implement the nodes within an HDInsight cluster are distributed across these fault domains.</span></span> <span data-ttu-id="7e946-111">Cette architecture limite l’impact potentiel des défaillances de matériel physique.</span><span class="sxs-lookup"><span data-stu-id="7e946-111">This architecture limits the potential impact of physical hardware failures.</span></span>

<span data-ttu-id="7e946-112">Chaque région Azure possède un certain nombre de domaines d’erreur.</span><span class="sxs-lookup"><span data-stu-id="7e946-112">Each Azure region has a specific number of fault domains.</span></span> <span data-ttu-id="7e946-113">Pour obtenir la liste des domaines et le nombre de domaines d’erreur qu’ils contiennent, consultez la documentation [Groupes à haute disponibilité](../virtual-machines/linux/regions-and-availability.md#availability-sets).</span><span class="sxs-lookup"><span data-stu-id="7e946-113">For a list of domains and the number of fault domains they contain, see the [Availability sets](../virtual-machines/linux/regions-and-availability.md#availability-sets) documentation.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7e946-114">Kafka n’est pas informé des domaines d’erreur.</span><span class="sxs-lookup"><span data-stu-id="7e946-114">Kafka is not aware of fault domains.</span></span> <span data-ttu-id="7e946-115">Lorsque vous créez une rubrique dans Kafka, ce dernier peut stocker tous les réplicas de partition dans le même domaine d’erreur.</span><span class="sxs-lookup"><span data-stu-id="7e946-115">When you create a topic in Kafka, it may store all partition replicas in the same fault domain.</span></span> <span data-ttu-id="7e946-116">Pour résoudre ce problème, nous fournissons [l’outil de rééquilibrage de partitions Kafka](https://github.com/hdinsight/hdinsight-kafka-tools).</span><span class="sxs-lookup"><span data-stu-id="7e946-116">To solve this problem, we provide the [Kafka partition rebalance tool](https://github.com/hdinsight/hdinsight-kafka-tools).</span></span>

## <a name="when-to-rebalance-partition-replicas"></a><span data-ttu-id="7e946-117">Quand rééquilibrer les réplicas de partition</span><span class="sxs-lookup"><span data-stu-id="7e946-117">When to rebalance partition replicas</span></span>

<span data-ttu-id="7e946-118">Pour garantir la haute disponibilité de vos données Kafka, vous devez rééquilibrer les réplicas de partition de votre rubrique aux heures suivantes :</span><span class="sxs-lookup"><span data-stu-id="7e946-118">To ensure the highest availability of your Kafka data, you should rebalance the partition replicas for your topic at the following times:</span></span>

* <span data-ttu-id="7e946-119">Lorsqu’une rubrique ou une partition est créée</span><span class="sxs-lookup"><span data-stu-id="7e946-119">When a new topic or partition is created</span></span>

* <span data-ttu-id="7e946-120">Lorsque vous mettez à l’échelle un cluster</span><span class="sxs-lookup"><span data-stu-id="7e946-120">When you scale up a cluster</span></span>

## <a name="replication-factor"></a><span data-ttu-id="7e946-121">Facteur de réplication</span><span class="sxs-lookup"><span data-stu-id="7e946-121">Replication factor</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7e946-122">Il est recommandé d’utiliser une région Azure qui contient les trois domaines d’erreur, et un facteur de réplication de 3.</span><span class="sxs-lookup"><span data-stu-id="7e946-122">We recommend using an Azure region that contains three fault domains, and using a replication factor of 3.</span></span>

<span data-ttu-id="7e946-123">Si vous devez utiliser une région qui contient uniquement deux domaines d’erreur, utilisez un facteur de réplication de 4 afin de répartir uniformément les réplicas sur les domaines d’erreur.</span><span class="sxs-lookup"><span data-stu-id="7e946-123">If you must use a region that contains only two fault domains, use a replication factor of 4 to spread the replicas evenly across the two fault domains.</span></span>

<span data-ttu-id="7e946-124">Pour obtenir un exemple de création de rubriques et de paramétrage du facteur de réplication, consultez le document [Démarrer avec Kafka sur HDInsight](hdinsight-apache-kafka-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="7e946-124">For an example of creating topics and setting the replication factor, see the [Start with Kafka on HDInsight](hdinsight-apache-kafka-get-started.md) document.</span></span>

## <a name="how-to-rebalance-partition-replicas"></a><span data-ttu-id="7e946-125">Comment rééquilibrer les réplicas de partition</span><span class="sxs-lookup"><span data-stu-id="7e946-125">How to rebalance partition replicas</span></span>

<span data-ttu-id="7e946-126">Utilisez [l’outil rééquilibrage de partition Kafka](https://github.com/hdinsight/hdinsight-kafka-tools) pour rééquilibrer les rubriques sélectionnées.</span><span class="sxs-lookup"><span data-stu-id="7e946-126">Use the [Kafka partition rebalance tool](https://github.com/hdinsight/hdinsight-kafka-tools) to rebalance selected topics.</span></span> <span data-ttu-id="7e946-127">Cet outil doit être exécuté à partir d’une session SSH pour le nœud principal de votre cluster Kafka.</span><span class="sxs-lookup"><span data-stu-id="7e946-127">This tool must be ran from an SSH session to the head node of your Kafka cluster.</span></span>

<span data-ttu-id="7e946-128">Pour plus d’informations sur la connexion à HDInsight avec SSH, consultez le document [Utilisation de SSH avec HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="7e946-128">For more information on connecting to HDInsight using SSH, see the [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7e946-129">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="7e946-129">Next steps</span></span>

* [<span data-ttu-id="7e946-130">Évolutivité de Kafka sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="7e946-130">Scalability of Kafka on HDInsight</span></span>](hdinsight-apache-kafka-scalability.md)
* [<span data-ttu-id="7e946-131">Mise en miroir avec Kafka sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="7e946-131">Mirroring with Kafka on HDInsight</span></span>](hdinsight-apache-kafka-mirroring.md)