---
title: aaaAccess application des fils de Hadoop enregistre par programmation - Azure | Documents Microsoft
description: "Accéder aux journaux des applications par programmation sur un cluster Hadoop dans HDInsight."
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 0198d6c9-7767-4682-bd34-42838cf48fc5
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: 064efee1ea6a864c29ab897692ead0152c926c0b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="access-yarn-application-logs-on-windows-based-hdinsight"></a>Accéder aux journaux des applications YARN dans HDInsight sous Windows
Cette rubrique explique comment tooaccess hello journaux pour les applications de fils (encore une autre ressource négociateur) qui ont terminé sur un cluster Hadoop basé sur Windows dans Azure HDInsight

> [!IMPORTANT]
> les informations de Hello dans ce document s’appliquent en fonction de tooWindows uniquement des clusters HDInsight. Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure. Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement). Pour plus d'informations sur l'accès aux journaux YARN sur les clusters HDInsight sous Linux, consultez [Accès aux journaux d'application YARN basés sur Hadoop Linux sous HDInsight](hdinsight-hadoop-access-yarn-app-logs-linux.md)
>


### <a name="prerequisites"></a>Conditions préalables
* Un cluster HDInsight Windows  Voir [Création de clusters Hadoop basés sur Windows dans HDInsight](hdinsight-hadoop-provision-linux-clusters.md).

## <a name="yarn-timeline-server"></a>YARN Timeline Server
Hello <a href="http://hadoop.apache.org/docs/r2.4.0/hadoop-yarn/hadoop-yarn-site/TimelineServer.html" target="_blank">fils chronologie Server</a> fournit des informations génériques sur les applications terminées informations ainsi que spécifiques à l’infrastructure de l’application via deux interfaces différentes. Plus précisément :

* Le stockage et la récupération d’informations génériques sur les applications sur les clusters HDInsight sont activés dans les versions 3.1.1.374 ou ultérieures.
* élément d’informations spécifiques à l’infrastructure application Hello Hello chronologie serveur n’est pas disponible actuellement sur les clusters HDInsight.

Informations générales sur les applications incluent hello suivant trie des données :

* ID d’application Hello, un identificateur unique d’une application
* utilisateur Hello qui a démarré l’application hello
* Pour plus d’informations sur les tentatives effectuées application hello de toocomplete
* conteneurs Hello utilisées par toute tentative d’application donnée

Sur vos clusters HDInsight, ces informations sont stockées par le magasin de l’historique tooa Azure Resource Manager dans un conteneur par défaut hello de votre compte de stockage Azure par défaut. Vous pouvez récupérer ces données génériques sur les applications terminées via une API REST :

    GET on https://<cluster-dns-name>.azurehdinsight.net/ws/v1/applicationhistory/apps


## <a name="yarn-applications-and-logs"></a>Applications et journaux YARN
YARN (Yet Another Resource Negotiator) prend en charge plusieurs modèles de programmation (dont MapReduce) en séparant la gestion des ressources de la planification et de l’analyse des applications. YARN se compose d’un gestionnaire de ressources (RM, *Resource Manager*) global, de gestionnaires de nœuds (NM, *Node Manager*) pour chaque nœud de travail, ainsi que de maîtres d’application (AM, *Application Master*) pour chaque application. Hello par application AM négocie ressources (processeur, mémoire, disque, réseau) pour l’exécution de votre application avec le Gestionnaire de ressources hello. Hello RM fonctionne avec NMs toogrant ces ressources, qui sont accordées en tant que *conteneurs*. Hello AM est responsable du suivi des progrès hello de hello conteneurs assignés tooit par le Gestionnaire de ressources hello. Une application peut nécessiter de nombreux conteneurs selon la nature hello de l’application hello.

En outre, chaque application peut se composer de plusieurs *tentatives application* dans l’ordre des toofinish en présence de hello de pannes ou en raison de la perte de toohello de communication entre un AM et un gestionnaire de ressources. Par conséquent, les conteneurs sont accordées tooa de tentative spécifique d’une application. Dans un sens, un conteneur fournit le contexte de hello pour l’unité de base du travail effectué par une application fils et tout le travail est effectué dans le contexte de hello d’un conteneur est effectué sur le nœud de travail unique hello sur quel hello conteneur a été alloué. Pour plus d’informations, consultez la rubrique [Concepts relatifs à YARN][YARN-concepts].

Journaux de l’application (et journaux du conteneur hello associé) sont critiques dans le débogage des applications Hadoop problématiques. FILS fournit une infrastructure intéressante pour la collecte, l’agrégation et le stockage des journaux d’application hello [journal agrégation] [ log-aggregation] fonctionnalité. fonction d’agrégation de journal Hello rend l’accès aux journaux d’application plus déterministe, il regroupe les journaux sur tous les conteneurs sur un nœud de travail et les stocke sous la forme d’un fichier journal agrégées par nœud de travail sur le système de fichiers par défaut hello à l’issue de l’exécution d’une application. Votre application peut utiliser des centaines, voire des milliers de conteneurs, mais les journaux pour tous les conteneurs s’exécutent sur un nœud de travail unique sera toujours tooa agrégée fichier unique, qui en résulte dans un fichier journal par nœud de travail utilisé par votre application. Agrégation de journal est activée par défaut sur les clusters HDInsight (version 3.0 et versions ultérieures), et agrégées journaux se trouvent dans un conteneur par défaut hello de votre cluster à hello l’emplacement suivant :

    wasb:///app-logs/<user>/logs/<applicationId>

Dans cet emplacement, *utilisateur* hello nom de hello utilisateur qui a démarré l’application hello, et *applicationId* est l’identificateur unique de hello d’une application assigné par le Gestionnaire de ressources hello fils.

Hello agrégées journaux ne sont pas directement accessible en lecture, qu’ils sont écrits un [TFile][T-file], [format binaire] [ binary-format] indexé par le conteneur. FILS fournit CLI outils toodump ces journaux au format texte brut pour des applications ou des conteneurs d’intérêt. Vous pouvez afficher ces journaux sous forme de texte brut en exécutant un de hello suivant les commandes de fils directement sur les nœuds de cluster hello (après connexion tooit via RDP) :

    yarn logs -applicationId <applicationId> -appOwner <user-who-started-the-application>
    yarn logs -applicationId <applicationId> -appOwner <user-who-started-the-application> -containerId <containerId> -nodeAddress <worker-node-address>


## <a name="yarn-resourcemanager-ui"></a>Interface utilisateur de ResourceManager YARN
Bonjour fils ResourceManager UI s’exécute sur le nœud principal du cluster hello et sont accessibles via hello tableau de bord de portail Azure :

1. Connectez-vous trop[portail Azure](https://portal.azure.com/).
2. Dans le menu de gauche hello, cliquez sur **Parcourir**, cliquez sur **Clusters HDInsight**, cliquez sur un cluster Windows que vous souhaitez tooaccess hello fils journaux d’application.
3. Dans le menu supérieur de hello, cliquez sur **tableau de bord**. Une page appelée **Console de requête HDInsight**s’ouvre dans un nouvel onglet.
4. À partir de la **Console de requête HDInsight**, cliquez sur l’**interface utilisateur YARN**.

[YARN-timeline-server]:http://hadoop.apache.org/docs/r2.4.0/hadoop-yarn/hadoop-yarn-site/TimelineServer.html
[log-aggregation]:http://hortonworks.com/blog/simplifying-user-logs-management-and-access-in-yarn/
[T-file]:https://issues.apache.org/jira/secure/attachment/12396286/TFile%20Specification%2020081217.pdf
[binary-format]:https://issues.apache.org/jira/browse/HADOOP-3315
[YARN-concepts]:http://hortonworks.com/blog/apache-hadoop-yarn-concepts-and-applications/
