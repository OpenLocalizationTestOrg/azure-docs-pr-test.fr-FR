---
title: "aaaAzure exemple de script PowerShell - créer un réseau pour les applications multicouches | Documents Microsoft"
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
ms.openlocfilehash: 46d6d16dc5dbc8be467359f31346f017727b1abe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-network-for-multi-tier-applications"></a><span data-ttu-id="3b0f2-103">Créer un réseau pour les applications multiniveau</span><span class="sxs-lookup"><span data-stu-id="3b0f2-103">Create a network for multi-tier applications</span></span>

<span data-ttu-id="3b0f2-104">Cet exemple de script permet de créer un réseau virtuel avec des sous-réseaux frontaux et principaux.</span><span class="sxs-lookup"><span data-stu-id="3b0f2-104">This script sample creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="3b0f2-105">Sous-réseau de trafic toohello frontal est limitée tooHTTP et SSH, lors du trafic toohello sous-réseau principal est limitée tooMySQL, port 3306.</span><span class="sxs-lookup"><span data-stu-id="3b0f2-105">Traffic toohello front-end subnet is limited tooHTTP and SSH, while traffic toohello back-end subnet is limited tooMySQL, port 3306.</span></span> <span data-ttu-id="3b0f2-106">Après l’exécution du script hello, vous aurez deux machines virtuelles, une dans chaque sous-réseau que vous pouvez déployer le serveur web et le logiciel MySQL.</span><span class="sxs-lookup"><span data-stu-id="3b0f2-106">After running hello script, you will have two virtual machines, one in each subnet that you can deploy web server and MySQL software to.</span></span>

<span data-ttu-id="3b0f2-107">Si nécessaire, installez hello Azure PowerShell en utilisant une instruction de hello trouvé dans hello [guide Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), puis exécutez `Login-AzureRmAccount` toocreate une connexion avec Azure.</span><span class="sxs-lookup"><span data-stu-id="3b0f2-107">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="3b0f2-108">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="3b0f2-108">Sample script</span></span>


[!code-powershell[main](../../../powershell_scripts/virtual-network/virtual-network-multi-tier-application/virtual-network-multi-tier-application.ps1  "Virtual network for multi-tier application")]

## <a name="clean-up-deployment"></a><span data-ttu-id="3b0f2-109">Nettoyer le déploiement</span><span class="sxs-lookup"><span data-stu-id="3b0f2-109">Clean up deployment</span></span> 

<span data-ttu-id="3b0f2-110">Exécutez hello suivant du groupe de ressources de commande tooremove hello, machine virtuelle et toutes les ressources.</span><span class="sxs-lookup"><span data-stu-id="3b0f2-110">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="3b0f2-111">Explication du script</span><span class="sxs-lookup"><span data-stu-id="3b0f2-111">Script explanation</span></span>

<span data-ttu-id="3b0f2-112">Ce script utilise hello suivant de commandes toocreate un groupe de ressources, de réseau virtuel et de groupes de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="3b0f2-112">This script uses hello following commands toocreate a resource group, virtual network,  and network security groups.</span></span> <span data-ttu-id="3b0f2-113">Chaque commande dans la table de hello lie documentation toocommand spécifique.</span><span class="sxs-lookup"><span data-stu-id="3b0f2-113">Each command in hello table links toocommand-specific documentation.</span></span>

| <span data-ttu-id="3b0f2-114">Commande</span><span class="sxs-lookup"><span data-stu-id="3b0f2-114">Command</span></span> | <span data-ttu-id="3b0f2-115">Remarques</span><span class="sxs-lookup"><span data-stu-id="3b0f2-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="3b0f2-116">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="3b0f2-116">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="3b0f2-117">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="3b0f2-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="3b0f2-118">New-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="3b0f2-118">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="3b0f2-119">Crée un réseau virtuel et un sous-réseau frontal Azure.</span><span class="sxs-lookup"><span data-stu-id="3b0f2-119">Creates an Azure virtual network and front-end subnet.</span></span> |
| [<span data-ttu-id="3b0f2-120">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="3b0f2-120">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="3b0f2-121">Crée un sous-réseau principal.</span><span class="sxs-lookup"><span data-stu-id="3b0f2-121">Creates a back-end subnet.</span></span> |
| [<span data-ttu-id="3b0f2-122">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="3b0f2-122">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="3b0f2-123">Crée un Bonjour de tooaccess adresse IP publique machine virtuelle à partir de hello Internet.</span><span class="sxs-lookup"><span data-stu-id="3b0f2-123">Creates a public IP address tooaccess hello VM from hello Internet.</span></span> |
| [<span data-ttu-id="3b0f2-124">New-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="3b0f2-124">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="3b0f2-125">Crée des interfaces réseau virtuelles et les attacher à des sous-réseaux du réseau virtuel toohello frontaux et principaux.</span><span class="sxs-lookup"><span data-stu-id="3b0f2-125">Creates virtual network interfaces and attaches them toohello virtual network's front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="3b0f2-126">New-AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="3b0f2-126">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="3b0f2-127">Crée des groupes de sécurité réseau (NSG) qui sont des sous-réseaux frontaux et principaux toohello associé.</span><span class="sxs-lookup"><span data-stu-id="3b0f2-127">Creates network security groups (NSG) that are associated toohello front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="3b0f2-128">New-AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="3b0f2-128">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) |<span data-ttu-id="3b0f2-129">Crée des règles de groupe de sécurité réseau autoriser ou bloquent des sous-réseaux toospecific de ports spécifiques.</span><span class="sxs-lookup"><span data-stu-id="3b0f2-129">Creates NSG rules that allow or block specific ports toospecific subnets.</span></span> |
| [<span data-ttu-id="3b0f2-130">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="3b0f2-130">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="3b0f2-131">Crée des machines virtuelles et attache un tooeach de carte réseau virtuelle.</span><span class="sxs-lookup"><span data-stu-id="3b0f2-131">Creates virtual machines and attaches a NIC tooeach VM.</span></span> <span data-ttu-id="3b0f2-132">Cette commande spécifie également hello machine virtuelle image toouse et les informations d’identification administratives.</span><span class="sxs-lookup"><span data-stu-id="3b0f2-132">This command also specifies hello virtual machine image toouse and administrative credentials.</span></span> |
| [<span data-ttu-id="3b0f2-133">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="3b0f2-133">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="3b0f2-134">Supprime un groupe de ressources, ainsi que toutes ses ressources.</span><span class="sxs-lookup"><span data-stu-id="3b0f2-134">Deletes a resource group and all resources it contains.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="3b0f2-135">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="3b0f2-135">Next steps</span></span>

<span data-ttu-id="3b0f2-136">Pour plus d’informations sur hello Azure PowerShell, consultez [documentation Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="3b0f2-136">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azure/overview).</span></span>

<span data-ttu-id="3b0f2-137">Vous trouverez des exemples de script PowerShell mise en réseau supplémentaires dans hello [documentation de vue d’ensemble de la mise en réseau Azure](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3b0f2-137">Additional networking PowerShell script samples can be found in hello [Azure Networking Overview documentation](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span></span>
