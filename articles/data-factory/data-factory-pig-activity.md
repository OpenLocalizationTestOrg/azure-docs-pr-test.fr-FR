---
title: "Transformer des données à l’aide d’une activité Pig dans Azure Data Factory | Microsoft Docs"
description: "Découvrez comment utiliser l'activité pig d’une fabrique de données Azure pour exécuter des requêtes pig sur un cluster HDInsight à la demande/ou votre propre cluster."
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 5af07a1a-2087-455e-a67b-a79841b4ada5
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: shlo
ms.openlocfilehash: 182a637ab98955129d269e2afc3ba581aa1a7c03
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="transform-data-using-pig-activity-in-azure-data-factory"></a><span data-ttu-id="c0bbc-103">Transformer des données à l’aide d’une activité Pig dans Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="c0bbc-103">Transform data using Pig Activity in Azure Data Factory</span></span>
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="c0bbc-104">Activité Hive</span><span class="sxs-lookup"><span data-stu-id="c0bbc-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="c0bbc-105">Activité pig</span><span class="sxs-lookup"><span data-stu-id="c0bbc-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="c0bbc-106">Activité MapReduce</span><span class="sxs-lookup"><span data-stu-id="c0bbc-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="c0bbc-107">Activité de diffusion en continu Hadoop</span><span class="sxs-lookup"><span data-stu-id="c0bbc-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="c0bbc-108">Activité Spark</span><span class="sxs-lookup"><span data-stu-id="c0bbc-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="c0bbc-109">Activité d’exécution par lot Machine Learning</span><span class="sxs-lookup"><span data-stu-id="c0bbc-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="c0bbc-110">Activité des ressources de mise à jour de Machine Learning</span><span class="sxs-lookup"><span data-stu-id="c0bbc-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="c0bbc-111">Activité de procédure stockée</span><span class="sxs-lookup"><span data-stu-id="c0bbc-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="c0bbc-112">Activité U-SQL Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="c0bbc-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="c0bbc-113">Activité personnalisée .NET</span><span class="sxs-lookup"><span data-stu-id="c0bbc-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

<span data-ttu-id="c0bbc-114">L’activité Pig de HDInsight d’un [pipeline](data-factory-create-pipelines.md) Data Factory exécute des requêtes Pig sur [votre propre](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) cluster ou le cluster [à la demande](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) HDInsight sous Windows ou Linux.</span><span class="sxs-lookup"><span data-stu-id="c0bbc-114">The HDInsight Pig activity in a Data Factory [pipeline](data-factory-create-pipelines.md) executes Pig queries on [your own](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) or [on-demand](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) Windows/Linux-based HDInsight cluster.</span></span> <span data-ttu-id="c0bbc-115">Cet article s'appuie sur l'article [Activités de transformation des données](data-factory-data-transformation-activities.md) qui présente une vue d'ensemble de la transformation des données et les activités de transformation prises en charge.</span><span class="sxs-lookup"><span data-stu-id="c0bbc-115">This article builds on the [data transformation activities](data-factory-data-transformation-activities.md) article, which presents a general overview of data transformation and the supported transformation activities.</span></span>

> [!NOTE] 
> <span data-ttu-id="c0bbc-116">Si vous découvrez Azure Data Factory, lisez la [Présentation d’Azure Data Factory](data-factory-introduction.md) et suivez le didacticiel : [Générer votre premier pipeline de données](data-factory-build-your-first-pipeline.md) avant de lire cet article.</span><span class="sxs-lookup"><span data-stu-id="c0bbc-116">If you are new to Azure Data Factory, read through [Introduction to Azure Data Factory](data-factory-introduction.md) and do the tutorial: [Build your first data pipeline](data-factory-build-your-first-pipeline.md) before reading this article.</span></span> 

## <a name="syntax"></a><span data-ttu-id="c0bbc-117">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="c0bbc-117">Syntax</span></span>

```JSON
{
    "name": "HiveActivitySamplePipeline",
      "properties": {
    "activities": [
        {
            "name": "Pig Activity",
            "description": "description",
            "type": "HDInsightPig",
            "inputs": [
                  {
                    "name": "input tables"
                  }
            ],
            "outputs": [
                  {
                    "name": "output tables"
                  }
            ],
            "linkedServiceName": "MyHDInsightLinkedService",
            "typeProperties": {
                  "script": "Pig script",
                  "scriptPath": "<pathtothePigscriptfileinAzureblobstorage>",
                  "defines": {
                    "param1": "param1Value"
                  }
            },
               "scheduler": {
                  "frequency": "Day",
                  "interval": 1
            }
          }
    ]
  }
}
```
## <a name="syntax-details"></a><span data-ttu-id="c0bbc-118">Détails de la syntaxe</span><span class="sxs-lookup"><span data-stu-id="c0bbc-118">Syntax details</span></span>
| <span data-ttu-id="c0bbc-119">Propriété</span><span class="sxs-lookup"><span data-stu-id="c0bbc-119">Property</span></span> | <span data-ttu-id="c0bbc-120">Description</span><span class="sxs-lookup"><span data-stu-id="c0bbc-120">Description</span></span> | <span data-ttu-id="c0bbc-121">Requis</span><span class="sxs-lookup"><span data-stu-id="c0bbc-121">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c0bbc-122">name</span><span class="sxs-lookup"><span data-stu-id="c0bbc-122">name</span></span> |<span data-ttu-id="c0bbc-123">Nom de l’activité</span><span class="sxs-lookup"><span data-stu-id="c0bbc-123">Name of the activity</span></span> |<span data-ttu-id="c0bbc-124">Oui</span><span class="sxs-lookup"><span data-stu-id="c0bbc-124">Yes</span></span> |
| <span data-ttu-id="c0bbc-125">Description</span><span class="sxs-lookup"><span data-stu-id="c0bbc-125">description</span></span> |<span data-ttu-id="c0bbc-126">Texte décrivant la raison motivant l’activité.</span><span class="sxs-lookup"><span data-stu-id="c0bbc-126">Text describing what the activity is used for</span></span> |<span data-ttu-id="c0bbc-127">Non</span><span class="sxs-lookup"><span data-stu-id="c0bbc-127">No</span></span> |
| <span data-ttu-id="c0bbc-128">type</span><span class="sxs-lookup"><span data-stu-id="c0bbc-128">type</span></span> |<span data-ttu-id="c0bbc-129">HDinsightPig</span><span class="sxs-lookup"><span data-stu-id="c0bbc-129">HDinsightPig</span></span> |<span data-ttu-id="c0bbc-130">Oui</span><span class="sxs-lookup"><span data-stu-id="c0bbc-130">Yes</span></span> |
| <span data-ttu-id="c0bbc-131">inputs</span><span class="sxs-lookup"><span data-stu-id="c0bbc-131">inputs</span></span> |<span data-ttu-id="c0bbc-132">Une ou plusieurs entrées utilisées par l'activité pig</span><span class="sxs-lookup"><span data-stu-id="c0bbc-132">One or more inputs consumed by the Pig activity</span></span> |<span data-ttu-id="c0bbc-133">Non</span><span class="sxs-lookup"><span data-stu-id="c0bbc-133">No</span></span> |
| <span data-ttu-id="c0bbc-134">outputs</span><span class="sxs-lookup"><span data-stu-id="c0bbc-134">outputs</span></span> |<span data-ttu-id="c0bbc-135">Une ou plusieurs sorties produites par l’activité pig</span><span class="sxs-lookup"><span data-stu-id="c0bbc-135">One or more outputs produced by the Pig activity</span></span> |<span data-ttu-id="c0bbc-136">Oui</span><span class="sxs-lookup"><span data-stu-id="c0bbc-136">Yes</span></span> |
| <span data-ttu-id="c0bbc-137">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="c0bbc-137">linkedServiceName</span></span> |<span data-ttu-id="c0bbc-138">Référence au cluster HDInsight enregistré comme un service lié dans Data Factory</span><span class="sxs-lookup"><span data-stu-id="c0bbc-138">Reference to the HDInsight cluster registered as a linked service in Data Factory</span></span> |<span data-ttu-id="c0bbc-139">Oui</span><span class="sxs-lookup"><span data-stu-id="c0bbc-139">Yes</span></span> |
| <span data-ttu-id="c0bbc-140">script</span><span class="sxs-lookup"><span data-stu-id="c0bbc-140">script</span></span> |<span data-ttu-id="c0bbc-141">Spécifier le script en ligne pig</span><span class="sxs-lookup"><span data-stu-id="c0bbc-141">Specify the Pig script inline</span></span> |<span data-ttu-id="c0bbc-142">Non</span><span class="sxs-lookup"><span data-stu-id="c0bbc-142">No</span></span> |
| <span data-ttu-id="c0bbc-143">chemin d'accès du script</span><span class="sxs-lookup"><span data-stu-id="c0bbc-143">script path</span></span> |<span data-ttu-id="c0bbc-144">Stockez le script pig dans un stockage d'objets blob Azure et indiquez le chemin d'accès au fichier.</span><span class="sxs-lookup"><span data-stu-id="c0bbc-144">Store the Pig script in an Azure blob storage and provide the path to the file.</span></span> <span data-ttu-id="c0bbc-145">Utilisez la propriété ’script’ ou ’scriptPath’.</span><span class="sxs-lookup"><span data-stu-id="c0bbc-145">Use 'script' or 'scriptPath' property.</span></span> <span data-ttu-id="c0bbc-146">Les deux propriétés ne peuvent pas être utilisées simultanément.</span><span class="sxs-lookup"><span data-stu-id="c0bbc-146">Both cannot be used together.</span></span> <span data-ttu-id="c0bbc-147">Le nom de fichier respecte la casse.</span><span class="sxs-lookup"><span data-stu-id="c0bbc-147">The file name is case-sensitive.</span></span> |<span data-ttu-id="c0bbc-148">Non</span><span class="sxs-lookup"><span data-stu-id="c0bbc-148">No</span></span> |
| <span data-ttu-id="c0bbc-149">defines</span><span class="sxs-lookup"><span data-stu-id="c0bbc-149">defines</span></span> |<span data-ttu-id="c0bbc-150">Spécifier les paramètres sous forme de paires clé/valeur pour le référencement au sein du script pig</span><span class="sxs-lookup"><span data-stu-id="c0bbc-150">Specify parameters as key/value pairs for referencing within the Pig script</span></span> |<span data-ttu-id="c0bbc-151">Non</span><span class="sxs-lookup"><span data-stu-id="c0bbc-151">No</span></span> |

## <a name="example"></a><span data-ttu-id="c0bbc-152">Exemple</span><span class="sxs-lookup"><span data-stu-id="c0bbc-152">Example</span></span>
<span data-ttu-id="c0bbc-153">Prenons un exemple d'analyse de journaux de jeux où vous souhaitez identifier le temps passé par les joueurs à jouer à des jeux créés par votre entreprise.</span><span class="sxs-lookup"><span data-stu-id="c0bbc-153">Let’s consider an example of game logs analytics where you want to identify the time spent by players playing games launched by your company.</span></span>

<span data-ttu-id="c0bbc-154">L’exemple de journal de jeu suivant est un fichier séparé par des virgules (,).</span><span class="sxs-lookup"><span data-stu-id="c0bbc-154">The following sample game log is a comma (,) separated file.</span></span> <span data-ttu-id="c0bbc-155">Il contient les champs suivants : ProfileID, SessionStart, Duration, SrcIPAddress et GameType.</span><span class="sxs-lookup"><span data-stu-id="c0bbc-155">It contains the following fields – ProfileID, SessionStart, Duration, SrcIPAddress, and GameType.</span></span>

```
1809,2014-05-04 12:04:25.3470000,14,221.117.223.75,CaptureFlag
1703,2014-05-04 06:05:06.0090000,16,12.49.178.247,KingHill
1703,2014-05-04 10:21:57.3290000,10,199.118.18.179,CaptureFlag
1809,2014-05-04 05:24:22.2100000,23,192.84.66.141,KingHill
.....
```

<span data-ttu-id="c0bbc-156">Le **script pig** pour traiter ces données :</span><span class="sxs-lookup"><span data-stu-id="c0bbc-156">The **Pig script** to process this data:</span></span>

```
PigSampleIn = LOAD 'wasb://adfwalkthrough@anandsub14.blob.core.windows.net/samplein/' USING PigStorage(',') AS (ProfileID:chararray, SessionStart:chararray, Duration:int, SrcIPAddress:chararray, GameType:chararray);

GroupProfile = Group PigSampleIn all;

PigSampleOut = Foreach GroupProfile Generate PigSampleIn.ProfileID, SUM(PigSampleIn.Duration);

Store PigSampleOut into 'wasb://adfwalkthrough@anandsub14.blob.core.windows.net/sampleoutpig/' USING PigStorage (',');
```

<span data-ttu-id="c0bbc-157">Pour exécuter ce script pig dans un pipeline Data Factory, appliquez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="c0bbc-157">To execute this Pig script in a Data Factory pipeline, do the following steps:</span></span>

1. <span data-ttu-id="c0bbc-158">Créez un service lié pour inscrire [votre propre cluster de calcul HDInsight](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) ou configurer un [cluster de calcul HDInsight à la demande](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).</span><span class="sxs-lookup"><span data-stu-id="c0bbc-158">Create a linked service to register [your own HDInsight compute cluster](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) or configure [on-demand HDInsight compute cluster](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).</span></span> <span data-ttu-id="c0bbc-159">Appelons ce service lié **HDInsightLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="c0bbc-159">Let’s call this linked service **HDInsightLinkedService**.</span></span>
2. <span data-ttu-id="c0bbc-160">Créez un [service lié](data-factory-azure-blob-connector.md) pour configurer la connexion au stockage d'objets blob Azure qui héberge les données.</span><span class="sxs-lookup"><span data-stu-id="c0bbc-160">Create a [linked service](data-factory-azure-blob-connector.md) to configure the connection to Azure Blob storage hosting the data.</span></span> <span data-ttu-id="c0bbc-161">Appelons ce service lié **StorageLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="c0bbc-161">Let’s call this linked service **StorageLinkedService**.</span></span>
3. <span data-ttu-id="c0bbc-162">Créez des [jeux de données](data-factory-create-datasets.md) pointant vers les données d'entrée et de sortie.</span><span class="sxs-lookup"><span data-stu-id="c0bbc-162">Create [datasets](data-factory-create-datasets.md) pointing to the input and the output data.</span></span> <span data-ttu-id="c0bbc-163">Appelons le jeu de données d’entrée **PigSampleIn** et le jeu de données de sortie **PigSampleOut**.</span><span class="sxs-lookup"><span data-stu-id="c0bbc-163">Let’s call the input dataset **PigSampleIn** and the output dataset **PigSampleOut**.</span></span>
4. <span data-ttu-id="c0bbc-164">Copiez la requête Pig dans le fichier configuré par le stockage d’objets Blob Azure à l’étape #2.</span><span class="sxs-lookup"><span data-stu-id="c0bbc-164">Copy the Pig query in a file the Azure Blob Storage configured in step #2.</span></span> <span data-ttu-id="c0bbc-165">Si le stockage Azure qui héberge les données est différent de celui qui héberge le fichier de requête, créez un service de stockage Azure lié distinct.</span><span class="sxs-lookup"><span data-stu-id="c0bbc-165">If the Azure storage that hosts the data is different from the one that hosts the query file, create a separate Azure Storage linked service.</span></span> <span data-ttu-id="c0bbc-166">Consultez le service lié dans la configuration de l’activité.</span><span class="sxs-lookup"><span data-stu-id="c0bbc-166">Refer to the linked service in the activity configuration.</span></span> <span data-ttu-id="c0bbc-167">Utilisez **scriptPath ** pour spécifier le chemin d’accès au fichier de script pig et **scriptLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="c0bbc-167">Use **scriptPath **to specify the path to pig script file and **scriptLinkedService**.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="c0bbc-168">Vous pouvez également fournir le script en ligne pig dans la définition d’activité à l’aide de la propriété **script** .</span><span class="sxs-lookup"><span data-stu-id="c0bbc-168">You can also provide the Pig script inline in the activity definition by using the **script** property.</span></span> <span data-ttu-id="c0bbc-169">Cependant, cela n’est pas recommandé car tous les caractères spéciaux du script au sein du document JSON doivent être placés dans une séquence d’échappement, ce qui risque d’entraîner des problèmes de débogage.</span><span class="sxs-lookup"><span data-stu-id="c0bbc-169">However, we do not recommend this approach as all special characters in the script needs to be escaped and may cause debugging issues.</span></span> <span data-ttu-id="c0bbc-170">La meilleure pratique consiste à suivre l’étape 4.</span><span class="sxs-lookup"><span data-stu-id="c0bbc-170">The best practice is to follow step #4.</span></span>
   > 
   > 
5. <span data-ttu-id="c0bbc-171">Créez le pipeline avec l'activité HDInsightPig.</span><span class="sxs-lookup"><span data-stu-id="c0bbc-171">Create the pipeline with the HDInsightPig activity.</span></span> <span data-ttu-id="c0bbc-172">Cette activité traite les données d’entrée en exécutant le script Pig sur un cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c0bbc-172">This activity processes the input data by running Pig script on HDInsight cluster.</span></span>

    ```JSON   
    {
      "name": "PigActivitySamplePipeline",
      "properties": {
        "activities": [
          {
            "name": "PigActivitySample",
            "type": "HDInsightPig",
            "inputs": [
              {
                "name": "PigSampleIn"
              }
            ],
            "outputs": [
              {
                "name": "PigSampleOut"
              }
            ],
            "linkedServiceName": "HDInsightLinkedService",
            "typeproperties": {
              "scriptPath": "adfwalkthrough\\scripts\\enrichlogs.pig",
              "scriptLinkedService": "StorageLinkedService"
            },
               "scheduler": {
                  "frequency": "Day",
                  "interval": 1
            }
          }
        ]
      }
    } 
    ```
6. <span data-ttu-id="c0bbc-173">Déployez le pipeline.</span><span class="sxs-lookup"><span data-stu-id="c0bbc-173">Deploy the pipeline.</span></span> <span data-ttu-id="c0bbc-174">Consultez l’article [Création de pipelines](data-factory-create-pipelines.md) pour plus de détails.</span><span class="sxs-lookup"><span data-stu-id="c0bbc-174">See [Creating pipelines](data-factory-create-pipelines.md) article for details.</span></span> 
7. <span data-ttu-id="c0bbc-175">Surveillez le pipeline à l'aide des vues de gestion et de surveillance Data Factory.</span><span class="sxs-lookup"><span data-stu-id="c0bbc-175">Monitor the pipeline using the data factory monitoring and management views.</span></span> <span data-ttu-id="c0bbc-176">Consultez l’article [Surveillance et gestion des pipelines Data Factory](data-factory-monitor-manage-pipelines.md) pour plus d'informations.</span><span class="sxs-lookup"><span data-stu-id="c0bbc-176">See [Monitoring and manage Data Factory pipelines](data-factory-monitor-manage-pipelines.md) article for details.</span></span>

## <a name="specifying-parameters-for-a-pig-script"></a><span data-ttu-id="c0bbc-177">Spécification des paramètres d’un script Pig</span><span class="sxs-lookup"><span data-stu-id="c0bbc-177">Specifying parameters for a Pig script</span></span>
<span data-ttu-id="c0bbc-178">Prenons l'exemple suivant : des journaux de jeux sont reçus quotidiennement dans le stockage blob Azure et conservés dans un dossier partitionné selon la date et l’heure.</span><span class="sxs-lookup"><span data-stu-id="c0bbc-178">Consider the following example: game logs are ingested daily into Azure Blob Storage and stored in a folder partitioned based on date and time.</span></span> <span data-ttu-id="c0bbc-179">Vous souhaitez paramétrer le script pig et fournir dynamiquement l'emplacement du dossier d'entrée pendant l'exécution mais aussi produire la sortie partitionnée par date et par heure.</span><span class="sxs-lookup"><span data-stu-id="c0bbc-179">You want to parameterize the Pig script and pass the input folder location dynamically during runtime and also produce the output partitioned with date and time.</span></span>

<span data-ttu-id="c0bbc-180">Pour utiliser le script pig paramétré, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="c0bbc-180">To use parameterized Pig script, do the following:</span></span>

* <span data-ttu-id="c0bbc-181">Définissez les paramètres dans **defines**.</span><span class="sxs-lookup"><span data-stu-id="c0bbc-181">Define the parameters in **defines**.</span></span>

    ```JSON  
    {
        "name": "PigActivitySamplePipeline",
          "properties": {
        "activities": [
            {
                "name": "PigActivitySample",
                "type": "HDInsightPig",
                "inputs": [
                      {
                        "name": "PigSampleIn"
                      }
                ],
                "outputs": [
                      {
                        "name": "PigSampleOut"
                      }
                ],
                "linkedServiceName": "HDInsightLinkedService",
                "typeproperties": {
                      "scriptPath": "adfwalkthrough\\scripts\\samplepig.hql",
                      "scriptLinkedService": "StorageLinkedService",
                      "defines": {
                        "Input": "$$Text.Format('wasb: //adfwalkthrough@<storageaccountname>.blob.core.windows.net/samplein/yearno={0: yyyy}/monthno={0:MM}/dayno={0: dd}/',SliceStart)",
                        "Output": "$$Text.Format('wasb://adfwalkthrough@<storageaccountname>.blob.core.windows.net/sampleout/yearno={0:yyyy}/monthno={0:MM}/dayno={0:dd}/', SliceStart)"
                      }
                },
                   "scheduler": {
                      "frequency": "Day",
                      "interval": 1
                }
              }
        ]
      }
    }
    ```  
* <span data-ttu-id="c0bbc-182">Dans le script pig, reportez-vous aux paramètres à l'aide de ’**$parameterName**’ comme indiqué dans l'exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="c0bbc-182">In the Pig Script, refer to the parameters using '**$parameterName**' as shown in the following example:</span></span>

    ```  
    PigSampleIn = LOAD '$Input' USING PigStorage(',') AS (ProfileID:chararray, SessionStart:chararray, Duration:int, SrcIPAddress:chararray, GameType:chararray);    
    GroupProfile = Group PigSampleIn all;        
    PigSampleOut = Foreach GroupProfile Generate PigSampleIn.ProfileID, SUM(PigSampleIn.Duration);        
    Store PigSampleOut into '$Output' USING PigStorage (','); 
    ```
## <a name="see-also"></a><span data-ttu-id="c0bbc-183">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="c0bbc-183">See Also</span></span>
* [<span data-ttu-id="c0bbc-184">Activité Hive</span><span class="sxs-lookup"><span data-stu-id="c0bbc-184">Hive Activity</span></span>](data-factory-hive-activity.md)
* [<span data-ttu-id="c0bbc-185">Activité MapReduce</span><span class="sxs-lookup"><span data-stu-id="c0bbc-185">MapReduce Activity</span></span>](data-factory-map-reduce.md)
* [<span data-ttu-id="c0bbc-186">Activité de diffusion en continu Hadoop</span><span class="sxs-lookup"><span data-stu-id="c0bbc-186">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
* [<span data-ttu-id="c0bbc-187">Appeler des programmes Spark</span><span class="sxs-lookup"><span data-stu-id="c0bbc-187">Invoke Spark programs</span></span>](data-factory-spark.md)
* [<span data-ttu-id="c0bbc-188">Appeler des scripts R</span><span class="sxs-lookup"><span data-stu-id="c0bbc-188">Invoke R scripts</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)

