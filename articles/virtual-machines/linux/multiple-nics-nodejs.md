---
title: "aaaCreate un VM Linux dans Azure avec plusieurs cartes réseau | Documents Microsoft"
description: "Découvrez comment toocreate un VM Linux avec plusieurs cartes réseau connectée tooit utilisant des modèles de hello CLI d’Azure ou le Gestionnaire de ressources."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 457dab734ceeeefd35cddaf1ebb9ea0a82f4e207
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-linux-virtual-machine-with-multiple-nics-using-hello-azure-cli-10"></a><span data-ttu-id="c02e8-103">Créer une machine virtuelle Linux avec plusieurs cartes réseau à l’aide de hello Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="c02e8-103">Create a Linux virtual machine with multiple NICs using hello Azure CLI 1.0</span></span>
<span data-ttu-id="c02e8-104">Vous pouvez créer un ordinateur virtuel (VM) dans Azure qui a plusieurs tooit d’interfaces (NIC) connectées de réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="c02e8-104">You can create a virtual machine (VM) in Azure that has multiple virtual network interfaces (NICs) attached tooit.</span></span> <span data-ttu-id="c02e8-105">Un scénario courant consiste à toohave des sous-réseaux différents pour la connectivité des serveurs frontale et principaux, ou un réseau dédié tooa analyse ou la solution de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="c02e8-105">A common scenario is toohave different subnets for front-end and back-end connectivity, or a network dedicated tooa monitoring or backup solution.</span></span> <span data-ttu-id="c02e8-106">Cet article fournit des commandes rapides toocreate une machine virtuelle avec plusieurs cartes réseau attaché tooit.</span><span class="sxs-lookup"><span data-stu-id="c02e8-106">This article provides quick commands toocreate a VM with multiple NICs attached tooit.</span></span> <span data-ttu-id="c02e8-107">Pour plus d’informations, y compris comment toocreate Bash plusieurs cartes réseau dans vos propres scripts, en savoir plus sur [déploiement de machines virtuelles multi-NIC](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="c02e8-107">For detailed information, including how toocreate multiple NICs within your own Bash scripts, read more about [deploying multi-NIC VMs](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md).</span></span> <span data-ttu-id="c02e8-108">Comme le nombre de cartes réseau prises en charge varie suivant la [taille des machines virtuelles](sizes.md) , pensez à dimensionner la vôtre en conséquence.</span><span class="sxs-lookup"><span data-stu-id="c02e8-108">Different [VM sizes](sizes.md) support a varying number of NICs, so size your VM accordingly.</span></span>

> [!WARNING]
> <span data-ttu-id="c02e8-109">Vous devez associer plusieurs cartes réseau quand vous créez une machine virtuelle, vous ne pouvez pas ajouter tooan de cartes réseau existantes de machine virtuelle avec hello Azure CLI 1.0.</span><span class="sxs-lookup"><span data-stu-id="c02e8-109">You must attach multiple NICs when you create a VM - you cannot add NICs tooan existing VM with hello Azure CLI 1.0.</span></span> <span data-ttu-id="c02e8-110">Vous pouvez [ajouter tooan de cartes réseau existantes de machine virtuelle avec hello Azure CLI 2.0](multiple-nics.md).</span><span class="sxs-lookup"><span data-stu-id="c02e8-110">You can [add NICs tooan existing VM with hello Azure CLI 2.0](multiple-nics.md).</span></span> <span data-ttu-id="c02e8-111">Vous pouvez également [créer une machine virtuelle basée sur des disques virtuels d’origine de hello](copy-vm.md) et créer plusieurs cartes réseau lorsque vous déployez hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="c02e8-111">You can also [create a VM based on hello original virtual disk(s)](copy-vm.md) and create multiple NICs as you deploy hello VM.</span></span>


## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="c02e8-112">Tâche de hello CLI versions toocomplete</span><span class="sxs-lookup"><span data-stu-id="c02e8-112">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="c02e8-113">Vous pouvez exécuter la tâche hello à l’aide de hello CLI versions suivantes :</span><span class="sxs-lookup"><span data-stu-id="c02e8-113">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="c02e8-114">[Azure CLI 1.0](#create-supporting-resources) – notre CLI pour hello classique et la ressource gestion des modèles de déploiement (cet article)</span><span class="sxs-lookup"><span data-stu-id="c02e8-114">[Azure CLI 1.0](#create-supporting-resources) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="c02e8-115">[Azure CLI 2.0](multiple-nics.md) -notre prochaine génération CLI pour le modèle de déploiement de gestion de ressources hello</span><span class="sxs-lookup"><span data-stu-id="c02e8-115">[Azure CLI 2.0](multiple-nics.md) - our next generation CLI for hello resource management deployment model</span></span>


## <a name="create-supporting-resources"></a><span data-ttu-id="c02e8-116">Créer des ressources de support</span><span class="sxs-lookup"><span data-stu-id="c02e8-116">Create supporting resources</span></span>
<span data-ttu-id="c02e8-117">Assurez-vous que vous avez hello [CLI d’Azure](../../cli-install-nodejs.md) connecté et l’utilisation du mode de gestionnaire de ressources :</span><span class="sxs-lookup"><span data-stu-id="c02e8-117">Make sure that you have hello [Azure CLI](../../cli-install-nodejs.md) logged in and using Resource Manager mode:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="c02e8-118">Bonjour les exemples suivants, remplacez les exemples de noms de paramètre par vos propres valeurs.</span><span class="sxs-lookup"><span data-stu-id="c02e8-118">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="c02e8-119">Les noms de paramètre sont par exemple *myResourceGroup*, *mystorageaccount* et *myVM*.</span><span class="sxs-lookup"><span data-stu-id="c02e8-119">Example parameter names included *myResourceGroup*, *mystorageaccount*, and *myVM*.</span></span>

<span data-ttu-id="c02e8-120">Créez d’abord un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="c02e8-120">First, create a resource group.</span></span> <span data-ttu-id="c02e8-121">Hello exemple suivant crée un groupe de ressources nommé *myResourceGroup* Bonjour *eastus* emplacement :</span><span class="sxs-lookup"><span data-stu-id="c02e8-121">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location:</span></span>

```azurecli
azure group create myResourceGroup --location eastus
```

<span data-ttu-id="c02e8-122">Créer un toohold de compte de stockage de vos machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="c02e8-122">Create a storage account toohold your VMs.</span></span> <span data-ttu-id="c02e8-123">Hello exemple suivant crée un compte de stockage nommé *mystorageaccount*:</span><span class="sxs-lookup"><span data-stu-id="c02e8-123">hello following example creates a storage account named *mystorageaccount*:</span></span>

```azurecli
azure storage account create mystorageaccount \
    --resource-group myResourceGroup \
    --location eastus \
    --kind Storage \
    --sku-name PLRS
```

<span data-ttu-id="c02e8-124">Créer un réseau virtuel de tooconnect vos machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="c02e8-124">Create a virtual network tooconnect your VMs to.</span></span> <span data-ttu-id="c02e8-125">Hello exemple suivant crée un réseau virtuel nommé *myVnet* avec un préfixe d’adresse *192.168.0.0/16*:</span><span class="sxs-lookup"><span data-stu-id="c02e8-125">hello following example creates a virtual network named *myVnet* with an address prefix of *192.168.0.0/16*:</span></span>

```azurecli
azure network vnet create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myVnet \
    --address-prefixes 192.168.0.0/16
```

<span data-ttu-id="c02e8-126">Créez deux sous-réseaux de réseau virtuel : l’un pour le trafic frontal, l’autre pour le trafic principal.</span><span class="sxs-lookup"><span data-stu-id="c02e8-126">Create two virtual network subnets - one for front-end traffic and one for back-end traffic.</span></span> <span data-ttu-id="c02e8-127">Hello exemple suivant crée deux sous-réseaux, nommés *mySubnetFrontEnd* et *mySubnetBackEnd*:</span><span class="sxs-lookup"><span data-stu-id="c02e8-127">hello following example creates two subnets, named *mySubnetFrontEnd* and *mySubnetBackEnd*:</span></span>

```azurecli
azure network vnet subnet create \
    --resource-group myResourceGroup \
    --location myVnet \
    --name mySubnetFrontEnd \
    --address-prefix 192.168.1.0/24
azure network vnet subnet create \
    --resource-group myResourceGroup \
    --location myVnet \
    --name mySubnetBackEnd \
    --address-prefix 192.168.2.0/24
```

## <a name="create-and-configure-multiple-nics"></a><span data-ttu-id="c02e8-128">Créer et configurer plusieurs cartes réseau</span><span class="sxs-lookup"><span data-stu-id="c02e8-128">Create and configure multiple NICs</span></span>
<span data-ttu-id="c02e8-129">Vous trouverez plus d’informations sur les [déploiement de plusieurs cartes réseau à l’aide de hello CLI d’Azure](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md), y compris les scripts de processus hello de boucle toocreate toutes les cartes réseau de hello.</span><span class="sxs-lookup"><span data-stu-id="c02e8-129">You can read more details about [deploying multiple NICs using hello Azure CLI](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md), including scripting hello process of looping through toocreate all hello NICs.</span></span>

<span data-ttu-id="c02e8-130">Hello exemple suivant crée deux cartes réseau, nommé *myNic1* et *myNic2*, avec une carte réseau qui connectent tooeach sous-réseau :</span><span class="sxs-lookup"><span data-stu-id="c02e8-130">hello following example creates two NICs, named *myNic1* and *myNic2*, with one NIC connecting tooeach subnet:</span></span>

```azurecli
azure network nic create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNic1 \
    --subnet-vnet-name myVnet \
    --subnet-name mySubnetFrontEnd
azure network nic create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNic2 \
    --subnet-vnet-name myVnet \
    --subnet-name mySubnetBackEnd
```

<span data-ttu-id="c02e8-131">En général, vous créez également un [groupe de sécurité réseau](../../virtual-network/virtual-networks-nsg.md) ou [l’équilibrage de charge](../../load-balancer/load-balancer-overview.md) toohelp gérer et répartir le trafic entre vos machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="c02e8-131">Typically you also create a [Network Security Group](../../virtual-network/virtual-networks-nsg.md) or [load balancer](../../load-balancer/load-balancer-overview.md) toohelp manage and distribute traffic across your VMs.</span></span> <span data-ttu-id="c02e8-132">Hello exemple suivant crée un groupe de sécurité réseau nommé *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="c02e8-132">hello following example creates a Network Security Group named *myNetworkSecurityGroup*:</span></span>

```azurecli
azure network nsg create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNetworkSecurityGroup
```

<span data-ttu-id="c02e8-133">Lier à votre groupe de sécurité réseau de toohello de cartes réseau à l’aide `azure network nic set`.</span><span class="sxs-lookup"><span data-stu-id="c02e8-133">Bind your NICs toohello Network Security Group using `azure network nic set`.</span></span> <span data-ttu-id="c02e8-134">Hello exemple suivant lie *myNic1* et *myNic2* avec *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="c02e8-134">hello following example binds *myNic1* and *myNic2* with *myNetworkSecurityGroup*:</span></span>

```azurecli
azure network nic set \
    --resource-group myResourceGroup \
    --name myNic1 \
    --network-security-group-name myNetworkSecurityGroup
azure network nic set \
    --resource-group myResourceGroup \
    --name myNic2 \
    --network-security-group-name myNetworkSecurityGroup
```

## <a name="create-a-vm-and-attach-hello-nics"></a><span data-ttu-id="c02e8-135">Créer une machine virtuelle et d’attachement des cartes réseau de hello</span><span class="sxs-lookup"><span data-stu-id="c02e8-135">Create a VM and attach hello NICs</span></span>
<span data-ttu-id="c02e8-136">Lorsque vous créez hello machine virtuelle, vous spécifiez maintenant plusieurs cartes réseau.</span><span class="sxs-lookup"><span data-stu-id="c02e8-136">When creating hello VM, you now specify multiple NICs.</span></span> <span data-ttu-id="c02e8-137">Au lieu de cela à l’aide de `--nic-name` tooprovide une seule carte réseau, vous utilisez `--nic-names` et fournir une liste séparée par des virgules de cartes réseau.</span><span class="sxs-lookup"><span data-stu-id="c02e8-137">Rather using `--nic-name` tooprovide a single NIC, instead you use `--nic-names` and provide a comma-separated list of NICs.</span></span> <span data-ttu-id="c02e8-138">Vous devez également tootake attention lorsque vous sélectionnez hello taille de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="c02e8-138">You also need tootake care when you select hello VM size.</span></span> <span data-ttu-id="c02e8-139">Il existe des limites pour le nombre total de hello de cartes réseau que vous pouvez ajouter tooa machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="c02e8-139">There are limits for hello total number of NICs that you can add tooa VM.</span></span> <span data-ttu-id="c02e8-140">En savoir plus sur les [tailles des machines virtuelles Linux](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="c02e8-140">Read more about [Linux VM sizes](sizes.md).</span></span> <span data-ttu-id="c02e8-141">Hello exemple suivant montre comment toospecify plusieurs cartes réseau, puis sur une machine virtuelle de taille qui prend en charge à l’aide de plusieurs cartes réseau (*Standard_DS2_v2*) :</span><span class="sxs-lookup"><span data-stu-id="c02e8-141">hello following example shows how toospecify multiple NICs and then a VM size that supports using multiple NICs (*Standard_DS2_v2*):</span></span>

```azurecli
azure vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --location eastus \
    --os-type linux \
    --nic-names myNic1,myNic2 \
    --vm-size Standard_DS2_v2 \
    --storage-account-name mystorageaccount \
    --image-urn UbuntuLTS \
    --admin-username azureuser \
    --ssh-publickey-file ~/.ssh/id_rsa.pub
```

## <a name="create-multiple-nics-using-resource-manager-templates"></a><span data-ttu-id="c02e8-142">Créer plusieurs cartes réseau à l’aide de modèles Resource Manager</span><span class="sxs-lookup"><span data-stu-id="c02e8-142">Create multiple NICs using Resource Manager templates</span></span>
<span data-ttu-id="c02e8-143">Les modèles de gestionnaire de ressources Azure utilisent déclarative toodefine de fichiers JSON de votre environnement.</span><span class="sxs-lookup"><span data-stu-id="c02e8-143">Azure Resource Manager templates use declarative JSON files toodefine your environment.</span></span> <span data-ttu-id="c02e8-144">Vous pouvez consulter une [vue d’ensemble d’Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c02e8-144">You can read an [overview of Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="c02e8-145">Les modèles de gestionnaire de ressources fournissent une toocreate de façon plusieurs instances d’une ressource pendant le déploiement, telles que la création de plusieurs cartes réseau.</span><span class="sxs-lookup"><span data-stu-id="c02e8-145">Resource Manager templates provide a way toocreate multiple instances of a resource during deployment, such as creating multiple NICs.</span></span> <span data-ttu-id="c02e8-146">Vous utilisez *copie* nombre de hello toospecify de toocreate d’instances :</span><span class="sxs-lookup"><span data-stu-id="c02e8-146">You use *copy* toospecify hello number of instances toocreate:</span></span>

```json
"copy": {
    "name": "multiplenics"
    "count": "[parameters('count')]"
}
```

<span data-ttu-id="c02e8-147">En savoir plus sur la [création de plusieurs instances à l’aide de *copy*](../../resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="c02e8-147">Read more about [creating multiple instances using *copy*](../../resource-group-create-multiple.md).</span></span> 

<span data-ttu-id="c02e8-148">Vous pouvez également utiliser un `copyIndex()` toothen ajouter un nom de ressource tooa nombre, qui vous permet de toocreate `myNic1`, `myNic2`, etc. hello Voici un exemple d’ajout de valeur d’index hello :</span><span class="sxs-lookup"><span data-stu-id="c02e8-148">You can also use a `copyIndex()` toothen append a number tooa resource name, which allows you toocreate `myNic1`, `myNic2`, etc. hello following shows an example of appending hello index value:</span></span>

```json
"name": "[concat('myNic', copyIndex())]", 
```

<span data-ttu-id="c02e8-149">Vous pouvez consulter un exemple complet de la [création de plusieurs cartes réseau à l’aide de modèles Resource Manager](../../virtual-network/virtual-network-deploy-multinic-arm-template.md).</span><span class="sxs-lookup"><span data-stu-id="c02e8-149">You can read a complete example of [creating multiple NICs using Resource Manager templates](../../virtual-network/virtual-network-deploy-multinic-arm-template.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c02e8-150">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c02e8-150">Next steps</span></span>
<span data-ttu-id="c02e8-151">Assurez-vous que tooreview [tailles de Linux VM](sizes.md) lors de la tentative de toocreating une machine virtuelle avec plusieurs cartes réseau.</span><span class="sxs-lookup"><span data-stu-id="c02e8-151">Make sure tooreview [Linux VM sizes](sizes.md) when trying toocreating a VM with multiple NICs.</span></span> <span data-ttu-id="c02e8-152">Payer une attention toohello nombre de cartes réseau prend en charge la taille de chaque machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="c02e8-152">Pay attention toohello maximum number of NICs each VM size supports.</span></span> 

<span data-ttu-id="c02e8-153">Souvenez-vous que vous ne pouvez pas ajouter tooan de cartes réseau supplémentaire existant de machine virtuelle, vous devez créer des toutes les cartes réseau de hello lorsque vous déployez hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="c02e8-153">Remember that you cannot add additional NICs tooan existing VM, you must create all hello NICs when you deploy hello VM.</span></span> <span data-ttu-id="c02e8-154">Prenez soin lors de la planification de votre toomake de déploiements que vous avez toute la connectivité réseau hello requis à partir du début de hello.</span><span class="sxs-lookup"><span data-stu-id="c02e8-154">Take care when planning your deployments toomake sure that you have all hello required network connectivity from hello outset.</span></span>

