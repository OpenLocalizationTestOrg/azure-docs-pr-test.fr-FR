---
title: "exemple de script PowerShell aaaAzure - acheminer le trafic via un matériel de réseau virtuel | Documents Microsoft"
description: "Exemple de script Azure PowerShell - Acheminer le trafic via une appliance virtuelle réseau de pare-feu."
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
ms.openlocfilehash: 3b999f3289d654c00d5becb973e2883896457d52
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="route-traffic-through-a-network-virtual-appliance"></a><span data-ttu-id="c9caf-103">Acheminer le trafic via une appliance virtuelle réseau</span><span class="sxs-lookup"><span data-stu-id="c9caf-103">Route traffic through a network virtual appliance</span></span>

<span data-ttu-id="c9caf-104">Cet exemple de script permet de créer un réseau virtuel avec des sous-réseaux frontaux et principaux.</span><span class="sxs-lookup"><span data-stu-id="c9caf-104">This script sample creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="c9caf-105">Il crée également un ordinateur virtuel IP le trafic tooroute activé entre deux sous-réseaux de hello.</span><span class="sxs-lookup"><span data-stu-id="c9caf-105">It also creates a VM with IP forwarding enabled tooroute traffic between hello two subnets.</span></span> <span data-ttu-id="c9caf-106">Après avoir exécuté le script de hello, vous pouvez déployer un logiciel réseau, telle qu’une application de pare-feu, toohello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="c9caf-106">After running hello script you can deploy network software, such as a firewall application, toohello VM.</span></span>

<span data-ttu-id="c9caf-107">Si nécessaire, installez hello Azure PowerShell en utilisant une instruction de hello trouvé dans hello [guide Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), puis exécutez `Login-AzureRmAccount` toocreate une connexion avec Azure.</span><span class="sxs-lookup"><span data-stu-id="c9caf-107">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="c9caf-108">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="c9caf-108">Sample script</span></span>


[!code-powershell[main](../../../powershell_scripts/virtual-network/route-traffic-through-nva/route-traffic-through-nva.ps1 "Route traffic through a network virtual appliance")]

## <a name="clean-up-deployment"></a><span data-ttu-id="c9caf-109">Nettoyer le déploiement</span><span class="sxs-lookup"><span data-stu-id="c9caf-109">Clean up deployment</span></span> 

<span data-ttu-id="c9caf-110">Exécutez hello suivant du groupe de ressources de commande tooremove hello, machine virtuelle et toutes les ressources.</span><span class="sxs-lookup"><span data-stu-id="c9caf-110">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```
## <a name="script-explanation"></a><span data-ttu-id="c9caf-111">Explication du script</span><span class="sxs-lookup"><span data-stu-id="c9caf-111">Script explanation</span></span>

<span data-ttu-id="c9caf-112">Ce script utilise hello suivant de commandes toocreate un groupe de ressources, de réseau virtuel et de groupes de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="c9caf-112">This script uses hello following commands toocreate a resource group, virtual network,  and network security groups.</span></span> <span data-ttu-id="c9caf-113">Chaque commande dans la table de hello lie documentation toocommand spécifique.</span><span class="sxs-lookup"><span data-stu-id="c9caf-113">Each command in hello table links toocommand-specific documentation.</span></span>

| <span data-ttu-id="c9caf-114">Commande</span><span class="sxs-lookup"><span data-stu-id="c9caf-114">Command</span></span> | <span data-ttu-id="c9caf-115">Remarques</span><span class="sxs-lookup"><span data-stu-id="c9caf-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="c9caf-116">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="c9caf-116">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup)  | <span data-ttu-id="c9caf-117">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="c9caf-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="c9caf-118">New-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="c9caf-118">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="c9caf-119">Crée un réseau virtuel et un sous-réseau frontal Azure.</span><span class="sxs-lookup"><span data-stu-id="c9caf-119">Creates an Azure virtual network and front-end subnet.</span></span> |
| [<span data-ttu-id="c9caf-120">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="c9caf-120">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="c9caf-121">Crée des sous-réseaux principaux et DMZ.</span><span class="sxs-lookup"><span data-stu-id="c9caf-121">Creates back-end and DMZ subnets.</span></span> |
| [<span data-ttu-id="c9caf-122">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="c9caf-122">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="c9caf-123">Crée un Bonjour de tooaccess adresse IP publique machine virtuelle à partir de hello Internet.</span><span class="sxs-lookup"><span data-stu-id="c9caf-123">Creates a public IP address tooaccess hello VM from hello Internet.</span></span> |
| [<span data-ttu-id="c9caf-124">New-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="c9caf-124">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="c9caf-125">Crée une interface réseau virtuelle et active le transfert IP pour celle-ci.</span><span class="sxs-lookup"><span data-stu-id="c9caf-125">Creates a virtual network interface and enable IP forwarding for it.</span></span> |
| [<span data-ttu-id="c9caf-126">New-AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="c9caf-126">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="c9caf-127">Crée un groupe de sécurité réseau (NSG).</span><span class="sxs-lookup"><span data-stu-id="c9caf-127">Creates a network security group (NSG).</span></span> |
| [<span data-ttu-id="c9caf-128">New-AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="c9caf-128">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="c9caf-129">Crée des règles de groupe de sécurité réseau qui autorise les ports HTTP et HTTPS entrant toohello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="c9caf-129">Creates NSG rules that allow HTTP and HTTPS ports inbound toohello VM.</span></span> |
| [<span data-ttu-id="c9caf-130">Set-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="c9caf-130">Set-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig)| <span data-ttu-id="c9caf-131">Associe hello des groupes de sécurité réseau et toosubnets des tables de routage.</span><span class="sxs-lookup"><span data-stu-id="c9caf-131">Associates hello NSGs and route tables toosubnets.</span></span> |
| [<span data-ttu-id="c9caf-132">New-AzureRmRouteTable</span><span class="sxs-lookup"><span data-stu-id="c9caf-132">New-AzureRmRouteTable</span></span>](/powershell/module/azurerm.network/new-azurermroutetable)| <span data-ttu-id="c9caf-133">Crée une table de routage pour tous les itinéraires.</span><span class="sxs-lookup"><span data-stu-id="c9caf-133">Creates a route table for all routes.</span></span> |
| [<span data-ttu-id="c9caf-134">New-AzureRMRouteConfig</span><span class="sxs-lookup"><span data-stu-id="c9caf-134">New-AzureRMRouteConfig</span></span>](/powershell/module/azurerm.network/new-azurermrouteconfig)| <span data-ttu-id="c9caf-135">Crée des itinéraires tooroute un trafic entre les sous-réseaux et hello Internet via hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="c9caf-135">Creates routes tooroute traffic between subnets and hello Internet through hello VM.</span></span> |
| [<span data-ttu-id="c9caf-136">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="c9caf-136">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="c9caf-137">Crée une machine virtuelle et attache hello NIC tooit.</span><span class="sxs-lookup"><span data-stu-id="c9caf-137">Creates a virtual machine and attaches hello NIC tooit.</span></span> <span data-ttu-id="c9caf-138">Cette commande spécifie également hello machine virtuelle image toouse et les informations d’identification administratives.</span><span class="sxs-lookup"><span data-stu-id="c9caf-138">This command also specifies hello virtual machine image toouse and administrative credentials.</span></span> |
| [<span data-ttu-id="c9caf-139">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="c9caf-139">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup)  | <span data-ttu-id="c9caf-140">Supprime un groupe de ressources, ainsi que toutes ses ressources.</span><span class="sxs-lookup"><span data-stu-id="c9caf-140">Deletes a resource group and all resources it contains.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="c9caf-141">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c9caf-141">Next steps</span></span>

<span data-ttu-id="c9caf-142">Pour plus d’informations sur hello Azure PowerShell, consultez [documentation Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c9caf-142">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azure/overview).</span></span>

<span data-ttu-id="c9caf-143">Vous trouverez des exemples de script PowerShell mise en réseau supplémentaires dans hello [documentation de vue d’ensemble de la mise en réseau Azure](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c9caf-143">Additional networking PowerShell script samples can be found in hello [Azure Networking Overview documentation](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span></span>
