---
title: "Utilisation de données géospatiales dans Azure Cosmos DB | Microsoft Docs"
description: "Comprendre comment créer, indexer et interroger les objets spatiaux avec Azure Cosmos DB et l’API DocumentDB."
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
ms.openlocfilehash: d5785c81fb597e7d30eb7d3a880e7194d8358ed5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="working-with-geospatial-and-geojson-location-data-in-azure-cosmos-db"></a><span data-ttu-id="ec5f6-103">Utilisation de données d’emplacement géospatiales et GeoJSON dans Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="ec5f6-103">Working with geospatial and GeoJSON location data in Azure Cosmos DB</span></span>
<span data-ttu-id="ec5f6-104">Cet article est une introduction aux fonctionnalités géospatiales dans [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="ec5f6-104">This article is an introduction to the geospatial functionality in [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span></span> <span data-ttu-id="ec5f6-105">Après avoir lu cet article, vous serez en mesure de répondre aux questions suivantes :</span><span class="sxs-lookup"><span data-stu-id="ec5f6-105">After reading this, you will be able to answer the following questions:</span></span>

* <span data-ttu-id="ec5f6-106">Comment puis-je stocker des données spatiales dans Azure Cosmos DB ?</span><span class="sxs-lookup"><span data-stu-id="ec5f6-106">How do I store spatial data in Azure Cosmos DB?</span></span>
* <span data-ttu-id="ec5f6-107">Comment puis-je interroger des données géospaciales dans Azure Cosmos DB dans SQL et LINQ ?</span><span class="sxs-lookup"><span data-stu-id="ec5f6-107">How can I query geospatial data in Azure Cosmos DB in SQL and LINQ?</span></span>
* <span data-ttu-id="ec5f6-108">Comment puis-je activer ou désactiver l’indexation spatiale dans Azure Cosmos DB ?</span><span class="sxs-lookup"><span data-stu-id="ec5f6-108">How do I enable or disable spatial indexing in Azure Cosmos DB?</span></span>

<span data-ttu-id="ec5f6-109">Cet article montre comment utiliser les données spatiales avec l’API DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="ec5f6-109">This article shows how to work with spatial data with the DocumentDB API.</span></span> <span data-ttu-id="ec5f6-110">Consultez ce [projet GitHub](https://github.com/Azure/azure-documentdb-dotnet/blob/master/samples/code-samples/Geospatial/Program.cs) pour obtenir des échantillons de code.</span><span class="sxs-lookup"><span data-stu-id="ec5f6-110">Please see this [GitHub project](https://github.com/Azure/azure-documentdb-dotnet/blob/master/samples/code-samples/Geospatial/Program.cs) for code samples.</span></span>

## <a name="introduction-to-spatial-data"></a><span data-ttu-id="ec5f6-111">Présentation des données spatiales</span><span class="sxs-lookup"><span data-stu-id="ec5f6-111">Introduction to spatial data</span></span>
<span data-ttu-id="ec5f6-112">Les données spatiales décrivent la position et la forme des objets dans l'espace.</span><span class="sxs-lookup"><span data-stu-id="ec5f6-112">Spatial data describes the position and shape of objects in space.</span></span> <span data-ttu-id="ec5f6-113">Dans la plupart des applications, ils correspondent aux objets sur terre, c'est-à-dire aux données géographiques.</span><span class="sxs-lookup"><span data-stu-id="ec5f6-113">In most applications, these correspond to objects on the earth, i.e. geospatial data.</span></span> <span data-ttu-id="ec5f6-114">Les données spatiales peuvent servir à représenter l'emplacement d'une personne, d'un point d'intérêt ou de la limite d'une ville ou un lac.</span><span class="sxs-lookup"><span data-stu-id="ec5f6-114">Spatial data can be used to represent the location of a person, a place of interest, or the boundary of a city, or a lake.</span></span> <span data-ttu-id="ec5f6-115">Les scénarios d'utilisation courants impliquent souvent des requêtes de proximité, comme « rechercher tous les cafés près de mon emplacement actuel ».</span><span class="sxs-lookup"><span data-stu-id="ec5f6-115">Common use cases often involve proximity queries, for e.g., "find all coffee shops near my current location".</span></span> 

### <a name="geojson"></a><span data-ttu-id="ec5f6-116">GeoJSON</span><span class="sxs-lookup"><span data-stu-id="ec5f6-116">GeoJSON</span></span>
<span data-ttu-id="ec5f6-117">Azure Cosmos DB prend en charge l’indexation et l’interrogation des données de point géospatiales représentées à l’aide de la [spécification GeoJSON](https://tools.ietf.org/html/rfc7946).</span><span class="sxs-lookup"><span data-stu-id="ec5f6-117">Azure Cosmos DB supports indexing and querying of geospatial point data that's represented using the [GeoJSON specification](https://tools.ietf.org/html/rfc7946).</span></span> <span data-ttu-id="ec5f6-118">Les structures de données GeoJSON sont toujours des objets JSON valides, afin de pouvoir les stocker et les interroger à l’aide d’Azure Cosmos DB, sans bibliothèques ou outils spécialisés.</span><span class="sxs-lookup"><span data-stu-id="ec5f6-118">GeoJSON data structures are always valid JSON objects, so they can be stored and queried using Azure Cosmos DB without any specialized tools or libraries.</span></span> <span data-ttu-id="ec5f6-119">Les kits de développement logiciel (SDK) Azure Cosmos DB fournissent des classes d’assistance et des méthodes qui facilitent la manipulation des données spatiales.</span><span class="sxs-lookup"><span data-stu-id="ec5f6-119">The Azure Cosmos DB SDKs provide helper classes and methods that make it easy to work with spatial data.</span></span> 

### <a name="points-linestrings-and-polygons"></a><span data-ttu-id="ec5f6-120">Points, LineStrings et polygones</span><span class="sxs-lookup"><span data-stu-id="ec5f6-120">Points, LineStrings and Polygons</span></span>
<span data-ttu-id="ec5f6-121">Un **point** désigne une position unique dans l'espace.</span><span class="sxs-lookup"><span data-stu-id="ec5f6-121">A **Point** denotes a single position in space.</span></span> <span data-ttu-id="ec5f6-122">Dans les données géographiques, un point représente l’emplacement exact, qui peut être une adresse postale d’une épicerie, un kiosque, une voiture ou une ville.</span><span class="sxs-lookup"><span data-stu-id="ec5f6-122">In geospatial data, a Point represents the exact location, which could be a street address of a grocery store, a kiosk, an automobile or a city.</span></span>  <span data-ttu-id="ec5f6-123">Un point est représenté dans GeoJSON (et Azure Cosmos DB) à l’aide de sa paire de coordonnées ou de longitude et latitude.</span><span class="sxs-lookup"><span data-stu-id="ec5f6-123">A point is represented in GeoJSON (and Azure Cosmos DB) using its coordinate pair or longitude and latitude.</span></span> <span data-ttu-id="ec5f6-124">Voici un exemple JSON pour un point.</span><span class="sxs-lookup"><span data-stu-id="ec5f6-124">Here's an example JSON for a point.</span></span>

<span data-ttu-id="ec5f6-125">**Points dans Azure Cosmos DB**</span><span class="sxs-lookup"><span data-stu-id="ec5f6-125">**Points in Azure Cosmos DB**</span></span>

```json
{
    "type":"Point",
    "coordinates":[ 31.9, -4.8 ]
}
```

> [!NOTE]
> <span data-ttu-id="ec5f6-126">La spécification GeoJSON spécifie la longitude d’abord, puis la latitude.</span><span class="sxs-lookup"><span data-stu-id="ec5f6-126">The GeoJSON specification specifies longitude first and latitude second.</span></span> <span data-ttu-id="ec5f6-127">Comme dans d'autres applications de mappage, la longitude et la latitude sont des angles et sont exprimées en degrés.</span><span class="sxs-lookup"><span data-stu-id="ec5f6-127">Like in other mapping applications, longitude and latitude are angles and represented in terms of degrees.</span></span> <span data-ttu-id="ec5f6-128">Les valeurs de longitude sont mesurées à partir du premier méridien et sont comprises entre -180 et 180 degrés. Les valeurs de latitude sont mesurées à partir de l'Équateur et sont comprises entre -90 et 90 degrés.</span><span class="sxs-lookup"><span data-stu-id="ec5f6-128">Longitude values are measured from the Prime Meridian and are between -180 and 180.0 degrees, and latitude values are measured from the equator and are between -90.0 and 90.0 degrees.</span></span> 
> 
> <span data-ttu-id="ec5f6-129">Azure Cosmos DB interprète les coordonnées représentées par le système de référence WGS-84.</span><span class="sxs-lookup"><span data-stu-id="ec5f6-129">Azure Cosmos DB interprets coordinates as represented per the WGS-84 reference system.</span></span> <span data-ttu-id="ec5f6-130">Voir ci-dessous pour plus d'informations sur les systèmes de coordonnées de référence.</span><span class="sxs-lookup"><span data-stu-id="ec5f6-130">Please see below for more details about coordinate reference systems.</span></span>
> 
> 

<span data-ttu-id="ec5f6-131">Cela peut être incorporé dans un document Azure Cosmos DB, comme illustré dans cet exemple de profil utilisateur contenant des données d’emplacement :</span><span class="sxs-lookup"><span data-stu-id="ec5f6-131">This can be embedded in an Azure Cosmos DB document as shown in this example of a user profile containing location data:</span></span>

<span data-ttu-id="ec5f6-132">**Utilisation de profil avec emplacement stocké dans Azure Cosmos DB**</span><span class="sxs-lookup"><span data-stu-id="ec5f6-132">**Use Profile with Location stored in Azure Cosmos DB**</span></span>

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

<span data-ttu-id="ec5f6-133">En plus des points, GeoJSON prend en charge les polygones et LineStrings.</span><span class="sxs-lookup"><span data-stu-id="ec5f6-133">In addition to points, GeoJSON also supports LineStrings and Polygons.</span></span> <span data-ttu-id="ec5f6-134">**LineStrings** représentent une série de deux ou plusieurs points dans l'espace et les segments de ligne qui les connectent.</span><span class="sxs-lookup"><span data-stu-id="ec5f6-134">**LineStrings** represent a series of two or more points in space and the line segments that connect them.</span></span> <span data-ttu-id="ec5f6-135">Dans les données géographiques, les LineStrings sont généralement utilisées pour représenter les autoroutes ou les cours d’eau.</span><span class="sxs-lookup"><span data-stu-id="ec5f6-135">In geospatial data, LineStrings are commonly used to represent highways or rivers.</span></span> <span data-ttu-id="ec5f6-136">Un **polygone** est une limite de points reliés qui constitue une LineString fermée.</span><span class="sxs-lookup"><span data-stu-id="ec5f6-136">A **Polygon** is a boundary of connected points that forms a closed LineString.</span></span> <span data-ttu-id="ec5f6-137">Les polygones sont couramment utilisés pour représenter des formations naturelles comme des lacs ou des juridictions politiques comme les villes et les États.</span><span class="sxs-lookup"><span data-stu-id="ec5f6-137">Polygons are commonly used to represent natural formations like lakes or political jurisdictions like cities and states.</span></span> <span data-ttu-id="ec5f6-138">Voici un exemple de polygone dans Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="ec5f6-138">Here's an example of a Polygon in Azure Cosmos DB.</span></span> 

<span data-ttu-id="ec5f6-139">**Polygones dans GeoJSON**</span><span class="sxs-lookup"><span data-stu-id="ec5f6-139">**Polygons in GeoJSON**</span></span>

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
> <span data-ttu-id="ec5f6-140">La spécification GeoJSON impose que, pour les polygones valides, la dernière paire de coordonnées fournie soit identique à la première, pour créer une forme fermée.</span><span class="sxs-lookup"><span data-stu-id="ec5f6-140">The GeoJSON specification requires that for valid Polygons, the last coordinate pair provided should be the same as the first, to create a closed shape.</span></span>
> 
> <span data-ttu-id="ec5f6-141">Les points dans un polygone doivent être spécifiés dans le sens antihoraire.</span><span class="sxs-lookup"><span data-stu-id="ec5f6-141">Points within a Polygon must be specified in counter-clockwise order.</span></span> <span data-ttu-id="ec5f6-142">Un polygone spécifié dans le sens horaire représente l’inverse de la région qu’il contient.</span><span class="sxs-lookup"><span data-stu-id="ec5f6-142">A Polygon specified in clockwise order represents the inverse of the region within it.</span></span>
> 
> 

<span data-ttu-id="ec5f6-143">En plus des points, des LineStrings et des polygones, GeoJSON spécifie également la représentation pour le regroupement de plusieurs emplacements géographiques, ainsi que l’association de propriétés arbitraires avec la géolocalisation comme **fonctionnalité**.</span><span class="sxs-lookup"><span data-stu-id="ec5f6-143">In addition to Point, LineString and Polygon, GeoJSON also specifies the representation for how to group multiple geospatial locations, as well as how to associate arbitrary properties with geolocation as a **Feature**.</span></span> <span data-ttu-id="ec5f6-144">Étant donné que ces objets sont des JSON valides, ils peuvent tous être stockés et traités dans Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="ec5f6-144">Since these objects are valid JSON, they can all be stored and processed in Azure Cosmos DB.</span></span> <span data-ttu-id="ec5f6-145">Cependant, Azure Cosmos DB prend uniquement en charge l’indexation automatique des points.</span><span class="sxs-lookup"><span data-stu-id="ec5f6-145">However Azure Cosmos DB only supports automatic indexing of points.</span></span>

### <a name="coordinate-reference-systems"></a><span data-ttu-id="ec5f6-146">Coordination des systèmes de référence</span><span class="sxs-lookup"><span data-stu-id="ec5f6-146">Coordinate reference systems</span></span>
<span data-ttu-id="ec5f6-147">Étant donné que la forme de la terre est irrégulière, les coordonnées des données géospatiales sont représentées dans de nombreux systèmes de coordonnées de référence (CRS), chacun ayant ses propres images de référence et unités de mesure.</span><span class="sxs-lookup"><span data-stu-id="ec5f6-147">Since the shape of the earth is irregular, coordinates of geospatial data is represented in many coordinate reference systems (CRS), each with their own frames of reference and units of measurement.</span></span> <span data-ttu-id="ec5f6-148">Par exemple, le « National Grid of Britain » est un système de référence très précis pour le Royaume-Uni, mais pas à l'extérieur.</span><span class="sxs-lookup"><span data-stu-id="ec5f6-148">For example, the "National Grid of Britain" is a reference system is very accurate for the United Kingdom, but not outside it.</span></span> 

<span data-ttu-id="ec5f6-149">Le CRS moderne le plus populaire est le World Geodetic System [WGS-84](http://earth-info.nga.mil/GandG/wgs84/).</span><span class="sxs-lookup"><span data-stu-id="ec5f6-149">The most popular CRS in use today is the World Geodetic System  [WGS-84](http://earth-info.nga.mil/GandG/wgs84/).</span></span> <span data-ttu-id="ec5f6-150">Les périphériques GPS et de nombreux services de mappage, notamment les API Bing Maps et Google Maps, utilisent le WGS-84.</span><span class="sxs-lookup"><span data-stu-id="ec5f6-150">GPS devices, and many mapping services including Google Maps and Bing Maps APIs use WGS-84.</span></span> <span data-ttu-id="ec5f6-151">Azure Cosmos DB prend en charge l’indexation et l’interrogation de données géographiques uniquement à l’aide du CRS WGS-84.</span><span class="sxs-lookup"><span data-stu-id="ec5f6-151">Azure Cosmos DB supports indexing and querying of geospatial data using the WGS-84 CRS only.</span></span> 

## <a name="creating-documents-with-spatial-data"></a><span data-ttu-id="ec5f6-152">Création de documents avec les données spatiales</span><span class="sxs-lookup"><span data-stu-id="ec5f6-152">Creating documents with spatial data</span></span>
<span data-ttu-id="ec5f6-153">Lorsque vous créez des documents qui contiennent des valeurs GeoJSON, ils sont automatiquement indexés avec un index spatial conformément à la stratégie d'indexation de la collection.</span><span class="sxs-lookup"><span data-stu-id="ec5f6-153">When you create documents that contain GeoJSON values, they are automatically indexed with a spatial index in accordance to the indexing policy of the collection.</span></span> <span data-ttu-id="ec5f6-154">Si vous travaillez avec un Kit de développement logiciel (SDK) Azure Cosmos DB dans un langage saisi dynamiquement comme Python ou Node.js, vous devez créer un GeoJSON valide.</span><span class="sxs-lookup"><span data-stu-id="ec5f6-154">If you're working with an Azure Cosmos DB SDK in a dynamically typed language like Python or Node.js, you must create valid GeoJSON.</span></span>

<span data-ttu-id="ec5f6-155">**Création d’un document avec les données géographiques dans Node.js**</span><span class="sxs-lookup"><span data-stu-id="ec5f6-155">**Create Document with Geospatial data in Node.js**</span></span>

```json
var userProfileDocument = {
    "name":"documentdb",
    "location":{
        "type":"Point",
        "coordinates":[ -122.12, 47.66 ]
    }
};

client.createDocument(`dbs/${databaseName}/colls/${collectionName}`, userProfileDocument, (err, created) => {
    // additional code within the callback
});
```

<span data-ttu-id="ec5f6-156">Si vous travaillez avec les API DocumentDB, vous pouvez utiliser les classes `Point` et `Polygon` dans l’espace de noms `Microsoft.Azure.Documents.Spatial` pour incorporer des informations d’emplacement au sein des objets de votre application.</span><span class="sxs-lookup"><span data-stu-id="ec5f6-156">If you're working with the DocumentDB APIs, you can use the `Point` and `Polygon` classes within the `Microsoft.Azure.Documents.Spatial` namespace to embed location information within your application objects.</span></span> <span data-ttu-id="ec5f6-157">Ces classes permettent de simplifier la sérialisation et la désérialisation de données spatiales dans GeoJSON.</span><span class="sxs-lookup"><span data-stu-id="ec5f6-157">These classes help simplify the serialization and deserialization of spatial data into GeoJSON.</span></span>

<span data-ttu-id="ec5f6-158">**Création d’un document avec les données géographiques dans .NET**</span><span class="sxs-lookup"><span data-stu-id="ec5f6-158">**Create Document with Geospatial data in .NET**</span></span>

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

<span data-ttu-id="ec5f6-159">Si vous n'avez pas les informations de latitude et de longitude, mais disposez des adresses physiques ou du nom d'emplacement comme la ville ou le pays, vous pouvez rechercher les coordonnées réelles à l'aide d'un service de géocodage comme Bing Maps REST Services.</span><span class="sxs-lookup"><span data-stu-id="ec5f6-159">If you don't have the latitude and longitude information, but have the physical addresses or location name like city or country, you can look up the actual coordinates by using a geocoding service like Bing Maps REST Services.</span></span> <span data-ttu-id="ec5f6-160">En savoir plus sur le géocodage de Bing Maps [ici](https://msdn.microsoft.com/library/ff701713.aspx).</span><span class="sxs-lookup"><span data-stu-id="ec5f6-160">Learn more about Bing Maps geocoding [here](https://msdn.microsoft.com/library/ff701713.aspx).</span></span>

## <a name="querying-spatial-types"></a><span data-ttu-id="ec5f6-161">Interrogation des types spatiaux</span><span class="sxs-lookup"><span data-stu-id="ec5f6-161">Querying spatial types</span></span>
<span data-ttu-id="ec5f6-162">Maintenant que nous avons vu comment insérer des données géospatiales, voyons comment interroger ces données à l’aide d’Azure Cosmos DB avec SQL et LINQ.</span><span class="sxs-lookup"><span data-stu-id="ec5f6-162">Now that we've taken a look at how to insert geospatial data, let's take a look at how to query this data using Azure Cosmos DB using SQL and LINQ.</span></span>

### <a name="spatial-sql-built-in-functions"></a><span data-ttu-id="ec5f6-163">Fonctions spatiales SQL intégrées</span><span class="sxs-lookup"><span data-stu-id="ec5f6-163">Spatial SQL built-in functions</span></span>
<span data-ttu-id="ec5f6-164">Azure Cosmos DB prend en charge les fonctions intégrées Open Geospatial Consortium (OGC) suivantes pour les requêtes géospatiales.</span><span class="sxs-lookup"><span data-stu-id="ec5f6-164">Azure Cosmos DB supports the following Open Geospatial Consortium (OGC) built-in functions for geospatial querying.</span></span> <span data-ttu-id="ec5f6-165">Pour plus d’informations sur l’ensemble complet de fonctions intégrées dans le langage SQL, reportez-vous à [Requête Azure Cosmos DB](documentdb-sql-query.md).</span><span class="sxs-lookup"><span data-stu-id="ec5f6-165">For more details on the complete set of built-in functions in the SQL language, please refer to [Query Azure Cosmos DB](documentdb-sql-query.md).</span></span>

<table>
<tr>
  <td><span data-ttu-id="ec5f6-166"><strong>Utilisation</strong></span><span class="sxs-lookup"><span data-stu-id="ec5f6-166"><strong>Usage</strong></span></span></td>
  <td><span data-ttu-id="ec5f6-167"><strong>Description</strong></span><span class="sxs-lookup"><span data-stu-id="ec5f6-167"><strong>Description</strong></span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="ec5f6-168">ST_DISTANCE (spatial_expr, spatial_expr)</span><span class="sxs-lookup"><span data-stu-id="ec5f6-168">ST_DISTANCE (spatial_expr, spatial_expr)</span></span></td>
  <td><span data-ttu-id="ec5f6-169">Retourne la distance entre les deux expressions Point, Polygone ou LineString de GeoJSON.</span><span class="sxs-lookup"><span data-stu-id="ec5f6-169">Returns the distance between the two GeoJSON Point, Polygon, or LineString expressions.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="ec5f6-170">ST_WITHIN (spatial_expr, spatial_expr)</span><span class="sxs-lookup"><span data-stu-id="ec5f6-170">ST_WITHIN (spatial_expr, spatial_expr)</span></span></td>
  <td><span data-ttu-id="ec5f6-171">Retourne une expression booléenne indiquant si le premier objet GeoJSON (Point, Polygone ou LineString) se trouve dans le second objet GeoJSON (Point, Polygone ou LineString).</span><span class="sxs-lookup"><span data-stu-id="ec5f6-171">Returns a Boolean expression indicating whether the first GeoJSON object (Point, Polygon, or LineString) is within the second GeoJSON object (Point, Polygon, or LineString).</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="ec5f6-172">ST_INTERSECTS (spatial_expr, spatial_expr)</span><span class="sxs-lookup"><span data-stu-id="ec5f6-172">ST_INTERSECTS (spatial_expr, spatial_expr)</span></span></td>
  <td><span data-ttu-id="ec5f6-173">Retourne une expression booléenne indiquant si les deux objets GeoJSON spécifiés (Point, Polygone ou LineString) se croisent.</span><span class="sxs-lookup"><span data-stu-id="ec5f6-173">Returns a Boolean expression indicating whether the two specified GeoJSON objects (Point, Polygon, or LineString) intersect.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="ec5f6-174">ST_ISVALID</span><span class="sxs-lookup"><span data-stu-id="ec5f6-174">ST_ISVALID</span></span></td>
  <td><span data-ttu-id="ec5f6-175">Renvoie une valeur booléenne indiquant si l’expression Point, Polygone ou LineString GeoJSON spécifiée est valide.</span><span class="sxs-lookup"><span data-stu-id="ec5f6-175">Returns a Boolean value indicating whether the specified GeoJSON Point, Polygon, or LineString expression is valid.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="ec5f6-176">ST_ISVALIDDETAILED</span><span class="sxs-lookup"><span data-stu-id="ec5f6-176">ST_ISVALIDDETAILED</span></span></td>
  <td><span data-ttu-id="ec5f6-177">Renvoie une valeur JSON contenant une valeur booléenne si l’expression Point, Polygone ou LineString GeoJSON spécifiée est valide et, dans le cas contraire, le motif sous forme de valeur de chaîne.</span><span class="sxs-lookup"><span data-stu-id="ec5f6-177">Returns a JSON value containing a Boolean value if the specified GeoJSON Point, Polygon, or LineString expression is valid, and if invalid, additionally the reason as a string value.</span></span></td>
</tr>
</table>

<span data-ttu-id="ec5f6-178">Les fonctions spatiales peuvent être utilisées pour effectuer des requêtes de proximité par rapport aux données spatiales.</span><span class="sxs-lookup"><span data-stu-id="ec5f6-178">Spatial functions can be used to perform proximity queries against spatial data.</span></span> <span data-ttu-id="ec5f6-179">Par exemple, voici une requête qui retourne tous les documents de famille se trouvant dans un rayon de 30 kilomètres de l'emplacement spécifié à l'aide de la fonction intégrée ST_DISTANCE.</span><span class="sxs-lookup"><span data-stu-id="ec5f6-179">For example, here's a query that returns all family documents that are within 30 km of the specified location using the ST_DISTANCE built-in function.</span></span> 

<span data-ttu-id="ec5f6-180">**Requête**</span><span class="sxs-lookup"><span data-stu-id="ec5f6-180">**Query**</span></span>

    SELECT f.id 
    FROM Families f 
    WHERE ST_DISTANCE(f.location, {'type': 'Point', 'coordinates':[31.9, -4.8]}) < 30000

<span data-ttu-id="ec5f6-181">**Résultats**</span><span class="sxs-lookup"><span data-stu-id="ec5f6-181">**Results**</span></span>

    [{
      "id": "WakefieldFamily"
    }]

<span data-ttu-id="ec5f6-182">Si vous incluez l'indexation spatiale dans votre stratégie d'indexation, les « requêtes à distance » seront servies efficacement dans l'index.</span><span class="sxs-lookup"><span data-stu-id="ec5f6-182">If you include spatial indexing in your indexing policy, then "distance queries" will be served efficiently through the index.</span></span> <span data-ttu-id="ec5f6-183">Pour plus d'informations sur l'indexation spatiale, consultez la section ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="ec5f6-183">For more details on spatial indexing, please see the section below.</span></span> <span data-ttu-id="ec5f6-184">Si vous n'avez pas un index spatial pour les chemins d'accès spécifiés, vous pouvez quand même effectuer des requêtes spatiales en spécifiant l’en-tête de requête `x-ms-documentdb-query-enable-scan` avec la valeur définie sur « true ».</span><span class="sxs-lookup"><span data-stu-id="ec5f6-184">If you don't have a spatial index for the specified paths, you can still perform spatial queries by specifying `x-ms-documentdb-query-enable-scan` request header with the value set to "true".</span></span> <span data-ttu-id="ec5f6-185">Dans .NET, cela est possible en passant l’argument facultatif **FeedOptions** aux requêtes avec [EnableScanInQuery](https://msdn.microsoft.com/library/microsoft.azure.documents.client.feedoptions.enablescaninquery.aspx#P:Microsoft.Azure.Documents.Client.FeedOptions.EnableScanInQuery) défini sur true.</span><span class="sxs-lookup"><span data-stu-id="ec5f6-185">In .NET, this can be done by passing the optional **FeedOptions** argument to queries with [EnableScanInQuery](https://msdn.microsoft.com/library/microsoft.azure.documents.client.feedoptions.enablescaninquery.aspx#P:Microsoft.Azure.Documents.Client.FeedOptions.EnableScanInQuery) set to true.</span></span> 

<span data-ttu-id="ec5f6-186">Vous pouvez utiliser ST_WITHIN pour vérifier si un point se trouve dans un polygone.</span><span class="sxs-lookup"><span data-stu-id="ec5f6-186">ST_WITHIN can be used to check if a point lies within a Polygon.</span></span> <span data-ttu-id="ec5f6-187">Généralement, les polygones sont utilisés pour représenter des limites comme les codes postaux, les frontières d’États ou les formations naturelles.</span><span class="sxs-lookup"><span data-stu-id="ec5f6-187">Commonly Polygons are used to represent boundaries like zip codes, state boundaries, or natural formations.</span></span> <span data-ttu-id="ec5f6-188">Si vous incluez l'indexation spatiale dans votre stratégie d'indexation, les requêtes « within » seront servies efficacement dans l'index.</span><span class="sxs-lookup"><span data-stu-id="ec5f6-188">Again if you include spatial indexing in your indexing policy, then "within" queries will be served efficiently through the index.</span></span> 

<span data-ttu-id="ec5f6-189">Les arguments de polygone dans ST_WITHIN peuvent contenir un seul cercle. Cela signifie que les polygones ne doivent pas contenir de trous.</span><span class="sxs-lookup"><span data-stu-id="ec5f6-189">Polygon arguments in ST_WITHIN can contain only a single ring, i.e. the Polygons must not contain holes in them.</span></span> 

<span data-ttu-id="ec5f6-190">**Requête**</span><span class="sxs-lookup"><span data-stu-id="ec5f6-190">**Query**</span></span>

    SELECT * 
    FROM Families f 
    WHERE ST_WITHIN(f.location, {
        'type':'Polygon', 
        'coordinates': [[[31.8, -5], [32, -5], [32, -4.7], [31.8, -4.7], [31.8, -5]]]
    })

<span data-ttu-id="ec5f6-191">**Résultats**</span><span class="sxs-lookup"><span data-stu-id="ec5f6-191">**Results**</span></span>

    [{
      "id": "WakefieldFamily",
    }]

> [!NOTE]
> <span data-ttu-id="ec5f6-192">Tout comme pour les types non correspondants dans une requête Azure Cosmos DB, si la valeur de l’emplacement spécifié dans un argument est incorrecte ou non valide, elle prend alors la valeur **indéfinie** et le document évalué est ignoré des résultats de requête.</span><span class="sxs-lookup"><span data-stu-id="ec5f6-192">Similar to how mismatched types works in Azure Cosmos DB query, if the location value specified in either argument is malformed or invalid, then it will evaluate to **undefined** and the evaluated document to be skipped from the query results.</span></span> <span data-ttu-id="ec5f6-193">Si votre requête ne retourne aucun résultat, exécutez ST_ISVALIDDETAILED afin de déboguer l’absence de validité du type spatial.</span><span class="sxs-lookup"><span data-stu-id="ec5f6-193">If your query returns no results, run ST_ISVALIDDETAILED To debug why the spatail type is invalid.</span></span>     
> 
> 

<span data-ttu-id="ec5f6-194">Azure Cosmos DB prend également en charge les requêtes inversées. Vous pouvez, par exemple, indexer des polygones ou des lignes dans Azure Cosmos DB, puis interroger les zones qui contiennent un point spécifique.</span><span class="sxs-lookup"><span data-stu-id="ec5f6-194">Azure Cosmos DB also supports performing inverse queries, i.e. you can index Polygons or lines in Azure Cosmos DB, then query for the areas that contain a specified point.</span></span> <span data-ttu-id="ec5f6-195">Ce modèle est généralement utilisé dans la logistique pour identifier lorsqu’un camion entre ou quitte une région spécifiée, par exemple.</span><span class="sxs-lookup"><span data-stu-id="ec5f6-195">This pattern is commonly used in logistics to identify e.g. when a truck enters or leaves a designated area.</span></span> 

<span data-ttu-id="ec5f6-196">**Requête**</span><span class="sxs-lookup"><span data-stu-id="ec5f6-196">**Query**</span></span>

    SELECT * 
    FROM Areas a 
    WHERE ST_WITHIN({'type': 'Point', 'coordinates':[31.9, -4.8]}, a.location)


<span data-ttu-id="ec5f6-197">**Résultats**</span><span class="sxs-lookup"><span data-stu-id="ec5f6-197">**Results**</span></span>

    [{
      "id": "MyDesignatedLocation",
      "location": {
        "type":"Polygon", 
        "coordinates": [[[31.8, -5], [32, -5], [32, -4.7], [31.8, -4.7], [31.8, -5]]]
      }
    }]

<span data-ttu-id="ec5f6-198">ST_ISVALID et ST_ISVALIDDETAILED peuvent être utilisés pour vérifier si un objet spatial est valide.</span><span class="sxs-lookup"><span data-stu-id="ec5f6-198">ST_ISVALID and ST_ISVALIDDETAILED can be used to check if a spatial object is valid.</span></span> <span data-ttu-id="ec5f6-199">Par exemple, la requête suivante vérifie la validité d'un point avec une valeur de latitude hors limites (-132.8).</span><span class="sxs-lookup"><span data-stu-id="ec5f6-199">For example, the following query checks the validity of a point with an out of range latitude value (-132.8).</span></span> <span data-ttu-id="ec5f6-200">ST_ISVALID retourne simplement une valeur booléenne et ST_ISVALIDDETAILED renvoie la valeur booléenne et une chaîne contenant la raison pour laquelle il est non valide.</span><span class="sxs-lookup"><span data-stu-id="ec5f6-200">ST_ISVALID returns just a Boolean value, and ST_ISVALIDDETAILED returns the Boolean and a string containing the reason why it is considered invalid.</span></span>

<span data-ttu-id="ec5f6-201">** Requête **</span><span class="sxs-lookup"><span data-stu-id="ec5f6-201">** Query **</span></span>

    SELECT ST_ISVALID({ "type": "Point", "coordinates": [31.9, -132.8] })

<span data-ttu-id="ec5f6-202">**Résultats**</span><span class="sxs-lookup"><span data-stu-id="ec5f6-202">**Results**</span></span>

    [{
      "$1": false
    }]

<span data-ttu-id="ec5f6-203">Vous pouvez aussi utiliser ces fonctions pour valider des polygones.</span><span class="sxs-lookup"><span data-stu-id="ec5f6-203">These functions can also be used to validate Polygons.</span></span> <span data-ttu-id="ec5f6-204">Par exemple, nous utilisons ici ST_ISVALIDDETAILED pour valider un polygone non fermé.</span><span class="sxs-lookup"><span data-stu-id="ec5f6-204">For example, here we use ST_ISVALIDDETAILED to validate a Polygon that is not closed.</span></span> 

<span data-ttu-id="ec5f6-205">**Requête**</span><span class="sxs-lookup"><span data-stu-id="ec5f6-205">**Query**</span></span>

    SELECT ST_ISVALIDDETAILED({ "type": "Polygon", "coordinates": [[ 
        [ 31.8, -5 ], [ 31.8, -4.7 ], [ 32, -4.7 ], [ 32, -5 ] 
        ]]})

<span data-ttu-id="ec5f6-206">**Résultats**</span><span class="sxs-lookup"><span data-stu-id="ec5f6-206">**Results**</span></span>

    [{
       "$1": { 
            "valid": false, 
            "reason": "The Polygon input is not valid because the start and end points of the ring number 1 are not the same. Each ring of a Polygon must have the same start and end points." 
          }
    }]

### <a name="linq-querying-in-the-net-sdk"></a><span data-ttu-id="ec5f6-207">Interrogation LINQ dans le Kit de développement logiciel (SDK) .NET</span><span class="sxs-lookup"><span data-stu-id="ec5f6-207">LINQ Querying in the .NET SDK</span></span>
<span data-ttu-id="ec5f6-208">Le Kit de développement logiciel (SDK) .NET DocumentDB fournit également les méthodes de stub `Distance()` et `Within()` pour une utilisation dans des expressions LINQ.</span><span class="sxs-lookup"><span data-stu-id="ec5f6-208">The DocumentDB .NET SDK also providers stub methods `Distance()` and `Within()` for use within LINQ expressions.</span></span> <span data-ttu-id="ec5f6-209">Le fournisseur DocumentDB LINQ traduit ces appels de méthode pour les appels de fonction intégrés SQL équivalents (ST_DISTANCE et ST_WITHIN, respectivement).</span><span class="sxs-lookup"><span data-stu-id="ec5f6-209">The DocumentDB LINQ provider translates these method calls to the equivalent SQL built-in function calls (ST_DISTANCE and ST_WITHIN respectively).</span></span> 

<span data-ttu-id="ec5f6-210">Voici un exemple d’une requête LINQ qui recherche tous les documents de la collection Azure Cosmos DB dont la valeur « location » est dans un rayon de 30 kilomètres du point spécifié à l’aide de LINQ.</span><span class="sxs-lookup"><span data-stu-id="ec5f6-210">Here's an example of a LINQ query that finds all documents in the Azure Cosmos DB collection whose "location" value is within a radius of 30km of the specified point using LINQ.</span></span>

<span data-ttu-id="ec5f6-211">**Requête LINQ de distance**</span><span class="sxs-lookup"><span data-stu-id="ec5f6-211">**LINQ query for Distance**</span></span>

    foreach (UserProfile user in client.CreateDocumentQuery<UserProfile>(UriFactory.CreateDocumentCollectionUri("db", "profiles"))
        .Where(u => u.ProfileType == "Public" && a.Location.Distance(new Point(32.33, -4.66)) < 30000))
    {
        Console.WriteLine("\t" + user);
    }

<span data-ttu-id="ec5f6-212">De même, voici une requête pour rechercher tous les documents dont la « location » est dans la zone/le polygone spécifié.</span><span class="sxs-lookup"><span data-stu-id="ec5f6-212">Similarly, here's a query for finding all the documents whose "location" is within the specified box/Polygon.</span></span> 

<span data-ttu-id="ec5f6-213">**Requête LINQ within**</span><span class="sxs-lookup"><span data-stu-id="ec5f6-213">**LINQ query for Within**</span></span>

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


<span data-ttu-id="ec5f6-214">Maintenant que nous avons expliqué l’interrogation de documents à l’aide de LINQ et SQL, voyons comment configurer Azure Cosmos DB pour l’indexation spatiale.</span><span class="sxs-lookup"><span data-stu-id="ec5f6-214">Now that we've taken a look at how to query documents using LINQ and SQL, let's take a look at how to configure Azure Cosmos DB for spatial indexing.</span></span>

## <a name="indexing"></a><span data-ttu-id="ec5f6-215">Indexation</span><span class="sxs-lookup"><span data-stu-id="ec5f6-215">Indexing</span></span>
<span data-ttu-id="ec5f6-216">Comme décrit dans le livre [Schema Agnostic Indexing with Azure Cosmos DB](http://www.vldb.org/pvldb/vol8/p1668-shukla.pdf), nous avons conçu le moteur de base de données Azure Cosmos DB pour être véritablement indépendant du schéma et fournir une assistance exceptionnelle pour JSON.</span><span class="sxs-lookup"><span data-stu-id="ec5f6-216">As we described in the [Schema Agnostic Indexing with Azure Cosmos DB](http://www.vldb.org/pvldb/vol8/p1668-shukla.pdf) paper, we designed Azure Cosmos DB’s database engine to be truly schema agnostic and provide first class support for JSON.</span></span> <span data-ttu-id="ec5f6-217">Le moteur de base de données optimisé en écriture d’Azure Cosmos DB comprend les données spatiales (points, polygones et lignes) représentées dans la norme GeoJSON en mode natif.</span><span class="sxs-lookup"><span data-stu-id="ec5f6-217">The write optimized database engine of Azure Cosmos DB natively understands spatial data (points, Polygons and lines) represented in the GeoJSON standard.</span></span>

<span data-ttu-id="ec5f6-218">En bref, la géométrie est projetée à partir des coordonnées géodésiques sur un plan 2D, puis divisée progressivement en cellules à l'aide un **quadtree**.</span><span class="sxs-lookup"><span data-stu-id="ec5f6-218">In a nutshell, the geometry is projected from geodetic coordinates onto a 2D plane then divided progressively into cells using a **quadtree**.</span></span> <span data-ttu-id="ec5f6-219">Ces cellules sont mappées en 1D selon l'emplacement de la cellule dans une **courbe de remplissage d'espace de Hilbert**qui permet de préserver la localité des points.</span><span class="sxs-lookup"><span data-stu-id="ec5f6-219">These cells are mapped to 1D based on the location of the cell within a **Hilbert space filling curve**, which preserves locality of points.</span></span> <span data-ttu-id="ec5f6-220">En outre, lorsque les données d’emplacement sont indexées, elles passent par un processus connu sous le nom de **pavage**, c’est-à-dire que toutes les cellules qui se croisent à un emplacement sont identifiées et stockées en tant que clés dans l’index Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="ec5f6-220">Additionally when location data is indexed, it goes through a process known as **tessellation**, i.e. all the cells that intersect a location are identified and stored as keys in the Azure Cosmos DB index.</span></span> <span data-ttu-id="ec5f6-221">Au moment de la requête, des arguments comme les points et les polygones sont également fractionnés pour extraire les plages d’ID de cellule appropriées, puis utilisés pour récupérer des données à partir de l’index.</span><span class="sxs-lookup"><span data-stu-id="ec5f6-221">At query time, arguments like points and Polygons are also tessellated to extract the relevant cell ID ranges, then used to retrieve data from the index.</span></span>

<span data-ttu-id="ec5f6-222">Si vous spécifiez une stratégie d'indexation qui inclut un index spatial pour /* (tous les chemins d'accès), tous les points trouvés dans la collection sont indexés pour des requêtes spatiales efficaces (ST_WITHIN et ST_DISTANCE).</span><span class="sxs-lookup"><span data-stu-id="ec5f6-222">If you specify an indexing policy that includes spatial index for /* (all paths), then all points found within the collection are indexed for efficient spatial queries (ST_WITHIN and ST_DISTANCE).</span></span> <span data-ttu-id="ec5f6-223">Les index spatiaux n'ont pas une valeur de précision et utilisent toujours une valeur de précision par défaut.</span><span class="sxs-lookup"><span data-stu-id="ec5f6-223">Spatial indexes do not have a precision value, and always use a default precision value.</span></span>

> [!NOTE]
> <span data-ttu-id="ec5f6-224">Azure Cosmos DB prend en charge l’indexation automatique des points, polygones et lineStrings.</span><span class="sxs-lookup"><span data-stu-id="ec5f6-224">Azure Cosmos DB supports automatic indexing of Points, Polygons, and LineStrings</span></span>
> 
> 

<span data-ttu-id="ec5f6-225">L'extrait JSON suivant montre une politique d'indexation avec l’indexation spatiale activée, c'est-à-dire n'importe quel point GeoJSON trouvé au sein de documents pour l'interrogation spatiale d'index.</span><span class="sxs-lookup"><span data-stu-id="ec5f6-225">The following JSON snippet shows an indexing policy with spatial indexing enabled, i.e. index any GeoJSON point found within documents for spatial querying.</span></span> <span data-ttu-id="ec5f6-226">Si vous modifiez la stratégie d’indexation à l’aide du portail Azure, vous pouvez spécifier le JSON suivant pour la stratégie d’indexation pour activer l’indexation spatiale pour votre collection.</span><span class="sxs-lookup"><span data-stu-id="ec5f6-226">If you are modifying the indexing policy using the Azure Portal, you can specify the following JSON for indexing policy to enable spatial indexing on your collection.</span></span>

<span data-ttu-id="ec5f6-227">**Stratégie d’indexation de collection JSON avec Spatial activé pour les points et les polygones**</span><span class="sxs-lookup"><span data-stu-id="ec5f6-227">**Collection Indexing Policy JSON with Spatial enabled for points and Polygons**</span></span>

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

<span data-ttu-id="ec5f6-228">Voici un extrait de code dans .NET qui montre comment créer une collection avec l’indexation spatiale activée pour tous les chemins d'accès contenant des points.</span><span class="sxs-lookup"><span data-stu-id="ec5f6-228">Here's a code snippet in .NET that shows how to create a collection with spatial indexing turned on for all paths containing points.</span></span> 

<span data-ttu-id="ec5f6-229">**Création d’une collection avec l'indexation spatiale**</span><span class="sxs-lookup"><span data-stu-id="ec5f6-229">**Create a collection with spatial indexing**</span></span>

    DocumentCollection spatialData = new DocumentCollection()
    spatialData.IndexingPolicy = new IndexingPolicy(new SpatialIndex(DataType.Point)); //override to turn spatial on by default
    collection = await client.CreateDocumentCollectionAsync(UriFactory.CreateDatabaseUri("db"), spatialData);

<span data-ttu-id="ec5f6-230">Voici comment vous pouvez modifier un regroupement existant pour tirer parti de l'indexation spatiale sur tous les points stockés au sein de documents.</span><span class="sxs-lookup"><span data-stu-id="ec5f6-230">And here's how you can modify an existing collection to take advantage of spatial indexing over any points that are stored within documents.</span></span>

<span data-ttu-id="ec5f6-231">**Modification d’une collection existante avec l'indexation spatiale**</span><span class="sxs-lookup"><span data-stu-id="ec5f6-231">**Modify an existing collection with spatial indexing**</span></span>

    Console.WriteLine("Updating collection with spatial indexing enabled in indexing policy...");
    collection.IndexingPolicy = new IndexingPolicy(new SpatialIndex(DataType.Point));
    await client.ReplaceDocumentCollectionAsync(collection);

    Console.WriteLine("Waiting for indexing to complete...");
    long indexTransformationProgress = 0;
    while (indexTransformationProgress < 100)
    {
        ResourceResponse<DocumentCollection> response = await client.ReadDocumentCollectionAsync(UriFactory.CreateDocumentCollectionUri("db", "coll"));
        indexTransformationProgress = response.IndexTransformationProgress;

        await Task.Delay(TimeSpan.FromSeconds(1));
    }

> [!NOTE]
> <span data-ttu-id="ec5f6-232">Si la valeur GeoJSON d'emplacement dans le document est incorrecte ou non valide, elle n’est pas indexée pour les requêtes spatiales.</span><span class="sxs-lookup"><span data-stu-id="ec5f6-232">If the location GeoJSON value within the document is malformed or invalid, then it will not get indexed for spatial querying.</span></span> <span data-ttu-id="ec5f6-233">Vous pouvez valider les valeurs d'emplacement à l'aide de ST_ISVALID et ST_ISVALIDDETAILED.</span><span class="sxs-lookup"><span data-stu-id="ec5f6-233">You can validate location values using ST_ISVALID and ST_ISVALIDDETAILED.</span></span>
> 
> <span data-ttu-id="ec5f6-234">Si la définition de votre collection contient une clé de partition, la progression de la transformation d’indexation n’est pas signalée.</span><span class="sxs-lookup"><span data-stu-id="ec5f6-234">If your collection definition includes a partition key, indexing transformation progress is not reported.</span></span> 
> 
> 

## <a name="next-steps"></a><span data-ttu-id="ec5f6-235">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ec5f6-235">Next steps</span></span>
<span data-ttu-id="ec5f6-236">Maintenant que vous avez appris à utiliser la prise en charge géospatiale dans Azure Cosmos DB, vous pouvez :</span><span class="sxs-lookup"><span data-stu-id="ec5f6-236">Now that you've learnt about how to get started with geospatial support in Azure Cosmos DB, you can:</span></span>

* <span data-ttu-id="ec5f6-237">Commencer à coder avec les [exemples de code .NET Geospatial sur GitHub](https://github.com/Azure/azure-documentdb-dotnet/blob/fcf23d134fc5019397dcf7ab97d8d6456cd94820/samples/code-samples/Geospatial/Program.cs)</span><span class="sxs-lookup"><span data-stu-id="ec5f6-237">Start coding with the [Geospatial .NET code samples on GitHub](https://github.com/Azure/azure-documentdb-dotnet/blob/fcf23d134fc5019397dcf7ab97d8d6456cd94820/samples/code-samples/Geospatial/Program.cs)</span></span>
* <span data-ttu-id="ec5f6-238">Découvrir l’interrogation géospatiale dans [Azure Cosmos DB Query Playground](http://www.documentdb.com/sql/demo#geospatial)</span><span class="sxs-lookup"><span data-stu-id="ec5f6-238">Get hands on with geospatial querying at the [Azure Cosmos DB Query Playground](http://www.documentdb.com/sql/demo#geospatial)</span></span>
* <span data-ttu-id="ec5f6-239">En savoir plus sur les [requêtes Azure Cosmos DB](documentdb-sql-query.md)</span><span class="sxs-lookup"><span data-stu-id="ec5f6-239">Learn more about [Azure Cosmos DB Query](documentdb-sql-query.md)</span></span>
* <span data-ttu-id="ec5f6-240">En savoir plus sur les [stratégies d’indexation Azure Cosmos DB](indexing-policies.md)</span><span class="sxs-lookup"><span data-stu-id="ec5f6-240">Learn more about [Azure Cosmos DB Indexing Policies](indexing-policies.md)</span></span>

