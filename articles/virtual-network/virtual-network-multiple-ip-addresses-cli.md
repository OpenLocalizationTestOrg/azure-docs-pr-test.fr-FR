---
title: "Machine virtuelle avec adresses IP à l’aide d’Azure CLI 2.0 | Microsoft Docs"
description: "Découvrez comment attribuer plusieurs adresses IP à une machine virtuelle à l’aide d’Azure CLI 2.0 | Resource Manager"
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
ms.openlocfilehash: 0e9b2ef89ca39a7988a7b2573496a605dfc604b4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="assign-multiple-ip-addresses-to-virtual-machines-using-the-azure-cli-20"></a><span data-ttu-id="f0b2c-103">Affecter plusieurs adresses IP à des machines virtuelles à l’aide d’Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="f0b2c-103">Assign multiple IP addresses to virtual machines using the Azure CLI 2.0</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-intro.md](../../includes/virtual-network-multiple-ip-addresses-intro.md)]

<span data-ttu-id="f0b2c-104">Cet article explique comment créer une machine virtuelle dans le modèle de déploiement Azure Resource Manager à l’aide de l’interface Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="f0b2c-104">This article explains how to create a virtual machine (VM) through the Azure Resource Manager deployment model using the Azure CLI 2.0.</span></span> <span data-ttu-id="f0b2c-105">Il n’est pas possible d’affecter plusieurs adresses IP à des ressources créées à l’aide du modèle de déploiement classique.</span><span class="sxs-lookup"><span data-stu-id="f0b2c-105">Multiple IP addresses cannot be assigned to resources created through the classic deployment model.</span></span> <span data-ttu-id="f0b2c-106">Pour en savoir plus sur les modèles de déploiement Azure, voir [Comprendre les modèles de déploiement](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="f0b2c-106">To learn more about Azure deployment models, read the [Understand deployment models](../resource-manager-deployment-model.md) article.</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-template-scenario.md](../../includes/virtual-network-multiple-ip-addresses-scenario.md)]

## <span data-ttu-id="f0b2c-107"><a name = "create"></a>Créer une machine virtuelle avec plusieurs adresses IP</span><span class="sxs-lookup"><span data-stu-id="f0b2c-107"><a name = "create"></a>Create a VM with multiple IP addresses</span></span>

<span data-ttu-id="f0b2c-108">Vous pouvez effectuer cette tâche à l’aide d’Azure CLI 2.0 (cet article) ou d’[Azure CLI 1.0](virtual-network-multiple-ip-addresses-cli-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="f0b2c-108">You can complete this task using the Azure CLI 2.0 (this article) or the [Azure CLI 1.0](virtual-network-multiple-ip-addresses-cli-nodejs.md).</span></span> <span data-ttu-id="f0b2c-109">Modifiez les valeurs, le cas échéant, en fonction de votre environnement.</span><span class="sxs-lookup"><span data-stu-id="f0b2c-109">Change the values, as appropriate, for your environment.</span></span> <span data-ttu-id="f0b2c-110">Les étapes qui suivent expliquent comment créer un exemple de machine virtuelle avec plusieurs adresses IP, comme décrit dans le scénario.</span><span class="sxs-lookup"><span data-stu-id="f0b2c-110">The steps that follow explain how to create an example VM with multiple IP addresses, as described in the scenario.</span></span> <span data-ttu-id="f0b2c-111">Modifiez les valeurs des variables entre symboles "" et les types d’adresses IP en fonction des besoins de votre implémentation.</span><span class="sxs-lookup"><span data-stu-id="f0b2c-111">Change variable values in "" and IP address types as required for your implementation.</span></span> 

1. <span data-ttu-id="f0b2c-112">Installez [Azure CLI 2.0](/cli/azure/install-az-cli2) si vous ne l’avez pas encore fait.</span><span class="sxs-lookup"><span data-stu-id="f0b2c-112">Install the [Azure CLI 2.0](/cli/azure/install-az-cli2) if you don't already have it installed.</span></span>
2. <span data-ttu-id="f0b2c-113">Créez une paire de clés SSH publique et privée pour les machines virtuelles Linux en effectuant les étapes décrites dans l’article [Créer une paire de clés publique et privée SSH pour les machines virtuelles Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f0b2c-113">Create an SSH public and private key pair for Linux VMs by completing the steps in the [Create an SSH public and private key pair for Linux VMs](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
3. <span data-ttu-id="f0b2c-114">À partir d’un interpréteur de commandes, connectez-vous avec la commande `az login`, puis sélectionnez l’abonnement que vous utilisez.</span><span class="sxs-lookup"><span data-stu-id="f0b2c-114">From a command shell, login with the command `az login` and select the subscription you're using.</span></span>
4. <span data-ttu-id="f0b2c-115">Créez la machine virtuelle en exécutant le script suivant sur un ordinateur Linux ou Mac.</span><span class="sxs-lookup"><span data-stu-id="f0b2c-115">Create the VM by executing the script that follows on a Linux or Mac computer.</span></span> <span data-ttu-id="f0b2c-116">Le script crée un groupe de ressources, un réseau virtuel (VNet), une carte réseau avec trois configurations IP et une machine virtuelle avec les deux cartes réseau qui lui sont associées.</span><span class="sxs-lookup"><span data-stu-id="f0b2c-116">The script creates a resource group, one virtual network (VNet), one NIC with three IP configurations, and a VM with the two NICs attached to it.</span></span> <span data-ttu-id="f0b2c-117">La carte réseau, l’adresse IP publique, le réseau virtuel et les ressources de la machine virtuelle doivent se trouver au même emplacement et correspondre au même abonnement.</span><span class="sxs-lookup"><span data-stu-id="f0b2c-117">The NIC, public IP address, virtual network, and VM resources must all exist in the same location and subscription.</span></span> <span data-ttu-id="f0b2c-118">Bien que les ressources n’aient pas toutes à se trouver dans le même groupe de ressources, c’est le cas dans le script suivant.</span><span class="sxs-lookup"><span data-stu-id="f0b2c-118">Though the resources don't all have to exist in the same resource group, in the following script they do.</span></span>

```bash
    
#!/bin/sh
    
RgName="myResourceGroup"
Location="westcentralus"
az group create --name $RgName --location $Location
    
# Create a public IP address resource with a static IP address using the `--allocation-method Static` option. If you
# do not specify this option, the address is allocated dynamically. The address is assigned to the resource from a pool
# of IP adresses unique to each Azure region. Download and view the file from
# https://www.microsoft.com/en-us/download/details.aspx?id=41653 that lists the ranges for each region.

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

# Create a network interface connected to the subnet and associate the public IP address to it. Azure will create the
# first IP configuration with a static private IP address and will associate the public IP address resource to it.

NicName="MyNic1"
az network nic create \
--name $NicName \
--resource-group $RgName \
--location $Location \
--subnet $VnetSubnet1Name \
--private-ip-address 10.0.0.4
--vnet-name $VnetName \
--public-ip-address $PipName
    
# Create a second public IP address, a second IP configuration, and associate it to the NIC. This configuration has a
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

# Create a third IP configuration, and associate it to the NIC. This configuration has  static private IP address and   # no public IP address.

azure network nic ip-config create \
--resource-group $RgName \
--nic-name $NicName \
--private-ip-address 10.0.0.6 \
--name IPConfig-3

# Note: Though this article assigns all IP configurations to a single NIC, you can also assign multiple IP configurations
# to any NIC in a VM. To learn how to create a VM with multiple NICs, read the Create a VM with multiple NICs 
# article: https://docs.microsoft.com/azure/virtual-network/virtual-network-deploy-multinic-arm-cli.

# Create a VM and attach the NIC.

VmName="myVm"

# Replace the value for the following **VmSize** variable with a value from the
# https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-sizes rticle. The script fails if the VM size
# is not supported in the location you select. Run the `azure vm sizes --location estcentralus` command to get a full list
# of VMs in US West Central, for example.

VmSize="Standard_DS1"

# Replace the value for the OsImage variable value with a value for *urn* from the utput returned by entering the
# `az vm image list` command.

OsImage="credativ:Debian:8:latest"

Username="adminuser"

# Replace the following value with the path to your public key file. If you're creating a Windows VM, remove the following
# line and you'll be prompted for the password you want to configure for the VM.

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

<span data-ttu-id="f0b2c-119">Outre la création d’une machine virtuelle avec une carte réseau dotée de 3 configurations IP, le script crée :</span><span class="sxs-lookup"><span data-stu-id="f0b2c-119">In addition to creating a VM with a NIC with 3 IP configurations, the script creates:</span></span>

- <span data-ttu-id="f0b2c-120">Un disque unique géré par compte Premium par défaut, mais vous pouvez choisir un autre type de disque.</span><span class="sxs-lookup"><span data-stu-id="f0b2c-120">A single premium managed disk by default, but you have other options for the disk type you can create.</span></span> <span data-ttu-id="f0b2c-121">Consultez l’article [Créer une machine virtuelle Linux à l’aide d’Azure CLI 2.0](../virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="f0b2c-121">Read the [Create a Linux VM using the Azure CLI 2.0](../virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json) article for details.</span></span>
- <span data-ttu-id="f0b2c-122">Un réseau virtuel avec un sous-réseau et deux adresses IP publiques.</span><span class="sxs-lookup"><span data-stu-id="f0b2c-122">A virtual network with one subnet and two public IP addresses.</span></span> <span data-ttu-id="f0b2c-123">Vous pouvez également utiliser des ressources *existantes* en matière de réseau virtuel, sous-réseau, carte réseau ou adresse IP publique.</span><span class="sxs-lookup"><span data-stu-id="f0b2c-123">Alternatively, you can use *existing* virtual network, subnet, NIC, or public IP address resources.</span></span> <span data-ttu-id="f0b2c-124">Pour savoir comment utiliser des ressources réseau existantes au lieu de créer des ressources supplémentaires, utilisez `az vm create -h`.</span><span class="sxs-lookup"><span data-stu-id="f0b2c-124">To learn how to use existing network resources rather than creating additional resources, enter `az vm create -h`.</span></span>

<span data-ttu-id="f0b2c-125">Les adresses IP publiques ont un coût nominal.</span><span class="sxs-lookup"><span data-stu-id="f0b2c-125">Public IP addresses have a nominal fee.</span></span> <span data-ttu-id="f0b2c-126">Pour en savoir plus, lisez la page [Tarification des adresses IP](https://azure.microsoft.com/pricing/details/ip-addresses) .</span><span class="sxs-lookup"><span data-stu-id="f0b2c-126">To learn more about IP address pricing, read the [IP address pricing](https://azure.microsoft.com/pricing/details/ip-addresses) page.</span></span> <span data-ttu-id="f0b2c-127">Il existe une limite au nombre d’adresses IP publiques qui peuvent être utilisées dans un abonnement.</span><span class="sxs-lookup"><span data-stu-id="f0b2c-127">There is a limit to the number of public IP addresses that can be used in a subscription.</span></span> <span data-ttu-id="f0b2c-128">Pour plus d’informations sur les limites, voir [Limites d’Azure](../azure-subscription-service-limits.md#networking-limits).</span><span class="sxs-lookup"><span data-stu-id="f0b2c-128">To learn more about the limits, read the [Azure limits](../azure-subscription-service-limits.md#networking-limits) article.</span></span>

<span data-ttu-id="f0b2c-129">Une fois la machine virtuelle créée, saisissez la commande `az network nic show --name MyNic1 --resource-group myResourceGroup` afin d’afficher la configuration de carte réseau.</span><span class="sxs-lookup"><span data-stu-id="f0b2c-129">After the VM is created, enter the `az network nic show --name MyNic1 --resource-group myResourceGroup` command to view the NIC configuration.</span></span> <span data-ttu-id="f0b2c-130">Saisissez l’élément `az network nic ip-config list --nic-name MyNic1 --resource-group myResourceGroup --output table` afin d’afficher une liste des configurations IP associées à la carte réseau.</span><span class="sxs-lookup"><span data-stu-id="f0b2c-130">Enter the `az network nic ip-config list --nic-name MyNic1 --resource-group myResourceGroup --output table` to view a list of the IP configurations associated to the NIC.</span></span>

<span data-ttu-id="f0b2c-131">Ajoutez les adresses IP privées pour le système d’exploitation de la machine virtuelle en suivant les étapes pour votre système d’exploitation dans la section [Ajouter des adresses IP à un système d’exploitation de machine virtuelle](#os-config) de cet article.</span><span class="sxs-lookup"><span data-stu-id="f0b2c-131">Add the private IP addresses to the VM operating system by completing the steps for your operating system in the [Add IP addresses to a VM operating system](#os-config) section of this article.</span></span>

## <span data-ttu-id="f0b2c-132"><a name="add"></a>Ajouter des adresses IP à une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="f0b2c-132"><a name="add"></a>Add IP addresses to a VM</span></span>

<span data-ttu-id="f0b2c-133">Vous pouvez ajouter des adresses IP privées et publiques à une carte réseau en suivant les étapes décrites ci-après.</span><span class="sxs-lookup"><span data-stu-id="f0b2c-133">You can add additional private and public IP addresses to an existing NIC by completing the steps that follow.</span></span> <span data-ttu-id="f0b2c-134">Les exemples reposent sur le [scénario](#Scenario) décrit dans cet article.</span><span class="sxs-lookup"><span data-stu-id="f0b2c-134">The examples build upon the [scenario](#Scenario) described in this article.</span></span>

1. <span data-ttu-id="f0b2c-135">Ouvrez un interpréteur de commandes Azure et effectuez les étapes restantes de cette section en une seule session.</span><span class="sxs-lookup"><span data-stu-id="f0b2c-135">Open a command shell and complete the remaining steps in this section within a single session.</span></span> <span data-ttu-id="f0b2c-136">Si l’interface Azure CLI n’est pas encore installée et configurée, suivez les étapes décrites dans l’article consacré à l’[installation d’Azure CLI 2.0](/cli/azure/install-az-cli2?toc=%2fazure%2fvirtual-network%2ftoc.json) et connectez-vous à votre compte Azure avec la commande `az-login`.</span><span class="sxs-lookup"><span data-stu-id="f0b2c-136">If you don't already have Azure CLI installed and configured, complete the steps in the [Azure CLI 2.0 installation](/cli/azure/install-az-cli2?toc=%2fazure%2fvirtual-network%2ftoc.json) article and login to your Azure account with the `az-login` command.</span></span>

2. <span data-ttu-id="f0b2c-137">Suivez les étapes de l’une des sections suivantes, selon vos besoins :</span><span class="sxs-lookup"><span data-stu-id="f0b2c-137">Complete the steps in one of the following sections, based on your requirements:</span></span>

    <span data-ttu-id="f0b2c-138">**Ajouter une adresse IP privée**</span><span class="sxs-lookup"><span data-stu-id="f0b2c-138">**Add a private IP address**</span></span>
    
    <span data-ttu-id="f0b2c-139">Pour ajouter une adresse IP privée à une carte d’interface réseau, vous devez créer une configuration IP à l’aide de la commande ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="f0b2c-139">To add a private IP address to a NIC, you must create an IP configuration using the command that follows.</span></span> <span data-ttu-id="f0b2c-140">L’adresse IP statique doit être une adresse non utilisée pour le sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="f0b2c-140">The static IP address must be an unused address for the subnet.</span></span>

    ```bash
    az network nic ip-config create \
    --resource-group myResourceGroup \
    --nic-name myNic1 \
    --private-ip-address 10.0.0.7 \
    --name IPConfig-4
    ```
    
    <span data-ttu-id="f0b2c-141">Créez autant de configurations que nécessaire, à l’aide de noms de configuration unique et d’adresses IP privées (pour les configurations avec des adresses IP statiques).</span><span class="sxs-lookup"><span data-stu-id="f0b2c-141">Create as many configurations as you require, using unique configuration names and private IP addresses (for configurations with static IP addresses).</span></span>

    <span data-ttu-id="f0b2c-142">**Ajouter une adresse IP publique**</span><span class="sxs-lookup"><span data-stu-id="f0b2c-142">**Add a public IP address**</span></span>
    
    <span data-ttu-id="f0b2c-143">Pour ajouter une adresse IP publique, associez-la à une configuration IP nouvelle ou existante.</span><span class="sxs-lookup"><span data-stu-id="f0b2c-143">A public IP address is added by associating it to either a new IP configuration or an existing IP configuration.</span></span> <span data-ttu-id="f0b2c-144">Suivez les étapes de l’une des sections ci-après, selon votre besoin.</span><span class="sxs-lookup"><span data-stu-id="f0b2c-144">Complete the steps in one of the sections that follow, as you require.</span></span>

    <span data-ttu-id="f0b2c-145">Les adresses IP publiques ont un coût nominal.</span><span class="sxs-lookup"><span data-stu-id="f0b2c-145">Public IP addresses have a nominal fee.</span></span> <span data-ttu-id="f0b2c-146">Pour en savoir plus, lisez la page [Tarification des adresses IP](https://azure.microsoft.com/pricing/details/ip-addresses) .</span><span class="sxs-lookup"><span data-stu-id="f0b2c-146">To learn more about IP address pricing, read the [IP address pricing](https://azure.microsoft.com/pricing/details/ip-addresses) page.</span></span> <span data-ttu-id="f0b2c-147">Il existe une limite au nombre d’adresses IP publiques qui peuvent être utilisées dans un abonnement.</span><span class="sxs-lookup"><span data-stu-id="f0b2c-147">There is a limit to the number of public IP addresses that can be used in a subscription.</span></span> <span data-ttu-id="f0b2c-148">Pour plus d’informations sur les limites, voir [Limites d’Azure](../azure-subscription-service-limits.md#networking-limits).</span><span class="sxs-lookup"><span data-stu-id="f0b2c-148">To learn more about the limits, read the [Azure limits](../azure-subscription-service-limits.md#networking-limits) article.</span></span>

    - <span data-ttu-id="f0b2c-149">**Associer la ressource à une nouvelle configuration IP**</span><span class="sxs-lookup"><span data-stu-id="f0b2c-149">**Associate the resource to a new IP configuration**</span></span>
    
        <span data-ttu-id="f0b2c-150">Lorsque vous ajoutez une adresse IP publique dans une nouvelle configuration IP, vous devez également ajouter une adresse IP privée, car toutes les configurations IP doivent avoir une adresse IP privée.</span><span class="sxs-lookup"><span data-stu-id="f0b2c-150">Whenever you add a public IP address in a new IP configuration, you must also add a private IP address, because all IP configurations must have a private IP address.</span></span> <span data-ttu-id="f0b2c-151">Vous pouvez ajouter une ressource d’adresse IP publique existante ou en créer une.</span><span class="sxs-lookup"><span data-stu-id="f0b2c-151">You can either add an existing public IP address resource, or create a new one.</span></span> <span data-ttu-id="f0b2c-152">Pour en créer une nouvelle, saisissez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="f0b2c-152">To create a new one, enter the following command:</span></span>
    
        ```bash
        az network public-ip create \
        --resource-group myResourceGroup \
        --location westcentralus \
        --name myPublicIP3 \
        --dns-name mypublicdns3
        ```

        <span data-ttu-id="f0b2c-153">Pour créer une nouvelle configuration IP avec une adresse IP privée statique et la ressource d’adresse IP publique *myPublicIP3*, saisissez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="f0b2c-153">To create a new IP configuration with a static private IP address and the associated *myPublicIP3* public IP address resource, enter the following command:</span></span>

        ```bash
        az network nic ip-config create \
        --resource-group myResourceGroup \
        --nic-name myNic1 \
        --name IPConfig-5 \
        --private-ip-address 10.0.0.8
        --public-ip-address myPublicIP3
        ```

    - <span data-ttu-id="f0b2c-154">**Associer la ressource à une configuration IP existante** une ressource d’adresse IP publique peut uniquement être associée à une configuration IP qui n’en avez pas encore associé.</span><span class="sxs-lookup"><span data-stu-id="f0b2c-154">**Associate the resource to an existing IP configuration** A public IP address resource can only be associated to an IP configuration that doesn't already have one associated.</span></span> <span data-ttu-id="f0b2c-155">Pour déterminer si une configuration IP a une adresse IP publique associée, entrez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="f0b2c-155">You can determine whether an IP configuration has an associated public IP address by entering the following command:</span></span>

        ```bash
        az network nic ip-config list \
        --resource-group myResourceGroup \
        --nic-name myNic1 \
        --query "[?provisioningState=='Succeeded'].{ Name: name, PublicIpAddressId: publicIpAddress.id }" --output table
        ```

        <span data-ttu-id="f0b2c-156">Sortie retournée :</span><span class="sxs-lookup"><span data-stu-id="f0b2c-156">Returned output:</span></span>
    
            Name        PublicIpAddressId
            
            ipconfig1   /subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP1
            IPConfig-2  /subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP2
            IPConfig-3

        <span data-ttu-id="f0b2c-157">Étant donné que la colonne **PublicIpAddress** pour *IpConfig-3* est vide dans la sortie, aucune ressource d’adresse IP publique n’y est actuellement associée.</span><span class="sxs-lookup"><span data-stu-id="f0b2c-157">Since the **PublicIpAddressId** column for *IpConfig-3* is blank in the output, no public IP address resource is currently associated to it.</span></span> <span data-ttu-id="f0b2c-158">Vous pouvez ajouter une ressource d’adresse IP publique existante sur IpConfig-3, ou entrer la commande suivante pour en créer une :</span><span class="sxs-lookup"><span data-stu-id="f0b2c-158">You can add an existing public IP address resource to IpConfig-3, or enter the following command to create one:</span></span>

        ```bash
        az network public-ip create \
        --resource-group  myResourceGroup
        --location westcentralus \
        --name myPublicIP3 \
        --dns-name mypublicdns3 \
        --allocation-method Static
        ```
    
        <span data-ttu-id="f0b2c-159">Entrez la commande suivante pour associer la ressource d’adresse IP publique à la configuration IP existante nommée *IPConfig-3* :</span><span class="sxs-lookup"><span data-stu-id="f0b2c-159">Enter the following command to associate the public IP address resource to the existing IP configuration named *IPConfig-3*:</span></span>
    
        ```bash
        az network nic ip-config update \
        --resource-group myResourceGroup \
        --nic-name myNic1 \
        --name IPConfig-3 \
        --public-ip myPublicIP3
        ```

3. <span data-ttu-id="f0b2c-160">Affichez les ressources d’adresses IP privées et l’adresse IP publique affectées à la carte d’interface réseau en saisissant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="f0b2c-160">View the private IP addresses and the public IP address resource Ids assigned to the NIC by entering the following command:</span></span>

    ```bash
    az network nic ip-config list \
    --resource-group myResourceGroup \
    --nic-name myNic1 \
    --query "[?provisioningState=='Succeeded'].{ Name: name, PrivateIpAddress: privateIpAddress, PrivateIpAllocationMethod: privateIpAllocationMethod, PublicIpAddressId: publicIpAddress.id }" --output table
    ```

    <span data-ttu-id="f0b2c-161">Sortie retournée :</span><span class="sxs-lookup"><span data-stu-id="f0b2c-161">Returned output:</span></span> <br>
    
        Name        PrivateIpAddress    PrivateIpAllocationMethod   PublicIpAddressId
        
        ipconfig1   10.0.0.4            Static                      /subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP1
        IPConfig-2  10.0.0.5            Static                      /subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP2
        IPConfig-3  10.0.0.6            Static                      /subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP3
    

4. <span data-ttu-id="f0b2c-162">Ajoutez les adresses IP privées que vous avez ajoutées à l’interface réseau pour le système d’exploitation de la machine virtuelle en suivant les instructions fournies dans la section [Ajouter des adresses IP à un système d’exploitation de machine virtuelle](#os-config) de cet article.</span><span class="sxs-lookup"><span data-stu-id="f0b2c-162">Add the private IP addresses you added to the NIC to the VM operating system by following the instructions in the [Add IP addresses to a VM operating system](#os-config) section of this article.</span></span> <span data-ttu-id="f0b2c-163">N’ajoutez pas les adresses IP publiques au système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="f0b2c-163">Do not add the public IP addresses to the operating system.</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-os-config.md](../../includes/virtual-network-multiple-ip-addresses-os-config.md)]
