---
title: "modèles du Gestionnaire de ressources aaaUse dans la fabrique de données | Documents Microsoft"
description: "Découvrez comment toocreate et utilisez entités Azure Resource Manager modèles toocreate Data Factory."
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
ms.openlocfilehash: 60d5dbd29494420006aed6d5bd9a10a63c36bec3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-templates-toocreate-azure-data-factory-entities"></a><span data-ttu-id="6eb80-103">Utiliser des entités de modèles toocreate Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="6eb80-103">Use templates toocreate Azure Data Factory entities</span></span>
## <a name="overview"></a><span data-ttu-id="6eb80-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="6eb80-104">Overview</span></span>
<span data-ttu-id="6eb80-105">Lors de l’utilisation d’Azure Data Factory à vos besoins d’intégration de données, vous pouvez être obligé de réutilisation hello même modèle dans différents environnements ou implémentation hello même tâche de façon répétée dans hello même solution.</span><span class="sxs-lookup"><span data-stu-id="6eb80-105">While using Azure Data Factory for your data integration needs, you may find yourself reusing hello same pattern across different environments or implementing hello same task repetitively within hello same solution.</span></span> <span data-ttu-id="6eb80-106">Les modèles vous aident à implémenter et à gérer ces scénarios de manière simple.</span><span class="sxs-lookup"><span data-stu-id="6eb80-106">Templates help you implement and manage these scenarios in an easy manner.</span></span> <span data-ttu-id="6eb80-107">Les modèles dans Azure Data Factory sont parfaitement adaptés aux scénarios qui impliquent la réutilisation et la répétition.</span><span class="sxs-lookup"><span data-stu-id="6eb80-107">Templates in Azure Data Factory are ideal for scenarios that involve reusability and repetition.</span></span>

<span data-ttu-id="6eb80-108">Imaginons une situation hello où une organisation a des 10 unités de fabrication dans Bonjour.</span><span class="sxs-lookup"><span data-stu-id="6eb80-108">Consider hello situation where an organization has 10 manufacturing plants across hello world.</span></span> <span data-ttu-id="6eb80-109">journaux de Hello à partir de chaque plante sont stockés dans une base de données SQL Server local distinct.</span><span class="sxs-lookup"><span data-stu-id="6eb80-109">hello logs from each plant are stored in a separate on-premises SQL Server database.</span></span> <span data-ttu-id="6eb80-110">société de Hello veut toobuild un entrepôt de données unique dans le cloud de hello pour ad-hoc analytique.</span><span class="sxs-lookup"><span data-stu-id="6eb80-110">hello company wants toobuild a single data warehouse in hello cloud for ad-hoc analytics.</span></span> <span data-ttu-id="6eb80-111">Elle souhaite également toohave hello même logique, mais différentes configurations pour les environnements de développement, test et de production.</span><span class="sxs-lookup"><span data-stu-id="6eb80-111">It also wants toohave hello same logic but different configurations for development, test, and production environments.</span></span>

<span data-ttu-id="6eb80-112">Dans ce cas, une tâche doit toobe répété dans hello même environnement, mais avec des valeurs différentes sur hello 10 fabriques de données pour chaque installation.</span><span class="sxs-lookup"><span data-stu-id="6eb80-112">In this case, a task needs toobe repeated within hello same environment, but with different values across hello 10 data factories for each manufacturing plant.</span></span> <span data-ttu-id="6eb80-113">Le facteur de **répétition** est donc présent.</span><span class="sxs-lookup"><span data-stu-id="6eb80-113">In effect, **repetition** is present.</span></span> <span data-ttu-id="6eb80-114">Création de modèles permet abstraction hello de ce flux générique (autrement dit, pipelines ayant hello activités mêmes dans chaque fabrique de données), mais utilise un fichier de paramètres distincts pour chaque installation.</span><span class="sxs-lookup"><span data-stu-id="6eb80-114">Templating allows hello abstraction of this generic flow (that is, pipelines having hello same activities in each data factory), but uses a separate parameter file for each manufacturing plant.</span></span>

<span data-ttu-id="6eb80-115">En outre, comme hello organisation souhaite toodeploy ces usines 10 données plusieurs fois entre les différents environnements, modèles peuvent utiliser ce **réutilisabilité** en utilisant des fichiers de paramètres distincts pour le développement, test, et environnements de production.</span><span class="sxs-lookup"><span data-stu-id="6eb80-115">Furthermore, as hello organization wants toodeploy these 10 data factories multiple times across different environments, templates can use this **reusability** by utilizing separate parameter files for development, test, and production environments.</span></span>

## <a name="templating-with-azure-resource-manager"></a><span data-ttu-id="6eb80-116">Création de modèles avec Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="6eb80-116">Templating with Azure Resource Manager</span></span>
<span data-ttu-id="6eb80-117">[Les modèles de gestionnaire de ressources Azure](../azure-resource-manager/resource-group-overview.md#template-deployment) sont une création de modèles tooachieve idéale dans Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="6eb80-117">[Azure Resource Manager templates](../azure-resource-manager/resource-group-overview.md#template-deployment) are a great way tooachieve templating in Azure Data Factory.</span></span> <span data-ttu-id="6eb80-118">Les modèles de gestionnaire de ressources définissent l’infrastructure de hello et la configuration de votre solution Azure via un fichier JSON.</span><span class="sxs-lookup"><span data-stu-id="6eb80-118">Resource Manager templates define hello infrastructure and configuration of your Azure solution through a JSON file.</span></span> <span data-ttu-id="6eb80-119">Étant donné que les modèles Azure Resource Manager fonctionnent avec tous les/la plupart des services Azure, il peut être largement utilisé tooeasily gérer toutes les ressources de vos ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="6eb80-119">Because Azure Resource Manager templates work with all/most Azure services, it can be widely used tooeasily manage all resources of your Azure assets.</span></span> <span data-ttu-id="6eb80-120">Consultez [les modèles de programmation Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) toolearn savoir plus sur hello en général les modèles du Gestionnaire de ressources.</span><span class="sxs-lookup"><span data-stu-id="6eb80-120">See [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md) toolearn more about hello Resource Manager Templates in general.</span></span>

## <a name="tutorials"></a><span data-ttu-id="6eb80-121">Didacticiels</span><span class="sxs-lookup"><span data-stu-id="6eb80-121">Tutorials</span></span>
<span data-ttu-id="6eb80-122">Consultez hello suivant des didacticiels pour les entités de fabrique de données toocreate des instructions détaillées en utilisant des modèles de gestionnaire de ressources :</span><span class="sxs-lookup"><span data-stu-id="6eb80-122">See hello following tutorials for step-by-step instructions toocreate Data Factory entities by using Resource Manager templates:</span></span>

* [<span data-ttu-id="6eb80-123">Didacticiel : Créer un toocopy de données de pipeline à l’aide du modèle Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="6eb80-123">Tutorial: Create a pipeline toocopy data by using Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
* [<span data-ttu-id="6eb80-124">Didacticiel : Créer un tooprocess de données de pipeline à l’aide du modèle Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="6eb80-124">Tutorial: Create a pipeline tooprocess data by using Azure Resource Manager template</span></span>](data-factory-build-your-first-pipeline.md)

## <a name="data-factory-templates-on-github"></a><span data-ttu-id="6eb80-125">Modèles Data Factory sur GitHub</span><span class="sxs-lookup"><span data-stu-id="6eb80-125">Data Factory templates on GitHub</span></span>
<span data-ttu-id="6eb80-126">Passez en revue hello suivant des modèles de démarrage rapide d’Azure sur GitHub :</span><span class="sxs-lookup"><span data-stu-id="6eb80-126">Check out hello following Azure quick start templates on GitHub:</span></span>

* [<span data-ttu-id="6eb80-127">Créer une fabrique toocopy de données à partir du stockage d’objets Blob Azure tooAzure base de données SQL</span><span class="sxs-lookup"><span data-stu-id="6eb80-127">Create a Data factory toocopy data from Azure Blob Storage tooAzure SQL Database</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-blob-to-sql-copy)
* [<span data-ttu-id="6eb80-128">Créer une fabrique de données avec une activité Hive sur un cluster Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="6eb80-128">Create a Data factory with Hive activity on Azure HDInsight cluster</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-hive-transformation)
* [<span data-ttu-id="6eb80-129">Créer une fabrique toocopy de données à partir d’objets BLOB tooAzure de Salesforce</span><span class="sxs-lookup"><span data-stu-id="6eb80-129">Create a Data factory toocopy data from Salesforce tooAzure Blobs</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-salesforce-to-blob-copy)
* [<span data-ttu-id="6eb80-130">Créer une fabrique de données qui est lié activités : copie des données à partir d’un serveur FTP tooAzure BLOB, appelle un script hive sur un à la demande HDInsight cluster tootransform hello de données et copie le résultat dans la base de données SQL Azure</span><span class="sxs-lookup"><span data-stu-id="6eb80-130">Create a Data factory that chains activities: copies data from an FTP server tooAzure Blobs, invokes a hive script on an on-demand HDInsight cluster tootransform hello data, and copies result into Azure SQL Database</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/201-data-factory-ftp-hive-blob)

<span data-ttu-id="6eb80-131">Pensez tooshare libre vos modèles Azure Data Factory à [démarrage rapide Azure](https://azure.microsoft.com/documentation/templates/).</span><span class="sxs-lookup"><span data-stu-id="6eb80-131">Feel free tooshare your Azure Data Factory templates at [Azure Quick start](https://azure.microsoft.com/documentation/templates/).</span></span> <span data-ttu-id="6eb80-132">Consultez toohello [guide de contribution au](https://github.com/Azure/azure-quickstart-templates/tree/master/1-CONTRIBUTION-GUIDE) lors du développement de modèles qui peuvent être partagées via ce référentiel.</span><span class="sxs-lookup"><span data-stu-id="6eb80-132">Refer toohello [contribution guide](https://github.com/Azure/azure-quickstart-templates/tree/master/1-CONTRIBUTION-GUIDE) while developing templates that can be shared via this repository.</span></span>

<span data-ttu-id="6eb80-133">Hello les sections suivantes fournit des détails sur la définition des ressources de la fabrique de données dans un modèle de gestionnaire de ressources.</span><span class="sxs-lookup"><span data-stu-id="6eb80-133">hello following sections provide details about defining Data Factory resources in a Resource Manager template.</span></span>

## <a name="defining-data-factory-resources-in-templates"></a><span data-ttu-id="6eb80-134">Définition de ressources Data Factory dans les modèles</span><span class="sxs-lookup"><span data-stu-id="6eb80-134">Defining Data Factory resources in templates</span></span>
<span data-ttu-id="6eb80-135">modèle de niveau supérieur de Hello permettant de définir une fabrique de données est la suivante :</span><span class="sxs-lookup"><span data-stu-id="6eb80-135">hello top-level template for defining a data factory is:</span></span>

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

### <a name="define-data-factory"></a><span data-ttu-id="6eb80-136">Définir une fabrique de données</span><span class="sxs-lookup"><span data-stu-id="6eb80-136">Define data factory</span></span>
<span data-ttu-id="6eb80-137">Vous définissez une fabrique de données dans le modèle de gestionnaire de ressources hello comme indiqué dans hello suivant l’exemple :</span><span class="sxs-lookup"><span data-stu-id="6eb80-137">You define a data factory in hello Resource Manager template as shown in hello following sample:</span></span>

```JSON
"resources": [
{
    "name": "[variables('<mydataFactoryName>')]",
    "apiVersion": "2015-10-01",
    "type": "Microsoft.DataFactory/datafactories",
    "location": "East US"
}
```
<span data-ttu-id="6eb80-138">Hello dataFactoryName est défini dans « variables » en tant que :</span><span class="sxs-lookup"><span data-stu-id="6eb80-138">hello dataFactoryName is defined in “variables” as:</span></span>

```JSON
"dataFactoryName": "[concat('<myDataFactoryName>', uniqueString(resourceGroup().id))]",
```

### <a name="define-linked-services"></a><span data-ttu-id="6eb80-139">Définir les services liés</span><span class="sxs-lookup"><span data-stu-id="6eb80-139">Define linked services</span></span>

```JSON
"type": "linkedservices",
"name": "[variables('<LinkedServiceName>')]",
"apiVersion": "2015-10-01",
"dependsOn": [ "[variables('<dataFactoryName>')]" ],
"properties": {
    ...
}
```

<span data-ttu-id="6eb80-140">Consultez [Service lié de stockage](data-factory-azure-blob-connector.md#azure-storage-linked-service) ou [de calcul des Services liés](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) pour plus d’informations sur les propriétés JSON hello pour le service lié de hello spécifique, vous souhaitez toodeploy.</span><span class="sxs-lookup"><span data-stu-id="6eb80-140">See [Storage Linked Service](data-factory-azure-blob-connector.md#azure-storage-linked-service) or [Compute Linked Services](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details about hello JSON properties for hello specific linked service you wish toodeploy.</span></span> <span data-ttu-id="6eb80-141">paramètre de « dependsOn » Hello Spécifie le nom de la fabrique de données correspondante hello.</span><span class="sxs-lookup"><span data-stu-id="6eb80-141">hello “dependsOn” parameter specifies name of hello corresponding data factory.</span></span> <span data-ttu-id="6eb80-142">Un exemple de définition d’un service lié pour le stockage Azure est indiqué dans hello JSON définition :</span><span class="sxs-lookup"><span data-stu-id="6eb80-142">An example of defining a linked service for Azure Storage is shown in hello following JSON definition:</span></span>

### <a name="define-datasets"></a><span data-ttu-id="6eb80-143">Définir les jeux de données</span><span class="sxs-lookup"><span data-stu-id="6eb80-143">Define datasets</span></span>

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
<span data-ttu-id="6eb80-144">Consultez trop[prise en charge des magasins de données](data-factory-data-movement-activities.md#supported-data-stores-and-formats) pour plus d’informations sur les propriétés JSON hello pour le type de jeu de données spécifique hello vous souhaitez toodeploy.</span><span class="sxs-lookup"><span data-stu-id="6eb80-144">Refer too[Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) for details about hello JSON properties for hello specific dataset type you wish toodeploy.</span></span> <span data-ttu-id="6eb80-145">Remarque hello « dependsOn » paramètre spécifie le nom de données correspondantes de hello service lié de fabrique et stockage.</span><span class="sxs-lookup"><span data-stu-id="6eb80-145">Note hello “dependsOn” parameter specifies name of hello corresponding data factory and storage linked service.</span></span> <span data-ttu-id="6eb80-146">Un exemple de définition de type de jeu de données de stockage d’objets blob Azure est indiqué dans hello JSON définition :</span><span class="sxs-lookup"><span data-stu-id="6eb80-146">An example of defining dataset type of Azure blob storage is shown in hello following JSON definition:</span></span>

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

### <a name="define-pipelines"></a><span data-ttu-id="6eb80-147">Définir les pipelines</span><span class="sxs-lookup"><span data-stu-id="6eb80-147">Define pipelines</span></span>

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

<span data-ttu-id="6eb80-148">Consultez trop[définition de pipelines](data-factory-create-pipelines.md#pipeline-json) pour plus d’informations sur les propriétés JSON hello permettant de définir hello pipeline spécifique et des activités vous souhaitez toodeploy.</span><span class="sxs-lookup"><span data-stu-id="6eb80-148">Refer too[defining pipelines](data-factory-create-pipelines.md#pipeline-json) for details about hello JSON properties for defining hello specific pipeline and activities you wish toodeploy.</span></span> <span data-ttu-id="6eb80-149">Remarque hello « dependsOn » paramètre spécifie le nom de la fabrique de données hello et les services liés correspondants ou les jeux de données.</span><span class="sxs-lookup"><span data-stu-id="6eb80-149">Note hello “dependsOn” parameter specifies name of hello data factory, and any corresponding linked services or datasets.</span></span> <span data-ttu-id="6eb80-150">Hello extrait de code JSON de suivant montre un pipeline qui copie les données de stockage d’objets Blob Azure tooAzure base de données SQL :</span><span class="sxs-lookup"><span data-stu-id="6eb80-150">An example of a pipeline that copies data from Azure Blob Storage tooAzure SQL Database is shown in hello following JSON snippet:</span></span>

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
        "description": "Copy data frm Azure blob tooAzure SQL",
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
## <a name="parameterizing-data-factory-template"></a><span data-ttu-id="6eb80-151">Paramétrage du modèle Data Factory</span><span class="sxs-lookup"><span data-stu-id="6eb80-151">Parameterizing Data Factory template</span></span>
<span data-ttu-id="6eb80-152">Pour connaître les meilleures pratiques de paramétrage, consultez [Bonnes pratiques relatives à la création de modèles Azure Resource Manager](../azure-resource-manager/resource-manager-template-best-practices.md#parameters).</span><span class="sxs-lookup"><span data-stu-id="6eb80-152">For best practices on parameterizing, see [Best practices for creating Azure Resource Manager templates](../azure-resource-manager/resource-manager-template-best-practices.md#parameters) article.</span></span> <span data-ttu-id="6eb80-153">En général, l’utilisation des paramètres doit être minimale, surtout s’il est possible d’utiliser des variables à la place.</span><span class="sxs-lookup"><span data-stu-id="6eb80-153">In general, parameter usage should be minimized, especially if variables can be used instead.</span></span> <span data-ttu-id="6eb80-154">Fournir uniquement des paramètres Bonjour les scénarios suivants :</span><span class="sxs-lookup"><span data-stu-id="6eb80-154">Only provide parameters in hello following scenarios:</span></span>

* <span data-ttu-id="6eb80-155">Les paramètres varient selon l’environnement (exemple : développement, test et production)</span><span class="sxs-lookup"><span data-stu-id="6eb80-155">Settings vary by environment (example: development, test, and production)</span></span>
* <span data-ttu-id="6eb80-156">les clés secrètes (notamment les mots de passe) ;</span><span class="sxs-lookup"><span data-stu-id="6eb80-156">Secrets (such as passwords)</span></span>

<span data-ttu-id="6eb80-157">Si vous avez besoin des secrets toopull de [Azure Key Vault](../key-vault/key-vault-get-started.md) lors du déploiement des entités de Azure Data Factory à l’aide de modèles, spécifiez hello **coffre de clés** et **nom secret** comme dans Hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="6eb80-157">If you need toopull secrets from [Azure Key Vault](../key-vault/key-vault-get-started.md) when deploying Azure Data Factory entities using templates, specify hello **key vault** and **secret name** as shown in hello following example:</span></span>

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
> <span data-ttu-id="6eb80-158">Pendant l’exportation de modèles pour les fabriques de données existante est actuellement pas encore pris en charge, il est hello fonctionne.</span><span class="sxs-lookup"><span data-stu-id="6eb80-158">While exporting templates for existing data factories is currently not yet supported, it is in hello works.</span></span>
>
>
