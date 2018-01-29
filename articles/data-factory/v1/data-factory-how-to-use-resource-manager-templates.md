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
ms.date: 01/10/2018
ms.author: shlo
robots: noindex
ms.openlocfilehash: e6dbac2f88df3b7c2e4d7f982fc9a573e3d6e62f
ms.sourcegitcommit: 9cc3d9b9c36e4c973dd9c9028361af1ec5d29910
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/23/2018
---
# <a name="use-templates-to-create-azure-data-factory-entities"></a>Utilisation de modèles pour créer des entités Azure Data Factory
> [!NOTE]
> Cet article s’applique à la version 1 de Data factory, qui est généralement disponible (GA). 

## <a name="overview"></a>Vue d’ensemble
Lors de l’utilisation d’Azure Data Factory pour vos besoins d’intégration de données, vous pourriez être amené à réutiliser le même modèle dans différents environnements ou à implémenter la même tâche de façon répétée dans la même solution. Les modèles vous aident à implémenter et à gérer ces scénarios de manière simple. Les modèles dans Azure Data Factory sont parfaitement adaptés aux scénarios qui impliquent la réutilisation et la répétition.

Prenons le cas d’une entreprise qui compte 10 usines de fabrication dans le monde entier. Les journaux de chaque usine sont stockés dans une base de données SQL Server locale distincte. L’entreprise souhaite créer un entrepôt de données unique dans le cloud pour l’analyse ad-hoc. Elle souhaite également avoir la même logique mais des configurations différentes pour les environnements de développement, de test et de production.

Dans ce cas, une tâche doit être répétée dans le même environnement, mais avec des valeurs différentes dans les 10 entrepôts de données pour chaque usine de fabrication. Le facteur de **répétition** est donc présent. La création de modèles permet l’abstraction de ce flux générique (autrement dit, les pipelines ayant les mêmes activités dans chaque entrepôt de données), mais utilise un fichier de paramètres distinct pour chaque usine de fabrication.

En outre, étant donné que l’entreprise souhaite déployer ces 10 entrepôts de données plusieurs fois dans différents environnements, les modèles peuvent utiliser cette **réutilisation** à l’aide de fichiers de paramètres distincts pour les environnements de développement, de test et de production.

## <a name="templating-with-azure-resource-manager"></a>Création de modèles avec Azure Resource Manager
Les [modèles Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md#template-deployment) constituent une excellente méthode de création de modèles dans Azure Data Factory. Les modèles Resource Manager définissent l’infrastructure et la configuration de votre solution Azure à l’aide d’un fichier JSON. Étant donné que les modèles Azure Resource Manager fonctionnent avec tous les services ou la plupart des services Azure, ils peuvent être utilisés pour gérer facilement toutes les ressources de vos actifs Azure. Pour en savoir plus sur les modèles Resource Manager en général, consultez [Création de modèles Azure Resource Manager](../../azure-resource-manager/resource-group-authoring-templates.md).

## <a name="tutorials"></a>Didacticiels
Reportez-vous aux didacticiels suivants pour obtenir des instructions détaillées sur la création d’entités Data Factory à l’aide de modèles Resource Manager :

* [Didacticiel : Créer un pipeline pour copier des données à l’aide du modèle Azure Resource Manager](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
* [Didacticiel : Créer un pipeline pour traiter des données à l’aide du modèle Azure Resource Manager](data-factory-build-your-first-pipeline.md)

## <a name="data-factory-templates-on-github"></a>Modèles Data Factory sur GitHub
Découvrez les modèles de démarrage rapide Azure suivants sur GitHub :

* [Créer une fabrique de données pour copier des données à partir du Stockage Blob Azure vers une base de données SQL Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-blob-to-sql-copy)
* [Créer une fabrique de données avec une activité Hive sur un cluster Azure HDInsight](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-hive-transformation)
* [Créer une fabrique de données pour copier des données à partir de Salesforce vers des objets blob Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-salesforce-to-blob-copy)
* [Créer une fabrique de données qui lié les activités : copie des données à partir d’un serveur FTP vers des objets Blob Azure, appelle un script hive sur un cluster HDInsight à la demande pour transformer les données et copie le résultat dans Azure SQL Database](https://github.com/Azure/azure-quickstart-templates/tree/master/201-data-factory-ftp-hive-blob)

N’hésitez pas à partager vos modèles Azure Data Factory dans [Démarrage rapide d’Azure](https://azure.microsoft.com/documentation/templates/). Reportez-vous au [guide de contribution](https://github.com/Azure/azure-quickstart-templates/tree/master/1-CONTRIBUTION-GUIDE) lors du développement de modèles qui peuvent être partagés via ce référentiel.

Les sections suivantes fournissent plus d’informations sur la définition de ressources Data Factory dans un modèle Resource Manager.

## <a name="defining-data-factory-resources-in-templates"></a>Définition de ressources Data Factory dans les modèles
Le modèle de niveau supérieur pour la définition d’une fabrique de données est :

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

### <a name="define-data-factory"></a>Définir une fabrique de données
Vous définissez une fabrique de données dans le modèle Resource Manager, comme indiqué dans l’exemple suivant :

```JSON
"resources": [
{
    "name": "[variables('<mydataFactoryName>')]",
    "apiVersion": "2015-10-01",
    "type": "Microsoft.DataFactory/datafactories",
    "location": "East US"
}
```
Le dataFactoryName est défini dans « variables » en tant que :

```JSON
"dataFactoryName": "[concat('<myDataFactoryName>', uniqueString(resourceGroup().id))]",
```

### <a name="define-linked-services"></a>Définir les services liés

```JSON
"type": "linkedservices",
"name": "[variables('<LinkedServiceName>')]",
"apiVersion": "2015-10-01",
"dependsOn": [ "[variables('<dataFactoryName>')]" ],
"properties": {
    ...
}
```

Consultez [Service de stockage lié](data-factory-azure-blob-connector.md#azure-storage-linked-service) ou [Services liés de calcul](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) pour plus d’informations sur les propriétés JSON pour le service lié spécifique que vous souhaitez déployer. Le paramètre « dependsOn » spécifie le nom de la fabrique de données correspondante. Un exemple de définition d’un service lié pour le Stockage Azure est indiqué dans la définition JSON suivante :

### <a name="define-datasets"></a>Définir les jeux de données

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
Consultez [Magasins de données pris en charge](data-factory-data-movement-activities.md#supported-data-stores-and-formats) pour plus d’informations sur les propriétés JSON pour le type de jeu de données spécifique que vous souhaitez déployer. Notez que le paramètre « dependsOn » spécifie le nom de la fabrique de données et du service lié de stockage correspondants. Un exemple de définition d’un type de jeu de données pour le Stockage Blob Azure est indiqué dans la définition JSON suivante :

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

### <a name="define-pipelines"></a>Définir les pipelines

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

Consultez [Définition des pipelines](data-factory-create-pipelines.md#pipeline-json) pour plus d’informations sur les propriétés JSON permettant de définir le pipeline et les activités spécifiques que vous souhaitez déployer. Notez que le paramètre « dependsOn » spécifie le nom de la fabrique de données, ainsi que les services liés ou les jeux de données correspondants. Un exemple de pipeline qui copie des données depuis le Stockage Blob Azure vers une base de données SQL Azure est indiqué dans l’extrait de code JSON suivant :

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
## <a name="parameterizing-data-factory-template"></a>Paramétrage du modèle Data Factory
Pour connaître les meilleures pratiques de paramétrage, consultez [Bonnes pratiques relatives à la création de modèles Azure Resource Manager](../../azure-resource-manager/resource-manager-template-best-practices.md). En général, l’utilisation des paramètres doit être minimale, surtout s’il est possible d’utiliser des variables à la place. Fournissez uniquement des paramètres dans les scénarios suivants :

* Les paramètres varient selon l’environnement (exemple : développement, test et production)
* les clés secrètes (notamment les mots de passe) ;

Si vous avez besoin d’extraire des clés secrètes à partir [d’Azure Key Vault](../../key-vault/key-vault-get-started.md) lors du déploiement d’entités Azure Data Factory à l’aide de modèles, spécifiez le **coffre de clés** et le **nom secret** comme indiqué dans l’exemple suivant :

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
> L’exportation de modèles pour les fabriques de données existantes n’est actuellement pas prise en charge, mais nous y travaillons.
>
>
