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
# <a name="azure-cosmos-db-how-to-query-table-data-by-using-the-table-api-preview"></a><span data-ttu-id="215f1-104">Azure Cosmos DB : Comment interroger les données d’une table avec l’API Table (préversion) ?</span><span class="sxs-lookup"><span data-stu-id="215f1-104">Azure Cosmos DB: How to query table data by using the Table API (preview)?</span></span>

<span data-ttu-id="215f1-105">L’[API de table](table-introduction.md) d’Azure Cosmos DB (version préliminaire) prend en charge les requêtes OData et [LINQ](https://docs.microsoft.com/rest/api/storageservices/fileservices/writing-linq-queries-against-the-table-service) requêtes sur des données de clé/valeur (table).</span><span class="sxs-lookup"><span data-stu-id="215f1-105">The Azure Cosmos DB [Table API](table-introduction.md) (preview) supports OData and [LINQ](https://docs.microsoft.com/rest/api/storageservices/fileservices/writing-linq-queries-against-the-table-service) queries against key/value (table) data.</span></span>  

<span data-ttu-id="215f1-106">Cet article décrit les tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="215f1-106">This article covers the following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="215f1-107">Interrogation des données avec l’API de table</span><span class="sxs-lookup"><span data-stu-id="215f1-107">Querying data with the Table API</span></span>

<span data-ttu-id="215f1-108">L’exemple de table `People` suivant est utilisé pour les interrogations de cet article :</span><span class="sxs-lookup"><span data-stu-id="215f1-108">The queries in this article use the following sample `People` table:</span></span>

| <span data-ttu-id="215f1-109">PartitionKey</span><span class="sxs-lookup"><span data-stu-id="215f1-109">PartitionKey</span></span> | <span data-ttu-id="215f1-110">RowKey</span><span class="sxs-lookup"><span data-stu-id="215f1-110">RowKey</span></span> | <span data-ttu-id="215f1-111">Email</span><span class="sxs-lookup"><span data-stu-id="215f1-111">Email</span></span> | <span data-ttu-id="215f1-112">PhoneNumber</span><span class="sxs-lookup"><span data-stu-id="215f1-112">PhoneNumber</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="215f1-113">Harp</span><span class="sxs-lookup"><span data-stu-id="215f1-113">Harp</span></span> | <span data-ttu-id="215f1-114">Walter</span><span class="sxs-lookup"><span data-stu-id="215f1-114">Walter</span></span> | Walter@contoso.com| <span data-ttu-id="215f1-115">425-555-0101</span><span class="sxs-lookup"><span data-stu-id="215f1-115">425-555-0101</span></span> |
| <span data-ttu-id="215f1-116">Smith</span><span class="sxs-lookup"><span data-stu-id="215f1-116">Smith</span></span> | <span data-ttu-id="215f1-117">Ben</span><span class="sxs-lookup"><span data-stu-id="215f1-117">Ben</span></span> | Ben@contoso.com| <span data-ttu-id="215f1-118">425-555-0102</span><span class="sxs-lookup"><span data-stu-id="215f1-118">425-555-0102</span></span> |
| <span data-ttu-id="215f1-119">Smith</span><span class="sxs-lookup"><span data-stu-id="215f1-119">Smith</span></span> | <span data-ttu-id="215f1-120">Jeff</span><span class="sxs-lookup"><span data-stu-id="215f1-120">Jeff</span></span> | Jeff@contoso.com| <span data-ttu-id="215f1-121">425-555-0104</span><span class="sxs-lookup"><span data-stu-id="215f1-121">425-555-0104</span></span> | 

<span data-ttu-id="215f1-122">Azure Cosmos DB étant compatible avec les API d’Azure Stockage Table, consultez [Querying Tables and Entities] (https://docs.microsoft.com/rest/api/storageservices/fileservices/querying-tables-and-entities) pour plus d’informations sur la manière d’effectuer des interrogations avec l’API Table.</span><span class="sxs-lookup"><span data-stu-id="215f1-122">Because Azure Cosmos DB is compatible with the Azure Table storage APIs, see [Querying Tables and Entities] (https://docs.microsoft.com/rest/api/storageservices/fileservices/querying-tables-and-entities) for details on how to query by using the Table API.</span></span> 

<span data-ttu-id="215f1-123">Pour plus d’informations sur les fonctionnalités étendues offertes par Azure Cosmos DB, consultez [Azure Cosmos DB : API Table](table-introduction.md) et [Développer avec l’API Table en utilisant .NET](tutorial-develop-table-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="215f1-123">For more information on the premium capabilities that Azure Cosmos DB offers, see [Azure Cosmos DB: Table API](table-introduction.md) and [Develop with the Table API in .NET](tutorial-develop-table-dotnet.md).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="215f1-124">Composants requis</span><span class="sxs-lookup"><span data-stu-id="215f1-124">Prerequisites</span></span>

<span data-ttu-id="215f1-125">Pour le bon fonctionnement de ces requêtes, vous devez disposer d’un compte Azure Cosmos DB et de données d’entité dans le conteneur.</span><span class="sxs-lookup"><span data-stu-id="215f1-125">For these queries to work, you must have an Azure Cosmos DB account and have entity data in the container.</span></span> <span data-ttu-id="215f1-126">Cela n’est pas le cas ?</span><span class="sxs-lookup"><span data-stu-id="215f1-126">Don't have any of those?</span></span> <span data-ttu-id="215f1-127">Lancez le [démarrage rapide en 5 minutes](https://aka.ms/acdbtnetqs) ou le [didacticiel destiné aux développeurs](https://aka.ms/acdbtabletut) pour créer un compte et alimenter votre base de données.</span><span class="sxs-lookup"><span data-stu-id="215f1-127">Complete the [five-minute quickstart](https://aka.ms/acdbtnetqs) or the [developer tutorial](https://aka.ms/acdbtabletut) to create an account and populate your database.</span></span>

## <a name="query-on-partitionkey-and-rowkey"></a><span data-ttu-id="215f1-128">Interroger sur PartitionKey et RowKey</span><span class="sxs-lookup"><span data-stu-id="215f1-128">Query on PartitionKey and RowKey</span></span>
<span data-ttu-id="215f1-129">Les propriétés PartitionKey et RowKey formant une clé primaire d’une entité, vous pouvez utiliser la syntaxe spéciale suivante pour identifier l’entité :</span><span class="sxs-lookup"><span data-stu-id="215f1-129">Because the PartitionKey and RowKey properties form an entity's primary key, you can use the following special syntax to identify the entity:</span></span> 

<span data-ttu-id="215f1-130">**Requête**</span><span class="sxs-lookup"><span data-stu-id="215f1-130">**Query**</span></span>

```
https://<mytableendpoint>/People(PartitionKey='Harp',RowKey='Walter')  
```
<span data-ttu-id="215f1-131">**Résultats**</span><span class="sxs-lookup"><span data-stu-id="215f1-131">**Results**</span></span>

| <span data-ttu-id="215f1-132">PartitionKey</span><span class="sxs-lookup"><span data-stu-id="215f1-132">PartitionKey</span></span> | <span data-ttu-id="215f1-133">RowKey</span><span class="sxs-lookup"><span data-stu-id="215f1-133">RowKey</span></span> | <span data-ttu-id="215f1-134">Email</span><span class="sxs-lookup"><span data-stu-id="215f1-134">Email</span></span> | <span data-ttu-id="215f1-135">PhoneNumber</span><span class="sxs-lookup"><span data-stu-id="215f1-135">PhoneNumber</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="215f1-136">Harp</span><span class="sxs-lookup"><span data-stu-id="215f1-136">Harp</span></span> | <span data-ttu-id="215f1-137">Walter</span><span class="sxs-lookup"><span data-stu-id="215f1-137">Walter</span></span> | Walter@contoso.com| <span data-ttu-id="215f1-138">425-555-0104</span><span class="sxs-lookup"><span data-stu-id="215f1-138">425-555-0104</span></span> |

<span data-ttu-id="215f1-139">Vous pouvez également spécifier ces propriétés dans le cadre de l’option `$filter`, comme indiqué dans la section suivante.</span><span class="sxs-lookup"><span data-stu-id="215f1-139">Alternatively, you can specify these properties as part of the `$filter` option, as shown in the following section.</span></span> <span data-ttu-id="215f1-140">Notez que les noms de propriété de clé et les valeurs de constante respectent la casse.</span><span class="sxs-lookup"><span data-stu-id="215f1-140">Note that the key property names and constant values are case-sensitive.</span></span> <span data-ttu-id="215f1-141">Les propriétés PartitionKey et RowKey sont de type chaîne.</span><span class="sxs-lookup"><span data-stu-id="215f1-141">Both the PartitionKey and RowKey properties are of type String.</span></span> 

## <a name="query-by-using-an-odata-filter"></a><span data-ttu-id="215f1-142">Interroger en utilisant un filtre OData</span><span class="sxs-lookup"><span data-stu-id="215f1-142">Query by using an OData filter</span></span>
<span data-ttu-id="215f1-143">Quand vous construisez une chaîne de filtrage, prenez en compte les règles suivantes :</span><span class="sxs-lookup"><span data-stu-id="215f1-143">When you're constructing a filter string, keep these rules in mind:</span></span> 

* <span data-ttu-id="215f1-144">Utilisez les opérateurs logiques définis par la spécification du protocole OData Protocol pour comparer une propriété par rapport à une valeur.</span><span class="sxs-lookup"><span data-stu-id="215f1-144">Use the logical operators defined by the OData Protocol Specification to compare a property to a value.</span></span> <span data-ttu-id="215f1-145">Notez que vous ne pouvez pas comparer une propriété à une valeur dynamique.</span><span class="sxs-lookup"><span data-stu-id="215f1-145">Note that you can't compare a property to a dynamic value.</span></span> <span data-ttu-id="215f1-146">Un côté de l’expression doit être une constante.</span><span class="sxs-lookup"><span data-stu-id="215f1-146">One side of the expression must be a constant.</span></span> 
* <span data-ttu-id="215f1-147">Le nom de la propriété, l’opérateur et la valeur de constante doivent être séparés par des espaces codés URL.</span><span class="sxs-lookup"><span data-stu-id="215f1-147">The property name, operator, and constant value must be separated by URL-encoded spaces.</span></span> <span data-ttu-id="215f1-148">Un espace est codé URL sous la forme `%20`.</span><span class="sxs-lookup"><span data-stu-id="215f1-148">A space is URL-encoded as `%20`.</span></span> 
* <span data-ttu-id="215f1-149">Toutes les parties de la chaîne de filtrage respectent la casse.</span><span class="sxs-lookup"><span data-stu-id="215f1-149">All parts of the filter string are case-sensitive.</span></span> 
* <span data-ttu-id="215f1-150">Pour que le filtre retourne des résultats valides, la valeur constante doit être du même type de données que la propriété.</span><span class="sxs-lookup"><span data-stu-id="215f1-150">The constant value must be of the same data type as the property in order for the filter to return valid results.</span></span> <span data-ttu-id="215f1-151">Pour plus d’informations sur les types de propriétés pris en charge, consultez [Présentation du modèle de données du service de Table](https://docs.microsoft.com/rest/api/storageservices/understanding-the-table-service-data-model).</span><span class="sxs-lookup"><span data-stu-id="215f1-151">For more information about supported property types, see [Understanding the Table Service Data Model](https://docs.microsoft.com/rest/api/storageservices/understanding-the-table-service-data-model).</span></span> 

<span data-ttu-id="215f1-152">Voici un exemple de requête qui montre comment filtrer sur les propriétés PartitionKey et Email en utilisant un `$filter` OData.</span><span class="sxs-lookup"><span data-stu-id="215f1-152">Here's an example query that shows how to filter by the PartitionKey and Email properties by using an OData `$filter`.</span></span>

<span data-ttu-id="215f1-153">**Requête**</span><span class="sxs-lookup"><span data-stu-id="215f1-153">**Query**</span></span>

```
https://<mytableapi-endpoint>/People()?$filter=PartitionKey%20eq%20'Smith'%20and%20Email%20eq%20'Ben@contoso.com'
```

<span data-ttu-id="215f1-154">Pour plus d’informations sur la construction d’expressions de filtre pour différents types de données, consultez [Querying Tables and Entities](https://docs.microsoft.com/rest/api/storageservices/querying-tables-and-entities).</span><span class="sxs-lookup"><span data-stu-id="215f1-154">For more information on how to construct filter expressions for various data types, see [Querying Tables and Entities](https://docs.microsoft.com/rest/api/storageservices/querying-tables-and-entities).</span></span>

<span data-ttu-id="215f1-155">**Résultats**</span><span class="sxs-lookup"><span data-stu-id="215f1-155">**Results**</span></span>

| <span data-ttu-id="215f1-156">PartitionKey</span><span class="sxs-lookup"><span data-stu-id="215f1-156">PartitionKey</span></span> | <span data-ttu-id="215f1-157">RowKey</span><span class="sxs-lookup"><span data-stu-id="215f1-157">RowKey</span></span> | <span data-ttu-id="215f1-158">Email</span><span class="sxs-lookup"><span data-stu-id="215f1-158">Email</span></span> | <span data-ttu-id="215f1-159">PhoneNumber</span><span class="sxs-lookup"><span data-stu-id="215f1-159">PhoneNumber</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="215f1-160">Ben</span><span class="sxs-lookup"><span data-stu-id="215f1-160">Ben</span></span> |<span data-ttu-id="215f1-161">Smith</span><span class="sxs-lookup"><span data-stu-id="215f1-161">Smith</span></span> | Ben@contoso.com| <span data-ttu-id="215f1-162">425-555-0102</span><span class="sxs-lookup"><span data-stu-id="215f1-162">425-555-0102</span></span> |

## <a name="query-by-using-linq"></a><span data-ttu-id="215f1-163">Interroger en utilisant LINQ</span><span class="sxs-lookup"><span data-stu-id="215f1-163">Query by using LINQ</span></span> 
<span data-ttu-id="215f1-164">Vous pouvez également interroger en utilisant LINQ, qui est traduit en expressions de requête OData correspondantes.</span><span class="sxs-lookup"><span data-stu-id="215f1-164">You can also query by using LINQ, which translates to the corresponding OData query expressions.</span></span> <span data-ttu-id="215f1-165">Voici un exemple montrant comment créer des requêtes en utilisant le SDK .NET :</span><span class="sxs-lookup"><span data-stu-id="215f1-165">Here's an example of how to build queries by using the .NET SDK:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="215f1-166">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="215f1-166">Next steps</span></span>

<span data-ttu-id="215f1-167">Dans ce didacticiel, vous avez effectué les tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="215f1-167">In this tutorial, you've done the following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="215f1-168">Découvrez comment interroger en utilisant l’API Table (préversion)</span><span class="sxs-lookup"><span data-stu-id="215f1-168">Learned how to query by using the Table API (preview)</span></span> 

<span data-ttu-id="215f1-169">Vous pouvez maintenant poursuivre avec le didacticiel suivant montrant comment distribuer vos données globalement.</span><span class="sxs-lookup"><span data-stu-id="215f1-169">You can now proceed to the next tutorial to learn how to distribute your data globally.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="215f1-170">Distribuer vos données globalement</span><span class="sxs-lookup"><span data-stu-id="215f1-170">Distribute your data globally</span></span>](tutorial-global-distribution-documentdb.md)
