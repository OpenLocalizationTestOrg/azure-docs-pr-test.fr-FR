---
title: "aaaIntegrating Data Lake Store avec d’autres Services Azure | Documents Microsoft"
description: "Présentation de l'intégration de Data Lake Store à d'autres services Azure"
documentationcenter: 
services: data-lake-store
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 48a5d1f4-3850-4c22-bbc4-6d1d394fba8a
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 839689f04623f8225884e7aa9c0b533a09323e80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="integrating-data-lake-store-with-other-azure-services"></a>Intégration de Data Lake Store à d'autres services Azure
Azure Data Lake Store peut être utilisé conjointement avec d’autres services Azure de tooenable un éventail plus large de scénarios. Hello ci-dessous répertorie les services hello Data Lake Store peut être intégré à.

## <a name="use-data-lake-store-with-azure-hdinsight"></a>Utiliser Data Lake Store avec Azure HDInsight
Vous pouvez configurer un [Azure HDInsight](https://azure.microsoft.com/documentation/learning-paths/hdinsight-self-guided-hadoop-training/) cluster qui utilise Data Lake Store en tant que stockage de hello HDFS conforme. Pour cette version, pour les clusters Hadoop et Storm sous Windows et Linux, vous ne pouvez utiliser Data Lake Store que comme stockage supplémentaire. Ces clusters toujours utiliseront le stockage Azure (WASB) comme stockage par défaut de hello. Toutefois, pour les clusters HBase sur Windows et Linux, vous pouvez utiliser Data Lake Store comme stockage par défaut de hello, ou le stockage supplémentaire ou les deux.

Pour savoir comment tooprovision un HDInsight de cluster avec Data Lake Store, consultez :

* [Approvisionner un cluster HDInsight avec Data Lake Store à l’aide du portail Azure](data-lake-store-hdinsight-hadoop-use-portal.md)
* [Approvisionner un cluster HDInsight avec Data Lake Store comme stockage par défaut à l’aide d’Azure PowerShell](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
* [Approvisionner un cluster HDInsight avec Data Lake Store comme stockage supplémentaire à l’aide d’Azure PowerShell](data-lake-store-hdinsight-hadoop-use-powershell.md)

## <a name="use-data-lake-store-with-azure-data-lake-analytics"></a>Utiliser Data Lake Store avec Azure Data Lake Analytics
[Analytique de LAC de données Azure](../data-lake-analytics/data-lake-analytics-overview.md) vous permet de toowork des données volumineuses à l’échelle du cloud. Il approvisionne dynamiquement des ressources et vous permet d'effectuer des analyses sur des téraoctets, voire des exaoctets, de données stockées dans plusieurs sources de données prises en charge, parmi lesquelles Data Lake Store. Analytique de LAC de données est toowork spécialement optimisé avec Azure Data Lake Store - fournissant des charges de travail de données volumineuses hello plus haut niveau de performances, le débit et la parallélisation pour vous.

Pour obtenir des instructions sur la façon de toouse Analytique lac de données avec Data Lake Store, consultez [prise en main Analytique lac de données à l’aide de Data Lake Store](../data-lake-analytics/data-lake-analytics-get-started-portal.md).

## <a name="use-data-lake-store-with-azure-data-factory"></a>Utiliser Data Lake Store avec Azure Data Factory
Vous pouvez utiliser [Azure Data Factory](https://azure.microsoft.com/services/data-factory/) tooingest des données à partir de tables Azure, base de données SQL Azure, entrepôt de données SQL Azure, objets BLOB de stockage Azure et bases de données locales. Être un citoyen de première classe Bonjour écosystème Azure, Azure Data Factory peut être utilisé tooorchestrate hello vitesses d’ingestion de données à partir de ces tooAzure source Data Lake Store.

Pour obtenir des instructions sur toouse Azure Data Factory avec Data Lake Store, voir [déplacer tooand de données à partir de Data Lake Store à l’aide de la fabrique de données](../data-factory/data-factory-azure-datalake-connector.md).

## <a name="copy-data-from-azure-storage-blobs-into-data-lake-store"></a>Copier des données d’objets blob Azure Storage dans Data Lake Store
Azure Data Lake Store fournit un outil de ligne de commande, AdlCopy, ce qui vous permet de toocopy des données à partir du stockage d’objets Blob Azure dans un compte Data Lake Store. Pour plus d’informations, consultez [copier les données d’objets BLOB de stockage Azure tooData Lake Store](data-lake-store-copy-data-azure-storage-blob.md).

## <a name="copy-data-between-azure-sql-database-and-data-lake-store"></a>Copier des données entre Azure SQL Database et Data Lake Store
Vous pouvez utiliser Apache Sqoop tooimport et exporter des données entre la base de données SQL Azure et Data Lake Store. Pour plus d’informations, consultez [Copier des données entre Data Lake Store et une base de données SQL Azure à l’aide de Sqoop](data-lake-store-data-transfer-sql-sqoop.md).

## <a name="use-data-lake-store-with-stream-analytics"></a>Utiliser Data Lake Store avec Stream Analytics
Vous pouvez utiliser Data Lake Store comme un des hello génère des données toostore en continu à l’aide d’Analytique de flux de données Azure. Pour plus d’informations, consultez [Diffuser des données à partir d’un objet blob Azure Storage dans Data Lake Store à l’aide d’Azure Stream Analytics](data-lake-store-stream-analytics.md).

## <a name="use-data-lake-store-with-power-bi"></a>Utiliser Data Lake Store avec Power BI
Vous pouvez utiliser des données de tooimport Power BI à partir d’un tooanalyze du compte Data Lake Store et visualiser les données de hello. Pour plus d’informations, consultez [Analyse des données dans Data Lake Store à l’aide de Power BI](data-lake-store-power-bi.md).

## <a name="use-data-lake-store-with-data-catalog"></a>Utiliser Data Lake Store avec Data Catalog
Vous pouvez enregistrer des données à partir de Data Lake Store hello Azure Data Catalog toomake les données de salutation détectables dans toute organisation de hello. Pour plus d’informations, consultez [Register data from Data Lake Store in Azure Data Catalog](data-lake-store-with-data-catalog.md)(Inscrire des données issues de Data Lake Store dans Azure Data Catalog).

## <a name="use-data-lake-store-with-sql-server-integration-services-ssis"></a>Utiliser Data Lake Store avec SQL Server Integration Services (SSIS)
Vous pouvez utiliser le Gestionnaire de connexions Azure Data Lake Store hello dans SSIS tooconnect un package SSIS avec Azure Data Lake Store. Pour obtenir plus d’informations, consultez [Utiliser Data Lake Store avec SSIS](https://docs.microsoft.com/sql/integration-services/connection-manager/azure-data-lake-store-connection-manager).

## <a name="use-data-lake-store-with-sql-data-warehouse"></a>Utiliser Data Lake Store avec SQL Data Warehouse
Vous pouvez utiliser les données de tooload de PolyBase à partir d’Azure Data Lake Store dans l’entrepôt de données SQL. Pour obtenir plus d’informations, consultez [Utiliser Data Lake Store avec SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-load-from-azure-data-lake-store.md).

## <a name="see-also"></a>Voir aussi
* [Présentation d'Azure Data Lake Store](data-lake-store-overview.md)
* [Prise en main de Data Lake Store avec le portail](data-lake-store-get-started-portal.md)
* [Prise en main de Data Lake Store avec PowerShell](data-lake-store-get-started-powershell.md)  

