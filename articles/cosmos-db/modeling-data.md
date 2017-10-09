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
# <a name="modeling-document-data-for-nosql-databases"></a>Modélisation de données de document pour des bases de données NoSQL
Alors que les bases de données sans schéma, comme base de données Azure Cosmos, facilitent super modèle de données tooembrace modifications tooyour prenez toujours certain laps de temps réfléchir à vos données. 

Comment les données se toobe stockée ? Comment est votre application continue tooretrieve et interroger des données ? Votre application exige-t-elle de nombreuses lectures (read heavy) ou de nombreuses écritures (write heavy) ? 

Après avoir lu cet article, vous serez hello en mesure de tooanswer suivant questions :

* Comment dois-je considérer un document dans une base de données de documents ?
* Qu'est-ce que la modélisation de données et pourquoi dois-je m'en soucier ? 
* Quelle est la modélisation des données dans une base de données relationnelle tooa autre document de base de données ?
* Comment exprimer les relations entre les données dans une base de données non relationnelle ?
* Lorsque incorporer des données et lorsque lier des toodata ?

## <a name="embedding-data"></a>Incorporation de données
Lorsque vous démarrez la modélisation des données dans un magasin de document, tels que de la base de données Azure Cosmos, essayez tootreat vos entités en tant que **documents autonomes** représenté dans JSON.

Avant d'aller trop loin, revenons quelques étapes en arrière et examinons comment nous pouvons modéliser un élément dans une base de données relationnelle. Beaucoup d'entre nous connaissent déjà le sujet. Hello suivant montre comment une personne peut être stockée dans une base de données relationnelle. 

![Modèle de base de données relationnelle](./media/documentdb-modeling-data/relational-data-model.png)

Lorsque vous travaillez avec des bases de données relationnelles, pour les années toonormalize, nous avons appris normaliser, normaliser.

En général, la normalisation de vos données implique la prise d’une entité, par exemple une personne et de décomposer en fragments toodiscrete de données. Dans l’exemple hello ci-dessus, une personne peut avoir plusieurs enregistrements de détail de contact, ainsi que plusieurs enregistrements d’adresse. Nous allons même plus loin et décomposons les coordonnées en extrayant des champs communs tels qu'un type. Même chose pour l’adresse : chaque enregistrement ici a un type, tel que *Home* ou *Business*. 

Hello que guidage local lors de la normalisation des données est trop**éviter de stocker des données redondantes** sur chaque enregistrement et plutôt faire référence toodata. Dans cet exemple, tooread une personne, avec toutes leurs informations de contact et les adresses, vous devez toouse jointures tooeffectively d’agrégation vos données au moment de l’exécution.

    SELECT p.FirstName, p.LastName, a.City, cd.Detail
    FROM Person p
    JOIN ContactDetail cd ON cd.PersonId = p.Id
    JOIN ContactDetailType on cdt ON cdt.Id = cd.TypeId
    JOIN Address a ON a.PersonId = p.Id

La mise à jour d'une personne avec ses coordonnées et adresses nécessite des opérations d'écriture sur plusieurs tables individuelles. 

Maintenant nous allons examinez comment nous serait modèle hello même données comme une entité autonome dans une base de données du document.

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

Approche hello ci-dessus nous disposons maintenant **dénormalisé** hello enregistrement personne où nous **incorporé** tous hello renseignements toothis personnes, tels que leurs informations de contact et les adresses, dans tooa unique Document JSON.
En outre, étant donné que nous n’avons pas contraint tooa fixe de schéma que nous avons hello flexibilité toodo opérations ayant entièrement les coordonnées des formes différentes. 

La récupération d’un enregistrement de personne complète de base de données hello est maintenant une seule opération sur une collection unique et pour un seul document de lecture. La mise à jour d'un enregistrement de personne, avec ses coordonnées et adresses, correspond également à une seule opération d'écriture sur un document unique.

À la dénormalisation des données, votre application peut avoir besoin tooissue moins les requêtes et les mises à jour toocomplete les opérations courantes. 

### <a name="when-tooembed"></a>Lorsque tooembed
En général, utilisez des modèles de données incorporés dans les cas suivants :

* Il existe des relations de type **contient** entre des entités.
* Il existe des relations de type **un-à-plusieurs** entre des entités.
* Des données incorporées **changent rarement**.
* Des données incorporées ne croîtront pas **sans limite**.
* Il existe des données incorporées sont **intégraux** toodata dans un document.

> [!NOTE]
> Normalement, les modèles de données dénormalisés offrent de meilleures performances en **lecture** .
> 
> 

### <a name="when-not-tooembed"></a>Lorsque tooembed pas
Bien que hello règle empirique dans une base de données de document est toodenormalize tous les éléments et incorporer toutes les données dans un document unique de tooa, cela peut entraîner des situations toosome qui doivent être évitées.

Prenons cet extrait de code JSON.

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

Une entité post avec commentaires incorporés pourrait avoir cet aspect si nous étions en train de modéliser un système de blog, ou CMS, classique. problème avec cet exemple Hello est que hello tableau de commentaires est **unbounded**, c'est-à-dire qu’il n’existe aucun numéro de toohello (limite) de toute publication unique peut avoir des commentaires. Cela devient un problème comme taille hello du document de hello peut augmenter considérablement la taille.

En tant que taille hello Hello document croît de données de salutation hello capacité tootransmit câble de hello, ainsi que la lecture et mise à jour document hello, à grande échelle, est affectée.

Dans ce cas, il serait mieux hello tooconsider suivant le modèle.

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

Ce modèle a commentaires les plus récents hello trois incorporées sur hello lui-même, qui est un tableau avec une limite fixe comptabiliser ce temps. Hello autres commentaires sont regroupées dans toobatches de 100 commentaires et stockées dans des documents distincts. taille de Hello du lot de hello a été choisie comme 100 autorisant notre application fictive hello des commentaires utilisateur tooload 100 à la fois.  

Un autre cas où l’incorporation de données ne sont pas une bonne idée est lorsque hello incorporées données souvent utilisées dans les documents et changent fréquemment. 

Prenons cet extrait de code JSON.

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

Il pourrait représenter le portefeuille d'actions d'une personne. Nous avons choisi des informations boursières tooembed hello dans le document de portefeuille tooeach. Dans un environnement où les données connexes changent fréquemment, comme une action commerciaux d’application, l’incorporation de données qui changent fréquemment va toomean que vous mettez constamment à jour chaque document portefeuille chaque fois qu’une action est échangée.

Des actions *zaza* peuvent être échangées des centaines de fois au cours d’une même journée, et des milliers d’utilisateurs peuvent posséder des actions *zaza* dans leur portefeuille. Avec un modèle de données comme hello ci-dessus nous devrions tooupdate plusieurs milliers de documents de portefeuille plusieurs fois par jour conduisant système tooa mise à l’échelle ne sont pas très bien. 

## <a id="Refer"></a>Référencement des données
Ainsi, l'incorporation de données fonctionne bien dans la plupart des cas, mais il est clair qu'il existe des scénarios où la dénormalisation de vos données provoque plus de problèmes qu'il n'en faudrait. Que faire, alors ? 

Bases de données relationnelles ne sont pas hello seul emplacement où vous pouvez créer des relations entre des entités. Dans une base de données de document, vous pouvez avoir des informations dans un document qui est effectivement lié toodata dans d’autres documents. Maintenant, je suis préconisent pas pendant une minute même que les systèmes qui seraient mieux adaptés tooa base de données relationnelle dans une base de données Azure Cosmos ou toute autre base de données de document, mais que des relations simples conviennent et peuvent être très utiles. 

Bonjour JSON ci-dessous, nous avons choisi toouse hello exemple d’un portefeuille de précédemment, mais cette fois, que nous nous référons toohello stock élément portefeuille hello au lieu d’incorporer il. Ainsi, quand hello stock élément change fréquemment hello jour hello uniquement document nécessitant toobe mis à jour est stock monodocument hello. 

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


Une approche de toothis inconvénient immédiate est bien que si votre application est requis tooshow plus d’informations sur chaque action qui a lieu lors de l’affichage du portefeuille d’une personne ; Dans ce cas vous devez toomake plusieurs allers-retours toohello de base de données tooload hello plus d’informations pour chaque document de stock. Ici, nous avons apporté une efficacité de hello tooimprove la décision d’opérations d’écriture, ce qui se produire fréquemment au cours de la journée de hello, mais à son tour compromis sur hello d’opérations de lecture qui susceptibles d’avoir moins d’impact sur les performances de hello de ce système.

> [!NOTE]
> Normalisation des modèles de données **peut nécessiter plusieurs allers-retours** toohello server.
> 
> 

### <a name="what-about-foreign-keys"></a>Qu'en est-il des clés étrangères ?
Car il n’existe actuellement aucun concept d’une contrainte, clé étrangère ou dans le cas contraire, toutes les relations entre documents que vous avez dans les documents sont effectivement « faibles » et la ne seront pas vérifiées par base de données hello lui-même. Si vous souhaitez tooensure qui hello des données de qu'un document fait référence tooactually existe, puis vous en avez besoin toodo dans votre application, ou via l’utilisation de hello de déclencheurs côté serveur ou des procédures stockées sur la base de données Azure Cosmos.

### <a name="when-tooreference"></a>Lorsque tooreference
En général, utilisez des modèles de données normalisés dans les cas suivants :

* Représentation des relations **un-à-plusieurs** .
* Représentation des relations **plusieurs-à-plusieurs** .
* Les données associées **changent fréquemment**.
* Les données référencées peuvent être **illimitées**.

> [!NOTE]
> En général, la normalisation offre de meilleures performances en **écriture** .
> 
> 

### <a name="where-do-i-put-hello-relationship"></a>Où placer la relation de hello ?
croissance Hello de relation de hello pour déterminer dans quel document toostore hello de référence.

Si nous examinons hello JSON ci-dessous qui modélise les serveurs de publication et de la documentation.

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

Si le nombre de hello de livres hello par le serveur de publication est réduit avec une croissance limitée, puis le stockage référence book hello hello publisher document peut être utile. Toutefois, si le nombre hello de livres par le serveur de publication est illimitée, ce modèle de données pourrait entraîner toomutable, augmente de tableaux, comme dans les documents de serveur de publication hello exemple ci-dessus. 

Choses un peu de commutation serait le résultat dans un modèle que représente toujours hello mais désormais les mêmes données évite ces grandes collections mutables.

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

Bonjour exemple ci-dessus, nous avons supprimé hello unbounded collection sur le document du serveur de publication hello. Au lieu de cela que nous avons simplement un un serveur de publication de toohello de référence sur chaque document de livre.

### <a name="how-do-i-model-manymany-relationships"></a>Comment modéliser des relations plusieurs-à-plusieurs ?
Dans une base de données relationnelle *plusieurs-à-plusieurs* , les relations sont souvent modélisées avec des tables de jointure qui relient simplement les enregistrements d’autres tables. 

![Tables de jointures](./media/documentdb-modeling-data/join-table.png)

Vous pouvez être tenté tooreplicate hello même chose à l’aide de documents et de produire un modèle de données qui semble similaire toohello suivant.

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

Cette méthode fonctionne. Toutefois, le chargement soit un auteur avec leurs livres ou le chargement d’un livre avec son auteur, toujours nécessite au moins deux requêtes supplémentaires par rapport à la base de données hello. Une seule requête toohello de jointure de document et un autre toofetch hello réel document de requête jointe. 

Si cette table de jointure ne fait rien d'autre que coller ensemble deux éléments de données, pourquoi ne pas la supprimer complètement ?
Considérez les éléments suivants de hello.

    Author documents:
    {"id": "a1", "name": "Thomas Andersen", "books": ["b1, "b2", "b3"]}
    {"id": "a2", "name": "William Wakefield", "books": ["b1", "b4"]}

    Book documents: 
    {"id": "b1", "name": "Azure Cosmos DB 101", "authors": ["a1", "a2"]}
    {"id": "b2", "name": "Azure Cosmos DB for RDBMS Users", "authors": ["a1"]}
    {"id": "b3", "name": "Learn about Azure Cosmos DB", "authors": ["a1"]}
    {"id": "b4", "name": "Deep Dive in tooAzure Cosmos DB", "authors": ["a2"]}

Maintenant, si j’avais un auteur, immédiatement savoir quels sont les livres qu’ils ont écrits, et inversement si j’avais un document de livre chargé serait savoir ID hello de hello auteurs. Ceci permet d’enregistrer cette requête intermédiaire par rapport à la table de jointure hello en réduisant le nombre hello du serveur de votre application a toomake des allers-retours. 

## <a id="WrapUp"></a>Modèles de données hybrides
Nous savons maintenant que l'incorporation (ou la dénormalisation) et le référencement (ou la normalisation) des données ont tous deux leurs avantages, mais qu'ils impliquent également des compromis. 

Il ne toujours avoir toobe ou, ne pas être toomix vous en faites d’un peu. 

En fonction des habitudes d’utilisation de votre application et les charges de travail il peut y avoir des cas où la combinaison incorporé et données référencés de sens et pourrait logique d’application responsable toosimpler avec moins de boucles tout en conservant un bon niveau de performances .

Envisagez de hello suivant JSON. 

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

Ici nous avons suivi (principalement) de modèle incorporés hello, où les données à partir d’autres entités sont incorporées dans les documents de niveau supérieur de hello, mais les autres données sont référencées. 

Si vous examinez le document de livre hello, nous pouvons voir quelques exemples intéressants de champs lorsque nous observons la tableau hello des auteurs. Il existe un *id* champ qui est le champ hello que nous utilisons également document d’auteur toorefer tooan précédent, une pratique courante dans un modèle normalisé mais nous avoir *nom* et *thumbnailUrl*. Nous avons simplement avez bloquée avec *id* et a laissé hello application tooget des informations supplémentaires, il est nécessaire à partir du document d’auteur respectifs hello à l’aide de hello « liaison », mais étant donné que notre application affiche le nom de l’auteur hello et un image miniature avec chaque livre nous pouvons enregistrer un serveur de toohello aller-retour par livre dans une liste par dénormalisation **certains** données de l’auteur de hello.

Bien sûr, si hello auteur modifié ou qu’ils voulaient tooupdate leur photo nous devrions toogo une mise à jour chaque livre ils jamais publié, mais pour notre application, en fonction de l’hypothèse hello que les auteurs ne changent pas leurs noms très souvent, il s’agit d’une conception acceptable décision.  

Dans l’exemple de hello **précalculée agrégats** valeurs toosave coûteux de traitement sur une opération de lecture. Dans l’exemple de hello, certaines données hello incorporées dans un document d’auteur hello donnée est calculée au moment de l’exécution. Chaque fois qu’un nouveau livre est publié, création d’un document de livre **et** hello countOfBooks champ a la valeur valeur tooa calculé en fonction du nombre de hello de documents d’un livre qui existent pour un auteur particulier. Cette optimisation serait correcte dans les systèmes lourde lecture où nous pouvons nous permettre de toodo des calculs sur les écritures dans l’ordre toooptimize lectures.

Hello toohave possibilité un modèle avec des champs calculés préalable est possible parce que prend en charge de la base de données Azure Cosmos **documents plusieurs transactions**. Nombreux magasins NoSQL ne peut pas effectuer des transactions dans les documents et par conséquent préconisent les décisions de conception, telles que « toujours incorporer tout », en raison de la limitation de toothis. Avec Azure Cosmos DB, vous pouvez utiliser des déclencheurs côté serveur, ou des procédures stockées, qui insèrent des livres et mettent à jour les auteurs au sein d’une transaction ACID. Maintenant vous n’avez pas **ont** tooembed de tous les éléments de tooone document simplement toobe sûr que vos données restent cohérentes.

## <a name="NextSteps"></a>Étapes suivantes
principaux éléments importants à retenir de Hello à partir de cet article est toounderstand que la modélisation des données dans un monde de schéma sont tout aussi importantes que jamais. 

Comme il n’existe aucun toorepresent de façon unique un élément de données sur un écran, il n’est aucun moyen simple de toomodel vos données. Vous devez toounderstand votre application et comment il génère, utiliser et traiter les données hello. Puis, en appliquant des hello les instructions présentées ici, vous peuvent définir sur la création d’un modèle qui répond aux besoins immédiats hello de votre application. Lorsque vos applications ont besoin de toochange, vous pouvez tirer parti flexibilité hello d’un tooembrace du schéma de base de données qui changent et évoluer facilement de votre modèle de données. 

toolearn savoir plus sur la base de données Azure Cosmos, référence du service toohello [documentation](https://azure.microsoft.com/documentation/services/cosmos-db/) page. 

toounderstand comment tooshard vos données sur plusieurs partitions, référence trop[le partitionnement des données dans la base de données Azure Cosmos](documentdb-partition-data.md). 
