---
title: "exemples d’aaaStorm-starter sur Apache Storm sur HDInsight - Azure | Documents Microsoft"
description: "Découvrez comment analytique de données volumineuses toodo et traiter les données en temps réel à l’aide d’Apache Storm hello exemples storm-starter sur HDInsight."
keywords: storm-starter, exemple apache storm
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: d710dcac-35d1-4c27-a8d6-acaf8146b485
ms.service: hdinsight
ms.devlang: java
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/15/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive,hdiseo17may2017
ms.openlocfilehash: bb6d6549e67ca5b557f0692f98c89692a87267b0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
#<a name="get-started-with-apache-storm-on-hdinsight-using-hello-storm-starter-examples"></a>Prise en main Apache Storm sur HDInsight à l’aide des exemples de storm-starter hello

Découvrez comment toouse Apache Storm dans HDInsight à l’aide de hello exemples de storm-starter.

Apache Storm est un système de calcul en temps réel, évolutif, distribué, à tolérance de panne, qui permet de traiter des flux de données. Avec Storm sur Azure HDInsight, vous pouvez créer un cluster Storm basé sur le cloud qui effectue l’analyse de données volumineuses en temps réel.

> [!IMPORTANT]
> Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure. Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

## <a name="prerequisites"></a>Composants requis

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

* **Un abonnement Azure**. Consultez la rubrique [Obtenir une version d'évaluation gratuite d'Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).

* **Des connaissances en SSH et SCP**. Pour en savoir plus, voir [Utilisation de SSH avec HDInsight (Hadoop) depuis Bash (l’interpréteur de commande) sur Windows 10, Linux, Unix ou OS X](hdinsight-hadoop-linux-use-ssh-unix.md).

## <a name="create-a-storm-cluster"></a>Créer un cluster Storm

Utilisez hello suivant les étapes toocreate une tempête de cluster HDInsight :

1. À partir de hello [portail Azure](https://portal.azure.com), sélectionnez **+ nouveau**, **Intelligence + Analytique**, puis sélectionnez **HDInsight**.

    ![Création d'un cluster HDInsight](./media/hdinsight-apache-storm-tutorial-get-started-linux/create-hdinsight.png)

2. À partir de hello **notions de base** panneau, entrez hello informations suivantes :

    * **Nom du cluster**: nom hello du cluster HDInsight de hello.
    * **Abonnement**: sélectionnez hello abonnement toouse.
    * **Nom d’utilisateur de cluster** et **mot de passe de connexion Cluster**: connexion hello lors de l’accès de cluster de hello via le protocole HTTPS. Vous utilisez ces services de tooaccess des informations d’identification telles que hello l’interface utilisateur de Ambari Web ou l’API REST.
    * **Secure Shell (SSH) username**: connexion hello utilisée lors de l’accès de cluster de hello via SSH. Par défaut, un mot de passe hello est hello identique au mot de passe de connexion hello cluster.
    * **Groupe de ressources**: hello ressource groupe toocreate hello cluster.
    * **Emplacement**: hello région Azure toocreate hello cluster.

    ![Sélectionnez un abonnement](./media/hdinsight-apache-storm-tutorial-get-started-linux/hdinsight-basic-configuration.png)

3. Sélectionnez **Cluster type**, et puis hello du jeu de valeurs suivantes sur hello **configuration de Cluster** panneau :

    * **Type de cluster** : Storm

    * **Système d’exploitation** : Linux

    * **Version** : Storm 1.1.0 (HDI 3.6)

    * **Niveau cluster** : standard

    Enfin, utilisez hello **sélectionnez** bouton toosave paramètres.

    ![Sélectionner un type de cluster](./media/hdinsight-apache-storm-tutorial-get-started-linux/set-hdinsight-cluster-type.png)

4. Après avoir sélectionné le type de cluster hello, utilisez hello __sélectionnez__ tooset hello cluster type de bouton. Ensuite, utilisez hello __suivant__ configuration de base de toofinish de bouton.

5. À partir de hello **stockage** panneau, sélectionnez ou créez un compte de stockage. Pour connaître les étapes hello dans ce document, laissez hello autres champs sur ce panneau valeurs par défaut de hello. Hello d’utilisation __suivant__ configuration du stockage toosave bouton.

    ![Définir les paramètres de compte de stockage hello pour HDInsight](./media/hdinsight-apache-storm-tutorial-get-started-linux/set-hdinsight-storage-account.png)

6. À partir de hello **Résumé** panneau, revoir la configuration de cluster de hello hello. Hello d’utilisation __modifier__ lie toochange tous les paramètres sont incorrects. Enfin, utilisez le cluster de hello toocreate the__Create__ bouton.

    ![Résumé de la configuration du cluster](./media/hdinsight-apache-storm-tutorial-get-started-linux/hdinsight-configuration-summary.png)

    > [!NOTE]
    > Il peut prendre jusqu'à cluster de hello toocreate too20 minutes.

## <a name="run-a-storm-starter-sample-on-hdinsight"></a>Exécuter un exemple storm-starter sur HDInsight

1. Connecter le cluster HDInsight de toohello à l’aide de SSH :

        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net

    Si vous avez utilisé un toosecure de mot de passe de votre compte d’utilisateur SSH, vous êtes invité à tooenter il. Si vous avez utilisé une clé publique, vous pouvez peut-être utiliser hello `-i` paramètre toospecify hello la clé privée correspondante. Par exemple, `ssh -i ~/.ssh/id_rsa USERNAME@CLUSTERNAME-ssh.azurehdinsight.net`.

    Pour en savoir plus, voir [Utilisation de SSH avec HDInsight (Hadoop) depuis Bash (l’interpréteur de commande) sur Windows 10, Linux, Unix ou OS X](hdinsight-hadoop-linux-use-ssh-unix.md).

2. Utilisez hello suivant commande toostart un exemple de topologie :

        storm jar /usr/hdp/current/storm-client/contrib/storm-starter/storm-starter-topologies-*.jar org.apache.storm.starter.WordCountTopology wordcount

    > [!NOTE]
    > Dans les versions précédentes de HDInsight, nom de la classe hello de topologie de hello est `storm.starter.WordCountTopology` au lieu de `org.apache.storm.starter.WordCountTopology`.

    Cette commande démarre hello exemple WordCount de topologie sur cluster hello, avec un nom convivial 'wordcount'. Il génère de manière aléatoire les phrases et les occurrences de hello de nombre de chaque mot dans les phrases hello.

    > [!NOTE]
    > Lorsque vous soumettez votre propre cluster toohello de topologies, vous devez d’abord copier le fichier jar hello contenant le cluster de hello avant d’utiliser hello `storm` commande. Hello d’utilisation `scp` fichier de commandes toocopy hello. Par exemple, `scp FILENAME.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:FILENAME.jar`
    >
    > exemple WordCount de Hello et des autres exemples storm-starter, figurent déjà sur votre cluster à `/usr/hdp/current/storm-client/contrib/storm-starter/`.

Si vous êtes intéressé par source hello pour obtenir des exemples hello storm-starter, vous pouvez trouver le code hello au [https://github.com/apache/storm/tree/1.1.x-branch/examples/storm-starter](https://github.com/apache/storm/tree/1.1.x-branch/examples/storm-starter). Ce lien concerne Storm 1.1.x, qui est fourni avec HDInsight 3.6. Pour les autres versions de Storm, utilisez hello __branche__ bouton haut hello hello page tooselect une autre version de Storm.

## <a name="monitor-hello-topology"></a>Moniteur hello topologie

Bonjour Storm UI fournit une interface web pour l’utilisation des topologies en cours d’exécution et est inclus dans votre cluster HDInsight.

Utilisez hello suivant la topologie de hello toomonitor étapes à l’aide de hello Storm UI :

1. toodisplay hello Storm UI, ouvrez un web browser toohttps://CLUSTERNAME.azurehdinsight.net/stormui. Remplacez **CLUSTERNAME** avec nom hello de votre cluster.

    > [!NOTE]
    > Si vous êtes invité tooprovide un nom d’utilisateur et un mot de passe, entrez l’administrateur de cluster hello (admin) et un mot de passe que vous avez utilisé lors des cluster hello création.

2. Sous **récapitulatif de la topologie**, sélectionnez hello **wordcount** entrée Bonjour **nom** colonne. Informations sur la topologie hello s’affiche.

    ![Tableau de bord Storm avec les informations sur la topologie WordCount storm-starter.](./media/hdinsight-apache-storm-tutorial-get-started-linux/topology-summary.png)

    Cette page fournit hello informations suivantes :

    * **Statistiques de topologie** -informations de base sur les performances de topologie hello, organisés dans des fenêtres de temps.

        > [!NOTE]
        > Sélection d’une fenêtre de temps de temps spécifique fenêtre modifications hello pour les informations affichées dans d’autres sections de la page de hello.

    * **Becs verseurs amovibles** -informations de base sur becs verseurs, y compris hello dernière erreur retournée par chaque bec.

    * **Bolts** : informations de base sur les bolts.

    * **Configuration de la topologie** -des informations détaillées sur la configuration de la topologie hello.

    Cette page fournit également des actions qui peuvent être effectuées sur la topologie de hello :

    * **Activer** : reprend le traitement d’une topologie désactivée.

    * **Désactiver** : suspend une topologie en cours d’exécution.

    * **Rééquilibrer** -ajuste le parallélisme hello de topologie de hello. Vous devez rééquilibrer les topologies en cours d’exécution une fois que vous avez modifié le nombre de hello de nœuds de cluster de hello. Rééquilibrage ajuste toocompensate de parallélisme pour le numéro d’augmenté/diminué hello de nœuds de cluster de hello. Pour plus d’informations, consultez [présentation parallélisme hello d’une topologie de Storm](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html).

    * **KILL** -met fin à une topologie Storm après hello spécifié le délai d’attente.

3. À partir de cette page, sélectionnez une entrée de hello **becs verseurs amovibles** ou **boulons** section. Pour plus d’informations à propos du composant sélectionné hello s’affiche.

    ![Tableau de bord Storm avec des informations sur les composants sélectionnés.](./media/hdinsight-apache-storm-tutorial-get-started-linux/component-summary.png)

    Cette page affiche hello informations suivantes :

    * **BEC/éclair statistiques** -informations de base sur les performances du composant hello, organisés dans des fenêtres de temps.

        > [!NOTE]
        > Sélection d’une fenêtre de temps de temps spécifique fenêtre modifications hello pour les informations affichées dans d’autres sections de la page de hello.

    * **D’entrée statistiques** (boulon uniquement) - informations sur les composants qui produisent des données consommées par un éclair de hello.

    * **Statistiques de sortie** : informations sur les données émises par ce bolt.

    * **Exécuteurs** : informations sur les instances de ce composant.

    * **Erreurs** : erreurs générées par ce composant.

4. Lorsque vous affichez les détails de hello d’un bec ou d’éclair, sélectionnez une entrée hello **Port** colonne Bonjour **exécuteurs** section tooview les détails d’une instance spécifique du composant de hello.

        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: split default ["with"]
        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: split default ["nature"]
        2015-01-27 14:18:02 b.s.d.executor [INFO] Processing received message source: split:21, stream: default, id: {}, [snow]
        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: count default [snow, 747293]
        2015-01-27 14:18:02 b.s.d.executor [INFO] Processing received message source: split:21, stream: default, id: {}, [white]
        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: count default [white, 747293]
        2015-01-27 14:18:02 b.s.d.executor [INFO] Processing received message source: split:21, stream: default, id: {}, [seven]
        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: count default [seven, 1493957]

    Dans cet exemple, hello word **sept** s’est produite 1493957 fois. Ce nombre est le nombre de fois hello a été rencontrée depuis le démarrage de cette topologie.

## <a name="stop-hello-topology"></a>Arrêter la topologie de hello

Retourner toohello **récapitulatif de la topologie** page topologie du nombre de mots hello et sélectionnez hello **Kill** bouton hello **actions de topologie** section. Lorsque vous y êtes invité, entrez 10 hello secondes toowait avant d’arrêter la topologie de hello. Après le délai d’attente hello, topologie de hello n’apparaît plus lorsque vous visitez hello **Storm UI** section du tableau de bord hello.

## <a name="delete-hello-cluster"></a>Supprimer le cluster de hello

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

Si vous rencontrez un problème lors de la création de clusters HDInsight, reportez-vous aux [exigences de contrôle d’accès](hdinsight-administer-use-portal-linux.md#create-clusters).

## <a id="next"></a>Étapes suivantes

Dans ce didacticiel d’Apache Storm, vous avez appris didacticiel hello utilisation Storm sur HDInsight. Ensuite, découvrez comment trop[basée sur Java de développer des topologies, à l’aide de Maven](hdinsight-storm-develop-java-topology.md).

Si vous êtes déjà familiarisé avec le développement basé sur Java de topologies et que vous souhaitez toodeploy un tooHDInsight de topologie existante, consultez [déployer et gérer les topologies d’Apache Storm sur HDInsight](hdinsight-storm-deploy-monitor-topology-linux.md).

Si vous êtes un développeur .NET, vous pouvez créer des topologies C# ou C#/Java hybrides à l’aide de Visual Studio. Pour plus d’informations, consultez la rubrique [Développer des topologies C# pour Apache Storm sur HDInsight en utilisant les outils Hadoop pour Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).

Par exemple, les topologies qui peuvent être utilisés avec Storm sur HDInsight, consultez hello exemple suivant :

* [Exemples de topologies pour Storm dans HDInsight](hdinsight-storm-example-topology.md)

[apachestorm]: https://storm.incubator.apache.org
[stormdocs]: http://storm.incubator.apache.org/documentation/Documentation.html
[stormstarter]: https://github.com/apache/storm/tree/master/examples/storm-starter
[stormjavadocs]: https://storm.incubator.apache.org/apidocs/
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[preview-portal]: https://portal.azure.com/
