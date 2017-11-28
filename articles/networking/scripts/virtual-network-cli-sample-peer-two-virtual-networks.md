---
title: "Exemple de script Azure CLI - Homologuer deux réseaux virtuels | Microsoft Docs"
description: "Exemple de script Azure CLI - Homologuer deux réseaux virtuels"
services: virtual-network
documentationcenter: virtual-network
author: KumudD
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: infrastructure
ms.date: 07/07/2017
ms.author: kumud
ms.openlocfilehash: a2b8fda288072e2fb0087988bbd68d3e4d9031d8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="peer-two-virtual-networks"></a><span data-ttu-id="5c3dc-103">Homologuer deux réseaux virtuels</span><span class="sxs-lookup"><span data-stu-id="5c3dc-103">Peer two virtual networks</span></span>

<span data-ttu-id="5c3dc-104">Ce script crée et connecte deux réseaux virtuels dans la même région via le réseau Azure.</span><span class="sxs-lookup"><span data-stu-id="5c3dc-104">This script creates and connects two virtual networks in the same region trhough the Azure network.</span></span> <span data-ttu-id="5c3dc-105">Après l’exécution du script, vous créerez une homologation entre deux réseaux virtuels.</span><span class="sxs-lookup"><span data-stu-id="5c3dc-105">After running the script, you will create a peering between two virtual networks.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


## <a name="sample-script"></a><span data-ttu-id="5c3dc-106">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="5c3dc-106">Sample script</span></span>

<span data-ttu-id="5c3dc-107">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-network/peer-two-virtual-networks/peer-two-virtual-networks.sh "Homologuer deux réseaux")]</span><span class="sxs-lookup"><span data-stu-id="5c3dc-107">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-network/peer-two-virtual-networks/peer-two-virtual-networks.sh "Peer two networks")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="5c3dc-108">Nettoyer le déploiement</span><span class="sxs-lookup"><span data-stu-id="5c3dc-108">Clean up deployment</span></span> 

<span data-ttu-id="5c3dc-109">Exécutez la commande suivante pour supprimer le groupe de ressources, la machine virtuelle et toutes les ressources associées.</span><span class="sxs-lookup"><span data-stu-id="5c3dc-109">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="5c3dc-110">Explication du script</span><span class="sxs-lookup"><span data-stu-id="5c3dc-110">Script explanation</span></span>

<span data-ttu-id="5c3dc-111">Ce script utilise les commandes suivantes pour créer un groupe de ressources, une machine virtuelle et toutes les ressources associées.</span><span class="sxs-lookup"><span data-stu-id="5c3dc-111">This script uses the following commands to create a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="5c3dc-112">Chaque commande du tableau renvoie à une documentation spécifique.</span><span class="sxs-lookup"><span data-stu-id="5c3dc-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="5c3dc-113">Commande</span><span class="sxs-lookup"><span data-stu-id="5c3dc-113">Command</span></span> | <span data-ttu-id="5c3dc-114">Remarques</span><span class="sxs-lookup"><span data-stu-id="5c3dc-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="5c3dc-115">az group create</span><span class="sxs-lookup"><span data-stu-id="5c3dc-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="5c3dc-116">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="5c3dc-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="5c3dc-117">az network vnet create</span><span class="sxs-lookup"><span data-stu-id="5c3dc-117">az network vnet create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet#create) | <span data-ttu-id="5c3dc-118">Crée un réseau virtuel et un sous-réseau Azure.</span><span class="sxs-lookup"><span data-stu-id="5c3dc-118">Creates an Azure virtual network and subnet.</span></span> |
| [<span data-ttu-id="5c3dc-119">az network vnet peering create</span><span class="sxs-lookup"><span data-stu-id="5c3dc-119">az network vnet peering create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet/peering#create) | <span data-ttu-id="5c3dc-120">Crée une homologation entre deux réseaux virtuels.</span><span class="sxs-lookup"><span data-stu-id="5c3dc-120">Creates a peering between two virtual networks.</span></span>  |
| [<span data-ttu-id="5c3dc-121">az group delete</span><span class="sxs-lookup"><span data-stu-id="5c3dc-121">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="5c3dc-122">Supprime un groupe de ressources, y compris toutes les ressources imbriquées.</span><span class="sxs-lookup"><span data-stu-id="5c3dc-122">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="5c3dc-123">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="5c3dc-123">Next steps</span></span>

<span data-ttu-id="5c3dc-124">Pour plus d’informations sur l’interface Azure CLI, consultez la [documentation relative à l’interface Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="5c3dc-124">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="5c3dc-125">Vous pouvez trouver des exemples supplémentaires de scripts CLI de mise en réseau dans la [documentation Vue d’ensemble de la mise en réseau Azure](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="5c3dc-125">Additional networking CLI script samples can be found in the [Azure Networking Overview documentation](../cli-samples.md).</span></span>
