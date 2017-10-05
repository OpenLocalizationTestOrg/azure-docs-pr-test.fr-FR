---
title: "Modélisation de données de document pour une base de données NoSQL | Microsoft Docs"
description: "Découvrir la modélisation des données pour les bases de données NoSQL"
keywords: "modélisation des données"
services: cosmos-db
author: arramac
manager: jhubbard
editor: mimig1
documentationcenter: 
ms.assetid: 69521eb9-590b-403c-9b36-98253a4c88b5
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/29/2016
ms.author: arramac
ms.openlocfilehash: 16c387fe574243544cf54cf283c7713ddcaa1942
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="modeling-document-data-for-nosql-databases"></a><span data-ttu-id="6c7d4-104">Modélisation de données de document pour des bases de données NoSQL</span><span class="sxs-lookup"><span data-stu-id="6c7d4-104">Modeling document data for NoSQL databases</span></span>
<span data-ttu-id="6c7d4-105">Bien que les bases de données exemptes de schéma, comme Azure Cosmos DB, rendent très facile l’adoption des modifications apportées à votre modèle de données, vous devez quand même prendre le temps de réfléchir à vos données.</span><span class="sxs-lookup"><span data-stu-id="6c7d4-105">While schema-free databases, like Azure Cosmos DB, make it super easy to embrace changes to your data model you should still spend some time thinking about your data.</span></span> 

<span data-ttu-id="6c7d4-106">Comment les données seront-elles stockées ?</span><span class="sxs-lookup"><span data-stu-id="6c7d4-106">How is data going to be stored?</span></span> <span data-ttu-id="6c7d4-107">Comment votre application va-t-elle récupérer et interroger des données ?</span><span class="sxs-lookup"><span data-stu-id="6c7d4-107">How is your application going to retrieve and query data?</span></span> <span data-ttu-id="6c7d4-108">Votre application exige-t-elle de nombreuses lectures (read heavy) ou de nombreuses écritures (write heavy) ?</span><span class="sxs-lookup"><span data-stu-id="6c7d4-108">Is your application read heavy, or write heavy?</span></span> 

<span data-ttu-id="6c7d4-109">Après avoir lu cet article, vous serez en mesure de répondre aux questions suivantes :</span><span class="sxs-lookup"><span data-stu-id="6c7d4-109">After reading this article, you will be able to answer the following questions:</span></span>

* <span data-ttu-id="6c7d4-110">Comment dois-je considérer un document dans une base de données de documents ?</span><span class="sxs-lookup"><span data-stu-id="6c7d4-110">How should I think about a document in a document database?</span></span>
* <span data-ttu-id="6c7d4-111">Qu'est-ce que la modélisation de données et pourquoi dois-je m'en soucier ?</span><span class="sxs-lookup"><span data-stu-id="6c7d4-111">What is data modeling and why should I care?</span></span> 
* <span data-ttu-id="6c7d4-112">En quoi la modélisation des données dans une base de données de documents et dans une base de données relationnelle diffère-t-elle ?</span><span class="sxs-lookup"><span data-stu-id="6c7d4-112">How is modeling data in a document database different to a relational database?</span></span>
* <span data-ttu-id="6c7d4-113">Comment exprimer les relations entre les données dans une base de données non relationnelle ?</span><span class="sxs-lookup"><span data-stu-id="6c7d4-113">How do I express data relationships in a non-relational database?</span></span>
* <span data-ttu-id="6c7d4-114">Quand dois-je incorporer les données et quand dois-je créer un lien vers les données ?</span><span class="sxs-lookup"><span data-stu-id="6c7d4-114">When do I embed data and when do I link to data?</span></span>

## <a name="embedding-data"></a><span data-ttu-id="6c7d4-115">Incorporation de données</span><span class="sxs-lookup"><span data-stu-id="6c7d4-115">Embedding data</span></span>
<span data-ttu-id="6c7d4-116">Lorsque vous entamez la modélisation des données dans une banque de documents telle qu’Azure Cosmos DB, essayez de traiter vos entités en tant que **documents autonomes** représentés dans JSON.</span><span class="sxs-lookup"><span data-stu-id="6c7d4-116">When you start modeling data in a document store, such as Azure Cosmos DB, try to treat your entities as **self-contained documents** represented in JSON.</span></span>

<span data-ttu-id="6c7d4-117">Avant d'aller trop loin, revenons quelques étapes en arrière et examinons comment nous pouvons modéliser un élément dans une base de données relationnelle. Beaucoup d'entre nous connaissent déjà le sujet.</span><span class="sxs-lookup"><span data-stu-id="6c7d4-117">Before we dive in too much further, let us take a few steps back and have a look at how we might model something in a relational database, a subject many of us are already familiar with.</span></span> <span data-ttu-id="6c7d4-118">L'exemple suivant montre comment une personne peut être stockée dans une base de données relationnelle.</span><span class="sxs-lookup"><span data-stu-id="6c7d4-118">The following example shows how a person might be stored in a relational database.</span></span> 

![Modèle de base de données relationnelle](./media/documentdb-modeling-data/relational-data-model.png)

<span data-ttu-id="6c7d4-120">Lorsqu'il s'agit de travailler avec des bases de données relationnelles, on nous a appris pendant des années qu'il fallait normaliser, normaliser, normaliser.</span><span class="sxs-lookup"><span data-stu-id="6c7d4-120">When working with relational databases, we've been taught for years to normalize, normalize, normalize.</span></span>

<span data-ttu-id="6c7d4-121">En général, la normalisation de vos données consiste à prendre une entité, une personne par exemple, et à la décomposer en éléments de données discrets.</span><span class="sxs-lookup"><span data-stu-id="6c7d4-121">Normalizing your data typically involves taking an entity, such as a person, and breaking it down in to discrete pieces of data.</span></span> <span data-ttu-id="6c7d4-122">Dans l'exemple ci-dessus, une personne peut avoir plusieurs enregistrements de coordonnées, ainsi que plusieurs enregistrements d'adresse.</span><span class="sxs-lookup"><span data-stu-id="6c7d4-122">In the example above, a person can have multiple contact detail records as well as multiple address records.</span></span> <span data-ttu-id="6c7d4-123">Nous allons même plus loin et décomposons les coordonnées en extrayant des champs communs tels qu'un type.</span><span class="sxs-lookup"><span data-stu-id="6c7d4-123">We even go one step further and break down contact details by further extracting common fields like a type.</span></span> <span data-ttu-id="6c7d4-124">Même chose pour l’adresse : chaque enregistrement ici a un type, tel que *Home* ou *Business*.</span><span class="sxs-lookup"><span data-stu-id="6c7d4-124">Same for address, each record here has a type like *Home* or *Business*</span></span> 

<span data-ttu-id="6c7d4-125">Le principe directeur lors de la normalisation des données consiste à **éviter de stocker des données redondantes** dans chaque enregistrement et à faire plutôt référence aux données.</span><span class="sxs-lookup"><span data-stu-id="6c7d4-125">The guiding premise when normalizing data is to **avoid storing redundant data** on each record and rather refer to data.</span></span> <span data-ttu-id="6c7d4-126">Dans cet exemple, pour lire une personne, avec ses coordonnées et ses adresses, vous devez utiliser des jointures pour agréger efficacement vos données au moment de l'exécution.</span><span class="sxs-lookup"><span data-stu-id="6c7d4-126">In this example, to read a person, with all their contact details and addresses, you need to use JOINS to effectively aggregate your data at run time.</span></span>

    SELECT p.FirstName, p.LastName, a.City, cd.Detail
    FROM Person p
    JOIN ContactDetail cd ON cd.PersonId = p.Id
    JOIN ContactDetailType on cdt ON cdt.Id = cd.TypeId
    JOIN Address a ON a.PersonId = p.Id

<span data-ttu-id="6c7d4-127">La mise à jour d'une personne avec ses coordonnées et adresses nécessite des opérations d'écriture sur plusieurs tables individuelles.</span><span class="sxs-lookup"><span data-stu-id="6c7d4-127">Updating a single person with their contact details and addresses requires write operations across many individual tables.</span></span> 

<span data-ttu-id="6c7d4-128">Examinons à présent comment nous pourrions modéliser les mêmes données comme une entité autonome dans une base de données de documents.</span><span class="sxs-lookup"><span data-stu-id="6c7d4-128">Now let's take a look at how we would model the same data as a self-contained entity in a document database.</span></span>

    {
        "id": "1",
        "firstName": "Thomas",
        "lastName": "Andersen",
        "addresses": [
            {            
                "line1": "100 Some Street",
                "line2": "Unit 1",
                "city": "Seattle",
                "state": "WA",
                "zip": 98012
            }
        ],
        "contactDetails": [
            {"email: "thomas@andersen.com"},
            {"phone": "+1 555 555-5555", "extension": 5555}
        ] 
    }

<span data-ttu-id="6c7d4-129">Avec l’approche ci-dessus, nous avons maintenant **dénormalisé** l’enregistrement de la personne, où nous avons **incorporé** toutes les informations relatives à cette personne, telles que ses coordonnées et adresses, dans un seul document JSON.</span><span class="sxs-lookup"><span data-stu-id="6c7d4-129">Using the approach above we have now **denormalized** the person record where we **embedded** all the information relating to this person, such as their contact details and addresses, in to a single JSON document.</span></span>
<span data-ttu-id="6c7d4-130">En outre, étant donné que nous ne sommes pas limités à un schéma fixe, nous avons la possibilité d'avoir des coordonnées de formes entièrement différentes.</span><span class="sxs-lookup"><span data-stu-id="6c7d4-130">In addition, because we're not confined to a fixed schema we have the flexibility to do things like having contact details of different shapes entirely.</span></span> 

<span data-ttu-id="6c7d4-131">La récupération d'un enregistrement complet de personne dans la base de données correspond désormais à une seule opération de lecture sur une collection unique et pour un document unique.</span><span class="sxs-lookup"><span data-stu-id="6c7d4-131">Retrieving a complete person record from the database is now a single read operation against a single collection and for a single document.</span></span> <span data-ttu-id="6c7d4-132">La mise à jour d'un enregistrement de personne, avec ses coordonnées et adresses, correspond également à une seule opération d'écriture sur un document unique.</span><span class="sxs-lookup"><span data-stu-id="6c7d4-132">Updating a person record, with their contact details and addresses, is also a single write operation against a single document.</span></span>

<span data-ttu-id="6c7d4-133">Avec la dénormalisation des données, votre application aura peut-être besoin d'émettre moins de requêtes et de mises à jour pour effectuer les opérations courantes.</span><span class="sxs-lookup"><span data-stu-id="6c7d4-133">By denormalizing data, your application may need to issue fewer queries and updates to complete common operations.</span></span> 

### <a name="when-to-embed"></a><span data-ttu-id="6c7d4-134">Quand utiliser l'incorporation</span><span class="sxs-lookup"><span data-stu-id="6c7d4-134">When to embed</span></span>
<span data-ttu-id="6c7d4-135">En général, utilisez des modèles de données incorporés dans les cas suivants :</span><span class="sxs-lookup"><span data-stu-id="6c7d4-135">In general, use embedded data models when:</span></span>

* <span data-ttu-id="6c7d4-136">Il existe des relations de type **contient** entre des entités.</span><span class="sxs-lookup"><span data-stu-id="6c7d4-136">There are **contains** relationships between entities.</span></span>
* <span data-ttu-id="6c7d4-137">Il existe des relations de type **un-à-plusieurs** entre des entités.</span><span class="sxs-lookup"><span data-stu-id="6c7d4-137">There are **one-to-few** relationships between entities.</span></span>
* <span data-ttu-id="6c7d4-138">Des données incorporées **changent rarement**.</span><span class="sxs-lookup"><span data-stu-id="6c7d4-138">There is embedded data that **changes infrequently**.</span></span>
* <span data-ttu-id="6c7d4-139">Des données incorporées ne croîtront pas **sans limite**.</span><span class="sxs-lookup"><span data-stu-id="6c7d4-139">There is embedded data won't grow **without bound**.</span></span>
* <span data-ttu-id="6c7d4-140">Des données incorporées sont une partie **intégrante** des données d’un document.</span><span class="sxs-lookup"><span data-stu-id="6c7d4-140">There is embedded data that is **integral** to data in a document.</span></span>

> [!NOTE]
> <span data-ttu-id="6c7d4-141">Normalement, les modèles de données dénormalisés offrent de meilleures performances en **lecture** .</span><span class="sxs-lookup"><span data-stu-id="6c7d4-141">Typically denormalized data models provide better **read** performance.</span></span>
> 
> 

### <a name="when-not-to-embed"></a><span data-ttu-id="6c7d4-142">Quand éviter l'incorporation</span><span class="sxs-lookup"><span data-stu-id="6c7d4-142">When not to embed</span></span>
<span data-ttu-id="6c7d4-143">Bien que la règle générale dans une base de données de documents soit de tout dénormaliser et d'incorporer toutes les données dans un seul document, cela peut déboucher sur des situations qui devraient être évitées.</span><span class="sxs-lookup"><span data-stu-id="6c7d4-143">While the rule of thumb in a document database is to denormalize everything and embed all data in to a single document, this can lead to some situations that should be avoided.</span></span>

<span data-ttu-id="6c7d4-144">Prenons cet extrait de code JSON.</span><span class="sxs-lookup"><span data-stu-id="6c7d4-144">Take this JSON snippet.</span></span>

    {
        "id": "1",
        "name": "What's new in the coolest Cloud",
        "summary": "A blog post by someone real famous",
        "comments": [
            {"id": 1, "author": "anon", "comment": "something useful, I'm sure"},
            {"id": 2, "author": "bob", "comment": "wisdom from the interwebs"},
            …
            {"id": 100001, "author": "jane", "comment": "and on we go ..."},
            …
            {"id": 1000000001, "author": "angry", "comment": "blah angry blah angry"},
            …
            {"id": ∞ + 1, "author": "bored", "comment": "oh man, will this ever end?"},
        ]
    }

<span data-ttu-id="6c7d4-145">Une entité post avec commentaires incorporés pourrait avoir cet aspect si nous étions en train de modéliser un système de blog, ou CMS, classique.</span><span class="sxs-lookup"><span data-stu-id="6c7d4-145">This might be what a post entity with embedded comments would look like if we were modeling a typical blog, or CMS, system.</span></span> <span data-ttu-id="6c7d4-146">Dans cet exemple, le problème est que le tableau de commentaires est **illimité**, c’est-à-dire qu’il n’existe aucune limite (pratique) au nombre de commentaires possibles pour une publication.</span><span class="sxs-lookup"><span data-stu-id="6c7d4-146">The problem with this example is that the comments array is **unbounded**, meaning that there is no (practical) limit to the number of comments any single post can have.</span></span> <span data-ttu-id="6c7d4-147">Cela posera un problème car la taille du document risque d'augmenter considérablement.</span><span class="sxs-lookup"><span data-stu-id="6c7d4-147">This will become a problem as the size of the document could grow significantly.</span></span>

<span data-ttu-id="6c7d4-148">L'augmentation de la taille du document a une incidence sur les possibilités de transmission des données par câble, ainsi que sur les possibilités de lecture et de mise à jour du document, à l'échelle.</span><span class="sxs-lookup"><span data-stu-id="6c7d4-148">As the size of the document grows the ability to transmit the data over the wire as well as reading and updating the document, at scale, will be impacted.</span></span>

<span data-ttu-id="6c7d4-149">Dans ce cas, il serait préférable de considérer le modèle suivant.</span><span class="sxs-lookup"><span data-stu-id="6c7d4-149">In this case it would be better to consider the following model.</span></span>

    Post document:
    {
        "id": "1",
        "name": "What's new in the coolest Cloud",
        "summary": "A blog post by someone real famous",
        "recentComments": [
            {"id": 1, "author": "anon", "comment": "something useful, I'm sure"},
            {"id": 2, "author": "bob", "comment": "wisdom from the interwebs"},
            {"id": 3, "author": "jane", "comment": "....."}
        ]
    }

    Comment documents:
    {
        "postId": "1"
        "comments": [
            {"id": 4, "author": "anon", "comment": "more goodness"},
            {"id": 5, "author": "bob", "comment": "tails from the field"},
            ...
            {"id": 99, "author": "angry", "comment": "blah angry blah angry"}
        ]
    },
    {
        "postId": "1"
        "comments": [
            {"id": 100, "author": "anon", "comment": "yet more"},
            ...
            {"id": 199, "author": "bored", "comment": "will this ever end?"}
        ]
    }

<span data-ttu-id="6c7d4-150">Ce modèle présente les trois derniers commentaires incorporés dans la publication proprement dite, qui est un tableau avec une limite fixe cette fois-ci.</span><span class="sxs-lookup"><span data-stu-id="6c7d4-150">This model has the three most recent comments embedded on the post itself, which is an array with a fixed bound this time.</span></span> <span data-ttu-id="6c7d4-151">Les autres commentaires sont regroupés par lots de 100 commentaires et stockés dans des documents distincts.</span><span class="sxs-lookup"><span data-stu-id="6c7d4-151">The other comments are grouped in to batches of 100 comments and stored in separate documents.</span></span> <span data-ttu-id="6c7d4-152">100 a été choisi comme taille de lot parce que notre application fictive permet à l'utilisateur de charger 100 commentaires à la fois.</span><span class="sxs-lookup"><span data-stu-id="6c7d4-152">The size of the batch was chosen as 100 because our fictitious application allows the user to load 100 comments at a time.</span></span>  

<span data-ttu-id="6c7d4-153">Autre cas de figure où l'incorporation de données est déconseillée : lorsque les données incorporées sont souvent utilisées dans les documents et changent fréquemment.</span><span class="sxs-lookup"><span data-stu-id="6c7d4-153">Another case where embedding data is not a good idea is when the embedded data is used often across documents and will change frequently.</span></span> 

<span data-ttu-id="6c7d4-154">Prenons cet extrait de code JSON.</span><span class="sxs-lookup"><span data-stu-id="6c7d4-154">Take this JSON snippet.</span></span>

    {
        "id": "1",
        "firstName": "Thomas",
        "lastName": "Andersen",
        "holdings": [
            {
                "numberHeld": 100,
                "stock": { "symbol": "zaza", "open": 1, "high": 2, "low": 0.5 }
            },
            {
                "numberHeld": 50,
                "stock": { "symbol": "xcxc", "open": 89, "high": 93.24, "low": 88.87 }
            }
        ]
    }

<span data-ttu-id="6c7d4-155">Il pourrait représenter le portefeuille d'actions d'une personne.</span><span class="sxs-lookup"><span data-stu-id="6c7d4-155">This could represent a person's stock portfolio.</span></span> <span data-ttu-id="6c7d4-156">Nous avons choisi d'incorporer les informations boursières dans chaque document de portefeuille.</span><span class="sxs-lookup"><span data-stu-id="6c7d4-156">We have chosen to embed the stock information in to each portfolio document.</span></span> <span data-ttu-id="6c7d4-157">Dans un environnement où les données associées changent fréquemment, comme une application de transactions boursières, incorporer les données qui changent fréquemment signifie que vous devez mettre à jour constamment chaque document de portefeuille, chaque fois que des actions sont échangées.</span><span class="sxs-lookup"><span data-stu-id="6c7d4-157">In an environment where related data is changing frequently, like a stock trading application, embedding data that changes frequently is going to mean that you are constantly updating each portfolio document every time a stock is traded.</span></span>

<span data-ttu-id="6c7d4-158">Des actions *zaza* peuvent être échangées des centaines de fois au cours d’une même journée, et des milliers d’utilisateurs peuvent posséder des actions *zaza* dans leur portefeuille.</span><span class="sxs-lookup"><span data-stu-id="6c7d4-158">Stock *zaza* may be traded many hundreds of times in a single day and thousands of users could have *zaza* on their portfolio.</span></span> <span data-ttu-id="6c7d4-159">Avec un modèle de données comme le modèle ci-dessus, nous devons mettre à jour quotidiennement et à de nombreuses reprises des milliers de documents de portefeuille. Cela aboutit à un système qui n'est pas très évolutif.</span><span class="sxs-lookup"><span data-stu-id="6c7d4-159">With a data model like the above we would have to update many thousands of portfolio documents many times every day leading to a system that won't scale very well.</span></span> 

## <span data-ttu-id="6c7d4-160"><a id="Refer"></a>Référencement des données</span><span class="sxs-lookup"><span data-stu-id="6c7d4-160"><a id="Refer"></a>Referencing data</span></span>
<span data-ttu-id="6c7d4-161">Ainsi, l'incorporation de données fonctionne bien dans la plupart des cas, mais il est clair qu'il existe des scénarios où la dénormalisation de vos données provoque plus de problèmes qu'il n'en faudrait.</span><span class="sxs-lookup"><span data-stu-id="6c7d4-161">So, embedding data works nicely for many cases but it is clear that there are scenarios when denormalizing your data will cause more problems than it is worth.</span></span> <span data-ttu-id="6c7d4-162">Que faire, alors ?</span><span class="sxs-lookup"><span data-stu-id="6c7d4-162">So what do we do now?</span></span> 

<span data-ttu-id="6c7d4-163">Les bases de données relationnelles ne sont pas le seul endroit où vous pouvez créer des relations entre les entités.</span><span class="sxs-lookup"><span data-stu-id="6c7d4-163">Relational databases are not the only place where you can create relationships between entities.</span></span> <span data-ttu-id="6c7d4-164">Dans une base de données de documents, vous pouvez avoir des informations dans un document qui sont en relation avec des données dans autres documents.</span><span class="sxs-lookup"><span data-stu-id="6c7d4-164">In a document database you can have information in one document that actually relates to data in other documents.</span></span> <span data-ttu-id="6c7d4-165">Maintenant, je ne préconise absolument pas de créer des systèmes qui seraient mieux adaptés à une base de données relationnelle dans Azure Cosmos DB, ou toute autre base de données de documents, mais de simples relations conviennent et peuvent être très utiles.</span><span class="sxs-lookup"><span data-stu-id="6c7d4-165">Now, I am not advocating for even one minute that we build systems that would be better suited to a relational database in Azure Cosmos DB, or any other document database, but simple relationships are fine and can be very useful.</span></span> 

<span data-ttu-id="6c7d4-166">Dans le code JSON ci-dessous, nous avons choisi d'utiliser l'exemple de portefeuille d'actions précédent, mais cette fois, nous faisons référence à l'action dans le portefeuille au lieu de l'incorporer.</span><span class="sxs-lookup"><span data-stu-id="6c7d4-166">In the JSON below we chose to use the example of a stock portfolio from earlier but this time we refer to the stock item on the portfolio instead of embedding it.</span></span> <span data-ttu-id="6c7d4-167">Ainsi, lorsque l'action change fréquemment au cours de la journée, le seul document à mettre à jour est le document d'action (stock).</span><span class="sxs-lookup"><span data-stu-id="6c7d4-167">This way, when the stock item changes frequently throughout the day the only document that needs to be updated is the single stock document.</span></span> 

    Person document:
    {
        "id": "1",
        "firstName": "Thomas",
        "lastName": "Andersen",
        "holdings": [
            { "numberHeld":  100, "stockId": 1},
            { "numberHeld":  50, "stockId": 2}
        ]
    }

    Stock documents:
    {
        "id": "1",
        "symbol": "zaza",
        "open": 1,
        "high": 2,
        "low": 0.5,
        "vol": 11970000,
        "mkt-cap": 42000000,
        "pe": 5.89
    },
    {
        "id": "2",
        "symbol": "xcxc",
        "open": 89,
        "high": 93.24,
        "low": 88.87,
        "vol": 2970200,
        "mkt-cap": 1005000,
        "pe": 75.82
    }


<span data-ttu-id="6c7d4-168">Cette approche présente cependant un inconvénient si votre application doit afficher des informations sur chaque action qui est conservée lors de l'affichage du portefeuille d'une personne ; dans ce cas, vous devez faire plusieurs aller et retour jusqu'à la base de données afin de charger les informations pour chaque document d'action.</span><span class="sxs-lookup"><span data-stu-id="6c7d4-168">An immediate downside to this approach though is if your application is required to show information about each stock that is held when displaying a person's portfolio; in this case you would need to make multiple trips to the database to load the information for each stock document.</span></span> <span data-ttu-id="6c7d4-169">Ici, nous avons pris une décision pour améliorer l'efficacité des opérations d'écriture, qui ont lieu fréquemment pendant la journée, mais nous avons fait un compromis sur les opérations de lecture, qui ont potentiellement moins d'impact sur les performances de ce système.</span><span class="sxs-lookup"><span data-stu-id="6c7d4-169">Here we've made a decision to improve the efficiency of write operations, which happen frequently throughout the day, but in turn compromised on the read operations that potentially have less impact on the performance of this particular system.</span></span>

> [!NOTE]
> <span data-ttu-id="6c7d4-170">Les modèles de données normalisés **peuvent nécessiter davantage d’aller-retour** jusqu’au serveur.</span><span class="sxs-lookup"><span data-stu-id="6c7d4-170">Normalized data models **can require more round trips** to the server.</span></span>
> 
> 

### <a name="what-about-foreign-keys"></a><span data-ttu-id="6c7d4-171">Qu'en est-il des clés étrangères ?</span><span class="sxs-lookup"><span data-stu-id="6c7d4-171">What about foreign keys?</span></span>
<span data-ttu-id="6c7d4-172">Dans la mesure où il n'existe actuellement aucun concept d'une contrainte (clé étrangère ou autre), toutes les relations entre documents que vous avez dans les documents sont effectivement des « liens faibles » et elles ne sont pas vérifiées par la base de données.</span><span class="sxs-lookup"><span data-stu-id="6c7d4-172">Because there is currently no concept of a constraint, foreign-key or otherwise, any inter-document relationships that you have in documents are effectively "weak links" and will not be verified by the database itself.</span></span> <span data-ttu-id="6c7d4-173">Si vous souhaitez vous assurer que les données auxquelles un document fait référence existent réellement, vous devez le faire dans votre application, ou en utilisant des déclencheurs côté serveur ou des procédures stockées sur Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="6c7d4-173">If you want to ensure that the data a document is referring to actually exists, then you need to do this in your application, or through the use of server-side triggers or stored procedures on Azure Cosmos DB.</span></span>

### <a name="when-to-reference"></a><span data-ttu-id="6c7d4-174">Quand utiliser des références</span><span class="sxs-lookup"><span data-stu-id="6c7d4-174">When to reference</span></span>
<span data-ttu-id="6c7d4-175">En général, utilisez des modèles de données normalisés dans les cas suivants :</span><span class="sxs-lookup"><span data-stu-id="6c7d4-175">In general, use normalized data models when:</span></span>

* <span data-ttu-id="6c7d4-176">Représentation des relations **un-à-plusieurs** .</span><span class="sxs-lookup"><span data-stu-id="6c7d4-176">Representing **one-to-many** relationships.</span></span>
* <span data-ttu-id="6c7d4-177">Représentation des relations **plusieurs-à-plusieurs** .</span><span class="sxs-lookup"><span data-stu-id="6c7d4-177">Representing **many-to-many** relationships.</span></span>
* <span data-ttu-id="6c7d4-178">Les données associées **changent fréquemment**.</span><span class="sxs-lookup"><span data-stu-id="6c7d4-178">Related data **changes frequently**.</span></span>
* <span data-ttu-id="6c7d4-179">Les données référencées peuvent être **illimitées**.</span><span class="sxs-lookup"><span data-stu-id="6c7d4-179">Referenced data could be **unbounded**.</span></span>

> [!NOTE]
> <span data-ttu-id="6c7d4-180">En général, la normalisation offre de meilleures performances en **écriture** .</span><span class="sxs-lookup"><span data-stu-id="6c7d4-180">Typically normalizing provides better **write** performance.</span></span>
> 
> 

### <a name="where-do-i-put-the-relationship"></a><span data-ttu-id="6c7d4-181">Où placer la relation ?</span><span class="sxs-lookup"><span data-stu-id="6c7d4-181">Where do I put the relationship?</span></span>
<span data-ttu-id="6c7d4-182">La croissance de la relation permet de déterminer dans quel document doit être stockée la référence.</span><span class="sxs-lookup"><span data-stu-id="6c7d4-182">The growth of the relationship will help determine in which document to store the reference.</span></span>

<span data-ttu-id="6c7d4-183">Examinons le code JSON ci-dessous qui modélise des éditeurs et des livres :</span><span class="sxs-lookup"><span data-stu-id="6c7d4-183">If we look at the JSON below that models publishers and books.</span></span>

    Publisher document:
    {
        "id": "mspress",
        "name": "Microsoft Press",
        "books": [ 1, 2, 3, ..., 100, ..., 1000]
    }

    Book documents:
    {"id": "1", "name": "Azure Cosmos DB 101" }
    {"id": "2", "name": "Azure Cosmos DB for RDBMS Users" }
    {"id": "3", "name": "Taking over the world one JSON doc at a time" }
    ...
    {"id": "100", "name": "Learn about Azure Cosmos DB" }
    ...
    {"id": "1000", "name": "Deep Dive in to Azure Cosmos DB" }

<span data-ttu-id="6c7d4-184">Si le nombre de livres par éditeur est peu élevé avec une croissance faible limitée, il peut être utile de stocker la référence du livre dans le document d'éditeur (publisher).</span><span class="sxs-lookup"><span data-stu-id="6c7d4-184">If the number of the books per publisher is small with limited growth, then storing the book reference inside the publisher document may be useful.</span></span> <span data-ttu-id="6c7d4-185">Toutefois, si le nombre de livres par éditeur est illimité, ce modèle de données aboutira à des tableaux mutables, croissants, comme dans l'exemple de document d'éditeur ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="6c7d4-185">However, if the number of books per publisher is unbounded, then this data model would lead to mutable, growing arrays, as in the example publisher document above.</span></span> 

<span data-ttu-id="6c7d4-186">Un petit changement donnera un modèle qui représente toujours les mêmes données, mais évite désormais ces grandes collections mutables.</span><span class="sxs-lookup"><span data-stu-id="6c7d4-186">Switching things around a bit would result in a model that still represents the same data but now avoids these large mutable collections.</span></span>

    Publisher document: 
    {
        "id": "mspress",
        "name": "Microsoft Press"
    }

    Book documents: 
    {"id": "1","name": "Azure Cosmos DB 101", "pub-id": "mspress"}
    {"id": "2","name": "Azure Cosmos DB for RDBMS Users", "pub-id": "mspress"}
    {"id": "3","name": "Taking over the world one JSON doc at a time"}
    ...
    {"id": "100","name": "Learn about Azure Cosmos DB", "pub-id": "mspress"}
    ...
    {"id": "1000","name": "Deep Dive in to Azure Cosmos DB", "pub-id": "mspress"}

<span data-ttu-id="6c7d4-187">Dans l'exemple ci-dessus, nous avons supprimé la collection illimitée dans le document d'éditeur (publisher).</span><span class="sxs-lookup"><span data-stu-id="6c7d4-187">In the above example, we have dropped the unbounded collection on the publisher document.</span></span> <span data-ttu-id="6c7d4-188">Nous avons simplement une référence à l'éditeur dans chaque document de livre (book).</span><span class="sxs-lookup"><span data-stu-id="6c7d4-188">Instead we just have a a reference to the publisher on each book document.</span></span>

### <a name="how-do-i-model-manymany-relationships"></a><span data-ttu-id="6c7d4-189">Comment modéliser des relations plusieurs-à-plusieurs ?</span><span class="sxs-lookup"><span data-stu-id="6c7d4-189">How do I model many:many relationships?</span></span>
<span data-ttu-id="6c7d4-190">Dans une base de données relationnelle *plusieurs-à-plusieurs* , les relations sont souvent modélisées avec des tables de jointure qui relient simplement les enregistrements d’autres tables.</span><span class="sxs-lookup"><span data-stu-id="6c7d4-190">In a relational database *many:many* relationships are often modeled with join tables, which just join records from other tables together.</span></span> 

![Tables de jointures](./media/documentdb-modeling-data/join-table.png)

<span data-ttu-id="6c7d4-192">Vous pouvez être tenté de répliquer la même chose à l'aide de documents et de générer un modèle de données qui ressemble à ce qui suit.</span><span class="sxs-lookup"><span data-stu-id="6c7d4-192">You might be tempted to replicate the same thing using documents and produce a data model that looks similar to the following.</span></span>

    Author documents: 
    {"id": "a1", "name": "Thomas Andersen" }
    {"id": "a2", "name": "William Wakefield" }

    Book documents:
    {"id": "b1", "name": "Azure Cosmos DB 101" }
    {"id": "b2", "name": "Azure Cosmos DB for RDBMS Users" }
    {"id": "b3", "name": "Taking over the world one JSON doc at a time" }
    {"id": "b4", "name": "Learn about Azure Cosmos DB" }
    {"id": "b5", "name": "Deep Dive in to Azure Cosmos DB" }

    Joining documents: 
    {"authorId": "a1", "bookId": "b1" }
    {"authorId": "a2", "bookId": "b1" }
    {"authorId": "a1", "bookId": "b2" }
    {"authorId": "a1", "bookId": "b3" }

<span data-ttu-id="6c7d4-193">Cette méthode fonctionne.</span><span class="sxs-lookup"><span data-stu-id="6c7d4-193">This would work.</span></span> <span data-ttu-id="6c7d4-194">Toutefois, le fait de charger soit un auteur avec ses livres soit un livre avec son auteur nécessite toujours au moins deux requêtes supplémentaires sur la base de données.</span><span class="sxs-lookup"><span data-stu-id="6c7d4-194">However, loading either an author with their books, or loading a book with its author, would always require at least two additional queries against the database.</span></span> <span data-ttu-id="6c7d4-195">Une requête pour le document de jointure (joining) et une autre requête pour extraire le document joint.</span><span class="sxs-lookup"><span data-stu-id="6c7d4-195">One query to the joining document and then another query to fetch the actual document being joined.</span></span> 

<span data-ttu-id="6c7d4-196">Si cette table de jointure ne fait rien d'autre que coller ensemble deux éléments de données, pourquoi ne pas la supprimer complètement ?</span><span class="sxs-lookup"><span data-stu-id="6c7d4-196">If all this join table is doing is gluing together two pieces of data, then why not drop it completely?</span></span>
<span data-ttu-id="6c7d4-197">Examinons le code suivant.</span><span class="sxs-lookup"><span data-stu-id="6c7d4-197">Consider the following.</span></span>

    Author documents:
    {"id": "a1", "name": "Thomas Andersen", "books": ["b1, "b2", "b3"]}
    {"id": "a2", "name": "William Wakefield", "books": ["b1", "b4"]}

    Book documents: 
    {"id": "b1", "name": "Azure Cosmos DB 101", "authors": ["a1", "a2"]}
    {"id": "b2", "name": "Azure Cosmos DB for RDBMS Users", "authors": ["a1"]}
    {"id": "b3", "name": "Learn about Azure Cosmos DB", "authors": ["a1"]}
    {"id": "b4", "name": "Deep Dive in to Azure Cosmos DB", "authors": ["a2"]}

<span data-ttu-id="6c7d4-198">Maintenant, si j'ai un auteur, je saurai immédiatement quels livres il a écrits, et inversement, si j'ai un document de livre (book) chargé, je connaîtrai le ou les ID des auteurs.</span><span class="sxs-lookup"><span data-stu-id="6c7d4-198">Now, if I had an author, I immediately know which books they have written, and conversely if I had a book document loaded I would know the ids of the author(s).</span></span> <span data-ttu-id="6c7d4-199">Cela permet de faire l'économie de cette requête intermédiaire sur la table de jointure en réduisant le nombre d'aller et retour jusqu'au serveur pour votre application.</span><span class="sxs-lookup"><span data-stu-id="6c7d4-199">This saves that intermediary query against the join table reducing the number of server round trips your application has to make.</span></span> 

## <span data-ttu-id="6c7d4-200"><a id="WrapUp"></a>Modèles de données hybrides</span><span class="sxs-lookup"><span data-stu-id="6c7d4-200"><a id="WrapUp"></a>Hybrid data models</span></span>
<span data-ttu-id="6c7d4-201">Nous savons maintenant que l'incorporation (ou la dénormalisation) et le référencement (ou la normalisation) des données ont tous deux leurs avantages, mais qu'ils impliquent également des compromis.</span><span class="sxs-lookup"><span data-stu-id="6c7d4-201">We've now looked embedding (or denormalizing) and referencing (or normalizing) data, each have their upsides and each have compromises as we have seen.</span></span> 

<span data-ttu-id="6c7d4-202">Vous n'êtes pas toujours obligé de choisir soit l'un soit l'autre. N'ayez pas peur de combiner les deux.</span><span class="sxs-lookup"><span data-stu-id="6c7d4-202">It doesn't always have to be either or, don't be scared to mix things up a little.</span></span> 

<span data-ttu-id="6c7d4-203">En fonction des modèles d'utilisation et des charges de travail spécifiques de votre application, dans certains cas, la combinaison de données incorporées et de données référencées peut s'avérer intéressante et conduire à une logique d'application plus simple, avec moins d'aller et retour jusqu'au serveur, tout en préservant un bon niveau de performances.</span><span class="sxs-lookup"><span data-stu-id="6c7d4-203">Based on your application's specific usage patterns and workloads there may be cases where mixing embedded and referenced data makes sense and could lead to simpler application logic with fewer server round trips while still maintaining a good level of performance.</span></span>

<span data-ttu-id="6c7d4-204">Examinons le code JSON suivant.</span><span class="sxs-lookup"><span data-stu-id="6c7d4-204">Consider the following JSON.</span></span> 

    Author documents: 
    {
        "id": "a1",
        "firstName": "Thomas",
        "lastName": "Andersen",        
        "countOfBooks": 3,
         "books": ["b1", "b2", "b3"],
        "images": [
            {"thumbnail": "http://....png"}
            {"profile": "http://....png"}
            {"large": "http://....png"}
        ]
    },
    {
        "id": "a2",
        "firstName": "William",
        "lastName": "Wakefield",
        "countOfBooks": 1,
        "books": ["b1"],
        "images": [
            {"thumbnail": "http://....png"}
        ]
    }

    Book documents:
    {
        "id": "b1",
        "name": "Azure Cosmos DB 101",
        "authors": [
            {"id": "a1", "name": "Thomas Andersen", "thumbnailUrl": "http://....png"},
            {"id": "a2", "name": "William Wakefield", "thumbnailUrl": "http://....png"}
        ]
    },
    {
        "id": "b2",
        "name": "Azure Cosmos DB for RDBMS Users",
        "authors": [
            {"id": "a1", "name": "Thomas Andersen", "thumbnailUrl": "http://....png"},
        ]
    }

<span data-ttu-id="6c7d4-205">Ici nous avons suivi (principalement) le modèle incorporé, où les données des autres entités sont incorporées dans le document de niveau supérieur, mais les autres données sont référencées.</span><span class="sxs-lookup"><span data-stu-id="6c7d4-205">Here we've (mostly) followed the embedded model, where data from other entities are embedded in the top-level document, but other data is referenced.</span></span> 

<span data-ttu-id="6c7d4-206">Dans le document de livre (book), nous pouvons voir quelques champs intéressants lorsque nous examinons le tableau des auteurs.</span><span class="sxs-lookup"><span data-stu-id="6c7d4-206">If you look at the book document, we can see a few interesting fields when we look at the array of authors.</span></span> <span data-ttu-id="6c7d4-207">Il existe un champ *id* que nous utilisons pour faire référence à un document d’auteur (author), une pratique courante dans un modèle normalisé, mais nous avons également les champs *name* et *thumbnailUrl*.</span><span class="sxs-lookup"><span data-stu-id="6c7d4-207">There is an *id* field which is the field we use to refer back to an author document, standard practice in a normalized model, but then we also have *name* and *thumbnailUrl*.</span></span> <span data-ttu-id="6c7d4-208">Nous aurions pu nous arrêter à l’ *id* et laisser l’application obtenir les informations supplémentaires dont elle avait besoin à partir du document d’auteur (author) respectif à l’aide du « lien », mais comme notre application affiche le nom de l’auteur et une image miniature avec chaque livre, nous pouvons économiser un aller-retour par livre jusqu’au serveur en dénormalisant **certaines** données de l’auteur.</span><span class="sxs-lookup"><span data-stu-id="6c7d4-208">We could've just stuck with *id* and left the application to get any additional information it needed from the respective author document using the "link", but because our application displays the author's name and a thumbnail picture with every book displayed we can save a round trip to the server per book in a list by denormalizing **some** data from the author.</span></span>

<span data-ttu-id="6c7d4-209">Bien sûr, si le nom de l'auteur changeait ou qu'il souhaitait mettre à jour sa photo, nous devrions procéder à une mise à jour sur chaque livre publié par lui ; mais pour notre application, si l'on se base sur l'hypothèse que les auteurs ne changent pas de nom très souvent, il s'agit d'une décision de conception acceptable.</span><span class="sxs-lookup"><span data-stu-id="6c7d4-209">Sure, if the author's name changed or they wanted to update their photo we'd have to go an update every book they ever published but for our application, based on the assumption that authors don't change their names very often, this is an acceptable design decision.</span></span>  

<span data-ttu-id="6c7d4-210">Dans cet exemple, il existe des valeurs d’ **agrégats précalculés** pour économiser un traitement coûteux sur une opération de lecture.</span><span class="sxs-lookup"><span data-stu-id="6c7d4-210">In the example there are **pre-calculated aggregates** values to save expensive processing on a read operation.</span></span> <span data-ttu-id="6c7d4-211">Dans l'exemple, certaines données incorporées dans le document d'auteur (author) sont des données calculées au moment de l'exécution.</span><span class="sxs-lookup"><span data-stu-id="6c7d4-211">In the example, some of the data embedded in the author document is data that is calculated at run-time.</span></span> <span data-ttu-id="6c7d4-212">À chaque publication d’un nouveau livre, un document de type livre est créé **et** le champ countOfBooks est défini sur une valeur calculée en fonction du nombre de documents de type livre existant pour un auteur particulier.</span><span class="sxs-lookup"><span data-stu-id="6c7d4-212">Every time a new book is published, a book document is created **and** the countOfBooks field is set to a calculated value based on the number of book documents that exist for a particular author.</span></span> <span data-ttu-id="6c7d4-213">Cette optimisation serait appropriée dans les systèmes qui exigent de nombreuses lectures (read heavy), où nous pouvons nous permettre d'effectuer des calculs sur les écritures afin d'optimiser les lectures.</span><span class="sxs-lookup"><span data-stu-id="6c7d4-213">This optimization would be good in read heavy systems where we can afford to do computations on writes in order to optimize reads.</span></span>

<span data-ttu-id="6c7d4-214">L’existence d’un modèle avec des champs précalculés est possible, car Azure Cosmos DB prend en charge les **transactions multidocuments**.</span><span class="sxs-lookup"><span data-stu-id="6c7d4-214">The ability to have a model with pre-calculated fields is made possible because Azure Cosmos DB supports **multi-document transactions**.</span></span> <span data-ttu-id="6c7d4-215">De nombreuses boutiques NoSQL ne peuvent pas effectuer des transactions à travers plusieurs documents et plaident par conséquent en faveur de décisions de conception, telles que « incorporer tout systématiquement », en raison de cette limitation.</span><span class="sxs-lookup"><span data-stu-id="6c7d4-215">Many NoSQL stores cannot do transactions across documents and therefore advocate design decisions, such as "always embed everything", due to this limitation.</span></span> <span data-ttu-id="6c7d4-216">Avec Azure Cosmos DB, vous pouvez utiliser des déclencheurs côté serveur, ou des procédures stockées, qui insèrent des livres et mettent à jour les auteurs au sein d’une transaction ACID.</span><span class="sxs-lookup"><span data-stu-id="6c7d4-216">With Azure Cosmos DB, you can use server-side triggers, or stored procedures, that insert books and update authors all within an ACID transaction.</span></span> <span data-ttu-id="6c7d4-217">Aujourd’hui, vous n’êtes pas **tenu** d’intégrer tous les éléments dans un document, simplement pour vous assurer que vos données restent cohérentes.</span><span class="sxs-lookup"><span data-stu-id="6c7d4-217">Now you don't **have** to embed everything in to one document just to be sure that your data remains consistent.</span></span>

## <span data-ttu-id="6c7d4-218"><a name="NextSteps"></a>Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6c7d4-218"><a name="NextSteps"></a>Next steps</span></span>
<span data-ttu-id="6c7d4-219">Comprendre que la modélisation des données dans un monde sans schéma reste aussi importante que jamais, telle est la principale leçon à tirer de cet article.</span><span class="sxs-lookup"><span data-stu-id="6c7d4-219">The biggest takeaways from this article is to understand that data modeling in a schema-free world is just as important as ever.</span></span> 

<span data-ttu-id="6c7d4-220">De même qu'il existe plusieurs façons de représenter un élément de données sur un écran, il existe plusieurs manières de modéliser vos données.</span><span class="sxs-lookup"><span data-stu-id="6c7d4-220">Just as there is no single way to represent a piece of data on a screen, there is no single way to model your data.</span></span> <span data-ttu-id="6c7d4-221">Vous devez comprendre votre application et comment elle produira, utilisera et traitera les données.</span><span class="sxs-lookup"><span data-stu-id="6c7d4-221">You need to understand your application and how it will produce, consume, and process the data.</span></span> <span data-ttu-id="6c7d4-222">Ensuite, en appliquant certaines des instructions présentées ici, vous pouvez entreprendre de créer un modèle qui répond aux besoins immédiats de votre application.</span><span class="sxs-lookup"><span data-stu-id="6c7d4-222">Then, by applying some of the guidelines presented here you can set about creating a model that addresses the immediate needs of your application.</span></span> <span data-ttu-id="6c7d4-223">Lorsque vos applications doivent changer, vous pouvez exploiter la flexibilité d'une base de données sans schéma pour adopter ce changement et développer facilement votre modèle de données.</span><span class="sxs-lookup"><span data-stu-id="6c7d4-223">When your applications need to change, you can leverage the flexibility of a schema-free database to embrace that change and evolve your data model easily.</span></span> 

<span data-ttu-id="6c7d4-224">Pour en savoir plus sur Azure Cosmos DB, consultez la page de [documentation](https://azure.microsoft.com/documentation/services/cosmos-db/) du service.</span><span class="sxs-lookup"><span data-stu-id="6c7d4-224">To learn more about Azure Cosmos DB, refer to the service's [documentation](https://azure.microsoft.com/documentation/services/cosmos-db/) page.</span></span> 

<span data-ttu-id="6c7d4-225">Pour comprendre la répartition de vos données entre plusieurs partitions, consultez [Partitionnement, clés de partition et mise à l’échelle dans Azure Cosmos DB](documentdb-partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="6c7d4-225">To understand how to shard your data across multiple partitions, refer to [Partitioning Data in Azure Cosmos DB](documentdb-partition-data.md).</span></span> 
