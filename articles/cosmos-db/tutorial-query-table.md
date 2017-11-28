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
# <a name="azure-cosmos-db-how-tooquery-table-data-by-using-hello-table-api-preview"></a><span data-ttu-id="475a4-104">Azure Cosmos DB : Comment tooquery les données de table à l’aide de hello API (version préliminaire) de la Table ?</span><span class="sxs-lookup"><span data-stu-id="475a4-104">Azure Cosmos DB: How tooquery table data by using hello Table API (preview)?</span></span>

<span data-ttu-id="475a4-105">Bonjour Azure Cosmos DB [Table API](table-introduction.md) (version préliminaire) prend en charge OData et [LINQ](https://docs.microsoft.com/rest/api/storageservices/fileservices/writing-linq-queries-against-the-table-service) requêtes sur les données de clé/valeur (table).</span><span class="sxs-lookup"><span data-stu-id="475a4-105">hello Azure Cosmos DB [Table API](table-introduction.md) (preview) supports OData and [LINQ](https://docs.microsoft.com/rest/api/storageservices/fileservices/writing-linq-queries-against-the-table-service) queries against key/value (table) data.</span></span>  

<span data-ttu-id="475a4-106">Cet article traite des hello tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="475a4-106">This article covers hello following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="475a4-107">Interrogation des données avec hello API de Table</span><span class="sxs-lookup"><span data-stu-id="475a4-107">Querying data with hello Table API</span></span>

<span data-ttu-id="475a4-108">Hello dans cet article, les requêtes utilisent hello suivant exemple `People` table :</span><span class="sxs-lookup"><span data-stu-id="475a4-108">hello queries in this article use hello following sample `People` table:</span></span>

| <span data-ttu-id="475a4-109">PartitionKey</span><span class="sxs-lookup"><span data-stu-id="475a4-109">PartitionKey</span></span> | <span data-ttu-id="475a4-110">RowKey</span><span class="sxs-lookup"><span data-stu-id="475a4-110">RowKey</span></span> | <span data-ttu-id="475a4-111">Email</span><span class="sxs-lookup"><span data-stu-id="475a4-111">Email</span></span> | <span data-ttu-id="475a4-112">PhoneNumber</span><span class="sxs-lookup"><span data-stu-id="475a4-112">PhoneNumber</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="475a4-113">Harp</span><span class="sxs-lookup"><span data-stu-id="475a4-113">Harp</span></span> | <span data-ttu-id="475a4-114">Walter</span><span class="sxs-lookup"><span data-stu-id="475a4-114">Walter</span></span> | Walter@contoso.com| <span data-ttu-id="475a4-115">425-555-0101</span><span class="sxs-lookup"><span data-stu-id="475a4-115">425-555-0101</span></span> |
| <span data-ttu-id="475a4-116">Smith</span><span class="sxs-lookup"><span data-stu-id="475a4-116">Smith</span></span> | <span data-ttu-id="475a4-117">Ben</span><span class="sxs-lookup"><span data-stu-id="475a4-117">Ben</span></span> | Ben@contoso.com| <span data-ttu-id="475a4-118">425-555-0102</span><span class="sxs-lookup"><span data-stu-id="475a4-118">425-555-0102</span></span> |
| <span data-ttu-id="475a4-119">Smith</span><span class="sxs-lookup"><span data-stu-id="475a4-119">Smith</span></span> | <span data-ttu-id="475a4-120">Jeff</span><span class="sxs-lookup"><span data-stu-id="475a4-120">Jeff</span></span> | Jeff@contoso.com| <span data-ttu-id="475a4-121">425-555-0104</span><span class="sxs-lookup"><span data-stu-id="475a4-121">425-555-0104</span></span> | 

<span data-ttu-id="475a4-122">Base de données Azure Cosmos étant compatible avec hello API de stockage de Table Azure, consultez [interrogation de Tables et entités] (https://docs.microsoft.com/rest/api/storageservices/fileservices/querying-tables-and-entities) pour plus d’informations sur comment tooquery à l’aide de hello API de table.</span><span class="sxs-lookup"><span data-stu-id="475a4-122">Because Azure Cosmos DB is compatible with hello Azure Table storage APIs, see [Querying Tables and Entities] (https://docs.microsoft.com/rest/api/storageservices/fileservices/querying-tables-and-entities) for details on how tooquery by using hello Table API.</span></span> 

<span data-ttu-id="475a4-123">Pour plus d’informations sur les fonctions hello premium offre de base de données Azure Cosmos, consultez [base de données Azure Cosmos : API de Table](table-introduction.md) et [développer avec hello API de Table dans .NET](tutorial-develop-table-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="475a4-123">For more information on hello premium capabilities that Azure Cosmos DB offers, see [Azure Cosmos DB: Table API](table-introduction.md) and [Develop with hello Table API in .NET](tutorial-develop-table-dotnet.md).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="475a4-124">Composants requis</span><span class="sxs-lookup"><span data-stu-id="475a4-124">Prerequisites</span></span>

<span data-ttu-id="475a4-125">Pour ces requêtes toowork, vous devez disposer d’un compte de base de données Azure Cosmos et données d’entité dans le conteneur de hello.</span><span class="sxs-lookup"><span data-stu-id="475a4-125">For these queries toowork, you must have an Azure Cosmos DB account and have entity data in hello container.</span></span> <span data-ttu-id="475a4-126">Cela n’est pas le cas ?</span><span class="sxs-lookup"><span data-stu-id="475a4-126">Don't have any of those?</span></span> <span data-ttu-id="475a4-127">Hello complète [démarrage rapide de cinq minutes](https://aka.ms/acdbtnetqs) ou hello [didacticiel pour développeur](https://aka.ms/acdbtabletut) toocreate un compte et le remplir votre base de données.</span><span class="sxs-lookup"><span data-stu-id="475a4-127">Complete hello [five-minute quickstart](https://aka.ms/acdbtnetqs) or hello [developer tutorial](https://aka.ms/acdbtabletut) toocreate an account and populate your database.</span></span>

## <a name="query-on-partitionkey-and-rowkey"></a><span data-ttu-id="475a4-128">Interroger sur PartitionKey et RowKey</span><span class="sxs-lookup"><span data-stu-id="475a4-128">Query on PartitionKey and RowKey</span></span>
<span data-ttu-id="475a4-129">Étant donné que les propriétés PartitionKey et RowKey hello forment la clé primaire d’une entité, vous pouvez utiliser hello suivant l’entité de hello tooidentify une syntaxe spéciale :</span><span class="sxs-lookup"><span data-stu-id="475a4-129">Because hello PartitionKey and RowKey properties form an entity's primary key, you can use hello following special syntax tooidentify hello entity:</span></span> 

<span data-ttu-id="475a4-130">**Requête**</span><span class="sxs-lookup"><span data-stu-id="475a4-130">**Query**</span></span>

```
https://<mytableendpoint>/People(PartitionKey='Harp',RowKey='Walter')  
```
<span data-ttu-id="475a4-131">**Résultats**</span><span class="sxs-lookup"><span data-stu-id="475a4-131">**Results**</span></span>

| <span data-ttu-id="475a4-132">PartitionKey</span><span class="sxs-lookup"><span data-stu-id="475a4-132">PartitionKey</span></span> | <span data-ttu-id="475a4-133">RowKey</span><span class="sxs-lookup"><span data-stu-id="475a4-133">RowKey</span></span> | <span data-ttu-id="475a4-134">Email</span><span class="sxs-lookup"><span data-stu-id="475a4-134">Email</span></span> | <span data-ttu-id="475a4-135">PhoneNumber</span><span class="sxs-lookup"><span data-stu-id="475a4-135">PhoneNumber</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="475a4-136">Harp</span><span class="sxs-lookup"><span data-stu-id="475a4-136">Harp</span></span> | <span data-ttu-id="475a4-137">Walter</span><span class="sxs-lookup"><span data-stu-id="475a4-137">Walter</span></span> | Walter@contoso.com| <span data-ttu-id="475a4-138">425-555-0104</span><span class="sxs-lookup"><span data-stu-id="475a4-138">425-555-0104</span></span> |

<span data-ttu-id="475a4-139">Vous pouvez également spécifier ces propriétés dans le cadre de hello `$filter` option, comme indiqué dans hello suivant la section.</span><span class="sxs-lookup"><span data-stu-id="475a4-139">Alternatively, you can specify these properties as part of hello `$filter` option, as shown in hello following section.</span></span> <span data-ttu-id="475a4-140">Notez que les noms de propriété de clé hello et les valeurs de constante respectent la casse.</span><span class="sxs-lookup"><span data-stu-id="475a4-140">Note that hello key property names and constant values are case-sensitive.</span></span> <span data-ttu-id="475a4-141">Hello PartitionKey et RowKey propriétés sont de type chaîne.</span><span class="sxs-lookup"><span data-stu-id="475a4-141">Both hello PartitionKey and RowKey properties are of type String.</span></span> 

## <a name="query-by-using-an-odata-filter"></a><span data-ttu-id="475a4-142">Interroger en utilisant un filtre OData</span><span class="sxs-lookup"><span data-stu-id="475a4-142">Query by using an OData filter</span></span>
<span data-ttu-id="475a4-143">Quand vous construisez une chaîne de filtrage, prenez en compte les règles suivantes :</span><span class="sxs-lookup"><span data-stu-id="475a4-143">When you're constructing a filter string, keep these rules in mind:</span></span> 

* <span data-ttu-id="475a4-144">Utilisez les opérateurs logiques hello définis par hello spécification du protocole OData toocompare une valeur de la propriété tooa.</span><span class="sxs-lookup"><span data-stu-id="475a4-144">Use hello logical operators defined by hello OData Protocol Specification toocompare a property tooa value.</span></span> <span data-ttu-id="475a4-145">Notez que vous ne peut pas comparer une valeur dynamique tooa de propriété.</span><span class="sxs-lookup"><span data-stu-id="475a4-145">Note that you can't compare a property tooa dynamic value.</span></span> <span data-ttu-id="475a4-146">Côté « un » de l’expression de hello doit être une constante.</span><span class="sxs-lookup"><span data-stu-id="475a4-146">One side of hello expression must be a constant.</span></span> 
* <span data-ttu-id="475a4-147">nom de la propriété Hello, opérateur et valeur de constante doivent être séparés par des espaces encodés URL.</span><span class="sxs-lookup"><span data-stu-id="475a4-147">hello property name, operator, and constant value must be separated by URL-encoded spaces.</span></span> <span data-ttu-id="475a4-148">Un espace est codé URL sous la forme `%20`.</span><span class="sxs-lookup"><span data-stu-id="475a4-148">A space is URL-encoded as `%20`.</span></span> 
* <span data-ttu-id="475a4-149">Toutes les parties de la chaîne de filtrage hello respectent la casse.</span><span class="sxs-lookup"><span data-stu-id="475a4-149">All parts of hello filter string are case-sensitive.</span></span> 
* <span data-ttu-id="475a4-150">valeur de constante Hello doit être de hello même type de propriété hello dans l’ordre des résultats valides de hello filtre tooreturn.</span><span class="sxs-lookup"><span data-stu-id="475a4-150">hello constant value must be of hello same data type as hello property in order for hello filter tooreturn valid results.</span></span> <span data-ttu-id="475a4-151">Pour plus d’informations sur les types de propriété pris en charge, consultez [hello de présentation des modèle de données de Service de Table](https://docs.microsoft.com/rest/api/storageservices/understanding-the-table-service-data-model).</span><span class="sxs-lookup"><span data-stu-id="475a4-151">For more information about supported property types, see [Understanding hello Table Service Data Model](https://docs.microsoft.com/rest/api/storageservices/understanding-the-table-service-data-model).</span></span> 

<span data-ttu-id="475a4-152">Voici un exemple de requête qui montre comment toofilter par hello PartitionKey et propriétés de courrier électronique à l’aide d’un OData `$filter`.</span><span class="sxs-lookup"><span data-stu-id="475a4-152">Here's an example query that shows how toofilter by hello PartitionKey and Email properties by using an OData `$filter`.</span></span>

<span data-ttu-id="475a4-153">**Requête**</span><span class="sxs-lookup"><span data-stu-id="475a4-153">**Query**</span></span>

```
https://<mytableapi-endpoint>/People()?$filter=PartitionKey%20eq%20'Smith'%20and%20Email%20eq%20'Ben@contoso.com'
```

<span data-ttu-id="475a4-154">Pour plus d’informations sur la façon dont les expressions pour différents types de données de filtre de tooconstruct, consultez [interrogeant les Tables et les entités](https://docs.microsoft.com/rest/api/storageservices/querying-tables-and-entities).</span><span class="sxs-lookup"><span data-stu-id="475a4-154">For more information on how tooconstruct filter expressions for various data types, see [Querying Tables and Entities](https://docs.microsoft.com/rest/api/storageservices/querying-tables-and-entities).</span></span>

<span data-ttu-id="475a4-155">**Résultats**</span><span class="sxs-lookup"><span data-stu-id="475a4-155">**Results**</span></span>

| <span data-ttu-id="475a4-156">PartitionKey</span><span class="sxs-lookup"><span data-stu-id="475a4-156">PartitionKey</span></span> | <span data-ttu-id="475a4-157">RowKey</span><span class="sxs-lookup"><span data-stu-id="475a4-157">RowKey</span></span> | <span data-ttu-id="475a4-158">Email</span><span class="sxs-lookup"><span data-stu-id="475a4-158">Email</span></span> | <span data-ttu-id="475a4-159">PhoneNumber</span><span class="sxs-lookup"><span data-stu-id="475a4-159">PhoneNumber</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="475a4-160">Ben</span><span class="sxs-lookup"><span data-stu-id="475a4-160">Ben</span></span> |<span data-ttu-id="475a4-161">Smith</span><span class="sxs-lookup"><span data-stu-id="475a4-161">Smith</span></span> | Ben@contoso.com| <span data-ttu-id="475a4-162">425-555-0102</span><span class="sxs-lookup"><span data-stu-id="475a4-162">425-555-0102</span></span> |

## <a name="query-by-using-linq"></a><span data-ttu-id="475a4-163">Interroger en utilisant LINQ</span><span class="sxs-lookup"><span data-stu-id="475a4-163">Query by using LINQ</span></span> 
<span data-ttu-id="475a4-164">Vous pouvez également interroger à l’aide de LINQ, ce qui se traduit par des expressions de requête OData toohello correspondantes.</span><span class="sxs-lookup"><span data-stu-id="475a4-164">You can also query by using LINQ, which translates toohello corresponding OData query expressions.</span></span> <span data-ttu-id="475a4-165">Voici un exemple de comment toobuild des requêtes à l’aide de hello .NET SDK :</span><span class="sxs-lookup"><span data-stu-id="475a4-165">Here's an example of how toobuild queries by using hello .NET SDK:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="475a4-166">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="475a4-166">Next steps</span></span>

<span data-ttu-id="475a4-167">Dans ce didacticiel, vous avez effectué les éléments suivants de hello :</span><span class="sxs-lookup"><span data-stu-id="475a4-167">In this tutorial, you've done hello following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="475a4-168">Appris comment tooquery à l’aide de hello API de Table (version préliminaire)</span><span class="sxs-lookup"><span data-stu-id="475a4-168">Learned how tooquery by using hello Table API (preview)</span></span> 

<span data-ttu-id="475a4-169">Vous pouvez maintenant toolearn de didacticiel suivant toohello comment toodistribute vos données globalement.</span><span class="sxs-lookup"><span data-stu-id="475a4-169">You can now proceed toohello next tutorial toolearn how toodistribute your data globally.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="475a4-170">Distribuer vos données globalement</span><span class="sxs-lookup"><span data-stu-id="475a4-170">Distribute your data globally</span></span>](tutorial-global-distribution-documentdb.md)
