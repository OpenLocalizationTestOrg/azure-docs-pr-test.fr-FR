---
title: "exemple de script PowerShell aaaAzure - le trafic réseau de machine virtuelle de filtre | Documents Microsoft"
description: "Exemple de script Azure PowerShell - Filtrer le trafic réseau de machine virtuelle entrant et sortant"
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
ms.openlocfilehash: 39eae6a43a8dc7f9fc616ef3ec50f95443fd3547
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="filter-inbound-and-outbound-vm-network-traffic"></a><span data-ttu-id="7dbd2-103">Filtrer le trafic réseau de machine virtuelle entrant et sortant</span><span class="sxs-lookup"><span data-stu-id="7dbd2-103">Filter inbound and outbound VM network traffic</span></span>

<span data-ttu-id="7dbd2-104">Cet exemple de script permet de créer un réseau virtuel avec des sous-réseaux frontaux et principaux.</span><span class="sxs-lookup"><span data-stu-id="7dbd2-104">This script sample creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="7dbd2-105">Le trafic du réseau entrant toohello le sous-réseau frontal est limitée tooHTTP et HTTPS, pendant sortant du trafic toohello Internet à partir du sous-réseau de hello principal n’est pas autorisée.</span><span class="sxs-lookup"><span data-stu-id="7dbd2-105">Inbound network traffic toohello front-end subnet is limited tooHTTP, and HTTPS, while outbound traffic toohello Internet from hello back-end subnet is not permitted.</span></span> <span data-ttu-id="7dbd2-106">Après avoir exécuté le script de hello, vous aurez une machine virtuelle avec deux cartes réseau.</span><span class="sxs-lookup"><span data-stu-id="7dbd2-106">After running hello script, you will have one virtual machine with two NICs.</span></span> <span data-ttu-id="7dbd2-107">Chaque carte réseau est connectée tooa autre sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="7dbd2-107">Each NIC is connected tooa different subnet.</span></span>

<span data-ttu-id="7dbd2-108">Si nécessaire, installez hello Azure PowerShell en utilisant une instruction de hello trouvé dans hello [guide Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), puis exécutez `Login-AzureRmAccount` toocreate une connexion avec Azure.</span><span class="sxs-lookup"><span data-stu-id="7dbd2-108">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="7dbd2-109">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="7dbd2-109">Sample script</span></span>


[!code-powershell[main](../../../powershell_scripts/virtual-network/filter-network-traffic/filter-network-traffic.ps1  "Filter VM network traffic")]

## <a name="clean-up-deployment"></a><span data-ttu-id="7dbd2-110">Nettoyer le déploiement</span><span class="sxs-lookup"><span data-stu-id="7dbd2-110">Clean up deployment</span></span> 

<span data-ttu-id="7dbd2-111">Exécutez hello suivant du groupe de ressources de commande tooremove hello, machine virtuelle et toutes les ressources.</span><span class="sxs-lookup"><span data-stu-id="7dbd2-111">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="7dbd2-112">Explication du script</span><span class="sxs-lookup"><span data-stu-id="7dbd2-112">Script explanation</span></span>

<span data-ttu-id="7dbd2-113">Ce script utilise hello suivant de commandes toocreate un groupe de ressources, de réseau virtuel et de groupes de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="7dbd2-113">This script uses hello following commands toocreate a resource group, virtual network,  and network security groups.</span></span> <span data-ttu-id="7dbd2-114">Chaque commande dans la table de hello lie documentation toocommand spécifique.</span><span class="sxs-lookup"><span data-stu-id="7dbd2-114">Each command in hello table links toocommand-specific documentation.</span></span>

| <span data-ttu-id="7dbd2-115">Commande</span><span class="sxs-lookup"><span data-stu-id="7dbd2-115">Command</span></span> | <span data-ttu-id="7dbd2-116">Remarques</span><span class="sxs-lookup"><span data-stu-id="7dbd2-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="7dbd2-117">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="7dbd2-117">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="7dbd2-118">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="7dbd2-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="7dbd2-119">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="7dbd2-119">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="7dbd2-120">Crée un objet de configuration de sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="7dbd2-120">Creates a subnet configuration object</span></span> |
| [<span data-ttu-id="7dbd2-121">New-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="7dbd2-121">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="7dbd2-122">Crée un réseau virtuel et un sous-réseau frontal Azure.</span><span class="sxs-lookup"><span data-stu-id="7dbd2-122">Creates an Azure virtual network and front-end subnet.</span></span> |
| [<span data-ttu-id="7dbd2-123">New-AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="7dbd2-123">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="7dbd2-124">Crée un toobe de règles de sécurité attribué tooa groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="7dbd2-124">Creates security rules toobe assigned tooa network security group.</span></span> |
| [<span data-ttu-id="7dbd2-125">New-AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="7dbd2-125">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) |<span data-ttu-id="7dbd2-126">Crée des règles de groupe de sécurité réseau autoriser ou bloquent des sous-réseaux toospecific de ports spécifiques.</span><span class="sxs-lookup"><span data-stu-id="7dbd2-126">Creates NSG rules that allow or block specific ports toospecific subnets.</span></span> |
| [<span data-ttu-id="7dbd2-127">Set-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="7dbd2-127">Set-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="7dbd2-128">Associe les groupes de sécurité réseau toosubnets.</span><span class="sxs-lookup"><span data-stu-id="7dbd2-128">Associates NSGs toosubnets.</span></span> |
| [<span data-ttu-id="7dbd2-129">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="7dbd2-129">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="7dbd2-130">Crée un Bonjour de tooaccess adresse IP publique machine virtuelle à partir de hello Internet.</span><span class="sxs-lookup"><span data-stu-id="7dbd2-130">Creates a public IP address tooaccess hello VM from hello Internet.</span></span> |
| [<span data-ttu-id="7dbd2-131">New-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="7dbd2-131">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="7dbd2-132">Crée des interfaces réseau virtuelles et les attacher à des sous-réseaux du réseau virtuel toohello frontaux et principaux.</span><span class="sxs-lookup"><span data-stu-id="7dbd2-132">Creates virtual network interfaces and attaches them toohello virtual network's front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="7dbd2-133">New-AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="7dbd2-133">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="7dbd2-134">Crée une configuration de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="7dbd2-134">Creates a VM configuration.</span></span> <span data-ttu-id="7dbd2-135">Cette configuration inclut des informations telles que le nom de la machine virtuelle, le système d’exploitation et les informations d’identification d’administration.</span><span class="sxs-lookup"><span data-stu-id="7dbd2-135">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="7dbd2-136">configuration de Hello est utilisée lors de la création de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="7dbd2-136">hello configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="7dbd2-137">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="7dbd2-137">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="7dbd2-138">Création d’une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="7dbd2-138">Create a virtual machine.</span></span> |
|[<span data-ttu-id="7dbd2-139">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="7dbd2-139">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="7dbd2-140">Supprime un groupe de ressources et toutes les ressources contenues.</span><span class="sxs-lookup"><span data-stu-id="7dbd2-140">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="7dbd2-141">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="7dbd2-141">Next steps</span></span>

<span data-ttu-id="7dbd2-142">Pour plus d’informations sur hello Azure PowerShell, consultez [documentation Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="7dbd2-142">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azure/overview).</span></span>

<span data-ttu-id="7dbd2-143">Vous trouverez des exemples de script PowerShell mise en réseau supplémentaires dans hello [documentation de vue d’ensemble de la mise en réseau Azure](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7dbd2-143">Additional networking PowerShell script samples can be found in hello [Azure Networking Overview documentation](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span></span>
