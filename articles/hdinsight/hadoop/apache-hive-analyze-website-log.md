---
title: "Utilisation de Hive avec Hadoop pour l’analyse des journaux de site web - Azure HDInsight | Microsoft Docs"
description: "Découvrez comment utiliser Hive avec HDInsight pour analyser les journaux de site web. Vous allez utiliser un fichier journal en tant qu'entrée dans une table HDInsight, puis faire appel à HiveQL pour interroger les données."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 6fb7b5c2-8df4-40b1-a9e2-6815080004f9
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/17/2016
ms.author: nitinme
ROBOTS: NOINDEX
ms.openlocfilehash: 5aabb69dc233dfd927c1d6cc1b131115e2d096d4
ms.sourcegitcommit: f8437edf5de144b40aed00af5c52a20e35d10ba1
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/03/2017
---
# <a name="use-hive-with-windows-based-hdinsight-to-analyze-logs-from-websites"></a>Utiliser Hive avec HDInsight Windows pour analyser les journaux de site web
Découvrez comment utiliser HiveQL avec HDInsight pour analyser les journaux d'un site web. L’analyse des journaux de site web permet de segmenter votre public en fonction d’activités similaires, de classer les visiteurs d’un site sur la base de données démographiques, d’identifier le contenu qu’ils affichent, les sites web qu’ils ont visités avant, etc.

> [!IMPORTANT]
> Les étapes décrites dans ce document fonctionnent uniquement avec les clusters HDInsight Windows. HDInsight est uniquement disponible sur Windows pour les versions antérieures à HDInsight 3.4. Linux est le seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure. Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](../hdinsight-component-versioning.md#hdinsight-windows-retirement).

Dans cet exemple, vous utilisez un cluster HDInsight pour analyser des fichiers journaux de site web afin d’obtenir des informations sur la fréquence des accès au site web en une journée à partir de sites web externes. Vous générez également un résumé des erreurs de site web rencontrées par les utilisateurs. Vous allez apprendre à effectuer les actions suivantes :

* Vous connecter à un stockage d’objets blob Azure contenant des fichiers journaux de site web.
* Créer des tables HIVE pour interroger ces journaux.
* Créer des requêtes HIVE pour analyser les données.
* Utiliser Microsoft Excel pour vous connecter à HDInsight (au moyen d’une connexion ODBC) pour extraire les données analysées.

![HDI.Samples.Website.Log.Analysis](./media/apache-hive-analyze-website-log/hdinsight-weblogs-sample.png)

## <a name="prerequisites"></a>Composants requis
* Vous devez avoir approvisionné un cluster Hadoop sur Azure HDInsight. Pour plus d’informations, consultez la rubrique [Provisionner des clusters HDInsight](../hdinsight-hadoop-provision-linux-clusters.md).
* Microsoft Excel 2013 ou Microsoft Excel 2010 doivent être installés.
* Vous devez disposer d'un [pilote ODBC Microsoft Hive](http://www.microsoft.com/download/details.aspx?id=40886) pour importer des données à partir de Hive dans Excel.

## <a name="to-run-the-sample"></a>Exécution de l'exemple
1. Dans le [portail Azure](https://portal.azure.com/), depuis le tableau d’accueil (si vous y avez épinglé le cluster), cliquez sur la vignette du cluster sur lequel vous souhaitez exécuter l’exemple.
2. Dans le panneau du cluster, sous **Liens rapides**, cliquez sur **Tableau de bord du cluster**, puis dans le panneau **Tableau de bord du cluster**, cliquez sur **Tableau de bord de cluster HDInsight**. Vous pouvez également ouvrir directement le tableau de bord en utilisant l'URL suivante :

         https://<clustername>.azurehdinsight.net

    À l’invite, authentifiez-vous au moyen du nom d’utilisateur et du mot de passe d’administrateur que vous avez utilisés lors de l’approvisionnement du cluster.
3. Dans la page web qui s’ouvre, cliquez sur l’onglet **Galerie de mise en route**, puis sous la catégorie **Solutions avec des exemples de données**, cliquez sur l’exemple **Analyse du journal du site web**.
4. Suivez les instructions fournies dans la page web pour terminer l'exemple.

## <a name="next-steps"></a>Étapes suivantes
Essayez l’exemple suivant : [Analyse des données de capteur au moyen de Hive avec HDInsight](apache-hive-analyze-sensor-data.md).

[hdinsight-sensor-data-sample]: ../hdinsight-use-hive-sensor-data-analysis.md
