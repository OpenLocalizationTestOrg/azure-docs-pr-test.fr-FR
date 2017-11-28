---
title: "aaaIndexing une source de données de base de données Cosmos pour Azure Search | Documents Microsoft"
description: "Cet article vous explique comment toocreate un indexeur Azure Search avec DB Cosmos en tant que source de données."
services: search
documentationcenter: 
author: chaosrealm
manager: pablocas
editor: 
ms.assetid: 
ms.service: search
ms.devlang: rest-api
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: search
ms.date: 08/10/2017
ms.author: eugenesh
ms.openlocfilehash: 195c9bc026ee1591679dc425ef083a32a3c86be6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connecting-cosmos-db-with-azure-search-using-indexers"></a>Connexion de Cosmos DB à Recherche Azure à l’aide d’indexeurs

Si vous souhaitez tooimplement expérience d’une recherche sur vos données Cosmos DB, vous pouvez utiliser un Azure Search indexeur toopull de données dans un index Azure Search. Dans cet article, nous vous indiquons comment toointegrate base de données Azure Cosmos avec Azure Search sans avoir toowrite n’importe quelle infrastructure d’indexation de code toomaintain.

tooset d’un indexeur Cosmos DB, vous devez avoir un [service Azure Search](search-create-service-portal.md)et créer un index, la source de données et enfin indexeur de hello. Vous pouvez créer ces objets à l’aide de hello [portal](search-import-data-portal.md), [.NET SDK](/dotnet/api/microsoft.azure.search), ou [API REST](/rest/api/searchservice/) pour tous les langages non .NET. 

Si vous optez pour le portail de hello, hello [Assistant Importer des données](search-import-data-portal.md) vous guide tout au long de la création de hello de toutes ces ressources.

> [!NOTE]
> COSMOS DB est hello nouvelle génération de DocumentDB. Bien que la modification du nom de produit hello, syntaxe est hello même qu’avant. Continuer toospecify `documentdb` comme indiqué dans cet article de l’indexeur. 

> [!TIP]
> Vous pouvez lancer hello **importer des données** Assistant à partir de hello Cosmos de base de données du tableau de bord toosimplify l’indexation pour cette source de données. Dans la navigation de gauche, accédez trop**Collections** > **ajouter Azure Search** tooget a démarré.

<a name="Concepts"></a>
## <a name="azure-search-indexer-concepts"></a>Concepts d’indexeur Azure Search
Azure Search prend en charge hello création et la gestion des sources de données (y compris la base de données Cosmos) et indexeurs qui fonctionnent sur les sources de données.

A **source de données** spécifie hello données tooindex, les informations d’identification et les stratégies pour identifier les modifications apportées aux données hello (tels que les documents modifiés ou supprimés à l’intérieur de votre collection). source de données Hello définie en tant que ressources indépendantes de sorte qu’il peut être utilisé par plusieurs indexeurs.

Un **indexeur** décrit hello flux des données à partir de votre source de données dans un index de recherche cible. Un indexeur peut servir à :

* Effectuer une copie ponctuelle des données de hello toopopulate un index.
* Un index avec des modifications dans la source de données hello selon un calendrier de synchronisation. planification de Hello fait partie de la définition d’indexeur hello.
* Appeler l’index de tooan mises à jour à la demande en fonction des besoins.

<a name="CreateDataSource"></a>
## <a name="step-1-create-a-data-source"></a>Étape 1 : Création d’une source de données
toocreate une source de données, effectuez une publication :

    POST https://[service name].search.windows.net/datasources?api-version=2016-09-01
    Content-Type: application/json
    api-key: [Search service admin key]

    {
        "name": "mydocdbdatasource",
        "type": "documentdb",
        "credentials": {
            "connectionString": "AccountEndpoint=https://myDocDbEndpoint.documents.azure.com;AccountKey=myDocDbAuthKey;Database=myDocDbDatabaseId"
        },
        "container": { "name": "myDocDbCollectionId", "query": null },
        "dataChangeDetectionPolicy": {
            "@odata.type": "#Microsoft.Azure.Search.HighWaterMarkChangeDetectionPolicy",
            "highWaterMarkColumnName": "_ts"
        }
    }

corps de la Hello de demande de hello contient la définition de source de données hello, qui doit inclure hello suivant des champs :

* **nom**: choisissez toorepresent de n’importe quel nom de votre base de données de la base de données Cosmos.
* **type** : doit être `documentdb`.
* **credentials**:
  
  * **connectionString**: obligatoire. Spécifier la base de données de la base de données Azure Cosmos de tooyour de hello connexion info Bonjour suivant le format :`AccountEndpoint=<Cosmos DB endpoint url>;AccountKey=<Cosmos DB auth key>;Database=<Cosmos DB database id>`
* **container**:
  
  * **name**: obligatoire. Spécifiez des id de hello de hello Cosmos DB collection toobe indexé.
  * **query**: facultatif. Vous pouvez spécifier une requête de tooflatten un document JSON arbitraire dans un schéma plat Azure Search peut indexer.
* **dataChangeDetectionPolicy** : recommandé. Consultez la section [Indexation des documents modifiés](#DataChangeDetectionPolicy).
* **dataDeletionDetectionPolicy**: facultatif. Consultez la section [Indexation des documents supprimés](#DataDeletionDetectionPolicy).

### <a name="using-queries-tooshape-indexed-data"></a>À l’aide de requêtes tooshape données indexées
Vous pouvez spécifier un tooflatten de requête de base de données Cosmos des propriétés imbriquées ou des tableaux JSON propriétés de projet et filtrer hello toobe de données indexée. 

Exemple de document :

    {
        "userId": 10001,
        "contact": {
            "firstName": "andy",
            "lastName": "hoh"
        },
        "company": "microsoft",
        "tags": ["azure", "documentdb", "search"]
    }

Requête de filtre :

    SELECT * FROM c WHERE c.company = "microsoft" and c._ts >= @HighWaterMark ORDER BY c._ts

Requête d’aplatissage :

    SELECT c.id, c.userId, c.contact.firstName, c.contact.lastName, c.company, c._ts FROM c WHERE c._ts >= @HighWaterMark ORDER BY c._ts
    
    
Requête de projection :

    SELECT VALUE { "id":c.id, "Name":c.contact.firstName, "Company":c.company, "_ts":c._ts } FROM c WHERE c._ts >= @HighWaterMark ORDER BY c._ts


Requête d’aplatissage de tableau :

    SELECT c.id, c.userId, tag, c._ts FROM c JOIN tag IN c.tags WHERE c._ts >= @HighWaterMark ORDER BY c._ts

<a name="CreateIndex"></a>
## <a name="step-2-create-an-index"></a>Étape 2 : Création d’un index
Créez un index Azure Search cible si vous n'en possédez pas déjà un. Vous pouvez créer un index à l’aide de hello [interface utilisateur du portail Azure](search-create-index-portal.md), hello [API REST de Index créer](/rest/api/searchservice/create-index) ou [Index, classe](/dotnet/api/microsoft.azure.search.models.index).

Bonjour à l’exemple suivant crée un index avec un champ d’id et la description :

    POST https://[service name].search.windows.net/indexes?api-version=2016-09-01
    Content-Type: application/json
    api-key: [Search service admin key]

    {
       "name": "mysearchindex",
       "fields": [{
         "name": "id",
         "type": "Edm.String",
         "key": true,
         "searchable": false
       }, {
         "name": "description",
         "type": "Edm.String",
         "filterable": false,
         "sortable": false,
         "facetable": false,
         "suggestions": true
       }]
     }

Vérifiez que hello schéma de l’index cible est compatible avec le schéma hello de documents JSON hello ou sortie hello de projection de votre requête personnalisée.

> [!NOTE]
> Pour les collections partitionnées, clé de document par défaut hello est Cosmos DB `_rid` propriété, qui est renommée trop`rid` dans Azure Search. De même, les valeurs `_rid` de Cosmos DB contiennent des caractères qui ne sont pas valides dans les clés de Recherche Azure. Pour cette raison, hello `_rid` valeurs sont codées en Base64.
> 
> 

### <a name="mapping-between-json-data-types-and-azure-search-data-types"></a>Mappage entre les types de données JSON et les types de données Azure Search
| TYPE DE DONNÉES JSON | TYPES DE CHAMPS D’INDEX CIBLE COMPATIBLES |
| --- | --- |
| Bool |Edm.Boolean, Edm.String |
| Nombres qui ressemblent à des nombres entiers |Edm.Int32, Edm.Int64, Edm.String |
| Nombres qui ressemblent à des nombres avec points flottants |Edm.Double, Edm.String |
| String |Edm.String |
| Tableaux de types primitifs, par exemple ["a", "b", "c"] |Collection(Edm.String) |
| Chaînes qui ressemblent à des dates |Edm.DateTimeOffset, Edm.String |
| Objets GeoJSON, par exemple { "type": "Point", "coordinates": [long, lat] } |Edm.GeographyPoint |
| Autres objets JSON |N/A |

<a name="CreateIndexer"></a>
## <a name="step-3-create-an-indexer"></a>Étape 3 : Création d’un indexeur

Une fois que la source de données et d’index hello ont été créées, vous êtes indexeur de hello toocreate prêt :

    POST https://[service name].search.windows.net/indexers?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
      "name" : "mydocdbindexer",
      "dataSourceName" : "mydocdbdatasource",
      "targetIndexName" : "mysearchindex",
      "schedule" : { "interval" : "PT2H" }
    }

Cet indexeur s’exécute toutes les deux heures (intervalle de planification est défini trop « PT2H »). toorun un indexeur toutes les 30 minutes, définissez intervalle de salutation trop « PT30M ». intervalle de pris en charge le plus court Hello est de 5 minutes. Bonjour planification est facultative : en cas d’omission, un indexeur s’exécute qu’une seule fois lorsqu’il est créé. Toutefois, vous pouvez à tout moment exécuter un indexeur à la demande.   

Pour plus d’informations sur hello créer des API indexeur, l’extraction [créer un indexeur](https://docs.microsoft.com/rest/api/searchservice/create-indexer).

<a id="RunIndexer"></a>
### <a name="running-indexer-on-demand"></a>Exécution de l’indexeur à la demande
Dans toorunning Ajout périodiquement selon une planification, un indexeur peut également être appelé à la demande :

    POST https://[service name].search.windows.net/indexers/[indexer name]/run?api-version=2016-09-01
    api-key: [Search service admin key]

> [!NOTE]
> Lors de l’API d’exécution est retournée avec succès, appel de l’indexeur hello a été planifiée mais hello traitement se produit de façon asynchrone. 

Vous pouvez surveiller l’état de l’indexeur dans le portail de hello ou hello obtenir indexeur état API, qui nous allons décrire ensuite hello. 

<a name="GetIndexerStatus"></a>
### <a name="getting-indexer-status"></a>Obtention de l’état de l’indexeur
Vous pouvez récupérer hello statut et l’exécution de l’historique d’un indexeur :

    GET https://[service name].search.windows.net/indexers/[indexer name]/status?api-version=2016-09-01
    api-key: [Search service admin key]

réponse de Hello contient état global de l’indexeur, appel de l’indexeur dernière (ou en cours) hello et historique hello des appels récents de l’indexeur.

    {
        "status":"running",
        "lastResult": {
            "status":"success",
            "errorMessage":null,
            "startTime":"2014-11-26T03:37:18.853Z",
            "endTime":"2014-11-26T03:37:19.012Z",
            "errors":[],
            "itemsProcessed":11,
            "itemsFailed":0,
            "initialTrackingState":null,
            "finalTrackingState":null
         },
        "executionHistory":[ {
            "status":"success",
             "errorMessage":null,
            "startTime":"2014-11-26T03:37:18.853Z",
            "endTime":"2014-11-26T03:37:19.012Z",
            "errors":[],
            "itemsProcessed":11,
            "itemsFailed":0,
            "initialTrackingState":null,
            "finalTrackingState":null
        }]
    }

L’historique d’exécution contient des toohello 50 dernières exécutions, qui sont triées dans l’ordre chronologique inverse (de sorte que l’exécution de la plus récente de hello en premier dans la réponse de hello).

<a name="DataChangeDetectionPolicy"></a>
## <a name="indexing-changed-documents"></a>Indexation des documents modifiés
objectif Hello d’une donnée de modifier la stratégie de détection est tooefficiently identifient les éléments de données modifiées. Actuellement, la stratégie de hello uniquement pris en charge est hello `High Water Mark` stratégie à l’aide de hello `_ts` (timestamp) cette propriété est fournie par la base de données Cosmos, qui est spécifiée comme suit :

    {
        "@odata.type" : "#Microsoft.Azure.Search.HighWaterMarkChangeDetectionPolicy",
        "highWaterMarkColumnName" : "_ts"
    }

À l’aide de cette stratégie est fortement recommandé les performances de l’indexeur bon tooensure. 

Si vous utilisez une requête personnalisée, assurez-vous que hello `_ts` propriété est projetée par requête de hello.

<a name="IncrementalProgress"></a>
### <a name="incremental-progress-and-custom-queries"></a>Progression incrémentielle et requêtes personnalisées
Incrémentielles de progression pendant l’indexation de garantit que si l’exécution de l’indexeur est interrompue par des erreurs temporaires ou la limite de temps d’exécution, indexeur de hello peut reprendre là où il s’hors tension de la prochaine fois que qu’il s’exécute, au lieu d’avoir des index toore hello ensemble de la collection à partir de zéro. Ceci est particulièrement important lors de l’indexation de grandes collections. 

tooenable incrémentielles de progression lors de l’utilisation d’une requête personnalisée, assurez-vous que votre requête trie les résultats de hello en hello `_ts` colonne. Cela permet de périodiques ponctuels que Azure Search utilise tooprovide incrémentielles de progression en présence de hello d’échecs.   

Dans certains cas, même si votre requête contient un `ORDER BY [collection alias]._ts` clause, Azure Search ne peut pas déduire les cette requête hello est triée par hello `_ts`. Vous pouvez indiquer à Azure Search que les résultats sont triés à l’aide de hello `assumeOrderByHighWaterMarkColumn` propriété de configuration. toospecify cet indicateur, créer ou mettre à jour l’indexeur comme suit : 

    {
     ... other indexer definition properties
     "parameters" : {
            "configuration" : { "assumeOrderByHighWaterMarkColumn" : true } }
    } 

<a name="DataDeletionDetectionPolicy"></a>
## <a name="indexing-deleted-documents"></a>Indexation des documents supprimés
Lorsque des lignes sont supprimées à partir de la collection de hello, vous souhaitez normalement toodelete ces lignes à partir de l’index de recherche hello également. objectif de Hello d’une stratégie de détection de suppression de données est tooefficiently identifient les éléments de données supprimées. Actuellement, la stratégie de hello uniquement pris en charge est hello `Soft Delete` stratégie (suppression est marquée avec un indicateur quelconque), qui est spécifié comme suit :

    {
        "@odata.type" : "#Microsoft.Azure.Search.SoftDeleteColumnDeletionDetectionPolicy",
        "softDeleteColumnName" : "hello property that specifies whether a document was deleted",
        "softDeleteMarkerValue" : "hello value that identifies a document as deleted"
    }

Si vous utilisez une requête personnalisée, assurez-vous que cette propriété hello référencée par `softDeleteColumnName` est projetée par requête de hello.

Bonjour à l’exemple suivant crée une source de données avec une stratégie de soft-suppression :

    POST https://[Search service name].search.windows.net/datasources?api-version=2016-09-01
    Content-Type: application/json
    api-key: [Search service admin key]

    {
        "name": "mydocdbdatasource",
        "type": "documentdb",
        "credentials": {
            "connectionString": "AccountEndpoint=https://myDocDbEndpoint.documents.azure.com;AccountKey=myDocDbAuthKey;Database=myDocDbDatabaseId"
        },
        "container": { "name": "myDocDbCollectionId" },
        "dataChangeDetectionPolicy": {
            "@odata.type": "#Microsoft.Azure.Search.HighWaterMarkChangeDetectionPolicy",
            "highWaterMarkColumnName": "_ts"
        },
        "dataDeletionDetectionPolicy": {
            "@odata.type": "#Microsoft.Azure.Search.SoftDeleteColumnDeletionDetectionPolicy",
            "softDeleteColumnName": "isDeleted",
            "softDeleteMarkerValue": "true"
        }
    }

## <a name="NextSteps"></a>Étapes suivantes
Félicitations ! Vous avez appris comment toointegrate base de données Azure Cosmos avec Azure Search à l’aide hello indexeur pour la base de données Cosmos.

* toolearn comment plus sur la base de données Azure Cosmos, consultez hello [page de service de base de données Cosmos](https://azure.microsoft.com/services/documentdb/).
* toolearn comment plus sur Azure Search, consultez hello [page de service de recherche](https://azure.microsoft.com/services/search/).
