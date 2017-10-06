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

Dans cet article, vous utilisez un toocreate de modèle Azure Resource Manager votre première Azure data factory. didacticiel de hello toodo à l’aide d’autres outils/kits de développement logiciel, sélectionnez une des options de hello à partir de la liste déroulante de hello.

pipeline Hello dans ce didacticiel a une activité : **activité HDInsight Hive**. Cette activité s’exécute un script hive sur un cluster Azure HDInsight et les transformations d’entrée de données de sortie tooproduce. pipeline de Hello est planifiée toorun une fois qu’un mois entre hello spécifié d’heures de début et de fin. 

> [!NOTE]
> le pipeline de données Hello dans ce didacticiel transforme les données de sortie de données d’entrée tooproduce. Pour obtenir un didacticiel sur la façon de toocopy les données à l’aide d’Azure Data Factory, consultez [didacticiel : copier des données à partir du stockage d’objets Blob tooSQL de base de données](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).
> 
> pipeline de Hello dans ce didacticiel ne comprend qu’une seule activité de type : HDInsightHive. Un pipeline peut contenir plusieurs activités. De plus, vous pouvez concaténer les deux activités (exécutée une activité après l’autre) en définissant le dataset de sortie hello d’une activité hello d’entrée dataset Hello autre activité. Pour plus d’informations, consultez [Planification et exécution dans Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline). 

## <a name="prerequisites"></a>Composants requis
* Lisez [vue d’ensemble du didacticiel](data-factory-build-your-first-pipeline.md) article et hello complète **condition préalable** étapes.
* Suivez les instructions de [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview) article tooinstall version la plus récente d’Azure PowerShell sur votre ordinateur.
* Consultez [de création de modèles de gestionnaire de ressources Azure](../azure-resource-manager/resource-group-authoring-templates.md) toolearn sur les modèles Azure Resource Manager. 

## <a name="in-this-tutorial"></a>Dans ce didacticiel
| Entité | Description |
| --- | --- |
| Service lié Azure Storage |Lie votre fabrique de données toohello compte Azure Storage. blocages de compte de stockage Azure Hello hello des données d’entrée et de sortie pour le pipeline hello dans cet exemple. |
| Service lié à la demande HDInsight |Lie une fabrique de données à la demande HDInsight cluster toohello. cluster de Hello est automatiquement créé pour vous tooprocess des données et est supprimé après que traitement de hello est effectué. |
| Jeu de données d'entrée d'objet Blob Azure |Fait référence toohello lié Azure Storage service. Hello service lié fait référence compte de stockage Azure tooan et dataset d’objets Blob Azure hello spécifie hello conteneur, dossier et nom de fichier dans le stockage hello qui contient les données d’entrée hello. |
| Jeu de données de sortie d’objet Blob Azure |Fait référence toohello lié Azure Storage service. Hello service lié fait référence compte de stockage Azure tooan et dataset d’objets Blob Azure hello spécifie hello conteneur, dossier et nom de fichier dans le stockage hello qui contient les données de sortie hello. |
| Pipeline de données |pipeline de Hello a une activité de type HDInsightHive, ce qui consomme hello de jeu de données d’entrée et produit le jeu de données de sortie hello. |

Une fabrique de données peut avoir un ou plusieurs pipelines. Un pipeline peut contenir une ou plusieurs activités. Il existe deux types d’activités : les [activités de déplacement des données](data-factory-data-movement-activities.md) et les [activités de transformation des données](data-factory-data-transformation-activities.md). Dans ce didacticiel, vous créez un pipeline avec une activité (activité Hive).

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
Créez un fichier JSON nommé **ADFTutorialARM.json** dans **C:\ADFGetStarted** dossier avec hello suivant le contenu :

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
> Vous trouverez un autre exemple de modèle Resource Manager pour créer une fabrique de données Azure dans le [didacticiel : Créer un pipeline avec activité de copie à l’aide d’un modèle Azure Resource Manager](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md).  
> 
> 

## <a name="parameters-json"></a>Paramètres JSON
Créez un fichier JSON nommé **ADFTutorialARM-Parameters.json** qui contient les paramètres de modèle de gestionnaire de ressources Azure hello.  

> [!IMPORTANT]
> Spécifiez le nom de hello et la clé de votre compte de stockage Azure pour hello **storageAccountName** et **storageAccountKey** paramètres dans ce fichier de paramètres. 
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
   * Tooselect hello abonnement toowork avec la commande suivante d’exécution hello. Cet abonnement doit être hello identique à celui Bonjour portail Azure hello.
    ```
    Get-AzureRmSubscription -SubscriptionName <SUBSCRIPTION NAME> | Set-AzureRmContext
    ```   
2. Hello exécution suivant des entités de fabrique de données toodeploy de commande à l’aide du modèle de gestionnaire de ressources hello que vous avez créé à l’étape 1. 

    ```PowerShell
    New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile C:\ADFGetStarted\ADFTutorialARM.json -TemplateParameterFile C:\ADFGetStarted\ADFTutorialARM-Parameters.json
    ```

## <a name="monitor-pipeline"></a>Surveillance d’un pipeline
1. Une fois connecté toohello [portail Azure](https://portal.azure.com/), cliquez sur **Parcourir** et sélectionnez **fabriques de données**.
     ![Parcourir-&gt;Fabriques de données](./media/data-factory-build-your-first-pipeline-using-arm/BrowseDataFactories.png)
2. Bonjour **fabriques de données** panneau, cliquez sur la fabrique de données hello (**TutorialFactoryARM**) que vous avez créé.    
3. Bonjour **Data Factory** Panneau de votre fabrique de données, cliquez sur **diagramme**.

     ![Vignette du diagramme](./media/data-factory-build-your-first-pipeline-using-arm/DiagramTile.png)
4. Bonjour **vue de diagramme**, vous voyez une vue d’ensemble des pipelines de hello et les datasets utilisés dans ce didacticiel.
   
   ![Vue du diagramme](./media/data-factory-build-your-first-pipeline-using-arm/DiagramView.png) 
5. Dans la vue de diagramme de hello, double-cliquez sur hello dataset **AzureBlobOutput**. Vous voyez ce secteur hello qui est en cours de traitement.
   
    ![Jeu de données](./media/data-factory-build-your-first-pipeline-using-arm/AzureBlobOutput.png)
6. Lorsque le traitement est terminé, vous consultez la section hello dans **prêt** état. La création d’un cluster HDInsight à la demande prend généralement un certain temps (environ 20 minutes). Par conséquent, s’attendent hello pipeline tootake **environ 30 minutes** tooprocess hello tranche.
   
    ![Jeu de données](./media/data-factory-build-your-first-pipeline-using-arm/SliceReady.png)    
7. Lorsque la tranche de hello est à **prêt** d’état, vérifiez hello **partitioneddata** dossier Bonjour **adfgetstarted** conteneur dans votre stockage d’objets blob pour hello les données de sortie.  

Consultez [analyser des jeux de données et le pipeline](data-factory-monitor-manage-pipelines.md) pour obtenir des instructions sur la façon dont le pipeline hello toomonitor toouse hello panneaux portail Azure et les jeux de données vous avez créé dans ce didacticiel.

Vous pouvez également utiliser toomonitor moniteur et l’application de gérer vos pipelines de données. Consultez [analyse et de gérer les pipelines Azure Data Factory à l’aide d’application de surveillance](data-factory-monitor-manage-app.md) pour plus d’informations sur l’utilisation d’application hello. 

> [!IMPORTANT]
> fichier d’entrée de Hello est supprimé lors de la tranche de hello est traitée avec succès. Par conséquent, si vous souhaitez tranche de hello toorerun ou que vous hello didacticiel à nouveau, téléchargez hello d’entrée (input.log) toohello inputdata dossier des fichiers du conteneur d’adfgetstarted hello.
> 
> 

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
"dataFactoryName": "[concat('HiveTransformDF', uniqueString(resourceGroup().id))]",
```
Il s’agit d’une chaîne unique en fonction de l’ID de groupe de ressources hello.  

### <a name="defining-data-factory-entities"></a>Définition des entités Data Factory
Hello des entités de fabrique de données suivantes sont définies dans le modèle JSON hello : 

* [Service lié Azure Storage](#azure-storage-linked-service)
* [Service lié à la demande HDInsight](#hdinsight-on-demand-linked-service)
* [Jeu de données d'entrée d'objet Blob Azure](#azure-blob-input-dataset)
* [Jeu de données de sortie d’objet Blob Azure](#azure-blob-output-dataset)
* [Pipeline de données avec une activité de copie](#data-pipeline)

#### <a name="azure-storage-linked-service"></a>Service lié Azure Storage
Vous spécifiez le nom de hello et la clé de votre compte de stockage Azure dans cette section. Consultez [service lié Azure Storage](data-factory-azure-blob-connector.md#azure-storage-linked-service) pour plus d’informations sur JSON propriétés utilisées toodefine un stockage Azure le service lié. 

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
Hello **connectionString** utilise hello paramètres storageAccountName et storageAccountKey. valeurs Hello pour ces paramètres passés à l’aide d’un fichier de configuration. définition de Hello utilise également des variables : azureStroageLinkedService et dataFactoryName définies dans le modèle de hello. 

#### <a name="hdinsight-on-demand-linked-service"></a>Service lié à la demande HDInsight
Consultez [services liés de calcul](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) article pour plus d’informations sur JSON propriétés utilisées toodefine un service lié à la demande de HDInsight.  

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
Hello Notez les points suivants : 

* Hello Data Factory crée un **basés sur Linux** cluster HDInsight pour vous par hello au-dessus de JSON. Pour plus d’informations, voir [Service lié à la demande Azure HDInsight](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) . 
* Vous pouvez utiliser votre **propre cluster HDInsight** au lieu d’utiliser un cluster HDInsight à la demande. Pour plus d’informations, voir [Service lié Azure HDInsight](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) .
* Hello HDInsight cluster crée un **conteneur par défaut** dans le stockage blob hello spécifié dans hello JSON (**linkedServiceName**). HDInsight ne supprime pas ce conteneur lorsque le cluster de hello est supprimé. Ce comportement est normal. Service lié HDInsight à la demande un cluster HDInsight est créé chaque fois qu’une tranche doit toobe traité sauf s’il existe un cluster dynamique existant (**timeToLive**) et est supprimé quand le traitement de hello est effectué.
  
    Comme un nombre croissant de tranches sont traitées, vous voyez un grand nombre de conteneurs dans votre stockage d’objets blob Azure. Si vous ne devez pas les pour la résolution des problèmes de travaux de hello, vous souhaiterez peut-être toodelete les coûts de stockage tooreduce hello. les noms de ces conteneurs Hello suivent un modèle : « adf**yourdatafactoryname**-**linkedservicename**- datetimestamp ». Utiliser des outils tels que [Explorateur de stockage Microsoft](http://storageexplorer.com/) stockage d’objets blob des conteneurs de toodelete dans votre Azure.

Pour plus d’informations, voir [Service lié à la demande Azure HDInsight](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) .

#### <a name="azure-blob-input-dataset"></a>Jeu de données d'entrée d'objet Blob Azure
Vous spécifiez les noms de conteneur d’objets blob, de dossier et de fichier qui contient les données d’entrée hello hello. Consultez [propriétés de jeu de données d’objets Blob Azure](data-factory-azure-blob-connector.md#dataset-properties) pour plus d’informations sur les propriétés utilisées de JSON toodefine un jeu de données d’objets Blob Azure. 

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
Cette définition utilise hello suivant les paramètres définis dans le modèle de paramètre : blobContainer, inputBlobFolder et inputBlobName. 

#### <a name="azure-blob-output-dataset"></a>Jeu de données de sortie d’objet Blob Azure
Vous spécifiez les noms de conteneur d’objets blob et le dossier qui contient les données de sortie hello hello. Consultez [propriétés de jeu de données d’objets Blob Azure](data-factory-azure-blob-connector.md#dataset-properties) pour plus d’informations sur les propriétés utilisées de JSON toodefine un jeu de données d’objets Blob Azure.  

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

Cette définition utilise hello suivant les paramètres définis dans le modèle de paramètre hello : blobContainer et outputBlobFolder. 

#### <a name="data-pipeline"></a>Pipeline de données
Vous définissez un pipeline qui transforme les données en exécutant le script Hive sur un cluster Azure HDInsight à la demande. Consultez [JSON de Pipeline](data-factory-create-pipelines.md#pipeline-json) pour les descriptions des éléments utilisés de JSON toodefine un pipeline dans cet exemple. 

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

## <a name="reuse-hello-template"></a>Réutiliser le modèle de hello
Dans le didacticiel de hello, vous avez créé un modèle permettant de définir des entités de fabrique de données et un modèle pour passer des valeurs pour les paramètres. toouse hello même modèle toodeploy Data Factory entités toodifferent des environnements, vous créez un fichier de paramètres pour chaque environnement et l’utilisez lors de la toothat environnement de déploiement.     

Exemple :  

```PowerShell
New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFTutorialARM.json -TemplateParameterFile ADFTutorialARM-Parameters-Dev.json

New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFTutorialARM.json -TemplateParameterFile ADFTutorialARM-Parameters-Test.json

New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFTutorialARM.json -TemplateParameterFile ADFTutorialARM-Parameters-Production.json
```
Notez que hello première commande utilise le fichier de paramètres pour l’environnement de développement hello, deuxième hello un environnement de test et hello un tiers pour l’environnement de production hello.  

Vous pouvez également réutiliser hello modèle tooperform tâches récurrentes. Par exemple, vous devez toocreate plusieurs fabriques de données avec l’un ou plusieurs pipelines qui implémentent hello même logique, mais chaque données fabrique utilise différents le stockage Azure et les comptes de la base de données SQL Azure. Dans ce scénario, vous utilisez hello même modèle Bonjour même environnement (développement, test ou production) avec des paramètres différents fichiers toocreate les fabriques de données. 

## <a name="resource-manager-template-for-creating-a-gateway"></a>Modèle Resource Manager pour la création d’une passerelle
Voici un exemple de modèle de gestionnaire de ressources pour la création d’une passerelle logique Bonjour précédent. Installer une passerelle sur votre ordinateur local ou d’une machine virtuelle IaaS de Azure et passerelle de hello auprès de service de fabrique de données à l’aide d’une clé. Pour plus d’informations, consultez [Déplacer des données entre un emplacement local et le cloud](data-factory-move-data-between-onprem-and-cloud.md) .

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
| [Pipelines](data-factory-create-pipelines.md) |Cet article vous aidera à comprendre les pipelines et les activités dans Azure Data Factory et comment toouse les tooconstruct bout en bout piloté par les données des flux de travail pour votre entreprise ou votre scénario. |
| [Groupes de données](data-factory-create-datasets.md) |Cet article vous aide à comprendre les jeux de données dans Azure Data Factory. |
| [Planification et exécution](data-factory-scheduling-and-execution.md) |Cet article explique les aspects de planification et l’exécution de hello du modèle d’application Azure Data Factory. |
| [Surveiller et gérer les pipelines Azure Data Factory à l’aide de la nouvelle application de surveillance et gestion.](data-factory-monitor-manage-app.md) |Cet article décrit comment toomonitor, gérer et déboguer des pipelines à l’aide de hello analyse & application de gestion. |

