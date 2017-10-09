---
title: "aaaInvoke programme MapReduce à partir d’Azure Data Factory"
description: "Découvrez comment tooprocess les données en exécutant des programmes MapReduce sur un Azure HDInsight de cluster à partir d’une fabrique de données Azure."
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: c34db93f-570a-44f1-a7d6-00390f4dc0fa
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: shlo
ms.openlocfilehash: 448ef93a10bd97e7ecd4be4f04f88f8a05decc1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="invoke-mapreduce-programs-from-data-factory"></a>Appeler des programmes MapReduce à partir de Data Factory
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [Activité Hive](data-factory-hive-activity.md) 
> * [Activité pig](data-factory-pig-activity.md)
> * [Activité MapReduce](data-factory-map-reduce.md)
> * [Activité de diffusion en continu Hadoop](data-factory-hadoop-streaming-activity.md)
> * [Activité Spark](data-factory-spark.md)
> * [Activité d’exécution par lot Machine Learning](data-factory-azure-ml-batch-execution-activity.md)
> * [Activité des ressources de mise à jour de Machine Learning](data-factory-azure-ml-update-resource-activity.md)
> * [Activité de procédure stockée](data-factory-stored-proc-activity.md)
> * [Activité U-SQL Data Lake Analytics](data-factory-usql-activity.md)
> * [Activité personnalisée .NET](data-factory-use-custom-activities.md)

Hello activité HDInsight MapReduce dans une fabrique de données [pipeline](data-factory-create-pipelines.md) exécute les programmes MapReduce sur [votre propre](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) ou [à la demande](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) cluster HDInsight de basés sur Windows/Linux. Cet article s’appuie sur hello [activités de transformation des données](data-factory-data-transformation-activities.md) article, qui présente une vue d’ensemble de la transformation des données et des activités de transformation hello pris en charge.

> [!NOTE] 
> Si vous êtes tooAzure nouvelle fabrique de données, lisez [Introduction tooAzure Data Factory](data-factory-introduction.md) et hello didacticiel : [générer votre première pipeline de données](data-factory-build-your-first-pipeline.md) avant de lire cet article.  

## <a name="introduction"></a>Introduction
Un pipeline dans une fabrique de données Azure traite les données dans les services de stockage liés à l'aide des services de calcul liés. Il contient une séquence d'activités dans laquelle chaque activité effectue une opération de traitement spécifique. Cet article décrit l’utilisation de hello HDInsight MapReduce activité.

Consultez [Pig](data-factory-pig-activity.md) et [Hive](data-factory-hive-activity.md) pour plus d’informations sur l’exécution de scripts Pig/Hive sur un cluster HDInsight sous Windows ou Linux à partir d’un pipeline à l’aide des activités Pig et Hive de HDInsight. 

## <a name="json-for-hdinsight-mapreduce-activity"></a>JSON pour l’activité MapReduce de HDInsight
Bonjour définition JSON pour hello activité HDInsight : 

1. Ensemble hello **type** Hello **activité** trop**HDInsight**.
2. Spécifiez le nom hello de classe hello pour **className** propriété.
3. Spécifier le fichier JAR hello chemin d’accès toohello sont notamment le nom de fichier hello pour **jarFilePath** propriété.
4. Spécifier le service hello lié qui fait référence toohello stockage d’objets Blob Azure qui contient le fichier JAR hello **jarLinkedService** propriété.   
5. Spécifiez les arguments de programme MapReduce de hello dans hello **arguments** section. Lors de l’exécution, vous consultez quelques arguments supplémentaires (par exemple : mapreduce.job.tags) à partir de l’infrastructure de MapReduce hello. toodifferentiate vos arguments avec des arguments de MapReduce hello, envisagez d’utiliser des option et la valeur en tant qu’arguments comme indiqué dans hello exemple suivant (- s,--entrée,--sortie, etc., sont des options de suivi immédiatement par leurs valeurs).

    ```JSON   
    {
        "name": "MahoutMapReduceSamplePipeline",
        "properties": {
            "description": "Sample Pipeline tooRun a Mahout Custom Map Reduce Jar. This job calcuates an Item Similarity Matrix toodetermine hello similarity between 2 items",
            "activities": [
                {
                    "type": "HDInsightMapReduce",
                    "typeProperties": {
                        "className": "org.apache.mahout.cf.taste.hadoop.similarity.item.ItemSimilarityJob",
                        "jarFilePath": "adfsamples/Mahout/jars/mahout-examples-0.9.0.2.2.7.1-34.jar",
                        "jarLinkedService": "StorageLinkedService",
                        "arguments": [
                            "-s",
                            "SIMILARITY_LOGLIKELIHOOD",
                            "--input",
                            "wasb://adfsamples@spestore.blob.core.windows.net/Mahout/input",
                            "--output",
                            "wasb://adfsamples@spestore.blob.core.windows.net/Mahout/output/",
                            "--maxSimilaritiesPerItem",
                            "500",
                            "--tempDir",
                            "wasb://adfsamples@spestore.blob.core.windows.net/Mahout/temp/mahout"
                        ]
                    },
                    "inputs": [
                        {
                            "name": "MahoutInput"
                        }
                    ],
                    "outputs": [
                        {
                            "name": "MahoutOutput"
                        }
                    ],
                    "policy": {
                        "timeout": "01:00:00",
                        "concurrency": 1,
                        "retry": 3
                    },
                    "scheduler": {
                        "frequency": "Hour",
                        "interval": 1
                    },
                    "name": "MahoutActivity",
                    "description": "Custom Map Reduce toogenerate Mahout result",
                    "linkedServiceName": "HDInsightLinkedService"
                }
            ],
            "start": "2017-01-03T00:00:00Z",
            "end": "2017-01-04T00:00:00Z"
        }
    }
    ```
Vous pouvez utiliser hello HDInsight MapReduce activité toorun n’importe quel fichier jar de MapReduce sur un cluster HDInsight. Bonjour exemple suivant JSON de définition d’un pipeline, hello activité HDInsight est configuré toorun un fichier Mahout JAR.

## <a name="sample-on-github"></a>Exemple sur GitHub
Vous pouvez télécharger un exemple d’utilisation de hello HDInsight MapReduce activité à partir de : [exemples de fabrique de données sur GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/JSON/MapReduce_Activity_Sample).  

## <a name="running-hello-word-count-program"></a>Programme de statistiques hello en cours d’exécution
pipeline Hello dans cet exemple s’exécute hello programme de mappage/réduction du nombre de mots sur votre cluster Azure HDInsight.   

### <a name="linked-services"></a>Services liés
Tout d’abord, vous créez un hello toolink de service lié Azure Storage qui est utilisé par la fabrique de données Azure hello Azure HDInsight cluster toohello. Si vous copiez-collez hello suivant de code, n’oubliez pas de tooreplace **nom de compte** et **clé de compte** avec le nom de hello et la clé de votre stockage Azure. 

#### <a name="azure-storage-linked-service"></a>Service lié Azure Storage

```JSON
{
    "name": "StorageLinkedService",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<account name>;AccountKey=<account key>"
        }
    }
}
```

#### <a name="azure-hdinsight-linked-service"></a>Service lié Azure HDInsight
Ensuite, créez un service lié de toolink votre fabrique de données Azure toohello cluster Azure HDInsight. Si vous copiez-collez hello suivant de code, remplacez **nom du cluster HDInsight** nom hello votre cluster HDInsight et modifier utilisateur les valeurs de nom et mot de passe.   

```JSON
{
    "name": "HDInsightLinkedService",
    "properties": {
        "type": "HDInsight",
        "typeProperties": {
            "clusterUri": "https://<HDInsight cluster name>.azurehdinsight.net",
            "userName": "admin",
            "password": "**********",
            "linkedServiceName": "StorageLinkedService"
        }
    }
}
```

### <a name="datasets"></a>JEUX DE DONNÉES
#### <a name="output-dataset"></a>Jeu de données de sortie
pipeline Hello dans cet exemple ne prend pas d’entrées. Vous spécifiez un dataset de sortie pour une activité de MapReduce HDInsight de hello. Ce jeu de données est uniquement un jeu de données factice qui est la planification de pipeline hello toodrive requis.  

```JSON
{
    "name": "MROutput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "fileName": "WordCountOutput1.txt",
            "folderPath": "example/data/",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability": {
            "frequency": "Day",
            "interval": 1
        }
    }
}
```

### <a name="pipeline"></a>Pipeline
pipeline Hello dans cet exemple n'a qu’une seule activité qui est de type : HDInsightMapReduce. Certaines des propriétés importantes de hello Bonjour JSON sont : 

| Propriété | Remarques |
|:--- |:--- |
| type |type de Hello doit être défini de trop**HDInsightMapReduce**. |
| className |Nom de la classe hello est : **wordcount** |
| jarFilePath |Chemin d’accès des fichier jar toohello contenant la classe hello. Si vous copiez-collez hello suivant de code, n’oubliez pas de nom de hello toochange du cluster de hello. |
| jarLinkedService |Service lié de stockage Azure qui contient le fichier jar hello. Ce service lié fait référence toohello stockage associé au cluster HDInsight de hello. |
| arguments |programme de wordcount Hello prend deux arguments, une entrée et une sortie. Hello d’entrée est hello davinci.txt fichier. |
| frequency/interval |les valeurs Hello pour ces propriétés correspond à dataset de sortie hello. |
| linkedServiceName |désigne le service lié HDInsight de toohello créé précédemment. |

```JSON
{
    "name": "MRSamplePipeline",
    "properties": {
        "description": "Sample Pipeline tooRun hello Word Count Program",
        "activities": [
            {
                "type": "HDInsightMapReduce",
                "typeProperties": {
                    "className": "wordcount",
                    "jarFilePath": "<HDInsight cluster name>/example/jars/hadoop-examples.jar",
                    "jarLinkedService": "StorageLinkedService",
                    "arguments": [
                        "/example/data/gutenberg/davinci.txt",
                        "/example/data/WordCountOutput1"
                    ]
                },
                "outputs": [
                    {
                        "name": "MROutput"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "retry": 3
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "name": "MRActivity",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2014-01-03T00:00:00Z",
        "end": "2014-01-04T00:00:00Z"
    }
}
```

## <a name="run-spark-programs"></a>Exécuter des programmes Spark
Vous pouvez utiliser les programmes MapReduce activité toorun Spark sur votre cluster HDInsight Spark. Consultez la page [Appeler des programmes Spark à partir d'Azure Data Factory](data-factory-spark.md) pour plus d'informations.  

[developer-reference]: http://go.microsoft.com/fwlink/?LinkId=516908
[cmdlet-reference]: http://go.microsoft.com/fwlink/?LinkId=517456


[adfgetstarted]: data-factory-copy-data-from-azure-blob-storage-to-sql-database.md
[adfgetstartedmonitoring]:data-factory-copy-data-from-azure-blob-storage-to-sql-database.md#monitor-pipelines 

[Developer Reference]: http://go.microsoft.com/fwlink/?LinkId=516908
[Azure Portal]: http://portal.azure.com

## <a name="see-also"></a>Voir aussi
* [Activité Hive](data-factory-hive-activity.md)
* [Activité pig](data-factory-pig-activity.md)
* [Activité de diffusion en continu Hadoop](data-factory-hadoop-streaming-activity.md)
* [Appeler des programmes Spark](data-factory-spark.md)
* [Appeler des scripts R](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)

