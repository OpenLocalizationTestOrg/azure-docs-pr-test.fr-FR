---
title: "aaaMove des données à partir de la force de vente à l’aide de Data Factory | Documents Microsoft"
description: "En savoir plus sur la façon de toomove les données à partir de la force de vente à l’aide d’Azure Data Factory."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: dbe3bfd6-fa6a-491a-9638-3a9a10d396d1
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: c1bde2a333f5a3c0a995eb8c13ecf585132888b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-salesforce-by-using-azure-data-factory"></a>Déplacer des données depuis Salesforce à l’aide d’Azure Data Factory
Cet article décrit comment vous pouvez utiliser l’activité de copie dans un Azure data factory toocopy données Salesforce tooany magasin de données qui est répertorié sous la colonne de récepteur hello Bonjour [prise en charge des sources et récepteurs](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table. Cet article s’appuie sur hello [les activités de déplacement des données](data-factory-data-movement-activities.md) article, qui présente une vue d’ensemble du déplacement des données avec l’activité de copie et de combinaisons de magasin de données pris en charge.

Azure Data Factory prend actuellement en charge uniquement le déplacement des données à partir de Salesforce trop[prise en charge des magasins de données récepteur](data-factory-data-movement-activities.md#supported-data-stores-and-formats), mais ne prend pas en charge le déplacement des données d’autres tooSalesforce de magasins de données.

## <a name="supported-versions"></a>Versions prises en charge
Ce connecteur prend en charge hello suivant des éditions de Salesforce : Developer Edition, Professional Edition, Enterprise Edition ou illimité Edition. Et il prend en charge la copie de production Salesforce, bac à sable (sandbox) et domaine personnalisé.

## <a name="prerequisites"></a>Composants requis
* L’autorisation d’API doit être activée. Consultez l’article [How do I enable API access in Salesforce by permission set?](https://www.data2crm.com/migration/faqs/enable-api-access-salesforce-permission-set/)
* toocopy des données à partir des magasins de données Salesforce tooon local, vous devez disposer au moins données Management Gateway 2.0 est installé dans votre environnement local.

## <a name="salesforce-request-limits"></a>Limites des requêtes Salesforce
Salesforce prend en charge un nombre limité de requêtes d’API totales et de requêtes d’API simultanées. Hello Notez les points suivants :

- Si le nombre de hello de demandes simultanées dépasse la limite de hello, la limitation se produit et vous verrez des échecs aléatoires.
- Si le nombre total de hello de demandes dépasse la limite de hello, hello compte Salesforce sera bloqué pour 24 heures.

Vous pouvez aussi recevoir l’erreur de « REQUEST_LIMIT_EXCEEDED » hello dans les deux scénarios. Consultez la section hello « API limites des demandes » hello [limites de développeur Salesforce](http://resources.docs.salesforce.com/200/20/en-us/sfdc/pdf/salesforce_app_limits_cheatsheet.pdf) article pour plus d’informations.

## <a name="getting-started"></a>Prise en main
Vous pouvez créer un pipeline avec une activité de copie qui déplace les données de Salesforce en utilisant différents outils/API.

toocreate de façon plus simple Hello un pipeline est toouse hello **Assistant copie de**. Consultez [didacticiel : créer un pipeline à l’aide d’Assistant copie de](data-factory-copy-data-wizard-tutorial.md) pour une procédure pas à pas rapides sur la création d’un pipeline à l’aide d’Assistant de données de copie hello.

Vous pouvez également utiliser hello suivant outils toocreate un pipeline : **portail Azure**, **Visual Studio**, **Azure PowerShell**, **modèle Azure Resource Manager** , **API .NET**, et **API REST**. Consultez [didacticiel d’activité de copie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) pour obtenir des instructions toocreate un pipeline avec une activité de copie. 

Si vous utilisez hello ou une API, vous effectuez hello suivant les étapes toocreate un pipeline qui déplace la banque de données récepteur tooa du magasin de données à partir des données d’une source : 

1. Créer **services liés** fabrique de données tooyour toolink les données d’entrée et de sortie magasins.
2. Créer **datasets** toorepresent d’entrée et sortie l’opération de copie des données pour hello. 
3. Création d’un **pipeline** avec une activité de copie qui utilise un jeu de données en tant qu’entrée et un jeu de données en tant que sortie. 

Lorsque vous utilisez hello Assistant, les définitions de JSON pour ces entités de fabrique de données (services liés, des datasets et pipeline de hello) sont créées automatiquement pour vous. Lorsque vous utilisez/API des outils (à l’exception des API .NET), vous définissez ces entités de fabrique de données à l’aide du format JSON de hello.  Pour voir un exemple avec des définitions de JSON pour les entités de fabrique de données qui sont utilisés toocopy des données à partir de Salesforce, [exemple de JSON : copier des données à partir de Salesforce tooAzure Blob](#json-example-copy-data-from-salesforce-to-azure-blob) section de cet article. 

Hello les sections suivantes fournit des détails sur les propriétés JSON qui sont utilisés toodefine Data Factory entités spécifique tooSalesforce : 

## <a name="linked-service-properties"></a>Propriétés du service lié
Hello tableau suivant fournit des descriptions pour les éléments JSON toohello spécifique au service lié de Salesforce.

| Propriété | Description | Requis |
| --- | --- | --- |
| type |propriété de type Hello doit indiquer : **Salesforce**. |Oui |
| environmentUrl | Spécifier l’instance d’URL de la force de vente hello. <br><br> - L’URL par défaut est « https://login.salesforce.com ». <br> -toocopy des données à partir de bac à sable, spécifiez « https://test.salesforce.com ». <br> -toocopy des données à partir d’un domaine personnalisé, spécifiez, par exemple, « https://[domain].my.salesforce.com ». |Non |
| username |Spécifiez un nom d’utilisateur pour le compte d’utilisateur hello. |Oui |
| password |Spécifiez un mot de passe pour le compte d’utilisateur hello. |Oui |
| securityToken |Spécifier un jeton de sécurité pour le compte d’utilisateur hello. Consultez [obtenir jeton de sécurité](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) pour obtenir des instructions sur la façon de tooreset/obtenir un jeton de sécurité. toolearn sur les jetons de sécurité en général, consultez [API de sécurité et hello](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_concepts_security.htm). |Oui |

## <a name="dataset-properties"></a>Propriétés du jeu de données
Pour obtenir une liste complète des sections et les propriétés qui sont disponibles pour définir des jeux de données, consultez hello [création de datasets](data-factory-create-datasets.md) l’article. Les sections comme la structure, la disponibilité et la stratégie d’un jeu de données JSON sont similaires pour tous les types de jeux de données (SQL Azure, Azure Blob, Azure Table, etc.).

Hello **typeProperties** section est différente pour chaque type de jeu de données et fournit des informations sur l’emplacement de hello de données hello dans le magasin de données hello. Hello typeProperties section pour un jeu de données de type de hello **RelationalTable** a hello propriétés suivantes :

| Propriété | Description | Requis |
| --- | --- | --- |
| TableName |Nom de table hello dans Salesforce. |Non (si une **requête** de type **RelationalSource** est spécifiée) |

> [!IMPORTANT]
> Hello « __c » partie hello nom de l’API est nécessaire pour tout objet personnalisé.

![Connexion Salesforce - Data Factory - Nom de l’API](media/data-factory-salesforce-connector/data-factory-salesforce-api-name.png)

## <a name="copy-activity-properties"></a>Propriétés de l’activité de copie
Pour obtenir une liste complète des sections et des propriétés qui sont disponibles pour la définition d’activités, consultez hello [création de pipelines](data-factory-create-pipelines.md) l’article. Les propriétés telles que le nom, la description, les tables d’entrée et de sortie, les différentes stratégies, etc. sont disponibles pour tous les types d’activités.

propriétés de Hello qui sont disponibles dans hello section typeProperties d’activité hello sur hello autre part, varient selon chaque type d’activité. Pour l’activité de copie, ils varient selon les types de sources et récepteurs hello.

Dans l’activité de copie, lors de la source de hello est de type de hello **RelationalSource** (qui inclut Salesforce), hello propriétés suivantes est disponible dans la section de typeProperties :

| Propriété | Description | Valeurs autorisées | Requis |
| --- | --- | --- | --- |
| query |Utiliser des données tooread hello requête personnalisée. |Une requête SQL-92 ou une requête [SOQL (Salesforce Object Query Language)](https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/sforce_api_calls_soql.htm). Par exemple : `select * from MyTable__c`. |Non (si hello **tableName** Hello **dataset** est spécifié) |

> [!IMPORTANT]
> Hello « __c » partie hello nom de l’API est nécessaire pour tout objet personnalisé.

![Connexion Salesforce - Data Factory - Nom de l’API](media/data-factory-salesforce-connector/data-factory-salesforce-api-name-2.png)

## <a name="query-tips"></a>Conseils pour les requêtes
### <a name="retrieving-data-using-where-clause-on-datetime-column"></a>Récupération de données à l’aide de la clause where sur la colonne DateTime
Lorsque spécifiez hello SOQL ou SQL requête, prêtez attention toohello différence de format de date/heure. Par exemple :

* **Exemple SOQL** : `$$Text.Format('SELECT Id, Name, BillingCity FROM Account WHERE LastModifiedDate >= {0:yyyy-MM-ddTHH:mm:ssZ} AND LastModifiedDate < {1:yyyy-MM-ddTHH:mm:ssZ}', WindowStart, WindowEnd)`
* **Exemple SQL** :
    * **À l’aide de la requête de hello toospecify l’Assistant copie :**`$$Text.Format('SELECT * FROM Account WHERE LastModifiedDate >= {{ts\'{0:yyyy-MM-dd HH:mm:ss}\'}} AND LastModifiedDate < {{ts\'{1:yyyy-MM-dd HH:mm:ss}\'}}', WindowStart, WindowEnd)`
    * **L’utilisation de JSON modification toospecify hello requête (séquence d’échappement de char correctement) :**`$$Text.Format('SELECT * FROM Account WHERE LastModifiedDate >= {{ts\\'{0:yyyy-MM-dd HH:mm:ss}\\'}} AND LastModifiedDate < {{ts\\'{1:yyyy-MM-dd HH:mm:ss}\\'}}', WindowStart, WindowEnd)`

### <a name="retrieving-data-from-salesforce-report"></a>Récupération de données à partir d’un rapport Salesforce
Vous pouvez récupérer des données à partir de rapports Salesforce en spécifiant la requête en tant que `{call "<report name>"}`, par exemple. `"query": "{call \"TestReport\"}"`.

### <a name="retrieving-deleted-records-from-salesforce-recycle-bin"></a>Récupération d’enregistrements supprimés dans la Corbeille Salesforce
tooquery des enregistrements de hello logicielle supprimé à partir de la Corbeille de Salesforce, vous pouvez spécifier **« IsDeleted = 1 »** dans votre requête. Par exemple,

* tooquery uniquement les enregistrements supprimé de hello, spécifiez « sélectionner * à partir de MyTable__c **où IsDeleted = 1**»
* tooquery tous hello enregistrements notamment hello existant et hello supprimé, spécifiez « sélectionner * à partir de MyTable__c **où IsDeleted = 0 ou IsDeleted = 1**»

## <a name="json-example-copy-data-from-salesforce-tooazure-blob"></a>Exemple de JSON : copier des données à partir de Salesforce tooAzure Blob
Hello exemple suivant fournit des exemples de définitions de JSON que vous pouvez utiliser toocreate un pipeline à l’aide de hello [portail Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), ou [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Elles montrent comment toocopy des données à partir de Salesforce tooAzure stockage d’objets Blob. Toutefois, les données peuvent être copié tooany de récepteurs hello indiqué [ici](data-factory-data-movement-activities.md#supported-data-stores-and-formats) à l’aide de hello activité de copie dans Azure Data Factory.   

Voici les artefacts de Data Factory hello que vous devez le scénario de toocreate tooimplement hello. les sections Hello qui suivent hello liste fournissent des détails sur ces étapes.

* Un service lié de type de hello [Salesforce](#linked-service-properties)
* Un service lié de type de hello [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)
* Une entrée [dataset](data-factory-create-datasets.md) de type de hello [RelationalTable](#dataset-properties)
* Une sortie [dataset](data-factory-create-datasets.md) de type de hello [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)
* Un [pipeline](data-factory-create-pipelines.md) avec une activité de copie qui utilise [RelationalSource](#copy-activity-properties) et [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)

**Service lié Salesforce**

Cet exemple utilise hello **Salesforce** service lié. Consultez hello [service lié de Salesforce](#linked-service-properties) section pour les propriétés hello sont pris en charge par ce service lié.  Consultez [obtenir jeton de sécurité](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) pour obtenir des instructions sur la façon dont tooreset/get hello le jeton de sécurité.

```json
{
    "name": "SalesforceLinkedService",
    "properties":
    {
        "type": "Salesforce",
        "typeProperties":
        {
            "username": "<user name>",
            "password": "<password>",
            "securityToken": "<security token>"
        }
    }
}
```
**Service lié Azure Storage**

```json
{
    "name": "AzureStorageLinkedService",
    "properties": {
    "type": "AzureStorage",
    "typeProperties": {
        "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
    }
}
```
**Jeu de données d’entrée Salesforce**

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

Paramètre **externe** trop**true** informe le service de fabrique de données hello ce jeu de données hello est la fabrique de données externe toohello et n’est pas généré par une activité dans la fabrique de données hello.

> [!IMPORTANT]
> Hello « __c » partie hello nom de l’API est nécessaire pour tout objet personnalisé.

![Connexion Salesforce - Data Factory - Nom de l’API](media/data-factory-salesforce-connector/data-factory-salesforce-api-name.png)

**Jeu de données de sortie d’objet Blob Azure**

Les données sont écrites tooa nouvel objet blob toutes les heures (fréquence : heure, intervalle : 1).

```json
{
    "name": "AzureBlobOutput",
    "properties":
    {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties":
        {
            "folderPath": "adfgetstarted/alltypes_c"
        },
        "availability":
        {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

**Pipeline avec activité de copie**

pipeline Hello contient l’activité de copie, qui est configuré toouse hello des jeux de données d’entrée et de sortie et est toorun planifiée toutes les heures. Dans la définition JSON du pipeline hello, hello **source** type est défini trop**RelationalSource**et hello **récepteur** type est défini trop**BlobSink**.

Consultez [RelationalSource les propriétés de type](#copy-activity-properties) pour la liste des propriétés qui sont prises en charge par hello RelationalSource hello.

```json
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2016-06-01T18:00:00",
        "end":"2016-06-01T19:00:00",
        "description":"pipeline with copy activity",
        "activities":[  
        {
            "name": "SalesforceToAzureBlob",
            "description": "Copy from Salesforce tooan Azure blob",
            "type": "Copy",
            "inputs": [
            {
                "name": "SalesforceInput"
            }
            ],
            "outputs": [
            {
                "name": "AzureBlobOutput"
            }
            ],
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
        }
        ]
    }
}
```
> [!IMPORTANT]
> Hello « __c » partie hello nom de l’API est nécessaire pour tout objet personnalisé.

![Connexion Salesforce - Data Factory - Nom de l’API](media/data-factory-salesforce-connector/data-factory-salesforce-api-name-2.png)


### <a name="type-mapping-for-salesforce"></a>Mappage de type pour Salesforce
| Type Salesforce | Type basé sur .NET |
| --- | --- |
| Numérotation automatique |String |
| Case à cocher |Boolean |
| Devise |Double |
| Date |DateTime |
| Date/Heure |DateTime |
| Email |String |
| ID |String |
| Relation de recherche |String |
| Liste déroulante à sélection multiple |String |
| Number |Double |
| Pourcentage |Double |
| Téléphone |String |
| Liste déroulante |String |
| Texte |String |
| Zone de texte |String |
| Zone de texte (long) |String |
| Zone de texte (enrichi) |String |
| Texte (chiffré) |String |
| URL |String |

> [!NOTE]
> colonnes de toomap de toocolumns du jeu de données source à partir du jeu de données récepteur, consultez [mappage des colonnes de jeu de données dans Azure Data Factory](data-factory-map-columns.md).

[!INCLUDE [data-factory-structure-for-rectangualr-datasets](../../includes/data-factory-structure-for-rectangualr-datasets.md)]

## <a name="performance-and-tuning"></a>Performances et réglage
Consultez hello [l’activité de copie guide des performances et paramétrage](data-factory-copy-activity-performance.md) toolearn sur la clé de facteurs d’affecter les performances de transfert de données (activité de copie) dans Azure Data Factory et de différentes façons toooptimize il.
