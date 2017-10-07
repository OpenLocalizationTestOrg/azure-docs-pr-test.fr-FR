---
title: "les données de capteur aaaAnalyze à l’aide de la ruche et Hadoop - Azure HDInsight | Documents Microsoft"
description: "Découvrez comment les données de capteur tooanalyze à l’aide de hello Console de requête Hive hdinsight (Hadoop), puis visualiser des données dans Microsoft Excel avec PowerView hello."
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
ms.openlocfilehash: 70e595705c33d9835dc9809161f79c3ac5ece870
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-sensor-data-using-hello-hive-query-console-on-hadoop-in-hdinsight"></a>Analyser les données de capteur à l’aide de hello Console de requête Hive sur Hadoop dans HDInsight

Découvrez comment les données de capteur tooanalyze à l’aide de hello Console de requête Hive hdinsight (Hadoop), puis visualiser les données de hello dans Microsoft Excel à l’aide de Power View.

> [!IMPORTANT]
> les étapes dans ce travail seul document avec des clusters HDInsight de basés sur Windows Hello. HDInsight est uniquement disponible sur Windows pour les versions antérieures à HDInsight 3.4. Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure. Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).


Dans cet exemple, les données d’historique tooprocess Hive et d’identifier des problèmes avec les systèmes de chauffage et la climatisation. Plus précisément, vous identifiez les systèmes sont tooreliably n’a pas pu mettre à jour une jeu de température en effectuant hello tâches suivantes :

* Créer des tables de la ruche tooquery les données stockées dans les fichiers de valeurs séparées par des virgules (CSV).
* Créer des requêtes HIVE tooanalyze les données de salutation.
* les données analysée de hello tooretrieve, utilisez tooHDInsight tooconnect de Microsoft Excel.
* les données de salutation toovisualize, utilisez Power View.

![Un diagramme d’architecture de solution hello](./media/hdinsight-hive-analyze-sensor-data/hvac-architecture.png)

## <a name="prerequisites"></a>Composants requis

* Un cluster HDInsight (Hadoop) : consultez la rubrique [Créer des clusters Hadoop dans HDInsight](hdinsight-hadoop-provision-linux-clusters.md) pour des informations sur la création d’un cluster.
* Microsoft Excel 2013

  > [!NOTE]
  > Microsoft Excel est utilisé pour la visualisation des données avec [Power View](https://support.office.com/Article/Power-View-Explore-visualize-and-present-your-data-98268d31-97e2-42aa-a52b-a68cf460472e?ui=en-US&rs=en-US&ad=US).

* [Pilote ODBC Microsoft Hive](http://www.microsoft.com/download/details.aspx?id=40886)

## <a name="toorun-hello-sample"></a>hello, exemple toorun

1. À partir de votre navigateur web, accédez à toohello suivant l’URL : 

         https://<clustername>.azurehdinsight.net

    Remplacez `<clustername>` par nom de hello de votre cluster HDInsight.

    Lorsque vous y êtes invité, s’authentifier en utilisant le nom d’utilisateur administrateur hello et le mot de passe utilisé lors de la configuration de ce cluster.

2. Hello page web qui s’ouvre, cliquez sur hello **prise en main galerie** onglet, puis sous hello **Solutions avec des exemples de données** catégorie, cliquez sur hello **analyse des données de capteur** exemple.

    ![Image Galerie de mise en route](./media/hdinsight-hive-analyze-sensor-data/getting-started-gallery.png)

3. Suivez les instructions hello de toofinish hello exemple hello page web.
