---
title: "aaaAzure CLI des exemples de base de données Azure Cosmos | Documents Microsoft"
description: "Exemples de CLI Azure - Créer et gérer des bases de données, conteneurs, régions et pare-feu et comptes Azure Cosmos DB."
services: cosmos-db
author: mimig1
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: cosmos-db
ms.custom: mvc
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: database
ms.date: 06/07/2017
ms.author: mimig
ms.openlocfilehash: d6eefc3274e0b66eec4e69166bb7d4ddd58a522e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cli-samples-for-azure-cosmos-db"></a>Exemples de CLI pour Azure Cosmos DB

Hello tableau suivant inclut des liens toosample CLI d’Azure des scripts pour la base de données Azure Cosmos. Pages de référence pour toutes les commandes CLI de base de données Azure Cosmos sont disponibles dans hello [Azure CLI 2.0 référence](https://docs.microsoft.com/cli/azure/cosmosdb).

| |  |
|---|---|
|**Créer un compte, une base de données et des conteneurs Azure Cosmos DB**||
|[Créer un compte d’API Table, Graph ou DocumentDB](scripts/create-database-account-collections-cli.md?toc=%2fcli%2fazure%2ftoc.json)| Crée un seul compte de l’API de base de données Azure Cosmos, base de données et conteneur pour une utilisation avec hello DocumentDB, graphique ou des API de la Table. |
| [Créer un compte d’API MongoDB](scripts/create-mongodb-database-account-cli.md?toc=%2fcli%2fazure%2ftoc.json) | Crée un compte unique d’API DocumentDB Azure MongoDB avec base de données et collection. |
|**Mettre à l’échelle Azure Cosmos DB**||
| [Mettre à l’échelle le débit d’un conteneur](scripts/scale-collection-throughput-cli.md?toc=%2fcli%2fazure%2ftoc.json) | Hello des modifications configuré débit sur un conteneur.|
|[Répliquer un compte de base de données Azure Cosmos DB dans plusieurs régions et configurer les priorités de basculement](scripts/scale-multiregion-cli.md?toc=%2fcli%2fazure%2ftoc.json)|Réplique les données de compte globalement dans plusieurs régions avec une priorité de basculement spécifié.|
|**Sécuriser Azure Cosmos DB**||
| [Obtenir les clés de compte](scripts/secure-get-account-key-cli.md?toc=%2fcli%2fazure%2ftoc.json) | Obtient les clés primaires et secondaires écriture master hello et messages clés primaires et secondaires en lecture seule pour le compte de hello.|
| [Obtenir la chaîne de connexion MongoDB](scripts/secure-mongo-connection-string-cli.md?toc=%2fcli%2fazure%2ftoc.json) | Obtient les tooconnect de chaîne de connexion hello votre tooyour d’application MongoDB compte de base de données Azure Cosmos.|
|[Régénération des clés de compte](scripts/secure-regenerate-key-cli.md?toc=%2fcli%2fazure%2ftoc.json)|Régénère les master hello ou clé en lecture seule pour le compte de hello.|
|[Créer un pare-feu](scripts/create-firewall-cli.md?toc=%2fcli%2fazure%2ftoc.json)| Crée un entrants IP accès contrôle stratégie toolimit accès toohello compte depuis un jeu approuvé des ordinateurs et/ou des services de cloud computing.|
|**Haute disponibilité et récupération d'urgence, sauvegarde et restauration**||
|[Configurer la stratégie de basculement](scripts/ha-failover-policy-cli.md?toc=%2fcli%2fazure%2ftoc.json)|Jeux de hello priorité de basculement de chaque région dans laquelle le compte de hello est répliquée.|
|**Connecter Azure Cosmos DB aux ressources**||
|[Se connecter à un tooAzure d’application web Cosmos DB](https://docs.microsoft.com/azure/app-service-web/scripts/app-service-cli-app-service-documentdb?toc=%2fcli%2fazure%2ftoc.json)|Créez et connectez une base de données Azure Cosmos DB et une application web Azure.|
|||
