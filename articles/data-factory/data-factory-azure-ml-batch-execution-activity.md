---
title: "les pipelines de données prédictives aaaCreate à l’aide d’Azure Data Factory | Documents Microsoft"
description: "Décrit comment toocreate créer des pipelines PRÉDICTIFS à l’aide d’Azure Data Factory et Azure Machine Learning"
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
ms.date: 05/16/2017
ms.author: shlo
ms.openlocfilehash: 943210c28b1696e299ff9b7cc96369b95f182354
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
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

### <a name="azure-machine-learning"></a>Azure Machine Learning
[Azure Machine Learning](https://azure.microsoft.com/documentation/services/machine-learning/) Active toobuild, tester et déployer des solutions d’analytique prédictive. D’un point de vue très général, cela s’effectue en trois étapes :

1. **Créez une expérience de formation**. Vous effectuez cette étape à l’aide de hello Azure ML Studio. ML studio de Hello est un environnement collaboratif de développement visuel que vous utilisez tootrain et testez d’un modèle prédictif analytique à l’aide des données d’apprentissage.
2. **Convertir les expérience prédictive tooa**. Une fois que votre modèle a été formé avec des données existantes et que vous êtes prêt toouse il tooscore de nouvelles données, préparer et de simplifier votre expérience pour calculer les scores.
3. **Déployez-la en tant que service web**. Vous pouvez publier votre expérience de notation comme un service web Azure. Vous pouvez envoyer le modèle de tooyour des données via ce point de terminaison de service web et recevoir des prédictions de résultat de modèle de hello.  

### <a name="azure-data-factory"></a>Azure Data Factory
Fabrique de données est un service d’intégration de données basés sur le cloud qui orchestre et automatise hello **mouvement** et **transformation** de données. Vous pouvez créer des solutions d’intégration données à l’aide d’Azure Data Factory réception des données à partir de différentes banques de données, / processus de transformation des données de hello, et publier des données de résultats hello toohello des magasins de données.

Service de fabrique de données vous permet des pipelines de données toocreate déplacent et transforment des données et puis exécutez les pipelines hello selon un calendrier défini (horaire, quotidienne, hebdomadaire, etc.). Il fournit également lignage de visualisation enrichie toodisplay hello et les dépendances entre vos pipelines de données et surveiller vos pipelines de données à partir d’une vue unifiée unique tooeasily localiser les problèmes et configurer des alertes d’analyse.

Consultez [Introduction tooAzure Data Factory](data-factory-introduction.md) et [générer votre première pipeline](data-factory-build-your-first-pipeline.md) articles tooquickly prise en main hello service Azure Data Factory.

### <a name="data-factory-and-machine-learning-together"></a>Data Factory et Machine Learning
Azure permet de Data Factory tooeasily vous créer des pipelines qui utilisent un rapport publié [Azure Machine Learning] [ azure-machine-learning] web service pour l’analytique prédictive. À l’aide de hello **l’activité d’exécution par lots** dans un pipeline Azure Data Factory, vous pouvez appeler une Azure ML web service toomake de prédictions sur les données de salutation dans le lot. Consultez [appel d’un Azure ML à l’aide du service web hello l’activité d’exécution par lots](#invoking-an-azure-ml-web-service-using-the-batch-execution-activity) pour plus d’informations.

Au fil du temps, utiliser des modèles prédictifs hello dans des expériences de score Azure ML hello doivent toobe reformé à l’aide de nouveaux jeux de données d’entrée. Vous pouvez recycler un modèle Azure ML à partir d’un pipeline de fabrique de données en procédant comme hello comme suit :

1. Publier l’expérience de formation hello (expérience pas prédictive) comme un service web. Vous effectuez cette étape Bonjour Azure ML Studio comme vous le faisiez expérience prédictive de tooexpose comme un service web dans le scénario précédent de hello.
2. Utilisez hello activité de l’exécution du lot Azure ML tooinvoke hello web service pour une expérience de formation hello. En fait, vous pouvez utiliser hello exécution du lot Azure ML activité tooinvoke apprentissage service web et le calcul du score du service web.

Une fois que vous avez terminé avec le réapprentissage, mettre à jour hello calculer les scores avec qui vient d’être formé hello le service web (expérience prédictive exposé comme service web) à l’aide de hello **activité de la ressource mise à jour Azure ML**. Consultez l’article [Mise à jour des modèles à l’aide de l’activité des ressources de mise à jour](data-factory-azure-ml-update-resource-activity.md) pour plus d’informations.

## <a name="invoking-a-web-service-using-batch-execution-activity"></a>Appeler un service web à l’aide de l’activité d’exécution par lots
Vous utilisez le traitement et le déplacement des données de Azure Data Factory tooorchestrate, puis effectuez l’exécution du lot à l’aide d’Azure Machine Learning. Voici les étapes de niveau supérieur de hello :

1. Créer un service lié Azure Machine Learning. Vous devez hello valeurs suivantes :

   1. **URI de demande** pour hello API de l’exécution du lot. Vous pouvez trouver hello URI de requête en cliquant sur hello **l’exécution par lots** lien dans la page des services web hello.
   2. **Clé API** pour hello publié le service web Azure Machine Learning. Vous trouverez la clé d’API hello en cliquant sur le service web hello que vous avez publié.
   3. Hello d’utilisation **AzureMLBatchExecution** activité.

      ![Tableau de bord Machine Learning](./media/data-factory-azure-ml-batch-execution-activity/AzureMLDashboard.png)

      ![URI de lot](./media/data-factory-azure-ml-batch-execution-activity/batch-uri.png)

### <a name="scenario-experiments-using-web-service-inputsoutputs-that-refer-toodata-in-azure-blob-storage"></a>Scénario : Expériences à l’aide de la charge des entrées/sorties de service de Web qui font référence toodata dans le stockage d’objets Blob Azure
Dans ce scénario, hello service Web de Azure Machine Learning effectue des prédictions à l’aide des données à partir d’un fichier dans un stockage d’objets blob Azure et stocke les résultats de prédiction hello dans le stockage blob hello. Hello JSON suivant définit un pipeline de fabrique de données avec une activité AzureMLBatchExecution. activité Hello a hello dataset **DecisionTreeInputBlob** en tant qu’entrée et **DecisionTreeResultBlob** en tant que sortie de hello. Hello **DecisionTreeInputBlob** est passée comme un service web toohello d’entrée à l’aide de hello **webServiceInput** propriété JSON. Hello **DecisionTreeResultBlob** est passé en tant que sortie toohello Web service par à l’aide de hello **webServiceOutputs** propriété JSON.  

> [!IMPORTANT]
> Si le service web de hello accepte plusieurs entrées, utilisez hello **webServiceInputs** propriété au lieu d’utiliser **webServiceInput**. Consultez hello [service Web nécessite plusieurs entrées](#web-service-requires-multiple-inputs) pour obtenir un exemple d’utilisation de hello webServiceInputs propriété.
>
> Jeux de données qui est référencées par hello **webServiceInput**/**webServiceInputs** et **webServiceOutputs** propriétés (dans  **typeProperties**) doit également être inclus dans hello activité **entrées** et **génère**.
>
> Dans votre expérience Azure ML, les ports et paramètres globaux de l’entrée et la sortie du service web ont des noms par défaut (« input1 », « input2 ») que vous pouvez personnaliser. noms Hello que vous utilisez pour webServiceInputs, webServiceOutputs et globalParameters paramètres doivent correspondre exactement noms hello dans des expériences de hello. Vous pouvez afficher la charge utile de demande hello exemple sur la page d’aide de l’exécution de lot hello pour votre mappage hello attendu d’Azure ML point de terminaison tooverify.
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
> Uniquement les entrées et sorties de hello AzureMLBatchExecution activité peuvent être passés en tant que paramètres toohello service Web. Par exemple, Bonjour ci-dessus extrait de code JSON, DecisionTreeInputBlob est une activité AzureMLBatchExecution, qui est passée comme un service Web de toohello d’entrée via un paramètre de webServiceInput de toohello d’entrée.   
>
>

### <a name="example"></a>Exemple
Cette toohold de stockage Azure exemple utilise les deux hello les données d’entrée et de sortie.

Nous recommandons que vous parcourez hello [générer votre première pipeline avec Data Factory] [ adf-build-1st-pipeline] didacticiel avant de passer par cet exemple. Utiliser des artefacts de Data Factory hello éditeur Data Factory toocreate (services liés, les datasets, pipeline) dans cet exemple.   

1. Créez un **service lié** pour votre service **Azure Storage**. Si hello des fichiers d’entrée et de sortie sont dans différents comptes de stockage, vous avez besoin de deux services liés. Voici un exemple JSON :

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
2. Créer hello **d’entrée** Azure Data Factory **dataset**. Contrairement à d’autres jeux de données Data Factory, ceux-ci doivent contenir les valeurs **folderPath** et **fileName**. Vous pouvez utiliser toocause partitionnement chaque tooprocess (chaque tranche de données) de l’exécution de traitement par lots ou produire une entrée unique et fichiers de sortie. Vous devrez peut-être tooinclude certains hello de tootransform activité en amont d’entrée dans le format de fichier CSV hello et placez-le dans le compte de stockage hello pour chaque secteur. Dans ce cas, vous ne devez pas inclure hello **externe** et **externalData** paramètres affichés dans hello suivant exemple et votre DecisionTreeInputBlob serait hello dataset de sortie d’une autre activité.

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

    Votre fichier csv d’entrée doit avoir la ligne d’en-tête de colonne hello. Si vous utilisez hello **l’activité de copie** toocreate/déplacement hello volumes partagés de cluster dans le stockage d’objets blob hello, vous devez définir les propriétés du récepteur hello **blobWriterAddHeader** trop**true**. Par exemple :

    ```JSON
    sink:
    {
        "type": "BlobSink",     
        "blobWriterAddHeader": true
    }
    ```

    Si un fichier csv hello n’a pas de ligne d’en-tête hello, vous pouvez voir hello l’erreur suivante : **erreur dans l’activité : erreur de lecture de chaîne. Jeton inattendu : StartObject. Chemin d’accès ’’, ligne 1, position 1**.
3. Créer hello **sortie** Azure Data Factory **dataset**. Cet exemple utilise un partitionnement toocreate un chemin d’accès unique pour chaque exécution de la tranche. Sans partitionnement de hello, activité hello entraînerait le remplacement du fichier de hello.

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
4. Créer un **service lié** de type : **AzureMLLinkedService**, en fournissant la clé d’API de hello et modèle d’URL d’exécution du lot.

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
5. Enfin, créez un pipeline contenant une activité **AzureMLBatchExecution** . Lors de l’exécution, le pipeline exécute hello comme suit :

   1. Obtient l’emplacement hello du fichier d’entrée de hello à partir de vos jeux de données d’entrée.
   2. Appelle l’exécution du lot Azure Machine Learning hello API
   3. Copies hello lot d’exécution sortie toohello objet blob fourni dans votre jeu de données de sortie.

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

      Les dates/heures de **début** et de **fin** doivent toutes deux être au [format ISO](http://en.wikipedia.org/wiki/ISO_8601). Par exemple : 2014-10-14T16:32:41Z. Hello **fin** fois est facultative. Si vous ne spécifiez pas de valeur pour hello **fin** propriété, il est calculé en tant que «**start + 48 heures.**» pipeline de hello toorun indéfiniment, spécifiez **9999-09-09** en tant que valeur hello pour hello **fin** propriété. Pour plus d'informations sur les propriétés JSON, consultez [Référence sur la création de scripts JSON](https://msdn.microsoft.com/library/dn835050.aspx) .

      > [!NOTE]
      > Définition d’une entrée pour l’activité de AzureMLBatchExecution hello est facultative.
      >
      >

### <a name="scenario-experiments-using-readerwriter-modules-toorefer-toodata-in-various-storages"></a>Scénario : Expériences à l’aide des Modules de lecture/écriture toorefer toodata dans différents stockages
Un autre scénario courant lors de la création d’expériences Azure ML est toouse des modules de lecture et d’écriture. module de lecture Hello est données tooload utilisé dans une expérience et module de writer hello toosave les données de vos expériences. Pour plus d’informations sur les modules lecteur et enregistreur, voir les rubriques [Lecteur](https://msdn.microsoft.com/library/azure/dn905997.aspx) et [Enregistreur](https://msdn.microsoft.com/library/azure/dn905984.aspx) dans la bibliothèque MSDN.     

Lorsque vous utilisez des modules de lecteur et writer hello, il est conseillé toouse un paramètre de service Web pour chaque propriété de ces modules de lecture/écriture. Ces paramètres web permettent les valeurs hello tooconfigure pendant l’exécution. Par exemple, vous pouvez créer une expérience avec un module lecteur qui utilise une base de données Azure SQL Database : XXX.database.windows.net. Après avoir déployé le service web de hello, vous souhaitez tooenable les consommateurs de hello de hello web service toospecify un autre serveur Azure SQL Server appelée YYY.database.windows.net. Cette toobe valeur configuré, vous pouvez utiliser un tooallow de paramètre de service Web.

> [!NOTE]
> L’entrée et la sortie du service web diffèrent des paramètres de service web. Dans le premier scénario de hello, vous avez vu comment une entrée et la sortie peuvent être spécifiés pour un service Azure ML Web. Dans ce scénario, vous passez des paramètres pour un service Web qui correspondent tooproperties des modules de lecture/écriture.
>
>

Examinons un scénario d’utilisation de paramètres de service web. Vous avez un service web Azure Machine Learning déployé qui utilise un lecteur module tooread de données à partir d’une des sources de données hello pris en charge par Azure Machine Learning (par exemple : base de données SQL Azure). Après que l’exécution du lot hello est effectuée, les résultats hello sont écrites à l’aide d’un module de Writer (de base de données SQL Azure).  Aucune entrées du service web et les sorties ne sont définies dans des expériences de hello. Dans ce cas, nous vous recommandons de configurer les paramètres de service web appropriés pour les modules de lecteur et writer hello. Cette configuration permet de toobe modules configuré à l’aide d’activité de AzureMLBatchExecution hello hello lecture/écriture. Vous spécifiez des paramètres de service Web Bonjour **globalParameters** section dans l’activité hello JSON comme suit.

```JSON
"typeProperties": {
    "globalParameters": {
        "Param 1": "Value 1",
        "Param 2": "Value 2"
    }
}
```

Vous pouvez également utiliser [fonctions de Data Factory](data-factory-functions-variables.md) lors du passage des valeurs hello pour les paramètres de service Web comme indiqué dans hello l’exemple suivant :

```JSON
"typeProperties": {
    "globalParameters": {
       "Database query": "$$Text.Format('SELECT * FROM myTable WHERE timeColumn = \\'{0:yyyy-MM-dd HH:mm:ss}\\'', Time.AddHours(WindowStart, 0))"
    }
}
```

> [!NOTE]
> paramètres de service Web Hello respectent la casse, assurez-vous que les noms de hello que vous spécifiez dans l’activité hello JSON correspondent hello ceux qui sont exposées par le service Web de hello.
>
>

### <a name="using-a-reader-module-tooread-data-from-multiple-files-in-azure-blob"></a>À l’aide d’un lecteur module tooread de données à partir de plusieurs fichiers d’objets Blob Azure
Les pipelines Big Data avec des activités telles que Pig et Hive peuvent produire un ou plusieurs fichiers de sortie sans extensions. Par exemple, lorsque vous spécifiez une table Hive externe, les données hello pour une table Hive hello externe peuvent être stockées dans le stockage blob Azure avec hello suivant 000000_0 de nom. Vous pouvez utiliser le module de lecture hello dans une expérience de tooread plusieurs fichiers et les utiliser pour les prévisions.

Lorsque vous utilisez le module de lecture hello dans une expérience Azure Machine Learning, vous pouvez spécifier les objets Blob Azure en tant qu’entrée. les fichiers de Hello Bonjour stockage d’objets blob Azure peuvent être des fichiers de sortie hello (exemple : 000000_0) qui sont produites par un script Pig et Hive en cours d’exécution sur HDInsight. Hello lecteur module vous permet de fichiers tooread (avec aucune extension) en configurant hello **toocontainer de chemin d’accès, les objets blob ou répertoire**. Hello **toocontainer de chemin d’accès** points toohello conteneur et **objets blob ou répertoire** pointe toofolder qui contient les fichiers de hello comme indiqué dans hello suivant l’image. Hello astérisque, \*) **Spécifie que tous les hello des fichiers dans le dossier/conteneur hello (autrement dit, données/aggregateddata/année = mois/2014-6 /\*)** sont lues dans le cadre de l’expérience de hello.

![Propriétés des objets blob Azure](./media/data-factory-create-predictive-pipelines/azure-blob-properties.png)

### <a name="example"></a>Exemple
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

Bonjour, exemple JSON ci-dessus :

* Hello déployé Azure Machine Learning service Web utilise un lecteur et une writer module tooread/écrire des données à partir de / tooan base de données SQL Azure. Ce service Web expose hello quatre paramètres suivants : nom du serveur, nom de la base de données, le nom de compte d’utilisateur serveur et mot de passe utilisateur serveur de base de données.  
* Les dates/heures de **début** et de **fin** doivent toutes deux être au [format ISO](http://en.wikipedia.org/wiki/ISO_8601). Par exemple : 2014-10-14T16:32:41Z. Hello **fin** fois est facultative. Si vous ne spécifiez pas de valeur pour hello **fin** propriété, il est calculé en tant que «**start + 48 heures.**» pipeline de hello toorun indéfiniment, spécifiez **9999-09-09** en tant que valeur hello pour hello **fin** propriété. Pour plus d'informations sur les propriétés JSON, consultez [Référence sur la création de scripts JSON](https://msdn.microsoft.com/library/dn835050.aspx) .

### <a name="other-scenarios"></a>Autres scénarios
#### <a name="web-service-requires-multiple-inputs"></a>Service web nécessitant plusieurs entrées
Si le service web de hello accepte plusieurs entrées, utilisez hello **webServiceInputs** propriété au lieu d’utiliser **webServiceInput**. Jeux de données qui est référencées par hello **webServiceInputs** doit également être inclus dans hello activité **entrées**.

Dans votre expérience Azure ML, les ports et paramètres globaux de l’entrée et la sortie du service web ont des noms par défaut (« input1 », « input2 ») que vous pouvez personnaliser. noms Hello que vous utilisez pour webServiceInputs, webServiceOutputs et globalParameters paramètres doivent correspondre exactement noms hello dans des expériences de hello. Vous pouvez afficher la charge utile de demande hello exemple sur la page d’aide de l’exécution de lot hello pour votre mappage hello attendu d’Azure ML point de terminaison tooverify.

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
Services web de Azure ML par lots d’exécution peut être utilisé toorun de flux de travail, par exemple R ou scripts Python, qui peut requièrent pas d’entrées. Ou bien, expérience de hello peut-être être configurée avec un module de lecture qui n’expose pas de n’importe quel GlobalParameters. Dans ce cas, hello AzureMLBatchExecution activité serait configurée comme suit :

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
Hello service web d’exécution par lots d’Azure ML ne dispose ne peut-être pas de sortie de Service Web configuré. Dans cet exemple, aucune entrée ou sortie ni aucun paramètre GlobalParameters n’est configuré. Une sortie configurée sur l’activité hello elle-même est toujours, mais il n’est pas spécifié comme un webServiceOutput.

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

#### <a name="web-service-uses-readers-and-writers-and-hello-activity-runs-only-when-other-activities-have-succeeded"></a>Web Service utilise lecteurs et writers et hello activité s’exécute uniquement lorsque les autres activités ont réussi.
Hello modules Azure ML web service lecteur et writer peuvent être configuré toorun avec ou sans les GlobalParameters. Toutefois, vous souhaiterez peut-être tooembed service appelle dans un pipeline qui utilise le service de jeu de données dépendances tooinvoke hello uniquement lorsqu’un traitement en amont est terminée. Vous pouvez également déclencher d’autres actions après que l’exécution du lot hello est terminée à l’aide de cette approche. Dans ce cas, vous pouvez exprimer des dépendances hello à l’aide d’activité entrées et sorties, sans les nommer un d'entre eux en tant que Service Web entrée ni sortie.

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

Hello **éléments importants à retenir** sont :

* Si le point de terminaison de votre expérience utilise un webServiceInput : il est représenté par un jeu de données d’objet blob et est inclus dans les entrées de l’activité hello et propriété de webServiceInput hello. Sinon, la propriété de webServiceInput hello est omise.
* Si le point de terminaison de votre expérience utilise webServiceOutput(s) : ils sont représentés par des jeux de données objet blob et sont inclus dans les sorties d’activité hello et dans la propriété de webServiceOutputs hello. activité Hello génère et webServiceOutputs sont mappés par nom hello de chaque sortie dans l’expérience de hello. Dans le cas contraire, la propriété de webServiceOutputs hello est omise.
* Si le point de terminaison de votre expérience expose globalParameter(s), ils reçoivent dans la propriété globalParameters de l’activité hello comme la paires clé / valeur. Dans le cas contraire, la propriété de globalParameters hello est omise. les clés Hello respectent la casse. [Fonctions d’Azure Data Factory](data-factory-functions-variables.md) peuvent être utilisées dans les valeurs hello.
* Datasets supplémentaires peuvent figurer dans les propriétés entrées et sorties d’activité hello, sans référencé dans typeProperties d’activité hello. Ces jeux de données régissent l’exécution à l’aide de la tranche dépendances mais est sinon ignorées par hello AzureMLBatchExecution activité.


## <a name="updating-models-using-update-resource-activity"></a>Mise à jour des modèles à l’aide de l’activité des ressources de mise à jour
Une fois que vous avez terminé avec le réapprentissage, mettre à jour hello calculer les scores avec qui vient d’être formé hello le service web (expérience prédictive exposé comme service web) à l’aide de hello **activité de la ressource mise à jour Azure ML**. Consultez l’article [Mise à jour des modèles à l’aide de l’activité des ressources de mise à jour](data-factory-azure-ml-update-resource-activity.md) pour plus d’informations.

### <a name="reader-and-writer-modules"></a>Modules Lecteur et Enregistreur
Un scénario courant pour l’utilisation de paramètres de service Web est utiliser hello enregistreurs et lecteurs de SQL Azure. module de lecture Hello est données tooload utilisé dans une expérience à partir des services de gestion des données en dehors d’Azure Machine Learning Studio. module de writer Hello est toosave les données de vos expériences dans les services de gestion en dehors d’Azure Machine Learning Studio.  

Pour plus d’informations sur les modules enregistreur/lecteur Azure Blob/SQL Azure, voir les rubriques [Lecteur](https://msdn.microsoft.com/library/azure/dn905997.aspx) et [Enregistreur](https://msdn.microsoft.com/library/azure/dn905984.aspx) dans la bibliothèque MSDN. exemple Hello dans la section précédente de hello utilisé la lecture d’objets Blob Azure hello et un writer d’objets Blob Azure. Cette section décrit leur utilisation.

## <a name="frequently-asked-questions"></a>Forum Aux Questions
**Q :** J’ai plusieurs fichiers qui sont générés par mes pipelines Big Data. Puis-je utiliser hello AzureMLBatchExecution activité toowork sur tous les fichiers hello ?

**R :** Oui. Consultez hello **à l’aide d’un lecteur module tooread de données à partir de plusieurs fichiers d’objets Blob Azure** pour plus d’informations.

## <a name="azure-ml-batch-scoring-activity"></a>Activité de notation par lots Azure ML
Si vous utilisez hello **AzureMLBatchScoring** toointegrate d’activité avec Azure Machine Learning, nous vous recommandons d’utiliser hello dernières **AzureMLBatchExecution** activité.

Hello AzureMLBatchExecution activité est introduit dans hello version d’août 2015 de Windows Azure SDK et Azure PowerShell.

Si vous souhaitez toocontinue à l’aide d’activité de AzureMLBatchScoring hello, continuer à lire dans cette section.  

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
toospecify des valeurs pour les paramètres de service Web, ajoutez un **typeProperties** section toohello **AzureMLBatchScoringActivty** section dans le pipeline hello JSON comme indiqué dans hello l’exemple suivant :

```JSON
"typeProperties": {
    "webServiceParameters": {
        "Param 1": "Value 1",
        "Param 2": "Value 2"
    }
}
```
Vous pouvez également utiliser [fonctions de Data Factory](data-factory-functions-variables.md) lors du passage des valeurs hello pour les paramètres de service Web comme indiqué dans hello l’exemple suivant :

```JSON
"typeProperties": {
    "webServiceParameters": {
       "Database query": "$$Text.Format('SELECT * FROM myTable WHERE timeColumn = \\'{0:yyyy-MM-dd HH:mm:ss}\\'', Time.AddHours(WindowStart, 0))"
    }
}
```

> [!NOTE]
> paramètres de service Web Hello respectent la casse, assurez-vous que les noms de hello que vous spécifiez dans l’activité hello JSON correspondent hello ceux qui sont exposées par le service Web de hello.
>
>

## <a name="see-also"></a>Voir aussi
* [Article de blog Azure : prise en main d’Azure Data Factory et d’Azure Machine Learning](https://azure.microsoft.com/blog/getting-started-with-azure-data-factory-and-azure-machine-learning-4/)

[adf-build-1st-pipeline]: data-factory-build-your-first-pipeline.md

[azure-machine-learning]: http://azure.microsoft.com/services/machine-learning/
