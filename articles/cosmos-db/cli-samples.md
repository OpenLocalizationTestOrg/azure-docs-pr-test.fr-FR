---
title: "Exemples Azure CLI pour Azure Cosmos DB | Microsoft Docs"
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
ms.openlocfilehash: 709d2ccce0f4b9827a8076f683c7e0f74cbdd4ea
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-cli-samples-for-azure-cosmos-db"></a><span data-ttu-id="4557d-103">Exemples de CLI pour Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="4557d-103">Azure CLI samples for Azure Cosmos DB</span></span>

<span data-ttu-id="4557d-104">Le tableau suivant comprend des liens vers des exemples de scripts Azure CLI pour Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="4557d-104">The following table includes links to sample Azure CLI scripts for Azure Cosmos DB.</span></span> <span data-ttu-id="4557d-105">Des pages de référence pour toutes les commandes CLI d’Azure Cosmos DB sont disponibles dans la [référence Azure CLI 2.0](https://docs.microsoft.com/cli/azure/cosmosdb).</span><span class="sxs-lookup"><span data-stu-id="4557d-105">Reference pages for all Azure Cosmos DB CLI commands are available in the [Azure CLI 2.0 Reference](https://docs.microsoft.com/cli/azure/cosmosdb).</span></span>

| |  |
|---|---|
|<span data-ttu-id="4557d-106">**Créer un compte, une base de données et des conteneurs Azure Cosmos DB**</span><span class="sxs-lookup"><span data-stu-id="4557d-106">**Create Azure Cosmos DB account, database, and containers**</span></span>||
|[<span data-ttu-id="4557d-107">Créer un compte d’API Table, Graph ou DocumentDB</span><span class="sxs-lookup"><span data-stu-id="4557d-107">Create a DocumentDB API, Graph, or Table API account</span></span>](scripts/create-database-account-collections-cli.md?toc=%2fcli%2fazure%2ftoc.json)| <span data-ttu-id="4557d-108">Crée un compte unique d’API Azure Cosmos DB avec base de données et conteneur, à utiliser avec les API Table, Graph et DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="4557d-108">Creates a single Azure Cosmos DB API account, database, and container for use with the DocumentDB, Graph, or Table APIs.</span></span> |
| [<span data-ttu-id="4557d-109">Créer un compte d’API MongoDB</span><span class="sxs-lookup"><span data-stu-id="4557d-109">Create a MongoDB API account</span></span>](scripts/create-mongodb-database-account-cli.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="4557d-110">Crée un compte unique d’API DocumentDB Azure MongoDB avec base de données et collection.</span><span class="sxs-lookup"><span data-stu-id="4557d-110">Creates a single Azure Cosmos DB MongoDB API account, database, and collection.</span></span> |
|<span data-ttu-id="4557d-111">**Mettre à l’échelle Azure Cosmos DB**</span><span class="sxs-lookup"><span data-stu-id="4557d-111">**Scale Azure Cosmos DB**</span></span>||
| [<span data-ttu-id="4557d-112">Mettre à l’échelle le débit d’un conteneur</span><span class="sxs-lookup"><span data-stu-id="4557d-112">Scale container throughput</span></span>](scripts/scale-collection-throughput-cli.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="4557d-113">Modifie le débit configuré sur un conteneur.</span><span class="sxs-lookup"><span data-stu-id="4557d-113">Changes the provisioned througput on a container.</span></span>|
|[<span data-ttu-id="4557d-114">Répliquer un compte de base de données Azure Cosmos DB dans plusieurs régions et configurer les priorités de basculement</span><span class="sxs-lookup"><span data-stu-id="4557d-114">Replicate Azure Cosmos DB database account in multiple regions and configure failover priorities</span></span>](scripts/scale-multiregion-cli.md?toc=%2fcli%2fazure%2ftoc.json)|<span data-ttu-id="4557d-115">Réplique les données de compte globalement dans plusieurs régions avec une priorité de basculement spécifié.</span><span class="sxs-lookup"><span data-stu-id="4557d-115">Globally replicates account data into multiple regions with a specified failover priority.</span></span>|
|<span data-ttu-id="4557d-116">**Sécuriser Azure Cosmos DB**</span><span class="sxs-lookup"><span data-stu-id="4557d-116">**Secure Azure Cosmos DB**</span></span>||
| [<span data-ttu-id="4557d-117">Obtenir les clés de compte</span><span class="sxs-lookup"><span data-stu-id="4557d-117">Get account keys</span></span>](scripts/secure-get-account-key-cli.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="4557d-118">Obtient les clés primaire et secondaire d’écriture maître et les clés primaire et secondaire de lecture seule pour le compte.</span><span class="sxs-lookup"><span data-stu-id="4557d-118">Gets the primary and secondary master write keys and primary and secondary read-only keys for the account.</span></span>|
| [<span data-ttu-id="4557d-119">Obtenir la chaîne de connexion MongoDB</span><span class="sxs-lookup"><span data-stu-id="4557d-119">Get MongoDB connection string</span></span>](scripts/secure-mongo-connection-string-cli.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="4557d-120">Obtient la chaîne de connexion pour connecter votre application MongoDB à votre compte Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="4557d-120">Gets the connection string to connect your MongoDB app to your Azure Cosmos DB account.</span></span>|
|[<span data-ttu-id="4557d-121">Régénération des clés de compte</span><span class="sxs-lookup"><span data-stu-id="4557d-121">Regenerate account keys</span></span>](scripts/secure-regenerate-key-cli.md?toc=%2fcli%2fazure%2ftoc.json)|<span data-ttu-id="4557d-122">Régénère la clé de maître ou en lecture seule pour le compte.</span><span class="sxs-lookup"><span data-stu-id="4557d-122">Regenerates the master or read-only key for the account.</span></span>|
|[<span data-ttu-id="4557d-123">Créer un pare-feu</span><span class="sxs-lookup"><span data-stu-id="4557d-123">Create a firewall</span></span>](scripts/create-firewall-cli.md?toc=%2fcli%2fazure%2ftoc.json)| <span data-ttu-id="4557d-124">Crée une stratégie de contrôle d’accès des IP entrantes pour limiter l’accès au compte à un ensemble de machines et/ou services cloud approuvés.</span><span class="sxs-lookup"><span data-stu-id="4557d-124">Creates an inbound IP access control policy to limit access to the account from an approved set of machines and/or cloud services.</span></span>|
|<span data-ttu-id="4557d-125">**Haute disponibilité et récupération d'urgence, sauvegarde et restauration**</span><span class="sxs-lookup"><span data-stu-id="4557d-125">**High availability, disaster recovery, backup and restore**</span></span>||
|[<span data-ttu-id="4557d-126">Configurer la stratégie de basculement</span><span class="sxs-lookup"><span data-stu-id="4557d-126">Configure failover policy</span></span>](scripts/ha-failover-policy-cli.md?toc=%2fcli%2fazure%2ftoc.json)|<span data-ttu-id="4557d-127">Définit la priorité de basculement de chaque région dans laquelle le compte est répliqué.</span><span class="sxs-lookup"><span data-stu-id="4557d-127">Sets the failover priority of each region in which the account is replicated.</span></span>|
|<span data-ttu-id="4557d-128">**Connecter Azure Cosmos DB aux ressources**</span><span class="sxs-lookup"><span data-stu-id="4557d-128">**Connect Azure Cosmos DB to resources**</span></span>||
|[<span data-ttu-id="4557d-129">Connecter une application web à Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="4557d-129">Connect a web app to Azure Cosmos DB</span></span>](https://docs.microsoft.com/azure/app-service-web/scripts/app-service-cli-app-service-documentdb?toc=%2fcli%2fazure%2ftoc.json)|<span data-ttu-id="4557d-130">Créez et connectez une base de données Azure Cosmos DB et une application web Azure.</span><span class="sxs-lookup"><span data-stu-id="4557d-130">Create and connect an Azure Cosmos DB database and an Azure web app.</span></span>|
|||
