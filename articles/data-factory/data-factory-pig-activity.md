---
title: "les données d’aaaTransform à l’aide d’activité Pig dans Azure Data Factory | Documents Microsoft"
description: "Découvrez comment vous pouvez utiliser hello activité Pig dans un script de données Azure fabrique toorun Pig sur un cluster de HDInsight sur la demande/votre propre."
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
ms.openlocfilehash: 3ad096c4a9e8603b09f574f6d129b4339a75d381
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="transform-data-using-pig-activity-in-azure-data-factory"></a><span data-ttu-id="f9acc-103">Transformer des données à l’aide d’une activité Pig dans Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="f9acc-103">Transform data using Pig Activity in Azure Data Factory</span></span>
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="f9acc-104">Activité Hive</span><span class="sxs-lookup"><span data-stu-id="f9acc-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="f9acc-105">Activité pig</span><span class="sxs-lookup"><span data-stu-id="f9acc-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="f9acc-106">Activité MapReduce</span><span class="sxs-lookup"><span data-stu-id="f9acc-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="f9acc-107">Activité de diffusion en continu Hadoop</span><span class="sxs-lookup"><span data-stu-id="f9acc-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="f9acc-108">Activité Spark</span><span class="sxs-lookup"><span data-stu-id="f9acc-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="f9acc-109">Activité d’exécution par lot Machine Learning</span><span class="sxs-lookup"><span data-stu-id="f9acc-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="f9acc-110">Activité des ressources de mise à jour de Machine Learning</span><span class="sxs-lookup"><span data-stu-id="f9acc-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="f9acc-111">Activité de procédure stockée</span><span class="sxs-lookup"><span data-stu-id="f9acc-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="f9acc-112">Activité U-SQL Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="f9acc-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="f9acc-113">Activité personnalisée .NET</span><span class="sxs-lookup"><span data-stu-id="f9acc-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

<span data-ttu-id="f9acc-114">Hello activité HDInsight Pig dans une fabrique de données [pipeline](data-factory-create-pipelines.md) exécute des requêtes de Pig sur [votre propre](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) ou [à la demande](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) cluster HDInsight de basés sur Windows/Linux.</span><span class="sxs-lookup"><span data-stu-id="f9acc-114">hello HDInsight Pig activity in a Data Factory [pipeline](data-factory-create-pipelines.md) executes Pig queries on [your own](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) or [on-demand](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) Windows/Linux-based HDInsight cluster.</span></span> <span data-ttu-id="f9acc-115">Cet article s’appuie sur hello [activités de transformation des données](data-factory-data-transformation-activities.md) article, qui présente une vue d’ensemble de la transformation des données et des activités de transformation hello pris en charge.</span><span class="sxs-lookup"><span data-stu-id="f9acc-115">This article builds on hello [data transformation activities](data-factory-data-transformation-activities.md) article, which presents a general overview of data transformation and hello supported transformation activities.</span></span>

> [!NOTE] 
> <span data-ttu-id="f9acc-116">Si vous êtes tooAzure nouvelle fabrique de données, lisez [Introduction tooAzure Data Factory](data-factory-introduction.md) et hello didacticiel : [générer votre première pipeline de données](data-factory-build-your-first-pipeline.md) avant de lire cet article.</span><span class="sxs-lookup"><span data-stu-id="f9acc-116">If you are new tooAzure Data Factory, read through [Introduction tooAzure Data Factory](data-factory-introduction.md) and do hello tutorial: [Build your first data pipeline](data-factory-build-your-first-pipeline.md) before reading this article.</span></span> 

## <a name="syntax"></a><span data-ttu-id="f9acc-117">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="f9acc-117">Syntax</span></span>

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
## <a name="syntax-details"></a><span data-ttu-id="f9acc-118">Détails de la syntaxe</span><span class="sxs-lookup"><span data-stu-id="f9acc-118">Syntax details</span></span>
| <span data-ttu-id="f9acc-119">Propriété</span><span class="sxs-lookup"><span data-stu-id="f9acc-119">Property</span></span> | <span data-ttu-id="f9acc-120">Description</span><span class="sxs-lookup"><span data-stu-id="f9acc-120">Description</span></span> | <span data-ttu-id="f9acc-121">Requis</span><span class="sxs-lookup"><span data-stu-id="f9acc-121">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f9acc-122">name</span><span class="sxs-lookup"><span data-stu-id="f9acc-122">name</span></span> |<span data-ttu-id="f9acc-123">Nom de l’activité hello</span><span class="sxs-lookup"><span data-stu-id="f9acc-123">Name of hello activity</span></span> |<span data-ttu-id="f9acc-124">Oui</span><span class="sxs-lookup"><span data-stu-id="f9acc-124">Yes</span></span> |
| <span data-ttu-id="f9acc-125">description</span><span class="sxs-lookup"><span data-stu-id="f9acc-125">description</span></span> |<span data-ttu-id="f9acc-126">Texte qui décrit quelle activité hello est utilisé pour</span><span class="sxs-lookup"><span data-stu-id="f9acc-126">Text describing what hello activity is used for</span></span> |<span data-ttu-id="f9acc-127">Non</span><span class="sxs-lookup"><span data-stu-id="f9acc-127">No</span></span> |
| <span data-ttu-id="f9acc-128">type</span><span class="sxs-lookup"><span data-stu-id="f9acc-128">type</span></span> |<span data-ttu-id="f9acc-129">HDinsightPig</span><span class="sxs-lookup"><span data-stu-id="f9acc-129">HDinsightPig</span></span> |<span data-ttu-id="f9acc-130">Oui</span><span class="sxs-lookup"><span data-stu-id="f9acc-130">Yes</span></span> |
| <span data-ttu-id="f9acc-131">inputs</span><span class="sxs-lookup"><span data-stu-id="f9acc-131">inputs</span></span> |<span data-ttu-id="f9acc-132">Une ou plusieurs entrées consommée par hello activité Pig</span><span class="sxs-lookup"><span data-stu-id="f9acc-132">One or more inputs consumed by hello Pig activity</span></span> |<span data-ttu-id="f9acc-133">Non</span><span class="sxs-lookup"><span data-stu-id="f9acc-133">No</span></span> |
| <span data-ttu-id="f9acc-134">outputs</span><span class="sxs-lookup"><span data-stu-id="f9acc-134">outputs</span></span> |<span data-ttu-id="f9acc-135">Une ou plusieurs sorties produites par hello activité Pig</span><span class="sxs-lookup"><span data-stu-id="f9acc-135">One or more outputs produced by hello Pig activity</span></span> |<span data-ttu-id="f9acc-136">Oui</span><span class="sxs-lookup"><span data-stu-id="f9acc-136">Yes</span></span> |
| <span data-ttu-id="f9acc-137">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="f9acc-137">linkedServiceName</span></span> |<span data-ttu-id="f9acc-138">Cluster HDInsight de référence toohello enregistré comme un service lié dans la fabrique de données</span><span class="sxs-lookup"><span data-stu-id="f9acc-138">Reference toohello HDInsight cluster registered as a linked service in Data Factory</span></span> |<span data-ttu-id="f9acc-139">Oui</span><span class="sxs-lookup"><span data-stu-id="f9acc-139">Yes</span></span> |
| <span data-ttu-id="f9acc-140">script</span><span class="sxs-lookup"><span data-stu-id="f9acc-140">script</span></span> |<span data-ttu-id="f9acc-141">Spécifiez hello Pig script inline</span><span class="sxs-lookup"><span data-stu-id="f9acc-141">Specify hello Pig script inline</span></span> |<span data-ttu-id="f9acc-142">Non</span><span class="sxs-lookup"><span data-stu-id="f9acc-142">No</span></span> |
| <span data-ttu-id="f9acc-143">chemin d'accès du script</span><span class="sxs-lookup"><span data-stu-id="f9acc-143">script path</span></span> |<span data-ttu-id="f9acc-144">Stocker le script Pig hello dans un stockage d’objets blob Azure et fournir hello chemin d’accès toohello fichier.</span><span class="sxs-lookup"><span data-stu-id="f9acc-144">Store hello Pig script in an Azure blob storage and provide hello path toohello file.</span></span> <span data-ttu-id="f9acc-145">Utilisez la propriété ’script’ ou ’scriptPath’.</span><span class="sxs-lookup"><span data-stu-id="f9acc-145">Use 'script' or 'scriptPath' property.</span></span> <span data-ttu-id="f9acc-146">Les deux propriétés ne peuvent pas être utilisées simultanément.</span><span class="sxs-lookup"><span data-stu-id="f9acc-146">Both cannot be used together.</span></span> <span data-ttu-id="f9acc-147">nom de fichier Hello respecte la casse.</span><span class="sxs-lookup"><span data-stu-id="f9acc-147">hello file name is case-sensitive.</span></span> |<span data-ttu-id="f9acc-148">Non</span><span class="sxs-lookup"><span data-stu-id="f9acc-148">No</span></span> |
| <span data-ttu-id="f9acc-149">defines</span><span class="sxs-lookup"><span data-stu-id="f9acc-149">defines</span></span> |<span data-ttu-id="f9acc-150">Spécifiez les paramètres en tant que paires clé/valeur pour le référencement dans hello script Pig</span><span class="sxs-lookup"><span data-stu-id="f9acc-150">Specify parameters as key/value pairs for referencing within hello Pig script</span></span> |<span data-ttu-id="f9acc-151">Non</span><span class="sxs-lookup"><span data-stu-id="f9acc-151">No</span></span> |

## <a name="example"></a><span data-ttu-id="f9acc-152">Exemple</span><span class="sxs-lookup"><span data-stu-id="f9acc-152">Example</span></span>
<span data-ttu-id="f9acc-153">Prenons l’exemple d’un exemple de jeu consigne analytique où vous souhaitez tooidentify hello temps de lecteurs jeux lancée par votre entreprise.</span><span class="sxs-lookup"><span data-stu-id="f9acc-153">Let’s consider an example of game logs analytics where you want tooidentify hello time spent by players playing games launched by your company.</span></span>

<span data-ttu-id="f9acc-154">Hello suivant l’exemple de journal jeu est un fichier de séparés par des virgules (,).</span><span class="sxs-lookup"><span data-stu-id="f9acc-154">hello following sample game log is a comma (,) separated file.</span></span> <span data-ttu-id="f9acc-155">Il contient hello suivant champs – ID de profil, SessionStart, durée, SrcIPAddress et type de partie.</span><span class="sxs-lookup"><span data-stu-id="f9acc-155">It contains hello following fields – ProfileID, SessionStart, Duration, SrcIPAddress, and GameType.</span></span>

```
1809,2014-05-04 12:04:25.3470000,14,221.117.223.75,CaptureFlag
1703,2014-05-04 06:05:06.0090000,16,12.49.178.247,KingHill
1703,2014-05-04 10:21:57.3290000,10,199.118.18.179,CaptureFlag
1809,2014-05-04 05:24:22.2100000,23,192.84.66.141,KingHill
.....
```

<span data-ttu-id="f9acc-156">Hello **porc script** tooprocess ces données :</span><span class="sxs-lookup"><span data-stu-id="f9acc-156">hello **Pig script** tooprocess this data:</span></span>

```
PigSampleIn = LOAD 'wasb://adfwalkthrough@anandsub14.blob.core.windows.net/samplein/' USING PigStorage(',') AS (ProfileID:chararray, SessionStart:chararray, Duration:int, SrcIPAddress:chararray, GameType:chararray);

GroupProfile = Group PigSampleIn all;

PigSampleOut = Foreach GroupProfile Generate PigSampleIn.ProfileID, SUM(PigSampleIn.Duration);

Store PigSampleOut into 'wasb://adfwalkthrough@anandsub14.blob.core.windows.net/sampleoutpig/' USING PigStorage (',');
```

<span data-ttu-id="f9acc-157">tooexecute cette Pig de script dans un pipeline de la fabrique de données, procédez comme hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="f9acc-157">tooexecute this Pig script in a Data Factory pipeline, do hello following steps:</span></span>

1. <span data-ttu-id="f9acc-158">Créer un service lié de tooregister [cluster de calcul de votre propre HDInsight](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) ou configurer [cluster de calcul à la demande HDInsight](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).</span><span class="sxs-lookup"><span data-stu-id="f9acc-158">Create a linked service tooregister [your own HDInsight compute cluster](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) or configure [on-demand HDInsight compute cluster](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).</span></span> <span data-ttu-id="f9acc-159">Appelons ce service lié **HDInsightLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="f9acc-159">Let’s call this linked service **HDInsightLinkedService**.</span></span>
2. <span data-ttu-id="f9acc-160">Créer un [service lié](data-factory-azure-blob-connector.md) tooconfigure hello connexion tooAzure stockage d’objets Blob qui héberge les données de salutation.</span><span class="sxs-lookup"><span data-stu-id="f9acc-160">Create a [linked service](data-factory-azure-blob-connector.md) tooconfigure hello connection tooAzure Blob storage hosting hello data.</span></span> <span data-ttu-id="f9acc-161">Appelons ce service lié **StorageLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="f9acc-161">Let’s call this linked service **StorageLinkedService**.</span></span>
3. <span data-ttu-id="f9acc-162">Créer [datasets](data-factory-create-datasets.md) pointant vers l’entrée de toohello et hello les données de sortie.</span><span class="sxs-lookup"><span data-stu-id="f9acc-162">Create [datasets](data-factory-create-datasets.md) pointing toohello input and hello output data.</span></span> <span data-ttu-id="f9acc-163">Jeu de données d’entrée hello, nous allons appeler **PigSampleIn** et hello dataset de sortie **PigSampleOut**.</span><span class="sxs-lookup"><span data-stu-id="f9acc-163">Let’s call hello input dataset **PigSampleIn** and hello output dataset **PigSampleOut**.</span></span>
4. <span data-ttu-id="f9acc-164">Copier requête Pig de hello dans un stockage d’objets Blob Azure configuré à l’étape 2 de # de hello fichier.</span><span class="sxs-lookup"><span data-stu-id="f9acc-164">Copy hello Pig query in a file hello Azure Blob Storage configured in step #2.</span></span> <span data-ttu-id="f9acc-165">Si hello le stockage Azure qui héberge les données de salutation est différent de hello une qui héberge un fichier de requête hello, créez un service lié Azure Storage distinct.</span><span class="sxs-lookup"><span data-stu-id="f9acc-165">If hello Azure storage that hosts hello data is different from hello one that hosts hello query file, create a separate Azure Storage linked service.</span></span> <span data-ttu-id="f9acc-166">Voir la rubrique service toohello lié dans la configuration d’activité hello.</span><span class="sxs-lookup"><span data-stu-id="f9acc-166">Refer toohello linked service in hello activity configuration.</span></span> <span data-ttu-id="f9acc-167">Utilisez ** scriptPath ** le fichier script toopig toospecify hello chemin d’accès et **scriptLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="f9acc-167">Use **scriptPath **toospecify hello path toopig script file and **scriptLinkedService**.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="f9acc-168">Vous pouvez également fournir hello Pig script inline dans la définition d’activité hello à l’aide de hello **script** propriété.</span><span class="sxs-lookup"><span data-stu-id="f9acc-168">You can also provide hello Pig script inline in hello activity definition by using hello **script** property.</span></span> <span data-ttu-id="f9acc-169">Toutefois, nous déconseillons cette approche en tant que tous les caractères spéciaux dans le script de hello doit toobe séquence d’échappement et peut provoquer des problèmes de débogage.</span><span class="sxs-lookup"><span data-stu-id="f9acc-169">However, we do not recommend this approach as all special characters in hello script needs toobe escaped and may cause debugging issues.</span></span> <span data-ttu-id="f9acc-170">Il est recommandé de Hello est toofollow étape #4.</span><span class="sxs-lookup"><span data-stu-id="f9acc-170">hello best practice is toofollow step #4.</span></span>
   > 
   > 
5. <span data-ttu-id="f9acc-171">Créer le pipeline de hello avec hello HDInsightPig activité.</span><span class="sxs-lookup"><span data-stu-id="f9acc-171">Create hello pipeline with hello HDInsightPig activity.</span></span> <span data-ttu-id="f9acc-172">Cette activité traite les données d’entrée hello en exécutant le script Pig sur un cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f9acc-172">This activity processes hello input data by running Pig script on HDInsight cluster.</span></span>

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
6. <span data-ttu-id="f9acc-173">Déploiement du pipeline de hello.</span><span class="sxs-lookup"><span data-stu-id="f9acc-173">Deploy hello pipeline.</span></span> <span data-ttu-id="f9acc-174">Consultez l’article [Création de pipelines](data-factory-create-pipelines.md) pour plus de détails.</span><span class="sxs-lookup"><span data-stu-id="f9acc-174">See [Creating pipelines](data-factory-create-pipelines.md) article for details.</span></span> 
7. <span data-ttu-id="f9acc-175">Surveiller le pipeline hello à l’aide de la surveillance de fabrique de données hello et vues de gestion.</span><span class="sxs-lookup"><span data-stu-id="f9acc-175">Monitor hello pipeline using hello data factory monitoring and management views.</span></span> <span data-ttu-id="f9acc-176">Consultez l’article [Surveillance et gestion des pipelines Data Factory](data-factory-monitor-manage-pipelines.md) pour plus d'informations.</span><span class="sxs-lookup"><span data-stu-id="f9acc-176">See [Monitoring and manage Data Factory pipelines](data-factory-monitor-manage-pipelines.md) article for details.</span></span>

## <a name="specifying-parameters-for-a-pig-script"></a><span data-ttu-id="f9acc-177">Spécification des paramètres d’un script Pig</span><span class="sxs-lookup"><span data-stu-id="f9acc-177">Specifying parameters for a Pig script</span></span>
<span data-ttu-id="f9acc-178">Envisagez de hello l’exemple suivant : journaux de jeu sont ingérés tous les jours dans le stockage d’objets Blob Azure et stockés dans un dossier date selon partitionnée et l’heure.</span><span class="sxs-lookup"><span data-stu-id="f9acc-178">Consider hello following example: game logs are ingested daily into Azure Blob Storage and stored in a folder partitioned based on date and time.</span></span> <span data-ttu-id="f9acc-179">Vous souhaitez que le script Pig tooparameterize hello et passez emplacement du dossier d’entrée hello dynamiquement pendant l’exécution et également exportent hello partitionnée avec la date et l’heure.</span><span class="sxs-lookup"><span data-stu-id="f9acc-179">You want tooparameterize hello Pig script and pass hello input folder location dynamically during runtime and also produce hello output partitioned with date and time.</span></span>

<span data-ttu-id="f9acc-180">toouse paramétrables script Pig, procédez comme hello suivant :</span><span class="sxs-lookup"><span data-stu-id="f9acc-180">toouse parameterized Pig script, do hello following:</span></span>

* <span data-ttu-id="f9acc-181">Définir les paramètres de hello dans **définit**.</span><span class="sxs-lookup"><span data-stu-id="f9acc-181">Define hello parameters in **defines**.</span></span>

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
* <span data-ttu-id="f9acc-182">Bonjour Script Pig, font référence à l’aide des paramètres de toohello '**$parameterName**' comme indiqué dans hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="f9acc-182">In hello Pig Script, refer toohello parameters using '**$parameterName**' as shown in hello following example:</span></span>

    ```  
    PigSampleIn = LOAD '$Input' USING PigStorage(',') AS (ProfileID:chararray, SessionStart:chararray, Duration:int, SrcIPAddress:chararray, GameType:chararray);    
    GroupProfile = Group PigSampleIn all;        
    PigSampleOut = Foreach GroupProfile Generate PigSampleIn.ProfileID, SUM(PigSampleIn.Duration);        
    Store PigSampleOut into '$Output' USING PigStorage (','); 
    ```
## <a name="see-also"></a><span data-ttu-id="f9acc-183">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="f9acc-183">See Also</span></span>
* [<span data-ttu-id="f9acc-184">Activité Hive</span><span class="sxs-lookup"><span data-stu-id="f9acc-184">Hive Activity</span></span>](data-factory-hive-activity.md)
* [<span data-ttu-id="f9acc-185">Activité MapReduce</span><span class="sxs-lookup"><span data-stu-id="f9acc-185">MapReduce Activity</span></span>](data-factory-map-reduce.md)
* [<span data-ttu-id="f9acc-186">Activité de diffusion en continu Hadoop</span><span class="sxs-lookup"><span data-stu-id="f9acc-186">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
* [<span data-ttu-id="f9acc-187">Appeler des programmes Spark</span><span class="sxs-lookup"><span data-stu-id="f9acc-187">Invoke Spark programs</span></span>](data-factory-spark.md)
* [<span data-ttu-id="f9acc-188">Appeler des scripts R</span><span class="sxs-lookup"><span data-stu-id="f9acc-188">Invoke R scripts</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)

