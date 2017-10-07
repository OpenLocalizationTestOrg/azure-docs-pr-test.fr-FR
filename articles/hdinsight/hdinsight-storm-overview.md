---
title: aaaWhat est Apache Storm - Azure HDInsight | Documents Microsoft
description: "Apache Storm vous permet de tooprocess des flux de données en temps réel. Azure HDInsight vous permet de tooeasily créer des clusters de Storm sur hello cloud Azure. Avec Visual Studio, vous pouvez créer des solutions Storm à l’aide de c# et ensuite déployer tooyour que des clusters HDInsight Storm."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
keywords: "cas d’utilisation d’apache storm,cluster storm,présentation d’apache storm"
ms.assetid: 72d54080-1e48-4a5e-aa50-cce4ffc85077
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/03/2017
ms.author: larryfr
ms.openlocfilehash: 6c6b2925ef3e5666dfecc3fb3c835bb362902c51
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-apache-storm-on-azure-hdinsight"></a>Présentation d’Apache Storm sur Azure HDInsight

[Apache Storm](http://storm.apache.org/) est un système de calcul distribué, à tolérance de panne et open source. Vous pouvez utiliser des flux de tooprocess tempête de données en temps réel avec Hadoop. Storm peut proposent également garantit le traitement des données, avec hello capacité tooreplay les données qui n’a pas été traitement hello première fois.

Storm sur HDInsight fournit hello avantages clés suivants :

* Il s’exécute en tant que service géré, avec un contrat de niveau de service garantissant un taux de disponibilité de 99,9 pour cent.

* Il prend en charge une personnalisation aisée via l’exécution de scripts sur un cluster Storm pendant ou après la création. Pour en savoir plus, voir [Personnaliser des clusters HDInsight à l’aide d’une d’action de script](hdinsight-hadoop-customize-cluster-linux.md).

* Utilise plusieurs langues. Vous pouvez écrire des composants de Storm en langage hello de votre choix, comme Java, c# et Python.

    * Visual Studio intègre de HDInsight pour le développement de hello, la gestion et la surveillance des topologies de c#. Pour plus d’informations, consultez [topologies c# Storm développer avec hello outils HDInsight pour Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).

    * Interface de Trident Java hello prend en charge. Vous pouvez créer des topologies Storm qui prennent en charge « exactement une fois » le traitement des messages, la persistance de magasin de données « transactionnels » et un ensemble d’opérations d’analyses courantes de flux de données.

*  Montée et descente en puissance facile des clusters Storm. Vous pouvez ajouter ou supprimer des nœuds de travail avec aucun impact toorunning tempête de topologies.

* S’intègre à hello suivant des services Azure :

    * Hubs d'événements Azure

    * Réseau virtuel Azure

    * Base de données SQL Azure

    * Azure Storage

    * Azure Cosmos DB

* Associe les fonctions hello plusieurs clusters HDInsight en toute sécurité à l’aide de réseau virtuel. Vous pouvez créer des pipelines analytiques qui utilisent des clusters Storm, Kafka, Spark, HBase ou Hadoop.

Pour obtenir la liste des entreprises qui utilisent Apache Storm pour leurs solutions d’analyse en temps réel, voir [Entreprises utilisant Apache Storm](https://storm.apache.org/documentation/Powered-By.html).

tooget démarré à l’aide de Storm, consultez [prise en main Storm sur HDInsight][gettingstarted].

## <a name="how-does-storm-work"></a>Fonctionnement de Storm

Storm exécute topologies au lieu de hello travaux MapReduce que vous connaissez peut-être. Les topologies Storm sont constituées de plusieurs composants organisés dans un graphe orienté acyclique (DAG). Flux de données entre les composants hello dans le graphique de hello. Chaque composant consomme un ou plusieurs flux de données, et peut émettre éventuellement un ou plusieurs flux. Hello suivant le diagramme illustre le flux des données entre les composants dans une topologie de statistiques de base :

![Exemple d’organisation des composants dans une topologie Storm](./media/hdinsight-storm-overview/example-apache-storm-topology-diagram.png)

* Les composants Spout importent les données dans une topologie. Ils émettent un ou plusieurs flux dans une topologie de hello.

* Les composants Bolt utilisent les flux émis à partir des spouts ou des autres bolts. Boulons peuvent éventuellement émettre des flux de données dans une topologie de hello. Boulons sont également responsables de l’écriture de services tooexternal de données ou de stockage, telles que HDFS, Kafka ou HBase.

## <a name="ease-of-creation"></a>Facilité de création

Vous pouvez approvisionner un nouveau cluster Storm sur HDInsight en quelques minutes. Pour plus d’informations sur la création d’un cluster Storm, consultez [Prise en main de Storm sur un cluster HDInsight](hdinsight-apache-storm-tutorial-get-started-linux.md).

## <a name="ease-of-use"></a>Simplicité d'utilisation

* __Secure Shell (SSH) connectivité__: vous pouvez accéder à des nœuds de tête hello de votre cluster Storm sur hello Internet à l’aide de SSH. Vous pouvez exécuter des commandes directement sur votre cluster à l’aide de SSH.

  Pour en savoir plus, voir [Utilisation de SSH avec Hadoop Linux sur HDInsight depuis Linux, Unix ou OS X](hdinsight-hadoop-linux-use-ssh-unix.md).

* __Web connectivité__: HDInsight tous les clusters fournissent hello Ambari web l’interface utilisateur. Vous pouvez facilement surveiller, configurer et gérer les services sur votre cluster à l’aide de l’interface utilisateur web de Ambari hello. Les clusters de Storm offrent également hello Storm UI. Vous pouvez surveiller et gérer des topologies de Storm en cours d’exécution à partir de votre navigateur à l’aide de hello Storm UI.

  Pour plus d’informations, consultez hello [HDInsight de gérer à l’aide de hello l’interface utilisateur Web de Ambari](hdinsight-hadoop-manage-ambari.md) et [analyse et de gérer à l’aide de hello Storm UI](hdinsight-storm-deploy-monitor-topology-linux.md#monitor-and-manage-storm-ui) documents.

* __Azure PowerShell et CLI d’Azure__: PowerShell et l’interface CLI fournissent des utilitaires de ligne de commande que vous pouvez utiliser à partir de votre toowork de système de client avec HDInsight et d’autres services Azure.

* __Intégration de Visual Studio__: Azure Data Lake Tools pour Visual Studio incluent des modèles de projet pour la création de topologies de Storm c# à l’aide hello SCP.Net framework. Outils de LAC de données fournissent également des outils toodeploy, surveiller et gérer des solutions avec Storm sur HDInsight.

  Pour plus d’informations, consultez [topologies c# Storm développer avec hello outils HDInsight pour Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).

## <a name="integration-with-other-azure-services"></a>Intégration avec d’autres services Azure

* __Azure Data Lake Store__ : pour obtenir un exemple d’utilisation de Data Lake Store avec un cluster Storm, voir [Utilisation d’Azure Data Lake Store avec Apache Storm sur HDInsight](hdinsight-storm-write-data-lake-store.md).

* __Concentrateurs d’événements__: pour obtenir un exemple d’utilisation des concentrateurs d’événements avec un cluster Storm, consultez hello suivant des documents :

    * [Développer une topologie basée sur Java pour Storm sur HDInsight](hdinsight-storm-develop-java-topology.md)

    * [Traiter des événements issus d’Azure Event Hubs avec Storm sur HDInsight (C#)](hdinsight-storm-develop-csharp-event-hub-topology.md)

* __Base de données SQL__, __Cosmos DB__, __concentrateurs d’événements__, et __HBase__: exemples de modèles sont inclus dans hello Data Lake Tools pour Visual Studio. Pour plus d’informations, voir [Développement de topologies C# pour Apache Storm sur HDInsight à l’aide des outils Hadoop pour Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).

## <a name="reliability"></a>Fiabilité

Apache Storm garantit que chaque message entrant est toujours entièrement traité, même lorsque l’analyse des données hello est réparti sur des centaines de nœuds.

nœud de Nimbus Hello fournit toohello de fonctionnalités similaires Hadoop JobTracker, et il affecte aux tâches tooother des nœuds dans un cluster via soigneur. Les nœuds soigneur une coordination pour un cluster et facilitent la communication entre Nimbus et hello processus superviseur sur les nœuds de travail hello. Si un nœud de traitement s’arrête, nœud de Nimbus hello est informé et il affecte la tâche hello et nœud tooanother de données associées.

Hello est par défaut pour les clusters Apache Storm toohave qu’un seul nœud de Nimbus. Storm sur HDInsight fournit deux nœuds Nimbus. Si le nœud principal de hello échoue, cluster Storm de hello bascule le nœud secondaire de toohello alors que le nœud principal de hello est récupérée. Hello diagramme suivant illustre la configuration du flux de tâches hello pour Storm sur HDInsight :

![Schéma de Nimbus, de Zookeeper et de Superviseur](./media/hdinsight-storm-overview/nimbus.png)

## <a name="scale"></a>Mettre à l'échelle

Les clusters HDInsight peuvent être mis à l’échelle de façon dynamique en ajoutant ou en supprimant des nœuds Worker. Cette opération peut être effectuée lors du traitement des données.

> [!IMPORTANT]
> avantage tootake de nouveaux nœuds ajoutés via la mise à l’échelle, vous devez les topologies de Storm toorebalance démarrés avant que la taille de cluster hello a été augmentée.

## <a name="support"></a>Support

Storm sur HDInsight bénéficie d’une assistance professionnelle continue. Storm sur HDInsight possède également un contrat SLA garantissant un taux de disponibilité de 99,9 pour cent. Cela signifie que nous garantissons qu’un cluster Storm dispose d’au moins 99,9 % du temps de hello une connectivité externe.

Pour plus d’informations, consultez le [support Azure](https://azure.microsoft.com/support/options/).

## <a name="apache-storm-use-cases"></a>Cas d’utilisation d’Apache Storm

Hello Voici quelques scénarios courants pour lequel vous pouvez utiliser Storm sur HDInsight :

* Internet des objets (IoT)
* Détection des fraudes
* Analyse des réseaux sociaux
* Extraction, transformation et chargement (ETL)
* Analyse du réseau
* Search
* Engagement mobile

Pour plus d’informations sur les scénarios réels, consultez hello [comment les sociétés utilisent Storm](https://storm.apache.org/documentation/Powered-By.html) document.

## <a name="development"></a>Développement

Les développeurs .NET peuvent concevoir et implémenter des topologies en C# à l’aide de Data Lake Tools pour Visual Studio. Vous pouvez également créer des topologies hybrides qui utilisent des composants Java et C#.

Pour plus d‘informations, consultez la rubrique [Développer des topologies C# pour Storm sur HDInsight en utilisant Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).

Vous pouvez également développer des solutions de Java à l’aide de hello IDE de votre choix. Pour plus d’informations, voir [Développer des topologies Java pour Storm sur HDInsight](hdinsight-storm-develop-java-topology.md).

Python peut également être utilisé toodevelop Storm composants. Pour plus d’informations, voir [Développer des topologies Storm à l’aide de Python sur HDInsight](hdinsight-storm-develop-python-topology.md).

## <a name="common-development-patterns"></a>Modèles de développement courants

### <a name="guaranteed-message-processing"></a>Traitement de message garanti

Apache Storm peut fournir différents niveaux de traitement de message garanti. Par exemple, une application Storm de base peut garantir un traitement « Une fois au minimum », tandis que Trident peut garantir un traitement « Exactement une fois ».

Pour plus d‘informations, consultez la rubrique [Garanties sur le traitement des données](https://storm.apache.org/about/guarantees-data-processing.html) sur le site apache.org.

### <a name="ibasicbolt"></a>IBasicBolt

Hello motif de la lecture d’un tuple d’entrée, l’émission de zéro ou plusieurs tuples, et puis acking hello tuple d’entrée immédiatement à la fin de hello Hello exécuter la méthode est courant. Storm fournit hello [IBasicBolt](https://storm.apache.org/releases/1.0.3/javadocs/org/apache/storm/topology/IBasicBolt.html) interface tooautomate ce modèle.

### <a name="joins"></a>Jointures

La façon dont les flux de données sont joints varie entre les applications. Vous pouvez, par exemple, joindre chaque tuple provenant de plusieurs flux dans un nouveau flux, ou joindre uniquement des lots de tuples pour une fenêtre spécifique. Dans les deux cas, la jonction peut être effectuée à l’aide de [fieldsGrouping](http://storm.apache.org/releases/current/javadocs/org/apache/storm/topology/InputDeclarer.html#fieldsGrouping-java.lang.String-org.apache.storm.tuple.Fields-). Champ de regroupement est un moyen de définir la façon dont les tuples sont routés toobolts.

Bonjour Java l’exemple suivant, fieldsGrouping est utilisé tooroute tuples qui proviennent de composants « 1 », « 2 » et « 3 » toohello MyJoiner éclair :

    builder.setBolt("join", new MyJoiner(), parallelism) .fieldsGrouping("1", new Fields("joinfield1", "joinfield2")) .fieldsGrouping("2", new Fields("joinfield1", "joinfield2")) .fieldsGrouping("3", new Fields("joinfield1", "joinfield2"));

### <a name="batches"></a>Lots

Apache Storm fournit un mécanisme de minutage interne appelé « tuple de graduation ». Vous pouvez définir la fréquence à laquelle un tuple de graduation est émis dans votre topologie.

Pour obtenir un exemple d’utilisation d’un tick tuple à partir d’un composant C#, consultez le fichier [PartialBoltCount.cs](https://github.com/hdinsight/hdinsight-storm-examples/blob/3b2c960549cac122e8874931df4801f0934fffa7/EventCountExample/EventCountTopology/src/main/java/com/microsoft/hdinsight/storm/examples/PartialCountBolt.java).

### <a name="caches"></a>Caches

La mise en cache en mémoire est souvent utilisée pour accélérer le traitement, car elle garde en mémoire les éléments les plus utilisés. Dans la mesure où une topologie est distribuée entre plusieurs nœuds et plusieurs processus au sein de chaque nœud, vous devez envisager d’utiliser [fieldsGrouping](http://storm.apache.org/releases/current/javadocs/org/apache/storm/topology/InputDeclarer.html#fieldsGrouping-java.lang.String-org.apache.storm.tuple.Fields-). Utilisez `fieldsGrouping` tooensure que les tuples contenant les champs de hello sont utilisées pour la recherche de cache sont toujours toohello routé même processus. Cette fonctionnalité de groupage permet d’éviter la duplication des entrées de cache à travers les processus.

### <a name="stream-top-n"></a>Diffuser les N premiers

Lorsque votre topologie dépend de calculer une valeur N premiers, calculer la valeur de N premiers de hello en parallèle. Ensuite, fusionnez hello la sortie à partir de ces calculs en une valeur globale. Cette opération peut être effectuée à l’aide de [fieldsGrouping](http://storm.apache.org/releases/current/javadocs/org/apache/storm/topology/InputDeclarer.html#fieldsGrouping-java.lang.String-org.apache.storm.tuple.Fields-) tooroute par champ pour un traitement parallèle. Vous pouvez ensuite router éclair tooa globalement déterminant la valeur des N premières hello.

Pour obtenir un exemple de calcul d’une valeur N premiers, consultez hello [RollingTopWords](https://github.com/apache/storm/blob/master/examples/storm-starter/src/jvm/org/apache/storm/starter/RollingTopWords.java) exemple.

## <a name="logging"></a>Journalisation

Storm utilise Apache Log4j toolog informations. Par défaut, une grande quantité de données est connectée, et il peut être difficile toosort via des informations hello. Vous pouvez inclure un fichier de configuration de journalisation dans le cadre de votre comportement de journalisation de toocontrol topologie Storm.

Pour un exemple de topologie qui montre comment tooconfigure journalisation, consultez [basée sur Java de WordCount](hdinsight-storm-develop-java-topology.md) exemple de Storm sur HDInsight.

## <a name="next-steps"></a>Étapes suivantes

En savoir plus sur les solutions d’analyse en temps réel avec Storm sur HDInsight :

* [Prise en main d’Apache Storm sur HDInsight][gettingstarted]
* [Exemples de topologies pour Apache Storm dans HDInsight](hdinsight-storm-example-topology.md)

[stormtrident]: https://storm.apache.org/documentation/Trident-API-Overview.html
[samoa]: http://yahooeng.tumblr.com/post/65453012905/introducing-samoa-an-open-source-platform-for-mining
[apachetutorial]: https://storm.apache.org/documentation/Tutorial.html
[gettingstarted]: hdinsight-apache-storm-tutorial-get-started-linux.md
