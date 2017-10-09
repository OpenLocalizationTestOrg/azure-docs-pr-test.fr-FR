---
title: "diffusion en continu d’aaaUse Apache Spark avec des concentrateurs d’événements dans Azure HDInsight | Documents Microsoft"
description: "Générer un exemple de diffusion en continu d’Apache Spark sur toosend données tooAzure concentrateur d’événements de flux et recevoir les événements dans le cluster HDInsight Spark à l’aide d’une application scala."
keywords: diffusion en continu apache spark,diffusion en continu spark, exemple spark,exemple de diffusion en continu apache spark,exemple azure event hubs
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 68894e75-3ffa-47bd-8982-96cdad38b7d0
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: nitinme
ms.openlocfilehash: 10cc5884047b3b8249fe8a8822a16a19780a4af3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="apache-spark-streaming-process-data-from-azure-event-hubs-with-spark-cluster-on-hdinsight"></a>Diffusion en continu Apache Spark : traitement de données d’Azure Event Hubs avec un cluster Spark sur HDInsight

Dans cet article, vous créez un Apache Spark de diffusion en continu d’exemple qui implique hello comme suit :

1. Vous utilisez un message tooingest d’application autonome dans un concentrateur d’événements Azure.

2. Avec deux approches différentes, vous extrayez des messages hello de concentrateur d’événements en temps réel à l’aide d’une application en cours d’exécution dans le cluster Spark sur Azure HDInsight.

3. Génération de diffusion en continu des pipelines analytiques toopersist toodifferent systèmes de stockage ou obtenir des informations à partir des données volée hello.

## <a name="prerequisites"></a>Composants requis

* Un abonnement Azure. Consultez la page [Obtention d’un essai gratuit d’Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).

* Un cluster Apache Spark sur HDInsight. Pour obtenir des instructions, consultez [Création de clusters Apache Spark dans Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).

## <a name="spark-streaming-concepts"></a>Concepts de la diffusion en continu de Spark

Pour obtenir une explication détaillée de la diffusion en continu Spark, voir la [présentation de la diffusion en continu Apache Spark](http://spark.apache.org/docs/latest/streaming-programming-guide.html#overview). HDInsight met hello de cluster même tooa fonctionnalités diffusion en continu Spark sur Azure.  

## <a name="what-does-this-solution-do"></a>Que fait cette solution ?

Dans cet article, toocreate un exemple de diffusion en continu Spark, effectuez hello comme suit :

1. Créez un Event Hub Azure qui doit recevoir un flux d’événements.

2. Exécuter une application autonome local qui génère des événements et le place toohello concentrateur d’événements Azure. exemple d’application Hello qui effectue l’opération est publiée à [https://github.com/hdinsight/spark-streaming-data-persistence-examples](https://github.com/hdinsight/spark-streaming-data-persistence-examples).

3. Exécutez une application de diffusion en continu à distance sur un cluster Spark qui lit les événements de diffusion en continu à partir d’Azure Event Hub et effectuez diverses tâches de traitement/d’analyse des données.

## <a name="create-an-azure-event-hub"></a>Création d'un hub d'événements Azure

1. Session toohello [Azure Portal](https://ms.portal.azure.com), puis cliquez sur **nouveau** à hello haut à gauche de l’écran hello.

2. Cliquez sur **Internet des Objets**, puis sur **Hubs d’événements**.

    ![Créer un Event Hub pour un exemple de diffusion en continu Spark](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-create-event-hub-for-spark-streaming.png "Créer un Event Hub pour un exemple de diffusion en continu Spark")

3. Bonjour **créer l’espace de noms** panneau, entrez un nom d’espace de noms. Choisissez hello tarification (base ou Standard). En outre, choisissez un abonnement Azure, le groupe de ressources et l’emplacement de ressources toocreate hello. Cliquez sur **créer** toocreate hello espace de noms.

      ![Fournir un nom d’Event Hub pour un exemple de diffusion en continu Spark](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-provide-event-hub-name-for-spark-streaming.png "Fournir un nom d’Event Hub pour un exemple de diffusion en continu Spark")

    > [!NOTE]
    > Vous devez sélectionnez hello même **emplacement** que votre cluster Apache Spark dans HDInsight tooreduce latence et les coûts.
    >
    >

4. Dans hello concentrateurs d’événements espace de noms, cliquez sur espace de noms nouvellement créé hello.      


5. Dans le panneau espace de noms de hello, cliquez sur **concentrateurs d’événements**, puis cliquez sur **+ concentrateur d’événements** toocreate un concentrateur d’événements.
   
    ![Créer un Event Hub pour un exemple de diffusion en continu Spark](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-open-event-hubs-blade-for-spark-streaming-example.png "Créer un Event Hub pour un exemple de diffusion en continu Spark")

6. Tapez un nom pour votre concentrateur d’événements, jeu hello partition count too10 et too1 de rétention de message. Nous ne sommes pas archivage des messages hello dans cette solution afin de vous pouvez laisser le reste hello comme valeur par défaut, puis cliquez sur **créer**.
   
    ![Fournir des détails d’Event Hub pour un exemple de diffusion en continu Spark](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-provide-event-hub-details-for-spark-streaming-example.png "Fournir des détails d’Event Hub pour un exemple de diffusion en continu Spark")

7. Hello nouvellement créé Hub d’événements est répertorié dans le panneau de concentrateur d’événements hello.
    
     ![Afficher le concentrateur d’événements pour l’exemple de diffusion en continu de Spark hello](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-view-event-hub-for-spark-streaming-example.png "mode concentrateur d’événements pour hello au service de diffusion en continu d’exemple")

8. Dans le panneau d’espace de noms hello (pas hello spécifique concentrateur d’événements blade), cliquez sur **les stratégies d’accès partagé**, puis cliquez sur **RootManageSharedAccessKey**.
    
     ![Définir des stratégies de concentrateur d’événements pour l’exemple de diffusion en continu de Spark hello](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-set-event-hub-policies-for-spark-streaming-example.png "des stratégies de concentrateur d’événements défini pour hello au service de diffusion en continu d’exemple")

9. Cliquez sur Bonjour copie bouton toocopy Bonjour **RootManageSharedAccessKey** principal Presse-papiers toohello chaîne clé et de la connexion. Enregistrez ces toouse plus loin dans le didacticiel de hello.
    
     ![Afficher les clés de stratégie de concentrateur d’événements pour l’exemple de diffusion en continu de Spark hello](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-view-event-hub-policy-keys.png "clés de stratégie de mode concentrateur d’événements pour hello au service de diffusion en continu d’exemple")

## <a name="send-messages-tooazure-event-hub-using-a-sample-scala-application"></a>Envoyer des messages tooAzure concentrateur d’événements à l’aide d’un exemple d’application Scala

Dans cette section vous utilisez une application Scala autonome locale qui génère un flux d’événements et l’envoie tooAzure concentrateur d’événements que vous avez créé précédemment. Cette application est disponible sur GitHub à l’adresse [https://github.com/hdinsight/eventhubs-sample-event-producer](https://github.com/hdinsight/eventhubs-sample-event-producer). Hello étapes supposent que vous avez déjà dupliquée ce référentiel GitHub.

1. Assurez-vous que vous avez suivant hello installé sur l’ordinateur hello sur lequel vous exécutez cette application.

    * Kit de développement logiciel (SDK) Oracle Java. Vous pouvez l’installer à partir d’ [ici](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).
    * Apache Maven. Vous pouvez le télécharger [ici](https://maven.apache.org/download.cgi). Instructions tooinstall Maven sont disponibles [ici](https://maven.apache.org/install.html).

2. Ouvrez une invite de commandes et accédez emplacement toohello vous avez cloné du référentiel GitHub hello pour exemple d’application de Scala hello et exécutez hello après application de commande toobuild hello.

        mvn package

3. jar de sortie Hello pour l’application hello, **com-microsoft-azure-eventhubs-client-example-0.2.0.jar**, est créé sous **/target** active. Vous utilisez ce fichier JAR plus loin dans cette solution complète de l’article tootest hello.

## <a name="create-application-tooreceive-messages-from-event-hub-into-a-spark-cluster"></a>Créer des messages tooreceive d’application à partir du concentrateur d’événements dans un cluster Spark 

Nous avons deux approches tooconnect Spark de diffusion en continu Azure Event Hubs, connexion basée sur le récepteur et Direct DStream pas en charge les connexions. En fonction des DStream direct est introduit sur janvier 2017, dans la version de hello 2.0.3. Il est supposé tooreplace hello d’origine récepteur connexion car il n’est plus performante et efficace de ressources. Vous trouverez plus de détails à l’adresse [https://github.com/hdinsight/spark-eventhubs](https://github.com/hdinsight/spark-eventhubs). Direct DStream prend uniquement en charge Spark 2.0+.

### <a name="build-applications-with-hello-dependency-toospark-eventhubs-connector"></a>Créer des applications avec le connecteur de hello dépendance toospark-eventhubs

Nous publierons également hello mise en lots de la version de Spark-EventHubs dans GitHub. version de mise en lots hello toouse de Spark-EventHubs, hello première étape consiste tooindicate GitHub comme hello référentiel de code source en ajoutant hello suivant toopom.xml d’entrée :

```xml
<repository>
      <id>spark-eventhubs</id>
      <url>https://raw.github.com/hdinsight/spark-eventhubs/maven-repo/</url>
      <snapshots>
        <enabled>true</enabled>
        <updatePolicy>always</updatePolicy>
      </snapshots>
</repository>
```

Vous pouvez ensuite ajouter hello suivant dépendance tooyour projet tootake hello version précédente.

Dépendance Maven

```xml
<!-- https://mvnrepository.com/artifact/com.microsoft.azure/spark-streaming-eventhubs_2.11 -->
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>spark-streaming-eventhubs_2.11</artifactId>
    <version>2.0.4</version>
</dependency>
```

Dépendance SBT

```
// https://mvnrepository.com/artifact/com.microsoft.azure/spark-streaming-eventhubs_2.11
libraryDependencies += "com.microsoft.azure" % "spark-streaming-eventhubs_2.11" % "2.0.4"
```

### <a name="direct-dstream-connection"></a>Connexion Direct DStream

Un fichier jar prégénéré contenant des exemples utilisant Direct DStream peut être téléchargé dans [http://central.maven.org/maven2/com/microsoft/azure/spark-streaming-eventhubs_2.11/2.0.4/spark-streaming-eventhubs_2.11-2.0.4.jar](http://central.maven.org/maven2/com/microsoft/azure/spark-streaming-eventhubs_2.11/2.0.4/spark-streaming-eventhubs_2.11-2.0.4.jar).

le fichier jar Hello contient trois exemples dont le code source sont disponibles au [https://github.com/hdinsight/spark-eventhubs/tree/master/examples/src/main/scala/com/microsoft/spark/streaming/examples/directdstream](https://github.com/hdinsight/spark-eventhubs/tree/master/examples/src/main/scala/com/microsoft/spark/streaming/examples/directdstream).

Utilisons [WindowingWordCount](https://github.com/hdinsight/spark-eventhubs/blob/master/examples/src/main/scala/com/microsoft/spark/streaming/examples/directdstream/WindowingWordCount.scala) comme exemple :

```scala
private def createStreamingContext(
  sparkCheckpointDir: String,
  batchDuration: Int,
  namespace: String,
  eventHunName: String,
  eventhubParams: Map[String, String],
  progressDir: String) = {
val ssc = new StreamingContext(new SparkContext(), Seconds(batchDuration))
ssc.checkpoint(sparkCheckpointDir)
val inputDirectStream = EventHubsUtils.createDirectStreams(
  ssc,
  namespace,
  progressDir,
  Map(eventHunName -> eventhubParams))

inputDirectStream.map(receivedRecord => (new String(receivedRecord.getBody), 1)).
  reduceByKeyAndWindow((v1, v2) => v1 + v2, (v1, v2) => v1 - v2, Seconds(batchDuration * 3),
    Seconds(batchDuration)).print()

ssc
}

def main(args: Array[String]): Unit = {

if (args.length != 8) {
  println("Usage: program progressDir PolicyName PolicyKey EventHubNamespace EventHubName" +
    " BatchDuration(seconds) Spark_Checkpoint_Directory maxRate")
  sys.exit(1)
}

val progressDir = args(0)
val policyName = args(1)
val policykey = args(2)
val namespace = args(3)
val name = args(4)
val batchDuration = args(5).toInt
val sparkCheckpointDir = args(6)
val maxRate = args(7)

val eventhubParameters = Map[String, String] (
  "eventhubs.policyname" -> policyName,
  "eventhubs.policykey" -> policykey,
  "eventhubs.namespace" -> namespace,
  "eventhubs.name" -> name,
  "eventhubs.partition.count" -> "32",
  "eventhubs.consumergroup" -> "$Default",
  "eventhubs.maxRate" -> s"$maxRate"
)

val ssc = StreamingContext.getOrCreate(sparkCheckpointDir,
  () => createStreamingContext(sparkCheckpointDir, batchDuration, namespace, name,
    eventhubParameters, progressDir))

ssc.start()
ssc.awaitTermination()
}
```

Bonjour au-dessus de l’exemple, `eventhubParameters` sont hello paramètres spécifiques tooa EventHubs uniques et que vous avez toopass il toohello `createDirectStreams` API qui crée un espace de concentrateurs d’événements tooa DStream Direct objet mappage noms. Sur l’objet DStream directe de hello, vous pouvez appeler toute API DStream fournie par l’infrastructure de l’API de diffusion en continu de Spark. Dans cet exemple, nous calculons fréquence hello de chaque mot dans des intervalles de lot micro 3 dernière hello.

### <a name="receiver-based-connection"></a>Connexion basée sur récepteur

Un Spark écrite dans Scala, qui reçoit les événements et les destinations de routage hello toodifferent, exemple d’application de diffusion en continu est disponible à l’adresse [https://github.com/hdinsight/spark-streaming-data-persistence-examples](https://github.com/hdinsight/spark-streaming-data-persistence-examples). Suivez les étapes de hello sous l’application de hello tooupdate pour votre configuration de concentrateur d’événements et créez des hello sortie jar.

1. Lancez l’idée de IntelliJ et de hello lancer l’écran, sélectionnez **extraire du contrôle de Version** puis cliquez sur **Git**.
   
    ![Exemple de diffusion en continu Apache Spark - obtenir des sources de Git](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-get-source-from-git.png "Exemple de diffusion en continu Apache Spark - obtenir des sources de Git")

2. Bonjour **Clone référentiel** boîte de dialogue, fournissez hello URL toohello Git référentiel tooclone à partir de, spécifiez tooclone de répertoire hello pour, puis cliquez sur **Clone**.
   
    ![Exemple de diffusion en continu Apache Spark - cloner Git](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-clone-from-git.png "Exemple de diffusion en continu Apache Spark - cloner Git")
3. Suivez les invites de hello jusqu'à ce que le projet de hello est entièrement cloné. Appuyez sur **Alt + 1** tooopen hello **vue projet**. Il doit ressembler à suivant de hello.
   
    ![Exemple de diffusion en continu Apache Spark - Affichage de projet](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-project-view.png "Exemple de diffusion en continu Apache Spark - Affichage de projet")
4. Assurez-vous que le code de l’application hello est compilé avec Java8. tooensure, cliquez sur **fichier**, cliquez sur **Structure de projet**et sur hello **projet** onglet, vérifiez qu’au niveau du projet language est défini trop**8 - les expressions lambda, type annotations, etc.**.
   
    ![Exemple de diffusion en continu Apache Spark - Définir un compilateur](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-java-8-compiler.png "Exemple de diffusion en continu Apache Spark - Définir un compilateur")
5. Ouvrez hello **pom.xml** et assurez-vous que la version de Spark hello est correcte. Sous `<properties>` nœud, recherchez hello suivant extrait et vérifier la version de Spark hello.

        <scala.version>2.11.8</scala.version>
        <scala.compat.version>2.11.8</scala.compat.version>
        <scala.binary.version>2.11</scala.binary.version>
        <spark.version>2.0.0</spark.version>

6. application Hello nécessite un fichier jar de dépendance appelé **jar du pilote JDBC**. Il s’agit de messages de type hello toowrite requis provenant du concentrateur d’événements dans une base de données SQL Azure. Vous pouvez télécharger ce fichier jar (version 4.1 ou version ultérieure) à partir d’[ici](https://msdn.microsoft.com/sqlserver/aa937724.aspx). Ajoutez la référence toothis jar dans la bibliothèque de projet hello. Effectuez hello comme suit :
     
     1. Dans la fenêtre IntelliJ idée où vous avez application hello ouvert, cliquez sur **fichier**, cliquez sur **Structure de projet**, puis cliquez sur **bibliothèques**. 
     2. Cliquez sur hello icône d’ajout (![icône d’ajout de](./media/hdinsight-apache-spark-eventhub-streaming/add-icon.png)), cliquez sur **Java**, puis accédez emplacement toohello où vous avez téléchargé le jar de pilote JDBC hello. Suivez les bibliothèque de projet toohello hello jar fichier hello invites tooadd.

         ![ajouter les dépendances manquantes](./media/hdinsight-apache-spark-eventhub-streaming/add-missing-dependency-jars.png "Ajouter les fichiers jars de dépendance manquants")
     3. Cliquez sur **Apply**.

7. Créer le fichier jar de sortie hello. Effectuer hello comme suit.

   1. Bonjour **Structure de projet** boîte de dialogue, cliquez sur **artefacts** puis hello plus de symbole. Dans la boîte de dialogue contextuelle hello, cliquez sur **JAR**, puis cliquez sur **à partir de modules avec des dépendances**.      
       
       ![Exemple de diffusion en continu Apache Spark - créer un fichier jar](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-create-jar.png "Exemple de diffusion en continu Apache Spark - créer un fichier jar")
   2. Bonjour **créer JAR à partir de Modules** boîte de dialogue, cliquez sur les points de suspension hello (![points de suspension](./media/hdinsight-apache-spark-eventhub-streaming/ellipsis.png)) par rapport à hello **principale classe**.
   3. Bonjour **sélection de la classe principale** boîte de dialogue zone, sélectionnez une des classes disponibles de hello, puis sur **OK**.
      
       ![Exemple de diffusion en continu Apache Spark - sélectionner une classe pour un fichier jar](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-select-class-for-jar.png "Exemple de diffusion en continu Apache Spark - sélectionner une classe pour un fichier jar")
   4. Bonjour **créer JAR à partir de Modules** boîte de dialogue zone, assurez-vous que cette option hello trop**extraire toohello cible JAR** est sélectionné, puis cliquez sur **OK**. Cela crée un fichier JAR contenant toutes les dépendances.
      
       ![Exemple de diffusion en continu Apache Spark - créer un fichier jar à partir de modules](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-create-jar-from-modules.png "Exemple de diffusion en continu Apache Spark - créer un fichier jar à partir de modules")
   5. Hello **mise en page de sortie** onglet répertorie tous les fichiers JAR hello qui sont inclus dans le cadre du projet de Maven hello. Vous pouvez sélectionner et hello supprimer ceux sur lesquels hello Scala application ne possède pas de dépendance directe. Pour l’application hello, nous allons créer ici, vous pouvez supprimer tout sauf hello dernière (**spark-diffusion en continu--persistance-exemples de données de compilation sortie**). Sélectionnez hello JAR toodelete, puis cliquez sur hello **supprimer** icône (![icône Supprimer](./media/hdinsight-apache-spark-eventhub-streaming/delete-icon.png)).
      
       ![Exemple de diffusion en continu Apache Spark - supprimer un fichier jar extrait](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-delete-output-jars.png "Exemple de diffusion en continu Apache Spark - supprimer un fichier jar extrait")
      
       Assurez-vous que **Build sur Vérifiez** à cocher est activée, ce qui garantit que ce fichier jar hello est créé chaque fois que projet de hello est généré ou mis à jour. Cliquez sur **Apply**.
   6. Bonjour **mise en page de sortie** onglet, à droite en bas de hello de hello **éléments disponibles** zone, que vous avez jar SQL JDBC hello que vous avez ajouté de bibliothèque de projet toohello antérieur. Vous devez ajouter cette toohello **mise en page de sortie** onglet. Cliquez sur le fichier jar hello, puis cliquez sur **extraire dans la racine de sortie**.
      
       ![Exemple de diffusion en continu Apache Spark - extraire un fichier jar de dépendance](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-extract-dependency-jar.png "Exemple de diffusion en continu Apache Spark - extraire un fichier jar de dépendance")  
      
       Hello **mise en page de sortie** onglet doit maintenant ressembler à ceci.
      
       ![Exemple de diffusion en continu Apache Spark - onglet de sortie finale](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-final-output-tab.png "Exemple de diffusion en continu Apache Spark - onglet de sortie finale")        
      
       Bonjour **Structure de projet** boîte de dialogue, cliquez sur **appliquer** puis cliquez sur **OK**.    
   7. Dans la barre de menus de hello, cliquez sur **générer**, puis cliquez sur **créer le projet**. Vous pouvez également cliquer sur **des artefacts de Build** jar de hello toocreate. Hello jar de sortie est créé sous **\classes\artifacts**.
      
       ![Exemple de diffusion en continu Apache Spark - fichier jar de sortie](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-output-jar.png "Exemple de diffusion en continu Apache Spark - fichier jar de sortie")

## <a name="run-hello-application-remotely-on-a-spark-cluster-using-livy"></a>Exécuter des application hello à distance sur un cluster Spark à l’aide de Livy

Dans cet article vous utilisez Livy toorun hello Apache Spark diffusion en continu application à distance sur un cluster Spark. Pour obtenir une présentation détaillée sur comment toouse Livy avec HDInsight Spark de cluster, consultez [travaux d’envoi à distance tooan Apache Spark cluster sur Azure HDInsight](hdinsight-apache-spark-livy-rest-interface.md). Avant de démarrer l’application de diffusion en continu de Spark hello en cours d’exécution, il existe deux choses à faire :

1. Début hello toogenerate les événements d’application local autonome et envoyé tooEvent Hub. Utilisez hello suivant commande toodo ainsi :

        java -cp com-microsoft-azure-eventhubs-client-example-0.2.0.jar com.microsoft.eventhubs.client.example.EventhubsClientDriver --eventhubs-namespace "mysbnamespace" --eventhubs-name "myeventhub" --policy-name "mysendpolicy" --policy-key "<policy key>" --message-length 32 --thread-count 32 --message-count -1

2. Hello copie jar de diffusion en continu (**spark-diffusion en continu-données-persistance-Examples.jar**) toohello stockage d’objets Blob Azure associé hello cluster. Cela rend tooLivy accessible de hello jar. Vous pouvez utiliser [ **AzCopy**](../storage/common/storage-use-azcopy.md), par conséquent, utilitaire, toodo une commande de ligne. Il existe beaucoup d’autres clients, vous pouvez utiliser les données tooupload. Pour en savoir plus à leur sujet, consultez [Téléchargement de données pour les travaux Hadoop dans HDInsight](hdinsight-upload-data.md).
3. Installez CURL sur hello ordinateur sur lequel vous exécutez ces applications à partir de. Nous utilisons hello de tooinvoke CURL hello de toorun de points de terminaison Livy des travaux à distance.

### <a name="run-hello-spark-streaming-application-tooreceive-hello-events-into-an-azure-storage-blob-as-text"></a>Exécutez hello Spark diffusion en continu tooreceive hello événements de l’application dans un objet Blob de stockage Azure sous forme de texte

Ouvrez une invite de commandes, accédez répertoire toohello où vous avez installé CURL et exécutez hello (remplacer le nom d’utilisateur/mot de passe et du cluster) de commande suivante :

    curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\inputBlob.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

Hello paramètres hello fichier **inputBlob.txt** sont définies comme suit :

    { "file":"wasb:///example/jars/spark-streaming-data-persistence-examples.jar", "className":"com.microsoft.spark.streaming.examples.workloads.EventhubsEventCount", "args":["--eventhubs-namespace", "mysbnamespace", "--eventhubs-name", "myeventhub", "--policy-name", "myreceivepolicy", "--policy-key", "<put-your-key-here>", "--consumer-group", "$default", "--partition-count", 10, "--batch-interval-in-seconds", 20, "--checkpoint-directory", "/EventCheckpoint", "--event-count-folder", "/EventCount/EventCount10"], "numExecutors":20, "executorMemory":"1G", "executorCores":1, "driverMemory":"2G" }

Découvrons que sont les paramètres hello hello fichier d’entrée :

* **fichier** est fichier hello chemin d’accès toohello application jar sur le compte de stockage Azure hello associé hello cluster.
* **className** est le nom hello de classe hello dans jar de hello.
* **args** liste hello d’arguments requis par la classe hello
* **numExecutors** est nombre hello de noyaux utilisés par hello de toorun Spark application de diffusion en continu. Il doit toujours être au moins deux fois hello différentes partitions du Hub d’événements.
* **executorMemory**, **executorCores**, **driverMemory** sont des applications de diffusion en continu toohello ressources tooassign requis de paramètres utilisés.

> [!NOTE]
> Vous n’avez pas besoin de toocreate hello dossiers de sortie (EventCheckpoint, nombre d’événements/EventCount10) qui sont utilisées comme paramètres. application de diffusion en continu de Hello crée pour vous.
>
>

Lorsque vous exécutez la commande hello, vous devez voir une sortie semblable à hello suivante :

    < HTTP/1.1 201 Created
    < Content-Type: application/json; charset=UTF-8
    < Location: /18
    < Server: Microsoft-IIS/8.5
    < X-Powered-By: ARR/2.5
    < X-Powered-By: ASP.NET
    < Date: Tue, 01 Dec 2015 05:39:10 GMT
    < Content-Length: 37
    <
    {"id":1,"state":"starting","log":[]}* Connection #0 toohost mysparkcluster.azurehdinsight.net left intact

Prenez note de l’ID de lot hello dans hello dernière ligne de sortie hello (dans cet exemple, il est « 1 »). tooverify qui hello application s’exécute correctement, vous pouvez consulter votre compte de stockage Azure associé hello cluster et vous devez voir hello **/nombre d’événements/EventCount10** dossier créé. Ce dossier doit contenir les objets BLOB qui capture le nombre de hello d’événements traités au sein de hello période de temps spécifiée pour le paramètre hello **lot intervalle en secondes**.

application de diffusion en continu de Spark Hello continuera toorun jusqu'à ce que vous l’arrêter. toodo utilisez donc hello de commande suivante :

    curl -k --user "admin:mypassword1!" -v -X DELETE "https://mysparkcluster.azurehdinsight.net/livy/batches/1"

### <a name="run-hello-applications-tooreceive-hello-events-into-an-azure-storage-blob-as-json"></a>Exécuter des applications de hello les événements hello tooreceive dans un objet Blob de stockage Azure en tant que JSON
Ouvrez une invite de commandes, accédez répertoire toohello où vous avez installé CURL et exécutez hello (remplacer le nom d’utilisateur/mot de passe et du cluster) de commande suivante :

    curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\inputJSON.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

Hello paramètres hello fichier **inputJSON.txt** sont définies comme suit :

    { "file":"wasb:///example/jars/spark-streaming-data-persistence-examples.jar", "className":"com.microsoft.spark.streaming.examples.workloads.EventhubsToAzureBlobAsJSON", "args":["--eventhubs-namespace", "mysbnamespace", "--eventhubs-name", "myeventhub", "--policy-name", "myreceivepolicy", "--policy-key", "<put-your-key-here>", "--consumer-group", "$default", "--partition-count", 10, "--batch-interval-in-seconds", 20, "--checkpoint-directory", "/EventCheckpoint", "--event-count-folder", "/EventCount/EventCount10", "--event-store-folder", "/EventStore10"], "numExecutors":20, "executorMemory":"1G", "executorCores":1, "driverMemory":"2G" }

les paramètres de Hello sont similaires toowhat que vous avez spécifié pour la sortie de texte hello, dans l’étape précédente de hello. Là encore, il est inutile toocreate hello dossiers de sortie (EventCheckpoint, nombre d’événements/EventCount10) qui sont utilisées comme paramètres. application de diffusion en continu de Hello crée pour vous.

 Une fois que vous exécutez la commande hello, vous pouvez consulter votre compte de stockage Azure associé hello cluster et vous devez voir hello **/EventStore10** dossier créé. Ouvrez n’importe quel fichier préfixe **partie -** et vous devez voir les événements de hello traités dans un format JSON.

### <a name="run-hello-applications-tooreceive-hello-events-into-a-hive-table"></a>Exécuter des applications de hello les événements hello tooreceive dans une table Hive
toorun hello application de diffusion en continu de Spark que les événements de flux de données dans une ruche tables que vous avez besoin des composants supplémentaires. Ces composants sont les suivants :

* datanucleus-api-jdo-3.2.6.jar
* datanucleus-SGBDR-3.2.9.jar
* datanucleus-core-3.2.10.jar
* hive-site.xml

Hello **.jar** fichiers sont disponibles sur votre cluster HDInsight Spark à `/usr/hdp/current/spark-client/lib`. Hello **hive-site.XML** est disponible à l’adresse `/usr/hdp/current/spark-client/conf`.

Vous pouvez utiliser [WinScp](http://winscp.net/eng/download.php) toocopy ces fichiers à partir de l’ordinateur local de hello cluster tooyour. Vous pouvez ensuite utiliser toocopy outils ces fichiers sur le compte de stockage tooyour associées au cluster de hello. Pour plus d’informations sur l’utilisation des fichiers de compte de stockage toohello tooupload, consultez [télécharger des données pour les travaux Hadoop dans HDInsight](hdinsight-upload-data.md).

Une fois que vous avez copié les fichiers de hello tooyour compte de stockage Azure, ouvrez une invite de commandes, accédez répertoire toohello où vous avez installé CURL et exécutez hello (remplacer le nom d’utilisateur/mot de passe et du cluster) de commande suivante :

    curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\inputHive.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

Hello paramètres hello fichier **inputHive.txt** sont définies comme suit :

    { "file":"wasb:///example/jars/spark-streaming-data-persistence-examples.jar", "className":"com.microsoft.spark.streaming.examples.workloads.EventhubsToHiveTable", "args":["--eventhubs-namespace", "mysbnamespace", "--eventhubs-name", "myeventhub", "--policy-name", "myreceivepolicy", "--policy-key", "<put-your-key-here>", "--consumer-group", "$default", "--partition-count", 10, "--batch-interval-in-seconds", 20, "--checkpoint-directory", "/EventCheckpoint", "--event-count-folder", "/EventCount/EventCount10", "--event-hive-table", "EventHiveTable10" ], "jars":["wasb:///example/jars/datanucleus-api-jdo-3.2.6.jar", "wasb:///example/jars/datanucleus-rdbms-3.2.9.jar", "wasb:///example/jars/datanucleus-core-3.2.10.jar"], "files":["wasb:///example/jars/hive-site.xml"], "numExecutors":20, "executorMemory":"1G", "executorCores":1, "driverMemory":"2G" }

les paramètres de Hello sont similaires toowhat que vous avez spécifié pour la sortie de texte hello, dans les étapes précédentes hello. Là encore, vous ne devez pas de sortie de hello toocreate table Hive (EventHiveTable10) qui sont utilisées comme paramètres de sortie de dossiers (EventCheckpoint, nombre d’événements/EventCount10) ou hello. application de diffusion en continu de Hello crée pour vous. Notez que hello **JAR** et **fichiers** option inclut les fichiers de chemins d’accès toohello .jar et hello hive-site.XML que vous avez copié sur le compte de stockage toohello.

tooverify qui hello table hive a été créé avec succès, vous pouvez SSH en cluster de hello et exécution des requêtes Hive. Pour obtenir des instructions, consultez [Utilisation de Hive avec Hadoop dans HDInsight avec SSH](hdinsight-hadoop-use-hive-ssh.md). Une fois que vous êtes connecté à l’aide de SSH, vous pouvez exécuter hello suivant commande tooverify cette table Hive hello, **EventHiveTable10**, est créé.

    show tables;

Vous devez voir s’afficher une sortie similaire toohello :

    OK
    eventhivetable10
    hivesampletable

Vous pouvez également exécuter une requête SELECT contenu de hello tooview de la table de hello.

    SELECT * FROM eventhivetable10 LIMIT 10;

Vous devez voir une sortie semblable à hello suivante :

    ZN90apUSQODDTx7n6Toh6jDbuPngqT4c
    sor2M7xsFwmaRW8W8NDwMneFNMrOVkW1
    o2HcsU735ejSi2bGEcbUSB4btCFmI1lW
    TLuibq4rbj0T9st9eEzIWJwNGtMWYoYS
    HKCpPlWFWAJILwR69MAq863nCWYzDEw6
    Mvx0GQOPYvPR7ezBEpIHYKTKiEhYammQ
    85dRppSBSbZgThLr1s0GMgKqynDUqudr
    5LAWkNqorLj3ZN9a2mfWr9rZqeXKN4pF
    ulf9wSFNjD7BZXCyunozecov9QpEIYmJ
    vWzM3nvOja8DhYcwn0n5eTfOItZ966pa
    Time taken: 4.434 seconds, Fetched: 10 row(s)


### <a name="run-hello-applications-tooreceive-hello-events-into-an-azure-sql-database-table"></a>Exécuter des applications de hello les événements hello tooreceive dans une table de base de données SQL Azure
Avant d’exécuter cette étape, assurez-vous que vous disposez d’une base de données SQL Azure. Pour obtenir des instructions, consultez [Créer une base de données SQL en quelques minutes](../sql-database/sql-database-get-started.md). toocomplete cette section, vous avez besoin de valeurs pour le nom de la base de données, nom du serveur de base de données et administrateur de base de données hello en tant que paramètres. Il est inutile table de base de données toocreate hello cependant. Hello application de diffusion en continu de Spark qui crée pour vous.

Ouvrez une invite de commandes, accédez répertoire toohello où vous avez installé CURL et exécutez hello de commande suivante :

    curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\inputSQL.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

Hello paramètres hello fichier **inputSQL.txt** sont définies comme suit :

    { "file":"wasb:///example/jars/spark-streaming-data-persistence-examples.jar", "className":"com.microsoft.spark.streaming.examples.workloads.EventhubsToAzureSQLTable", "args":["--eventhubs-namespace", "mysbnamespace", "--eventhubs-name", "myeventhub", "--policy-name", "myreceivepolicy", "--policy-key", "<put-your-key-here>", "--consumer-group", "$default", "--partition-count", 10, "--batch-interval-in-seconds", 20, "--checkpoint-directory", "/EventCheckpoint", "--event-count-folder", "/EventCount/EventCount10", "--sql-server-fqdn", "<database-server-name>.database.windows.net", "--sql-database-name", "mysparkdatabase", "--database-username", "sparkdbadmin", "--database-password", "<put-password-here>", "--event-sql-table", "EventContent" ], "numExecutors":20, "executorMemory":"1G", "executorCores":1, "driverMemory":"2G" }

tooverify qui hello application s’exécute correctement, vous pouvez vous connecter à base de données SQL Azure toohello à l’aide de SQL Server Management Studio. Pour obtenir des instructions sur la façon de toodo qui, consultez [connecter tooSQL de base de données avec SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md). Une fois que vous êtes connecté toohello de base de données, vous pouvez naviguer toohello **EventContent** table qui a été créé par l’application de diffusion en continu de hello. Vous pouvez exécuter un requête rapide tooget hello de données à partir de la table de hello. Exécutez hello suivant la requête :

    SELECT * FROM EventCount

Vous devez voir s’afficher sortie similaire toohello :

    00046b0f-2552-4980-9c3f-8bba5647c8ee
    000b7530-12f9-4081-8e19-90acd26f9c0c
    000bc521-9c1b-4a42-ab08-dc1893b83f3b
    00123a2a-e00d-496a-9104-108920955718
    0017c68f-7a4e-452d-97ad-5cb1fe5ba81b
    001KsmqL2gfu5ZcuQuTqTxQvVyGCqPp9
    001vIZgOStka4DXtud0e3tX7XbfMnZrN
    00220586-3e1a-4d2d-a89b-05c5892e541a
    0029e309-9e54-4e1b-84be-cd04e6fce5ec
    003333cf-874f-4045-9da3-9f98c2b4ea49
    0043c07e-8d73-420a-9af7-1fcb94575356
    004a11a9-0c2c-4bc0-a7d5-2e0ebd947ab9


## <a name="seealso"></a>Voir aussi
* [Vue d’ensemble : Apache Spark sur Azure HDInsight](hdinsight-apache-spark-overview.md)
* [Conception de la connexion basée sur récepteur et Direct DStream](https://www.slideshare.net/NanZhu/seattle-sparkmeetup032317)

### <a name="scenarios"></a>Scénarios
* [Spark avec BI : effectuez une analyse interactive des données à l’aide de Spark dans HDInsight avec des outils BI](hdinsight-apache-spark-use-bi-tools.md)
* [Spark avec Machine Learning : utilisez Spark dans HDInsight pour l’analyse de la température des bâtiments à l’aide des données des systèmes HVAC](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Spark avec Machine Learning : Spark utilisation dans résultats de l’inspection alimentaires toopredict HDInsight](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Analyse des journaux de site web à l’aide de Spark dans HDInsight](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a>Créer et exécuter des applications
* [Créer une application autonome avec Scala](hdinsight-apache-spark-create-standalone-application.md)
* [Exécuter des tâches à distance avec Livy sur un cluster Spark](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a>Outils et extensions
* [Utiliser le plug-in des outils HDInsight pour IntelliJ idée toocreate et soumettre des applications les plus importantes Spark Scala](hdinsight-apache-spark-intellij-tool-plugin.md)
* [Utiliser des plug-in des outils HDInsight pour les applications de Spark toodebug IntelliJ idée à distance](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [Utiliser des bloc-notes Zeppelin avec un cluster Spark sur HDInsight](hdinsight-apache-spark-zeppelin-notebook.md)
* [Noyaux disponibles pour le bloc-notes Jupyter dans un cluster Spark pour HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Utiliser des packages externes avec les blocs-notes Jupyter](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [Installer Notebook sur votre ordinateur et vous connecter tooan cluster HDInsight Spark](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a>Gestion des ressources
* [Gérer les ressources de cluster d’Apache Spark hello dans Azure HDInsight](hdinsight-apache-spark-resource-manager.md)
* [Track and debug jobs running on an Apache Spark cluster in HDInsight (Suivi et débogage des tâches en cours d’exécution sur un cluster Apache Spark dans HDInsight)](hdinsight-apache-spark-job-debugging.md)

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-create-storageaccount]: ../storage-create-storage-account/
