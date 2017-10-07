---
title: "aaaUse Hive avec Hadoop pour l’analyse du journal du site Web - Azure HDInsight | Documents Microsoft"
description: "Découvrez comment toouse Hive avec un site Web de HDInsight tooanalyze se connecte. Vous allez utiliser un fichier journal en tant qu’entrée dans une table HDInsight et utilisent des données de HiveQL tooquery hello."
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
ms.openlocfilehash: 9cbce3cc8cf8bc3ad104dc4ca6a5628802c8fe89
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hive-with-windows-based-hdinsight-tooanalyze-logs-from-websites"></a>Utilisez la ruche avec des journaux de tooanalyze HDInsight de basé sur Windows à partir de sites Web
Découvrez comment toouse HiveQL avec HDInsight tooanalyze se connecte à partir d’un site Web. L’analyse du journal du site Web peut être utilisé toosegment votre audience en fonction d’activités similaires, classer les visiteurs du site par les données démographiques et toofind contenus hello qu’ils affichent, ils proviennent des sites Web hello et ainsi de suite.

> [!IMPORTANT]
> les étapes dans ce travail seul document avec des clusters HDInsight de basés sur Windows Hello. HDInsight est uniquement disponible sur Windows pour les versions antérieures à HDInsight 3.4. Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure. Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

Dans cet exemple, vous allez utiliser une HDInsight cluster tooanalyze site Web du journal des fichiers tooget idée fréquence hello du site Web de toohello visites à partir des sites Web externes dans un jour. Vous allez également générer un résumé des erreurs de site Web que les utilisateurs de hello rencontrer. Vous apprendrez à :

* Se connecter tooa stockage d’objets Blob Azure, qui contient les fichiers journaux du site Web.
* Créer des tables ruche tooquery ces journaux.
* Créer des requêtes HIVE tooanalyze les données de salutation.
* Utiliser Microsoft Excel tooconnect tooHDInsight (à l’aide de la base de données ouverte (ODBC) tooretrieve hello analysé les données de connectivité.

![HDI.Samples.Website.Log.Analysis][img-hdi-weblogs-sample]

## <a name="prerequisites"></a>Composants requis
* Vous devez avoir approvisionné un cluster Hadoop sur Azure HDInsight. Pour plus d’informations, consultez la rubrique [Approvisionnement de clusters HDInsight][hdinsight-provision].
* Microsoft Excel 2013 ou Microsoft Excel 2010 doivent être installés.
* Vous devez avoir [Microsoft ODBC Driver de la ruche](http://www.microsoft.com/download/details.aspx?id=40886) tooimport des données à partir de la ruche dans Excel.

## <a name="toorun-hello-sample"></a>hello, exemple toorun
1. À partir de hello [Azure Portal](https://portal.azure.com/), à partir du tableau d’accueil (si vous avez épinglé cluster hello) de hello, cliquez sur la vignette de cluster hello sur lequel vous souhaitez toorun hello exemple.
2. À partir de hello cluster panneau, sous **liens rapides**, cliquez sur **tableau de bord de Cluster**, puis à partir de hello **tableau de bord de Cluster** panneau, cliquez sur **HDInsight Cluster Tableau de bord**. Ou bien, vous pouvez ouvrir directement du tableau de bord hello à l’aide de hello suivant l’URL :

         https://<clustername>.azurehdinsight.net

    Lorsque vous y êtes invité, s’authentifier en utilisant le nom d’utilisateur administrateur hello et le mot de passe utilisé lors de la configuration de cluster de hello.
3. À partir de la page web hello qui s’ouvre, cliquez sur hello **prise en main galerie** onglet, puis, sous hello **Solutions avec des exemples de données** catégorie, cliquez sur hello **l’analyse du journal du site Web** exemple.
4. Suivez les instructions hello de toofinish hello exemple hello page web.

## <a name="next-steps"></a>Étapes suivantes
Essayez de hello suivant l’exemple : [analyse des données de capteur à l’aide de la ruche hdinsight](hdinsight-hive-analyze-sensor-data.md).

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-sensor-data-sample]: ../hdinsight-use-hive-sensor-data-analysis.md

[img-hdi-weblogs-sample]: ./media/hdinsight-hive-analyze-website-log/hdinsight-weblogs-sample.png
