---
title: "le programme d’installation d’aaaCluster pour Hadoop, Spark, Kafka, HBase ou R Server - Azure HDInsight | Documents Microsoft"
description: "Configurer des clusters Hadoop, Kafka, Spark, HBase, R Server ou Storm pour HDInsight à partir d’un navigateur, hello CLI d’Azure, Azure PowerShell, REST ou de kit de développement logiciel."
keywords: "configuration de cluster Hadoop, configuration de cluster kafka, configuration de cluster spark, définition d’un cluster dans hadoop"
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 23a01938-3fe5-4e2e-8e8b-3368e1bbe2ca
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/06/2017
ms.author: jgao
ms.openlocfilehash: 80ec59d8a39f7fccb940503fd2dc3ae5afee6bcf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-clusters-in-hdinsight-with-hadoop-spark-kafka-and-more"></a>Configurer des clusters dans HDInsight avec Hadoop, Spark, Kafka et bien plus encore

[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

Découvrez comment tooset installer et configurer des clusters dans HDInsight avec Hadoop, Spark, Kafka, Hive interactif, HBase, R Server ou Storm. En outre, découvrez comment toocustomize clusters et ajouter une sécurité en joignant tooa domaine.

Un cluster Hadoop se compose de plusieurs machines virtuelles (nœuds) utilisées pour le traitement distribué de tâches. HDInsight Azure gère les détails d’implémentation de l’installation et configuration des nœuds individuels, afin que vous ayez uniquement les informations de configuration générales tooprovide. 

> [!IMPORTANT]
>Cluster HDInsight facturation démarre une fois qu’un cluster est créé et s’arrête lorsque le cluster de hello est supprimé. La facturation est effectuée au prorata des minutes écoulées. Par conséquent, vous devez toujours supprimer votre cluster lorsqu’il n’est plus utilisé. Découvrez comment trop[supprimer un cluster.](hdinsight-delete-cluster.md)
>

## <a name="cluster-setup-methods"></a>Méthodes de configuration du cluster
Hello tableau suivant montre différentes méthodes de hello qu'utiliser tooset configuration d’un cluster HDInsight.

| Clusters créés avec | un navigateur Web | Ligne de commande | API REST | Foundation | 
| --- |:---:|:---:|:---:|:---:|
| [Portail Azure](hdinsight-hadoop-create-linux-clusters-portal.md) |✔ |&nbsp; |&nbsp; |&nbsp; |
| [Azure Data Factory](hdinsight-hadoop-create-linux-clusters-adf.md) |✔ |✔ |✔ |✔ |
| [Interface de ligne de commande Azure](hdinsight-hadoop-create-linux-clusters-azure-cli.md) |&nbsp; |✔ |&nbsp; |&nbsp; |
| [Azure PowerShell](hdinsight-hadoop-create-linux-clusters-azure-powershell.md) |&nbsp; |✔ |&nbsp; |&nbsp; |
| [cURL](hdinsight-hadoop-create-linux-clusters-curl-rest.md) |&nbsp; |✔ |✔ |&nbsp; |
| [KIT DE DÉVELOPPEMENT LOGICIEL (SDK) .NET](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md) |&nbsp; |&nbsp; |&nbsp; |✔ |
| [Modèles Microsoft Azure Resource Manager](hdinsight-hadoop-create-linux-clusters-arm-templates.md) |&nbsp; |✔ |&nbsp; |&nbsp; |

## <a name="quick-create-basic-cluster-setup"></a>Création rapide : configuration du cluster de base
Cet article vous guide à travers l’installation Bonjour [portail Azure](https://portal.azure.com), où vous pouvez créer un cluster HDInsight à l’aide *création rapide* ou *personnalisé*. 

Suivez les instructions sur l’écran de hello toodo un programme d’installation de cluster de base. Les détails sont fournis ci-dessous pour :

* [Nom de groupe ressources](#resource-group-name)
* [Types de cluster et configuration](#cluster-types) 
* [Connexion au cluster et nom d’utilisateur SSH](#cluster-login-and-ssh-username)
* [Emplacement](#location)

> [!IMPORTANT]
> Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure. Pour plus d’informations, reportez-vous à la rubrique [Déclassement de HDInsight 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).
>

## <a name="resource-group-name"></a>Nom de groupe ressources 

[Le Gestionnaire de ressources Azure](../azure-resource-manager/resource-group-overview.md) vous permet de travailler avec des ressources hello dans votre application comme une tooas de groupe, ou un groupe de ressources Azure. Vous pouvez déployer, mettre à jour, analyser ou supprimer toutes les ressources hello pour votre application en une seule opération coordonnée.

## <a name="cluster-types"></a> Types de cluster et configuration
HDInsight Azure fournit actuellement des types, chacun avec un ensemble de composants tooprovide de certaines fonctionnalités de cluster suivant de hello.

> [!IMPORTANT]
> Les clusters HDInsight sont disponibles dans différents types, chacun d’eux pour une charge de travail ou une technologie unique. Il n’a aucun toocreate méthode prise en charge un cluster qui combine plusieurs types, tels que Storm et HBase sur un seul cluster. Si votre solution nécessite des technologies qui sont réparties sur plusieurs types de cluster HDInsight, un [réseau virtuel Azure](https://docs.microsoft.com/azure/virtual-network) peut se connecter à des types de cluster hello requis. 
>
>

| Type de cluster | Fonctionnalités |
| --- | --- |
| [Hadoop](hdinsight-hadoop-introduction.md) |Requête par lot et analyse des données stockées |
| [HBase](hdinsight-hbase-overview.md) |Traitement de grandes quantités de données de NoSQL sans schéma |
| [Storm](hdinsight-storm-overview.md) |Traitement d’événements en temps réel |
| [Spark](hdinsight-apache-spark-overview.md) |Traitement en mémoire, requêtes interactives, traitement du flux de traitement micro-batch |
| [Kafka (version préliminaire)](hdinsight-apache-kafka-introduction.md) | Une plateforme de diffusion en continu distribuée qui peut être des pipelines de données de diffusion en continu en temps réel toobuild utilisés et des applications |
| [R Server](hdinsight-hadoop-r-server-overview.md) |Différentes statistiques Big Data, modélisation prédictive et fonctionnalités Machine Learning |
| [Hive interactif (version préliminaire)](hdinsight-hadoop-use-interactive-hive.md) |Mise en cache pour les requêtes Hive interactives et plus rapides |

### <a name="number-of-nodes-for-each-cluster-type"></a>Nombre de nœuds pour chaque type de cluster
Chaque type de cluster possède son propre nombre de nœuds, sa terminologie pour les nœuds et la taille de machine virtuelle par défaut. Dans le tableau suivant de hello, nombre de hello de nœuds pour chaque type de nœud figure entre parenthèses.

| Type | Nœuds | Diagramme |
| --- | --- | --- |
| Hadoop |Nœud principal (2), nœud de données (1+) |![Nœuds de cluster Hadoop HDInsight](./media/hdinsight-hadoop-provision-linux-clusters/hdinsight-hadoop-cluster-type-nodes.png) |
| HBase |Serveur principal (2), serveur de région (1+), nœud principal/ZooKeeper (3) |![Nœuds de cluster HDInsight HBase](./media/hdinsight-hadoop-provision-linux-clusters/hdinsight-hbase-cluster-type-setup.png) |
| Storm |Nœud Nimbus (2), serveur supervisor (1+), nœud ZooKeeper (3) |![Nœuds de cluster HDInsight Storm](./media/hdinsight-hadoop-provision-linux-clusters/hdinsight-storm-cluster-type-setup.png) |
| Spark |Nœud principal (2), nœud worker (1+), nœud ZooKeeper (3) (gratuits pour les machines virtuelles ZooKeeper A1) |![Nœuds de cluster HDInsight Spark](./media/hdinsight-hadoop-provision-linux-clusters/hdinsight-spark-cluster-type-setup.png) |

Pour plus d’informations, consultez [nœud les tailles de machine virtuelle et de configuration pour les clusters par défaut](hdinsight-component-versioning.md#default-node-configuration-and-virtual-machine-sizes-for-clusters) dans « Quels sont les composants Hadoop hello et les versions dans HDInsight ? »

### <a name="hdinsight-version"></a>Version de HDInsight
Choisissez la version hello de HDInsight pour ce cluster. Pour plus d’informations, voir [Versions de HDInsight prises en charge](hdinsight-component-versioning.md#supported-hdinsight-versions).

### <a name="cluster-tiers"></a>Niveau de cluster : les niveaux de service HDInsight

HDInsight Azure fournit les offres de cloud de données volumineuses hello dans deux niveaux de service : Standard et Premium.  Pour plus d’informations, consultez [HDInsight Standard et HDInsight Premium](hdinsight-component-versioning.md#hdinsight-standard-and-hdinsight-premium).

Hello capture d’écran suivante montre hello informations sur le portails Azure pour la sélection des types de cluster.

![Configuration de HDInsight Premium](./media/hdinsight-hadoop-provision-linux-clusters/hdinsight-cluster-type-configuration.png)


## <a name="cluster-login-and-ssh-user-name"></a>Connexion au cluster et nom d’utilisateur SSH
Les clusters HDInsight vous permettent de configurer deux comptes d’utilisateur lors de la création :

* Utilisateur HTTP : nom d’utilisateur par défaut hello est *admin*. Elle utilise la configuration de base hello sur hello portail Azure. Parfois, le nom par défaut est « Utilisateur du cluster ».
* L’utilisateur SSH (Linux clusters) : cluster de toohello tooconnect utilisée via SSH. Pour en savoir plus, voir [Utilisation de SSH avec Hadoop Linux sur HDInsight depuis Linux, Unix ou OS X](hdinsight-hadoop-linux-use-ssh-unix.md).

## <a name="location"></a>Emplacement (régions) pour les clusters et le stockage

Vous n’avez pas besoin emplacement du cluster toospecify hello explicitement : hello cluster est hello même emplacement que le stockage par défaut de hello. Pour obtenir la liste des régions prises en charge, cliquez sur hello **région** liste déroulante sur [tarification HDInsight](https://go.microsoft.com/fwLink/?LinkID=282635&clcid=0x409).

## <a name="storage-endpoints-for-clusters"></a>Points de terminaison de stockage pour les clusters

Bien qu’une installation locale de Hadoop utilise hello système de fichiers distribués Hadoop (HDFS) pour le stockage sur le cluster de hello, cloud que vous utilisez des points de terminaison de stockage connecté Bonjour toocluster. Les clusters HDInsight utilisent [Azure Data Lake Store](hdinsight-hadoop-use-data-lake-store.md) ou des [Blobs dans Azure Storage](hdinsight-hadoop-use-blob-storage.md). À l’aide du stockage Azure ou Data Lake Store signifie que vous pouvez supprimer sans risque les clusters HDInsight hello utilisés pour le calcul tout en conservant vos données. 

> [!WARNING]
> À l’aide d’un compte de stockage supplémentaire à un autre emplacement à partir du cluster HDInsight de hello n’est pas pris en charge.

Lors de la configuration, pour le point de terminaison de stockage hello par défaut vous spécifiez un conteneur d’objets blob d’un compte de stockage Azure ou d’un magasin Data Lake Store. Hello du stockage par défaut contient des applications et du système des journaux. Si vous le souhaitez, vous pouvez spécifier des comptes de stockage Azure liés supplémentaires et comptes Data Lake Store hello cluster peuvent accéder à. cluster HDInsight de Hello et de stockage dépendant de hello doivent être dans hello même emplacement.

![Paramètres de stockage de cluster : points de terminaison de stockage compatibles HDFS](./media/hdinsight-hadoop-provision-linux-clusters/hdinsight-cluster-creation-storage.png)

[!INCLUDE [secure-transfer-enabled-storage-account](../../includes/hdinsight-secure-transfer.md)]


### <a name="optional-metastores"></a>Metastores en option
Vous pouvez créer des metastores Hive ou Oozie en option. Toutefois, tous les types de clusters ne prennent pas les metastores et Azure SQL Data Warehouse n’est pas compatible avec les metastores. 

> [!IMPORTANT]
> N’utilisez pas lorsque vous créez un magasin de métadonnées personnalisée, des tirets, des traits d’union ou d’espaces dans le nom de base de données hello. Cela peut entraîner des toofail de processus de création de cluster hello.

### <a name="use-hiveoozie-metastore"></a>Metastore Hive

Si vous souhaitez tooretain vos tables ruche après avoir supprimé un cluster HDInsight, utilisez un magasin de métadonnées personnalisé. Vous pouvez ensuite joindre le cluster de HDInsight tooanother hello le magasin de métadonnées.

Un metastore HDInsight créé pour une version de cluster HDInsight ne peut pas être partagé entre différentes versions de cluster HDInsight. Pour obtenir la liste des versions de HDInsight, consultez la section [Versions de HDInsight prises en charge](hdinsight-component-versioning.md#supported-hdinsight-versions).

### <a name="oozie-metastore"></a>Metastore Oozie

performances tooincrease lors de l’utilisation de Oozie, utilisez un magasin de métadonnées personnalisé. Un magasin de métadonnées peut également fournir des données de la tâche accès tooOozie après la suppression de votre cluster. 

> [!IMPORTANT]
> Vous ne pouvez pas réutiliser un metastore Oozie personnalisé. toouse un magasin de métadonnées Oozie personnalisé, vous devez fournir une base de données SQL Azure vide lors de la création du cluster HDInsight de hello.

## <a name="configure-cluster-size"></a>Configurer la taille du cluster

Vous êtes facturé pour l’utilisation du nœud pour tant que cluster de hello existe. La facturation commence lorsqu’un cluster est créé et s’arrête lorsque le cluster de hello est supprimé. Les clusters ne peuvent pas être désalloués ou mis en attente.

coût de Hello des clusters HDInsight est déterminé par un nombre de nœuds et les tailles de machines virtuelles hello pour les nœuds de hello hello. 

Les différents types de clusters ont des types de nœuds, nombres de nœuds et tailles de nœuds différents :
* Type de cluster Hadoop par défaut : 
    * Deux *nœuds principaux*  
    * Quatre *nœuds de données*
* Type de cluster Storm par défaut : 
    * Deux *nœuds Nimbus*
    * Trois *nœuds ZooKeeper*
    * Quatre *nœuds superviseurs* 

Si vous essayez simplement out HDInsight, nous vous recommandons d'utiliser un nœud de données. Pour plus d'informations sur la tarification de HDInsight, consultez la rubrique [Tarification HDInsight](https://go.microsoft.com/fwLink/?LinkID=282635&clcid=0x409).

> [!NOTE]
> limite de taille de cluster Hello varie selon les abonnements Azure. Contact [support de facturation Azure](https://docs.microsoft.com/azure/azure-supportability/how-to-create-azure-support-request) limite de hello tooincrease.
>

Lorsque vous utilisez hello tooconfigure portail Azure hello cluster, taille du nœud hello est disponible via hello **niveaux de tarification de nœud** panneau. Dans le portail hello, vous pouvez également voir hello coût associé aux tailles de nœud différents hello. 

![Tailles de nœuds de machine virtuelle HDInsight](./media/hdinsight-hadoop-provision-linux-clusters/hdinsight-node-sizes.png)

### <a name="virtual-machine-sizes"></a>Tailles de machines virtuelles 
Lorsque vous déployez des clusters, choisissez les ressources de calcul basés sur la solution de hello vous envisagez de toodeploy. Hello machines virtuelles suivantes sont utilisées pour les clusters HDInsight :
* Machines virtuelles de série A et D1-4 : [tailles de machines virtuelles Linux à usage général](https://docs.microsoft.com/azure/virtual-machines/linux/sizes-general)
* Machine virtuelle de série D11-14 : [tailles de machines virtuelles Linux avec mémoire optimisée](https://docs.microsoft.com/azure/virtual-machines/linux/sizes-memory)

toofind à la valeur que vous devez utiliser toospecify une taille de machine virtuelle lors de la création d’un cluster à l’aide de hello différents kits de développement logiciel ou lorsque vous utilisez Azure PowerShell, consultez [toouse pour des clusters HDInsight des tailles de machine virtuelle](../cloud-services/cloud-services-sizes-specs.md#size-tables). À partir de cet article lié, utilisez la valeur de la hello Bonjour **taille** colonne des tables de hello.

> [!IMPORTANT]
> Si vous avez besoin de plus de 32 nœuds worker dans un cluster, vous devez sélectionner une taille de nœud principal avec au moins 8 cœurs et 14 Go de RAM.
>
>

Pour plus d’informations, consultez [Tailles des machines virtuelles](../virtual-machines/windows/sizes.md). Pour plus d’informations sur la tarification de hello de différentes tailles, consultez [tarification HDInsight](https://azure.microsoft.com/pricing/details/hdinsight).   

## <a name="custom-cluster-setup"></a>Configuration du cluster personnalisé
Builds le programme d’installation de cluster personnalisé sur hello rapide créer des paramètres et ajoute hello options suivantes :
- [Applications HDInsight](#hdinsight-applications)
- [Taille du cluster](#cluster-size)
- Paramètres avancés
  - [Actions de script](#customize-clusters-using-script-action)
  - [Réseau virtuel](#use-virtual-network)

## <a name="install-hdinsight-applications-on-clusters"></a>Installer des applications HDInsight sur des clusters

Une application HDInsight est une application que les utilisateurs peuvent installer sur un cluster HDInsight sous Linux. Vous pouvez utiliser des applications fournies par Microsoft, des tiers ou que vous développez vous-même. Pour plus d’informations, consultez [Installer des applications Hadoop tierces sur Azure HDInsight](hdinsight-apps-install-applications.md).

La plupart des applications de HDInsight hello est installée sur un nœud vide.  Un nœud vide est une machine virtuelle Linux hello mêmes outils client installé et configuré comme nœud principal de hello. Vous pouvez utiliser le nœud de périmètre hello pour accédant à hello cluster, le test de vos applications clientes et hébergement de vos applications clientes. Pour plus d’informations, consultez [Utiliser des nœuds de périmètre vides dans HDInsight](hdinsight-apps-use-edge-node.md).

## <a name="advanced-settings-script-actions"></a>Paramètres avancés : actions de script

Vous pouvez installer des composants supplémentaires ou personnaliser la configuration de cluster à l’aide de scripts lors de la création. Ces scripts sont appelées **Action de Script**, qui est une option de configuration qui peut être utilisée à partir de hello portail Azure, les applets de commande PowerShell HDInsight ou hello HDInsight .NET SDK. Pour plus d’informations, consultez la page [Personnalisation d’un cluster HDInsight à l’aide d’une d’action de script](hdinsight-hadoop-customize-cluster-linux.md).

Certains composants Java natifs, telles que Mahout et en cascade, peuvent être exécutés sur le cluster de hello en tant que fichiers d’Archive Java (JAR). Ces fichiers JAR peuvent être distribuée tooAzure stockage et soumis tooHDInsight clusters avec les mécanismes de soumission de travail Hadoop. Pour plus d’informations, consultez la rubrique [Envoi de tâches Hadoop par programme](hdinsight-submit-hadoop-jobs-programmatically.md).

> [!NOTE]
> Si vous rencontrez des problèmes de déploiement de clusters de tooHDInsight fichiers JAR ou appeler des fichiers JAR sur les clusters HDInsight, contactez [Support technique de Microsoft](https://azure.microsoft.com/support/options/).
>
> Cascading n’est pas pris en charge par HDInsight et ne peut pas bénéficier du support Microsoft. Pour les listes de composants pris en charge, consultez [quelles sont les nouveautés dans les versions de cluster hello fournies par HDInsight](hdinsight-component-versioning.md).
>
>

Vous pouvez souhaiter hello tooconfigure suivant des fichiers de configuration pendant le processus de création de hello :

* clusterIdentity.xml
* core-site.xml
* gateway.xml
* hbase-env.xml
* hbase-site.xml
* hdfs-site.xml
* hive-env.xml
* hive-site.xml
* mapred-site
* oozie-site.xml
* oozie-env.xml
* storm-site.xml
* tez-site.xml
* webhcat-site.xml
* yarn-site.xml

Pour plus d’informations, consultez [Personnalisation de clusters HDInsight à l’aide de Bootstrap](hdinsight-hadoop-customize-cluster-bootstrap.md).

## <a name="advanced-settings-extend-clusters-with-a-virtual-network"></a>Paramètres avancés : étendre des clusters avec un réseau virtuel
Si votre solution nécessite des technologies qui sont réparties sur plusieurs types de cluster HDInsight, un [réseau virtuel Azure](https://docs.microsoft.com/azure/virtual-network) peut se connecter à des types de cluster hello requis. Cette configuration autorise les clusters hello et tout code que vous déployez toothem, toodirectly communiquent entre eux.

Pour plus d’informations sur l’utilisation du réseau virtuel Azure avec HDInsight, consultez [Étendre HDInsight à l’aide de réseaux virtuels Azure](hdinsight-extend-hadoop-virtual-network.md).

Pour voir un exemple d’utilisation de deux types de cluster au sein d’un réseau virtuel Azure, consultez la section [Analyser les données de capteur avec Storm et HBase](hdinsight-storm-sensor-data-analysis.md). Pour plus d’informations sur l’utilisation de HDInsight avec un réseau virtuel, y compris la configuration spécifique requise pour le réseau virtuel de hello, consultez [HDInsight d’étendre les fonctionnalités à l’aide de réseau virtuel Azure](hdinsight-extend-hadoop-virtual-network.md).

## <a name="troubleshoot-access-control-issues"></a>Résoudre les problèmes de contrôle d’accès

Si vous rencontrez des problèmes lors de la création de clusters HDInsight, reportez-vous aux [exigences de contrôle d’accès](hdinsight-administer-use-portal-linux.md#create-clusters).

## <a name="next-steps"></a>Étapes suivantes

- [Quelles sont les clusters Hadoop HDInsight et écosystème de Hadoop hello ?](hdinsight-hadoop-introduction.md)
- [Prise en main de Hadoop dans HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md)
- [Travailler à partir d’un PC Windows dans Hadoop sur HDInsight](hdinsight-hadoop-windows-tools.md)
