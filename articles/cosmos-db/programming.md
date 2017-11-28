---
title: "Programmation en JavaScript côté serveur pour Azure Cosmos DB | Microsoft Docs"
description: "Découvrez comment utiliser Azure Cosmos DB pour écrire des procédures stockées, des déclencheurs de base de données et des fonctions définies par l’utilisateur en JavaScript. Obtenez notamment des conseils en matière de programmation de base de données."
keywords: "Déclencheurs de base de données, procédure stockée, procédure stockée, programme de base de données, sproc, documentdb, azure, Microsoft azure"
services: cosmos-db
documentationcenter: 
author: aliuy
manager: jhubbard
editor: mimig
ms.assetid: 0fba7ebd-a4fc-4253-a786-97f1354fbf17
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2016
ms.author: andrl
ms.openlocfilehash: 8cddc7a8c9aa677b9c93bee3a7e05c226cc1f655
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-cosmos-db-server-side-programming-stored-procedures-database-triggers-and-udfs"></a><span data-ttu-id="1f04f-105">Programmation Azure Cosmos DB côté serveur : procédures stockées, déclencheurs de base de données et fonctions définies par l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="1f04f-105">Azure Cosmos DB server-side programming: Stored procedures, database triggers, and UDFs</span></span>
<span data-ttu-id="1f04f-106">Découvrez comment l’exécution transactionnelle de JavaScript intégrée au langage d’Azure Cosmos DB permet aux développeurs d’écrire des **procédures stockées**, des **déclencheurs** et des **fonctions définies par l’utilisateur (FDU)** en mode natif dans une version [ECMAScript 2015](http://www.ecma-international.org/ecma-262/6.0/) pour JavaScript.</span><span class="sxs-lookup"><span data-stu-id="1f04f-106">Learn how Azure Cosmos DB’s language integrated, transactional execution of JavaScript lets developers write **stored procedures**, **triggers** and **user defined functions (UDFs)** natively in an [ECMAScript 2015](http://www.ecma-international.org/ecma-262/6.0/) JavaScript.</span></span> <span data-ttu-id="1f04f-107">Vous pouvez ainsi écrire une logique d’application de programme de base de données qui peut être expédiée et exécutée directement dans les partitions de stockage de base de données.</span><span class="sxs-lookup"><span data-stu-id="1f04f-107">This allows you to write database program application logic that can be shipped and executed directly on the database storage partitions.</span></span> 

<span data-ttu-id="1f04f-108">Nous vous recommandons de commencer par regarder la vidéo suivante, dans laquelle Andrew Liu présente brièvement le modèle de programmation de base de données côté serveur d’Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="1f04f-108">We recommend getting started by watching the following video, where Andrew Liu provides a brief introduction to Cosmos DB's server-side database programming model.</span></span> 

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-Demo-A-Quick-Intro-to-Azure-DocumentDBs-Server-Side-Javascript/player]
> 
> 

<span data-ttu-id="1f04f-109">Ensuite, revenez à cet article dans lequel vous découvrirez les réponses aux questions suivantes :</span><span class="sxs-lookup"><span data-stu-id="1f04f-109">Then, return to this article, where you'll learn the answers to the following questions:</span></span>  

* <span data-ttu-id="1f04f-110">Comment écrire une procédure stockée, un déclencheur ou une fonction définie par l'utilisateur à l'aide de JavaScript ?</span><span class="sxs-lookup"><span data-stu-id="1f04f-110">How do I write a a stored procedure, trigger, or UDF using JavaScript?</span></span>
* <span data-ttu-id="1f04f-111">Comment Azure Cosmos DB offre-il une garantie ACID ?</span><span class="sxs-lookup"><span data-stu-id="1f04f-111">How does Cosmos DB guarantee ACID?</span></span>
* <span data-ttu-id="1f04f-112">Comment les transactions fonctionnent-elles dans Azure Cosmos DB ?</span><span class="sxs-lookup"><span data-stu-id="1f04f-112">How do transactions work in Cosmos DB?</span></span>
* <span data-ttu-id="1f04f-113">Qu'est-ce que les pré-déclencheurs et les post-déclencheurs, et comment procède-t-on pour leur écriture ?</span><span class="sxs-lookup"><span data-stu-id="1f04f-113">What are pre-triggers and post-triggers and how do I write one?</span></span>
* <span data-ttu-id="1f04f-114">Comment enregistrer et exécuter une procédure stockée, un déclencheur ou une fonction définie par l'utilisateur sur la base de l'architecture REST avec HTTP ?</span><span class="sxs-lookup"><span data-stu-id="1f04f-114">How do I register and execute a stored procedure, trigger, or UDF in a RESTful manner by using HTTP?</span></span>
* <span data-ttu-id="1f04f-115">Quels sont les kits SDK Azure Cosmos DB disponibles pour créer et exécuter des procédures stockées, des déclencheurs et des fonctions définies par l’utilisateur ?</span><span class="sxs-lookup"><span data-stu-id="1f04f-115">What Cosmos DB SDKs are available to create and execute stored procedures, triggers, and UDFs?</span></span>

## <a name="introduction-to-stored-procedure-and-udf-programming"></a><span data-ttu-id="1f04f-116">Introduction à la programmation de procédures stockées et de fonctions définies par l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="1f04f-116">Introduction to Stored Procedure and UDF Programming</span></span>
<span data-ttu-id="1f04f-117">Cette approche du *« JavaScript en tant que langage T-SQL actualisé »* libère les développeurs d’applications des complexités liées aux incompatibilités de système de type et aux technologies de mappage de relationnel objet.</span><span class="sxs-lookup"><span data-stu-id="1f04f-117">This approach of *“JavaScript as a modern day T-SQL”* frees application developers from the complexities of type system mismatches and object-relational mapping technologies.</span></span> <span data-ttu-id="1f04f-118">Elle présente également une série d'avantages intrinsèques pouvant être utilisés pour créer des applications enrichies :</span><span class="sxs-lookup"><span data-stu-id="1f04f-118">It also has a number of intrinsic advantages that can be utilized to build rich applications:</span></span>  

* <span data-ttu-id="1f04f-119">**Logique procédurale :** JavaScript en tant que langage de programmation de haut niveau offre une interface riche et familière permettant d’exprimer la logique métier.</span><span class="sxs-lookup"><span data-stu-id="1f04f-119">**Procedural Logic:** JavaScript as a high level programming language, provides a rich and familiar interface to express business logic.</span></span> <span data-ttu-id="1f04f-120">Vous pouvez effectuer des séquences d'opérations complexes plus proches des données.</span><span class="sxs-lookup"><span data-stu-id="1f04f-120">You can perform complex sequences of operations closer to the data.</span></span>
* <span data-ttu-id="1f04f-121">**Transactions atomiques :** Azure Cosmos DB garantit que les opérations de base de données effectuées dans un déclencheur ou une procédure stockée sont atomiques.</span><span class="sxs-lookup"><span data-stu-id="1f04f-121">**Atomic Transactions:** Cosmos DB guarantees that database operations performed inside a single stored procedure or trigger are atomic.</span></span> <span data-ttu-id="1f04f-122">Cela permet à une application de combiner des applications connexes en un seul lot de façon à ce que toutes réussissent ou qu’aucune ne réussisse.</span><span class="sxs-lookup"><span data-stu-id="1f04f-122">This lets an application combine related operations in a single batch so that either all of them succeed or none of them succeed.</span></span> 
* <span data-ttu-id="1f04f-123">**Performances :** le fait que JSON soit intrinsèquement mappé au système en langage Javascript et qu’il constitue l’unité de base du stockage dans Azure Cosmos DB permet une série d’optimisations telles que la matérialisation différée de documents JSON dans le pool de mémoires tampons et leur transmission au code en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="1f04f-123">**Performance:** The fact that JSON is intrinsically mapped to the Javascript language type system and is also the basic unit of storage in Cosmos DB allows for a number of optimizations like lazy materialization of JSON documents in the buffer pool and making them available on-demand to the executing code.</span></span> <span data-ttu-id="1f04f-124">Il existe d'autres avantages en matière de performances en lien avec l'expédition de la logique métier à la base de données :</span><span class="sxs-lookup"><span data-stu-id="1f04f-124">There are more performance benefits associated with shipping business logic to the database:</span></span>
  
  * <span data-ttu-id="1f04f-125">Traitement par lot - Les développeurs peuvent regrouper les opérations telles que les insertions et les envoyer en bloc.</span><span class="sxs-lookup"><span data-stu-id="1f04f-125">Batching – Developers can group operations like inserts and submit them in bulk.</span></span> <span data-ttu-id="1f04f-126">Le coût lié à la latence du trafic réseau et la surcharge en matière de stockage pour créer des transactions séparées sont considérablement réduits.</span><span class="sxs-lookup"><span data-stu-id="1f04f-126">The network traffic latency cost and the store overhead to create separate transactions are reduced significantly.</span></span> 
  * <span data-ttu-id="1f04f-127">Précompilation : Azure Cosmos DB précompile les procédures stockées, les déclencheurs et les fonctions définies par l’utilisateur pour éviter les frais de compilation JavaScript liés à chaque appel.</span><span class="sxs-lookup"><span data-stu-id="1f04f-127">Pre-compilation – Cosmos DB precompiles stored procedures, triggers and user defined functions (UDFs) to avoid JavaScript compilation cost for each invocation.</span></span> <span data-ttu-id="1f04f-128">La surcharge liée à la création du code d'octet pour la logique procédurale est amortie à une valeur minimale.</span><span class="sxs-lookup"><span data-stu-id="1f04f-128">The overhead of building the byte code for the procedural logic is amortized to a minimal value.</span></span>
  * <span data-ttu-id="1f04f-129">Séquencement - De nombreuses opérations requièrent un effet secondaire (« déclencheur ») qui implique potentiellement d'effectuer une ou plusieurs opérations de stockage secondaires.</span><span class="sxs-lookup"><span data-stu-id="1f04f-129">Sequencing – Many operations need a side-effect (“trigger”) that potentially involves doing one or many secondary store operations.</span></span> <span data-ttu-id="1f04f-130">En dehors de l'atomicité, ceci est plus performant lors du déplacement vers le serveur.</span><span class="sxs-lookup"><span data-stu-id="1f04f-130">Aside from atomicity, this is more performant when moved to the server.</span></span> 
* <span data-ttu-id="1f04f-131">**Encapsulation :** Les procédures stockées peuvent être utilisées pour regrouper la logique métier à un endroit.</span><span class="sxs-lookup"><span data-stu-id="1f04f-131">**Encapsulation:** Stored procedures can be used to group business logic in one place.</span></span> <span data-ttu-id="1f04f-132">Ceci présente deux avantages :</span><span class="sxs-lookup"><span data-stu-id="1f04f-132">This has two advantages:</span></span>
  * <span data-ttu-id="1f04f-133">Une couche d'abstraction est ajoutée aux données brutes, ce qui permet aux architectes de données de faire évoluer leurs applications indépendamment des données.</span><span class="sxs-lookup"><span data-stu-id="1f04f-133">It adds an abstraction layer on top of the raw data, which enables data architects to evolve their applications independently from the data.</span></span> <span data-ttu-id="1f04f-134">Ceci est particulièrement avantageux lorsque les données ne présentent pas de schéma, en raison des hypothèses fragiles devant être intégrées à l'application si elles doivent gérer des données directement.</span><span class="sxs-lookup"><span data-stu-id="1f04f-134">This is particularly advantageous when the data is schema-less, due to the brittle assumptions that may need to be baked into the application if they have to deal with data directly.</span></span>  
  * <span data-ttu-id="1f04f-135">Cette abstraction permet aux entreprises d'assurer la sécurité de leurs données en simplifiant l'accès à partir des scripts.</span><span class="sxs-lookup"><span data-stu-id="1f04f-135">This abstraction lets enterprises keep their data secure by streamlining the access from the scripts.</span></span>  

<span data-ttu-id="1f04f-136">La création et l’exécution de déclencheurs de base de données, de procédures stockées et d’opérateurs de requêtes personnalisés sont prises en charge par le biais de [l’API REST](/rest/api/documentdb/), [d’Azure Document DB Studio](https://github.com/mingaliu/DocumentDBStudio/releases) et de [Kits SDK clients](documentdb-sdk-dotnet.md) sur de nombreuses plateformes, dont .NET, Node.js et JavaScript.</span><span class="sxs-lookup"><span data-stu-id="1f04f-136">The creation and execution of database triggers, stored procedure and custom query operators is supported through the [REST API](/rest/api/documentdb/), [Azure DocumentDB Studio](https://github.com/mingaliu/DocumentDBStudio/releases), and [client SDKs](documentdb-sdk-dotnet.md) in many platforms including .NET, Node.js and JavaScript.</span></span>

<span data-ttu-id="1f04f-137">Ce didacticiel utilise le [kit SDK Node.js avec Q Promises](http://azure.github.io/azure-documentdb-node-q/) pour illustrer la syntaxe et l’utilisation des procédures stockées, des déclencheurs et des fonctions définies par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="1f04f-137">This tutorial uses the [Node.js SDK with Q Promises](http://azure.github.io/azure-documentdb-node-q/) to illustrate syntax and usage of stored procedures, triggers, and UDFs.</span></span>   

## <a name="stored-procedures"></a><span data-ttu-id="1f04f-138">Procédures stockées</span><span class="sxs-lookup"><span data-stu-id="1f04f-138">Stored procedures</span></span>
### <a name="example-write-a-simple-stored-procedure"></a><span data-ttu-id="1f04f-139">Exemple : Écriture d’une simple procédure stockée</span><span class="sxs-lookup"><span data-stu-id="1f04f-139">Example: Write a simple stored procedure</span></span>
<span data-ttu-id="1f04f-140">Commençons par une simple procédure stockée qui renvoie une réponse « Hello World ».</span><span class="sxs-lookup"><span data-stu-id="1f04f-140">Let’s start with a simple stored procedure that returns a “Hello World” response.</span></span>

    var helloWorldStoredProc = {
        id: "helloWorld",
        serverScript: function () {
            var context = getContext();
            var response = context.getResponse();

            response.setBody("Hello, World");
        }
    }


<span data-ttu-id="1f04f-141">Les procédures stockées sont enregistrées par collection, et elles peuvent s'appliquer à tout document et toute pièce jointe figurant dans cette collection.</span><span class="sxs-lookup"><span data-stu-id="1f04f-141">Stored procedures are registered per collection, and can operate on any document and attachment present in that collection.</span></span> <span data-ttu-id="1f04f-142">L'extrait de code suivant indique comment enregistrer la procédure stockée helloWorld avec une collection.</span><span class="sxs-lookup"><span data-stu-id="1f04f-142">The following snippet shows how to register the helloWorld stored procedure with a collection.</span></span> 

    // register the stored procedure
    var createdStoredProcedure;
    client.createStoredProcedureAsync('dbs/testdb/colls/testColl', helloWorldStoredProc)
        .then(function (response) {
            createdStoredProcedure = response.resource;
            console.log("Successfully created stored procedure");
        }, function (error) {
            console.log("Error", error);
        });


<span data-ttu-id="1f04f-143">Une fois que la procédure stockée est enregistrée, nous pouvons l'exécuter sur la base de la collection et renvoyer les résultats au client.</span><span class="sxs-lookup"><span data-stu-id="1f04f-143">Once the stored procedure is registered, we can execute it against the collection, and read the results back at the client.</span></span> 

    // execute the stored procedure
    client.executeStoredProcedureAsync('dbs/testdb/colls/testColl/sprocs/helloWorld')
        .then(function (response) {
            console.log(response.result); // "Hello, World"
        }, function (err) {
            console.log("Error", error);
        });


<span data-ttu-id="1f04f-144">L’objet context donne accès à toutes les opérations pouvant être effectuées dans le stockage Azure Cosmos DB, ainsi que l’accès aux objets request et response.</span><span class="sxs-lookup"><span data-stu-id="1f04f-144">The context object provides access to all operations that can be performed on Cosmos DB storage, as well as access to the request and response objects.</span></span> <span data-ttu-id="1f04f-145">En l'occurrence, nous avons utilisé l'objet response pour définir le corps de la réponse renvoyée au client.</span><span class="sxs-lookup"><span data-stu-id="1f04f-145">In this case, we used the response object to set the body of the response that was sent back to the client.</span></span> <span data-ttu-id="1f04f-146">Pour plus d’informations, consultez la [documentation du kit SDK du serveur JavaScript Azure Cosmos DB](http://azure.github.io/azure-documentdb-js-server/).</span><span class="sxs-lookup"><span data-stu-id="1f04f-146">For more details, refer to the [Azure Cosmos DB JavaScript server SDK documentation](http://azure.github.io/azure-documentdb-js-server/).</span></span>  

<span data-ttu-id="1f04f-147">Extrapolons à partir de cet exemple et ajoutons à la procédure stockée d'autres fonctionnalités liées à la base de données.</span><span class="sxs-lookup"><span data-stu-id="1f04f-147">Let us expand on this example and add more database related functionality to the stored procedure.</span></span> <span data-ttu-id="1f04f-148">Les procédures stockées peuvent créer, mettre à jour, lire, interroger et supprimer des documents et des pièces jointes au sein de la collection.</span><span class="sxs-lookup"><span data-stu-id="1f04f-148">Stored procedures can create, update, read, query and delete documents and attachments inside the collection.</span></span>    

### <a name="example-write-a-stored-procedure-to-create-a-document"></a><span data-ttu-id="1f04f-149">Exemple : Écriture d’une procédure stockée pour créer un document</span><span class="sxs-lookup"><span data-stu-id="1f04f-149">Example: Write a stored procedure to create a document</span></span>
<span data-ttu-id="1f04f-150">L’extrait de code suivant indique comment utiliser l’objet context pour interagir avec les ressources Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="1f04f-150">The next snippet shows how to use the context object to interact with Cosmos DB resources.</span></span>

    var createDocumentStoredProc = {
        id: "createMyDocument",
        serverScript: function createMyDocument(documentToCreate) {
            var context = getContext();
            var collection = context.getCollection();

            var accepted = collection.createDocument(collection.getSelfLink(),
                  documentToCreate,
                  function (err, documentCreated) {
                      if (err) throw new Error('Error' + err.message);
                      context.getResponse().setBody(documentCreated.id)
                  });
            if (!accepted) return;
        }
    }


<span data-ttu-id="1f04f-151">Cette procédure stockée prend en entrée documentToCreate, le corps d'un document à créer dans la collection actuelle.</span><span class="sxs-lookup"><span data-stu-id="1f04f-151">This stored procedure takes as input documentToCreate, the body of a document to be created in the current collection.</span></span> <span data-ttu-id="1f04f-152">Toutes ces opérations sont asynchrones et dépendent de rappels de fonction JavaScript.</span><span class="sxs-lookup"><span data-stu-id="1f04f-152">All such operations are asynchronous and depend on JavaScript function callbacks.</span></span> <span data-ttu-id="1f04f-153">La fonction de rappel présente deux paramètres, un pour l'objet d'erreur en cas d'échec de l'opération et un pour l'objet créé.</span><span class="sxs-lookup"><span data-stu-id="1f04f-153">The callback function has two parameters, one for the error object in case the operation fails, and one for the created object.</span></span> <span data-ttu-id="1f04f-154">À l'intérieur du rappel, les utilisateurs peuvent gérer l'exception ou générer une erreur.</span><span class="sxs-lookup"><span data-stu-id="1f04f-154">Inside the callback, users can either handle the exception or throw an error.</span></span> <span data-ttu-id="1f04f-155">Si aucun rappel n’est fourni et qu’une erreur se produit, le runtime d’Azure Cosmos DB génère une erreur.</span><span class="sxs-lookup"><span data-stu-id="1f04f-155">In case a callback is not provided and there is an error, the Azure Cosmos DB runtime throws an error.</span></span>   

<span data-ttu-id="1f04f-156">Dans l'exemple ci-dessous, la fonction de rappel génère une erreur si l'opération a échoué.</span><span class="sxs-lookup"><span data-stu-id="1f04f-156">In the example above, the callback throws an error if the operation failed.</span></span> <span data-ttu-id="1f04f-157">Dans le cas contraire, elle définit l'ID du document créé en tant que corps de la réponse au client.</span><span class="sxs-lookup"><span data-stu-id="1f04f-157">Otherwise, it sets the id of the created document as the body of the response to the client.</span></span> <span data-ttu-id="1f04f-158">Voici la façon dont cette procédure stockée est exécutée avec des paramètres d'entrée.</span><span class="sxs-lookup"><span data-stu-id="1f04f-158">Here is how this stored procedure is executed with input parameters.</span></span>

    // register the stored procedure
    client.createStoredProcedureAsync('dbs/testdb/colls/testColl', createDocumentStoredProc)
        .then(function (response) {
            var createdStoredProcedure = response.resource;

            // run stored procedure to create a document
            var docToCreate = {
                id: "DocFromSproc",
                book: "The Hitchhiker’s Guide to the Galaxy",
                author: "Douglas Adams"
            };

            return client.executeStoredProcedureAsync('dbs/testdb/colls/testColl/sprocs/createMyDocument',
                  docToCreate);
        }, function (error) {
            console.log("Error", error);
        })
    .then(function (response) {
        console.log(response); // "DocFromSproc"
    }, function (error) {
        console.log("Error", error);
    });


<span data-ttu-id="1f04f-159">Notez que cette procédure stockée peut être modifiée pour accepter en entrée un tableau de corps de document et pour les créer dans la même exécution de procédure stockée au lieu de plusieurs demandes du réseau visant à les créer chacune séparément.</span><span class="sxs-lookup"><span data-stu-id="1f04f-159">Note that this stored procedure can be modified to take an array of document bodies as input and create them all in the same stored procedure execution instead of multiple network requests to create each of them individually.</span></span> <span data-ttu-id="1f04f-160">Ceci permet de mettre en œuvre une importation en bloc efficace pour Azure Cosmos DB (un point que nous aborderons plus tard dans ce didacticiel).</span><span class="sxs-lookup"><span data-stu-id="1f04f-160">This can be used to implement an efficient bulk importer for Cosmos DB (discussed later in this tutorial).</span></span>   

<span data-ttu-id="1f04f-161">L'exemple décrit ci-dessus a illustré la façon d'utiliser des procédures stockées.</span><span class="sxs-lookup"><span data-stu-id="1f04f-161">The example described demonstrated how to use stored procedures.</span></span> <span data-ttu-id="1f04f-162">Nous verrons les déclencheurs et les fonctions définies par l'utilisateur plus loin dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="1f04f-162">We will cover triggers and user defined functions (UDFs) later in the tutorial.</span></span>

## <a name="database-program-transactions"></a><span data-ttu-id="1f04f-163">Transactions de programme de base de données</span><span class="sxs-lookup"><span data-stu-id="1f04f-163">Database program transactions</span></span>
<span data-ttu-id="1f04f-164">Une transaction dans une base de données classique peut être définie comme étant une séquence d'opérations effectuées en tant qu'unité de travail logique unique.</span><span class="sxs-lookup"><span data-stu-id="1f04f-164">Transaction in a typical database can be defined as a sequence of operations performed as a single logical unit of work.</span></span> <span data-ttu-id="1f04f-165">Chaque transaction offre des **garanties ACID**.</span><span class="sxs-lookup"><span data-stu-id="1f04f-165">Each transaction provides **ACID guarantees**.</span></span> <span data-ttu-id="1f04f-166">ACID est un acronyme bien connu qui est l’abréviation de quatre propriétés : Atomicité, Cohérence, Isolation et Durabilité.</span><span class="sxs-lookup"><span data-stu-id="1f04f-166">ACID is a well-known acronym that stands for four properties -  Atomicity, Consistency, Isolation and Durability.</span></span>  

<span data-ttu-id="1f04f-167">En bref, l'atomicité permet de s'assurer que tout le travail effectué au sein d'une transaction est traité en tant que simple unité validée dans son intégralité ou aucunement.</span><span class="sxs-lookup"><span data-stu-id="1f04f-167">Briefly, atomicity guarantees that all the work done inside a transaction is treated as a single unit where either all of it is committed or none.</span></span> <span data-ttu-id="1f04f-168">La cohérence permet de s'assurer que les données sont toujours dans un état interne correct d'une transaction à l'autre.</span><span class="sxs-lookup"><span data-stu-id="1f04f-168">Consistency makes sure that the data is always in a good internal state across transactions.</span></span> <span data-ttu-id="1f04f-169">L'isolation, quant à elle, permet de garantir qu'aucune transaction n'interfère avec les autres. Généralement, la plupart des systèmes commerciaux fournissent plusieurs niveaux d'isolation pouvant être utilisés en fonction des besoins des applications.</span><span class="sxs-lookup"><span data-stu-id="1f04f-169">Isolation guarantees that no two transactions interfere with each other – generally, most commercial systems provide multiple isolation levels that can be used based on the application needs.</span></span> <span data-ttu-id="1f04f-170">Enfin, la durabilité permet de s'assurer que toute modification validée dans la base de données sera toujours présente.</span><span class="sxs-lookup"><span data-stu-id="1f04f-170">Durability ensures that any change that’s committed in the database will always be present.</span></span>   

<span data-ttu-id="1f04f-171">Dans Azure Cosmos DB, JavaScript est hébergé dans le même espace mémoire que la base de données.</span><span class="sxs-lookup"><span data-stu-id="1f04f-171">In Cosmos DB, JavaScript is hosted in the same memory space as the database.</span></span> <span data-ttu-id="1f04f-172">Par conséquent, les demandes effectuées au sein de procédures stockées et de déclencheurs s'exécutent dans la même étendue qu'une session de base de données.</span><span class="sxs-lookup"><span data-stu-id="1f04f-172">Hence, requests made within stored procedures and triggers execute in the same scope of a database session.</span></span> <span data-ttu-id="1f04f-173">Cela permet à Azure Cosmos DB de garantir ACID pour toutes les opérations qui font partie d’une procédure stockée ou d’un déclencheur.</span><span class="sxs-lookup"><span data-stu-id="1f04f-173">This enables Cosmos DB to guarantee ACID for all operations that are part of a single stored procedure/trigger.</span></span> <span data-ttu-id="1f04f-174">Envisageons la définition de procédure stockée suivante :</span><span class="sxs-lookup"><span data-stu-id="1f04f-174">Consider the following stored procedure definition:</span></span>

    // JavaScript source code
    var exchangeItemsSproc = {
        id: "exchangeItems",
        serverScript: function (playerId1, playerId2) {
            var context = getContext();
            var collection = context.getCollection();
            var response = context.getResponse();

            var player1Document, player2Document;

            // query for players
            var filterQuery = 'SELECT * FROM Players p where p.id  = "' + playerId1 + '"';
            var accept = collection.queryDocuments(collection.getSelfLink(), filterQuery, {},
                function (err, documents, responseOptions) {
                    if (err) throw new Error("Error" + err.message);

                    if (documents.length != 1) throw "Unable to find both names";
                    player1Document = documents[0];

                    var filterQuery2 = 'SELECT * FROM Players p where p.id = "' + playerId2 + '"';
                    var accept2 = collection.queryDocuments(collection.getSelfLink(), filterQuery2, {},
                        function (err2, documents2, responseOptions2) {
                            if (err2) throw new Error("Error" + err2.message);
                            if (documents2.length != 1) throw "Unable to find both names";
                            player2Document = documents2[0];
                            swapItems(player1Document, player2Document);
                            return;
                        });
                    if (!accept2) throw "Unable to read player details, abort ";
                });

            if (!accept) throw "Unable to read player details, abort ";

            // swap the two players’ items
            function swapItems(player1, player2) {
                var player1ItemSave = player1.item;
                player1.item = player2.item;
                player2.item = player1ItemSave;

                var accept = collection.replaceDocument(player1._self, player1,
                    function (err, docReplaced) {
                        if (err) throw "Unable to update player 1, abort ";

                        var accept2 = collection.replaceDocument(player2._self, player2,
                            function (err2, docReplaced2) {
                                if (err) throw "Unable to update player 2, abort"
                            });

                        if (!accept2) throw "Unable to update player 2, abort";
                    });

                if (!accept) throw "Unable to update player 1, abort";
            }
        }
    }

    // register the stored procedure in Node.js client
    client.createStoredProcedureAsync(collection._self, exchangeItemsSproc)
        .then(function (response) {
            var createdStoredProcedure = response.resource;
        }
    );

<span data-ttu-id="1f04f-175">Cette procédure stockée utilise des transactions au sein d'une application de jeu pour échanger des éléments entre deux joueurs en une seule opération.</span><span class="sxs-lookup"><span data-stu-id="1f04f-175">This stored procedure uses transactions within a gaming app to trade items between two players in a single operation.</span></span> <span data-ttu-id="1f04f-176">Elle essaie de lire deux documents, correspondant chacun aux ID de joueur transmis en tant qu'arguments.</span><span class="sxs-lookup"><span data-stu-id="1f04f-176">The stored procedure attempts to read two documents each corresponding to the player IDs passed in as an argument.</span></span> <span data-ttu-id="1f04f-177">Si les deux documents de joueur sont trouvés, la procédure stockée les met à jour en intervertissant leurs éléments.</span><span class="sxs-lookup"><span data-stu-id="1f04f-177">If both player documents are found, then the stored procedure updates the documents by swapping their items.</span></span> <span data-ttu-id="1f04f-178">Si des erreurs se produisent en chemin, elle génère une exception JavaScript qui annule implicitement la transaction.</span><span class="sxs-lookup"><span data-stu-id="1f04f-178">If any errors are encountered along the way, it throws a JavaScript exception that implicitly aborts the transaction.</span></span>

<span data-ttu-id="1f04f-179">Si la collection de la procédure stockée est enregistrée sur une collection à partition unique, la transaction est étendue à tous les documents au sein de la collection.</span><span class="sxs-lookup"><span data-stu-id="1f04f-179">If the collection the stored procedure is registered against is a single-partition collection, then the transaction is scoped to all the documents within the collection.</span></span> <span data-ttu-id="1f04f-180">Si la collection est partitionnée, les procédures stockées sont exécutées dans l’étendue de transaction d’une clé de partition unique.</span><span class="sxs-lookup"><span data-stu-id="1f04f-180">If the collection is partitioned, then stored procedures are executed in the transaction scope of a single partition key.</span></span> <span data-ttu-id="1f04f-181">Chaque exécution de procédure stockée doit alors inclure une valeur de clé de partition correspondant à l’étendue sous laquelle la transaction doit être exécutée.</span><span class="sxs-lookup"><span data-stu-id="1f04f-181">Each stored procedure execution must then include a partition key value corresponding to the scope the transaction must run under.</span></span> <span data-ttu-id="1f04f-182">Pour plus d’informations, consultez [Partitionnement dans Azure Cosmos DB](partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="1f04f-182">For more details, see [Azure Cosmos DB Partitioning](partition-data.md).</span></span>

### <a name="commit-and-rollback"></a><span data-ttu-id="1f04f-183">Validation et restauration</span><span class="sxs-lookup"><span data-stu-id="1f04f-183">Commit and rollback</span></span>
<span data-ttu-id="1f04f-184">Les transactions sont intégrées de façon approfondie et native dans le modèle de programmation JavaScript d’Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="1f04f-184">Transactions are deeply and natively integrated into Cosmos DB’s JavaScript programming model.</span></span> <span data-ttu-id="1f04f-185">Dans une fonction JavaScript, toutes les opérations sont automatiquement encapsulées dans une transaction unique.</span><span class="sxs-lookup"><span data-stu-id="1f04f-185">Inside a JavaScript function, all operations are automatically wrapped under a single transaction.</span></span> <span data-ttu-id="1f04f-186">Si le code JavaScript s'exécute sans erreur, les opérations dans la base de données sont validées.</span><span class="sxs-lookup"><span data-stu-id="1f04f-186">If the JavaScript completes without any exception, the operations to the database are committed.</span></span> <span data-ttu-id="1f04f-187">En effet, les instructions BEGIN TRANSACTION et COMMIT TRANSACTION des bases de données relationnelles sont implicites dans Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="1f04f-187">In effect, the “BEGIN TRANSACTION” and “COMMIT TRANSACTION” statements in relational databases are implicit in Cosmos DB.</span></span>  

<span data-ttu-id="1f04f-188">Si une exception est propagée à partir du script, le runtime JavaScript d’Azure Cosmos DB annule toute la transaction.</span><span class="sxs-lookup"><span data-stu-id="1f04f-188">If there is any exception that’s propagated from the script, Cosmos DB’s JavaScript runtime will roll back the whole transaction.</span></span> <span data-ttu-id="1f04f-189">Comme le montre l’exemple précédent, la génération d’une exception équivaut à une instruction ROLLBACK TRANSACTION dans Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="1f04f-189">As shown in the earlier example, throwing an exception is effectively equivalent to a “ROLLBACK TRANSACTION” in Cosmos DB.</span></span>

### <a name="data-consistency"></a><span data-ttu-id="1f04f-190">Cohérence des données</span><span class="sxs-lookup"><span data-stu-id="1f04f-190">Data consistency</span></span>
<span data-ttu-id="1f04f-191">Les procédures stockées et les déclencheurs sont toujours exécutés dans le réplica principal du conteneur Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="1f04f-191">Stored procedures and triggers are always executed on the primary replica of the Azure Cosmos DB container.</span></span> <span data-ttu-id="1f04f-192">Cela permet de s'assurer que les lectures à partir des procédures stockées offrent une cohérence forte.</span><span class="sxs-lookup"><span data-stu-id="1f04f-192">This ensures that reads from inside stored procedures offer strong consistency.</span></span> <span data-ttu-id="1f04f-193">Les requêtes utilisant des fonctions définies par l'utilisateur peuvent être exécutées dans le réplica principal ou n'importe quel réplica secondaire, mais nous veillons à répondre au niveau de cohérence demandé en choisissant le réplica approprié.</span><span class="sxs-lookup"><span data-stu-id="1f04f-193">Queries using user defined functions can be executed on the primary or any secondary replica, but we ensure to meet the requested consistency level by choosing the appropriate replica.</span></span>

## <a name="bounded-execution"></a><span data-ttu-id="1f04f-194">Exécution limitée</span><span class="sxs-lookup"><span data-stu-id="1f04f-194">Bounded execution</span></span>
<span data-ttu-id="1f04f-195">Toutes les opérations Azure Cosmos DB doivent s’effectuer avant l’expiration de la demande spécifiée par le serveur.</span><span class="sxs-lookup"><span data-stu-id="1f04f-195">All Cosmos DB operations must complete within the server specified request timeout duration.</span></span> <span data-ttu-id="1f04f-196">Cette contrainte s'applique également aux fonctions JavaScript (procédures stockées, déclencheurs et fonctions définies par l'utilisateur).</span><span class="sxs-lookup"><span data-stu-id="1f04f-196">This constraint also applies to JavaScript functions (stored procedures, triggers and user-defined functions).</span></span> <span data-ttu-id="1f04f-197">Si une opération n'est pas terminée dans ce délai imparti, la transaction est annulée.</span><span class="sxs-lookup"><span data-stu-id="1f04f-197">If an operation does not complete with that time limit, the transaction is rolled back.</span></span> <span data-ttu-id="1f04f-198">Les fonctions JavaScript doivent s'exécuter dans ce délai ou mettre en œuvre un modèle basé sur la continuation pour traiter par lots/reprendre l'exécution.</span><span class="sxs-lookup"><span data-stu-id="1f04f-198">JavaScript functions must finish within the time limit or implement a continuation based model to batch/resume execution.</span></span>  

<span data-ttu-id="1f04f-199">Afin de simplifier le développement de procédures stockées et de déclencheurs pour gérer les limites de temps, toutes les fonctions sous l'objet de collection (pour la création, la lecture, le remplacement et la suppression de documents et de pièces jointes) renvoient une valeur booléenne qui indique si l'opération arrivera à son terme.</span><span class="sxs-lookup"><span data-stu-id="1f04f-199">In order to simplify development of stored procedures and triggers to handle time limits, all functions under the collection object (for create, read, replace, and delete of documents and attachments) return a Boolean value that represents whether that operation will complete.</span></span> <span data-ttu-id="1f04f-200">Si cette valeur est false, cela indique que la limite de temps est sur le point d'arriver à échéance et que la procédure doit clôturer l'exécution.</span><span class="sxs-lookup"><span data-stu-id="1f04f-200">If this value is false, it is an indication that the time limit is about to expire and that the procedure must wrap up execution.</span></span>  <span data-ttu-id="1f04f-201">Les opérations mises en file d'attente avant la première opération de stockage non acceptée sont assurées de s'exécuter si la procédure stockée s'exécute à temps et ne place pas d'autres demandes dans la file d'attente.</span><span class="sxs-lookup"><span data-stu-id="1f04f-201">Operations queued prior to the first unaccepted store operation are guaranteed to complete if the stored procedure completes in time and does not queue any more requests.</span></span>  

<span data-ttu-id="1f04f-202">Les fonctions JavaScript sont également liées lors de la consommation de ressources.</span><span class="sxs-lookup"><span data-stu-id="1f04f-202">JavaScript functions are also bounded on resource consumption.</span></span> <span data-ttu-id="1f04f-203">Azure Cosmos DB réserve le débit par collection en fonction de la taille configurée d’un compte de base de données.</span><span class="sxs-lookup"><span data-stu-id="1f04f-203">Cosmos DB reserves throughput per collection based on the provisioned size of a database account.</span></span> <span data-ttu-id="1f04f-204">Le débit est exprimé en unités normalisées de processeur, de mémoire et de consommation d'E/S, appelées unités de demande.</span><span class="sxs-lookup"><span data-stu-id="1f04f-204">Throughput is expressed in terms of a normalized unit of CPU, memory and IO consumption called request units or RUs.</span></span> <span data-ttu-id="1f04f-205">Les fonctions JavaScript peuvent potentiellement utiliser un nombre élevé d'unités de demande en peu de temps, et la limite de débit peut être restreinte si la limite de la collection est atteinte.</span><span class="sxs-lookup"><span data-stu-id="1f04f-205">JavaScript functions can potentially use up a large number of RUs within a short time, and might get rate-limited if the collection’s limit is reached.</span></span> <span data-ttu-id="1f04f-206">Les procédures stockées gourmandes en ressources peuvent également être mises en quarantaine pour garantir la disponibilité des opérations de base de données primitives.</span><span class="sxs-lookup"><span data-stu-id="1f04f-206">Resource intensive stored procedures might also be quarantined to ensure availability of primitive database operations.</span></span>  

### <a name="example-bulk-importing-data-into-a-database-program"></a><span data-ttu-id="1f04f-207">Exemple : importation de données en bloc dans un programme de base de données</span><span class="sxs-lookup"><span data-stu-id="1f04f-207">Example: Bulk importing data into a database program</span></span>
<span data-ttu-id="1f04f-208">Ci-dessous se trouve un exemple de procédure stockée qui a été écrite pour importer des documents en bloc dans une collection.</span><span class="sxs-lookup"><span data-stu-id="1f04f-208">Below is an example of a stored procedure that is written to bulk-import documents into a collection.</span></span> <span data-ttu-id="1f04f-209">Notez la façon dont la procédure stockée gère l'exécution liée en vérifiant la valeur de retour booléenne à partir de createDocument, puis utilise le nombre de documents insérés dans chaque appel de la procédure stockée pour effectuer le suivi de la progression et la reprendre d'un lot à un autre.</span><span class="sxs-lookup"><span data-stu-id="1f04f-209">Note how the stored procedure handles bounded execution by checking the Boolean return value from createDocument, and then uses the count of documents inserted in each invocation of the stored procedure to track and resume progress across batches.</span></span>

    function bulkImport(docs) {
        var collection = getContext().getCollection();
        var collectionLink = collection.getSelfLink();

        // The count of imported docs, also used as current doc index.
        var count = 0;

        // Validate input.
        if (!docs) throw new Error("The array is undefined or null.");

        var docsLength = docs.length;
        if (docsLength == 0) {
            getContext().getResponse().setBody(0);
        }

        // Call the create API to create a document.
        tryCreate(docs[count], callback);

        // Note that there are 2 exit conditions:
        // 1) The createDocument request was not accepted. 
        //    In this case the callback will not be called, we just call setBody and we are done.
        // 2) The callback was called docs.length times.
        //    In this case all documents were created and we don’t need to call tryCreate anymore. Just call setBody and we are done.
        function tryCreate(doc, callback) {
            var isAccepted = collection.createDocument(collectionLink, doc, callback);

            // If the request was accepted, callback will be called.
            // Otherwise report current count back to the client, 
            // which will call the script again with remaining set of docs.
            if (!isAccepted) getContext().getResponse().setBody(count);
        }

        // This is called when collection.createDocument is done in order to process the result.
        function callback(err, doc, options) {
            if (err) throw err;

            // One more document has been inserted, increment the count.
            count++;

            if (count >= docsLength) {
                // If we created all documents, we are done. Just set the response.
                getContext().getResponse().setBody(count);
            } else {
                // Create next document.
                tryCreate(docs[count], callback);
            }
        }
    }

## <span data-ttu-id="1f04f-210"><a id="trigger"></a> Déclencheurs de base de données</span><span class="sxs-lookup"><span data-stu-id="1f04f-210"><a id="trigger"></a> Database triggers</span></span>
### <a name="database-pre-triggers"></a><span data-ttu-id="1f04f-211">Pré-déclencheurs de base de données</span><span class="sxs-lookup"><span data-stu-id="1f04f-211">Database pre-triggers</span></span>
<span data-ttu-id="1f04f-212">Azure Cosmos DB fournit des déclencheurs qui sont exécutés ou déclenchés par une opération sur un document.</span><span class="sxs-lookup"><span data-stu-id="1f04f-212">Cosmos DB provides triggers that are executed or triggered by an operation on a document.</span></span> <span data-ttu-id="1f04f-213">Par exemple, vous pouvez spécifier un pré-déclencheur lorsque vous créez un document ; ce pré-déclencheur s'exécutera avant la création du document</span><span class="sxs-lookup"><span data-stu-id="1f04f-213">For example, you can specify a pre-trigger when you are creating a document – this pre-trigger will run before the document is created.</span></span> <span data-ttu-id="1f04f-214">Voici un exemple de la façon dont les pré-déclencheurs peuvent être utilisés pour valider les propriétés d'un document en cours de création.</span><span class="sxs-lookup"><span data-stu-id="1f04f-214">The following is an example of how pre-triggers can be used to validate the properties of a document that is being created:</span></span>

    var validateDocumentContentsTrigger = {
        id: "validateDocumentContents",
        serverScript: function validate() {
            var context = getContext();
            var request = context.getRequest();

            // document to be created in the current operation
            var documentToCreate = request.getBody();

            // validate properties
            if (!("timestamp" in documentToCreate)) {
                var ts = new Date();
                documentToCreate["my timestamp"] = ts.getTime();
            }

            // update the document that will be created
            request.setBody(documentToCreate);
        },
        triggerType: TriggerType.Pre,
        triggerOperation: TriggerOperation.Create
    }


<span data-ttu-id="1f04f-215">Ainsi que le code d'enregistrement côté client Node.js correspondant pour le déclencheur :</span><span class="sxs-lookup"><span data-stu-id="1f04f-215">And the corresponding Node.js client-side registration code for the trigger:</span></span>

    // register pre-trigger
    client.createTriggerAsync(collection.self, validateDocumentContentsTrigger)
        .then(function (response) {
            console.log("Created", response.resource);
            var docToCreate = {
                id: "DocWithTrigger",
                event: "Error",
                source: "Network outage"
            };

            // run trigger while creating above document 
            var options = { preTriggerInclude: "validateDocumentContents" };

            return client.createDocumentAsync(collection.self,
                  docToCreate, options);
        }, function (error) {
            console.log("Error", error);
        })
    .then(function (response) {
        console.log(response.resource); // document with timestamp property added
    }, function (error) {
        console.log("Error", error);
    });


<span data-ttu-id="1f04f-216">Les pré-déclencheurs ne peuvent pas avoir de paramètres en entrée.</span><span class="sxs-lookup"><span data-stu-id="1f04f-216">Pre-triggers cannot have any input parameters.</span></span> <span data-ttu-id="1f04f-217">L'objet request peut être utilisé pour manipuler le message de demande associé à l'opération.</span><span class="sxs-lookup"><span data-stu-id="1f04f-217">The request object can be used to manipulate the request message associated with the operation.</span></span> <span data-ttu-id="1f04f-218">Ici, le pré-déclencheur est exécuté avec la création d'un document et le corps du message de demande contient le document à créer au format JSON.</span><span class="sxs-lookup"><span data-stu-id="1f04f-218">Here, the pre-trigger is being run with the creation of a document, and the request message body contains the document to be created in JSON format.</span></span>   

<span data-ttu-id="1f04f-219">Lorsque les déclencheurs sont enregistrés, les utilisateurs peuvent spécifier les opérations avec lesquelles il peut s'exécuter.</span><span class="sxs-lookup"><span data-stu-id="1f04f-219">When triggers are registered, users can specify the operations that it can run with.</span></span> <span data-ttu-id="1f04f-220">Ce déclencheur a été créé avec TriggerOperation.Create, ce qui signifie que le code suivant n'est pas autorisé.</span><span class="sxs-lookup"><span data-stu-id="1f04f-220">This trigger was created with TriggerOperation.Create, which means the following is not permitted.</span></span>

    var options = { preTriggerInclude: "validateDocumentContents" };

    client.replaceDocumentAsync(docToReplace.self,
                  newDocBody, options)
    .then(function (response) {
        console.log(response.resource);
    }, function (error) {
        console.log("Error", error);
    });

    // Fails, can’t use a create trigger in a replace operation

### <a name="database-post-triggers"></a><span data-ttu-id="1f04f-221">Post-déclencheurs de base de données</span><span class="sxs-lookup"><span data-stu-id="1f04f-221">Database post-triggers</span></span>
<span data-ttu-id="1f04f-222">Les post-déclencheurs, comme les pré-déclencheurs, sont associés à une opération dans un document et n'acceptent pas de paramètres en entrée.</span><span class="sxs-lookup"><span data-stu-id="1f04f-222">Post-triggers, like pre-triggers, are associated with an operation on a document and don’t take any input parameters.</span></span> <span data-ttu-id="1f04f-223">Ils s'exécutent **après** la fin de l'opération et ils ont accès au message de réponse qui est envoyé au client.</span><span class="sxs-lookup"><span data-stu-id="1f04f-223">They run **after** the operation has completed, and have access to the response message that is sent to the client.</span></span>   

<span data-ttu-id="1f04f-224">L'exemple suivant montre les post-déclencheurs en action :</span><span class="sxs-lookup"><span data-stu-id="1f04f-224">The following example shows post-triggers in action:</span></span>

    var updateMetadataTrigger = {
        id: "updateMetadata",
        serverScript: function updateMetadata() {
            var context = getContext();
            var collection = context.getCollection();
            var response = context.getResponse();

            // document that was created
            var createdDocument = response.getBody();

            // query for metadata document
            var filterQuery = 'SELECT * FROM root r WHERE r.id = "_metadata"';
            var accept = collection.queryDocuments(collection.getSelfLink(), filterQuery,
                updateMetadataCallback);
            if(!accept) throw "Unable to update metadata, abort";

            function updateMetadataCallback(err, documents, responseOptions) {
                if(err) throw new Error("Error" + err.message);
                         if(documents.length != 1) throw 'Unable to find metadata document';

                         var metadataDocument = documents[0];

                         // update metadata
                         metadataDocument.createdDocuments += 1;
                         metadataDocument.createdNames += " " + createdDocument.id;
                         var accept = collection.replaceDocument(metadataDocument._self,
                               metadataDocument, function(err, docReplaced) {
                                      if(err) throw "Unable to update metadata, abort";
                               });
                         if(!accept) throw "Unable to update metadata, abort";
                         return;                    
            }                                                                                            
        },
        triggerType: TriggerType.Post,
        triggerOperation: TriggerOperation.All
    }


<span data-ttu-id="1f04f-225">Le déclencheur peut être enregistré comme indiqué dans l'exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="1f04f-225">The trigger can be registered as shown in the following sample.</span></span>

    // register post-trigger
    client.createTriggerAsync('dbs/testdb/colls/testColl', updateMetadataTrigger)
        .then(function(createdTrigger) { 
            var docToCreate = { 
                name: "artist_profile_1023",
                artist: "The Band",
                albums: ["Hellujah", "Rotators", "Spinning Top"]
            };

            // run trigger while creating above document 
            var options = { postTriggerInclude: "updateMetadata" };

            return client.createDocumentAsync(collection.self,
                  docToCreate, options);
        }, function(error) {
            console.log("Error" , error);
        })
    .then(function(response) {
        console.log(response.resource); 
    }, function(error) {
        console.log("Error" , error);
    });


<span data-ttu-id="1f04f-226">Ce déclencheur interroge le document de métadonnées et le met à jour avec des informations relatives au document qui vient d'être créé.</span><span class="sxs-lookup"><span data-stu-id="1f04f-226">This trigger queries for the metadata document and updates it with details about the newly created document.</span></span>  

<span data-ttu-id="1f04f-227">Un élément important à noter est l’exécution **transactionnelle** des déclencheurs dans Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="1f04f-227">One thing that is important to note is the **transactional** execution of triggers in Cosmos DB.</span></span> <span data-ttu-id="1f04f-228">Ce post-déclencheur s'exécute dans le cadre de la même transaction que la création du document initial.</span><span class="sxs-lookup"><span data-stu-id="1f04f-228">This post-trigger runs as part of the same transaction as the creation of the original document.</span></span> <span data-ttu-id="1f04f-229">Par conséquent, si nous générons une exception à partir du post-déclencheur (supposons que nous ne soyons pas en mesure de mettre à jour le document de métadonnées), la transaction entière échoue et est annulée.</span><span class="sxs-lookup"><span data-stu-id="1f04f-229">Therefore, if we throw an exception from the post-trigger (say if we are unable to update the metadata document), the whole transaction will fail and be rolled back.</span></span> <span data-ttu-id="1f04f-230">Aucun document n'est créé et une exception est renvoyée.</span><span class="sxs-lookup"><span data-stu-id="1f04f-230">No document will be created, and an exception will be returned.</span></span>  

## <span data-ttu-id="1f04f-231"><a id="udf"></a>Fonctions définies par l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="1f04f-231"><a id="udf"></a>User-defined functions</span></span>
<span data-ttu-id="1f04f-232">Les fonctions définies par l’utilisateur (FDU) permettent d’étendre la grammaire du langage de requête SQL de l’API DocumentDB et de mettre en œuvre une logique métier personnalisée.</span><span class="sxs-lookup"><span data-stu-id="1f04f-232">User-defined functions (UDFs) are used to extend the DocumentDB API SQL query language grammar and implement custom business logic.</span></span> <span data-ttu-id="1f04f-233">Elles peuvent uniquement être appelées à partir de requêtes.</span><span class="sxs-lookup"><span data-stu-id="1f04f-233">They can only be called from inside queries.</span></span> <span data-ttu-id="1f04f-234">Elles n'ont pas accès à l'objet de contexte et sont destinées à être utilisées en tant que JavaScript en calcul seul.</span><span class="sxs-lookup"><span data-stu-id="1f04f-234">They do not have access to the context object and are meant to be used as compute-only JavaScript.</span></span> <span data-ttu-id="1f04f-235">Par conséquent, elles peuvent être exécutées sur des réplicas secondaires du service Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="1f04f-235">Therefore, UDFs can be run on secondary replicas of the Cosmos DB service.</span></span>  

<span data-ttu-id="1f04f-236">L'exemple suivant crée une fonction définie par l'utilisateur pour calculer les impôts sur la base des taux de différentes tranches de revenu, puis utilise celle-ci au sein d'une requête pour trouver toutes les personnes ayant payé des impôts supérieurs à 20 000 $.</span><span class="sxs-lookup"><span data-stu-id="1f04f-236">The following sample creates a UDF to calculate income tax based on rates for various income brackets, and then uses it inside a query to find all people who paid more than $20,000 in taxes.</span></span>

    var taxUdf = {
        id: "tax",
        serverScript: function tax(income) {

            if(income == undefined) 
                throw 'no input';

            if (income < 1000) 
                return income * 0.1;
            else if (income < 10000) 
                return income * 0.2;
            else
                return income * 0.4;
        }
    }


<span data-ttu-id="1f04f-237">La fonction définie par l'utilisateur peut ensuite être utilisée dans des requêtes comme dans l'exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="1f04f-237">The UDF can subsequently be used in queries like in the following sample:</span></span>

    // register UDF
    client.createUserDefinedFunctionAsync('dbs/testdb/colls/testColl', taxUdf)
        .then(function(response) { 
            console.log("Created", response.resource);

            var query = 'SELECT * FROM TaxPayers t WHERE udf.tax(t.income) > 20000'; 
            return client.queryDocuments('dbs/testdb/colls/testColl',
                   query).toArrayAsync();
        }, function(error) {
            console.log("Error" , error);
        })
    .then(function(response) {
        var documents = response.feed;
        console.log(response.resource); 
    }, function(error) {
        console.log("Error" , error);
    });

## <a name="javascript-language-integrated-query-api"></a><span data-ttu-id="1f04f-238">API de requête intégrée au langage JavaScript</span><span class="sxs-lookup"><span data-stu-id="1f04f-238">JavaScript language-integrated query API</span></span>
<span data-ttu-id="1f04f-239">En plus de l’émission de requêtes à l’aide de la grammaire SQL de DocumentDB, le kit SDK côté serveur vous permet d’effectuer des requêtes optimisées à l’aide d’une interface JavaScript fluide sans aucune connaissance de SQL.</span><span class="sxs-lookup"><span data-stu-id="1f04f-239">In addition to issuing queries using DocumentDB’s SQL grammar, the server-side SDK allows you to perform optimized queries using a fluent JavaScript interface without any knowledge of SQL.</span></span> <span data-ttu-id="1f04f-240">L’API de requête JavaScript permet de créer des requêtes par programme en transmettant des fonctions de prédicat dans des appels de fonction chaînables, avec une syntaxe connue des types prédéfinis de Array ECMAScript5 et des bibliothèques JavaScript courantes, telles que lodash.</span><span class="sxs-lookup"><span data-stu-id="1f04f-240">The JavaScript query API allows you to programmatically build queries by passing predicate functions into chainable function calls, with a syntax familiar to ECMAScript5's Array built-ins and popular JavaScript libraries like lodash.</span></span> <span data-ttu-id="1f04f-241">Les requêtes sont analysées par le runtime JavaScript pour être exécutées efficacement à l’aide d’index Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="1f04f-241">Queries are parsed by the JavaScript runtime to be executed efficiently using Azure Cosmos DB’s indices.</span></span>

> [!NOTE]
> <span data-ttu-id="1f04f-242">`__` (trait de soulignement double) est un alias pour `getContext().getCollection()`.</span><span class="sxs-lookup"><span data-stu-id="1f04f-242">`__` (double-underscore) is an alias to `getContext().getCollection()`.</span></span>
> <br/>
> <span data-ttu-id="1f04f-243">En d’autres termes, vous pouvez utiliser `__` ou `getContext().getCollection()` pour accéder à l’API de requête JavaScript.</span><span class="sxs-lookup"><span data-stu-id="1f04f-243">In other words, you can use `__` or `getContext().getCollection()` to access the JavaScript query API.</span></span>
> 
> 

<span data-ttu-id="1f04f-244">Les fonctions prises en charge sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="1f04f-244">Supported functions include:</span></span>

<ul>
<li><span data-ttu-id="1f04f-245">
<b>chain() ... .value([callback] [, options])</b>
</span><span class="sxs-lookup"><span data-stu-id="1f04f-245">
<b>chain() ... .value([callback] [, options])</b>
</span></span><ul>
<li>
<span data-ttu-id="1f04f-246">Commence un appel chaîné qui doit se terminer par value().</span><span class="sxs-lookup"><span data-stu-id="1f04f-246">Starts a chained call which must be terminated with value().</span></span>
</li>
</ul>
</li>
<li><span data-ttu-id="1f04f-247">
<b>filter(predicateFunction [, options] [, callback])</b>
</span><span class="sxs-lookup"><span data-stu-id="1f04f-247">
<b>filter(predicateFunction [, options] [, callback])</b>
</span></span><ul>
<li>
<span data-ttu-id="1f04f-248">Filtre l’entrée à l’aide d’une fonction de prédicat qui renvoie true/false afin de filtrer les documents d’entrée dans le jeu résultant.</span><span class="sxs-lookup"><span data-stu-id="1f04f-248">Filters the input using a predicate function which returns true/false in order to filter in/out input documents into the resulting set.</span></span> <span data-ttu-id="1f04f-249">Ce comportement est semblable à celui d’une clause WHERE dans SQL.</span><span class="sxs-lookup"><span data-stu-id="1f04f-249">This behaves similar to a WHERE clause in SQL.</span></span>
</li>
</ul>
</li>
<li><span data-ttu-id="1f04f-250">
<b>map(transformationFunction [, options] [, callback])</b>
</span><span class="sxs-lookup"><span data-stu-id="1f04f-250">
<b>map(transformationFunction [, options] [, callback])</b>
</span></span><ul>
<li>
<span data-ttu-id="1f04f-251">Applique une projection à partir d’une fonction de transformation qui mappe chaque élément d’entrée à une valeur ou un objet JavaScript.</span><span class="sxs-lookup"><span data-stu-id="1f04f-251">Applies a projection given a transformation function which maps each input item to a JavaScript object or value.</span></span> <span data-ttu-id="1f04f-252">Ce comportement est semblable à celui d’une clause SELECT dans SQL.</span><span class="sxs-lookup"><span data-stu-id="1f04f-252">This behaves similar to a SELECT clause in SQL.</span></span>
</li>
</ul>
</li>
<li><span data-ttu-id="1f04f-253">
<b>pluck([propertyName] [, options] [, callback])</b>
</span><span class="sxs-lookup"><span data-stu-id="1f04f-253">
<b>pluck([propertyName] [, options] [, callback])</b>
</span></span><ul>
<li>
<span data-ttu-id="1f04f-254">Ceci est un raccourci pour un mappage qui extrait la valeur d’une propriété unique de chaque élément d’entrée.</span><span class="sxs-lookup"><span data-stu-id="1f04f-254">This is a shortcut for a map which extracts the value of a single property from each input item.</span></span>
</li>
</ul>
</li>
<li><span data-ttu-id="1f04f-255">
<b>flatten([isShallow] [, options] [, callback])</b>
</span><span class="sxs-lookup"><span data-stu-id="1f04f-255">
<b>flatten([isShallow] [, options] [, callback])</b>
</span></span><ul>
<li>
<span data-ttu-id="1f04f-256">Combine et aplatit les tableaux à partir de chaque élément d’entrée en un seul tableau.</span><span class="sxs-lookup"><span data-stu-id="1f04f-256">Combines and flattens arrays from each input item in to a single array.</span></span> <span data-ttu-id="1f04f-257">Ce comportement est semblable à SelectMany dans LINQ.</span><span class="sxs-lookup"><span data-stu-id="1f04f-257">This behaves similar to SelectMany in LINQ.</span></span>
</li>
</ul>
</li>
<li><span data-ttu-id="1f04f-258">
<b>sortBy([predicate] [, options] [, callback])</b>
</span><span class="sxs-lookup"><span data-stu-id="1f04f-258">
<b>sortBy([predicate] [, options] [, callback])</b>
</span></span><ul>
<li>
<span data-ttu-id="1f04f-259">Produit un nouvel ensemble de documents en les triant dans le flux du document d’entrée dans l’ordre croissant à l’aide du prédicat donné.</span><span class="sxs-lookup"><span data-stu-id="1f04f-259">Produce a new set of documents by sorting the documents in the input document stream in ascending order using the given predicate.</span></span> <span data-ttu-id="1f04f-260">Ce comportement est semblable à celui d’une clause ORDER BY dans SQL.</span><span class="sxs-lookup"><span data-stu-id="1f04f-260">This behaves similar to a ORDER BY clause in SQL.</span></span>
</li>
</ul>
</li>
<li><span data-ttu-id="1f04f-261">
<b>sortByDescending([predicate] [, options] [, callback])</b>
</span><span class="sxs-lookup"><span data-stu-id="1f04f-261">
<b>sortByDescending([predicate] [, options] [, callback])</b>
</span></span><ul>
<li>
<span data-ttu-id="1f04f-262">Produit un nouvel ensemble de documents en les triant dans le flux du document d’entrée dans l’ordre décroissant à l’aide du prédicat donné.</span><span class="sxs-lookup"><span data-stu-id="1f04f-262">Produce a new set of documents by sorting the documents in the input document stream in descending order using the given predicate.</span></span> <span data-ttu-id="1f04f-263">Ce comportement est semblable à celui d’une clause ORDER BY x DESC dans SQL.</span><span class="sxs-lookup"><span data-stu-id="1f04f-263">This behaves similar to a ORDER BY x DESC clause in SQL.</span></span>
</li>
</ul>
</li>
</ul>


<span data-ttu-id="1f04f-264">Quand elles sont incluses dans les fonctions de prédicat et/ou de sélecteur, les constructions JavaScript suivantes sont automatiquement optimisées pour s’exécuter directement sur les index Azure Cosmos DB :</span><span class="sxs-lookup"><span data-stu-id="1f04f-264">When included inside predicate and/or selector functions, the following JavaScript constructs get automatically optimized to run directly on Azure Cosmos DB indices:</span></span>

* <span data-ttu-id="1f04f-265">Opérateurs simples : = + - * / % | ^ &amp; == != === !=== &lt; &gt; &lt;= &gt;= || &amp;&amp; &lt;&lt; &gt;&gt; &gt;&gt;&gt;!</span><span class="sxs-lookup"><span data-stu-id="1f04f-265">Simple operators: = + - * / % | ^ &amp; == != === !=== &lt; &gt; &lt;= &gt;= || &amp;&amp; &lt;&lt; &gt;&gt; &gt;&gt;&gt;!</span></span> ~
* <span data-ttu-id="1f04f-266">Littéraux, y compris le littéral d’objet : {}</span><span class="sxs-lookup"><span data-stu-id="1f04f-266">Literals, including the object literal: {}</span></span>
* <span data-ttu-id="1f04f-267">var, return</span><span class="sxs-lookup"><span data-stu-id="1f04f-267">var, return</span></span>

<span data-ttu-id="1f04f-268">Les constructions JavaScript suivantes ne sont pas optimisées pour les index Azure Cosmos DB :</span><span class="sxs-lookup"><span data-stu-id="1f04f-268">The following JavaScript constructs do not get optimized for Azure Cosmos DB indices:</span></span>

* <span data-ttu-id="1f04f-269">Flux de contrôle (par exemple, if, for, while)</span><span class="sxs-lookup"><span data-stu-id="1f04f-269">Control flow (e.g. if, for, while)</span></span>
* <span data-ttu-id="1f04f-270">Appels de fonction</span><span class="sxs-lookup"><span data-stu-id="1f04f-270">Function calls</span></span>

<span data-ttu-id="1f04f-271">Pour plus d’informations, voir [JSDocs côté serveur](http://azure.github.io/azure-documentdb-js-server/).</span><span class="sxs-lookup"><span data-stu-id="1f04f-271">For more information, please see our [Server-Side JSDocs](http://azure.github.io/azure-documentdb-js-server/).</span></span>

### <a name="example-write-a-stored-procedure-using-the-javascript-query-api"></a><span data-ttu-id="1f04f-272">Exemple : Écrire une procédure stockée à l’aide de l’API de requête JavaScript</span><span class="sxs-lookup"><span data-stu-id="1f04f-272">Example: Write a stored procedure using the JavaScript query API</span></span>
<span data-ttu-id="1f04f-273">L’exemple de code suivant illustre comment l’API de requête JavaScript peut être utilisée dans le contexte d’une procédure stockée.</span><span class="sxs-lookup"><span data-stu-id="1f04f-273">The following code sample is an example of how the JavaScript Query API can be used in the context of a stored procedure.</span></span> <span data-ttu-id="1f04f-274">La procédure stockée insère un document donné par un paramètre d’entrée et met à jour les métadonnées de document, à l’aide de la méthode `__.filter()` avec minSize, maxSize et totalSize basées sur la propriété de taille du document d’entrée.</span><span class="sxs-lookup"><span data-stu-id="1f04f-274">The stored procedure inserts a document, given by an input parameter, and updates a metadata document, using the `__.filter()` method, with minSize, maxSize, and totalSize based upon the input document's size property.</span></span>

    /**
     * Insert actual doc and update metadata doc: minSize, maxSize, totalSize based on doc.size.
     */
    function insertDocumentAndUpdateMetadata(doc) {
      // HTTP error codes sent to our callback funciton by DocDB server.
      var ErrorCode = {
        RETRY_WITH: 449,
      }

      var isAccepted = __.createDocument(__.getSelfLink(), doc, {}, function(err, doc, options) {
        if (err) throw err;

        // Check the doc (ignore docs with invalid/zero size and metaDoc itself) and call updateMetadata.
        if (!doc.isMetadata && doc.size > 0) {
          // Get the meta document. We keep it in the same collection. it's the only doc that has .isMetadata = true.
          var result = __.filter(function(x) {
            return x.isMetadata === true
          }, function(err, feed, options) {
            if (err) throw err;

            // We assume that metadata doc was pre-created and must exist when this script is called.
            if (!feed || !feed.length) throw new Error("Failed to find the metadata document.");

            // The metadata document.
            var metaDoc = feed[0];

            // Update metaDoc.minSize:
            // for 1st document use doc.Size, for all the rest see if it's less than last min.
            if (metaDoc.minSize == 0) metaDoc.minSize = doc.size;
            else metaDoc.minSize = Math.min(metaDoc.minSize, doc.size);

            // Update metaDoc.maxSize.
            metaDoc.maxSize = Math.max(metaDoc.maxSize, doc.size);

            // Update metaDoc.totalSize.
            metaDoc.totalSize += doc.size;

            // Update/replace the metadata document in the store.
            var isAccepted = __.replaceDocument(metaDoc._self, metaDoc, function(err) {
              if (err) throw err;
              // Note: in case concurrent updates causes conflict with ErrorCode.RETRY_WITH, we can't read the meta again 
              //       and update again because due to Snapshot isolation we will read same exact version (we are in same transaction).
              //       We have to take care of that on the client side.
            });
            if (!isAccepted) throw new Error("replaceDocument(metaDoc) returned false.");
          });
          if (!result.isAccepted) throw new Error("filter for metaDoc returned false.");
        }
      });
      if (!isAccepted) throw new Error("createDocument(actual doc) returned false.");
    }

## <a name="sql-to-javascript-cheat-sheet"></a><span data-ttu-id="1f04f-275">Aide-mémoire SQL vers Javascript</span><span class="sxs-lookup"><span data-stu-id="1f04f-275">SQL to Javascript cheat sheet</span></span>
<span data-ttu-id="1f04f-276">Le tableau suivant présente différentes requêtes SQL et les requêtes JavaScript correspondantes.</span><span class="sxs-lookup"><span data-stu-id="1f04f-276">The following table presents various SQL queries and the corresponding JavaScript queries.</span></span>

<span data-ttu-id="1f04f-277">Comme pour les requêtes SQL, les clés de propriété de document (par exemple, `doc.id`) respectent la casse.</span><span class="sxs-lookup"><span data-stu-id="1f04f-277">As with SQL queries, document property keys (e.g. `doc.id`) are case-sensitive.</span></span>

|<span data-ttu-id="1f04f-278">SQL</span><span class="sxs-lookup"><span data-stu-id="1f04f-278">SQL</span></span>| <span data-ttu-id="1f04f-279">API de requête JavaScript</span><span class="sxs-lookup"><span data-stu-id="1f04f-279">JavaScript Query API</span></span>|<span data-ttu-id="1f04f-280">Description ci-dessous</span><span class="sxs-lookup"><span data-stu-id="1f04f-280">Description below</span></span>|
|---|---|---|
|<span data-ttu-id="1f04f-281">SELECT *</span><span class="sxs-lookup"><span data-stu-id="1f04f-281">SELECT *</span></span><br><span data-ttu-id="1f04f-282">FROM docs</span><span class="sxs-lookup"><span data-stu-id="1f04f-282">FROM docs</span></span>| <span data-ttu-id="1f04f-283">__.map(function(doc) {</span><span class="sxs-lookup"><span data-stu-id="1f04f-283">__.map(function(doc) {</span></span> <br><span data-ttu-id="1f04f-284">&nbsp;&nbsp;&nbsp;&nbsp;return doc;</span><span class="sxs-lookup"><span data-stu-id="1f04f-284">&nbsp;&nbsp;&nbsp;&nbsp;return doc;</span></span><br><span data-ttu-id="1f04f-285">});</span><span class="sxs-lookup"><span data-stu-id="1f04f-285">});</span></span>|<span data-ttu-id="1f04f-286">1</span><span class="sxs-lookup"><span data-stu-id="1f04f-286">1</span></span>|
|<span data-ttu-id="1f04f-287">SELECT docs.id, docs.message AS msg, docs.actions</span><span class="sxs-lookup"><span data-stu-id="1f04f-287">SELECT docs.id, docs.message AS msg, docs.actions</span></span> <br><span data-ttu-id="1f04f-288">FROM docs</span><span class="sxs-lookup"><span data-stu-id="1f04f-288">FROM docs</span></span>|<span data-ttu-id="1f04f-289">__.map(function(doc) {</span><span class="sxs-lookup"><span data-stu-id="1f04f-289">__.map(function(doc) {</span></span><br><span data-ttu-id="1f04f-290">&nbsp;&nbsp;&nbsp;&nbsp;return {</span><span class="sxs-lookup"><span data-stu-id="1f04f-290">&nbsp;&nbsp;&nbsp;&nbsp;return {</span></span><br><span data-ttu-id="1f04f-291">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;id: doc.id,</span><span class="sxs-lookup"><span data-stu-id="1f04f-291">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;id: doc.id,</span></span><br><span data-ttu-id="1f04f-292">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;msg: doc.message,</span><span class="sxs-lookup"><span data-stu-id="1f04f-292">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;msg: doc.message,</span></span><br><span data-ttu-id="1f04f-293">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;actions:doc.actions</span><span class="sxs-lookup"><span data-stu-id="1f04f-293">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;actions:doc.actions</span></span><br><span data-ttu-id="1f04f-294">&nbsp;&nbsp;&nbsp;&nbsp;};</span><span class="sxs-lookup"><span data-stu-id="1f04f-294">&nbsp;&nbsp;&nbsp;&nbsp;};</span></span><br><span data-ttu-id="1f04f-295">});</span><span class="sxs-lookup"><span data-stu-id="1f04f-295">});</span></span>|<span data-ttu-id="1f04f-296">2</span><span class="sxs-lookup"><span data-stu-id="1f04f-296">2</span></span>|
|<span data-ttu-id="1f04f-297">SELECT *</span><span class="sxs-lookup"><span data-stu-id="1f04f-297">SELECT *</span></span><br><span data-ttu-id="1f04f-298">FROM docs</span><span class="sxs-lookup"><span data-stu-id="1f04f-298">FROM docs</span></span><br><span data-ttu-id="1f04f-299">WHERE docs.id="X998_Y998"</span><span class="sxs-lookup"><span data-stu-id="1f04f-299">WHERE docs.id="X998_Y998"</span></span>|<span data-ttu-id="1f04f-300">__.filter(function(doc) {</span><span class="sxs-lookup"><span data-stu-id="1f04f-300">__.filter(function(doc) {</span></span><br><span data-ttu-id="1f04f-301">&nbsp;&nbsp;&nbsp;&nbsp;return doc.id ==="X998_Y998";</span><span class="sxs-lookup"><span data-stu-id="1f04f-301">&nbsp;&nbsp;&nbsp;&nbsp;return doc.id ==="X998_Y998";</span></span><br><span data-ttu-id="1f04f-302">});</span><span class="sxs-lookup"><span data-stu-id="1f04f-302">});</span></span>|<span data-ttu-id="1f04f-303">3</span><span class="sxs-lookup"><span data-stu-id="1f04f-303">3</span></span>|
|<span data-ttu-id="1f04f-304">SELECT *</span><span class="sxs-lookup"><span data-stu-id="1f04f-304">SELECT *</span></span><br><span data-ttu-id="1f04f-305">FROM docs</span><span class="sxs-lookup"><span data-stu-id="1f04f-305">FROM docs</span></span><br><span data-ttu-id="1f04f-306">WHERE ARRAY_CONTAINS(docs.Tags, 123)</span><span class="sxs-lookup"><span data-stu-id="1f04f-306">WHERE ARRAY_CONTAINS(docs.Tags, 123)</span></span>|<span data-ttu-id="1f04f-307">__.filter(function(x) {</span><span class="sxs-lookup"><span data-stu-id="1f04f-307">__.filter(function(x) {</span></span><br><span data-ttu-id="1f04f-308">&nbsp;&nbsp;&nbsp;&nbsp;return x.Tags && x.Tags.indexOf(123) > -1;</span><span class="sxs-lookup"><span data-stu-id="1f04f-308">&nbsp;&nbsp;&nbsp;&nbsp;return x.Tags && x.Tags.indexOf(123) > -1;</span></span><br><span data-ttu-id="1f04f-309">});</span><span class="sxs-lookup"><span data-stu-id="1f04f-309">});</span></span>|<span data-ttu-id="1f04f-310">4</span><span class="sxs-lookup"><span data-stu-id="1f04f-310">4</span></span>|
|<span data-ttu-id="1f04f-311">SELECT docs.id, docs.message AS msg</span><span class="sxs-lookup"><span data-stu-id="1f04f-311">SELECT docs.id, docs.message AS msg</span></span><br><span data-ttu-id="1f04f-312">FROM docs</span><span class="sxs-lookup"><span data-stu-id="1f04f-312">FROM docs</span></span><br><span data-ttu-id="1f04f-313">WHERE docs.id="X998_Y998"</span><span class="sxs-lookup"><span data-stu-id="1f04f-313">WHERE docs.id="X998_Y998"</span></span>|<span data-ttu-id="1f04f-314">__.chain()</span><span class="sxs-lookup"><span data-stu-id="1f04f-314">__.chain()</span></span><br><span data-ttu-id="1f04f-315">&nbsp;&nbsp;&nbsp;&nbsp;.filter(function(doc) {</span><span class="sxs-lookup"><span data-stu-id="1f04f-315">&nbsp;&nbsp;&nbsp;&nbsp;.filter(function(doc) {</span></span><br><span data-ttu-id="1f04f-316">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return doc.id ==="X998_Y998";</span><span class="sxs-lookup"><span data-stu-id="1f04f-316">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return doc.id ==="X998_Y998";</span></span><br><span data-ttu-id="1f04f-317">&nbsp;&nbsp;&nbsp;&nbsp;})</span><span class="sxs-lookup"><span data-stu-id="1f04f-317">&nbsp;&nbsp;&nbsp;&nbsp;})</span></span><br><span data-ttu-id="1f04f-318">&nbsp;&nbsp;&nbsp;&nbsp;.map(function(doc) {</span><span class="sxs-lookup"><span data-stu-id="1f04f-318">&nbsp;&nbsp;&nbsp;&nbsp;.map(function(doc) {</span></span><br><span data-ttu-id="1f04f-319">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return {</span><span class="sxs-lookup"><span data-stu-id="1f04f-319">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return {</span></span><br><span data-ttu-id="1f04f-320">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;id: doc.id,</span><span class="sxs-lookup"><span data-stu-id="1f04f-320">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;id: doc.id,</span></span><br><span data-ttu-id="1f04f-321">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;msg: doc.message</span><span class="sxs-lookup"><span data-stu-id="1f04f-321">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;msg: doc.message</span></span><br><span data-ttu-id="1f04f-322">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;};</span><span class="sxs-lookup"><span data-stu-id="1f04f-322">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;};</span></span><br><span data-ttu-id="1f04f-323">&nbsp;&nbsp;&nbsp;&nbsp;})</span><span class="sxs-lookup"><span data-stu-id="1f04f-323">&nbsp;&nbsp;&nbsp;&nbsp;})</span></span><br><span data-ttu-id="1f04f-324">.value();</span><span class="sxs-lookup"><span data-stu-id="1f04f-324">.value();</span></span>|<span data-ttu-id="1f04f-325">5</span><span class="sxs-lookup"><span data-stu-id="1f04f-325">5</span></span>|
|<span data-ttu-id="1f04f-326">SELECT VALUE tag</span><span class="sxs-lookup"><span data-stu-id="1f04f-326">SELECT VALUE tag</span></span><br><span data-ttu-id="1f04f-327">FROM docs</span><span class="sxs-lookup"><span data-stu-id="1f04f-327">FROM docs</span></span><br><span data-ttu-id="1f04f-328">JOIN tag IN docs.Tags</span><span class="sxs-lookup"><span data-stu-id="1f04f-328">JOIN tag IN docs.Tags</span></span><br><span data-ttu-id="1f04f-329">ORDER BY docs._ts</span><span class="sxs-lookup"><span data-stu-id="1f04f-329">ORDER BY docs._ts</span></span>|<span data-ttu-id="1f04f-330">__.chain()</span><span class="sxs-lookup"><span data-stu-id="1f04f-330">__.chain()</span></span><br><span data-ttu-id="1f04f-331">&nbsp;&nbsp;&nbsp;&nbsp;.filter(function(doc) {</span><span class="sxs-lookup"><span data-stu-id="1f04f-331">&nbsp;&nbsp;&nbsp;&nbsp;.filter(function(doc) {</span></span><br><span data-ttu-id="1f04f-332">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return doc.Tags && Array.isArray(doc.Tags);</span><span class="sxs-lookup"><span data-stu-id="1f04f-332">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return doc.Tags && Array.isArray(doc.Tags);</span></span><br><span data-ttu-id="1f04f-333">&nbsp;&nbsp;&nbsp;&nbsp;})</span><span class="sxs-lookup"><span data-stu-id="1f04f-333">&nbsp;&nbsp;&nbsp;&nbsp;})</span></span><br><span data-ttu-id="1f04f-334">&nbsp;&nbsp;&nbsp;&nbsp;.sortBy(function(doc) {</span><span class="sxs-lookup"><span data-stu-id="1f04f-334">&nbsp;&nbsp;&nbsp;&nbsp;.sortBy(function(doc) {</span></span><br><span data-ttu-id="1f04f-335">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return doc._ts;</span><span class="sxs-lookup"><span data-stu-id="1f04f-335">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return doc._ts;</span></span><br><span data-ttu-id="1f04f-336">&nbsp;&nbsp;&nbsp;&nbsp;})</span><span class="sxs-lookup"><span data-stu-id="1f04f-336">&nbsp;&nbsp;&nbsp;&nbsp;})</span></span><br><span data-ttu-id="1f04f-337">&nbsp;&nbsp;&nbsp;&nbsp;.pluck("Tags")</span><span class="sxs-lookup"><span data-stu-id="1f04f-337">&nbsp;&nbsp;&nbsp;&nbsp;.pluck("Tags")</span></span><br><span data-ttu-id="1f04f-338">&nbsp;&nbsp;&nbsp;&nbsp;.flatten()</span><span class="sxs-lookup"><span data-stu-id="1f04f-338">&nbsp;&nbsp;&nbsp;&nbsp;.flatten()</span></span><br><span data-ttu-id="1f04f-339">&nbsp;&nbsp;&nbsp;&nbsp;.value()</span><span class="sxs-lookup"><span data-stu-id="1f04f-339">&nbsp;&nbsp;&nbsp;&nbsp;.value()</span></span>|<span data-ttu-id="1f04f-340">6</span><span class="sxs-lookup"><span data-stu-id="1f04f-340">6</span></span>|

<span data-ttu-id="1f04f-341">Les descriptions suivantes expliquent chaque requête du tableau ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="1f04f-341">The following descriptions explain each query in the table above.</span></span>
1. <span data-ttu-id="1f04f-342">Renvoie tous les documents (paginés avec jeton de continuation) tels quels.</span><span class="sxs-lookup"><span data-stu-id="1f04f-342">Results in all documents (paginated with continuation token) as is.</span></span>
2. <span data-ttu-id="1f04f-343">Projette l’ID, le message (alias msg) et l’action de tous les documents.</span><span class="sxs-lookup"><span data-stu-id="1f04f-343">Projects the id, message (aliased to msg), and action from all documents.</span></span>
3. <span data-ttu-id="1f04f-344">Requêtes pour les documents avec le prédicat : id = "X998_Y998".</span><span class="sxs-lookup"><span data-stu-id="1f04f-344">Queries for documents with the predicate: id = "X998_Y998".</span></span>
4. <span data-ttu-id="1f04f-345">Requêtes pour les documents comportant une propriété Tags, et Tags est un tableau contenant la valeur 123.</span><span class="sxs-lookup"><span data-stu-id="1f04f-345">Queries for documents that have a Tags property and Tags is an array containing the value 123.</span></span>
5. <span data-ttu-id="1f04f-346">Interroge les documents avec un prédicat, id = "X998_Y998", puis projette l’ID et le message (alias msg).</span><span class="sxs-lookup"><span data-stu-id="1f04f-346">Queries for documents with a predicate, id = "X998_Y998", and then projects the id and message (aliased to msg).</span></span>
6. <span data-ttu-id="1f04f-347">Filtre les documents comportant une propriété de tableau, Tags, trie les documents résultants par la propriété système _ts timestamp, puis projette et aplatit le tableau Tags.</span><span class="sxs-lookup"><span data-stu-id="1f04f-347">Filters for documents which have an array property, Tags, and sorts the resulting documents by the _ts timestamp system property, and then projects + flattens the Tags array.</span></span>


## <a name="runtime-support"></a><span data-ttu-id="1f04f-348">Prise en charge du runtime</span><span class="sxs-lookup"><span data-stu-id="1f04f-348">Runtime support</span></span>
<span data-ttu-id="1f04f-349">L’[API côté serveur JavaScript DocumentDB](http://azure.github.io/azure-documentdb-js-server/) offre la prise en charge de la plupart des fonctionnalités de langage JavaScript répondant à la norme [ECMA-262](http://www.ecma-international.org/publications/standards/Ecma-262.htm).</span><span class="sxs-lookup"><span data-stu-id="1f04f-349">[DocumentDB JavaScript server side API](http://azure.github.io/azure-documentdb-js-server/) provides support for the most of the mainstream JavaScript language features as standardized by [ECMA-262](http://www.ecma-international.org/publications/standards/Ecma-262.htm).</span></span>

### <a name="security"></a><span data-ttu-id="1f04f-350">Sécurité</span><span class="sxs-lookup"><span data-stu-id="1f04f-350">Security</span></span>
<span data-ttu-id="1f04f-351">Les déclencheurs et les procédures stockées JavaScript sont exécutés dans le bac à sable (sandbox) de façon à ce que les effets d'un script ne soient divulgués à un autre sans passer par l'isolement de transaction de capture instantanée au niveau de la base de données.</span><span class="sxs-lookup"><span data-stu-id="1f04f-351">JavaScript stored procedures and triggers are sandboxed so that the effects of one script do not leak to the other without going through the snapshot transaction isolation at the database level.</span></span> <span data-ttu-id="1f04f-352">Les environnements d'exécution sont regroupés mais leur contexte est nettoyé après chaque exécution.</span><span class="sxs-lookup"><span data-stu-id="1f04f-352">The runtime environments are pooled but cleaned of the context after each run.</span></span> <span data-ttu-id="1f04f-353">Par conséquent, ils sont assurés d'être préservés de tout effet secondaire inattendu les uns des autres.</span><span class="sxs-lookup"><span data-stu-id="1f04f-353">Hence they are guaranteed to be safe of any unintended side effects from each other.</span></span>

### <a name="pre-compilation"></a><span data-ttu-id="1f04f-354">Précompilation</span><span class="sxs-lookup"><span data-stu-id="1f04f-354">Pre-compilation</span></span>
<span data-ttu-id="1f04f-355">Les procédures stockées, les déclencheurs et les fonctions définies par l'utilisateur sont précompilés de façon implicite en format de code d'octet afin d'éviter les frais de compilation à chaque appel de script.</span><span class="sxs-lookup"><span data-stu-id="1f04f-355">Stored procedures, triggers and UDFs are implicitly precompiled to the byte code format in order to avoid compilation cost at the time of each script invocation.</span></span> <span data-ttu-id="1f04f-356">Cela permet de s'assurer que les appels de procédures stockées sont rapides et présentent un encombrement réduit.</span><span class="sxs-lookup"><span data-stu-id="1f04f-356">This ensures invocations of stored procedures are fast and have a low footprint.</span></span>

## <a name="client-sdk-support"></a><span data-ttu-id="1f04f-357">Prise en charge du kit SDK client</span><span class="sxs-lookup"><span data-stu-id="1f04f-357">Client SDK support</span></span>
<span data-ttu-id="1f04f-358">En plus de l’API DocumentDB pour le client [Node.js](documentdb-sdk-node.md), Azure Cosmos DB propose [.NET](documentdb-sdk-dotnet.md), [.NET Core](documentdb-sdk-dotnet-core.md), [Java](documentdb-sdk-java.md), [JavaScript](http://azure.github.io/azure-documentdb-js/) et les [Kits SDK Python](documentdb-sdk-python.md) pour l’API DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="1f04f-358">In addition to the DocumentDB API for [Node.js](documentdb-sdk-node.md) client, Azure Cosmos DB has [.NET](documentdb-sdk-dotnet.md), [.NET Core](documentdb-sdk-dotnet-core.md), [Java](documentdb-sdk-java.md), [JavaScript](http://azure.github.io/azure-documentdb-js/), and [Python SDKs](documentdb-sdk-python.md) for the DocumentDB API.</span></span> <span data-ttu-id="1f04f-359">Les procédures stockées, les déclencheurs et les fonctions définies par l'utilisateur peuvent être créés et exécutés au moyen de l'un de ces kits SDK également.</span><span class="sxs-lookup"><span data-stu-id="1f04f-359">Stored procedures, triggers and UDFs can be created and executed using any of these SDKs as well.</span></span> <span data-ttu-id="1f04f-360">Voici un exemple de la façon de créer et d'exécuter une procédure stockée au moyen du client .NET.</span><span class="sxs-lookup"><span data-stu-id="1f04f-360">The following example shows how to create and execute a stored procedure using the .NET client.</span></span> <span data-ttu-id="1f04f-361">Notez la façon dont les types .NET sont transmis dans la procédure stockée au format JSON et lus.</span><span class="sxs-lookup"><span data-stu-id="1f04f-361">Note how the .NET types are passed into the stored procedure as JSON and read back.</span></span>

    var markAntiquesSproc = new StoredProcedure
    {
        Id = "ValidateDocumentAge",
        Body = @"
                function(docToCreate, antiqueYear) {
                    var collection = getContext().getCollection();    
                    var response = getContext().getResponse();    

                    if(docToCreate.Year != undefined && docToCreate.Year < antiqueYear){
                        docToCreate.antique = true;
                    }

                    collection.createDocument(collection.getSelfLink(), docToCreate, {}, 
                        function(err, docCreated, options) { 
                            if(err) throw new Error('Error while creating document: ' + err.message);                              
                            if(options.maxCollectionSizeInMb == 0) throw 'max collection size not found'; 
                            response.setBody(docCreated);
                    });
             }"
    };

    // register stored procedure
    StoredProcedure createdStoredProcedure = await client.CreateStoredProcedureAsync(UriFactory.CreateDocumentCollectionUri("db", "coll"), markAntiquesSproc);
    dynamic document = new Document() { Id = "Borges_112" };
    document.Title = "Aleph";
    document.Year = 1949;

    // execute stored procedure
    Document createdDocument = await client.ExecuteStoredProcedureAsync<Document>(UriFactory.CreateStoredProcedureUri("db", "coll", "sproc"), document, 1920);


<span data-ttu-id="1f04f-362">Cet exemple illustre l’utilisation de l’[API .NET DocumentDB](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet) pour créer un prédéclencheur et un document dans lequel le déclencheur est activé.</span><span class="sxs-lookup"><span data-stu-id="1f04f-362">This sample shows how to use the [DocumentDB .NET API](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet) to create a pre-trigger and create a document with the trigger enabled.</span></span> 

    Trigger preTrigger = new Trigger()
    {
        Id = "CapitalizeName",
        Body = @"function() {
            var item = getContext().getRequest().getBody();
            item.id = item.id.toUpperCase();
            getContext().getRequest().setBody(item);
        }",
        TriggerOperation = TriggerOperation.Create,
        TriggerType = TriggerType.Pre
    };

    Document createdItem = await client.CreateDocumentAsync(UriFactory.CreateDocumentCollectionUri("db", "coll"), new Document { Id = "documentdb" },
        new RequestOptions
        {
            PreTriggerInclude = new List<string> { "CapitalizeName" },
        });


<span data-ttu-id="1f04f-363">Enfin, l’exemple suivant décrit comment créer une fonction définie par l’utilisateur et l’utiliser une [requête SQL de l’API DocumentDB](documentdb-sql-query.md).</span><span class="sxs-lookup"><span data-stu-id="1f04f-363">And the following example shows how to create a user defined function (UDF) and use it in a [DocumentDB API SQL query](documentdb-sql-query.md).</span></span>

    UserDefinedFunction function = new UserDefinedFunction()
    {
        Id = "LOWER",
        Body = @"function(input) 
        {
            return input.toLowerCase();
        }"
    };

    foreach (Book book in client.CreateDocumentQuery(UriFactory.CreateDocumentCollectionUri("db", "coll"),
        "SELECT * FROM Books b WHERE udf.LOWER(b.Title) = 'war and peace'"))
    {
        Console.WriteLine("Read {0} from query", book);
    }

## <a name="rest-api"></a><span data-ttu-id="1f04f-364">API REST</span><span class="sxs-lookup"><span data-stu-id="1f04f-364">REST API</span></span>
<span data-ttu-id="1f04f-365">Toutes les opérations Azure Cosmos DB peuvent être effectuées sur la base de l’architecture REST.</span><span class="sxs-lookup"><span data-stu-id="1f04f-365">All Azure Cosmos DB operations can be performed in a RESTful manner.</span></span> <span data-ttu-id="1f04f-366">Les procédures stockées, les déclencheurs et les fonctions définies par l'utilisateur peuvent être enregistrés dans une collection au moyen de HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="1f04f-366">Stored procedures, triggers and user-defined functions can be registered under a collection by using HTTP POST.</span></span> <span data-ttu-id="1f04f-367">Voici un exemple de la façon d'enregistrer une procédure stockée :</span><span class="sxs-lookup"><span data-stu-id="1f04f-367">The following is an example of how to register a stored procedure:</span></span>

    POST https://<url>/sprocs/ HTTP/1.1
    authorization: <<auth>>
    x-ms-date: Thu, 07 Aug 2014 03:43:10 GMT


    var x = {
      "name": "createAndAddProperty",
      "body": function (docToCreate, addedPropertyName, addedPropertyValue) {
                var collectionManager = getContext().getCollection();
                collectionManager.createDocument(
                    collectionManager.getSelfLink(),
                    docToCreate,
                    function(err, docCreated) {
                      if(err) throw new Error('Error:  ' + err.message);
                      docCreated[addedPropertyName] = addedPropertyValue;
                      getContext().getResponse().setBody(docCreated);
                    });
            }
    }


<span data-ttu-id="1f04f-368">La procédure stockée est enregistrée en exécutant une requête POST sur la base de l’URI dbs/testdb/colls/testColl/sprocs avec le corps contenant la procédure stockée à créer.</span><span class="sxs-lookup"><span data-stu-id="1f04f-368">The stored procedure is registered by executing a POST request against the URI dbs/testdb/colls/testColl/sprocs with the body containing the stored procedure to create.</span></span> <span data-ttu-id="1f04f-369">Les déclencheurs et les fonctions définies par l'utilisateur peuvent être inscrits de la même façon en émettant une demande POST sur /triggers et /udfs respectivement.</span><span class="sxs-lookup"><span data-stu-id="1f04f-369">Triggers and UDFs can be registered similarly by issuing a POST against /triggers and /udfs respectively.</span></span>
<span data-ttu-id="1f04f-370">Cette procédure stockée peut ensuite être exécutée en émettant une demande POST sur son lien de ressource :</span><span class="sxs-lookup"><span data-stu-id="1f04f-370">This stored procedure can then be executed by issuing a POST request against its resource link:</span></span>

    POST https://<url>/sprocs/<sproc> HTTP/1.1
    authorization: <<auth>>
    x-ms-date: Thu, 07 Aug 2014 03:43:20 GMT


    [ { "name": "TestDocument", "book": "Autumn of the Patriarch"}, "Price", 200 ]


<span data-ttu-id="1f04f-371">Ici, la valeur entrée pour la procédure stockée est transmise dans le corps de la requête.</span><span class="sxs-lookup"><span data-stu-id="1f04f-371">Here, the input to the stored procedure is passed in the request body.</span></span> <span data-ttu-id="1f04f-372">Notez que la valeur entrée est transmise en tant que tableau JSON de paramètres d'entrée.</span><span class="sxs-lookup"><span data-stu-id="1f04f-372">Note that the input is passed as a JSON array of input parameters.</span></span> <span data-ttu-id="1f04f-373">La procédure stockée prend la première entrée en tant que document correspondant à un corps de réponse.</span><span class="sxs-lookup"><span data-stu-id="1f04f-373">The stored procedure takes the first input as a document that is a response body.</span></span> <span data-ttu-id="1f04f-374">La réponse reçue se présente comme suit :</span><span class="sxs-lookup"><span data-stu-id="1f04f-374">The response we receive is as follows:</span></span>

    HTTP/1.1 200 OK

    { 
      name: 'TestDocument',
      book: ‘Autumn of the Patriarch’,
      id: ‘V7tQANV3rAkDAAAAAAAAAA==‘,
      ts: 1407830727,
      self: ‘dbs/V7tQAA==/colls/V7tQANV3rAk=/docs/V7tQANV3rAkDAAAAAAAAAA==/’,
      etag: ‘6c006596-0000-0000-0000-53e9cac70000’,
      attachments: ‘attachments/’,
      Price: 200
    }


<span data-ttu-id="1f04f-375">Contrairement aux procédures stockées, les déclencheurs ne peuvent pas être exécutés directement.</span><span class="sxs-lookup"><span data-stu-id="1f04f-375">Triggers, unlike stored procedures, cannot be executed directly.</span></span> <span data-ttu-id="1f04f-376">À la place, ils sont exécutés au sein d'une opération dans un document.</span><span class="sxs-lookup"><span data-stu-id="1f04f-376">Instead they are executed as part of an operation on a document.</span></span> <span data-ttu-id="1f04f-377">Nous pouvons spécifier les déclencheurs à exécuter avec une demande au moyen d'en-têtes HTTP.</span><span class="sxs-lookup"><span data-stu-id="1f04f-377">We can specify the triggers to run with a request using HTTP headers.</span></span> <span data-ttu-id="1f04f-378">Voici une demande de création de document.</span><span class="sxs-lookup"><span data-stu-id="1f04f-378">The following is request to create a document.</span></span>

    POST https://<url>/docs/ HTTP/1.1
    authorization: <<auth>>
    x-ms-date: Thu, 07 Aug 2014 03:43:10 GMT
    x-ms-documentdb-pre-trigger-include: validateDocumentContents 
    x-ms-documentdb-post-trigger-include: bookCreationPostTrigger


    {
       "name": "newDocument",
       “title”: “The Wizard of Oz”,
       “author”: “Frank Baum”,
       “pages”: 92
    }


<span data-ttu-id="1f04f-379">Ici, le pré-déclencheur devant s'exécuter avec la demande est spécifié dans l'en-tête x-ms-documentdb-pre-trigger-include.</span><span class="sxs-lookup"><span data-stu-id="1f04f-379">Here the pre-trigger to be run with the request is specified in the x-ms-documentdb-pre-trigger-include header.</span></span> <span data-ttu-id="1f04f-380">De même, tous les post-déclencheurs sont fournis dans l'en-tête x-ms-documentdb-post-trigger-include.</span><span class="sxs-lookup"><span data-stu-id="1f04f-380">Correspondingly, any post-triggers are given in the x-ms-documentdb-post-trigger-include header.</span></span> <span data-ttu-id="1f04f-381">Notez que les pré- et post-déclencheurs peuvent tous deux être spécifiés pour une demande donnée.</span><span class="sxs-lookup"><span data-stu-id="1f04f-381">Note that both pre- and post-triggers can be specified for a given request.</span></span>

## <a name="sample-code"></a><span data-ttu-id="1f04f-382">Exemple de code</span><span class="sxs-lookup"><span data-stu-id="1f04f-382">Sample code</span></span>
<span data-ttu-id="1f04f-383">Vous trouverez d’autres exemples de code côté serveur (notamment [bulk-delete](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples/stored-procedures/bulkDelete.js) et [update](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples/stored-procedures/update.js)) dans notre [référentiel GitHub](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples).</span><span class="sxs-lookup"><span data-stu-id="1f04f-383">You can find more server-side code examples (including [bulk-delete](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples/stored-procedures/bulkDelete.js), and [update](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples/stored-procedures/update.js)) on our [GitHub repository](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples).</span></span>

<span data-ttu-id="1f04f-384">Vous souhaitez partager votre remarquable procédure stockée ?</span><span class="sxs-lookup"><span data-stu-id="1f04f-384">Want to share your awesome stored procedure?</span></span> <span data-ttu-id="1f04f-385">Envoyez-nous une requête d’extraction !</span><span class="sxs-lookup"><span data-stu-id="1f04f-385">Please, send us a pull-request!</span></span> 

## <a name="next-steps"></a><span data-ttu-id="1f04f-386">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1f04f-386">Next steps</span></span>
<span data-ttu-id="1f04f-387">Après avoir créé des procédures stockées, des déclencheurs et des fonctions définies par l’utilisateur, vous pouvez les charger et les afficher dans le portail Azure à l’aide de l’Explorateur de données.</span><span class="sxs-lookup"><span data-stu-id="1f04f-387">Once you have one or more stored procedures, triggers, and user-defined functions created, you can load them and view them in the Azure portal using Data Explorer.</span></span>

<span data-ttu-id="1f04f-388">Pour en savoir plus sur la programmation Azure Cosmos DB côté serveur, vous pouvez également trouver utiles les références et les ressources suivantes :</span><span class="sxs-lookup"><span data-stu-id="1f04f-388">You may also find the following references and resources useful in your path to learn more about Azure Cosmos dB server-side programming:</span></span>

* [<span data-ttu-id="1f04f-389">Kits SDK Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="1f04f-389">Azure Cosmos DB SDKs</span></span>](documentdb-sdk-dotnet.md)
* [<span data-ttu-id="1f04f-390">Studio DocumentDB</span><span class="sxs-lookup"><span data-stu-id="1f04f-390">DocumentDB Studio</span></span>](https://github.com/mingaliu/DocumentDBStudio/releases)
* [<span data-ttu-id="1f04f-391">JSON</span><span class="sxs-lookup"><span data-stu-id="1f04f-391">JSON</span></span>](http://www.json.org/) 
* [<span data-ttu-id="1f04f-392">JavaScript ECMA-262</span><span class="sxs-lookup"><span data-stu-id="1f04f-392">JavaScript ECMA-262</span></span>](http://www.ecma-international.org/publications/standards/Ecma-262.htm)
* [<span data-ttu-id="1f04f-393">Extensibilité de la base de données sécurisée et portable</span><span class="sxs-lookup"><span data-stu-id="1f04f-393">Secure and Portable Database Extensibility</span></span>](http://dl.acm.org/citation.cfm?id=276339) 
* [<span data-ttu-id="1f04f-394">Architecture de base de données orientée services</span><span class="sxs-lookup"><span data-stu-id="1f04f-394">Service Oriented Database Architecture</span></span>](http://dl.acm.org/citation.cfm?id=1066267&coll=Portal&dl=GUIDE) 
* [<span data-ttu-id="1f04f-395">Hébergement du Runtime .NET dans Microsoft SQL Server</span><span class="sxs-lookup"><span data-stu-id="1f04f-395">Hosting the .NET Runtime in Microsoft SQL server</span></span>](http://dl.acm.org/citation.cfm?id=1007669)

