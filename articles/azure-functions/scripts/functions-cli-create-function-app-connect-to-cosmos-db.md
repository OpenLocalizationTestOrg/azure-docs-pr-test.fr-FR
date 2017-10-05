---
title: "Créer une fonction Azure qui se connecte à une base de données Azure Cosmos DB | Documents Microsoft"
description: "Exemple de script Azure CLI - Créer une fonction Azure qui se connecte à une base de données Azure Cosmos DB"
services: functions
documentationcenter: functions
author: rachelappel
manager: erikre
editor: 
tags: functions
ms.assetid: 
ms.service: functions
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 04/20/2017
ms.author: rachelap
ms.custom: mvc
ms.openlocfilehash: ba7e934f71824493f29b001cea6dd1c567ef3414
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-azure-function-that-connects-to-an-azure-cosmos-db"></a><span data-ttu-id="141b9-103">Créer une fonction Azure Functions qui se connecte à une base de données Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="141b9-103">Create an Azure Function that connects to an Azure Cosmos DB</span></span>

<span data-ttu-id="141b9-104">Cet exemple de script crée une Function App Azure et se connecte à une base de données Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="141b9-104">This sample script creates an Azure Function App and connects to an Azure Cosmos DB database.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="141b9-105">Si vous choisissez d’installer et d’utiliser l’interface de ligne de commande localement, vous devez exécuter Azure CLI version 2.0 ou une version ultérieure pour poursuivre la procédure décrite dans cet article.</span><span class="sxs-lookup"><span data-stu-id="141b9-105">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="141b9-106">Exécutez `az --version` pour trouver la version.</span><span class="sxs-lookup"><span data-stu-id="141b9-106">Run `az --version` to find the version.</span></span> <span data-ttu-id="141b9-107">Si vous devez installer ou mettre à niveau, consultez [Installation d’Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="141b9-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="141b9-108">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="141b9-108">Sample script</span></span>

<span data-ttu-id="141b9-109">Cet exemple crée une Function App Azure et ajoute un point de terminaison et une clé d’accès Cosmos DB aux paramètres d’application.</span><span class="sxs-lookup"><span data-stu-id="141b9-109">This sample creates an Azure Function app and adds a Cosmos DB endpoint and access key to app settings.</span></span>

<span data-ttu-id="141b9-110">[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/create-function-app-connect-to-cosmos-db/create-function-app-connect-to-cosmos-db.sh "Créer une fonction Azure Functions qui se connecte à une base de données Azure Cosmos DB")]</span><span class="sxs-lookup"><span data-stu-id="141b9-110">[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/create-function-app-connect-to-cosmos-db/create-function-app-connect-to-cosmos-db.sh "Create an Azure Function that connects to an Azure Cosmos DB")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="141b9-111">Nettoyer le déploiement</span><span class="sxs-lookup"><span data-stu-id="141b9-111">Clean up deployment</span></span>

<span data-ttu-id="141b9-112">Une fois l’exemple de script exécuté, la commande suivante permet de supprimer le groupe de ressources et toutes les ressources associées.</span><span class="sxs-lookup"><span data-stu-id="141b9-112">After the script sample has been run, the follow command can be used to remove the resource group and all related resources.</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="141b9-113">Explication du script</span><span class="sxs-lookup"><span data-stu-id="141b9-113">Script explanation</span></span>

<span data-ttu-id="141b9-114">Ce script utilise les commandes suivantes.</span><span class="sxs-lookup"><span data-stu-id="141b9-114">This script uses the following commands.</span></span> <span data-ttu-id="141b9-115">Chaque commande du tableau renvoie à une documentation spécifique.</span><span class="sxs-lookup"><span data-stu-id="141b9-115">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="141b9-116">Commande</span><span class="sxs-lookup"><span data-stu-id="141b9-116">Command</span></span> | <span data-ttu-id="141b9-117">Remarques</span><span class="sxs-lookup"><span data-stu-id="141b9-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="141b9-118">az login</span><span class="sxs-lookup"><span data-stu-id="141b9-118">az login</span></span>](https://docs.microsoft.com/cli/azure/#login) | <span data-ttu-id="141b9-119">Connexion à Azure.</span><span class="sxs-lookup"><span data-stu-id="141b9-119">Login to Azure.</span></span> |
| [<span data-ttu-id="141b9-120">az group create</span><span class="sxs-lookup"><span data-stu-id="141b9-120">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="141b9-121">Crée un groupe de ressources avec un emplacement.</span><span class="sxs-lookup"><span data-stu-id="141b9-121">Create a resource group with location</span></span> |
| [<span data-ttu-id="141b9-122">az storage account create</span><span class="sxs-lookup"><span data-stu-id="141b9-122">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/storage/account) | <span data-ttu-id="141b9-123">Créez un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="141b9-123">Create a storage account</span></span> |
| [<span data-ttu-id="141b9-124">az functionapp create</span><span class="sxs-lookup"><span data-stu-id="141b9-124">az functionapp create</span></span>](https://docs.microsoft.com/cli/azure/functionapp#create) | <span data-ttu-id="141b9-125">Crée une Function App.</span><span class="sxs-lookup"><span data-stu-id="141b9-125">Create a new function app</span></span> |
| [<span data-ttu-id="141b9-126">az documentdb create</span><span class="sxs-lookup"><span data-stu-id="141b9-126">az documentdb create</span></span>](https://docs.microsoft.com/cli/azure/documentdb#create) | <span data-ttu-id="141b9-127">Crée une base de données DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="141b9-127">Create documentdb database</span></span> |
| [<span data-ttu-id="141b9-128">az group delete</span><span class="sxs-lookup"><span data-stu-id="141b9-128">az group delete</span></span>](https://docs.microsoft.com/cli/azure/group#delete) | <span data-ttu-id="141b9-129">Nettoyer</span><span class="sxs-lookup"><span data-stu-id="141b9-129">Clean up</span></span> |

## <a name="next-steps"></a><span data-ttu-id="141b9-130">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="141b9-130">Next steps</span></span>

<span data-ttu-id="141b9-131">Pour plus d’informations sur l’interface Azure CLI, consultez la [documentation relative à l’interface Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="141b9-131">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="141b9-132">Vous trouverez des exemples supplémentaires de scripts CLI Azure Functions dans la [documentation d’Azure Functions](../functions-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="141b9-132">Additional Azure Functions CLI script samples can be found in the [Azure Functions documentation](../functions-cli-samples.md).</span></span>




