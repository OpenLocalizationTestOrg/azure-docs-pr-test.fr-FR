---
title: "Exemple de script Azure PowerShell - Créer un réseau pour les applications multiniveau | Microsoft Docs"
description: "Exemple de script Azure PowerShell - Créer un réseau pour les applications multiniveau."
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
ms.openlocfilehash: ab49e78ef17b093d2bbe4e3276a1ece3a4247f91
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-network-for-multi-tier-applications"></a><span data-ttu-id="aa520-103">Créer un réseau pour les applications multiniveau</span><span class="sxs-lookup"><span data-stu-id="aa520-103">Create a network for multi-tier applications</span></span>

<span data-ttu-id="aa520-104">Cet exemple de script permet de créer un réseau virtuel avec des sous-réseaux frontaux et principaux.</span><span class="sxs-lookup"><span data-stu-id="aa520-104">This script sample creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="aa520-105">Le trafic vers le sous-réseau frontal est limité à HTTP et SSH, tandis que le trafic vers le sous-réseau principal est limité à MySQL, port 3306.</span><span class="sxs-lookup"><span data-stu-id="aa520-105">Traffic to the front-end subnet is limited to HTTP and SSH, while traffic to the back-end subnet is limited to MySQL, port 3306.</span></span> <span data-ttu-id="aa520-106">Après avoir exécuté le script, vous obtenez deux machines virtuelles, une dans chaque sous-réseau sur laquelle que vous pouvez déployer le serveur web et le logiciel MySQL.</span><span class="sxs-lookup"><span data-stu-id="aa520-106">After running the script, you will have two virtual machines, one in each subnet that you can deploy web server and MySQL software to.</span></span>

<span data-ttu-id="aa520-107">Si nécessaire, installez Azure PowerShell à l’aide des instructions figurant dans le [Guide Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), puis exécutez `Login-AzureRmAccount` pour créer une connexion avec Azure.</span><span class="sxs-lookup"><span data-stu-id="aa520-107">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="aa520-108">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="aa520-108">Sample script</span></span>


<span data-ttu-id="aa520-109">[!code-powershell[principal](../../../powershell_scripts/virtual-network/virtual-network-multi-tier-application/virtual-network-multi-tier-application.ps1  "Créer un réseau virtuel pour les applications multiniveau")]</span><span class="sxs-lookup"><span data-stu-id="aa520-109">[!code-powershell[main](../../../powershell_scripts/virtual-network/virtual-network-multi-tier-application/virtual-network-multi-tier-application.ps1  "Virtual network for multi-tier application")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="aa520-110">Nettoyer le déploiement</span><span class="sxs-lookup"><span data-stu-id="aa520-110">Clean up deployment</span></span> 

<span data-ttu-id="aa520-111">Exécutez la commande suivante pour supprimer le groupe de ressources, la machine virtuelle et toutes les ressources associées.</span><span class="sxs-lookup"><span data-stu-id="aa520-111">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="aa520-112">Explication du script</span><span class="sxs-lookup"><span data-stu-id="aa520-112">Script explanation</span></span>

<span data-ttu-id="aa520-113">Ce script utilise les commandes suivantes pour créer un groupe de ressources, un réseau virtuel et les groupes de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="aa520-113">This script uses the following commands to create a resource group, virtual network,  and network security groups.</span></span> <span data-ttu-id="aa520-114">Chaque commande de la table renvoie à une documentation spécifique.</span><span class="sxs-lookup"><span data-stu-id="aa520-114">Each command in the table links to command-specific documentation.</span></span>

| <span data-ttu-id="aa520-115">Commande</span><span class="sxs-lookup"><span data-stu-id="aa520-115">Command</span></span> | <span data-ttu-id="aa520-116">Remarques</span><span class="sxs-lookup"><span data-stu-id="aa520-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="aa520-117">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="aa520-117">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="aa520-118">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="aa520-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="aa520-119">New-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="aa520-119">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="aa520-120">Crée un réseau virtuel et un sous-réseau frontal Azure.</span><span class="sxs-lookup"><span data-stu-id="aa520-120">Creates an Azure virtual network and front-end subnet.</span></span> |
| [<span data-ttu-id="aa520-121">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="aa520-121">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="aa520-122">Crée un sous-réseau principal.</span><span class="sxs-lookup"><span data-stu-id="aa520-122">Creates a back-end subnet.</span></span> |
| [<span data-ttu-id="aa520-123">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="aa520-123">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="aa520-124">Crée une adresse IP publique pour accéder à la machine virtuelle à partir d’Internet.</span><span class="sxs-lookup"><span data-stu-id="aa520-124">Creates a public IP address to access the VM from the Internet.</span></span> |
| [<span data-ttu-id="aa520-125">New-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="aa520-125">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="aa520-126">Crée des interfaces réseau virtuelles et les attache aux sous-réseaux frontaux et principaux du réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="aa520-126">Creates virtual network interfaces and attaches them to the virtual network's front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="aa520-127">New-AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="aa520-127">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="aa520-128">Crée des groupes de sécurité réseau (NSG) associés aux sous-réseaux frontaux et principaux.</span><span class="sxs-lookup"><span data-stu-id="aa520-128">Creates network security groups (NSG) that are associated to the front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="aa520-129">New-AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="aa520-129">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) |<span data-ttu-id="aa520-130">Crée des règles NSG qui autorisent ou bloquent des ports spécifiques sur des sous-réseaux donnés.</span><span class="sxs-lookup"><span data-stu-id="aa520-130">Creates NSG rules that allow or block specific ports to specific subnets.</span></span> |
| [<span data-ttu-id="aa520-131">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="aa520-131">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="aa520-132">Crée des machines virtuelles et associe une carte d’interface réseau à chacune d’elles.</span><span class="sxs-lookup"><span data-stu-id="aa520-132">Creates virtual machines and attaches a NIC to each VM.</span></span> <span data-ttu-id="aa520-133">Cette commande spécifie également l’image de machine virtuelle à utiliser ainsi que les informations d’identification d’administration.</span><span class="sxs-lookup"><span data-stu-id="aa520-133">This command also specifies the virtual machine image to use and administrative credentials.</span></span> |
| [<span data-ttu-id="aa520-134">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="aa520-134">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="aa520-135">Supprime un groupe de ressources, ainsi que toutes ses ressources.</span><span class="sxs-lookup"><span data-stu-id="aa520-135">Deletes a resource group and all resources it contains.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="aa520-136">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="aa520-136">Next steps</span></span>

<span data-ttu-id="aa520-137">Pour plus d’informations sur Azure PowerShell, consultez la [documentation Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="aa520-137">For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azure/overview).</span></span>

<span data-ttu-id="aa520-138">Vous pouvez trouver des exemples supplémentaires de scripts PowerShell de mise en réseau dans la [documentation Vue d’ensemble de la mise en réseau Azure](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="aa520-138">Additional networking PowerShell script samples can be found in the [Azure Networking Overview documentation](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span></span>