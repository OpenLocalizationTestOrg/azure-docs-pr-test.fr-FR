---
title: "aaaVM avec plusieurs adresses IP à l’aide de hello Azure CLI 2.0 | Documents Microsoft"
description: "Découvrez comment tooassign des adresses IP multiples à l’aide de machine virtuelle tooa hello Azure CLI 2.0 | Gestionnaire de ressources."
services: virtual-network
documentationcenter: na
author: anavinahar
manager: narayan
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/17/2016
ms.author: annahar
ms.openlocfilehash: 15efd853cc7c31bacb64ed052dabedd3fe4d3079
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="assign-multiple-ip-addresses-toovirtual-machines-using-hello-azure-cli-20"></a><span data-ttu-id="e8974-103">Affecter des ordinateurs toovirtual hello Azure CLI 2.0 à l’aide de plusieurs adresses IP</span><span class="sxs-lookup"><span data-stu-id="e8974-103">Assign multiple IP addresses toovirtual machines using hello Azure CLI 2.0</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-intro.md](../../includes/virtual-network-multiple-ip-addresses-intro.md)]

<span data-ttu-id="e8974-104">Cet article explique comment toocreate un ordinateur virtuel (VM) l’utilisation de modèle de déploiement Azure Resource Manager hello hello Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="e8974-104">This article explains how toocreate a virtual machine (VM) through hello Azure Resource Manager deployment model using hello Azure CLI 2.0.</span></span> <span data-ttu-id="e8974-105">Tooresources créé via le modèle de déploiement classique hello ne peut pas être assignés à plusieurs adresses IP.</span><span class="sxs-lookup"><span data-stu-id="e8974-105">Multiple IP addresses cannot be assigned tooresources created through hello classic deployment model.</span></span> <span data-ttu-id="e8974-106">toolearn plus d’informations sur les modèles de déploiement Azure, lisez hello [comprendre les modèles de déploiement](../resource-manager-deployment-model.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="e8974-106">toolearn more about Azure deployment models, read hello [Understand deployment models](../resource-manager-deployment-model.md) article.</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-template-scenario.md](../../includes/virtual-network-multiple-ip-addresses-scenario.md)]

## <span data-ttu-id="e8974-107"><a name = "create"></a>Créer une machine virtuelle avec plusieurs adresses IP</span><span class="sxs-lookup"><span data-stu-id="e8974-107"><a name = "create"></a>Create a VM with multiple IP addresses</span></span>

<span data-ttu-id="e8974-108">Vous pouvez effectuer cette tâche à l’aide de hello Azure CLI 2.0 (cet article) ou hello [Azure CLI 1.0](virtual-network-multiple-ip-addresses-cli-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="e8974-108">You can complete this task using hello Azure CLI 2.0 (this article) or hello [Azure CLI 1.0](virtual-network-multiple-ip-addresses-cli-nodejs.md).</span></span> <span data-ttu-id="e8974-109">Modifier les valeurs hello, comme il convient pour votre environnement.</span><span class="sxs-lookup"><span data-stu-id="e8974-109">Change hello values, as appropriate, for your environment.</span></span> <span data-ttu-id="e8974-110">Hello étapes qui suivent expliquent comment toocreate un exemple de machine virtuelle avec plusieurs IP, les adresses, comme décrit dans le scénario de hello.</span><span class="sxs-lookup"><span data-stu-id="e8974-110">hello steps that follow explain how toocreate an example VM with multiple IP addresses, as described in hello scenario.</span></span> <span data-ttu-id="e8974-111">Modifiez les valeurs des variables entre symboles "" et les types d’adresses IP en fonction des besoins de votre implémentation.</span><span class="sxs-lookup"><span data-stu-id="e8974-111">Change variable values in "" and IP address types as required for your implementation.</span></span> 

1. <span data-ttu-id="e8974-112">Installer hello [Azure CLI 2.0](/cli/azure/install-az-cli2) si vous n’en avez pas encore installé.</span><span class="sxs-lookup"><span data-stu-id="e8974-112">Install hello [Azure CLI 2.0](/cli/azure/install-az-cli2) if you don't already have it installed.</span></span>
2. <span data-ttu-id="e8974-113">Créer une paire de clés SSH publique et privée pour les machines virtuelles Linux en effectuant les étapes hello Bonjour [créer une paire de clés SSH publique et privée pour les machines virtuelles Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e8974-113">Create an SSH public and private key pair for Linux VMs by completing hello steps in hello [Create an SSH public and private key pair for Linux VMs](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
3. <span data-ttu-id="e8974-114">À partir d’une invite de commandes, la connexion avec la commande hello `az login` et sélectionnez l’abonnement hello vous utilisez.</span><span class="sxs-lookup"><span data-stu-id="e8974-114">From a command shell, login with hello command `az login` and select hello subscription you're using.</span></span>
4. <span data-ttu-id="e8974-115">Créer hello machine virtuelle en exécutant le script hello qui suit sur un ordinateur Linux ou Mac.</span><span class="sxs-lookup"><span data-stu-id="e8974-115">Create hello VM by executing hello script that follows on a Linux or Mac computer.</span></span> <span data-ttu-id="e8974-116">script de Hello crée un groupe de ressources, un réseau virtuel (VNet), une carte réseau avec trois configurations IP et une machine virtuelle avec hello deux cartes réseau attaché tooit.</span><span class="sxs-lookup"><span data-stu-id="e8974-116">hello script creates a resource group, one virtual network (VNet), one NIC with three IP configurations, and a VM with hello two NICs attached tooit.</span></span> <span data-ttu-id="e8974-117">Hello de carte réseau, adresse IP publique, réseau virtuel et ressources d’ordinateur virtuel doivent tous exister dans hello même emplacement et abonnement.</span><span class="sxs-lookup"><span data-stu-id="e8974-117">hello NIC, public IP address, virtual network, and VM resources must all exist in hello same location and subscription.</span></span> <span data-ttu-id="e8974-118">Bien que les ressources hello n’ont pas toutes tooexist Bonjour même groupe de ressources, Bonjour elles font de script suivant.</span><span class="sxs-lookup"><span data-stu-id="e8974-118">Though hello resources don't all have tooexist in hello same resource group, in hello following script they do.</span></span>

```bash
    
#!/bin/sh
    
RgName="myResourceGroup"
Location="westcentralus"
az group create --name $RgName --location $Location
    
# Create a public IP address resource with a static IP address using hello `--allocation-method Static` option. If you
# do not specify this option, hello address is allocated dynamically. hello address is assigned toohello resource from a pool
# of IP adresses unique tooeach Azure region. Download and view hello file from
# https://www.microsoft.com/en-us/download/details.aspx?id=41653 that lists hello ranges for each region.

PipName="myPublicIP"

# This name must be unique within an Azure location.
DnsName="myDNSName"

az network public-ip create \
--name $PipName \
--resource-group $RgName \
--location $Location \
--dns-name $DnsName\
--allocation-method Static

# Create a virtual network with one subnet

VnetName="myVnet"
VnetPrefix="10.0.0.0/16"
VnetSubnetName="mySubnet"
VnetSubnetPrefix="10.0.0.0/24"

az network vnet create \
--name $VnetName \
--resource-group $RgName \
--location $Location \
--address-prefix $VnetPrefix \
--subnet-name $VnetSubnetName \
--subnet-prefix $VnetSubnetPrefix

# Create a network interface connected toohello subnet and associate hello public IP address tooit. Azure will create the
# first IP configuration with a static private IP address and will associate hello public IP address resource tooit.

NicName="MyNic1"
az network nic create \
--name $NicName \
--resource-group $RgName \
--location $Location \
--subnet $VnetSubnet1Name \
--private-ip-address 10.0.0.4
--vnet-name $VnetName \
--public-ip-address $PipName
    
# Create a second public IP address, a second IP configuration, and associate it toohello NIC. This configuration has a
# static public IP address and a static private IP address.

az network public-ip create \
--resource-group $RgName \
--location $Location \
--name myPublicIP2 \
--dns-name mypublicdns2 \
--allocation-method Static

az network nic ip-config create \
--resource-group $RgName \
--nic-name $NicName \
--name IPConfig-2 \
--private-ip-address 10.0.0.5 \
--public-ip-name myPublicIP2

# Create a third IP configuration, and associate it toohello NIC. This configuration has  static private IP address and # no public IP address.

azure network nic ip-config create \
--resource-group $RgName \
--nic-name $NicName \
--private-ip-address 10.0.0.6 \
--name IPConfig-3

# Note: Though this article assigns all IP configurations tooa single NIC, you can also assign multiple IP configurations
# tooany NIC in a VM. toolearn how toocreate a VM with multiple NICs, read hello Create a VM with multiple NICs 
# article: https://docs.microsoft.com/azure/virtual-network/virtual-network-deploy-multinic-arm-cli.

# Create a VM and attach hello NIC.

VmName="myVm"

# Replace hello value for hello following **VmSize** variable with a value from the
# https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-sizes rticle. hello script fails if hello VM size
# is not supported in hello location you select. Run hello `azure vm sizes --location estcentralus` command tooget a full list
# of VMs in US West Central, for example.

VmSize="Standard_DS1"

# Replace hello value for hello OsImage variable value with a value for *urn* from hello utput returned by entering the
# `az vm image list` command.

OsImage="credativ:Debian:8:latest"

Username="adminuser"

# Replace hello following value with hello path tooyour public key file. If you're creating a Windows VM, remove hello following
# line and you'll be prompted for hello password you want tooconfigure for hello VM.

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
```

<span data-ttu-id="e8974-119">En outre toocreating une machine virtuelle avec une carte réseau avec des configurations IP 3, hello script crée :</span><span class="sxs-lookup"><span data-stu-id="e8974-119">In addition toocreating a VM with a NIC with 3 IP configurations, hello script creates:</span></span>

- <span data-ttu-id="e8974-120">Une prime unique géré disque par défaut, mais vous disposez d’autres options pour le type de disque hello que vous pouvez créer.</span><span class="sxs-lookup"><span data-stu-id="e8974-120">A single premium managed disk by default, but you have other options for hello disk type you can create.</span></span> <span data-ttu-id="e8974-121">Hello de lecture [créer un VM Linux à l’aide de hello Azure CLI 2.0](../virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json) article pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="e8974-121">Read hello [Create a Linux VM using hello Azure CLI 2.0](../virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json) article for details.</span></span>
- <span data-ttu-id="e8974-122">Un réseau virtuel avec un sous-réseau et deux adresses IP publiques.</span><span class="sxs-lookup"><span data-stu-id="e8974-122">A virtual network with one subnet and two public IP addresses.</span></span> <span data-ttu-id="e8974-123">Vous pouvez également utiliser des ressources *existantes* en matière de réseau virtuel, sous-réseau, carte réseau ou adresse IP publique.</span><span class="sxs-lookup"><span data-stu-id="e8974-123">Alternatively, you can use *existing* virtual network, subnet, NIC, or public IP address resources.</span></span> <span data-ttu-id="e8974-124">toolearn comment toouse existant ressources réseau plutôt que la création de ressources supplémentaires, entrez `az vm create -h`.</span><span class="sxs-lookup"><span data-stu-id="e8974-124">toolearn how toouse existing network resources rather than creating additional resources, enter `az vm create -h`.</span></span>

<span data-ttu-id="e8974-125">Les adresses IP publiques ont un coût nominal.</span><span class="sxs-lookup"><span data-stu-id="e8974-125">Public IP addresses have a nominal fee.</span></span> <span data-ttu-id="e8974-126">toolearn en savoir plus sur le protocole IP adresse tarification, lire hello [tarification d’adresse IP](https://azure.microsoft.com/pricing/details/ip-addresses) page.</span><span class="sxs-lookup"><span data-stu-id="e8974-126">toolearn more about IP address pricing, read hello [IP address pricing](https://azure.microsoft.com/pricing/details/ip-addresses) page.</span></span> <span data-ttu-id="e8974-127">Il existe un toohello limiter le nombre d’adresses IP publiques qui peut être utilisé dans un abonnement.</span><span class="sxs-lookup"><span data-stu-id="e8974-127">There is a limit toohello number of public IP addresses that can be used in a subscription.</span></span> <span data-ttu-id="e8974-128">toolearn plus d’informations sur les limites de hello, lire hello [Azure limite](../azure-subscription-service-limits.md#networking-limits) l’article.</span><span class="sxs-lookup"><span data-stu-id="e8974-128">toolearn more about hello limits, read hello [Azure limits](../azure-subscription-service-limits.md#networking-limits) article.</span></span>

<span data-ttu-id="e8974-129">Après la création de hello machine virtuelle, entrez hello `az network nic show --name MyNic1 --resource-group myResourceGroup` configuration de carte réseau de commande tooview hello.</span><span class="sxs-lookup"><span data-stu-id="e8974-129">After hello VM is created, enter hello `az network nic show --name MyNic1 --resource-group myResourceGroup` command tooview hello NIC configuration.</span></span> <span data-ttu-id="e8974-130">Entrez hello `az network nic ip-config list --nic-name MyNic1 --resource-group myResourceGroup --output table` tooview une liste des configurations IP de hello associés toohello carte</span><span class="sxs-lookup"><span data-stu-id="e8974-130">Enter hello `az network nic ip-config list --nic-name MyNic1 --resource-group myResourceGroup --output table` tooview a list of hello IP configurations associated toohello NIC.</span></span>

<span data-ttu-id="e8974-131">Système d’exploitation de l’ordinateur virtuel toohello les adresses IP privée de hello ajouter en procédant comme hello pour votre système d’exploitation Bonjour [ajouter une adresse IP traite le système d’exploitation de l’ordinateur virtuel tooa](#os-config) section de cet article.</span><span class="sxs-lookup"><span data-stu-id="e8974-131">Add hello private IP addresses toohello VM operating system by completing hello steps for your operating system in hello [Add IP addresses tooa VM operating system](#os-config) section of this article.</span></span>

## <span data-ttu-id="e8974-132"><a name="add"></a>Ajouter tooa d’adresses IP virtuelle</span><span class="sxs-lookup"><span data-stu-id="e8974-132"><a name="add"></a>Add IP addresses tooa VM</span></span>

<span data-ttu-id="e8974-133">Vous pouvez ajouter plus privé et public IP adresses tooan existant de carte réseau en effectuant les étapes hello qui suivent.</span><span class="sxs-lookup"><span data-stu-id="e8974-133">You can add additional private and public IP addresses tooan existing NIC by completing hello steps that follow.</span></span> <span data-ttu-id="e8974-134">les exemples Hello reposent sur hello [scénario](#Scenario) décrit dans cet article.</span><span class="sxs-lookup"><span data-stu-id="e8974-134">hello examples build upon hello [scenario](#Scenario) described in this article.</span></span>

1. <span data-ttu-id="e8974-135">Ouvrez une invite de commandes et complète hello restant étapes de cette section dans une session unique.</span><span class="sxs-lookup"><span data-stu-id="e8974-135">Open a command shell and complete hello remaining steps in this section within a single session.</span></span> <span data-ttu-id="e8974-136">Si vous n’avez pas encore installé et configuré CLI d’Azure, hello terminé les étapes Bonjour [Azure CLI 2.0 installation](/cli/azure/install-az-cli2?toc=%2fazure%2fvirtual-network%2ftoc.json) tooyour de connexion et de l’article compte Azure avec hello `az-login` commande.</span><span class="sxs-lookup"><span data-stu-id="e8974-136">If you don't already have Azure CLI installed and configured, complete hello steps in hello [Azure CLI 2.0 installation](/cli/azure/install-az-cli2?toc=%2fazure%2fvirtual-network%2ftoc.json) article and login tooyour Azure account with hello `az-login` command.</span></span>

2. <span data-ttu-id="e8974-137">Suivez les étapes de hello dans un des hello les sections, en fonction de vos exigences suivantes :</span><span class="sxs-lookup"><span data-stu-id="e8974-137">Complete hello steps in one of hello following sections, based on your requirements:</span></span>

    <span data-ttu-id="e8974-138">**Ajouter une adresse IP privée**</span><span class="sxs-lookup"><span data-stu-id="e8974-138">**Add a private IP address**</span></span>
    
    <span data-ttu-id="e8974-139">tooadd un tooa d’adresse IP privée carte réseau, vous devez créer une configuration IP à l’aide de la commande hello qui suit.</span><span class="sxs-lookup"><span data-stu-id="e8974-139">tooadd a private IP address tooa NIC, you must create an IP configuration using hello command that follows.</span></span> <span data-ttu-id="e8974-140">adresse IP statique de Hello doit être une adresse non utilisée pour le sous-réseau de hello.</span><span class="sxs-lookup"><span data-stu-id="e8974-140">hello static IP address must be an unused address for hello subnet.</span></span>

    ```bash
    az network nic ip-config create \
    --resource-group myResourceGroup \
    --nic-name myNic1 \
    --private-ip-address 10.0.0.7 \
    --name IPConfig-4
    ```
    
    <span data-ttu-id="e8974-141">Créez autant de configurations que nécessaire, à l’aide de noms de configuration unique et d’adresses IP privées (pour les configurations avec des adresses IP statiques).</span><span class="sxs-lookup"><span data-stu-id="e8974-141">Create as many configurations as you require, using unique configuration names and private IP addresses (for configurations with static IP addresses).</span></span>

    <span data-ttu-id="e8974-142">**Ajouter une adresse IP publique**</span><span class="sxs-lookup"><span data-stu-id="e8974-142">**Add a public IP address**</span></span>
    
    <span data-ttu-id="e8974-143">Une adresse IP publique est ajoutée en l’associant tooeither une nouvelle configuration IP ou une configuration IP existante.</span><span class="sxs-lookup"><span data-stu-id="e8974-143">A public IP address is added by associating it tooeither a new IP configuration or an existing IP configuration.</span></span> <span data-ttu-id="e8974-144">Effectuez les étapes de hello dans une des sections hello qui suivent, dont vous avez besoin.</span><span class="sxs-lookup"><span data-stu-id="e8974-144">Complete hello steps in one of hello sections that follow, as you require.</span></span>

    <span data-ttu-id="e8974-145">Les adresses IP publiques ont un coût nominal.</span><span class="sxs-lookup"><span data-stu-id="e8974-145">Public IP addresses have a nominal fee.</span></span> <span data-ttu-id="e8974-146">toolearn en savoir plus sur le protocole IP adresse tarification, lire hello [tarification d’adresse IP](https://azure.microsoft.com/pricing/details/ip-addresses) page.</span><span class="sxs-lookup"><span data-stu-id="e8974-146">toolearn more about IP address pricing, read hello [IP address pricing](https://azure.microsoft.com/pricing/details/ip-addresses) page.</span></span> <span data-ttu-id="e8974-147">Il existe un toohello limiter le nombre d’adresses IP publiques qui peut être utilisé dans un abonnement.</span><span class="sxs-lookup"><span data-stu-id="e8974-147">There is a limit toohello number of public IP addresses that can be used in a subscription.</span></span> <span data-ttu-id="e8974-148">toolearn plus d’informations sur les limites de hello, lire hello [Azure limite](../azure-subscription-service-limits.md#networking-limits) l’article.</span><span class="sxs-lookup"><span data-stu-id="e8974-148">toolearn more about hello limits, read hello [Azure limits](../azure-subscription-service-limits.md#networking-limits) article.</span></span>

    - <span data-ttu-id="e8974-149">**Associer hello ressource tooa nouvelle configuration IP**</span><span class="sxs-lookup"><span data-stu-id="e8974-149">**Associate hello resource tooa new IP configuration**</span></span>
    
        <span data-ttu-id="e8974-150">Lorsque vous ajoutez une adresse IP publique dans une nouvelle configuration IP, vous devez également ajouter une adresse IP privée, car toutes les configurations IP doivent avoir une adresse IP privée.</span><span class="sxs-lookup"><span data-stu-id="e8974-150">Whenever you add a public IP address in a new IP configuration, you must also add a private IP address, because all IP configurations must have a private IP address.</span></span> <span data-ttu-id="e8974-151">Vous pouvez ajouter une ressource d’adresse IP publique existante ou en créer une.</span><span class="sxs-lookup"><span data-stu-id="e8974-151">You can either add an existing public IP address resource, or create a new one.</span></span> <span data-ttu-id="e8974-152">toocreate un nouveau, entrez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="e8974-152">toocreate a new one, enter hello following command:</span></span>
    
        ```bash
        az network public-ip create \
        --resource-group myResourceGroup \
        --location westcentralus \
        --name myPublicIP3 \
        --dns-name mypublicdns3
        ```

        <span data-ttu-id="e8974-153">toocreate une nouvelle configuration IP avec une adresse IP privée statique et le hello associés *myPublicIP3* adresse IP publique de ressources d’adresses, entrez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="e8974-153">toocreate a new IP configuration with a static private IP address and hello associated *myPublicIP3* public IP address resource, enter hello following command:</span></span>

        ```bash
        az network nic ip-config create \
        --resource-group myResourceGroup \
        --nic-name myNic1 \
        --name IPConfig-5 \
        --private-ip-address 10.0.0.8
        --public-ip-address myPublicIP3
        ```

    - <span data-ttu-id="e8974-154">**Configuration IP existante de hello associer ressource tooan** une ressource d’adresse IP publique peut être uniquement la configuration IP tooan associés qui n’en avez pas encore associé.</span><span class="sxs-lookup"><span data-stu-id="e8974-154">**Associate hello resource tooan existing IP configuration** A public IP address resource can only be associated tooan IP configuration that doesn't already have one associated.</span></span> <span data-ttu-id="e8974-155">Vous pouvez déterminer si une configuration IP a une adresse IP publique associée en saisissant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="e8974-155">You can determine whether an IP configuration has an associated public IP address by entering hello following command:</span></span>

        ```bash
        az network nic ip-config list \
        --resource-group myResourceGroup \
        --nic-name myNic1 \
        --query "[?provisioningState=='Succeeded'].{ Name: name, PublicIpAddressId: publicIpAddress.id }" --output table
        ```

        <span data-ttu-id="e8974-156">Sortie retournée :</span><span class="sxs-lookup"><span data-stu-id="e8974-156">Returned output:</span></span>
    
            Name        PublicIpAddressId
            
            ipconfig1   /subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP1
            IPConfig-2  /subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP2
            IPConfig-3

        <span data-ttu-id="e8974-157">Depuis hello **PublicIpAddressId** colonne *IpConfig-3* est vide dans hello de sortie, aucune ressource d’adresse IP publique n’est tooit actuellement associé.</span><span class="sxs-lookup"><span data-stu-id="e8974-157">Since hello **PublicIpAddressId** column for *IpConfig-3* is blank in hello output, no public IP address resource is currently associated tooit.</span></span> <span data-ttu-id="e8974-158">Vous pouvez ajouter un existant publique IP adresse ressource tooIpConfig-3, ou entrez hello suivant toocreate commande une :</span><span class="sxs-lookup"><span data-stu-id="e8974-158">You can add an existing public IP address resource tooIpConfig-3, or enter hello following command toocreate one:</span></span>

        ```bash
        az network public-ip create \
        --resource-group  myResourceGroup
        --location westcentralus \
        --name myPublicIP3 \
        --dns-name mypublicdns3 \
        --allocation-method Static
        ```
    
        <span data-ttu-id="e8974-159">Entrez hello commande hello tooassociate adresse IP publique adresse configuration IP existante toohello ressource nommée suivante *IPConfig-3*:</span><span class="sxs-lookup"><span data-stu-id="e8974-159">Enter hello following command tooassociate hello public IP address resource toohello existing IP configuration named *IPConfig-3*:</span></span>
    
        ```bash
        az network nic ip-config update \
        --resource-group myResourceGroup \
        --nic-name myNic1 \
        --name IPConfig-3 \
        --public-ip myPublicIP3
        ```

3. <span data-ttu-id="e8974-160">Vue hello des adresses IP privées et hello publique d’adresses IP les ID de ressource attribués toohello carte réseau en entrant hello la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="e8974-160">View hello private IP addresses and hello public IP address resource Ids assigned toohello NIC by entering hello following command:</span></span>

    ```bash
    az network nic ip-config list \
    --resource-group myResourceGroup \
    --nic-name myNic1 \
    --query "[?provisioningState=='Succeeded'].{ Name: name, PrivateIpAddress: privateIpAddress, PrivateIpAllocationMethod: privateIpAllocationMethod, PublicIpAddressId: publicIpAddress.id }" --output table
    ```

    <span data-ttu-id="e8974-161">Sortie retournée :</span><span class="sxs-lookup"><span data-stu-id="e8974-161">Returned output:</span></span> <br>
    
        Name        PrivateIpAddress    PrivateIpAllocationMethod   PublicIpAddressId
        
        ipconfig1   10.0.0.4            Static                      /subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP1
        IPConfig-2  10.0.0.5            Static                      /subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP2
        IPConfig-3  10.0.0.6            Static                      /subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP3
    

4. <span data-ttu-id="e8974-162">Ajouter des adresses IP privées de hello, vous avez ajouté le système d’exploitation VM toohello NIC toohello en suivant les instructions de hello Bonjour [ajouter une adresse IP traite le système d’exploitation de l’ordinateur virtuel tooa](#os-config) section de cet article.</span><span class="sxs-lookup"><span data-stu-id="e8974-162">Add hello private IP addresses you added toohello NIC toohello VM operating system by following hello instructions in hello [Add IP addresses tooa VM operating system](#os-config) section of this article.</span></span> <span data-ttu-id="e8974-163">N’ajoutez pas hello publique IP adresses toohello système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="e8974-163">Do not add hello public IP addresses toohello operating system.</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-os-config.md](../../includes/virtual-network-multiple-ip-addresses-os-config.md)]
