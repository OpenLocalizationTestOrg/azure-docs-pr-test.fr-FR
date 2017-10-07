---
title: aaaCreate une machine virtuelle avec une adresse IP publique statique - Azure CLI 2.0 | Documents Microsoft
description: "Découvrez comment toocreate une machine virtuelle avec un statique publique adresse IP via hello Azure interface de ligne de commande (CLI) 2.0."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 55bc21b0-2a45-4943-a5e7-8d785d0d015c
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 486060463486462dd8336734a7ad23c4a2cba452
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-a-static-public-ip-address-using-hello-azure-cli-20"></a><span data-ttu-id="af811-103">Créer une machine virtuelle avec une adresse IP publique statique à l’aide de hello Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="af811-103">Create a VM with a static public IP address using hello Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="af811-104">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="af811-104">Azure portal</span></span>](virtual-network-deploy-static-pip-arm-portal.md)
> * [<span data-ttu-id="af811-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="af811-105">PowerShell</span></span>](virtual-network-deploy-static-pip-arm-ps.md)
> * [<span data-ttu-id="af811-106">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="af811-106">Azure CLI 2.0</span></span>](virtual-network-deploy-static-pip-arm-cli.md)
> * [<span data-ttu-id="af811-107">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="af811-107">Azure CLI 1.0</span></span>](virtual-network-deploy-static-pip-cli-nodejs.md)
> * [<span data-ttu-id="af811-108">Modèle</span><span class="sxs-lookup"><span data-stu-id="af811-108">Template</span></span>](virtual-network-deploy-static-pip-arm-template.md)
> * [<span data-ttu-id="af811-109">PowerShell (classique)</span><span class="sxs-lookup"><span data-stu-id="af811-109">PowerShell (Classic)</span></span>](virtual-networks-reserved-public-ip.md)

[!INCLUDE [virtual-network-deploy-static-pip-intro-include.md](../../includes/virtual-network-deploy-static-pip-intro-include.md)]

<span data-ttu-id="af811-110">Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [Resource Manager et classique](../resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="af811-110">Azure has two different deployment models for creating and working with resources: [Resource Manager and classic](../resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span> <span data-ttu-id="af811-111">Cet article décrit à l’aide du modèle de déploiement Resource Manager hello, qui recommandées par Microsoft pour la plupart des déploiements de nouveau au lieu du modèle de déploiement classique hello.</span><span class="sxs-lookup"><span data-stu-id="af811-111">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello classic deployment model.</span></span>

[!INCLUDE [virtual-network-deploy-static-pip-scenario-include.md](../../includes/virtual-network-deploy-static-pip-scenario-include.md)]

## <span data-ttu-id="af811-112"><a name = "create"></a>Créer hello machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="af811-112"><a name = "create"></a>Create hello VM</span></span>

<span data-ttu-id="af811-113">Vous pouvez effectuer cette tâche à l’aide de hello Azure CLI 2.0 (cet article) ou hello [Azure CLI 1.0](virtual-network-deploy-static-pip-cli-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="af811-113">You can complete this task using hello Azure CLI 2.0 (this article) or hello [Azure CLI 1.0](virtual-network-deploy-static-pip-cli-nodejs.md).</span></span> <span data-ttu-id="af811-114">Hello dans les valeurs « » pour les variables hello dans les étapes de hello qui suivent créer des ressources avec les paramètres d’un scénario de hello.</span><span class="sxs-lookup"><span data-stu-id="af811-114">hello values in "" for hello variables in hello steps that follow create resources with settings from hello scenario.</span></span> <span data-ttu-id="af811-115">Modifier les valeurs hello, comme il convient pour votre environnement.</span><span class="sxs-lookup"><span data-stu-id="af811-115">Change hello values, as appropriate, for your environment.</span></span>

1. <span data-ttu-id="af811-116">Installer hello [Azure CLI 2.0](/cli/azure/install-az-cli2) si vous n’en avez pas encore installé.</span><span class="sxs-lookup"><span data-stu-id="af811-116">Install hello [Azure CLI 2.0](/cli/azure/install-az-cli2) if you don't already have it installed.</span></span>
2. <span data-ttu-id="af811-117">Créer une paire de clés SSH publique et privée pour les machines virtuelles Linux en effectuant les étapes hello Bonjour [créer une paire de clés SSH publique et privée pour les machines virtuelles Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="af811-117">Create an SSH public and private key pair for Linux VMs by completing hello steps in hello [Create an SSH public and private key pair for Linux VMs](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
3. <span data-ttu-id="af811-118">À partir d’une invite de commandes, la connexion avec la commande hello `az login`.</span><span class="sxs-lookup"><span data-stu-id="af811-118">From a command shell, login with hello command `az login`.</span></span>
4. <span data-ttu-id="af811-119">Créer hello machine virtuelle en exécutant le script hello qui suit sur un ordinateur Linux ou Mac.</span><span class="sxs-lookup"><span data-stu-id="af811-119">Create hello VM by executing hello script that follows on a Linux or Mac computer.</span></span> <span data-ttu-id="af811-120">Hello Azure adresse IP publique, de réseau virtuel, d’interface réseau et ressources d’ordinateur virtuel doivent tous exister dans hello même emplacement.</span><span class="sxs-lookup"><span data-stu-id="af811-120">hello Azure public IP address, virtual network, network interface, and VM resources must all exist in hello same location.</span></span> <span data-ttu-id="af811-121">Bien que les ressources hello n’ont pas toutes tooexist Bonjour même groupe de ressources, Bonjour elles font de script suivant.</span><span class="sxs-lookup"><span data-stu-id="af811-121">Though hello resources don't all have tooexist in hello same resource group, in hello following script they do.</span></span>

```bash
RgName="IaaSStory"
Location="westus"

# Create a resource group.

az group create \
--name $RgName \
--location $Location

# Create a public IP address resource with a static IP address using hello --allocation-method Static option.
# If you do not specify this option, hello address is allocated dynamically. hello address is assigned toothe
# resource from a pool of IP adresses unique tooeach Azure region. hello DnsName must be unique within the
# Azure location it's created in. Download and view hello file from https://www.microsoft.com/en-us/download/details.aspx?id=41653#
# that lists hello ranges for each region.

PipName="PIPWEB1"
DnsName="iaasstoryws1"
az network public-ip create \
--name $PipName \
--resource-group $RgName \
--location $Location \
--allocation-method Static \
--dns-name $DnsName

# Create a virtual network with one subnet

VnetName="TestVNet"
VnetPrefix="192.168.0.0/16"
SubnetName="FrontEnd"
SubnetPrefix="192.168.1.0/24"
az network vnet create \
--name $VnetName \
--resource-group $RgName \
--location $Location \
--address-prefix $VnetPrefix \
--subnet-name $SubnetName \
--subnet-prefix $SubnetPrefix

# Create a network interface connected toohello VNet with a static private IP address and associate hello public IP address
# resource toohello NIC.

NicName="NICWEB1"
PrivateIpAddress="192.168.1.101"
az network nic create \
--name $NicName \
--resource-group $RgName \
--location $Location \
--subnet $SubnetName \
--vnet-name $VnetName \
--private-ip-address $PrivateIpAddress \
--public-ip-address $PipName

# Create a new VM with hello NIC

VmName="WEB1"

# Replace hello value for hello VmSize variable with a value from the
# https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-sizes article.
VmSize="Standard_DS1"

# Replace hello value for hello OsImage variable with a value for *urn* from hello output returned by entering
# hello `az vm image list` command. 

OsImage="credativ:Debian:8:latest"
Username='adminuser'

# Replace hello following value with hello path tooyour public key file.
SshKeyValue="~/.ssh/id_rsa.pub"

az vm create \
--name $VmName \
--resource-group $RgName \
--image $OsImage \
--location $Location \
--size $VmSize \
--nics $NicName \
--admin-username $Username \
--ssh-key-value $SshKeyValue
# If creating a Windows VM, remove hello previous line and you'll be prompted for hello password you want tooconfigure for hello VM.
```

<span data-ttu-id="af811-122">En outre toocreating une machine virtuelle, hello script crée :</span><span class="sxs-lookup"><span data-stu-id="af811-122">In addition toocreating a VM, hello script creates:</span></span>
- <span data-ttu-id="af811-123">Une prime unique géré disque par défaut, mais vous disposez d’autres options pour le type de disque hello que vous pouvez créer.</span><span class="sxs-lookup"><span data-stu-id="af811-123">A single premium managed disk by default, but you have other options for hello disk type you can create.</span></span> <span data-ttu-id="af811-124">Hello de lecture [créer un VM Linux à l’aide de hello Azure CLI 2.0](../virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json) article pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="af811-124">Read hello [Create a Linux VM using hello Azure CLI 2.0](../virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json) article for details.</span></span>
- <span data-ttu-id="af811-125">Des ressources de réseau virtuel, de sous-réseau, de carte réseau et d’adresse IP publique.</span><span class="sxs-lookup"><span data-stu-id="af811-125">Virtual network, subnet, NIC, and public IP address resources.</span></span> <span data-ttu-id="af811-126">Vous pouvez également utiliser des ressources *existantes* en matière de réseau virtuel, sous-réseau, carte réseau ou adresse IP publique.</span><span class="sxs-lookup"><span data-stu-id="af811-126">Alternatively, you can use *existing* virtual network, subnet, NIC, or public IP address resources.</span></span> <span data-ttu-id="af811-127">toolearn comment toouse existant ressources réseau plutôt que la création de ressources supplémentaires, entrez `az vm create -h`.</span><span class="sxs-lookup"><span data-stu-id="af811-127">toolearn how toouse existing network resources rather than creating additional resources, enter `az vm create -h`.</span></span>

## <span data-ttu-id="af811-128"><a name = "validate"></a>Valider la création de la machine virtuelle et l’adresse IP publique</span><span class="sxs-lookup"><span data-stu-id="af811-128"><a name = "validate"></a>Validate VM creation and public IP address</span></span>

1. <span data-ttu-id="af811-129">Entrez la commande hello `az resource list --resouce-group IaaSStory --output table` toosee une liste de ressources hello créé par un script de hello.</span><span class="sxs-lookup"><span data-stu-id="af811-129">Enter hello command `az resource list --resouce-group IaaSStory --output table` toosee a list of hello resources created by hello script.</span></span> <span data-ttu-id="af811-130">Il doit y avoir cinq ressources Bonjour retourné de sortie : réseau interface, disque, adresse IP publique, réseau virtuel et un ordinateur virtuel.</span><span class="sxs-lookup"><span data-stu-id="af811-130">There should be five resources in hello returned output: network interface, disk, public IP address, virtual network, and a virtual machine.</span></span>
2. <span data-ttu-id="af811-131">Entrez la commande hello `az network public-ip show --name PIPWEB1 --resource-group IaaSStory --output table`.</span><span class="sxs-lookup"><span data-stu-id="af811-131">Enter hello command `az network public-ip show --name PIPWEB1 --resource-group IaaSStory --output table`.</span></span> <span data-ttu-id="af811-132">Bonjour retourné de sortie, notez hello de **IpAddress** et cette valeur hello de **PublicIpAllocationMethod** est *statique*.</span><span class="sxs-lookup"><span data-stu-id="af811-132">In hello returned output, note hello value of **IpAddress** and that hello value of **PublicIpAllocationMethod** is *Static*.</span></span>
3. <span data-ttu-id="af811-133">Avant d’exécuter hello commande suivante, supprimez hello <>, remplacez *nom d’utilisateur* avec nom hello de hello **nom d’utilisateur** variable dans le script de hello, puis remplacez *ipAddress* avec hello **ipAddress** à partir de l’étape précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="af811-133">Before executing hello following command, remove hello <>, replace *Username* with hello name you used for hello **Username** variable in hello script, and replace *ipAddress* with hello **ipAddress** from hello previous step.</span></span> <span data-ttu-id="af811-134">Suivante d’exécution hello commande tooconnect toohello machine virtuelle : `ssh -i ~/.ssh/azure_id_rsa <Username>@<ipAddress>`.</span><span class="sxs-lookup"><span data-stu-id="af811-134">Run hello following command tooconnect toohello VM: `ssh -i ~/.ssh/azure_id_rsa <Username>@<ipAddress>`.</span></span> 

## <span data-ttu-id="af811-135"><a name= "clean-up"></a>Supprimer hello machine virtuelle et les ressources associées</span><span class="sxs-lookup"><span data-stu-id="af811-135"><a name= "clean-up"></a>Remove hello VM and associated resources</span></span>

<span data-ttu-id="af811-136">Il est recommandé de supprimer les ressources hello créés dans cet exercice, si vous ne les utilisez en production.</span><span class="sxs-lookup"><span data-stu-id="af811-136">It's recommended that you delete hello resources created in this exercise if you won't use them in production.</span></span> <span data-ttu-id="af811-137">La machine virtuelle, l’adresse IP publique et le disque occasionnent des frais tant que ces ressources sont configurées.</span><span class="sxs-lookup"><span data-stu-id="af811-137">VM, public IP address, and disk resources incur charges, as long as they're provisioned.</span></span> <span data-ttu-id="af811-138">ressources de hello tooremove créés au cours de cet exercice, hello complète comme suit :</span><span class="sxs-lookup"><span data-stu-id="af811-138">tooremove hello resources created during this exercise, complete hello following steps:</span></span>

1. <span data-ttu-id="af811-139">tooview hello ressources hello groupe de ressources, exécutez hello `az resource list --resource-group IaaSStory` commande.</span><span class="sxs-lookup"><span data-stu-id="af811-139">tooview hello resources in hello resource group, run hello `az resource list --resource-group IaaSStory` command.</span></span>
2. <span data-ttu-id="af811-140">Ne vérifiez qu’aucune ressource dans le groupe de ressources hello, autres que les ressources hello créées par script hello dans cet article.</span><span class="sxs-lookup"><span data-stu-id="af811-140">Confirm there are no resources in hello resource group, other than hello resources created by hello script in this article.</span></span> 
3. <span data-ttu-id="af811-141">toodelete toutes les ressources créées dans cet exercice, exécutez hello `az group delete -n IaaSStory` commande.</span><span class="sxs-lookup"><span data-stu-id="af811-141">toodelete all resources created in this exercise, run hello `az group delete -n IaaSStory` command.</span></span> <span data-ttu-id="af811-142">commande Hello supprime le groupe de ressources hello et toutes les ressources hello qu’il contient.</span><span class="sxs-lookup"><span data-stu-id="af811-142">hello command deletes hello resource group and all hello resources it contains.</span></span>

## <a name="next-steps"></a><span data-ttu-id="af811-143">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="af811-143">Next steps</span></span>

<span data-ttu-id="af811-144">Tout le trafic réseau peut circuler tooand de hello que machine virtuelle créée dans cet article.</span><span class="sxs-lookup"><span data-stu-id="af811-144">Any network traffic can flow tooand from hello VM created in this article.</span></span> <span data-ttu-id="af811-145">Vous pouvez définir des règles entrantes et sortantes au sein d’un groupe de sécurité réseau qui limitent le trafic hello qui peut circuler tooand d’interface réseau de hello, le sous-réseau de hello ou les deux.</span><span class="sxs-lookup"><span data-stu-id="af811-145">You can define inbound and outbound rules within an NSG that limit hello traffic that can flow tooand from hello network interface, hello subnet, or both.</span></span> <span data-ttu-id="af811-146">toolearn plus d’informations sur les groupes de sécurité réseau, lire hello [vue d’ensemble du groupe de sécurité réseau](virtual-networks-nsg.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="af811-146">toolearn more about NSGs, read hello [NSG overview](virtual-networks-nsg.md) article.</span></span>
