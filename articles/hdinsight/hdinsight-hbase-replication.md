---
title: "réplication de cluster HBase aaaConfigure dans les réseaux virtuels - Azure | Documents Microsoft"
description: "Découvrez comment tooconfigure HBase la réplication pour l’équilibrage de charge, une haute disponibilité, sans interruption de service migration/mise à jour un tooanother de version HDInsight et la récupération d’urgence."
services: hdinsight,virtual-network
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: ba1c44f26b7cbf4a7a88159b12b3e064ea9f9a20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hbase-cluster-replication-within-virtual-networks"></a>Configurer la réplication de cluster HBase dans les réseaux virtuels

Découvrez comment tooconfigure HBase réplication dans un réseau virtuel (VNet) ou entre deux réseaux virtuels.

La réplication en cluster utilise une méthodologie par émission de données source. Un cluster HBase peut être une source, une destination ou jouer les deux rôles à la fois. La réplication est asynchrone et objectif hello de réplication est cohérence éventuelle. Lors de la source de hello reçoit une famille de colonne tooa Edition avec la réplication est activée, cette modification est propagé tooall les clusters de destination. Lorsque les données sont répliquées à partir d’un cluster tooanother, du cluster source hello et tous les clusters qui ont sollicité déjà les données de salutation sont suivies tooprevent les boucles de réplication.

Dans ce didacticiel, vous allez configurer une réplication source-destination. Pour d'autres topologies de cluster, consultez le [Guide de référence d'Apache HBase](http://hbase.apache.org/book.html#_cluster_replication).

Cas d’utilisation de la réplication HBase pour un seul réseau virtuel :

* L’équilibrage de charge--par exemple, en cours d’exécution des analyses ou des tâches MapReduce sur le cluster de destination hello et la réception de données sur le cluster source de hello
* Haute disponibilité
* Migration des données à partir d’un tooanother de cluster HBase
* La mise à niveau d’un cluster Azure HDInsight à partir d’une version tooanother

Cas d’utilisation de la réplication HBase pour deux réseaux virtuels :

* Récupération d'urgence
* L’équilibrage de charge et de partitionnement application hello
* Haute disponibilité

Vous répliquez des clusters à l’aide de scripts [d’action de script](hdinsight-hadoop-customize-cluster-linux.md) disponibles dans [GitHub](https://github.com/Azure/hbase-utils/tree/master/replication).

## <a name="prerequisites"></a>Composants requis
Avant de commencer ce didacticiel, vous devez disposer d’un abonnement Azure. Consultez la rubrique [Obtenir une version d'évaluation gratuite d'Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).

## <a name="configure-hello-environments"></a>Configurez des environnements de hello

Il existe trois options de configuration :

- Deux clusters HBase dans un réseau virtuel Azure
- Deux clusters HBase dans deux réseaux virtuels différents dans hello même région
- Deux clusters HBase dans deux réseaux virtuels différents dans deux régions distinctes (géoréplication)

toomake il les environnements hello tooconfigure plus faciles, nous avons créé certains [modèles Azure Resource Manager](../azure-resource-manager/resource-group-overview.md). Si vous préférez les environnements hello tooconfigure par d’autres méthodes, consultez :

- [Création de clusters Hadoop basés sur Linux dans HDInsight](hdinsight-hadoop-provision-linux-clusters.md)
- [Création de clusters HBase dans un réseau virtuel Azure](hdinsight-hbase-provision-vnet.md)

### <a name="configure-one-virtual-network"></a>Configurer un réseau virtuel

Cliquez sur hello suivant image toocreate deux HBase clusters Bonjour même réseau virtuel. modèle de Hello est stocké dans [modèles de démarrage rapide Azure](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-replication-one-vnet/).

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-hbase-replication-one-vnet%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hbase-replication/deploy-to-azure.png" alt="Deploy tooAzure"></a>

### <a name="configure-two-virtual-networks-in-hello-same-region"></a>Configurer deux réseaux virtuels Bonjour même région

Cliquez sur Suivant image toocreate deux réseaux virtuels avec deux clusters HBase Bonjour et de réseau virtuel d’homologation de hello même région. modèle de Hello est stocké dans [modèles de démarrage rapide Azure](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-replication-two-vnets-same-region/).

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-hbase-replication-two-vnets-same-region%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hbase-replication/deploy-to-azure.png" alt="Deploy tooAzure"></a>



Ce scénario nécessite [l’homologation de réseaux virtuels](../virtual-network/virtual-network-peering-overview.md). modèle de Hello permet d’homologation de réseau virtuel.   

HBase la réplication utilise des adresses IP de hello soigneur VMs. Vous devez configurer des adresses IP statiques pour les nœuds de HBase soigneur destination hello.

**tooconfigure des adresses IP statiques**

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com).
2. Dans le menu de gauche hello, cliquez sur **groupes de ressources**.
3. Cliquez sur votre groupe de ressources qui contient le cluster HBase de destination hello. Il s’agit de groupe de ressources hello que vous avez spécifié lorsque vous avez utilisé l’environnement de hello toocreate hello Gestionnaire de ressources du modèle. Vous pouvez utiliser toonarrow de filtre hello déroulant hello. Vous pouvez voir une liste de ressources qui contient les réseaux virtuels deux hello.
4. Cliquez sur le réseau virtuel hello qui contient le cluster HBase de destination hello. Par exemple, cliquez sur **xxxx-vnet2**. Vous pouvez voir trois appareils avec des noms qui commencent par **nic-zookeepermode-**. Ces appareils sont des machines virtuelles de hello trois soigneur.
5. Cliquez sur une de hello soigneur VMs.
6. Cliquez sur **Configurations IP**.
7. Cliquez sur **ipConfig1** à partir de la liste de hello.
8. Cliquez sur **statique**et notez les adresses IP réelles hello. Vous devez adresse hello lors de l’exécution de la réplication de tooenable hello script action.

  ![Adresse IP statique ZooKeeper de réplication HDInsight HBase](./media/hdinsight-hbase-replication/hdinsight-hbase-replication-zookeeper-static-ip.png)

9. Répétez l’étape 6 tooset hello adresse IP pour hello deux autres nœuds soigneur.

Pour le scénario de réseau virtuel entre hello, vous devez utiliser hello **- ip** commutateur lors de l’appel hello **hdi_enable_replication.sh** action de script.

### <a name="configure-two-virtual-networks-in-two-different-regions"></a>Configurer deux réseaux virtuels dans deux régions différentes

Cliquez sur hello suivant image toocreate deux réseaux virtuels dans les deux régions différentes. modèle de Hello est stocké dans un conteneur d’objets Blob Azure publique.

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Fhbaseha%2Fdeploy-hbase-geo-replication.json" target="_blank"><img src="./media/hdinsight-hbase-replication/deploy-to-azure.png" alt="Deploy tooAzure"></a>

Créer une passerelle VPN entre les réseaux virtuels deux hello. Pour savoir comment faire, consultez [Création d’un réseau virtuel avec une connexion de site à site à l’aide du portail Azure](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md).

HBase la réplication utilise des adresses IP de hello soigneur VMs. Vous devez configurer des adresses IP statiques pour les nœuds de HBase soigneur destination hello. tooconfigure l’adresse IP statique, consultez hello « configurer deux des réseaux virtuels dans hello même région » section dans cet article.

Pour le scénario de réseau virtuel entre hello, vous devez utiliser hello **- ip** commutateur lors de l’appel hello **hdi_enable_replication.sh** action de script.

## <a name="load-test-data"></a>Charger les données de test

Lorsque vous répliquez un cluster, vous devez spécifier hello tables tooreplicate. Dans cette section, vous allez charger des données dans un cluster de source de hello. Dans la section suivante de hello, vous devez activer la réplication entre deux clusters de hello.

Suivez les instructions de hello dans [HBase didacticiel : prise en main Apache HBase avec basés sur Linux de Hadoop dans HDInsight](hdinsight-hbase-tutorial-get-started-linux.md) toocreate un **Contacts** de table et d’insérer des données dans la table de hello.

## <a name="enable-replication"></a>Activer la réplication

Hello suit montrent comment toocall hello script d’action de script à partir de hello portail Azure. Pour exécuter une action de script à l’aide d’Azure PowerShell et hello Azure interface de ligne de commande (CLI), consultez [HDInsight de basés sur Linux de personnaliser des clusters à l’aide d’action de script](hdinsight-hadoop-customize-cluster-linux.md).

**réplication HBase tooenable hello portail Azure**

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com).
2. Cluster de HBase hello Open source.
3. Dans le menu de cluster hello, cliquez sur **Actions de Script**.
4. Cliquez sur **soumettre de nouvelles** de haut hello du Panneau de hello.
5. Sélectionnez ou entrez hello informations suivantes :

  - **Nom** : saisissez **Activer la réplication**.
  - **Bash Script URL (URL de script bash)** : saisissez **https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_enable_replication.sh**.
  - **Principal** : Sélectionné. Bonjour clairement des autres types de nœuds.
  - **Paramètres**: suivante de hello exemples de paramètres activer la réplication pour toutes les tables existantes hello et copier toutes les données hello du cluster de destination toohello hello source cluster :

            -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password> -copydata

6. Cliquez sur **Créer**. script de Hello peut prendre un certain temps, en particulier lorsque l’argument de - copydata hello est utilisé.

Arguments requis :

|Nom|Description|
|----|-----------|
|-s, --src-cluster | Spécifiez le nom DNS de hello du cluster de HBase hello source. Par exemple : -s hbsrccluster, --src-cluster=hbsrccluster |
|-d, --dst-cluster | Spécifiez le nom DNS de hello de destination de hello (réplica) cluster HBase. Par exemple : -s dsthbcluster, --src-cluster=dsthbcluster |
|-sp, --src-ambari-password | Spécifiez un mot de passe administrateur hello pour Ambari sur un cluster HBase de source hello. |
|-dp, --dst-ambari-password | Spécifiez un mot de passe administrateur hello pour Ambari sur un cluster HBase de destination hello.|

Arguments facultatifs :

|Nom|Description|
|----|-----------|
|-su, --src-ambari-user | Spécifiez le nom d’utilisateur de hello admin pour Ambari sur un cluster HBase de source hello. la valeur par défaut Hello est **admin**. |
|-du, --dst-ambari-user | Spécifiez le nom d’utilisateur de hello admin pour Ambari sur un cluster HBase de destination hello. la valeur par défaut Hello est **admin**. |
|-t, --table-list | Spécifiez hello toobe de tables répliquée. Par exemple : --table-list="table1;table2;table3". Si vous ne spécifiez pas de tables, toutes les tables HBase existantes sont répliquées.|
|-m, --machine | Spécifiez le nœud principal de hello où l’action de script hello s’exécutera. valeur de Hello est hn1 ou hn0. La valeur hn0 étant généralement plus utilisée, nous vous recommandons de choisir hn1. Vous utilisez cette option lorsque vous exécutez le script de hello $0 comme une action de script à partir de portail de HDInsight hello ou Azure PowerShell.|
|-ip | Cet argument est obligatoire lorsque vous activez la réplication entre deux réseaux virtuels. Cet argument agit comme un commutateur toouse hello IPs de soigneur des nœuds statiques à partir de clusters de réplica au lieu des noms de domaine complets. Hello statique des adresses IP doivent toobe préconfiguré avant d’activer la réplication. |
|-cp, -copydata | Activez hello la migration des données existantes sur les tables hello où la réplication est activée. |
|-rpm, -replicate-phoenix-meta | Activez la réplication sur les tables système Phoenix. <br><br>*Utilisez cette option avec précaution.* Nous vous recommandons de recréer des tables Phoenix sur les clusters de réplica avant d’utiliser ce script. |
|-h, --help | Affichez des informations sur l’utilisation. |

Hello section print_usage() Hello [script](https://github.com/Azure/hbase-utils/blob/master/replication/hdi_enable_replication.sh) fournit une explication détaillée des paramètres.

Une fois l’action de script hello correctement déployé, vous pouvez utiliser SSH tooconnect toohello destination HBase cluster et vérifiez que les données de salutation ont été répliquées.

### <a name="replication-scenarios"></a>Scénarios de réplication

Hello liste suivante montre certains cas d’utilisation générales et leurs paramètres :

- **Activer la réplication sur toutes les tables entre les clusters hello deux**. Ce scénario ne nécessite pas de copie de hello/migration de données sur les tables de hello, et il n’utilise pas de tables de Phoenix. Utilisez hello paramètres suivants :

        -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password>  

- **Activer la réplication sur des tables spécifiques**. Utilisez hello suivant la réplication tooenable paramètres table1, table2 et table3 :

        -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password> -t "table1;table2;table3"

- **Activer la réplication sur des tables spécifiques et copier les données existantes hello**. Utilisez hello suivant la réplication tooenable paramètres table1, table2 et table3 :

        -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password> -t "table1;table2;table3" -copydata

- **Activer la réplication sur toutes les tables avec la réplication phoenix métadonnées à partir de la source toodestination**. La réplication des métadonnées Phoenix n’est pas parfaite et doit être utilisée avec précaution.

        -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password> -t "table1;table2;table3" -replicate-phoenix-meta

## <a name="copy-and-migrate-data"></a>Copier et migrer des données

Il existe deux scripts d’action de script distincts pour copier/migrer des données une fois la réplication activée :

- [Script pour les petites tables](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_copy_table.sh) (copie globale et taille de quelques gigaoctets est toofinish attendu dans moins d’une heure)

- [Script pour les tables volumineuses](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/nohup_hdi_copy_table.sh) (attendu tootake supérieure à une heure toocopy)

Vous pouvez suivre hello même procédure dans [activer la réplication](#enable-replication) action de script toocall hello avec hello paramètres suivants :

    -m hn1 -t <table1:start_timestamp:end_timestamp;table2:start_timestamp:end_timestamp;...> -p <replication_peer> [-everythingTillNow]

Hello section print_usage() Hello [script](https://github.com/Azure/hbase-utils/blob/master/replication/hdi_copy_table.sh) fournit une description détaillée des paramètres.

### <a name="scenarios"></a>Scénarios

- **Copier des tables spécifiques (test1, test2 et test3) pour toutes les lignes modifiées jusqu’à présent (horodatage actuel)** :

        -m hn1 -t "test1::;test2::;test3::" -p "zk5-hbrpl2;zk1-hbrpl2;zk5-hbrpl2:2181:/hbase-unsecure" -everythingTillNow
  ou

        -m hn1 -t "test1::;test2::;test3::" --replication-peer="zk5-hbrpl2;zk1-hbrpl2;zk5-hbrpl2:2181:/hbase-unsecure" -everythingTillNow


- **Copier des tables spécifiques avec une plage horaire spécifiée** :

        -m hn1 -t "table1:0:452256397;table2:14141444:452256397" -p "zk5-hbrpl2;zk1-hbrpl2;zk5-hbrpl2:2181:/hbase-unsecure"


## <a name="disable-replication"></a>Désactiver la réplication

toodisable la réplication, vous utilisez un autre script d’action de script situé [GitHub](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_disable_replication.sh). Vous pouvez suivre hello même procédure dans [activer la réplication](#enable-replication) action de script toocall hello avec hello paramètres suivants :

    -m hn1 -s <source cluster DNS name> -sp <source cluster Ambari Password> <-all|-t "table1;table2;...">  

Hello section print_usage() Hello [script](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_disable_replication.sh) fournit une explication détaillée des paramètres.

### <a name="scenarios"></a>Scénarios

- **Désactiver la réplication sur toutes les tables** :

        -m hn1 -s <source cluster DNS name> -sp Mypassword\!789 -all
  ou

        --src-cluster=<source cluster DNS name> --dst-cluster=<destination cluster DNS name> --src-ambari-user=<source cluster Ambari username> --src-ambari-password=<source cluster Ambari password>

- **Désactiver la réplication sur les tables spécifiées (table1, table2 et table3)** :

        -m hn1 -s <source cluster DNS name> -sp <source cluster Ambari password> -t "table1;table2;table3"

## <a name="next-steps"></a>Étapes suivantes

Dans ce didacticiel, vous avez appris comment tooconfigure HBase la réplication entre deux centres de données. toolearn en savoir plus sur HDInsight et HBase, consultez :

* [Didacticiel HBase : prise en main de HBase avec Hadoop dans HDInsight Linux][hdinsight-hbase-get-started]
* [Présentation de HBase dans HDInsight : une base de données NoSQL fournissant des fonctionnalités similaires à BigTable pour Hadoop][hdinsight-hbase-overview]
* [Création de clusters HBase dans un réseau virtuel Azure][hdinsight-hbase-provision-vnet]
* [Analyse de sentiments Twitter en temps réel avec HBase dans HDInsight][hdinsight-hbase-twitter-sentiment]
* [Analyse des données de capteur avec Storm et HBase dans HDInsight (Hadoop)][hdinsight-sensor-data]

[hdinsight-hbase-geo-replication-vnet]: hdinsight-hbase-geo-replication-configure-vnets.md
[hdinsight-hbase-geo-replication-dns]: ../hdinsight-hbase-geo-replication-configure-VNet.md


[img-vnet-diagram]: ./media/hdinsight-hbase-geo-replication/HDInsight.HBase.Replication.Network.diagram.png

[powershell-install]: /powershell/azureps-cmdlets-docs
[hdinsight-hbase-get-started]: hdinsight-hbase-tutorial-get-started-linux.md
[hdinsight-manage-portal]: hdinsight-administer-use-management-portal.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-hbase-twitter-sentiment]: hdinsight-hbase-analyze-twitter-sentiment.md
[hdinsight-sensor-data]: hdinsight-storm-sensor-data-analysis.md
[hdinsight-hbase-overview]: hdinsight-hbase-overview.md
[hdinsight-hbase-provision-vnet]: hdinsight-hbase-provision-vnet.md
