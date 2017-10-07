---
title: "topologies d’Apache Storm aaaExample sur HDInsight | Documents Microsoft"
description: "Liste d’exemples de topologies Storm créées et testées avec Apache Storm sur HDInsight, y compris les topologies C# et Java de base et l’utilisation d’Event Hubs."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: f9b1bdff-5928-4705-a76d-52fd200917cb
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/07/2017
ms.author: larryfr
ms.openlocfilehash: b20299112f6489b7c99360f0a539fc732703c64a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="example-storm-topologies-and-components-for-apache-storm-on-hdinsight"></a>Exemples de topologies et de composants Storm pour Apache Storm sur HDInsight

Hello Voici une liste d’exemples créés et gérés par Microsoft pour une utilisation avec Apache Storm sur HDInsight. Ces exemples traitent d’un ensemble de rubriques, de création de base c# et Java topologies tooworking avec des services Azure tels que des concentrateurs d’événements, Cosmos DB, Power BI, base de données SQL, HBase sur HDInsight et le stockage Azure. Certains exemples montrent également comment toowork non-Azure, ou même non Microsoft sur les technologies, telles que SignalR et Socket.IO.

| Description | Illustre le | Langage/structure |
|:--- |:--- |:--- |
| [Écrire tooAzure Data Lake Store à partir d’Apache Storm](hdinsight-storm-write-data-lake-store.md) |L’écriture tooAzure Data Lake Store |Java |
| [Source de spout et bolt Event Hub](https://github.com/apache/storm/tree/master/external/storm-eventhubs) |Source pour hello bec de concentrateur d’événements et éclair |Java |
| [Développement de topologies basées sur Java pour Apache Storm dans HDInsight][5797064f] |Maven |Java |
| [Développement de topologies C# pour Apache Storm dans HDInsight à l’aide de Visual Studio][16fce2d1] |Outils HDInsight pour Visual Studio |C#, Java |
| [Création de plusieurs flux de données dans une topologie C# Storm][ec5a4064] |Plusieurs flux de données |C# |
| [Traitement des événements Azure Event Hubs avec Storm sur HDInsight (C#)][844d1d81] |Event Hubs |C# et Java |
| [Traitement des événements Azure Event Hubs avec Storm sur HDInsight (Java)](hdinsight-storm-develop-java-event-hub-topology.md) |Event Hubs |Java |
| [Utiliser les données de toovisualize Power Bi à partir d’une topologie Storm][94d15238] |Power BI |C# |
| [Analyse des données de capteur avec Storm et HBase dans HDInsight][ab894747] |Event Hubs, HBase, Socket.IO, tableau de bord web |C#, Java, JavaScript, HTML |
| [Traitement des données de capteur de véhicule à partir d’Event Hubs à l’aide de Storm dans HDInsight][246ee964] |Event Hubs, Cosmos DB, Azure Storage Blob (WASB) |C#, Java |
| [Extraction, transformation et chargement (ETL) à partir d’Azure Event Hubs tooHBase, à l’aide de Storm sur HDInsight][b4b68194] |Event Hubs, HBase |C# |
| [Modèle de projet de topologie Storm C# pour l’utilisation des services Azure à partir de Storm sur HDInsight][ce0c02a2] |Event Hubs, Cosmos DB, SQL Database, HBase, SignalR |C#, Java |
| [Tests d’extensibilité pour la lecture à partir d’Azure Event Hubs à l’aide de Storm sur HDInsight][d6c540e3] |Débit des messages, Event Hubs, SQL Database |C#, Java |
| [Corrélation des événements à l’aide de Storm et HBase sur HDInsight](hdinsight-storm-correlation-topology.md) |HBase |C# |
| [Utilisation de Python avec Storm sur HDInsight](hdinsight-storm-develop-python-topology.md) |Composants de Python avec une topologie Flux |Python |
| [Utilisation de Kafka avec Storm sur HDInsight](hdinsight-apache-storm-with-kafka.md) | Lecture d’Apache Storm et l’écriture de tooApache Kafka | Java |

### <a name="next-steps"></a>Étapes suivantes

* [Prise en main d’Apache Storm sur HDInsight][2b8c3488]
* [Découvrez comment toodeploy et gérer des topologies Storm avec Storm sur HDInsight][6eb0d3b8]

[2b8c3488]: hdinsight-apache-storm-tutorial-get-started-linux.md "Découvrez comment toocreate une tempête sur cluster HDInsight et utilisez hello toodeploy exemples de topologies de tableau de bord Storm."
[6eb0d3b8]: hdinsight-storm-deploy-monitor-topology.md "Découvrez comment toodeploy et gérer des topologies à l’aide de hello Storm tableau de bord web et l’interface utilisateur Storm ou hello HDInsight Tools pour Visual Studio."
[16fce2d1]: hdinsight-storm-develop-csharp-visual-studio-topology.md "Découvrez comment toocreate les topologies Storm c# à l’aide de hello outils HDInsight pour Visual Studio."
[5797064f]: hdinsight-storm-develop-java-topology.md "Découvrez comment les topologies Storm toocreate dans Java, à l’aide de Maven, en créant une topologie de base wordcount."
[94d15238]: hdinsight-storm-power-bi-topology.md "Montre comment toowrite données tooPower BI à partir d’une topologie c#, puis créer un graphique et un tableau de bord à partir des données de hello."
[ec5a4064]: https://github.com/Blackmist/csharp-storm-example "Illustre une topologie Storm simple qui effectue un comptage de mots, implémentée en C#. Il montre également comment toocreate plusieurs flux de données dans une topologie c#."
[844d1d81]: hdinsight-storm-develop-csharp-event-hub-topology.md "Découvrez comment tooread et écrire les données à partir d’Azure Event Hubs avec Storm sur HDInsight."
[ab894747]: hdinsight-storm-sensor-data-analysis.md "Découvrez comment toouse Apache Storm sur les données de capteur tooprocess HDInsight à partir d’Azure Event Hubs, visualiser à l’aide de D3.js et (facultativement), stockez-le tooHBase."
[246ee964]: https://github.com/hdinsight/hdinsight-storm-examples/blob/master/IotExample/README.md "Découvrez comment toouse une tempête topologie tooread les messages à partir d’Azure Event Hubs, lisez les documents à partir de la base de données Azure Cosmos pour faire référence à des données et enregistrer des données tooAzure stockage."
[d6c540e3]: https://github.com/hdinsight/hdinsight-storm-examples/blob/master/EventCountExample "Plusieurs topologies toodemonstrate débit lors de la lecture à partir d’Azure Event Hubs et le stockage tooSQL base de données à l’aide d’Apache Storm sur HDInsight."
[b4b68194]: https://github.com/hdinsight/hdinsight-storm-examples/blob/master/RealTimeETLExample "Découvrez comment tooread des données à partir d’Azure Event Hubs, agréger et transformer hello des données, puis stocker tooHBase sur HDInsight."
[ce0c02a2]: https://github.com/hdinsight/hdinsight-storm-examples/tree/master/templates/HDInsightStormExamples "Ce projet contient des modèles pour les topologies, boulons et becs verseurs toointeract avec différents services Azure comme base de données SQL, Cosmos DB et concentrateurs d’événements."

