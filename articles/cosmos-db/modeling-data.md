---
title: "données du document pour une base de données NoSQL aaaModeling | Documents Microsoft"
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
ms.openlocfilehash: 2e388c833f204287896dfa8e6f79c88073731b6b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="modeling-document-data-for-nosql-databases"></a><span data-ttu-id="d4a51-104">Modélisation de données de document pour des bases de données NoSQL</span><span class="sxs-lookup"><span data-stu-id="d4a51-104">Modeling document data for NoSQL databases</span></span>
<span data-ttu-id="d4a51-105">Alors que les bases de données sans schéma, comme base de données Azure Cosmos, facilitent super modèle de données tooembrace modifications tooyour prenez toujours certain laps de temps réfléchir à vos données.</span><span class="sxs-lookup"><span data-stu-id="d4a51-105">While schema-free databases, like Azure Cosmos DB, make it super easy tooembrace changes tooyour data model you should still spend some time thinking about your data.</span></span> 

<span data-ttu-id="d4a51-106">Comment les données se toobe stockée ?</span><span class="sxs-lookup"><span data-stu-id="d4a51-106">How is data going toobe stored?</span></span> <span data-ttu-id="d4a51-107">Comment est votre application continue tooretrieve et interroger des données ?</span><span class="sxs-lookup"><span data-stu-id="d4a51-107">How is your application going tooretrieve and query data?</span></span> <span data-ttu-id="d4a51-108">Votre application exige-t-elle de nombreuses lectures (read heavy) ou de nombreuses écritures (write heavy) ?</span><span class="sxs-lookup"><span data-stu-id="d4a51-108">Is your application read heavy, or write heavy?</span></span> 

<span data-ttu-id="d4a51-109">Après avoir lu cet article, vous serez hello en mesure de tooanswer suivant questions :</span><span class="sxs-lookup"><span data-stu-id="d4a51-109">After reading this article, you will be able tooanswer hello following questions:</span></span>

* <span data-ttu-id="d4a51-110">Comment dois-je considérer un document dans une base de données de documents ?</span><span class="sxs-lookup"><span data-stu-id="d4a51-110">How should I think about a document in a document database?</span></span>
* <span data-ttu-id="d4a51-111">Qu'est-ce que la modélisation de données et pourquoi dois-je m'en soucier ?</span><span class="sxs-lookup"><span data-stu-id="d4a51-111">What is data modeling and why should I care?</span></span> 
* <span data-ttu-id="d4a51-112">Quelle est la modélisation des données dans une base de données relationnelle tooa autre document de base de données ?</span><span class="sxs-lookup"><span data-stu-id="d4a51-112">How is modeling data in a document database different tooa relational database?</span></span>
* <span data-ttu-id="d4a51-113">Comment exprimer les relations entre les données dans une base de données non relationnelle ?</span><span class="sxs-lookup"><span data-stu-id="d4a51-113">How do I express data relationships in a non-relational database?</span></span>
* <span data-ttu-id="d4a51-114">Lorsque incorporer des données et lorsque lier des toodata ?</span><span class="sxs-lookup"><span data-stu-id="d4a51-114">When do I embed data and when do I link toodata?</span></span>

## <a name="embedding-data"></a><span data-ttu-id="d4a51-115">Incorporation de données</span><span class="sxs-lookup"><span data-stu-id="d4a51-115">Embedding data</span></span>
<span data-ttu-id="d4a51-116">Lorsque vous démarrez la modélisation des données dans un magasin de document, tels que de la base de données Azure Cosmos, essayez tootreat vos entités en tant que **documents autonomes** représenté dans JSON.</span><span class="sxs-lookup"><span data-stu-id="d4a51-116">When you start modeling data in a document store, such as Azure Cosmos DB, try tootreat your entities as **self-contained documents** represented in JSON.</span></span>

<span data-ttu-id="d4a51-117">Avant d'aller trop loin, revenons quelques étapes en arrière et examinons comment nous pouvons modéliser un élément dans une base de données relationnelle. Beaucoup d'entre nous connaissent déjà le sujet.</span><span class="sxs-lookup"><span data-stu-id="d4a51-117">Before we dive in too much further, let us take a few steps back and have a look at how we might model something in a relational database, a subject many of us are already familiar with.</span></span> <span data-ttu-id="d4a51-118">Hello suivant montre comment une personne peut être stockée dans une base de données relationnelle.</span><span class="sxs-lookup"><span data-stu-id="d4a51-118">hello following example shows how a person might be stored in a relational database.</span></span> 

![Modèle de base de données relationnelle](./media/documentdb-modeling-data/relational-data-model.png)

<span data-ttu-id="d4a51-120">Lorsque vous travaillez avec des bases de données relationnelles, pour les années toonormalize, nous avons appris normaliser, normaliser.</span><span class="sxs-lookup"><span data-stu-id="d4a51-120">When working with relational databases, we've been taught for years toonormalize, normalize, normalize.</span></span>

<span data-ttu-id="d4a51-121">En général, la normalisation de vos données implique la prise d’une entité, par exemple une personne et de décomposer en fragments toodiscrete de données.</span><span class="sxs-lookup"><span data-stu-id="d4a51-121">Normalizing your data typically involves taking an entity, such as a person, and breaking it down in toodiscrete pieces of data.</span></span> <span data-ttu-id="d4a51-122">Dans l’exemple hello ci-dessus, une personne peut avoir plusieurs enregistrements de détail de contact, ainsi que plusieurs enregistrements d’adresse.</span><span class="sxs-lookup"><span data-stu-id="d4a51-122">In hello example above, a person can have multiple contact detail records as well as multiple address records.</span></span> <span data-ttu-id="d4a51-123">Nous allons même plus loin et décomposons les coordonnées en extrayant des champs communs tels qu'un type.</span><span class="sxs-lookup"><span data-stu-id="d4a51-123">We even go one step further and break down contact details by further extracting common fields like a type.</span></span> <span data-ttu-id="d4a51-124">Même chose pour l’adresse : chaque enregistrement ici a un type, tel que *Home* ou *Business*.</span><span class="sxs-lookup"><span data-stu-id="d4a51-124">Same for address, each record here has a type like *Home* or *Business*</span></span> 

<span data-ttu-id="d4a51-125">Hello que guidage local lors de la normalisation des données est trop**éviter de stocker des données redondantes** sur chaque enregistrement et plutôt faire référence toodata.</span><span class="sxs-lookup"><span data-stu-id="d4a51-125">hello guiding premise when normalizing data is too**avoid storing redundant data** on each record and rather refer toodata.</span></span> <span data-ttu-id="d4a51-126">Dans cet exemple, tooread une personne, avec toutes leurs informations de contact et les adresses, vous devez toouse jointures tooeffectively d’agrégation vos données au moment de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="d4a51-126">In this example, tooread a person, with all their contact details and addresses, you need toouse JOINS tooeffectively aggregate your data at run time.</span></span>

    SELECT p.FirstName, p.LastName, a.City, cd.Detail
    FROM Person p
    JOIN ContactDetail cd ON cd.PersonId = p.Id
    JOIN ContactDetailType on cdt ON cdt.Id = cd.TypeId
    JOIN Address a ON a.PersonId = p.Id

<span data-ttu-id="d4a51-127">La mise à jour d'une personne avec ses coordonnées et adresses nécessite des opérations d'écriture sur plusieurs tables individuelles.</span><span class="sxs-lookup"><span data-stu-id="d4a51-127">Updating a single person with their contact details and addresses requires write operations across many individual tables.</span></span> 

<span data-ttu-id="d4a51-128">Maintenant nous allons examinez comment nous serait modèle hello même données comme une entité autonome dans une base de données du document.</span><span class="sxs-lookup"><span data-stu-id="d4a51-128">Now let's take a look at how we would model hello same data as a self-contained entity in a document database.</span></span>

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

<span data-ttu-id="d4a51-129">Approche hello ci-dessus nous disposons maintenant **dénormalisé** hello enregistrement personne où nous **incorporé** tous hello renseignements toothis personnes, tels que leurs informations de contact et les adresses, dans tooa unique Document JSON.</span><span class="sxs-lookup"><span data-stu-id="d4a51-129">Using hello approach above we have now **denormalized** hello person record where we **embedded** all hello information relating toothis person, such as their contact details and addresses, in tooa single JSON document.</span></span>
<span data-ttu-id="d4a51-130">En outre, étant donné que nous n’avons pas contraint tooa fixe de schéma que nous avons hello flexibilité toodo opérations ayant entièrement les coordonnées des formes différentes.</span><span class="sxs-lookup"><span data-stu-id="d4a51-130">In addition, because we're not confined tooa fixed schema we have hello flexibility toodo things like having contact details of different shapes entirely.</span></span> 

<span data-ttu-id="d4a51-131">La récupération d’un enregistrement de personne complète de base de données hello est maintenant une seule opération sur une collection unique et pour un seul document de lecture.</span><span class="sxs-lookup"><span data-stu-id="d4a51-131">Retrieving a complete person record from hello database is now a single read operation against a single collection and for a single document.</span></span> <span data-ttu-id="d4a51-132">La mise à jour d'un enregistrement de personne, avec ses coordonnées et adresses, correspond également à une seule opération d'écriture sur un document unique.</span><span class="sxs-lookup"><span data-stu-id="d4a51-132">Updating a person record, with their contact details and addresses, is also a single write operation against a single document.</span></span>

<span data-ttu-id="d4a51-133">À la dénormalisation des données, votre application peut avoir besoin tooissue moins les requêtes et les mises à jour toocomplete les opérations courantes.</span><span class="sxs-lookup"><span data-stu-id="d4a51-133">By denormalizing data, your application may need tooissue fewer queries and updates toocomplete common operations.</span></span> 

### <a name="when-tooembed"></a><span data-ttu-id="d4a51-134">Lorsque tooembed</span><span class="sxs-lookup"><span data-stu-id="d4a51-134">When tooembed</span></span>
<span data-ttu-id="d4a51-135">En général, utilisez des modèles de données incorporés dans les cas suivants :</span><span class="sxs-lookup"><span data-stu-id="d4a51-135">In general, use embedded data models when:</span></span>

* <span data-ttu-id="d4a51-136">Il existe des relations de type **contient** entre des entités.</span><span class="sxs-lookup"><span data-stu-id="d4a51-136">There are **contains** relationships between entities.</span></span>
* <span data-ttu-id="d4a51-137">Il existe des relations de type **un-à-plusieurs** entre des entités.</span><span class="sxs-lookup"><span data-stu-id="d4a51-137">There are **one-to-few** relationships between entities.</span></span>
* <span data-ttu-id="d4a51-138">Des données incorporées **changent rarement**.</span><span class="sxs-lookup"><span data-stu-id="d4a51-138">There is embedded data that **changes infrequently**.</span></span>
* <span data-ttu-id="d4a51-139">Des données incorporées ne croîtront pas **sans limite**.</span><span class="sxs-lookup"><span data-stu-id="d4a51-139">There is embedded data won't grow **without bound**.</span></span>
* <span data-ttu-id="d4a51-140">Il existe des données incorporées sont **intégraux** toodata dans un document.</span><span class="sxs-lookup"><span data-stu-id="d4a51-140">There is embedded data that is **integral** toodata in a document.</span></span>

> [!NOTE]
> <span data-ttu-id="d4a51-141">Normalement, les modèles de données dénormalisés offrent de meilleures performances en **lecture** .</span><span class="sxs-lookup"><span data-stu-id="d4a51-141">Typically denormalized data models provide better **read** performance.</span></span>
> 
> 

### <a name="when-not-tooembed"></a><span data-ttu-id="d4a51-142">Lorsque tooembed pas</span><span class="sxs-lookup"><span data-stu-id="d4a51-142">When not tooembed</span></span>
<span data-ttu-id="d4a51-143">Bien que hello règle empirique dans une base de données de document est toodenormalize tous les éléments et incorporer toutes les données dans un document unique de tooa, cela peut entraîner des situations toosome qui doivent être évitées.</span><span class="sxs-lookup"><span data-stu-id="d4a51-143">While hello rule of thumb in a document database is toodenormalize everything and embed all data in tooa single document, this can lead toosome situations that should be avoided.</span></span>

<span data-ttu-id="d4a51-144">Prenons cet extrait de code JSON.</span><span class="sxs-lookup"><span data-stu-id="d4a51-144">Take this JSON snippet.</span></span>

    {
        "id": "1",
        "name": "What's new in hello coolest Cloud",
        "summary": "A blog post by someone real famous",
        "comments": [
            {"id": 1, "author": "anon", "comment": "something useful, I'm sure"},
            {"id": 2, "author": "bob", "comment": "wisdom from hello interwebs"},
            …
            {"id": 100001, "author": "jane", "comment": "and on we go ..."},
            …
            {"id": 1000000001, "author": "angry", "comment": "blah angry blah angry"},
            …
            {"id": ∞ + 1, "author": "bored", "comment": "oh man, will this ever end?"},
        ]
    }

<span data-ttu-id="d4a51-145">Une entité post avec commentaires incorporés pourrait avoir cet aspect si nous étions en train de modéliser un système de blog, ou CMS, classique.</span><span class="sxs-lookup"><span data-stu-id="d4a51-145">This might be what a post entity with embedded comments would look like if we were modeling a typical blog, or CMS, system.</span></span> <span data-ttu-id="d4a51-146">problème avec cet exemple Hello est que hello tableau de commentaires est **unbounded**, c'est-à-dire qu’il n’existe aucun numéro de toohello (limite) de toute publication unique peut avoir des commentaires.</span><span class="sxs-lookup"><span data-stu-id="d4a51-146">hello problem with this example is that hello comments array is **unbounded**, meaning that there is no (practical) limit toohello number of comments any single post can have.</span></span> <span data-ttu-id="d4a51-147">Cela devient un problème comme taille hello du document de hello peut augmenter considérablement la taille.</span><span class="sxs-lookup"><span data-stu-id="d4a51-147">This will become a problem as hello size of hello document could grow significantly.</span></span>

<span data-ttu-id="d4a51-148">En tant que taille hello Hello document croît de données de salutation hello capacité tootransmit câble de hello, ainsi que la lecture et mise à jour document hello, à grande échelle, est affectée.</span><span class="sxs-lookup"><span data-stu-id="d4a51-148">As hello size of hello document grows hello ability tootransmit hello data over hello wire as well as reading and updating hello document, at scale, will be impacted.</span></span>

<span data-ttu-id="d4a51-149">Dans ce cas, il serait mieux hello tooconsider suivant le modèle.</span><span class="sxs-lookup"><span data-stu-id="d4a51-149">In this case it would be better tooconsider hello following model.</span></span>

    Post document:
    {
        "id": "1",
        "name": "What's new in hello coolest Cloud",
        "summary": "A blog post by someone real famous",
        "recentComments": [
            {"id": 1, "author": "anon", "comment": "something useful, I'm sure"},
            {"id": 2, "author": "bob", "comment": "wisdom from hello interwebs"},
            {"id": 3, "author": "jane", "comment": "....."}
        ]
    }

    Comment documents:
    {
        "postId": "1"
        "comments": [
            {"id": 4, "author": "anon", "comment": "more goodness"},
            {"id": 5, "author": "bob", "comment": "tails from hello field"},
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

<span data-ttu-id="d4a51-150">Ce modèle a commentaires les plus récents hello trois incorporées sur hello lui-même, qui est un tableau avec une limite fixe comptabiliser ce temps.</span><span class="sxs-lookup"><span data-stu-id="d4a51-150">This model has hello three most recent comments embedded on hello post itself, which is an array with a fixed bound this time.</span></span> <span data-ttu-id="d4a51-151">Hello autres commentaires sont regroupées dans toobatches de 100 commentaires et stockées dans des documents distincts.</span><span class="sxs-lookup"><span data-stu-id="d4a51-151">hello other comments are grouped in toobatches of 100 comments and stored in separate documents.</span></span> <span data-ttu-id="d4a51-152">taille de Hello du lot de hello a été choisie comme 100 autorisant notre application fictive hello des commentaires utilisateur tooload 100 à la fois.</span><span class="sxs-lookup"><span data-stu-id="d4a51-152">hello size of hello batch was chosen as 100 because our fictitious application allows hello user tooload 100 comments at a time.</span></span>  

<span data-ttu-id="d4a51-153">Un autre cas où l’incorporation de données ne sont pas une bonne idée est lorsque hello incorporées données souvent utilisées dans les documents et changent fréquemment.</span><span class="sxs-lookup"><span data-stu-id="d4a51-153">Another case where embedding data is not a good idea is when hello embedded data is used often across documents and will change frequently.</span></span> 

<span data-ttu-id="d4a51-154">Prenons cet extrait de code JSON.</span><span class="sxs-lookup"><span data-stu-id="d4a51-154">Take this JSON snippet.</span></span>

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

<span data-ttu-id="d4a51-155">Il pourrait représenter le portefeuille d'actions d'une personne.</span><span class="sxs-lookup"><span data-stu-id="d4a51-155">This could represent a person's stock portfolio.</span></span> <span data-ttu-id="d4a51-156">Nous avons choisi des informations boursières tooembed hello dans le document de portefeuille tooeach.</span><span class="sxs-lookup"><span data-stu-id="d4a51-156">We have chosen tooembed hello stock information in tooeach portfolio document.</span></span> <span data-ttu-id="d4a51-157">Dans un environnement où les données connexes changent fréquemment, comme une action commerciaux d’application, l’incorporation de données qui changent fréquemment va toomean que vous mettez constamment à jour chaque document portefeuille chaque fois qu’une action est échangée.</span><span class="sxs-lookup"><span data-stu-id="d4a51-157">In an environment where related data is changing frequently, like a stock trading application, embedding data that changes frequently is going toomean that you are constantly updating each portfolio document every time a stock is traded.</span></span>

<span data-ttu-id="d4a51-158">Des actions *zaza* peuvent être échangées des centaines de fois au cours d’une même journée, et des milliers d’utilisateurs peuvent posséder des actions *zaza* dans leur portefeuille.</span><span class="sxs-lookup"><span data-stu-id="d4a51-158">Stock *zaza* may be traded many hundreds of times in a single day and thousands of users could have *zaza* on their portfolio.</span></span> <span data-ttu-id="d4a51-159">Avec un modèle de données comme hello ci-dessus nous devrions tooupdate plusieurs milliers de documents de portefeuille plusieurs fois par jour conduisant système tooa mise à l’échelle ne sont pas très bien.</span><span class="sxs-lookup"><span data-stu-id="d4a51-159">With a data model like hello above we would have tooupdate many thousands of portfolio documents many times every day leading tooa system that won't scale very well.</span></span> 

## <span data-ttu-id="d4a51-160"><a id="Refer"></a>Référencement des données</span><span class="sxs-lookup"><span data-stu-id="d4a51-160"><a id="Refer"></a>Referencing data</span></span>
<span data-ttu-id="d4a51-161">Ainsi, l'incorporation de données fonctionne bien dans la plupart des cas, mais il est clair qu'il existe des scénarios où la dénormalisation de vos données provoque plus de problèmes qu'il n'en faudrait.</span><span class="sxs-lookup"><span data-stu-id="d4a51-161">So, embedding data works nicely for many cases but it is clear that there are scenarios when denormalizing your data will cause more problems than it is worth.</span></span> <span data-ttu-id="d4a51-162">Que faire, alors ?</span><span class="sxs-lookup"><span data-stu-id="d4a51-162">So what do we do now?</span></span> 

<span data-ttu-id="d4a51-163">Bases de données relationnelles ne sont pas hello seul emplacement où vous pouvez créer des relations entre des entités.</span><span class="sxs-lookup"><span data-stu-id="d4a51-163">Relational databases are not hello only place where you can create relationships between entities.</span></span> <span data-ttu-id="d4a51-164">Dans une base de données de document, vous pouvez avoir des informations dans un document qui est effectivement lié toodata dans d’autres documents.</span><span class="sxs-lookup"><span data-stu-id="d4a51-164">In a document database you can have information in one document that actually relates toodata in other documents.</span></span> <span data-ttu-id="d4a51-165">Maintenant, je suis préconisent pas pendant une minute même que les systèmes qui seraient mieux adaptés tooa base de données relationnelle dans une base de données Azure Cosmos ou toute autre base de données de document, mais que des relations simples conviennent et peuvent être très utiles.</span><span class="sxs-lookup"><span data-stu-id="d4a51-165">Now, I am not advocating for even one minute that we build systems that would be better suited tooa relational database in Azure Cosmos DB, or any other document database, but simple relationships are fine and can be very useful.</span></span> 

<span data-ttu-id="d4a51-166">Bonjour JSON ci-dessous, nous avons choisi toouse hello exemple d’un portefeuille de précédemment, mais cette fois, que nous nous référons toohello stock élément portefeuille hello au lieu d’incorporer il.</span><span class="sxs-lookup"><span data-stu-id="d4a51-166">In hello JSON below we chose toouse hello example of a stock portfolio from earlier but this time we refer toohello stock item on hello portfolio instead of embedding it.</span></span> <span data-ttu-id="d4a51-167">Ainsi, quand hello stock élément change fréquemment hello jour hello uniquement document nécessitant toobe mis à jour est stock monodocument hello.</span><span class="sxs-lookup"><span data-stu-id="d4a51-167">This way, when hello stock item changes frequently throughout hello day hello only document that needs toobe updated is hello single stock document.</span></span> 

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


<span data-ttu-id="d4a51-168">Une approche de toothis inconvénient immédiate est bien que si votre application est requis tooshow plus d’informations sur chaque action qui a lieu lors de l’affichage du portefeuille d’une personne ; Dans ce cas vous devez toomake plusieurs allers-retours toohello de base de données tooload hello plus d’informations pour chaque document de stock.</span><span class="sxs-lookup"><span data-stu-id="d4a51-168">An immediate downside toothis approach though is if your application is required tooshow information about each stock that is held when displaying a person's portfolio; in this case you would need toomake multiple trips toohello database tooload hello information for each stock document.</span></span> <span data-ttu-id="d4a51-169">Ici, nous avons apporté une efficacité de hello tooimprove la décision d’opérations d’écriture, ce qui se produire fréquemment au cours de la journée de hello, mais à son tour compromis sur hello d’opérations de lecture qui susceptibles d’avoir moins d’impact sur les performances de hello de ce système.</span><span class="sxs-lookup"><span data-stu-id="d4a51-169">Here we've made a decision tooimprove hello efficiency of write operations, which happen frequently throughout hello day, but in turn compromised on hello read operations that potentially have less impact on hello performance of this particular system.</span></span>

> [!NOTE]
> <span data-ttu-id="d4a51-170">Normalisation des modèles de données **peut nécessiter plusieurs allers-retours** toohello server.</span><span class="sxs-lookup"><span data-stu-id="d4a51-170">Normalized data models **can require more round trips** toohello server.</span></span>
> 
> 

### <a name="what-about-foreign-keys"></a><span data-ttu-id="d4a51-171">Qu'en est-il des clés étrangères ?</span><span class="sxs-lookup"><span data-stu-id="d4a51-171">What about foreign keys?</span></span>
<span data-ttu-id="d4a51-172">Car il n’existe actuellement aucun concept d’une contrainte, clé étrangère ou dans le cas contraire, toutes les relations entre documents que vous avez dans les documents sont effectivement « faibles » et la ne seront pas vérifiées par base de données hello lui-même.</span><span class="sxs-lookup"><span data-stu-id="d4a51-172">Because there is currently no concept of a constraint, foreign-key or otherwise, any inter-document relationships that you have in documents are effectively "weak links" and will not be verified by hello database itself.</span></span> <span data-ttu-id="d4a51-173">Si vous souhaitez tooensure qui hello des données de qu'un document fait référence tooactually existe, puis vous en avez besoin toodo dans votre application, ou via l’utilisation de hello de déclencheurs côté serveur ou des procédures stockées sur la base de données Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="d4a51-173">If you want tooensure that hello data a document is referring tooactually exists, then you need toodo this in your application, or through hello use of server-side triggers or stored procedures on Azure Cosmos DB.</span></span>

### <a name="when-tooreference"></a><span data-ttu-id="d4a51-174">Lorsque tooreference</span><span class="sxs-lookup"><span data-stu-id="d4a51-174">When tooreference</span></span>
<span data-ttu-id="d4a51-175">En général, utilisez des modèles de données normalisés dans les cas suivants :</span><span class="sxs-lookup"><span data-stu-id="d4a51-175">In general, use normalized data models when:</span></span>

* <span data-ttu-id="d4a51-176">Représentation des relations **un-à-plusieurs** .</span><span class="sxs-lookup"><span data-stu-id="d4a51-176">Representing **one-to-many** relationships.</span></span>
* <span data-ttu-id="d4a51-177">Représentation des relations **plusieurs-à-plusieurs** .</span><span class="sxs-lookup"><span data-stu-id="d4a51-177">Representing **many-to-many** relationships.</span></span>
* <span data-ttu-id="d4a51-178">Les données associées **changent fréquemment**.</span><span class="sxs-lookup"><span data-stu-id="d4a51-178">Related data **changes frequently**.</span></span>
* <span data-ttu-id="d4a51-179">Les données référencées peuvent être **illimitées**.</span><span class="sxs-lookup"><span data-stu-id="d4a51-179">Referenced data could be **unbounded**.</span></span>

> [!NOTE]
> <span data-ttu-id="d4a51-180">En général, la normalisation offre de meilleures performances en **écriture** .</span><span class="sxs-lookup"><span data-stu-id="d4a51-180">Typically normalizing provides better **write** performance.</span></span>
> 
> 

### <a name="where-do-i-put-hello-relationship"></a><span data-ttu-id="d4a51-181">Où placer la relation de hello ?</span><span class="sxs-lookup"><span data-stu-id="d4a51-181">Where do I put hello relationship?</span></span>
<span data-ttu-id="d4a51-182">croissance Hello de relation de hello pour déterminer dans quel document toostore hello de référence.</span><span class="sxs-lookup"><span data-stu-id="d4a51-182">hello growth of hello relationship will help determine in which document toostore hello reference.</span></span>

<span data-ttu-id="d4a51-183">Si nous examinons hello JSON ci-dessous qui modélise les serveurs de publication et de la documentation.</span><span class="sxs-lookup"><span data-stu-id="d4a51-183">If we look at hello JSON below that models publishers and books.</span></span>

    Publisher document:
    {
        "id": "mspress",
        "name": "Microsoft Press",
        "books": [ 1, 2, 3, ..., 100, ..., 1000]
    }

    Book documents:
    {"id": "1", "name": "Azure Cosmos DB 101" }
    {"id": "2", "name": "Azure Cosmos DB for RDBMS Users" }
    {"id": "3", "name": "Taking over hello world one JSON doc at a time" }
    ...
    {"id": "100", "name": "Learn about Azure Cosmos DB" }
    ...
    {"id": "1000", "name": "Deep Dive in tooAzure Cosmos DB" }

<span data-ttu-id="d4a51-184">Si le nombre de hello de livres hello par le serveur de publication est réduit avec une croissance limitée, puis le stockage référence book hello hello publisher document peut être utile.</span><span class="sxs-lookup"><span data-stu-id="d4a51-184">If hello number of hello books per publisher is small with limited growth, then storing hello book reference inside hello publisher document may be useful.</span></span> <span data-ttu-id="d4a51-185">Toutefois, si le nombre hello de livres par le serveur de publication est illimitée, ce modèle de données pourrait entraîner toomutable, augmente de tableaux, comme dans les documents de serveur de publication hello exemple ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="d4a51-185">However, if hello number of books per publisher is unbounded, then this data model would lead toomutable, growing arrays, as in hello example publisher document above.</span></span> 

<span data-ttu-id="d4a51-186">Choses un peu de commutation serait le résultat dans un modèle que représente toujours hello mais désormais les mêmes données évite ces grandes collections mutables.</span><span class="sxs-lookup"><span data-stu-id="d4a51-186">Switching things around a bit would result in a model that still represents hello same data but now avoids these large mutable collections.</span></span>

    Publisher document: 
    {
        "id": "mspress",
        "name": "Microsoft Press"
    }

    Book documents: 
    {"id": "1","name": "Azure Cosmos DB 101", "pub-id": "mspress"}
    {"id": "2","name": "Azure Cosmos DB for RDBMS Users", "pub-id": "mspress"}
    {"id": "3","name": "Taking over hello world one JSON doc at a time"}
    ...
    {"id": "100","name": "Learn about Azure Cosmos DB", "pub-id": "mspress"}
    ...
    {"id": "1000","name": "Deep Dive in tooAzure Cosmos DB", "pub-id": "mspress"}

<span data-ttu-id="d4a51-187">Bonjour exemple ci-dessus, nous avons supprimé hello unbounded collection sur le document du serveur de publication hello.</span><span class="sxs-lookup"><span data-stu-id="d4a51-187">In hello above example, we have dropped hello unbounded collection on hello publisher document.</span></span> <span data-ttu-id="d4a51-188">Au lieu de cela que nous avons simplement un un serveur de publication de toohello de référence sur chaque document de livre.</span><span class="sxs-lookup"><span data-stu-id="d4a51-188">Instead we just have a a reference toohello publisher on each book document.</span></span>

### <a name="how-do-i-model-manymany-relationships"></a><span data-ttu-id="d4a51-189">Comment modéliser des relations plusieurs-à-plusieurs ?</span><span class="sxs-lookup"><span data-stu-id="d4a51-189">How do I model many:many relationships?</span></span>
<span data-ttu-id="d4a51-190">Dans une base de données relationnelle *plusieurs-à-plusieurs* , les relations sont souvent modélisées avec des tables de jointure qui relient simplement les enregistrements d’autres tables.</span><span class="sxs-lookup"><span data-stu-id="d4a51-190">In a relational database *many:many* relationships are often modeled with join tables, which just join records from other tables together.</span></span> 

![Tables de jointures](./media/documentdb-modeling-data/join-table.png)

<span data-ttu-id="d4a51-192">Vous pouvez être tenté tooreplicate hello même chose à l’aide de documents et de produire un modèle de données qui semble similaire toohello suivant.</span><span class="sxs-lookup"><span data-stu-id="d4a51-192">You might be tempted tooreplicate hello same thing using documents and produce a data model that looks similar toohello following.</span></span>

    Author documents: 
    {"id": "a1", "name": "Thomas Andersen" }
    {"id": "a2", "name": "William Wakefield" }

    Book documents:
    {"id": "b1", "name": "Azure Cosmos DB 101" }
    {"id": "b2", "name": "Azure Cosmos DB for RDBMS Users" }
    {"id": "b3", "name": "Taking over hello world one JSON doc at a time" }
    {"id": "b4", "name": "Learn about Azure Cosmos DB" }
    {"id": "b5", "name": "Deep Dive in tooAzure Cosmos DB" }

    Joining documents: 
    {"authorId": "a1", "bookId": "b1" }
    {"authorId": "a2", "bookId": "b1" }
    {"authorId": "a1", "bookId": "b2" }
    {"authorId": "a1", "bookId": "b3" }

<span data-ttu-id="d4a51-193">Cette méthode fonctionne.</span><span class="sxs-lookup"><span data-stu-id="d4a51-193">This would work.</span></span> <span data-ttu-id="d4a51-194">Toutefois, le chargement soit un auteur avec leurs livres ou le chargement d’un livre avec son auteur, toujours nécessite au moins deux requêtes supplémentaires par rapport à la base de données hello.</span><span class="sxs-lookup"><span data-stu-id="d4a51-194">However, loading either an author with their books, or loading a book with its author, would always require at least two additional queries against hello database.</span></span> <span data-ttu-id="d4a51-195">Une seule requête toohello de jointure de document et un autre toofetch hello réel document de requête jointe.</span><span class="sxs-lookup"><span data-stu-id="d4a51-195">One query toohello joining document and then another query toofetch hello actual document being joined.</span></span> 

<span data-ttu-id="d4a51-196">Si cette table de jointure ne fait rien d'autre que coller ensemble deux éléments de données, pourquoi ne pas la supprimer complètement ?</span><span class="sxs-lookup"><span data-stu-id="d4a51-196">If all this join table is doing is gluing together two pieces of data, then why not drop it completely?</span></span>
<span data-ttu-id="d4a51-197">Considérez les éléments suivants de hello.</span><span class="sxs-lookup"><span data-stu-id="d4a51-197">Consider hello following.</span></span>

    Author documents:
    {"id": "a1", "name": "Thomas Andersen", "books": ["b1, "b2", "b3"]}
    {"id": "a2", "name": "William Wakefield", "books": ["b1", "b4"]}

    Book documents: 
    {"id": "b1", "name": "Azure Cosmos DB 101", "authors": ["a1", "a2"]}
    {"id": "b2", "name": "Azure Cosmos DB for RDBMS Users", "authors": ["a1"]}
    {"id": "b3", "name": "Learn about Azure Cosmos DB", "authors": ["a1"]}
    {"id": "b4", "name": "Deep Dive in tooAzure Cosmos DB", "authors": ["a2"]}

<span data-ttu-id="d4a51-198">Maintenant, si j’avais un auteur, immédiatement savoir quels sont les livres qu’ils ont écrits, et inversement si j’avais un document de livre chargé serait savoir ID hello de hello auteurs.</span><span class="sxs-lookup"><span data-stu-id="d4a51-198">Now, if I had an author, I immediately know which books they have written, and conversely if I had a book document loaded I would know hello ids of hello author(s).</span></span> <span data-ttu-id="d4a51-199">Ceci permet d’enregistrer cette requête intermédiaire par rapport à la table de jointure hello en réduisant le nombre hello du serveur de votre application a toomake des allers-retours.</span><span class="sxs-lookup"><span data-stu-id="d4a51-199">This saves that intermediary query against hello join table reducing hello number of server round trips your application has toomake.</span></span> 

## <span data-ttu-id="d4a51-200"><a id="WrapUp"></a>Modèles de données hybrides</span><span class="sxs-lookup"><span data-stu-id="d4a51-200"><a id="WrapUp"></a>Hybrid data models</span></span>
<span data-ttu-id="d4a51-201">Nous savons maintenant que l'incorporation (ou la dénormalisation) et le référencement (ou la normalisation) des données ont tous deux leurs avantages, mais qu'ils impliquent également des compromis.</span><span class="sxs-lookup"><span data-stu-id="d4a51-201">We've now looked embedding (or denormalizing) and referencing (or normalizing) data, each have their upsides and each have compromises as we have seen.</span></span> 

<span data-ttu-id="d4a51-202">Il ne toujours avoir toobe ou, ne pas être toomix vous en faites d’un peu.</span><span class="sxs-lookup"><span data-stu-id="d4a51-202">It doesn't always have toobe either or, don't be scared toomix things up a little.</span></span> 

<span data-ttu-id="d4a51-203">En fonction des habitudes d’utilisation de votre application et les charges de travail il peut y avoir des cas où la combinaison incorporé et données référencés de sens et pourrait logique d’application responsable toosimpler avec moins de boucles tout en conservant un bon niveau de performances .</span><span class="sxs-lookup"><span data-stu-id="d4a51-203">Based on your application's specific usage patterns and workloads there may be cases where mixing embedded and referenced data makes sense and could lead toosimpler application logic with fewer server round trips while still maintaining a good level of performance.</span></span>

<span data-ttu-id="d4a51-204">Envisagez de hello suivant JSON.</span><span class="sxs-lookup"><span data-stu-id="d4a51-204">Consider hello following JSON.</span></span> 

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

<span data-ttu-id="d4a51-205">Ici nous avons suivi (principalement) de modèle incorporés hello, où les données à partir d’autres entités sont incorporées dans les documents de niveau supérieur de hello, mais les autres données sont référencées.</span><span class="sxs-lookup"><span data-stu-id="d4a51-205">Here we've (mostly) followed hello embedded model, where data from other entities are embedded in hello top-level document, but other data is referenced.</span></span> 

<span data-ttu-id="d4a51-206">Si vous examinez le document de livre hello, nous pouvons voir quelques exemples intéressants de champs lorsque nous observons la tableau hello des auteurs.</span><span class="sxs-lookup"><span data-stu-id="d4a51-206">If you look at hello book document, we can see a few interesting fields when we look at hello array of authors.</span></span> <span data-ttu-id="d4a51-207">Il existe un *id* champ qui est le champ hello que nous utilisons également document d’auteur toorefer tooan précédent, une pratique courante dans un modèle normalisé mais nous avoir *nom* et *thumbnailUrl*.</span><span class="sxs-lookup"><span data-stu-id="d4a51-207">There is an *id* field which is hello field we use toorefer back tooan author document, standard practice in a normalized model, but then we also have *name* and *thumbnailUrl*.</span></span> <span data-ttu-id="d4a51-208">Nous avons simplement avez bloquée avec *id* et a laissé hello application tooget des informations supplémentaires, il est nécessaire à partir du document d’auteur respectifs hello à l’aide de hello « liaison », mais étant donné que notre application affiche le nom de l’auteur hello et un image miniature avec chaque livre nous pouvons enregistrer un serveur de toohello aller-retour par livre dans une liste par dénormalisation **certains** données de l’auteur de hello.</span><span class="sxs-lookup"><span data-stu-id="d4a51-208">We could've just stuck with *id* and left hello application tooget any additional information it needed from hello respective author document using hello "link", but because our application displays hello author's name and a thumbnail picture with every book displayed we can save a round trip toohello server per book in a list by denormalizing **some** data from hello author.</span></span>

<span data-ttu-id="d4a51-209">Bien sûr, si hello auteur modifié ou qu’ils voulaient tooupdate leur photo nous devrions toogo une mise à jour chaque livre ils jamais publié, mais pour notre application, en fonction de l’hypothèse hello que les auteurs ne changent pas leurs noms très souvent, il s’agit d’une conception acceptable décision.</span><span class="sxs-lookup"><span data-stu-id="d4a51-209">Sure, if hello author's name changed or they wanted tooupdate their photo we'd have toogo an update every book they ever published but for our application, based on hello assumption that authors don't change their names very often, this is an acceptable design decision.</span></span>  

<span data-ttu-id="d4a51-210">Dans l’exemple de hello **précalculée agrégats** valeurs toosave coûteux de traitement sur une opération de lecture.</span><span class="sxs-lookup"><span data-stu-id="d4a51-210">In hello example there are **pre-calculated aggregates** values toosave expensive processing on a read operation.</span></span> <span data-ttu-id="d4a51-211">Dans l’exemple de hello, certaines données hello incorporées dans un document d’auteur hello donnée est calculée au moment de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="d4a51-211">In hello example, some of hello data embedded in hello author document is data that is calculated at run-time.</span></span> <span data-ttu-id="d4a51-212">Chaque fois qu’un nouveau livre est publié, création d’un document de livre **et** hello countOfBooks champ a la valeur valeur tooa calculé en fonction du nombre de hello de documents d’un livre qui existent pour un auteur particulier.</span><span class="sxs-lookup"><span data-stu-id="d4a51-212">Every time a new book is published, a book document is created **and** hello countOfBooks field is set tooa calculated value based on hello number of book documents that exist for a particular author.</span></span> <span data-ttu-id="d4a51-213">Cette optimisation serait correcte dans les systèmes lourde lecture où nous pouvons nous permettre de toodo des calculs sur les écritures dans l’ordre toooptimize lectures.</span><span class="sxs-lookup"><span data-stu-id="d4a51-213">This optimization would be good in read heavy systems where we can afford toodo computations on writes in order toooptimize reads.</span></span>

<span data-ttu-id="d4a51-214">Hello toohave possibilité un modèle avec des champs calculés préalable est possible parce que prend en charge de la base de données Azure Cosmos **documents plusieurs transactions**.</span><span class="sxs-lookup"><span data-stu-id="d4a51-214">hello ability toohave a model with pre-calculated fields is made possible because Azure Cosmos DB supports **multi-document transactions**.</span></span> <span data-ttu-id="d4a51-215">Nombreux magasins NoSQL ne peut pas effectuer des transactions dans les documents et par conséquent préconisent les décisions de conception, telles que « toujours incorporer tout », en raison de la limitation de toothis.</span><span class="sxs-lookup"><span data-stu-id="d4a51-215">Many NoSQL stores cannot do transactions across documents and therefore advocate design decisions, such as "always embed everything", due toothis limitation.</span></span> <span data-ttu-id="d4a51-216">Avec Azure Cosmos DB, vous pouvez utiliser des déclencheurs côté serveur, ou des procédures stockées, qui insèrent des livres et mettent à jour les auteurs au sein d’une transaction ACID.</span><span class="sxs-lookup"><span data-stu-id="d4a51-216">With Azure Cosmos DB, you can use server-side triggers, or stored procedures, that insert books and update authors all within an ACID transaction.</span></span> <span data-ttu-id="d4a51-217">Maintenant vous n’avez pas **ont** tooembed de tous les éléments de tooone document simplement toobe sûr que vos données restent cohérentes.</span><span class="sxs-lookup"><span data-stu-id="d4a51-217">Now you don't **have** tooembed everything in tooone document just toobe sure that your data remains consistent.</span></span>

## <span data-ttu-id="d4a51-218"><a name="NextSteps"></a>Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d4a51-218"><a name="NextSteps"></a>Next steps</span></span>
<span data-ttu-id="d4a51-219">principaux éléments importants à retenir de Hello à partir de cet article est toounderstand que la modélisation des données dans un monde de schéma sont tout aussi importantes que jamais.</span><span class="sxs-lookup"><span data-stu-id="d4a51-219">hello biggest takeaways from this article is toounderstand that data modeling in a schema-free world is just as important as ever.</span></span> 

<span data-ttu-id="d4a51-220">Comme il n’existe aucun toorepresent de façon unique un élément de données sur un écran, il n’est aucun moyen simple de toomodel vos données.</span><span class="sxs-lookup"><span data-stu-id="d4a51-220">Just as there is no single way toorepresent a piece of data on a screen, there is no single way toomodel your data.</span></span> <span data-ttu-id="d4a51-221">Vous devez toounderstand votre application et comment il génère, utiliser et traiter les données hello.</span><span class="sxs-lookup"><span data-stu-id="d4a51-221">You need toounderstand your application and how it will produce, consume, and process hello data.</span></span> <span data-ttu-id="d4a51-222">Puis, en appliquant des hello les instructions présentées ici, vous peuvent définir sur la création d’un modèle qui répond aux besoins immédiats hello de votre application.</span><span class="sxs-lookup"><span data-stu-id="d4a51-222">Then, by applying some of hello guidelines presented here you can set about creating a model that addresses hello immediate needs of your application.</span></span> <span data-ttu-id="d4a51-223">Lorsque vos applications ont besoin de toochange, vous pouvez tirer parti flexibilité hello d’un tooembrace du schéma de base de données qui changent et évoluer facilement de votre modèle de données.</span><span class="sxs-lookup"><span data-stu-id="d4a51-223">When your applications need toochange, you can leverage hello flexibility of a schema-free database tooembrace that change and evolve your data model easily.</span></span> 

<span data-ttu-id="d4a51-224">toolearn savoir plus sur la base de données Azure Cosmos, référence du service toohello [documentation](https://azure.microsoft.com/documentation/services/cosmos-db/) page.</span><span class="sxs-lookup"><span data-stu-id="d4a51-224">toolearn more about Azure Cosmos DB, refer toohello service's [documentation](https://azure.microsoft.com/documentation/services/cosmos-db/) page.</span></span> 

<span data-ttu-id="d4a51-225">toounderstand comment tooshard vos données sur plusieurs partitions, référence trop[le partitionnement des données dans la base de données Azure Cosmos](documentdb-partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="d4a51-225">toounderstand how tooshard your data across multiple partitions, refer too[Partitioning Data in Azure Cosmos DB](documentdb-partition-data.md).</span></span> 
