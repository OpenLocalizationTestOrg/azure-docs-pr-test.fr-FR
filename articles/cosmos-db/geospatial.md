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
# <a name="working-with-geospatial-and-geojson-location-data-in-azure-cosmos-db"></a><span data-ttu-id="52d92-103">Utilisation de données d’emplacement géospatiales et GeoJSON dans Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="52d92-103">Working with geospatial and GeoJSON location data in Azure Cosmos DB</span></span>
<span data-ttu-id="52d92-104">Cet article est une fonctionnalité de geospatial introduction toohello dans [base de données Azure Cosmos](https://azure.microsoft.com/services/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="52d92-104">This article is an introduction toohello geospatial functionality in [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span></span> <span data-ttu-id="52d92-105">Après avoir lu ce problème, vous serez hello en mesure de tooanswer suivant questions :</span><span class="sxs-lookup"><span data-stu-id="52d92-105">After reading this, you will be able tooanswer hello following questions:</span></span>

* <span data-ttu-id="52d92-106">Comment puis-je stocker des données spatiales dans Azure Cosmos DB ?</span><span class="sxs-lookup"><span data-stu-id="52d92-106">How do I store spatial data in Azure Cosmos DB?</span></span>
* <span data-ttu-id="52d92-107">Comment puis-je interroger des données géospaciales dans Azure Cosmos DB dans SQL et LINQ ?</span><span class="sxs-lookup"><span data-stu-id="52d92-107">How can I query geospatial data in Azure Cosmos DB in SQL and LINQ?</span></span>
* <span data-ttu-id="52d92-108">Comment puis-je activer ou désactiver l’indexation spatiale dans Azure Cosmos DB ?</span><span class="sxs-lookup"><span data-stu-id="52d92-108">How do I enable or disable spatial indexing in Azure Cosmos DB?</span></span>

<span data-ttu-id="52d92-109">Cet article explique comment toowork avec les données spatiales avec hello API DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="52d92-109">This article shows how toowork with spatial data with hello DocumentDB API.</span></span> <span data-ttu-id="52d92-110">Consultez ce [projet GitHub](https://github.com/Azure/azure-documentdb-dotnet/blob/master/samples/code-samples/Geospatial/Program.cs) pour obtenir des échantillons de code.</span><span class="sxs-lookup"><span data-stu-id="52d92-110">Please see this [GitHub project](https://github.com/Azure/azure-documentdb-dotnet/blob/master/samples/code-samples/Geospatial/Program.cs) for code samples.</span></span>

## <a name="introduction-toospatial-data"></a><span data-ttu-id="52d92-111">Données de toospatial de présentation</span><span class="sxs-lookup"><span data-stu-id="52d92-111">Introduction toospatial data</span></span>
<span data-ttu-id="52d92-112">Données spatiales décrivent la position de hello et la forme d’objets dans l’espace.</span><span class="sxs-lookup"><span data-stu-id="52d92-112">Spatial data describes hello position and shape of objects in space.</span></span> <span data-ttu-id="52d92-113">Dans la plupart des applications, celles-ci correspondent tooobjects sur terre hello, autrement dit, les données géographiques.</span><span class="sxs-lookup"><span data-stu-id="52d92-113">In most applications, these correspond tooobjects on hello earth, i.e. geospatial data.</span></span> <span data-ttu-id="52d92-114">Données spatiales peuvent être à l’emplacement de hello toorepresent utilisé d’une personne, un point d’intérêt, ou hello une limite d’une ville ou un lac.</span><span class="sxs-lookup"><span data-stu-id="52d92-114">Spatial data can be used toorepresent hello location of a person, a place of interest, or hello boundary of a city, or a lake.</span></span> <span data-ttu-id="52d92-115">Les scénarios d'utilisation courants impliquent souvent des requêtes de proximité, comme « rechercher tous les cafés près de mon emplacement actuel ».</span><span class="sxs-lookup"><span data-stu-id="52d92-115">Common use cases often involve proximity queries, for e.g., "find all coffee shops near my current location".</span></span> 

### <a name="geojson"></a><span data-ttu-id="52d92-116">GeoJSON</span><span class="sxs-lookup"><span data-stu-id="52d92-116">GeoJSON</span></span>
<span data-ttu-id="52d92-117">Base de données Azure Cosmos prend en charge l’indexation et l’interrogation des données géospatiales point qui sont représentées à l’aide de hello [GeoJSON spécification](https://tools.ietf.org/html/rfc7946).</span><span class="sxs-lookup"><span data-stu-id="52d92-117">Azure Cosmos DB supports indexing and querying of geospatial point data that's represented using hello [GeoJSON specification](https://tools.ietf.org/html/rfc7946).</span></span> <span data-ttu-id="52d92-118">Les structures de données GeoJSON sont toujours des objets JSON valides, afin de pouvoir les stocker et les interroger à l’aide d’Azure Cosmos DB, sans bibliothèques ou outils spécialisés.</span><span class="sxs-lookup"><span data-stu-id="52d92-118">GeoJSON data structures are always valid JSON objects, so they can be stored and queried using Azure Cosmos DB without any specialized tools or libraries.</span></span> <span data-ttu-id="52d92-119">Hello kits de développement de base de données Azure Cosmos fournissent des classes d’assistance et les méthodes qui la rendent facile toowork avec les données spatiales.</span><span class="sxs-lookup"><span data-stu-id="52d92-119">hello Azure Cosmos DB SDKs provide helper classes and methods that make it easy toowork with spatial data.</span></span> 

### <a name="points-linestrings-and-polygons"></a><span data-ttu-id="52d92-120">Points, LineStrings et polygones</span><span class="sxs-lookup"><span data-stu-id="52d92-120">Points, LineStrings and Polygons</span></span>
<span data-ttu-id="52d92-121">Un **point** désigne une position unique dans l'espace.</span><span class="sxs-lookup"><span data-stu-id="52d92-121">A **Point** denotes a single position in space.</span></span> <span data-ttu-id="52d92-122">Dans les données géographiques, un Point représente emplacement exact hello, qui peut être une adresse postale d’une épicerie, une borne, une voiture ou une ville.</span><span class="sxs-lookup"><span data-stu-id="52d92-122">In geospatial data, a Point represents hello exact location, which could be a street address of a grocery store, a kiosk, an automobile or a city.</span></span>  <span data-ttu-id="52d92-123">Un point est représenté dans GeoJSON (et Azure Cosmos DB) à l’aide de sa paire de coordonnées ou de longitude et latitude.</span><span class="sxs-lookup"><span data-stu-id="52d92-123">A point is represented in GeoJSON (and Azure Cosmos DB) using its coordinate pair or longitude and latitude.</span></span> <span data-ttu-id="52d92-124">Voici un exemple JSON pour un point.</span><span class="sxs-lookup"><span data-stu-id="52d92-124">Here's an example JSON for a point.</span></span>

<span data-ttu-id="52d92-125">**Points dans Azure Cosmos DB**</span><span class="sxs-lookup"><span data-stu-id="52d92-125">**Points in Azure Cosmos DB**</span></span>

```json
{
    "type":"Point",
    "coordinates":[ 31.9, -4.8 ]
}
```

> [!NOTE]
> <span data-ttu-id="52d92-126">Hello GeoJSON spécification spécifie la longitude latitude premier et le deuxième.</span><span class="sxs-lookup"><span data-stu-id="52d92-126">hello GeoJSON specification specifies longitude first and latitude second.</span></span> <span data-ttu-id="52d92-127">Comme dans d'autres applications de mappage, la longitude et la latitude sont des angles et sont exprimées en degrés.</span><span class="sxs-lookup"><span data-stu-id="52d92-127">Like in other mapping applications, longitude and latitude are angles and represented in terms of degrees.</span></span> <span data-ttu-id="52d92-128">Les valeurs de longitude sont mesurées à partir du premier méridien de hello et sont comprises entre -180 et degrés 180.0 et latitude valeurs sont mesurés à partir de l’Équateur de hello et sont comprises entre -90.0 et 90.0 degrés.</span><span class="sxs-lookup"><span data-stu-id="52d92-128">Longitude values are measured from hello Prime Meridian and are between -180 and 180.0 degrees, and latitude values are measured from hello equator and are between -90.0 and 90.0 degrees.</span></span> 
> 
> <span data-ttu-id="52d92-129">Base de données Azure Cosmos interprète les coordonnées comme représenté par le système de référence-WGS 84 hello.</span><span class="sxs-lookup"><span data-stu-id="52d92-129">Azure Cosmos DB interprets coordinates as represented per hello WGS-84 reference system.</span></span> <span data-ttu-id="52d92-130">Voir ci-dessous pour plus d'informations sur les systèmes de coordonnées de référence.</span><span class="sxs-lookup"><span data-stu-id="52d92-130">Please see below for more details about coordinate reference systems.</span></span>
> 
> 

<span data-ttu-id="52d92-131">Cela peut être incorporé dans un document Azure Cosmos DB, comme illustré dans cet exemple de profil utilisateur contenant des données d’emplacement :</span><span class="sxs-lookup"><span data-stu-id="52d92-131">This can be embedded in an Azure Cosmos DB document as shown in this example of a user profile containing location data:</span></span>

<span data-ttu-id="52d92-132">**Utilisation de profil avec emplacement stocké dans Azure Cosmos DB**</span><span class="sxs-lookup"><span data-stu-id="52d92-132">**Use Profile with Location stored in Azure Cosmos DB**</span></span>

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

<span data-ttu-id="52d92-133">En outre toopoints, GeoJSON prend également en charge LineStrings et des polygones.</span><span class="sxs-lookup"><span data-stu-id="52d92-133">In addition toopoints, GeoJSON also supports LineStrings and Polygons.</span></span> <span data-ttu-id="52d92-134">**LineStrings** représentent une série de deux ou plusieurs points dans l’espace et hello des segments de ligne qui les connectent.</span><span class="sxs-lookup"><span data-stu-id="52d92-134">**LineStrings** represent a series of two or more points in space and hello line segments that connect them.</span></span> <span data-ttu-id="52d92-135">Dans les données géographiques, LineStrings sont couramment utilisés toorepresent autoroutes ou cours d’eau.</span><span class="sxs-lookup"><span data-stu-id="52d92-135">In geospatial data, LineStrings are commonly used toorepresent highways or rivers.</span></span> <span data-ttu-id="52d92-136">Un **polygone** est une limite de points reliés qui constitue une LineString fermée.</span><span class="sxs-lookup"><span data-stu-id="52d92-136">A **Polygon** is a boundary of connected points that forms a closed LineString.</span></span> <span data-ttu-id="52d92-137">Polygones sont formations naturel de toorepresent couramment utilisés comme des lacs ou politiques juridictions telles que les États et villes.</span><span class="sxs-lookup"><span data-stu-id="52d92-137">Polygons are commonly used toorepresent natural formations like lakes or political jurisdictions like cities and states.</span></span> <span data-ttu-id="52d92-138">Voici un exemple de polygone dans Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="52d92-138">Here's an example of a Polygon in Azure Cosmos DB.</span></span> 

<span data-ttu-id="52d92-139">**Polygones dans GeoJSON**</span><span class="sxs-lookup"><span data-stu-id="52d92-139">**Polygons in GeoJSON**</span></span>

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
> <span data-ttu-id="52d92-140">Hello GeoJSON spécification requiert que pour les polygones valides, hello dernière paire de coordonnées fourni doit être identique à hello comme hello, toocreate tout d’abord, une forme fermée.</span><span class="sxs-lookup"><span data-stu-id="52d92-140">hello GeoJSON specification requires that for valid Polygons, hello last coordinate pair provided should be hello same as hello first, toocreate a closed shape.</span></span>
> 
> <span data-ttu-id="52d92-141">Les points dans un polygone doivent être spécifiés dans le sens antihoraire.</span><span class="sxs-lookup"><span data-stu-id="52d92-141">Points within a Polygon must be specified in counter-clockwise order.</span></span> <span data-ttu-id="52d92-142">Un polygone spécifié dans le sens horaire représente inverse hello de région de hello qu’il contient.</span><span class="sxs-lookup"><span data-stu-id="52d92-142">A Polygon specified in clockwise order represents hello inverse of hello region within it.</span></span>
> 
> 

<span data-ttu-id="52d92-143">Dans Ajout tooPoint, LineString et polygone, GeoJSON spécifie également pour la représentation sous forme de hello toogroup plusieurs emplacements géographiques, ainsi que comme des propriétés arbitraires tooassociate avec un emplacement géographique qu’un **fonctionnalité**.</span><span class="sxs-lookup"><span data-stu-id="52d92-143">In addition tooPoint, LineString and Polygon, GeoJSON also specifies hello representation for how toogroup multiple geospatial locations, as well as how tooassociate arbitrary properties with geolocation as a **Feature**.</span></span> <span data-ttu-id="52d92-144">Étant donné que ces objets sont des JSON valides, ils peuvent tous être stockés et traités dans Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="52d92-144">Since these objects are valid JSON, they can all be stored and processed in Azure Cosmos DB.</span></span> <span data-ttu-id="52d92-145">Cependant, Azure Cosmos DB prend uniquement en charge l’indexation automatique des points.</span><span class="sxs-lookup"><span data-stu-id="52d92-145">However Azure Cosmos DB only supports automatic indexing of points.</span></span>

### <a name="coordinate-reference-systems"></a><span data-ttu-id="52d92-146">Coordination des systèmes de référence</span><span class="sxs-lookup"><span data-stu-id="52d92-146">Coordinate reference systems</span></span>
<span data-ttu-id="52d92-147">Forme hello de terre de hello étant anormale, les coordonnées des données géospatiales est représenté dans de nombreux systèmes de coordonnées de référence (DM), chacun ayant leurs propres images de référence et les unités de mesure.</span><span class="sxs-lookup"><span data-stu-id="52d92-147">Since hello shape of hello earth is irregular, coordinates of geospatial data is represented in many coordinate reference systems (CRS), each with their own frames of reference and units of measurement.</span></span> <span data-ttu-id="52d92-148">Par exemple, hello « Grille National de Grande-Bretagne » est un système de référence est très précis pour hello Royaume-Uni, mais pas à l’extérieur.</span><span class="sxs-lookup"><span data-stu-id="52d92-148">For example, hello "National Grid of Britain" is a reference system is very accurate for hello United Kingdom, but not outside it.</span></span> 

<span data-ttu-id="52d92-149">Hello CRS les plus populaires en cours d’utilisation est aujourd'hui hello World Geodetic System [-WGS 84](http://earth-info.nga.mil/GandG/wgs84/).</span><span class="sxs-lookup"><span data-stu-id="52d92-149">hello most popular CRS in use today is hello World Geodetic System  [WGS-84](http://earth-info.nga.mil/GandG/wgs84/).</span></span> <span data-ttu-id="52d92-150">Les périphériques GPS et de nombreux services de mappage, notamment les API Bing Maps et Google Maps, utilisent le WGS-84.</span><span class="sxs-lookup"><span data-stu-id="52d92-150">GPS devices, and many mapping services including Google Maps and Bing Maps APIs use WGS-84.</span></span> <span data-ttu-id="52d92-151">Base de données Azure Cosmos prend en charge l’indexation et l’interrogation des données géospatiales à l’aide de hello-WGS 84 CRS.</span><span class="sxs-lookup"><span data-stu-id="52d92-151">Azure Cosmos DB supports indexing and querying of geospatial data using hello WGS-84 CRS only.</span></span> 

## <a name="creating-documents-with-spatial-data"></a><span data-ttu-id="52d92-152">Création de documents avec les données spatiales</span><span class="sxs-lookup"><span data-stu-id="52d92-152">Creating documents with spatial data</span></span>
<span data-ttu-id="52d92-153">Lorsque vous créez des documents qui contiennent des valeurs GeoJSON, ils sont automatiquement indexés avec un index spatial dans la stratégie d’indexation conformément aux toohello de collection de hello.</span><span class="sxs-lookup"><span data-stu-id="52d92-153">When you create documents that contain GeoJSON values, they are automatically indexed with a spatial index in accordance toohello indexing policy of hello collection.</span></span> <span data-ttu-id="52d92-154">Si vous travaillez avec un Kit de développement logiciel (SDK) Azure Cosmos DB dans un langage saisi dynamiquement comme Python ou Node.js, vous devez créer un GeoJSON valide.</span><span class="sxs-lookup"><span data-stu-id="52d92-154">If you're working with an Azure Cosmos DB SDK in a dynamically typed language like Python or Node.js, you must create valid GeoJSON.</span></span>

<span data-ttu-id="52d92-155">**Création d’un document avec les données géographiques dans Node.js**</span><span class="sxs-lookup"><span data-stu-id="52d92-155">**Create Document with Geospatial data in Node.js**</span></span>

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

<span data-ttu-id="52d92-156">Si vous travaillez avec hello APIs DocumentDB, vous pouvez utiliser hello `Point` et `Polygon` classes hello `Microsoft.Azure.Documents.Spatial` des informations d’emplacement de tooembed d’espace de noms dans les objets de votre application.</span><span class="sxs-lookup"><span data-stu-id="52d92-156">If you're working with hello DocumentDB APIs, you can use hello `Point` and `Polygon` classes within hello `Microsoft.Azure.Documents.Spatial` namespace tooembed location information within your application objects.</span></span> <span data-ttu-id="52d92-157">Ces classes permettent de simplifier la sérialisation de hello et la désérialisation des données spatiales dans GeoJSON.</span><span class="sxs-lookup"><span data-stu-id="52d92-157">These classes help simplify hello serialization and deserialization of spatial data into GeoJSON.</span></span>

<span data-ttu-id="52d92-158">**Création d’un document avec les données géographiques dans .NET**</span><span class="sxs-lookup"><span data-stu-id="52d92-158">**Create Document with Geospatial data in .NET**</span></span>

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

<span data-ttu-id="52d92-159">Si vous n’avez pas les informations de latitude et longitude hello, mais avez des adresses physiques de hello ou nom de l’emplacement comme ville ou pays, vous pouvez rechercher les coordonnées réel hello à l’aide d’un service de géocodage comme Services REST Bing Maps.</span><span class="sxs-lookup"><span data-stu-id="52d92-159">If you don't have hello latitude and longitude information, but have hello physical addresses or location name like city or country, you can look up hello actual coordinates by using a geocoding service like Bing Maps REST Services.</span></span> <span data-ttu-id="52d92-160">En savoir plus sur le géocodage de Bing Maps [ici](https://msdn.microsoft.com/library/ff701713.aspx).</span><span class="sxs-lookup"><span data-stu-id="52d92-160">Learn more about Bing Maps geocoding [here](https://msdn.microsoft.com/library/ff701713.aspx).</span></span>

## <a name="querying-spatial-types"></a><span data-ttu-id="52d92-161">Interrogation des types spatiaux</span><span class="sxs-lookup"><span data-stu-id="52d92-161">Querying spatial types</span></span>
<span data-ttu-id="52d92-162">Maintenant que nous avons observez comment les données géospatiales tooinsert, examinons la tooquery ces données à l’aide de la base de données Azure Cosmos à l’aide de SQL et LINQ.</span><span class="sxs-lookup"><span data-stu-id="52d92-162">Now that we've taken a look at how tooinsert geospatial data, let's take a look at how tooquery this data using Azure Cosmos DB using SQL and LINQ.</span></span>

### <a name="spatial-sql-built-in-functions"></a><span data-ttu-id="52d92-163">Fonctions spatiales SQL intégrées</span><span class="sxs-lookup"><span data-stu-id="52d92-163">Spatial SQL built-in functions</span></span>
<span data-ttu-id="52d92-164">Base de données Azure Cosmos prend en charge hello suivant des fonctions intégrées d’Open Geospatial Consortium (OGC) pour l’interrogation de géographiques.</span><span class="sxs-lookup"><span data-stu-id="52d92-164">Azure Cosmos DB supports hello following Open Geospatial Consortium (OGC) built-in functions for geospatial querying.</span></span> <span data-ttu-id="52d92-165">Pour plus d’informations sur l’ensemble complet de hello de fonctions intégrées dans hello langage SQL, consultez trop[base de données de requête Azure Cosmos](documentdb-sql-query.md).</span><span class="sxs-lookup"><span data-stu-id="52d92-165">For more details on hello complete set of built-in functions in hello SQL language, please refer too[Query Azure Cosmos DB](documentdb-sql-query.md).</span></span>

<table>
<tr>
  <td><span data-ttu-id="52d92-166"><strong>Utilisation</strong></span><span class="sxs-lookup"><span data-stu-id="52d92-166"><strong>Usage</strong></span></span></td>
  <td><span data-ttu-id="52d92-167"><strong>Description</strong></span><span class="sxs-lookup"><span data-stu-id="52d92-167"><strong>Description</strong></span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="52d92-168">ST_DISTANCE (spatial_expr, spatial_expr)</span><span class="sxs-lookup"><span data-stu-id="52d92-168">ST_DISTANCE (spatial_expr, spatial_expr)</span></span></td>
  <td><span data-ttu-id="52d92-169">Retourne la distance hello entre les expressions LineString, Polygon ou GeoJSON Point hello deux.</span><span class="sxs-lookup"><span data-stu-id="52d92-169">Returns hello distance between hello two GeoJSON Point, Polygon, or LineString expressions.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="52d92-170">ST_WITHIN (spatial_expr, spatial_expr)</span><span class="sxs-lookup"><span data-stu-id="52d92-170">ST_WITHIN (spatial_expr, spatial_expr)</span></span></td>
  <td><span data-ttu-id="52d92-171">Retourne une expression booléenne indiquant si hello premier GeoJSON objet (Point, polygone ou LineString) se trouve dans hello deuxième GeoJSON objet (Point, polygone ou LineString).</span><span class="sxs-lookup"><span data-stu-id="52d92-171">Returns a Boolean expression indicating whether hello first GeoJSON object (Point, Polygon, or LineString) is within hello second GeoJSON object (Point, Polygon, or LineString).</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="52d92-172">ST_INTERSECTS (spatial_expr, spatial_expr)</span><span class="sxs-lookup"><span data-stu-id="52d92-172">ST_INTERSECTS (spatial_expr, spatial_expr)</span></span></td>
  <td><span data-ttu-id="52d92-173">Retourne une expression booléenne indiquant si hello deux GeoJSON objets spécifiés (Point, polygone ou LineString) se croisent.</span><span class="sxs-lookup"><span data-stu-id="52d92-173">Returns a Boolean expression indicating whether hello two specified GeoJSON objects (Point, Polygon, or LineString) intersect.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="52d92-174">ST_ISVALID</span><span class="sxs-lookup"><span data-stu-id="52d92-174">ST_ISVALID</span></span></td>
  <td><span data-ttu-id="52d92-175">Retourne une valeur booléenne indiquant si hello spécifiée expression LineString, Polygon ou GeoJSON Point n’est valide.</span><span class="sxs-lookup"><span data-stu-id="52d92-175">Returns a Boolean value indicating whether hello specified GeoJSON Point, Polygon, or LineString expression is valid.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="52d92-176">ST_ISVALIDDETAILED</span><span class="sxs-lookup"><span data-stu-id="52d92-176">ST_ISVALIDDETAILED</span></span></td>
  <td><span data-ttu-id="52d92-177">Retourne une valeur JSON contenant une valeur booléenne si hello de l’expression LineString, Polygon ou GeoJSON Point spécifiée est valide et si elle est non valide, en outre hello motif en tant que valeur de chaîne.</span><span class="sxs-lookup"><span data-stu-id="52d92-177">Returns a JSON value containing a Boolean value if hello specified GeoJSON Point, Polygon, or LineString expression is valid, and if invalid, additionally hello reason as a string value.</span></span></td>
</tr>
</table>

<span data-ttu-id="52d92-178">Les fonctions spatiale peuvent être des requêtes de proximité tooperform utilisé par rapport aux données spatiales.</span><span class="sxs-lookup"><span data-stu-id="52d92-178">Spatial functions can be used tooperform proximity queries against spatial data.</span></span> <span data-ttu-id="52d92-179">Par exemple, voici une requête qui retourne la que famille de tous les documents qu’est 30 kilomètres de hello emplacement spécifié à l’aide de fonctions intégrées de ST_DISTANCE hello.</span><span class="sxs-lookup"><span data-stu-id="52d92-179">For example, here's a query that returns all family documents that are within 30 km of hello specified location using hello ST_DISTANCE built-in function.</span></span> 

<span data-ttu-id="52d92-180">**Requête**</span><span class="sxs-lookup"><span data-stu-id="52d92-180">**Query**</span></span>

    SELECT f.id 
    FROM Families f 
    WHERE ST_DISTANCE(f.location, {'type': 'Point', 'coordinates':[31.9, -4.8]}) < 30000

<span data-ttu-id="52d92-181">**Résultats**</span><span class="sxs-lookup"><span data-stu-id="52d92-181">**Results**</span></span>

    [{
      "id": "WakefieldFamily"
    }]

<span data-ttu-id="52d92-182">Si vous incluez l’indexation spatiale dans votre stratégie d’indexation, puis « requêtes à distance » seront pris en charge efficacement par le biais des index de hello.</span><span class="sxs-lookup"><span data-stu-id="52d92-182">If you include spatial indexing in your indexing policy, then "distance queries" will be served efficiently through hello index.</span></span> <span data-ttu-id="52d92-183">Pour plus d’informations sur l’indexation spatiale, consultez la section hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="52d92-183">For more details on spatial indexing, please see hello section below.</span></span> <span data-ttu-id="52d92-184">Si vous n’avez pas un spatial index pour hello spécifié des chemins d’accès, vous pouvez encore effectuer des requêtes spatiales en spécifiant `x-ms-documentdb-query-enable-scan` en-tête de demande avec la valeur de hello défini trop « true ».</span><span class="sxs-lookup"><span data-stu-id="52d92-184">If you don't have a spatial index for hello specified paths, you can still perform spatial queries by specifying `x-ms-documentdb-query-enable-scan` request header with hello value set too"true".</span></span> <span data-ttu-id="52d92-185">Dans .NET, cela est possible en hello en passant facultatif **FeedOptions** tooqueries argument avec [EnableScanInQuery](https://msdn.microsoft.com/library/microsoft.azure.documents.client.feedoptions.enablescaninquery.aspx#P:Microsoft.Azure.Documents.Client.FeedOptions.EnableScanInQuery) définir tootrue.</span><span class="sxs-lookup"><span data-stu-id="52d92-185">In .NET, this can be done by passing hello optional **FeedOptions** argument tooqueries with [EnableScanInQuery](https://msdn.microsoft.com/library/microsoft.azure.documents.client.feedoptions.enablescaninquery.aspx#P:Microsoft.Azure.Documents.Client.FeedOptions.EnableScanInQuery) set tootrue.</span></span> 

<span data-ttu-id="52d92-186">ST_WITHIN peut être utilisé toocheck si un point se trouve dans un polygone.</span><span class="sxs-lookup"><span data-stu-id="52d92-186">ST_WITHIN can be used toocheck if a point lies within a Polygon.</span></span> <span data-ttu-id="52d92-187">En règle générale polygones sont des limites de toorepresent utilisés comme codes postaux, les frontières de l’état ou les formations naturelles.</span><span class="sxs-lookup"><span data-stu-id="52d92-187">Commonly Polygons are used toorepresent boundaries like zip codes, state boundaries, or natural formations.</span></span> <span data-ttu-id="52d92-188">À nouveau si vous incluez l’indexation spatiale dans votre stratégie d’indexation, puis requêtes « dans » seront pris en charge efficacement par le biais des index de hello.</span><span class="sxs-lookup"><span data-stu-id="52d92-188">Again if you include spatial indexing in your indexing policy, then "within" queries will be served efficiently through hello index.</span></span> 

<span data-ttu-id="52d92-189">Arguments de polygone dans ST_WITHIN peuvent contenir uniquement un anneau unique, c'est-à-dire hello polygones ne doit pas contenir de trous.</span><span class="sxs-lookup"><span data-stu-id="52d92-189">Polygon arguments in ST_WITHIN can contain only a single ring, i.e. hello Polygons must not contain holes in them.</span></span> 

<span data-ttu-id="52d92-190">**Requête**</span><span class="sxs-lookup"><span data-stu-id="52d92-190">**Query**</span></span>

    SELECT * 
    FROM Families f 
    WHERE ST_WITHIN(f.location, {
        'type':'Polygon', 
        'coordinates': [[[31.8, -5], [32, -5], [32, -4.7], [31.8, -4.7], [31.8, -5]]]
    })

<span data-ttu-id="52d92-191">**Résultats**</span><span class="sxs-lookup"><span data-stu-id="52d92-191">**Results**</span></span>

    [{
      "id": "WakefieldFamily",
    }]

> [!NOTE]
> <span data-ttu-id="52d92-192">Types toohow incompatible similaires fonctionne dans la requête de base de données Azure Cosmos, si la valeur hello emplacement spécifié dans soit argument est mal formé ou non valide, puis il évalue trop**non défini** et hello évaluée document toobe ignorées à partir de hello résultats de la requête.</span><span class="sxs-lookup"><span data-stu-id="52d92-192">Similar toohow mismatched types works in Azure Cosmos DB query, if hello location value specified in either argument is malformed or invalid, then it will evaluate too**undefined** and hello evaluated document toobe skipped from hello query results.</span></span> <span data-ttu-id="52d92-193">Si votre requête ne retourne aucun résultat, exécutez toodebug ST_ISVALIDDETAILED pourquoi type spatail de hello n’est pas valide.</span><span class="sxs-lookup"><span data-stu-id="52d92-193">If your query returns no results, run ST_ISVALIDDETAILED toodebug why hello spatail type is invalid.</span></span>     
> 
> 

<span data-ttu-id="52d92-194">Base de données Azure Cosmos prend également en charge les interrogations inverse, par exemple, vous pouvez indexer des polygones ou lignes de base de données Azure Cosmos, puis rechercher des zones hello contenant un point spécifié.</span><span class="sxs-lookup"><span data-stu-id="52d92-194">Azure Cosmos DB also supports performing inverse queries, i.e. you can index Polygons or lines in Azure Cosmos DB, then query for hello areas that contain a specified point.</span></span> <span data-ttu-id="52d92-195">Ce modèle est utilisé communément dans logistique tooidentify par exemple, quand un camion entre ou quitte une région.</span><span class="sxs-lookup"><span data-stu-id="52d92-195">This pattern is commonly used in logistics tooidentify e.g. when a truck enters or leaves a designated area.</span></span> 

<span data-ttu-id="52d92-196">**Requête**</span><span class="sxs-lookup"><span data-stu-id="52d92-196">**Query**</span></span>

    SELECT * 
    FROM Areas a 
    WHERE ST_WITHIN({'type': 'Point', 'coordinates':[31.9, -4.8]}, a.location)


<span data-ttu-id="52d92-197">**Résultats**</span><span class="sxs-lookup"><span data-stu-id="52d92-197">**Results**</span></span>

    [{
      "id": "MyDesignatedLocation",
      "location": {
        "type":"Polygon", 
        "coordinates": [[[31.8, -5], [32, -5], [32, -4.7], [31.8, -4.7], [31.8, -5]]]
      }
    }]

<span data-ttu-id="52d92-198">ST_ISVALID et ST_ISVALIDDETAILED peuvent être utilisé toocheck si un objet spatial est valide.</span><span class="sxs-lookup"><span data-stu-id="52d92-198">ST_ISVALID and ST_ISVALIDDETAILED can be used toocheck if a spatial object is valid.</span></span> <span data-ttu-id="52d92-199">Par exemple, hello suivant de requête vérifie la validité de hello d’un point avec une valeur hors limites latitude (-132.8).</span><span class="sxs-lookup"><span data-stu-id="52d92-199">For example, hello following query checks hello validity of a point with an out of range latitude value (-132.8).</span></span> <span data-ttu-id="52d92-200">ST_ISVALID retourne simplement une valeur booléenne et ST_ISVALIDDETAILED renvoie hello booléenne et une chaîne contenant la raison hello pourquoi il est considéré comme non valide.</span><span class="sxs-lookup"><span data-stu-id="52d92-200">ST_ISVALID returns just a Boolean value, and ST_ISVALIDDETAILED returns hello Boolean and a string containing hello reason why it is considered invalid.</span></span>

<span data-ttu-id="52d92-201">** Requête **</span><span class="sxs-lookup"><span data-stu-id="52d92-201">** Query **</span></span>

    SELECT ST_ISVALID({ "type": "Point", "coordinates": [31.9, -132.8] })

<span data-ttu-id="52d92-202">**Résultats**</span><span class="sxs-lookup"><span data-stu-id="52d92-202">**Results**</span></span>

    [{
      "$1": false
    }]

<span data-ttu-id="52d92-203">Ces fonctions peuvent également être utilisés toovalidate polygones.</span><span class="sxs-lookup"><span data-stu-id="52d92-203">These functions can also be used toovalidate Polygons.</span></span> <span data-ttu-id="52d92-204">Par exemple, nous utilisons ici ST_ISVALIDDETAILED toovalidate un polygone n’est pas fermé.</span><span class="sxs-lookup"><span data-stu-id="52d92-204">For example, here we use ST_ISVALIDDETAILED toovalidate a Polygon that is not closed.</span></span> 

<span data-ttu-id="52d92-205">**Requête**</span><span class="sxs-lookup"><span data-stu-id="52d92-205">**Query**</span></span>

    SELECT ST_ISVALIDDETAILED({ "type": "Polygon", "coordinates": [[ 
        [ 31.8, -5 ], [ 31.8, -4.7 ], [ 32, -4.7 ], [ 32, -5 ] 
        ]]})

<span data-ttu-id="52d92-206">**Résultats**</span><span class="sxs-lookup"><span data-stu-id="52d92-206">**Results**</span></span>

    [{
       "$1": { 
            "valid": false, 
            "reason": "hello Polygon input is not valid because hello start and end points of hello ring number 1 are not hello same. Each ring of a Polygon must have hello same start and end points." 
          }
    }]

### <a name="linq-querying-in-hello-net-sdk"></a><span data-ttu-id="52d92-207">L’interrogation LINQ Bonjour .NET SDK</span><span class="sxs-lookup"><span data-stu-id="52d92-207">LINQ Querying in hello .NET SDK</span></span>
<span data-ttu-id="52d92-208">Hello DocumentDB .NET SDK également les fournisseurs de stub méthodes `Distance()` et `Within()` pour une utilisation dans des expressions LINQ.</span><span class="sxs-lookup"><span data-stu-id="52d92-208">hello DocumentDB .NET SDK also providers stub methods `Distance()` and `Within()` for use within LINQ expressions.</span></span> <span data-ttu-id="52d92-209">fournisseur de DocumentDB LINQ Hello traduit ces méthode appels toohello équivalent SQL appels de fonction intégrée (ST_DISTANCE et ST_WITHIN respectivement).</span><span class="sxs-lookup"><span data-stu-id="52d92-209">hello DocumentDB LINQ provider translates these method calls toohello equivalent SQL built-in function calls (ST_DISTANCE and ST_WITHIN respectively).</span></span> 

<span data-ttu-id="52d92-210">Voici un exemple d’une requête LINQ qui recherche tous les documents dans la collection de base de données Azure Cosmos hello dont la valeur « location » est dans un rayon de 30 kilomètres de hello spécifiée point à l’aide de LINQ.</span><span class="sxs-lookup"><span data-stu-id="52d92-210">Here's an example of a LINQ query that finds all documents in hello Azure Cosmos DB collection whose "location" value is within a radius of 30km of hello specified point using LINQ.</span></span>

<span data-ttu-id="52d92-211">**Requête LINQ de distance**</span><span class="sxs-lookup"><span data-stu-id="52d92-211">**LINQ query for Distance**</span></span>

    foreach (UserProfile user in client.CreateDocumentQuery<UserProfile>(UriFactory.CreateDocumentCollectionUri("db", "profiles"))
        .Where(u => u.ProfileType == "Public" && a.Location.Distance(new Point(32.33, -4.66)) < 30000))
    {
        Console.WriteLine("\t" + user);
    }

<span data-ttu-id="52d92-212">De même, voici une requête pour rechercher tous les documents hello dont « location » est dans hello spécifié boîte/polygone.</span><span class="sxs-lookup"><span data-stu-id="52d92-212">Similarly, here's a query for finding all hello documents whose "location" is within hello specified box/Polygon.</span></span> 

<span data-ttu-id="52d92-213">**Requête LINQ within**</span><span class="sxs-lookup"><span data-stu-id="52d92-213">**LINQ query for Within**</span></span>

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


<span data-ttu-id="52d92-214">Maintenant que nous avons observez comment les documents de tooquery à l’aide de LINQ et SQL, examinons la tooconfigure base de données Azure Cosmos pour l’indexation spatiale.</span><span class="sxs-lookup"><span data-stu-id="52d92-214">Now that we've taken a look at how tooquery documents using LINQ and SQL, let's take a look at how tooconfigure Azure Cosmos DB for spatial indexing.</span></span>

## <a name="indexing"></a><span data-ttu-id="52d92-215">Indexation</span><span class="sxs-lookup"><span data-stu-id="52d92-215">Indexing</span></span>
<span data-ttu-id="52d92-216">Comme décrit dans hello [schéma agnostique en termes d’indexation avec la base de données Azure Cosmos](http://www.vldb.org/pvldb/vol8/p1668-shukla.pdf) papier, nous avons conçu toobe de moteur de base de données Azure Cosmos DB réellement indépendant du schéma et de la première classe prennent en charge de JSON.</span><span class="sxs-lookup"><span data-stu-id="52d92-216">As we described in hello [Schema Agnostic Indexing with Azure Cosmos DB](http://www.vldb.org/pvldb/vol8/p1668-shukla.pdf) paper, we designed Azure Cosmos DB’s database engine toobe truly schema agnostic and provide first class support for JSON.</span></span> <span data-ttu-id="52d92-217">en mode natif, le moteur de base de données d’écriture optimisé Hello de base de données Azure Cosmos comprend des données spatiales (points, lignes et les polygones) représentées dans la norme de GeoJSON hello.</span><span class="sxs-lookup"><span data-stu-id="52d92-217">hello write optimized database engine of Azure Cosmos DB natively understands spatial data (points, Polygons and lines) represented in hello GeoJSON standard.</span></span>

<span data-ttu-id="52d92-218">En bref, géométrie de hello est projetée à partir des coordonnées géodésiques sur un plan 2D puis divisée progressivement les cellules à l’aide un **quadtree**.</span><span class="sxs-lookup"><span data-stu-id="52d92-218">In a nutshell, hello geometry is projected from geodetic coordinates onto a 2D plane then divided progressively into cells using a **quadtree**.</span></span> <span data-ttu-id="52d92-219">Ces cellules sont mappés too1D basés sur l’emplacement de hello de cellule hello dans un **courbe de remplissage d’espace de Hilbert**, qui permet de préserver la localité de points.</span><span class="sxs-lookup"><span data-stu-id="52d92-219">These cells are mapped too1D based on hello location of hello cell within a **Hilbert space filling curve**, which preserves locality of points.</span></span> <span data-ttu-id="52d92-220">En outre lorsque les données d’emplacement sont indexées, il passe par un processus appelé **pavage**, autrement dit, toutes les cellules de hello qui se croisent à un emplacement sont identifiées et stockées en tant que clés dans l’index de base de données Azure Cosmos hello.</span><span class="sxs-lookup"><span data-stu-id="52d92-220">Additionally when location data is indexed, it goes through a process known as **tessellation**, i.e. all hello cells that intersect a location are identified and stored as keys in hello Azure Cosmos DB index.</span></span> <span data-ttu-id="52d92-221">Au moment de la requête, arguments telles que les points et des polygones sont également fractionné tooextract hello des plages d’ID de cellule appropriée, puis utilisé tooretrieve des données à partir de l’index de hello.</span><span class="sxs-lookup"><span data-stu-id="52d92-221">At query time, arguments like points and Polygons are also tessellated tooextract hello relevant cell ID ranges, then used tooretrieve data from hello index.</span></span>

<span data-ttu-id="52d92-222">Si vous spécifiez une stratégie d’indexation qui inclut un index spatial pour / * (tous les chemins d’accès), tous les points trouvés au sein de la collection de hello sont indexés pour des requêtes spatiales efficace (ST_WITHIN et ST_DISTANCE).</span><span class="sxs-lookup"><span data-stu-id="52d92-222">If you specify an indexing policy that includes spatial index for /* (all paths), then all points found within hello collection are indexed for efficient spatial queries (ST_WITHIN and ST_DISTANCE).</span></span> <span data-ttu-id="52d92-223">Les index spatiaux n'ont pas une valeur de précision et utilisent toujours une valeur de précision par défaut.</span><span class="sxs-lookup"><span data-stu-id="52d92-223">Spatial indexes do not have a precision value, and always use a default precision value.</span></span>

> [!NOTE]
> <span data-ttu-id="52d92-224">Azure Cosmos DB prend en charge l’indexation automatique des points, polygones et lineStrings.</span><span class="sxs-lookup"><span data-stu-id="52d92-224">Azure Cosmos DB supports automatic indexing of Points, Polygons, and LineStrings</span></span>
> 
> 

<span data-ttu-id="52d92-225">Hello extrait de code JSON suivant illustre une stratégie d’indexation avec indexation spatiale activé, autrement dit, l’index n’importe quel point GeoJSON trouvé au sein de documents pour les requêtes spatiales.</span><span class="sxs-lookup"><span data-stu-id="52d92-225">hello following JSON snippet shows an indexing policy with spatial indexing enabled, i.e. index any GeoJSON point found within documents for spatial querying.</span></span> <span data-ttu-id="52d92-226">Si vous modifiez hello l’indexation de stratégie à l’aide de hello portail Azure, vous pouvez spécifier hello suivant JSON pour l’indexation tooenable stratégie spatiale de l’indexation sur votre collection.</span><span class="sxs-lookup"><span data-stu-id="52d92-226">If you are modifying hello indexing policy using hello Azure Portal, you can specify hello following JSON for indexing policy tooenable spatial indexing on your collection.</span></span>

<span data-ttu-id="52d92-227">**Stratégie d’indexation de collection JSON avec Spatial activé pour les points et les polygones**</span><span class="sxs-lookup"><span data-stu-id="52d92-227">**Collection Indexing Policy JSON with Spatial enabled for points and Polygons**</span></span>

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

<span data-ttu-id="52d92-228">Voici un extrait de code dans .NET qui montre comment toocreate une collection de l’indexation spatiale activé pour tous les chemins d’accès contenant des points.</span><span class="sxs-lookup"><span data-stu-id="52d92-228">Here's a code snippet in .NET that shows how toocreate a collection with spatial indexing turned on for all paths containing points.</span></span> 

<span data-ttu-id="52d92-229">**Création d’une collection avec l'indexation spatiale**</span><span class="sxs-lookup"><span data-stu-id="52d92-229">**Create a collection with spatial indexing**</span></span>

    DocumentCollection spatialData = new DocumentCollection()
    spatialData.IndexingPolicy = new IndexingPolicy(new SpatialIndex(DataType.Point)); //override tooturn spatial on by default
    collection = await client.CreateDocumentCollectionAsync(UriFactory.CreateDatabaseUri("db"), spatialData);

<span data-ttu-id="52d92-230">Et Voici comment vous pouvez modifier un existant collection tootake des avantages de l’indexation spatiale sur tous les points qui sont stockés dans les documents.</span><span class="sxs-lookup"><span data-stu-id="52d92-230">And here's how you can modify an existing collection tootake advantage of spatial indexing over any points that are stored within documents.</span></span>

<span data-ttu-id="52d92-231">**Modification d’une collection existante avec l'indexation spatiale**</span><span class="sxs-lookup"><span data-stu-id="52d92-231">**Modify an existing collection with spatial indexing**</span></span>

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
> <span data-ttu-id="52d92-232">Si l’emplacement hello valeur GeoJSON dans le document de hello est incorrect ou non valide, puis il ne sera pas été indexé pour les requêtes spatiales.</span><span class="sxs-lookup"><span data-stu-id="52d92-232">If hello location GeoJSON value within hello document is malformed or invalid, then it will not get indexed for spatial querying.</span></span> <span data-ttu-id="52d92-233">Vous pouvez valider les valeurs d'emplacement à l'aide de ST_ISVALID et ST_ISVALIDDETAILED.</span><span class="sxs-lookup"><span data-stu-id="52d92-233">You can validate location values using ST_ISVALID and ST_ISVALIDDETAILED.</span></span>
> 
> <span data-ttu-id="52d92-234">Si la définition de votre collection contient une clé de partition, la progression de la transformation d’indexation n’est pas signalée.</span><span class="sxs-lookup"><span data-stu-id="52d92-234">If your collection definition includes a partition key, indexing transformation progress is not reported.</span></span> 
> 
> 

## <a name="next-steps"></a><span data-ttu-id="52d92-235">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="52d92-235">Next steps</span></span>
<span data-ttu-id="52d92-236">Maintenant que vous avez appris sur comment tooget démarrer avec prise en charge géographique dans la base de données Azure Cosmos, vous pouvez :</span><span class="sxs-lookup"><span data-stu-id="52d92-236">Now that you've learnt about how tooget started with geospatial support in Azure Cosmos DB, you can:</span></span>

* <span data-ttu-id="52d92-237">Démarrer le codage avec hello [exemples de code Geospatial .NET sur GitHub](https://github.com/Azure/azure-documentdb-dotnet/blob/fcf23d134fc5019397dcf7ab97d8d6456cd94820/samples/code-samples/Geospatial/Program.cs)</span><span class="sxs-lookup"><span data-stu-id="52d92-237">Start coding with hello [Geospatial .NET code samples on GitHub](https://github.com/Azure/azure-documentdb-dotnet/blob/fcf23d134fc5019397dcf7ab97d8d6456cd94820/samples/code-samples/Geospatial/Program.cs)</span></span>
* <span data-ttu-id="52d92-238">Découvrir avec geospatial interrogeant au hello [Azure Cosmos DB Query Playground](http://www.documentdb.com/sql/demo#geospatial)</span><span class="sxs-lookup"><span data-stu-id="52d92-238">Get hands on with geospatial querying at hello [Azure Cosmos DB Query Playground](http://www.documentdb.com/sql/demo#geospatial)</span></span>
* <span data-ttu-id="52d92-239">En savoir plus sur les [requêtes Azure Cosmos DB](documentdb-sql-query.md)</span><span class="sxs-lookup"><span data-stu-id="52d92-239">Learn more about [Azure Cosmos DB Query](documentdb-sql-query.md)</span></span>
* <span data-ttu-id="52d92-240">En savoir plus sur les [stratégies d’indexation Azure Cosmos DB](indexing-policies.md)</span><span class="sxs-lookup"><span data-stu-id="52d92-240">Learn more about [Azure Cosmos DB Indexing Policies](indexing-policies.md)</span></span>

