---
title: API de Table de DB Cosmos aaaIntroduction tooAzure | Documents Microsoft
description: "Découvrez comment vous pouvez utiliser la base de données Azure Cosmos toostore et les volumes de requêtes massives de données de clé-valeur avec une latence faible à l’aide hello populaires OSS MongoDB APIs."
services: cosmos-db
author: bhanupr
manager: jhubbard
editor: monicar
documentationcenter: 
ms.assetid: 
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/25/2017
ms.author: arramac
ms.openlocfilehash: 4c5678898a772808f4bcd1465a23d436b0f8fc0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-cosmos-db-table-api"></a>Introduction tooAzure Cosmos DB : API de Table

[Azure Cosmos DB](introduction.md) est le service de base de données multi-modèle de Microsoft distribué à l’échelle mondiale pour les applications stratégiques. Fournit de la base de données Azure Cosmos [distribution globale des clés en main](distribute-data-globally.md), [mise à l’échelle élastique de débit et de stockage](partition-data.md) des latences de milliseconde dans le monde entier, à un chiffre à 99e centile de hello, [cinq niveaux de cohérence bien définis](consistency-levels.md)et la garantie de haute disponibilité, bénéficient toutes [pointe SLA](https://azure.microsoft.com/support/legal/sla/cosmos-db/). Base de données Azure Cosmos [automatiquement les données d’index](http://www.vldb.org/pvldb/vol8/p1668-shukla.pdf) sans avoir toodeal avec la gestion de schéma et d’index. Il est multi-modèle et prend en charge les modèles de données en colonnes, documents, graphiques et clé-valeur. 

![API de stockage de table Azure et Azure Cosmos DB](./media/table-introduction/premium-tables.png) 

Base de données Azure Cosmos fournit hello API (version préliminaire) de la Table pour les applications qui ont besoin d’un magasin clé-valeur avec schéma flexible, des performances prévisibles, distribution globale et un débit élevé. Hello Table API fournit hello mêmes fonctionnalités que le stockage de Table Azure, mais tire parti des avantages de hello du moteur de base de données Azure Cosmos hello. 

Vous pouvez continuer toouse stockage Azure Table pour les tables de stockage et réduire les besoins de débit. Base de données Azure Cosmos introduira prise en charge pour les tables de stockage optimisé dans une prochaine mise à jour et nouveaux et existants Table Azure des comptes de stockage doivent être mis à niveau tooAzure Cosmos DB.

## <a name="premium-and-standard-table-apis"></a>API de table standard et Premium
Si vous utilisez actuellement le stockage de Table Azure, vous bénéficiez des avantages suivants en déplaçant « premium » aperçu tooAzure Cosmos DB de hello :

|  | Stockage de table Azure | Azure Cosmos DB : stockage de table (version préliminaire) |
| --- | --- | --- |
| Latence | Rapide, mais aucune limite supérieure sur la latence | Une latence chiffre millisecondes pour les lectures et écritures commercialement à < latence de 10 ms lit et < 15 ms latence écrit hello 99e centile, à n’importe quelle échelle, n’importe où dans Bonjour |
| Throughput | Modèle de débit hautement évolutif, mais non dédié. Les tables ont une limite d’évolutivité de 20 000 opérations/s | Hautement évolutif avec un [débit dédié réservé par table](request-units.md), qui est soutenu par des contrats SLA. Les comptes n’ont aucune limite supérieure sur le débit, et prennent en charge > 10 millions d’opérations/s par table |
| Diffusion mondiale | Une région unique avec une région de lecture secondaire en option pour la haute disponibilité. Vous ne pouvez pas lancer le basculement | [Distribution globale des clés en main](distribute-data-globally.md) un too30 + régions, prend en charge pour [basculements automatiques et manuels](regional-failover.md) à tout moment, n’importe où dans Bonjour |
| Indexation | Index primaire uniquement sur PartitionKey et RowKey. Pas d’index secondaire | Indexation automatique et complète de toutes les propriétés, aucune gestion des index |
| Requête | L’exécution des requêtes utilise un index de clé primaire, et effectue une recherche dans le cas contraire. | Les requêtes peuvent tirer parti de l’indexation automatique de propriétés pour des temps de requête rapides. Le moteur de base de données d’Azure Cosmos DB est capable de prendre en charge les agrégats, les données géospatiales et le tri. |
| Cohérence | Robuste au sein de la région principale, avec une région secondaire en option | [Cinq niveaux de cohérence bien définis](consistency-levels.md) tootrade hors tension de la disponibilité, la latence, le débit et la cohérence selon les besoins de votre application |
| Tarification | Optimisé pour le stockage  | Optimisé pour le débit |
| Contrats SLA | Disponibilité à 99,9 % | disponibilité de 99,99 % au sein d’une seule région et capacité tooadd plusieurs régions pour accroître la disponibilité. [Contrats SLA complets à la pointe du secteur](https://azure.microsoft.com/support/legal/sla/cosmos-db/) sur la disponibilité générale |

## <a name="how-tooget-started"></a>Mode de démarrage tooget

Créer un compte de base de données Azure Cosmos Bonjour [portail Azure](https://portal.azure.com)et commencer à utiliser notre [démarrage rapide pour l’API de Table à l’aide de .NET](create-table-dotnet.md). 

## <a name="next-steps"></a>Étapes suivantes

Voici quelques pointeurs tooget commencer :
* [Créer une application .NET à l’aide de hello API de Table](create-table-dotnet.md)
* [Développer avec hello dans .NET, les API de Table](tutorial-develop-table-dotnet.md)
* [Interroger des données de la table à l’aide de hello API de Table](tutorial-query-table.md)
* [À l’aide de distribution globale de base de données Azure Cosmos toosetup comment hello des API de Table](tutorial-global-distribution-table.md)
* [Kit de développement logiciel (SDK) de l’API de table d’Azure Cosmos DB pour .NET](table-sdk-dotnet.md)
