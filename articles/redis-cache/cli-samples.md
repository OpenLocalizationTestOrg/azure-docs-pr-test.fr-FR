---
title: Exemples de CLI du Cache Redis Azure | Microsoft Docs
description: Exemples de CLI pour le Cache Redis Azure.
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 8d2de145-50c0-4f76-bf8f-fdf679f03698
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: azurecli
ms.topic: article
ms.date: 04/14/2017
ms.author: sdanie
ms.openlocfilehash: a3debf3380b57faa5b7b30f612698fe6de5b7067
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-cli-samples-for-azure-redis-cache"></a><span data-ttu-id="f3a3b-103">Exemples de CLI pour le Cache Redis Azure</span><span class="sxs-lookup"><span data-stu-id="f3a3b-103">Azure CLI Samples for Azure Redis Cache</span></span>

<span data-ttu-id="f3a3b-104">Le tableau suivant contient des liens vers des scripts Bash créés à l’aide de l’interface de ligne de commande Azure.</span><span class="sxs-lookup"><span data-stu-id="f3a3b-104">The following table includes links to bash scripts built using the Azure CLI.</span></span>

| | |
|---|---|
|<span data-ttu-id="f3a3b-105">**Créer un cache**</span><span class="sxs-lookup"><span data-stu-id="f3a3b-105">**Create cache**</span></span>||
| [<span data-ttu-id="f3a3b-106">Créer un cache</span><span class="sxs-lookup"><span data-stu-id="f3a3b-106">Create a cache</span></span>](./scripts/create-cache.md) | <span data-ttu-id="f3a3b-107">Crée un groupe de ressources et un Cache Redis Azure de niveau de base.</span><span class="sxs-lookup"><span data-stu-id="f3a3b-107">Creates a resource group and a basic tier Azure Redis Cache.</span></span> |
| [<span data-ttu-id="f3a3b-108">Créer un cache Premium avec clustering</span><span class="sxs-lookup"><span data-stu-id="f3a3b-108">Create a premium cache with clustering</span></span>](./scripts/create-premium-cache-cluster.md) | <span data-ttu-id="f3a3b-109">Crée un groupe de ressources et un cache de niveau Premium avec activation du clustering.</span><span class="sxs-lookup"><span data-stu-id="f3a3b-109">Creates a resource group and a premium tier cache with clustering enabled.</span></span>|
| [<span data-ttu-id="f3a3b-110">Obtenir les détails du cache</span><span class="sxs-lookup"><span data-stu-id="f3a3b-110">Get cache details</span></span>](./scripts/show-cache.md) | <span data-ttu-id="f3a3b-111">Obtient les détails d’une instance du Cache Redis Azure, dont l’état d’approvisionnement.</span><span class="sxs-lookup"><span data-stu-id="f3a3b-111">Gets details of an Azure Redis Cache instance, including provisioning status.</span></span> |
| [<span data-ttu-id="f3a3b-112">Obtenir le nom d’hôte, les ports et les clés</span><span class="sxs-lookup"><span data-stu-id="f3a3b-112">Get the hostname, ports, and keys</span></span>](./scripts/cache-keys-ports.md) | <span data-ttu-id="f3a3b-113">Obtient le nom d’hôte, les ports et les clés pour une instance du Cache Redis Azure.</span><span class="sxs-lookup"><span data-stu-id="f3a3b-113">Gets the hostname, ports, and keys for an Azure Redis Cache instance.</span></span> |
|<span data-ttu-id="f3a3b-114">**Application web avec cache**</span><span class="sxs-lookup"><span data-stu-id="f3a3b-114">**Web app plus cache**</span></span>||
| [<span data-ttu-id="f3a3b-115">Connecter une application web à un cache redis</span><span class="sxs-lookup"><span data-stu-id="f3a3b-115">Connect a web app to a redis cache</span></span>](./../app-service-web/scripts/app-service-cli-app-service-redis.md) | <span data-ttu-id="f3a3b-116">Crée une application web Azure et un Cache Redis, puis ajoute les détails de connexion Redis aux paramètres d’application.</span><span class="sxs-lookup"><span data-stu-id="f3a3b-116">Creates an Azure web app and a redis cache, then adds the redis connection details to the app settings.</span></span> |
|<span data-ttu-id="f3a3b-117">**Supprimer un cache**</span><span class="sxs-lookup"><span data-stu-id="f3a3b-117">**Delete cache**</span></span>||
| [<span data-ttu-id="f3a3b-118">Supprimer un cache</span><span class="sxs-lookup"><span data-stu-id="f3a3b-118">Delete a cache</span></span>](./scripts/delete-cache.md) | <span data-ttu-id="f3a3b-119">Supprime une instance du Cache Redis Azure</span><span class="sxs-lookup"><span data-stu-id="f3a3b-119">Deletes an Azure Redis Cache instance</span></span>  |
| | |

<span data-ttu-id="f3a3b-120">Pour plus d’informations sur Azure CLI 2.0, voir [Installer Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) et [Prise en main d’Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="f3a3b-120">For more information about Azure CLI 2.0, see [Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) and [Get started with Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli).</span></span>