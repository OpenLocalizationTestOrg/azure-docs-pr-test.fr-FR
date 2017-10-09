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
# <a name="introducing-apache-kafka-on-hdinsight-preview"></a>Présentation d’Apache Kafka sur HDInsight (version préliminaire)

[Apache Kafka](https://kafka.apache.org) est une plate-forme de diffusion en continu distribuée open source qui peut être utilisé toobuild en temps réel de diffusion en continu des pipelines de données et applications. Kafka fournit également des fonctionnalités similaires tooa file d’attente, où vous pouvez publier et s’abonner à des flux de données toonamed courtier de messages. Kafka sur HDInsight vous offre un service géré, évolutif et hautement disponible dans le cloud de Microsoft Azure hello.

## <a name="why-use-kafka-on-hdinsight"></a>Pourquoi utiliser Kafka sur HDInsight ?

Kafka fournit hello suivant de fonctionnalités :

* Modèle de messagerie de publication / abonnement : Kafka fournit une API de production pour la publication des enregistrements tooa rubrique de Kafka. Hello consommateur API est utilisée lors de l’abonnement tooa rubrique.

* Traitement des flux : Kafka est souvent utilisé avec Apache Storm ou Spark pour le traitement des flux en temps réel. Kafka 0.10.0.0 (HDInsight version 3.5) a introduit une API de diffusion en continu qui vous permet de toobuild solutions de diffusion en continu sans Storm ou Spark.

* Échelle horizontale : Kafka partitionne les flux de données entre les nœuds de hello dans le cluster HDInsight de hello. Processus de consommateur peuvent être associés à des partitions individuelles tooprovide l’équilibrage de charge lors de l’utilisation des enregistrements.

* Commande livraison : au sein de chaque partition, les enregistrements sont stockés dans le flux hello dans l’ordre de hello qu’ils ont été reçus. En associant un processus consommateur par partition, vous pouvez garantir que les enregistrements sont traités dans l’ordre.

* À tolérance de pannes : Les Partitions peuvent être répliquées entre une tolérance de panne tooprovide nœuds.

* Intégration avec des disques gérés Azure : managé disques fournit plus élevé de débit et de mise à l’échelle pour les disques hello utilisés par les ordinateurs virtuels de hello dans le cluster HDInsight de hello.

    Disques gérés sont activées par défaut pour Kafka sur HDInsight et nombre de hello de disques utilisés par le nœud peut être configuré lors de la création de HDInsight. Pour plus d’informations sur les disques gérés, consultez [Azure Managed Disks](../virtual-machines/windows/managed-disks-overview.md).

    Pour plus d’informations sur la configuration des disques gérés avec Kafka sur HDInsight, consultez [Increase scalability of Kafka on HDInsight](hdinsight-apache-kafka-scalability.md) (Augmenter l’évolutivité de Kafka sur HDInsight).

## <a name="use-cases"></a>Cas d'utilisation

* **Messagerie**: car il prend en charge hello publication-abonnement de modèle de message, Kafka est souvent utilisé comme un courtier de messages.

* **Suivi des activités**: étant donné que Kafka fournit la journalisation dans l’ordre des enregistrements, peut être utilisé tootrack et recréer les activités. Par exemple, les actions de l’utilisateur sur un site web ou dans une application.

* **Agrégation**: à l’aide du traitement de flux de données, vous pouvez agréger des informations à partir de différents flux toocombine et centraliser des informations hello dans les données opérationnelles.

* **Transformation** : avec le traitement de flux de données, vous pouvez combiner et enrichir les données à partir de plusieurs rubriques d’entrée dans une ou plusieurs rubriques de sortie.

## <a name="next-steps"></a>Étapes suivantes

Toolearn de la façon dont liens suivants de hello utilisation toouse Kafka Apache sur HDInsight :

* [Prise en main de Kafka sur HDInsight](hdinsight-apache-kafka-get-started.md)

* [Utilisez MirrorMaker toocreate un réplica de Kafka sur HDInsight](hdinsight-apache-kafka-mirroring.md)

* [Utilisation d’Apache Storm avec Kafka sur HDInsight](hdinsight-apache-storm-with-kafka.md)

* [Use Apache Spark with Kafka on HDInsight](hdinsight-apache-spark-with-kafka.md) (Utilisation d’Apache Spark avec Kafka sur HDInsight)

* [Se connecter tooKafka via un réseau virtuel Azure](hdinsight-apache-kafka-connect-vpn-gateway.md)
