---
title: aaaUse Kafka Apache avec Storm sur HDInsight - Azure | Documents Microsoft
description: "Apache Kafka est installé avec Apache Storm sur HDInsight. Découvrez comment toowrite tooKafka, puis lisez à partir de celui-ci, à l’aide de hello KafkaBolt et KafkaSpout des composants fournis avec Storm. Également apprendre comment toouse hello Flux framework toodefine et soumettre des topologies de Storm."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: e4941329-1580-4cd8-b82e-a2258802c1a7
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/21/2017
ms.author: larryfr
ms.openlocfilehash: 95701f51dfdf6f1a859dcde96d7053df4f21701f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-apache-kafka-preview-with-storm-on-hdinsight"></a>Utilisation d’Apache Kafka (version préliminaire) avec Storm sur HDInsight

Découvrez comment tooread d’Apache Storm toouse à partir d’et d’écriture tooApache Kafka. Cet exemple montre également comment toosave des données à partir d’un toohello de topologie Storm compatible HDFS fichier système utilisé par HDInsight.

> [!NOTE]
> étapes Hello dans ce document créent un groupe de ressources Azure qui contient à la fois une tempête sur HDInsight et un Kafka sur le cluster HDInsight. Ces clusters sont situés dans un réseau virtuel Azure, ce qui permet de hello Storm cluster toodirectly communiquent avec hello cluster de Kafka.
> 
> Lorsque vous avez terminé les étapes hello dans ce document, n’oubliez pas de frais supplémentaires de toodelete hello clusters tooavoid.

## <a name="get-hello-code"></a>Obtenir le code de hello

code Hello pour exemple hello utilisé dans ce document est disponible à l’adresse [https://github.com/Azure-Samples/hdinsight-storm-java-kafka](https://github.com/Azure-Samples/hdinsight-storm-java-kafka).

toocompile ce projet, vous devez hello configuration pour votre environnement de développement suivante :

* [Java JDK 1.8](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) ou version ultérieure. HDInsight 3.5 ou les versions ultérieures requièrent Java 8.

* [Maven 3.x](https://maven.apache.org/download.cgi)

* Un client SSH (vous devez hello `ssh` et `scp` commandes) - pour plus d’informations, consultez [utilisation de SSH avec HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

* Un éditeur de texte ou IDE.

Hello variables d’environnement suivantes peuvent être définis lors de l’installation de Java et hello JDK sur votre station de travail de développement. Toutefois, vous devez vérifier qu’ils existent et qu’ils contiennent des valeurs correctes de hello pour votre système.

* `JAVA_HOME`-doit pointer toohello répertoire où hello JDK est installé.
* `PATH`-doit contenir hello suivant des chemins d’accès :
  
    * `JAVA_HOME`(ou les chemins d’accès équivalents hello).
    * `JAVA_HOME\bin`(ou les chemins d’accès équivalents hello).
    * répertoire de Hello où Maven est installé.

## <a name="create-hello-clusters"></a>Créer des clusters de hello

Kafka Apache sur HDInsight ne fournit pas d’accès toohello Kafka courtiers sur hello internet public. Tout ce qui tooKafka doit se trouver dans des entretiens hello même réseau virtuel Azure en tant que nœuds hello dans hello cluster de Kafka. Pour cet exemple, hello Kafka et les clusters Storm se trouvent dans un réseau virtuel Azure. Hello diagramme suivant illustre le flux de communication entre les clusters hello :

![Diagramme des clusters Storm et Kafka dans un réseau virtuel Azure](./media/hdinsight-apache-storm-with-kafka/storm-kafka-vnet.png)

> [!NOTE]
> Autres services sur un cluster de hello tels que SSH et Ambari sont accessibles via hello internet. Pour plus d’informations sur les ports publics de hello disponibles avec HDInsight, consultez [Ports et URI utilisé par HDInsight](hdinsight-hadoop-port-settings-for-services.md).

Tandis que vous pouvez créer un réseau virtuel Azure, Kafka, Storm clusters manuellement, il est plus facile toouse un modèle Azure Resource Manager. Toodeploy un réseau virtuel Azure, Kafka, les étapes suivantes de hello utilisation et Storm clusters tooyour abonnement Azure.

1. Utilisez hello suivant toosign bouton dans tooAzure et modèle ouvert hello Bonjour portail Azure.
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-kafka-storm-cluster-in-vnet-v2.json" target="_blank"><img src="./media/hdinsight-apache-storm-with-kafka/deploy-to-azure.png" alt="Deploy tooAzure"></a>
   
    Hello modèle Azure Resource Manager se trouve dans **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-storm-cluster-in-vnet-v1.json**. Il crée hello suivant des ressources :
    
    * Groupe de ressources Azure
    * Réseau virtuel Azure
    * Compte de Stockage Azure
    * Kafka sur HDInsight version 3.6 (trois nœuds worker)
    * Storm sur HDInsight version 3.6 (trois nœuds worker)

  > [!WARNING]
  > disponibilité tooguarantee de Kafka sur HDInsight, votre cluster doit contenir au moins trois nœuds de travail. Ce modèle crée un cluster Kafka qui contient trois nœuds Worker.

2. Hello utilisation suivant des entrées de hello toopopulate des conseils de hello **les déploiement personnalisé** panneau :
   
    ![Déploiement HDInsight personnalisé](./media/hdinsight-apache-storm-with-kafka/parameters.png)

    * **Groupe de ressources** : créez un groupe de ressources ou sélectionnez-en un. Ce groupe contient un cluster HDInsight de hello.
   
    * **Emplacement**: sélectionnez un tooyou géographiquement fermer d’emplacement.

    * **Nom du Cluster de base**: cette valeur est utilisée comme nom de base hello pour les clusters de Storm et Kafka hello. Par exemple, si vous entrez **hdi**, cela crée un cluster Storm nommé **storm-hdi** et un cluster Kafka nommé **kafka-hdi**.
   
    * **Nom d’utilisateur de cluster**: nom d’utilisateur admin hello pour les clusters de Storm et Kafka hello.
   
    * **Mot de passe de connexion cluster**: hello mot de passe administrateur pour les clusters de Storm et Kafka hello.
    
    * **Nom d’utilisateur SSH**: hello toocreate d’utilisateur SSH pour les clusters de Storm et Kafka hello.
    
    * **Mot de passe SSH**: mot de passe de hello pour hello SSH pour les clusters de Storm et Kafka hello.

3. Hello de lecture **termes et Conditions**, puis sélectionnez **J’accepte les termes du contrat de toohello et conditions susmentionnées**.

4. Enfin, recherchez **code confidentiel toodashboard** , puis sélectionnez **bon**. Il prend environ 20 minutes toocreate les clusters hello.

Une fois que les ressources hello ont été créées, panneau hello pour le groupe de ressources hello s’affiche.

![Panneau des ressources de groupe de réseau virtuel de hello et des clusters](./media/hdinsight-apache-storm-with-kafka/groupblade.png)

> [!IMPORTANT]
> Notez que les noms de hello des clusters HDInsight de hello sont **storm-BASENAME** et **kafka-BASENAME**, où BASENAME est nom hello toohello modèle fourni. Vous utilisez ces noms dans les étapes suivantes lors de la connexion toohello clusters.

## <a name="understanding-hello-code"></a>Description du code hello

Ce projet contient deux topologies :

* **KafkaWriter**: défini par hello **writer.yaml** fichier, écrit de cette topologie tooKafka phrases aléatoire à l’aide de hello KafkaBolt fourni avec Apache Storm.

    Cette topologie utilise personnalisé **SentenceSpout** phrases aléatoire toogenerate de composant.

* **KafkaReader**: défini par hello **reader.yaml** fichier, cette topologie lit les données à partir de Kafka à l’aide de hello KafkaSpout fourni avec Apache Storm, puis journaux hello toostdout de données.

    Cette topologie utilise stockage toodefault hello Storm HdfsBolt toowrite pour le cluster de Storm hello.
### <a name="flux"></a>Flux

topologies de Hello sont définis à l’aide de [Flux](https://storm.apache.org/releases/1.1.0/flux.html). Flux a été introduite dans renverser 0.10.x et vous permet de configuration de la topologie hello tooseparate à partir du code hello. Pour les Topologies qui utilisent l’infrastructure de Flux hello, topologie de hello est défini dans un fichier YAML. fichier YAML Hello peut être inclus dans le cadre de la topologie de hello. Il peut également être un fichier autonome utilisé lorsque vous soumettez une topologie de hello. Flux prend également en charge la substitution des variables au moment de l’exécution, ce qui est utilisé dans cet exemple.

Hello paramètres suivants sont définies au moment de l’exécution de ces topologies :

* `${kafka.topic}`: nom hello Hello Kafka rubrique topologies de hello en lecture/écriture à.

* `${kafka.broker.hosts}`: hello héberge ce hello Kafka fournit s’exécutent sur. informations de service broker Hello sont utilisées par hello KafkaBolt lors de l’écriture de tooKafka.

* `${kafka.zookeeper.hosts}`: hôtes hello soigneur s’exécute dans hello cluster de Kafka.

Pour plus d’informations sur les topologies Flux, voir la page [https://storm.apache.org/releases/1.1.0/flux.html](https://storm.apache.org/releases/1.1.0/flux.html).

## <a name="download-and-compile-hello-project"></a>Télécharger et compilez le projet de hello

1. Sur votre environnement de développement, télécharger le projet à partir de hello [https://github.com/Azure-Samples/hdinsight-storm-java-kafka](https://github.com/Azure-Samples/hdinsight-storm-java-kafka), ouvrez une ligne de commande et modifier l’emplacement de toohello répertoires que vous avez téléchargé le projet de hello.

2. À partir de hello **hdinsight-storm-java-kafka** répertoire, suivante de hello utilisation projet hello de toocompile de commande et créer un package de déploiement :

  ```bash
  mvn clean package
  ```

    processus du package Hello crée un fichier nommé `KafkaTopology-1.0-SNAPSHOT.jar` Bonjour `target` active.

3. Utilisez hello suivant de commandes toocopy hello package tooyour tempête de cluster HDInsight. Remplacez **nom d’utilisateur** avec le nom d’utilisateur SSH hello pour le cluster de hello. Remplacez **BASENAME** avec le nom de base hello que vous avez utilisé lors de la création du cluster de hello.

  ```bash
  scp ./target/KafkaTopology-1.0-SNAPSHOT.jar USERNAME@storm-BASENAME-ssh.azurehdinsight.net:KafkaTopology-1.0-SNAPSHOT.jar
  ```

    Lorsque vous y êtes invité, entrez le mot de passe hello utilisé lors de la création de clusters de hello.

## <a name="configure-hello-topology"></a>Configurer la topologie de hello

1. Utilisez une des hello suivant les méthodes toodiscover hello hôtes de service broker Kafka :

    ```powershell
    $creds = Get-Credential -UserName "admin" -Message "Enter hello HDInsight login"
    $clusterName = Read-Host -Prompt "Enter hello Kafka cluster name"
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/KAFKA/components/KAFKA_BROKER" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $brokerHosts = $respObj.host_components.HostRoles.host_name[0..1]
    ($brokerHosts -join ":9092,") + ":9092"
    ```

    ```bash
    curl -su admin -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/KAFKA/components/KAFKA_BROKER" | jq -r '["\(.host_components[].HostRoles.host_name):9092"] | join(",")' | cut -d',' -f1,2
    ```

    > [!IMPORTANT]
    > Hello Bash exemple suppose que `$CLUSTERNAME` contient le nom hello du cluster HDInsight de hello. Il suppose également que [jq](https://stedolan.github.io/jq/) est installé. Lorsque vous y êtes invité, entrez le mot de passe de hello hello cluster compte de connexion.

    valeur de Hello retournée est similaire toohello suivant du texte :

        wn0-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:9092,wn1-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:9092

    > [!IMPORTANT]
    > Il peut être plus de deux hôtes de service broker pour votre cluster, il est inutile tooprovide une liste complète de tous les hôtes tooclients. Un ou deux sont suffisants.

2. Utilisez une des hello suivant les ordinateurs hôtes de méthodes toodiscover hello Kafka soigneur :

    ```powershell
    $creds = Get-Credential -UserName "admin" -Message "Enter hello HDInsight login"
    $clusterName = Read-Host -Prompt "Enter hello Kafka cluster name"
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/ZOOKEEPER/components/ZOOKEEPER_SERVER" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $zookeeperHosts = $respObj.host_components.HostRoles.host_name[0..1]
    ($zookeeperHosts -join ":2181,") + ":2181"
    ```

    ```bash
    curl -su admin -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/ZOOKEEPER/components/ZOOKEEPER_SERVER" | jq -r '["\(.host_components[].HostRoles.host_name):2181"] | join(",")' | cut -d',' -f1,2
    ```

    > [!IMPORTANT]
    > Hello Bash exemple suppose que `$CLUSTERNAME` contient le nom hello du cluster HDInsight de hello. Il suppose également que [jq](https://stedolan.github.io/jq/) est installé. Lorsque vous y êtes invité, entrez le mot de passe de hello hello cluster compte de connexion.

    valeur de Hello retournée est similaire toohello suivant du texte :

        zk0-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:2181,zk2-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:2181

    > [!IMPORTANT]
    > Lorsqu’il y a plus de deux nœuds soigneur, il est inutile tooprovide une liste complète de tous les hôtes tooclients. Un ou deux sont suffisants.

    Enregistrez cette valeur, car vous l’utiliserez plus tard.

3. Modifier hello `dev.properties` dans fichier hello la racine du projet de hello. Ajoutez hello Broker et les lignes correspondantes de soigneur hôtes informations toohello dans ce fichier. Hello suivant configuré avec les valeurs d’exemple hello des étapes précédentes de hello :

        kafka.zookeeper.hosts: zk0-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:2181,zk2-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:2181
        kafka.broker.hosts: wn0-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:9092,wn1-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:9092
        kafka.topic: stormtopic

4. Enregistrer hello `dev.properties` fichier, puis utiliser hello suivant tooupload de commande de cluster de Storm toohello :

     ```bash
    scp dev.properties USERNAME@storm-BASENAME-ssh.azurehdinsight.net:KafkaTopology-1.0-SNAPSHOT.jar
    ```

    Remplacez **nom d’utilisateur** avec le nom d’utilisateur SSH hello pour le cluster de hello. Remplacez **BASENAME** avec le nom de base hello que vous avez utilisé lors de la création du cluster de hello.

## <a name="start-hello-writer"></a>Démarrer l’enregistreur de hello

1. Utilisez hello suivant cluster Storm de tooconnect toohello à l’aide de SSH. Remplacez **nom d’utilisateur** par nom d’utilisateur SSH hello utilisé lors de la création du cluster de hello. Remplacez **BASENAME** par nom de base hello utilisé lors de la création du cluster de hello.

  ```bash
  ssh USERNAME@storm-BASENAME-ssh.azurehdinsight.net
  ```

    Lorsque vous y êtes invité, entrez le mot de passe hello utilisé lors de la création de clusters de hello.
   
    Pour en savoir plus, voir [Utilisation de SSH avec HDInsight (Hadoop) depuis Bash (l’interpréteur de commande) sur Windows 10, Linux, Unix ou OS X](hdinsight-hadoop-linux-use-ssh-unix.md).

2. À partir de hello connexion SSH, utilisez hello suivant commande toocreate hello rubrique Kafka utilisé par la topologie de hello :

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --create --replication-factor 3 --partitions 8 --topic stormtopic --zookeeper $KAFKAZKHOSTS
    ```

    Remplacez `$KAFKAZKHOSTS` par hello soigneur héberger les informations que vous avez récupéré dans la section précédente de hello.

2. À partir de cluster de Storm toohello hello SSH connexion, utilisez hello suivant la topologie d’enregistreur commande toostart hello :

    ```bash
    storm jar KafkaTopology-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /writer.yaml --filter dev.properties
    ```

    paramètres de Hello utilisés avec cette commande sont :

    * `org.apache.storm.flux.Flux`: Utilisez des Flux tooconfigure et exécuter cette topologie.

    * `--remote`: Envoyez hello topologie tooNimbus. topologie de Hello est réparti entre les nœuds de cluster de hello travail de hello.

    * `-R /writer.yaml`: Hello d’utilisation `writer.yaml` topologie de hello tooconfigure de fichiers. `-R`Indique que cette ressource est incluse dans le fichier jar hello. Il est donc dans racine hello JAR de hello, `/writer.yaml` est tooit de chemin d’accès hello.

    * `--filter`: Remplir les entrées de hello `writer.yaml` topologie à l’aide de valeurs Bonjour `dev.properties` fichier. Par exemple, hello valeur Hello `kafka.topic` entrée dans le fichier de hello est utilisé tooreplace hello `${kafka.topic}` entrée dans la définition de la topologie hello.

5. Une fois que la topologie de hello a démarré, utilisez hello suivant tooverify commande que qu’elle écrit des données toohello rubrique de Kafka :

  ```bash
  /usr/hdp/current/kafka-broker/bin/kafka-console-consumer.sh --zookeeper $KAFKAZKHOSTS --from-beginning --topic stormtopic
  ```

    Remplacez `$KAFKAZKHOSTS` par hello soigneur héberger les informations que vous avez récupéré dans la section précédente de hello.

    Cette commande utilise un script inclu dans la rubrique de Kafka toomonitor hello. Après quelques instants, il doit commence à renvoyer des phrases aléatoires qui ont été écrits toohello rubrique. Hello la sortie est similaire toohello l’exemple suivant :

        i am at two with nature             
        an apple a day keeps hello doctor away
        snow white and hello seven dwarfs     
        hello cow jumped over hello moon        
        an apple a day keeps hello doctor away
        an apple a day keeps hello doctor away
        hello cow jumped over hello moon        
        an apple a day keeps hello doctor away
        an apple a day keeps hello doctor away
        four score and seven years ago      
        snow white and hello seven dwarfs     
        snow white and hello seven dwarfs     
        i am at two with nature             
        an apple a day keeps hello doctor away

    Utilisez Ctrl + script de hello toostop c.

## <a name="start-hello-reader"></a>Démarrer le lecteur de hello

1. À partir de cluster de Storm toohello hello SSH session, utilisez hello suivant la topologie du lecteur de commande toostart hello :

  ```bash
  storm jar KafkaTopology-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /reader.yaml --filter dev.properties
  ```

2. Une fois que la topologie de hello démarre, ouvrez hello Storm UI. Cette interface utilisateur web est située dans https://storm-BASENAME.azurehdinsight.net/stormui. Remplacez __BASENAME__ par nom de base hello utilisé lors de la création de cluster de hello. 

    Lorsque vous y êtes invité, utilisez le nom de connexion d’administrateur hello (valeur par défaut, `admin`) et le mot de passe utilisé lors de la création de cluster de hello. Vous voyez un toohello similaire de page web suivant image :

    ![Interface utilisateur de Storm](./media/hdinsight-apache-storm-with-kafka/stormui.png)

3. À partir de l’interface utilisateur tempête de hello, sélectionnez hello __kafka-lecteur__ lien Bonjour __récapitulatif de la topologie__ section toodisplay informations hello __kafka-lecteur__ topologie.

    ![Section de résumé de topologie de l’interface utilisateur web de Storm hello](./media/hdinsight-apache-storm-with-kafka/topology-summary.png)

4. toodisplay plus d’informations sur les instances du composant de journal-éclair hello, sélectionnez hello hello __éclair de l’enregistreur d’événements__ lien Bonjour __boulons (tout temps)__ section.

    ![Lien d’éclair de l’enregistreur d’événements dans la section de boulons hello](./media/hdinsight-apache-storm-with-kafka/bolts.png)

5. Bonjour __exécuteurs__ , sélectionnez un lien dans hello __Port__ les informations de journalisation toodisplay de colonne sur cette instance du composant de hello.

    ![Exécuteurs de lien](./media/hdinsight-apache-storm-with-kafka/executors.png)

    journal de Hello contient un journal des données de hello lues à partir de la rubrique de Kafka de hello. informations Hello dans le journal de hello sont similaire toohello suivant du texte :

        2016-11-04 17:47:14.907 c.m.e.LoggerBolt [INFO] Received data: four score and seven years ago
        2016-11-04 17:47:14.907 STDIO [INFO] hello cow jumped over hello moon
        2016-11-04 17:47:14.908 c.m.e.LoggerBolt [INFO] Received data: hello cow jumped over hello moon
        2016-11-04 17:47:14.911 STDIO [INFO] snow white and hello seven dwarfs
        2016-11-04 17:47:14.911 c.m.e.LoggerBolt [INFO] Received data: snow white and hello seven dwarfs
        2016-11-04 17:47:14.932 STDIO [INFO] snow white and hello seven dwarfs
        2016-11-04 17:47:14.932 c.m.e.LoggerBolt [INFO] Received data: snow white and hello seven dwarfs
        2016-11-04 17:47:14.969 STDIO [INFO] an apple a day keeps hello doctor away
        2016-11-04 17:47:14.970 c.m.e.LoggerBolt [INFO] Received data: an apple a day keeps hello doctor away

## <a name="stop-hello-topologies"></a>Arrêter les topologies hello

À partir d’un cluster Storm SSH session toohello, utilisez hello suivant des topologies de commandes toostop hello Storm :

  ```bash
  storm kill kafka-writer
  storm kill kafka-reader
  ```

## <a name="delete-hello-cluster"></a>Supprimer le cluster de hello

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

Étant donné que les étapes de hello dans ce document vous allez créer deux clusters dans hello même groupe de ressources Azure, vous pouvez supprimer le groupe de ressources hello Bonjour portail Azure. Groupe de ressources hello suppression supprime toutes les ressources créées en suivant ce document.

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’exemples de topologies qui peuvent être utilisées avec Storm sur HDInsight, consultez [Exemples de topologies et composants Storm](hdinsight-storm-example-topology.md).

Pour plus d’informations sur le déploiement et la surveillance des topologies sur HDInsight Linux, consultez [Déploiement et gestion des topologies Apache Storm sur HDInsight Linux](hdinsight-storm-deploy-monitor-topology-linux.md)