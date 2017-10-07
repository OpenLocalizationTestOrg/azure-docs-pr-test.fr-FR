---
title: "les données d’aaaTransform à l’aide de la ruche activité - Azure | Documents Microsoft"
description: "Découvrez comment vous pouvez utiliser hello Hive une activité dans un requêtes de données Azure fabrique toorun Hive sur un cluster de HDInsight sur la demande/votre propre."
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 80083218-743e-4da8-bdd2-60d1c77b1227
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: shlo
ms.openlocfilehash: 032400cdb8e8f9873f85b811b4ad7380f4410edf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="transform-data-using-hive-activity-in-azure-data-factory"></a><span data-ttu-id="38662-103">Transformer des données à l’aide d’une activité Hive dans Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="38662-103">Transform data using Hive Activity in Azure Data Factory</span></span> 
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="38662-104">Activité Hive</span><span class="sxs-lookup"><span data-stu-id="38662-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="38662-105">Activité pig</span><span class="sxs-lookup"><span data-stu-id="38662-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="38662-106">Activité MapReduce</span><span class="sxs-lookup"><span data-stu-id="38662-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="38662-107">Activité de diffusion en continu Hadoop</span><span class="sxs-lookup"><span data-stu-id="38662-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="38662-108">Activité Spark</span><span class="sxs-lookup"><span data-stu-id="38662-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="38662-109">Activité d’exécution par lot Machine Learning</span><span class="sxs-lookup"><span data-stu-id="38662-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="38662-110">Activité des ressources de mise à jour de Machine Learning</span><span class="sxs-lookup"><span data-stu-id="38662-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="38662-111">Activité de procédure stockée</span><span class="sxs-lookup"><span data-stu-id="38662-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="38662-112">Activité U-SQL Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="38662-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="38662-113">Activité personnalisée .NET</span><span class="sxs-lookup"><span data-stu-id="38662-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

<span data-ttu-id="38662-114">Hello activité HDInsight Hive dans une fabrique de données [pipeline](data-factory-create-pipelines.md) exécute des requêtes Hive sur [votre propre](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) ou [à la demande](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) cluster HDInsight de basés sur Windows/Linux.</span><span class="sxs-lookup"><span data-stu-id="38662-114">hello HDInsight Hive activity in a Data Factory [pipeline](data-factory-create-pipelines.md) executes Hive queries on [your own](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) or [on-demand](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) Windows/Linux-based HDInsight cluster.</span></span> <span data-ttu-id="38662-115">Cet article s’appuie sur hello [activités de transformation des données](data-factory-data-transformation-activities.md) article, qui présente une vue d’ensemble de la transformation des données et des activités de transformation hello pris en charge.</span><span class="sxs-lookup"><span data-stu-id="38662-115">This article builds on hello [data transformation activities](data-factory-data-transformation-activities.md) article, which presents a general overview of data transformation and hello supported transformation activities.</span></span>

> [!NOTE] 
> <span data-ttu-id="38662-116">Si vous êtes tooAzure nouvelle fabrique de données, lisez [Introduction tooAzure Data Factory](data-factory-introduction.md) et hello didacticiel : [générer votre première pipeline de données](data-factory-build-your-first-pipeline.md) avant de lire cet article.</span><span class="sxs-lookup"><span data-stu-id="38662-116">If you are new tooAzure Data Factory, read through [Introduction tooAzure Data Factory](data-factory-introduction.md) and do hello tutorial: [Build your first data pipeline](data-factory-build-your-first-pipeline.md) before reading this article.</span></span> 

## <a name="syntax"></a><span data-ttu-id="38662-117">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="38662-117">Syntax</span></span>

```JSON
{
    "name": "Hive Activity",
    "description": "description",
    "type": "HDInsightHive",
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
      "script": "Hive script",
      "scriptPath": "<pathtotheHivescriptfileinAzureblobstorage>",
      "defines": {
        "param1": "param1Value"
      }
    },
   "scheduler": {
      "frequency": "Day",
      "interval": 1
    }
}
```
## <a name="syntax-details"></a><span data-ttu-id="38662-118">Détails de la syntaxe</span><span class="sxs-lookup"><span data-stu-id="38662-118">Syntax details</span></span>
| <span data-ttu-id="38662-119">Propriété</span><span class="sxs-lookup"><span data-stu-id="38662-119">Property</span></span> | <span data-ttu-id="38662-120">Description</span><span class="sxs-lookup"><span data-stu-id="38662-120">Description</span></span> | <span data-ttu-id="38662-121">Requis</span><span class="sxs-lookup"><span data-stu-id="38662-121">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="38662-122">name</span><span class="sxs-lookup"><span data-stu-id="38662-122">name</span></span> |<span data-ttu-id="38662-123">Nom de l’activité hello</span><span class="sxs-lookup"><span data-stu-id="38662-123">Name of hello activity</span></span> |<span data-ttu-id="38662-124">Oui</span><span class="sxs-lookup"><span data-stu-id="38662-124">Yes</span></span> |
| <span data-ttu-id="38662-125">description</span><span class="sxs-lookup"><span data-stu-id="38662-125">description</span></span> |<span data-ttu-id="38662-126">Texte qui décrit quelle activité hello est utilisé pour</span><span class="sxs-lookup"><span data-stu-id="38662-126">Text describing what hello activity is used for</span></span> |<span data-ttu-id="38662-127">Non</span><span class="sxs-lookup"><span data-stu-id="38662-127">No</span></span> |
| <span data-ttu-id="38662-128">type</span><span class="sxs-lookup"><span data-stu-id="38662-128">type</span></span> |<span data-ttu-id="38662-129">HDinsightHive</span><span class="sxs-lookup"><span data-stu-id="38662-129">HDinsightHive</span></span> |<span data-ttu-id="38662-130">Oui</span><span class="sxs-lookup"><span data-stu-id="38662-130">Yes</span></span> |
| <span data-ttu-id="38662-131">inputs</span><span class="sxs-lookup"><span data-stu-id="38662-131">inputs</span></span> |<span data-ttu-id="38662-132">Entrées consommée par hello activité Hive</span><span class="sxs-lookup"><span data-stu-id="38662-132">Inputs consumed by hello Hive activity</span></span> |<span data-ttu-id="38662-133">Non</span><span class="sxs-lookup"><span data-stu-id="38662-133">No</span></span> |
| <span data-ttu-id="38662-134">outputs</span><span class="sxs-lookup"><span data-stu-id="38662-134">outputs</span></span> |<span data-ttu-id="38662-135">Sorties produites par l’activité de ruche hello</span><span class="sxs-lookup"><span data-stu-id="38662-135">Outputs produced by hello Hive activity</span></span> |<span data-ttu-id="38662-136">Oui</span><span class="sxs-lookup"><span data-stu-id="38662-136">Yes</span></span> |
| <span data-ttu-id="38662-137">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="38662-137">linkedServiceName</span></span> |<span data-ttu-id="38662-138">Cluster HDInsight de référence toohello enregistré comme un service lié dans la fabrique de données</span><span class="sxs-lookup"><span data-stu-id="38662-138">Reference toohello HDInsight cluster registered as a linked service in Data Factory</span></span> |<span data-ttu-id="38662-139">Oui</span><span class="sxs-lookup"><span data-stu-id="38662-139">Yes</span></span> |
| <span data-ttu-id="38662-140">script</span><span class="sxs-lookup"><span data-stu-id="38662-140">script</span></span> |<span data-ttu-id="38662-141">Spécifiez le script inline Hive de hello</span><span class="sxs-lookup"><span data-stu-id="38662-141">Specify hello Hive script inline</span></span> |<span data-ttu-id="38662-142">Non</span><span class="sxs-lookup"><span data-stu-id="38662-142">No</span></span> |
| <span data-ttu-id="38662-143">chemin d'accès du script</span><span class="sxs-lookup"><span data-stu-id="38662-143">script path</span></span> |<span data-ttu-id="38662-144">Hello du magasin Hive script dans un stockage d’objets blob Azure et fournir hello chemin d’accès toohello fichier.</span><span class="sxs-lookup"><span data-stu-id="38662-144">Store hello Hive script in an Azure blob storage and provide hello path toohello file.</span></span> <span data-ttu-id="38662-145">Utilisez la propriété ’script’ ou ’scriptPath’.</span><span class="sxs-lookup"><span data-stu-id="38662-145">Use 'script' or 'scriptPath' property.</span></span> <span data-ttu-id="38662-146">Les deux propriétés ne peuvent pas être utilisées simultanément.</span><span class="sxs-lookup"><span data-stu-id="38662-146">Both cannot be used together.</span></span> <span data-ttu-id="38662-147">nom de fichier Hello respecte la casse.</span><span class="sxs-lookup"><span data-stu-id="38662-147">hello file name is case-sensitive.</span></span> |<span data-ttu-id="38662-148">Non</span><span class="sxs-lookup"><span data-stu-id="38662-148">No</span></span> |
| <span data-ttu-id="38662-149">defines</span><span class="sxs-lookup"><span data-stu-id="38662-149">defines</span></span> |<span data-ttu-id="38662-150">Spécifiez les paramètres en tant que paires clé/valeur pour le référencement dans le script Hive de hello à l’aide de 'hiveconf'</span><span class="sxs-lookup"><span data-stu-id="38662-150">Specify parameters as key/value pairs for referencing within hello Hive script using 'hiveconf'</span></span> |<span data-ttu-id="38662-151">Non</span><span class="sxs-lookup"><span data-stu-id="38662-151">No</span></span> |

## <a name="example"></a><span data-ttu-id="38662-152">Exemple</span><span class="sxs-lookup"><span data-stu-id="38662-152">Example</span></span>
<span data-ttu-id="38662-153">Prenons l’exemple d’un exemple de jeu consigne analytique où vous souhaitez tooidentify hello temps par les utilisateurs jeux lancée par votre entreprise.</span><span class="sxs-lookup"><span data-stu-id="38662-153">Let’s consider an example of game logs analytics where you want tooidentify hello time spent by users playing games launched by your company.</span></span> 

<span data-ttu-id="38662-154">Bonjour journal suivant est un exemple jeu de journal, qui est la virgule (`,`) séparés et contient hello suivant champs – ID de profil, SessionStart, durée, SrcIPAddress et type de partie.</span><span class="sxs-lookup"><span data-stu-id="38662-154">hello following log is a sample game log, which is comma (`,`) separated and contains hello following fields – ProfileID, SessionStart, Duration, SrcIPAddress, and GameType.</span></span>

```
1809,2014-05-04 12:04:25.3470000,14,221.117.223.75,CaptureFlag
1703,2014-05-04 06:05:06.0090000,16,12.49.178.247,KingHill
1703,2014-05-04 10:21:57.3290000,10,199.118.18.179,CaptureFlag
1809,2014-05-04 05:24:22.2100000,23,192.84.66.141,KingHill
.....
```

<span data-ttu-id="38662-155">Hello **script Hive** tooprocess ces données :</span><span class="sxs-lookup"><span data-stu-id="38662-155">hello **Hive script** tooprocess this data:</span></span>

```
DROP TABLE IF EXISTS HiveSampleIn; 
CREATE EXTERNAL TABLE HiveSampleIn 
(
    ProfileID        string, 
    SessionStart     string, 
    Duration         int, 
    SrcIPAddress     string, 
    GameType         string
) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION 'wasb://adfwalkthrough@<storageaccount>.blob.core.windows.net/samplein/'; 

DROP TABLE IF EXISTS HiveSampleOut; 
CREATE EXTERNAL TABLE HiveSampleOut 
(    
    ProfileID     string, 
    Duration     int
) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION 'wasb://adfwalkthrough@<storageaccount>.blob.core.windows.net/sampleout/';

INSERT OVERWRITE TABLE HiveSampleOut
Select 
    ProfileID,
    SUM(Duration)
FROM HiveSampleIn Group by ProfileID
```

<span data-ttu-id="38662-156">tooexecute cette ruche de script dans un pipeline de fabrique de données, vous devez suivant de hello toodo</span><span class="sxs-lookup"><span data-stu-id="38662-156">tooexecute this Hive script in a Data Factory pipeline, you need toodo hello following</span></span>

1. <span data-ttu-id="38662-157">Créer un service lié de tooregister [cluster de calcul de votre propre HDInsight](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) ou configurer [cluster de calcul à la demande HDInsight](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).</span><span class="sxs-lookup"><span data-stu-id="38662-157">Create a linked service tooregister [your own HDInsight compute cluster](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) or configure [on-demand HDInsight compute cluster](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).</span></span> <span data-ttu-id="38662-158">Appelons ce service lié « HDInsightLinkedService ».</span><span class="sxs-lookup"><span data-stu-id="38662-158">Let’s call this linked service “HDInsightLinkedService”.</span></span>
2. <span data-ttu-id="38662-159">Créer un [service lié](data-factory-azure-blob-connector.md) tooconfigure hello connexion tooAzure stockage d’objets Blob qui héberge les données de salutation.</span><span class="sxs-lookup"><span data-stu-id="38662-159">Create a [linked service](data-factory-azure-blob-connector.md) tooconfigure hello connection tooAzure Blob storage hosting hello data.</span></span> <span data-ttu-id="38662-160">Appelons ce service lié « StorageLinkedService ».</span><span class="sxs-lookup"><span data-stu-id="38662-160">Let’s call this linked service “StorageLinkedService”</span></span>
3. <span data-ttu-id="38662-161">Créer [datasets](data-factory-create-datasets.md) pointant vers l’entrée de toohello et hello les données de sortie.</span><span class="sxs-lookup"><span data-stu-id="38662-161">Create [datasets](data-factory-create-datasets.md) pointing toohello input and hello output data.</span></span> <span data-ttu-id="38662-162">Nous allons appeler hello dataset d’entrée « HiveSampleIn » et hello dataset de sortie « HiveSampleOut »</span><span class="sxs-lookup"><span data-stu-id="38662-162">Let’s call hello input dataset “HiveSampleIn” and hello output dataset “HiveSampleOut”</span></span>
4. <span data-ttu-id="38662-163">Copier requête Hive de hello en tant qu’un tooAzure fichier stockage d’objets Blob configuré à l’étape 2 de #.</span><span class="sxs-lookup"><span data-stu-id="38662-163">Copy hello Hive query as a file tooAzure Blob Storage configured in step #2.</span></span> <span data-ttu-id="38662-164">Si le stockage hello pour héberger les données de hello est différent de hello un hébergement de ce fichier de requête, créer un service lié Azure Storage distinct et faire référence tooit dans l’activité hello.</span><span class="sxs-lookup"><span data-stu-id="38662-164">if hello storage for hosting hello data is different from hello one hosting this query file, create a separate Azure Storage linked service and refer tooit in hello activity.</span></span> <span data-ttu-id="38662-165">Utilisez ** scriptPath ** fichier de requête toohive toospecify hello chemin d’accès et **scriptLinkedService** toospecify hello le stockage Azure qui contient le fichier de script hello.</span><span class="sxs-lookup"><span data-stu-id="38662-165">Use **scriptPath **toospecify hello path toohive query file and **scriptLinkedService** toospecify hello Azure storage that contains hello script file.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="38662-166">Vous pouvez également fournir le script inline Hive hello dans la définition d’activité hello à l’aide de hello **script** propriété.</span><span class="sxs-lookup"><span data-stu-id="38662-166">You can also provide hello Hive script inline in hello activity definition by using hello **script** property.</span></span> <span data-ttu-id="38662-167">Nous déconseillons cette approche que tous les caractères spéciaux dans le script hello dans le document JSON de hello doit toobe séquence d’échappement et peut cause débogage des problèmes.</span><span class="sxs-lookup"><span data-stu-id="38662-167">We do not recommend this approach as all special characters in hello script within hello JSON document needs toobe escaped and may cause debugging issues.</span></span> <span data-ttu-id="38662-168">Il est recommandé de Hello est toofollow étape #4.</span><span class="sxs-lookup"><span data-stu-id="38662-168">hello best practice is toofollow step #4.</span></span>
   > 
   > 
5. <span data-ttu-id="38662-169">Créer un pipeline avec hello HDInsightHive activité.</span><span class="sxs-lookup"><span data-stu-id="38662-169">Create a pipeline with hello HDInsightHive activity.</span></span> <span data-ttu-id="38662-170">les données de salutation processus/transformations activité Hello.</span><span class="sxs-lookup"><span data-stu-id="38662-170">hello activity processes/transforms hello data.</span></span>

    ```JSON   
    {   
        "name": "HiveActivitySamplePipeline",
        "properties": {
        "activities": [
            {
                "name": "HiveActivitySample",
                "type": "HDInsightHive",
                "inputs": [
                {
                    "name": "HiveSampleIn"
                }
                ],
                "outputs": [
                {
                    "name": "HiveSampleOut"
                }
                ],
                "linkedServiceName": "HDInsightLinkedService",
                "typeproperties": {
                    "scriptPath": "adfwalkthrough\\scripts\\samplehive.hql",
                    "scriptLinkedService": "StorageLinkedService"
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                }
            }
            ]
        }
    }
    ```
6. <span data-ttu-id="38662-171">Déploiement du pipeline de hello.</span><span class="sxs-lookup"><span data-stu-id="38662-171">Deploy hello pipeline.</span></span> <span data-ttu-id="38662-172">Consultez l’article [Création de pipelines](data-factory-create-pipelines.md) pour plus de détails.</span><span class="sxs-lookup"><span data-stu-id="38662-172">See [Creating pipelines](data-factory-create-pipelines.md) article for details.</span></span> 
7. <span data-ttu-id="38662-173">Surveiller le pipeline hello à l’aide de la surveillance de fabrique de données hello et vues de gestion.</span><span class="sxs-lookup"><span data-stu-id="38662-173">Monitor hello pipeline using hello data factory monitoring and management views.</span></span> <span data-ttu-id="38662-174">Consultez l’article [Surveillance et gestion des pipelines Data Factory](data-factory-monitor-manage-pipelines.md) pour plus d'informations.</span><span class="sxs-lookup"><span data-stu-id="38662-174">See [Monitoring and manage Data Factory pipelines](data-factory-monitor-manage-pipelines.md) article for details.</span></span> 

## <a name="specifying-parameters-for-a-hive-script"></a><span data-ttu-id="38662-175">Spécification des paramètres d’un script Hive</span><span class="sxs-lookup"><span data-stu-id="38662-175">Specifying parameters for a Hive script</span></span>
<span data-ttu-id="38662-176">Dans cet exemple, les journaux de jeux sont reçus quotidiennement dans le stockage blob Azure et sont conservés dans un dossier partitionné par date et par heure.</span><span class="sxs-lookup"><span data-stu-id="38662-176">In this example, game logs are ingested daily into Azure Blob Storage and are stored in a folder partitioned with date and time.</span></span> <span data-ttu-id="38662-177">Vous voulez tooparameterize hello ruche script et passez emplacement du dossier d’entrée hello dynamiquement pendant l’exécution et également exportent hello partitionnée avec la date et l’heure.</span><span class="sxs-lookup"><span data-stu-id="38662-177">You want tooparameterize hello Hive script and pass hello input folder location dynamically during runtime and also produce hello output partitioned with date and time.</span></span>

<span data-ttu-id="38662-178">toouse paramétrables script Hive, effectuez l’hello suivant</span><span class="sxs-lookup"><span data-stu-id="38662-178">toouse parameterized Hive script, do hello following</span></span>

* <span data-ttu-id="38662-179">Définir les paramètres de hello dans **définit**.</span><span class="sxs-lookup"><span data-stu-id="38662-179">Define hello parameters in **defines**.</span></span>

    ```JSON  
    {
        "name": "HiveActivitySamplePipeline",
          "properties": {
        "activities": [
             {
                "name": "HiveActivitySample",
                "type": "HDInsightHive",
                "inputs": [
                      {
                        "name": "HiveSampleIn"
                      }
                ],
                "outputs": [
                      {
                        "name": "HiveSampleOut"
                    }
                ],
                "linkedServiceName": "HDInsightLinkedService",
                "typeproperties": {
                      "scriptPath": "adfwalkthrough\\scripts\\samplehive.hql",
                      "scriptLinkedService": "StorageLinkedService",
                      "defines": {
                        "Input": "$$Text.Format('wasb://adfwalkthrough@<storageaccountname>.blob.core.windows.net/samplein/yearno={0:yyyy}/monthno={0:MM}/dayno={0:dd}/', SliceStart)",
                        "Output": "$$Text.Format('wasb://adfwalkthrough@<storageaccountname>.blob.core.windows.net/sampleout/yearno={0:yyyy}/monthno={0:MM}/dayno={0:dd}/', SliceStart)"
                      },
                       "scheduler": {
                          "frequency": "Hour",
                          "interval": 1
                    }
                }
              }
        ]
      }
    }
    ```
* <span data-ttu-id="38662-180">Bonjour Script Hive, reportez-vous à l’aide du paramètre toohello **${hiveconf : ParameterName}**.</span><span class="sxs-lookup"><span data-stu-id="38662-180">In hello Hive Script, refer toohello parameter using **${hiveconf:parameterName}**.</span></span> 
  
    ```
    DROP TABLE IF EXISTS HiveSampleIn; 
    CREATE EXTERNAL TABLE HiveSampleIn 
    (
        ProfileID     string, 
        SessionStart     string, 
        Duration     int, 
        SrcIPAddress     string, 
        GameType     string
    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:Input}'; 

    DROP TABLE IF EXISTS HiveSampleOut; 
    CREATE EXTERNAL TABLE HiveSampleOut 
    (
        ProfileID     string, 
        Duration     int
    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:Output}';

    INSERT OVERWRITE TABLE HiveSampleOut
    Select 
        ProfileID,
        SUM(Duration)
    FROM HiveSampleIn Group by ProfileID
    ```
## <a name="see-also"></a><span data-ttu-id="38662-181">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="38662-181">See Also</span></span>
* [<span data-ttu-id="38662-182">Activité pig</span><span class="sxs-lookup"><span data-stu-id="38662-182">Pig Activity</span></span>](data-factory-pig-activity.md)
* [<span data-ttu-id="38662-183">Activité MapReduce</span><span class="sxs-lookup"><span data-stu-id="38662-183">MapReduce Activity</span></span>](data-factory-map-reduce.md)
* [<span data-ttu-id="38662-184">Activité de diffusion en continu Hadoop</span><span class="sxs-lookup"><span data-stu-id="38662-184">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
* [<span data-ttu-id="38662-185">Appeler des programmes Spark</span><span class="sxs-lookup"><span data-stu-id="38662-185">Invoke Spark programs</span></span>](data-factory-spark.md)
* [<span data-ttu-id="38662-186">Appeler des scripts R</span><span class="sxs-lookup"><span data-stu-id="38662-186">Invoke R scripts</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)

