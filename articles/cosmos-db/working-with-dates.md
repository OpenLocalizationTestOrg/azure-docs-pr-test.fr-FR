---
title: "Utilisation des dates dans Azure Cosmos DB | Microsoft Docs"
description: "En savoir plus sur l’utilisation des dates dans Azure Cosmos DB."
services: cosmos-db
author: arramac
manager: jhubbard
editor: mimig
documentationcenter: 
ms.assetid: e587772f-ce9f-498c-a017-a51e7265bb23
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: arramac
ms.openlocfilehash: b6a77e33eea24000037ffb31d7aae3cb1d345ce9
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="working-with-dates-in-azure-cosmos-db"></a><span data-ttu-id="dd117-103">Utilisation des dates dans Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="dd117-103">Working with Dates in Azure Cosmos DB</span></span>
<span data-ttu-id="dd117-104">Azure Cosmos DB offre une flexibilité des schémas et une indexation riche par le biais d’un modèle de données [JSON](http://www.json.org) natif.</span><span class="sxs-lookup"><span data-stu-id="dd117-104">Azure Cosmos DB delivers schema flexibility and rich indexing via a native [JSON](http://www.json.org) data model.</span></span> <span data-ttu-id="dd117-105">Toutes les ressources Azure Cosmos DB, y compris les bases de données, les collections, les documents et les procédures stockées, sont modélisées et stockées en tant que documents JSON.</span><span class="sxs-lookup"><span data-stu-id="dd117-105">All Azure Cosmos DB resources including databases, collections, documents, and stored procedures are modeled and stored as JSON documents.</span></span> <span data-ttu-id="dd117-106">Pour être portable, JSON (et Azure Cosmos DB) prend en charge uniquement un petit ensemble de types de base : chaîne, nombre, booléen, tableau, objet et null.</span><span class="sxs-lookup"><span data-stu-id="dd117-106">As a requirement for being portable, JSON (and Azure Cosmos DB) supports only a small set of basic types: String, Number, Boolean, Array, Object, and Null.</span></span> <span data-ttu-id="dd117-107">Toutefois, JSON est flexible et permet aux développeurs et aux infrastructures de représenter des types plus complexes en utilisant ces primitives et en les composant en tant qu’objets ou tableaux.</span><span class="sxs-lookup"><span data-stu-id="dd117-107">However, JSON is flexible and allow developers and frameworks to represent more complex types using these primitives and composing them as objects or arrays.</span></span> 

<span data-ttu-id="dd117-108">Outre les types de base, de nombreuses applications ont besoin du type [DateTime](https://msdn.microsoft.com/library/system.datetime(v=vs.110).aspx) pour représenter des dates et horodatages.</span><span class="sxs-lookup"><span data-stu-id="dd117-108">In addition to the basic types, many applications need the [DateTime](https://msdn.microsoft.com/library/system.datetime(v=vs.110).aspx) type to represent dates and timestamps.</span></span> <span data-ttu-id="dd117-109">Cet article décrit comment des développeurs peuvent stocker, récupérer et interroger des dates dans Azure Cosmos DB à l’aide du kit SDK .NET.</span><span class="sxs-lookup"><span data-stu-id="dd117-109">This article describes how developers can store, retrieve, and query dates in Azure Cosmos DB using the .NET SDK.</span></span>

## <a name="storing-datetimes"></a><span data-ttu-id="dd117-110">Stockage de valeurs DateTime</span><span class="sxs-lookup"><span data-stu-id="dd117-110">Storing DateTimes</span></span>
<span data-ttu-id="dd117-111">Par défaut, le [SDK Azure Cosmos DB](documentdb-sdk-dotnet.md) sérialise les valeurs DateTime en tant que chaînes [ISO 8601](http://www.iso.org/iso/catalogue_detail?csnumber=40874).</span><span class="sxs-lookup"><span data-stu-id="dd117-111">By default, the [Azure Cosmos DB SDK](documentdb-sdk-dotnet.md) serializes DateTime values as [ISO 8601](http://www.iso.org/iso/catalogue_detail?csnumber=40874) strings.</span></span> <span data-ttu-id="dd117-112">La plupart des applications peuvent utiliser la représentation sous forme de chaîne par défaut pour DateTime pour les raisons suivantes :</span><span class="sxs-lookup"><span data-stu-id="dd117-112">Most applications can use the default string representation for DateTime for the following reasons:</span></span>

* <span data-ttu-id="dd117-113">Les chaînes peuvent être comparées et l’ordre relatif des valeurs DateTime est conservé lorsque celles-ci sont transformées en chaînes.</span><span class="sxs-lookup"><span data-stu-id="dd117-113">Strings can be compared, and the relative ordering of the DateTime values is preserved when they are transformed to strings.</span></span> 
* <span data-ttu-id="dd117-114">Cette approche ne nécessite pas de code personnalisé ou d’attributs pour la conversion JSON.</span><span class="sxs-lookup"><span data-stu-id="dd117-114">This approach doesn't require any custom code or attributes for JSON conversion.</span></span>
* <span data-ttu-id="dd117-115">Les dates stockées au format JSON sont lisibles.</span><span class="sxs-lookup"><span data-stu-id="dd117-115">The dates as stored in JSON are human readable.</span></span>
* <span data-ttu-id="dd117-116">Cette approche peut tirer parti de l’index d’Azure Cosmos DB pour offrir des performances de requête rapides.</span><span class="sxs-lookup"><span data-stu-id="dd117-116">This approach can take advantage of Azure Cosmos DB's index for fast query performance.</span></span>

<span data-ttu-id="dd117-117">Par exemple, l’extrait de code suivant stocke un objet `Order` contenant deux propriétés DateTime (`ShipDate` et `OrderDate`) en tant que document à l’aide du SDK .NET :</span><span class="sxs-lookup"><span data-stu-id="dd117-117">For example, the following snippet stores an `Order` object containing two DateTime properties - `ShipDate` and `OrderDate` as a document using the .NET SDK:</span></span>

    public class Order
    {
        [JsonProperty(PropertyName="id")]
        public string Id { get; set; }
        public DateTime OrderDate { get; set; }
        public DateTime ShipDate { get; set; }
        public double Total { get; set; }
    }

    await client.CreateDocumentAsync("/dbs/orderdb/colls/orders", 
        new Order 
        { 
            Id = "09152014101",
            OrderDate = DateTime.UtcNow.AddDays(-30),
            ShipDate = DateTime.UtcNow.AddDays(-14), 
            Total = 113.39
        });

<span data-ttu-id="dd117-118">Ce document est stocké dans Azure Cosmos DB comme suit :</span><span class="sxs-lookup"><span data-stu-id="dd117-118">This document is stored in Azure Cosmos DB as follows:</span></span>

    {
        "id": "09152014101",
        "OrderDate": "2014-09-15T23:14:25.7251173Z",
        "ShipDate": "2014-09-30T23:14:25.7251173Z",
        "Total": 113.39
    }
    

<span data-ttu-id="dd117-119">Vous pouvez également stocker les valeurs DateTime comme horodateurs Unix, autrement dit, comme un nombre représentant le nombre de secondes écoulées depuis le 1er janvier 1970.</span><span class="sxs-lookup"><span data-stu-id="dd117-119">Alternatively, you can store DateTimes as Unix timestamps, that is, as a number representing the number of elapsed seconds since January 1, 1970.</span></span> <span data-ttu-id="dd117-120">La propriété Timestamp interne d’Azure Cosmos DB (`_ts`) suit cette approche.</span><span class="sxs-lookup"><span data-stu-id="dd117-120">Azure Cosmos DB's internal Timestamp (`_ts`) property follows this approach.</span></span> <span data-ttu-id="dd117-121">Vous pouvez utiliser la classe [UnixDateTimeConverter](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.unixdatetimeconverter.aspx) pour sérialiser les valeurs DateTime en tant que nombres.</span><span class="sxs-lookup"><span data-stu-id="dd117-121">You can use the [UnixDateTimeConverter](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.unixdatetimeconverter.aspx) class to serialize DateTimes as numbers.</span></span> 

## <a name="indexing-datetimes-for-range-queries"></a><span data-ttu-id="dd117-122">Indexation des valeurs DateTime pour les requêtes de plage</span><span class="sxs-lookup"><span data-stu-id="dd117-122">Indexing DateTimes for range queries</span></span>
<span data-ttu-id="dd117-123">Les requêtes de plage ont souvent des valeurs DateTime.</span><span class="sxs-lookup"><span data-stu-id="dd117-123">Range queries are common with DateTime values.</span></span> <span data-ttu-id="dd117-124">Par exemple, si vous avez besoin de rechercher toutes les commandes créées depuis la veille ou de rechercher toutes les commandes expédiées au cours des cinq dernières minutes, vous devez effectuer des requêtes de plage.</span><span class="sxs-lookup"><span data-stu-id="dd117-124">For example, if you need to find all orders created since yesterday, or find all orders shipped in the last five minutes, you need to perform range queries.</span></span> <span data-ttu-id="dd117-125">Pour exécuter ces requêtes efficacement, vous devez configurer votre collection pour l’indexation de plage sur les chaînes.</span><span class="sxs-lookup"><span data-stu-id="dd117-125">To execute these queries efficiently, you must configure your collection for Range indexing on strings.</span></span>

    DocumentCollection collection = new DocumentCollection { Id = "orders" };
    collection.IndexingPolicy = new IndexingPolicy(new RangeIndex(DataType.String) { Precision = -1 });
    await client.CreateDocumentCollectionAsync("/dbs/orderdb", collection);

<span data-ttu-id="dd117-126">Pour plus d’informations sur la configuration des stratégies d’indexation, consultez [Stratégies d’indexation d’Azure Cosmos DB](indexing-policies.md).</span><span class="sxs-lookup"><span data-stu-id="dd117-126">You can learn more about how to configure indexing policies at [Azure Cosmos DB Indexing Policies](indexing-policies.md).</span></span>

## <a name="querying-datetimes-in-linq"></a><span data-ttu-id="dd117-127">Interrogation des valeurs DateTime dans LINQ</span><span class="sxs-lookup"><span data-stu-id="dd117-127">Querying DateTimes in LINQ</span></span>
<span data-ttu-id="dd117-128">Le kit de développement logiciel (SDK) .NET DocumentDB prend automatiquement en charge l’interrogation des données stockées dans Azure Cosmos DB via LINQ.</span><span class="sxs-lookup"><span data-stu-id="dd117-128">The DocumentDB .NET SDK automatically supports querying data stored in Azure Cosmos DB via LINQ.</span></span> <span data-ttu-id="dd117-129">Par exemple, l’extrait de code suivant montre une requête LINQ qui filtre les commandes qui ont été expédiées au cours des trois derniers jours.</span><span class="sxs-lookup"><span data-stu-id="dd117-129">For example, the following snippet shows a LINQ query that filters orders that were shipped in the last three days.</span></span>

    IQueryable<Order> orders = client.CreateDocumentQuery<Order>("/dbs/orderdb/colls/orders")
        .Where(o => o.ShipDate >= DateTime.UtcNow.AddDays(-3));
          
    // Translated to the following SQL statement and executed on Azure Cosmos DB
    SELECT * FROM root WHERE (root["ShipDate"] >= "2016-12-18T21:55:03.45569Z")

<span data-ttu-id="dd117-130">Pour plus d’informations sur le langage de requête SQL d’Azure Cosmos DB et le fournisseur LINQ, consultez [Interrogation de Cosmos DB](documentdb-sql-query.md).</span><span class="sxs-lookup"><span data-stu-id="dd117-130">You can learn more about Azure Cosmos DB's SQL query language and the LINQ provider at [Querying Cosmos DB](documentdb-sql-query.md).</span></span>

<span data-ttu-id="dd117-131">Dans cet article, nous avons vu comment stocker, indexer et interroger les valeurs DateTime dans Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="dd117-131">In this article, we looked at how to store, index, and query DateTimes in Azure Cosmos DB.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dd117-132">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="dd117-132">Next Steps</span></span>
* <span data-ttu-id="dd117-133">Télécharger et exécuter les [exemples de code sur GitHub](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/code-samples)</span><span class="sxs-lookup"><span data-stu-id="dd117-133">Download and run the [Code samples on GitHub](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/code-samples)</span></span>
* <span data-ttu-id="dd117-134">En savoir plus sur les [requêtes d’API DocumentDB](documentdb-sql-query.md)</span><span class="sxs-lookup"><span data-stu-id="dd117-134">Learn more about [DocumentDB API Query](documentdb-sql-query.md)</span></span>
* <span data-ttu-id="dd117-135">En savoir plus sur les [stratégies d’indexation Azure Cosmos DB](indexing-policies.md)</span><span class="sxs-lookup"><span data-stu-id="dd117-135">Learn more about [Azure Cosmos DB Indexing Policies](indexing-policies.md)</span></span>
