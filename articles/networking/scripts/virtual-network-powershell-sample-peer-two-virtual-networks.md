---
title: "deux réseaux virtuels d’homologues aaaAzure exemple de Script PowerShell - | Documents Microsoft"
description: "Exemple de script Azure PowerShell - Homologuer deux réseaux virtuels"
services: virtual-network
documentationcenter: virtual-network
author: georgewallace
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: powershell
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: infrastructure
ms.date: 05/16/2017
ms.author: gwallace
ms.openlocfilehash: 8b66085c35de2fc30bcef57a00d7d370911d1f3c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="peer-two-virtual-networks"></a><span data-ttu-id="e7ec3-103">Homologuer deux réseaux virtuels</span><span class="sxs-lookup"><span data-stu-id="e7ec3-103">Peer two virtual networks</span></span>

<span data-ttu-id="e7ec3-104">Ce script crée et connecte deux réseaux virtuels Bonjour hello de trhough même région réseau Azure.</span><span class="sxs-lookup"><span data-stu-id="e7ec3-104">This script creates and connects two virtual networks in hello same region trhough hello Azure network.</span></span> <span data-ttu-id="e7ec3-105">Après avoir exécuté le script de hello, vous allez créer une homologation entre deux réseaux virtuels.</span><span class="sxs-lookup"><span data-stu-id="e7ec3-105">After running hello script, you will create a peering between two virtual networks.</span></span>

<span data-ttu-id="e7ec3-106">Si nécessaire, installez hello Azure PowerShell en utilisant une instruction de hello trouvé dans hello [guide Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), puis exécutez `Login-AzureRmAccount` toocreate une connexion avec Azure.</span><span class="sxs-lookup"><span data-stu-id="e7ec3-106">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="e7ec3-107">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="e7ec3-107">Sample script</span></span>

[!code-azurepowershell[main](../../../powershell_scripts/virtual-network/peer-two-virtual-networks/peer-two-virtual-networks.ps1 "Peer two networks")]

## <a name="clean-up-deployment"></a><span data-ttu-id="e7ec3-108">Nettoyer le déploiement</span><span class="sxs-lookup"><span data-stu-id="e7ec3-108">Clean up deployment</span></span> 

<span data-ttu-id="e7ec3-109">Exécutez hello suivant du groupe de ressources de commande tooremove hello, machine virtuelle et toutes les ressources.</span><span class="sxs-lookup"><span data-stu-id="e7ec3-109">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="e7ec3-110">Explication du script</span><span class="sxs-lookup"><span data-stu-id="e7ec3-110">Script explanation</span></span>

<span data-ttu-id="e7ec3-111">Ce script utilise hello suivant de commandes toocreate un groupe de ressources, l’ordinateur virtuel, et toutes les ressources associées.</span><span class="sxs-lookup"><span data-stu-id="e7ec3-111">This script uses hello following commands toocreate a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="e7ec3-112">Chaque commande figurant dans la documentation spécifique du toocommand liens table hello.</span><span class="sxs-lookup"><span data-stu-id="e7ec3-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="e7ec3-113">Commande</span><span class="sxs-lookup"><span data-stu-id="e7ec3-113">Command</span></span> | <span data-ttu-id="e7ec3-114">Remarques</span><span class="sxs-lookup"><span data-stu-id="e7ec3-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="e7ec3-115">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="e7ec3-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="e7ec3-116">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="e7ec3-116">Creates a resource group in which all resources are stored.</span></span> | 
| [<span data-ttu-id="e7ec3-117">New-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="e7ec3-117">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork)| <span data-ttu-id="e7ec3-118">Crée un réseau virtuel et un sous-réseau Azure.</span><span class="sxs-lookup"><span data-stu-id="e7ec3-118">Creates an Azure virtual network and subnet.</span></span> |
| [<span data-ttu-id="e7ec3-119">Add-AzureRmVirtualNetworkPeering</span><span class="sxs-lookup"><span data-stu-id="e7ec3-119">Add-AzureRmVirtualNetworkPeering</span></span>](/powershell/module/azurerm.network/add-azurermvirtualnetworkpeering) | <span data-ttu-id="e7ec3-120">Crée une homologation entre deux réseaux virtuels.</span><span class="sxs-lookup"><span data-stu-id="e7ec3-120">Creates a peering between two virtual networks.</span></span>  |
| [<span data-ttu-id="e7ec3-121">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="e7ec3-121">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="e7ec3-122">Supprime un groupe de ressources, y compris toutes les ressources imbriquées.</span><span class="sxs-lookup"><span data-stu-id="e7ec3-122">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="e7ec3-123">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e7ec3-123">Next steps</span></span>

<span data-ttu-id="e7ec3-124">Pour plus d’informations sur hello Azure PowerShell, consultez [documentation Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="e7ec3-124">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azure/overview).</span></span>

<span data-ttu-id="e7ec3-125">Vous trouverez des exemples de script PowerShell mise en réseau supplémentaires dans hello [documentation de vue d’ensemble de la mise en réseau Azure](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e7ec3-125">Additional networking PowerShell script samples can be found in hello [Azure Networking Overview documentation](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span></span>
