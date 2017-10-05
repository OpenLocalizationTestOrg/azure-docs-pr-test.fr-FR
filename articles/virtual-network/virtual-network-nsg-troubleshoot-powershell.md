---
title: "Résoudre les problèmes relatifs aux groupes de sécurité réseau - PowerShell | Microsoft Docs"
description: "Découvrez comment résoudre les problèmes liés aux groupes de sécurité réseau dans le modèle de déploiement Azure Resource Manager à l’aide d’Azure PowerShell."
services: virtual-network
documentationcenter: na
author: AnithaAdusumilli
manager: narayan
editor: 
tags: azure-resource-manager
ms.assetid: 4c732bb7-5cb1-40af-9e6d-a2a307c2a9c4
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/23/2016
ms.author: anithaa
ms.openlocfilehash: 5edaf7197576ac1c0bd1fc6bed21fd65ed135106
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-network-security-groups-using-azure-powershell"></a><span data-ttu-id="3b551-103">Résoudre les groupes de sécurité réseau à l’aide d’Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="3b551-103">Troubleshoot Network Security Groups using Azure PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3b551-104">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="3b551-104">Azure Portal</span></span>](virtual-network-nsg-troubleshoot-portal.md)
> * [<span data-ttu-id="3b551-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3b551-105">PowerShell</span></span>](virtual-network-nsg-troubleshoot-powershell.md)
> 
> 

<span data-ttu-id="3b551-106">Si vous avez configuré des groupes de sécurité réseau sur votre machine virtuelle et rencontrez des problèmes de connectivité de machine virtuelle, cet article fournit une vue d’ensemble des fonctionnalités de diagnostic pour les groupes de sécurité réseau afin de vous aider à dépanner.</span><span class="sxs-lookup"><span data-stu-id="3b551-106">If you configured Network Security Groups (NSGs) on your virtual machine (VM) and are experiencing VM connectivity issues, this article provides an overview of diagnostics capabilities for NSGs to help troubleshoot further.</span></span>

<span data-ttu-id="3b551-107">Les groupes de sécurité réseau vous permettent de contrôler les types de trafic transitant sur vos machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="3b551-107">NSGs enable you to control the types of traffic that flow in and out of your virtual machines (VMs).</span></span> <span data-ttu-id="3b551-108">Des groupes de sécurité réseau peuvent être appliqués à des sous-réseaux d’un réseau virtuel Azure (VNet), à des cartes réseau ou aux deux.</span><span class="sxs-lookup"><span data-stu-id="3b551-108">NSGs can be applied to subnets in an Azure Virtual Network (VNet), network interfaces (NIC), or both.</span></span> <span data-ttu-id="3b551-109">Les règles effectives appliquées à une carte réseau sont une agrégation de règles existant dans les groupes de sécurité réseau appliqués à une carte réseau et au sous-réseau auquel elle est connectée.</span><span class="sxs-lookup"><span data-stu-id="3b551-109">The effective rules applied to a NIC are an aggregation of the rules that exist in the NSGs applied to a NIC and the subnet it is connected to.</span></span> <span data-ttu-id="3b551-110">Les règles appliquées à ces groupes de sécurité réseau sont parfois en conflit entre elles et peuvent avoir une incidence sur la connectivité réseau d’une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="3b551-110">Rules across these NSGs can sometimes conflict with each other and impact a VM's network connectivity.</span></span>  

<span data-ttu-id="3b551-111">Vous pouvez afficher toutes les règles de sécurité effectives de vos groupes de sécurité réseau, telles qu’appliquées aux cartes réseau de votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="3b551-111">You can view all the effective security rules from your NSGs, as applied on your VM's NICs.</span></span> <span data-ttu-id="3b551-112">Cet article explique comment résoudre les problèmes de connectivité de machine virtuelle à l’aide de ces règles dans le modèle de déploiement Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="3b551-112">This article shows how to troubleshoot VM connectivity issues using these rules in the Azure Resource Manager deployment model.</span></span> <span data-ttu-id="3b551-113">Si vous n’êtes pas familiarisé avec les concepts de réseau virtuel et de groupe de sécurité réseau, lisez les articles de présentation [Réseau virtuel](virtual-networks-overview.md) et [Groupes de sécurité réseau](virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="3b551-113">If you're not familiar with VNet and NSG concepts, read the [Virtual network](virtual-networks-overview.md) and [Network security groups](virtual-networks-nsg.md) overview articles.</span></span>

## <a name="using-effective-security-rules-to-troubleshoot-vm-traffic-flow"></a><span data-ttu-id="3b551-114">Utilisation de règles de sécurité effectives pour résoudre des problèmes de flux de trafic de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="3b551-114">Using Effective Security Rules to troubleshoot VM traffic flow</span></span>
<span data-ttu-id="3b551-115">Le scénario qui suit illustre un problème de connexion courant :</span><span class="sxs-lookup"><span data-stu-id="3b551-115">The scenario that follows is an example of a common connection problem:</span></span>

<span data-ttu-id="3b551-116">Une machine virtuelle nommée *VM1* fait partie d’un sous-réseau nommé *Subnet1* au sein d’un réseau virtuel nommé *WestUS-VNet1*.</span><span class="sxs-lookup"><span data-stu-id="3b551-116">A VM named *VM1* is part of a subnet named *Subnet1* within a VNet named *WestUS-VNet1*.</span></span> <span data-ttu-id="3b551-117">Une tentative de connexion à la machine virtuelle à l’aide du protocole RDP sur le port TCP 3389 a échoué.</span><span class="sxs-lookup"><span data-stu-id="3b551-117">An attempt to connect to the VM using RDP over TCP port 3389 fails.</span></span> <span data-ttu-id="3b551-118">Des groupes de sécurité réseau sont appliqués tant à la carte réseau *VM1-NIC1* qu’au sous-réseau *Subnet1*.</span><span class="sxs-lookup"><span data-stu-id="3b551-118">NSGs are applied at both the NIC *VM1-NIC1* and the subnet *Subnet1*.</span></span> <span data-ttu-id="3b551-119">Le trafic vers le port TCP 3389 est autorisé dans le groupe de sécurité réseau associé à l’interface réseau *VM1-NIC1*. Toutefois, le test Ping du port TCP 3389 de VM1 échoue.</span><span class="sxs-lookup"><span data-stu-id="3b551-119">Traffic to TCP port 3389 is allowed in the NSG associated with the network interface *VM1-NIC1*, however TCP ping to VM1's port 3389 fails.</span></span>

<span data-ttu-id="3b551-120">Bien que cet exemple utilise le port TCP 3389, les étapes suivantes permettent de déterminer les échecs de connexion entrante et sortante sur n’importe quel port.</span><span class="sxs-lookup"><span data-stu-id="3b551-120">While this example uses TCP port 3389, the following steps can be used to determine inbound and outbound connection failures over any port.</span></span>

## <a name="detailed-troubleshooting-steps"></a><span data-ttu-id="3b551-121">Étapes de dépannage détaillées</span><span class="sxs-lookup"><span data-stu-id="3b551-121">Detailed Troubleshooting Steps</span></span>
<span data-ttu-id="3b551-122">Pour dépanner des groupes de sécurité réseau pour une machine virtuelle, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="3b551-122">Complete the following steps to troubleshoot NSGs for a VM:</span></span>

1. <span data-ttu-id="3b551-123">Démarrez une session Azure PowerShell et connectez-vous à Azure.</span><span class="sxs-lookup"><span data-stu-id="3b551-123">Start an Azure PowerShell session and login to Azure.</span></span> <span data-ttu-id="3b551-124">Si vous n’êtes pas familiarisé avec l’utilisation d’Azure PowerShell, lisez l’article [Installation et configuration d’Azure PowerShell](/powershell/azure/overview) .</span><span class="sxs-lookup"><span data-stu-id="3b551-124">If you're not familiar with using Azure PowerShell, read the [How to install and configure Azure PowerShell](/powershell/azure/overview) article.</span></span>
2. <span data-ttu-id="3b551-125">Entrez la commande suivante pour renvoyer toutes les règles du groupe de sécurité réseau appliquées à une carte d’interface réseau nommée *VM1-NIC1* dans le groupe de ressources *RG1* :</span><span class="sxs-lookup"><span data-stu-id="3b551-125">Enter the following command to return all NSG rules applied to a NIC named *VM1-NIC1* in the resource group *RG1*:</span></span>
   
        Get-AzureRmEffectiveNetworkSecurityGroup -NetworkInterfaceName VM1-NIC1 -ResourceGroupName RG1
   
   > [!TIP]
   > <span data-ttu-id="3b551-126">Si vous ne connaissez pas le nom d’une carte d’interface réseau, entrez la commande suivante pour récupérer les noms de toutes les cartes d’interface réseau d’un groupe de ressources :</span><span class="sxs-lookup"><span data-stu-id="3b551-126">If you don't know the name of a NIC, enter the following command to retrieve the names of all NICs in a resource group:</span></span> 
   > 
   > `Get-AzureRmNetworkInterface -ResourceGroupName RG1 | Format-Table Name`
   > 
   > 
   
    <span data-ttu-id="3b551-127">Le texte suivant est un exemple de sortie de règles effectives retournée pour la carte d’interface réseau *VM1-NIC1* :</span><span class="sxs-lookup"><span data-stu-id="3b551-127">The following text is a sample of the effective rules output returned for the *VM1-NIC1* NIC:</span></span>
   
        NetworkSecurityGroup   : {
                                   "Id": "/subscriptions/[Subscription ID]/resourceGroups/RG1/providers/Microsoft.Network/networkSecurityGroups/VM1-NIC1-NSG"
                                 }
        Association            : {
                                   "NetworkInterface": {
                                     "Id": "/subscriptions/[Subscription ID]/resourceGroups/RG1/providers/Microsoft.Network/networkInterfaces/VM1-NIC1"
                                   }
                                 }
        EffectiveSecurityRules : [
                                 {
                                 "Name": "securityRules/allowRDP",
                                 "Protocol": "Tcp",
                                 "SourcePortRange": "0-65535",
                                 "DestinationPortRange": "3389-3389",
                                 "SourceAddressPrefix": "Internet",
                                 "DestinationAddressPrefix": "0.0.0.0/0",
                                 "ExpandedSourceAddressPrefix": [… ],
                                 "ExpandedDestinationAddressPrefix": [],
                                 "Access": "Allow",
                                 "Priority": 1000,
                                 "Direction": "Inbound"
                                 },
                                 {
                                 "Name": "defaultSecurityRules/AllowVnetInBound",
                                 "Protocol": "All",
                                 "SourcePortRange": "0-65535",
                                 "DestinationPortRange": "0-65535",
                                 "SourceAddressPrefix": "VirtualNetwork",
                                 "DestinationAddressPrefix": "VirtualNetwork",
                                 "ExpandedSourceAddressPrefix": [
                                  "10.9.0.0/16",
                                  "168.63.129.16/32",
                                  "10.0.0.0/16",
                                  "10.1.0.0/16"
                                  ],
                                 "ExpandedDestinationAddressPrefix": [
                                  "10.9.0.0/16",
                                  "168.63.129.16/32",
                                  "10.0.0.0/16",
                                  "10.1.0.0/16"
                                  ],
                                  "Access": "Allow",
                                  "Priority": 65000,
                                  "Direction": "Inbound"
                                  },…
                         ]
   
        NetworkSecurityGroup   : {
                                   "Id": 
                                 "/subscriptions/[Subscription ID]/resourceGroups/RG1/providers/Microsoft.Network/networkSecurityGroups/Subnet1-NSG"
                                 }
        Association            : {
                                   "Subnet": {
                                     "Id": 
                                 "/subscriptions/[Subscription ID]/resourceGroups/RG1/providers/Microsoft.Network/virtualNetworks/WestUS-VNet1/subnets/Subnet1"
                                 }
                                 }
        EffectiveSecurityRules : [
                                 {
                                "Name": "securityRules/denyRDP",
                                "Protocol": "Tcp",
                                "SourcePortRange": "0-65535",
                                "DestinationPortRange": "3389-3389",
                                "SourceAddressPrefix": "Internet",
                                "DestinationAddressPrefix": "0.0.0.0/0",
                                "ExpandedSourceAddressPrefix": [
                                   ... ],
                                "ExpandedDestinationAddressPrefix": [],
                                "Access": "Deny",
                                "Priority": 1000,
                                "Direction": "Inbound"
                                },
                                {
                                "Name": "defaultSecurityRules/AllowVnetInBound",
                                "Protocol": "All",
                                "SourcePortRange": "0-65535",
                                "DestinationPortRange": "0-65535",
                                "SourceAddressPrefix": "VirtualNetwork",
                                "DestinationAddressPrefix": "VirtualNetwork",
                                "ExpandedSourceAddressPrefix": [
                                "10.9.0.0/16",
                                "168.63.129.16/32",
                                "10.0.0.0/16",
                                "10.1.0.0/16"
                                ],
                                "ExpandedDestinationAddressPrefix": [
                                "10.9.0.0/16",
                                "168.63.129.16/32",
                                "10.0.0.0/16",
                                "10.1.0.0/16"
                                ],
                                "Access": "Allow",
                                "Priority": 65000,
                                "Direction": "Inbound"
                                },...
                                ]
   
    <span data-ttu-id="3b551-128">Notez les informations suivantes dans la sortie :</span><span class="sxs-lookup"><span data-stu-id="3b551-128">Note the following information in the output:</span></span>
   
   * <span data-ttu-id="3b551-129">Il existe deux sections **NetworkSecurityGroup** : l’une est associée à un sous-réseau (*Subnet1*), et l’autre à une carte d’interface réseau (*VM1-NIC1*).</span><span class="sxs-lookup"><span data-stu-id="3b551-129">There are two **NetworkSecurityGroup** sections: One is associated with a subnet (*Subnet1*) and one is associated with a NIC (*VM1-NIC1*).</span></span> <span data-ttu-id="3b551-130">Dans cet exemple, un groupe de sécurité réseau a été appliquée à chacune d’elles.</span><span class="sxs-lookup"><span data-stu-id="3b551-130">In this example, an NSG has been applied to each.</span></span>
   * <span data-ttu-id="3b551-131">**Association** montre les ressources (carte d’interface réseau ou sous-réseau) auxquelles un groupe de sécurité réseau donné est associé.</span><span class="sxs-lookup"><span data-stu-id="3b551-131">**Association** shows the resource (subnet or NIC) a given NSG is associated with.</span></span> <span data-ttu-id="3b551-132">Si la ressource de groupe de sécurité réseau est déplacée/dissociée immédiatement avant l’exécution de cette commande, il se peut que vous deviez attendre quelques secondes pour que la modification apparaisse dans la sortie de la commande.</span><span class="sxs-lookup"><span data-stu-id="3b551-132">If the NSG resource is moved/disassociated immediately before running this command, you may need to wait a few seconds for the change to reflect in the command output.</span></span> 
   * <span data-ttu-id="3b551-133">Les noms de règle sont précédés de *defaultSecurityRules*: lors de la création d’un groupe de sécurité réseau, plusieurs règles de sécurité par défaut sont créées à l’intérieur de celui-ci.</span><span class="sxs-lookup"><span data-stu-id="3b551-133">The rule names that are prefaced with *defaultSecurityRules*: When an NSG is created, several default security rules are created within it.</span></span> <span data-ttu-id="3b551-134">Vous ne pouvez pas supprimer des règles par défaut, mais vous pouvez les remplacer par des règles de priorité plus élevée.</span><span class="sxs-lookup"><span data-stu-id="3b551-134">Default rules can't be removed, but they can be overridden with higher priority rules.</span></span>
     <span data-ttu-id="3b551-135">Pour en savoir plus sur les règles de sécurité par défaut de groupe de sécurité réseau , voir l’article [Vue d’ensemble de groupe de sécurité réseau](virtual-networks-nsg.md#default-rules) .</span><span class="sxs-lookup"><span data-stu-id="3b551-135">Read the [NSG overview](virtual-networks-nsg.md#default-rules) article to learn more about NSG default security rules.</span></span>
   * <span data-ttu-id="3b551-136">**ExpandedAddressPrefix** développe les préfixes d’adresse pour les balises par défaut de groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="3b551-136">**ExpandedAddressPrefix** expands the address prefixes for NSG default tags.</span></span> <span data-ttu-id="3b551-137">Les balises représentent plusieurs préfixes d’adresse.</span><span class="sxs-lookup"><span data-stu-id="3b551-137">Tags represent multiple address prefixes.</span></span> <span data-ttu-id="3b551-138">L’expansion des balises peut être utile lors de la résolution de problèmes de connectivité de machine virtuelle avec des préfixes d’adresse spécifiques.</span><span class="sxs-lookup"><span data-stu-id="3b551-138">Expansion of the tags can be useful when troubleshooting VM connectivity to/from specific address prefixes.</span></span> <span data-ttu-id="3b551-139">Par exemple, avec VNET Peering, la balise VIRTUAL_NETWORK se développe pour afficher les préfixes de réseau virtuel homologués dans la sortie précédente.</span><span class="sxs-lookup"><span data-stu-id="3b551-139">For example, with VNET peering, VIRTUAL_NETWORK tag expands to show peered VNet prefixes in the previous output.</span></span>
     
     > [!NOTE]
     > <span data-ttu-id="3b551-140">La commande affiche des règles effectives uniquement si un groupe de sécurité réseau est associé à un sous-réseau, à une carte d’interface réseau ou aux deux.</span><span class="sxs-lookup"><span data-stu-id="3b551-140">The command only shows effective rules if an NSG is associated with either a subnet, a NIC, or both.</span></span> <span data-ttu-id="3b551-141">Une machine virtuelle peut avoir plusieurs cartes d’interface réseau à laquelle différents groupes de sécurité réseau sont appliqués.</span><span class="sxs-lookup"><span data-stu-id="3b551-141">A VM may have multiple NICs with different NSGs applied.</span></span> <span data-ttu-id="3b551-142">Lors de la résolution du problème, exécutez la commande pour chaque carte d’interface réseau.</span><span class="sxs-lookup"><span data-stu-id="3b551-142">When troubleshooting, run the command for each NIC.</span></span>
     > 
     > 
3. <span data-ttu-id="3b551-143">Pour faciliter le filtrage d’un nombre plus important de règles de groupe de sécurité réseau, entrez les commandes suivantes pour résoudre le problème :</span><span class="sxs-lookup"><span data-stu-id="3b551-143">To ease filtering over larger number of NSG rules, enter the following commands to troubleshoot further:</span></span> 
   
        $NSGs = Get-AzureRmEffectiveNetworkSecurityGroup -NetworkInterfaceName VM1-NIC1 -ResourceGroupName RG1
        $NSGs.EffectiveSecurityRules | Sort-Object Direction, Access, Priority | Out-GridView
   
    <span data-ttu-id="3b551-144">Un filtre pour le trafic RDP (port TCP 3389) est appliqué à l’affichage grille, comme illustré dans l’image suivante :</span><span class="sxs-lookup"><span data-stu-id="3b551-144">A filter for RDP traffic (TCP port 3389), is applied to the grid view, as shown in the following picture:</span></span>
   
    ![Liste des règles](./media/virtual-network-nsg-troubleshoot-powershell/rules.png)
4. <span data-ttu-id="3b551-146">Comme vous pouvez le voir dans l’affichage grille, il existe des règles d’autorisation et de refus pour RDP.</span><span class="sxs-lookup"><span data-stu-id="3b551-146">As you can see in the grid view, there are both allow and deny rules for RDP.</span></span> <span data-ttu-id="3b551-147">La sortie de l’étape 2 montre que la règle *DenyRDP* figure dans le groupe de sécurité réseau appliqué au sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="3b551-147">The output from step 2 shows that the *DenyRDP* rule is in the NSG applied to the subnet.</span></span> <span data-ttu-id="3b551-148">Pour les règles de trafic entrant, les groupes de sécurité réseau appliqués au sous-réseau sont traités en premier.</span><span class="sxs-lookup"><span data-stu-id="3b551-148">For inbound rules, NSGs applied to the subnet are processed first.</span></span> <span data-ttu-id="3b551-149">Si une correspondance est trouvée, le groupe de sécurité réseau appliqué à l’interface réseau n’est pas traité.</span><span class="sxs-lookup"><span data-stu-id="3b551-149">If a match is found, the NSG applied to the network interface is not processed.</span></span> <span data-ttu-id="3b551-150">Dans ce cas, la règle *DenyRDP* du sous-réseau bloque le RDP à la machine virtuelle (**VM1**).</span><span class="sxs-lookup"><span data-stu-id="3b551-150">In this case, the *DenyRDP* rule from the subnet blocks RDP to the VM (**VM1**).</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="3b551-151">Plusieurs cartes d’interface réseau peuvent être attachées à une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="3b551-151">A VM may have multiple NICs attached to it.</span></span> <span data-ttu-id="3b551-152">Chacune peut être connectée à un sous-réseau différent.</span><span class="sxs-lookup"><span data-stu-id="3b551-152">Each may be connected to a different subnet.</span></span> <span data-ttu-id="3b551-153">Étant donné que les commandes des étapes précédentes sont exécutées sur une carte d’interface réseau, il est important de spécifier la carte d’interface réseau avec laquelle l’échec de connectivité se produit.</span><span class="sxs-lookup"><span data-stu-id="3b551-153">Since the commands in the previous steps are run against a NIC, it's important to ensure that you specify the NIC you're having the connectivity failure to.</span></span> <span data-ttu-id="3b551-154">Si vous n’êtes pas sûr, vous pouvez toujours exécuter les commandes sur chaque carte d’interface réseau attachée à la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="3b551-154">If you're not sure, you can always run the commands against each NIC attached to the VM.</span></span>
   > 
   > 
5. <span data-ttu-id="3b551-155">Pour le protocole RDP dans la machine virtuelle VM1, modifiez la règle *Refuser RDP (3389)* en *Autoriser RDP(3389)* dans le groupe de sécurité réseau **Subnet1-NSG**.</span><span class="sxs-lookup"><span data-stu-id="3b551-155">To RDP into VM1, change the *Deny RDP (3389)* rule to *Allow RDP(3389)* in the **Subnet1-NSG** NSG.</span></span> <span data-ttu-id="3b551-156">Vérifiez que le port TCP 3389 est ouvert en ouvrant une connexion RDP à la machine virtuelle ou en utilisant l’outil PsPing.</span><span class="sxs-lookup"><span data-stu-id="3b551-156">Confirm that TCP port 3389 is open by opening an RDP connection to the VM or using the PsPing tool.</span></span> <span data-ttu-id="3b551-157">Pour en savoir plus sur PsPing, lire la [page de téléchargement de PsPing](https://technet.microsoft.com/sysinternals/psping.aspx)</span><span class="sxs-lookup"><span data-stu-id="3b551-157">You can learn more about PsPing by reading the [PsPing download page](https://technet.microsoft.com/sysinternals/psping.aspx)</span></span>
   
    <span data-ttu-id="3b551-158">Vous pouvez supprimer des règles d’un groupe de sécurité réseau en utilisant les informations de la sortie de la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="3b551-158">You can or remove rules from an NSG by using the information in the output from the following command:</span></span>
   
        Get-Help *-AzureRmNetworkSecurityRuleConfig

## <a name="considerations"></a><span data-ttu-id="3b551-159">Considérations</span><span class="sxs-lookup"><span data-stu-id="3b551-159">Considerations</span></span>
<span data-ttu-id="3b551-160">Lors de la résolution de problèmes de connectivité, considérez les points suivants :</span><span class="sxs-lookup"><span data-stu-id="3b551-160">Consider the following points when troubleshooting connectivity problems:</span></span>

* <span data-ttu-id="3b551-161">Des règles de groupe de sécurité réseau par défaut bloquent l’accès entrant à partir d’internet et n’autorisent que le trafic entrant dans le réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="3b551-161">Default NSG rules will block inbound access from the internet and only permit VNet inbound traffic.</span></span> <span data-ttu-id="3b551-162">Les règles doivent être ajoutées de façon explicite afin d’autoriser l’accès entrant à partir d’Internet, en fonction des besoins.</span><span class="sxs-lookup"><span data-stu-id="3b551-162">Rules should be explicitly added to allow inbound access from Internet, as required.</span></span>
* <span data-ttu-id="3b551-163">Si aucune règle de sécurité du groupe de sécurité réseau n’est à l’origine d’un échec de connectivité réseau d’une machine virtuelle, les causes du problème peuvent être les suivantes :</span><span class="sxs-lookup"><span data-stu-id="3b551-163">If there are no NSG security rules causing a VM’s network connectivity to fail, the problem may be due to:</span></span>
  * <span data-ttu-id="3b551-164">Logiciel de pare-feu s’exécutant à l’intérieur du système d’exploitation de la machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="3b551-164">Firewall software running within the VM's operating system</span></span>
  * <span data-ttu-id="3b551-165">Itinéraires configurés pour des appliances virtuelles ou un trafic local.</span><span class="sxs-lookup"><span data-stu-id="3b551-165">Routes configured for virtual appliances or on-premises traffic.</span></span> <span data-ttu-id="3b551-166">Le trafic Internet peut être redirigé localement au moyen d’un tunneling forcé.</span><span class="sxs-lookup"><span data-stu-id="3b551-166">Internet traffic can be redirected to on-premises via forced-tunneling.</span></span> <span data-ttu-id="3b551-167">Il se peut qu’une connexion RDP/SSH d’Internet à votre machine virtuelle ne fonctionne pas avec ce paramètre, selon la façon dont le matériel de réseau local gère ce trafic.</span><span class="sxs-lookup"><span data-stu-id="3b551-167">An RDP/SSH connection from the Internet to your VM may not work with this setting, depending on how the on-premises network hardware handles this traffic.</span></span> <span data-ttu-id="3b551-168">Pour savoir comment diagnostiquer des problèmes d’itinéraire susceptibles d’entraver le flux de trafic échangé avec la machine virtuelle, consultez [Résolution des problèmes d’itinéraire](virtual-network-routes-troubleshoot-powershell.md) .</span><span class="sxs-lookup"><span data-stu-id="3b551-168">Read the [Troubleshooting Routes](virtual-network-routes-troubleshoot-powershell.md) article to learn how to diagnose route problems that may be impeding the flow of traffic in and out of the VM.</span></span> 
* <span data-ttu-id="3b551-169">Si vous avez des réseaux virtuels homologues, par défaut, la balise VIRTUAL_NETWORK s’étend automatiquement pour inclure les préfixes des réseaux virtuels homologues.</span><span class="sxs-lookup"><span data-stu-id="3b551-169">If you have peered VNets, by default, the VIRTUAL_NETWORK tag will automatically expand to include prefixes for peered VNets.</span></span> <span data-ttu-id="3b551-170">Pour résoudre des problèmes liés à la connectivité d’homologation de réseau virtuel, vous pouvez consulter ces préfixes dans la liste **ExpandedAddressPrefix** .</span><span class="sxs-lookup"><span data-stu-id="3b551-170">You can view these prefixes in the **ExpandedAddressPrefix** list, to troubleshoot any issues related to VNet peering connectivity.</span></span> 
* <span data-ttu-id="3b551-171">Les règles de sécurité effectives sont affichées uniquement s’il existe un groupe de sécurité réseau associé à la carte réseau et au sous-réseau de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="3b551-171">Effective security rules are only shown if there is an NSG associated with the VM’s NIC and or subnet.</span></span> 
* <span data-ttu-id="3b551-172">Si aucun groupe de sécurité réseau n’est associé à la carte réseau ou au sous-réseau, et si une adresse IP publique est affectée à votre machine virtuelle, tous les ports sont ouverts pour les accès entrants et sortants.</span><span class="sxs-lookup"><span data-stu-id="3b551-172">If there are no NSGs associated with the NIC or subnet and you have a public IP address assigned to your VM, all ports will be open for inbound and outbound access.</span></span> <span data-ttu-id="3b551-173">Si la machine virtuelle a une adresse IP publique, l’application de groupes de sécurité réseau à la carte réseau ou au sous-réseau est vivement recommandée.</span><span class="sxs-lookup"><span data-stu-id="3b551-173">If the VM has a public IP address, applying NSGs to the NIC or subnet is strongly recommended.</span></span>  

