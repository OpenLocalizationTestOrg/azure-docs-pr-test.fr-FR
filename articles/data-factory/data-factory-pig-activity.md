---
title: "les données d’aaaTransform à l’aide d’activité Pig dans Azure Data Factory | Documents Microsoft"
description: "Découvrez comment vous pouvez utiliser hello activité Pig dans un script de données Azure fabrique toorun Pig sur un cluster de HDInsight sur la demande/votre propre."
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 5af07a1a-2087-455e-a67b-a79841b4ada5
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: shlo
ms.openlocfilehash: 3ad096c4a9e8603b09f574f6d129b4339a75d381
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="transform-data-using-pig-activity-in-azure-data-factory"></a>Transformer des données à l’aide d’une activité Pig dans Azure Data Factory
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

Hello activité HDInsight Pig dans une fabrique de données [pipeline](data-factory-create-pipelines.md) exécute des requêtes de Pig sur [votre propre](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) ou [à la demande](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) cluster HDInsight de basés sur Windows/Linux. Cet article s’appuie sur hello [activités de transformation des données](data-factory-data-transformation-activities.md) article, qui présente une vue d’ensemble de la transformation des données et des activités de transformation hello pris en charge.

> [!NOTE] 
> Si vous êtes tooAzure nouvelle fabrique de données, lisez [Introduction tooAzure Data Factory](data-factory-introduction.md) et hello didacticiel : [générer votre première pipeline de données](data-factory-build-your-first-pipeline.md) avant de lire cet article. 

## <a name="syntax"></a>Syntaxe

```JSON
{
    "name": "HiveActivitySamplePipeline",
      "properties": {
    "activities": [
        {
            "name": "Pig Activity",
            "description": "description",
            "type": "HDInsightPig",
            "inputs": [
                  {
                    "name": "input tables"
                  }
            ],
            "outputs": [
                  {
                    "name": "output tables"
                  }
            ],
            "linkedServiceName": "MyHDInsightLinkedService",
            "typeProperties": {
                  "script": "Pig script",
                  "scriptPath": "<pathtothePigscriptfileinAzureblobstorage>",
                  "defines": {
                    "param1": "param1Value"
                  }
            },
               "scheduler": {
                  "frequency": "Day",
                  "interval": 1
            }
          }
    ]
  }
}
```
## <a name="syntax-details"></a>Détails de la syntaxe
| Propriété | Description | Requis |
| --- | --- | --- |
| name |Nom de l’activité hello |Oui |
| description |Texte qui décrit quelle activité hello est utilisé pour |Non |
| type |HDinsightPig |Oui |
| inputs |Une ou plusieurs entrées consommée par hello activité Pig |Non |
| outputs |Une ou plusieurs sorties produites par hello activité Pig |Oui |
| linkedServiceName |Cluster HDInsight de référence toohello enregistré comme un service lié dans la fabrique de données |Oui |
| script |Spécifiez hello Pig script inline |Non |
| chemin d'accès du script |Stocker le script Pig hello dans un stockage d’objets blob Azure et fournir hello chemin d’accès toohello fichier. Utilisez la propriété ’script’ ou ’scriptPath’. Les deux propriétés ne peuvent pas être utilisées simultanément. nom de fichier Hello respecte la casse. |Non |
| defines |Spécifiez les paramètres en tant que paires clé/valeur pour le référencement dans hello script Pig |Non |

## <a name="example"></a>Exemple
Prenons l’exemple d’un exemple de jeu consigne analytique où vous souhaitez tooidentify hello temps de lecteurs jeux lancée par votre entreprise.

Hello suivant l’exemple de journal jeu est un fichier de séparés par des virgules (,). Il contient hello suivant champs – ID de profil, SessionStart, durée, SrcIPAddress et type de partie.

```
1809,2014-05-04 12:04:25.3470000,14,221.117.223.75,CaptureFlag
1703,2014-05-04 06:05:06.0090000,16,12.49.178.247,KingHill
1703,2014-05-04 10:21:57.3290000,10,199.118.18.179,CaptureFlag
1809,2014-05-04 05:24:22.2100000,23,192.84.66.141,KingHill
.....
```

Hello **porc script** tooprocess ces données :

```
PigSampleIn = LOAD 'wasb://adfwalkthrough@anandsub14.blob.core.windows.net/samplein/' USING PigStorage(',') AS (ProfileID:chararray, SessionStart:chararray, Duration:int, SrcIPAddress:chararray, GameType:chararray);

GroupProfile = Group PigSampleIn all;

PigSampleOut = Foreach GroupProfile Generate PigSampleIn.ProfileID, SUM(PigSampleIn.Duration);

Store PigSampleOut into 'wasb://adfwalkthrough@anandsub14.blob.core.windows.net/sampleoutpig/' USING PigStorage (',');
```

tooexecute cette Pig de script dans un pipeline de la fabrique de données, procédez comme hello comme suit :

1. Créer un service lié de tooregister [cluster de calcul de votre propre HDInsight](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) ou configurer [cluster de calcul à la demande HDInsight](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service). Appelons ce service lié **HDInsightLinkedService**.
2. Créer un [service lié](data-factory-azure-blob-connector.md) tooconfigure hello connexion tooAzure stockage d’objets Blob qui héberge les données de salutation. Appelons ce service lié **StorageLinkedService**.
3. Créer [datasets](data-factory-create-datasets.md) pointant vers l’entrée de toohello et hello les données de sortie. Jeu de données d’entrée hello, nous allons appeler **PigSampleIn** et hello dataset de sortie **PigSampleOut**.
4. Copier requête Pig de hello dans un stockage d’objets Blob Azure configuré à l’étape 2 de # de hello fichier. Si hello le stockage Azure qui héberge les données de salutation est différent de hello une qui héberge un fichier de requête hello, créez un service lié Azure Storage distinct. Voir la rubrique service toohello lié dans la configuration d’activité hello. Utilisez ** scriptPath ** le fichier script toopig toospecify hello chemin d’accès et **scriptLinkedService**. 
   
   > [!NOTE]
   > Vous pouvez également fournir hello Pig script inline dans la définition d’activité hello à l’aide de hello **script** propriété. Toutefois, nous déconseillons cette approche en tant que tous les caractères spéciaux dans le script de hello doit toobe séquence d’échappement et peut provoquer des problèmes de débogage. Il est recommandé de Hello est toofollow étape #4.
   > 
   > 
5. Créer le pipeline de hello avec hello HDInsightPig activité. Cette activité traite les données d’entrée hello en exécutant le script Pig sur un cluster HDInsight.

    ```JSON   
    {
      "name": "PigActivitySamplePipeline",
      "properties": {
        "activities": [
          {
            "name": "PigActivitySample",
            "type": "HDInsightPig",
            "inputs": [
              {
                "name": "PigSampleIn"
              }
            ],
            "outputs": [
              {
                "name": "PigSampleOut"
              }
            ],
            "linkedServiceName": "HDInsightLinkedService",
            "typeproperties": {
              "scriptPath": "adfwalkthrough\\scripts\\enrichlogs.pig",
              "scriptLinkedService": "StorageLinkedService"
            },
               "scheduler": {
                  "frequency": "Day",
                  "interval": 1
            }
          }
        ]
      }
    } 
    ```
6. Déploiement du pipeline de hello. Consultez l’article [Création de pipelines](data-factory-create-pipelines.md) pour plus de détails. 
7. Surveiller le pipeline hello à l’aide de la surveillance de fabrique de données hello et vues de gestion. Consultez l’article [Surveillance et gestion des pipelines Data Factory](data-factory-monitor-manage-pipelines.md) pour plus d'informations.

## <a name="specifying-parameters-for-a-pig-script"></a>Spécification des paramètres d’un script Pig
Envisagez de hello l’exemple suivant : journaux de jeu sont ingérés tous les jours dans le stockage d’objets Blob Azure et stockés dans un dossier date selon partitionnée et l’heure. Vous souhaitez que le script Pig tooparameterize hello et passez emplacement du dossier d’entrée hello dynamiquement pendant l’exécution et également exportent hello partitionnée avec la date et l’heure.

toouse paramétrables script Pig, procédez comme hello suivant :

* Définir les paramètres de hello dans **définit**.

    ```JSON  
    {
        "name": "PigActivitySamplePipeline",
          "properties": {
        "activities": [
            {
                "name": "PigActivitySample",
                "type": "HDInsightPig",
                "inputs": [
                      {
                        "name": "PigSampleIn"
                      }
                ],
                "outputs": [
                      {
                        "name": "PigSampleOut"
                      }
                ],
                "linkedServiceName": "HDInsightLinkedService",
                "typeproperties": {
                      "scriptPath": "adfwalkthrough\\scripts\\samplepig.hql",
                      "scriptLinkedService": "StorageLinkedService",
                      "defines": {
                        "Input": "$$Text.Format('wasb: //adfwalkthrough@<storageaccountname>.blob.core.windows.net/samplein/yearno={0: yyyy}/monthno={0:MM}/dayno={0: dd}/',SliceStart)",
                        "Output": "$$Text.Format('wasb://adfwalkthrough@<storageaccountname>.blob.core.windows.net/sampleout/yearno={0:yyyy}/monthno={0:MM}/dayno={0:dd}/', SliceStart)"
                      }
                },
                   "scheduler": {
                      "frequency": "Day",
                      "interval": 1
                }
              }
        ]
      }
    }
    ```  
* Bonjour Script Pig, font référence à l’aide des paramètres de toohello '**$parameterName**' comme indiqué dans hello l’exemple suivant :

    ```  
    PigSampleIn = LOAD '$Input' USING PigStorage(',') AS (ProfileID:chararray, SessionStart:chararray, Duration:int, SrcIPAddress:chararray, GameType:chararray);    
    GroupProfile = Group PigSampleIn all;        
    PigSampleOut = Foreach GroupProfile Generate PigSampleIn.ProfileID, SUM(PigSampleIn.Duration);        
    Store PigSampleOut into '$Output' USING PigStorage (','); 
    ```
## <a name="see-also"></a>Voir aussi
* [Activité Hive](data-factory-hive-activity.md)
* [Activité MapReduce](data-factory-map-reduce.md)
* [Activité de diffusion en continu Hadoop](data-factory-hadoop-streaming-activity.md)
* [Appeler des programmes Spark](data-factory-spark.md)
* [Appeler des scripts R](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)

