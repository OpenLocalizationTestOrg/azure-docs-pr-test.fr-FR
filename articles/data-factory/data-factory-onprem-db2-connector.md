---
title: "aaaMove des données à partir de DB2 à l’aide d’Azure Data Factory | Documents Microsoft"
description: "Découvrez comment toomove des données à partir d’un DB2 sur site de base de données à l’aide d’activité de copie de fabrique de données Azure"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: c1644e17-4560-46bb-bf3c-b923126671f1
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jingwang
ms.openlocfilehash: 696ac059be644cb3901c37d2fc746e0682c65a1f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-db2-by-using-azure-data-factory-copy-activity"></a>Déplacer des données depuis DB2 à l’aide de l’activité de copie dans Azure Data Factory
Cet article décrit comment vous pouvez utiliser l’activité de copie de données de toocopy Azure Data Factory à partir d’une banque de données de tooa de base de données locale DB2. Vous pouvez copier le magasin de tooany de données qui est répertorié comme un récepteur pris en charge dans hello [activités de déplacement de données de Data Factory](data-factory-data-movement-activities.md#supported-data-stores-and-formats) l’article. Cette rubrique s’appuie sur l’article Data Factory hello, qui présente une vue d’ensemble du déplacement des données à l’aide de l’activité de copie et répertorie les combinaisons de magasin de données hello pris en charge. 

Fabrique de données prend actuellement en charge le déplacement des données uniquement à partir d’un tooa de la base de données DB2 [magasin de données pris en charge de récepteur](data-factory-data-movement-activities.md#supported-data-stores-and-formats). Déplacement des données à partir d’autres données stocke tooa DB2 de base de données n’est pas pris en charge.

## <a name="prerequisites"></a>Composants requis
Fabrique de données prend en charge la connexion de base de données DB2 de local tooan à l’aide de hello [passerelle de gestion des données](data-factory-data-management-gateway.md). Pour tooset des instructions pas à pas les données de passerelle hello pipeline toomove vos données, consultez hello [déplacer des données locales toocloud](data-factory-move-data-between-onprem-and-cloud.md) l’article.

Une passerelle est requise même si DB2 hello est hébergé sur la machine virtuelle de Azure IaaS. Vous pouvez installer la passerelle de hello sur hello même VM IaaS comme magasin de données hello. Si la passerelle de hello peut se connecter toohello de base de données, vous pouvez installer la passerelle de hello sur une machine virtuelle différente.

passerelle de gestion des données Hello fournit un pilote DB2 intégré, donc vous ne devez toomanually installer les une pilote toocopy données à partir de DB2.

> [!NOTE]
> Pour obtenir des conseils sur la résolution des problèmes de connexion et les problèmes de passerelle, consultez hello [résoudre les problèmes de passerelle](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) l’article.


## <a name="supported-versions"></a>Versions prises en charge
connecteur de Hello DB2 de fabrique de données prend en charge hello suivant plateformes IBM DB2 et les versions avec le Gestionnaire d’accès de base de données Architecture DRDA (Distributed Relational) SQL versions 9, 10 et 11 :

* IBM DB2 pour z/OS version 11.1
* IBM DB2 pour z/OS version 10.1
* IBM DB2 pour i (AS400) version 7.2
* IBM DB2 pour i (AS400) version 7.1
* IBM DB2 pour Linux, UNIX et Windows (LUW) version 11
* IBM DB2 pour LUW version 10.5
* IBM DB2 pour LUW version 10.1

> [!TIP]
> Si vous recevez message d’erreur hello « demande hello package correspondant tooan SQL instruction d’exécution introuvable. SQLSTATE = 51002 SQLCODE =-805, « hello fait un package nécessaire n’est pas créé pour un utilisateur normal de hello sur hello du système d’exploitation. tooresolve ce problème, suivez ces instructions pour le type de votre serveur DB2 :
> - DB2 pour i (AS400) : permettent à un utilisateur avec pouvoir de créer la collection hello pour un utilisateur normal de hello avant d’exécuter l’activité de copie. collection de hello toocreate, utilisez hello commande :`create collection <username>`
> - DB2 pour z/OS ou LUW : utilisez un compte doté de privilèges élevés, un utilisateur avec pouvoir ou un administrateur qui a des autorités de package et de liaison, BINDADD, ACCORDEZ les autorisations de tooPUBLIC EXECUTE--copie de hello toorun qu’une seule fois. package nécessaire de Hello est créé automatiquement pendant la copie de hello. Par la suite, vous pouvez basculer utilisateur normal de toohello arrière pour vos séries de copie suivantes.

## <a name="getting-started"></a>Prise en main
Vous pouvez créer un pipeline comportant des données d’activité toomove copie à partir d’une banque de données DB2 locale à l’aide de différents outils et API : 

- toocreate de façon plus simple Hello un pipeline est toouse hello Assistant de copie de fabrique de données Azure. Pour une procédure pas à pas rapides sur la création d’un pipeline à l’aide d’Assistant copie de hello, consultez hello [didacticiel : créer un pipeline à l’aide de hello Assistant copie de](data-factory-copy-data-wizard-tutorial.md). 
- Vous pouvez également utiliser les outils toocreate un pipeline, y compris hello portail Azure, Visual Studio, Azure PowerShell, un modèle Azure Resource Manager, hello API .NET et hello API REST. Pour obtenir des instructions toocreate un pipeline avec une activité de copie, consultez hello [didacticiel de l’activité de copie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md). 

Si vous utilisez hello ou une API, vous effectuez hello suivant les étapes toocreate un pipeline qui déplace la banque de données récepteur tooa du magasin de données à partir des données d’une source :

1. Créer fabrique de données tooyour de magasins de services liés toolink des données d’entrée et de sortie.
2. Créer des groupes de données toorepresent d’entrée et sortie des données pour l’opération de copie hello. 
3. Création d’un pipeline avec une activité de copie qui utilise un jeu de données en tant qu’entrée et un jeu de données en tant que sortie. 

Lorsque vous utilisez hello Assistant copie de définitions de JSON pour les services de fabrique de données lié hello, jeux de données et des entités de pipeline sont créées automatiquement pour vous. Lorsque vous utilisez des API ou des outils (à l’exception de hello API .NET), vous définissez des entités de fabrique de données hello à l’aide du format JSON de hello. Hello [exemple de JSON : copier des données à partir de DB2 tooAzure stockage d’objets Blob](#json-example-copy-data-from-db2-to-azure-blob) montre définitions JSON hello hello des entités de fabrique de données qui sont des données toocopy utilisé à partir d’une banque de données DB2 locale.

Hello les sections suivantes fournit des détails sur hello propriétés JSON qui sont des entités de fabrique de données hello toodefine utilisés qui sont le magasin de données spécifique tooa DB2.

## <a name="db2-linked-service-properties"></a>Propriétés du service lié DB2
Hello tableau suivant répertorie les propriétés JSON de hello tooa spécifique au service lié DB2.

| Propriété | Description | Requis |
| --- | --- | --- |
| **type** |Cette propriété doit être définie trop**OnPremisesDB2**. |Oui |
| **server** |nom de Hello du serveur de hello DB2. |Oui |
| **database** |nom Hello de base de données hello DB2. |Oui |
| **schema** |nom de Hello du schéma hello hello DB2 de base de données. Cette propriété est sensible à la casse. |Non |
| **authenticationType** |type de Hello d’authentification qui est la base de données utilisé tooconnect toohello DB2. Hello les valeurs possibles sont : anonyme, Basic et Windows. |Oui |
| **nom d’utilisateur** |Hello nom hello compte d’utilisateur si vous utilisez l’authentification de base ou Windows. |Non |
| **mot de passe** |mot de passe Hello hello compte d’utilisateur. |Non |
| **gatewayName** |nom Hello de passerelle hello hello service Data Factory doit utiliser la base de données DB2 tooconnect toohello local. |Oui |

## <a name="dataset-properties"></a>Propriétés du jeu de données
Pour obtenir la liste des sections de hello et des propriétés qui sont disponibles pour définir des jeux de données, consultez hello [création de datasets](data-factory-create-datasets.md) l’article. Sections, tel que **structure**, **disponibilité**et hello **stratégie** pour un jeu de données JSON, sont similaires pour tous les types de jeu de données (SQL Azure, le stockage Blob Azure, Azure Table stockage et ainsi de suite).

Hello **typeProperties** section est différente pour chaque type de jeu de données et fournit des informations sur l’emplacement de hello de données hello dans le magasin de données hello. Hello **typeProperties** section pour un jeu de données de type **RelationalTable**, qui inclut le jeu de données hello DB2, a hello suivant la propriété :

| Propriété | Description | Requis |
| --- | --- | --- |
| **tableName** |nom de Hello de table hello d’instance de base de données DB2 de hello hello service lié fait référence à. Cette propriété est sensible à la casse. |Non (si hello **requête** propriété d’une activité de copie de type **RelationalSource** est spécifié) |

## <a name="copy-activity-properties"></a>Propriétés de l’activité de copie
Pour obtenir la liste des sections de hello et des propriétés qui sont disponibles pour la définition d’activités de copie, consultez hello [création de Pipelines](data-factory-create-pipelines.md) l’article. Les propriétés d’activité de copie comme le **nom**, la **description**, la table d’**entrée**, la table de **sortie** et la **stratégie** sont disponibles pour tous les types d’activités. Hello des propriétés qui sont disponibles dans hello **typeProperties** section d’activité hello pour chaque type d’activité. Pour l’activité de copie, les propriétés de hello varient en fonction des types hello de sources de données et les récepteurs.

Pour l’activité de copie, lors de la source de hello est de type **RelationalSource** (qui inclut DB2), hello propriétés suivantes est disponible dans hello **typeProperties** section :

| Propriété | Description | Valeurs autorisées | Requis |
| --- | --- | --- | --- |
| **query** |Utiliser des données de hello tooread hello requête personnalisée. |Chaîne de requête SQL. Par exemple : `"query": "select * from "MySchema"."MyTable""` |Non (si hello **tableName** propriété d’un jeu de données est spécifiée) |

> [!NOTE]
> Les noms de schéma et de table respectent la casse. Dans l’instruction de requête hello, placez les noms de propriétés à l’aide de « » (guillemets doubles). Par exemple :
>
> ```sql
> "query": "select * from "DB2ADMIN"."Customers""
> ```

## <a name="json-example-copy-data-from-db2-tooazure-blob-storage"></a>Exemple de JSON : copier des données à partir de DB2 tooAzure stockage d’objets Blob
Cet exemple fournit des exemples de définitions de JSON que vous pouvez utiliser toocreate un pipeline à l’aide de hello [portail Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), ou [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Hello montre tooBlob stockage base de données toocopy à partir de DB2. Toutefois, les données peuvent être copiées trop[toutes les données prises en charge stocker le type de récepteur](data-factory-data-movement-activities.md#supported-data-stores-and-formats) à l’aide d’activité de copie de fabrique de données Azure.

exemple Hello a hello suivant des entités de fabrique de données :

- Un service lié DB2 de type [OnPremisesDb2](data-factory-onprem-db2-connector.md#linked-service-properties)
- Un service lié de stockage Azure Blob de type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)
- Un [jeu de données](data-factory-create-datasets.md) d’entrée de type [RelationalTable](data-factory-onprem-db2-connector.md#dataset-properties)
- Un [jeu de données](data-factory-create-datasets.md) de sortie de type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)
- A [pipeline](data-factory-create-pipelines.md) avec une activité de copie qui utilise hello [RelationalSource](data-factory-onprem-db2-connector.md#copy-activity-properties) et [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) propriétés

exemple Hello copie toutes les heures des données à partir d’un résultat de requête dans un tooan de base de données DB2 blob Azure. les propriétés JSON Hello qui sont utilisées dans l’exemple hello sont décrites dans les sections hello qui suivent les définitions d’entité hello.

Pour commencer, installez et configurez une passerelle de données. Instructions sont fournies dans hello [déplacement des données entre les emplacements locaux et cloud](data-factory-move-data-between-onprem-and-cloud.md) l’article.

**Service lié DB2**

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

**Service lié Azure Blob Storage**

```json
{
    "name": "AzureStorageLinkedService",
    "properties": {
        "type": "AzureStorageLinkedService",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<AccountName>;AccountKey=<AccountKey>"
        }
    }
}
```

**Jeu de données d’entrée DB2**

exemple Hello part du principe que vous avez créé une table dans DB2 nommé « MyTable » qui comporte une colonne intitulée « timestamp » pour les données de série chronologique hello.

Hello **externe** propriété a la valeur trop « true ». Ce paramètre informe le service de fabrique de données hello que ce jeu de données est la fabrique de données externe toohello et qu’il n’est pas généré par une activité dans la fabrique de données hello. Notez que hello **type** propriété a la valeur trop**RelationalTable**.


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

**Jeu de données de sortie d’objet Blob Azure**

Les données sont écrites tooa nouvel objet blob toutes les heures en définissant un hello **fréquence** propriété trop « Heure » et hello **intervalle** too1 de propriété. Hello **folderPath** propriété pour les blob hello est dynamiquement évaluée selon l’heure de début hello de tranche hello qui est en cours de traitement. chemin d’accès du dossier Hello utilise hello des parties d’année, mois, jour et heure de l’heure de début hello.

```json
{
    "name": "AzureBlobDb2DataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/db2/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
            "format": {
                "type": "TextFormat",
                "rowDelimiter": "\n",
                "columnDelimiter": "\t"
            },
            "partitionedBy": [
                {
                    "name": "Year",
                    "value": {
                        "type": "DateTime",
                        "date": "SliceStart",
                        "format": "yyyy"
                    }
                },
                {
                    "name": "Month",
                    "value": {
                        "type": "DateTime",
                        "date": "SliceStart",
                        "format": "MM"
                    }
                },
                {
                    "name": "Day",
                    "value": {
                        "type": "DateTime",
                        "date": "SliceStart",
                        "format": "dd"
                    }
                },
                {
                    "name": "Hour",
                    "value": {
                        "type": "DateTime",
                        "date": "SliceStart",
                        "format": "HH"
                    }
                }
            ]
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

**Pipeline pour l’activité de copie hello**

pipeline de Hello contient une activité de copie qui est configurée toouse spécifié des jeux de données d’entrée et de sortie et qui est toorun planifiée toutes les heures. Bonjour définition JSON pour le pipeline de hello, hello **source** type est défini trop**RelationalSource** et hello **récepteur** type est défini trop**BlobSink**. la requête SQL Hello spécifiée pour hello **requête** propriété sélectionne les données de salutation à partir de la table « Orders » de hello.

```json
{
    "name": "CopyDb2ToBlob",
    "properties": {
        "description": "pipeline for hello copy activity",
        "activities": [
            {
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
                "inputs": [
                    {
                        "name": "Db2DataSet"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobDb2DataSet"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "Db2ToBlob"
            }
        ],
        "start": "2014-06-01T18:00:00Z",
        "end": "2014-06-01T19:00:00Z"
    }
}
```

## <a name="type-mapping-for-db2"></a>Mappage de type pour DB2
Comme mentionné dans hello [les activités de déplacement des données](data-factory-data-movement-activities.md) article, l’activité de copie effectue des conversions de type automatique à partir de la source de type type toosink à l’aide de hello suivant l’approche en deux étapes :

1. Convertir un type de source native type tooa .NET
2. Convertir un type de récepteur natif .NET type tooa

mappages suivants Hello sont utilisées lorsque l’activité de copie convertit les données de salutation à partir d’un type .NET de DB2 type tooa :

| Type de base de données DB2 | Type de .NET Framework |
| --- | --- |
| SmallInt |Int16 |
| Integer |Int32 |
| BigInt |Int64 |
| Real |Single |
| Double |Double |
| Float |Double |
| Décimal |Décimal |
| DecimalFloat |Décimal |
| Chiffre |Décimal |
| Date |DateTime |
| Time |TimeSpan |
| Timestamp |Datetime |
| xml |Byte[] |
| Char |String |
| VarChar |String |
| LongVarChar |String |
| DB2DynArray |String |
| Fichier binaire |Byte[] |
| VarBinary |Byte[] |
| LongVarBinary |Byte[] |
| Graphic |String |
| VarGraphic |String |
| LongVarGraphic |String |
| Clob |String |
| Blob |Byte[] |
| DbClob |String |
| SmallInt |Int16 |
| Integer |Int32 |
| BigInt |Int64 |
| Real |Single |
| Double |Double |
| Float |Double |
| Décimal |Décimal |
| DecimalFloat |Décimal |
| Chiffre |Décimal |
| Date |DateTime |
| Time |TimeSpan |
| Timestamp |Datetime |
| xml |Byte[] |
| Char |String |

## <a name="map-source-toosink-columns"></a>Mapper les colonnes de source toosink
toolearn colonnes toomap hello toocolumns de jeu de données source dans le jeu de données récepteur hello, voir [mappage des colonnes de jeu de données dans Azure Data Factory](data-factory-map-columns.md).

## <a name="repeatable-reads-from-relational-sources"></a>Lectures renouvelées de sources relationnelles
Lorsque vous copiez des données à partir d’un magasin de données relationnelles, conserver la répétabilité dans l’esprit tooavoid des résultats inattendus. Dans Azure Data Factory, vous pouvez réexécuter une tranche manuellement. Vous pouvez également configurer les nouvelles tentatives de hello **stratégie** propriété pour un toorerun de jeu de données un secteur lorsqu’une défaillance se produit. Vérifiez que hello les mêmes données ne sont en lecture aucune question comment tranche de hello autant de fois est exécuter à nouveau et indépendamment de la façon dont vous réexécutez tranche de hello. Pour plus d’informations, consultez [Lectures renouvelées de sources relationnelles](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).

## <a name="performance-and-tuning"></a>Performances et réglage
En savoir plus sur les principaux facteurs qui affectent les performances hello de l’activité de copie et de méthodes toooptimize Bonjour [copie activité Guide des performances et paramétrage](data-factory-copy-activity-performance.md).
