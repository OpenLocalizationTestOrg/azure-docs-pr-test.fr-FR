---
title: "aaaExplore des données dans les tables de ruche avec les requêtes Hive | Documents Microsoft"
description: "Explorer les données dans des tables Hive à l’aide de requêtes Hive."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 0d46cea5-2b4c-4384-9bfa-fa20f6f75148
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: 2ede3d41682aa08ced19284f7a83ec95e0c2a93a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="explore-data-in-hive-tables-with-hive-queries"></a>Explorer les données dans des tables Hive avec des requêtes Hive
Ce document fournit des exemples de scripts Hive qui sont des données tooexplore utilisés dans les tables dans un cluster HDInsight Hadoop Hive.

suivant de Hello **menu** tootopics qui décrivent comment toouse outils tooexplore des données à partir de différents environnements de stockage est liée.

[!INCLUDE [cap-explore-data-selector](../../includes/cap-explore-data-selector.md)]

## <a name="prerequisites"></a>Composants requis
Cet article suppose que vous avez :

* Créé un compte Azure Storage. Pour des instructions, voir [Créer un compte Stockage Azure](../storage/common/storage-create-storage-account.md#create-a-storage-account).
* Configurer un cluster Hadoop personnalisée avec hello service HDInsight. Si vous avez besoin d'aide, consultez [Personnaliser des clusters Hadoop Azure HDInsight pour l'analyse avancée](machine-learning-data-science-customize-hadoop-cluster.md).
* les données de salutation a été téléchargé tooHive des tables dans les clusters Azure HDInsight Hadoop. S’il n’a pas le cas, suivez les instructions de hello dans [créer et charger des tables de tooHive données](machine-learning-data-science-move-hive-tables.md) tooupload données tooHive tout d’abord les tables.
* Cluster de toohello activé l’accès à distance. Si vous avez besoin d’instructions, consultez [hello d’accès nœud principal de Hadoop Cluster](machine-learning-data-science-customize-hadoop-cluster.md#headnode).
* Si vous avez besoin d’informations sur les requêtes Hive toosubmit, consultez [comment tooSubmit requêtes Hive](machine-learning-data-science-move-hive-tables.md#submit)

## <a name="example-hive-query-scripts-for-data-exploration"></a>Exemples de scripts de requête Hive pour l’exploration de données
1. Obtenir le nombre de hello d’observations par partition`SELECT <partitionfieldname>, count(*) from <databasename>.<tablename> group by <partitionfieldname>;`
2. Obtenir le nombre de hello d’observations par jour`SELECT to_date(<date_columnname>), count(*) from <databasename>.<tablename> group by to_date(<date_columnname>);`
3. Obtenir des niveaux de hello dans une colonne catégorielle  
    `SELECT  distinct <column_name> from <databasename>.<tablename>`
4. Obtenir le nombre hello de niveaux dans la combinaison de deux colonnes catégorielles`SELECT <column_a>, <column_b>, count(*) from <databasename>.<tablename> group by <column_a>, <column_b>`
5. Obtenir distribution hello pour les colonnes numériques  
    `SELECT <column_name>, count(*) from <databasename>.<tablename> group by <column_name>`
6. Extraire les enregistrements à partir de la jointure des deux tables
   
        SELECT
            a.<common_columnname1> as <new_name1>,
            a.<common_columnname2> as <new_name2>,
            a.<a_column_name1> as <new_name3>,
            a.<a_column_name2> as <new_name4>,
            b.<b_column_name1> as <new_name5>,
            b.<b_column_name2> as <new_name6>
        FROM
            (
            SELECT <common_columnname1>,
                <common_columnname2>,
                <a_column_name1>,
                <a_column_name2>,
            FROM <databasename>.<tablename1>
            ) a
            join
            (
            SELECT <common_columnname1>,
                <common_columnname2>,
                <b_column_name1>,
                <b_column_name2>,
            FROM <databasename>.<tablename2>
            ) b
            ON a.<common_columnname1>=b.<common_columnname1> and a.<common_columnname2>=b.<common_columnname2>

## <a name="additional-query-scripts-for-taxi-trip-data-scenarios"></a>Scripts de requête supplémentaires pour les scénarios de données de courses de taxi
Exemples de requêtes qui sont spécifiques à trop[NYC Taxi voyage données](http://chriswhong.com/open-data/foil_nyc_taxi/) scénarios sont également fournis dans [référentiel GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts). Ces requêtes déjà le schéma de données spécifié et sont prêt toobe soumis toorun.

