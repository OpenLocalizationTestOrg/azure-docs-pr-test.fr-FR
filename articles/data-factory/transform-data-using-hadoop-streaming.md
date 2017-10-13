---
title: "Transformer des données à l’aide d’une activité de diffusion en continu Hadoop dans Azure Data Factory | Microsoft Docs"
description: "Explique comment utiliser l’activité de diffusion en continu Hadoop dans Azure Data Factory pour transformer des données en exécutant des programmes de diffusion en continu Hadoop sur un cluster Hadoop."
services: data-factory
documentationcenter: 
author: shengcmsft
manager: jhubbard
editor: spelluru
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/19/2017
ms.author: shengc
ms.openlocfilehash: 0452dcaa039c23b9e41f78a43df88f61d13033be
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/11/2017
---
# <a name="transform-data-using-hadoop-streaming-activity-in-azure-data-factory"></a>Transformer des données à l’aide d’une activité de diffusion en continu Hadoop dans Azure Data Factory
> [!div class="op_single_selector" title1="Select the version of Data Factory service you are using:"]
> * [Version 1 : disponibilité générale](v1/data-factory-hadoop-streaming-activity.md)
> * [Version 2 : préversion](transform-data-using-hadoop-streaming.md)

L’activité de diffusion en continu HDInsight dans un [pipeline](concepts-pipelines-activities.md) Data Factory exécute des programmes de diffusion en continu Hadoop sur votre cluster HDInsight [propre](compute-linked-services.md#azure-hdinsight-linked-service) ou [à la demande](compute-linked-services.md#azure-hdinsight-on-demand-linked-service). Cet article s'appuie sur l'article [Activités de transformation des données](transform-data.md) qui présente une vue d'ensemble de la transformation des données et les activités de transformation prises en charge.

> [!NOTE]
> Cet article s’applique à la version 2 de Data Factory, actuellement en préversion. Si vous utilisez la version 1 du service Data Factory, qui est en disponibilité générale, consultez [Activité de diffusion en continu Hadoop dans V1](v1/data-factory-hadoop-streaming-activity.md).

Si vous découvrez Azure Data Factory, lisez la [présentation d’Azure Data Factory](introduction.md) et suivez le [Didacticiel : Transformer des données](tutorial-transform-data-spark-powershell.md) avant de lire cet article. 

## <a name="json-sample"></a>Exemple JSON
```json
{
    "name": "Streaming Activity",
    "description": "Description",
    "type": "HDInsightStreaming",
    "linkedServiceName": {
        "referenceName": "MyHDInsightLinkedService",
        "type": "LinkedServiceReference"
    },
    "typeProperties": {
        "mapper": "MyMapper.exe",
        "reducer": "MyReducer.exe",
        "combiner": "MyCombiner.exe",
        "fileLinkedService": {
            "referenceName": "MyAzureStorageLinkedService",
            "type": "LinkedServiceReference"
        },
        "filePaths": [
            "<containername>/example/apps/MyMapper.exe",
            "<containername>/example/apps/MyReducer.exe",
            "<containername>/example/apps/MyCombiner.exe"
        ],
        "input": "wasb://<containername>@<accountname>.blob.core.windows.net/example/input/MapperInput.txt",
        "output": "wasb://<containername>@<accountname>.blob.core.windows.net/example/output/ReducerOutput.txt",
        "commandEnvironment": [
            "CmdEnvVarName=CmdEnvVarValue"
        ],
        "getDebugInfo": "Failure",
        "arguments": [
            "SampleHadoopJobArgument1"
        ],
        "defines": {
            "param1": "param1Value"
        }
    }
}
```

## <a name="syntax-details"></a>Détails de la syntaxe

| Propriété          | Description                              | Requis |
| ----------------- | ---------------------------------------- | -------- |
| name              | Nom de l’activité                     | Oui      |
| Description       | Texte décrivant la raison motivant l’activité. | Non       |
| type              | Pour l’activité de diffusion en continu Hadoop, le type d’activité est HDInsightStreaming. | Oui      |
| linkedServiceName | Référence au cluster HDInsight enregistré en tant que service lié dans Data Factory. Pour en savoir plus sur ce service lié, consultez l’article [Services liés de calcul](compute-linked-services.md). | Oui      |
| mappeur            | Spécifie le nom de l’exécutable du mappeur. | Oui      |
| raccord de réduction           | Spécifie le nom de l’exécutable du raccord de réduction. | Oui      |
| combinateur          | Spécifie le nom de l’exécutable du combinateur. | Non       |
| fileLinkedService | Référence à un service lié de stockage Azure utilisée pour stocker les programmes du mappeur, du combinateur et du raccord de réduction à exécuter. Si vous ne spécifiez pas ce service lié, le service lié Stockage Azure défini dans le service lié HDInsight est utilisé. | Non       |
| filePath          | Fournissez un tableau du chemin vers les programmes du mappeur, du combinateur et du raccord de réduction stockés dans le stockage Azure référencé par fileLinkedService. Le chemin respecte la casse. | Oui      |
| entrée             | Spécifie le chemin WASB vers le fichier d’entrée du mappeur. | Oui      |
| sortie            | Spécifie le chemin WASB vers le fichier de sortie du raccord de réduction. | Oui      |
| getDebugInfo      | Spécifie quand les fichiers journaux sont copiés vers le stockage Azure utilisé par le cluster HDInsight (ou) spécifié par scriptLinkedService. Valeurs autorisées : Aucun, Toujours ou Échec. Valeur par défaut : Aucun. | Non       |
| arguments         | Spécifie un tableau d’arguments pour un travail Hadoop. Les arguments sont passés sous la forme d’arguments de ligne de commande à chaque tâche. | Non       |
| defines           | Spécifier les paramètres sous forme de paires clé/valeur pour le référencement au sein du script Hive. | Non       | 

## <a name="next-steps"></a>Étapes suivantes
Consultez les articles suivants qui expliquent comment transformer des données par d’autres moyens : 

* [Activité U-SQL](transform-data-using-data-lake-analytics.md)
* [Activité Hive](transform-data-using-hadoop-hive.md)
* [Activité Pig](transform-data-using-hadoop-pig.md)
* [Activité MapReduce](transform-data-using-hadoop-map-reduce.md)
* [Activité Spark](transform-data-using-spark.md)
* [Activité personnalisée .NET](transform-data-using-dotnet-custom-activity.md)
* [Activité d’exécution du lot Machine Learning](transform-data-using-machine-learning.md)
* [Activité de procédure stockée](transform-data-using-stored-procedure.md)
