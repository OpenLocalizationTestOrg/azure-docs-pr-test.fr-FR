---
title: "programmation de JavaScript côté aaaServer pour la base de données Azure Cosmos | Documents Microsoft"
description: "Découvrez comment toowrite de base de données Azure Cosmos toouse procédures stockées, les déclencheurs de base de données et les fonctions définies par l’utilisateur (UDF) dans JavaScript. Obtenez notamment des conseils en matière de programmation de base de données."
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
ms.openlocfilehash: 5a011d1c4b0b5908d5de73607a1bc328ed1711d0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-server-side-programming-stored-procedures-database-triggers-and-udfs"></a><span data-ttu-id="224e8-105">Programmation Azure Cosmos DB côté serveur : procédures stockées, déclencheurs de base de données et fonctions définies par l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="224e8-105">Azure Cosmos DB server-side programming: Stored procedures, database triggers, and UDFs</span></span>
<span data-ttu-id="224e8-106">Découvrez comment l’exécution transactionnelle de JavaScript intégrée au langage d’Azure Cosmos DB permet aux développeurs d’écrire des **procédures stockées**, des **déclencheurs** et des **fonctions définies par l’utilisateur (FDU)** en mode natif dans une version [ECMAScript 2015](http://www.ecma-international.org/ecma-262/6.0/) pour JavaScript.</span><span class="sxs-lookup"><span data-stu-id="224e8-106">Learn how Azure Cosmos DB’s language integrated, transactional execution of JavaScript lets developers write **stored procedures**, **triggers** and **user defined functions (UDFs)** natively in an [ECMAScript 2015](http://www.ecma-international.org/ecma-262/6.0/) JavaScript.</span></span> <span data-ttu-id="224e8-107">Cela vous permet de logique d’application toowrite base de données programme qui peut être livrée et exécutée directement sur les partitions de stockage de base de données hello.</span><span class="sxs-lookup"><span data-stu-id="224e8-107">This allows you toowrite database program application logic that can be shipped and executed directly on hello database storage partitions.</span></span> 

<span data-ttu-id="224e8-108">Nous vous recommandons de mise en route démarrée par regarder hello suivant vidéo, où Andrew Liu fournit une brève introduction de tooCosmos de base de données modèle de programmation côté serveur de base de données.</span><span class="sxs-lookup"><span data-stu-id="224e8-108">We recommend getting started by watching hello following video, where Andrew Liu provides a brief introduction tooCosmos DB's server-side database programming model.</span></span> 

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-Demo-A-Quick-Intro-to-Azure-DocumentDBs-Server-Side-Javascript/player]
> 
> 

<span data-ttu-id="224e8-109">Ensuite, retourner toothis article, où vous allez apprendre toohello de réponses hello suivant questions :</span><span class="sxs-lookup"><span data-stu-id="224e8-109">Then, return toothis article, where you'll learn hello answers toohello following questions:</span></span>  

* <span data-ttu-id="224e8-110">Comment écrire une procédure stockée, un déclencheur ou une fonction définie par l'utilisateur à l'aide de JavaScript ?</span><span class="sxs-lookup"><span data-stu-id="224e8-110">How do I write a a stored procedure, trigger, or UDF using JavaScript?</span></span>
* <span data-ttu-id="224e8-111">Comment Azure Cosmos DB offre-il une garantie ACID ?</span><span class="sxs-lookup"><span data-stu-id="224e8-111">How does Cosmos DB guarantee ACID?</span></span>
* <span data-ttu-id="224e8-112">Comment les transactions fonctionnent-elles dans Azure Cosmos DB ?</span><span class="sxs-lookup"><span data-stu-id="224e8-112">How do transactions work in Cosmos DB?</span></span>
* <span data-ttu-id="224e8-113">Qu'est-ce que les pré-déclencheurs et les post-déclencheurs, et comment procède-t-on pour leur écriture ?</span><span class="sxs-lookup"><span data-stu-id="224e8-113">What are pre-triggers and post-triggers and how do I write one?</span></span>
* <span data-ttu-id="224e8-114">Comment enregistrer et exécuter une procédure stockée, un déclencheur ou une fonction définie par l'utilisateur sur la base de l'architecture REST avec HTTP ?</span><span class="sxs-lookup"><span data-stu-id="224e8-114">How do I register and execute a stored procedure, trigger, or UDF in a RESTful manner by using HTTP?</span></span>
* <span data-ttu-id="224e8-115">Les kits de développement logiciel Cosmos DB toocreate disponible et exécutez et procédures stockées, déclencheurs, UDF ?</span><span class="sxs-lookup"><span data-stu-id="224e8-115">What Cosmos DB SDKs are available toocreate and execute stored procedures, triggers, and UDFs?</span></span>

## <a name="introduction-toostored-procedure-and-udf-programming"></a><span data-ttu-id="224e8-116">Introduction tooStored procédure et la programmation des UDF</span><span class="sxs-lookup"><span data-stu-id="224e8-116">Introduction tooStored Procedure and UDF Programming</span></span>
<span data-ttu-id="224e8-117">Cette approche de *« JavaScript sous la forme d’un jour modern T-SQL »* évite aux développeurs d’application de la complexité hello des incompatibilités au niveau du système de type et les technologies de mappage relationnel objet.</span><span class="sxs-lookup"><span data-stu-id="224e8-117">This approach of *“JavaScript as a modern day T-SQL”* frees application developers from hello complexities of type system mismatches and object-relational mapping technologies.</span></span> <span data-ttu-id="224e8-118">Elle comporte également plusieurs avantages intrinsèques qui peuvent être des applications riches toobuild utilisé :</span><span class="sxs-lookup"><span data-stu-id="224e8-118">It also has a number of intrinsic advantages that can be utilized toobuild rich applications:</span></span>  

* <span data-ttu-id="224e8-119">**Logique procédurale :** JavaScript sous la forme d’un langage de programmation de haut niveau, fournit une interface riche et familière de tooexpress une logique métier.</span><span class="sxs-lookup"><span data-stu-id="224e8-119">**Procedural Logic:** JavaScript as a high level programming language, provides a rich and familiar interface tooexpress business logic.</span></span> <span data-ttu-id="224e8-120">Vous pouvez effectuer des séquences de données toohello proche des opérations complexes.</span><span class="sxs-lookup"><span data-stu-id="224e8-120">You can perform complex sequences of operations closer toohello data.</span></span>
* <span data-ttu-id="224e8-121">**Transactions atomiques :** Azure Cosmos DB garantit que les opérations de base de données effectuées dans un déclencheur ou une procédure stockée sont atomiques.</span><span class="sxs-lookup"><span data-stu-id="224e8-121">**Atomic Transactions:** Cosmos DB guarantees that database operations performed inside a single stored procedure or trigger are atomic.</span></span> <span data-ttu-id="224e8-122">Cela permet à une application de combiner des applications connexes en un seul lot de façon à ce que toutes réussissent ou qu’aucune ne réussisse.</span><span class="sxs-lookup"><span data-stu-id="224e8-122">This lets an application combine related operations in a single batch so that either all of them succeed or none of them succeed.</span></span> 
* <span data-ttu-id="224e8-123">**Performances :** hello fait que JSON est le système de type de langage Javascript toohello intrinsèquement mappé et est également permet à l’unité de stockage dans la base de données Cosmos hello pour un nombre d’optimisations de matérialisation différée de JSON documents dans la mémoire tampon de hello pool des rendre disponibles à la demande toohello l’exécution de code.</span><span class="sxs-lookup"><span data-stu-id="224e8-123">**Performance:** hello fact that JSON is intrinsically mapped toohello Javascript language type system and is also hello basic unit of storage in Cosmos DB allows for a number of optimizations like lazy materialization of JSON documents in hello buffer pool and making them available on-demand toohello executing code.</span></span> <span data-ttu-id="224e8-124">Il existe des gains de performance plus associés avec l’envoi de journaux de base de données toohello de logique métier :</span><span class="sxs-lookup"><span data-stu-id="224e8-124">There are more performance benefits associated with shipping business logic toohello database:</span></span>
  
  * <span data-ttu-id="224e8-125">Traitement par lot - Les développeurs peuvent regrouper les opérations telles que les insertions et les envoyer en bloc.</span><span class="sxs-lookup"><span data-stu-id="224e8-125">Batching – Developers can group operations like inserts and submit them in bulk.</span></span> <span data-ttu-id="224e8-126">coût de la latence du trafic réseau Hello et des transactions distinctes hello magasin toocreate généraux sont considérablement réduites.</span><span class="sxs-lookup"><span data-stu-id="224e8-126">hello network traffic latency cost and hello store overhead toocreate separate transactions are reduced significantly.</span></span> 
  * <span data-ttu-id="224e8-127">Précompilation – Cosmos DB précompilation des procédures stockées, déclencheurs et définies par l’utilisateur (UDF) de fonctions tooavoid le coût de compilation JavaScript pour chaque appel.</span><span class="sxs-lookup"><span data-stu-id="224e8-127">Pre-compilation – Cosmos DB precompiles stored procedures, triggers and user defined functions (UDFs) tooavoid JavaScript compilation cost for each invocation.</span></span> <span data-ttu-id="224e8-128">Hello surcharge de la création de code d’octet hello pour la logique procédurale de hello est amorti tooa présenter d’avantage.</span><span class="sxs-lookup"><span data-stu-id="224e8-128">hello overhead of building hello byte code for hello procedural logic is amortized tooa minimal value.</span></span>
  * <span data-ttu-id="224e8-129">Séquencement - De nombreuses opérations requièrent un effet secondaire (« déclencheur ») qui implique potentiellement d'effectuer une ou plusieurs opérations de stockage secondaires.</span><span class="sxs-lookup"><span data-stu-id="224e8-129">Sequencing – Many operations need a side-effect (“trigger”) that potentially involves doing one or many secondary store operations.</span></span> <span data-ttu-id="224e8-130">À part l’atomicité, il est plus performant lorsque déplacées toohello server.</span><span class="sxs-lookup"><span data-stu-id="224e8-130">Aside from atomicity, this is more performant when moved toohello server.</span></span> 
* <span data-ttu-id="224e8-131">**Encapsulation :** les procédures stockées peuvent être logique toogroup utilisé dans un seul emplacement.</span><span class="sxs-lookup"><span data-stu-id="224e8-131">**Encapsulation:** Stored procedures can be used toogroup business logic in one place.</span></span> <span data-ttu-id="224e8-132">Ceci présente deux avantages :</span><span class="sxs-lookup"><span data-stu-id="224e8-132">This has two advantages:</span></span>
  * <span data-ttu-id="224e8-133">Il ajoute une couche d’abstraction sur les données brutes de hello, qui permet aux données architectes tooevolve leurs applications indépendamment à partir des données de hello.</span><span class="sxs-lookup"><span data-stu-id="224e8-133">It adds an abstraction layer on top of hello raw data, which enables data architects tooevolve their applications independently from hello data.</span></span> <span data-ttu-id="224e8-134">Cela est particulièrement avantageux lorsque les données de salutation sont sans schéma, en raison des hypothèses fragile toohello qui peuvent nécessiter une toobe intégrée application hello s’ils ont toodeal avec des données directement.</span><span class="sxs-lookup"><span data-stu-id="224e8-134">This is particularly advantageous when hello data is schema-less, due toohello brittle assumptions that may need toobe baked into hello application if they have toodeal with data directly.</span></span>  
  * <span data-ttu-id="224e8-135">Cette abstraction permet aux entreprises de sécuriser leurs données en rationalisant l’accès à partir de scripts de hello hello.</span><span class="sxs-lookup"><span data-stu-id="224e8-135">This abstraction lets enterprises keep their data secure by streamlining hello access from hello scripts.</span></span>  

<span data-ttu-id="224e8-136">Hello création et l’exécution des déclencheurs de base de données, d’une procédure stockée et d’opérateurs de requête personnalisée est pris en charge par le biais hello [API REST](/rest/api/documentdb/), [Azure DocumentDB Studio](https://github.com/mingaliu/DocumentDBStudio/releases), et [client SDK](documentdb-sdk-dotnet.md) sur de nombreuses plateformes, y compris .NET, Node.js et JavaScript.</span><span class="sxs-lookup"><span data-stu-id="224e8-136">hello creation and execution of database triggers, stored procedure and custom query operators is supported through hello [REST API](/rest/api/documentdb/), [Azure DocumentDB Studio](https://github.com/mingaliu/DocumentDBStudio/releases), and [client SDKs](documentdb-sdk-dotnet.md) in many platforms including .NET, Node.js and JavaScript.</span></span>

<span data-ttu-id="224e8-137">Ce didacticiel utilise hello [SDK Node.js avec Q promesses](http://azure.github.io/azure-documentdb-node-q/) tooillustrate syntaxe et l’utilisation de procédures stockées, des déclencheurs et des UDF.</span><span class="sxs-lookup"><span data-stu-id="224e8-137">This tutorial uses hello [Node.js SDK with Q Promises](http://azure.github.io/azure-documentdb-node-q/) tooillustrate syntax and usage of stored procedures, triggers, and UDFs.</span></span>   

## <a name="stored-procedures"></a><span data-ttu-id="224e8-138">Procédures stockées</span><span class="sxs-lookup"><span data-stu-id="224e8-138">Stored procedures</span></span>
### <a name="example-write-a-simple-stored-procedure"></a><span data-ttu-id="224e8-139">Exemple : Écriture d’une simple procédure stockée</span><span class="sxs-lookup"><span data-stu-id="224e8-139">Example: Write a simple stored procedure</span></span>
<span data-ttu-id="224e8-140">Commençons par une simple procédure stockée qui renvoie une réponse « Hello World ».</span><span class="sxs-lookup"><span data-stu-id="224e8-140">Let’s start with a simple stored procedure that returns a “Hello World” response.</span></span>

    var helloWorldStoredProc = {
        id: "helloWorld",
        serverScript: function () {
            var context = getContext();
            var response = context.getResponse();

            response.setBody("Hello, World");
        }
    }


<span data-ttu-id="224e8-141">Les procédures stockées sont enregistrées par collection, et elles peuvent s'appliquer à tout document et toute pièce jointe figurant dans cette collection.</span><span class="sxs-lookup"><span data-stu-id="224e8-141">Stored procedures are registered per collection, and can operate on any document and attachment present in that collection.</span></span> <span data-ttu-id="224e8-142">Hello extrait de code suivant montre comment tooregister hello helloWorld procédure stockée avec une collection.</span><span class="sxs-lookup"><span data-stu-id="224e8-142">hello following snippet shows how tooregister hello helloWorld stored procedure with a collection.</span></span> 

    // register hello stored procedure
    var createdStoredProcedure;
    client.createStoredProcedureAsync('dbs/testdb/colls/testColl', helloWorldStoredProc)
        .then(function (response) {
            createdStoredProcedure = response.resource;
            console.log("Successfully created stored procedure");
        }, function (error) {
            console.log("Error", error);
        });


<span data-ttu-id="224e8-143">Une fois la procédure stockée hello est inscrit, nous pouvons exécuter par rapport à la collection de hello et lire hello les résultats au client de hello.</span><span class="sxs-lookup"><span data-stu-id="224e8-143">Once hello stored procedure is registered, we can execute it against hello collection, and read hello results back at hello client.</span></span> 

    // execute hello stored procedure
    client.executeStoredProcedureAsync('dbs/testdb/colls/testColl/sprocs/helloWorld')
        .then(function (response) {
            console.log(response.result); // "Hello, World"
        }, function (err) {
            console.log("Error", error);
        });


<span data-ttu-id="224e8-144">objet de contexte Hello fournit l’accès tooall les opérations qui peuvent être effectuées sur le stockage de base de données Cosmos, ainsi que pour accéder aux objets de demande et de réponse toohello.</span><span class="sxs-lookup"><span data-stu-id="224e8-144">hello context object provides access tooall operations that can be performed on Cosmos DB storage, as well as access toohello request and response objects.</span></span> <span data-ttu-id="224e8-145">Dans ce cas, nous avons utilisé hello objet tooset hello corps de réponse de réponse hello qui a été envoyé arrière toohello client.</span><span class="sxs-lookup"><span data-stu-id="224e8-145">In this case, we used hello response object tooset hello body of hello response that was sent back toohello client.</span></span> <span data-ttu-id="224e8-146">Pour plus d’informations, consultez toohello [JavaScript de base de données Azure Cosmos server documentation SDK](http://azure.github.io/azure-documentdb-js-server/).</span><span class="sxs-lookup"><span data-stu-id="224e8-146">For more details, refer toohello [Azure Cosmos DB JavaScript server SDK documentation](http://azure.github.io/azure-documentdb-js-server/).</span></span>  

<span data-ttu-id="224e8-147">Nous développer cet exemple et ajouter plusieurs fonctionnalités de la base de données toohello de procédure stockée.</span><span class="sxs-lookup"><span data-stu-id="224e8-147">Let us expand on this example and add more database related functionality toohello stored procedure.</span></span> <span data-ttu-id="224e8-148">Les procédures stockées peuvent créer, mettre à jour, lire, interroger et supprimer des documents et pièces jointes à l’intérieur de la collection de hello.</span><span class="sxs-lookup"><span data-stu-id="224e8-148">Stored procedures can create, update, read, query and delete documents and attachments inside hello collection.</span></span>    

### <a name="example-write-a-stored-procedure-toocreate-a-document"></a><span data-ttu-id="224e8-149">Exemple : Écrire une procédure stockée de toocreate un document</span><span class="sxs-lookup"><span data-stu-id="224e8-149">Example: Write a stored procedure toocreate a document</span></span>
<span data-ttu-id="224e8-150">extrait de code Hello suivant montre comment toouse hello toointeract d’objet de contexte avec des ressources de base de données Cosmos.</span><span class="sxs-lookup"><span data-stu-id="224e8-150">hello next snippet shows how toouse hello context object toointeract with Cosmos DB resources.</span></span>

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


<span data-ttu-id="224e8-151">Cette procédure stockée accepte comme entrée documentToCreate, corps hello d’un toobe document créé dans la collection actuelle de hello.</span><span class="sxs-lookup"><span data-stu-id="224e8-151">This stored procedure takes as input documentToCreate, hello body of a document toobe created in hello current collection.</span></span> <span data-ttu-id="224e8-152">Toutes ces opérations sont asynchrones et dépendent de rappels de fonction JavaScript.</span><span class="sxs-lookup"><span data-stu-id="224e8-152">All such operations are asynchronous and depend on JavaScript function callbacks.</span></span> <span data-ttu-id="224e8-153">fonction de rappel Hello possède deux paramètres, un pour l’objet d’erreur hello hello échoue et l’autre pour hello créé l’objet.</span><span class="sxs-lookup"><span data-stu-id="224e8-153">hello callback function has two parameters, one for hello error object in case hello operation fails, and one for hello created object.</span></span> <span data-ttu-id="224e8-154">À l’intérieur du rappel de hello, les utilisateurs peuvent gérer l’exception de hello ou lever une erreur.</span><span class="sxs-lookup"><span data-stu-id="224e8-154">Inside hello callback, users can either handle hello exception or throw an error.</span></span> <span data-ttu-id="224e8-155">Si un rappel n’est pas fourni, et il existe une erreur, le runtime de base de données Azure Cosmos hello génère une erreur.</span><span class="sxs-lookup"><span data-stu-id="224e8-155">In case a callback is not provided and there is an error, hello Azure Cosmos DB runtime throws an error.</span></span>   

<span data-ttu-id="224e8-156">Dans l’exemple hello ci-dessus, le rappel de hello génère une erreur en cas d’échec de l’opération de hello.</span><span class="sxs-lookup"><span data-stu-id="224e8-156">In hello example above, hello callback throws an error if hello operation failed.</span></span> <span data-ttu-id="224e8-157">Sinon, il définit les id hello Hello créé le document en tant que corps hello du client de toohello réponse hello.</span><span class="sxs-lookup"><span data-stu-id="224e8-157">Otherwise, it sets hello id of hello created document as hello body of hello response toohello client.</span></span> <span data-ttu-id="224e8-158">Voici la façon dont cette procédure stockée est exécutée avec des paramètres d'entrée.</span><span class="sxs-lookup"><span data-stu-id="224e8-158">Here is how this stored procedure is executed with input parameters.</span></span>

    // register hello stored procedure
    client.createStoredProcedureAsync('dbs/testdb/colls/testColl', createDocumentStoredProc)
        .then(function (response) {
            var createdStoredProcedure = response.resource;

            // run stored procedure toocreate a document
            var docToCreate = {
                id: "DocFromSproc",
                book: "hello Hitchhiker’s Guide toohello Galaxy",
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


<span data-ttu-id="224e8-159">Notez que cette procédure stockée peut tootake modifié un tableau d’instances de document en tant qu’entrée et créer les hello même stockée dans l’exécution de la procédure au lieu de réseau de plusieurs demandes toocreate d'entre eux individuellement.</span><span class="sxs-lookup"><span data-stu-id="224e8-159">Note that this stored procedure can be modified tootake an array of document bodies as input and create them all in hello same stored procedure execution instead of multiple network requests toocreate each of them individually.</span></span> <span data-ttu-id="224e8-160">Cela peut être utilisé tooimplement un importateur en bloc efficace pour DB Cosmos (décrit plus loin dans ce didacticiel).</span><span class="sxs-lookup"><span data-stu-id="224e8-160">This can be used tooimplement an efficient bulk importer for Cosmos DB (discussed later in this tutorial).</span></span>   

<span data-ttu-id="224e8-161">exemple Hello décrit a montré comment toouse des procédures stockées.</span><span class="sxs-lookup"><span data-stu-id="224e8-161">hello example described demonstrated how toouse stored procedures.</span></span> <span data-ttu-id="224e8-162">Nous allons aborder les déclencheurs et les fonctions définies par l’utilisateur (UDF) plus loin dans le didacticiel de hello.</span><span class="sxs-lookup"><span data-stu-id="224e8-162">We will cover triggers and user defined functions (UDFs) later in hello tutorial.</span></span>

## <a name="database-program-transactions"></a><span data-ttu-id="224e8-163">Transactions de programme de base de données</span><span class="sxs-lookup"><span data-stu-id="224e8-163">Database program transactions</span></span>
<span data-ttu-id="224e8-164">Une transaction dans une base de données classique peut être définie comme étant une séquence d'opérations effectuées en tant qu'unité de travail logique unique.</span><span class="sxs-lookup"><span data-stu-id="224e8-164">Transaction in a typical database can be defined as a sequence of operations performed as a single logical unit of work.</span></span> <span data-ttu-id="224e8-165">Chaque transaction offre des **garanties ACID**.</span><span class="sxs-lookup"><span data-stu-id="224e8-165">Each transaction provides **ACID guarantees**.</span></span> <span data-ttu-id="224e8-166">ACID est un acronyme bien connu qui est l’abréviation de quatre propriétés : Atomicité, Cohérence, Isolation et Durabilité.</span><span class="sxs-lookup"><span data-stu-id="224e8-166">ACID is a well-known acronym that stands for four properties -  Atomicity, Consistency, Isolation and Durability.</span></span>  

<span data-ttu-id="224e8-167">En bref, l’atomicité garantit que tout le travail hello effectué à l’intérieur d’une transaction est considéré comme une unité unique où soit sont validées ou none.</span><span class="sxs-lookup"><span data-stu-id="224e8-167">Briefly, atomicity guarantees that all hello work done inside a transaction is treated as a single unit where either all of it is committed or none.</span></span> <span data-ttu-id="224e8-168">Cohérence permet de s’assurer que les données de salutation sont toujours en bon état interne entre les transactions.</span><span class="sxs-lookup"><span data-stu-id="224e8-168">Consistency makes sure that hello data is always in a good internal state across transactions.</span></span> <span data-ttu-id="224e8-169">Isolation garantit que deux transactions n’interfèrent avec d’autres : en général, la plupart des systèmes de fournissent plusieurs niveaux d’isolement qui peuvent être utilisés selon les besoins de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="224e8-169">Isolation guarantees that no two transactions interfere with each other – generally, most commercial systems provide multiple isolation levels that can be used based on hello application needs.</span></span> <span data-ttu-id="224e8-170">Durabilité garantit que toute modification est validée dans la base de données hello sera toujours présente.</span><span class="sxs-lookup"><span data-stu-id="224e8-170">Durability ensures that any change that’s committed in hello database will always be present.</span></span>   

<span data-ttu-id="224e8-171">Dans la base de données Cosmos, JavaScript est hébergé dans hello même espace mémoire en tant que base de données hello.</span><span class="sxs-lookup"><span data-stu-id="224e8-171">In Cosmos DB, JavaScript is hosted in hello same memory space as hello database.</span></span> <span data-ttu-id="224e8-172">Par conséquent, les demandes effectuées au sein des procédures stockées et les déclencheurs s’exécutent dans hello même étendue d’une session de base de données.</span><span class="sxs-lookup"><span data-stu-id="224e8-172">Hence, requests made within stored procedures and triggers execute in hello same scope of a database session.</span></span> <span data-ttu-id="224e8-173">Cela permet de Cosmos DB tooguarantee ACID pour toutes les opérations qui font partie d’un seul procédure stocké/déclencheur.</span><span class="sxs-lookup"><span data-stu-id="224e8-173">This enables Cosmos DB tooguarantee ACID for all operations that are part of a single stored procedure/trigger.</span></span> <span data-ttu-id="224e8-174">Tenez compte de hello suit stocké la définition de la procédure :</span><span class="sxs-lookup"><span data-stu-id="224e8-174">Consider hello following stored procedure definition:</span></span>

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

                    if (documents.length != 1) throw "Unable toofind both names";
                    player1Document = documents[0];

                    var filterQuery2 = 'SELECT * FROM Players p where p.id = "' + playerId2 + '"';
                    var accept2 = collection.queryDocuments(collection.getSelfLink(), filterQuery2, {},
                        function (err2, documents2, responseOptions2) {
                            if (err2) throw new Error("Error" + err2.message);
                            if (documents2.length != 1) throw "Unable toofind both names";
                            player2Document = documents2[0];
                            swapItems(player1Document, player2Document);
                            return;
                        });
                    if (!accept2) throw "Unable tooread player details, abort ";
                });

            if (!accept) throw "Unable tooread player details, abort ";

            // swap hello two players’ items
            function swapItems(player1, player2) {
                var player1ItemSave = player1.item;
                player1.item = player2.item;
                player2.item = player1ItemSave;

                var accept = collection.replaceDocument(player1._self, player1,
                    function (err, docReplaced) {
                        if (err) throw "Unable tooupdate player 1, abort ";

                        var accept2 = collection.replaceDocument(player2._self, player2,
                            function (err2, docReplaced2) {
                                if (err) throw "Unable tooupdate player 2, abort"
                            });

                        if (!accept2) throw "Unable tooupdate player 2, abort";
                    });

                if (!accept) throw "Unable tooupdate player 1, abort";
            }
        }
    }

    // register hello stored procedure in Node.js client
    client.createStoredProcedureAsync(collection._self, exchangeItemsSproc)
        .then(function (response) {
            var createdStoredProcedure = response.resource;
        }
    );

<span data-ttu-id="224e8-175">Cette procédure stockée utilise des transactions au sein d’un jeu application tootrade des éléments entre deux lecteurs en une seule opération.</span><span class="sxs-lookup"><span data-stu-id="224e8-175">This stored procedure uses transactions within a gaming app tootrade items between two players in a single operation.</span></span> <span data-ttu-id="224e8-176">Hello stockées deux documents procédure tentatives tooread que chaque lecteur toohello correspondant ID passée en tant qu’argument.</span><span class="sxs-lookup"><span data-stu-id="224e8-176">hello stored procedure attempts tooread two documents each corresponding toohello player IDs passed in as an argument.</span></span> <span data-ttu-id="224e8-177">Si les deux documents de lecteur sont trouvés, puis procédure stockée hello met à jour les documents hello en échangeant leurs éléments.</span><span class="sxs-lookup"><span data-stu-id="224e8-177">If both player documents are found, then hello stored procedure updates hello documents by swapping their items.</span></span> <span data-ttu-id="224e8-178">Si des erreurs se produisent le long de la façon de hello, elle lève une exception de JavaScript qui abandonne implicitement des transactions de hello.</span><span class="sxs-lookup"><span data-stu-id="224e8-178">If any errors are encountered along hello way, it throws a JavaScript exception that implicitly aborts hello transaction.</span></span>

<span data-ttu-id="224e8-179">Si hello procédure stockée hello de collection est inscrit sur est une collection de partition unique, documents de hello tooall étendue au sein de la collection de hello est hello transaction.</span><span class="sxs-lookup"><span data-stu-id="224e8-179">If hello collection hello stored procedure is registered against is a single-partition collection, then hello transaction is scoped tooall hello documents within hello collection.</span></span> <span data-ttu-id="224e8-180">Si la collection de hello est partitionnée, les procédures stockées sont exécutées dans la portée de transaction hello d’une clé de partition unique.</span><span class="sxs-lookup"><span data-stu-id="224e8-180">If hello collection is partitioned, then stored procedures are executed in hello transaction scope of a single partition key.</span></span> <span data-ttu-id="224e8-181">Stockée de chaque exécution de la procédure doit comporter une valeur de clé de partition toohello étendue hello de la transaction doit s’exécuter sous.</span><span class="sxs-lookup"><span data-stu-id="224e8-181">Each stored procedure execution must then include a partition key value corresponding toohello scope hello transaction must run under.</span></span> <span data-ttu-id="224e8-182">Pour plus d’informations, consultez [Partitionnement dans Azure Cosmos DB](partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="224e8-182">For more details, see [Azure Cosmos DB Partitioning](partition-data.md).</span></span>

### <a name="commit-and-rollback"></a><span data-ttu-id="224e8-183">Validation et restauration</span><span class="sxs-lookup"><span data-stu-id="224e8-183">Commit and rollback</span></span>
<span data-ttu-id="224e8-184">Les transactions sont intégrées de façon approfondie et native dans le modèle de programmation JavaScript d’Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="224e8-184">Transactions are deeply and natively integrated into Cosmos DB’s JavaScript programming model.</span></span> <span data-ttu-id="224e8-185">Dans une fonction JavaScript, toutes les opérations sont automatiquement encapsulées dans une transaction unique.</span><span class="sxs-lookup"><span data-stu-id="224e8-185">Inside a JavaScript function, all operations are automatically wrapped under a single transaction.</span></span> <span data-ttu-id="224e8-186">Si hello JavaScript se termine sans qu’aucune exception, base de données toohello hello opérations sont validées.</span><span class="sxs-lookup"><span data-stu-id="224e8-186">If hello JavaScript completes without any exception, hello operations toohello database are committed.</span></span> <span data-ttu-id="224e8-187">En effet, hello « instructions BEGIN TRANSACTION » et « COMMIT TRANSACTION » dans les bases de données relationnelles sont implicites dans la base de données Cosmos.</span><span class="sxs-lookup"><span data-stu-id="224e8-187">In effect, hello “BEGIN TRANSACTION” and “COMMIT TRANSACTION” statements in relational databases are implicit in Cosmos DB.</span></span>  

<span data-ttu-id="224e8-188">S’il existe une exception est propagée à partir du script de hello, le runtime JavaScript Cosmos DB annule toute transaction de hello.</span><span class="sxs-lookup"><span data-stu-id="224e8-188">If there is any exception that’s propagated from hello script, Cosmos DB’s JavaScript runtime will roll back hello whole transaction.</span></span> <span data-ttu-id="224e8-189">Comme indiqué précédemment dans hello exemple, en levant une exception est équivalent effectivement tooa « ROLLBACK TRANSACTION » dans la base de données Cosmos.</span><span class="sxs-lookup"><span data-stu-id="224e8-189">As shown in hello earlier example, throwing an exception is effectively equivalent tooa “ROLLBACK TRANSACTION” in Cosmos DB.</span></span>

### <a name="data-consistency"></a><span data-ttu-id="224e8-190">Cohérence des données</span><span class="sxs-lookup"><span data-stu-id="224e8-190">Data consistency</span></span>
<span data-ttu-id="224e8-191">Déclencheurs et procédures stockées sont toujours exécutées sur le réplica principal de hello du conteneur de base de données Azure Cosmos hello.</span><span class="sxs-lookup"><span data-stu-id="224e8-191">Stored procedures and triggers are always executed on hello primary replica of hello Azure Cosmos DB container.</span></span> <span data-ttu-id="224e8-192">Cela permet de s'assurer que les lectures à partir des procédures stockées offrent une cohérence forte.</span><span class="sxs-lookup"><span data-stu-id="224e8-192">This ensures that reads from inside stored procedures offer strong consistency.</span></span> <span data-ttu-id="224e8-193">Les requêtes utilisant les fonctions définies par l’utilisateur peuvent être exécutées sur hello principal ou de n’importe quel réplica secondaire, mais nous nous assurons que toomeet hello demandée au niveau de cohérence en choisissant de réplica approprié de hello.</span><span class="sxs-lookup"><span data-stu-id="224e8-193">Queries using user defined functions can be executed on hello primary or any secondary replica, but we ensure toomeet hello requested consistency level by choosing hello appropriate replica.</span></span>

## <a name="bounded-execution"></a><span data-ttu-id="224e8-194">Exécution limitée</span><span class="sxs-lookup"><span data-stu-id="224e8-194">Bounded execution</span></span>
<span data-ttu-id="224e8-195">Toutes les opérations de base de données Cosmos doivent se terminer dans le serveur hello spécifié durée du délai d’attente de la demande.</span><span class="sxs-lookup"><span data-stu-id="224e8-195">All Cosmos DB operations must complete within hello server specified request timeout duration.</span></span> <span data-ttu-id="224e8-196">Cette contrainte s’applique également à des fonctions de tooJavaScript (procédures stockées, déclencheurs et fonctions définies par l’utilisateur).</span><span class="sxs-lookup"><span data-stu-id="224e8-196">This constraint also applies tooJavaScript functions (stored procedures, triggers and user-defined functions).</span></span> <span data-ttu-id="224e8-197">Si une opération ne se termine pas avec ce délai, hello transaction est restaurée.</span><span class="sxs-lookup"><span data-stu-id="224e8-197">If an operation does not complete with that time limit, hello transaction is rolled back.</span></span> <span data-ttu-id="224e8-198">Fonctions JavaScript doivent terminer délai hello ou implémenter une exécution toobatch/reprise de modèle en fonction de continuation.</span><span class="sxs-lookup"><span data-stu-id="224e8-198">JavaScript functions must finish within hello time limit or implement a continuation based model toobatch/resume execution.</span></span>  

<span data-ttu-id="224e8-199">Dans le développement de toosimplify commande stockées procédures et déclencheurs toohandle des limites de temps, toutes les fonctions sous l’objet de collection hello (pour créer, lire, remplacer et supprimer des documents et des pièces jointes) retournent une valeur booléenne qui représente si qui l’opération sera effectuée.</span><span class="sxs-lookup"><span data-stu-id="224e8-199">In order toosimplify development of stored procedures and triggers toohandle time limits, all functions under hello collection object (for create, read, replace, and delete of documents and attachments) return a Boolean value that represents whether that operation will complete.</span></span> <span data-ttu-id="224e8-200">Si cette valeur est false, cela indique que délai hello est sur tooexpire et que cette procédure hello doit encapsuler l’exécution des requêtes.</span><span class="sxs-lookup"><span data-stu-id="224e8-200">If this value is false, it is an indication that hello time limit is about tooexpire and that hello procedure must wrap up execution.</span></span>  <span data-ttu-id="224e8-201">Opérations en file d’attente toohello préalable première opération de magasin non accepté est garanti que toocomplete si la procédure stockée hello est terminée dans le temps et ne pas en file d’attente d’autres requêtes.</span><span class="sxs-lookup"><span data-stu-id="224e8-201">Operations queued prior toohello first unaccepted store operation are guaranteed toocomplete if hello stored procedure completes in time and does not queue any more requests.</span></span>  

<span data-ttu-id="224e8-202">Les fonctions JavaScript sont également liées lors de la consommation de ressources.</span><span class="sxs-lookup"><span data-stu-id="224e8-202">JavaScript functions are also bounded on resource consumption.</span></span> <span data-ttu-id="224e8-203">COSMOS DB réserve le débit par la collection en fonction de la taille de hello configuré d’un compte de base de données.</span><span class="sxs-lookup"><span data-stu-id="224e8-203">Cosmos DB reserves throughput per collection based on hello provisioned size of a database account.</span></span> <span data-ttu-id="224e8-204">Le débit est exprimé en unités normalisées de processeur, de mémoire et de consommation d'E/S, appelées unités de demande.</span><span class="sxs-lookup"><span data-stu-id="224e8-204">Throughput is expressed in terms of a normalized unit of CPU, memory and IO consumption called request units or RUs.</span></span> <span data-ttu-id="224e8-205">Les fonctions JavaScript peuvent utiliser d’un grand nombre d’unités réservées dans un délai court et peuvent obtenir limitée si limite la collection hello est atteinte.</span><span class="sxs-lookup"><span data-stu-id="224e8-205">JavaScript functions can potentially use up a large number of RUs within a short time, and might get rate-limited if hello collection’s limit is reached.</span></span> <span data-ttu-id="224e8-206">Procédures stockées utilisant beaucoup de ressources peuvent également être disponibilité tooensure mis en quarantaine des opérations de base de données primitif.</span><span class="sxs-lookup"><span data-stu-id="224e8-206">Resource intensive stored procedures might also be quarantined tooensure availability of primitive database operations.</span></span>  

### <a name="example-bulk-importing-data-into-a-database-program"></a><span data-ttu-id="224e8-207">Exemple : importation de données en bloc dans un programme de base de données</span><span class="sxs-lookup"><span data-stu-id="224e8-207">Example: Bulk importing data into a database program</span></span>
<span data-ttu-id="224e8-208">Voici un exemple d’une procédure stockée qui est écrit toobulk-importer des documents dans une collection.</span><span class="sxs-lookup"><span data-stu-id="224e8-208">Below is an example of a stored procedure that is written toobulk-import documents into a collection.</span></span> <span data-ttu-id="224e8-209">Remarque hello stockage l’exécution des procédures handles limitées en vérifiant hello booléen valeur de retour à partir de createDocument, et puis utilise hello le nombre de documents insérées dans chaque appel de la progression de tootrack et de reprise de la procédure stockée hello sur des lots.</span><span class="sxs-lookup"><span data-stu-id="224e8-209">Note how hello stored procedure handles bounded execution by checking hello Boolean return value from createDocument, and then uses hello count of documents inserted in each invocation of hello stored procedure tootrack and resume progress across batches.</span></span>

    function bulkImport(docs) {
        var collection = getContext().getCollection();
        var collectionLink = collection.getSelfLink();

        // hello count of imported docs, also used as current doc index.
        var count = 0;

        // Validate input.
        if (!docs) throw new Error("hello array is undefined or null.");

        var docsLength = docs.length;
        if (docsLength == 0) {
            getContext().getResponse().setBody(0);
        }

        // Call hello create API toocreate a document.
        tryCreate(docs[count], callback);

        // Note that there are 2 exit conditions:
        // 1) hello createDocument request was not accepted. 
        //    In this case hello callback will not be called, we just call setBody and we are done.
        // 2) hello callback was called docs.length times.
        //    In this case all documents were created and we don’t need toocall tryCreate anymore. Just call setBody and we are done.
        function tryCreate(doc, callback) {
            var isAccepted = collection.createDocument(collectionLink, doc, callback);

            // If hello request was accepted, callback will be called.
            // Otherwise report current count back toohello client, 
            // which will call hello script again with remaining set of docs.
            if (!isAccepted) getContext().getResponse().setBody(count);
        }

        // This is called when collection.createDocument is done in order tooprocess hello result.
        function callback(err, doc, options) {
            if (err) throw err;

            // One more document has been inserted, increment hello count.
            count++;

            if (count >= docsLength) {
                // If we created all documents, we are done. Just set hello response.
                getContext().getResponse().setBody(count);
            } else {
                // Create next document.
                tryCreate(docs[count], callback);
            }
        }
    }

## <span data-ttu-id="224e8-210"><a id="trigger"></a> Déclencheurs de base de données</span><span class="sxs-lookup"><span data-stu-id="224e8-210"><a id="trigger"></a> Database triggers</span></span>
### <a name="database-pre-triggers"></a><span data-ttu-id="224e8-211">Pré-déclencheurs de base de données</span><span class="sxs-lookup"><span data-stu-id="224e8-211">Database pre-triggers</span></span>
<span data-ttu-id="224e8-212">Azure Cosmos DB fournit des déclencheurs qui sont exécutés ou déclenchés par une opération sur un document.</span><span class="sxs-lookup"><span data-stu-id="224e8-212">Cosmos DB provides triggers that are executed or triggered by an operation on a document.</span></span> <span data-ttu-id="224e8-213">Par exemple, vous pouvez spécifier un déclencheur avant lorsque vous créez un document – ce déclencheur préliminaire s’exécutera avant la création de document de hello.</span><span class="sxs-lookup"><span data-stu-id="224e8-213">For example, you can specify a pre-trigger when you are creating a document – this pre-trigger will run before hello document is created.</span></span> <span data-ttu-id="224e8-214">Hello Voici un exemple de comment pré-déclencheurs peuvent être des propriétés de hello toovalidate utilisées d’un document qui est en cours de création :</span><span class="sxs-lookup"><span data-stu-id="224e8-214">hello following is an example of how pre-triggers can be used toovalidate hello properties of a document that is being created:</span></span>

    var validateDocumentContentsTrigger = {
        id: "validateDocumentContents",
        serverScript: function validate() {
            var context = getContext();
            var request = context.getRequest();

            // document toobe created in hello current operation
            var documentToCreate = request.getBody();

            // validate properties
            if (!("timestamp" in documentToCreate)) {
                var ts = new Date();
                documentToCreate["my timestamp"] = ts.getTime();
            }

            // update hello document that will be created
            request.setBody(documentToCreate);
        },
        triggerType: TriggerType.Pre,
        triggerOperation: TriggerOperation.Create
    }


<span data-ttu-id="224e8-215">Et hello code d’inscription côté client Node.js correspondant pour le déclencheur de hello :</span><span class="sxs-lookup"><span data-stu-id="224e8-215">And hello corresponding Node.js client-side registration code for hello trigger:</span></span>

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


<span data-ttu-id="224e8-216">Les pré-déclencheurs ne peuvent pas avoir de paramètres en entrée.</span><span class="sxs-lookup"><span data-stu-id="224e8-216">Pre-triggers cannot have any input parameters.</span></span> <span data-ttu-id="224e8-217">objet de demande Hello peut être le message de demande utilisé toomanipulate hello associé hello opération.</span><span class="sxs-lookup"><span data-stu-id="224e8-217">hello request object can be used toomanipulate hello request message associated with hello operation.</span></span> <span data-ttu-id="224e8-218">Ici, déclencheur avant de hello est en cours d’exécution avec la création d’un document hello et corps du message de demande hello contient hello document toobe est créé au format JSON.</span><span class="sxs-lookup"><span data-stu-id="224e8-218">Here, hello pre-trigger is being run with hello creation of a document, and hello request message body contains hello document toobe created in JSON format.</span></span>   

<span data-ttu-id="224e8-219">Lorsque les déclencheurs sont enregistrées, les utilisateurs peuvent spécifier des opérations de hello, il peut s’exécuter avec.</span><span class="sxs-lookup"><span data-stu-id="224e8-219">When triggers are registered, users can specify hello operations that it can run with.</span></span> <span data-ttu-id="224e8-220">Ce déclencheur a été créé avec TriggerOperation.Create, ce qui signifie que suivant de hello n’est pas autorisée.</span><span class="sxs-lookup"><span data-stu-id="224e8-220">This trigger was created with TriggerOperation.Create, which means hello following is not permitted.</span></span>

    var options = { preTriggerInclude: "validateDocumentContents" };

    client.replaceDocumentAsync(docToReplace.self,
                  newDocBody, options)
    .then(function (response) {
        console.log(response.resource);
    }, function (error) {
        console.log("Error", error);
    });

    // Fails, can’t use a create trigger in a replace operation

### <a name="database-post-triggers"></a><span data-ttu-id="224e8-221">Post-déclencheurs de base de données</span><span class="sxs-lookup"><span data-stu-id="224e8-221">Database post-triggers</span></span>
<span data-ttu-id="224e8-222">Les post-déclencheurs, comme les pré-déclencheurs, sont associés à une opération dans un document et n'acceptent pas de paramètres en entrée.</span><span class="sxs-lookup"><span data-stu-id="224e8-222">Post-triggers, like pre-triggers, are associated with an operation on a document and don’t take any input parameters.</span></span> <span data-ttu-id="224e8-223">Ils ne s’exécutent **après** opération de hello est terminée et ont accès toohello réponse message qui est envoyé toohello client.</span><span class="sxs-lookup"><span data-stu-id="224e8-223">They run **after** hello operation has completed, and have access toohello response message that is sent toohello client.</span></span>   

<span data-ttu-id="224e8-224">Hello, l’exemple suivant montre les post-déclencheurs en action :</span><span class="sxs-lookup"><span data-stu-id="224e8-224">hello following example shows post-triggers in action:</span></span>

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
            if(!accept) throw "Unable tooupdate metadata, abort";

            function updateMetadataCallback(err, documents, responseOptions) {
                if(err) throw new Error("Error" + err.message);
                         if(documents.length != 1) throw 'Unable toofind metadata document';

                         var metadataDocument = documents[0];

                         // update metadata
                         metadataDocument.createdDocuments += 1;
                         metadataDocument.createdNames += " " + createdDocument.id;
                         var accept = collection.replaceDocument(metadataDocument._self,
                               metadataDocument, function(err, docReplaced) {
                                      if(err) throw "Unable tooupdate metadata, abort";
                               });
                         if(!accept) throw "Unable tooupdate metadata, abort";
                         return;                    
            }                                                                                            
        },
        triggerType: TriggerType.Post,
        triggerOperation: TriggerOperation.All
    }


<span data-ttu-id="224e8-225">déclencheur de Hello peut être inscrit comme indiqué dans hello suivant l’exemple.</span><span class="sxs-lookup"><span data-stu-id="224e8-225">hello trigger can be registered as shown in hello following sample.</span></span>

    // register post-trigger
    client.createTriggerAsync('dbs/testdb/colls/testColl', updateMetadataTrigger)
        .then(function(createdTrigger) { 
            var docToCreate = { 
                name: "artist_profile_1023",
                artist: "hello Band",
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


<span data-ttu-id="224e8-226">Ce déclencheur interroge pour le document de métadonnées hello et met à jour avec des détails sur le document de hello nouvellement créé.</span><span class="sxs-lookup"><span data-stu-id="224e8-226">This trigger queries for hello metadata document and updates it with details about hello newly created document.</span></span>  

<span data-ttu-id="224e8-227">Une chose importante toonote est hello **transactionnelle** l’exécution des déclencheurs dans la base de données Cosmos.</span><span class="sxs-lookup"><span data-stu-id="224e8-227">One thing that is important toonote is hello **transactional** execution of triggers in Cosmos DB.</span></span> <span data-ttu-id="224e8-228">Ce déclencheur après s’exécute en tant que partie de hello même transaction que la création de hello hello document d’origine.</span><span class="sxs-lookup"><span data-stu-id="224e8-228">This post-trigger runs as part of hello same transaction as hello creation of hello original document.</span></span> <span data-ttu-id="224e8-229">Par conséquent, si nous lève une exception à partir de post-déclencheur de hello (par exemple si nous sommes le document de métadonnées hello tooupdate impossible), toute transaction de hello échouera et être restaurée.</span><span class="sxs-lookup"><span data-stu-id="224e8-229">Therefore, if we throw an exception from hello post-trigger (say if we are unable tooupdate hello metadata document), hello whole transaction will fail and be rolled back.</span></span> <span data-ttu-id="224e8-230">Aucun document n'est créé et une exception est renvoyée.</span><span class="sxs-lookup"><span data-stu-id="224e8-230">No document will be created, and an exception will be returned.</span></span>  

## <span data-ttu-id="224e8-231"><a id="udf"></a>Fonctions définies par l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="224e8-231"><a id="udf"></a>User-defined functions</span></span>
<span data-ttu-id="224e8-232">Fonctions définies par l’utilisateur (UDF) sont la grammaire du langage de requête utilisé tooextend hello DocumentDB API SQL et implémentent la logique métier personnalisée.</span><span class="sxs-lookup"><span data-stu-id="224e8-232">User-defined functions (UDFs) are used tooextend hello DocumentDB API SQL query language grammar and implement custom business logic.</span></span> <span data-ttu-id="224e8-233">Elles peuvent uniquement être appelées à partir de requêtes.</span><span class="sxs-lookup"><span data-stu-id="224e8-233">They can only be called from inside queries.</span></span> <span data-ttu-id="224e8-234">Ils n’ont pas d’objet de contexte d’accès toohello et sont censées toobe utilisé en tant que calcul seule JavaScript.</span><span class="sxs-lookup"><span data-stu-id="224e8-234">They do not have access toohello context object and are meant toobe used as compute-only JavaScript.</span></span> <span data-ttu-id="224e8-235">Par conséquent, l’UDF peuvent être exécuté sur les réplicas secondaires de hello Cosmos DB service.</span><span class="sxs-lookup"><span data-stu-id="224e8-235">Therefore, UDFs can be run on secondary replicas of hello Cosmos DB service.</span></span>  

<span data-ttu-id="224e8-236">Hello exemple suivant crée un fichier UDF toocalculate impôt basée sur les taux de différents supports de revenu et utilise alors à l’intérieur d’une requête toofind toutes les personnes qui les taxes payant plus de 20 000 $.</span><span class="sxs-lookup"><span data-stu-id="224e8-236">hello following sample creates a UDF toocalculate income tax based on rates for various income brackets, and then uses it inside a query toofind all people who paid more than $20,000 in taxes.</span></span>

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


<span data-ttu-id="224e8-237">Hello UDF peut ensuite être utilisé dans les requêtes comme Bonjour suivant l’exemple :</span><span class="sxs-lookup"><span data-stu-id="224e8-237">hello UDF can subsequently be used in queries like in hello following sample:</span></span>

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

## <a name="javascript-language-integrated-query-api"></a><span data-ttu-id="224e8-238">API de requête intégrée au langage JavaScript</span><span class="sxs-lookup"><span data-stu-id="224e8-238">JavaScript language-integrated query API</span></span>
<span data-ttu-id="224e8-239">En outre tooissuing les requêtes à l’aide de la grammaire SQL de DocumentDB, hello Kit de développement logiciel côté serveur vous permet de requêtes tooperform optimisé à l’aide d’une interface JavaScript fluent sans aucune connaissance de SQL.</span><span class="sxs-lookup"><span data-stu-id="224e8-239">In addition tooissuing queries using DocumentDB’s SQL grammar, hello server-side SDK allows you tooperform optimized queries using a fluent JavaScript interface without any knowledge of SQL.</span></span> <span data-ttu-id="224e8-240">requête de JavaScript Hello QU'API vous permet de requêtes de build tooprogrammatically en passant des fonctions de prédicat dans une fonction enchaînée appelle, avec un tooECMAScript5 familiers syntaxe intégrés du tableau et les bibliothèques JavaScript comme lodash.</span><span class="sxs-lookup"><span data-stu-id="224e8-240">hello JavaScript query API allows you tooprogrammatically build queries by passing predicate functions into chainable function calls, with a syntax familiar tooECMAScript5's Array built-ins and popular JavaScript libraries like lodash.</span></span> <span data-ttu-id="224e8-241">Les requêtes sont analysées par hello JavaScript runtime toobe exécutée efficacement les indices de DB Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="224e8-241">Queries are parsed by hello JavaScript runtime toobe executed efficiently using Azure Cosmos DB’s indices.</span></span>

> [!NOTE]
> <span data-ttu-id="224e8-242">`__`(trait de soulignement double) est un alias trop`getContext().getCollection()`.</span><span class="sxs-lookup"><span data-stu-id="224e8-242">`__` (double-underscore) is an alias too`getContext().getCollection()`.</span></span>
> <br/>
> <span data-ttu-id="224e8-243">En d’autres termes, vous pouvez utiliser `__` ou `getContext().getCollection()` tooaccess hello API de requête de JavaScript.</span><span class="sxs-lookup"><span data-stu-id="224e8-243">In other words, you can use `__` or `getContext().getCollection()` tooaccess hello JavaScript query API.</span></span>
> 
> 

<span data-ttu-id="224e8-244">Les fonctions prises en charge sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="224e8-244">Supported functions include:</span></span>

<ul>
<li><span data-ttu-id="224e8-245">
<b>chain() ... .value([callback] [, options])</b>
</span><span class="sxs-lookup"><span data-stu-id="224e8-245">
<b>chain() ... .value([callback] [, options])</b>
</span></span><ul>
<li>
<span data-ttu-id="224e8-246">Commence un appel chaîné qui doit se terminer par value().</span><span class="sxs-lookup"><span data-stu-id="224e8-246">Starts a chained call which must be terminated with value().</span></span>
</li>
</ul>
</li>
<li><span data-ttu-id="224e8-247">
<b>filter(predicateFunction [, options] [, callback])</b>
</span><span class="sxs-lookup"><span data-stu-id="224e8-247">
<b>filter(predicateFunction [, options] [, callback])</b>
</span></span><ul>
<li>
<span data-ttu-id="224e8-248">Filtre hello d’entrée à l’aide d’une fonction de prédicat qui retourne la valeur true/false dans l’ordre toofilter documents d’entrée/sortie dans le jeu résultant de hello.</span><span class="sxs-lookup"><span data-stu-id="224e8-248">Filters hello input using a predicate function which returns true/false in order toofilter in/out input documents into hello resulting set.</span></span> <span data-ttu-id="224e8-249">Ce comportement similaire tooa clause WHERE dans SQL.</span><span class="sxs-lookup"><span data-stu-id="224e8-249">This behaves similar tooa WHERE clause in SQL.</span></span>
</li>
</ul>
</li>
<li><span data-ttu-id="224e8-250">
<b>map(transformationFunction [, options] [, callback])</b>
</span><span class="sxs-lookup"><span data-stu-id="224e8-250">
<b>map(transformationFunction [, options] [, callback])</b>
</span></span><ul>
<li>
<span data-ttu-id="224e8-251">Applique une projection d’une fonction de transformation qui mappe chaque élément d’entrée tooa JavaScript objet ou une valeur.</span><span class="sxs-lookup"><span data-stu-id="224e8-251">Applies a projection given a transformation function which maps each input item tooa JavaScript object or value.</span></span> <span data-ttu-id="224e8-252">Cela a un comportement similaire clause SELECT tooa dans SQL.</span><span class="sxs-lookup"><span data-stu-id="224e8-252">This behaves similar tooa SELECT clause in SQL.</span></span>
</li>
</ul>
</li>
<li><span data-ttu-id="224e8-253">
<b>pluck([propertyName] [, options] [, callback])</b>
</span><span class="sxs-lookup"><span data-stu-id="224e8-253">
<b>pluck([propertyName] [, options] [, callback])</b>
</span></span><ul>
<li>
<span data-ttu-id="224e8-254">Il s’agit d’un raccourci pour une carte qui extrait la valeur hello d’une propriété unique de chaque élément d’entrée.</span><span class="sxs-lookup"><span data-stu-id="224e8-254">This is a shortcut for a map which extracts hello value of a single property from each input item.</span></span>
</li>
</ul>
</li>
<li><span data-ttu-id="224e8-255">
<b>flatten([isShallow] [, options] [, callback])</b>
</span><span class="sxs-lookup"><span data-stu-id="224e8-255">
<b>flatten([isShallow] [, options] [, callback])</b>
</span></span><ul>
<li>
<span data-ttu-id="224e8-256">Combine et aplatissement des tableaux à partir de chaque élément d’entrée dans un tableau à une seule tooa.</span><span class="sxs-lookup"><span data-stu-id="224e8-256">Combines and flattens arrays from each input item in tooa single array.</span></span> <span data-ttu-id="224e8-257">Le système de comporte tooSelectMany similaires dans LINQ.</span><span class="sxs-lookup"><span data-stu-id="224e8-257">This behaves similar tooSelectMany in LINQ.</span></span>
</li>
</ul>
</li>
<li><span data-ttu-id="224e8-258">
<b>sortBy([predicate] [, options] [, callback])</b>
</span><span class="sxs-lookup"><span data-stu-id="224e8-258">
<b>sortBy([predicate] [, options] [, callback])</b>
</span></span><ul>
<li>
<span data-ttu-id="224e8-259">Générer un nouvel ensemble de documents en triant les documents hello dans le flux de document d’entrée hello croissant à l’aide de hello fonction de prédicat.</span><span class="sxs-lookup"><span data-stu-id="224e8-259">Produce a new set of documents by sorting hello documents in hello input document stream in ascending order using hello given predicate.</span></span> <span data-ttu-id="224e8-260">Cela a un comportement similaire tooa clause ORDER BY dans SQL.</span><span class="sxs-lookup"><span data-stu-id="224e8-260">This behaves similar tooa ORDER BY clause in SQL.</span></span>
</li>
</ul>
</li>
<li><span data-ttu-id="224e8-261">
<b>sortByDescending([predicate] [, options] [, callback])</b>
</span><span class="sxs-lookup"><span data-stu-id="224e8-261">
<b>sortByDescending([predicate] [, options] [, callback])</b>
</span></span><ul>
<li>
<span data-ttu-id="224e8-262">Générer un nouvel ensemble de documents en triant les documents hello dans le flux de document d’entrée hello décroissant à l’aide de hello fonction de prédicat.</span><span class="sxs-lookup"><span data-stu-id="224e8-262">Produce a new set of documents by sorting hello documents in hello input document stream in descending order using hello given predicate.</span></span> <span data-ttu-id="224e8-263">Cela a un comportement similaire clause ORDER BY x DESC de tooa dans SQL.</span><span class="sxs-lookup"><span data-stu-id="224e8-263">This behaves similar tooa ORDER BY x DESC clause in SQL.</span></span>
</li>
</ul>
</li>
</ul>


<span data-ttu-id="224e8-264">Lorsque inclus dans des fonctions de prédicat ou sélecteur, hello constructions JavaScript suivantes obtenir automatiquement optimisé toorun directement sur l’index de base de données Azure Cosmos :</span><span class="sxs-lookup"><span data-stu-id="224e8-264">When included inside predicate and/or selector functions, hello following JavaScript constructs get automatically optimized toorun directly on Azure Cosmos DB indices:</span></span>

* <span data-ttu-id="224e8-265">Opérateurs simples : = + - * / % | ^ &amp; == != === !=== &lt; &gt; &lt;= &gt;= || &amp;&amp; &lt;&lt; &gt;&gt; &gt;&gt;&gt;!</span><span class="sxs-lookup"><span data-stu-id="224e8-265">Simple operators: = + - * / % | ^ &amp; == != === !=== &lt; &gt; &lt;= &gt;= || &amp;&amp; &lt;&lt; &gt;&gt; &gt;&gt;&gt;!</span></span> ~
* <span data-ttu-id="224e8-266">Littéraux, y compris le littéral d’objet hello : {}</span><span class="sxs-lookup"><span data-stu-id="224e8-266">Literals, including hello object literal: {}</span></span>
* <span data-ttu-id="224e8-267">var, return</span><span class="sxs-lookup"><span data-stu-id="224e8-267">var, return</span></span>

<span data-ttu-id="224e8-268">Hello construit du code JavaScript suivant n’a pas obtenir optimisée pour les index de base de données Azure Cosmos de :</span><span class="sxs-lookup"><span data-stu-id="224e8-268">hello following JavaScript constructs do not get optimized for Azure Cosmos DB indices:</span></span>

* <span data-ttu-id="224e8-269">Flux de contrôle (par exemple, if, for, while)</span><span class="sxs-lookup"><span data-stu-id="224e8-269">Control flow (e.g. if, for, while)</span></span>
* <span data-ttu-id="224e8-270">Appels de fonction</span><span class="sxs-lookup"><span data-stu-id="224e8-270">Function calls</span></span>

<span data-ttu-id="224e8-271">Pour plus d’informations, voir [JSDocs côté serveur](http://azure.github.io/azure-documentdb-js-server/).</span><span class="sxs-lookup"><span data-stu-id="224e8-271">For more information, please see our [Server-Side JSDocs](http://azure.github.io/azure-documentdb-js-server/).</span></span>

### <a name="example-write-a-stored-procedure-using-hello-javascript-query-api"></a><span data-ttu-id="224e8-272">Exemple : Écrire une procédure stockée à l’aide des API de requête hello JavaScript</span><span class="sxs-lookup"><span data-stu-id="224e8-272">Example: Write a stored procedure using hello JavaScript query API</span></span>
<span data-ttu-id="224e8-273">Hello suivant l’exemple de code est un exemple d’utilisation de la hello API de requête de JavaScript dans le contexte hello d’une procédure stockée.</span><span class="sxs-lookup"><span data-stu-id="224e8-273">hello following code sample is an example of how hello JavaScript Query API can be used in hello context of a stored procedure.</span></span> <span data-ttu-id="224e8-274">Insère un document donné par le paramètre d’entrée, Hello procédure stockée et met à jour d’un document de métadonnées, à l’aide de hello `__.filter()` méthode, avec minSize, maxSize et totalSize en fonction de propriété de taille du document d’entrée hello.</span><span class="sxs-lookup"><span data-stu-id="224e8-274">hello stored procedure inserts a document, given by an input parameter, and updates a metadata document, using hello `__.filter()` method, with minSize, maxSize, and totalSize based upon hello input document's size property.</span></span>

    /**
     * Insert actual doc and update metadata doc: minSize, maxSize, totalSize based on doc.size.
     */
    function insertDocumentAndUpdateMetadata(doc) {
      // HTTP error codes sent tooour callback funciton by DocDB server.
      var ErrorCode = {
        RETRY_WITH: 449,
      }

      var isAccepted = __.createDocument(__.getSelfLink(), doc, {}, function(err, doc, options) {
        if (err) throw err;

        // Check hello doc (ignore docs with invalid/zero size and metaDoc itself) and call updateMetadata.
        if (!doc.isMetadata && doc.size > 0) {
          // Get hello meta document. We keep it in hello same collection. it's hello only doc that has .isMetadata = true.
          var result = __.filter(function(x) {
            return x.isMetadata === true
          }, function(err, feed, options) {
            if (err) throw err;

            // We assume that metadata doc was pre-created and must exist when this script is called.
            if (!feed || !feed.length) throw new Error("Failed toofind hello metadata document.");

            // hello metadata document.
            var metaDoc = feed[0];

            // Update metaDoc.minSize:
            // for 1st document use doc.Size, for all hello rest see if it's less than last min.
            if (metaDoc.minSize == 0) metaDoc.minSize = doc.size;
            else metaDoc.minSize = Math.min(metaDoc.minSize, doc.size);

            // Update metaDoc.maxSize.
            metaDoc.maxSize = Math.max(metaDoc.maxSize, doc.size);

            // Update metaDoc.totalSize.
            metaDoc.totalSize += doc.size;

            // Update/replace hello metadata document in hello store.
            var isAccepted = __.replaceDocument(metaDoc._self, metaDoc, function(err) {
              if (err) throw err;
              // Note: in case concurrent updates causes conflict with ErrorCode.RETRY_WITH, we can't read hello meta again 
              //       and update again because due tooSnapshot isolation we will read same exact version (we are in same transaction).
              //       We have tootake care of that on hello client side.
            });
            if (!isAccepted) throw new Error("replaceDocument(metaDoc) returned false.");
          });
          if (!result.isAccepted) throw new Error("filter for metaDoc returned false.");
        }
      });
      if (!isAccepted) throw new Error("createDocument(actual doc) returned false.");
    }

## <a name="sql-toojavascript-cheat-sheet"></a><span data-ttu-id="224e8-275">Aide-mémoire de tooJavascript SQL</span><span class="sxs-lookup"><span data-stu-id="224e8-275">SQL tooJavascript cheat sheet</span></span>
<span data-ttu-id="224e8-276">Hello tableau suivant présente les différentes requêtes SQL et les requêtes de JavaScript correspondantes hello.</span><span class="sxs-lookup"><span data-stu-id="224e8-276">hello following table presents various SQL queries and hello corresponding JavaScript queries.</span></span>

<span data-ttu-id="224e8-277">Comme pour les requêtes SQL, les clés de propriété de document (par exemple, `doc.id`) respectent la casse.</span><span class="sxs-lookup"><span data-stu-id="224e8-277">As with SQL queries, document property keys (e.g. `doc.id`) are case-sensitive.</span></span>

|<span data-ttu-id="224e8-278">SQL</span><span class="sxs-lookup"><span data-stu-id="224e8-278">SQL</span></span>| <span data-ttu-id="224e8-279">API de requête JavaScript</span><span class="sxs-lookup"><span data-stu-id="224e8-279">JavaScript Query API</span></span>|<span data-ttu-id="224e8-280">Description ci-dessous</span><span class="sxs-lookup"><span data-stu-id="224e8-280">Description below</span></span>|
|---|---|---|
|<span data-ttu-id="224e8-281">SELECT *</span><span class="sxs-lookup"><span data-stu-id="224e8-281">SELECT *</span></span><br><span data-ttu-id="224e8-282">FROM docs</span><span class="sxs-lookup"><span data-stu-id="224e8-282">FROM docs</span></span>| <span data-ttu-id="224e8-283">__.map(function(doc) {</span><span class="sxs-lookup"><span data-stu-id="224e8-283">__.map(function(doc) {</span></span> <br><span data-ttu-id="224e8-284">&nbsp;&nbsp;&nbsp;&nbsp;return doc;</span><span class="sxs-lookup"><span data-stu-id="224e8-284">&nbsp;&nbsp;&nbsp;&nbsp;return doc;</span></span><br><span data-ttu-id="224e8-285">});</span><span class="sxs-lookup"><span data-stu-id="224e8-285">});</span></span>|<span data-ttu-id="224e8-286">1</span><span class="sxs-lookup"><span data-stu-id="224e8-286">1</span></span>|
|<span data-ttu-id="224e8-287">SELECT docs.id, docs.message AS msg, docs.actions</span><span class="sxs-lookup"><span data-stu-id="224e8-287">SELECT docs.id, docs.message AS msg, docs.actions</span></span> <br><span data-ttu-id="224e8-288">FROM docs</span><span class="sxs-lookup"><span data-stu-id="224e8-288">FROM docs</span></span>|<span data-ttu-id="224e8-289">__.map(function(doc) {</span><span class="sxs-lookup"><span data-stu-id="224e8-289">__.map(function(doc) {</span></span><br><span data-ttu-id="224e8-290">&nbsp;&nbsp;&nbsp;&nbsp;return {</span><span class="sxs-lookup"><span data-stu-id="224e8-290">&nbsp;&nbsp;&nbsp;&nbsp;return {</span></span><br><span data-ttu-id="224e8-291">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;id: doc.id,</span><span class="sxs-lookup"><span data-stu-id="224e8-291">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;id: doc.id,</span></span><br><span data-ttu-id="224e8-292">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;msg: doc.message,</span><span class="sxs-lookup"><span data-stu-id="224e8-292">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;msg: doc.message,</span></span><br><span data-ttu-id="224e8-293">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;actions:doc.actions</span><span class="sxs-lookup"><span data-stu-id="224e8-293">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;actions:doc.actions</span></span><br><span data-ttu-id="224e8-294">&nbsp;&nbsp;&nbsp;&nbsp;};</span><span class="sxs-lookup"><span data-stu-id="224e8-294">&nbsp;&nbsp;&nbsp;&nbsp;};</span></span><br><span data-ttu-id="224e8-295">});</span><span class="sxs-lookup"><span data-stu-id="224e8-295">});</span></span>|<span data-ttu-id="224e8-296">2</span><span class="sxs-lookup"><span data-stu-id="224e8-296">2</span></span>|
|<span data-ttu-id="224e8-297">SELECT *</span><span class="sxs-lookup"><span data-stu-id="224e8-297">SELECT *</span></span><br><span data-ttu-id="224e8-298">FROM docs</span><span class="sxs-lookup"><span data-stu-id="224e8-298">FROM docs</span></span><br><span data-ttu-id="224e8-299">WHERE docs.id="X998_Y998"</span><span class="sxs-lookup"><span data-stu-id="224e8-299">WHERE docs.id="X998_Y998"</span></span>|<span data-ttu-id="224e8-300">__.filter(function(doc) {</span><span class="sxs-lookup"><span data-stu-id="224e8-300">__.filter(function(doc) {</span></span><br><span data-ttu-id="224e8-301">&nbsp;&nbsp;&nbsp;&nbsp;return doc.id ==="X998_Y998";</span><span class="sxs-lookup"><span data-stu-id="224e8-301">&nbsp;&nbsp;&nbsp;&nbsp;return doc.id ==="X998_Y998";</span></span><br><span data-ttu-id="224e8-302">});</span><span class="sxs-lookup"><span data-stu-id="224e8-302">});</span></span>|<span data-ttu-id="224e8-303">3</span><span class="sxs-lookup"><span data-stu-id="224e8-303">3</span></span>|
|<span data-ttu-id="224e8-304">SELECT *</span><span class="sxs-lookup"><span data-stu-id="224e8-304">SELECT *</span></span><br><span data-ttu-id="224e8-305">FROM docs</span><span class="sxs-lookup"><span data-stu-id="224e8-305">FROM docs</span></span><br><span data-ttu-id="224e8-306">WHERE ARRAY_CONTAINS(docs.Tags, 123)</span><span class="sxs-lookup"><span data-stu-id="224e8-306">WHERE ARRAY_CONTAINS(docs.Tags, 123)</span></span>|<span data-ttu-id="224e8-307">__.filter(function(x) {</span><span class="sxs-lookup"><span data-stu-id="224e8-307">__.filter(function(x) {</span></span><br><span data-ttu-id="224e8-308">&nbsp;&nbsp;&nbsp;&nbsp;return x.Tags &amp;&amp; x.Tags.indexOf(123) &gt; -1;</span><span class="sxs-lookup"><span data-stu-id="224e8-308">&nbsp;&nbsp;&nbsp;&nbsp;return x.Tags && x.Tags.indexOf(123) > -1;</span></span><br><span data-ttu-id="224e8-309">});</span><span class="sxs-lookup"><span data-stu-id="224e8-309">});</span></span>|<span data-ttu-id="224e8-310">4</span><span class="sxs-lookup"><span data-stu-id="224e8-310">4</span></span>|
|<span data-ttu-id="224e8-311">SELECT docs.id, docs.message AS msg</span><span class="sxs-lookup"><span data-stu-id="224e8-311">SELECT docs.id, docs.message AS msg</span></span><br><span data-ttu-id="224e8-312">FROM docs</span><span class="sxs-lookup"><span data-stu-id="224e8-312">FROM docs</span></span><br><span data-ttu-id="224e8-313">WHERE docs.id="X998_Y998"</span><span class="sxs-lookup"><span data-stu-id="224e8-313">WHERE docs.id="X998_Y998"</span></span>|<span data-ttu-id="224e8-314">__.chain()</span><span class="sxs-lookup"><span data-stu-id="224e8-314">__.chain()</span></span><br><span data-ttu-id="224e8-315">&nbsp;&nbsp;&nbsp;&nbsp;.filter(function(doc) {</span><span class="sxs-lookup"><span data-stu-id="224e8-315">&nbsp;&nbsp;&nbsp;&nbsp;.filter(function(doc) {</span></span><br><span data-ttu-id="224e8-316">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;return doc.id ==="X998_Y998";</span><span class="sxs-lookup"><span data-stu-id="224e8-316">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return doc.id ==="X998_Y998";</span></span><br><span data-ttu-id="224e8-317">&nbsp;&nbsp;&nbsp;&nbsp;})</span><span class="sxs-lookup"><span data-stu-id="224e8-317">&nbsp;&nbsp;&nbsp;&nbsp;})</span></span><br><span data-ttu-id="224e8-318">&nbsp;&nbsp;&nbsp;&nbsp;.map(function(doc) {</span><span class="sxs-lookup"><span data-stu-id="224e8-318">&nbsp;&nbsp;&nbsp;&nbsp;.map(function(doc) {</span></span><br><span data-ttu-id="224e8-319">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;return {</span><span class="sxs-lookup"><span data-stu-id="224e8-319">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return {</span></span><br><span data-ttu-id="224e8-320">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;id: doc.id,</span><span class="sxs-lookup"><span data-stu-id="224e8-320">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;id: doc.id,</span></span><br><span data-ttu-id="224e8-321">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;msg: doc.message</span><span class="sxs-lookup"><span data-stu-id="224e8-321">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;msg: doc.message</span></span><br><span data-ttu-id="224e8-322">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;};</span><span class="sxs-lookup"><span data-stu-id="224e8-322">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;};</span></span><br><span data-ttu-id="224e8-323">&nbsp;&nbsp;&nbsp;&nbsp;})</span><span class="sxs-lookup"><span data-stu-id="224e8-323">&nbsp;&nbsp;&nbsp;&nbsp;})</span></span><br><span data-ttu-id="224e8-324">.value();</span><span class="sxs-lookup"><span data-stu-id="224e8-324">.value();</span></span>|<span data-ttu-id="224e8-325">5</span><span class="sxs-lookup"><span data-stu-id="224e8-325">5</span></span>|
|<span data-ttu-id="224e8-326">SELECT VALUE tag</span><span class="sxs-lookup"><span data-stu-id="224e8-326">SELECT VALUE tag</span></span><br><span data-ttu-id="224e8-327">FROM docs</span><span class="sxs-lookup"><span data-stu-id="224e8-327">FROM docs</span></span><br><span data-ttu-id="224e8-328">JOIN tag IN docs.Tags</span><span class="sxs-lookup"><span data-stu-id="224e8-328">JOIN tag IN docs.Tags</span></span><br><span data-ttu-id="224e8-329">ORDER BY docs._ts</span><span class="sxs-lookup"><span data-stu-id="224e8-329">ORDER BY docs._ts</span></span>|<span data-ttu-id="224e8-330">__.chain()</span><span class="sxs-lookup"><span data-stu-id="224e8-330">__.chain()</span></span><br><span data-ttu-id="224e8-331">&nbsp;&nbsp;&nbsp;&nbsp;.filter(function(doc) {</span><span class="sxs-lookup"><span data-stu-id="224e8-331">&nbsp;&nbsp;&nbsp;&nbsp;.filter(function(doc) {</span></span><br><span data-ttu-id="224e8-332">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;return doc.Tags &amp;&amp; Array.isArray(doc.Tags);</span><span class="sxs-lookup"><span data-stu-id="224e8-332">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return doc.Tags && Array.isArray(doc.Tags);</span></span><br><span data-ttu-id="224e8-333">&nbsp;&nbsp;&nbsp;&nbsp;})</span><span class="sxs-lookup"><span data-stu-id="224e8-333">&nbsp;&nbsp;&nbsp;&nbsp;})</span></span><br><span data-ttu-id="224e8-334">&nbsp;&nbsp;&nbsp;&nbsp;.sortBy(function(doc) {</span><span class="sxs-lookup"><span data-stu-id="224e8-334">&nbsp;&nbsp;&nbsp;&nbsp;.sortBy(function(doc) {</span></span><br><span data-ttu-id="224e8-335">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;return doc._ts;</span><span class="sxs-lookup"><span data-stu-id="224e8-335">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return doc._ts;</span></span><br><span data-ttu-id="224e8-336">&nbsp;&nbsp;&nbsp;&nbsp;})</span><span class="sxs-lookup"><span data-stu-id="224e8-336">&nbsp;&nbsp;&nbsp;&nbsp;})</span></span><br><span data-ttu-id="224e8-337">&nbsp;&nbsp;&nbsp;&nbsp;.pluck("Tags")</span><span class="sxs-lookup"><span data-stu-id="224e8-337">&nbsp;&nbsp;&nbsp;&nbsp;.pluck("Tags")</span></span><br><span data-ttu-id="224e8-338">&nbsp;&nbsp;&nbsp;&nbsp;.flatten()</span><span class="sxs-lookup"><span data-stu-id="224e8-338">&nbsp;&nbsp;&nbsp;&nbsp;.flatten()</span></span><br><span data-ttu-id="224e8-339">&nbsp;&nbsp;&nbsp;&nbsp;.value()</span><span class="sxs-lookup"><span data-stu-id="224e8-339">&nbsp;&nbsp;&nbsp;&nbsp;.value()</span></span>|<span data-ttu-id="224e8-340">6</span><span class="sxs-lookup"><span data-stu-id="224e8-340">6</span></span>|

<span data-ttu-id="224e8-341">Hello descriptions suivantes expliquent chaque requête de table hello ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="224e8-341">hello following descriptions explain each query in hello table above.</span></span>
1. <span data-ttu-id="224e8-342">Renvoie tous les documents (paginés avec jeton de continuation) tels quels.</span><span class="sxs-lookup"><span data-stu-id="224e8-342">Results in all documents (paginated with continuation token) as is.</span></span>
2. <span data-ttu-id="224e8-343">Projets hello id, le message (alias toomsg) et l’action à partir de tous les documents.</span><span class="sxs-lookup"><span data-stu-id="224e8-343">Projects hello id, message (aliased toomsg), and action from all documents.</span></span>
3. <span data-ttu-id="224e8-344">Requêtes pour les documents avec le prédicat de hello : id = « X998_Y998 ».</span><span class="sxs-lookup"><span data-stu-id="224e8-344">Queries for documents with hello predicate: id = "X998_Y998".</span></span>
4. <span data-ttu-id="224e8-345">Requêtes pour les documents qui ont une propriété de balises et de balises est un tableau qui contient la valeur de hello 123.</span><span class="sxs-lookup"><span data-stu-id="224e8-345">Queries for documents that have a Tags property and Tags is an array containing hello value 123.</span></span>
5. <span data-ttu-id="224e8-346">Requêtes pour les documents avec un prédicat, id = « X998_Y998 » et l’id de hello puis projets et de message (alias toomsg).</span><span class="sxs-lookup"><span data-stu-id="224e8-346">Queries for documents with a predicate, id = "X998_Y998", and then projects hello id and message (aliased toomsg).</span></span>
6. <span data-ttu-id="224e8-347">Les filtres pour les documents qui ont une propriété de tableau, les balises, et trie les documents qui en résultent hello par la propriété du système hello _ts timestamp et projette ensuite + aplatit le tableau de balises hello.</span><span class="sxs-lookup"><span data-stu-id="224e8-347">Filters for documents which have an array property, Tags, and sorts hello resulting documents by hello _ts timestamp system property, and then projects + flattens hello Tags array.</span></span>


## <a name="runtime-support"></a><span data-ttu-id="224e8-348">Prise en charge du runtime</span><span class="sxs-lookup"><span data-stu-id="224e8-348">Runtime support</span></span>
<span data-ttu-id="224e8-349">[API du côté serveur JavaScript pour DocumentDB](http://azure.github.io/azure-documentdb-js-server/) hello prend en charge la plupart des hello grand public des fonctionnalités de langage JavaScript standard par [ECMA-262](http://www.ecma-international.org/publications/standards/Ecma-262.htm).</span><span class="sxs-lookup"><span data-stu-id="224e8-349">[DocumentDB JavaScript server side API](http://azure.github.io/azure-documentdb-js-server/) provides support for hello most of hello mainstream JavaScript language features as standardized by [ECMA-262](http://www.ecma-international.org/publications/standards/Ecma-262.htm).</span></span>

### <a name="security"></a><span data-ttu-id="224e8-350">Sécurité</span><span class="sxs-lookup"><span data-stu-id="224e8-350">Security</span></span>
<span data-ttu-id="224e8-351">JavaScript des procédures stockées et déclencheurs sont sandbox afin que les effets de hello d’un script ne pas renvoyer les toohello autres sans passer par le biais d’isolation des transactions hello instantané au niveau de base de données hello.</span><span class="sxs-lookup"><span data-stu-id="224e8-351">JavaScript stored procedures and triggers are sandboxed so that hello effects of one script do not leak toohello other without going through hello snapshot transaction isolation at hello database level.</span></span> <span data-ttu-id="224e8-352">environnements d’exécution Hello regroupées sont nettoyés du contexte de hello après chaque exécution.</span><span class="sxs-lookup"><span data-stu-id="224e8-352">hello runtime environments are pooled but cleaned of hello context after each run.</span></span> <span data-ttu-id="224e8-353">Par conséquent, elles sont garanties toobe sans échec de toutes les effets secondaires involontaires entre eux.</span><span class="sxs-lookup"><span data-stu-id="224e8-353">Hence they are guaranteed toobe safe of any unintended side effects from each other.</span></span>

### <a name="pre-compilation"></a><span data-ttu-id="224e8-354">Précompilation</span><span class="sxs-lookup"><span data-stu-id="224e8-354">Pre-compilation</span></span>
<span data-ttu-id="224e8-355">Les procédures stockées, déclencheurs et des UDF sont format du code précompilé implicitement toohello octets dans le coût de compilation de commande tooavoid lors de chaque appel du script hello.</span><span class="sxs-lookup"><span data-stu-id="224e8-355">Stored procedures, triggers and UDFs are implicitly precompiled toohello byte code format in order tooavoid compilation cost at hello time of each script invocation.</span></span> <span data-ttu-id="224e8-356">Cela permet de s'assurer que les appels de procédures stockées sont rapides et présentent un encombrement réduit.</span><span class="sxs-lookup"><span data-stu-id="224e8-356">This ensures invocations of stored procedures are fast and have a low footprint.</span></span>

## <a name="client-sdk-support"></a><span data-ttu-id="224e8-357">Prise en charge du kit SDK client</span><span class="sxs-lookup"><span data-stu-id="224e8-357">Client SDK support</span></span>
<span data-ttu-id="224e8-358">En outre toohello API DocumentDB pour [Node.js](documentdb-sdk-node.md) client, la base de données Azure Cosmos a [.NET](documentdb-sdk-dotnet.md), [.NET Core](documentdb-sdk-dotnet-core.md), [Java](documentdb-sdk-java.md), [ JavaScript](http://azure.github.io/azure-documentdb-js/), et [kits de développement logiciel Python](documentdb-sdk-python.md) pour hello API DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="224e8-358">In addition toohello DocumentDB API for [Node.js](documentdb-sdk-node.md) client, Azure Cosmos DB has [.NET](documentdb-sdk-dotnet.md), [.NET Core](documentdb-sdk-dotnet-core.md), [Java](documentdb-sdk-java.md), [JavaScript](http://azure.github.io/azure-documentdb-js/), and [Python SDKs](documentdb-sdk-python.md) for hello DocumentDB API.</span></span> <span data-ttu-id="224e8-359">Les procédures stockées, les déclencheurs et les fonctions définies par l'utilisateur peuvent être créés et exécutés au moyen de l'un de ces kits SDK également.</span><span class="sxs-lookup"><span data-stu-id="224e8-359">Stored procedures, triggers and UDFs can be created and executed using any of these SDKs as well.</span></span> <span data-ttu-id="224e8-360">Hello suivant montre l’exemple de comment toocreate et exécuter une procédure stockée à l’aide du client de .NET hello.</span><span class="sxs-lookup"><span data-stu-id="224e8-360">hello following example shows how toocreate and execute a stored procedure using hello .NET client.</span></span> <span data-ttu-id="224e8-361">Notez comment hello .NET sont passés dans hello procédure stockée au format JSON et lire.</span><span class="sxs-lookup"><span data-stu-id="224e8-361">Note how hello .NET types are passed into hello stored procedure as JSON and read back.</span></span>

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


<span data-ttu-id="224e8-362">Cet exemple montre comment toouse hello [DocumentDB .NET API](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet) toocreate un déclencheur préalable et créer un document avec déclencheur hello activé.</span><span class="sxs-lookup"><span data-stu-id="224e8-362">This sample shows how toouse hello [DocumentDB .NET API](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet) toocreate a pre-trigger and create a document with hello trigger enabled.</span></span> 

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


<span data-ttu-id="224e8-363">Et hello l’exemple suivant montre comment toocreate un utilisateur défini (fonction) (UDF) et l’utiliser dans un [requête DocumentDB API SQL](documentdb-sql-query.md).</span><span class="sxs-lookup"><span data-stu-id="224e8-363">And hello following example shows how toocreate a user defined function (UDF) and use it in a [DocumentDB API SQL query](documentdb-sql-query.md).</span></span>

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

## <a name="rest-api"></a><span data-ttu-id="224e8-364">API REST</span><span class="sxs-lookup"><span data-stu-id="224e8-364">REST API</span></span>
<span data-ttu-id="224e8-365">Toutes les opérations Azure Cosmos DB peuvent être effectuées sur la base de l’architecture REST.</span><span class="sxs-lookup"><span data-stu-id="224e8-365">All Azure Cosmos DB operations can be performed in a RESTful manner.</span></span> <span data-ttu-id="224e8-366">Les procédures stockées, les déclencheurs et les fonctions définies par l'utilisateur peuvent être enregistrés dans une collection au moyen de HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="224e8-366">Stored procedures, triggers and user-defined functions can be registered under a collection by using HTTP POST.</span></span> <span data-ttu-id="224e8-367">Hello Voici un exemple d’une procédure stockée de tooregister :</span><span class="sxs-lookup"><span data-stu-id="224e8-367">hello following is an example of how tooregister a stored procedure:</span></span>

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


<span data-ttu-id="224e8-368">Hello procédure stockée est enregistrée en exécutant une demande POST sur hello URI dbs/testdb/colls/testColl/procédures stockées contenant hello corps hello toocreate de procédure stockée.</span><span class="sxs-lookup"><span data-stu-id="224e8-368">hello stored procedure is registered by executing a POST request against hello URI dbs/testdb/colls/testColl/sprocs with hello body containing hello stored procedure toocreate.</span></span> <span data-ttu-id="224e8-369">Les déclencheurs et les fonctions définies par l'utilisateur peuvent être inscrits de la même façon en émettant une demande POST sur /triggers et /udfs respectivement.</span><span class="sxs-lookup"><span data-stu-id="224e8-369">Triggers and UDFs can be registered similarly by issuing a POST against /triggers and /udfs respectively.</span></span>
<span data-ttu-id="224e8-370">Cette procédure stockée peut ensuite être exécutée en émettant une demande POST sur son lien de ressource :</span><span class="sxs-lookup"><span data-stu-id="224e8-370">This stored procedure can then be executed by issuing a POST request against its resource link:</span></span>

    POST https://<url>/sprocs/<sproc> HTTP/1.1
    authorization: <<auth>>
    x-ms-date: Thu, 07 Aug 2014 03:43:20 GMT


    [ { "name": "TestDocument", "book": "Autumn of hello Patriarch"}, "Price", 200 ]


<span data-ttu-id="224e8-371">Ici, la procédure stockée de toohello d’entrée de hello est passé dans le corps de la demande hello.</span><span class="sxs-lookup"><span data-stu-id="224e8-371">Here, hello input toohello stored procedure is passed in hello request body.</span></span> <span data-ttu-id="224e8-372">Notez que l’entrée de hello est passée comme un tableau JSON des paramètres d’entrée.</span><span class="sxs-lookup"><span data-stu-id="224e8-372">Note that hello input is passed as a JSON array of input parameters.</span></span> <span data-ttu-id="224e8-373">Hello stockées procédure prend hello la première entrée sous la forme d’un document qui est un corps de réponse.</span><span class="sxs-lookup"><span data-stu-id="224e8-373">hello stored procedure takes hello first input as a document that is a response body.</span></span> <span data-ttu-id="224e8-374">réponse Hello que nous de réception est la suivante :</span><span class="sxs-lookup"><span data-stu-id="224e8-374">hello response we receive is as follows:</span></span>

    HTTP/1.1 200 OK

    { 
      name: 'TestDocument',
      book: ‘Autumn of hello Patriarch’,
      id: ‘V7tQANV3rAkDAAAAAAAAAA==‘,
      ts: 1407830727,
      self: ‘dbs/V7tQAA==/colls/V7tQANV3rAk=/docs/V7tQANV3rAkDAAAAAAAAAA==/’,
      etag: ‘6c006596-0000-0000-0000-53e9cac70000’,
      attachments: ‘attachments/’,
      Price: 200
    }


<span data-ttu-id="224e8-375">Contrairement aux procédures stockées, les déclencheurs ne peuvent pas être exécutés directement.</span><span class="sxs-lookup"><span data-stu-id="224e8-375">Triggers, unlike stored procedures, cannot be executed directly.</span></span> <span data-ttu-id="224e8-376">À la place, ils sont exécutés au sein d'une opération dans un document.</span><span class="sxs-lookup"><span data-stu-id="224e8-376">Instead they are executed as part of an operation on a document.</span></span> <span data-ttu-id="224e8-377">Nous pouvons spécifier hello déclencheurs toorun avec une demande à l’aide d’en-têtes HTTP.</span><span class="sxs-lookup"><span data-stu-id="224e8-377">We can specify hello triggers toorun with a request using HTTP headers.</span></span> <span data-ttu-id="224e8-378">Hello Voici demande toocreate un document.</span><span class="sxs-lookup"><span data-stu-id="224e8-378">hello following is request toocreate a document.</span></span>

    POST https://<url>/docs/ HTTP/1.1
    authorization: <<auth>>
    x-ms-date: Thu, 07 Aug 2014 03:43:10 GMT
    x-ms-documentdb-pre-trigger-include: validateDocumentContents 
    x-ms-documentdb-post-trigger-include: bookCreationPostTrigger


    {
       "name": "newDocument",
       “title”: “hello Wizard of Oz”,
       “author”: “Frank Baum”,
       “pages”: 92
    }


<span data-ttu-id="224e8-379">Ici, toobe de déclencheur préliminaire hello exécuter avec la demande de hello est spécifié dans l’en-tête de x-ms-documentdb-pre-trigger-include de hello.</span><span class="sxs-lookup"><span data-stu-id="224e8-379">Here hello pre-trigger toobe run with hello request is specified in hello x-ms-documentdb-pre-trigger-include header.</span></span> <span data-ttu-id="224e8-380">En conséquence, tous les déclencheurs après figurent dans l’en-tête de x-ms-documentdb-post-trigger-include hello.</span><span class="sxs-lookup"><span data-stu-id="224e8-380">Correspondingly, any post-triggers are given in hello x-ms-documentdb-post-trigger-include header.</span></span> <span data-ttu-id="224e8-381">Notez que les pré- et post-déclencheurs peuvent tous deux être spécifiés pour une demande donnée.</span><span class="sxs-lookup"><span data-stu-id="224e8-381">Note that both pre- and post-triggers can be specified for a given request.</span></span>

## <a name="sample-code"></a><span data-ttu-id="224e8-382">Exemple de code</span><span class="sxs-lookup"><span data-stu-id="224e8-382">Sample code</span></span>
<span data-ttu-id="224e8-383">Vous trouverez d’autres exemples de code côté serveur (notamment [bulk-delete](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples/stored-procedures/bulkDelete.js) et [update](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples/stored-procedures/update.js)) dans notre [référentiel GitHub](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples).</span><span class="sxs-lookup"><span data-stu-id="224e8-383">You can find more server-side code examples (including [bulk-delete](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples/stored-procedures/bulkDelete.js), and [update](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples/stored-procedures/update.js)) on our [GitHub repository](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples).</span></span>

<span data-ttu-id="224e8-384">Vous souhaitez tooshare votre procédure stockée impressionnant ?</span><span class="sxs-lookup"><span data-stu-id="224e8-384">Want tooshare your awesome stored procedure?</span></span> <span data-ttu-id="224e8-385">Envoyez-nous une requête d’extraction !</span><span class="sxs-lookup"><span data-stu-id="224e8-385">Please, send us a pull-request!</span></span> 

## <a name="next-steps"></a><span data-ttu-id="224e8-386">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="224e8-386">Next steps</span></span>
<span data-ttu-id="224e8-387">Une fois que vous avez une ou plusieurs procédures stockées, déclencheurs et fonctions définies par l’utilisateur créées, vous pouvez les charger et les afficher dans hello portail Azure à l’aide de l’Explorateur de données.</span><span class="sxs-lookup"><span data-stu-id="224e8-387">Once you have one or more stored procedures, triggers, and user-defined functions created, you can load them and view them in hello Azure portal using Data Explorer.</span></span>

<span data-ttu-id="224e8-388">Vous pouvez également trouver des éléments suivants de hello références et ressources utiles dans votre chemin d’accès toolearn plus en détail la programmation côté serveur de base de données Azure Cosmos :</span><span class="sxs-lookup"><span data-stu-id="224e8-388">You may also find hello following references and resources useful in your path toolearn more about Azure Cosmos dB server-side programming:</span></span>

* [<span data-ttu-id="224e8-389">Kits SDK Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="224e8-389">Azure Cosmos DB SDKs</span></span>](documentdb-sdk-dotnet.md)
* [<span data-ttu-id="224e8-390">Studio DocumentDB</span><span class="sxs-lookup"><span data-stu-id="224e8-390">DocumentDB Studio</span></span>](https://github.com/mingaliu/DocumentDBStudio/releases)
* [<span data-ttu-id="224e8-391">JSON</span><span class="sxs-lookup"><span data-stu-id="224e8-391">JSON</span></span>](http://www.json.org/) 
* [<span data-ttu-id="224e8-392">JavaScript ECMA-262</span><span class="sxs-lookup"><span data-stu-id="224e8-392">JavaScript ECMA-262</span></span>](http://www.ecma-international.org/publications/standards/Ecma-262.htm)
* [<span data-ttu-id="224e8-393">Extensibilité de la base de données sécurisée et portable</span><span class="sxs-lookup"><span data-stu-id="224e8-393">Secure and Portable Database Extensibility</span></span>](http://dl.acm.org/citation.cfm?id=276339) 
* [<span data-ttu-id="224e8-394">Architecture de base de données orientée services</span><span class="sxs-lookup"><span data-stu-id="224e8-394">Service Oriented Database Architecture</span></span>](http://dl.acm.org/citation.cfm?id=1066267&coll=Portal&dl=GUIDE) 
* [<span data-ttu-id="224e8-395">Hébergement hello Runtime .NET dans Microsoft SQL server</span><span class="sxs-lookup"><span data-stu-id="224e8-395">Hosting hello .NET Runtime in Microsoft SQL server</span></span>](http://dl.acm.org/citation.cfm?id=1007669)

