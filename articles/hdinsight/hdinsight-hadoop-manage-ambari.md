---
title: "aaaMonitor et gérer Azure HDInsight à l’aide de l’interface utilisateur de Ambari Web | Documents Microsoft"
description: "Découvrez comment toouse Ambari toomonitor et gérer des clusters HDInsight de basés sur Linux. Dans ce document, vous découvrez comment les clusters toouse hello l’interface utilisateur Web de Ambari inclus avec HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 4787f3cc-a650-4dc3-9d96-a19a67aad046
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: d422c40e63345d7054839a625e115c50dad040f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hdinsight-clusters-by-using-hello-ambari-web-ui"></a>Gérer des clusters HDInsight à l’aide de hello Ambari Web UI

[!INCLUDE [ambari-selector](../../includes/hdinsight-ambari-selector.md)]

Apache Ambari simplifie la gestion de hello et la surveillance d’un cluster Hadoop en fournissant un web toouse simple API REST et de l’interface utilisateur. Ambari est inclus sur les clusters HDInsight de basés sur Linux et est utilisé toomonitor hello cluster et apporter des modifications de configuration.

Dans ce document, vous découvrez comment toouse hello l’interface utilisateur de Ambari Web avec un cluster HDInsight.

## <a id="whatis"></a>Présentation d'Ambari

[Apache Ambari](http://ambari.apache.org) simplifie la gestion d’Hadoop grâce à une interface utilisateur web facile à utiliser. Vous pouvez utiliser Ambari pour créer, gérer et surveiller les clusters Hadoop. Les développeurs peuvent intégrer ces fonctionnalités dans leurs applications à l’aide de hello [API REST de Ambari](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).

Hello l’interface utilisateur de Ambari Web est fourni par défaut avec les clusters HDInsight qui utilisent le système d’exploitation de Linux hello.

> [!IMPORTANT]
> Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure. Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement). 

## <a name="connectivity"></a>Connectivité

Hello l’interface utilisateur de Ambari Web est disponible sur votre cluster HDInsight à HTTPS://CLUSTERNAME.azurehdidnsight.net, où **CLUSTERNAME** est le nom hello de votre cluster.

> [!IMPORTANT]
> Connexion tooAmbari sur HDInsight nécessite HTTPS. Lorsque vous y êtes invité pour l’authentification, utilisez le nom de compte d’administrateur hello et le mot de passe fourni lors de la création de cluster de hello.

## <a name="ssh-tunnel-proxy"></a>Tunnel SSH (proxy)

Alors que Ambari pour votre cluster est accessible directement sur hello Internet, des liens à partir de hello l’interface utilisateur de Ambari Web (par exemple, toohello JobTracker) ne sont pas exposés sur hello internet. tooaccess ces services, vous devez créer un tunnel SSH. Pour plus d’informations, consultez [Utilisation du tunneling SSH avec HDInsight](hdinsight-linux-ambari-ssh-tunnel.md).

## <a name="ambari-web-ui"></a>Interface utilisateur web d'Ambari

Lors de la connexion toohello l’interface utilisateur de Ambari Web, vous êtes invité à tooauthenticate toohello page. Utilisateur d’administrateur de cluster de hello utilisation (par défaut, administrateur) et le mot de passe que vous avez utilisé lors de la création du cluster.

Lors de la page de hello s’ouvre, notez barre hello haut hello. Cette barre contient des éléments suivants de hello plus d’informations et des contrôles :

![ambari-nav](./media/hdinsight-hadoop-manage-ambari/ambari-nav.png)

* **Logo de Ambari** -tableau de bord de hello s’ouvre, ce qui peut être utilisé toomonitor hello cluster.

* **Ops # de nom de cluster** -affiche le nombre hello des opérations de Ambari en cours. Nom de cluster en sélectionnant hello ou **ops de #** affiche une liste des opérations d’arrière-plan.

* **alertes de #** -affiche les avertissements ou les alertes critiques, le cas échéant, pour un cluster de hello.

* **Tableau de bord** -tableau de bord affiche hello.

* **Services** -informations et la configuration des paramètres pour les services cluster de hello hello.

* **Hôtes** -informations et la configuration des paramètres pour les nœuds dans le cluster de hello hello.

* **Alertes** : journal contenant informations, avertissements et alertes critiques.

* **Administrateur** -pile/services logiciels qui sont installés sur le cluster de hello, les informations de compte de service et la sécurité Kerberos.

* **Bouton Administrateur** : gestion d'Ambari, paramètres utilisateur et déconnexion.

## <a name="monitoring"></a>Surveillance

### <a name="alerts"></a>Alertes

Hello liste suivante contient des États alerte courantes hello utilisés par Ambari :

* **OK**
* **Avertissement**
* **CRITIQUE**
* **INCONNU**

Autres que des alertes **OK** provoquer hello **les alertes #** entrée haut hello hello numéro de page toodisplay hello d’alertes. Cette entrée affiche les alertes hello et leur état.

Les alertes sont organisés en plusieurs groupes par défaut, qui peuvent être affichés à partir de hello **alertes** page.

![page d’alertes](./media/hdinsight-hadoop-manage-ambari/alerts.png)

Vous pouvez gérer les groupes de hello à l’aide de hello **Actions** menu et en sélectionnant **gérer les groupes d’alerte**.

![gérer des groupes d'alertes, boîte de dialogue](./media/hdinsight-hadoop-manage-ambari/manage-alerts.png)

Vous pouvez également gérer les méthodes d’alerte et créer des notifications d’alerte à partir de hello **Actions** menu en sélectionnant __gérer les Notifications d’alerte__. Les notifications en cours sont affichées. Vous pouvez également créer des notifications à partir d’ici. Les notifications peuvent être envoyées via **EMAIL** ou **SNMP** lorsque des combinaisons spécifiques alerte/gravité se produisent. Par exemple, vous pouvez envoyer un message électronique lorsqu’un des alertes de hello Bonjour **fils par défaut** groupe est défini trop**critique**.

![créer une alerte, boîte de dialogue](./media/hdinsight-hadoop-manage-ambari/create-alert-notification.png)

Enfin, en sélectionnant __gérer les paramètres d’alerte__ de hello __Actions__ menu vous permet de nombre de hello tooset d’occurrences d’une alerte avant une notification est envoyée. Ce paramètre peut être utilisé tooprevent des notifications pour les erreurs temporaires.

### <a name="cluster"></a>Cluster

Hello **métriques** du tableau de bord hello contient une série de widgets qui la rendent l’état de hello toomonitor facile de votre cluster en un coup de œil. Plusieurs widgets, tels que **Utilisation du processeur**, fournissent des informations supplémentaires lorsque vous cliquez dessus.

![tableau de bord avec des mesures](./media/hdinsight-hadoop-manage-ambari/metrics.png)

Hello **Heatmaps** onglet affiche les métriques comme couleur heatmaps, allant de toored vert.

![tableau de bord avec des cartes thermiques](./media/hdinsight-hadoop-manage-ambari/heatmap.png)

Pour plus d’informations sur les nœuds de hello au sein du cluster de hello, sélectionnez **hôtes**. Puis sélectionnez le nœud spécifique de hello que vous intéressez.

![détails de l'hôte](./media/hdinsight-hadoop-manage-ambari/host-details.png)

### <a name="services"></a>Services

Hello **Services** encadré sur le tableau de bord hello fournit un aperçu rapide des état hello de services hello en cours d’exécution sur le cluster de hello. Des icônes différentes sont utilisées tooindicate état ou les actions qui doivent être prises. Par exemple, un symbole de recyclage jaune s’affiche si un service doit toobe de recyclage.

![barre latérale des services](./media/hdinsight-hadoop-manage-ambari/service-bar.png)

> [!NOTE]
> services Hello affichées varient entre les versions et les types de cluster HDInsight. services Hello affichés ici peuvent être différentes de celle des services hello affichées pour votre cluster.

Sélection d’un service affiche des informations plus détaillées sur le service de hello.

![informations de résumé du service](./media/hdinsight-hadoop-manage-ambari/service-details.png)

#### <a name="quick-links"></a>Liens rapides

Affichage de certains services une **liens rapides** lien en hello haut hello. Cela peut être utilisé tooaccess web de spécifique au service interfaces utilisateur, tel que :

* **Historique des travaux** : historique des travaux MapReduce.
* **Gestionnaire des ressources** : interface utilisateur du gestionnaire des ressources YARN.
* **NameNode** : interface utilisateur NameNode HDFS.
* **Interface utilisateur web Oozie** : interface utilisateur Oozie.

En sélectionnant une de ces liaisons, un nouvel onglet s’ouvre dans votre navigateur, qui affiche la page sélectionnée de hello.

> [!NOTE]
> En sélectionnant hello **liens rapides** entrée pour un service peut retourner une erreur « serveur introuvable ». Si vous rencontrez cette erreur, vous devez utiliser un tunnel SSH lors de l’utilisation de hello **liens rapides** entrée pour ce service. Pour plus d’informations, consultez [Utilisation du tunneling SSH avec HDInsight](hdinsight-linux-ambari-ssh-tunnel.md).

## <a name="management"></a>Gestion

### <a name="ambari-users-groups-and-permissions"></a>Utilisateurs d'Ambari, groupes et autorisations

Il est possible de travailler avec des utilisateurs, des groupes et des autorisations lorsque vous utilisez un cluster HDInsight [joint au domaine](hdinsight-domain-joined-introduction.md). Pour plus d’informations sur l’utilisation de hello Ambari interface utilisateur de gestion sur un cluster à un domaine, consultez [gérer appartenant au domaine des clusters HDInsight](hdinsight-domain-joined-introduction.md).

> [!WARNING]
> Ne modifiez pas le mot de passe hello de surveillance de Ambari hello (hdinsightwatchdog) sur votre cluster HDInsight de basés sur Linux. Modification des sauts de mot de passe hello hello des actions de script toouse capacité ou effectuer des opérations de mise à l’échelle avec votre cluster.

### <a name="hosts"></a>Hôtes

Hello **hôtes** page répertorie tous les hôtes de cluster de hello. toomanage hôtes, procédez comme suit.

![page d'hôtes](./media/hdinsight-hadoop-manage-ambari/hosts.png)

> [!NOTE]
> L’ajout, la désactivation et la remise en service d’un hôte ne doivent pas être utilisés avec des clusters HDInsight.

1. Sélectionnez l’hôte hello que vous souhaitez toomanage.

2. Hello d’utilisation **Actions** action de hello tooselect de menu que vous souhaitez tooperform :

   * **Démarrer tous les composants** -démarrer tous les composants sur l’ordinateur hôte de hello.

   * **Arrêter tous les composants** -arrêter tous les composants sur l’ordinateur hôte de hello.

   * **Redémarrez tous les composants** - arrêter et démarrer tous les composants sur l’ordinateur hôte de hello.

   * **Activer le mode de maintenance** -supprime les alertes pour les hôtes hello. Ce mode doit être activé si vous effectuez des actions qui génèrent des alertes. Par exemple, l’arrêt et le démarrage d’un service.

   * **Désactiver le mode de maintenance** -renvoie hello d’alerte de toonormal hôte.

   * **Arrêter** -arrêt DataNode ou NodeManagers sur l’ordinateur hôte de hello.

   * **Démarrer** -démarre le DataNode ou NodeManagers sur l’ordinateur hôte de hello.

   * **Redémarrez** -s’arrête et démarre DataNode ou NodeManagers sur l’ordinateur hôte de hello.

   * **Désaffecter** -supprime un ordinateur hôte en cluster de hello.

     > [!NOTE]
     > N'utilisez pas cette action sur les clusters HDInsight.

   * **Recommission** -ajoute un cluster de toohello hôte précédemment mis hors service.

     > [!NOTE]
     > N'utilisez pas cette action sur les clusters HDInsight.

### <a id="service"></a>Services

À partir de hello **tableau de bord** ou **Services** page, utilisez hello **Actions** situé en bas de hello de liste hello de services toostop et démarrer tous les services.

![Actions de service](./media/hdinsight-hadoop-manage-ambari/service-actions.png)

> [!WARNING]
> Alors que **ajouter un Service** est répertorié dans ce menu ne doit pas être le cluster HDInsight de tooadd utilisé services toohello. Les nouveaux services doivent être ajoutés à l'aide d'une action de script lors de l’approvisionnement du cluster. Pour plus d’informations sur l’utilisation des actions de script, consultez [Personnaliser des clusters HDInsight à l’aide d’actions de script](hdinsight-hadoop-customize-cluster-linux.md).

Lors de hello **Actions** bouton peut redémarrer tous les services, la fréquence à laquelle vous souhaitez toostart, arrêter ou redémarrer un service spécifique. Utilisez hello suivant des actions de tooperform étapes sur chaque service :

1. À partir de hello **tableau de bord** ou **Services** , sélectionnez un service.

2. À partir du haut hello Hello **Résumé** utiliser hello, onglet **Actions Service** bouton et sélectionnez hello action tootake. Cette action redémarre le service hello sur tous les nœuds.

    ![action de service](./media/hdinsight-hadoop-manage-ambari/individual-service-actions.png)

   > [!NOTE]
   > Le redémarrage de certains services pendant l’exécution du cluster de hello peut générer des alertes. tooavoid des alertes, vous pouvez utiliser hello **Actions Service** bouton tooenable **mode Maintenance** service hello avant d’effectuer le redémarrage de hello.

3. Une fois qu’une action a été sélectionnée, hello **op de #** entrée haut hello tooshow par incréments de page hello qu’une opération d’arrière-plan est en cours. Si configuré toodisplay, liste hello des opérations d’arrière-plan s’affiche.

   > [!NOTE]
   > Si vous avez activé **mode Maintenance** pour le service de hello, n’oubliez pas de toodisable à l’aide de hello **Actions Service** bouton une fois l’opération de hello est terminée.

tooconfigure un service, utilisez hello comme suit :

1. À partir de hello **tableau de bord** ou **Services** , sélectionnez un service.

2. Sélectionnez hello **configurations** configuration actuelle de hello onglet s’affiche. Une liste des configurations précédentes est également affichée.

    ![configurations](./media/hdinsight-hadoop-manage-ambari/service-configs.png)

3. Utilisez hello champs affichés toomodify hello configuration, puis sélectionnez **enregistrer**. Ou sélectionnez une configuration précédente, puis **rendre actuel** tooroll sauvegarder toohello les paramètres précédents.

## <a name="ambari-views"></a>Affichages Ambari

Ambari vues permettent aux développeurs les éléments d’interface utilisateur tooplug dans hello l’interface utilisateur de Ambari Web à l’aide de hello [Ambari vues Framework](https://cwiki.apache.org/confluence/display/AMBARI/Views). HDInsight fournit hello suivant vues avec les types de cluster Hadoop :

* Gestionnaire de file d’attente de fils : Gestionnaire de file d’attente hello fournit une interface utilisateur simple pour afficher et modifier des files d’attente des fils.

* Ruche vue : hello la ruche de vue vous permet de toorun les requêtes Hive directement à partir de votre navigateur web. Vous pouvez enregistrer des requêtes, afficher les résultats, enregistrer les résultats de stockage de cluster toohello ou télécharger le système local tooyour de résultats. Pour plus d’informations sur l’utilisation des affichages Hive, consultez [Utiliser des affichages Hive avec HDInsight](hdinsight-hadoop-use-hive-ambari-view.md).

* Affichage de tez : hello Tez vue vous permet de toobetter comprendre et optimiser des travaux. Vous pouvez afficher des informations sur l’exécution des tâches Tez et les ressources utilisées.
