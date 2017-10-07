---
title: "données de capteur aaaProcess véhicule avec Apache Storm sur HDInsight | Documents Microsoft"
description: "Découvrez comment les données du capteur de véhicule tooprocess de concentrateurs d’événements à l’aide d’Apache Storm sur HDInsight. Ajouter des données de modèle à partir de la base de données Azure Cosmos et stocker la sortie toostorage."
services: hdinsight,documentdb,notification-hubs
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 78980635-8bef-4c33-96c3-fae50e932e31
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/03/2017
ms.author: larryfr
ms.openlocfilehash: 8f7b1dbb9072e095ea32160bb731bedd071288af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="process-vehicle-sensor-data-from-azure-event-hubs-using-apache-storm-on-hdinsight"></a>Traitement des données de capteur de véhicules à partir d’Azure Event Hubs à l’aide d’Apache Storm dans HDInsight

Découvrez comment les données du capteur de véhicule tooprocess de concentrateurs d’événements Azure à l’aide d’Apache Storm sur HDInsight. Cet exemple lit les données de capteur d’Azure Event Hubs, enrichit les données de hello en faisant référence à des données stockées dans la base de données Azure Cosmos. les données de salutation sont stockées dans le stockage Azure à l’aide de hello système de fichier Hadoop (HDFS).

![HDInsight et hello diagramme d’architecture Internet of Things (IoT)](./media/hdinsight-storm-iot-eventhub-documentdb/iot.png)

## <a name="overview"></a>Vue d'ensemble

Ajout des capteurs toovehicles vous permet de problèmes d’équipement toopredict basées sur les tendances des données historiques. Il vous permet également de vous toomake améliorations apportées à des versions toofuture basées sur l’analyse du modèle d’utilisation. Vous devez être en mesure de tooquickly et charger efficacement des données de hello de tous les véhicules dans Hadoop avant le traitement de MapReduce peut se produire. En outre, vous pouvez d’analyse toodo des chemins d’accès de défaillance critique (température du moteur, freins, etc.) en temps réel.

Les concentrateurs d’événements Azure repose volume massives de hello toohandle des données générées par les capteurs. Apache Storm peut être utilisé tooload et traiter les données hello avant de les stocker dans HDFS.

## <a name="solution"></a>Solution

Les données de télémétrie concernant la température du moteur, la température ambiante et la vitesse du véhicule sont enregistrées par des capteurs. Données sont ensuite envoyées concentrateurs tooEvent ainsi que Identification nombre du véhicule la voiture hello et un horodatage. Une topologie Storm en cours d’exécution sur un Apache Storm sur le cluster HDInsight à partir de là, lit les données de hello, traite et stocke dans HDFS.

Au cours du traitement, hello VIN est tooretrieve utilisé les informations de modèle de base de données Cosmos. Ces données sont ajoutées des flux de données toohello avant d’être stockée.

composants Hello utilisés Bonjour Storm topologie sont :

* **EventHubSpout** : lit les données à partir d'Azure Event Hubs
* **TypeConversionBolt** -convertit hello chaîne JSON à partir de concentrateurs d’événements dans un tuple contenant hello capteur données suivantes :
    * Engine temperature
    * Température ambiante
    * Vitesse
    * VIN
    * Timestamp
* **DataReferencBolt** -recherche de base de données Cosmos à l’aide de hello VIN modèle du véhicule hello
* **WasbStoreBolt** -magasins hello données tooHDFS (stockage Azure)

Hello suivant l’image est un diagramme de cette solution :

![topologie Storm](./media/hdinsight-storm-iot-eventhub-documentdb/iottopology.png)

## <a name="implementation"></a>Implémentation

Complète, solution automatisée pour ce scénario est disponible dans le cadre de hello [HDInsight-Storm-exemples](https://github.com/hdinsight/hdinsight-storm-examples) référentiel sur GitHub. toouse cet exemple, suivez les étapes hello Bonjour [IoTExample README. MD](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/IotExample/README.md).

## <a name="next-steps"></a>Étapes suivantes

Pour plus d'exemples de topologies Storm, consultez les [exemples de topologies pour Storm dans HDInsight](hdinsight-storm-example-topology.md).

