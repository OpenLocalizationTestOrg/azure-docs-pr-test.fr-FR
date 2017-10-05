---
title: "Déployer des machines virtuelles Linux dans un réseau existant avec l’interface Azure CLI 2.0 | Microsoft Docs"
description: "Découvrez comment déployer une machine virtuelle Linux dans un réseau virtuel existant à l’aide de l’interface Azure CLI 2.0"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 932fd74ec83f43b604382346ee2c273f5453fcd0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-deploy-a-linux-virtual-machine-into-an-existing-azure-virtual-network-with-the-azure-cli"></a><span data-ttu-id="b3f53-103">Procédure de déploiement d’une machine virtuelle Linux dans un réseau virtuel Azure existant à l’aide de l’interface Azure CLI</span><span class="sxs-lookup"><span data-stu-id="b3f53-103">How to deploy a Linux virtual machine into an existing Azure Virtual Network with the Azure CLI</span></span>

<span data-ttu-id="b3f53-104">Cet article vous montre comment utiliser l’interface Azure CLI 2.0 pour déployer une machine virtuelle dans un réseau virtuel existant.</span><span class="sxs-lookup"><span data-stu-id="b3f53-104">This article shows you how to use the Azure CLI 2.0 to deploy a virtual machine (VM) into an existing virtual network.</span></span> <span data-ttu-id="b3f53-105">Les conditions requises sont :</span><span class="sxs-lookup"><span data-stu-id="b3f53-105">The requirements are:</span></span>

- [<span data-ttu-id="b3f53-106">un compte Azure</span><span class="sxs-lookup"><span data-stu-id="b3f53-106">an Azure account</span></span>](https://azure.microsoft.com/pricing/free-trial/)
- [<span data-ttu-id="b3f53-107">des fichiers de clés SSH publiques et privées</span><span class="sxs-lookup"><span data-stu-id="b3f53-107">SSH public and private key files</span></span>](mac-create-ssh-keys.md)

<span data-ttu-id="b3f53-108">Vous pouvez également effectuer ces étapes à l’aide [d’Azure CLI 1.0](deploy-linux-vm-into-existing-vnet-using-cli-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="b3f53-108">You can also perform these steps with the [Azure CLI 1.0](deploy-linux-vm-into-existing-vnet-using-cli-nodejs.md).</span></span>


## <a name="quick-commands"></a><span data-ttu-id="b3f53-109">Commandes rapides</span><span class="sxs-lookup"><span data-stu-id="b3f53-109">Quick Commands</span></span>
<span data-ttu-id="b3f53-110">Si vous avez besoin d’accomplir rapidement cette tâche, la section suivante décrit les commandes nécessaires.</span><span class="sxs-lookup"><span data-stu-id="b3f53-110">If you need to quickly accomplish the task, the following section details the  commands needed.</span></span> <span data-ttu-id="b3f53-111">Pour obtenir plus d’informations et davantage de contexte pour chaque étape, lisez la suite de ce document, [à partir de cette section](#detailed-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="b3f53-111">More detailed information and context for each step can be found the rest of the document, [starting here](#detailed-walkthrough).</span></span>

<span data-ttu-id="b3f53-112">Pour créer cet environnement personnalisé, la dernière version de l’interface [Azure CLI 2.0](/cli/azure/install-az-cli2) doit être installée et connectée à un compte Azure à l’aide de la commande [az login](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="b3f53-112">To create this custom environment, you need the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="b3f53-113">Dans les exemples suivants, remplacez les exemples de noms de paramètre par vos propres valeurs.</span><span class="sxs-lookup"><span data-stu-id="b3f53-113">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="b3f53-114">Les noms de paramètre sont par exemple *myResourceGroup*, *myVnet* et *myVM*.</span><span class="sxs-lookup"><span data-stu-id="b3f53-114">Example parameter names include *myResourceGroup*, *myVnet*, and *myVM*.</span></span>

<span data-ttu-id="b3f53-115">**Conditions préalables :** groupe de ressources Azure, réseau virtuel et sous-réseau, groupe de sécurité réseau avec SSH entrant et une carte d’interface réseau virtuelle.</span><span class="sxs-lookup"><span data-stu-id="b3f53-115">**Pre-requirements:** Azure resource group, virtual network and subnet, network security group with SSH inbound, and a virtual network interface card.</span></span>

### <a name="deploy-the-vm-into-the-virtual-network-infrastructure"></a><span data-ttu-id="b3f53-116">Déployer la machine virtuelle dans l’infrastructure de réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="b3f53-116">Deploy the VM into the virtual network infrastructure</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image Debian \
    --admin-username azureuser \
    --generate-ssh-keys \
    --nics myNic
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="b3f53-117">Procédure pas à pas</span><span class="sxs-lookup"><span data-stu-id="b3f53-117">Detailed walkthrough</span></span>

<span data-ttu-id="b3f53-118">Les ressources Azure telles que les réseaux virtuels et les groupes de sécurité réseau doivent être des ressources statiques et durables qui sont rarement déployées.</span><span class="sxs-lookup"><span data-stu-id="b3f53-118">Azure assets like virtual networks and network security groups should be static and long lived resources that are rarely deployed.</span></span> <span data-ttu-id="b3f53-119">Une fois un réseau virtuel déployé, il peut être réutilisé par de nouveaux redéploiements, sans impact négatif sur l’infrastructure.</span><span class="sxs-lookup"><span data-stu-id="b3f53-119">Once a virtual network has been deployed, it can be reused by new deployments without any adverse affects to the infrastructure.</span></span> <span data-ttu-id="b3f53-120">Si on considère un réseau virtuel comme un commutateur réseau matériel classique, il est évident qu’il serait inutile de configurer un tout nouveau commutateur matériel lors de chaque déploiement.</span><span class="sxs-lookup"><span data-stu-id="b3f53-120">Think about a virtual network as being a traditional hardware network switch - you would not need to configure a brand new hardware switch with each deployment.</span></span> <span data-ttu-id="b3f53-121">Avec un réseau virtuel correctement configuré, vous pouvez continuer à déployer de nouveaux serveurs dans ce réseau virtuel encore et encore avec peu de modifications requises, voire aucune, tout au long de la durée de vie du réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="b3f53-121">With a correctly configured virtual network, you can continue to deploy new VMs into that virtual network over and over with few, if any, changes required over the life of the virtual network.</span></span>

<span data-ttu-id="b3f53-122">Pour créer cet environnement personnalisé, la dernière version de l’interface [Azure CLI 2.0](/cli/azure/install-az-cli2) doit être installée et connectée à un compte Azure à l’aide de la commande [az login](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="b3f53-122">To create this custom environment, you need the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="b3f53-123">Dans les exemples suivants, remplacez les exemples de noms de paramètre par vos propres valeurs.</span><span class="sxs-lookup"><span data-stu-id="b3f53-123">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="b3f53-124">Les noms de paramètre sont par exemple *myResourceGroup*, *myVnet* et *myVM*.</span><span class="sxs-lookup"><span data-stu-id="b3f53-124">Example parameter names include *myResourceGroup*, *myVnet*, and *myVM*.</span></span>

## <a name="create-the-resource-group"></a><span data-ttu-id="b3f53-125">Créer le groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="b3f53-125">Create the resource group</span></span>

<span data-ttu-id="b3f53-126">Tout d’abord, créez un groupe de ressources Azure pour organiser tous les éléments créés dans cette procédure pas à pas.</span><span class="sxs-lookup"><span data-stu-id="b3f53-126">First, create an Azure resource group to organize everything you create in this walkthrough.</span></span> <span data-ttu-id="b3f53-127">Pour plus d’informations sur les groupes de ressources, consultez [Vue d’ensemble d’Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b3f53-127">For more information on resource groups, see [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="b3f53-128">Créez le groupe de ressources avec la commande [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="b3f53-128">Create the resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="b3f53-129">L’exemple suivant crée un groupe de ressources nommé *myResourceGroup* à l’emplacement *eastus* :</span><span class="sxs-lookup"><span data-stu-id="b3f53-129">The following example creates a resource group named *myResourceGroup* in the *eastus* location:</span></span>

```azurecli
az group create \
    --name myResourceGroup \
    --location eastus
```

## <a name="create-the-virtual-network"></a><span data-ttu-id="b3f53-130">Créer un réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="b3f53-130">Create the virtual network</span></span>

<span data-ttu-id="b3f53-131">Permet de créer un réseau virtuel Azure dans lequel lancer les machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="b3f53-131">Lets build an Azure virtual network to launch the VMs into.</span></span> <span data-ttu-id="b3f53-132">Pour plus d’informations sur les réseaux virtuels Azure, consultez la section [Créer un réseau virtuel à l’aide de l’interface de ligne de commande Azure](../../virtual-network/virtual-networks-create-vnet-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="b3f53-132">For more information on virtual networks, see [Create a virtual network by using the Azure CLI](../../virtual-network/virtual-networks-create-vnet-arm-cli.md).</span></span> <span data-ttu-id="b3f53-133">Créez le réseau virtuel avec la commande [az network vnet create](/cli/azure/network/vnet#create).</span><span class="sxs-lookup"><span data-stu-id="b3f53-133">Create the virtual network with [az network vnet create](/cli/azure/network/vnet#create).</span></span> <span data-ttu-id="b3f53-134">L’exemple suivant permet de créer un réseau virtuel nommé *myVnet* et un sous-réseau nommé *mySubnet* :</span><span class="sxs-lookup"><span data-stu-id="b3f53-134">The following example creates a virtual network named *myVnet* and subnet named *mySubnet*:</span></span>

```azurecli
az network vnet create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myVnet \
    --address-prefix 10.10.0.0/16 \
    --subnet-name mySubnet \
    --subnet-prefix 10.10.1.0/24
```

## <a name="create-the-network-security-group"></a><span data-ttu-id="b3f53-135">Créer le groupe de sécurité réseau</span><span class="sxs-lookup"><span data-stu-id="b3f53-135">Create the network security group</span></span>

<span data-ttu-id="b3f53-136">Les groupes de sécurité réseau Azure s’apparentent à un pare-feu au niveau de la couche réseau.</span><span class="sxs-lookup"><span data-stu-id="b3f53-136">Azure network security groups are equivalent to a firewall at the network layer.</span></span> <span data-ttu-id="b3f53-137">Pour plus d’informations sur les groupes de sécurité réseau, voir [Guide de création des groupes de sécurité réseau dans l’interface de ligne de commande Azure](../../virtual-network/virtual-networks-create-nsg-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="b3f53-137">For more information on network security groups, see [How to create network security groups in the Azure CLI](../../virtual-network/virtual-networks-create-nsg-arm-cli.md).</span></span> <span data-ttu-id="b3f53-138">Créez le groupe de sécurité réseau avec la commande [az network nsg create](/cli/azure/network/nsg#create).</span><span class="sxs-lookup"><span data-stu-id="b3f53-138">Create the network security group with [az network nsg create](/cli/azure/network/nsg#create).</span></span> <span data-ttu-id="b3f53-139">L’exemple suivant crée un groupe de sécurité réseau nommé *myNetworkSecurityGroup* :</span><span class="sxs-lookup"><span data-stu-id="b3f53-139">The following example creates a network security group named *myNetworkSecurityGroup*:</span></span>

```azurecli
az network nsg create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNetworkSecurityGroup
```

## <a name="add-an-inbound-ssh-allow-rule"></a><span data-ttu-id="b3f53-140">Ajouter une règle d’autorisation SSH entrante</span><span class="sxs-lookup"><span data-stu-id="b3f53-140">Add an inbound SSH allow rule</span></span>

<span data-ttu-id="b3f53-141">La machine virtuelle a besoin d’un accès à partir d’Internet. Une règle autorisant le trafic entrant sur le port 22 à être acheminé à travers le réseau jusqu’au port 22 de la machine virtuelle est donc nécessaire.</span><span class="sxs-lookup"><span data-stu-id="b3f53-141">The VM needs access from the internet, so a rule allowing inbound port 22 traffic to be passed through the network to port 22 on the VM is needed.</span></span> <span data-ttu-id="b3f53-142">Ajoutez une règle de trafic entrant pour le groupe de sécurité réseau avec la commande [az network nsg rule create](/cli/azure/network/nsg/rule#create).</span><span class="sxs-lookup"><span data-stu-id="b3f53-142">Add an inbound rule for the network security group with [az network nsg rule create](/cli/azure/network/nsg/rule#create).</span></span> <span data-ttu-id="b3f53-143">L’exemple suivant crée une règle nommée *myNetworkSecurityGroupRuleSSH* :</span><span class="sxs-lookup"><span data-stu-id="b3f53-143">The following example creates a rule named *myNetworkSecurityGroupRuleSSH*:</span></span>

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRuleSSH \
    --priority 1000 \
    --protocol tcp \
    --destination-port-range 22 \
```

## <a name="attach-the-subnet-to-the-network-security-group"></a><span data-ttu-id="b3f53-144">Joindre le sous-réseau au groupe de sécurité réseau</span><span class="sxs-lookup"><span data-stu-id="b3f53-144">Attach the subnet to the network security group</span></span>

<span data-ttu-id="b3f53-145">Les règles des groupes de sécurité réseau peuvent être appliquées à un sous-réseau ou à une interface réseau spécifique.</span><span class="sxs-lookup"><span data-stu-id="b3f53-145">The network security group rules can be applied to a subnet or a specific virtual network interface.</span></span> <span data-ttu-id="b3f53-146">Permet de joindre le groupe de sécurité réseau à notre sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="b3f53-146">Lets attach the network security group to our subnet.</span></span> <span data-ttu-id="b3f53-147">Joignez votre sous-réseau au groupe de sécurité réseau avec [az network vnet subnet update](/cli/azure/network/vnet/subnet#update) :</span><span class="sxs-lookup"><span data-stu-id="b3f53-147">Attach your subnet to the network security group with [az network vnet subnet update](/cli/azure/network/vnet/subnet#update):</span></span>

```azurecli
az network vnet subnet update \
    --resource-group myResourceGroup \
    --vnet-name myVnet \
    --name mySubnet \
    --network-security-group myNetworkSecurityGroup
```

## <a name="add-a-virtual-network-interface-card-to-the-subnet"></a><span data-ttu-id="b3f53-148">Ajout d’une carte réseau virtuelle au sous-réseau</span><span class="sxs-lookup"><span data-stu-id="b3f53-148">Add a virtual network interface card to the subnet</span></span>

<span data-ttu-id="b3f53-149">Les cartes réseau virtuelles (VNic) sont importantes, car vous pouvez les réutiliser en les connectant sur différentes machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="b3f53-149">Virtual network interface cards (VNics) are important as you can reuse them by connecting them to different VMs.</span></span> <span data-ttu-id="b3f53-150">Cette réutilisation vous permet de conserver la carte réseau virtuelle comme une ressource statique, tandis que les machines virtuelles peuvent être temporaires.</span><span class="sxs-lookup"><span data-stu-id="b3f53-150">This reuse allows you to keep the VNic as a static resource while the VMs can be temporary.</span></span> <span data-ttu-id="b3f53-151">Créez une carte réseau virtuelle et associez-la au sous-réseau avec [az network nic create](/cli/azure/network/nic#create).</span><span class="sxs-lookup"><span data-stu-id="b3f53-151">Create a VNic and associate it with the subnet with [az network nic create](/cli/azure/network/nic#create).</span></span> <span data-ttu-id="b3f53-152">L’exemple suivant crée une carte réseau virtuelle nommée *myNic* :</span><span class="sxs-lookup"><span data-stu-id="b3f53-152">The following example creates a VNic named *myNic*:</span></span>

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNic \
    --vnet-name myVnet \
    --subnet mySubnet
```

## <a name="deploy-the-vm-into-the-virtual-network-infrastructure"></a><span data-ttu-id="b3f53-153">Déployer la machine virtuelle dans l’infrastructure de réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="b3f53-153">Deploy the VM into the virtual network infrastructure</span></span>

<span data-ttu-id="b3f53-154">Vous disposez désormais d’un réseau virtuel et d’un sous-réseau, ainsi que d’un groupe de sécurité réseau qui protège le sous-réseau en bloquant l’ensemble du trafic entrant, à l’exception du port 22 pour SSH.</span><span class="sxs-lookup"><span data-stu-id="b3f53-154">You now have a virtual network and subnet, and a network security group to protect the subnet by blocking all inbound traffic except port 22 for SSH.</span></span> <span data-ttu-id="b3f53-155">La machine virtuelle peut désormais être déployée au sein de cette infrastructure réseau existante.</span><span class="sxs-lookup"><span data-stu-id="b3f53-155">The VM can now be deployed inside this existing network infrastructure.</span></span>

<span data-ttu-id="b3f53-156">Créez votre machine virtuelle avec [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="b3f53-156">Create your VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="b3f53-157">Pour plus d’informations sur l’utilisation des indicateurs avec l’interface Azure 2.0 pour déployer une machine virtuelle complète, consultez la section [Créer un environnement Linux complet à l’aide de l’interface Azure CLI 2.0 (version préliminaire)](create-cli-complete.md).</span><span class="sxs-lookup"><span data-stu-id="b3f53-157">For more information on the flags to use with the Azure CLI 2.0 to deploy a complete VM, see [Create a complete Linux environment by using the Azure CLI](create-cli-complete.md).</span></span>

<span data-ttu-id="b3f53-158">L’exemple qui suit permet de créer une machine virtuelle qui utilise Azure Managed Disks.</span><span class="sxs-lookup"><span data-stu-id="b3f53-158">The following example creates a VM using Azure Managed Disks.</span></span> <span data-ttu-id="b3f53-159">Ces disques sont gérés par la plateforme Azure et ne nécessitent pas de préparation ou d’emplacement pour les stocker.</span><span class="sxs-lookup"><span data-stu-id="b3f53-159">These disks are handled by the Azure platform and do not require any preparation or location to store them.</span></span> <span data-ttu-id="b3f53-160">Pour plus d’informations sur les disques gérés, consultez [Vue d’ensemble d’Azure Managed Disks](../../storage/storage-managed-disks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b3f53-160">For more information about managed disks, see [Azure Managed Disks overview](../../storage/storage-managed-disks-overview.md).</span></span> <span data-ttu-id="b3f53-161">Si vous souhaitez utiliser des disques non gérés, consultez la remarque supplémentaire ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="b3f53-161">If you wish to use unmanaged disks, see the additional note below.</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image Debian \
    --admin-username azureuser \
    --generate-ssh-keys \
    --nics myNic
```

<span data-ttu-id="b3f53-162">Si vous utilisez des disques gérés, ignorez cette étape.</span><span class="sxs-lookup"><span data-stu-id="b3f53-162">If you use managed disks, skip this step.</span></span> <span data-ttu-id="b3f53-163">Si vous voulez utiliser des disques non gérés, vous devez ajouter les paramètres supplémentaires suivants à la commande de traitement pour créer les disques non gérés dans le compte de stockage nommé `mystorageaccount` :</span><span class="sxs-lookup"><span data-stu-id="b3f53-163">If you wish to use unmanaged disks, you need to add the following additional parameters to the proceeding command to create unmanaged disks in the storage account named `mystorageaccount`:</span></span> 

```azurecli
    --use-unmanaged-disk \
    --storage-account mystorageaccount
```

<span data-ttu-id="b3f53-164">En utilisant les indicateurs CLI pour appeler les ressources existantes, vous indiquez à Azure de déployer la machine virtuelle au sein du réseau existant.</span><span class="sxs-lookup"><span data-stu-id="b3f53-164">By using the CLI flags to call out existing resources, you instruct Azure to deploy the VM inside the existing network.</span></span> <span data-ttu-id="b3f53-165">Lorsqu’un réseau virtuel et un sous-réseau ont été déployés, ils peuvent être conservés en tant que ressources statiques ou permanentes à l’intérieur de votre région Azure.</span><span class="sxs-lookup"><span data-stu-id="b3f53-165">Once a virtual network and subnet have been deployed, they can be left as static or permanent resources inside your Azure region.</span></span> <span data-ttu-id="b3f53-166">Dans cet exemple, vous n’avez pas créé ou affecté une adresse IP publique à la carte réseau virtuelle, cette machine virtuelle n’est donc pas accessible publiquement sur Internet.</span><span class="sxs-lookup"><span data-stu-id="b3f53-166">In this example, you did not create and assign a public IP address to the VNic, so this VM is not publicly accessible over the Internet.</span></span> <span data-ttu-id="b3f53-167">Pour plus d’informations, consultez [Créer une machine virtuelle avec une adresse IP publique statique à l’aide de l’interface de ligne de commande Azure](../../virtual-network/virtual-network-deploy-static-pip-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="b3f53-167">For more information, see [Create a VM with a static public IP using the Azure CLI](../../virtual-network/virtual-network-deploy-static-pip-arm-cli.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b3f53-168">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b3f53-168">Next steps</span></span>
<span data-ttu-id="b3f53-169">Pour plus d’informations sur les façons de créer des machines virtuelles dans Azure, consultez les ressources suivantes :</span><span class="sxs-lookup"><span data-stu-id="b3f53-169">For more information about ways to create virtual machines in Azure, see the following resources:</span></span>

* [<span data-ttu-id="b3f53-170">Déploiement et gestion de machines virtuelles à l’aide des modèles Azure Resource Manager et de l’interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="b3f53-170">Use an Azure Resource Manager template to create a specific deployment</span></span>](../windows/cli-deploy-templates.md)
* [<span data-ttu-id="b3f53-171">Créer votre propre environnement personnalisé pour une machine virtuelle Linux à l’aide des commandes de l’interface de ligne de commande Azure directement</span><span class="sxs-lookup"><span data-stu-id="b3f53-171">Create your own custom environment for a Linux VM using Azure CLI commands directly</span></span>](create-cli-complete.md)
* [<span data-ttu-id="b3f53-172">Création d’une machine virtuelle Linux sur Azure à l’aide de modèles</span><span class="sxs-lookup"><span data-stu-id="b3f53-172">Create a Linux VM on Azure using templates</span></span>](create-ssh-secured-vm-from-template.md)
