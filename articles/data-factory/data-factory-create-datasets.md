---
title: "jeux de données aaaCreate dans Azure Data Factory | Documents Microsoft"
description: "Découvrez comment les jeux de données toocreate dans Azure Data Factory, avec des exemples qui utilisent des propriétés, telles que décalage et anchorDateTime."
keywords: "créer un jeu de données, exemple de jeu de données, exemple offset"
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 0614cd24-2ff0-49d3-9301-06052fd4f92a
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2017
ms.author: shlo
ms.openlocfilehash: 181859ed250595d756df73e9ebcac08d9e7184c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="datasets-in-azure-data-factory"></a>Jeux de données dans Azure Data Factory
Cet article décrit les jeux de données, comment ils sont définis au format JSON et comment ils sont utilisés dans les pipelines d’Azure Data Factory. Il fournit des détails sur chaque section (par exemple, structure, disponibilité et stratégie) dans la définition JSON de jeu de données hello. Hello article fournit également des exemples d’utilisation de hello **offset**, **anchorDateTime**, et **style** propriétés dans une définition de jeu de données JSON.

> [!NOTE]
> Si vous êtes tooData nouvelle fabrique, consultez [Introduction tooAzure Data Factory](data-factory-introduction.md) pour une vue d’ensemble. Si vous n’avez pas l’expérience pratique de création de fabriques de données, vous pouvez obtenir une meilleure compréhension par la lecture de hello [didacticiel de transformation de données](data-factory-build-your-first-pipeline.md) et hello [didacticiel sur le déplacement des données](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md). 

## <a name="overview"></a>Vue d'ensemble
Une fabrique de données peut avoir un ou plusieurs pipelines. Un **pipeline** constitue un regroupement logique d’**activités** qui exécutent ensemble une tâche. activités Hello dans un pipeline de définissent les actions tooperform sur vos données. Par exemple, vous pouvez utiliser un copie activité toocopy des données d’une tooAzure de SQL Server locale stockage d’objets Blob. Ensuite, vous pouvez utiliser une activité Hive qui exécute un script Hive sur des données de tooprocess cluster Azure HDInsight à partir des données de sortie de tooproduce de stockage Blob. Enfin, vous pouvez utiliser une deuxième copie activité toocopy hello sortie données tooAzure SQL Data Warehouse, par-dessus le décisionnel (BI) reporting les solutions sont créées. Pour plus d’informations sur les pipelines et les activités, voir [Pipelines et activités dans Azure Data Factory](data-factory-create-pipelines.md).

Une activité peut inclure zéro ou plusieurs **jeux de données** d’entrée et produire un ou plusieurs jeux de données de sortie. Un jeu de données d’entrée représente une entrée hello pour une activité dans le pipeline de hello et un jeu de données de sortie sortie hello pour l’activité de hello. Les jeux de données identifient les données dans différents magasins de données, par exemple des tables, des fichiers, des dossiers et des documents. Par exemple, un jeu de données d’objets Blob Azure Spécifie le conteneur d’objets blob hello et le dossier de stockage d’objets Blob à partir de quels hello pipeline doit lire les données de hello. 

Avant de créer un jeu de données, créer un **service lié** toolink fabrique de données toohello du magasin de vos données. Services liés ressemblent aux chaînes de connexion, qui définissent les informations de connexion hello requises pour les ressources de tooexternal tooconnect Data Factory. Jeux de données identifient les données dans les magasins de données hello lié, tels que des tables SQL, des fichiers, des dossiers et des documents. Par exemple, un stockage Azure lié à des liens de service une fabrique de données de stockage compte toohello. Un jeu de données d’objets Blob Azure représente le conteneur d’objets blob hello et dossier hello contenant toobe d’objets BLOB d’entrée hello traité. 

Voici un exemple de scénario. toocopy des données à partir de la base de données Blob stockage tooa SQL, vous créez deux services liés : le stockage Azure et base de données SQL Azure. Ensuite, créez deux jeux de données : dataset d’objets Blob Azure (c'est-à-dire toohello lié Azure Storage service) et le jeu de données de Table de SQL Azure (qui fait référence le service de base de données SQL Azure lié toohello). Bonjour Azure Storage et la base de données SQL Azure Data Factory utilise respectivement au runtime tooconnect tooyour le stockage Azure et à la base de données SQL Azure, les chaînes de connexion contiennent des services liés. dataset d’objets Blob Azure Hello Spécifie le conteneur d’objets blob hello et le dossier d’objets blob qui contient des objets BLOB d’entrée de hello dans votre stockage d’objets Blob. jeu de données de Table de SQL Azure Hello spécifie hello SQL table dans les données de salutation toowhich votre base de données SQL est toobe copié.

Hello diagramme suivant présente hello relations entre pipeline, activité, jeu de données et le service lié dans la fabrique de données : 

![Relation entre le pipeline, l’activité, le jeu de données et les services liés](media/data-factory-create-datasets/relationship-between-data-factory-entities.png)

## <a name="dataset-json"></a>Jeu de données JSON
Un jeu de données dans la fabrique de données est défini au format JSON comme suit :

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
| name |Nom du jeu de données hello. Pour connaître les règles d’affectation des noms, voir [Azure Data Factory - Règles d’affectation des noms](data-factory-naming-rules.md). |Oui |N/D |
| type |Type de jeu de données hello. Spécifiez un des types hello pris en charge par la fabrique de données (par exemple : AzureBlob, AzureSqlTable). <br/><br/>Pour plus d’informations, consultez [Type du jeu de données](#Type). |Oui |N/D |
| structure |Schéma du jeu de données hello.<br/><br/>Pour plus d’informations, consultez [Structure d’un jeu de données](#Structure). |Non |N/D |
| typeProperties | propriétés de type Hello sont différentes pour chaque type (par exemple : objet Blob Azure, table SQL Azure). Pour plus d’informations sur les types hello pris en charge et leurs propriétés, consultez [type Dataset](#Type). |Oui |N/D |
| external | Indicateur booléen toospecify si un jeu de données est explicitement généré par un pipeline de fabrique de données ou non. Si hello un jeu de données d’entrée pour une activité n’est pas produit par le pipeline actuel de hello, définissez cette tootrue indicateur. Définissez cette tootrue indicateur pour hello un jeu de données d’entrée de la première activité hello dans le pipeline de hello.  |Non |false |
| availability | Définit hello fenêtre de traitement (par exemple, toutes les heures ou tous les jours) ou hello le découpage du modèle pour la production de dataset hello. Chaque unité de données consommée et produite pendant l’exécution d’une activité est appelée tranche de données. Si la disponibilité de hello d’un dataset de sortie est toodaily de jeu (fréquence - Day, intervalle de-1), une tranche est produite quotidiennement. <br/><br/>Pour plus d’informations, consultez [Disponibilité du jeu de données](#Availability). <br/><br/>Pour plus d’informations sur le jeu de données hello le découpage du modèle, consultez hello [de planification et de l’exécution](data-factory-scheduling-and-execution.md) l’article. |Oui |N/D |
| policy |Définit les critères de hello ou une condition hello tranches de dataset hello doivent répondre. <br/><br/>Pour plus d’informations, consultez hello [stratégie de groupe de données](#Policy) section. |Non |N/D |

## <a name="dataset-example"></a>Exemple de jeu de données
Dans l’exemple suivant de hello, hello dataset représente une table nommée **MyTable** dans une base de données SQL.

```json
{
    "name": "DatasetSample",
    "properties": {
        "type": "AzureSqlTable",
        "linkedServiceName": "AzureSqlLinkedService",
        "typeProperties":
        {
            "tableName": "MyTable"
        },
        "availability":
        {
            "frequency": "Day",
            "interval": 1
        }
    }
}
```

Hello Notez les points suivants :

* **type** a la valeur tooAzureSqlTable.
* **tableName** la propriété de type (type tooAzureSqlTable spécifique) a la valeur tooMyTable.
* **linkedServiceName** fait référence de service tooa lié de type AzureSqlDatabase, qui est définie dans l’extrait de code JSON suivant hello. 
* **fréquence de disponibilité** a la valeur tooDay, et **intervalle** a la valeur too1. Cela signifie que cette tranche de dataset hello est produite quotidiennement.  

**AzureSqlLinkedService** est défini comme suit :

```json
{
    "name": "AzureSqlLinkedService",
    "properties": {
        "type": "AzureSqlDatabase",
        "description": "",
        "typeProperties": {
            "connectionString": "Data Source=tcp:<servername>.database.windows.net,1433;Initial Catalog=<databasename>;User ID=<username>@<servername>;Password=<password>;Integrated Security=False;Encrypt=True;Connect Timeout=30"
        }
    }
}
```

Bonjour précédant l’extrait de code JSON :

* **type** a la valeur tooAzureSqlDatabase.
* **connectionString** propriété type spécifie des informations de base de données tooconnect tooa SQL.  

Comme vous pouvez le voir, hello service lié définit comment tooconnect tooa base de données SQL. jeu de données Hello définit quelle table est utilisée comme entrée et de sortie pour l’activité hello dans un pipeline.   

> [!IMPORTANT]
> Sauf si un jeu de données n’est produit par le pipeline de hello, il doit être marqué comme étant **externe**. Ce paramètre s’applique généralement à tooinputs de la première activité dans un pipeline.   


## <a name="Type"></a> Type du jeu de données
type Hello du jeu de données hello dépend du magasin de données hello. Consultez hello tableau pour obtenir la liste des magasins de données pris en charge par la fabrique de données suivant. Cliquez sur un toolearn de magasin de données comment toocreate un service lié et un jeu de données pour que les données de stockage.

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

> [!NOTE]
> Les magasins de données avec * peuvent être locaux ou sur l’infrastructure Azure en tant que service (IaaS). Ces magasins de données nécessitent tooinstall [passerelle de gestion des données](data-factory-data-management-gateway.md).

Dans l’exemple hello dans la section précédente de hello, type hello du jeu de données hello est défini trop**AzureSqlTable**. De même, pour un jeu de données d’objets Blob Azure, hello type du jeu de données hello est défini trop**AzureBlob**, comme indiqué dans hello suivant JSON :

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

## <a name="Structure"></a>Structure d’un jeu de données
Hello **structure** section est facultative. Il définit le schéma hello du jeu de données hello par contenant une collection de noms et types de données des colonnes. Vous utilisez hello section tooprovide type information de structure qui est utilisé tooconvert types et mapper les colonnes de destination de toohello hello source. Dans l’exemple suivant de hello, jeu de données hello possède trois colonnes : `slicetimestamp`, `projectname`, et `pageviews`. Elles sont respectivement de type String, String et Decimal.

```json
structure:  
[
    { "name": "slicetimestamp", "type": "String"},
    { "name": "projectname", "type": "String"},
    { "name": "pageviews", "type": "Decimal"}
]
```

Chaque colonne de structure de hello contient hello propriétés suivantes :

| Propriété | Description | Requis |
| --- | --- | --- |
| name |Nom de colonne de hello. |Oui |
| type |Type de données de colonne de hello.  |Non |
| culture |. Toobe culture basée sur le réseau utilisé lorsque le type de hello est un type .NET : `Datetime` ou `Datetimeoffset`. valeur par défaut Hello est `en-us`. |Non |
| format |Mettre en forme toobe de chaîne utilisé lorsque le type de hello est un type .NET : `Datetime` ou `Datetimeoffset`. |Non |

Hello indications suivantes vous aider à déterminer quand tooinclude structurer les informations et le tooinclude Bonjour **structure** section.

* **Pour les sources de données structurées**, spécifiez la section de structure hello uniquement si vous souhaitez mapper les colonnes de toosink de colonnes sources et leurs noms ne sont pas hello identiques. Ce type de source de données structurées stocke les informations de schéma et de type de données, ainsi que les données de salutation lui-même. SQL Server, Oracle et la table Azure sont des exemples de sources de données structurées. 
  
    Comme les informations de type sont déjà disponibles pour les sources de données structurées, vous ne devez pas inclure les informations de type lorsque vous incluez la section de structure hello.
* **Pour le schéma sur les sources de données de lecture (stockage d’objets Blob spécifiquement)**, vous pouvez choisir les données toostore sans stocker toutes les informations de type ou de schéma avec des données hello. Pour ces types de sources de données, incluez structure lorsque vous souhaitez que les colonnes toosink colonnes toomap source. Inclure également structure lorsque hello dataset est une entrée pour une activité de copie et de types de données de jeu de données source doivent être de types toonative converti pour le récepteur de hello. 
    
    Fabrique de données prend en charge hello valeurs pour fournir des informations de type de structure suivantes : **Int16, Int32, Int64, unique, Double, Decimal, Byte [], booléen, chaîne, Guid, Datetime, Datetimeoffset et Timespan**. Ces valeurs sont des valeurs de type basées sur .NET compatibles avec la norme CLS (Common Language Specification).

Fabrique de données effectue automatiquement les conversions de type lors du déplacement du magasin de données récepteur tooa du magasin de données à partir des données sources. 
  

## <a name="dataset-availability"></a>Disponibilité du jeu de données
Hello **disponibilité** section dans un jeu de données définit la fenêtre de traitement hello (par exemple, toutes les heures, tous les jours, ou toutes les semaines) pour le jeu de données hello. Pour plus d’informations sur les fenêtres d’activité, voir [Planification et exécution](data-factory-scheduling-and-execution.md).

Hello suivant la section disponibilité Spécifie que hello dataset de sortie soit produit toutes les heures ou jeu de données d’entrée hello est disponible, toutes les heures :

```json
"availability":    
{    
    "frequency": "Hour",        
    "interval": 1    
}
```

Si le pipeline de hello a hello après les heures de début et de fin :  

```json
    "start": "2016-08-25T00:00:00Z",
    "end": "2016-08-25T05:00:00Z",
```

Hello dataset de sortie est généré dans le pipeline de hello Démarrer toutes les heures et d’heure de fin. Par conséquent, cinq tranches de jeu de données sont générées par ce pipeline, une pour chaque fenêtre d’activité (0 h - 1 h, 1 h - 2 h, 2 h - 3 h, 3 h - 4 h, 4 h - 5 h). 

Hello tableau suivant décrit les propriétés que vous pouvez utiliser la section disponibilité hello :

| Propriété | Description | Requis | Default |
| --- | --- | --- | --- |
| frequency |Spécifie l’unité de temps hello pour la production de tranche de jeu de données.<br/><br/><b>Fréquence prise en charge</b>: minute, heure, jour, semaine, mois |Oui |N/D |
| interval |Spécifie un multiplicateur de fréquence.<br/><br/>« Intervalle de fréquence x » détermine la fréquence à laquelle hello tranche est produite. Par exemple, si vous avez besoin de hello toobe dataset découpée sur toutes les heures, vous définissez <b>fréquence</b> trop<b>heure</b>, et <b>intervalle</b> trop<b>1</b>.<br/><br/>Notez que si vous spécifiez **fréquence** en tant que **Minute**, vous devez définir hello intervalle toono inférieur à 15. |Oui |N/D |
| style |Spécifie si la tranche de hello doit être produite au démarrage de hello ou à la fin de l’intervalle de salutation.<ul><li>StartOfInterval</li><li>EndOfInterval</li></ul>Si **fréquence** est défini trop**mois**, et **style** est défini trop**EndOfInterval**, tranche de hello est produite sur hello dernier jour du mois. Si **style** est défini trop**StartOfInterval**, hello tranche est produite hello premier jour du mois.<br/><br/>Si **fréquence** est défini trop**jour**, et **style** est défini trop**EndOfInterval**, tranche de hello est produite dans hello dernière heure du jour de hello.<br/><br/>Si **fréquence** est défini trop**heure**, et **style** est défini trop**EndOfInterval**, tranche de hello est produite à fin hello d’heure de hello. Par exemple, pour une tranche de hello période de 13 h 00 - 14 h 00, la tranche de hello est produite à 14 heures. |Non |EndOfInterval |
| anchorDateTime |Définit la position absolue de hello dans le temps utilisé par les limites de la section hello planificateur toocompute jeu de données. <br/><br/>Notez que si cette propoerty comporte les parties de date qui sont plus précis hello spécifié fréquence, hello plus granulaires parties sont ignorés. Par exemple, si hello **intervalle** est **toutes les heures** (fréquence : heure et intervalle : 1) et hello **anchorDateTime** contient **minutes et secondes**, puis hello minutes et secondes des parties de **anchorDateTime** sont ignorés. |Non |01/01/0001 |
| Offset |Intervalle de temps par le hello début et fin de toutes les tranches de jeu de données sont déplacées. <br/><br/>Notez que si les deux **anchorDateTime** et **offset** est spécifié, les résultats hello sont hello combinée MAJ. |Non |N/D |

### <a name="offset-example"></a>exemple offset
Par défaut, les tranches quotidiennes (`"frequency": "Day", "interval": 1`) commencent à 12:00 (minuit), temps universel coordonné (UTC). Si vous souhaitez hello début toobe 6 h 00 UTC heure au lieu de cela, définissez hello décalage comme indiqué dans hello suivant extrait de code : 

```json
"availability":
{
    "frequency": "Day",
    "interval": 1,
    "offset": "06:00:00"
}
```
### <a name="anchordatetime-example"></a>Exemple anchorDateTime
Dans l’exemple suivant de hello, hello dataset se produit une fois toutes les 23 heures. Hello première tranche commence à heure hello spécifiée par **anchorDateTime**, qui est défini trop`2017-04-19T08:00:00` (UTC).

```json
"availability":    
{    
    "frequency": "Hour",        
    "interval": 23,    
    "anchorDateTime":"2017-04-19T08:00:00"    
}
```

### <a name="offsetstyle-example"></a>Exemple de décalage/style
Bonjour dataset suivant est tous les mois et est généré sur hello 3e de chaque mois à 8 h 00 (`3.08:00:00`) :

```json
"availability": {
    "frequency": "Month",
    "interval": 1,
    "offset": "3.08:00:00", 
    "style": "StartOfInterval"
}
```

## <a name="Policy"></a>Stratégie du jeu de données
Hello **stratégie** section dans la définition de dataset hello définit les critères de hello ou condition hello hello tranches de jeu de données doit répondre.

### <a name="validation-policies"></a>Stratégies de validation
| Nom de la stratégie | Description | Appliqué trop| Requis | Default |
| --- | --- | --- | --- | --- |
| minimumSizeMB |Valide les données hello **le stockage Blob Azure** répond aux hello exigences de taille minimale (en mégaoctets). |Stockage d'objets blob Azure |Non |N/D |
| minimumRows |Valide les données hello dans un **base de données SQL Azure** ou un **table Azure** contient hello le nombre minimal de lignes. |<ul><li>Base de données SQL Azure</li><li>Table Azure</li></ul> |Non |N/D |

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

**minimumRows :**

```json
"policy":
{
    "validation":
    {
        "minimumRows": 100
    }
}
```

### <a name="external-datasets"></a>Jeux de données externes
Jeux de données externes est hello ceux qui ne sont pas produits par un pipeline en cours d’exécution dans la fabrique de données hello. Si hello le jeu de données est marquée comme **externe**, hello **ExternalData** stratégie peut être le comportement de hello tooinfluence défini de la disponibilité de coupe de dataset hello.

À moins qu’un jeu de données ne soit généré par la fabrique de données, il doit être marqué comme **external**(externe). Ce paramètre s’applique généralement toohello les entrées de la première activité dans un pipeline, à moins que l’activité ou le chaînage des propriétés de pipeline sont utilisé.

| Nom | Description | Requis | Valeur par défaut |
| --- | --- | --- | --- |
| dataDelay |temps de Hello toodelay hello Vérifier disponibilité hello de données externes de hello pour hello donné tranche. Par exemple, vous pouvez retarder une vérification de toutes les heures à l’aide de ce paramètre.<br/><br/>Hello paramètre s’applique uniquement toohello moment présent.  Par exemple, si elle est de 1:00 PM maintenant et cette valeur est de 10 minutes, la validation hello démarre à 1 h 10.<br/><br/>Notez que ce paramètre n’affecte pas les tranches Bonjour passées. Les tranches avec **Slice End Time** + **dataDelay** < **Now** sont traitées sans aucun délai.<br/><br/>Fois supérieure à 23:59 heures doivent être spécifiés à l’aide de hello `day.hours:minutes:seconds` format. Par exemple, toospecify 24 heures, n’utilisez pas 24:00:00. Utilisez plutôt 1.00:00:00. Si vous utilisez 24:00:00, cette valeur est traitée comme 24 jours (24.00:00:00). Pour 1 jour et 4 heures, spécifiez 1:04:00:00. |Non |0 |
| retryInterval |temps d’attente Hello entre un échec et hello prochaine tentative. Ce paramètre s’applique toopresent heure. Si vous essayez de hello précédente a échoué, la prochaine tentative de hello est après hello **retryInterval** période. <br/><br/>S’il s’agit de 1:00 PM dès maintenant, nous commençons hello première tentative. Si hello durée toocomplete hello premier contrôle de validation est 1 minute et échoué de l’opération hello, nouvelle tentative suivante d’hello est à 1:00 + 1 min (durée) + 1 minute (intervalle avant nouvelle tentative) = 1:02 PM. <br/><br/>Aux tranches passées de hello, il n’existe aucun délai. nouvelle tentative de Hello se produit immédiatement. |Non |00:01:00 (1 minute) |
| retryTimeout |délai d’expiration de Hello pour chaque nouvelle tentative.<br/><br/>Si cette propriété a la valeur too10 minutes, la validation hello doit être effectuée dans les 10 minutes. Si elle dure plus longtemps que la validation de 10 minutes tooperform hello, hello recommencez arrive à expiration.<br/><br/>Si toutes les tentatives pour hello validation expirent, hello tranche est marquée comme **TimedOut**. |Non |00:10:00 (10 minutes) |
| maximumRetry |Hello fréquence toocheck pour la disponibilité de données externes de hello hello. Hello valeur maximale autorisée est de 10. |Non |3 |


## <a name="create-datasets"></a>Créer des jeux de données
Vous pouvez créer des jeux de données à l’aide de l’un de ces outils ou kits de développement logiciel (SDK) : 

- Assistant de copie 
- Portail Azure
- Visual Studio
- PowerShell
- Modèle Azure Resource Manager
- API REST
- API .NET

Consultez hello suivant des didacticiels pour obtenir des instructions pour la création de pipelines et les jeux de données en utilisant l’une de ces outils ou les kits de développement logiciel :
 
- [Créer un pipeline avec une activité de transformation des données](data-factory-build-your-first-pipeline.md)
- [Créer un pipeline avec une activité de déplacement des données](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)

Après un pipeline est créé et déployé, vous pouvez gérer et surveiller vos pipelines à l’aide de hello panneaux portail Azure ou une application de gestion et de surveillance hello. Consultez hello rubriques pour obtenir des instructions pas à pas suivantes : 

- [Surveiller et gérer les pipelines à l’aide des panneaux du portail Azure](data-factory-monitor-manage-pipelines.md)
- [Surveiller et gérer des pipelines à l’aide d’application de gestion et de surveillance hello](data-factory-monitor-manage-app.md)


## <a name="scoped-datasets"></a>Étendue des jeux de données
Vous pouvez créer des jeux de données qui est incluses dans l’étendue tooa pipeline à l’aide de hello **datasets** propriété. Ces jeux de données peuvent uniquement être utilisés par les activités dans ce pipeline, et non pas par les activités d’autres pipelines. Bonjour à l’exemple suivant définit un pipeline avec toobe (InputDataset-rdc et OutputDataset-rdc) deux jeux de données utilisé dans le pipeline de hello.  

> [!IMPORTANT]
> Jeux de données incluses dans l’étendue est pris en charge uniquement avec des pipelines à usage unique (où **pipelineMode** est défini trop**OneTime**). Pour plus d’informations, consultez [Pipeline onetime](data-factory-create-pipelines.md#onetime-pipeline) .
>
>

```json
{
    "name": "CopyPipeline-rdc",
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
                        "name": "InputDataset-rdc"
                    }
                ],
                "outputs": [
                    {
                        "name": "OutputDataset-rdc"
                    }
                ],
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1,
                    "style": "StartOfInterval"
                },
                "name": "CopyActivity-0"
            }
        ],
        "start": "2016-02-28T00:00:00Z",
        "end": "2016-02-28T00:00:00Z",
        "isPaused": false,
        "pipelineMode": "OneTime",
        "expirationTime": "15.00:00:00",
        "datasets": [
            {
                "name": "InputDataset-rdc",
                "properties": {
                    "type": "AzureBlob",
                    "linkedServiceName": "InputLinkedService-rdc",
                    "typeProperties": {
                        "fileName": "emp.txt",
                        "folderPath": "adftutorial/input",
                        "format": {
                            "type": "TextFormat",
                            "rowDelimiter": "\n",
                            "columnDelimiter": ","
                        }
                    },
                    "availability": {
                        "frequency": "Day",
                        "interval": 1
                    },
                    "external": true,
                    "policy": {}
                }
            },
            {
                "name": "OutputDataset-rdc",
                "properties": {
                    "type": "AzureBlob",
                    "linkedServiceName": "OutputLinkedService-rdc",
                    "typeProperties": {
                        "fileName": "emp.txt",
                        "folderPath": "adftutorial/output",
                        "format": {
                            "type": "TextFormat",
                            "rowDelimiter": "\n",
                            "columnDelimiter": ","
                        }
                    },
                    "availability": {
                        "frequency": "Day",
                        "interval": 1
                    },
                    "external": false,
                    "policy": {}
                }
            }
        ]
    }
}
```

## <a name="next-steps"></a>Étapes suivantes
- Pour plus d’informations sur les pipelines, voir [Créer des pipelines](data-factory-create-pipelines.md). 
- Pour plus d’informations sur la façon dont les pipelines sont planifiés et exécutés, voir [Planification et exécution dans Azure Data Factory](data-factory-scheduling-and-execution.md). 
