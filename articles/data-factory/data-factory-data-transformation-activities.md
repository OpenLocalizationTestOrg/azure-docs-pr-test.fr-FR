---
title: "Transformation des données : traiter et transformer des données | Microsoft Docs"
description: "Découvrez comment tootransform données ou traiter des données dans Azure Data Factory à l’aide de Hadoop ou Analytique de LAC de données Azure Machine Learning."
keywords: "transformation des données, traiter les données, transformer les données, activité de transformation"
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 39786731-1e4b-40a4-81b7-d06e127427aa
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: shlo
ms.openlocfilehash: 917d617259699b0e71de3a0e0c17463d00f2e0a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="transform-data-in-azure-data-factory"></a>Transformer des données dans Azure Data Factory
> [!div class="op_single_selector"]
> * [Hive](data-factory-hive-activity.md)  
> * [Pig](data-factory-pig-activity.md)  
> * [MapReduce](data-factory-map-reduce.md)  
> * [Diffusion en continu Hadoop](data-factory-hadoop-streaming-activity.md)
> * [Machine Learning](data-factory-azure-ml-batch-execution-activity.md) 
> * [Procédure stockée](data-factory-stored-proc-activity.md)
> * [Langage U-SQL du service Analytique Data Lake](data-factory-usql-activity.md)
> * [.NET personnalisé](data-factory-use-custom-activities.md)

## <a name="overview"></a>Vue d'ensemble
Cet article explique les activités de transformation des données dans Azure Data Factory que vous pouvez utiliser tootransform et traite les données brutes dans des prédictions et des informations. Une activité de transformation s’exécute dans un environnement de calcul comme un cluster Azure HDInsight ou un Azure Batch. Il fournit des liens tooarticles avec des informations détaillées sur chaque activité de transformation.

Fabrique de données prend en charge hello suivant des activités de transformation des données qui peuvent être ajoutées trop[pipelines](data-factory-create-pipelines.md) soit individuellement ou chaînés avec une autre activité.

> [!NOTE]
> Pour des instructions détaillées, consultez l’article [Créer un pipeline avec la transformation Hive](data-factory-build-your-first-pipeline.md) .  
> 
> 

## <a name="hdinsight-hive-activity"></a>Activité Hive HDInsight
Hello activité HDInsight Hive dans un pipeline de fabrique de données exécute des requêtes Hive vous-même ou un cluster de basés sur Windows/Linux de HDInsight à la demande. Consultez l’article [Activité Hive](data-factory-hive-activity.md) pour plus de détails sur cette activité. 

## <a name="hdinsight-pig-activity"></a>Activité Pig HDInsight
Hello activité HDInsight Pig dans un pipeline de fabrique de données exécute des requêtes Pig vous-même ou un cluster de basés sur Windows/Linux de HDInsight à la demande. Consultez l’article [Activité Pig](data-factory-pig-activity.md) pour plus de détails sur cette activité. 

## <a name="hdinsight-mapreduce-activity"></a>Activité MapReduce HDInsight
Hello activité HDInsight MapReduce dans un pipeline Azure Data Factory exécute les programmes MapReduce vous-même ou un cluster de basés sur Windows/Linux de HDInsight à la demande. Consultez l’article [Activité MapReduce](data-factory-map-reduce.md) pour plus de détails sur cette activité.

## <a name="hdinsight-streaming-activity"></a>Activité de diffusion en continu HDInsight
Hello activité de diffusion en continu HDInsight dans un pipeline Azure Data Factory exécute les programmes de diffusion en continu Hadoop sur votre propre ou un cluster de Windows/Linux-based de HDInsight à la demande. Consultez [l’activité de diffusion en continu HDInsight](data-factory-hadoop-streaming-activity.md) pour plus d’informations sur cette activité.

## <a name="hdinsight-spark-activity"></a>Activité Spark HDInsight
Hello activité HDInsight Spark dans un pipeline Azure Data Factory exécute les programmes Spark sur votre propre cluster HDInsight. Pour plus d’informations, consultez la page [Appeler des programmes Spark à partir de Data Factory](data-factory-spark.md). 

## <a name="machine-learning-activities"></a>Activités Machine Learning
Azure Data Factory permet tooeasily vous créer des pipelines qui utilisent un publiée Azure Machine Learning web de service pour l’analytique prédictive. À l’aide de hello [l’activité d’exécution par lots](data-factory-azure-ml-batch-execution-activity.md#invoking-a-web-service-using-batch-execution-activity) dans un pipeline Azure Data Factory, vous pouvez appeler une prédictions de toomake du service web Machine Learning sur des données hello dans le lot.

Au fil du temps, d’entrée de modèles prédictifs de hello Bonjour apprentissage expériences score doivent toobe reformé à l’aide de nouveaux jeux de données. Une fois que vous avez terminé avec le réapprentissage, vous souhaitez hello tooupdate calcul du score du service web avec hello reformés modèle d’apprentissage. Vous pouvez utiliser hello [mise à jour de ressource activité](data-factory-azure-ml-batch-execution-activity.md#updating-models-using-update-resource-activity) service web qui vient d’être formé hello tooupdate hello.  

Consultez la page [Utiliser les activités Machine Learning](data-factory-azure-ml-batch-execution-activity.md) pour plus d’informations sur ces activités Machine Learning. 

## <a name="stored-procedure-activity"></a>Activité de procédure stockée
Vous pouvez utiliser l’activité de procédure stockée SQL Server hello dans un tooinvoke de pipeline de fabrique de données dans une procédure stockée dans un des hello suivant des magasins de données : Azure SQL Database, Azure SQL Data Warehouse, base de données SQL Server dans votre entreprise ou d’une machine virtuelle Azure. Consultez l’article [Activité de procédure stockée](data-factory-stored-proc-activity.md) pour plus de détails.  

## <a name="data-lake-analytics-u-sql-activity"></a>Activité U-SQL Data Lake Analytics
L’activité U-SQL Data Lake Analytics exécute un script U-SQL sur un cluster Azure Data Lake Analytics. Consultez l’article [Activité U-SQL Data Analytics](data-factory-usql-activity.md) pour plus de détails. 

## <a name="net-custom-activity"></a>Activité personnalisée .NET
Si vous avez besoin de données tootransform d’une manière qui n’est pas pris en charge par la fabrique de données, vous pouvez créer une activité personnalisée avec votre propre logique de traitement des données et utiliser l’activité hello dans le pipeline de hello. Vous pouvez configurer hello personnalisées .NET activité toorun à l’aide d’un service de traitement par lots Azure ou un cluster Azure HDInsight. Consultez l’article [Utilisation des activités personnalisées](data-factory-use-custom-activities.md) pour plus de détails. 

Vous pouvez créer une activité personnalisée toorun R scripts sur votre cluster HDInsight avec R installé. Consultez la page [Exécuter des scripts R avec Azure Data Factory](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample). 

## <a name="compute-environments"></a>Environnements de calcul
Vous créez un service lié pour un environnement de calcul hello et ensuite utilisez hello lié service lors de la définition d’une activité de transformation. Il existe deux types d'environnements de calcul pris en charge par Data Factory. 

1. **À la demande**: dans ce cas, environnement hello est entièrement gérée par la fabrique de données. Il est automatiquement créé par hello service Data Factory avant un travail est soumis tooprocess données et supprimé lorsque hello tâche est terminée. Vous pouvez configurer et contrôler les paramètres granulaires de l’environnement de calcul de la demande de hello pour l’exécution du travail, gestion du cluster et actions d’amorçage. 
2. **Apport de votre propre environnement**: dans ce cas, vous pouvez inscrire votre propre environnement de calcul (par exemple un cluster HDInsight) en tant que service lié dans Data Factory. environnement Hello est gérée par vous et hello service Data Factory utilise les activités tooexecute hello. 

Consultez [de calcul des Services liés](data-factory-compute-linked-services.md) toolearn l’article sur les services pris en charge par la fabrique de données de calcul. 

## <a name="summary"></a>Résumé
Azure prend en charge de Data Factory hello suivant des activités de transformation des données et hello des environnements de calcul pour les activités de hello. activitésent de transformation Hello peut être ajouté toopipelines soit individuellement ou chaîné avec une autre activité.

| Activités de transformation des données | Environnement de calcul |
|:--- |:--- |
| [Hive](data-factory-hive-activity.md) |HDInsight [Hadoop] |
| [Pig](data-factory-pig-activity.md) |HDInsight [Hadoop] |
| [MapReduce](data-factory-map-reduce.md) |HDInsight [Hadoop] |
| [Diffusion en continu Hadoop](data-factory-hadoop-streaming-activity.md) |HDInsight [Hadoop] |
| [Activités Machine Learning : exécution de lot et mise à jour de ressource](data-factory-azure-ml-batch-execution-activity.md) |Microsoft Azure |
| [Procédure stockée](data-factory-stored-proc-activity.md) |SQL Azure, Azure SQL Data Warehouse ou SQL Server |
| [Langage U-SQL du service Analytique Data Lake](data-factory-usql-activity.md) |Service Analytique Azure Data Lake |
| [DotNet](data-factory-use-custom-activities.md) |HDInsight [Hadoop] ou Azure Batch |

