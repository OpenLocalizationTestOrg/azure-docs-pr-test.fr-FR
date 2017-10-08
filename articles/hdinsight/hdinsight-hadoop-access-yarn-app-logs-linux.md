---
title: "se connecte aaaAccess application des fils de Hadoop HDInsight basés sur Linux - Azure | Documents Microsoft"
description: "Découvrez comment application des fils tooaccess ouvre une session sur un cluster basé sur Linux HDInsight (Hadoop) à l’aide en ligne de commande de hello et un navigateur web."
services: hdinsight
documentationcenter: 
tags: azure-portal
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 3ec08d20-4f19-4a8e-ac86-639c04d2f12e
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: 0bab356e3b97114abbb05712c8e7b21a194f2508
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="access-yarn-application-logs-on-linux-based-hdinsight"></a>Accéder aux journaux des applications YARN dans HDInsight sous Linux

Découvrez comment tooaccess hello journaux pour les applications de fils (encore une autre ressource négociateur) sur un cluster Hadoop dans HDInsight de Azure.

> [!IMPORTANT]
> étapes de Hello dans ce document nécessitent un cluster HDInsight qui utilise Linux. Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure. Pour plus d’informations, consultez [Contrôle de version des composants HDInsight](hdinsight-component-versioning.md#hdinsight-windows-retirement).

## <a name="YARNTimelineServer"></a>YARN Timeline Server

Hello [fils chronologie Server](http://hadoop.apache.org/docs/r2.4.0/hadoop-yarn/hadoop-yarn-site/TimelineServer.html) fournit des informations génériques sur les applications terminées et aux informations spécifiques à l’infrastructure via deux interfaces différentes. Plus précisément :

* Le stockage et la récupération d’informations génériques sur les applications sur les clusters HDInsight sont activés dans les versions 3.1.1.374 ou ultérieures.
* élément d’informations spécifiques à l’infrastructure application Hello Hello chronologie serveur n’est pas disponible actuellement sur les clusters HDInsight.

Informations générales sur les applications incluent hello suivant le type de données :

* ID d’application Hello, un identificateur unique d’une application
* utilisateur Hello qui a démarré l’application hello
* Pour plus d’informations sur les tentatives effectuées application hello de toocomplete
* conteneurs Hello utilisées par toute tentative d’application donnée

## <a name="YARNAppsAndLogs"></a>Applications et journaux YARN

YARN (Yet Another Resource Negotiator) prend en charge plusieurs modèles de programmation (dont MapReduce) en séparant la gestion des ressources de la planification et de l’analyse des applications. YARN utilise les éléments suivant : *ResourceManager* (RM) global, *NodeManagers* (NM) par nœud worker et *ApplicationMasters* (AM) par application. Hello par application AM négocie ressources (processeur, mémoire, disque, réseau) pour l’exécution de votre application avec le Gestionnaire de ressources hello. Hello RM fonctionne avec NMs toogrant ces ressources, qui sont accordées en tant que *conteneurs*. Hello AM est responsable du suivi des progrès hello de hello conteneurs assignés tooit par le Gestionnaire de ressources hello. Une application peut nécessiter de nombreux conteneurs selon la nature hello de l’application hello.

Chaque application peut comporter plusieurs *tentatives d’application*. Si une application échoue, vous pouvez la relancer. Il s’agit alors d’une nouvelle tentative. Chaque tentative est exécutée dans un conteneur. Dans un sens, un conteneur fournit le contexte hello pour l’unité de base du travail effectué par une application fils. Tout le travail est effectué dans le contexte de hello d’un conteneur est effectué sur le nœud de travail unique hello sur quel hello conteneur a été alloué. Pour plus d’informations, consultez la rubrique [Concepts relatifs à YARN][YARN-concepts].

Journaux de l’application (et journaux du conteneur hello associé) sont critiques dans le débogage des applications Hadoop problématiques. FILS fournit une infrastructure intéressante pour la collecte, l’agrégation et le stockage des journaux d’application hello [journal agrégation] [ log-aggregation] fonctionnalité. fonction d’agrégation de journal Hello rend l’accès aux journaux d’application plus déterministe. Il regroupe les journaux de tous les conteneurs sur un nœud Worker et les stocke dans un fichier journal agrégé par nœud Worker. journal de Hello est stocké sur le système de fichiers par défaut hello à l’issue de l’exécution d’une application. Votre application peut utiliser des centaines, voire des milliers de conteneurs, mais les journaux pour s’exécuter sur un nœud de travail unique de tous les conteneurs sont toujours tooa agrégée fichier unique. Cela se traduit par l’existence d’un seul fichier journal par nœud worker utilisé par votre application. L’agrégation de journaux est activée par défaut sur les clusters HDInsight version 3.0 et versions ultérieures. Journaux agrégées sont situés dans le stockage par défaut pour le cluster de hello. Hello suivant le chemin d’accès est hello HDFS chemin d’accès toohello journaux :

    /app-logs/<user>/logs/<applicationId>

Dans le chemin d’accès de hello, `user` hello nom de hello utilisateur qui a démarré l’application hello. Hello `applicationId` est application de tooan hello identificateur unique affecté par le Gestionnaire de ressources hello fils.

Hello agrégées journaux ne sont pas directement accessible en lecture, qu’ils sont écrits un [TFile][T-file], [format binaire] [ binary-format] indexé par le conteneur. Utiliser hello que fils ResourceManager consigne ou CLI outils tooview ces journaux comme texte brut pour des applications ou des conteneurs d’intérêt.

## <a name="yarn-cli-tools"></a>Outils de l’interface de ligne de commande YARN

outils de toouse hello fils CLI, vous devez d’abord connecter cluster HDInsight de toohello à l’aide de SSH. Pour en savoir plus, voir [Utilisation de SSH avec HDInsight (Hadoop) depuis Bash (l’interpréteur de commande) sur Windows 10, Linux, Unix ou OS X](hdinsight-hadoop-linux-use-ssh-unix.md).

Vous pouvez afficher ces journaux sous forme de texte brut en exécutant un de hello suivant de commandes :

    yarn logs -applicationId <applicationId> -appOwner <user-who-started-the-application>
    yarn logs -applicationId <applicationId> -appOwner <user-who-started-the-application> -containerId <containerId> -nodeAddress <worker-node-address>

Spécifiez hello &lt;applicationId >, &lt;utilisateur qui-démarré-applications >, &lt;Id_conteneur >, et &lt;adresse du nœud de travail > informations lors de l’exécution de ces commandes.

## <a name="yarn-resourcemanager-ui"></a>Interface utilisateur de ResourceManager YARN

Hello fils ResourceManager UI s’exécute sur le nœud principal du cluster hello. Il est accessible via l’interface utilisateur web de Ambari hello. Hello utilisation suivant les étapes tooview hello fils de journaux :

1. Dans votre navigateur web, accédez à toohttps://CLUSTERNAME.azurehdinsight.net. Remplacez CLUSTERNAME par nom hello de votre cluster HDInsight.
2. À partir de la liste de hello des services sur hello gauche, sélectionnez **fils**.

    ![Service YARN sélectionné](./media/hdinsight-hadoop-access-yarn-app-logs-linux/yarnservice.png)
3. À partir de hello **liens rapides** liste déroulante, sélectionnez un des nœuds principaux d’un cluster hello puis **ResourceManager journal**.

    ![Liens rapides YARN](./media/hdinsight-hadoop-access-yarn-app-logs-linux/yarnquicklinks.png)

    Vous sont présentées avec une liste de liens tooYARN journaux.

[YARN-timeline-server]:http://hadoop.apache.org/docs/r2.4.0/hadoop-yarn/hadoop-yarn-site/TimelineServer.html
[log-aggregation]:http://hortonworks.com/blog/simplifying-user-logs-management-and-access-in-yarn/
[T-file]:https://issues.apache.org/jira/secure/attachment/12396286/TFile%20Specification%2020081217.pdf
[binary-format]:https://issues.apache.org/jira/browse/HADOOP-3315
[YARN-concepts]:http://hortonworks.com/blog/apache-hadoop-yarn-concepts-and-applications/
