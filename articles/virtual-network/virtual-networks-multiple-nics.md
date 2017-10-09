---
title: "aaaCreate une machine virtuelle (classique) avec plusieurs cartes réseau à l’aide de PowerShell | Documents Microsoft"
description: "Découvrez comment toocreate et configurer des machines virtuelles avec plusieurs cartes réseau à l’aide de PowerShell."
services: virtual-network, virtual-machines
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
tags: azure-service-management
ms.assetid: a1a3952c-2dcc-4977-bd7a-52d623c1fb07
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.openlocfilehash: 8ef35bd4cfd7e6a527080f1cfc541275ca86f5e7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-classic-with-multiple-nics"></a><span data-ttu-id="db8ac-103">Créer une machine virtuelle (classique) avec plusieurs cartes réseau</span><span class="sxs-lookup"><span data-stu-id="db8ac-103">Create a VM (Classic) with multiple NICs</span></span>
<span data-ttu-id="db8ac-104">Vous pouvez créer des machines virtuelles (VM) dans Azure et attacher plusieurs tooeach de cartes réseau de vos ordinateurs virtuels.</span><span class="sxs-lookup"><span data-stu-id="db8ac-104">You can create virtual machines (VMs) in Azure and attach multiple network interfaces (NICs) tooeach of your VMs.</span></span> <span data-ttu-id="db8ac-105">Il s’agit d’une exigence pour de nombreuses appliances virtuelles réseau, comme les solutions de distribution d’applications et d’optimisation de réseau étendu (WAN).</span><span class="sxs-lookup"><span data-stu-id="db8ac-105">Multiple NICs are a requirement for many network virtual appliances, such as application delivery and WAN optimization solutions.</span></span> <span data-ttu-id="db8ac-106">La présence de plusieurs cartes réseau assure aussi une isolation du trafic entre les cartes réseau.</span><span class="sxs-lookup"><span data-stu-id="db8ac-106">Multiple NICs also provide isolation of traffic between NICs.</span></span>

![Fonctionnalité Multi-NIC pour machine virtuelle](./media/virtual-networks-multiple-nics/IC757773.png)

<span data-ttu-id="db8ac-108">Hello figure illustre une machine virtuelle avec trois cartes réseau, chacun connecté tooa autre sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="db8ac-108">hello figure shows a VM with three NICs, each connected tooa different subnet.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="db8ac-109">Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [Resource Manager et classique](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="db8ac-109">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="db8ac-110">Cet article décrit à l’aide du modèle de déploiement classique hello.</span><span class="sxs-lookup"><span data-stu-id="db8ac-110">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="db8ac-111">Pour la plupart des nouveaux déploiements, Microsoft recommande d’utiliser Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="db8ac-111">Microsoft recommends that most new deployments use Resource Manager.</span></span>

* <span data-ttu-id="db8ac-112">Adresse IP virtuelle sur Internet (déploiements classiques) est uniquement pris en charge sur hello, « default » NIC.</span><span class="sxs-lookup"><span data-stu-id="db8ac-112">Internet-facing VIP (classic deployments) is only supported on hello "default" NIC.</span></span> <span data-ttu-id="db8ac-113">Il est IP de toohello qu’une seule adresse IP virtuelle de NIC hello par défaut.</span><span class="sxs-lookup"><span data-stu-id="db8ac-113">There is only one VIP toohello IP of hello default NIC.</span></span>
* <span data-ttu-id="db8ac-114">Pour l’instant, les adresses IP publiques de niveau d’instance (LPIP) (déploiements classiques) ne sont pas prises en charge pour les machines virtuelles à plusieurs NIC.</span><span class="sxs-lookup"><span data-stu-id="db8ac-114">At this time, Instance Level Public IP (LPIP) addresses (classic deployments) are not supported for multi NIC VMs.</span></span>
* <span data-ttu-id="db8ac-115">Hello ordre des NIC hello à l’intérieur de hello machine virtuelle est aléatoire et peut également changer entre les mises à jour de l’infrastructure Azure.</span><span class="sxs-lookup"><span data-stu-id="db8ac-115">hello order of hello NICs from inside hello VM will be random, and could also change across Azure infrastructure updates.</span></span> <span data-ttu-id="db8ac-116">Toutefois, hello des adresses IP et hello correspondant ethernet MAC adresses resteront identiques hello.</span><span class="sxs-lookup"><span data-stu-id="db8ac-116">However, hello IP addresses, and hello corresponding ethernet MAC addresses will remain hello same.</span></span> <span data-ttu-id="db8ac-117">Par exemple, supposons que **Eth1** a l’adresse IP 10.1.0.100 et une adresse MAC 00-0D-3A-B0-39-0D ; après une mise à jour de l’infrastructure Azure et un redémarrage, il peut être modifié trop**Eth2**, mais hello IP et MAC appariement va restent identiques hello.</span><span class="sxs-lookup"><span data-stu-id="db8ac-117">For example, assume **Eth1** has IP address 10.1.0.100 and MAC address 00-0D-3A-B0-39-0D; after an Azure infrastructure update and reboot, it could be changed too**Eth2**, but hello IP and MAC pairing will remain hello same.</span></span> <span data-ttu-id="db8ac-118">Lorsqu’un redémarrage est lancée par le client, hello ordre des NIC reste identique hello.</span><span class="sxs-lookup"><span data-stu-id="db8ac-118">When a restart is customer-initiated, hello NIC order will remain hello same.</span></span>
* <span data-ttu-id="db8ac-119">Hello adresse pour chaque carte réseau sur chaque machine virtuelle doit se trouver dans un sous-réseau, plusieurs cartes réseau sur un seul ordinateur virtuel peut chacun avoir des adresses qui se trouvent dans hello même sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="db8ac-119">hello address for each NIC on each VM must be located in a subnet, multiple NICs on a single VM can each be assigned addresses that are in hello same subnet.</span></span>
* <span data-ttu-id="db8ac-120">Hello taille de machine virtuelle détermine le nombre de hello de cartes réseau que vous pouvez créer pour une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="db8ac-120">hello VM size determines hello number of NICS that you can create for a VM.</span></span> <span data-ttu-id="db8ac-121">Hello de référence [Windows Server](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) et [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) combien de cartes réseau prend en charge la taille de chaque machine virtuelle articles toodetermine des tailles de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="db8ac-121">Reference hello [Windows Server](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) and [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) VM sizes articles toodetermine how many NICS each VM size supports.</span></span> 

## <a name="network-security-groups-nsgs"></a><span data-ttu-id="db8ac-122">Groupes de sécurité réseau (NSG)</span><span class="sxs-lookup"><span data-stu-id="db8ac-122">Network Security Groups (NSGs)</span></span>
<span data-ttu-id="db8ac-123">Dans un déploiement avec gestionnaire de ressources, les NIC d’une machine virtuelle peuvent être associées à un groupe de sécurité réseau (NSG), y compris les NIC d’une machine virtuelle sur laquelle la fonctionnalité Multi-NIC est activée.</span><span class="sxs-lookup"><span data-stu-id="db8ac-123">In a Resource Manager deployment, any NIC on a VM may be associated with a Network Security Group (NSG), including any NICs on a VM that has multiple NICs enabled.</span></span> <span data-ttu-id="db8ac-124">Si une adresse dans un sous-réseau dans lequel le sous-réseau de hello est associé à un groupe de sécurité réseau est assignée à une carte réseau, puis hello règles dans le groupe de sécurité réseau du sous-réseau hello s’appliquent également toothat carte</span><span class="sxs-lookup"><span data-stu-id="db8ac-124">If a NIC is assigned an address within a subnet where hello subnet is associated with an NSG, then hello rules in hello subnet’s NSG also apply toothat NIC.</span></span> <span data-ttu-id="db8ac-125">Dans des sous-réseaux tooassociating addition avec des groupes de sécurité réseau, vous pouvez également associer une carte réseau avec un groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="db8ac-125">In addition tooassociating subnets with NSGs, you can also associate a NIC with an NSG.</span></span>

<span data-ttu-id="db8ac-126">Si un sous-réseau est associé à un groupe de sécurité réseau et une carte réseau au sein de ce sous-réseau est individuellement associé à un groupe de sécurité réseau, les règles de groupe de sécurité réseau hello associée sont appliquées dans **flux ordre** selon la direction de toohello du trafic de hello transmis vers ou depuis Hello carte réseau :</span><span class="sxs-lookup"><span data-stu-id="db8ac-126">If a subnet is associated with an NSG, and a NIC within that subnet is individually associated with an NSG, hello associated NSG rules are applied in **flow order** according toohello direction of hello traffic being passed into or out of hello NIC:</span></span>

* <span data-ttu-id="db8ac-127">**Le trafic entrant** sous-réseau hello, déclencher des règles de groupe de sécurité réseau du sous-réseau hello, avant de passer dans hello carte réseau, puis déclencher des règles de groupe de sécurité réseau hello carte d’interface réseau dont la destination est hello NIC en question parcourt tout d’abord.</span><span class="sxs-lookup"><span data-stu-id="db8ac-127">**Incoming traffic** whose destination is hello NIC in question flows first through hello subnet, triggering hello subnet’s NSG rules, before passing into hello NIC, then triggering hello NIC’s NSG rules.</span></span>
* <span data-ttu-id="db8ac-128">**Le trafic sortant** dont la source est hello NIC en question flux premier sorti de hello NIC, déclencher des règles de groupe de sécurité réseau hello carte d’interface réseau, avant de passer par le sous-réseau de hello, puis déclencher des règles de groupe de sécurité réseau du sous-réseau hello.</span><span class="sxs-lookup"><span data-stu-id="db8ac-128">**Outgoing traffic** whose source is hello NIC in question flows first out from hello NIC, triggering hello NIC’s NSG rules, before passing through hello subnet, then triggering hello subnet’s NSG rules.</span></span>

<span data-ttu-id="db8ac-129">En savoir plus sur [groupes de sécurité réseau](virtual-networks-nsg.md) et comment elles sont appliquées selon les associations toosubnets, les machines virtuelles et les cartes réseau...</span><span class="sxs-lookup"><span data-stu-id="db8ac-129">Learn more about [Network Security Groups](virtual-networks-nsg.md) and how they are applied based on associations toosubnets, VMs, and NICs..</span></span>

## <a name="how-tooconfigure-a-multi-nic-vm-in-a-classic-deployment"></a><span data-ttu-id="db8ac-130">Comment tooConfigure un plusieurs NIC VM dans un déploiement classique</span><span class="sxs-lookup"><span data-stu-id="db8ac-130">How tooConfigure a multi NIC VM in a classic deployment</span></span>
<span data-ttu-id="db8ac-131">instructions Hello ci-dessous vous aide à créer un multi VM NIC contenant 3 NIC : une carte réseau par défaut et deux cartes réseau supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="db8ac-131">hello instructions below will help you create a multi NIC VM containing 3 NICs: a default NIC and two additional NICs.</span></span> <span data-ttu-id="db8ac-132">étapes de configuration Hello va créer une machine virtuelle qui est configurée en fonction de fragment de fichier de configuration d’un service de toohello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="db8ac-132">hello configuration steps will create a VM that will be configured according toohello service configuration file fragment below:</span></span>

    <VirtualNetworkSite name="MultiNIC-VNet" Location="North Europe">
    <AddressSpace>
      <AddressPrefix>10.1.0.0/16</AddressPrefix>
        </AddressSpace>
        <Subnets>
          <Subnet name="Frontend">
            <AddressPrefix>10.1.0.0/24</AddressPrefix>
          </Subnet>
          <Subnet name="Midtier">
            <AddressPrefix>10.1.1.0/24</AddressPrefix>
          </Subnet>
          <Subnet name="Backend">
            <AddressPrefix>10.1.2.0/23</AddressPrefix>
          </Subnet>
          <Subnet name="GatewaySubnet">
            <AddressPrefix>10.1.200.0/28</AddressPrefix>
          </Subnet>
        </Subnets>
    … Skip over hello remainder section …
    </VirtualNetworkSite>


<span data-ttu-id="db8ac-133">Vous devez hello suivant des conditions préalables avant d’essayer de commandes PowerShell hello exemple toorun hello.</span><span class="sxs-lookup"><span data-stu-id="db8ac-133">You need hello following prerequisites before trying toorun hello PowerShell commands in hello example.</span></span>

* <span data-ttu-id="db8ac-134">Un abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="db8ac-134">An Azure subscription.</span></span>
* <span data-ttu-id="db8ac-135">Un réseau virtuel configuré.</span><span class="sxs-lookup"><span data-stu-id="db8ac-135">A configured virtual network.</span></span> <span data-ttu-id="db8ac-136">Pour plus d’informations sur les réseaux virtuels, voir l’article [Présentation du réseau virtuel](virtual-networks-overview.md) .</span><span class="sxs-lookup"><span data-stu-id="db8ac-136">See [Virtual Network Overview](virtual-networks-overview.md) for more information about VNets.</span></span>
* <span data-ttu-id="db8ac-137">version la plus récente d’Azure PowerShell Hello téléchargé et installé.</span><span class="sxs-lookup"><span data-stu-id="db8ac-137">hello latest version of Azure PowerShell downloaded and installed.</span></span> <span data-ttu-id="db8ac-138">Consultez [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="db8ac-138">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="db8ac-139">toocreate une machine virtuelle avec plusieurs cartes réseau, hello complète à l’aide de chaque commande dans une session PowerShell unique comme suit :</span><span class="sxs-lookup"><span data-stu-id="db8ac-139">toocreate a VM with multiple NICs, complete hello following steps by entering each command within a single PowerShell session:</span></span>

1. <span data-ttu-id="db8ac-140">Sélectionnez une image de machine virtuelle dans la galerie d’images de machine virtuelle Azure.</span><span class="sxs-lookup"><span data-stu-id="db8ac-140">Select a VM image from Azure VM image gallery.</span></span> <span data-ttu-id="db8ac-141">Notez que les images changent fréquemment et sont disponibles par région.</span><span class="sxs-lookup"><span data-stu-id="db8ac-141">Note that images change frequently and are available by region.</span></span> <span data-ttu-id="db8ac-142">Hello image spécifiée dans l’exemple hello ci-dessous peut modifier ou peut pas se trouver dans votre région, veillez donc à image de hello toospecify vous avez besoin.</span><span class="sxs-lookup"><span data-stu-id="db8ac-142">hello image specified in hello example below may change or might not be in your region, so be sure toospecify hello image you need.</span></span>

    ```powershell
    $image = Get-AzureVMImage `
    -ImageName "a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-R2-201410.01-en.us-127GB.vhd"
    ```

2. <span data-ttu-id="db8ac-143">Créez une configuration de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="db8ac-143">Create a VM configuration.</span></span>

    ```powershell
    $vm = New-AzureVMConfig -Name "MultiNicVM" -InstanceSize "ExtraLarge" `
    -Image $image.ImageName –AvailabilitySetName "MyAVSet"
    ```

3. <span data-ttu-id="db8ac-144">Créer la connexion de l’administrateur par défaut hello.</span><span class="sxs-lookup"><span data-stu-id="db8ac-144">Create hello default administrator login.</span></span>

    ```powershell
    Add-AzureProvisioningConfig –VM $vm -Windows -AdminUserName "<YourAdminUID>" `
    -Password "<YourAdminPassword>"
    ```

4. <span data-ttu-id="db8ac-145">Ajouter la configuration de machine virtuelle toohello cartes réseau supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="db8ac-145">Add additional NICs toohello VM configuration.</span></span>

    ```powershell
    Add-AzureNetworkInterfaceConfig -Name "Ethernet1" `
    -SubnetName "Midtier" -StaticVNetIPAddress "10.1.1.111" -VM $vm
    Add-AzureNetworkInterfaceConfig -Name "Ethernet2" `
    -SubnetName "Backend" -StaticVNetIPAddress "10.1.2.222" -VM $vm
    ```

5. <span data-ttu-id="db8ac-146">Spécifiez le sous-réseau de hello et l’adresse IP pour NIC hello par défaut.</span><span class="sxs-lookup"><span data-stu-id="db8ac-146">Specify hello subnet and IP address for hello default NIC.</span></span>

    ```powershell
    Set-AzureSubnet -SubnetNames "Frontend" -VM $vm
    Set-AzureStaticVNetIP -IPAddress "10.1.0.100" -VM $vm
    ```

6. <span data-ttu-id="db8ac-147">Créez hello machine virtuelle dans votre réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="db8ac-147">Create hello VM in your virtual network.</span></span>

    ```powershell
    New-AzureVM -ServiceName "MultiNIC-CS" –VNetName "MultiNIC-VNet" –VMs $vm
    ```

    > [!NOTE]
    > <span data-ttu-id="db8ac-148">Hello réseau virtuel que vous spécifiez ici doit déjà exister (comme indiqué dans les conditions préalables de hello).</span><span class="sxs-lookup"><span data-stu-id="db8ac-148">hello VNet that you specify here must already exist (as mentioned in hello prerequisites).</span></span> <span data-ttu-id="db8ac-149">exemple Hello ci-dessous spécifie un réseau virtuel nommé **MultiNIC-VNet**.</span><span class="sxs-lookup"><span data-stu-id="db8ac-149">hello example below specifies a virtual network named **MultiNIC-VNet**.</span></span>
    >

## <a name="limitations"></a><span data-ttu-id="db8ac-150">Limites</span><span class="sxs-lookup"><span data-stu-id="db8ac-150">Limitations</span></span>
<span data-ttu-id="db8ac-151">Hello limites suivantes s’appliquent lors de l’utilisation de plusieurs cartes réseau :</span><span class="sxs-lookup"><span data-stu-id="db8ac-151">hello following limitations are applicable when using multiple NICs:</span></span>

* <span data-ttu-id="db8ac-152">Les machines virtuelles à plusieurs cartes réseau doivent être créées dans des réseaux virtuels Azure.</span><span class="sxs-lookup"><span data-stu-id="db8ac-152">VMs with multiple NICs must be created in Azure virtual networks (VNets).</span></span> <span data-ttu-id="db8ac-153">Les machines virtuelles n’appartenant pas à un réseau virtuel ne peuvent pas être configurées avec plusieurs cartes réseau.</span><span class="sxs-lookup"><span data-stu-id="db8ac-153">Non-VNet VMs cannot be configured with multiple NICs.</span></span>
* <span data-ttu-id="db8ac-154">Tous les ordinateurs virtuels d’un groupe défini besoin toouse plusieurs cartes réseau ou une carte réseau. unique</span><span class="sxs-lookup"><span data-stu-id="db8ac-154">All VMs in an availability set need toouse either multiple NICs or a single NIC.</span></span> <span data-ttu-id="db8ac-155">La cohabitation entre des machines virtuelles à plusieurs cartes réseau et des machines virtuelles à une seule carte réseau n’est pas possible au sein d’un groupe à haute disponibilité.</span><span class="sxs-lookup"><span data-stu-id="db8ac-155">There cannot be a mixture of multiple NIC VMs and single NIC VMs within an availability set.</span></span> <span data-ttu-id="db8ac-156">Les mêmes règles s’appliquent pour les machines virtuelles dans un service cloud.</span><span class="sxs-lookup"><span data-stu-id="db8ac-156">Same rules apply for VMs in a cloud service.</span></span> <span data-ttu-id="db8ac-157">Pour plusieurs machines virtuelles de carte réseau, ils ne sont pas indispensables toohave hello même nombre de cartes réseau, tant qu’ils ont chacun au moins deux.</span><span class="sxs-lookup"><span data-stu-id="db8ac-157">For multiple NIC VMs, they aren't required toohave hello same number of NICs, as long as they each have at least two.</span></span>
* <span data-ttu-id="db8ac-158">Une machine virtuelle à une seule carte réseau ne peut pas être configurée avec plusieurs cartes réseau (et inversement) une fois qu’elle est déployée. Il faut la supprimer et la recréer.</span><span class="sxs-lookup"><span data-stu-id="db8ac-158">A VM with a single NIC cannot be configured with multi NICs (and vice-versa) once it is deployed, without deleting and re-creating it.</span></span>

## <a name="secondary-nics-access-tooother-subnets"></a><span data-ttu-id="db8ac-159">Cartes d’interface réseau secondaire accéder aux sous-réseaux de tooother</span><span class="sxs-lookup"><span data-stu-id="db8ac-159">Secondary NICs access tooother subnets</span></span>
<span data-ttu-id="db8ac-160">Par défaut de cartes d’interface réseau secondaire ne seront pas configurés avec une passerelle par défaut, en raison de flux de trafic toowhich hello sur hello NIC secondaire sera limité toobe dans hello même sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="db8ac-160">By default secondary NICs will not be configured with a default gateway, due toowhich hello traffic flow on hello secondary NICs will be limited toobe within hello same subnet.</span></span> <span data-ttu-id="db8ac-161">Si les utilisateurs de hello souhaitent tooenable tootalk de cartes d’interface réseau secondaire à l’extérieur de leur propre sous-réseau, ils devront tooadd une entrée dans hello table tooconfigure hello passerelle de routage comme décrit ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="db8ac-161">If hello users want tooenable secondary NICs tootalk outside their own subnet, they will need tooadd an entry in hello routing table tooconfigure hello gateway as described below.</span></span>

> [!NOTE]
> <span data-ttu-id="db8ac-162">Les machines virtuelles créées avant juillet 2015 peuvent avoir une passerelle par défaut configurée pour toutes les cartes réseau.</span><span class="sxs-lookup"><span data-stu-id="db8ac-162">VMs created before July 2015 may have a default gateway configured for all NICs.</span></span> <span data-ttu-id="db8ac-163">passerelle par défaut de Hello pour les cartes réseau secondaire n’est pas supprimé jusqu'à ce que ces machines virtuelles sont redémarrés.</span><span class="sxs-lookup"><span data-stu-id="db8ac-163">hello default gateway for secondary NICs will not be removed until these VMs are rebooted.</span></span> <span data-ttu-id="db8ac-164">Dans les systèmes d’exploitation qui utilisent le modèle de routage d’hôte faible hello, tels que Linux, une connectivité Internet peut cesser de fonctionner si le trafic entrant et sortant hello utilise différentes cartes réseau.</span><span class="sxs-lookup"><span data-stu-id="db8ac-164">In Operating systems that use hello weak host routing model, such as Linux, Internet connectivity can break if hello ingress and egress traffic use different NICs.</span></span>
> 

### <a name="configure-windows-vms"></a><span data-ttu-id="db8ac-165">Configurer les machines virtuelles Windows</span><span class="sxs-lookup"><span data-stu-id="db8ac-165">Configure Windows VMs</span></span>
<span data-ttu-id="db8ac-166">Supposons que vous disposiez d’une machine virtuelle Windows avec deux cartes réseau, comme suit :</span><span class="sxs-lookup"><span data-stu-id="db8ac-166">Suppose that you have a Windows VM with two NICs as follows:</span></span>

* <span data-ttu-id="db8ac-167">Adresse IP de la carte réseau principale : 192.168.1.4</span><span class="sxs-lookup"><span data-stu-id="db8ac-167">Primary NIC IP address: 192.168.1.4</span></span>
* <span data-ttu-id="db8ac-168">Adresse IP de la carte réseau secondaire : 192.168.2.5</span><span class="sxs-lookup"><span data-stu-id="db8ac-168">Secondary NIC IP address: 192.168.2.5</span></span>

<span data-ttu-id="db8ac-169">table de routage IPv4 Hello pour cet ordinateur virtuel ressemble à ceci :</span><span class="sxs-lookup"><span data-stu-id="db8ac-169">hello IPv4 route table for this VM would look like this:</span></span>

    IPv4 Route Table
    ===========================================================================
    Active Routes:
    Network Destination        Netmask          Gateway       Interface  Metric
              0.0.0.0          0.0.0.0      192.168.1.1      192.168.1.4      5
            127.0.0.0        255.0.0.0         On-link         127.0.0.1    306
            127.0.0.1  255.255.255.255         On-link         127.0.0.1    306
      127.255.255.255  255.255.255.255         On-link         127.0.0.1    306
        168.63.129.16  255.255.255.255      192.168.1.1      192.168.1.4      6
          192.168.1.0    255.255.255.0         On-link       192.168.1.4    261
          192.168.1.4  255.255.255.255         On-link       192.168.1.4    261
        192.168.1.255  255.255.255.255         On-link       192.168.1.4    261
          192.168.2.0    255.255.255.0         On-link       192.168.2.5    261
          192.168.2.5  255.255.255.255         On-link       192.168.2.5    261
        192.168.2.255  255.255.255.255         On-link       192.168.2.5    261
            224.0.0.0        240.0.0.0         On-link         127.0.0.1    306
            224.0.0.0        240.0.0.0         On-link       192.168.1.4    261
            224.0.0.0        240.0.0.0         On-link       192.168.2.5    261
      255.255.255.255  255.255.255.255         On-link         127.0.0.1    306
      255.255.255.255  255.255.255.255         On-link       192.168.1.4    261
      255.255.255.255  255.255.255.255         On-link       192.168.2.5    261
    ===========================================================================

<span data-ttu-id="db8ac-170">Notez que cet itinéraire par défaut de hello (0.0.0.0) est uniquement une carte principal toohello disponibles</span><span class="sxs-lookup"><span data-stu-id="db8ac-170">Notice that hello default route (0.0.0.0) is only available toohello primary NIC.</span></span> <span data-ttu-id="db8ac-171">Vous ne serez pas tooaccess en mesure des ressources à l’extérieur du sous-réseau hello pour hello secondaire carte réseau, comme indiqué ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="db8ac-171">You will not be able tooaccess resources outside hello subnet for hello secondary NIC, as seen below:</span></span>

    C:\Users\Administrator>ping 192.168.1.7 -S 192.165.2.5

    Pinging 192.168.1.7 from 192.165.2.5 with 32 bytes of data:
    PING: transmit failed. General failure.
    PING: transmit failed. General failure.
    PING: transmit failed. General failure.
    PING: transmit failed. General failure.

<span data-ttu-id="db8ac-172">tooadd un itinéraire par défaut sur hello NIC secondaire, hello suivez les étapes ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="db8ac-172">tooadd a default route on hello secondary NIC, follow hello steps below:</span></span>

1. <span data-ttu-id="db8ac-173">À partir d’une invite de commandes, exécuter la commande hello ci-dessous le numéro d’index tooidentify hello pour hello NIC secondaire :</span><span class="sxs-lookup"><span data-stu-id="db8ac-173">From a command prompt, run hello command below tooidentify hello index number for hello secondary NIC:</span></span>
   
        C:\Users\Administrator>route print
        ===========================================================================
        Interface List
         29...00 15 17 d9 b1 6d ......Microsoft Virtual Machine Bus Network Adapter #16
         27...00 15 17 d9 b1 41 ......Microsoft Virtual Machine Bus Network Adapter #14
          1...........................Software Loopback Interface 1
         14...00 00 00 00 00 00 00 e0 Teredo Tunneling Pseudo-Interface
         20...00 00 00 00 00 00 00 e0 Microsoft ISATAP Adapter #2
        ===========================================================================
2. <span data-ttu-id="db8ac-174">Notez la deuxième entrée de hello dans la table hello, avec un index de 27 (dans cet exemple).</span><span class="sxs-lookup"><span data-stu-id="db8ac-174">Notice hello second entry in hello table, with an index of 27 (in this example).</span></span>
3. <span data-ttu-id="db8ac-175">À partir de l’invite de commandes hello, exécutez hello **itinéraire ajouter** commande comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="db8ac-175">From hello command prompt, run hello **route add** command as shown below.</span></span> <span data-ttu-id="db8ac-176">Dans cet exemple, vous spécifiez 192.168.2.1 en tant que passerelle par défaut de hello pour hello NIC secondaire :</span><span class="sxs-lookup"><span data-stu-id="db8ac-176">In this example, you are specifying 192.168.2.1 as hello default gateway for hello secondary NIC:</span></span>
   
        route ADD -p 0.0.0.0 MASK 0.0.0.0 192.168.2.1 METRIC 5000 IF 27
4. <span data-ttu-id="db8ac-177">tootest connectivité, invite de commandes toohello revenir en arrière et essayez tooping un sous-réseau différent de celui hello NIC secondaire en tant qu’int indiqué eh exemple ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="db8ac-177">tootest connectivity, go back toohello command prompt and try tooping a different subnet from hello secondary NIC as shown int eh example below:</span></span>
   
        C:\Users\Administrator>ping 192.168.1.7 -S 192.165.2.5
   
        Reply from 192.168.1.7: bytes=32 time<1ms TTL=128
        Reply from 192.168.1.7: bytes=32 time<1ms TTL=128
        Reply from 192.168.1.7: bytes=32 time=2ms TTL=128
        Reply from 192.168.1.7: bytes=32 time<1ms TTL=128
5. <span data-ttu-id="db8ac-178">Vous pouvez également vérifier votre hello toocheck de table itinéraire récemment ajouté itinéraire, comme indiqué ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="db8ac-178">You can also check your route table toocheck hello newly added route, as shown below:</span></span>
   
        C:\Users\Administrator>route print
   
        ...
   
        IPv4 Route Table
        ===========================================================================
        Active Routes:
        Network Destination        Netmask          Gateway       Interface  Metric
                  0.0.0.0          0.0.0.0      192.168.1.1      192.168.1.4      5
                  0.0.0.0          0.0.0.0      192.168.2.1      192.168.2.5   5005
                127.0.0.0        255.0.0.0         On-link         127.0.0.1    306

### <a name="configure-linux-vms"></a><span data-ttu-id="db8ac-179">Configurer des machines virtuelles Linux</span><span class="sxs-lookup"><span data-stu-id="db8ac-179">Configure Linux VMs</span></span>
<span data-ttu-id="db8ac-180">Pour les machines virtuelles Linux, par défaut hello utilise hôte faible routage, il est recommandé que hello NIC secondaire sont des flux tootraffic restreint uniquement dans hello même sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="db8ac-180">For Linux VMs, since hello default behavior uses weak host routing, we recommend that hello secondary NICs are restricted tootraffic flows only within hello same subnet.</span></span> <span data-ttu-id="db8ac-181">Toutefois si certains scénarios exigent de connectivité en dehors du sous-réseau de hello, les utilisateurs doivent activer tooensure de routage basée sur la stratégie qui hello en entrée et sortie trafic utilise hello même carte réseau.</span><span class="sxs-lookup"><span data-stu-id="db8ac-181">However if certain scenarios demand connectivity outside hello subnet, users should enable policy based routing tooensure that hello ingress and egress traffic uses hello same NIC.</span></span>

## <a name="next-steps"></a><span data-ttu-id="db8ac-182">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="db8ac-182">Next steps</span></span>
* <span data-ttu-id="db8ac-183">Déploiement de [machines virtuelles MultiNIC dans un scénario d’application à 2 niveaux pour un déploiement Resource Manager](virtual-network-deploy-multinic-arm-template.md).</span><span class="sxs-lookup"><span data-stu-id="db8ac-183">Deploy [MultiNIC VMs in a 2-tier application scenario in a Resource Manager deployment](virtual-network-deploy-multinic-arm-template.md).</span></span>
* <span data-ttu-id="db8ac-184">Déploiement de [machines virtuelles MultiNIC dans un scénario d’application à 2 niveaux pour un déploiement classique](virtual-network-deploy-multinic-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="db8ac-184">Deploy [MultiNIC VMs in a 2-tier application scenario in a classic deployment](virtual-network-deploy-multinic-classic-ps.md).</span></span>

