---
title: "Introduction tooAzure Cosmos DB : API pour MongoDB | Documents Microsoft"
description: "Découvrez comment vous pouvez utiliser la base de données Azure Cosmos toostore et les volumes de gros volumes de requêtes de documents JSON avec une latence faible à l’aide hello populaires OSS MongoDB APIs."
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
ms.openlocfilehash: 1eb88014cc4809332e3f5c109a44a55814194934
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-cosmos-db-api-for-mongodb"></a>Introduction tooAzure Cosmos DB : API pour MongoDB

[Azure Cosmos DB](../cosmos-db/introduction.md) est le service de base de données multi-modèle de Microsoft distribué à l’échelle mondiale pour les applications stratégiques. Fournit de la base de données Azure Cosmos [distribution globale des clés en main](distribute-data-globally.md), [mise à l’échelle élastique de débit et de stockage](partition-data.md) des latences de milliseconde dans le monde entier, à un chiffre à 99e centile de hello, [cinq niveaux de cohérence bien définis](consistency-levels.md)et la garantie de haute disponibilité, bénéficient toutes [pointe SLA](https://azure.microsoft.com/support/legal/sla/cosmos-db/). Base de données Azure Cosmos [automatiquement les données d’index](http://www.vldb.org/pvldb/vol8/p1668-shukla.pdf) sans avoir toodeal avec la gestion de schéma et d’index. Il est multi-modèle et prend en charge les modèles de données en colonnes, documents, graphiques et clé-valeur. 

![Azure Cosmos DB : API MongoDB](./media/mongodb-introduction/cosmosdb-mongodb.png) 

Bases de données de COSMOS DB peuvent être utilisées en tant que banque de données hello pour les applications écrites pour [MongoDB](https://docs.mongodb.com/manual/introduction/). Cela signifie qu’en utilisant les [pilotes](https://docs.mongodb.org/ecosystem/drivers/), votre application écrite pour MongoDB peut désormais communiquer avec Cosmos DB et utiliser des bases de données Cosmos DB au lieu de bases de données MongoDB. Dans de nombreux cas, vous pouvez basculer de l’utilisation de MongoDB tooCosmos DB en modifiant simplement une chaîne de connexion. À l’aide de cette fonctionnalité, vous pouvez facilement créer et exécuter des applications de base de données MongoDB Bonjour Azure cloud avec la distribution globale d’Azure Cosmos DB et [SLA de pointe complète](https://azure.microsoft.com/support/legal/sla/cosmos-db), tout en continuant toouse familier compétences et outils pour MongoDB.


## <a name="what-is-hello-benefit-of-using-azure-cosmos-db-for-mongodb-applications"></a>Quels sont les avantages de hello de l’utilisation de la base de données Azure Cosmos pour MongoDB applications ?

**Débit de façon élastique évolutif et de stockage :** faire évoluer ou vers le bas de votre toomeet de la base de données MongoDB votre application a besoin. Vos données sont stockées sur des disques SSD (SSD) pour garantir une faible latence de manière prévisible. COSMOS DB prend en charge les collections de MongoDB pouvant prendre en charge les toovirtually les tailles de stockage illimité et débit approvisionné. Vous pouvez mettre à l’échelle Cosmos DB de manière flexible et transparente avec des performances prévisibles à mesure que votre application se développe. 

**Réplication de plusieurs région :** Cosmos DB réplique en toute transparence vos tooall les régions de données vous avez associé votre compte MongoDB, ce qui vous toodevelop les applications qui requièrent l’accès global toodata tout en offrant un compromis la cohérence et les performances, tout avec les garanties correspondantes. COSMOS DB fournit un basculement transparent régional avec hébergement multiple d’API et de débit de l’échelle tooelastically hello capacité et de stockage monde hello. Pour en savoir plus, consultez [Distribution mondiale des données avec DocumentDB](distribute-data-globally.md).

**Compatibilité de MongoDB** : vous pouvez utiliser votre expertise, votre code d’application et vos outils MongoDB existants. Vous pouvez développer des applications à l’aide de MongoDB et déployez-les tooproduction à l’aide de hello entièrement gérés distribués internationalement Cosmos DB service.

**Aucune gestion de serveur**: vous n’avez toomanage et mettre à l’échelle de vos bases de données MongoDB. COSMOS DB est un service entièrement géré, ce qui signifie que vous n’avez pas toomanage d’infrastructure ni d’ordinateurs virtuels vous-même. Cosmos DB est disponible dans plus de 30 [régions Azure](https://azure.microsoft.com/regions/services/).

**Niveaux de cohérence analysables :** Select à partir de cinq bien définie cohérence niveaux tooachieve compromis optimal se situe entre la cohérence et performances. Pour les requêtes et les opérations de lecture, Cosmos DB propose cinq niveaux de cohérence distincts : Fort, Obsolescence limitée, Session, Préfixe cohérent et Éventuel. Ces niveaux de cohérence granulaire et bien définie autorise toomake son compromis entre la cohérence, la disponibilité et la latence. Pour en savoir plus [à l’aide de la cohérence des niveaux de performances et la disponibilité de toomaximize](consistency-levels.md).

**L’indexation automatique**: par défaut, Cosmos DB automatiquement indexe toutes les propriétés de hello dans les documents dans votre base de données MongoDB et ne pas attendre ou exiger n’importe quel schéma ou la création d’index secondaire.

**Échelle de l’entreprise** -base de données Azure Cosmos prend en charge plusieurs réplicas locaux toodeliver 99,99 % disponibilité et protection des données en face de hello d’échecs locaux et régionaux. Azure Cosmos DB offre des [certifications de conformité](https://www.microsoft.com/trustcenter) et des fonctionnalités de sécurité de qualité professionnelle. 

Apprenez en plus grâce à cette vidéo Azure Friday avec Scott Hanselman et Kirill Gavrylyuk, responsable principal de l’ingénierie Azure Cosmos DB.

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Introducing-Azure-Cosmos-DB/player]
> 

## <a name="how-tooget-started"></a>Mode de démarrage tooget

Suivez hello MongoDB Démarrages rapides toocreate un compte de base de données Cosmos et migrer votre toouse d’application existant Mongodb Cosmos DB ou générer un nouveau :

* [Migrer une application web MongoDB Node.js existante](create-mongodb-nodejs.md)
* [Créer une application web de MongoDB API .NET et hello portail Azure](create-mongodb-dotnet.md)
* [Créer une application de console MongoDB API avec Java et hello portail Azure](create-mongodb-java.md)

## <a name="next-steps"></a>Étapes suivantes

Plus d’informations sur les API de MongoDB Azure Cosmos DB sont intégrés à hello documentation de Cosmos global Azure DB, mais il existe quelques pointeurs tooget commencer :

* Suivez hello [tooa MongoDB compte de connexion](connect-mongodb-account.md) toolearn didacticiel comment tooget vos informations de chaîne de connexion de compte.
* Suivez hello [MongoChef d’utilisation avec la base de données Azure Cosmos](mongodb-mongochef.md) toolearn didacticiel comment toocreate une connexion entre votre base de données de la base de données Azure Cosmos et l’application MongoDB dans MongoChef.
* Suivez hello [migrer des données tooAzure Cosmos DB avec prise en charge de protocole pour MongoDB](mongodb-migrate.md) tooimport didacticiel votre tooan données API de base de données MongoDB.
* API tooan MongoDB compte à l’aide de connecter [Robomongo](mongodb-robomongo.md).
* Découvrez combien RUs sont à l’aide de vos opérations avec hello [GetLastRequestStatistics des commandes et hello métriques portail Azure](request-units.md#GetLastRequestStatistics).
* Découvrez comment trop[configurer les préférences de lecture pour les applications distribuées globalement](../cosmos-db/tutorial-global-distribution-mongodb.md).
