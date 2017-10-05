---
title: "Créer votre première fabrique de données Azure (modèle Resource Manager) | Microsoft Docs"
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
ms.openlocfilehash: c67169f296f2f13b9ee87180f126fb1dcf10fbea
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-build-your-first-azure-data-factory-using-azure-resource-manager-template"></a><span data-ttu-id="08b1a-103">Didacticiel : concevoir votre première fabrique de données Azure à l’aide du modèle Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="08b1a-103">Tutorial: Build your first Azure data factory using Azure Resource Manager template</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="08b1a-104">Vue d’ensemble et étapes préalables requises</span><span class="sxs-lookup"><span data-stu-id="08b1a-104">Overview and prerequisites</span></span>](data-factory-build-your-first-pipeline.md)
> * [<span data-ttu-id="08b1a-105">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="08b1a-105">Azure portal</span></span>](data-factory-build-your-first-pipeline-using-editor.md)
> * [<span data-ttu-id="08b1a-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="08b1a-106">Visual Studio</span></span>](data-factory-build-your-first-pipeline-using-vs.md)
> * [<span data-ttu-id="08b1a-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="08b1a-107">PowerShell</span></span>](data-factory-build-your-first-pipeline-using-powershell.md)
> * [<span data-ttu-id="08b1a-108">Modèle Resource Manager</span><span class="sxs-lookup"><span data-stu-id="08b1a-108">Resource Manager Template</span></span>](data-factory-build-your-first-pipeline-using-arm.md)
> * [<span data-ttu-id="08b1a-109">API REST</span><span class="sxs-lookup"><span data-stu-id="08b1a-109">REST API</span></span>](data-factory-build-your-first-pipeline-using-rest-api.md)
> 
> 

<span data-ttu-id="08b1a-110">Dans cet article, vous utilisez un modèle Azure Resource Manager pour créer votre première fabrique de données Azure.</span><span class="sxs-lookup"><span data-stu-id="08b1a-110">In this article, you use an Azure Resource Manager template to create your first Azure data factory.</span></span> <span data-ttu-id="08b1a-111">Pour suivre le didacticiel avec d’autres outils/Kits de développement logiciel (SDK), sélectionnez une des options dans la liste déroulante.</span><span class="sxs-lookup"><span data-stu-id="08b1a-111">To do the tutorial using other tools/SDKs, select one of the options from the drop-down list.</span></span>

<span data-ttu-id="08b1a-112">Le pipeline dans ce didacticiel a une activité : **Activité HDInsight Hive**.</span><span class="sxs-lookup"><span data-stu-id="08b1a-112">The pipeline in this tutorial has one activity: **HDInsight Hive activity**.</span></span> <span data-ttu-id="08b1a-113">Cette activité exécute un script Hive sur un cluster HDInsight qui transforme des données d’entrée pour produire des données de sortie.</span><span class="sxs-lookup"><span data-stu-id="08b1a-113">This activity runs a hive script on an Azure HDInsight cluster that transforms input data to produce output data.</span></span> <span data-ttu-id="08b1a-114">Le pipeline est programmé pour s’exécuter une fois par mois entre les heures de début et de fin spécifiées.</span><span class="sxs-lookup"><span data-stu-id="08b1a-114">The pipeline is scheduled to run once a month between the specified start and end times.</span></span> 

> [!NOTE]
> <span data-ttu-id="08b1a-115">Dans ce didacticiel, le pipeline de données transforme les données d’entrée pour produire des données de sortie.</span><span class="sxs-lookup"><span data-stu-id="08b1a-115">The data pipeline in this tutorial transforms input data to produce output data.</span></span> <span data-ttu-id="08b1a-116">Pour un didacticiel sur la copie de données à l’aide d’Azure Data Factory, consultez [Copie de données Blob Storage vers une base de données SQL à l’aide de Data Factory](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="08b1a-116">For a tutorial on how to copy data using Azure Data Factory, see [Tutorial: Copy data from Blob Storage to SQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
> 
> <span data-ttu-id="08b1a-117">Le pipeline dans ce didacticiel a une seule activité de type : HDInsightHive.</span><span class="sxs-lookup"><span data-stu-id="08b1a-117">The pipeline in this tutorial has only one activity of type: HDInsightHive.</span></span> <span data-ttu-id="08b1a-118">Un pipeline peut contenir plusieurs activités.</span><span class="sxs-lookup"><span data-stu-id="08b1a-118">A pipeline can have more than one activity.</span></span> <span data-ttu-id="08b1a-119">En outre, vous pouvez chaîner deux activités (une après l’autre) en configurant le jeu de données de sortie d’une activité en tant que jeu de données d’entrée de l’autre activité.</span><span class="sxs-lookup"><span data-stu-id="08b1a-119">And, you can chain two activities (run one activity after another) by setting the output dataset of one activity as the input dataset of the other activity.</span></span> <span data-ttu-id="08b1a-120">Pour plus d’informations, consultez [Planification et exécution dans Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span><span class="sxs-lookup"><span data-stu-id="08b1a-120">For more information, see [scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="08b1a-121">Composants requis</span><span class="sxs-lookup"><span data-stu-id="08b1a-121">Prerequisites</span></span>
* <span data-ttu-id="08b1a-122">Lisez l’article [Vue d’ensemble du didacticiel](data-factory-build-your-first-pipeline.md) et effectuez les **étapes préalables requises** .</span><span class="sxs-lookup"><span data-stu-id="08b1a-122">Read through [Tutorial Overview](data-factory-build-your-first-pipeline.md) article and complete the **prerequisite** steps.</span></span>
* <span data-ttu-id="08b1a-123">Suivez les instructions de l’article [Installation et configuration d’Azure PowerShell](/powershell/azure/overview) pour installer la dernière version d’Azure PowerShell sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="08b1a-123">Follow instructions in [How to install and configure Azure PowerShell](/powershell/azure/overview) article to install latest version of Azure PowerShell on your computer.</span></span>
* <span data-ttu-id="08b1a-124">Consultez [Création de modèles Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) pour en savoir plus sur les modèles Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="08b1a-124">See [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md) to learn about Azure Resource Manager templates.</span></span> 

## <a name="in-this-tutorial"></a><span data-ttu-id="08b1a-125">Dans ce didacticiel</span><span class="sxs-lookup"><span data-stu-id="08b1a-125">In this tutorial</span></span>
| <span data-ttu-id="08b1a-126">Entité</span><span class="sxs-lookup"><span data-stu-id="08b1a-126">Entity</span></span> | <span data-ttu-id="08b1a-127">Description</span><span class="sxs-lookup"><span data-stu-id="08b1a-127">Description</span></span> |
| --- | --- |
| <span data-ttu-id="08b1a-128">Service lié Azure Storage</span><span class="sxs-lookup"><span data-stu-id="08b1a-128">Azure Storage linked service</span></span> |<span data-ttu-id="08b1a-129">Lie votre compte Stockage Azure à la fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="08b1a-129">Links your Azure Storage account to the data factory.</span></span> <span data-ttu-id="08b1a-130">Le compte Stockage Azure contient les données d’entrée et de sortie pour le pipeline de cet exemple.</span><span class="sxs-lookup"><span data-stu-id="08b1a-130">The Azure Storage account holds the input and output data for the pipeline in this sample.</span></span> |
| <span data-ttu-id="08b1a-131">Service lié à la demande HDInsight</span><span class="sxs-lookup"><span data-stu-id="08b1a-131">HDInsight on-demand linked service</span></span> |<span data-ttu-id="08b1a-132">Lie un cluster HDInsight à la demande à la fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="08b1a-132">Links an on-demand HDInsight cluster to the data factory.</span></span> <span data-ttu-id="08b1a-133">Le cluster est automatiquement créé pour traiter les données puis est supprimé une fois le traitement terminé.</span><span class="sxs-lookup"><span data-stu-id="08b1a-133">The cluster is automatically created for you to process data and is deleted after the processing is done.</span></span> |
| <span data-ttu-id="08b1a-134">Jeu de données d'entrée d'objet Blob Azure</span><span class="sxs-lookup"><span data-stu-id="08b1a-134">Azure Blob input dataset</span></span> |<span data-ttu-id="08b1a-135">Fait référence au service Stockage Azure lié.</span><span class="sxs-lookup"><span data-stu-id="08b1a-135">Refers to the Azure Storage linked service.</span></span> <span data-ttu-id="08b1a-136">Le service lié fait référence à un compte de stockage Azure, et les jeux de données d’objet Blob Azure spécifie le conteneur, le dossier et le nom de fichier dans le stockage contenant les données d’entrée.</span><span class="sxs-lookup"><span data-stu-id="08b1a-136">The linked service refers to an Azure Storage account and the Azure Blob dataset specifies the container, folder, and file name in the storage that holds the input data.</span></span> |
| <span data-ttu-id="08b1a-137">Jeu de données de sortie d’objet Blob Azure</span><span class="sxs-lookup"><span data-stu-id="08b1a-137">Azure Blob output dataset</span></span> |<span data-ttu-id="08b1a-138">Fait référence au service Stockage Azure lié.</span><span class="sxs-lookup"><span data-stu-id="08b1a-138">Refers to the Azure Storage linked service.</span></span> <span data-ttu-id="08b1a-139">Le service lié fait référence à un compte de stockage Azure, et les jeux de données d’objet Blob Azure spécifie le conteneur, le dossier et le nom de fichier dans le stockage contenant les données de sortie.</span><span class="sxs-lookup"><span data-stu-id="08b1a-139">The linked service refers to an Azure Storage account and the Azure Blob dataset specifies the container, folder, and file name in the storage that holds the output data.</span></span> |
| <span data-ttu-id="08b1a-140">Pipeline de données</span><span class="sxs-lookup"><span data-stu-id="08b1a-140">Data pipeline</span></span> |<span data-ttu-id="08b1a-141">Le pipeline exerce une activité de type HDInsightHive, utilise le jeu de données d’entrée et génère le jeu de données de sortie.</span><span class="sxs-lookup"><span data-stu-id="08b1a-141">The pipeline has one activity of type HDInsightHive, which consumes the input dataset and produces the output dataset.</span></span> |

<span data-ttu-id="08b1a-142">Une fabrique de données peut avoir un ou plusieurs pipelines.</span><span class="sxs-lookup"><span data-stu-id="08b1a-142">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="08b1a-143">Un pipeline peut contenir une ou plusieurs activités.</span><span class="sxs-lookup"><span data-stu-id="08b1a-143">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="08b1a-144">Il existe deux types d’activités : les [activités de déplacement des données](data-factory-data-movement-activities.md) et les [activités de transformation des données](data-factory-data-transformation-activities.md).</span><span class="sxs-lookup"><span data-stu-id="08b1a-144">There are two types of activities: [data movement activities](data-factory-data-movement-activities.md) and [data transformation activities](data-factory-data-transformation-activities.md).</span></span> <span data-ttu-id="08b1a-145">Dans ce didacticiel, vous créez un pipeline avec une activité (activité Hive).</span><span class="sxs-lookup"><span data-stu-id="08b1a-145">In this tutorial, you create a pipeline with one activity (Hive activity).</span></span>

<span data-ttu-id="08b1a-146">La section suivante fournit le modèle Resource Manager complet permettant de définir des entités Data Factory pour que vous puissiez rapidement parcourir le didacticiel et tester le modèle.</span><span class="sxs-lookup"><span data-stu-id="08b1a-146">The following section provides the complete Resource Manager template for defining Data Factory entities so that you can quickly run through the tutorial and test the template.</span></span> <span data-ttu-id="08b1a-147">Pour comprendre comment chaque entité Data Factory est définie, consultez la section [Entités Data Factory dans le modèle](#data-factory-entities-in-the-template).</span><span class="sxs-lookup"><span data-stu-id="08b1a-147">To understand how each Data Factory entity is defined, see [Data Factory entities in the template](#data-factory-entities-in-the-template) section.</span></span>

## <a name="data-factory-json-template"></a><span data-ttu-id="08b1a-148">Modèle JSON Data Factory</span><span class="sxs-lookup"><span data-stu-id="08b1a-148">Data Factory JSON template</span></span>
<span data-ttu-id="08b1a-149">Le modèle Resource Manager de niveau supérieur pour la définition d’une fabrique de données est :</span><span class="sxs-lookup"><span data-stu-id="08b1a-149">The top-level Resource Manager template for defining a data factory is:</span></span> 

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
<span data-ttu-id="08b1a-150">Créez un fichier JSON nommé **ADFTutorialARM.json** dans le dossier **C:\ADFGetStarted** avec le contenu suivant :</span><span class="sxs-lookup"><span data-stu-id="08b1a-150">Create a JSON file named **ADFTutorialARM.json** in **C:\ADFGetStarted** folder with the following content:</span></span>

```json
{
    "contentVersion": "1.0.0.0",
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "parameters": {
        "storageAccountName": { "type": "string", "metadata": { "description": "Name of the Azure storage account that contains the input/output data." } },
          "storageAccountKey": { "type": "securestring", "metadata": { "description": "Key for the Azure storage account." } },
          "blobContainer": { "type": "string", "metadata": { "description": "Name of the blob container in the Azure Storage account." } },
          "inputBlobFolder": { "type": "string", "metadata": { "description": "The folder in the blob container that has the input file." } },
          "inputBlobName": { "type": "string", "metadata": { "description": "Name of the input file/blob." } },
          "outputBlobFolder": { "type": "string", "metadata": { "description": "The folder in the blob container that will hold the transformed data." } },
          "hiveScriptFolder": { "type": "string", "metadata": { "description": "The folder in the blob container that contains the Hive query file." } },
          "hiveScriptFile": { "type": "string", "metadata": { "description": "Name of the hive query (HQL) file." } }
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
> <span data-ttu-id="08b1a-151">Vous trouverez un autre exemple de modèle Resource Manager pour créer une fabrique de données Azure dans le [didacticiel : Créer un pipeline avec activité de copie à l’aide d’un modèle Azure Resource Manager](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md).</span><span class="sxs-lookup"><span data-stu-id="08b1a-151">You can find another example of Resource Manager template for creating an Azure data factory on [Tutorial: Create a pipeline with Copy Activity using an Azure Resource Manager template](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md).</span></span>  
> 
> 

## <a name="parameters-json"></a><span data-ttu-id="08b1a-152">Paramètres JSON</span><span class="sxs-lookup"><span data-stu-id="08b1a-152">Parameters JSON</span></span>
<span data-ttu-id="08b1a-153">Créez un fichier JSON nommé **ADFTutorialARM-Parameters** contient les paramètres du modèle Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="08b1a-153">Create a JSON file named **ADFTutorialARM-Parameters.json** that contains parameters for the Azure Resource Manager template.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="08b1a-154">Spécifiez le nom et la clé de votre compte Stockage Azure pour les paramètres **storageAccountName** et **storageAccountKey** dans ce fichier de paramètres.</span><span class="sxs-lookup"><span data-stu-id="08b1a-154">Specify the name and key of your Azure Storage account for the **storageAccountName** and **storageAccountKey** parameters in this parameter file.</span></span> 
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
> <span data-ttu-id="08b1a-155">Vous pouvez utiliser des fichiers JSON de paramètres distincts pour les environnements de développement, de test et de production avec le même modèle JSON Data Factory.</span><span class="sxs-lookup"><span data-stu-id="08b1a-155">You may have separate parameter JSON files for development, testing, and production environments that you can use with the same Data Factory JSON template.</span></span> <span data-ttu-id="08b1a-156">En utilisant un script PowerShell, vous pouvez automatiser le déploiement des entités Data Factory dans ces environnements.</span><span class="sxs-lookup"><span data-stu-id="08b1a-156">By using a Power Shell script, you can automate deploying Data Factory entities in these environments.</span></span> 
> 
> 

## <a name="create-data-factory"></a><span data-ttu-id="08b1a-157">Créer une fabrique de données</span><span class="sxs-lookup"><span data-stu-id="08b1a-157">Create data factory</span></span>
1. <span data-ttu-id="08b1a-158">Démarrez **Azure PowerShell** et exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="08b1a-158">Start **Azure PowerShell** and run the following command:</span></span> 
   * <span data-ttu-id="08b1a-159">Exécutez la commande suivante, puis saisissez le nom d’utilisateur et le mot de passe que vous avez utilisés pour la connexion au portail Azure.</span><span class="sxs-lookup"><span data-stu-id="08b1a-159">Run the following command and enter the user name and password that you use to sign in to the Azure portal.</span></span>
    ```PowerShell
    Login-AzureRmAccount
    ```  
   * <span data-ttu-id="08b1a-160">Exécutez la commande suivante pour afficher tous les abonnements de ce compte.</span><span class="sxs-lookup"><span data-stu-id="08b1a-160">Run the following command to view all the subscriptions for this account.</span></span>
    ```PowerShell
    Get-AzureRmSubscription
    ``` 
   * <span data-ttu-id="08b1a-161">Exécutez la commande suivante pour sélectionner l’abonnement que vous souhaitez utiliser.</span><span class="sxs-lookup"><span data-stu-id="08b1a-161">Run the following command to select the subscription that you want to work with.</span></span> <span data-ttu-id="08b1a-162">Cet abonnement doit être identique à celui utilisé dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="08b1a-162">This subscription should be the same as the one you used in the Azure portal.</span></span>
    ```
    Get-AzureRmSubscription -SubscriptionName <SUBSCRIPTION NAME> | Set-AzureRmContext
    ```   
2. <span data-ttu-id="08b1a-163">Exécutez la commande suivante pour déployer des entités Data Factory à l’aide du modèle Resource Manager que vous avez créé à l’étape 1.</span><span class="sxs-lookup"><span data-stu-id="08b1a-163">Run the following command to deploy Data Factory entities using the Resource Manager template you created in Step 1.</span></span> 

    ```PowerShell
    New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile C:\ADFGetStarted\ADFTutorialARM.json -TemplateParameterFile C:\ADFGetStarted\ADFTutorialARM-Parameters.json
    ```

## <a name="monitor-pipeline"></a><span data-ttu-id="08b1a-164">Surveillance d’un pipeline</span><span class="sxs-lookup"><span data-stu-id="08b1a-164">Monitor pipeline</span></span>
1. <span data-ttu-id="08b1a-165">Après la connexion au [portail Azure](https://portal.azure.com/), cliquez sur **Parcourir** et sélectionnez **Fabriques de données**.</span><span class="sxs-lookup"><span data-stu-id="08b1a-165">After logging in to the [Azure portal](https://portal.azure.com/), Click **Browse** and select **Data factories**.</span></span>
     <span data-ttu-id="08b1a-166">![Parcourir->Fabriques de données](./media/data-factory-build-your-first-pipeline-using-arm/BrowseDataFactories.png)</span><span class="sxs-lookup"><span data-stu-id="08b1a-166">![Browse->Data factories](./media/data-factory-build-your-first-pipeline-using-arm/BrowseDataFactories.png)</span></span>
2. <span data-ttu-id="08b1a-167">Dans le panneau **Fabriques de données**, cliquez sur la fabrique de données (**TutorialFactoryARM**) que vous avez créée.</span><span class="sxs-lookup"><span data-stu-id="08b1a-167">In the **Data Factories** blade, click the data factory (**TutorialFactoryARM**) you created.</span></span>    
3. <span data-ttu-id="08b1a-168">Dans le panneau **Fabrique de données** de votre fabrique de données, cliquez sur **Diagramme**.</span><span class="sxs-lookup"><span data-stu-id="08b1a-168">In the **Data Factory** blade for your data factory, click **Diagram**.</span></span>

     ![Vignette du diagramme](./media/data-factory-build-your-first-pipeline-using-arm/DiagramTile.png)
4. <span data-ttu-id="08b1a-170">Dans la **Vue de diagramme**, une vue d’ensemble des pipelines et des jeux de données utilisés dans ce didacticiel s’affiche.</span><span class="sxs-lookup"><span data-stu-id="08b1a-170">In the **Diagram View**, you see an overview of the pipelines, and datasets used in this tutorial.</span></span>
   
   ![Vue de diagramme](./media/data-factory-build-your-first-pipeline-using-arm/DiagramView.png) 
5. <span data-ttu-id="08b1a-172">Dans la vue de diagramme, double-cliquez sur le jeu de données **AzureBlobOutput**.</span><span class="sxs-lookup"><span data-stu-id="08b1a-172">In the Diagram View, double-click the dataset **AzureBlobOutput**.</span></span> <span data-ttu-id="08b1a-173">La tranche est en cours de traitement.</span><span class="sxs-lookup"><span data-stu-id="08b1a-173">You see that the slice that is currently being processed.</span></span>
   
    ![Jeu de données](./media/data-factory-build-your-first-pipeline-using-arm/AzureBlobOutput.png)
6. <span data-ttu-id="08b1a-175">Quand le traitement est terminé, l’état de la tranche est **Prêt** .</span><span class="sxs-lookup"><span data-stu-id="08b1a-175">When processing is done, you see the slice in **Ready** state.</span></span> <span data-ttu-id="08b1a-176">La création d’un cluster HDInsight à la demande prend généralement un certain temps (environ 20 minutes).</span><span class="sxs-lookup"><span data-stu-id="08b1a-176">Creation of an on-demand HDInsight cluster usually takes sometime (approximately 20 minutes).</span></span> <span data-ttu-id="08b1a-177">Le pipeline devrait donc traiter la tranche en **30 minutes environ** .</span><span class="sxs-lookup"><span data-stu-id="08b1a-177">Therefore, expect the pipeline to take **approximately 30 minutes** to process the slice.</span></span>
   
    ![Jeu de données](./media/data-factory-build-your-first-pipeline-using-arm/SliceReady.png)    
7. <span data-ttu-id="08b1a-179">Quand l’état du segment est **Prêt**, vérifiez la présence des données de sortie dans le dossier **partitioneddata** du conteneur **adfgetstarted** de votre stockage d’objets blob.</span><span class="sxs-lookup"><span data-stu-id="08b1a-179">When the slice is in **Ready** state, check the **partitioneddata** folder in the **adfgetstarted** container in your blob storage for the output data.</span></span>  

<span data-ttu-id="08b1a-180">Consultez [Surveiller les jeux de données et le pipeline](data-factory-monitor-manage-pipelines.md) pour obtenir des instructions sur l’utilisation des panneaux du portail Azure afin de surveiller le pipeline et les jeux de données que vous avez créés dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="08b1a-180">See [Monitor datasets and pipeline](data-factory-monitor-manage-pipelines.md) for instructions on how to use the Azure portal blades to monitor the pipeline and datasets you have created in this tutorial.</span></span>

<span data-ttu-id="08b1a-181">Vous pouvez également utiliser l’application Surveillance et gestion pour surveiller vos pipelines de données.</span><span class="sxs-lookup"><span data-stu-id="08b1a-181">You can also use Monitor and Manage App to monitor your data pipelines.</span></span> <span data-ttu-id="08b1a-182">Pour en savoir plus sur l’utilisation de l’application, consultez l’article [Surveiller et gérer les pipelines Azure Data Factory à l’aide de la nouvelle application de surveillance et gestion](data-factory-monitor-manage-app.md) .</span><span class="sxs-lookup"><span data-stu-id="08b1a-182">See [Monitor and manage Azure Data Factory pipelines using Monitoring App](data-factory-monitor-manage-app.md) for details about using the application.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="08b1a-183">Le fichier d’entrée sera supprimé lorsque la tranche est traitée avec succès.</span><span class="sxs-lookup"><span data-stu-id="08b1a-183">The input file gets deleted when the slice is processed successfully.</span></span> <span data-ttu-id="08b1a-184">Par conséquent, si vous souhaitez réexécuter la tranche ou refaire le didacticiel, chargez le fichier d’entrée (input.log) dans le dossier inputdata du conteneur adfgetstarted.</span><span class="sxs-lookup"><span data-stu-id="08b1a-184">Therefore, if you want to rerun the slice or do the tutorial again, upload the input file (input.log) to the inputdata folder of the adfgetstarted container.</span></span>
> 
> 

## <a name="data-factory-entities-in-the-template"></a><span data-ttu-id="08b1a-185">Entités Data Factory dans le modèle</span><span class="sxs-lookup"><span data-stu-id="08b1a-185">Data Factory entities in the template</span></span>
### <a name="define-data-factory"></a><span data-ttu-id="08b1a-186">Définir une fabrique de données</span><span class="sxs-lookup"><span data-stu-id="08b1a-186">Define data factory</span></span>
<span data-ttu-id="08b1a-187">Vous définissez une fabrique de données dans le modèle Resource Manager, comme indiqué dans l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="08b1a-187">You define a data factory in the Resource Manager template as shown in the following sample:</span></span>  

```json
"resources": [
{
    "name": "[variables('dataFactoryName')]",
    "apiVersion": "2015-10-01",
    "type": "Microsoft.DataFactory/datafactories",
    "location": "West US"
}
```
<span data-ttu-id="08b1a-188">La propriété dataFactoryName est défini en tant que :</span><span class="sxs-lookup"><span data-stu-id="08b1a-188">The dataFactoryName is defined as:</span></span> 

```json
"dataFactoryName": "[concat('HiveTransformDF', uniqueString(resourceGroup().id))]",
```
<span data-ttu-id="08b1a-189">Il s’agit d’une chaîne unique basée sur l’ID du groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="08b1a-189">It is a unique string based on the resource group ID.</span></span>  

### <a name="defining-data-factory-entities"></a><span data-ttu-id="08b1a-190">Définition des entités Data Factory</span><span class="sxs-lookup"><span data-stu-id="08b1a-190">Defining Data Factory entities</span></span>
<span data-ttu-id="08b1a-191">Les entités Data Factory suivantes sont définies dans le modèle JSON :</span><span class="sxs-lookup"><span data-stu-id="08b1a-191">The following Data Factory entities are defined in the JSON template:</span></span> 

* [<span data-ttu-id="08b1a-192">Service lié Azure Storage</span><span class="sxs-lookup"><span data-stu-id="08b1a-192">Azure Storage linked service</span></span>](#azure-storage-linked-service)
* [<span data-ttu-id="08b1a-193">Service lié à la demande HDInsight</span><span class="sxs-lookup"><span data-stu-id="08b1a-193">HDInsight on-demand linked service</span></span>](#hdinsight-on-demand-linked-service)
* [<span data-ttu-id="08b1a-194">Jeu de données d'entrée d'objet Blob Azure</span><span class="sxs-lookup"><span data-stu-id="08b1a-194">Azure blob input dataset</span></span>](#azure-blob-input-dataset)
* [<span data-ttu-id="08b1a-195">Jeu de données de sortie d’objet Blob Azure</span><span class="sxs-lookup"><span data-stu-id="08b1a-195">Azure blob output dataset</span></span>](#azure-blob-output-dataset)
* [<span data-ttu-id="08b1a-196">Pipeline de données avec une activité de copie</span><span class="sxs-lookup"><span data-stu-id="08b1a-196">Data pipeline with a copy activity</span></span>](#data-pipeline)

#### <a name="azure-storage-linked-service"></a><span data-ttu-id="08b1a-197">Service lié Azure Storage</span><span class="sxs-lookup"><span data-stu-id="08b1a-197">Azure Storage linked service</span></span>
<span data-ttu-id="08b1a-198">Vous spécifiez le nom et la clé de votre compte Stockage Azure dans cette section.</span><span class="sxs-lookup"><span data-stu-id="08b1a-198">You specify the name and key of your Azure storage account in this section.</span></span> <span data-ttu-id="08b1a-199">Consultez [Service lié Stockage Azure](data-factory-azure-blob-connector.md#azure-storage-linked-service) pour en savoir plus sur les propriétés JSON utilisées pour définir un service lié Stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="08b1a-199">See [Azure Storage linked service](data-factory-azure-blob-connector.md#azure-storage-linked-service) for details about JSON properties used to define an Azure Storage linked service.</span></span> 

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
<span data-ttu-id="08b1a-200">La propriété **connectionString** utilise les paramètres storageAccountName et storageAccountKey.</span><span class="sxs-lookup"><span data-stu-id="08b1a-200">The **connectionString** uses the storageAccountName and storageAccountKey parameters.</span></span> <span data-ttu-id="08b1a-201">Les valeurs de ces paramètres sont transmises à l’aide d’un fichier de configuration.</span><span class="sxs-lookup"><span data-stu-id="08b1a-201">The values for these parameters passed by using a configuration file.</span></span> <span data-ttu-id="08b1a-202">La définition utilise également les variables azureStroageLinkedService et dataFactoryName, définies dans le modèle.</span><span class="sxs-lookup"><span data-stu-id="08b1a-202">The definition also uses variables: azureStroageLinkedService and dataFactoryName defined in the template.</span></span> 

#### <a name="hdinsight-on-demand-linked-service"></a><span data-ttu-id="08b1a-203">Service lié à la demande HDInsight</span><span class="sxs-lookup"><span data-stu-id="08b1a-203">HDInsight on-demand linked service</span></span>
<span data-ttu-id="08b1a-204">Consultez l’article [Services liés de calcul](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) pour en savoir plus sur les propriétés JSON utilisées pour définir un service lié à la demande HDInsight.</span><span class="sxs-lookup"><span data-stu-id="08b1a-204">See [Compute linked services](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) article for details about JSON properties used to define an HDInsight on-demand linked service.</span></span>  

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
<span data-ttu-id="08b1a-205">Notez les points suivants :</span><span class="sxs-lookup"><span data-stu-id="08b1a-205">Note the following points:</span></span> 

* <span data-ttu-id="08b1a-206">La fabrique de données crée pour vous un cluster HDInsight **Linux** avec le code JSON ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="08b1a-206">The Data Factory creates a **Linux-based** HDInsight cluster for you with the above JSON.</span></span> <span data-ttu-id="08b1a-207">Pour plus d’informations, voir [Service lié à la demande Azure HDInsight](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) .</span><span class="sxs-lookup"><span data-stu-id="08b1a-207">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span> 
* <span data-ttu-id="08b1a-208">Vous pouvez utiliser votre **propre cluster HDInsight** au lieu d’utiliser un cluster HDInsight à la demande.</span><span class="sxs-lookup"><span data-stu-id="08b1a-208">You could use **your own HDInsight cluster** instead of using an on-demand HDInsight cluster.</span></span> <span data-ttu-id="08b1a-209">Pour plus d’informations, voir [Service lié Azure HDInsight](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) .</span><span class="sxs-lookup"><span data-stu-id="08b1a-209">See [HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) for details.</span></span>
* <span data-ttu-id="08b1a-210">Le cluster HDInsight crée un **conteneur par défaut** dans le stockage d’objets blob que vous avez spécifié dans le JSON (**linkedServiceName**).</span><span class="sxs-lookup"><span data-stu-id="08b1a-210">The HDInsight cluster creates a **default container** in the blob storage you specified in the JSON (**linkedServiceName**).</span></span> <span data-ttu-id="08b1a-211">HDInsight ne supprime pas ce conteneur lorsque le cluster est supprimé.</span><span class="sxs-lookup"><span data-stu-id="08b1a-211">HDInsight does not delete this container when the cluster is deleted.</span></span> <span data-ttu-id="08b1a-212">Ce comportement est normal.</span><span class="sxs-lookup"><span data-stu-id="08b1a-212">This behavior is by design.</span></span> <span data-ttu-id="08b1a-213">Avec le service lié HDInsight à la demande, un cluster HDInsight est créé à chaque fois qu’une tranche doit être traitée, à moins qu’il n’existe un cluster activé (**timeToLive**), et est supprimé une fois le traitement activé.</span><span class="sxs-lookup"><span data-stu-id="08b1a-213">With on-demand HDInsight linked service, a HDInsight cluster is created every time a slice needs to be processed unless there is an existing live cluster (**timeToLive**) and is deleted when the processing is done.</span></span>
  
    <span data-ttu-id="08b1a-214">Comme un nombre croissant de tranches sont traitées, vous voyez un grand nombre de conteneurs dans votre stockage d’objets blob Azure.</span><span class="sxs-lookup"><span data-stu-id="08b1a-214">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="08b1a-215">Si vous n’en avez pas besoin pour dépanner les travaux, il se peut que vous deviez les supprimer pour réduire les frais de stockage.</span><span class="sxs-lookup"><span data-stu-id="08b1a-215">If you do not need them for troubleshooting of the jobs, you may want to delete them to reduce the storage cost.</span></span> <span data-ttu-id="08b1a-216">Le nom de ces conteneurs suit un modèle : « **nomdevotrefabriquededonnéesadf**-**nomduservicelié**-horodatage ».</span><span class="sxs-lookup"><span data-stu-id="08b1a-216">The names of these containers follow a pattern: "adf**yourdatafactoryname**-**linkedservicename**-datetimestamp".</span></span> <span data-ttu-id="08b1a-217">Utilisez des outils tels que [Microsoft Storage Explorer](http://storageexplorer.com/) pour supprimer des conteneurs dans votre stockage d’objets blob Azure.</span><span class="sxs-lookup"><span data-stu-id="08b1a-217">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) to delete containers in your Azure blob storage.</span></span>

<span data-ttu-id="08b1a-218">Pour plus d’informations, voir [Service lié à la demande Azure HDInsight](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) .</span><span class="sxs-lookup"><span data-stu-id="08b1a-218">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>

#### <a name="azure-blob-input-dataset"></a><span data-ttu-id="08b1a-219">Jeu de données d'entrée d'objet Blob Azure</span><span class="sxs-lookup"><span data-stu-id="08b1a-219">Azure blob input dataset</span></span>
<span data-ttu-id="08b1a-220">Vous spécifiez les noms du conteneur d’objets blob, du dossier et du fichier contenant les données d’entrée.</span><span class="sxs-lookup"><span data-stu-id="08b1a-220">You specify the names of blob container, folder, and file that contains the input data.</span></span> <span data-ttu-id="08b1a-221">Consultez [Propriétés du jeu de données d’objet blob Azure](data-factory-azure-blob-connector.md#dataset-properties) pour en savoir plus sur les propriétés JSON permettant de définir un jeu de données d’objets blob Azure.</span><span class="sxs-lookup"><span data-stu-id="08b1a-221">See [Azure Blob dataset properties](data-factory-azure-blob-connector.md#dataset-properties) for details about JSON properties used to define an Azure Blob dataset.</span></span> 

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
<span data-ttu-id="08b1a-222">Cette définition utilise les paramètres suivants, définis dans le modèle de paramètre : blobContainer, inputBlobFolder et inputBlobName.</span><span class="sxs-lookup"><span data-stu-id="08b1a-222">This definition uses the following parameters defined in parameter template: blobContainer, inputBlobFolder, and inputBlobName.</span></span> 

#### <a name="azure-blob-output-dataset"></a><span data-ttu-id="08b1a-223">Jeu de données de sortie d’objet Blob Azure</span><span class="sxs-lookup"><span data-stu-id="08b1a-223">Azure Blob output dataset</span></span>
<span data-ttu-id="08b1a-224">Vous spécifiez les noms du conteneur d’objets blob et du dossier contenant les données de sortie.</span><span class="sxs-lookup"><span data-stu-id="08b1a-224">You specify the names of blob container and folder that holds the output data.</span></span> <span data-ttu-id="08b1a-225">Consultez [Propriétés du jeu de données d’objet blob Azure](data-factory-azure-blob-connector.md#dataset-properties) pour en savoir plus sur les propriétés JSON permettant de définir un jeu de données d’objets blob Azure.</span><span class="sxs-lookup"><span data-stu-id="08b1a-225">See [Azure Blob dataset properties](data-factory-azure-blob-connector.md#dataset-properties) for details about JSON properties used to define an Azure Blob dataset.</span></span>  

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

<span data-ttu-id="08b1a-226">Cette définition utilise les paramètres suivants, définis dans le modèle de paramètre : blobContainer and outputBlobFolder.</span><span class="sxs-lookup"><span data-stu-id="08b1a-226">This definition uses the following parameters defined in the parameter template: blobContainer and outputBlobFolder.</span></span> 

#### <a name="data-pipeline"></a><span data-ttu-id="08b1a-227">Pipeline de données</span><span class="sxs-lookup"><span data-stu-id="08b1a-227">Data pipeline</span></span>
<span data-ttu-id="08b1a-228">Vous définissez un pipeline qui transforme les données en exécutant le script Hive sur un cluster Azure HDInsight à la demande.</span><span class="sxs-lookup"><span data-stu-id="08b1a-228">You define a pipeline that transform data by running Hive script on an on-demand Azure HDInsight cluster.</span></span> <span data-ttu-id="08b1a-229">Consultez [Pipeline JSON](data-factory-create-pipelines.md#pipeline-json) pour obtenir des descriptions des éléments JSON permettant de définir un pipeline dans cet exemple.</span><span class="sxs-lookup"><span data-stu-id="08b1a-229">See [Pipeline JSON](data-factory-create-pipelines.md#pipeline-json) for descriptions of JSON elements used to define a pipeline in this example.</span></span> 

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

## <a name="reuse-the-template"></a><span data-ttu-id="08b1a-230">Réutiliser le modèle</span><span class="sxs-lookup"><span data-stu-id="08b1a-230">Reuse the template</span></span>
<span data-ttu-id="08b1a-231">Dans ce didacticiel, vous avez créé un modèle pour définir des entités Data Factory et un modèle pour transmettre les valeurs des paramètres.</span><span class="sxs-lookup"><span data-stu-id="08b1a-231">In the tutorial, you created a template for defining Data Factory entities and a template for passing values for parameters.</span></span> <span data-ttu-id="08b1a-232">Pour utiliser le même modèle afin de déployer des entités Data Factory dans des environnements différents, vous créez un fichier de paramètres pour chaque environnement et l’utiliser lors du déploiement de cet environnement.</span><span class="sxs-lookup"><span data-stu-id="08b1a-232">To use the same template to deploy Data Factory entities to different environments, you create a parameter file for each environment and use it when deploying to that environment.</span></span>     

<span data-ttu-id="08b1a-233">Exemple :</span><span class="sxs-lookup"><span data-stu-id="08b1a-233">Example:</span></span>  

```PowerShell
New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFTutorialARM.json -TemplateParameterFile ADFTutorialARM-Parameters-Dev.json

New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFTutorialARM.json -TemplateParameterFile ADFTutorialARM-Parameters-Test.json

New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFTutorialARM.json -TemplateParameterFile ADFTutorialARM-Parameters-Production.json
```
<span data-ttu-id="08b1a-234">Notez que la première commande utilise le fichier de paramètres pour l’environnement de développement, la deuxième pour l’environnement de test et la troisième pour l’environnement de production.</span><span class="sxs-lookup"><span data-stu-id="08b1a-234">Notice that the first command uses parameter file for the development environment, second one for the test environment, and the third one for the production environment.</span></span>  

<span data-ttu-id="08b1a-235">Vous pouvez également réutiliser le modèle pour effectuer des tâches répétitives.</span><span class="sxs-lookup"><span data-stu-id="08b1a-235">You can also reuse the template to perform repeated tasks.</span></span> <span data-ttu-id="08b1a-236">Par exemple, vous devez créer plusieurs fabriques de données avec un ou plusieurs pipelines qui implémentent la même logique, mais chaque fabrique de données utilise des comptes Stockage Azure et Azure SQL Database différents.</span><span class="sxs-lookup"><span data-stu-id="08b1a-236">For example, you need to create many data factories with one or more pipelines that implement the same logic but each data factory uses different Azure storage and Azure SQL Database accounts.</span></span> <span data-ttu-id="08b1a-237">Dans ce scénario, vous utilisez le même modèle dans le même environnement (développement, test ou production) avec différents fichiers de paramètres pour créer des fabriques de données.</span><span class="sxs-lookup"><span data-stu-id="08b1a-237">In this scenario, you use the same template in the same environment (dev, test, or production) with different parameter files to create data factories.</span></span> 

## <a name="resource-manager-template-for-creating-a-gateway"></a><span data-ttu-id="08b1a-238">Modèle Resource Manager pour la création d’une passerelle</span><span class="sxs-lookup"><span data-stu-id="08b1a-238">Resource Manager template for creating a gateway</span></span>
<span data-ttu-id="08b1a-239">Voici un exemple de modèle Resource Manager pour la création d’une passerelle logique à l’arrière.</span><span class="sxs-lookup"><span data-stu-id="08b1a-239">Here is a sample Resource Manager template for creating a logical gateway in the back.</span></span> <span data-ttu-id="08b1a-240">Installez une passerelle sur votre ordinateur local ou sur une machine virtuelle IaaS Azure et l’enregistrer auprès du service Data Factory à l’aide d’une clé.</span><span class="sxs-lookup"><span data-stu-id="08b1a-240">Install a gateway on your on-premises computer or Azure IaaS VM and register the gateway with Data Factory service using a key.</span></span> <span data-ttu-id="08b1a-241">Pour plus d’informations, consultez [Déplacer des données entre un emplacement local et le cloud](data-factory-move-data-between-onprem-and-cloud.md) .</span><span class="sxs-lookup"><span data-stu-id="08b1a-241">See [Move data between on-premises and cloud](data-factory-move-data-between-onprem-and-cloud.md) for details.</span></span>

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
<span data-ttu-id="08b1a-242">Ce modèle crée une fabrique de données nommée GatewayUsingArmDF avec une passerelle nommée GatewayUsingARM.</span><span class="sxs-lookup"><span data-stu-id="08b1a-242">This template creates a data factory named GatewayUsingArmDF with a gateway named: GatewayUsingARM.</span></span> 

## <a name="see-also"></a><span data-ttu-id="08b1a-243">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="08b1a-243">See Also</span></span>
| <span data-ttu-id="08b1a-244">Rubrique</span><span class="sxs-lookup"><span data-stu-id="08b1a-244">Topic</span></span> | <span data-ttu-id="08b1a-245">Description</span><span class="sxs-lookup"><span data-stu-id="08b1a-245">Description</span></span> |
|:--- |:--- |
| [<span data-ttu-id="08b1a-246">Pipelines</span><span class="sxs-lookup"><span data-stu-id="08b1a-246">Pipelines</span></span>](data-factory-create-pipelines.md) |<span data-ttu-id="08b1a-247">Cet article vous aide à comprendre les pipelines et les activités dans Azure Data Factory, et à les utiliser dans l’optique de créer des workflows pilotés par les données de bout en bout pour votre scénario ou votre entreprise.</span><span class="sxs-lookup"><span data-stu-id="08b1a-247">This article helps you understand pipelines and activities in Azure Data Factory and how to use them to construct end-to-end data-driven workflows for your scenario or business.</span></span> |
| [<span data-ttu-id="08b1a-248">Groupes de données</span><span class="sxs-lookup"><span data-stu-id="08b1a-248">Datasets</span></span>](data-factory-create-datasets.md) |<span data-ttu-id="08b1a-249">Cet article vous aide à comprendre les jeux de données dans Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="08b1a-249">This article helps you understand datasets in Azure Data Factory.</span></span> |
| [<span data-ttu-id="08b1a-250">Planification et exécution</span><span class="sxs-lookup"><span data-stu-id="08b1a-250">Scheduling and execution</span></span>](data-factory-scheduling-and-execution.md) |<span data-ttu-id="08b1a-251">Cet article explique les aspects de la planification et de l’exécution du modèle d’application Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="08b1a-251">This article explains the scheduling and execution aspects of Azure Data Factory application model.</span></span> |
| [<span data-ttu-id="08b1a-252">Surveiller et gérer les pipelines Azure Data Factory à l’aide de la nouvelle application de surveillance et gestion.</span><span class="sxs-lookup"><span data-stu-id="08b1a-252">Monitor and manage pipelines using Monitoring App</span></span>](data-factory-monitor-manage-app.md) |<span data-ttu-id="08b1a-253">Cet article décrit comment surveiller, gérer et déboguer les pipelines à l’aide de l’application de surveillance et gestion.</span><span class="sxs-lookup"><span data-stu-id="08b1a-253">This article describes how to monitor, manage, and debug pipelines using the Monitoring & Management App.</span></span> |

