---
title: "aaaMove des données à partir de magasins de données ODBC | Documents Microsoft"
description: "En savoir plus sur le stockage des données toomove à partir de données ODBC à l’aide d’Azure Data Factory."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: ad70a598-c031-4339-a883-c6125403cb76
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: jingwang
ms.openlocfilehash: bf96e71da449313b6144bb194205c572d2ca2030
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-odbc-data-stores-using-azure-data-factory"></a>Transfert de données à partir de magasins de données ODBC à l’aide d’Azure Data Factory
Cet article explique comment stocker des toouse hello activité de copie de données Azure Data Factory toomove une locale, les données ODBC. Il repose sur hello [les activités de déplacement des données](data-factory-data-movement-activities.md) article, qui présente une vue d’ensemble du déplacement des données avec l’activité de copie hello.

Vous pouvez copier des données à partir d’une banque de données de récepteur ODBC données magasin tooany pris en charge. Pour une liste de données pris en charge des magasins récepteurs par l’activité de copie hello, consultez hello [prise en charge des magasins de données](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table. Fabrique de données prend en charge uniquement le déplacement tooother les magasins de données du magasin de données à partir de des données ODBC, mais ne pas pour déplacer des données d’une autre banque de données ODBC tooan données magasins. 

## <a name="enabling-connectivity"></a>Activation de la connectivité
Service de fabrique de données prend en charge des sources de ODBC tooon local qui se connecte à l’aide de la passerelle de gestion des données de hello. Consultez [déplacement des données entre les emplacements locaux et cloud](data-factory-move-data-between-onprem-and-cloud.md) toolearn l’article sur la passerelle de gestion des données et des instructions détaillées sur la configuration de passerelle de hello. Utiliser le magasin de données ODBC hello passerelle tooconnect tooan même s’il est hébergé dans une machine virtuelle IaaS de Azure.

Vous pouvez installer la passerelle de hello sur hello même local de l’ordinateur ou hello Azure VM comme magasin de données ODBC hello. Toutefois, nous vous recommandons d’installer hello passerelle sur un ordinateur distinct/Azure IaaS VM tooavoid les conflits de ressources et pour de meilleures performances. Lorsque vous installez la passerelle de hello sur un ordinateur distinct, machine de hello doit être machine hello tooaccess en mesure de magasin de données ODBC hello.

Outre hello passerelle de gestion des données, vous devez également pilote ODBC de hello tooinstall de banque de données hello sur l’ordinateur de passerelle hello.

> [!NOTE]
> Consultez [Résolution des problèmes de passerelle](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) pour obtenir des conseils sur la résolution des problèmes de connexion/passerelle.

## <a name="getting-started"></a>Prise en main
Vous pouvez créer un pipeline avec une activité de copie qui déplace les données d’un magasin de données ODBC local à l’aide de différents outils/API.

toocreate de façon plus simple Hello un pipeline est toouse hello **Assistant copie de**. Consultez [didacticiel : créer un pipeline à l’aide d’Assistant copie de](data-factory-copy-data-wizard-tutorial.md) pour une procédure pas à pas rapides sur la création d’un pipeline à l’aide d’Assistant de données de copie hello.

Vous pouvez également utiliser hello suivant outils toocreate un pipeline : **portail Azure**, **Visual Studio**, **Azure PowerShell**, **modèle Azure Resource Manager** , **API .NET**, et **API REST**. Consultez [didacticiel d’activité de copie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) pour obtenir des instructions toocreate un pipeline avec une activité de copie. 

Si vous utilisez hello ou une API, vous effectuez hello suivant les étapes toocreate un pipeline qui déplace la banque de données récepteur tooa du magasin de données à partir des données d’une source : 

1. Créer **services liés** fabrique de données tooyour toolink les données d’entrée et de sortie magasins.
2. Créer **datasets** toorepresent d’entrée et sortie l’opération de copie des données pour hello. 
3. Création d’un **pipeline** avec une activité de copie qui utilise un jeu de données en tant qu’entrée et un jeu de données en tant que sortie. 

Lorsque vous utilisez hello Assistant, les définitions de JSON pour ces entités de fabrique de données (services liés, des datasets et pipeline de hello) sont créées automatiquement pour vous. Lorsque vous utilisez/API des outils (à l’exception des API .NET), vous définissez ces entités de fabrique de données à l’aide du format JSON de hello.  Pour obtenir un exemple avec des définitions de JSON pour les entités de fabrique de données qui sont utilisées toocopy des données à partir d’une banque de données ODBC, consultez [exemple de JSON : tooAzure Blob de magasin de données de copie à partir de données ODBC](#json-example-copy-data-from-odbc-data-store-to-azure-blob) section de cet article. 

Hello les sections suivantes fournit des détails sur les propriétés JSON qui sont le magasin de données utilisé toodefine Data Factory entités tooODBC spécifique :

## <a name="linked-service-properties"></a>Propriétés du service lié
Hello tableau suivant fournit la description du service de tooODBC spécifique lié éléments JSON.

| Propriété | Description | Requis |
| --- | --- | --- |
| type |propriété de type Hello doit indiquer : **OnPremisesOdbc** |Oui |
| connectionString |partie des informations d’identification de l’accès non Hello de chaîne de connexion hello et éventuellement un chiffrées d’informations d’identification. Consultez les exemples dans les sections suivantes de hello. |Oui |
| credential |Hello accès informations d’identification la partie de chaîne de connexion hello spécifié au format de la valeur de propriété spécifiques au pilote. Exemple : « Uid=<user ID>;Pwd=<password>;RefreshToken=<secret refresh token>; ». |Non |
| authenticationType |Type d’authentification utilisé le magasin de données ODBC tooconnect toohello. Les valeurs possibles sont : Anonyme et De base. |Oui |
| username |Spécifiez le nom d’utilisateur si vous utilisez l’authentification de base. |Non |
| password |Spécifiez le mot de passe de compte d’utilisateur hello que vous avez spécifié pour le nom d’utilisateur hello. |Non |
| gatewayName |Nom de passerelle hello hello service Data Factory doit utiliser le magasin de données ODBC tooconnect toohello. |Oui |

### <a name="using-basic-authentication"></a>Utilisation de l’authentification de base

```json
{
    "name": "odbc",
    "properties":
    {
        "type": "OnPremisesOdbc",
        "typeProperties":
        {
            "authenticationType": "Basic",
            "connectionString": "Driver={SQL Server};Server=Server.database.windows.net; Database=TestDatabase;",
            "userName": "username",
            "password": "password",
            "gatewayName": "mygateway"
        }
    }
}
```
### <a name="using-basic-authentication-with-encrypted-credentials"></a>Utilisation de l’authentification de base avec des informations d’identification chiffrées
Vous pouvez chiffrer les informations d’identification hello à l’aide de hello [New-AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) applet de commande (1.0 version d’Azure PowerShell) ou [New-AzureDataFactoryEncryptValue](https://msdn.microsoft.com/library/dn834940.aspx) (0,9 version ou antérieure de hello Azure PowerShell).  

```json
{
    "name": "odbc",
    "properties":
    {
        "type": "OnPremisesOdbc",
        "typeProperties":
        {
            "authenticationType": "Basic",
            "connectionString": "Driver={SQL Server};Server=myserver.database.windows.net; Database=TestDatabase;;EncryptedCredential=eyJDb25uZWN0...........................",
            "gatewayName": "mygateway"
        }
    }
}
```

### <a name="using-anonymous-authentication"></a>Utilisation de l’authentification anonyme

```json
{
    "name": "odbc",
    "properties":
    {
        "type": "OnPremisesOdbc",
        "typeProperties":
        {
            "authenticationType": "Anonymous",
            "connectionString": "Driver={SQL Server};Server={servername}.database.windows.net; Database=TestDatabase;",
            "credential": "UID={uid};PWD={pwd}",
            "gatewayName": "mygateway"
        }
    }
}
```


## <a name="dataset-properties"></a>Propriétés du jeu de données
Pour obtenir une liste complète des sections et les propriétés disponibles pour définir des jeux de données, consultez hello [création de datasets](data-factory-create-datasets.md) l’article. Les sections comme la structure, la disponibilité et la stratégie d'un jeu de données JSON sont similaires pour tous les types de jeux de données (SQL Azure, Azure Blob, Azure Table, etc.).

Hello **typeProperties** section est différente pour chaque type de jeu de données et fournit des informations sur l’emplacement de hello de données hello dans le magasin de données hello. jeu de données de type Hello typeProperties section **RelationalTable** (qui comprend de jeu de données ODBC) a hello propriétés suivantes

| Propriété | Description | Requis |
| --- | --- | --- |
| TableName |Nom de table hello dans le magasin de données ODBC hello. |Oui |

## <a name="copy-activity-properties"></a>Propriétés de l’activité de copie
Pour obtenir une liste complète des sections et les propriétés disponibles pour la définition d’activités, consultez hello [création de Pipelines](data-factory-create-pipelines.md) l’article. Les propriétés comme le nom, la description, les tables d'entrée et de sortie et les différentes stratégies sont disponibles pour tous les types d'activités.

Propriétés disponibles dans hello **typeProperties** section de l’activité de hello sur hello autre part varient selon chaque type d’activité. Pour l’activité de copie, ils varient selon les types de sources et récepteurs hello.

Dans l’activité de copie, lors de la source est de type **RelationalSource** (qui inclut ODBC), hello propriétés suivantes est disponible dans la section de typeProperties :

| Propriété | Description | Valeurs autorisées | Requis |
| --- | --- | --- | --- |
| query |Utiliser des données tooread hello requête personnalisée. |Chaîne de requête SQL. Par exemple : select * from MyTable. |Oui |


## <a name="json-example-copy-data-from-odbc-data-store-tooazure-blob"></a>Exemple de JSON : tooAzure Blob de magasin de données de copie à partir de données ODBC
Cet exemple fournit les définitions de JSON que vous pouvez utiliser toocreate un pipeline à l’aide de [portail Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) ou [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) ou [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Il montre comment la source de données de toocopy à partir d’une application ODBC tooan stockage d’objets Blob Azure. Toutefois, les données peuvent être copié tooany de récepteurs hello indiqué [ici](data-factory-data-movement-activities.md#supported-data-stores-and-formats) à l’aide de hello activité de copie dans Azure Data Factory.

exemple Hello a hello suivant des entités de fabrique de données :

1. Un service lié de type [OnPremisesOdbc](#linked-service-properties).
2. Un service lié de type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. Un [jeu de données](data-factory-create-datasets.md) d’entrée de type [RelationalTable](#dataset-properties).
4. Un [jeu de données](data-factory-create-datasets.md) de sortie de type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
5. Un [pipeline](data-factory-create-pipelines.md) avec une activité de copie qui utilise [RelationalSource](#copy-activity-properties) et [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

exemple Hello copie des données à partir d’un résultat de requête dans un blob de tooa de magasin de données ODBC toutes les heures. propriétés JSON Hello utilisées dans ces exemples sont décrits dans les sections suivantes des exemples de hello.

Dans un premier temps, configurer la passerelle de gestion des données hello. instructions de Hello sont Bonjour [déplacement des données entre les emplacements locaux et cloud](data-factory-move-data-between-onprem-and-cloud.md) l’article.

**Service lié de ODBC** cet exemple utilise hello l’authentification de base. Consultez la section [Service lié ODBC](#linked-service-properties) pour connaître les différents types d’authentification que vous pouvez utiliser.

```json
{
    "name": "OnPremOdbcLinkedService",
    "properties":
    {
        "type": "OnPremisesOdbc",
        "typeProperties":
        {
            "authenticationType": "Basic",
            "connectionString": "Driver={SQL Server};Server=Server.database.windows.net; Database=TestDatabase;",
            "userName": "username",
            "password": "password",
            "gatewayName": "mygateway"
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

**Jeu de données d’entrée ODBC**

exemple Hello suppose que vous avez créé une table « MaTable » dans une base de données ODBC et qu’il contient une colonne appelée « timestampcolumn » pour les données de série chronologique.

Paramètre « external » : « true » informe service Data Factory de hello ce jeu de données hello est la fabrique de données externe toohello et n’est pas généré par une activité dans la fabrique de données hello.

```json
{
    "name": "ODBCDataSet",
    "properties": {
        "published": false,
        "type": "RelationalTable",
        "linkedServiceName": "OnPremOdbcLinkedService",
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

Les données sont écrites tooa nouvel objet blob toutes les heures (fréquence : heure, intervalle : 1). chemin d’accès du dossier Hello pour l’objet blob de hello est évaluée dynamiquement en fonction de l’heure de début hello de tranche hello qui est en cours de traitement. chemin d’accès du dossier Hello utilise l’année, mois, jours et heures des parties de l’heure de début hello.

```json
{
    "name": "AzureBlobOdbcDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/odbc/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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


**Activité de copie dans un pipeline, avec une source ODBC (RelationalSource) et un récepteur blob (BlobSink)**

pipeline de Hello contient une activité de copie qui est configuré toouse ces jeux de données d’entrée et de sortie et est toorun planifiée toutes les heures. Dans la définition JSON du pipeline hello, hello **source** type est défini trop**RelationalSource** et **récepteur** type est défini trop**BlobSink**. la requête SQL Hello spécifiée pour hello **requête** propriété sélectionne des données de hello Bonjour au-delà de toocopy d’heure.

```json
{
    "name": "CopyODBCToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
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
                "inputs": [
                    {
                        "name": "OdbcDataSet"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobOdbcDataSet"
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
                "name": "OdbcToBlob"
            }
        ],
        "start": "2016-06-01T18:00:00Z",
        "end": "2016-06-01T19:00:00Z"
    }
}
```
### <a name="type-mapping-for-odbc"></a>Mappage de type pour ODBC
Comme mentionné dans hello [les activités de déplacement des données](data-factory-data-movement-activities.md) article, l’activité de copie effectue les conversions de type automatique à partir de types de sources de toosink types avec hello suivant l’approche en deux étapes :

1. Convertir à partir de la source native types too.NET type
2. Conversion de type de récepteur de toonative de type .NET

Lors du déplacement des données à partir de magasins de données ODBC, types de données ODBC sont mappés too.NET types comme indiqué dans hello [les mappages de types de données ODBC](https://msdn.microsoft.com/library/cc668763.aspx) rubrique.

## <a name="map-source-toosink-columns"></a>Mapper les colonnes de source toosink
toolearn sur le mappage des colonnes dans toocolumns du jeu de données source dans le jeu de données récepteur, consultez [mappage des colonnes de jeu de données dans Azure Data Factory](data-factory-map-columns.md).

## <a name="repeatable-read-from-relational-sources"></a>Lecture renouvelée de sources relationnelles
Lors de la copie des données à partir de banques de données relationnelles, conserver la répétabilité dans l’esprit tooavoid des résultats inattendus. Dans Azure Data Factory, vous pouvez réexécuter une tranche manuellement. Vous pouvez également configurer une stratégie de nouvelles tentatives pour un jeu de données, afin qu’une tranche soit réexécutée en cas de défaillance. Lorsqu’une tranche est exécuté à nouveau dans les deux cas, vous devez toomake vraiment qui hello des mêmes données n’est en lecture aucune question comment plusieurs fois une tranche est exécutée. Voir [Lecture renouvelée de sources relationnelles](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).

## <a name="ge-historian-store"></a>Magasin GE Historian
Vous créez un toolink de service ODBC lié un [GE Proficy historien (désormais GE historien)](http://www.geautomation.com/products/proficy-historian) tooan service Azure data factory du magasin de données comme indiqué dans hello l’exemple suivant :

```json
{
    "name": "HistorianLinkedService",
    "properties":
    {
        "type": "OnPremisesOdbc",
        "typeProperties":
        {
            "connectionString": "DSN=<name of hello GE Historian store>",
            "gatewayName": "<gateway name>",
            "authenticationType": "Basic",
            "userName": "<user name>",
            "password": "<password>"
        }
    }
}
```

Installer la passerelle de gestion des données sur une machine locale et inscrire la passerelle de hello via le portail de hello. passerelle Hello installé sur votre ordinateur local utilise le pilote ODBC de hello pour GE historien tooconnect toohello magasin de données GE historien. Par conséquent, installez les pilotes hello s’il n’est pas déjà installé sur l’ordinateur de passerelle hello. Consultez la section [Activation de la connectivité](#enabling-connectivity) pour plus d’informations.

Avant d’utiliser hello GE historien stocker dans une solution de fabrique de données, vérifiez si la passerelle de hello peut se connecter toohello magasin de données à l’aide des instructions dans la section suivante de hello.

Article de hello en lecture à partir du début de hello pour obtenir une présentation détaillée de l’utilisation de données ODBC stocke en tant que magasins de données source dans une opération de copie.  

## <a name="troubleshoot-connectivity-issues"></a>Résoudre les problèmes de connectivité
tootroubleshoot des problèmes de connexion, utilisez hello **Diagnostics** onglet de **Gestionnaire de Configuration de passerelle de gestion de données**.

1. Lancez le **Gestionnaire de configuration de la passerelle de gestion des données**. Vous pouvez exécuter « C:\Program Files\Microsoft données Gestion Gateway\1.0\Shared\ConfigManager.exe « directement (ou) recherche pour **passerelle** toofind un lien trop**passerelle de gestion des données Microsoft** application, comme illustré dans hello suivant l’image.

    ![Rechercher la passerelle](./media/data-factory-odbc-connector/search-gateway.png)
2. Commutateur toohello **Diagnostics** onglet.

    ![Diagnostics de la passerelle](./media/data-factory-odbc-connector/data-factory-gateway-diagnostics.png)
3. Sélectionnez hello **type** de stocker des données (lié de service).
4. Spécifiez **authentification** et entrez **informations d’identification** (ou) entrez **chaîne de connexion** qui est le magasin de données toohello tooconnect utilisé.
5. Cliquez sur **tester la connexion** magasin de données toohello tootest hello connexion.

## <a name="performance-and-tuning"></a>Performances et réglage
Consultez [copie activité optimiser les performances et Guide d’optimisation](data-factory-copy-activity-performance.md) toolearn sur la clé de facteurs d’affecter les performances de transfert de données (activité de copie) dans Azure Data Factory et de différentes façons toooptimize il.
