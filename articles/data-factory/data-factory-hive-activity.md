---
title: "les données d’aaaTransform à l’aide de la ruche activité - Azure | Documents Microsoft"
description: "Découvrez comment vous pouvez utiliser hello Hive une activité dans un requêtes de données Azure fabrique toorun Hive sur un cluster de HDInsight sur la demande/votre propre."
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 80083218-743e-4da8-bdd2-60d1c77b1227
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: shlo
ms.openlocfilehash: 032400cdb8e8f9873f85b811b4ad7380f4410edf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="transform-data-using-hive-activity-in-azure-data-factory"></a>Transformer des données à l’aide d’une activité Hive dans Azure Data Factory 
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

Hello activité HDInsight Hive dans une fabrique de données [pipeline](data-factory-create-pipelines.md) exécute des requêtes Hive sur [votre propre](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) ou [à la demande](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) cluster HDInsight de basés sur Windows/Linux. Cet article s’appuie sur hello [activités de transformation des données](data-factory-data-transformation-activities.md) article, qui présente une vue d’ensemble de la transformation des données et des activités de transformation hello pris en charge.

> [!NOTE] 
> Si vous êtes tooAzure nouvelle fabrique de données, lisez [Introduction tooAzure Data Factory](data-factory-introduction.md) et hello didacticiel : [générer votre première pipeline de données](data-factory-build-your-first-pipeline.md) avant de lire cet article. 

## <a name="syntax"></a>Syntaxe

```JSON
{
    "name": "Hive Activity",
    "description": "description",
    "type": "HDInsightHive",
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
      "script": "Hive script",
      "scriptPath": "<pathtotheHivescriptfileinAzureblobstorage>",
      "defines": {
        "param1": "param1Value"
      }
    },
   "scheduler": {
      "frequency": "Day",
      "interval": 1
    }
}
```
## <a name="syntax-details"></a>Détails de la syntaxe
| Propriété | Description | Requis |
| --- | --- | --- |
| name |Nom de l’activité hello |Oui |
| description |Texte qui décrit quelle activité hello est utilisé pour |Non |
| type |HDinsightHive |Oui |
| inputs |Entrées consommée par hello activité Hive |Non |
| outputs |Sorties produites par l’activité de ruche hello |Oui |
| linkedServiceName |Cluster HDInsight de référence toohello enregistré comme un service lié dans la fabrique de données |Oui |
| script |Spécifiez le script inline Hive de hello |Non |
| chemin d'accès du script |Hello du magasin Hive script dans un stockage d’objets blob Azure et fournir hello chemin d’accès toohello fichier. Utilisez la propriété ’script’ ou ’scriptPath’. Les deux propriétés ne peuvent pas être utilisées simultanément. nom de fichier Hello respecte la casse. |Non |
| defines |Spécifiez les paramètres en tant que paires clé/valeur pour le référencement dans le script Hive de hello à l’aide de 'hiveconf' |Non |

## <a name="example"></a>Exemple
Prenons l’exemple d’un exemple de jeu consigne analytique où vous souhaitez tooidentify hello temps par les utilisateurs jeux lancée par votre entreprise. 

Bonjour journal suivant est un exemple jeu de journal, qui est la virgule (`,`) séparés et contient hello suivant champs – ID de profil, SessionStart, durée, SrcIPAddress et type de partie.

```
1809,2014-05-04 12:04:25.3470000,14,221.117.223.75,CaptureFlag
1703,2014-05-04 06:05:06.0090000,16,12.49.178.247,KingHill
1703,2014-05-04 10:21:57.3290000,10,199.118.18.179,CaptureFlag
1809,2014-05-04 05:24:22.2100000,23,192.84.66.141,KingHill
.....
```

Hello **script Hive** tooprocess ces données :

```
DROP TABLE IF EXISTS HiveSampleIn; 
CREATE EXTERNAL TABLE HiveSampleIn 
(
    ProfileID        string, 
    SessionStart     string, 
    Duration         int, 
    SrcIPAddress     string, 
    GameType         string
) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION 'wasb://adfwalkthrough@<storageaccount>.blob.core.windows.net/samplein/'; 

DROP TABLE IF EXISTS HiveSampleOut; 
CREATE EXTERNAL TABLE HiveSampleOut 
(    
    ProfileID     string, 
    Duration     int
) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION 'wasb://adfwalkthrough@<storageaccount>.blob.core.windows.net/sampleout/';

INSERT OVERWRITE TABLE HiveSampleOut
Select 
    ProfileID,
    SUM(Duration)
FROM HiveSampleIn Group by ProfileID
```

tooexecute cette ruche de script dans un pipeline de fabrique de données, vous devez suivant de hello toodo

1. Créer un service lié de tooregister [cluster de calcul de votre propre HDInsight](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) ou configurer [cluster de calcul à la demande HDInsight](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service). Appelons ce service lié « HDInsightLinkedService ».
2. Créer un [service lié](data-factory-azure-blob-connector.md) tooconfigure hello connexion tooAzure stockage d’objets Blob qui héberge les données de salutation. Appelons ce service lié « StorageLinkedService ».
3. Créer [datasets](data-factory-create-datasets.md) pointant vers l’entrée de toohello et hello les données de sortie. Nous allons appeler hello dataset d’entrée « HiveSampleIn » et hello dataset de sortie « HiveSampleOut »
4. Copier requête Hive de hello en tant qu’un tooAzure fichier stockage d’objets Blob configuré à l’étape 2 de #. Si le stockage hello pour héberger les données de hello est différent de hello un hébergement de ce fichier de requête, créer un service lié Azure Storage distinct et faire référence tooit dans l’activité hello. Utilisez ** scriptPath ** fichier de requête toohive toospecify hello chemin d’accès et **scriptLinkedService** toospecify hello le stockage Azure qui contient le fichier de script hello. 
   
   > [!NOTE]
   > Vous pouvez également fournir le script inline Hive hello dans la définition d’activité hello à l’aide de hello **script** propriété. Nous déconseillons cette approche que tous les caractères spéciaux dans le script hello dans le document JSON de hello doit toobe séquence d’échappement et peut cause débogage des problèmes. Il est recommandé de Hello est toofollow étape #4.
   > 
   > 
5. Créer un pipeline avec hello HDInsightHive activité. les données de salutation processus/transformations activité Hello.

    ```JSON   
    {   
        "name": "HiveActivitySamplePipeline",
        "properties": {
        "activities": [
            {
                "name": "HiveActivitySample",
                "type": "HDInsightHive",
                "inputs": [
                {
                    "name": "HiveSampleIn"
                }
                ],
                "outputs": [
                {
                    "name": "HiveSampleOut"
                }
                ],
                "linkedServiceName": "HDInsightLinkedService",
                "typeproperties": {
                    "scriptPath": "adfwalkthrough\\scripts\\samplehive.hql",
                    "scriptLinkedService": "StorageLinkedService"
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                }
            }
            ]
        }
    }
    ```
6. Déploiement du pipeline de hello. Consultez l’article [Création de pipelines](data-factory-create-pipelines.md) pour plus de détails. 
7. Surveiller le pipeline hello à l’aide de la surveillance de fabrique de données hello et vues de gestion. Consultez l’article [Surveillance et gestion des pipelines Data Factory](data-factory-monitor-manage-pipelines.md) pour plus d'informations. 

## <a name="specifying-parameters-for-a-hive-script"></a>Spécification des paramètres d’un script Hive
Dans cet exemple, les journaux de jeux sont reçus quotidiennement dans le stockage blob Azure et sont conservés dans un dossier partitionné par date et par heure. Vous voulez tooparameterize hello ruche script et passez emplacement du dossier d’entrée hello dynamiquement pendant l’exécution et également exportent hello partitionnée avec la date et l’heure.

toouse paramétrables script Hive, effectuez l’hello suivant

* Définir les paramètres de hello dans **définit**.

    ```JSON  
    {
        "name": "HiveActivitySamplePipeline",
          "properties": {
        "activities": [
             {
                "name": "HiveActivitySample",
                "type": "HDInsightHive",
                "inputs": [
                      {
                        "name": "HiveSampleIn"
                      }
                ],
                "outputs": [
                      {
                        "name": "HiveSampleOut"
                    }
                ],
                "linkedServiceName": "HDInsightLinkedService",
                "typeproperties": {
                      "scriptPath": "adfwalkthrough\\scripts\\samplehive.hql",
                      "scriptLinkedService": "StorageLinkedService",
                      "defines": {
                        "Input": "$$Text.Format('wasb://adfwalkthrough@<storageaccountname>.blob.core.windows.net/samplein/yearno={0:yyyy}/monthno={0:MM}/dayno={0:dd}/', SliceStart)",
                        "Output": "$$Text.Format('wasb://adfwalkthrough@<storageaccountname>.blob.core.windows.net/sampleout/yearno={0:yyyy}/monthno={0:MM}/dayno={0:dd}/', SliceStart)"
                      },
                       "scheduler": {
                          "frequency": "Hour",
                          "interval": 1
                    }
                }
              }
        ]
      }
    }
    ```
* Bonjour Script Hive, reportez-vous à l’aide du paramètre toohello **${hiveconf : ParameterName}**. 
  
    ```
    DROP TABLE IF EXISTS HiveSampleIn; 
    CREATE EXTERNAL TABLE HiveSampleIn 
    (
        ProfileID     string, 
        SessionStart     string, 
        Duration     int, 
        SrcIPAddress     string, 
        GameType     string
    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:Input}'; 

    DROP TABLE IF EXISTS HiveSampleOut; 
    CREATE EXTERNAL TABLE HiveSampleOut 
    (
        ProfileID     string, 
        Duration     int
    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:Output}';

    INSERT OVERWRITE TABLE HiveSampleOut
    Select 
        ProfileID,
        SUM(Duration)
    FROM HiveSampleIn Group by ProfileID
    ```
## <a name="see-also"></a>Voir aussi
* [Activité pig](data-factory-pig-activity.md)
* [Activité MapReduce](data-factory-map-reduce.md)
* [Activité de diffusion en continu Hadoop](data-factory-hadoop-streaming-activity.md)
* [Appeler des programmes Spark](data-factory-spark.md)
* [Appeler des scripts R](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)

