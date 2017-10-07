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
# <a name="high-availability-of-your-data-with-apache-kafka-preview-on-hdinsight"></a>Haute disponibilité de vos données avec Apache Kafka (version préliminaire) sur HDInsight

Découvrez comment tooconfigure les réplicas de partition pour avantage de tootake Kafka rubriques du matériel sous-jacent en rack de configuration. Cette configuration garantit la disponibilité de hello des données stockées dans Kafka Apache sur HDInsight.

## <a name="fault-and-update-domains-with-kafka"></a>Domaines d’erreur et de mise à jour avec Kafka

Un domaine d’erreur est un regroupement logique de matériel sous-jacent dans un datacenter Azure. Chaque domaine d’erreur partage une source d’alimentation et un commutateur réseau communs. machines virtuelles de Hello et des disques gérés qui implémentent des nœuds hello au sein d’un cluster HDInsight sont distribués dans ces domaines d’erreur. Cette architecture limite l’impact potentiel de hello d’échecs de matériel physique.

Chaque région Azure possède un certain nombre de domaines d’erreur. Pour obtenir la liste de domaines et nombre hello de domaines d’erreur qu’ils contiennent, consultez hello [à haute disponibilité](../virtual-machines/linux/regions-and-availability.md#availability-sets) documentation.

> [!IMPORTANT]
> Kafka n’est pas informé des domaines d’erreur. Lorsque vous créez une rubrique dans Kafka, il peut stocker tous les réplicas de partition Bonjour même domaine par défaut. toosolve ce problème, nous fournissons hello [outil rééquilibrage de partition Kafka](https://github.com/hdinsight/hdinsight-kafka-tools).

## <a name="when-toorebalance-partition-replicas"></a>Lorsque la partition toorebalance réplicas

tooensure hello optimiser la disponibilité de vos données Kafka, vous devez rééquilibrer les réplicas de partition hello pour votre rubrique à hello suivant fois :

* Lorsqu’une rubrique ou une partition est créée

* Lorsque vous mettez à l’échelle un cluster

## <a name="replication-factor"></a>Facteur de réplication

> [!IMPORTANT]
> Il est recommandé d’utiliser une région Azure qui contient les trois domaines d’erreur, et un facteur de réplication de 3.

Si vous devez utiliser une région qui contient uniquement deux domaines d’erreur, utilisez un facteur de réplication de 4 réplicas de hello toospread uniformément entre les deux domaines d’erreur hello.

Pour obtenir un exemple de création de rubriques et le facteur de réplication paramètre hello, consultez hello [démarrer avec Kafka sur HDInsight](hdinsight-apache-kafka-get-started.md) document.

## <a name="how-toorebalance-partition-replicas"></a>Réplicas de partition toorebalance

Hello d’utilisation [outil rééquilibrage de partition Kafka](https://github.com/hdinsight/hdinsight-kafka-tools) toorebalance les rubriques sélectionnées. Cet outil doit être exécuté à partir d’un nœud principal SSH session toohello de votre cluster Kafka.

Pour plus d’informations sur la connexion à l’aide de SSH de tooHDInsight, consultez la [utilisation de SSH avec HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.

## <a name="next-steps"></a>Étapes suivantes

* [Évolutivité de Kafka sur HDInsight](hdinsight-apache-kafka-scalability.md)
* [Mise en miroir avec Kafka sur HDInsight](hdinsight-apache-kafka-mirroring.md)