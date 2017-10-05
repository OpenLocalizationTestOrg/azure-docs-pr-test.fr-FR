---
title: "Transformer des données à l’aide d’une activité Hive - Azure | Microsoft Docs"
description: "Découvrez comment vous pouvez utiliser l'activité Hive d’une fabrique de données Azure pour exécuter des requêtes Hive sur un cluster HDInsight à la demande/ou votre propre cluster."
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
ms.openlocfilehash: a3e9b2d0a8c851939acd228d8086ddfc9f38a4c1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="transform-data-using-hive-activity-in-azure-data-factory"></a><span data-ttu-id="35819-103">Transformer des données à l’aide d’une activité Hive dans Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="35819-103">Transform data using Hive Activity in Azure Data Factory</span></span> 
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="35819-104">Activité Hive</span><span class="sxs-lookup"><span data-stu-id="35819-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="35819-105">Activité pig</span><span class="sxs-lookup"><span data-stu-id="35819-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="35819-106">Activité MapReduce</span><span class="sxs-lookup"><span data-stu-id="35819-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="35819-107">Activité de diffusion en continu Hadoop</span><span class="sxs-lookup"><span data-stu-id="35819-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="35819-108">Activité Spark</span><span class="sxs-lookup"><span data-stu-id="35819-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="35819-109">Activité d’exécution par lot Machine Learning</span><span class="sxs-lookup"><span data-stu-id="35819-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="35819-110">Activité des ressources de mise à jour de Machine Learning</span><span class="sxs-lookup"><span data-stu-id="35819-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="35819-111">Activité de procédure stockée</span><span class="sxs-lookup"><span data-stu-id="35819-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="35819-112">Activité U-SQL Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="35819-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="35819-113">Activité personnalisée .NET</span><span class="sxs-lookup"><span data-stu-id="35819-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

<span data-ttu-id="35819-114">L’activité Hive HDInsight d’un [pipeline](data-factory-create-pipelines.md) Data Factory exécute des requêtes Hive sur [votre propre](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) cluster ou cluster [à la demande](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) HDInsight sous Windows ou Linux.</span><span class="sxs-lookup"><span data-stu-id="35819-114">The HDInsight Hive activity in a Data Factory [pipeline](data-factory-create-pipelines.md) executes Hive queries on [your own](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) or [on-demand](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) Windows/Linux-based HDInsight cluster.</span></span> <span data-ttu-id="35819-115">Cet article s'appuie sur l'article [Activités de transformation des données](data-factory-data-transformation-activities.md) qui présente une vue d'ensemble de la transformation des données et les activités de transformation prises en charge.</span><span class="sxs-lookup"><span data-stu-id="35819-115">This article builds on the [data transformation activities](data-factory-data-transformation-activities.md) article, which presents a general overview of data transformation and the supported transformation activities.</span></span>

> [!NOTE] 
> <span data-ttu-id="35819-116">Si vous découvrez Azure Data Factory, lisez la [Présentation d’Azure Data Factory](data-factory-introduction.md) et suivez le didacticiel : [Générer votre premier pipeline de données](data-factory-build-your-first-pipeline.md) avant de lire cet article.</span><span class="sxs-lookup"><span data-stu-id="35819-116">If you are new to Azure Data Factory, read through [Introduction to Azure Data Factory](data-factory-introduction.md) and do the tutorial: [Build your first data pipeline](data-factory-build-your-first-pipeline.md) before reading this article.</span></span> 

## <a name="syntax"></a><span data-ttu-id="35819-117">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="35819-117">Syntax</span></span>

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
## <a name="syntax-details"></a><span data-ttu-id="35819-118">Détails de la syntaxe</span><span class="sxs-lookup"><span data-stu-id="35819-118">Syntax details</span></span>
| <span data-ttu-id="35819-119">Propriété</span><span class="sxs-lookup"><span data-stu-id="35819-119">Property</span></span> | <span data-ttu-id="35819-120">Description</span><span class="sxs-lookup"><span data-stu-id="35819-120">Description</span></span> | <span data-ttu-id="35819-121">Requis</span><span class="sxs-lookup"><span data-stu-id="35819-121">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="35819-122">name</span><span class="sxs-lookup"><span data-stu-id="35819-122">name</span></span> |<span data-ttu-id="35819-123">Nom de l’activité</span><span class="sxs-lookup"><span data-stu-id="35819-123">Name of the activity</span></span> |<span data-ttu-id="35819-124">Oui</span><span class="sxs-lookup"><span data-stu-id="35819-124">Yes</span></span> |
| <span data-ttu-id="35819-125">Description</span><span class="sxs-lookup"><span data-stu-id="35819-125">description</span></span> |<span data-ttu-id="35819-126">Texte décrivant la raison motivant l’activité.</span><span class="sxs-lookup"><span data-stu-id="35819-126">Text describing what the activity is used for</span></span> |<span data-ttu-id="35819-127">Non</span><span class="sxs-lookup"><span data-stu-id="35819-127">No</span></span> |
| <span data-ttu-id="35819-128">type</span><span class="sxs-lookup"><span data-stu-id="35819-128">type</span></span> |<span data-ttu-id="35819-129">HDinsightHive</span><span class="sxs-lookup"><span data-stu-id="35819-129">HDinsightHive</span></span> |<span data-ttu-id="35819-130">Oui</span><span class="sxs-lookup"><span data-stu-id="35819-130">Yes</span></span> |
| <span data-ttu-id="35819-131">inputs</span><span class="sxs-lookup"><span data-stu-id="35819-131">inputs</span></span> |<span data-ttu-id="35819-132">Entrées utilisées par l’activité Hive</span><span class="sxs-lookup"><span data-stu-id="35819-132">Inputs consumed by the Hive activity</span></span> |<span data-ttu-id="35819-133">Non</span><span class="sxs-lookup"><span data-stu-id="35819-133">No</span></span> |
| <span data-ttu-id="35819-134">outputs</span><span class="sxs-lookup"><span data-stu-id="35819-134">outputs</span></span> |<span data-ttu-id="35819-135">Sorties produites par l’activité Hive</span><span class="sxs-lookup"><span data-stu-id="35819-135">Outputs produced by the Hive activity</span></span> |<span data-ttu-id="35819-136">Oui</span><span class="sxs-lookup"><span data-stu-id="35819-136">Yes</span></span> |
| <span data-ttu-id="35819-137">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="35819-137">linkedServiceName</span></span> |<span data-ttu-id="35819-138">Référence au cluster HDInsight enregistré comme un service lié dans Data Factory</span><span class="sxs-lookup"><span data-stu-id="35819-138">Reference to the HDInsight cluster registered as a linked service in Data Factory</span></span> |<span data-ttu-id="35819-139">Oui</span><span class="sxs-lookup"><span data-stu-id="35819-139">Yes</span></span> |
| <span data-ttu-id="35819-140">script</span><span class="sxs-lookup"><span data-stu-id="35819-140">script</span></span> |<span data-ttu-id="35819-141">Spécifier le script en ligne Hive</span><span class="sxs-lookup"><span data-stu-id="35819-141">Specify the Hive script inline</span></span> |<span data-ttu-id="35819-142">Non</span><span class="sxs-lookup"><span data-stu-id="35819-142">No</span></span> |
| <span data-ttu-id="35819-143">Chemin d'accès du script</span><span class="sxs-lookup"><span data-stu-id="35819-143">script path</span></span> |<span data-ttu-id="35819-144">Stockez le script Hive dans un stockage d'objets blob Azure et indiquez le chemin d'accès au fichier.</span><span class="sxs-lookup"><span data-stu-id="35819-144">Store the Hive script in an Azure blob storage and provide the path to the file.</span></span> <span data-ttu-id="35819-145">Utilisez la propriété ’script’ ou ’scriptPath’.</span><span class="sxs-lookup"><span data-stu-id="35819-145">Use 'script' or 'scriptPath' property.</span></span> <span data-ttu-id="35819-146">Les deux propriétés ne peuvent pas être utilisées simultanément.</span><span class="sxs-lookup"><span data-stu-id="35819-146">Both cannot be used together.</span></span> <span data-ttu-id="35819-147">Le nom de fichier respecte la casse.</span><span class="sxs-lookup"><span data-stu-id="35819-147">The file name is case-sensitive.</span></span> |<span data-ttu-id="35819-148">Non</span><span class="sxs-lookup"><span data-stu-id="35819-148">No</span></span> |
| <span data-ttu-id="35819-149">defines</span><span class="sxs-lookup"><span data-stu-id="35819-149">defines</span></span> |<span data-ttu-id="35819-150">Spécifier les paramètres sous forme de paires clé/valeur pour le référencement au sein du script Hive à l'aide de ’hiveconf’</span><span class="sxs-lookup"><span data-stu-id="35819-150">Specify parameters as key/value pairs for referencing within the Hive script using 'hiveconf'</span></span> |<span data-ttu-id="35819-151">Non</span><span class="sxs-lookup"><span data-stu-id="35819-151">No</span></span> |

## <a name="example"></a><span data-ttu-id="35819-152">Exemple</span><span class="sxs-lookup"><span data-stu-id="35819-152">Example</span></span>
<span data-ttu-id="35819-153">Prenons un exemple d'analyse de journaux de jeux où vous souhaitez identifier le temps passé par les utilisateurs à jouer à des jeux créés par votre entreprise.</span><span class="sxs-lookup"><span data-stu-id="35819-153">Let’s consider an example of game logs analytics where you want to identify the time spent by users playing games launched by your company.</span></span> 

<span data-ttu-id="35819-154">Le journal suivant est un exemple de journal de jeu séparé par des virgules (`,`) et contenant les champs suivants : ProfileID, SessionStart, Duration, SrcIPAddress et GameType.</span><span class="sxs-lookup"><span data-stu-id="35819-154">The following log is a sample game log, which is comma (`,`) separated and contains the following fields – ProfileID, SessionStart, Duration, SrcIPAddress, and GameType.</span></span>

```
1809,2014-05-04 12:04:25.3470000,14,221.117.223.75,CaptureFlag
1703,2014-05-04 06:05:06.0090000,16,12.49.178.247,KingHill
1703,2014-05-04 10:21:57.3290000,10,199.118.18.179,CaptureFlag
1809,2014-05-04 05:24:22.2100000,23,192.84.66.141,KingHill
.....
```

<span data-ttu-id="35819-155">**Script Hive** pour traiter ces données :</span><span class="sxs-lookup"><span data-stu-id="35819-155">The **Hive script** to process this data:</span></span>

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

<span data-ttu-id="35819-156">Pour exécuter ce script Hive dans un pipeline Data Factory, vous devez effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="35819-156">To execute this Hive script in a Data Factory pipeline, you need to do the following</span></span>

1. <span data-ttu-id="35819-157">Créez un service lié pour inscrire [votre propre cluster de calcul HDInsight](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) ou configurer un [cluster de calcul HDInsight à la demande](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).</span><span class="sxs-lookup"><span data-stu-id="35819-157">Create a linked service to register [your own HDInsight compute cluster](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) or configure [on-demand HDInsight compute cluster](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).</span></span> <span data-ttu-id="35819-158">Appelons ce service lié « HDInsightLinkedService ».</span><span class="sxs-lookup"><span data-stu-id="35819-158">Let’s call this linked service “HDInsightLinkedService”.</span></span>
2. <span data-ttu-id="35819-159">Créez un [service lié](data-factory-azure-blob-connector.md) pour configurer la connexion au stockage d'objets blob Azure qui héberge les données.</span><span class="sxs-lookup"><span data-stu-id="35819-159">Create a [linked service](data-factory-azure-blob-connector.md) to configure the connection to Azure Blob storage hosting the data.</span></span> <span data-ttu-id="35819-160">Appelons ce service lié « StorageLinkedService ».</span><span class="sxs-lookup"><span data-stu-id="35819-160">Let’s call this linked service “StorageLinkedService”</span></span>
3. <span data-ttu-id="35819-161">Créez des [jeux de données](data-factory-create-datasets.md) pointant vers les données d'entrée et de sortie.</span><span class="sxs-lookup"><span data-stu-id="35819-161">Create [datasets](data-factory-create-datasets.md) pointing to the input and the output data.</span></span> <span data-ttu-id="35819-162">Appelons le jeu de données d'entrée « HiveSampleIn » et le jeu de données de sortie « HiveSampleOut »</span><span class="sxs-lookup"><span data-stu-id="35819-162">Let’s call the input dataset “HiveSampleIn” and the output dataset “HiveSampleOut”</span></span>
4. <span data-ttu-id="35819-163">Copiez la requête Hive en tant que fichier dans le stockage d’objets blob Azure configuré à l’étape 2 ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="35819-163">Copy the Hive query as a file to Azure Blob Storage configured in step #2.</span></span> <span data-ttu-id="35819-164">Si le stockage pour l’hébergement des données est différent de celui qui héberge ce fichier de requête, créez un service lié de stockage Azure distinct et référencez-le dans l’activité.</span><span class="sxs-lookup"><span data-stu-id="35819-164">if the storage for hosting the data is different from the one hosting this query file, create a separate Azure Storage linked service and refer to it in the activity.</span></span> <span data-ttu-id="35819-165">Utilisez **scriptPath ** pour spécifier le chemin d’accès au fichier de requête Hive et **scriptLinkedService** pour spécifier le stockage Azure qui contient le fichier de script.</span><span class="sxs-lookup"><span data-stu-id="35819-165">Use **scriptPath **to specify the path to hive query file and **scriptLinkedService** to specify the Azure storage that contains the script file.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="35819-166">Vous pouvez également fournir le script en ligne Hive dans la définition d’activité à l’aide de la propriété **script** .</span><span class="sxs-lookup"><span data-stu-id="35819-166">You can also provide the Hive script inline in the activity definition by using the **script** property.</span></span> <span data-ttu-id="35819-167">Nous ne le recommandons pas, car tous les caractères spéciaux du script dans le document JSON doivent être placés dans une séquence d’échappement, ce qui risque d’entraîner des problèmes de débogage.</span><span class="sxs-lookup"><span data-stu-id="35819-167">We do not recommend this approach as all special characters in the script within the JSON document needs to be escaped and may cause debugging issues.</span></span> <span data-ttu-id="35819-168">La meilleure pratique consiste à suivre l’étape 4.</span><span class="sxs-lookup"><span data-stu-id="35819-168">The best practice is to follow step #4.</span></span>
   > 
   > 
5. <span data-ttu-id="35819-169">Créez un pipeline avec l’activité HDInsightHive.</span><span class="sxs-lookup"><span data-stu-id="35819-169">Create a pipeline with the HDInsightHive activity.</span></span> <span data-ttu-id="35819-170">L’activité traite/transforme les données.</span><span class="sxs-lookup"><span data-stu-id="35819-170">The activity processes/transforms the data.</span></span>

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
6. <span data-ttu-id="35819-171">Déployez le pipeline.</span><span class="sxs-lookup"><span data-stu-id="35819-171">Deploy the pipeline.</span></span> <span data-ttu-id="35819-172">Consultez l’article [Création de pipelines](data-factory-create-pipelines.md) pour plus de détails.</span><span class="sxs-lookup"><span data-stu-id="35819-172">See [Creating pipelines](data-factory-create-pipelines.md) article for details.</span></span> 
7. <span data-ttu-id="35819-173">Surveillez le pipeline à l'aide des vues de gestion et de surveillance Data Factory.</span><span class="sxs-lookup"><span data-stu-id="35819-173">Monitor the pipeline using the data factory monitoring and management views.</span></span> <span data-ttu-id="35819-174">Consultez l’article [Surveillance et gestion des pipelines Data Factory](data-factory-monitor-manage-pipelines.md) pour plus d'informations.</span><span class="sxs-lookup"><span data-stu-id="35819-174">See [Monitoring and manage Data Factory pipelines](data-factory-monitor-manage-pipelines.md) article for details.</span></span> 

## <a name="specifying-parameters-for-a-hive-script"></a><span data-ttu-id="35819-175">Spécification des paramètres d’un script Hive</span><span class="sxs-lookup"><span data-stu-id="35819-175">Specifying parameters for a Hive script</span></span>
<span data-ttu-id="35819-176">Dans cet exemple, les journaux de jeux sont reçus quotidiennement dans le stockage blob Azure et sont conservés dans un dossier partitionné par date et par heure.</span><span class="sxs-lookup"><span data-stu-id="35819-176">In this example, game logs are ingested daily into Azure Blob Storage and are stored in a folder partitioned with date and time.</span></span> <span data-ttu-id="35819-177">Vous souhaitez paramétrer le script Hive et fournir dynamiquement l'emplacement du dossier d'entrée pendant l'exécution mais aussi produire la sortie partitionnée par date et par heure.</span><span class="sxs-lookup"><span data-stu-id="35819-177">You want to parameterize the Hive script and pass the input folder location dynamically during runtime and also produce the output partitioned with date and time.</span></span>

<span data-ttu-id="35819-178">Pour utiliser le script Hive paramétré, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="35819-178">To use parameterized Hive script, do the following</span></span>

* <span data-ttu-id="35819-179">Définissez les paramètres dans **defines**.</span><span class="sxs-lookup"><span data-stu-id="35819-179">Define the parameters in **defines**.</span></span>

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
* <span data-ttu-id="35819-180">Dans le script Hive, reportez-vous au paramètre **${hiveconf:parameterName}**.</span><span class="sxs-lookup"><span data-stu-id="35819-180">In the Hive Script, refer to the parameter using **${hiveconf:parameterName}**.</span></span> 
  
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
## <a name="see-also"></a><span data-ttu-id="35819-181">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="35819-181">See Also</span></span>
* [<span data-ttu-id="35819-182">Activité pig</span><span class="sxs-lookup"><span data-stu-id="35819-182">Pig Activity</span></span>](data-factory-pig-activity.md)
* [<span data-ttu-id="35819-183">Activité MapReduce</span><span class="sxs-lookup"><span data-stu-id="35819-183">MapReduce Activity</span></span>](data-factory-map-reduce.md)
* [<span data-ttu-id="35819-184">Activité de diffusion en continu Hadoop</span><span class="sxs-lookup"><span data-stu-id="35819-184">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
* [<span data-ttu-id="35819-185">Appeler des programmes Spark</span><span class="sxs-lookup"><span data-stu-id="35819-185">Invoke Spark programs</span></span>](data-factory-spark.md)
* [<span data-ttu-id="35819-186">Appeler des scripts R</span><span class="sxs-lookup"><span data-stu-id="35819-186">Invoke R scripts</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)

