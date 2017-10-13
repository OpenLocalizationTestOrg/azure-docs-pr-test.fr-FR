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
robots: noindex
ms.openlocfilehash: 1778a4af004afd45464e37e198d78b4f0977c1c4
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/11/2017
---
# <a name="tutorial-build-your-first-azure-data-factory-using-azure-resource-manager-template"></a>Didacticiel : concevoir votre première fabrique de données Azure à l’aide du modèle Azure Resource Manager
> [!div class="op_single_selector"]
> * [Vue d’ensemble et étapes préalables requises](data-factory-build-your-first-pipeline.md)
> * [Portail Azure](data-factory-build-your-first-pipeline-using-editor.md)
> * [Visual Studio](data-factory-build-your-first-pipeline-using-vs.md)
> * [PowerShell](data-factory-build-your-first-pipeline-using-powershell.md)
> * [Modèle Resource Manager](data-factory-build-your-first-pipeline-using-arm.md)
> * [API REST](data-factory-build-your-first-pipeline-using-rest-api.md)
> 
> 

Dans cet article, vous utilisez un modèle Azure Resource Manager pour créer votre première fabrique de données Azure. Pour suivre le didacticiel avec d’autres outils/Kits de développement logiciel (SDK), sélectionnez une des options dans la liste déroulante.

Le pipeline dans ce didacticiel a une activité : **Activité HDInsight Hive**. Cette activité exécute un script Hive sur un cluster HDInsight qui transforme des données d’entrée pour produire des données de sortie. Le pipeline est programmé pour s’exécuter une fois par mois entre les heures de début et de fin spécifiées. 

> [!NOTE]
> Dans ce didacticiel, le pipeline de données transforme les données d’entrée pour produire des données de sortie. Pour un didacticiel sur la copie de données à l’aide d’Azure Data Factory, consultez [Copie de données Blob Storage vers une base de données SQL à l’aide de Data Factory](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).
> 
> Le pipeline dans ce didacticiel a une seule activité de type : HDInsightHive. Un pipeline peut contenir plusieurs activités. En outre, vous pouvez chaîner deux activités (une après l’autre) en configurant le jeu de données de sortie d’une activité en tant que jeu de données d’entrée de l’autre activité. Pour plus d’informations, consultez [Planification et exécution dans Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline). 

## <a name="prerequisites"></a>Composants requis
* Lisez l’article [Vue d’ensemble du didacticiel](data-factory-build-your-first-pipeline.md) et effectuez les **étapes préalables requises** .
* Suivez les instructions de l’article [Installation et configuration d’Azure PowerShell](/powershell/azure/overview) pour installer la dernière version d’Azure PowerShell sur votre ordinateur.
* Consultez [Création de modèles Azure Resource Manager](../../azure-resource-manager/resource-group-authoring-templates.md) pour en savoir plus sur les modèles Azure Resource Manager. 

## <a name="in-this-tutorial"></a>Dans ce didacticiel
| Entité | Description |
| --- | --- |
| Service lié Azure Storage |Lie votre compte Stockage Azure à la fabrique de données. Le compte Stockage Azure contient les données d’entrée et de sortie pour le pipeline de cet exemple. |
| Service lié à la demande HDInsight |Lie un cluster HDInsight à la demande à la fabrique de données. Le cluster est automatiquement créé pour traiter les données puis est supprimé une fois le traitement terminé. |
| Jeu de données d'entrée d'objet Blob Azure |Fait référence au service Stockage Azure lié. Le service lié fait référence à un compte de stockage Azure, et les jeux de données d’objet Blob Azure spécifie le conteneur, le dossier et le nom de fichier dans le stockage contenant les données d’entrée. |
| Jeu de données de sortie d’objet Blob Azure |Fait référence au service Stockage Azure lié. Le service lié fait référence à un compte de stockage Azure, et les jeux de données d’objet Blob Azure spécifie le conteneur, le dossier et le nom de fichier dans le stockage contenant les données de sortie. |
| Pipeline de données |Le pipeline exerce une activité de type HDInsightHive, utilise le jeu de données d’entrée et génère le jeu de données de sortie. |

Une fabrique de données peut avoir un ou plusieurs pipelines. Un pipeline peut contenir une ou plusieurs activités. Il existe deux types d’activités : les [activités de déplacement des données](data-factory-data-movement-activities.md) et les [activités de transformation des données](data-factory-data-transformation-activities.md). Dans ce didacticiel, vous créez un pipeline avec une activité (activité Hive).

La section suivante fournit le modèle Resource Manager complet permettant de définir des entités Data Factory pour que vous puissiez rapidement parcourir le didacticiel et tester le modèle. Pour comprendre comment chaque entité Data Factory est définie, consultez la section [Entités Data Factory dans le modèle](#data-factory-entities-in-the-template).

## <a name="data-factory-json-template"></a>Modèle JSON Data Factory
Le modèle Resource Manager de niveau supérieur pour la définition d’une fabrique de données est : 

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
Créez un fichier JSON nommé **ADFTutorialARM.json** dans le dossier **C:\ADFGetStarted** avec le contenu suivant :

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
> Vous trouverez un autre exemple de modèle Resource Manager pour créer une fabrique de données Azure dans le [didacticiel : Créer un pipeline avec activité de copie à l’aide d’un modèle Azure Resource Manager](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md).  
> 
> 

## <a name="parameters-json"></a>Paramètres JSON
Créez un fichier JSON nommé **ADFTutorialARM-Parameters** contient les paramètres du modèle Azure Resource Manager.  

> [!IMPORTANT]
> Spécifiez le nom et la clé de votre compte Stockage Azure pour les paramètres **storageAccountName** et **storageAccountKey** dans ce fichier de paramètres. 
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
> Vous pouvez utiliser des fichiers JSON de paramètres distincts pour les environnements de développement, de test et de production avec le même modèle JSON Data Factory. En utilisant un script PowerShell, vous pouvez automatiser le déploiement des entités Data Factory dans ces environnements. 
> 
> 

## <a name="create-data-factory"></a>Créer une fabrique de données
1. Démarrez **Azure PowerShell** et exécutez la commande suivante : 
   * Exécutez la commande suivante, puis saisissez le nom d’utilisateur et le mot de passe que vous avez utilisés pour la connexion au portail Azure.
    ```PowerShell
    Login-AzureRmAccount
    ```  
   * Exécutez la commande suivante pour afficher tous les abonnements de ce compte.
    ```PowerShell
    Get-AzureRmSubscription
    ``` 
   * Exécutez la commande suivante pour sélectionner l’abonnement que vous souhaitez utiliser. Cet abonnement doit être identique à celui utilisé dans le portail Azure.
    ```
    Get-AzureRmSubscription -SubscriptionName <SUBSCRIPTION NAME> | Set-AzureRmContext
    ```   
2. Exécutez la commande suivante pour déployer des entités Data Factory à l’aide du modèle Resource Manager que vous avez créé à l’étape 1. 

    ```PowerShell
    New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile C:\ADFGetStarted\ADFTutorialARM.json -TemplateParameterFile C:\ADFGetStarted\ADFTutorialARM-Parameters.json
    ```

## <a name="monitor-pipeline"></a>Surveillance d’un pipeline
1. Après la connexion au [portail Azure](https://portal.azure.com/), cliquez sur **Parcourir** et sélectionnez **Fabriques de données**.
     ![Parcourir-&gt;Fabriques de données](./media/data-factory-build-your-first-pipeline-using-arm/BrowseDataFactories.png)
2. Dans le panneau **Fabriques de données**, cliquez sur la fabrique de données (**TutorialFactoryARM**) que vous avez créée.    
3. Dans le panneau **Fabrique de données** de votre fabrique de données, cliquez sur **Diagramme**.

     ![Vignette du diagramme](./media/data-factory-build-your-first-pipeline-using-arm/DiagramTile.png)
4. Dans la **Vue de diagramme**, une vue d’ensemble des pipelines et des jeux de données utilisés dans ce didacticiel s’affiche.
   
   ![Vue de diagramme](./media/data-factory-build-your-first-pipeline-using-arm/DiagramView.png) 
5. Dans la vue de diagramme, double-cliquez sur le jeu de données **AzureBlobOutput**. La tranche est en cours de traitement.
   
    ![Jeu de données](./media/data-factory-build-your-first-pipeline-using-arm/AzureBlobOutput.png)
6. Quand le traitement est terminé, l’état de la tranche est **Prêt** . La création d’un cluster HDInsight à la demande prend généralement un certain temps (environ 20 minutes). Le pipeline devrait donc traiter la tranche en **30 minutes environ** .
   
    ![Jeu de données](./media/data-factory-build-your-first-pipeline-using-arm/SliceReady.png)    
7. Quand l’état du segment est **Prêt**, vérifiez la présence des données de sortie dans le dossier **partitioneddata** du conteneur **adfgetstarted** de votre stockage d’objets blob.  

Consultez [Surveiller les jeux de données et le pipeline](data-factory-monitor-manage-pipelines.md) pour obtenir des instructions sur l’utilisation des panneaux du portail Azure afin de surveiller le pipeline et les jeux de données que vous avez créés dans ce didacticiel.

Vous pouvez également utiliser l’application Surveillance et gestion pour surveiller vos pipelines de données. Pour en savoir plus sur l’utilisation de l’application, consultez l’article [Surveiller et gérer les pipelines Azure Data Factory à l’aide de la nouvelle application de surveillance et gestion](data-factory-monitor-manage-app.md) . 

> [!IMPORTANT]
> Le fichier d’entrée sera supprimé lorsque la tranche est traitée avec succès. Par conséquent, si vous souhaitez réexécuter la tranche ou refaire le didacticiel, chargez le fichier d’entrée (input.log) dans le dossier inputdata du conteneur adfgetstarted.
> 
> 

## <a name="data-factory-entities-in-the-template"></a>Entités Data Factory dans le modèle
### <a name="define-data-factory"></a>Définir une fabrique de données
Vous définissez une fabrique de données dans le modèle Resource Manager, comme indiqué dans l’exemple suivant :  

```json
"resources": [
{
    "name": "[variables('dataFactoryName')]",
    "apiVersion": "2015-10-01",
    "type": "Microsoft.DataFactory/datafactories",
    "location": "West US"
}
```
La propriété dataFactoryName est défini en tant que : 

```json
"dataFactoryName": "[concat('HiveTransformDF', uniqueString(resourceGroup().id))]",
```
Il s’agit d’une chaîne unique basée sur l’ID du groupe de ressources.  

### <a name="defining-data-factory-entities"></a>Définition des entités Data Factory
Les entités Data Factory suivantes sont définies dans le modèle JSON : 

* [Service lié Azure Storage](#azure-storage-linked-service)
* [Service lié à la demande HDInsight](#hdinsight-on-demand-linked-service)
* [Jeu de données d'entrée d'objet Blob Azure](#azure-blob-input-dataset)
* [Jeu de données de sortie d’objet Blob Azure](#azure-blob-output-dataset)
* [Pipeline de données avec une activité de copie](#data-pipeline)

#### <a name="azure-storage-linked-service"></a>Service lié Azure Storage
Vous spécifiez le nom et la clé de votre compte Stockage Azure dans cette section. Consultez [Service lié Stockage Azure](data-factory-azure-blob-connector.md#azure-storage-linked-service) pour en savoir plus sur les propriétés JSON utilisées pour définir un service lié Stockage Azure. 

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
La propriété **connectionString** utilise les paramètres storageAccountName et storageAccountKey. Les valeurs de ces paramètres sont transmises à l’aide d’un fichier de configuration. La définition utilise également les variables azureStroageLinkedService et dataFactoryName, définies dans le modèle. 

#### <a name="hdinsight-on-demand-linked-service"></a>Service lié à la demande HDInsight
Consultez l’article [Services liés de calcul](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) pour en savoir plus sur les propriétés JSON utilisées pour définir un service lié à la demande HDInsight.  

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
Notez les points suivants : 

* La fabrique de données crée pour vous un cluster HDInsight **Linux** avec le code JSON ci-dessus. Pour plus d’informations, voir [Service lié à la demande Azure HDInsight](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) . 
* Vous pouvez utiliser votre **propre cluster HDInsight** au lieu d’utiliser un cluster HDInsight à la demande. Pour plus d’informations, voir [Service lié Azure HDInsight](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) .
* Le cluster HDInsight crée un **conteneur par défaut** dans le stockage d’objets blob que vous avez spécifié dans le JSON (**linkedServiceName**). HDInsight ne supprime pas ce conteneur lorsque le cluster est supprimé. Ce comportement est normal. Avec le service lié HDInsight à la demande, un cluster HDInsight est créé à chaque fois qu’une tranche doit être traitée, à moins qu’il n’existe un cluster activé (**timeToLive**), et est supprimé une fois le traitement activé.
  
    Comme un nombre croissant de tranches sont traitées, vous voyez un grand nombre de conteneurs dans votre stockage d’objets blob Azure. Si vous n’en avez pas besoin pour dépanner les travaux, il se peut que vous deviez les supprimer pour réduire les frais de stockage. Le nom de ces conteneurs suit un modèle : « **nomdevotrefabriquededonnéesadf**-**nomduservicelié**-horodatage ». Utilisez des outils tels que [Microsoft Storage Explorer](http://storageexplorer.com/) pour supprimer des conteneurs dans votre stockage d’objets blob Azure.

Pour plus d’informations, voir [Service lié à la demande Azure HDInsight](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) .

#### <a name="azure-blob-input-dataset"></a>Jeu de données d'entrée d'objet Blob Azure
Vous spécifiez les noms du conteneur d’objets blob, du dossier et du fichier contenant les données d’entrée. Consultez [Propriétés du jeu de données d’objet blob Azure](data-factory-azure-blob-connector.md#dataset-properties) pour en savoir plus sur les propriétés JSON permettant de définir un jeu de données d’objets blob Azure. 

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
Cette définition utilise les paramètres suivants, définis dans le modèle de paramètre : blobContainer, inputBlobFolder et inputBlobName. 

#### <a name="azure-blob-output-dataset"></a>Jeu de données de sortie d’objet Blob Azure
Vous spécifiez les noms du conteneur d’objets blob et du dossier contenant les données de sortie. Consultez [Propriétés du jeu de données d’objet blob Azure](data-factory-azure-blob-connector.md#dataset-properties) pour en savoir plus sur les propriétés JSON permettant de définir un jeu de données d’objets blob Azure.  

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

Cette définition utilise les paramètres suivants, définis dans le modèle de paramètre : blobContainer and outputBlobFolder. 

#### <a name="data-pipeline"></a>Pipeline de données
Vous définissez un pipeline qui transforme les données en exécutant le script Hive sur un cluster Azure HDInsight à la demande. Consultez [Pipeline JSON](data-factory-create-pipelines.md#pipeline-json) pour obtenir des descriptions des éléments JSON permettant de définir un pipeline dans cet exemple. 

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

## <a name="reuse-the-template"></a>Réutiliser le modèle
Dans ce didacticiel, vous avez créé un modèle pour définir des entités Data Factory et un modèle pour transmettre les valeurs des paramètres. Pour utiliser le même modèle afin de déployer des entités Data Factory dans des environnements différents, vous créez un fichier de paramètres pour chaque environnement et l’utiliser lors du déploiement de cet environnement.     

Exemple :  

```PowerShell
New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFTutorialARM.json -TemplateParameterFile ADFTutorialARM-Parameters-Dev.json

New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFTutorialARM.json -TemplateParameterFile ADFTutorialARM-Parameters-Test.json

New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFTutorialARM.json -TemplateParameterFile ADFTutorialARM-Parameters-Production.json
```
Notez que la première commande utilise le fichier de paramètres pour l’environnement de développement, la deuxième pour l’environnement de test et la troisième pour l’environnement de production.  

Vous pouvez également réutiliser le modèle pour effectuer des tâches répétitives. Par exemple, vous devez créer plusieurs fabriques de données avec un ou plusieurs pipelines qui implémentent la même logique, mais chaque fabrique de données utilise des comptes Stockage Azure et Azure SQL Database différents. Dans ce scénario, vous utilisez le même modèle dans le même environnement (développement, test ou production) avec différents fichiers de paramètres pour créer des fabriques de données. 

## <a name="resource-manager-template-for-creating-a-gateway"></a>Modèle Resource Manager pour la création d’une passerelle
Voici un exemple de modèle Resource Manager pour la création d’une passerelle logique à l’arrière. Installez une passerelle sur votre ordinateur local ou sur une machine virtuelle IaaS Azure et l’enregistrer auprès du service Data Factory à l’aide d’une clé. Pour plus d’informations, consultez [Déplacer des données entre un emplacement local et le cloud](data-factory-move-data-between-onprem-and-cloud.md) .

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
Ce modèle crée une fabrique de données nommée GatewayUsingArmDF avec une passerelle nommée GatewayUsingARM. 

## <a name="see-also"></a>Voir aussi
| Rubrique | Description |
|:--- |:--- |
| [Pipelines](data-factory-create-pipelines.md) |Cet article vous aide à comprendre les pipelines et les activités dans Azure Data Factory, et à les utiliser dans l’optique de créer des workflows pilotés par les données de bout en bout pour votre scénario ou votre entreprise. |
| [Groupes de données](data-factory-create-datasets.md) |Cet article vous aide à comprendre les jeux de données dans Azure Data Factory. |
| [Planification et exécution](data-factory-scheduling-and-execution.md) |Cet article explique les aspects de la planification et de l’exécution du modèle d’application Azure Data Factory. |
| [Surveiller et gérer les pipelines Azure Data Factory à l’aide de la nouvelle application de surveillance et gestion.](data-factory-monitor-manage-app.md) |Cet article décrit comment surveiller, gérer et déboguer les pipelines à l’aide de l’application de surveillance et gestion. |

