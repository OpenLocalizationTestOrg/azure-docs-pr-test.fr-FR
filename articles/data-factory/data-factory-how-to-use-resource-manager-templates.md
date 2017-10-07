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
# <a name="use-templates-toocreate-azure-data-factory-entities"></a>Utiliser des entités de modèles toocreate Azure Data Factory
## <a name="overview"></a>Vue d'ensemble
Lors de l’utilisation d’Azure Data Factory à vos besoins d’intégration de données, vous pouvez être obligé de réutilisation hello même modèle dans différents environnements ou implémentation hello même tâche de façon répétée dans hello même solution. Les modèles vous aident à implémenter et à gérer ces scénarios de manière simple. Les modèles dans Azure Data Factory sont parfaitement adaptés aux scénarios qui impliquent la réutilisation et la répétition.

Imaginons une situation hello où une organisation a des 10 unités de fabrication dans Bonjour. journaux de Hello à partir de chaque plante sont stockés dans une base de données SQL Server local distinct. société de Hello veut toobuild un entrepôt de données unique dans le cloud de hello pour ad-hoc analytique. Elle souhaite également toohave hello même logique, mais différentes configurations pour les environnements de développement, test et de production.

Dans ce cas, une tâche doit toobe répété dans hello même environnement, mais avec des valeurs différentes sur hello 10 fabriques de données pour chaque installation. Le facteur de **répétition** est donc présent. Création de modèles permet abstraction hello de ce flux générique (autrement dit, pipelines ayant hello activités mêmes dans chaque fabrique de données), mais utilise un fichier de paramètres distincts pour chaque installation.

En outre, comme hello organisation souhaite toodeploy ces usines 10 données plusieurs fois entre les différents environnements, modèles peuvent utiliser ce **réutilisabilité** en utilisant des fichiers de paramètres distincts pour le développement, test, et environnements de production.

## <a name="templating-with-azure-resource-manager"></a>Création de modèles avec Azure Resource Manager
[Les modèles de gestionnaire de ressources Azure](../azure-resource-manager/resource-group-overview.md#template-deployment) sont une création de modèles tooachieve idéale dans Azure Data Factory. Les modèles de gestionnaire de ressources définissent l’infrastructure de hello et la configuration de votre solution Azure via un fichier JSON. Étant donné que les modèles Azure Resource Manager fonctionnent avec tous les/la plupart des services Azure, il peut être largement utilisé tooeasily gérer toutes les ressources de vos ressources Azure. Consultez [les modèles de programmation Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) toolearn savoir plus sur hello en général les modèles du Gestionnaire de ressources.

## <a name="tutorials"></a>Didacticiels
Consultez hello suivant des didacticiels pour les entités de fabrique de données toocreate des instructions détaillées en utilisant des modèles de gestionnaire de ressources :

* [Didacticiel : Créer un toocopy de données de pipeline à l’aide du modèle Azure Resource Manager](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
* [Didacticiel : Créer un tooprocess de données de pipeline à l’aide du modèle Azure Resource Manager](data-factory-build-your-first-pipeline.md)

## <a name="data-factory-templates-on-github"></a>Modèles Data Factory sur GitHub
Passez en revue hello suivant des modèles de démarrage rapide d’Azure sur GitHub :

* [Créer une fabrique toocopy de données à partir du stockage d’objets Blob Azure tooAzure base de données SQL](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-blob-to-sql-copy)
* [Créer une fabrique de données avec une activité Hive sur un cluster Azure HDInsight](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-hive-transformation)
* [Créer une fabrique toocopy de données à partir d’objets BLOB tooAzure de Salesforce](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-salesforce-to-blob-copy)
* [Créer une fabrique de données qui est lié activités : copie des données à partir d’un serveur FTP tooAzure BLOB, appelle un script hive sur un à la demande HDInsight cluster tootransform hello de données et copie le résultat dans la base de données SQL Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-data-factory-ftp-hive-blob)

Pensez tooshare libre vos modèles Azure Data Factory à [démarrage rapide Azure](https://azure.microsoft.com/documentation/templates/). Consultez toohello [guide de contribution au](https://github.com/Azure/azure-quickstart-templates/tree/master/1-CONTRIBUTION-GUIDE) lors du développement de modèles qui peuvent être partagées via ce référentiel.

Hello les sections suivantes fournit des détails sur la définition des ressources de la fabrique de données dans un modèle de gestionnaire de ressources.

## <a name="defining-data-factory-resources-in-templates"></a>Définition de ressources Data Factory dans les modèles
modèle de niveau supérieur de Hello permettant de définir une fabrique de données est la suivante :

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
Vous définissez une fabrique de données dans le modèle de gestionnaire de ressources hello comme indiqué dans hello suivant l’exemple :

```JSON
"resources": [
{
    "name": "[variables('<mydataFactoryName>')]",
    "apiVersion": "2015-10-01",
    "type": "Microsoft.DataFactory/datafactories",
    "location": "East US"
}
```
Hello dataFactoryName est défini dans « variables » en tant que :

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

Consultez [Service lié de stockage](data-factory-azure-blob-connector.md#azure-storage-linked-service) ou [de calcul des Services liés](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) pour plus d’informations sur les propriétés JSON hello pour le service lié de hello spécifique, vous souhaitez toodeploy. paramètre de « dependsOn » Hello Spécifie le nom de la fabrique de données correspondante hello. Un exemple de définition d’un service lié pour le stockage Azure est indiqué dans hello JSON définition :

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
Consultez trop[prise en charge des magasins de données](data-factory-data-movement-activities.md#supported-data-stores-and-formats) pour plus d’informations sur les propriétés JSON hello pour le type de jeu de données spécifique hello vous souhaitez toodeploy. Remarque hello « dependsOn » paramètre spécifie le nom de données correspondantes de hello service lié de fabrique et stockage. Un exemple de définition de type de jeu de données de stockage d’objets blob Azure est indiqué dans hello JSON définition :

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

Consultez trop[définition de pipelines](data-factory-create-pipelines.md#pipeline-json) pour plus d’informations sur les propriétés JSON hello permettant de définir hello pipeline spécifique et des activités vous souhaitez toodeploy. Remarque hello « dependsOn » paramètre spécifie le nom de la fabrique de données hello et les services liés correspondants ou les jeux de données. Hello extrait de code JSON de suivant montre un pipeline qui copie les données de stockage d’objets Blob Azure tooAzure base de données SQL :

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
## <a name="parameterizing-data-factory-template"></a>Paramétrage du modèle Data Factory
Pour connaître les meilleures pratiques de paramétrage, consultez [Bonnes pratiques relatives à la création de modèles Azure Resource Manager](../azure-resource-manager/resource-manager-template-best-practices.md#parameters). En général, l’utilisation des paramètres doit être minimale, surtout s’il est possible d’utiliser des variables à la place. Fournir uniquement des paramètres Bonjour les scénarios suivants :

* Les paramètres varient selon l’environnement (exemple : développement, test et production)
* les clés secrètes (notamment les mots de passe) ;

Si vous avez besoin des secrets toopull de [Azure Key Vault](../key-vault/key-vault-get-started.md) lors du déploiement des entités de Azure Data Factory à l’aide de modèles, spécifiez hello **coffre de clés** et **nom secret** comme dans Hello l’exemple suivant :

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
> Pendant l’exportation de modèles pour les fabriques de données existante est actuellement pas encore pris en charge, il est hello fonctionne.
>
>
