---
title: "disponibilité aaaHigh de Hadoop - Azure HDInsight | Documents Microsoft"
description: "Découvrez comment les clusters HDInsight améliorent la fiabilité et la disponibilité en utilisant un nœud principal supplémentaire. Apprenez comment cela a un impact sur les services Hadoop tels que Ambari et Hive, ainsi que comment tooindividually connecter tooeach de nœud principal à l’aide de SSH."
services: hdinsight
editor: cgronlun
manager: jhubbard
author: Blackmist
documentationcenter: 
tags: azure-portal
keywords: "haute disponibilité hadoop"
ms.assetid: 99c9f59c-cf6b-4529-99d1-bf060435e8d4
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 07/28/2017
ms.author: larryfr
ms.openlocfilehash: 9ff62afe6b63b241cb984225233157219f8d7411
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="availability-and-reliability-of-hadoop-clusters-in-hdinsight"></a>Disponibilité et fiabilité des clusters Hadoop dans HDInsight

Clusters HDInsight fournissent deux disponibilité de nœuds principaux tooincrease hello et la fiabilité des services Hadoop et des travaux en cours d’exécution.

Hadoop garantit de hauts niveaux de disponibilité et de fiabilité en répliquant des services et données sur plusieurs nœuds d’un cluster. Toutefois, les distributions standard de Hadoop ne comportent généralement qu’un seul nœud principal. Toute coupure de courant de nœud principal de hello unique peut entraîner l’utilisation de toostop hello cluster. HDInsight fournit la disponibilité et la fiabilité de Hadoop deux headnodes tooimprove.

> [!IMPORTANT]
> Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure. Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

## <a name="availability-and-reliability-of-nodes"></a>Disponibilité et fiabilité des nœuds

Les nœuds d’un cluster HDInsight sont implémentés à l’aide de machines virtuelles Azure. Hello sections suivantes abordent les types de nœud individuel hello utilisés avec HDInsight. 

> [!NOTE]
> Les types de nœuds utilisables varient selon le type de cluster concerné. Par exemple, un type de cluster Hadoop ne comporte aucun nœud Nimbus. Pour plus d’informations sur les nœuds utilisés par les types de cluster HDInsight, consultez la section de types de Cluster de hello Hello [Hadoop basé sur Linux de créer des clusters dans HDInsight](hdinsight-hadoop-provision-linux-clusters.md#cluster-types) document.

### <a name="head-nodes"></a>Nœuds principaux

tooensure haute disponibilité des services Hadoop, HDInsight fournit deux nœuds principaux. Les deux nœuds principaux sont actifs et en cours d’exécution dans le cluster HDInsight de hello simultanément. Certains services, par exemple HDFS et YARN, ne sont « actifs » que sur un seul nœud principal à un instant t. Autres services tels que HiveServer2 ou le magasin de métadonnées Hive sont actifs sur les deux nœuds principal hello même temps.

Les nœuds principaux (et autres nœuds dans HDInsight) ont une valeur numérique en tant que partie du nom d’hôte hello du nœud de hello. Par exemple, `hn0-CLUSTERNAME` ou `hn4-CLUSTERNAME`.

> [!IMPORTANT]
> N’associez pas de valeur numérique de hello indique si un nœud est principal ou secondaire. valeur numérique de Hello est uniquement présent tooprovide un nom unique pour chaque nœud.

### <a name="nimbus-nodes"></a>Nœuds Nimbus

Des nœuds Nimbus sont disponibles avec les clusters Storm. nœuds de Nimbus Hello fournissent toohello fonctionnalités similaires Hadoop JobTracker par la distribution et le traitement d’analyse sur les nœuds de travail. HDInsight fournit deux nœuds Nimbus pour les clusters Storm

### <a name="zookeeper-nodes"></a>Nœuds Zookeeper

Des nœuds [ZooKeeper](http://zookeeper.apache.org/) sont utilisés pour l’élection de leader des services maîtres sur nœuds principaux. Ils sont également utilisé tooinsure que les services, les nœuds de données (traitement) et les passerelles connaissent le nœud principal, un service principal est actif sur. Par défaut, HDInsight fournit trois nœuds ZooKeeper.

### <a name="worker-nodes"></a>Nœuds de travail

Nœuds de travail effectuent une analyse de données réelles hello lorsqu’une tâche est soumis toohello cluster. Si un nœud de travail échoue, la tâche hello elle effectuait est nœud de travail tooanother soumis. Par défaut, HDInsight crée quatre nœuds de travail. Vous pouvez modifier ce nombre toosuit à vos besoins pendant et après la création du cluster.

### <a name="edge-node"></a>Nœud de périmètre

Un nœud ne participe pas activement à dans l’analyse des données au sein du cluster de hello. Il est utilisé par les développeurs ou chercheurs de données qui travaillent avec Hadoop. qualité de vie du nœud Hello edge dans hello même réseau virtuel Azure comme hello autres nœuds de cluster de hello et peut accéder directement à tous les autres nœuds. nœud de bord de Hello peut être utilisé sans mettre les ressources en s’éloignant de services Hadoop critiques ou des tâches d’analyse.

Actuellement, le serveur R HDInsight est hello seul cluster type qui fournit un nœud par défaut. Pour R Server sur HDInsight, nœud de périmètre hello est utilisé code de test R localement sur le nœud hello avant de le soumettre cluster toohello pour le traitement distribué.

Pour plus d’informations sur l’utilisation d’un nœud avec les types de clusters autre que R Server, consultez hello [utiliser noeuds dans HDInsight](hdinsight-apps-use-edge-node.md) document.

## <a name="accessing-hello-nodes"></a>L’accès aux nœuds de hello

Cluster d’accès toohello sur hello internet est fournie via une passerelle publique. L’accès est limité tooconnecting nœuds principaux de toohello et (si elle existe) hello nœud de périmètre. Tooservices d’accès en cours d’exécution sur les nœuds principal hello n’est pas concerné en demandant à plusieurs nœuds principal. Hello passerelle publique itinéraires demandes toohello nœud principal qui héberge hello le service demandé. Par exemple, si Ambari est actuellement hébergé sur le nœud principal de hello secondaire, la passerelle de hello route les demandes entrantes pour le nœud de toothat Ambari.

L’accès via la passerelle de public hello est limitée tooport 443 (HTTPS), 22 et 23.

* Port __443__ est utilisé tooaccess Ambari et autres web l’interface utilisateur ou des API REST hébergée sur les nœuds principaux hello.

* Port __22__ est le nœud principal de tooaccess utilisé hello principal ou un nœud de bord avec SSH.

* Port __23__ est utilisé tooaccess hello secondaire nœud principal avec SSH. Par exemple, `ssh username@mycluster-ssh.azurehdinsight.net` se connecte toohello principal nœud de tête hello cluster nommé **mycluster**.

Pour plus d’informations sur l’utilisation de SSH, consultez hello [utilisation de SSH avec HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.

### <a name="internal-fully-qualified-domain-names-fqdn"></a>Noms de domaine pleinement qualifiés internes (FQDN)

Nœuds dans un cluster HDInsight ont une adresse IP et le nom de domaine complet qui est accessible à partir du cluster de hello interne. Lors de l’accès aux services sur le cluster hello à l’aide de hello interne nom de domaine complet ou l’adresse IP, vous devez utiliser Ambari tooverify hello IP ou nom de domaine complet toouse lorsque vous accédez hello service.

Par exemple, hello Oozie service peut s’exécuter uniquement sur un seul nœud principal et à l’aide de hello `oozie` commande à partir d’une session SSH requiert le service de toohello URL hello. Cette URL peut être récupérée à partir de Ambari à l’aide de hello de commande suivante :

    curl -u admin:PASSWORD "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/configurations?type=oozie-site&tag=TOPOLOGY_RESOLVED" | grep oozie.base.url

Cette commande retourne un toohello similaire valeur suivant la commande, qui contient les toouse URL interne hello avec hello `oozie` commande :

    "oozie.base.url": "http://hn0-CLUSTERNAME-randomcharacters.cx.internal.cloudapp.net:11000/oozie"

Pour plus d’informations sur l’utilisation des API REST de Ambari de hello, consultez [surveiller et gérer HDInsight, à l’aide de hello API REST de Ambari](hdinsight-hadoop-manage-ambari-rest-api.md).

### <a name="accessing-other-node-types"></a>Accès à d’autres types de nœuds

Vous pouvez vous connecter toonodes pas directement accessibles sur hello internet à l’aide des méthodes suivantes de hello :

* **SSH**: une fois connecté tooa du nœud principal à l’aide de SSH, vous pouvez ensuite utiliser SSH à partir des nœuds de tooother tooconnect hello du nœud principal dans le cluster de hello. Pour plus d’informations, consultez hello [utilisation de SSH avec HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.

* **Tunnel SSH**: Si vous avez besoin de tooaccess un service web hébergé sur un des nœuds hello qui n’est pas exposée toohello internet, vous devez utiliser un tunnel SSH. Pour plus d’informations, consultez hello [utiliser un tunnel SSH avec HDInsight](hdinsight-linux-ambari-ssh-tunnel.md) document.

* **Réseau virtuel Azure**: Si votre HDInsight cluster fait partie d’un réseau virtuel Azure, n’importe quelle ressource sur hello même réseau virtuel peut accéder directement à tous les nœuds de cluster de hello. Pour plus d’informations, consultez hello [HDInsight étendre à l’aide du réseau virtuel Azure](hdinsight-extend-hadoop-virtual-network.md) document.

## <a name="how-toocheck-on-a-service-status"></a>Comment toocheck sur un état de service

état de hello toocheck des services qui s’exécutent sur les nœuds principaux hello, utilisez hello Ambari Web UI ou hello Ambari REST API.

### <a name="ambari-web-ui"></a>Interface utilisateur web d'Ambari

Hello l’interface utilisateur de Ambari Web est visible à https://CLUSTERNAME.azurehdinsight.net. Remplacez **CLUSTERNAME** avec nom hello de votre cluster. Si vous y êtes invité, entrez les informations d’identification des utilisateurs HTTP hello pour votre cluster. nom d’utilisateur HTTP Hello par défaut est **admin** et hello est hello de mot de passe saisis lors de la création du cluster de hello.

Lorsque vous arrivez sur la page de confirmation d’Ambari hello, services de hello installé sont répertoriés sur la gauche hello de page de hello.

![Services installés](./media/hdinsight-high-availability-linux/services.png)

Il existe une série d’icônes qui peuvent s’afficher l’état tooindicate de service suivante tooa. Toutes les alertes liées tooa peut être affiché à l’aide hello **alertes** lien en hello haut hello. Vous pouvez sélectionner chaque tooview service plus d’informations sur ce dernier.

Lors de la page du service hello fournit des informations sur l’état de hello et la configuration de chaque service, il ne fournit pas les informations sur lequel service hello de nœud principal est en cours d’exécution sur. tooview cette plus d’informations, l’utilisation hello **hôtes** lien en hello haut hello. Cette page affiche les ordinateurs hôtes au sein du cluster hello, y compris les nœuds principal hello.

![liste des hôtes](./media/hdinsight-high-availability-linux/hosts.png)

En sélectionnant hello lien de l’un des nœuds de tête hello affiche hello composants services et en cours d’exécution sur ce nœud.

![État du composant](./media/hdinsight-high-availability-linux/nodeservices.png)

Pour plus d’informations sur l’utilisation de Ambari, consultez [analyse et de gérer HDInsight à l’aide de hello l’interface utilisateur de Ambari Web](hdinsight-hadoop-manage-ambari.md).

### <a name="ambari-rest-api"></a>API Ambari REST

Hello Ambari REST API est disponible via hello internet. passerelle de Hello HDInsight publique gère routage demandes toohello nœud principal qui héberge actuellement hello API REST.

Vous pouvez utiliser hello suivant l’état d’un service via l’API REST de Ambari de hello hello de toocheck la commande :

    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/SERVICENAME?fields=ServiceInfo/state

* Remplacez **mot de passe** avec le mot de passe utilisateur (admin) hello HTTP.
* Remplacez **CLUSTERNAME** avec nom hello du cluster de hello.
* Remplacez **SERVICENAME** avec nom hello du service de hello vous souhaitez que l’état de hello de toocheck de.

Par exemple, les état hello toocheck Hello **HDFS** service sur un cluster nommé **mycluster**, avec un mot de passe **mot de passe**, vous utiliseriez hello de commande suivante :

    curl -u admin:password https://mycluster.azurehdinsight.net/api/v1/clusters/mycluster/services/HDFS?fields=ServiceInfo/state

réponse de Hello est similaire toohello suivant JSON :

    {
      "href" : "http://hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:8080/api/v1/clusters/mycluster/services/HDFS?fields=ServiceInfo/state",
      "ServiceInfo" : {
        "cluster_name" : "mycluster",
        "service_name" : "HDFS",
        "state" : "STARTED"
      }
    }

Hello URL indique que le service de hello est en cours d’exécution sur un nœud principal nommé **hn0-CLUSTERNAME**.

Hello état indique que le service de hello est en cours d’exécution, ou **démarré**.

Si vous ne connaissez pas les services sont installés sur le cluster de hello, vous pouvez utiliser hello suivant commande tooretrieve une liste :

    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services

Pour plus d’informations sur l’utilisation des API REST de Ambari de hello, consultez [surveiller et gérer HDInsight, à l’aide de hello API REST de Ambari](hdinsight-hadoop-manage-ambari-rest-api.md).

#### <a name="service-components"></a>Composants du service

Services peuvent contenir des composants que vous souhaitez état hello toocheck individuellement. Par exemple, HDFS contient hello NameNode. tooview plus d’informations sur un composant, commande hello serait :

    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/SERVICE/components/component

Si vous ne connaissez pas les composants sont fournis par un service, vous pouvez utiliser hello suivant commande tooretrieve une liste :

    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/SERVICE/components/component

## <a name="how-tooaccess-log-files-on-hello-head-nodes"></a>Comment tooaccess fichiers journaux sur les nœuds principaux hello

### <a name="ssh"></a>SSH

Lors de nœud principal de tooa connecté via SSH, les fichiers journaux se trouve dans **/var/log**. Par exemple, **/var/log/hadoop-yarn/yarn** contiennent les journaux correspondant à YARN.

Chaque nœud principal peut avoir des entrées de journal unique, vérifiez donc hello se connecte à la fois.

### <a name="sftp"></a>SFTP

Vous pouvez également connecter toohello de nœud principal à l’aide de hello SSH File Transfer Protocol ou sécuriser fichier SFTP (Transfer Protocol) et le télécharger directement les fichiers journaux de hello.

Toousing similaire lors de la connexion de cluster toohello vous devez fournir un client SSH hello SSH utilisateur compte nom et hello SSH l’adresse du cluster de hello. Par exemple, `sftp username@mycluster-ssh.azurehdinsight.net`. Fournir le mot de passe de hello compte hello lorsque vous y êtes invité, ou fournissez une clé publique à l’aide de hello `-i` paramètre.

Une fois connecté, vous voyez apparaître une invite `sftp>` . À partir de cette invite, vous pouvez changer de répertoire, ainsi que charger et télécharger des fichiers. Par exemple, hello suivant les commandes modifier les répertoires toohello **/var/log/hadoop/hdfs** active, puis téléchargez de tous les fichiers dans le répertoire de hello.

    cd /var/log/hadoop/hdfs
    get *

Pour obtenir la liste des commandes disponibles, entrez `help` à hello `sftp>` invite.

> [!NOTE]
> Il existe également des interfaces graphiques qui vous permettent de système de fichiers toovisualize hello lorsqu’il est connecté à l’aide de SFTP. Par exemple, [MobaXTerm](http://mobaxterm.mobatek.net/) vous permet de système de fichiers toobrowse hello à l’aide d’un Explorateur de tooWindows similaire interface.

### <a name="ambari"></a>Ambari

> [!NOTE]
> tooaccess journaux à l’aide de Ambari, vous devez utiliser un tunnel SSH. des interfaces web Hello pour les services individuels hello ne sont pas exposées publiquement sur Internet de hello. Pour plus d’informations sur l’utilisation d’un tunnel SSH, consultez hello [utiliser SSH Tunneling](hdinsight-linux-ambari-ssh-tunnel.md) document.

À partir de l’interface utilisateur de Ambari Web de hello, sélectionnez service hello vous souhaitez tooview journaux (par exemple, des fils). Utilisez ensuite **liens rapides** tooselect les journaux pour le hello tooview de nœud principal.

![À l’aide rapide lie tooview journaux](./media/hdinsight-high-availability-linux/viewlogs.png)

## <a name="how-tooconfigure-hello-node-size"></a>Comment tooconfigure hello taille du nœud

taille de Hello d’un nœud peut être sélectionné uniquement lors de la création du cluster. Vous trouverez une liste de hello différentes tailles de machine virtuelle disponibles pour HDInsight sur hello [HDInsight page de tarification](https://azure.microsoft.com/pricing/details/hdinsight/).

Lorsque vous créez un cluster, vous pouvez spécifier la taille hello de nœuds de hello. Hello ci-après fournit des conseils sur la façon dont la taille de hello toospecify à l’aide hello [portail Azure][preview-portal], [Azure PowerShell][azure-powershell], et hello [CLI d’Azure][azure-cli]:

* **Portail Azure**: lorsque vous créez un cluster, vous pouvez définir la taille hello de nœuds hello utilisé par hello cluster :

    ![Image de l'Assistant de création de cluster avec sélection de taille de nœud](./media/hdinsight-high-availability-linux/headnodesize.png)

* **CLI Azure**: lors de l’utilisation de hello `azure hdinsight cluster create` de commande, vous pouvez définir la taille de hello de tête de hello, de traitement et les nœuds soigneur à l’aide de hello `--headNodeSize`, `--workerNodeSize`, et `--zookeeperNodeSize` paramètres.

* **Azure PowerShell**: lors de l’utilisation de hello `New-AzureRmHDInsightCluster` applet de commande, vous pouvez définir taille hello de tête de hello, de traitement et les nœuds soigneur à l’aide de hello `-HeadNodeVMSize`, `-WorkerNodeSize`, et `-ZookeeperNodeSize` paramètres.

## <a name="next-steps"></a>Étapes suivantes

Utilisez hello suivant toolearn des liens plus sur les éléments mentionnés dans ce document.

* [Référence REST Ambari](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md)
* [Installer et configurer hello CLI d’Azure](../cli-install-nodejs.md)
* [Installation et configuration d'Azure PowerShell](/powershell/azure/overview)
* [Gestion de HDInsight à l'aide d'Ambari](hdinsight-hadoop-manage-ambari.md)
* [Approvisionnement de clusters HDInsight sous Linux](hdinsight-hadoop-provision-linux-clusters.md)

[preview-portal]: https://portal.azure.com/
[azure-powershell]: /powershell/azureps-cmdlets-docs
[azure-cli]: ../cli-install-nodejs.md
