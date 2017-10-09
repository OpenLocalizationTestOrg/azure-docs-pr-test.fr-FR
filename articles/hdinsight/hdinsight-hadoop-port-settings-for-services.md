---
title: "aaaPorts utilisé par les services de Hadoop dans HDInsight - Azure | Documents Microsoft"
description: "Liste des ports utilisés par les services Hadoop sur HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: dd14aed9-ec25-4bb3-a20c-e29562735a7d
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/23/2017
ms.author: larryfr
ms.openlocfilehash: 0abc5c1c678aa79816e3e82a74538d2fb6db40ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="ports-used-by-hadoop-services-on-hdinsight"></a>Ports utilisés par les services Hadoop sur HDInsight

Ce document fournit une liste des ports de hello utilisés par les services de Hadoop en cours d’exécution sur les clusters HDInsight de basés sur Linux. Il fournit également des informations sur les ports utilisés tooconnect toohello cluster est à l’aide de SSH.

## <a name="public-ports-vs-non-public-ports"></a>Ports publics et ports non publics

HDInsight basés sur Linux clusters exposent uniquement trois ports publiquement sur hello internet ; 22, 23 et 443. Ces ports sont utilisés toosecurely cluster de hello d’accès à l’aide de SSH et les services exposés sur le protocole HTTPS sécurisé hello.

En interne, HDInsight est implémentée par plusieurs Machines virtuelles Azure (nœuds hello au sein du cluster de hello) en cours d’exécution sur un réseau virtuel Azure. Dans le réseau virtuel de hello, vous pouvez d’accéder à ports ne pas exposées sur hello internet. Par exemple, si vous vous connectez tooone de nœuds principaux d’hello via SSH, à partir du nœud principal hello vous pouvez puis accèdent directement aux services en cours d’exécution sur les nœuds de cluster hello.

> [!IMPORTANT]
> Si vous ne spécifiez pas de réseau virtuel Azure comme une option de configuration pour HDInsight, un réseau virtuel Azure sera créé automatiquement. Toutefois, vous ne pouvez pas joindre autre réseau virtuel de toothis machines (tels que les autres Machines virtuelles Azure ou votre ordinateur de développement client).


réseau virtuel toojoin des ordinateurs supplémentaires toohello, vous devez créer le réseau virtuel de hello tout d’abord et puis de le spécifier lors de la création de votre cluster HDInsight. Pour plus d’informations, consultez [Étendre les capacités de HDInsight en utilisant un réseau virtuel Azure](hdinsight-extend-hadoop-virtual-network.md)

## <a name="public-ports"></a>Ports publics

Hello tous les nœuds dans un cluster HDInsight se trouvent dans un réseau virtuel Azure et ne sont pas accessibles directement à partir de hello internet. Une passerelle publique fournit toohello d’accès internet suivant les ports qui sont communes à tous les types de cluster HDInsight.

| Service | Port | Protocole | Description |
| --- | --- | --- | --- | --- |
| sshd |22 |SSH |Établit une connexion toosshd de clients sur le nœud principal de principal hello. Pour en savoir plus, voir [Utilisation de SSH avec Hadoop Linux sur HDInsight depuis Linux, Unix ou OS X](hdinsight-hadoop-linux-use-ssh-unix.md). |
| sshd |22 |SSH |Établit une connexion toosshd de clients sur le nœud de périmètre hello. Pour en savoir plus, voir [Utilisation de SSH avec Hadoop Linux sur HDInsight depuis Linux, Unix ou OS X](hdinsight-hadoop-linux-use-ssh-unix.md). |
| sshd |23 |SSH |Établit une connexion toosshd de clients sur le nœud principal secondaire de hello. Pour en savoir plus, voir [Utilisation de SSH avec Hadoop Linux sur HDInsight depuis Linux, Unix ou OS X](hdinsight-hadoop-linux-use-ssh-unix.md). |
| Ambari |443 |HTTPS |Interface utilisateur web d’Ambari. Consultez [HDInsight de gérer à l’aide de hello Ambari Web UI](hdinsight-hadoop-manage-ambari.md) |
| Ambari |443 |HTTPS |API Ambari REST. Consultez [HDInsight de gérer à l’aide de hello API REST de Ambari](hdinsight-hadoop-manage-ambari-rest-api.md) |
| WebHCat, |443 |HTTPS |API REST HCatalog. Consultez les pages [Utilisation de Hive avec Curl](hdinsight-hadoop-use-pig-curl.md), [Utilisation de Pig avec Curl](hdinsight-hadoop-use-pig-curl.md), [Utilisation de MapReduce avec Curl](hdinsight-hadoop-use-mapreduce-curl.md) |
| HiveServer2 |443 |ODBC |Se connecte tooHive à l’aide d’ODBC. Consultez [tooHDInsight Excel de se connecter avec le pilote ODBC Microsoft hello](hdinsight-connect-excel-hive-odbc-driver.md). |
| HiveServer2 |443 |JDBC |Se connecte tooHive à l’aide de JDBC. Consultez [connecter tooHive sur HDInsight à l’aide du pilote JDBC de la ruche de hello](hdinsight-connect-hive-jdbc-driver.md) |

suivantes de Hello sont disponibles pour les types de cluster spécifique :

| Service | Port | Protocole | Type de cluster | Description |
| --- | --- | --- | --- | --- |
| Stargate |443 |HTTPS |HBase |API REST HBase. Consultez la page [Prise en main de HBase](hdinsight-hbase-tutorial-get-started-linux.md) |
| Livy |443 |HTTPS |Spark |API REST Spark. Consultez la page [Envoi de travaux Spark à distance à l’aide de Livy](hdinsight-apache-spark-livy-rest-interface.md) |
| Storm |443 |HTTPS |Storm |Interface utilisateur web de Storm. Consultez la page [Déploiement et gestion des topologies Storm sur HDInsight](hdinsight-storm-deploy-monitor-topology-linux.md) |

### <a name="authentication"></a>Authentification

Tous les services exposés publiquement sur hello qu'internet doit être authentifié :

| Port | Informations d'identification |
| --- | --- |
| 22 ou 23 |informations d’identification de Hello SSH utilisateur spécifiées lors de la création du cluster |
| 443 |nom de connexion Hello (valeur par défaut : administrateur) et le mot de passe qui ont été définis lors de la création du cluster |

## <a name="non-public-ports"></a>Ports non publics

> [!NOTE]
> Certains services sont disponibles uniquement sur certains types de clusters. Par exemple, HBase est disponible uniquement sur les clusters de type HBase.

> [!IMPORTANT]
> Certains services s’exécutent uniquement sur un nœud principal à la fois. Si vous essayez de service de toohello tooconnect sur le nœud principal de principal hello et que vous obtenez une erreur 404, recommencez à l’aide du nœud principal secondaire de hello.

### <a name="ambari"></a>Ambari

| Service | Nœuds | Port | Chemin d'accès de l'URL | Protocole | 
| --- | --- | --- | --- | --- |
| Interface utilisateur Web d'Ambari | Nœuds principaux | 8080 | / | HTTP |
| API Ambari REST | Nœuds principaux | 8080 | /api/v1 | HTTP |

Exemples :

* API Ambari REST : `curl -u admin "http://10.0.0.11:8080/api/v1/clusters"`

### <a name="hdfs-ports"></a>Ports HDFS

| Service | Nœuds | Port | Protocole | Description |
| --- | --- | --- | --- | --- |
| Interface utilisateur web de NameNode |Nœuds principaux |30070 |HTTPS |Tooview état de l’interface utilisateur Web |
| Service de métadonnées NameNode |Nœuds principaux |8020 |IPC |Métadonnées du système de fichiers |
| DataNode |Tous les nœuds de travail |30075 |HTTPS |Tooview état de l’interface utilisateur Web, les journaux, etc. |
| DataNode |Tous les nœuds de travail |30010 |&nbsp; |Transfert de données |
| DataNode |Tous les nœuds de travail |30020 |IPC |Opérations sur les métadonnées |
| NameNode secondaire |Nœuds principaux |50090 |HTTP |Point de contrôle pour les métadonnées NameNode |

### <a name="yarn-ports"></a>Ports YARN

| Service | Nœuds | Port | Protocole | Description |
| --- | --- | --- | --- | --- |
| Interface utilisateur web de Resource Manager |Nœuds principaux |8088 |HTTP |Interface utilisateur web pour Resource Manager |
| Interface utilisateur web de Resource Manager |Nœuds principaux |8090 |HTTPS |Interface utilisateur web pour Resource Manager |
| Interface d’administration de Resource Manager |Nœuds principaux |8141 |IPC |Pour les envois d’application (Hive, serveur Hive, Pig, etc.) |
| Scheduler Resource Manager |Nœuds principaux |8030 |HTTP |Interface d’administration |
| Interface d’application Resource Manager |Nœuds principaux |8050 |HTTP |Adresse de l’interface du Gestionnaire d’applications hello |
| NodeManager |Tous les nœuds de travail |30050 |&nbsp; |adresse de Hello du Gestionnaire de conteneur hello |
| Interface utilisateur web de NodeManager |Tous les nœuds de travail |30060 |HTTP |Interface de Resource Manager |
| Adresse de Timeline |Nœuds principaux |10200 |RPC |Hello service RPC du service chronologie. |
| Interface utilisateur web de Timeline |Nœuds principaux |8181 |HTTP |l’interface utilisateur web du service de la chronologie Hello. |

### <a name="hive-ports"></a>Ports Hive

| Service | Nœuds | Port | Protocole | Description |
| --- | --- | --- | --- | --- |
| HiveServer2 |Nœuds principaux |10001 |Thrift |Service pour la connexion tooHive (Thrift/JDBC) |
| Metastore Hive |Nœuds principaux |9083 |Thrift |Service de connexion tooHive métadonnées Thrift/JDBC) |

### <a name="webhcat-ports"></a>Ports WebHCat

| Service | Nœuds | Port | Protocole | Description |
| --- | --- | --- | --- | --- |
| Serveur WebHCat |Nœuds principaux |30111 |HTTP |API web sur HCatalog et d’autres services Hadoop |

### <a name="mapreduce-ports"></a>Ports MapReduce

| Service | Nœuds | Port | Protocole | Description |
| --- | --- | --- | --- | --- |
| JobHistory |Nœuds principaux |19888 |HTTP |Interface utilisateur web de MapReduce JobHistory |
| JobHistory |Nœuds principaux |10020 |&nbsp; |Serveur MapReduce JobHistory |
| ShuffleHandler |&nbsp; |13562 |&nbsp; |Mappage intermédiaire de transferts génère toorequesting REDUCTEURS |

### <a name="oozie"></a>Oozie

| Service | Nœuds | Port | Protocole | Description |
| --- | --- | --- | --- | --- |
| Serveur Oozie |Nœuds principaux |11000 |HTTP |URL du service Oozie |
| Serveur Oozie |Nœuds principaux |11001 |HTTP |Port pour l’administration Oozie |

### <a name="ambari-metrics"></a>Mesures d’Ambari

| Service | Nœuds | Port | Protocole | Description |
| --- | --- | --- | --- | --- |
| TimeLine (historique d’application) |Nœuds principaux |6188 |HTTP |l’interface utilisateur web du service de la chronologie Hello. |
| TimeLine (historique d’application) |Nœuds principaux |30200 |RPC |l’interface utilisateur web du service de la chronologie Hello. |

### <a name="hbase-ports"></a>Ports HBase

| Service | Nœuds | Port | Protocole | Description |
| --- | --- | --- | --- | --- |
| HMaster |Nœuds principaux |16000 |&nbsp; |&nbsp; |
| Interface utilisateur web d’informations sur HMaster |Nœuds principaux |16010 |HTTP |port Hello pour l’interface utilisateur web de HBase Master hello |
| Serveur de la région |Tous les nœuds de travail |16020 |&nbsp; |&nbsp; |
| &nbsp; |&nbsp; |2181 |&nbsp; |port Hello que les clients utilisent tooconnect tooZooKeeper |

### <a name="kafka-ports"></a>Ports Kafka

| Service | Nœuds | Port | Protocole | Description |
| --- | --- | --- | --- | --- |
| Service Broker |Nœuds de travail |9092 |[Protocole Kafka](http://kafka.apache.org/protocol.html) |Utilisé pour la communication client |
| &nbsp; |Nœuds Zookeeper |2181 |&nbsp; |port Hello que les clients utilisent tooconnect tooZookeeper |

### <a name="spark-ports"></a>Ports Spark

| Service | Nœuds | Port | Protocole | Chemin d'accès de l'URL | Description |
| --- | --- | --- | --- | --- | --- |
| Serveurs Thrift Spark |Nœuds principaux |10002 |Thrift | &nbsp; | Service pour la connexion tooSpark SQL (Thrift/JDBC) |
| Serveur Livy | Nœuds principaux | 8998 | HTTP | /batches | Service d’exécution des instructions, des travaux et des applications |

Exemples :

* Livy : `curl "http://10.0.0.11:8998/batches"`. Dans cet exemple, `10.0.0.11` est l’adresse IP de hello du nœud principal hello qui héberge le service de Livy de hello.
