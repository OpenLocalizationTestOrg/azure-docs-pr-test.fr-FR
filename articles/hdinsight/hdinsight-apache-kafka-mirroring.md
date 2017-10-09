---
title: "rubriques d’Apache Kafka aaaMirror - Azure HDInsight | Documents Microsoft"
description: "Découvrez comment la mise en miroir de Kafka toouse Apache de fonctionnalité toomaintain un réplica d’un Kafka sur le cluster HDInsight en cluster secondaire tooa de rubriques de mise en miroir."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 015d276e-f678-4f2b-9572-75553c56625b
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/13/2017
ms.author: larryfr
ms.openlocfilehash: 5ace0251d7402d4d7d9b28726e253ce7091a87ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-mirrormaker-tooreplicate-apache-kafka-topics-with-kafka-on-hdinsight-preview"></a>Utilisez les rubriques d’Apache Kafka MirrorMaker tooreplicate avec Kafka sur HDInsight (version préliminaire)

Découvrez comment toouse Apache Kafka de mise en miroir de fonctionnalité tooreplicate rubriques tooa secondaire de cluster. Mise en miroir peut être exécuté comme un processus continu, ou en tant que méthode de migration, utilisé par intermittence tooanother de données à partir d’un cluster.

Dans cet exemple, la mise en miroir est rubriques tooreplicate utilisé entre deux clusters HDInsight. Les deux clusters se trouvant dans un réseau virtuel Azure Bonjour même région.

> [!WARNING]
> Mise en miroir ne doit pas être considéré comme un moyen tooachieve une tolérance de pannes. tooitems de décalage Hello au sein d’une rubrique sont différentes entre les clusters sources et de destination de hello, pour les clients ne peuvent pas utiliser de manière interchangeable hello deux.
>
> Si vous êtes inquiet de la tolérance de panne, vous devez définir la réplication pour les rubriques hello dans votre cluster. Pour plus d’informations, consultez [Prise en main de Kafka sur HDInsight](hdinsight-apache-kafka-get-started.md).

## <a name="how-kafka-mirroring-works"></a>Fonctionne de la mise en miroir Kafka

Fonctionnement de la mise en miroir à l’aide de hello MirrorMaker outil (partie de Apache Kafka) tooconsume des enregistrements à partir des rubriques sur le cluster source de hello, puis créez une copie locale sur le cluster de destination hello. MirrorMaker utilise un (ou plusieurs) *consommateurs* lus à partir du cluster source hello et un *producteur* qui écrit du cluster de toohello local (destination).

Hello suivant schéma illustre le processus de mise en miroir hello :

![Diagramme de processus de mise en miroir de hello](./media/hdinsight-apache-kafka-mirroring/kafka-mirroring.png)

Kafka Apache sur HDInsight ne fournit pas d’accès toohello service de Kafka sur hello internet public. Les producteurs Kafka ou qu’ils doivent être Bonjour même réseau virtuel Azure en tant que nœuds hello Bonjour cluster de Kafka. Pour cet exemple, hello source de Kafka et clusters de destination se trouvent dans un réseau virtuel Azure. Hello diagramme suivant illustre le flux de communication entre les clusters hello :

![Diagramme du cluster source et du cluster de destination Kafka dans un réseau virtuel Azure](./media/hdinsight-apache-kafka-mirroring/spark-kafka-vnet.png)

les clusters sources et de destination Hello peuvent être différents dans nombre hello des nœuds et des partitions, et les décalages dans les rubriques hello diffèrent également. Mise en miroir de conserve la valeur de clé de hello qui est utilisé pour le partitionnement, afin de l’ordre d’enregistrement est conservé sur une base par clé.

### <a name="mirroring-across-network-boundaries"></a>Mise en miroir au-delà des limites réseau

Si vous devez toomirror entre Kafka des clusters sur différents réseaux, il existe des hello suivant des considérations supplémentaires :

* **Passerelles**: les réseaux hello doivent être en mesure de toocommunicate à hello au niveau du TCPIP.

* **La résolution de noms**: hello Kafka des clusters dans chaque réseau doit être en mesure de tooconnect tooeach autres à l’aide de noms d’hôte. Cette opération peut nécessiter un serveur de système DNS (Domain Name) de chaque réseau est configuré tooforward demandes toohello autres réseaux.

    Lors de la création d’un réseau virtuel Azure, au lieu d’utiliser hello qu'automatique DNS fourni avec le réseau de hello, vous devez spécifier une personnalisé DNS server hello adresse IP et de serveur de hello. Après hello que réseau virtuel a été créé, vous devez ensuite créer une Machine virtuelle Azure qui utilise cette adresse IP, puis installer et configurer le logiciel DNS sur celui-ci.

    > [!WARNING]
    > Créez et configurez un serveur DNS personnalisé hello avant d’installer HDInsight dans hello réseau virtuel. Il n’existe aucune configuration supplémentaire requise pour le serveur DNS HDInsight toouse hello sont configuré pour hello réseau virtuel.

Pour plus d’informations sur la connexion de deux réseaux virtuels Azure, consultez [Configurer une connexion de réseau virtuel à réseau virtuel](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md).

## <a name="create-kafka-clusters"></a>Création de clusters Kafka

Pendant que vous pouvez créer un réseau virtuel Azure et Kafka clusters manuellement, il est plus facile toouse un modèle Azure Resource Manager. Utilisez hello suivant les étapes toodeploy un réseau virtuel Azure et deux tooyour de clusters Kafka abonnement Azure.

1. Utilisez hello suivant toosign bouton dans tooAzure et modèle ouvert hello Bonjour portail Azure.
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json" target="_blank"><img src="./media/hdinsight-apache-kafka-mirroring/deploy-to-azure.png" alt="Deploy tooAzure"></a>
   
    Hello modèle Azure Resource Manager se trouve dans **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json**.

    > [!WARNING]
    > disponibilité tooguarantee de Kafka sur HDInsight, votre cluster doit contenir au moins trois nœuds de travail. Ce modèle crée un cluster Kafka qui contient trois nœuds Worker.

2. Hello utilisation suivant des entrées d’information toopopulate hello de hello **les déploiement personnalisé** panneau :
    
    ![Déploiement HDInsight personnalisé](./media/hdinsight-apache-kafka-mirroring/parameters.png)
    
    * **Groupe de ressources** : créez un groupe de ressources ou sélectionnez-en un. Ce groupe contient un cluster HDInsight de hello.

    * **Emplacement**: sélectionnez un tooyou géographiquement fermer d’emplacement.
     
    * **Nom du Cluster de base**: cette valeur est utilisée comme nom de base hello pour hello Kafka clusters. Par exemple, l’entrée de **hdi** crée des clusters nommés **source-hdi** et **dest-hdi**.

    * **Nom d’utilisateur de cluster**: clusters de Kafka nom d’utilisateur admin hello pour hello source et de destination.

    * **Mot de passe de connexion cluster**: les clusters Kafka hello mot de passe administrateur pour hello source et de destination.

    * **Nom d’utilisateur SSH**: les clusters Kafka hello SSH utilisateur toocreate pour hello source et de destination.

    * **Mot de passe SSH**: clusters de Kafka de mot de passe de hello pour hello SSH pour hello source et de destination.

3. Hello de lecture **termes et Conditions**, puis sélectionnez **J’accepte les termes du contrat de toohello et conditions susmentionnées**.

4. Enfin, recherchez **code confidentiel toodashboard** , puis sélectionnez **bon**. Il prend environ 20 minutes toocreate les clusters hello.

Une fois que les ressources hello ont été créées, vous êtes panneau tooa redirigé hello groupe de ressources qui contient des clusters de hello et tableau de bord web.

![Panneau des ressources de groupe de réseau virtuel de hello et des clusters](./media/hdinsight-apache-kafka-mirroring/groupblade.png)

> [!IMPORTANT]
> Notez que les noms de hello des clusters HDInsight de hello sont **source-BASENAME** et **dest-BASENAME**, où BASENAME est nom hello toohello modèle fourni. Vous utilisez ces noms dans les étapes suivantes lors de la connexion toohello clusters.

## <a name="create-topics"></a>Création de sujets

1. Se connecter toohello **source** cluster à l’aide de SSH :

    ```bash
    ssh sshuser@source-BASENAME-ssh.azurehdinsight.net
    ```

    Remplacez **sshuser** avec nom d’utilisateur SSH hello utilisé lors de la création du cluster de hello. Remplacez **BASENAME** par nom de base hello utilisé lors de la création du cluster de hello.

    Pour en savoir plus, voir [Utilisation de SSH avec HDInsight (Hadoop) depuis Bash (l’interpréteur de commande) sur Windows 10, Linux, Unix ou OS X](hdinsight-hadoop-linux-use-ssh-unix.md).

2. Suivant de hello utilisez commandes toofind hello soigneur ordinateurs hôtes pour du cluster source hello :

    ```bash
    # Install jq if it is not installed
    sudo apt -y install jq
    # get hello zookeeper hosts for hello source cluster
    export SOURCE_ZKHOSTS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/ZOOKEEPER/components/ZOOKEEPER_SERVER | jq -r '["\(.host_components[].HostRoles.host_name):2181"] | join(",")' | cut -d',' -f1,2`
    
    Replace `$PASSWORD` with hello password for hello cluster.

    Replace `$CLUSTERNAME` with hello name of hello source cluster.

3. toocreate a topic named `testtopic`, use hello following command:

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --create --replication-factor 2 --partitions 8 --topic testtopic --zookeeper $SOURCE_ZKHOSTS
    ```

3. Hello utilisation suivant tooverify de commande qui hello rubrique a été créé :

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --list --zookeeper $SOURCE_ZKHOSTS
    ```

    réponse de Hello contient `testtopic`.

4. Hello utilisation suivant tooview hello soigneur informations sur l’hôte pour ce (hello **source**) cluster :

    ```bash
    echo $SOURCE_ZKHOSTS
    ```

    Cet exemple renvoie toohello similaire à informations suivant le texte :

    `zk0-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:2181,zk1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:2181`

    Enregistrez ces informations. Il est utilisé dans la section suivante de hello.

## <a name="configure-mirroring"></a>Configuration de la mise en miroir

1. Se connecter toohello **destination** cluster à l’aide d’une autre session SSH :

    ```bash
    ssh sshuser@dest-BASENAME-ssh.azurehdinsight.net
    ```

    Remplacez **sshuser** avec nom d’utilisateur SSH hello utilisé lors de la création du cluster de hello. Remplacez **BASENAME** par nom de base hello utilisé lors de la création du cluster de hello.

    Pour en savoir plus, voir [Utilisation de SSH avec HDInsight (Hadoop) depuis Bash (l’interpréteur de commande) sur Windows 10, Linux, Unix ou OS X](hdinsight-hadoop-linux-use-ssh-unix.md).

2. Suivant de hello utilisez commande toocreate un `consumer.properties` décrivant comment toocommunicate avec hello **source** cluster :

    ```bash
    nano consumer.properties
    ```

    Hello utilisation après le texte en tant que contenu hello Hello `consumer.properties` fichier :

    ```yaml
    zookeeper.connect=SOURCE_ZKHOSTS
    group.id=mirrorgroup
    ```

    Remplacez **SOURCE_ZKHOSTS** avec hello soigneur héberge les informations à partir de hello **source** cluster.

    Ce fichier décrit hello consommateur informations toouse lors de la lecture à partir de la source de hello cluster de Kafka. Pour plus d’informations sur la configuration du consommateur, consultez [Consumer Configs](https://kafka.apache.org/documentation#consumerconfigs) (Configurations de consommateur) sur kafka.apache.org.

    fichier de hello toosave, utilisez **Ctrl + X**, **Y**, puis **entrée**.

3. Avant de configurer le producteur hello qui communique avec le cluster de destination hello, vous devez trouver hello broker hôtes pour hello **destination** cluster. Utilisez hello suivant de commandes tooretrieve ces informations :

    ```bash
    sudo apt -y install jq
    DEST_BROKERHOSTS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/KAFKA/components/KAFKA_BROKER | jq -r '["\(.host_components[].HostRoles.host_name):9092"] | join(",")' | cut -d',' -f1,2`
    echo $DEST_BROKERHOSTS
    ```

    Remplacez `$PASSWORD` avec le mot de passe du compte (administrateur) hello connexion pour le cluster de hello.

    Remplacez `$CLUSTERNAME` par nom de hello du cluster de destination hello.

    Ces commandes retournent des informations similaires toohello qui suivent :

        wn0-dest.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn1-dest.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092

4. Hello utilisation suivant toocreate un `producer.properties` décrivant comment toocommunicate avec hello **destination** cluster :

    ```bash
    nano producer.properties
    ```

    Hello utilisation après le texte en tant que contenu hello Hello `producer.properties` fichier :

    ```yaml
    bootstrap.servers=DEST_BROKERS
    compression.type=none
    ```

    Remplacez **DEST_BROKERS** avec les informations de service broker hello à partir de l’étape précédente de hello.

    Pour plus d’informations sur la configuration du producteur, consultez [Producer Configs](https://kafka.apache.org/documentation#producerconfigs) (Configurations de producteur) sur kafka.apache.org.

## <a name="start-mirrormaker"></a>Lancement de MirrorMaker

1. À partir de hello SSH connexion toohello **destination** de cluster, utilisez hello suivant commande toostart hello MirrorMaker processus :

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-run-class.sh kafka.tools.MirrorMaker --consumer.config consumer.properties --producer.config producer.properties --whitelist testtopic --num.streams 4
    ```

    paramètres Hello utilisés dans cet exemple sont :

    * **--consumer.config**: Spécifie le fichier hello qui contient les propriétés de consommateur. Ces propriétés sont utilisée toocreate un consommateur qui lit à partir de hello *source* cluster de Kafka.

    * **--producer.config**: Spécifie le fichier hello qui contient les propriétés de producteur. Ces propriétés sont utilisée toocreate un producteur qui écrit toohello *destination* cluster de Kafka.

    * **liste blanche--**: une liste de rubriques MirrorMaker réplique de hello source cluster toohello de destination.

    * **--num.streams**: hello nombre de toocreate de threads de consommateur.

 Au démarrage, MirrorMaker retourne toohello similaire à informations suivant le texte :

    ```json
    {metadata.broker.list=wn1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn0-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092, request.timeout.ms=30000, client.id=mirror-group-3, security.protocol=PLAINTEXT}{metadata.broker.list=wn1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn0-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092, request.timeout.ms=30000, client.id=mirror-group-0, security.protocol=PLAINTEXT}
    metadata.broker.list=wn1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn0-kafka.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092, request.timeout.ms=30000, client.id=mirror-group-2, security.protocol=PLAINTEXT}
    metadata.broker.list=wn1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn0-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092, request.timeout.ms=30000, client.id=mirror-group-1, security.protocol=PLAINTEXT}
    ```

2. À partir de hello SSH connexion toohello **source** de cluster, utilisez hello suivant commande toostart un producteur et rubrique toohello de messages d’envoi :

    ```bash
    SOURCE_BROKERHOSTS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/KAFKA/components/KAFKA_BROKER | jq -r '["\(.host_components[].HostRoles.host_name):9092"] | join(",")' | cut -d',' -f1,2`
    /usr/hdp/current/kafka-broker/bin/kafka-console-producer.sh --broker-list $SOURCE_BROKERHOSTS --topic testtopic
    ```

    Remplacez `$PASSWORD` avec un mot de passe de connexion (admin) pour le cluster source de hello hello.

    Remplacez `$CLUSTERNAME` par nom de hello du cluster de source de hello.

     Lorsque vous arrivez sur une ligne vide avec un curseur, tapez quelques messages texte. Ceux-ci sont envoyés toohello rubrique sur hello **source** cluster. Lorsque vous avez terminé, utilisez **Ctrl + C** processus de producteur tooend hello.

3. À partir de hello SSH connexion toohello **destination** de cluster, utilisez **Ctrl + C** tooend hello MirrorMaker processus. Puis suit de hello utilisez commandes tooverify que hello `testtopic` rubrique a été créée, et que les données de la rubrique de hello a été répliquée toothis miroir :

    ```bash
    DEST_ZKHOSTS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/ZOOKEEPER/components/ZOOKEEPER_SERVER | jq -r '["\(.host_components[].HostRoles.host_name):2181"] | join(",")' | cut -d',' -f1,2`
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --list --zookeeper $DEST_ZKHOSTS
    /usr/hdp/current/kafka-broker/bin/kafka-console-consumer.sh --zookeeper $DEST_ZKHOSTS --topic testtopic --from-beginning
    ```

    Remplacez `$PASSWORD` avec un mot de passe de connexion (admin) pour le cluster de destination hello hello.

    Remplacez `$CLUSTERNAME` par nom de hello du cluster de destination hello.

    Hello la liste des rubriques inclut désormais `testtopic`, qui est créé lorsque MirrorMaster reflète rubrique hello hello source cluster toohello de destination. messages Hello récupérées à partir de la rubrique de hello sont hello entré sur le cluster de hello source identique.

## <a name="delete-hello-cluster"></a>Supprimer le cluster de hello

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

Étant donné que les étapes de hello dans ce document vous allez créer deux clusters dans hello même groupe de ressources Azure, vous pouvez supprimer le groupe de ressources hello Bonjour portail Azure. Groupe de ressources hello suppression supprime toutes les ressources créées en suivant ce document, hello réseau virtuel Azure et compte de stockage utilisé par les clusters de hello.

## <a name="next-steps"></a>Étapes suivantes

Dans ce document, vous avez appris comment toouse MirrorMaker toocreate un réplica d’un Kafka cluster. Utilisez des autres façons toowork hello suivant les liens toodiscover avec Kafka :

* [Documentation d’Apache Kafka MirrorMaker](https://cwiki.apache.org/confluence/pages/viewpage.action?pageId=27846330) sur cwiki.apache.org.
* [Prise en main d’Apache Kafka sur HDInsight](hdinsight-apache-kafka-get-started.md)
* [Use Apache Spark with Kafka on HDInsight](hdinsight-apache-spark-with-kafka.md) (Utilisation d’Apache Spark avec Kafka sur HDInsight)
* [Utilisation d’Apache Storm avec Kafka sur HDInsight](hdinsight-apache-storm-with-kafka.md)
* [Se connecter tooKafka via un réseau virtuel Azure](hdinsight-apache-kafka-connect-vpn-gateway.md)
