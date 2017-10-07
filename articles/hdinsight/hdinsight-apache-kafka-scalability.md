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
# <a name="configure-storage-and-scalability-for-apache-kafka-on-hdinsight"></a>Configurer le stockage et l’extensibilité pour Apache Kafka sur HDInsight

Découvrez comment le nombre de hello tooconfigure de disques gérés utilisé par Kafka Apache sur HDInsight.

Kafka sur HDInsight utilise un disque local de hello d’ordinateurs virtuels hello dans le cluster HDInsight de hello. Kafka étant e/s très importante, [disques gérés d’Azure](../virtual-machines/windows/managed-disks-overview.md) tooprovide utilisé un débit élevé et pour fournir plus de stockage par nœud. Si traditionnel des disques durs virtuels (VHD) ont été utilisés pour Kafka, chaque nœud est limité too1 to. Avec des disques gérés, vous pouvez utiliser plusieurs disques tooachieve pour chaque nœud de cluster de hello jusqu'à 16 To.

Hello diagramme suivant fournit une comparaison entre Kafka sur HDInsight avant de disques gérés et Kafka sur HDInsight avec disques gérés :

![Diagramme illustrant l’utilisation de Kafka sur HDInsight avec un seul VHD par machine virtuelle et avec plusieurs disques gérés par machine virtuelle](./media/hdinsight-apache-kafka-scalability/kafka-with-managed-disks-architecture.png)

## <a name="configure-managed-disks-azure-portal"></a>Configurer les disques gérés : Portail Azure

1. Suivez les étapes de hello Bonjour [créer un cluster HDInsight](hdinsight-hadoop-create-linux-clusters-portal.md) hello toounderstand commun étapes toocreate un cluster à l’aide du portail de hello. N’effectuez pas le processus de création de portail hello.

2. À partir de hello __taille de Cluster__ panneau, utilisez hello __disques par nœud de travail__ champ nombre de hello tooconfigure de disques.

    > [!NOTE]
    > Hello type de disque géré peut être soit __Standard__ (HDD) ou __Premium__ (SSD). Les disques Premium sont utilisés avec les machines virtuelles séries DS et GS. Tous les autres types de machines virtuelles utilisent des disques Standard.

    ![Image du Panneau de taille de cluster hello avec disques hello par nœud de travail mis en surbrillance](./media/hdinsight-apache-kafka-scalability/set-managed-disks-portal.png)

## <a name="configure-managed-disks-resource-manager-template"></a>Configurer les disques gérés : modèle Resource Manager

nombre de hello toocontrol de disques utilisés par les nœuds de travail hello dans un cluster Kafka, hello utilisation après la section du modèle de hello :

```json
"dataDisksGroups": [
    {
        "disksPerNode": "[variables('disksPerWorkerNode')]"
    }
    ],
```

Vous pouvez trouver un modèle complet qui montre comment tooconfigure des disques gérés par à [https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json](https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json).

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur l’utilisation avec Kafka sur HDInsight, consultez hello suivant des documents :

* [Utilisez MirrorMaker toocreate un réplica de Kafka sur HDInsight](hdinsight-apache-kafka-mirroring.md)
* [Utilisation d’Apache Storm avec Kafka sur HDInsight](hdinsight-apache-storm-with-kafka.md)
* [Use Apache Spark with Kafka on HDInsight](hdinsight-apache-spark-with-kafka.md) (Utilisation d’Apache Spark avec Kafka sur HDInsight)
* [Se connecter tooKafka via un réseau virtuel Azure](hdinsight-apache-kafka-connect-vpn-gateway.md)

* [Blog HDInsight sur les disques gérés avec Kafka](https://azure.microsoft.com/blog/announcing-public-preview-of-apache-kafka-on-hdinsight-with-azure-managed-disks/)