---
title: "aaaTroubleshoot Storm à l’aide d’Azure HDInsight | Documents Microsoft"
description: "Obtenez des réponses toocommon des questions sur l’utilisation d’Apache Storm avec Azure HDInsight."
keywords: "Azure HDInsight, Storm, FAQ, guide de dépannage, problèmes courants"
services: Azure HDInsight
documentationcenter: na
author: raviperi
manager: 
editor: 
ms.assetid: 74E51183-3EF4-4C67-AA60-6E12FAC999B5
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/7/2017
ms.author: raviperi
ms.openlocfilehash: 51bcb3dc28eff5ee7bb33252fb2ec71a88ed8e09
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-storm-by-using-azure-hdinsight"></a>Résolution de problèmes Storm à l’aide d’Azure HDInsight

En savoir plus sur les principaux problèmes de hello et leurs résolutions pour travailler avec des charges utiles d’Apache Storm dans Apache Ambari.

## <a name="how-do-i-access-hello-storm-ui-on-a-cluster"></a>Comment accéder à hello Storm UI sur un cluster
Vous avez deux options pour l’accès aux hello Storm UI à partir d’un navigateur :

### <a name="ambari-ui"></a>Interface utilisateur Ambari
1. Accédez à tableau de bord toohello Ambari.
2. Dans la liste de hello des services, sélectionnez **Storm**.
3. Bonjour **liens rapides** menu, sélectionnez **Storm UI**.

### <a name="direct-link"></a>Lien direct
Vous pouvez accéder hello Storm UI à hello suivant l’URL :

https://\<nom DNS du cluster\>/stormui

Exemple :

 https://stormcluster.azurehdinsight.net/stormui

## <a name="how-do-i-transfer-storm-event-hub-spout-checkpoint-information-from-one-topology-tooanother"></a>Comment transférer des informations de point de contrôle du concentrateur bec Storm événement à partir d’une topologie tooanother

Lorsque vous développez des topologies de lecture à partir de concentrateurs d’événements Azure à l’aide de hello HDInsight Storm événement hub bec .jar fichier, vous devez déployer une topologie disposant hello même nom sur un nouveau cluster. Toutefois, vous devez conserver les données de point de contrôle hello qui a été validée tooApache soigneur sur l’ancien cluster de hello.

### <a name="where-checkpoint-data-is-stored"></a>Où sont stockées les données de point de contrôle ?
Les données de point de contrôle pour les décalages sont stockées par bec de concentrateur d’événements hello dans soigneur dans deux chemins d’accès racine :
- Les points de contrôle de spout non transactionnels sont stockés dans /eventhubspout.
- Les données de point de contrôle de spout transactionnel sont stockées dans /transactional.

### <a name="how-toorestore"></a>Comment toorestore
scripts de hello tooget et bibliothèques que vous utilisez données tooexport hors soigneur et l’importer tooZooKeeper de retour de données hello avec un nouveau nom, consultez [exemples de HDInsight Storm](https://github.com/hdinsight/hdinsight-storm-examples/tree/master/tools/zkdatatool-1.0).

le dossier lib Hello a fichiers .jar qui contiennent l’implémentation hello pour l’opération d’importation/exportation hello. Hello bash dossier a un exemple de script qui montre comment les données tooexport à partir de hello server soigneur sur l’ancien cluster de hello et importez-le server de soigneur toohello arrière sur le nouveau cluster de hello.

Exécutez hello [stormmeta.sh](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/tools/zkdatatool-1.0/bash/stormmeta.sh) hello soigneur nœuds tooexport de script et importer des données. Mise à jour hello script toohello Hortonworks Data Platform (HDP) version correcte. (Nous travaillons sur la création de scripts génériques dans HDInsight. Scripts génériques peuvent s’exécuter n’importe quel nœud à cluster hello sans modification par l’utilisateur de hello.)

commande d’exportation Hello écrit hello métadonnées tooan système de fichiers distribués d’Apache Hadoop (HDFS) chemin (dans un magasin de stockage d’objets Blob Azure ou Azure Data Lake Store) à un emplacement que vous définissez.

### <a name="examples"></a>Exemples

#### <a name="export-offset-metadata"></a>Exporter les métadonnées de décalage
1. Utilisez cluster soigneur SSH toogo toohello sur cluster hello quel point de contrôle hello offset doit toobe exporté.
2. Exécution hello commande suivante (une fois que vous mettez à jour hello chaîne de version HDP) tooexport soigneur décalage des données toohello /stormmetadta/zkdata HDFS chemin d’accès :

    ```apache   
    java -cp ./*:/etc/hadoop/conf/*:/usr/hdp/2.5.1.0-56/hadoop/*:/usr/hdp/2.5.1.0-56/hadoop/lib/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/lib/*:/etc/failover-controller/conf/*:/etc/hadoop/* com.microsoft.storm.zkdatatool.ZkdataImporter export /eventhubspout /stormmetadata/zkdata
    ```

#### <a name="import-offset-metadata"></a>Importer les métadonnées de décalage
1. Utilisez cluster soigneur SSH toogo toohello sur cluster hello quel point de contrôle hello offset doit toobe exporté.
2. Exécution hello après une commande (une fois que vous mettez à jour de chaîne de version HDP hello) tooimport soigneur décalage des données hello HDFS chemin d’accès/stormmetadata/zkdata toohello soigneur serveur sur un cluster de hello cible :

    ```apache
    java -cp ./*:/etc/hadoop/conf/*:/usr/hdp/2.5.1.0-56/hadoop/*:/usr/hdp/2.5.1.0-56/hadoop/lib/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/lib/*:/etc/failover-controller/conf/*:/etc/hadoop/* com.microsoft.storm.zkdatatool.ZkdataImporter import /eventhubspout /home/sshadmin/zkdata
    ```
   
#### <a name="delete-offset-metadata-so-that-topologies-can-start-processing-data-from-hello-beginning-or-from-a-timestamp-that-hello-user-chooses"></a>Supprimer les métadonnées de décalage topologies peuvent démarrer le traitement des données à partir du début de hello, ou d’un horodateur choisit cet utilisateur hello
1. Utilisez cluster soigneur SSH toogo toohello sur cluster hello quel point de contrôle hello offset doit toobe exporté.
2. Exécution hello après une commande (une fois que vous mettez à jour de chaîne de version HDP hello) toodelete tous les soigneur décalage des données dans le cluster actuel hello :

    ```apache
    java -cp ./*:/etc/hadoop/conf/*:/usr/hdp/2.5.1.0-56/hadoop/*:/usr/hdp/2.5.1.0-56/hadoop/lib/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/lib/*:/etc/failover-controller/conf/*:/etc/hadoop/* com.microsoft.storm.zkdatatool.ZkdataImporter delete /eventhubspout
    ```

## <a name="how-do-i-locate-storm-binaries-on-a-cluster"></a>Comment localiser les fichiers binaires de Storm sur un cluster ?
Fichiers binaires de Storm pour la pile HDP hello en cours sont dans /usr/hdp/current/storm-client. emplacement de Hello est hello même pour les nœuds principaux et les nœuds de travail.
 
Il peut y avoir plusieurs fichiers binaires pour des versions spécifiques de HDP à l’emplacement /usr/hdp (par exemple, /usr/hdp/2.5.0.1233/storm). dossier de /usr/hdp/current/storm-client Hello est symlinked toohello version la plus récente est en cours d’exécution sur le cluster de hello.

Pour plus d’informations, consultez [cluster de HDInsight tooan de se connecter à l’aide de SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix) et [Storm](http://storm.apache.org/).
 
## <a name="how-do-i-determine-hello-deployment-topology-of-a-storm-cluster"></a>Comment déterminer la topologie de déploiement hello d’un cluster Storm
Commencez par identifier tous les composants installés avec HDInsight Storm. Un cluster Storm se compose de quatre catégories de nœuds :

* Nœuds de passerelle
* Nœuds principaux
* Nœuds ZooKeeper
* Nœuds de travail
 
### <a name="gateway-nodes"></a>Nœuds de passerelle
Un nœud de passerelle est une passerelle et le service de proxy inverse qui permet un accès public tooan active Ambari management service. Il gère également le choix du leader Ambari.
 
### <a name="head-nodes"></a>Nœuds principaux
Les nœuds principaux Storm exécutent hello suivant services :
* Nimbus
* Ambari Server
* Ambari Metrics Server
* Ambari Metrics Collector
 
### <a name="zookeeper-nodes"></a>Nœuds ZooKeeper
HDInsight est fourni avec un quorum de trois nœuds ZooKeeper. taille du quorum Hello est fixe et ne peuvent pas être reconfiguré.
 
Services Storm dans un cluster de hello sont quorum de soigneur tooautomatically configuré utilisez hello.
 
### <a name="worker-nodes"></a>Nœuds de travail
Nœuds de travail Storm exécutent hello suivant services :
* Supervisor
* Machines virtuelles Java (JVM) de travail, pour l’exécution des topologies
* Ambari Agent
 
## <a name="how-do-i-locate-storm-event-hub-spout-binaries-for-development"></a>Comment localiser les fichiers binaires de spout EventHub Storm pour le développement ?
 
Pour plus d’informations sur l’utilisation de fichiers .jar de Storm événement hub bec avec votre topologie, consultez hello suivant des ressources.
 
### <a name="java-based-topology"></a>Topologie basée sur Java
[Traitement des événements Azure Event Hubs avec Storm sur HDInsight (Java)](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-storm-develop-java-event-hub-topology)
 
### <a name="c-based-topology-mono-on-hdinsight-34-linux-storm-clusters"></a>Topologie basée sur C# (Mono sur les clusters Storm HDInsight 3.4+ Linux)
[Traiter des événements issus d’Azure Event Hubs avec Storm sur HDInsight (C#)](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-storm-develop-csharp-event-hub-topology)
 
### <a name="latest-storm-event-hub-spout-binaries-for-hdinsight-35-linux-storm-clusters"></a>Fichiers binaires de spout EventHub Storm les plus récents pour les clusters Storm HDInsight 3.5+ Linux
toolearn toouse hello dernière Storm événement hub bec qui fonctionne avec HDInsight 3.5 + Linux Storm clusters, voir hello mvn-repo [fichier Lisez-moi](https://github.com/hdinsight/mvn-repo/blob/master/README.md).
 
### <a name="source-code-examples"></a>Exemples de code source
Consultez [exemples](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub) de façon tooread et écrire à partir du concentrateur d’événements Azure à l’aide d’une topologie d’Apache Storm (écrite en Java) sur un cluster Azure HDInsight.
 
## <a name="how-do-i-locate-storm-log4j-configuration-files-on-clusters"></a>Comment localiser les fichiers de configuration Storm Log4J sur les clusters ?
 
tooidentify Apache Log4J les fichiers de configuration pour les services de Storm.
 
### <a name="on-head-nodes"></a>Sur les nœuds principaux
configuration de Hello Nimbus Log4J est lu à partir / usr/hdp/\<version HDP\>/storm/log4j2/cluster.xml.
 
### <a name="on-worker-nodes"></a>Sur les nœuds de travail
configuration de superviseur Log4J Hello est lu à partir / usr/hdp/\<version HDP\>/storm/log4j2/cluster.xml.
 
fichier de configuration du travail Log4J Hello est lu à partir / usr/hdp/\<version HDP\>/storm/log4j2/worker.xml.
 
Par exemple : /usr/hdp/2.6.0.2-76/storm/log4j2/cluster.xml /usr/hdp/2.6.0.2-76/storm/log4j2/worker.xml

