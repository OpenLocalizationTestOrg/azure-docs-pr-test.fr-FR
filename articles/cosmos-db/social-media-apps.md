---
title: "Modèle de conception Azure Cosmos DB : applications de réseaux sociaux | Microsoft Docs"
description: "En savoir plus sur un modèle de conception pour les réseaux sociaux en tirant parti de flexibilité hello du stockage de base de données Azure Cosmos et d’autres services Azure."
keywords: "applications de réseaux sociaux"
services: cosmos-db
author: ealsur
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: 2dbf83a7-512a-4993-bf1b-ea7d72e095d9
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/29/2017
ms.author: mimig
ms.openlocfilehash: 47a22f2c5762d62b176921c8052e7bd75d8cf6ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="going-social-with-azure-cosmos-db"></a>Réseaux sociaux avec Azure Cosmos DB
Vivre dans une société massivement interconnectée signifie qu’à un moment donné, vous intégrerez forcément un **réseau social**. Nous utilisons à notre passionné tookeep de réseaux sociaux en contact avec des amis, collègues, ou parfois tooshare avec des personnes ayant des intérêts communs.

En tant que les ingénieurs ou aux développeurs, nous pourrions avoir demandé comment ces réseaux de stocker et d’interconnexion nos données, ou peut avoir même été toocreate ressources en stockage sous-utilisées ou architecte un nouveau réseau social pour une niche spécifique du marché vous-même. C'est-à-dire lorsque les question big hello se pose : comment toutes ces données sont stockées ?

Supposons que nous avons décidé de créer un nouveau réseau social, où nos utilisateurs peuvent publier des articles accompagnés de contenu multimédia tel que des images, des vidéos ou même de la musique. Les utilisateurs peuvent commenter les publications et attribuer des points pour créer des classements. Il y aura un flux de messages que les utilisateurs vont voir et être en mesure de toointeract avec sur la page d’accueil du site Web principal hello. Cela ne sembler très complexe (dans un premier temps), mais pour des raisons de hello de simplicité, nous allons vous arrêter là (nous avons plonger dans les flux d’utilisateur personnalisée affectés par les relations, mais elle dépasse l’objectif hello de cet article).

Alors, comment et où stockons-nous ces données ?

Beaucoup d'entre vous peuvent bénéficier de bases de données SQL ou disposer au moins la notion de [relationnelle de modélisation de données](https://en.wikipedia.org/wiki/Relational_model) et vous pouvez être tenté toostart dessin quelque chose comme ceci :

![Diagramme illustrant un modèle relationnel relatif](./media/social-media-apps/social-media-apps-sql.png) 

Une structure de données tout à fait normalisée et agréable... qui n’est pas extensible. 

Ne vous méprenez pas, j’utilise des bases de données SQL depuis très longtemps, elles sont parfaites, mais comme tout modèle, pratique et plateforme logicielle, elles ne sont pas adaptées à tous les scénarios.

Pourquoi n’est pas SQL hello meilleur choix dans ce scénario ? Examinons structure hello d’une publication unique, si je souhaitais tooshow valider dans une application ou un site Web, je devrais toodo une requête avec... tableau 8 jointures ( !) tooshow simplement un unique post, maintenant, image, un flux de messages qui dynamiquement charger et s’affichent sur l’écran hello et que vous pouvez voir où je vais.

Nous pourrions, bien sûr, utiliser une instance SQL humongous avec suffisamment d’alimentation toosolve des milliers de requêtes avec ces nombreuses tooserve de jointures notre contenu, mais réellement, pourquoi serait nous lorsqu’une solution plus simple existe ?

## <a name="hello-nosql-road"></a>feuille de route Hello NoSQL
Cet article vous guide dans la modélisation des données de votre plate-forme sociaux avec la base de données NoSQL de Azure [base de données Azure Cosmos](https://azure.microsoft.com/services/cosmos-db/) de façon économique tout en tirant parti d’autres fonctionnalités de base de données Azure Cosmos comme hello [GREMLINE l’API Graph ](../cosmos-db/graph-introduction.md). Avec une approche [NoSQL](https://en.wikipedia.org/wiki/NoSQL), le stockage des données au format JSON et l’application de la [dénormalisation](https://en.wikipedia.org/wiki/Denormalization), notre publication si compliquée auparavant peut être transformée en un seul [document](https://en.wikipedia.org/wiki/Document-oriented_database) :


    {
        "id":"ew12-res2-234e-544f",
        "title":"post title",
        "date":"2016-01-01",
        "body":"this is an awesome post stored on NoSQL",
        "createdBy":User,
        "images":["http://myfirstimage.png","http://mysecondimage.png"],
        "videos":[
            {"url":"http://myfirstvideo.mp4", "title":"hello first video"},
            {"url":"http://mysecondvideo.mp4", "title":"hello second video"}
        ],
        "audios":[
            {"url":"http://myfirstaudio.mp3", "title":"hello first audio"},
            {"url":"http://mysecondaudio.mp3", "title":"hello second audio"}
        ]
    }

Et il peut être obtenu avec une seule requête, sans jointure. Cela est beaucoup plus simple et directe et budget-wise, elle nécessite moins ressources tooachieve un meilleur résultat.

Base de données Azure Cosmos permet de s’assurer que toutes les propriétés de hello sont indexées avec son indexation automatique, ce qui peut même être [personnalisé](indexing-policies.md). Hello schéma approche nous permet de stocker des Documents avec différents et structures dynamiques, peut-être demain que nous souhaitons toohave publications gère une liste de catégories ou de hashtags associé, Cosmos DB hello des Documents avec hello ajouté les attributs avec sans supplémentaires travail nous requis.

Les commentaires sur une publication peuvent être traités comme n’importe quelle autre publication avec une propriété parente (cela simplifie le mappage d’objets). 

    {
        "id":"1234-asd3-54ts-199a",
        "title":"Awesome post!",
        "date":"2016-01-02",
        "createdBy":User2,
        "parent":"ew12-res2-234e-544f"
    }

    {
        "id":"asd2-fee4-23gc-jh67",
        "title":"Ditto!",
        "date":"2016-01-03",
        "createdBy":User3,
        "parent":"ew12-res2-234e-544f"
    }

Et toutes les interactions sociales peuvent être stockées sur un objet distinct en tant que compteurs :

    {
        "id":"dfe3-thf5-232s-dse4",
        "post":"ew12-res2-234e-544f",
        "comments":2,
        "likes":10,
        "points":200
    }

La création de flux consiste simplement à créer des documents qui peuvent contenir une liste des ID des publications avec un ordre de pertinence donné :

    [
        {"relevance":9, "post":"ew12-res2-234e-544f"},
        {"relevance":8, "post":"fer7-mnb6-fgh9-2344"},
        {"relevance":7, "post":"w34r-qeg6-ref6-8565"}
    ]

Nous aurions pu un flux de données « dernier » avec classés par date de création de publications, un flux de données « plu » avec ceux publie avec aime plus Bonjour des dernières 24 heures, nous avons même implémenter un flux personnalisé pour chaque utilisateur basée sur la logique du marché et intérêts, et il est toujours une liste de  valide. C’est une question de comment toobuild ces listes, mais les performances de lecture hello reste être confrontées. Une fois que l’acquisition d’une de ces listes, nous nous émettre une requête unique de tooCosmos base de données à l’aide de hello [dans l’opérateur](documentdb-sql-query.md#WhereClause) tooobtain des pages de publications à la fois.

Hello de flux de flux de données peut être créé à l’aide de [des Services d’application Azure](https://azure.microsoft.com/services/app-service/) les processus d’arrière-plan : [Webjobs](../app-service-web/web-sites-create-web-jobs.md). Une fois qu’une publication est créée, le traitement en arrière-plan peut être déclenché à l’aide de [Azure Storage](https://azure.microsoft.com/services/storage/) [les files d’attente](../storage/queues/storage-dotnet-how-to-use-queues.md) et tâches Web déclenchées à l’aide de hello [Azure Webjobs SDK](../app-service-web/websites-dotnet-webjobs-sdk.md), qui implémente Hello valider la propagation à l’intérieur du flux de données en fonction de votre propre logique personnalisée. 

Points et similaire sur une publication peut être traités de manière différée à l’aide de cette même toocreate de technique un environnement cohérent par la suite.

Cela est plus compliqué pour les abonnés. COSMOS DB a une limite de taille maximale des documents, et lecture/écriture de documents volumineux peuvent affecter l’évolutivité de hello de votre application. Vous pouvez envisager de stocker les abonnés dans un document avec cette structure :

    {
        "id":"234d-sd23-rrf2-552d",
        "followersOf": "dse4-qwe2-ert4-aad2",
        "followers":[
            "ewr5-232d-tyrg-iuo2",
            "qejh-2345-sdf1-ytg5",
            //...
            "uie0-4tyg-3456-rwjh"
        ]
    }

Cela peut fonctionner pour un utilisateur avec quelques milliers suivis, mais si certains célébrités joint nos rangs, cette approche entraîne une taille de document volumineux tooa, et peut limiter la taille du document hello finalement d’accès.

toosolve, nous pouvons utiliser une approche mixte. Dans le cadre du document de statistiques utilisateur hello, nous pouvons stocker nombre hello imposait :

    {
        "id":"234d-sd23-rrf2-552d",
        "user": "dse4-qwe2-ert4-aad2",
        "followers":55230,
        "totalPosts":452,
        "totalPoints":11342
    }

Et graphique de réel hello imposait peut être stockée à l’aide de la base de données Azure Cosmos [l’API Graph GREMLINE](../cosmos-db/graph-introduction.md), toocreate [sommets](http://mathworld.wolfram.com/GraphVertex.html) pour chaque utilisateur et [bords](http://mathworld.wolfram.com/GraphEdge.html) conservant hello » Relations de suit-A-B ». Hello API Graph nous allons vous non seulement obtenez barreaux hello d’un utilisateur donné, mais créez des requêtes plus complexes tooeven suggérer des personnes en commun. Si nous ajoutons hello du graphique toohello catégories de contenu que les utilisateurs telles qu’ou profitez, nous pouvons démarrer a expériences qui incluent la découverte de contenu active, suggérant contenu que celles que nous suivre comme, ou la recherche des personnes avec lesquelles nous pouvons ont beaucoup en commun.

document de statistiques utilisateur Hello peut toujours être toocreate utilisé cartes hello l’interface utilisateur ou des versions préliminaires de profil rapide.

## <a name="hello-ladder-pattern-and-data-duplication"></a>Hello « Dans le cas » modèle et données de la duplication
Comme vous l’avez peut-être remarqué dans le document JSON hello qui fait référence à une publication, il existe plusieurs occurrences d’un utilisateur. Et vous devez deviner droite, que cela signifie que les informations hello qui représente un utilisateur, étant donné cette dénormalisation, peuvent être présentes dans plusieurs emplacements.

Dans tooallow ordre pour les requêtes plus rapides, nous entraînent la déduplication des données. Hello problème avec cet effet est que si par une action, les modifications de données d’un utilisateur, nous devons toofind toutes les activités hello il jamais a et mettre à jour toutes les. Cela ne semble pas très pratique, n’est-ce pas ?

Nous sommes toosolve continu en identifiant hello des attributs de clé d’un utilisateur qui nous indiquent dans notre application pour chaque activité. Si nous visuellement afficher un billet dans notre application et afficher uniquement l’auteur hello nom et image, pourquoi stocker toutes les données de l’utilisateur hello dans hello « createdBy » attribut ? Si chaque commentaire, nous affichons simplement hello l’image d’utilisateur, nous n’avez vraiment reste hello de ses informations. C’est là, quelque chose qu'appeler hello « échelle pattern » entre en jeu.

Prenons comme exemple les informations utilisateur :

    {
        "id":"dse4-qwe2-ert4-aad2",
        "name":"John",
        "surname":"Doe",
        "address":"742 Evergreen Terrace",
        "birthday":"1983-05-07",
        "email":"john@doe.com",
        "twitterHandle":"@john",
        "username":"johndoe",
        "password":"some_encrypted_phrase",
        "totalPoints":100,
        "totalPosts":24
    }

En examinant ces informations, nous pouvons rapidement détecter les informations essentielles et celles qui ne le sont pas, créant ainsi une « échelle » :

![Diagramme d’un modèle d’échelle](./media/social-media-apps/social-media-apps-ladder.png)

étape de plus petite Hello est appelée un UserChunk, un hello minimale information qui identifie un utilisateur et il est utilisé pour la duplication de données. En réduisant la taille de hello hello dupliqué tooonly hello des informations de données nous sera « afficher », nous réduire la possibilité de hello de mises à jour massives.

étape intermédiaire de Hello est appelée utilisateur de hello, hello complète des données qui seront utilisées à la plupart des requêtes dépendant des performances sur la base de données Cosmos, hello plus sollicitées et critiques. Il inclut des informations de hello représentées par un UserChunk.

Hello plus grande est hello étendue utilisateur. Elle inclut toutes les informations d’utilisateur critique hello ainsi que les autres données ne nécessitant pas vraiment toobe lecture rapidement ou son utilisation est éventuelle (par exemple, le processus de connexion hello). Ces données peuvent être stockées en dehors de Cosmos DB, dans Azure SQL Database ou des tables Stockage Azure.

Pourquoi serait fractionner les utilisateur hello et même stocker ces informations dans des emplacements différents ? Parce que, à partir d’un point de vue des performances, hello les documents hello plus grandes, hello costlier requêtes de hello. Conserver les documents compacte avec hello droite informations toodo toutes vos performances dépendant de requêtes de votre réseau social et magasin hello autres informations supplémentaires pour les scénarios éventuelles, par exemple, les modifications de profil complet, connexions, même d’exploration de données pour l’analytique de l’utilisation et Big Initiatives de données. Nous avons vraiment ne se soucient pas si hello collecte de données d’exploration de données sont plus lentes, car il est en cours d’exécution sur la base de données SQL Azure, nous ont concernent cependant que nos utilisateurs bénéficient d’une expérience rapide et compacte. Un utilisateur, stocké sur Cosmos DB, ressemblerait à ceci :

    {
        "id":"dse4-qwe2-ert4-aad2",
        "name":"John",
        "surname":"Doe",
        "username":"johndoe"
        "email":"john@doe.com",
        "twitterHandle":"@john"
    }

Et une publication ressemblerait à ce qui suit :

    {
        "id":"1234-asd3-54ts-199a",
        "title":"Awesome post!",
        "date":"2016-01-02",
        "createdBy":{
            "id":"dse4-qwe2-ert4-aad2",
            "username":"johndoe"
        }
    }

Et lorsqu’une modification se produit lorsque un des attributs hello de segment de hello est affecté, il est toofind facilement des documents hello affectée à l’aide de requêtes qui pointent les attributs toohello indexé (sélectionnez * FROM publie p WHERE p.createdBy.id == « edited_user_id ») et de la mise à jour segments de Hello.

## <a name="hello-search-box"></a>zone de recherche Hello
Heureusement, les utilisateurs génèrent beaucoup de contenu. Nous devons être en mesure de tooprovide hello capacité toosearch et rechercher le contenu peut ne pas être directement leurs flux de données de contenu, peut-être parce que nous ne suivent pas les créateurs de hello et peut-être nous essayons simplement toofind ce billet ancien que nous l’avons fait il y a 6 mois.

Heureusement, et étant donné que nous utilisons la base de données Azure Cosmos, nous pouvons facilement implémenter un moteur de recherche à l’aide de [Azure Search](https://azure.microsoft.com/services/search/) dans quelques minutes et sans avoir à taper une seule ligne de code (autre que hello évidemment, recherchez les processus et l’interface utilisateur).

Pourquoi est-ce si facile ?

Azure Search implémente ce qu’ils appellent [indexeurs](https://msdn.microsoft.com/library/azure/dn946891.aspx), connectées dans les référentiels de votre processus d’arrière-plan et comme par magie ajouter, mettre à jour ou supprimer vos objets dans les index de hello. Ils prennent en charge les [indexeurs Azure SQL Database](https://blogs.msdn.microsoft.com/kaevans/2015/03/06/indexing-azure-sql-database-with-azure-search/), les [indexeurs d’objets blob Azure](../search/search-howto-indexing-azure-blob-storage.md) et les [indexeurs Azure Cosmos DB](../search/search-howto-index-documentdb.md). Hello transition des informations à partir de la base de données Cosmos tooAzure recherche est simple, comme les informations de magasin au format JSON, nous devons trop[créer notre Index](../search/search-create-index-portal.md) et mapper les attributs à partir de notre Documents nous indexer et voilà, en quelques minutes (dépend de taille hello de nos données), notre tout le contenu sera disponible toobe recherché, par la meilleure solution de recherche en tant que Service hello dans l’infrastructure cloud. 

Pour plus d’informations sur Azure Search, vous pouvez visiter hello [tooSearch du Guide Hitchhiker](https://blogs.msdn.microsoft.com/mvpawardprogram/2016/02/02/a-hitchhikers-guide-to-search/).

## <a name="hello-underlying-knowledge"></a>base de connaissances Hello sous-jacent
Après avoir stocké ce contenu dont la taille augmente chaque jour, nous pourrions penser : que puis-je faire avec toutes ces informations de mes utilisateurs ?

les réponses Hello sont simple : placer toowork et apprendre à partir de celui-ci.

Mais, que pouvons-nous apprendre ? Exemples facile [analyse des sentiments](https://en.wikipedia.org/wiki/Sentiment_analysis), les recommandations en fonction des préférences de l’utilisateur ou même un automatisés moderator contenu qui permet de s’assurer que tous les hello contenu publié par notre réseau social est sécurisé pour hello de contenu famille.

Maintenant que j’ai reçu vous raccordé, vous devez penser vous devez certains bloc dans math science tooextract ces motifs et les informations en dehors des bases de données simples et des fichiers, mais vous serez incorrect.

[Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/)dans le cadre du hello [Cortana Intelligence Suite](https://www.microsoft.com/en/server-cloud/cortana-analytics-suite/overview.aspx), hello n’est un service cloud entièrement géré qui vous permet de créer des workflows à l’aide d’algorithmes dans une simple interface de glisser-déplacer, de vos propres algorithmes de code dans [R](https://en.wikipedia.org/wiki/R_\(programming_language\)) ou utiliser certaines des hello déjà créé et prêt toouse API telles que : [texte Analytique](https://gallery.cortanaanalytics.com/MachineLearningAPI/Text-Analytics-2), [Moderator contenu](https://www.microsoft.com/moderator) ou [recommandations](https://gallery.cortanaanalytics.com/MachineLearningAPI/Recommendations-2).

tooachieve n’importe quel de ces scénarios d’apprentissage, nous pouvons utiliser [Azure Data Lake](https://azure.microsoft.com/services/data-lake-store/) tooingest hello des informations à partir de sources différentes et utiliser [U-SQL](https://azure.microsoft.com/documentation/videos/data-lake-u-sql-query-execution/) tooprocess hello des informations et générer une sortie qui peuvent être traités par Azure Machine Learning.

Une autre option disponible est toouse [Microsoft cognitifs Services](https://www.microsoft.com/cognitive-services) une meilleure de nos utilisateurs contenus ; seulement pouvons nous comprenons les tooanalyze (en analysant qu’ils écrivent avec [texte Analytique API](https://www.microsoft.com/cognitive-services/en-us/text-analytics-api)), mais Nous avons également détecter du contenu indésirable ou réservé aux adultes et agir en conséquence avec [ordinateur Vision API](https://www.microsoft.com/cognitive-services/en-us/computer-vision-api). Les Services cognitifs comprennent un grand nombre de solutions out of box qui ne nécessitent pas tous les types de Machine Learning connaissances toouse.

## <a name="a-planet-scale-social-experience"></a>Une expérience sociale à l’échelle de la planète
Il existe un dernier sujet tout aussi important à traiter : **l’évolutivité**. Lors de la conception d’une architecture, qu'il est essentiel que chaque composant peut mettre à l’échelle sur son propre, soit parce que nous avons besoin de davantage de données tooprocess ou car nous souhaitons toohave une plus grande couverture géographique (ou les deux). Heureusement, Cosmos DB offre une **solution clé en main** pour gérer une tâche aussi complexe.

Prend en charge de COSMOS DB [le partitionnement dynamique](https://azure.microsoft.com/blog/10-things-to-know-about-documentdb-partitioned-collections/) out-of-the-box en créant automatiquement des partitions basées sur une donnée **clé de partition** (défini comme un des attributs hello dans vos documents). Définition hello correct de clé de partition doit être effectuée au moment du design et en conservant Bonjour d’esprit [meilleures pratiques](../cosmos-db/partition-data.md#designing-for-partitioning) disponible ; dans les cas de hello une expérience de réseaux sociaux, votre stratégie de partitionnement doit être alignée avec moyen hello vous interroger (lectures au sein de hello même partition sont souhaitable) et d’écriture (éviter des « zones réactives » en répartissant les écritures sur plusieurs partitions). Certaines options sont : partitions basées sur une clé temporaire (jour/mois/semaine), par catégorie de contenu, par région géographique, par l’utilisateur ; tout dépend vraiment comment vous interroge les données de salutation et afficher dans votre expérience sociale. 

Un point intéressant intéressant de mentionner que Cosmos DB exécutera vos requêtes (y compris [agrégats](https://azure.microsoft.com/blog/planet-scale-aggregates-with-azure-documentdb/)) sur toutes vos partitions en toute transparence, vous n’avez pas besoin tooadd toute logique à mesure que vos données augmentent.

Avec le temps, le trafic et la consommation des ressources augmenteront (mesurés en unité de requête ou [RU](request-units.md)). Vous allez lire et écrire plus fréquemment que votre userbase se développe et ils démarrent créer et de lire davantage de contenu ; Hello la possibilité de **mise à l’échelle votre débit** est indispensable. Augmentation de notre RUs est très simple, nous pouvons le faire en quelques clics sur hello portail Azure ou par [émettre des commandes via hello API](https://docs.microsoft.com/rest/api/documentdb/replace-an-offer).

![Mise à l’échelle et définition d’une clé de partition](./media/social-media-apps/social-media-apps-scaling.png)

Imaginez que les choses continuent de s’améliorer et que des utilisateurs d’une autre région, d’un autre pays ou d’un autre continent découvrent votre plateforme et l’utilisent ? Quelle bonne surprise !

Mais attendez... vous réalisez dès leur expérience avec votre plateforme n’est pas optimal ; ils sont jusqu'à présent en dehors de votre région opérationnelle que la latence de hello est horribles, que vous évidemment ne les tooquit. Mais il existe un moyen facile de **développer votre visibilité globale** !

COSMOS DB vous permet de [répliquer vos données globalement](../cosmos-db/tutorial-global-distribution-documentdb.md) et en toute transparence, en quelques clics et automatiquement sélection parmi les régions disponibles hello votre [code client](../cosmos-db/tutorial-global-distribution-documentdb.md). Cela signifie également que vous pouvez avoir [plusieurs régions de basculement](regional-failover.md). 

Lorsque vous répliquez vos données globalement, vous devez toomake sûr que vos clients peuvent profiter de celui-ci. Si vous utilisez un serveur web frontal ou un accès API à partir de clients mobiles, vous pouvez déployer [Azure Traffic Manager](https://azure.microsoft.com/services/traffic-manager/) et votre Service d’applications Azure sur toutes les régions hello souhaité, à l’aide de cloner un [configuration des performances](../app-service-web/web-sites-traffic-manager.md)toosupport couverture étendue globale. Lorsque vos clients accèdent à votre API ou un serveur frontal, ils seront routé toohello du Service d’applications le plus proche, qui à son tour, connecte réplica de base de données Cosmos toohello local.

![Ajout global couverture tooyour social de la plateforme](./media/social-media-apps/social-media-apps-global-replicate.png)

## <a name="conclusion"></a>Conclusion
Cet article tente tooshed certaines clair dans alternatives hello de création de réseaux sociaux entièrement sur Azure avec les services de faible coût et de fournir d’excellents résultats en promouvant le recours hello d’une distribution de solution et les données de plusieurs niveaux de stockage appelée « Échelle ».

![Diagramme de l’interaction entre les services Azure pour les réseaux sociaux](./media/social-media-apps/social-media-apps-azure-solution.png)

Hello fait qu’il n’existe aucune puce silver pour ce genre de scénarios, il comprend hello synergy créé par combinaison de hello de services excellents qui nous permettent des expériences exceptionnelles toobuild : hello vitesse et libre de base de données Azure Cosmos tooprovide une application sociale, intelligence Hello derrière une solution de recherche de première classe telles que Azure Search et la flexibilité de hello de Services d’application Azure toohost pas même les applications indépendantes du langage mais le processus d’arrière-plan puissant et hello extensible de stockage Azure et de base de données SQL Azure pour le stockage des volumes importants de données et hello power analytique d’Azure Machine Learning toocreate connaissances et analyse décisionnelle qui peut fournir des commentaires tooour processus et nous aider à remettre hello toohello contenu directement les utilisateurs appropriés.

## <a name="next-steps"></a>Étapes suivantes
toolearn en savoir plus sur les cas d’usage pour Cosmos DB, consultez [cas d’usage courants Cosmos DB](use-cases.md).
