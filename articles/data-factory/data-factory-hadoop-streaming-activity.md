---
title: "Transformer des données à l’aide d’une activité de diffusion en continu Hadoop - Azure | Microsoft Docs"
description: "Découvrez comment vous pouvez utiliser l’activité de diffusion en continu Hadoop dans une fabrique de données Azure pour transformer les données en exécutant des programmes de diffusion en continu Hadoop sur votre cluster HDInsight propre/à la demande."
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
ms.openlocfilehash: bfe62aa60f5a0ff339e1d495d22a5fdfac10d5dc
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="transform-data-using-hadoop-streaming-activity-in-azure-data-factory"></a><span data-ttu-id="53c53-103">Transformer des données à l’aide d’une activité de diffusion en continu Hadoop dans Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="53c53-103">Transform data using Hadoop Streaming Activity in Azure Data Factory</span></span>
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="53c53-104">Activité Hive</span><span class="sxs-lookup"><span data-stu-id="53c53-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="53c53-105">Activité pig</span><span class="sxs-lookup"><span data-stu-id="53c53-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="53c53-106">Activité MapReduce</span><span class="sxs-lookup"><span data-stu-id="53c53-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="53c53-107">Activité de diffusion en continu Hadoop</span><span class="sxs-lookup"><span data-stu-id="53c53-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="53c53-108">Activité Spark</span><span class="sxs-lookup"><span data-stu-id="53c53-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="53c53-109">Activité d’exécution par lot Machine Learning</span><span class="sxs-lookup"><span data-stu-id="53c53-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="53c53-110">Activité des ressources de mise à jour de Machine Learning</span><span class="sxs-lookup"><span data-stu-id="53c53-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="53c53-111">Activité de procédure stockée</span><span class="sxs-lookup"><span data-stu-id="53c53-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="53c53-112">Activité U-SQL Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="53c53-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="53c53-113">Activité personnalisée .NET</span><span class="sxs-lookup"><span data-stu-id="53c53-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

<span data-ttu-id="53c53-114">Vous pouvez utiliser l’activité HDInsightStreamingActivity pour appeler une tâche de diffusion en continu Hadoop à partir d’un pipeline Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="53c53-114">You can use the HDInsightStreamingActivity Activity invoke a Hadoop Streaming job from an Azure Data Factory pipeline.</span></span> <span data-ttu-id="53c53-115">L’extrait de code JSON suivant illustre la syntaxe pour l’utilisation de HDInsightStreamingActivity dans un fichier JSON de pipeline.</span><span class="sxs-lookup"><span data-stu-id="53c53-115">The following JSON snippet shows the syntax for using the HDInsightStreamingActivity in a pipeline JSON file.</span></span> 

<span data-ttu-id="53c53-116">L’activité de streaming HDInsight dans un [pipeline](data-factory-create-pipelines.md) Data Factory exécute des programmes de streaming Hadoop sur votre cluster HDInsight [propre](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) ou [à la demande](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) sous Windows ou Linux.</span><span class="sxs-lookup"><span data-stu-id="53c53-116">The HDInsight Streaming Activity in a Data Factory [pipeline](data-factory-create-pipelines.md) executes Hadoop Streaming programs on [your own](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) or [on-demand](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) Windows/Linux-based HDInsight cluster.</span></span> <span data-ttu-id="53c53-117">Cet article s'appuie sur l'article [Activités de transformation des données](data-factory-data-transformation-activities.md) qui présente une vue d'ensemble de la transformation des données et les activités de transformation prises en charge.</span><span class="sxs-lookup"><span data-stu-id="53c53-117">This article builds on the [data transformation activities](data-factory-data-transformation-activities.md) article, which presents a general overview of data transformation and the supported transformation activities.</span></span>

> [!NOTE] 
> <span data-ttu-id="53c53-118">Si vous découvrez Azure Data Factory, lisez la [Présentation d’Azure Data Factory](data-factory-introduction.md) et suivez le didacticiel : [Générer votre premier pipeline de données](data-factory-build-your-first-pipeline.md) avant de lire cet article.</span><span class="sxs-lookup"><span data-stu-id="53c53-118">If you are new to Azure Data Factory, read through [Introduction to Azure Data Factory](data-factory-introduction.md) and do the tutorial: [Build your first data pipeline](data-factory-build-your-first-pipeline.md) before reading this article.</span></span> 

## <a name="json-sample"></a><span data-ttu-id="53c53-119">Exemple JSON</span><span class="sxs-lookup"><span data-stu-id="53c53-119">JSON sample</span></span>
<span data-ttu-id="53c53-120">Le cluster HDInsight est automatiquement rempli avec les données (davinci.txt) et les exemples de programmes (wc.exe et cat.exe).</span><span class="sxs-lookup"><span data-stu-id="53c53-120">The HDInsight cluster is automatically populated with example programs (wc.exe and cat.exe) and data (davinci.txt).</span></span> <span data-ttu-id="53c53-121">Par défaut, le nom du conteneur utilisé par le cluster HDInsight est le nom du cluster lui-même.</span><span class="sxs-lookup"><span data-stu-id="53c53-121">By default, name of the container that is used by the HDInsight cluster is the name of the cluster itself.</span></span> <span data-ttu-id="53c53-122">Par exemple, si votre nom de cluster est myhdicluster, le nom du conteneur d’objets blob associé est myhdicluster.</span><span class="sxs-lookup"><span data-stu-id="53c53-122">For example, if your cluster name is myhdicluster, name of the blob container associated would be myhdicluster.</span></span> 

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

<span data-ttu-id="53c53-123">Notez les points suivants :</span><span class="sxs-lookup"><span data-stu-id="53c53-123">Note the following points:</span></span>

1. <span data-ttu-id="53c53-124">Définissez **linkedServiceName** sur le nom du service lié qui pointe vers votre cluster HDInsight sur lequel est exécutée la tâche de diffusion en continu mapreduce.</span><span class="sxs-lookup"><span data-stu-id="53c53-124">Set the **linkedServiceName** to the name of the linked service that points to your HDInsight cluster on which the streaming mapreduce job is run.</span></span>
2. <span data-ttu-id="53c53-125">Affectez au type de l’activité la valeur **HDInsightStreaming**.</span><span class="sxs-lookup"><span data-stu-id="53c53-125">Set the type of the activity to **HDInsightStreaming**.</span></span>
3. <span data-ttu-id="53c53-126">Pour la propriété **mapper** , spécifiez le nom du fichier exécutable du mappeur.</span><span class="sxs-lookup"><span data-stu-id="53c53-126">For the **mapper** property, specify the name of mapper executable.</span></span> <span data-ttu-id="53c53-127">Dans l’exemple, cat.exe est le fichier exécutable du mappeur.</span><span class="sxs-lookup"><span data-stu-id="53c53-127">In the example, cat.exe is the mapper executable.</span></span>
4. <span data-ttu-id="53c53-128">Pour la propriété **reducer** , spécifiez le nom du fichier exécutable du raccord de réduction.</span><span class="sxs-lookup"><span data-stu-id="53c53-128">For the **reducer** property, specify the name of reducer executable.</span></span> <span data-ttu-id="53c53-129">Dans l’exemple, wc.exe est le fichier exécutable du raccord de réduction.</span><span class="sxs-lookup"><span data-stu-id="53c53-129">In the example, wc.exe is the reducer executable.</span></span>
5. <span data-ttu-id="53c53-130">Pour la propriété de type **input** , spécifiez le fichier en entrée (y compris son emplacement) du mappeur.</span><span class="sxs-lookup"><span data-stu-id="53c53-130">For the **input** type property, specify the input file (including the location) for the mapper.</span></span> <span data-ttu-id="53c53-131">Dans l’exemple « wasb://adfsample@<account name>.blob.core.windows.net/example/data/gutenberg/davinci.txt », adfsample est le conteneur de l’objet blob, example/data/Gutenberg est le dossier et davinci.txt est l’objet blob.</span><span class="sxs-lookup"><span data-stu-id="53c53-131">In the example: "wasb://adfsample@<account name>.blob.core.windows.net/example/data/gutenberg/davinci.txt": adfsample is the blob container, example/data/Gutenberg is the folder, and davinci.txt is the blob.</span></span>
6. <span data-ttu-id="53c53-132">Pour la propriété de type **output** , spécifiez le fichier en sortie (y compris son emplacement) du raccord de réduction.</span><span class="sxs-lookup"><span data-stu-id="53c53-132">For the **output** type property, specify the output file (including the location) for the reducer.</span></span> <span data-ttu-id="53c53-133">La sortie de la tâche de diffusion en continu Hadoop est écrite à l’emplacement spécifié pour cette propriété.</span><span class="sxs-lookup"><span data-stu-id="53c53-133">The output of the Hadoop Streaming job is written to the location specified for this property.</span></span>
7. <span data-ttu-id="53c53-134">Dans la section **filePaths** , spécifiez les chemins des fichiers exécutables du mappeur et du raccord de réduction.</span><span class="sxs-lookup"><span data-stu-id="53c53-134">In the **filePaths** section, specify the paths for the mapper and reducer executables.</span></span> <span data-ttu-id="53c53-135">Dans l’exemple « adfsample/example/apps/wc.exe », adfsample est le conteneur de l’objet blob, example/apps est le dossier et wc.exe est le fichier exécutable.</span><span class="sxs-lookup"><span data-stu-id="53c53-135">In the example: "adfsample/example/apps/wc.exe", adfsample is the blob container, example/apps is the folder, and wc.exe is the executable.</span></span>
8. <span data-ttu-id="53c53-136">Pour la propriété **fileLinkedService** , spécifiez le service lié Azure Storage qui représente le stockage Azure qui contient les fichiers spécifiés dans la section filePaths.</span><span class="sxs-lookup"><span data-stu-id="53c53-136">For the **fileLinkedService** property, specify the Azure Storage linked service that represents the Azure storage that contains the files specified in the filePaths section.</span></span>
9. <span data-ttu-id="53c53-137">Pour la propriété **arguments** , spécifiez les arguments de la tâche de diffusion en continu.</span><span class="sxs-lookup"><span data-stu-id="53c53-137">For the **arguments** property, specify the arguments for the streaming job.</span></span>
10. <span data-ttu-id="53c53-138">La propriété **getDebugInfo** est un élément facultatif.</span><span class="sxs-lookup"><span data-stu-id="53c53-138">The **getDebugInfo** property is an optional element.</span></span> <span data-ttu-id="53c53-139">Si sa valeur est Failure, les journaux ne sont téléchargés qu’en cas d’échec.</span><span class="sxs-lookup"><span data-stu-id="53c53-139">When it is set to Failure, the logs are downloaded only on failure.</span></span> <span data-ttu-id="53c53-140">Si sa valeur est Toujours, les journaux sont toujours téléchargés, quel que soit l’état de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="53c53-140">When it is set to Always, logs are always downloaded irrespective of the execution status.</span></span>

> [!NOTE]
> <span data-ttu-id="53c53-141">Comme indiqué dans l’exemple, vous spécifiez un jeu de données de sortie pour l’activité de diffusion en continu Hadoop pour la propriété **outputs** .</span><span class="sxs-lookup"><span data-stu-id="53c53-141">As shown in the example, you specify an output dataset for the Hadoop Streaming Activity for the **outputs** property.</span></span> <span data-ttu-id="53c53-142">Il s’agit simplement d’un ensemble de données factice qui est nécessaire au fonctionnement de la planification de pipeline.</span><span class="sxs-lookup"><span data-stu-id="53c53-142">This dataset is just a dummy dataset that is required to drive the pipeline schedule.</span></span> <span data-ttu-id="53c53-143">Il est inutile de spécifier un jeu de données en entrée pour l’activité de la propriété **entrées** .</span><span class="sxs-lookup"><span data-stu-id="53c53-143">You do not need to specify any input dataset for the activity for the **inputs** property.</span></span>  
> 
> 

## <a name="example"></a><span data-ttu-id="53c53-144">Exemple</span><span class="sxs-lookup"><span data-stu-id="53c53-144">Example</span></span>
<span data-ttu-id="53c53-145">Le pipeline dans cette procédure pas à pas exécute le programme de diffusion en continu Map/Reduce de calcul du nombre de mots sur votre cluster Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="53c53-145">The pipeline in this walkthrough runs the Word Count streaming Map/Reduce program on your Azure HDInsight cluster.</span></span> 

### <a name="linked-services"></a><span data-ttu-id="53c53-146">Services liés</span><span class="sxs-lookup"><span data-stu-id="53c53-146">Linked services</span></span>
#### <a name="azure-storage-linked-service"></a><span data-ttu-id="53c53-147">Service lié Azure Storage</span><span class="sxs-lookup"><span data-stu-id="53c53-147">Azure Storage linked service</span></span>
<span data-ttu-id="53c53-148">Tout d'abord, vous créez un service lié pour lier le stockage Azure qui est utilisé par le cluster Azure HDInsight à la fabrique de données Azure.</span><span class="sxs-lookup"><span data-stu-id="53c53-148">First, you create a linked service to link the Azure Storage that is used by the Azure HDInsight cluster to the Azure data factory.</span></span> <span data-ttu-id="53c53-149">Si vous copiez/collez le code suivant, n’oubliez pas de remplacer le nom de compte et la clé de compte par le nom et la clé de votre stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="53c53-149">If you copy/paste the following code, do not forget to replace account name and account key with the name and key of your Azure Storage.</span></span> 

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

#### <a name="azure-hdinsight-linked-service"></a><span data-ttu-id="53c53-150">Service lié Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="53c53-150">Azure HDInsight linked service</span></span>
<span data-ttu-id="53c53-151">Tout d'abord, vous créez un service lié pour lier le cluster Azure HDInsight à la fabrique de données Azure.</span><span class="sxs-lookup"><span data-stu-id="53c53-151">Next, you create a linked service to link your Azure HDInsight cluster to the Azure data factory.</span></span> <span data-ttu-id="53c53-152">Si vous copiez/collez le code suivant, remplacez le nom du cluster HDInsight par le nom de votre cluster HDInsight et modifiez le nom d’utilisateur et le mot de passe.</span><span class="sxs-lookup"><span data-stu-id="53c53-152">If you copy/paste the following code, replace HDInsight cluster name with the name of your HDInsight cluster, and change user name and password values.</span></span> 

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

### <a name="datasets"></a><span data-ttu-id="53c53-153">Groupes de données</span><span class="sxs-lookup"><span data-stu-id="53c53-153">Datasets</span></span>
#### <a name="output-dataset"></a><span data-ttu-id="53c53-154">Jeu de données de sortie</span><span class="sxs-lookup"><span data-stu-id="53c53-154">Output dataset</span></span>
<span data-ttu-id="53c53-155">Le pipeline de cet exemple n’accepte pas d’entrées.</span><span class="sxs-lookup"><span data-stu-id="53c53-155">The pipeline in this example does not take any inputs.</span></span> <span data-ttu-id="53c53-156">Vous spécifiez un jeu de données de sortie pour l’activité de diffusion en continu HDInsight.</span><span class="sxs-lookup"><span data-stu-id="53c53-156">You specify an output dataset for the HDInsight Streaming Activity.</span></span> <span data-ttu-id="53c53-157">Il s’agit simplement d’un ensemble de données factice qui est nécessaire au fonctionnement de la planification de pipeline.</span><span class="sxs-lookup"><span data-stu-id="53c53-157">This dataset is just a dummy dataset that is required to drive the pipeline schedule.</span></span> 

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

### <a name="pipeline"></a><span data-ttu-id="53c53-158">Pipeline</span><span class="sxs-lookup"><span data-stu-id="53c53-158">Pipeline</span></span>
<span data-ttu-id="53c53-159">Le pipeline de cet exemple n’a qu’une seule activité de type : **HDInsightStreaming**.</span><span class="sxs-lookup"><span data-stu-id="53c53-159">The pipeline in this example has only one activity that is of type: **HDInsightStreaming**.</span></span> 

<span data-ttu-id="53c53-160">Le cluster HDInsight est automatiquement rempli avec les données (davinci.txt) et les exemples de programmes (wc.exe et cat.exe).</span><span class="sxs-lookup"><span data-stu-id="53c53-160">The HDInsight cluster is automatically populated with example programs (wc.exe and cat.exe) and data (davinci.txt).</span></span> <span data-ttu-id="53c53-161">Par défaut, le nom du conteneur utilisé par le cluster HDInsight est le nom du cluster lui-même.</span><span class="sxs-lookup"><span data-stu-id="53c53-161">By default, name of the container that is used by the HDInsight cluster is the name of the cluster itself.</span></span> <span data-ttu-id="53c53-162">Par exemple, si votre nom de cluster est myhdicluster, le nom du conteneur d’objets blob associé est myhdicluster.</span><span class="sxs-lookup"><span data-stu-id="53c53-162">For example, if your cluster name is myhdicluster, name of the blob container associated would be myhdicluster.</span></span>  

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
## <a name="see-also"></a><span data-ttu-id="53c53-163">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="53c53-163">See Also</span></span>
* [<span data-ttu-id="53c53-164">Activité Hive</span><span class="sxs-lookup"><span data-stu-id="53c53-164">Hive Activity</span></span>](data-factory-hive-activity.md)
* [<span data-ttu-id="53c53-165">Activité pig</span><span class="sxs-lookup"><span data-stu-id="53c53-165">Pig Activity</span></span>](data-factory-pig-activity.md)
* [<span data-ttu-id="53c53-166">Activité MapReduce</span><span class="sxs-lookup"><span data-stu-id="53c53-166">MapReduce Activity</span></span>](data-factory-map-reduce.md)
* [<span data-ttu-id="53c53-167">Appeler des programmes Spark</span><span class="sxs-lookup"><span data-stu-id="53c53-167">Invoke Spark programs</span></span>](data-factory-spark.md)
* [<span data-ttu-id="53c53-168">Appeler des scripts R</span><span class="sxs-lookup"><span data-stu-id="53c53-168">Invoke R scripts</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)

