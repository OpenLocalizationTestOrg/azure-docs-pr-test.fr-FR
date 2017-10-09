---
title: "les Pipelines aaaCreate/planification, les activités de chaîne dans la fabrique de données | Documents Microsoft"
description: "En savoir plus toocreate un pipeline de données dans Azure Data Factory toomove et transformer des données. Créer un données pilotée par les informations de flux de travail tooproduce toouse prêt."
keywords: "pipeline de données, flux de travail piloté par les données"
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 13b137c7-1033-406f-aea7-b66f25b313c0
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/12/2017
ms.author: shlo
ms.openlocfilehash: 4a0fc20f98ce6453c16955e97fddb891926c173a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="pipelines-and-activities-in-azure-data-factory"></a>Pipelines et activités dans Azure Data Factory
Cet article vous aidera à comprendre comment pipelines et les activités dans Azure Data Factory et utiliser les workflows de piloté par les données de bout en bout tooconstruct votre le déplacement des données et les scénarios de traitement de données.  

> [!NOTE]
> Cet article suppose que vous avez parcouru [Introduction tooAzure Data Factory](data-factory-introduction.md). Si vous n’avez pas d’expérience pratique de création de fabriques de données, le [didacticiel relatif à la transformation de données](data-factory-build-your-first-pipeline.md) et/ou [le didacticiel relatif au déplacement de données](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) vous aidera à mieux comprendre cet article.  

## <a name="overview"></a>Vue d'ensemble
Une fabrique de données peut avoir un ou plusieurs pipelines. Un pipeline constitue un regroupement logique d’activités qui exécutent ensemble une tâche. activités Hello dans un pipeline de définissent les actions tooperform sur vos données. Par exemple, vous pouvez utiliser un copie activité toocopy des données d’une tooan de SQL Server locale stockage d’objets Blob Azure. Ensuite, utilisez une activité Hive qui exécute un script Hive sur une Azure HDInsight cluster tooprocess/transformer les données à partir des données de sortie tooproduce hello blob storage. Enfin, utilisez une deuxième copie activité toocopy hello sortie données tooan Azure SQL Data Warehouse sur le décisionnel (BI) des solutions de création de rapports sont générées. 

Une activité peut inclure zéro ou plusieurs [jeux de données](data-factory-create-datasets.md) d’entrée et produire un ou plusieurs [jeux de données](data-factory-create-datasets.md) de sortie. Hello diagramme suivant montre hello relation entre le pipeline, l’activité et jeu de données dans la fabrique de données : 

![Relation entre le pipeline, l’activité et le jeu de données](media/data-factory-create-pipelines/relationship-pipeline-activity-dataset.png)

Un pipeline vous permet de toomanage activités en tant qu’ensemble au lieu de chacun d’eux individuellement. Par exemple, vous pouvez déployer, planifier, suspendre et reprise d’un pipeline, au lieu de gérer indépendamment des activités dans le pipeline de hello.

Data Factory prend en charge deux types d’activités : les activités de déplacement des données et les activités de transformation des données. Chaque activité peut avoir zéro ou plusieurs [jeux de données](data-factory-create-datasets.md) d’entrée et produire un ou plusieurs jeux de données de sortie.

Un jeu de données d’entrée représente une entrée hello pour une activité dans le pipeline de hello et un jeu de données de sortie sortie hello pour l’activité de hello. Les jeux de données identifient les données dans différents magasins de données, par exemple des tables, des fichiers, des dossiers et des documents. Après avoir créé un jeu de données, vous pouvez l’utiliser avec des activités d’un pipeline. Un jeu de données peut, par exemple, constituer un jeu de données d’entrée/sortie d’une activité de copie ou d’une activité HDInsightHive. Pour plus d’informations sur les jeux de données, consultez l’article [Jeux de données dans Azure Data Factory](data-factory-create-datasets.md).

### <a name="data-movement-activities"></a>Activités de déplacement des données
Activité de copie dans la fabrique de données copie des données à partir d’un magasin de données de source données magasin tooa récepteur. Fabrique de données prend en charge hello suivant des magasins de données. Données à partir de n’importe quelle source peuvent être écrites tooany récepteur. Cliquez sur un toolearn de magasin de données comment tooand de données toocopy de ce magasin.

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

> [!NOTE]
> Stocke des données avec * peut être local ou sur Azure IaaS et vous obligent tooinstall [passerelle de gestion des données](data-factory-data-management-gateway.md) sur un ordinateur de IaaS Azure/le local.

Pour plus d’informations, consultez l’article [Activités de déplacement des données](data-factory-data-movement-activities.md).

### <a name="data-transformation-activities"></a>Activités de transformation des données
[!INCLUDE [data-factory-transformation-activities](../../includes/data-factory-transformation-activities.md)]

Pour plus d’informations, consultez l’article [Activités de déplacement des données](data-factory-data-transformation-activities.md).

### <a name="custom-net-activities"></a>Activités .NET personnalisées 
Si vous avez besoin des données toomove/à partir de données magasin qui hello activité de copie ne prend en charge, ou transformer des données à l’aide de votre propre logique, créez un **activité .NET personnalisée**. Pour plus d’informations sur la création et l’utilisation d’une activité personnalisée, consultez [Utilisation des activités personnalisées dans un pipeline Azure Data Factory](data-factory-use-custom-activities.md).

## <a name="schedule-pipelines"></a>Planifier des pipelines
Un pipeline est actif uniquement entre son heure de **début** et son heure de **fin**. Il n’est pas exécutée avant l’heure de début hello ou après l’heure de fin hello. Si le pipeline de hello est suspendu, il ne soit exécuté quelle que soit son heure de début et de fin. Pour un pipeline toorun, il ne doit pas être suspendu. Consultez [de planification et de l’exécution](data-factory-scheduling-and-execution.md) toounderstand le fonctionnement de planification et l’exécution dans Azure Data Factory.

## <a name="pipeline-json"></a>Pipeline JSON
Examinons de plus près la définition d’un pipeline au format JSON. structure générique de Hello pour un pipeline se présente comme suit :

```json
{
    "name": "PipelineName",
    "properties": 
    {
        "description" : "pipeline description",
        "activities":
        [

        ],
        "start": "<start date-time>",
        "end": "<end date-time>",
        "isPaused": true/false,
        "pipelineMode": "scheduled/onetime",
        "expirationTime": "15.00:00:00",
        "datasets": 
        [
        ]
    }
}
```

| Tag | Description | Requis |
| --- | --- | --- |
| name |Nom du pipeline de hello. Spécifiez un nom qui représente l’action hello hello pipeline effectue. <br/><ul><li>Nombre maximal de caractères : 260</li><li>Doit commencer par une lettre, un chiffre ou un trait de soulignement (_)</li><li>Les caractères suivants ne sont pas autorisés : « . », « + », « ? », « / », « < », « > », « * », « % », « & », « : », « \\ »</li></ul> |Oui |
| description | Spécifier le texte hello décrivant le pipeline hello est utilisé pour. |Oui |
| activités | Hello **activités** section peut avoir une ou plusieurs activités définies. Consultez hello la section suivante pour plus d’informations sur l’élément JSON activités hello. | Oui |  
| start | Date-heure de début pour le pipeline de hello. Doit se trouver au [format ISO](http://en.wikipedia.org/wiki/ISO_8601). Par exemple : `2016-10-14T16:32:41Z`. <br/><br/>Il est possible de toospecify une heure locale, par exemple une heure EST. Voici un exemple : `2016-02-27T06:00:00-05:00`, qui correspond à 6h EST.<br/><br/>Hello propriétés start et end spécifient ensemble la période active pour le pipeline de hello. Les tranches de sortie sont uniquement générées pendant cette période active. |Non<br/><br/>Si vous spécifiez une valeur pour la propriété de fin hello, vous devez spécifier la valeur de propriété de début hello.<br/><br/>Hello heures de début et de fin peuvent tous deux être vide toocreate un pipeline. Vous devez spécifier les deux valeurs tooset une période active pour hello pipeline toorun. Si vous ne spécifiez pas les heures de début et de fin lors de la création d’un pipeline, vous pouvez les définir à l’aide d’applet de commande hello ensemble-AzureRmDataFactoryPipelineActivePeriod plus tard. |
| end | Date-heure de fin pour le pipeline de hello. Si spécifiée, doit être au format ISO. Par exemple : `2016-10-14T17:32:41Z` <br/><br/>Il est possible de toospecify une heure locale, par exemple une heure EST. Voici un exemple : `2016-02-27T06:00:00-05:00`, qui correspond à 6h EST.<br/><br/>pipeline de hello toorun spécifiez indéfiniment, 9999-09-09 en tant que valeur hello pour la propriété de fin hello. <br/><br/> Un pipeline est actif uniquement entre son heure de début et son heure de fin. Il n’est pas exécutée avant l’heure de début hello ou après l’heure de fin hello. Si le pipeline de hello est suspendu, il ne soit exécuté quelle que soit son heure de début et de fin. Pour un pipeline toorun, il ne doit pas être suspendu. Consultez [de planification et de l’exécution](data-factory-scheduling-and-execution.md) toounderstand le fonctionnement de planification et l’exécution dans Azure Data Factory. |Non <br/><br/>Si vous spécifiez une valeur pour la propriété de démarrage hello, vous devez spécifier la valeur de propriété de fin hello.<br/><br/>Consultez les remarques pour hello **Démarrer** propriété. |
| isPaused | Si set tootrue, pipeline de hello ne s’exécute pas. Il a l’état hello suspendu. Valeur par défaut = false. Vous pouvez utiliser cette propriété tooenable ou désactiver un pipeline. |Non |
| pipelineMode | méthode Hello pour la planification s’exécute pour le pipeline de hello. Les valeurs autorisées sont : scheduled (par défaut) et onetime.<br/><br/>'Planifiée' indique ce pipeline hello s’exécute sur un intervalle de temps spécifié selon la période active de tooits (heure de début et de fin). « Unique » indique que ce pipeline hello s’exécute qu’une seule fois. Une fois créés, les pipelines de type onetime ne peuvent pas être modifiés ni mis à jour pour le moment. Consultez la page [Pipeline onetime](#onetime-pipeline) pour plus d’informations sur le paramètre onetime. |Non |
| expirationTime | Durée de temps après sa création pour le hello [à usage unique pipeline](#onetime-pipeline) est valide et doit rester mis en service. Si elle n’a pas tout actif, échec, ou en attente d’exécution, le pipeline de hello est automatiquement supprimé une fois qu’il atteint hello d’expiration. valeur par défaut de Hello :`"expirationTime": "3.00:00:00"`|Non |
| jeux de données |Liste des toobe de jeux de données utilisé par les activités définies dans le pipeline de hello. Cette propriété peut être utilisé toodefine des jeux de données spécifique toothis pipeline et non définies dans la fabrique de données hello. Les jeux de données définis dans ce pipeline ne peuvent être utilisés que par ce pipeline et ne peuvent pas être partagés. Pour plus d’informations, consultez la page [Étendue des jeux de données](data-factory-create-datasets.md#scoped-datasets) . |Non |

## <a name="activity-json"></a>Activité JSON
Hello **activités** section peut avoir une ou plusieurs activités définies. Chaque activité possède hello suivant la structure de niveau supérieur :

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
    },
    "scheduler":
    {
    }
}
```

Tableau suivant décrit les propriétés de l’activité hello définition JSON :

| Tag | Description | Requis |
| --- | --- | --- |
| name | Nom de l’activité hello. Spécifiez un nom qui représente l’action de hello activité hello effectue. <br/><ul><li>Nombre maximal de caractères : 260</li><li>Doit commencer par une lettre, un chiffre ou un trait de soulignement (_)</li><li>Les caractères suivants ne sont pas autorisés : « . », « + », « ? », « / », « < », « > », « * », « % », « & », « : », « \\ »</li></ul> |Oui |
| description | Texte décrivant ce hello activité ou ce qui est utilisé pour |Oui |
| type | Type d’activité hello. Consultez hello [les activités de déplacement des données](#data-movement-activities) et [activités de Transformation des données](#data-transformation-activities) sections pour les différents types d’activités. |Oui |
| inputs |Tables d’entrée utilisés par l’activité hello<br/><br/>`// one input table`<br/>`"inputs":  [ { "name": "inputtable1"  } ],`<br/><br/>`// two input tables` <br/>`"inputs":  [ { "name": "inputtable1"  }, { "name": "inputtable2"  } ],` |Oui |
| outputs |Tables de sortie utilisés par l’activité hello.<br/><br/>`// one output table`<br/>`"outputs":  [ { "name": "outputtable1" } ],`<br/><br/>`//two output tables`<br/>`"outputs":  [ { "name": "outputtable1" }, { "name": "outputtable2" }  ],` |Oui |
| linkedServiceName |Nom du service hello lié utilisé par l’activité hello. <br/><br/>Une activité peut nécessiter que vous spécifiez service hello lié qui lie l’environnement de calcul requis toohello. |Oui pour les activités HDInsight et de calcul de score Azure Machine Learning  <br/><br/>Non pour toutes les autres |
| typeProperties |Propriétés Bonjour **typeProperties** section varie selon le type d’activité hello. les propriétés de type toosee pour une activité, cliquez sur l’activité toohello de liens dans la section précédente de hello. | Non |
| policy |Stratégies qui affectent le comportement d’exécution hello d’activité hello. Si aucune valeur n’est spécifiée, les stratégies par défaut sont utilisées. |Non |
| scheduler | propriété de « planificateur » est utilisé toodefine souhaité pour l’activité hello. Sous-propriétés sont hello identique à celle de hello hello [propriété de disponibilité dans un jeu de données](data-factory-create-datasets.md#dataset-availability). |Non |


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

## <a name="sample-copy-pipeline"></a>Exemple de pipeline de copie
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
    "start": "2016-07-12T00:00:00Z",
    "end": "2016-07-13T00:00:00Z"
  }
} 
```

Hello Notez les points suivants :

* Dans la section d’activités hello, il n'existe qu’une seule activité dont **type** est défini trop**copie**.
* Entrée d’activité hello est définie trop**InputDataset** et de sortie d’activité hello est définie trop**OutputDataset**. Consultez l’article [Jeux de données](data-factory-create-datasets.md) pour en savoir plus sur la définition de jeux de données dans JSON. 
* Bonjour **typeProperties** section, **BlobSource** est spécifié comme type de source de hello et **SqlSink** est spécifié comme type de récepteur hello. Bonjour [les activités de déplacement des données](#data-movement-activities) , cliquez sur hello du magasin de données que vous souhaitez toouse comme source ou un récepteur toolearn plus d’informations sur le déplacement des données vers/à partir de ce magasin de données. 

Pour obtenir une description complète de la création de ce pipeline, consultez [didacticiel : copier des données à partir du stockage d’objets Blob tooSQL de base de données](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md). 

## <a name="sample-transformation-pipeline"></a>Exemple de pipeline de transformation
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
        "start": "2016-04-01T00:00:00Z",
        "end": "2016-04-02T00:00:00Z",
        "isPaused": false
    }
}
```

Hello Notez les points suivants : 

* Dans la section d’activités hello, il n'existe qu’une seule activité dont **type** est défini trop**HDInsightHive**.
* fichier de script Hive Hello, **partitionweblogs.hql**, est stocké dans hello compte de stockage Azure (spécifié par scriptLinkedService hello, appelé **AzureStorageLinkedService**) et dans  **script** dossier dans le conteneur de hello **adfgetstarted**.
* Hello `defines` section est de paramètres d’exécution utilisés toospecify hello script hive de toohello passés en tant que valeurs de configuration Hive (par exemple `${hiveconf:inputtable}`, `${hiveconf:partitionedtable}`).

Hello **typeProperties** section est différente pour chaque activité de transformation. toolearn sur les propriétés de type pris en charge pour une activité de transformation, cliquez sur l’activité de transformation hello Bonjour [activités de transformation des données](#data-transformation-activities) table. 

Pour obtenir une description complète de la création de ce pipeline, consultez [didacticiel : créer vos premières données tooprocess de pipeline à l’aide de cluster Hadoop](data-factory-build-your-first-pipeline.md). 

## <a name="multiple-activities-in-a-pipeline"></a>Plusieurs activités à l’intérieur d’un pipeline
pipelines de deux exemples précédents Hello ne contiennent qu’une seule activité. Un pipeline peut toutefois contenir plusieurs activités.  

Si vous avez plusieurs activités dans un pipeline et la sortie d’une activité n’est pas une entrée d’une autre activité, les activités hello peuvent s’exécuter en parallèle si de tranches de données d’entrée pour les activités de hello sont prêtes. 

Vous pouvez chaîner les deux activités à un dataset de sortie hello d’une activité en tant que jeu de données d’entrée hello Hello autre activité. la deuxième activité Hello s’exécute uniquement lorsque hello tout d’abord une se termine correctement.

![Chaînage des propriétés des activités Bonjour même pipeline](./media/data-factory-create-pipelines/chaining-one-pipeline.png)

Dans cet exemple, le pipeline de hello a deux activités : Activity1 et Activity2. Hello Activity1 prend Dataset1 comme entrée et produit une sortie Dataset2. Hello activité prend Dataset2 comme entrée et génère une sortie Dataset3. Depuis la sortie de hello de Activity1 (Dataset2) est entrée hello Activity2, hello Activity2 s’exécute uniquement après hello activité se termine correctement et produit hello Dataset2 tranche. Si hello Activity1 échoue pour une raison quelconque et ne produit pas de tranche de hello Dataset2, hello 2 de l’activité ne s’exécute pas pour ce secteur (par exemple : 9 AM too10 AM). 

Vous pouvez également chaîner des activités se trouvant dans des pipelines différents.

![Chaînage des activités dans deux pipelines](./media/data-factory-create-pipelines/chaining-two-pipelines.png)

Dans cet exemple, Pipeline1 ne contient qu’une seule activité qui utilise Dataset1 comme entrée et produit Dataset2 comme sortie. Hello Pipeline2 a également qu’une seule activité qui prend Dataset2 comme entrée et Dataset3 comme sortie. 

Pour plus d’informations, consultez [Planification et exécution](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline). 

## <a name="create-and-monitor-pipelines"></a>Créer et surveiller des pipelines
Vous pouvez créer des pipelines à l’aide de l’un de ces outils ou kits de développement logiciel (SDK). 

- Assistant Copie. 
- Portail Azure
- Visual Studio
- Azure PowerShell
- Modèle Azure Resource Manager
- API REST
- API .NET

Consultez hello suivant des didacticiels pour obtenir des instructions pour la création de pipelines à l’aide d’un de ces outils ou les kits de développement logiciel.
 
- [Créer un pipeline avec une activité de transformation des données](data-factory-build-your-first-pipeline.md)
- [Créer un pipeline avec une activité de déplacement des données](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)

Une fois qu’un pipeline est créé/déployé, vous pouvez gérer et surveiller vos pipelines à l’aide de hello panneaux portail Azure et un moniteur et gérer une application. Consultez hello rubriques pour obtenir des instructions suivantes. 

- [Surveillez et gérez les pipelines à l’aide des panneaux du portail Azure](data-factory-monitor-manage-pipelines.md).
- [Surveiller et gérer les pipelines à l’aide de l’application Surveiller et gérer](data-factory-monitor-manage-app.md)


## <a name="onetime-pipeline"></a>Pipeline onetime
Vous pouvez créer et planifier une toorun pipeline régulièrement (par exemple : toutes les heures ou tous les jours) au sein de hello début et de fin des heures que vous spécifiez dans la définition de pipeline hello. Pour plus d’informations, consultez [Planification des activités](#scheduling-and-execution) . Vous pouvez également créer un pipeline qui ne s’exécute qu’une seule fois. toodo par conséquent, vous définissez hello **pipelineMode** définition de propriété Bonjour pipeline trop**onetime** comme indiqué dans hello suivant l’exemple JSON. valeur par défaut de Hello pour cette propriété est **planifiée**.

```json
{
    "name": "CopyPipeline",
    "properties": {
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource",
                        "recursive": false
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "InputDataset"
                    }
                ],
                "outputs": [
                    {
                        "name": "OutputDataset"
                    }
                ]
                "name": "CopyActivity-0"
            }
        ]
        "pipelineMode": "OneTime"
    }
}
```

Notez hello suivantes :

* **Démarrer** et **fin** temps pour le pipeline de hello n’est spécifié.
* **Disponibilité** des entrées et sorties des jeux de données est spécifié (**fréquence** et **intervalle**), même si la fabrique de données n’utilise pas les valeurs hello.  
* La vue schématique n’affiche pas les pipelines à usage unique (onetime). Ce comportement est normal.
* Les pipelines à usage unique ne peuvent pas être mis à jour. Vous pouvez cloner un pipeline à usage unique, renommez-le, mettre à jour les propriétés et déployez-le toocreate un autre.


## <a name="next-steps"></a>Étapes suivantes
- Pour plus d’informations sur les jeux de données, consultez l’article [Créer des jeux de données](data-factory-create-datasets.md). 
- Pour plus d’informations sur la façon dont les pipelines sont planifiés et exécutés, consultez l’article [Planification et exécution dans Azure Data Factory](data-factory-scheduling-and-execution.md). 
  

