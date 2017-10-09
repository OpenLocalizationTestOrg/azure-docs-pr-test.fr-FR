---
title: "Azure Cosmos DB : API DocumentDB | Microsoft Docs"
description: "Découvrez comment vous pouvez utiliser la base de données Azure Cosmos toostore requête massives volumes de documents JSON avec une faible latence à l’aide de SQL et JavaScript."
keywords: "base de données JSON, base de données Document"
services: cosmos-db
author: mimig1
manager: jhubbard
editor: monicar
documentationcenter: 
ms.assetid: 686cdd2b-704a-4488-921e-8eefb70d5c63
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/22/2017
ms.author: mimig
ms.openlocfilehash: c96dfa5e2685782a99d2bcaf992f88dd2bef920b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-cosmos-db-documentdb-api"></a>Introduction tooAzure Cosmos DB : API DocumentDB

[Azure Cosmos DB](introduction.md) est le service de base de données multi-modèle de Microsoft distribué à l’échelle mondiale pour les applications stratégiques. Fournit de la base de données Azure Cosmos [distribution globale des clés en main](distribute-data-globally.md), [mise à l’échelle élastique de débit et de stockage](partition-data.md) des latences de milliseconde dans le monde entier, à un chiffre à 99e centile de hello, [cinq niveaux de cohérence bien définis](consistency-levels.md)et la garantie de haute disponibilité, bénéficient toutes [pointe SLA](https://azure.microsoft.com/support/legal/sla/cosmos-db/). Base de données Azure Cosmos [automatiquement les données d’index](http://www.vldb.org/pvldb/vol8/p1668-shukla.pdf) sans avoir toodeal avec la gestion de schéma et d’index. Il est multi-modèle et prend en charge les modèles de données en colonnes, documents, graphiques et clé-valeur. 

![API Azure DocumentDB](./media/documentdb-introduction/cosmosdb-documentdb.png) 

With hello API DocumentDB, base de données Azure Cosmos fournit un riche et familière [des fonctions de requête SQL](documentdb-sql-query.md) avec des latences de faibles cohérence sur des données JSON sans schéma. Dans cet article, nous fournissent une vue d’ensemble de hello Azure Cosmos DB API DocumentDB, et comment vous pouvez l’utiliser toostore des volumes importants de données JSON, les requêtes dans l’ordre de la latence en millisecondes et évoluer facilement des schémas de hello. 

## <a name="what-capabilities-and-key-features-does-azure-cosmos-db-offer"></a>Quelles fonctionnalités et caractéristiques clés sont offertes par Azure Cosmos DB ?
Azure DB Cosmos, via hello API DocumentDB, offre hello suivant les avantages et les fonctionnalités clées :

* **Débit de façon élastique évolutif et de stockage :** facilement monter ou à l’échelle votre toomeet de la base de données JSON votre application a besoin. Vos données sont stockées sur des disques SSD (SSD) pour garantir une faible latence de manière prévisible. Base de données Azure Cosmos prend en charge les conteneurs pour le stockage des données JSON appelé regroupements qui peuvent mettre à l’échelle toovirtually les tailles de stockage illimité et débit approvisionné. Vous pouvez mettre à l’échelle Azure Cosmos DB de manière flexible et transparente avec des performances prévisibles à mesure que votre application se développe. 


* **Réplication de plusieurs région :** base de données Azure Cosmos réplique en toute transparence vos tooall les régions de données vous avez associé votre compte de base de données Azure Cosmos, ce qui vous toodevelop les applications qui nécessitent l’accès global toodata tout en offrant compromis entre la cohérence, la disponibilité et performances, toutes les données avec les garanties correspondants. Base de données Cosmos Azure fournit un basculement régional transparent avec hébergement multiple d’API et de débit de l’échelle tooelastically hello capacité et de stockage monde hello. Pour en savoir plus, consultez [Azure Cosmos DB, un service de base de données mondialement distribué sur Azure](distribute-data-globally.md).

* **Requêtes ad hoc à l’aide de la syntaxe SQL familière :** stockez des documents JSON hétérogènes et interrogez-les via la syntaxe SQL. Base de données Azure Cosmos utilise un verrou de simultanéité, libre, journal structuré d’indexation index tooautomatically de technologie tout contenu de document. Cela permet des requêtes riches en temps réel sans indicateurs de schéma toospecify hello besoin, des index secondaires ou des vues. Pour en savoir plus, consultez [Requête SQL et syntaxe SQL dans Azure Cosmos DB](documentdb-sql-query.md). 
* **Exécution du code JavaScript au sein de la base de données hello :** Express logique d’application en tant que procédures stockées, déclencheurs et les fonctions définies par l’utilisateur (UDF) à l’aide de JavaScript standard. Ainsi, votre toooperate de logique d’application sur des données sans vous soucier d’incompatibilité hello entre l’application hello et schéma de base de données hello. Hello API DocumentDB fournit transactionnelle complète d’exécution de la logique d’application JavaScript directement à l’intérieur du moteur de base de données hello. intégration en profondeur Hello JavaScript permet l’exécution à la hello de INSERT, REPLACE, DELETE et des opérations SELECT à partir d’un programme JavaScript comme une transaction isolée. Pour plus d’informations, consultez la rubrique [Programmation côté serveur dans DocumentDB](programming.md).

* **Niveaux de cohérence analysables :** Select à partir de cinq bien définie cohérence niveaux tooachieve compromis optimal se situe entre la cohérence et performances. Pour les requêtes et les opérations de lecture, Azure Cosmos DB propose cinq niveaux de cohérence distincts : Fort, En fonction de l’obsolescence, Par session, Préfixe cohérent et Éventuel. Ces niveaux de cohérence granulaire et bien définie autorise toomake son compromis entre la cohérence, la disponibilité et la latence. Pour en savoir plus [à l’aide de la cohérence des niveaux de performances et la disponibilité de toomaximize](consistency-levels.md).

* **Entièrement géré :** éliminer hello besoin toomanage de base de données et ordinateur ressources. Comme un service entièrement géré de Microsoft Azure, vous effectuez pas besoin de toomanage virtuels, déployez et configurez les logiciels, gérez la mise à l’échelle ou traiter les mises à niveau de la couche de données complexes. Chaque base de données est automatiquement sauvegardée et protégée contre les défaillances régionales. Vous pouvez facilement ajouter un compte de base de données Azure Cosmos et allouer des capacités que vous le souhaitez, ce qui vous toofocus sur votre application au lieu d’exploitation et la gestion de votre base de données. 

* **Conception ouverte :** Démarrez rapidement à l’aide de compétences et d’outils existants. Programmer hello API DocumentDB est simple et conviviale et ne requiert pas vous tooadopt de nouveaux outils ou conforme toocustom extensions tooJSON ou JavaScript. Vous pouvez accéder à toutes les fonctionnalités de base de données hello notamment CRUD, requête et JavaScript, le traitement via une simple interface RESTful HTTP. Hello API DocumentDB prend en compte les formats existants, des langages et des normes tout en offrant des fonctionnalités de base de données sur les valeur élevée.

* **L’indexation automatique :** par défaut, Azure Cosmos DB automatiquement tous les documents hello dans la base de données hello d’index et ne pas attendre ou nécessitent de n’importe quel schéma ou la création d’index secondaire. Ne voulez pas tooindex tous les éléments ? Ne vous inquiétez pas, vous pouvez aussi [refuser des chemins d’accès dans vos fichiers JSON](indexing-policies.md) .

* **Prise en charge de flux de modification :** flux de modification fournit une liste triée de documents dans une collection de base de données Azure Cosmos dans l’ordre de hello dans lequel ils ont été modifiés. Ce flux peut être toolisten utilisé pour toodata des modifications dans les données de commande tooreplicate, déclencher des appels d’API ou réaliser un traitement de flux de données des mises à jour. Flux de modification est automatiquement activé et facile toouse : [en savoir plus sur Modifier le flux](https://docs.microsoft.com/azure/cosmos-db/change-feed). 

## <a name="data-management"></a>Comment gérer les données avec hello API DocumentDB ?
Hello API DocumentDB vous permet de gérer les données JSON via des ressources de base de données bien défini. Ces ressources sont répliquées à des fins de haute disponibilité et adressables de manière unique via leur URI logique. Hello API DocumentDB offre qu'un HTTP simple en fonction d’un modèle de programmation RESTful pour toutes les ressources. 


compte de base de données de base de données Azure Cosmos Hello est un espace de noms unique qui vous donne accès tooAzure Cosmos DB. Avant de pouvoir créer un compte de base de données, vous devez disposer d’un abonnement Azure, ce qui permet d’accéder à divers services Azure tooa. 

Toutes les ressources au sein d’Azure Cosmos DB sont modélisées et stockées en tant que documents JSON. Les ressources sont gérées en tant qu'éléments (documents JSON contenant des métadonnées) et en tant que flux (collections d'éléments). Les ensembles d'éléments sont contenus dans leurs flux respectifs.

image Hello ci-dessous montre les relations entre les ressources de base de données Azure Cosmos hello hello :

![relation hiérarchique de Hello entre les ressources dans la base de données Azure Cosmos][1] 

Un compte de base de données est constitué d'un ensemble de bases de données. Chacune d'elles contient plusieurs collections, lesquelles comportent des procédures stockées, des déclencheurs, des fonctions définies par l'utilisateur, des documents et les pièces jointes associées. Une base de données a également associée aux utilisateurs, chacun avec un jeu d’autorisations tooaccess divers autres regroupements, des procédures stockées, déclencheurs, UDF, des documents ou des pièces jointes. Les bases de données, les utilisateurs, les autorisations et les collections sont des ressources définies par le système avec des schémas connus, tandis que les documents, les procédures stockées, les fonctions définies par l'utilisateur et les pièces jointes comportent un contenu JSON arbitraire défini par l'utilisateur.  

> [!NOTE]
> Étant donné que hello API DocumentDB était précédemment disponible en tant que hello Azure DocumentDB service, vous pouvez continuer tooprovision, surveiller et gérer des comptes créés via hello API REST de gestion des ressources Azure ou à l’aide des outils hello Azure DocumentDB ou base de données Azure Cosmos noms de ressources. Nous utilisons des noms de hello indifféremment lorsque vous faites référence toohello Azure DocumentDB APIs. 

## <a name="develop"></a>Comment puis-je développer des applications avec hello API DocumentDB ?

Base de données Azure Cosmos expose des ressources via hello API REST qui peut être appelée par n’importe quel langage capable d’effectuer des demandes HTTP/HTTPS. En outre, nous proposons des bibliothèques de programmation pour plusieurs langues courantes pour hello API DocumentDB. les bibliothèques clientes Hello simplifient de nombreux aspects de l’utilisation des API de hello en gérant des détails tels que la mise en cache d’une adresse, gestion des exceptions, nouvelles tentatives automatiques, etc.. Les bibliothèques sont actuellement disponibles pour hello suivant langues et plateformes :  

| Télécharger | Documentation |
| --- | --- |
| [KIT DE DÉVELOPPEMENT LOGICIEL (SDK) .NET](http://go.microsoft.com/fwlink/?LinkID=402989) |[Bibliothèque .NET](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet) |
| [Kit de développement logiciel (SDK) Node.js](http://go.microsoft.com/fwlink/?LinkID=402990) |[Bibliothèque Node.js](http://azure.github.io/azure-documentdb-node/) |
| [Kit de développement logiciel (SDK) Java](http://go.microsoft.com/fwlink/?LinkID=402380) |[Bibliothèque Java](/java/api/com.microsoft.azure.documentdb) |
| [Kit de développement logiciel (SDK) JavaScript](http://go.microsoft.com/fwlink/?LinkID=402991) |[Bibliothèque JavaScript](http://azure.github.io/azure-documentdb-js/) |
| n/a |[Kit de développement logiciel (SDK) JavaScript côté serveur](http://azure.github.io/azure-documentdb-js-server/) |
| [Kit de développement logiciel (SDK) Python](https://pypi.python.org/pypi/pydocumentdb) |[Bibliothèque Python](http://azure.github.io/azure-documentdb-python/) |
| n/a | [API pour MongoDB](mongodb-introduction.md)


À l’aide de hello [Azure Cosmos DB émulateur](local-emulator.md), vous pouvez développer et tester votre application localement avec hello API DocumentDB, sans création d’un abonnement Azure ou d’encourir les coûts. Lorsque vous êtes satisfait du fonctionne de votre application dans l’émulateur de hello, vous pouvez basculer toousing un compte de base de données Azure Cosmos dans le cloud de hello.

Au-delà de la base créer, lire, mettre à jour et supprimer des opérations, hello API DocumentDB fournit une interface de requête SQL riche pour la récupération de documents JSON et prise en charge du côté serveur pour l’exécution transactionnelle de logique d’application JavaScript. interfaces de l’exécution de requêtes et de script Hello sont disponibles dans toutes les bibliothèques de plateforme ainsi que les API REST de hello. 

### <a name="sql-query"></a>Requête SQL
prend en charge de l’API DocumentDB Hello interrogation de documents JavaScript à l’aide d’un langage SQL, qui est associé à une racine Bonjour type système et des expressions avec prise en charge pour les requêtes relationnelles et hiérarchiques spatiales. langage de requête DocumentDB Hello est un simple et puissante interface tooquery JSON les documents. langue de Hello prend en charge un sous-ensemble de la grammaire SQL ANSI et ajoute l’intégration en profondeur de l’objet JavaScript, tableaux, construction d’objet et l’appel de fonction. Hello API DocumentDB fournit son modèle de requête sans indicateurs d’indexation ou de n’importe quel schéma explicite du développeur de hello.

Fonctions de définies par l’utilisateur (UDF) peuvent être inscrites avec hello API DocumentDB et référencées dans le cadre d’une requête SQL, étendant par conséquent la logique d’application personnalisée hello grammaire toosupport. Ces fonctions UDF sont écrites en tant que programmes JavaScript et exécutés au sein de la base de données hello. 

Pour les développeurs .NET, hello API DocumentDB [.NET SDK](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.linq.aspx) offre également un fournisseur de requête LINQ. 

### <a name="transactions-and-javascript-execution"></a>Transactions et exécution JavaScript
Hello API DocumentDB vous permet de toowrite la logique d’application en tant que programmes nommés entièrement écrits dans JavaScript. Ces programmes sont enregistrées pour une collection et peuvent émettre des opérations de base de données sur des documents de hello au sein d’une collection donnée. JavaScript peut être inscrit à des fins d'exécution en tant que déclencheur, procédure stockée ou fonction définie par l'utilisateur. Déclencheurs et procédures stockées peuvent créer, lire, mettre à jour et supprimer des documents tandis que les fonctions définies par l’utilisateur qui s’exécutent dans le cadre de la logique d’exécution de requête hello sans accès en écriture toohello collection.

Exécution du code JavaScript dans hello Cosmos DB est modélisée d’après les concepts hello pris en charge par les systèmes de base de données relationnelle avec JavaScript sous la forme d’un remplacement modern pour Transact-SQL. Toute la logique JavaScript est exécutée dans une transaction ACID ambiante avec isolement de capture instantanée. Pendant son exécution, hello si hello JavaScript lève une exception, hello puis la totalité de la transaction est abandonnée.

## <a name="are-there-any-online-courses-on-azure-cosmos-db"></a>Y a-t-il des formations en ligne sur Azure Cosmos DB ?

Oui, il y a une formation [Microsoft Virtual Academy](https://mva.microsoft.com/en-US/training-courses/azure-documentdb-planetscale-nosql-16847) cours sur Azure DocumentDB. 

>[!VIDEO https://mva.microsoft.com/en-US/training-courses-embed/azure-documentdb-planetscale-nosql-16847]
>
>

## <a name="next-steps"></a>Étapes suivantes
Vous disposez déjà d’un compte Azure ? Vous pouvez donc découvrir Azure Cosmos DB en suivant nos [démarrages rapides](../cosmos-db/create-documentdb-dotnet.md), qui vous guideront pour créer un compte et prendre en main Cosmos DB.

[1]: ./media/documentdb-introduction/json-database-resources1.png

