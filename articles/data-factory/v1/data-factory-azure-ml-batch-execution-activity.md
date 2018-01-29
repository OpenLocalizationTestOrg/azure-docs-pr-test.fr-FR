---
title: "Création de pipelines de données prédictifs avec Azure Data Factory | Microsoft Docs"
description: "Décrit comment créer des pipelines prédictifs à l’aide d’Azure Data Factory et d’Azure Machine Learning."
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 4fad8445-4e96-4ce0-aa23-9b88e5ec1965
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/22/2018
ms.author: shlo
robots: noindex
ms.openlocfilehash: 05ae7cdc78e909c9aaa2b690d03eff8da09b6242
ms.sourcegitcommit: 9cc3d9b9c36e4c973dd9c9028361af1ec5d29910
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/23/2018
---
# <a name="create-predictive-pipelines-using-azure-machine-learning-and-azure-data-factory"></a>Création de pipelines prédictifs à l'aide d'Azure Data Factory et Azure Machine Learning

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

## <a name="introduction"></a>Introduction
> [!NOTE]
> Cet article s’applique à la version 1 de Data factory, qui est généralement disponible (GA). Si vous utilisez la version 2 du service Data Factory, qui est en préversion, consultez [transform data using machine learning in Data Factory version 2](../transform-data-using-machine-learning.md) (Transformer des données à l’aide de l’apprentissage machine dans Data Factory version 2).


### <a name="azure-machine-learning"></a>Azure Machine Learning
[AZURE MACHINE LEARNING](https://azure.microsoft.com/documentation/services/machine-learning/) vous permet de générer, tester et déployer des solutions d’analyse prédictive. D’un point de vue très général, cela s’effectue en trois étapes :

1. **Créez une expérience de formation**. Vous effectuez cette étape à l’aide d’Azure ML Studio. ML Studio est un environnement de développement visuel collaboratif qui vous permet de former et de tester un modèle d’analyse prédictive à l’aide de données d’apprentissage.
2. **Convertissez-la en une expérience prédictive**. Une fois que votre modèle a été formé avec des données existantes et que vous êtes prêt à l’utiliser pour la notation de nouvelles données, vous préparez et simplifiez votre expérience de notation.
3. **Déployez-la en tant que service web**. Vous pouvez publier votre expérience de notation comme un service web Azure. Vous pouvez envoyer des données à votre modèle via ce point de terminaison de service web et recevoir des prédictions de résultats pour le modèle.  

### <a name="azure-data-factory"></a>Azure Data Factory
Data Factory est un service d’intégration de données dans le cloud qui gère et automatise le **déplacement** et la **transformation** des données. Vous pouvez créer des solutions d’intégration de données à l’aide du service Azure Data Factory, qui peut ingérer des données provenant de différentes banques de données, transformer/traiter les données et publier les données résultantes dans les banques de données.

Le service Data Factory vous permet de créer des pipelines de données qui déplacent et transforment les données, puis d’exécuter ces pipelines selon une planification spécifique (une fois par heure, par jour, par semaine, etc.). Il fournit également des affichages élaborés pour visualiser le lignage et les dépendances entre vos pipelines de données, ainsi qu’une vue unifiée depuis laquelle vous pouvez surveiller l’ensemble de ces pipelines afin d’identifier les problèmes et de configurer des alertes d’analyse en toute simplicité.

Pour prendre en main le service Azure Data Factory rapidement, voir [Présentation d’Azure Data Factory](data-factory-introduction.md) et [Créer votre premier pipeline](data-factory-build-your-first-pipeline.md).

### <a name="data-factory-and-machine-learning-together"></a>Data Factory et Machine Learning
Azure Data Factory vous permet de créer facilement des pipelines qui utilisent un service web [Azure Machine Learning][azure-machine-learning] publié pour l’analyse prédictive. À l’aide de l’ **activité d’exécution par lots** dans un pipeline Azure Data Factory, vous pouvez appeler un service web Azure ML pour effectuer des prédictions sur les données par lots. Consultez la section [Appeler un service web Azure ML à l’aide de l’activité d’exécution par lots](#invoking-an-azure-ml-web-service-using-the-batch-execution-activity) pour plus d’informations.

Au fil du temps, les modèles prédictifs dans les expériences de notation Azure ML doivent être reformés à l’aide de nouveaux jeux de données d’entrée. Vous pouvez reformer un modèle Azure ML à partir d’un pipeline Data Factory en procédant comme suit :

1. Publiez l’expérience de formation (et non l’expérience prédictive) comme un service web. Vous pouvez effectuer cette tâche dans Azure ML Studio comme vous l’avez fait pour exposer l’expérience prédictive en tant que service web dans le scénario précédent.
2. Utilisez l’activité d’exécution par lots Azure ML pour appeler le service web pour l’expérience de formation. En fait, vous pouvez utiliser l’activité d’exécution par lots Azure ML pour appeler à la fois le service web de formation et le service web de notation.

Une fois que vous avez fini la reformation, mettez à jour le service web de notation (expérience prédictive exposée comme un service web) avec le modèle qui vient d’être formé à l’aide de l’**Activité des ressources de mise à jour Azure ML**. Consultez l’article [Mise à jour des modèles à l’aide de l’activité des ressources de mise à jour](data-factory-azure-ml-update-resource-activity.md) pour plus d’informations.

## <a name="invoking-a-web-service-using-batch-execution-activity"></a>Appeler un service web à l’aide de l’activité d’exécution par lots
Vous utilisez Azure Data Factory pour orchestrer le déplacement et le traitement des données, puis pour effectuer une exécution par lot à l’aide d’Azure Machine Learning. Voici les étapes principales :

1. Créer un service lié Azure Machine Learning. Vous avez besoin des valeurs suivantes :

   1. **URI DE DEMANDE** pour l’API d’exécution de lot. Pour trouver l’URI de demande, cliquez sur le lien **EXÉCUTION PAR LOT** dans la page des services web.
   2. **CLÉ API** pour le service web Azure Machine Learning publié. Vous trouverez la clé API en cliquant sur le service web que vous avez publié.
   3. L’activité **AzureMLBatchExecution** .

      ![Tableau de bord Machine Learning](./media/data-factory-azure-ml-batch-execution-activity/AzureMLDashboard.png)

      ![URI de lot](./media/data-factory-azure-ml-batch-execution-activity/batch-uri.png)

### <a name="scenario-experiments-using-web-service-inputsoutputs-that-refer-to-data-in-azure-blob-storage"></a>Scénario : utilisation d’entrées/sorties de service web qui font référence à des données du stockage d’objets blob Azure
Dans ce scénario, le service web Azure Machine Learning effectue des prédictions à l’aide des données d’un fichier dans un stockage d’objets blob Azure et stocke les résultats des prédictions dans le stockage d’objets blob. Le code JSON suivant définit un pipeline Data Factory avec une activité AzureMLBatchExecution. L’activité a le jeu de données **DecisionTreeInputBlob** en tant qu’entrée, et le jeu de données **DecisionTreeResultBlob** en tant que sortie. Le jeu de données **DecisionTreeInputBlob** est transmis en tant qu’entrée au service web à l’aide de la propriété JSON **webServiceInput**. Le jeu de données **DecisionTreeResultBlob** est transmis en tant que sortie au service web à l’aide de la propriété JSON **webServiceOuputs**.  

> [!IMPORTANT]
> Si le service web prend plusieurs entrées, utilisez la propriété **webServiceInputs** au lieu de la propriété **webServiceInput**. Consultez la section [Service web nécessitant plusieurs entrées](#web-service-requires-multiple-inputs) pour obtenir un exemple d’utilisation de la propriété webServiceInputs.
>
> Les jeux de données référencés par les propriétés **webServiceInput**/**webServiceInputs** et **webServiceOutputs** (dans **typeProperties**) doivent également être inclus dans les **entrées** et **sorties** de l’activité.
>
> Dans votre expérience Azure ML, les ports et paramètres globaux de l’entrée et la sortie du service web ont des noms par défaut (« input1 », « input2 ») que vous pouvez personnaliser. Les noms que vous utilisez pour les paramètres globalParameters, webServiceOutputs et webServiceInputs doivent correspondre exactement aux noms utilisés dans les expériences. Vous pouvez afficher la charge utile de l’exemple de requête sur la page d’aide relative à l’exécution par lots pour votre point de terminaison Azure ML afin de vérifier le mappage attendu.
>
>

```JSON
{
  "name": "PredictivePipeline",
  "properties": {
    "description": "use AzureML model",
    "activities": [
      {
        "name": "MLActivity",
        "type": "AzureMLBatchExecution",
        "description": "prediction analysis on batch input",
        "inputs": [
          {
            "name": "DecisionTreeInputBlob"
          }
        ],
        "outputs": [
          {
            "name": "DecisionTreeResultBlob"
          }
        ],
        "linkedServiceName": "MyAzureMLLinkedService",
        "typeProperties":
        {
            "webServiceInput": "DecisionTreeInputBlob",
            "webServiceOutputs": {
                "output1": "DecisionTreeResultBlob"
            }                
        },
        "policy": {
          "concurrency": 3,
          "executionPriorityOrder": "NewestFirst",
          "retry": 1,
          "timeout": "02:00:00"
        }
      }
    ],
    "start": "2016-02-13T00:00:00Z",
    "end": "2016-02-14T00:00:00Z"
  }
}
```
> [!NOTE]
> Seules les entrées et sorties de l’activité AzureMLBatchExecution peuvent être transmises en tant que paramètres au service web. Par exemple, dans l’extrait de code JSON ci-dessus, DecisionTreeInputBlob est une entrée de l’activité AzureMLBatchExecution, qui est transmise comme entrée au service web via le paramètre webServiceInput.   
>
>

### <a name="example"></a>exemples
Cet exemple utilise Azure Storage pour stocker les données d'entrée et de sortie.

Nous vous recommandons de suivre le didacticiel [Créer votre premier pipeline avec Data Factory][adf-build-1st-pipeline] avant de consulter cet exemple. Utilisez Data Factory Editor pour créer des artefacts Data Factory (services liés, jeux de données, pipeline) dans cet exemple.   

1. Créez un **service lié** pour votre service **Azure Storage**. Si les fichiers d’entrée et de sortie se trouvent dans des comptes de stockage distincts, vous avez besoin de deux services liés. Voici un exemple JSON :

    ```JSON
    {
      "name": "StorageLinkedService",
      "properties": {
        "type": "AzureStorage",
        "typeProperties": {
          "connectionString": "DefaultEndpointsProtocol=https;AccountName=[acctName];AccountKey=[acctKey]"
        }
      }
    }
    ```
2. Créez le **jeu de données** Azure Data Factory d’**entrée**. Contrairement à d’autres jeux de données Data Factory, ceux-ci doivent contenir les valeurs **folderPath** et **fileName**. Vous pouvez utiliser le partitionnement et provoquer l'exécution de chaque lot (chaque tranche de données) pour traiter ou produire des fichiers d'entrée et de sortie uniques. Vous aurez peut-être besoin d’inclure une activité en amont pour convertir l’entrée au format de fichier CSV, et la placer dans le compte de stockage pour chaque tranche. Dans ce cas, n’incluez pas les paramètres **external** et **externalData** indiqués dans l’exemple suivant. Par ailleurs, DecisionTreeInputBlob représente le jeu de données de sortie d’une autre activité.

    ```JSON
    {
      "name": "DecisionTreeInputBlob",
      "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
          "folderPath": "azuremltesting/input",
          "fileName": "in.csv",
          "format": {
            "type": "TextFormat",
            "columnDelimiter": ","
          }
        },
        "external": true,
        "availability": {
          "frequency": "Day",
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

    Votre fichier csv d’entrée doit disposer d’une ligne d’en-tête de colonnes. Si vous utilisez **Copier l’activité** pour créer/déplacer le fichier .csv dans le stockage d’objets blob, vous devez définir la propriété du récepteur **blobWriterAddHeader** sur **true**. Par exemple : 

    ```JSON
    sink:
    {
        "type": "BlobSink",     
        "blobWriterAddHeader": true
    }
    ```

    Si le fichier csv ne dispose pas de ligne d'en-tête, l'erreur suivante risque de se produire : **Erreur pendant l'activité : erreur de lecture de la chaîne. Jeton inattendu : StartObject. Chemin d’accès ’’, ligne 1, position 1**.
3. Créez le **jeu de données** Azure Data Factory de **sortie**. Cet exemple utilise le partitionnement pour créer un chemin de sortie unique à chaque exécution de tranche. Sans partitionnement, l’activité remplace le fichier.

    ```JSON
    {
      "name": "DecisionTreeResultBlob",
      "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
          "folderPath": "azuremltesting/scored/{folderpart}/",
          "fileName": "{filepart}result.csv",
          "partitionedBy": [
            {
              "name": "folderpart",
              "value": {
                "type": "DateTime",
                "date": "SliceStart",
                "format": "yyyyMMdd"
              }
            },
            {
              "name": "filepart",
              "value": {
                "type": "DateTime",
                "date": "SliceStart",
                "format": "HHmmss"
              }
            }
          ],
          "format": {
            "type": "TextFormat",
            "columnDelimiter": ","
          }
        },
        "availability": {
          "frequency": "Day",
          "interval": 15
        }
      }
    }
    ```
4. Créez un **service lié** de type **AzureMLLinkedService** en fournissant la clé API et l’URL d’exécution par lots du modèle.

    ```JSON
    {
      "name": "MyAzureMLLinkedService",
      "properties": {
        "type": "AzureML",
        "typeProperties": {
          "mlEndpoint": "https://[batch execution endpoint]/jobs",
          "apiKey": "[apikey]"
        }
      }
    }
    ```
5. Enfin, créez un pipeline contenant une activité **AzureMLBatchExecution** . Au moment de l’exécution, le pipeline effectue les étapes suivantes :

   1. Obtient l’emplacement du fichier d’entrée à partir de vos jeux de données d’entrée.
   2. Appelle l’API d’exécution par lot Azure Machine Learning.
   3. Copie la sortie de l’exécution par lot dans l’objet blob spécifié dans votre jeu de données de sortie.

      > [!NOTE]
      > L’activité AzureMLBatchExecution peut avoir zéro ou plusieurs entrées et une ou plusieurs sorties.
      >
      >

    ```JSON
    {
        "name": "PredictivePipeline",
        "properties": {
            "description": "use AzureML model",
            "activities": [
            {
                "name": "MLActivity",
                "type": "AzureMLBatchExecution",
                "description": "prediction analysis on batch input",
                "inputs": [
                {
                    "name": "DecisionTreeInputBlob"
                }
                ],
                "outputs": [
                {
                    "name": "DecisionTreeResultBlob"
                }
                ],
                "linkedServiceName": "MyAzureMLLinkedService",
                "typeProperties":
                {
                    "webServiceInput": "DecisionTreeInputBlob",
                    "webServiceOutputs": {
                        "output1": "DecisionTreeResultBlob"
                    }                
                },
                "policy": {
                    "concurrency": 3,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1,
                    "timeout": "02:00:00"
                }
            }
            ],
            "start": "2016-02-13T00:00:00Z",
            "end": "2016-02-14T00:00:00Z"
        }
    }
    ```

      Les dates/heures de **début** et de **fin** doivent toutes deux être au [format ISO](http://en.wikipedia.org/wiki/ISO_8601). Par exemple : 2014-10-14T16:32:41Z. L’heure de **fin** est facultative. Si vous ne spécifiez aucune valeur pour la propriété **end**, cette dernière est calculée comme suit : « **start + 48 heures** ». Pour exécuter le pipeline indéfiniment, spécifiez **9999-09-09** comme valeur pour la propriété **end**. Pour plus d'informations sur les propriétés JSON, consultez [Référence sur la création de scripts JSON](https://msdn.microsoft.com/library/dn835050.aspx) .

      > [!NOTE]
      > Définir une entrée pour l’activité AzureMLBatchExecution est facultatif.
      >
      >

### <a name="scenario-experiments-using-readerwriter-modules-to-refer-to-data-in-various-storages"></a>Scénario : utilisation de modules lecteur/enregistreur pour faire référence à des données dans différents stockages
Un autre scénario courant pour créer des expériences Azure ML consiste à utiliser des modules lecteur et enregistreur. Le module lecteur permet de charger des données dans une expérience, tandis que le module enregistreur sert à enregistrer les données issues de cette expérience. Pour plus d’informations sur les modules lecteur et enregistreur, voir les rubriques [Lecteur](https://msdn.microsoft.com/library/azure/dn905997.aspx) et [Enregistreur](https://msdn.microsoft.com/library/azure/dn905984.aspx) dans la bibliothèque MSDN.     

Quand vous utilisez les modules lecteur et enregistreur, nous vous recommandons de recourir à un paramètre de service web pour chaque propriété de ces modules. Ces paramètres web permettent de configurer les valeurs pendant l’exécution. Par exemple, vous pouvez créer une expérience avec un module lecteur qui utilise une base de données Azure SQL Database : XXX.database.windows.net. Une fois le service web déployé, vous pouvez autoriser les consommateurs du service web à spécifier un autre serveur Azure SQL Server appelé YYY.database.windows.net. Vous pouvez utiliser un paramètre de service web pour permettre à cette valeur d’être configurée.

> [!NOTE]
> L’entrée et la sortie du service web diffèrent des paramètres de service web. Dans le premier scénario, vous avez vu comment une entrée et une sortie peuvent être spécifiées pour un service web Azure ML. Dans ce scénario, vous passez pour un service web des paramètres qui correspondent aux propriétés des modules lecteur/enregistreur.
>
>

Examinons un scénario d’utilisation de paramètres de service web. Vous disposez d’un service web Azure Machine Learning déployé qui utilise un module lecteur pour lire les données de l’une des sources de données prises en charge par Azure Machine Learning (par exemple : Azure SQL Database). Après l’exécution par lots, les résultats sont écrits à l’aide d’un module enregistreur (Azure SQL Database).  Aucune entrée ou sortie de service web n’est définie dans les expériences. Dans ce cas, nous vous recommandons de configurer les paramètres de service web appropriés pour les modules lecteur et enregistreur. Cela permet la configuration des modules lecteur/enregistreur quand vous utilisez l’activité AzureMLBatchExecution. Spécifiez les paramètres de service web dans la section **globalParameters** du code JSON de l’activité comme suit.

```JSON
"typeProperties": {
    "globalParameters": {
        "Param 1": "Value 1",
        "Param 2": "Value 2"
    }
}
```

Vous pouvez également utiliser les [fonctions de Data Factory](data-factory-functions-variables.md) pour transmettre les valeurs aux paramètres de service web, comme indiqué dans l'exemple suivant :

```JSON
"typeProperties": {
    "globalParameters": {
       "Database query": "$$Text.Format('SELECT * FROM myTable WHERE timeColumn = \\'{0:yyyy-MM-dd HH:mm:ss}\\'', Time.AddHours(WindowStart, 0))"
    }
}
```

> [!NOTE]
> Les paramètres de service web respectent la casse ; veillez donc à ce que les noms que vous indiquez dans le script JSON de l'activité correspondent à ceux exposés par le service web.
>
>

### <a name="using-a-reader-module-to-read-data-from-multiple-files-in-azure-blob"></a>Utilisation d’un module lecteur pour lire les données de plusieurs fichiers dans le stockage d’objets blob Azure
Les pipelines Big Data avec des activités telles que Pig et Hive peuvent produire un ou plusieurs fichiers de sortie sans extensions. Par exemple, quand vous spécifiez une table Hive externe, les données de cette table peuvent être stockées dans le stockage d’objets blob Azure avec le nom 000000_0 suivant. Vous pouvez utiliser le module lecteur dans une expérience pour lire plusieurs fichiers et les utiliser pour les prédictions.

Quand vous utilisez le module lecteur dans une expérience Azure Machine Learning, vous pouvez spécifier un objet blob Azure comme entrée. Les fichiers du stockage d’objets blob Azure peuvent être les fichiers de sortie (par exemple, 000000_0) qui sont générés par un script Pig et Hive exécuté sur HDInsight. Le module lecteur vous permet de lire des fichiers (sans extension) en configurant le **chemin d’accès au conteneur et le répertoire/l’objet blob**. Le **chemin d’accès au conteneur** pointe vers le conteneur et le **répertoire/objet blob** pointe vers le dossier qui contient les fichiers, comme illustré dans l’image suivante. L’astérisque \*) **spécifie que tous les fichiers du conteneur/dossier (c’est-à-dire, data/aggregateddata/year=2014/month-6/*\*)** sont lus dans le cadre de l’expérience.

![Propriétés des objets blob Azure](./media/data-factory-create-predictive-pipelines/azure-blob-properties.png)

### <a name="example"></a>exemples
#### <a name="pipeline-with-azuremlbatchexecution-activity-with-web-service-parameters"></a>Pipeline avec l’activité AzureMLBatchExecution avec les paramètres de service web

```JSON
{
  "name": "MLWithSqlReaderSqlWriter",
  "properties": {
    "description": "Azure ML model with sql azure reader/writer",
    "activities": [
      {
        "name": "MLSqlReaderSqlWriterActivity",
        "type": "AzureMLBatchExecution",
        "description": "test",
        "inputs": [
          {
            "name": "MLSqlInput"
          }
        ],
        "outputs": [
          {
            "name": "MLSqlOutput"
          }
        ],
        "linkedServiceName": "MLSqlReaderSqlWriterDecisionTreeModel",
        "typeProperties":
        {
            "webServiceInput": "MLSqlInput",
            "webServiceOutputs": {
                "output1": "MLSqlOutput"
            }
              "globalParameters": {
                "Database server name": "<myserver>.database.windows.net",
                "Database name": "<database>",
                "Server user account name": "<user name>",
                "Server user account password": "<password>"
              }              
        },
        "policy": {
          "concurrency": 1,
          "executionPriorityOrder": "NewestFirst",
          "retry": 1,
          "timeout": "02:00:00"
        },
      }
    ],
    "start": "2016-02-13T00:00:00Z",
    "end": "2016-02-14T00:00:00Z"
  }
}
```

Dans l'exemple JSON ci-dessus :

* Le service web Azure Machine Learning déployé utilise un module lecteur et un module enregistreur pour lire/écrire des données depuis/vers une base de données Azure SQL Database. Ce service web expose les quatre paramètres suivants : Database server name, Database name, Server user account name et Server user account password.  
* Les dates/heures de **début** et de **fin** doivent toutes deux être au [format ISO](http://en.wikipedia.org/wiki/ISO_8601). Par exemple : 2014-10-14T16:32:41Z. L’heure de **fin** est facultative. Si vous ne spécifiez aucune valeur pour la propriété **end**, cette dernière est calculée comme suit : « **start + 48 heures** ». Pour exécuter le pipeline indéfiniment, spécifiez **9999-09-09** comme valeur pour la propriété **end**. Pour plus d'informations sur les propriétés JSON, consultez [Référence sur la création de scripts JSON](https://msdn.microsoft.com/library/dn835050.aspx) .

### <a name="other-scenarios"></a>Autres scénarios
#### <a name="web-service-requires-multiple-inputs"></a>Service web nécessitant plusieurs entrées
Si le service web prend plusieurs entrées, utilisez la propriété **webServiceInputs** au lieu de la propriété **webServiceInput**. Les jeux de données référencés par **webServiceInputs** doivent également être inclus dans les **entrées** de l’activité.

Dans votre expérience Azure ML, les ports et paramètres globaux de l’entrée et la sortie du service web ont des noms par défaut (« input1 », « input2 ») que vous pouvez personnaliser. Les noms que vous utilisez pour les paramètres globalParameters, webServiceOutputs et webServiceInputs doivent correspondre exactement aux noms utilisés dans les expériences. Vous pouvez afficher la charge utile de l’exemple de requête sur la page d’aide relative à l’exécution par lots pour votre point de terminaison Azure ML afin de vérifier le mappage attendu.

```JSON
{
    "name": "PredictivePipeline",
    "properties": {
        "description": "use AzureML model",
        "activities": [{
            "name": "MLActivity",
            "type": "AzureMLBatchExecution",
            "description": "prediction analysis on batch input",
            "inputs": [{
                "name": "inputDataset1"
            }, {
                "name": "inputDataset2"
            }],
            "outputs": [{
                "name": "outputDataset"
            }],
            "linkedServiceName": "MyAzureMLLinkedService",
            "typeProperties": {
                "webServiceInputs": {
                    "input1": "inputDataset1",
                    "input2": "inputDataset2"
                },
                "webServiceOutputs": {
                    "output1": "outputDataset"
                }
            },
            "policy": {
                "concurrency": 3,
                "executionPriorityOrder": "NewestFirst",
                "retry": 1,
                "timeout": "02:00:00"
            }
        }],
        "start": "2016-02-13T00:00:00Z",
        "end": "2016-02-14T00:00:00Z"
    }
}
```

#### <a name="web-service-does-not-require-an-input"></a>Le service web ne nécessite pas d’entrée
Les services web d’exécution par lot Azure ML peuvent servir à exécuter n’importe quel flux de travail (par exemple des scripts R ou Python) qui ne nécessite pas d’entrées. Ou bien, l’expérience peut être configurée avec un module Lecteur qui n’expose pas de paramètres GlobalParameters. Dans ce cas, l’activité AzureMLBatchExecution doit être configurée comme suit :

```JSON
{
    "name": "scoring service",
    "type": "AzureMLBatchExecution",
    "outputs": [
        {
            "name": "myBlob"
        }
    ],
    "typeProperties": {
        "webServiceOutputs": {
            "output1": "myBlob"
        }              
     },
    "linkedServiceName": "mlEndpoint",
    "policy": {
        "concurrency": 1,
        "executionPriorityOrder": "NewestFirst",
        "retry": 1,
        "timeout": "02:00:00"
    }
},
```

#### <a name="web-service-does-not-require-an-inputoutput"></a>Le service web ne nécessite pas d’entrée/sortie
Il se peut qu’aucune sortie de service web ne soit configurée pour le service web d’exécution par lot Azure ML. Dans cet exemple, aucune entrée ou sortie ni aucun paramètre GlobalParameters n’est configuré. Il existe toujours une sortie configurée sur l’activité elle-même, mais elle n’est pas donnée comme sortie webServiceOutput.

```JSON
{
    "name": "retraining",
    "type": "AzureMLBatchExecution",
    "outputs": [
        {
            "name": "placeholderOutputDataset"
        }
    ],
    "typeProperties": {
     },
    "linkedServiceName": "mlEndpoint",
    "policy": {
        "concurrency": 1,
        "executionPriorityOrder": "NewestFirst",
        "retry": 1,
        "timeout": "02:00:00"
    }
},
```

#### <a name="web-service-uses-readers-and-writers-and-the-activity-runs-only-when-other-activities-have-succeeded"></a>Le service web utilise des lecteurs et enregistreurs et l’activité s’exécute uniquement lorsque d’autres activités ont réussi
Les modules de lecteur et d’enregistreur du service web Azure ML peuvent être configurés pour s’exécuter avec ou sans paramètres GlobalParameters. Toutefois, il peut être utile d’incorporer les appels de service dans un pipeline qui utilise des dépendances de jeux de données, afin d’appeler le service uniquement lorsqu’un traitement en amont est terminé. Cette approche vous permet également de déclencher d’autres actions une fois l’exécution par lot terminée. Dans ce cas, vous pouvez exprimer les dépendances à l’aide d’entrées et de sorties d’activité, sans les nommer en tant qu’entrées ou sorties de service web.

```JSON
{
    "name": "retraining",
    "type": "AzureMLBatchExecution",
    "inputs": [
        {
            "name": "upstreamData1"
        },
        {
            "name": "upstreamData2"
        }
    ],
    "outputs": [
        {
            "name": "downstreamData"
        }
    ],
    "typeProperties": {
     },
    "linkedServiceName": "mlEndpoint",
    "policy": {
        "concurrency": 1,
        "executionPriorityOrder": "NewestFirst",
        "retry": 1,
        "timeout": "02:00:00"
    }
},
```

Les **points importants** sont les suivants :

* Si le point de terminaison de votre expérience utilise un élément webServiceInput, il est représenté par un jeu de données d’objets blob et il est inclus dans les entrées de l’activité, ainsi que dans la propriété webServiceInput. Sinon, la propriété webServiceInput est omise.
* Si le point de terminaison de votre expérience utilise des éléments webServiceOutput, ils sont représentés par des jeux de données d’objets blob et sont inclus dans les sorties de l’activité, ainsi que dans la propriété webServiceOutputs. Les sorties de l’activité et les éléments webServiceOutputs sont mappés par le nom de chaque sortie de l’expérience. Sinon, la propriété webServiceOutputs est omise.
* Si le point de terminaison de votre expérience expose des éléments globalParameters, ceux-ci figurent dans la propriété globalParameters de l’activité sous forme de paires clé/valeur. Sinon, la propriété globalParameters est omise. Les clés sont sensibles à la casse. [fonctions Azure Data Factory](data-factory-functions-variables.md) peuvent être utilisées dans les valeurs.
* Des jeux de données supplémentaires peuvent être inclus dans les propriétés d’entrée et de sortie de l’activité, sans être référencés dans l’activité typeProperties. Ces jeux de données contrôlent l’exécution à l’aide de dépendances entre les tranches. Sinon, ils sont ignorés par l’activité AzureMLBatchExecution.


## <a name="updating-models-using-update-resource-activity"></a>Mise à jour des modèles à l’aide de l’activité des ressources de mise à jour
Une fois que vous avez fini la reformation, mettez à jour le service web de notation (expérience prédictive exposée comme un service web) avec le modèle qui vient d’être formé à l’aide de l’**Activité des ressources de mise à jour Azure ML**. Consultez l’article [Mise à jour des modèles à l’aide de l’activité des ressources de mise à jour](data-factory-azure-ml-update-resource-activity.md) pour plus d’informations.

### <a name="reader-and-writer-modules"></a>Modules Lecteur et Enregistreur
L'utilisation des paramètres de service web passe par un scénario commun : l'utilisation des lecteurs et enregistreurs SQL Azure. Le module lecteur est utilisé pour charger des données dans une expérience à partir des services de gestion des données en dehors d’Azure Machine Learning Studio. Le module enregistreur est utilisé pour enregistrer les données de vos expériences dans les services de gestion des données en dehors d’Azure Machine Learning Studio.  

Pour plus d’informations sur les modules enregistreur/lecteur Azure Blob/SQL Azure, voir les rubriques [Lecteur](https://msdn.microsoft.com/library/azure/dn905997.aspx) et [Enregistreur](https://msdn.microsoft.com/library/azure/dn905984.aspx) dans la bibliothèque MSDN. L'exemple de la section précédente utilisait le lecteur et l'enregistreur d'objets blob Azure. Cette section décrit leur utilisation.

## <a name="frequently-asked-questions"></a>Questions fréquentes (FAQ)
**Q :** J’ai plusieurs fichiers qui sont générés par mes pipelines Big Data. L’activité AzureMLBatchExecution peut-elle fonctionner sur tous les fichiers ?

**R :** Oui. Pour plus d’informations, consultez la section **Utilisation d’un module lecteur pour lire les données de plusieurs fichiers dans le stockage d’objets blob Azure** .

## <a name="azure-ml-batch-scoring-activity"></a>Activité de notation par lots Azure ML
Si vous utilisez l’activité **AzureMLBatchScoring** en vue d’une intégration avec Azure Machine Learning, nous vous recommandons d’utiliser la dernière activité **AzureMLBatchExecution**.

L’activité AzureMLBatchExecution est introduite dans la version d’août 2015 du Kit de développement logiciel (SDK) Azure et d’Azure PowerShell.

Si vous souhaitez continuer à utiliser l’activité AzureMLBatchScoring, poursuivez la lecture de cette section.  

### <a name="azure-ml-batch-scoring-activity-using-azure-storage-for-inputoutput"></a>Activité de notation par lots Azure ML utilisant Azure Storage pour l’entrée/la sortie

```JSON
{
  "name": "PredictivePipeline",
  "properties": {
    "description": "use AzureML model",
    "activities": [
      {
        "name": "MLActivity",
        "type": "AzureMLBatchScoring",
        "description": "prediction analysis on batch input",
        "inputs": [
          {
            "name": "ScoringInputBlob"
          }
        ],
        "outputs": [
          {
            "name": "ScoringResultBlob"
          }
        ],
        "linkedServiceName": "MyAzureMLLinkedService",
        "policy": {
          "concurrency": 3,
          "executionPriorityOrder": "NewestFirst",
          "retry": 1,
          "timeout": "02:00:00"
        }
      }
    ],
    "start": "2016-02-13T00:00:00Z",
    "end": "2016-02-14T00:00:00Z"
  }
}
```

### <a name="web-service-parameters"></a>Paramètres de service web
Pour spécifier les valeurs des paramètres de service web, ajoutez une section **typeProperties** à la section **AzureMLBatchScoringActivty** dans le script JSON du pipeline, comme indiqué dans l’exemple suivant :

```JSON
"typeProperties": {
    "webServiceParameters": {
        "Param 1": "Value 1",
        "Param 2": "Value 2"
    }
}
```
Vous pouvez également utiliser les [fonctions de Data Factory](data-factory-functions-variables.md) pour transmettre les valeurs aux paramètres de service web, comme indiqué dans l'exemple suivant :

```JSON
"typeProperties": {
    "webServiceParameters": {
       "Database query": "$$Text.Format('SELECT * FROM myTable WHERE timeColumn = \\'{0:yyyy-MM-dd HH:mm:ss}\\'', Time.AddHours(WindowStart, 0))"
    }
}
```

> [!NOTE]
> Les paramètres de service web respectent la casse ; veillez donc à ce que les noms que vous indiquez dans le script JSON de l'activité correspondent à ceux exposés par le service web.
>
>

## <a name="see-also"></a>Voir aussi
* [Article de blog Azure : prise en main d’Azure Data Factory et d’Azure Machine Learning](https://azure.microsoft.com/blog/getting-started-with-azure-data-factory-and-azure-machine-learning-4/)

[adf-build-1st-pipeline]: data-factory-build-your-first-pipeline.md

[azure-machine-learning]: http://azure.microsoft.com/services/machine-learning/
