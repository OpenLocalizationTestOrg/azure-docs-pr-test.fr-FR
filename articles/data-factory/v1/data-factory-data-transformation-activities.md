---
title: "Transformation des données : traiter et transformer des données | Microsoft Docs"
description: "Découvrez comment transformer des données ou traiter les données dans Azure Data Factory à l’aide de Hadoop, Machine Learning ou Azure Data Lake Analytics."
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
ms.date: 01/10/2018
ms.author: shlo
robots: noindex
ms.openlocfilehash: 4dd393f1f808e5cfc804bdf90ee31f69f15eed7c
ms.sourcegitcommit: 9cc3d9b9c36e4c973dd9c9028361af1ec5d29910
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/23/2018
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

## <a name="overview"></a>Vue d’ensemble
> [!NOTE]
> Cet article s’applique à la version 1 de Data factory, qui est généralement disponible (GA). Si vous utilisez la version 2 du service Data Factory, qui est en préversion, consultez [Activités de transformation des données dans la version 2 de Data Factory](../transform-data.md).

Cet article explique les activités de transformation des données dans Azure Data Factory, que vous pouvez utiliser pour transformer et traiter vos données brutes pour en tirer des prévisions et des informations. Une activité de transformation s’exécute dans un environnement de calcul comme un cluster Azure HDInsight ou un Azure Batch. Elle fournit des liens vers des articles contenant des informations détaillées sur chaque activité de transformation.

Data Factory prend en charge les activités de transformation des données suivantes, qui peuvent être ajoutées à des [pipelines](data-factory-create-pipelines.md) , soit individuellement soit de façon chaînée avec une autre activité.

> [!NOTE]
> Pour des instructions détaillées, consultez l’article [Créer un pipeline avec la transformation Hive](data-factory-build-your-first-pipeline.md) .  
> 
> 

## <a name="hdinsight-hive-activity"></a>Activité Hive HDInsight
L’activité Hive HDInsight d’un pipeline Data Factory exécute des requêtes Hive sur votre propre cluster ou cluster à la demande HDInsight sous Windows ou Linux. Consultez l’article [Activité Hive](data-factory-hive-activity.md) pour plus de détails sur cette activité. 

## <a name="hdinsight-pig-activity"></a>Activité Pig HDInsight
L’activité Pig HDInsight d’un pipeline Data Factory exécute des requêtes Pig sur votre propre cluster ou cluster à la demande HDInsight sous Windows ou Linux. Consultez l’article [Activité Pig](data-factory-pig-activity.md) pour plus de détails sur cette activité. 

## <a name="hdinsight-mapreduce-activity"></a>Activité MapReduce HDInsight
L’activité MapReduce de HDInsight dans un pipeline Data Factory exécute des programmes MapReduce sur votre cluster HDInsight propre ou à la demande sous Windows ou Linux. Consultez l’article [Activité MapReduce](data-factory-map-reduce.md) pour plus de détails sur cette activité.

## <a name="hdinsight-streaming-activity"></a>Activité de diffusion en continu HDInsight
L’activité de diffusion en continu HDInsight dans un pipeline Data Factory exécute des programmes de diffusion en continu Hadoop sur votre cluster HDInsight propre ou à la demande sous Windows ou Linux. Consultez [l’activité de diffusion en continu HDInsight](data-factory-hadoop-streaming-activity.md) pour plus d’informations sur cette activité.

## <a name="hdinsight-spark-activity"></a>Activité Spark HDInsight
L’activité Spark HDInsight d’un pipeline Data Factory exécute des programmes Spark sur votre propre cluster HDInsight. Pour plus d’informations, consultez la page [Appeler des programmes Spark à partir de Data Factory](data-factory-spark.md). 

## <a name="machine-learning-activities"></a>Activités Machine Learning
Azure Data Factory vous permet de créer facilement des pipelines qui utilisent un service web Azure Machine Learning publié pour l’analyse prédictive. À l’aide de l’ [activité d’exécution par lots](data-factory-azure-ml-batch-execution-activity.md#invoking-a-web-service-using-batch-execution-activity) dans un pipeline Azure Data Factory, vous pouvez appeler un service web Machine Learning pour effectuer des prédictions sur les données par lots.

Au fil du temps, les modèles prédictifs dans les expériences de notation Machine Learning doivent être reformés à l’aide de nouveaux jeux de données d’entrée. Une fois que vous avez fini la reformation, vous souhaitez mettre à jour le service web de notation avec le modèle Machine Learning reformé. Vous pouvez utiliser [l’activité des ressources de mise à jour](data-factory-azure-ml-batch-execution-activity.md#updating-models-using-update-resource-activity) pour mettre à jour le service web avec le modèle qui vient d’être formé.  

Consultez la page [Utiliser les activités Machine Learning](data-factory-azure-ml-batch-execution-activity.md) pour plus d’informations sur ces activités Machine Learning. 

## <a name="stored-procedure-activity"></a>Activité de procédure stockée
Vous pouvez utiliser l’activité de procédure stockée SQL Server dans un pipeline Data Factory pour appeler une procédure stockée dans l’une des banques de données suivantes : Azure SQL Database, Azure SQL Data Warehouse, base de données SQL Server dans votre entreprise ou une machine virtuelle Azure. Consultez l’article [Activité de procédure stockée](data-factory-stored-proc-activity.md) pour plus de détails.  

## <a name="data-lake-analytics-u-sql-activity"></a>Activité U-SQL Data Lake Analytics
L’activité U-SQL Data Lake Analytics exécute un script U-SQL sur un cluster Azure Data Lake Analytics. Consultez l’article [Activité U-SQL Data Analytics](data-factory-usql-activity.md) pour plus de détails. 

## <a name="net-custom-activity"></a>Activité personnalisée .NET
Si vous devez transformer les données d’une manière qui n’est pas prise en charge par Data Factory, créez une activité personnalisée avec votre propre logique de traitement des données et utilisez cette activité dans le pipeline. Vous pouvez configurer l’activité .NET personnalisée pour l’exécuter en utilisant un service Azure Batch ou un cluster Azure HDInsight. Consultez l’article [Utilisation des activités personnalisées](data-factory-use-custom-activities.md) pour plus de détails. 

Vous pouvez créer une activité personnalisée pour exécuter des scripts R sur votre cluster HDInsight si R est installé. Consultez la page [Exécuter des scripts R avec Azure Data Factory](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample). 

## <a name="compute-environments"></a>Environnements de calcul
Vous créez un service lié à l’environnement de calcul puis l’utilisez lorsque vous définissez une activité de transformation. Il existe deux types d'environnements de calcul pris en charge par Data Factory. 

1. **À la demande** : dans ce cas, l’environnement de calcul est entièrement géré par Data Factory. Il est automatiquement créé par le service Azure Data Factory avant qu'une tâche de traitement des données ne soit soumise et il est supprimé lorsque la tâche est terminée. Vous pouvez configurer et contrôler les paramètres granulaires de l’environnement de calcul à la demande pour l'exécution de la tâche, la gestion du cluster et les actions d’amorçage. 
2. **Apport de votre propre environnement**: dans ce cas, vous pouvez inscrire votre propre environnement de calcul (par exemple un cluster HDInsight) en tant que service lié dans Data Factory. C’est vous qui gérez l'environnement de calcul et le service Data Factory l'utilise pour exécuter les activités. 

Consultez l’article [Services liés de calcul](data-factory-compute-linked-services.md) pour en savoir plus sur les services de calcul pris en charge par Data Factory. 

## <a name="summary"></a>Résumé
Azure Data Factory prend en charge les activités suivantes de transformation des données et les environnements de calcul pour les activités. Les activités de transformation peuvent être ajoutées à des pipelines, soit individuellement soit de façon chaînée avec une autre activité.

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

