---
title: Utiliser une diffusion en continu Apache Spark avec Kafka - Azure HDInsight | Documents Microsoft
description: "Découvrez comment utiliser Apache Spark pour diffuser des données vers ou depuis Apache Kafka à l’aide de DStreams. Dans cet exemple, vous diffusez des données à l’aide d’un bloc-notes Jupyter à partir de Spark sur HDInsight."
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
ms.openlocfilehash: 81fa319f6fb94bdabacd8f68d14b9a1063a9749a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="apache-spark-streaming-dstream-example-with-kafka-preview-on-hdinsight"></a>Exemple Apache Spark Streaming (DStream) avec Kafka (aperçu) sur HDInsight

Découvrez comment utiliser Apache Spark pour diffuser des données vers ou depuis Apache Kafka à l’aide de DStreams. Cet exemple utilise un bloc-notes jupyter qui s’exécute sur le cluster Spark.
> [!NOTE]
> Les étapes décrites dans ce document créent un groupe de ressources Azure qui contient à la fois un Spark sur HDInsight et un Kafka sur un cluster HDInsight. Ces clusters sont tous deux situés dans un réseau virtuel Azure, ce qui permet au cluster Spark de communiquer directement avec le cluster Kafka.
>
> Lorsque vous avez terminé les étapes décrites dans ce document, n’oubliez pas de supprimer les clusters pour éviter les frais supplémentaires.

## <a name="create-the-clusters"></a>Création des clusters

Apache Kafka sur HDInsight ne donne pas accès aux répartiteurs Kafka via l’internet public. Tout ce qui communique avec Kafka doit se trouver sur le même réseau virtuel Azure que les nœuds du cluster Kafka. Pour cet exemple, les clusters Kafka et Spark sont situés dans un réseau virtuel Azure. Le diagramme suivant illustre le flux de communication entre les clusters :

![Diagramme des clusters Spark et Kafka dans un réseau virtuel Azure](./media/hdinsight-apache-spark-with-kafka/spark-kafka-vnet.png)

> [!NOTE]
> Bien que Kafka soit lui-même limité à la communication au sein du réseau virtuel, d’autres services sur le cluster comme SSH et Ambari sont accessibles sur Internet. Pour plus d’informations sur les ports publics disponibles avec HDInsight, consultez [Ports et URI utilisés par HDInsight](hdinsight-hadoop-port-settings-for-services.md).

Même si vous pouvez créer un réseau virtuel Azure, et des clusters Kafka et Spark manuellement, il est plus facile d’utiliser un modèle Azure Resource Manager. Utilisez les étapes suivantes pour déployer un réseau virtuel Azure et des clusters Kafka et Spark sur votre abonnement Azure.

1. Utilisez le bouton suivant pour vous connecter à Azure et ouvrir le modèle dans le portail Azure.
    
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-kafka-spark-cluster-in-vnet-v2.1.json" target="_blank"><img src="./media/hdinsight-apache-spark-with-kafka/deploy-to-azure.png" alt="Deploy to Azure"></a>
    
    Le modèle Azure Resource Manager se trouve à l’adresse **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-spark-cluster-in-vnet-v2.1.json**.

    > [!WARNING]
    > Pour garantir la disponibilité de Kafka sur HDInsight, votre cluster doit contenir au moins trois nœuds Worker. Ce modèle crée un cluster Kafka qui contient trois nœuds de travail.

    Ce modèle crée un cluster HDInsight 3.6 pour Kafka et Spark.

2. Utilisez les informations suivantes pour remplir les entrées sur le panneau **déploiement personnalisé** :
   
    ![Déploiement HDInsight personnalisé](./media/hdinsight-apache-spark-with-kafka/parameters.png)
   
    * **Groupe de ressources** : créez un groupe de ressources ou sélectionnez-en un. Ce groupe contient le cluster HDInsight.

    * **Emplacement** : choisissez un emplacement proche de vous géographiquement.

    * **Nom de cluster de base** : cette valeur sera utilisée comme nom de base pour les clusters Spark et Kafka. Par exemple, si vous entrez **hdi**, cela crée un cluster Spark nommé spark-hdi__ et un cluster Kafka nommé **kafka-hdi**.

    * **Nom d’utilisateur du cluster** : nom utilisateur Admin pour les clusters Spark et Kafka.

    * **Mot de passe du cluster** : mot de passe utilisateur Admin pour les clusters Spark et Kafka.

    * **Nom d’utilisateur SSH** : utilisateur SSH permettant de créer des clusters Spark et Kafka.

    * **Mot de passe SSH** : mot de passe de l’utilisateur SSH pour les clusters Spark et Kafka.

3. Passez en revue les **termes et conditions**, puis cochez la case **J’accepte les termes et conditions mentionnés ci-dessus**.

4. Pour finir, cochez **Épingler au tableau de bord**, puis sélectionnez **Acheter**. La création des clusters prend environ 20 minutes.

Une fois les ressources créées, vous êtes redirigé vers un panneau pour le groupe de ressources contenant les clusters et le tableau de bord Web.

![Volet du groupe de ressources pour les clusters et le réseau virtuel](./media/hdinsight-apache-spark-with-kafka/groupblade.png)

> [!IMPORTANT]
> Les noms des clusters HDInsight sont **spark-BASENAME** et **kafka-BASENAME**, où BASENAME est le nom que vous avez fourni pour le modèle. Vous utilisez ces noms dans les étapes ultérieures, lors de la connexion aux clusters.

## <a name="use-the-notebooks"></a>Obtenir les blocs-notes

Le code de l’exemple décrit dans ce document est disponible à l’adresse [https://github.com/Azure-Samples/hdinsight-spark-scala-kafka](https://github.com/Azure-Samples/hdinsight-spark-scala-kafka).

Suivez les étapes du fichier `README.md` pour terminer cet exemple.

## <a name="delete-the-cluster"></a>Suppression du cluster

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

Étant donné que les étapes décrites dans ce document créent deux clusters dans le même groupe de ressources Azure, vous pouvez supprimer le groupe de ressources du portail Azure. La suppression de ce groupe supprime toutes les ressources créées par la suite dans ce document, le réseau virtuel Azure et le compte de stockage utilisé par les clusters.

## <a name="next-steps"></a>Étapes suivantes

Dans ce document, vous avez appris à utiliser Spark pour lire et écrire dans Kafka. Utilisez les liens suivants pour découvrir d’autres façons de travailler avec Kafka :

* [Prise en main d’Apache Kafka sur HDInsight](hdinsight-apache-kafka-get-started.md)
* [Utilisation de MirrorMaker pour créer un réplica de Kafka sur HDInsight](hdinsight-apache-kafka-mirroring.md)
* [Utilisation d’Apache Storm avec Kafka sur HDInsight](hdinsight-apache-storm-with-kafka.md)

