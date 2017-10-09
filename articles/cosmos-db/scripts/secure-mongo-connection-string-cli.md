---
title: "aaaAzure chaîne de connexion de base de données Cosmos CLI Get-Script Azure pour les applications de MongoDB | Documents Microsoft"
description: "Exemple de script CLI Azure - Obtenir la chaîne de connexion à Azure Cosmos DB pour les applications MongoDB"
services: cosmos-db
documentationcenter: cosmosdb
author: mimig1
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: cosmos-db
ms.custom: mvc
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: cosmosdb
ms.workload: database
ms.date: 06/02/2017
ms.author: mimig
ms.openlocfilehash: 9b0a4bf020039c9bf9554b4199a279622c15a15d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-an-azure-cosmos-db-connection-string-for-mongodb-apps-using-hello-azure-cli"></a><span data-ttu-id="a3fd5-103">Obtenir une chaîne de connexion de base de données Azure Cosmos pour les applications MongoDB à l’aide de hello CLI d’Azure</span><span class="sxs-lookup"><span data-stu-id="a3fd5-103">Get an Azure Cosmos DB connection string for MongoDB apps using hello Azure CLI</span></span>

<span data-ttu-id="a3fd5-104">Cet exemple obtient une chaîne de connexion de base de données Azure Cosmos pour les applications MongoDB à l’aide de hello CLI d’Azure.</span><span class="sxs-lookup"><span data-stu-id="a3fd5-104">This sample gets an Azure Cosmos DB connection string for MongoDB apps using hello Azure CLI.</span></span> 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="a3fd5-105">Si vous choisissez tooinstall et que vous utilisez hello CLI localement, cette rubrique requiert que vous exécutez hello CLI d’Azure version 2.0 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="a3fd5-105">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="a3fd5-106">Exécutez `az --version` version de hello toofind.</span><span class="sxs-lookup"><span data-stu-id="a3fd5-106">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="a3fd5-107">Si vous avez besoin de tooinstall ou mise à niveau, consultez [installer Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="a3fd5-107">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="a3fd5-108">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="a3fd5-108">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/cosmosdb/secure-cosmosdb-get-mongodb-connection-string/secure-cosmosdb-get-mongodb-connection-string.sh?highlight=36-39 "Get Azure Cosmos DB connection string for MongoDB apps")]

## <a name="clean-up-deployment"></a><span data-ttu-id="a3fd5-109">Nettoyer le déploiement</span><span class="sxs-lookup"><span data-stu-id="a3fd5-109">Clean up deployment</span></span>

<span data-ttu-id="a3fd5-110">Après exécution de l’exemple de script hello, hello commande suivante peut être de groupe de ressources utilisé tooremove hello et toutes les ressources associées.</span><span class="sxs-lookup"><span data-stu-id="a3fd5-110">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="a3fd5-111">Explication du script</span><span class="sxs-lookup"><span data-stu-id="a3fd5-111">Script explanation</span></span>

<span data-ttu-id="a3fd5-112">Ce script utilise hello suivant les commandes.</span><span class="sxs-lookup"><span data-stu-id="a3fd5-112">This script uses hello following commands.</span></span> <span data-ttu-id="a3fd5-113">Chaque commande figurant dans la documentation spécifique du toocommand liens table hello.</span><span class="sxs-lookup"><span data-stu-id="a3fd5-113">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="a3fd5-114">Commande</span><span class="sxs-lookup"><span data-stu-id="a3fd5-114">Command</span></span> | <span data-ttu-id="a3fd5-115">Remarques</span><span class="sxs-lookup"><span data-stu-id="a3fd5-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="a3fd5-116">az group create</span><span class="sxs-lookup"><span data-stu-id="a3fd5-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="a3fd5-117">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="a3fd5-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="a3fd5-118">az cosmosdb update</span><span class="sxs-lookup"><span data-stu-id="a3fd5-118">az cosmosdb update</span></span>](https://docs.microsoft.com/cli/azure/cosmosdb#update) | <span data-ttu-id="a3fd5-119">Met à jour un compte Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="a3fd5-119">Updates an Azure Cosmos DB account.</span></span> |
| [<span data-ttu-id="a3fd5-120">az cosmosdb list-connection-strings</span><span class="sxs-lookup"><span data-stu-id="a3fd5-120">az cosmosdb list-connection-strings</span></span>](https://docs.microsoft.com/cli/azure/cosmosdb#list-connection-strings) | <span data-ttu-id="a3fd5-121">Obtient la chaîne de connexion hello pour le compte de hello.</span><span class="sxs-lookup"><span data-stu-id="a3fd5-121">Gets hello connection string for hello account.</span></span>|
| [<span data-ttu-id="a3fd5-122">az group delete</span><span class="sxs-lookup"><span data-stu-id="a3fd5-122">az group delete</span></span>](https://docs.microsoft.com/cli/azure/group#delete) | <span data-ttu-id="a3fd5-123">Supprime un groupe de ressources, y compris toutes les ressources imbriquées.</span><span class="sxs-lookup"><span data-stu-id="a3fd5-123">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="a3fd5-124">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a3fd5-124">Next steps</span></span>

<span data-ttu-id="a3fd5-125">Pour plus d’informations sur hello CLI d’Azure, consultez [documentation relative à Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="a3fd5-125">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="a3fd5-126">Vous trouverez des exemples supplémentaires de script CLI de base de données Azure Cosmos Bonjour [documentation de l’interface CLI de base de données Azure Cosmos](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="a3fd5-126">Additional Azure Cosmos DB CLI script samples can be found in hello [Azure Cosmos DB CLI documentation](../cli-samples.md).</span></span>
