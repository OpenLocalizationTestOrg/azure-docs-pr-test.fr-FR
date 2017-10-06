---
title: "aaaScheduling et l’exécution avec la fabrique de données | Documents Microsoft"
description: "Apprenez à connaître les aspects de planification et d’exécution du modèle d’application Azure Data Factory."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 088a83df-4d1b-4ac1-afb3-0787a9bd1ca5
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 6114dd4896f5537c789c3b632fb90e501b694285
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="data-factory-scheduling-and-execution"></a>Planification et exécution avec Data Factory
Cet article explique les aspects de planification et l’exécution de hello du modèle d’application hello Azure Data Factory. Cet article suppose que vous avez des notions de base sur les concepts de modèle de données Data Factory, dont l’activité, les pipelines, les services connexes et les groupes de données. Pour les concepts de base d’Azure Data Factory, consultez hello suivant des articles :

* [Introduction tooData usine](data-factory-introduction.md)
* [Pipelines](data-factory-create-pipelines.md)
* [Groupes de données](data-factory-create-datasets.md) 

## <a name="start-and-end-times-of-pipeline"></a>Heures de début et de fin de pipeline
Un pipeline est actif uniquement entre son heure de **début** et son heure de **fin**. Il n’est pas exécutée avant l’heure de début hello ou après l’heure de fin hello. Si le pipeline de hello est suspendu, il n’est pas exécutée indépendamment de son heure de début et de fin. Pour un pipeline toorun, il ne doit pas être suspendu. Vous recherchez ces paramètres (début, fin, en pause) dans la définition de pipeline hello : 

```json
"start": "2017-04-01T08:00:00Z",
"end": "2017-04-01T11:00:00Z"
"isPaused": false
```

Pour plus d’informations sur ces propriétés, consultez l’article [Créer des pipelines](data-factory-create-pipelines.md). 


## <a name="specify-schedule-for-an-activity"></a>Spécifier la planification d’une activité
Il n’est pas pipeline hello qui est exécutée. Il s’agit des activités hello dans le pipeline de hello qui sont exécutées dans hello contexte général du pipeline de hello. Vous pouvez spécifier une planification périodique pour une activité à l’aide de hello **planificateur** section de l’activité JSON. Par exemple, vous pouvez planifier une activité toorun toutes les heures comme suit :  

```json
"scheduler": {
    "frequency": "Hour",
    "interval": 1
},
```

Comme indiqué dans hello suivant schéma, en spécifiant qu'une planification pour une activité crée une série de fenêtres bascules avec Bonjour pipeline début heures et de fin. Les fenêtres récurrentes sont une série d’intervalles de temps fixes contigus, qui ne se chevauchent pas. Ces fenêtres récurrentes logiques pour une activité sont appelées des **fenêtres d’activité**.

![Exemple de planificateur d’activité](media/data-factory-scheduling-and-execution/scheduler-example.png)

Hello **planificateur** propriété pour une activité est facultative. Si vous ne spécifiez pas cette propriété, il doit correspondre au rythme hello que vous spécifiez dans la définition de hello du dataset de sortie pour l’activité de hello. Actuellement, le dataset de sortie est les lecteurs hello planification. Par conséquent, vous devez créer un jeu de données de sortie même si l’activité hello ne produit pas de sortie. 

## <a name="specify-schedule-for-a-dataset"></a>Spécifier la planification d’un jeu de données
Une activité dans un pipeline Data Factory peut inclure zéro ou plusieurs **jeux de données** d’entrée et produire un ou plusieurs jeux de données de sortie. Pour une activité, vous pouvez spécifier la cadence hello à quels hello les données d’entrée sont disponibles ou les données de sortie hello sont générées à l’aide de hello **disponibilité** section dans les définitions de jeu de données hello. 

**Fréquence** Bonjour **disponibilité** section spécifie l’unité de temps hello. Hello valeurs autorisées pour la fréquence sont : Minute, heure, jour, semaine et mois. Hello **intervalle** propriété dans la section disponibilité hello spécifie un multiplicateur de fréquence. Par exemple : si hello frequency tooDay et l’intervalle est défini too1 pour un dataset de sortie, les données de sortie hello produites quotidiennement. Si vous spécifiez la fréquence de hello minute, nous vous recommandons de définir hello intervalle toono inférieur à 15. 

Bonjour l’exemple suivant, les données d’entrée hello sont disponibles toutes les heures et les données de sortie hello sont produites toutes les heures (`"frequency": "Hour", "interval": 1`). 

**Jeu de données d'entrée :** 

```json
{
    "name": "AzureSqlInput",
    "properties": {
        "published": false,
        "type": "AzureSqlTable",
        "linkedServiceName": "AzureSqlLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {}
    }
}
```


**Jeu de données de sortie**

```json
{
    "name": "AzureBlobOutput",
    "properties": {
        "published": false,
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "mypath/{Year}/{Month}/{Day}/{Hour}",
            "format": {
                "type": "TextFormat"
            },
            "partitionedBy": [
                { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
                { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
                { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
                { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "HH" }}
            ]
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

Actuellement, **sortie dataset lecteurs hello planification**. En d’autres termes, planification hello spécifiée pour le jeu de données de sortie hello est toorun utilisé une activité lors de l’exécution. Par conséquent, vous devez créer un jeu de données de sortie même si l’activité hello ne produit pas de sortie. Si l’activité hello n’accepte aucune entrée, vous pouvez ignorer le jeu de données d’entrée création hello. 

Suivant de hello pipeline définition, hello **planificateur** propriété est planification toospecify utilisé pour l’activité de hello. Cette propriété est facultative. Actuellement, planification hello pour l’activité de hello doit correspondre au calendrier hello spécifié pour le jeu de données de sortie hello.
 
```json
{
    "name": "SamplePipeline",
    "properties": {
        "description": "copy activity",
        "activities": [
            {
                "type": "Copy",
                "name": "AzureSQLtoBlob",
                "description": "copy activity",
                "typeProperties": {
                    "source": {
                        "type": "SqlSource",
                        "sqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 100000,
                        "writeBatchTimeout": "00:05:00"
                    }
                },
                "inputs": [
                    {
                        "name": "AzureSQLInput"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobOutput"
                    }
                ],
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                }
            }
        ],
        "start": "2017-04-01T08:00:00Z",
        "end": "2017-04-01T11:00:00Z"
    }
}
```

Dans cet exemple, hello activité exécute toutes les heures entre hello début et de fin des heures de pipeline de hello. les données de sortie Hello sont produites toutes les heures pour windows de trois heures (8 h 00 - 9 AM, 9 : 00 - 10 : 00 et 10 AM - 11 AM). 

Chaque unité de données consommée ou produite pendant l’exécution d’une activité est appelée **tranche de données**. Hello suivant schéma montre un exemple d’une activité avec un jeu de données d’entrée et un jeu de données de sortie : 

![Planificateur de disponibilité](./media/data-factory-scheduling-and-execution/availability-scheduler.png)

diagramme de Hello montre toutes les heures hello hello des tranches de données d’entrée et sortie de jeu de données. diagramme de Hello montre trois tranches d’entrée qui sont prêts pour le traitement. activité de 10 et 11 AM Hello est en cours, production de tranche de sortie de 10-11 AM hello. 

Vous pouvez accéder à intervalle de temps hello associé tranche hello dans le dataset hello JSON à l’aide de variables : [SliceStart](data-factory-functions-variables.md#data-factory-system-variables) et [SliceEnd](data-factory-functions-variables.md#data-factory-system-variables). De même, vous pouvez accéder à intervalle de temps hello associé à une fenêtre d’activité à l’aide de hello WindowStart et WindowEnd. planification Hello d’une activité doit correspondre au calendrier hello du dataset de sortie hello pour l’activité de hello. Par conséquent, hello SliceStart et SliceEnd valeurs sont hello même en tant que valeurs WindowStart et WindowEnd respectivement. Pour plus d’informations sur ces variables, consultez les articles [Variables système et fonctions Data Factory](data-factory-functions-variables.md#data-factory-system-variables).  

Vous pouvez utiliser ces variables à différentes fins dans votre activité JSON. Par exemple, vous pouvez utiliser les données tooselect de jeux de données d’entrée et de sortie qui représente les données de série chronologique (par exemple : 8 AM too9 AM). Cet exemple utilise également **WindowStart** et **WindowEnd** tooselect les données pertinentes pour une activité exécuter et copiez-le blob tooa avec hello approprié **folderPath**. Hello **folderPath** est paramétrable toohave un dossier distinct pour chaque heure.  

Bonjour précédent exemple, planification hello spécifiée pour les jeux de données d’entrée et de sortie est hello même (horaire). Si hello un jeu de données d’entrée pour l’activité de hello est disponible à une fréquence différente, par exemple toutes les 15 minutes, activité hello qui génère ce jeu de données de sortie s’exécute toujours une fois par heure comme dataset de sortie hello est que les lecteurs hello planification d’activité. Pour plus d’informations, consultez [Modélisation des jeux de données avec des fréquences différentes](#model-datasets-with-different-frequencies).

## <a name="dataset-availability-and-policies"></a>Disponibilité et stratégies du jeu de données
Vous avez vu l’utilisation de hello des propriétés de fréquence et l’intervalle dans la section disponibilité hello de définition de dataset. Il existe quelques autres propriétés qui affectent la planification de hello et l’exécution d’une activité. 

### <a name="dataset-availability"></a>Disponibilité du jeu de données 
Hello tableau suivant décrit les propriétés que vous pouvez utiliser Bonjour **disponibilité** section :

| Propriété | Description | Requis | Default |
| --- | --- | --- | --- |
| frequency |Spécifie l’unité de temps hello pour la production de tranche de jeu de données.<br/><br/><b>Fréquence prise en charge</b>: minute, heure, jour, semaine, mois |Oui |N/D |
| interval |Spécifie un multiplicateur de fréquence<br/><br/>« Intervalle de fréquence x » détermine la fréquence à laquelle hello tranche est produite.<br/><br/>Si vous avez besoin de hello toobe dataset découpée sur toutes les heures, vous définissez <b>fréquence</b> trop<b>heure</b>, et <b>intervalle</b> trop<b>1</b>.<br/><br/><b>Remarque</b>: Si vous spécifiez la fréquence de minutes, nous vous recommandons de définir hello intervalle toono inférieur à 15 |Oui |N/D |
| style |Spécifie si la tranche de hello doit être produite au hello début/fin d’intervalle de salutation.<ul><li>StartOfInterval</li><li>EndOfInterval</li></ul><br/><br/>Si tooMonth est définie à la fréquence et le style a la valeur tooEndOfInterval, hello tranche est produite hello dernier jour du mois. Si le style de hello a la valeur tooStartOfInterval, hello tranche est produite hello premier jour du mois.<br/><br/>Si tooDay est définie à la fréquence et le style a la valeur tooEndOfInterval, tranche de hello est produite dans hello dernière heure du jour de hello.<br/><br/>Si tooHour est définie à la fréquence et le style a la valeur tooEndOfInterval, tranche de hello est produite à fin hello d’heure de hello. Par exemple, pour une tranche de période de 13 h 00 à 14 h 00, la tranche de hello est produite à 14 heures. |Non |EndOfInterval |
| anchorDateTime |Définit la position absolue de hello dans le temps utilisé par les limites de la section Planificateur toocompute jeu de données. <br/><br/><b>Remarque</b>: si hello AnchorDateTime comporte des parties de date qui sont plus précis que la fréquence de hello, hello plus granulaires parties sont ignorés. <br/><br/>Par exemple, si hello <b>intervalle</b> est <b>toutes les heures</b> (fréquence : heure et intervalle : 1) et hello <b>AnchorDateTime</b> contient <b>minutes et secondes</b>, puis hello <b>minutes et secondes</b> parties Hello AnchorDateTime sont ignorées. |Non |01/01/0001 |
| Offset |Intervalle de temps par le hello début et fin de toutes les tranches de jeu de données sont déplacées. <br/><br/><b>Remarque</b>: si anchorDateTime et offset sont spécifiés, hello résulte hello combinée MAJ. |Non |N/D |

### <a name="offset-example"></a>exemple offset
Par défaut, les tranches quotidiennes (`"frequency": "Day", "interval": 1`) commencent à 0 h UTC (minuit). Si vous souhaitez hello début toobe 6 h 00 UTC heure au lieu de cela, définissez hello décalage comme indiqué dans hello suivant extrait de code : 

```json
"availability":
{
    "frequency": "Day",
    "interval": 1,
    "offset": "06:00:00"
}
```
### <a name="anchordatetime-example"></a>Exemple anchorDateTime
Dans l’exemple suivant de hello, hello dataset se produit une fois toutes les 23 heures. Hello première tranche commence à heure hello spécifié par anchorDateTime hello, qui est défini trop`2017-04-19T08:00:00` (heure UTC).

```json
"availability":    
{    
    "frequency": "Hour",        
    "interval": 23,    
    "anchorDateTime":"2017-04-19T08:00:00"    
}
```

### <a name="offsetstyle-example"></a>Exemple de décalage/style
Hello dataset suivant est un jeu de données mensuel et 3e de chaque mois à 8 h 00 est produite (`3.08:00:00`) :

```json
"availability": {
    "frequency": "Month",
    "interval": 1,
    "offset": "3.08:00:00", 
    "style": "StartOfInterval"
}
```

### <a name="dataset-policy"></a>Stratégie du jeu de données
Un jeu de données peut avoir une stratégie de validation définie qui spécifie comment les données de salutation générées par l’exécution d’une tranche peuvent être validées avant qu’il soit prêt à être utilisé. Dans ce cas, une fois la tranche de hello a terminé l’exécution, état de la tranche hello sortie est modifié trop**attente** avec un sous-état de **Validation**. Une fois validées, les tranches hello hello tranche devient trop**prêt**. Si une tranche de données a été générée mais n’a pas réussi la validation de hello, les séries de l’activité pour tranches en aval qui dépendent de cette tranche ne sont pas traités. [Surveiller et gérer des pipelines](data-factory-monitor-manage-pipelines.md) couvre hello différents États de tranche de données dans la fabrique de données.

Hello **stratégie** section dans la définition de dataset définit des critères de hello ou condition hello hello tranches de jeu de données doit répondre. Hello tableau suivant décrit les propriétés que vous pouvez utiliser Bonjour **stratégie** section :

| Nom de la stratégie | Description | Appliqué trop| Requis | Default |
| --- | --- | --- | --- | --- |
| minimumSizeMB | Valide les données hello dans un **objets blob Azure** répond aux hello exigences de taille minimale (en mégaoctets). |Objets blob Azure |Non |N/D |
| minimumRows | Valide les données hello dans un **base de données SQL Azure** ou un **table Azure** contient hello le nombre minimal de lignes. |<ul><li>Base de données SQL Azure</li><li>table Azure</li></ul> |Non |N/D |

#### <a name="examples"></a>Exemples
**minimumSizeMB :**

```json
"policy":

{
    "validation":
    {
        "minimumSizeMB": 10.0
    }
}
```

**minimumRows**

```json
"policy":
{
    "validation":
    {
        "minimumRows": 100
    }
}
```

Pour plus d’informations sur ces propriétés et exemples, consultez l’article [Créer des jeux de données](data-factory-create-datasets.md). 

## <a name="activity-policies"></a>Stratégies d’activité
Stratégies affectent le comportement d’exécution hello d’une activité, en particulier lors du traitement de hello une tranche de table. Hello tableau suivant fournit des détails de hello.

| Propriété | Valeurs autorisées | Valeur par défaut | Description |
| --- | --- | --- | --- |
| accès concurrentiel |Entier  <br/><br/>Valeur max : 10 |1 |Nombre d’exécutions simultanées de l’activité hello.<br/><br/>Il détermine le nombre de hello d’exécutions d’activité parallèles qui peuvent se produire sur différentes tranches. Par exemple, si une activité doit toogo via un grand ensemble de données disponibles, une plus grande valeur d’accès concurrentiel accélère le traitement des données hello. |
| executionPriorityOrder |NewestFirst<br/><br/>OldestFirst |OldestFirst |Détermine hello classement de tranches de données qui sont en cours de traitement.<br/><br/>Par exemple, si vous avez 2 segments (l’un se produisant à 16 heures et l’autre à 17 heures) et que les deux sont en attente d’exécution. Si vous définissez hello executionPriorityOrder toobe NewestFirst, tranche hello à 17 h 00 est traitée en premier. Même si vous définissez executionPriorityORder de hello toobe OldestFIrst, tranche hello à 16 h 00 est traité. |
| retry |Entier <br/><br/>La valeur max peut être 10 |0 |Nombre de tentatives avant le traitement des données de la tranche de hello hello est marqué comme défectueux. Exécution de l’activité pour une tranche de données est retentée des toohello spécifié nombre de tentatives. nouvelle tentative de Hello est faite dès que possible après l’échec de hello. |
| timeout |TimeSpan |00:00:00 |Délai d’expiration pour l’activité de hello. Exemple : 00:10:00 (implique un délai d’expiration de 10 minutes)<br/><br/>Si une valeur n’est pas spécifiée ou est égal à 0, hello est infini.<br/><br/>Si le temps de traitement de données hello sur une tranche dépasse la valeur de délai d’attente de hello, elle est annulée et le traitement de hello tooretry tente de système de hello. nombre de Hello de nouvelles tentatives dépend de la propriété de nouvelle tentative hello. En cas de délai d’attente, état de hello a la valeur tooTimedOut. |
| delay |TimeSpan |00:00:00 |Spécifier le délai de hello avant le traitement des données de hello tranche commence.<br/><br/>exécution de Hello d’activité pour une tranche de données est démarrée une fois hello délai passé hello attendu des temps d’exécution.<br/><br/>Exemple : 00:10:00 (implique un délai de 10 minutes) |
| longRetry |Entier <br/><br/>Valeur max : 10 |1 |nombre de Hello de long tentatives avant l’échec de l’exécution de la tranche hello.<br/><br/>Les tentatives longRetry sont espacées par longRetryInterval. Par conséquent, si vous devez toospecify une heure entre chaque tentative, utilisez longRetry. Si les valeurs Retry et longRetry sont spécifiées, chaque tentative longRetry inclut de nouvelles tentatives et le nombre maximal de hello de tentatives est de nouvelle tentative * longRetry.<br/><br/>Par exemple, si nous avons hello suivant les paramètres de stratégie d’activité hello :<br/>Retry : 3<br/>longRetry : 2<br/>longRetryInterval : 01:00:00<br/><br/>Supposons qu’une seule tranche tooexecute (l’état est en attente) et de l’exécution de l’activité hello échoue à chaque fois. Au départ, il y aurait 3 tentatives consécutives d'exécution. Après chaque tentative, état hello de la tranche est Retry. Une fois les 3 premiers tentatives sur, état hello de la tranche est LongRetry.<br/><br/>Après une heure (c’est-à-dire la valeur de longRetryInterval), il y aurait un autre ensemble de 3 tentatives consécutives d’exécution. Après cela, état de la tranche hello est Failed et aucune nouvelle tentative n’a lieu. Par conséquent, 6 tentatives ont été exécutées.<br/><br/>Si toute exécution réussit, état de la tranche hello est prêt et aucune nouvelle tentative n’est tentées.<br/><br/>longRetry peut être utilisé dans les situations où les données dépendantes arrivent à des moments non déterministe ou hello environnement global est instable sous laquelle le traitement de données se produit. Dans ce cas, effectuant une après l’autre les nouvelles tentatives ne permettra pas de, et cela après un intervalle de résultats en temps Bonjour souhaitée de sortie.<br/><br/>Mise en garde : ne définissez pas de valeurs élevées pour longRetry ou longRetryInterval. En règle générale, des valeurs plus élevées impliquent d’autres problèmes systémiques. |
| longRetryInterval |TimeSpan |00:00:00 |délai de Hello entre les nouvelles tentatives longues |

Pour plus d’informations, consultez l’article [Pipelines](data-factory-create-pipelines.md). 

## <a name="parallel-processing-of-data-slices"></a>Traitement en parallèle des tranches de données
Vous pouvez définir la date de début hello pour le pipeline de hello Bonjour passées. Lorsque vous procédez ainsi, Data Factory calcule (remplissages arrière) toutes les tranches de données Bonjour passées et commence à les traiter automatiquement. Par exemple : Si vous créez un pipeline avec la date de début 2017-04-01 et hello date actuelle est 2017-04-10. Si la sortie cadence hello Hello dataset est tous les jours, puis démarre le Data Factory traitement toutes les tranches hello 2017-04-01 too2017-04-09 immédiatement, car la date de début hello est Bonjour passées. tranche Hello depuis 2017-04-10 n'est pas encore traité, car la valeur hello de propriété de style dans la section disponibilité hello est EndOfInterval par défaut. Hello plus ancienne tranche est traitée tout d’abord comme valeur par défaut hello executionPriorityOrder vaut OldestFirst. Pour obtenir une description de la propriété de style hello, consultez [dataset disponibilité](#dataset-availability) section. Pour obtenir une description de la section d’executionPriorityOrder hello, consultez hello [stratégies d’activité](#activity-policies) section. 

Vous pouvez configurer toobe de tranches renvoyées les données traitée en parallèle en définissant un hello **concurrency** propriété Bonjour **stratégie** section de l’activité hello JSON. Cette propriété détermine le nombre de hello d’exécutions d’activité parallèles qui peuvent se produire sur différentes tranches. valeur par défaut de Hello pour la propriété d’accès concurrentiel hello est 1. Une tranche est donc traitée à la fois par défaut. valeur maximale de Hello est 10. Lorsqu’un pipeline doit toogo via un grand ensemble de données disponibles, une valeur concurrency plus importante accélère le traitement des données hello. 

## <a name="rerun-a-failed-data-slice"></a>Réexécuter une tranche de données ayant échoué
Lorsqu’une erreur se produit lors du traitement d’une tranche de données, vous pouvez trouver des Échec du traitement hello d’une tranche à l’aide de panneaux de portail Azure et un moniteur et gérer une application. Pour plus d’informations, consultez [Surveillance et gestion des pipelines à l’aide des panneaux du portail Azure](data-factory-monitor-manage-pipelines.md) ou de [l’application Surveillance et gestion](data-factory-monitor-manage-app.md).

Envisagez de hello exemple qui illustre les deux activités suivant. Activity1 et Activity2. Activity1 consomme une tranche de Dataset1 et produit une tranche de Dataset2, qui est utilisée en tant qu’entrée par Activity2 tooproduce une tranche de hello finale du jeu de données.

![Tranche de données ayant échoué](./media/data-factory-scheduling-and-execution/failed-slice.png)

Hello diagramme montre que, hors trois tranches récentes, il a été un secteur 9 et 10 AM échec production hello pour Dataset2. Fabrique de données suit automatiquement dépendance pour le jeu de données hello temps série. Par conséquent, il ne démarre pas activité hello exécutée de la tranche en aval de hello 9 et 10 du matin.

Outils de surveillance et de gestion de fabrique de données permettent de toodrill dans les journaux de diagnostic hello pour hello tranche ayant échoué tooeasily rechercher hello cause d’origine pour le problème de hello et corrigez-le. Après avoir résolu le problème de hello, vous pouvez facilement démarrer tranche de tooproduce hello Échec d’exécution de l’activité hello. Pour plus d’informations sur la façon de toorerun et comprendre les transitions d’état pour les tranches de données, consultez [analyse et la gestion des pipelines à l’aide de panneaux de portail Azure](data-factory-monitor-manage-pipelines.md) ou [analyse et gestion de l’application](data-factory-monitor-manage-app.md).

Une fois que vous exécutez à nouveau hello 9 et 10 AM découper pour **Dataset2**, Data Factory démarre hello s’exécuter pour la tranche dépendant de hello 9 et 10 du matin sur hello de jeu de données final.

![Réexécuter une tranche de données ayant échoué](./media/data-factory-scheduling-and-execution/rerun-failed-slice.png)

## <a name="multiple-activities-in-a-pipeline"></a>Plusieurs activités à l’intérieur d’un pipeline
Un pipeline peut toutefois contenir plusieurs activités. Si vous avez plusieurs activités dans un pipeline et sortie hello d’une activité n’est pas une entrée d’une autre activité, les activités hello peuvent s’exécuter en parallèle si de tranches de données d’entrée pour les activités de hello sont prêtes.

Vous pouvez chaîner les deux activités (exécutée une activité après l’autre) en définissant le dataset de sortie hello d’une activité hello d’entrée dataset Hello autre activité. activités de Hello peuvent être Bonjour même pipeline ou dans différents pipelines. la deuxième activité Hello s’exécute uniquement lorsque hello tout d’abord un terminé avec succès.

Par exemple, considérez hello suivant les cas où un pipeline a deux activités :

1. L’activité A1 nécessitant le jeu de données d’entrée externe D1 et qui produit le jeu de données de sortie D2.
2. L’activité A2 nécessitant le jeu de données d’entrée D2 et qui produit le jeu de données de sortie D3.

Dans ce scénario, les activités A1 et A2 sont Bonjour même pipeline. activité Hello qu'a1 s’exécute lorsque les données externes hello sont disponibles et la fréquence de disponibilité hello planifiée est atteinte. Hello activité A2 s’exécute lorsque hello planifiées tranches D2 deviennent disponibles et hello fréquence de disponibilité planifiée est atteinte. S’il existe une erreur dans un des tranches hello dans dataset D2, A2 ne fonctionne pas pour ce secteur jusqu'à ce qu’il devienne disponible.

Hello vue de diagramme avec les deux activités Bonjour même pipeline ressemble à hello suivant schéma :

![Chaînage des propriétés des activités Bonjour même pipeline](./media/data-factory-scheduling-and-execution/chaining-one-pipeline.png)

Comme mentionné précédemment, les activités hello peuvent avoir différents pipelines. Dans ce scénario, vue de diagramme hello ressemblerait hello suivant schéma :

![Chaînage des activités dans deux pipelines](./media/data-factory-scheduling-and-execution/chaining-two-pipelines.png)

Consultez hello [copier de manière séquentielle](#copy-sequentially) section annexe hello pour obtenir un exemple.

## <a name="model-datasets-with-different-frequencies"></a>Modélisation des jeux de données avec des fréquences différentes
Dans les exemples de hello, les fréquences de hello pour entrée et de sortie des datasets et hello activité fenêtre de planification ont été hello même. Certains scénarios requièrent la sortie de tooproduce hello possibilité à une fréquence autre que les fréquences hello d’une ou plusieurs entrées. Data factory prend en charge la modélisation de ces scénarios.

### <a name="sample-1-produce-a-daily-output-report-for-input-data-that-is-available-every-hour"></a>Exemple 1 : production d’un rapport de sortie quotidien pour les données d’entrée est disponible toutes les heures
Imaginez un scénario dans lequel nous avons entré des données de mesure à partir de capteurs disponibles toutes les heures dans un stockage Azure Blob. Vous souhaitez tooproduce un rapport quotidien d’agrégation avec des statistiques, telles que la moyenne, maximum et minimum pour jour hello avec [activité hive de Data Factory](data-factory-hive-activity.md).

Voici ce que vous pouvez modéliser ce scénario avec data factory :

**Jeu de données d'entrée**

Hello toutes les heures d’entrée de fichiers sont supprimés dans le dossier hello pour hello donné de jours. La disponibilité de l’entrée est définie sur **Toutes les heures** (fréquence : Heure, intervalle: 1).

```json
{
  "name": "AzureBlobInput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/{Year}/{Month}/{Day}/",
      "partitionedBy": [
        { "name": "Year", "value": {"type": "DateTime","date": "SliceStart","format": "yyyy"}},
        { "name": "Month","value": {"type": "DateTime","date": "SliceStart","format": "MM"}},
        { "name": "Day","value": {"type": "DateTime","date": "SliceStart","format": "dd"}}
      ],
      "format": {
        "type": "TextFormat"
      }
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```
**Jeu de données de sortie**

Un fichier de sortie est créé chaque jour dans le dossier du jour hello. Disponibilité de sortie a pour valeur **Quotidien** (fréquence : jour et intervalle : 1).

```json
{
  "name": "AzureBlobOutput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/{Year}/{Month}/{Day}/",
      "partitionedBy": [
        { "name": "Year", "value": {"type": "DateTime","date": "SliceStart","format": "yyyy"}},
        { "name": "Month","value": {"type": "DateTime","date": "SliceStart","format": "MM"}},
        { "name": "Day","value": {"type": "DateTime","date": "SliceStart","format": "dd"}}
      ],
      "format": {
        "type": "TextFormat"
      }
    },
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```

**Activité : activité Hive dans un pipeline**

script de hive Hello reçoit hello approprié *DateTime* les informations qui utilisent hello **WindowStart** variable comme indiqué dans hello suivant extrait de code. script de hive Hello utilise ces données de hello de variable tooload à partir du dossier hello correct pour le jour de hello et exécutez hello agrégation toogenerate hello sortie.

```json
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2015-01-01T08:00:00",
    "end":"2015-01-01T11:00:00",
    "description":"hive activity",
    "activities": [
        {
            "name": "SampleHiveActivity",
            "inputs": [
                {
                    "name": "AzureBlobInput"
                }
            ],
            "outputs": [
                {
                    "name": "AzureBlobOutput"
                }
            ],
            "linkedServiceName": "HDInsightLinkedService",
            "type": "HDInsightHive",
            "typeProperties": {
                "scriptPath": "adftutorial\\hivequery.hql",
                "scriptLinkedService": "StorageLinkedService",
                "defines": {
                    "Year": "$$Text.Format('{0:yyyy}',WindowStart)",
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

Hello diagramme suivant illustre scénario hello à partir d’un point de vue de dépendances de données.

![Dépendance des données](./media/data-factory-scheduling-and-execution/data-dependency.png)

Hello tranche de sortie pour chaque jour dépend de 24 tranches horaires à partir d’un jeu de données d’entrée. Calcule de fabrique de données ces dépendances automatiquement en déterminant hello tranches de données d’entrée qui se trouvent dans hello même période que hello toobe de tranche de sortie généré. Si une des tranches d’entrée de hello 24 n’est pas disponible, Data Factory attend toobe de tranche d’entrée hello prêt avant de commencer l’exécution d’activité quotidienne hello.

### <a name="sample-2-specify-dependency-with-expressions-and-data-factory-functions"></a>Exemple 2 : spécifier les dépendances avec des expressions et des fonctions Data Factory
Prenons en compte un autre scénario. Supposez que vous avez une activité Hive qui traite deux jeux de données d’entrée. Un d’eux a de nouvelles données tous les jours, mais l’autre obtient de nouvelles données toutes les semaines. Supposons que vous souhaitiez toodo une jointure entre les deux entrées de hello et produire une sortie chaque jour.

approche simple de Hello dans lequel Data Factory automatiquement cherche l’entrée de droite hello tranches tooprocess en alignant sortie toohello temps de la de tranche de données période ne fonctionne pas.

Vous devez spécifier que pour chaque exécution de l’activité, hello Data Factory doit utiliser la tranche de données de la dernière semaine de jeu de données d’entrée hebdomadaires hello. Utilisez les fonctions Azure Data Factory comme Bonjour suivant extrait tooimplement ce comportement.

**Entrée1 : Azure Blob**

Hello première entrée est hello Azure blob mis à jour quotidiennement.

```json
{
  "name": "AzureBlobInputDaily",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/{Year}/{Month}/{Day}/",
      "partitionedBy": [
        { "name": "Year", "value": {"type": "DateTime","date": "SliceStart","format": "yyyy"}},
        { "name": "Month","value": {"type": "DateTime","date": "SliceStart","format": "MM"}},
        { "name": "Day","value": {"type": "DateTime","date": "SliceStart","format": "dd"}}
      ],
      "format": {
        "type": "TextFormat"
      }
    },
    "external": true,
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```

**Entrée2 : objet Blob Azure**

Entrée2 est hello Azure blob mis à jour chaque semaine.

```json
{
  "name": "AzureBlobInputWeekly",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/{Year}/{Month}/{Day}/",
      "partitionedBy": [
        { "name": "Year", "value": {"type": "DateTime","date": "SliceStart","format": "yyyy"}},
        { "name": "Month","value": {"type": "DateTime","date": "SliceStart","format": "MM"}},
        { "name": "Day","value": {"type": "DateTime","date": "SliceStart","format": "dd"}}
      ],
      "format": {
        "type": "TextFormat"
      }
    },
    "external": true,
    "availability": {
      "frequency": "Day",
      "interval": 7
    }
  }
}
```

**Sortie : objet Blob Azure**

Un fichier de sortie est créé chaque jour dans le dossier de hello pour le jour de hello. Disponibilité de la sortie est définie trop**jour** (fréquence : Day, intervalle : 1).

```json
{
  "name": "AzureBlobOutputDaily",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/{Year}/{Month}/{Day}/",
      "partitionedBy": [
        { "name": "Year", "value": {"type": "DateTime","date": "SliceStart","format": "yyyy"}},
        { "name": "Month","value": {"type": "DateTime","date": "SliceStart","format": "MM"}},
        { "name": "Day","value": {"type": "DateTime","date": "SliceStart","format": "dd"}}
      ],
      "format": {
        "type": "TextFormat"
      }
    },
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```

**Activité : activité Hive dans un pipeline**

activité de ruche Hello prend hello deux entrées et produit une tranche de sortie chaque jour. Vous pouvez spécifier toodepend de tranche de sortie de tous les jours sur hello tranche d’entrée de la semaine précédente pour l’entrée hebdomadaire comme suit.

```json
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2015-01-01T08:00:00",
    "end":"2015-01-01T11:00:00",
    "description":"hive activity",
    "activities": [
      {
        "name": "SampleHiveActivity",
        "inputs": [
          {
            "name": "AzureBlobInputDaily"
          },
          {
            "name": "AzureBlobInputWeekly",
            "startTime": "Date.AddDays(SliceStart, - Date.DayOfWeek(SliceStart))",
            "endTime": "Date.AddDays(SliceEnd,  -Date.DayOfWeek(SliceEnd))"  
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutputDaily"
          }
        ],
        "linkedServiceName": "HDInsightLinkedService",
        "type": "HDInsightHive",
        "typeProperties": {
          "scriptPath": "adftutorial\\hivequery.hql",
          "scriptLinkedService": "StorageLinkedService",
          "defines": {
            "Year": "$$Text.Format('{0:yyyy}',WindowStart)",
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

Pour obtenir la liste des fonctions et variables système prises en charge par Azure Data Factory, consultez [Variables système et fonctions Data Factory](data-factory-functions-variables.md) .

## <a name="appendix"></a>Annexe

### <a name="example-copy-sequentially"></a>Exemple : Copier de manière séquentielle
Il est possible de toorun plusieurs opérations de copie une après l’autre de manière séquentielle/classés. Par exemple, vous pouvez avoir deux datasets de sortie de données copie les activités dans un pipeline (CopyActivity1 et CopyActivity2) avec hello suivant d’entrée :   

Activitédecopie1

Jeu de données d'entrée. Sortie : Dataset2.

Activitédecopie2

Entrée : Jeudedonnées2.  Sortie : Jeudedonnées3.

CopyActivity2 s’exécute uniquement si hello CopyActivity1 a exécuté avec succès et Dataset2 est disponible.

Voici le code JSON de pipeline exemple hello :

```json
{
    "name": "ChainActivities",
    "properties": {
        "description": "Run activities in sequence",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "copyBehavior": "PreserveHierarchy",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "Dataset1"
                    }
                ],
                "outputs": [
                    {
                        "name": "Dataset2"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00"
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "CopyFromBlob1ToBlob2",
                "description": "Copy data from a blob tooanother"
            },
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "Dataset2"
                    }
                ],
                "outputs": [
                    {
                        "name": "Dataset3"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00"
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "CopyFromBlob2ToBlob3",
                "description": "Copy data from a blob tooanother"
            }
        ],
        "start": "2016-08-25T01:00:00Z",
        "end": "2016-08-25T01:00:00Z",
        "isPaused": false
    }
}
```

Notez que dans l’exemple de hello, le dataset de sortie hello Hello première activité de copie (Dataset2) est spécifié en tant qu’entrée pour la deuxième activité hello. Par conséquent, hello deuxième activité s’exécute uniquement lorsque le dataset de sortie hello à partir de la première activité hello est prêt.  

Dans l’exemple de hello, CopyActivity2 peut avoir une entrée différents, tels que Dataset3, mais vous spécifiez Dataset2 comme une tooCopyActivity2 d’entrée, afin de l’activité hello ne s’exécute pas avant la fin de CopyActivity1. Par exemple :

Activitédecopie1

Entrée : Jeudedonnées1. Sortie : Dataset2.

Activitédecopie2

Entrées : Jeudedonnées3, Jeudedonnées2. Sortie : Jeudedonnées4.

```json
{
    "name": "ChainActivities",
    "properties": {
        "description": "Run activities in sequence",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "copyBehavior": "PreserveHierarchy",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "Dataset1"
                    }
                ],
                "outputs": [
                    {
                        "name": "Dataset2"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00"
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "CopyFromBlobToBlob",
                "description": "Copy data from a blob tooanother"
            },
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "Dataset3"
                    },
                    {
                        "name": "Dataset2"
                    }
                ],
                "outputs": [
                    {
                        "name": "Dataset4"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00"
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "CopyFromBlob3ToBlob4",
                "description": "Copy data from a blob tooanother"
            }
        ],
        "start": "2017-04-25T01:00:00Z",
        "end": "2017-04-25T01:00:00Z",
        "isPaused": false
    }
}
```

Notez que dans l’exemple de hello, deux jeux de données d’entrée est spécifiés pour la deuxième activité de copie hello. Lorsque plusieurs entrées sont spécifiées, uniquement hello première entrée jeu de données est utilisé pour copier des données, mais les autres jeux de données est utilisés en tant que dépendances. CopyActivity2 démarre uniquement une fois hello conditions suivantes sont remplies :

* ActivitédeCopie1 s’est terminée avec succès et JeudeDonnées2 est disponible. Ce jeu de données n’est pas utilisé lors de la copie des données tooDataset4. Il sert uniquement de dépendance de planification pour ActivitédeCopie2.   
* JeudeDonnées3 est disponible. Ce jeu de données représente des données hello sont copié toohello destination. 
