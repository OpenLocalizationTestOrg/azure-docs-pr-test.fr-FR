---
title: "les clusters de Hadoop aaaCreate à l’aide de la ligne de commande - hello Azure HDInsight | Documents Microsoft"
description: "Découvrez comment les clusters HDInsight toocreate à l’aide de hello multiplateforme Azure CLI 1.0."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 50b01483-455c-4d87-b754-2229005a8ab9
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/26/2017
ms.author: larryfr
ms.openlocfilehash: 5295b01054b8c23df0e3b75a3e0e8c933ac48b3c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-hdinsight-clusters-using-hello-azure-cli"></a>Créer des clusters HDInsight à l’aide de hello CLI d’Azure

[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

les étapes dans cette procédure pas à pas document Création d’un cluster HDInsight 3.5 à l’aide de hello Azure CLI 1.0 Hello.

> [!IMPORTANT]
> Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure. Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).


## <a name="prerequisites"></a>Composants requis

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

* **Un abonnement Azure**. Consultez la page [Obtention d’un essai gratuit d’Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).

* **Interface de ligne de commande Azure**. étapes Hello dans ce document ont été testés dernière avec version 0.10.14 CLI d’Azure.

    > [!IMPORTANT]
    > étapes de Hello dans ce document ne fonctionnent pas avec Azure CLI 2.0. Azure CLI 2.0 ne prend pas en charge la création d’un cluster HDInsight.

## <a name="log-in-tooyour-azure-subscription"></a>Ouvrez une session dans tooyour abonnement Azure

Suivez les étapes de hello documentées dans [connecter tooan abonnement Azure à partir de hello Azure Interface de ligne (Azure)](../xplat-cli-connect.md) et connecter abonnement tooyour à l’aide de hello **connexion** (méthode).

## <a name="create-a-cluster"></a>Créer un cluster

Hello suit doit être effectuée à partir d’une ligne de commande, tels que PowerShell ou Bash.

1. Utilisez hello suivant commande tooauthenticate tooyour abonnement Azure :

        azure login

    Vous est demandée tooprovide votre nom et le mot de passe. Si vous avez plusieurs abonnements Azure, utilisez `azure account set <subscriptionname>` abonnement hello tooset hello CLI d’Azure commandes utilisent.

2. Basculez en mode de gestionnaire de ressources tooAzure à l’aide de hello commande suivante :

        azure config mode arm

3. Créez un groupe de ressources. Ce groupe de ressources contient le cluster HDInsight de hello et compte de stockage associé.

        azure group create groupname location

    * Remplacez `groupname` avec un nom unique pour le groupe de hello.

    * Remplacez `location` par région géographique hello que toocreate hello groupe dans.

       Pour obtenir la liste des emplacements valides, utilisez hello `azure location list` de commandes et utilisez un des emplacements hello de hello `Name` colonne.

4. Créez un compte de stockage. Ce compte de stockage est utilisé comme espace de stockage par défaut hello pour le cluster HDInsight de hello.

        azure storage account create -g groupname --sku-name RAGRS -l location --kind Storage storagename

    * Remplacez `groupname` par nom de hello du groupe de hello créé à l’étape précédente de hello.

    * Remplacez `location` par hello même emplacement utilisé à l’étape précédente de hello.

    * Remplacez `storagename` avec un nom unique pour le compte de stockage hello.

        > [!NOTE]
        > Pour plus d’informations sur les paramètres de hello utilisé dans cette commande, utilisez `azure storage account create -h` aide tooview pour cette commande.

5. Récupérer le compte de stockage hello hello clé tooaccess utilisé.

        azure storage account keys list -g groupname storagename

    * Remplacez `groupname` avec le nom de groupe de ressources hello.
    * Remplacez `storagename` par nom hello hello du compte de stockage.

     Dans les données hello qui sont retournées, enregistrer hello `key` valeur `key1`.

6. Créez un cluster HDInsight.

        azure hdinsight cluster create -g groupname -l location -y Linux --clusterType Hadoop --defaultStorageAccountName storagename.blob.core.windows.net --defaultStorageAccountKey storagekey --defaultStorageContainer clustername --workerNodeCount 3 --userName admin --password httppassword --sshUserName sshuser --sshPassword sshuserpassword clustername

    * Remplacez `groupname` avec le nom de groupe de ressources hello.

    * Remplacez `Hadoop` avec le type de cluster hello que vous souhaitez toocreate. Par exemple, `Hadoop`, `HBase`, `Kafka`, `Spark` ou `Storm`.

     > [!IMPORTANT]
     > HDInsight clusters sont disponibles dans différents types, qui correspondent toohello la charge de travail ou la technologie qui hello cluster est réglée pour. Il n’a aucun toocreate méthode prise en charge un cluster qui combine plusieurs types, tels que Storm et HBase sur un seul cluster.

    * Remplacez `location` par hello même emplacement utilisé dans les étapes précédentes.

    * Remplacez `storagename` par le nom de compte de stockage hello.

    * Remplacez `storagekey` avec clé hello obtenu à l’étape précédente de hello.

    * Pourquoi `--defaultStorageContainer` paramètre, hello utilisez même nom que celui que vous utilisez pour le cluster de hello.

    * Remplacez `admin` et `httppassword` avec le nom de hello et le mot de passe vous souhaitez toouse lors de l’accès de cluster de hello via HTTPS.

    * Remplacez `sshuser` et `sshuserpassword` avec le nom d’utilisateur hello et le mot de passe vous souhaitez toouse lors de l’accès cluster hello à l’aide de SSH

    > [!IMPORTANT]
    > Cet exemple crée un cluster avec deux nœuds de travail. Vous pouvez également modifier le nombre de hello de nœuds worker après la création du cluster en effectuant des opérations de mise à l’échelle. Si vous envisagez d’utiliser plus de 32 nœuds worker, vous devez sélectionner une taille de nœud principal avec au moins 8 cœurs et 14 Go de RAM. Vous pouvez définir la taille du nœud principal hello à l’aide de hello `--headNodeSize` paramètre lors de la création du cluster.
    >
    > Pour plus d’informations sur les tailles de nœud et les coûts associés, consultez [Tarification HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/).

    Il peut prendre plusieurs minutes pour toofinish de processus de création de cluster hello. En règle générale, il dure environ 15 minutes.

## <a name="troubleshoot"></a>Résolution des problèmes

Si vous rencontrez des problèmes lors de la création de clusters HDInsight, reportez-vous aux [exigences de contrôle d’accès](hdinsight-administer-use-portal-linux.md#create-clusters).

## <a name="next-steps"></a>Étapes suivantes

Maintenant que vous avez créé un cluster HDInsight à l’aide de hello CLI d’Azure, utilisez hello suivant toolearn comment toowork avec votre cluster :

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
