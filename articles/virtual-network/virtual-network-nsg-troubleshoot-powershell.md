---
title: "aaaTroubleshoot des groupes de sécurité réseau - PowerShell | Documents Microsoft"
description: "Découvrez comment les groupes de sécurité réseau tootroubleshoot dans un déploiement d’Azure Resource Manager hello modèle à l’aide d’Azure PowerShell."
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
ms.openlocfilehash: 95fd60fa72cf6d17fa990e3c3eb7d980878f7c15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-network-security-groups-using-azure-powershell"></a><span data-ttu-id="c6f4e-103">Résoudre les groupes de sécurité réseau à l’aide d’Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="c6f4e-103">Troubleshoot Network Security Groups using Azure PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c6f4e-104">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="c6f4e-104">Azure Portal</span></span>](virtual-network-nsg-troubleshoot-portal.md)
> * [<span data-ttu-id="c6f4e-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c6f4e-105">PowerShell</span></span>](virtual-network-nsg-troubleshoot-powershell.md)
> 
> 

<span data-ttu-id="c6f4e-106">Si vous configuré des groupes de sécurité réseau (NSG) sur votre machine virtuelle (VM) et qui rencontrent des problèmes de connectivité de machine virtuelle, cet article fournit une vue d’ensemble des fonctionnalités des diagnostics pour les groupes de sécurité réseau toohelp dépannage.</span><span class="sxs-lookup"><span data-stu-id="c6f4e-106">If you configured Network Security Groups (NSGs) on your virtual machine (VM) and are experiencing VM connectivity issues, this article provides an overview of diagnostics capabilities for NSGs toohelp troubleshoot further.</span></span>

<span data-ttu-id="c6f4e-107">Groupes de sécurité réseau permettent de types de hello toocontrol de trafic ce flux et vos machines virtuelles (VM).</span><span class="sxs-lookup"><span data-stu-id="c6f4e-107">NSGs enable you toocontrol hello types of traffic that flow in and out of your virtual machines (VMs).</span></span> <span data-ttu-id="c6f4e-108">Groupes de sécurité réseau peuvent être appliqués toosubnets dans un réseau virtuel de Azure (VNet), les interfaces de réseau (NIC) ou les deux.</span><span class="sxs-lookup"><span data-stu-id="c6f4e-108">NSGs can be applied toosubnets in an Azure Virtual Network (VNet), network interfaces (NIC), or both.</span></span> <span data-ttu-id="c6f4e-109">Hello efficace règles appliquées tooa NIC sont un regroupement de règles hello qui existent dans hello NSG appliqué tooa NIC hello sous-réseau et il est connecté à.</span><span class="sxs-lookup"><span data-stu-id="c6f4e-109">hello effective rules applied tooa NIC are an aggregation of hello rules that exist in hello NSGs applied tooa NIC and hello subnet it is connected to.</span></span> <span data-ttu-id="c6f4e-110">Les règles appliquées à ces groupes de sécurité réseau sont parfois en conflit entre elles et peuvent avoir une incidence sur la connectivité réseau d’une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="c6f4e-110">Rules across these NSGs can sometimes conflict with each other and impact a VM's network connectivity.</span></span>  

<span data-ttu-id="c6f4e-111">Vous pouvez afficher toutes les règles de sécurité efficace hello à partir de vos groupes de sécurité réseau, tel qu’appliqué sur les cartes d’interface réseau de votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="c6f4e-111">You can view all hello effective security rules from your NSGs, as applied on your VM's NICs.</span></span> <span data-ttu-id="c6f4e-112">Cet article explique comment tootroubleshoot des problèmes de connectivité de la machine virtuelle à l’aide de ces règles dans hello modèle de déploiement Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="c6f4e-112">This article shows how tootroubleshoot VM connectivity issues using these rules in hello Azure Resource Manager deployment model.</span></span> <span data-ttu-id="c6f4e-113">Si vous n’êtes pas familiarisé avec les concepts de réseau virtuel et le groupe de sécurité réseau, lire hello [réseau virtuel](virtual-networks-overview.md) et [groupes de sécurité réseau](virtual-networks-nsg.md) articles de vue d’ensemble.</span><span class="sxs-lookup"><span data-stu-id="c6f4e-113">If you're not familiar with VNet and NSG concepts, read hello [Virtual network](virtual-networks-overview.md) and [Network security groups](virtual-networks-nsg.md) overview articles.</span></span>

## <a name="using-effective-security-rules-tootroubleshoot-vm-traffic-flow"></a><span data-ttu-id="c6f4e-114">À l’aide de flux de trafic des règles de sécurité efficace tootroubleshoot machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="c6f4e-114">Using Effective Security Rules tootroubleshoot VM traffic flow</span></span>
<span data-ttu-id="c6f4e-115">scénario Hello qui suit est un exemple d’un problème de connexion courantes :</span><span class="sxs-lookup"><span data-stu-id="c6f4e-115">hello scenario that follows is an example of a common connection problem:</span></span>

<span data-ttu-id="c6f4e-116">Une machine virtuelle nommée *VM1* fait partie d’un sous-réseau nommé *Subnet1* au sein d’un réseau virtuel nommé *WestUS-VNet1*.</span><span class="sxs-lookup"><span data-stu-id="c6f4e-116">A VM named *VM1* is part of a subnet named *Subnet1* within a VNet named *WestUS-VNet1*.</span></span> <span data-ttu-id="c6f4e-117">Un toohello tooconnect de tentative de machine virtuelle à l’aide du protocole RDP sur le port TCP 3389 échoue.</span><span class="sxs-lookup"><span data-stu-id="c6f4e-117">An attempt tooconnect toohello VM using RDP over TCP port 3389 fails.</span></span> <span data-ttu-id="c6f4e-118">Groupes de sécurité réseau sont appliquées sur les deux cartes réseau hello *NIC1 de VM1* et hello sous-réseau *Subnet1*.</span><span class="sxs-lookup"><span data-stu-id="c6f4e-118">NSGs are applied at both hello NIC *VM1-NIC1* and hello subnet *Subnet1*.</span></span> <span data-ttu-id="c6f4e-119">Le port du trafic tooTCP 3389 est autorisé dans hello NSG associée à interface réseau de hello *NIC1 de VM1*toutefois TCP ping échoue de tooVM1 port 3389.</span><span class="sxs-lookup"><span data-stu-id="c6f4e-119">Traffic tooTCP port 3389 is allowed in hello NSG associated with hello network interface *VM1-NIC1*, however TCP ping tooVM1's port 3389 fails.</span></span>

<span data-ttu-id="c6f4e-120">Bien que cet exemple utilise le port TCP 3389, hello comme suit peut être utilisé toodetermine échecs de connexion entrant et sortant sur n’importe quel port.</span><span class="sxs-lookup"><span data-stu-id="c6f4e-120">While this example uses TCP port 3389, hello following steps can be used toodetermine inbound and outbound connection failures over any port.</span></span>

## <a name="detailed-troubleshooting-steps"></a><span data-ttu-id="c6f4e-121">Étapes de dépannage détaillées</span><span class="sxs-lookup"><span data-stu-id="c6f4e-121">Detailed Troubleshooting Steps</span></span>
<span data-ttu-id="c6f4e-122">Terminer hello suivant les étapes tootroubleshoot groupes de sécurité réseau pour une machine virtuelle :</span><span class="sxs-lookup"><span data-stu-id="c6f4e-122">Complete hello following steps tootroubleshoot NSGs for a VM:</span></span>

1. <span data-ttu-id="c6f4e-123">Démarrer un tooAzure de session et de connexion Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c6f4e-123">Start an Azure PowerShell session and login tooAzure.</span></span> <span data-ttu-id="c6f4e-124">Si vous n’êtes pas familiarisé avec l’utilisation d’Azure PowerShell, lire hello [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview) l’article.</span><span class="sxs-lookup"><span data-stu-id="c6f4e-124">If you're not familiar with using Azure PowerShell, read hello [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) article.</span></span>
2. <span data-ttu-id="c6f4e-125">Entrez hello commande tooreturn toutes les règles du groupe de sécurité réseau appliquent tooa carte réseau nommée suivante *NIC1 de VM1* dans le groupe de ressources hello *RG1*:</span><span class="sxs-lookup"><span data-stu-id="c6f4e-125">Enter hello following command tooreturn all NSG rules applied tooa NIC named *VM1-NIC1* in hello resource group *RG1*:</span></span>
   
        Get-AzureRmEffectiveNetworkSecurityGroup -NetworkInterfaceName VM1-NIC1 -ResourceGroupName RG1
   
   > [!TIP]
   > <span data-ttu-id="c6f4e-126">Si vous ne connaissez pas nom hello d’une carte réseau, entrez hello commande tooretrieve hello nom de toutes les cartes réseau dans un groupe de ressources :</span><span class="sxs-lookup"><span data-stu-id="c6f4e-126">If you don't know hello name of a NIC, enter hello following command tooretrieve hello names of all NICs in a resource group:</span></span> 
   > 
   > `Get-AzureRmNetworkInterface -ResourceGroupName RG1 | Format-Table Name`
   > 
   > 
   
    <span data-ttu-id="c6f4e-127">Hello texte suivant est un exemple de sortie de règles efficaces de hello retournée pour hello *NIC1 de VM1* carte réseau :</span><span class="sxs-lookup"><span data-stu-id="c6f4e-127">hello following text is a sample of hello effective rules output returned for hello *VM1-NIC1* NIC:</span></span>
   
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
   
    <span data-ttu-id="c6f4e-128">Notez hello informations dans la sortie de hello suivantes :</span><span class="sxs-lookup"><span data-stu-id="c6f4e-128">Note hello following information in hello output:</span></span>
   
   * <span data-ttu-id="c6f4e-129">Il existe deux sections **NetworkSecurityGroup** : l’une est associée à un sous-réseau (*Subnet1*), et l’autre à une carte d’interface réseau (*VM1-NIC1*).</span><span class="sxs-lookup"><span data-stu-id="c6f4e-129">There are two **NetworkSecurityGroup** sections: One is associated with a subnet (*Subnet1*) and one is associated with a NIC (*VM1-NIC1*).</span></span> <span data-ttu-id="c6f4e-130">Dans cet exemple, un groupe de sécurité réseau a été appliqué tooeach.</span><span class="sxs-lookup"><span data-stu-id="c6f4e-130">In this example, an NSG has been applied tooeach.</span></span>
   * <span data-ttu-id="c6f4e-131">**Association** montre les ressources de hello (carte réseau ou sous-réseau) à un groupe de sécurité réseau donné est associé.</span><span class="sxs-lookup"><span data-stu-id="c6f4e-131">**Association** shows hello resource (subnet or NIC) a given NSG is associated with.</span></span> <span data-ttu-id="c6f4e-132">Si hello ressource du groupe de sécurité réseau est déplacée/dissocié immédiatement avant d’exécuter cette commande, vous devrez peut-être toowait quelques secondes pour tooreflect de modification hello dans la sortie de la commande hello.</span><span class="sxs-lookup"><span data-stu-id="c6f4e-132">If hello NSG resource is moved/disassociated immediately before running this command, you may need toowait a few seconds for hello change tooreflect in hello command output.</span></span> 
   * <span data-ttu-id="c6f4e-133">les noms de règle qui sont précédés de Hello *defaultSecurityRules*: quand un groupe de sécurité réseau est créé, plusieurs règles de sécurité par défaut sont créés dans celui-ci.</span><span class="sxs-lookup"><span data-stu-id="c6f4e-133">hello rule names that are prefaced with *defaultSecurityRules*: When an NSG is created, several default security rules are created within it.</span></span> <span data-ttu-id="c6f4e-134">Vous ne pouvez pas supprimer des règles par défaut, mais vous pouvez les remplacer par des règles de priorité plus élevée.</span><span class="sxs-lookup"><span data-stu-id="c6f4e-134">Default rules can't be removed, but they can be overridden with higher priority rules.</span></span>
     <span data-ttu-id="c6f4e-135">Hello de lecture [vue d’ensemble du groupe de sécurité réseau](virtual-networks-nsg.md#default-rules) toolearn article en savoir plus sur le groupe de sécurité réseau par défaut des règles de sécurité.</span><span class="sxs-lookup"><span data-stu-id="c6f4e-135">Read hello [NSG overview](virtual-networks-nsg.md#default-rules) article toolearn more about NSG default security rules.</span></span>
   * <span data-ttu-id="c6f4e-136">**ExpandedAddressPrefix** développe les préfixes d’adresse hello pour les étiquettes de groupe de sécurité réseau par défaut.</span><span class="sxs-lookup"><span data-stu-id="c6f4e-136">**ExpandedAddressPrefix** expands hello address prefixes for NSG default tags.</span></span> <span data-ttu-id="c6f4e-137">Les balises représentent plusieurs préfixes d’adresse.</span><span class="sxs-lookup"><span data-stu-id="c6f4e-137">Tags represent multiple address prefixes.</span></span> <span data-ttu-id="c6f4e-138">Expansion de balises de hello peut être utile lors de la résolution des problèmes de connectivité de machine virtuelle à partir de préfixes d’adresse spécifique.</span><span class="sxs-lookup"><span data-stu-id="c6f4e-138">Expansion of hello tags can be useful when troubleshooting VM connectivity to/from specific address prefixes.</span></span> <span data-ttu-id="c6f4e-139">Par exemple, avec le réseau virtuel d’homologation, balise VIRTUAL_NETWORK développe tooshow homologuer les préfixes de réseau virtuel dans la sortie précédente hello.</span><span class="sxs-lookup"><span data-stu-id="c6f4e-139">For example, with VNET peering, VIRTUAL_NETWORK tag expands tooshow peered VNet prefixes in hello previous output.</span></span>
     
     > [!NOTE]
     > <span data-ttu-id="c6f4e-140">Bonjour commande effective règles affiche uniquement si un groupe de sécurité réseau est associé à un sous-réseau, une carte réseau ou les deux.</span><span class="sxs-lookup"><span data-stu-id="c6f4e-140">hello command only shows effective rules if an NSG is associated with either a subnet, a NIC, or both.</span></span> <span data-ttu-id="c6f4e-141">Une machine virtuelle peut avoir plusieurs cartes d’interface réseau à laquelle différents groupes de sécurité réseau sont appliqués.</span><span class="sxs-lookup"><span data-stu-id="c6f4e-141">A VM may have multiple NICs with different NSGs applied.</span></span> <span data-ttu-id="c6f4e-142">Lors de la résolution du problème, exécutez la commande hello pour chaque carte réseau.</span><span class="sxs-lookup"><span data-stu-id="c6f4e-142">When troubleshooting, run hello command for each NIC.</span></span>
     > 
     > 
3. <span data-ttu-id="c6f4e-143">tooease le filtrage sur un plus grand nombre de règles du groupe de sécurité réseau, entrez hello suivant tootroubleshoot des commandes supplémentaires :</span><span class="sxs-lookup"><span data-stu-id="c6f4e-143">tooease filtering over larger number of NSG rules, enter hello following commands tootroubleshoot further:</span></span> 
   
        $NSGs = Get-AzureRmEffectiveNetworkSecurityGroup -NetworkInterfaceName VM1-NIC1 -ResourceGroupName RG1
        $NSGs.EffectiveSecurityRules | Sort-Object Direction, Access, Priority | Out-GridView
   
    <span data-ttu-id="c6f4e-144">Un filtre pour le trafic RDP (port TCP 3389), est appliqué toohello affichage de grille, comme indiqué dans hello illustration suivante :</span><span class="sxs-lookup"><span data-stu-id="c6f4e-144">A filter for RDP traffic (TCP port 3389), is applied toohello grid view, as shown in hello following picture:</span></span>
   
    ![Liste des règles](./media/virtual-network-nsg-troubleshoot-powershell/rules.png)
4. <span data-ttu-id="c6f4e-146">Comme vous pouvez le voir dans l’affichage de grille hello, il existe deux autorisent et refuser des règles pour RDP.</span><span class="sxs-lookup"><span data-stu-id="c6f4e-146">As you can see in hello grid view, there are both allow and deny rules for RDP.</span></span> <span data-ttu-id="c6f4e-147">sortie de l’étape 2 Hello indique que hello *DenyRDP* règle est Bonjour NSG appliqué toohello sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="c6f4e-147">hello output from step 2 shows that hello *DenyRDP* rule is in hello NSG applied toohello subnet.</span></span> <span data-ttu-id="c6f4e-148">Pour les règles de trafic entrant, groupes de sécurité réseau appliquées toohello sous-réseau sont traitées en premier.</span><span class="sxs-lookup"><span data-stu-id="c6f4e-148">For inbound rules, NSGs applied toohello subnet are processed first.</span></span> <span data-ttu-id="c6f4e-149">Si une correspondance est trouvée, l’interface de réseau toohello hello NSG appliqué n’est pas traitée.</span><span class="sxs-lookup"><span data-stu-id="c6f4e-149">If a match is found, hello NSG applied toohello network interface is not processed.</span></span> <span data-ttu-id="c6f4e-150">Dans ce cas, hello *DenyRDP* de règle de sous-réseau de hello bloque RDP toohello VM (**VM1**).</span><span class="sxs-lookup"><span data-stu-id="c6f4e-150">In this case, hello *DenyRDP* rule from hello subnet blocks RDP toohello VM (**VM1**).</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="c6f4e-151">Une machine virtuelle peut avoir plusieurs tooit de cartes réseau attachée.</span><span class="sxs-lookup"><span data-stu-id="c6f4e-151">A VM may have multiple NICs attached tooit.</span></span> <span data-ttu-id="c6f4e-152">Chacun peut être connecté tooa autre sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="c6f4e-152">Each may be connected tooa different subnet.</span></span> <span data-ttu-id="c6f4e-153">Étant donné que les commandes hello dans les étapes précédentes hello sont exécutées sur une carte réseau, il est important de tooensure que vous spécifiez hello carte réseau que vous rencontrez Échec de connectivité hello.</span><span class="sxs-lookup"><span data-stu-id="c6f4e-153">Since hello commands in hello previous steps are run against a NIC, it's important tooensure that you specify hello NIC you're having hello connectivity failure to.</span></span> <span data-ttu-id="c6f4e-154">Si vous n’êtes pas sûr, vous pouvez toujours exécuter des commandes hello sur chaque machine virtuelle de toohello carte réseau attachée.</span><span class="sxs-lookup"><span data-stu-id="c6f4e-154">If you're not sure, you can always run hello commands against each NIC attached toohello VM.</span></span>
   > 
   > 
5. <span data-ttu-id="c6f4e-155">tooRDP dans VM1, modification hello *refuser RDP (3389)* trop de règles*autoriser les RDP(3389)* Bonjour **Subnet1-groupe de sécurité réseau** groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="c6f4e-155">tooRDP into VM1, change hello *Deny RDP (3389)* rule too*Allow RDP(3389)* in hello **Subnet1-NSG** NSG.</span></span> <span data-ttu-id="c6f4e-156">Vérifiez que le port TCP 3389 est ouvert en ouvrant un toohello de connexion RDP machine virtuelle ou en utilisant l’outil PsPing de hello.</span><span class="sxs-lookup"><span data-stu-id="c6f4e-156">Confirm that TCP port 3389 is open by opening an RDP connection toohello VM or using hello PsPing tool.</span></span> <span data-ttu-id="c6f4e-157">Vous pouvez en savoir plus sur PsPing par la lecture de hello [page de téléchargement PsPing](https://technet.microsoft.com/sysinternals/psping.aspx)</span><span class="sxs-lookup"><span data-stu-id="c6f4e-157">You can learn more about PsPing by reading hello [PsPing download page](https://technet.microsoft.com/sysinternals/psping.aspx)</span></span>
   
    <span data-ttu-id="c6f4e-158">Vous pouvez ou supprimez des règles à partir d’un groupe de sécurité réseau en utilisant les informations de hello sortie hello hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="c6f4e-158">You can or remove rules from an NSG by using hello information in hello output from hello following command:</span></span>
   
        Get-Help *-AzureRmNetworkSecurityRuleConfig

## <a name="considerations"></a><span data-ttu-id="c6f4e-159">Considérations</span><span class="sxs-lookup"><span data-stu-id="c6f4e-159">Considerations</span></span>
<span data-ttu-id="c6f4e-160">Tenez compte des points suivants lors de la résolution des problèmes de connectivité de hello :</span><span class="sxs-lookup"><span data-stu-id="c6f4e-160">Consider hello following points when troubleshooting connectivity problems:</span></span>

* <span data-ttu-id="c6f4e-161">Règles du groupe de sécurité réseau par défaut bloque l’accès entrant à partir de hello internet et seulement ce réseau virtuel qui permet le trafic entrant.</span><span class="sxs-lookup"><span data-stu-id="c6f4e-161">Default NSG rules will block inbound access from hello internet and only permit VNet inbound traffic.</span></span> <span data-ttu-id="c6f4e-162">Les règles doivent être ajoutés explicitement tooallow accès entrant depuis Internet, en fonction des besoins.</span><span class="sxs-lookup"><span data-stu-id="c6f4e-162">Rules should be explicitly added tooallow inbound access from Internet, as required.</span></span>
* <span data-ttu-id="c6f4e-163">S’il n’y a aucune règle de sécurité groupe de sécurité réseau à l’origine de toofail de connectivité de réseau de l’ordinateur virtuel, problème de hello peut être due à :</span><span class="sxs-lookup"><span data-stu-id="c6f4e-163">If there are no NSG security rules causing a VM’s network connectivity toofail, hello problem may be due to:</span></span>
  * <span data-ttu-id="c6f4e-164">Logiciel de pare-feu qui s’exécutent dans le système d’exploitation de la machine virtuelle hello</span><span class="sxs-lookup"><span data-stu-id="c6f4e-164">Firewall software running within hello VM's operating system</span></span>
  * <span data-ttu-id="c6f4e-165">Itinéraires configurés pour des appliances virtuelles ou un trafic local.</span><span class="sxs-lookup"><span data-stu-id="c6f4e-165">Routes configured for virtual appliances or on-premises traffic.</span></span> <span data-ttu-id="c6f4e-166">Le trafic Internet peut être redirigé tooon-site via le tunneling forcé.</span><span class="sxs-lookup"><span data-stu-id="c6f4e-166">Internet traffic can be redirected tooon-premises via forced-tunneling.</span></span> <span data-ttu-id="c6f4e-167">Une connexion RDP/SSH à partir de hello Internet tooyour machine virtuelle peut ne pas fonctionne avec ce paramètre, selon la façon dont le matériel de réseau local hello gère ce trafic.</span><span class="sxs-lookup"><span data-stu-id="c6f4e-167">An RDP/SSH connection from hello Internet tooyour VM may not work with this setting, depending on how hello on-premises network hardware handles this traffic.</span></span> <span data-ttu-id="c6f4e-168">Hello de lecture [dépannage des itinéraires](virtual-network-routes-troubleshoot-powershell.md) article toolearn, comment les problèmes d’itinéraire toodiagnose qui peuvent être compromettent hello flux du trafic et se déconnecte de hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="c6f4e-168">Read hello [Troubleshooting Routes](virtual-network-routes-troubleshoot-powershell.md) article toolearn how toodiagnose route problems that may be impeding hello flow of traffic in and out of hello VM.</span></span> 
* <span data-ttu-id="c6f4e-169">Si vous avez homologuer les réseaux virtuels, par défaut, hello balise VIRTUAL_NETWORK développe automatiquement les préfixes tooinclude pour les réseaux virtuels de ressources.</span><span class="sxs-lookup"><span data-stu-id="c6f4e-169">If you have peered VNets, by default, hello VIRTUAL_NETWORK tag will automatically expand tooinclude prefixes for peered VNets.</span></span> <span data-ttu-id="c6f4e-170">Vous pouvez afficher ces préfixes Bonjour **ExpandedAddressPrefix** répertorier, tootroubleshoot tout tooVNet connexes de problèmes d’homologation de connectivité.</span><span class="sxs-lookup"><span data-stu-id="c6f4e-170">You can view these prefixes in hello **ExpandedAddressPrefix** list, tootroubleshoot any issues related tooVNet peering connectivity.</span></span> 
* <span data-ttu-id="c6f4e-171">Les règles de sécurité efficace sont affichent uniquement s’il existe qu'un groupe de sécurité réseau associé à la machine virtuelle hello NIC et ou un sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="c6f4e-171">Effective security rules are only shown if there is an NSG associated with hello VM’s NIC and or subnet.</span></span> 
* <span data-ttu-id="c6f4e-172">Si aucun groupes de sécurité réseau associés hello carte réseau ou sous-réseau et que vous avez une adresse IP publique affectée tooyour machine virtuelle, tous les ports seront ouverts pour un accès entrant et sortant.</span><span class="sxs-lookup"><span data-stu-id="c6f4e-172">If there are no NSGs associated with hello NIC or subnet and you have a public IP address assigned tooyour VM, all ports will be open for inbound and outbound access.</span></span> <span data-ttu-id="c6f4e-173">Si hello machine virtuelle a une adresse IP publique, appliquer des groupes de sécurité réseau toohello carte réseau ou sous-réseau est fortement recommandé.</span><span class="sxs-lookup"><span data-stu-id="c6f4e-173">If hello VM has a public IP address, applying NSGs toohello NIC or subnet is strongly recommended.</span></span>  

