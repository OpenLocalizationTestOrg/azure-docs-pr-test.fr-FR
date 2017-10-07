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
# <a name="transform-data-using-hadoop-streaming-activity-in-azure-data-factory"></a><span data-ttu-id="d358f-103">Transformer des données à l’aide d’une activité de diffusion en continu Hadoop dans Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="d358f-103">Transform data using Hadoop Streaming Activity in Azure Data Factory</span></span>
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="d358f-104">Activité Hive</span><span class="sxs-lookup"><span data-stu-id="d358f-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="d358f-105">Activité pig</span><span class="sxs-lookup"><span data-stu-id="d358f-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="d358f-106">Activité MapReduce</span><span class="sxs-lookup"><span data-stu-id="d358f-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="d358f-107">Activité de diffusion en continu Hadoop</span><span class="sxs-lookup"><span data-stu-id="d358f-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="d358f-108">Activité Spark</span><span class="sxs-lookup"><span data-stu-id="d358f-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="d358f-109">Activité d’exécution par lot Machine Learning</span><span class="sxs-lookup"><span data-stu-id="d358f-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="d358f-110">Activité des ressources de mise à jour de Machine Learning</span><span class="sxs-lookup"><span data-stu-id="d358f-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="d358f-111">Activité de procédure stockée</span><span class="sxs-lookup"><span data-stu-id="d358f-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="d358f-112">Activité U-SQL Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="d358f-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="d358f-113">Activité personnalisée .NET</span><span class="sxs-lookup"><span data-stu-id="d358f-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

<span data-ttu-id="d358f-114">Vous pouvez utiliser hello HDInsightStreamingActivity activité appeler un travail Hadoop de diffusion en continu à partir d’un pipeline Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="d358f-114">You can use hello HDInsightStreamingActivity Activity invoke a Hadoop Streaming job from an Azure Data Factory pipeline.</span></span> <span data-ttu-id="d358f-115">Hello extrait de code JSON suivant illustre syntaxe hello pour l’utilisation de hello HDInsightStreamingActivity dans un fichier JSON de pipeline.</span><span class="sxs-lookup"><span data-stu-id="d358f-115">hello following JSON snippet shows hello syntax for using hello HDInsightStreamingActivity in a pipeline JSON file.</span></span> 

<span data-ttu-id="d358f-116">Hello activité de diffusion en continu HDInsight dans une fabrique de données [pipeline](data-factory-create-pipelines.md) exécute les programmes de diffusion en continu Hadoop sur [votre propre](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) ou [à la demande](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) HDInsight de basés sur Windows/Linux cluster.</span><span class="sxs-lookup"><span data-stu-id="d358f-116">hello HDInsight Streaming Activity in a Data Factory [pipeline](data-factory-create-pipelines.md) executes Hadoop Streaming programs on [your own](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) or [on-demand](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) Windows/Linux-based HDInsight cluster.</span></span> <span data-ttu-id="d358f-117">Cet article s’appuie sur hello [activités de transformation des données](data-factory-data-transformation-activities.md) article, qui présente une vue d’ensemble de la transformation des données et des activités de transformation hello pris en charge.</span><span class="sxs-lookup"><span data-stu-id="d358f-117">This article builds on hello [data transformation activities](data-factory-data-transformation-activities.md) article, which presents a general overview of data transformation and hello supported transformation activities.</span></span>

> [!NOTE] 
> <span data-ttu-id="d358f-118">Si vous êtes tooAzure nouvelle fabrique de données, lisez [Introduction tooAzure Data Factory](data-factory-introduction.md) et hello didacticiel : [générer votre première pipeline de données](data-factory-build-your-first-pipeline.md) avant de lire cet article.</span><span class="sxs-lookup"><span data-stu-id="d358f-118">If you are new tooAzure Data Factory, read through [Introduction tooAzure Data Factory](data-factory-introduction.md) and do hello tutorial: [Build your first data pipeline](data-factory-build-your-first-pipeline.md) before reading this article.</span></span> 

## <a name="json-sample"></a><span data-ttu-id="d358f-119">Exemple JSON</span><span class="sxs-lookup"><span data-stu-id="d358f-119">JSON sample</span></span>
<span data-ttu-id="d358f-120">cluster HDInsight de Hello est automatiquement remplie avec les données (davinci.txt) et les exemples de programmes (wc.exe et cat.exe).</span><span class="sxs-lookup"><span data-stu-id="d358f-120">hello HDInsight cluster is automatically populated with example programs (wc.exe and cat.exe) and data (davinci.txt).</span></span> <span data-ttu-id="d358f-121">Par défaut, le nom du conteneur de hello est utilisé par le cluster HDInsight de hello est nom hello de cluster hello lui-même.</span><span class="sxs-lookup"><span data-stu-id="d358f-121">By default, name of hello container that is used by hello HDInsight cluster is hello name of hello cluster itself.</span></span> <span data-ttu-id="d358f-122">Par exemple, si votre nom de cluster est myhdicluster, nom du conteneur d’objets blob hello associé serait myhdicluster.</span><span class="sxs-lookup"><span data-stu-id="d358f-122">For example, if your cluster name is myhdicluster, name of hello blob container associated would be myhdicluster.</span></span> 

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

<span data-ttu-id="d358f-123">Hello Notez les points suivants :</span><span class="sxs-lookup"><span data-stu-id="d358f-123">Note hello following points:</span></span>

1. <span data-ttu-id="d358f-124">Ensemble hello **linkedServiceName** toohello le nom de hello lié service qui pointe le cluster HDInsight de tooyour sur le hello mapreduce de diffusion en continu le travail est exécuté.</span><span class="sxs-lookup"><span data-stu-id="d358f-124">Set hello **linkedServiceName** toohello name of hello linked service that points tooyour HDInsight cluster on which hello streaming mapreduce job is run.</span></span>
2. <span data-ttu-id="d358f-125">Définir le type de hello d’activité hello trop**HDInsightStreaming**.</span><span class="sxs-lookup"><span data-stu-id="d358f-125">Set hello type of hello activity too**HDInsightStreaming**.</span></span>
3. <span data-ttu-id="d358f-126">Pourquoi **Mappeur** propriété, spécifiez le nom hello du fichier exécutable du mappeur.</span><span class="sxs-lookup"><span data-stu-id="d358f-126">For hello **mapper** property, specify hello name of mapper executable.</span></span> <span data-ttu-id="d358f-127">Dans l’exemple de hello, cat.exe est le Mappeur hello exécutable.</span><span class="sxs-lookup"><span data-stu-id="d358f-127">In hello example, cat.exe is hello mapper executable.</span></span>
4. <span data-ttu-id="d358f-128">Pourquoi **réducteur** propriété, spécifiez le nom hello du fichier exécutable du réducteur.</span><span class="sxs-lookup"><span data-stu-id="d358f-128">For hello **reducer** property, specify hello name of reducer executable.</span></span> <span data-ttu-id="d358f-129">Dans l’exemple de hello, wc.exe est hello fichier exécutable du réducteur.</span><span class="sxs-lookup"><span data-stu-id="d358f-129">In hello example, wc.exe is hello reducer executable.</span></span>
5. <span data-ttu-id="d358f-130">Pourquoi **d’entrée** la propriété de type, spécifiez le fichier d’entrée de hello (y compris l’emplacement de hello) pour le Mappeur hello.</span><span class="sxs-lookup"><span data-stu-id="d358f-130">For hello **input** type property, specify hello input file (including hello location) for hello mapper.</span></span> <span data-ttu-id="d358f-131">Dans l’exemple de hello : « wasb://adfsample@<account name>.blob.core.windows.net/example/data/gutenberg/davinci.txt » : adfsample est le conteneur d’objets blob hello, exemple/data/Gutenberg est hello dossier, et davinci.txt est l’objet blob de hello.</span><span class="sxs-lookup"><span data-stu-id="d358f-131">In hello example: "wasb://adfsample@<account name>.blob.core.windows.net/example/data/gutenberg/davinci.txt": adfsample is hello blob container, example/data/Gutenberg is hello folder, and davinci.txt is hello blob.</span></span>
6. <span data-ttu-id="d358f-132">Pourquoi **sortie** la propriété de type, spécifiez le fichier de sortie de hello (y compris l’emplacement de hello) pour le réducteur de hello.</span><span class="sxs-lookup"><span data-stu-id="d358f-132">For hello **output** type property, specify hello output file (including hello location) for hello reducer.</span></span> <span data-ttu-id="d358f-133">sortie de Hello du travail de diffusion en continu Hadoop hello est écrite emplacement toohello spécifiée pour cette propriété.</span><span class="sxs-lookup"><span data-stu-id="d358f-133">hello output of hello Hadoop Streaming job is written toohello location specified for this property.</span></span>
7. <span data-ttu-id="d358f-134">Bonjour **filePaths** section, spécifiez des chemins d’accès hello pour hello exécutables du Mappeur et du réducteur.</span><span class="sxs-lookup"><span data-stu-id="d358f-134">In hello **filePaths** section, specify hello paths for hello mapper and reducer executables.</span></span> <span data-ttu-id="d358f-135">Dans l’exemple de hello : « adfsample/example/apps/wc.exe », adfsample est le conteneur d’objets blob hello, exemple/apps est le dossier de hello et wc.exe est hello exécutable.</span><span class="sxs-lookup"><span data-stu-id="d358f-135">In hello example: "adfsample/example/apps/wc.exe", adfsample is hello blob container, example/apps is hello folder, and wc.exe is hello executable.</span></span>
8. <span data-ttu-id="d358f-136">Pourquoi **fileLinkedService** propriété, spécifiez hello Azure Storage service lié qui représente hello le stockage Azure qui contient les fichiers hello spécifiés dans la section de filePaths hello.</span><span class="sxs-lookup"><span data-stu-id="d358f-136">For hello **fileLinkedService** property, specify hello Azure Storage linked service that represents hello Azure storage that contains hello files specified in hello filePaths section.</span></span>
9. <span data-ttu-id="d358f-137">Pourquoi **arguments** propriété, spécifiez les arguments de hello pour hello travail de diffusion en continu.</span><span class="sxs-lookup"><span data-stu-id="d358f-137">For hello **arguments** property, specify hello arguments for hello streaming job.</span></span>
10. <span data-ttu-id="d358f-138">Hello **getDebugInfo** propriété est un élément facultatif.</span><span class="sxs-lookup"><span data-stu-id="d358f-138">hello **getDebugInfo** property is an optional element.</span></span> <span data-ttu-id="d358f-139">Lorsqu’il est défini tooFailure, les journaux de hello sont téléchargés uniquement en cas d’échec.</span><span class="sxs-lookup"><span data-stu-id="d358f-139">When it is set tooFailure, hello logs are downloaded only on failure.</span></span> <span data-ttu-id="d358f-140">Lorsqu’il est défini tooAlways, les journaux sont toujours téléchargées quel que soit l’état d’exécution hello.</span><span class="sxs-lookup"><span data-stu-id="d358f-140">When it is set tooAlways, logs are always downloaded irrespective of hello execution status.</span></span>

> [!NOTE]
> <span data-ttu-id="d358f-141">Comme indiqué dans l’exemple de hello, vous spécifiez un dataset de sortie pour une activité de Streaming Hadoop de hello pour hello **génère** propriété.</span><span class="sxs-lookup"><span data-stu-id="d358f-141">As shown in hello example, you specify an output dataset for hello Hadoop Streaming Activity for hello **outputs** property.</span></span> <span data-ttu-id="d358f-142">Ce jeu de données est uniquement un jeu de données factice qui est la planification de pipeline hello toodrive requis.</span><span class="sxs-lookup"><span data-stu-id="d358f-142">This dataset is just a dummy dataset that is required toodrive hello pipeline schedule.</span></span> <span data-ttu-id="d358f-143">Il est inutile toospecify tout jeu de données d’entrée pour l’activité hello pour hello **entrées** propriété.</span><span class="sxs-lookup"><span data-stu-id="d358f-143">You do not need toospecify any input dataset for hello activity for hello **inputs** property.</span></span>  
> 
> 

## <a name="example"></a><span data-ttu-id="d358f-144">Exemple</span><span class="sxs-lookup"><span data-stu-id="d358f-144">Example</span></span>
<span data-ttu-id="d358f-145">pipeline Hello dans cette procédure pas à pas exécute le programme de mappage/réduction diffusion en continu hello statistiques sur votre cluster Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d358f-145">hello pipeline in this walkthrough runs hello Word Count streaming Map/Reduce program on your Azure HDInsight cluster.</span></span> 

### <a name="linked-services"></a><span data-ttu-id="d358f-146">Services liés</span><span class="sxs-lookup"><span data-stu-id="d358f-146">Linked services</span></span>
#### <a name="azure-storage-linked-service"></a><span data-ttu-id="d358f-147">Service lié Azure Storage</span><span class="sxs-lookup"><span data-stu-id="d358f-147">Azure Storage linked service</span></span>
<span data-ttu-id="d358f-148">Tout d’abord, vous créez un hello toolink de service lié Azure Storage qui est utilisé par la fabrique de données Azure hello Azure HDInsight cluster toohello.</span><span class="sxs-lookup"><span data-stu-id="d358f-148">First, you create a linked service toolink hello Azure Storage that is used by hello Azure HDInsight cluster toohello Azure data factory.</span></span> <span data-ttu-id="d358f-149">Si vous copiez-collez hello suivant de code, n’oubliez pas de clé de compte et le nom de compte avec le nom de hello tooreplace et la clé de votre stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="d358f-149">If you copy/paste hello following code, do not forget tooreplace account name and account key with hello name and key of your Azure Storage.</span></span> 

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

#### <a name="azure-hdinsight-linked-service"></a><span data-ttu-id="d358f-150">Service lié Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="d358f-150">Azure HDInsight linked service</span></span>
<span data-ttu-id="d358f-151">Ensuite, créez un service lié de toolink votre fabrique de données Azure toohello cluster Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d358f-151">Next, you create a linked service toolink your Azure HDInsight cluster toohello Azure data factory.</span></span> <span data-ttu-id="d358f-152">Si vous copiez-collez hello suivant de code, remplacez le nom du cluster HDInsight avec nom hello de votre cluster HDInsight et modifier les valeurs nom et mot de passe utilisateur.</span><span class="sxs-lookup"><span data-stu-id="d358f-152">If you copy/paste hello following code, replace HDInsight cluster name with hello name of your HDInsight cluster, and change user name and password values.</span></span> 

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

### <a name="datasets"></a><span data-ttu-id="d358f-153">JEUX DE DONNÉES</span><span class="sxs-lookup"><span data-stu-id="d358f-153">Datasets</span></span>
#### <a name="output-dataset"></a><span data-ttu-id="d358f-154">Jeu de données de sortie</span><span class="sxs-lookup"><span data-stu-id="d358f-154">Output dataset</span></span>
<span data-ttu-id="d358f-155">pipeline Hello dans cet exemple ne prend pas d’entrées.</span><span class="sxs-lookup"><span data-stu-id="d358f-155">hello pipeline in this example does not take any inputs.</span></span> <span data-ttu-id="d358f-156">Vous spécifiez un dataset de sortie pour une activité de diffusion en continu HDInsight de hello.</span><span class="sxs-lookup"><span data-stu-id="d358f-156">You specify an output dataset for hello HDInsight Streaming Activity.</span></span> <span data-ttu-id="d358f-157">Ce jeu de données est uniquement un jeu de données factice qui est la planification de pipeline hello toodrive requis.</span><span class="sxs-lookup"><span data-stu-id="d358f-157">This dataset is just a dummy dataset that is required toodrive hello pipeline schedule.</span></span> 

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

### <a name="pipeline"></a><span data-ttu-id="d358f-158">Pipeline</span><span class="sxs-lookup"><span data-stu-id="d358f-158">Pipeline</span></span>
<span data-ttu-id="d358f-159">pipeline Hello dans cet exemple n'a qu’une seule activité qui est de type : **HDInsightStreaming**.</span><span class="sxs-lookup"><span data-stu-id="d358f-159">hello pipeline in this example has only one activity that is of type: **HDInsightStreaming**.</span></span> 

<span data-ttu-id="d358f-160">cluster HDInsight de Hello est automatiquement remplie avec les données (davinci.txt) et les exemples de programmes (wc.exe et cat.exe).</span><span class="sxs-lookup"><span data-stu-id="d358f-160">hello HDInsight cluster is automatically populated with example programs (wc.exe and cat.exe) and data (davinci.txt).</span></span> <span data-ttu-id="d358f-161">Par défaut, le nom du conteneur de hello est utilisé par le cluster HDInsight de hello est nom hello de cluster hello lui-même.</span><span class="sxs-lookup"><span data-stu-id="d358f-161">By default, name of hello container that is used by hello HDInsight cluster is hello name of hello cluster itself.</span></span> <span data-ttu-id="d358f-162">Par exemple, si votre nom de cluster est myhdicluster, nom du conteneur d’objets blob hello associé serait myhdicluster.</span><span class="sxs-lookup"><span data-stu-id="d358f-162">For example, if your cluster name is myhdicluster, name of hello blob container associated would be myhdicluster.</span></span>  

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
## <a name="see-also"></a><span data-ttu-id="d358f-163">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="d358f-163">See Also</span></span>
* [<span data-ttu-id="d358f-164">Activité Hive</span><span class="sxs-lookup"><span data-stu-id="d358f-164">Hive Activity</span></span>](data-factory-hive-activity.md)
* [<span data-ttu-id="d358f-165">Activité pig</span><span class="sxs-lookup"><span data-stu-id="d358f-165">Pig Activity</span></span>](data-factory-pig-activity.md)
* [<span data-ttu-id="d358f-166">Activité MapReduce</span><span class="sxs-lookup"><span data-stu-id="d358f-166">MapReduce Activity</span></span>](data-factory-map-reduce.md)
* [<span data-ttu-id="d358f-167">Appeler des programmes Spark</span><span class="sxs-lookup"><span data-stu-id="d358f-167">Invoke Spark programs</span></span>](data-factory-spark.md)
* [<span data-ttu-id="d358f-168">Appeler des scripts R</span><span class="sxs-lookup"><span data-stu-id="d358f-168">Invoke R scripts</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)

