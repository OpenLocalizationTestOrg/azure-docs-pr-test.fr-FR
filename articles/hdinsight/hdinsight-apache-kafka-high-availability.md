---
title: "disponibilité aaaHigh avec Apache Kafka - Azure HDInsight | Documents Microsoft"
description: "Découvrez comment tooensure haute disponibilité avec Kafka Apache sur Azure HDInsight. Découvrez comment toorebalance partitionner les réplicas dans Kafka afin qu’ils soient sur différents domaines d’erreur dans hello région Azure qui contient HDInsight."
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
ms.openlocfilehash: 337468f36b531f83c2999e87907de89cf3d19dd4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="high-availability-of-your-data-with-apache-kafka-preview-on-hdinsight"></a><span data-ttu-id="12c4b-104">Haute disponibilité de vos données avec Apache Kafka (version préliminaire) sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="12c4b-104">High availability of your data with Apache Kafka (preview) on HDInsight</span></span>

<span data-ttu-id="12c4b-105">Découvrez comment tooconfigure les réplicas de partition pour avantage de tootake Kafka rubriques du matériel sous-jacent en rack de configuration.</span><span class="sxs-lookup"><span data-stu-id="12c4b-105">Learn how tooconfigure partition replicas for Kafka topics tootake advantage of underlying hardware rack configuration.</span></span> <span data-ttu-id="12c4b-106">Cette configuration garantit la disponibilité de hello des données stockées dans Kafka Apache sur HDInsight.</span><span class="sxs-lookup"><span data-stu-id="12c4b-106">This configuration ensures hello availability of data stored in Apache Kafka on HDInsight.</span></span>

## <a name="fault-and-update-domains-with-kafka"></a><span data-ttu-id="12c4b-107">Domaines d’erreur et de mise à jour avec Kafka</span><span class="sxs-lookup"><span data-stu-id="12c4b-107">Fault and update domains with Kafka</span></span>

<span data-ttu-id="12c4b-108">Un domaine d’erreur est un regroupement logique de matériel sous-jacent dans un datacenter Azure.</span><span class="sxs-lookup"><span data-stu-id="12c4b-108">A fault domain is a logical grouping of underlying hardware in an Azure data center.</span></span> <span data-ttu-id="12c4b-109">Chaque domaine d’erreur partage une source d’alimentation et un commutateur réseau communs.</span><span class="sxs-lookup"><span data-stu-id="12c4b-109">Each fault domain shares a common power source and network switch.</span></span> <span data-ttu-id="12c4b-110">machines virtuelles de Hello et des disques gérés qui implémentent des nœuds hello au sein d’un cluster HDInsight sont distribués dans ces domaines d’erreur.</span><span class="sxs-lookup"><span data-stu-id="12c4b-110">hello virtual machines and managed disks that implement hello nodes within an HDInsight cluster are distributed across these fault domains.</span></span> <span data-ttu-id="12c4b-111">Cette architecture limite l’impact potentiel de hello d’échecs de matériel physique.</span><span class="sxs-lookup"><span data-stu-id="12c4b-111">This architecture limits hello potential impact of physical hardware failures.</span></span>

<span data-ttu-id="12c4b-112">Chaque région Azure possède un certain nombre de domaines d’erreur.</span><span class="sxs-lookup"><span data-stu-id="12c4b-112">Each Azure region has a specific number of fault domains.</span></span> <span data-ttu-id="12c4b-113">Pour obtenir la liste de domaines et nombre hello de domaines d’erreur qu’ils contiennent, consultez hello [à haute disponibilité](../virtual-machines/linux/regions-and-availability.md#availability-sets) documentation.</span><span class="sxs-lookup"><span data-stu-id="12c4b-113">For a list of domains and hello number of fault domains they contain, see hello [Availability sets](../virtual-machines/linux/regions-and-availability.md#availability-sets) documentation.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="12c4b-114">Kafka n’est pas informé des domaines d’erreur.</span><span class="sxs-lookup"><span data-stu-id="12c4b-114">Kafka is not aware of fault domains.</span></span> <span data-ttu-id="12c4b-115">Lorsque vous créez une rubrique dans Kafka, il peut stocker tous les réplicas de partition Bonjour même domaine par défaut.</span><span class="sxs-lookup"><span data-stu-id="12c4b-115">When you create a topic in Kafka, it may store all partition replicas in hello same fault domain.</span></span> <span data-ttu-id="12c4b-116">toosolve ce problème, nous fournissons hello [outil rééquilibrage de partition Kafka](https://github.com/hdinsight/hdinsight-kafka-tools).</span><span class="sxs-lookup"><span data-stu-id="12c4b-116">toosolve this problem, we provide hello [Kafka partition rebalance tool](https://github.com/hdinsight/hdinsight-kafka-tools).</span></span>

## <a name="when-toorebalance-partition-replicas"></a><span data-ttu-id="12c4b-117">Lorsque la partition toorebalance réplicas</span><span class="sxs-lookup"><span data-stu-id="12c4b-117">When toorebalance partition replicas</span></span>

<span data-ttu-id="12c4b-118">tooensure hello optimiser la disponibilité de vos données Kafka, vous devez rééquilibrer les réplicas de partition hello pour votre rubrique à hello suivant fois :</span><span class="sxs-lookup"><span data-stu-id="12c4b-118">tooensure hello highest availability of your Kafka data, you should rebalance hello partition replicas for your topic at hello following times:</span></span>

* <span data-ttu-id="12c4b-119">Lorsqu’une rubrique ou une partition est créée</span><span class="sxs-lookup"><span data-stu-id="12c4b-119">When a new topic or partition is created</span></span>

* <span data-ttu-id="12c4b-120">Lorsque vous mettez à l’échelle un cluster</span><span class="sxs-lookup"><span data-stu-id="12c4b-120">When you scale up a cluster</span></span>

## <a name="replication-factor"></a><span data-ttu-id="12c4b-121">Facteur de réplication</span><span class="sxs-lookup"><span data-stu-id="12c4b-121">Replication factor</span></span>

> [!IMPORTANT]
> <span data-ttu-id="12c4b-122">Il est recommandé d’utiliser une région Azure qui contient les trois domaines d’erreur, et un facteur de réplication de 3.</span><span class="sxs-lookup"><span data-stu-id="12c4b-122">We recommend using an Azure region that contains three fault domains, and using a replication factor of 3.</span></span>

<span data-ttu-id="12c4b-123">Si vous devez utiliser une région qui contient uniquement deux domaines d’erreur, utilisez un facteur de réplication de 4 réplicas de hello toospread uniformément entre les deux domaines d’erreur hello.</span><span class="sxs-lookup"><span data-stu-id="12c4b-123">If you must use a region that contains only two fault domains, use a replication factor of 4 toospread hello replicas evenly across hello two fault domains.</span></span>

<span data-ttu-id="12c4b-124">Pour obtenir un exemple de création de rubriques et le facteur de réplication paramètre hello, consultez hello [démarrer avec Kafka sur HDInsight](hdinsight-apache-kafka-get-started.md) document.</span><span class="sxs-lookup"><span data-stu-id="12c4b-124">For an example of creating topics and setting hello replication factor, see hello [Start with Kafka on HDInsight](hdinsight-apache-kafka-get-started.md) document.</span></span>

## <a name="how-toorebalance-partition-replicas"></a><span data-ttu-id="12c4b-125">Réplicas de partition toorebalance</span><span class="sxs-lookup"><span data-stu-id="12c4b-125">How toorebalance partition replicas</span></span>

<span data-ttu-id="12c4b-126">Hello d’utilisation [outil rééquilibrage de partition Kafka](https://github.com/hdinsight/hdinsight-kafka-tools) toorebalance les rubriques sélectionnées.</span><span class="sxs-lookup"><span data-stu-id="12c4b-126">Use hello [Kafka partition rebalance tool](https://github.com/hdinsight/hdinsight-kafka-tools) toorebalance selected topics.</span></span> <span data-ttu-id="12c4b-127">Cet outil doit être exécuté à partir d’un nœud principal SSH session toohello de votre cluster Kafka.</span><span class="sxs-lookup"><span data-stu-id="12c4b-127">This tool must be ran from an SSH session toohello head node of your Kafka cluster.</span></span>

<span data-ttu-id="12c4b-128">Pour plus d’informations sur la connexion à l’aide de SSH de tooHDInsight, consultez la [utilisation de SSH avec HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span><span class="sxs-lookup"><span data-stu-id="12c4b-128">For more information on connecting tooHDInsight using SSH, see the [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

## <a name="next-steps"></a><span data-ttu-id="12c4b-129">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="12c4b-129">Next steps</span></span>

* [<span data-ttu-id="12c4b-130">Évolutivité de Kafka sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="12c4b-130">Scalability of Kafka on HDInsight</span></span>](hdinsight-apache-kafka-scalability.md)
* [<span data-ttu-id="12c4b-131">Mise en miroir avec Kafka sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="12c4b-131">Mirroring with Kafka on HDInsight</span></span>](hdinsight-apache-kafka-mirroring.md)