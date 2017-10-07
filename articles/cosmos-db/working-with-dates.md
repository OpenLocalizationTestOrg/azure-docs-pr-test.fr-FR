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
# <a name="working-with-dates-in-azure-cosmos-db"></a>Utilisation des dates dans Azure Cosmos DB
Azure Cosmos DB offre une flexibilité des schémas et une indexation riche par le biais d’un modèle de données [JSON](http://www.json.org) natif. Toutes les ressources Azure Cosmos DB, y compris les bases de données, les collections, les documents et les procédures stockées, sont modélisées et stockées en tant que documents JSON. Pour être portable, JSON (et Azure Cosmos DB) prend en charge uniquement un petit ensemble de types de base : chaîne, nombre, booléen, tableau, objet et null. Toutefois, JSON est flexible et permettre aux développeurs et infrastructures toorepresent types plus complexes à l’aide de ces primitives et les composer en tant qu’objets ou tableaux. 

Dans les types de base toohello Ajout, de nombreuses applications doivent hello [DateTime](https://msdn.microsoft.com/library/system.datetime(v=vs.110).aspx) toorepresent dates et les horodateurs de type. Cet article décrit comment les développeurs peuvent stocker, récupérer et interroger des dates dans la base de données Azure Cosmos à l’aide de hello .NET SDK.

## <a name="storing-datetimes"></a>Stockage de valeurs DateTime
Par défaut, hello [Azure Cosmos DB SDK](documentdb-sdk-dotnet.md) sérialise les valeurs DateTime en tant que [ISO 8601](http://www.iso.org/iso/catalogue_detail?csnumber=40874) chaînes. La plupart des applications permettent représentation de chaîne par défaut hello pour DateTime pour hello suivant raisons :

* Chaînes peuvent être comparées et hello relatif de classement des valeurs de date/heure hello est conservée lorsqu’elles sont transformées toostrings. 
* Cette approche ne nécessite pas de code personnalisé ou d’attributs pour la conversion JSON.
* dates Hello stocké dans JSON sont lisibles.
* Cette approche peut tirer parti de l’index d’Azure Cosmos DB pour offrir des performances de requête rapides.

Hello, par exemple, après les magasins de l’extrait de code une `Order` de l’objet contenant deux propriétés DateTime - `ShipDate` et `OrderDate` sous forme de document à l’aide de hello .NET SDK :

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

Ce document est stocké dans Azure Cosmos DB comme suit :

    {
        "id": "09152014101",
        "OrderDate": "2014-09-15T23:14:25.7251173Z",
        "ShipDate": "2014-09-30T23:14:25.7251173Z",
        "Total": 113.39
    }
    

Ou bien, vous pouvez stocker les dates/heures comme Unix horodateurs, autrement dit, en tant que nombre représentant le nombre de hello de secondes écoulées depuis le 1er janvier 1970. La propriété Timestamp interne d’Azure Cosmos DB (`_ts`) suit cette approche. Vous pouvez utiliser hello [UnixDateTimeConverter](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.unixdatetimeconverter.aspx) classe tooserialize dates/heures comme des nombres. 

## <a name="indexing-datetimes-for-range-queries"></a>Indexation des valeurs DateTime pour les requêtes de plage
Les requêtes de plage ont souvent des valeurs DateTime. Par exemple, si vous devez toofind toutes les commandes créées depuis hier ou recherchez toutes les commandes livrées Bonjour cinq dernières minutes, vous devez tooperform les requêtes de plage. tooexecute ces requêtes efficacement, vous devez configurer votre collection pour l’indexation de plage sur les chaînes.

    DocumentCollection collection = new DocumentCollection { Id = "orders" };
    collection.IndexingPolicy = new IndexingPolicy(new RangeIndex(DataType.String) { Precision = -1 });
    await client.CreateDocumentCollectionAsync("/dbs/orderdb", collection);

Vous pouvez apprendre tooconfigure stratégies au niveau d’indexation [stratégies de l’indexation de base de données Azure Cosmos](indexing-policies.md).

## <a name="querying-datetimes-in-linq"></a>Interrogation des valeurs DateTime dans LINQ
Hello DocumentDB .NET SDK prend automatiquement en charge l’interrogation des données stockées dans la base de données Azure Cosmos via LINQ. Par exemple, hello extrait de code suivant montre une requête LINQ qui classe les filtres qui ont été expédiées hello trois derniers jours.

    IQueryable<Order> orders = client.CreateDocumentQuery<Order>("/dbs/orderdb/colls/orders")
        .Where(o => o.ShipDate >= DateTime.UtcNow.AddDays(-3));
          
    // Translated toohello following SQL statement and executed on Azure Cosmos DB
    SELECT * FROM root WHERE (root["ShipDate"] >= "2016-12-18T21:55:03.45569Z")

Plus d’informations sur langage et hello LINQ fournisseur de requêtes SQL du Azure Cosmos base de données à [base de données Cosmos interrogation](documentdb-sql-query.md).

Dans cet article, nous avons examiné comment toostore, index et interroger des dates/heures dans la base de données Azure Cosmos.

## <a name="next-steps"></a>Étapes suivantes
* Téléchargez et exécutez hello [exemples sur GitHub de Code](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/code-samples)
* En savoir plus sur les [requêtes d’API DocumentDB](documentdb-sql-query.md)
* En savoir plus sur les [stratégies d’indexation Azure Cosmos DB](indexing-policies.md)
