---
title: "aaaOpen ports tooa machine virtuelle à l’aide d’Azure PowerShell | Documents Microsoft"
description: "Découvrez comment tooopen un port / créer un point de terminaison de tooyour machine virtuelle Windows à l’aide du mode de déploiement de gestionnaire de ressources Azure hello et Azure PowerShell"
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: cf45f7d8-451a-48ab-8419-730366d54f1e
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 08/21/2017
ms.author: iainfou
ms.openlocfilehash: c1817a0c447ae4ce7a1ce2a1fc6927bedf2dacb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooopen-ports-and-endpoints-tooa-vm-in-azure-using-powershell"></a><span data-ttu-id="a4ccb-103">Comment tooopen tooa de ports et les points de terminaison de machine virtuelle dans Azure à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="a4ccb-103">How tooopen ports and endpoints tooa VM in Azure using PowerShell</span></span>
[!INCLUDE [virtual-machines-common-nsg-quickstart](../../../includes/virtual-machines-common-nsg-quickstart.md)]

## <a name="quick-commands"></a><span data-ttu-id="a4ccb-104">Commandes rapides</span><span class="sxs-lookup"><span data-stu-id="a4ccb-104">Quick commands</span></span>
<span data-ttu-id="a4ccb-105">Groupe de sécurité réseau toocreate et ACL des règles [version la plus récente d’Azure PowerShell est installé hello](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="a4ccb-105">toocreate a Network Security Group and ACL rules you need [hello latest version of Azure PowerShell installed](/powershell/azureps-cmdlets-docs).</span></span> <span data-ttu-id="a4ccb-106">Vous pouvez également [effectuer ces étapes à l’aide de hello Azure portal](nsg-quickstart-portal.md).</span><span class="sxs-lookup"><span data-stu-id="a4ccb-106">You can also [perform these steps using hello Azure portal](nsg-quickstart-portal.md).</span></span>

<span data-ttu-id="a4ccb-107">Ouvrez une session dans tooyour compte Azure :</span><span class="sxs-lookup"><span data-stu-id="a4ccb-107">Log in tooyour Azure account:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="a4ccb-108">Bonjour les exemples suivants, remplacez les exemples de noms de paramètre par vos propres valeurs.</span><span class="sxs-lookup"><span data-stu-id="a4ccb-108">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="a4ccb-109">Les exemples de noms de paramètre comprennent *myResourceGroup*, *myNetworkSecurityGroup* et *myVMnet*.</span><span class="sxs-lookup"><span data-stu-id="a4ccb-109">Example parameter names included *myResourceGroup*, *myNetworkSecurityGroup*, and *myVnet*.</span></span>

<span data-ttu-id="a4ccb-110">Créez une règle avec [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig).</span><span class="sxs-lookup"><span data-stu-id="a4ccb-110">Create a rule with [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig).</span></span> <span data-ttu-id="a4ccb-111">Hello exemple suivant crée une règle nommée *myNetworkSecurityGroupRule* tooallow *tcp* le trafic sur le port *80*:</span><span class="sxs-lookup"><span data-stu-id="a4ccb-111">hello following example creates a rule named *myNetworkSecurityGroupRule* tooallow *tcp* traffic on port *80*:</span></span>

```powershell
$httprule = New-AzureRmNetworkSecurityRuleConfig `
    -Name "myNetworkSecurityGroupRule" `
    -Description "Allow HTTP" `
    -Access "Allow" `
    -Protocol "Tcp" `
    -Direction "Inbound" `
    -Priority "100" `
    -SourceAddressPrefix "Internet" `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 80
```

<span data-ttu-id="a4ccb-112">Ensuite, créez un groupe de sécurité réseau par [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) et affecter hello HTTP règle vous venez de créer comme suit.</span><span class="sxs-lookup"><span data-stu-id="a4ccb-112">Next, create your Network Security group with [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) and assign hello HTTP rule you just created as follows.</span></span> <span data-ttu-id="a4ccb-113">Hello exemple suivant crée un groupe de sécurité réseau nommé *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="a4ccb-113">hello following example creates a Network Security Group named *myNetworkSecurityGroup*:</span></span>

```powershell
$nsg = New-AzureRmNetworkSecurityGroup `
    -ResourceGroupName "myResourceGroup" `
    -Location "EastUS" `
    -Name "myNetworkSecurityGroup" `
    -SecurityRules $httprule
```

<span data-ttu-id="a4ccb-114">Maintenant nous allons affecter votre sous-réseau tooa de groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="a4ccb-114">Now let's assign your Network Security Group tooa subnet.</span></span> <span data-ttu-id="a4ccb-115">exemple Hello affecte un réseau virtuel existant nommé *myVnet* toohello variable *$vnet* avec [Get-AzureRmVirtualNetwork](/powershell/module/azurerm.network/get-azurermvirtualnetwork):</span><span class="sxs-lookup"><span data-stu-id="a4ccb-115">hello following example assigns an existing virtual network named *myVnet* toohello variable *$vnet* with [Get-AzureRmVirtualNetwork](/powershell/module/azurerm.network/get-azurermvirtualnetwork):</span></span>

```powershell
$vnet = Get-AzureRmVirtualNetwork `
    -ResourceGroupName "myResourceGroup" `
    -Name "myVnet"
```

<span data-ttu-id="a4ccb-116">Associez votre groupe de sécurité réseau à votre sous-réseau avec [Set-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig).</span><span class="sxs-lookup"><span data-stu-id="a4ccb-116">Associate your Network Security Group with your subnet with [Set-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig).</span></span> <span data-ttu-id="a4ccb-117">exemple Hello associe sous-réseau hello nommé *mySubnet* avec votre groupe de sécurité réseau :</span><span class="sxs-lookup"><span data-stu-id="a4ccb-117">hello following example associates hello subnet named *mySubnet* with your Network Security Group:</span></span>

```powershell
$subnetPrefix = $vnet.Subnets|?{$_.Name -eq 'mySubnet'}

Set-AzureRmVirtualNetworkSubnetConfig `
    -VirtualNetwork $vnet `
    -Name "mySubnet" `
    -AddressPrefix $subnetPrefix.AddressPrefix `
    -NetworkSecurityGroup $nsg
```

<span data-ttu-id="a4ccb-118">Enfin, mettre à jour votre réseau virtuel avec [Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork) afin que l’effet de tootake de modifications :</span><span class="sxs-lookup"><span data-stu-id="a4ccb-118">Finally, update your virtual network with [Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork) in order for your changes tootake effect:</span></span>

```powershell
Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
```


## <a name="more-information-on-network-security-groups"></a><span data-ttu-id="a4ccb-119">En savoir plus sur les groupes de sécurité réseau</span><span class="sxs-lookup"><span data-stu-id="a4ccb-119">More information on Network Security Groups</span></span>
<span data-ttu-id="a4ccb-120">Hello rapide commandes vous permettent de tooget haut et en cours d’exécution avec tooyour de flux de trafic VM.</span><span class="sxs-lookup"><span data-stu-id="a4ccb-120">hello quick commands here allow you tooget up and running with traffic flowing tooyour VM.</span></span> <span data-ttu-id="a4ccb-121">Groupes de sécurité réseau fournissent de nombreuses fonctionnalités et granularité pour contrôler les ressources tooyour accès.</span><span class="sxs-lookup"><span data-stu-id="a4ccb-121">Network Security Groups provide many great features and granularity for controlling access tooyour resources.</span></span> <span data-ttu-id="a4ccb-122">Découvrez plus d’informations sur la [création d’un groupe de sécurité réseau et de règles de liste de contrôle d’accès ici](tutorial-virtual-network.md#manage-internal-traffic).</span><span class="sxs-lookup"><span data-stu-id="a4ccb-122">You can read more about [creating a Network Security Group and ACL rules here](tutorial-virtual-network.md#manage-internal-traffic).</span></span>

<span data-ttu-id="a4ccb-123">Pour les applications Web hautement disponibles, vous devez placer vos machines virtuelles derrière un équilibreur de charge Azure.</span><span class="sxs-lookup"><span data-stu-id="a4ccb-123">For highly available web applications, you should place your VMs behind an Azure Load Balancer.</span></span> <span data-ttu-id="a4ccb-124">équilibrage de charge Hello distribue tooVMs le trafic, avec un groupe de sécurité réseau qui fournit un filtrage du trafic.</span><span class="sxs-lookup"><span data-stu-id="a4ccb-124">hello load balancer distributes traffic tooVMs, with a Network Security Group that provides traffic filtering.</span></span> <span data-ttu-id="a4ccb-125">Pour plus d’informations, consultez [comment le solde tooload Linux virtual machines dans Azure toocreate une application hautement disponible](tutorial-load-balancer.md).</span><span class="sxs-lookup"><span data-stu-id="a4ccb-125">For more information, see [How tooload balance Linux virtual machines in Azure toocreate a highly available application](tutorial-load-balancer.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a4ccb-126">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a4ccb-126">Next steps</span></span>
<span data-ttu-id="a4ccb-127">Dans cet exemple, vous avez créé un trafic de tooallow HTTP règle simple.</span><span class="sxs-lookup"><span data-stu-id="a4ccb-127">In this example, you created a simple rule tooallow HTTP traffic.</span></span> <span data-ttu-id="a4ccb-128">Vous trouverez des informations sur la création d’environnements plus Bonjour suivant des articles :</span><span class="sxs-lookup"><span data-stu-id="a4ccb-128">You can find information on creating more detailed environments in hello following articles:</span></span>

* [<span data-ttu-id="a4ccb-129">Présentation d’Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="a4ccb-129">Azure Resource Manager overview</span></span>](../../azure-resource-manager/resource-group-overview.md)
* [<span data-ttu-id="a4ccb-130">Présentation du groupe de sécurité réseau</span><span class="sxs-lookup"><span data-stu-id="a4ccb-130">What is a Network Security Group (NSG)?</span></span>](../../virtual-network/virtual-networks-nsg.md)
* [<span data-ttu-id="a4ccb-131">Présentation d’Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="a4ccb-131">Azure Resource Manager Overview for Load Balancers</span></span>](../../load-balancer/load-balancer-arm.md)

