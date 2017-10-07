---
title: "aaaApache Kafka augmente l’échelle - Azure HDInsight | Documents Microsoft"
description: "Découvrez comment tooconfigure des disques gérés par cluster Apache Kafka sur Azure HDInsight tooincrease évolutivité."
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
ms.date: 06/14/2017
ms.author: larryfr
ms.openlocfilehash: b51114b33359f2c385f057a7a7a5b134cad27e51
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-storage-and-scalability-for-apache-kafka-on-hdinsight"></a><span data-ttu-id="50959-103">Configurer le stockage et l’extensibilité pour Apache Kafka sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="50959-103">Configure storage and scalability for Apache Kafka on HDInsight</span></span>

<span data-ttu-id="50959-104">Découvrez comment le nombre de hello tooconfigure de disques gérés utilisé par Kafka Apache sur HDInsight.</span><span class="sxs-lookup"><span data-stu-id="50959-104">Learn how tooconfigure hello number of managed disks used by Apache Kafka on HDInsight.</span></span>

<span data-ttu-id="50959-105">Kafka sur HDInsight utilise un disque local de hello d’ordinateurs virtuels hello dans le cluster HDInsight de hello.</span><span class="sxs-lookup"><span data-stu-id="50959-105">Kafka on HDInsight uses hello local disk of hello virtual machines in hello HDInsight cluster.</span></span> <span data-ttu-id="50959-106">Kafka étant e/s très importante, [disques gérés d’Azure](../virtual-machines/windows/managed-disks-overview.md) tooprovide utilisé un débit élevé et pour fournir plus de stockage par nœud.</span><span class="sxs-lookup"><span data-stu-id="50959-106">Since Kafka is very I/O heavy, [Azure Managed Disks](../virtual-machines/windows/managed-disks-overview.md) is used tooprovide high throughput and provide more storage per node.</span></span> <span data-ttu-id="50959-107">Si traditionnel des disques durs virtuels (VHD) ont été utilisés pour Kafka, chaque nœud est limité too1 to.</span><span class="sxs-lookup"><span data-stu-id="50959-107">If traditional virtual hard drives (VHD) were used for Kafka, each node is limited too1 TB.</span></span> <span data-ttu-id="50959-108">Avec des disques gérés, vous pouvez utiliser plusieurs disques tooachieve pour chaque nœud de cluster de hello jusqu'à 16 To.</span><span class="sxs-lookup"><span data-stu-id="50959-108">With managed disks, you can use multiple disks tooachieve 16 TB for each node in hello cluster.</span></span>

<span data-ttu-id="50959-109">Hello diagramme suivant fournit une comparaison entre Kafka sur HDInsight avant de disques gérés et Kafka sur HDInsight avec disques gérés :</span><span class="sxs-lookup"><span data-stu-id="50959-109">hello following diagram provides a comparison between Kafka on HDInsight before managed disks, and Kafka on HDInsight with managed disks:</span></span>

![Diagramme illustrant l’utilisation de Kafka sur HDInsight avec un seul VHD par machine virtuelle et avec plusieurs disques gérés par machine virtuelle](./media/hdinsight-apache-kafka-scalability/kafka-with-managed-disks-architecture.png)

## <a name="configure-managed-disks-azure-portal"></a><span data-ttu-id="50959-111">Configurer les disques gérés : Portail Azure</span><span class="sxs-lookup"><span data-stu-id="50959-111">Configure managed disks: Azure portal</span></span>

1. <span data-ttu-id="50959-112">Suivez les étapes de hello Bonjour [créer un cluster HDInsight](hdinsight-hadoop-create-linux-clusters-portal.md) hello toounderstand commun étapes toocreate un cluster à l’aide du portail de hello.</span><span class="sxs-lookup"><span data-stu-id="50959-112">Follow hello steps in hello [Create an HDInsight cluster](hdinsight-hadoop-create-linux-clusters-portal.md) toounderstand hello common steps toocreate a cluster using hello portal.</span></span> <span data-ttu-id="50959-113">N’effectuez pas le processus de création de portail hello.</span><span class="sxs-lookup"><span data-stu-id="50959-113">Do not complete hello portal creation process.</span></span>

2. <span data-ttu-id="50959-114">À partir de hello __taille de Cluster__ panneau, utilisez hello __disques par nœud de travail__ champ nombre de hello tooconfigure de disques.</span><span class="sxs-lookup"><span data-stu-id="50959-114">From hello __Cluster size__ blade, use hello __Disks per worker node__ field tooconfigure hello number of disks.</span></span>

    > [!NOTE]
    > <span data-ttu-id="50959-115">Hello type de disque géré peut être soit __Standard__ (HDD) ou __Premium__ (SSD).</span><span class="sxs-lookup"><span data-stu-id="50959-115">hello type of managed disk can be either __Standard__ (HDD) or __Premium__ (SSD).</span></span> <span data-ttu-id="50959-116">Les disques Premium sont utilisés avec les machines virtuelles séries DS et GS.</span><span class="sxs-lookup"><span data-stu-id="50959-116">Premium disks are used with DS and GS series VMs.</span></span> <span data-ttu-id="50959-117">Tous les autres types de machines virtuelles utilisent des disques Standard.</span><span class="sxs-lookup"><span data-stu-id="50959-117">All other VM types use standard.</span></span>

    ![Image du Panneau de taille de cluster hello avec disques hello par nœud de travail mis en surbrillance](./media/hdinsight-apache-kafka-scalability/set-managed-disks-portal.png)

## <a name="configure-managed-disks-resource-manager-template"></a><span data-ttu-id="50959-119">Configurer les disques gérés : modèle Resource Manager</span><span class="sxs-lookup"><span data-stu-id="50959-119">Configure managed disks: Resource Manager template</span></span>

<span data-ttu-id="50959-120">nombre de hello toocontrol de disques utilisés par les nœuds de travail hello dans un cluster Kafka, hello utilisation après la section du modèle de hello :</span><span class="sxs-lookup"><span data-stu-id="50959-120">toocontrol hello number of disks used by hello worker nodes in a Kafka cluster, use hello following section of hello template:</span></span>

```json
"dataDisksGroups": [
    {
        "disksPerNode": "[variables('disksPerWorkerNode')]"
    }
    ],
```

<span data-ttu-id="50959-121">Vous pouvez trouver un modèle complet qui montre comment tooconfigure des disques gérés par à [https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json](https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json).</span><span class="sxs-lookup"><span data-stu-id="50959-121">You can find a complete template that demonstrates how tooconfigure managed disks at [https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json](https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json).</span></span>

## <a name="next-steps"></a><span data-ttu-id="50959-122">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="50959-122">Next steps</span></span>

<span data-ttu-id="50959-123">Pour plus d’informations sur l’utilisation avec Kafka sur HDInsight, consultez hello suivant des documents :</span><span class="sxs-lookup"><span data-stu-id="50959-123">For more information on working with Kafka on HDInsight, see hello following documents:</span></span>

* [<span data-ttu-id="50959-124">Utilisez MirrorMaker toocreate un réplica de Kafka sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="50959-124">Use MirrorMaker toocreate a replica of Kafka on HDInsight</span></span>](hdinsight-apache-kafka-mirroring.md)
* [<span data-ttu-id="50959-125">Utilisation d’Apache Storm avec Kafka sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="50959-125">Use Apache Storm with Kafka on HDInsight</span></span>](hdinsight-apache-storm-with-kafka.md)
* <span data-ttu-id="50959-126">[Use Apache Spark with Kafka on HDInsight](hdinsight-apache-spark-with-kafka.md) (Utilisation d’Apache Spark avec Kafka sur HDInsight)</span><span class="sxs-lookup"><span data-stu-id="50959-126">[Use Apache Spark with Kafka on HDInsight](hdinsight-apache-spark-with-kafka.md)</span></span>
* [<span data-ttu-id="50959-127">Se connecter tooKafka via un réseau virtuel Azure</span><span class="sxs-lookup"><span data-stu-id="50959-127">Connect tooKafka through an Azure Virtual Network</span></span>](hdinsight-apache-kafka-connect-vpn-gateway.md)

* [<span data-ttu-id="50959-128">Blog HDInsight sur les disques gérés avec Kafka</span><span class="sxs-lookup"><span data-stu-id="50959-128">HDInsight blog on managed disks with Kafka</span></span>](https://azure.microsoft.com/blog/announcing-public-preview-of-apache-kafka-on-hdinsight-with-azure-managed-disks/)