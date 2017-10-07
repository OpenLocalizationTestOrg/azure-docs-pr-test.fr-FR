---
title: "les données d’aaaTransform à l’aide d’activité de diffusion en continu Hadoop - Azure | Documents Microsoft"
description: "Découvrez comment vous pouvez utiliser hello activité de Streaming Hadoop dans un Azure data factory tootransform de données en exécutant des programmes de diffusion en continu Hadoop sur un cluster de HDInsight sur la demande/votre propre."
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 4c3ff8f2-2c00-434e-a416-06dfca2c41ec
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: shlo
ms.openlocfilehash: a7ddb7268f47162709a9c8136ccd69e0b7d4ad7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="transform-data-using-hadoop-streaming-activity-in-azure-data-factory"></a>Transformer des données à l’aide d’une activité de diffusion en continu Hadoop dans Azure Data Factory
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

Vous pouvez utiliser hello HDInsightStreamingActivity activité appeler un travail Hadoop de diffusion en continu à partir d’un pipeline Azure Data Factory. Hello extrait de code JSON suivant illustre syntaxe hello pour l’utilisation de hello HDInsightStreamingActivity dans un fichier JSON de pipeline. 

Hello activité de diffusion en continu HDInsight dans une fabrique de données [pipeline](data-factory-create-pipelines.md) exécute les programmes de diffusion en continu Hadoop sur [votre propre](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) ou [à la demande](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) HDInsight de basés sur Windows/Linux cluster. Cet article s’appuie sur hello [activités de transformation des données](data-factory-data-transformation-activities.md) article, qui présente une vue d’ensemble de la transformation des données et des activités de transformation hello pris en charge.

> [!NOTE] 
> Si vous êtes tooAzure nouvelle fabrique de données, lisez [Introduction tooAzure Data Factory](data-factory-introduction.md) et hello didacticiel : [générer votre première pipeline de données](data-factory-build-your-first-pipeline.md) avant de lire cet article. 

## <a name="json-sample"></a>Exemple JSON
cluster HDInsight de Hello est automatiquement remplie avec les données (davinci.txt) et les exemples de programmes (wc.exe et cat.exe). Par défaut, le nom du conteneur de hello est utilisé par le cluster HDInsight de hello est nom hello de cluster hello lui-même. Par exemple, si votre nom de cluster est myhdicluster, nom du conteneur d’objets blob hello associé serait myhdicluster. 

```JSON
{
    "name": "HadoopStreamingPipeline",
    "properties": {
        "description": "Hadoop Streaming Demo",
        "activities": [
            {
                "type": "HDInsightStreaming",
                "typeProperties": {
                    "mapper": "cat.exe",
                    "reducer": "wc.exe",
                    "input": "wasb://<nameofthecluster>@spestore.blob.core.windows.net/example/data/gutenberg/davinci.txt",
                    "output": "wasb://<nameofthecluster>@spestore.blob.core.windows.net/example/data/StreamingOutput/wc.txt",
                    "filePaths": [
                        "<nameofthecluster>/example/apps/wc.exe",
                        "<nameofthecluster>/example/apps/cat.exe"
                    ],
                    "fileLinkedService": "AzureStorageLinkedService",
                    "getDebugInfo": "Failure"
                },
                "outputs": [
                    {
                        "name": "StreamingOutputDataset"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "name": "RunHadoopStreamingJob",
                "description": "Run a Hadoop streaming job",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2014-01-04T00:00:00Z",
        "end": "2014-01-05T00:00:00Z"
    }
}
```

Hello Notez les points suivants :

1. Ensemble hello **linkedServiceName** toohello le nom de hello lié service qui pointe le cluster HDInsight de tooyour sur le hello mapreduce de diffusion en continu le travail est exécuté.
2. Définir le type de hello d’activité hello trop**HDInsightStreaming**.
3. Pourquoi **Mappeur** propriété, spécifiez le nom hello du fichier exécutable du mappeur. Dans l’exemple de hello, cat.exe est le Mappeur hello exécutable.
4. Pourquoi **réducteur** propriété, spécifiez le nom hello du fichier exécutable du réducteur. Dans l’exemple de hello, wc.exe est hello fichier exécutable du réducteur.
5. Pourquoi **d’entrée** la propriété de type, spécifiez le fichier d’entrée de hello (y compris l’emplacement de hello) pour le Mappeur hello. Dans l’exemple de hello : « wasb://adfsample@<account name>.blob.core.windows.net/example/data/gutenberg/davinci.txt » : adfsample est le conteneur d’objets blob hello, exemple/data/Gutenberg est hello dossier, et davinci.txt est l’objet blob de hello.
6. Pourquoi **sortie** la propriété de type, spécifiez le fichier de sortie de hello (y compris l’emplacement de hello) pour le réducteur de hello. sortie de Hello du travail de diffusion en continu Hadoop hello est écrite emplacement toohello spécifiée pour cette propriété.
7. Bonjour **filePaths** section, spécifiez des chemins d’accès hello pour hello exécutables du Mappeur et du réducteur. Dans l’exemple de hello : « adfsample/example/apps/wc.exe », adfsample est le conteneur d’objets blob hello, exemple/apps est le dossier de hello et wc.exe est hello exécutable.
8. Pourquoi **fileLinkedService** propriété, spécifiez hello Azure Storage service lié qui représente hello le stockage Azure qui contient les fichiers hello spécifiés dans la section de filePaths hello.
9. Pourquoi **arguments** propriété, spécifiez les arguments de hello pour hello travail de diffusion en continu.
10. Hello **getDebugInfo** propriété est un élément facultatif. Lorsqu’il est défini tooFailure, les journaux de hello sont téléchargés uniquement en cas d’échec. Lorsqu’il est défini tooAlways, les journaux sont toujours téléchargées quel que soit l’état d’exécution hello.

> [!NOTE]
> Comme indiqué dans l’exemple de hello, vous spécifiez un dataset de sortie pour une activité de Streaming Hadoop de hello pour hello **génère** propriété. Ce jeu de données est uniquement un jeu de données factice qui est la planification de pipeline hello toodrive requis. Il est inutile toospecify tout jeu de données d’entrée pour l’activité hello pour hello **entrées** propriété.  
> 
> 

## <a name="example"></a>Exemple
pipeline Hello dans cette procédure pas à pas exécute le programme de mappage/réduction diffusion en continu hello statistiques sur votre cluster Azure HDInsight. 

### <a name="linked-services"></a>Services liés
#### <a name="azure-storage-linked-service"></a>Service lié Azure Storage
Tout d’abord, vous créez un hello toolink de service lié Azure Storage qui est utilisé par la fabrique de données Azure hello Azure HDInsight cluster toohello. Si vous copiez-collez hello suivant de code, n’oubliez pas de clé de compte et le nom de compte avec le nom de hello tooreplace et la clé de votre stockage Azure. 

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
Ensuite, créez un service lié de toolink votre fabrique de données Azure toohello cluster Azure HDInsight. Si vous copiez-collez hello suivant de code, remplacez le nom du cluster HDInsight avec nom hello de votre cluster HDInsight et modifier les valeurs nom et mot de passe utilisateur. 

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
pipeline Hello dans cet exemple ne prend pas d’entrées. Vous spécifiez un dataset de sortie pour une activité de diffusion en continu HDInsight de hello. Ce jeu de données est uniquement un jeu de données factice qui est la planification de pipeline hello toodrive requis. 

```JSON
{
    "name": "StreamingOutputDataset",
    "properties": {
        "published": false,
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "adftutorial/streamingdata/",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            },
        },
        "availability": {
            "frequency": "Day",
            "interval": 1
        }
    }
}
```

### <a name="pipeline"></a>Pipeline
pipeline Hello dans cet exemple n'a qu’une seule activité qui est de type : **HDInsightStreaming**. 

cluster HDInsight de Hello est automatiquement remplie avec les données (davinci.txt) et les exemples de programmes (wc.exe et cat.exe). Par défaut, le nom du conteneur de hello est utilisé par le cluster HDInsight de hello est nom hello de cluster hello lui-même. Par exemple, si votre nom de cluster est myhdicluster, nom du conteneur d’objets blob hello associé serait myhdicluster.  

```JSON
{
    "name": "HadoopStreamingPipeline",
    "properties": {
        "description": "Hadoop Streaming Demo",
        "activities": [
            {
                "type": "HDInsightStreaming",
                "typeProperties": {
                    "mapper": "cat.exe",
                    "reducer": "wc.exe",
                    "input": "wasb://<blobcontainer>@spestore.blob.core.windows.net/example/data/gutenberg/davinci.txt",
                    "output": "wasb://<blobcontainer>@spestore.blob.core.windows.net/example/data/StreamingOutput/wc.txt",
                    "filePaths": [
                        "<blobcontainer>/example/apps/wc.exe",
                        "<blobcontainer>/example/apps/cat.exe"
                    ],
                    "fileLinkedService": "StorageLinkedService"
                },
                "outputs": [
                    {
                        "name": "StreamingOutputDataset"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "name": "RunHadoopStreamingJob",
                "description": "Run a Hadoop streaming job",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2017-01-03T00:00:00Z",
        "end": "2017-01-04T00:00:00Z"
    }
}
```
## <a name="see-also"></a>Voir aussi
* [Activité Hive](data-factory-hive-activity.md)
* [Activité pig](data-factory-pig-activity.md)
* [Activité MapReduce](data-factory-map-reduce.md)
* [Appeler des programmes Spark](data-factory-spark.md)
* [Appeler des scripts R](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)

