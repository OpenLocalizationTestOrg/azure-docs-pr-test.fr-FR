---
title: "deux réseaux virtuels d’homologues aaaAzure exemple de Script CLI - | Documents Microsoft"
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
ms.openlocfilehash: 54dabb2b9e05951d10f1b6b4f61ca592ce11d364
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="peer-two-virtual-networks"></a><span data-ttu-id="9cd36-103">Homologuer deux réseaux virtuels</span><span class="sxs-lookup"><span data-stu-id="9cd36-103">Peer two virtual networks</span></span>

<span data-ttu-id="9cd36-104">Ce script crée et connecte deux réseaux virtuels Bonjour hello de trhough même région réseau Azure.</span><span class="sxs-lookup"><span data-stu-id="9cd36-104">This script creates and connects two virtual networks in hello same region trhough hello Azure network.</span></span> <span data-ttu-id="9cd36-105">Après avoir exécuté le script de hello, vous allez créer une homologation entre deux réseaux virtuels.</span><span class="sxs-lookup"><span data-stu-id="9cd36-105">After running hello script, you will create a peering between two virtual networks.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


## <a name="sample-script"></a><span data-ttu-id="9cd36-106">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="9cd36-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-network/peer-two-virtual-networks/peer-two-virtual-networks.sh "Peer two networks")]

## <a name="clean-up-deployment"></a><span data-ttu-id="9cd36-107">Nettoyer le déploiement</span><span class="sxs-lookup"><span data-stu-id="9cd36-107">Clean up deployment</span></span> 

<span data-ttu-id="9cd36-108">Exécutez hello suivant du groupe de ressources de commande tooremove hello, machine virtuelle et toutes les ressources.</span><span class="sxs-lookup"><span data-stu-id="9cd36-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="9cd36-109">Explication du script</span><span class="sxs-lookup"><span data-stu-id="9cd36-109">Script explanation</span></span>

<span data-ttu-id="9cd36-110">Ce script utilise hello suivant de commandes toocreate un groupe de ressources, l’ordinateur virtuel, et toutes les ressources associées.</span><span class="sxs-lookup"><span data-stu-id="9cd36-110">This script uses hello following commands toocreate a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="9cd36-111">Chaque commande figurant dans la documentation spécifique du toocommand liens table hello.</span><span class="sxs-lookup"><span data-stu-id="9cd36-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="9cd36-112">Commande</span><span class="sxs-lookup"><span data-stu-id="9cd36-112">Command</span></span> | <span data-ttu-id="9cd36-113">Remarques</span><span class="sxs-lookup"><span data-stu-id="9cd36-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="9cd36-114">az group create</span><span class="sxs-lookup"><span data-stu-id="9cd36-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="9cd36-115">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="9cd36-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="9cd36-116">az network vnet create</span><span class="sxs-lookup"><span data-stu-id="9cd36-116">az network vnet create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet#create) | <span data-ttu-id="9cd36-117">Crée un réseau virtuel et un sous-réseau Azure.</span><span class="sxs-lookup"><span data-stu-id="9cd36-117">Creates an Azure virtual network and subnet.</span></span> |
| [<span data-ttu-id="9cd36-118">az network vnet peering create</span><span class="sxs-lookup"><span data-stu-id="9cd36-118">az network vnet peering create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet/peering#create) | <span data-ttu-id="9cd36-119">Crée une homologation entre deux réseaux virtuels.</span><span class="sxs-lookup"><span data-stu-id="9cd36-119">Creates a peering between two virtual networks.</span></span>  |
| [<span data-ttu-id="9cd36-120">az group delete</span><span class="sxs-lookup"><span data-stu-id="9cd36-120">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="9cd36-121">Supprime un groupe de ressources, y compris toutes les ressources imbriquées.</span><span class="sxs-lookup"><span data-stu-id="9cd36-121">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="9cd36-122">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="9cd36-122">Next steps</span></span>

<span data-ttu-id="9cd36-123">Pour plus d’informations sur hello CLI d’Azure, consultez [documentation relative à Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="9cd36-123">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="9cd36-124">Vous trouverez des exemples de script CLI mise en réseau supplémentaires dans hello [documentation de vue d’ensemble de la mise en réseau Azure](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="9cd36-124">Additional networking CLI script samples can be found in hello [Azure Networking Overview documentation](../cli-samples.md).</span></span>
