---
title: aaaApache Spark diffusion en continu avec Kafka - Azure HDInsight | Documents Microsoft
description: "Découvrez comment toouse Spark Apache Spark toostream de données dans ou hors Kafka Apache à l’aide de DStreams. Dans cet exemple, vous diffusez des données à l’aide d’un bloc-notes Jupyter à partir de Spark sur HDInsight."
keywords: exemple kafka, zookeeper kafka, kafka de diffusion spark, exemple kafka de diffusion spark
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: dd8f53c1-bdee-4921-b683-3be4c46c2039
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: 
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/13/2017
ms.author: larryfr
ms.openlocfilehash: f48b37aadafa4979cd27af68e8417db6acc8a0e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="apache-spark-streaming-dstream-example-with-kafka-preview-on-hdinsight"></a>Exemple Apache Spark Streaming (DStream) avec Kafka (aperçu) sur HDInsight

Découvrez comment toouse Spark Apache Spark toostream de données dans ou hors Kafka Apache sur HDInsight à l’aide de DStreams. Cet exemple utilise un bloc-notes jupyter qui s’exécute sur un cluster de Spark hello.
> [!NOTE]
> étapes Hello dans ce document créent un groupe de ressources Azure qui contient à la fois un Spark sur HDInsight et un Kafka sur le cluster HDInsight. Ces clusters sont situés dans un réseau virtuel Azure, ce qui permet de hello toodirectly de cluster Spark communiquent avec hello cluster de Kafka.
>
> Lorsque vous avez terminé les étapes hello dans ce document, n’oubliez pas de frais supplémentaires de toodelete hello clusters tooavoid.

## <a name="create-hello-clusters"></a>Créer des clusters de hello

Kafka Apache sur HDInsight ne fournit pas d’accès toohello Kafka courtiers sur hello internet public. Tout ce qui tooKafka doit se trouver dans des entretiens hello même réseau virtuel Azure en tant que nœuds hello dans hello cluster de Kafka. Pour cet exemple, hello Kafka et les clusters Spark se trouvent dans un réseau virtuel Azure. Hello diagramme suivant illustre le flux de communication entre les clusters hello :

![Diagramme des clusters Spark et Kafka dans un réseau virtuel Azure](./media/hdinsight-apache-spark-with-kafka/spark-kafka-vnet.png)

> [!NOTE]
> Bien que Kafka proprement dit est limitée toocommunication au sein du réseau virtuel de hello, autres services sur un cluster de hello hello tels que SSH et Ambari est accessible via internet. Pour plus d’informations sur les ports publics de hello disponibles avec HDInsight, consultez [Ports et URI utilisé par HDInsight](hdinsight-hadoop-port-settings-for-services.md).

Si vous pouvez créer un réseau virtuel Azure, Kafka et Spark clusters manuellement, il est plus facile toouse un modèle Azure Resource Manager. Toodeploy un réseau virtuel Azure, Kafka, les étapes suivantes de hello utilisation et Spark clusters tooyour abonnement Azure.

1. Utilisez hello suivant toosign bouton dans tooAzure et modèle ouvert hello Bonjour portail Azure.
    
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-kafka-spark-cluster-in-vnet-v2.1.json" target="_blank"><img src="./media/hdinsight-apache-spark-with-kafka/deploy-to-azure.png" alt="Deploy tooAzure"></a>
    
    Hello modèle Azure Resource Manager se trouve dans **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-spark-cluster-in-vnet-v2.1.json**.

    > [!WARNING]
    > disponibilité tooguarantee de Kafka sur HDInsight, votre cluster doit contenir au moins trois nœuds de travail. Ce modèle crée un cluster Kafka qui contient trois nœuds Worker.

    Ce modèle crée un cluster HDInsight 3.6 pour Kafka et Spark.

2. Hello utilisation suivant des entrées d’information toopopulate hello de hello **les déploiement personnalisé** panneau :
   
    ![Déploiement HDInsight personnalisé](./media/hdinsight-apache-spark-with-kafka/parameters.png)
   
    * **Groupe de ressources** : créez un groupe de ressources ou sélectionnez-en un. Ce groupe contient un cluster HDInsight de hello.

    * **Emplacement**: sélectionnez un tooyou géographiquement fermer d’emplacement.

    * **Nom du Cluster de base**: cette valeur est utilisée comme nom de base hello pour les clusters de Spark et Kafka hello. Par exemple, si vous entrez **hdi**, cela crée un cluster Spark nommé spark-hdi__ et un cluster Kafka nommé **kafka-hdi**.

    * **Nom d’utilisateur de cluster**: nom d’utilisateur admin hello pour les clusters de Spark et Kafka hello.

    * **Mot de passe de connexion cluster**: hello mot de passe administrateur pour les clusters de Spark et Kafka hello.

    * **Nom d’utilisateur SSH**: hello toocreate d’utilisateur SSH pour les clusters de Spark et Kafka hello.

    * **Mot de passe SSH**: mot de passe de hello pour hello SSH pour les clusters de Spark et Kafka hello.

3. Hello de lecture **termes et Conditions**, puis sélectionnez **J’accepte les termes du contrat de toohello et conditions susmentionnées**.

4. Enfin, recherchez **code confidentiel toodashboard** , puis sélectionnez **bon**. Il prend environ 20 minutes toocreate les clusters hello.

Une fois que les ressources hello ont été créées, vous êtes panneau tooa redirigé hello groupe de ressources qui contient des clusters de hello et tableau de bord web.

![Panneau des ressources de groupe de réseau virtuel de hello et des clusters](./media/hdinsight-apache-spark-with-kafka/groupblade.png)

> [!IMPORTANT]
> Notez que les noms de hello des clusters HDInsight de hello sont **spark-BASENAME** et **kafka-BASENAME**, où BASENAME est nom hello toohello modèle fourni. Vous utilisez ces noms dans les étapes suivantes lors de la connexion toohello clusters.

## <a name="use-hello-notebooks"></a>Utilisez les blocs-notes hello

code Hello pour exemple hello décrite dans ce document est disponible à l’adresse [https://github.com/Azure-Samples/hdinsight-spark-scala-kafka](https://github.com/Azure-Samples/hdinsight-spark-scala-kafka).

Suivez les étapes de hello Bonjour `README.md` toocomplete de fichiers de cet exemple.

## <a name="delete-hello-cluster"></a>Supprimer le cluster de hello

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

Étant donné que les étapes de hello dans ce document vous allez créer deux clusters dans hello même groupe de ressources Azure, vous pouvez supprimer le groupe de ressources hello Bonjour portail Azure. Suppression du groupe hello supprime toutes les ressources créées en suivant ce document, hello réseau virtuel Azure et compte de stockage utilisé par les clusters de hello.

## <a name="next-steps"></a>Étapes suivantes

Dans cet exemple, vous avez appris comment toouse nouvelles tooread et tooKafka d’écriture. Utilisez des autres façons toowork hello suivant les liens toodiscover avec Kafka :

* [Prise en main d’Apache Kafka sur HDInsight](hdinsight-apache-kafka-get-started.md)
* [Utilisez MirrorMaker toocreate un réplica de Kafka sur HDInsight](hdinsight-apache-kafka-mirroring.md)
* [Utilisation d’Apache Storm avec Kafka sur HDInsight](hdinsight-apache-storm-with-kafka.md)

