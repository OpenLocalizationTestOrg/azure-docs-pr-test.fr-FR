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
# <a name="invoke-mapreduce-programs-from-data-factory"></a><span data-ttu-id="5ff51-103">Appeler des programmes MapReduce à partir de Data Factory</span><span class="sxs-lookup"><span data-stu-id="5ff51-103">Invoke MapReduce Programs from Data Factory</span></span>
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="5ff51-104">Activité Hive</span><span class="sxs-lookup"><span data-stu-id="5ff51-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="5ff51-105">Activité pig</span><span class="sxs-lookup"><span data-stu-id="5ff51-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="5ff51-106">Activité MapReduce</span><span class="sxs-lookup"><span data-stu-id="5ff51-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="5ff51-107">Activité de diffusion en continu Hadoop</span><span class="sxs-lookup"><span data-stu-id="5ff51-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="5ff51-108">Activité Spark</span><span class="sxs-lookup"><span data-stu-id="5ff51-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="5ff51-109">Activité d’exécution par lot Machine Learning</span><span class="sxs-lookup"><span data-stu-id="5ff51-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="5ff51-110">Activité des ressources de mise à jour de Machine Learning</span><span class="sxs-lookup"><span data-stu-id="5ff51-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="5ff51-111">Activité de procédure stockée</span><span class="sxs-lookup"><span data-stu-id="5ff51-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="5ff51-112">Activité U-SQL Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="5ff51-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="5ff51-113">Activité personnalisée .NET</span><span class="sxs-lookup"><span data-stu-id="5ff51-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

<span data-ttu-id="5ff51-114">Hello activité HDInsight MapReduce dans une fabrique de données [pipeline](data-factory-create-pipelines.md) exécute les programmes MapReduce sur [votre propre](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) ou [à la demande](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) cluster HDInsight de basés sur Windows/Linux.</span><span class="sxs-lookup"><span data-stu-id="5ff51-114">hello HDInsight MapReduce activity in a Data Factory [pipeline](data-factory-create-pipelines.md) executes MapReduce programs on [your own](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) or [on-demand](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) Windows/Linux-based HDInsight cluster.</span></span> <span data-ttu-id="5ff51-115">Cet article s’appuie sur hello [activités de transformation des données](data-factory-data-transformation-activities.md) article, qui présente une vue d’ensemble de la transformation des données et des activités de transformation hello pris en charge.</span><span class="sxs-lookup"><span data-stu-id="5ff51-115">This article builds on hello [data transformation activities](data-factory-data-transformation-activities.md) article, which presents a general overview of data transformation and hello supported transformation activities.</span></span>

> [!NOTE] 
> <span data-ttu-id="5ff51-116">Si vous êtes tooAzure nouvelle fabrique de données, lisez [Introduction tooAzure Data Factory](data-factory-introduction.md) et hello didacticiel : [générer votre première pipeline de données](data-factory-build-your-first-pipeline.md) avant de lire cet article.</span><span class="sxs-lookup"><span data-stu-id="5ff51-116">If you are new tooAzure Data Factory, read through [Introduction tooAzure Data Factory](data-factory-introduction.md) and do hello tutorial: [Build your first data pipeline](data-factory-build-your-first-pipeline.md) before reading this article.</span></span>  

## <a name="introduction"></a><span data-ttu-id="5ff51-117">Introduction</span><span class="sxs-lookup"><span data-stu-id="5ff51-117">Introduction</span></span>
<span data-ttu-id="5ff51-118">Un pipeline dans une fabrique de données Azure traite les données dans les services de stockage liés à l'aide des services de calcul liés.</span><span class="sxs-lookup"><span data-stu-id="5ff51-118">A pipeline in an Azure data factory processes data in linked storage services by using linked compute services.</span></span> <span data-ttu-id="5ff51-119">Il contient une séquence d'activités dans laquelle chaque activité effectue une opération de traitement spécifique.</span><span class="sxs-lookup"><span data-stu-id="5ff51-119">It contains a sequence of activities where each activity performs a specific processing operation.</span></span> <span data-ttu-id="5ff51-120">Cet article décrit l’utilisation de hello HDInsight MapReduce activité.</span><span class="sxs-lookup"><span data-stu-id="5ff51-120">This article describes using hello HDInsight MapReduce Activity.</span></span>

<span data-ttu-id="5ff51-121">Consultez [Pig](data-factory-pig-activity.md) et [Hive](data-factory-hive-activity.md) pour plus d’informations sur l’exécution de scripts Pig/Hive sur un cluster HDInsight sous Windows ou Linux à partir d’un pipeline à l’aide des activités Pig et Hive de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5ff51-121">See [Pig](data-factory-pig-activity.md) and [Hive](data-factory-hive-activity.md) for details about running Pig/Hive scripts on a Windows/Linux-based HDInsight cluster from a pipeline by using HDInsight Pig and Hive activities.</span></span> 

## <a name="json-for-hdinsight-mapreduce-activity"></a><span data-ttu-id="5ff51-122">JSON pour l’activité MapReduce de HDInsight</span><span class="sxs-lookup"><span data-stu-id="5ff51-122">JSON for HDInsight MapReduce Activity</span></span>
<span data-ttu-id="5ff51-123">Bonjour définition JSON pour hello activité HDInsight :</span><span class="sxs-lookup"><span data-stu-id="5ff51-123">In hello JSON definition for hello HDInsight Activity:</span></span> 

1. <span data-ttu-id="5ff51-124">Ensemble hello **type** Hello **activité** trop**HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="5ff51-124">Set hello **type** of hello **activity** too**HDInsight**.</span></span>
2. <span data-ttu-id="5ff51-125">Spécifiez le nom hello de classe hello pour **className** propriété.</span><span class="sxs-lookup"><span data-stu-id="5ff51-125">Specify hello name of hello class for **className** property.</span></span>
3. <span data-ttu-id="5ff51-126">Spécifier le fichier JAR hello chemin d’accès toohello sont notamment le nom de fichier hello pour **jarFilePath** propriété.</span><span class="sxs-lookup"><span data-stu-id="5ff51-126">Specify hello path toohello JAR file including hello file name for **jarFilePath** property.</span></span>
4. <span data-ttu-id="5ff51-127">Spécifier le service hello lié qui fait référence toohello stockage d’objets Blob Azure qui contient le fichier JAR hello **jarLinkedService** propriété.</span><span class="sxs-lookup"><span data-stu-id="5ff51-127">Specify hello linked service that refers toohello Azure Blob Storage that contains hello JAR file for **jarLinkedService** property.</span></span>   
5. <span data-ttu-id="5ff51-128">Spécifiez les arguments de programme MapReduce de hello dans hello **arguments** section.</span><span class="sxs-lookup"><span data-stu-id="5ff51-128">Specify any arguments for hello MapReduce program in hello **arguments** section.</span></span> <span data-ttu-id="5ff51-129">Lors de l’exécution, vous consultez quelques arguments supplémentaires (par exemple : mapreduce.job.tags) à partir de l’infrastructure de MapReduce hello.</span><span class="sxs-lookup"><span data-stu-id="5ff51-129">At runtime, you see a few extra arguments (for example: mapreduce.job.tags) from hello MapReduce framework.</span></span> <span data-ttu-id="5ff51-130">toodifferentiate vos arguments avec des arguments de MapReduce hello, envisagez d’utiliser des option et la valeur en tant qu’arguments comme indiqué dans hello exemple suivant (- s,--entrée,--sortie, etc., sont des options de suivi immédiatement par leurs valeurs).</span><span class="sxs-lookup"><span data-stu-id="5ff51-130">toodifferentiate your arguments with hello MapReduce arguments, consider using both option and value as arguments as shown in hello following example (-s, --input, --output etc., are options immediately followed by their values).</span></span>

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
<span data-ttu-id="5ff51-131">Vous pouvez utiliser hello HDInsight MapReduce activité toorun n’importe quel fichier jar de MapReduce sur un cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5ff51-131">You can use hello HDInsight MapReduce Activity toorun any MapReduce jar file on an HDInsight cluster.</span></span> <span data-ttu-id="5ff51-132">Bonjour exemple suivant JSON de définition d’un pipeline, hello activité HDInsight est configuré toorun un fichier Mahout JAR.</span><span class="sxs-lookup"><span data-stu-id="5ff51-132">In hello following sample JSON definition of a pipeline, hello HDInsight Activity is configured toorun a Mahout JAR file.</span></span>

## <a name="sample-on-github"></a><span data-ttu-id="5ff51-133">Exemple sur GitHub</span><span class="sxs-lookup"><span data-stu-id="5ff51-133">Sample on GitHub</span></span>
<span data-ttu-id="5ff51-134">Vous pouvez télécharger un exemple d’utilisation de hello HDInsight MapReduce activité à partir de : [exemples de fabrique de données sur GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/JSON/MapReduce_Activity_Sample).</span><span class="sxs-lookup"><span data-stu-id="5ff51-134">You can download a sample for using hello HDInsight MapReduce Activity from: [Data Factory Samples on GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/JSON/MapReduce_Activity_Sample).</span></span>  

## <a name="running-hello-word-count-program"></a><span data-ttu-id="5ff51-135">Programme de statistiques hello en cours d’exécution</span><span class="sxs-lookup"><span data-stu-id="5ff51-135">Running hello Word Count program</span></span>
<span data-ttu-id="5ff51-136">pipeline Hello dans cet exemple s’exécute hello programme de mappage/réduction du nombre de mots sur votre cluster Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5ff51-136">hello pipeline in this example runs hello Word Count Map/Reduce program on your Azure HDInsight cluster.</span></span>   

### <a name="linked-services"></a><span data-ttu-id="5ff51-137">Services liés</span><span class="sxs-lookup"><span data-stu-id="5ff51-137">Linked Services</span></span>
<span data-ttu-id="5ff51-138">Tout d’abord, vous créez un hello toolink de service lié Azure Storage qui est utilisé par la fabrique de données Azure hello Azure HDInsight cluster toohello.</span><span class="sxs-lookup"><span data-stu-id="5ff51-138">First, you create a linked service toolink hello Azure Storage that is used by hello Azure HDInsight cluster toohello Azure data factory.</span></span> <span data-ttu-id="5ff51-139">Si vous copiez-collez hello suivant de code, n’oubliez pas de tooreplace **nom de compte** et **clé de compte** avec le nom de hello et la clé de votre stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="5ff51-139">If you copy/paste hello following code, do not forget tooreplace **account name** and **account key** with hello name and key of your Azure Storage.</span></span> 

#### <a name="azure-storage-linked-service"></a><span data-ttu-id="5ff51-140">Service lié Azure Storage</span><span class="sxs-lookup"><span data-stu-id="5ff51-140">Azure Storage linked service</span></span>

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

#### <a name="azure-hdinsight-linked-service"></a><span data-ttu-id="5ff51-141">Service lié Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="5ff51-141">Azure HDInsight linked service</span></span>
<span data-ttu-id="5ff51-142">Ensuite, créez un service lié de toolink votre fabrique de données Azure toohello cluster Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5ff51-142">Next, you create a linked service toolink your Azure HDInsight cluster toohello Azure data factory.</span></span> <span data-ttu-id="5ff51-143">Si vous copiez-collez hello suivant de code, remplacez **nom du cluster HDInsight** nom hello votre cluster HDInsight et modifier utilisateur les valeurs de nom et mot de passe.</span><span class="sxs-lookup"><span data-stu-id="5ff51-143">If you copy/paste hello following code, replace **HDInsight cluster name** with hello name of your HDInsight cluster, and change user name and password values.</span></span>   

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

### <a name="datasets"></a><span data-ttu-id="5ff51-144">JEUX DE DONNÉES</span><span class="sxs-lookup"><span data-stu-id="5ff51-144">Datasets</span></span>
#### <a name="output-dataset"></a><span data-ttu-id="5ff51-145">Jeu de données de sortie</span><span class="sxs-lookup"><span data-stu-id="5ff51-145">Output dataset</span></span>
<span data-ttu-id="5ff51-146">pipeline Hello dans cet exemple ne prend pas d’entrées.</span><span class="sxs-lookup"><span data-stu-id="5ff51-146">hello pipeline in this example does not take any inputs.</span></span> <span data-ttu-id="5ff51-147">Vous spécifiez un dataset de sortie pour une activité de MapReduce HDInsight de hello.</span><span class="sxs-lookup"><span data-stu-id="5ff51-147">You specify an output dataset for hello HDInsight MapReduce Activity.</span></span> <span data-ttu-id="5ff51-148">Ce jeu de données est uniquement un jeu de données factice qui est la planification de pipeline hello toodrive requis.</span><span class="sxs-lookup"><span data-stu-id="5ff51-148">This dataset is just a dummy dataset that is required toodrive hello pipeline schedule.</span></span>  

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

### <a name="pipeline"></a><span data-ttu-id="5ff51-149">Pipeline</span><span class="sxs-lookup"><span data-stu-id="5ff51-149">Pipeline</span></span>
<span data-ttu-id="5ff51-150">pipeline Hello dans cet exemple n'a qu’une seule activité qui est de type : HDInsightMapReduce.</span><span class="sxs-lookup"><span data-stu-id="5ff51-150">hello pipeline in this example has only one activity that is of type: HDInsightMapReduce.</span></span> <span data-ttu-id="5ff51-151">Certaines des propriétés importantes de hello Bonjour JSON sont :</span><span class="sxs-lookup"><span data-stu-id="5ff51-151">Some of hello important properties in hello JSON are:</span></span> 

| <span data-ttu-id="5ff51-152">Propriété</span><span class="sxs-lookup"><span data-stu-id="5ff51-152">Property</span></span> | <span data-ttu-id="5ff51-153">Remarques</span><span class="sxs-lookup"><span data-stu-id="5ff51-153">Notes</span></span> |
|:--- |:--- |
| <span data-ttu-id="5ff51-154">type</span><span class="sxs-lookup"><span data-stu-id="5ff51-154">type</span></span> |<span data-ttu-id="5ff51-155">type de Hello doit être défini de trop**HDInsightMapReduce**.</span><span class="sxs-lookup"><span data-stu-id="5ff51-155">hello type must be set too**HDInsightMapReduce**.</span></span> |
| <span data-ttu-id="5ff51-156">className</span><span class="sxs-lookup"><span data-stu-id="5ff51-156">className</span></span> |<span data-ttu-id="5ff51-157">Nom de la classe hello est : **wordcount**</span><span class="sxs-lookup"><span data-stu-id="5ff51-157">Name of hello class is: **wordcount**</span></span> |
| <span data-ttu-id="5ff51-158">jarFilePath</span><span class="sxs-lookup"><span data-stu-id="5ff51-158">jarFilePath</span></span> |<span data-ttu-id="5ff51-159">Chemin d’accès des fichier jar toohello contenant la classe hello.</span><span class="sxs-lookup"><span data-stu-id="5ff51-159">Path toohello jar file containing hello class.</span></span> <span data-ttu-id="5ff51-160">Si vous copiez-collez hello suivant de code, n’oubliez pas de nom de hello toochange du cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="5ff51-160">If you copy/paste hello following code, don't forget toochange hello name of hello cluster.</span></span> |
| <span data-ttu-id="5ff51-161">jarLinkedService</span><span class="sxs-lookup"><span data-stu-id="5ff51-161">jarLinkedService</span></span> |<span data-ttu-id="5ff51-162">Service lié de stockage Azure qui contient le fichier jar hello.</span><span class="sxs-lookup"><span data-stu-id="5ff51-162">Azure Storage linked service that contains hello jar file.</span></span> <span data-ttu-id="5ff51-163">Ce service lié fait référence toohello stockage associé au cluster HDInsight de hello.</span><span class="sxs-lookup"><span data-stu-id="5ff51-163">This linked service refers toohello storage that is associated with hello HDInsight cluster.</span></span> |
| <span data-ttu-id="5ff51-164">arguments</span><span class="sxs-lookup"><span data-stu-id="5ff51-164">arguments</span></span> |<span data-ttu-id="5ff51-165">programme de wordcount Hello prend deux arguments, une entrée et une sortie.</span><span class="sxs-lookup"><span data-stu-id="5ff51-165">hello wordcount program takes two arguments, an input and an output.</span></span> <span data-ttu-id="5ff51-166">Hello d’entrée est hello davinci.txt fichier.</span><span class="sxs-lookup"><span data-stu-id="5ff51-166">hello input file is hello davinci.txt file.</span></span> |
| <span data-ttu-id="5ff51-167">frequency/interval</span><span class="sxs-lookup"><span data-stu-id="5ff51-167">frequency/interval</span></span> |<span data-ttu-id="5ff51-168">les valeurs Hello pour ces propriétés correspond à dataset de sortie hello.</span><span class="sxs-lookup"><span data-stu-id="5ff51-168">hello values for these properties match hello output dataset.</span></span> |
| <span data-ttu-id="5ff51-169">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="5ff51-169">linkedServiceName</span></span> |<span data-ttu-id="5ff51-170">désigne le service lié HDInsight de toohello créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="5ff51-170">refers toohello HDInsight linked service you had created earlier.</span></span> |

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

## <a name="run-spark-programs"></a><span data-ttu-id="5ff51-171">Exécuter des programmes Spark</span><span class="sxs-lookup"><span data-stu-id="5ff51-171">Run Spark programs</span></span>
<span data-ttu-id="5ff51-172">Vous pouvez utiliser les programmes MapReduce activité toorun Spark sur votre cluster HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="5ff51-172">You can use MapReduce activity toorun Spark programs on your HDInsight Spark cluster.</span></span> <span data-ttu-id="5ff51-173">Consultez la page [Appeler des programmes Spark à partir d'Azure Data Factory](data-factory-spark.md) pour plus d'informations.</span><span class="sxs-lookup"><span data-stu-id="5ff51-173">See [Invoke Spark programs from Azure Data Factory](data-factory-spark.md) for details.</span></span>  

[developer-reference]: http://go.microsoft.com/fwlink/?LinkId=516908
[cmdlet-reference]: http://go.microsoft.com/fwlink/?LinkId=517456


[adfgetstarted]: data-factory-copy-data-from-azure-blob-storage-to-sql-database.md
[adfgetstartedmonitoring]:data-factory-copy-data-from-azure-blob-storage-to-sql-database.md#monitor-pipelines 

[Developer Reference]: http://go.microsoft.com/fwlink/?LinkId=516908
[Azure Portal]: http://portal.azure.com

## <a name="see-also"></a><span data-ttu-id="5ff51-174">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="5ff51-174">See Also</span></span>
* [<span data-ttu-id="5ff51-175">Activité Hive</span><span class="sxs-lookup"><span data-stu-id="5ff51-175">Hive Activity</span></span>](data-factory-hive-activity.md)
* [<span data-ttu-id="5ff51-176">Activité pig</span><span class="sxs-lookup"><span data-stu-id="5ff51-176">Pig Activity</span></span>](data-factory-pig-activity.md)
* [<span data-ttu-id="5ff51-177">Activité de diffusion en continu Hadoop</span><span class="sxs-lookup"><span data-stu-id="5ff51-177">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
* [<span data-ttu-id="5ff51-178">Appeler des programmes Spark</span><span class="sxs-lookup"><span data-stu-id="5ff51-178">Invoke Spark programs</span></span>](data-factory-spark.md)
* [<span data-ttu-id="5ff51-179">Appeler des scripts R</span><span class="sxs-lookup"><span data-stu-id="5ff51-179">Invoke R scripts</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)

