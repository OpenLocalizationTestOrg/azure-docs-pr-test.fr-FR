---
title: "Exemples Azure PowerShell pour Azure Cosmos DB | Microsoft Docs"
description: "Exemples Azure PowerShell - Des scripts pour vous aider à créer et gérer des comptes Azure Cosmos DB."
services: cosmos-db
author: mimig1
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: cosmos-db
ms.custom: mvc
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: database
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: 7698e03c0dc8d1c6d1e926f45e903a909bfd0c93
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-powershell-samples-for-azure-cosmos-db"></a><span data-ttu-id="d7277-103">Exemples Azure PowerShell pour Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="d7277-103">Azure PowerShell samples for Azure Cosmos DB</span></span>

<span data-ttu-id="d7277-104">Le tableau suivant comprend des liens vers des exemples de scripts Azure PowerShell pour Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d7277-104">The following table includes links to sample Azure PowerShell scripts for Azure Cosmos DB.</span></span>

| |  |
|---|---|
|<span data-ttu-id="d7277-105">**Création d’un compte Azure Cosmos DB**</span><span class="sxs-lookup"><span data-stu-id="d7277-105">**Create an Azure Cosmos DB account**</span></span>||
|[<span data-ttu-id="d7277-106">Créer un compte d’API DocumentDB</span><span class="sxs-lookup"><span data-stu-id="d7277-106">Create a DocumentDB API account</span></span>](scripts/create-database-account-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)| <span data-ttu-id="d7277-107">Crée un seul compte Azure Cosmos DB à utiliser avec l’API DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="d7277-107">Creates a single Azure Cosmos DB account to use with the DocumentDB API.</span></span> |
|<span data-ttu-id="d7277-108">**Mettre à l’échelle Azure Cosmos DB**</span><span class="sxs-lookup"><span data-stu-id="d7277-108">**Scale Azure Cosmos DB**</span></span>||
|[<span data-ttu-id="d7277-109">Répliquer un compte Azure Cosmos DB dans plusieurs régions et configurer les priorités de basculement</span><span class="sxs-lookup"><span data-stu-id="d7277-109">Replicate Azure Cosmos DB account in multiple regions and configure failover priorities</span></span>](scripts/scale-multiregion-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)|<span data-ttu-id="d7277-110">Réplique les données de compte globalement dans plusieurs régions avec une priorité de basculement spécifié.</span><span class="sxs-lookup"><span data-stu-id="d7277-110">Globally replicates account data into multiple regions with a specified failover priority.</span></span>|
|<span data-ttu-id="d7277-111">**Sécuriser Azure Cosmos DB**</span><span class="sxs-lookup"><span data-stu-id="d7277-111">**Secure Azure Cosmos DB**</span></span>||
| [<span data-ttu-id="d7277-112">Obtenir les clés de compte</span><span class="sxs-lookup"><span data-stu-id="d7277-112">Get account keys</span></span>](scripts/secure-get-account-key-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="d7277-113">Obtient les clés primaire et secondaire d’écriture maître et les clés primaire et secondaire de lecture seule pour le compte.</span><span class="sxs-lookup"><span data-stu-id="d7277-113">Gets the primary and secondary master write keys and primary and secondary read-only keys for the account.</span></span>|
| [<span data-ttu-id="d7277-114">Obtenir la chaîne de connexion MongoDB</span><span class="sxs-lookup"><span data-stu-id="d7277-114">Get MongoDB connection string</span></span>](scripts/secure-mongo-connection-string-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="d7277-115">Obtient la chaîne de connexion pour connecter votre application MongoDB à votre compte Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d7277-115">Gets the connection string to connect your MongoDB app to your Azure Cosmos DB account.</span></span>|
|[<span data-ttu-id="d7277-116">Régénération des clés de compte</span><span class="sxs-lookup"><span data-stu-id="d7277-116">Regenerate account keys</span></span>](scripts/secure-regenerate-key-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)|<span data-ttu-id="d7277-117">Régénère la clé de maître ou en lecture seule pour le compte.</span><span class="sxs-lookup"><span data-stu-id="d7277-117">Regenerates the master or read-only key for the account.</span></span>|
|[<span data-ttu-id="d7277-118">Créer un pare-feu</span><span class="sxs-lookup"><span data-stu-id="d7277-118">Create a firewall</span></span>](scripts/create-firewall-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)| <span data-ttu-id="d7277-119">Crée une stratégie de contrôle d’accès des IP entrantes pour limiter l’accès au compte à un ensemble de machines et/ou services cloud approuvés.</span><span class="sxs-lookup"><span data-stu-id="d7277-119">Creates an inbound IP access control policy to limit access to the account from an approved set of machines and/or cloud services.</span></span>|
|<span data-ttu-id="d7277-120">**Haute disponibilité et récupération d'urgence, sauvegarde et restauration**</span><span class="sxs-lookup"><span data-stu-id="d7277-120">**High availability, disaster recovery, backup and restore**</span></span>||
|[<span data-ttu-id="d7277-121">Configurer la stratégie de basculement</span><span class="sxs-lookup"><span data-stu-id="d7277-121">Configure failover policy</span></span>](scripts/ha-failover-policy-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)|<span data-ttu-id="d7277-122">Définit la priorité de basculement de chaque région dans laquelle le compte est répliqué.</span><span class="sxs-lookup"><span data-stu-id="d7277-122">Sets the failover priority of each region in which the account is replicated.</span></span>|
|||