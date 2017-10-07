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
# <a name="azure-cli-samples-for-azure-cosmos-db"></a><span data-ttu-id="4e0e5-103">Exemples de CLI pour Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="4e0e5-103">Azure CLI samples for Azure Cosmos DB</span></span>

<span data-ttu-id="4e0e5-104">Hello tableau suivant inclut des liens toosample CLI d’Azure des scripts pour la base de données Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="4e0e5-104">hello following table includes links toosample Azure CLI scripts for Azure Cosmos DB.</span></span> <span data-ttu-id="4e0e5-105">Pages de référence pour toutes les commandes CLI de base de données Azure Cosmos sont disponibles dans hello [Azure CLI 2.0 référence](https://docs.microsoft.com/cli/azure/cosmosdb).</span><span class="sxs-lookup"><span data-stu-id="4e0e5-105">Reference pages for all Azure Cosmos DB CLI commands are available in hello [Azure CLI 2.0 Reference](https://docs.microsoft.com/cli/azure/cosmosdb).</span></span>

| |  |
|---|---|
|<span data-ttu-id="4e0e5-106">**Créer un compte, une base de données et des conteneurs Azure Cosmos DB**</span><span class="sxs-lookup"><span data-stu-id="4e0e5-106">**Create Azure Cosmos DB account, database, and containers**</span></span>||
|[<span data-ttu-id="4e0e5-107">Créer un compte d’API Table, Graph ou DocumentDB</span><span class="sxs-lookup"><span data-stu-id="4e0e5-107">Create a DocumentDB API, Graph, or Table API account</span></span>](scripts/create-database-account-collections-cli.md?toc=%2fcli%2fazure%2ftoc.json)| <span data-ttu-id="4e0e5-108">Crée un seul compte de l’API de base de données Azure Cosmos, base de données et conteneur pour une utilisation avec hello DocumentDB, graphique ou des API de la Table.</span><span class="sxs-lookup"><span data-stu-id="4e0e5-108">Creates a single Azure Cosmos DB API account, database, and container for use with hello DocumentDB, Graph, or Table APIs.</span></span> |
| [<span data-ttu-id="4e0e5-109">Créer un compte d’API MongoDB</span><span class="sxs-lookup"><span data-stu-id="4e0e5-109">Create a MongoDB API account</span></span>](scripts/create-mongodb-database-account-cli.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="4e0e5-110">Crée un compte unique d’API DocumentDB Azure MongoDB avec base de données et collection.</span><span class="sxs-lookup"><span data-stu-id="4e0e5-110">Creates a single Azure Cosmos DB MongoDB API account, database, and collection.</span></span> |
|<span data-ttu-id="4e0e5-111">**Mettre à l’échelle Azure Cosmos DB**</span><span class="sxs-lookup"><span data-stu-id="4e0e5-111">**Scale Azure Cosmos DB**</span></span>||
| [<span data-ttu-id="4e0e5-112">Mettre à l’échelle le débit d’un conteneur</span><span class="sxs-lookup"><span data-stu-id="4e0e5-112">Scale container throughput</span></span>](scripts/scale-collection-throughput-cli.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="4e0e5-113">Hello des modifications configuré débit sur un conteneur.</span><span class="sxs-lookup"><span data-stu-id="4e0e5-113">Changes hello provisioned througput on a container.</span></span>|
|[<span data-ttu-id="4e0e5-114">Répliquer un compte de base de données Azure Cosmos DB dans plusieurs régions et configurer les priorités de basculement</span><span class="sxs-lookup"><span data-stu-id="4e0e5-114">Replicate Azure Cosmos DB database account in multiple regions and configure failover priorities</span></span>](scripts/scale-multiregion-cli.md?toc=%2fcli%2fazure%2ftoc.json)|<span data-ttu-id="4e0e5-115">Réplique les données de compte globalement dans plusieurs régions avec une priorité de basculement spécifié.</span><span class="sxs-lookup"><span data-stu-id="4e0e5-115">Globally replicates account data into multiple regions with a specified failover priority.</span></span>|
|<span data-ttu-id="4e0e5-116">**Sécuriser Azure Cosmos DB**</span><span class="sxs-lookup"><span data-stu-id="4e0e5-116">**Secure Azure Cosmos DB**</span></span>||
| [<span data-ttu-id="4e0e5-117">Obtenir les clés de compte</span><span class="sxs-lookup"><span data-stu-id="4e0e5-117">Get account keys</span></span>](scripts/secure-get-account-key-cli.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="4e0e5-118">Obtient les clés primaires et secondaires écriture master hello et messages clés primaires et secondaires en lecture seule pour le compte de hello.</span><span class="sxs-lookup"><span data-stu-id="4e0e5-118">Gets hello primary and secondary master write keys and primary and secondary read-only keys for hello account.</span></span>|
| [<span data-ttu-id="4e0e5-119">Obtenir la chaîne de connexion MongoDB</span><span class="sxs-lookup"><span data-stu-id="4e0e5-119">Get MongoDB connection string</span></span>](scripts/secure-mongo-connection-string-cli.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="4e0e5-120">Obtient les tooconnect de chaîne de connexion hello votre tooyour d’application MongoDB compte de base de données Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="4e0e5-120">Gets hello connection string tooconnect your MongoDB app tooyour Azure Cosmos DB account.</span></span>|
|[<span data-ttu-id="4e0e5-121">Régénération des clés de compte</span><span class="sxs-lookup"><span data-stu-id="4e0e5-121">Regenerate account keys</span></span>](scripts/secure-regenerate-key-cli.md?toc=%2fcli%2fazure%2ftoc.json)|<span data-ttu-id="4e0e5-122">Régénère les master hello ou clé en lecture seule pour le compte de hello.</span><span class="sxs-lookup"><span data-stu-id="4e0e5-122">Regenerates hello master or read-only key for hello account.</span></span>|
|[<span data-ttu-id="4e0e5-123">Créer un pare-feu</span><span class="sxs-lookup"><span data-stu-id="4e0e5-123">Create a firewall</span></span>](scripts/create-firewall-cli.md?toc=%2fcli%2fazure%2ftoc.json)| <span data-ttu-id="4e0e5-124">Crée un entrants IP accès contrôle stratégie toolimit accès toohello compte depuis un jeu approuvé des ordinateurs et/ou des services de cloud computing.</span><span class="sxs-lookup"><span data-stu-id="4e0e5-124">Creates an inbound IP access control policy toolimit access toohello account from an approved set of machines and/or cloud services.</span></span>|
|<span data-ttu-id="4e0e5-125">**Haute disponibilité et récupération d'urgence, sauvegarde et restauration**</span><span class="sxs-lookup"><span data-stu-id="4e0e5-125">**High availability, disaster recovery, backup and restore**</span></span>||
|[<span data-ttu-id="4e0e5-126">Configurer la stratégie de basculement</span><span class="sxs-lookup"><span data-stu-id="4e0e5-126">Configure failover policy</span></span>](scripts/ha-failover-policy-cli.md?toc=%2fcli%2fazure%2ftoc.json)|<span data-ttu-id="4e0e5-127">Jeux de hello priorité de basculement de chaque région dans laquelle le compte de hello est répliquée.</span><span class="sxs-lookup"><span data-stu-id="4e0e5-127">Sets hello failover priority of each region in which hello account is replicated.</span></span>|
|<span data-ttu-id="4e0e5-128">**Connecter Azure Cosmos DB aux ressources**</span><span class="sxs-lookup"><span data-stu-id="4e0e5-128">**Connect Azure Cosmos DB to resources**</span></span>||
|[<span data-ttu-id="4e0e5-129">Se connecter à un tooAzure d’application web Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="4e0e5-129">Connect a web app tooAzure Cosmos DB</span></span>](https://docs.microsoft.com/azure/app-service-web/scripts/app-service-cli-app-service-documentdb?toc=%2fcli%2fazure%2ftoc.json)|<span data-ttu-id="4e0e5-130">Créez et connectez une base de données Azure Cosmos DB et une application web Azure.</span><span class="sxs-lookup"><span data-stu-id="4e0e5-130">Create and connect an Azure Cosmos DB database and an Azure web app.</span></span>|
|||
