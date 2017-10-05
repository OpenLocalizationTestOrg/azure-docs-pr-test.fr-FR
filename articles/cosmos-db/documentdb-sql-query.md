---
title: "Requêtes SQL pour l’API DocumentDB Azure Cosmos DB | Microsoft Docs"
description: "Obtenez plus d’informations sur la syntaxe SQL, les concepts de bases de données et les requêtes SQL pour Azure Cosmos DB. SQL peut être utilisé comme un langage de requête JSON dans Azure Cosmos DB."
keywords: "syntaxe sql, requête sql, requêtes sql, langage de requête json, concepts de bases de données, requêtes sql et fonctions agrégées"
services: cosmos-db
documentationcenter: 
author: arramac
manager: jhubbard
editor: monicar
ms.assetid: a73b4ab3-0786-42fd-b59b-555fce09db6e
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: arramac
ms.openlocfilehash: 9b2b5668ef0552485a86f63a120b57c4623bfe35
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="sql-queries-for-azure-cosmos-db-documentdb-api"></a><span data-ttu-id="de9d7-105">Requêtes SQL pour l’API DocumentDB Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="de9d7-105">SQL queries for Azure Cosmos DB DocumentDB API</span></span>
<span data-ttu-id="de9d7-106">Microsoft Azure Cosmos DB prend en charge l’interrogation de documents à l’aide du langage SQL en tant que langage de requête JSON.</span><span class="sxs-lookup"><span data-stu-id="de9d7-106">Microsoft Azure Cosmos DB supports querying documents using SQL (Structured Query Language) as a JSON query language.</span></span> <span data-ttu-id="de9d7-107">Cosmos DB n’utilise pas de schéma.</span><span class="sxs-lookup"><span data-stu-id="de9d7-107">Cosmos DB is truly schema-free.</span></span> <span data-ttu-id="de9d7-108">En raison de son engagement dans le modèle de données JSON directement au sein du moteur de base de données, il fournit l'indexation automatique des documents JSON sans nécessiter un schéma explicite ou la création d'index secondaires.</span><span class="sxs-lookup"><span data-stu-id="de9d7-108">By virtue of its commitment to the JSON data model directly within the database engine, it provides automatic indexing of JSON documents without requiring explicit schema or creation of secondary indexes.</span></span> 

<span data-ttu-id="de9d7-109">Lors de la conception du langage de requête pour Cosmos DB, nous avions deux objectifs à l’esprit :</span><span class="sxs-lookup"><span data-stu-id="de9d7-109">While designing the query language for Cosmos DB, we had two goals in mind:</span></span>

* <span data-ttu-id="de9d7-110">Au lieu d’inventer un langage de requête JSON, nous voulions prendre en charge SQL.</span><span class="sxs-lookup"><span data-stu-id="de9d7-110">Instead of inventing a new JSON query language, we wanted to support SQL.</span></span> <span data-ttu-id="de9d7-111">SQL est l’un des langages de requête les plus conviviaux et populaires.</span><span class="sxs-lookup"><span data-stu-id="de9d7-111">SQL is one of the most familiar and popular query languages.</span></span> <span data-ttu-id="de9d7-112">Le langage SQL de Cosmos DB fournit un modèle de programmation formel pour créer des requêtes élaborées sur les documents JSON.</span><span class="sxs-lookup"><span data-stu-id="de9d7-112">Cosmos DB SQL provides a formal programming model for rich queries over JSON documents.</span></span>
* <span data-ttu-id="de9d7-113">Comme une base de données de documents JSON peut exécuter JavaScript directement dans le moteur de base de données, nous avons voulu utiliser le modèle de programmation de JavaScript comme base pour notre langage de requête.</span><span class="sxs-lookup"><span data-stu-id="de9d7-113">As a JSON document database capable of executing JavaScript directly in the database engine, we wanted to use JavaScript's programming model as the foundation for our query language.</span></span> <span data-ttu-id="de9d7-114">Le langage SQL de l’API DocumentDB est inclus dans le système de type, l’évaluation d’expression et l’appel de fonction de JavaScript.</span><span class="sxs-lookup"><span data-stu-id="de9d7-114">The DocumentDB API SQL is rooted in JavaScript's type system, expression evaluation, and function invocation.</span></span> <span data-ttu-id="de9d7-115">En retour, cela fournit un modèle de programmation naturel pour les projections relationnelles, la navigation hiérarchique entre les documents JSON, les jointures réflexives, les requêtes spatiales et l’appel de fonctions définies par l’utilisateur écrites entièrement en JavaScript, entre autres fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="de9d7-115">This in-turn provides a natural programming model for relational projections, hierarchical navigation across JSON documents, self joins, spatial queries, and invocation of user-defined functions (UDFs) written entirely in JavaScript, among other features.</span></span> 

<span data-ttu-id="de9d7-116">Nous pensons que ces capacités sont la clé pour réduire la friction entre l'application et la base de données et sont cruciales pour la productivité des développeurs.</span><span class="sxs-lookup"><span data-stu-id="de9d7-116">We believe that these capabilities are key to reducing the friction between the application and the database and are crucial for developer productivity.</span></span>

<span data-ttu-id="de9d7-117">Nous vous recommandons de commencer par visionner la vidéo suivante, dans laquelle Aravind Ramachandran présente les fonctionnalités d’interrogation de Cosmos DB, puis d’utiliser notre [Query Playground](http://www.documentdb.com/sql/demo)pour essayer Cosmos DB et exécuter des requêtes SQL sur notre jeu de données.</span><span class="sxs-lookup"><span data-stu-id="de9d7-117">We recommend getting started by watching the following video, where Aravind Ramachandran shows Cosmos DB's querying capabilities, and by visiting our [Query Playground](http://www.documentdb.com/sql/demo), where you can try out Cosmos DB and run SQL queries against our dataset.</span></span>

> [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/DataExposedQueryingDocumentDB/player]
> 
> 

<span data-ttu-id="de9d7-118">Revenez ensuite à cet article, qui commence par un didacticiel sur les requêtes SQL destiné à vous montrer quelques documents JSON et commandes SQL simples.</span><span class="sxs-lookup"><span data-stu-id="de9d7-118">Then, return to this article, where we start with a SQL query tutorial that walks you through some simple JSON documents and SQL commands.</span></span>

## <span data-ttu-id="de9d7-119"><a id="GettingStarted"></a>Prise en main des commandes du langage SQL dans Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="de9d7-119"><a id="GettingStarted"></a>Getting started with SQL commands in Cosmos DB</span></span>
<span data-ttu-id="de9d7-120">Pour voir comment le langage SQL de Cosmos DB fonctionne, nous allons commencer par quelques documents JSON simples sur lesquels nous allons appliquer certaines requêtes simples.</span><span class="sxs-lookup"><span data-stu-id="de9d7-120">To see Cosmos DB SQL at work, let's begin with a few simple JSON documents and walk through some simple queries against it.</span></span> <span data-ttu-id="de9d7-121">Prenez ces deux documents JSON relatifs à deux familles.</span><span class="sxs-lookup"><span data-stu-id="de9d7-121">Consider these two JSON documents about two families.</span></span> <span data-ttu-id="de9d7-122">Avec Cosmos DB, nous n’avons pas besoin de créer de schéma ou d’index secondaire de façon explicite.</span><span class="sxs-lookup"><span data-stu-id="de9d7-122">With Cosmos DB, we do not need to create any schemas or secondary indices explicitly.</span></span> <span data-ttu-id="de9d7-123">Nous devons simplement insérer les documents JSON dans une collection Cosmos DB et ensuite les interroger.</span><span class="sxs-lookup"><span data-stu-id="de9d7-123">We simply need to insert the JSON documents to a Cosmos DB collection and subsequently query.</span></span> <span data-ttu-id="de9d7-124">Nous avons ici un document JSON simple pour la famille Andersen, les parents, les enfants (et leurs animaux), l’adresse et les informations d’inscription.</span><span class="sxs-lookup"><span data-stu-id="de9d7-124">Here we have a simple JSON document for the Andersen family, the parents, children (and their pets), address, and registration information.</span></span> <span data-ttu-id="de9d7-125">Le document se compose de chaînes, de nombres, d'opérateurs booléens, de tableaux et de propriétés imbriquées.</span><span class="sxs-lookup"><span data-stu-id="de9d7-125">The document has strings, numbers, Booleans, arrays, and nested properties.</span></span> 

<span data-ttu-id="de9d7-126">**Document**</span><span class="sxs-lookup"><span data-stu-id="de9d7-126">**Document**</span></span>  

```JSON
{
  "id": "AndersenFamily",
  "lastName": "Andersen",
  "parents": [
     { "firstName": "Thomas" },
     { "firstName": "Mary Kay"}
  ],
  "children": [
     {
         "firstName": "Henriette Thaulow", 
         "gender": "female", 
         "grade": 5,
         "pets": [{ "givenName": "Fluffy" }]
     }
  ],
  "address": { "state": "WA", "county": "King", "city": "seattle" },
  "creationDate": 1431620472,
  "isRegistered": true
}
```

<span data-ttu-id="de9d7-127">Voici un second document comportant une différence subtile : `givenName` et `familyName` sont utilisés au lieu de `firstName` et `lastName`.</span><span class="sxs-lookup"><span data-stu-id="de9d7-127">Here's a second document with one subtle difference – `givenName` and `familyName` are used instead of `firstName` and `lastName`.</span></span>

<span data-ttu-id="de9d7-128">**Document**</span><span class="sxs-lookup"><span data-stu-id="de9d7-128">**Document**</span></span>  

```json
{
  "id": "WakefieldFamily",
  "parents": [
      { "familyName": "Wakefield", "givenName": "Robin" },
      { "familyName": "Miller", "givenName": "Ben" }
  ],
  "children": [
      {
        "familyName": "Merriam", 
        "givenName": "Jesse", 
        "gender": "female", "grade": 1,
        "pets": [
            { "givenName": "Goofy" },
            { "givenName": "Shadow" }
        ]
      },
      { 
        "familyName": "Miller", 
         "givenName": "Lisa", 
         "gender": "female", 
         "grade": 8 }
  ],
  "address": { "state": "NY", "county": "Manhattan", "city": "NY" },
  "creationDate": 1431620462,
  "isRegistered": false
}
```

<span data-ttu-id="de9d7-129">À présent, appliquons quelques requêtes sur ces données pour comprendre certains aspects clés du langage SQL de l’API DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="de9d7-129">Now let's try a few queries against this data to understand some of the key aspects of DocumentDB API SQL.</span></span> <span data-ttu-id="de9d7-130">Par exemple, la requête suivante renvoie les documents dans lesquels le champ ID correspond à `AndersenFamily`.</span><span class="sxs-lookup"><span data-stu-id="de9d7-130">For example, the following query returns the documents where the id field matches `AndersenFamily`.</span></span> <span data-ttu-id="de9d7-131">Comme il s’agit d’un `SELECT *`, le résultat de la requête est le document JSON complet :</span><span class="sxs-lookup"><span data-stu-id="de9d7-131">Since it's a `SELECT *`, the output of the query is the complete JSON document:</span></span>

<span data-ttu-id="de9d7-132">**Requête**</span><span class="sxs-lookup"><span data-stu-id="de9d7-132">**Query**</span></span>

    SELECT * 
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="de9d7-133">**Résultats**</span><span class="sxs-lookup"><span data-stu-id="de9d7-133">**Results**</span></span>

    [{
        "id": "AndersenFamily",
        "lastName": "Andersen",
        "parents": [
           { "firstName": "Thomas" },
           { "firstName": "Mary Kay"}
        ],
        "children": [
           {
               "firstName": "Henriette Thaulow", "gender": "female", "grade": 5,
               "pets": [{ "givenName": "Fluffy" }]
           }
        ],
        "address": { "state": "WA", "county": "King", "city": "seattle" },
        "creationDate": 1431620472,
        "isRegistered": true
    }]


<span data-ttu-id="de9d7-134">À présent, imaginez que nous ayons besoin de remettre en forme le résultat JSON.</span><span class="sxs-lookup"><span data-stu-id="de9d7-134">Now consider the case where we need to reformat the JSON output in a different shape.</span></span> <span data-ttu-id="de9d7-135">Cette requête projette un nouvel objet JSON avec 2 champs sélectionnés, Name et City, où le nom de la ville de l'adresse est identique à celui de l'État.</span><span class="sxs-lookup"><span data-stu-id="de9d7-135">This query projects a new JSON object with two selected fields, Name and City, when the address' city has the same name as the state.</span></span> <span data-ttu-id="de9d7-136">Dans ce cas, « NY, NY » correspond.</span><span class="sxs-lookup"><span data-stu-id="de9d7-136">In this case, "NY, NY" matches.</span></span>

<span data-ttu-id="de9d7-137">**Requête**</span><span class="sxs-lookup"><span data-stu-id="de9d7-137">**Query**</span></span>    

    SELECT {"Name":f.id, "City":f.address.city} AS Family 
    FROM Families f 
    WHERE f.address.city = f.address.state

<span data-ttu-id="de9d7-138">**Résultats**</span><span class="sxs-lookup"><span data-stu-id="de9d7-138">**Results**</span></span>

    [{
        "Family": {
            "Name": "WakefieldFamily", 
            "City": "NY"
        }
    }]


<span data-ttu-id="de9d7-139">La requête suivante retourne tous les noms donnés des enfants de la famille dont l’ID correspond à `WakefieldFamily` classés par ville de résidence.</span><span class="sxs-lookup"><span data-stu-id="de9d7-139">The next query returns all the given names of children in the family whose id matches `WakefieldFamily` ordered by the city of residence.</span></span>

<span data-ttu-id="de9d7-140">**Requête**</span><span class="sxs-lookup"><span data-stu-id="de9d7-140">**Query**</span></span>

    SELECT c.givenName 
    FROM Families f 
    JOIN c IN f.children 
    WHERE f.id = 'WakefieldFamily'
    ORDER BY f.address.city ASC

<span data-ttu-id="de9d7-141">**Résultats**</span><span class="sxs-lookup"><span data-stu-id="de9d7-141">**Results**</span></span>

    [
      { "givenName": "Jesse" }, 
      { "givenName": "Lisa"}
    ]


<span data-ttu-id="de9d7-142">Nous aimerions attirer votre attention sur quelques aspects importants du langage de requête Cosmos DB à travers les exemples que nous venons de voir :</span><span class="sxs-lookup"><span data-stu-id="de9d7-142">We would like to draw attention to a few noteworthy aspects of the Cosmos DB query language through the examples we've seen so far:</span></span>  

* <span data-ttu-id="de9d7-143">Comme le langage SQL de l’API DocumentDB fonctionne avec les valeurs JSON, il traite des entités d’arborescence au lieu des lignes et des colonnes.</span><span class="sxs-lookup"><span data-stu-id="de9d7-143">Since DocumentDB API SQL works on JSON values, it deals with tree shaped entities instead of rows and columns.</span></span> <span data-ttu-id="de9d7-144">C’est pourquoi ce langage vous permet de faire référence aux nœuds de l’arborescence à n’importe quel niveau arbitraire, comme `Node1.Node2.Node3…..Nodem`, tout comme le SQL relationnel se rattachant à la référence en deux parties de `<table>.<column>`.</span><span class="sxs-lookup"><span data-stu-id="de9d7-144">Therefore, the language lets you refer to nodes of the tree at any arbitrary depth, like `Node1.Node2.Node3…..Nodem`, similar to relational SQL referring to the two part reference of `<table>.<column>`.</span></span>   
* <span data-ttu-id="de9d7-145">Le langage SQL fonctionne avec des données sans schéma.</span><span class="sxs-lookup"><span data-stu-id="de9d7-145">The structured query language works with schema-less data.</span></span> <span data-ttu-id="de9d7-146">C'est pourquoi le système de type doit être lié de façon dynamique.</span><span class="sxs-lookup"><span data-stu-id="de9d7-146">Therefore, the type system needs to be bound dynamically.</span></span> <span data-ttu-id="de9d7-147">La même expression peut engendrer différents types sur différents documents.</span><span class="sxs-lookup"><span data-stu-id="de9d7-147">The same expression could yield different types on different documents.</span></span> <span data-ttu-id="de9d7-148">Le résultat d'une requête est une valeur JSON valide, mais n'est pas forcément un schéma fixe.</span><span class="sxs-lookup"><span data-stu-id="de9d7-148">The result of a query is a valid JSON value, but is not guaranteed to be of a fixed schema.</span></span>  
* <span data-ttu-id="de9d7-149">Cosmos DB prend uniquement en charge les documents JSON stricts.</span><span class="sxs-lookup"><span data-stu-id="de9d7-149">Cosmos DB only supports strict JSON documents.</span></span> <span data-ttu-id="de9d7-150">Cela signifie que le système de type et les expressions peuvent uniquement traiter des types JSON.</span><span class="sxs-lookup"><span data-stu-id="de9d7-150">This means the type system and expressions are restricted to deal only with JSON types.</span></span> <span data-ttu-id="de9d7-151">Reportez-vous à la [spécification JSON](http://www.json.org/) pour en savoir plus.</span><span class="sxs-lookup"><span data-stu-id="de9d7-151">Refer to the [JSON specification](http://www.json.org/) for more details.</span></span>  
* <span data-ttu-id="de9d7-152">Une collection Cosmos DB est un conteneur sans schéma pour vos documents JSON.</span><span class="sxs-lookup"><span data-stu-id="de9d7-152">A Cosmos DB collection is a schema-free container of JSON documents.</span></span> <span data-ttu-id="de9d7-153">Les relations des entités de données dans et entre les documents d'une collection sont capturées de façon implicite par le contenant et non par les relations de clé primaire et de clé étrangère.</span><span class="sxs-lookup"><span data-stu-id="de9d7-153">The relations in data entities within and across documents in a collection are implicitly captured by containment and not by primary key and foreign key relations.</span></span> <span data-ttu-id="de9d7-154">Cet aspect est important dans le cadre des liaisons entre documents (ce sujet est abordé plus loin dans cet article).</span><span class="sxs-lookup"><span data-stu-id="de9d7-154">This is an important aspect worth pointing out in light of the intra-document joins discussed later in this article.</span></span>

## <span data-ttu-id="de9d7-155"><a id="Indexing"></a> Indexation Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="de9d7-155"><a id="Indexing"></a> Cosmos DB indexing</span></span>
<span data-ttu-id="de9d7-156">Avant d’aborder la syntaxe SQL de l’API DocumentDB, nous allons présenter la conception de l’indexation dans Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="de9d7-156">Before we get into the DocumentDB API SQL syntax, it is worth exploring the indexing design in Cosmos DB.</span></span> 

<span data-ttu-id="de9d7-157">L'objectif des index de base de données est de servir les requêtes dans leurs différents formulaires et formes tout en consommant un minimum de ressources (comme le temps processeur ou les E/S) et en fournissant un bon débit et une faible latence.</span><span class="sxs-lookup"><span data-stu-id="de9d7-157">The purpose of database indexes is to serve queries in their various forms and shapes with minimum resource consumption (like CPU and input/output) while providing good throughput and low latency.</span></span> <span data-ttu-id="de9d7-158">Souvent, le choix des index adéquats pour l'interrogation d'une base de données requiert une planification et une expérimentation importantes.</span><span class="sxs-lookup"><span data-stu-id="de9d7-158">Often, the choice of the right index for querying a database requires much planning and experimentation.</span></span> <span data-ttu-id="de9d7-159">Cette approche constitue un défi pour les bases de données sans schéma, où les données ne sont pas conformes à un schéma strict et évoluent rapidement.</span><span class="sxs-lookup"><span data-stu-id="de9d7-159">This approach poses a challenge for schema-less databases where the data doesn’t conform to a strict schema and evolves rapidly.</span></span> 

<span data-ttu-id="de9d7-160">C’est pourquoi, lorsque nous avons conçu le sous-système d’indexation de Cosmos DB, nous avons fixé les objectifs suivants :</span><span class="sxs-lookup"><span data-stu-id="de9d7-160">Therefore, when we designed the Cosmos DB indexing subsystem, we set the following goals:</span></span>

* <span data-ttu-id="de9d7-161">Indexer les documents sans requérir un schéma : Le sous-système d’indexation ne requiert pas d’informations de schéma ou n’établit pas d’hypothèse sur les schémas des documents.</span><span class="sxs-lookup"><span data-stu-id="de9d7-161">Index documents without requiring schema: The indexing subsystem does not require any schema information or make any assumptions about schema of the documents.</span></span> 
* <span data-ttu-id="de9d7-162">Prendre en charge des requêtes hiérarchiques et relationnelles enrichies et efficaces : l’index prend en charge le langage de requête Cosmos DB de manière efficace, notamment la prise en charge des projections hiérarchiques et relationnelles.</span><span class="sxs-lookup"><span data-stu-id="de9d7-162">Support for efficient, rich hierarchical, and relational queries: The index supports the Cosmos DB query language efficiently, including support for hierarchical and relational projections.</span></span>
* <span data-ttu-id="de9d7-163">Prendre en charge des requêtes cohérentes en dépit de volumes soutenus d’écritures : Dans le cas des charges de travail à débits d’écriture élevés avec des requêtes cohérentes, l’index est mis à jour de manière incrémentielle, efficacement et en ligne, en dépit de volumes soutenus d’écritures.</span><span class="sxs-lookup"><span data-stu-id="de9d7-163">Support for consistent queries in face of a sustained volume of writes: For high write throughput workloads with consistent queries, the index is updated incrementally, efficiently, and online in the face of a sustained volume of writes.</span></span> <span data-ttu-id="de9d7-164">La mise à jour d'index cohérente est cruciale pour servir les requêtes en respectant le niveau de cohérence défini par l'utilisateur pour le service du document.</span><span class="sxs-lookup"><span data-stu-id="de9d7-164">The consistent index update is crucial to serve the queries at the consistency level in which the user configured the document service.</span></span>
* <span data-ttu-id="de9d7-165">Prendre en charge l’infrastructure multilocataire : Étant donné le modèle basé sur la réservation pour la gouvernance des ressources sur les locataires, les mises à jour d’index sont effectuées dans le budget des ressources système (processeur, mémoire, opérations d’E/S par seconde) allouées par réplica.</span><span class="sxs-lookup"><span data-stu-id="de9d7-165">Support for multi-tenancy: Given the reservation-based model for resource governance across tenants, index updates are performed within the budget of system resources (CPU, memory, and input/output operations per second) allocated per replica.</span></span> 
* <span data-ttu-id="de9d7-166">Efficacité du stockage : Pour des raisons économiques, la surcharge de stockage sur disque de l’index est limitée et prévisible.</span><span class="sxs-lookup"><span data-stu-id="de9d7-166">Storage efficiency: For cost effectiveness, the on-disk storage overhead of the index is bounded and predictable.</span></span> <span data-ttu-id="de9d7-167">C’est très important, car Cosmos DB permet au développeur de trouver des compromis en fonction des coûts entre la surcharge d’index et les performances des requêtes.</span><span class="sxs-lookup"><span data-stu-id="de9d7-167">This is crucial because Cosmos DB allows the developer to make cost-based tradeoffs between index overhead in relation to the query performance.</span></span>  

<span data-ttu-id="de9d7-168">Reportez-vous aux [exemples Azure Cosmos DB](https://github.com/Azure/azure-documentdb-net) sur MSDN pour obtenir des exemples montrant comment configurer la stratégie d’indexation d’une collection.</span><span class="sxs-lookup"><span data-stu-id="de9d7-168">Refer to the [Azure Cosmos DB samples](https://github.com/Azure/azure-documentdb-net) on MSDN for samples showing how to configure the indexing policy for a collection.</span></span> <span data-ttu-id="de9d7-169">Nous allons à présent détailler davantage la syntaxe SQL d’Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="de9d7-169">Let’s now get into the details of the Azure Cosmos DB SQL syntax.</span></span>

## <span data-ttu-id="de9d7-170"><a id="Basics"></a>Principes de base d’une requête SQL Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="de9d7-170"><a id="Basics"></a>Basics of an Azure Cosmos DB SQL query</span></span>
<span data-ttu-id="de9d7-171">Chaque requête se compose d'une clause SELECT et de clauses FROM et WHERE facultatives conformes aux normes ANSI-SQL.</span><span class="sxs-lookup"><span data-stu-id="de9d7-171">Every query consists of a SELECT clause and optional FROM and WHERE clauses per ANSI-SQL standards.</span></span> <span data-ttu-id="de9d7-172">Généralement, pour chaque requête, la source de la clause FROM est énumérée.</span><span class="sxs-lookup"><span data-stu-id="de9d7-172">Typically, for each query, the source in the FROM clause is enumerated.</span></span> <span data-ttu-id="de9d7-173">Puis le filtre de la clause WHERE est appliqué sur la source pour extraire un sous-ensemble de documents JSON.</span><span class="sxs-lookup"><span data-stu-id="de9d7-173">Then the filter in the WHERE clause is applied on the source to retrieve a subset of JSON documents.</span></span> <span data-ttu-id="de9d7-174">Finalement, la clause SELECT est utilisée pour projeter les valeurs JSON demandées dans la liste sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="de9d7-174">Finally, the SELECT clause is used to project the requested JSON values in the select list.</span></span>

    SELECT <select_list> 
    [FROM <from_specification>] 
    [WHERE <filter_condition>]
    [ORDER BY <sort_specification]    


## <span data-ttu-id="de9d7-175"><a id="FromClause"></a>Clause FROM</span><span class="sxs-lookup"><span data-stu-id="de9d7-175"><a id="FromClause"></a>FROM clause</span></span>
<span data-ttu-id="de9d7-176">La clause `FROM <from_specification>` est facultative, sauf si la source est filtrée ou projetée plus loin dans la requête.</span><span class="sxs-lookup"><span data-stu-id="de9d7-176">The `FROM <from_specification>` clause is optional unless the source is filtered or projected later in the query.</span></span> <span data-ttu-id="de9d7-177">L'objectif de cette clause est de spécifier la source des données à partir de laquelle la requête doit fonctionner.</span><span class="sxs-lookup"><span data-stu-id="de9d7-177">The purpose of this clause is to specify the data source upon which the query must operate.</span></span> <span data-ttu-id="de9d7-178">Généralement, l'intégralité de la collection est la source, mais parfois, il peut s'agir plutôt d'un sous-ensemble de la collection.</span><span class="sxs-lookup"><span data-stu-id="de9d7-178">Commonly the whole collection is the source, but one can specify a subset of the collection instead.</span></span> 

<span data-ttu-id="de9d7-179">Une requête telle que `SELECT * FROM Families` indique que l’intégralité de la collection Families est la source de l’énumération.</span><span class="sxs-lookup"><span data-stu-id="de9d7-179">A query like `SELECT * FROM Families` indicates that the entire Families collection is the source over which to enumerate.</span></span> <span data-ttu-id="de9d7-180">Un identificateur ROOT spécial peut être utilisé pour représenter la collection au lieu d'utiliser le nom de la collection.</span><span class="sxs-lookup"><span data-stu-id="de9d7-180">A special identifier ROOT can be used to represent the collection instead of using the collection name.</span></span> <span data-ttu-id="de9d7-181">La liste suivante contient les règles appliquées par requête :</span><span class="sxs-lookup"><span data-stu-id="de9d7-181">The following list contains the rules that are enforced per query:</span></span>

* <span data-ttu-id="de9d7-182">La collection peut être un alias, tel que `SELECT f.id FROM Families AS f` ou simplement `SELECT f.id FROM Families f`.</span><span class="sxs-lookup"><span data-stu-id="de9d7-182">The collection can be aliased, such as `SELECT f.id FROM Families AS f` or simply `SELECT f.id FROM Families f`.</span></span> <span data-ttu-id="de9d7-183">Ici, `f` équivaut à `Families`.</span><span class="sxs-lookup"><span data-stu-id="de9d7-183">Here `f` is the equivalent of `Families`.</span></span> <span data-ttu-id="de9d7-184">`AS` est un mot clé facultatif pour appliquer un alias à l’identificateur.</span><span class="sxs-lookup"><span data-stu-id="de9d7-184">`AS` is an optional keyword to alias the identifier.</span></span>
* <span data-ttu-id="de9d7-185">Une fois l’alias appliqué, vous ne pouvez plus lier la source d’origine.</span><span class="sxs-lookup"><span data-stu-id="de9d7-185">Once aliased, the original source cannot be bound.</span></span> <span data-ttu-id="de9d7-186">Par exemple, `SELECT Families.id FROM Families f` est syntaxiquement incorrect dans la mesure où l’identificateur « Families » ne peut plus être résolu.</span><span class="sxs-lookup"><span data-stu-id="de9d7-186">For example, `SELECT Families.id FROM Families f` is syntactically invalid since the identifier "Families" cannot be resolved anymore.</span></span>
* <span data-ttu-id="de9d7-187">Toutes les propriétés qui doivent être référencées doivent être entièrement qualifiées.</span><span class="sxs-lookup"><span data-stu-id="de9d7-187">All properties that need to be referenced must be fully qualified.</span></span> <span data-ttu-id="de9d7-188">Si le schéma strict n'est pas respecté, ceci est renforcé pour éviter toute liaison ambiguë.</span><span class="sxs-lookup"><span data-stu-id="de9d7-188">In the absence of strict schema adherence, this is enforced to avoid any ambiguous bindings.</span></span> <span data-ttu-id="de9d7-189">`SELECT id FROM Families f` est donc syntaxiquement incorrect, car la propriété `id` n’est pas liée.</span><span class="sxs-lookup"><span data-stu-id="de9d7-189">Therefore, `SELECT id FROM Families f` is syntactically invalid since the property `id` is not bound.</span></span>

### <a name="subdocuments"></a><span data-ttu-id="de9d7-190">Sous-documents</span><span class="sxs-lookup"><span data-stu-id="de9d7-190">Subdocuments</span></span>
<span data-ttu-id="de9d7-191">Vous pouvez également réduire la source à un sous-ensemble.</span><span class="sxs-lookup"><span data-stu-id="de9d7-191">The source can also be reduced to a smaller subset.</span></span> <span data-ttu-id="de9d7-192">Par exemple, en cas d’énumération de la seule sous-arborescence de chaque document, le sous-dossier racine peut alors devenir la source, comme indiqué dans l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="de9d7-192">For instance, to enumerating only a subtree in each document, the subroot could then become the source, as shown in the following example:</span></span>

<span data-ttu-id="de9d7-193">**Requête**</span><span class="sxs-lookup"><span data-stu-id="de9d7-193">**Query**</span></span>

    SELECT * 
    FROM Families.children

<span data-ttu-id="de9d7-194">**Résultats**</span><span class="sxs-lookup"><span data-stu-id="de9d7-194">**Results**</span></span>  

    [
      [
        {
            "firstName": "Henriette Thaulow",
            "gender": "female",
            "grade": 5,
            "pets": [
              {
                  "givenName": "Fluffy"
              }
            ]
        }
      ],
      [
        {
            "familyName": "Merriam",
            "givenName": "Jesse",
            "gender": "female",
            "grade": 1
        },
        {
            "familyName": "Miller",
            "givenName": "Lisa",
            "gender": "female",
            "grade": 8
        }
      ]
    ]

<span data-ttu-id="de9d7-195">Bien que l’exemple ci-dessus utilise un tableau comme source, un objet peut également servir de source, comme dans l’exemple suivant : toute valeur JSON valide (non indéfinie) qui se trouve dans la source est prise en compte pour une inclusion dans le résultat de la requête.</span><span class="sxs-lookup"><span data-stu-id="de9d7-195">While the above example used an array as the source, an object could also be used as the source, which is what's shown in the following example: Any valid JSON value (not undefined) that can be found in the source is considered for inclusion in the result of the query.</span></span> <span data-ttu-id="de9d7-196">Si certaines familles n’ont pas de valeur `address.state`, elles sont exclues des résultats de la requête.</span><span class="sxs-lookup"><span data-stu-id="de9d7-196">If some families don’t have an `address.state` value, they are excluded in the query result.</span></span>

<span data-ttu-id="de9d7-197">**Requête**</span><span class="sxs-lookup"><span data-stu-id="de9d7-197">**Query**</span></span>

    SELECT * 
    FROM Families.address.state

<span data-ttu-id="de9d7-198">**Résultats**</span><span class="sxs-lookup"><span data-stu-id="de9d7-198">**Results**</span></span>

    [
      "WA", 
      "NY"
    ]


## <span data-ttu-id="de9d7-199"><a id="WhereClause"></a>Clause WHERE</span><span class="sxs-lookup"><span data-stu-id="de9d7-199"><a id="WhereClause"></a>WHERE clause</span></span>
<span data-ttu-id="de9d7-200">La clause WHERE (**`WHERE <filter_condition>`**) est facultative.</span><span class="sxs-lookup"><span data-stu-id="de9d7-200">The WHERE clause (**`WHERE <filter_condition>`**) is optional.</span></span> <span data-ttu-id="de9d7-201">Elle indique les conditions que doivent respecter les documents JSON fournis par la source pour être inclus dans le résultat.</span><span class="sxs-lookup"><span data-stu-id="de9d7-201">It specifies the condition(s) that the JSON documents provided by the source must satisfy in order to be included as part of the result.</span></span> <span data-ttu-id="de9d7-202">Chaque document JSON doit évaluer les conditions indiquées sur « true » pour être inclus dans le résultat.</span><span class="sxs-lookup"><span data-stu-id="de9d7-202">Any JSON document must evaluate the specified conditions to "true" to be considered for the result.</span></span> <span data-ttu-id="de9d7-203">La clause WHERE est utilisée par la couche d'index pour déterminer le sous-ensemble le plus petit absolu de documents sources pouvant appartenir au résultat.</span><span class="sxs-lookup"><span data-stu-id="de9d7-203">The WHERE clause is used by the index layer in order to determine the absolute smallest subset of source documents that can be part of the result.</span></span> 

<span data-ttu-id="de9d7-204">La requête suivante demande des documents qui contiennent une propriété name dont la valeur est `AndersenFamily`.</span><span class="sxs-lookup"><span data-stu-id="de9d7-204">The following query requests documents that contain a name property whose value is `AndersenFamily`.</span></span> <span data-ttu-id="de9d7-205">Tous les documents n’ayant pas la propriété name ou ceux dont la valeur de la propriété name ne correspond pas à `AndersenFamily` sont exclus.</span><span class="sxs-lookup"><span data-stu-id="de9d7-205">Any other document that does not have a name property, or where the value does not match `AndersenFamily` is excluded.</span></span> 

<span data-ttu-id="de9d7-206">**Requête**</span><span class="sxs-lookup"><span data-stu-id="de9d7-206">**Query**</span></span>

    SELECT f.address
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="de9d7-207">**Résultats**</span><span class="sxs-lookup"><span data-stu-id="de9d7-207">**Results**</span></span>

    [{
      "address": {
        "state": "WA", 
        "county": "King", 
        "city": "seattle"
      }
    }]


<span data-ttu-id="de9d7-208">L'exemple précédent illustrait une simple requête d'égalité.</span><span class="sxs-lookup"><span data-stu-id="de9d7-208">The previous example showed a simple equality query.</span></span> <span data-ttu-id="de9d7-209">Le langage SQL de l’API DocumentDB prend également en charge plusieurs expressions scalaires.</span><span class="sxs-lookup"><span data-stu-id="de9d7-209">DocumentDB API SQL also supports a variety of scalar expressions.</span></span> <span data-ttu-id="de9d7-210">Les plus répandues sont les expressions binaires et unaires.</span><span class="sxs-lookup"><span data-stu-id="de9d7-210">The most commonly used are binary and unary expressions.</span></span> <span data-ttu-id="de9d7-211">Les références de propriété de l'objet JSON source sont également des expressions valides.</span><span class="sxs-lookup"><span data-stu-id="de9d7-211">Property references from the source JSON object are also valid expressions.</span></span> 

<span data-ttu-id="de9d7-212">Les opérateurs binaires suivants sont actuellement pris en charge et peuvent être utilisés dans les requêtes, comme indiqué dans les exemples suivants :</span><span class="sxs-lookup"><span data-stu-id="de9d7-212">The following binary operators are currently supported and can be used in queries as shown in the following examples:</span></span>  

<table>
<tr>
<td><span data-ttu-id="de9d7-213">Opérateurs arithmétiques</span><span class="sxs-lookup"><span data-stu-id="de9d7-213">Arithmetic</span></span></td>    
<td><span data-ttu-id="de9d7-214">+,-,*,/,%</span><span class="sxs-lookup"><span data-stu-id="de9d7-214">+,-,*,/,%</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="de9d7-215">Opérateurs au niveau du bit</span><span class="sxs-lookup"><span data-stu-id="de9d7-215">Bitwise</span></span></td>    
<td><span data-ttu-id="de9d7-216">|, &, ^, <<, >>, >>> (décalage vers la droite avec remplissage de zéros)</span><span class="sxs-lookup"><span data-stu-id="de9d7-216">|, &, ^, <<, >>, >>> (zero-fill right shift)</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="de9d7-217">Opérateurs logiques</span><span class="sxs-lookup"><span data-stu-id="de9d7-217">Logical</span></span></td>
<td><span data-ttu-id="de9d7-218">AND, OR, NOT</span><span class="sxs-lookup"><span data-stu-id="de9d7-218">AND, OR, NOT</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="de9d7-219">Opérateurs de comparaison</span><span class="sxs-lookup"><span data-stu-id="de9d7-219">Comparison</span></span></td>    
<td><span data-ttu-id="de9d7-220">=, !=, &lt;, &gt;, &lt;=, &gt;=, <></span><span class="sxs-lookup"><span data-stu-id="de9d7-220">=, !=, &lt;, &gt;, &lt;=, &gt;=, <></span></span></td>
</tr>
<tr>
<td><span data-ttu-id="de9d7-221">String</span><span class="sxs-lookup"><span data-stu-id="de9d7-221">String</span></span></td>    
<td><span data-ttu-id="de9d7-222">|| (concaténer)</span><span class="sxs-lookup"><span data-stu-id="de9d7-222">|| (concatenate)</span></span></td>
</tr>
</table>  


<span data-ttu-id="de9d7-223">Examinons certaines requêtes utilisant des opérateurs binaires.</span><span class="sxs-lookup"><span data-stu-id="de9d7-223">Let’s take a look at some queries using binary operators.</span></span>

    SELECT * 
    FROM Families.children[0] c
    WHERE c.grade % 2 = 1     -- matching grades == 5, 1

    SELECT * 
    FROM Families.children[0] c
    WHERE c.grade ^ 4 = 1    -- matching grades == 5

    SELECT *
    FROM Families.children[0] c
    WHERE c.grade >= 5     -- matching grades == 5


<span data-ttu-id="de9d7-224">Les opérateurs unaires +,-, ~ et NOT sont également pris en charge et peuvent être utilisés dans des requêtes comme illustré dans l'exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="de9d7-224">The unary operators +,-, ~ and NOT are also supported, and can be used inside queries as shown in the following example:</span></span>

    SELECT *
    FROM Families.children[0] c
    WHERE NOT(c.grade = 5)  -- matching grades == 1

    SELECT *
    FROM Families.children[0] c
    WHERE (-c.grade = -5)  -- matching grades == 5



<span data-ttu-id="de9d7-225">En plus des opérateurs binaires et unaires, les références de propriétés sont également autorisées.</span><span class="sxs-lookup"><span data-stu-id="de9d7-225">In addition to binary and unary operators, property references are also allowed.</span></span> <span data-ttu-id="de9d7-226">Par exemple, `SELECT * FROM Families f WHERE f.isRegistered` retourne le document JSON qui contient la propriété `isRegistered` dont la valeur est égale à la valeur `true` JSON.</span><span class="sxs-lookup"><span data-stu-id="de9d7-226">For example, `SELECT * FROM Families f WHERE f.isRegistered` returns the JSON document containing the property `isRegistered` where the property's value is equal to the JSON `true` value.</span></span> <span data-ttu-id="de9d7-227">Toutes les autres valeurs (false, null, Undefined, `<number>`, `<string>`, `<object>`, `<array>`, etc.) entraînent l'exclusion du document source du résultat.</span><span class="sxs-lookup"><span data-stu-id="de9d7-227">Any other values (false, null, Undefined, `<number>`, `<string>`, `<object>`, `<array>`, etc.) leads to the source document being excluded from the result.</span></span> 

### <a name="equality-and-comparison-operators"></a><span data-ttu-id="de9d7-228">Opérateurs d'égalité et de comparaison</span><span class="sxs-lookup"><span data-stu-id="de9d7-228">Equality and comparison operators</span></span>
<span data-ttu-id="de9d7-229">Le tableau suivant répertorie les résultats des comparaisons d’égalité dans le langage SQL de l’API DocumentDB entre deux types JSON.</span><span class="sxs-lookup"><span data-stu-id="de9d7-229">The following table shows the result of equality comparisons in DocumentDB API SQL between any two JSON types.</span></span>

<table style = "width:300px">
   <tbody>
      <tr>
         <td valign="top"><span data-ttu-id="de9d7-230">
            <strong>Op</strong>
         </span><span class="sxs-lookup"><span data-stu-id="de9d7-230">
            <strong>Op</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="de9d7-231">
            <strong>Undefined</strong>
         </span><span class="sxs-lookup"><span data-stu-id="de9d7-231">
            <strong>Undefined</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="de9d7-232">
            <strong>Null</strong>
         </span><span class="sxs-lookup"><span data-stu-id="de9d7-232">
            <strong>Null</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="de9d7-233">
            <strong>Boolean</strong>
         </span><span class="sxs-lookup"><span data-stu-id="de9d7-233">
            <strong>Boolean</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="de9d7-234">
            <strong>Number</strong>
         </span><span class="sxs-lookup"><span data-stu-id="de9d7-234">
            <strong>Number</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="de9d7-235">
            <strong>String</strong>
         </span><span class="sxs-lookup"><span data-stu-id="de9d7-235">
            <strong>String</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="de9d7-236">
            <strong>Object</strong>
         </span><span class="sxs-lookup"><span data-stu-id="de9d7-236">
            <strong>Object</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="de9d7-237">
            <strong>Array</strong>
         </span><span class="sxs-lookup"><span data-stu-id="de9d7-237">
            <strong>Array</strong>
         </span></span></td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="de9d7-238">
            <strong>Undefined<strong>
         </span><span class="sxs-lookup"><span data-stu-id="de9d7-238">
            <strong>Undefined<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="de9d7-239">Undefined</span><span class="sxs-lookup"><span data-stu-id="de9d7-239">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="de9d7-240">Undefined</span><span class="sxs-lookup"><span data-stu-id="de9d7-240">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="de9d7-241">Undefined</span><span class="sxs-lookup"><span data-stu-id="de9d7-241">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="de9d7-242">Undefined</span><span class="sxs-lookup"><span data-stu-id="de9d7-242">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="de9d7-243">Undefined</span><span class="sxs-lookup"><span data-stu-id="de9d7-243">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="de9d7-244">Undefined</span><span class="sxs-lookup"><span data-stu-id="de9d7-244">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="de9d7-245">Undefined</span><span class="sxs-lookup"><span data-stu-id="de9d7-245">Undefined</span></span> </td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="de9d7-246">
            <strong>Null<strong>
         </span><span class="sxs-lookup"><span data-stu-id="de9d7-246">
            <strong>Null<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="de9d7-247">Undefined</span><span class="sxs-lookup"><span data-stu-id="de9d7-247">Undefined</span></span> </td>
         <td valign="top"><span data-ttu-id="de9d7-248">
            <strong>OK</strong>
         </span><span class="sxs-lookup"><span data-stu-id="de9d7-248">
            <strong>OK</strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="de9d7-249">Undefined</span><span class="sxs-lookup"><span data-stu-id="de9d7-249">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="de9d7-250">Undefined</span><span class="sxs-lookup"><span data-stu-id="de9d7-250">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="de9d7-251">Undefined</span><span class="sxs-lookup"><span data-stu-id="de9d7-251">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="de9d7-252">Undefined</span><span class="sxs-lookup"><span data-stu-id="de9d7-252">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="de9d7-253">Undefined</span><span class="sxs-lookup"><span data-stu-id="de9d7-253">Undefined</span></span> </td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="de9d7-254">
            <strong>Boolean<strong>
         </span><span class="sxs-lookup"><span data-stu-id="de9d7-254">
            <strong>Boolean<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="de9d7-255">Undefined</span><span class="sxs-lookup"><span data-stu-id="de9d7-255">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="de9d7-256">Undefined</span><span class="sxs-lookup"><span data-stu-id="de9d7-256">Undefined</span></span> </td>
         <td valign="top"><span data-ttu-id="de9d7-257">
            <strong>OK</strong>
         </span><span class="sxs-lookup"><span data-stu-id="de9d7-257">
            <strong>OK</strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="de9d7-258">Undefined</span><span class="sxs-lookup"><span data-stu-id="de9d7-258">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="de9d7-259">Undefined</span><span class="sxs-lookup"><span data-stu-id="de9d7-259">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="de9d7-260">Undefined</span><span class="sxs-lookup"><span data-stu-id="de9d7-260">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="de9d7-261">Undefined</span><span class="sxs-lookup"><span data-stu-id="de9d7-261">Undefined</span></span> </td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="de9d7-262">
            <strong>Number<strong>
         </span><span class="sxs-lookup"><span data-stu-id="de9d7-262">
            <strong>Number<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="de9d7-263">Undefined</span><span class="sxs-lookup"><span data-stu-id="de9d7-263">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="de9d7-264">Undefined</span><span class="sxs-lookup"><span data-stu-id="de9d7-264">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="de9d7-265">Undefined</span><span class="sxs-lookup"><span data-stu-id="de9d7-265">Undefined</span></span> </td>
         <td valign="top"><span data-ttu-id="de9d7-266">
            <strong>OK</strong>
         </span><span class="sxs-lookup"><span data-stu-id="de9d7-266">
            <strong>OK</strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="de9d7-267">Undefined</span><span class="sxs-lookup"><span data-stu-id="de9d7-267">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="de9d7-268">Undefined</span><span class="sxs-lookup"><span data-stu-id="de9d7-268">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="de9d7-269">Undefined</span><span class="sxs-lookup"><span data-stu-id="de9d7-269">Undefined</span></span> </td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="de9d7-270">
            <strong>String<strong>
         </span><span class="sxs-lookup"><span data-stu-id="de9d7-270">
            <strong>String<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="de9d7-271">Undefined</span><span class="sxs-lookup"><span data-stu-id="de9d7-271">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="de9d7-272">Undefined</span><span class="sxs-lookup"><span data-stu-id="de9d7-272">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="de9d7-273">Undefined</span><span class="sxs-lookup"><span data-stu-id="de9d7-273">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="de9d7-274">Undefined</span><span class="sxs-lookup"><span data-stu-id="de9d7-274">Undefined</span></span> </td>
         <td valign="top"><span data-ttu-id="de9d7-275">
            <strong>OK</strong>
         </span><span class="sxs-lookup"><span data-stu-id="de9d7-275">
            <strong>OK</strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="de9d7-276">Undefined</span><span class="sxs-lookup"><span data-stu-id="de9d7-276">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="de9d7-277">Undefined</span><span class="sxs-lookup"><span data-stu-id="de9d7-277">Undefined</span></span> </td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="de9d7-278">
            <strong>Object<strong>
         </span><span class="sxs-lookup"><span data-stu-id="de9d7-278">
            <strong>Object<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="de9d7-279">Undefined</span><span class="sxs-lookup"><span data-stu-id="de9d7-279">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="de9d7-280">Undefined</span><span class="sxs-lookup"><span data-stu-id="de9d7-280">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="de9d7-281">Undefined</span><span class="sxs-lookup"><span data-stu-id="de9d7-281">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="de9d7-282">Undefined</span><span class="sxs-lookup"><span data-stu-id="de9d7-282">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="de9d7-283">Undefined</span><span class="sxs-lookup"><span data-stu-id="de9d7-283">Undefined</span></span> </td>
         <td valign="top"><span data-ttu-id="de9d7-284">
            <strong>OK</strong>
         </span><span class="sxs-lookup"><span data-stu-id="de9d7-284">
            <strong>OK</strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="de9d7-285">Undefined</span><span class="sxs-lookup"><span data-stu-id="de9d7-285">Undefined</span></span> </td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="de9d7-286">
            <strong>Array<strong>
         </span><span class="sxs-lookup"><span data-stu-id="de9d7-286">
            <strong>Array<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="de9d7-287">Undefined</span><span class="sxs-lookup"><span data-stu-id="de9d7-287">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="de9d7-288">Undefined</span><span class="sxs-lookup"><span data-stu-id="de9d7-288">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="de9d7-289">Undefined</span><span class="sxs-lookup"><span data-stu-id="de9d7-289">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="de9d7-290">Undefined</span><span class="sxs-lookup"><span data-stu-id="de9d7-290">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="de9d7-291">Undefined</span><span class="sxs-lookup"><span data-stu-id="de9d7-291">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="de9d7-292">Undefined</span><span class="sxs-lookup"><span data-stu-id="de9d7-292">Undefined</span></span> </td>
         <td valign="top"><span data-ttu-id="de9d7-293">
            <strong>OK</strong>
         </span><span class="sxs-lookup"><span data-stu-id="de9d7-293">
            <strong>OK</strong>
         </span></span></td>
      </tr>
   </tbody>
</table>

<span data-ttu-id="de9d7-294">Pour les autres opérateurs de comparaison tels que >, >=,! =, < et <=, les règles suivantes s'appliquent :</span><span class="sxs-lookup"><span data-stu-id="de9d7-294">For other comparison operators such as >, >=, !=, < and <=, the following rules apply:</span></span>   

* <span data-ttu-id="de9d7-295">Une comparaison entre des types entraîne le résultat Undefined.</span><span class="sxs-lookup"><span data-stu-id="de9d7-295">Comparison across types results in Undefined.</span></span>
* <span data-ttu-id="de9d7-296">Une comparaison entre deux objets ou deux tableaux entraîne le résultat Undefined.</span><span class="sxs-lookup"><span data-stu-id="de9d7-296">Comparison between two objects or two arrays results in Undefined.</span></span>   

<span data-ttu-id="de9d7-297">Si le résultat de l'expression scalaire dans le filtre est Undefined, le document correspondant ne doit pas être inclus dans le résultat, car Undefined n'équivaut pas logiquement à « true ».</span><span class="sxs-lookup"><span data-stu-id="de9d7-297">If the result of the scalar expression in the filter is Undefined, the corresponding document would not be included in the result, since Undefined doesn't logically equate to "true".</span></span>

### <a name="between-keyword"></a><span data-ttu-id="de9d7-298">Mot clé BETWEEN</span><span class="sxs-lookup"><span data-stu-id="de9d7-298">BETWEEN keyword</span></span>
<span data-ttu-id="de9d7-299">Vous pouvez également utiliser le mot clé BETWEEN pour exprimer des requêtes sur des plages de valeurs, comme dans SQL ANSI.</span><span class="sxs-lookup"><span data-stu-id="de9d7-299">You can also use the BETWEEN keyword to express queries against ranges of values like in ANSI SQL.</span></span> <span data-ttu-id="de9d7-300">Vous pouvez utiliser BETWEEN sur des chaînes ou des nombres.</span><span class="sxs-lookup"><span data-stu-id="de9d7-300">BETWEEN can be used against strings or numbers.</span></span>

<span data-ttu-id="de9d7-301">Par exemple, cette requête retourne tous les documents de la famille dans lesquels la note du premier enfant est comprise entre 1 et 5 (tous deux inclus).</span><span class="sxs-lookup"><span data-stu-id="de9d7-301">For example, this query returns all family documents in which the first child's grade is between 1-5 (both inclusive).</span></span> 

    SELECT *
    FROM Families.children[0] c
    WHERE c.grade BETWEEN 1 AND 5

<span data-ttu-id="de9d7-302">Contrairement à SQL ANSI, vous pouvez également utiliser la clause BETWEEN dans la clause FROM, comme dans l'exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="de9d7-302">Unlike in ANSI-SQL, you can also use the BETWEEN clause in the FROM clause like in the following example.</span></span>

    SELECT (c.grade BETWEEN 0 AND 10)
    FROM Families.children[0] c

<span data-ttu-id="de9d7-303">Pour accélérer le temps d'exécution de requête, pensez à créer une stratégie d'indexation qui utilise un type d'index de plage sur tous les chemins d'accès/propriétés numériques qui sont filtrés dans la clause BETWEEN.</span><span class="sxs-lookup"><span data-stu-id="de9d7-303">For faster query execution times, remember to create an indexing policy that uses a range index type against any numeric properties/paths that are filtered in the BETWEEN clause.</span></span> 

<span data-ttu-id="de9d7-304">La principale différence entre l’utilisation de BETWEEN dans l’API DocumentDB et ANSI SQL est que vous pouvez exprimer des requêtes de plage sur des propriétés de types mixtes. Vous pourriez par exemple faire en sorte que « grade » soit un nombre (5) dans certains documents et des chaînes dans d’autres (« grade4 »).</span><span class="sxs-lookup"><span data-stu-id="de9d7-304">The main difference between using BETWEEN in DocumentDB API and ANSI SQL is that you can express range queries against properties of mixed types – for example, you might have "grade" be a number (5) in some documents and strings in others ("grade4").</span></span> <span data-ttu-id="de9d7-305">Dans ces cas-là, comme dans JavaScript, une comparaison entre deux types différents a comme résultat « undefined » et le document est ignoré.</span><span class="sxs-lookup"><span data-stu-id="de9d7-305">In these cases, like in JavaScript, a comparison between two different types results in "undefined", and the document will be skipped.</span></span>

### <a name="logical-and-or-and-not-operators"></a><span data-ttu-id="de9d7-306">Opérateurs logiques (AND, OR et NOT)</span><span class="sxs-lookup"><span data-stu-id="de9d7-306">Logical (AND, OR and NOT) operators</span></span>
<span data-ttu-id="de9d7-307">Les opérateurs logiques interviennent sur des valeurs booléennes.</span><span class="sxs-lookup"><span data-stu-id="de9d7-307">Logical operators operate on Boolean values.</span></span> <span data-ttu-id="de9d7-308">Les tables de vérité logiques de ces opérateurs sont présentées dans les tableaux suivants.</span><span class="sxs-lookup"><span data-stu-id="de9d7-308">The logical truth tables for these operators are shown in the following tables.</span></span>

| <span data-ttu-id="de9d7-309">OU</span><span class="sxs-lookup"><span data-stu-id="de9d7-309">OR</span></span> | <span data-ttu-id="de9d7-310">True</span><span class="sxs-lookup"><span data-stu-id="de9d7-310">True</span></span> | <span data-ttu-id="de9d7-311">False</span><span class="sxs-lookup"><span data-stu-id="de9d7-311">False</span></span> | <span data-ttu-id="de9d7-312">Undefined</span><span class="sxs-lookup"><span data-stu-id="de9d7-312">Undefined</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="de9d7-313">True</span><span class="sxs-lookup"><span data-stu-id="de9d7-313">True</span></span> |<span data-ttu-id="de9d7-314">True</span><span class="sxs-lookup"><span data-stu-id="de9d7-314">True</span></span> |<span data-ttu-id="de9d7-315">True</span><span class="sxs-lookup"><span data-stu-id="de9d7-315">True</span></span> |<span data-ttu-id="de9d7-316">True</span><span class="sxs-lookup"><span data-stu-id="de9d7-316">True</span></span> |
| <span data-ttu-id="de9d7-317">False</span><span class="sxs-lookup"><span data-stu-id="de9d7-317">False</span></span> |<span data-ttu-id="de9d7-318">True</span><span class="sxs-lookup"><span data-stu-id="de9d7-318">True</span></span> |<span data-ttu-id="de9d7-319">False</span><span class="sxs-lookup"><span data-stu-id="de9d7-319">False</span></span> |<span data-ttu-id="de9d7-320">Undefined</span><span class="sxs-lookup"><span data-stu-id="de9d7-320">Undefined</span></span> |
| <span data-ttu-id="de9d7-321">Undefined</span><span class="sxs-lookup"><span data-stu-id="de9d7-321">Undefined</span></span> |<span data-ttu-id="de9d7-322">True</span><span class="sxs-lookup"><span data-stu-id="de9d7-322">True</span></span> |<span data-ttu-id="de9d7-323">Undefined</span><span class="sxs-lookup"><span data-stu-id="de9d7-323">Undefined</span></span> |<span data-ttu-id="de9d7-324">Undefined</span><span class="sxs-lookup"><span data-stu-id="de9d7-324">Undefined</span></span> |

| <span data-ttu-id="de9d7-325">AND</span><span class="sxs-lookup"><span data-stu-id="de9d7-325">AND</span></span> | <span data-ttu-id="de9d7-326">True</span><span class="sxs-lookup"><span data-stu-id="de9d7-326">True</span></span> | <span data-ttu-id="de9d7-327">False</span><span class="sxs-lookup"><span data-stu-id="de9d7-327">False</span></span> | <span data-ttu-id="de9d7-328">Undefined</span><span class="sxs-lookup"><span data-stu-id="de9d7-328">Undefined</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="de9d7-329">True</span><span class="sxs-lookup"><span data-stu-id="de9d7-329">True</span></span> |<span data-ttu-id="de9d7-330">True</span><span class="sxs-lookup"><span data-stu-id="de9d7-330">True</span></span> |<span data-ttu-id="de9d7-331">False</span><span class="sxs-lookup"><span data-stu-id="de9d7-331">False</span></span> |<span data-ttu-id="de9d7-332">Undefined</span><span class="sxs-lookup"><span data-stu-id="de9d7-332">Undefined</span></span> |
| <span data-ttu-id="de9d7-333">False</span><span class="sxs-lookup"><span data-stu-id="de9d7-333">False</span></span> |<span data-ttu-id="de9d7-334">False</span><span class="sxs-lookup"><span data-stu-id="de9d7-334">False</span></span> |<span data-ttu-id="de9d7-335">False</span><span class="sxs-lookup"><span data-stu-id="de9d7-335">False</span></span> |<span data-ttu-id="de9d7-336">False</span><span class="sxs-lookup"><span data-stu-id="de9d7-336">False</span></span> |
| <span data-ttu-id="de9d7-337">Undefined</span><span class="sxs-lookup"><span data-stu-id="de9d7-337">Undefined</span></span> |<span data-ttu-id="de9d7-338">Undefined</span><span class="sxs-lookup"><span data-stu-id="de9d7-338">Undefined</span></span> |<span data-ttu-id="de9d7-339">False</span><span class="sxs-lookup"><span data-stu-id="de9d7-339">False</span></span> |<span data-ttu-id="de9d7-340">Undefined</span><span class="sxs-lookup"><span data-stu-id="de9d7-340">Undefined</span></span> |

| <span data-ttu-id="de9d7-341">NOT</span><span class="sxs-lookup"><span data-stu-id="de9d7-341">NOT</span></span> |  |
| --- | --- |
| <span data-ttu-id="de9d7-342">True</span><span class="sxs-lookup"><span data-stu-id="de9d7-342">True</span></span> |<span data-ttu-id="de9d7-343">False</span><span class="sxs-lookup"><span data-stu-id="de9d7-343">False</span></span> |
| <span data-ttu-id="de9d7-344">False</span><span class="sxs-lookup"><span data-stu-id="de9d7-344">False</span></span> |<span data-ttu-id="de9d7-345">True</span><span class="sxs-lookup"><span data-stu-id="de9d7-345">True</span></span> |
| <span data-ttu-id="de9d7-346">Undefined</span><span class="sxs-lookup"><span data-stu-id="de9d7-346">Undefined</span></span> |<span data-ttu-id="de9d7-347">Undefined</span><span class="sxs-lookup"><span data-stu-id="de9d7-347">Undefined</span></span> |

### <a name="in-keyword"></a><span data-ttu-id="de9d7-348">Mot clé IN</span><span class="sxs-lookup"><span data-stu-id="de9d7-348">IN keyword</span></span>
<span data-ttu-id="de9d7-349">Le mot clé IN permet de vérifier si une valeur spécifiée correspond à une valeur dans une liste.</span><span class="sxs-lookup"><span data-stu-id="de9d7-349">The IN keyword can be used to check whether a specified value matches any value in a list.</span></span> <span data-ttu-id="de9d7-350">Par exemple, cette requête renvoie tous les documents de famille dont l’ID est « WakefieldFamily » ou « AndersenFamily ».</span><span class="sxs-lookup"><span data-stu-id="de9d7-350">For example, this query returns all family documents where the id is one of "WakefieldFamily" or "AndersenFamily".</span></span> 

    SELECT *
    FROM Families 
    WHERE Families.id IN ('AndersenFamily', 'WakefieldFamily')

<span data-ttu-id="de9d7-351">Cet exemple renvoie tous les documents dans lesquels l’état est l’une des valeurs spécifiées.</span><span class="sxs-lookup"><span data-stu-id="de9d7-351">This example returns all documents where the state is any of the specified values.</span></span>

    SELECT *
    FROM Families 
    WHERE Families.address.state IN ("NY", "WA", "CA", "PA", "OH", "OR", "MI", "WI", "MN", "FL")

### <a name="ternary--and-coalesce--operators"></a><span data-ttu-id="de9d7-352">Opérateurs Ternary (?) et Coalesce (??)</span><span class="sxs-lookup"><span data-stu-id="de9d7-352">Ternary (?) and Coalesce (??) operators</span></span>
<span data-ttu-id="de9d7-353">Vous pouvez utiliser les opérateurs Ternary et Coalesce pour créer des expressions conditionnelles, un peu comme dans des langages de programmation courants tels que C# et JavaScript.</span><span class="sxs-lookup"><span data-stu-id="de9d7-353">The Ternary and Coalesce operators can be used to build conditional expressions, similar to popular programming languages like C# and JavaScript.</span></span> 

<span data-ttu-id="de9d7-354">L'opérateur Ternary (?) peut être très pratique lors de la construction de nouvelles propriétés JSON à la volée.</span><span class="sxs-lookup"><span data-stu-id="de9d7-354">The Ternary (?) operator can be very handy when constructing new JSON properties on the fly.</span></span> <span data-ttu-id="de9d7-355">Par exemple, vous pouvez maintenant écrire des requêtes pour classer les niveaux de classe dans un format lisible tel que Débutant/Intermédiaire/Avancé, comme illustré ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="de9d7-355">For example, now you can write queries to classify the class levels into a human readable form like Beginner/Intermediate/Advanced as shown below.</span></span>

     SELECT (c.grade < 5)? "elementary": "other" AS gradeLevel 
     FROM Families.children[0] c

<span data-ttu-id="de9d7-356">Vous pouvez également imbriquer les appels à l'opérateur, comme dans la requête ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="de9d7-356">You can also nest the calls to the operator like in the query below.</span></span>

    SELECT (c.grade < 5)? "elementary": ((c.grade < 9)? "junior": "high")  AS gradeLevel 
    FROM Families.children[0] c

<span data-ttu-id="de9d7-357">Comme avec d’autres opérateurs de requête, si les propriétés référencées dans l’expression conditionnelle sont manquantes dans un document, ou si les types comparés sont différents, ces documents sont exclus dans les résultats de requête.</span><span class="sxs-lookup"><span data-stu-id="de9d7-357">As with other query operators, if the referenced properties in the conditional expression are missing in any document, or if the types being compared are different, then those documents are excluded in the query results.</span></span>

<span data-ttu-id="de9d7-358">Vous pouvez utiliser l’opérateur Coalesce (?) pour vérifier la présence d’une propriété (c’est-à-dire</span><span class="sxs-lookup"><span data-stu-id="de9d7-358">The Coalesce (??) operator can be used to efficiently check for the presence of a property (a.k.a.</span></span> <span data-ttu-id="de9d7-359">vérifier si elle est définie) dans un document.</span><span class="sxs-lookup"><span data-stu-id="de9d7-359">is defined) in a document.</span></span> <span data-ttu-id="de9d7-360">Cela est utile lors de l'interrogation de données semi-structurées ou de types différents.</span><span class="sxs-lookup"><span data-stu-id="de9d7-360">This is useful when querying against semi-structured or data of mixed types.</span></span> <span data-ttu-id="de9d7-361">Par exemple, cette requête retourne « lastName » s'il est présent ou « surname » dans le cas contraire.</span><span class="sxs-lookup"><span data-stu-id="de9d7-361">For example, this query returns the "lastName" if present, or the "surname" if it isn't present.</span></span>

    SELECT f.lastName ?? f.surname AS familyName
    FROM Families f

### <span data-ttu-id="de9d7-362"><a id="EscapingReservedKeywords"></a>Accesseur de propriété entre guillemets</span><span class="sxs-lookup"><span data-stu-id="de9d7-362"><a id="EscapingReservedKeywords"></a>Quoted property accessor</span></span>
<span data-ttu-id="de9d7-363">Vous pouvez également accéder aux propriétés à l’aide de l’opérateur de propriété entre guillemets `[]`.</span><span class="sxs-lookup"><span data-stu-id="de9d7-363">You can also access properties using the quoted property operator `[]`.</span></span> <span data-ttu-id="de9d7-364">Par exemple, `SELECT c.grade` and `SELECT c["grade"]` sont équivalentes.</span><span class="sxs-lookup"><span data-stu-id="de9d7-364">For example, `SELECT c.grade` and `SELECT c["grade"]` are equivalent.</span></span> <span data-ttu-id="de9d7-365">Cette syntaxe est utile si vous devez placer dans une séquence d’échappement une propriété qui contient des espaces, des caractères spéciaux, ou qui partage le même nom qu’un mot clé SQL ou un mot réservé.</span><span class="sxs-lookup"><span data-stu-id="de9d7-365">This syntax is useful when you need to escape a property that contains spaces, special characters, or happens to share the same name as a SQL keyword or reserved word.</span></span>

    SELECT f["lastName"]
    FROM Families f
    WHERE f["id"] = "AndersenFamily"


## <span data-ttu-id="de9d7-366"><a id="SelectClause"></a>Clause SELECT</span><span class="sxs-lookup"><span data-stu-id="de9d7-366"><a id="SelectClause"></a>SELECT clause</span></span>
<span data-ttu-id="de9d7-367">La clause SELECT (**`SELECT <select_list>`**) est obligatoire et indique les valeurs récupérées à partir de la requête, comme dans ANSI-SQL.</span><span class="sxs-lookup"><span data-stu-id="de9d7-367">The SELECT clause (**`SELECT <select_list>`**) is mandatory and specifies what values are retrieved from the query, just like in ANSI-SQL.</span></span> <span data-ttu-id="de9d7-368">Le sous-ensemble filtré au début des documents source est transmis à la phase de projection, où les valeurs JSON spécifiées sont récupérées et un nouvel objet JSON est construit, pour chaque entrée qui lui est transmise.</span><span class="sxs-lookup"><span data-stu-id="de9d7-368">The subset that's been filtered on top of the source documents are passed onto the projection phase, where the specified JSON values are retrieved and a new JSON object is constructed, for each input passed onto it.</span></span> 

<span data-ttu-id="de9d7-369">L'exemple ci-dessous illustre une requête SELECT classique.</span><span class="sxs-lookup"><span data-stu-id="de9d7-369">The following example shows a typical SELECT query.</span></span> 

<span data-ttu-id="de9d7-370">**Requête**</span><span class="sxs-lookup"><span data-stu-id="de9d7-370">**Query**</span></span>

    SELECT f.address
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="de9d7-371">**Résultats**</span><span class="sxs-lookup"><span data-stu-id="de9d7-371">**Results**</span></span>

    [{
      "address": {
        "state": "WA", 
        "county": "King", 
        "city": "seattle"
      }
    }]


### <a name="nested-properties"></a><span data-ttu-id="de9d7-372">Propriétés imbriquées</span><span class="sxs-lookup"><span data-stu-id="de9d7-372">Nested properties</span></span>
<span data-ttu-id="de9d7-373">Dans l’exemple suivant, nous allons projeter les deux propriétés imbriquées `f.address.state` et `f.address.city`.</span><span class="sxs-lookup"><span data-stu-id="de9d7-373">In the following example, we are projecting two nested properties `f.address.state` and `f.address.city`.</span></span>

<span data-ttu-id="de9d7-374">**Requête**</span><span class="sxs-lookup"><span data-stu-id="de9d7-374">**Query**</span></span>

    SELECT f.address.state, f.address.city
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="de9d7-375">**Résultats**</span><span class="sxs-lookup"><span data-stu-id="de9d7-375">**Results**</span></span>

    [{
      "state": "WA", 
      "city": "seattle"
    }]


<span data-ttu-id="de9d7-376">La projection prend également en charge les expressions JSON, comme le montre l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="de9d7-376">Projection also supports JSON expressions as shown in the following example:</span></span>

<span data-ttu-id="de9d7-377">**Requête**</span><span class="sxs-lookup"><span data-stu-id="de9d7-377">**Query**</span></span>

    SELECT { "state": f.address.state, "city": f.address.city, "name": f.id }
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="de9d7-378">**Résultats**</span><span class="sxs-lookup"><span data-stu-id="de9d7-378">**Results**</span></span>

    [{
      "$1": {
        "state": "WA", 
        "city": "seattle", 
        "name": "AndersenFamily"
      }
    }]


<span data-ttu-id="de9d7-379">Observons le rôle de `$1` ici.</span><span class="sxs-lookup"><span data-stu-id="de9d7-379">Let's look at the role of `$1` here.</span></span> <span data-ttu-id="de9d7-380">La clause `SELECT` doit créer un objet JSON et, comme aucune clé n’est fournie, nous utilisons des noms de variable d’argument implicites commençant par `$1`.</span><span class="sxs-lookup"><span data-stu-id="de9d7-380">The `SELECT` clause needs to create a JSON object and since no key is provided, we use implicit argument variable names starting with `$1`.</span></span> <span data-ttu-id="de9d7-381">Par exemple, cette requête renvoie 2 variables d’argument implicites, étiquetées `$1` and `$2`.</span><span class="sxs-lookup"><span data-stu-id="de9d7-381">For example, this query returns two implicit argument variables, labeled `$1` and `$2`.</span></span>

<span data-ttu-id="de9d7-382">**Requête**</span><span class="sxs-lookup"><span data-stu-id="de9d7-382">**Query**</span></span>

    SELECT { "state": f.address.state, "city": f.address.city }, 
           { "name": f.id }
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="de9d7-383">**Résultats**</span><span class="sxs-lookup"><span data-stu-id="de9d7-383">**Results**</span></span>

    [{
      "$1": {
        "state": "WA", 
        "city": "seattle"
      }, 
      "$2": {
        "name": "AndersenFamily"
      }
    }]


### <a name="aliasing"></a><span data-ttu-id="de9d7-384">Alias</span><span class="sxs-lookup"><span data-stu-id="de9d7-384">Aliasing</span></span>
<span data-ttu-id="de9d7-385">À présent, nous allons développer l'exemple précédent en appliquant des alias de valeurs explicites.</span><span class="sxs-lookup"><span data-stu-id="de9d7-385">Now let's extend the example above with explicit aliasing of values.</span></span> <span data-ttu-id="de9d7-386">AS est le mot clé utilisé pour l'application d'alias.</span><span class="sxs-lookup"><span data-stu-id="de9d7-386">AS is the keyword used for aliasing.</span></span> <span data-ttu-id="de9d7-387">Cela est facultatif, comme indiqué lors de la projection de la seconde valeur en tant que `NameInfo`.</span><span class="sxs-lookup"><span data-stu-id="de9d7-387">It's optional as shown while projecting the second value as `NameInfo`.</span></span> 

<span data-ttu-id="de9d7-388">Si une requête a deux propriétés portant le même nom, l'alias doit être utilisé pour renommer l'une ou l'autre des propriétés, pour éviter toute ambiguïté dans le résultat projeté.</span><span class="sxs-lookup"><span data-stu-id="de9d7-388">In case a query has two properties with the same name, aliasing must be used to rename one or both of the properties so that they are disambiguated in the projected result.</span></span>

<span data-ttu-id="de9d7-389">**Requête**</span><span class="sxs-lookup"><span data-stu-id="de9d7-389">**Query**</span></span>

    SELECT 
           { "state": f.address.state, "city": f.address.city } AS AddressInfo, 
           { "name": f.id } NameInfo
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="de9d7-390">**Résultats**</span><span class="sxs-lookup"><span data-stu-id="de9d7-390">**Results**</span></span>

    [{
      "AddressInfo": {
        "state": "WA", 
        "city": "seattle"
      }, 
      "NameInfo": {
        "name": "AndersenFamily"
      }
    }]


### <a name="scalar-expressions"></a><span data-ttu-id="de9d7-391">Expressions scalaires</span><span class="sxs-lookup"><span data-stu-id="de9d7-391">Scalar expressions</span></span>
<span data-ttu-id="de9d7-392">Outre les références de propriété, la clause SELECT prend également en charge les expressions scalaires telles que les constantes, les expressions arithmétiques, les expressions logiques, etc. Par exemple, voici une requête « Hello World » simple.</span><span class="sxs-lookup"><span data-stu-id="de9d7-392">In addition to property references, the SELECT clause also supports scalar expressions like constants, arithmetic expressions, logical expressions, etc. For example, here's a simple "Hello World" query.</span></span>

<span data-ttu-id="de9d7-393">**Requête**</span><span class="sxs-lookup"><span data-stu-id="de9d7-393">**Query**</span></span>

    SELECT "Hello World"

<span data-ttu-id="de9d7-394">**Résultats**</span><span class="sxs-lookup"><span data-stu-id="de9d7-394">**Results**</span></span>

    [{
      "$1": "Hello World"
    }]


<span data-ttu-id="de9d7-395">Voici un exemple plus complexe utilisant une expression scalaire.</span><span class="sxs-lookup"><span data-stu-id="de9d7-395">Here's a more complex example that uses a scalar expression.</span></span>

<span data-ttu-id="de9d7-396">**Requête**</span><span class="sxs-lookup"><span data-stu-id="de9d7-396">**Query**</span></span>

    SELECT ((2 + 11 % 7)-2)/3    

<span data-ttu-id="de9d7-397">**Résultats**</span><span class="sxs-lookup"><span data-stu-id="de9d7-397">**Results**</span></span>

    [{
      "$1": 1.33333
    }]


<span data-ttu-id="de9d7-398">Dans l'exemple suivant, le résultat de l'expression scalaire est un booléen.</span><span class="sxs-lookup"><span data-stu-id="de9d7-398">In the following example, the result of the scalar expression is a Boolean.</span></span>

<span data-ttu-id="de9d7-399">**Requête**</span><span class="sxs-lookup"><span data-stu-id="de9d7-399">**Query**</span></span>

    SELECT f.address.city = f.address.state AS AreFromSameCityState
    FROM Families f    

<span data-ttu-id="de9d7-400">**Résultats**</span><span class="sxs-lookup"><span data-stu-id="de9d7-400">**Results**</span></span>

    [
      {
        "AreFromSameCityState": false
      }, 
      {
        "AreFromSameCityState": true
      }
    ]


### <a name="object-and-array-creation"></a><span data-ttu-id="de9d7-401">Création d'objet et de tableau</span><span class="sxs-lookup"><span data-stu-id="de9d7-401">Object and array creation</span></span>
<span data-ttu-id="de9d7-402">Une autre fonctionnalité clé du langage SQL de l’API DocumentDB est la possibilité de créer un tableau ou un objet.</span><span class="sxs-lookup"><span data-stu-id="de9d7-402">Another key feature of DocumentDB API SQL is array/object creation.</span></span> <span data-ttu-id="de9d7-403">Dans l'exemple précédent, notez que nous avons créé un objet JSON.</span><span class="sxs-lookup"><span data-stu-id="de9d7-403">In the previous example, note that we created a new JSON object.</span></span> <span data-ttu-id="de9d7-404">De même, on peut également construire des tableaux comme indiqué dans les exemples suivants :</span><span class="sxs-lookup"><span data-stu-id="de9d7-404">Similarly, one can also construct arrays as shown in the following examples:</span></span>

<span data-ttu-id="de9d7-405">**Requête**</span><span class="sxs-lookup"><span data-stu-id="de9d7-405">**Query**</span></span>

    SELECT [f.address.city, f.address.state] AS CityState 
    FROM Families f    

<span data-ttu-id="de9d7-406">**Résultats**</span><span class="sxs-lookup"><span data-stu-id="de9d7-406">**Results**</span></span>  

    [
      {
        "CityState": [
          "seattle", 
          "WA"
        ]
      }, 
      {
        "CityState": [
          "NY", 
          "NY"
        ]
      }
    ]

### <span data-ttu-id="de9d7-407"><a id="ValueKeyword"></a>Mot clé VALUE</span><span class="sxs-lookup"><span data-stu-id="de9d7-407"><a id="ValueKeyword"></a>VALUE keyword</span></span>
<span data-ttu-id="de9d7-408">Le mot clé **VALUE** fournit une méthode pour renvoyer une valeur JSON.</span><span class="sxs-lookup"><span data-stu-id="de9d7-408">The **VALUE** keyword provides a way to return JSON value.</span></span> <span data-ttu-id="de9d7-409">Par exemple, la requête indiquée ci-dessous renvoie le scalaire `"Hello World"` au lieu de `{$1: "Hello World"}`.</span><span class="sxs-lookup"><span data-stu-id="de9d7-409">For example, the query shown below returns the scalar `"Hello World"` instead of `{$1: "Hello World"}`.</span></span>

<span data-ttu-id="de9d7-410">**Requête**</span><span class="sxs-lookup"><span data-stu-id="de9d7-410">**Query**</span></span>

    SELECT VALUE "Hello World"

<span data-ttu-id="de9d7-411">**Résultats**</span><span class="sxs-lookup"><span data-stu-id="de9d7-411">**Results**</span></span>

    [
      "Hello World"
    ]


<span data-ttu-id="de9d7-412">La requête suivante renvoie la valeur JSON sans l’étiquette `"address"` dans les résultats.</span><span class="sxs-lookup"><span data-stu-id="de9d7-412">The following query returns the JSON value without the `"address"` label in the results.</span></span>

<span data-ttu-id="de9d7-413">**Requête**</span><span class="sxs-lookup"><span data-stu-id="de9d7-413">**Query**</span></span>

    SELECT VALUE f.address
    FROM Families f    

<span data-ttu-id="de9d7-414">**Résultats**</span><span class="sxs-lookup"><span data-stu-id="de9d7-414">**Results**</span></span>  

    [
      {
        "state": "WA", 
        "county": "King", 
        "city": "seattle"
      }, 
      {
        "state": "NY", 
        "county": "Manhattan", 
        "city": "NY"
      }
    ]

<span data-ttu-id="de9d7-415">L'exemple suivant développe ceci pour expliquer comment renvoyer des valeurs JSON primitives, comme le niveau feuille de l'arborescence JSON.</span><span class="sxs-lookup"><span data-stu-id="de9d7-415">The following example extends this to show how to return JSON primitive values (the leaf level of the JSON tree).</span></span> 

<span data-ttu-id="de9d7-416">**Requête**</span><span class="sxs-lookup"><span data-stu-id="de9d7-416">**Query**</span></span>

    SELECT VALUE f.address.state
    FROM Families f    

<span data-ttu-id="de9d7-417">**Résultats**</span><span class="sxs-lookup"><span data-stu-id="de9d7-417">**Results**</span></span>

    [
      "WA",
      "NY"
    ]


### <a name="-operator"></a><span data-ttu-id="de9d7-418">Opérateur *</span><span class="sxs-lookup"><span data-stu-id="de9d7-418">* Operator</span></span>
<span data-ttu-id="de9d7-419">L'opérateur spécial (*) est pris en charge pour projeter le document tel quel.</span><span class="sxs-lookup"><span data-stu-id="de9d7-419">The special operator (*) is supported to project the document as-is.</span></span> <span data-ttu-id="de9d7-420">Une fois utilisé, il doit être le seul champ projeté.</span><span class="sxs-lookup"><span data-stu-id="de9d7-420">When used, it must be the only projected field.</span></span> <span data-ttu-id="de9d7-421">Si une requête comme `SELECT * FROM Families f` est valide, `SELECT VALUE * FROM Families f ` et `SELECT *, f.id FROM Families f ` ne le sont pas.</span><span class="sxs-lookup"><span data-stu-id="de9d7-421">While a query like `SELECT * FROM Families f` is valid, `SELECT VALUE * FROM Families f ` and  `SELECT *, f.id FROM Families f ` are not valid.</span></span>

<span data-ttu-id="de9d7-422">**Requête**</span><span class="sxs-lookup"><span data-stu-id="de9d7-422">**Query**</span></span>

    SELECT * 
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="de9d7-423">**Résultats**</span><span class="sxs-lookup"><span data-stu-id="de9d7-423">**Results**</span></span>

    [{
        "id": "AndersenFamily",
        "lastName": "Andersen",
        "parents": [
           { "firstName": "Thomas" },
           { "firstName": "Mary Kay"}
        ],
        "children": [
           {
               "firstName": "Henriette Thaulow", "gender": "female", "grade": 5,
               "pets": [{ "givenName": "Fluffy" }]
           }
        ],
        "address": { "state": "WA", "county": "King", "city": "seattle" },
        "creationDate": 1431620472,
        "isRegistered": true
    }]

### <span data-ttu-id="de9d7-424"><a id="TopKeyword"></a>Opérateur TOP</span><span class="sxs-lookup"><span data-stu-id="de9d7-424"><a id="TopKeyword"></a>TOP Operator</span></span>
<span data-ttu-id="de9d7-425">Le mot clé TOP peut être utilisé pour limiter le nombre de valeurs provenant d'une requête.</span><span class="sxs-lookup"><span data-stu-id="de9d7-425">The TOP keyword can be used to limit the number of values from a query.</span></span> <span data-ttu-id="de9d7-426">Lorsque TOP est utilisé conjointement avec la clause ORDER BY, le jeu de résultats est limité aux N premières valeurs ordonnées ; sinon, il retourne les N premiers résultats dans un ordre non défini.</span><span class="sxs-lookup"><span data-stu-id="de9d7-426">When TOP is used in conjunction with the ORDER BY clause, the result set is limited to the first N number of ordered values; otherwise, it returns the first N number of results in an undefined order.</span></span> <span data-ttu-id="de9d7-427">En tant que meilleure pratique, dans une instruction SELECT, utilisez toujours une clause ORDER BY avec la clause TOP.</span><span class="sxs-lookup"><span data-stu-id="de9d7-427">As a best practice, in a SELECT statement, always use an ORDER BY clause with the TOP clause.</span></span> <span data-ttu-id="de9d7-428">Il s'agit de la seule façon d'indiquer de manière prévisible les lignes qui sont affectées par TOP.</span><span class="sxs-lookup"><span data-stu-id="de9d7-428">This is the only way to predictably indicate which rows are affected by TOP.</span></span> 

<span data-ttu-id="de9d7-429">**Requête**</span><span class="sxs-lookup"><span data-stu-id="de9d7-429">**Query**</span></span>

    SELECT TOP 1 * 
    FROM Families f 

<span data-ttu-id="de9d7-430">**Résultats**</span><span class="sxs-lookup"><span data-stu-id="de9d7-430">**Results**</span></span>

    [{
        "id": "AndersenFamily",
        "lastName": "Andersen",
        "parents": [
           { "firstName": "Thomas" },
           { "firstName": "Mary Kay"}
        ],
        "children": [
           {
               "firstName": "Henriette Thaulow", "gender": "female", "grade": 5,
               "pets": [{ "givenName": "Fluffy" }]
           }
        ],
        "address": { "state": "WA", "county": "King", "city": "seattle" },
        "creationDate": 1431620472,
        "isRegistered": true
    }]

<span data-ttu-id="de9d7-431">L’opérateur TOP peut être utilisé avec une valeur constante (comme indiqué ci-dessus) ou avec une valeur variable à l'aide de requêtes paramétrables.</span><span class="sxs-lookup"><span data-stu-id="de9d7-431">TOP can be used with a constant value (as shown above) or with a variable value using parameterized queries.</span></span> <span data-ttu-id="de9d7-432">Pour plus d'informations, consultez les requêtes paramétrables ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="de9d7-432">For more details, please see parameterized queries below.</span></span>

### <span data-ttu-id="de9d7-433"><a id="Aggregates"></a>Fonctions d’agrégation</span><span class="sxs-lookup"><span data-stu-id="de9d7-433"><a id="Aggregates"></a>Aggregate Functions</span></span>
<span data-ttu-id="de9d7-434">Vous pouvez également effectuer des agrégations dans la clause `SELECT`.</span><span class="sxs-lookup"><span data-stu-id="de9d7-434">You can also perform aggregations in the `SELECT` clause.</span></span> <span data-ttu-id="de9d7-435">Les fonctions d’agrégation effectuent un calcul sur un ensemble de valeurs et renvoient une valeur unique.</span><span class="sxs-lookup"><span data-stu-id="de9d7-435">Aggregate functions perform a calculation on a set of values and return a single value.</span></span> <span data-ttu-id="de9d7-436">Par exemple, la requête suivante renvoie le nombre de documents de famille que contient la collection.</span><span class="sxs-lookup"><span data-stu-id="de9d7-436">For example, the following query returns the count of family documents within the collection.</span></span>

<span data-ttu-id="de9d7-437">**Requête**</span><span class="sxs-lookup"><span data-stu-id="de9d7-437">**Query**</span></span>

    SELECT COUNT(1) 
    FROM Families f 

<span data-ttu-id="de9d7-438">**Résultats**</span><span class="sxs-lookup"><span data-stu-id="de9d7-438">**Results**</span></span>

    [{
        "$1": 2
    }]

<span data-ttu-id="de9d7-439">Vous pouvez également renvoyer la valeur scalaire de l’agrégation à l’aide du mot clé `VALUE`.</span><span class="sxs-lookup"><span data-stu-id="de9d7-439">You can also return the scalar value of the aggregate by using the `VALUE` keyword.</span></span> <span data-ttu-id="de9d7-440">Par exemple, la requête suivante renvoie le nombre de valeurs sous forme de nombre unique :</span><span class="sxs-lookup"><span data-stu-id="de9d7-440">For example, the following query returns the count of values as a single number:</span></span>

<span data-ttu-id="de9d7-441">**Requête**</span><span class="sxs-lookup"><span data-stu-id="de9d7-441">**Query**</span></span>

    SELECT VALUE COUNT(1) 
    FROM Families f 

<span data-ttu-id="de9d7-442">**Résultats**</span><span class="sxs-lookup"><span data-stu-id="de9d7-442">**Results**</span></span>

    [ 2 ]

<span data-ttu-id="de9d7-443">Vous pouvez également effectuer des agrégations en appliquant des filtres simultanément.</span><span class="sxs-lookup"><span data-stu-id="de9d7-443">You can also perform aggregates in combination with filters.</span></span> <span data-ttu-id="de9d7-444">Par exemple, la requête suivante renvoie le nombre de documents avec une adresse dans l’état de Washington.</span><span class="sxs-lookup"><span data-stu-id="de9d7-444">For example, the following query returns the count of documents with the address in the state of Washington.</span></span>

<span data-ttu-id="de9d7-445">**Requête**</span><span class="sxs-lookup"><span data-stu-id="de9d7-445">**Query**</span></span>

    SELECT VALUE COUNT(1) 
    FROM Families f
    WHERE f.address.state = "WA" 

<span data-ttu-id="de9d7-446">**Résultats**</span><span class="sxs-lookup"><span data-stu-id="de9d7-446">**Results**</span></span>

    [ 1 ]

<span data-ttu-id="de9d7-447">Le tableau suivant présente la liste des fonctions d’agrégation prises en charge dans l’API DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="de9d7-447">The following table shows the list of supported aggregate functions in DocumentDB API.</span></span> <span data-ttu-id="de9d7-448">`SUM` et `AVG` s’appliquent à des valeurs numériques, tandis que `COUNT`, `MIN`, et `MAX` peuvent être effectuées sur des nombres, des chaînes, des booléens et des valeurs Null.</span><span class="sxs-lookup"><span data-stu-id="de9d7-448">`SUM` and `AVG` are performed over numeric values, whereas `COUNT`, `MIN`, and `MAX` can be performed over numbers, strings, Booleans, and nulls.</span></span> 

| <span data-ttu-id="de9d7-449">Usage</span><span class="sxs-lookup"><span data-stu-id="de9d7-449">Usage</span></span> | <span data-ttu-id="de9d7-450">Description</span><span class="sxs-lookup"><span data-stu-id="de9d7-450">Description</span></span> |
|-------|-------------|
| <span data-ttu-id="de9d7-451">COUNT</span><span class="sxs-lookup"><span data-stu-id="de9d7-451">COUNT</span></span> | <span data-ttu-id="de9d7-452">Renvoie le nombre d’éléments que contient l’expression.</span><span class="sxs-lookup"><span data-stu-id="de9d7-452">Returns the number of items in the expression.</span></span> |
| <span data-ttu-id="de9d7-453">SUM</span><span class="sxs-lookup"><span data-stu-id="de9d7-453">SUM</span></span>   | <span data-ttu-id="de9d7-454">Renvoie la somme de toutes les valeurs de l’expression.</span><span class="sxs-lookup"><span data-stu-id="de9d7-454">Returns the sum of all the values in the expression.</span></span> |
| <span data-ttu-id="de9d7-455">MIN</span><span class="sxs-lookup"><span data-stu-id="de9d7-455">MIN</span></span>   | <span data-ttu-id="de9d7-456">Renvoie la valeur minimale de l’expression.</span><span class="sxs-lookup"><span data-stu-id="de9d7-456">Returns the minimum value in the expression.</span></span> |
| <span data-ttu-id="de9d7-457">MAX</span><span class="sxs-lookup"><span data-stu-id="de9d7-457">MAX</span></span>   | <span data-ttu-id="de9d7-458">Renvoie la valeur maximale de l’expression.</span><span class="sxs-lookup"><span data-stu-id="de9d7-458">Returns the maximum value in the expression.</span></span> |
| <span data-ttu-id="de9d7-459">MOY</span><span class="sxs-lookup"><span data-stu-id="de9d7-459">AVG</span></span>   | <span data-ttu-id="de9d7-460">Renvoie la moyenne des valeurs de l’expression.</span><span class="sxs-lookup"><span data-stu-id="de9d7-460">Returns the average of the values in the expression.</span></span> |

<span data-ttu-id="de9d7-461">Il est également possible d’effectuer des agrégations sur les résultats d’une itération de tableau.</span><span class="sxs-lookup"><span data-stu-id="de9d7-461">Aggregates can also be performed over the results of an array iteration.</span></span> <span data-ttu-id="de9d7-462">Pour en savoir plus, consultez la section relative à [l’itération de tableaux dans les requêtes](#Iteration).</span><span class="sxs-lookup"><span data-stu-id="de9d7-462">For more information, see [Array Iteration in Queries](#Iteration).</span></span>

> [!NOTE]
> <span data-ttu-id="de9d7-463">Lorsque vous utilisez l’Explorateur de requêtes du portail Azure, notez que les requêtes d’agrégation peuvent renvoyer les résultats partiellement agrégés sur une page de requête.</span><span class="sxs-lookup"><span data-stu-id="de9d7-463">When using the Azure portal's Query Explorer, note that aggregation queries may return the partially aggregated results over a query page.</span></span> <span data-ttu-id="de9d7-464">Les kits de développement logiciel (SDK) génèrent une valeur cumulée unique sur toutes les pages.</span><span class="sxs-lookup"><span data-stu-id="de9d7-464">The SDKs produces a single cumulative value across all pages.</span></span> 
> 
> <span data-ttu-id="de9d7-465">Pour effectuer des requêtes d’agrégation à l’aide de code, vous avez besoin du SDK .NET 1.12.0, du SDK .NET Core 1.1.0 ou du SDK Java 1.9.5 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="de9d7-465">In order to perform aggregation queries using code, you need .NET SDK 1.12.0, .NET Core SDK 1.1.0, or Java SDK 1.9.5 or above.</span></span>    
>

## <span data-ttu-id="de9d7-466"><a id="OrderByClause"></a>Clause ORDER BY</span><span class="sxs-lookup"><span data-stu-id="de9d7-466"><a id="OrderByClause"></a>ORDER BY clause</span></span>
<span data-ttu-id="de9d7-467">Comme dans ANSI-SQL, vous pouvez désormais inclure une clause Order By facultative lors d’une interrogation.</span><span class="sxs-lookup"><span data-stu-id="de9d7-467">Like in ANSI-SQL, you can include an optional Order By clause while querying.</span></span> <span data-ttu-id="de9d7-468">La clause peut inclure un argument ASC/DESC facultatif pour spécifier l'ordre dans lequel les résultats doivent être récupérés.</span><span class="sxs-lookup"><span data-stu-id="de9d7-468">The clause can include an optional ASC/DESC argument to specify the order in which results must be retrieved.</span></span>

<span data-ttu-id="de9d7-469">Par exemple, voici une requête qui récupère les familles dans l'ordre de la ville de résidence.</span><span class="sxs-lookup"><span data-stu-id="de9d7-469">For example, here's a query that retrieves families in order of the resident city's name.</span></span>

<span data-ttu-id="de9d7-470">**Requête**</span><span class="sxs-lookup"><span data-stu-id="de9d7-470">**Query**</span></span>

    SELECT f.id, f.address.city
    FROM Families f 
    ORDER BY f.address.city

<span data-ttu-id="de9d7-471">**Résultats**</span><span class="sxs-lookup"><span data-stu-id="de9d7-471">**Results**</span></span>

    [
      {
        "id": "WakefieldFamily",
        "city": "NY"
      },
      {
        "id": "AndersenFamily",
        "city": "Seattle"    
      }
    ]

<span data-ttu-id="de9d7-472">Et voici une requête qui récupère les familles suivant l'ordre de la date de création, qui est stockée comme un nombre représentant l'époque d’époque, c'est-à-dire le temps écoulé depuis le 1er janvier 1970 en secondes.</span><span class="sxs-lookup"><span data-stu-id="de9d7-472">And here's a query that retrieves families in order of creation date, which is stored as a number representing the epoch time, i.e, elapsed time since Jan 1, 1970 in seconds.</span></span>

<span data-ttu-id="de9d7-473">**Requête**</span><span class="sxs-lookup"><span data-stu-id="de9d7-473">**Query**</span></span>

    SELECT f.id, f.creationDate
    FROM Families f 
    ORDER BY f.creationDate DESC

<span data-ttu-id="de9d7-474">**Résultats**</span><span class="sxs-lookup"><span data-stu-id="de9d7-474">**Results**</span></span>

    [
      {
        "id": "WakefieldFamily",
        "creationDate": 1431620462
      },
      {
        "id": "AndersenFamily",
        "creationDate": 1431620472    
      }
    ]

## <span data-ttu-id="de9d7-475"><a id="Advanced"></a>Concepts avancés de base de données et requêtes SQL</span><span class="sxs-lookup"><span data-stu-id="de9d7-475"><a id="Advanced"></a>Advanced database concepts and SQL queries</span></span>

### <span data-ttu-id="de9d7-476"><a id="Iteration"></a>Itération</span><span class="sxs-lookup"><span data-stu-id="de9d7-476"><a id="Iteration"></a>Iteration</span></span>
<span data-ttu-id="de9d7-477">Une nouvelle construction a été ajoutée par le biais du mot clé **IN** du langage SQL de l’API DocumentDB pour prendre en charge l’itération sur les tableaux JSON.</span><span class="sxs-lookup"><span data-stu-id="de9d7-477">A new construct was added via the **IN** keyword in DocumentDB API SQL to provide support for iterating over JSON arrays.</span></span> <span data-ttu-id="de9d7-478">La source FROM fournit une prise en charge pour l'itération.</span><span class="sxs-lookup"><span data-stu-id="de9d7-478">The FROM source provides support for iteration.</span></span> <span data-ttu-id="de9d7-479">Commençons par l'exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="de9d7-479">Let's start with the following example:</span></span>

<span data-ttu-id="de9d7-480">**Requête**</span><span class="sxs-lookup"><span data-stu-id="de9d7-480">**Query**</span></span>

    SELECT * 
    FROM Families.children

<span data-ttu-id="de9d7-481">**Résultats**</span><span class="sxs-lookup"><span data-stu-id="de9d7-481">**Results**</span></span>  

    [
      [
        {
          "firstName": "Henriette Thaulow", 
          "gender": "female", 
          "grade": 5, 
          "pets": [{ "givenName": "Fluffy"}]
        }
      ], 
      [
        {
            "familyName": "Merriam", 
            "givenName": "Jesse", 
            "gender": "female", 
            "grade": 1
        }, 
        {
            "familyName": "Miller", 
            "givenName": "Lisa", 
            "gender": "female", 
            "grade": 8
        }
      ]
    ]

<span data-ttu-id="de9d7-482">À présent, intéressons-nous à une autre requête, qui effectue une itération sur les enfants de la collection.</span><span class="sxs-lookup"><span data-stu-id="de9d7-482">Now let's look at another query that performs iteration over children in the collection.</span></span> <span data-ttu-id="de9d7-483">Notez la différence dans le tableau de sortie.</span><span class="sxs-lookup"><span data-stu-id="de9d7-483">Note the difference in the output array.</span></span> <span data-ttu-id="de9d7-484">Cet exemple fractionne `children` et regroupe les résultats en un seul tableau.</span><span class="sxs-lookup"><span data-stu-id="de9d7-484">This example splits `children` and flattens the results into a single array.</span></span>  

<span data-ttu-id="de9d7-485">**Requête**</span><span class="sxs-lookup"><span data-stu-id="de9d7-485">**Query**</span></span>

    SELECT * 
    FROM c IN Families.children

<span data-ttu-id="de9d7-486">**Résultats**</span><span class="sxs-lookup"><span data-stu-id="de9d7-486">**Results**</span></span>  

    [
      {
          "firstName": "Henriette Thaulow",
          "gender": "female",
          "grade": 5,
          "pets": [{ "givenName": "Fluffy" }]
      },
      {
          "familyName": "Merriam",
          "givenName": "Jesse",
          "gender": "female",
          "grade": 1
      },
      {
          "familyName": "Miller",
          "givenName": "Lisa",
          "gender": "female",
          "grade": 8
      }
    ]

<span data-ttu-id="de9d7-487">Cette utilisation peut être généralisée pour filtrer chaque entrée du tableau, comme dans l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="de9d7-487">This can be further used to filter on each individual entry of the array as shown in the following example:</span></span>

<span data-ttu-id="de9d7-488">**Requête**</span><span class="sxs-lookup"><span data-stu-id="de9d7-488">**Query**</span></span>

    SELECT c.givenName
    FROM c IN Families.children
    WHERE c.grade = 8

<span data-ttu-id="de9d7-489">**Résultats**</span><span class="sxs-lookup"><span data-stu-id="de9d7-489">**Results**</span></span>  

    [{
      "givenName": "Lisa"
    }]

<span data-ttu-id="de9d7-490">Vous pouvez également effectuer une agrégation sur le résultat de l’itération de tableau.</span><span class="sxs-lookup"><span data-stu-id="de9d7-490">You can also perform aggregation over the result of array iteration.</span></span> <span data-ttu-id="de9d7-491">Par exemple, la requête suivante compte le nombre d’enfants parmi toutes les familles.</span><span class="sxs-lookup"><span data-stu-id="de9d7-491">For example, the following query counts the number of children among all families.</span></span>

<span data-ttu-id="de9d7-492">**Requête**</span><span class="sxs-lookup"><span data-stu-id="de9d7-492">**Query**</span></span>

    SELECT COUNT(child) 
    FROM child IN Families.children

<span data-ttu-id="de9d7-493">**Résultats**</span><span class="sxs-lookup"><span data-stu-id="de9d7-493">**Results**</span></span>  

    [
      { 
        "$1": 3
      }
    ]

### <span data-ttu-id="de9d7-494"><a id="Joins"></a>Jointures</span><span class="sxs-lookup"><span data-stu-id="de9d7-494"><a id="Joins"></a>Joins</span></span>
<span data-ttu-id="de9d7-495">Dans une base de données relationnelle, il est important de joindre les tables.</span><span class="sxs-lookup"><span data-stu-id="de9d7-495">In a relational database, the need to join across tables is important.</span></span> <span data-ttu-id="de9d7-496">Ceci est la conséquence logique de la conception de schémas normalisés.</span><span class="sxs-lookup"><span data-stu-id="de9d7-496">It's the logical corollary to designing normalized schemas.</span></span> <span data-ttu-id="de9d7-497">Au contraire, l’API DocumentDB traite les modèles de données dénormalisés de documents sans schéma.</span><span class="sxs-lookup"><span data-stu-id="de9d7-497">Contrary to this, DocumentDB API deals with the denormalized data model of schema-free documents.</span></span> <span data-ttu-id="de9d7-498">Il s'agit de l'équivalent logique d'une « jointure réflexive ».</span><span class="sxs-lookup"><span data-stu-id="de9d7-498">This is the logical equivalent of a "self-join".</span></span>

<span data-ttu-id="de9d7-499">La syntaxe prise en charge par le langage est la suivante : <from_source1> JOIN <from_source2> JOIN… JOIN <from_sourceN>.</span><span class="sxs-lookup"><span data-stu-id="de9d7-499">The syntax that the language supports is <from_source1> JOIN <from_source2> JOIN ... JOIN <from_sourceN>.</span></span> <span data-ttu-id="de9d7-500">D’une façon générale, ceci renvoie un ensemble de **N**-tuples (un tuple avec **N** valeurs).</span><span class="sxs-lookup"><span data-stu-id="de9d7-500">Overall, this returns a set of **N**-tuples (tuple with **N** values).</span></span> <span data-ttu-id="de9d7-501">Les valeurs de chaque tuple sont produites par l'itération de tous les alias de la collection sur leurs ensembles respectifs.</span><span class="sxs-lookup"><span data-stu-id="de9d7-501">Each tuple has values produced by iterating all collection aliases over their respective sets.</span></span> <span data-ttu-id="de9d7-502">En d'autres termes, il s'agit d'un produit croisé complet des ensembles participants à la jointure.</span><span class="sxs-lookup"><span data-stu-id="de9d7-502">In other words, this is a full cross product of the sets participating in the join.</span></span>

<span data-ttu-id="de9d7-503">Les exemples suivants illustrent le fonctionnement de la clause JOIN.</span><span class="sxs-lookup"><span data-stu-id="de9d7-503">The following examples show how the JOIN clause works.</span></span> <span data-ttu-id="de9d7-504">Dans l'exemple suivant, le résultat est vide, car le produit croisé de chaque document de la source et d'un ensemble vide est vide.</span><span class="sxs-lookup"><span data-stu-id="de9d7-504">In the following example, the result is empty since the cross product of each document from source and an empty set is empty.</span></span>

<span data-ttu-id="de9d7-505">**Requête**</span><span class="sxs-lookup"><span data-stu-id="de9d7-505">**Query**</span></span>

    SELECT f.id
    FROM Families f
    JOIN f.NonExistent

<span data-ttu-id="de9d7-506">**Résultats**</span><span class="sxs-lookup"><span data-stu-id="de9d7-506">**Results**</span></span>  

    [{
    }]


<span data-ttu-id="de9d7-507">Dans l’exemple suivant, la jointure concerne la racine du document et la sous-racine `children`.</span><span class="sxs-lookup"><span data-stu-id="de9d7-507">In the following example, the join is between the document root and the `children` subroot.</span></span> <span data-ttu-id="de9d7-508">Il s'agit d'un produit croisé entre deux objets JSON.</span><span class="sxs-lookup"><span data-stu-id="de9d7-508">It's a cross product between two JSON objects.</span></span> <span data-ttu-id="de9d7-509">Le fait que les enfants soient compris dans un tableau n'est pas valide dans le JOIN, car nous traitons une seule racine qui est le tableau des enfants.</span><span class="sxs-lookup"><span data-stu-id="de9d7-509">The fact that children is an array is not effective in the JOIN since we are dealing with a single root that is the children array.</span></span> <span data-ttu-id="de9d7-510">Nous n'obtenons donc que deux résultats, car le produit croisé de chaque document avec le tableau renvoie exactement un seul document.</span><span class="sxs-lookup"><span data-stu-id="de9d7-510">Hence the result contains only two results, since the cross product of each document with the array yields exactly only one document.</span></span>

<span data-ttu-id="de9d7-511">**Requête**</span><span class="sxs-lookup"><span data-stu-id="de9d7-511">**Query**</span></span>

    SELECT f.id
    FROM Families f
    JOIN f.children

<span data-ttu-id="de9d7-512">**Résultats**</span><span class="sxs-lookup"><span data-stu-id="de9d7-512">**Results**</span></span>

    [
      {
        "id": "AndersenFamily"
      }, 
      {
        "id": "WakefieldFamily"
      }
    ]


<span data-ttu-id="de9d7-513">L'exemple suivant illustre une jointure plus conventionnelle :</span><span class="sxs-lookup"><span data-stu-id="de9d7-513">The following example shows a more conventional join:</span></span>

<span data-ttu-id="de9d7-514">**Requête**</span><span class="sxs-lookup"><span data-stu-id="de9d7-514">**Query**</span></span>

    SELECT f.id
    FROM Families f
    JOIN c IN f.children 

<span data-ttu-id="de9d7-515">**Résultats**</span><span class="sxs-lookup"><span data-stu-id="de9d7-515">**Results**</span></span>

    [
      {
        "id": "AndersenFamily"
      }, 
      {
        "id": "WakefieldFamily"
      }, 
      {
        "id": "WakefieldFamily"
      }
    ]



<span data-ttu-id="de9d7-516">La première chose à noter est que l’élément `from_source` de la clause **JOIN** est un itérateur.</span><span class="sxs-lookup"><span data-stu-id="de9d7-516">The first thing to note is that the `from_source` of the **JOIN** clause is an iterator.</span></span> <span data-ttu-id="de9d7-517">Dans ce cas, le flux est le suivant :</span><span class="sxs-lookup"><span data-stu-id="de9d7-517">So, the flow in this case is as follows:</span></span>  

* <span data-ttu-id="de9d7-518">Développez chaque élément enfant **c** dans le tableau.</span><span class="sxs-lookup"><span data-stu-id="de9d7-518">Expand each child element **c** in the array.</span></span>
* <span data-ttu-id="de9d7-519">Appliquez le produit croisé de la racine du document **f** avec chaque élément enfant **c** aplati à la première étape.</span><span class="sxs-lookup"><span data-stu-id="de9d7-519">Apply a cross product with the root of the document **f** with each child element **c** that was flattened in the first step.</span></span>
* <span data-ttu-id="de9d7-520">Enfin, projetez seule la propriété du nom **f** de l’objet racine.</span><span class="sxs-lookup"><span data-stu-id="de9d7-520">Finally, project the root object **f** name property alone.</span></span> 

<span data-ttu-id="de9d7-521">Le premier document (`AndersenFamily`) contient un seul élément enfant. Le jeu de résultats contient donc un seul objet correspondant à ce document.</span><span class="sxs-lookup"><span data-stu-id="de9d7-521">The first document (`AndersenFamily`) contains only one child element, so the result set contains only a single object corresponding to this document.</span></span> <span data-ttu-id="de9d7-522">Le second document (`WakefieldFamily`) contient deux enfants.</span><span class="sxs-lookup"><span data-stu-id="de9d7-522">The second document (`WakefieldFamily`) contains two children.</span></span> <span data-ttu-id="de9d7-523">Le produit croisé produit donc un objet distinct pour chaque enfant, résultant en deux objets, un pour chaque enfant correspondant à ce document.</span><span class="sxs-lookup"><span data-stu-id="de9d7-523">So, the cross product produces a separate object for each child, thereby resulting in two objects, one for each child corresponding to this document.</span></span> <span data-ttu-id="de9d7-524">Les champs racine de ces deux documents sont identiques, comme on peut l’attendre d’un produit croisé.</span><span class="sxs-lookup"><span data-stu-id="de9d7-524">The root fields in both these documents are the same, just as you would expect in a cross product.</span></span>

<span data-ttu-id="de9d7-525">La véritable utilité de la syntaxe JOIN est de former des tuples à partir du produit croisé dans une forme qui serait autrement difficile à projeter.</span><span class="sxs-lookup"><span data-stu-id="de9d7-525">The real utility of the JOIN is to form tuples from the cross-product in a shape that's otherwise difficult to project.</span></span> <span data-ttu-id="de9d7-526">En outre, comme nous pouvons le voir dans l’exemple ci-dessous, vous pouvez filtrer la combinaison d’un tuple permettant à l’utilisateur de choisir une condition respectée par l’ensemble des tuples.</span><span class="sxs-lookup"><span data-stu-id="de9d7-526">Furthermore, as we see in the example below, you could filter on the combination of a tuple that lets' the user chose a condition satisfied by the tuples overall.</span></span>

<span data-ttu-id="de9d7-527">**Requête**</span><span class="sxs-lookup"><span data-stu-id="de9d7-527">**Query**</span></span>

    SELECT 
        f.id AS familyName,
        c.givenName AS childGivenName,
        c.firstName AS childFirstName,
        p.givenName AS petName 
    FROM Families f 
    JOIN c IN f.children 
    JOIN p IN c.pets

<span data-ttu-id="de9d7-528">**Résultats**</span><span class="sxs-lookup"><span data-stu-id="de9d7-528">**Results**</span></span>

    [
      {
        "familyName": "AndersenFamily", 
        "childFirstName": "Henriette Thaulow", 
        "petName": "Fluffy"
      }, 
      {
        "familyName": "WakefieldFamily", 
        "childGivenName": "Jesse", 
        "petName": "Goofy"
      }, 
      {
       "familyName": "WakefieldFamily", 
       "childGivenName": "Jesse", 
       "petName": "Shadow"
      }
    ]



<span data-ttu-id="de9d7-529">Cet exemple est une extension naturelle du précédent, et effectue une double jointure.</span><span class="sxs-lookup"><span data-stu-id="de9d7-529">This example is a natural extension of the preceding example, and performs a double join.</span></span> <span data-ttu-id="de9d7-530">Le produit croisé peut donc être affiché comme le pseudo-code ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="de9d7-530">So, the cross product can be viewed as the following pseudo-code:</span></span>

    for-each(Family f in Families)
    {    
        for-each(Child c in f.children)
        {
            for-each(Pet p in c.pets)
            {
                return (Tuple(f.id AS familyName, 
                  c.givenName AS childGivenName, 
                  c.firstName AS childFirstName,
                  p.givenName AS petName));
            }
        }
    }

<span data-ttu-id="de9d7-531">`AndersenFamily` a un enfant qui a un animal.</span><span class="sxs-lookup"><span data-stu-id="de9d7-531">`AndersenFamily` has one child who has one pet.</span></span> <span data-ttu-id="de9d7-532">Le produit croisé renvoie une ligne (1\*1\*1) à partir de cette famille.</span><span class="sxs-lookup"><span data-stu-id="de9d7-532">So, the cross product yields one row (1\*1\*1) from this family.</span></span> <span data-ttu-id="de9d7-533">Cependant, WakefieldFamily a deux enfants, mais seul l'un d'eux, « Jesse », a des animaux.</span><span class="sxs-lookup"><span data-stu-id="de9d7-533">WakefieldFamily however has two children, but only one child "Jesse" has pets.</span></span> <span data-ttu-id="de9d7-534">Or, Jesse a deux animaux.</span><span class="sxs-lookup"><span data-stu-id="de9d7-534">Jesse has two pets though.</span></span> <span data-ttu-id="de9d7-535">Le produit croisé renvoie donc 1\*1\*2 = 2 lignes à partir de cette famille.</span><span class="sxs-lookup"><span data-stu-id="de9d7-535">Hence the cross product yields 1\*1\*2 = 2 rows from this family.</span></span>

<span data-ttu-id="de9d7-536">L’exemple suivant ajoute un filtre supplémentaire sur `pet`.</span><span class="sxs-lookup"><span data-stu-id="de9d7-536">In the next example, there is an additional filter on `pet`.</span></span> <span data-ttu-id="de9d7-537">Ceci exclut tous les tuples où le nom de l'animal n'est pas « Shadow ».</span><span class="sxs-lookup"><span data-stu-id="de9d7-537">This excludes all the tuples where the pet name is not "Shadow".</span></span> <span data-ttu-id="de9d7-538">Notez que nous pouvons développer des tuples à partir de tableaux, filtrer n'importe quel élément du tuple et projeter n'importe quelle combinaison d'éléments.</span><span class="sxs-lookup"><span data-stu-id="de9d7-538">Notice that we are able to build tuples from arrays, filter on any of the elements of the tuple, and project any combination of the elements.</span></span> 

<span data-ttu-id="de9d7-539">**Requête**</span><span class="sxs-lookup"><span data-stu-id="de9d7-539">**Query**</span></span>

    SELECT 
        f.id AS familyName,
        c.givenName AS childGivenName,
        c.firstName AS childFirstName,
        p.givenName AS petName 
    FROM Families f 
    JOIN c IN f.children 
    JOIN p IN c.pets
    WHERE p.givenName = "Shadow"

<span data-ttu-id="de9d7-540">**Résultats**</span><span class="sxs-lookup"><span data-stu-id="de9d7-540">**Results**</span></span>

    [
      {
       "familyName": "WakefieldFamily", 
       "childGivenName": "Jesse", 
       "petName": "Shadow"
      }
    ]


## <span data-ttu-id="de9d7-541"><a id="JavaScriptIntegration"></a>Intégration JavaScript</span><span class="sxs-lookup"><span data-stu-id="de9d7-541"><a id="JavaScriptIntegration"></a>JavaScript integration</span></span>
<span data-ttu-id="de9d7-542">Azure Cosmos DB fournit un modèle de programmation pour l’exécution de la logique d’application JavaScript directement sur les collections en termes de procédures stockées et de déclencheurs.</span><span class="sxs-lookup"><span data-stu-id="de9d7-542">Azure Cosmos DB provides a programming model for executing JavaScript based application logic directly on the collections in terms of stored procedures and triggers.</span></span> <span data-ttu-id="de9d7-543">Ceci permet pour les deux :</span><span class="sxs-lookup"><span data-stu-id="de9d7-543">This allows for both:</span></span>

* <span data-ttu-id="de9d7-544">La possibilité d’effectuer des opérations CRUD transactionnelles hautes performances et d’interroger les documents d’une collection grâce à l’intégration approfondie de l’exécution JavaScript directement dans le moteur de base de données.</span><span class="sxs-lookup"><span data-stu-id="de9d7-544">Ability to do high-performance transactional CRUD operations and queries against documents in a collection by virtue of the deep integration of JavaScript runtime directly within the database engine.</span></span> 
* <span data-ttu-id="de9d7-545">Une modélisation naturelle du flux de contrôle, de l'étendue des variables, de l'attribution et de l'intégration des primitives de gestion d'exception avec des transactions de base de données.</span><span class="sxs-lookup"><span data-stu-id="de9d7-545">A natural modeling of control flow, variable scoping, and assignment and integration of exception handling primitives with database transactions.</span></span> <span data-ttu-id="de9d7-546">Pour plus de détails sur la prise en charge Azure Cosmos DB dans le cadre de l’intégration JavaScript, veuillez consulter la documentation sur la programmation côté serveur de JavaScript.</span><span class="sxs-lookup"><span data-stu-id="de9d7-546">For more details about Azure Cosmos DB support for JavaScript integration, please refer to the JavaScript server-side programmability documentation.</span></span>

### <span data-ttu-id="de9d7-547"><a id="UserDefinedFunctions"></a>Fonctions définies par l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="de9d7-547"><a id="UserDefinedFunctions"></a>User-Defined Functions (UDFs)</span></span>
<span data-ttu-id="de9d7-548">En plus des types déjà définis dans cet article, le langage SQL de l’API DocumentDB prend en charge les fonctions définies par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="de9d7-548">Along with the types already defined in this article, DocumentDB API SQL provides support for User Defined Functions (UDF).</span></span> <span data-ttu-id="de9d7-549">En particulier, les fonctions définies par l'utilisateur scalaires sont prises en charge pour que les développeurs puissent transmettre de nombreux arguments ou aucun, puis renvoyer un seul argument en retour.</span><span class="sxs-lookup"><span data-stu-id="de9d7-549">In particular, scalar UDFs are supported where the developers can pass in zero or many arguments and return a single argument result back.</span></span> <span data-ttu-id="de9d7-550">La légalité des valeurs JSON de chacun de ces arguments est vérifiée.</span><span class="sxs-lookup"><span data-stu-id="de9d7-550">Each of these arguments is checked for being legal JSON values.</span></span>  

<span data-ttu-id="de9d7-551">La syntaxe du langage SQL de l’API DocumentDB est étendue pour prendre en charge la logique d’application personnalisée à l’aide de ces fonctions définies par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="de9d7-551">The DocumentDB API SQL syntax is extended to support custom application logic using these User-Defined Functions.</span></span> <span data-ttu-id="de9d7-552">Ces dernières peuvent être enregistrées avec l’API DocumentDB, puis référencées dans le cadre d’une requête SQL.</span><span class="sxs-lookup"><span data-stu-id="de9d7-552">UDFs can be registered with DocumentDB API and then be referenced as part of a SQL query.</span></span> <span data-ttu-id="de9d7-553">En fait, les fonctions définies par l'utilisateur sont conçues avec soin pour pouvoir être appelées par des requêtes.</span><span class="sxs-lookup"><span data-stu-id="de9d7-553">In fact, the UDFs are exquisitely designed to be invoked by queries.</span></span> <span data-ttu-id="de9d7-554">En conséquence, les fonctions définies par l'utilisateur ne peuvent pas accéder à l'objet de contexte que possèdent les autres types JavaScript (procédures stockées, déclencheurs).</span><span class="sxs-lookup"><span data-stu-id="de9d7-554">As a corollary to this choice, UDFs do not have access to the context object which the other JavaScript types (stored procedures and triggers) have.</span></span> <span data-ttu-id="de9d7-555">Comme les requêtes s'exécutent en lecture seule, elles peuvent démarrer sur des réplicas principaux ou secondaires.</span><span class="sxs-lookup"><span data-stu-id="de9d7-555">Since queries execute as read-only, they can run either on primary or on secondary replicas.</span></span> <span data-ttu-id="de9d7-556">Par conséquent, les fonctions définies par l'utilisateur sont conçues pour être exécutées sur des réplicas secondaires, contrairement à d'autres types JavaScript.</span><span class="sxs-lookup"><span data-stu-id="de9d7-556">Therefore, UDFs are designed to run on secondary replicas unlike other JavaScript types.</span></span>

<span data-ttu-id="de9d7-557">Voici un exemple de méthode d’enregistrement de fonction définie par l’utilisateur sur la base de données Cosmos DB, plus précisément sous une collection de documents.</span><span class="sxs-lookup"><span data-stu-id="de9d7-557">Below is an example of how a UDF can be registered at the Cosmos DB database, specifically under a document collection.</span></span>

       UserDefinedFunction regexMatchUdf = new UserDefinedFunction
       {
           Id = "REGEX_MATCH",
           Body = @"function (input, pattern) { 
                       return input.match(pattern) !== null;
                   };",
       };

       UserDefinedFunction createdUdf = client.CreateUserDefinedFunctionAsync(
           UriFactory.CreateDocumentCollectionUri("testdb", "families"), 
           regexMatchUdf).Result;  

<span data-ttu-id="de9d7-558">L’exemple ci-dessus crée une fonction définie par l’utilisateur dont le nom est `REGEX_MATCH`.</span><span class="sxs-lookup"><span data-stu-id="de9d7-558">The preceding example creates a UDF whose name is `REGEX_MATCH`.</span></span> <span data-ttu-id="de9d7-559">Elle accepte les deux valeurs de chaîne JSON `input` and `pattern` , et vérifie si la première correspond au modèle spécifié dans la seconde à l’aide de la fonction string.match() de JavaScript.</span><span class="sxs-lookup"><span data-stu-id="de9d7-559">It accepts two JSON string values `input` and `pattern` and checks if the first matches the pattern specified in the second using JavaScript's string.match() function.</span></span>

<span data-ttu-id="de9d7-560">Nous pouvons maintenant utiliser cette fonction définie par l'utilisateur dans une requête, dans une projection.</span><span class="sxs-lookup"><span data-stu-id="de9d7-560">We can now use this UDF in a query in a projection.</span></span> <span data-ttu-id="de9d7-561">Les fonctions définies par l’utilisateur doivent être qualifiées par le préfixe respectant la casse « udf.»</span><span class="sxs-lookup"><span data-stu-id="de9d7-561">UDFs must be qualified with the case-sensitive prefix "udf."</span></span> <span data-ttu-id="de9d7-562">quand elles sont appelées à partir de requêtes.</span><span class="sxs-lookup"><span data-stu-id="de9d7-562">when called from within queries.</span></span> 

> [!NOTE]
> <span data-ttu-id="de9d7-563">Jusqu’au 17 mars 2015, Cosmos DB prenait en charge les appels de fonctions définies par l’utilisateur sans préfixe « udf ».</span><span class="sxs-lookup"><span data-stu-id="de9d7-563">Prior to 3/17/2015, Cosmos DB supported UDF calls without the "udf."</span></span> <span data-ttu-id="de9d7-564">comme SELECT REGEX_MATCH().</span><span class="sxs-lookup"><span data-stu-id="de9d7-564">prefix like SELECT REGEX_MATCH().</span></span> <span data-ttu-id="de9d7-565">Ce modèle d'appel est maintenant déconseillé.</span><span class="sxs-lookup"><span data-stu-id="de9d7-565">This calling pattern has been deprecated.</span></span>  
> 
> 

<span data-ttu-id="de9d7-566">**Requête**</span><span class="sxs-lookup"><span data-stu-id="de9d7-566">**Query**</span></span>

    SELECT udf.REGEX_MATCH(Families.address.city, ".*eattle")
    FROM Families

<span data-ttu-id="de9d7-567">**Résultats**</span><span class="sxs-lookup"><span data-stu-id="de9d7-567">**Results**</span></span>

    [
      {
        "$1": true
      }, 
      {
        "$1": false
      }
    ]

<span data-ttu-id="de9d7-568">Vous pouvez également utiliser les fonctions définies par l'utilisateur (et qualifiées par le préfixe « udf.</span><span class="sxs-lookup"><span data-stu-id="de9d7-568">The UDF can also be used inside a filter as shown in the example below, also qualified with the "udf."</span></span> <span data-ttu-id="de9d7-569">Préfixe :</span><span class="sxs-lookup"><span data-stu-id="de9d7-569">prefix:</span></span>

<span data-ttu-id="de9d7-570">**Requête**</span><span class="sxs-lookup"><span data-stu-id="de9d7-570">**Query**</span></span>

    SELECT Families.id, Families.address.city
    FROM Families
    WHERE udf.REGEX_MATCH(Families.address.city, ".*eattle")

<span data-ttu-id="de9d7-571">**Résultats**</span><span class="sxs-lookup"><span data-stu-id="de9d7-571">**Results**</span></span>

    [{
        "id": "AndersenFamily",
        "city": "Seattle"
    }]


<span data-ttu-id="de9d7-572">Fondamentalement, les fonctions définies par l'utilisateur sont des expressions scalaires valides et peuvent être utilisées dans des projections et des filtres.</span><span class="sxs-lookup"><span data-stu-id="de9d7-572">In essence, UDFs are valid scalar expressions and can be used in both projections and filters.</span></span> 

<span data-ttu-id="de9d7-573">Pour développer la puissance des fonctions définies par l'utilisateur, étudions un autre exemple de logique conditionnelle :</span><span class="sxs-lookup"><span data-stu-id="de9d7-573">To expand on the power of UDFs, let's look at another example with conditional logic:</span></span>

       UserDefinedFunction seaLevelUdf = new UserDefinedFunction()
       {
           Id = "SEALEVEL",
           Body = @"function(city) {
                   switch (city) {
                       case 'seattle':
                           return 520;
                       case 'NY':
                           return 410;
                       case 'Chicago':
                           return 673;
                       default:
                           return -1;
                    }"
            };

            UserDefinedFunction createdUdf = await client.CreateUserDefinedFunctionAsync(
                UriFactory.CreateDocumentCollectionUri("testdb", "families"), 
                seaLevelUdf);


<span data-ttu-id="de9d7-574">L'exemple ci-dessous utilise les fonctions définies par l'utilisateur.</span><span class="sxs-lookup"><span data-stu-id="de9d7-574">Below is an example that exercises the UDF.</span></span>

<span data-ttu-id="de9d7-575">**Requête**</span><span class="sxs-lookup"><span data-stu-id="de9d7-575">**Query**</span></span>

    SELECT f.address.city, udf.SEALEVEL(f.address.city) AS seaLevel
    FROM Families f    

<span data-ttu-id="de9d7-576">**Résultats**</span><span class="sxs-lookup"><span data-stu-id="de9d7-576">**Results**</span></span>

     [
      {
        "city": "seattle", 
        "seaLevel": 520
      }, 
      {
        "city": "NY", 
        "seaLevel": 410
      }
    ]


<span data-ttu-id="de9d7-577">Les exemples suivants illustrent l’aptitude des fonctions définies par l’utilisateur à intégrer la puissance du langage JavaScript dans le langage SQL de l’API DocumentDB afin de fournir une interface programmable enrichie pour mener à bien des procédures complexes et employer une logique conditionnelle en exploitant les capacités intégrées de l’exécution JavaScript.</span><span class="sxs-lookup"><span data-stu-id="de9d7-577">As the preceding examples showcase, UDFs integrate the power of JavaScript language with the DocumentDB API SQL to provide a rich programmable interface to do complex procedural, conditional logic with the help of inbuilt JavaScript runtime capabilities.</span></span>

<span data-ttu-id="de9d7-578">Le langage SQL de l’API DocumentDB fournit les arguments aux fonctions définies par l’utilisateur pour chaque document de la source lors de l’étape actuelle (clause WHERE ou SELECT) du traitement des fonctions définies par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="de9d7-578">DocumentDB API SQL provides the arguments to the UDFs for each document in the source at the current stage (WHERE clause or SELECT clause) of processing the UDF.</span></span> <span data-ttu-id="de9d7-579">Le résultat est intégré au pipeline d'exécution générale en toute transparence.</span><span class="sxs-lookup"><span data-stu-id="de9d7-579">The result is incorporated in the overall execution pipeline seamlessly.</span></span> <span data-ttu-id="de9d7-580">Si les propriétés de référence des paramètres des fonctions définies par l'utilisateur ne sont pas disponibles dans la valeur JSON, les paramètres sont considérés comme non définis et l'appel des fonctions définies par l'utilisateur est entièrement ignoré.</span><span class="sxs-lookup"><span data-stu-id="de9d7-580">If the properties referred to by the UDF parameters are not available in the JSON value, the parameter is considered as undefined and hence the UDF invocation is entirely skipped.</span></span> <span data-ttu-id="de9d7-581">De même, si le résultat des fonctions définies par l'utilisateur est indéfini, il n'est pas inclus dans le résultat.</span><span class="sxs-lookup"><span data-stu-id="de9d7-581">Similarly if the result of the UDF is undefined, it's not included in the result.</span></span> 

<span data-ttu-id="de9d7-582">En résumé, les fonctions définies par l'utilisateur sont des outils efficaces pour mener à bien des logiques métier complexes dans le cadre d'une requête.</span><span class="sxs-lookup"><span data-stu-id="de9d7-582">In summary, UDFs are great tools to do complex business logic as part of the query.</span></span>

### <a name="operator-evaluation"></a><span data-ttu-id="de9d7-583">Évaluation d'opérateur</span><span class="sxs-lookup"><span data-stu-id="de9d7-583">Operator evaluation</span></span>
<span data-ttu-id="de9d7-584">Cosmos DB, en sa qualité de base de données JSON, peut établir des correspondances entre les opérateurs JavaScript et sa sémantique d’évaluation.</span><span class="sxs-lookup"><span data-stu-id="de9d7-584">Cosmos DB, by the virtue of being a JSON database, draws parallels with JavaScript operators and its evaluation semantics.</span></span> <span data-ttu-id="de9d7-585">Même si Cosmos DB tente de préserver la sémantique JavaScript dans le cadre de la prise en charge JSON, l’opération d’évaluation dévie dans certains cas.</span><span class="sxs-lookup"><span data-stu-id="de9d7-585">While Cosmos DB tries to preserve JavaScript semantics in terms of JSON support, the operation evaluation deviates in some instances.</span></span>

<span data-ttu-id="de9d7-586">Dans le langage SQL de l’API DocumentDB, contrairement au langage SQL classique, les types de valeur sont souvent inconnus jusqu’à ce que les valeurs soient extraites de la base de données.</span><span class="sxs-lookup"><span data-stu-id="de9d7-586">In DocumentDB API SQL, unlike in traditional SQL, the types of values are often not known until the values are retrieved from database.</span></span> <span data-ttu-id="de9d7-587">Afin d'exécuter les requêtes de manière efficace, la plupart des opérateurs ont des exigences de type strictes.</span><span class="sxs-lookup"><span data-stu-id="de9d7-587">In order to efficiently execute queries, most of the operators have strict type requirements.</span></span> 

<span data-ttu-id="de9d7-588">Le langage SQL de l’API DocumentDB n’effectue pas de conversions implicites, contrairement à JavaScript.</span><span class="sxs-lookup"><span data-stu-id="de9d7-588">DocumentDB API SQL doesn't perform implicit conversions, unlike JavaScript.</span></span> <span data-ttu-id="de9d7-589">Par exemple, une requête comme `SELECT * FROM Person p WHERE p.Age = 21` correspond à des documents qui contiennent une propriété Age dont la valeur est 21.</span><span class="sxs-lookup"><span data-stu-id="de9d7-589">For instance, a query like `SELECT * FROM Person p WHERE p.Age = 21` matches documents that contain an Age property whose value is 21.</span></span> <span data-ttu-id="de9d7-590">Tout autre document dont la propriété Age correspond à la chaîne « 21 » ou à l'une de ses multiples variantes telles que « 021 », « 21.0 », « 0021 », « 00021 », etc. ne sera pas mis en correspondance.</span><span class="sxs-lookup"><span data-stu-id="de9d7-590">Any other document whose Age property matches string "21", or other possibly infinite variations like "021", "21.0", "0021", "00021", etc. will not be matched.</span></span> <span data-ttu-id="de9d7-591">Ce comportement contraste avec celui de JavaScript où les valeurs de chaîne sont implicitement converties en nombres (à partir de l’opérateur, par exemple :==).</span><span class="sxs-lookup"><span data-stu-id="de9d7-591">This is in contrast to the JavaScript where the string values are implicitly casted to numbers (based on operator, ex: ==).</span></span> <span data-ttu-id="de9d7-592">Ce choix est crucial pour une correspondance d’index efficace dans le langage SQL de l’API DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="de9d7-592">This choice is crucial for efficient index matching in DocumentDB API SQL.</span></span> 

## <a name="parameterized-sql-queries"></a><span data-ttu-id="de9d7-593">Requêtes SQL paramétrables</span><span class="sxs-lookup"><span data-stu-id="de9d7-593">Parameterized SQL queries</span></span>
<span data-ttu-id="de9d7-594">Cosmos DB prend en charge les requêtes avec des paramètres, exprimées avec la notation @ classique.</span><span class="sxs-lookup"><span data-stu-id="de9d7-594">Cosmos DB supports queries with parameters expressed with the familiar @ notation.</span></span> <span data-ttu-id="de9d7-595">SQL paramétré fournit une gestion et un échappement robustes de l'entrée utilisateur et empêche l'exposition accidentelle des données par l'intermédiaire de l'injection SQL.</span><span class="sxs-lookup"><span data-stu-id="de9d7-595">Parameterized SQL provides robust handling and escaping of user input, preventing accidental exposure of data through SQL injection.</span></span> 

<span data-ttu-id="de9d7-596">Par exemple, vous pouvez écrire une requête qui prend le nom et l'état de l'adresse comme paramètres, puis l'exécuter pour différentes valeurs de nom et d'état d'adresse en fonction de l'entrée utilisateur.</span><span class="sxs-lookup"><span data-stu-id="de9d7-596">For example, you can write a query that takes last name and address state as parameters, and then execute it for various values of last name and address state based on user input.</span></span>

    SELECT * 
    FROM Families f
    WHERE f.lastName = @lastName AND f.address.state = @addressState

<span data-ttu-id="de9d7-597">Cette demande peut ensuite être envoyée à Cosmos DB comme requête JSON paramétrable, tel qu’indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="de9d7-597">This request can then be sent to Cosmos DB as a parameterized JSON query like shown below.</span></span>

    {      
        "query": "SELECT * FROM Families f WHERE f.lastName = @lastName AND f.address.state = @addressState",     
        "parameters": [          
            {"name": "@lastName", "value": "Wakefield"},         
            {"name": "@addressState", "value": "NY"},           
        ] 
    }

<span data-ttu-id="de9d7-598">L'argument de l’opérateur TOP peut être défini à l'aide de requêtes paramétrables, comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="de9d7-598">The argument to TOP can be set using parameterized queries like shown below.</span></span>

    {      
        "query": "SELECT TOP @n * FROM Families",     
        "parameters": [          
            {"name": "@n", "value": 10},         
        ] 
    }

<span data-ttu-id="de9d7-599">Les valeurs de paramètres peuvent être n'importe quel format JSON valide (chaînes, nombres, valeurs booléennes, null, même des tableaux ou des valeurs JSON imbriquées).</span><span class="sxs-lookup"><span data-stu-id="de9d7-599">Parameter values can be any valid JSON (strings, numbers, Booleans, null, even arrays or nested JSON).</span></span> <span data-ttu-id="de9d7-600">De plus, comme Cosmos DB est sans schéma, les paramètres ne sont pas validés par rapport à un type.</span><span class="sxs-lookup"><span data-stu-id="de9d7-600">Also since Cosmos DB is schema-less, parameters are not validated against any type.</span></span>

## <span data-ttu-id="de9d7-601"><a id="BuiltinFunctions"></a>Fonctions intégrées</span><span class="sxs-lookup"><span data-stu-id="de9d7-601"><a id="BuiltinFunctions"></a>Built-in functions</span></span>
<span data-ttu-id="de9d7-602">Cosmos DB prend également en charge plusieurs fonctions intégrées pour des opérations courantes. Ces fonctions s’utilisent dans les requêtes comme les fonctions définies par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="de9d7-602">Cosmos DB also supports a number of built-in functions for common operations, that can be used inside queries like user-defined functions (UDFs).</span></span>

| <span data-ttu-id="de9d7-603">Groupe de fonctions</span><span class="sxs-lookup"><span data-stu-id="de9d7-603">Function group</span></span>          | <span data-ttu-id="de9d7-604">Opérations</span><span class="sxs-lookup"><span data-stu-id="de9d7-604">Operations</span></span>                                                                                                                                          |
|-------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="de9d7-605">Fonctions mathématiques</span><span class="sxs-lookup"><span data-stu-id="de9d7-605">Mathematical functions</span></span>  | <span data-ttu-id="de9d7-606">ABS, CEILING, EXP, FLOOR, LOG, LOG10, POWER, ROUND, SIGN, SQRT, SQUARE, TRUNC, ACOS, ASIN, ATAN, ATN2, COS, COT, DEGREES, PI, RADIANS, SIN et TAN</span><span class="sxs-lookup"><span data-stu-id="de9d7-606">ABS, CEILING, EXP, FLOOR, LOG, LOG10, POWER, ROUND, SIGN, SQRT, SQUARE, TRUNC, ACOS, ASIN, ATAN, ATN2, COS, COT, DEGREES, PI, RADIANS, SIN, and TAN</span></span> |
| <span data-ttu-id="de9d7-607">Fonctions de vérification du type</span><span class="sxs-lookup"><span data-stu-id="de9d7-607">Type checking functions</span></span> | <span data-ttu-id="de9d7-608">IS_ARRAY, IS_BOOL, IS_NULL, IS_NUMBER, IS_OBJECT, IS_STRING, IS_DEFINED et IS_PRIMITIVE</span><span class="sxs-lookup"><span data-stu-id="de9d7-608">IS_ARRAY, IS_BOOL, IS_NULL, IS_NUMBER, IS_OBJECT, IS_STRING, IS_DEFINED, and IS_PRIMITIVE</span></span>                                                           |
| <span data-ttu-id="de9d7-609">Fonctions de chaîne</span><span class="sxs-lookup"><span data-stu-id="de9d7-609">String functions</span></span>        | <span data-ttu-id="de9d7-610">CONCAT, CONTAINS, ENDSWITH, INDEX_OF, LEFT, LENGTH, LOWER, LTRIM, REPLACE, REPLICATE, REVERSE, RIGHT, RTRIM, STARTSWITH, SUBSTRING et UPPER</span><span class="sxs-lookup"><span data-stu-id="de9d7-610">CONCAT, CONTAINS, ENDSWITH, INDEX_OF, LEFT, LENGTH, LOWER, LTRIM, REPLACE, REPLICATE, REVERSE, RIGHT, RTRIM, STARTSWITH, SUBSTRING, and UPPER</span></span>       |
| <span data-ttu-id="de9d7-611">Fonctions de tableau</span><span class="sxs-lookup"><span data-stu-id="de9d7-611">Array functions</span></span>         | <span data-ttu-id="de9d7-612">ARRAY_CONCAT, ARRAY_CONTAINS, ARRAY_LENGTH et ARRAY_SLICE</span><span class="sxs-lookup"><span data-stu-id="de9d7-612">ARRAY_CONCAT, ARRAY_CONTAINS, ARRAY_LENGTH, and ARRAY_SLICE</span></span>                                                                                         |
| <span data-ttu-id="de9d7-613">Fonctions spatiales</span><span class="sxs-lookup"><span data-stu-id="de9d7-613">Spatial functions</span></span>       | <span data-ttu-id="de9d7-614">ST_DISTANCE, ST_WITHIN, ST_INTERSECTS, ST_ISVALID et ST_ISVALIDDETAILED</span><span class="sxs-lookup"><span data-stu-id="de9d7-614">ST_DISTANCE, ST_WITHIN, ST_INTERSECTS, ST_ISVALID, and ST_ISVALIDDETAILED</span></span>                                                                           | 

<span data-ttu-id="de9d7-615">Si vous utilisez actuellement une fonction définie par l’utilisateur pour laquelle une fonction intégrée est désormais disponible, remplacez-la par la fonction intégrée correspondante, car celle-ci s’exécutera plus rapidement et sera plus performante.</span><span class="sxs-lookup"><span data-stu-id="de9d7-615">If you’re currently using a user-defined function (UDF) for which a built-in function is now available, you should use the corresponding built-in function as it is going to be quicker to run and more efficiently.</span></span> 

### <a name="mathematical-functions"></a><span data-ttu-id="de9d7-616">Fonctions mathématiques</span><span class="sxs-lookup"><span data-stu-id="de9d7-616">Mathematical functions</span></span>
<span data-ttu-id="de9d7-617">Chaque fonction mathématique effectue un calcul, basé sur les valeurs d’entrée fournies comme arguments, et renvoie une valeur numérique.</span><span class="sxs-lookup"><span data-stu-id="de9d7-617">The mathematical functions each perform a calculation, based on input values that are provided as arguments, and return a numeric value.</span></span> <span data-ttu-id="de9d7-618">Ce tableau répertorie les fonctions mathématiques intégrées qui sont prises en charge.</span><span class="sxs-lookup"><span data-stu-id="de9d7-618">Here’s a table of supported built-in mathematical functions.</span></span>


| <span data-ttu-id="de9d7-619">Utilisation</span><span class="sxs-lookup"><span data-stu-id="de9d7-619">Usage</span></span> | <span data-ttu-id="de9d7-620">Description</span><span class="sxs-lookup"><span data-stu-id="de9d7-620">Description</span></span> |
|----------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="de9d7-621">[[ABS (num_expr)](#bk_abs)</span><span class="sxs-lookup"><span data-stu-id="de9d7-621">[[ABS (num_expr)](#bk_abs)</span></span> | <span data-ttu-id="de9d7-622">Retourne la valeur (positive) absolue de l'expression numérique spécifiée.</span><span class="sxs-lookup"><span data-stu-id="de9d7-622">Returns the absolute (positive) value of the specified numeric expression.</span></span> |
| [<span data-ttu-id="de9d7-623">CEILING (num_expr)</span><span class="sxs-lookup"><span data-stu-id="de9d7-623">CEILING (num_expr)</span></span>](#bk_ceiling) | <span data-ttu-id="de9d7-624">Retourne le plus petit nombre entier qui est supérieur ou égal à l'expression numérique spécifiée.</span><span class="sxs-lookup"><span data-stu-id="de9d7-624">Returns the smallest integer value greater than, or equal to, the specified numeric expression.</span></span> |
| [<span data-ttu-id="de9d7-625">FLOOR (num_expr)</span><span class="sxs-lookup"><span data-stu-id="de9d7-625">FLOOR (num_expr)</span></span>](#bk_floor) | <span data-ttu-id="de9d7-626">Retourne le plus grand nombre entier qui est inférieur ou égal à l'expression numérique spécifiée.</span><span class="sxs-lookup"><span data-stu-id="de9d7-626">Returns the largest integer less than or equal to the specified numeric expression.</span></span> |
| [<span data-ttu-id="de9d7-627">EXP (num_expr)</span><span class="sxs-lookup"><span data-stu-id="de9d7-627">EXP (num_expr)</span></span>](#bk_exp) | <span data-ttu-id="de9d7-628">Retourne l'exposant de l'expression numérique spécifiée.</span><span class="sxs-lookup"><span data-stu-id="de9d7-628">Returns the exponent of the specified numeric expression.</span></span> |
| <span data-ttu-id="de9d7-629">[LOG (num_expr [,base])](#bk_log)</span><span class="sxs-lookup"><span data-stu-id="de9d7-629">[LOG (num_expr [,base])](#bk_log)</span></span> | <span data-ttu-id="de9d7-630">Retourne le logarithme népérien de l'expression numérique spécifiée, ou le logarithme dans la base spécifiée.</span><span class="sxs-lookup"><span data-stu-id="de9d7-630">Returns the natural logarithm of the specified numeric expression, or the logarithm using the specified base</span></span> |
| [<span data-ttu-id="de9d7-631">LOG10 (num_expr)</span><span class="sxs-lookup"><span data-stu-id="de9d7-631">LOG10 (num_expr)</span></span>](#bk_log10) | <span data-ttu-id="de9d7-632">Retourne le logarithme en base 10 de l'expression numérique spécifiée.</span><span class="sxs-lookup"><span data-stu-id="de9d7-632">Returns the base-10 logarithmic value of the specified numeric expression.</span></span> |
| [<span data-ttu-id="de9d7-633">ROUND (num_expr)</span><span class="sxs-lookup"><span data-stu-id="de9d7-633">ROUND (num_expr)</span></span>](#bk_round) | <span data-ttu-id="de9d7-634">Retourne une valeur numérique, arrondie au nombre entier le plus proche.</span><span class="sxs-lookup"><span data-stu-id="de9d7-634">Returns a numeric value, rounded to the closest integer value.</span></span> |
| [<span data-ttu-id="de9d7-635">TRUNC (num_expr)</span><span class="sxs-lookup"><span data-stu-id="de9d7-635">TRUNC (num_expr)</span></span>](#bk_trunc) | <span data-ttu-id="de9d7-636">Retourne une valeur numérique, tronquée au nombre entier le plus proche.</span><span class="sxs-lookup"><span data-stu-id="de9d7-636">Returns a numeric value, truncated to the closest integer value.</span></span> |
| [<span data-ttu-id="de9d7-637">SQRT (num_expr)</span><span class="sxs-lookup"><span data-stu-id="de9d7-637">SQRT (num_expr)</span></span>](#bk_sqrt) | <span data-ttu-id="de9d7-638">Retourne la racine carrée de l'expression numérique spécifiée.</span><span class="sxs-lookup"><span data-stu-id="de9d7-638">Returns the square root of the specified numeric expression.</span></span> |
| [<span data-ttu-id="de9d7-639">SQUARE (num_expr)</span><span class="sxs-lookup"><span data-stu-id="de9d7-639">SQUARE (num_expr)</span></span>](#bk_square) | <span data-ttu-id="de9d7-640">Retourne le carré de l'expression numérique spécifiée.</span><span class="sxs-lookup"><span data-stu-id="de9d7-640">Returns the square of the specified numeric expression.</span></span> |
| [<span data-ttu-id="de9d7-641">POWER (num_expr, num_expr)</span><span class="sxs-lookup"><span data-stu-id="de9d7-641">POWER (num_expr, num_expr)</span></span>](#bk_power) | <span data-ttu-id="de9d7-642">Renvoie un nombre spécifié élevé à la puissance spécifiée.</span><span class="sxs-lookup"><span data-stu-id="de9d7-642">Returns the power of the specified numeric expression to the value specified.</span></span> |
| [<span data-ttu-id="de9d7-643">SIGN (num_expr)</span><span class="sxs-lookup"><span data-stu-id="de9d7-643">SIGN (num_expr)</span></span>](#bk_sign) | <span data-ttu-id="de9d7-644">Retourne la valeur du signe (-1, 0, 1) de l'expression numérique spécifiée.</span><span class="sxs-lookup"><span data-stu-id="de9d7-644">Returns the sign value (-1, 0, 1) of the specified numeric expression.</span></span> |
| [<span data-ttu-id="de9d7-645">ACOS (num_expr)</span><span class="sxs-lookup"><span data-stu-id="de9d7-645">ACOS (num_expr)</span></span>](#bk_acos) | <span data-ttu-id="de9d7-646">Retourne l’angle, en radians, dont le cosinus est l’expression numérique spécifiée ; également appelée arccosinus.</span><span class="sxs-lookup"><span data-stu-id="de9d7-646">Returns the angle, in radians, whose cosine is the specified numeric expression; also called arccosine.</span></span> |
| [<span data-ttu-id="de9d7-647">ASIN (num_expr)</span><span class="sxs-lookup"><span data-stu-id="de9d7-647">ASIN (num_expr)</span></span>](#bk_asin) | <span data-ttu-id="de9d7-648">Retourne l’angle, en radians, dont le sinus est l’expression numérique spécifiée.</span><span class="sxs-lookup"><span data-stu-id="de9d7-648">Returns the angle, in radians, whose sine is the specified numeric expression.</span></span> <span data-ttu-id="de9d7-649">Cette fonction est également appelée arcsinus.</span><span class="sxs-lookup"><span data-stu-id="de9d7-649">This is also called arcsine.</span></span> |
| [<span data-ttu-id="de9d7-650">ATAN (num_expr)</span><span class="sxs-lookup"><span data-stu-id="de9d7-650">ATAN (num_expr)</span></span>](#bk_atan) | <span data-ttu-id="de9d7-651">Retourne l’angle, en radians, dont la tangente est l’expression numérique spécifiée.</span><span class="sxs-lookup"><span data-stu-id="de9d7-651">Returns the angle, in radians, whose tangent is the specified numeric expression.</span></span> <span data-ttu-id="de9d7-652">Cette fonction est également appelée arctangente.</span><span class="sxs-lookup"><span data-stu-id="de9d7-652">This is also called arctangent.</span></span> |
| [<span data-ttu-id="de9d7-653">ATN2 (num_expr)</span><span class="sxs-lookup"><span data-stu-id="de9d7-653">ATN2 (num_expr)</span></span>](#bk_atn2) | <span data-ttu-id="de9d7-654">Retourne l’angle, en radians, entre l’axe des abscisses positives et le rayon depuis l’origine vers le point (y, x), où x et y sont les valeurs des deux expressions flottantes spécifiées.</span><span class="sxs-lookup"><span data-stu-id="de9d7-654">Returns the angle, in radians, between the positive x-axis and the ray from the origin to the point (y, x), where x and y are the values of the two specified float expressions.</span></span> |
| [<span data-ttu-id="de9d7-655">COS (num_expr)</span><span class="sxs-lookup"><span data-stu-id="de9d7-655">COS (num_expr)</span></span>](#bk_cos) | <span data-ttu-id="de9d7-656">Retourne le cosinus trigonométrique de l’angle spécifié, en radians, dans l’expression spécifiée.</span><span class="sxs-lookup"><span data-stu-id="de9d7-656">Returns the trigonometric cosine of the specified angle, in radians, in the specified expression.</span></span> |
| [<span data-ttu-id="de9d7-657">COT (num_expr)</span><span class="sxs-lookup"><span data-stu-id="de9d7-657">COT (num_expr)</span></span>](#bk_cot) | <span data-ttu-id="de9d7-658">Retourne la cotangente trigonométrique de l’angle spécifié, en radians, dans l’expression numérique spécifiée.</span><span class="sxs-lookup"><span data-stu-id="de9d7-658">Returns the trigonometric cotangent of the specified angle, in radians, in the specified numeric expression.</span></span> |
| [<span data-ttu-id="de9d7-659">DEGREES (num_expr)</span><span class="sxs-lookup"><span data-stu-id="de9d7-659">DEGREES (num_expr)</span></span>](#bk_degrees) | <span data-ttu-id="de9d7-660">Retourne l’angle correspondant en degrés d’un angle spécifié en radians.</span><span class="sxs-lookup"><span data-stu-id="de9d7-660">Returns the corresponding angle in degrees for an angle specified in radians.</span></span> |
| [<span data-ttu-id="de9d7-661">PI ()</span><span class="sxs-lookup"><span data-stu-id="de9d7-661">PI ()</span></span>](#bk_pi) | <span data-ttu-id="de9d7-662">Retourne la valeur constante de PI.</span><span class="sxs-lookup"><span data-stu-id="de9d7-662">Returns the constant value of PI.</span></span> |
| [<span data-ttu-id="de9d7-663">RADIANS (num_expr)</span><span class="sxs-lookup"><span data-stu-id="de9d7-663">RADIANS (num_expr)</span></span>](#bk_radians) | <span data-ttu-id="de9d7-664">Retourne des radians lorsqu’une expression numérique, en degrés, est entrée.</span><span class="sxs-lookup"><span data-stu-id="de9d7-664">Returns radians when a numeric expression, in degrees, is entered.</span></span> |
| [<span data-ttu-id="de9d7-665">SIN (num_expr)</span><span class="sxs-lookup"><span data-stu-id="de9d7-665">SIN (num_expr)</span></span>](#bk_sin) | <span data-ttu-id="de9d7-666">Retourne le sinus trigonométrique de l’angle spécifié, en radians, dans l’expression spécifiée.</span><span class="sxs-lookup"><span data-stu-id="de9d7-666">Returns the trigonometric sine of the specified angle, in radians, in the specified expression.</span></span> |
| [<span data-ttu-id="de9d7-667">TAN (num_expr)</span><span class="sxs-lookup"><span data-stu-id="de9d7-667">TAN (num_expr)</span></span>](#bk_tan) | <span data-ttu-id="de9d7-668">Retourne la tangente de l’expression d’entrée, dans l’expression spécifiée.</span><span class="sxs-lookup"><span data-stu-id="de9d7-668">Returns the tangent of the input expression, in the specified expression.</span></span> |

<span data-ttu-id="de9d7-669">Par exemple, vous pouvez désormais exécuter des requêtes similaires à celle-ci :</span><span class="sxs-lookup"><span data-stu-id="de9d7-669">For example, you can now run queries like the following:</span></span>

<span data-ttu-id="de9d7-670">**Requête**</span><span class="sxs-lookup"><span data-stu-id="de9d7-670">**Query**</span></span>

    SELECT VALUE ABS(-4)

<span data-ttu-id="de9d7-671">**Résultats**</span><span class="sxs-lookup"><span data-stu-id="de9d7-671">**Results**</span></span>

    [4]

<span data-ttu-id="de9d7-672">La principale différence entre les fonctions de Cosmos DB et le langage SQL ANSI est que les fonctions sont conçues pour s’exécuter avec des données sans schéma et des données avec un schéma mixte.</span><span class="sxs-lookup"><span data-stu-id="de9d7-672">The main difference between Cosmos DB’s functions compared to ANSI SQL is that they are designed to work well with schema-less and mixed schema data.</span></span> <span data-ttu-id="de9d7-673">Par exemple, si vous avez un document pour lequel la propriété Size est manquante ou a une valeur non numérique (de type « inconnu »), le document est ignoré, et aucune erreur n'est retournée.</span><span class="sxs-lookup"><span data-stu-id="de9d7-673">For example, if you have a document where the Size property is missing, or has a non-numeric value like “unknown”, then the document is skipped over, instead of returning an error.</span></span>

### <a name="type-checking-functions"></a><span data-ttu-id="de9d7-674">Fonctions de vérification du type</span><span class="sxs-lookup"><span data-stu-id="de9d7-674">Type checking functions</span></span>
<span data-ttu-id="de9d7-675">Les fonctions de vérification du type vous permettent de vérifier le type d'une expression donnée dans les requêtes SQL.</span><span class="sxs-lookup"><span data-stu-id="de9d7-675">The type checking functions allow you to check the type of an expression within SQL queries.</span></span> <span data-ttu-id="de9d7-676">Elles peuvent être utilisées pour déterminer instantanément le type variable ou inconnu des propriétés dans les documents.</span><span class="sxs-lookup"><span data-stu-id="de9d7-676">Type checking functions can be used to determine the type of properties within documents on the fly when it is variable or unknown.</span></span> <span data-ttu-id="de9d7-677">Le tableau répertorie les fonctions de vérification du type intégrées qui sont prises en charge.</span><span class="sxs-lookup"><span data-stu-id="de9d7-677">Here’s a table of supported built-in type checking functions.</span></span>

<table>
<tr>
  <td><span data-ttu-id="de9d7-678"><strong>Utilisation</strong></span><span class="sxs-lookup"><span data-stu-id="de9d7-678"><strong>Usage</strong></span></span></td>
  <td><span data-ttu-id="de9d7-679"><strong>Description</strong></span><span class="sxs-lookup"><span data-stu-id="de9d7-679"><strong>Description</strong></span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="de9d7-680"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_array">IS_ARRAY (expr)</a></span><span class="sxs-lookup"><span data-stu-id="de9d7-680"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_array">IS_ARRAY (expr)</a></span></span></td>
  <td><span data-ttu-id="de9d7-681">Retourne une valeur booléenne indiquant si la valeur est du type tableau.</span><span class="sxs-lookup"><span data-stu-id="de9d7-681">Returns a Boolean indicating if the type of the value is an array.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="de9d7-682"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_bool">IS_BOOL (expr)</a></span><span class="sxs-lookup"><span data-stu-id="de9d7-682"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_bool">IS_BOOL (expr)</a></span></span></td>
  <td><span data-ttu-id="de9d7-683">Retourne une valeur booléenne indiquant si la valeur est du type booléen.</span><span class="sxs-lookup"><span data-stu-id="de9d7-683">Returns a Boolean indicating if the type of the value is a Boolean.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="de9d7-684"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_null">IS_NULL (expr)</a></span><span class="sxs-lookup"><span data-stu-id="de9d7-684"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_null">IS_NULL (expr)</a></span></span></td>
  <td><span data-ttu-id="de9d7-685">Retourne une valeur booléenne indiquant si la valeur est du type null.</span><span class="sxs-lookup"><span data-stu-id="de9d7-685">Returns a Boolean indicating if the type of the value is null.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="de9d7-686"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_number">IS_NUMBER (expr)</a></span><span class="sxs-lookup"><span data-stu-id="de9d7-686"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_number">IS_NUMBER (expr)</a></span></span></td>
  <td><span data-ttu-id="de9d7-687">Retourne une valeur booléenne indiquant si la valeur est du type numérique.</span><span class="sxs-lookup"><span data-stu-id="de9d7-687">Returns a Boolean indicating if the type of the value is a number.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="de9d7-688"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_object">IS_OBJECT (expr)</a></span><span class="sxs-lookup"><span data-stu-id="de9d7-688"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_object">IS_OBJECT (expr)</a></span></span></td>
  <td><span data-ttu-id="de9d7-689">Retourne une valeur booléenne indiquant si la valeur est du type objet JSON.</span><span class="sxs-lookup"><span data-stu-id="de9d7-689">Returns a Boolean indicating if the type of the value is a JSON object.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="de9d7-690"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_string">IS_STRING (expr)</a></span><span class="sxs-lookup"><span data-stu-id="de9d7-690"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_string">IS_STRING (expr)</a></span></span></td>
  <td><span data-ttu-id="de9d7-691">Retourne une valeur booléenne indiquant si la valeur est du type chaîne.</span><span class="sxs-lookup"><span data-stu-id="de9d7-691">Returns a Boolean indicating if the type of the value is a string.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="de9d7-692"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_defined">IS_DEFINED (expr)</a></span><span class="sxs-lookup"><span data-stu-id="de9d7-692"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_defined">IS_DEFINED (expr)</a></span></span></td>
  <td><span data-ttu-id="de9d7-693">Retourne une valeur booléenne indiquant si une valeur a été attribuée à la propriété.</span><span class="sxs-lookup"><span data-stu-id="de9d7-693">Returns a Boolean indicating if the property has been assigned a value.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="de9d7-694"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_primitive">IS_PRIMITIVE (expr)</a></span><span class="sxs-lookup"><span data-stu-id="de9d7-694"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_primitive">IS_PRIMITIVE (expr)</a></span></span></td>
  <td><span data-ttu-id="de9d7-695">Retourne une valeur booléenne indiquant si la valeur est du type chaîne, nombre, valeur booléenne ou Null.</span><span class="sxs-lookup"><span data-stu-id="de9d7-695">Returns a Boolean indicating if the type of the value is a string, number, Boolean or null.</span></span></td>
</tr>

</table>

<span data-ttu-id="de9d7-696">Avec ces fonctions, vous pouvez désormais exécuter des requêtes similaires à celle-ci :</span><span class="sxs-lookup"><span data-stu-id="de9d7-696">Using these functions, you can now run queries like the following:</span></span>

<span data-ttu-id="de9d7-697">**Requête**</span><span class="sxs-lookup"><span data-stu-id="de9d7-697">**Query**</span></span>

    SELECT VALUE IS_NUMBER(-4)

<span data-ttu-id="de9d7-698">**Résultats**</span><span class="sxs-lookup"><span data-stu-id="de9d7-698">**Results**</span></span>

    [true]

### <a name="string-functions"></a><span data-ttu-id="de9d7-699">Fonctions de chaîne</span><span class="sxs-lookup"><span data-stu-id="de9d7-699">String functions</span></span>
<span data-ttu-id="de9d7-700">Les fonctions scalaires suivantes effectuent une opération sur une valeur d’entrée de chaîne et retournent une valeur de type chaîne, une valeur numérique ou une valeur booléenne.</span><span class="sxs-lookup"><span data-stu-id="de9d7-700">The following scalar functions perform an operation on a string input value and return a string, numeric or Boolean value.</span></span> <span data-ttu-id="de9d7-701">Voici un tableau des fonctions de chaîne intégrées :</span><span class="sxs-lookup"><span data-stu-id="de9d7-701">Here's a table of built-in string functions:</span></span>

| <span data-ttu-id="de9d7-702">Utilisation</span><span class="sxs-lookup"><span data-stu-id="de9d7-702">Usage</span></span> | <span data-ttu-id="de9d7-703">Description</span><span class="sxs-lookup"><span data-stu-id="de9d7-703">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="de9d7-704">LENGTH (str_expr)</span><span class="sxs-lookup"><span data-stu-id="de9d7-704">LENGTH (str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_length) |<span data-ttu-id="de9d7-705">Retourne le nombre de caractères de l’expression de chaîne spécifiée.</span><span class="sxs-lookup"><span data-stu-id="de9d7-705">Returns the number of characters of the specified string expression</span></span> |
| <span data-ttu-id="de9d7-706">[CONCAT (str_expr, str_expr [, str_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_concat)</span><span class="sxs-lookup"><span data-stu-id="de9d7-706">[CONCAT (str_expr, str_expr [, str_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_concat)</span></span> |<span data-ttu-id="de9d7-707">Retourne une chaîne qui est le résultat de la concaténation d’au moins deux valeurs de chaîne.</span><span class="sxs-lookup"><span data-stu-id="de9d7-707">Returns a string that is the result of concatenating two or more string values.</span></span> |
| [<span data-ttu-id="de9d7-708">SUBSTRING (str_expr, num_expr, num_expr)</span><span class="sxs-lookup"><span data-stu-id="de9d7-708">SUBSTRING (str_expr, num_expr, num_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_substring) |<span data-ttu-id="de9d7-709">Retourne une partie d’une expression de chaîne.</span><span class="sxs-lookup"><span data-stu-id="de9d7-709">Returns part of a string expression.</span></span> |
| [<span data-ttu-id="de9d7-710">STARTSWITH (str_expr, str_expr)</span><span class="sxs-lookup"><span data-stu-id="de9d7-710">STARTSWITH (str_expr, str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_startswith) |<span data-ttu-id="de9d7-711">Retourne une valeur booléenne indiquant si la première expression de chaîne se termine par la seconde.</span><span class="sxs-lookup"><span data-stu-id="de9d7-711">Returns a Boolean indicating whether the first string expression ends with the second</span></span> |
| [<span data-ttu-id="de9d7-712">ENDSWITH (str_expr, str_expr)</span><span class="sxs-lookup"><span data-stu-id="de9d7-712">ENDSWITH (str_expr, str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_endswith) |<span data-ttu-id="de9d7-713">Retourne une valeur booléenne indiquant si la première expression de chaîne se termine par la seconde.</span><span class="sxs-lookup"><span data-stu-id="de9d7-713">Returns a Boolean indicating whether the first string expression ends with the second</span></span> |
| [<span data-ttu-id="de9d7-714">CONTAINS (str_expr, str_expr)</span><span class="sxs-lookup"><span data-stu-id="de9d7-714">CONTAINS (str_expr, str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_contains) |<span data-ttu-id="de9d7-715">Retourne une valeur booléenne indiquant si la première expression de chaîne contient la seconde.</span><span class="sxs-lookup"><span data-stu-id="de9d7-715">Returns a Boolean indicating whether the first string expression contains the second.</span></span> |
| [<span data-ttu-id="de9d7-716">INDEX_OF (str_expr, str_expr)</span><span class="sxs-lookup"><span data-stu-id="de9d7-716">INDEX_OF (str_expr, str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_index_of) |<span data-ttu-id="de9d7-717">Retourne la position de départ de la première occurrence de la seconde expression de chaîne dans la première expression de chaîne spécifiée, ou -1 si la chaîne est introuvable.</span><span class="sxs-lookup"><span data-stu-id="de9d7-717">Returns the starting position of the first occurrence of the second string expression within the first specified string expression, or -1 if the string is not found.</span></span> |
| [<span data-ttu-id="de9d7-718">LEFT (str_expr, num_expr)</span><span class="sxs-lookup"><span data-stu-id="de9d7-718">LEFT (str_expr, num_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_left) |<span data-ttu-id="de9d7-719">Retourne la partie gauche d’une chaîne avec le nombre de caractères spécifié.</span><span class="sxs-lookup"><span data-stu-id="de9d7-719">Returns the left part of a string with the specified number of characters.</span></span> |
| [<span data-ttu-id="de9d7-720">RIGHT (str_expr, num_expr)</span><span class="sxs-lookup"><span data-stu-id="de9d7-720">RIGHT (str_expr, num_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_right) |<span data-ttu-id="de9d7-721">Retourne la partie droite d’une chaîne avec le nombre de caractères spécifié.</span><span class="sxs-lookup"><span data-stu-id="de9d7-721">Returns the right part of a string with the specified number of characters.</span></span> |
| [<span data-ttu-id="de9d7-722">LTRIM (str_expr)</span><span class="sxs-lookup"><span data-stu-id="de9d7-722">LTRIM (str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_ltrim) |<span data-ttu-id="de9d7-723">Retourne une expression de chaîne après avoir supprimé les espaces de début.</span><span class="sxs-lookup"><span data-stu-id="de9d7-723">Returns a string expression after it removes leading blanks.</span></span> |
| [<span data-ttu-id="de9d7-724">RTRIM (str_expr)</span><span class="sxs-lookup"><span data-stu-id="de9d7-724">RTRIM (str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_rtrim) |<span data-ttu-id="de9d7-725">Retourne une expression de chaîne après avoir tronqué tous les espaces de fin.</span><span class="sxs-lookup"><span data-stu-id="de9d7-725">Returns a string expression after truncating all trailing blanks.</span></span> |
| [<span data-ttu-id="de9d7-726">LOWER (str_expr)</span><span class="sxs-lookup"><span data-stu-id="de9d7-726">LOWER (str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_lower) |<span data-ttu-id="de9d7-727">Retourne une expression de chaîne après la conversion des caractères majuscules en caractères minuscules.</span><span class="sxs-lookup"><span data-stu-id="de9d7-727">Returns a string expression after converting uppercase character data to lowercase.</span></span> |
| [<span data-ttu-id="de9d7-728">UPPER (str_expr)</span><span class="sxs-lookup"><span data-stu-id="de9d7-728">UPPER (str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_upper) |<span data-ttu-id="de9d7-729">Retourne une expression de chaîne après la conversion des caractères minuscules en caractères majuscules.</span><span class="sxs-lookup"><span data-stu-id="de9d7-729">Returns a string expression after converting lowercase character data to uppercase.</span></span> |
| [<span data-ttu-id="de9d7-730">REPLACE (str_expr, str_expr, str_expr)</span><span class="sxs-lookup"><span data-stu-id="de9d7-730">REPLACE (str_expr, str_expr, str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_replace) |<span data-ttu-id="de9d7-731">Remplace toutes les occurrences d’une valeur de chaîne spécifiée par une autre valeur de chaîne.</span><span class="sxs-lookup"><span data-stu-id="de9d7-731">Replaces all occurrences of a specified string value with another string value.</span></span> |
| [<span data-ttu-id="de9d7-732">REPLICATE (str_expr, num_expr)</span><span class="sxs-lookup"><span data-stu-id="de9d7-732">REPLICATE (str_expr, num_expr)</span></span>](https://docs.microsoft.com/azure/cosmos-db/documentdb-sql-query-reference#bk_replicate) |<span data-ttu-id="de9d7-733">Répète une valeur de chaîne un nombre de fois spécifié.</span><span class="sxs-lookup"><span data-stu-id="de9d7-733">Repeats a string value a specified number of times.</span></span> |
| [<span data-ttu-id="de9d7-734">REVERSE (str_expr)</span><span class="sxs-lookup"><span data-stu-id="de9d7-734">REVERSE (str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_reverse) |<span data-ttu-id="de9d7-735">Retourne l’ordre inverse d’une valeur de chaîne.</span><span class="sxs-lookup"><span data-stu-id="de9d7-735">Returns the reverse order of a string value.</span></span> |

<span data-ttu-id="de9d7-736">Avec ces fonctions, vous pouvez désormais exécuter des requêtes similaires aux suivantes.</span><span class="sxs-lookup"><span data-stu-id="de9d7-736">Using these functions, you can now run queries like the following.</span></span> <span data-ttu-id="de9d7-737">Par exemple, vous pouvez retourner le nom de famille en majuscules comme suit :</span><span class="sxs-lookup"><span data-stu-id="de9d7-737">For example, you can return the family name in uppercase as follows:</span></span>

<span data-ttu-id="de9d7-738">**Requête**</span><span class="sxs-lookup"><span data-stu-id="de9d7-738">**Query**</span></span>

    SELECT VALUE UPPER(Families.id)
    FROM Families

<span data-ttu-id="de9d7-739">**Résultats**</span><span class="sxs-lookup"><span data-stu-id="de9d7-739">**Results**</span></span>

    [
        "WAKEFIELDFAMILY", 
        "ANDERSENFAMILY"
    ]

<span data-ttu-id="de9d7-740">Vous pouvez également concaténer des chaînes, comme dans cet exemple :</span><span class="sxs-lookup"><span data-stu-id="de9d7-740">Or concatenate strings like in this example:</span></span>

<span data-ttu-id="de9d7-741">**Requête**</span><span class="sxs-lookup"><span data-stu-id="de9d7-741">**Query**</span></span>

    SELECT Families.id, CONCAT(Families.address.city, ",", Families.address.state) AS location
    FROM Families

<span data-ttu-id="de9d7-742">**Résultats**</span><span class="sxs-lookup"><span data-stu-id="de9d7-742">**Results**</span></span>

    [{
      "id": "WakefieldFamily",
      "location": "NY,NY"
    },
    {
      "id": "AndersenFamily",
      "location": "seattle,WA"
    }]


<span data-ttu-id="de9d7-743">Les fonctions de chaîne peuvent également être utilisées dans la clause WHERE pour filtrer les résultats, comme dans l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="de9d7-743">String functions can also be used in the WHERE clause to filter results, like in the following example:</span></span>

<span data-ttu-id="de9d7-744">**Requête**</span><span class="sxs-lookup"><span data-stu-id="de9d7-744">**Query**</span></span>

    SELECT Families.id, Families.address.city
    FROM Families
    WHERE STARTSWITH(Families.id, "Wakefield")

<span data-ttu-id="de9d7-745">**Résultats**</span><span class="sxs-lookup"><span data-stu-id="de9d7-745">**Results**</span></span>

    [{
      "id": "WakefieldFamily",
      "city": "NY"
    }]

### <a name="array-functions"></a><span data-ttu-id="de9d7-746">Fonctions de tableau</span><span class="sxs-lookup"><span data-stu-id="de9d7-746">Array functions</span></span>
<span data-ttu-id="de9d7-747">Les fonctions scalaires suivantes effectuent une opération sur une valeur d’entrée de tableau et retournent une valeur numérique, une valeur booléenne ou une valeur de tableau.</span><span class="sxs-lookup"><span data-stu-id="de9d7-747">The following scalar functions perform an operation on an array input value and return numeric, Boolean or array value.</span></span> <span data-ttu-id="de9d7-748">Voici un tableau des fonctions de tableau intégrées :</span><span class="sxs-lookup"><span data-stu-id="de9d7-748">Here's a table of built-in array functions:</span></span>

| <span data-ttu-id="de9d7-749">Utilisation</span><span class="sxs-lookup"><span data-stu-id="de9d7-749">Usage</span></span> | <span data-ttu-id="de9d7-750">Description</span><span class="sxs-lookup"><span data-stu-id="de9d7-750">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="de9d7-751">ARRAY_LENGTH (arr_expr)</span><span class="sxs-lookup"><span data-stu-id="de9d7-751">ARRAY_LENGTH (arr_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_length) |<span data-ttu-id="de9d7-752">Retourne le nombre d’éléments de l’expression de tableau spécifiée.</span><span class="sxs-lookup"><span data-stu-id="de9d7-752">Returns the number of elements of the specified array expression.</span></span> |
| <span data-ttu-id="de9d7-753">[ARRAY_CONCAT (arr_expr, arr_expr [, arr_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_concat)</span><span class="sxs-lookup"><span data-stu-id="de9d7-753">[ARRAY_CONCAT (arr_expr, arr_expr [, arr_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_concat)</span></span> |<span data-ttu-id="de9d7-754">Retourne un tableau qui est le résultat de la concaténation d’au moins deux valeurs de tableau.</span><span class="sxs-lookup"><span data-stu-id="de9d7-754">Returns an array that is the result of concatenating two or more array values.</span></span> |
| <span data-ttu-id="de9d7-755">[ARRAY_CONTAINS (arr_expr, expr [, bool_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_contains)</span><span class="sxs-lookup"><span data-stu-id="de9d7-755">[ARRAY_CONTAINS (arr_expr, expr [, bool_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_contains)</span></span> |<span data-ttu-id="de9d7-756">Retourne une valeur booléenne qui indique si le tableau contient la valeur spécifiée.</span><span class="sxs-lookup"><span data-stu-id="de9d7-756">Returns a Boolean indicating whether the array contains the specified value.</span></span> <span data-ttu-id="de9d7-757">Peut spécifier si la correspondance est totale ou partielle.</span><span class="sxs-lookup"><span data-stu-id="de9d7-757">Can specify if the match is full or partial.</span></span> |
| <span data-ttu-id="de9d7-758">[ARRAY_SLICE (arr_expr, num_expr [, num_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_slice)</span><span class="sxs-lookup"><span data-stu-id="de9d7-758">[ARRAY_SLICE (arr_expr, num_expr [, num_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_slice)</span></span> |<span data-ttu-id="de9d7-759">Retourne une partie d’une expression de tableau.</span><span class="sxs-lookup"><span data-stu-id="de9d7-759">Returns part of an array expression.</span></span> |

<span data-ttu-id="de9d7-760">Les fonctions de tableau permettent de manipuler des tableaux dans JSON.</span><span class="sxs-lookup"><span data-stu-id="de9d7-760">Array functions can be used to manipulate arrays within JSON.</span></span> <span data-ttu-id="de9d7-761">Par exemple, voici une requête qui retourne tous les documents dans lesquels l’un des parents est « Robin Wakefield ».</span><span class="sxs-lookup"><span data-stu-id="de9d7-761">For example, here's a query that returns all documents where one of the parents is "Robin Wakefield".</span></span> 

<span data-ttu-id="de9d7-762">**Requête**</span><span class="sxs-lookup"><span data-stu-id="de9d7-762">**Query**</span></span>

    SELECT Families.id 
    FROM Families 
    WHERE ARRAY_CONTAINS(Families.parents, { givenName: "Robin", familyName: "Wakefield" })

<span data-ttu-id="de9d7-763">**Résultats**</span><span class="sxs-lookup"><span data-stu-id="de9d7-763">**Results**</span></span>

    [{
      "id": "WakefieldFamily"
    }]

<span data-ttu-id="de9d7-764">Vous pouvez spécifier un fragment partiel pour faire correspondre des éléments dans le tableau.</span><span class="sxs-lookup"><span data-stu-id="de9d7-764">You can specify a partial fragment for matching elements within the array.</span></span> <span data-ttu-id="de9d7-765">La requête suivante recherche tous les parents avec le `givenName` `Robin`.</span><span class="sxs-lookup"><span data-stu-id="de9d7-765">The following query finds all parents with the `givenName` of `Robin`.</span></span>

<span data-ttu-id="de9d7-766">**Requête**</span><span class="sxs-lookup"><span data-stu-id="de9d7-766">**Query**</span></span>

    SELECT Families.id 
    FROM Families 
    WHERE ARRAY_CONTAINS(Families.parents, { givenName: "Robin" }, true)

<span data-ttu-id="de9d7-767">**Résultats**</span><span class="sxs-lookup"><span data-stu-id="de9d7-767">**Results**</span></span>

    [{
      "id": "WakefieldFamily"
    }]


<span data-ttu-id="de9d7-768">Voici un autre exemple dans lequel la fonction ARRAY_LENGTH est utilisée pour obtenir le nombre d’enfants par famille.</span><span class="sxs-lookup"><span data-stu-id="de9d7-768">Here's another example that uses ARRAY_LENGTH to get the number of children per family.</span></span>

<span data-ttu-id="de9d7-769">**Requête**</span><span class="sxs-lookup"><span data-stu-id="de9d7-769">**Query**</span></span>

    SELECT Families.id, ARRAY_LENGTH(Families.children) AS numberOfChildren
    FROM Families 

<span data-ttu-id="de9d7-770">**Résultats**</span><span class="sxs-lookup"><span data-stu-id="de9d7-770">**Results**</span></span>

    [{
      "id": "WakefieldFamily",
      "numberOfChildren": 2
    },
    {
      "id": "AndersenFamily",
      "numberOfChildren": 1
    }]

### <a name="spatial-functions"></a><span data-ttu-id="de9d7-771">Fonctions spatiales</span><span class="sxs-lookup"><span data-stu-id="de9d7-771">Spatial functions</span></span>
<span data-ttu-id="de9d7-772">Cosmos DB prend en charge les fonctions intégrées Open Geospatial Consortium (OGC) suivantes pour les requêtes géospatiales.</span><span class="sxs-lookup"><span data-stu-id="de9d7-772">Cosmos DB supports the following Open Geospatial Consortium (OGC) built-in functions for geospatial querying.</span></span> 

<table>
<tr>
  <td><span data-ttu-id="de9d7-773"><strong>Utilisation</strong></span><span class="sxs-lookup"><span data-stu-id="de9d7-773"><strong>Usage</strong></span></span></td>
  <td><span data-ttu-id="de9d7-774"><strong>Description</strong></span><span class="sxs-lookup"><span data-stu-id="de9d7-774"><strong>Description</strong></span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="de9d7-775">ST_DISTANCE (point_expr, point_expr)</span><span class="sxs-lookup"><span data-stu-id="de9d7-775">ST_DISTANCE (point_expr, point_expr)</span></span></td>
  <td><span data-ttu-id="de9d7-776">Renvoie la distance entre les deux expressions Point, Polygone ou LineString de GeoJSON.</span><span class="sxs-lookup"><span data-stu-id="de9d7-776">Returns the distance between the two GeoJSON Point, Polygon, or LineString expressions.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="de9d7-777">ST_WITHIN (point_expr, polygon_expr)</span><span class="sxs-lookup"><span data-stu-id="de9d7-777">ST_WITHIN (point_expr, polygon_expr)</span></span></td>
  <td><span data-ttu-id="de9d7-778">Renvoie une expression booléenne indiquant si le premier objet GeoJSON (Point, Polygone ou LineString) se trouve dans le second objet GeoJSON (Point, Polygone ou LineString).</span><span class="sxs-lookup"><span data-stu-id="de9d7-778">Returns a Boolean expression indicating whether the first GeoJSON object (Point, Polygon, or LineString) is within the second GeoJSON object (Point, Polygon, or LineString).</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="de9d7-779">ST_INTERSECTS (spatial_expr, spatial_expr)</span><span class="sxs-lookup"><span data-stu-id="de9d7-779">ST_INTERSECTS (spatial_expr, spatial_expr)</span></span></td>
  <td><span data-ttu-id="de9d7-780">Retourne une expression booléenne indiquant si les deux objets GeoJSON spécifiés (Point, Polygone ou LineString) se croisent.</span><span class="sxs-lookup"><span data-stu-id="de9d7-780">Returns a Boolean expression indicating whether the two specified GeoJSON objects (Point, Polygon, or LineString) intersect.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="de9d7-781">ST_ISVALID</span><span class="sxs-lookup"><span data-stu-id="de9d7-781">ST_ISVALID</span></span></td>
  <td><span data-ttu-id="de9d7-782">Renvoie une valeur booléenne indiquant si l’expression Point, Polygone ou LineString GeoJSON spécifiée est valide.</span><span class="sxs-lookup"><span data-stu-id="de9d7-782">Returns a Boolean value indicating whether the specified GeoJSON Point, Polygon, or LineString expression is valid.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="de9d7-783">ST_ISVALIDDETAILED</span><span class="sxs-lookup"><span data-stu-id="de9d7-783">ST_ISVALIDDETAILED</span></span></td>
  <td><span data-ttu-id="de9d7-784">Renvoie une valeur JSON contenant une valeur booléenne si l’expression Point, Polygone ou LineString GeoJSON spécifiée est valide et, dans le cas contraire, le motif sous forme de valeur de chaîne.</span><span class="sxs-lookup"><span data-stu-id="de9d7-784">Returns a JSON value containing a Boolean value if the specified GeoJSON Point, Polygon, or LineString expression is valid, and if invalid, additionally the reason as a string value.</span></span></td>
</tr>
</table>

<span data-ttu-id="de9d7-785">Les fonctions spatiales peuvent être utilisées pour effectuer des requêtes de proximité par rapport aux données spatiales.</span><span class="sxs-lookup"><span data-stu-id="de9d7-785">Spatial functions can be used to perform proximity queries against spatial data.</span></span> <span data-ttu-id="de9d7-786">Par exemple, voici une requête qui retourne tous les documents de famille se trouvant dans un rayon de 30 kilomètres de l'emplacement spécifié à l'aide de la fonction intégrée ST_DISTANCE.</span><span class="sxs-lookup"><span data-stu-id="de9d7-786">For example, here's a query that returns all family documents that are within 30 km of the specified location using the ST_DISTANCE built-in function.</span></span> 

<span data-ttu-id="de9d7-787">**Requête**</span><span class="sxs-lookup"><span data-stu-id="de9d7-787">**Query**</span></span>

    SELECT f.id 
    FROM Families f 
    WHERE ST_DISTANCE(f.location, {'type': 'Point', 'coordinates':[31.9, -4.8]}) < 30000

<span data-ttu-id="de9d7-788">**Résultats**</span><span class="sxs-lookup"><span data-stu-id="de9d7-788">**Results**</span></span>

    [{
      "id": "WakefieldFamily"
    }]

<span data-ttu-id="de9d7-789">Pour plus d’informations sur la prise en charge géospatiale dans Cosmos DB, consultez [Working with geospatial data in Azure Cosmos DB (Utilisation de données géospatiales dans Azure Cosmos DB)](geospatial.md).</span><span class="sxs-lookup"><span data-stu-id="de9d7-789">For more details on geospatial support in Cosmos DB, please see [Working with geospatial data in Azure Cosmos DB](geospatial.md).</span></span> <span data-ttu-id="de9d7-790">Cela inclut les fonctions spatiales et la syntaxe SQL pour Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="de9d7-790">That wraps up spatial functions, and the SQL syntax for Cosmos DB.</span></span> <span data-ttu-id="de9d7-791">Maintenant, examinons le fonctionnement de l’interrogation LINQ et voyons comment elle interagit avec la syntaxe que nous avons vue jusqu’à présent.</span><span class="sxs-lookup"><span data-stu-id="de9d7-791">Now let's take a look at how LINQ querying works and how it interacts with the syntax we've seen so far.</span></span>

## <span data-ttu-id="de9d7-792"><a id="Linq"></a>LINQ vers le langage SQL de l’API DocumentDB</span><span class="sxs-lookup"><span data-stu-id="de9d7-792"><a id="Linq"></a>LINQ to DocumentDB API SQL</span></span>
<span data-ttu-id="de9d7-793">LINQ est un modèle de programmation .NET qui exprime un calcul en tant que requête sur des flux d'objets.</span><span class="sxs-lookup"><span data-stu-id="de9d7-793">LINQ is a .NET programming model that expresses computation as queries on streams of objects.</span></span> <span data-ttu-id="de9d7-794">Cosmos DB fournit une bibliothèque côté client pour interagir avec LINQ en facilitant la conversion entre les objets JSON et .NET, ainsi qu’un mappage à partir d’un sous-ensemble de requêtes LINQ vers des requêtes Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="de9d7-794">Cosmos DB provides a client-side library to interface with LINQ by facilitating a conversion between JSON and .NET objects and a mapping from a subset of LINQ queries to Cosmos DB queries.</span></span> 

<span data-ttu-id="de9d7-795">L’image suivante illustre l’architecture de prise en charge des requêtes LINQ à l’aide de Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="de9d7-795">The picture below shows the architecture of supporting LINQ queries using Cosmos DB.</span></span>  <span data-ttu-id="de9d7-796">En utilisant le client Cosmos DB, les développeurs peuvent créer un objet **IQueryable** dirigeant les requêtes vers le fournisseur de requête de Cosmos DB, qui traduit alors les requêtes LINQ en requêtes Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="de9d7-796">Using the Cosmos DB client, developers can create an **IQueryable** object that directly queries the Cosmos DB query provider, which then translates the LINQ query into a Cosmos DB query.</span></span> <span data-ttu-id="de9d7-797">Ces requêtes sont ensuite transmises au serveur Cosmos DB pour récupérer un ensemble de résultats au format JSON.</span><span class="sxs-lookup"><span data-stu-id="de9d7-797">The query is then passed to the Cosmos DB server to retrieve a set of results in JSON format.</span></span> <span data-ttu-id="de9d7-798">Les résultats renvoyés sont désérialisés en un flux d'objets .NET, côté client.</span><span class="sxs-lookup"><span data-stu-id="de9d7-798">The returned results are deserialized into a stream of .NET objects on the client side.</span></span>

![Architecture de prise en charge des requêtes LINQ avec l’API DocumentDB (syntaxe SQL, langage de requête JSON, concepts de bases de données et requêtes SQL)][1]

### <a name="net-and-json-mapping"></a><span data-ttu-id="de9d7-800">Mappage .NET et JSON</span><span class="sxs-lookup"><span data-stu-id="de9d7-800">.NET and JSON mapping</span></span>
<span data-ttu-id="de9d7-801">Le mappage entre les objets .NET et les documents JSON est naturel : chaque champ de membre de données est mappé vers un objet JSON, où le nom du champ est mappé vers la partie « clé » de l'objet tandis que la partie « valeur » est mappée de façon récursive vers la partie de valeur de l'objet.</span><span class="sxs-lookup"><span data-stu-id="de9d7-801">The mapping between .NET objects and JSON documents is natural - each data member field is mapped to a JSON object, where the field name is mapped to the "key" part of the object and the "value" part is recursively mapped to the value part of the object.</span></span> <span data-ttu-id="de9d7-802">Prenons pour exemple : L’objet Family créé est mappé vers le document JSON, comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="de9d7-802">Consider the following example: The Family object created is mapped to the JSON document as shown below.</span></span> <span data-ttu-id="de9d7-803">À l'inverse, le document JSON est mappé vers un objet .NET.</span><span class="sxs-lookup"><span data-stu-id="de9d7-803">And vice versa, the JSON document is mapped back to a .NET object.</span></span>

<span data-ttu-id="de9d7-804">**Classe C#**</span><span class="sxs-lookup"><span data-stu-id="de9d7-804">**C# Class**</span></span>

    public class Family
    {
        [JsonProperty(PropertyName="id")]
        public string Id;
        public Parent[] parents;
        public Child[] children;
        public bool isRegistered;
    };

    public struct Parent
    {
        public string familyName;
        public string givenName;
    };

    public class Child
    {
        public string familyName;
        public string givenName;
        public string gender;
        public int grade;
        public List<Pet> pets;
    };

    public class Pet
    {
        public string givenName;
    };

    public class Address
    {
        public string state;
        public string county;
        public string city;
    };

    // Create a Family object.
    Parent mother = new Parent { familyName= "Wakefield", givenName="Robin" };
    Parent father = new Parent { familyName = "Miller", givenName = "Ben" };
    Child child = new Child { familyName="Merriam", givenName="Jesse", gender="female", grade=1 };
    Pet pet = new Pet { givenName = "Fluffy" };
    Address address = new Address { state = "NY", county = "Manhattan", city = "NY" };
    Family family = new Family { Id = "WakefieldFamily", parents = new Parent [] { mother, father}, children = new Child[] { child }, isRegistered = false };


<span data-ttu-id="de9d7-805">**JSON**</span><span class="sxs-lookup"><span data-stu-id="de9d7-805">**JSON**</span></span>  

    {
        "id": "WakefieldFamily",
        "parents": [
            { "familyName": "Wakefield", "givenName": "Robin" },
            { "familyName": "Miller", "givenName": "Ben" }
        ],
        "children": [
            {
                "familyName": "Merriam", 
                "givenName": "Jesse", 
                "gender": "female", 
                "grade": 1,
                "pets": [
                    { "givenName": "Goofy" },
                    { "givenName": "Shadow" }
                ]
            },
            { 
              "familyName": "Miller", 
              "givenName": "Lisa", 
              "gender": "female", 
              "grade": 8 
            }
        ],
        "address": { "state": "NY", "county": "Manhattan", "city": "NY" },
        "isRegistered": false
    };



### <a name="linq-to-sql-translation"></a><span data-ttu-id="de9d7-806">Conversion LINQ en SQL</span><span class="sxs-lookup"><span data-stu-id="de9d7-806">LINQ to SQL translation</span></span>
<span data-ttu-id="de9d7-807">Le fournisseur de requêtes de Cosmos DB effectue le meilleur mappage possible entre une requête LINQ et une requête SQL Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="de9d7-807">The Cosmos DB query provider performs a best effort mapping from a LINQ query into a Cosmos DB SQL query.</span></span> <span data-ttu-id="de9d7-808">Dans la description suivante, nous partons du principe que le lecteur connaît les principes de base de LINQ.</span><span class="sxs-lookup"><span data-stu-id="de9d7-808">In the following description, we assume the reader has a basic familiarity of LINQ.</span></span>

<span data-ttu-id="de9d7-809">D'abord, pour le système de type, nous prenons en charge tous les types JSON primitifs : numérique, booléen, chaîne et Null.</span><span class="sxs-lookup"><span data-stu-id="de9d7-809">First, for the type system, we support all JSON primitive types – numeric types, boolean, string, and null.</span></span> <span data-ttu-id="de9d7-810">Seuls ces types JSON sont pris en charge.</span><span class="sxs-lookup"><span data-stu-id="de9d7-810">Only these JSON types are supported.</span></span> <span data-ttu-id="de9d7-811">Les expressions scalaires suivantes sont prises en charge.</span><span class="sxs-lookup"><span data-stu-id="de9d7-811">The following scalar expressions are supported.</span></span>

* <span data-ttu-id="de9d7-812">Valeurs constantes : elles incluent des valeurs constantes des types de données primitifs au moment de l’évaluation de la requête.</span><span class="sxs-lookup"><span data-stu-id="de9d7-812">Constant values – these include constant values of the primitive data types at the time the query is evaluated.</span></span>
* <span data-ttu-id="de9d7-813">Expressions d'index de propriété/tableau : ces expressions font référence à la propriété d'un objet ou d'un élément de tableau.</span><span class="sxs-lookup"><span data-stu-id="de9d7-813">Property/array index expressions – these expressions refer to the property of an object or an array element.</span></span>
  
     <span data-ttu-id="de9d7-814">family.Id;    family.children[0].familyName;    family.children[0].grade;    family.children[n].grade; //n étant un entier</span><span class="sxs-lookup"><span data-stu-id="de9d7-814">family.Id;    family.children[0].familyName;    family.children[0].grade;    family.children[n].grade; //n is an int variable</span></span>
* <span data-ttu-id="de9d7-815">Expressions arithmétiques : elles incluent les expressions arithmétiques communes sur les valeurs numériques et booléennes.</span><span class="sxs-lookup"><span data-stu-id="de9d7-815">Arithmetic expressions - These include common arithmetic expressions on numerical and boolean values.</span></span> <span data-ttu-id="de9d7-816">Pour obtenir une liste complète, reportez-vous à la spécification SQL.</span><span class="sxs-lookup"><span data-stu-id="de9d7-816">For the complete list, refer to the SQL specification.</span></span>
  
     <span data-ttu-id="de9d7-817">2 * family.children[0].grade;    x + y;</span><span class="sxs-lookup"><span data-stu-id="de9d7-817">2 * family.children[0].grade;    x + y;</span></span>
* <span data-ttu-id="de9d7-818">Expressions de comparaison de chaîne : elles incluent les comparaisons de valeurs de chaînes à certaines valeurs de chaînes constantes.</span><span class="sxs-lookup"><span data-stu-id="de9d7-818">String comparison expression - these include comparing a string value to some constant string value.</span></span>  
  
     <span data-ttu-id="de9d7-819">mother.familyName == "Smith";    child.givenName == s; //s étant une chaîne</span><span class="sxs-lookup"><span data-stu-id="de9d7-819">mother.familyName == "Smith";    child.givenName == s; //s is a string variable</span></span>
* <span data-ttu-id="de9d7-820">Expressions de création d'objet/tableau : ces expressions renvoient un objet de type de valeur composée ou de type anonyme ou un tableau de tels objets.</span><span class="sxs-lookup"><span data-stu-id="de9d7-820">Object/array creation expression - these expressions return an object of compound value type or anonymous type or an array of such objects.</span></span> <span data-ttu-id="de9d7-821">Ces valeurs peuvent être imbriquées.</span><span class="sxs-lookup"><span data-stu-id="de9d7-821">These values can be nested.</span></span>
  
     <span data-ttu-id="de9d7-822">new Parent { familyName = "Smith", givenName = "Joe" }; new { first = 1, second = 2 }; //type anonyme avec deux champs</span><span class="sxs-lookup"><span data-stu-id="de9d7-822">new Parent { familyName = "Smith", givenName = "Joe" }; new { first = 1, second = 2 }; //an anonymous type with two fields</span></span>              
     <span data-ttu-id="de9d7-823">new int[] { 3, child.grade, 5 };</span><span class="sxs-lookup"><span data-stu-id="de9d7-823">new int[] { 3, child.grade, 5 };</span></span>

### <span data-ttu-id="de9d7-824"><a id="SupportedLinqOperators"></a>Liste des opérateurs LINQ pris en charge</span><span class="sxs-lookup"><span data-stu-id="de9d7-824"><a id="SupportedLinqOperators"></a>List of supported LINQ operators</span></span>
<span data-ttu-id="de9d7-825">Voici une liste des opérateurs LINQ pris en charge dans le fournisseur LINQ inclus avec le kit SDK .NET DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="de9d7-825">Here is a list of supported LINQ operators in the LINQ provider included with the DocumentDB .NET SDK.</span></span>

* <span data-ttu-id="de9d7-826">**Select**: les projections sont traduites en SQL SELECT, y compris la construction d'objets</span><span class="sxs-lookup"><span data-stu-id="de9d7-826">**Select**: Projections translate to the SQL SELECT including object construction</span></span>
* <span data-ttu-id="de9d7-827">**Where** : les filtres sont traduits en SQL WHERE et prennent en charge la traduction entre && , || et !</span><span class="sxs-lookup"><span data-stu-id="de9d7-827">**Where**: Filters translate to the SQL WHERE, and support translation between && , || and !</span></span> <span data-ttu-id="de9d7-828">vers les opérateurs SQL</span><span class="sxs-lookup"><span data-stu-id="de9d7-828">to the SQL operators</span></span>
* <span data-ttu-id="de9d7-829">**SelectMany**: autorise le déroulement de tableaux vers la clause SQL JOIN.</span><span class="sxs-lookup"><span data-stu-id="de9d7-829">**SelectMany**: Allows unwinding of arrays to the SQL JOIN clause.</span></span> <span data-ttu-id="de9d7-830">Peut être utilisé pour associer/imbriquer des expressions afin de filtrer les éléments de tableau</span><span class="sxs-lookup"><span data-stu-id="de9d7-830">Can be used to chain/nest expressions to filter on array elements</span></span>
* <span data-ttu-id="de9d7-831">**OrderBy et OrderByDescending** : se traduit par ORDER BY dans l’ordre croissant/décroissant</span><span class="sxs-lookup"><span data-stu-id="de9d7-831">**OrderBy and OrderByDescending**: Translates to ORDER BY ascending/descending</span></span>
* <span data-ttu-id="de9d7-832">Les opérateurs **Count**, **Sum**, **Min**, **Max** et **Average** pour l’agrégation, et leurs équivalents asynchrones **CountAsync**, **SumAsync**, **MinAsync**, **MaxAsync** et **AverageAsync**.</span><span class="sxs-lookup"><span data-stu-id="de9d7-832">**Count**, **Sum**, **Min**, **Max**, and **Average** operators for aggregation, and their async equivalents **CountAsync**, **SumAsync**, **MinAsync**, **MaxAsync**, and **AverageAsync**.</span></span>
* <span data-ttu-id="de9d7-833">**CompareTo**: se traduit par des comparaisons de plages.</span><span class="sxs-lookup"><span data-stu-id="de9d7-833">**CompareTo**: Translates to range comparisons.</span></span> <span data-ttu-id="de9d7-834">Généralement utilisés pour les chaînes car ils ne sont pas comparables dans .NET</span><span class="sxs-lookup"><span data-stu-id="de9d7-834">Commonly used for strings since they’re not comparable in .NET</span></span>
* <span data-ttu-id="de9d7-835">**Take**: se traduit par SQL TOP pour limiter les résultats provenant d'une requête</span><span class="sxs-lookup"><span data-stu-id="de9d7-835">**Take**: Translates to the SQL TOP for limiting results from a query</span></span>
* <span data-ttu-id="de9d7-836">**Math Functions**: prend en charge la traduction de .NET’s Abs, Acos, Asin, Atan, Ceiling, Cos, Exp, Floor, Log, Log10, Pow, Round, Sign, Sin, Sqrt, Tan et Truncate vers les fonctions SQL intégrées équivalentes.</span><span class="sxs-lookup"><span data-stu-id="de9d7-836">**Math Functions**: Supports translation from .NET’s Abs, Acos, Asin, Atan, Ceiling, Cos, Exp, Floor, Log, Log10, Pow, Round, Sign, Sin, Sqrt, Tan, Truncate to the equivalent SQL built-in functions.</span></span>
* <span data-ttu-id="de9d7-837">**String Functions**: prend en charge la traduction de .NET’s Concat, Contains, EndsWith, IndexOf, Count, ToLower, TrimStart, Replace, Reverse, TrimEnd, StartsWith, SubString et ToUpper vers les fonctions SQL intégrées équivalentes.</span><span class="sxs-lookup"><span data-stu-id="de9d7-837">**String Functions**: Supports translation from .NET’s Concat, Contains, EndsWith, IndexOf, Count, ToLower, TrimStart, Replace, Reverse, TrimEnd, StartsWith, SubString, ToUpper to the equivalent SQL built-in functions.</span></span>
* <span data-ttu-id="de9d7-838">**Array Functions**: prend en charge la traduction à partir de .NET’s Concat, Contains et Count pour les fonctions SQL intégrées équivalentes.</span><span class="sxs-lookup"><span data-stu-id="de9d7-838">**Array Functions**: Supports translation from .NET’s Concat, Contains, and Count to the equivalent SQL built-in functions.</span></span>
* <span data-ttu-id="de9d7-839">**Geospatial Extension Functions**: prend en charge la traduction des méthodes stub Distance, Within, IsValid et IsValidDetailed vers les fonctions SQL intégrées équivalentes.</span><span class="sxs-lookup"><span data-stu-id="de9d7-839">**Geospatial Extension Functions**: Supports translation from stub methods Distance, Within, IsValid, and IsValidDetailed to the equivalent SQL built-in functions.</span></span>
* <span data-ttu-id="de9d7-840">**User Defined Function Extension Function** : prend en charge la traduction de la méthode stub UserDefinedFunctionProvider.Invoke vers la fonction définie par l’utilisateur correspondante.</span><span class="sxs-lookup"><span data-stu-id="de9d7-840">**User-Defined Function Extension Function**: Supports translation from the stub method UserDefinedFunctionProvider.Invoke to the corresponding user-defined function.</span></span>
* <span data-ttu-id="de9d7-841">**Miscellaneous**: prend en charge la traduction des opérateurs conditionnels et coalesce.</span><span class="sxs-lookup"><span data-stu-id="de9d7-841">**Miscellaneous**: Supports translation of the coalesce and conditional operators.</span></span> <span data-ttu-id="de9d7-842">Peut traduire Contains en chaîne CONTAINS, ARRAY_CONTAINS ou SQL IN, selon le contexte.</span><span class="sxs-lookup"><span data-stu-id="de9d7-842">Can translate Contains to String CONTAINS, ARRAY_CONTAINS, or the SQL IN depending on context.</span></span>

### <a name="sql-query-operators"></a><span data-ttu-id="de9d7-843">Opérateurs de requête SQL</span><span class="sxs-lookup"><span data-stu-id="de9d7-843">SQL query operators</span></span>
<span data-ttu-id="de9d7-844">Voici quelques exemples illustrant comment certains opérateurs de requête LINQ standard sont traduits en requêtes Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="de9d7-844">Here are some examples that illustrate how some of the standard LINQ query operators are translated down to Cosmos DB queries.</span></span>

#### <a name="select-operator"></a><span data-ttu-id="de9d7-845">Opérateur Select</span><span class="sxs-lookup"><span data-stu-id="de9d7-845">Select Operator</span></span>
<span data-ttu-id="de9d7-846">La syntaxe est `input.Select(x => f(x))`, où `f` est une expression scalaire.</span><span class="sxs-lookup"><span data-stu-id="de9d7-846">The syntax is `input.Select(x => f(x))`, where `f` is a scalar expression.</span></span>

<span data-ttu-id="de9d7-847">**Expression Lambda LINQ**</span><span class="sxs-lookup"><span data-stu-id="de9d7-847">**LINQ lambda expression**</span></span>

    input.Select(family => family.parents[0].familyName);

<span data-ttu-id="de9d7-848">**SQL**</span><span class="sxs-lookup"><span data-stu-id="de9d7-848">**SQL**</span></span> 

    SELECT VALUE f.parents[0].familyName
    FROM Families f



<span data-ttu-id="de9d7-849">**Expression Lambda LINQ**</span><span class="sxs-lookup"><span data-stu-id="de9d7-849">**LINQ lambda expression**</span></span>

    input.Select(family => family.children[0].grade + c); // c is an int variable


<span data-ttu-id="de9d7-850">**SQL**</span><span class="sxs-lookup"><span data-stu-id="de9d7-850">**SQL**</span></span> 

    SELECT VALUE f.children[0].grade + c
    FROM Families f 



<span data-ttu-id="de9d7-851">**Expression Lambda LINQ**</span><span class="sxs-lookup"><span data-stu-id="de9d7-851">**LINQ lambda expression**</span></span>

    input.Select(family => new
    {
        name = family.children[0].familyName,
        grade = family.children[0].grade + 3
    });


<span data-ttu-id="de9d7-852">**SQL**</span><span class="sxs-lookup"><span data-stu-id="de9d7-852">**SQL**</span></span> 

    SELECT VALUE {"name":f.children[0].familyName, 
                  "grade": f.children[0].grade + 3 }
    FROM Families f



#### <a name="selectmany-operator"></a><span data-ttu-id="de9d7-853">Opérateur SelectMany</span><span class="sxs-lookup"><span data-stu-id="de9d7-853">SelectMany operator</span></span>
<span data-ttu-id="de9d7-854">La syntaxe est `input.SelectMany(x => f(x))`, où `f` est une expression scalaire qui retourne un type de collection.</span><span class="sxs-lookup"><span data-stu-id="de9d7-854">The syntax is `input.SelectMany(x => f(x))`, where `f` is a scalar expression that returns a collection type.</span></span>

<span data-ttu-id="de9d7-855">**Expression Lambda LINQ**</span><span class="sxs-lookup"><span data-stu-id="de9d7-855">**LINQ lambda expression**</span></span>

    input.SelectMany(family => family.children);

<span data-ttu-id="de9d7-856">**SQL**</span><span class="sxs-lookup"><span data-stu-id="de9d7-856">**SQL**</span></span> 

    SELECT VALUE child
    FROM child IN Families.children



#### <a name="where-operator"></a><span data-ttu-id="de9d7-857">Opérateur Where</span><span class="sxs-lookup"><span data-stu-id="de9d7-857">Where operator</span></span>
<span data-ttu-id="de9d7-858">La syntaxe est `input.Where(x => f(x))`, où `f` est une expression scalaire qui retourne une valeur booléenne.</span><span class="sxs-lookup"><span data-stu-id="de9d7-858">The syntax is `input.Where(x => f(x))`, where `f` is a scalar expression, which returns a Boolean value.</span></span>

<span data-ttu-id="de9d7-859">**Expression Lambda LINQ**</span><span class="sxs-lookup"><span data-stu-id="de9d7-859">**LINQ lambda expression**</span></span>

    input.Where(family=> family.parents[0].familyName == "Smith");

<span data-ttu-id="de9d7-860">**SQL**</span><span class="sxs-lookup"><span data-stu-id="de9d7-860">**SQL**</span></span> 

    SELECT *
    FROM Families f
    WHERE f.parents[0].familyName = "Smith" 



<span data-ttu-id="de9d7-861">**Expression Lambda LINQ**</span><span class="sxs-lookup"><span data-stu-id="de9d7-861">**LINQ lambda expression**</span></span>

    input.Where(
        family => family.parents[0].familyName == "Smith" && 
        family.children[0].grade < 3);

<span data-ttu-id="de9d7-862">**SQL**</span><span class="sxs-lookup"><span data-stu-id="de9d7-862">**SQL**</span></span> 

    SELECT *
    FROM Families f
    WHERE f.parents[0].familyName = "Smith"
    AND f.children[0].grade < 3


### <a name="composite-sql-queries"></a><span data-ttu-id="de9d7-863">Requêtes SQL composites</span><span class="sxs-lookup"><span data-stu-id="de9d7-863">Composite SQL queries</span></span>
<span data-ttu-id="de9d7-864">Les opérateurs suivants peuvent être composés pour former des requêtes plus puissantes.</span><span class="sxs-lookup"><span data-stu-id="de9d7-864">The above operators can be composed to form more powerful queries.</span></span> <span data-ttu-id="de9d7-865">Étant donné que Cosmos DB prend en charge les collections imbriquées, la composition peut être concaténée ou imbriquée.</span><span class="sxs-lookup"><span data-stu-id="de9d7-865">Since Cosmos DB supports nested collections, the composition can either be concatenated or nested.</span></span>

#### <a name="concatenation"></a><span data-ttu-id="de9d7-866">Concaténation</span><span class="sxs-lookup"><span data-stu-id="de9d7-866">Concatenation</span></span>
<span data-ttu-id="de9d7-867">La syntaxe est `input(.|.SelectMany())(.Select()|.Where())*`.</span><span class="sxs-lookup"><span data-stu-id="de9d7-867">The syntax is `input(.|.SelectMany())(.Select()|.Where())*`.</span></span> <span data-ttu-id="de9d7-868">Une requête concaténée peut commencer par une requête `SelectMany` facultative suivie de plusieurs opérateurs `Select` ou `Where`.</span><span class="sxs-lookup"><span data-stu-id="de9d7-868">A concatenated query can start with an optional `SelectMany` query followed by multiple `Select` or `Where` operators.</span></span>

<span data-ttu-id="de9d7-869">**Expression Lambda LINQ**</span><span class="sxs-lookup"><span data-stu-id="de9d7-869">**LINQ lambda expression**</span></span>

    input.Select(family=>family.parents[0])
        .Where(familyName == "Smith");

<span data-ttu-id="de9d7-870">**SQL**</span><span class="sxs-lookup"><span data-stu-id="de9d7-870">**SQL**</span></span>

    SELECT *
    FROM Families f
    WHERE f.parents[0].familyName = "Smith"



<span data-ttu-id="de9d7-871">**Expression Lambda LINQ**</span><span class="sxs-lookup"><span data-stu-id="de9d7-871">**LINQ lambda expression**</span></span>

    input.Where(family => family.children[0].grade > 3)
        .Select(family => family.parents[0].familyName);

<span data-ttu-id="de9d7-872">**SQL**</span><span class="sxs-lookup"><span data-stu-id="de9d7-872">**SQL**</span></span> 

    SELECT VALUE f.parents[0].familyName
    FROM Families f
    WHERE f.children[0].grade > 3



<span data-ttu-id="de9d7-873">**Expression Lambda LINQ**</span><span class="sxs-lookup"><span data-stu-id="de9d7-873">**LINQ lambda expression**</span></span>

    input.Select(family => new { grade=family.children[0].grade}).
        Where(anon=> anon.grade < 3);

<span data-ttu-id="de9d7-874">**SQL**</span><span class="sxs-lookup"><span data-stu-id="de9d7-874">**SQL**</span></span> 

    SELECT *
    FROM Families f
    WHERE ({grade: f.children[0].grade}.grade > 3)



<span data-ttu-id="de9d7-875">**Expression Lambda LINQ**</span><span class="sxs-lookup"><span data-stu-id="de9d7-875">**LINQ lambda expression**</span></span>

    input.SelectMany(family => family.parents)
        .Where(parent => parents.familyName == "Smith");

<span data-ttu-id="de9d7-876">**SQL**</span><span class="sxs-lookup"><span data-stu-id="de9d7-876">**SQL**</span></span> 

    SELECT *
    FROM p IN Families.parents
    WHERE p.familyName = "Smith"



#### <a name="nesting"></a><span data-ttu-id="de9d7-877">Imbrication</span><span class="sxs-lookup"><span data-stu-id="de9d7-877">Nesting</span></span>
<span data-ttu-id="de9d7-878">La syntaxe est `input.SelectMany(x=>x.Q())`, où Q est un opérateur `Select`, `SelectMany` ou `Where`.</span><span class="sxs-lookup"><span data-stu-id="de9d7-878">The syntax is `input.SelectMany(x=>x.Q())` where Q is a `Select`, `SelectMany`, or `Where` operator.</span></span>

<span data-ttu-id="de9d7-879">Dans une requête imbriquée, la requête interne est appliquée à chaque élément de la collection externe.</span><span class="sxs-lookup"><span data-stu-id="de9d7-879">In a nested query, the inner query is applied to each element of the outer collection.</span></span> <span data-ttu-id="de9d7-880">La requête interne peut faire référence aux champs des éléments dans la collection externe, comme des jointures réflexives : cette fonctionnalité est importante.</span><span class="sxs-lookup"><span data-stu-id="de9d7-880">One important feature is that the inner query can refer to the fields of the elements in the outer collection like self-joins.</span></span>

<span data-ttu-id="de9d7-881">**Expression Lambda LINQ**</span><span class="sxs-lookup"><span data-stu-id="de9d7-881">**LINQ lambda expression**</span></span>

    input.SelectMany(family=> 
        family.parents.Select(p => p.familyName));

<span data-ttu-id="de9d7-882">**SQL**</span><span class="sxs-lookup"><span data-stu-id="de9d7-882">**SQL**</span></span> 

    SELECT VALUE p.familyName
    FROM Families f
    JOIN p IN f.parents


<span data-ttu-id="de9d7-883">**Expression Lambda LINQ**</span><span class="sxs-lookup"><span data-stu-id="de9d7-883">**LINQ lambda expression**</span></span>

    input.SelectMany(family => 
        family.children.Where(child => child.familyName == "Jeff"));

<span data-ttu-id="de9d7-884">**SQL**</span><span class="sxs-lookup"><span data-stu-id="de9d7-884">**SQL**</span></span> 

    SELECT *
    FROM Families f
    JOIN c IN f.children
    WHERE c.familyName = "Jeff"



<span data-ttu-id="de9d7-885">**Expression Lambda LINQ**</span><span class="sxs-lookup"><span data-stu-id="de9d7-885">**LINQ lambda expression**</span></span>

    input.SelectMany(family => family.children.Where(
        child => child.familyName == family.parents[0].familyName));

<span data-ttu-id="de9d7-886">**SQL**</span><span class="sxs-lookup"><span data-stu-id="de9d7-886">**SQL**</span></span> 

    SELECT *
    FROM Families f
    JOIN c IN f.children
    WHERE c.familyName = f.parents[0].familyName


## <span data-ttu-id="de9d7-887"><a id="ExecutingSqlQueries"></a>Exécution de requêtes SQL</span><span class="sxs-lookup"><span data-stu-id="de9d7-887"><a id="ExecutingSqlQueries"></a>Executing SQL queries</span></span>
<span data-ttu-id="de9d7-888">Cosmos DB expose les ressources par le biais d’une API REST qui peut être appelée par n’importe quel langage capable de créer des requêtes HTTP/HTTPS.</span><span class="sxs-lookup"><span data-stu-id="de9d7-888">Cosmos DB exposes resources through a REST API that can be called by any language capable of making HTTP/HTTPS requests.</span></span> <span data-ttu-id="de9d7-889">Par ailleurs, Cosmos DB propose des bibliothèques de programmation pour plusieurs langages populaires comme .NET, Node.js, JavaScript et Python.</span><span class="sxs-lookup"><span data-stu-id="de9d7-889">Additionally, Cosmos DB offers programming libraries for several popular languages like .NET, Node.js, JavaScript, and Python.</span></span> <span data-ttu-id="de9d7-890">L'API REST et les différentes bibliothèques prennent toutes en charge l'interrogation via SQL.</span><span class="sxs-lookup"><span data-stu-id="de9d7-890">The REST API and the various libraries all support querying through SQL.</span></span> <span data-ttu-id="de9d7-891">Le kit SDK .NET prend en charge l'interrogation LINQ en plus du SQL.</span><span class="sxs-lookup"><span data-stu-id="de9d7-891">The .NET SDK supports LINQ querying in addition to SQL.</span></span>

<span data-ttu-id="de9d7-892">Les exemples suivants montrent comment créer une requête et la soumettre à un compte de base de données Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="de9d7-892">The following examples show how to create a query and submit it against a Cosmos DB database account.</span></span>

### <span data-ttu-id="de9d7-893"><a id="RestAPI"></a>API REST</span><span class="sxs-lookup"><span data-stu-id="de9d7-893"><a id="RestAPI"></a>REST API</span></span>
<span data-ttu-id="de9d7-894">Cosmos DB fournit un modèle de programmation RESTful ouvert sur HTTP.</span><span class="sxs-lookup"><span data-stu-id="de9d7-894">Cosmos DB offers an open RESTful programming model over HTTP.</span></span> <span data-ttu-id="de9d7-895">Vous pouvez approvisionner vos comptes de bases de données en utilisant un abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="de9d7-895">Database accounts can be provisioned using an Azure subscription.</span></span> <span data-ttu-id="de9d7-896">Le modèle de ressource de Cosmos DB se compose d’un ensemble de ressources sous un compte de base de données, toutes adressables par le biais d’un URI stable et logique.</span><span class="sxs-lookup"><span data-stu-id="de9d7-896">The Cosmos DB resource model consists of a set of resources under a database account, each  of which is addressable using a logical and stable URI.</span></span> <span data-ttu-id="de9d7-897">Dans ce document, de tels ensembles de ressources sont désignés sous le nom de « flux ».</span><span class="sxs-lookup"><span data-stu-id="de9d7-897">A set of resources is referred to as a feed in this document.</span></span> <span data-ttu-id="de9d7-898">Un compte de base de données se compose d'un ensemble de bases de données. Chacune d'elles contient plusieurs collections et chaque collection contient des documents, des fonctions définies par l'utilisateur et d'autres types de ressources.</span><span class="sxs-lookup"><span data-stu-id="de9d7-898">A database account consists of a set of databases, each containing multiple collections, each of which in-turn contain documents, UDFs, and other resource types.</span></span>

<span data-ttu-id="de9d7-899">Le modèle d’interaction de base avec ces ressources consiste à utiliser des verbes HTTP, tels que GET, PUT, POST et DELETE, avec leur interprétation standard.</span><span class="sxs-lookup"><span data-stu-id="de9d7-899">The basic interaction model with these resources is through the HTTP verbs GET, PUT, POST, and DELETE with their standard interpretation.</span></span> <span data-ttu-id="de9d7-900">Le verbe POST permet de créer une ressource, d’exécuter une procédure stockée ou d’émettre une requête Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="de9d7-900">The POST verb is used for creation of a new resource, for executing a stored procedure or for issuing a Cosmos DB query.</span></span> <span data-ttu-id="de9d7-901">Les requêtes sont toujours des opérations en lecture seule sans effets secondaires.</span><span class="sxs-lookup"><span data-stu-id="de9d7-901">Queries are always read-only operations with no side-effects.</span></span>

<span data-ttu-id="de9d7-902">Les exemples suivants illustrent l’utilisation d’une action POST pour une requête API DocumentDB appliquée sur une collection contenant les deux exemples de documents utilisés jusqu’à présent.</span><span class="sxs-lookup"><span data-stu-id="de9d7-902">The following examples show a POST for a DocumentDB API query made against a collection containing the two sample documents we've reviewed so far.</span></span> <span data-ttu-id="de9d7-903">La requête contient un simple filtre sur la propriété de nom JSON.</span><span class="sxs-lookup"><span data-stu-id="de9d7-903">The query has a simple filter on the JSON name property.</span></span> <span data-ttu-id="de9d7-904">Notez l’utilisation des en-têtes `x-ms-documentdb-isquery` et Content-Type: `application/query+json` pour indiquer que l’opération est une requête.</span><span class="sxs-lookup"><span data-stu-id="de9d7-904">Note the use of the `x-ms-documentdb-isquery` and Content-Type: `application/query+json` headers to denote that the operation is a query.</span></span>

<span data-ttu-id="de9d7-905">**Requête**</span><span class="sxs-lookup"><span data-stu-id="de9d7-905">**Request**</span></span>

    POST https://<REST URI>/docs HTTP/1.1
    ...
    x-ms-documentdb-isquery: True
    Content-Type: application/query+json

    {      
        "query": "SELECT * FROM Families f WHERE f.id = @familyId",     
        "parameters": [          
            {"name": "@familyId", "value": "AndersenFamily"}         
        ] 
    }


<span data-ttu-id="de9d7-906">**Résultats**</span><span class="sxs-lookup"><span data-stu-id="de9d7-906">**Results**</span></span>

    HTTP/1.1 200 Ok
    x-ms-activity-id: 8b4678fa-a947-47d3-8dd3-549a40da6eed
    x-ms-item-count: 1
    x-ms-request-charge: 0.32

    <indented for readability, results highlighted>

    {  
       "_rid":"u1NXANcKogE=",
       "Documents":[  
          {  
             "id":"AndersenFamily",
             "lastName":"Andersen",
             "parents":[  
                {  
                   "firstName":"Thomas"
                },
                {  
                   "firstName":"Mary Kay"
                }
             ],
             "children":[  
                {  
                   "firstName":"Henriette Thaulow",
                   "gender":"female",
                   "grade":5,
                   "pets":[  
                      {  
                         "givenName":"Fluffy"
                      }
                   ]
                }
             ],
             "address":{  
                "state":"WA",
                "county":"King",
                "city":"seattle"
             },
             "_rid":"u1NXANcKogEcAAAAAAAAAA==",
             "_ts":1407691744,
             "_self":"dbs\/u1NXAA==\/colls\/u1NXANcKogE=\/docs\/u1NXANcKogEcAAAAAAAAAA==\/",
             "_etag":"00002b00-0000-0000-0000-53e7abe00000",
             "_attachments":"_attachments\/"
          }
       ],
       "count":1
    }


<span data-ttu-id="de9d7-907">Le deuxième exemple illustre une requête plus complexe qui renvoie plusieurs résultats à partir de la jointure.</span><span class="sxs-lookup"><span data-stu-id="de9d7-907">The second example shows a more complex query that returns multiple results from the join.</span></span>

<span data-ttu-id="de9d7-908">**Requête**</span><span class="sxs-lookup"><span data-stu-id="de9d7-908">**Request**</span></span>

    POST https://<REST URI>/docs HTTP/1.1
    ...
    x-ms-documentdb-isquery: True
    Content-Type: application/query+json

    {      
        "query": "SELECT 
                     f.id AS familyName, 
                     c.givenName AS childGivenName, 
                     c.firstName AS childFirstName, 
                     p.givenName AS petName 
                  FROM Families f 
                  JOIN c IN f.children 
                  JOIN p in c.pets",     
        "parameters": [] 
    }


<span data-ttu-id="de9d7-909">**Résultats**</span><span class="sxs-lookup"><span data-stu-id="de9d7-909">**Results**</span></span>

    HTTP/1.1 200 Ok
    x-ms-activity-id: 568f34e3-5695-44d3-9b7d-62f8b83e509d
    x-ms-item-count: 1
    x-ms-request-charge: 7.84

    <indented for readability, results highlighted>

    {  
       "_rid":"u1NXANcKogE=",
       "Documents":[  
          {  
             "familyName":"AndersenFamily",
             "childFirstName":"Henriette Thaulow",
             "petName":"Fluffy"
          },
          {  
             "familyName":"WakefieldFamily",
             "childGivenName":"Jesse",
             "petName":"Goofy"
          },
          {  
             "familyName":"WakefieldFamily",
             "childGivenName":"Jesse",
             "petName":"Shadow"
          }
       ],
       "count":3
    }


<span data-ttu-id="de9d7-910">Si les résultats d’une requête ne tiennent pas sur une seule page, l’API REST retourne un jeton de liaison via l’en-tête de réponse `x-ms-continuation-token` .</span><span class="sxs-lookup"><span data-stu-id="de9d7-910">If a query's results cannot fit within a single page of results, then the REST API returns a continuation token through the `x-ms-continuation-token` response header.</span></span> <span data-ttu-id="de9d7-911">Les clients peuvent paginer les résultats en incluant l'en-tête dans les résultats suivants.</span><span class="sxs-lookup"><span data-stu-id="de9d7-911">Clients can paginate results by including the header in subsequent results.</span></span> <span data-ttu-id="de9d7-912">Vous pouvez aussi contrôler le nombre de résultats par page via l'en-tête de nombre `x-ms-max-item-count` .</span><span class="sxs-lookup"><span data-stu-id="de9d7-912">The number of results per page can also be controlled through the `x-ms-max-item-count` number header.</span></span> <span data-ttu-id="de9d7-913">Si la requête spécifiée inclut une fonction d’agrégation telle que `COUNT`, la page de requête peut renvoyer une valeur partiellement agrégée sur la page de résultats.</span><span class="sxs-lookup"><span data-stu-id="de9d7-913">If the specified query has an aggregation function like `COUNT`, then the query page may return a partially aggregated value over the page of results.</span></span> <span data-ttu-id="de9d7-914">Les clients doivent effectuer une agrégation de deuxième niveau sur ces résultats pour produire les résultats finaux, par exemple effectuer la somme des nombres renvoyés dans les pages individuelles pour renvoyer le nombre total.</span><span class="sxs-lookup"><span data-stu-id="de9d7-914">The clients must perform a second-level aggregation over these results to produce the final results, for example, sum over the counts returned in the individual pages to return the total count.</span></span>

<span data-ttu-id="de9d7-915">Pour gérer la stratégie de cohérence des données des requêtes, utilisez l’en-tête `x-ms-consistency-level` comme pour toutes les requêtes d’API REST.</span><span class="sxs-lookup"><span data-stu-id="de9d7-915">To manage the data consistency policy for queries, use the `x-ms-consistency-level` header like all REST API requests.</span></span> <span data-ttu-id="de9d7-916">Pour maintenir la cohérence par session, vous devez aussi appliquer l’écho sur le dernier en-tête de cookie `x-ms-session-token` dans la demande de requête.</span><span class="sxs-lookup"><span data-stu-id="de9d7-916">For session consistency, it is required to also echo the latest `x-ms-session-token` Cookie header in the query request.</span></span> <span data-ttu-id="de9d7-917">La stratégie d’indexation de la collection interrogée peut également influencer la cohérence des résultats de la requête.</span><span class="sxs-lookup"><span data-stu-id="de9d7-917">The queried collection's indexing policy can also influence the consistency of query results.</span></span> <span data-ttu-id="de9d7-918">Avec les paramètres de stratégie d’indexation par défaut, les collections de l’index sont toujours actualisées par rapport aux contenus du document, et les résultats de la requête correspondent à la cohérence choisie pour les données.</span><span class="sxs-lookup"><span data-stu-id="de9d7-918">With the default indexing policy settings, for collections the index is always current with the document contents and query results match the consistency chosen for data.</span></span> <span data-ttu-id="de9d7-919">Si la stratégie d'indexation est passée en différé, les requêtes peuvent renvoyer des résultats obsolètes.</span><span class="sxs-lookup"><span data-stu-id="de9d7-919">If the indexing policy is relaxed to Lazy, then queries can return stale results.</span></span> <span data-ttu-id="de9d7-920">Pour en savoir plus, voir [Niveaux de cohérence des données paramétrables dans Azure Cosmos DB][consistency-levels].</span><span class="sxs-lookup"><span data-stu-id="de9d7-920">For more information, see [Azure Cosmos DB Consistency Levels][consistency-levels].</span></span>

<span data-ttu-id="de9d7-921">Si la stratégie d’indexation configurée pour la collection ne peut pas prendre en charge la requête spécifiée, le serveur Azure Cosmos DB renvoie le code d’état 400 « Demande incorrecte ».</span><span class="sxs-lookup"><span data-stu-id="de9d7-921">If the configured indexing policy on the collection cannot support the specified query, the Azure Cosmos DB server returns 400 "Bad Request".</span></span> <span data-ttu-id="de9d7-922">Ce code est renvoyé pour les requêtes de plage par rapport aux chemins d'accès configurés pour les recherches (d'égalité) de hachage et pour les chemins d'accès explicitement exclus de l'indexation.</span><span class="sxs-lookup"><span data-stu-id="de9d7-922">This is returned for range queries against paths configured for hash (equality) lookups, and for paths explicitly excluded from indexing.</span></span> <span data-ttu-id="de9d7-923">L’en-tête `x-ms-documentdb-query-enable-scan` peut être spécifié pour permettre à la requête d’effectuer une analyse quand un index n’est pas disponible.</span><span class="sxs-lookup"><span data-stu-id="de9d7-923">The `x-ms-documentdb-query-enable-scan` header can be specified to allow the query to perform a scan when an index is not available.</span></span>

<span data-ttu-id="de9d7-924">Vous pouvez obtenir les métriques détaillées sur l’exécution des requêtes en définissant l’en-tête `x-ms-documentdb-populatequerymetrics` sur `True`.</span><span class="sxs-lookup"><span data-stu-id="de9d7-924">You can get detailed metrics on query execution by setting `x-ms-documentdb-populatequerymetrics` header to `True`.</span></span> <span data-ttu-id="de9d7-925">Pour en savoir plus, consultez la section relative aux [métriques de requête SQL pour l’API DocumentDB Azure Cosmos DB](documentdb-sql-query-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="de9d7-925">For more information, see [SQL query metrics for Azure Cosmos DB DocumentDB API](documentdb-sql-query-metrics.md).</span></span>

### <span data-ttu-id="de9d7-926"><a id="DotNetSdk"></a>Kit SDK C# (.NET)</span><span class="sxs-lookup"><span data-stu-id="de9d7-926"><a id="DotNetSdk"></a>C# (.NET) SDK</span></span>
<span data-ttu-id="de9d7-927">Le kit SDK .NET prend en charge l'interrogation LINQ et SQL.</span><span class="sxs-lookup"><span data-stu-id="de9d7-927">The .NET SDK supports both LINQ and SQL querying.</span></span> <span data-ttu-id="de9d7-928">L'exemple suivant illustre l'exécution d'une simple requête de filtre présentée précédemment dans ce document.</span><span class="sxs-lookup"><span data-stu-id="de9d7-928">The following example shows how to perform the simple filter query introduced earlier in this document.</span></span>

    foreach (var family in client.CreateDocumentQuery(collectionLink, 
        "SELECT * FROM Families f WHERE f.id = \"AndersenFamily\""))
    {
        Console.WriteLine("\tRead {0} from SQL", family);
    }

    SqlQuerySpec query = new SqlQuerySpec("SELECT * FROM Families f WHERE f.id = @familyId");
    query.Parameters = new SqlParameterCollection();
    query.Parameters.Add(new SqlParameter("@familyId", "AndersenFamily"));

    foreach (var family in client.CreateDocumentQuery(collectionLink, query))
    {
        Console.WriteLine("\tRead {0} from parameterized SQL", family);
    }

    foreach (var family in (
        from f in client.CreateDocumentQuery(collectionLink)
        where f.Id == "AndersenFamily"
        select f))
    {
        Console.WriteLine("\tRead {0} from LINQ query", family);
    }

    foreach (var family in client.CreateDocumentQuery(collectionLink)
        .Where(f => f.Id == "AndersenFamily")
        .Select(f => f))
    {
        Console.WriteLine("\tRead {0} from LINQ lambda", family);
    }


<span data-ttu-id="de9d7-929">Cet exemple compare l'égalité de deux propriétés dans chaque document et utilise des projections anonymes.</span><span class="sxs-lookup"><span data-stu-id="de9d7-929">This sample compares two properties for equality within each document and uses anonymous projections.</span></span> 

    foreach (var family in client.CreateDocumentQuery(collectionLink,
        @"SELECT {""Name"": f.id, ""City"":f.address.city} AS Family 
        FROM Families f 
        WHERE f.address.city = f.address.state"))
    {
        Console.WriteLine("\tRead {0} from SQL", family);
    }

    foreach (var family in (
        from f in client.CreateDocumentQuery<Family>(collectionLink)
        where f.address.city == f.address.state
        select new { Name = f.Id, City = f.address.city }))
    {
        Console.WriteLine("\tRead {0} from LINQ query", family);
    }

    foreach (var family in
        client.CreateDocumentQuery<Family>(collectionLink)
        .Where(f => f.address.city == f.address.state)
        .Select(f => new { Name = f.Id, City = f.address.city }))
    {
        Console.WriteLine("\tRead {0} from LINQ lambda", family);
    }


<span data-ttu-id="de9d7-930">Le prochain exemple illustre des jointures, exprimées via l'opérateur LINQ SelectMany.</span><span class="sxs-lookup"><span data-stu-id="de9d7-930">The next sample shows joins, expressed through LINQ SelectMany.</span></span>

    foreach (var pet in client.CreateDocumentQuery(collectionLink,
          @"SELECT p
            FROM Families f 
                 JOIN c IN f.children 
                 JOIN p in c.pets 
            WHERE p.givenName = ""Shadow"""))
    {
        Console.WriteLine("\tRead {0} from SQL", pet);
    }

    // Equivalent in Lambda expressions
    foreach (var pet in
        client.CreateDocumentQuery<Family>(collectionLink)
        .SelectMany(f => f.children)
        .SelectMany(c => c.pets)
        .Where(p => p.givenName == "Shadow"))
    {
        Console.WriteLine("\tRead {0} from LINQ lambda", pet);
    }



<span data-ttu-id="de9d7-931">Le client .NET effectue une itération automatique à travers l'ensemble des pages des résultats de la requête dans les blocs foreach, comme indiqué précédemment.</span><span class="sxs-lookup"><span data-stu-id="de9d7-931">The .NET client automatically iterates through all the pages of query results in the foreach blocks as shown above.</span></span> <span data-ttu-id="de9d7-932">Les options de requête présentées dans la section sur l’API REST sont également disponibles dans le kit SDK .NET à l’aide des classes `FeedOptions` et `FeedResponse` dans la méthode CreateDocumentQuery.</span><span class="sxs-lookup"><span data-stu-id="de9d7-932">The query options introduced in the REST API section are also available in the .NET SDK using the `FeedOptions` and `FeedResponse` classes in the CreateDocumentQuery method.</span></span> <span data-ttu-id="de9d7-933">Vous pouvez aussi contrôler le nombre de pages en utilisant le paramètre `MaxItemCount` .</span><span class="sxs-lookup"><span data-stu-id="de9d7-933">The number of pages can be controlled using the `MaxItemCount` setting.</span></span> 

<span data-ttu-id="de9d7-934">Vous pouvez également contrôler explicitement la pagination en créant `IDocumentQueryable` à l’aide de l’objet `IQueryable`, puis en lisant les valeurs ` ResponseContinuationToken` et en les retransférant en tant que `RequestContinuationToken` dans `FeedOptions`.</span><span class="sxs-lookup"><span data-stu-id="de9d7-934">You can also explicitly control paging by creating `IDocumentQueryable` using the `IQueryable` object, then by reading the` ResponseContinuationToken` values and passing them back as `RequestContinuationToken` in `FeedOptions`.</span></span> <span data-ttu-id="de9d7-935">`EnableScanInQuery` peut être défini pour autoriser les analyses lorsque la stratégie d’indexation configurée ne peut pas prendre en charge la requête.</span><span class="sxs-lookup"><span data-stu-id="de9d7-935">`EnableScanInQuery` can be set to enable scans when the query cannot be supported by the configured indexing policy.</span></span> <span data-ttu-id="de9d7-936">Dans le cas des collections partitionnées, vous pouvez utiliser `PartitionKey` pour exécuter la requête sur une seule partition (bien que Cosmos DB puisse extraire automatiquement cet élément du texte de la requête) et `EnableCrossPartitionQuery` pour exécuter des requêtes qu’il peut être nécessaire d’exécuter sur plusieurs partitions.</span><span class="sxs-lookup"><span data-stu-id="de9d7-936">For partitioned collections, you can use `PartitionKey` to run the query against a single partition (though Cosmos DB can automatically extract this from the query text), and `EnableCrossPartitionQuery` to run queries that may need to be run against multiple partitions.</span></span> 

<span data-ttu-id="de9d7-937">Reportez-vous aux [Exemples .NET Azure Cosmos DB](https://github.com/Azure/azure-documentdb-net) pour obtenir plus d’exemples de requête.</span><span class="sxs-lookup"><span data-stu-id="de9d7-937">Refer to [Azure Cosmos DB .NET samples](https://github.com/Azure/azure-documentdb-net) for more samples containing queries.</span></span> 

### <span data-ttu-id="de9d7-938"><a id="JavaScriptServerSideApi"></a>API JavaScript côté serveur</span><span class="sxs-lookup"><span data-stu-id="de9d7-938"><a id="JavaScriptServerSideApi"></a>JavaScript server-side API</span></span>
<span data-ttu-id="de9d7-939">Cosmos DB fournit un modèle de programmation pour l’exécution de la logique d’application JavaScript directement sur les collections par le biais de procédures stockées et de déclencheurs.</span><span class="sxs-lookup"><span data-stu-id="de9d7-939">Cosmos DB provides a programming model for executing JavaScript based application logic directly on the collections using stored procedures and triggers.</span></span> <span data-ttu-id="de9d7-940">La logique JavaScript enregistrée au niveau d'une collection peut alors émettre des opérations de base de données sur les opérations des documents d'une collection donnée.</span><span class="sxs-lookup"><span data-stu-id="de9d7-940">The JavaScript logic registered at a collection level can then issue database operations on the operations on the documents of the given collection.</span></span> <span data-ttu-id="de9d7-941">Ces opérations sont encapsulées dans les transactions ACID ambiantes.</span><span class="sxs-lookup"><span data-stu-id="de9d7-941">These operations are wrapped in ambient ACID transactions.</span></span>

<span data-ttu-id="de9d7-942">L’exemple suivant illustre l’utilisation de queryDocuments dans l’API JavaScript côté serveur pour créer des requêtes depuis l’intérieur des procédures stockées et des déclencheurs.</span><span class="sxs-lookup"><span data-stu-id="de9d7-942">The following example shows how to use the queryDocuments in the JavaScript server API to make queries from inside stored procedures and triggers.</span></span>

    function businessLogic(name, author) {
        var context = getContext();
        var collectionManager = context.getCollection();
        var collectionLink = collectionManager.getSelfLink()

        // create a new document.
        collectionManager.createDocument(collectionLink,
            { name: name, author: author },
            function (err, documentCreated) {
                if (err) throw new Error(err.message);

                // filter documents by author
                var filterQuery = "SELECT * from root r WHERE r.author = 'George R.'";
                collectionManager.queryDocuments(collectionLink,
                    filterQuery,
                    function (err, matchingDocuments) {
                        if (err) throw new Error(err.message);
    context.getResponse().setBody(matchingDocuments.length);

                        // Replace the author name for all documents that satisfied the query.
                        for (var i = 0; i < matchingDocuments.length; i++) {
                            matchingDocuments[i].author = "George R. R. Martin";
                            // we don't need to execute a callback because they are in parallel
                            collectionManager.replaceDocument(matchingDocuments[i]._self,
                                matchingDocuments[i]);
                        }
                    })
            });
    }

## <span data-ttu-id="de9d7-943"><a id="References"></a>Références</span><span class="sxs-lookup"><span data-stu-id="de9d7-943"><a id="References"></a>References</span></span>
1. <span data-ttu-id="de9d7-944">[Présentation d’Azure Cosmos DB][introduction]</span><span class="sxs-lookup"><span data-stu-id="de9d7-944">[Introduction to Azure Cosmos DB][introduction]</span></span>
2. [<span data-ttu-id="de9d7-945">Spécification SQL Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="de9d7-945">Azure Cosmos DB SQL specification</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=510612)
3. [<span data-ttu-id="de9d7-946">Exemples .NET Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="de9d7-946">Azure Cosmos DB .NET samples</span></span>](https://github.com/Azure/azure-documentdb-net)
4. <span data-ttu-id="de9d7-947">[Niveaux de cohérence de base Azure Cosmos DB][consistency-levels]</span><span class="sxs-lookup"><span data-stu-id="de9d7-947">[Azure Cosmos DB Consistency Levels][consistency-levels]</span></span>
5. <span data-ttu-id="de9d7-948">ANSI SQL 2011 [http://www.iso.org/iso/iso_catalogue/catalogue_tc/catalogue_detail.htm?csnumber=53681](http://www.iso.org/iso/iso_catalogue/catalogue_tc/catalogue_detail.htm?csnumber=53681)</span><span class="sxs-lookup"><span data-stu-id="de9d7-948">ANSI SQL 2011 [http://www.iso.org/iso/iso_catalogue/catalogue_tc/catalogue_detail.htm?csnumber=53681](http://www.iso.org/iso/iso_catalogue/catalogue_tc/catalogue_detail.htm?csnumber=53681)</span></span>
6. <span data-ttu-id="de9d7-949">JSON [http://json.org/](http://json.org/)</span><span class="sxs-lookup"><span data-stu-id="de9d7-949">JSON [http://json.org/](http://json.org/)</span></span>
7. <span data-ttu-id="de9d7-950">Spécification Javascript [http://www.ecma-international.org/publications/standards/Ecma-262.htm](http://www.ecma-international.org/publications/standards/Ecma-262.htm)</span><span class="sxs-lookup"><span data-stu-id="de9d7-950">Javascript Specification [http://www.ecma-international.org/publications/standards/Ecma-262.htm](http://www.ecma-international.org/publications/standards/Ecma-262.htm)</span></span> 
8. <span data-ttu-id="de9d7-951">LINQ [http://msdn.microsoft.com/library/bb308959.aspx](http://msdn.microsoft.com/library/bb308959.aspx)</span><span class="sxs-lookup"><span data-stu-id="de9d7-951">LINQ [http://msdn.microsoft.com/library/bb308959.aspx](http://msdn.microsoft.com/library/bb308959.aspx)</span></span> 
9. <span data-ttu-id="de9d7-952">Techniques d’évaluation des requêtes pour les bases de données volumineuses [http://dl.acm.org/citation.cfm?id=152611](http://dl.acm.org/citation.cfm?id=152611)</span><span class="sxs-lookup"><span data-stu-id="de9d7-952">Query evaluation techniques for large databases [http://dl.acm.org/citation.cfm?id=152611](http://dl.acm.org/citation.cfm?id=152611)</span></span>
10. <span data-ttu-id="de9d7-953">Query Processing in Parallel Relational Database Systems, IEEE Computer Society Press, 1994</span><span class="sxs-lookup"><span data-stu-id="de9d7-953">Query Processing in Parallel Relational Database Systems, IEEE Computer Society Press, 1994</span></span>
11. <span data-ttu-id="de9d7-954">Lu, Ooi, Tan, Query Processing in Parallel Relational Database Systems, IEEE Computer Society Press, 1994.</span><span class="sxs-lookup"><span data-stu-id="de9d7-954">Lu, Ooi, Tan, Query Processing in Parallel Relational Database Systems, IEEE Computer Society Press, 1994.</span></span>
12. <span data-ttu-id="de9d7-955">Christopher Olston, Benjamin Reed, Utkarsh Srivastava, Ravi Kumar, Andrew Tomkins : Pig Latin: A Not-So-Foreign Language for Data Processing, SIGMOD 2008.</span><span class="sxs-lookup"><span data-stu-id="de9d7-955">Christopher Olston, Benjamin Reed, Utkarsh Srivastava, Ravi Kumar, Andrew Tomkins: Pig Latin: A Not-So-Foreign Language for Data Processing, SIGMOD 2008.</span></span>
13. <span data-ttu-id="de9d7-956">G.</span><span class="sxs-lookup"><span data-stu-id="de9d7-956">G.</span></span> <span data-ttu-id="de9d7-957">Graefe.</span><span class="sxs-lookup"><span data-stu-id="de9d7-957">Graefe.</span></span> <span data-ttu-id="de9d7-958">The Cascades framework for query optimization.</span><span class="sxs-lookup"><span data-stu-id="de9d7-958">The Cascades framework for query optimization.</span></span> <span data-ttu-id="de9d7-959">IEEE Data Eng.</span><span class="sxs-lookup"><span data-stu-id="de9d7-959">IEEE Data Eng.</span></span> <span data-ttu-id="de9d7-960">Bull., 18(3): 1995.</span><span class="sxs-lookup"><span data-stu-id="de9d7-960">Bull., 18(3): 1995.</span></span>

[1]: ./media/documentdb-sql-query/sql-query1.png
[introduction]: introduction.md
[consistency-levels]: consistency-levels.md