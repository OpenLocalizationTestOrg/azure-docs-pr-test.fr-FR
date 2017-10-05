---
title: "Didacticiel : Créer un pipeline à l’aide du modèle Azure Resource Manager | Microsoft Docs"
description: "Dans ce didacticiel, vous créez un pipeline Azure Data Factory en utilisant un modèle Azure Resource Manager. Ce pipeline copie des données d’un stockage Blob Azure dans une base de données Azure SQL."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 1274e11a-e004-4df5-af07-850b2de7c15e
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 8a155213ed17e516a5c46abbe3d8a2bcc52268ed
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-use-azure-resource-manager-template-to-create-a-data-factory-pipeline-to-copy-data"></a><span data-ttu-id="1b5c1-104">Didacticiel : Utiliser le modèle Azure Resource Manager pour créer un pipeline Data Factory afin de copier des données</span><span class="sxs-lookup"><span data-stu-id="1b5c1-104">Tutorial: Use Azure Resource Manager template to create a Data Factory pipeline to copy data</span></span> 
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1b5c1-105">Vue d’ensemble et étapes préalables requises</span><span class="sxs-lookup"><span data-stu-id="1b5c1-105">Overview and prerequisites</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [<span data-ttu-id="1b5c1-106">Assistant de copie</span><span class="sxs-lookup"><span data-stu-id="1b5c1-106">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
> * [<span data-ttu-id="1b5c1-107">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="1b5c1-107">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [<span data-ttu-id="1b5c1-108">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1b5c1-108">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [<span data-ttu-id="1b5c1-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1b5c1-109">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
> * [<span data-ttu-id="1b5c1-110">Modèle Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="1b5c1-110">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [<span data-ttu-id="1b5c1-111">API REST</span><span class="sxs-lookup"><span data-stu-id="1b5c1-111">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [<span data-ttu-id="1b5c1-112">API .NET</span><span class="sxs-lookup"><span data-stu-id="1b5c1-112">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)
> 
> 

<span data-ttu-id="1b5c1-113">Ce didacticiel vous montre comment utiliser un modèle Azure Resource Manager pour créer une fabrique de données Azure.</span><span class="sxs-lookup"><span data-stu-id="1b5c1-113">This tutorial shows you how to use an Azure Resource Manager template to create an Azure data factory.</span></span> <span data-ttu-id="1b5c1-114">Dans ce didacticiel, le pipeline de données copie les données d’un magasin de données source vers un magasin de données de destination.</span><span class="sxs-lookup"><span data-stu-id="1b5c1-114">The data pipeline in this tutorial copies data from a source data store to a destination data store.</span></span> <span data-ttu-id="1b5c1-115">Il ne transforme pas les données d’entrée pour produire des données de sortie.</span><span class="sxs-lookup"><span data-stu-id="1b5c1-115">It does not transform input data to produce output data.</span></span> <span data-ttu-id="1b5c1-116">Pour un didacticiel sur la transformation des données à l’aide d’Azure Data Factory, consultez [Tutorial: Build your first pipeline to transform data using Hadoop cluster](data-factory-build-your-first-pipeline.md) (Didacticiel : Créer un pipeline pour transformer des données à l’aide d’un cluster Hadoop).</span><span class="sxs-lookup"><span data-stu-id="1b5c1-116">For a tutorial on how to transform data using Azure Data Factory, see [Tutorial: Build a pipeline to transform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span>

<span data-ttu-id="1b5c1-117">Dans ce didacticiel, vous créez un pipeline avec une activité : activité de copie.</span><span class="sxs-lookup"><span data-stu-id="1b5c1-117">In this tutorial, you create a pipeline with one activity in it: Copy Activity.</span></span> <span data-ttu-id="1b5c1-118">L’activité de copie copie les données d’un magasin de données pris en charge vers un magasin de données de récepteur pris en charge.</span><span class="sxs-lookup"><span data-stu-id="1b5c1-118">The copy activity copies data from a supported data store to a supported sink data store.</span></span> <span data-ttu-id="1b5c1-119">Pour obtenir la liste des magasins de données pris en charge en tant que sources et récepteurs, consultez [Magasins de données pris en charge](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="1b5c1-119">For a list of data stores supported as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="1b5c1-120">Elle est mise en œuvre par un service disponible dans le monde entier, capable de copier des données entre différents magasins de données de façon sécurisée, fiable et évolutive.</span><span class="sxs-lookup"><span data-stu-id="1b5c1-120">The activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="1b5c1-121">Pour plus d’informations sur l’activité de copie, consultez [Activités de déplacement des données](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="1b5c1-121">For more information about the Copy Activity, see [Data Movement Activities](data-factory-data-movement-activities.md).</span></span>

<span data-ttu-id="1b5c1-122">Un pipeline peut contenir plusieurs activités.</span><span class="sxs-lookup"><span data-stu-id="1b5c1-122">A pipeline can have more than one activity.</span></span> <span data-ttu-id="1b5c1-123">En outre, vous pouvez chaîner deux activités (une après l’autre) en configurant le jeu de données de sortie d’une activité en tant que jeu de données d’entrée de l’autre activité.</span><span class="sxs-lookup"><span data-stu-id="1b5c1-123">And, you can chain two activities (run one activity after another) by setting the output dataset of one activity as the input dataset of the other activity.</span></span> <span data-ttu-id="1b5c1-124">Pour plus d’informations, consultez [Plusieurs activités dans un pipeline](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span><span class="sxs-lookup"><span data-stu-id="1b5c1-124">For more information, see [multiple activities in a pipeline](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span> 

> [!NOTE] 
> <span data-ttu-id="1b5c1-125">Dans ce didacticiel, le pipeline de données copie les données d’un magasin de données source vers un magasin de données de destination.</span><span class="sxs-lookup"><span data-stu-id="1b5c1-125">The data pipeline in this tutorial copies data from a source data store to a destination data store.</span></span> <span data-ttu-id="1b5c1-126">Pour un didacticiel sur la transformation des données à l’aide d’Azure Data Factory, consultez [Tutorial: Build your first pipeline to transform data using Hadoop cluster](data-factory-build-your-first-pipeline.md) (Didacticiel : Créer un pipeline pour transformer des données à l’aide d’un cluster Hadoop).</span><span class="sxs-lookup"><span data-stu-id="1b5c1-126">For a tutorial on how to transform data using Azure Data Factory, see [Tutorial: Build a pipeline to transform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="1b5c1-127">Composants requis</span><span class="sxs-lookup"><span data-stu-id="1b5c1-127">Prerequisites</span></span>
* <span data-ttu-id="1b5c1-128">Lisez l’article [Vue d’ensemble et étapes préalables requises](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) et effectuez les **étapes préalables requises**.</span><span class="sxs-lookup"><span data-stu-id="1b5c1-128">Go through [Tutorial Overview and Prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) and complete the **prerequisite** steps.</span></span>
* <span data-ttu-id="1b5c1-129">Suivez les instructions de l’article [Installation et configuration d’Azure PowerShell](/powershell/azure/overview) pour installer la dernière version d’Azure PowerShell sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="1b5c1-129">Follow instructions in [How to install and configure Azure PowerShell](/powershell/azure/overview) article to install latest version of Azure PowerShell on your computer.</span></span> <span data-ttu-id="1b5c1-130">Dans ce didacticiel, vous utilisez PowerShell pour déployer des entités Data Factory.</span><span class="sxs-lookup"><span data-stu-id="1b5c1-130">In this tutorial, you use PowerShell to deploy Data Factory entities.</span></span> 
* <span data-ttu-id="1b5c1-131">(Facultatif) Consultez [Création de modèles Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) pour en savoir plus sur les modèles Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="1b5c1-131">(optional) See [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md) to learn about Azure Resource Manager templates.</span></span>

## <a name="in-this-tutorial"></a><span data-ttu-id="1b5c1-132">Dans ce didacticiel</span><span class="sxs-lookup"><span data-stu-id="1b5c1-132">In this tutorial</span></span>
<span data-ttu-id="1b5c1-133">Dans ce didacticiel, vous créez une fabrique de données avec les entités Data Factory suivantes :</span><span class="sxs-lookup"><span data-stu-id="1b5c1-133">In this tutorial, you create a data factory with the following Data Factory entities:</span></span>

| <span data-ttu-id="1b5c1-134">Entité</span><span class="sxs-lookup"><span data-stu-id="1b5c1-134">Entity</span></span> | <span data-ttu-id="1b5c1-135">Description</span><span class="sxs-lookup"><span data-stu-id="1b5c1-135">Description</span></span> |
| --- | --- |
| <span data-ttu-id="1b5c1-136">Service lié Azure Storage</span><span class="sxs-lookup"><span data-stu-id="1b5c1-136">Azure Storage linked service</span></span> |<span data-ttu-id="1b5c1-137">Lie votre compte Stockage Azure à la fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="1b5c1-137">Links your Azure Storage account to the data factory.</span></span> <span data-ttu-id="1b5c1-138">Stockage Azure est le magasin de données source et la base de données SQL Azure est le magasin de données récepteur de l’activité de copie dans le didacticiel.</span><span class="sxs-lookup"><span data-stu-id="1b5c1-138">Azure Storage is the source data store and Azure SQL database is the sink data store for the copy activity in the tutorial.</span></span> <span data-ttu-id="1b5c1-139">Il spécifie le compte de stockage contenant les données d’entrée pour l’activité de copie.</span><span class="sxs-lookup"><span data-stu-id="1b5c1-139">It specifies the storage account that contains the input data for the copy activity.</span></span> |
| <span data-ttu-id="1b5c1-140">Service lié pour base de données SQL Azure</span><span class="sxs-lookup"><span data-stu-id="1b5c1-140">Azure SQL Database linked service</span></span> |<span data-ttu-id="1b5c1-141">Lie votre base de données SQL Azure à la fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="1b5c1-141">Links your Azure SQL database to the data factory.</span></span> <span data-ttu-id="1b5c1-142">Il spécifie la base de données SQL Azure qui conserve les données de sortie de l’activité de copie.</span><span class="sxs-lookup"><span data-stu-id="1b5c1-142">It specifies the Azure SQL database that holds the output data for the copy activity.</span></span> |
| <span data-ttu-id="1b5c1-143">Jeu de données d'entrée d'objet Blob Azure</span><span class="sxs-lookup"><span data-stu-id="1b5c1-143">Azure Blob input dataset</span></span> |<span data-ttu-id="1b5c1-144">Fait référence au service Stockage Azure lié.</span><span class="sxs-lookup"><span data-stu-id="1b5c1-144">Refers to the Azure Storage linked service.</span></span> <span data-ttu-id="1b5c1-145">Le service lié fait référence à un compte de stockage Azure, et les jeux de données d’objet Blob Azure spécifie le conteneur, le dossier et le nom de fichier dans le stockage contenant les données d’entrée.</span><span class="sxs-lookup"><span data-stu-id="1b5c1-145">The linked service refers to an Azure Storage account and the Azure Blob dataset specifies the container, folder, and file name in the storage that holds the input data.</span></span> |
| <span data-ttu-id="1b5c1-146">Jeu de données de sortie SQL Azure</span><span class="sxs-lookup"><span data-stu-id="1b5c1-146">Azure SQL output dataset</span></span> |<span data-ttu-id="1b5c1-147">Fait référence au service SQL Azure lié.</span><span class="sxs-lookup"><span data-stu-id="1b5c1-147">Refers to the Azure SQL linked service.</span></span> <span data-ttu-id="1b5c1-148">Le service lié SQL Azure fait référence à un serveur SQL Azure et le jeu de données SQL Azure spécifie le nom de la table qui contient les données de sortie.</span><span class="sxs-lookup"><span data-stu-id="1b5c1-148">The Azure SQL linked service refers to an Azure SQL server and the Azure SQL dataset specifies the name of the table that holds the output data.</span></span> |
| <span data-ttu-id="1b5c1-149">Pipeline de données</span><span class="sxs-lookup"><span data-stu-id="1b5c1-149">Data pipeline</span></span> |<span data-ttu-id="1b5c1-150">Le pipeline a une activité de type copie qui sélectionne le jeu de données d’objets blob Azure comme entrée et le jeu de données SQL Azure comme sortie.</span><span class="sxs-lookup"><span data-stu-id="1b5c1-150">The pipeline has one activity of type Copy that takes the Azure blob dataset as an input and the Azure SQL dataset as an output.</span></span> <span data-ttu-id="1b5c1-151">L’activité de copie les données d’un objet blob Azure vers une table dans la base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="1b5c1-151">The copy activity copies data from an Azure blob to a table in the Azure SQL database.</span></span> |

<span data-ttu-id="1b5c1-152">Une fabrique de données peut avoir un ou plusieurs pipelines.</span><span class="sxs-lookup"><span data-stu-id="1b5c1-152">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="1b5c1-153">Un pipeline peut contenir une ou plusieurs activités.</span><span class="sxs-lookup"><span data-stu-id="1b5c1-153">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="1b5c1-154">Il existe deux types d’activités : les [activités de déplacement des données](data-factory-data-movement-activities.md) et les [activités de transformation des données](data-factory-data-transformation-activities.md).</span><span class="sxs-lookup"><span data-stu-id="1b5c1-154">There are two types of activities: [data movement activities](data-factory-data-movement-activities.md) and [data transformation activities](data-factory-data-transformation-activities.md).</span></span> <span data-ttu-id="1b5c1-155">Dans ce didacticiel, vous créez un pipeline avec une activité (activité de copie).</span><span class="sxs-lookup"><span data-stu-id="1b5c1-155">In this tutorial, you create a pipeline with one activity (copy activity).</span></span>

![Copie de données d’un objet blob Azure vers une base de données SQL Azure](media/data-factory-copy-activity-tutorial-using-azure-resource-manager-template/CopyBlob2SqlDiagram.png) 

<span data-ttu-id="1b5c1-157">La section suivante fournit le modèle Resource Manager complet permettant de définir des entités Data Factory pour que vous puissiez rapidement parcourir le didacticiel et tester le modèle.</span><span class="sxs-lookup"><span data-stu-id="1b5c1-157">The following section provides the complete Resource Manager template for defining Data Factory entities so that you can quickly run through the tutorial and test the template.</span></span> <span data-ttu-id="1b5c1-158">Pour comprendre comment chaque entité Data Factory est définie, consultez la section [Entités Data Factory dans le modèle](#data-factory-entities-in-the-template).</span><span class="sxs-lookup"><span data-stu-id="1b5c1-158">To understand how each Data Factory entity is defined, see [Data Factory entities in the template](#data-factory-entities-in-the-template) section.</span></span>

## <a name="data-factory-json-template"></a><span data-ttu-id="1b5c1-159">Modèle JSON Data Factory</span><span class="sxs-lookup"><span data-stu-id="1b5c1-159">Data Factory JSON template</span></span>
<span data-ttu-id="1b5c1-160">Le modèle Resource Manager de niveau supérieur pour la définition d’une fabrique de données est :</span><span class="sxs-lookup"><span data-stu-id="1b5c1-160">The top-level Resource Manager template for defining a data factory is:</span></span> 

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
<span data-ttu-id="1b5c1-161">Créez un fichier JSON nommé **ADFCopyTutorialARM.json** dans le dossier **C:\ADFGetStarted** avec le contenu suivant :</span><span class="sxs-lookup"><span data-stu-id="1b5c1-161">Create a JSON file named **ADFCopyTutorialARM.json** in **C:\ADFGetStarted** folder with the following content:</span></span>

```json
{
    "contentVersion": "1.0.0.0",
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "parameters": {
      "storageAccountName": { "type": "string", "metadata": { "description": "Name of the Azure storage account that contains the data to be copied." } },
      "storageAccountKey": { "type": "securestring", "metadata": { "description": "Key for the Azure storage account." } },
      "sourceBlobContainer": { "type": "string", "metadata": { "description": "Name of the blob container in the Azure Storage account." } },
      "sourceBlobName": { "type": "string", "metadata": { "description": "Name of the blob in the container that has the data to be copied to Azure SQL Database table" } },
      "sqlServerName": { "type": "string", "metadata": { "description": "Name of the Azure SQL Server that will hold the output/copied data." } },
      "databaseName": { "type": "string", "metadata": { "description": "Name of the Azure SQL Database in the Azure SQL server." } },
      "sqlServerUserName": { "type": "string", "metadata": { "description": "Name of the user that has access to the Azure SQL server." } },
      "sqlServerPassword": { "type": "securestring", "metadata": { "description": "Password for the user." } },
      "targetSQLTable": { "type": "string", "metadata": { "description": "Table in the Azure SQL Database that will hold the copied data." } 
      } 
    },
    "variables": {
      "dataFactoryName": "[concat('AzureBlobToAzureSQLDatabaseDF', uniqueString(resourceGroup().id))]",
      "azureSqlLinkedServiceName": "AzureSqlLinkedService",
      "azureStorageLinkedServiceName": "AzureStorageLinkedService",
      "blobInputDatasetName": "BlobInputDataset",
      "sqlOutputDatasetName": "SQLOutputDataset",
      "pipelineName": "Blob2SQLPipeline"
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
            "name": "[variables('azureSqlLinkedServiceName')]",
            "dependsOn": [
              "[variables('dataFactoryName')]"
            ],
            "apiVersion": "2015-10-01",
            "properties": {
              "type": "AzureSqlDatabase",
              "description": "Azure SQL linked service",
              "typeProperties": {
                "connectionString": "[concat('Server=tcp:',parameters('sqlServerName'),'.database.windows.net,1433;Database=', parameters('databaseName'), ';User ID=',parameters('sqlServerUserName'),';Password=',parameters('sqlServerPassword'),';Trusted_Connection=False;Encrypt=True;Connection Timeout=30')]"
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
              "structure": [
                {
                  "name": "Column0",
                  "type": "String"
                },
                {
                  "name": "Column1",
                  "type": "String"
                }
              ],
              "typeProperties": {
                "folderPath": "[concat(parameters('sourceBlobContainer'), '/')]",
                "fileName": "[parameters('sourceBlobName')]",
                "format": {
                  "type": "TextFormat",
                  "columnDelimiter": ","
                }
              },
              "availability": {
                "frequency": "Hour",
                "interval": 1
              },
              "external": true
            }
          },
          {
            "type": "datasets",
            "name": "[variables('sqlOutputDatasetName')]",
            "dependsOn": [
              "[variables('dataFactoryName')]",
              "[variables('azureSqlLinkedServiceName')]"
            ],
            "apiVersion": "2015-10-01",
            "properties": {
              "type": "AzureSqlTable",
              "linkedServiceName": "[variables('azureSqlLinkedServiceName')]",
              "structure": [
                {
                  "name": "FirstName",
                  "type": "String"
                },
                {
                  "name": "LastName",
                  "type": "String"
                }
              ],
              "typeProperties": {
                "tableName": "[parameters('targetSQLTable')]"
              },
              "availability": {
                "frequency": "Hour",
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
              "[variables('azureSqlLinkedServiceName')]",
              "[variables('blobInputDatasetName')]",
              "[variables('sqlOutputDatasetName')]"
            ],
            "apiVersion": "2015-10-01",
            "properties": {
              "activities": [
                {
                  "name": "CopyFromAzureBlobToAzureSQL",
                  "description": "Copy data frm Azure blob to Azure SQL",
                  "type": "Copy",
                  "inputs": [
                    {
                      "name": "[variables('blobInputDatasetName')]"
                    }
                  ],
                  "outputs": [
                    {
                      "name": "[variables('sqlOutputDatasetName')]"
                    }
                  ],
                  "typeProperties": {
                    "source": {
                      "type": "BlobSource"
                    },
                    "sink": {
                      "type": "SqlSink",
                      "sqlWriterCleanupScript": "$$Text.Format('DELETE FROM {0}', 'emp')"
                    },
                    "translator": {
                      "type": "TabularTranslator",
                      "columnMappings": "Column0:FirstName,Column1:LastName"
                    }
                  },
                  "Policy": {
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 3,
                    "timeout": "01:00:00"
                  }
                }
              ],
              "start": "2017-05-11T00:00:00Z",
              "end": "2017-05-12T00:00:00Z"
            }
          }
        ]
      }
    ]
  }
```

## <a name="parameters-json"></a><span data-ttu-id="1b5c1-162">Paramètres JSON</span><span class="sxs-lookup"><span data-stu-id="1b5c1-162">Parameters JSON</span></span>
<span data-ttu-id="1b5c1-163">Créez un fichier JSON nommé **ADFCopyTutorialARM-Parameters** contient les paramètres du modèle Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="1b5c1-163">Create a JSON file named **ADFCopyTutorialARM-Parameters.json** that contains parameters for the Azure Resource Manager template.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="1b5c1-164">Spécifiez le nom et la clé de votre compte de stockage Azure pour les paramètres storageAccountName et storageAccountKey.</span><span class="sxs-lookup"><span data-stu-id="1b5c1-164">Specify name and key of your Azure Storage account for storageAccountName and storageAccountKey parameters.</span></span>  
> 
> <span data-ttu-id="1b5c1-165">Spécifiez le serveur SQL Azure, la base de données, l’utilisateur et le mot de passe pour les paramètres sqlServerName, databaseName, sqlServerUserName et sqlServerPassword.</span><span class="sxs-lookup"><span data-stu-id="1b5c1-165">Specify Azure SQL server, database, user, and password for sqlServerName, databaseName, sqlServerUserName, and sqlServerPassword parameters.</span></span>  

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
    "contentVersion": "1.0.0.0",
    "parameters": { 
        "storageAccountName": { "value": "<Name of the Azure storage account>"    },
        "storageAccountKey": {
            "value": "<Key for the Azure storage account>"
        },
        "sourceBlobContainer": { "value": "adftutorial" },
        "sourceBlobName": { "value": "emp.txt" },
        "sqlServerName": { "value": "<Name of the Azure SQL server>" },
        "databaseName": { "value": "<Name of the Azure SQL database>" },
        "sqlServerUserName": { "value": "<Name of the user who has access to the Azure SQL database>" },
        "sqlServerPassword": { "value": "<password for the user>" },
        "targetSQLTable": { "value": "emp" }
    }
}
```

> [!IMPORTANT]
> <span data-ttu-id="1b5c1-166">Vous pouvez utiliser des fichiers JSON de paramètres distincts pour les environnements de développement, de test et de production avec le même modèle JSON Data Factory.</span><span class="sxs-lookup"><span data-stu-id="1b5c1-166">You may have separate parameter JSON files for development, testing, and production environments that you can use with the same Data Factory JSON template.</span></span> <span data-ttu-id="1b5c1-167">En utilisant un script PowerShell, vous pouvez automatiser le déploiement des entités Data Factory dans ces environnements.</span><span class="sxs-lookup"><span data-stu-id="1b5c1-167">By using a Power Shell script, you can automate deploying Data Factory entities in these environments.</span></span>  
> 
> 

## <a name="create-data-factory"></a><span data-ttu-id="1b5c1-168">Créer une fabrique de données</span><span class="sxs-lookup"><span data-stu-id="1b5c1-168">Create data factory</span></span>
1. <span data-ttu-id="1b5c1-169">Démarrez **Azure PowerShell** et exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="1b5c1-169">Start **Azure PowerShell** and run the following command:</span></span>
   * <span data-ttu-id="1b5c1-170">Exécutez la commande suivante, puis saisissez le nom d’utilisateur et le mot de passe que vous avez utilisés pour la connexion au portail Azure.</span><span class="sxs-lookup"><span data-stu-id="1b5c1-170">Run the following command and enter the user name and password that you use to sign in to the Azure portal.</span></span>
   
    ```PowerShell
    Login-AzureRmAccount    
    ```  
   * <span data-ttu-id="1b5c1-171">Exécutez la commande suivante pour afficher tous les abonnements de ce compte.</span><span class="sxs-lookup"><span data-stu-id="1b5c1-171">Run the following command to view all the subscriptions for this account.</span></span>
   
    ```PowerShell
    Get-AzureRmSubscription
    ```   
   * <span data-ttu-id="1b5c1-172">Exécutez la commande suivante pour sélectionner l’abonnement que vous souhaitez utiliser.</span><span class="sxs-lookup"><span data-stu-id="1b5c1-172">Run the following command to select the subscription that you want to work with.</span></span>
    
    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <SUBSCRIPTION NAME> | Set-AzureRmContext
    ```    
2. <span data-ttu-id="1b5c1-173">Exécutez la commande suivante pour déployer des entités Data Factory à l’aide du modèle Resource Manager que vous avez créé à l’étape 1.</span><span class="sxs-lookup"><span data-stu-id="1b5c1-173">Run the following command to deploy Data Factory entities using the Resource Manager template you created in Step 1.</span></span>

    ```PowerShell   
    New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile C:\ADFGetStarted\ADFCopyTutorialARM.json -TemplateParameterFile C:\ADFGetStarted\ADFCopyTutorialARM-Parameters.json
    ```

## <a name="monitor-pipeline"></a><span data-ttu-id="1b5c1-174">Surveillance d’un pipeline</span><span class="sxs-lookup"><span data-stu-id="1b5c1-174">Monitor pipeline</span></span>

1. <span data-ttu-id="1b5c1-175">Connectez-vous au [portail Azure](https://portal.azure.com) avec votre compte Azure.</span><span class="sxs-lookup"><span data-stu-id="1b5c1-175">Log in to the [Azure portal](https://portal.azure.com) using your Azure account.</span></span>
2. <span data-ttu-id="1b5c1-176">Cliquez sur **Fabriques de données** dans le menu à gauche (ou) cliquez sur **Plus de services** puis sur **Fabriques de données** sous la catégorie **Intelligence et analyse**.</span><span class="sxs-lookup"><span data-stu-id="1b5c1-176">Click **Data factories** on the left menu (or) click **More services** and click **Data factories** under **INTELLIGENCE + ANALYTICS** category.</span></span>
   
    ![Menu Fabriques de données](media/data-factory-copy-activity-tutorial-using-azure-resource-manager-template/data-factories-menu.png)
3. <span data-ttu-id="1b5c1-178">Sur la page **Fabriques de données**, recherchez votre fabrique de données (AzureBlobToAzureSQLDatabaseDF).</span><span class="sxs-lookup"><span data-stu-id="1b5c1-178">In the **Data factories** page, search for and find your data factory (AzureBlobToAzureSQLDatabaseDF).</span></span> 
   
    ![Recherche d’une fabrique de données](media/data-factory-copy-activity-tutorial-using-azure-resource-manager-template/search-for-data-factory.png)  
4. <span data-ttu-id="1b5c1-180">Cliquez sur votre fabrique de données Azure.</span><span class="sxs-lookup"><span data-stu-id="1b5c1-180">Click your Azure data factory.</span></span> <span data-ttu-id="1b5c1-181">La page d’accueil de la fabrique de données apparaît.</span><span class="sxs-lookup"><span data-stu-id="1b5c1-181">You see the home page for the data factory.</span></span>
   
    ![Page d’accueil de la fabrique de données](media/data-factory-copy-activity-tutorial-using-azure-resource-manager-template/data-factory-home-page.png)  
6. <span data-ttu-id="1b5c1-183">Suivez les instructions dans [Surveiller les jeux de données et le pipeline](data-factory-copy-activity-tutorial-using-azure-portal.md#monitor-pipeline) pour surveiller le pipeline et les jeux de données que vous avez créés dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="1b5c1-183">Follow instructions from [Monitor datasets and pipeline](data-factory-copy-activity-tutorial-using-azure-portal.md#monitor-pipeline) to monitor the pipeline and datasets you have created in this tutorial.</span></span> <span data-ttu-id="1b5c1-184">Pour le moment, Visual Studio ne prend pas en charge la surveillance des pipelines Data Factory.</span><span class="sxs-lookup"><span data-stu-id="1b5c1-184">Currently, Visual Studio does not support monitoring Data Factory pipelines.</span></span>
7. <span data-ttu-id="1b5c1-185">Lorsqu’une tranche est à l’état **Prêt**, vérifiez que les données sont copiées vers la table **emp** dans la base de données Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="1b5c1-185">When a slice is in the **Ready** state, verify that the data is copied to the **emp** table in the Azure SQL database.</span></span>


<span data-ttu-id="1b5c1-186">Pour plus d’informations sur l’utilisation des panneaux du portail Azure afin de surveiller le pipeline et les jeux de données que vous avez créés dans ce didacticiel, consultez [Surveiller les jeux de données et le pipeline](data-factory-monitor-manage-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="1b5c1-186">For more information on how to use Azure portal blades to monitor pipeline and datasets you have created in this tutorial, see [Monitor datasets and pipeline](data-factory-monitor-manage-pipelines.md) .</span></span>

<span data-ttu-id="1b5c1-187">Pour plus d’informations sur l’utilisation de l’application Surveiller et gérer afin de surveiller vos pipelines de données, consultez [Surveillance et gestion des pipelines d’Azure Data Factory à l’aide d’application Surveiller](data-factory-monitor-manage-app.md).</span><span class="sxs-lookup"><span data-stu-id="1b5c1-187">For more information on how to use the Monitor & Manage application to monitor your data pipelines, see [Monitor and manage Azure Data Factory pipelines using Monitoring App](data-factory-monitor-manage-app.md).</span></span>

## <a name="data-factory-entities-in-the-template"></a><span data-ttu-id="1b5c1-188">Entités Data Factory dans le modèle</span><span class="sxs-lookup"><span data-stu-id="1b5c1-188">Data Factory entities in the template</span></span>
### <a name="define-data-factory"></a><span data-ttu-id="1b5c1-189">Définir une fabrique de données</span><span class="sxs-lookup"><span data-stu-id="1b5c1-189">Define data factory</span></span>
<span data-ttu-id="1b5c1-190">Vous définissez une fabrique de données dans le modèle Resource Manager, comme indiqué dans l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="1b5c1-190">You define a data factory in the Resource Manager template as shown in the following sample:</span></span>  

```json
"resources": [
{
    "name": "[variables('dataFactoryName')]",
    "apiVersion": "2015-10-01",
    "type": "Microsoft.DataFactory/datafactories",
    "location": "West US"
}
```

<span data-ttu-id="1b5c1-191">La propriété dataFactoryName est défini en tant que :</span><span class="sxs-lookup"><span data-stu-id="1b5c1-191">The dataFactoryName is defined as:</span></span> 

```json
"dataFactoryName": "[concat('AzureBlobToAzureSQLDatabaseDF', uniqueString(resourceGroup().id))]"
```

<span data-ttu-id="1b5c1-192">Il s’agit d’une chaîne unique basée sur l’ID du groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="1b5c1-192">It is a unique string based on the resource group ID.</span></span>  

### <a name="defining-data-factory-entities"></a><span data-ttu-id="1b5c1-193">Définition des entités Data Factory</span><span class="sxs-lookup"><span data-stu-id="1b5c1-193">Defining Data Factory entities</span></span>
<span data-ttu-id="1b5c1-194">Les entités Data Factory suivantes sont définies dans le modèle JSON :</span><span class="sxs-lookup"><span data-stu-id="1b5c1-194">The following Data Factory entities are defined in the JSON template:</span></span> 

1. [<span data-ttu-id="1b5c1-195">Service lié Azure Storage</span><span class="sxs-lookup"><span data-stu-id="1b5c1-195">Azure Storage linked service</span></span>](#azure-storage-linked-service)
2. [<span data-ttu-id="1b5c1-196">Service lié SQL Azure</span><span class="sxs-lookup"><span data-stu-id="1b5c1-196">Azure SQL linked service</span></span>](#azure-sql-database-linked-service)
3. [<span data-ttu-id="1b5c1-197">Jeu de données d’objet blob Azure</span><span class="sxs-lookup"><span data-stu-id="1b5c1-197">Azure blob dataset</span></span>](#azure-blob-dataset)
4. [<span data-ttu-id="1b5c1-198">Jeu de données SQL Azure</span><span class="sxs-lookup"><span data-stu-id="1b5c1-198">Azure SQL dataset</span></span>](#azure-sql-dataset)
5. [<span data-ttu-id="1b5c1-199">Pipeline de données avec une activité de copie</span><span class="sxs-lookup"><span data-stu-id="1b5c1-199">Data pipeline with a copy activity</span></span>](#data-pipeline)

#### <a name="azure-storage-linked-service"></a><span data-ttu-id="1b5c1-200">Service lié Azure Storage</span><span class="sxs-lookup"><span data-stu-id="1b5c1-200">Azure Storage linked service</span></span>
<span data-ttu-id="1b5c1-201">AzureStorageLinkedService relie votre compte de stockage Azure à la fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="1b5c1-201">The AzureStorageLinkedService links your Azure storage account to the data factory.</span></span> <span data-ttu-id="1b5c1-202">Vous avez créé un conteneur et chargé des données dans ce compte de stockage en remplissant les [conditions préalables](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="1b5c1-202">You created a container and uploaded data to this storage account as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span> <span data-ttu-id="1b5c1-203">Vous spécifiez le nom et la clé de votre compte Stockage Azure dans cette section.</span><span class="sxs-lookup"><span data-stu-id="1b5c1-203">You specify the name and key of your Azure storage account in this section.</span></span> <span data-ttu-id="1b5c1-204">Consultez [Service lié Stockage Azure](data-factory-azure-blob-connector.md#azure-storage-linked-service) pour en savoir plus sur les propriétés JSON utilisées pour définir un service lié Stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="1b5c1-204">See [Azure Storage linked service](data-factory-azure-blob-connector.md#azure-storage-linked-service) for details about JSON properties used to define an Azure Storage linked service.</span></span> 

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

<span data-ttu-id="1b5c1-205">La propriété connectionString utilise les paramètres storageAccountName et storageAccountKey.</span><span class="sxs-lookup"><span data-stu-id="1b5c1-205">The connectionString uses the storageAccountName and storageAccountKey parameters.</span></span> <span data-ttu-id="1b5c1-206">Les valeurs de ces paramètres sont transmises à l’aide d’un fichier de configuration.</span><span class="sxs-lookup"><span data-stu-id="1b5c1-206">The values for these parameters passed by using a configuration file.</span></span> <span data-ttu-id="1b5c1-207">La définition utilise également les variables azureStroageLinkedService et dataFactoryName, définies dans le modèle.</span><span class="sxs-lookup"><span data-stu-id="1b5c1-207">The definition also uses variables: azureStroageLinkedService and dataFactoryName defined in the template.</span></span> 

#### <a name="azure-sql-database-linked-service"></a><span data-ttu-id="1b5c1-208">Service lié pour base de données SQL Azure</span><span class="sxs-lookup"><span data-stu-id="1b5c1-208">Azure SQL Database linked service</span></span>
<span data-ttu-id="1b5c1-209">AzureSqlLinkedService lie votre base de données SQL Azure à la fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="1b5c1-209">AzureSqlLinkedService links your Azure SQL database to the data factory.</span></span> <span data-ttu-id="1b5c1-210">Les données copiées à partir du stockage Blob sont stockées dans cette base de données.</span><span class="sxs-lookup"><span data-stu-id="1b5c1-210">The data that is copied from the blob storage is stored in this database.</span></span> <span data-ttu-id="1b5c1-211">Vous avez créé une table emp dans cette base de données en remplissant les [conditions préalables](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="1b5c1-211">You created the emp table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span> <span data-ttu-id="1b5c1-212">Vous spécifiez le nom du serveur SQL Azure, le nom de la base de données, le nom d’utilisateur et le mot de passe de l’utilisateur dans cette section.</span><span class="sxs-lookup"><span data-stu-id="1b5c1-212">You specify the Azure SQL server name, database name, user name, and user password in this section.</span></span> <span data-ttu-id="1b5c1-213">Consultez [Service lié SQL Azure](data-factory-azure-sql-connector.md#linked-service-properties) pour en savoir plus sur les propriétés JSON utilisées pour définir un service lié SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="1b5c1-213">See [Azure SQL linked service](data-factory-azure-sql-connector.md#linked-service-properties) for details about JSON properties used to define an Azure SQL linked service.</span></span>  

```json
{
    "type": "linkedservices",
    "name": "[variables('azureSqlLinkedServiceName')]",
    "dependsOn": [
      "[variables('dataFactoryName')]"
    ],
    "apiVersion": "2015-10-01",
    "properties": {
          "type": "AzureSqlDatabase",
          "description": "Azure SQL linked service",
          "typeProperties": {
            "connectionString": "[concat('Server=tcp:',parameters('sqlServerName'),'.database.windows.net,1433;Database=', parameters('databaseName'), ';User ID=',parameters('sqlServerUserName'),';Password=',parameters('sqlServerPassword'),';Trusted_Connection=False;Encrypt=True;Connection Timeout=30')]"
          }
    }
}
```

<span data-ttu-id="1b5c1-214">La propriété connectionString utilise les paramètres sqlServerName, databaseName, sqlServerUserName et sqlServerPassword, dont les valeurs sont transmises à l’aide d’un fichier de configuration.</span><span class="sxs-lookup"><span data-stu-id="1b5c1-214">The connectionString uses sqlServerName, databaseName, sqlServerUserName, and sqlServerPassword parameters whose values are passed by using a configuration file.</span></span> <span data-ttu-id="1b5c1-215">La définition utilise également les variables suivantes du modèle : azureSqlLinkedServiceName, dataFactoryName.</span><span class="sxs-lookup"><span data-stu-id="1b5c1-215">The definition also uses the following variables from the template: azureSqlLinkedServiceName, dataFactoryName.</span></span>

#### <a name="azure-blob-dataset"></a><span data-ttu-id="1b5c1-216">Jeu de données d’objet blob Azure</span><span class="sxs-lookup"><span data-stu-id="1b5c1-216">Azure blob dataset</span></span>
<span data-ttu-id="1b5c1-217">Le service lié Stockage Azure spécifie la chaîne de connexion que le service Data Factory utilise au moment de l’exécution pour se connecter à votre compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="1b5c1-217">The Azure storage linked service specifies the connection string that Data Factory service uses at run time to connect to your Azure storage account.</span></span> <span data-ttu-id="1b5c1-218">Dans la définition du jeu de données d’objets blob Azure, vous spécifiez les noms du conteneur d’objets blob, du dossier et du fichier contenant les données d’entrée.</span><span class="sxs-lookup"><span data-stu-id="1b5c1-218">In Azure blob dataset definition, you specify names of blob container, folder, and file that contains the input data.</span></span> <span data-ttu-id="1b5c1-219">Consultez [Propriétés du jeu de données d’objet blob Azure](data-factory-azure-blob-connector.md#dataset-properties) pour en savoir plus sur les propriétés JSON permettant de définir un jeu de données d’objets blob Azure.</span><span class="sxs-lookup"><span data-stu-id="1b5c1-219">See [Azure Blob dataset properties](data-factory-azure-blob-connector.md#dataset-properties) for details about JSON properties used to define an Azure Blob dataset.</span></span> 

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
        "structure": [
        {
              "name": "Column0",
              "type": "String"
        },
        {
              "name": "Column1",
              "type": "String"
        }
          ],
          "typeProperties": {
            "folderPath": "[concat(parameters('sourceBlobContainer'), '/')]",
            "fileName": "[parameters('sourceBlobName')]",
            "format": {
                  "type": "TextFormat",
                  "columnDelimiter": ","
            }
          },
          "availability": {
            "frequency": "Hour",
            "interval": 1
          },
          "external": true
    }
}
```

#### <a name="azure-sql-dataset"></a><span data-ttu-id="1b5c1-220">Jeu de données SQL Azure</span><span class="sxs-lookup"><span data-stu-id="1b5c1-220">Azure SQL dataset</span></span>
<span data-ttu-id="1b5c1-221">Vous spécifiez le nom de la table dans Azure SQL Database contenant les données copiées à partir du Stockage Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="1b5c1-221">You specify the name of the table in the Azure SQL database that holds the copied data from the Azure Blob storage.</span></span> <span data-ttu-id="1b5c1-222">Consultez [Propriétés du jeu de données SQL Azure](data-factory-azure-sql-connector.md#dataset-properties) pour en savoir plus sur les propriétés JSON permettant de définir un jeu de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="1b5c1-222">See [Azure SQL dataset properties](data-factory-azure-sql-connector.md#dataset-properties) for details about JSON properties used to define an Azure SQL dataset.</span></span> 

```json
{
    "type": "datasets",
    "name": "[variables('sqlOutputDatasetName')]",
    "dependsOn": [
        "[variables('dataFactoryName')]",
          "[variables('azureSqlLinkedServiceName')]"
    ],
    "apiVersion": "2015-10-01",
    "properties": {
          "type": "AzureSqlTable",
          "linkedServiceName": "[variables('azureSqlLinkedServiceName')]",
          "structure": [
        {
              "name": "FirstName",
              "type": "String"
        },
        {
              "name": "LastName",
              "type": "String"
        }
          ],
          "typeProperties": {
            "tableName": "[parameters('targetSQLTable')]"
          },
          "availability": {
            "frequency": "Hour",
            "interval": 1
          }
    }
}
```

#### <a name="data-pipeline"></a><span data-ttu-id="1b5c1-223">Pipeline de données</span><span class="sxs-lookup"><span data-stu-id="1b5c1-223">Data pipeline</span></span>
<span data-ttu-id="1b5c1-224">Vous définissez un pipeline qui copie les données du jeu de données d’objets blob Azure vers le jeu de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="1b5c1-224">You define a pipeline that copies data from the Azure blob dataset to the Azure SQL dataset.</span></span> <span data-ttu-id="1b5c1-225">Consultez [Pipeline JSON](data-factory-create-pipelines.md#pipeline-json) pour obtenir des descriptions des éléments JSON permettant de définir un pipeline dans cet exemple.</span><span class="sxs-lookup"><span data-stu-id="1b5c1-225">See [Pipeline JSON](data-factory-create-pipelines.md#pipeline-json) for descriptions of JSON elements used to define a pipeline in this example.</span></span> 

```json
{
    "type": "datapipelines",
    "name": "[variables('pipelineName')]",
    "dependsOn": [
        "[variables('dataFactoryName')]",
          "[variables('azureStorageLinkedServiceName')]",
          "[variables('azureSqlLinkedServiceName')]",
          "[variables('blobInputDatasetName')]",
          "[variables('sqlOutputDatasetName')]"
    ],
    "apiVersion": "2015-10-01",
    "properties": {
          "activities": [
        {
              "name": "CopyFromAzureBlobToAzureSQL",
              "description": "Copy data frm Azure blob to Azure SQL",
              "type": "Copy",
              "inputs": [
            {
                  "name": "[variables('blobInputDatasetName')]"
            }
              ],
              "outputs": [
            {
                  "name": "[variables('sqlOutputDatasetName')]"
            }
              ],
              "typeProperties": {
                "source": {
                      "type": "BlobSource"
                },
                "sink": {
                      "type": "SqlSink",
                      "sqlWriterCleanupScript": "$$Text.Format('DELETE FROM {0}', 'emp')"
                },
                "translator": {
                      "type": "TabularTranslator",
                      "columnMappings": "Column0:FirstName,Column1:LastName"
                }
              },
              "Policy": {
                "concurrency": 1,
                "executionPriorityOrder": "NewestFirst",
                "retry": 3,
                "timeout": "01:00:00"
              }
        }
          ],
          "start": "2017-05-11T00:00:00Z",
          "end": "2017-05-12T00:00:00Z"
    }
}
```

## <a name="reuse-the-template"></a><span data-ttu-id="1b5c1-226">Réutiliser le modèle</span><span class="sxs-lookup"><span data-stu-id="1b5c1-226">Reuse the template</span></span>
<span data-ttu-id="1b5c1-227">Dans ce didacticiel, vous avez créé un modèle pour définir des entités Data Factory et un modèle pour transmettre les valeurs des paramètres.</span><span class="sxs-lookup"><span data-stu-id="1b5c1-227">In the tutorial, you created a template for defining Data Factory entities and a template for passing values for parameters.</span></span> <span data-ttu-id="1b5c1-228">Le pipeline copie les données d’un compte Stockage Azure vers une base de données SQL Azure spécifiée via des paramètres.</span><span class="sxs-lookup"><span data-stu-id="1b5c1-228">The pipeline copies data from an Azure Storage account to an Azure SQL database specified via parameters.</span></span> <span data-ttu-id="1b5c1-229">Pour utiliser le même modèle afin de déployer des entités Data Factory dans des environnements différents, vous créez un fichier de paramètres pour chaque environnement et l’utiliser lors du déploiement de cet environnement.</span><span class="sxs-lookup"><span data-stu-id="1b5c1-229">To use the same template to deploy Data Factory entities to different environments, you create a parameter file for each environment and use it when deploying to that environment.</span></span>     

<span data-ttu-id="1b5c1-230">Exemple :</span><span class="sxs-lookup"><span data-stu-id="1b5c1-230">Example:</span></span>  

```PowerShell
New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFCopyTutorialARM.json -TemplateParameterFile ADFCopyTutorialARM-Parameters-Dev.json
```
```PowerShell
New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFCopyTutorialARM.json -TemplateParameterFile ADFCopyTutorialARM-Parameters-Test.json
```
```PowerShell
New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFCopyTutorialARM.json -TemplateParameterFile ADFCopyTutorialARM-Parameters-Production.json
```

<span data-ttu-id="1b5c1-231">Notez que la première commande utilise le fichier de paramètres pour l’environnement de développement, la deuxième pour l’environnement de test et la troisième pour l’environnement de production.</span><span class="sxs-lookup"><span data-stu-id="1b5c1-231">Notice that the first command uses parameter file for the development environment, second one for the test environment, and the third one for the production environment.</span></span>  

<span data-ttu-id="1b5c1-232">Vous pouvez également réutiliser le modèle pour effectuer des tâches répétitives.</span><span class="sxs-lookup"><span data-stu-id="1b5c1-232">You can also reuse the template to perform repeated tasks.</span></span> <span data-ttu-id="1b5c1-233">Par exemple, vous devez créer plusieurs fabriques de données avec un ou plusieurs pipelines qui implémentent la même logique, mais chaque fabrique de données utilise des comptes Stockage et SQL Database différents.</span><span class="sxs-lookup"><span data-stu-id="1b5c1-233">For example, you need to create many data factories with one or more pipelines that implement the same logic but each data factory uses different Storage and SQL Database accounts.</span></span> <span data-ttu-id="1b5c1-234">Dans ce scénario, vous utilisez le même modèle dans le même environnement (développement, test ou production) avec différents fichiers de paramètres pour créer des fabriques de données.</span><span class="sxs-lookup"><span data-stu-id="1b5c1-234">In this scenario, you use the same template in the same environment (dev, test, or production) with different parameter files to create data factories.</span></span>   

## <a name="next-steps"></a><span data-ttu-id="1b5c1-235">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1b5c1-235">Next steps</span></span>
<span data-ttu-id="1b5c1-236">Dans ce didacticiel, vous avez utilisé le stockage Blob Azure comme magasin de données source et une base de données SQL Azure comme banque de données de destination dans une opération de copie.</span><span class="sxs-lookup"><span data-stu-id="1b5c1-236">In this tutorial, you used Azure blob storage as a source data store and an Azure SQL database as a destination data store in a copy operation.</span></span> <span data-ttu-id="1b5c1-237">Le tableau ci-dessous contient la liste des magasins de données pris en charge en tant que sources et destinations par l’activité de copie :</span><span class="sxs-lookup"><span data-stu-id="1b5c1-237">The following table provides a list of data stores supported as sources and destinations by the copy activity:</span></span> 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

<span data-ttu-id="1b5c1-238">Pour découvrir comment copier des données vers/depuis un magasin de données, cliquez sur le lien du magasin de données dans le tableau.</span><span class="sxs-lookup"><span data-stu-id="1b5c1-238">To learn about how to copy data to/from a data store, click the link for the data store in the table.</span></span>
