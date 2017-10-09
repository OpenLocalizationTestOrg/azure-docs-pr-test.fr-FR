---
title: "aaaCreate une machine virtuelle avec plusieurs cartes réseau - Azure CLI 2.0 | Documents Microsoft"
description: "Découvrez comment toocreate une machine virtuelle avec plusieurs cartes réseau à l’aide de hello Azure CLI 2.0."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 8e906a4b-8583-4a97-9416-ee34cfa09a98
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ac0291a978e2c8682c69104915196cc6c4fcf8dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-multiple-nics-using-hello-azure-cli-20"></a><span data-ttu-id="e3347-103">Créer une machine virtuelle avec plusieurs cartes réseau à l’aide de hello Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="e3347-103">Create a VM with multiple NICs using hello Azure CLI 2.0</span></span>

[!INCLUDE [virtual-network-deploy-multinic-arm-selectors-include.md](../../includes/virtual-network-deploy-multinic-arm-selectors-include.md)]

[!INCLUDE [virtual-network-deploy-multinic-intro-include.md](../../includes/virtual-network-deploy-multinic-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="e3347-104">Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [Resource Manager et classique](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="e3347-104">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="e3347-105">Cet article couvre l’utilisation de modèle de déploiement Resource Manager hello, qui recommandées par Microsoft pour la plupart des déploiements de nouveau au lieu de hello [modèle de déploiement classique](virtual-network-deploy-multinic-classic-cli.md).</span><span class="sxs-lookup"><span data-stu-id="e3347-105">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello [classic deployment model](virtual-network-deploy-multinic-classic-cli.md).</span></span>
>

## <span data-ttu-id="e3347-106"><a name="create"></a>Créer hello machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="e3347-106"><a name="create"></a>Create hello VM</span></span>

<span data-ttu-id="e3347-107">Vous pouvez effectuer cette tâche à l’aide de hello Azure CLI 2.0 (cet article) ou hello [Azure CLI 1.0](virtual-network-deploy-multinic-cli-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="e3347-107">You can complete this task using hello Azure CLI 2.0 (this article) or hello [Azure CLI 1.0](virtual-network-deploy-multinic-cli-nodejs.md).</span></span> <span data-ttu-id="e3347-108">Hello dans les valeurs « » pour les variables hello dans les étapes de hello qui suivent créer des ressources avec les paramètres d’un scénario de hello.</span><span class="sxs-lookup"><span data-stu-id="e3347-108">hello values in "" for hello variables in hello steps that follow create resources with settings from hello scenario.</span></span> <span data-ttu-id="e3347-109">Modifier les valeurs hello, comme il convient pour votre environnement.</span><span class="sxs-lookup"><span data-stu-id="e3347-109">Change hello values, as appropriate, for your environment.</span></span>

1. <span data-ttu-id="e3347-110">Installer hello [Azure CLI 2.0](/cli/azure/install-az-cli2) si vous n’en avez pas encore installé.</span><span class="sxs-lookup"><span data-stu-id="e3347-110">Install hello [Azure CLI 2.0](/cli/azure/install-az-cli2) if you don't already have it installed.</span></span>
2. <span data-ttu-id="e3347-111">Créer une paire de clés SSH publique et privée pour les machines virtuelles Linux en effectuant les étapes hello Bonjour [créer une paire de clés SSH publique et privée pour les machines virtuelles Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e3347-111">Create an SSH public and private key pair for Linux VMs by completing hello steps in hello [Create an SSH public and private key pair for Linux VMs](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
3. <span data-ttu-id="e3347-112">À partir d’une invite de commandes, la connexion avec la commande hello `az login`.</span><span class="sxs-lookup"><span data-stu-id="e3347-112">From a command shell, login with hello command `az login`.</span></span>
4. <span data-ttu-id="e3347-113">Créer hello machine virtuelle en exécutant le script hello qui suit sur un ordinateur Linux ou Mac.</span><span class="sxs-lookup"><span data-stu-id="e3347-113">Create hello VM by executing hello script that follows on a Linux or Mac computer.</span></span> <span data-ttu-id="e3347-114">script de Hello crée un groupe de ressources, un réseau virtuel (VNet) avec deux sous-réseaux, deux cartes réseau et une machine virtuelle avec hello deux cartes d’interface réseau attachée tooit.</span><span class="sxs-lookup"><span data-stu-id="e3347-114">hello script creates a resource group, one virtual network (VNet) with two subnets, two NICs, and a VM with hello two NICs attached tooit.</span></span> <span data-ttu-id="e3347-115">Une des cartes réseau de hello est connecté tooone sous-réseau et est affectée à une adresse IP publique et privée.</span><span class="sxs-lookup"><span data-stu-id="e3347-115">One of hello NICs is connected tooone subnet and is assigned a static public and private IP address.</span></span> <span data-ttu-id="e3347-116">Hello autre carte réseau est connectée toohello les autres sous-réseaux et reçoit une adresse IP privée statique et aucune adresse IP publique.</span><span class="sxs-lookup"><span data-stu-id="e3347-116">hello other NIC is connected toohello other subnet and is assigned a static private IP address and no public IP address.</span></span> <span data-ttu-id="e3347-117">Hello de carte réseau, adresse IP publique, réseau virtuel et ressources d’ordinateur virtuel doivent tous exister dans hello même emplacement et abonnement.</span><span class="sxs-lookup"><span data-stu-id="e3347-117">hello NIC, public IP address, virtual network, and VM resources must all exist in hello same location and subscription.</span></span> <span data-ttu-id="e3347-118">Bien que les ressources hello n’ont pas toutes tooexist Bonjour même groupe de ressources, Bonjour elles font de script suivant.</span><span class="sxs-lookup"><span data-stu-id="e3347-118">Though hello resources don't all have tooexist in hello same resource group, in hello following script they do.</span></span>

```bash
#!/bin/sh

RgName="Multi-NIC-VM"
Location="westus"

# Create a resource group.
az group create \
--name $RgName \
--location $Location

# hello address is assigned toohello resource from a pool of IP adresses unique tooeach Azure region. 
# Download and view hello file from https://www.microsoft.com/en-us/download/details.aspx?id=41653 that lists
# hello ranges for each region.

PipName="PIP-WEB"
az network public-ip create \
--name $PipName \
--resource-group $RgName \
--location $Location \
--allocation-method Static

# Create a virtual network with one subnet

VnetName="VNet1"
VnetPrefix="10.0.0.0/16"
VnetSubnet1Name="Front-End"
VnetSubnet1Prefix="10.0.0.0/24"
az network vnet create \
--name $VnetName \
--resource-group $RgName \
--location $Location \
--address-prefix $VnetPrefix \
--subnet-name $VnetSubnet1Name \
--subnet-prefix $VnetSubnet1Prefix

# Create a second subnet within hello VNet

VnetSubnet2Name="Back-end"
VnetSubnet2Prefix="10.0.1.0/24"
az network vnet subnet create \
--vnet-name $VnetName \
--resource-group $RgName \
--name $VnetSubnet2Name \
--address-prefix $VnetSubnet2Prefix

# Create a network interface connected tooone of hello subnets. hello NIC is assigned a single dynamic private and
# public IP address by default, but you can instead, assign static addresses, or no public IP address at all.
# You can also assign multiple private or public IP addresses tooeach NIC. toolearn more about IP addressing
# options for NICs, enter hello az network nic create -h command.

Nic1Name="NIC-FE"
PrivateIpAddress1="10.0.0.5"

az network nic create \
--name $Nic1Name \
--resource-group $RgName \
--location $Location \
--subnet $VnetSubnet1Name \
--vnet-name $VnetName \
--private-ip-address $PrivateIpAddress1 \
--public-ip-address $PipName

# Create a second network interface and connect it toohello other subnet. Though multiple NICs attached toohello same
# VM can be connected toodifferent subnets, hello subnets must all be within hello same VNet. Add additional NICs as necessary.

Nic2Name="NIC-BE"
PrivateIpAddress2="10.0.1.5"

az network nic create \
--name $Nic2Name \
--resource-group $RgName \
--location $Location \
--subnet $VnetSubnet2Name \
--vnet-name $VnetName \
--private-ip-address $PrivateIpAddress2

# Create a VM and attach hello two NICs.

VmName="WEB"

# Replace hello value for hello following **VmSize** variable with a value from the
# https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-sizes article. Not all VM sizes support
# more than one NIC, so be sure tooselect a VM size that supports hello number of NICs you want tooattach toohello VM.
# You must create hello VM with at least two NICs if you want tooadd more after VM creation. If you create a VM with
# only one NIC, you can't add additional NICs toohello VM after VM creation, regardless of how many NICs hello VM supports.
# hello VM size specified in hello following variable supports two NICs.

VmSize="Standard_DS2"

# Replace hello value for hello OsImage variable value with a value for *urn* from hello output returned by entering the
# az vm image list command.

OsImage="credativ:Debian:8:latest"

Username="adminuser"

# Replace hello following value with hello path tooyour public key file.

SshKeyValue="~/.ssh/id_rsa.pub"

# Before executing hello following command, add variable names of additional NICs you may have added toohello script that
# you want tooattach toohello VM. If creating a Windows VM, remove hello **ssh-key-value** line and you'll be prompted for
# hello password you want tooconfigure for hello VM.

az vm create \
--name $VmName \
--resource-group $RgName \
--image $OsImage \
--location $Location \
--size $VmSize \
--nics $Nic1Name $Nic2Name \
--admin-username $Username \
--ssh-key-value $SshKeyValue
```

<span data-ttu-id="e3347-119">En outre toocreating une machine virtuelle avec deux cartes réseau, hello script crée :</span><span class="sxs-lookup"><span data-stu-id="e3347-119">In addition toocreating a VM with two NICs, hello script creates:</span></span>
- <span data-ttu-id="e3347-120">Une prime unique géré disque par défaut, mais vous disposez d’autres options pour le type de disque hello que vous pouvez créer.</span><span class="sxs-lookup"><span data-stu-id="e3347-120">A single premium managed disk by default, but you have other options for hello disk type you can create.</span></span> <span data-ttu-id="e3347-121">Hello de lecture [créer un VM Linux à l’aide de hello Azure CLI 2.0](../virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json) article pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="e3347-121">Read hello [Create a Linux VM using hello Azure CLI 2.0](../virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json) article for details.</span></span>
- <span data-ttu-id="e3347-122">Un réseau virtuel avec deux sous-réseaux et une seule adresse IP publique.</span><span class="sxs-lookup"><span data-stu-id="e3347-122">A virtual network with two subnets and a single public IP address.</span></span> <span data-ttu-id="e3347-123">Vous pouvez également utiliser des ressources *existantes* en matière de réseau virtuel, sous-réseau, carte réseau ou adresse IP publique.</span><span class="sxs-lookup"><span data-stu-id="e3347-123">Alternatively, you can use *existing* virtual network, subnet, NIC, or public IP address resources.</span></span> <span data-ttu-id="e3347-124">toolearn comment toouse existant ressources réseau plutôt que la création de ressources supplémentaires, entrez `az vm create -h`.</span><span class="sxs-lookup"><span data-stu-id="e3347-124">toolearn how toouse existing network resources rather than creating additional resources, enter `az vm create -h`.</span></span>

## <span data-ttu-id="e3347-125"><a name = "validate"></a>Valider la création d’une machine virtuelle et de cartes réseau</span><span class="sxs-lookup"><span data-stu-id="e3347-125"><a name = "validate"></a>Validate VM creation and NICs</span></span>

1. <span data-ttu-id="e3347-126">Entrez la commande hello `az resource list --resouce-group Multi-NIC-VM --output table` toosee une liste de ressources hello créé par un script de hello.</span><span class="sxs-lookup"><span data-stu-id="e3347-126">Enter hello command `az resource list --resouce-group Multi-NIC-VM --output table` toosee a list of hello resources created by hello script.</span></span> <span data-ttu-id="e3347-127">Il doit y avoir six ressources Bonjour retourné de sortie : deux cartes réseau, un disque, une adresse IP publique, un réseau virtuel et un ordinateur virtuel.</span><span class="sxs-lookup"><span data-stu-id="e3347-127">There should be six resources in hello returned output: Two NICs, one disk, one public IP address, one virtual network, and a virtual machine.</span></span>
2. <span data-ttu-id="e3347-128">Entrez la commande hello `az network public-ip show --name PIP-WEB --resource-group Multi-NIC-VM --output table`.</span><span class="sxs-lookup"><span data-stu-id="e3347-128">Enter hello command `az network public-ip show --name PIP-WEB --resource-group Multi-NIC-VM --output table`.</span></span> <span data-ttu-id="e3347-129">Bonjour retourné de sortie, notez hello de **IpAddress** et cette valeur hello de **PublicIpAllocationMethod** est *statique*.</span><span class="sxs-lookup"><span data-stu-id="e3347-129">In hello returned output, note hello value of **IpAddress** and that hello value of **PublicIpAllocationMethod** is *Static*.</span></span>
3. <span data-ttu-id="e3347-130">Avant d’exécuter hello commande suivante, supprimez hello <>, remplacez *nom d’utilisateur* avec nom hello de hello **nom d’utilisateur** variable dans le script de hello, puis remplacez *ipAddress* avec hello **ipAddress** à partir de l’étape précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="e3347-130">Before running hello following command, remove hello <>, replace *Username* with hello name you used for hello **Username** variable in hello script, and replace *ipAddress* with hello **ipAddress** from hello previous step.</span></span> <span data-ttu-id="e3347-131">Suivante d’exécution hello commande tooconnect toohello machine virtuelle : `ssh -i ~/.ssh/azure_id_rsa <Username>@<ipAddress>`.</span><span class="sxs-lookup"><span data-stu-id="e3347-131">Run hello following command tooconnect toohello VM: `ssh -i ~/.ssh/azure_id_rsa <Username>@<ipAddress>`.</span></span> 
4. <span data-ttu-id="e3347-132">Une fois connecté toohello machine virtuelle, exécutez hello `sudo ifconfig` commande toosee *eth0* et *eth1* interfaces.</span><span class="sxs-lookup"><span data-stu-id="e3347-132">Once connected toohello VM, run hello `sudo ifconfig` command toosee *eth0* and *eth1* interfaces.</span></span> <span data-ttu-id="e3347-133">Hello privée des adresses IP statiques spécifiés dans le script de hello par les serveurs DHCP Azure hello a été attribuée à chaque carte réseau.</span><span class="sxs-lookup"><span data-stu-id="e3347-133">Each NIC has been assigned hello static private IP addresses specified in hello script by hello Azure DHCP servers.</span></span> <span data-ttu-id="e3347-134">Hello des adresses IP et MAC affectés toohello NIC ne changent pas tant que hello que machine virtuelle est supprimée.</span><span class="sxs-lookup"><span data-stu-id="e3347-134">hello IP and MAC addresses assigned toohello NICs do not change until hello VM is deleted.</span></span> <span data-ttu-id="e3347-135">Nous vous recommandons de ne pas modifier l’adressage IP dans un système d’exploitation, car il peut désactiver ordinateur toohello de connectivité.</span><span class="sxs-lookup"><span data-stu-id="e3347-135">We recommend that you do not change IP addressing within an operating system, as it can disable connectivity toohello computer.</span></span> <span data-ttu-id="e3347-136">Les adresses IP publiques n’apparaissent pas dans le système d’exploitation de hello, lorsqu’ils sont tooand adresse traduite de réseau à partir de l’adresse IP privée de hello en hello infrastructure Azure.</span><span class="sxs-lookup"><span data-stu-id="e3347-136">Public IP addresses do not appear within hello operating system, as they are network address translated tooand from hello private IP address by hello Azure infrastructure.</span></span>

## <span data-ttu-id="e3347-137"><a name= "clean-up"></a>Supprimer hello machine virtuelle et les ressources associées</span><span class="sxs-lookup"><span data-stu-id="e3347-137"><a name= "clean-up"></a>Remove hello VM and associated resources</span></span>

<span data-ttu-id="e3347-138">Il est recommandé de supprimer les ressources hello créés dans cet exercice, si vous ne les utilisez en production.</span><span class="sxs-lookup"><span data-stu-id="e3347-138">It's recommended that you delete hello resources created in this exercise if you won't use them in production.</span></span> <span data-ttu-id="e3347-139">La machine virtuelle, l’adresse IP publique et le disque occasionnent des frais tant que ces ressources sont configurées.</span><span class="sxs-lookup"><span data-stu-id="e3347-139">VM, public IP address, and disk resources incur charges, as long as they're provisioned.</span></span> <span data-ttu-id="e3347-140">ressources de hello tooremove créés au cours de cet exercice, hello complète comme suit :</span><span class="sxs-lookup"><span data-stu-id="e3347-140">tooremove hello resources created during this exercise, complete hello following steps:</span></span>
1. <span data-ttu-id="e3347-141">tooview hello ressources hello groupe de ressources, exécutez hello `az resource list --resource-group Multi-NIC-VM` commande.</span><span class="sxs-lookup"><span data-stu-id="e3347-141">tooview hello resources in hello resource group, run hello `az resource list --resource-group Multi-NIC-VM` command.</span></span>
2. <span data-ttu-id="e3347-142">Ne vérifiez qu’aucune ressource dans le groupe de ressources hello, autres que les ressources hello créées par script hello dans cet article.</span><span class="sxs-lookup"><span data-stu-id="e3347-142">Confirm there are no resources in hello resource group, other than hello resources created by hello script in this article.</span></span> 
3. <span data-ttu-id="e3347-143">toodelete toutes les ressources créées dans cet exercice, exécutez hello `az group delete --name Multi-NIC-VM` commande.</span><span class="sxs-lookup"><span data-stu-id="e3347-143">toodelete all resources created in this exercise, run hello `az group delete --name Multi-NIC-VM` command.</span></span> <span data-ttu-id="e3347-144">commande Hello supprime le groupe de ressources hello et toutes les ressources hello qu’il contient.</span><span class="sxs-lookup"><span data-stu-id="e3347-144">hello command deletes hello resource group and all hello resources it contains.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e3347-145">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e3347-145">Next steps</span></span>

<span data-ttu-id="e3347-146">Tout le trafic réseau peut circuler tooand de hello que machine virtuelle créée dans cet article.</span><span class="sxs-lookup"><span data-stu-id="e3347-146">Any network traffic can flow tooand from hello VM created in this article.</span></span> <span data-ttu-id="e3347-147">Vous pouvez définir des règles entrantes et sortantes au sein d’un groupe de sécurité réseau qui limitent le trafic hello qui peut circuler tooand à partir de chaque interface réseau, chaque sous-réseau ou les deux.</span><span class="sxs-lookup"><span data-stu-id="e3347-147">You can define inbound and outbound rules within an NSG that limit hello traffic that can flow tooand from each network interface, each subnet, or both.</span></span> <span data-ttu-id="e3347-148">toolearn plus d’informations sur les groupes de sécurité réseau, lire hello [vue d’ensemble du groupe de sécurité réseau](virtual-networks-nsg.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="e3347-148">toolearn more about NSGs, read hello [NSG overview](virtual-networks-nsg.md) article.</span></span>
