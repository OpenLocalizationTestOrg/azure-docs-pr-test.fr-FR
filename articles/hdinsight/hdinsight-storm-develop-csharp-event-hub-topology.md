---
title: "événements d’aaaProcess de concentrateurs d’événements avec Storm - Azure HDInsight | Documents Microsoft"
description: "Découvrez comment tooprocess des données à partir d’Azure Event Hubs avec une topologie Storm c# créés dans Visual Studio, à l’aide de hello outils HDInsight pour Visual Studio."
services: hdinsight,notification hubs
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 67f9d08c-eea0-401b-952b-db765655dad0
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/03/2017
ms.author: larryfr
ms.openlocfilehash: 30cd910d80eba066f283197bcbbaf11145bc5524
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="process-events-from-azure-event-hubs-with-storm-on-hdinsight-c"></a>Traitement des événements Azure Event Hubs avec Storm sur HDInsight (C#)

Découvrez comment toowork avec des concentrateurs d’événements Azure à partir d’Apache Storm sur HDInsight. Ce document utilise une tempête c# topologie tooread et écrire les données de concentrateurs de Evbent

> [!NOTE]
> Pour obtenir une version Java de ce projet, consultez [Traitement des événements Azure Event Hubs avec Storm sur HDInsight (Java)](hdinsight-storm-develop-java-event-hub-topology.md).

## <a name="scpnet"></a>SCP.NET

étapes Hello dans ce document utilisent SCP.NET, un package NuGet qui la rend facile toocreate c# topologies et les composants pour une utilisation avec Storm sur HDInsight.

> [!IMPORTANT]
> Alors que les étapes hello dans ce document reposent sur un environnement de développement Windows avec Visual Studio, projet compilé de hello peut être soumis tooa Storm sur le cluster HDInsight qui utilise Linux. Seuls les clusters basés sur Linux créés après le 28 octobre 2016 prennent en charge les topologies SCP.NET.

HDInsight 3.4 et topologies de toorun Mono c# utilisation supérieure. exemple Hello utilisé dans ce document fonctionne avec HDInsight 3.6. Si vous prévoyez de créer vos propres solutions .NET pour HDInsight, vérifiez hello [compatibilité Mono](http://www.mono-project.com/docs/about-mono/compatibility/) document pour identifier les éventuelles incompatibilités.

### <a name="cluster-versioning"></a>Contrôle de version de cluster

Hello package NuGet de Microsoft.SCP.Net.SDK vous utilisez pour votre projet doit correspondre au version majeure de hello de Storm installé sur HDInsight. Les versions 3.5 et 3.6 de HDInsight utilisent Storm 1.x. Vous devez donc utiliser la version 1.0.x.x de SCP.NET avec ces clusters.

> [!IMPORTANT]
> exemple Hello dans ce document attend un 3.5 HDInsight ou cluster 3.6.
>
> Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure. Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

Les topologies C# doivent également cibler la version 4.5 de .NET.

## <a name="how-toowork-with-event-hubs"></a>Comment toowork avec des concentrateurs d’événements

Microsoft fournit un ensemble de composants Java qui peuvent être toocommunicate utilisé avec les concentrateurs d’événements à partir d’une topologie Storm. Vous pouvez trouver hello Java archives (JAR) fichier qui contient une version compatible de HDInsight 3.6 de ces composants à [https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar](https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar).

> [!IMPORTANT]
> Alors que les composants de hello sont écrits en Java, vous pouvez les utiliser facilement à partir d’une topologie c#.

Hello, suivant les composants est utilisé dans cet exemple :

* __EventHubSpout__ : lit les données à partir d’Event Hubs.
* __EventHubBolt__: écrit les données tooEvent concentrateurs.
* __EventHubSpoutConfig__: utilisé tooconfigure EventHubSpout.
* __EventHubBoltConfig__: utilisé tooconfigure EventHubBolt.

### <a name="example-spout-usage"></a>Exemple d’utilisation du spout

SCP.NET fournit des méthodes pour l’ajout d’une topologie de tooyour EventHubSpout. Ces méthodes rendent plus facile tooadd un bec que l’utilisation des méthodes génériques de hello pour ajouter un composant Java. Hello exemple suivant montre comment un bec à l’aide de toocreate hello __SetEventHubSpout__ et **EventHubSpoutConfig** méthodes fournies par SCP.NET :

```csharp
 topologyBuilder.SetEventHubSpout(
    "EventHubSpout",
    new EventHubSpoutConfig(
        ConfigurationManager.AppSettings["EventHubSharedAccessKeyName"],
        ConfigurationManager.AppSettings["EventHubSharedAccessKey"],
        ConfigurationManager.AppSettings["EventHubNamespace"],
        ConfigurationManager.AppSettings["EventHubEntityPath"],
        eventHubPartitions),
    eventHubPartitions);
```

Hello précédent exemple crée un nouveau composant bec nommé __EventHubSpout__et il configure toocommunicate avec un concentrateur d’événements. indicateur de parallélisme Hello pour le composant de hello a la valeur nombre toohello de partitions dans le concentrateur d’événements hello. Ce paramètre permet de Storm toocreate une instance du composant hello pour chaque partition.

### <a name="example-bolt-usage"></a>Exemple d’utilisation du bolt

Hello d’utilisation **JavaComponmentConstructor** méthode toocreate une instance d’éclair de hello. Hello exemple suivant montre comment toocreate et configurer une nouvelle instance de hello **EventHubBolt**:

```csharp
// Java construcvtor for hello Event Hub Bolt
JavaComponentConstructor constructor = JavaComponentConstructor.CreateFromClojureExpr(
    String.Format(@"(org.apache.storm.eventhubs.bolt.EventHubBolt. (org.apache.storm.eventhubs.bolt.EventHubBoltConfig. " +
        @"""{0}"" ""{1}"" ""{2}"" ""{3}"" ""{4}"" {5}))",
        ConfigurationManager.AppSettings["EventHubPolicyName"],
        ConfigurationManager.AppSettings["EventHubPolicyKey"],
        ConfigurationManager.AppSettings["EventHubNamespace"],
        "servicebus.windows.net",
        ConfigurationManager.AppSettings["EventHubName"],
        "true"));

// Set hello bolt toosubscribe toodata from hello spout
topologyBuilder.SetJavaBolt(
    "eventhubbolt",
    constructor,
    partitionCount)
        .shuffleGrouping("Spout");
```

> [!NOTE]
> Cet exemple utilise une expression Clojure transmise sous forme de chaîne au lieu d’utiliser **JavaComponentConstructor** toocreate un **EventHubBoltConfig**, comme l’exemple de bec hello a fait. Les deux méthodes fonctionnent. Utiliser la méthode hello qui vous semble la meilleure tooyou.

## <a name="download-hello-completed-project"></a>Télécharger le projet de hello terminée

Vous pouvez télécharger une version complète du projet hello créée dans ce didacticiel à partir de [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub). Toutefois, vous devez toujours les paramètres de configuration tooprovide en suivant les étapes de hello dans ce didacticiel.

### <a name="prerequisites"></a>Composants requis

* Un cluster [Apache Storm sur HDInsight version 3.5 ou 3.6](hdinsight-apache-storm-tutorial-get-started.md).

    > [!WARNING]
    > exemple Hello utilisé dans ce document requiert Storm sur HDInsight version 3.5 ou 3.6. Cela ne fonctionne pas avec les versions antérieures de HDInsight, en raison de changements de nom de classe toobreaking. Pour une version de cet exemple fonctionnant avec les anciens clusters, consultez [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub/releases).

* Un [concentrateur d’événements Azure](../event-hubs/event-hubs-csharp-ephcs-getstarted.md).

* Hello [Azure .NET SDK](http://azure.microsoft.com/downloads/).

* Hello [outils HDInsight pour Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).

* Java JDK 1.8 ou version ultérieure sur votre environnement de développement. Les téléchargements JDK sont disponibles dans [Oracle](http://www.oracle.com/technetwork/java/javase/downloads/index.html).

  * Hello **JAVA_HOME** environnement variable doit toohello de point de répertoire qui contient Java.
  * Hello **%JAVA_HOME%/bin** répertoire doit être dans le chemin d’accès hello.

## <a name="download-hello-event-hubs-components"></a>Télécharger les composants de concentrateurs d’événements hello

Téléchargement hello concentrateurs d’événements bec et composant à partir de boulon [https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar](https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar).

Créez un répertoire nommé `eventhubspout`et enregistrez le fichier de hello dans l’annuaire de hello.

## <a name="configure-event-hubs"></a>Configurer les hubs d’événement

Concentrateurs d’événements est la source de données de hello pour cet exemple. Utilisez les informations de hello de section de « Créer un concentrateur d’événements » hello de [prise en main les concentrateurs d’événements](../event-hubs/event-hubs-csharp-ephcs-getstarted.md).

1. Après avoir créé un concentrateur d’événements hello, afficher hello **EventHub** panneau Bonjour Azure portail, puis sélectionnez **les stratégies d’accès partagé**. Sélectionnez **+ ajouter** hello tooadd suivant des stratégies :

   | Nom | Autorisations |
   | --- | --- |
   | writer |Envoyer |
   | reader |Écouter |

    ![Capture d’écran de la fenêtre de stratégies d’accès partagé](./media/hdinsight-storm-develop-csharp-event-hub-topology/sas.png)

2. Sélectionnez hello **lecteur** et **writer** stratégies. Copiez et enregistrez la valeur de clé primaire hello pour les deux stratégies, car ces valeurs sont utilisées ultérieurement.

## <a name="configure-hello-eventhubwriter"></a>Configurer hello EventHubWriter

1. Si vous n’avez pas déjà installé version la plus récente des outils de HDInsight hello hello pour Visual Studio, consultez [prise en main à l’aide des outils HDInsight pour Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).

2. Télécharger à partir de solution hello [eventhub-storm-hybride](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub).

3. Bonjour **EventHubWriter** projet, ouvrez hello **App.config** fichier. Utilisez hello des informations à partir du concentrateur d’événements hello que vous avez configuré toofill antérieure dans la valeur hello pour hello suivant clés :

   | Clé | Valeur |
   | --- | --- |
   | EventHubPolicyName |enregistreur (si vous avez utilisé un autre nom pour la stratégie hello avec *envoyer* autorisation, utilisez-le à la place.) |
   | EventHubPolicyKey |clé Hello pour la stratégie de writer hello. |
   | eventHubNamespace |espace de noms Hello qui contient votre concentrateur d’événements. |
   | eventHubName |Le nom de votre concentrateur d’événements. |
   | EventHubPartitionCount |nombre de Hello de partitions dans votre concentrateur d’événements. |

4. Enregistrez et fermez hello **App.config** fichier.

## <a name="configure-hello-eventhubreader"></a>Configurer hello EventHubReader

1. Ouvrez hello **EventHubReader** projet.

2. Ouvrez hello **App.config** fichier hello **EventHubReader**. Utilisez hello des informations à partir du concentrateur d’événements hello que vous avez configuré toofill antérieure dans la valeur hello pour hello suivant clés :

   | Clé | Valeur |
   | --- | --- |
   | EventHubPolicyName |lecteur (si vous avez utilisé un autre nom pour la stratégie hello avec *écouter* autorisation, utilisez-le à la place.) |
   | EventHubPolicyKey |clé Hello pour la stratégie de lecteur hello. |
   | eventHubNamespace |espace de noms Hello qui contient votre concentrateur d’événements. |
   | eventHubName |Le nom de votre concentrateur d’événements. |
   | EventHubPartitionCount |nombre de Hello de partitions dans votre concentrateur d’événements. |

3. Enregistrez et fermez hello **App.config** fichier.

## <a name="deploy-hello-topologies"></a>Déployer des topologies de hello

1. À partir de **l’Explorateur de solutions**, avec le bouton hello **EventHubReader** le projet, puis sélectionnez **envoyer tooStorm sur HDInsight**.

    ![Capture d’écran d’Explorateur de solutions, avec tooStorm envoyer sur HDInsight mis en surbrillance](./media/hdinsight-storm-develop-csharp-event-hub-topology/submittostorm.png)

2. Sur hello **soumettre une topologie** boîte de dialogue, sélectionnez votre **Cluster Storm**. Développez **des Configurations supplémentaires**, sélectionnez **chemins d’accès de Java**, sélectionnez **...** et sélectionnez hello répertoire qui contient le fichier JAR hello que vous avez téléchargé précédemment. Pour finir, cliquez sur **Envoyer**.

    ![Capture d’écran de la boîte de dialogue Envoyer la topologie](./media/hdinsight-storm-develop-csharp-event-hub-topology/submit.png)

3. Lors de la topologie de hello a été envoyée, hello **Storm Topologies visionneuse** s’affiche. tooview plus d’informations sur la topologie de hello, sélectionnez hello **EventHubReader** topologie dans le volet gauche de hello.

    ![Capture d’écran de la visionneuse de topologies Storm](./media/hdinsight-storm-develop-csharp-event-hub-topology/topologyviewer.png)

4. À partir de **l’Explorateur de solutions**, avec le bouton hello **EventHubWriter** le projet, puis sélectionnez **envoyer tooStorm sur HDInsight**.

5. Sur hello **soumettre une topologie** boîte de dialogue, sélectionnez votre **Cluster Storm**. Développez **des Configurations supplémentaires**, sélectionnez **chemins d’accès de Java**, sélectionnez **...** , et le répertoire hello select qui contient le fichier JAR hello que vous avez téléchargé précédemment. Pour finir, cliquez sur **Envoyer**.

6. Lors de la topologie de hello a été envoyée, actualisez la liste de topologie de hello Bonjour **Storm Topologies visionneuse** tooverify les deux topologies sont en cours d’exécution sur le cluster de hello.

7. Dans **Storm Topologies visionneuse**, sélectionnez hello **EventHubReader** topologie.

8. composant de hello tooopen résumé d’éclair de hello, double-cliquez sur hello **LogBolt** composant dans le diagramme de hello.

9. Bonjour **exécuteurs** , sélectionnez un des liens de hello Bonjour **Port** colonne. Affiche les informations enregistrées par le composant hello. les informations de Hello connecté sont similaires toohello suivant du texte :

        2017-03-02 14:51:29.255 m.s.p.TaskHost [INFO] Received C# STDOUT: 2017-03-02 14:51:29,255 [1] INFO  EventHubReader_LogBolt [(null)] - Received data: {"deviceValue":1830978598,"deviceId":"8566ccbc-034d-45db-883d-d8a31f34068e"}
        2017-03-02 14:51:29.283 m.s.p.TaskHost [INFO] Received C# STDOUT: 2017-03-02 14:51:29,283 [1] INFO  EventHubReader_LogBolt [(null)] - Received data: {"deviceValue":1756413275,"deviceId":"647a5eff-823d-482f-a8b4-b95b35ae570b"}
        2017-03-02 14:51:29.313 m.s.p.TaskHost [INFO] Received C# STDOUT: 2017-03-02 14:51:29,312 [1] INFO  EventHubReader_LogBolt [(null)] - Received data: {"deviceValue":1108478910,"deviceId":"206a68fa-8264-4d61-9100-bfdb68ee8f0a"}

## <a name="stop-hello-topologies"></a>Arrêter les topologies hello

topologies de hello toostop, sélectionnez chaque topologie Bonjour **visionneuse de topologie Storm**, puis cliquez sur **Kill**.

![Capture d’écran de la visionneuse de topologies Storm avec le bouton Supprimer mis en surbrillance](./media/hdinsight-storm-develop-csharp-event-hub-topology/killtopology.png)

## <a name="delete-your-cluster"></a>Supprimer votre cluster

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a>Étapes suivantes

Dans ce document, vous avez appris comment toouse de concentrateurs d’événements Java hello bec et boulon à partir d’un toowork topologie c# avec des données dans Azure Event Hubs. toolearn plus sur la création de topologies de c#, voir hello :

* [Développement de topologies C# pour Apache Storm dans HDInsight à l'aide de Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md)
* [Guide de programmation SCP](hdinsight-storm-scp-programming-guide.md)
* [Exemples de topologies pour Storm dans HDInsight](hdinsight-storm-example-topology.md)
