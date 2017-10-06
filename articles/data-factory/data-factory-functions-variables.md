---
title: "aaaData fabrique de fonctions et Variables système | Documents Microsoft"
description: "Fournit la liste des variables système et fonctions Azure Data Factory"
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
services: data-factory
ms.assetid: b6b3c2ae-b0e8-4e28-90d8-daf20421660d
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: shlo
ms.openlocfilehash: d2936c2821797947bb37d9775226a6c19c4b8ab9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-factory---functions-and-system-variables"></a>Azure Data Factory - Variables système et fonctions
Cet article fournit des informations sur les fonctions et variables prises en charge par Azure Data Factory.

## <a name="data-factory-system-variables"></a>Variables système Data Factory
| Nom de la variable | Description | Portée de l’objet | Étendue JSON et cas d’utilisation |
| --- | --- | --- | --- |
| WindowStart |Début de l’intervalle de temps pour l’intervalle d’exécution d’activité en cours |activité |<ol><li>Spécifier des requêtes de sélection de données. Consultez les articles de connecteur référencés dans hello [les activités de déplacement des données](data-factory-data-movement-activities.md) l’article.</li> |
| WindowEnd |Fin de l’intervalle de temps de l’intervalle d’exécution d’activité en cours |activité |identique à WindowStart. |
| SliceStart |Début de l’intervalle de temps pour une tranche de données en cours de génération |activité<br/>jeu de données |<ol><li>Spécifier les chemins d’accès et les noms de fichiers dynamiques tout en travaillant avec [Blob Azure](data-factory-azure-blob-connector.md) et [Jeux de données du système de fichiers](data-factory-onprem-file-system-connector.md).</li><li>Spécifier les dépendances d’entrée avec les fonctions Data Factory dans la collecte d’activité.</li></ol> |
| SliceEnd |Fin de l’intervalle de temps pour la tranche de données en cours. |activité<br/>dataset |identique à SliceStart. |

> [!NOTE]
> Actuellement la fabrique de données requiert que hello planifier hello spécifié dans activité correspond exactement à planification hello spécifiée dans la disponibilité du jeu de données de sortie hello. Par conséquent, WindowStart, WindowEnd et SliceStart et SliceEnd toujours mappent toohello même moment période et une tranche de sortie unique.
> 

### <a name="example-for-using-a-system-variable"></a>Exemple d’utilisation d’une variable système
Bonjour suivant l’exemple, année, mois, jour et l’heure de **SliceStart** sont extraits dans des variables distinctes qui sont utilisés par **folderPath** et **nom de fichier** propriétés.

```json
"folderPath": "wikidatagateway/wikisampledataout/{Year}/{Month}/{Day}",
"fileName": "{Hour}.csv",
"partitionedBy":
 [
    { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
    { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
    { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
    { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "hh" } }
],
```

## <a name="data-factory-functions"></a>Fonctions Data Factory
Vous pouvez utiliser des fonctions dans la fabrique de données, ainsi que des variables système pour hello suite à des fins :

1. Spécification de requêtes de sélection de données (voir les articles de connecteur référencés par hello [les activités de déplacement des données](data-factory-data-movement-activities.md) l’article.
   
   Hello tooinvoke syntaxe une fonction de fabrique de données est :  **$$ <function>**  pour les requêtes de sélection de données et d’autres propriétés dans l’activité hello et jeux de données.  
2. Spécifier les dépendances d’entrée avec les fonctions Data Factory dans la collecte d’entrées d’activité.
   
    $$ n’est pas nécessaire pour spécifier des expressions de dépendance d’entrée.     

Bonjour suivant l’exemple, **sqlReaderQuery** dans un fichier JSON est affectée à tooa retourné par hello `Text.Format` (fonction). Cet exemple utilise également une variable système nommée **WindowStart**, qui représente l’heure de début de hello de fenêtre d’exécution de l’activité hello.

```json
{
    "Type": "SqlSource",
    "sqlReaderQuery": "$$Text.Format('SELECT * FROM MyTable WHERE StartTime = \\'{0:yyyyMMdd-HH}\\'', WindowStart)"
}
```

Consultez la rubrique [Chaînes de format de date et d’heure personnalisées](https://msdn.microsoft.com/library/8kb3ddd4.aspx) , qui décrit les différentes options de formatage que vous pouvez utiliser (par exemple : aa et aaaa). 

### <a name="functions"></a>Fonctions
Hello les tableaux suivants répertorie toutes les fonctions hello dans Azure Data Factory :

| Catégorie | Fonction | Paramètres | Description |
| --- | --- | --- | --- |
| Time |AddHours(X,Y) |X: DateTime  <br/><br/>Y: int |Ajoute Y heures toohello est heure X. <br/><br/>Exemple : `9/5/2013 12:00:00 PM + 2 hours = 9/5/2013 2:00:00 PM` |
| Temps |AddMinutes(X,Y) |X: DateTime  <br/><br/>Y: int |Ajoute Y minutes tooX.<br/><br/>Exemple : `9/15/2013 12: 00:00 PM + 15 minutes = 9/15/2013 12: 15:00 PM` |
| Temps |StartOfHour(X) |X: DateTime  |Obtient hello heure de début de heure hello représenté par le composant « heure » hello de X. <br/><br/>Exemple : `StartOfHour of 9/15/2013 05: 10:23 PM is 9/15/2013 05: 00:00 PM` |
| Date |AddDays(X,Y) |X: DateTime <br/><br/>Y: int |Ajoute Y jours tooX. <br/><br/>Exemple : 9/15/2013 12:00:00 PM + 2 jours = 9/17/2013 12:00:00 PM.<br/><br/>Vous pouvez également soustraire les jours en spécifiant Y en tant que nombre négatif.<br/><br/>Exemple : `9/15/2013 12:00:00 PM - 2 days = 9/13/2013 12:00:00 PM`. |
| Date |AddMonths(X,Y) |X: DateTime <br/><br/>Y: int |Ajoute Y mois tooX.<br/><br/>`Example: 9/15/2013 12:00:00 PM + 1 month = 10/15/2013 12:00:00 PM`.<br/><br/>Vous pouvez également soustraire les mois en spécifiant Y en tant que nombre négatif.<br/><br/>Exemple : `9/15/2013 12:00:00 PM - 1 month = 8/15/2013 12:00:00 PM`.|
| Date |AddQuarters(X,Y) |X: DateTime  <br/><br/>Y: int |Ajoute Y * 3 mois tooX.<br/><br/>Exemple : `9/15/2013 12:00:00 PM + 1 quarter = 12/15/2013 12:00:00 PM` |
| Date |AddWeeks(X,Y) |X: DateTime <br/><br/>Y: int |Ajoute Y * 7 jours tooX<br/><br/>Exemple : 15/9/2013 12:00:00 PM + 1 semaine = 22/9/2013 12:00:00 PM<br/><br/>Vous pouvez également soustraire les semaines en spécifiant Y en tant que nombre négatif.<br/><br/>Exemple : `9/15/2013 12:00:00 PM - 1 week = 9/7/2013 12:00:00 PM`. |
| Date |AddYears(X,Y) |X: DateTime <br/><br/>Y: int |Ajoute Y années tooX.<br/><br/>`Example: 9/15/2013 12:00:00 PM + 1 year = 9/15/2014 12:00:00 PM`<br/><br/>Vous pouvez également soustraire les années en spécifiant Y en tant que nombre négatif.<br/><br/>Exemple : `9/15/2013 12:00:00 PM - 1 year = 9/15/2012 12:00:00 PM`. |
| Date |Day(X) |X: DateTime  |Obtient le composant « jour » hello de X.<br/><br/>Exemple : `Day of 9/15/2013 12:00:00 PM is 9`. |
| Date |DayOfWeek(X) |X: DateTime  |Obtient le jour hello de composant semaine de X.<br/><br/>Exemple : `DayOfWeek of 9/15/2013 12:00:00 PM is Sunday`. |
| Date |DayOfYear(X) |X: DateTime  |Obtient le jour hello année hello représenté par le composant « année » hello de X.<br/><br/>Exemples :<br/>`12/1/2015: day 335 of 2015`<br/>`12/31/2015: day 365 of 2015`<br/>`12/31/2016: day 366 of 2016 (Leap Year)` |
| Date |DaysInMonth(X) |X: DateTime  |Obtient les jours hello mois hello représenté par le composant de mois hello du paramètre X.<br/><br/>Exemple : `DaysInMonth of 9/15/2013 are 30 since there are 30 days in hello September month`. |
| Date |EndOfDay(X) |X: DateTime  |Obtient la date-heure hello qui représente la fin de hello du jour hello (composant day) de X.<br/><br/>Exemple : `EndOfDay of 9/15/2013 05:10:23 PM is 9/15/2013 11:59:59 PM`. |
| Date |EndOfMonth(X) |X: DateTime  |Obtient la fin de hello du mois de hello représenté par le composant month du paramètre X. <br/><br/>Exemple : `EndOfMonth of 9/15/2013 05:10:23 PM is 9/30/2013 11:59:59 PM` (date représentant une fin hello du mois de septembre) |
| Date |StartOfDay(X) |X: DateTime  |Obtient le début hello du jour hello représenté par le composant de jour hello du paramètre X.<br/><br/>Exemple : `StartOfDay of 9/15/2013 05:10:23 PM is 9/15/2013 12:00:00 AM`. |
| DateTime |From(X) |X: String |Analyser la chaîne X tooa date heure. |
| DateTime |Ticks(X) |X: DateTime  |Obtient les graduations hello propriété de paramètre de hello X. Un cycle est égal à 100 nanosecondes. valeur Hello de cette propriété représente le nombre de hello de graduations qui se sont écoulées depuis 12:00:00 minuit, le 1er janvier 0001. |
| Texte |Format(X) |X : variable de chaîne |Formats hello texte (utilisez `\\'` combinaison tooescape `'` caractères).|

> [!IMPORTANT]
> Lorsque vous utilisez une fonction dans une autre fonction, vous n’avez pas besoin de toouse  **$$**  préfixe de fonction interne de hello. Par exemple : $$Text.Format('PartitionKey eq \\'my_pkey_filter_value\\' et RowKey ge \\'{0: yyyy-MM-dd HH:mm:ss}\\'', Time.AddHours(SliceStart, -6)). Dans cet exemple, notez que  **$$**  préfixe n’est pas utilisé pour hello **Time.AddHours** (fonction). 

#### <a name="example"></a>Exemple
Bonjour, des paramètres d’exemple, les entrées et sorties suivants pour l’activité de ruche hello sont déterminées à l’aide de hello `Text.Format` fonction et la variable SliceStart du système. 

```json  
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

### <a name="example-2"></a>Exemple 2

Bonjour l’exemple suivant, le paramètre DateTime hello hello activité de procédure stockée est déterminée à l’aide de hello texte. Formatage de la fonction et hello SliceStart variable. 

```json
{
    "name": "SprocActivitySamplePipeline",
    "properties": {
        "activities": [
            {
                "type": "SqlServerStoredProcedure",
                "typeProperties": {
                    "storedProcedureName": "sp_sample",
                    "storedProcedureParameters": {
                        "DateTime": "$$Text.Format('{0:yyyy-MM-dd HH:mm:ss}', SliceStart)"
                    }
                },
                "outputs": [
                    {
                        "name": "sprocsampleout"
                    }
                ],
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "SprocActivitySample"
            }
        ],
            "start": "2016-08-02T00:00:00Z",
            "end": "2016-08-02T05:00:00Z",
        "isPaused": false
    }
}
```

### <a name="example-3"></a>Exemple 3
tooread des données à partir de la journée précédente au lieu de jours représenté par hello SliceStart, utilisez la fonction AddDays de hello comme indiqué dans hello l’exemple suivant : 

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-01-01T08:00:00",
        "end": "2017-01-01T11:00:00",
        "description": "hive activity",
        "activities": [
            {
                "name": "SampleHiveActivity",
                "inputs": [
                    {
                        "name": "MyAzureBlobInput",
                        "startTime": "Date.AddDays(SliceStart, -1)",
                        "endTime": "Date.AddDays(SliceEnd, -1)"
                    }
                ],
                "outputs": [
                    {
                        "name": "MyAzureBlobOutput"
                    }
                ],
                "linkedServiceName": "HDInsightLinkedService",
                "type": "HDInsightHive",
                "typeProperties": {
                    "scriptPath": "adftutorial\\hivequery.hql",
                    "scriptLinkedService": "StorageLinkedService",
                    "defines": {
                        "Year": "$$Text.Format('{0:yyyy}',WindowsStart)",
                        "Month": "$$Text.Format('{0:MM}',WindowStart)",
                        "Day": "$$Text.Format('{0:dd}',WindowStart)"
                    }
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "policy": {
                    "concurrency": 1,
                    "executionPriorityOrder": "OldestFirst",
                    "retry": 2,
                    "timeout": "01:00:00"
                }
            }
        ]
    }
}
```

Consultez la rubrique [Chaînes de format de date et d’heure personnalisées](https://msdn.microsoft.com/library/8kb3ddd4.aspx) , qui décrit les différentes options de formatage que vous pouvez utiliser (par exemple : aa et aaaa). 

