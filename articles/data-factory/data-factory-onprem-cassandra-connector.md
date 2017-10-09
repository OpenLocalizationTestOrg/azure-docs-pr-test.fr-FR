---
title: "données aaaMove Cassandra à l’aide de la fabrique de données | Documents Microsoft"
description: "Découvrez comment toomove des données à partir d’un Cassandra local de base de données à l’aide d’Azure Data Factory."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 085cc312-42ca-4f43-aa35-535b35a102d5
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jingwang
ms.openlocfilehash: 0e265d3a8439d0a2cb2a5c32e5ea8348a1617621
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-an-on-premises-cassandra-database-using-azure-data-factory"></a>Déplacer des données depuis une base de données Cassandra locale à l’aide d’Azure Data Factory
Cet article explique comment toouse hello activité de copie de données de toomove Azure Data Factory à partir d’une base de données locale Cassandra. Il repose sur hello [les activités de déplacement des données](data-factory-data-movement-activities.md) article, qui présente une vue d’ensemble du déplacement des données avec l’activité de copie hello.

Vous pouvez copier les données d’une banque de données locale Cassandra données magasin tooany pris en charge récepteur. Pour une liste de données pris en charge des magasins récepteurs par l’activité de copie hello, consultez hello [prise en charge des magasins de données](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table. Fabrique de données prend en charge uniquement le déplacement tooother les magasins de données du magasin de données à partir de données Cassandra, mais ne pas pour déplacer des données d’une autre banque de données Cassandra tooa données magasins. 

## <a name="supported-versions"></a>Versions prises en charge
connecteur de Cassandra Hello prend en charge hello versions de Cassandra suivantes : 2.X.

## <a name="prerequisites"></a>Composants requis
Pour hello Azure Data Factory service toobe tooconnect en mesure de tooyour Cassandra base de données locale, vous devez installer une passerelle de gestion des données sur hello même cette base de données hello hôtes de l’ordinateur ou sur un tooavoid machine distincte qui entrent en concurrence pour les ressources par hello base de données. Passerelle de gestion des données est un composant qui établit des services de toocloud de sources de données sur site de manière sécurisée et gérée. Consultez l’article [Passerelle de gestion des données](data-factory-data-management-gateway.md) pour obtenir des informations détaillées sur la passerelle de gestion des données. Consultez [déplacer des données locales toocloud](data-factory-move-data-between-onprem-and-cloud.md) article pour obtenir des instructions sur la configuration de passerelle de hello données toomove de pipeline de données.

Vous devez utiliser la base de données hello passerelle tooconnect tooa Cassandra même si la base de données hello est hébergé dans le cloud de hello, par exemple, sur une machine virtuelle IaaS de Azure. Y avoir de passerelle de hello sur hello même machine virtuelle de cette base de données hôtes hello ou sur un ordinateur distinct virtuel tant que passerelle de hello peuvent se connecter toohello de base de données.  

Lorsque vous installez la passerelle de hello, il installe automatiquement une base de données ODBC de Microsoft Cassandra pilote utilisé tooconnect tooCassandra. Par conséquent, vous n’avez pas besoin toomanually installer un pilote sur l’ordinateur de passerelle hello lors de la copie des données à partir de la base de données Cassandra hello. 

> [!NOTE]
> Consultez [Résolution des problèmes de passerelle](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) pour obtenir des conseils sur la résolution des problèmes de connexion/passerelle.

## <a name="getting-started"></a>Prise en main
Vous pouvez créer un pipeline avec une activité de copie qui déplace les données d’un magasin de données Cassandra local à l’aide de différents outils/API. 

- toocreate de façon plus simple Hello un pipeline est toouse hello **Assistant copie de**. Consultez [didacticiel : créer un pipeline à l’aide d’Assistant copie de](data-factory-copy-data-wizard-tutorial.md) pour une procédure pas à pas rapides sur la création d’un pipeline à l’aide d’Assistant de données de copie hello. 
- Vous pouvez également utiliser hello suivant outils toocreate un pipeline : **portail Azure**, **Visual Studio**, **Azure PowerShell**, **modèle Azure Resource Manager** , **API .NET**, et **API REST**. Consultez [didacticiel d’activité de copie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) pour obtenir des instructions toocreate un pipeline avec une activité de copie. 

Si vous utilisez hello ou une API, vous effectuez hello suivant les étapes toocreate un pipeline qui déplace la banque de données récepteur tooa du magasin de données à partir des données d’une source :

1. Créer **services liés** fabrique de données tooyour toolink les données d’entrée et de sortie magasins.
2. Créer **datasets** toorepresent d’entrée et sortie l’opération de copie des données pour hello. 
3. Création d’un **pipeline** avec une activité de copie qui utilise un jeu de données en tant qu’entrée et un jeu de données en tant que sortie. 

Lorsque vous utilisez hello Assistant, les définitions de JSON pour ces entités de fabrique de données (services liés, des datasets et pipeline de hello) sont créées automatiquement pour vous. Lorsque vous utilisez/API des outils (à l’exception des API .NET), vous définissez ces entités de fabrique de données à l’aide du format JSON de hello.  Pour voir un exemple avec des définitions de JSON pour les entités de fabrique de données qui sont utilisés toocopy des données à partir d’une banque de données locale Cassandra, [exemple de JSON : copier des données à partir de Cassandra tooAzure Blob](#json-example-copy-data-from-cassandra-to-azure-blob) section de cet article. 

Hello les sections suivantes fournit des détails sur les propriétés JSON qui sont le magasin de données Cassandra utilisé toodefine Data Factory entités tooa spécifique :

## <a name="linked-service-properties"></a>Propriétés du service lié
Hello tableau suivant fournit la description du service de tooCassandra spécifique lié éléments JSON.

| Propriété | Description | Requis |
| --- | --- | --- |
| type |propriété de type Hello doit indiquer : **OnPremisesCassandra** |Oui |
| host |Une ou plusieurs adresses IP ou noms d’hôte de serveurs Cassandra.<br/><br/>Spécifiez une liste séparée par des virgules des adresses IP ou hôte noms tooconnect tooall serveurs simultanément. |Oui |
| port |Hello le port TCP qui hello du serveur de Cassandra utilise toolisten pour les connexions client. |Non, valeur par défaut : 9042 |
| authenticationType |Basique ou anonyme |Oui |
| username |Spécifiez le nom d’utilisateur pour le compte d’utilisateur hello. |Oui, si authenticationType a la valeur tooBasic. |
| password |Spécifiez le mot de passe de compte d’utilisateur hello. |Oui, si authenticationType a la valeur tooBasic. |
| gatewayName |nom Hello de passerelle hello est utilisé tooconnect toohello Cassandra base de données locale. |Oui |
| Encryptedcredential |Informations d’identification chiffrées par la passerelle de hello. |Non |

## <a name="dataset-properties"></a>Propriétés du jeu de données
Pour obtenir une liste complète des sections et les propriétés disponibles pour définir des jeux de données, consultez hello [création de datasets](data-factory-create-datasets.md) l’article. Les sections comme la structure, la disponibilité et la stratégie d'un jeu de données JSON sont similaires pour tous les types de jeux de données (SQL Azure, Azure Blob, Azure Table, etc.).

Hello **typeProperties** section est différente pour chaque type de jeu de données et fournit des informations sur l’emplacement de hello de données hello dans le magasin de données hello. jeu de données de type Hello typeProperties section **CassandraTable** a les propriétés suivantes de hello

| Propriété | Description | Requis |
| --- | --- | --- |
| espace de clé |Nom de l’espace de clés hello ou un schéma de base de données Cassandra. |Oui (si la **requête** pour **CassandraSource** n’est pas définie). |
| TableName |Nom de table hello Cassandra de base de données. |Oui (si la **requête** pour **CassandraSource** n’est pas définie). |

## <a name="copy-activity-properties"></a>Propriétés de l’activité de copie
Pour obtenir une liste complète des sections et les propriétés disponibles pour la définition d’activités, consultez hello [création de Pipelines](data-factory-create-pipelines.md) l’article. Les propriétés comme le nom, la description, les tables d’entrée et de sortie et la stratégie sont disponibles pour tous les types d’activités.

Alors que les propriétés disponibles dans la section typeProperties hello activité hello varient selon chaque type d’activité. Pour l’activité de copie, ils varient selon les types de sources et récepteurs hello.

Lorsque la source est de type **CassandraSource**, hello propriétés suivantes est disponible dans la section de typeProperties :

| Propriété | Description | Valeurs autorisées | Requis |
| --- | --- | --- | --- |
| query |Utiliser des données tooread hello requête personnalisée. |Requête SQL-92 ou requête CQL. Reportez-vous à [référence CQL](https://docs.datastax.com/en/cql/3.1/cql/cql_reference/cqlReferenceTOC.html). <br/><br/>Lorsque vous utilisez la requête SQL, spécifiez **nom d’espace de clés name.table** toorepresent hello tableau tooquery. |Non (si tableName et keyspace sur le jeu de données sont définis). |
| Niveau de cohérence |niveau de cohérence Hello Spécifie le nombre de réplicas doit répondre de requête de lecture tooa avant de retourner l’application data toohello client. Les vérifications Cassandra hello un nombre spécifié de réplicas pour la requête de lecture hello toosatisfy de données. |UN, DEUX, TROIS, QUORUM, TOUT, LOCAL_QUORUM, EACH_QUORUM, LOCAL_ONE. Reportez-vous à [Configuring data consistency (Configuration de la cohérence des données)](http://docs.datastax.com/en//cassandra/2.0/cassandra/dml/dml_config_consistency_c.html) pour plus d’informations. |Non. La valeur par défaut est UN. |

## <a name="json-example-copy-data-from-cassandra-tooazure-blob"></a>Exemple de JSON : copier des données à partir de Cassandra tooAzure Blob
Cet exemple fournit des exemples de définitions de JSON que vous pouvez utiliser toocreate un pipeline à l’aide de [portail Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) ou [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) ou [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Elle indique la base de données toocopy à partir d’un Cassandra local tooan stockage d’objets Blob Azure. Toutefois, les données peuvent être copié tooany de récepteurs hello indiqué [ici](data-factory-data-movement-activities.md#supported-data-stores-and-formats) à l’aide de hello activité de copie dans Azure Data Factory.

> [!IMPORTANT]
> Cet exemple fournit des extraits de code JSON. Il n’inclut pas d’instructions détaillées pour créer la fabrique de données hello. Les instructions se trouvent dans l’article [Déplacement de données entre des emplacements locaux et le cloud](data-factory-move-data-between-onprem-and-cloud.md) .

exemple Hello a hello suivant des entités de fabrique de données :

* Un service lié de type [OnPremisesCassandra](#linked-service-properties).
* Un service lié de type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
* Un [jeu de données](data-factory-create-datasets.md) d’entrée de type [CassandraTable](#dataset-properties).
* Un [jeu de données](data-factory-create-datasets.md) de sortie de type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
* Un [pipeline](data-factory-create-pipelines.md) avec une activité de copie qui utilise [CassandraSource](#copy-activity-properties) et [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

**Service lié Cassandra :**

Cet exemple utilise hello **Cassandra** service lié. Consultez [Cassandra de service lié](#linked-service-properties) section pour les propriétés hello pris en charge par ce service lié.  

```json
{
    "name": "CassandraLinkedService",
    "properties":
    {
        "type": "OnPremisesCassandra",
        "typeProperties":
        {
            "authenticationType": "Basic",
            "host": "mycassandraserver",
            "port": 9042,
            "username": "user",
            "password": "password",
            "gatewayName": "mygateway"
        }
    }
}
```

**Service lié Azure Storage :**

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

**Jeu de données d’entrée Cassandra :**

```json
{
    "name": "CassandraInput",
    "properties": {
        "linkedServiceName": "CassandraLinkedService",
        "type": "CassandraTable",
        "typeProperties": {
            "tableName": "mytable",
            "keySpace": "mykeyspace"
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

**Jeu de données de sortie Azure Blob :**

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
            "folderPath": "adfgetstarted/fromcassandra"
        },
        "availability":
        {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

**Activité de copie dans un pipeline avec une source Cassandra et un récepteur blob :**

Hello pipeline contient une activité de copie qui est configuré toouse hello des jeux de données d’entrée et de sortie et est toorun planifiée toutes les heures. Dans la définition JSON du pipeline hello, hello **source** type est défini trop**CassandraSource** et **récepteur** type est défini trop**BlobSink**.

Consultez [RelationalSource les propriétés de type](#copy-activity-properties) pour la liste des propriétés prises en charge par hello RelationalSource hello.

```json
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2016-06-01T18:00:00",
        "end":"2016-06-01T19:00:00",
        "description":"pipeline with copy activity",
        "activities":[  
        {
            "name": "CassandraToAzureBlob",
            "description": "Copy from Cassandra tooan Azure blob",
            "type": "Copy",
            "inputs": [
            {
                "name": "CassandraInput"
            }
            ],
            "outputs": [
            {
                "name": "AzureBlobOutput"
            }
            ],
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
        }
        ]    
    }
}
```

### <a name="type-mapping-for-cassandra"></a>Mappage de type pour Cassandra
| Type Cassandra | Type basé sur .Net |
| --- | --- |
| ASCII |String |
| BIGINT |Int64 |
| BLOB |Byte[] |
| BOOLEAN |BOOLEAN |
| DÉCIMAL |DÉCIMAL |
| DOUBLE |DOUBLE |
| FLOAT |Single |
| INET |String |
| INT |Int32 |
| TEXTE |String |
| TIMESTAMP |DateTime |
| TIMEUUID |Guid |
| UUID |Guid |
| VARCHAR |String |
| VARINT |Décimal |

> [!NOTE]
> Pour la collection de types (carte, ensemble, liste, etc.), consultez trop[travailler avec les types de collection Cassandra à l’aide de la table virtuelle](#work-with-collections-using-virtual-table) section.
>
> Les types définis par l’utilisateur ne sont pas pris en charge.
>
> longueur de Hello de longueurs de colonne binaire et de la colonne de chaîne ne peut pas être supérieure à 4000.
>
>

## <a name="work-with-collections-using-virtual-table"></a>Travailler avec des collections à l’aide d’une table virtuelle
Azure Data Factory utilise une intégrés ODBC driver tooconnect tooand copier les données de votre base de données Cassandra. Pour les types de collection, y compris la carte, ensemble et liste, les pilotes hello renormalise les données hello dans les tables virtuelles correspondants. Plus précisément, si une table contient des colonnes de la collection, pilote de hello génère hello tables virtuelles suivantes :

* A **table de base**, lequel contient hello les mêmes données que la table réelle de hello sauf pour les colonnes de regroupement hello. table de base Hello utilise hello même nom en tant que table réelle hello qu’elle représente.
* A **table virtuelle** pour chaque colonne de la collection, qui étend les données de salutation imbriquée. tables virtuelles Hello qui représentent des collections sont nommées à l’aide du nom hello de table réelle hello, un séparateur «*vt*» et le nom hello de colonne de hello.

Tables virtuelles font référence à des données de toohello dans la table réelle de hello, l’activation tooaccess de pilote hello hello données dénormalisées. Consultez la section Exemple pour plus d’informations. Vous pouvez accéder à contenu hello des collections de Cassandra en interrogeant et en joignant les tables virtuelles hello.

Vous pouvez utiliser hello [Assistant copie de](data-factory-data-movement-activities.md#create-a-pipeline-with-copy-activity) toointuitively vue hello la liste des tables de base de données Cassandra, y compris les tables virtuelles hello et afficher un aperçu des données hello à l’intérieur. Vous pouvez également créer une requête dans l’Assistant copie de hello et toosee hello résultat de la validation.

### <a name="example"></a>Exemple
Par exemple, hello suivant « ExampleTable » est une table de base de données Cassandra qui contient une colonne clé primaire d’entiers nommés « pk_int », une colonne de texte nommé value, une colonne de liste, une colonne de table et une colonne de jeu (nommé « StringSet »).

| pk_int | Valeur | Énumérer | Mappage | StringSet |
| --- | --- | --- | --- | --- |
| 1 |« exemple de valeur 1 » |[« 1 », « 2 », « 3 »] |{« S1 » : « a », « S2 » : « b »} |{« A », « B », « C »} |
| 3 |« exemple de valeur 3 » |[« 100 », « 101 », « 102 », « 105 »] |{« S1 » : « t »} |{« A », « E »} |

pilote de Hello génèrent plusieurs tables virtuelles toorepresent ce tableau. Hello colonnes clés étrangères dans les tables virtuelles hello référencer des colonnes de clé primaire hello dans la table réelle de hello et indiquer quels réel table ligne hello table virtuelle ligne correspond à.

table virtuelle de Hello première est la table de base hello nommé « ExampleTable » est indiqué dans hello tableau suivant. table de base Hello contient hello mêmes données que la table de base de données d’origine hello à l’exception des collections de hello, qui sont omis dans cette table et développés dans d’autres tables virtuelles.

| pk_int | Valeur |
| --- | --- |
| 1 |« exemple de valeur 1 » |
| 3 |« exemple de valeur 3 » |

Hello tableaux suivants indiquent les tables virtuelles hello qui renormalize données hello à partir de colonnes de liste, carte et StringSet hello. colonnes de Hello avec des noms qui se terminent par « _index » ou « _clés » indiquent position hello de données hello dans la liste d’origine de hello ou un mappage. les colonnes avec des noms qui se terminent par « _value » Hello contiennent des données de hello développé à partir de la collection de hello.

#### <a name="table-exampletablevtlist"></a>Table « ExampleTable_vt_List » :
| pk_int | List_index | List_value |
| --- | --- | --- |
| 1 |0 |1 |
| 1 |1 |2 |
| 1 |2 |3 |
| 3 |0 |100 |
| 3 |1 |101 |
| 3 |2 |102 |
| 3 |3 |103 |

#### <a name="table-exampletablevtmap"></a>Table « ExampleTable_vt_List » :
| pk_int | Map_key | Map_value |
| --- | --- | --- |
| 1 |S1 |Un  |
| 1 |S2 |b |
| 3 |S1 |t |

#### <a name="table-exampletablevtstringset"></a>Table « ExampleTable_vt_List » :
| pk_int | StringSet_value |
| --- | --- |
| 1 |Un  |
| 1 |b |
| 1 |C |
| 3 |Un  |
| 3 |E |

## <a name="map-source-toosink-columns"></a>Mapper les colonnes de source toosink
toolearn sur le mappage des colonnes dans toocolumns du jeu de données source dans le jeu de données récepteur, consultez [mappage des colonnes de jeu de données dans Azure Data Factory](data-factory-map-columns.md).

## <a name="repeatable-read-from-relational-sources"></a>Lecture renouvelée de sources relationnelles
Lors de la copie des données à partir de banques de données relationnelles, conserver la répétabilité dans l’esprit tooavoid des résultats inattendus. Dans Azure Data Factory, vous pouvez réexécuter une tranche manuellement. Vous pouvez également configurer une stratégie de nouvelles tentatives pour un jeu de données, afin qu’une tranche soit réexécutée en cas de défaillance. Lorsqu’une tranche est exécuté à nouveau dans les deux cas, vous devez toomake vraiment qui hello des mêmes données n’est en lecture aucune question comment plusieurs fois une tranche est exécutée. Voir [Lecture renouvelée de sources relationnelles](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).

## <a name="performance-and-tuning"></a>Performances et réglage
Consultez [copie activité optimiser les performances et Guide d’optimisation](data-factory-copy-activity-performance.md) toolearn sur la clé de facteurs d’affecter les performances de transfert de données (activité de copie) dans Azure Data Factory et de différentes façons toooptimize il.
