---
title: "requêtes aaaSQL pour l’API Azure Cosmos DB DocumentDB | Documents Microsoft"
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
ms.openlocfilehash: f4db95b87f5796c4e4299aaf016435cb6301bbfe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="sql-queries-for-azure-cosmos-db-documentdb-api"></a><span data-ttu-id="92424-105">Requêtes SQL pour l’API DocumentDB Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="92424-105">SQL queries for Azure Cosmos DB DocumentDB API</span></span>
<span data-ttu-id="92424-106">Microsoft Azure Cosmos DB prend en charge l’interrogation de documents à l’aide du langage SQL en tant que langage de requête JSON.</span><span class="sxs-lookup"><span data-stu-id="92424-106">Microsoft Azure Cosmos DB supports querying documents using SQL (Structured Query Language) as a JSON query language.</span></span> <span data-ttu-id="92424-107">Cosmos DB n’utilise pas de schéma.</span><span class="sxs-lookup"><span data-stu-id="92424-107">Cosmos DB is truly schema-free.</span></span> <span data-ttu-id="92424-108">En vertu de son engagement toohello JSON modèle de données directement dans le moteur de base de données hello, il fournit l’indexation automatique des documents JSON sans schéma explicite ou la création d’index secondaires.</span><span class="sxs-lookup"><span data-stu-id="92424-108">By virtue of its commitment toohello JSON data model directly within hello database engine, it provides automatic indexing of JSON documents without requiring explicit schema or creation of secondary indexes.</span></span> 

<span data-ttu-id="92424-109">Lors de la conception du langage de requête hello pour Cosmos DB, nous avions deux objectifs à l’esprit :</span><span class="sxs-lookup"><span data-stu-id="92424-109">While designing hello query language for Cosmos DB, we had two goals in mind:</span></span>

* <span data-ttu-id="92424-110">Au lieu d’un nouveau langage de requête JSON à inventer, nous voulions toosupport SQL.</span><span class="sxs-lookup"><span data-stu-id="92424-110">Instead of inventing a new JSON query language, we wanted toosupport SQL.</span></span> <span data-ttu-id="92424-111">SQL est un des langages de requête plus populaires et familiers hello.</span><span class="sxs-lookup"><span data-stu-id="92424-111">SQL is one of hello most familiar and popular query languages.</span></span> <span data-ttu-id="92424-112">Le langage SQL de Cosmos DB fournit un modèle de programmation formel pour créer des requêtes élaborées sur les documents JSON.</span><span class="sxs-lookup"><span data-stu-id="92424-112">Cosmos DB SQL provides a formal programming model for rich queries over JSON documents.</span></span>
* <span data-ttu-id="92424-113">Comme une base de document JSON est capable d’exécuter JavaScript directement dans le moteur de base de données hello, nous voulions modèle de programmation de toouse JavaScript en tant que base de hello pour le langage de requête.</span><span class="sxs-lookup"><span data-stu-id="92424-113">As a JSON document database capable of executing JavaScript directly in hello database engine, we wanted toouse JavaScript's programming model as hello foundation for our query language.</span></span> <span data-ttu-id="92424-114">Hello DocumentDB API SQL racine se trouve dans le système de type de JavaScript, évaluation de l’expression et l’appel de fonction.</span><span class="sxs-lookup"><span data-stu-id="92424-114">hello DocumentDB API SQL is rooted in JavaScript's type system, expression evaluation, and function invocation.</span></span> <span data-ttu-id="92424-115">En retour, cela fournit un modèle de programmation naturel pour les projections relationnelles, la navigation hiérarchique entre les documents JSON, les jointures réflexives, les requêtes spatiales et l’appel de fonctions définies par l’utilisateur écrites entièrement en JavaScript, entre autres fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="92424-115">This in-turn provides a natural programming model for relational projections, hierarchical navigation across JSON documents, self joins, spatial queries, and invocation of user-defined functions (UDFs) written entirely in JavaScript, among other features.</span></span> 

<span data-ttu-id="92424-116">Nous pensons que ces fonctionnalités sont friction de hello tooreducing clé entre l’application hello et la base de données hello et sont cruciale pour la productivité des développeurs.</span><span class="sxs-lookup"><span data-stu-id="92424-116">We believe that these capabilities are key tooreducing hello friction between hello application and hello database and are crucial for developer productivity.</span></span>

<span data-ttu-id="92424-117">Nous vous recommandons de mise en route en regardant hello suivant vidéo, où Aravind Ramachandran montre les fonctionnalités d’interrogation de base de données Cosmos et en vous rendant sur notre [Query Playground](http://www.documentdb.com/sql/demo), où vous pouvez essayer Cosmos DB et exécuter des requêtes SQL sur notre jeu de données.</span><span class="sxs-lookup"><span data-stu-id="92424-117">We recommend getting started by watching hello following video, where Aravind Ramachandran shows Cosmos DB's querying capabilities, and by visiting our [Query Playground](http://www.documentdb.com/sql/demo), where you can try out Cosmos DB and run SQL queries against our dataset.</span></span>

> [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/DataExposedQueryingDocumentDB/player]
> 
> 

<span data-ttu-id="92424-118">Ensuite, retourner l’article toothis, où nous commençons avec un didacticiel de requête SQL qui vous guide à travers certains documents JSON simples et les commandes SQL.</span><span class="sxs-lookup"><span data-stu-id="92424-118">Then, return toothis article, where we start with a SQL query tutorial that walks you through some simple JSON documents and SQL commands.</span></span>

## <span data-ttu-id="92424-119"><a id="GettingStarted"></a>Prise en main des commandes du langage SQL dans Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="92424-119"><a id="GettingStarted"></a>Getting started with SQL commands in Cosmos DB</span></span>
<span data-ttu-id="92424-120">toosee Cosmos DB SQL au travail, nous allons commencer avec des documents JSON simples et suivre les étapes certaines requêtes simples.</span><span class="sxs-lookup"><span data-stu-id="92424-120">toosee Cosmos DB SQL at work, let's begin with a few simple JSON documents and walk through some simple queries against it.</span></span> <span data-ttu-id="92424-121">Prenez ces deux documents JSON relatifs à deux familles.</span><span class="sxs-lookup"><span data-stu-id="92424-121">Consider these two JSON documents about two families.</span></span> <span data-ttu-id="92424-122">Avec la base de données Cosmos, nous n’avez pas besoin toocreate les schémas ou un index secondaire explicitement.</span><span class="sxs-lookup"><span data-stu-id="92424-122">With Cosmos DB, we do not need toocreate any schemas or secondary indices explicitly.</span></span> <span data-ttu-id="92424-123">Nous suffit tooinsert hello JSON documents tooa Cosmos DB collection et de requête par la suite.</span><span class="sxs-lookup"><span data-stu-id="92424-123">We simply need tooinsert hello JSON documents tooa Cosmos DB collection and subsequently query.</span></span> <span data-ttu-id="92424-124">Ici, nous avons JSON simple document pour hello famille de Andersen, hello parents, enfants (et leurs animaux), adresse et les informations d’inscription.</span><span class="sxs-lookup"><span data-stu-id="92424-124">Here we have a simple JSON document for hello Andersen family, hello parents, children (and their pets), address, and registration information.</span></span> <span data-ttu-id="92424-125">document de Hello possède des chaînes, des nombres, des valeurs booléennes, des tableaux et des propriétés imbriquées.</span><span class="sxs-lookup"><span data-stu-id="92424-125">hello document has strings, numbers, Booleans, arrays, and nested properties.</span></span> 

<span data-ttu-id="92424-126">**Document**</span><span class="sxs-lookup"><span data-stu-id="92424-126">**Document**</span></span>  

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

<span data-ttu-id="92424-127">Voici un second document comportant une différence subtile : `givenName` et `familyName` sont utilisés au lieu de `firstName` et `lastName`.</span><span class="sxs-lookup"><span data-stu-id="92424-127">Here's a second document with one subtle difference – `givenName` and `familyName` are used instead of `firstName` and `lastName`.</span></span>

<span data-ttu-id="92424-128">**Document**</span><span class="sxs-lookup"><span data-stu-id="92424-128">**Document**</span></span>  

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

<span data-ttu-id="92424-129">Désormais tentons des requêtes par rapport à cette toounderstand données hello certains aspects clés du DocumentDB API SQL.</span><span class="sxs-lookup"><span data-stu-id="92424-129">Now let's try a few queries against this data toounderstand some of hello key aspects of DocumentDB API SQL.</span></span> <span data-ttu-id="92424-130">Par exemple, suivant de hello requête renvoie des documents hello où correspond au champ de code hello `AndersenFamily`.</span><span class="sxs-lookup"><span data-stu-id="92424-130">For example, hello following query returns hello documents where hello id field matches `AndersenFamily`.</span></span> <span data-ttu-id="92424-131">Dans la mesure où il s’agit d’un `SELECT *`, sortie hello de requête de hello est le document JSON complet hello :</span><span class="sxs-lookup"><span data-stu-id="92424-131">Since it's a `SELECT *`, hello output of hello query is hello complete JSON document:</span></span>

<span data-ttu-id="92424-132">**Requête**</span><span class="sxs-lookup"><span data-stu-id="92424-132">**Query**</span></span>

    SELECT * 
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="92424-133">**Résultats**</span><span class="sxs-lookup"><span data-stu-id="92424-133">**Results**</span></span>

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


<span data-ttu-id="92424-134">Considérez maintenant le cas de hello où nous devons tooreformat hello la sortie JSON dans une forme différente.</span><span class="sxs-lookup"><span data-stu-id="92424-134">Now consider hello case where we need tooreformat hello JSON output in a different shape.</span></span> <span data-ttu-id="92424-135">Cette requête avec deux champs sélectionnés, nom et la ville, de l’objet projets un nouveau JSON quand des hello ville a hello même nom en tant qu’état de hello.</span><span class="sxs-lookup"><span data-stu-id="92424-135">This query projects a new JSON object with two selected fields, Name and City, when hello address' city has hello same name as hello state.</span></span> <span data-ttu-id="92424-136">Dans ce cas, « NY, NY » correspond.</span><span class="sxs-lookup"><span data-stu-id="92424-136">In this case, "NY, NY" matches.</span></span>

<span data-ttu-id="92424-137">**Requête**</span><span class="sxs-lookup"><span data-stu-id="92424-137">**Query**</span></span>    

    SELECT {"Name":f.id, "City":f.address.city} AS Family 
    FROM Families f 
    WHERE f.address.city = f.address.state

<span data-ttu-id="92424-138">**Résultats**</span><span class="sxs-lookup"><span data-stu-id="92424-138">**Results**</span></span>

    [{
        "Family": {
            "Name": "WakefieldFamily", 
            "City": "NY"
        }
    }]


<span data-ttu-id="92424-139">les requêtes suivant Hello retourne tous les noms de donné de hello d’enfants dans la famille hello dont l’id correspond à `WakefieldFamily` classés par ville hello de résidence.</span><span class="sxs-lookup"><span data-stu-id="92424-139">hello next query returns all hello given names of children in hello family whose id matches `WakefieldFamily` ordered by hello city of residence.</span></span>

<span data-ttu-id="92424-140">**Requête**</span><span class="sxs-lookup"><span data-stu-id="92424-140">**Query**</span></span>

    SELECT c.givenName 
    FROM Families f 
    JOIN c IN f.children 
    WHERE f.id = 'WakefieldFamily'
    ORDER BY f.address.city ASC

<span data-ttu-id="92424-141">**Résultats**</span><span class="sxs-lookup"><span data-stu-id="92424-141">**Results**</span></span>

    [
      { "givenName": "Jesse" }, 
      { "givenName": "Lisa"}
    ]


<span data-ttu-id="92424-142">Nous aimerions tooa d’attention toodraw exemples hello que nous avons vu jusqu'à présent de langage de requête de quelques aspects dignes d’intérêt de hello Cosmos DB :</span><span class="sxs-lookup"><span data-stu-id="92424-142">We would like toodraw attention tooa few noteworthy aspects of hello Cosmos DB query language through hello examples we've seen so far:</span></span>  

* <span data-ttu-id="92424-143">Comme le langage SQL de l’API DocumentDB fonctionne avec les valeurs JSON, il traite des entités d’arborescence au lieu des lignes et des colonnes.</span><span class="sxs-lookup"><span data-stu-id="92424-143">Since DocumentDB API SQL works on JSON values, it deals with tree shaped entities instead of rows and columns.</span></span> <span data-ttu-id="92424-144">Par conséquent, langage de hello permet de faire référence toonodes d’arborescence hello à toute profondeur arbitraire, comme `Node1.Node2.Node3…..Nodem`, similaire toorelational SQL référence toohello deux référence de partie de `<table>.<column>`.</span><span class="sxs-lookup"><span data-stu-id="92424-144">Therefore, hello language lets you refer toonodes of hello tree at any arbitrary depth, like `Node1.Node2.Node3…..Nodem`, similar toorelational SQL referring toohello two part reference of `<table>.<column>`.</span></span>   
* <span data-ttu-id="92424-145">Hello structuré fonctionne de langage de requête avec des données sans schéma.</span><span class="sxs-lookup"><span data-stu-id="92424-145">hello structured query language works with schema-less data.</span></span> <span data-ttu-id="92424-146">Par conséquent, hello type système besoins toobe limite dynamiquement.</span><span class="sxs-lookup"><span data-stu-id="92424-146">Therefore, hello type system needs toobe bound dynamically.</span></span> <span data-ttu-id="92424-147">Hello même expression peut produire des types différents sur des documents.</span><span class="sxs-lookup"><span data-stu-id="92424-147">hello same expression could yield different types on different documents.</span></span> <span data-ttu-id="92424-148">résultat de Hello d’une requête est une valeur JSON valide, mais n’est pas garanti toobe d’un schéma fixe.</span><span class="sxs-lookup"><span data-stu-id="92424-148">hello result of a query is a valid JSON value, but is not guaranteed toobe of a fixed schema.</span></span>  
* <span data-ttu-id="92424-149">Cosmos DB prend uniquement en charge les documents JSON stricts.</span><span class="sxs-lookup"><span data-stu-id="92424-149">Cosmos DB only supports strict JSON documents.</span></span> <span data-ttu-id="92424-150">Cela signifie les expressions et système de type hello sont restreinte toodeal uniquement avec les types JSON.</span><span class="sxs-lookup"><span data-stu-id="92424-150">This means hello type system and expressions are restricted toodeal only with JSON types.</span></span> <span data-ttu-id="92424-151">Consultez toohello [spécification JSON](http://www.json.org/) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="92424-151">Refer toohello [JSON specification](http://www.json.org/) for more details.</span></span>  
* <span data-ttu-id="92424-152">Une collection Cosmos DB est un conteneur sans schéma pour vos documents JSON.</span><span class="sxs-lookup"><span data-stu-id="92424-152">A Cosmos DB collection is a schema-free container of JSON documents.</span></span> <span data-ttu-id="92424-153">relations Hello dans les entités dans et entre des documents dans une collection de données sont implicitement capturées par la relation contenant-contenu et non par des relations de clé étrangères et de clé primaire.</span><span class="sxs-lookup"><span data-stu-id="92424-153">hello relations in data entities within and across documents in a collection are implicitly captured by containment and not by primary key and foreign key relations.</span></span> <span data-ttu-id="92424-154">Il s’agit d’un aspect important de noter abordez jointures intra-document de hello présentés plus loin dans cet article.</span><span class="sxs-lookup"><span data-stu-id="92424-154">This is an important aspect worth pointing out in light of hello intra-document joins discussed later in this article.</span></span>

## <span data-ttu-id="92424-155"><a id="Indexing"></a> Indexation Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="92424-155"><a id="Indexing"></a> Cosmos DB indexing</span></span>
<span data-ttu-id="92424-156">Avant de passer à hello syntaxe DocumentDB API SQL, il convient d’Explorer hello l’indexation de conception dans la base de données Cosmos.</span><span class="sxs-lookup"><span data-stu-id="92424-156">Before we get into hello DocumentDB API SQL syntax, it is worth exploring hello indexing design in Cosmos DB.</span></span> 

<span data-ttu-id="92424-157">Hello d’index de base de données vise requêtes tooserve dans leurs diverses formes et les formes avec une consommation minimale des ressources (telles que l’UC et d’entrée/sortie) tout en fournissant un débit relativement élevé et une faible latence.</span><span class="sxs-lookup"><span data-stu-id="92424-157">hello purpose of database indexes is tooserve queries in their various forms and shapes with minimum resource consumption (like CPU and input/output) while providing good throughput and low latency.</span></span> <span data-ttu-id="92424-158">Souvent, les choix hello de l’index de droit hello pour interroger une base de données nécessite beaucoup de planification et d’expérimentation.</span><span class="sxs-lookup"><span data-stu-id="92424-158">Often, hello choice of hello right index for querying a database requires much planning and experimentation.</span></span> <span data-ttu-id="92424-159">Cette approche présente une difficulté pour les bases de données sans schéma où les données de salutation tooa stricte de schéma n’est pas conforme et évoluent rapidement.</span><span class="sxs-lookup"><span data-stu-id="92424-159">This approach poses a challenge for schema-less databases where hello data doesn’t conform tooa strict schema and evolves rapidly.</span></span> 

<span data-ttu-id="92424-160">Par conséquent, lorsque nous avons conçu sous-système d’indexation de hello Cosmos DB, nous avons défini hello suivant objectifs :</span><span class="sxs-lookup"><span data-stu-id="92424-160">Therefore, when we designed hello Cosmos DB indexing subsystem, we set hello following goals:</span></span>

* <span data-ttu-id="92424-161">Indexer les documents sans nécessiter de schéma : hello indexation sous-système ne pas exiger des informations de schéma ou faire d’hypothèses concernant les schémas de documents de hello.</span><span class="sxs-lookup"><span data-stu-id="92424-161">Index documents without requiring schema: hello indexing subsystem does not require any schema information or make any assumptions about schema of hello documents.</span></span> 
* <span data-ttu-id="92424-162">Prend en charge pour les requêtes relationnelles et hiérarchiques efficaces et riches : hello index prend en charge le langage de requête Cosmos DB hello efficacement, y compris la prise en charge pour les projections relationnelles et hiérarchiques.</span><span class="sxs-lookup"><span data-stu-id="92424-162">Support for efficient, rich hierarchical, and relational queries: hello index supports hello Cosmos DB query language efficiently, including support for hierarchical and relational projections.</span></span>
* <span data-ttu-id="92424-163">Prise en charge pour les requêtes cohérents résister à un volume maintenu d’écritures : pour écriture haute débit les charges de travail avec des requêtes cohérents, hello index est mis à jour de façon incrémentielle, efficacement et en ligne en face de hello d’un volume maintenu d’écritures.</span><span class="sxs-lookup"><span data-stu-id="92424-163">Support for consistent queries in face of a sustained volume of writes: For high write throughput workloads with consistent queries, hello index is updated incrementally, efficiently, and online in hello face of a sustained volume of writes.</span></span> <span data-ttu-id="92424-164">mise à jour des index cohérent de Hello est cruciale tooserve les requêtes de hello au niveau de cohérence hello dans le service de document hello hello utilisateur configuré.</span><span class="sxs-lookup"><span data-stu-id="92424-164">hello consistent index update is crucial tooserve hello queries at hello consistency level in which hello user configured hello document service.</span></span>
* <span data-ttu-id="92424-165">Prise en charge d’une architecture mutualisée : Breakfast hello réservation-modèle de gouvernance des ressources locataires, mises à jour de l’index sont effectuées dans budget hello des ressources système (processeur, mémoire et les opérations d’entrée/sortie par seconde) allouée par le réplica.</span><span class="sxs-lookup"><span data-stu-id="92424-165">Support for multi-tenancy: Given hello reservation-based model for resource governance across tenants, index updates are performed within hello budget of system resources (CPU, memory, and input/output operations per second) allocated per replica.</span></span> 
* <span data-ttu-id="92424-166">L’efficacité du stockage : de rentabilité, stockage sur disque hello surcharge d’index de hello est limitée et prévisibles.</span><span class="sxs-lookup"><span data-stu-id="92424-166">Storage efficiency: For cost effectiveness, hello on-disk storage overhead of hello index is bounded and predictable.</span></span> <span data-ttu-id="92424-167">Cela est essentiel car Cosmos DB permet hello développeur toomake basé sur coût compromis traitement des index dans les performances des requêtes toohello relation.</span><span class="sxs-lookup"><span data-stu-id="92424-167">This is crucial because Cosmos DB allows hello developer toomake cost-based tradeoffs between index overhead in relation toohello query performance.</span></span>  

<span data-ttu-id="92424-168">Consultez toohello [exemples de base de données Azure Cosmos](https://github.com/Azure/azure-documentdb-net) sur MSDN pour obtenir des exemples montrant comment tooconfigure hello stratégie d’indexation pour une collection.</span><span class="sxs-lookup"><span data-stu-id="92424-168">Refer toohello [Azure Cosmos DB samples](https://github.com/Azure/azure-documentdb-net) on MSDN for samples showing how tooconfigure hello indexing policy for a collection.</span></span> <span data-ttu-id="92424-169">Nous allons désormais obtenir les détails de hello de hello syntaxe SQL de base de données Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="92424-169">Let’s now get into hello details of hello Azure Cosmos DB SQL syntax.</span></span>

## <span data-ttu-id="92424-170"><a id="Basics"></a>Principes de base d’une requête SQL Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="92424-170"><a id="Basics"></a>Basics of an Azure Cosmos DB SQL query</span></span>
<span data-ttu-id="92424-171">Chaque requête se compose d'une clause SELECT et de clauses FROM et WHERE facultatives conformes aux normes ANSI-SQL.</span><span class="sxs-lookup"><span data-stu-id="92424-171">Every query consists of a SELECT clause and optional FROM and WHERE clauses per ANSI-SQL standards.</span></span> <span data-ttu-id="92424-172">En règle générale, pour chaque requête, source hello dans la clause FROM de hello est énuméré.</span><span class="sxs-lookup"><span data-stu-id="92424-172">Typically, for each query, hello source in hello FROM clause is enumerated.</span></span> <span data-ttu-id="92424-173">Hello filtrer dans la clause WHERE est appliquée sur hello source tooretrieve de hello un sous-ensemble de documents JSON.</span><span class="sxs-lookup"><span data-stu-id="92424-173">Then hello filter in hello WHERE clause is applied on hello source tooretrieve a subset of JSON documents.</span></span> <span data-ttu-id="92424-174">Enfin, la clause SELECT de hello est utilisé tooproject hello demandé la liste de sélection de valeurs JSON dans hello.</span><span class="sxs-lookup"><span data-stu-id="92424-174">Finally, hello SELECT clause is used tooproject hello requested JSON values in hello select list.</span></span>

    SELECT <select_list> 
    [FROM <from_specification>] 
    [WHERE <filter_condition>]
    [ORDER BY <sort_specification]    


## <span data-ttu-id="92424-175"><a id="FromClause"></a>Clause FROM</span><span class="sxs-lookup"><span data-stu-id="92424-175"><a id="FromClause"></a>FROM clause</span></span>
<span data-ttu-id="92424-176">Hello `FROM <from_specification>` clause est facultative, sauf si la source de hello est filtrée ou projeté plus loin dans la requête de hello.</span><span class="sxs-lookup"><span data-stu-id="92424-176">hello `FROM <from_specification>` clause is optional unless hello source is filtered or projected later in hello query.</span></span> <span data-ttu-id="92424-177">objectif de Hello de cette clause est source de données toospecify hello sur quel hello requête doit fonctionner.</span><span class="sxs-lookup"><span data-stu-id="92424-177">hello purpose of this clause is toospecify hello data source upon which hello query must operate.</span></span> <span data-ttu-id="92424-178">Couramment ensemble de la collection hello est source de hello, mais on peut spécifier un sous-ensemble de la collection de hello à la place.</span><span class="sxs-lookup"><span data-stu-id="92424-178">Commonly hello whole collection is hello source, but one can specify a subset of hello collection instead.</span></span> 

<span data-ttu-id="92424-179">Une requête comme `SELECT * FROM Families` indique que l’ensemble des familles hello est source de hello via le tooenumerate.</span><span class="sxs-lookup"><span data-stu-id="92424-179">A query like `SELECT * FROM Families` indicates that hello entire Families collection is hello source over which tooenumerate.</span></span> <span data-ttu-id="92424-180">Un identificateur spécial racine peut être la collection de hello toorepresent utilisé au lieu d’utiliser le nom de la collection hello.</span><span class="sxs-lookup"><span data-stu-id="92424-180">A special identifier ROOT can be used toorepresent hello collection instead of using hello collection name.</span></span> <span data-ttu-id="92424-181">Hello liste suivante contient des hello règles qui sont appliquées par la requête :</span><span class="sxs-lookup"><span data-stu-id="92424-181">hello following list contains hello rules that are enforced per query:</span></span>

* <span data-ttu-id="92424-182">collection de Hello peut être un alias, tel que `SELECT f.id FROM Families AS f` ou simplement `SELECT f.id FROM Families f`.</span><span class="sxs-lookup"><span data-stu-id="92424-182">hello collection can be aliased, such as `SELECT f.id FROM Families AS f` or simply `SELECT f.id FROM Families f`.</span></span> <span data-ttu-id="92424-183">Ici `f` revient à hello `Families`.</span><span class="sxs-lookup"><span data-stu-id="92424-183">Here `f` is hello equivalent of `Families`.</span></span> <span data-ttu-id="92424-184">`AS`est un identificateur de hello tooalias mot clé facultatif.</span><span class="sxs-lookup"><span data-stu-id="92424-184">`AS` is an optional keyword tooalias hello identifier.</span></span>
* <span data-ttu-id="92424-185">Une fois un alias, source d’origine de hello ne peut pas être lié.</span><span class="sxs-lookup"><span data-stu-id="92424-185">Once aliased, hello original source cannot be bound.</span></span> <span data-ttu-id="92424-186">Par exemple, `SELECT Families.id FROM Families f` est syntaxiquement non valide, car l’identificateur hello « Familles » ne peut pas être résolu plus.</span><span class="sxs-lookup"><span data-stu-id="92424-186">For example, `SELECT Families.id FROM Families f` is syntactically invalid since hello identifier "Families" cannot be resolved anymore.</span></span>
* <span data-ttu-id="92424-187">Toutes les propriétés qui doivent toobe référencée doivent être qualifiées complet.</span><span class="sxs-lookup"><span data-stu-id="92424-187">All properties that need toobe referenced must be fully qualified.</span></span> <span data-ttu-id="92424-188">En absence de hello de respect de la stricte de schéma, il s’agit de tooavoid appliqué toutes les liaisons ambiguës.</span><span class="sxs-lookup"><span data-stu-id="92424-188">In hello absence of strict schema adherence, this is enforced tooavoid any ambiguous bindings.</span></span> <span data-ttu-id="92424-189">Par conséquent, `SELECT id FROM Families f` est syntaxiquement incorrecte depuis la propriété de hello `id` n’est pas lié.</span><span class="sxs-lookup"><span data-stu-id="92424-189">Therefore, `SELECT id FROM Families f` is syntactically invalid since hello property `id` is not bound.</span></span>

### <a name="subdocuments"></a><span data-ttu-id="92424-190">Sous-documents</span><span class="sxs-lookup"><span data-stu-id="92424-190">Subdocuments</span></span>
<span data-ttu-id="92424-191">Hello source peut également être réduite tooa plus petit sous-ensemble.</span><span class="sxs-lookup"><span data-stu-id="92424-191">hello source can also be reduced tooa smaller subset.</span></span> <span data-ttu-id="92424-192">Par exemple, tooenumerating uniquement une sous-arborescence dans chaque document, subroot de hello pourrait devenir puis hello source, comme indiqué dans hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="92424-192">For instance, tooenumerating only a subtree in each document, hello subroot could then become hello source, as shown in hello following example:</span></span>

<span data-ttu-id="92424-193">**Requête**</span><span class="sxs-lookup"><span data-stu-id="92424-193">**Query**</span></span>

    SELECT * 
    FROM Families.children

<span data-ttu-id="92424-194">**Résultats**</span><span class="sxs-lookup"><span data-stu-id="92424-194">**Results**</span></span>  

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

<span data-ttu-id="92424-195">Est hello exemple ci-dessus a utilisé un tableau en tant que source de hello, un objet peut également servir en tant que source de hello, qui est ce que montre hello l’exemple suivant : toute valeur JSON valide (non définie) qui se trouvent dans la source de hello est pris en compte pour l’inclure dans le résultat de hello de requête de Hello.</span><span class="sxs-lookup"><span data-stu-id="92424-195">While hello above example used an array as hello source, an object could also be used as hello source, which is what's shown in hello following example: Any valid JSON value (not undefined) that can be found in hello source is considered for inclusion in hello result of hello query.</span></span> <span data-ttu-id="92424-196">Si vous n’ont pas certaines familles un `address.state` valeur, elles sont exclues dans le résultat de la requête hello.</span><span class="sxs-lookup"><span data-stu-id="92424-196">If some families don’t have an `address.state` value, they are excluded in hello query result.</span></span>

<span data-ttu-id="92424-197">**Requête**</span><span class="sxs-lookup"><span data-stu-id="92424-197">**Query**</span></span>

    SELECT * 
    FROM Families.address.state

<span data-ttu-id="92424-198">**Résultats**</span><span class="sxs-lookup"><span data-stu-id="92424-198">**Results**</span></span>

    [
      "WA", 
      "NY"
    ]


## <span data-ttu-id="92424-199"><a id="WhereClause"></a>Clause WHERE</span><span class="sxs-lookup"><span data-stu-id="92424-199"><a id="WhereClause"></a>WHERE clause</span></span>
<span data-ttu-id="92424-200">Hello clause WHERE (**`WHERE <filter_condition>`**) est facultatif.</span><span class="sxs-lookup"><span data-stu-id="92424-200">hello WHERE clause (**`WHERE <filter_condition>`**) is optional.</span></span> <span data-ttu-id="92424-201">Il spécifie hello condition que les documents JSON hello fournies par hello source doivent satisfaire toobe ordre inclus en tant que partie du résultat de hello.</span><span class="sxs-lookup"><span data-stu-id="92424-201">It specifies hello condition(s) that hello JSON documents provided by hello source must satisfy in order toobe included as part of hello result.</span></span> <span data-ttu-id="92424-202">N’importe quel document JSON doit évaluer hello spécifié conditions trop « true » toobe pris en compte pour le résultat de hello.</span><span class="sxs-lookup"><span data-stu-id="92424-202">Any JSON document must evaluate hello specified conditions too"true" toobe considered for hello result.</span></span> <span data-ttu-id="92424-203">Hello où clause est utilisée par couche d’index hello dans l’ordre toodetermine hello absolu plus petit sous-ensemble de documents source qui peuvent faire partie du résultat de hello.</span><span class="sxs-lookup"><span data-stu-id="92424-203">hello WHERE clause is used by hello index layer in order toodetermine hello absolute smallest subset of source documents that can be part of hello result.</span></span> 

<span data-ttu-id="92424-204">Hello requête suivante demande des documents qui contiennent une propriété de nom dont la valeur est `AndersenFamily`.</span><span class="sxs-lookup"><span data-stu-id="92424-204">hello following query requests documents that contain a name property whose value is `AndersenFamily`.</span></span> <span data-ttu-id="92424-205">Tout autre document qui ne dispose pas d’une propriété de nom, ou lorsque la valeur de hello ne correspond pas à `AndersenFamily` est exclu.</span><span class="sxs-lookup"><span data-stu-id="92424-205">Any other document that does not have a name property, or where hello value does not match `AndersenFamily` is excluded.</span></span> 

<span data-ttu-id="92424-206">**Requête**</span><span class="sxs-lookup"><span data-stu-id="92424-206">**Query**</span></span>

    SELECT f.address
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="92424-207">**Résultats**</span><span class="sxs-lookup"><span data-stu-id="92424-207">**Results**</span></span>

    [{
      "address": {
        "state": "WA", 
        "county": "King", 
        "city": "seattle"
      }
    }]


<span data-ttu-id="92424-208">Hello l’exemple précédent a montré une requête simple d’égalité.</span><span class="sxs-lookup"><span data-stu-id="92424-208">hello previous example showed a simple equality query.</span></span> <span data-ttu-id="92424-209">Le langage SQL de l’API DocumentDB prend également en charge plusieurs expressions scalaires.</span><span class="sxs-lookup"><span data-stu-id="92424-209">DocumentDB API SQL also supports a variety of scalar expressions.</span></span> <span data-ttu-id="92424-210">Hello couramment utilisé sont des expressions binaires et unaire.</span><span class="sxs-lookup"><span data-stu-id="92424-210">hello most commonly used are binary and unary expressions.</span></span> <span data-ttu-id="92424-211">Références de propriété à partir de l’objet JSON hello source sont également des expressions valides.</span><span class="sxs-lookup"><span data-stu-id="92424-211">Property references from hello source JSON object are also valid expressions.</span></span> 

<span data-ttu-id="92424-212">Hello après les opérateurs binaires est actuellement pris en charge et peut être utilisé dans les requêtes, comme indiqué dans hello exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="92424-212">hello following binary operators are currently supported and can be used in queries as shown in hello following examples:</span></span>  

<table>
<tr>
<td><span data-ttu-id="92424-213">Opérateurs arithmétiques</span><span class="sxs-lookup"><span data-stu-id="92424-213">Arithmetic</span></span></td>    
<td><span data-ttu-id="92424-214">+,-,*,/,%</span><span class="sxs-lookup"><span data-stu-id="92424-214">+,-,*,/,%</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="92424-215">Opérateurs au niveau du bit</span><span class="sxs-lookup"><span data-stu-id="92424-215">Bitwise</span></span></td>    
<td><span data-ttu-id="92424-216">|, &, ^, <<, >>, >>> (décalage vers la droite avec remplissage de zéros)</span><span class="sxs-lookup"><span data-stu-id="92424-216">|, &, ^, <<, >>, >>> (zero-fill right shift)</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="92424-217">Opérateurs logiques</span><span class="sxs-lookup"><span data-stu-id="92424-217">Logical</span></span></td>
<td><span data-ttu-id="92424-218">AND, OR, NOT</span><span class="sxs-lookup"><span data-stu-id="92424-218">AND, OR, NOT</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="92424-219">Opérateurs de comparaison</span><span class="sxs-lookup"><span data-stu-id="92424-219">Comparison</span></span></td>    
<td><span data-ttu-id="92424-220">=, !=, &lt;, &gt;, &lt;=, &gt;=, <></span><span class="sxs-lookup"><span data-stu-id="92424-220">=, !=, &lt;, &gt;, &lt;=, &gt;=, <></span></span></td>
</tr>
<tr>
<td><span data-ttu-id="92424-221">String</span><span class="sxs-lookup"><span data-stu-id="92424-221">String</span></span></td>    
<td><span data-ttu-id="92424-222">|| (concaténer)</span><span class="sxs-lookup"><span data-stu-id="92424-222">|| (concatenate)</span></span></td>
</tr>
</table>  


<span data-ttu-id="92424-223">Examinons certaines requêtes utilisant des opérateurs binaires.</span><span class="sxs-lookup"><span data-stu-id="92424-223">Let’s take a look at some queries using binary operators.</span></span>

    SELECT * 
    FROM Families.children[0] c
    WHERE c.grade % 2 = 1     -- matching grades == 5, 1

    SELECT * 
    FROM Families.children[0] c
    WHERE c.grade ^ 4 = 1    -- matching grades == 5

    SELECT *
    FROM Families.children[0] c
    WHERE c.grade >= 5     -- matching grades == 5


<span data-ttu-id="92424-224">Hello opérateurs unaires +,-, ~ pas sont également prises en charge et peut être utilisé dans des requêtes, comme indiqué dans hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="92424-224">hello unary operators +,-, ~ and NOT are also supported, and can be used inside queries as shown in hello following example:</span></span>

    SELECT *
    FROM Families.children[0] c
    WHERE NOT(c.grade = 5)  -- matching grades == 1

    SELECT *
    FROM Families.children[0] c
    WHERE (-c.grade = -5)  -- matching grades == 5



<span data-ttu-id="92424-225">En outre toobinary et les opérateurs unaires, des références de propriété sont également autorisées.</span><span class="sxs-lookup"><span data-stu-id="92424-225">In addition toobinary and unary operators, property references are also allowed.</span></span> <span data-ttu-id="92424-226">Par exemple, `SELECT * FROM Families f WHERE f.isRegistered` renvoie hello document JSON qui contient la propriété de hello `isRegistered` où la valeur de la propriété hello est égal toohello JSON `true` valeur.</span><span class="sxs-lookup"><span data-stu-id="92424-226">For example, `SELECT * FROM Families f WHERE f.isRegistered` returns hello JSON document containing hello property `isRegistered` where hello property's value is equal toohello JSON `true` value.</span></span> <span data-ttu-id="92424-227">Toutes les autres valeurs (false, null, non défini, `<number>`, `<string>`, `<object>`, `<array>`, etc.) entraîne le document de source toohello est exclu de résultat de hello.</span><span class="sxs-lookup"><span data-stu-id="92424-227">Any other values (false, null, Undefined, `<number>`, `<string>`, `<object>`, `<array>`, etc.) leads toohello source document being excluded from hello result.</span></span> 

### <a name="equality-and-comparison-operators"></a><span data-ttu-id="92424-228">Opérateurs d'égalité et de comparaison</span><span class="sxs-lookup"><span data-stu-id="92424-228">Equality and comparison operators</span></span>
<span data-ttu-id="92424-229">Hello tableau suivant montre les résultats hello de comparaisons d’égalité dans DocumentDB API SQL entre deux types JSON.</span><span class="sxs-lookup"><span data-stu-id="92424-229">hello following table shows hello result of equality comparisons in DocumentDB API SQL between any two JSON types.</span></span>

<table style = "width:300px">
   <tbody>
      <tr>
         <td valign="top"><span data-ttu-id="92424-230">
            <strong>Op</strong>
         </span><span class="sxs-lookup"><span data-stu-id="92424-230">
            <strong>Op</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="92424-231">
            <strong>Undefined</strong>
         </span><span class="sxs-lookup"><span data-stu-id="92424-231">
            <strong>Undefined</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="92424-232">
            <strong>Null</strong>
         </span><span class="sxs-lookup"><span data-stu-id="92424-232">
            <strong>Null</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="92424-233">
            <strong>Boolean</strong>
         </span><span class="sxs-lookup"><span data-stu-id="92424-233">
            <strong>Boolean</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="92424-234">
            <strong>Number</strong>
         </span><span class="sxs-lookup"><span data-stu-id="92424-234">
            <strong>Number</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="92424-235">
            <strong>String</strong>
         </span><span class="sxs-lookup"><span data-stu-id="92424-235">
            <strong>String</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="92424-236">
            <strong>Object</strong>
         </span><span class="sxs-lookup"><span data-stu-id="92424-236">
            <strong>Object</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="92424-237">
            <strong>Array</strong>
         </span><span class="sxs-lookup"><span data-stu-id="92424-237">
            <strong>Array</strong>
         </span></span></td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="92424-238">
            <strong>Undefined<strong>
         </span><span class="sxs-lookup"><span data-stu-id="92424-238">
            <strong>Undefined<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="92424-239">Undefined</span><span class="sxs-lookup"><span data-stu-id="92424-239">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="92424-240">Undefined</span><span class="sxs-lookup"><span data-stu-id="92424-240">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="92424-241">Undefined</span><span class="sxs-lookup"><span data-stu-id="92424-241">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="92424-242">Undefined</span><span class="sxs-lookup"><span data-stu-id="92424-242">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="92424-243">Undefined</span><span class="sxs-lookup"><span data-stu-id="92424-243">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="92424-244">Undefined</span><span class="sxs-lookup"><span data-stu-id="92424-244">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="92424-245">Undefined</span><span class="sxs-lookup"><span data-stu-id="92424-245">Undefined</span></span> </td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="92424-246">
            <strong>Null<strong>
         </span><span class="sxs-lookup"><span data-stu-id="92424-246">
            <strong>Null<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="92424-247">Undefined</span><span class="sxs-lookup"><span data-stu-id="92424-247">Undefined</span></span> </td>
         <td valign="top"><span data-ttu-id="92424-248">
            <strong>OK</strong>
         </span><span class="sxs-lookup"><span data-stu-id="92424-248">
            <strong>OK</strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="92424-249">Undefined</span><span class="sxs-lookup"><span data-stu-id="92424-249">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="92424-250">Undefined</span><span class="sxs-lookup"><span data-stu-id="92424-250">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="92424-251">Undefined</span><span class="sxs-lookup"><span data-stu-id="92424-251">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="92424-252">Undefined</span><span class="sxs-lookup"><span data-stu-id="92424-252">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="92424-253">Undefined</span><span class="sxs-lookup"><span data-stu-id="92424-253">Undefined</span></span> </td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="92424-254">
            <strong>Boolean<strong>
         </span><span class="sxs-lookup"><span data-stu-id="92424-254">
            <strong>Boolean<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="92424-255">Undefined</span><span class="sxs-lookup"><span data-stu-id="92424-255">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="92424-256">Undefined</span><span class="sxs-lookup"><span data-stu-id="92424-256">Undefined</span></span> </td>
         <td valign="top"><span data-ttu-id="92424-257">
            <strong>OK</strong>
         </span><span class="sxs-lookup"><span data-stu-id="92424-257">
            <strong>OK</strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="92424-258">Undefined</span><span class="sxs-lookup"><span data-stu-id="92424-258">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="92424-259">Undefined</span><span class="sxs-lookup"><span data-stu-id="92424-259">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="92424-260">Undefined</span><span class="sxs-lookup"><span data-stu-id="92424-260">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="92424-261">Undefined</span><span class="sxs-lookup"><span data-stu-id="92424-261">Undefined</span></span> </td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="92424-262">
            <strong>Number<strong>
         </span><span class="sxs-lookup"><span data-stu-id="92424-262">
            <strong>Number<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="92424-263">Undefined</span><span class="sxs-lookup"><span data-stu-id="92424-263">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="92424-264">Undefined</span><span class="sxs-lookup"><span data-stu-id="92424-264">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="92424-265">Undefined</span><span class="sxs-lookup"><span data-stu-id="92424-265">Undefined</span></span> </td>
         <td valign="top"><span data-ttu-id="92424-266">
            <strong>OK</strong>
         </span><span class="sxs-lookup"><span data-stu-id="92424-266">
            <strong>OK</strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="92424-267">Undefined</span><span class="sxs-lookup"><span data-stu-id="92424-267">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="92424-268">Undefined</span><span class="sxs-lookup"><span data-stu-id="92424-268">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="92424-269">Undefined</span><span class="sxs-lookup"><span data-stu-id="92424-269">Undefined</span></span> </td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="92424-270">
            <strong>String<strong>
         </span><span class="sxs-lookup"><span data-stu-id="92424-270">
            <strong>String<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="92424-271">Undefined</span><span class="sxs-lookup"><span data-stu-id="92424-271">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="92424-272">Undefined</span><span class="sxs-lookup"><span data-stu-id="92424-272">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="92424-273">Undefined</span><span class="sxs-lookup"><span data-stu-id="92424-273">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="92424-274">Undefined</span><span class="sxs-lookup"><span data-stu-id="92424-274">Undefined</span></span> </td>
         <td valign="top"><span data-ttu-id="92424-275">
            <strong>OK</strong>
         </span><span class="sxs-lookup"><span data-stu-id="92424-275">
            <strong>OK</strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="92424-276">Undefined</span><span class="sxs-lookup"><span data-stu-id="92424-276">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="92424-277">Undefined</span><span class="sxs-lookup"><span data-stu-id="92424-277">Undefined</span></span> </td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="92424-278">
            <strong>Object<strong>
         </span><span class="sxs-lookup"><span data-stu-id="92424-278">
            <strong>Object<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="92424-279">Undefined</span><span class="sxs-lookup"><span data-stu-id="92424-279">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="92424-280">Undefined</span><span class="sxs-lookup"><span data-stu-id="92424-280">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="92424-281">Undefined</span><span class="sxs-lookup"><span data-stu-id="92424-281">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="92424-282">Undefined</span><span class="sxs-lookup"><span data-stu-id="92424-282">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="92424-283">Undefined</span><span class="sxs-lookup"><span data-stu-id="92424-283">Undefined</span></span> </td>
         <td valign="top"><span data-ttu-id="92424-284">
            <strong>OK</strong>
         </span><span class="sxs-lookup"><span data-stu-id="92424-284">
            <strong>OK</strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="92424-285">Undefined</span><span class="sxs-lookup"><span data-stu-id="92424-285">Undefined</span></span> </td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="92424-286">
            <strong>Array<strong>
         </span><span class="sxs-lookup"><span data-stu-id="92424-286">
            <strong>Array<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="92424-287">Undefined</span><span class="sxs-lookup"><span data-stu-id="92424-287">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="92424-288">Undefined</span><span class="sxs-lookup"><span data-stu-id="92424-288">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="92424-289">Undefined</span><span class="sxs-lookup"><span data-stu-id="92424-289">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="92424-290">Undefined</span><span class="sxs-lookup"><span data-stu-id="92424-290">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="92424-291">Undefined</span><span class="sxs-lookup"><span data-stu-id="92424-291">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="92424-292">Undefined</span><span class="sxs-lookup"><span data-stu-id="92424-292">Undefined</span></span> </td>
         <td valign="top"><span data-ttu-id="92424-293">
            <strong>OK</strong>
         </span><span class="sxs-lookup"><span data-stu-id="92424-293">
            <strong>OK</strong>
         </span></span></td>
      </tr>
   </tbody>
</table>

<span data-ttu-id="92424-294">Pour les autres opérateurs de comparaison tels que >, > =, ! =, < et < =, hello règles suivantes s’appliquent :</span><span class="sxs-lookup"><span data-stu-id="92424-294">For other comparison operators such as >, >=, !=, < and <=, hello following rules apply:</span></span>   

* <span data-ttu-id="92424-295">Une comparaison entre des types entraîne le résultat Undefined.</span><span class="sxs-lookup"><span data-stu-id="92424-295">Comparison across types results in Undefined.</span></span>
* <span data-ttu-id="92424-296">Une comparaison entre deux objets ou deux tableaux entraîne le résultat Undefined.</span><span class="sxs-lookup"><span data-stu-id="92424-296">Comparison between two objects or two arrays results in Undefined.</span></span>   

<span data-ttu-id="92424-297">Si le résultat hello d’expression scalaire de hello dans le filtre de hello est non défini, document correspondant de hello n'est pas inclus dans le résultat de hello, étant donné que Undefined ne sont logiquement équivalentes trop « true ».</span><span class="sxs-lookup"><span data-stu-id="92424-297">If hello result of hello scalar expression in hello filter is Undefined, hello corresponding document would not be included in hello result, since Undefined doesn't logically equate too"true".</span></span>

### <a name="between-keyword"></a><span data-ttu-id="92424-298">Mot clé BETWEEN</span><span class="sxs-lookup"><span data-stu-id="92424-298">BETWEEN keyword</span></span>
<span data-ttu-id="92424-299">Vous pouvez également utiliser hello BETWEEN mot clé tooexpress l’interrogation des plages de valeurs, comme dans ANSI SQL.</span><span class="sxs-lookup"><span data-stu-id="92424-299">You can also use hello BETWEEN keyword tooexpress queries against ranges of values like in ANSI SQL.</span></span> <span data-ttu-id="92424-300">Vous pouvez utiliser BETWEEN sur des chaînes ou des nombres.</span><span class="sxs-lookup"><span data-stu-id="92424-300">BETWEEN can be used against strings or numbers.</span></span>

<span data-ttu-id="92424-301">Par exemple, cette requête renvoie tous les documents de famille dans quels hello niveau du premier enfant est compris entre 1-5 (tous deux inclus).</span><span class="sxs-lookup"><span data-stu-id="92424-301">For example, this query returns all family documents in which hello first child's grade is between 1-5 (both inclusive).</span></span> 

    SELECT *
    FROM Families.children[0] c
    WHERE c.grade BETWEEN 1 AND 5

<span data-ttu-id="92424-302">Contrairement à dans ANSI-SQL, vous pouvez également utiliser hello BETWEEN clause dans la clause FROM de hello comme Bonjour l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="92424-302">Unlike in ANSI-SQL, you can also use hello BETWEEN clause in hello FROM clause like in hello following example.</span></span>

    SELECT (c.grade BETWEEN 0 AND 10)
    FROM Families.children[0] c

<span data-ttu-id="92424-303">Pour les temps d’exécution de requête plus rapides, n’oubliez pas de toocreate une stratégie d’indexation qui utilise un type d’index de plage par rapport à toutes les propriétés/chemins d’accès numériques qui sont filtrés dans la clause BETWEEN hello.</span><span class="sxs-lookup"><span data-stu-id="92424-303">For faster query execution times, remember toocreate an indexing policy that uses a range index type against any numeric properties/paths that are filtered in hello BETWEEN clause.</span></span> 

<span data-ttu-id="92424-304">Hello de principale différence entre l’utilisation de BETWEEN dans ANSI SQL et les API DocumentDB est que vous pouvez exprimer des requêtes de plage par rapport aux propriétés de types mixtes : par exemple, avoir « niveau » est un nombre (5) dans des documents et les chaînes dans d’autres (« grade4 »).</span><span class="sxs-lookup"><span data-stu-id="92424-304">hello main difference between using BETWEEN in DocumentDB API and ANSI SQL is that you can express range queries against properties of mixed types – for example, you might have "grade" be a number (5) in some documents and strings in others ("grade4").</span></span> <span data-ttu-id="92424-305">Dans ce cas, comme dans JavaScript, une comparaison entre deux résultats de différents types de « non définie » et hello document sera ignorée.</span><span class="sxs-lookup"><span data-stu-id="92424-305">In these cases, like in JavaScript, a comparison between two different types results in "undefined", and hello document will be skipped.</span></span>

### <a name="logical-and-or-and-not-operators"></a><span data-ttu-id="92424-306">Opérateurs logiques (AND, OR et NOT)</span><span class="sxs-lookup"><span data-stu-id="92424-306">Logical (AND, OR and NOT) operators</span></span>
<span data-ttu-id="92424-307">Les opérateurs logiques interviennent sur des valeurs booléennes.</span><span class="sxs-lookup"><span data-stu-id="92424-307">Logical operators operate on Boolean values.</span></span> <span data-ttu-id="92424-308">tables de vérité logiques Hello pour ces opérateurs sont affichés dans hello les tableaux suivants.</span><span class="sxs-lookup"><span data-stu-id="92424-308">hello logical truth tables for these operators are shown in hello following tables.</span></span>

| <span data-ttu-id="92424-309">OU</span><span class="sxs-lookup"><span data-stu-id="92424-309">OR</span></span> | <span data-ttu-id="92424-310">True</span><span class="sxs-lookup"><span data-stu-id="92424-310">True</span></span> | <span data-ttu-id="92424-311">False</span><span class="sxs-lookup"><span data-stu-id="92424-311">False</span></span> | <span data-ttu-id="92424-312">Undefined</span><span class="sxs-lookup"><span data-stu-id="92424-312">Undefined</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="92424-313">True</span><span class="sxs-lookup"><span data-stu-id="92424-313">True</span></span> |<span data-ttu-id="92424-314">True</span><span class="sxs-lookup"><span data-stu-id="92424-314">True</span></span> |<span data-ttu-id="92424-315">True</span><span class="sxs-lookup"><span data-stu-id="92424-315">True</span></span> |<span data-ttu-id="92424-316">True</span><span class="sxs-lookup"><span data-stu-id="92424-316">True</span></span> |
| <span data-ttu-id="92424-317">False</span><span class="sxs-lookup"><span data-stu-id="92424-317">False</span></span> |<span data-ttu-id="92424-318">True</span><span class="sxs-lookup"><span data-stu-id="92424-318">True</span></span> |<span data-ttu-id="92424-319">False</span><span class="sxs-lookup"><span data-stu-id="92424-319">False</span></span> |<span data-ttu-id="92424-320">Undefined</span><span class="sxs-lookup"><span data-stu-id="92424-320">Undefined</span></span> |
| <span data-ttu-id="92424-321">Undefined</span><span class="sxs-lookup"><span data-stu-id="92424-321">Undefined</span></span> |<span data-ttu-id="92424-322">True</span><span class="sxs-lookup"><span data-stu-id="92424-322">True</span></span> |<span data-ttu-id="92424-323">Undefined</span><span class="sxs-lookup"><span data-stu-id="92424-323">Undefined</span></span> |<span data-ttu-id="92424-324">Undefined</span><span class="sxs-lookup"><span data-stu-id="92424-324">Undefined</span></span> |

| <span data-ttu-id="92424-325">AND</span><span class="sxs-lookup"><span data-stu-id="92424-325">AND</span></span> | <span data-ttu-id="92424-326">True</span><span class="sxs-lookup"><span data-stu-id="92424-326">True</span></span> | <span data-ttu-id="92424-327">False</span><span class="sxs-lookup"><span data-stu-id="92424-327">False</span></span> | <span data-ttu-id="92424-328">Undefined</span><span class="sxs-lookup"><span data-stu-id="92424-328">Undefined</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="92424-329">True</span><span class="sxs-lookup"><span data-stu-id="92424-329">True</span></span> |<span data-ttu-id="92424-330">True</span><span class="sxs-lookup"><span data-stu-id="92424-330">True</span></span> |<span data-ttu-id="92424-331">False</span><span class="sxs-lookup"><span data-stu-id="92424-331">False</span></span> |<span data-ttu-id="92424-332">Undefined</span><span class="sxs-lookup"><span data-stu-id="92424-332">Undefined</span></span> |
| <span data-ttu-id="92424-333">False</span><span class="sxs-lookup"><span data-stu-id="92424-333">False</span></span> |<span data-ttu-id="92424-334">False</span><span class="sxs-lookup"><span data-stu-id="92424-334">False</span></span> |<span data-ttu-id="92424-335">False</span><span class="sxs-lookup"><span data-stu-id="92424-335">False</span></span> |<span data-ttu-id="92424-336">False</span><span class="sxs-lookup"><span data-stu-id="92424-336">False</span></span> |
| <span data-ttu-id="92424-337">Undefined</span><span class="sxs-lookup"><span data-stu-id="92424-337">Undefined</span></span> |<span data-ttu-id="92424-338">Undefined</span><span class="sxs-lookup"><span data-stu-id="92424-338">Undefined</span></span> |<span data-ttu-id="92424-339">False</span><span class="sxs-lookup"><span data-stu-id="92424-339">False</span></span> |<span data-ttu-id="92424-340">Undefined</span><span class="sxs-lookup"><span data-stu-id="92424-340">Undefined</span></span> |

| <span data-ttu-id="92424-341">NOT</span><span class="sxs-lookup"><span data-stu-id="92424-341">NOT</span></span> |  |
| --- | --- |
| <span data-ttu-id="92424-342">True</span><span class="sxs-lookup"><span data-stu-id="92424-342">True</span></span> |<span data-ttu-id="92424-343">False</span><span class="sxs-lookup"><span data-stu-id="92424-343">False</span></span> |
| <span data-ttu-id="92424-344">False</span><span class="sxs-lookup"><span data-stu-id="92424-344">False</span></span> |<span data-ttu-id="92424-345">True</span><span class="sxs-lookup"><span data-stu-id="92424-345">True</span></span> |
| <span data-ttu-id="92424-346">Undefined</span><span class="sxs-lookup"><span data-stu-id="92424-346">Undefined</span></span> |<span data-ttu-id="92424-347">Undefined</span><span class="sxs-lookup"><span data-stu-id="92424-347">Undefined</span></span> |

### <a name="in-keyword"></a><span data-ttu-id="92424-348">Mot clé IN</span><span class="sxs-lookup"><span data-stu-id="92424-348">IN keyword</span></span>
<span data-ttu-id="92424-349">mot clé IN de Hello peut être utilisé toocheck si une valeur spécifiée correspond à la valeur dans une liste.</span><span class="sxs-lookup"><span data-stu-id="92424-349">hello IN keyword can be used toocheck whether a specified value matches any value in a list.</span></span> <span data-ttu-id="92424-350">Par exemple, cette requête retourne tous les documents de famille où id de hello est un des « WakefieldFamily » ou « AndersenFamily ».</span><span class="sxs-lookup"><span data-stu-id="92424-350">For example, this query returns all family documents where hello id is one of "WakefieldFamily" or "AndersenFamily".</span></span> 

    SELECT *
    FROM Families 
    WHERE Families.id IN ('AndersenFamily', 'WakefieldFamily')

<span data-ttu-id="92424-351">Cet exemple retourne tous les documents où l’état de hello est hello spécifié les valeurs.</span><span class="sxs-lookup"><span data-stu-id="92424-351">This example returns all documents where hello state is any of hello specified values.</span></span>

    SELECT *
    FROM Families 
    WHERE Families.address.state IN ("NY", "WA", "CA", "PA", "OH", "OR", "MI", "WI", "MN", "FL")

### <a name="ternary--and-coalesce--operators"></a><span data-ttu-id="92424-352">Opérateurs Ternary (?) et Coalesce (??)</span><span class="sxs-lookup"><span data-stu-id="92424-352">Ternary (?) and Coalesce (??) operators</span></span>
<span data-ttu-id="92424-353">les opérateurs ternaire et Coalesce Hello peuvent être toobuild utilisées les expressions conditionnelles, toopopular similaire programmation des langages tels que c# et JavaScript.</span><span class="sxs-lookup"><span data-stu-id="92424-353">hello Ternary and Coalesce operators can be used toobuild conditional expressions, similar toopopular programming languages like C# and JavaScript.</span></span> 

<span data-ttu-id="92424-354">opérateur ternaire ( ?) de Hello peut être très utile lors de la construction nouvelles propriétés JSON sur hello vol.</span><span class="sxs-lookup"><span data-stu-id="92424-354">hello Ternary (?) operator can be very handy when constructing new JSON properties on hello fly.</span></span> <span data-ttu-id="92424-355">Par exemple, maintenant vous pouvez écrire les niveaux de classe de requêtes tooclassify hello dans un format lisible humain comme débutant/intermédiaire/Avancé comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="92424-355">For example, now you can write queries tooclassify hello class levels into a human readable form like Beginner/Intermediate/Advanced as shown below.</span></span>

     SELECT (c.grade < 5)? "elementary": "other" AS gradeLevel 
     FROM Families.children[0] c

<span data-ttu-id="92424-356">Vous pouvez également imbriquer hello appels toohello (opérateur), comme dans la requête hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="92424-356">You can also nest hello calls toohello operator like in hello query below.</span></span>

    SELECT (c.grade < 5)? "elementary": ((c.grade < 9)? "junior": "high")  AS gradeLevel 
    FROM Families.children[0] c

<span data-ttu-id="92424-357">Comme avec d’autres opérateurs de requête, si hello propriétés référencées dans une expression conditionnelle hello sont manquantes dans n’importe quel document, ou si les types hello comparés sont différents, puis ces documents sont exclus dans les résultats de la requête hello.</span><span class="sxs-lookup"><span data-stu-id="92424-357">As with other query operators, if hello referenced properties in hello conditional expression are missing in any document, or if hello types being compared are different, then those documents are excluded in hello query results.</span></span>

<span data-ttu-id="92424-358">Hello Coalesce ( ?) opérateur peut être utilisé tooefficiently cocher présence hello d’une propriété (aussi appelé)</span><span class="sxs-lookup"><span data-stu-id="92424-358">hello Coalesce (??) operator can be used tooefficiently check for hello presence of a property (a.k.a.</span></span> <span data-ttu-id="92424-359">vérifier si elle est définie) dans un document.</span><span class="sxs-lookup"><span data-stu-id="92424-359">is defined) in a document.</span></span> <span data-ttu-id="92424-360">Cela est utile lors de l'interrogation de données semi-structurées ou de types différents.</span><span class="sxs-lookup"><span data-stu-id="92424-360">This is useful when querying against semi-structured or data of mixed types.</span></span> <span data-ttu-id="92424-361">Par exemple, cette requête renvoie hello « lastName » le cas échéant, ou hello « nom » si elle n’est pas présent.</span><span class="sxs-lookup"><span data-stu-id="92424-361">For example, this query returns hello "lastName" if present, or hello "surname" if it isn't present.</span></span>

    SELECT f.lastName ?? f.surname AS familyName
    FROM Families f

### <span data-ttu-id="92424-362"><a id="EscapingReservedKeywords"></a>Accesseur de propriété entre guillemets</span><span class="sxs-lookup"><span data-stu-id="92424-362"><a id="EscapingReservedKeywords"></a>Quoted property accessor</span></span>
<span data-ttu-id="92424-363">Vous pouvez également accéder aux propriétés à l’aide d’opérateur de propriété entre guillemets hello `[]`.</span><span class="sxs-lookup"><span data-stu-id="92424-363">You can also access properties using hello quoted property operator `[]`.</span></span> <span data-ttu-id="92424-364">Par exemple, `SELECT c.grade` and `SELECT c["grade"]` sont équivalentes.</span><span class="sxs-lookup"><span data-stu-id="92424-364">For example, `SELECT c.grade` and `SELECT c["grade"]` are equivalent.</span></span> <span data-ttu-id="92424-365">Cette syntaxe est utile lorsque vous devez tooescape une propriété qui contient des espaces, des caractères spéciaux, ou qui se passe hello tooshare même nom qu’un mot clé SQL ou un mot réservé.</span><span class="sxs-lookup"><span data-stu-id="92424-365">This syntax is useful when you need tooescape a property that contains spaces, special characters, or happens tooshare hello same name as a SQL keyword or reserved word.</span></span>

    SELECT f["lastName"]
    FROM Families f
    WHERE f["id"] = "AndersenFamily"


## <span data-ttu-id="92424-366"><a id="SelectClause"></a>Clause SELECT</span><span class="sxs-lookup"><span data-stu-id="92424-366"><a id="SelectClause"></a>SELECT clause</span></span>
<span data-ttu-id="92424-367">clause SELECT de Hello (**`SELECT <select_list>`**) est obligatoire et spécifie que les valeurs sont récupérées à partir de la requête de hello, comme dans ANSI-SQL.</span><span class="sxs-lookup"><span data-stu-id="92424-367">hello SELECT clause (**`SELECT <select_list>`**) is mandatory and specifies what values are retrieved from hello query, just like in ANSI-SQL.</span></span> <span data-ttu-id="92424-368">sous-ensemble Hello été filtré sur les documents source hello sont passés sur la phase de projection hello, où hello spécifié les valeurs JSON sont récupérés et un nouvel objet JSON est construit, pour chaque entrée passée sur lui.</span><span class="sxs-lookup"><span data-stu-id="92424-368">hello subset that's been filtered on top of hello source documents are passed onto hello projection phase, where hello specified JSON values are retrieved and a new JSON object is constructed, for each input passed onto it.</span></span> 

<span data-ttu-id="92424-369">Hello, l’exemple suivant montre une requête SELECT classique.</span><span class="sxs-lookup"><span data-stu-id="92424-369">hello following example shows a typical SELECT query.</span></span> 

<span data-ttu-id="92424-370">**Requête**</span><span class="sxs-lookup"><span data-stu-id="92424-370">**Query**</span></span>

    SELECT f.address
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="92424-371">**Résultats**</span><span class="sxs-lookup"><span data-stu-id="92424-371">**Results**</span></span>

    [{
      "address": {
        "state": "WA", 
        "county": "King", 
        "city": "seattle"
      }
    }]


### <a name="nested-properties"></a><span data-ttu-id="92424-372">Propriétés imbriquées</span><span class="sxs-lookup"><span data-stu-id="92424-372">Nested properties</span></span>
<span data-ttu-id="92424-373">Bonjour l’exemple suivant, nous allons projection deux propriétés imbriquées `f.address.state` et `f.address.city`.</span><span class="sxs-lookup"><span data-stu-id="92424-373">In hello following example, we are projecting two nested properties `f.address.state` and `f.address.city`.</span></span>

<span data-ttu-id="92424-374">**Requête**</span><span class="sxs-lookup"><span data-stu-id="92424-374">**Query**</span></span>

    SELECT f.address.state, f.address.city
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="92424-375">**Résultats**</span><span class="sxs-lookup"><span data-stu-id="92424-375">**Results**</span></span>

    [{
      "state": "WA", 
      "city": "seattle"
    }]


<span data-ttu-id="92424-376">Projection prend également en charge les expressions de JSON comme indiqué dans hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="92424-376">Projection also supports JSON expressions as shown in hello following example:</span></span>

<span data-ttu-id="92424-377">**Requête**</span><span class="sxs-lookup"><span data-stu-id="92424-377">**Query**</span></span>

    SELECT { "state": f.address.state, "city": f.address.city, "name": f.id }
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="92424-378">**Résultats**</span><span class="sxs-lookup"><span data-stu-id="92424-378">**Results**</span></span>

    [{
      "$1": {
        "state": "WA", 
        "city": "seattle", 
        "name": "AndersenFamily"
      }
    }]


<span data-ttu-id="92424-379">Examinons le rôle hello `$1` ici.</span><span class="sxs-lookup"><span data-stu-id="92424-379">Let's look at hello role of `$1` here.</span></span> <span data-ttu-id="92424-380">Hello `SELECT` clause doit toocreate un objet JSON et car aucune clé n’est fournie, nous utilisons des noms de variables d’argument implicite en commençant par `$1`.</span><span class="sxs-lookup"><span data-stu-id="92424-380">hello `SELECT` clause needs toocreate a JSON object and since no key is provided, we use implicit argument variable names starting with `$1`.</span></span> <span data-ttu-id="92424-381">Par exemple, cette requête renvoie 2 variables d’argument implicites, étiquetées `$1` and `$2`.</span><span class="sxs-lookup"><span data-stu-id="92424-381">For example, this query returns two implicit argument variables, labeled `$1` and `$2`.</span></span>

<span data-ttu-id="92424-382">**Requête**</span><span class="sxs-lookup"><span data-stu-id="92424-382">**Query**</span></span>

    SELECT { "state": f.address.state, "city": f.address.city }, 
           { "name": f.id }
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="92424-383">**Résultats**</span><span class="sxs-lookup"><span data-stu-id="92424-383">**Results**</span></span>

    [{
      "$1": {
        "state": "WA", 
        "city": "seattle"
      }, 
      "$2": {
        "name": "AndersenFamily"
      }
    }]


### <a name="aliasing"></a><span data-ttu-id="92424-384">Alias</span><span class="sxs-lookup"><span data-stu-id="92424-384">Aliasing</span></span>
<span data-ttu-id="92424-385">Maintenant nous allons étendre exemple hello ci-dessus rencontreraient explicite de valeurs.</span><span class="sxs-lookup"><span data-stu-id="92424-385">Now let's extend hello example above with explicit aliasing of values.</span></span> <span data-ttu-id="92424-386">EN l’état hello mot clé utilisé pour l’utilisation d’alias.</span><span class="sxs-lookup"><span data-stu-id="92424-386">AS is hello keyword used for aliasing.</span></span> <span data-ttu-id="92424-387">Il est facultatif, comme indiqué lors de la projection hello deuxième valeur en tant que `NameInfo`.</span><span class="sxs-lookup"><span data-stu-id="92424-387">It's optional as shown while projecting hello second value as `NameInfo`.</span></span> 

<span data-ttu-id="92424-388">Au cas où une requête présente deux propriétés hello même nom, alias doit être utilisé toorename une ou les deux hello propriétés afin qu’ils sont de lever l’ambiguïté dans hello projetée résultat.</span><span class="sxs-lookup"><span data-stu-id="92424-388">In case a query has two properties with hello same name, aliasing must be used toorename one or both of hello properties so that they are disambiguated in hello projected result.</span></span>

<span data-ttu-id="92424-389">**Requête**</span><span class="sxs-lookup"><span data-stu-id="92424-389">**Query**</span></span>

    SELECT 
           { "state": f.address.state, "city": f.address.city } AS AddressInfo, 
           { "name": f.id } NameInfo
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="92424-390">**Résultats**</span><span class="sxs-lookup"><span data-stu-id="92424-390">**Results**</span></span>

    [{
      "AddressInfo": {
        "state": "WA", 
        "city": "seattle"
      }, 
      "NameInfo": {
        "name": "AndersenFamily"
      }
    }]


### <a name="scalar-expressions"></a><span data-ttu-id="92424-391">Expressions scalaires</span><span class="sxs-lookup"><span data-stu-id="92424-391">Scalar expressions</span></span>
<span data-ttu-id="92424-392">En outre tooproperty fait référence à, la clause SELECT de hello prend également en charge les expressions scalaires tels que des constantes, des expressions arithmétiques, des expressions logiques, etc.. Par exemple, voici une requête « Hello World » simple.</span><span class="sxs-lookup"><span data-stu-id="92424-392">In addition tooproperty references, hello SELECT clause also supports scalar expressions like constants, arithmetic expressions, logical expressions, etc. For example, here's a simple "Hello World" query.</span></span>

<span data-ttu-id="92424-393">**Requête**</span><span class="sxs-lookup"><span data-stu-id="92424-393">**Query**</span></span>

    SELECT "Hello World"

<span data-ttu-id="92424-394">**Résultats**</span><span class="sxs-lookup"><span data-stu-id="92424-394">**Results**</span></span>

    [{
      "$1": "Hello World"
    }]


<span data-ttu-id="92424-395">Voici un exemple plus complexe utilisant une expression scalaire.</span><span class="sxs-lookup"><span data-stu-id="92424-395">Here's a more complex example that uses a scalar expression.</span></span>

<span data-ttu-id="92424-396">**Requête**</span><span class="sxs-lookup"><span data-stu-id="92424-396">**Query**</span></span>

    SELECT ((2 + 11 % 7)-2)/3    

<span data-ttu-id="92424-397">**Résultats**</span><span class="sxs-lookup"><span data-stu-id="92424-397">**Results**</span></span>

    [{
      "$1": 1.33333
    }]


<span data-ttu-id="92424-398">Dans l’exemple suivant de hello, résultat hello d’expression scalaire de hello est une valeur booléenne.</span><span class="sxs-lookup"><span data-stu-id="92424-398">In hello following example, hello result of hello scalar expression is a Boolean.</span></span>

<span data-ttu-id="92424-399">**Requête**</span><span class="sxs-lookup"><span data-stu-id="92424-399">**Query**</span></span>

    SELECT f.address.city = f.address.state AS AreFromSameCityState
    FROM Families f    

<span data-ttu-id="92424-400">**Résultats**</span><span class="sxs-lookup"><span data-stu-id="92424-400">**Results**</span></span>

    [
      {
        "AreFromSameCityState": false
      }, 
      {
        "AreFromSameCityState": true
      }
    ]


### <a name="object-and-array-creation"></a><span data-ttu-id="92424-401">Création d'objet et de tableau</span><span class="sxs-lookup"><span data-stu-id="92424-401">Object and array creation</span></span>
<span data-ttu-id="92424-402">Une autre fonctionnalité clé du langage SQL de l’API DocumentDB est la possibilité de créer un tableau ou un objet.</span><span class="sxs-lookup"><span data-stu-id="92424-402">Another key feature of DocumentDB API SQL is array/object creation.</span></span> <span data-ttu-id="92424-403">Dans l’exemple précédent de hello, notez que nous avons créé un nouvel objet JSON.</span><span class="sxs-lookup"><span data-stu-id="92424-403">In hello previous example, note that we created a new JSON object.</span></span> <span data-ttu-id="92424-404">De même, un peut également construire des tableaux comme hello exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="92424-404">Similarly, one can also construct arrays as shown in hello following examples:</span></span>

<span data-ttu-id="92424-405">**Requête**</span><span class="sxs-lookup"><span data-stu-id="92424-405">**Query**</span></span>

    SELECT [f.address.city, f.address.state] AS CityState 
    FROM Families f    

<span data-ttu-id="92424-406">**Résultats**</span><span class="sxs-lookup"><span data-stu-id="92424-406">**Results**</span></span>  

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

### <span data-ttu-id="92424-407"><a id="ValueKeyword"></a>Mot clé VALUE</span><span class="sxs-lookup"><span data-stu-id="92424-407"><a id="ValueKeyword"></a>VALUE keyword</span></span>
<span data-ttu-id="92424-408">Hello **valeur** (mot clé) fournit une valeur de façon tooreturn JSON.</span><span class="sxs-lookup"><span data-stu-id="92424-408">hello **VALUE** keyword provides a way tooreturn JSON value.</span></span> <span data-ttu-id="92424-409">Par exemple, les requêtes hello ci-dessous retourne hello scalaire `"Hello World"` au lieu de `{$1: "Hello World"}`.</span><span class="sxs-lookup"><span data-stu-id="92424-409">For example, hello query shown below returns hello scalar `"Hello World"` instead of `{$1: "Hello World"}`.</span></span>

<span data-ttu-id="92424-410">**Requête**</span><span class="sxs-lookup"><span data-stu-id="92424-410">**Query**</span></span>

    SELECT VALUE "Hello World"

<span data-ttu-id="92424-411">**Résultats**</span><span class="sxs-lookup"><span data-stu-id="92424-411">**Results**</span></span>

    [
      "Hello World"
    ]


<span data-ttu-id="92424-412">Hello requête suivante renvoie valeur JSON de hello sans hello `"address"` étiquette dans les résultats de hello.</span><span class="sxs-lookup"><span data-stu-id="92424-412">hello following query returns hello JSON value without hello `"address"` label in hello results.</span></span>

<span data-ttu-id="92424-413">**Requête**</span><span class="sxs-lookup"><span data-stu-id="92424-413">**Query**</span></span>

    SELECT VALUE f.address
    FROM Families f    

<span data-ttu-id="92424-414">**Résultats**</span><span class="sxs-lookup"><span data-stu-id="92424-414">**Results**</span></span>  

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

<span data-ttu-id="92424-415">Hello exemple suivant étend cette tooshow comment tooreturn JSON des valeurs de primitives (hello inférieurs d’arborescence JSON hello).</span><span class="sxs-lookup"><span data-stu-id="92424-415">hello following example extends this tooshow how tooreturn JSON primitive values (hello leaf level of hello JSON tree).</span></span> 

<span data-ttu-id="92424-416">**Requête**</span><span class="sxs-lookup"><span data-stu-id="92424-416">**Query**</span></span>

    SELECT VALUE f.address.state
    FROM Families f    

<span data-ttu-id="92424-417">**Résultats**</span><span class="sxs-lookup"><span data-stu-id="92424-417">**Results**</span></span>

    [
      "WA",
      "NY"
    ]


### <a name="-operator"></a><span data-ttu-id="92424-418">Opérateur *</span><span class="sxs-lookup"><span data-stu-id="92424-418">* Operator</span></span>
<span data-ttu-id="92424-419">Bonjour opérateur spécial (*) est document hello tooproject pris en charge-est.</span><span class="sxs-lookup"><span data-stu-id="92424-419">hello special operator (*) is supported tooproject hello document as-is.</span></span> <span data-ttu-id="92424-420">Lorsqu’il est utilisé, il doit être hello projetée uniquement le champ.</span><span class="sxs-lookup"><span data-stu-id="92424-420">When used, it must be hello only projected field.</span></span> <span data-ttu-id="92424-421">Si une requête comme `SELECT * FROM Families f` est valide, `SELECT VALUE * FROM Families f ` et `SELECT *, f.id FROM Families f ` ne le sont pas.</span><span class="sxs-lookup"><span data-stu-id="92424-421">While a query like `SELECT * FROM Families f` is valid, `SELECT VALUE * FROM Families f ` and  `SELECT *, f.id FROM Families f ` are not valid.</span></span>

<span data-ttu-id="92424-422">**Requête**</span><span class="sxs-lookup"><span data-stu-id="92424-422">**Query**</span></span>

    SELECT * 
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="92424-423">**Résultats**</span><span class="sxs-lookup"><span data-stu-id="92424-423">**Results**</span></span>

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

### <span data-ttu-id="92424-424"><a id="TopKeyword"></a>Opérateur TOP</span><span class="sxs-lookup"><span data-stu-id="92424-424"><a id="TopKeyword"></a>TOP Operator</span></span>
<span data-ttu-id="92424-425">mot clé TOP de Hello peut être utilisé numéro de hello toolimit de valeurs à partir d’une requête.</span><span class="sxs-lookup"><span data-stu-id="92424-425">hello TOP keyword can be used toolimit hello number of values from a query.</span></span> <span data-ttu-id="92424-426">Lorsque TOP est utilisé conjointement avec la clause ORDER BY hello, jeu de résultats hello est limitée toohello N premiers de valeurs ordonnés ; Sinon, elle retourne hello N premiers résultats dans un ordre non défini.</span><span class="sxs-lookup"><span data-stu-id="92424-426">When TOP is used in conjunction with hello ORDER BY clause, hello result set is limited toohello first N number of ordered values; otherwise, it returns hello first N number of results in an undefined order.</span></span> <span data-ttu-id="92424-427">Comme meilleure pratique, dans une instruction SELECT, toujours utiliser une clause ORDER BY avec la clause TOP de hello.</span><span class="sxs-lookup"><span data-stu-id="92424-427">As a best practice, in a SELECT statement, always use an ORDER BY clause with hello TOP clause.</span></span> <span data-ttu-id="92424-428">Il s’agit de hello seule façon toopredictably indiquer quelles lignes sont affectées par TOP.</span><span class="sxs-lookup"><span data-stu-id="92424-428">This is hello only way toopredictably indicate which rows are affected by TOP.</span></span> 

<span data-ttu-id="92424-429">**Requête**</span><span class="sxs-lookup"><span data-stu-id="92424-429">**Query**</span></span>

    SELECT TOP 1 * 
    FROM Families f 

<span data-ttu-id="92424-430">**Résultats**</span><span class="sxs-lookup"><span data-stu-id="92424-430">**Results**</span></span>

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

<span data-ttu-id="92424-431">L’opérateur TOP peut être utilisé avec une valeur constante (comme indiqué ci-dessus) ou avec une valeur variable à l'aide de requêtes paramétrables.</span><span class="sxs-lookup"><span data-stu-id="92424-431">TOP can be used with a constant value (as shown above) or with a variable value using parameterized queries.</span></span> <span data-ttu-id="92424-432">Pour plus d'informations, consultez les requêtes paramétrables ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="92424-432">For more details, please see parameterized queries below.</span></span>

### <span data-ttu-id="92424-433"><a id="Aggregates"></a>Fonctions d’agrégation</span><span class="sxs-lookup"><span data-stu-id="92424-433"><a id="Aggregates"></a>Aggregate Functions</span></span>
<span data-ttu-id="92424-434">Vous pouvez également effectuer des agrégations Bonjour `SELECT` clause.</span><span class="sxs-lookup"><span data-stu-id="92424-434">You can also perform aggregations in hello `SELECT` clause.</span></span> <span data-ttu-id="92424-435">Les fonctions d’agrégation effectuent un calcul sur un ensemble de valeurs et renvoient une valeur unique.</span><span class="sxs-lookup"><span data-stu-id="92424-435">Aggregate functions perform a calculation on a set of values and return a single value.</span></span> <span data-ttu-id="92424-436">Par exemple, hello requête suivante retourne hello nombre de documents familles au sein de la collection de hello.</span><span class="sxs-lookup"><span data-stu-id="92424-436">For example, hello following query returns hello count of family documents within hello collection.</span></span>

<span data-ttu-id="92424-437">**Requête**</span><span class="sxs-lookup"><span data-stu-id="92424-437">**Query**</span></span>

    SELECT COUNT(1) 
    FROM Families f 

<span data-ttu-id="92424-438">**Résultats**</span><span class="sxs-lookup"><span data-stu-id="92424-438">**Results**</span></span>

    [{
        "$1": 2
    }]

<span data-ttu-id="92424-439">Vous pouvez également retourner la valeur scalaire hello hello d’agrégation à l’aide de hello `VALUE` (mot clé).</span><span class="sxs-lookup"><span data-stu-id="92424-439">You can also return hello scalar value of hello aggregate by using hello `VALUE` keyword.</span></span> <span data-ttu-id="92424-440">Par exemple, hello requête suivante retourne hello nombre de valeurs comme un nombre unique :</span><span class="sxs-lookup"><span data-stu-id="92424-440">For example, hello following query returns hello count of values as a single number:</span></span>

<span data-ttu-id="92424-441">**Requête**</span><span class="sxs-lookup"><span data-stu-id="92424-441">**Query**</span></span>

    SELECT VALUE COUNT(1) 
    FROM Families f 

<span data-ttu-id="92424-442">**Résultats**</span><span class="sxs-lookup"><span data-stu-id="92424-442">**Results**</span></span>

    [ 2 ]

<span data-ttu-id="92424-443">Vous pouvez également effectuer des agrégations en appliquant des filtres simultanément.</span><span class="sxs-lookup"><span data-stu-id="92424-443">You can also perform aggregates in combination with filters.</span></span> <span data-ttu-id="92424-444">Par exemple, hello requête suivante retourne hello nombre de documents avec l’adresse de hello dans hello état de Washington.</span><span class="sxs-lookup"><span data-stu-id="92424-444">For example, hello following query returns hello count of documents with hello address in hello state of Washington.</span></span>

<span data-ttu-id="92424-445">**Requête**</span><span class="sxs-lookup"><span data-stu-id="92424-445">**Query**</span></span>

    SELECT VALUE COUNT(1) 
    FROM Families f
    WHERE f.address.state = "WA" 

<span data-ttu-id="92424-446">**Résultats**</span><span class="sxs-lookup"><span data-stu-id="92424-446">**Results**</span></span>

    [ 1 ]

<span data-ttu-id="92424-447">Hello tableau suivant répertorie hello des fonctions d’agrégation prises en charge dans l’API DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="92424-447">hello following table shows hello list of supported aggregate functions in DocumentDB API.</span></span> <span data-ttu-id="92424-448">`SUM` et `AVG` s’appliquent à des valeurs numériques, tandis que `COUNT`, `MIN`, et `MAX` peuvent être effectuées sur des nombres, des chaînes, des booléens et des valeurs Null.</span><span class="sxs-lookup"><span data-stu-id="92424-448">`SUM` and `AVG` are performed over numeric values, whereas `COUNT`, `MIN`, and `MAX` can be performed over numbers, strings, Booleans, and nulls.</span></span> 

| <span data-ttu-id="92424-449">Usage</span><span class="sxs-lookup"><span data-stu-id="92424-449">Usage</span></span> | <span data-ttu-id="92424-450">Description</span><span class="sxs-lookup"><span data-stu-id="92424-450">Description</span></span> |
|-------|-------------|
| <span data-ttu-id="92424-451">COUNT</span><span class="sxs-lookup"><span data-stu-id="92424-451">COUNT</span></span> | <span data-ttu-id="92424-452">Retourne hello nombre d’éléments dans l’expression de hello.</span><span class="sxs-lookup"><span data-stu-id="92424-452">Returns hello number of items in hello expression.</span></span> |
| <span data-ttu-id="92424-453">SUM</span><span class="sxs-lookup"><span data-stu-id="92424-453">SUM</span></span>   | <span data-ttu-id="92424-454">Retourne hello somme de toutes les valeurs hello dans l’expression de hello.</span><span class="sxs-lookup"><span data-stu-id="92424-454">Returns hello sum of all hello values in hello expression.</span></span> |
| <span data-ttu-id="92424-455">MIN</span><span class="sxs-lookup"><span data-stu-id="92424-455">MIN</span></span>   | <span data-ttu-id="92424-456">Retourne hello valeur minimale dans l’expression de hello.</span><span class="sxs-lookup"><span data-stu-id="92424-456">Returns hello minimum value in hello expression.</span></span> |
| <span data-ttu-id="92424-457">MAX</span><span class="sxs-lookup"><span data-stu-id="92424-457">MAX</span></span>   | <span data-ttu-id="92424-458">Retourne hello valeur maximale dans l’expression de hello.</span><span class="sxs-lookup"><span data-stu-id="92424-458">Returns hello maximum value in hello expression.</span></span> |
| <span data-ttu-id="92424-459">MOY</span><span class="sxs-lookup"><span data-stu-id="92424-459">AVG</span></span>   | <span data-ttu-id="92424-460">Retourne hello moyenne des valeurs hello dans l’expression de hello.</span><span class="sxs-lookup"><span data-stu-id="92424-460">Returns hello average of hello values in hello expression.</span></span> |

<span data-ttu-id="92424-461">Agrégats peuvent également être effectuées sur les résultats de hello d’une itération du tableau.</span><span class="sxs-lookup"><span data-stu-id="92424-461">Aggregates can also be performed over hello results of an array iteration.</span></span> <span data-ttu-id="92424-462">Pour en savoir plus, consultez la section relative à [l’itération de tableaux dans les requêtes](#Iteration).</span><span class="sxs-lookup"><span data-stu-id="92424-462">For more information, see [Array Iteration in Queries](#Iteration).</span></span>

> [!NOTE]
> <span data-ttu-id="92424-463">Lors de l’aide hello Explorer de requête du portail Azure, notez que les requêtes d’agrégation des résultats hello partiellement agrégées sur une page de requête.</span><span class="sxs-lookup"><span data-stu-id="92424-463">When using hello Azure portal's Query Explorer, note that aggregation queries may return hello partially aggregated results over a query page.</span></span> <span data-ttu-id="92424-464">Hello kits de développement logiciel génère une seule valeur cumulative dans toutes les pages.</span><span class="sxs-lookup"><span data-stu-id="92424-464">hello SDKs produces a single cumulative value across all pages.</span></span> 
> 
> <span data-ttu-id="92424-465">Ordre tooperform requêtes d’agrégation à l’aide de code, vous avez besoin de kit de développement .NET 1.12.0, Kit de développement logiciel .NET Core 1.1.0 ou kit de développement logiciel Java 1.9.5 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="92424-465">In order tooperform aggregation queries using code, you need .NET SDK 1.12.0, .NET Core SDK 1.1.0, or Java SDK 1.9.5 or above.</span></span>    
>

## <span data-ttu-id="92424-466"><a id="OrderByClause"></a>Clause ORDER BY</span><span class="sxs-lookup"><span data-stu-id="92424-466"><a id="OrderByClause"></a>ORDER BY clause</span></span>
<span data-ttu-id="92424-467">Comme dans ANSI-SQL, vous pouvez désormais inclure une clause Order By facultative lors d’une interrogation.</span><span class="sxs-lookup"><span data-stu-id="92424-467">Like in ANSI-SQL, you can include an optional Order By clause while querying.</span></span> <span data-ttu-id="92424-468">clause de Hello peut inclure une commande facultative de hello toospecify argument ASC/DESC dans lequel les résultats doivent être récupérées.</span><span class="sxs-lookup"><span data-stu-id="92424-468">hello clause can include an optional ASC/DESC argument toospecify hello order in which results must be retrieved.</span></span>

<span data-ttu-id="92424-469">Par exemple, voici une requête qui Récupère des familles dans l’ordre du nom de la ville de résidence hello.</span><span class="sxs-lookup"><span data-stu-id="92424-469">For example, here's a query that retrieves families in order of hello resident city's name.</span></span>

<span data-ttu-id="92424-470">**Requête**</span><span class="sxs-lookup"><span data-stu-id="92424-470">**Query**</span></span>

    SELECT f.id, f.address.city
    FROM Families f 
    ORDER BY f.address.city

<span data-ttu-id="92424-471">**Résultats**</span><span class="sxs-lookup"><span data-stu-id="92424-471">**Results**</span></span>

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

<span data-ttu-id="92424-472">Et Voici une requête qui Récupère des familles dans l’ordre de date de création, qui est stockée comme un nombre représentant hello date, c'est-à-dire, temps écoulé depuis le 1er janvier 1970, en secondes.</span><span class="sxs-lookup"><span data-stu-id="92424-472">And here's a query that retrieves families in order of creation date, which is stored as a number representing hello epoch time, i.e, elapsed time since Jan 1, 1970 in seconds.</span></span>

<span data-ttu-id="92424-473">**Requête**</span><span class="sxs-lookup"><span data-stu-id="92424-473">**Query**</span></span>

    SELECT f.id, f.creationDate
    FROM Families f 
    ORDER BY f.creationDate DESC

<span data-ttu-id="92424-474">**Résultats**</span><span class="sxs-lookup"><span data-stu-id="92424-474">**Results**</span></span>

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

## <span data-ttu-id="92424-475"><a id="Advanced"></a>Concepts avancés de base de données et requêtes SQL</span><span class="sxs-lookup"><span data-stu-id="92424-475"><a id="Advanced"></a>Advanced database concepts and SQL queries</span></span>

### <span data-ttu-id="92424-476"><a id="Iteration"></a>Itération</span><span class="sxs-lookup"><span data-stu-id="92424-476"><a id="Iteration"></a>Iteration</span></span>
<span data-ttu-id="92424-477">Une nouvelle construction a été ajoutée via hello **IN** mot clé dans la prise en charge de tooprovide DocumentDB API SQL pour itérer sur des tableaux JSON.</span><span class="sxs-lookup"><span data-stu-id="92424-477">A new construct was added via hello **IN** keyword in DocumentDB API SQL tooprovide support for iterating over JSON arrays.</span></span> <span data-ttu-id="92424-478">source de Hello FROM prend en charge pour l’itération.</span><span class="sxs-lookup"><span data-stu-id="92424-478">hello FROM source provides support for iteration.</span></span> <span data-ttu-id="92424-479">Commençons par hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="92424-479">Let's start with hello following example:</span></span>

<span data-ttu-id="92424-480">**Requête**</span><span class="sxs-lookup"><span data-stu-id="92424-480">**Query**</span></span>

    SELECT * 
    FROM Families.children

<span data-ttu-id="92424-481">**Résultats**</span><span class="sxs-lookup"><span data-stu-id="92424-481">**Results**</span></span>  

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

<span data-ttu-id="92424-482">Maintenant nous allons examiner une autre requête qui effectue une itération sur les enfants dans la collection de hello.</span><span class="sxs-lookup"><span data-stu-id="92424-482">Now let's look at another query that performs iteration over children in hello collection.</span></span> <span data-ttu-id="92424-483">Notez la différence de hello dans le tableau de sortie hello.</span><span class="sxs-lookup"><span data-stu-id="92424-483">Note hello difference in hello output array.</span></span> <span data-ttu-id="92424-484">Cet exemple fractionne `children` et aplatit les résultats hello dans un seul tableau.</span><span class="sxs-lookup"><span data-stu-id="92424-484">This example splits `children` and flattens hello results into a single array.</span></span>  

<span data-ttu-id="92424-485">**Requête**</span><span class="sxs-lookup"><span data-stu-id="92424-485">**Query**</span></span>

    SELECT * 
    FROM c IN Families.children

<span data-ttu-id="92424-486">**Résultats**</span><span class="sxs-lookup"><span data-stu-id="92424-486">**Results**</span></span>  

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

<span data-ttu-id="92424-487">Cela peut être plus toofilter utilisé sur chaque écriture du tableau hello comme indiqué dans hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="92424-487">This can be further used toofilter on each individual entry of hello array as shown in hello following example:</span></span>

<span data-ttu-id="92424-488">**Requête**</span><span class="sxs-lookup"><span data-stu-id="92424-488">**Query**</span></span>

    SELECT c.givenName
    FROM c IN Families.children
    WHERE c.grade = 8

<span data-ttu-id="92424-489">**Résultats**</span><span class="sxs-lookup"><span data-stu-id="92424-489">**Results**</span></span>  

    [{
      "givenName": "Lisa"
    }]

<span data-ttu-id="92424-490">Vous pouvez également effectuer l’agrégation sur le résultat de hello d’itération du tableau.</span><span class="sxs-lookup"><span data-stu-id="92424-490">You can also perform aggregation over hello result of array iteration.</span></span> <span data-ttu-id="92424-491">Par exemple, hello requête suivante compte hello nombre d’enfants parmi toutes les familles.</span><span class="sxs-lookup"><span data-stu-id="92424-491">For example, hello following query counts hello number of children among all families.</span></span>

<span data-ttu-id="92424-492">**Requête**</span><span class="sxs-lookup"><span data-stu-id="92424-492">**Query**</span></span>

    SELECT COUNT(child) 
    FROM child IN Families.children

<span data-ttu-id="92424-493">**Résultats**</span><span class="sxs-lookup"><span data-stu-id="92424-493">**Results**</span></span>  

    [
      { 
        "$1": 3
      }
    ]

### <span data-ttu-id="92424-494"><a id="Joins"></a>Jointures</span><span class="sxs-lookup"><span data-stu-id="92424-494"><a id="Joins"></a>Joins</span></span>
<span data-ttu-id="92424-495">Dans une base de données relationnelle, toojoin besoin de hello dans des tables est important.</span><span class="sxs-lookup"><span data-stu-id="92424-495">In a relational database, hello need toojoin across tables is important.</span></span> <span data-ttu-id="92424-496">Il s’agit de schémas de logique toodesigning facultatif normalisée hello.</span><span class="sxs-lookup"><span data-stu-id="92424-496">It's hello logical corollary toodesigning normalized schemas.</span></span> <span data-ttu-id="92424-497">Toothis contraires, API DocumentDB porte sur le modèle de données dénormalisées hello de documents de schéma.</span><span class="sxs-lookup"><span data-stu-id="92424-497">Contrary toothis, DocumentDB API deals with hello denormalized data model of schema-free documents.</span></span> <span data-ttu-id="92424-498">Revient à hello logique une « jointure réflexive ».</span><span class="sxs-lookup"><span data-stu-id="92424-498">This is hello logical equivalent of a "self-join".</span></span>

<span data-ttu-id="92424-499">syntaxe Hello hello langage prend en charge est la jointure de jointure que < from_source2 > < que from_source1 est étendu >... JOIN <from_sourceN>.</span><span class="sxs-lookup"><span data-stu-id="92424-499">hello syntax that hello language supports is <from_source1> JOIN <from_source2> JOIN ... JOIN <from_sourceN>.</span></span> <span data-ttu-id="92424-500">D’une façon générale, ceci renvoie un ensemble de **N**-tuples (un tuple avec **N** valeurs).</span><span class="sxs-lookup"><span data-stu-id="92424-500">Overall, this returns a set of **N**-tuples (tuple with **N** values).</span></span> <span data-ttu-id="92424-501">Les valeurs de chaque tuple sont produites par l'itération de tous les alias de la collection sur leurs ensembles respectifs.</span><span class="sxs-lookup"><span data-stu-id="92424-501">Each tuple has values produced by iterating all collection aliases over their respective sets.</span></span> <span data-ttu-id="92424-502">En d’autres termes, il s’agit d’un produit cartésien des jeux hello participant à la jointure de hello.</span><span class="sxs-lookup"><span data-stu-id="92424-502">In other words, this is a full cross product of hello sets participating in hello join.</span></span>

<span data-ttu-id="92424-503">Hello exemples suivants montrent comment la clause de jointure hello fonctionne.</span><span class="sxs-lookup"><span data-stu-id="92424-503">hello following examples show how hello JOIN clause works.</span></span> <span data-ttu-id="92424-504">Dans l’exemple suivant de hello, résultat de hello est vide, car hello produit croisé de chaque document à partir de la source et un jeu vide est vide.</span><span class="sxs-lookup"><span data-stu-id="92424-504">In hello following example, hello result is empty since hello cross product of each document from source and an empty set is empty.</span></span>

<span data-ttu-id="92424-505">**Requête**</span><span class="sxs-lookup"><span data-stu-id="92424-505">**Query**</span></span>

    SELECT f.id
    FROM Families f
    JOIN f.NonExistent

<span data-ttu-id="92424-506">**Résultats**</span><span class="sxs-lookup"><span data-stu-id="92424-506">**Results**</span></span>  

    [{
    }]


<span data-ttu-id="92424-507">Dans l’exemple suivant de hello, jointure de hello est entre la racine du document hello et hello `children` subroot.</span><span class="sxs-lookup"><span data-stu-id="92424-507">In hello following example, hello join is between hello document root and hello `children` subroot.</span></span> <span data-ttu-id="92424-508">Il s'agit d'un produit croisé entre deux objets JSON.</span><span class="sxs-lookup"><span data-stu-id="92424-508">It's a cross product between two JSON objects.</span></span> <span data-ttu-id="92424-509">faits Hello qu’enfants est un tableau n’est pas efficace hello jointure étant donné que nous avons affaire à une racine unique qui est le tableau des enfants hello.</span><span class="sxs-lookup"><span data-stu-id="92424-509">hello fact that children is an array is not effective in hello JOIN since we are dealing with a single root that is hello children array.</span></span> <span data-ttu-id="92424-510">Par conséquent, les résultats hello contient uniquement deux résultats, étant donné que le produit croisé de chaque document par un tableau hello hello produit exactement un seul document.</span><span class="sxs-lookup"><span data-stu-id="92424-510">Hence hello result contains only two results, since hello cross product of each document with hello array yields exactly only one document.</span></span>

<span data-ttu-id="92424-511">**Requête**</span><span class="sxs-lookup"><span data-stu-id="92424-511">**Query**</span></span>

    SELECT f.id
    FROM Families f
    JOIN f.children

<span data-ttu-id="92424-512">**Résultats**</span><span class="sxs-lookup"><span data-stu-id="92424-512">**Results**</span></span>

    [
      {
        "id": "AndersenFamily"
      }, 
      {
        "id": "WakefieldFamily"
      }
    ]


<span data-ttu-id="92424-513">Bonjour à l’exemple suivant montre une jointure plus classique :</span><span class="sxs-lookup"><span data-stu-id="92424-513">hello following example shows a more conventional join:</span></span>

<span data-ttu-id="92424-514">**Requête**</span><span class="sxs-lookup"><span data-stu-id="92424-514">**Query**</span></span>

    SELECT f.id
    FROM Families f
    JOIN c IN f.children 

<span data-ttu-id="92424-515">**Résultats**</span><span class="sxs-lookup"><span data-stu-id="92424-515">**Results**</span></span>

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



<span data-ttu-id="92424-516">Hello première toonote est que hello `from_source` Hello **joindre** clause est un itérateur.</span><span class="sxs-lookup"><span data-stu-id="92424-516">hello first thing toonote is that hello `from_source` of hello **JOIN** clause is an iterator.</span></span> <span data-ttu-id="92424-517">Par conséquent, les flux hello dans ce cas est comme suit :</span><span class="sxs-lookup"><span data-stu-id="92424-517">So, hello flow in this case is as follows:</span></span>  

* <span data-ttu-id="92424-518">Développez chaque élément enfant **c** dans le tableau de hello.</span><span class="sxs-lookup"><span data-stu-id="92424-518">Expand each child element **c** in hello array.</span></span>
* <span data-ttu-id="92424-519">Appliquer un produit croisé par la racine du document de hello hello **f** avec chaque élément enfant **c** qui a été aplatie dans la première étape de hello.</span><span class="sxs-lookup"><span data-stu-id="92424-519">Apply a cross product with hello root of hello document **f** with each child element **c** that was flattened in hello first step.</span></span>
* <span data-ttu-id="92424-520">Enfin, projet objet racine de hello **f** uniquement de la propriété name.</span><span class="sxs-lookup"><span data-stu-id="92424-520">Finally, project hello root object **f** name property alone.</span></span> 

<span data-ttu-id="92424-521">document de première Hello (`AndersenFamily`) contient uniquement un élément enfant, afin de l’ensemble de résultats hello contient uniquement un seul objet toothis document correspondant.</span><span class="sxs-lookup"><span data-stu-id="92424-521">hello first document (`AndersenFamily`) contains only one child element, so hello result set contains only a single object corresponding toothis document.</span></span> <span data-ttu-id="92424-522">document de deuxième Hello (`WakefieldFamily`) contient deux enfants.</span><span class="sxs-lookup"><span data-stu-id="92424-522">hello second document (`WakefieldFamily`) contains two children.</span></span> <span data-ttu-id="92424-523">Par conséquent, hello produit croisé génère un objet distinct pour chaque enfant, ce qui entraîne deux objets, un pour chaque document de toothis enfant correspondant.</span><span class="sxs-lookup"><span data-stu-id="92424-523">So, hello cross product produces a separate object for each child, thereby resulting in two objects, one for each child corresponding toothis document.</span></span> <span data-ttu-id="92424-524">racine Hello champs dans les deux de ces documents sont identiques, hello simplement comme prévu dans un produit croisé.</span><span class="sxs-lookup"><span data-stu-id="92424-524">hello root fields in both these documents are hello same, just as you would expect in a cross product.</span></span>

<span data-ttu-id="92424-525">Hello réel utilitaire Hello jointure est tooform les tuples à partir du produit croisé hello dans une forme qui est sinon tooproject difficile.</span><span class="sxs-lookup"><span data-stu-id="92424-525">hello real utility of hello JOIN is tooform tuples from hello cross-product in a shape that's otherwise difficult tooproject.</span></span> <span data-ttu-id="92424-526">En outre, comme nous le voir dans l’exemple hello ci-dessous, vous pouvez filtrer sur combinaison hello d’un tuple hello de permet de cet utilisateur a choisi une condition satisfaite par les tuples hello globale.</span><span class="sxs-lookup"><span data-stu-id="92424-526">Furthermore, as we see in hello example below, you could filter on hello combination of a tuple that lets' hello user chose a condition satisfied by hello tuples overall.</span></span>

<span data-ttu-id="92424-527">**Requête**</span><span class="sxs-lookup"><span data-stu-id="92424-527">**Query**</span></span>

    SELECT 
        f.id AS familyName,
        c.givenName AS childGivenName,
        c.firstName AS childFirstName,
        p.givenName AS petName 
    FROM Families f 
    JOIN c IN f.children 
    JOIN p IN c.pets

<span data-ttu-id="92424-528">**Résultats**</span><span class="sxs-lookup"><span data-stu-id="92424-528">**Results**</span></span>

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



<span data-ttu-id="92424-529">Cet exemple est un prolongement naturel de hello précédent exemple et effectue une jointure en double.</span><span class="sxs-lookup"><span data-stu-id="92424-529">This example is a natural extension of hello preceding example, and performs a double join.</span></span> <span data-ttu-id="92424-530">Par conséquent, hello produit croisé peut être considéré comme hello suivant pseudo-code :</span><span class="sxs-lookup"><span data-stu-id="92424-530">So, hello cross product can be viewed as hello following pseudo-code:</span></span>

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

<span data-ttu-id="92424-531">`AndersenFamily` a un enfant qui a un animal.</span><span class="sxs-lookup"><span data-stu-id="92424-531">`AndersenFamily` has one child who has one pet.</span></span> <span data-ttu-id="92424-532">Par conséquent, hello produit croisé génère une ligne (1\*1\*1) à partir de cette famille.</span><span class="sxs-lookup"><span data-stu-id="92424-532">So, hello cross product yields one row (1\*1\*1) from this family.</span></span> <span data-ttu-id="92424-533">Cependant, WakefieldFamily a deux enfants, mais seul l'un d'eux, « Jesse », a des animaux.</span><span class="sxs-lookup"><span data-stu-id="92424-533">WakefieldFamily however has two children, but only one child "Jesse" has pets.</span></span> <span data-ttu-id="92424-534">Or, Jesse a deux animaux.</span><span class="sxs-lookup"><span data-stu-id="92424-534">Jesse has two pets though.</span></span> <span data-ttu-id="92424-535">Par conséquent, hello produit croisé donne 1\*1\*2 = 2 lignes à partir de cette famille.</span><span class="sxs-lookup"><span data-stu-id="92424-535">Hence hello cross product yields 1\*1\*2 = 2 rows from this family.</span></span>

<span data-ttu-id="92424-536">Dans l’exemple suivant de hello, il existe un filtre supplémentaire sur `pet`.</span><span class="sxs-lookup"><span data-stu-id="92424-536">In hello next example, there is an additional filter on `pet`.</span></span> <span data-ttu-id="92424-537">Cela exclut tous les tuples hello où hello pet nom n’est pas « Clichés instantané ».</span><span class="sxs-lookup"><span data-stu-id="92424-537">This excludes all hello tuples where hello pet name is not "Shadow".</span></span> <span data-ttu-id="92424-538">Notez que nous nous toobuild en mesure des tuples à partir des tableaux, le filtre sur un des éléments hello du tuple de hello et n’importe quelle combinaison d’éléments de hello du projet.</span><span class="sxs-lookup"><span data-stu-id="92424-538">Notice that we are able toobuild tuples from arrays, filter on any of hello elements of hello tuple, and project any combination of hello elements.</span></span> 

<span data-ttu-id="92424-539">**Requête**</span><span class="sxs-lookup"><span data-stu-id="92424-539">**Query**</span></span>

    SELECT 
        f.id AS familyName,
        c.givenName AS childGivenName,
        c.firstName AS childFirstName,
        p.givenName AS petName 
    FROM Families f 
    JOIN c IN f.children 
    JOIN p IN c.pets
    WHERE p.givenName = "Shadow"

<span data-ttu-id="92424-540">**Résultats**</span><span class="sxs-lookup"><span data-stu-id="92424-540">**Results**</span></span>

    [
      {
       "familyName": "WakefieldFamily", 
       "childGivenName": "Jesse", 
       "petName": "Shadow"
      }
    ]


## <span data-ttu-id="92424-541"><a id="JavaScriptIntegration"></a>Intégration JavaScript</span><span class="sxs-lookup"><span data-stu-id="92424-541"><a id="JavaScriptIntegration"></a>JavaScript integration</span></span>
<span data-ttu-id="92424-542">Azure Cosmos DB fournit un modèle de programmation pour l’exécution de la logique d’application basée sur JavaScript directement sur des collections de hello en termes de procédures stockées et déclencheurs.</span><span class="sxs-lookup"><span data-stu-id="92424-542">Azure Cosmos DB provides a programming model for executing JavaScript based application logic directly on hello collections in terms of stored procedures and triggers.</span></span> <span data-ttu-id="92424-543">Ceci permet pour les deux :</span><span class="sxs-lookup"><span data-stu-id="92424-543">This allows for both:</span></span>

* <span data-ttu-id="92424-544">Opérations CRUD transactionnelles de capacité toodo hautes performances et des requêtes sur des documents dans une collection en vertu de l’intégration en profondeur hello du runtime JavaScript directement dans le moteur de base de données hello.</span><span class="sxs-lookup"><span data-stu-id="92424-544">Ability toodo high-performance transactional CRUD operations and queries against documents in a collection by virtue of hello deep integration of JavaScript runtime directly within hello database engine.</span></span> 
* <span data-ttu-id="92424-545">Une modélisation naturelle du flux de contrôle, de l'étendue des variables, de l'attribution et de l'intégration des primitives de gestion d'exception avec des transactions de base de données.</span><span class="sxs-lookup"><span data-stu-id="92424-545">A natural modeling of control flow, variable scoping, and assignment and integration of exception handling primitives with database transactions.</span></span> <span data-ttu-id="92424-546">Pour plus d’informations sur la prise en charge de la base de données Azure Cosmos pour l’intégration de JavaScript, veuillez consultez la documentation de programmabilité du côté serveur du JavaScript toohello.</span><span class="sxs-lookup"><span data-stu-id="92424-546">For more details about Azure Cosmos DB support for JavaScript integration, please refer toohello JavaScript server-side programmability documentation.</span></span>

### <span data-ttu-id="92424-547"><a id="UserDefinedFunctions"></a>Fonctions définies par l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="92424-547"><a id="UserDefinedFunctions"></a>User-Defined Functions (UDFs)</span></span>
<span data-ttu-id="92424-548">Avec les types hello déjà définis dans cet article, DocumentDB API SQL fournit la prise en charge pour le fonctions défini utilisateur (UDF).</span><span class="sxs-lookup"><span data-stu-id="92424-548">Along with hello types already defined in this article, DocumentDB API SQL provides support for User Defined Functions (UDF).</span></span> <span data-ttu-id="92424-549">En particulier, les fonctions UDF scalaires sont prises en charge dans lesquelles les développeurs de hello peuvent passer de zéro ou plusieurs arguments et retourner un résultat unique argument précédent.</span><span class="sxs-lookup"><span data-stu-id="92424-549">In particular, scalar UDFs are supported where hello developers can pass in zero or many arguments and return a single argument result back.</span></span> <span data-ttu-id="92424-550">La légalité des valeurs JSON de chacun de ces arguments est vérifiée.</span><span class="sxs-lookup"><span data-stu-id="92424-550">Each of these arguments is checked for being legal JSON values.</span></span>  

<span data-ttu-id="92424-551">Hello syntaxe SQL d’API DocumentDB est étendue toosupport logique d’application personnalisée à l’aide de ces fonctions définies par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="92424-551">hello DocumentDB API SQL syntax is extended toosupport custom application logic using these User-Defined Functions.</span></span> <span data-ttu-id="92424-552">Ces dernières peuvent être enregistrées avec l’API DocumentDB, puis référencées dans le cadre d’une requête SQL.</span><span class="sxs-lookup"><span data-stu-id="92424-552">UDFs can be registered with DocumentDB API and then be referenced as part of a SQL query.</span></span> <span data-ttu-id="92424-553">En fait, hello UDF sont ordinateurs conçu toobe appelé par les requêtes.</span><span class="sxs-lookup"><span data-stu-id="92424-553">In fact, hello UDFs are exquisitely designed toobe invoked by queries.</span></span> <span data-ttu-id="92424-554">Comme un choix toothis facultatif, UDF n’ont accès toohello contexte objet qui hello autres JavaScript ont des types (procédures stockées et déclencheurs).</span><span class="sxs-lookup"><span data-stu-id="92424-554">As a corollary toothis choice, UDFs do not have access toohello context object which hello other JavaScript types (stored procedures and triggers) have.</span></span> <span data-ttu-id="92424-555">Comme les requêtes s'exécutent en lecture seule, elles peuvent démarrer sur des réplicas principaux ou secondaires.</span><span class="sxs-lookup"><span data-stu-id="92424-555">Since queries execute as read-only, they can run either on primary or on secondary replicas.</span></span> <span data-ttu-id="92424-556">Par conséquent, UDF sont conçu toorun sur les réplicas secondaires, contrairement à d’autres types de JavaScript.</span><span class="sxs-lookup"><span data-stu-id="92424-556">Therefore, UDFs are designed toorun on secondary replicas unlike other JavaScript types.</span></span>

<span data-ttu-id="92424-557">Voici un exemple de la façon dont un fichier UDF peut être enregistré à hello Cosmos DB de base de données, en particulier dans une collection de documents.</span><span class="sxs-lookup"><span data-stu-id="92424-557">Below is an example of how a UDF can be registered at hello Cosmos DB database, specifically under a document collection.</span></span>

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

<span data-ttu-id="92424-558">Hello exemple précédent crée une fonction dont le nom est `REGEX_MATCH`.</span><span class="sxs-lookup"><span data-stu-id="92424-558">hello preceding example creates a UDF whose name is `REGEX_MATCH`.</span></span> <span data-ttu-id="92424-559">Il accepte deux valeurs de chaîne JSON `input` et `pattern` et vérifie si hello premières correspondances hello modèle défini dans hello ensuite à l’aide de fonction de String.Match () de JavaScript.</span><span class="sxs-lookup"><span data-stu-id="92424-559">It accepts two JSON string values `input` and `pattern` and checks if hello first matches hello pattern specified in hello second using JavaScript's string.match() function.</span></span>

<span data-ttu-id="92424-560">Nous pouvons maintenant utiliser cette fonction définie par l'utilisateur dans une requête, dans une projection.</span><span class="sxs-lookup"><span data-stu-id="92424-560">We can now use this UDF in a query in a projection.</span></span> <span data-ttu-id="92424-561">UDF doivent être qualifiés par préfixe qui respecte la casse de hello « udf. »</span><span class="sxs-lookup"><span data-stu-id="92424-561">UDFs must be qualified with hello case-sensitive prefix "udf."</span></span> <span data-ttu-id="92424-562">quand elles sont appelées à partir de requêtes.</span><span class="sxs-lookup"><span data-stu-id="92424-562">when called from within queries.</span></span> 

> [!NOTE]
> <span data-ttu-id="92424-563">Préalable too3/17/2015 Cosmos DB pris en charge les appels UDF sans hello « udf. »</span><span class="sxs-lookup"><span data-stu-id="92424-563">Prior too3/17/2015, Cosmos DB supported UDF calls without hello "udf."</span></span> <span data-ttu-id="92424-564">comme SELECT REGEX_MATCH().</span><span class="sxs-lookup"><span data-stu-id="92424-564">prefix like SELECT REGEX_MATCH().</span></span> <span data-ttu-id="92424-565">Ce modèle d'appel est maintenant déconseillé.</span><span class="sxs-lookup"><span data-stu-id="92424-565">This calling pattern has been deprecated.</span></span>  
> 
> 

<span data-ttu-id="92424-566">**Requête**</span><span class="sxs-lookup"><span data-stu-id="92424-566">**Query**</span></span>

    SELECT udf.REGEX_MATCH(Families.address.city, ".*eattle")
    FROM Families

<span data-ttu-id="92424-567">**Résultats**</span><span class="sxs-lookup"><span data-stu-id="92424-567">**Results**</span></span>

    [
      {
        "$1": true
      }, 
      {
        "$1": false
      }
    ]

<span data-ttu-id="92424-568">Hello UDF peut également servir à l’intérieur d’un filtre comme illustré dans l’exemple hello ci-dessous, également qualifié avec hello « udf. »</span><span class="sxs-lookup"><span data-stu-id="92424-568">hello UDF can also be used inside a filter as shown in hello example below, also qualified with hello "udf."</span></span> <span data-ttu-id="92424-569">Préfixe :</span><span class="sxs-lookup"><span data-stu-id="92424-569">prefix:</span></span>

<span data-ttu-id="92424-570">**Requête**</span><span class="sxs-lookup"><span data-stu-id="92424-570">**Query**</span></span>

    SELECT Families.id, Families.address.city
    FROM Families
    WHERE udf.REGEX_MATCH(Families.address.city, ".*eattle")

<span data-ttu-id="92424-571">**Résultats**</span><span class="sxs-lookup"><span data-stu-id="92424-571">**Results**</span></span>

    [{
        "id": "AndersenFamily",
        "city": "Seattle"
    }]


<span data-ttu-id="92424-572">Fondamentalement, les fonctions définies par l'utilisateur sont des expressions scalaires valides et peuvent être utilisées dans des projections et des filtres.</span><span class="sxs-lookup"><span data-stu-id="92424-572">In essence, UDFs are valid scalar expressions and can be used in both projections and filters.</span></span> 

<span data-ttu-id="92424-573">tooexpand sous tension hello des UDF, examinons un autre exemple avec une logique conditionnelle :</span><span class="sxs-lookup"><span data-stu-id="92424-573">tooexpand on hello power of UDFs, let's look at another example with conditional logic:</span></span>

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


<span data-ttu-id="92424-574">Voici un exemple qu’exercices hello UDF.</span><span class="sxs-lookup"><span data-stu-id="92424-574">Below is an example that exercises hello UDF.</span></span>

<span data-ttu-id="92424-575">**Requête**</span><span class="sxs-lookup"><span data-stu-id="92424-575">**Query**</span></span>

    SELECT f.address.city, udf.SEALEVEL(f.address.city) AS seaLevel
    FROM Families f    

<span data-ttu-id="92424-576">**Résultats**</span><span class="sxs-lookup"><span data-stu-id="92424-576">**Results**</span></span>

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


<span data-ttu-id="92424-577">Comme hello Galerie d’exemples précédents, UDF intégrant power hello du langage JavaScript hello DocumentDB API SQL tooprovide une riche interface programmable toodo procédurale, conditionnelle une logique complexe à l’aide de hello d’intégrés JavaScript runtime fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="92424-577">As hello preceding examples showcase, UDFs integrate hello power of JavaScript language with hello DocumentDB API SQL tooprovide a rich programmable interface toodo complex procedural, conditional logic with hello help of inbuilt JavaScript runtime capabilities.</span></span>

<span data-ttu-id="92424-578">DocumentDB API SQL fournit des arguments de hello toohello UDF pour chaque document dans la source de hello stade hello actuel (clause WHERE ou sélectionnez) de traitement hello UDF.</span><span class="sxs-lookup"><span data-stu-id="92424-578">DocumentDB API SQL provides hello arguments toohello UDFs for each document in hello source at hello current stage (WHERE clause or SELECT clause) of processing hello UDF.</span></span> <span data-ttu-id="92424-579">résultat Hello est incorporé dans hello pipeline de l’exécution globale en toute transparence.</span><span class="sxs-lookup"><span data-stu-id="92424-579">hello result is incorporated in hello overall execution pipeline seamlessly.</span></span> <span data-ttu-id="92424-580">Si les propriétés hello tooby référencé hello UDF paramètres ne sont pas disponibles dans hello valeur JSON, hello paramètre est considéré comme non défini et donc hello appel de fonction est entièrement ignorée.</span><span class="sxs-lookup"><span data-stu-id="92424-580">If hello properties referred tooby hello UDF parameters are not available in hello JSON value, hello parameter is considered as undefined and hence hello UDF invocation is entirely skipped.</span></span> <span data-ttu-id="92424-581">Même si le résultat de hello Hello UDF n’est pas défini, il n’est pas inclus dans le résultat de hello.</span><span class="sxs-lookup"><span data-stu-id="92424-581">Similarly if hello result of hello UDF is undefined, it's not included in hello result.</span></span> 

<span data-ttu-id="92424-582">En résumé, UDF sont une logique métier complexe toodo outils sophistiqués en tant que partie de la requête de hello.</span><span class="sxs-lookup"><span data-stu-id="92424-582">In summary, UDFs are great tools toodo complex business logic as part of hello query.</span></span>

### <a name="operator-evaluation"></a><span data-ttu-id="92424-583">Évaluation d'opérateur</span><span class="sxs-lookup"><span data-stu-id="92424-583">Operator evaluation</span></span>
<span data-ttu-id="92424-584">COSMOS DB, en vertu de hello d’en cours d’une base de données JSON, dessine parallels avec JavaScript, opérateurs et sa sémantique d’évaluation.</span><span class="sxs-lookup"><span data-stu-id="92424-584">Cosmos DB, by hello virtue of being a JSON database, draws parallels with JavaScript operators and its evaluation semantics.</span></span> <span data-ttu-id="92424-585">Alors que Cosmos DB tente de la sémantique JavaScript toopreserve en termes de prise en charge JSON, évaluation d’opération hello dévie dans certains cas.</span><span class="sxs-lookup"><span data-stu-id="92424-585">While Cosmos DB tries toopreserve JavaScript semantics in terms of JSON support, hello operation evaluation deviates in some instances.</span></span>

<span data-ttu-id="92424-586">Dans DocumentDB API SQL, contrairement à dans SQL traditionnel, types hello de valeurs sont souvent inconnus jusqu'à ce que les valeurs de hello sont récupérées à partir de la base de données.</span><span class="sxs-lookup"><span data-stu-id="92424-586">In DocumentDB API SQL, unlike in traditional SQL, hello types of values are often not known until hello values are retrieved from database.</span></span> <span data-ttu-id="92424-587">Dans l’ordre tooefficiently exécuter des requêtes, la plupart des opérateurs de hello ont des exigences de type strict.</span><span class="sxs-lookup"><span data-stu-id="92424-587">In order tooefficiently execute queries, most of hello operators have strict type requirements.</span></span> 

<span data-ttu-id="92424-588">Le langage SQL de l’API DocumentDB n’effectue pas de conversions implicites, contrairement à JavaScript.</span><span class="sxs-lookup"><span data-stu-id="92424-588">DocumentDB API SQL doesn't perform implicit conversions, unlike JavaScript.</span></span> <span data-ttu-id="92424-589">Par exemple, une requête comme `SELECT * FROM Person p WHERE p.Age = 21` correspond à des documents qui contiennent une propriété Age dont la valeur est 21.</span><span class="sxs-lookup"><span data-stu-id="92424-589">For instance, a query like `SELECT * FROM Person p WHERE p.Age = 21` matches documents that contain an Age property whose value is 21.</span></span> <span data-ttu-id="92424-590">Tout autre document dont la propriété Age correspond à la chaîne « 21 » ou à l'une de ses multiples variantes telles que « 021 », « 21.0 », « 0021 », « 00021 », etc. ne sera pas mis en correspondance.</span><span class="sxs-lookup"><span data-stu-id="92424-590">Any other document whose Age property matches string "21", or other possibly infinite variations like "021", "21.0", "0021", "00021", etc. will not be matched.</span></span> <span data-ttu-id="92424-591">Il s’agit en revanche toohello JavaScript où les valeurs de chaîne hello sont implicitement converti toonumbers (basé sur un opérateur, ex : ==).</span><span class="sxs-lookup"><span data-stu-id="92424-591">This is in contrast toohello JavaScript where hello string values are implicitly casted toonumbers (based on operator, ex: ==).</span></span> <span data-ttu-id="92424-592">Ce choix est crucial pour une correspondance d’index efficace dans le langage SQL de l’API DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="92424-592">This choice is crucial for efficient index matching in DocumentDB API SQL.</span></span> 

## <a name="parameterized-sql-queries"></a><span data-ttu-id="92424-593">Requêtes SQL paramétrables</span><span class="sxs-lookup"><span data-stu-id="92424-593">Parameterized SQL queries</span></span>
<span data-ttu-id="92424-594">COSMOS DB prend en charge les requêtes avec paramètres exprimés par hello familier notation @.</span><span class="sxs-lookup"><span data-stu-id="92424-594">Cosmos DB supports queries with parameters expressed with hello familiar @ notation.</span></span> <span data-ttu-id="92424-595">SQL paramétré fournit une gestion et un échappement robustes de l'entrée utilisateur et empêche l'exposition accidentelle des données par l'intermédiaire de l'injection SQL.</span><span class="sxs-lookup"><span data-stu-id="92424-595">Parameterized SQL provides robust handling and escaping of user input, preventing accidental exposure of data through SQL injection.</span></span> 

<span data-ttu-id="92424-596">Par exemple, vous pouvez écrire une requête qui prend le nom et l'état de l'adresse comme paramètres, puis l'exécuter pour différentes valeurs de nom et d'état d'adresse en fonction de l'entrée utilisateur.</span><span class="sxs-lookup"><span data-stu-id="92424-596">For example, you can write a query that takes last name and address state as parameters, and then execute it for various values of last name and address state based on user input.</span></span>

    SELECT * 
    FROM Families f
    WHERE f.lastName = @lastName AND f.address.state = @addressState

<span data-ttu-id="92424-597">Cette demande peut ensuite être envoyée tooCosmos DB en tant qu’une requête paramétrable de JSON, comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="92424-597">This request can then be sent tooCosmos DB as a parameterized JSON query like shown below.</span></span>

    {      
        "query": "SELECT * FROM Families f WHERE f.lastName = @lastName AND f.address.state = @addressState",     
        "parameters": [          
            {"name": "@lastName", "value": "Wakefield"},         
            {"name": "@addressState", "value": "NY"},           
        ] 
    }

<span data-ttu-id="92424-598">Hello argument tooTOP peut être définie à l’aide de requêtes paramétrables, comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="92424-598">hello argument tooTOP can be set using parameterized queries like shown below.</span></span>

    {      
        "query": "SELECT TOP @n * FROM Families",     
        "parameters": [          
            {"name": "@n", "value": 10},         
        ] 
    }

<span data-ttu-id="92424-599">Les valeurs de paramètres peuvent être n'importe quel format JSON valide (chaînes, nombres, valeurs booléennes, null, même des tableaux ou des valeurs JSON imbriquées).</span><span class="sxs-lookup"><span data-stu-id="92424-599">Parameter values can be any valid JSON (strings, numbers, Booleans, null, even arrays or nested JSON).</span></span> <span data-ttu-id="92424-600">De plus, comme Cosmos DB est sans schéma, les paramètres ne sont pas validés par rapport à un type.</span><span class="sxs-lookup"><span data-stu-id="92424-600">Also since Cosmos DB is schema-less, parameters are not validated against any type.</span></span>

## <span data-ttu-id="92424-601"><a id="BuiltinFunctions"></a>Fonctions intégrées</span><span class="sxs-lookup"><span data-stu-id="92424-601"><a id="BuiltinFunctions"></a>Built-in functions</span></span>
<span data-ttu-id="92424-602">Cosmos DB prend également en charge plusieurs fonctions intégrées pour des opérations courantes. Ces fonctions s’utilisent dans les requêtes comme les fonctions définies par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="92424-602">Cosmos DB also supports a number of built-in functions for common operations, that can be used inside queries like user-defined functions (UDFs).</span></span>

| <span data-ttu-id="92424-603">Groupe de fonctions</span><span class="sxs-lookup"><span data-stu-id="92424-603">Function group</span></span>          | <span data-ttu-id="92424-604">Opérations</span><span class="sxs-lookup"><span data-stu-id="92424-604">Operations</span></span>                                                                                                                                          |
|-------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="92424-605">Fonctions mathématiques</span><span class="sxs-lookup"><span data-stu-id="92424-605">Mathematical functions</span></span>  | <span data-ttu-id="92424-606">ABS, CEILING, EXP, FLOOR, LOG, LOG10, POWER, ROUND, SIGN, SQRT, SQUARE, TRUNC, ACOS, ASIN, ATAN, ATN2, COS, COT, DEGREES, PI, RADIANS, SIN et TAN</span><span class="sxs-lookup"><span data-stu-id="92424-606">ABS, CEILING, EXP, FLOOR, LOG, LOG10, POWER, ROUND, SIGN, SQRT, SQUARE, TRUNC, ACOS, ASIN, ATAN, ATN2, COS, COT, DEGREES, PI, RADIANS, SIN, and TAN</span></span> |
| <span data-ttu-id="92424-607">Fonctions de vérification du type</span><span class="sxs-lookup"><span data-stu-id="92424-607">Type checking functions</span></span> | <span data-ttu-id="92424-608">IS_ARRAY, IS_BOOL, IS_NULL, IS_NUMBER, IS_OBJECT, IS_STRING, IS_DEFINED et IS_PRIMITIVE</span><span class="sxs-lookup"><span data-stu-id="92424-608">IS_ARRAY, IS_BOOL, IS_NULL, IS_NUMBER, IS_OBJECT, IS_STRING, IS_DEFINED, and IS_PRIMITIVE</span></span>                                                           |
| <span data-ttu-id="92424-609">Fonctions de chaîne</span><span class="sxs-lookup"><span data-stu-id="92424-609">String functions</span></span>        | <span data-ttu-id="92424-610">CONCAT, CONTAINS, ENDSWITH, INDEX_OF, LEFT, LENGTH, LOWER, LTRIM, REPLACE, REPLICATE, REVERSE, RIGHT, RTRIM, STARTSWITH, SUBSTRING et UPPER</span><span class="sxs-lookup"><span data-stu-id="92424-610">CONCAT, CONTAINS, ENDSWITH, INDEX_OF, LEFT, LENGTH, LOWER, LTRIM, REPLACE, REPLICATE, REVERSE, RIGHT, RTRIM, STARTSWITH, SUBSTRING, and UPPER</span></span>       |
| <span data-ttu-id="92424-611">Fonctions de tableau</span><span class="sxs-lookup"><span data-stu-id="92424-611">Array functions</span></span>         | <span data-ttu-id="92424-612">ARRAY_CONCAT, ARRAY_CONTAINS, ARRAY_LENGTH et ARRAY_SLICE</span><span class="sxs-lookup"><span data-stu-id="92424-612">ARRAY_CONCAT, ARRAY_CONTAINS, ARRAY_LENGTH, and ARRAY_SLICE</span></span>                                                                                         |
| <span data-ttu-id="92424-613">Fonctions spatiales</span><span class="sxs-lookup"><span data-stu-id="92424-613">Spatial functions</span></span>       | <span data-ttu-id="92424-614">ST_DISTANCE, ST_WITHIN, ST_INTERSECTS, ST_ISVALID et ST_ISVALIDDETAILED</span><span class="sxs-lookup"><span data-stu-id="92424-614">ST_DISTANCE, ST_WITHIN, ST_INTERSECTS, ST_ISVALID, and ST_ISVALIDDETAILED</span></span>                                                                           | 

<span data-ttu-id="92424-615">Si vous utilisez actuellement une fonction définie par l’utilisateur (UDF) pour laquelle une fonction intégrée est désormais disponible, vous devez utiliser la fonction intégrée de hello correspondant comme il va toobe les toorun plus rapide et plus efficacement.</span><span class="sxs-lookup"><span data-stu-id="92424-615">If you’re currently using a user-defined function (UDF) for which a built-in function is now available, you should use hello corresponding built-in function as it is going toobe quicker toorun and more efficiently.</span></span> 

### <a name="mathematical-functions"></a><span data-ttu-id="92424-616">Fonctions mathématiques</span><span class="sxs-lookup"><span data-stu-id="92424-616">Mathematical functions</span></span>
<span data-ttu-id="92424-617">fonctions mathématiques Hello chaque effectuent un calcul, en fonction des valeurs d’entrée qui sont fournies en tant qu’arguments et retournent une valeur numérique.</span><span class="sxs-lookup"><span data-stu-id="92424-617">hello mathematical functions each perform a calculation, based on input values that are provided as arguments, and return a numeric value.</span></span> <span data-ttu-id="92424-618">Ce tableau répertorie les fonctions mathématiques intégrées qui sont prises en charge.</span><span class="sxs-lookup"><span data-stu-id="92424-618">Here’s a table of supported built-in mathematical functions.</span></span>


| <span data-ttu-id="92424-619">Utilisation</span><span class="sxs-lookup"><span data-stu-id="92424-619">Usage</span></span> | <span data-ttu-id="92424-620">Description</span><span class="sxs-lookup"><span data-stu-id="92424-620">Description</span></span> |
|----------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="92424-621">[[ABS (num_expr)](#bk_abs)</span><span class="sxs-lookup"><span data-stu-id="92424-621">[[ABS (num_expr)](#bk_abs)</span></span> | <span data-ttu-id="92424-622">Retourne hello valeur absolue (positive) de hello de l’expression numérique spécifiée.</span><span class="sxs-lookup"><span data-stu-id="92424-622">Returns hello absolute (positive) value of hello specified numeric expression.</span></span> |
| [<span data-ttu-id="92424-623">CEILING (num_expr)</span><span class="sxs-lookup"><span data-stu-id="92424-623">CEILING (num_expr)</span></span>](#bk_ceiling) | <span data-ttu-id="92424-624">Retourne hello plus petit entier supérieur à, ou être égal, hello expression numérique spécifiée.</span><span class="sxs-lookup"><span data-stu-id="92424-624">Returns hello smallest integer value greater than, or equal to, hello specified numeric expression.</span></span> |
| [<span data-ttu-id="92424-625">FLOOR (num_expr)</span><span class="sxs-lookup"><span data-stu-id="92424-625">FLOOR (num_expr)</span></span>](#bk_floor) | <span data-ttu-id="92424-626">Retourne des hello plus grand entier inférieur ou égal toohello l’expression numérique spécifiée.</span><span class="sxs-lookup"><span data-stu-id="92424-626">Returns hello largest integer less than or equal toohello specified numeric expression.</span></span> |
| [<span data-ttu-id="92424-627">EXP (num_expr)</span><span class="sxs-lookup"><span data-stu-id="92424-627">EXP (num_expr)</span></span>](#bk_exp) | <span data-ttu-id="92424-628">Exposant de hello retourne Hello l’expression numérique spécifiée.</span><span class="sxs-lookup"><span data-stu-id="92424-628">Returns hello exponent of hello specified numeric expression.</span></span> |
| <span data-ttu-id="92424-629">[LOG (num_expr [,base])](#bk_log)</span><span class="sxs-lookup"><span data-stu-id="92424-629">[LOG (num_expr [,base])](#bk_log)</span></span> | <span data-ttu-id="92424-630">Népérien retourne hello Hello spécifié expression numérique, voire logarithme hello hello à l’aide de base</span><span class="sxs-lookup"><span data-stu-id="92424-630">Returns hello natural logarithm of hello specified numeric expression, or hello logarithm using hello specified base</span></span> |
| [<span data-ttu-id="92424-631">LOG10 (num_expr)</span><span class="sxs-lookup"><span data-stu-id="92424-631">LOG10 (num_expr)</span></span>](#bk_log10) | <span data-ttu-id="92424-632">Valeur logarithmique de base 10 hello retourne Hello spécifié expression numérique.</span><span class="sxs-lookup"><span data-stu-id="92424-632">Returns hello base-10 logarithmic value of hello specified numeric expression.</span></span> |
| [<span data-ttu-id="92424-633">ROUND (num_expr)</span><span class="sxs-lookup"><span data-stu-id="92424-633">ROUND (num_expr)</span></span>](#bk_round) | <span data-ttu-id="92424-634">Retourne une valeur numérique, arrondie toohello nombre entier le plus proche.</span><span class="sxs-lookup"><span data-stu-id="92424-634">Returns a numeric value, rounded toohello closest integer value.</span></span> |
| [<span data-ttu-id="92424-635">TRUNC (num_expr)</span><span class="sxs-lookup"><span data-stu-id="92424-635">TRUNC (num_expr)</span></span>](#bk_trunc) | <span data-ttu-id="92424-636">Retourne une valeur numérique, tronquée toohello nombre entier le plus proche.</span><span class="sxs-lookup"><span data-stu-id="92424-636">Returns a numeric value, truncated toohello closest integer value.</span></span> |
| [<span data-ttu-id="92424-637">SQRT (num_expr)</span><span class="sxs-lookup"><span data-stu-id="92424-637">SQRT (num_expr)</span></span>](#bk_sqrt) | <span data-ttu-id="92424-638">Racine carrée retourne hello hello de l’expression numérique spécifiée.</span><span class="sxs-lookup"><span data-stu-id="92424-638">Returns hello square root of hello specified numeric expression.</span></span> |
| [<span data-ttu-id="92424-639">SQUARE (num_expr)</span><span class="sxs-lookup"><span data-stu-id="92424-639">SQUARE (num_expr)</span></span>](#bk_square) | <span data-ttu-id="92424-640">Hello retourne carrée hello de l’expression numérique spécifiée.</span><span class="sxs-lookup"><span data-stu-id="92424-640">Returns hello square of hello specified numeric expression.</span></span> |
| [<span data-ttu-id="92424-641">POWER (num_expr, num_expr)</span><span class="sxs-lookup"><span data-stu-id="92424-641">POWER (num_expr, num_expr)</span></span>](#bk_power) | <span data-ttu-id="92424-642">Puissance hello retourne hello toohello valeur de l’expression numérique spécifiée.</span><span class="sxs-lookup"><span data-stu-id="92424-642">Returns hello power of hello specified numeric expression toohello value specified.</span></span> |
| [<span data-ttu-id="92424-643">SIGN (num_expr)</span><span class="sxs-lookup"><span data-stu-id="92424-643">SIGN (num_expr)</span></span>](#bk_sign) | <span data-ttu-id="92424-644">Retourne hello signe la valeur (-1, 0, 1) de hello de l’expression numérique spécifiée.</span><span class="sxs-lookup"><span data-stu-id="92424-644">Returns hello sign value (-1, 0, 1) of hello specified numeric expression.</span></span> |
| [<span data-ttu-id="92424-645">ACOS (num_expr)</span><span class="sxs-lookup"><span data-stu-id="92424-645">ACOS (num_expr)</span></span>](#bk_acos) | <span data-ttu-id="92424-646">Angle de hello retourne, en radians, dont le cosinus est hello expression numérique spécifiée ; également appelé arc cosinus.</span><span class="sxs-lookup"><span data-stu-id="92424-646">Returns hello angle, in radians, whose cosine is hello specified numeric expression; also called arccosine.</span></span> |
| [<span data-ttu-id="92424-647">ASIN (num_expr)</span><span class="sxs-lookup"><span data-stu-id="92424-647">ASIN (num_expr)</span></span>](#bk_asin) | <span data-ttu-id="92424-648">Angle de hello retourne, en radians, dont le sinus est hello spécifié expression numérique.</span><span class="sxs-lookup"><span data-stu-id="92424-648">Returns hello angle, in radians, whose sine is hello specified numeric expression.</span></span> <span data-ttu-id="92424-649">Cette fonction est également appelée arcsinus.</span><span class="sxs-lookup"><span data-stu-id="92424-649">This is also called arcsine.</span></span> |
| [<span data-ttu-id="92424-650">ATAN (num_expr)</span><span class="sxs-lookup"><span data-stu-id="92424-650">ATAN (num_expr)</span></span>](#bk_atan) | <span data-ttu-id="92424-651">Angle de hello retourne, en radians, dont la tangente est hello spécifié expression numérique.</span><span class="sxs-lookup"><span data-stu-id="92424-651">Returns hello angle, in radians, whose tangent is hello specified numeric expression.</span></span> <span data-ttu-id="92424-652">Cette fonction est également appelée arctangente.</span><span class="sxs-lookup"><span data-stu-id="92424-652">This is also called arctangent.</span></span> |
| [<span data-ttu-id="92424-653">ATN2 (num_expr)</span><span class="sxs-lookup"><span data-stu-id="92424-653">ATN2 (num_expr)</span></span>](#bk_atn2) | <span data-ttu-id="92424-654">Retourne hello angle, en radians, entre l’axe des x positif de hello et ray hello à partir du point de toohello origine hello (y, x), où x et y sont des valeurs hello Hello deux expressions de type float spécifiée.</span><span class="sxs-lookup"><span data-stu-id="92424-654">Returns hello angle, in radians, between hello positive x-axis and hello ray from hello origin toohello point (y, x), where x and y are hello values of hello two specified float expressions.</span></span> |
| [<span data-ttu-id="92424-655">COS (num_expr)</span><span class="sxs-lookup"><span data-stu-id="92424-655">COS (num_expr)</span></span>](#bk_cos) | <span data-ttu-id="92424-656">Cosinus trigonométrique de hello retourne Hello spécifié d’angle, en radians, Bonjour de l’expression spécifiée.</span><span class="sxs-lookup"><span data-stu-id="92424-656">Returns hello trigonometric cosine of hello specified angle, in radians, in hello specified expression.</span></span> |
| [<span data-ttu-id="92424-657">COT (num_expr)</span><span class="sxs-lookup"><span data-stu-id="92424-657">COT (num_expr)</span></span>](#bk_cot) | <span data-ttu-id="92424-658">Cotangente trigonométrique de hello retourne Hello spécifié d’angle, en radians, Bonjour de l’expression numérique spécifiée.</span><span class="sxs-lookup"><span data-stu-id="92424-658">Returns hello trigonometric cotangent of hello specified angle, in radians, in hello specified numeric expression.</span></span> |
| [<span data-ttu-id="92424-659">DEGREES (num_expr)</span><span class="sxs-lookup"><span data-stu-id="92424-659">DEGREES (num_expr)</span></span>](#bk_degrees) | <span data-ttu-id="92424-660">Retourne hello angle correspondant en degrés pour un angle spécifié en radians.</span><span class="sxs-lookup"><span data-stu-id="92424-660">Returns hello corresponding angle in degrees for an angle specified in radians.</span></span> |
| [<span data-ttu-id="92424-661">PI ()</span><span class="sxs-lookup"><span data-stu-id="92424-661">PI ()</span></span>](#bk_pi) | <span data-ttu-id="92424-662">Retourne hello valeur constante de PI.</span><span class="sxs-lookup"><span data-stu-id="92424-662">Returns hello constant value of PI.</span></span> |
| [<span data-ttu-id="92424-663">RADIANS (num_expr)</span><span class="sxs-lookup"><span data-stu-id="92424-663">RADIANS (num_expr)</span></span>](#bk_radians) | <span data-ttu-id="92424-664">Retourne des radians lorsqu’une expression numérique, en degrés, est entrée.</span><span class="sxs-lookup"><span data-stu-id="92424-664">Returns radians when a numeric expression, in degrees, is entered.</span></span> |
| [<span data-ttu-id="92424-665">SIN (num_expr)</span><span class="sxs-lookup"><span data-stu-id="92424-665">SIN (num_expr)</span></span>](#bk_sin) | <span data-ttu-id="92424-666">Sinus trigonométrique de hello retourne Hello spécifié d’angle, en radians, Bonjour de l’expression spécifiée.</span><span class="sxs-lookup"><span data-stu-id="92424-666">Returns hello trigonometric sine of hello specified angle, in radians, in hello specified expression.</span></span> |
| [<span data-ttu-id="92424-667">TAN (num_expr)</span><span class="sxs-lookup"><span data-stu-id="92424-667">TAN (num_expr)</span></span>](#bk_tan) | <span data-ttu-id="92424-668">Tangente de hello retourne d’expression d’entrée hello dans hello de l’expression spécifiée.</span><span class="sxs-lookup"><span data-stu-id="92424-668">Returns hello tangent of hello input expression, in hello specified expression.</span></span> |

<span data-ttu-id="92424-669">Par exemple, vous pouvez maintenant exécuter des requêtes hello suivante :</span><span class="sxs-lookup"><span data-stu-id="92424-669">For example, you can now run queries like hello following:</span></span>

<span data-ttu-id="92424-670">**Requête**</span><span class="sxs-lookup"><span data-stu-id="92424-670">**Query**</span></span>

    SELECT VALUE ABS(-4)

<span data-ttu-id="92424-671">**Résultats**</span><span class="sxs-lookup"><span data-stu-id="92424-671">**Results**</span></span>

    [4]

<span data-ttu-id="92424-672">Hello principale différence entre tooANSI de fonctions en comparaison de base de données Cosmos SQL est qu’ils sont conçu toowork correctement avec les données de schéma sans schéma et mixte.</span><span class="sxs-lookup"><span data-stu-id="92424-672">hello main difference between Cosmos DB’s functions compared tooANSI SQL is that they are designed toowork well with schema-less and mixed schema data.</span></span> <span data-ttu-id="92424-673">Par exemple, si vous avez un document dans lequel la propriété Size hello est manquant ou a une valeur non numérique comme « inconnu », puis le document de hello est ignorée, au lieu de retourner une erreur.</span><span class="sxs-lookup"><span data-stu-id="92424-673">For example, if you have a document where hello Size property is missing, or has a non-numeric value like “unknown”, then hello document is skipped over, instead of returning an error.</span></span>

### <a name="type-checking-functions"></a><span data-ttu-id="92424-674">Fonctions de vérification du type</span><span class="sxs-lookup"><span data-stu-id="92424-674">Type checking functions</span></span>
<span data-ttu-id="92424-675">les fonctions de vérification de type Hello vous autorisent toocheck hello ce type d’une expression dans des requêtes SQL.</span><span class="sxs-lookup"><span data-stu-id="92424-675">hello type checking functions allow you toocheck hello type of an expression within SQL queries.</span></span> <span data-ttu-id="92424-676">Type de fonctions de vérification peuvent être utilisé type hello de toodetermine des propriétés dans les documents volée hello lorsqu’il est variable ou inconnu.</span><span class="sxs-lookup"><span data-stu-id="92424-676">Type checking functions can be used toodetermine hello type of properties within documents on hello fly when it is variable or unknown.</span></span> <span data-ttu-id="92424-677">Le tableau répertorie les fonctions de vérification du type intégrées qui sont prises en charge.</span><span class="sxs-lookup"><span data-stu-id="92424-677">Here’s a table of supported built-in type checking functions.</span></span>

<table>
<tr>
  <td><span data-ttu-id="92424-678"><strong>Utilisation</strong></span><span class="sxs-lookup"><span data-stu-id="92424-678"><strong>Usage</strong></span></span></td>
  <td><span data-ttu-id="92424-679"><strong>Description</strong></span><span class="sxs-lookup"><span data-stu-id="92424-679"><strong>Description</strong></span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="92424-680"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_array">IS_ARRAY (expr)</a></span><span class="sxs-lookup"><span data-stu-id="92424-680"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_array">IS_ARRAY (expr)</a></span></span></td>
  <td><span data-ttu-id="92424-681">Retourne une valeur booléenne indiquant si le type hello de valeur de hello est un tableau.</span><span class="sxs-lookup"><span data-stu-id="92424-681">Returns a Boolean indicating if hello type of hello value is an array.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="92424-682"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_bool">IS_BOOL (expr)</a></span><span class="sxs-lookup"><span data-stu-id="92424-682"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_bool">IS_BOOL (expr)</a></span></span></td>
  <td><span data-ttu-id="92424-683">Retourne une valeur booléenne indiquant si le type hello de valeur de hello est une valeur booléenne.</span><span class="sxs-lookup"><span data-stu-id="92424-683">Returns a Boolean indicating if hello type of hello value is a Boolean.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="92424-684"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_null">IS_NULL (expr)</a></span><span class="sxs-lookup"><span data-stu-id="92424-684"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_null">IS_NULL (expr)</a></span></span></td>
  <td><span data-ttu-id="92424-685">Retourne une valeur booléenne indiquant si le type hello de valeur de hello est null.</span><span class="sxs-lookup"><span data-stu-id="92424-685">Returns a Boolean indicating if hello type of hello value is null.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="92424-686"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_number">IS_NUMBER (expr)</a></span><span class="sxs-lookup"><span data-stu-id="92424-686"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_number">IS_NUMBER (expr)</a></span></span></td>
  <td><span data-ttu-id="92424-687">Retourne une valeur booléenne indiquant si le type hello de valeur de hello est un nombre.</span><span class="sxs-lookup"><span data-stu-id="92424-687">Returns a Boolean indicating if hello type of hello value is a number.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="92424-688"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_object">IS_OBJECT (expr)</a></span><span class="sxs-lookup"><span data-stu-id="92424-688"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_object">IS_OBJECT (expr)</a></span></span></td>
  <td><span data-ttu-id="92424-689">Retourne une valeur booléenne indiquant si le type hello de valeur de hello est un objet JSON.</span><span class="sxs-lookup"><span data-stu-id="92424-689">Returns a Boolean indicating if hello type of hello value is a JSON object.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="92424-690"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_string">IS_STRING (expr)</a></span><span class="sxs-lookup"><span data-stu-id="92424-690"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_string">IS_STRING (expr)</a></span></span></td>
  <td><span data-ttu-id="92424-691">Retourne une valeur booléenne indiquant si le type hello de valeur de hello est une chaîne.</span><span class="sxs-lookup"><span data-stu-id="92424-691">Returns a Boolean indicating if hello type of hello value is a string.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="92424-692"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_defined">IS_DEFINED (expr)</a></span><span class="sxs-lookup"><span data-stu-id="92424-692"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_defined">IS_DEFINED (expr)</a></span></span></td>
  <td><span data-ttu-id="92424-693">Retourne une valeur booléenne indiquant si une valeur a été assignée à la propriété de hello.</span><span class="sxs-lookup"><span data-stu-id="92424-693">Returns a Boolean indicating if hello property has been assigned a value.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="92424-694"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_primitive">IS_PRIMITIVE (expr)</a></span><span class="sxs-lookup"><span data-stu-id="92424-694"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_primitive">IS_PRIMITIVE (expr)</a></span></span></td>
  <td><span data-ttu-id="92424-695">Retourne une valeur booléenne indiquant si le type hello de valeur de hello est null, nombre, booléen ou chaîne.</span><span class="sxs-lookup"><span data-stu-id="92424-695">Returns a Boolean indicating if hello type of hello value is a string, number, Boolean or null.</span></span></td>
</tr>

</table>

<span data-ttu-id="92424-696">L’utilisation de ces fonctions, vous pouvez maintenant exécuter des requêtes hello suivante :</span><span class="sxs-lookup"><span data-stu-id="92424-696">Using these functions, you can now run queries like hello following:</span></span>

<span data-ttu-id="92424-697">**Requête**</span><span class="sxs-lookup"><span data-stu-id="92424-697">**Query**</span></span>

    SELECT VALUE IS_NUMBER(-4)

<span data-ttu-id="92424-698">**Résultats**</span><span class="sxs-lookup"><span data-stu-id="92424-698">**Results**</span></span>

    [true]

### <a name="string-functions"></a><span data-ttu-id="92424-699">Fonctions de chaîne</span><span class="sxs-lookup"><span data-stu-id="92424-699">String functions</span></span>
<span data-ttu-id="92424-700">Bonjour fonctions scalaires suivantes effectuent une opération sur une valeur de chaîne d’entrée et retournent une valeur numérique ou booléenne, une chaîne.</span><span class="sxs-lookup"><span data-stu-id="92424-700">hello following scalar functions perform an operation on a string input value and return a string, numeric or Boolean value.</span></span> <span data-ttu-id="92424-701">Voici un tableau des fonctions de chaîne intégrées :</span><span class="sxs-lookup"><span data-stu-id="92424-701">Here's a table of built-in string functions:</span></span>

| <span data-ttu-id="92424-702">Utilisation</span><span class="sxs-lookup"><span data-stu-id="92424-702">Usage</span></span> | <span data-ttu-id="92424-703">Description</span><span class="sxs-lookup"><span data-stu-id="92424-703">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="92424-704">LENGTH (str_expr)</span><span class="sxs-lookup"><span data-stu-id="92424-704">LENGTH (str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_length) |<span data-ttu-id="92424-705">Retourne hello nombre de caractères de hello de l’expression de chaîne spécifiée</span><span class="sxs-lookup"><span data-stu-id="92424-705">Returns hello number of characters of hello specified string expression</span></span> |
| <span data-ttu-id="92424-706">[CONCAT (str_expr, str_expr [, str_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_concat)</span><span class="sxs-lookup"><span data-stu-id="92424-706">[CONCAT (str_expr, str_expr [, str_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_concat)</span></span> |<span data-ttu-id="92424-707">Retourne une chaîne qui est le résultat de hello de la concaténation de deux ou plusieurs valeurs de chaîne.</span><span class="sxs-lookup"><span data-stu-id="92424-707">Returns a string that is hello result of concatenating two or more string values.</span></span> |
| [<span data-ttu-id="92424-708">SUBSTRING (str_expr, num_expr, num_expr)</span><span class="sxs-lookup"><span data-stu-id="92424-708">SUBSTRING (str_expr, num_expr, num_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_substring) |<span data-ttu-id="92424-709">Retourne une partie d’une expression de chaîne.</span><span class="sxs-lookup"><span data-stu-id="92424-709">Returns part of a string expression.</span></span> |
| [<span data-ttu-id="92424-710">STARTSWITH (str_expr, str_expr)</span><span class="sxs-lookup"><span data-stu-id="92424-710">STARTSWITH (str_expr, str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_startswith) |<span data-ttu-id="92424-711">Retourne une valeur booléenne indiquant si les première expression de chaîne hello se termine ensuite par hello</span><span class="sxs-lookup"><span data-stu-id="92424-711">Returns a Boolean indicating whether hello first string expression ends with hello second</span></span> |
| [<span data-ttu-id="92424-712">ENDSWITH (str_expr, str_expr)</span><span class="sxs-lookup"><span data-stu-id="92424-712">ENDSWITH (str_expr, str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_endswith) |<span data-ttu-id="92424-713">Retourne une valeur booléenne indiquant si les première expression de chaîne hello se termine ensuite par hello</span><span class="sxs-lookup"><span data-stu-id="92424-713">Returns a Boolean indicating whether hello first string expression ends with hello second</span></span> |
| [<span data-ttu-id="92424-714">CONTAINS (str_expr, str_expr)</span><span class="sxs-lookup"><span data-stu-id="92424-714">CONTAINS (str_expr, str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_contains) |<span data-ttu-id="92424-715">Retourne une valeur booléenne qui indique si le première expression de chaîne hello contient hello ensuite.</span><span class="sxs-lookup"><span data-stu-id="92424-715">Returns a Boolean indicating whether hello first string expression contains hello second.</span></span> |
| [<span data-ttu-id="92424-716">INDEX_OF (str_expr, str_expr)</span><span class="sxs-lookup"><span data-stu-id="92424-716">INDEX_OF (str_expr, str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_index_of) |<span data-ttu-id="92424-717">Retourne hello position de départ des hello première occurrence de hello deuxième expression de chaîne hello première expression de chaîne spécifiée, ou -1 si la chaîne de hello est introuvable.</span><span class="sxs-lookup"><span data-stu-id="92424-717">Returns hello starting position of hello first occurrence of hello second string expression within hello first specified string expression, or -1 if hello string is not found.</span></span> |
| [<span data-ttu-id="92424-718">LEFT (str_expr, num_expr)</span><span class="sxs-lookup"><span data-stu-id="92424-718">LEFT (str_expr, num_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_left) |<span data-ttu-id="92424-719">Retourne hello partie gauche d’une chaîne avec hello spécifié de caractères.</span><span class="sxs-lookup"><span data-stu-id="92424-719">Returns hello left part of a string with hello specified number of characters.</span></span> |
| [<span data-ttu-id="92424-720">RIGHT (str_expr, num_expr)</span><span class="sxs-lookup"><span data-stu-id="92424-720">RIGHT (str_expr, num_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_right) |<span data-ttu-id="92424-721">Hello retourne à droite dans le cadre d’une chaîne avec hello nombre spécifié de caractères.</span><span class="sxs-lookup"><span data-stu-id="92424-721">Returns hello right part of a string with hello specified number of characters.</span></span> |
| [<span data-ttu-id="92424-722">LTRIM (str_expr)</span><span class="sxs-lookup"><span data-stu-id="92424-722">LTRIM (str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_ltrim) |<span data-ttu-id="92424-723">Retourne une expression de chaîne après avoir supprimé les espaces de début.</span><span class="sxs-lookup"><span data-stu-id="92424-723">Returns a string expression after it removes leading blanks.</span></span> |
| [<span data-ttu-id="92424-724">RTRIM (str_expr)</span><span class="sxs-lookup"><span data-stu-id="92424-724">RTRIM (str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_rtrim) |<span data-ttu-id="92424-725">Retourne une expression de chaîne après avoir tronqué tous les espaces de fin.</span><span class="sxs-lookup"><span data-stu-id="92424-725">Returns a string expression after truncating all trailing blanks.</span></span> |
| [<span data-ttu-id="92424-726">LOWER (str_expr)</span><span class="sxs-lookup"><span data-stu-id="92424-726">LOWER (str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_lower) |<span data-ttu-id="92424-727">Retourne une expression de chaîne après la conversion de toolowercase de données de caractères majuscules en caractères.</span><span class="sxs-lookup"><span data-stu-id="92424-727">Returns a string expression after converting uppercase character data toolowercase.</span></span> |
| [<span data-ttu-id="92424-728">UPPER (str_expr)</span><span class="sxs-lookup"><span data-stu-id="92424-728">UPPER (str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_upper) |<span data-ttu-id="92424-729">Retourne une expression de chaîne après la conversion de toouppercase de données de caractères en minuscules.</span><span class="sxs-lookup"><span data-stu-id="92424-729">Returns a string expression after converting lowercase character data toouppercase.</span></span> |
| [<span data-ttu-id="92424-730">REPLACE (str_expr, str_expr, str_expr)</span><span class="sxs-lookup"><span data-stu-id="92424-730">REPLACE (str_expr, str_expr, str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_replace) |<span data-ttu-id="92424-731">Remplace toutes les occurrences d’une valeur de chaîne spécifiée par une autre valeur de chaîne.</span><span class="sxs-lookup"><span data-stu-id="92424-731">Replaces all occurrences of a specified string value with another string value.</span></span> |
| [<span data-ttu-id="92424-732">REPLICATE (str_expr, num_expr)</span><span class="sxs-lookup"><span data-stu-id="92424-732">REPLICATE (str_expr, num_expr)</span></span>](https://docs.microsoft.com/azure/cosmos-db/documentdb-sql-query-reference#bk_replicate) |<span data-ttu-id="92424-733">Répète une valeur de chaîne un nombre de fois spécifié.</span><span class="sxs-lookup"><span data-stu-id="92424-733">Repeats a string value a specified number of times.</span></span> |
| [<span data-ttu-id="92424-734">REVERSE (str_expr)</span><span class="sxs-lookup"><span data-stu-id="92424-734">REVERSE (str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_reverse) |<span data-ttu-id="92424-735">Retourne l’ordre inverse d’une valeur de chaîne hello.</span><span class="sxs-lookup"><span data-stu-id="92424-735">Returns hello reverse order of a string value.</span></span> |

<span data-ttu-id="92424-736">À l’aide de ces fonctions, vous pouvez maintenant exécuter des requêtes hello suivante.</span><span class="sxs-lookup"><span data-stu-id="92424-736">Using these functions, you can now run queries like hello following.</span></span> <span data-ttu-id="92424-737">Par exemple, vous pouvez retourner nom de famille hello en majuscules comme suit :</span><span class="sxs-lookup"><span data-stu-id="92424-737">For example, you can return hello family name in uppercase as follows:</span></span>

<span data-ttu-id="92424-738">**Requête**</span><span class="sxs-lookup"><span data-stu-id="92424-738">**Query**</span></span>

    SELECT VALUE UPPER(Families.id)
    FROM Families

<span data-ttu-id="92424-739">**Résultats**</span><span class="sxs-lookup"><span data-stu-id="92424-739">**Results**</span></span>

    [
        "WAKEFIELDFAMILY", 
        "ANDERSENFAMILY"
    ]

<span data-ttu-id="92424-740">Vous pouvez également concaténer des chaînes, comme dans cet exemple :</span><span class="sxs-lookup"><span data-stu-id="92424-740">Or concatenate strings like in this example:</span></span>

<span data-ttu-id="92424-741">**Requête**</span><span class="sxs-lookup"><span data-stu-id="92424-741">**Query**</span></span>

    SELECT Families.id, CONCAT(Families.address.city, ",", Families.address.state) AS location
    FROM Families

<span data-ttu-id="92424-742">**Résultats**</span><span class="sxs-lookup"><span data-stu-id="92424-742">**Results**</span></span>

    [{
      "id": "WakefieldFamily",
      "location": "NY,NY"
    },
    {
      "id": "AndersenFamily",
      "location": "seattle,WA"
    }]


<span data-ttu-id="92424-743">Fonctions de chaîne permet également de hello où les résultats de toofilter de clause, comme dans hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="92424-743">String functions can also be used in hello WHERE clause toofilter results, like in hello following example:</span></span>

<span data-ttu-id="92424-744">**Requête**</span><span class="sxs-lookup"><span data-stu-id="92424-744">**Query**</span></span>

    SELECT Families.id, Families.address.city
    FROM Families
    WHERE STARTSWITH(Families.id, "Wakefield")

<span data-ttu-id="92424-745">**Résultats**</span><span class="sxs-lookup"><span data-stu-id="92424-745">**Results**</span></span>

    [{
      "id": "WakefieldFamily",
      "city": "NY"
    }]

### <a name="array-functions"></a><span data-ttu-id="92424-746">Fonctions de tableau</span><span class="sxs-lookup"><span data-stu-id="92424-746">Array functions</span></span>
<span data-ttu-id="92424-747">Hello suivant des fonctions scalaires effectuent une opération sur une valeur d’entrée de tableau et le retour numérique, la valeur booléenne ou de tableau.</span><span class="sxs-lookup"><span data-stu-id="92424-747">hello following scalar functions perform an operation on an array input value and return numeric, Boolean or array value.</span></span> <span data-ttu-id="92424-748">Voici un tableau des fonctions de tableau intégrées :</span><span class="sxs-lookup"><span data-stu-id="92424-748">Here's a table of built-in array functions:</span></span>

| <span data-ttu-id="92424-749">Utilisation</span><span class="sxs-lookup"><span data-stu-id="92424-749">Usage</span></span> | <span data-ttu-id="92424-750">Description</span><span class="sxs-lookup"><span data-stu-id="92424-750">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="92424-751">ARRAY_LENGTH (arr_expr)</span><span class="sxs-lookup"><span data-stu-id="92424-751">ARRAY_LENGTH (arr_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_length) |<span data-ttu-id="92424-752">Nombre de hello retourne des éléments de hello spécifié expression de tableau.</span><span class="sxs-lookup"><span data-stu-id="92424-752">Returns hello number of elements of hello specified array expression.</span></span> |
| <span data-ttu-id="92424-753">[ARRAY_CONCAT (arr_expr, arr_expr [, arr_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_concat)</span><span class="sxs-lookup"><span data-stu-id="92424-753">[ARRAY_CONCAT (arr_expr, arr_expr [, arr_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_concat)</span></span> |<span data-ttu-id="92424-754">Retourne un tableau qui est le résultat de hello de la concaténation de deux ou plusieurs valeurs de tableau.</span><span class="sxs-lookup"><span data-stu-id="92424-754">Returns an array that is hello result of concatenating two or more array values.</span></span> |
| <span data-ttu-id="92424-755">[ARRAY_CONTAINS (arr_expr, expr [, bool_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_contains)</span><span class="sxs-lookup"><span data-stu-id="92424-755">[ARRAY_CONTAINS (arr_expr, expr [, bool_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_contains)</span></span> |<span data-ttu-id="92424-756">Retourne une valeur booléenne qui indique si le tableau de hello contient hello valeur spécifiée.</span><span class="sxs-lookup"><span data-stu-id="92424-756">Returns a Boolean indicating whether hello array contains hello specified value.</span></span> <span data-ttu-id="92424-757">Peut spécifier si la correspondance de hello est complet ou partiel.</span><span class="sxs-lookup"><span data-stu-id="92424-757">Can specify if hello match is full or partial.</span></span> |
| <span data-ttu-id="92424-758">[ARRAY_SLICE (arr_expr, num_expr [, num_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_slice)</span><span class="sxs-lookup"><span data-stu-id="92424-758">[ARRAY_SLICE (arr_expr, num_expr [, num_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_slice)</span></span> |<span data-ttu-id="92424-759">Retourne une partie d’une expression de tableau.</span><span class="sxs-lookup"><span data-stu-id="92424-759">Returns part of an array expression.</span></span> |

<span data-ttu-id="92424-760">Fonctions de tableau peuvent être utilisé toomanipulate des tableaux dans JSON.</span><span class="sxs-lookup"><span data-stu-id="92424-760">Array functions can be used toomanipulate arrays within JSON.</span></span> <span data-ttu-id="92424-761">Par exemple, voici une requête qui retourne tous les documents où un des parents de hello « Robin Wakefield ».</span><span class="sxs-lookup"><span data-stu-id="92424-761">For example, here's a query that returns all documents where one of hello parents is "Robin Wakefield".</span></span> 

<span data-ttu-id="92424-762">**Requête**</span><span class="sxs-lookup"><span data-stu-id="92424-762">**Query**</span></span>

    SELECT Families.id 
    FROM Families 
    WHERE ARRAY_CONTAINS(Families.parents, { givenName: "Robin", familyName: "Wakefield" })

<span data-ttu-id="92424-763">**Résultats**</span><span class="sxs-lookup"><span data-stu-id="92424-763">**Results**</span></span>

    [{
      "id": "WakefieldFamily"
    }]

<span data-ttu-id="92424-764">Vous pouvez spécifier un fragment partiels pour les éléments correspondants dans le tableau de hello.</span><span class="sxs-lookup"><span data-stu-id="92424-764">You can specify a partial fragment for matching elements within hello array.</span></span> <span data-ttu-id="92424-765">Hello requête suivante recherche tous les parents avec hello `givenName` de `Robin`.</span><span class="sxs-lookup"><span data-stu-id="92424-765">hello following query finds all parents with hello `givenName` of `Robin`.</span></span>

<span data-ttu-id="92424-766">**Requête**</span><span class="sxs-lookup"><span data-stu-id="92424-766">**Query**</span></span>

    SELECT Families.id 
    FROM Families 
    WHERE ARRAY_CONTAINS(Families.parents, { givenName: "Robin" }, true)

<span data-ttu-id="92424-767">**Résultats**</span><span class="sxs-lookup"><span data-stu-id="92424-767">**Results**</span></span>

    [{
      "id": "WakefieldFamily"
    }]


<span data-ttu-id="92424-768">Voici un autre exemple qui utilise ARRAY_LENGTH tooget hello nombre d’enfants par famille.</span><span class="sxs-lookup"><span data-stu-id="92424-768">Here's another example that uses ARRAY_LENGTH tooget hello number of children per family.</span></span>

<span data-ttu-id="92424-769">**Requête**</span><span class="sxs-lookup"><span data-stu-id="92424-769">**Query**</span></span>

    SELECT Families.id, ARRAY_LENGTH(Families.children) AS numberOfChildren
    FROM Families 

<span data-ttu-id="92424-770">**Résultats**</span><span class="sxs-lookup"><span data-stu-id="92424-770">**Results**</span></span>

    [{
      "id": "WakefieldFamily",
      "numberOfChildren": 2
    },
    {
      "id": "AndersenFamily",
      "numberOfChildren": 1
    }]

### <a name="spatial-functions"></a><span data-ttu-id="92424-771">Fonctions spatiales</span><span class="sxs-lookup"><span data-stu-id="92424-771">Spatial functions</span></span>
<span data-ttu-id="92424-772">COSMOS DB prend en charge hello suivant des fonctions intégrées d’Open Geospatial Consortium (OGC) pour l’interrogation de géographiques.</span><span class="sxs-lookup"><span data-stu-id="92424-772">Cosmos DB supports hello following Open Geospatial Consortium (OGC) built-in functions for geospatial querying.</span></span> 

<table>
<tr>
  <td><span data-ttu-id="92424-773"><strong>Utilisation</strong></span><span class="sxs-lookup"><span data-stu-id="92424-773"><strong>Usage</strong></span></span></td>
  <td><span data-ttu-id="92424-774"><strong>Description</strong></span><span class="sxs-lookup"><span data-stu-id="92424-774"><strong>Description</strong></span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="92424-775">ST_DISTANCE (point_expr, point_expr)</span><span class="sxs-lookup"><span data-stu-id="92424-775">ST_DISTANCE (point_expr, point_expr)</span></span></td>
  <td><span data-ttu-id="92424-776">Retourne la distance hello entre les expressions LineString, Polygon ou GeoJSON Point hello deux.</span><span class="sxs-lookup"><span data-stu-id="92424-776">Returns hello distance between hello two GeoJSON Point, Polygon, or LineString expressions.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="92424-777">ST_WITHIN (point_expr, polygon_expr)</span><span class="sxs-lookup"><span data-stu-id="92424-777">ST_WITHIN (point_expr, polygon_expr)</span></span></td>
  <td><span data-ttu-id="92424-778">Retourne une expression booléenne indiquant si hello premier GeoJSON objet (Point, polygone ou LineString) se trouve dans hello deuxième GeoJSON objet (Point, polygone ou LineString).</span><span class="sxs-lookup"><span data-stu-id="92424-778">Returns a Boolean expression indicating whether hello first GeoJSON object (Point, Polygon, or LineString) is within hello second GeoJSON object (Point, Polygon, or LineString).</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="92424-779">ST_INTERSECTS (spatial_expr, spatial_expr)</span><span class="sxs-lookup"><span data-stu-id="92424-779">ST_INTERSECTS (spatial_expr, spatial_expr)</span></span></td>
  <td><span data-ttu-id="92424-780">Retourne une expression booléenne indiquant si hello deux GeoJSON objets spécifiés (Point, polygone ou LineString) se croisent.</span><span class="sxs-lookup"><span data-stu-id="92424-780">Returns a Boolean expression indicating whether hello two specified GeoJSON objects (Point, Polygon, or LineString) intersect.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="92424-781">ST_ISVALID</span><span class="sxs-lookup"><span data-stu-id="92424-781">ST_ISVALID</span></span></td>
  <td><span data-ttu-id="92424-782">Retourne une valeur booléenne indiquant si hello spécifiée expression LineString, Polygon ou GeoJSON Point n’est valide.</span><span class="sxs-lookup"><span data-stu-id="92424-782">Returns a Boolean value indicating whether hello specified GeoJSON Point, Polygon, or LineString expression is valid.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="92424-783">ST_ISVALIDDETAILED</span><span class="sxs-lookup"><span data-stu-id="92424-783">ST_ISVALIDDETAILED</span></span></td>
  <td><span data-ttu-id="92424-784">Retourne une valeur JSON contenant une valeur booléenne si hello de l’expression LineString, Polygon ou GeoJSON Point spécifiée est valide et si elle est non valide, en outre hello motif en tant que valeur de chaîne.</span><span class="sxs-lookup"><span data-stu-id="92424-784">Returns a JSON value containing a Boolean value if hello specified GeoJSON Point, Polygon, or LineString expression is valid, and if invalid, additionally hello reason as a string value.</span></span></td>
</tr>
</table>

<span data-ttu-id="92424-785">Les fonctions spatiale peuvent être des requêtes de proximité tooperform utilisé par rapport aux données spatiales.</span><span class="sxs-lookup"><span data-stu-id="92424-785">Spatial functions can be used tooperform proximity queries against spatial data.</span></span> <span data-ttu-id="92424-786">Par exemple, voici une requête qui retourne la que famille de tous les documents qu’est 30 kilomètres de hello emplacement spécifié à l’aide de fonctions intégrées de ST_DISTANCE hello.</span><span class="sxs-lookup"><span data-stu-id="92424-786">For example, here's a query that returns all family documents that are within 30 km of hello specified location using hello ST_DISTANCE built-in function.</span></span> 

<span data-ttu-id="92424-787">**Requête**</span><span class="sxs-lookup"><span data-stu-id="92424-787">**Query**</span></span>

    SELECT f.id 
    FROM Families f 
    WHERE ST_DISTANCE(f.location, {'type': 'Point', 'coordinates':[31.9, -4.8]}) < 30000

<span data-ttu-id="92424-788">**Résultats**</span><span class="sxs-lookup"><span data-stu-id="92424-788">**Results**</span></span>

    [{
      "id": "WakefieldFamily"
    }]

<span data-ttu-id="92424-789">Pour plus d’informations sur la prise en charge géospatiale dans Cosmos DB, consultez [Working with geospatial data in Azure Cosmos DB (Utilisation de données géospatiales dans Azure Cosmos DB)](geospatial.md).</span><span class="sxs-lookup"><span data-stu-id="92424-789">For more details on geospatial support in Cosmos DB, please see [Working with geospatial data in Azure Cosmos DB](geospatial.md).</span></span> <span data-ttu-id="92424-790">Qui encapsule des fonctions spatiales hello syntaxe SQL pour la base de données Cosmos.</span><span class="sxs-lookup"><span data-stu-id="92424-790">That wraps up spatial functions, and hello SQL syntax for Cosmos DB.</span></span> <span data-ttu-id="92424-791">Maintenant examinons à présent comment LINQ interrogation fonctionne et comment il interagit avec la syntaxe hello nous avons vu jusqu'à présent.</span><span class="sxs-lookup"><span data-stu-id="92424-791">Now let's take a look at how LINQ querying works and how it interacts with hello syntax we've seen so far.</span></span>

## <span data-ttu-id="92424-792"><a id="Linq"></a>LINQ tooDocumentDB API SQL</span><span class="sxs-lookup"><span data-stu-id="92424-792"><a id="Linq"></a>LINQ tooDocumentDB API SQL</span></span>
<span data-ttu-id="92424-793">LINQ est un modèle de programmation .NET qui exprime un calcul en tant que requête sur des flux d'objets.</span><span class="sxs-lookup"><span data-stu-id="92424-793">LINQ is a .NET programming model that expresses computation as queries on streams of objects.</span></span> <span data-ttu-id="92424-794">COSMOS DB fournit un toointerface bibliothèque côté client avec LINQ grâce à une conversion entre JSON et les objets .NET et un mappage à partir d’un sous-ensemble de LINQ interroge les requêtes tooCosmos DB.</span><span class="sxs-lookup"><span data-stu-id="92424-794">Cosmos DB provides a client-side library toointerface with LINQ by facilitating a conversion between JSON and .NET objects and a mapping from a subset of LINQ queries tooCosmos DB queries.</span></span> 

<span data-ttu-id="92424-795">image Hello ci-dessous montre l’architecture hello de prendre en charge les requêtes LINQ à l’aide de la base de données Cosmos.</span><span class="sxs-lookup"><span data-stu-id="92424-795">hello picture below shows hello architecture of supporting LINQ queries using Cosmos DB.</span></span>  <span data-ttu-id="92424-796">À l’aide du client de base de données Cosmos hello, les développeurs peuvent créer un **IQueryable** que directement des requêtes hello Cosmos DB demandez au fournisseur, ce qui traduit par requête LINQ de hello une requête de base de données Cosmos de l’objet.</span><span class="sxs-lookup"><span data-stu-id="92424-796">Using hello Cosmos DB client, developers can create an **IQueryable** object that directly queries hello Cosmos DB query provider, which then translates hello LINQ query into a Cosmos DB query.</span></span> <span data-ttu-id="92424-797">requête de Hello est ensuite transmise toohello tooretrieve de serveur de base de données Cosmos un jeu de résultats au format JSON.</span><span class="sxs-lookup"><span data-stu-id="92424-797">hello query is then passed toohello Cosmos DB server tooretrieve a set of results in JSON format.</span></span> <span data-ttu-id="92424-798">Hello retourné les résultats sont désérialisés dans un flux d’objets .NET côté client de hello.</span><span class="sxs-lookup"><span data-stu-id="92424-798">hello returned results are deserialized into a stream of .NET objects on hello client side.</span></span>

![Architecture de prise en charge des requêtes LINQ avec l’API DocumentDB (syntaxe SQL, langage de requête JSON, concepts de bases de données et requêtes SQL)][1]

### <a name="net-and-json-mapping"></a><span data-ttu-id="92424-800">Mappage .NET et JSON</span><span class="sxs-lookup"><span data-stu-id="92424-800">.NET and JSON mapping</span></span>
<span data-ttu-id="92424-801">mappage de Hello entre les objets .NET et les documents JSON est naturelle - chaque champ de membre de données est mappé tooa JSON objet, où le nom du champ hello est mappé dans « clé » toohello objet de hello et hello « value » est mappée de manière récursive toohello valeur faisant partie d’hello objet.</span><span class="sxs-lookup"><span data-stu-id="92424-801">hello mapping between .NET objects and JSON documents is natural - each data member field is mapped tooa JSON object, where hello field name is mapped toohello "key" part of hello object and hello "value" part is recursively mapped toohello value part of hello object.</span></span> <span data-ttu-id="92424-802">Envisagez de hello l’exemple suivant : objet de famille hello créé est document JSON de toohello mappé comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="92424-802">Consider hello following example: hello Family object created is mapped toohello JSON document as shown below.</span></span> <span data-ttu-id="92424-803">Et vice versa, document JSON de hello mappé tooa arrière .NET objet.</span><span class="sxs-lookup"><span data-stu-id="92424-803">And vice versa, hello JSON document is mapped back tooa .NET object.</span></span>

<span data-ttu-id="92424-804">**Classe C#**</span><span class="sxs-lookup"><span data-stu-id="92424-804">**C# Class**</span></span>

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


<span data-ttu-id="92424-805">**JSON**</span><span class="sxs-lookup"><span data-stu-id="92424-805">**JSON**</span></span>  

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



### <a name="linq-toosql-translation"></a><span data-ttu-id="92424-806">Traduction de tooSQL LINQ</span><span class="sxs-lookup"><span data-stu-id="92424-806">LINQ tooSQL translation</span></span>
<span data-ttu-id="92424-807">fournisseur de requêtes de base de données Cosmos Hello effectue un mappage de l’effort optimal à partir d’une requête LINQ dans une requête SQL de base de données Cosmos.</span><span class="sxs-lookup"><span data-stu-id="92424-807">hello Cosmos DB query provider performs a best effort mapping from a LINQ query into a Cosmos DB SQL query.</span></span> <span data-ttu-id="92424-808">Bonjour suivant description, nous supposons que lecteur de hello possède une connaissance élémentaire de LINQ.</span><span class="sxs-lookup"><span data-stu-id="92424-808">In hello following description, we assume hello reader has a basic familiarity of LINQ.</span></span>

<span data-ttu-id="92424-809">Tout d’abord, pour le système de type hello, nous prenons en charge tous les types primitifs JSON-types numériques, boolean, string et null.</span><span class="sxs-lookup"><span data-stu-id="92424-809">First, for hello type system, we support all JSON primitive types – numeric types, boolean, string, and null.</span></span> <span data-ttu-id="92424-810">Seuls ces types JSON sont pris en charge.</span><span class="sxs-lookup"><span data-stu-id="92424-810">Only these JSON types are supported.</span></span> <span data-ttu-id="92424-811">Hello après les expressions scalaires est prises en charge.</span><span class="sxs-lookup"><span data-stu-id="92424-811">hello following scalar expressions are supported.</span></span>

* <span data-ttu-id="92424-812">Des valeurs constantes, notamment des valeurs constantes des types de données primitifs hello au moment de hello hello requête est évaluée.</span><span class="sxs-lookup"><span data-stu-id="92424-812">Constant values – these include constant values of hello primitive data types at hello time hello query is evaluated.</span></span>
* <span data-ttu-id="92424-813">Expressions d’index de tableau de la propriété – ces expressions font référence de propriété toohello d’un objet ou un élément de tableau.</span><span class="sxs-lookup"><span data-stu-id="92424-813">Property/array index expressions – these expressions refer toohello property of an object or an array element.</span></span>
  
     <span data-ttu-id="92424-814">family.Id;    family.children[0].familyName;    family.children[0].grade;    family.children[n].grade; //n étant un entier</span><span class="sxs-lookup"><span data-stu-id="92424-814">family.Id;    family.children[0].familyName;    family.children[0].grade;    family.children[n].grade; //n is an int variable</span></span>
* <span data-ttu-id="92424-815">Expressions arithmétiques : elles incluent les expressions arithmétiques communes sur les valeurs numériques et booléennes.</span><span class="sxs-lookup"><span data-stu-id="92424-815">Arithmetic expressions - These include common arithmetic expressions on numerical and boolean values.</span></span> <span data-ttu-id="92424-816">Pour la liste complète de hello, consultez Spécification de SQL toohello.</span><span class="sxs-lookup"><span data-stu-id="92424-816">For hello complete list, refer toohello SQL specification.</span></span>
  
     <span data-ttu-id="92424-817">2 * family.children[0].grade;    x + y;</span><span class="sxs-lookup"><span data-stu-id="92424-817">2 * family.children[0].grade;    x + y;</span></span>
* <span data-ttu-id="92424-818">Expression de comparaison de chaîne, notamment les comparer une valeur de chaîne constante de chaîne valeur toosome.</span><span class="sxs-lookup"><span data-stu-id="92424-818">String comparison expression - these include comparing a string value toosome constant string value.</span></span>  
  
     <span data-ttu-id="92424-819">mother.familyName == "Smith";    child.givenName == s; //s étant une chaîne</span><span class="sxs-lookup"><span data-stu-id="92424-819">mother.familyName == "Smith";    child.givenName == s; //s is a string variable</span></span>
* <span data-ttu-id="92424-820">Expressions de création d'objet/tableau : ces expressions renvoient un objet de type de valeur composée ou de type anonyme ou un tableau de tels objets.</span><span class="sxs-lookup"><span data-stu-id="92424-820">Object/array creation expression - these expressions return an object of compound value type or anonymous type or an array of such objects.</span></span> <span data-ttu-id="92424-821">Ces valeurs peuvent être imbriquées.</span><span class="sxs-lookup"><span data-stu-id="92424-821">These values can be nested.</span></span>
  
     <span data-ttu-id="92424-822">new Parent { familyName = "Smith", givenName = "Joe" }; new { first = 1, second = 2 }; //type anonyme avec deux champs</span><span class="sxs-lookup"><span data-stu-id="92424-822">new Parent { familyName = "Smith", givenName = "Joe" }; new { first = 1, second = 2 }; //an anonymous type with two fields</span></span>              
     <span data-ttu-id="92424-823">new int[] { 3, child.grade, 5 };</span><span class="sxs-lookup"><span data-stu-id="92424-823">new int[] { 3, child.grade, 5 };</span></span>

### <span data-ttu-id="92424-824"><a id="SupportedLinqOperators"></a>Liste des opérateurs LINQ pris en charge</span><span class="sxs-lookup"><span data-stu-id="92424-824"><a id="SupportedLinqOperators"></a>List of supported LINQ operators</span></span>
<span data-ttu-id="92424-825">Voici une liste des opérateurs LINQ pris en charge dans le fournisseur LINQ de hello inclus avec hello DocumentDB .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="92424-825">Here is a list of supported LINQ operators in hello LINQ provider included with hello DocumentDB .NET SDK.</span></span>

* <span data-ttu-id="92424-826">**Sélectionnez**: Projections traduire toohello SQL SELECT, y compris la construction d’objet</span><span class="sxs-lookup"><span data-stu-id="92424-826">**Select**: Projections translate toohello SQL SELECT including object construction</span></span>
* <span data-ttu-id="92424-827">**Où**: filtres traduire toohello SQL WHERE et prend en charge la traduction entre & &, || et !</span><span class="sxs-lookup"><span data-stu-id="92424-827">**Where**: Filters translate toohello SQL WHERE, and support translation between && , || and !</span></span> <span data-ttu-id="92424-828">opérateurs de toohello SQL</span><span class="sxs-lookup"><span data-stu-id="92424-828">toohello SQL operators</span></span>
* <span data-ttu-id="92424-829">**SelectMany**: autorise le déroulement de la clause de jointure SQL toohello tableaux.</span><span class="sxs-lookup"><span data-stu-id="92424-829">**SelectMany**: Allows unwinding of arrays toohello SQL JOIN clause.</span></span> <span data-ttu-id="92424-830">Peut être toofilter d’expressions toochain/imbrication utilisés sur les éléments de tableau</span><span class="sxs-lookup"><span data-stu-id="92424-830">Can be used toochain/nest expressions toofilter on array elements</span></span>
* <span data-ttu-id="92424-831">**OrderBy et OrderByDescending**: traduit tooORDER par ordre croissant ou décroissant</span><span class="sxs-lookup"><span data-stu-id="92424-831">**OrderBy and OrderByDescending**: Translates tooORDER BY ascending/descending</span></span>
* <span data-ttu-id="92424-832">Les opérateurs **Count**, **Sum**, **Min**, **Max** et **Average** pour l’agrégation, et leurs équivalents asynchrones **CountAsync**, **SumAsync**, **MinAsync**, **MaxAsync** et **AverageAsync**.</span><span class="sxs-lookup"><span data-stu-id="92424-832">**Count**, **Sum**, **Min**, **Max**, and **Average** operators for aggregation, and their async equivalents **CountAsync**, **SumAsync**, **MinAsync**, **MaxAsync**, and **AverageAsync**.</span></span>
* <span data-ttu-id="92424-833">**CompareTo**: traduit toorange comparaisons.</span><span class="sxs-lookup"><span data-stu-id="92424-833">**CompareTo**: Translates toorange comparisons.</span></span> <span data-ttu-id="92424-834">Généralement utilisés pour les chaînes car ils ne sont pas comparables dans .NET</span><span class="sxs-lookup"><span data-stu-id="92424-834">Commonly used for strings since they’re not comparable in .NET</span></span>
* <span data-ttu-id="92424-835">**Prendre**: traduit toohello SQL TOP pour limiter les résultats d’une requête</span><span class="sxs-lookup"><span data-stu-id="92424-835">**Take**: Translates toohello SQL TOP for limiting results from a query</span></span>
* <span data-ttu-id="92424-836">**Fonctions mathématiques**: prend en charge la traduction à partir de. Abs, Acos, Asin de NET, Atan, Ceiling, Cos, Exp, Floor, journal, Log10, Pow, Round, signe, Sin, Sqrt, Tan, tronquer des fonctions intégrées de toohello équivalentes SQL.</span><span class="sxs-lookup"><span data-stu-id="92424-836">**Math Functions**: Supports translation from .NET’s Abs, Acos, Asin, Atan, Ceiling, Cos, Exp, Floor, Log, Log10, Pow, Round, Sign, Sin, Sqrt, Tan, Truncate toohello equivalent SQL built-in functions.</span></span>
* <span data-ttu-id="92424-837">**Fonctions de chaîne**: prend en charge la traduction à partir de. Concat, Contains, EndsWith de NET, IndexOf, nombre, ToLower, TrimStart, Replace, inverse, TrimEnd, StartsWith, SubString, ToUpper toohello équivalent SQL des fonctions intégrées.</span><span class="sxs-lookup"><span data-stu-id="92424-837">**String Functions**: Supports translation from .NET’s Concat, Contains, EndsWith, IndexOf, Count, ToLower, TrimStart, Replace, Reverse, TrimEnd, StartsWith, SubString, ToUpper toohello equivalent SQL built-in functions.</span></span>
* <span data-ttu-id="92424-838">**Fonctions de tableau**: prend en charge la traduction à partir de. Concat, Contains et nombre toohello équivalent SQL fonctions intégrées de NET.</span><span class="sxs-lookup"><span data-stu-id="92424-838">**Array Functions**: Supports translation from .NET’s Concat, Contains, and Count toohello equivalent SQL built-in functions.</span></span>
* <span data-ttu-id="92424-839">**Fonctions d’Extension Geospatial**: prend en charge la traduction à partir de la Distance, dans, IsValid, les méthodes stub et IsValidDetailed toohello équivalent SQL des fonctions intégrées.</span><span class="sxs-lookup"><span data-stu-id="92424-839">**Geospatial Extension Functions**: Supports translation from stub methods Distance, Within, IsValid, and IsValidDetailed toohello equivalent SQL built-in functions.</span></span>
* <span data-ttu-id="92424-840">**Extension de fonction définie par l’utilisateur**: traduction prend en charge à partir de hello stub de méthode UserDefinedFunctionProvider.Invoke toohello correspondante définie par l’utilisateur (fonction).</span><span class="sxs-lookup"><span data-stu-id="92424-840">**User-Defined Function Extension Function**: Supports translation from hello stub method UserDefinedFunctionProvider.Invoke toohello corresponding user-defined function.</span></span>
* <span data-ttu-id="92424-841">**Divers**: prend en charge la traduction de hello coalesce et des opérateurs conditionnels.</span><span class="sxs-lookup"><span data-stu-id="92424-841">**Miscellaneous**: Supports translation of hello coalesce and conditional operators.</span></span> <span data-ttu-id="92424-842">Peut traduire Contains tooString CONTAINS, ARRAY_CONTAINS ou hello SQL IN selon le contexte.</span><span class="sxs-lookup"><span data-stu-id="92424-842">Can translate Contains tooString CONTAINS, ARRAY_CONTAINS, or hello SQL IN depending on context.</span></span>

### <a name="sql-query-operators"></a><span data-ttu-id="92424-843">Opérateurs de requête SQL</span><span class="sxs-lookup"><span data-stu-id="92424-843">SQL query operators</span></span>
<span data-ttu-id="92424-844">Voici quelques exemples qui illustrent comment certains des opérateurs de requête LINQ standards hello sont convertis vers le bas des requêtes de base de données tooCosmos.</span><span class="sxs-lookup"><span data-stu-id="92424-844">Here are some examples that illustrate how some of hello standard LINQ query operators are translated down tooCosmos DB queries.</span></span>

#### <a name="select-operator"></a><span data-ttu-id="92424-845">Opérateur Select</span><span class="sxs-lookup"><span data-stu-id="92424-845">Select Operator</span></span>
<span data-ttu-id="92424-846">syntaxe de Hello est `input.Select(x => f(x))`, où `f` est une expression scalaire.</span><span class="sxs-lookup"><span data-stu-id="92424-846">hello syntax is `input.Select(x => f(x))`, where `f` is a scalar expression.</span></span>

<span data-ttu-id="92424-847">**Expression Lambda LINQ**</span><span class="sxs-lookup"><span data-stu-id="92424-847">**LINQ lambda expression**</span></span>

    input.Select(family => family.parents[0].familyName);

<span data-ttu-id="92424-848">**SQL**</span><span class="sxs-lookup"><span data-stu-id="92424-848">**SQL**</span></span> 

    SELECT VALUE f.parents[0].familyName
    FROM Families f



<span data-ttu-id="92424-849">**Expression Lambda LINQ**</span><span class="sxs-lookup"><span data-stu-id="92424-849">**LINQ lambda expression**</span></span>

    input.Select(family => family.children[0].grade + c); // c is an int variable


<span data-ttu-id="92424-850">**SQL**</span><span class="sxs-lookup"><span data-stu-id="92424-850">**SQL**</span></span> 

    SELECT VALUE f.children[0].grade + c
    FROM Families f 



<span data-ttu-id="92424-851">**Expression Lambda LINQ**</span><span class="sxs-lookup"><span data-stu-id="92424-851">**LINQ lambda expression**</span></span>

    input.Select(family => new
    {
        name = family.children[0].familyName,
        grade = family.children[0].grade + 3
    });


<span data-ttu-id="92424-852">**SQL**</span><span class="sxs-lookup"><span data-stu-id="92424-852">**SQL**</span></span> 

    SELECT VALUE {"name":f.children[0].familyName, 
                  "grade": f.children[0].grade + 3 }
    FROM Families f



#### <a name="selectmany-operator"></a><span data-ttu-id="92424-853">Opérateur SelectMany</span><span class="sxs-lookup"><span data-stu-id="92424-853">SelectMany operator</span></span>
<span data-ttu-id="92424-854">syntaxe de Hello est `input.SelectMany(x => f(x))`, où `f` est une expression scalaire qui retourne un type de collection.</span><span class="sxs-lookup"><span data-stu-id="92424-854">hello syntax is `input.SelectMany(x => f(x))`, where `f` is a scalar expression that returns a collection type.</span></span>

<span data-ttu-id="92424-855">**Expression Lambda LINQ**</span><span class="sxs-lookup"><span data-stu-id="92424-855">**LINQ lambda expression**</span></span>

    input.SelectMany(family => family.children);

<span data-ttu-id="92424-856">**SQL**</span><span class="sxs-lookup"><span data-stu-id="92424-856">**SQL**</span></span> 

    SELECT VALUE child
    FROM child IN Families.children



#### <a name="where-operator"></a><span data-ttu-id="92424-857">Opérateur Where</span><span class="sxs-lookup"><span data-stu-id="92424-857">Where operator</span></span>
<span data-ttu-id="92424-858">syntaxe de Hello est `input.Where(x => f(x))`, où `f` est une expression scalaire, qui retourne une valeur booléenne.</span><span class="sxs-lookup"><span data-stu-id="92424-858">hello syntax is `input.Where(x => f(x))`, where `f` is a scalar expression, which returns a Boolean value.</span></span>

<span data-ttu-id="92424-859">**Expression Lambda LINQ**</span><span class="sxs-lookup"><span data-stu-id="92424-859">**LINQ lambda expression**</span></span>

    input.Where(family=> family.parents[0].familyName == "Smith");

<span data-ttu-id="92424-860">**SQL**</span><span class="sxs-lookup"><span data-stu-id="92424-860">**SQL**</span></span> 

    SELECT *
    FROM Families f
    WHERE f.parents[0].familyName = "Smith" 



<span data-ttu-id="92424-861">**Expression Lambda LINQ**</span><span class="sxs-lookup"><span data-stu-id="92424-861">**LINQ lambda expression**</span></span>

    input.Where(
        family => family.parents[0].familyName == "Smith" && 
        family.children[0].grade < 3);

<span data-ttu-id="92424-862">**SQL**</span><span class="sxs-lookup"><span data-stu-id="92424-862">**SQL**</span></span> 

    SELECT *
    FROM Families f
    WHERE f.parents[0].familyName = "Smith"
    AND f.children[0].grade < 3


### <a name="composite-sql-queries"></a><span data-ttu-id="92424-863">Requêtes SQL composites</span><span class="sxs-lookup"><span data-stu-id="92424-863">Composite SQL queries</span></span>
<span data-ttu-id="92424-864">Hello ci-dessus opérateurs peut être tooform composer des requêtes plus puissantes.</span><span class="sxs-lookup"><span data-stu-id="92424-864">hello above operators can be composed tooform more powerful queries.</span></span> <span data-ttu-id="92424-865">Étant donné que Cosmos DB prend en charge les collections imbriquées, composition de hello peut être concaténée ou imbriquée.</span><span class="sxs-lookup"><span data-stu-id="92424-865">Since Cosmos DB supports nested collections, hello composition can either be concatenated or nested.</span></span>

#### <a name="concatenation"></a><span data-ttu-id="92424-866">Concaténation</span><span class="sxs-lookup"><span data-stu-id="92424-866">Concatenation</span></span>
<span data-ttu-id="92424-867">syntaxe de Hello est `input(.|.SelectMany())(.Select()|.Where())*`.</span><span class="sxs-lookup"><span data-stu-id="92424-867">hello syntax is `input(.|.SelectMany())(.Select()|.Where())*`.</span></span> <span data-ttu-id="92424-868">Une requête concaténée peut commencer par une requête `SelectMany` facultative suivie de plusieurs opérateurs `Select` ou `Where`.</span><span class="sxs-lookup"><span data-stu-id="92424-868">A concatenated query can start with an optional `SelectMany` query followed by multiple `Select` or `Where` operators.</span></span>

<span data-ttu-id="92424-869">**Expression Lambda LINQ**</span><span class="sxs-lookup"><span data-stu-id="92424-869">**LINQ lambda expression**</span></span>

    input.Select(family=>family.parents[0])
        .Where(familyName == "Smith");

<span data-ttu-id="92424-870">**SQL**</span><span class="sxs-lookup"><span data-stu-id="92424-870">**SQL**</span></span>

    SELECT *
    FROM Families f
    WHERE f.parents[0].familyName = "Smith"



<span data-ttu-id="92424-871">**Expression Lambda LINQ**</span><span class="sxs-lookup"><span data-stu-id="92424-871">**LINQ lambda expression**</span></span>

    input.Where(family => family.children[0].grade > 3)
        .Select(family => family.parents[0].familyName);

<span data-ttu-id="92424-872">**SQL**</span><span class="sxs-lookup"><span data-stu-id="92424-872">**SQL**</span></span> 

    SELECT VALUE f.parents[0].familyName
    FROM Families f
    WHERE f.children[0].grade > 3



<span data-ttu-id="92424-873">**Expression Lambda LINQ**</span><span class="sxs-lookup"><span data-stu-id="92424-873">**LINQ lambda expression**</span></span>

    input.Select(family => new { grade=family.children[0].grade}).
        Where(anon=> anon.grade < 3);

<span data-ttu-id="92424-874">**SQL**</span><span class="sxs-lookup"><span data-stu-id="92424-874">**SQL**</span></span> 

    SELECT *
    FROM Families f
    WHERE ({grade: f.children[0].grade}.grade > 3)



<span data-ttu-id="92424-875">**Expression Lambda LINQ**</span><span class="sxs-lookup"><span data-stu-id="92424-875">**LINQ lambda expression**</span></span>

    input.SelectMany(family => family.parents)
        .Where(parent => parents.familyName == "Smith");

<span data-ttu-id="92424-876">**SQL**</span><span class="sxs-lookup"><span data-stu-id="92424-876">**SQL**</span></span> 

    SELECT *
    FROM p IN Families.parents
    WHERE p.familyName = "Smith"



#### <a name="nesting"></a><span data-ttu-id="92424-877">Imbrication</span><span class="sxs-lookup"><span data-stu-id="92424-877">Nesting</span></span>
<span data-ttu-id="92424-878">syntaxe de Hello est `input.SelectMany(x=>x.Q())` où Q est un `Select`, `SelectMany`, ou `Where` opérateur.</span><span class="sxs-lookup"><span data-stu-id="92424-878">hello syntax is `input.SelectMany(x=>x.Q())` where Q is a `Select`, `SelectMany`, or `Where` operator.</span></span>

<span data-ttu-id="92424-879">Dans une requête imbriquée, requête interne de hello est élément tooeach appliqué de la collection externe de hello.</span><span class="sxs-lookup"><span data-stu-id="92424-879">In a nested query, hello inner query is applied tooeach element of hello outer collection.</span></span> <span data-ttu-id="92424-880">Une fonctionnalité importante est que cette requête interne hello peut faire référence toohello des champs d’éléments de hello dans la collection externe de hello telles que les jointures réflexives.</span><span class="sxs-lookup"><span data-stu-id="92424-880">One important feature is that hello inner query can refer toohello fields of hello elements in hello outer collection like self-joins.</span></span>

<span data-ttu-id="92424-881">**Expression Lambda LINQ**</span><span class="sxs-lookup"><span data-stu-id="92424-881">**LINQ lambda expression**</span></span>

    input.SelectMany(family=> 
        family.parents.Select(p => p.familyName));

<span data-ttu-id="92424-882">**SQL**</span><span class="sxs-lookup"><span data-stu-id="92424-882">**SQL**</span></span> 

    SELECT VALUE p.familyName
    FROM Families f
    JOIN p IN f.parents


<span data-ttu-id="92424-883">**Expression Lambda LINQ**</span><span class="sxs-lookup"><span data-stu-id="92424-883">**LINQ lambda expression**</span></span>

    input.SelectMany(family => 
        family.children.Where(child => child.familyName == "Jeff"));

<span data-ttu-id="92424-884">**SQL**</span><span class="sxs-lookup"><span data-stu-id="92424-884">**SQL**</span></span> 

    SELECT *
    FROM Families f
    JOIN c IN f.children
    WHERE c.familyName = "Jeff"



<span data-ttu-id="92424-885">**Expression Lambda LINQ**</span><span class="sxs-lookup"><span data-stu-id="92424-885">**LINQ lambda expression**</span></span>

    input.SelectMany(family => family.children.Where(
        child => child.familyName == family.parents[0].familyName));

<span data-ttu-id="92424-886">**SQL**</span><span class="sxs-lookup"><span data-stu-id="92424-886">**SQL**</span></span> 

    SELECT *
    FROM Families f
    JOIN c IN f.children
    WHERE c.familyName = f.parents[0].familyName


## <span data-ttu-id="92424-887"><a id="ExecutingSqlQueries"></a>Exécution de requêtes SQL</span><span class="sxs-lookup"><span data-stu-id="92424-887"><a id="ExecutingSqlQueries"></a>Executing SQL queries</span></span>
<span data-ttu-id="92424-888">Cosmos DB expose les ressources par le biais d’une API REST qui peut être appelée par n’importe quel langage capable de créer des requêtes HTTP/HTTPS.</span><span class="sxs-lookup"><span data-stu-id="92424-888">Cosmos DB exposes resources through a REST API that can be called by any language capable of making HTTP/HTTPS requests.</span></span> <span data-ttu-id="92424-889">Par ailleurs, Cosmos DB propose des bibliothèques de programmation pour plusieurs langages populaires comme .NET, Node.js, JavaScript et Python.</span><span class="sxs-lookup"><span data-stu-id="92424-889">Additionally, Cosmos DB offers programming libraries for several popular languages like .NET, Node.js, JavaScript, and Python.</span></span> <span data-ttu-id="92424-890">Hello API REST et hello différentes bibliothèques prennent en charge interrogation via SQL.</span><span class="sxs-lookup"><span data-stu-id="92424-890">hello REST API and hello various libraries all support querying through SQL.</span></span> <span data-ttu-id="92424-891">Hello .NET SDK prend en charge LINQ interrogation en outre tooSQL.</span><span class="sxs-lookup"><span data-stu-id="92424-891">hello .NET SDK supports LINQ querying in addition tooSQL.</span></span>

<span data-ttu-id="92424-892">Hello suivant exemples montrent comment toocreate une requête et l’envoyer par rapport à un compte de base de données de base de données Cosmos.</span><span class="sxs-lookup"><span data-stu-id="92424-892">hello following examples show how toocreate a query and submit it against a Cosmos DB database account.</span></span>

### <span data-ttu-id="92424-893"><a id="RestAPI"></a>API REST</span><span class="sxs-lookup"><span data-stu-id="92424-893"><a id="RestAPI"></a>REST API</span></span>
<span data-ttu-id="92424-894">Cosmos DB fournit un modèle de programmation RESTful ouvert sur HTTP.</span><span class="sxs-lookup"><span data-stu-id="92424-894">Cosmos DB offers an open RESTful programming model over HTTP.</span></span> <span data-ttu-id="92424-895">Vous pouvez approvisionner vos comptes de bases de données en utilisant un abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="92424-895">Database accounts can be provisioned using an Azure subscription.</span></span> <span data-ttu-id="92424-896">modèle de ressource de base de données Cosmos Hello se compose d’un ensemble de ressources sous un compte de base de données, chacune d’elles étant adressable en utilisant un URI logique et stable.</span><span class="sxs-lookup"><span data-stu-id="92424-896">hello Cosmos DB resource model consists of a set of resources under a database account, each  of which is addressable using a logical and stable URI.</span></span> <span data-ttu-id="92424-897">Un ensemble de ressources est tooas auxquels un flux dans ce document.</span><span class="sxs-lookup"><span data-stu-id="92424-897">A set of resources is referred tooas a feed in this document.</span></span> <span data-ttu-id="92424-898">Un compte de base de données se compose d'un ensemble de bases de données. Chacune d'elles contient plusieurs collections et chaque collection contient des documents, des fonctions définies par l'utilisateur et d'autres types de ressources.</span><span class="sxs-lookup"><span data-stu-id="92424-898">A database account consists of a set of databases, each containing multiple collections, each of which in-turn contain documents, UDFs, and other resource types.</span></span>

<span data-ttu-id="92424-899">modèle d’interaction de base Hello avec ces ressources est via les verbes hello HTTP GET, PUT, POST et DELETE avec leur interprétation standard.</span><span class="sxs-lookup"><span data-stu-id="92424-899">hello basic interaction model with these resources is through hello HTTP verbs GET, PUT, POST, and DELETE with their standard interpretation.</span></span> <span data-ttu-id="92424-900">verbe POST de Hello est utilisé pour la création d’une nouvelle ressource, l’exécution d’une procédure stockée ou pour l’émission d’une requête de base de données Cosmos.</span><span class="sxs-lookup"><span data-stu-id="92424-900">hello POST verb is used for creation of a new resource, for executing a stored procedure or for issuing a Cosmos DB query.</span></span> <span data-ttu-id="92424-901">Les requêtes sont toujours des opérations en lecture seule sans effets secondaires.</span><span class="sxs-lookup"><span data-stu-id="92424-901">Queries are always read-only operations with no side-effects.</span></span>

<span data-ttu-id="92424-902">Hello exemples suivants montrent un billet pour une requête d’API DocumentDB adressée à une collection contenant hello deux exemples de documents que nous avons examiné jusqu'à présent.</span><span class="sxs-lookup"><span data-stu-id="92424-902">hello following examples show a POST for a DocumentDB API query made against a collection containing hello two sample documents we've reviewed so far.</span></span> <span data-ttu-id="92424-903">requête de Hello a un filtre simple sur la propriété de nom hello JSON.</span><span class="sxs-lookup"><span data-stu-id="92424-903">hello query has a simple filter on hello JSON name property.</span></span> <span data-ttu-id="92424-904">Notez que hello hello `x-ms-documentdb-isquery` et Content-Type : `application/query+json` toodenote en-têtes qui hello opération est une requête.</span><span class="sxs-lookup"><span data-stu-id="92424-904">Note hello use of hello `x-ms-documentdb-isquery` and Content-Type: `application/query+json` headers toodenote that hello operation is a query.</span></span>

<span data-ttu-id="92424-905">**Requête**</span><span class="sxs-lookup"><span data-stu-id="92424-905">**Request**</span></span>

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


<span data-ttu-id="92424-906">**Résultats**</span><span class="sxs-lookup"><span data-stu-id="92424-906">**Results**</span></span>

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


<span data-ttu-id="92424-907">Hello deuxième exemple montre une requête plus complexe qui retourne plusieurs résultats à partir de la jointure de hello.</span><span class="sxs-lookup"><span data-stu-id="92424-907">hello second example shows a more complex query that returns multiple results from hello join.</span></span>

<span data-ttu-id="92424-908">**Requête**</span><span class="sxs-lookup"><span data-stu-id="92424-908">**Request**</span></span>

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


<span data-ttu-id="92424-909">**Résultats**</span><span class="sxs-lookup"><span data-stu-id="92424-909">**Results**</span></span>

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


<span data-ttu-id="92424-910">Si les résultats d’une requête ne peut pas tenir dans une seule page de résultats, puis hello API REST retourne un jeton de continuation via hello `x-ms-continuation-token` en-tête de réponse.</span><span class="sxs-lookup"><span data-stu-id="92424-910">If a query's results cannot fit within a single page of results, then hello REST API returns a continuation token through hello `x-ms-continuation-token` response header.</span></span> <span data-ttu-id="92424-911">Les clients peuvent paginer les résultats en incluant l’en-tête de hello dans les résultats suivants.</span><span class="sxs-lookup"><span data-stu-id="92424-911">Clients can paginate results by including hello header in subsequent results.</span></span> <span data-ttu-id="92424-912">nombre de Hello de résultats par page peut également être contrôlé via hello `x-ms-max-item-count` en-tête du numéro.</span><span class="sxs-lookup"><span data-stu-id="92424-912">hello number of results per page can also be controlled through hello `x-ms-max-item-count` number header.</span></span> <span data-ttu-id="92424-913">Si la requête spécifiée de hello possède une fonction d’agrégation comme `COUNT`, puis page hello de la requête peut retourner une valeur de partiellement agrégée sur la page de résultats hello.</span><span class="sxs-lookup"><span data-stu-id="92424-913">If hello specified query has an aggregation function like `COUNT`, then hello query page may return a partially aggregated value over hello page of results.</span></span> <span data-ttu-id="92424-914">les clients de Hello doit effectuer une agrégation de second niveau sur ces résultats tooproduce hello finale des résultats, par exemple, somme des nombres hello retournées dans le nombre total de hello des pages individuelles tooreturn hello.</span><span class="sxs-lookup"><span data-stu-id="92424-914">hello clients must perform a second-level aggregation over these results tooproduce hello final results, for example, sum over hello counts returned in hello individual pages tooreturn hello total count.</span></span>

<span data-ttu-id="92424-915">stratégie de la cohérence des données toomanage hello pour les requêtes, utilisez hello `x-ms-consistency-level` en-tête comme toutes les demandes d’API REST.</span><span class="sxs-lookup"><span data-stu-id="92424-915">toomanage hello data consistency policy for queries, use hello `x-ms-consistency-level` header like all REST API requests.</span></span> <span data-ttu-id="92424-916">Par souci de cohérence de session, il est plus récente hello d’écho tooalso requis `x-ms-session-token` en-tête Cookie demande de requête hello.</span><span class="sxs-lookup"><span data-stu-id="92424-916">For session consistency, it is required tooalso echo hello latest `x-ms-session-token` Cookie header in hello query request.</span></span> <span data-ttu-id="92424-917">Hello stratégie d’indexation de collection interrogée peut également influer sur la cohérence de hello des résultats de la requête.</span><span class="sxs-lookup"><span data-stu-id="92424-917">hello queried collection's indexing policy can also influence hello consistency of query results.</span></span> <span data-ttu-id="92424-918">La valeur par défaut hello les paramètres de stratégie d’indexation, pour les collections hello index est toujours en cours avec le contenu du document hello et cohérence hello choisie pour les données de résultat de requête.</span><span class="sxs-lookup"><span data-stu-id="92424-918">With hello default indexing policy settings, for collections hello index is always current with hello document contents and query results match hello consistency chosen for data.</span></span> <span data-ttu-id="92424-919">Si hello stratégie d’indexation est tooLazy souple, requêtes peuvent renvoyer des résultats obsolètes.</span><span class="sxs-lookup"><span data-stu-id="92424-919">If hello indexing policy is relaxed tooLazy, then queries can return stale results.</span></span> <span data-ttu-id="92424-920">Pour en savoir plus, voir [Niveaux de cohérence des données paramétrables dans Azure Cosmos DB][consistency-levels].</span><span class="sxs-lookup"><span data-stu-id="92424-920">For more information, see [Azure Cosmos DB Consistency Levels][consistency-levels].</span></span>

<span data-ttu-id="92424-921">Si la stratégie d’indexation hello configuré sur la collection de hello ne peut pas prendre en charge la requête spécifiée de hello, le serveur de base de données Azure Cosmos hello retourne 400 » demande incorrecte ».</span><span class="sxs-lookup"><span data-stu-id="92424-921">If hello configured indexing policy on hello collection cannot support hello specified query, hello Azure Cosmos DB server returns 400 "Bad Request".</span></span> <span data-ttu-id="92424-922">Ce code est renvoyé pour les requêtes de plage par rapport aux chemins d'accès configurés pour les recherches (d'égalité) de hachage et pour les chemins d'accès explicitement exclus de l'indexation.</span><span class="sxs-lookup"><span data-stu-id="92424-922">This is returned for range queries against paths configured for hash (equality) lookups, and for paths explicitly excluded from indexing.</span></span> <span data-ttu-id="92424-923">Hello `x-ms-documentdb-query-enable-scan` en-tête peut être spécifié tooallow hello requête tooperform une analyse lorsqu’un index n’est pas disponible.</span><span class="sxs-lookup"><span data-stu-id="92424-923">hello `x-ms-documentdb-query-enable-scan` header can be specified tooallow hello query tooperform a scan when an index is not available.</span></span>

<span data-ttu-id="92424-924">Vous pouvez obtenir les métriques détaillées sur l’exécution des requêtes en définissant `x-ms-documentdb-populatequerymetrics` en-tête trop`True`.</span><span class="sxs-lookup"><span data-stu-id="92424-924">You can get detailed metrics on query execution by setting `x-ms-documentdb-populatequerymetrics` header too`True`.</span></span> <span data-ttu-id="92424-925">Pour en savoir plus, consultez la section relative aux [métriques de requête SQL pour l’API DocumentDB Azure Cosmos DB](documentdb-sql-query-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="92424-925">For more information, see [SQL query metrics for Azure Cosmos DB DocumentDB API](documentdb-sql-query-metrics.md).</span></span>

### <span data-ttu-id="92424-926"><a id="DotNetSdk"></a>Kit SDK C# (.NET)</span><span class="sxs-lookup"><span data-stu-id="92424-926"><a id="DotNetSdk"></a>C# (.NET) SDK</span></span>
<span data-ttu-id="92424-927">Hello .NET SDK prend en charge LINQ et SQL interrogation.</span><span class="sxs-lookup"><span data-stu-id="92424-927">hello .NET SDK supports both LINQ and SQL querying.</span></span> <span data-ttu-id="92424-928">Hello suivant montre comment la requête de filtre simple tooperform hello introduit précédemment dans ce document.</span><span class="sxs-lookup"><span data-stu-id="92424-928">hello following example shows how tooperform hello simple filter query introduced earlier in this document.</span></span>

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


<span data-ttu-id="92424-929">Cet exemple compare l'égalité de deux propriétés dans chaque document et utilise des projections anonymes.</span><span class="sxs-lookup"><span data-stu-id="92424-929">This sample compares two properties for equality within each document and uses anonymous projections.</span></span> 

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


<span data-ttu-id="92424-930">Hello l’exemple suivant montre des jointures, exprimées par LINQ SelectMany.</span><span class="sxs-lookup"><span data-stu-id="92424-930">hello next sample shows joins, expressed through LINQ SelectMany.</span></span>

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



<span data-ttu-id="92424-931">client .NET de Hello itère automatiquement toutes les pages hello des résultats de requête dans les blocs de foreach hello comme indiqué ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="92424-931">hello .NET client automatically iterates through all hello pages of query results in hello foreach blocks as shown above.</span></span> <span data-ttu-id="92424-932">requête Hello options introduites dans la section de l’API REST de hello sont également disponibles dans hello .NET SDK à l’aide de hello `FeedOptions` et `FeedResponse` classes Bonjour CreateDocumentQuery méthode.</span><span class="sxs-lookup"><span data-stu-id="92424-932">hello query options introduced in hello REST API section are also available in hello .NET SDK using hello `FeedOptions` and `FeedResponse` classes in hello CreateDocumentQuery method.</span></span> <span data-ttu-id="92424-933">nombre de Hello de pages peut être contrôlé à l’aide de hello `MaxItemCount` paramètre.</span><span class="sxs-lookup"><span data-stu-id="92424-933">hello number of pages can be controlled using hello `MaxItemCount` setting.</span></span> 

<span data-ttu-id="92424-934">Vous pouvez explicitement contrôler la pagination en créant `IDocumentQueryable` à l’aide de hello `IQueryable` objet, puis en lisant le` ResponseContinuationToken` valeurs et en les passant sauvegarder en tant que `RequestContinuationToken` dans `FeedOptions`.</span><span class="sxs-lookup"><span data-stu-id="92424-934">You can also explicitly control paging by creating `IDocumentQueryable` using hello `IQueryable` object, then by reading the` ResponseContinuationToken` values and passing them back as `RequestContinuationToken` in `FeedOptions`.</span></span> <span data-ttu-id="92424-935">`EnableScanInQuery`peuvent être les analyses de tooenable ensemble lors de la requête de hello ne peut pas être pris en charge par la stratégie d’indexation hello configuré.</span><span class="sxs-lookup"><span data-stu-id="92424-935">`EnableScanInQuery` can be set tooenable scans when hello query cannot be supported by hello configured indexing policy.</span></span> <span data-ttu-id="92424-936">Pour les collections partitionnées, vous pouvez utiliser `PartitionKey` requête de hello toorun par rapport à une seule partition (bien que Cosmos DB peut extraire automatiquement ce texte de requête hello), et `EnableCrossPartitionQuery` exécuter des requêtes de toorun qui peuvent nécessiter une toobe sur plusieurs partitions.</span><span class="sxs-lookup"><span data-stu-id="92424-936">For partitioned collections, you can use `PartitionKey` toorun hello query against a single partition (though Cosmos DB can automatically extract this from hello query text), and `EnableCrossPartitionQuery` toorun queries that may need toobe run against multiple partitions.</span></span> 

<span data-ttu-id="92424-937">Consultez trop[exemples Azure Cosmos DB .NET](https://github.com/Azure/azure-documentdb-net) pour plus d’exemples contenant des requêtes.</span><span class="sxs-lookup"><span data-stu-id="92424-937">Refer too[Azure Cosmos DB .NET samples](https://github.com/Azure/azure-documentdb-net) for more samples containing queries.</span></span> 

### <span data-ttu-id="92424-938"><a id="JavaScriptServerSideApi"></a>API JavaScript côté serveur</span><span class="sxs-lookup"><span data-stu-id="92424-938"><a id="JavaScriptServerSideApi"></a>JavaScript server-side API</span></span>
<span data-ttu-id="92424-939">COSMOS DB fournit un modèle de programmation pour l’exécution de la logique d’application basée sur JavaScript directement sur des collections de hello à l’aide de procédures stockées et les déclencheurs.</span><span class="sxs-lookup"><span data-stu-id="92424-939">Cosmos DB provides a programming model for executing JavaScript based application logic directly on hello collections using stored procedures and triggers.</span></span> <span data-ttu-id="92424-940">logique de JavaScript Hello inscrite à un niveau de la collection peut alors émettre des opérations de base de données sur les opérations de hello sur des documents de hello Hello étant donné la collection.</span><span class="sxs-lookup"><span data-stu-id="92424-940">hello JavaScript logic registered at a collection level can then issue database operations on hello operations on hello documents of hello given collection.</span></span> <span data-ttu-id="92424-941">Ces opérations sont encapsulées dans les transactions ACID ambiantes.</span><span class="sxs-lookup"><span data-stu-id="92424-941">These operations are wrapped in ambient ACID transactions.</span></span>

<span data-ttu-id="92424-942">Hello suivant montre comment queryDocuments de hello toouse dans hello JavaScript server API toomake les requêtes provenant à l’intérieur des procédures stockées et déclencheurs.</span><span class="sxs-lookup"><span data-stu-id="92424-942">hello following example shows how toouse hello queryDocuments in hello JavaScript server API toomake queries from inside stored procedures and triggers.</span></span>

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

                        // Replace hello author name for all documents that satisfied hello query.
                        for (var i = 0; i < matchingDocuments.length; i++) {
                            matchingDocuments[i].author = "George R. R. Martin";
                            // we don't need tooexecute a callback because they are in parallel
                            collectionManager.replaceDocument(matchingDocuments[i]._self,
                                matchingDocuments[i]);
                        }
                    })
            });
    }

## <span data-ttu-id="92424-943"><a id="References"></a>Références</span><span class="sxs-lookup"><span data-stu-id="92424-943"><a id="References"></a>References</span></span>
1. <span data-ttu-id="92424-944">[Introduction tooAzure Cosmos DB][introduction]</span><span class="sxs-lookup"><span data-stu-id="92424-944">[Introduction tooAzure Cosmos DB][introduction]</span></span>
2. [<span data-ttu-id="92424-945">Spécification SQL Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="92424-945">Azure Cosmos DB SQL specification</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=510612)
3. [<span data-ttu-id="92424-946">Exemples .NET Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="92424-946">Azure Cosmos DB .NET samples</span></span>](https://github.com/Azure/azure-documentdb-net)
4. <span data-ttu-id="92424-947">[Niveaux de cohérence de base Azure Cosmos DB][consistency-levels]</span><span class="sxs-lookup"><span data-stu-id="92424-947">[Azure Cosmos DB Consistency Levels][consistency-levels]</span></span>
5. <span data-ttu-id="92424-948">ANSI SQL 2011 [http://www.iso.org/iso/iso_catalogue/catalogue_tc/catalogue_detail.htm?csnumber=53681](http://www.iso.org/iso/iso_catalogue/catalogue_tc/catalogue_detail.htm?csnumber=53681)</span><span class="sxs-lookup"><span data-stu-id="92424-948">ANSI SQL 2011 [http://www.iso.org/iso/iso_catalogue/catalogue_tc/catalogue_detail.htm?csnumber=53681](http://www.iso.org/iso/iso_catalogue/catalogue_tc/catalogue_detail.htm?csnumber=53681)</span></span>
6. <span data-ttu-id="92424-949">JSON [http://json.org/](http://json.org/)</span><span class="sxs-lookup"><span data-stu-id="92424-949">JSON [http://json.org/](http://json.org/)</span></span>
7. <span data-ttu-id="92424-950">Spécification Javascript [http://www.ecma-international.org/publications/standards/Ecma-262.htm](http://www.ecma-international.org/publications/standards/Ecma-262.htm)</span><span class="sxs-lookup"><span data-stu-id="92424-950">Javascript Specification [http://www.ecma-international.org/publications/standards/Ecma-262.htm](http://www.ecma-international.org/publications/standards/Ecma-262.htm)</span></span> 
8. <span data-ttu-id="92424-951">LINQ [http://msdn.microsoft.com/library/bb308959.aspx](http://msdn.microsoft.com/library/bb308959.aspx)</span><span class="sxs-lookup"><span data-stu-id="92424-951">LINQ [http://msdn.microsoft.com/library/bb308959.aspx](http://msdn.microsoft.com/library/bb308959.aspx)</span></span> 
9. <span data-ttu-id="92424-952">Techniques d’évaluation des requêtes pour les bases de données volumineuses [http://dl.acm.org/citation.cfm?id=152611](http://dl.acm.org/citation.cfm?id=152611)</span><span class="sxs-lookup"><span data-stu-id="92424-952">Query evaluation techniques for large databases [http://dl.acm.org/citation.cfm?id=152611](http://dl.acm.org/citation.cfm?id=152611)</span></span>
10. <span data-ttu-id="92424-953">Query Processing in Parallel Relational Database Systems, IEEE Computer Society Press, 1994</span><span class="sxs-lookup"><span data-stu-id="92424-953">Query Processing in Parallel Relational Database Systems, IEEE Computer Society Press, 1994</span></span>
11. <span data-ttu-id="92424-954">Lu, Ooi, Tan, Query Processing in Parallel Relational Database Systems, IEEE Computer Society Press, 1994.</span><span class="sxs-lookup"><span data-stu-id="92424-954">Lu, Ooi, Tan, Query Processing in Parallel Relational Database Systems, IEEE Computer Society Press, 1994.</span></span>
12. <span data-ttu-id="92424-955">Christopher Olston, Benjamin Reed, Utkarsh Srivastava, Ravi Kumar, Andrew Tomkins : Pig Latin: A Not-So-Foreign Language for Data Processing, SIGMOD 2008.</span><span class="sxs-lookup"><span data-stu-id="92424-955">Christopher Olston, Benjamin Reed, Utkarsh Srivastava, Ravi Kumar, Andrew Tomkins: Pig Latin: A Not-So-Foreign Language for Data Processing, SIGMOD 2008.</span></span>
13. <span data-ttu-id="92424-956">G.</span><span class="sxs-lookup"><span data-stu-id="92424-956">G.</span></span> <span data-ttu-id="92424-957">Graefe.</span><span class="sxs-lookup"><span data-stu-id="92424-957">Graefe.</span></span> <span data-ttu-id="92424-958">infrastructure de Cascades Hello pour l’optimisation des requêtes.</span><span class="sxs-lookup"><span data-stu-id="92424-958">hello Cascades framework for query optimization.</span></span> <span data-ttu-id="92424-959">IEEE Data Eng.</span><span class="sxs-lookup"><span data-stu-id="92424-959">IEEE Data Eng.</span></span> <span data-ttu-id="92424-960">Bull., 18(3): 1995.</span><span class="sxs-lookup"><span data-stu-id="92424-960">Bull., 18(3): 1995.</span></span>

[1]: ./media/documentdb-sql-query/sql-query1.png
[introduction]: introduction.md
[consistency-levels]: consistency-levels.md