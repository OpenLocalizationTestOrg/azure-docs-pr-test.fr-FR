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
# <a name="explore-data-in-hive-tables-with-hive-queries"></a><span data-ttu-id="d0e13-103">Explorer les données dans des tables Hive avec des requêtes Hive</span><span class="sxs-lookup"><span data-stu-id="d0e13-103">Explore data in Hive tables with Hive queries</span></span>
<span data-ttu-id="d0e13-104">Ce document fournit des exemples de scripts Hive qui sont des données tooexplore utilisés dans les tables dans un cluster HDInsight Hadoop Hive.</span><span class="sxs-lookup"><span data-stu-id="d0e13-104">This document provides sample Hive scripts that are used tooexplore data in Hive tables in an HDInsight Hadoop cluster.</span></span>

<span data-ttu-id="d0e13-105">suivant de Hello **menu** tootopics qui décrivent comment toouse outils tooexplore des données à partir de différents environnements de stockage est liée.</span><span class="sxs-lookup"><span data-stu-id="d0e13-105">hello following **menu** links tootopics that describe how toouse tools tooexplore data from various storage environments.</span></span>

[!INCLUDE [cap-explore-data-selector](../../includes/cap-explore-data-selector.md)]

## <a name="prerequisites"></a><span data-ttu-id="d0e13-106">Composants requis</span><span class="sxs-lookup"><span data-stu-id="d0e13-106">Prerequisites</span></span>
<span data-ttu-id="d0e13-107">Cet article suppose que vous avez :</span><span class="sxs-lookup"><span data-stu-id="d0e13-107">This article assumes that you have:</span></span>

* <span data-ttu-id="d0e13-108">Créé un compte Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="d0e13-108">Created an Azure storage account.</span></span> <span data-ttu-id="d0e13-109">Pour des instructions, voir [Créer un compte Stockage Azure](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span><span class="sxs-lookup"><span data-stu-id="d0e13-109">If you need instructions, see [Create an Azure Storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account)</span></span>
* <span data-ttu-id="d0e13-110">Configurer un cluster Hadoop personnalisée avec hello service HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d0e13-110">Provisioned a customized Hadoop cluster with hello HDInsight service.</span></span> <span data-ttu-id="d0e13-111">Si vous avez besoin d'aide, consultez [Personnaliser des clusters Hadoop Azure HDInsight pour l'analyse avancée](machine-learning-data-science-customize-hadoop-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="d0e13-111">If you need instructions, see [Customize Azure HDInsight Hadoop Clusters for Advanced Analytics](machine-learning-data-science-customize-hadoop-cluster.md).</span></span>
* <span data-ttu-id="d0e13-112">les données de salutation a été téléchargé tooHive des tables dans les clusters Azure HDInsight Hadoop.</span><span class="sxs-lookup"><span data-stu-id="d0e13-112">hello data has been uploaded tooHive tables in Azure HDInsight Hadoop clusters.</span></span> <span data-ttu-id="d0e13-113">S’il n’a pas le cas, suivez les instructions de hello dans [créer et charger des tables de tooHive données](machine-learning-data-science-move-hive-tables.md) tooupload données tooHive tout d’abord les tables.</span><span class="sxs-lookup"><span data-stu-id="d0e13-113">If it has not, follow hello instructions in [Create and load data tooHive tables](machine-learning-data-science-move-hive-tables.md) tooupload data tooHive tables first.</span></span>
* <span data-ttu-id="d0e13-114">Cluster de toohello activé l’accès à distance.</span><span class="sxs-lookup"><span data-stu-id="d0e13-114">Enabled remote access toohello cluster.</span></span> <span data-ttu-id="d0e13-115">Si vous avez besoin d’instructions, consultez [hello d’accès nœud principal de Hadoop Cluster](machine-learning-data-science-customize-hadoop-cluster.md#headnode).</span><span class="sxs-lookup"><span data-stu-id="d0e13-115">If you need instructions, see [Access hello Head Node of Hadoop Cluster](machine-learning-data-science-customize-hadoop-cluster.md#headnode).</span></span>
* <span data-ttu-id="d0e13-116">Si vous avez besoin d’informations sur les requêtes Hive toosubmit, consultez [comment tooSubmit requêtes Hive](machine-learning-data-science-move-hive-tables.md#submit)</span><span class="sxs-lookup"><span data-stu-id="d0e13-116">If you need instructions on how toosubmit Hive queries, see [How tooSubmit Hive Queries](machine-learning-data-science-move-hive-tables.md#submit)</span></span>

## <a name="example-hive-query-scripts-for-data-exploration"></a><span data-ttu-id="d0e13-117">Exemples de scripts de requête Hive pour l’exploration de données</span><span class="sxs-lookup"><span data-stu-id="d0e13-117">Example Hive query scripts for data exploration</span></span>
1. <span data-ttu-id="d0e13-118">Obtenir le nombre de hello d’observations par partition`SELECT <partitionfieldname>, count(*) from <databasename>.<tablename> group by <partitionfieldname>;`</span><span class="sxs-lookup"><span data-stu-id="d0e13-118">Get hello count of observations per partition  `SELECT <partitionfieldname>, count(*) from <databasename>.<tablename> group by <partitionfieldname>;`</span></span>
2. <span data-ttu-id="d0e13-119">Obtenir le nombre de hello d’observations par jour`SELECT to_date(<date_columnname>), count(*) from <databasename>.<tablename> group by to_date(<date_columnname>);`</span><span class="sxs-lookup"><span data-stu-id="d0e13-119">Get hello count of observations per day  `SELECT to_date(<date_columnname>), count(*) from <databasename>.<tablename> group by to_date(<date_columnname>);`</span></span>
3. <span data-ttu-id="d0e13-120">Obtenir des niveaux de hello dans une colonne catégorielle</span><span class="sxs-lookup"><span data-stu-id="d0e13-120">Get hello levels in a categorical column</span></span>  
    `SELECT  distinct <column_name> from <databasename>.<tablename>`
4. <span data-ttu-id="d0e13-121">Obtenir le nombre hello de niveaux dans la combinaison de deux colonnes catégorielles`SELECT <column_a>, <column_b>, count(*) from <databasename>.<tablename> group by <column_a>, <column_b>`</span><span class="sxs-lookup"><span data-stu-id="d0e13-121">Get hello number of levels in combination of two categorical columns  `SELECT <column_a>, <column_b>, count(*) from <databasename>.<tablename> group by <column_a>, <column_b>`</span></span>
5. <span data-ttu-id="d0e13-122">Obtenir distribution hello pour les colonnes numériques</span><span class="sxs-lookup"><span data-stu-id="d0e13-122">Get hello distribution for numerical columns</span></span>  
    `SELECT <column_name>, count(*) from <databasename>.<tablename> group by <column_name>`
6. <span data-ttu-id="d0e13-123">Extraire les enregistrements à partir de la jointure des deux tables</span><span class="sxs-lookup"><span data-stu-id="d0e13-123">Extract records from joining two tables</span></span>
   
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

## <a name="additional-query-scripts-for-taxi-trip-data-scenarios"></a><span data-ttu-id="d0e13-124">Scripts de requête supplémentaires pour les scénarios de données de courses de taxi</span><span class="sxs-lookup"><span data-stu-id="d0e13-124">Additional query scripts for taxi trip data scenarios</span></span>
<span data-ttu-id="d0e13-125">Exemples de requêtes qui sont spécifiques à trop[NYC Taxi voyage données](http://chriswhong.com/open-data/foil_nyc_taxi/) scénarios sont également fournis dans [référentiel GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts).</span><span class="sxs-lookup"><span data-stu-id="d0e13-125">Examples of queries that are specific too[NYC Taxi Trip Data](http://chriswhong.com/open-data/foil_nyc_taxi/) scenarios are also provided in [GitHub repository](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts).</span></span> <span data-ttu-id="d0e13-126">Ces requêtes déjà le schéma de données spécifié et sont prêt toobe soumis toorun.</span><span class="sxs-lookup"><span data-stu-id="d0e13-126">These queries already have data schema specified and are ready toobe submitted toorun.</span></span>

