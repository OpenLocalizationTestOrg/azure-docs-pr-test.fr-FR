---
title: "aaaWorking avec les données géographiques dans la base de données Azure Cosmos | Documents Microsoft"
description: "Comprendre comment toocreate, index et interroger des objets spatiaux avec la base de données Azure Cosmos et hello API DocumentDB."
services: cosmos-db
documentationcenter: 
author: arramac
manager: jhubbard
editor: monicar
ms.assetid: 82ce2898-a9f9-4acf-af4d-8ca4ba9c7b8f
ms.service: cosmos-db
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 05/22/2017
ms.author: arramac
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a1e40b78cb4595631d845d46c21d07a30c8b972f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-geospatial-and-geojson-location-data-in-azure-cosmos-db"></a>Utilisation de données d’emplacement géospatiales et GeoJSON dans Azure Cosmos DB
Cet article est une fonctionnalité de geospatial introduction toohello dans [base de données Azure Cosmos](https://azure.microsoft.com/services/cosmos-db/). Après avoir lu ce problème, vous serez hello en mesure de tooanswer suivant questions :

* Comment puis-je stocker des données spatiales dans Azure Cosmos DB ?
* Comment puis-je interroger des données géospaciales dans Azure Cosmos DB dans SQL et LINQ ?
* Comment puis-je activer ou désactiver l’indexation spatiale dans Azure Cosmos DB ?

Cet article explique comment toowork avec les données spatiales avec hello API DocumentDB. Consultez ce [projet GitHub](https://github.com/Azure/azure-documentdb-dotnet/blob/master/samples/code-samples/Geospatial/Program.cs) pour obtenir des échantillons de code.

## <a name="introduction-toospatial-data"></a>Données de toospatial de présentation
Données spatiales décrivent la position de hello et la forme d’objets dans l’espace. Dans la plupart des applications, celles-ci correspondent tooobjects sur terre hello, autrement dit, les données géographiques. Données spatiales peuvent être à l’emplacement de hello toorepresent utilisé d’une personne, un point d’intérêt, ou hello une limite d’une ville ou un lac. Les scénarios d'utilisation courants impliquent souvent des requêtes de proximité, comme « rechercher tous les cafés près de mon emplacement actuel ». 

### <a name="geojson"></a>GeoJSON
Base de données Azure Cosmos prend en charge l’indexation et l’interrogation des données géospatiales point qui sont représentées à l’aide de hello [GeoJSON spécification](https://tools.ietf.org/html/rfc7946). Les structures de données GeoJSON sont toujours des objets JSON valides, afin de pouvoir les stocker et les interroger à l’aide d’Azure Cosmos DB, sans bibliothèques ou outils spécialisés. Hello kits de développement de base de données Azure Cosmos fournissent des classes d’assistance et les méthodes qui la rendent facile toowork avec les données spatiales. 

### <a name="points-linestrings-and-polygons"></a>Points, LineStrings et polygones
Un **point** désigne une position unique dans l'espace. Dans les données géographiques, un Point représente emplacement exact hello, qui peut être une adresse postale d’une épicerie, une borne, une voiture ou une ville.  Un point est représenté dans GeoJSON (et Azure Cosmos DB) à l’aide de sa paire de coordonnées ou de longitude et latitude. Voici un exemple JSON pour un point.

**Points dans Azure Cosmos DB**

```json
{
    "type":"Point",
    "coordinates":[ 31.9, -4.8 ]
}
```

> [!NOTE]
> Hello GeoJSON spécification spécifie la longitude latitude premier et le deuxième. Comme dans d'autres applications de mappage, la longitude et la latitude sont des angles et sont exprimées en degrés. Les valeurs de longitude sont mesurées à partir du premier méridien de hello et sont comprises entre -180 et degrés 180.0 et latitude valeurs sont mesurés à partir de l’Équateur de hello et sont comprises entre -90.0 et 90.0 degrés. 
> 
> Base de données Azure Cosmos interprète les coordonnées comme représenté par le système de référence-WGS 84 hello. Voir ci-dessous pour plus d'informations sur les systèmes de coordonnées de référence.
> 
> 

Cela peut être incorporé dans un document Azure Cosmos DB, comme illustré dans cet exemple de profil utilisateur contenant des données d’emplacement :

**Utilisation de profil avec emplacement stocké dans Azure Cosmos DB**

```json
{
    "id":"documentdb-profile",
    "screen_name":"@CosmosDB",
    "city":"Redmond",
    "topics":[ "global", "distributed" ],
    "location":{
        "type":"Point",
        "coordinates":[ 31.9, -4.8 ]
    }
}
```

En outre toopoints, GeoJSON prend également en charge LineStrings et des polygones. **LineStrings** représentent une série de deux ou plusieurs points dans l’espace et hello des segments de ligne qui les connectent. Dans les données géographiques, LineStrings sont couramment utilisés toorepresent autoroutes ou cours d’eau. Un **polygone** est une limite de points reliés qui constitue une LineString fermée. Polygones sont formations naturel de toorepresent couramment utilisés comme des lacs ou politiques juridictions telles que les États et villes. Voici un exemple de polygone dans Azure Cosmos DB. 

**Polygones dans GeoJSON**

```json
{
    "type":"Polygon",
    "coordinates":[
        [ 31.8, -5 ],
        [ 31.8, -4.7 ],
        [ 32, -4.7 ],
        [ 32, -5 ],
        [ 31.8, -5 ]
    ]
}
```

> [!NOTE]
> Hello GeoJSON spécification requiert que pour les polygones valides, hello dernière paire de coordonnées fourni doit être identique à hello comme hello, toocreate tout d’abord, une forme fermée.
> 
> Les points dans un polygone doivent être spécifiés dans le sens antihoraire. Un polygone spécifié dans le sens horaire représente inverse hello de région de hello qu’il contient.
> 
> 

Dans Ajout tooPoint, LineString et polygone, GeoJSON spécifie également pour la représentation sous forme de hello toogroup plusieurs emplacements géographiques, ainsi que comme des propriétés arbitraires tooassociate avec un emplacement géographique qu’un **fonctionnalité**. Étant donné que ces objets sont des JSON valides, ils peuvent tous être stockés et traités dans Azure Cosmos DB. Cependant, Azure Cosmos DB prend uniquement en charge l’indexation automatique des points.

### <a name="coordinate-reference-systems"></a>Coordination des systèmes de référence
Forme hello de terre de hello étant anormale, les coordonnées des données géospatiales est représenté dans de nombreux systèmes de coordonnées de référence (DM), chacun ayant leurs propres images de référence et les unités de mesure. Par exemple, hello « Grille National de Grande-Bretagne » est un système de référence est très précis pour hello Royaume-Uni, mais pas à l’extérieur. 

Hello CRS les plus populaires en cours d’utilisation est aujourd'hui hello World Geodetic System [-WGS 84](http://earth-info.nga.mil/GandG/wgs84/). Les périphériques GPS et de nombreux services de mappage, notamment les API Bing Maps et Google Maps, utilisent le WGS-84. Base de données Azure Cosmos prend en charge l’indexation et l’interrogation des données géospatiales à l’aide de hello-WGS 84 CRS. 

## <a name="creating-documents-with-spatial-data"></a>Création de documents avec les données spatiales
Lorsque vous créez des documents qui contiennent des valeurs GeoJSON, ils sont automatiquement indexés avec un index spatial dans la stratégie d’indexation conformément aux toohello de collection de hello. Si vous travaillez avec un Kit de développement logiciel (SDK) Azure Cosmos DB dans un langage saisi dynamiquement comme Python ou Node.js, vous devez créer un GeoJSON valide.

**Création d’un document avec les données géographiques dans Node.js**

```json
var userProfileDocument = {
    "name":"documentdb",
    "location":{
        "type":"Point",
        "coordinates":[ -122.12, 47.66 ]
    }
};

client.createDocument(`dbs/${databaseName}/colls/${collectionName}`, userProfileDocument, (err, created) => {
    // additional code within hello callback
});
```

Si vous travaillez avec hello APIs DocumentDB, vous pouvez utiliser hello `Point` et `Polygon` classes hello `Microsoft.Azure.Documents.Spatial` des informations d’emplacement de tooembed d’espace de noms dans les objets de votre application. Ces classes permettent de simplifier la sérialisation de hello et la désérialisation des données spatiales dans GeoJSON.

**Création d’un document avec les données géographiques dans .NET**

```json
using Microsoft.Azure.Documents.Spatial;

public class UserProfile
{
    [JsonProperty("name")]
    public string Name { get; set; }

    [JsonProperty("location")]
    public Point Location { get; set; }

    // More properties
}

await client.CreateDocumentAsync(
    UriFactory.CreateDocumentCollectionUri("db", "profiles"), 
    new UserProfile 
    { 
        Name = "documentdb", 
        Location = new Point (-122.12, 47.66) 
    });
```

Si vous n’avez pas les informations de latitude et longitude hello, mais avez des adresses physiques de hello ou nom de l’emplacement comme ville ou pays, vous pouvez rechercher les coordonnées réel hello à l’aide d’un service de géocodage comme Services REST Bing Maps. En savoir plus sur le géocodage de Bing Maps [ici](https://msdn.microsoft.com/library/ff701713.aspx).

## <a name="querying-spatial-types"></a>Interrogation des types spatiaux
Maintenant que nous avons observez comment les données géospatiales tooinsert, examinons la tooquery ces données à l’aide de la base de données Azure Cosmos à l’aide de SQL et LINQ.

### <a name="spatial-sql-built-in-functions"></a>Fonctions spatiales SQL intégrées
Base de données Azure Cosmos prend en charge hello suivant des fonctions intégrées d’Open Geospatial Consortium (OGC) pour l’interrogation de géographiques. Pour plus d’informations sur l’ensemble complet de hello de fonctions intégrées dans hello langage SQL, consultez trop[base de données de requête Azure Cosmos](documentdb-sql-query.md).

<table>
<tr>
  <td><strong>Utilisation</strong></td>
  <td><strong>Description</strong></td>
</tr>
<tr>
  <td>ST_DISTANCE (spatial_expr, spatial_expr)</td>
  <td>Retourne la distance hello entre les expressions LineString, Polygon ou GeoJSON Point hello deux.</td>
</tr>
<tr>
  <td>ST_WITHIN (spatial_expr, spatial_expr)</td>
  <td>Retourne une expression booléenne indiquant si hello premier GeoJSON objet (Point, polygone ou LineString) se trouve dans hello deuxième GeoJSON objet (Point, polygone ou LineString).</td>
</tr>
<tr>
  <td>ST_INTERSECTS (spatial_expr, spatial_expr)</td>
  <td>Retourne une expression booléenne indiquant si hello deux GeoJSON objets spécifiés (Point, polygone ou LineString) se croisent.</td>
</tr>
<tr>
  <td>ST_ISVALID</td>
  <td>Retourne une valeur booléenne indiquant si hello spécifiée expression LineString, Polygon ou GeoJSON Point n’est valide.</td>
</tr>
<tr>
  <td>ST_ISVALIDDETAILED</td>
  <td>Retourne une valeur JSON contenant une valeur booléenne si hello de l’expression LineString, Polygon ou GeoJSON Point spécifiée est valide et si elle est non valide, en outre hello motif en tant que valeur de chaîne.</td>
</tr>
</table>

Les fonctions spatiale peuvent être des requêtes de proximité tooperform utilisé par rapport aux données spatiales. Par exemple, voici une requête qui retourne la que famille de tous les documents qu’est 30 kilomètres de hello emplacement spécifié à l’aide de fonctions intégrées de ST_DISTANCE hello. 

**Requête**

    SELECT f.id 
    FROM Families f 
    WHERE ST_DISTANCE(f.location, {'type': 'Point', 'coordinates':[31.9, -4.8]}) < 30000

**Résultats**

    [{
      "id": "WakefieldFamily"
    }]

Si vous incluez l’indexation spatiale dans votre stratégie d’indexation, puis « requêtes à distance » seront pris en charge efficacement par le biais des index de hello. Pour plus d’informations sur l’indexation spatiale, consultez la section hello ci-dessous. Si vous n’avez pas un spatial index pour hello spécifié des chemins d’accès, vous pouvez encore effectuer des requêtes spatiales en spécifiant `x-ms-documentdb-query-enable-scan` en-tête de demande avec la valeur de hello défini trop « true ». Dans .NET, cela est possible en hello en passant facultatif **FeedOptions** tooqueries argument avec [EnableScanInQuery](https://msdn.microsoft.com/library/microsoft.azure.documents.client.feedoptions.enablescaninquery.aspx#P:Microsoft.Azure.Documents.Client.FeedOptions.EnableScanInQuery) définir tootrue. 

ST_WITHIN peut être utilisé toocheck si un point se trouve dans un polygone. En règle générale polygones sont des limites de toorepresent utilisés comme codes postaux, les frontières de l’état ou les formations naturelles. À nouveau si vous incluez l’indexation spatiale dans votre stratégie d’indexation, puis requêtes « dans » seront pris en charge efficacement par le biais des index de hello. 

Arguments de polygone dans ST_WITHIN peuvent contenir uniquement un anneau unique, c'est-à-dire hello polygones ne doit pas contenir de trous. 

**Requête**

    SELECT * 
    FROM Families f 
    WHERE ST_WITHIN(f.location, {
        'type':'Polygon', 
        'coordinates': [[[31.8, -5], [32, -5], [32, -4.7], [31.8, -4.7], [31.8, -5]]]
    })

**Résultats**

    [{
      "id": "WakefieldFamily",
    }]

> [!NOTE]
> Types toohow incompatible similaires fonctionne dans la requête de base de données Azure Cosmos, si la valeur hello emplacement spécifié dans soit argument est mal formé ou non valide, puis il évalue trop**non défini** et hello évaluée document toobe ignorées à partir de hello résultats de la requête. Si votre requête ne retourne aucun résultat, exécutez toodebug ST_ISVALIDDETAILED pourquoi type spatail de hello n’est pas valide.     
> 
> 

Base de données Azure Cosmos prend également en charge les interrogations inverse, par exemple, vous pouvez indexer des polygones ou lignes de base de données Azure Cosmos, puis rechercher des zones hello contenant un point spécifié. Ce modèle est utilisé communément dans logistique tooidentify par exemple, quand un camion entre ou quitte une région. 

**Requête**

    SELECT * 
    FROM Areas a 
    WHERE ST_WITHIN({'type': 'Point', 'coordinates':[31.9, -4.8]}, a.location)


**Résultats**

    [{
      "id": "MyDesignatedLocation",
      "location": {
        "type":"Polygon", 
        "coordinates": [[[31.8, -5], [32, -5], [32, -4.7], [31.8, -4.7], [31.8, -5]]]
      }
    }]

ST_ISVALID et ST_ISVALIDDETAILED peuvent être utilisé toocheck si un objet spatial est valide. Par exemple, hello suivant de requête vérifie la validité de hello d’un point avec une valeur hors limites latitude (-132.8). ST_ISVALID retourne simplement une valeur booléenne et ST_ISVALIDDETAILED renvoie hello booléenne et une chaîne contenant la raison hello pourquoi il est considéré comme non valide.

** Requête **

    SELECT ST_ISVALID({ "type": "Point", "coordinates": [31.9, -132.8] })

**Résultats**

    [{
      "$1": false
    }]

Ces fonctions peuvent également être utilisés toovalidate polygones. Par exemple, nous utilisons ici ST_ISVALIDDETAILED toovalidate un polygone n’est pas fermé. 

**Requête**

    SELECT ST_ISVALIDDETAILED({ "type": "Polygon", "coordinates": [[ 
        [ 31.8, -5 ], [ 31.8, -4.7 ], [ 32, -4.7 ], [ 32, -5 ] 
        ]]})

**Résultats**

    [{
       "$1": { 
            "valid": false, 
            "reason": "hello Polygon input is not valid because hello start and end points of hello ring number 1 are not hello same. Each ring of a Polygon must have hello same start and end points." 
          }
    }]

### <a name="linq-querying-in-hello-net-sdk"></a>L’interrogation LINQ Bonjour .NET SDK
Hello DocumentDB .NET SDK également les fournisseurs de stub méthodes `Distance()` et `Within()` pour une utilisation dans des expressions LINQ. fournisseur de DocumentDB LINQ Hello traduit ces méthode appels toohello équivalent SQL appels de fonction intégrée (ST_DISTANCE et ST_WITHIN respectivement). 

Voici un exemple d’une requête LINQ qui recherche tous les documents dans la collection de base de données Azure Cosmos hello dont la valeur « location » est dans un rayon de 30 kilomètres de hello spécifiée point à l’aide de LINQ.

**Requête LINQ de distance**

    foreach (UserProfile user in client.CreateDocumentQuery<UserProfile>(UriFactory.CreateDocumentCollectionUri("db", "profiles"))
        .Where(u => u.ProfileType == "Public" && a.Location.Distance(new Point(32.33, -4.66)) < 30000))
    {
        Console.WriteLine("\t" + user);
    }

De même, voici une requête pour rechercher tous les documents hello dont « location » est dans hello spécifié boîte/polygone. 

**Requête LINQ within**

    Polygon rectangularArea = new Polygon(
        new[]
        {
            new LinearRing(new [] {
                new Position(31.8, -5),
                new Position(32, -5),
                new Position(32, -4.7),
                new Position(31.8, -4.7),
                new Position(31.8, -5)
            })
        });

    foreach (UserProfile user in client.CreateDocumentQuery<UserProfile>(UriFactory.CreateDocumentCollectionUri("db", "profiles"))
        .Where(a => a.Location.Within(rectangularArea)))
    {
        Console.WriteLine("\t" + user);
    }


Maintenant que nous avons observez comment les documents de tooquery à l’aide de LINQ et SQL, examinons la tooconfigure base de données Azure Cosmos pour l’indexation spatiale.

## <a name="indexing"></a>Indexation
Comme décrit dans hello [schéma agnostique en termes d’indexation avec la base de données Azure Cosmos](http://www.vldb.org/pvldb/vol8/p1668-shukla.pdf) papier, nous avons conçu toobe de moteur de base de données Azure Cosmos DB réellement indépendant du schéma et de la première classe prennent en charge de JSON. en mode natif, le moteur de base de données d’écriture optimisé Hello de base de données Azure Cosmos comprend des données spatiales (points, lignes et les polygones) représentées dans la norme de GeoJSON hello.

En bref, géométrie de hello est projetée à partir des coordonnées géodésiques sur un plan 2D puis divisée progressivement les cellules à l’aide un **quadtree**. Ces cellules sont mappés too1D basés sur l’emplacement de hello de cellule hello dans un **courbe de remplissage d’espace de Hilbert**, qui permet de préserver la localité de points. En outre lorsque les données d’emplacement sont indexées, il passe par un processus appelé **pavage**, autrement dit, toutes les cellules de hello qui se croisent à un emplacement sont identifiées et stockées en tant que clés dans l’index de base de données Azure Cosmos hello. Au moment de la requête, arguments telles que les points et des polygones sont également fractionné tooextract hello des plages d’ID de cellule appropriée, puis utilisé tooretrieve des données à partir de l’index de hello.

Si vous spécifiez une stratégie d’indexation qui inclut un index spatial pour / * (tous les chemins d’accès), tous les points trouvés au sein de la collection de hello sont indexés pour des requêtes spatiales efficace (ST_WITHIN et ST_DISTANCE). Les index spatiaux n'ont pas une valeur de précision et utilisent toujours une valeur de précision par défaut.

> [!NOTE]
> Azure Cosmos DB prend en charge l’indexation automatique des points, polygones et lineStrings.
> 
> 

Hello extrait de code JSON suivant illustre une stratégie d’indexation avec indexation spatiale activé, autrement dit, l’index n’importe quel point GeoJSON trouvé au sein de documents pour les requêtes spatiales. Si vous modifiez hello l’indexation de stratégie à l’aide de hello portail Azure, vous pouvez spécifier hello suivant JSON pour l’indexation tooenable stratégie spatiale de l’indexation sur votre collection.

**Stratégie d’indexation de collection JSON avec Spatial activé pour les points et les polygones**

    {
       "automatic":true,
       "indexingMode":"Consistent",
       "includedPaths":[
          {
             "path":"/*",
             "indexes":[
                {
                   "kind":"Range",
                   "dataType":"String",
                   "precision":-1
                },
                {
                   "kind":"Range",
                   "dataType":"Number",
                   "precision":-1
                },
                {
                   "kind":"Spatial",
                   "dataType":"Point"
                },
                {
                   "kind":"Spatial",
                   "dataType":"Polygon"
                }                
             ]
          }
       ],
       "excludedPaths":[
       ]
    }

Voici un extrait de code dans .NET qui montre comment toocreate une collection de l’indexation spatiale activé pour tous les chemins d’accès contenant des points. 

**Création d’une collection avec l'indexation spatiale**

    DocumentCollection spatialData = new DocumentCollection()
    spatialData.IndexingPolicy = new IndexingPolicy(new SpatialIndex(DataType.Point)); //override tooturn spatial on by default
    collection = await client.CreateDocumentCollectionAsync(UriFactory.CreateDatabaseUri("db"), spatialData);

Et Voici comment vous pouvez modifier un existant collection tootake des avantages de l’indexation spatiale sur tous les points qui sont stockés dans les documents.

**Modification d’une collection existante avec l'indexation spatiale**

    Console.WriteLine("Updating collection with spatial indexing enabled in indexing policy...");
    collection.IndexingPolicy = new IndexingPolicy(new SpatialIndex(DataType.Point));
    await client.ReplaceDocumentCollectionAsync(collection);

    Console.WriteLine("Waiting for indexing toocomplete...");
    long indexTransformationProgress = 0;
    while (indexTransformationProgress < 100)
    {
        ResourceResponse<DocumentCollection> response = await client.ReadDocumentCollectionAsync(UriFactory.CreateDocumentCollectionUri("db", "coll"));
        indexTransformationProgress = response.IndexTransformationProgress;

        await Task.Delay(TimeSpan.FromSeconds(1));
    }

> [!NOTE]
> Si l’emplacement hello valeur GeoJSON dans le document de hello est incorrect ou non valide, puis il ne sera pas été indexé pour les requêtes spatiales. Vous pouvez valider les valeurs d'emplacement à l'aide de ST_ISVALID et ST_ISVALIDDETAILED.
> 
> Si la définition de votre collection contient une clé de partition, la progression de la transformation d’indexation n’est pas signalée. 
> 
> 

## <a name="next-steps"></a>Étapes suivantes
Maintenant que vous avez appris sur comment tooget démarrer avec prise en charge géographique dans la base de données Azure Cosmos, vous pouvez :

* Démarrer le codage avec hello [exemples de code Geospatial .NET sur GitHub](https://github.com/Azure/azure-documentdb-dotnet/blob/fcf23d134fc5019397dcf7ab97d8d6456cd94820/samples/code-samples/Geospatial/Program.cs)
* Découvrir avec geospatial interrogeant au hello [Azure Cosmos DB Query Playground](http://www.documentdb.com/sql/demo#geospatial)
* En savoir plus sur les [requêtes Azure Cosmos DB](documentdb-sql-query.md)
* En savoir plus sur les [stratégies d’indexation Azure Cosmos DB](indexing-policies.md)

