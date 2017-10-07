---
title: "Didacticiel : Créer un pipeline à l’aide du modèle Azure Resource Manager | Microsoft Docs"
description: "Dans ce didacticiel, vous créez un pipeline Azure Data Factory en utilisant un modèle Azure Resource Manager. Ce pipeline copie des données à partir d’une base de données SQL Azure de tooan stockage blob Azure."
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
ms.openlocfilehash: 1c7567cb0423f7ce3e0cab2d77a4d861b70eb56b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-use-azure-resource-manager-template-toocreate-a-data-factory-pipeline-toocopy-data"></a>Didacticiel : Utiliser Azure Resource Manager modèle toocreate données toocopy de pipeline de fabrique de données 
> [!div class="op_single_selector"]
> * [Vue d’ensemble et étapes préalables requises](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [Assistant de copie](data-factory-copy-data-wizard-tutorial.md)
> * [Portail Azure](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)
> * [Modèle Azure Resource Manager](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [API REST](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [API .NET](data-factory-copy-activity-tutorial-using-dotnet-api.md)
> 
> 

Ce didacticiel vous montre comment toouse un toocreate de modèle Azure Resource Manager une fabrique de données Azure. le pipeline de données Hello dans ce didacticiel copie des données à partir d’un magasin de données de destination source données magasin tooa. Il ne transforme pas les données de sortie de données d’entrée tooproduce. Pour obtenir un didacticiel sur la façon de tootransform les données à l’aide d’Azure Data Factory, consultez [didacticiel : créer un pipeline de données tootransform à l’aide de cluster Hadoop](data-factory-build-your-first-pipeline.md).

Dans ce didacticiel, vous créez un pipeline avec une activité : activité de copie. activité de copie Hello copie des données à partir d’un magasin de données de données pris en charge magasin tooa récepteur pris en charge. Pour obtenir la liste des magasins de données pris en charge en tant que sources et récepteurs, consultez [Magasins de données pris en charge](data-factory-data-movement-activities.md#supported-data-stores-and-formats). activité Hello est rendue possible par un service globalement disponible qui permettre copier des données entre différentes banques de données de manière sécurisée, fiable et évolutive. Pour plus d’informations sur l’activité de copie de hello, consultez [les activités de déplacement des données](data-factory-data-movement-activities.md).

Un pipeline peut contenir plusieurs activités. De plus, vous pouvez concaténer les deux activités (exécutée une activité après l’autre) en définissant le dataset de sortie hello d’une activité hello d’entrée dataset Hello autre activité. Pour plus d’informations, consultez [Plusieurs activités dans un pipeline](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline). 

> [!NOTE] 
> le pipeline de données Hello dans ce didacticiel copie des données à partir d’un magasin de données de destination source données magasin tooa. Pour obtenir un didacticiel sur la façon de tootransform les données à l’aide d’Azure Data Factory, consultez [didacticiel : créer un pipeline de données tootransform à l’aide de cluster Hadoop](data-factory-build-your-first-pipeline.md). 

## <a name="prerequisites"></a>Composants requis
* Passez en revue [vue d’ensemble et conditions préalables](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) et hello complète **condition préalable** étapes.
* Suivez les instructions de [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview) article tooinstall version la plus récente d’Azure PowerShell sur votre ordinateur. Dans ce didacticiel, vous utilisez des entités de fabrique de données toodeploy PowerShell. 
* (facultatif) Consultez [de création de modèles de gestionnaire de ressources Azure](../azure-resource-manager/resource-group-authoring-templates.md) toolearn sur les modèles Azure Resource Manager.

## <a name="in-this-tutorial"></a>Dans ce didacticiel
Dans ce didacticiel, vous créez une fabrique de données avec hello suivant des entités de fabrique de données :

| Entité | Description |
| --- | --- |
| Service lié Azure Storage |Lie votre fabrique de données toohello compte Azure Storage. Le stockage Azure est le magasin de données source hello et base de données SQL Azure est un magasin de données de récepteur de hello pour l’activité de copie hello dans le didacticiel de hello. Il spécifie le compte de stockage hello qui contient les données d’entrée pour l’activité de copie hello de salutation. |
| Service lié pour base de données SQL Azure |Lie votre fabrique de données de toohello de base de données SQL Azure. Il spécifie hello SQL Azure de base de données qui conserve les données de sortie de hello pour l’activité de copie hello. |
| Jeu de données d'entrée d'objet Blob Azure |Fait référence toohello lié Azure Storage service. Hello service lié fait référence compte de stockage Azure tooan et dataset d’objets Blob Azure hello spécifie hello conteneur, dossier et nom de fichier dans le stockage hello qui contient les données d’entrée hello. |
| Jeu de données de sortie SQL Azure |Désigne le service lié SQL Azure de toohello. service lié SQL Azure de Hello fait référence serveur SQL Azure de tooan et jeu de données SQL Azure hello Spécifie le nom hello de table hello qui contient les données de sortie hello. |
| Pipeline de données |pipeline de Hello a une activité de copie qui prend le dataset d’objets blob Azure hello en tant qu’entrée de type et hello du jeu de données SQL Azure comme sortie. activité de copie Hello copie des données à partir d’une table de tooa d’objets blob Azure dans la base de données SQL Azure hello. |

Une fabrique de données peut avoir un ou plusieurs pipelines. Un pipeline peut contenir une ou plusieurs activités. Il existe deux types d’activités : les [activités de déplacement des données](data-factory-data-movement-activities.md) et les [activités de transformation des données](data-factory-data-transformation-activities.md). Dans ce didacticiel, vous créez un pipeline avec une activité (activité de copie).

![Copier des objets Blob Azure tooAzure base de données SQL](media/data-factory-copy-activity-tutorial-using-azure-resource-manager-template/CopyBlob2SqlDiagram.png) 

Hello section suivante fournit modèle de gestionnaire de ressources hello complète permettant de définir des entités de fabrique de données afin que vous puissiez exécuter rapidement via hello didacticiel et test hello du modèle. toounderstand chaque entité de la fabrique de données est définie, voir [des entités de fabrique de données dans le modèle de hello](#data-factory-entities-in-the-template) section.

## <a name="data-factory-json-template"></a>Modèle JSON Data Factory
modèle de gestionnaire de ressources du niveau supérieur Hello pour la définition d’une fabrique de données est : 

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
Créez un fichier JSON nommé **ADFCopyTutorialARM.json** dans **C:\ADFGetStarted** dossier avec hello suivant le contenu :

```json
{
    "contentVersion": "1.0.0.0",
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "parameters": {
      "storageAccountName": { "type": "string", "metadata": { "description": "Name of hello Azure storage account that contains hello data toobe copied." } },
      "storageAccountKey": { "type": "securestring", "metadata": { "description": "Key for hello Azure storage account." } },
      "sourceBlobContainer": { "type": "string", "metadata": { "description": "Name of hello blob container in hello Azure Storage account." } },
      "sourceBlobName": { "type": "string", "metadata": { "description": "Name of hello blob in hello container that has hello data toobe copied tooAzure SQL Database table" } },
      "sqlServerName": { "type": "string", "metadata": { "description": "Name of hello Azure SQL Server that will hold hello output/copied data." } },
      "databaseName": { "type": "string", "metadata": { "description": "Name of hello Azure SQL Database in hello Azure SQL server." } },
      "sqlServerUserName": { "type": "string", "metadata": { "description": "Name of hello user that has access toohello Azure SQL server." } },
      "sqlServerPassword": { "type": "securestring", "metadata": { "description": "Password for hello user." } },
      "targetSQLTable": { "type": "string", "metadata": { "description": "Table in hello Azure SQL Database that will hold hello copied data." } 
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
              "start": "2017-05-11T00:00:00Z",
              "end": "2017-05-12T00:00:00Z"
            }
          }
        ]
      }
    ]
  }
```

## <a name="parameters-json"></a>Paramètres JSON
Créez un fichier JSON nommé **ADFCopyTutorialARM-Parameters.json** qui contient les paramètres de modèle de gestionnaire de ressources Azure hello. 

> [!IMPORTANT]
> Spécifiez le nom et la clé de votre compte de stockage Azure pour les paramètres storageAccountName et storageAccountKey.  
> 
> Spécifiez le serveur SQL Azure, la base de données, l’utilisateur et le mot de passe pour les paramètres sqlServerName, databaseName, sqlServerUserName et sqlServerPassword.  

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
    "contentVersion": "1.0.0.0",
    "parameters": { 
        "storageAccountName": { "value": "<Name of hello Azure storage account>"    },
        "storageAccountKey": {
            "value": "<Key for hello Azure storage account>"
        },
        "sourceBlobContainer": { "value": "adftutorial" },
        "sourceBlobName": { "value": "emp.txt" },
        "sqlServerName": { "value": "<Name of hello Azure SQL server>" },
        "databaseName": { "value": "<Name of hello Azure SQL database>" },
        "sqlServerUserName": { "value": "<Name of hello user who has access toohello Azure SQL database>" },
        "sqlServerPassword": { "value": "<password for hello user>" },
        "targetSQLTable": { "value": "emp" }
    }
}
```

> [!IMPORTANT]
> Vous avez peut-être fichiers JSON de paramètres distincts pour le développement, test et les environnements de production que vous pouvez utiliser avec hello même modèle JSON de fabrique de données. En utilisant un script PowerShell, vous pouvez automatiser le déploiement des entités Data Factory dans ces environnements.  
> 
> 

## <a name="create-data-factory"></a>Créer une fabrique de données
1. Démarrer **Azure PowerShell** et hello exécution de commande suivante :
   * Exécutez hello suivant de commande et entrez le nom d’utilisateur hello et le mot de passe que vous utilisez toosign dans toohello portail Azure.
   
    ```PowerShell
    Login-AzureRmAccount    
    ```  
   * Exécutez hello suivant commande tooview tous les abonnements hello pour ce compte.
   
    ```PowerShell
    Get-AzureRmSubscription
    ```   
   * Tooselect hello abonnement toowork avec la commande suivante d’exécution hello.
    
    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <SUBSCRIPTION NAME> | Set-AzureRmContext
    ```    
2. Hello exécution suivant des entités de fabrique de données toodeploy de commande à l’aide du modèle de gestionnaire de ressources hello que vous avez créé à l’étape 1.

    ```PowerShell   
    New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile C:\ADFGetStarted\ADFCopyTutorialARM.json -TemplateParameterFile C:\ADFGetStarted\ADFCopyTutorialARM-Parameters.json
    ```

## <a name="monitor-pipeline"></a>Surveillance d’un pipeline

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com) à l’aide de votre compte Azure.
2. Cliquez sur **fabriques de données** sur hello gauche menu (ou) cliquez sur **davantage de services** et cliquez sur **fabriques de données** sous **INTELLIGENCE + ANALYTICS** catégorie.
   
    ![Menu Fabriques de données](media/data-factory-copy-activity-tutorial-using-azure-resource-manager-template/data-factories-menu.png)
3. Bonjour **fabriques de données** page, rechercher et trouver votre fabrique de données (AzureBlobToAzureSQLDatabaseDF). 
   
    ![Recherche d’une fabrique de données](media/data-factory-copy-activity-tutorial-using-azure-resource-manager-template/search-for-data-factory.png)  
4. Cliquez sur votre fabrique de données Azure. Vous consultez la page d’accueil hello de fabrique de données hello.
   
    ![Page d’accueil de la fabrique de données](media/data-factory-copy-activity-tutorial-using-azure-resource-manager-template/data-factory-home-page.png)  
6. Suivez les instructions à partir de [analyser des jeux de données et le pipeline](data-factory-copy-activity-tutorial-using-azure-portal.md#monitor-pipeline) pipeline de hello toomonitor et jeux de données que vous avez créé dans ce didacticiel. Pour le moment, Visual Studio ne prend pas en charge la surveillance des pipelines Data Factory.
7. Lorsqu’une tranche est Bonjour **prêt** d’état, vérifiez que les données de salutation soient copié toohello **emp** table dans la base de données SQL Azure hello.


Pour plus d’informations sur la façon dont pipeline de toomonitor toouse panneaux portail Azure et les jeux de données vous avez créé dans ce didacticiel, consultez [analyser des jeux de données et de pipeline](data-factory-monitor-manage-pipelines.md) .

Pour plus d’informations sur comment toomonitor application toouse hello analyse et gestion de vos données pipelines, consultez [analyse et de gérer les pipelines Azure Data Factory à l’aide de la surveillance des applications](data-factory-monitor-manage-app.md).

## <a name="data-factory-entities-in-hello-template"></a>Entités de fabrique de données dans le modèle de hello
### <a name="define-data-factory"></a>Définir une fabrique de données
Vous définissez une fabrique de données dans le modèle de gestionnaire de ressources hello comme indiqué dans hello suivant l’exemple :  

```json
"resources": [
{
    "name": "[variables('dataFactoryName')]",
    "apiVersion": "2015-10-01",
    "type": "Microsoft.DataFactory/datafactories",
    "location": "West US"
}
```

Hello dataFactoryName est défini comme : 

```json
"dataFactoryName": "[concat('AzureBlobToAzureSQLDatabaseDF', uniqueString(resourceGroup().id))]"
```

Il s’agit d’une chaîne unique en fonction de l’ID de groupe de ressources hello.  

### <a name="defining-data-factory-entities"></a>Définition des entités Data Factory
Hello des entités de fabrique de données suivantes sont définies dans le modèle JSON hello : 

1. [Service lié Azure Storage](#azure-storage-linked-service)
2. [Service lié SQL Azure](#azure-sql-database-linked-service)
3. [Jeu de données d’objet blob Azure](#azure-blob-dataset)
4. [Jeu de données SQL Azure](#azure-sql-dataset)
5. [Pipeline de données avec une activité de copie](#data-pipeline)

#### <a name="azure-storage-linked-service"></a>Service lié Azure Storage
Hello AzureStorageLinkedService lie votre fabrique de données toohello compte stockage Azure. Création d’un conteneur et de téléchargé de compte de stockage de données toothis dans le cadre de [conditions préalables](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md). Vous spécifiez le nom de hello et la clé de votre compte de stockage Azure dans cette section. Consultez [service lié Azure Storage](data-factory-azure-blob-connector.md#azure-storage-linked-service) pour plus d’informations sur JSON propriétés utilisées toodefine un stockage Azure le service lié. 

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

Hello connectionString utilise les paramètres storageAccountName et storageAccountKey hello. valeurs Hello pour ces paramètres passés à l’aide d’un fichier de configuration. définition de Hello utilise également des variables : azureStroageLinkedService et dataFactoryName définies dans le modèle de hello. 

#### <a name="azure-sql-database-linked-service"></a>Service lié pour base de données SQL Azure
AzureSqlLinkedService lie votre fabrique de données de toohello de base de données SQL Azure. données Hello sont copiées à partir du stockage d’objets blob hello sont stockées dans cette base de données. Vous avez créé la table emp de hello dans cette base de données dans le cadre de [conditions préalables](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md). Vous spécifiez le nom du serveur SQL Azure hello, nom de la base de données, nom d’utilisateur et mot de passe utilisateur dans cette section. Consultez [service lié Azure SQL](data-factory-azure-sql-connector.md#linked-service-properties) pour plus d’informations sur JSON propriétés utilisées toodefine service lié de SQL Azure.  

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

Hello connectionString utilise sqlServerName, databaseName, sqlServerUserName et paramètres de sqlServerPassword dont les valeurs sont passées à l’aide d’un fichier de configuration. Hello définition utilise également hello suivant des variables de modèle de hello : azureSqlLinkedServiceName, dataFactoryName.

#### <a name="azure-blob-dataset"></a>Jeu de données d’objet blob Azure
service lié Azure storage de Hello spécifie la chaîne de connexion hello service Data Factory utilise au moment de l’exécution tooconnect tooyour compte de stockage Azure. Dans la définition de jeu de données d’objets blob Azure, vous spécifiez des noms de conteneur d’objets blob, de dossier et de fichier qui contient les données d’entrée hello. Consultez [propriétés de jeu de données d’objets Blob Azure](data-factory-azure-blob-connector.md#dataset-properties) pour plus d’informations sur les propriétés utilisées de JSON toodefine un jeu de données d’objets Blob Azure. 

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

#### <a name="azure-sql-dataset"></a>Jeu de données SQL Azure
Vous spécifiez le nom hello de table de hello dans la base de données SQL Azure hello qui contient les données hello copié à partir de hello le stockage Blob Azure. Consultez [propriétés du jeu de données SQL Azure](data-factory-azure-sql-connector.md#dataset-properties) pour plus d’informations sur les propriétés utilisées de JSON toodefine un jeu de données SQL Azure. 

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

#### <a name="data-pipeline"></a>Pipeline de données
Vous définissez un pipeline qui copie les données de jeu de données de SQL Azure hello blob Azure dataset toohello. Consultez [JSON de Pipeline](data-factory-create-pipelines.md#pipeline-json) pour les descriptions des éléments utilisés de JSON toodefine un pipeline dans cet exemple. 

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
          "start": "2017-05-11T00:00:00Z",
          "end": "2017-05-12T00:00:00Z"
    }
}
```

## <a name="reuse-hello-template"></a>Réutiliser le modèle de hello
Dans le didacticiel de hello, vous avez créé un modèle permettant de définir des entités de fabrique de données et un modèle pour passer des valeurs pour les paramètres. pipeline de Hello copie les données d’un stockage Azure compte tooan SQL Azure de base de données spécifié via les paramètres définis. toouse hello même modèle toodeploy Data Factory entités toodifferent des environnements, vous créez un fichier de paramètres pour chaque environnement et l’utilisez lors de la toothat environnement de déploiement.     

Exemple :  

```PowerShell
New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFCopyTutorialARM.json -TemplateParameterFile ADFCopyTutorialARM-Parameters-Dev.json
```
```PowerShell
New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFCopyTutorialARM.json -TemplateParameterFile ADFCopyTutorialARM-Parameters-Test.json
```
```PowerShell
New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFCopyTutorialARM.json -TemplateParameterFile ADFCopyTutorialARM-Parameters-Production.json
```

Notez que hello première commande utilise le fichier de paramètres pour l’environnement de développement hello, deuxième hello un environnement de test et hello un tiers pour l’environnement de production hello.  

Vous pouvez également réutiliser hello modèle tooperform tâches récurrentes. Par exemple, vous devez toocreate plusieurs fabriques de données avec l’un ou plusieurs pipelines qui implémentent hello même logique, mais chaque fabrique de données utilise différents comptes de stockage et de la base de données SQL. Dans ce scénario, vous utilisez hello même modèle Bonjour même environnement (développement, test ou production) avec des paramètres différents fichiers toocreate les fabriques de données.   

## <a name="next-steps"></a>Étapes suivantes
Dans ce didacticiel, vous avez utilisé le stockage Blob Azure comme magasin de données source et une base de données SQL Azure comme banque de données de destination dans une opération de copie. Hello tableau suivant fournit une liste de banques de données pris en charge en tant que sources et destinations par l’activité de copie hello : 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

toolearn sur la banque de données de toocopy vers/à partir de données, cliquez sur lien hello hello magasin de données dans la table de hello.
