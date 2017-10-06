---
title: "aaaHow tooquery les données de table dans la base de données Azure Cosmos ? | Microsoft Docs"
description: "En savoir plus les données de la table dans la base de données Azure Cosmos tooquery"
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
ms.openlocfilehash: 32526c3488c589c5be3a4a2f174aa769570f0c0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-how-tooquery-table-data-by-using-hello-table-api-preview"></a>Azure Cosmos DB : Comment tooquery les données de table à l’aide de hello API (version préliminaire) de la Table ?

Bonjour Azure Cosmos DB [Table API](table-introduction.md) (version préliminaire) prend en charge OData et [LINQ](https://docs.microsoft.com/rest/api/storageservices/fileservices/writing-linq-queries-against-the-table-service) requêtes sur les données de clé/valeur (table).  

Cet article traite des hello tâches suivantes : 

> [!div class="checklist"]
> * Interrogation des données avec hello API de Table

Hello dans cet article, les requêtes utilisent hello suivant exemple `People` table :

| PartitionKey | RowKey | Email | PhoneNumber |
| --- | --- | --- | --- |
| Harp | Walter | Walter@contoso.com| 425-555-0101 |
| Smith | Ben | Ben@contoso.com| 425-555-0102 |
| Smith | Jeff | Jeff@contoso.com| 425-555-0104 | 

Base de données Azure Cosmos étant compatible avec hello API de stockage de Table Azure, consultez [interrogation de Tables et entités] (https://docs.microsoft.com/rest/api/storageservices/fileservices/querying-tables-and-entities) pour plus d’informations sur comment tooquery à l’aide de hello API de table. 

Pour plus d’informations sur les fonctions hello premium offre de base de données Azure Cosmos, consultez [base de données Azure Cosmos : API de Table](table-introduction.md) et [développer avec hello API de Table dans .NET](tutorial-develop-table-dotnet.md). 

## <a name="prerequisites"></a>Composants requis

Pour ces requêtes toowork, vous devez disposer d’un compte de base de données Azure Cosmos et données d’entité dans le conteneur de hello. Cela n’est pas le cas ? Hello complète [démarrage rapide de cinq minutes](https://aka.ms/acdbtnetqs) ou hello [didacticiel pour développeur](https://aka.ms/acdbtabletut) toocreate un compte et le remplir votre base de données.

## <a name="query-on-partitionkey-and-rowkey"></a>Interroger sur PartitionKey et RowKey
Étant donné que les propriétés PartitionKey et RowKey hello forment la clé primaire d’une entité, vous pouvez utiliser hello suivant l’entité de hello tooidentify une syntaxe spéciale : 

**Requête**

```
https://<mytableendpoint>/People(PartitionKey='Harp',RowKey='Walter')  
```
**Résultats**

| PartitionKey | RowKey | Email | PhoneNumber |
| --- | --- | --- | --- |
| Harp | Walter | Walter@contoso.com| 425-555-0104 |

Vous pouvez également spécifier ces propriétés dans le cadre de hello `$filter` option, comme indiqué dans hello suivant la section. Notez que les noms de propriété de clé hello et les valeurs de constante respectent la casse. Hello PartitionKey et RowKey propriétés sont de type chaîne. 

## <a name="query-by-using-an-odata-filter"></a>Interroger en utilisant un filtre OData
Quand vous construisez une chaîne de filtrage, prenez en compte les règles suivantes : 

* Utilisez les opérateurs logiques hello définis par hello spécification du protocole OData toocompare une valeur de la propriété tooa. Notez que vous ne peut pas comparer une valeur dynamique tooa de propriété. Côté « un » de l’expression de hello doit être une constante. 
* nom de la propriété Hello, opérateur et valeur de constante doivent être séparés par des espaces encodés URL. Un espace est codé URL sous la forme `%20`. 
* Toutes les parties de la chaîne de filtrage hello respectent la casse. 
* valeur de constante Hello doit être de hello même type de propriété hello dans l’ordre des résultats valides de hello filtre tooreturn. Pour plus d’informations sur les types de propriété pris en charge, consultez [hello de présentation des modèle de données de Service de Table](https://docs.microsoft.com/rest/api/storageservices/understanding-the-table-service-data-model). 

Voici un exemple de requête qui montre comment toofilter par hello PartitionKey et propriétés de courrier électronique à l’aide d’un OData `$filter`.

**Requête**

```
https://<mytableapi-endpoint>/People()?$filter=PartitionKey%20eq%20'Smith'%20and%20Email%20eq%20'Ben@contoso.com'
```

Pour plus d’informations sur la façon dont les expressions pour différents types de données de filtre de tooconstruct, consultez [interrogeant les Tables et les entités](https://docs.microsoft.com/rest/api/storageservices/querying-tables-and-entities).

**Résultats**

| PartitionKey | RowKey | Email | PhoneNumber |
| --- | --- | --- | --- |
| Ben |Smith | Ben@contoso.com| 425-555-0102 |

## <a name="query-by-using-linq"></a>Interroger en utilisant LINQ 
Vous pouvez également interroger à l’aide de LINQ, ce qui se traduit par des expressions de requête OData toohello correspondantes. Voici un exemple de comment toobuild des requêtes à l’aide de hello .NET SDK :

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

Dans ce didacticiel, vous avez effectué les éléments suivants de hello :

> [!div class="checklist"]
> * Appris comment tooquery à l’aide de hello API de Table (version préliminaire) 

Vous pouvez maintenant toolearn de didacticiel suivant toohello comment toodistribute vos données globalement.

> [!div class="nextstepaction"]
> [Distribuer vos données globalement](tutorial-global-distribution-documentdb.md)
