---
title: "les modèles de Machine Learning aaaUpdate à l’aide d’Azure Data Factory | Documents Microsoft"
description: "Décrit comment toocreate créer des pipelines PRÉDICTIFS à l’aide d’Azure Data Factory et Azure Machine Learning"
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: shlo
ms.openlocfilehash: 6e5e4d2cfd245c7a9ed3bb9cdacca1f7f82b9620
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="updating-azure-machine-learning-models-using-update-resource-activity"></a>Mettre à jour les modèles Azure Machine Learning à l’aide de l’activité des ressources de mise à jour

> [!div class="op_single_selector" title1="Transformation Activities"]
> * [Activité Hive](data-factory-hive-activity.md) 
> * [Activité pig](data-factory-pig-activity.md)
> * [Activité MapReduce](data-factory-map-reduce.md)
> * [Activité de diffusion en continu Hadoop](data-factory-hadoop-streaming-activity.md)
> * [Activité Spark](data-factory-spark.md)
> * [Activité d’exécution par lot Machine Learning](data-factory-azure-ml-batch-execution-activity.md)
> * [Activité des ressources de mise à jour de Machine Learning](data-factory-azure-ml-update-resource-activity.md)
> * [Activité de procédure stockée](data-factory-stored-proc-activity.md)
> * [Activité U-SQL Data Lake Analytics](data-factory-usql-activity.md)
> * [Activité personnalisée .NET](data-factory-use-custom-activities.md)

Cet article complète hello principal Azure Data Factory - article de l’intégration d’Azure Machine Learning : [créer des pipelines PRÉDICTIFS à l’aide d’Azure Machine Learning et Azure Data Factory](data-factory-azure-ml-batch-execution-activity.md). Si vous n’avez pas déjà fait, passez en revue l’article principal de hello avant la lecture de cet article. 

## <a name="overview"></a>Vue d'ensemble
Au fil du temps, utiliser des modèles prédictifs hello dans des expériences de score Azure ML hello doivent toobe reformé à l’aide de nouveaux jeux de données d’entrée. Une fois que vous avez terminé avec le réapprentissage, vous souhaitez hello tooupdate calcul du score du service web avec hello reformés modèle ML. Hello étapes classiques tooenable réapprentissage et mise à jour des modèles Azure ML via les services web sont :

1. Créez une expérience dans [Azure ML Studio](https://studio.azureml.net).
2. Lorsque vous êtes satisfait de modèle de hello, utiliser des services web à la fois hello Azure ML Studio toopublish **expérience de formation** et le score /**expérience prédictive**.

Hello tableau suivant décrit les services web hello utilisés dans cet exemple.  Pour plus d’informations, consultez [Reformation des modèles Machine Learning par programme](../machine-learning/machine-learning-retrain-models-programmatically.md) .

- **Service Web de formation** - Reçoit les données d’apprentissage et produit les modèles formés. sortie de Hello de recyclage de hello est un fichier .ilearner dans un stockage d’objets Blob Azure. Hello **par défaut du point de terminaison** est automatiquement créé pour vous lors de la publication de la formation de hello expérimenter comme un service web. Vous pouvez créer plusieurs points de terminaison, mais hello exemple utilise uniquement les point de terminaison de valeur par défaut hello.
- **Service Web de notation** - Reçoit des exemples de données sans étiquette et effectue des prédictions. sortie Hello de prédiction peut avoir différentes formes, par exemple un fichier .csv ou des lignes dans une base de données SQL Azure, selon la configuration de hello d’expérimentation de hello. point de terminaison par défaut Hello est automatiquement créé lorsque vous publiez l’expérience de prédictive hello comme un service web. 

Hello image suivante illustre les relations de hello entre les jeux d’apprentissage et le score des points de terminaison dans Azure ML.

![SERVICES WEB](./media/data-factory-azure-ml-batch-execution-activity/web-services.png)

Vous pouvez appeler hello **formation service web** à l’aide de hello **activité de l’exécution du lot Azure ML**. L’appel d’un service web de formation est similaire à l’appel d’un service web Azure ML (service web de notation) pour les données de notation. Bonjour précédent garde sections Comment tooinvoke un service web de Azure ML à partir d’une fabrique de données Azure de pipeline en détail. 

Vous pouvez appeler hello **calcul du score du service web** à l’aide de hello **activité de ressource mise à jour Azure ML** service web qui vient d’être formé hello tooupdate hello. Hello exemple suivant fournit les définitions de service lié : 

## <a name="scoring-web-service-is-a-classic-web-service"></a>Service web de notation est un service web classique
Si hello calcul du score du service web est un **service web classique**, créer hello deuxième **point de terminaison par défaut et mettre à jour** à l’aide de hello [portail Azure](https://manage.windowsazure.com). Pour connaître les étapes, consultez l’article [Créer des points de terminaison](../machine-learning/machine-learning-create-endpoint.md). Après avoir créé le point de terminaison actualisable hello non définis par défaut, procédez comme hello comme suit :

* Cliquez sur **l’exécution par lots** tooget hello URI valeur hello **mlEndpoint** propriété JSON.
* Cliquez sur **mise à jour de ressource** lier la valeur de l’URI tooget hello pour hello **updateResourceEndpoint** propriété JSON. clé d’API Hello est sur la page de point de terminaison hello lui-même (dans le coin inférieur droit de hello).

![point de terminaison pouvant être mis à jour](./media/data-factory-azure-ml-batch-execution-activity/updatable-endpoint.png)

Hello, l’exemple suivant fournit un exemple de définition JSON pour hello service AzureML lié. Hello service lié utilise hello apiKey pour l’authentification.  

```json
{
    "name": "updatableScoringEndpoint2",
    "properties": {
        "type": "AzureML",
        "typeProperties": {
            "mlEndpoint": "https://ussouthcentral.services.azureml.net/workspaces/xxx/services/--scoring experiment--/jobs",
            "apiKey": "endpoint2Key",
            "updateResourceEndpoint": "https://management.azureml.net/workspaces/xxx/webservices/--scoring experiment--/endpoints/endpoint2"
        }
    }
}
```

## <a name="scoring-web-service-is-azure-resource-manager-web-service"></a>Le service web de notification est un service web Azure Resource Manager 
Si le service web de hello est hello nouveau type de service web qui expose un point de terminaison Azure Resource Manager, il est inutile tooadd hello deuxième **non définis par défaut** point de terminaison. Hello **updateResourceEndpoint** Bonjour service lié est hello format : 

```
https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resource-group-name}/providers/Microsoft.MachineLearning/webServices/{web-service-name}?api-version=2016-05-01-preview. 
```

Vous pouvez obtenir des valeurs pour les espaces réservés dans les URL hello lors de l’interrogation du service web hello hello [portail de Services Web Azure Machine Learning](https://services.azureml.net/). Hello nouveau type de point de terminaison de mise à jour de ressource requiert un jeton AAD (Azure Active Directory). Spécifiez **servicePrincipalId** et **servicePrincipalKey**dans le service lié AzureML. Consultez [comment toocreate principal de service et assigner des autorisations toomanage ressource Azure](../azure-resource-manager/resource-group-create-service-principal-portal.md). Voici un exemple de définition de service lié AzureML : 

```json
{
    "name": "AzureMLLinkedService",
    "properties": {
        "type": "AzureML",
        "description": "hello linked service for AML web service.",
        "typeProperties": {
            "mlEndpoint": "https://ussouthcentral.services.azureml.net/workspaces/0000000000000000000000000000000000000/services/0000000000000000000000000000000000000/jobs?api-version=2.0",
            "apiKey": "xxxxxxxxxxxx",
            "updateResourceEndpoint": "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myRG/providers/Microsoft.MachineLearning/webServices/myWebService?api-version=2016-05-01-preview",
            "servicePrincipalId": "000000000-0000-0000-0000-0000000000000",
            "servicePrincipalKey": "xxxxx",
            "tenant": "mycompany.com"
        }
    }
}
```

Hello scénario suivant fournit plus de détails. Il présente un exemple de reformation et de mise à jour de modèles Azure ML à partir d’un pipeline Azure Data Factory.

## <a name="scenario-retraining-and-updating-an-azure-ml-model"></a>Scénario : reformation et mise à jour d’un modèle Azure ML
Cette section fournit un exemple de pipeline qui utilise hello **l’activité d’exécution de lot Azure ML** tooretrain un modèle. pipeline de Hello utilise également hello **de ressources de mise à jour Azure ML activité** modèle hello tooupdate hello calcul du score du service web. Hello présente également des extraits de code JSON de tous les hello services liés, des datasets et pipeline dans l’exemple de hello.

Voici une vue de diagramme hello du pipeline d’exemple hello. Comme vous pouvez le voir, hello activité de l’exécution du lot Azure ML accepte l’entrée d’apprentissage hello et génère une sortie de formation (fichier iLearner). Hello activité de ressources Azure ML mise à jour prend cette sortie de formation et mises à jour hello modèle Bonjour calcul du score du point de terminaison de service web. Hello activité des ressources de mise à jour ne produit pas de sortie. Hello placeholderBlob est simplement un dataset de sortie factice est requis par le pipeline hello toorun hello Azure Data Factory service.

![schéma du pipeline](./media/data-factory-azure-ml-batch-execution-activity/update-activity-pipeline-diagram.png)

### <a name="azure-blob-storage-linked-service"></a>Service lié Azure Blob Storage :
Bonjour Azure Storage conserve hello données suivantes :

* Données de formation. données d’entrée de salutation pour le service web de hello Azure ML d’apprentissage.  
* Fichier iLearner. Hello la sortie à partir du service web de hello Azure ML d’apprentissage. Ce fichier est également hello, toohello d’entrée de ressources de mise à jour l’activité.  

Voici hello exemple JSON de définition de service de hello lié :

```JSON
{
    "name": "StorageLinkedService",
      "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=name;AccountKey=key"
        }
    }
}
```

### <a name="training-input-dataset"></a>Jeu de données d’entrée de formation
Hello dataset suivant représente hello les données de formation d’entrée pour le service web de hello Azure ML d’apprentissage. Hello activité d’exécution du lot Azure ML prend ce jeu de données comme entrée.

```JSON
{
    "name": "trainingData",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "labeledexamples",
            "fileName": "labeledexamples.arff",
            "format": {
                "type": "TextFormat"
            }
        },
        "availability": {
            "frequency": "Week",
            "interval": 1
        },
        "policy": {          
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

### <a name="training-output-dataset"></a>Jeu de données de sortie de formation :
Hello dataset suivant représente hello iLearner fichier de sortie à partir du service web de hello Azure ML d’apprentissage. Hello d’activité de l’exécution du lot Azure ML génère ce jeu de données. Ce jeu de données est également hello, toohello d’entrée de ressources de mise à jour Azure ML l’activité.

```JSON
{
    "name": "trainedModelBlob",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "trainingoutput",
            "fileName": "model.ilearner",
            "format": {
                "type": "TextFormat"
            }
        },
        "availability": {
            "frequency": "Week",
            "interval": 1
        }
    }
}
```

### <a name="linked-service-for-azure-ml-training-endpoint"></a>Service lié pour le point de terminaison de formation Azure ML
Hello suivant extrait de code JSON définit un service lié Azure Machine Learning qui pointe toohello point de terminaison par défaut du service web de formation hello.

```JSON
{    
    "name": "trainingEndpoint",
      "properties": {
        "type": "AzureML",
        "typeProperties": {
            "mlEndpoint": "https://ussouthcentral.services.azureml.net/workspaces/xxx/services/--training experiment--/jobs",
              "apiKey": "myKey"
        }
      }
}
```

Dans **Azure ML Studio**, hello tooget valeurs suivantes pour **mlEndpoint** et **apiKey**:

1. Cliquez sur **SERVICES WEB** sur le menu de gauche hello.
2. Cliquez sur hello **formation service web** dans la liste hello de services web.
3. Cliquez sur Copier ensuite trop**clé API** zone de texte. Collez la clé de hello dans le Presse-papiers de hello dans l’éditeur JSON de fabrique de données hello.
4. Bonjour **Azure ML studio**, cliquez sur **l’exécution par lots** lien.
5. Hello de copie **URI de requête** de hello **demande** section et collez-le dans l’éditeur JSON de fabrique de données hello.   

### <a name="linked-service-for-azure-ml-updatable-scoring-endpoint"></a>Service lié pour le point de terminaison de notation pouvant être mis à jour Azure ML :
Hello suivant extrait de code JSON définit un service lié Azure Machine Learning qui pointe de point de terminaison toohello non définis par défaut être mise à jour de hello calcul du score du service web.  

```JSON
{
    "name": "updatableScoringEndpoint2",
    "properties": {
        "type": "AzureML",
        "typeProperties": {
            "mlEndpoint": "https://ussouthcentral.services.azureml.net/workspaces/00000000eb0abe4d6bbb1d7886062747d7/services/00000000026734a5889e02fbb1f65cefd/jobs?api-version=2.0",
            "apiKey": "sooooooooooh3WvG1hBfKS2BNNcfwSO7hhY6dY98noLfOdqQydYDIXyf2KoIaN3JpALu/AKtflHWMOCuicm/Q==",
            "updateResourceEndpoint": "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/Default-MachineLearning-SouthCentralUS/providers/Microsoft.MachineLearning/webServices/myWebService?api-version=2016-05-01-preview",
            "servicePrincipalId": "fe200044-c008-4008-a005-94000000731",
            "servicePrincipalKey": "zWa0000000000Tp6FjtZOspK/WMA2tQ08c8U+gZRBlw=",
            "tenant": "mycompany.com"
        }
    }
}
```

### <a name="placeholder-output-dataset"></a>Jeu de données de sortie de l’espace réservé
Hello activité des ressources de mise à jour Azure ML ne génère pas de sortie. Toutefois, Azure Data Factory nécessite une planification de hello sortie dataset toodrive d’un pipeline. Par conséquent, nous utilisons dans cet exemple un jeu de données factice/paramètre fictif.  

```JSON
{
    "name": "placeholderBlob",
    "properties": {
        "availability": {
            "frequency": "Week",
            "interval": 1
        },
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "any",
            "format": {
                "type": "TextFormat"
            }
        }
    }
}
```

### <a name="pipeline"></a>Pipeline
pipeline de Hello a deux activités : **AzureMLBatchExecution** et **AzureMLUpdateResource**. Hello activité d’exécution du lot Azure ML prend les données d’apprentissage hello comme entrée et produit un fichier iLearner comme sortie. activité Hello appelle le service web de formation hello (expérience d’apprentissage exposé comme service web) avec une entrée hello données d’apprentissage et reçoit de fichier ilearner de hello de hello webservice. Hello placeholderBlob est simplement un dataset de sortie factice est requis par le pipeline hello toorun hello Azure Data Factory service.

![schéma du pipeline](./media/data-factory-azure-ml-batch-execution-activity/update-activity-pipeline-diagram.png)

```JSON
{
    "name": "pipeline",
    "properties": {
        "activities": [
            {
                "name": "retraining",
                "type": "AzureMLBatchExecution",
                "inputs": [
                    {
                        "name": "trainingData"
                    }
                ],
                "outputs": [
                    {
                        "name": "trainedModelBlob"
                    }
                ],
                "typeProperties": {
                    "webServiceInput": "trainingData",
                    "webServiceOutputs": {
                        "output1": "trainedModelBlob"
                    }              
                 },
                "linkedServiceName": "trainingEndpoint",
                "policy": {
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1,
                    "timeout": "02:00:00"
                }
            },
            {
                "type": "AzureMLUpdateResource",
                "typeProperties": {
                    "trainedModelName": "Training Exp for ADF ML [trained model]",
                    "trainedModelDatasetName" :  "trainedModelBlob"
                },
                "inputs": [
                    {
                        "name": "trainedModelBlob"
                    }
                ],
                "outputs": [
                    {
                        "name": "placeholderBlob"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "retry": 3
                },
                "name": "AzureML Update Resource",
                "linkedServiceName": "updatableScoringEndpoint2"
            }
        ],
        "start": "2016-02-13T00:00:00Z",
           "end": "2016-02-14T00:00:00Z"
    }
}
```
