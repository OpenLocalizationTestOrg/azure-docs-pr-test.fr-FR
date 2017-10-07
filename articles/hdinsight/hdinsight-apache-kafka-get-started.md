---
title: aaaStart avec Apache Kafka - Azure HDInsight | Documents Microsoft
description: "Découvrez comment toocreate un Kafka Apache cluster sur Azure HDInsight. Découvrez comment toocreate consommateurs, rubriques et les abonnés."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 43585abf-bec1-4322-adde-6db21de98d7f
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: 
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/14/2017
ms.author: larryfr
ms.openlocfilehash: b93299d88dc2cf9a9764662509308ff75fd74474
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="start-with-apache-kafka-preview-on-hdinsight"></a>Démarrer avec Apache Kafka (version préliminaire) sur HDInsight

Découvrez comment toocreate et utiliser une [Apache Kafka](https://kafka.apache.org) cluster sur Azure HDInsight. Kafka est une plateforme de diffusion en continu distribuée open source, disponible avec HDInsight. Il est souvent utilisé comme un courtier de messages, car il fournit des fonctionnalités similaires tooa publication-abonnement file d’attente.

> [!NOTE]
> Il existe actuellement deux versions de Kafka disponibles avec HDInsight ; 0.9.0 (HDInsight 3.4) et 0.10.0 (HDInsight 3.5 et 3.6). étapes de Hello dans ce document supposent que vous utilisez Kafka sur HDInsight 3.6.

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="create-a-kafka-cluster"></a>Création d’un cluster Kafka

Utilisez hello suivant les étapes toocreate un Kafka de cluster HDInsight :

1. À partir de hello [portail Azure](https://portal.azure.com), sélectionnez **+ nouveau**, **Intelligence + Analytique**, puis sélectionnez **HDInsight**.
   
    ![Création d'un cluster HDInsight](./media/hdinsight-apache-kafka-get-started/create-hdinsight.png)

2. À partir de **notions de base**, entrez hello informations suivantes :

    * **Nom du cluster**: nom hello du cluster HDInsight de hello.
    * **Abonnement**: sélectionnez hello abonnement toouse.
    * **Nom d’utilisateur de cluster** et **mot de passe de connexion Cluster**: connexion hello lors de l’accès de cluster de hello via le protocole HTTPS. Vous utilisez ces services de tooaccess des informations d’identification telles que hello l’interface utilisateur de Ambari Web ou l’API REST.
    * **Secure Shell (SSH) username**: connexion hello utilisée lors de l’accès de cluster de hello via SSH. Par défaut, un mot de passe hello est hello identique au mot de passe de connexion hello cluster.
    * **Groupe de ressources**: hello ressource groupe toocreate hello cluster.
    * **Emplacement**: hello région Azure toocreate hello cluster.
   
 ![Sélectionnez un abonnement](./media/hdinsight-apache-kafka-get-started/hdinsight-basic-configuration.png)

3. Sélectionnez **Cluster type**, puis en suivant hello du jeu de valeurs à partir de **configuration de Cluster**:
   
    * **Type de cluster** : Kafka

    * **Version** : Kafka 0.10.0 (HDI 3.6)

    * **Niveau cluster** : standard
     
 Enfin, utilisez hello **sélectionnez** bouton toosave paramètres.
     
 ![Sélectionner un type de cluster](./media/hdinsight-apache-kafka-get-started/set-hdinsight-cluster-type.png)

4. Après avoir sélectionné le type de cluster hello, utilisez hello __sélectionnez__ tooset hello cluster type de bouton. Ensuite, utilisez hello __suivant__ configuration de base de toofinish de bouton.

5. À partir du panneau **Stockage**, sélectionnez ou créez un compte de stockage. Pour connaître les étapes hello dans ce document, laissez hello autres champs à des valeurs par défaut hello. Hello d’utilisation __suivant__ configuration du stockage toosave bouton.

    ![Définir les paramètres de compte de stockage hello pour HDInsight](./media/hdinsight-apache-kafka-get-started/set-hdinsight-storage-account.png)

6. À partir de __(facultatives) les Applications__, sélectionnez __suivant__ toocontinue. Cet exemple ne requiert aucune application.

7. À partir de __taille de Cluster__, sélectionnez __suivant__ toocontinue.

    > [!WARNING]
    > disponibilité tooguarantee de Kafka sur HDInsight, votre cluster doit contenir au moins trois nœuds de travail.

    ![Ensemble hello taille de cluster Kafka](./media/hdinsight-apache-kafka-get-started/kafka-cluster-size.png)

    > [!NOTE]
    > Hello **disques par nœud de travail** contrôles d’entrée hello l’évolutivité de Kafka sur HDInsight. Pour plus d’informations, consultez l’article [Configurer le stockage et l’extensibilité pour Apache Kafka sur HDInsight](hdinsight-apache-kafka-scalability.md).

8. À partir de __paramètres avancés__, sélectionnez __suivant__ toocontinue.

9. À partir de hello **Résumé**, passez en revue la configuration hello pour le cluster de hello. Hello d’utilisation __modifier__ lie toochange tous les paramètres sont incorrects. Enfin, utilisez le cluster de hello toocreate the__Create__ bouton.
   
    ![Résumé de la configuration du cluster](./media/hdinsight-apache-kafka-get-started/hdinsight-configuration-summary.png)
   
    > [!NOTE]
    > Il peut prendre jusqu'à cluster de hello toocreate too20 minutes.

## <a name="connect-toohello-cluster"></a>Se connecter toohello cluster

> [!IMPORTANT]
> Lorsque vous effectuez hello comme suit, vous devez utiliser un client SSH. Pour plus d’informations, consultez hello [utilisation de SSH avec HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.

À partir de votre client, utilisez SSH tooconnect toohello cluster :

```ssh SSHUSER@CLUSTERNAME-ssh.azurehdinsight.net```

Remplacez **SSHUSER** avec nom d’utilisateur SSH de hello vous avez fourni pendant la création du cluster. Remplacez **CLUSTERNAME** avec nom hello du cluster de hello.

Lorsque vous y êtes invité, entrez mot de passe hello utilisé pour hello SSH compte.

Pour en savoir plus, voir [Utilisation de SSH avec HDInsight (Hadoop) depuis Bash (l’interpréteur de commande) sur Windows 10, Linux, Unix ou OS X](hdinsight-hadoop-linux-use-ssh-unix.md).

## <a id="getkafkainfo"></a>Obtenir hello soigneur et service Broker pour les informations sur l’hôte

Lorsque vous utilisez Kafka, vous devez connaître les deux valeurs de l’hôte ; Hello *soigneur* hôtes et hello *Broker* hôtes. Ces hôtes sont utilisés avec hello Kafka API et la plupart des utilitaires hello fournis avec Kafka.

Utilisez hello suivant des variables d’environnement toocreate étapes qui contiennent des informations sur l’hôte hello. Ces variables d’environnement sont utilisés dans les étapes de hello dans ce document.

1. À partir d’un cluster de toohello connexion SSH, suivant de hello utilisez commande tooinstall hello `jq` utilitaire. Cet utilitaire est utilisé tooparse documents JSON et est utile lors de la récupération des informations sur l’hôte service broker hello :
   
    ```bash
    sudo apt -y install jq
    ```

2. variables d’environnement hello tooset avec des informations extraites de Ambari, hello utilisation suivant de commandes :

    ```bash
    CLUSTERNAME='your cluster name'
    PASSWORD='your cluster password'
    export KAFKAZKHOSTS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/ZOOKEEPER/components/ZOOKEEPER_SERVER | jq -r '["\(.host_components[].HostRoles.host_name):2181"] | join(",")' | cut -d',' -f1,2`

    export KAFKABROKERS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/KAFKA/components/KAFKA_BROKER | jq -r '["\(.host_components[].HostRoles.host_name):9092"] | join(",")' | cut -d',' -f1,2`

    echo '$KAFKAZKHOSTS='$KAFKAZKHOSTS
    echo '$KAFKABROKERS='$KAFKABROKERS
    ```

    > [!IMPORTANT]
    > Définissez `CLUSTERNAME=` nom toohello Hello cluster de Kafka. Définissez `PASSWORD=` toohello mot de passe de connexion (admin) vous avez utilisé lors de la création du cluster de hello.

    Hello texte suivant est un exemple de contenu hello de `$KAFKAZKHOSTS`:
   
    `zk0-kafka.eahjefxxp1netdbyklgqj5y1ud.ex.internal.cloudapp.net:2181,zk2-kafka.eahjefxxp1netdbyklgqj5y1ud.ex.internal.cloudapp.net:2181`
   
    Hello texte suivant est un exemple de contenu hello de `$KAFKABROKERS`:
   
    `wn1-kafka.eahjefxxp1netdbyklgqj5y1ud.cx.internal.cloudapp.net:9092,wn0-kafka.eahjefxxp1netdbyklgqj5y1ud.cx.internal.cloudapp.net:9092`

    > [!NOTE]
    > Hello `cut` commande est la liste de hello de tootrim utilisé des entrées d’hôte tootwo hôtes. Vous n’avez pas besoin de tooprovide hello la liste complète des ordinateurs hôtes lors de la création d’un consommateur de Kafka ou le producteur.
   
    > [!WARNING]
    > Ne comptez pas sur les informations de hello retournées à partir de cette session tooalways être précis. Si vous redimensionnez le cluster de hello, nouveau courtiers sont ajoutés ou supprimés. Si une défaillance se produit et un nœud est remplacé, le nom d’hôte hello pour le nœud de hello peut changer.
    >
    > Vous devez récupérer hello soigneur et service Broker pour les informations sur les hôtes dans quelques instants avant de l’utiliser tooensure que vous disposez des informations valides.

## <a name="create-a-topic"></a>Création d'une rubrique

Kafka stocke les flux de données dans des catégories appelées *rubriques*. À partir de SSH une connexion tooa cluster nœud principal, utilisez un script fourni avec Kafka toocreate une rubrique :

```bash
/usr/hdp/current/kafka-broker/bin/kafka-topics.sh --create --replication-factor 3 --partitions 8 --topic test --zookeeper $KAFKAZKHOSTS
```

Cette commande connecte à l’aide des informations sur l’hôte hello stockées dans des tooZookeeper `$KAFKAZKHOSTS`, puis créer la rubrique Kafka nommée **test**. Vous pouvez vérifier que cette rubrique hello a été créée à l’aide de hello script toolist rubriques suivantes :

```bash
/usr/hdp/current/kafka-broker/bin/kafka-topics.sh --list --zookeeper $KAFKAZKHOSTS
```

Hello sortie de cette commande répertorie les rubriques Kafka, qui contient hello **test** rubrique.

## <a name="produce-and-consume-records"></a>Produire et consommer des enregistrements

Kafka stocke les *enregistrements* dans des rubriques. Les enregistrements sont produits par des *producteurs*, et utilisés par des *consommateurs*. Les producteurs récupèrent des enregistrements à partir des *répartiteurs* Kafka. Chaque nœud Worker dans votre cluster HDInsight est un répartiteur Kafka.

Utilisez hello suivant les étapes toostore enregistrements dans la rubrique de test hello vous créé précédemment, puis les lire à l’aide d’un consommateur :

1. À partir de la session SSH hello, utiliser un script fourni avec la rubrique de toohello Kafka toowrite enregistrements :
   
    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-console-producer.sh --broker-list $KAFKABROKERS --topic test
    ```
   
    Vous ne sont pas retournés toohello invite après cette commande. Au lieu de cela, tapez quelques messages texte, puis utilisez **Ctrl + C** toostop envoi toohello rubrique. Chaque ligne est envoyée en tant qu’enregistrement distinct.

2. Utiliser un script fourni avec les enregistrements de tooread Kafka à partir de la rubrique de hello :
   
    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-console-consumer.sh --bootstrap-server $KAFKABROKERS --topic test --from-beginning
    ```
   
    Cette commande récupère les enregistrements hello à partir de la rubrique de hello et les affiche. À l’aide de `--from-beginning` indique hello consommateur toostart à partir du début de hello du flux de hello, tous les enregistrements sont extraits.

3. Utilisez __Ctrl + C__ consommateur de hello toostop.

## <a name="producer-and-consumer-api"></a>API de producteur et de consommateur

Vous pouvez également programmer produire et consommer des enregistrements à l’aide de hello [Kafka API](http://kafka.apache.org/documentation#api). toobuild un producteur de Java et le consommateur, utilisez hello comme suit à partir de votre environnement de développement.

> [!IMPORTANT]
> Vous devez avoir hello suivant des composants installés dans votre environnement de développement :
>
> * [Java JDK 8](http://www.oracle.com/technetwork/java/javase/downloads/index.html), ou un équivalent, par exemple, OpenJDK.
>
> * [Apache Maven](http://maven.apache.org/)
>
> * Un client SSH et les hello `scp` commande. Pour plus d’informations, consultez hello [utilisation de SSH avec HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.

1. Télécharger les exemples de hello de [https://github.com/Azure-Samples/hdinsight-kafka-java-get-started](https://github.com/Azure-Samples/hdinsight-kafka-java-get-started). Par exemple de producteur/consommateur hello, utilisez project de hello Bonjour `Producer-Consumer` active. Cet exemple contient hello classes suivantes :
   
    * **Exécutez** -démarre le consommateur de hello ou le producteur.

    * **Producteur** -magasins 1 000 000 enregistrements toohello rubrique.

    * **Consommateur** -lit les enregistrements à partir de la rubrique de hello.

2. toocreate un package jar, répertoires toohello de déplacer hello `Producer-Consumer` active et l’utilisation hello commande suivante :

    ```
    mvn clean package
    ```

    Cette commande crée un répertoire nommé `target`, qui contient un fichier nommé `kafka-producer-consumer-1.0-SNAPSHOT.jar`.

3. Toocopy hello des commandes suivantes de hello utilisation `kafka-producer-consumer-1.0-SNAPSHOT.jar` HDInsight tooyour de fichiers :
   
    ```bash
    scp ./target/kafka-producer-consumer-1.0-SNAPSHOT.jar SSHUSER@CLUSTERNAME-ssh.azurehdinsight.net:kafka-producer-consumer.jar
    ```
   
    Remplacez **SSHUSER** avec l’utilisateur SSH hello pour votre cluster, puis remplacez **CLUSTERNAME** avec nom hello de votre cluster. Lorsque vous y êtes invité entrez hello le mot de passe utilisateur SSH hello.

4. Une fois hello `scp` commande a fini de copier le fichier de hello, connectez le cluster de toohello à l’aide de SSH. Utilisez hello commande toowrite enregistrements toohello test rubrique suivante :

    ```bash
    java -jar kafka-producer-consumer.jar producer $KAFKABROKERS
    ```

5. Une fois que hello est terminée, utilisez hello suivant tooread de commande à partir de la rubrique de hello :
   
    ```bash
    java -jar kafka-producer-consumer.jar consumer $KAFKABROKERS
    ```
   
    enregistrements Hello lire, ainsi que d’un nombre d’enregistrements, s’affiche. Vous pouvez voir quelques exemples plus de 1 000 000 connecté comme vous avez envoyé la rubrique de toohello plusieurs enregistrements à l’aide d’un script dans une étape antérieure.

6. Utilisez __Ctrl + C__ consommateur de hello tooexit.

### <a name="multiple-consumers"></a>Consommateurs multiples

Les consommateurs Kafka utilisent un groupe de consommateurs lors de la lecture des enregistrements. À l’aide de hello de groupe avec plusieurs consommateurs entraîne charge équilibrée lectures à partir d’une rubrique. Chaque consommateur dans le groupe de hello reçoit une partie des enregistrements de hello. toosee étapes de ce processus en action, hello utilisation suivant :

1. Ouvrez un nouveau cluster de toohello de session SSH, afin que vous ayez deux d'entre eux. Dans chaque session, utilisez hello suivant toostart un consommateur avec hello même ID de groupe de consommateurs :
   
    ```bash
    java -jar kafka-producer-consumer.jar consumer $KAFKABROKERS mygroup
    ```

    Cette commande démarre un consommateur à l’aide des ID de groupe hello `mygroup`.

    > [!NOTE]
    > Utilisez les commandes hello hello [obtenir hello soigneur et service Broker pour les informations sur l’hôte](#getkafkainfo) section tooset `$KAFKABROKERS` pour cette session SSH.

2. Observez comment chaque enregistrements de hello de nombres de session qu’il reçoit à partir de la rubrique de hello. total Hello de deux sessions doit être hello même que vous avez reçu précédemment à partir d’un seul client.

Consommation par des clients dans le même groupe est géré par le biais des partitions pour une rubrique de hello hello de hello. Pourquoi `test` rubrique créée précédemment, il a huit partitions. Si vous ouvrez huit sessions SSH et lancez un consommateur de toutes les sessions, chaque consommateur lit les enregistrements à partir d’une seule partition pour une rubrique de hello.

> [!IMPORTANT]
> Il ne peut pas y avoir plus d’instances de consommateurs dans un groupe de consommateurs que de partitions. Dans cet exemple, un groupe de consommateurs peut contenir des consommateurs de tooeight puisque c’est le nombre de hello de partitions dans la rubrique de hello. Vous pouvez également disposer de plusieurs groupes de consommateurs, chacun ne dépassant pas huit consommateurs.

Enregistrements stockés dans Kafka sont stockées dans l’ordre de hello qu’ils sont reçus au sein d’une partition. tooachieve dans-livraison chronologique des messages pour les enregistrements *au sein d’une partition*, créez un groupe de consommateurs où hello nombre d’instances de consommateur correspond au nombre de hello de partitions. tooachieve dans-livraison chronologique des messages pour les enregistrements *au sein de la rubrique de hello*, créez un groupe de consommateurs avec une instance de consommateur qu’un seul.

## <a name="streaming-api"></a>API de diffusion en continu

Hello API de diffusion en continu a été ajoutée tooKafka dans la version 0.10.0 ; les versions antérieures s’appuient sur Apache Spark ou Storm pour le traitement de flux de données.

1. Si vous n’avez pas déjà fait, téléchargez les exemples hello à partir de [https://github.com/Azure-Samples/hdinsight-kafka-java-get-started](https://github.com/Azure-Samples/hdinsight-kafka-java-get-started) tooyour les environnement de développement. Pour un exemple de diffusion en continu de hello, utilisez project de hello Bonjour `streaming` active.
   
    Ce projet contient une seule classe, `Stream`, qui lit les enregistrements d’hello `test` rubrique créée précédemment. Elle compte mots hello lire et émet chaque rubrique tooa word et nombre nommée `wordcounts`. Hello `wordcounts` rubrique est créée dans une étape ultérieure de cette section.

2. À partir de la ligne de commande hello dans votre environnement de développement, modifier l’emplacement de toohello répertoires de hello `Streaming` répertoire, puis hello utilisation suivant commande toocreate un package jar :

    ```bash
    mvn clean package
    ```

    Cette commande crée un répertoire nommé `target`, qui contient un fichier nommé `kafka-streaming-1.0-SNAPSHOT.jar`.

3. Toocopy hello des commandes suivantes de hello utilisation `kafka-streaming-1.0-SNAPSHOT.jar` HDInsight tooyour de fichiers :
   
    ```bash
    scp ./target/kafka-streaming-1.0-SNAPSHOT.jar SSHUSER@CLUSTERNAME-ssh.azurehdinsight.net:kafka-streaming.jar
    ```
   
    Remplacez **SSHUSER** avec l’utilisateur SSH hello pour votre cluster, puis remplacez **CLUSTERNAME** avec nom hello de votre cluster. Lorsque vous y êtes invité entrez hello le mot de passe utilisateur SSH hello.

4. Une fois hello `scp` commande a fini de copier le fichier de hello, connectez le cluster de toohello à l’aide de SSH et l’utiliser hello suivant commande toocreate hello `wordcounts` rubrique :

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --create --replication-factor 3 --partitions 8 --topic wordcounts --zookeeper $KAFKAZKHOSTS
    ```

5. Ensuite, démarrez hello processus de diffusion en continu à l’aide de hello de commande suivante :
   
    ```bash
    java -jar kafka-streaming.jar $KAFKABROKERS $KAFKAZKHOSTS 2>/dev/null &
    ```
   
    Cette commande démarre hello processus en arrière-plan de hello de diffusion en continu.

6. Suivant de hello utilisez commande toosend messages toohello `test` rubrique. Ces messages sont traités par hello exemple de diffusion en continu :
   
    ```bash
    java -jar kafka-producer-consumer.jar producer $KAFKABROKERS &>/dev/null &
    ```

7. Hello d’utilisation après la sortie de la commande tooview hello écrit toohello `wordcounts` rubrique par hello processus de diffusion en continu :
   
    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-console-consumer.sh --bootstrap-server $KAFKABROKERS --topic wordcounts --from-beginning --formatter kafka.tools.DefaultMessageFormatter --property print.key=true --property key.deserializer=org.apache.kafka.common.serialization.StringDeserializer --property value.deserializer=org.apache.kafka.common.serialization.LongDeserializer
    ```
   
    > [!NOTE]
    > les données de salutation tooview, vous devez indiquer à hello tooprint hello clé et toouse de désérialiseur hello pour hello clé et la valeur. nom de la clé Hello est word de hello et valeur de clé hello contient le nombre de hello.
   
    Hello est similaire toohello suivant texte de sortie :
   
        dwarfs  13635
        ago     13664
        snow    13636
        dwarfs  13636
        ago     13665
        a       13803
        ago     13666
        a       13804
        ago     13667
        ago     13668
        jumped  13640
        jumped  13641
        a       13805
        snow    13637
   
    > [!NOTE]
    > nombre de Hello est incrémenté à chaque fois un mot est rencontré.

7. Utilisez hello __Ctrl + C__ tooexit hello consommateur, puis utilisez hello `fg` commande toobring hello au premier plan de diffusion en continu en arrière-plan tâche toohello précédent. Utilisez __Ctrl + C__ tooexit il également.

## <a name="delete-hello-cluster"></a>Supprimer le cluster de hello

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="troubleshoot"></a>Résolution des problèmes

Si vous rencontrez des problèmes lors de la création de clusters HDInsight, reportez-vous aux [exigences de contrôle d’accès](hdinsight-administer-use-portal-linux.md#create-clusters).

## <a name="next-steps"></a>Étapes suivantes

Dans ce document, vous avez appris les notions de base de hello de l’utilisation de Kafka Apache sur HDInsight. Utilisez hello suivant toolearn plus sur l’utilisation de Kafka :

* [Garantir une haute disponibilité de vos données avec Apache Kafka sur HDInsight](hdinsight-apache-kafka-high-availability.md)
* [Configurer le stockage et l’extensibilité pour Apache Kafka sur HDInsight](hdinsight-apache-kafka-scalability.md)
* [Documentation Apache Kafka](http://kafka.apache.org/documentation.html) à l’adresse kafka.apache.org.
* [Utilisez MirrorMaker toocreate un réplica de Kafka sur HDInsight](hdinsight-apache-kafka-mirroring.md)
* [Utilisation d’Apache Storm avec Kafka sur HDInsight](hdinsight-apache-storm-with-kafka.md)
* [Use Apache Spark with Kafka on HDInsight](hdinsight-apache-spark-with-kafka.md) (Utilisation d’Apache Spark avec Kafka sur HDInsight)
* [Se connecter tooKafka via un réseau virtuel Azure](hdinsight-apache-kafka-connect-vpn-gateway.md)
