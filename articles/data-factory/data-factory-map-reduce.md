---
title: "Appeler le programme MapReduce à partir d'Azure Data Factory"
description: Learn how to process data by running MapReduce programs on an Azure HDInsight cluster from an Azure data factory.
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
ms.openlocfilehash: 55fc2196cb4ba50eced4a463914ae188217d0fed
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="invoke-mapreduce-programs-from-data-factory"></a><span data-ttu-id="575d3-103">Appeler des programmes MapReduce à partir de Data Factory</span><span class="sxs-lookup"><span data-stu-id="575d3-103">Invoke MapReduce Programs from Data Factory</span></span>
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="575d3-104">Activité Hive</span><span class="sxs-lookup"><span data-stu-id="575d3-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="575d3-105">Activité pig</span><span class="sxs-lookup"><span data-stu-id="575d3-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="575d3-106">Activité MapReduce</span><span class="sxs-lookup"><span data-stu-id="575d3-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="575d3-107">Activité de diffusion en continu Hadoop</span><span class="sxs-lookup"><span data-stu-id="575d3-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="575d3-108">Activité Spark</span><span class="sxs-lookup"><span data-stu-id="575d3-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="575d3-109">Activité d’exécution par lot Machine Learning</span><span class="sxs-lookup"><span data-stu-id="575d3-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="575d3-110">Activité des ressources de mise à jour de Machine Learning</span><span class="sxs-lookup"><span data-stu-id="575d3-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="575d3-111">Activité de procédure stockée</span><span class="sxs-lookup"><span data-stu-id="575d3-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="575d3-112">Activité U-SQL Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="575d3-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="575d3-113">Activité personnalisée .NET</span><span class="sxs-lookup"><span data-stu-id="575d3-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

<span data-ttu-id="575d3-114">L’activité MapReduce de HDInsight dans un [pipeline](data-factory-create-pipelines.md) Data Factory exécute des programmes MapReduce sur votre cluster HDInsight [propre](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) ou [à la demande](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) sous Windows ou Linux.</span><span class="sxs-lookup"><span data-stu-id="575d3-114">The HDInsight MapReduce activity in a Data Factory [pipeline](data-factory-create-pipelines.md) executes MapReduce programs on [your own](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) or [on-demand](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) Windows/Linux-based HDInsight cluster.</span></span> <span data-ttu-id="575d3-115">Cet article s'appuie sur l'article [Activités de transformation des données](data-factory-data-transformation-activities.md) qui présente une vue d'ensemble de la transformation des données et les activités de transformation prises en charge.</span><span class="sxs-lookup"><span data-stu-id="575d3-115">This article builds on the [data transformation activities](data-factory-data-transformation-activities.md) article, which presents a general overview of data transformation and the supported transformation activities.</span></span>

> [!NOTE] 
> <span data-ttu-id="575d3-116">Si vous découvrez Azure Data Factory, lisez la [Présentation d’Azure Data Factory](data-factory-introduction.md) et suivez le didacticiel : [Générer votre premier pipeline de données](data-factory-build-your-first-pipeline.md) avant de lire cet article.</span><span class="sxs-lookup"><span data-stu-id="575d3-116">If you are new to Azure Data Factory, read through [Introduction to Azure Data Factory](data-factory-introduction.md) and do the tutorial: [Build your first data pipeline](data-factory-build-your-first-pipeline.md) before reading this article.</span></span>  

## <a name="introduction"></a><span data-ttu-id="575d3-117">Introduction</span><span class="sxs-lookup"><span data-stu-id="575d3-117">Introduction</span></span>
<span data-ttu-id="575d3-118">Un pipeline dans une fabrique de données Azure traite les données dans les services de stockage liés à l'aide des services de calcul liés.</span><span class="sxs-lookup"><span data-stu-id="575d3-118">A pipeline in an Azure data factory processes data in linked storage services by using linked compute services.</span></span> <span data-ttu-id="575d3-119">Il contient une séquence d'activités dans laquelle chaque activité effectue une opération de traitement spécifique.</span><span class="sxs-lookup"><span data-stu-id="575d3-119">It contains a sequence of activities where each activity performs a specific processing operation.</span></span> <span data-ttu-id="575d3-120">Cet article décrit l'utilisation de l’activité MapReduce de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="575d3-120">This article describes using the HDInsight MapReduce Activity.</span></span>

<span data-ttu-id="575d3-121">Consultez [Pig](data-factory-pig-activity.md) et [Hive](data-factory-hive-activity.md) pour plus d’informations sur l’exécution de scripts Pig/Hive sur un cluster HDInsight sous Windows ou Linux à partir d’un pipeline à l’aide des activités Pig et Hive de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="575d3-121">See [Pig](data-factory-pig-activity.md) and [Hive](data-factory-hive-activity.md) for details about running Pig/Hive scripts on a Windows/Linux-based HDInsight cluster from a pipeline by using HDInsight Pig and Hive activities.</span></span> 

## <a name="json-for-hdinsight-mapreduce-activity"></a><span data-ttu-id="575d3-122">JSON pour l’activité MapReduce de HDInsight</span><span class="sxs-lookup"><span data-stu-id="575d3-122">JSON for HDInsight MapReduce Activity</span></span>
<span data-ttu-id="575d3-123">Dans la définition JSON de l’activité HDInsight :</span><span class="sxs-lookup"><span data-stu-id="575d3-123">In the JSON definition for the HDInsight Activity:</span></span> 

1. <span data-ttu-id="575d3-124">Affectez au **type** de l’**activité** la valeur **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="575d3-124">Set the **type** of the **activity** to **HDInsight**.</span></span>
2. <span data-ttu-id="575d3-125">Spécifiez le nom de la classe pour la propriété **className** .</span><span class="sxs-lookup"><span data-stu-id="575d3-125">Specify the name of the class for **className** property.</span></span>
3. <span data-ttu-id="575d3-126">Spécifiez le chemin d’accès du fichier JAR, ainsi que le nom de fichier, pour la propriété **jarFilePath** .</span><span class="sxs-lookup"><span data-stu-id="575d3-126">Specify the path to the JAR file including the file name for **jarFilePath** property.</span></span>
4. <span data-ttu-id="575d3-127">Spécifiez le service lié qui fait référence au stockage d’objets blob Azure contenant le fichier JAR pour la propriété **jarLinkedService** .</span><span class="sxs-lookup"><span data-stu-id="575d3-127">Specify the linked service that refers to the Azure Blob Storage that contains the JAR file for **jarLinkedService** property.</span></span>   
5. <span data-ttu-id="575d3-128">Spécifiez les arguments du programme MapReduce dans la section **arguments**.</span><span class="sxs-lookup"><span data-stu-id="575d3-128">Specify any arguments for the MapReduce program in the **arguments** section.</span></span> <span data-ttu-id="575d3-129">Lors de l’exécution, vous verrez quelques arguments supplémentaires (par exemple : mapreduce.job.tags) à partir de l’infrastructure MapReduce.</span><span class="sxs-lookup"><span data-stu-id="575d3-129">At runtime, you see a few extra arguments (for example: mapreduce.job.tags) from the MapReduce framework.</span></span> <span data-ttu-id="575d3-130">Pour différencier vos arguments avec les arguments MapReduce, envisagez d’utiliser l’option et la valeur en tant qu’arguments comme indiqué dans l’exemple suivant (-s, --entrée, --sortie etc. sont des options immédiatement suivies par leurs valeurs).</span><span class="sxs-lookup"><span data-stu-id="575d3-130">To differentiate your arguments with the MapReduce arguments, consider using both option and value as arguments as shown in the following example (-s, --input, --output etc., are options immediately followed by their values).</span></span>

    ```JSON   
    {
        "name": "MahoutMapReduceSamplePipeline",
        "properties": {
            "description": "Sample Pipeline to Run a Mahout Custom Map Reduce Jar. This job calcuates an Item Similarity Matrix to determine the similarity between 2 items",
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
                    "description": "Custom Map Reduce to generate Mahout result",
                    "linkedServiceName": "HDInsightLinkedService"
                }
            ],
            "start": "2017-01-03T00:00:00Z",
            "end": "2017-01-04T00:00:00Z"
        }
    }
    ```
<span data-ttu-id="575d3-131">Vous pouvez utiliser l’activité MapReduce de HDInsight pour exécuter un fichier jar MapReduce dans un cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="575d3-131">You can use the HDInsight MapReduce Activity to run any MapReduce jar file on an HDInsight cluster.</span></span> <span data-ttu-id="575d3-132">Dans l'exemple suivant de définition JSON d'un pipeline, l'activité HDInsight est configurée pour exécuter un fichier JAR Mahout.</span><span class="sxs-lookup"><span data-stu-id="575d3-132">In the following sample JSON definition of a pipeline, the HDInsight Activity is configured to run a Mahout JAR file.</span></span>

## <a name="sample-on-github"></a><span data-ttu-id="575d3-133">Exemple sur GitHub</span><span class="sxs-lookup"><span data-stu-id="575d3-133">Sample on GitHub</span></span>
<span data-ttu-id="575d3-134">Vous pouvez télécharger un exemple d’utilisation de l’activité MapReduce HDInsight à l’emplacement suivant : [Exemples Data Factory sur GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/JSON/MapReduce_Activity_Sample).</span><span class="sxs-lookup"><span data-stu-id="575d3-134">You can download a sample for using the HDInsight MapReduce Activity from: [Data Factory Samples on GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/JSON/MapReduce_Activity_Sample).</span></span>  

## <a name="running-the-word-count-program"></a><span data-ttu-id="575d3-135">Exécution du programme de nombre de mots</span><span class="sxs-lookup"><span data-stu-id="575d3-135">Running the Word Count program</span></span>
<span data-ttu-id="575d3-136">Le pipeline dans cet exemple exécute le programme Map/Reduce du nombre de mots sur votre cluster Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="575d3-136">The pipeline in this example runs the Word Count Map/Reduce program on your Azure HDInsight cluster.</span></span>   

### <a name="linked-services"></a><span data-ttu-id="575d3-137">Services liés</span><span class="sxs-lookup"><span data-stu-id="575d3-137">Linked Services</span></span>
<span data-ttu-id="575d3-138">Tout d'abord, vous créez un service lié pour lier le stockage Azure qui est utilisé par le cluster Azure HDInsight à la fabrique de données Azure.</span><span class="sxs-lookup"><span data-stu-id="575d3-138">First, you create a linked service to link the Azure Storage that is used by the Azure HDInsight cluster to the Azure data factory.</span></span> <span data-ttu-id="575d3-139">Si vous copiez/collez le code suivant, n’oubliez pas de remplacer le **nom de compte** et la **clé de compte** par le nom et la clé de votre stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="575d3-139">If you copy/paste the following code, do not forget to replace **account name** and **account key** with the name and key of your Azure Storage.</span></span> 

#### <a name="azure-storage-linked-service"></a><span data-ttu-id="575d3-140">Service lié Azure Storage</span><span class="sxs-lookup"><span data-stu-id="575d3-140">Azure Storage linked service</span></span>

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

#### <a name="azure-hdinsight-linked-service"></a><span data-ttu-id="575d3-141">Service lié Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="575d3-141">Azure HDInsight linked service</span></span>
<span data-ttu-id="575d3-142">Tout d'abord, vous créez un service lié pour lier le cluster Azure HDInsight à la fabrique de données Azure.</span><span class="sxs-lookup"><span data-stu-id="575d3-142">Next, you create a linked service to link your Azure HDInsight cluster to the Azure data factory.</span></span> <span data-ttu-id="575d3-143">Si vous copiez/collez le code suivant, remplacez **le nom du cluster HDInsight** par le nom de votre cluster HDInsight et modifiez le nom d’utilisateur et le mot de passe.</span><span class="sxs-lookup"><span data-stu-id="575d3-143">If you copy/paste the following code, replace **HDInsight cluster name** with the name of your HDInsight cluster, and change user name and password values.</span></span>   

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

### <a name="datasets"></a><span data-ttu-id="575d3-144">Groupes de données</span><span class="sxs-lookup"><span data-stu-id="575d3-144">Datasets</span></span>
#### <a name="output-dataset"></a><span data-ttu-id="575d3-145">Jeu de données de sortie</span><span class="sxs-lookup"><span data-stu-id="575d3-145">Output dataset</span></span>
<span data-ttu-id="575d3-146">Le pipeline de cet exemple n’accepte pas d’entrées.</span><span class="sxs-lookup"><span data-stu-id="575d3-146">The pipeline in this example does not take any inputs.</span></span> <span data-ttu-id="575d3-147">Vous spécifiez un jeu de données de sortie pour l’activité MapReduce HDInsight.</span><span class="sxs-lookup"><span data-stu-id="575d3-147">You specify an output dataset for the HDInsight MapReduce Activity.</span></span> <span data-ttu-id="575d3-148">Il s’agit simplement d’un ensemble de données factice qui est nécessaire au fonctionnement de la planification de pipeline.</span><span class="sxs-lookup"><span data-stu-id="575d3-148">This dataset is just a dummy dataset that is required to drive the pipeline schedule.</span></span>  

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

### <a name="pipeline"></a><span data-ttu-id="575d3-149">Pipeline</span><span class="sxs-lookup"><span data-stu-id="575d3-149">Pipeline</span></span>
<span data-ttu-id="575d3-150">Le pipeline de cet exemple n'a qu'une seule activité de type : HDInsightMapReduce.</span><span class="sxs-lookup"><span data-stu-id="575d3-150">The pipeline in this example has only one activity that is of type: HDInsightMapReduce.</span></span> <span data-ttu-id="575d3-151">Certaines propriétés importantes dans le JSON sont :</span><span class="sxs-lookup"><span data-stu-id="575d3-151">Some of the important properties in the JSON are:</span></span> 

| <span data-ttu-id="575d3-152">Propriété</span><span class="sxs-lookup"><span data-stu-id="575d3-152">Property</span></span> | <span data-ttu-id="575d3-153">Remarques</span><span class="sxs-lookup"><span data-stu-id="575d3-153">Notes</span></span> |
|:--- |:--- |
| <span data-ttu-id="575d3-154">type</span><span class="sxs-lookup"><span data-stu-id="575d3-154">type</span></span> |<span data-ttu-id="575d3-155">Le type doit être défini sur **HDInsightMapReduce**.</span><span class="sxs-lookup"><span data-stu-id="575d3-155">The type must be set to **HDInsightMapReduce**.</span></span> |
| <span data-ttu-id="575d3-156">className</span><span class="sxs-lookup"><span data-stu-id="575d3-156">className</span></span> |<span data-ttu-id="575d3-157">Le nom de la classe est : **wordcount**</span><span class="sxs-lookup"><span data-stu-id="575d3-157">Name of the class is: **wordcount**</span></span> |
| <span data-ttu-id="575d3-158">jarFilePath</span><span class="sxs-lookup"><span data-stu-id="575d3-158">jarFilePath</span></span> |<span data-ttu-id="575d3-159">Chemin d’accès au fichier jar contenant la classe.</span><span class="sxs-lookup"><span data-stu-id="575d3-159">Path to the jar file containing the class.</span></span> <span data-ttu-id="575d3-160">Si vous copiez/collez le code suivant, n'oubliez pas de modifier le nom du cluster.</span><span class="sxs-lookup"><span data-stu-id="575d3-160">If you copy/paste the following code, don't forget to change the name of the cluster.</span></span> |
| <span data-ttu-id="575d3-161">jarLinkedService</span><span class="sxs-lookup"><span data-stu-id="575d3-161">jarLinkedService</span></span> |<span data-ttu-id="575d3-162">Service Azure Storage lié qui contient le fichier jar.</span><span class="sxs-lookup"><span data-stu-id="575d3-162">Azure Storage linked service that contains the jar file.</span></span> <span data-ttu-id="575d3-163">Ce service lié fait référence au stockage associé au cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="575d3-163">This linked service refers to the storage that is associated with the HDInsight cluster.</span></span> |
| <span data-ttu-id="575d3-164">arguments</span><span class="sxs-lookup"><span data-stu-id="575d3-164">arguments</span></span> |<span data-ttu-id="575d3-165">Le programme de nombre de mots accepte deux arguments, une entrée et une sortie.</span><span class="sxs-lookup"><span data-stu-id="575d3-165">The wordcount program takes two arguments, an input and an output.</span></span> <span data-ttu-id="575d3-166">Le fichier d'entrée est le fichier davinci.txt.</span><span class="sxs-lookup"><span data-stu-id="575d3-166">The input file is the davinci.txt file.</span></span> |
| <span data-ttu-id="575d3-167">frequency/interval</span><span class="sxs-lookup"><span data-stu-id="575d3-167">frequency/interval</span></span> |<span data-ttu-id="575d3-168">Les valeurs de ces propriétés correspondent au jeu de données de sortie.</span><span class="sxs-lookup"><span data-stu-id="575d3-168">The values for these properties match the output dataset.</span></span> |
| <span data-ttu-id="575d3-169">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="575d3-169">linkedServiceName</span></span> |<span data-ttu-id="575d3-170">fait référence au service HDInsight lié créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="575d3-170">refers to the HDInsight linked service you had created earlier.</span></span> |

```JSON
{
    "name": "MRSamplePipeline",
    "properties": {
        "description": "Sample Pipeline to Run the Word Count Program",
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

## <a name="run-spark-programs"></a><span data-ttu-id="575d3-171">Exécuter des programmes Spark</span><span class="sxs-lookup"><span data-stu-id="575d3-171">Run Spark programs</span></span>
<span data-ttu-id="575d3-172">Vous pouvez utiliser l'activité MapReduce pour exécuter des programmes Spark sur votre cluster HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="575d3-172">You can use MapReduce activity to run Spark programs on your HDInsight Spark cluster.</span></span> <span data-ttu-id="575d3-173">Consultez la page [Appeler des programmes Spark à partir d'Azure Data Factory](data-factory-spark.md) pour plus d'informations.</span><span class="sxs-lookup"><span data-stu-id="575d3-173">See [Invoke Spark programs from Azure Data Factory](data-factory-spark.md) for details.</span></span>  

[developer-reference]: http://go.microsoft.com/fwlink/?LinkId=516908
[cmdlet-reference]: http://go.microsoft.com/fwlink/?LinkId=517456


[adfgetstarted]: data-factory-copy-data-from-azure-blob-storage-to-sql-database.md
[adfgetstartedmonitoring]:data-factory-copy-data-from-azure-blob-storage-to-sql-database.md#monitor-pipelines 

[Developer Reference]: http://go.microsoft.com/fwlink/?LinkId=516908
[Azure Portal]: http://portal.azure.com

## <a name="see-also"></a><span data-ttu-id="575d3-174">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="575d3-174">See Also</span></span>
* [<span data-ttu-id="575d3-175">Activité Hive</span><span class="sxs-lookup"><span data-stu-id="575d3-175">Hive Activity</span></span>](data-factory-hive-activity.md)
* [<span data-ttu-id="575d3-176">Activité pig</span><span class="sxs-lookup"><span data-stu-id="575d3-176">Pig Activity</span></span>](data-factory-pig-activity.md)
* [<span data-ttu-id="575d3-177">Activité de diffusion en continu Hadoop</span><span class="sxs-lookup"><span data-stu-id="575d3-177">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
* [<span data-ttu-id="575d3-178">Appeler des programmes Spark</span><span class="sxs-lookup"><span data-stu-id="575d3-178">Invoke Spark programs</span></span>](data-factory-spark.md)
* [<span data-ttu-id="575d3-179">Appeler des scripts R</span><span class="sxs-lookup"><span data-stu-id="575d3-179">Invoke R scripts</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)

