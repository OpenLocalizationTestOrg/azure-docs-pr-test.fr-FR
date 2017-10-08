---
title: Introduction tooAzure Cosmos DB Graph API | Documents Microsoft
description: "Découvrez comment utiliser des graphiques de gros volumes de parcours, de requête et toostore de la base de données Azure Cosmos avec une faible latence à l’aide du langage de requête graphique hello hello GREMLINE de TinkerPop d’Apache."
services: cosmos-db
author: dennyglee
documentationcenter: 
ms.assetid: b916644c-4f28-4964-95fe-681faa6d6e08
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/21/2017
ms.author: denlee
ms.openlocfilehash: a4e79a4aa27976966baf0554928026177991ff69
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-cosmos-db-graph-api"></a>Introduction tooAzure Cosmos DB : API Graph

[Base de données Azure Cosmos](introduction.md) est hello service de base de données distribués internationalement, comportant plusieurs modèles à partir de Microsoft pour les applications critiques. Fournit de la base de données Azure Cosmos [distribution globale des clés en main](distribute-data-globally.md), [mise à l’échelle élastique de débit et de stockage](partition-data.md) des latences de milliseconde dans le monde entier, à un chiffre à 99e centile de hello, [cinq niveaux de cohérence bien définis](consistency-levels.md)et la garantie de disponibilité sauvegardé par [pointe SLA](https://azure.microsoft.com/support/legal/sla/cosmos-db/). Base de données Azure Cosmos [automatiquement les données d’index](http://www.vldb.org/pvldb/vol8/p1668-shukla.pdf) sans avoir toodeal avec la gestion de schéma et d’index. Il est multi-modèle et prend en charge les modèles de données en colonnes, documents, graphiques et clé-valeur.

![Gremlin, graphiques et Azure Cosmos DB](./media/graph-introduction/graph-gremlin.png)

Bonjour Azure Cosmos DB Graph API fournit :

- Modélisation graphique
- API Traversal
- Distribution mondiale clé en main
- Évolution élastique de débit et de stockage avec moins de 10 ms, temps de latence de lecture et inférieure à 15 ms à 99e centile de hello
- Indexation automatique avec disponibilité de requête instantanée
- Modèles de cohérence ajustables
- SLA complets, incluant une disponibilité à 99,99 %

tooquery Azure Cosmos DB, vous pouvez utiliser hello [Apache TinkerPop](http://tinkerpop.apache.org) graphique de langage de parcours, [GREMLINE](http://tinkerpop.apache.org/docs/current/reference/#graph-traversal-steps), ou d’autres systèmes de graphique compatible TinkerPop comme [Apache Spark GraphX](spark-connector-graph.md).

Cet article fournit une vue d’ensemble de hello Azure Cosmos DB l’API Graph et explique comment vous pouvez l’utiliser des graphiques massive toostore avec des milliards de sommets et de bords. Vous pouvez interroger des graphiques de hello avec une latence de milliseconde et faire évoluer facilement de schéma et structure de graphique hello.

## <a name="graph-database"></a>Base de données de graphiques
Les données qu’il apparaît dans le monde réel de hello sont naturellement connectées. La modélisation de données traditionnelle se concentre sur les entités. Pour de nombreuses applications, il existe également un toomodel besoin ou toomodel entités et relations naturellement.

Un [graphique](http://mathworld.wolfram.com/Graph.html) est une structure composée de [sommets](http://mathworld.wolfram.com/GraphVertex.html) et de [bords](http://mathworld.wolfram.com/GraphEdge.html). Les sommets et les bords peuvent avoir un nombre arbitraire de propriétés. Les sommets désignent des objets discrets comme une personne, un lieu ou un événement. Les bords désignent les relations entre les sommets. Par exemple, une personne peut en connaître une autre, être impliquée dans un événement et avoir récemment été dans un lieu. Propriétés expriment plus d’informations sur les bords et les sommets hello. Les exemples de propriétés incluent un sommet qui a un nom et un âge, et un bord qui a un horodatage et/ou un poids. Plus formellement, ce modèle est appelé un [graphique de propriétés](http://tinkerpop.apache.org/docs/current/reference/#intro). Base de données Azure Cosmos prend en charge le modèle de graphique de propriété hello.

Hello exemple suivant indique graphique des relations entre les personnes, les appareils mobiles, les intérêts et les systèmes d’exploitation.

![Exemple de base de données montrant des personnes, des appareils et des centres d’intérêt](./media/graph-introduction/sample-graph.png)

Graphiques sont utile toounderstand un large éventail de jeux de données dans la science, la technologie et entreprise. Les bases de données de graphiques vous permettent de modéliser et de stocker des graphiques naturellement et efficacement, ce qui les rend utiles pour de nombreux scénarios. Les bases de données de graphiques sont généralement des bases de données NoSQL, car ces cas d’utilisation requièrent souvent aussi une flexibilité des schémas et une itération rapide.

Les graphiques offrent une nouvelle technique puissante de modélisation des données. Mais cela par lui-même n’est pas un toouse raison suffisante une base de données de graphique. Dans de nombreux cas et modèles d’utilisation impliquant des traversées de graphiques, ces derniers s’avèrent plus performants que les bases de données SQL et NoSQL traditionnelles en termes de magnitude. Cette différence de performances est encore amplifiée lors de la traversée de plusieurs relations telles que ami d’un ami.

Vous pouvez combiner hello rapide de manière répétée qui fournissent des bases de données de graphique avec les algorithmes de graphique, telles que la recherche en profondeur, recherche de prioritaire et l’algorithme de Dijkstra, problèmes toosolve dans différents domaines, comme les réseaux sociaux, gestion de contenu, géographiques, et les recommandations.

## <a name="planet-scale-graphs-with-azure-cosmos-db"></a>Graphiques à l’échelle de la planète avec Azure Cosmos DB
Base de données Cosmos Azure est une base de données de graphique entièrement géré qui offre la distribution globale, élastique mise à l’échelle de stockage et de débit, l’indexation automatique et requête, niveaux de cohérence paramétrables et prise en charge de la norme de TinkerPop hello.  

![Architecture graphique Azure Cosmos DB](./media/graph-introduction/cosmosdb-graph-architecture.png)

Base de données Azure Cosmos offre suivant de hello différenciés fonctionnalités lors de la comparaison tooother bases de données de graphique dans le marché de hello :

* Stockage et débit extensibles de façon élastique

 Graphiques dans le monde réel de hello doivent tooscale au-delà de la capacité de hello d’un serveur unique. Avec Azure Cosmos DB, vous pouvez mettre à l’échelle vos graphiques en toute transparence sur plusieurs serveurs. Vous pouvez également monter en débit hello de votre graphique indépendamment en fonction de vos modèles d’accès. Base de données Azure Cosmos prend en charge les bases de données de graphique qui peuvent mettre à l’échelle toovirtually les tailles de stockage illimité et débit approvisionné.

* Réplication multirégion

 Base de données Azure Cosmos réplique en toute transparence vos zones de tooall de données de graphique que vous avez associé votre compte. La réplication vous permet de toodevelop les applications qui requièrent l’accès global toodata. Il existe des compromis dans les zones hello de cohérence, disponibilité, performances et garanties correspondantes. Azure Cosmos DB fournit un basculement régional transparent avec des API d’hébergement multiple. Vous pouvez adapter configurées de débit et stockage monde hello.

* Requêtes et parcours rapides avec une syntaxe Gremlin familière

 Stockez des sommets et des bords hétérogènes, et interrogez ces documents via une syntaxe Gremlin familière. Base de données Azure Cosmos utilise un simultanéité sans verrouillage, structuré par journal indexation tooautomatically index de la technologie tout le contenu. Cette fonctionnalité permet des requêtes riches en temps réel et parcours sans hello besoin des indicateurs de schéma toospecify, des index secondaires ou des vues. Pour en savoir plus, consultez [Interroger des graphiques à l’aide de Gremlin](gremlin-support.md).

* Gestion intégrale

 Base de données Azure Cosmos élimine hello besoin toomanage de base de données et ordinateur ressources. Comme un service entièrement géré de Microsoft Azure, vous effectuez pas besoin de toomanage virtuels, déployez et configurez les logiciels, gérez la mise à l’échelle ou traiter les mises à niveau de la couche de données complexes. Chaque graphique est automatiquement sauvegardé et protégé contre les défaillances régionales. Vous pouvez facilement ajouter un compte Azure Cosmos DB et approvisionner la capacité dont vous avez besoin afin de vous concentrer pleinement sur votre application plutôt que sur l’exploitation et la gestion de votre base de données.

* Indexation automatique

 Par défaut, Azure Cosmos DB automatiquement indexe toutes les propriétés de hello au sein des nœuds et des arêtes dans le graphique de hello et ne pas attendre ou exiger n’importe quel schéma ou la création d’index secondaire.

* Compatibilité avec Apache TinkerPop

 Base de données Azure Cosmos en mode natif prend en charge hello open source Apache TinkerPop standard et peuvent être intégré avec d’autres systèmes compatibles TinkerPop le graphique. Par conséquent, vous pouvez facilement effectuer une migration à partir d’une autre base de données de graphiques comme Titan ou Neo4j, ou utiliser Azure Cosmos DB avec des infrastructures d’analyse graphique comme [Apache Spark GraphX](spark-connector-graph.md).

* Niveaux de cohérence ajustables

 Sélectionnez à partir de cinq cohérence bien définis niveaux tooachieve compromis optimal se situe entre la cohérence et performances. Pour les requêtes et les opérations de lecture, Azure Cosmos DB propose cinq niveaux de cohérence distincts : Fort, En fonction de l’obsolescence, Par session, Préfixe cohérent et Éventuel. Ces niveaux de cohérence granulaire et bien définie permettre toomake de son compromis entre la latence, la disponibilité et la cohérence. Pour en savoir plus [à l’aide de la cohérence des niveaux de disponibilité de toomaximize et les performances de DocumentDB](consistency-levels.md).

Base de données Azure Cosmos également peut utiliser plusieurs modèles, tels que le document et de graphique, dans hello les mêmes conteneurs/bases de données. Vous pouvez utiliser une collection toostore graphique des données du document côte à côte avec les documents. Vous pouvez utiliser les deux requêtes SQL sur JSON et GREMLINE requêtes tooquery hello des mêmes données sous forme de graphique.

## <a name="getting-started"></a>Prise en main
Vous pouvez utiliser hello Azure interface de ligne de commande (CLI), Azure Powershell, ou hello portail Azure avec prise en charge pour les comptes de base de données Azure Cosmos toocreate graph API. Après avoir créé les comptes, hello portail Azure fournit un point de terminaison de service, tel que `https://<youraccount>.graphs.azure.com`, qui fournit un serveur frontal WebSocket pour GREMLINE. Vous pouvez configurer vos outils TinkerPop compatible, comme hello [Gremin Console](http://tinkerpop.apache.org/docs/current/reference/#gremlin-console), applications de point de terminaison et de génération de toothis dans Java, Node.js ou un pilote de client GREMLINE tooconnect.

Hello tableau suivant présente les pilotes GREMLINE populaires que vous pouvez utiliser par rapport à la base de données Azure Cosmos :

| Télécharger | Documentation |
| --- | --- |
| [Java](https://mvnrepository.com/artifact/com.tinkerpop.gremlin/gremlin-java) |[Gremlin JavaDoc](http://tinkerpop.apache.org/javadocs/current/full/) |
| [Node.JS](https://www.npmjs.com/package/gremlin) |[Gremlin-JavaScript sur Github](https://github.com/jbmusso/gremlin-javascript) |
| [Console Gremlin](https://tinkerpop.apache.org/downloads.html) |[Documents TinkerPop](http://tinkerpop.apache.org/docs/current/reference/#gremlin-console) |

Base de données Cosmos Azure fournit également une bibliothèque .NET qui a des méthodes d’extension GREMLINE par-dessus hello [kits de développement de base de données Azure Cosmos](documentdb-sdk-dotnet.md) via NuGet. Cette bibliothèque fournit un serveur de GREMLINE « in-process » que vous pouvez utiliser tooconnect tooDocumentDB directement les partitions de données.

| Télécharger | Documentation |
| --- | --- |
| [.NET](https://www.nuget.org/packages/Microsoft.Azure.Graphs/) |[Microsoft.Azure.Graphs](https://msdn.microsoft.com/library/azure/dn948556.aspx) |

À l’aide de hello [Azure Cosmos DB émulateur](local-emulator.md), vous pouvez utiliser toodevelop de l’API Graph hello et tester localement sans création d’un abonnement Azure ou entraîner des coûts. Lorsque vous êtes satisfait du fonctionne de votre application dans l’émulateur de hello, vous pouvez basculer toousing un compte de base de données Azure Cosmos dans le cloud de hello.

## <a name="scenarios-for-graph-support-of-azure-cosmos-db"></a>Scénarios de prise en charge des graphiques par Azure Cosmos DB
Voici quelques scénarios où la prise en charge des graphiques par Azure Cosmos DB peut être utile :

* Réseaux sociaux

 En associant des données sur vos clients et leurs interactions avec d’autres personnes, vous pouvez développer des expériences personnalisées, prédire le comportement des clients ou connecter entre elles des personnes ayant les mêmes intérêts. Base de données Azure Cosmos pouvez toomanage utilisé réseaux sociaux et effectuer le suivi des données et les préférences du client.

* Moteurs de recommandation

 Ce scénario est couramment utilisé dans le secteur de vente au détail hello. En associant des informations sur les produits, les utilisateurs et les interactions des utilisateurs (achats, navigation ou notation d’un article), vous pouvez générer des recommandations personnalisées. Bonjour à faible latence, élastique et native prise en charge de graphique de base de données Azure Cosmos est idéal pour la modélisation de ces interactions.

* Géospatial

 De nombreuses applications de télécommunications, logistique et de la planification de voyage doivent toofind un emplacement d’intérêt dans une zone ou recherchez l’itinéraire le plus court/optimal de hello entre deux emplacements. Azure Cosmos DB constitue une solution naturelle à ces problèmes.

* Internet des Objets

 Avec un réseau hello et les connexions entre les appareils IoT modélisés sous forme de graphique, vous pouvez générer une meilleure compréhension de l’état de hello de vos périphériques et les ressources et savoir comment les modifications dans une partie du réseau de hello sont susceptible d’affecter une autre partie.

## <a name="next-steps"></a>Étapes suivantes
toolearn en savoir plus sur la prise en charge de graphique dans la base de données Azure Cosmos, consultez :

* Prise en main hello [didacticiel graphique de base de données Azure Cosmos](create-graph-dotnet.md).
* En savoir plus sur la façon de trop[de requête graphiques dans la base de données Azure Cosmos à l’aide de GREMLINE](gremlin-support.md).
