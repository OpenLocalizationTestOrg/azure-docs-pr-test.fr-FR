---
title: "aaaDeploy et gérer les topologies d’Apache Storm sur HDInsight de basés sur Linux | Documents Microsoft"
description: "Découvrez comment toodeploy, surveiller et gérer des topologies de Apache Storm à l’aide de hello du tableau de bord Storm sur HDInsight de basés sur Linux. Utilisez les outils Hadoop pour Visual Studio."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 35086e62-d6d8-4ccf-8cae-00073464a1e1
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/16/2017
ms.author: larryfr
ms.openlocfilehash: 3a1edb773089cc596fea423710aa88cf83c7b841
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-manage-apache-storm-topologies-on-hdinsight"></a>Déploiement et gestion des topologies Apache Storm sur HDInsight

Dans ce document, principes hello de gérer et surveiller les topologies Storm sur Storm sur les clusters HDInsight.

> [!IMPORTANT]
> Hello étapes décrites dans cet article nécessitent une tempête basés sur Linux sur un cluster HDInsight. Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure. Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement). 
>
> Pour plus d’informations sur le déploiement et la surveillance des topologies sur HDInsight Windows, consultez [Déploiement et gestion des topologies Apache Storm sur HDInsight Windows](hdinsight-storm-deploy-monitor-topology.md)


## <a name="prerequisites"></a>Composants requis

* **Un cluster Storm Linux sur HDInsight**: consultez [Prise en main d’Apache Storm sur HDInsight](hdinsight-apache-storm-tutorial-get-started-linux.md) pour connaître les étapes de création d’un cluster

* (Facultatif) **Des connaissances en SSH et SCP** : pour plus d’informations, voir [Utilisation de SSH avec HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

* (Facultatif) **Visual Studio**: Kit de développement logiciel Azure 2.5.1 ou plus récent et hello Data Lake Tools pour Visual Studio. Pour plus d’informations, consultez [Get started using Data Lake Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md) (Prise en main de Data Lake Tools pour Visual Studio).

    Une des hello versions de Visual Studio suivantes :

  * Visual Studio 2012 avec [Update 4](http://www.microsoft.com/download/details.aspx?id=39305)

  * Visual Studio 2013 avec [Update 4](http://www.microsoft.com/download/details.aspx?id=44921) ou [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?LinkId=517284)
  * [Visual Studio 2015](https://www.visualstudio.com/downloads/)

  * Visual Studio 2015 (toute édition)

  * Visual Studio 2017 (toute édition) Data Lake Tools pour Visual Studio 2017 sont installés dans le cadre de hello la charge de travail Azure.

## <a name="submit-a-topology-visual-studio"></a>Soumettre une topologie : Visual Studio

Hello HDInsight outils peut être utilisé toosubmit c# ou hybride topologies tooyour cluster Storm. Hello suit utilisent un exemple d’application. Pour plus d’informations sur la création de vos propres topologies à l’aide des outils de HDInsight hello, consultez [C# développer des topologies à l’aide des outils de hello HDInsight pour Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).

1. Si vous n’avez pas déjà installé version la plus récente des outils de Data Lake hello hello pour Visual Studio, consultez [prise en main Data Lake Tools pour Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).

    > [!NOTE]
    > Hello Data Lake Tools pour Visual Studio ont été précédemment appelé hello HDInsight Tools pour Visual Studio.
    >
    > Data Lake Tools pour Visual Studio sont inclus dans hello __la charge de travail Azure__ pour Visual Studio 2017.

2. Ouvrez Visual Studio, sélectionnez **Fichier** > **Nouveau** > **Projet**.

3. Bonjour **nouveau projet** boîte de dialogue, développez **installé** > **modèles**, puis sélectionnez **HDInsight**. Dans la liste hello des modèles, sélectionnez **Storm exemple**. Bas hello de boîte de dialogue hello, tapez un nom pour l’application hello.

    ![image](./media/hdinsight-storm-deploy-monitor-topology-linux/sample.png)

4. Dans **l’Explorateur de solutions**, cliquez sur le projet de hello, puis sélectionnez **envoyer tooStorm sur HDInsight**.

   > [!NOTE]
   > Si vous y êtes invité, entrez les informations d’identification de connexion hello pour votre abonnement Azure. Si vous avez plusieurs abonnements, connectez-vous toohello qui contient votre Storm sur le cluster HDInsight.

5. Sélectionnez votre Storm sur le cluster HDInsight à partir de hello **Cluster Storm** liste déroulante et sélectionnez **Submit**. Vous pouvez surveiller si l’envoi de hello réussit à l’aide de hello **sortie** fenêtre.

## <a name="submit-a-topology-ssh-and-hello-storm-command"></a>Envoyer une topologie : SSH et hello renverser commande

1. Utiliser SSH tooconnect toohello HDInsight cluster. Remplacez **nom d’utilisateur** nom hello de votre connexion SSH. Remplacez **CLUSTERNAME** par le nom de votre cluster HDInsight :

        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net

    Pour plus d’informations sur l’utilisation de SSH tooconnect tooyour HDInsight de cluster, consultez [utilisation de SSH avec HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

2. Utilisez hello suivant commande toostart un exemple de topologie :

        storm jar /usr/hdp/current/storm-client/contrib/storm-starter/storm-starter-topologies-*.jar org.apache.storm.starter.WordCountTopology WordCount

    Cette commande démarre hello exemple WordCount de topologie de cluster de hello. Cette topologie générer de façon aléatoire les phrases et les occurrences de hello de nombre de chaque mot dans les phrases hello.

   > [!NOTE]
   > Lors de la soumission cluster toohello de topologie, vous devez d’abord copier le fichier jar hello contenant le cluster de hello avant d’utiliser hello `storm` commande. toocopy hello toohello de fichiers, vous pouvez utiliser hello `scp` commande. Par exemple, `scp FILENAME.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:FILENAME.jar`
   >
   > exemple WordCount de Hello et des autres exemples de starter storm, figurent déjà sur votre cluster à `/usr/hdp/current/storm-client/contrib/storm-starter/`.

## <a name="submit-a-topology-programmatically"></a>Soumettre une topologie : par programme

Vous pouvez par programmation déployer un tooStorm topologie sur HDInsight en communiquant avec hello service Nimbus hébergé dans votre cluster. [https://github.com/Azure-Samples/hdinsight-Java-Deploy-Storm-Topology](https://github.com/Azure-Samples/hdinsight-java-deploy-storm-topology) fournit un exemple d’application Java qui montre comment toodeploy et démarrer une topologie via le service de Nimbus de hello.

## <a name="monitor-and-manage-visual-studio"></a>Surveiller et gérer : Visual Studio

Lorsqu’une topologie a été envoyée à l’aide de Visual Studio, hello **Storm Topologies** permet d’afficher de hello cluster apparaît. Sélectionnez la topologie de hello dans hello liste tooview informations hello topologie en cours d’exécution.

![Visual Studio Monitor](./media/hdinsight-storm-deploy-monitor-topology/vsmonitor.png)

> [!NOTE]
> Vous pouvez également afficher les **Topologies Storm** dans l’**Explorateur de serveurs** en développant **Azure** > **HDInsight**, puis en cliquant avec le bouton droit sur le cluster HDInsight et en sélectionnant **Affichage des topologies Storm**.

Sélectionnez la forme de hello pour hello becs verseurs amovibles ou boulons tooview d’informations sur ces composants. Une nouvelle fenêtre s’ouvre pour chaque élément sélectionné.

### <a name="deactivate-and-reactivate"></a>Désactivation et réactivation

La désactivation d’une topologie la met en pause jusqu’à ce qu’elle soit arrêtée ou réactivée. tooperform ces opérations, utilisez hello __Deactivate__ et __réactiver__ boutons haut hello hello __récapitulatif de la topologie__.

### <a name="rebalance"></a>Rééquilibrage

Rééquilibrage une topologie permet de parallélisme de hello hello système toorevise de topologie de hello. Par exemple, si vous avez redimensionné hello cluster tooadd autres notes, rééquilibrage permet une topologie de nouveaux nœuds de toosee hello.

toorebalance une topologie, utilisez hello __rééquilibrer__ bouton haut hello hello __récapitulatif de la topologie__.

> [!WARNING]
> Tout d’abord le rééquilibrage une topologie désactive la topologie de hello, répartit uniformément les travailleurs sur le cluster de hello, puis enfin retourne toohello état de la topologie hello qu'il se trouvait avant le rééquilibrage s’est produite. Par conséquent, si la topologie de hello était active, elle redevient actif. Si elle était désactivée, elle reste désactivée.

### <a name="kill-a-topology"></a>Supprimer une topologie

Les topologies Storm poursuivre l’exécution jusqu'à ce qu’ils sont arrêtés ou cluster de hello est supprimé. toostop une topologie, utilisez hello __Kill__ bouton haut hello hello __récapitulatif de la topologie__.

## <a name="monitor-and-manage-ssh-and-hello-storm-command"></a>Surveiller et gérer : SSH et hello renverser commande

Hello `storm` utilitaire vous permet de toowork avec les topologies en cours d’exécution à partir de la ligne de commande hello. Pour obtenir la liste complète des commandes, utilisez `storm -h` .

### <a name="list-topologies"></a>Liste de toutes les topologies

Utilisez hello suivant toolist de commande toutes les topologies en cours d’exécution :

    storm list

Cette commande retourne toohello similaire à informations suivant le texte :

    Topology_name        Status     Num_tasks  Num_workers  Uptime_secs
    -------------------------------------------------------------------
    WordCount            ACTIVE     29         2            263

### <a name="deactivate-and-reactivate"></a>Désactivation et réactivation

La désactivation d’une topologie la met en pause jusqu’à ce qu’elle soit arrêtée ou réactivée. Utilisez hello suivant commande toodeactivate et réactiver :

    storm Deactivate TOPOLOGYNAME

    storm Activate TOPOLOGYNAME

### <a name="kill-a-running-topology"></a>Arrêt d’une topologie en cours d’exécution

Les topologies Storm, une fois démarrées, continuent leur exécution jusqu’à ce qu’elles soient arrêtées. toostop une topologie, utilisez hello de commande suivante :

    storm kill TOPOLOGYNAME

### <a name="rebalance"></a>Rééquilibrage

Rééquilibrage une topologie permet de parallélisme de hello hello système toorevise de topologie de hello. Par exemple, si vous avez redimensionné hello cluster tooadd autres notes, rééquilibrage permet une topologie de nouveaux nœuds de toosee hello.

> [!WARNING]
> Tout d’abord le rééquilibrage une topologie désactive la topologie de hello, répartit uniformément les travailleurs sur le cluster de hello, puis enfin retourne toohello état de la topologie hello qu'il se trouvait avant le rééquilibrage s’est produite. Par conséquent, si la topologie de hello était active, elle redevient actif. Si elle était désactivée, elle reste désactivée.

    storm rebalance TOPOLOGYNAME

## <a name="monitor-and-manage-storm-ui"></a>Surveiller et gérer : interface utilisateur de Storm

Bonjour Storm UI fournit une interface web pour l’utilisation des topologies en cours d’exécution et est inclus dans votre cluster HDInsight. tooview hello Storm UI, utilisez un tooopen de navigateur web **https://CLUSTERNAME.azurehdinsight.net/stormui**, où **CLUSTERNAME** est le nom hello de votre cluster.

> [!NOTE]
> Si vous êtes invité tooprovide un nom d’utilisateur et un mot de passe, entrez l’administrateur de cluster hello (admin) et un mot de passe que vous avez utilisé lors des cluster hello création.

### <a name="main-page"></a>Page principale

page principale de Hello Hello Storm UI fournit hello informations suivantes :

* **Résumé du cluster**: informations de base sur le cluster de Storm hello.
* **Résumé de la topologie**: une liste des topologies en cours d’exécution. Utilisez les liens hello tooview de cette section plus d’informations sur les topologies spécifiques.
* **Résumé de superviseur**: plus d’informations sur le superviseur de Storm hello.
* **Configuration de Nimbus**: configuration Nimbus pour le cluster de hello.

### <a name="topology-summary"></a>Résumé de la topologie

Sélection d’un lien à partir de hello **récapitulatif de la topologie** section affiche hello informations sur la topologie de hello suivantes :

* **Résumé de la topologie**: informations de base sur la topologie de hello.
* **Actions de topologie**: actions de gestion que vous pouvez effectuer pour la topologie de hello.

  * **Activer**: reprend le traitement d’une topologie arrêtée.
  * **Désactiver**: suspend une topologie en cours d’exécution.
  * **Rééquilibrer**: ajuste le parallélisme hello de topologie de hello. Vous devez rééquilibrer les topologies en cours d’exécution une fois que vous avez modifié le nombre de hello de nœuds de cluster de hello. Cette opération permet de hello topologie tooadjust parallélisme toocompensate pour hello augmenté ou diminué le nombre de nœuds de cluster de hello.

    Pour plus d’informations, consultez <a href="http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html" target="_blank">présentation parallélisme hello d’une topologie de Storm</a>.
  * **KILL**: met fin à une topologie Storm après hello spécifié le délai d’attente.
* **Statistiques de topologie**: statistiques sur la topologie de hello. tooset hello laps de temps pour hello restant entrées sur la page de hello, utilisez les liens hello hello **fenêtre** colonne.
* **Becs verseurs amovibles**: hello becs verseurs utilisés par la topologie de hello. Utilisez les liens hello tooview de cette section plus d’informations sur becs verseurs spécifiques.
* **Boulons**: hello boulons utilisés par la topologie de hello. Utilisez les liens hello tooview de cette section plus d’informations sur les boulons spécifiques.
* **Configuration de la topologie**: configuration hello de topologie de hello sélectionné.

### <a name="spout-and-bolt-summary"></a>Résumé relatif aux spouts et aux bolts

En sélectionnant un bec de hello **becs verseurs amovibles** ou **boulons** sections affiche hello suit les informations d’élément de hello sélectionné :

* **Résumé des composants**: informations de base sur bec de hello ou éclair.
* **BEC/éclair statistiques**: statistiques sur hello bec ou boulon. tooset hello laps de temps pour hello restant entrées sur la page de hello, utilisez les liens hello hello **fenêtre** colonne.
* **D’entrée statistiques** (boulon uniquement) : flux consommées par un éclair de hello d’entrée le plus d’informations sur hello.
* **Statistiques de sortie**: plus d’informations sur les flux hello émis par ce bec ou boulon.
* **Les exécuteurs**: informations sur les instances de hello de bec de hello ou éclair. Sélectionnez hello **Port** entrée pour un tooview spécifique de l’exécuteur un journal d’informations de diagnostic généré pour cette instance.
* **Erreurs**: les informations d’erreur pour ce spout ou ce bolt.

## <a name="monitor-and-manage-rest-api"></a>Surveiller et gérer : API REST

Hello Storm UI repose sur hello API REST, afin de pouvoir effectuer similaires de gestion et de la fonctionnalité d’analyse à l’aide des API REST de hello. Vous pouvez utiliser des outils personnalisés hello API REST toocreate pour gérer et surveiller les topologies de Storm.

Pour plus d’informations, consultez la rubrique [API REST de l’interface utilisateur Storm](http://storm.apache.org/releases/0.9.6/STORM-UI-REST-API.html). Hello informations suivantes sont spécifiques toousing hello API REST avec Apache Storm sur HDInsight.

> [!IMPORTANT]
> Hello Storm REST API n’est pas disponible publiquement hello internet et doit être accessible à l’aide d’un SSH tunnel toohello HDInsight nœud principal du cluster. Pour plus d’informations sur la création et à l’aide d’un tunnel SSH, consultez [tooaccess utiliser SSH Tunneling Ambari web de l’interface utilisateur, ResourceManager, JobHistory, NameNode, Oozie et autres interfaces utilisateur web](hdinsight-linux-ambari-ssh-tunnel.md).

### <a name="base-uri"></a>URI de base

Bonjour URI de base pour l’API REST de hello sur les clusters HDInsight de basés sur Linux est disponible sur le nœud principal hello **https://HEADNODEFQDN:8744/api/v1/**. nom de domaine Hello de nœud principal de hello est généré au cours de la création du cluster et n’est pas statique.

Vous pouvez trouver le nom de domaine complet (FQDN) hello pour le nœud principal du cluster hello de plusieurs façons différentes :

* **À partir d’une session SSH**: utiliser la commande hello `headnode -f` à partir d’un cluster de toohello session SSH.
* **À partir de Ambari Web**: sélectionnez **Services** de hello en haut de page de hello, puis sélectionnez **Storm**. À partir de hello **Résumé** onglet, sélectionnez **Storm UI Server**. Hello, nom de domaine complet du nœud de hello hello Storm UI et l’API REST est en cours d’exécution est en hello haut hello.
* **À partir de l’API REST de Ambari**: utiliser la commande hello `curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/STORM/components/STORM_UI_SERVER"` tooretrieve plus d’informations sur le nœud hello hello Storm UI et l’API REST sont en cours d’exécution. Remplacez **mot de passe** avec le mot de passe administrateur hello pour le cluster de hello. Remplacez **CLUSTERNAME** avec le nom du cluster hello. Dans la réponse de hello, écriture de « host_name » hello contient hello nom de domaine complet du nœud de hello.

### <a name="authentication"></a>Authentification

Toohello demandes API REST doivent utiliser **l’authentification de base**, de sorte que vous utilisez le nom du cluster hello HDInsight administrateur et le mot de passe.

> [!NOTE]
> Étant donné que l’authentification de base est envoyée à l’aide de texte en clair, vous devez **toujours** utiliser les communications HTTPS toosecure avec cluster de hello.

### <a name="return-values"></a>Valeurs de retour

Informations qui sont retournées à partir de hello API REST peuvent uniquement être utilisable à partir de cluster de hello ou ordinateurs virtuels sur hello même réseau virtuel Azure en tant que cluster de hello. Par exemple, nom de domaine complet de hello (FQDN) retournée pour les serveurs soigneur n'est pas accessible à partir de hello Internet.

## <a name="next-steps"></a>Étapes suivantes

Maintenant que vous avez appris comment topologies toodeploy et le moniteur à l’aide de hello Storm le tableau de bord, découvrez comment trop[basée sur Java de développer des topologies, à l’aide de Maven](hdinsight-storm-develop-java-topology.md).

Pour accéder à une liste d’exemples supplémentaires de topologies, consultez la rubrique [Exemples de topologies Storm sur HDInsight](hdinsight-storm-example-topology.md).
