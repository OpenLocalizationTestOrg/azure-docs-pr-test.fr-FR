---
title: "aaaBuild votre première data factory (modèle de gestionnaire de ressources) | Documents Microsoft"
description: "Dans ce didacticiel, vous créez un exemple de pipeline Azure Data Factory en utilisant un modèle Azure Resource Manager."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: eb9e70b9-a13a-4a27-8256-2759496be470
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: fa08cd1ac3a0e5c5bf4bd4c6bd9dfa6dba9f4319
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-build-your-first-azure-data-factory-using-azure-resource-manager-template"></a><span data-ttu-id="9b0e6-103">Didacticiel : concevoir votre première fabrique de données Azure à l’aide du modèle Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="9b0e6-103">Tutorial: Build your first Azure data factory using Azure Resource Manager template</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9b0e6-104">Vue d’ensemble et étapes préalables requises</span><span class="sxs-lookup"><span data-stu-id="9b0e6-104">Overview and prerequisites</span></span>](data-factory-build-your-first-pipeline.md)
> * [<span data-ttu-id="9b0e6-105">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="9b0e6-105">Azure portal</span></span>](data-factory-build-your-first-pipeline-using-editor.md)
> * [<span data-ttu-id="9b0e6-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="9b0e6-106">Visual Studio</span></span>](data-factory-build-your-first-pipeline-using-vs.md)
> * [<span data-ttu-id="9b0e6-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="9b0e6-107">PowerShell</span></span>](data-factory-build-your-first-pipeline-using-powershell.md)
> * [<span data-ttu-id="9b0e6-108">Modèle Resource Manager</span><span class="sxs-lookup"><span data-stu-id="9b0e6-108">Resource Manager Template</span></span>](data-factory-build-your-first-pipeline-using-arm.md)
> * [<span data-ttu-id="9b0e6-109">API REST</span><span class="sxs-lookup"><span data-stu-id="9b0e6-109">REST API</span></span>](data-factory-build-your-first-pipeline-using-rest-api.md)
> 
> 

<span data-ttu-id="9b0e6-110">Dans cet article, vous utilisez un toocreate de modèle Azure Resource Manager votre première Azure data factory.</span><span class="sxs-lookup"><span data-stu-id="9b0e6-110">In this article, you use an Azure Resource Manager template toocreate your first Azure data factory.</span></span> <span data-ttu-id="9b0e6-111">didacticiel de hello toodo à l’aide d’autres outils/kits de développement logiciel, sélectionnez une des options de hello à partir de la liste déroulante de hello.</span><span class="sxs-lookup"><span data-stu-id="9b0e6-111">toodo hello tutorial using other tools/SDKs, select one of hello options from hello drop-down list.</span></span>

<span data-ttu-id="9b0e6-112">pipeline Hello dans ce didacticiel a une activité : **activité HDInsight Hive**.</span><span class="sxs-lookup"><span data-stu-id="9b0e6-112">hello pipeline in this tutorial has one activity: **HDInsight Hive activity**.</span></span> <span data-ttu-id="9b0e6-113">Cette activité s’exécute un script hive sur un cluster Azure HDInsight et les transformations d’entrée de données de sortie tooproduce.</span><span class="sxs-lookup"><span data-stu-id="9b0e6-113">This activity runs a hive script on an Azure HDInsight cluster that transforms input data tooproduce output data.</span></span> <span data-ttu-id="9b0e6-114">pipeline de Hello est planifiée toorun une fois qu’un mois entre hello spécifié d’heures de début et de fin.</span><span class="sxs-lookup"><span data-stu-id="9b0e6-114">hello pipeline is scheduled toorun once a month between hello specified start and end times.</span></span> 

> [!NOTE]
> <span data-ttu-id="9b0e6-115">le pipeline de données Hello dans ce didacticiel transforme les données de sortie de données d’entrée tooproduce.</span><span class="sxs-lookup"><span data-stu-id="9b0e6-115">hello data pipeline in this tutorial transforms input data tooproduce output data.</span></span> <span data-ttu-id="9b0e6-116">Pour obtenir un didacticiel sur la façon de toocopy les données à l’aide d’Azure Data Factory, consultez [didacticiel : copier des données à partir du stockage d’objets Blob tooSQL de base de données](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="9b0e6-116">For a tutorial on how toocopy data using Azure Data Factory, see [Tutorial: Copy data from Blob Storage tooSQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
> 
> <span data-ttu-id="9b0e6-117">pipeline de Hello dans ce didacticiel ne comprend qu’une seule activité de type : HDInsightHive.</span><span class="sxs-lookup"><span data-stu-id="9b0e6-117">hello pipeline in this tutorial has only one activity of type: HDInsightHive.</span></span> <span data-ttu-id="9b0e6-118">Un pipeline peut contenir plusieurs activités.</span><span class="sxs-lookup"><span data-stu-id="9b0e6-118">A pipeline can have more than one activity.</span></span> <span data-ttu-id="9b0e6-119">De plus, vous pouvez concaténer les deux activités (exécutée une activité après l’autre) en définissant le dataset de sortie hello d’une activité hello d’entrée dataset Hello autre activité.</span><span class="sxs-lookup"><span data-stu-id="9b0e6-119">And, you can chain two activities (run one activity after another) by setting hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="9b0e6-120">Pour plus d’informations, consultez [Planification et exécution dans Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span><span class="sxs-lookup"><span data-stu-id="9b0e6-120">For more information, see [scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="9b0e6-121">Composants requis</span><span class="sxs-lookup"><span data-stu-id="9b0e6-121">Prerequisites</span></span>
* <span data-ttu-id="9b0e6-122">Lisez [vue d’ensemble du didacticiel](data-factory-build-your-first-pipeline.md) article et hello complète **condition préalable** étapes.</span><span class="sxs-lookup"><span data-stu-id="9b0e6-122">Read through [Tutorial Overview](data-factory-build-your-first-pipeline.md) article and complete hello **prerequisite** steps.</span></span>
* <span data-ttu-id="9b0e6-123">Suivez les instructions de [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview) article tooinstall version la plus récente d’Azure PowerShell sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="9b0e6-123">Follow instructions in [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) article tooinstall latest version of Azure PowerShell on your computer.</span></span>
* <span data-ttu-id="9b0e6-124">Consultez [de création de modèles de gestionnaire de ressources Azure](../azure-resource-manager/resource-group-authoring-templates.md) toolearn sur les modèles Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="9b0e6-124">See [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md) toolearn about Azure Resource Manager templates.</span></span> 

## <a name="in-this-tutorial"></a><span data-ttu-id="9b0e6-125">Dans ce didacticiel</span><span class="sxs-lookup"><span data-stu-id="9b0e6-125">In this tutorial</span></span>
| <span data-ttu-id="9b0e6-126">Entité</span><span class="sxs-lookup"><span data-stu-id="9b0e6-126">Entity</span></span> | <span data-ttu-id="9b0e6-127">Description</span><span class="sxs-lookup"><span data-stu-id="9b0e6-127">Description</span></span> |
| --- | --- |
| <span data-ttu-id="9b0e6-128">Service lié Azure Storage</span><span class="sxs-lookup"><span data-stu-id="9b0e6-128">Azure Storage linked service</span></span> |<span data-ttu-id="9b0e6-129">Lie votre fabrique de données toohello compte Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="9b0e6-129">Links your Azure Storage account toohello data factory.</span></span> <span data-ttu-id="9b0e6-130">blocages de compte de stockage Azure Hello hello des données d’entrée et de sortie pour le pipeline hello dans cet exemple.</span><span class="sxs-lookup"><span data-stu-id="9b0e6-130">hello Azure Storage account holds hello input and output data for hello pipeline in this sample.</span></span> |
| <span data-ttu-id="9b0e6-131">Service lié à la demande HDInsight</span><span class="sxs-lookup"><span data-stu-id="9b0e6-131">HDInsight on-demand linked service</span></span> |<span data-ttu-id="9b0e6-132">Lie une fabrique de données à la demande HDInsight cluster toohello.</span><span class="sxs-lookup"><span data-stu-id="9b0e6-132">Links an on-demand HDInsight cluster toohello data factory.</span></span> <span data-ttu-id="9b0e6-133">cluster de Hello est automatiquement créé pour vous tooprocess des données et est supprimé après que traitement de hello est effectué.</span><span class="sxs-lookup"><span data-stu-id="9b0e6-133">hello cluster is automatically created for you tooprocess data and is deleted after hello processing is done.</span></span> |
| <span data-ttu-id="9b0e6-134">Jeu de données d'entrée d'objet Blob Azure</span><span class="sxs-lookup"><span data-stu-id="9b0e6-134">Azure Blob input dataset</span></span> |<span data-ttu-id="9b0e6-135">Fait référence toohello lié Azure Storage service.</span><span class="sxs-lookup"><span data-stu-id="9b0e6-135">Refers toohello Azure Storage linked service.</span></span> <span data-ttu-id="9b0e6-136">Hello service lié fait référence compte de stockage Azure tooan et dataset d’objets Blob Azure hello spécifie hello conteneur, dossier et nom de fichier dans le stockage hello qui contient les données d’entrée hello.</span><span class="sxs-lookup"><span data-stu-id="9b0e6-136">hello linked service refers tooan Azure Storage account and hello Azure Blob dataset specifies hello container, folder, and file name in hello storage that holds hello input data.</span></span> |
| <span data-ttu-id="9b0e6-137">Jeu de données de sortie d’objet Blob Azure</span><span class="sxs-lookup"><span data-stu-id="9b0e6-137">Azure Blob output dataset</span></span> |<span data-ttu-id="9b0e6-138">Fait référence toohello lié Azure Storage service.</span><span class="sxs-lookup"><span data-stu-id="9b0e6-138">Refers toohello Azure Storage linked service.</span></span> <span data-ttu-id="9b0e6-139">Hello service lié fait référence compte de stockage Azure tooan et dataset d’objets Blob Azure hello spécifie hello conteneur, dossier et nom de fichier dans le stockage hello qui contient les données de sortie hello.</span><span class="sxs-lookup"><span data-stu-id="9b0e6-139">hello linked service refers tooan Azure Storage account and hello Azure Blob dataset specifies hello container, folder, and file name in hello storage that holds hello output data.</span></span> |
| <span data-ttu-id="9b0e6-140">Pipeline de données</span><span class="sxs-lookup"><span data-stu-id="9b0e6-140">Data pipeline</span></span> |<span data-ttu-id="9b0e6-141">pipeline de Hello a une activité de type HDInsightHive, ce qui consomme hello de jeu de données d’entrée et produit le jeu de données de sortie hello.</span><span class="sxs-lookup"><span data-stu-id="9b0e6-141">hello pipeline has one activity of type HDInsightHive, which consumes hello input dataset and produces hello output dataset.</span></span> |

<span data-ttu-id="9b0e6-142">Une fabrique de données peut avoir un ou plusieurs pipelines.</span><span class="sxs-lookup"><span data-stu-id="9b0e6-142">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="9b0e6-143">Un pipeline peut contenir une ou plusieurs activités.</span><span class="sxs-lookup"><span data-stu-id="9b0e6-143">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="9b0e6-144">Il existe deux types d’activités : les [activités de déplacement des données](data-factory-data-movement-activities.md) et les [activités de transformation des données](data-factory-data-transformation-activities.md).</span><span class="sxs-lookup"><span data-stu-id="9b0e6-144">There are two types of activities: [data movement activities](data-factory-data-movement-activities.md) and [data transformation activities](data-factory-data-transformation-activities.md).</span></span> <span data-ttu-id="9b0e6-145">Dans ce didacticiel, vous créez un pipeline avec une activité (activité Hive).</span><span class="sxs-lookup"><span data-stu-id="9b0e6-145">In this tutorial, you create a pipeline with one activity (Hive activity).</span></span>

<span data-ttu-id="9b0e6-146">Hello section suivante fournit modèle de gestionnaire de ressources hello complète permettant de définir des entités de fabrique de données afin que vous puissiez exécuter rapidement via hello didacticiel et test hello du modèle.</span><span class="sxs-lookup"><span data-stu-id="9b0e6-146">hello following section provides hello complete Resource Manager template for defining Data Factory entities so that you can quickly run through hello tutorial and test hello template.</span></span> <span data-ttu-id="9b0e6-147">toounderstand chaque entité de la fabrique de données est définie, voir [des entités de fabrique de données dans le modèle de hello](#data-factory-entities-in-the-template) section.</span><span class="sxs-lookup"><span data-stu-id="9b0e6-147">toounderstand how each Data Factory entity is defined, see [Data Factory entities in hello template](#data-factory-entities-in-the-template) section.</span></span>

## <a name="data-factory-json-template"></a><span data-ttu-id="9b0e6-148">Modèle JSON Data Factory</span><span class="sxs-lookup"><span data-stu-id="9b0e6-148">Data Factory JSON template</span></span>
<span data-ttu-id="9b0e6-149">modèle de gestionnaire de ressources du niveau supérieur Hello pour la définition d’une fabrique de données est :</span><span class="sxs-lookup"><span data-stu-id="9b0e6-149">hello top-level Resource Manager template for defining a data factory is:</span></span> 

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": { ...
    },
    "variables": { ...
    },
    "resources": [
        {
            "name": "[parameters('dataFactoryName')]",
            "apiVersion": "[variables('apiVersion')]",
            "type": "Microsoft.DataFactory/datafactories",
            "location": "westus",
            "resources": [
                { ... },
                { ... },
                { ... },
                { ... }
            ]
        }
    ]
}
```
<span data-ttu-id="9b0e6-150">Créez un fichier JSON nommé **ADFTutorialARM.json** dans **C:\ADFGetStarted** dossier avec hello suivant le contenu :</span><span class="sxs-lookup"><span data-stu-id="9b0e6-150">Create a JSON file named **ADFTutorialARM.json** in **C:\ADFGetStarted** folder with hello following content:</span></span>

```json
{
    "contentVersion": "1.0.0.0",
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "parameters": {
        "storageAccountName": { "type": "string", "metadata": { "description": "Name of hello Azure storage account that contains hello input/output data." } },
          "storageAccountKey": { "type": "securestring", "metadata": { "description": "Key for hello Azure storage account." } },
          "blobContainer": { "type": "string", "metadata": { "description": "Name of hello blob container in hello Azure Storage account." } },
          "inputBlobFolder": { "type": "string", "metadata": { "description": "hello folder in hello blob container that has hello input file." } },
          "inputBlobName": { "type": "string", "metadata": { "description": "Name of hello input file/blob." } },
          "outputBlobFolder": { "type": "string", "metadata": { "description": "hello folder in hello blob container that will hold hello transformed data." } },
          "hiveScriptFolder": { "type": "string", "metadata": { "description": "hello folder in hello blob container that contains hello Hive query file." } },
          "hiveScriptFile": { "type": "string", "metadata": { "description": "Name of hello hive query (HQL) file." } }
    },
    "variables": {
          "dataFactoryName": "[concat('HiveTransformDF', uniqueString(resourceGroup().id))]",
          "azureStorageLinkedServiceName": "AzureStorageLinkedService",
          "hdInsightOnDemandLinkedServiceName": "HDInsightOnDemandLinkedService",
          "blobInputDatasetName": "AzureBlobInput",
          "blobOutputDatasetName": "AzureBlobOutput",
          "pipelineName": "HiveTransformPipeline"
    },
    "resources": [
      {
        "name": "[variables('dataFactoryName')]",
        "apiVersion": "2015-10-01",
        "type": "Microsoft.DataFactory/datafactories",
        "location": "West US",
        "resources": [
          {
            "type": "linkedservices",
            "name": "[variables('azureStorageLinkedServiceName')]",
            "dependsOn": [
                  "[variables('dataFactoryName')]"
            ],
            "apiVersion": "2015-10-01",
            "properties": {
                  "type": "AzureStorage",
                  "description": "Azure Storage linked service",
                  "typeProperties": {
                    "connectionString": "[concat('DefaultEndpointsProtocol=https;AccountName=',parameters('storageAccountName'),';AccountKey=',parameters('storageAccountKey'))]"
                  }
            }
          },
          {
            "type": "linkedservices",
            "name": "[variables('hdInsightOnDemandLinkedServiceName')]",
            "dependsOn": [
                  "[variables('dataFactoryName')]",
                  "[variables('azureStorageLinkedServiceName')]"
            ],
            "apiVersion": "2015-10-01",
            "properties": {
                  "type": "HDInsightOnDemand",
                  "typeProperties": {
                    "version": "3.5",
                    "clusterSize": 1,
                    "timeToLive": "00:05:00",
                    "osType": "Linux",
                    "linkedServiceName": "[variables('azureStorageLinkedServiceName')]"
                  }
            }
          },
          {
            "type": "datasets",
            "name": "[variables('blobInputDatasetName')]",
            "dependsOn": [
                  "[variables('dataFactoryName')]",
                  "[variables('azureStorageLinkedServiceName')]"
            ],
            "apiVersion": "2015-10-01",
            "properties": {
                  "type": "AzureBlob",
                  "linkedServiceName": "[variables('azureStorageLinkedServiceName')]",
                  "typeProperties": {
                    "fileName": "[parameters('inputBlobName')]",
                    "folderPath": "[concat(parameters('blobContainer'), '/', parameters('inputBlobFolder'))]",
                    "format": {
                          "type": "TextFormat",
                          "columnDelimiter": ","
                    }
                  },
                  "availability": {
                    "frequency": "Month",
                    "interval": 1
                  },
                  "external": true
            }
          },
          {
            "type": "datasets",
            "name": "[variables('blobOutputDatasetName')]",
            "dependsOn": [
                  "[variables('dataFactoryName')]",
                  "[variables('azureStorageLinkedServiceName')]"
            ],
            "apiVersion": "2015-10-01",
            "properties": {
                  "type": "AzureBlob",
                  "linkedServiceName": "[variables('azureStorageLinkedServiceName')]",
                  "typeProperties": {
                    "folderPath": "[concat(parameters('blobContainer'), '/', parameters('outputBlobFolder'))]",
                    "format": {
                          "type": "TextFormat",
                          "columnDelimiter": ","
                    }
                  },
                  "availability": {
                    "frequency": "Month",
                    "interval": 1
                  }
            }
          },
          {
            "type": "datapipelines",
            "name": "[variables('pipelineName')]",
            "dependsOn": [
                  "[variables('dataFactoryName')]",
                  "[variables('azureStorageLinkedServiceName')]",
                  "[variables('hdInsightOnDemandLinkedServiceName')]",
                  "[variables('blobInputDatasetName')]",
                  "[variables('blobOutputDatasetName')]"
            ],
            "apiVersion": "2015-10-01",
            "properties": {
                  "description": "Pipeline that transforms data using Hive script.",
                  "activities": [
                {
                      "type": "HDInsightHive",
                      "typeProperties": {
                        "scriptPath": "[concat(parameters('blobContainer'), '/', parameters('hiveScriptFolder'), '/', parameters('hiveScriptFile'))]",
                        "scriptLinkedService": "[variables('azureStorageLinkedServiceName')]",
                        "defines": {
                              "inputtable": "[concat('wasb://', parameters('blobContainer'), '@', parameters('storageAccountName'), '.blob.core.windows.net/', parameters('inputBlobFolder'))]",
                              "partitionedtable": "[concat('wasb://', parameters('blobContainer'), '@', parameters('storageAccountName'), '.blob.core.windows.net/', parameters('outputBlobFolder'))]"
                        }
                      },
                      "inputs": [
                        {
                              "name": "[variables('blobInputDatasetName')]"
                        }
                      ],
                      "outputs": [
                        {
                              "name": "[variables('blobOutputDatasetName')]"
                        }
                      ],
                      "policy": {
                        "concurrency": 1,
                        "retry": 3
                      },
                      "scheduler": {
                        "frequency": "Month",
                        "interval": 1
                      },
                      "name": "RunSampleHiveActivity",
                      "linkedServiceName": "[variables('hdInsightOnDemandLinkedServiceName')]"
                }
                  ],
                  "start": "2017-07-01T00:00:00Z",
                  "end": "2017-07-02T00:00:00Z",
                  "isPaused": false
              }
          }
        ]
      }
    ]
}
```

> [!NOTE]
> <span data-ttu-id="9b0e6-151">Vous trouverez un autre exemple de modèle Resource Manager pour créer une fabrique de données Azure dans le [didacticiel : Créer un pipeline avec activité de copie à l’aide d’un modèle Azure Resource Manager](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md).</span><span class="sxs-lookup"><span data-stu-id="9b0e6-151">You can find another example of Resource Manager template for creating an Azure data factory on [Tutorial: Create a pipeline with Copy Activity using an Azure Resource Manager template](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md).</span></span>  
> 
> 

## <a name="parameters-json"></a><span data-ttu-id="9b0e6-152">Paramètres JSON</span><span class="sxs-lookup"><span data-stu-id="9b0e6-152">Parameters JSON</span></span>
<span data-ttu-id="9b0e6-153">Créez un fichier JSON nommé **ADFTutorialARM-Parameters.json** qui contient les paramètres de modèle de gestionnaire de ressources Azure hello.</span><span class="sxs-lookup"><span data-stu-id="9b0e6-153">Create a JSON file named **ADFTutorialARM-Parameters.json** that contains parameters for hello Azure Resource Manager template.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="9b0e6-154">Spécifiez le nom de hello et la clé de votre compte de stockage Azure pour hello **storageAccountName** et **storageAccountKey** paramètres dans ce fichier de paramètres.</span><span class="sxs-lookup"><span data-stu-id="9b0e6-154">Specify hello name and key of your Azure Storage account for hello **storageAccountName** and **storageAccountKey** parameters in this parameter file.</span></span> 
> 
> 

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "storageAccountName": {
            "value": "<Name of your Azure Storage account>"
        },
        "storageAccountKey": {
            "value": "<Key of your Azure Storage account>"
        },
        "blobContainer": {
            "value": "adfgetstarted"
        },
        "inputBlobFolder": {
            "value": "inputdata"
        },
        "inputBlobName": {
            "value": "input.log"
        },
        "outputBlobFolder": {
            "value": "partitioneddata"
        },
        "hiveScriptFolder": {
              "value": "script"
        },
        "hiveScriptFile": {
              "value": "partitionweblogs.hql"
        }
    }
}
```

> [!IMPORTANT]
> <span data-ttu-id="9b0e6-155">Vous avez peut-être fichiers JSON de paramètres distincts pour le développement, test et les environnements de production que vous pouvez utiliser avec hello même modèle JSON de fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="9b0e6-155">You may have separate parameter JSON files for development, testing, and production environments that you can use with hello same Data Factory JSON template.</span></span> <span data-ttu-id="9b0e6-156">En utilisant un script PowerShell, vous pouvez automatiser le déploiement des entités Data Factory dans ces environnements.</span><span class="sxs-lookup"><span data-stu-id="9b0e6-156">By using a Power Shell script, you can automate deploying Data Factory entities in these environments.</span></span> 
> 
> 

## <a name="create-data-factory"></a><span data-ttu-id="9b0e6-157">Créer une fabrique de données</span><span class="sxs-lookup"><span data-stu-id="9b0e6-157">Create data factory</span></span>
1. <span data-ttu-id="9b0e6-158">Démarrer **Azure PowerShell** et hello exécution de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="9b0e6-158">Start **Azure PowerShell** and run hello following command:</span></span> 
   * <span data-ttu-id="9b0e6-159">Exécutez hello suivant de commande et entrez le nom d’utilisateur hello et le mot de passe que vous utilisez toosign dans toohello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="9b0e6-159">Run hello following command and enter hello user name and password that you use toosign in toohello Azure portal.</span></span>
    ```PowerShell
    Login-AzureRmAccount
    ```  
   * <span data-ttu-id="9b0e6-160">Exécutez hello suivant commande tooview tous les abonnements hello pour ce compte.</span><span class="sxs-lookup"><span data-stu-id="9b0e6-160">Run hello following command tooview all hello subscriptions for this account.</span></span>
    ```PowerShell
    Get-AzureRmSubscription
    ``` 
   * <span data-ttu-id="9b0e6-161">Tooselect hello abonnement toowork avec la commande suivante d’exécution hello.</span><span class="sxs-lookup"><span data-stu-id="9b0e6-161">Run hello following command tooselect hello subscription that you want toowork with.</span></span> <span data-ttu-id="9b0e6-162">Cet abonnement doit être hello identique à celui Bonjour portail Azure hello.</span><span class="sxs-lookup"><span data-stu-id="9b0e6-162">This subscription should be hello same as hello one you used in hello Azure portal.</span></span>
    ```
    Get-AzureRmSubscription -SubscriptionName <SUBSCRIPTION NAME> | Set-AzureRmContext
    ```   
2. <span data-ttu-id="9b0e6-163">Hello exécution suivant des entités de fabrique de données toodeploy de commande à l’aide du modèle de gestionnaire de ressources hello que vous avez créé à l’étape 1.</span><span class="sxs-lookup"><span data-stu-id="9b0e6-163">Run hello following command toodeploy Data Factory entities using hello Resource Manager template you created in Step 1.</span></span> 

    ```PowerShell
    New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile C:\ADFGetStarted\ADFTutorialARM.json -TemplateParameterFile C:\ADFGetStarted\ADFTutorialARM-Parameters.json
    ```

## <a name="monitor-pipeline"></a><span data-ttu-id="9b0e6-164">Surveillance d’un pipeline</span><span class="sxs-lookup"><span data-stu-id="9b0e6-164">Monitor pipeline</span></span>
1. <span data-ttu-id="9b0e6-165">Une fois connecté toohello [portail Azure](https://portal.azure.com/), cliquez sur **Parcourir** et sélectionnez **fabriques de données**.</span><span class="sxs-lookup"><span data-stu-id="9b0e6-165">After logging in toohello [Azure portal](https://portal.azure.com/), Click **Browse** and select **Data factories**.</span></span>
     <span data-ttu-id="9b0e6-166">![Parcourir-&gt;Fabriques de données](./media/data-factory-build-your-first-pipeline-using-arm/BrowseDataFactories.png)</span><span class="sxs-lookup"><span data-stu-id="9b0e6-166">![Browse->Data factories](./media/data-factory-build-your-first-pipeline-using-arm/BrowseDataFactories.png)</span></span>
2. <span data-ttu-id="9b0e6-167">Bonjour **fabriques de données** panneau, cliquez sur la fabrique de données hello (**TutorialFactoryARM**) que vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="9b0e6-167">In hello **Data Factories** blade, click hello data factory (**TutorialFactoryARM**) you created.</span></span>    
3. <span data-ttu-id="9b0e6-168">Bonjour **Data Factory** Panneau de votre fabrique de données, cliquez sur **diagramme**.</span><span class="sxs-lookup"><span data-stu-id="9b0e6-168">In hello **Data Factory** blade for your data factory, click **Diagram**.</span></span>

     ![Vignette du diagramme](./media/data-factory-build-your-first-pipeline-using-arm/DiagramTile.png)
4. <span data-ttu-id="9b0e6-170">Bonjour **vue de diagramme**, vous voyez une vue d’ensemble des pipelines de hello et les datasets utilisés dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="9b0e6-170">In hello **Diagram View**, you see an overview of hello pipelines, and datasets used in this tutorial.</span></span>
   
   ![Vue du diagramme](./media/data-factory-build-your-first-pipeline-using-arm/DiagramView.png) 
5. <span data-ttu-id="9b0e6-172">Dans la vue de diagramme de hello, double-cliquez sur hello dataset **AzureBlobOutput**.</span><span class="sxs-lookup"><span data-stu-id="9b0e6-172">In hello Diagram View, double-click hello dataset **AzureBlobOutput**.</span></span> <span data-ttu-id="9b0e6-173">Vous voyez ce secteur hello qui est en cours de traitement.</span><span class="sxs-lookup"><span data-stu-id="9b0e6-173">You see that hello slice that is currently being processed.</span></span>
   
    ![Jeu de données](./media/data-factory-build-your-first-pipeline-using-arm/AzureBlobOutput.png)
6. <span data-ttu-id="9b0e6-175">Lorsque le traitement est terminé, vous consultez la section hello dans **prêt** état.</span><span class="sxs-lookup"><span data-stu-id="9b0e6-175">When processing is done, you see hello slice in **Ready** state.</span></span> <span data-ttu-id="9b0e6-176">La création d’un cluster HDInsight à la demande prend généralement un certain temps (environ 20 minutes).</span><span class="sxs-lookup"><span data-stu-id="9b0e6-176">Creation of an on-demand HDInsight cluster usually takes sometime (approximately 20 minutes).</span></span> <span data-ttu-id="9b0e6-177">Par conséquent, s’attendent hello pipeline tootake **environ 30 minutes** tooprocess hello tranche.</span><span class="sxs-lookup"><span data-stu-id="9b0e6-177">Therefore, expect hello pipeline tootake **approximately 30 minutes** tooprocess hello slice.</span></span>
   
    ![Jeu de données](./media/data-factory-build-your-first-pipeline-using-arm/SliceReady.png)    
7. <span data-ttu-id="9b0e6-179">Lorsque la tranche de hello est à **prêt** d’état, vérifiez hello **partitioneddata** dossier Bonjour **adfgetstarted** conteneur dans votre stockage d’objets blob pour hello les données de sortie.</span><span class="sxs-lookup"><span data-stu-id="9b0e6-179">When hello slice is in **Ready** state, check hello **partitioneddata** folder in hello **adfgetstarted** container in your blob storage for hello output data.</span></span>  

<span data-ttu-id="9b0e6-180">Consultez [analyser des jeux de données et le pipeline](data-factory-monitor-manage-pipelines.md) pour obtenir des instructions sur la façon dont le pipeline hello toomonitor toouse hello panneaux portail Azure et les jeux de données vous avez créé dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="9b0e6-180">See [Monitor datasets and pipeline](data-factory-monitor-manage-pipelines.md) for instructions on how toouse hello Azure portal blades toomonitor hello pipeline and datasets you have created in this tutorial.</span></span>

<span data-ttu-id="9b0e6-181">Vous pouvez également utiliser toomonitor moniteur et l’application de gérer vos pipelines de données.</span><span class="sxs-lookup"><span data-stu-id="9b0e6-181">You can also use Monitor and Manage App toomonitor your data pipelines.</span></span> <span data-ttu-id="9b0e6-182">Consultez [analyse et de gérer les pipelines Azure Data Factory à l’aide d’application de surveillance](data-factory-monitor-manage-app.md) pour plus d’informations sur l’utilisation d’application hello.</span><span class="sxs-lookup"><span data-stu-id="9b0e6-182">See [Monitor and manage Azure Data Factory pipelines using Monitoring App](data-factory-monitor-manage-app.md) for details about using hello application.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="9b0e6-183">fichier d’entrée de Hello est supprimé lors de la tranche de hello est traitée avec succès.</span><span class="sxs-lookup"><span data-stu-id="9b0e6-183">hello input file gets deleted when hello slice is processed successfully.</span></span> <span data-ttu-id="9b0e6-184">Par conséquent, si vous souhaitez tranche de hello toorerun ou que vous hello didacticiel à nouveau, téléchargez hello d’entrée (input.log) toohello inputdata dossier des fichiers du conteneur d’adfgetstarted hello.</span><span class="sxs-lookup"><span data-stu-id="9b0e6-184">Therefore, if you want toorerun hello slice or do hello tutorial again, upload hello input file (input.log) toohello inputdata folder of hello adfgetstarted container.</span></span>
> 
> 

## <a name="data-factory-entities-in-hello-template"></a><span data-ttu-id="9b0e6-185">Entités de fabrique de données dans le modèle de hello</span><span class="sxs-lookup"><span data-stu-id="9b0e6-185">Data Factory entities in hello template</span></span>
### <a name="define-data-factory"></a><span data-ttu-id="9b0e6-186">Définir une fabrique de données</span><span class="sxs-lookup"><span data-stu-id="9b0e6-186">Define data factory</span></span>
<span data-ttu-id="9b0e6-187">Vous définissez une fabrique de données dans le modèle de gestionnaire de ressources hello comme indiqué dans hello suivant l’exemple :</span><span class="sxs-lookup"><span data-stu-id="9b0e6-187">You define a data factory in hello Resource Manager template as shown in hello following sample:</span></span>  

```json
"resources": [
{
    "name": "[variables('dataFactoryName')]",
    "apiVersion": "2015-10-01",
    "type": "Microsoft.DataFactory/datafactories",
    "location": "West US"
}
```
<span data-ttu-id="9b0e6-188">Hello dataFactoryName est défini comme :</span><span class="sxs-lookup"><span data-stu-id="9b0e6-188">hello dataFactoryName is defined as:</span></span> 

```json
"dataFactoryName": "[concat('HiveTransformDF', uniqueString(resourceGroup().id))]",
```
<span data-ttu-id="9b0e6-189">Il s’agit d’une chaîne unique en fonction de l’ID de groupe de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="9b0e6-189">It is a unique string based on hello resource group ID.</span></span>  

### <a name="defining-data-factory-entities"></a><span data-ttu-id="9b0e6-190">Définition des entités Data Factory</span><span class="sxs-lookup"><span data-stu-id="9b0e6-190">Defining Data Factory entities</span></span>
<span data-ttu-id="9b0e6-191">Hello des entités de fabrique de données suivantes sont définies dans le modèle JSON hello :</span><span class="sxs-lookup"><span data-stu-id="9b0e6-191">hello following Data Factory entities are defined in hello JSON template:</span></span> 

* [<span data-ttu-id="9b0e6-192">Service lié Azure Storage</span><span class="sxs-lookup"><span data-stu-id="9b0e6-192">Azure Storage linked service</span></span>](#azure-storage-linked-service)
* [<span data-ttu-id="9b0e6-193">Service lié à la demande HDInsight</span><span class="sxs-lookup"><span data-stu-id="9b0e6-193">HDInsight on-demand linked service</span></span>](#hdinsight-on-demand-linked-service)
* [<span data-ttu-id="9b0e6-194">Jeu de données d'entrée d'objet Blob Azure</span><span class="sxs-lookup"><span data-stu-id="9b0e6-194">Azure blob input dataset</span></span>](#azure-blob-input-dataset)
* [<span data-ttu-id="9b0e6-195">Jeu de données de sortie d’objet Blob Azure</span><span class="sxs-lookup"><span data-stu-id="9b0e6-195">Azure blob output dataset</span></span>](#azure-blob-output-dataset)
* [<span data-ttu-id="9b0e6-196">Pipeline de données avec une activité de copie</span><span class="sxs-lookup"><span data-stu-id="9b0e6-196">Data pipeline with a copy activity</span></span>](#data-pipeline)

#### <a name="azure-storage-linked-service"></a><span data-ttu-id="9b0e6-197">Service lié Azure Storage</span><span class="sxs-lookup"><span data-stu-id="9b0e6-197">Azure Storage linked service</span></span>
<span data-ttu-id="9b0e6-198">Vous spécifiez le nom de hello et la clé de votre compte de stockage Azure dans cette section.</span><span class="sxs-lookup"><span data-stu-id="9b0e6-198">You specify hello name and key of your Azure storage account in this section.</span></span> <span data-ttu-id="9b0e6-199">Consultez [service lié Azure Storage](data-factory-azure-blob-connector.md#azure-storage-linked-service) pour plus d’informations sur JSON propriétés utilisées toodefine un stockage Azure le service lié.</span><span class="sxs-lookup"><span data-stu-id="9b0e6-199">See [Azure Storage linked service](data-factory-azure-blob-connector.md#azure-storage-linked-service) for details about JSON properties used toodefine an Azure Storage linked service.</span></span> 

```json
{
    "type": "linkedservices",
    "name": "[variables('azureStorageLinkedServiceName')]",
    "dependsOn": [
        "[variables('dataFactoryName')]"
    ],
    "apiVersion": "2015-10-01",
    "properties": {
        "type": "AzureStorage",
        "description": "Azure Storage linked service",
        "typeProperties": {
            "connectionString": "[concat('DefaultEndpointsProtocol=https;AccountName=',parameters('storageAccountName'),';AccountKey=',parameters('storageAccountKey'))]"
        }
    }
}
```
<span data-ttu-id="9b0e6-200">Hello **connectionString** utilise hello paramètres storageAccountName et storageAccountKey.</span><span class="sxs-lookup"><span data-stu-id="9b0e6-200">hello **connectionString** uses hello storageAccountName and storageAccountKey parameters.</span></span> <span data-ttu-id="9b0e6-201">valeurs Hello pour ces paramètres passés à l’aide d’un fichier de configuration.</span><span class="sxs-lookup"><span data-stu-id="9b0e6-201">hello values for these parameters passed by using a configuration file.</span></span> <span data-ttu-id="9b0e6-202">définition de Hello utilise également des variables : azureStroageLinkedService et dataFactoryName définies dans le modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="9b0e6-202">hello definition also uses variables: azureStroageLinkedService and dataFactoryName defined in hello template.</span></span> 

#### <a name="hdinsight-on-demand-linked-service"></a><span data-ttu-id="9b0e6-203">Service lié à la demande HDInsight</span><span class="sxs-lookup"><span data-stu-id="9b0e6-203">HDInsight on-demand linked service</span></span>
<span data-ttu-id="9b0e6-204">Consultez [services liés de calcul](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) article pour plus d’informations sur JSON propriétés utilisées toodefine un service lié à la demande de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9b0e6-204">See [Compute linked services](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) article for details about JSON properties used toodefine an HDInsight on-demand linked service.</span></span>  

```json
{
    "type": "linkedservices",
    "name": "[variables('hdInsightOnDemandLinkedServiceName')]",
    "dependsOn": [
        "[variables('dataFactoryName')]"
    ],
    "apiVersion": "2015-10-01",
    "properties": {
        "type": "HDInsightOnDemand",
        "typeProperties": {
            "version": "3.5",
            "clusterSize": 1,
            "timeToLive": "00:05:00",
            "osType": "Linux",
            "linkedServiceName": "[variables('azureStorageLinkedServiceName')]"
        }
    }
}
```
<span data-ttu-id="9b0e6-205">Hello Notez les points suivants :</span><span class="sxs-lookup"><span data-stu-id="9b0e6-205">Note hello following points:</span></span> 

* <span data-ttu-id="9b0e6-206">Hello Data Factory crée un **basés sur Linux** cluster HDInsight pour vous par hello au-dessus de JSON.</span><span class="sxs-lookup"><span data-stu-id="9b0e6-206">hello Data Factory creates a **Linux-based** HDInsight cluster for you with hello above JSON.</span></span> <span data-ttu-id="9b0e6-207">Pour plus d’informations, voir [Service lié à la demande Azure HDInsight](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) .</span><span class="sxs-lookup"><span data-stu-id="9b0e6-207">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span> 
* <span data-ttu-id="9b0e6-208">Vous pouvez utiliser votre **propre cluster HDInsight** au lieu d’utiliser un cluster HDInsight à la demande.</span><span class="sxs-lookup"><span data-stu-id="9b0e6-208">You could use **your own HDInsight cluster** instead of using an on-demand HDInsight cluster.</span></span> <span data-ttu-id="9b0e6-209">Pour plus d’informations, voir [Service lié Azure HDInsight](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) .</span><span class="sxs-lookup"><span data-stu-id="9b0e6-209">See [HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) for details.</span></span>
* <span data-ttu-id="9b0e6-210">Hello HDInsight cluster crée un **conteneur par défaut** dans le stockage blob hello spécifié dans hello JSON (**linkedServiceName**).</span><span class="sxs-lookup"><span data-stu-id="9b0e6-210">hello HDInsight cluster creates a **default container** in hello blob storage you specified in hello JSON (**linkedServiceName**).</span></span> <span data-ttu-id="9b0e6-211">HDInsight ne supprime pas ce conteneur lorsque le cluster de hello est supprimé.</span><span class="sxs-lookup"><span data-stu-id="9b0e6-211">HDInsight does not delete this container when hello cluster is deleted.</span></span> <span data-ttu-id="9b0e6-212">Ce comportement est normal.</span><span class="sxs-lookup"><span data-stu-id="9b0e6-212">This behavior is by design.</span></span> <span data-ttu-id="9b0e6-213">Service lié HDInsight à la demande un cluster HDInsight est créé chaque fois qu’une tranche doit toobe traité sauf s’il existe un cluster dynamique existant (**timeToLive**) et est supprimé quand le traitement de hello est effectué.</span><span class="sxs-lookup"><span data-stu-id="9b0e6-213">With on-demand HDInsight linked service, a HDInsight cluster is created every time a slice needs toobe processed unless there is an existing live cluster (**timeToLive**) and is deleted when hello processing is done.</span></span>
  
    <span data-ttu-id="9b0e6-214">Comme un nombre croissant de tranches sont traitées, vous voyez un grand nombre de conteneurs dans votre stockage d’objets blob Azure.</span><span class="sxs-lookup"><span data-stu-id="9b0e6-214">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="9b0e6-215">Si vous ne devez pas les pour la résolution des problèmes de travaux de hello, vous souhaiterez peut-être toodelete les coûts de stockage tooreduce hello.</span><span class="sxs-lookup"><span data-stu-id="9b0e6-215">If you do not need them for troubleshooting of hello jobs, you may want toodelete them tooreduce hello storage cost.</span></span> <span data-ttu-id="9b0e6-216">les noms de ces conteneurs Hello suivent un modèle : « adf**yourdatafactoryname**-**linkedservicename**- datetimestamp ».</span><span class="sxs-lookup"><span data-stu-id="9b0e6-216">hello names of these containers follow a pattern: "adf**yourdatafactoryname**-**linkedservicename**-datetimestamp".</span></span> <span data-ttu-id="9b0e6-217">Utiliser des outils tels que [Explorateur de stockage Microsoft](http://storageexplorer.com/) stockage d’objets blob des conteneurs de toodelete dans votre Azure.</span><span class="sxs-lookup"><span data-stu-id="9b0e6-217">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) toodelete containers in your Azure blob storage.</span></span>

<span data-ttu-id="9b0e6-218">Pour plus d’informations, voir [Service lié à la demande Azure HDInsight](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) .</span><span class="sxs-lookup"><span data-stu-id="9b0e6-218">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>

#### <a name="azure-blob-input-dataset"></a><span data-ttu-id="9b0e6-219">Jeu de données d'entrée d'objet Blob Azure</span><span class="sxs-lookup"><span data-stu-id="9b0e6-219">Azure blob input dataset</span></span>
<span data-ttu-id="9b0e6-220">Vous spécifiez les noms de conteneur d’objets blob, de dossier et de fichier qui contient les données d’entrée hello hello.</span><span class="sxs-lookup"><span data-stu-id="9b0e6-220">You specify hello names of blob container, folder, and file that contains hello input data.</span></span> <span data-ttu-id="9b0e6-221">Consultez [propriétés de jeu de données d’objets Blob Azure](data-factory-azure-blob-connector.md#dataset-properties) pour plus d’informations sur les propriétés utilisées de JSON toodefine un jeu de données d’objets Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="9b0e6-221">See [Azure Blob dataset properties](data-factory-azure-blob-connector.md#dataset-properties) for details about JSON properties used toodefine an Azure Blob dataset.</span></span> 

```json
{
    "type": "datasets",
    "name": "[variables('blobInputDatasetName')]",
    "dependsOn": [
        "[variables('dataFactoryName')]",
        "[variables('azureStorageLinkedServiceName')]"
    ],
    "apiVersion": "2015-10-01",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "[variables('azureStorageLinkedServiceName')]",
        "typeProperties": {
            "fileName": "[parameters('inputBlobName')]",
            "folderPath": "[concat(parameters('blobContainer'), '/', parameters('inputBlobFolder'))]",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability": {
            "frequency": "Month",
            "interval": 1
        },
        "external": true
    }
}
```
<span data-ttu-id="9b0e6-222">Cette définition utilise hello suivant les paramètres définis dans le modèle de paramètre : blobContainer, inputBlobFolder et inputBlobName.</span><span class="sxs-lookup"><span data-stu-id="9b0e6-222">This definition uses hello following parameters defined in parameter template: blobContainer, inputBlobFolder, and inputBlobName.</span></span> 

#### <a name="azure-blob-output-dataset"></a><span data-ttu-id="9b0e6-223">Jeu de données de sortie d’objet Blob Azure</span><span class="sxs-lookup"><span data-stu-id="9b0e6-223">Azure Blob output dataset</span></span>
<span data-ttu-id="9b0e6-224">Vous spécifiez les noms de conteneur d’objets blob et le dossier qui contient les données de sortie hello hello.</span><span class="sxs-lookup"><span data-stu-id="9b0e6-224">You specify hello names of blob container and folder that holds hello output data.</span></span> <span data-ttu-id="9b0e6-225">Consultez [propriétés de jeu de données d’objets Blob Azure](data-factory-azure-blob-connector.md#dataset-properties) pour plus d’informations sur les propriétés utilisées de JSON toodefine un jeu de données d’objets Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="9b0e6-225">See [Azure Blob dataset properties](data-factory-azure-blob-connector.md#dataset-properties) for details about JSON properties used toodefine an Azure Blob dataset.</span></span>  

```json
{
    "type": "datasets",
    "name": "[variables('blobOutputDatasetName')]",
    "dependsOn": [
        "[variables('dataFactoryName')]",
        "[variables('azureStorageLinkedServiceName')]"
    ],
    "apiVersion": "2015-10-01",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "[variables('azureStorageLinkedServiceName')]",
        "typeProperties": {
            "folderPath": "[concat(parameters('blobContainer'), '/', parameters('outputBlobFolder'))]",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability": {
            "frequency": "Month",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="9b0e6-226">Cette définition utilise hello suivant les paramètres définis dans le modèle de paramètre hello : blobContainer et outputBlobFolder.</span><span class="sxs-lookup"><span data-stu-id="9b0e6-226">This definition uses hello following parameters defined in hello parameter template: blobContainer and outputBlobFolder.</span></span> 

#### <a name="data-pipeline"></a><span data-ttu-id="9b0e6-227">Pipeline de données</span><span class="sxs-lookup"><span data-stu-id="9b0e6-227">Data pipeline</span></span>
<span data-ttu-id="9b0e6-228">Vous définissez un pipeline qui transforme les données en exécutant le script Hive sur un cluster Azure HDInsight à la demande.</span><span class="sxs-lookup"><span data-stu-id="9b0e6-228">You define a pipeline that transform data by running Hive script on an on-demand Azure HDInsight cluster.</span></span> <span data-ttu-id="9b0e6-229">Consultez [JSON de Pipeline](data-factory-create-pipelines.md#pipeline-json) pour les descriptions des éléments utilisés de JSON toodefine un pipeline dans cet exemple.</span><span class="sxs-lookup"><span data-stu-id="9b0e6-229">See [Pipeline JSON](data-factory-create-pipelines.md#pipeline-json) for descriptions of JSON elements used toodefine a pipeline in this example.</span></span> 

```json
{
    "type": "datapipelines",
    "name": "[variables('pipelineName')]",
    "dependsOn": [
        "[variables('dataFactoryName')]",
        "[variables('azureStorageLinkedServiceName')]",
        "[variables('hdInsightOnDemandLinkedServiceName')]",
        "[variables('blobInputDatasetName')]",
        "[variables('blobOutputDatasetName')]"
    ],
    "apiVersion": "2015-10-01",
    "properties": {
        "description": "Pipeline that transforms data using Hive script.",
        "activities": [
        {
            "type": "HDInsightHive",
            "typeProperties": {
                "scriptPath": "[concat(parameters('blobContainer'), '/', parameters('hiveScriptFolder'), '/', parameters('hiveScriptFile'))]",
                "scriptLinkedService": "[variables('azureStorageLinkedServiceName')]",
                "defines": {
                    "inputtable": "[concat('wasb://', parameters('blobContainer'), '@', parameters('storageAccountName'), '.blob.core.windows.net/', parameters('inputBlobFolder'))]",
                    "partitionedtable": "[concat('wasb://', parameters('blobContainer'), '@', parameters('storageAccountName'), '.blob.core.windows.net/', parameters('outputBlobFolder'))]"
                }
            },
            "inputs": [
            {
                "name": "[variables('blobInputDatasetName')]"
            }
            ],
            "outputs": [
            {
                "name": "[variables('blobOutputDatasetName')]"
            }
            ],
            "policy": {
                "concurrency": 1,
                "retry": 3
            },
            "scheduler": {
                "frequency": "Month",
                "interval": 1
            },
            "name": "RunSampleHiveActivity",
            "linkedServiceName": "[variables('hdInsightOnDemandLinkedServiceName')]"
        }
        ],
        "start": "2017-07-01T00:00:00Z",
        "end": "2017-07-02T00:00:00Z",
        "isPaused": false
    }
}
```

## <a name="reuse-hello-template"></a><span data-ttu-id="9b0e6-230">Réutiliser le modèle de hello</span><span class="sxs-lookup"><span data-stu-id="9b0e6-230">Reuse hello template</span></span>
<span data-ttu-id="9b0e6-231">Dans le didacticiel de hello, vous avez créé un modèle permettant de définir des entités de fabrique de données et un modèle pour passer des valeurs pour les paramètres.</span><span class="sxs-lookup"><span data-stu-id="9b0e6-231">In hello tutorial, you created a template for defining Data Factory entities and a template for passing values for parameters.</span></span> <span data-ttu-id="9b0e6-232">toouse hello même modèle toodeploy Data Factory entités toodifferent des environnements, vous créez un fichier de paramètres pour chaque environnement et l’utilisez lors de la toothat environnement de déploiement.</span><span class="sxs-lookup"><span data-stu-id="9b0e6-232">toouse hello same template toodeploy Data Factory entities toodifferent environments, you create a parameter file for each environment and use it when deploying toothat environment.</span></span>     

<span data-ttu-id="9b0e6-233">Exemple :</span><span class="sxs-lookup"><span data-stu-id="9b0e6-233">Example:</span></span>  

```PowerShell
New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFTutorialARM.json -TemplateParameterFile ADFTutorialARM-Parameters-Dev.json

New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFTutorialARM.json -TemplateParameterFile ADFTutorialARM-Parameters-Test.json

New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFTutorialARM.json -TemplateParameterFile ADFTutorialARM-Parameters-Production.json
```
<span data-ttu-id="9b0e6-234">Notez que hello première commande utilise le fichier de paramètres pour l’environnement de développement hello, deuxième hello un environnement de test et hello un tiers pour l’environnement de production hello.</span><span class="sxs-lookup"><span data-stu-id="9b0e6-234">Notice that hello first command uses parameter file for hello development environment, second one for hello test environment, and hello third one for hello production environment.</span></span>  

<span data-ttu-id="9b0e6-235">Vous pouvez également réutiliser hello modèle tooperform tâches récurrentes.</span><span class="sxs-lookup"><span data-stu-id="9b0e6-235">You can also reuse hello template tooperform repeated tasks.</span></span> <span data-ttu-id="9b0e6-236">Par exemple, vous devez toocreate plusieurs fabriques de données avec l’un ou plusieurs pipelines qui implémentent hello même logique, mais chaque données fabrique utilise différents le stockage Azure et les comptes de la base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="9b0e6-236">For example, you need toocreate many data factories with one or more pipelines that implement hello same logic but each data factory uses different Azure storage and Azure SQL Database accounts.</span></span> <span data-ttu-id="9b0e6-237">Dans ce scénario, vous utilisez hello même modèle Bonjour même environnement (développement, test ou production) avec des paramètres différents fichiers toocreate les fabriques de données.</span><span class="sxs-lookup"><span data-stu-id="9b0e6-237">In this scenario, you use hello same template in hello same environment (dev, test, or production) with different parameter files toocreate data factories.</span></span> 

## <a name="resource-manager-template-for-creating-a-gateway"></a><span data-ttu-id="9b0e6-238">Modèle Resource Manager pour la création d’une passerelle</span><span class="sxs-lookup"><span data-stu-id="9b0e6-238">Resource Manager template for creating a gateway</span></span>
<span data-ttu-id="9b0e6-239">Voici un exemple de modèle de gestionnaire de ressources pour la création d’une passerelle logique Bonjour précédent.</span><span class="sxs-lookup"><span data-stu-id="9b0e6-239">Here is a sample Resource Manager template for creating a logical gateway in hello back.</span></span> <span data-ttu-id="9b0e6-240">Installer une passerelle sur votre ordinateur local ou d’une machine virtuelle IaaS de Azure et passerelle de hello auprès de service de fabrique de données à l’aide d’une clé.</span><span class="sxs-lookup"><span data-stu-id="9b0e6-240">Install a gateway on your on-premises computer or Azure IaaS VM and register hello gateway with Data Factory service using a key.</span></span> <span data-ttu-id="9b0e6-241">Pour plus d’informations, consultez [Déplacer des données entre un emplacement local et le cloud](data-factory-move-data-between-onprem-and-cloud.md) .</span><span class="sxs-lookup"><span data-stu-id="9b0e6-241">See [Move data between on-premises and cloud](data-factory-move-data-between-onprem-and-cloud.md) for details.</span></span>

```json
{
    "contentVersion": "1.0.0.0",
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "parameters": {
    },
    "variables": {
        "dataFactoryName":  "GatewayUsingArmDF",
        "apiVersion": "2015-10-01",
        "singleQuote": "'"
    },
    "resources": [
        {
            "name": "[variables('dataFactoryName')]",
            "apiVersion": "[variables('apiVersion')]",
            "type": "Microsoft.DataFactory/datafactories",
            "location": "eastus",
            "resources": [
                {
                    "dependsOn": [ "[concat('Microsoft.DataFactory/dataFactories/', variables('dataFactoryName'))]" ],
                    "type": "gateways",
                    "apiVersion": "[variables('apiVersion')]",
                    "name": "GatewayUsingARM",
                    "properties": {
                        "description": "my gateway"
                    }
                }            
            ]
        }
    ]
}
```
<span data-ttu-id="9b0e6-242">Ce modèle crée une fabrique de données nommée GatewayUsingArmDF avec une passerelle nommée GatewayUsingARM.</span><span class="sxs-lookup"><span data-stu-id="9b0e6-242">This template creates a data factory named GatewayUsingArmDF with a gateway named: GatewayUsingARM.</span></span> 

## <a name="see-also"></a><span data-ttu-id="9b0e6-243">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="9b0e6-243">See Also</span></span>
| <span data-ttu-id="9b0e6-244">Rubrique</span><span class="sxs-lookup"><span data-stu-id="9b0e6-244">Topic</span></span> | <span data-ttu-id="9b0e6-245">Description</span><span class="sxs-lookup"><span data-stu-id="9b0e6-245">Description</span></span> |
|:--- |:--- |
| [<span data-ttu-id="9b0e6-246">Pipelines</span><span class="sxs-lookup"><span data-stu-id="9b0e6-246">Pipelines</span></span>](data-factory-create-pipelines.md) |<span data-ttu-id="9b0e6-247">Cet article vous aidera à comprendre les pipelines et les activités dans Azure Data Factory et comment toouse les tooconstruct bout en bout piloté par les données des flux de travail pour votre entreprise ou votre scénario.</span><span class="sxs-lookup"><span data-stu-id="9b0e6-247">This article helps you understand pipelines and activities in Azure Data Factory and how toouse them tooconstruct end-to-end data-driven workflows for your scenario or business.</span></span> |
| [<span data-ttu-id="9b0e6-248">Groupes de données</span><span class="sxs-lookup"><span data-stu-id="9b0e6-248">Datasets</span></span>](data-factory-create-datasets.md) |<span data-ttu-id="9b0e6-249">Cet article vous aide à comprendre les jeux de données dans Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="9b0e6-249">This article helps you understand datasets in Azure Data Factory.</span></span> |
| [<span data-ttu-id="9b0e6-250">Planification et exécution</span><span class="sxs-lookup"><span data-stu-id="9b0e6-250">Scheduling and execution</span></span>](data-factory-scheduling-and-execution.md) |<span data-ttu-id="9b0e6-251">Cet article explique les aspects de planification et l’exécution de hello du modèle d’application Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="9b0e6-251">This article explains hello scheduling and execution aspects of Azure Data Factory application model.</span></span> |
| [<span data-ttu-id="9b0e6-252">Surveiller et gérer les pipelines Azure Data Factory à l’aide de la nouvelle application de surveillance et gestion.</span><span class="sxs-lookup"><span data-stu-id="9b0e6-252">Monitor and manage pipelines using Monitoring App</span></span>](data-factory-monitor-manage-app.md) |<span data-ttu-id="9b0e6-253">Cet article décrit comment toomonitor, gérer et déboguer des pipelines à l’aide de hello analyse & application de gestion.</span><span class="sxs-lookup"><span data-stu-id="9b0e6-253">This article describes how toomonitor, manage, and debug pipelines using hello Monitoring & Management App.</span></span> |

