---
title: "aaaAzure Data Factory - référence des scripts JSON | Documents Microsoft"
description: "Fournit des schémas JSON pour les entités Data Factory."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: 
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 813fd752bb0ecb1b513d022b9f302325105dac31
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-factory---json-scripting-reference"></a>Azure Data Factory - Référence de script JSON
Cet article fournit des schémas JSON et des exemples pour la définition des entités Azure Data Factory (pipeline, activité, jeu de données et service lié).  

## <a name="pipeline"></a>Pipeline 
structure de haut niveau Hello pour une définition de pipeline est la suivante : 

```json
{
  "name": "SamplePipeline",
  "properties": {
    "description": "Describe what pipeline does",
    "activities": [
    ],
    "start": "2016-07-12T00:00:00",
    "end": "2016-07-13T00:00:00"
  }
} 
```

Tableau suivant décrit les propriétés de hello au sein de la définition JSON du pipeline hello :

| Propriété | Description | Requis
-------- | ----------- | --------
| name | Nom du pipeline de hello. Spécifiez un nom qui représente l’action hello hello activité ou le pipeline est configuré toodo<br/><ul><li>Nombre maximal de caractères : 260</li><li>Doit commencer par une lettre, un chiffre ou un trait de soulignement (_)</li><li>Les caractères suivants ne sont pas autorisés : « . », « + », « ? », « / », « < », « > », « * », « % », « & », « : », « \\ »</li></ul> |Oui |
| description |Texte décrivant les activité hello ou un pipeline est utilisé pour | Non |
| activités | Contient une liste d’activités. | Oui |
| start |Date-heure de début pour le pipeline de hello. Doit se trouver au [format ISO](http://en.wikipedia.org/wiki/ISO_8601). Par exemple : 2014-10-14T16:32:41. <br/><br/>Il est possible de toospecify une heure locale, par exemple une heure EST. Voici un exemple : `2016-02-27T06:00:00**-05:00`, qui correspond à 6h EST.<br/><br/>Hello propriétés start et end spécifient ensemble la période active pour le pipeline de hello. Les tranches de sortie sont uniquement générées pendant cette période active. |Non<br/><br/>Si vous spécifiez une valeur pour la propriété de fin hello, vous devez spécifier la valeur de propriété de début hello.<br/><br/>Hello heures de début et de fin peuvent tous deux être vide toocreate un pipeline. Vous devez spécifier les deux valeurs tooset une période active pour hello pipeline toorun. Si vous ne spécifiez pas les heures de début et de fin lors de la création d’un pipeline, vous pouvez les définir à l’aide d’applet de commande hello ensemble-AzureRmDataFactoryPipelineActivePeriod plus tard. |
| end |Date-heure de fin pour le pipeline de hello. Si spécifiée, doit être au format ISO. Par exemple : 2014-10-14T17:32:41 <br/><br/>Il est possible de toospecify une heure locale, par exemple une heure EST. Voici un exemple : `2016-02-27T06:00:00**-05:00`, qui correspond à 6h EST.<br/><br/>pipeline de hello toorun spécifiez indéfiniment, 9999-09-09 en tant que valeur hello pour la propriété de fin hello. |Non <br/><br/>Si vous spécifiez une valeur pour la propriété de démarrage hello, vous devez spécifier la valeur de propriété de fin hello.<br/><br/>Consultez les remarques pour hello **Démarrer** propriété. |
| isPaused |Si set tootrue hello pipeline ne s’exécute pas. Valeur par défaut = false. Vous pouvez utiliser cette propriété tooenable ou désactiver. |Non |
| pipelineMode |méthode Hello pour la planification s’exécute pour le pipeline de hello. Les valeurs autorisées sont : scheduled (par défaut) et onetime.<br/><br/>'Planifiée' indique ce pipeline hello s’exécute sur un intervalle de temps spécifié selon la période active de tooits (heure de début et de fin). « Unique » indique que ce pipeline hello s’exécute qu’une seule fois. Une fois créés, les pipelines de type onetime ne peuvent pas être modifiés ni mis à jour pour le moment. Consultez la page [Pipeline onetime](data-factory-create-pipelines.md#onetime-pipeline) pour plus d’informations sur le paramètre onetime. |Non |
| expirationTime |Durée de temps après sa création pour le hello pipeline est valide et doit rester mis en service. Si elle n’a pas tout actif, échec, ou en attente d’exécution, le pipeline de hello est supprimé automatiquement lorsqu’il atteint le délai d’expiration de hello. |Non |


## <a name="activity"></a>Activité 
structure de haut niveau Hello pour une activité dans une définition de pipeline (élément activités) est la suivante :

```json
{
    "name": "ActivityName",
    "description": "description", 
    "type": "<ActivityType>",
    "inputs":  "[]",
    "outputs":  "[]",
    "linkedServiceName": "MyLinkedService",
    "typeProperties":
    {

    },
    "policy":
    {
    }
    "scheduler":
    {
    }
}
```

Tableau suivant décrivent les propriétés hello dans l’activité hello définition JSON :

| Tag | Description | Requis |
| --- | --- | --- |
| name |Nom de l’activité hello. Spécifiez un nom qui représente l’action de hello activité hello est configuré toodo<br/><ul><li>Nombre maximal de caractères : 260</li><li>Doit commencer par une lettre, un chiffre ou un trait de soulignement (_)</li><li>Les caractères suivants ne sont pas autorisés : « . », « + », « ? », « / », « < », « > », « * », « % », « & », « : », « \\ »</li></ul> |Oui |
| description |Texte décrivant de quelle activité hello est destiné. |Oui |
| type |Spécifie le type hello d’activité hello. Consultez hello [banques de données](#data-stores) et [activités de TRANSFORMATION des données](#data-transformation-activities) sections pour les différents types d’activités. |Oui |
| inputs |Tables d’entrée utilisés par l’activité hello<br/><br/>`// one input table`<br/>`"inputs":  [ { "name": "inputtable1"  } ],`<br/><br/>`// two input tables` <br/>`"inputs":  [ { "name": "inputtable1"  }, { "name": "inputtable2"  } ],` |Oui |
| outputs |Tables de sortie utilisés par l’activité hello.<br/><br/>`// one output table`<br/>`"outputs":  [ { "name": “outputtable1” } ],`<br/><br/>`//two output tables`<br/>`"outputs":  [ { "name": “outputtable1” }, { "name": “outputtable2” }  ],` |Oui |
| linkedServiceName |Nom du service hello lié utilisé par l’activité hello. <br/><br/>Une activité peut nécessiter que vous spécifiez service hello lié qui lie l’environnement de calcul requis toohello. |Oui pour les activités HDInsight, les activités de Azure Machine Learning et les activités de procédure stockée. <br/><br/>Non pour toutes les autres |
| typeProperties |Propriétés dans la section de typeProperties hello dépendent du type d’activité hello. |Non |
| policy |Stratégies qui affectent le comportement d’exécution hello d’activité hello. Si aucune valeur n’est spécifiée, les stratégies par défaut sont utilisées. |Non |
| scheduler |propriété de « planificateur » est utilisé toodefine souhaité pour l’activité hello. Sous-propriétés sont hello identique à celle de hello hello [propriété de disponibilité dans un jeu de données](data-factory-create-datasets.md#dataset-availability). |Non |

### <a name="policies"></a>Stratégies
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

### <a name="typeproperties-section"></a>Section typeProperties
section de typeProperties Hello est différente pour chaque activité. Les activités de transformation ont uniquement des propriétés de type hello. Consultez la section [Activités de transformation des données](#data-transformation-activities) dans cet article pour obtenir des exemples JSON qui définissent les activités de transformation dans un pipeline. 

**Activité de copie** a deux sous-sections suivantes dans la section de typeProperties hello : **source** et **récepteur**. Consultez [banques de données](#data-stores) section de cet article pour JSON exemples qui montrent comment stocker des toouse données comme une source et/ou un récepteur. 

### <a name="sample-copy-pipeline"></a>Exemple de pipeline de copie
Bonjour suivant l’exemple de pipeline, il existe une activité de type **copie** Bonjour **activités** section. Dans cet exemple, hello [activité de copie](data-factory-data-movement-activities.md) copie les données à partir d’une base de données SQL Azure de tooan stockage Blob Azure. 

```json
{
  "name": "CopyPipeline",
  "properties": {
    "description": "Copy data from a blob tooAzure SQL table",
    "activities": [
      {
        "name": "CopyFromBlobToSQL",
        "type": "Copy",
        "inputs": [
          {
            "name": "InputDataset"
          }
        ],
        "outputs": [
          {
            "name": "OutputDataset"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "BlobSource"
          },
          "sink": {
            "type": "SqlSink",
            "writeBatchSize": 10000,
            "writeBatchTimeout": "60:00:00"
          }
        },
        "Policy": {
          "concurrency": 1,
          "executionPriorityOrder": "NewestFirst",
          "retry": 0,
          "timeout": "01:00:00"
        }
      }
    ],
    "start": "2016-07-12T00:00:00",
    "end": "2016-07-13T00:00:00"
  }
} 
```

Hello Notez les points suivants :

* Dans la section d’activités hello, il n'existe qu’une seule activité dont **type** est défini trop**copie**.
* Entrée d’activité hello est définie trop**InputDataset** et de sortie d’activité hello est définie trop**OutputDataset**.
* Bonjour **typeProperties** section, **BlobSource** est spécifié comme type de source de hello et **SqlSink** est spécifié comme type de récepteur hello.

Consultez [banques de données](#data-stores) section de cet article pour JSON exemples qui montrent comment stocker des toouse données comme une source et/ou un récepteur.    

Pour obtenir une description complète de la création de ce pipeline, consultez [didacticiel : copier des données à partir du stockage d’objets Blob tooSQL de base de données](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md). 

### <a name="sample-transformation-pipeline"></a>Exemple de pipeline de transformation
Bonjour suivant l’exemple de pipeline, il existe une activité de type **HDInsightHive** Bonjour **activités** section. Dans cet exemple, hello [activité HDInsight Hive](data-factory-hive-activity.md) transforme les données d’un stockage d’objets Blob Azure en exécutant un fichier de script Hive sur un cluster Azure HDInsight Hadoop. 

```json
{
    "name": "TransformPipeline",
    "properties": {
        "description": "My first Azure Data Factory pipeline",
        "activities": [
            {
                "type": "HDInsightHive",
                "typeProperties": {
                    "scriptPath": "adfgetstarted/script/partitionweblogs.hql",
                    "scriptLinkedService": "AzureStorageLinkedService",
                    "defines": {
                        "inputtable": "wasb://adfgetstarted@<storageaccountname>.blob.core.windows.net/inputdata",
                        "partitionedtable": "wasb://adfgetstarted@<storageaccountname>.blob.core.windows.net/partitioneddata"
                    }
                },
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
                "policy": {
                    "concurrency": 1,
                    "retry": 3
                },
                "scheduler": {
                    "frequency": "Month",
                    "interval": 1
                },
                "name": "RunSampleHiveActivity",
                "linkedServiceName": "HDInsightOnDemandLinkedService"
            }
        ],
        "start": "2016-04-01T00:00:00",
        "end": "2016-04-02T00:00:00",
        "isPaused": false
    }
}
```

Hello Notez les points suivants : 

* Dans la section d’activités hello, il n'existe qu’une seule activité dont **type** est défini trop**HDInsightHive**.
* fichier de script Hive Hello, **partitionweblogs.hql**, est stocké dans hello compte de stockage Azure (spécifié par scriptLinkedService hello, appelé **AzureStorageLinkedService**) et dans  **script** dossier dans le conteneur de hello **adfgetstarted**.
* Hello **définit** section est de paramètres d’exécution utilisés toospecify hello script hive de toohello passés en tant que valeurs de configuration Hive (par exemple `${hiveconf:inputtable}`, `${hiveconf:partitionedtable}`).

Consultez la section [Activités de transformation des données](#data-transformation-activities) dans cet article pour obtenir des exemples JSON qui définissent les activités de transformation dans un pipeline.

Pour obtenir une description complète de la création de ce pipeline, consultez [didacticiel : créer vos premières données tooprocess de pipeline à l’aide de cluster Hadoop](data-factory-build-your-first-pipeline.md). 

## <a name="linked-service"></a>Service lié
structure de haut niveau Hello pour une définition de service lié est comme suit :

```json
{
    "name": "<name of hello linked service>",
    "properties": {
        "type": "<type of hello linked service>",
        "typeProperties": {
        }
    }
}
```

Tableau suivant décrivent les propriétés hello dans l’activité hello définition JSON :

| Propriété | Description | Requis |
| -------- | ----------- | -------- | 
| name | Nom du service de hello lié. | Oui | 
| propriétés - type | Type de service de hello lié. Par exemple : Stockage Azure, Azure SQL Database. |
| typeProperties | section de typeProperties Hello comporte des éléments qui sont différents pour chaque magasin de données ou l’environnement de calcul. Consultez [banques de données](#datastores) section pour toutes les données hello magasin des services liés et [environnements de calcul](#compute-environments) pourquoi tous les services liés de calcul. |   

## <a name="dataset"></a>Jeu de données 
Un jeu de données dans Azure Data Factory est défini comme suit :

```json
{
    "name": "<name of dataset>",
    "properties": {
        "type": "<type of dataset: AzureBlob, AzureSql etc...>",
        "external": <boolean flag tooindicate external data. only for input datasets>,
        "linkedServiceName": "<Name of hello linked service that refers tooa data store.>",
        "structure": [
            {
                "name": "<Name of hello column>",
                "type": "<Name of hello type>"
            }
        ],
        "typeProperties": {
            "<type specific property>": "<value>",
            "<type specific property 2>": "<value 2>",
        },
        "availability": {
            "frequency": "<Specifies hello time unit for data slice production. Supported frequency: Minute, Hour, Day, Week, Month>",
            "interval": "<Specifies hello interval within hello defined frequency. For example, frequency set too'Hour' and interval set too1 indicates that new data slices should be produced hourly>"
        },
       "policy":
        {      
        }
    }
}
```

Hello tableau suivant décrit les propriétés dans hello ci-dessus JSON :   

| Propriété | Description | Requis | Default |
| --- | --- | --- | --- |
| name | Nom du jeu de données hello. Pour connaître les règles d’affectation des noms, voir [Azure Data Factory - Règles d’affectation des noms](data-factory-naming-rules.md). |Oui |N/D |
| type | Type de jeu de données hello. Spécifiez un des types hello pris en charge par Azure Data Factory (par exemple : AzureBlob, AzureSqlTable). Consultez [banques de données](#data-stores) section tous hello banques de données et les types de jeu de données pris en charge par la fabrique de données. | 
| structure | Schéma du jeu de données hello. Il contient des colonnes, leurs types, etc. | Non |N/D |
| typeProperties | Les propriétés correspondant toohello le type sélectionné. Consultez la section [Magasins de données](#data-stores) pour en savoir plus sur les types pris en charge et leurs propriétés. |Oui |N/D |
| external | Indicateur booléen toospecify si un jeu de données est explicitement généré par un pipeline de fabrique de données ou non. |Non |false |
| availability | Définit hello du traitement de fenêtre ou hello le découpage du modèle pour la production de dataset hello. Pour plus d’informations sur le dataset hello le découpage du modèle, consultez [de planification et de l’exécution](data-factory-scheduling-and-execution.md) l’article. |Oui |N/D |
| policy |Définit les critères de hello ou une condition hello tranches de dataset hello doivent répondre. <br/><br/>Pour plus d’informations, consultez la section [Disponibilité du jeu de données](#Policy) . |Non |N/D |

Chaque colonne de hello **structure** section contient hello propriétés suivantes :

| Propriété | Description | Requis |
| --- | --- | --- |
| name |Nom de colonne de hello. |Oui |
| type |Type de données de colonne de hello.  |Non |
| culture |.NET basé toobe culture utilisée lorsque le type est spécifié et qu’il est de type .NET `Datetime` ou `Datetimeoffset`. La valeur par défaut est `en-us`. |Non |
| format |Mettre en forme toobe de chaîne utilisé lorsque le type est spécifié et qu’il est de type .NET `Datetime` ou `Datetimeoffset`. |Non |

Dans l’exemple suivant de hello, jeu de données hello possède trois colonnes `slicetimestamp`, `projectname`, et `pageviews` et ils sont de type : chaîne, chaîne et Decimal respectivement.

```json
structure:  
[
    { "name": "slicetimestamp", "type": "String"},
    { "name": "projectname", "type": "String"},
    { "name": "pageviews", "type": "Decimal"}
]
```

Hello tableau suivant décrit les propriétés que vous pouvez utiliser Bonjour **disponibilité** section :

| Propriété | Description | Requis | Default |
| --- | --- | --- | --- |
| frequency |Spécifie l’unité de temps hello pour la production de tranche de jeu de données.<br/><br/><b>Fréquence prise en charge</b>: minute, heure, jour, semaine, mois |Oui |N/D |
| interval |Spécifie un multiplicateur de fréquence<br/><br/>« Intervalle de fréquence x » détermine la fréquence à laquelle hello tranche est produite.<br/><br/>Si vous avez besoin de hello toobe dataset découpée sur toutes les heures, vous définissez <b>fréquence</b> trop<b>heure</b>, et <b>intervalle</b> trop<b>1</b>.<br/><br/><b>Remarque</b>: Si vous spécifiez la fréquence de minutes, nous vous recommandons de définir hello intervalle toono inférieur à 15 |Oui |N/D |
| style |Spécifie si la tranche de hello doit être produite au hello début/fin d’intervalle de salutation.<ul><li>StartOfInterval</li><li>EndOfInterval</li></ul><br/><br/>Si tooMonth est définie à la fréquence et le style a la valeur tooEndOfInterval, hello tranche est produite hello dernier jour du mois. Si le style de hello a la valeur tooStartOfInterval, hello tranche est produite hello premier jour du mois.<br/><br/>Si tooDay est définie à la fréquence et le style a la valeur tooEndOfInterval, tranche de hello est produite dans hello dernière heure du jour de hello.<br/><br/>Si tooHour est définie à la fréquence et le style a la valeur tooEndOfInterval, tranche de hello est produite à fin hello d’heure de hello. Par exemple, pour une tranche de période de 13 h 00 à 14 h 00, la tranche de hello est produite à 14 heures. |Non |EndOfInterval |
| anchorDateTime |Définit la position absolue de hello dans le temps utilisé par les limites de la section Planificateur toocompute jeu de données. <br/><br/><b>Remarque</b>: si hello AnchorDateTime comporte des parties de date qui sont plus précis que la fréquence de hello, hello plus granulaires parties sont ignorés. <br/><br/>Par exemple, si hello <b>intervalle</b> est <b>toutes les heures</b> (fréquence : heure et intervalle : 1) et hello <b>AnchorDateTime</b> contient <b>minutes et secondes</b>puis hello <b>minutes et secondes</b> parties Hello AnchorDateTime sont ignorées. |Non |01/01/0001 |
| Offset |Intervalle de temps par le hello début et fin de toutes les tranches de jeu de données sont déplacées. <br/><br/><b>Remarque</b>: si anchorDateTime et offset sont spécifiés, hello résulte hello combinée MAJ. |Non |N/D |

Hello suivant la section disponibilité spécifie ce jeu de données de sortie hello est produit toutes les heures (ou) entrée jeu de données est disponible, toutes les heures :

```json
"availability":    
{    
    "frequency": "Hour",        
    "interval": 1    
}
```

Hello **stratégie** section dans la définition de dataset définit des critères de hello ou condition hello hello tranches de jeu de données doit répondre.

| Nom de la stratégie | Description | Appliqué trop| Requis | Default |
| --- | --- | --- | --- | --- |
| minimumSizeMB |Valide les données hello dans un **objets blob Azure** répond aux hello exigences de taille minimale (en mégaoctets). |Objets blob Azure |Non |N/D |
| minimumRows |Valide les données hello dans un **base de données SQL Azure** ou un **table Azure** contient hello le nombre minimal de lignes. |<ul><li>Base de données SQL Azure</li><li>table Azure</li></ul> |Non |N/D |

**Exemple :**

```json
"policy":

{
    "validation":
    {
        "minimumSizeMB": 10.0
    }
}
```

À moins qu’un jeu de données ne soit généré par Azure Data Factory, il doit être marqué comme **external**(externe). Ce paramètre s’applique généralement toohello les entrées de la première activité dans un pipeline, sauf si l’activité ou le chaînage des propriétés de pipeline sont utilisé.

| Nom | Description | Requis | Valeur par défaut |
| --- | --- | --- | --- |
| dataDelay |Vérification de hello toodelay temps sur la disponibilité de données externes de hello pour hello donné tranche hello. Par exemple, si les données de salutation sont disponibles, toutes les heures, hello vérification toosee hello externe des données sont disponibles et hello la tranche correspondante est prêt peut être différée à l’aide de dataDelay.<br/><br/>S’applique uniquement toohello moment présent.  Par exemple, si elle est de 1:00 PM maintenant et cette valeur est de 10 minutes, la validation hello démarre à 1 h 10.<br/><br/>Ce paramètre n’affecte pas les tranches Bonjour passées (tranches Slice End Time + dataDelay < maintenant) sont traitées sans délai.<br/><br/>Durée supérieure à 23:59 heures doivent toospecified à l’aide de hello `day.hours:minutes:seconds` format. Par exemple, toospecify 24 heures, n’utilisez pas 24:00:00 ; au lieu de cela, utilisez 1.00:00:00. Si vous utilisez 24:00:00, cette valeur est traitée comme 24 jours (24.00:00:00). Pour 1 jour et 4 heures, spécifiez 1:04:00:00. |Non |0 |
| retryInterval |temps d’attente Hello entre une défaillance et hello suivant nouvelle tentative. Si une tentative échoue, la prochaine tentative de hello est après retryInterval. <br/><br/>S’il s’agit de 1:00 PM dès maintenant, nous commençons hello première tentative. Si hello durée toocomplete hello premier contrôle de validation est 1 minute et échoué de l’opération hello, nouvelle tentative suivante d’hello est à 1:00 + 1 min (durée) + 1 minute (intervalle avant nouvelle tentative) = 1:02 PM. <br/><br/>Aux tranches passées de hello, il n’existe aucun délai. nouvelle tentative de Hello se produit immédiatement. |Non |00:01:00 (1 minute) |
| retryTimeout |délai d’expiration de Hello pour chaque nouvelle tentative.<br/><br/>Si cette propriété a la valeur too10 minutes, hello toobe de besoins de validation s’est terminée dans les 10 minutes. Si elle dure plus longtemps que la validation de 10 minutes tooperform hello, hello recommencez arrive à expiration.<br/><br/>Si toutes les tentatives pour la validation de hello expire, la tranche de hello est marquée comme TimedOut. |Non |00:10:00 (10 minutes) |
| maximumRetry |Nombre de fois où toocheck pour la disponibilité de données externes de hello hello. Hello autorisé la valeur maximale est 10. |Non |3 |


## <a name="data-stores"></a>MAGASINS DE DONNÉES
Hello [service lié](#linked-service) descriptions section fournie pour les éléments JSON qui sont des types courants de tooall de services liés. Cette section fournit des détails sur les éléments JSON qui sont le magasin de données tooeach spécifique.

Hello [Dataset](#dataset) descriptions section fournie pour les éléments JSON qui sont des types courants de tooall des jeux de données. Cette section fournit des détails sur les éléments JSON qui sont le magasin de données tooeach spécifique.

Hello [activité](#activity) des descriptions de section fournie pour les éléments JSON qui sont des types tooall communs d’activités. Cette section fournit des détails sur les éléments JSON qui sont le magasin de données tooeach spécifique lorsqu’elle est utilisée comme un source/récepteur dans une activité de copie.  

Cliquez sur lien hello magasin hello vous intéressez dans les schémas JSON toosee hello pour le service lié, le jeu de données et hello source/récepteur pour l’activité de copie hello.

| Catégorie | Banque de données 
|:--- |:--- |
| **Microsoft Azure** |[stockage d’objets blob Azure](#azure-blob-storage) |
| &nbsp; |[Azure Data Lake Store](#azure-datalake-store) |
| &nbsp; |[Azure Cosmos DB](#azure-cosmos-db) |
| &nbsp; |[Azure SQL Database](#azure-sql-database) |
| &nbsp; |[Azure SQL Data Warehouse](#azure-sql-data-warehouse) |
| &nbsp; |[Recherche Azure](#azure-search) |
| &nbsp; |[Stockage Table Azure](#azure-table-storage) |
| **Bases de données** |[Amazon Redshift](#amazon-redshift) |
| &nbsp; |[IBM DB2](#ibm-db2) |
| &nbsp; |[MySQL](#mysql) |
| &nbsp; |[Oracle](#oracle) |
| &nbsp; |[PostgreSQL](#postgresql) |
| &nbsp; |[SAP Business Warehouse](#sap-business-warehouse) |
| &nbsp; |[SAP HANA](#sap-hana) |
| &nbsp; |[SQL Server](#sql-server) |
| &nbsp; |[Sybase](#sybase) |
| &nbsp; |[Teradata](#teradata) |
| **NoSQL** |[Cassandra](#cassandra) |
| &nbsp; |[MongoDB](#mongodb) |
| **File** |[Amazon S3](#amazon-s3) |
| &nbsp; |[Système de fichiers](#file-system) |
| &nbsp; |[FTP](#ftp) |
| &nbsp; |[HDFS](#hdfs) |
| &nbsp; |[SFTP](#sftp) |
| **Autres** |[HTTP](#http) |
| &nbsp; |[OData](#odata) |
| &nbsp; |[ODBC](#odbc) |
| &nbsp; |[Salesforce](#salesforce) |
| &nbsp; |[Table web](#web-table) |

## <a name="azure-blob-storage"></a>un stockage Azure Blob

### <a name="linked-service"></a>Service lié
Il existe deux types de services liés : les services liés de stockage Azure et les services liés SAP de stockage Azure.

#### <a name="azure-storage-linked-service"></a>Service lié Stockage Azure
toolink votre fabrique de données tooa compte stockage Azure à l’aide de hello **clé de compte**, créez un service lié Azure Storage. le service ensemble hello lié toodefine un stockage Azure **type** Hello service lié trop**AzureStorage**. Ensuite, vous pouvez spécifier les propriétés Bonjour suivantes **typeProperties** section :  

| Propriété | Description | Requis |
|:--- |:--- |:--- |
| connectionString |Spécifiez les informations nécessaires tooconnect tooAzure stockage pour la propriété connectionString de hello. |Oui |

##### <a name="example"></a>Exemple  

```json
{
    "name": "StorageLinkedService",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
        }
    }
}
```

#### <a name="azure-storage-sas-linked-service"></a>Service lié SAP de stockage Azure
Hello SAS de stockage Azure lié service vous permet de toolink une fabrique de données Azure tooan compte de stockage Azure à l’aide d’une Signature d’accès partagé (SAS). Il fournit des fabrique de données hello avec l’accès restreint/limitées dans le temps de tooall/spécifiques des ressources (objet blob/conteneur) dans le stockage hello. toolink votre fabrique de données tooa compte stockage Azure à l’aide de Signature d’accès partagé, créez un service de SAS de stockage Azure lié. le service ensemble hello lié toodefine un SAS de stockage Azure **type** Hello service lié trop**AzureStorageSas**. Ensuite, vous pouvez spécifier les propriétés Bonjour suivantes **typeProperties** section :   

| Propriété | Description | Requis |
|:--- |:--- |:--- |
| sasUri |Spécifier des ressources de stockage Azure toohello URI de Signature d’accès partagé comme objet blob, conteneur ou une table. |Oui |

##### <a name="example"></a>Exemple

```json
{  
    "name": "StorageSasLinkedService",  
    "properties": {  
        "type": "AzureStorageSas",  
        "typeProperties": {  
            "sasUri": "<storageUri>?<sasToken>"   
        }  
    }  
}  
```

Pour plus d’informations sur ces services liés, consultez l’article [Connecteur de stockage Blob Azure](data-factory-azure-blob-connector.md#linked-service-properties). 

### <a name="dataset"></a>Jeu de données
toodefine un jeu de données d’objets Blob Azure, jeu hello **type** du jeu de données hello trop**AzureBlob**. Ensuite, spécifiez hello propriétés spécifiques d’objets Blob Azure Bonjour suivantes **typeProperties** section : 

| Propriété | Description | Requis |
| --- | --- | --- |
| folderPath |Conteneur toohello de chemin d’accès et le dossier de stockage d’objets blob hello. Exemple : monconteneurblob\mondossierblob\ |Oui |
| fileName |Nom de l’objet blob de hello. fileName est facultatif et sensible à la casse.<br/><br/>Si vous spécifiez un nom de fichier, le hello activité (y compris la copie) fonctionne sur hello Blob spécifique.<br/><br/>Lorsque le nom de fichier n’est pas spécifié, copie inclut tous les objets BLOB dans folderPath hello pour le jeu de données d’entrée.<br/><br/>Lorsque le nom de fichier n’est pas spécifié pour un dataset de sortie, nom hello du fichier de hello généré serait Bonjour sous ce format : données. <Guid>.txt (par exemple : : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt |Non |
| partitionedBy |partitionedBy est une propriété facultative. Vous pouvez utiliser il toospecify un folderPath dynamique et le nom de fichier de données de série chronologique. Par exemple, folderPath peut être paramétré pour toutes les heures de données. |Non |
| format | Hello, les types de format suivants est pris en charge : **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**. Ensemble hello **type** propriété sous tooone de format de ces valeurs. Pour en savoir plus, consultez les sections relatives à [format Text](data-factory-supported-file-and-compression-formats.md#text-format), [format Json](data-factory-supported-file-and-compression-formats.md#json-format), [format Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [format Orc](data-factory-supported-file-and-compression-formats.md#orc-format) et [format Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format). <br><br> Si vous souhaitez trop**copier les fichiers en tant que-est** entre des magasins basée sur le fichier (copie binaire), ignorer la section de format hello dans les deux définitions de jeu de données d’entrée et de sortie. |Non |
| compression | Spécifiez le type de hello et le niveau de compression pour les données de salutation. Les types pris en charge sont : **GZip**, **Deflate**, **BZip2** et **ZipDeflate**. Les niveaux pris en charge sont **Optimal** et **Fastest**. Pour plus d’informations, consultez [Formats de fichiers et de compression pris en charge dans Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support). |Non |

#### <a name="example"></a>Exemple

```json
{
    "name": "AzureBlobInput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "fileName": "input.log",
            "folderPath": "adfgetstarted/inputdata",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability": {
            "frequency": "Month",
            "interval": 1
        },
        "external": true,
        "policy": {}
    }
}
 ```


Pour plus d’informations, consultez l’article [Azure Blob connector (connecteur d’objet blob Azure)](data-factory-azure-blob-connector.md#dataset-properties).

### <a name="blobsource-in-copy-activity"></a>BlobSource dans l’activité de copie
Si vous copiez des données à partir d’un stockage d’objets Blob Azure, la valeur hello **type de source de** Hello activité de copie trop**BlobSource**et spécifiez les propriétés Bonjour suivantes ** source ** section :

| Propriété | Description | Valeurs autorisées | Requis |
| --- | --- | --- | --- |
| recursive |Indique si les données de salutation sont lu de manière récursive à partir de dossiers de sub hello ou uniquement à partir de dossier spécifié de hello. |True (valeur par défaut), False |Non |

#### <a name="example-blobsource"></a>Exemple : BlobSource**
```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoSQL",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "AzureSqlOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "BlobSource"
                },
                "sink": {
                    "type": "SqlSink"
                }
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```
### <a name="blobsink-in-copy-activity"></a>BlobSink dans l’activité de copie
Si vous copiez des données tooan stockage d’objets Blob Azure, la valeur hello **type de récepteur** Hello activité de copie trop**BlobSink**et spécifiez les propriétés Bonjour suivantes **récepteur** section :

| Propriété | Description | Valeurs autorisées | Requis |
| --- | --- | --- | --- |
| copyBehavior |Définit le comportement de copie de hello lors de la source de hello est BlobSource ou système de fichiers. |<b>PreserveHierarchy</b>: préserve hello hiérarchie de fichiers dans le dossier cible de hello. chemin d’accès relatif de Hello du dossier source du fichier toosource est identique toohello un chemin d’accès relatif du dossier tootarget de fichier cible.<br/><br/><b>FlattenHierarchy</b>: tous les fichiers à partir du dossier source hello sont Bonjour tout d’abord au niveau du dossier cible. les fichiers cibles Hello ont un nom généré automatiquement. <br/><br/><b>MergeFiles (valeur par défaut) :</b> fusionne tous les fichiers à partir de fichiers de tooone du dossier source hello. Si hello nom de fichier/objet Blob est spécifié, le nom de fichier fusionné hello serait nom spécifié de hello ; dans le cas contraire, serait de nom de fichier généré automatiquement. |Non |

#### <a name="example-blobsink"></a>Exemple : BlobSink

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "AzureSQLtoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureSQLInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "SqlSource",
                    "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

Pour plus d’informations, consultez l’article [Azure Blob connector (connecteur d’objet blob Azure)](data-factory-azure-blob-connector.md#copy-activity-properties). 

## <a name="azure-data-lake-store"></a>Azure Data Lake Store

### <a name="linked-service"></a>Service lié
toodefine un service Azure Data Lake Store lié, définir le type de hello de hello service lié trop**AzureDataLakeStore**et spécifiez les propriétés Bonjour suivantes **typeProperties** section :  

| Propriété | Description | Requis |
|:--- |:--- |:--- |
| type | propriété de type Hello doit indiquer : **AzureDataLakeStore** | Oui |
| dataLakeStoreUri | Indiquez les informations hello compte Azure Data Lake Store. Il se trouve dans hello suivant le format : `https://[accountname].azuredatalakestore.net/webhdfs/v1` ou `adl://[accountname].azuredatalakestore.net/`. | Oui |
| subscriptionId | Abonnement Azure Id toowhich Data Lake Store appartient. | Requis pour le récepteur |
| resourceGroupName | Toowhich de nom du groupe de ressources Azure Data Lake Store appartient. | Requis pour le récepteur |
| servicePrincipalId | Spécifiez l’ID client de. l’application hello | Oui (pour l’authentification du principal du service) |
| servicePrincipalKey | Spécifiez la clé de l’application hello. | Oui (pour l’authentification du principal du service) |
| locataire | Spécifiez les informations de locataire hello (ID client ou le nom de domaine) dans lequel réside votre application. Vous pouvez le récupérer par pointage de souris hello en hello en haut à droite de hello portail Azure. | Oui (pour l’authentification du principal du service) |
| autorisation | Cliquez sur **Authorize** bouton Bonjour **éditeur Data Factory** et entrez vos informations d’identification qui lui attribue hello généré automatiquement l’autorisation URL toothis. | Oui (pour l’authentification des informations d’identification utilisateur)|
| sessionId | Id de session OAuth à partir de la session de d’autorisation OAuth hello. Chaque ID de session est unique et ne peut être utilisé qu’une seule fois. Ce paramètre est généré automatiquement lorsque vous utilisez Data Factory Editor. | Oui (pour l’authentification des informations d’identification utilisateur) |

#### <a name="example-using-service-principal-authentication"></a>Exemple : utilisation de l’authentification d’un principal du service
```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info. Example: microsoft.onmicrosoft.com>"
        }
    }
}
```

#### <a name="example-using-user-credential-authentication"></a>Exemple : utilisation de l’authentification des informations d’identification utilisateur
```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "sessionId": "<session ID>",
            "authorization": "<authorization URL>",
            "subscriptionId": "<subscription of ADLS>",
            "resourceGroupName": "<resource group of ADLS>"
        }
    }
}
```

Pour plus d’informations, consultez l’article [Azure Data Lake Store connector (connecteur Azure Data Lake Store)](data-factory-azure-datalake-connector.md#linked-service-properties). 

### <a name="dataset"></a>Jeu de données
toodefine un dataset Azure Data Lake Store, jeu hello **type** du jeu de données hello trop**AzureDataLakeStore**et spécifiez hello propriétés Bonjour suivantes **typeProperties**section : 

| Propriété | Description | Requis |
|:--- |:--- |:--- |
| folderPath |Conteneur toohello de chemin d’accès et le dossier à hello Azure Data Lake stockent. |Oui |
| fileName |Nom du fichier hello dans le magasin d’Azure Data Lake hello. fileName est facultatif et sensible à la casse. <br/><br/>Si vous spécifiez un nom de fichier, activité hello (y compris la copie) fonctionne sur un fichier spécifique hello.<br/><br/>Lorsque le nom de fichier n’est pas spécifié, la copie inclut tous les fichiers dans folderPath hello pour le jeu de données d’entrée.<br/><br/>Lorsque le nom de fichier n’est pas spécifié pour un dataset de sortie, nom hello du fichier de hello généré serait Bonjour sous ce format : données. <Guid>.txt (par exemple : : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt |Non |
| partitionedBy |partitionedBy est une propriété facultative. Vous pouvez utiliser il toospecify un folderPath dynamique et le nom de fichier de données de série chronologique. Par exemple, folderPath peut être paramétré pour toutes les heures de données. |Non |
| format | Hello, les types de format suivants est pris en charge : **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**. Ensemble hello **type** propriété sous tooone de format de ces valeurs. Pour en savoir plus, consultez les sections relatives à [format Text](data-factory-supported-file-and-compression-formats.md#text-format), [format Json](data-factory-supported-file-and-compression-formats.md#json-format), [format Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [format Orc](data-factory-supported-file-and-compression-formats.md#orc-format) et [format Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format). <br><br> Si vous souhaitez trop**copier les fichiers en tant que-est** entre des magasins basée sur le fichier (copie binaire), ignorer la section de format hello dans les deux définitions de jeu de données d’entrée et de sortie. |Non |
| compression | Spécifiez le type de hello et le niveau de compression pour les données de salutation. Les types pris en charge sont : **GZip**, **Deflate**, **BZip2** et **ZipDeflate**. Les niveaux pris en charge sont **Optimal** et **Fastest**. Pour plus d’informations, consultez [Formats de fichiers et de compression pris en charge dans Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support). |Non |

#### <a name="example"></a>Exemple
```json
{
    "name": "AzureDataLakeStoreInput",
    "properties": {
        "type": "AzureDataLakeStore",
        "linkedServiceName": "AzureDataLakeStoreLinkedService",
        "typeProperties": {
            "folderPath": "datalake/input/",
            "fileName": "SearchLog.tsv",
            "format": {
                "type": "TextFormat",
                "rowDelimiter": "\n",
                "columnDelimiter": "\t"
            }
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
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

Pour plus d’informations, consultez l’article [Azure Data Lake Store connector (connecteur Azure Data Lake Store)](data-factory-azure-datalake-connector.md#dataset-properties). 

### <a name="azure-data-lake-store-source-in-copy-activity"></a>Source Azure Data Lake Store dans l’activité de copie
Si vous copiez des données à partir d’un Azure Data Lake Store, la valeur hello **type de source de** Hello activité de copie trop**AzureDataLakeStoreSource**et spécifiez les propriétés Bonjour suivantes **source**  section :

**AzureDataLakeStoreSource** prend en charge les propriétés suivantes de hello **typeProperties** section :

| Propriété | Description | Valeurs autorisées | Requis |
| --- | --- | --- | --- |
| recursive |Indique si les données de salutation sont lu de manière récursive à partir de dossiers de sub hello ou uniquement à partir de dossier spécifié de hello. |True (valeur par défaut), False |Non |

#### <a name="example-azuredatalakestoresource"></a>Exemple : AzureDataLakeStoreSource

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "AzureDakeLaketoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureDataLakeStoreInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "AzureDataLakeStoreSource"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

Pour plus d’informations, consultez l’article [Azure Data Lake Store connector (connecteur Azure Data Lake Store)](data-factory-azure-datalake-connector.md#copy-activity-properties).

### <a name="azure-data-lake-store-sink-in-copy-activity"></a>Récepteur Azure Data Lake Store dans l’activité de copie
Si vous copiez des données tooan Azure Data Lake Store, la valeur hello **type de récepteur** Hello activité de copie trop**AzureDataLakeStoreSink**et spécifiez les propriétés Bonjour suivantes **récepteur**section :

| Propriété | Description | Valeurs autorisées | Requis |
| --- | --- | --- | --- |
| copyBehavior |Spécifie le comportement de copie hello. |<b>PreserveHierarchy</b>: préserve hello hiérarchie de fichiers dans le dossier cible de hello. chemin d’accès relatif de Hello du dossier source du fichier toosource est identique toohello un chemin d’accès relatif du dossier tootarget de fichier cible.<br/><br/><b>FlattenHierarchy</b>: tous les fichiers à partir du dossier source hello sont créés dans hello premier niveau du dossier cible. les fichiers cibles Hello sont créés avec le nom généré automatiquement.<br/><br/><b>MergeFiles</b>: fusionne tous les fichiers à partir de fichiers de tooone du dossier source hello. Si hello nom de fichier/objet Blob est spécifié, le nom de fichier fusionné hello serait nom spécifié de hello ; dans le cas contraire, serait de nom de fichier généré automatiquement. |Non |

#### <a name="example-azuredatalakestoresink"></a>Exemple : AzureDataLakeStoreSink
```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoDataLake",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "AzureDataLakeStoreOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "BlobSource"
                },
                "sink": {
                    "type": "AzureDataLakeStoreSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

Pour plus d’informations, consultez l’article [Azure Data Lake Store connector (connecteur Azure Data Lake Store)](data-factory-azure-datalake-connector.md#copy-activity-properties). 

## <a name="azure-cosmos-db"></a>Azure Cosmos DB  

### <a name="linked-service"></a>Service lié
toodefine une base de données Azure Cosmos le service ensemble hello lié **type** Hello service lié trop**DocumentDb**et spécifiez les propriétés Bonjour suivantes **typeProperties** section :  

| **Propriété** | **Description** | **Obligatoire** |
| --- | --- | --- |
| connectionString |Spécifiez les informations nécessaires de base de données de base de données Cosmos tooconnect tooAzure. |Oui |

#### <a name="example"></a>Exemple

```json
{
    "name": "CosmosDBLinkedService",
    "properties": {
        "type": "DocumentDb",
        "typeProperties": {
            "connectionString": "AccountEndpoint=<EndpointUrl>;AccountKey=<AccessKey>;Database=<Database>"
        }
    }
}
```
Pour plus d’informations, consultez l’article sur le [connecteur d’objet blob Azure](data-factory-azure-documentdb-connector.md#linked-service-properties).

### <a name="dataset"></a>Jeu de données
toodefine un jeu de données de base de données Azure Cosmos, jeu hello **type** du jeu de données hello trop**DocumentDbCollection**et spécifiez hello propriétés Bonjour suivantes **typeProperties** section : 

| **Propriété** | **Description** | **Obligatoire** |
| --- | --- | --- |
| collectionName |Nom de collection de base de données Azure Cosmos de hello. |Oui |

#### <a name="example"></a>Exemple

```json
{
    "name": "PersonCosmosDBTable",
    "properties": {
        "type": "DocumentDbCollection",
        "linkedServiceName": "CosmosDBLinkedService",
        "typeProperties": {
            "collectionName": "Person"
        },
        "external": true,
        "availability": {
            "frequency": "Day",
            "interval": 1
        }
    }
}
```
Pour plus d’informations, consultez l’article sur le [connecteur Azure Cosmos DB](data-factory-azure-documentdb-connector.md#dataset-properties).

### <a name="azure-cosmos-db-collection-source-in-copy-activity"></a>Source de la collection Azure Cosmos DB dans l’activité de copie
Si vous copiez des données à partir d’une base de données Azure Cosmos, définissez hello **type de source de** Hello activité de copie trop**DocumentDbCollectionSource**et spécifiez les propriétés Bonjour suivantes **source** section :


| **Propriété** | **Description** | **Valeurs autorisées** | **Obligatoire** |
| --- | --- | --- | --- |
| query |Spécifier les données de tooread requête hello. |Chaîne de requête prise en charge par Azure Cosmos DB. <br/><br/>Exemple : `SELECT c.BusinessEntityID, c.PersonType, c.NameStyle, c.Title, c.Name.First AS FirstName, c.Name.Last AS LastName, c.Suffix, c.EmailPromotion FROM c WHERE c.ModifiedDate > \"2009-01-01T00:00:00\"` |Non <br/><br/>Si ce n’est pas spécifié, hello instruction SQL exécutée :`select <columns defined in structure> from mycollection` |
| nestingSeparator |Tooindicate caractère spécial qui hello document est imbriquée. |Tout caractère. <br/><br/>Azure Cosmos DB est une banque NoSQL de documents JSON, où les structures imbriquées sont autorisées. Azure Data Factory permet de hiérarchie de toodenote utilisateur via nestingSeparator, qui est «. » Bonjour exemples ci-dessus. Avec séparateur de hello, activité de copie hello génère un objet de « Name » hello avec des éléments de trois enfants too"Name.First première, intermédiaire et dernière, en fonction », « Name.Middle » et « Name.Last « Bonjour de définition de table. |Non |

#### <a name="example"></a>Exemple

```json
{
    "name": "DocDbToBlobPipeline",
    "properties": {
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "DocumentDbCollectionSource",
                    "query": "SELECT Person.Id, Person.Name.First AS FirstName, Person.Name.Middle as MiddleName, Person.Name.Last AS LastName FROM Person",
                    "nestingSeparator": "."
                },
                "sink": {
                    "type": "BlobSink",
                    "blobWriterAddHeader": true,
                    "writeBatchSize": 1000,
                    "writeBatchTimeout": "00:00:59"
                }
            },
            "inputs": [{
                "name": "PersonCosmosDBTable"
            }],
            "outputs": [{
                "name": "PersonBlobTableOut"
            }],
            "policy": {
                "concurrency": 1
            },
            "name": "CopyFromCosmosDbToBlob"
        }],
        "start": "2016-04-01T00:00:00",
        "end": "2016-04-02T00:00:00"
    }
}
```

### <a name="azure-cosmos-db-collection-sink-in-copy-activity"></a>Récepteur de collection Azure Cosmos DB dans l’activité de copie
Si vous copiez des données tooAzure Cosmos DB, la valeur hello **type de récepteur** Hello activité de copie trop**DocumentDbCollectionSink**et spécifiez les propriétés Bonjour suivantes **récepteur**section :

| **Propriété** | **Description** | **Valeurs autorisées** | **Obligatoire** |
| --- | --- | --- | --- |
| nestingSeparator |Un caractère spécial dans tooindicate de nom hello source colonne imbriquées de document est nécessaire. <br/><br/>Par exemple ci-dessus : `Name.First` dans la sortie de hello table génère hello suivant structure JSON dans le document de base de données Cosmos hello :<br/><br/>"Name": {<br/>    "First": "John"<br/>}, |Caractère utilisé tooseparate des niveaux d’imbrication.<br/><br/>La valeur par défaut est `.` (point). |Caractère utilisé tooseparate des niveaux d’imbrication. <br/><br/>La valeur par défaut est `.` (point). |
| writeBatchSize |Nombre de parallèle demandes documents toocreate de service de base de données Cosmos tooAzure.<br/><br/>Vous pouvez affiner les performances des hello lors de la copie des données à partir de base de données Azure Cosmos à l’aide de cette propriété. Vous pouvez vous attendre de meilleures performances lorsque vous augmentez la valeur writeBatchSize, car plusieurs demandes parallèles tooAzure Cosmos DB sont envoyés. Toutefois, vous devez tooavoid la limitation peut lever de message d’erreur hello : « Requête taux est grand ».<br/><br/>Une limitation dépend de divers facteurs, dont la taille des documents, le nombre de termes qu’ils contiennent, la stratégie d’indexation de la collection cible, etc. Pour les opérations de copie, vous pouvez utiliser la plupart des débit disponible à une meilleure hello de toohave de collection (par exemple, S3) (2 500 demande unités par seconde). |Entier  |Non (valeur par défaut : 5) |
| writeBatchTimeout |Temps d’attente pour hello opération toocomplete avant d’expirer. |intervalle de temps<br/><br/> Exemple : « 00:30:00 » (30 minutes). |Non |

#### <a name="example"></a>Exemple

```json
{
    "name": "BlobToDocDbPipeline",
    "properties": {
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "BlobSource"
                },
                "sink": {
                    "type": "DocumentDbCollectionSink",
                    "nestingSeparator": ".",
                    "writeBatchSize": 2,
                    "writeBatchTimeout": "00:00:00"
                },
                "translator": {
                    "type": "TabularTranslator",
                    "ColumnMappings": "FirstName: Name.First, MiddleName: Name.Middle, LastName: Name.Last, BusinessEntityID: BusinessEntityID, PersonType: PersonType, NameStyle: NameStyle, title: aaaTitle, Suffix: Suffix"
                }
            },
            "inputs": [{
                "name": "PersonBlobTableIn"
            }],
            "outputs": [{
                "name": "PersonCosmosDbTableOut"
            }],
            "policy": {
                "concurrency": 1
            },
            "name": "CopyFromBlobToCosmosDb"
        }],
        "start": "2016-04-14T00:00:00",
        "end": "2016-04-15T00:00:00"
    }
}
```

Pour plus d’informations, consultez l’article sur le [connecteur Azure Cosmos DB](data-factory-azure-documentdb-connector.md#copy-activity-properties).

## <a name="azure-sql-database"></a>Base de données SQL Azure

### <a name="linked-service"></a>Service lié
le service ensemble hello lié toodefine une base de données SQL Azure **type** Hello service lié trop**AzureSqlDatabase**et spécifiez les propriétés Bonjour suivantes **typeProperties**section :  

| Propriété | Description | Requis |
| --- | --- | --- |
| connectionString |Spécifiez les informations nécessaires d’instance de base de données SQL Azure tooconnect toohello pour la propriété connectionString de hello. |Oui |

#### <a name="example"></a>Exemple
```json
{
    "name": "AzureSqlLinkedService",
    "properties": {
        "type": "AzureSqlDatabase",
        "typeProperties": {
            "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
        }
    }
}
```

Pour plus d’informations, consultez l’article [Azure SQL connector (connecteur Azure SQL)](data-factory-azure-sql-connector.md#linked-service-properties). 

### <a name="dataset"></a>Jeu de données
toodefine un jeu de données de base de données SQL Azure, jeu hello **type** du jeu de données hello trop**AzureSqlTable**et spécifiez hello propriétés Bonjour suivantes **typeProperties** section : 

| Propriété | Description | Requis |
| --- | --- | --- |
| TableName |Nom de la table de hello ou la vue d’instance de base de données SQL Azure hello service lié fait référence à. |Oui |

#### <a name="example"></a>Exemple

```json
{
    "name": "AzureSqlInput",
    "properties": {
        "type": "AzureSqlTable",
        "linkedServiceName": "AzureSqlLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
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
Pour plus d’informations, consultez l’article [Azure SQL connector (connecteur Azure SQL)](data-factory-azure-sql-connector.md#dataset-properties). 

### <a name="sql-source-in-copy-activity"></a>Source SQL dans l’activité de copie
Si vous copiez des données à partir d’une base de données SQL Azure, la valeur hello **type de source de** Hello activité de copie trop**SqlSource**et spécifiez les propriétés Bonjour suivantes **source** section :


| Propriété | Description | Valeurs autorisées | Requis |
| --- | --- | --- | --- |
| SqlReaderQuery |Utiliser des données tooread hello requête personnalisée. |Chaîne de requête SQL. Exemple : `select * from MyTable`. |Non |
| sqlReaderStoredProcedureName |Nom de hello procédure stockée qui lit les données à partir de la table de source de hello. |Nom de hello procédure stockée. |Non |
| storedProcedureParameters |Pourquoi les paramètres de procédure stockée. |Paires nom/valeur. Noms et la casse des paramètres doivent correspondre à des noms de hello et la casse des paramètres de la procédure stockée hello. |Non |

#### <a name="example"></a>Exemple

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "AzureSQLtoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureSQLInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "SqlSource",
                    "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```
Pour plus d’informations, consultez l’article [Azure SQL connector (connecteur Azure SQL)](data-factory-azure-sql-connector.md#copy-activity-properties). 

### <a name="sql-sink-in-copy-activity"></a>Récepteur SQL dans l’activité de copie
Si vous copiez des données tooAzure base de données SQL, la valeur hello **type de récepteur** Hello activité de copie trop**SqlSink**et spécifiez les propriétés Bonjour suivantes **récepteur** section :

| Propriété | Description | Valeurs autorisées | Requis |
| --- | --- | --- | --- |
| writeBatchTimeout |Temps d’attente pour hello lot insert opération toocomplete avant d’expirer. |intervalle de temps<br/><br/> Exemple : « 00:30:00 » (30 minutes). |Non |
| writeBatchSize |Insère des données dans une table SQL de hello lorsque la taille de mémoire tampon de hello atteint la valeur writeBatchSize. |Nombre entier (nombre de lignes) |Non (valeur par défaut : 10000) |
| sqlWriterCleanupScript |Spécifier une requête pour l’activité de copie tooexecute telles que les données d’un secteur spécifique sont nettoyées. |Une instruction de requête. |Non |
| sliceIdentifierColumnName |Spécifiez un nom de colonne pour l’activité de copie toofill avec l’identificateur de secteur généré automatiquement, qui est utilisé tooclean des données d’un secteur spécifique quand réexécutée. |Nom d’une colonne avec le type de données binary(32). |Non |
| sqlWriterStoredProcedureName |Nom de hello procédure stockée que les données upserts (mises à jour/insertion) dans la table cible hello. |Nom de hello procédure stockée. |Non |
| storedProcedureParameters |Pourquoi les paramètres de procédure stockée. |Paires nom/valeur. Noms et la casse des paramètres doivent correspondre à des noms de hello et la casse des paramètres de la procédure stockée hello. |Non |
| sqlWriterTableType |Spécifiez un toobe de nom de type de table utilisée dans la procédure stockée hello. Activité de copie rend les données de hello déplacées disponibles dans une table temporaire avec ce type de table. Code de procédure stockée puis de fusionner des données hello copiées avec les données existantes. |Nom de type de table. |Non |

#### <a name="example"></a>Exemple

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoSQL",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "AzureSqlOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "BlobSource",
                    "blobColumnSeparators": ","
                },
                "sink": {
                    "type": "SqlSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

Pour plus d’informations, consultez l’article [Azure SQL connector (connecteur Azure SQL)](data-factory-azure-sql-connector.md#copy-activity-properties). 

## <a name="azure-sql-data-warehouse"></a>Azure SQL Data Warehouse

### <a name="linked-service"></a>Service lié
le service ensemble hello lié toodefine un entrepôt de données SQL Azure **type** Hello service lié trop**AzureSqlDW**et spécifiez les propriétés Bonjour suivantes **typeProperties**section :  

| Propriété | Description | Requis |
| --- | --- | --- |
| connectionString |Spécifiez les informations nécessaires d’instance d’Azure SQL Data Warehouse tooconnect toohello pour la propriété connectionString de hello. |Oui |



#### <a name="example"></a>Exemple

```json
{
    "name": "AzureSqlDWLinkedService",
    "properties": {
        "type": "AzureSqlDW",
        "typeProperties": {
            "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
        }
    }
}
```

Pour plus d’informations, consultez l’article [Azure SQL Data Warehouse connector (connecteur Azure SQL Data Warehouse)](data-factory-azure-sql-data-warehouse-connector.md#linked-service-properties). 

### <a name="dataset"></a>Jeu de données
toodefine un jeu de données Azure SQL Data Warehouse, jeu hello **type** du jeu de données hello trop**AzureSqlDWTable**et spécifiez hello propriétés Bonjour suivantes **typeProperties**section : 

| Propriété | Description | Requis |
| --- | --- | --- |
| TableName |Nom de la table de hello ou une vue dans la base de données Azure SQL Data Warehouse hello qui hello service lié fait référence à. |Oui |

#### <a name="example"></a>Exemple

```json
{
    "name": "AzureSqlDWInput",
    "properties": {
    "type": "AzureSqlDWTable",
        "linkedServiceName": "AzureSqlDWLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
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

Pour plus d’informations, consultez l’article [Azure SQL Data Warehouse connector (connecteur Azure SQL Data Warehouse)](data-factory-azure-sql-data-warehouse-connector.md#dataset-properties). 

### <a name="sql-dw-source-in-copy-activity"></a>Source SQL DW dans l’activité de copie
Si vous copiez des données à partir de l’entrepôt de données SQL Azure, la valeur hello **type de source de** Hello activité de copie trop**SqlDWSource**et spécifiez les propriétés Bonjour suivantes **source**section :


| Propriété | Description | Valeurs autorisées | Requis |
| --- | --- | --- | --- |
| SqlReaderQuery |Utiliser des données tooread hello requête personnalisée. |Chaîne de requête SQL. Par exemple : `select * from MyTable`. |Non |
| sqlReaderStoredProcedureName |Nom de hello procédure stockée qui lit les données à partir de la table de source de hello. |Nom de hello procédure stockée. |Non |
| storedProcedureParameters |Pourquoi les paramètres de procédure stockée. |Paires nom/valeur. Noms et la casse des paramètres doivent correspondre à des noms de hello et la casse des paramètres de la procédure stockée hello. |Non |

#### <a name="example"></a>Exemple

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "AzureSQLDWtoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureSqlDWInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "SqlDWSource",
                    "sqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

Pour plus d’informations, consultez l’article [Azure SQL Data Warehouse connector (connecteur Azure SQL Data Warehouse)](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties). 

### <a name="sql-dw-sink-in-copy-activity"></a>Récepteur SQL DW dans l’activité de copie
Si vous copiez des données tooAzure SQL Data Warehouse, définissez hello **type de récepteur** Hello activité de copie trop**SqlDWSink**et spécifiez les propriétés Bonjour suivantes **récepteur** section :

| Propriété | Description | Valeurs autorisées | Requis |
| --- | --- | --- | --- |
| sqlWriterCleanupScript |Spécifier une requête pour l’activité de copie tooexecute telles que les données d’un secteur spécifique sont nettoyées. |Une instruction de requête. |Non |
| allowPolyBase |Indique si toouse PolyBase (le cas échéant) au lieu de mécanisme BULKINSERT. <br/><br/> **À l’aide de PolyBase est hello recommandé la façon dont les données tooload dans SQL Data Warehouse.** |true <br/>False (valeur par défaut) |Non |
| polyBaseSettings |Un groupe de propriétés qui peuvent être spécifiés lorsque hello **allowPolybase** propriété a la valeur trop**true**. |&nbsp; |Non |
| rejectValue |Spécifie le nombre de hello ou un pourcentage de lignes peut être rejetée avant l’échec de la requête de hello. <br/><br/>En savoir plus sur de PolyBase hello rejettent options Bonjour **Arguments** section de [CREATE EXTERNAL TABLE (Transact-SQL)](https://msdn.microsoft.com/library/dn935021.aspx) rubrique. |0 (par défaut), 1, 2, … |Non |
| rejectType |Spécifie si l’option de rejectValue hello est spécifiée comme une valeur littérale ou pourcentage. |Value (par défaut), Percentage |Non |
| rejectSampleValue |Détermine le nombre hello de lignes tooretrieve avant hello PolyBase recalcule le pourcentage de hello de lignes rejetées. |1, 2, … |Oui, si le **rejectType** est **percentage** |
| useTypeDefault |Spécifie comment toohandle manque des valeurs dans le fichiers texte délimités lorsque PolyBase récupère les données à partir du fichier de texte hello.<br/><br/>En savoir plus sur cette propriété à partir de la section Arguments hello [CREATE EXTERNAL FILE FORMAT (Transact-SQL)](https://msdn.microsoft.com/library/dn935026.aspx). |True, False (par défaut) |Non |
| writeBatchSize |Insère des données dans une table SQL de hello lorsque la taille de mémoire tampon de hello atteint la valeur writeBatchSize |Nombre entier (nombre de lignes) |Non (valeur par défaut : 10000) |
| writeBatchTimeout |Temps d’attente pour hello lot insert opération toocomplete avant d’expirer. |intervalle de temps<br/><br/> Exemple : « 00:30:00 » (30 minutes). |Non |

#### <a name="example"></a>Exemple

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoSQLDW",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "AzureSqlDWOutput"
            }],
            "typeProperties": {
                "source": {
                "type": "BlobSource",
                    "blobColumnSeparators": ","
                },
                "sink": {
                    "type": "SqlDWSink",
                    "allowPolyBase": true
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

Pour plus d’informations, consultez l’article [Azure SQL Data Warehouse connector (connecteur Azure SQL Data Warehouse)](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties). 

## <a name="azure-search"></a>Recherche Azure

### <a name="linked-service"></a>Service lié
le service ensemble hello lié toodefine un indexeur Azure Search **type** Hello service lié trop**AzureSearch**et spécifiez les propriétés Bonjour suivantes **typeProperties** section :  

| Propriété | Description | Requis |
| -------- | ----------- | -------- |
| url | URL de hello service Azure Search. | Oui |
| key | Clé d’administration pour hello service Azure Search. | Oui |

#### <a name="example"></a>Exemple

```json
{
    "name": "AzureSearchLinkedService",
    "properties": {
        "type": "AzureSearch",
        "typeProperties": {
            "url": "https://<service>.search.windows.net",
            "key": "<AdminKey>"
        }
    }
}
```

Pour plus d’informations, consultez l’article [Connecteur Recherche Azure](data-factory-azure-search-connector.md#linked-service-properties).

### <a name="dataset"></a>Jeu de données
toodefine un jeu de données Azure Search, jeu hello **type** du jeu de données hello trop**AzureSearchIndex**et spécifiez hello propriétés Bonjour suivantes **typeProperties** section : 

| Propriété | Description | Requis |
| -------- | ----------- | -------- |
| type | propriété de type Hello doit être définie trop**AzureSearchIndex**.| Oui |
| indexName | Nom de l’index de recherche de Azure hello. Fabrique de données ne crée pas d’index de hello. index de Hello doit exister dans Azure Search. | Oui |

#### <a name="example"></a>Exemple

```json
{
    "name": "AzureSearchIndexDataset",
    "properties": {
        "type": "AzureSearchIndex",
        "linkedServiceName": "AzureSearchLinkedService",
        "typeProperties": {
            "indexName": "products"
        },
        "availability": {
            "frequency": "Minute",
            "interval": 15
        }
    }
}
```

Pour plus d’informations, consultez l’article [Connecteur Recherche Azure](data-factory-azure-search-connector.md#dataset-properties).

### <a name="azure-search-index-sink-in-copy-activity"></a>Récepteur Index Recherche Azure dans l’activité de copie
Si vous copiez des index de recherche de Azure tooan de données, la valeur hello **type de récepteur** Hello activité de copie trop**AzureSearchIndexSink**et spécifiez les propriétés Bonjour suivantes **récepteur**section :

| Propriété | Description | Valeurs autorisées | Requis |
| -------- | ----------- | -------------- | -------- |
| WriteBehavior | Spécifie si toomerge ou remplacer un document existe déjà dans l’index de hello. | Merge (par défaut)<br/>Télécharger| Non |
| writeBatchSize | Télécharge des données dans l’index de recherche de Azure hello lorsque la taille de mémoire tampon de hello atteint la valeur writeBatchSize. | 1 too1, 000. Valeur par défaut : 1 000. | Non |

#### <a name="example"></a>Exemple

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "SqlServertoAzureSearchIndex",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": " SqlServerInput"
            }],
            "outputs": [{
                "name": "AzureSearchIndexDataset"
            }],
            "typeProperties": {
                "source": {
                    "type": "SqlSource",
                    "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "AzureSearchIndexSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

Pour plus d’informations, consultez l’article [Connecteur Recherche Azure](data-factory-azure-search-connector.md#copy-activity-properties).

## <a name="azure-table-storage"></a>Stockage de table Azure

### <a name="linked-service"></a>Service lié
Il existe deux types de services liés : les services liés de stockage Azure et les services liés SAP de stockage Azure.

#### <a name="azure-storage-linked-service"></a>Service lié Stockage Azure
toolink votre fabrique de données tooa compte stockage Azure à l’aide de hello **clé de compte**, créez un service lié Azure Storage. le service ensemble hello lié toodefine un stockage Azure **type** Hello service lié trop**AzureStorage**. Ensuite, vous pouvez spécifier les propriétés Bonjour suivantes **typeProperties** section :  

| Propriété | Description | Requis |
|:--- |:--- |:--- |
| type |propriété de type Hello doit indiquer : **AzureStorage** |Oui |
| connectionString |Spécifiez les informations nécessaires tooconnect tooAzure stockage pour la propriété connectionString de hello. |Oui |

**Exemple :**  

```json
{  
    "name": "StorageLinkedService",  
    "properties": {  
        "type": "AzureStorage",  
        "typeProperties": {  
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"  
        }  
    }  
}  
```

#### <a name="azure-storage-sas-linked-service"></a>Service lié SAP de stockage Azure
Hello SAS de stockage Azure lié service vous permet de toolink une fabrique de données Azure tooan compte de stockage Azure à l’aide d’une Signature d’accès partagé (SAS). Il fournit des fabrique de données hello avec l’accès restreint/limitées dans le temps de tooall/spécifiques des ressources (objet blob/conteneur) dans le stockage hello. toolink votre fabrique de données tooa compte stockage Azure à l’aide de Signature d’accès partagé, créez un service de SAS de stockage Azure lié. le service ensemble hello lié toodefine un SAS de stockage Azure **type** Hello service lié trop**AzureStorageSas**. Ensuite, vous pouvez spécifier les propriétés Bonjour suivantes **typeProperties** section :   

| Propriété | Description | Requis |
|:--- |:--- |:--- |
| type |propriété de type Hello doit indiquer : **AzureStorageSas** |Oui |
| sasUri |Spécifier des ressources de stockage Azure toohello URI de Signature d’accès partagé comme objet blob, conteneur ou une table. |Oui |

**Exemple :**

```json
{  
    "name": "StorageSasLinkedService",  
    "properties": {  
        "type": "AzureStorageSas",  
        "typeProperties": {  
            "sasUri": "<storageUri>?<sasToken>"   
        }  
    }  
}  
```

Pour plus d’informations sur ces services liés, consultez l’article [Connecteur de stockage Table Azure](data-factory-azure-table-connector.md#linked-service-properties). 

### <a name="dataset"></a>Jeu de données
toodefine un jeu de données de Table Azure, jeu hello **type** du jeu de données hello trop**AzureTable**et spécifiez hello propriétés Bonjour suivantes **typeProperties** section : 

| Propriété | Description | Requis |
| --- | --- | --- |
| TableName |Nom de table hello dans l’instance de base de données de Table Azure hello ce service lié fait référence à. |Oui. Lorsqu’un nom de table est spécifié sans un azureTableSourceQuery, tous les enregistrements à partir de la table de hello sont copiés toohello destination. Si un azureTableSourceQuery est également spécifiée, les enregistrements de la table hello qui répond aux requêtes de hello sont copiés toohello destination. |

#### <a name="example"></a>Exemple

```json
{
    "name": "AzureTableInput",
    "properties": {
        "type": "AzureTable",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
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

Pour plus d’informations sur ces services liés, consultez l’article [Connecteur de stockage Table Azure)](data-factory-azure-table-connector.md#dataset-properties). 

### <a name="azure-table-source-in-copy-activity"></a>Source Table Azure dans l’activité de copie
Si vous copiez des données depuis le stockage de Table Azure, la valeur hello **type de source de** Hello activité de copie trop**AzureTableSource**et spécifiez les propriétés Bonjour suivantes **source**section :

| Propriété | Description | Valeurs autorisées | Requis |
| --- | --- | --- | --- |
| AzureTableSourceQuery |Utiliser des données tooread hello requête personnalisée. |Chaîne de requête de table Azure. Consultez les exemples dans la section suivante de hello. |Non. Lorsqu’un nom de table est spécifié sans un azureTableSourceQuery, tous les enregistrements à partir de la table de hello sont copiés toohello destination. Si un azureTableSourceQuery est également spécifiée, les enregistrements de la table hello qui répond aux requêtes de hello sont copiés toohello destination. |
| azureTableSourceIgnoreTableNotFound |Indiquer si exception de hello avale de table n’existe pas. |TRUE<br/>FALSE |Non |

#### <a name="example"></a>Exemple

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "AzureTabletoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureTableInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "AzureTableSource",
                    "AzureTableSourceQuery": "PartitionKey eq 'DefaultPartitionKey'"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

Pour plus d’informations sur ces services liés, consultez l’article [Connecteur de stockage Table Azure)](data-factory-azure-table-connector.md#copy-activity-properties). 

### <a name="azure-table-sink-in-copy-activity"></a>Récepteur Table Azure dans l’activité de copie
Si vous copiez des données tooAzure le stockage de Table, la valeur hello **type de récepteur** Hello activité de copie trop**AzureTableSink**et spécifiez les propriétés Bonjour suivantes **récepteur** section :

| Propriété | Description | Valeurs autorisées | Requis |
| --- | --- | --- | --- |
| azureTableDefaultPartitionKeyValue |Valeur par défaut partition clé qui peut être utilisé par le récepteur de hello. |Valeur de chaîne. |Non |
| azureTablePartitionKeyName |Spécifiez le nom de colonne hello dont les valeurs sont utilisées comme clés de partition. Si non spécifié, AzureTableDefaultPartitionKeyValue est utilisé comme clé de partition hello. |Nom de colonne. |Non |
| azureTableRowKeyName |Spécifiez le nom de colonne hello dont les valeurs de colonne sont utilisées comme clé de ligne. Si aucune valeur n'est spécifiée, un GUID est utilisé pour chaque ligne. |Nom de colonne. |Non |
| azureTableInsertType |Hello mode tooinsert les données dans Azure table.<br/><br/>Cette propriété contrôle si les lignes existantes dans la table de sortie hello avec les clés de partition et de ligne correspondantes ont leurs valeurs remplacé ou fusionnées. <br/><br/>toolearn sur le fonctionnement de ces paramètres (fusion et remplacement), consultez [insertion ou l’entité de fusion](https://msdn.microsoft.com/library/azure/hh452241.aspx) et [insérer ou remplacer une entité](https://msdn.microsoft.com/library/azure/hh452242.aspx) rubriques. <br/><br> Ce paramètre s’applique au niveau de ligne hello, pas de niveau de table d’hello, et aucune de ces options supprime des lignes dans la table de sortie hello qui n’existent pas dans l’entrée de hello. |fusionner (par défaut)<br/>remplacer |Non |
| writeBatchSize |Insère des données dans hello table Azure quand la valeur de hello writeBatchSize ou writeBatchTimeout est atteinte. |Nombre entier (nombre de lignes) |Non (valeur par défaut : 10000) |
| writeBatchTimeout |Insère des données dans hello table Azure quand la valeur de hello writeBatchSize ou writeBatchTimeout est atteinte |intervalle de temps<br/><br/>Exemple : « 00: 20:00 » (20 minutes) |Non (le délai d’expiration de valeur par défaut toostorage client par défaut la valeur 90 s) |

#### <a name="example"></a>Exemple

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoTable",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "AzureTableOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "BlobSource"
                },
                "sink": {
                    "type": "AzureTableSink",
                    "writeBatchSize": 100,
                    "writeBatchTimeout": "01:00:00"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```
Pour plus d’informations sur ces services liés, consultez l’article [Connecteur de stockage Table Azure)](data-factory-azure-table-connector.md#copy-activity-properties). 

## <a name="amazon-redshift"></a>Amazon Redshift

### <a name="linked-service"></a>Service lié
toodefine un Amazon Redshift le service ensemble hello lié **type** Hello service lié trop**AmazonRedshift**et spécifiez les propriétés Bonjour suivantes **typeProperties**section :  

| Propriété | Description | Requis |
| --- | --- | --- |
| server |Nom hôte ou adresse IP du serveur d’Amazon Redshift hello. |Oui |
| port |nombre de Hello de port TCP hello hello Amazon Redshift serveur utilise toolisten pour les connexions client. |Non, valeur par défaut : 5439 |
| database |Nom de la base de données Amazon Redshift hello. |Oui |
| username |Nom d’utilisateur qui a la base de données access toohello. |Oui |
| password |Mot de passe pour le compte d’utilisateur hello. |Oui |

#### <a name="example"></a>Exemple

```json
{
    "name": "AmazonRedshiftLinkedService",
    "properties": {
        "type": "AmazonRedshift",
        "typeProperties": {
            "server": "<Amazon Redshift host name or IP address>",
            "port": 5439,
            "database": "<database name>",
            "username": "user",
            "password": "password"
        }
    }
}
```

Pour plus d’informations, consultez l’article [Amazon Redshift connector (connecteur Amazon Redshift)](#data-factory-amazon-redshift-connector.md#linked-service-properties). 

### <a name="dataset"></a>Jeu de données
toodefine un jeu de données Amazon Redshift, jeu hello **type** du jeu de données hello trop**RelationalTable**et spécifiez hello propriétés Bonjour suivantes **typeProperties** section : 

| Propriété | Description | Requis |
| --- | --- | --- |
| TableName |Nom de table hello dans la base de données Amazon Redshift hello ce service lié fait référence à. |Non (si la **requête** de **RelationalSource** est spécifiée) |


#### <a name="example"></a>Exemple

```json
{
    "name": "AmazonRedshiftInputDataset",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "AmazonRedshiftLinkedService",
        "typeProperties": {
            "tableName": "<Table name>"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```
Pour plus d’informations, consultez l’article [Amazon Redshift connector (connecteur Amazon Redshift)](#data-factory-amazon-redshift-connector.md#dataset-properties).

### <a name="relational-source-in-copy-activity"></a>Source relationnelle dans l’activité de copie 
Si vous copiez des données à partir d’Amazon Redshift, la valeur hello **type de source de** Hello activité de copie trop**RelationalSource**et spécifiez les propriétés Bonjour suivantes **source** section :

| Propriété | Description | Valeurs autorisées | Requis |
| --- | --- | --- | --- |
| query |Utiliser des données tooread hello requête personnalisée. |Chaîne de requête SQL. Par exemple : `select * from MyTable`. |Non (si **tableName** de **dataset** est spécifiée) |

#### <a name="example"></a>Exemple

```json
{
    "name": "CopyAmazonRedshiftToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "$$Text.Format('select * from MyTable where timestamp >= \\'{0:yyyy-MM-ddTHH:mm:ss}\\' AND timestamp < \\'{1:yyyy-MM-ddTHH:mm:ss}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "AmazonRedshiftInputDataset"
            }],
            "outputs": [{
                "name": "AzureBlobOutputDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "AmazonRedshiftToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```
Pour plus d’informations, consultez l’article [Amazon Redshift connector (connecteur Amazon Redshift)](#data-factory-amazon-redshift-connector.md#copy-activity-properties).

## <a name="ibm-db2"></a>IBM DB2

### <a name="linked-service"></a>Service lié
toodefine un IBM DB2 lié service, jeu hello **type** Hello service lié trop**OnPremisesDB2**et spécifiez les propriétés Bonjour suivantes **typeProperties** section :  

| Propriété | Description | Requis |
| --- | --- | --- |
| server |Nom du serveur de hello DB2. |Oui |
| database |Nom de la base de données hello DB2. |Oui |
| schema |Nom de schéma hello hello de base de données. nom du schéma Hello respecte la casse. |Non |
| authenticationType |Type d’authentification utilisé tooconnect toohello base de données DB2. Les valeurs possibles sont : Anonyme, De base et Windows. |Oui |
| username |Spécifiez le nom d'utilisateur si vous utilisez l'authentification de base ou Windows. |Non |
| password |Spécifiez le mot de passe de compte d’utilisateur hello que vous avez spécifié pour le nom d’utilisateur hello. |Non |
| gatewayName |Nom de passerelle hello hello service Data Factory doit utiliser la base de données DB2 tooconnect toohello local. |Oui |

#### <a name="example"></a>Exemple
```json
{
    "name": "OnPremDb2LinkedService",
    "properties": {
        "type": "OnPremisesDb2",
        "typeProperties": {
            "server": "<server>",
            "database": "<database>",
            "schema": "<schema>",
            "authenticationType": "<authentication type>",
            "username": "<username>",
            "password": "<password>",
            "gatewayName": "<gatewayName>"
        }
    }
}
```
Pour plus d’informations, consultez l’article [IBM DB2 connector (connecteur IBM DB2)](#data-factory-onprem-db2-connector.md#linked-service-properties).

### <a name="dataset"></a>Jeu de données
dataset toodefine DB2, jeu hello **type** du jeu de données hello trop**RelationalTable**et spécifiez hello propriétés Bonjour suivantes **typeProperties** section :

| Propriété | Description | Requis |
| --- | --- | --- |
| TableName |Nom de table hello dans l’instance de base de données DB2 hello ce service lié fait référence à. Hello tableName respecte la casse. |Non (si la **requête** de **RelationalSource** est spécifiée) 

#### <a name="example"></a>Exemple
```json
{
    "name": "Db2DataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremDb2LinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
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

Pour plus d’informations, consultez l’article [IBM DB2 connector (connecteur IBM DB2)](#data-factory-onprem-db2-connector.md#dataset-properties).

### <a name="relational-source-in-copy-activity"></a>Source relationnelle dans l’activité de copie
Si vous copiez des données à partir d’IBM DB2, la valeur hello **type de source de** Hello activité de copie trop**RelationalSource**et spécifiez les propriétés Bonjour suivantes **source** section :


| Propriété | Description | Valeurs autorisées | Requis |
| --- | --- | --- | --- |
| query |Utiliser des données tooread hello requête personnalisée. |Chaîne de requête SQL. Par exemple : `"query": "select * from "MySchema"."MyTable""`. |Non (si **tableName** de **dataset** est spécifiée) |

#### <a name="example"></a>Exemple
```json
{
    "name": "CopyDb2ToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "select * from \"Orders\""
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "inputs": [{
                "name": "Db2DataSet"
            }],
            "outputs": [{
                "name": "AzureBlobDb2DataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "Db2ToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```
Pour plus d’informations, consultez l’article [IBM DB2 connector (connecteur IBM DB2)](#data-factory-onprem-db2-connector.md#copy-activity-properties).

## <a name="mysql"></a>MySQL

### <a name="linked-service"></a>Service lié
toodefine un MySQL le service ensemble hello lié **type** Hello service lié trop**OnPremisesMySql**et spécifiez les propriétés Bonjour suivantes **typeProperties** section :  

| Propriété | Description | Requis |
| --- | --- | --- |
| server |Nom du serveur de MySQL hello. |Oui |
| database |Nom de la base de données MySQL hello. |Oui |
| schema |Nom de schéma hello hello de base de données. |Non |
| authenticationType |Type d’authentification utilisé tooconnect toohello base de données MySQL. Les valeurs possibles sont les suivantes : `Basic`. |Oui |
| username |Spécifiez la base de données utilisateur nom tooconnect toohello MySQL. |Oui |
| password |Spécifiez le mot de passe de compte d’utilisateur hello spécifié. |Oui |
| gatewayName |Nom de passerelle hello hello service Data Factory doit utiliser la base de données MySQL tooconnect toohello local. |Oui |

#### <a name="example"></a>Exemple

```json
{
    "name": "OnPremMySqlLinkedService",
    "properties": {
        "type": "OnPremisesMySql",
        "typeProperties": {
            "server": "<server name>",
            "database": "<database name>",
            "schema": "<schema name>",
            "authenticationType": "<authentication type>",
            "userName": "<user name>",
            "password": "<password>",
            "gatewayName": "<gateway>"
        }
    }
}
```

Pour plus d’informations, consultez l’article [MySQL connector (connecteur MySQL)](data-factory-onprem-mysql-connector.md#linked-service-properties). 

### <a name="dataset"></a>Jeu de données
toodefine un jeu de données MySQL, jeu hello **type** du jeu de données hello trop**RelationalTable**et spécifiez hello propriétés Bonjour suivantes **typeProperties** section : 

| Propriété | Description | Requis |
| --- | --- | --- |
| TableName |Nom de table hello Bonjour instance de base de données MySQL service lié fait référence à. |Non (si la **requête** de **RelationalSource** est spécifiée) |

#### <a name="example"></a>Exemple

```json
{
    "name": "MySqlDataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremMySqlLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
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
Pour plus d’informations, consultez l’article [MySQL connector (connecteur MySQL)](data-factory-onprem-mysql-connector.md#dataset-properties). 

### <a name="relational-source-in-copy-activity"></a>Source relationnelle dans l’activité de copie
Si vous copiez des données à partir d’une base de données MySQL, la valeur hello **type de source de** Hello activité de copie trop**RelationalSource**et spécifiez les propriétés Bonjour suivantes **source** section :


| Propriété | Description | Valeurs autorisées | Requis |
| --- | --- | --- | --- |
| query |Utiliser des données tooread hello requête personnalisée. |Chaîne de requête SQL. Par exemple : `select * from MyTable`. |Non (si **tableName** de **dataset** est spécifiée) |


#### <a name="example"></a>Exemple
```json
{
    "name": "CopyMySqlToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "$$Text.Format('select * from MyTable where timestamp >= \\'{0:yyyy-MM-ddTHH:mm:ss}\\' AND timestamp < \\'{1:yyyy-MM-ddTHH:mm:ss}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "MySqlDataSet"
            }],
            "outputs": [{
                "name": "AzureBlobMySqlDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "MySqlToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```

Pour plus d’informations, consultez l’article [MySQL connector (connecteur MySQL)](data-factory-onprem-mysql-connector.md#copy-activity-properties). 

## <a name="oracle"></a>Oracle 

### <a name="linked-service"></a>Service lié
toodefine Oracle lié service, jeu hello **type** Hello service lié trop**OnPremisesOracle**et spécifiez les propriétés Bonjour suivantes **typeProperties** section :  

| Propriété | Description | Requis |
| --- | --- | --- |
| driverType | Spécifier les données de toocopy toouse pilote à partir de / tooOracle de base de données. Valeurs autorisées : **Microsoft** ou **ODP** (par défaut). Consultez la section [Version prise en charge et installation](#supported-versions-and-installation) sur les détails du pilote. | Non |
| connectionString | Spécifiez les informations nécessaires d’instance de base de données Oracle tooconnect toohello pour la propriété connectionString de hello. | Oui |
| gatewayName | Nom de la passerelle hello qui est utilisé tooconnect toohello serveur Oracle locale |Oui |

#### <a name="example"></a>Exemple
```json
{
    "name": "OnPremisesOracleLinkedService",
    "properties": {
        "type": "OnPremisesOracle",
        "typeProperties": {
            "driverType": "Microsoft",
            "connectionString": "Host=<host>;Port=<port>;Sid=<sid>;User Id=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```

Pour plus d’informations, consultez l’article [Oracle connector (connecteur Oracle)](data-factory-onprem-oracle-connector.md#linked-service-properties).

### <a name="dataset"></a>Jeu de données
toodefine un jeu de données Oracle, set hello **type** du jeu de données hello trop**OracleTable**et spécifiez hello propriétés Bonjour suivantes **typeProperties** section : 

| Propriété | Description | Requis |
| --- | --- | --- |
| TableName |Nom de table hello Bonjour base de données Oracle hello service lié fait référence à. |Non (si **oracleReaderQuery** de **OracleSource** est spécifié) |

#### <a name="example"></a>Exemple

```json
{
    "name": "OracleInput",
    "properties": {
        "type": "OracleTable",
        "linkedServiceName": "OnPremisesOracleLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "external": true,
        "availability": {
            "offset": "01:00:00",
            "interval": "1",
            "anchorDateTime": "2016-02-27T12:00:00",
            "frequency": "Hour"
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
Pour plus d’informations, consultez l’article [Oracle connector (connecteur Oracle)](data-factory-onprem-oracle-connector.md#dataset-properties).

### <a name="oracle-source-in-copy-activity"></a>Source Oracle dans l’activité de copie
Si vous copiez des données à partir d’une base de données Oracle, la valeur hello **type de source de** Hello activité de copie trop**OracleSource**et spécifiez les propriétés Bonjour suivantes **source** section :

| Propriété | Description | Valeurs autorisées | Requis |
| --- | --- | --- | --- |
| oracleReaderQuery |Utiliser des données tooread hello requête personnalisée. |Chaîne de requête SQL. Par exemple : `select * from MyTable` <br/><br/>Si ce n’est pas spécifié, hello instruction SQL exécutée :`select * from MyTable` |Non (si **tableName** de **dataset** est spécifiée) |

#### <a name="example"></a>Exemple

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "OracletoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": " OracleInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "OracleSource",
                    "oracleReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
            "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

Pour plus d’informations, consultez l’article [Oracle connector (connecteur Oracle)](data-factory-onprem-oracle-connector.md#copy-activity-properties).

### <a name="oracle-sink-in-copy-activity"></a>Récepteur Oracle dans l’activité de copie
Si vous copiez une base de données Oracle de données tooam, définissez hello **type de récepteur** Hello activité de copie trop**OracleSink**et spécifiez les propriétés Bonjour suivantes **récepteur** section :

| Propriété | Description | Valeurs autorisées | Requis |
| --- | --- | --- | --- |
| writeBatchTimeout |Temps d’attente pour hello lot insert opération toocomplete avant d’expirer. |intervalle de temps<br/><br/> Exemple : « 00:30:00 » (30 minutes). |Non |
| writeBatchSize |Insère des données dans une table SQL de hello lorsque la taille de mémoire tampon de hello atteint la valeur writeBatchSize. |Nombre entier (nombre de lignes) |Non (valeur par défaut : 100) |
| sqlWriterCleanupScript |Spécifier une requête pour l’activité de copie tooexecute telles que les données d’un secteur spécifique sont nettoyées. |Une instruction de requête. |Non |
| sliceIdentifierColumnName |Spécifiez nom de colonne pour l’activité de copie toofill avec l’identificateur de secteur généré automatiquement, qui est utilisé tooclean des données d’un secteur spécifique quand réexécutée. |Nom d’une colonne avec le type de données binary(32). |Non |

#### <a name="example"></a>Exemple
```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-05T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoOracle",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "OracleOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "BlobSource"
                },
                "sink": {
                    "type": "OracleSink"
                }
            },
            "scheduler": {
                "frequency": "Day",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```
Pour plus d’informations, consultez l’article [Oracle connector (connecteur Oracle)](data-factory-onprem-oracle-connector.md#copy-activity-properties).

## <a name="postgresql"></a>PostgreSQL

### <a name="linked-service"></a>Service lié
toodefine un PostgreSQL le service ensemble hello lié **type** Hello service lié trop**OnPremisesPostgreSql**et spécifiez les propriétés Bonjour suivantes **typeProperties**section :  

| Propriété | Description | Requis |
| --- | --- | --- |
| server |Nom du serveur de PostgreSQL hello. |Oui |
| database |Nom de la base de données PostgreSQL hello. |Oui |
| schema |Nom de schéma hello hello de base de données. nom du schéma Hello respecte la casse. |Non |
| authenticationType |Type d’authentification utilisé tooconnect toohello base de données PostgreSQL. Les valeurs possibles sont : Anonyme, De base et Windows. |Oui |
| username |Spécifiez le nom d'utilisateur si vous utilisez l'authentification de base ou Windows. |Non |
| password |Spécifiez le mot de passe de compte d’utilisateur hello que vous avez spécifié pour le nom d’utilisateur hello. |Non |
| gatewayName |Nom de passerelle hello hello service Data Factory doit utiliser la base de données PostgreSQL tooconnect toohello local. |Oui |

#### <a name="example"></a>Exemple

```json
{
    "name": "OnPremPostgreSqlLinkedService",
    "properties": {
        "type": "OnPremisesPostgreSql",
        "typeProperties": {
            "server": "<server>",
            "database": "<database>",
            "schema": "<schema>",
            "authenticationType": "<authentication type>",
            "username": "<username>",
            "password": "<password>",
            "gatewayName": "<gatewayName>"
        }
    }
}
```
Pour plus d’informations, consultez l’article [PostgreSQL connector (connecteur PostgreSQL)](data-factory-onprem-postgresql-connector.md#linked-service-properties).

### <a name="dataset"></a>Jeu de données
toodefine un jeu de données PostgreSQL, jeu hello **type** du jeu de données hello trop**RelationalTable**et spécifiez hello propriétés Bonjour suivantes **typeProperties** section : 

| Propriété | Description | Requis |
| --- | --- | --- |
| TableName |Nom de table hello Bonjour instance de base de données PostgreSQL service lié fait référence à. Hello tableName respecte la casse. |Non (si la **requête** de **RelationalSource** est spécifiée) |

#### <a name="example"></a>Exemple
```json
{
    "name": "PostgreSqlDataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremPostgreSqlLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
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
Pour plus d’informations, consultez l’article [PostgreSQL connector (connecteur PostgreSQL)](data-factory-onprem-postgresql-connector.md#dataset-properties).

### <a name="relational-source-in-copy-activity"></a>Source relationnelle dans l’activité de copie
Si vous copiez des données à partir d’une base de données PostgreSQL, définissez hello **type de source de** Hello activité de copie trop**RelationalSource**et spécifiez les propriétés Bonjour suivantes **source**section :


| Propriété | Description | Valeurs autorisées | Requis |
| --- | --- | --- | --- |
| query |Utiliser des données tooread hello requête personnalisée. |Chaîne de requête SQL. Par exemple : "query": "select * from \"MySchema\".\"MyTable\"". |Non (si **tableName** de **dataset** est spécifiée) |

#### <a name="example"></a>Exemple

```json
{
    "name": "CopyPostgreSqlToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "select * from \"public\".\"usstates\""
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "inputs": [{
                "name": "PostgreSqlDataSet"
            }],
            "outputs": [{
                "name": "AzureBlobPostgreSqlDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "PostgreSqlToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```

Pour plus d’informations, consultez l’article [PostgreSQL connector (connecteur PostgreSQL)](data-factory-onprem-postgresql-connector.md#copy-activity-properties).

## <a name="sap-business-warehouse"></a>SAP Business Warehouse


### <a name="linked-service"></a>Service lié
toodefine une SAP Business Warehouse (BW) le service ensemble hello lié **type** Hello service lié trop**SapBw**et spécifiez les propriétés Bonjour suivantes **typeProperties**section :  

Propriété | Description | Valeurs autorisées | Requis
-------- | ----------- | -------------- | --------
server | Nom du serveur hello sur quel hello SAP BW instance réside. | string | Oui
systemNumber | Numéro de système de hello système SAP BW. | Nombre décimal à deux chiffres représenté sous forme de chaîne. | Oui
clientId | ID client du client hello Bonjour système SAP W. | Nombre décimal à trois chiffres représenté sous forme de chaîne. | Oui
username | Nom d’utilisateur de hello qui a le serveur d’accès toohello SAP | string | Oui
password | Mot de passe utilisateur de hello. | string | Oui
gatewayName | Nom de passerelle hello hello service Data Factory doit utiliser l’instance de SAP BW tooconnect toohello sur site. | string | Oui
Encryptedcredential | chaîne d’identification de Hello chiffré. | string | Non

#### <a name="example"></a>Exemple

```json
{
    "name": "SapBwLinkedService",
    "properties": {
        "type": "SapBw",
        "typeProperties": {
            "server": "<server name>",
            "systemNumber": "<system number>",
            "clientId": "<client id>",
            "username": "<SAP user>",
            "password": "<Password for SAP user>",
            "gatewayName": "<gateway name>"
        }
    }
}
```

Pour plus d’informations, consultez l’article [SAP Business Warehouse connector (connecteur SAP Business Warehouse)](data-factory-sap-business-warehouse-connector.md#linked-service-properties). 

### <a name="dataset"></a>Jeu de données
toodefine un jeu de données SAP BW, jeu hello **type** du jeu de données hello trop**RelationalTable**. Aucune propriété spécifique au type pris en charge pour le jeu de données hello SAP BW de type **RelationalTable**.  

#### <a name="example"></a>Exemple

```json
{
    "name": "SapBwDataset",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "SapBwLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```
Pour plus d’informations, consultez l’article [SAP Business Warehouse connector (connecteur SAP Business Warehouse)](data-factory-sap-business-warehouse-connector.md#dataset-properties). 

### <a name="relational-source-in-copy-activity"></a>Source relationnelle dans l’activité de copie
Si vous copiez des données à partir de SAP Business Warehouse, définissez hello **type de source de** Hello activité de copie trop**RelationalSource**et spécifiez les propriétés Bonjour suivantes **source**section :


| Propriété | Description | Valeurs autorisées | Requis |
| --- | --- | --- | --- |
| query | Spécifie les données de tooread requête hello MDX à partir de l’instance de SAP BW hello. | Requête MDX. | Oui |

#### <a name="example"></a>Exemple

```json
{
    "name": "CopySapBwToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "<MDX query for SAP BW>"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "SapBwDataset"
            }],
            "outputs": [{
                "name": "AzureBlobDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "SapBwToBlob"
        }],
        "start": "2017-03-01T18:00:00",
        "end": "2017-03-01T19:00:00"
    }
}
```

Pour plus d’informations, consultez l’article [SAP Business Warehouse connector (connecteur SAP Business Warehouse)](data-factory-sap-business-warehouse-connector.md#copy-activity-properties). 

## <a name="sap-hana"></a>SAP HANA

### <a name="linked-service"></a>Service lié
toodefine une SAP HANA le service ensemble hello lié **type** Hello service lié trop**SapHana**et spécifiez les propriétés Bonjour suivantes **typeProperties** section :  

Propriété | Description | Valeurs autorisées | Requis
-------- | ----------- | -------------- | --------
server | Nom du serveur hello sur quel hello SAP HANA instance réside. Si votre serveur utilise un port personnalisé, spécifiez `server:port`. | string | Oui
authenticationType | Type d'authentification. | chaîne. « Basic » ou « Windows » | Oui 
username | Nom d’utilisateur de hello qui a le serveur d’accès toohello SAP | string | Oui
password | Mot de passe utilisateur de hello. | string | Oui
gatewayName | Nom de passerelle hello hello service Data Factory doit utiliser l’instance de SAP HANA tooconnect toohello sur site. | string | Oui
Encryptedcredential | chaîne d’identification de Hello chiffré. | string | Non

#### <a name="example"></a>Exemple

```json
{
    "name": "SapHanaLinkedService",
    "properties": {
        "type": "SapHana",
        "typeProperties": {
            "server": "<server name>",
            "authenticationType": "<Basic, or Windows>",
            "username": "<SAP user>",
            "password": "<Password for SAP user>",
            "gatewayName": "<gateway name>"
        }
    }
}

```
Pour plus d’informations, consultez l’article [SAP HANA connector (connecteur SAP HANA)](data-factory-sap-hana-connector.md#linked-service-properties).
 
### <a name="dataset"></a>Jeu de données
toodefine un jeu de données SAP HANA, jeu hello **type** du jeu de données hello trop**RelationalTable**. Aucune propriété spécifique au type pris en charge pour le dataset de SAP HANA hello de type **RelationalTable**. 

#### <a name="example"></a>Exemple

```json
{
    "name": "SapHanaDataset",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "SapHanaLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```
Pour plus d’informations, consultez l’article [SAP HANA connector (connecteur SAP HANA)](data-factory-sap-hana-connector.md#dataset-properties). 

### <a name="relational-source-in-copy-activity"></a>Source relationnelle dans l’activité de copie
Si vous copiez des données à partir d’un magasin de données SAP HANA, la valeur hello **type de source de** Hello activité de copie trop**RelationalSource**et spécifiez les propriétés Bonjour suivantes **source**section :

| Propriété | Description | Valeurs autorisées | Requis |
| --- | --- | --- | --- |
| query | Spécifie les hello requête tooread de données SQL à partir de l’instance de SAP HANA hello. | Requête SQL. | Oui |


#### <a name="example"></a>Exemple


```json
{
    "name": "CopySapHanaToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "<SQL Query for HANA>"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "SapHanaDataset"
            }],
            "outputs": [{
                "name": "AzureBlobDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "SapHanaToBlob"
        }],
        "start": "2017-03-01T18:00:00",
        "end": "2017-03-01T19:00:00"
    }
}
```

Pour plus d’informations, consultez l’article [SAP HANA connector (connecteur SAP HANA)](data-factory-sap-hana-connector.md#copy-activity-properties).


## <a name="sql-server"></a>SQL Server

### <a name="linked-service"></a>Service lié
Vous créez un service lié de type **OnPremisesSqlServer** toolink une fabrique de données de tooa de base de données locale SQL Server. Hello tableau suivant fournit la description du service de SQL Server lié JSON éléments tooon local spécifique.

Hello tableau suivant fournit la description pour JSON éléments tooSQL spécifique service du serveur lié.

| Propriété | Description | Requis |
| --- | --- | --- |
| type |propriété de type Hello doit indiquer : **OnPremisesSqlServer**. |Oui |
| connectionString |Spécifiez les informations connectionString nécessaires de base de données SQL Server tooconnect toohello local à l’aide de l’authentification Windows ou authentification SQL. |Oui |
| gatewayName |Nom de passerelle hello hello service Data Factory doit utiliser la base de données SQL Server tooconnect toohello local. |Oui |
| username |Spécifiez le nom d’utilisateur si vous utilisez l’authentification Windows. Exemple : **domainname\\username**. |Non |
| password |Spécifiez le mot de passe de compte d’utilisateur hello que vous avez spécifié pour le nom d’utilisateur hello. |Non |

Vous pouvez chiffrer les informations d’identification à l’aide de hello **New-AzureRmDataFactoryEncryptValue** applet de commande et les utiliser dans la chaîne de connexion hello comme indiqué dans hello exemple suivant (**EncryptedCredential** propriété) :  

```json
"connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=True;EncryptedCredential=<encrypted credential>",
```


#### <a name="example-json-for-using-sql-authentication"></a>Exemple : JSON pour utilisation de l’authentification SQL

```json
{
    "name": "MyOnPremisesSQLDB",
    "properties": {
        "type": "OnPremisesSqlServer",
        "typeProperties": {
            "connectionString": "Data Source=<servername>;Initial Catalog=MarketingCampaigns;Integrated Security=False;User ID=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```
#### <a name="example-json-for-using-windows-authentication"></a>Exemple : JSON pour utilisation de l’authentification Windows

Si le nom d’utilisateur et mot de passe sont spécifiés, la passerelle les utilise tooimpersonate hello base de données utilisateur spécifié compte tooconnect toohello locale SQL Server. Dans le cas contraire, la passerelle connecte toohello SQL Server directement avec le contexte de sécurité hello de passerelle (son compte de démarrage).

```json
{
    "Name": " MyOnPremisesSQLDB",
    "Properties": {
        "type": "OnPremisesSqlServer",
        "typeProperties": {
            "ConnectionString": "Data Source=<servername>;Initial Catalog=MarketingCampaigns;Integrated Security=True;",
            "username": "<domain\\username>",
            "password": "<password>",
            "gatewayName": "<gateway name>"
        }
    }
}
```

Pour plus d’informations, consultez l’article [SQL Server connector (connecteur SQL Server)](data-factory-sqlserver-connector.md#linked-service-properties). 

### <a name="dataset"></a>Jeu de données
toodefine un jeu de données SQL Server, jeu hello **type** du jeu de données hello trop**SqlServerTable**et spécifiez hello propriétés Bonjour suivantes **typeProperties** section : 

| Propriété | Description | Requis |
| --- | --- | --- |
| TableName |Nom de la table de hello ou la vue d’instance de base de données SQL Server hello service lié fait référence à. |Oui |

#### <a name="example"></a>Exemple
```json
{
    "name": "SqlServerInput",
    "properties": {
        "type": "SqlServerTable",
        "linkedServiceName": "SqlServerLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
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

Pour plus d’informations, consultez l’article [SQL Server connector (connecteur SQL Server)](data-factory-sqlserver-connector.md#dataset-properties). 

### <a name="sql-source-in-copy-activity"></a>Source SQL dans l’activité de copie
Si vous copiez des données à partir d’une base de données SQL Server, la valeur hello **type de source de** Hello activité de copie trop**SqlSource**et spécifiez les propriétés Bonjour suivantes **source** section :


| Propriété | Description | Valeurs autorisées | Requis |
| --- | --- | --- | --- |
| SqlReaderQuery |Utiliser des données tooread hello requête personnalisée. |Chaîne de requête SQL. Par exemple : `select * from MyTable`. Peut faire référence à plusieurs tables de base de données hello référencé par le jeu de données d’entrée hello. Si non spécifié, hello instruction SQL exécutée : select from MyTable. |Non |
| sqlReaderStoredProcedureName |Nom de hello procédure stockée qui lit les données à partir de la table de source de hello. |Nom de hello procédure stockée. |Non |
| storedProcedureParameters |Pourquoi les paramètres de procédure stockée. |Paires nom/valeur. Noms et la casse des paramètres doivent correspondre à des noms de hello et la casse des paramètres de la procédure stockée hello. |Non |

Si hello **sqlReaderQuery** est spécifié pour hello SqlSource, hello activité de copie s’exécute cette requête sur des données hello tooget hello base de données SQL Server source.

Ou bien, vous pouvez spécifier une procédure stockée en spécifiant hello **sqlReaderStoredProcedureName** et **storedProcedureParameters** (si hello une procédure stockée accepte des paramètres).

Si vous ne spécifiez pas de sqlReaderQuery ou sqlReaderStoredProcedureName, les colonnes de hello définis dans la section de structure hello sont utilisée toobuild un toorun requête select sur hello de base de données SQL Server. Si la définition de dataset hello n’a pas de structure de hello, toutes les colonnes sont sélectionnées à partir de la table de hello.

> [!NOTE]
> Lorsque vous utilisez **sqlReaderStoredProcedureName**, vous devez toujours toospecify une valeur pour hello **tableName** propriété dans le dataset hello JSON. Cependant, il n’existe aucune validation effectuée pour cette table.


#### <a name="example"></a>Exemple
```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "SqlServertoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": " SqlServerInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "SqlSource",
                    "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

Dans cet exemple, **sqlReaderQuery** est spécifié pour hello SqlSource. Hello activité de copie s’exécute cette requête par rapport aux données de base de données SQL Server source tooget hello de hello. Ou bien, vous pouvez spécifier une procédure stockée en spécifiant hello **sqlReaderStoredProcedureName** et **storedProcedureParameters** (si hello une procédure stockée accepte des paramètres). Hello sqlReaderQuery permettre faire référence à plusieurs tables de base de données hello référencé par le jeu de données d’entrée hello. Il n’est pas limité tooonly hello tableau comme hello typeProperty de tableName du jeu de données.

Si vous ne spécifiez pas sqlReaderQuery ou sqlReaderStoredProcedureName, les colonnes de hello définis dans la section de structure hello sont utilisée toobuild un toorun requête select sur hello de base de données SQL Server. Si la définition de dataset hello n’a pas de structure de hello, toutes les colonnes sont sélectionnées à partir de la table de hello.

Pour plus d’informations, consultez l’article [SQL Server connector (connecteur SQL Server)](data-factory-sqlserver-connector.md#copy-activity-properties). 

### <a name="sql-sink-in-copy-activity"></a>Récepteur SQL dans l’activité de copie
Si vous copiez des données tooa base de données SQL, la valeur hello **type de récepteur** Hello activité de copie trop**SqlSink**et spécifiez les propriétés Bonjour suivantes **récepteur** section :

| Propriété | Description | Valeurs autorisées | Requis |
| --- | --- | --- | --- |
| writeBatchTimeout |Temps d’attente pour hello lot insert opération toocomplete avant d’expirer. |intervalle de temps<br/><br/> Exemple : « 00:30:00 » (30 minutes). |Non |
| writeBatchSize |Insère des données dans une table SQL de hello lorsque la taille de mémoire tampon de hello atteint la valeur writeBatchSize. |Nombre entier (nombre de lignes) |Non (valeur par défaut : 10000) |
| sqlWriterCleanupScript |Spécifier la requête pour l’activité de copie tooexecute telles que les données d’un secteur spécifique sont nettoyées. Consultez la [section sur la répétition](#repeatability-during-copy) pour plus de détails. |Une instruction de requête. |Non |
| sliceIdentifierColumnName |Spécifiez nom de colonne pour l’activité de copie toofill avec l’identificateur de secteur généré automatiquement, qui est utilisé tooclean des données d’un secteur spécifique quand réexécutée. Consultez la [section sur la répétition](#repeatability-during-copy) pour plus de détails. |Nom d’une colonne avec le type de données binary(32). |Non |
| sqlWriterStoredProcedureName |Nom de hello procédure stockée que les données upserts (mises à jour/insertion) dans la table cible hello. |Nom de hello procédure stockée. |Non |
| storedProcedureParameters |Pourquoi les paramètres de procédure stockée. |Paires nom/valeur. Noms et la casse des paramètres doivent correspondre à des noms de hello et la casse des paramètres de la procédure stockée hello. |Non |
| sqlWriterTableType |Spécifiez toobe de nom de type de table utilisée dans la procédure stockée hello. Activité de copie rend les données de hello déplacées disponibles dans une table temporaire avec ce type de table. Code de procédure stockée puis de fusionner des données hello copiées avec les données existantes. |Nom de type de table. |Non |

#### <a name="example"></a>Exemple
pipeline de Hello contient une activité de copie qui est configuré toouse ces jeux de données d’entrée et de sortie et est toorun planifiée toutes les heures. Dans la définition JSON du pipeline hello, hello **source** type est défini trop**BlobSource** et **récepteur** type est défini trop**SqlSink**.

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoSQL",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": " SqlServerOutput "
            }],
            "typeProperties": {
                "source": {
                    "type": "BlobSource",
                    "blobColumnSeparators": ","
                },
                "sink": {
                    "type": "SqlSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

Pour plus d’informations, consultez l’article [SQL Server connector (connecteur SQL Server)](data-factory-sqlserver-connector.md#copy-activity-properties). 

## <a name="sybase"></a>Sybase

### <a name="linked-service"></a>Service lié
toodefine un Sybase le service ensemble hello lié **type** Hello service lié trop**OnPremisesSybase**et spécifiez les propriétés Bonjour suivantes **typeProperties** section :  

| Propriété | Description | Requis |
| --- | --- | --- |
| server |Nom du serveur de Sybase hello. |Oui |
| database |Nom de la base de données Sybase hello. |Oui |
| schema |Nom de schéma hello hello de base de données. |Non |
| authenticationType |Type d’authentification utilisé tooconnect toohello base de données Sybase. Les valeurs possibles sont : Anonyme, De base et Windows. |Oui |
| username |Spécifiez le nom d'utilisateur si vous utilisez l'authentification de base ou Windows. |Non |
| password |Spécifiez le mot de passe de compte d’utilisateur hello que vous avez spécifié pour le nom d’utilisateur hello. |Non |
| gatewayName |Nom de passerelle hello hello service Data Factory doit utiliser la base de données Sybase tooconnect toohello local. |Oui |

#### <a name="example"></a>Exemple
```json
{
    "name": "OnPremSybaseLinkedService",
    "properties": {
        "type": "OnPremisesSybase",
        "typeProperties": {
            "server": "<server>",
            "database": "<database>",
            "schema": "<schema>",
            "authenticationType": "<authentication type>",
            "username": "<username>",
            "password": "<password>",
            "gatewayName": "<gatewayName>"
        }
    }
}
```

Pour plus d’informations, consultez l’article [Sybase connector (connecteur Sybase)](data-factory-onprem-sybase-connector.md#linked-service-properties). 

### <a name="dataset"></a>Jeu de données
toodefine un jeu de données Sybase, jeu hello **type** du jeu de données hello trop**RelationalTable**et spécifiez hello propriétés Bonjour suivantes **typeProperties** section : 

| Propriété | Description | Requis |
| --- | --- | --- |
| TableName |Nom de table hello Bonjour instance de base de données Sybase service lié fait référence à. |Non (si la **requête** de **RelationalSource** est spécifiée) |

#### <a name="example"></a>Exemple

```json
{
    "name": "SybaseDataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremSybaseLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
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

Pour plus d’informations, consultez l’article [Sybase connector (connecteur Sybase)](data-factory-onprem-sybase-connector.md#dataset-properties). 

### <a name="relational-source-in-copy-activity"></a>Source relationnelle dans l’activité de copie
Si vous copiez des données à partir d’une base de données Sybase, la valeur hello **type de source de** Hello activité de copie trop**RelationalSource**et spécifiez les propriétés Bonjour suivantes **source** section :


| Propriété | Description | Valeurs autorisées | Requis |
| --- | --- | --- | --- |
| query |Utiliser des données tooread hello requête personnalisée. |Chaîne de requête SQL. Par exemple : `select * from MyTable`. |Non (si **tableName** de **dataset** est spécifiée) |

#### <a name="example"></a>Exemple

```json
{
    "name": "CopySybaseToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "select * from DBA.Orders"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "inputs": [{
                "name": "SybaseDataSet"
            }],
            "outputs": [{
                "name": "AzureBlobSybaseDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "SybaseToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```

Pour plus d’informations, consultez l’article [Sybase connector (connecteur Sybase)](data-factory-onprem-sybase-connector.md#copy-activity-properties).

## <a name="teradata"></a>Teradata

### <a name="linked-service"></a>Service lié
toodefine un Teradata le service ensemble hello lié **type** Hello service lié trop**OnPremisesTeradata**et spécifiez les propriétés Bonjour suivantes **typeProperties** section :  

| Propriété | Description | Requis |
| --- | --- | --- |
| server |Nom du serveur de Teradata hello. |Oui |
| authenticationType |Type d’authentification utilisé tooconnect toohello base de données Teradata. Les valeurs possibles sont : Anonyme, De base et Windows. |Oui |
| username |Spécifiez le nom d'utilisateur si vous utilisez l'authentification de base ou Windows. |Non |
| password |Spécifiez le mot de passe de compte d’utilisateur hello que vous avez spécifié pour le nom d’utilisateur hello. |Non |
| gatewayName |Nom de passerelle hello hello service Data Factory doit utiliser la base de données Teradata tooconnect toohello local. |Oui |

#### <a name="example"></a>Exemple
```json
{
    "name": "OnPremTeradataLinkedService",
    "properties": {
        "type": "OnPremisesTeradata",
        "typeProperties": {
            "server": "<server>",
            "authenticationType": "<authentication type>",
            "username": "<username>",
            "password": "<password>",
            "gatewayName": "<gatewayName>"
        }
    }
}
```

Pour plus d’informations, consultez l’article [Teradata connector (connecteur Teradata)](data-factory-onprem-teradata-connector.md#linked-service-properties).

### <a name="dataset"></a>Jeu de données
toodefine un jeu de données Teradata Blob, jeu hello **type** du jeu de données hello trop**RelationalTable**. Actuellement, il n’y a aucune propriété de type pris en charge pour le jeu de données Teradata hello. 

#### <a name="example"></a>Exemple
```json
{
    "name": "TeradataDataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremTeradataLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
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

Pour plus d’informations, consultez l’article [Teradata connector (connecteur Teradata)](data-factory-onprem-teradata-connector.md#dataset-properties).

### <a name="relational-source-in-copy-activity"></a>Source relationnelle dans l’activité de copie
Si vous copiez des données à partir d’une base de données Teradata, la valeur hello **type de source de** Hello activité de copie trop**RelationalSource**et spécifiez les propriétés Bonjour suivantes **source**section :

| Propriété | Description | Valeurs autorisées | Requis |
| --- | --- | --- | --- |
| query |Utiliser des données tooread hello requête personnalisée. |Chaîne de requête SQL. Par exemple : `select * from MyTable`. |Oui |

#### <a name="example"></a>Exemple

```json
{
    "name": "CopyTeradataToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "$$Text.Format('select * from MyTable where timestamp >= \\'{0:yyyy-MM-ddTHH:mm:ss}\\' AND timestamp < \\'{1:yyyy-MM-ddTHH:mm:ss}\\'', SliceStart, SliceEnd)"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "TeradataDataSet"
            }],
            "outputs": [{
                "name": "AzureBlobTeradataDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "TeradataToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "isPaused": false
    }
}
```

Pour plus d’informations, consultez l’article [Teradata connector (connecteur Teradata)](data-factory-onprem-teradata-connector.md#copy-activity-properties).

## <a name="cassandra"></a>Cassandra


### <a name="linked-service"></a>Service lié
toodefine un Cassandra le service ensemble hello lié **type** Hello service lié trop**OnPremisesCassandra**et spécifiez les propriétés Bonjour suivantes **typeProperties** section :  

| Propriété | Description | Requis |
| --- | --- | --- |
| host |Une ou plusieurs adresses IP ou noms d’hôte de serveurs Cassandra.<br/><br/>Spécifiez une liste séparée par des virgules des adresses IP ou hôte noms tooconnect tooall serveurs simultanément. |Oui |
| port |Hello le port TCP qui hello du serveur de Cassandra utilise toolisten pour les connexions client. |Non, valeur par défaut : 9042 |
| authenticationType |Basique ou anonyme |Oui |
| username |Spécifiez le nom d’utilisateur pour le compte d’utilisateur hello. |Oui, si authenticationType a la valeur tooBasic. |
| password |Spécifiez le mot de passe de compte d’utilisateur hello. |Oui, si authenticationType a la valeur tooBasic. |
| gatewayName |nom Hello de passerelle hello est utilisé tooconnect toohello Cassandra base de données locale. |Oui |
| Encryptedcredential |Informations d’identification chiffrées par la passerelle de hello. |Non |

#### <a name="example"></a>Exemple

```json
{
    "name": "CassandraLinkedService",
    "properties": {
        "type": "OnPremisesCassandra",
        "typeProperties": {
            "authenticationType": "Basic",
            "host": "<cassandra server name or IP address>",
            "port": 9042,
            "username": "user",
            "password": "password",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

Pour plus d’informations, consultez l’article [Cassandra connector (connecteur Cassandra)](data-factory-onprem-cassandra-connector.md#linked-service-properties). 

### <a name="dataset"></a>Jeu de données
toodefine un dataset Cassandra, jeu hello **type** du jeu de données hello trop**CassandraTable**et spécifiez hello propriétés Bonjour suivantes **typeProperties** section : 

| Propriété | Description | Requis |
| --- | --- | --- |
| espace de clé |Nom de l’espace de clés hello ou un schéma de base de données Cassandra. |Oui (si la **requête** pour **CassandraSource** n’est pas définie). |
| TableName |Nom de table hello Cassandra de base de données. |Oui (si la **requête** pour **CassandraSource** n’est pas définie). |

#### <a name="example"></a>Exemple

```json
{
    "name": "CassandraInput",
    "properties": {
        "linkedServiceName": "CassandraLinkedService",
        "type": "CassandraTable",
        "typeProperties": {
            "tableName": "mytable",
            "keySpace": "<key space>"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
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

Pour plus d’informations, consultez l’article [Cassandra connector (connecteur Cassandra)](data-factory-onprem-cassandra-connector.md#dataset-properties). 

### <a name="cassandra-source-in-copy-activity"></a>Source Cassandra dans l’activité de copie
Si vous copiez des données à partir de Cassandra, définissez hello **type de source de** Hello activité de copie trop**CassandraSource**et spécifiez les propriétés Bonjour suivantes **source** section :

| Propriété | Description | Valeurs autorisées | Requis |
| --- | --- | --- | --- |
| query |Utiliser des données tooread hello requête personnalisée. |Requête SQL-92 ou requête CQL. Reportez-vous à [référence CQL](https://docs.datastax.com/en/cql/3.1/cql/cql_reference/cqlReferenceTOC.html). <br/><br/>Lorsque vous utilisez la requête SQL, spécifiez **nom d’espace de clés name.table** toorepresent hello tableau tooquery. |Non (si tableName et keyspace sur le jeu de données sont définis). |
| Niveau de cohérence |niveau de cohérence Hello Spécifie le nombre de réplicas doit répondre de requête de lecture tooa avant de retourner l’application data toohello client. Les vérifications Cassandra hello un nombre spécifié de réplicas pour la requête de lecture hello toosatisfy de données. |UN, DEUX, TROIS, QUORUM, TOUT, LOCAL_QUORUM, EACH_QUORUM, LOCAL_ONE. Reportez-vous à [Configuring data consistency (Configuration de la cohérence des données)](http://docs.datastax.com/en//cassandra/2.0/cassandra/dml/dml_config_consistency_c.html) pour plus d’informations. |Non. La valeur par défaut est UN. |

#### <a name="example"></a>Exemple
  
```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "CassandraToAzureBlob",
            "description": "Copy from Cassandra tooan Azure blob",
            "type": "Copy",
            "inputs": [{
                "name": "CassandraInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "CassandraSource",
                    "query": "select id, firstname, lastname from mykeyspace.mytable"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

Pour plus d’informations, consultez l’article [Cassandra connector (connecteur Cassandra)](data-factory-onprem-cassandra-connector.md#copy-activity-properties).

## <a name="mongodb"></a>MongoDB

### <a name="linked-service"></a>Service lié
toodefine un MongoDB le service ensemble hello lié **type** Hello service lié trop**OnPremisesMongoDB**et spécifiez les propriétés Bonjour suivantes **typeProperties** section :  

| Propriété | Description | Requis |
| --- | --- | --- |
| server |Nom hôte ou adresse IP du serveur de MongoDB hello. |Oui |
| port |Le port TCP qui hello MongoDB serveur utilise toolisten pour les connexions client. |Facultatif, valeur par défaut : 27017 |
| authenticationType |De base ou anonyme. |Oui |
| username |Tooaccess du compte utilisateur MongoDB. |Oui (si l’authentification de base est utilisée). |
| password |Mot de passe utilisateur de hello. |Oui (si l’authentification de base est utilisée). |
| authSource |Nom de la base de données MongoDB hello que vous souhaitez toouse toocheck vos informations d’identification pour l’authentification. |Facultatif (si l’authentification de base est utilisée). par défaut : utilise le compte d’administrateur hello et de la base de données de hello spécifié à l’aide de la propriété databaseName. |
| databaseName |Nom de la base de données MongoDB hello que vous souhaitez tooaccess. |Oui |
| gatewayName |Nom de la passerelle hello qui accède au magasin de données hello. |Oui |
| Encryptedcredential |Informations d’identification chiffrées par la passerelle. |Facultatif |

#### <a name="example"></a>Exemple

```json
{
    "name": "OnPremisesMongoDbLinkedService",
    "properties": {
        "type": "OnPremisesMongoDb",
        "typeProperties": {
            "authenticationType": "<Basic or Anonymous>",
            "server": "< hello IP address or host name of hello MongoDB server >",
            "port": "<hello number of hello TCP port that hello MongoDB server uses toolisten for client connections.>",
            "username": "<username>",
            "password": "<password>",
            "authSource": "< hello database that you want toouse toocheck your credentials for authentication. >",
            "databaseName": "<database name>",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

Pour plus d’informations, consultez l’article [MongoDB connector (connecteur MongoDB)](data-factory-on-premises-mongodb-connector.md#linked-service-properties)

### <a name="dataset"></a>Jeu de données
toodefine un jeu de données MongoDB, jeu hello **type** du jeu de données hello trop**MongoDbCollection**et spécifiez hello propriétés Bonjour suivantes **typeProperties** section : 

| Propriété | Description | Requis |
| --- | --- | --- |
| collectionName |Nom de collection hello dans la base de données MongoDB. |Oui |

#### <a name="example"></a>Exemple

```json
{
    "name": "MongoDbInputDataset",
    "properties": {
        "type": "MongoDbCollection",
        "linkedServiceName": "OnPremisesMongoDbLinkedService",
        "typeProperties": {
            "collectionName": "<Collection name>"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```

Pour plus d’informations, consultez l’article [MongoDB connector (connecteur MongoDB)](data-factory-on-premises-mongodb-connector.md#dataset-properties)

#### <a name="mongodb-source-in-copy-activity"></a>Source MongoDB dans l’activité de copie
Si vous copiez des données à partir de MongoDB, définissez hello **type de source de** Hello activité de copie trop**MongoDbSource**et spécifiez les propriétés Bonjour suivantes **source** section :

| Propriété | Description | Valeurs autorisées | Requis |
| --- | --- | --- | --- |
| query |Utiliser des données tooread hello requête personnalisée. |Chaîne de requête SQL-92. Par exemple : `select * from MyTable`. |Non (si **collectionName** du **jeu de données** est spécifié) |

#### <a name="example"></a>Exemple

```json
{
    "name": "CopyMongoDBToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "MongoDbSource",
                    "query": "select * from MyTable"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "MongoDbInputDataset"
            }],
            "outputs": [{
                "name": "AzureBlobOutputDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "MongoDBToAzureBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```

Pour plus d’informations, consultez l’article [MongoDB connector (connecteur MongoDB)](data-factory-on-premises-mongodb-connector.md#copy-activity-properties)

## <a name="amazon-s3"></a>Amazon S3


### <a name="linked-service"></a>Service lié
toodefine un S3 Amazon le service ensemble hello lié **type** Hello service lié trop**AwsAccessKey**et spécifiez les propriétés Bonjour suivantes **typeProperties** section :  

| Propriété | Description | Valeurs autorisées | Requis |
| --- | --- | --- | --- |
| accessKeyID |ID de clé d’accès de clé secrète hello. |string |Oui |
| secretAccessKey |clé d’accès de clé secrète Hello elle-même. |Chaîne secrète chiffrée |Oui |

#### <a name="example"></a>Exemple
```json
{
    "name": "AmazonS3LinkedService",
    "properties": {
        "type": "AwsAccessKey",
        "typeProperties": {
            "accessKeyId": "<access key id>",
            "secretAccessKey": "<secret access key>"
        }
    }
}
```

Pour plus d’informations, consultez l’article [Amazon S3 connector (connecteur Amazon S3)](data-factory-amazon-simple-storage-service-connector.md#linked-service-properties).

### <a name="dataset"></a>Jeu de données
toodefine un S3 Amazon dataset, ensemble hello **type** du jeu de données hello trop**AmazonS3**et spécifiez hello propriétés Bonjour suivantes **typeProperties** section : 

| Propriété | Description | Valeurs autorisées | Requis |
| --- | --- | --- | --- |
| bucketName |nom du compartiment Hello S3. |String |Oui |
| key |clé d’objet Hello S3. |String |Non |
| prefix |Préfixe de la clé d’objet hello S3. Les objets dont les clés commencent par ce préfixe sont sélectionnés. S’applique uniquement lorsque la clé est vide. |string |Non |
| version |version Hello d’objet S3 si le contrôle de version S3 est activé. |String |Non |
| format | Hello, les types de format suivants est pris en charge : **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**. Ensemble hello **type** propriété sous tooone de format de ces valeurs. Pour en savoir plus, consultez les sections relatives à [format Text](data-factory-supported-file-and-compression-formats.md#text-format), [format Json](data-factory-supported-file-and-compression-formats.md#json-format), [format Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [format Orc](data-factory-supported-file-and-compression-formats.md#orc-format) et [format Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format). <br><br> Si vous souhaitez trop**copier les fichiers en tant que-est** entre des magasins basée sur le fichier (copie binaire), ignorer la section de format hello dans les deux définitions de jeu de données d’entrée et de sortie. |Non | |
| compression | Spécifiez le type de hello et le niveau de compression pour les données de salutation. Les types pris en charge sont : **GZip**, **Deflate**, **BZip2** et **ZipDeflate**. les niveaux de Hello pris en charge sont : **Optimal** et **plus rapide**. Pour plus d’informations, consultez [Formats de fichiers et de compression pris en charge dans Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support). |Non | |


> [!NOTE]
> bucketName + clé spécifie l’emplacement hello d’objet hello S3 où compartiment est le conteneur racine hello S3 objets et la clé est hello chemin d’accès complet tooS3 objet.

#### <a name="example-sample-dataset-with-prefix"></a>Exemple : exemple de jeu de données avec le préfixe

```json
{
    "name": "dataset-s3",
    "properties": {
        "type": "AmazonS3",
        "linkedServiceName": "link- testS3",
        "typeProperties": {
            "prefix": "testFolder/test",
            "bucketName": "<S3 bucket name>",
            "format": {
                "type": "OrcFormat"
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
#### <a name="example-sample-data-set-with-version"></a>Exemple : exemple de jeu de données (avec la version)

```json
{
    "name": "dataset-s3",
    "properties": {
        "type": "AmazonS3",
        "linkedServiceName": "link- testS3",
        "typeProperties": {
            "key": "testFolder/test.orc",
            "bucketName": "<S3 bucket name>",
            "version": "XXXXXXXXXczm0CJajYkHf0_k6LhBmkcL",
            "format": {
                "type": "OrcFormat"
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

#### <a name="example-dynamic-paths-for-s3"></a>Exemple : chemins d’accès dynamiques pour S3
Dans l’exemple hello, nous utilisons des valeurs fixes pour les propriétés de clé et bucketName dans le jeu de données hello Amazon S3.

```json
"key": "testFolder/test.orc",
"bucketName": "<S3 bucket name>",
```

Vous pouvez avoir Data Factory calculer la clé de hello et bucketName dynamiquement au moment de l’exécution à l’aide de variables système tels que SliceStart.

```json
"key": "$$Text.Format('{0:MM}/{0:dd}/test.orc', SliceStart)"
"bucketName": "$$Text.Format('{0:yyyy}', SliceStart)"
```

Vous pouvez effectuer même hello pour la propriété de préfixe hello d’un jeu de données Amazon S3. Pour obtenir la liste des fonctions et variables prises en charge, consultez [Variables système et fonctions Data Factory](data-factory-functions-variables.md) .

Pour plus d’informations, consultez l’article [Amazon S3 connector (connecteur Amazon S3)](data-factory-amazon-simple-storage-service-connector.md#dataset-properties).

### <a name="file-system-source-in-copy-activity"></a>Source Système de fichiers dans l’activité de copie
Si vous copiez des données à partir d’Amazon S3, définissez hello **type de source de** Hello activité de copie trop**FileSystemSource**et spécifiez les propriétés Bonjour suivantes **source** section :


| Propriété | Description | Valeurs autorisées | Requis |
| --- | --- | --- | --- |
| recursive |Spécifie si la liste de toorecursively S3 objets sous le répertoire de hello. |true/false |Non |


#### <a name="example"></a>Exemple


```json
{
    "name": "CopyAmazonS3ToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "FileSystemSource",
                    "recursive": true
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "AmazonS3InputDataset"
            }],
            "outputs": [{
                "name": "AzureBlobOutputDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "AmazonS3ToBlob"
        }],
        "start": "2016-08-08T18:00:00",
        "end": "2016-08-08T19:00:00"
    }
}
```

Pour plus d’informations, consultez l’article [Amazon S3 connector (connecteur Amazon S3)](data-factory-amazon-simple-storage-service-connector.md#copy-activity-properties).

## <a name="file-system"></a>Système de fichiers


### <a name="linked-service"></a>Service lié
Vous pouvez lier une fabrique de données Azure local fichier système tooan avec hello **serveur de fichiers local** service lié. Hello tableau suivant fournit des descriptions pour les éléments JSON qui sont spécifique toohello service serveur de fichiers local lié.

| Propriété | Description | Requis |
| --- | --- | --- |
| type |Assurez-vous que les propriétés de type hello sont définie trop**OnPremisesFileServer**. |Oui |
| host |Spécifie le chemin d’accès racine de hello du dossier hello que vous souhaitez toocopy. Utilisez le caractère d’échappement de hello ' \ ' pour les caractères spéciaux dans la chaîne de hello. Consultez la section [Exemples de définitions de jeux de données et de service liés](#sample-linked-service-and-dataset-definitions) pour obtenir des exemples. |Oui |
| userId |Spécifiez des ID de hello de serveur d’accès toohello utilisateur hello. |Non (si vous choisissez encryptedcredential) |
| password |Spécifiez le mot de passe hello pour hello (userid). |Non (si vous choisissez encryptedcredential) |
| Encryptedcredential |Spécifiez les informations d’identification de hello chiffré que vous pouvez obtenir en exécutant l’applet de commande New-AzureRmDataFactoryEncryptValue de hello. |Non (si vous choisissez toospecify nom d’utilisateur et mot de passe en texte brut) |
| gatewayName |Spécifie le nom hello de passerelle hello que Data Factory doit utiliser de serveur de fichiers local tooconnect toohello. |Oui |

#### <a name="sample-folder-path-definitions"></a>Exemples de définitions de chemin d’accès du dossier 
| Scénario | Hôte dans la définition du service lié | folderPath dans la définition du jeu de données |
| --- | --- | --- |
| Dossier local sur l’ordinateur passerelle de gestion des données :  <br/><br/>Exemples : D:\\\* ou D:\dossier\sous-dossier\\* |D:\\\\ (pour la passerelle de gestion des données 2.0 et versions ultérieures) <br/><br/> hôte local (pour les versions de la passerelle de gestion des données antérieures à 2.0) |.\\\\ ou dossier\\\\sous-dossier (pour la passerelle de gestion des données 2.0 et versions ultérieures) <br/><br/>D:\\\\ ou D:\\\\dossier\\\\sous-dossier (pour les versions de la passerelle antérieures à 2.0) |
| Dossier partagé distant :  <br/><br/>Exemples : \\\\myserver\\share\\\* ou \\\\myserver\\share\\dossier\\sous-dossier\\* |\\\\\\\\myserver\\\\share |.\\\\ ou dossier\\\\sous-dossier |


#### <a name="example-using-username-and-password-in-plain-text"></a>Exemple : utilisation d’un nom d'utilisateur et d’un mot de passe en texte brut

```json
{
    "Name": "OnPremisesFileServerLinkedService",
    "properties": {
        "type": "OnPremisesFileServer",
        "typeProperties": {
            "host": "\\\\Contosogame-Asia",
            "userid": "Admin",
            "password": "123456",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="example-using-encryptedcredential"></a>Exemple : utilisation de l’élément encryptedcredential

```json
{
    "Name": " OnPremisesFileServerLinkedService ",
    "properties": {
        "type": "OnPremisesFileServer",
        "typeProperties": {
            "host": "D:\\",
            "encryptedCredential": "WFuIGlzIGRpc3Rpbmd1aXNoZWQsIG5vdCBvbmx5IGJ5xxxxxxxxxxxxxxxxx",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

Pour plus d’informations, consultez l’article [File System connector (connecteur Système de fichiers)](data-factory-onprem-file-system-connector.md#linked-service-properties).

### <a name="dataset"></a>Jeu de données
toodefine un jeu de données du système de fichiers, jeu hello **type** du jeu de données hello trop**le partage de fichiers**et spécifiez hello propriétés Bonjour suivantes **typeProperties** section : 

| Propriété | Description | Requis |
| --- | --- | --- |
| folderPath |Spécifie le dossier de toohello sous-chemin hello. Utilisez le caractère d’échappement de hello ' \' pour les caractères spéciaux dans la chaîne de hello. Consultez la section [Exemples de définitions de jeux de données et de service liés](#sample-linked-service-and-dataset-definitions) pour obtenir des exemples.<br/><br/>Vous pouvez combiner cette propriété avec **partitionBy** toohave chemins d’accès basés sur un secteur de début et date et l’heure de fin. |Oui |
| fileName |Spécifiez le nom hello du fichier de hello Bonjour **folderPath** si vous souhaitez hello table toorefer tooa fichier spécifique dans le dossier de hello. Si vous ne spécifiez pas de valeur pour cette propriété, la table de hello pointe tooall des fichiers dans le dossier de hello.<br/><br/>Lorsque le nom de fichier n’est pas spécifié pour un dataset de sortie, nom hello du fichier de hello généré est hello suivant le format suivant : <br/><br/>`Data.<Guid>.txt` (Exemple : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt) |Non |
| fileFilter |Spécifier qu'un filtre toobe utilisé tooselect un sous-ensemble de fichiers dans hello folderPath plutôt que tous les fichiers. <br/><br/>Les valeurs autorisées sont : `*` (plusieurs caractères) et `?` (caractère unique).<br/><br/>Exemple 1 : « fileFilter » : « *.log »<br/>Exemple 2 : « fileFilter » : « 2016-1-?.txt »<br/><br/>Remarque : fileFilter s’applique à un jeu de données FileShare d’entrée. |Non |
| partitionedBy |Vous pouvez utiliser partitionedBy toospecify folderPath/nom de fichier dynamique pour les données de série chronologique. Par exemple, folderPath peut être paramétré pour toutes les heures de données. |Non |
| format | Hello, les types de format suivants est pris en charge : **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**. Ensemble hello **type** propriété sous tooone de format de ces valeurs. Pour en savoir plus, consultez les sections relatives à [format Text](data-factory-supported-file-and-compression-formats.md#text-format), [format Json](data-factory-supported-file-and-compression-formats.md#json-format), [format Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [format Orc](data-factory-supported-file-and-compression-formats.md#orc-format) et [format Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format). <br><br> Si vous souhaitez trop**copier les fichiers en tant que-est** entre des magasins basée sur le fichier (copie binaire), ignorer la section de format hello dans les deux définitions de jeu de données d’entrée et de sortie. |Non |
| compression | Spécifiez le type de hello et le niveau de compression pour les données de salutation. Types pris en charge : **GZip**, **Deflate**, **BZip2** et **ZipDeflate**. Niveaux pris en charge : **Optimal** et **Fastest**. consultez [Formats de fichiers et de compression pris en charge dans Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support). |Non |

> [!NOTE]
> Vous ne pouvez pas utiliser fileName et fileFilter simultanément.

#### <a name="example"></a>Exemple

```json
{
    "name": "OnpremisesFileSystemInput",
    "properties": {
        "type": " FileShare",
        "linkedServiceName": " OnPremisesFileServerLinkedService ",
        "typeProperties": {
            "folderPath": "mysharedfolder/yearno={Year}/monthno={Month}/dayno={Day}",
            "fileName": "{Hour}.csv",
            "partitionedBy": [{
                "name": "Year",
                "value": {
                    "type": "DateTime",
                    "date": "SliceStart",
                        "format": "yyyy"
                }
            }, {
                "name": "Month",
                "value": {
                    "type": "DateTime",
                    "date": "SliceStart",
                    "format": "MM"
                }
            }, {
                "name": "Day",
                "value": {
                    "type": "DateTime",
                    "date": "SliceStart",
                    "format": "dd"
                }
            }, {
                "name": "Hour",
                "value": {
                    "type": "DateTime",
                    "date": "SliceStart",
                    "format": "HH"
                }
            }]
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
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

Pour plus d’informations, consultez l’article [File System connector (connecteur Système de fichiers)](data-factory-onprem-file-system-connector.md#dataset-properties).

### <a name="file-system-source-in-copy-activity"></a>Source Système de fichiers dans l’activité de copie
Si vous copiez des données à partir du système de fichiers, la valeur hello **type de source de** Hello activité de copie trop**FileSystemSource**et spécifiez les propriétés Bonjour suivantes **source** section :

| Propriété | Description | Valeurs autorisées | Requis |
| --- | --- | --- | --- |
| recursive |Indique si les données de salutation sont lu de manière récursive des sous-dossiers de hello ou uniquement à partir de dossier spécifié de hello. |True, False (par défaut) |Non |

#### <a name="example"></a>Exemple

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2015-06-01T18:00:00",
        "end": "2015-06-01T19:00:00",
        "description": "Pipeline for copy activity",
        "activities": [{
            "name": "OnpremisesFileSystemtoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "OnpremisesFileSystemInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "FileSystemSource"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
            "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```
Pour plus d’informations, consultez l’article [File System connector (connecteur Système de fichiers)](data-factory-onprem-file-system-connector.md#copy-activity-properties).

### <a name="file-system-sink-in-copy-activity"></a>Récepteur Système de fichiers dans l’activité de copie
Si vous copiez des données tooFile système, la valeur hello **type de récepteur** Hello activité de copie trop**FileSystemSink**et spécifiez les propriétés Bonjour suivantes **récepteur** section :

| Propriété | Description | Valeurs autorisées | Requis |
| --- | --- | --- | --- |
| copyBehavior |Définit le comportement de copie de hello lors de la source de hello est BlobSource ou système de fichiers. |**PreserveHierarchy :** conserve la hiérarchie des fichiers dans le dossier cible de hello hello. Autrement dit, chemin d’accès relatif de hello du dossier source de hello source fichier toohello est hello identique au chemin d’accès relatif de hello du dossier cible de hello cible fichier toohello.<br/><br/>**FlattenHierarchy :** tous les fichiers à partir du dossier source hello sont créés dans hello premier niveau du dossier cible. les fichiers cibles Hello sont créés avec un nom généré automatiquement.<br/><br/>**MergeFiles :** fusionne tous les fichiers à partir de fichiers de tooone du dossier source hello. Si le nom de blob/nom de fichier hello est spécifié, nom de fichier fusionné hello désigne hello spécifié. Dans le cas contraire, il s’agit d’un nom de fichier généré automatiquement. |Non |
auto-

#### <a name="example"></a>Exemple

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2015-06-01T18:00:00",
        "end": "2015-06-01T20:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "AzureSQLtoOnPremisesFile",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureSQLInput"
            }],
            "outputs": [{
                "name": "OnpremisesFileSystemOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "SqlSource",
                    "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "FileSystemSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 3,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

Pour plus d’informations, consultez l’article [File System connector (connecteur Système de fichiers)](data-factory-onprem-file-system-connector.md#copy-activity-properties).

## <a name="ftp"></a>FTP

### <a name="linked-service"></a>Service lié
toodefine FTP le service ensemble hello lié **type** Hello service lié trop**détails**et spécifiez les propriétés Bonjour suivantes **typeProperties** section :  

| Propriété | Description | Requis | Default |
| --- | --- | --- | --- |
| host |Nom ou adresse IP du serveur FTP de hello |Oui |&nbsp; |
| authenticationType |Spécification du type d’authentification |Oui |Basic, anonyme |
| username |Utilisateur qui possède le serveur d’accès toohello FTP |Non |&nbsp; |
| password |Mot de passe utilisateur de hello (nom d’utilisateur) |Non |&nbsp; |
| Encryptedcredential |Serveur FTP de d’informations d’identification chiffrées tooaccess hello |Non |&nbsp; |
| gatewayName |Nom de hello passerelle de gestion des données passerelle tooconnect tooan FTP serveur local |Non |&nbsp; |
| port |Port d’écoute sur le hello FTP serveur |Non |21 |
| enableSsl |Spécifiez si les toouse FTP sur le canal SSL/TLS |Non |true |
| enableServerCertificateValidation |Spécifiez si le serveur tooenable SSL la validation des certificats lorsque vous utilisez FTP sur un canal SSL/TLS |Non |true |

#### <a name="example-using-anonymous-authentication"></a>Exemple : utilisation de l’authentification anonyme

```json
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
            "typeProperties": {
            "authenticationType": "Anonymous",
            "host": "myftpserver.com"
        }
    }
}
```

#### <a name="example-using-username-and-password-in-plain-text-for-basic-authentication"></a>Exemple : utilisation d’un nom d’utilisateur et d’un mot de passe en texte brut pour l’authentification de base

```json
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
        "typeProperties": {
            "host": "myftpserver.com",
            "authenticationType": "Basic",
            "username": "Admin",
            "password": "123456"
        }
    }
}
```

#### <a name="example-using-port-enablessl-enableservercertificatevalidation"></a>Exemple : utilisation de port, enableSsl, enableServerCertificateValidation

```json
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
        "typeProperties": {
            "host": "myftpserver.com",
            "authenticationType": "Basic",    
            "username": "Admin",
            "password": "123456",
            "port": "21",
            "enableSsl": true,
            "enableServerCertificateValidation": true
        }
    }
}
```

#### <a name="example-using-encryptedcredential-for-authentication-and-gateway"></a>Exemple : utilisation d’encryptedCredential pour l’authentification et la passerelle

```json
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
        "typeProperties": {
            "host": "myftpserver.com",
            "authenticationType": "Basic",
            "encryptedCredential": "xxxxxxxxxxxxxxxxx",
            "gatewayName": "<onpremgateway>"
        }
      }
}
```

Pour plus d’informations, consultez l’article [FTP connector (connecteur FTP)](data-factory-ftp-connector.md#linked-service-properties).

### <a name="dataset"></a>Jeu de données
dataset toodefine FTP, jeu hello **type** du jeu de données hello trop**le partage de fichiers**et spécifiez hello propriétés Bonjour suivantes **typeProperties** section : 

| Propriété | Description | Requis |
| --- | --- | --- |
| folderPath |Sous-dossier des toohello chemin d’accès. Utilisez le caractère d’échappement ' \ ' pour les caractères spéciaux dans la chaîne de hello. Consultez la section [Exemples de définitions de jeux de données et de service liés](#sample-linked-service-and-dataset-definitions) pour obtenir des exemples.<br/><br/>Vous pouvez combiner cette propriété avec **partitionBy** toohave chemins d’accès basés sur un secteur de début et date et l’heure de fin. |Oui 
| fileName |Spécifiez le nom hello du fichier de hello Bonjour **folderPath** si vous souhaitez hello table toorefer tooa fichier spécifique dans le dossier de hello. Si vous ne spécifiez pas de valeur pour cette propriété, la table de hello pointe tooall des fichiers dans le dossier de hello.<br/><br/>Lorsque le nom de fichier n’est pas spécifié pour un dataset de sortie, nom hello du fichier de hello généré serait Bonjour sous ce format : <br/><br/>Data.<Guid>.txt (par exemple : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt) |Non |
| fileFilter |Spécifier qu'un filtre toobe utilisé tooselect un sous-ensemble de fichiers dans hello folderPath plutôt que tous les fichiers.<br/><br/>Les valeurs autorisées sont : `*` (plusieurs caractères) et `?` (caractère unique).<br/><br/>Exemple 1 : `"fileFilter": "*.log"`<br/>Exemple 2 : `"fileFilter": 2016-1-?.txt"`<br/><br/> fileFilter s’applique à un jeu de données FileShare d’entrée. Cette propriété n’est pas prise en charge avec HDFS. |Non |
| partitionedBy |partitionedBy peut être utilisé toospecify un folderPath dynamique, le nom de fichier de données de série chronologique. Par exemple, folderPath peut être paramétré pour toutes les heures de données. |Non |
| format | Hello, les types de format suivants est pris en charge : **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**. Ensemble hello **type** propriété sous tooone de format de ces valeurs. Pour en savoir plus, consultez les sections relatives à [format Text](data-factory-supported-file-and-compression-formats.md#text-format), [format Json](data-factory-supported-file-and-compression-formats.md#json-format), [format Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [format Orc](data-factory-supported-file-and-compression-formats.md#orc-format) et [format Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format). <br><br> Si vous souhaitez trop**copier les fichiers en tant que-est** entre des magasins basée sur le fichier (copie binaire), ignorer la section de format hello dans les deux définitions de jeu de données d’entrée et de sortie. |Non |
| compression | Spécifiez le type de hello et le niveau de compression pour les données de salutation. Types pris en charge : **GZip**, **Deflate**, **BZip2** et **ZipDeflate**. Niveaux pris en charge : **Optimal** et **Fastest**. Pour plus d’informations, consultez [Formats de fichiers et de compression pris en charge dans Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support). |Non |
| useBinaryTransfer |Spécifiez si vous voulez utiliser le mode de transfert binaire. True pour le mode binaire et false pour ASCII. Valeur par défaut : true. Cette propriété peut uniquement être utilisée lorsque le type de service lié associé est : FtpServer. |Non |

> [!NOTE]
> fileName et fileFilter ne peuvent pas être utilisés simultanément.

#### <a name="example"></a>Exemple

```json
{
    "name": "FTPFileInput",
    "properties": {
        "type": "FileShare",
        "linkedServiceName": "FTPLinkedService",
        "typeProperties": {
            "folderPath": "<path tooshared folder>",
            "fileName": "test.csv",
            "useBinaryTransfer": true
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

Pour plus d’informations, consultez l’article [FTP connector (connecteur FTP)](data-factory-ftp-connector.md#dataset-properties).

### <a name="file-system-source-in-copy-activity"></a>Source Système de fichiers dans l’activité de copie
Si vous copiez des données à partir d’un serveur FTP, définissez hello **type de source de** Hello activité de copie trop**FileSystemSource**et spécifiez les propriétés Bonjour suivantes **source** section :

| Propriété | Description | Valeurs autorisées | Requis |
| --- | --- | --- | --- |
| recursive |Indique si les données de salutation sont lu de manière récursive à partir de dossiers de sub hello ou uniquement à partir de dossier spécifié de hello. |True, False (par défaut) |Non |

#### <a name="example"></a>Exemple

```json
{
    "name": "pipeline",
    "properties": {
        "activities": [{
            "name": "FTPToBlobCopy",
            "inputs": [{
                "name": "FtpFileInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "FileSystemSource"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "NewestFirst",
                "retry": 1,
                "timeout": "00:05:00"
            }
        }],
        "start": "2016-08-24T18:00:00",
        "end": "2016-08-24T19:00:00"
    }
}
```

Pour plus d’informations, consultez l’article [FTP connector (connecteur FTP)](data-factory-ftp-connector.md#copy-activity-properties).


## <a name="hdfs"></a>HDFS

### <a name="linked-service"></a>Service lié
toodefine un HDFS le service ensemble hello lié **type** Hello service lié trop**Hdfs**et spécifiez les propriétés Bonjour suivantes **typeProperties** section :  

| Propriété | Description | Requis |
| --- | --- | --- |
| type |propriété de type Hello doit indiquer : **Hdfs** |Oui |
| Url |URL toohello HDFS |Oui |
| authenticationType |Anonyme ou Windows. <br><br> toouse **l’authentification Kerberos** pour le connecteur HDFS, consultez trop[cette section](#use-kerberos-authentication-for-hdfs-connector) tooset votre environnement local en conséquence. |Oui |
| userName |Nom d’utilisateur de l’authentification Windows |Oui (pour l’authentification Windows) |
| password |Mot de passe de l’authentification Windows |Oui (pour l’authentification Windows) |
| gatewayName |Nom de passerelle hello hello service Data Factory doit utiliser tooconnect toohello HDFS. |Oui |
| Encryptedcredential |[Nouveau-AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) sortie des informations d’identification de l’accès hello. |Non |

#### <a name="example-using-anonymous-authentication"></a>Exemple : utilisation de l’authentification anonyme

```json
{
    "name": "HDFSLinkedService",
    "properties": {
        "type": "Hdfs",
        "typeProperties": {
            "authenticationType": "Anonymous",
            "userName": "hadoop",
            "url": "http://<machine>:50070/webhdfs/v1/",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="example-using-windows-authentication"></a>Exemple : utilisation de l’authentification Windows

```json
{
    "name": "HDFSLinkedService",
    "properties": {
        "type": "Hdfs",
        "typeProperties": {
            "authenticationType": "Windows",
            "userName": "Administrator",
            "password": "password",
            "url": "http://<machine>:50070/webhdfs/v1/",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

Pour plus d’informations, consultez l’article [HDFS connector (connecteur HDFS)](#data-factory-hdfs-connector.md#linked-service-properties). 

### <a name="dataset"></a>Jeu de données
toodefine un jeu de données HDFS, jeu hello **type** du jeu de données hello trop**le partage de fichiers**et spécifiez hello propriétés Bonjour suivantes **typeProperties** section : 

| Propriété | Description | Requis |
| --- | --- | --- |
| folderPath |Dossier toohello de chemin d’accès. Exemple : `myfolder`<br/><br/>Utilisez le caractère d’échappement ' \ ' pour les caractères spéciaux dans la chaîne de hello. Par exemple : pour dossier\sous-dossier, spécifiez dossier\\\\sous-dossier et pour d:\dossier d’exemple, spécifiez d:\\\\dossier d’exemple.<br/><br/>Vous pouvez combiner cette propriété avec **partitionBy** toohave chemins d’accès basés sur un secteur de début et date et l’heure de fin. |Oui |
| fileName |Spécifiez le nom hello du fichier de hello Bonjour **folderPath** si vous souhaitez hello table toorefer tooa fichier spécifique dans le dossier de hello. Si vous ne spécifiez pas de valeur pour cette propriété, la table de hello pointe tooall des fichiers dans le dossier de hello.<br/><br/>Lorsque le nom de fichier n’est pas spécifié pour un dataset de sortie, nom hello du fichier de hello généré serait Bonjour sous ce format : <br/><br/>Data<Guid>.txt (par exemple : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt) |Non |
| partitionedBy |partitionedBy peut être utilisé toospecify un folderPath dynamique, le nom de fichier de données de série chronologique. Exemple : folderPath peut être paramétré pour toutes les heures de données. |Non |
| format | Hello, les types de format suivants est pris en charge : **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**. Ensemble hello **type** propriété sous tooone de format de ces valeurs. Pour en savoir plus, consultez les sections relatives à [format Text](data-factory-supported-file-and-compression-formats.md#text-format), [format Json](data-factory-supported-file-and-compression-formats.md#json-format), [format Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [format Orc](data-factory-supported-file-and-compression-formats.md#orc-format) et [format Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format). <br><br> Si vous souhaitez trop**copier les fichiers en tant que-est** entre des magasins basée sur le fichier (copie binaire), ignorer la section de format hello dans les deux définitions de jeu de données d’entrée et de sortie. |Non |
| compression | Spécifiez le type de hello et le niveau de compression pour les données de salutation. Les types pris en charge sont : **GZip**, **Deflate**, **BZip2** et **ZipDeflate**. Les niveaux pris en charge sont **Optimal** et **Fastest**. Pour plus d’informations, consultez [Formats de fichiers et de compression pris en charge dans Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support). |Non |

> [!NOTE]
> fileName et fileFilter ne peuvent pas être utilisés simultanément.

#### <a name="example"></a>Exemple

```json
{
    "name": "InputDataset",
    "properties": {
        "type": "FileShare",
        "linkedServiceName": "HDFSLinkedService",
        "typeProperties": {
            "folderPath": "DataTransfer/UnitTest/"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

Pour plus d’informations, consultez l’article [HDFS connector (connecteur HDFS)](#data-factory-hdfs-connector.md#dataset-properties). 

### <a name="file-system-source-in-copy-activity"></a>Source Système de fichiers dans l’activité de copie
Si vous copiez des données à partir de HDFS, la valeur hello **type de source de** Hello activité de copie trop**FileSystemSource**et spécifiez les propriétés Bonjour suivantes **source** section :

**FileSystemSource** prend en charge hello propriétés suivantes :

| Propriété | Description | Valeurs autorisées | Requis |
| --- | --- | --- | --- |
| recursive |Indique si les données de salutation sont lu de manière récursive à partir de dossiers de sub hello ou uniquement à partir de dossier spécifié de hello. |True, False (par défaut) |Non |

#### <a name="example"></a>Exemple

```json
{
    "name": "pipeline",
    "properties": {
        "activities": [{
            "name": "HdfsToBlobCopy",
            "inputs": [{
                "name": "InputDataset"
            }],
            "outputs": [{
                "name": "OutputDataset"
            }],
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "FileSystemSource"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "NewestFirst",
                "retry": 1,
                "timeout": "00:05:00"
            }
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```

Pour plus d’informations, consultez l’article [HDFS connector (connecteur HDFS)](#data-factory-hdfs-connector.md#copy-activity-properties).

## <a name="sftp"></a>SFTP


### <a name="linked-service"></a>Service lié
toodefine un SFTP le service ensemble hello lié **type** Hello service lié trop**Sftp**et spécifiez les propriétés Bonjour suivantes **typeProperties** section :  

| Propriété | Description | Requis |
| --- | --- | --- | --- |
| host | Nom ou adresse IP du serveur SFTP de hello. |Oui |
| port |Port d’écoute sur le hello SFTP serveur. la valeur par défaut Hello est : 21 |Non |
| authenticationType |Spécification du type d’authentification. Valeurs autorisées : **De base** et **SshPublicKey**. <br><br> Consultez trop[l’authentification de base à l’aide](#using-basic-authentication) et [à l’aide de SSH authentification par clé publique](#using-ssh-public-key-authentication) sections respectivement sur plus de propriétés et des exemples JSON. |Oui |
| skipHostKeyValidation | Spécifiez si tooskip validation de clé de l’hôte. | Non. Hello la valeur par défaut : false |
| hostKeyFingerprint | Spécifier les empreintes hello de clé d’hôte hello. | Oui si hello `skipHostKeyValidation` a la valeur toofalse.  |
| gatewayName |Nom de hello passerelle de gestion des données tooconnect tooan local serveur SFTP. | Oui en cas de copie de données à partir d’un serveur SFTP local. |
| Encryptedcredential | Les informations d’identification chiffrées tooaccess hello SFTP le serveur. Généré automatiquement lorsque vous spécifiez l’authentification de base (nom d’utilisateur + mot de passe) ou paramètres SshPublicKey (nom d’utilisateur + chemin d’accès de la clé privée ou contenu) dans la copie Assistant ou hello ClickOnce boîte de dialogue contextuelle. | Non. S’applique uniquement pour la copie de données à partir d’un serveur SFTP local. |

#### <a name="example-using-basic-authentication"></a>Exemple : utilisation de l’authentification de base

l’authentification de base toouse, définissez `authenticationType` comme `Basic`et spécifiez les propriétés suivantes en plus de hello connecteur SFTP génériques introduits dans la dernière section de hello de hello :

| Propriété | Description | Requis |
| --- | --- | --- | --- |
| username | Utilisateur a accès toohello SFTP serveur. |Oui |
| password | Mot de passe pour l’utilisateur hello (nom d’utilisateur). | Oui |

```json
{
    "name": "SftpLinkedService",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "<SFTP server name or IP address>",
            "port": 22,
            "authenticationType": "Basic",
            "username": "xxx",
            "password": "xxx",
            "skipHostKeyValidation": false,
            "hostKeyFingerPrint": "ssh-rsa 2048 xx:00:00:00:xx:00:x0:0x:0x:0x:0x:00:00:x0:x0:00",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="example-basic-authentication-with-encrypted-credential"></a>Exemple : authentification de base avec des informations d’identification chiffrées**

```json
{
    "name": "SftpLinkedService",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "<FTP server name or IP address>",
            "port": 22,
            "authenticationType": "Basic",
            "username": "xxx",
            "encryptedCredential": "xxxxxxxxxxxxxxxxx",
            "skipHostKeyValidation": false,
            "hostKeyFingerPrint": "ssh-rsa 2048 xx:00:00:00:xx:00:x0:0x:0x:0x:0x:00:00:x0:x0:00",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="using-ssh-public-key-authentication"></a>Utilisation de l’authentification par clé publique SSH : **

l’authentification de base toouse, définissez `authenticationType` comme `SshPublicKey`et spécifiez les propriétés suivantes en plus de hello connecteur SFTP génériques introduits dans la dernière section de hello de hello :

| Propriété | Description | Requis |
| --- | --- | --- | --- |
| username |Utilisateur qui a accès toohello SFTP serveur |Oui |
| privateKeyPath | Spécifiez le chemin d’accès absolu toohello cette passerelle peut accéder à fichier de clé privée. | Spécifiez soit hello `privateKeyPath` ou `privateKeyContent`. <br><br> S’applique uniquement pour la copie de données à partir d’un serveur SFTP local. |
| privateKeyContent | Une chaîne sérialisée de contenu de clé privée hello. Hello Assistant copie peut lire le fichier de clé privée hello et extraire le contenu de clé privée hello automatiquement. Si vous utilisez n’importe quel autre outil/Kit de développement logiciel, utilisez à la place des propriétés de privateKeyPath hello. | Spécifiez soit hello `privateKeyPath` ou `privateKeyContent`. |
| passPhrase | Spécifiez hello expression/mot de passe toodecrypt hello privée clé si le fichier de clé hello est protégé par un mot de passe. | Oui si le fichier de clé privée hello est protégé par un mot de passe. |

```json
{
    "name": "SftpLinkedServiceWithPrivateKeyPath",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "<FTP server name or IP address>",
            "port": 22,
            "authenticationType": "SshPublicKey",
            "username": "xxx",
            "privateKeyPath": "D:\\privatekey_openssh",
            "passPhrase": "xxx",
            "skipHostKeyValidation": true,
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="example-sshpublickey-authentication-using-private-key-content"></a>Exemple : authentification SshPublicKey à l’aide du contenu de clé privée**

```json
{
    "name": "SftpLinkedServiceWithPrivateKeyContent",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "mysftpserver.westus.cloudapp.azure.com",
            "port": 22,
            "authenticationType": "SshPublicKey",
            "username": "xxx",
            "privateKeyContent": "<base64 string of hello private key content>",
            "passPhrase": "xxx",
            "skipHostKeyValidation": true
        }
    }
}
```

Pour plus d’informations, consultez l’article [SFTP connector (connecteur SFTP)](data-factory-sftp-connector.md#linked-service-properties). 

### <a name="dataset"></a>Jeu de données
toodefine un dataset SFTP, jeu hello **type** du jeu de données hello trop**le partage de fichiers**et spécifiez hello propriétés Bonjour suivantes **typeProperties** section : 

| Propriété | Description | Requis |
| --- | --- | --- |
| folderPath |Sous-dossier des toohello chemin d’accès. Utilisez le caractère d’échappement ' \ ' pour les caractères spéciaux dans la chaîne de hello. Consultez la section [Exemples de définitions de jeux de données et de service liés](#sample-linked-service-and-dataset-definitions) pour obtenir des exemples.<br/><br/>Vous pouvez combiner cette propriété avec **partitionBy** toohave chemins d’accès basés sur un secteur de début et date et l’heure de fin. |Oui |
| fileName |Spécifiez le nom hello du fichier de hello Bonjour **folderPath** si vous souhaitez hello table toorefer tooa fichier spécifique dans le dossier de hello. Si vous ne spécifiez pas de valeur pour cette propriété, la table de hello pointe tooall des fichiers dans le dossier de hello.<br/><br/>Lorsque le nom de fichier n’est pas spécifié pour un dataset de sortie, nom hello du fichier de hello généré serait Bonjour sous ce format : <br/><br/>Data.<Guid>.txt (par exemple : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt) |Non |
| fileFilter |Spécifier qu'un filtre toobe utilisé tooselect un sous-ensemble de fichiers dans hello folderPath plutôt que tous les fichiers.<br/><br/>Les valeurs autorisées sont : `*` (plusieurs caractères) et `?` (caractère unique).<br/><br/>Exemple 1 : `"fileFilter": "*.log"`<br/>Exemple 2 : `"fileFilter": 2016-1-?.txt"`<br/><br/> fileFilter s’applique à un jeu de données FileShare d’entrée. Cette propriété n’est pas prise en charge avec HDFS. |Non |
| partitionedBy |partitionedBy peut être utilisé toospecify un folderPath dynamique, le nom de fichier de données de série chronologique. Par exemple, folderPath peut être paramétré pour toutes les heures de données. |Non |
| format | Hello, les types de format suivants est pris en charge : **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**. Ensemble hello **type** propriété sous tooone de format de ces valeurs. Pour en savoir plus, consultez les sections relatives à [format Text](data-factory-supported-file-and-compression-formats.md#text-format), [format Json](data-factory-supported-file-and-compression-formats.md#json-format), [format Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [format Orc](data-factory-supported-file-and-compression-formats.md#orc-format) et [format Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format). <br><br> Si vous souhaitez trop**copier les fichiers en tant que-est** entre des magasins basée sur le fichier (copie binaire), ignorer la section de format hello dans les deux définitions de jeu de données d’entrée et de sortie. |Non |
| compression | Spécifiez le type de hello et le niveau de compression pour les données de salutation. Les types pris en charge sont : **GZip**, **Deflate**, **BZip2** et **ZipDeflate**. Les niveaux pris en charge sont **Optimal** et **Fastest**. Pour plus d’informations, consultez [Formats de fichiers et de compression pris en charge dans Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support). |Non |
| useBinaryTransfer |Spécifiez si vous voulez utiliser le mode de transfert binaire. True pour le mode binaire et false pour ASCII. Valeur par défaut : true. Cette propriété peut uniquement être utilisée lorsque le type de service lié associé est : FtpServer. |Non |

> [!NOTE]
> fileName et fileFilter ne peuvent pas être utilisés simultanément.

#### <a name="example"></a>Exemple

```json
{
    "name": "SFTPFileInput",
    "properties": {
        "type": "FileShare",
        "linkedServiceName": "SftpLinkedService",
        "typeProperties": {
            "folderPath": "<path tooshared folder>",
            "fileName": "test.csv"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

Pour plus d’informations, consultez l’article [SFTP connector (connecteur SFTP)](data-factory-sftp-connector.md#dataset-properties). 

### <a name="file-system-source-in-copy-activity"></a>Source Système de fichiers dans l’activité de copie
Si vous copiez des données à partir d’une source SFTP, la valeur hello **type de source de** Hello activité de copie trop**FileSystemSource**et spécifiez les propriétés Bonjour suivantes **source** section :

| Propriété | Description | Valeurs autorisées | Requis |
| --- | --- | --- | --- |
| recursive |Indique si les données de salutation sont lu de manière récursive à partir de dossiers de sub hello ou uniquement à partir de dossier spécifié de hello. |True, False (par défaut) |Non |



#### <a name="example"></a>Exemple

```json
{
    "name": "pipeline",
    "properties": {
        "activities": [{
            "name": "SFTPToBlobCopy",
            "inputs": [{
                "name": "SFTPFileInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "FileSystemSource"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "NewestFirst",
                "retry": 1,
                "timeout": "00:05:00"
            }
        }],
        "start": "2017-02-20T18:00:00",
        "end": "2017-02-20T19:00:00"
    }
}
```

Pour plus d’informations, consultez l’article [SFTP connector (connecteur SFTP)](data-factory-sftp-connector.md#copy-activity-properties).


## <a name="http"></a>HTTP

### <a name="linked-service"></a>Service lié
le service ensemble hello lié toodefine un HTTP **type** Hello service lié trop**Http**et spécifiez les propriétés Bonjour suivantes **typeProperties** section :  

| Propriété | Description | Requis |
| --- | --- | --- |
| url | Toohello de l’URL du serveur Web de base | Oui |
| authenticationType | Spécifie le type d’authentification hello. Les valeurs autorisées sont : **Anonymous** (Anonyme), **Basic** (De base), **Digest**, **Windows**, **ClientCertificate** (Certificat client). <br><br> Font respectivement référence toosections sous ce tableau sur plus de propriétés et des exemples JSON pour ces types d’authentification. | Oui |
| enableServerCertificateValidation | Spécifiez si le serveur tooenable SSL la validation des certificats si la source est le serveur de Web HTTPS | Non, la valeur par défaut est True. |
| gatewayName | Nom de tooan de tooconnect hello passerelle de gestion des données sur site source HTTP. | Oui en cas de copie de données à partir d’une source HTTP locale. |
| Encryptedcredential | Les informations d’identification chiffrées tooaccess hello de point de terminaison HTTP. Généré automatiquement lorsque vous configurez des informations d’authentification hello dans copie Assistant ou hello ClickOnce boîte de dialogue contextuelle. | Non. S’applique uniquement pour la copie de données à partir d’un serveur HTTP local. |

#### <a name="example-using-basic-digest-or-windows-authentication"></a>Exemple : utilisation de l’authentification Basic (De base), Digest ou Windows
Définissez `authenticationType` en tant que `Basic`, `Digest`, ou `Windows`et spécifiez hello propriétés suivantes en plus de hello du connecteur HTTP générique celles présentées ci-dessus :

| Propriété | Description | Requis |
| --- | --- | --- |
| username | Nom d’utilisateur tooaccess hello de point de terminaison HTTP. | Oui |
| password | Mot de passe pour l’utilisateur hello (nom d’utilisateur). | Oui |

```json
{
    "name": "HttpLinkedService",
    "properties": {
        "type": "Http",
        "typeProperties": {
            "authenticationType": "basic",
            "url": "https://en.wikipedia.org/wiki/",
            "userName": "user name",
            "password": "password"
        }
    }
}
```

#### <a name="example-using-clientcertificate-authentication"></a>Exemple : utilisation de l’authentification ClientCertificate (Certificat client)

l’authentification de base toouse, définissez `authenticationType` comme `ClientCertificate`et spécifiez hello propriétés suivantes en plus de hello du connecteur HTTP générique celles présentées ci-dessus :

| Propriété | Description | Requis |
| --- | --- | --- |
| embeddedCertData | contenu codé en Base64 Hello de données binaires du fichier d’informations Exchange PFX (Personal) hello. | Spécifiez soit hello `embeddedCertData` ou `certThumbprint`. |
| certThumbprint | Bonjour empreinte numérique du certificat hello qui a été installé sur le magasin de certificats de l’ordinateur de votre passerelle. S’applique uniquement pour la copie de données à partir d’une source HTTP locale. | Spécifiez soit hello `embeddedCertData` ou `certThumbprint`. |
| password | Mot de passe associé au certificat de hello. | Non |

Si vous utilisez `certThumbprint` pour l’authentification et hello du certificat est installé dans le magasin personnel de l’ordinateur local de hello de hello, vous devez le service passerelle toohello toogrant hello autorisation de lecture :

1. Lancez Microsoft Management Console (MMC). Ajouter hello **certificats** que hello cibles du composant logiciel enfichable **ordinateur Local**.
2. Développez **Certificats**, **Personnel**, puis cliquez sur **Certificats**.
3. Certificat hello magasin personnel de hello d’avec le bouton droit, puis sélectionnez **toutes les tâches**->**gérer les clés privées...**
3. Sur hello **sécurité** onglet, ajoutez le compte d’utilisateur hello sous lequel le Service hôte de passerelle de gestion des données s’exécute avec le certificat de toohello hello accès en lecture.  

**Exemple : utilisation de certificat client :** cela les liaisons de service vos données fabrique tooan local HTTP web serveur lié. Il utilise un certificat de client est installé sur l’ordinateur de hello avec la passerelle de gestion des données installé.

```json
{
    "name": "HttpLinkedService",
    "properties": {
        "type": "Http",
        "typeProperties": {
            "authenticationType": "ClientCertificate",
            "url": "https://en.wikipedia.org/wiki/",
            "certThumbprint": "thumbprint of certificate",
            "gatewayName": "gateway name"
        }
    }
}
```

#### <a name="example-using-client-certificate-in-a-file"></a>Exemple : utilisation d’un certificat client dans un fichier
Cela les liaisons de service vos données fabrique tooan local HTTP web serveur lié. Elle utilise un fichier de certificat client sur l’ordinateur de hello avec la passerelle de gestion des données installé.

```json
{
    "name": "HttpLinkedService",
    "properties": {
        "type": "Http",
        "typeProperties": {
            "authenticationType": "ClientCertificate",
            "url": "https://en.wikipedia.org/wiki/",
            "embeddedCertData": "base64 encoded cert data",
            "password": "password of cert"
        }
    }
}
```

Pour plus d’informations, consultez l’article [HTTP connector (connecteur HTTP)](data-factory-http-connector.md#linked-service-properties).

### <a name="dataset"></a>Jeu de données
toodefine un HTTP dataset, ensemble hello **type** du jeu de données hello trop**Http**et spécifiez hello propriétés Bonjour suivantes **typeProperties** section : 

| Propriété | Description | Requis |
|:--- |:--- |:--- |
| relativeUrl | Une ressource URL toohello relative qui contient les données de salutation. Lorsque le chemin d’accès n’est pas spécifié, seul hello URL spécifiée dans la définition de service hello lié est utilisé. <br><br> tooconstruct des URL dynamique, vous pouvez utiliser [les variables système et les fonctions de Data Factory](data-factory-functions-variables.md), exemple : `"relativeUrl": "$$Text.Format('/my/report?month={0:yyyy}-{0:MM}&fmt=csv', SliceStart)"`. | Non |
| requestMethod | Méthode HTTP. Les valeurs autorisées sont **GET** ou **POST**. | Non. La valeur par défaut est `GET`. |
| additionalHeaders | En-têtes de requête HTTP supplémentaires. | Non |
| RequestBody | Corps de la requête HTTP. | Non |
| format | Si vous souhaitez toosimply **hello de données à partir du point de terminaison HTTP en tant que-est** sans qu’il analyse, ignorer les paramètres de ce format. <br><br> Si vous souhaitez la réponse de hello HTTP tooparse contenu pendant la copie, hello les types de format suivants est pris en charge : **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**. Pour en savoir plus, consultez les sections relatives à [format Text](data-factory-supported-file-and-compression-formats.md#text-format), [format Json](data-factory-supported-file-and-compression-formats.md#json-format), [format Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [format Orc](data-factory-supported-file-and-compression-formats.md#orc-format) et [format Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format). |Non |
| compression | Spécifiez le type de hello et le niveau de compression pour les données de salutation. Les types pris en charge sont : **GZip**, **Deflate**, **BZip2** et **ZipDeflate**. Les niveaux pris en charge sont **Optimal** et **Fastest**. Pour plus d’informations, consultez [Formats de fichiers et de compression pris en charge dans Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support). |Non |

#### <a name="example-using-hello-get-default-method"></a>Exemple : utilisation de méthode GET (par défaut) de hello

```json
{
    "name": "HttpSourceDataInput",
    "properties": {
        "type": "Http",
        "linkedServiceName": "HttpLinkedService",
        "typeProperties": {
            "relativeUrl": "XXX/test.xml",
            "additionalHeaders": "Connection: keep-alive\nUser-Agent: Mozilla/5.0\n"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

#### <a name="example-using-hello-post-method"></a>Exemple : utilisation de méthode POST hello

```json
{
    "name": "HttpSourceDataInput",
    "properties": {
        "type": "Http",
        "linkedServiceName": "HttpLinkedService",
        "typeProperties": {
            "relativeUrl": "/XXX/test.xml",
            "requestMethod": "Post",
            "requestBody": "body for POST HTTP request"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```
Pour plus d’informations, consultez l’article [HTTP connector (connecteur HTTP)](data-factory-http-connector.md#dataset-properties).

### <a name="http-source-in-copy-activity"></a>Source HTTP dans l’activité de copie
Si vous copiez des données à partir d’une source de HTTP, définissez hello **type de source de** Hello activité de copie trop**HttpSource**et spécifiez les propriétés Bonjour suivantes **source** section :

| Propriété | Description | Requis |
| -------- | ----------- | -------- |
| httpRequestTimeout | Bonjour le délai d’attente (TimeSpan) pour tooget de demande HTTP hello une réponse. Il est tooget hello du délai d’attente de réponse, pas les données de réponse du tooread hello du délai d’attente. | Non. Valeur par défaut : 00:01:40 |


#### <a name="example"></a>Exemple

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "HttpSourceToAzureBlob",
            "description": "Copy from an HTTP source tooan Azure blob",
            "type": "Copy",
            "inputs": [{
                "name": "HttpSourceDataInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "HttpSource"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

Pour plus d’informations, consultez l’article [HTTP connector (connecteur HTTP)](data-factory-http-connector.md#copy-activity-properties).

## <a name="odata"></a>OData

### <a name="linked-service"></a>Service lié
toodefine OData liée service, jeu hello **type** Hello service lié trop**OData**et spécifiez les propriétés Bonjour suivantes **typeProperties** section :  

| Propriété | Description | Requis |
| --- | --- | --- |
| url |URL de hello service OData. |Oui |
| authenticationType |Type d’authentification utilisé tooconnect toohello OData source. <br/><br/> Pour OData dans le cloud, les valeurs possibles sont Anonyme, De base et OAuth (notez qu’à l’heure actuelle, Azure Data Factory prend en charge uniquement l’authentification OAuth basée sur Azure Active Directory). <br/><br/> Pour OData en local, les valeurs possibles sont Anonyme, De base et Windows. |Oui |
| username |Spécifiez le nom d’utilisateur si vous utilisez l’authentification de base. |Oui (uniquement si vous utilisez l’authentification de base) |
| password |Spécifiez le mot de passe de compte d’utilisateur hello que vous avez spécifié pour le nom d’utilisateur hello. |Oui (uniquement si vous utilisez l’authentification de base) |
| authorizedCredential |Si vous utilisez OAuth, cliquez sur **Authorize** bouton de hello Assistant copie de fabrique de données ou de l’éditeur et entrez vos informations d’identification, puis de la valeur hello de cette propriété sera généré automatiquement. |Oui (uniquement si vous utilisez l’authentification OAuth) |
| gatewayName |Nom de passerelle hello hello service Data Factory doit utiliser le service OData de tooconnect toohello local. Indiquez uniquement si vous copiez des données à partir de la source OData locale. |Non |

#### <a name="example---using-basic-authentication"></a>Exemple : utilisation de l’authentification de base
```json
{
    "name": "inputLinkedService",
    "properties": {
        "type": "OData",
        "typeProperties": {
            "url": "http://services.odata.org/OData/OData.svc",
            "authenticationType": "Basic",
            "username": "username",
            "password": "password"
        }
    }
}
```

#### <a name="example---using-anonymous-authentication"></a>Exemple : utilisation de l’authentification anonyme

```json
{
    "name": "ODataLinkedService",
    "properties": {
        "type": "OData",
        "typeProperties": {
            "url": "http://services.odata.org/OData/OData.svc",
            "authenticationType": "Anonymous"
        }
    }
}
```

#### <a name="example---using-windows-authentication-accessing-on-premises-odata-source"></a>Exemple : utilisation de l’authentification Windows pour accéder à la source OData locale

```json
{
    "name": "inputLinkedService",
    "properties": {
        "type": "OData",
        "typeProperties": {
            "url": "<endpoint of on-premises OData source, for example, Dynamics CRM>",
            "authenticationType": "Windows",
            "username": "domain\\user",
            "password": "password",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="example---using-oauth-authentication-accessing-cloud-odata-source"></a>Exemple : utilisation de l’authentification OAuth pour accéder à la source OData dans le cloud
```json
{
    "name": "inputLinkedService",
    "properties":
    {
        "type": "OData",
            "typeProperties":
        {
            "url": "<endpoint of cloud OData source, for example, https://<tenant>.crm.dynamics.com/XRMServices/2011/OrganizationData.svc>",
            "authenticationType": "OAuth",
            "authorizedCredential": "<auto generated by clicking hello Authorize button on UI>"
        }
    }
}
```

Pour plus d’informations, consultez l’article [OData connector (connecteur OData)](data-factory-odata-connector.md#linked-service-properties).

### <a name="dataset"></a>Jeu de données
toodefine un jeu de données OData, jeu hello **type** du jeu de données hello trop**ODataResource**et spécifiez hello propriétés Bonjour suivantes **typeProperties** section : 

| Propriété | Description | Requis |
| --- | --- | --- |
| path |Chemin d’accès toohello ressource OData |Non |

#### <a name="example"></a>Exemple

```json
{
    "name": "ODataDataset",
    "properties": {
        "type": "ODataResource",
        "typeProperties": {
            "path": "Products"
        },
        "linkedServiceName": "ODataLinkedService",
        "structure": [],
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "retryInterval": "00:01:00",
            "retryTimeout": "00:10:00",
            "maximumRetry": 3
        }
    }
}
```

Pour plus d’informations, consultez l’article [OData connector (connecteur OData)](data-factory-odata-connector.md#dataset-properties).

### <a name="relational-source-in-copy-activity"></a>Source relationnelle dans l’activité de copie
Si vous copiez des données à partir d’une source OData, définissez hello **type de source de** Hello activité de copie trop**RelationalSource**et spécifiez les propriétés Bonjour suivantes **source** section :

| Propriété | Description | Exemple | Requis |
| --- | --- | --- | --- |
| query |Utiliser des données tooread hello requête personnalisée. |"?$select=Name, Description&$top=5" |Non |

#### <a name="example"></a>Exemple

```json
{
    "name": "CopyODataToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "?$select=Name, Description&$top=5"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "ODataDataSet"
            }],
            "outputs": [{
                "name": "AzureBlobODataDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "ODataToBlob"
        }],
        "start": "2017-02-01T18:00:00",
        "end": "2017-02-03T19:00:00"
    }
}
```

Pour plus d’informations, consultez l’article [OData connector (connecteur OData)](data-factory-odata-connector.md#copy-activity-properties).


## <a name="odbc"></a>ODBC


### <a name="linked-service"></a>Service lié
le service ensemble hello lié toodefine une application ODBC **type** Hello service lié trop**OnPremisesOdbc**et spécifiez les propriétés Bonjour suivantes **typeProperties** section :  

| Propriété | Description | Requis |
| --- | --- | --- |
| connectionString |partie des informations d’identification de l’accès non Hello de chaîne de connexion hello et éventuellement un chiffrées d’informations d’identification. Consultez les exemples dans les sections suivantes de hello. |Oui |
| credential |Hello accès informations d’identification la partie de chaîne de connexion hello spécifié au format de la valeur de propriété spécifiques au pilote. Exemple : « Uid=<user ID>;Pwd=<password>;RefreshToken=<secret refresh token>; ». |Non |
| authenticationType |Type d’authentification utilisé le magasin de données ODBC tooconnect toohello. Les valeurs possibles sont : Anonyme et De base. |Oui |
| username |Spécifiez le nom d’utilisateur si vous utilisez l’authentification de base. |Non |
| password |Spécifiez le mot de passe de compte d’utilisateur hello que vous avez spécifié pour le nom d’utilisateur hello. |Non |
| gatewayName |Nom de passerelle hello hello service Data Factory doit utiliser le magasin de données ODBC tooconnect toohello. |Oui |

#### <a name="example---using-basic-authentication"></a>Exemple : utilisation de l’authentification de base

```json
{
    "name": "ODBCLinkedService",
    "properties": {
        "type": "OnPremisesOdbc",
        "typeProperties": {
            "authenticationType": "Basic",
            "connectionString": "Driver={SQL Server};Server=Server.database.windows.net; Database=TestDatabase;",
            "userName": "username",
            "password": "password",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```
#### <a name="example---using-basic-authentication-with-encrypted-credentials"></a>Exemple : utilisation de l’authentification de base avec des informations d’identification chiffrées
Vous pouvez chiffrer les informations d’identification hello à l’aide de hello [New-AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) applet de commande (1.0 version d’Azure PowerShell) ou [New-AzureDataFactoryEncryptValue](https://msdn.microsoft.com/library/dn834940.aspx) (0,9 version ou antérieure de hello Azure PowerShell).  

```json
{
    "name": "ODBCLinkedService",
    "properties": {
        "type": "OnPremisesOdbc",
        "typeProperties": {
            "authenticationType": "Basic",
            "connectionString": "Driver={SQL Server};Server=myserver.database.windows.net; Database=TestDatabase;;EncryptedCredential=eyJDb25uZWN0...........................",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="example-using-anonymous-authentication"></a>Exemple : utilisation de l’authentification anonyme

```json
{
    "name": "ODBCLinkedService",
    "properties": {
        "type": "OnPremisesOdbc",
        "typeProperties": {
            "authenticationType": "Anonymous",
            "connectionString": "Driver={SQL Server};Server={servername}.database.windows.net; Database=TestDatabase;",
            "credential": "UID={uid};PWD={pwd}",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

Pour plus d’informations, consultez l’article [ODBC connector (connecteur ODBC)](data-factory-odbc-connector.md#linked-service-properties). 

### <a name="dataset"></a>Jeu de données
toodefine un jeu de données ODBC, jeu hello **type** du jeu de données hello trop**RelationalTable**et spécifiez hello propriétés Bonjour suivantes **typeProperties** section : 

| Propriété | Description | Requis |
| --- | --- | --- |
| TableName |Nom de table hello dans le magasin de données ODBC hello. |Oui |


#### <a name="example"></a>Exemple

```json
{
    "name": "ODBCDataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "ODBCLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
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

Pour plus d’informations, consultez l’article [ODBC connector (connecteur ODBC)](data-factory-odbc-connector.md#dataset-properties). 

### <a name="relational-source-in-copy-activity"></a>Source relationnelle dans l’activité de copie
Si vous copiez des données à partir d’une banque de données ODBC, la valeur hello **type de source de** Hello activité de copie trop**RelationalSource**et spécifiez les propriétés Bonjour suivantes **source** section :

| Propriété | Description | Valeurs autorisées | Requis |
| --- | --- | --- | --- |
| query |Utiliser des données tooread hello requête personnalisée. |Chaîne de requête SQL. Par exemple : `select * from MyTable`. |Oui |

#### <a name="example"></a>Exemple

```json
{
    "name": "CopyODBCToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "$$Text.Format('select * from MyTable where timestamp >= \\'{0:yyyy-MM-ddTHH:mm:ss}\\' AND timestamp < \\'{1:yyyy-MM-ddTHH:mm:ss}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "OdbcDataSet"
            }],
            "outputs": [{
                "name": "AzureBlobOdbcDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "OdbcToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
``` 

Pour plus d’informations, consultez l’article [ODBC connector (connecteur ODBC)](data-factory-odbc-connector.md#copy-activity-properties).

## <a name="salesforce"></a>Salesforce


### <a name="linked-service"></a>Service lié
le service ensemble hello lié toodefine une force de vente **type** Hello service lié trop**Salesforce**et spécifiez les propriétés Bonjour suivantes **typeProperties** section :  

| Propriété | Description | Requis |
| --- | --- | --- |
| environmentUrl | Spécifier l’instance d’URL de la force de vente hello. <br><br> - L’URL par défaut est « https://login.salesforce.com ». <br> -toocopy des données à partir de bac à sable, spécifiez « https://test.salesforce.com ». <br> -toocopy des données à partir d’un domaine personnalisé, spécifiez, par exemple, « https://[domain].my.salesforce.com ». |Non |
| username |Spécifiez un nom d’utilisateur pour le compte d’utilisateur hello. |Oui |
| password |Spécifiez un mot de passe pour le compte d’utilisateur hello. |Oui |
| securityToken |Spécifier un jeton de sécurité pour le compte d’utilisateur hello. Consultez [obtenir jeton de sécurité](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) pour obtenir des instructions sur la façon de tooreset/obtenir un jeton de sécurité. toolearn sur les jetons de sécurité en général, consultez [API de sécurité et hello](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_concepts_security.htm). |Oui |

#### <a name="example"></a>Exemple

```json
{
    "name": "SalesforceLinkedService",
    "properties": {
        "type": "Salesforce",
        "typeProperties": {
            "username": "<user name>",
            "password": "<password>",
            "securityToken": "<security token>"
        }
    }
}
```

Pour plus d’informations, consultez l’article [Salesforce connector (connecteur Salesforce)](data-factory-salesforce-connector.md#linked-service-properties). 

### <a name="dataset"></a>Jeu de données
toodefine un jeu de données Salesforce, jeu hello **type** du jeu de données hello trop**RelationalTable**et spécifiez hello propriétés Bonjour suivantes **typeProperties** section : 

| Propriété | Description | Requis |
| --- | --- | --- |
| TableName |Nom de table hello dans Salesforce. |Non (si une **requête** de type **RelationalSource** est spécifiée) |

#### <a name="example"></a>Exemple

```json
{
    "name": "SalesforceInput",
    "properties": {
        "linkedServiceName": "SalesforceLinkedService",
        "type": "RelationalTable",
        "typeProperties": {
            "tableName": "AllDataType__c"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
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

Pour plus d’informations, consultez l’article [Salesforce connector (connecteur Salesforce)](data-factory-salesforce-connector.md#dataset-properties). 

### <a name="relational-source-in-copy-activity"></a>Source relationnelle dans l’activité de copie
Si vous copiez des données à partir de la force de vente, la valeur hello **type de source de** Hello activité de copie trop**RelationalSource**et spécifiez les propriétés Bonjour suivantes **source** section :

| Propriété | Description | Valeurs autorisées | Requis |
| --- | --- | --- | --- |
| query |Utiliser des données tooread hello requête personnalisée. |Une requête SQL-92 ou une requête [SOQL (Salesforce Object Query Language)](https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/sforce_api_calls_soql.htm). Par exemple : `select * from MyTable__c`. |Non (si hello **tableName** Hello **dataset** est spécifié) |

#### <a name="example"></a>Exemple  



```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "SalesforceToAzureBlob",
            "description": "Copy from Salesforce tooan Azure blob",
            "type": "Copy",
            "inputs": [{
                "name": "SalesforceInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "SELECT Id, Col_AutoNumber__c, Col_Checkbox__c, Col_Currency__c, Col_Date__c, Col_DateTime__c, Col_Email__c, Col_Number__c, Col_Percent__c, Col_Phone__c, Col_Picklist__c, Col_Picklist_MultiSelect__c, Col_Text__c, Col_Text_Area__c, Col_Text_AreaLong__c, Col_Text_AreaRich__c, Col_URL__c, Col_Text_Encrypt__c, Col_Lookup__c FROM AllDataType__c"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

> [!IMPORTANT]
> Hello « __c » partie hello nom de l’API est nécessaire pour tout objet personnalisé.

Pour plus d’informations, consultez l’article [Salesforce connector (connecteur Salesforce)](data-factory-salesforce-connector.md#copy-activity-properties). 

## <a name="web-data"></a>Données Web 

### <a name="linked-service"></a>Service lié
le service ensemble hello lié toodefine un site Web **type** Hello service lié trop**Web**et spécifiez les propriétés Bonjour suivantes **typeProperties** section :  

| Propriété | Description | Requis |
| --- | --- | --- |
| Url |Source de l’URL toohello Web |Oui |
| authenticationType |Anonyme |Oui |
 

#### <a name="example"></a>Exemple


```json
{
    "name": "web",
    "properties": {
        "type": "Web",
        "typeProperties": {
            "authenticationType": "Anonymous",
            "url": "https://en.wikipedia.org/wiki/"
        }
    }
}
```

Pour plus d’informations, consultez l’article [Web Table connector (connecteur table web)](data-factory-web-table-connector.md#linked-service-properties). 

### <a name="dataset"></a>Jeu de données
toodefine un jeu de données Web, jeu hello **type** du jeu de données hello trop**WebTable**et spécifiez hello propriétés Bonjour suivantes **typeProperties** section : 

| Propriété | Description | Requis |
|:--- |:--- |:--- |
| type |Type de jeu de données hello. doit être défini trop**WebTable** |Oui |
| path |Une ressource URL toohello relative qui contient la table de hello. |Non. Lorsque le chemin d’accès n’est pas spécifié, seul hello URL spécifiée dans la définition de service hello lié est utilisé. |
| index |index de Hello de table hello dans la ressource de hello. Consultez [Get index d’une table dans une page HTML](#get-index-of-a-table-in-an-html-page) section pour l’index de toogetting étapes d’une table dans une page HTML. |Oui |

#### <a name="example"></a>Exemple

```json
{
    "name": "WebTableInput",
    "properties": {
        "type": "WebTable",
        "linkedServiceName": "WebLinkedService",
        "typeProperties": {
            "index": 1,
            "path": "AFI's_100_Years...100_Movies"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

Pour plus d’informations, consultez l’article [Web Table connector (connecteur table web)](data-factory-web-table-connector.md#dataset-properties). 

### <a name="web-source-in-copy-activity"></a>Source Web dans l’activité de copie
Si vous copiez des données à partir d’une table de web, définissez hello **type de source de** Hello activité de copie trop**WebSource**. Actuellement, lorsque source hello dans l’activité de copie est de type **WebSource**, aucune des propriétés supplémentaires ne sont pris en charge.

#### <a name="example"></a>Exemple

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "WebTableToAzureBlob",
            "description": "Copy from a Web table tooan Azure blob",
            "type": "Copy",
            "inputs": [{
                "name": "WebTableInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "WebSource"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

Pour plus d’informations, consultez l’article [Web Table connector (connecteur table web)](data-factory-web-table-connector.md#copy-activity-properties). 

## <a name="compute-environments"></a>ENVIRONNEMENTS DE CALCUL
Hello tableau suivant répertorie les environnements de calcul hello pris en charge par les activités de transformation de Data Factory et hello pouvant s’exécuter sur ces derniers. Cliquez sur lien hello pour le calcul de hello vous intéresser dans les schémas JSON toosee hello pour le service lié toolink de fabrique de données tooa. 

| Environnement de calcul | Activités |
| --- | --- |
| [Cluster HDInsight à la demande](#on-demand-azure-hdinsight-cluster) ou [votre propre cluster HDInsight](#existing-azure-hdinsight-cluster) |[Activité personnalisée .NET](#net-custom-activity), [Activité Hive](#hdinsight-hive-activity), [Activité pig](#hdinsight-pig-activity, [Activité MapReduce](#hdinsight-mapreduce-activity), [Activité de diffusion en continu Hadoop](#hdinsight-streaming-activityd), [Activité Spark](#hdinsight-spark-activity) |
| [Azure Batch](#azure-batch) |[Activité personnalisée .NET](#net-custom-activity) |
| [Azure Machine Learning](#azure-machine-learning) | [Activité d’exécution par lot Machine Learning](#machine-learning-batch-execution-activity), [Activité des ressources de mise à jour de Machine Learning](#machine-learning-update-resource-activity) |
| [Service Analytique Azure Data Lake](#azure-data-lake-analytics) |[Langage U-SQL du service Analytique Data Lake](#data-lake-analytics-u-sql-activity) |
| [Azure SQL Database](#azure-sql-database-1), [Azure SQL Data Warehouse](#azure-sql-data-warehouse-1), [SQL Server](#sql-server-1) |[Procédure stockée](#stored-procedure-activity) |

## <a name="on-demand-azure-hdinsight-cluster"></a>Cluster Azure HDInsight à la demande
Hello service Azure Data Factory peut créer automatiquement un données de tooprocess cluster basé sur Windows/Linux à la demande HDInsight. cluster de Hello est créé dans la même région que le compte de stockage hello (propriété linkedServiceName Bonjour JSON) associée au cluster de hello de hello. Vous pouvez exécuter hello suivant des activités de transformation de ce service lié : [les activités personnalisées .NET](#net-custom-activity), [Hive activité](#hdinsight-hive-activity), [porc activité] (#hdinsight--activité pig, [activité MapReduce ](#hdinsight-mapreduce-activity), [Activité de diffusion en continu Hadoop](#hdinsight-streaming-activityd), [nouvelles activités](#hdinsight-spark-activity). 

### <a name="linked-service"></a>Service lié 
Hello tableau suivant fournit des descriptions pour les propriétés de hello utilisées dans la définition de Azure JSON hello d’un service lié HDInsight de la demande.

| Propriété | Description | Requis |
| --- | --- | --- |
| type |propriété de type Hello doit être définie trop**HDInsightOnDemand**. |Oui |
| clusterSize |Nombre de nœuds de données des collaborateurs de cluster de hello. cluster HDInsight de Hello est créé avec 2 nœuds principal, ainsi que le nombre de hello de nœuds de travail que vous spécifiez pour cette propriété. les nœuds de Hello sont de taille D3 standard qui a 4 cœurs, pour un cluster de nœuds 4 worker prend 24 cœurs (4\*4 = 16 cœurs pour les nœuds de travail, ainsi que 2\*4 = 8 cœurs pour les nœuds principal). Consultez [Hadoop basé sur Linux de créer des clusters dans HDInsight](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md) pour plus d’informations sur la couche de hello D3 standard. |Oui |
| timetolive |Hello autorisé de temps d’inactivité pour le cluster de HDInsight hello à la demande. Spécifie la durée pendant laquelle hello à la demande HDInsight cluster reste actif après l’achèvement d’une activité à exécuter s’il en existe aucune autre tâche active dans le cluster de hello.<br/><br/>Par exemple, si une activité exécuter prend 6 minutes et la propriété timetolive est défini à too5 minutes, hello reste de cluster actif pendant 5 minutes après hello 6 minutes du traitement d’exécution de l’activité hello. Si l’exécution à une autre activité est exécutée avec la fenêtre de 6 minutes hello, il est traité par hello même cluster.<br/><br/>Création d’un cluster de HDInsight à la demande est une opération coûteuse (Impossible de prendre un certain temps), par conséquent, utilisez ce paramètre d’une fabrique de données de performances tooimprove nécessaires en réutilisant un cluster de HDInsight à la demande.<br/><br/>Si vous définissez la propriété timetolive valeur too0, cluster de hello est supprimé dès que l’activité hello exécuter dans traité. Sur hello autre part, si vous définissez une valeur élevée, le cluster de hello peut rester inactif inutilement entraîne des coûts élevés. Par conséquent, il est important que valeur hello approprié selon vos besoins.<br/><br/>Plusieurs pipelines peuvent partager hello la même instance de cluster de HDInsight à la demande hello si la valeur de la propriété timetolive hello est configuré correctement |Oui |
| version |Version du cluster HDInsight de hello. Pour plus d’informations, consultez [Versions de HDInsight prises en charge dans Azure Data Factory](data-factory-compute-linked-services.md#supported-hdinsight-versions-in-azure-data-factory). |Non |
| linkedServiceName |Toobe de service lié de stockage Azure utilisé par le cluster à la demande de hello pour le stockage et le traitement des données. <p>Actuellement, vous ne peut pas créer un cluster HDInsight à la demande qui utilise une Azure Data Lake Store en tant que stockage de hello. Si vous souhaitez que les données de résultat hello toostore de HDInsight de traitement dans un Azure Data Lake Store, utilisez un activité de copie toocopy hello des données de toohello de stockage d’objets Blob Azure hello Azure Data Lake Store.</p>  | Oui |
| additionalLinkedServiceNames |Spécifie les comptes de stockage supplémentaires pour hello HDInsight le service lié afin que le service de fabrique de données hello de les inscrire à votre place. |Non |
| osType |Type de système d'exploitation. Les valeurs autorisées sont Windows (par défaut) et Linux. |Non |
| hcatalogLinkedServiceName |nom de Hello de lié SQL Azure service point toohello HCatalog base de données. cluster de HDInsight Hello à la demande est créée à l’aide de la base de données SQL Azure hello en tant que le magasin de métadonnées hello. |Non |

### <a name="json-example"></a>Exemple JSON
Hello suivant JSON définit un service lié HDInsight à la demande sur Linux. Hello service Data Factory crée automatiquement un **basés sur Linux** cluster HDInsight lors du traitement d’une tranche de données. 

```json
{
    "name": "HDInsightOnDemandLinkedService",
    "properties": {
        "type": "HDInsightOnDemand",
        "typeProperties": {
            "version": "3.5",
            "clusterSize": 1,
            "timeToLive": "00:05:00",
            "osType": "Linux",
            "linkedServiceName": "StorageLinkedService"
        }
    }
}
```

Pour plus d’informations, consultez l’article [Compute linked services (services liés de calcul)](data-factory-compute-linked-services.md). 

## <a name="existing-azure-hdinsight-cluster"></a>Cluster Azure HDInsight existant
Vous pouvez créer un tooregister de service lié HDInsight Azure à votre propre cluster HDInsight avec la fabrique de données. Vous pouvez exécuter hello suivant des activités de transformation des données de ce service lié : [les activités personnalisées .NET](#net-custom-activity), [Hive activité](#hdinsight-hive-activity), [porc activité] (#hdinsight--activité pig, [MapReduce activité](#hdinsight-mapreduce-activity), [activité de diffusion en continu Hadoop](#hdinsight-streaming-activityd), [nouvelles activités](#hdinsight-spark-activity). 

### <a name="linked-service"></a>Service lié
Hello tableau suivant fournit des descriptions pour les propriétés de hello utilisées dans la définition de Azure JSON hello d’un service lié HDInsight Azure.

| Propriété | Description | Requis |
| --- | --- | --- |
| type |propriété de type Hello doit être définie trop**HDInsight**. |Oui |
| clusterUri |Hello URI du cluster HDInsight de hello. |Oui |
| username |Spécifier le nom hello de hello utilisateur toobe utilisé cluster HDInsight existant de tooconnect tooan. |Oui |
| password |Spécifiez le mot de passe de compte d’utilisateur hello. |Oui |
| linkedServiceName | Nom du service lié Azure Storage qui fait référence le stockage d’objets blob Azure toohello de hello utilisé par hello cluster HDInsight. <p>Actuellement, vous ne pouvez pas spécifier un service lié Azure Data Lake Store pour cette propriété. Données Bonjour Azure Data Lake Store sont accessibles à partir de scripts Hive/Pig si le cluster HDInsight de hello a accès toohello Data Lake Store. </p>  |Oui |

Pour obtenir la liste des versions des clusters HDInsight pris en charge, consultez [Versions de HDInsight prises en charge](data-factory-compute-linked-services.md#supported-hdinsight-versions-in-azure-data-factory). 

#### <a name="json-example"></a>Exemple JSON

```json
{
    "name": "HDInsightLinkedService",
    "properties": {
        "type": "HDInsight",
        "typeProperties": {
            "clusterUri": " https://<hdinsightclustername>.azurehdinsight.net/",
            "userName": "admin",
            "password": "<password>",
            "linkedServiceName": "MyHDInsightStoragelinkedService"
        }
    }
}
```

## <a name="azure-batch"></a>Azure Batch
Vous pouvez créer un tooregister de service lié Azure Batch un pool de traitement par lots de machines virtuelles (VM) avec une fabrique de données. Vous pouvez exécuter des activités personnalisées .NET à l'aide d'Azure Batch ou Azure HDInsight. Vous pouvez exécuter une [activité personnalisée .NET](#net-custom-activity) sur ce service lié. 

### <a name="linked-service"></a>Service lié
Hello tableau suivant fournit des descriptions pour les propriétés de hello utilisées dans la définition de Azure JSON hello d’un service lié Azure Batch.

| Propriété | Description | Requis |
| --- | --- | --- |
| type |propriété de type Hello doit être définie trop**AzureBatch**. |Oui |
| accountName |Nom du compte Azure Batch de hello. |Oui |
| accessKey |Clé d’accès pour hello compte Azure Batch. |Oui |
| poolName |Nom du pool hello d’ordinateurs virtuels. |Oui |
| linkedServiceName |Nom de hello service lié Azure Storage associé à ce service lié Azure Batch. Ce service lié est utilisé pour organiser des fichiers requis d’activité de hello toorun et le stockage des journaux de l’exécution d’activité hello. |Oui |


#### <a name="json-example"></a>Exemple JSON

```json
{
    "name": "AzureBatchLinkedService",
    "properties": {
        "type": "AzureBatch",
        "typeProperties": {
            "accountName": "<Azure Batch account name>",
            "accessKey": "<Azure Batch account key>",
            "poolName": "<Azure Batch pool name>",
            "linkedServiceName": "<Specify associated storage linked service reference here>"
        }
    }
}
```

## <a name="azure-machine-learning"></a>Azure Machine Learning
Vous créez un tooregister de service lié Azure Machine Learning un lot d’apprentissage calcul du score du point de terminaison avec une fabrique de données. Deux activités de transformation des données pouvant être exécutées sur ce service lié : [Activité d’exécution par lot Machine Learning](#machine-learning-batch-execution-activity), [Activité des ressources de mise à jour de Machine Learning](#machine-learning-update-resource-activity). 

### <a name="linked-service"></a>Service lié
Hello tableau suivant fournit des descriptions pour les propriétés de hello utilisées dans la définition de Azure JSON hello d’un service lié Azure Machine Learning.

| Propriété | Description | Requis |
| --- | --- | --- |
| Type |propriété de type Hello doit indiquer : **AzureML**. |Oui |
| mlEndpoint |lot Hello URL de calcul de score. |Oui |
| apiKey |Hello publiée API du modèle d’espace de travail. |Oui |

#### <a name="json-example"></a>Exemple JSON

```json
{
    "name": "AzureMLLinkedService",
    "properties": {
        "type": "AzureML",
        "typeProperties": {
            "mlEndpoint": "https://[batch scoring endpoint]/jobs",
            "apiKey": "<apikey>"
        }
    }
}
```

## <a name="azure-data-lake-analytics"></a>Service Analytique Azure Data Lake
Vous créez un **Analytique de LAC de données Azure** lié service toolink une fabrique de données Azure Analytique de LAC de données Azure compute service tooan avant d’utiliser hello [activité données Lake Analytique U-SQL](data-factory-usql-activity.md) dans un pipeline .

### <a name="linked-service"></a>Service lié

Hello tableau suivant fournit des descriptions pour les propriétés de hello utilisées dans la définition JSON de hello d’un service Azure données Lake Analytique est lié. 

| Propriété | Description | Requis |
| --- | --- | --- |
| Type |propriété de type Hello doit indiquer : **AzureDataLakeAnalytics**. |Oui |
| accountName |Nom du compte du service Analytique Azure Data Lake. |Oui |
| dataLakeAnalyticsUri |URI du service Analytique Azure Data Lake. |Non |
| autorisation |Code d’autorisation est automatiquement récupérée après avoir cliqué sur **Authorize** bouton hello éditeur Data Factory et de fin de connexion OAuth hello. |Oui |
| subscriptionId |ID d’abonnement Azure |Non (si non spécifié, abonnement Hello fabrique de données est utilisée). |
| resourceGroupName |Nom du groupe de ressources Azure |Non (si non spécifié, groupe de ressources de hello fabrique de données est utilisée). |
| sessionId |id de session à partir de la session de d’autorisation OAuth hello. Chaque ID de session est unique et ne peut être utilisé qu’une seule fois. Lorsque vous utilisez hello éditeur Data Factory, cet ID est généré automatiquement. |Oui |


#### <a name="json-example"></a>Exemple JSON
Hello l’exemple suivant fournit la définition JSON pour un service Azure données Lake Analytique est lié.

```json
{
    "name": "AzureDataLakeAnalyticsLinkedService",
    "properties": {
        "type": "AzureDataLakeAnalytics",
        "typeProperties": {
            "accountName": "<account name>",
            "dataLakeAnalyticsUri": "datalakeanalyticscompute.net",
            "authorization": "<authcode>",
            "sessionId": "<session ID>",
            "subscriptionId": "<subscription id>",
            "resourceGroupName": "<resource group name>"
        }
    }
}
```

## <a name="azure-sql-database"></a>Base de données SQL Azure
Vous créez un service lié SQL Azure et l’utiliser avec hello [activité de procédure stockée](#stored-procedure-activity) tooinvoke une procédure stockée à partir d’un pipeline de fabrique de données. 

### <a name="linked-service"></a>Service lié
le service ensemble hello lié toodefine une base de données SQL Azure **type** Hello service lié trop**AzureSqlDatabase**et spécifiez les propriétés Bonjour suivantes **typeProperties**section :  

| Propriété | Description | Requis |
| --- | --- | --- |
| connectionString |Spécifiez les informations nécessaires d’instance de base de données SQL Azure tooconnect toohello pour la propriété connectionString de hello. |Oui |

#### <a name="json-example"></a>Exemple JSON

```json
{
    "name": "AzureSqlLinkedService",
    "properties": {
        "type": "AzureSqlDatabase",
        "typeProperties": {
            "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
        }
    }
}
```

Pour plus d’informations sur ce service lié, consultez la page [Connecteur SQL Azure](data-factory-azure-sql-connector.md#linked-service-properties) .

## <a name="azure-sql-data-warehouse"></a>Azure SQL Data Warehouse
Vous créez un service Azure SQL Data Warehouse lié et l’utiliser avec hello [activité de procédure stockée](data-factory-stored-proc-activity.md) tooinvoke une procédure stockée à partir d’un pipeline de fabrique de données. 

### <a name="linked-service"></a>Service lié
le service ensemble hello lié toodefine un entrepôt de données SQL Azure **type** Hello service lié trop**AzureSqlDW**et spécifiez les propriétés Bonjour suivantes **typeProperties**section :  

| Propriété | Description | Requis |
| --- | --- | --- |
| connectionString |Spécifiez les informations nécessaires d’instance d’Azure SQL Data Warehouse tooconnect toohello pour la propriété connectionString de hello. |Oui |

#### <a name="json-example"></a>Exemple JSON

```json
{
    "name": "AzureSqlDWLinkedService",
    "properties": {
        "type": "AzureSqlDW",
        "typeProperties": {
            "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
        }
    }
}
```

Pour plus d’informations, consultez l’article [Azure SQL Data Warehouse connector (connecteur Azure SQL Data Warehouse)](data-factory-azure-sql-data-warehouse-connector.md#linked-service-properties). 

## <a name="sql-server"></a>SQL Server 
Vous créez un service lié SQL Server et l’utiliser avec hello [activité de procédure stockée](data-factory-stored-proc-activity.md) tooinvoke une procédure stockée à partir d’un pipeline de fabrique de données. 

### <a name="linked-service"></a>Service lié
Vous créez un service lié de type **OnPremisesSqlServer** toolink une fabrique de données de tooa de base de données locale SQL Server. Hello tableau suivant fournit la description du service de SQL Server lié JSON éléments tooon local spécifique.

Hello tableau suivant fournit la description pour JSON éléments tooSQL spécifique service du serveur lié.

| Propriété | Description | Requis |
| --- | --- | --- |
| type |propriété de type Hello doit indiquer : **OnPremisesSqlServer**. |Oui |
| connectionString |Spécifiez les informations connectionString nécessaires de base de données SQL Server tooconnect toohello local à l’aide de l’authentification Windows ou authentification SQL. |Oui |
| gatewayName |Nom de passerelle hello hello service Data Factory doit utiliser la base de données SQL Server tooconnect toohello local. |Oui |
| username |Spécifiez le nom d’utilisateur si vous utilisez l’authentification Windows. Exemple : **domainname\\username**. |Non |
| password |Spécifiez le mot de passe de compte d’utilisateur hello que vous avez spécifié pour le nom d’utilisateur hello. |Non |

Vous pouvez chiffrer les informations d’identification à l’aide de hello **New-AzureRmDataFactoryEncryptValue** applet de commande et les utiliser dans la chaîne de connexion hello comme indiqué dans hello exemple suivant (**EncryptedCredential** propriété) :  

```JSON
"connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=True;EncryptedCredential=<encrypted credential>",
```


#### <a name="example-json-for-using-sql-authentication"></a>Exemple : JSON pour utilisation de l’authentification SQL

```json
{
    "name": "MyOnPremisesSQLDB",
    "properties": {
        "type": "OnPremisesSqlServer",
        "typeProperties": {
            "connectionString": "Data Source=<servername>;Initial Catalog=MarketingCampaigns;Integrated Security=False;User ID=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```
#### <a name="example-json-for-using-windows-authentication"></a>Exemple : JSON pour utilisation de l’authentification Windows

Si le nom d’utilisateur et mot de passe sont spécifiés, la passerelle les utilise tooimpersonate hello base de données utilisateur spécifié compte tooconnect toohello locale SQL Server. Dans le cas contraire, la passerelle connecte toohello SQL Server directement avec le contexte de sécurité hello de passerelle (son compte de démarrage).

```json
{
    "Name": " MyOnPremisesSQLDB",
    "Properties": {
        "type": "OnPremisesSqlServer",
        "typeProperties": {
            "ConnectionString": "Data Source=<servername>;Initial Catalog=MarketingCampaigns;Integrated Security=True;",
            "username": "<domain\\username>",
            "password": "<password>",
            "gatewayName": "<gateway name>"
        }
    }
}
```

Pour plus d’informations, consultez l’article [SQL Server connector (connecteur SQL Server)](data-factory-sqlserver-connector.md#linked-service-properties).

## <a name="data-transformation-activities"></a>ACTIVITÉS DE TRANSFORMATION DES DONNÉES

Activité | Description
-------- | -----------
[Activité Hive HDInsight](#hdinsight-hive-activity) | Hello activité HDInsight Hive dans un pipeline de fabrique de données exécute des requêtes Hive vous-même ou un cluster de basés sur Windows/Linux de HDInsight à la demande. 
[Activité Pig HDInsight](#hdinsight-pig-activity) | Hello activité HDInsight Pig dans un pipeline de fabrique de données exécute des requêtes Pig vous-même ou un cluster de basés sur Windows/Linux de HDInsight à la demande.
[Activité MapReduce HDInsight](#hdinsight-mapreduce-activity) | Hello activité HDInsight MapReduce dans un pipeline Azure Data Factory exécute les programmes MapReduce vous-même ou un cluster de basés sur Windows/Linux de HDInsight à la demande.
[Activité de diffusion en continu HDInsight](#hdinsight-streaming-activity) | Hello activité de diffusion en continu HDInsight dans un pipeline Azure Data Factory exécute les programmes de diffusion en continu Hadoop sur votre propre ou un cluster de Windows/Linux-based de HDInsight à la demande.
[Activité HDInsight Spark](#hdinsight-spark-activity) | Hello activité HDInsight Spark dans un pipeline Azure Data Factory exécute les programmes Spark sur votre propre cluster HDInsight. 
[Activité d’exécution par lot Machine Learning](#machine-learning-batch-execution-activity) | Azure Data Factory permet tooeasily vous créer des pipelines qui utilisent un publiée Azure Machine Learning web de service pour l’analytique prédictive. À l’aide de hello activité d’exécution du lot dans un pipeline Azure Data Factory, vous pouvez appeler une prédictions de toomake du service web Machine Learning sur des données hello dans le lot. 
[Activité des ressources de mise à jour de Machine Learning](#machine-learning-update-resource-activity) | Au fil du temps, d’entrée de modèles prédictifs de hello Bonjour apprentissage expériences score doivent toobe reformé à l’aide de nouveaux jeux de données. Une fois que vous avez terminé avec le réapprentissage, vous souhaitez hello tooupdate calcul du score du service web avec hello reformés modèle d’apprentissage. Vous pouvez utiliser hello du service web hello tooupdate activité de ressources de mise à jour avec le modèle de hello qui vient d’être formé.
[Activité de procédure stockée](#stored-procedure-activity) | Vous pouvez utiliser l’activité de procédure stockée hello dans un tooinvoke de pipeline de fabrique de données dans une procédure stockée dans un des hello suivant des magasins de données : Azure SQL Database, Azure SQL Data Warehouse, base de données SQL Server dans votre entreprise ou d’une machine virtuelle Azure. 
[Activité U-SQL Data Lake Analytics](#data-lake-analytics-u-sql-activity) | L’activité U-SQL Data Lake Analytics exécute un script U-SQL sur un cluster Azure Data Lake Analytics.  
[Activité personnalisée .NET](#net-custom-activity) | Si vous avez besoin de données tootransform d’une manière qui n’est pas pris en charge par la fabrique de données, vous pouvez créer une activité personnalisée avec votre propre logique de traitement des données et utiliser l’activité hello dans le pipeline de hello. Vous pouvez configurer hello personnalisées .NET activité toorun à l’aide d’un service de traitement par lots Azure ou un cluster Azure HDInsight. 

     
## <a name="hdinsight-hive-activity"></a>Activité Hive HDInsight
Vous pouvez spécifier hello propriétés dans une définition JSON d’activité Hive suivantes. propriété de type Hello pour l’activité de hello doit être : **HDInsightHive**. Vous devez créer un service lié HDInsight tout d’abord et spécifier le nom hello de celui-ci en tant que valeur pour hello **linkedServiceName** propriété. Hello propriétés suivantes sont prises en charge hello **typeProperties** section lorsque vous définissez le type hello de tooHDInsightHive d’activité :

| Propriété | Description | Requis |
| --- | --- | --- |
| script |Spécifiez le script inline Hive de hello |Non |
| chemin d'accès du script |Hello du magasin Hive script dans un stockage d’objets blob Azure et fournir hello chemin d’accès toohello fichier. Utilisez la propriété ’script’ ou ’scriptPath’. Les deux propriétés ne peuvent pas être utilisées simultanément. nom de fichier Hello respecte la casse. |Non |
| defines |Spécifiez les paramètres en tant que paires clé/valeur pour le référencement dans le script Hive de hello à l’aide de 'hiveconf' |Non |

Ces propriétés sont spécifique toohello activité de la ruche. Autres propriétés (à l’extérieur de la section typeProperties hello) sont pris en charge pour toutes les activités.   

### <a name="json-example"></a>Exemple JSON
Hello suivant JSON définit une activité HDInsight Hive dans un pipeline.  

```json
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

Pour plus d’informations, consultez l’article [Hive Activity (activité Hive)](data-factory-hive-activity.md). 

## <a name="hdinsight-pig-activity"></a>Activité Pig HDInsight
Vous pouvez spécifier des propriétés dans une définition JSON d’activité Pig suivantes de hello. propriété de type Hello pour l’activité de hello doit être : **HDInsightPig**. Vous devez créer un service lié HDInsight tout d’abord et spécifier le nom hello de celui-ci en tant que valeur pour hello **linkedServiceName** propriété. Hello propriétés suivantes sont prises en charge hello **typeProperties** section lorsque vous définissez le type hello de tooHDInsightPig d’activité : 

| Propriété | Description | Requis |
| --- | --- | --- |
| script |Spécifiez hello Pig script inline |Non |
| chemin d'accès du script |Stocker le script Pig hello dans un stockage d’objets blob Azure et fournir hello chemin d’accès toohello fichier. Utilisez la propriété ’script’ ou ’scriptPath’. Les deux propriétés ne peuvent pas être utilisées simultanément. nom de fichier Hello respecte la casse. |Non |
| defines |Spécifiez les paramètres en tant que paires clé/valeur pour le référencement dans hello script Pig |Non |

Ces propriétés sont spécifique toohello activité Pig. Autres propriétés (à l’extérieur de la section typeProperties hello) sont pris en charge pour toutes les activités.   

### <a name="json-example"></a>Exemple JSON

```json
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

Pour plus d’informations, consultez l’article [Pig Activity (activité pig)](#data-factory-pig-activity.md). 

## <a name="hdinsight-mapreduce-activity"></a>Activité MapReduce HDInsight
Vous pouvez spécifier des propriétés dans une définition JSON d’activité MapReduce suivantes de hello. propriété de type Hello pour l’activité de hello doit être : **HDInsightMapReduce**. Vous devez créer un service lié HDInsight tout d’abord et spécifier le nom hello de celui-ci en tant que valeur pour hello **linkedServiceName** propriété. Hello propriétés suivantes sont prises en charge hello **typeProperties** section lorsque vous définissez le type hello de tooHDInsightMapReduce d’activité : 

| Propriété | Description | Requis |
| --- | --- | --- |
| jarLinkedService | Nom de hello lié service pourquoi le stockage Azure qui contient le fichier JAR hello. | Oui |
| jarFilePath | Chemin d’accès le fichier JAR toohello Bonjour Azure Storage. | Oui | 
| className | Nom de la classe principale hello dans le fichier JAR hello. | Oui | 
| arguments | Une liste séparée par des virgules des arguments de programme MapReduce de hello. Lors de l’exécution, vous consultez quelques arguments supplémentaires (par exemple : mapreduce.job.tags) à partir de l’infrastructure de MapReduce hello. toodifferentiate vos arguments avec des arguments de MapReduce hello, envisagez d’utiliser des option et la valeur en tant qu’arguments comme indiqué dans hello exemple suivant (- s,--entrée,--sortie, etc., sont immédiatement suivies par les valeurs des options) | Non | 

### <a name="json-example"></a>Exemple JSON

```json
{
    "name": "MahoutMapReduceSamplePipeline",
    "properties": {
        "description": "Sample Pipeline tooRun a Mahout Custom Map Reduce Jar. This job calculates an Item Similarity Matrix toodetermine hello similarity between two items",
        "activities": [
            {
                "type": "HDInsightMapReduce",
                "typeProperties": {
                    "className": "org.apache.mahout.cf.taste.hadoop.similarity.item.ItemSimilarityJob",
                    "jarFilePath": "adfsamples/Mahout/jars/mahout-examples-0.9.0.2.2.7.1-34.jar",
                    "jarLinkedService": "StorageLinkedService",
                    "arguments": ["-s", "SIMILARITY_LOGLIKELIHOOD", "--input", "wasb://adfsamples@spestore.blob.core.windows.net/Mahout/input", "--output", "wasb://adfsamples@spestore.blob.core.windows.net/Mahout/output/", "--maxSimilaritiesPerItem", "500", "--tempDir", "wasb://adfsamples@spestore.blob.core.windows.net/Mahout/temp/mahout"]
                },
                "inputs": [
                    {
                        "name": "MahoutInput"
                    }
                ],
                "outputs": [
                    {
                        "name": "MahoutOutput"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "retry": 3
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "MahoutActivity",
                "description": "Custom Map Reduce toogenerate Mahout result",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2017-01-03T00:00:00",
        "end": "2017-01-04T00:00:00"
    }
}
```

Pour plus d’informations, consultez l’article [MapReduce Activity (activité MapReduce)](data-factory-map-reduce.md). 

## <a name="hdinsight-streaming-activity"></a>Activité de diffusion en continu HDInsight
Vous pouvez spécifier hello propriétés dans une définition JSON d’activité de diffusion en continu Hadoop suivantes. propriété de type Hello pour l’activité de hello doit être : **HDInsightStreaming**. Vous devez créer un service lié HDInsight tout d’abord et spécifier le nom hello de celui-ci en tant que valeur pour hello **linkedServiceName** propriété. Hello propriétés suivantes sont prises en charge hello **typeProperties** section lorsque vous définissez le type hello de tooHDInsightStreaming d’activité : 

| Propriété | Description | 
| --- | --- |
| mappeur | Nom de l’exécutable du mappeur de hello. Dans l’exemple de hello, cat.exe est le Mappeur hello exécutable.| 
| raccord de réduction | Nom de l’exécutable du réducteur de hello. Dans l’exemple de hello, wc.exe est hello fichier exécutable du réducteur. | 
| entrée | Fichier d’entrée (y compris l’emplacement) pour le Mappeur hello. Dans l’exemple de hello : « wasb://adfsample@<account name>.blob.core.windows.net/example/data/gutenberg/davinci.txt » : adfsample est le conteneur d’objets blob hello, exemple/data/Gutenberg est hello dossier, et davinci.txt est l’objet blob de hello. |
| sortie | Fichier de sortie (y compris l’emplacement) pour le réducteur de hello. sortie de Hello du travail de diffusion en continu Hadoop hello est écrite emplacement toohello spécifiée pour cette propriété. |
| filePaths | Chemins d’accès pour les exécutables du Mappeur et du réducteur hello. Dans l’exemple de hello : « adfsample/example/apps/wc.exe », adfsample est le conteneur d’objets blob hello, exemple/apps est le dossier de hello et wc.exe est hello exécutable. | 
| fileLinkedService | Service lié de stockage Azure qui représente hello le stockage Azure qui contient les fichiers hello spécifiés dans la section de filePaths hello. | 
| arguments | Une liste séparée par des virgules des arguments de programme MapReduce de hello. Lors de l’exécution, vous consultez quelques arguments supplémentaires (par exemple : mapreduce.job.tags) à partir de l’infrastructure de MapReduce hello. toodifferentiate vos arguments avec des arguments de MapReduce hello, envisagez d’utiliser des option et la valeur en tant qu’arguments comme indiqué dans hello exemple suivant (- s,--entrée,--sortie, etc., sont immédiatement suivies par les valeurs des options) | 
| getDebugInfo | Un élément facultatif. Lorsqu’il est défini tooFailure, les journaux de hello sont téléchargés uniquement en cas d’échec. Lorsqu’il est défini tooAll, les journaux sont toujours téléchargées quel que soit l’état d’exécution hello. | 

> [!NOTE]
> Vous devez spécifier un dataset de sortie pour une activité de Streaming Hadoop de hello pour hello **génère** propriété. Ce jeu de données peut être uniquement un jeu de données factice qui est requis toodrive hello pipeline planification (horaire, quotidienne, etc.). Si l’activité hello n’accepte une entrée, vous pouvez ignorer la spécification d’un jeu de données d’entrée pour l’activité hello pour hello **entrées** propriété.  

## <a name="json-example"></a>Exemple JSON

```json
{
    "name": "HadoopStreamingPipeline",
    "properties": {
        "description": "Hadoop Streaming Demo",
        "activities": [
            {
                "type": "HDInsightStreaming",
                "typeProperties": {
                    "mapper": "cat.exe",
                    "reducer": "wc.exe",
                    "input": "wasb://<nameofthecluster>@spestore.blob.core.windows.net/example/data/gutenberg/davinci.txt",
                    "output": "wasb://<nameofthecluster>@spestore.blob.core.windows.net/example/data/StreamingOutput/wc.txt",
                    "filePaths": ["<nameofthecluster>/example/apps/wc.exe","<nameofthecluster>/example/apps/cat.exe"],
                    "fileLinkedService": "StorageLinkedService",
                    "getDebugInfo": "Failure"
                },
                "outputs": [
                    {
                        "name": "StreamingOutputDataset"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "name": "RunHadoopStreamingJob",
                "description": "Run a Hadoop streaming job",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2014-01-04T00:00:00",
        "end": "2014-01-05T00:00:00"
    }
}
```

Pour plus d’informations, consultez l’article [Hadoop Streaming Activity (activité de diffusion en continu Hadoop)](data-factory-hadoop-streaming-activity.md). 

## <a name="hdinsight-spark-activity"></a>Activité Spark HDInsight
Vous pouvez spécifier hello propriétés dans une définition JSON d’activité Spark suivantes. propriété de type Hello pour l’activité de hello doit être : **HDInsightSpark**. Vous devez créer un service lié HDInsight tout d’abord et spécifier le nom hello de celui-ci en tant que valeur pour hello **linkedServiceName** propriété. Hello propriétés suivantes sont prises en charge hello **typeProperties** section lorsque vous définissez le type hello de tooHDInsightSpark d’activité : 

| Propriété | Description | Requis |
| -------- | ----------- | -------- |
| rootPath | conteneur d’objets Blob Azure Hello et le dossier qui contient le fichier de Spark hello. nom de fichier Hello respecte la casse. | Oui |
| entryFilePath | Dossier racine du toohello chemin d’accès relatif de hello Spark/package de code. | Oui |
| className | Classe principale Java/Spark de l’application. | Non | 
| arguments | Une liste de programme de Spark toohello des arguments de ligne de commande. | Non | 
| proxyUser | programme Spark de Hello utilisateur compte tooimpersonate tooexecute hello | Non | 
| sparkConfig | Propriétés de configuration Spark. | Non | 
| getDebugInfo | Spécifie les fichiers journaux hello Spark toohello copié le stockage Azure utilisé par le cluster HDInsight (ou) spécifié par sparkJobLinkedService. Valeurs autorisées : Aucun, Toujours ou Échec. Valeur par défaut : Aucun. | Non | 
| sparkJobLinkedService | Hello service lié Azure Storage qui contient les journaux, les dépendances et les fichiers de travail hello Spark.  Si vous ne spécifiez pas une valeur pour cette propriété, le stockage de hello associé au cluster HDInsight est utilisé. | Non |

### <a name="json-example"></a>Exemple JSON

```json
{
    "name": "SparkPipeline",
    "properties": {
        "activities": [
            {
                "type": "HDInsightSpark",
                "typeProperties": {
                    "rootPath": "adfspark\\pyFiles",
                    "entryFilePath": "test.py",
                    "getDebugInfo": "Always"
                },
                "outputs": [
                    {
                        "name": "OutputDataset"
                    }
                ],
                "name": "MySparkActivity",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2017-02-05T00:00:00",
        "end": "2017-02-06T00:00:00"
    }
}
```
Hello Notez les points suivants : 

- Hello **type** propriété a la valeur trop**HDInsightSpark**.
- Hello **rootPath** est défini trop**adfspark\\pyFiles** où adfspark est le conteneur d’objets Blob Azure hello et pyFiles est un dossier précis dans le conteneur. Dans cet exemple, hello stockage d’objets Blob Azure est hello qui est associé au cluster de Spark hello. Vous pouvez télécharger hello fichier tooa stockage Azure différent. Si vous procédez ainsi, vous pouvez créer un toolink de service lié Azure Storage cette fabrique de données de stockage compte toohello. Ensuite, spécifiez le nom hello du service de hello lié en tant que valeur pour hello **sparkJobLinkedService** propriété. Consultez [propriétés de l’activité de Spark](#spark-activity-properties) pour plus d’informations sur cette propriété et d’autres propriétés prises en charge par hello Spark activité.
- Hello **entryFilePath** a la valeur toohello **test.py**, qui est le fichier de python hello. 
- Hello **getDebugInfo** propriété a la valeur trop**toujours**, ce qui signifie que les fichiers journaux de hello est toujours généré (succès ou échec).  

    > [!IMPORTANT]
    > Nous recommandons que vous ne définissez pas cette tooAlways de propriété dans un environnement de production, sauf si vous dépannez un problème. 
- Hello **génère** section a un jeu de données de sortie. Vous devez spécifier un jeu de données de sortie même si le programme de spark hello ne produit pas de sortie. planification de hello lecteurs Hello sortie dataset pour le pipeline de hello (horaire, quotidienne, etc.).

Pour plus d’informations sur l’activité hello, consultez [Spark activité](data-factory-spark.md) l’article.  

## <a name="machine-learning-batch-execution-activity"></a>Activité d’exécution par lot Machine Learning
Vous pouvez spécifier hello propriétés dans une définition JSON d’activité l’exécution du lot Azure ML suivantes. propriété de type Hello pour l’activité de hello doit être : **AzureMLBatchExecution**. Vous devez créer une Machine Azure tout d’abord le service lié d’apprentissage et spécifier le nom hello de celui-ci en tant que valeur pour hello **linkedServiceName** propriété. Hello propriétés suivantes sont prises en charge hello **typeProperties** section lorsque vous définissez le type hello de tooAzureMLBatchExecution d’activité :

Propriété | Description | Requis 
-------- | ----------- | --------
webServiceInput | Hello dataset toobe passé en tant qu’entrée pour le service web de Azure ML de hello. Ce jeu de données doit également être inclus dans les entrées de hello pour l’activité de hello. |Utilisez webServiceInput ou webServiceInputs. | 
webServiceInputs | Spécifier toobe de jeux de données transmises en tant qu’entrées pour le service web de Azure ML de hello. Si le service web de hello accepte plusieurs entrées, utilisez la propriété de webServiceInputs de hello au lieu d’utiliser la propriété de webServiceInput hello. Jeux de données qui est référencées par hello **webServiceInputs** doit également être inclus dans hello activité **entrées**. | Utilisez webServiceInput ou webServiceInputs. | 
webServiceOutputs | jeux de données Hello assignés en tant que sorties pour le service web de Azure ML hello. service web de Hello retourne des données de sortie dans ce jeu de données. | Oui | 
globalParameters | Spécifiez les valeurs des paramètres de service web hello dans cette section. | Non | 

### <a name="json-example"></a>Exemple JSON
Dans cet exemple, activité hello a hello dataset **MLSqlInput** en tant qu’entrée et **MLSqlOutput** en tant que sortie de hello. Hello **MLSqlInput** est passée comme un service web toohello d’entrée à l’aide de hello **webServiceInput** propriété JSON. Hello **MLSqlOutput** est passé en tant que sortie toohello Web service par à l’aide de hello **webServiceOutputs** propriété JSON. 

```json
{
   "name": "MLWithSqlReaderSqlWriter",
   "properties": {
      "description": "Azure ML model with sql azure reader/writer",
      "activities": [{
         "name": "MLSqlReaderSqlWriterActivity",
         "type": "AzureMLBatchExecution",
         "description": "test",
         "inputs": [ { "name": "MLSqlInput" }],
         "outputs": [ { "name": "MLSqlOutput" } ],
         "linkedServiceName": "MLSqlReaderSqlWriterDecisionTreeModel",
         "typeProperties":
         {
            "webServiceInput": "MLSqlInput",
            "webServiceOutputs": {
               "output1": "MLSqlOutput"
            },
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
         }
      }],
      "start": "2016-02-13T00:00:00",
       "end": "2016-02-14T00:00:00"
   }
}
```

Dans l’exemple de JSON hello, hello déployé Azure Machine Learning service Web utilise un lecteur et une writer module tooread/écrire des données à partir de / tooan base de données SQL Azure. Ce service Web expose hello quatre paramètres suivants : nom du serveur, nom de la base de données, le nom de compte d’utilisateur serveur et mot de passe utilisateur serveur de base de données.

> [!NOTE]
> Uniquement les entrées et sorties de hello AzureMLBatchExecution activité peuvent être passés en tant que paramètres toohello service Web. Par exemple, Bonjour ci-dessus extrait de code JSON, MLSqlInput est une activité AzureMLBatchExecution, qui est passée comme un service Web de toohello d’entrée via un paramètre de webServiceInput de toohello d’entrée.

## <a name="machine-learning-update-resource-activity"></a>Activité des ressources de mise à jour de Machine Learning
Vous pouvez spécifier hello propriétés dans une définition JSON d’activité ressource Azure ML mise à jour suivantes. propriété de type Hello pour l’activité de hello doit être : **AzureMLUpdateResource**. Vous devez créer une Machine Azure tout d’abord le service lié d’apprentissage et spécifier le nom hello de celui-ci en tant que valeur pour hello **linkedServiceName** propriété. Hello propriétés suivantes sont prises en charge hello **typeProperties** section lorsque vous définissez le type hello de tooAzureMLUpdateResource d’activité :

Propriété | Description | Requis 
-------- | ----------- | --------
trainedModelName | Nom de hello reformés modèle. | Oui |  
trainedModelDatasetName | Pointage toohello iLearner fichier DataSet retourné par hello réapprentissage d’opération. | Oui | 

### <a name="json-example"></a>Exemple JSON
pipeline de Hello a deux activités : **AzureMLBatchExecution** et **AzureMLUpdateResource**. Hello activité d’exécution du lot Azure ML prend les données d’apprentissage hello comme entrée et produit un fichier iLearner comme sortie. activité Hello appelle le service web de formation hello (expérience d’apprentissage exposé comme service web) avec une entrée hello données d’apprentissage et reçoit de fichier ilearner de hello de hello webservice. Hello placeholderBlob est simplement un dataset de sortie factice est requis par le pipeline hello toorun hello Azure Data Factory service.


```json
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
                    "trainedModelName": "trained model",
                    "trainedModelDatasetName" :  "trainedModelBlob"
                },
                "inputs": [{ "name": "trainedModelBlob" }],
                "outputs": [{ "name": "placeholderBlob" }],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "retry": 3
                },
                "name": "AzureML Update Resource",
                "linkedServiceName": "updatableScoringEndpoint2"
            }
        ],
        "start": "2016-02-13T00:00:00",
        "end": "2016-02-14T00:00:00"
    }
}
```

## <a name="data-lake-analytics-u-sql-activity"></a>Activité U-SQL Data Lake Analytics
Vous pouvez spécifier hello propriétés dans une définition JSON d’activité U-SQL suivantes. propriété de type Hello pour l’activité de hello doit être : **DataLakeAnalyticsU-SQL**. Vous devez créer un service Analytique de LAC de données Azure lié et spécifier le nom hello de celui-ci en tant que valeur pour hello **linkedServiceName** propriété. Hello propriétés suivantes sont prises en charge hello **typeProperties** section lorsque vous définissez le type hello activité tooDataLakeAnalyticsU-SQL : 

| Propriété | Description | Requis |
|:--- |:--- |:--- |
| scriptPath |Toofolder de chemin d’accès qui contient le script de hello U-SQL. Nom du fichier de hello respecte la casse. |Non (si vous utilisez le script) |
| scriptLinkedService |Service lié qui établit un lien stockage hello qui contient la fabrique de données hello script toohello |Non (si vous utilisez le script) |
| script |Spécifiez un script en ligne au lieu de spécifier scriptPath et scriptLinkedService. Par exemple : « script » : « Test CRÉER BASE DE DONNÉES ». |Non (si vous utilisez scriptPath et scriptLinkedService) |
| degreeOfParallelism |nombre maximal de Hello de nœuds utilisés simultanément tâche hello de toorun. |Non |
| priority |Détermine les tâches en dehors de tout ce qui sont en attente doivent être sélectionné toorun tout d’abord. Hello hello numéro inférieur, une priorité plus élevée hello hello. |Non |
| parameters |Paramètres de script de hello U-SQL |Non |

### <a name="json-example"></a>Exemple JSON

```json
{
    "name": "ComputeEventsByRegionPipeline",
    "properties": {
        "description": "This pipeline computes events for en-gb locale and date less than Feb 19, 2012.",
        "activities": 
        [
            {
                "type": "DataLakeAnalyticsU-SQL",
                "typeProperties": {
                    "scriptPath": "scripts\\kona\\SearchLogProcessing.txt",
                    "scriptLinkedService": "StorageLinkedService",
                    "degreeOfParallelism": 3,
                    "priority": 100,
                    "parameters": {
                        "in": "/datalake/input/SearchLog.tsv",
                        "out": "/datalake/output/Result.tsv"
                    }
                },
                "inputs": [
                    {
                        "name": "DataLakeTable"
                    }
                ],
                "outputs": 
                [
                    {
                        "name": "EventsByRegionTable"
                    }
                ],
                "policy": {
                    "timeout": "06:00:00",
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "name": "EventsByRegion",
                "linkedServiceName": "AzureDataLakeAnalyticsLinkedService"
            }
        ],
        "start": "2015-08-08T00:00:00",
        "end": "2015-08-08T01:00:00",
        "isPaused": false
    }
}
```

Pour plus d’informations, consultez [Activité U-SQL Data Lake Analytics](data-factory-usql-activity.md). 

## <a name="stored-procedure-activity"></a>Activité de procédure stockée
Vous pouvez spécifier hello propriétés dans une définition JSON d’activité procédure stockée suivantes. propriété de type Hello pour l’activité de hello doit être : **SqlServerStoredProcedure**. Vous devez créer une un Hello suivant des services liés et nommez hello du service de hello lié en tant que valeur pour hello **linkedServiceName** propriété :

- SQL Server 
- Base de données SQL Azure
- Azure SQL Data Warehouse

Hello propriétés suivantes sont prises en charge hello **typeProperties** section lorsque vous définissez le type hello de tooSqlServerStoredProcedure d’activité :

| Propriété | Description | Requis |
| --- | --- | --- |
| storedProcedureName |Spécifiez le nom hello de procédure stockée hello dans la base de données SQL Azure hello ou d’entrepôt de données SQL Azure qui est représenté par le service hello lié hello utilisations de table de sortie. |Oui |
| storedProcedureParameters |Spécifiez les valeurs des paramètres de procédure stockée. Si vous avez besoin de toopass null pour un paramètre, utilisez la syntaxe de hello : « param1 » : null (toutes les minuscules). Consultez hello suivant toolearn exemple sur l’utilisation de cette propriété. |Non |

Si vous ne spécifiez pas un jeu de données d’entrée, il doit être disponible (en état « Prêt ») pour hello stockées toorun d’activité de procédure. Hello de jeu de données d’entrée ne peut pas être utilisé dans la procédure stockée hello en tant que paramètre. Il est uniquement des dépendances hello toocheck utilisé avant l’activité de procédure stockée de départ hello. Vous devez spécifier un jeu de données de sortie pour une activité de procédure stockée. 

Dataset de sortie spécifie hello **planification** pour hello stockées activité de procédure (horaire, hebdomadaire, mensuelle, etc.). Hello dataset de sortie doit utiliser un **service lié** qui fait référence tooan de base de données SQL Azure ou d’un entrepôt de données SQL Azure ou d’une base de données SQL Server dans lequel vous souhaitez hello toorun de procédure stockée. Hello dataset de sortie puisse agir comme un moyen toopass hello de résultats de la procédure stockée hello pour un traitement ultérieur par une autre activité ([chaînage des propriétés des activités](data-factory-scheduling-and-execution.md##multiple-activities-in-a-pipeline)) dans le pipeline de hello. Toutefois, la fabrique de données n’écrit pas automatiquement sortie hello d’un dataset toothis de procédure stockée. Il est hello table SQL tooa écritures hello points de jeu de données de sortie à procédure stockée. Dans certains cas, le jeu de données de sortie hello peut être un **dataset factice**, qui est utilisé uniquement de l’activité de procédure stockée de toospecify hello planification de l’exécution hello.  

### <a name="json-example"></a>Exemple JSON

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
                "outputs": [{ "name": "sprocsampleout" }],
                "name": "SprocActivitySample"
            }
        ],
         "start": "2016-08-02T00:00:00",
         "end": "2016-08-02T05:00:00",
        "isPaused": false
    }
}
```

Pour plus de détails, consultez l’article [Stored Procedure Activity (activité de procédure stockée)](data-factory-stored-proc-activity.md). 

## <a name="net-custom-activity"></a>Activité personnalisée .NET
Vous pouvez spécifier hello propriétés dans une activité personnalisée de .NET définition JSON suivantes. propriété de type Hello pour l’activité de hello doit être : **DotNetActivity**. Vous devez créer un service lié HDInsight Azure ou un traitement par lots Azure liés de service et spécifiez nom hello du service de hello lié en tant que valeur pour hello **linkedServiceName** propriété. Hello propriétés suivantes sont prises en charge hello **typeProperties** section lorsque vous définissez le type hello de tooDotNetActivity d’activité :
 
| Propriété | Description | Requis |
|:--- |:--- |:--- |
| AssemblyName | Nom de l’assembly hello. Dans l’exemple de hello, il est : **MyDotnetActivity.dll**. | Oui |
| EntryPoint |Nom de classe hello qui implémente l’interface de IDotNetActivity hello. Dans l’exemple de hello, il est : **MyDotNetActivityNS.MyDotNetActivity** où MyDotNetActivityNS est l’espace de noms hello et MyDotNetActivity est la classe hello.  | Oui | 
| PackageLinkedService | Nom du service lié Azure Storage qui pointe de stockage d’objets blob toohello qui contient le fichier zip d’activité personnalisée hello de hello. Dans l’exemple de hello, il est : **AzureStorageLinkedService**.| Oui |
| PackageFile | Nom du fichier zip de hello. Dans l’exemple de hello, il est : **customactivitycontainer/MyDotNetActivity.zip**. | Oui |
| extendedProperties | Propriétés étendues que vous pouvez définir et passer sur toohello de code .NET. Dans cet exemple, hello **SliceStart** variable est définie la valeur tooa en fonction de la variable de système SliceStart hello. | Non | 

### <a name="json-example"></a>Exemple JSON

```json
{
  "name": "ADFTutorialPipelineCustom",
  "properties": {
    "description": "Use custom activity",
    "activities": [
      {
        "Name": "MyDotNetActivity",
        "Type": "DotNetActivity",
        "Inputs": [
          {
            "Name": "InputDataset"
          }
        ],
        "Outputs": [
          {
            "Name": "OutputDataset"
          }
        ],
        "LinkedServiceName": "AzureBatchLinkedService",
        "typeProperties": {
          "AssemblyName": "MyDotNetActivity.dll",
          "EntryPoint": "MyDotNetActivityNS.MyDotNetActivity",
          "PackageLinkedService": "AzureStorageLinkedService",
          "PackageFile": "customactivitycontainer/MyDotNetActivity.zip",
          "extendedProperties": {
            "SliceStart": "$$Text.Format('{0:yyyyMMddHH-mm}', Time.AddMinutes(SliceStart, 0))"
          }
        },
        "Policy": {
          "Concurrency": 2,
          "ExecutionPriorityOrder": "OldestFirst",
          "Retry": 3,
          "Timeout": "00:30:00",
          "Delay": "00:00:00"
        }
      }
    ],
    "start": "2016-11-16T00:00:00",
    "end": "2016-11-16T05:00:00",
    "isPaused": false
  }
}
```

Pour plus d’informations, consultez l’article [Use custom activities in Data Factory (utiliser des activités personnalisées dans Azure Data Factory)](data-factory-use-custom-activities.md). 

## <a name="next-steps"></a>Étapes suivantes
Hello suivant les didacticiels, consultez : 

- [Didacticiel : créer un pipeline avec une activité de copie](data-factory-copy-activity-tutorial-using-azure-portal.md)
- [Didacticiel : créer un pipeline avec une activité Hive](data-factory-build-your-first-pipeline-using-editor.md)