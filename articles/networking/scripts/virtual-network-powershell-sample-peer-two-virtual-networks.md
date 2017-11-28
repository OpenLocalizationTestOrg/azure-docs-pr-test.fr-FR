---
title: "Exemple de script Azure PowerShell - Homologuer deux réseaux virtuels | Microsoft Docs"
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
ms.openlocfilehash: 51c0b98727e148671cfd7ab2b31ffd1c705d8a4e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="peer-two-virtual-networks"></a><span data-ttu-id="b50ea-103">Homologuer deux réseaux virtuels</span><span class="sxs-lookup"><span data-stu-id="b50ea-103">Peer two virtual networks</span></span>

<span data-ttu-id="b50ea-104">Ce script crée et connecte deux réseaux virtuels dans la même région via le réseau Azure.</span><span class="sxs-lookup"><span data-stu-id="b50ea-104">This script creates and connects two virtual networks in the same region trhough the Azure network.</span></span> <span data-ttu-id="b50ea-105">Après l’exécution du script, vous créerez une homologation entre deux réseaux virtuels.</span><span class="sxs-lookup"><span data-stu-id="b50ea-105">After running the script, you will create a peering between two virtual networks.</span></span>

<span data-ttu-id="b50ea-106">Si nécessaire, installez Azure PowerShell à l’aide des instructions figurant dans le [Guide Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), puis exécutez `Login-AzureRmAccount` pour créer une connexion avec Azure.</span><span class="sxs-lookup"><span data-stu-id="b50ea-106">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="b50ea-107">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="b50ea-107">Sample script</span></span>

<span data-ttu-id="b50ea-108">[!code-azurepowershell[main](../../../powershell_scripts/virtual-network/peer-two-virtual-networks/peer-two-virtual-networks.ps1 "Homologuer deux réseaux")]</span><span class="sxs-lookup"><span data-stu-id="b50ea-108">[!code-azurepowershell[main](../../../powershell_scripts/virtual-network/peer-two-virtual-networks/peer-two-virtual-networks.ps1 "Peer two networks")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="b50ea-109">Nettoyer le déploiement</span><span class="sxs-lookup"><span data-stu-id="b50ea-109">Clean up deployment</span></span> 

<span data-ttu-id="b50ea-110">Exécutez la commande suivante pour supprimer le groupe de ressources, la machine virtuelle et toutes les ressources associées.</span><span class="sxs-lookup"><span data-stu-id="b50ea-110">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="b50ea-111">Explication du script</span><span class="sxs-lookup"><span data-stu-id="b50ea-111">Script explanation</span></span>

<span data-ttu-id="b50ea-112">Ce script utilise les commandes suivantes pour créer un groupe de ressources, une machine virtuelle et toutes les ressources associées.</span><span class="sxs-lookup"><span data-stu-id="b50ea-112">This script uses the following commands to create a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="b50ea-113">Chaque commande du tableau renvoie à une documentation spécifique.</span><span class="sxs-lookup"><span data-stu-id="b50ea-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="b50ea-114">Commande</span><span class="sxs-lookup"><span data-stu-id="b50ea-114">Command</span></span> | <span data-ttu-id="b50ea-115">Remarques</span><span class="sxs-lookup"><span data-stu-id="b50ea-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="b50ea-116">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="b50ea-116">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="b50ea-117">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="b50ea-117">Creates a resource group in which all resources are stored.</span></span> | 
| [<span data-ttu-id="b50ea-118">New-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="b50ea-118">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork)| <span data-ttu-id="b50ea-119">Crée un réseau virtuel et un sous-réseau Azure.</span><span class="sxs-lookup"><span data-stu-id="b50ea-119">Creates an Azure virtual network and subnet.</span></span> |
| [<span data-ttu-id="b50ea-120">Add-AzureRmVirtualNetworkPeering</span><span class="sxs-lookup"><span data-stu-id="b50ea-120">Add-AzureRmVirtualNetworkPeering</span></span>](/powershell/module/azurerm.network/add-azurermvirtualnetworkpeering) | <span data-ttu-id="b50ea-121">Crée une homologation entre deux réseaux virtuels.</span><span class="sxs-lookup"><span data-stu-id="b50ea-121">Creates a peering between two virtual networks.</span></span>  |
| [<span data-ttu-id="b50ea-122">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="b50ea-122">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="b50ea-123">Supprime un groupe de ressources, y compris toutes les ressources imbriquées.</span><span class="sxs-lookup"><span data-stu-id="b50ea-123">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="b50ea-124">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b50ea-124">Next steps</span></span>

<span data-ttu-id="b50ea-125">Pour plus d’informations sur Azure PowerShell, consultez la [documentation Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="b50ea-125">For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azure/overview).</span></span>

<span data-ttu-id="b50ea-126">Vous pouvez trouver des exemples supplémentaires de scripts PowerShell de mise en réseau dans la [documentation Vue d’ensemble de la mise en réseau Azure](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b50ea-126">Additional networking PowerShell script samples can be found in the [Azure Networking Overview documentation](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span></span>