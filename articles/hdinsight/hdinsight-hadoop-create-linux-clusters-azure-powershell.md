---
title: "aaaCreate Hadoop clusters à l’aide de PowerShell - Azure HDInsight | Documents Microsoft"
description: "Découvrez comment toocreate Hadoop, HBase, tempête ou Spark des clusters à l’aide d’Azure PowerShell sur Linux pour HDInsight."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 4208deca-d64a-45e1-8948-2673d5d7678c
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 53afe4702f6b61a0720ceda48a4a34d7fa8797d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-linux-based-clusters-in-hdinsight-using-azure-powershell"></a>Créer des clusters basés sur Linux dans HDInsight à l’aide d’Azure PowerShell

[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

Azure PowerShell est un environnement de script puissant que vous pouvez utiliser toocontrol et automatiser le déploiement de hello et la gestion de vos charges de travail dans Microsoft Azure. Ce document fournit des informations sur comment toocreate un HDInsight basés sur Linux cluster à l’aide de Azure PowerShell. Il inclut également un exemple de script.

> [!NOTE]
> Azure PowerShell est uniquement disponible sur les clients Windows. Si vous utilisez un client Mac OS X, Unix ou Linux, consultez [créer un cluster HDInsight de basés sur Linux à l’aide d’Azure CLI](hdinsight-hadoop-create-linux-clusters-azure-cli.md) pour plus d’informations sur l’utilisation de hello CLI d’Azure toocreate un cluster.

## <a name="prerequisites"></a>Composants requis
Vous devez disposer de hello avant de commencer cette procédure :

* Un abonnement Azure. Consultez la page [Obtention d’un essai gratuit d’Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* [Azure PowerShell](/powershell/azure/install-azurerm-ps)

    > [!IMPORTANT]
    > La prise en charge de la gestion des ressources HDInsight par Azure PowerShell à l’aide d’Azure Service Manager est **déconseillée** ; elle a été supprimée le 1er janvier 2017. étapes de Hello dans ce document Utilisez hello nouvelles applets de commande HDInsight qui fonctionnent avec Azure Resource Manager.
    >
    > Suivez les étapes de hello dans [installez Azure PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) tooinstall hello dernière version d’Azure PowerShell. Si vous avez des scripts qui toobe besoin modifié toouse hello nouvelles applets de commande qui fonctionnent avec Azure Resource Manager, consultez [des outils de migration tooAzure développement basé sur le Gestionnaire de ressources pour les clusters HDInsight](hdinsight-hadoop-development-using-azure-resource-manager.md) pour plus d’informations.

## <a name="create-cluster"></a>Créer un cluster

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

toocreate un cluster HDInsight à l’aide d’Azure PowerShell, vous devez effectuer hello procédures suivantes :

* Création d’un groupe de ressources Azure
* Création d'un compte Azure Storage
* Création d'un conteneur d'objets blob Azure
* Création d'un cluster HDInsight

Hello de script suivant montre comment toocreate un nouveau cluster :

[!code-powershell[main](../../powershell_scripts/hdinsight/create-cluster/create-cluster.ps1?range=5-71)]

valeurs Hello que vous spécifiez pour la connexion de cluster hello sont utilisées toocreate hello Hadoop compte d’utilisateur pour le cluster de hello. Utilisez cette tooservices tooconnect de compte hébergé sur le cluster de hello, comme des interfaces utilisateur ou des API REST de web.

valeurs Hello que vous spécifiez pour l’utilisateur SSH hello sont utilisateur SSH hello toocreate utilisé pour le cluster de hello. Utilisez ce compte toostart une session SSH à distance sur le cluster de hello et exécuter des tâches. Pour plus d’informations, consultez hello [utilisation de SSH avec HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.

> [!IMPORTANT]
> Si vous envisagez de toouse plus de 32 nœuds de travail (lors de la création du cluster ou en hello mise à l’échelle du cluster après la création), vous devez également spécifier une taille de nœud principal avec au moins 8 cœurs et 14 Go de RAM.
>
> Pour plus d’informations sur les tailles de nœud et les coûts associés, consultez [Tarification HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/).

Peut prendre jusqu'à too20 minutes toocreate un cluster.

## <a name="create-cluster-configuration-object"></a>Création de cluster : objet de configuration

Vous pouvez également créer un objet de configuration HDInsight à l’aide de l’applet de commande `New-AzureRmHDInsightClusterConfig`. Vous pouvez ensuite modifier cette configuration objet tooenable autres options de configuration de votre cluster. Enfin, utilisez hello `-Config` paramètre Hello `New-AzureRmHDInsightCluster` configuration de hello toouse applet de commande.

Hello script suivant crée un tooconfigure d’objet de configuration serveur R sur le type de cluster HDInsight. Hello configuration permet un nœud, RStudio et un compte de stockage supplémentaires.

[!code-powershell[main](../../powershell_scripts/hdinsight/create-cluster/create-cluster-with-config.ps1?range=59-98)]

> [!WARNING]
> À l’aide d’un compte de stockage dans un emplacement autre que le cluster HDInsight de hello n’est pas pris en charge. Lorsque vous utilisez cet exemple, créer un compte de stockage supplémentaire hello Bonjour même emplacement que le serveur de hello.

## <a name="customize-clusters"></a>Personnalisation des clusters

* Consultez [Personnalisation de clusters HDInsight à l’aide de Bootstrap](hdinsight-hadoop-customize-cluster-bootstrap.md#use-azure-powershell).
* Consultez [Personnalisation de clusters HDInsight à l’aide d’une action de script](hdinsight-hadoop-customize-cluster-linux.md).

## <a name="delete-hello-cluster"></a>Supprimer le cluster de hello

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="troubleshoot"></a>Résolution des problèmes

Si vous rencontrez des problèmes lors de la création de clusters HDInsight, reportez-vous aux [exigences de contrôle d’accès](hdinsight-administer-use-portal-linux.md#create-clusters).

## <a name="next-steps"></a>Étapes suivantes

Maintenant que vous avez créé un cluster HDInsight, utilisez hello suivant comment les ressources toolearn toowork avec votre cluster.

### <a name="hadoop-clusters"></a>Clusters Hadoop

* [Utilisation de Hive avec HDInsight](hdinsight-use-hive.md)
* [Utilisation de Pig avec HDInsight](hdinsight-use-pig.md)
* [Utilisation de MapReduce avec HDInsight](hdinsight-use-mapreduce.md)

### <a name="hbase-clusters"></a>Clusters HBase

* [Prise en main de HBase sur HDInsight](hdinsight-hbase-tutorial-get-started-linux.md)
* [Développement d’applications Java pour HBase sur HDInsight](hdinsight-hbase-build-java-maven-linux.md)

### <a name="storm-clusters"></a>Clusters Storm

* [Développement de topologies Java pour Storm sur HDInsight](hdinsight-storm-develop-java-topology.md)
* [Utilisation de composants Python dans Storm sur HDInsight](hdinsight-storm-develop-python-topology.md)
* [Déploiement et analyse des topologies avec Storm sur HDInsight](hdinsight-storm-deploy-monitor-topology-linux.md)

### <a name="spark-clusters"></a>Clusters Spark

* [Créer une application autonome avec Scala](hdinsight-apache-spark-create-standalone-application.md)
* [Exécution de travaux à distance avec Livy sur un cluster Spark](hdinsight-apache-spark-livy-rest-interface.md)
* [Spark avec BI : effectuez une analyse interactive des données à l’aide de Spark dans HDInsight avec des outils BI](hdinsight-apache-spark-use-bi-tools.md)
* [Spark avec Machine Learning : Spark utilisation dans résultats de l’inspection alimentaires toopredict HDInsight](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Streaming Spark : Utiliser Spark dans HDInsight pour créer des applications de diffusion en continu en temps réel](hdinsight-apache-spark-eventhub-streaming.md)

