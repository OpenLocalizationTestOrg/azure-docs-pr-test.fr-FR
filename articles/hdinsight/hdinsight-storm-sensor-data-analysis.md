---
title: "données de capteur aaaAnalyze avec Apache Storm et HBase | Documents Microsoft"
description: "Découvrez comment tooconnect tooApache renverser avec un réseau virtuel. Utilisez Storm avec des données de capteur tooprocess HBase à partir d’un concentrateur d’événements et le visualiser avec D3.js."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: a9a1ac8e-5708-4833-b965-e453815e671f
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/09/2017
ms.author: larryfr
ms.openlocfilehash: e54fe9ffc720b0089f90e302b24a9438bd43999a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-sensor-data-with-apache-storm-event-hub-and-hbase-in-hdinsight-hadoop"></a>Analyser les données de capteur avec Apache Storm, Event Hub, et HBase dans HDInsight (Hadoop)

Découvrez comment toouse Apache renverser sur les données de capteur tooprocess HDInsight à partir du concentrateur d’événements Azure. les données de salutation sont ensuite stockées dans HBase Apache sur HDInsight et visualisé à l’aide de D3.js.

modèle de gestionnaire de ressources Azure Hello utilisé dans ce document montre comment toocreate plusieurs ressources Azure dans un groupe de ressources. modèle de Hello crée un réseau virtuel Azure, deux clusters HDInsight (Storm et HBase) et une application Web Azure. Une implémentation de node.js d’un tableau de bord web en temps réel est toohello automatiquement déployé l’application web.

> [!NOTE]
> informations Hello dans ce document et l’exemple dans ce document nécessitent HDInsight version 3.6.
>
> Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure. Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

## <a name="prerequisites"></a>Composants requis

* Un abonnement Azure.
* [Node.js](http://nodejs.org/): tableau de bord web de hello toopreview utilisés localement sur votre environnement de développement.
* [Java et hello JDK 1.7](http://www.oracle.com/technetwork/java/javase/downloads/index.html): utilisé la topologie de Storm toodevelop hello.
* [Maven](http://maven.apache.org/what-is-maven.html): projet de hello toobuild et compilation utilisé.
* [GIT](http://git-scm.com/): projet de hello toodownload utilisé à partir de GitHub.
* Un **SSH** client : tooconnect toohello HDInsight de basés sur Linux clusters utilisés. Pour en savoir plus, voir [Utilisation de SSH avec Hadoop Linux sur HDInsight depuis Linux, Unix ou OS X](hdinsight-hadoop-linux-use-ssh-unix.md).


> [!IMPORTANT]
> Vous n’avez pas besoin d’un cluster HDInsight existant. Dans ce document, les étapes de Hello créent hello suivant des ressources :
> 
> * un réseau virtuel Azure ;
> * un cluster Storm sur HDInsight (basé sur Linux, 2 nœuds Worker) ;
> * un cluster HBase sur HDInsight (basé sur Linux, 2 nœuds Worker) ;
> * Une application Web Azure qui héberge le tableau de bord web hello

## <a name="architecture"></a>Architecture

![Diagramme d'architecture](./media/hdinsight-storm-sensor-data-analysis/devicesarchitecture.png)

Cet exemple se compose de hello suivant des composants :

* **Azure Event Hubs**: contient les données collectées à partir des capteurs.
* **Storm sur HDInsight**: fournit le traitement en temps réel des données à partir d’Event Hub.
* **HBase sur HDInsight**: fournit un magasin de données NoSQL persistant pour les données une fois celles-ci traitées par Storm.
* **Service de réseau virtuel Azure**: permet de sécuriser les communications entre hello Storm sur HDInsight et HBase sur les clusters HDInsight.
  
  > [!NOTE]
  > Un réseau virtuel est requis lors de l’utilisation des API du client Java HBase hello. Il n’est pas exposée via la passerelle de public hello pour les clusters HBase. Clusters HBase lors de l’installation et Storm dans le même réseau virtuel permet de hello hello cluster Storm (ou un autre système sur le réseau virtuel de hello) toodirectly HBase à l’aide des API du client d’accès.

* **Site web de tableau de bord**: un exemple de tableau de bord qui suit des données en temps réel.
  
  * site Web de Hello est implémenté dans Node.js.
  * [Socket.IO](http://socket.io/) est utilisé pour la communication en temps réel entre le topologie de Storm hello et hello.
    
    > [!NOTE]
    > L’utilisation de Socket.io pour la communication est un détail d’implémentation. Vous pouvez utiliser toute infrastructure de communications, telles que WebSockets brut ou SignalR.

  * [D3.js](http://d3js.org/) toograph utilisé hello donnée qui sont envoyées du site Web toohello.

> [!IMPORTANT]
> Deux clusters sont nécessaires, car il n’existe aucune méthode prise en charge toocreate un HDInsight cluster Storm et HBase.

Hello topologie lit les données à partir du concentrateur d’événements à l’aide de hello [org.apache.storm.eventhubs.spout.EventHubSpout](http://storm.apache.org/releases/0.10.1/javadocs/org/apache/storm/eventhubs/spout/class-use/EventHubSpout.html) classe et écrit des données dans HBase à l’aide de hello [org.apache.storm.hbase.bolt.HBaseBolt](https://storm.apache.org/releases/1.0.1/javadocs/org/apache/storm/hbase/bolt/HBaseBolt.html) classe. Communication avec le site Web de hello s’effectue à l’aide de [socket.io-client.java](https://github.com/nkzawa/socket.io-client.java).

Hello suivant schéma explique disposition hello de topologie de hello :

![diagramme de topologie](./media/hdinsight-storm-sensor-data-analysis/sensoranalysis.png)

> [!NOTE]
> Ce diagramme est une vue simplifiée d’une topologie de hello. Une instance de chaque composant est créée pour chaque partition de votre hub d’événements. Ces instances sont répartis entre les nœuds de hello dans un cluster de hello et données sont routées entre eux, comme suit :
> 
> * Les données à partir de l’Analyseur de toohello bec hello sont à charge équilibrée.
> * Données à partir de hello analyseur toohello du tableau de bord et HBase sont regroupées par ID de périphérique, afin que les messages à partir de hello même appareil toujours flux toohello même composant.

### <a name="topology-components"></a>Composants de la topologie

* **Bec de concentrateur d’événements**: bec de hello est fourni dans le cadre de la version d’Apache Storm 0.10.0 et versions ultérieures.
  
  > [!NOTE]
  > bec de concentrateur d’événements Hello utilisé dans cet exemple requiert une tempête sur la version 3.5 ou 3.6 du cluster HDInsight.

* **ParserBolt.java**: données hello qui sont émises par bec de hello sont JSON brut, et parfois plus d’un événement est émis à la fois. Cet éclair lit données hello émises par hello bec et traite le message de salutation JSON. éclair de Hello émet ensuite les données de salutation sous forme de tuple qui contient plusieurs champs.
* **DashboardBolt.java**: ce composant illustre comment toouse hello bibliothèque cliente de Socket.io pour les données de toosend Java dans le tableau de bord en temps réel toohello web.
* **non-hbase.yaml**: hello de définition de la topologie utilisée lors de l’exécution en mode local. Les composants de HBase ne sont pas utilisés.
* **avec hbase.yaml**: hello de définition de la topologie utilisée lors de la topologie de hello en cours d’exécution sur le cluster de hello. Les composants de HBase sont utilisés.
* **dev.Properties**: hello pour bec de concentrateur d’événements hello HBase éclair et composants de tableau de bord, les informations de configuration.

## <a name="prepare-your-environment"></a>Préparation de votre environnement

Avant d’utiliser cet exemple, vous devez créer un concentrateur d’événements Azure typologie Storm hello lit.

### <a name="configure-event-hub"></a>Configuration du hub d'événements

Concentrateur d’événements est la source de données hello pour cet exemple. Utilisez hello suivant les étapes toocreate un concentrateur d’événements.

1. À partir de hello [portail Azure](https://portal.azure.com), sélectionnez **+ nouveau** -> **Internet of Things** -> **concentrateurs d’événements**.
2. Bonjour **créer de Namespace** section, effectuer hello tâches suivantes :
   
   1. Entrez un **nom** pour l’espace de noms hello.
   2. Sélectionnez un niveau tarifaire. **De base** est suffisant pour cet exemple.
   3. Sélectionnez hello Azure **abonnement** toouse.
   4. Sélectionnez un groupe de ressources existant ou créez-en un.
   5. Sélectionnez hello **emplacement** pour hello concentrateur d’événements.
   6. Sélectionnez **code confidentiel toodashboard**, puis cliquez sur **créer**.

3. Lors de la fin du processus de création de hello, hello informations concentrateurs d’événements pour votre espace de noms s’affiche. À partir d’ici, sélectionnez **+ Ajouter un hub d’événements**. Bonjour **concentrateur d’événements créer** section, entrez un nom de **sensordata**, puis sélectionnez **créer**. Laissez hello autres champs à des valeurs par défaut hello.
4. À partir de concentrateurs d’événements hello consulter pour votre espace de noms, sélectionnez **concentrateurs d’événements**. Sélectionnez hello **sensordata** entrée.
5. À partir de hello sensordata concentrateur d’événements, sélectionnez **les stratégies d’accès partagé**. Hello d’utilisation **+ ajouter** hello tooadd de lien suivant des stratégies :

    | Nom de la stratégie | Revendications |
    | ----- | ----- |
    | périphériques | Envoyer |
    | storm | Écouter |

1. Sélectionnez les deux stratégies et prenez note de hello **clé primaire** valeur. Vous avez besoin de valeur de hello pour les deux stratégies dans les étapes suivantes.

## <a name="download-and-configure-hello-project"></a>Télécharger et configurer le projet de hello

Utilisez hello suivant du projet de hello toodownload à partir de GitHub.

    git clone https://github.com/Blackmist/hdinsight-eventhub-example

Après la commande hello, vous avez hello suivant la structure de répertoires :

    hdinsight-eventhub-example/
        TemperatureMonitor/ - this contains hello topology
            resources/
                log4j2.xml - set logging toominimal.
                no-hbase.yaml - topology definition without hbase components.
                with-hbase.yaml - topology definition with hbase components.
            src/main/java/com/microsoft/examples/bolts/
                ParserBolt.java - parses JSON data into tuples
                DashboardBolt.java - sends data over Socket.IO toohello web dashboard.
        dashboard/nodejs/ - this is hello node.js web dashboard.
        SendEvents/ - utilities toosend fake sensor data.

> [!NOTE]
> Ce document ne passe pas dans les détails de toofull de code hello inclus dans cet exemple. Toutefois, hello code entièrement contient des commentaires.

tooconfigure hello projet tooread à partir du concentrateur d’événements, ouvrez hello `hdinsight-eventhub-example/TemperatureMonitor/dev.properties` et ajoutez votre toohello d’informations de concentrateur d’événements lignes suivantes :

```bash
eventhub.read.policy.name: your_read_policy_name
eventhub.read.policy.key: your_key_here
eventhub.namespace: your_namespace_here
eventhub.name: your_event_hub_name
eventhub.partitions: 2
```

## <a name="compile-and-test-locally"></a>Compilation et test local

> [!IMPORTANT]
> À l’aide de la topologie de hello localement nécessite un environnement de développement Storm en cours. Pour plus d’informations, consultez la page [Configurer un environnement de développement Storm](http://storm.apache.org/releases/1.1.0/Setting-up-development-environment.html) à l’adresse Apache.org.

> [!WARNING]
> Si vous utilisez un environnement de développement Windows, vous pouvez recevoir un `java.io.IOException` lors de l’exécution topologie de hello localement. Dans ce cas, déplacez sur la topologie de hello toorunning sur HDInsight.

Avant de tester, vous devez démarrer hello du tableau de bord tooview hello sortie de la topologie de hello et générer des données toostore dans le concentrateur d’événements.

> [!IMPORTANT]
> composant de HBase Hello de cette topologie n’est pas actif lorsque vous testez localement. Hello API Java pour un cluster HBase de hello ne sont pas accessibles à partir de l’extérieur hello réseau virtuel Azure qui contient des clusters de hello.

### <a name="start-hello-web-application"></a>Démarrer l’application web de hello

1. Ouvrez une invite de commandes et modifiez les répertoires`hdinsight-eventhub-example/dashboard`. Utilisez hello suivant des dépendances de hello tooinstall de commande requis par hello web application :
   
    ```bash
    npm install
    ```

2. Utilisez hello suite de l’application web de commande toostart hello :
   
    ```bash
    node server.js
    ```
   
    Vous voyez un toohello similaire message suit texte :
   
        Server listening at port 3000

3. Ouvrez un navigateur web et entrez `http://localhost:3000/` en tant qu’adresse de hello. Un toohello similaire de page suivant l’image s’affiche :
   
    ![tableau de bord web](./media/hdinsight-storm-sensor-data-analysis/emptydashboard.png)
   
    Laissez l’invite de commandes ouverte. Après le test, utilisez le serveur web de Ctrl-C toostop hello.

### <a name="generate-data"></a>Générer des données

> [!NOTE]
> Hello étapes de cette section utilisent Node.js afin qu’elles peuvent être utilisées sur n’importe quelle plateforme. Pour obtenir des exemples de langage, consultez hello `SendEvents` active.

1. Ouvrez une nouvelle invite, interpréteur de commandes ou Terminal Server et remplacez les répertoires`hdinsight-eventhub-example/SendEvents/nodejs`. dépendances de hello tooinstall requis par l’application hello, utilisez hello de commande suivante :

    ```bash
    npm install
    ```

2. Ouvrez hello `app.js` dans un éditeur de texte et ajoutez hello informations du concentrateur d’événements obtenues précédemment :
   
    ```javascript
    // ServiceBus Namespace
    var namespace = 'YourNamespace';
    // Event Hub Name
    var hubname ='sensordata';
    // Shared access Policy name and key (from Event Hub configuration)
    var my_key_name = 'devices';
    var my_key = 'YourKey';
    ```
   
   > [!NOTE]
   > Cet exemple suppose que vous avez utilisé `sensordata` comme nom hello de votre Hub d’événements. Et que `devices` en tant que nom hello de stratégie hello qui a un `Send` de revendication.

3. Utilisez hello suivant commande tooinsert nouvelles entrées dans le concentrateur d’événements :
   
    ```bash
    node app.js
    ```
   
    Vous voyez plusieurs lignes de sortie qui contiennent des données hello envoyé tooEvent Hub :
   
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"0","Temperature":7}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"1","Temperature":39}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"2","Temperature":86}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"3","Temperature":29}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"4","Temperature":30}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"5","Temperature":5}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"6","Temperature":24}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"7","Temperature":40}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"8","Temperature":43}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"9","Temperature":84}

### <a name="build-and-start-hello-topology"></a>Créez et démarrez la topologie de hello

1. Ouvrez une nouvelle invite de commandes et modifiez les répertoires`hdinsight-eventhub-example/TemperatureMonitor`. toobuild et package hello topologie, utiliser hello commande suivante : 

    ```bash
    mvn clean package
    ```

2. toostart hello topologie en mode local, utilisez hello de commande suivante :

    ```bash
    storm jar target/TemperatureMonitor-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local --filter dev.properties resources/no-hbase.yaml
    ```

    * `--local`topologie de hello démarre en mode local.
    * `--filter`utilise hello `dev.properties` toopopulate paramètres du fichier de définition de la topologie hello.
    * `resources/no-hbase.yaml`utilise hello `no-hbase.yaml` définition de la topologie.
 
   Une fois démarré, la topologie de hello lit les entrées à partir du concentrateur d’événements et les envoie toohello le tableau de bord en cours d’exécution sur votre ordinateur local. Vous devriez voir lignes dans hello web du tableau de bord, toohello similaire suivant l’image :
   
    ![tableau de bord avec données](./media/hdinsight-storm-sensor-data-analysis/datadashboard.png)

2. Alors que le tableau de bord hello est en cours d’exécution, utilisez hello `node app.js` commande hello précédente étapes toosend nouvelles données tooEvent concentrateurs. Étant donné que les valeurs de température hello sont générés de façon aléatoire, graphique de hello doit mettre à jour des modifications importantes des tooshow de température.
   
   > [!NOTE]
   > Vous devez être en hello **hdinsight-eventhub-exemple/SendEvents/Nodejs** lorsque vous utilisez hello `node app.js` commande.

3. Après la vérification des mises à jour de ce tableau de bord hello, topologie de hello d’arrêt à l’aide de Ctrl + C. Vous pouvez également utiliser le serveur web local de Ctrl + C toostop hello.

## <a name="create-a-storm-and-hbase-cluster"></a>Créer un cluster Storm et HBase

Hello les étapes de cette section utilisent un [modèle Azure Resource Manager](../azure-resource-manager/resource-group-template-deploy.md) toocreate un cluster de réseau virtuel Azure et Storm et HBase sur le réseau virtuel de hello. modèle de Hello crée une application Web Azure et déploie une copie du tableau de bord hello dans celui-ci.

> [!NOTE]
> Un réseau virtuel est utilisé afin que la topologie hello en cours d’exécution sur le cluster de Storm hello peut communiquer directement avec cluster de HBase hello à l’aide de hello HBase Java API.

modèle de gestionnaire de ressources Hello utilisé dans ce document se trouve dans un conteneur d’objets blob publics à **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-hbase-storm-cluster-in-vnet-3.6.json**.

1. Cliquez sur hello suivant toosign bouton dans tooAzure et modèle du Gestionnaire de ressources ouvrir hello Bonjour portail Azure.
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-hbase-storm-cluster-in-vnet-3.6.json" target="_blank"><img src="./media/hdinsight-storm-sensor-data-analysis/deploy-to-azure.png" alt="Deploy tooAzure"></a>

2. À partir de hello **les déploiement personnalisé** section, entrez hello valeurs suivantes :
   
    ![Paramètres HDInsight](./media/hdinsight-storm-sensor-data-analysis/parameters.png)
   
   * **Nom du Cluster de base**: cette valeur est utilisée comme nom de base hello pour les clusters de Storm et HBase hello. Par exemple, si vous entrez **abc**, cela crée un cluster Storm nommé **storm-abc** et un cluster HBase nommé **hbase-abc**.
   * **Nom d’utilisateur de cluster**: nom d’utilisateur admin hello pour les clusters de Storm et HBase hello.
   * **Mot de passe de connexion cluster**: hello mot de passe administrateur pour les clusters de Storm et HBase hello.
   * **Nom d’utilisateur SSH**: hello toocreate d’utilisateur SSH pour les clusters de Storm et HBase hello.
   * **Mot de passe SSH**: mot de passe de hello pour hello SSH pour les clusters de Storm et HBase hello.
   * **Emplacement**: région hello créés dans les clusters hello.
     
     Cliquez sur **OK** toosave les paramètres hello.

3. Hello d’utilisation **notions de base** section toocreate un groupe de ressources ou sélectionnez-en un existant.
4. Bonjour **emplacement du groupe de ressources** menu déroulant, sélectionnez hello même emplacement que vous avez sélectionné pour hello **emplacement** paramètre Bonjour **paramètres** section.
5. Lire les conditions générales hello et sélectionnez **J’accepte les termes du contrat de toohello et conditions susmentionnées**.
6. Enfin, recherchez **code confidentiel toodashboard** , puis sélectionnez **bon**. Il prend environ 20 minutes toocreate les clusters hello.

Une fois que les ressources hello ont été créées, plus d’informations sur le groupe de ressources hello s’affiche.

![Groupe de ressources de réseau virtuel de hello et des clusters](./media/hdinsight-storm-sensor-data-analysis/groupblade.png)

> [!IMPORTANT]
> Notez que les noms de hello des clusters HDInsight de hello sont **storm-BASENAME** et **hbase-BASENAME**, où BASENAME est nom hello toohello modèle fourni. Vous utilisez ces noms dans une étape ultérieure lors de la connexion toohello clusters. Également, notez que hello nom du site de tableau de bord hello est **basename-tableau de bord**. Cette valeur sera utilisée ultérieurement dans ce document.

## <a name="configure-hello-dashboard-bolt"></a>Configurer éclair du tableau de bord hello

toosend données toohello tableau de bord déployé comme une application web, vous devez modifier hello ligne Bonjour `dev.properties`fichier :

```yaml
dashboard.uri: http://localhost:3000
```

Modification `http://localhost:3000` trop`http://BASENAME-dashboard.azurewebsites.net` et enregistrez le fichier de hello. Remplacez **BASENAME** par nom de base hello entré à l’étape précédente de hello. Vous pouvez également utiliser le groupe de ressources hello créé précédemment URL hello tooselect hello du tableau de bord et de la vue.

## <a name="create-hello-hbase-table"></a>Créer la table HBase à hello

toostore des données dans HBase, nous devons d’abord créer une table. Ressources nécessitant une tempête toowrite à créer au préalable, car des ressources toocreate lors de la tentative d’à l’intérieur d’une topologie Storm peuvent entraîner plusieurs instances de la tentative de toocreate hello même ressource. Créer des ressources de hello en dehors de la topologie de hello et utiliser Storm pour lecture/écriture et analytique.

1. Utiliser SSH tooconnect toohello HBase cluster à l’aide de SSH hello et mot de passe fourni toohello modèle lors de la création du cluster. Par exemple, si la connexion à l’aide de hello `ssh` vous utiliseriez hello selon la syntaxe de la commande :
   
    ```bash
    ssh sshuser@clustername-ssh.azurehdinsight.net
    ```
   
    Remplacez `sshuser` avec le nom d’utilisateur SSH hello que vous avez fourni lors de la création du cluster de hello. Remplacez `clustername` avec le nom du cluster HBase hello.

2. À partir de la session SSH de hello, démarrez le shell HBase de hello.
   
    ```bash
    hbase shell
    ```
   
    Une fois que l’interpréteur de commandes hello a chargé, vous voyez un `hbase(main):001:0>` invite.

3. À partir de hello shell HBase, entrez hello suivant commande toocreate données capteur table toostore hello :
   
    ```hbase
    create 'SensorData', 'cf'
    ```

4. Vérifiez que la table hello a été créée à l’aide de hello de commande suivante :
   
    ```hbase
    scan 'SensorData'
    ```
   
    Cela retourne les informations toohello semblable l’exemple suivant, qui indique qu’il n’y a 0 ligne dans la table de hello.
   
        ROW                   COLUMN+CELL                                       0 row(s) in 0.1900 seconds

5. Entrez `exit` tooexit hello shell HBase :

## <a name="configure-hello-hbase-bolt"></a>Configurer éclair de HBase hello

tooHBase toowrite à partir du cluster de Storm hello, vous devez fournir éclair de HBase hello avec les détails de la configuration de votre cluster HBase hello.

1. Utilisez une des hello suivant le quorum de soigneur exemples tooretrieve hello pour votre cluster HBase :

    ```bash
    CLUSTERNAME='your_HDInsight_cluster_name'
    curl -u admin -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/HBASE/components/HBASE_MASTER" | jq '.metrics.hbase.master.ZookeeperQuorum'
    ```

    > [!NOTE]
    > Remplacez `your_HDInsight_cluster_name` par nom de hello de votre cluster HDInsight. Pour plus d’informations sur l’installation de hello `jq` utilitaire, consultez [https://stedolan.github.io/jq/](https://stedolan.github.io/jq/).
    >
    > Lorsque vous y êtes invité, entrez le mot de passe de hello pour la connexion d’administration hello HDInsight.

    ```powershell
    $clusterName = 'your_HDInsight_cluster_name`
    $creds = Get-Credential -UserName "admin" -Message "Enter hello HDInsight login"
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/HBASE/components/HBASE_MASTER" -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.metrics.hbase.master.ZookeeperQuorum
    ```

    > [!NOTE]
    > Remplacez ' your_HDInsight_cluster_name avec nom hello de votre cluster HDInsight. Lorsque vous y êtes invité, entrez le mot de passe de hello pour la connexion d’administration hello HDInsight.
    >
    > Cet exemple nécessite Azure PowerShell. Pour plus d’informations sur l’utilisation d’Azure PowerShell, voir [Prise en main d’Azure PowerShell](https://docs.microsoft.com/en-us/powershell/scripting/Getting-Started-with-Windows-PowerShell?view=powershell-6)

    les informations de Hello retournées par ces exemples sont similaires toohello suivant du texte :

    `zk2-hbase.mf0yeg255m4ubit1auvj1tutvh.ex.internal.cloudapp.net:2181,zk0-hbase.mf0yeg255m4ubit1auvj1tutvh.ex.internal.cloudapp.net:2181,zk3-hbase.mf0yeg255m4ubit1auvj1tutvh.ex.internal.cloudapp.net:2181`

    Ces informations sont utilisées par toocommunicate Storm avec un cluster HBase de hello.

2. Modifier hello `dev.properties` et ajoutez hello soigneur quorum informations toohello ligne suivante :

    ```yaml
    hbase.zookeeper.quorum: your_hbase_quorum
    ```

## <a name="build-package-and-deploy-hello-solution-toohdinsight"></a>Générez, empaquetez et déployez hello solution tooHDInsight

Dans votre environnement de développement, utilisez hello suivant cluster storm toohello de la topologie étapes toodeploy hello Storm.

1. À partir de hello `TemperatureMonitor` répertoire, suivante de hello utilisez commande tooperform une nouvelle build et créer un package du fichier JAR à partir de votre projet :
   
        mvn clean package
   
    Cette commande crée un fichier nommé `TemperatureMonitor-1.0-SNAPSHOT.jar in hello `répertoire cible de votre projet.

2. Hello d’utilisation scp tooupload `TemperatureMonitor-1.0-SNAPSHOT.jar` et `dev.properties` cluster de fichiers tooyour Storm. Bonjour à l’exemple, remplacez `sshuser` avec vous fournies lors de la création du cluster de hello, par l’utilisateur SSH hello et `clustername` avec nom hello de votre cluster Storm. Lorsque vous y êtes invité, entrez le mot de passe de hello pour l’utilisateur SSH hello.
   
    ```bash
    scp target/TemperatureMonitor-1.0-SNAPSHOT.jar dev.properties sshuser@clustername-ssh.azurehdinsight.net:
    ```

   > [!NOTE]
   > Il peut prendre plusieurs minutes les fichiers tooupload hello.

    Pour plus d’informations sur l’utilisation de hello `scp` et `ssh` commandes hdinsight, consultez [utilisation de SSH avec HDInsight](./hdinsight-hadoop-linux-use-ssh-unix.md)

3. Une fois que le fichier de hello a été téléchargé, connectez le cluster de tempête de toohello à l’aide de SSH.
   
    ```bash
    ssh sshuser@clustername-ssh.azurehdinsight.net
    ```

    Remplacez `sshuser` avec le nom d’utilisateur SSH hello. Remplacez `clustername` avec le nom du cluster Storm hello.

4. toostart hello topologie, utiliser hello commande à partir de la session SSH hello suivante :
   
    ```bash
    storm jar TemperatureMonitor-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote --filter dev.properties -R /with-hbase.yaml
    ```

    * `--remote`soumet hello topologie toohello service Nimbus, qui distribue les nœuds de superviseur toohello dans un cluster de hello.
    * `--filter`utilise hello `dev.properties` toopopulate paramètres du fichier de définition de la topologie hello.
    * `-R /with-hbase.yaml`utilise hello `with-hbase.yaml` topologie inclus dans le package de hello.

5. Une fois que la topologie de hello a démarré, ouvrez un site Web toohello de navigateur vous avez publié sur Azure, puis utilisez hello `node app.js` commande toosend tooEvent de données concentrateur. Vous devez voir les informations de hello du tableau de bord mise à jour toodisplay hello web.
   
    ![dashboard](./media/hdinsight-storm-sensor-data-analysis/datadashboard.png)

## <a name="view-hbase-data"></a>Afficher les données HBase

Utilisez hello suivant les étapes tooconnect tooHBase et vérifiez que les données de hello ont été écrites toohello table :

1. Utiliser SSH tooconnect toohello HBase cluster.
   
    ```bash
    ssh sshuser@clustername-ssh.azurehdinsight.net
    ```

    Remplacez `sshuser` avec le nom d’utilisateur SSH hello. Remplacez `clustername` avec le nom du cluster HBase hello.

2. À partir de la session SSH de hello, démarrez le shell HBase de hello.
   
    ```bash
    hbase shell
    ```
   
    Une fois que l’interpréteur de commandes hello a chargé, vous voyez un `hbase(main):001:0>` invite.

3. Afficher les lignes de table de hello :
   
    ```hbase
    scan 'SensorData'
    ```
   
    Cette commande retourne toohello similaires en informations suivant le texte, indiquant qu’il existe des données dans la table de hello.
   
        hbase(main):002:0> scan 'SensorData'
        ROW                             COLUMN+CELL
        \x00\x00\x00\x00               column=cf:temperature, timestamp=1467290788277, value=\x00\x00\x00\x04
        \x00\x00\x00\x00               column=cf:timestamp, timestamp=1467290788277, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x01               column=cf:temperature, timestamp=1467290788348, value=\x00\x00\x00M
        \x00\x00\x00\x01               column=cf:timestamp, timestamp=1467290788348, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x02               column=cf:temperature, timestamp=1467290788268, value=\x00\x00\x00R
        \x00\x00\x00\x02               column=cf:timestamp, timestamp=1467290788268, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x03               column=cf:temperature, timestamp=1467290788269, value=\x00\x00\x00#
        \x00\x00\x00\x03               column=cf:timestamp, timestamp=1467290788269, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x04               column=cf:temperature, timestamp=1467290788356, value=\x00\x00\x00>
        \x00\x00\x00\x04               column=cf:timestamp, timestamp=1467290788356, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x05               column=cf:temperature, timestamp=1467290788326, value=\x00\x00\x00\x0D
        \x00\x00\x00\x05               column=cf:timestamp, timestamp=1467290788326, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x06               column=cf:temperature, timestamp=1467290788253, value=\x00\x00\x009
        \x00\x00\x00\x06               column=cf:timestamp, timestamp=1467290788253, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x07               column=cf:temperature, timestamp=1467290788229, value=\x00\x00\x00\x12
        \x00\x00\x00\x07               column=cf:timestamp, timestamp=1467290788229, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x08               column=cf:temperature, timestamp=1467290788336, value=\x00\x00\x00\x16
        \x00\x00\x00\x08               column=cf:timestamp, timestamp=1467290788336, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x09               column=cf:temperature, timestamp=1467290788246, value=\x00\x00\x001
        \x00\x00\x00\x09               column=cf:timestamp, timestamp=1467290788246, value=2015-02-10T14:43.05.00320Z
        10 row(s) in 0.1800 seconds
   
   > [!NOTE]
   > Cette opération retourne un maximum de 10 lignes à partir de la table de hello.

## <a name="delete-your-clusters"></a>Supprimer vos clusters

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

clusters de hello toodelete, de stockage et de l’application web à la fois, supprimer groupe de ressources hello qui les contient.

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’exemples de topologies Storm avec HDInsight, consultez les [exemples de topologies pour Storm sur HDInsight](hdinsight-storm-example-topology.md)

Pour plus d’informations sur Apache Storm, consultez hello [Apache Storm](https://storm.incubator.apache.org/) site.

Pour plus d’informations sur HBase sur HDInsight, consultez hello [HBase HDInsight aperçu](hdinsight-hbase-overview.md).

Pour plus d’informations sur Socket.io, consultez hello [socket.io](http://socket.io/) site.

Pour plus d'informations sur D3.js, consultez la page [D3.js : documents pilotés par les données](http://d3js.org/).

Pour plus d'informations sur la création de topologies en Java, consultez [Développement de topologies Java pour Apache Storm sur HDInsight](hdinsight-storm-develop-java-topology.md).

Pour plus d'informations sur la création de topologies en .NET, consultez [Développement de topologies C# pour Apache Storm sur HDInsight](hdinsight-storm-develop-csharp-visual-studio-topology.md).

[azure-portal]: https://portal.azure.com
