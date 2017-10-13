---
title: "Introduction à Azure Cosmos DB : API pour MongoDB | Microsoft Docs"
description: "Découvrez comment vous pouvez utiliser Azure Cosmos DB pour stocker et interroger d’immenses volumes de requêtes de documents JSON avec une faible latence, à l’aide des API MongoDB OSS populaires."
keywords: "qu’est-ce que MongoDB"
services: cosmos-db
author: AndrewHoh
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: 4afaf40d-c560-42e0-83b4-a64d94671f0a
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: anhoh
ms.openlocfilehash: 4dbf91a3c1d6a287d7337647f9e059566c7ddbe5
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="introduction-to-azure-cosmos-db-api-for-mongodb"></a>Introduction à Azure Cosmos DB : API pour MongoDB

[Azure Cosmos DB](../cosmos-db/introduction.md) est le service de base de données multimodèle de Microsoft distribué à l’échelle mondiale pour les applications stratégiques. Azure Cosmos DB fournit la [distribution mondiale clés en main](distribute-data-globally.md), la [mise à l’échelle élastique du débit et du stockage](partition-data.md), des latences de l’ordre de quelques millisecondes dans le monde entier dans plus de 99 pour cent des cas, [cinq niveaux de cohérence bien définis](consistency-levels.md) et une garantie d’une haute disponibilité, le tout soutenu par nos [contrats SLA de pointe](https://azure.microsoft.com/support/legal/sla/cosmos-db/). Azure Cosmos DB [indexe automatiquement les données](http://www.vldb.org/pvldb/vol8/p1668-shukla.pdf) sans avoir à s’occuper de la gestion des schémas et des index. Il est multi-modèle et prend en charge les modèles de données en colonnes, documents, graphes et clé-valeur. 

![Azure Cosmos DB : API MongoDB](./media/mongodb-introduction/cosmosdb-mongodb.png) 

Les bases de données Cosmos DB peuvent être utilisées comme magasin de données pour les applications écrites pour [MongoDB](https://docs.mongodb.com/manual/introduction/). Cela signifie qu’en utilisant les [pilotes](https://docs.mongodb.org/ecosystem/drivers/), votre application écrite pour MongoDB peut désormais communiquer avec Cosmos DB et utiliser des bases de données Cosmos DB au lieu de bases de données MongoDB. Dans de nombreux cas, vous pouvez passer de MongoDB à Cosmos DB en modifiant simplement une chaîne de connexion. Cette fonctionnalité vous permet de générer et d’exécuter facilement des applications de base de données MongoDB dans le cloud Azure avec la distribution mondiale et les [contrats SLA de pointe](https://azure.microsoft.com/support/legal/sla/cosmos-db) d’Azure Cosmos DB, tout en continuant à exploiter leurs outils et compétences existants pour MongoDB.


## <a name="what-is-the-benefit-of-using-azure-cosmos-db-for-mongodb-applications"></a>Quel avantage pouvez-vous tirer en utilisant Azure Cosmos DB pour les applications MongoDB ?

**Débit et stockage évolutifs avec flexibilité :** augmentez ou réduisez facilement la taille de votre base de données MongoDB pour répondre aux besoins de votre application. Vos données sont stockées sur des disques SSD (SSD) pour garantir une faible latence de manière prévisible. Cosmos DB prend en charge des collections MongoDB qui peuvent être mises à l’échelle pour atteindre des tailles de stockage quasi illimitées et un débit configuré. Vous pouvez mettre à l’échelle Cosmos DB de manière flexible et transparente avec des performances prévisibles à mesure que votre application se développe. 

**Réplication dans plusieurs régions :** Cosmos DB réplique en toute transparence vos données dans toutes les régions associées à votre compte MongoDB, ce qui vous permet de développer des applications qui requièrent l’accès global aux données tout en offrant un compromis entre cohérence, disponibilité et performances, le tout avec les garanties correspondantes. Cosmos DB fournit un basculement régional transparent avec les API multihébergement et la possibilité de mettre à l’échelle de manière élastique le débit et le stockage dans le monde entier. Pour en savoir plus, consultez [Distribution mondiale des données avec DocumentDB](distribute-data-globally.md).

**Compatibilité de MongoDB** : vous pouvez utiliser votre expertise, votre code d’application et vos outils MongoDB existants. Vous pouvez développer des applications à l’aide de MongoDB et les déployer en production avec le service Cosmos DB entièrement géré et distribué à l’échelle mondiale.

**Aucune gestion de serveur** : vous n’avez pas à vous soucier de la gestion et de la mise à l’échelle de vos bases de données MongoDB. Cosmos DB est un service entièrement géré, ce qui signifie que vous n’avez pas d’infrastructure ou de machines virtuelles à gérer. Cosmos DB est disponible dans plus de 30 [régions Azure](https://azure.microsoft.com/regions/services/).

**Niveaux de cohérence ajustables :** choisissez entre cinq niveaux de cohérence bien définis pour obtenir un équilibre optimal entre cohérence et performances. Pour les requêtes et les opérations de lecture, Cosmos DB propose cinq niveaux de cohérence distincts : Fort, Obsolescence limitée, Session, Préfixe cohérent et Éventuel. Ces niveaux de cohérence bien définis et granulaires vous permettent de trouver un bon compromis entre cohérence, disponibilité et latence. Pour en savoir plus, consultez [Niveaux de cohérence des données analysables dans Azure Cosmos DB](consistency-levels.md).

**Indexation automatique :** par défaut, Cosmos DB indexe automatiquement toutes les propriétés des documents de votre base de données MongoDB et n’attend pas et ne nécessite aucun schéma ou création d’index secondaires.

**Qualité professionnelle** : Azure Cosmos DB prend en charge plusieurs réplicas locaux pour fournir une disponibilité de 99,99 % et une protection des données en cas de défaillances locales et régionales. Azure Cosmos DB offre des [certifications de conformité](https://www.microsoft.com/trustcenter) et des fonctionnalités de sécurité de qualité professionnelle. 

Apprenez en plus grâce à cette vidéo Azure Friday avec Scott Hanselman et Kirill Gavrylyuk, responsable principal de l’ingénierie Azure Cosmos DB.

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Introducing-Azure-Cosmos-DB/player]
> 

## <a name="how-to-get-started"></a>Pour commencer

Suivez les démarrages rapides de MongoDB pour créer un compte Cosmos DB et migrer votre application Mongo DB existante afin d’utiliser Cosmos DB ou en générer une nouvelle :

* [Migrer une application web MongoDB Node.js existante](create-mongodb-nodejs.md)
* [Développer une application web API MongoDB avec .NET et le Portail Azure](create-mongodb-dotnet.md)
* [Développer une application console API MongoDB avec Java et le Portail Azure](create-mongodb-java.md)

## <a name="next-steps"></a>Étapes suivantes

Des informations sur l’API MongoDB d’Azure Cosmos DB sont intégrées dans l’ensemble de la documentation Azure Cosmos DB, mais voici quelques points qui vous aideront à démarrer :

* Pour savoir comment obtenir les informations de chaîne de connexion de votre compte, suivez le didacticiel [Se connecter à un compte MongoDB](connect-mongodb-account.md).
* Pour savoir comment créer une connexion entre votre base de données Azure Cosmos DB et l’application MongoDB dans MongoChef, suivez le didacticiel [Utiliser MongoChef avec un compte Azure Cosmos DB : API pour MongoDB](mongodb-mongochef.md).
* Suivez le didacticiel [Migrer des données vers Azure Cosmos DB à l’aide de mongoimport et mongorestore](mongodb-migrate.md) pour importer vos données dans une API de base de données MongoDB.
* Établissez une connexion à une API de compte MongoDB à l’aide de [Robomongo](mongodb-robomongo.md).
* Découvrez combien d’unités de requête sont utilisées par vos opérations avec la commande [GetLastRequestStatistics et des mesures du portail Azure](request-units.md#GetLastRequestStatistics).
* Découvrez comment [configurer des préférences de lecture pour les applications distribuées dans le monde entier](../cosmos-db/tutorial-global-distribution-mongodb.md).
