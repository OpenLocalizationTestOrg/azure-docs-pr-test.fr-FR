---
title: "Analyse des données de capteur au moyen de Hive et de Hadoop - HDInsight | Microsoft Docs"
description: "Découvrez comment analyser des données de capteur au moyen de la console de requête Hive avec HDInsight (Hadoop), puis visualiser les données dans Microsoft Excel avec Power View."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: a8ac160c-1cef-45d9-bf36-7beb5a439105
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/14/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: d4d216cd1d8de7c86f71d0181270607e12f761cf
ms.sourcegitcommit: f8437edf5de144b40aed00af5c52a20e35d10ba1
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/03/2017
---
# <a name="analyze-sensor-data-using-the-hive-query-console-on-hadoop-in-hdinsight"></a>Analyse des données de capteur à l’aide de la console de requête Hive sur Hadoop dans HDInsight

Découvrez comment analyser des données de capteur au moyen de la console de requête Hive avec HDInsight (Hadoop), puis visualiser les données dans Microsoft Excel à l’aide de Power View.

> [!IMPORTANT]
> Les étapes décrites dans ce document fonctionnent uniquement avec les clusters HDInsight Windows. HDInsight est uniquement disponible sur Windows pour les versions antérieures à HDInsight 3.4. Linux est le seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure. Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](../hdinsight-component-versioning.md#hdinsight-windows-retirement).


Dans cet exemple, vous utilisez Hive pour traiter les données historiques et identifier les problèmes relatifs aux systèmes de chauffage et de climatisation. Plus précisément, vous identifiez les systèmes qui ne sont pas en mesure de maintenir de façon fiable une température donnée en effectuant les tâches suivantes :

* Créer des tables HIVE pour interroger des données stockées dans des fichiers au format CSV.
* Créer des requêtes HIVE pour analyser les données.
* Utiliser Microsoft Excel pour vous connecter à HDInsight et extraire les données analysées.
* Utiliser Power View pour visualiser les données.

![A diagram of the solution architecture](./media/apache-hive-analyze-sensor-data/hvac-architecture.png)

## <a name="prerequisites"></a>Composants requis

* Un cluster HDInsight (Hadoop) : consultez la rubrique [Créer des clusters Hadoop dans HDInsight](../hdinsight-hadoop-provision-linux-clusters.md) pour des informations sur la création d’un cluster.
* Microsoft Excel 2013

  > [!NOTE]
  > Microsoft Excel est utilisé pour la visualisation des données avec [Power View](https://support.office.com/Article/Power-View-Explore-visualize-and-present-your-data-98268d31-97e2-42aa-a52b-a68cf460472e?ui=en-US&rs=en-US&ad=US).

* [Pilote ODBC Microsoft Hive](http://www.microsoft.com/download/details.aspx?id=40886)

## <a name="to-run-the-sample"></a>Exécution de l'exemple

1. À partir d’un navigateur web, accédez à l'URL suivante : 

         https://<clustername>.azurehdinsight.net

    Remplacez `<clustername>` par le nom de votre cluster HDInsight :

    À l’invite, authentifiez-vous au moyen du nom d’utilisateur et du mot de passe d’administrateur que vous avez utilisés lors de l’approvisionnement de ce cluster.

2. Dans la page web qui s’ouvre, cliquez sur l’onglet **Galerie de mise en route**, puis sous la catégorie **Solutions avec des exemples de données**, cliquez sur l’exemple **Analyse des données de capteur**.

    ![Image Galerie de mise en route](./media/apache-hive-analyze-sensor-data/getting-started-gallery.png)

3. Suivez les instructions fournies dans la page web pour terminer l'exemple.
