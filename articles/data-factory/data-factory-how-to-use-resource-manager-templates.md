---
title: "Utilisation de modèles Resource Manager dans Data Factory | Microsoft Docs"
description: "Découvrez comment créer et utiliser des modèles Azure Resource Manager pour créer des entités Data Factory."
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: 
ms.assetid: 37724021-f55f-4e85-9206-6d4a48bda3d8
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: shlo
ms.openlocfilehash: c3ea2c047434b5b5495f0ce85be9376a502e4962
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="use-templates-to-create-azure-data-factory-entities"></a><span data-ttu-id="f5fe7-103">Utilisation de modèles pour créer des entités Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="f5fe7-103">Use templates to create Azure Data Factory entities</span></span>
## <a name="overview"></a><span data-ttu-id="f5fe7-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="f5fe7-104">Overview</span></span>
<span data-ttu-id="f5fe7-105">Lors de l’utilisation d’Azure Data Factory pour vos besoins d’intégration de données, vous pourriez être amené à réutiliser le même modèle dans différents environnements ou à implémenter la même tâche de façon répétée dans la même solution.</span><span class="sxs-lookup"><span data-stu-id="f5fe7-105">While using Azure Data Factory for your data integration needs, you may find yourself reusing the same pattern across different environments or implementing the same task repetitively within the same solution.</span></span> <span data-ttu-id="f5fe7-106">Les modèles vous aident à implémenter et à gérer ces scénarios de manière simple.</span><span class="sxs-lookup"><span data-stu-id="f5fe7-106">Templates help you implement and manage these scenarios in an easy manner.</span></span> <span data-ttu-id="f5fe7-107">Les modèles dans Azure Data Factory sont parfaitement adaptés aux scénarios qui impliquent la réutilisation et la répétition.</span><span class="sxs-lookup"><span data-stu-id="f5fe7-107">Templates in Azure Data Factory are ideal for scenarios that involve reusability and repetition.</span></span>

<span data-ttu-id="f5fe7-108">Prenons le cas d’une entreprise qui compte 10 usines de fabrication dans le monde entier.</span><span class="sxs-lookup"><span data-stu-id="f5fe7-108">Consider the situation where an organization has 10 manufacturing plants across the world.</span></span> <span data-ttu-id="f5fe7-109">Les journaux de chaque usine sont stockés dans une base de données SQL Server locale distincte.</span><span class="sxs-lookup"><span data-stu-id="f5fe7-109">The logs from each plant are stored in a separate on-premises SQL Server database.</span></span> <span data-ttu-id="f5fe7-110">L’entreprise souhaite créer un entrepôt de données unique dans le cloud pour l’analyse ad-hoc.</span><span class="sxs-lookup"><span data-stu-id="f5fe7-110">The company wants to build a single data warehouse in the cloud for ad-hoc analytics.</span></span> <span data-ttu-id="f5fe7-111">Elle souhaite également avoir la même logique mais des configurations différentes pour les environnements de développement, de test et de production.</span><span class="sxs-lookup"><span data-stu-id="f5fe7-111">It also wants to have the same logic but different configurations for development, test, and production environments.</span></span>

<span data-ttu-id="f5fe7-112">Dans ce cas, une tâche doit être répétée dans le même environnement, mais avec des valeurs différentes dans les 10 entrepôts de données pour chaque usine de fabrication.</span><span class="sxs-lookup"><span data-stu-id="f5fe7-112">In this case, a task needs to be repeated within the same environment, but with different values across the 10 data factories for each manufacturing plant.</span></span> <span data-ttu-id="f5fe7-113">Le facteur de **répétition** est donc présent.</span><span class="sxs-lookup"><span data-stu-id="f5fe7-113">In effect, **repetition** is present.</span></span> <span data-ttu-id="f5fe7-114">La création de modèles permet l’abstraction de ce flux générique (autrement dit, les pipelines ayant les mêmes activités dans chaque entrepôt de données), mais utilise un fichier de paramètres distinct pour chaque usine de fabrication.</span><span class="sxs-lookup"><span data-stu-id="f5fe7-114">Templating allows the abstraction of this generic flow (that is, pipelines having the same activities in each data factory), but uses a separate parameter file for each manufacturing plant.</span></span>

<span data-ttu-id="f5fe7-115">En outre, étant donné que l’entreprise souhaite déployer ces 10 entrepôts de données plusieurs fois dans différents environnements, les modèles peuvent utiliser cette **réutilisation** à l’aide de fichiers de paramètres distincts pour les environnements de développement, de test et de production.</span><span class="sxs-lookup"><span data-stu-id="f5fe7-115">Furthermore, as the organization wants to deploy these 10 data factories multiple times across different environments, templates can use this **reusability** by utilizing separate parameter files for development, test, and production environments.</span></span>

## <a name="templating-with-azure-resource-manager"></a><span data-ttu-id="f5fe7-116">Création de modèles avec Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="f5fe7-116">Templating with Azure Resource Manager</span></span>
<span data-ttu-id="f5fe7-117">Les [modèles Azure Resource Manager](../azure-resource-manager/resource-group-overview.md#template-deployment) constituent une excellente méthode de création de modèles dans Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="f5fe7-117">[Azure Resource Manager templates](../azure-resource-manager/resource-group-overview.md#template-deployment) are a great way to achieve templating in Azure Data Factory.</span></span> <span data-ttu-id="f5fe7-118">Les modèles Resource Manager définissent l’infrastructure et la configuration de votre solution Azure à l’aide d’un fichier JSON.</span><span class="sxs-lookup"><span data-stu-id="f5fe7-118">Resource Manager templates define the infrastructure and configuration of your Azure solution through a JSON file.</span></span> <span data-ttu-id="f5fe7-119">Étant donné que les modèles Azure Resource Manager fonctionnent avec tous les services ou la plupart des services Azure, ils peuvent être utilisés pour gérer facilement toutes les ressources de vos actifs Azure.</span><span class="sxs-lookup"><span data-stu-id="f5fe7-119">Because Azure Resource Manager templates work with all/most Azure services, it can be widely used to easily manage all resources of your Azure assets.</span></span> <span data-ttu-id="f5fe7-120">Pour en savoir plus sur les modèles Resource Manager en général, consultez [Création de modèles Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="f5fe7-120">See [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md) to learn more about the Resource Manager Templates in general.</span></span>

## <a name="tutorials"></a><span data-ttu-id="f5fe7-121">Didacticiels</span><span class="sxs-lookup"><span data-stu-id="f5fe7-121">Tutorials</span></span>
<span data-ttu-id="f5fe7-122">Reportez-vous aux didacticiels suivants pour obtenir des instructions détaillées sur la création d’entités Data Factory à l’aide de modèles Resource Manager :</span><span class="sxs-lookup"><span data-stu-id="f5fe7-122">See the following tutorials for step-by-step instructions to create Data Factory entities by using Resource Manager templates:</span></span>

* [<span data-ttu-id="f5fe7-123">Didacticiel : Créer un pipeline pour copier des données à l’aide du modèle Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="f5fe7-123">Tutorial: Create a pipeline to copy data by using Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
* [<span data-ttu-id="f5fe7-124">Didacticiel : Créer un pipeline pour traiter des données à l’aide du modèle Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="f5fe7-124">Tutorial: Create a pipeline to process data by using Azure Resource Manager template</span></span>](data-factory-build-your-first-pipeline.md)

## <a name="data-factory-templates-on-github"></a><span data-ttu-id="f5fe7-125">Modèles Data Factory sur GitHub</span><span class="sxs-lookup"><span data-stu-id="f5fe7-125">Data Factory templates on GitHub</span></span>
<span data-ttu-id="f5fe7-126">Découvrez les modèles de démarrage rapide Azure suivants sur GitHub :</span><span class="sxs-lookup"><span data-stu-id="f5fe7-126">Check out the following Azure quick start templates on GitHub:</span></span>

* [<span data-ttu-id="f5fe7-127">Créer une fabrique de données pour copier des données à partir du Stockage Blob Azure vers une base de données SQL Azure</span><span class="sxs-lookup"><span data-stu-id="f5fe7-127">Create a Data factory to copy data from Azure Blob Storage to Azure SQL Database</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-blob-to-sql-copy)
* [<span data-ttu-id="f5fe7-128">Créer une fabrique de données avec une activité Hive sur un cluster Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="f5fe7-128">Create a Data factory with Hive activity on Azure HDInsight cluster</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-hive-transformation)
* [<span data-ttu-id="f5fe7-129">Créer une fabrique de données pour copier des données à partir de Salesforce vers des objets blob Azure</span><span class="sxs-lookup"><span data-stu-id="f5fe7-129">Create a Data factory to copy data from Salesforce to Azure Blobs</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-salesforce-to-blob-copy)
* [<span data-ttu-id="f5fe7-130">Créer une fabrique de données qui lié les activités : copie des données à partir d’un serveur FTP vers des objets Blob Azure, appelle un script hive sur un cluster HDInsight à la demande pour transformer les données et copie le résultat dans Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="f5fe7-130">Create a Data factory that chains activities: copies data from an FTP server to Azure Blobs, invokes a hive script on an on-demand HDInsight cluster to transform the data, and copies result into Azure SQL Database</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/201-data-factory-ftp-hive-blob)

<span data-ttu-id="f5fe7-131">N’hésitez pas à partager vos modèles Azure Data Factory dans [Démarrage rapide d’Azure](https://azure.microsoft.com/documentation/templates/).</span><span class="sxs-lookup"><span data-stu-id="f5fe7-131">Feel free to share your Azure Data Factory templates at [Azure Quick start](https://azure.microsoft.com/documentation/templates/).</span></span> <span data-ttu-id="f5fe7-132">Reportez-vous au [guide de contribution](https://github.com/Azure/azure-quickstart-templates/tree/master/1-CONTRIBUTION-GUIDE) lors du développement de modèles qui peuvent être partagés via ce référentiel.</span><span class="sxs-lookup"><span data-stu-id="f5fe7-132">Refer to the [contribution guide](https://github.com/Azure/azure-quickstart-templates/tree/master/1-CONTRIBUTION-GUIDE) while developing templates that can be shared via this repository.</span></span>

<span data-ttu-id="f5fe7-133">Les sections suivantes fournissent plus d’informations sur la définition de ressources Data Factory dans un modèle Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="f5fe7-133">The following sections provide details about defining Data Factory resources in a Resource Manager template.</span></span>

## <a name="defining-data-factory-resources-in-templates"></a><span data-ttu-id="f5fe7-134">Définition de ressources Data Factory dans les modèles</span><span class="sxs-lookup"><span data-stu-id="f5fe7-134">Defining Data Factory resources in templates</span></span>
<span data-ttu-id="f5fe7-135">Le modèle de niveau supérieur pour la définition d’une fabrique de données est :</span><span class="sxs-lookup"><span data-stu-id="f5fe7-135">The top-level template for defining a data factory is:</span></span>

```JSON
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
    { "type": "linkedservices",
        ...
    },
    {"type": "datasets",
        ...
    },
    {"type": "dataPipelines",
        ...
    }
}
```

### <a name="define-data-factory"></a><span data-ttu-id="f5fe7-136">Définir une fabrique de données</span><span class="sxs-lookup"><span data-stu-id="f5fe7-136">Define data factory</span></span>
<span data-ttu-id="f5fe7-137">Vous définissez une fabrique de données dans le modèle Resource Manager, comme indiqué dans l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="f5fe7-137">You define a data factory in the Resource Manager template as shown in the following sample:</span></span>

```JSON
"resources": [
{
    "name": "[variables('<mydataFactoryName>')]",
    "apiVersion": "2015-10-01",
    "type": "Microsoft.DataFactory/datafactories",
    "location": "East US"
}
```
<span data-ttu-id="f5fe7-138">Le dataFactoryName est défini dans « variables » en tant que :</span><span class="sxs-lookup"><span data-stu-id="f5fe7-138">The dataFactoryName is defined in “variables” as:</span></span>

```JSON
"dataFactoryName": "[concat('<myDataFactoryName>', uniqueString(resourceGroup().id))]",
```

### <a name="define-linked-services"></a><span data-ttu-id="f5fe7-139">Définir les services liés</span><span class="sxs-lookup"><span data-stu-id="f5fe7-139">Define linked services</span></span>

```JSON
"type": "linkedservices",
"name": "[variables('<LinkedServiceName>')]",
"apiVersion": "2015-10-01",
"dependsOn": [ "[variables('<dataFactoryName>')]" ],
"properties": {
    ...
}
```

<span data-ttu-id="f5fe7-140">Consultez [Service de stockage lié](data-factory-azure-blob-connector.md#azure-storage-linked-service) ou [Services liés de calcul](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) pour plus d’informations sur les propriétés JSON pour le service lié spécifique que vous souhaitez déployer.</span><span class="sxs-lookup"><span data-stu-id="f5fe7-140">See [Storage Linked Service](data-factory-azure-blob-connector.md#azure-storage-linked-service) or [Compute Linked Services](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details about the JSON properties for the specific linked service you wish to deploy.</span></span> <span data-ttu-id="f5fe7-141">Le paramètre « dependsOn » spécifie le nom de la fabrique de données correspondante.</span><span class="sxs-lookup"><span data-stu-id="f5fe7-141">The “dependsOn” parameter specifies name of the corresponding data factory.</span></span> <span data-ttu-id="f5fe7-142">Un exemple de définition d’un service lié pour le Stockage Azure est indiqué dans la définition JSON suivante :</span><span class="sxs-lookup"><span data-stu-id="f5fe7-142">An example of defining a linked service for Azure Storage is shown in the following JSON definition:</span></span>

### <a name="define-datasets"></a><span data-ttu-id="f5fe7-143">Définir les jeux de données</span><span class="sxs-lookup"><span data-stu-id="f5fe7-143">Define datasets</span></span>

```JSON
"type": "datasets",
"name": "[variables('<myDatasetName>')]",
"dependsOn": [
    "[variables('<dataFactoryName>')]",
    "[variables('<myDatasetLinkedServiceName>')]"
],
"apiVersion": "2015-10-01",
"properties": {
    ...
}
```
<span data-ttu-id="f5fe7-144">Consultez [Magasins de données pris en charge](data-factory-data-movement-activities.md#supported-data-stores-and-formats) pour plus d’informations sur les propriétés JSON pour le type de jeu de données spécifique que vous souhaitez déployer.</span><span class="sxs-lookup"><span data-stu-id="f5fe7-144">Refer to [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) for details about the JSON properties for the specific dataset type you wish to deploy.</span></span> <span data-ttu-id="f5fe7-145">Notez que le paramètre « dependsOn » spécifie le nom de la fabrique de données et du service lié de stockage correspondants.</span><span class="sxs-lookup"><span data-stu-id="f5fe7-145">Note the “dependsOn” parameter specifies name of the corresponding data factory and storage linked service.</span></span> <span data-ttu-id="f5fe7-146">Un exemple de définition d’un type de jeu de données pour le Stockage Blob Azure est indiqué dans la définition JSON suivante :</span><span class="sxs-lookup"><span data-stu-id="f5fe7-146">An example of defining dataset type of Azure blob storage is shown in the following JSON definition:</span></span>

```JSON
"type": "datasets",
"name": "[variables('storageDataset')]",
"dependsOn": [
    "[variables('dataFactoryName')]",
    "[variables('storageLinkedServiceName')]"
],
"apiVersion": "2015-10-01",
"properties": {
"type": "AzureBlob",
"linkedServiceName": "[variables('storageLinkedServiceName')]",
"typeProperties": {
    "folderPath": "[concat(parameters('sourceBlobContainer'), '/')]",
    "fileName": "[parameters('sourceBlobName')]",
    "format": {
        "type": "TextFormat"
    }
},
"availability": {
    "frequency": "Hour",
    "interval": 1
}
```

### <a name="define-pipelines"></a><span data-ttu-id="f5fe7-147">Définir les pipelines</span><span class="sxs-lookup"><span data-stu-id="f5fe7-147">Define pipelines</span></span>

```JSON
"type": "dataPipelines",
"name": "[variables('<mypipelineName>')]",
"dependsOn": [
    "[variables('<dataFactoryName>')]",
    "[variables('<inputDatasetLinkedServiceName>')]",
    "[variables('<outputDatasetLinkedServiceName>')]",
    "[variables('<inputDataset>')]",
    "[variables('<outputDataset>')]"
],
"apiVersion": "2015-10-01",
"properties": {
    activities: {
        ...
    }
}
```

<span data-ttu-id="f5fe7-148">Consultez [Définition des pipelines](data-factory-create-pipelines.md#pipeline-json) pour plus d’informations sur les propriétés JSON permettant de définir le pipeline et les activités spécifiques que vous souhaitez déployer.</span><span class="sxs-lookup"><span data-stu-id="f5fe7-148">Refer to [defining pipelines](data-factory-create-pipelines.md#pipeline-json) for details about the JSON properties for defining the specific pipeline and activities you wish to deploy.</span></span> <span data-ttu-id="f5fe7-149">Notez que le paramètre « dependsOn » spécifie le nom de la fabrique de données, ainsi que les services liés ou les jeux de données correspondants.</span><span class="sxs-lookup"><span data-stu-id="f5fe7-149">Note the “dependsOn” parameter specifies name of the data factory, and any corresponding linked services or datasets.</span></span> <span data-ttu-id="f5fe7-150">Un exemple de pipeline qui copie des données depuis le Stockage Blob Azure vers une base de données SQL Azure est indiqué dans l’extrait de code JSON suivant :</span><span class="sxs-lookup"><span data-stu-id="f5fe7-150">An example of a pipeline that copies data from Azure Blob Storage to Azure SQL Database is shown in the following JSON snippet:</span></span>

```JSON
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
    "start": "2016-10-03T00:00:00Z",
    "end": "2016-10-04T00:00:00Z"
}
```
## <a name="parameterizing-data-factory-template"></a><span data-ttu-id="f5fe7-151">Paramétrage du modèle Data Factory</span><span class="sxs-lookup"><span data-stu-id="f5fe7-151">Parameterizing Data Factory template</span></span>
<span data-ttu-id="f5fe7-152">Pour connaître les meilleures pratiques de paramétrage, consultez [Bonnes pratiques relatives à la création de modèles Azure Resource Manager](../azure-resource-manager/resource-manager-template-best-practices.md#parameters).</span><span class="sxs-lookup"><span data-stu-id="f5fe7-152">For best practices on parameterizing, see [Best practices for creating Azure Resource Manager templates](../azure-resource-manager/resource-manager-template-best-practices.md#parameters) article.</span></span> <span data-ttu-id="f5fe7-153">En général, l’utilisation des paramètres doit être minimale, surtout s’il est possible d’utiliser des variables à la place.</span><span class="sxs-lookup"><span data-stu-id="f5fe7-153">In general, parameter usage should be minimized, especially if variables can be used instead.</span></span> <span data-ttu-id="f5fe7-154">Fournissez uniquement des paramètres dans les scénarios suivants :</span><span class="sxs-lookup"><span data-stu-id="f5fe7-154">Only provide parameters in the following scenarios:</span></span>

* <span data-ttu-id="f5fe7-155">Les paramètres varient selon l’environnement (exemple : développement, test et production)</span><span class="sxs-lookup"><span data-stu-id="f5fe7-155">Settings vary by environment (example: development, test, and production)</span></span>
* <span data-ttu-id="f5fe7-156">les clés secrètes (notamment les mots de passe) ;</span><span class="sxs-lookup"><span data-stu-id="f5fe7-156">Secrets (such as passwords)</span></span>

<span data-ttu-id="f5fe7-157">Si vous avez besoin d’extraire des clés secrètes à partir [d’Azure Key Vault](../key-vault/key-vault-get-started.md) lors du déploiement d’entités Azure Data Factory à l’aide de modèles, spécifiez le **coffre de clés** et le **nom secret** comme indiqué dans l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="f5fe7-157">If you need to pull secrets from [Azure Key Vault](../key-vault/key-vault-get-started.md) when deploying Azure Data Factory entities using templates, specify the **key vault** and **secret name** as shown in the following example:</span></span>

```JSON
"parameters": {
    "storageAccountKey": {
        "reference": {
            "keyVault": {
                "id":"/subscriptions/<subscriptionID>/resourceGroups/<resourceGroupName>/providers/Microsoft.KeyVault/vaults/<keyVaultName>",
             },
            "secretName": "<secretName>"
           },
       },
       ...
}
```

> [!NOTE]
> <span data-ttu-id="f5fe7-158">L’exportation de modèles pour les fabriques de données existantes n’est actuellement pas prise en charge, mais nous y travaillons.</span><span class="sxs-lookup"><span data-stu-id="f5fe7-158">While exporting templates for existing data factories is currently not yet supported, it is in the works.</span></span>
>
>
