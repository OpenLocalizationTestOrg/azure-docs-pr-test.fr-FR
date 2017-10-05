---
title: "Explorer les données dans des tables Hive avec des requêtes Hive | Microsoft Docs"
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
ms.openlocfilehash: 67a33a9abc3d3dcdd2fc7205e11feff97e3582a3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="explore-data-in-hive-tables-with-hive-queries"></a><span data-ttu-id="6284d-103">Explorer les données dans des tables Hive avec des requêtes Hive</span><span class="sxs-lookup"><span data-stu-id="6284d-103">Explore data in Hive tables with Hive queries</span></span>
<span data-ttu-id="6284d-104">Ce document fournit des exemples de scripts Hive qui permettent d’explorer des données dans des tables Hive dans un cluster Hadoop HDInsight.</span><span class="sxs-lookup"><span data-stu-id="6284d-104">This document provides sample Hive scripts that are used to explore data in Hive tables in an HDInsight Hadoop cluster.</span></span>

<span data-ttu-id="6284d-105">Le **menu** suivant pointe vers des rubriques qui expliquent comment utiliser des outils pour explorer des données dans différents environnements de stockage.</span><span class="sxs-lookup"><span data-stu-id="6284d-105">The following **menu** links to topics that describe how to use tools to explore data from various storage environments.</span></span>

[!INCLUDE [cap-explore-data-selector](../../includes/cap-explore-data-selector.md)]

## <a name="prerequisites"></a><span data-ttu-id="6284d-106">Composants requis</span><span class="sxs-lookup"><span data-stu-id="6284d-106">Prerequisites</span></span>
<span data-ttu-id="6284d-107">Cet article suppose que vous avez :</span><span class="sxs-lookup"><span data-stu-id="6284d-107">This article assumes that you have:</span></span>

* <span data-ttu-id="6284d-108">Créé un compte Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="6284d-108">Created an Azure storage account.</span></span> <span data-ttu-id="6284d-109">Pour des instructions, voir [Créer un compte Stockage Azure](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span><span class="sxs-lookup"><span data-stu-id="6284d-109">If you need instructions, see [Create an Azure Storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account)</span></span>
* <span data-ttu-id="6284d-110">Approvisionné un cluster Hadoop personnalisé avec le service HDInsight.</span><span class="sxs-lookup"><span data-stu-id="6284d-110">Provisioned a customized Hadoop cluster with the HDInsight service.</span></span> <span data-ttu-id="6284d-111">Si vous avez besoin d'aide, consultez [Personnaliser des clusters Hadoop Azure HDInsight pour l'analyse avancée](machine-learning-data-science-customize-hadoop-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="6284d-111">If you need instructions, see [Customize Azure HDInsight Hadoop Clusters for Advanced Analytics](machine-learning-data-science-customize-hadoop-cluster.md).</span></span>
* <span data-ttu-id="6284d-112">Chargé les données dans les tables Hive de clusters Hadoop Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="6284d-112">The data has been uploaded to Hive tables in Azure HDInsight Hadoop clusters.</span></span> <span data-ttu-id="6284d-113">Si tel n’est pas le cas, commencez par suivre la procédure décrite sous [Créer et charger des données dans les tables Hive](machine-learning-data-science-move-hive-tables.md) .</span><span class="sxs-lookup"><span data-stu-id="6284d-113">If it has not, follow the instructions in [Create and load data to Hive tables](machine-learning-data-science-move-hive-tables.md) to upload data to Hive tables first.</span></span>
* <span data-ttu-id="6284d-114">Activé l’accès à distance au cluster.</span><span class="sxs-lookup"><span data-stu-id="6284d-114">Enabled remote access to the cluster.</span></span> <span data-ttu-id="6284d-115">Si vous avez besoin d’aide, consultez [Accéder au nœud principal du cluster Hadoop](machine-learning-data-science-customize-hadoop-cluster.md#headnode).</span><span class="sxs-lookup"><span data-stu-id="6284d-115">If you need instructions, see [Access the Head Node of Hadoop Cluster](machine-learning-data-science-customize-hadoop-cluster.md#headnode).</span></span>
* <span data-ttu-id="6284d-116">Si vous avez besoin d’aide sur l’envoi de requêtes Hive, consultez [Comment envoyer des requêtes Hive](machine-learning-data-science-move-hive-tables.md#submit)</span><span class="sxs-lookup"><span data-stu-id="6284d-116">If you need instructions on how to submit Hive queries, see [How to Submit Hive Queries](machine-learning-data-science-move-hive-tables.md#submit)</span></span>

## <a name="example-hive-query-scripts-for-data-exploration"></a><span data-ttu-id="6284d-117">Exemples de scripts de requête Hive pour l’exploration de données</span><span class="sxs-lookup"><span data-stu-id="6284d-117">Example Hive query scripts for data exploration</span></span>
1. <span data-ttu-id="6284d-118">Obtenir le nombre d’observations par partition  `SELECT <partitionfieldname>, count(*) from <databasename>.<tablename> group by <partitionfieldname>;`</span><span class="sxs-lookup"><span data-stu-id="6284d-118">Get the count of observations per partition  `SELECT <partitionfieldname>, count(*) from <databasename>.<tablename> group by <partitionfieldname>;`</span></span>
2. <span data-ttu-id="6284d-119">Obtenir le nombre d'observations par jour  `SELECT to_date(<date_columnname>), count(*) from <databasename>.<tablename> group by to_date(<date_columnname>);`</span><span class="sxs-lookup"><span data-stu-id="6284d-119">Get the count of observations per day  `SELECT to_date(<date_columnname>), count(*) from <databasename>.<tablename> group by to_date(<date_columnname>);`</span></span>
3. <span data-ttu-id="6284d-120">Obtenir les niveaux dans une colonne catégorielle </span><span class="sxs-lookup"><span data-stu-id="6284d-120">Get the levels in a categorical column</span></span>  
    `SELECT  distinct <column_name> from <databasename>.<tablename>`
4. <span data-ttu-id="6284d-121">Obtenir le nombre de niveaux en combinant deux colonnes catégorielles  `SELECT <column_a>, <column_b>, count(*) from <databasename>.<tablename> group by <column_a>, <column_b>`</span><span class="sxs-lookup"><span data-stu-id="6284d-121">Get the number of levels in combination of two categorical columns  `SELECT <column_a>, <column_b>, count(*) from <databasename>.<tablename> group by <column_a>, <column_b>`</span></span>
5. <span data-ttu-id="6284d-122">Obtenir la distribution relative aux colonnes numériques </span><span class="sxs-lookup"><span data-stu-id="6284d-122">Get the distribution for numerical columns</span></span>  
    `SELECT <column_name>, count(*) from <databasename>.<tablename> group by <column_name>`
6. <span data-ttu-id="6284d-123">Extraire les enregistrements à partir de la jointure des deux tables</span><span class="sxs-lookup"><span data-stu-id="6284d-123">Extract records from joining two tables</span></span>
   
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

## <a name="additional-query-scripts-for-taxi-trip-data-scenarios"></a><span data-ttu-id="6284d-124">Scripts de requête supplémentaires pour les scénarios de données de courses de taxi</span><span class="sxs-lookup"><span data-stu-id="6284d-124">Additional query scripts for taxi trip data scenarios</span></span>
<span data-ttu-id="6284d-125">Des exemples de requêtes propres aux scénarios mettant en œuvre le jeu de [données NYC Taxi Trip](http://chriswhong.com/open-data/foil_nyc_taxi/) sont également disponibles dans le [référentiel Github](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts).</span><span class="sxs-lookup"><span data-stu-id="6284d-125">Examples of queries that are specific to [NYC Taxi Trip Data](http://chriswhong.com/open-data/foil_nyc_taxi/) scenarios are also provided in [GitHub repository](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts).</span></span> <span data-ttu-id="6284d-126">Le schéma de données de ces requêtes est déjà spécifié et elles sont exécutables en l’état.</span><span class="sxs-lookup"><span data-stu-id="6284d-126">These queries already have data schema specified and are ready to be submitted to run.</span></span>

