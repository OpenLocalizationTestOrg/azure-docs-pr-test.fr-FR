---
title: "aaaWorking avec des dates dans la base de données Azure Cosmos | Documents Microsoft"
description: "Découvrez comment toowork avec des dates dans la base de données Azure Cosmos."
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
ms.openlocfilehash: 27ec170e4bef72c0b5b456738f1275ef02543024
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-dates-in-azure-cosmos-db"></a><span data-ttu-id="4adce-103">Utilisation des dates dans Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="4adce-103">Working with Dates in Azure Cosmos DB</span></span>
<span data-ttu-id="4adce-104">Azure Cosmos DB offre une flexibilité des schémas et une indexation riche par le biais d’un modèle de données [JSON](http://www.json.org) natif.</span><span class="sxs-lookup"><span data-stu-id="4adce-104">Azure Cosmos DB delivers schema flexibility and rich indexing via a native [JSON](http://www.json.org) data model.</span></span> <span data-ttu-id="4adce-105">Toutes les ressources Azure Cosmos DB, y compris les bases de données, les collections, les documents et les procédures stockées, sont modélisées et stockées en tant que documents JSON.</span><span class="sxs-lookup"><span data-stu-id="4adce-105">All Azure Cosmos DB resources including databases, collections, documents, and stored procedures are modeled and stored as JSON documents.</span></span> <span data-ttu-id="4adce-106">Pour être portable, JSON (et Azure Cosmos DB) prend en charge uniquement un petit ensemble de types de base : chaîne, nombre, booléen, tableau, objet et null.</span><span class="sxs-lookup"><span data-stu-id="4adce-106">As a requirement for being portable, JSON (and Azure Cosmos DB) supports only a small set of basic types: String, Number, Boolean, Array, Object, and Null.</span></span> <span data-ttu-id="4adce-107">Toutefois, JSON est flexible et permettre aux développeurs et infrastructures toorepresent types plus complexes à l’aide de ces primitives et les composer en tant qu’objets ou tableaux.</span><span class="sxs-lookup"><span data-stu-id="4adce-107">However, JSON is flexible and allow developers and frameworks toorepresent more complex types using these primitives and composing them as objects or arrays.</span></span> 

<span data-ttu-id="4adce-108">Dans les types de base toohello Ajout, de nombreuses applications doivent hello [DateTime](https://msdn.microsoft.com/library/system.datetime(v=vs.110).aspx) toorepresent dates et les horodateurs de type.</span><span class="sxs-lookup"><span data-stu-id="4adce-108">In addition toohello basic types, many applications need hello [DateTime](https://msdn.microsoft.com/library/system.datetime(v=vs.110).aspx) type toorepresent dates and timestamps.</span></span> <span data-ttu-id="4adce-109">Cet article décrit comment les développeurs peuvent stocker, récupérer et interroger des dates dans la base de données Azure Cosmos à l’aide de hello .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="4adce-109">This article describes how developers can store, retrieve, and query dates in Azure Cosmos DB using hello .NET SDK.</span></span>

## <a name="storing-datetimes"></a><span data-ttu-id="4adce-110">Stockage de valeurs DateTime</span><span class="sxs-lookup"><span data-stu-id="4adce-110">Storing DateTimes</span></span>
<span data-ttu-id="4adce-111">Par défaut, hello [Azure Cosmos DB SDK](documentdb-sdk-dotnet.md) sérialise les valeurs DateTime en tant que [ISO 8601](http://www.iso.org/iso/catalogue_detail?csnumber=40874) chaînes.</span><span class="sxs-lookup"><span data-stu-id="4adce-111">By default, hello [Azure Cosmos DB SDK](documentdb-sdk-dotnet.md) serializes DateTime values as [ISO 8601](http://www.iso.org/iso/catalogue_detail?csnumber=40874) strings.</span></span> <span data-ttu-id="4adce-112">La plupart des applications permettent représentation de chaîne par défaut hello pour DateTime pour hello suivant raisons :</span><span class="sxs-lookup"><span data-stu-id="4adce-112">Most applications can use hello default string representation for DateTime for hello following reasons:</span></span>

* <span data-ttu-id="4adce-113">Chaînes peuvent être comparées et hello relatif de classement des valeurs de date/heure hello est conservée lorsqu’elles sont transformées toostrings.</span><span class="sxs-lookup"><span data-stu-id="4adce-113">Strings can be compared, and hello relative ordering of hello DateTime values is preserved when they are transformed toostrings.</span></span> 
* <span data-ttu-id="4adce-114">Cette approche ne nécessite pas de code personnalisé ou d’attributs pour la conversion JSON.</span><span class="sxs-lookup"><span data-stu-id="4adce-114">This approach doesn't require any custom code or attributes for JSON conversion.</span></span>
* <span data-ttu-id="4adce-115">dates Hello stocké dans JSON sont lisibles.</span><span class="sxs-lookup"><span data-stu-id="4adce-115">hello dates as stored in JSON are human readable.</span></span>
* <span data-ttu-id="4adce-116">Cette approche peut tirer parti de l’index d’Azure Cosmos DB pour offrir des performances de requête rapides.</span><span class="sxs-lookup"><span data-stu-id="4adce-116">This approach can take advantage of Azure Cosmos DB's index for fast query performance.</span></span>

<span data-ttu-id="4adce-117">Hello, par exemple, après les magasins de l’extrait de code une `Order` de l’objet contenant deux propriétés DateTime - `ShipDate` et `OrderDate` sous forme de document à l’aide de hello .NET SDK :</span><span class="sxs-lookup"><span data-stu-id="4adce-117">For example, hello following snippet stores an `Order` object containing two DateTime properties - `ShipDate` and `OrderDate` as a document using hello .NET SDK:</span></span>

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

<span data-ttu-id="4adce-118">Ce document est stocké dans Azure Cosmos DB comme suit :</span><span class="sxs-lookup"><span data-stu-id="4adce-118">This document is stored in Azure Cosmos DB as follows:</span></span>

    {
        "id": "09152014101",
        "OrderDate": "2014-09-15T23:14:25.7251173Z",
        "ShipDate": "2014-09-30T23:14:25.7251173Z",
        "Total": 113.39
    }
    

<span data-ttu-id="4adce-119">Ou bien, vous pouvez stocker les dates/heures comme Unix horodateurs, autrement dit, en tant que nombre représentant le nombre de hello de secondes écoulées depuis le 1er janvier 1970.</span><span class="sxs-lookup"><span data-stu-id="4adce-119">Alternatively, you can store DateTimes as Unix timestamps, that is, as a number representing hello number of elapsed seconds since January 1, 1970.</span></span> <span data-ttu-id="4adce-120">La propriété Timestamp interne d’Azure Cosmos DB (`_ts`) suit cette approche.</span><span class="sxs-lookup"><span data-stu-id="4adce-120">Azure Cosmos DB's internal Timestamp (`_ts`) property follows this approach.</span></span> <span data-ttu-id="4adce-121">Vous pouvez utiliser hello [UnixDateTimeConverter](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.unixdatetimeconverter.aspx) classe tooserialize dates/heures comme des nombres.</span><span class="sxs-lookup"><span data-stu-id="4adce-121">You can use hello [UnixDateTimeConverter](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.unixdatetimeconverter.aspx) class tooserialize DateTimes as numbers.</span></span> 

## <a name="indexing-datetimes-for-range-queries"></a><span data-ttu-id="4adce-122">Indexation des valeurs DateTime pour les requêtes de plage</span><span class="sxs-lookup"><span data-stu-id="4adce-122">Indexing DateTimes for range queries</span></span>
<span data-ttu-id="4adce-123">Les requêtes de plage ont souvent des valeurs DateTime.</span><span class="sxs-lookup"><span data-stu-id="4adce-123">Range queries are common with DateTime values.</span></span> <span data-ttu-id="4adce-124">Par exemple, si vous devez toofind toutes les commandes créées depuis hier ou recherchez toutes les commandes livrées Bonjour cinq dernières minutes, vous devez tooperform les requêtes de plage.</span><span class="sxs-lookup"><span data-stu-id="4adce-124">For example, if you need toofind all orders created since yesterday, or find all orders shipped in hello last five minutes, you need tooperform range queries.</span></span> <span data-ttu-id="4adce-125">tooexecute ces requêtes efficacement, vous devez configurer votre collection pour l’indexation de plage sur les chaînes.</span><span class="sxs-lookup"><span data-stu-id="4adce-125">tooexecute these queries efficiently, you must configure your collection for Range indexing on strings.</span></span>

    DocumentCollection collection = new DocumentCollection { Id = "orders" };
    collection.IndexingPolicy = new IndexingPolicy(new RangeIndex(DataType.String) { Precision = -1 });
    await client.CreateDocumentCollectionAsync("/dbs/orderdb", collection);

<span data-ttu-id="4adce-126">Vous pouvez apprendre tooconfigure stratégies au niveau d’indexation [stratégies de l’indexation de base de données Azure Cosmos](indexing-policies.md).</span><span class="sxs-lookup"><span data-stu-id="4adce-126">You can learn more about how tooconfigure indexing policies at [Azure Cosmos DB Indexing Policies](indexing-policies.md).</span></span>

## <a name="querying-datetimes-in-linq"></a><span data-ttu-id="4adce-127">Interrogation des valeurs DateTime dans LINQ</span><span class="sxs-lookup"><span data-stu-id="4adce-127">Querying DateTimes in LINQ</span></span>
<span data-ttu-id="4adce-128">Hello DocumentDB .NET SDK prend automatiquement en charge l’interrogation des données stockées dans la base de données Azure Cosmos via LINQ.</span><span class="sxs-lookup"><span data-stu-id="4adce-128">hello DocumentDB .NET SDK automatically supports querying data stored in Azure Cosmos DB via LINQ.</span></span> <span data-ttu-id="4adce-129">Par exemple, hello extrait de code suivant montre une requête LINQ qui classe les filtres qui ont été expédiées hello trois derniers jours.</span><span class="sxs-lookup"><span data-stu-id="4adce-129">For example, hello following snippet shows a LINQ query that filters orders that were shipped in hello last three days.</span></span>

    IQueryable<Order> orders = client.CreateDocumentQuery<Order>("/dbs/orderdb/colls/orders")
        .Where(o => o.ShipDate >= DateTime.UtcNow.AddDays(-3));
          
    // Translated toohello following SQL statement and executed on Azure Cosmos DB
    SELECT * FROM root WHERE (root["ShipDate"] >= "2016-12-18T21:55:03.45569Z")

<span data-ttu-id="4adce-130">Plus d’informations sur langage et hello LINQ fournisseur de requêtes SQL du Azure Cosmos base de données à [base de données Cosmos interrogation](documentdb-sql-query.md).</span><span class="sxs-lookup"><span data-stu-id="4adce-130">You can learn more about Azure Cosmos DB's SQL query language and hello LINQ provider at [Querying Cosmos DB](documentdb-sql-query.md).</span></span>

<span data-ttu-id="4adce-131">Dans cet article, nous avons examiné comment toostore, index et interroger des dates/heures dans la base de données Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="4adce-131">In this article, we looked at how toostore, index, and query DateTimes in Azure Cosmos DB.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4adce-132">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4adce-132">Next Steps</span></span>
* <span data-ttu-id="4adce-133">Téléchargez et exécutez hello [exemples sur GitHub de Code](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/code-samples)</span><span class="sxs-lookup"><span data-stu-id="4adce-133">Download and run hello [Code samples on GitHub](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/code-samples)</span></span>
* <span data-ttu-id="4adce-134">En savoir plus sur les [requêtes d’API DocumentDB](documentdb-sql-query.md)</span><span class="sxs-lookup"><span data-stu-id="4adce-134">Learn more about [DocumentDB API Query](documentdb-sql-query.md)</span></span>
* <span data-ttu-id="4adce-135">En savoir plus sur les [stratégies d’indexation Azure Cosmos DB](indexing-policies.md)</span><span class="sxs-lookup"><span data-stu-id="4adce-135">Learn more about [Azure Cosmos DB Indexing Policies](indexing-policies.md)</span></span>
