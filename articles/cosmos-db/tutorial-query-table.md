---
title: "Comment interroger des données de table dans Azure Cosmos DB ? | Microsoft Docs"
description: "Apprendre à interroger des données de table dans Azure Cosmos DB"
services: cosmos-db
documentationcenter: 
author: kanshiG
manager: jhubbard
editor: 
tags: 
ms.assetid: 14bcb94e-583c-46f7-9ea8-db010eb2ab43
ms.service: cosmos-db
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 05/10/2017
ms.author: govindk
ms.openlocfilehash: e59cfa85c6bf584e44bdc6e88cc19d67df390041
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-cosmos-db-how-to-query-table-data-by-using-the-table-api-preview"></a>Azure Cosmos DB : Comment interroger les données d’une table avec l’API Table (préversion) ?

L’[API de table](table-introduction.md) d’Azure Cosmos DB (version préliminaire) prend en charge les requêtes OData et [LINQ](https://docs.microsoft.com/rest/api/storageservices/fileservices/writing-linq-queries-against-the-table-service) requêtes sur des données de clé/valeur (table).  

Cet article décrit les tâches suivantes : 

> [!div class="checklist"]
> * Interrogation des données avec l’API de table

L’exemple de table `People` suivant est utilisé pour les interrogations de cet article :

| PartitionKey | RowKey | Email | PhoneNumber |
| --- | --- | --- | --- |
| Harp | Walter | Walter@contoso.com| 425-555-0101 |
| Smith | Ben | Ben@contoso.com| 425-555-0102 |
| Smith | Jeff | Jeff@contoso.com| 425-555-0104 | 

Azure Cosmos DB étant compatible avec les API d’Azure Stockage Table, consultez [Querying Tables and Entities] (https://docs.microsoft.com/rest/api/storageservices/fileservices/querying-tables-and-entities) pour plus d’informations sur la manière d’effectuer des interrogations avec l’API Table. 

Pour plus d’informations sur les fonctionnalités étendues offertes par Azure Cosmos DB, consultez [Azure Cosmos DB : API Table](table-introduction.md) et [Développer avec l’API Table en utilisant .NET](tutorial-develop-table-dotnet.md). 

## <a name="prerequisites"></a>Composants requis

Pour le bon fonctionnement de ces requêtes, vous devez disposer d’un compte Azure Cosmos DB et de données d’entité dans le conteneur. Cela n’est pas le cas ? Lancez le [démarrage rapide en 5 minutes](https://aka.ms/acdbtnetqs) ou le [didacticiel destiné aux développeurs](https://aka.ms/acdbtabletut) pour créer un compte et alimenter votre base de données.

## <a name="query-on-partitionkey-and-rowkey"></a>Interroger sur PartitionKey et RowKey
Les propriétés PartitionKey et RowKey formant une clé primaire d’une entité, vous pouvez utiliser la syntaxe spéciale suivante pour identifier l’entité : 

**Requête**

```
https://<mytableendpoint>/People(PartitionKey='Harp',RowKey='Walter')  
```
**Résultats**

| PartitionKey | RowKey | Email | PhoneNumber |
| --- | --- | --- | --- |
| Harp | Walter | Walter@contoso.com| 425-555-0104 |

Vous pouvez également spécifier ces propriétés dans le cadre de l’option `$filter`, comme indiqué dans la section suivante. Notez que les noms de propriété de clé et les valeurs de constante respectent la casse. Les propriétés PartitionKey et RowKey sont de type chaîne. 

## <a name="query-by-using-an-odata-filter"></a>Interroger en utilisant un filtre OData
Quand vous construisez une chaîne de filtrage, prenez en compte les règles suivantes : 

* Utilisez les opérateurs logiques définis par la spécification du protocole OData Protocol pour comparer une propriété par rapport à une valeur. Notez que vous ne pouvez pas comparer une propriété à une valeur dynamique. Un côté de l’expression doit être une constante. 
* Le nom de la propriété, l’opérateur et la valeur de constante doivent être séparés par des espaces codés URL. Un espace est codé URL sous la forme `%20`. 
* Toutes les parties de la chaîne de filtrage respectent la casse. 
* Pour que le filtre retourne des résultats valides, la valeur constante doit être du même type de données que la propriété. Pour plus d’informations sur les types de propriétés pris en charge, consultez [Présentation du modèle de données du service de Table](https://docs.microsoft.com/rest/api/storageservices/understanding-the-table-service-data-model). 

Voici un exemple de requête qui montre comment filtrer sur les propriétés PartitionKey et Email en utilisant un `$filter` OData.

**Requête**

```
https://<mytableapi-endpoint>/People()?$filter=PartitionKey%20eq%20'Smith'%20and%20Email%20eq%20'Ben@contoso.com'
```

Pour plus d’informations sur la construction d’expressions de filtre pour différents types de données, consultez [Querying Tables and Entities](https://docs.microsoft.com/rest/api/storageservices/querying-tables-and-entities).

**Résultats**

| PartitionKey | RowKey | Email | PhoneNumber |
| --- | --- | --- | --- |
| Ben |Smith | Ben@contoso.com| 425-555-0102 |

## <a name="query-by-using-linq"></a>Interroger en utilisant LINQ 
Vous pouvez également interroger en utilisant LINQ, qui est traduit en expressions de requête OData correspondantes. Voici un exemple montrant comment créer des requêtes en utilisant le SDK .NET :

```csharp
CloudTableClient tableClient = account.CreateCloudTableClient();
CloudTable table = tableClient.GetTableReference("people");

TableQuery<CustomerEntity> query = new TableQuery<CustomerEntity>()
    .Where(
        TableQuery.CombineFilters(
            TableQuery.GenerateFilterCondition(PartitionKey, QueryComparisons.Equal, "Smith"),
            TableOperators.And,
            TableQuery.GenerateFilterCondition(Email, QueryComparisons.Equal,"Ben@contoso.com")
    ));

await table.ExecuteQuerySegmentedAsync<CustomerEntity>(query, null);
```

## <a name="next-steps"></a>Étapes suivantes

Dans ce didacticiel, vous avez effectué les tâches suivantes :

> [!div class="checklist"]
> * Découvrez comment interroger en utilisant l’API Table (préversion) 

Vous pouvez maintenant poursuivre avec le didacticiel suivant montrant comment distribuer vos données globalement.

> [!div class="nextstepaction"]
> [Distribuer vos données globalement](tutorial-global-distribution-documentdb.md)
