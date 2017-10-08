---
title: "aaaCommon cas d’utilisation et les scénarios de base de données Azure Cosmos | Documents Microsoft"
description: "En savoir plus sur la partie supérieure de hello cinq cas d’usage pour la base de données Azure Cosmos : contenu, la journalisation des événements, les données du catalogue, données de préférences utilisateur et Internet des objets (IoT) généré par l’utilisateur."
services: cosmos-db
author: mimig1
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: eca68a58-1a8c-4851-8cf8-6e4d2b889905
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: mimig
ms.openlocfilehash: 115a418e7b18d5033c4d7e64591bf302aea0190b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="common-azure-cosmos-db-use-cases"></a>Cas d’utilisation courants d’Azure Cosmos DB
Cet article présente plusieurs cas d’utilisation courants pour Azure Cosmos DB.  recommandations Hello dans cet article servent comme point de départ lorsque vous développez votre application avec la base de données Cosmos.   

Après avoir lu cet article, vous serez hello en mesure de tooanswer suivant questions : 

* Quelles sont les cas d’utilisation courants hello pour la base de données Azure Cosmos ?
* Quels sont les avantages de hello de l’utilisation de la base de données Azure Cosmos pour les applications de vente au détail ?
* Quels sont les avantages de hello de base de données Azure Cosmos comme magasin de données pour les systèmes Internet of Things (IoT) ?
* Quels sont les avantages de hello de l’utilisation de la base de données Azure Cosmos pour les applications web et mobiles ?

## <a name="introduction"></a>Introduction
[Azure Cosmos DB](../cosmos-db/introduction.md) est le service de base de données de Microsoft distribué à l’échelle mondiale. service Hello est conçue tooallow clients tooelastically (et de façon indépendante) l’échelle de débit et stockage entre plusieurs régions géographiques. Azure Cosmos DB est le premier service de base de données distribués internationalement hello dans hello marché aujourd'hui toooffer complète [contrats de niveau de service](https://azure.microsoft.com/support/legal/sla/cosmos-db/) estimer le débit, la latence, la disponibilité et la cohérence. 

projet de base de données Azure Cosmos Hello démarré en 2011 en tant que « Projet Florence » tooaddress développeur points faibles qui sont rencontrés par les grandes applications Internet à l’échelle à l’intérieur de Microsoft. En observant que ces problèmes ne sont pas les applications de tooMicrosoft unique, que nous avons décidé tooexternal généralement disponibles aux développeurs de la base de données Azure Cosmos toomake dans 2015 sous forme de hello de [Azure DocumentDB](https://azure.microsoft.com/blog/documentdb-moving-to-general-availability/). service de Hello sert omniprésente en interne au sein de Microsoft et est un des services de croître hello utilisées par les développeurs de Azure en externe. 

Azure Cosmos DB est une base de données multimodèle distribuée à l’échelle mondiale qui est utilisée dans un large éventail d’applications et de cas d’utilisation. Il s’agit d’un bon choix pour tout [sans](http://azure.com/serverless) application qui doit le temps de réponse de commande de milliseconde basse et tooscale rapidement et globalement. Elle prend en charge plusieurs modèles de données (clé-valeur, documents, graphiques et en colonnes) et de nombreuses API pour l’accès aux données, y compris [MongoDB](mongodb-introduction.md), [DocumentDB SQL](documentdb-introduction.md), [Gremlin](graph-introduction.md) et [Tables Azure](table-introduction.md) en mode natif et d’une manière extensible. 

Hello Voici certains attributs de base de données Azure Cosmos qui la rendent parfaitement adaptée aux applications hautes performances avec ambition globale.

* Azure Cosmos DB partitionne vos données en mode natif pour offrir une disponibilité et une évolutivité élevées. Ce service assure des garanties de disponibilité, de débit, de faible latence et de cohérence de 99,99 %.
* Azure Cosmos DB dispose d’un stockage SSD avec des temps de réponse de l’ordre des millisecondes à faible latence.
* La prise en charge par Azure Cosmos DB des niveaux de cohérence finale, de préfixe, de session et liée sans état offre un rapport coût-performances faible et une flexibilité totale. Aucun service de base de données n’offre autant de flexibilité qu’Azure Cosmos DB en matière de niveaux de cohérence. 
* Azure Cosmos DB possède un modèle de tarification flexible et adapté aux données qui mesure indépendamment le stockage et le débit.
* Modèle de débit réservés de DB Cosmos Azure vous permet de toothink en termes de nombre de lectures/écritures au lieu de processeur/mémoire/IOPs Hello matériel sous-jacent.
* Conception vous permet Azure Cosmos DB de dans que développer des volumes de demande toomassive hello ordre de codage de demandes par jour.

Ces attributs sont bénéfiques dans web, mobile, les jeux et applications IoT qui nécessitent un temps de réponse faibles et requièrent toohandle des quantités massives de lectures et écritures.

## <a name="iot-and-telematics"></a>IoT et télématique
Les cas d'utilisation IoT présentent généralement les mêmes schémas pour la réception, le traitement et le stockage des données.  Tout d’abord, ces systèmes doivent tooingest les pics de données à partir de différents paramètres régionaux, les capteurs de périphérique. Ensuite, ces systèmes de traitent et analyser des informations en temps réel de tooderive des données en continu. les données de salutation seront ensuite toocold d’archivage pour l’analytique de lot. Microsoft Azure propose des services enrichis applicables aux cas d’utilisation IoT, dont Azure Cosmos DB, Azure Event Hubs, Azure Stream Analytics, Azure Notification Hub, Azure Machine Learning, Azure HDInsight et PowerBI. 

![Architecture de référence IoT d’Azure Cosmos DB](./media/use-cases/iot.png)

Des paquets de données peuvent être reçus par Azure Event Hubs qui offre un débit d’ingestion de données élevé à faible latence. Données ingérées toobe traité pour obtenir un aperçu en temps réel peuvent être utilisé pour garantir que tooAzure Analytique de flux de données pour l’analytique en temps réel. Les données peuvent être chargées dans Azure Cosmos DB pour une interrogation ad hoc. Une fois les données de salutation sont chargées dans la base de données Azure Cosmos, les données de salutation sont prêt toobe interrogé. En outre, les nouvelles données et modifie les données tooexisting peuvent être lus sur les flux de modification. Flux de modification est un persistant, ajouter uniquement de journal qui stocke les modifications collections tooCosmos base de données dans un ordre séquentiel. Hello que toutes les données ou simplement de modifications toodata dans la base de données Azure Cosmos peut être utilisé en tant que données de référence dans le cadre de l’analytique en temps réel. En outre, données peuvent en outre être affinées et traitées par connexion tooHDInsight de données de base de données Azure Cosmos pour les travaux Pig, Hive ou mappage/réduction.  Données filtrées sont ensuite chargées tooAzure arrière Cosmos de base de données de création de rapports.   

Pour un exemple de solution IoT à l’aide de la base de données Azure Cosmos, EventHubs et Storm, consultez hello [dépôt d’exemples de storm hdinsight sur GitHub](https://github.com/hdinsight/hdinsight-storm-examples/).

Pour plus d’informations sur les offres Azure pour IoT, consultez [créer hello Internet of Things votre](http://www.microsoft.com/server-cloud/internet-of-things.aspx). 

## <a name="retail-and-marketing"></a>Ventes et marketing
Base de données Azure Cosmos est largement utilisé dans les plateformes de commerce électronique de Microsoft, qui exécutent Windows hello Store et XBox Live. Il est également utilisé dans le secteur de vente au détail hello pour stocker les données de catalogue et pour l’événement source dans les pipelines de traitement des commandes.

Les scénarios d’utilisation des données de catalogue impliquent le stockage et l’interrogation d’un ensemble d’attributs pour des entités telles que des personnes, des lieux et des produits. Les comptes d’utilisateurs, les catalogues de produits, les registres d’appareil IoT et les systèmes de facturation de matériaux sont des exemples de données de catalogue. Attributs de ces données peuvent varier et peuvent changer dans les spécifications de temps toofit application.

Prenons l’exemple d'un catalogue de produits pour un fournisseur de pièces détachées de voiture. Chaque partie peut avoir ses propres attributs dans Ajout toohello des attributs communs qui partagent de toutes les parties. En outre, les attributs pour une partie spécifique peuvent changer hello exercice lorsqu’un nouveau modèle est publié. Azure Cosmos DB prend en charge les schémas flexibles et les données hiérarchiques, ce qui en fait une solution idéale pour stocker les données d’un catalogue de produits.

![Architecture de référence d’un catalogue de vente Azure Cosmos DB](./media/use-cases/product-catalog.png)

Azure Cosmos DB est souvent utilisée pour l’événement d’approvisionnement toopower des architectures pilotés par des événements à l’aide de son [modifier le flux](change-feed.md) fonctionnalité. flux de changement de Hello fournit en aval microservices hello tooreliably de capacité et de façon incrémentielle en lecture insère et de mises à jour (par exemple, les événements de commande) sont tooan base de données Azure Cosmos. Cette fonctionnalité peut être exploitée tooprovide un événement permanent stocker en tant que message broker pour les événements de changement d’état et de lecteur ordre le traitement des flux de travail entre plusieurs microservices (qui peut être implémentée en tant que [fonctions Azure sans](http://azure.com/serverless)).

![Architecture de référence d’un pipeline de commande en cours Azure Cosmos DB](./media/use-cases/event-sourcing.png)

De plus, les données stockées dans Azure Cosmos DB peuvent être intégrées à HDInsight en vue d’une analyse de données volumineuses par le biais de tâches Apache Spark. Pour plus d’informations sur hello connecteur Spark pour la base de données Azure Cosmos, consultez [exécuter une tâche de Spark avec la base de données Cosmos et HDInsight](spark-connector.md).

## <a name="gaming"></a>Jeux
couche de base de données Hello est un composant essentiel d’applications de jeu. Les jeux modernes effectuer un traitement graphique sur les clients mobiles/console, mais s’appuient sur toodeliver de cloud hello personnalisé et un contenu personnalisé telles que les statistiques du jeu, l’intégration de médias sociaux et scores ajouterons. Souvent, des jeux requièrent des latences de millisecondes unique pour les lectures et écrit tooprovide une expérience dans le jeu mobilisation. Une base de données de jeu doit toobe rapide et être pics massive toohandle en mesure de taux de demandes pendant le lancement de jeu de nouveaux et des mises à jour de la fonctionnalité.

Azure Cosmos DB est utilisé par les jeux comme [hello parcours morts : terrestres l’homme non](https://azure.microsoft.com/blog/the-walking-dead-no-mans-land-game-soars-to-1-with-azure-documentdb/) par [jeux suivant](http://www.nextgames.com/), et [Halo 5 : gardiens](https://azure.microsoft.com/blog/how-halo-5-guardians-implemented-social-gameplay-using-azure-documentdb/). Base de données Azure Cosmos fournit suivant de hello avantages aux développeurs de toogame :

* Base de données Azure Cosmos permet toobe de performances à l’échelle vers le haut ou vers le bas de façon élastique. Cela permet de toohandle jeux mise à jour de profil et les statistiques de dizaines toomillions de joueurs simultanées par un seul appel d’API.
* Azure prend en charge de Cosmos DB milliseconde lit et écrit toohelp éviter les retards lors du jeu.
* L’indexation automatique d’Azure Cosmos DB permet le filtrage sur plusieurs propriétés différentes en temps réel, par exemple pour localiser les joueurs avec leur ID de joueur en interne, ou leur ID GameCenter, Facebook, Google, ou exécuter une requête basée sur l’appartenance du joueur à un groupe. Cela est possible sans générer d’indexation complexe, ni infrastructure de partitionnement.
* Les fonctionnalités sociale notamment les nouveaux messages dans le jeu, appartenances guild de lecteur, défis terminées, ajouterons des scores et graphiques sociaux sont tooimplement plus facile avec un schéma flexible.
* Azure DB Cosmos en tant qu’un managé platform-as-a-service (PaaS) le programme d’installation minimale et de tooallow de travail de gestion requis pour une itération rapide et réduire les temps toomarket.

![Architecture de référence de gaming Azure Cosmos DB](./media/use-cases/gaming.png)

## <a name="web-and-mobile-applications"></a>Applications web et mobiles
Azure Cosmos DB est couramment utilisé dans les applications web et mobiles, et ce service est bien adapté à la modélisation des interactions sociales, à l’intégration avec les services tiers et à la création d’expériences personnalisées riches. Hello Cosmos DB SDK peut être utilisé build riche applications iOS et Android à l’aide de hello populaires [Xamarin framework](mobile-apps-with-xamarin.md).  

### <a name="social-applications"></a>Applications des réseaux sociaux
Un cas d’usage courant pour la base de données Azure Cosmos est toostore et requête contenu généré par l’utilisateur (UGC) pour le web, d’applications mobiles et sociaux media. Les sessions de conversation, les tweets, les billets de blog, les évaluations et les commentaires sont des exemples de contenus générés par l’utilisateur. Souvent, hello UGC dans les applications de médias sociaux est un mélange de texte de forme libre, les propriétés, les balises et les relations qui ne sont pas limitées par structure rigide. Contenu tels que les conversations, les commentaires et les publications peuvent stockés dans la Cosmos BD sans nécessiter de transformations ou des couches de mappage objet complexe toorelational.  Propriétés de données peuvent être ajoutées ou modifiés facilement toomatch exigences que les développeurs itérer sur le code de l’application hello, donc promouvoir un développement rapide.  

Les applications qui s’intègrent avec les réseaux sociaux tiers doivent répondre toochanging schémas à partir de ces réseaux. Lorsque des données sont automatiquement indexées par défaut dans la base de données Cosmos, est prêt toobe interrogée à tout moment. Par conséquent, ces applications ont des projections de tooretrieve flexibilité hello conformément à leurs besoins respectifs.

La plupart des applications de réseaux sociaux hello s’exécutent à l’échelle mondiale et peuvent présenter des modèles d’utilisation imprévisibles. Une grande souplesse dans la mise à l’échelle de magasin de données hello est essentielle comme couche d’application hello s’adapte à la demande de toomatch d’utilisation.  Vous pouvez monter en charge en ajoutant des partitions de données supplémentaires sous un compte Cosmos DB.  De plus, vous pouvez également créer des comptes Cosmos DB supplémentaires dans plusieurs régions. Pour la disponibilité régionale du service Cosmos DB, consultez [Régions Azure](https://azure.microsoft.com/regions/#services).

![Architecture de référence des applications web Azure Cosmos DB](./media/use-cases/apps-with-global-reach.png)

### <a name="personalization"></a>Personnalisation
Aujourd’hui, la plupart des applications offrent des affichages et des expériences complexes. Il s’agit généralement dynamiques, à la restauration des préférences de toouser ou humeur et marque les besoins. Par conséquent, les applications doivent toobe en mesure de tooretrieve personnalisé paramètres toorender efficacement les éléments d’interface utilisateur et l’expérience rapidement. 

JSON, un format pris en charge par la base de données Cosmos, est un format efficace toorepresent UI mise en page de données tel qu’il n’est pas uniquement léger, mais également peut être facilement reconnu par JavaScript. Cosmos DB offre des niveaux de cohérence paramétrables qui permettent des lectures rapides avec des écritures à faible latence. Par conséquent, le stockage des données de mise en page de l’interface utilisateur, y compris les paramètres personnalisés comme documents JSON dans la base de données Cosmos est un moyen efficace de tooget ces données sur le câble de hello.

![Architecture de référence des applications web Azure Cosmos DB](./media/use-cases/personalization.png)

## <a name="next-steps"></a>Étapes suivantes
tooget a démarré avec la base de données Azure Cosmos, suivez notre [Démarrages rapides](create-documentdb-dotnet.md), qui vous guide dans la création d’un compte et la mise en route de la base de données Cosmos. 

Ou, si vous souhaitez que tooread plus d’informations sur les clients à l’aide de la base de données Cosmos, hello témoignages suivantes sont disponibles :

* [Jet.com](https://jet.com). Commerce électronique challenger yeux hello place supérieur, s’exécute sur le cloud de Microsoft hello, tire parti de Cosmos DB à une échelle globale.
* [Asos.com](http://www.asos.com/). Asos.com est une boutique de mode et beauté en ligne britannique. Ciblant principalement les jeunes adultes, Asos vend plus de 850 marques, ainsi que sa propre sélection de vêtements et accessoires.
* [Toyota](https://www.toyota.com/). Toyota Motor Corporation est un constructeur automobile japonais. Toyota a utilisé Cosmos DB dans le cadre d’une application IoT globale.
* [Citrix](https://customers.microsoft.com/story/citrix). Citrix développe une solution d’authentification unique à l’aide d’Azure Service Fabric et d’Azure Cosmos DB.
* [TEXA](https://customers.microsoft.com/story/texaspa) La solution IoT révolutionnaire de TEXA destinée aux propriétaires de véhicule permet d’économiser du temps, de l’argent, de l’essence, et même de sauver des vies.
* [Domino's Pizza](https://www.dominos.com). Domino's Pizza Inc. est une chaîne de pizzerias américaine.
* [Johnson Controls](http://www.johnsoncontrols.com). Johnson Controls est un leader technologique mondial qui propose ses solutions à une vaste clientèle de tous secteurs dans plus de 150 pays.
* [Microsoft Windows, Universal Store, Azure IoT Hub, Xbox Live et autres services Internet](https://azure.microsoft.com/blog/how-azure-documentdb-planet-scale-nosql-helps-run-microsoft-s-own-businesses/). Découvrez comment Microsoft crée des services hautement évolutifs à l’aide d’Azure Cosmos DB.
* [Équipe Microsoft en charge des données et des analyses](https://customers.microsoft.com/story/microsoftdataandanalytics). L’équipe Microsoft en charge des données et des analyses collecte un nombre impressionnant de données au niveau mondial avec Azure Cosmos DB.
* [Sulekha.com](https://customers.microsoft.com/story/sulekha-uses-azure-documentdb-to-connect-customers-and-businesses-across-india). Sulekha utilise la base de données Azure Cosmos tooconnect clients et les entreprises entre l’Inde.
* [NewOrbit](https://customers.microsoft.com/story/neworbit-takes-flight-with-azure-documentdb). NewOrbit prend de l’altitude avec Azure Cosmos DB.
* [Affinio](https://customers.microsoft.com/doclink/affinio-switches-from-aws-to-azure-documentdb-to-harness-social-data-at-scale). Affinio bascule de AWS tooAzure Cosmos DB tooharness des données sociales à grande échelle.
* [Next Games](https://azure.microsoft.com//blog/the-walking-dead-no-mans-land-game-soars-to-1-with-azure-documentdb/). Hello cannes mortes : soars de jeu non manuel de terrain trop #1 pris en charge par base de données Azure Cosmos.
* [Halo](https://azure.microsoft.com/blog/how-halo-5-guardians-implemented-social-gameplay-using-azure-documentdb/). Comment Halo 5 a mis en œuvre l’expérience de jeu de société avec Azure Cosmos DB.
* [Galerie Cortana Analytics](https://azure.microsoft.com/blog/cortana-analytics-gallery-a-scalable-community-site-built-on-azure-documentdb/). Galerie Cortana Analytics : un site communautaire évolutif basé sur Azure Cosmos DB.
* [Breeze](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=18602). L’intégrateur principal offre aux entreprises multinationales un aperçu global en quelques minutes avec les technologies de cloud flexibles.
* [News République](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=18639). Ajout d’intelligence toohello news tooprovide informations dont l’objet des citoyens occasion. 
* [SGS International](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=18653). Pour la couleur cohérent monde hello, marques principales activer tooSGS. Et tooAzure Active les groupes de stockage.
* [Telenor](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=18608). Mondial Telenor utilise hello cloud toomove doté d’une vitesse d’un démarrage hello. 
* [XOMNI](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=18667). magasin de Hello de futures exécutions de hello sur rapide recherche et hello facile de flux de données.
* [Nucleo](https://customers.microsoft.com/story/azure-based-software-platform-breaks-down-barriers-bet). Plateforme logicielle basée sur Azure, qui élimine les barrières entre les entreprises et les clients
* [Weka](https://customers.microsoft.com/story/weka-smart-fridge-improves-vaccine-management-so-more-people-can-be-protected-against-diseases). Weka Smart Fridge améliore la gestion des vaccins, ce qui permet de protéger davantage de personnes contre les maladies
* [Orange Tribes](https://customers.microsoft.com/story/theres-more-to-that-food-app-than-meets-the-eye-or-the-mouth). Il est plus d’application de produits alimentaires toothat que répond aux yeux de hello ou bouche de hello.
* [Real Madrid](https://customers.microsoft.com/story/real-madrid-brings-the-stadium-closer-to-450-million-f). Real Madrid met hello stade proche too450 millions ventilateurs monde hello avec hello Cloud Microsoft.
* [Tuku](https://customers.microsoft.com/story/tuku-makes-car-buying-fun-with-help-from-azure-services). Avec les services Azure, il est très amusant d’acheter une voiture sur TUKU
