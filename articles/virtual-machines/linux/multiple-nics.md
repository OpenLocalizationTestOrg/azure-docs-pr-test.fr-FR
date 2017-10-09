---
title: "aaaCreate un VM Linux dans Azure avec plusieurs cartes réseau | Documents Microsoft"
description: "Découvrez comment toocreate un VM Linux avec plusieurs cartes réseau connectée tooit à l’aide de modèles Azure CLI 2.0 ou le Gestionnaire de ressources de hello."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 5d2d04d0-fc62-45fa-88b1-61808a2bc691
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 2723405914777a5dce4354d4f5d8413e357f58e7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-linux-virtual-machine-in-azure-with-multiple-network-interface-cards"></a><span data-ttu-id="5459b-103">Comment toocreate une machine virtuelle de Linux dans Azure avec le réseau de plusieurs cartes d’interface</span><span class="sxs-lookup"><span data-stu-id="5459b-103">How toocreate a Linux virtual machine in Azure with multiple network interface cards</span></span>
<span data-ttu-id="5459b-104">Vous pouvez créer un ordinateur virtuel (VM) dans Azure qui a plusieurs tooit d’interfaces (NIC) connectées de réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="5459b-104">You can create a virtual machine (VM) in Azure that has multiple virtual network interfaces (NICs) attached tooit.</span></span> <span data-ttu-id="5459b-105">Un scénario courant consiste à toohave des sous-réseaux différents pour la connectivité des serveurs frontale et principaux, ou un réseau dédié tooa analyse ou la solution de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="5459b-105">A common scenario is toohave different subnets for front-end and back-end connectivity, or a network dedicated tooa monitoring or backup solution.</span></span> <span data-ttu-id="5459b-106">Cet article décrit en détail comment toocreate une machine virtuelle avec plusieurs cartes réseau attaché tooit et tooadd ou supprimer des cartes réseau à partir d’une machine virtuelle existante.</span><span class="sxs-lookup"><span data-stu-id="5459b-106">This article details how toocreate a VM with multiple NICs attached tooit and how tooadd or remove NICs from an existing VM.</span></span> <span data-ttu-id="5459b-107">Pour plus d’informations, y compris comment toocreate Bash plusieurs cartes réseau dans vos propres scripts, en savoir plus sur [déploiement de machines virtuelles multi-NIC](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="5459b-107">For detailed information, including how toocreate multiple NICs within your own Bash scripts, read more about [deploying multi-NIC VMs](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md).</span></span> <span data-ttu-id="5459b-108">Comme le nombre de cartes réseau prises en charge varie suivant la [taille des machines virtuelles](sizes.md) , pensez à dimensionner la vôtre en conséquence.</span><span class="sxs-lookup"><span data-stu-id="5459b-108">Different [VM sizes](sizes.md) support a varying number of NICs, so size your VM accordingly.</span></span>

<span data-ttu-id="5459b-109">Cet article décrit en détail comment toocreate une machine virtuelle avec plusieurs cartes réseau avec hello Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="5459b-109">This article details how toocreate a VM with multiple NICs with hello Azure CLI 2.0.</span></span> <span data-ttu-id="5459b-110">Vous pouvez également effectuer ces étapes avec hello [Azure CLI 1.0](multiple-nics-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="5459b-110">You can also perform these steps with hello [Azure CLI 1.0](multiple-nics-nodejs.md).</span></span>


## <a name="create-supporting-resources"></a><span data-ttu-id="5459b-111">Créer des ressources de support</span><span class="sxs-lookup"><span data-stu-id="5459b-111">Create supporting resources</span></span>
<span data-ttu-id="5459b-112">Hello installation dernières [Azure CLI 2.0](/cli/azure/install-az-cli2) et connectez-vous à l’aide du compte Azure tooan [ouverture de session az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="5459b-112">Install hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="5459b-113">Bonjour les exemples suivants, remplacez les exemples de noms de paramètre par vos propres valeurs.</span><span class="sxs-lookup"><span data-stu-id="5459b-113">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="5459b-114">Les noms de paramètre sont par exemple *myResourceGroup*, *mystorageaccount* et *myVM*.</span><span class="sxs-lookup"><span data-stu-id="5459b-114">Example parameter names included *myResourceGroup*, *mystorageaccount*, and *myVM*.</span></span>

<span data-ttu-id="5459b-115">Tout d’abord, créez un groupe de ressources avec la commande [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="5459b-115">First, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="5459b-116">Hello exemple suivant crée un groupe de ressources nommé *myResourceGroup* Bonjour *eastus* emplacement :</span><span class="sxs-lookup"><span data-stu-id="5459b-116">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="5459b-117">Créer le réseau virtuel hello [créer un réseau virtuel du réseau az](/cli/azure/network/vnet#create).</span><span class="sxs-lookup"><span data-stu-id="5459b-117">Create hello virtual network with [az network vnet create](/cli/azure/network/vnet#create).</span></span> <span data-ttu-id="5459b-118">Hello exemple suivant crée un réseau virtuel nommé *myVnet* et sous-réseau nommé *mySubnetFrontEnd*:</span><span class="sxs-lookup"><span data-stu-id="5459b-118">hello following example creates a virtual network named *myVnet* and subnet named *mySubnetFrontEnd*:</span></span>

```azurecli
az network vnet create \
    --resource-group myResourceGroup \
    --name myVnet \
    --address-prefix 192.168.0.0/16 \
    --subnet-name mySubnetFrontEnd \
    --subnet-prefix 192.168.1.0/24
```

<span data-ttu-id="5459b-119">Créer un sous-réseau pour le trafic de back-end hello avec [créer de sous-réseau de réseau virtuel az réseau](/cli/azure/network/vnet/subnet#create).</span><span class="sxs-lookup"><span data-stu-id="5459b-119">Create a subnet for hello back-end traffic with [az network vnet subnet create](/cli/azure/network/vnet/subnet#create).</span></span> <span data-ttu-id="5459b-120">Hello exemple suivant crée un sous-réseau nommé *mySubnetBackEnd*:</span><span class="sxs-lookup"><span data-stu-id="5459b-120">hello following example creates a subnet named *mySubnetBackEnd*:</span></span>

```azurecli
az network vnet subnet create \
    --resource-group myResourceGroup \
    --vnet-name myVnet \
    --name mySubnetBackEnd \
    --address-prefix 192.168.2.0/24
```

<span data-ttu-id="5459b-121">Créez un groupe de sécurité réseau avec la commande [az network nsg create](/cli/azure/network/nsg#create).</span><span class="sxs-lookup"><span data-stu-id="5459b-121">Create a network security group with [az network nsg create](/cli/azure/network/nsg#create).</span></span> <span data-ttu-id="5459b-122">Hello exemple suivant crée un groupe de sécurité réseau nommé *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="5459b-122">hello following example creates a network security group named *myNetworkSecurityGroup*:</span></span>

```azurecli
az network nsg create \
    --resource-group myResourceGroup \
    --name myNetworkSecurityGroup
```

## <a name="create-and-configure-multiple-nics"></a><span data-ttu-id="5459b-123">Créer et configurer plusieurs cartes réseau</span><span class="sxs-lookup"><span data-stu-id="5459b-123">Create and configure multiple NICs</span></span>
<span data-ttu-id="5459b-124">Créez deux cartes réseau avec la commande [az network nic create](/cli/azure/network/nic#create).</span><span class="sxs-lookup"><span data-stu-id="5459b-124">Create two NICs with [az network nic create](/cli/azure/network/nic#create).</span></span> <span data-ttu-id="5459b-125">Hello exemple suivant crée deux cartes réseau, nommé *myNic1* et *myNic2*et connectées, groupe de sécurité réseau hello, avec une carte réseau qui connectent tooeach sous-réseau :</span><span class="sxs-lookup"><span data-stu-id="5459b-125">hello following example creates two NICs, named *myNic1* and *myNic2*, connected hello network security group, with one NIC connecting tooeach subnet:</span></span>

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --name myNic1 \
    --vnet-name myVnet \
    --subnet mySubnetFrontEnd \
    --network-security-group myNetworkSecurityGroup
az network nic create \
    --resource-group myResourceGroup \
    --name myNic2 \
    --vnet-name myVnet \
    --subnet mySubnetBackEnd \
    --network-security-group myNetworkSecurityGroup
```

## <a name="create-a-vm-and-attach-hello-nics"></a><span data-ttu-id="5459b-126">Créer une machine virtuelle et d’attachement des cartes réseau de hello</span><span class="sxs-lookup"><span data-stu-id="5459b-126">Create a VM and attach hello NICs</span></span>
<span data-ttu-id="5459b-127">Lorsque vous créez hello machine virtuelle, spécifiez des cartes réseau de hello que vous avez créé avec `--nics`.</span><span class="sxs-lookup"><span data-stu-id="5459b-127">When you create hello VM, specify hello NICs you created with `--nics`.</span></span> <span data-ttu-id="5459b-128">Vous devez également tootake attention lorsque vous sélectionnez hello taille de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="5459b-128">You also need tootake care when you select hello VM size.</span></span> <span data-ttu-id="5459b-129">Il existe des limites pour le nombre total de hello de cartes réseau que vous pouvez ajouter tooa machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="5459b-129">There are limits for hello total number of NICs that you can add tooa VM.</span></span> <span data-ttu-id="5459b-130">En savoir plus sur les [tailles des machines virtuelles Linux](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="5459b-130">Read more about [Linux VM sizes](sizes.md).</span></span> 

<span data-ttu-id="5459b-131">Créez une machine virtuelle avec la commande [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="5459b-131">Create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="5459b-132">Hello exemple suivant crée un ordinateur virtuel nommé *myVM*:</span><span class="sxs-lookup"><span data-stu-id="5459b-132">hello following example creates a VM named *myVM*:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --size Standard_DS3_v2 \
    --admin-username azureuser \
    --generate-ssh-keys \
    --nics myNic1 myNic2
```

## <a name="add-a-nic-tooa-vm"></a><span data-ttu-id="5459b-133">Ajouter un tooa de carte réseau virtuelle</span><span class="sxs-lookup"><span data-stu-id="5459b-133">Add a NIC tooa VM</span></span>
<span data-ttu-id="5459b-134">les étapes précédentes Hello créé une machine virtuelle avec plusieurs cartes réseau.</span><span class="sxs-lookup"><span data-stu-id="5459b-134">hello previous steps created a VM with multiple NICs.</span></span> <span data-ttu-id="5459b-135">Vous pouvez également ajouter tooan de cartes réseau existantes de machine virtuelle avec hello Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="5459b-135">You can also add NICs tooan existing VM with hello Azure CLI 2.0.</span></span> 

<span data-ttu-id="5459b-136">Créez une autre carte réseau avec [az network nic create](/cli/azure/network/nic#create).</span><span class="sxs-lookup"><span data-stu-id="5459b-136">Create another NIC with [az network nic create](/cli/azure/network/nic#create).</span></span> <span data-ttu-id="5459b-137">Hello exemple suivant crée une carte réseau nommée *myNic3* connecté sous-réseau principal de toohello et le groupe de sécurité réseau créé dans les étapes précédentes hello :</span><span class="sxs-lookup"><span data-stu-id="5459b-137">hello following example creates a NIC named *myNic3* connected toohello back-end subnet and network security group created in hello previous steps:</span></span>

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --name myNic3 \
    --vnet-name myVnet \
    --subnet mySubnetBackEnd \
    --network-security-group myNetworkSecurityGroup
```

<span data-ttu-id="5459b-138">tooadd un tooan de carte réseau ordinateur virtuel existant, d’abord libérer hello machine virtuelle avec [az vm désallouer](/cli/azure/vm#deallocate).</span><span class="sxs-lookup"><span data-stu-id="5459b-138">tooadd a NIC tooan existing VM, first deallocate hello VM with [az vm deallocate](/cli/azure/vm#deallocate).</span></span> <span data-ttu-id="5459b-139">exemple Hello désalloue hello ordinateur virtuel nommé *myVM*:</span><span class="sxs-lookup"><span data-stu-id="5459b-139">hello following example deallocates hello VM named *myVM*:</span></span>

```azurecli
az vm deallocate --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="5459b-140">Ajouter hello carte réseau avec [ajouter de carte réseau de machine virtuelle az](/cli/azure/vm/nic#add).</span><span class="sxs-lookup"><span data-stu-id="5459b-140">Add hello NIC with [az vm nic add](/cli/azure/vm/nic#add).</span></span> <span data-ttu-id="5459b-141">Hello exemple suivant ajoute *myNic3* trop*myVM*:</span><span class="sxs-lookup"><span data-stu-id="5459b-141">hello following example adds *myNic3* too*myVM*:</span></span>

```azurecli
az vm nic add \
    --resource-group myResourceGroup \
    --vm-name myVM \
    --nics myNic3
```

<span data-ttu-id="5459b-142">Démarrer hello machine virtuelle avec [début de machine virtuelle az](/cli/azure/vm#start):</span><span class="sxs-lookup"><span data-stu-id="5459b-142">Start hello VM with [az vm start](/cli/azure/vm#start):</span></span>

```azurecli
az vm start --resource-group myResourceGroup --name myVM
```

## <a name="remove-a-nic-from-a-vm"></a><span data-ttu-id="5459b-143">Suppression d’une carte réseau d’une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="5459b-143">Remove a NIC from a VM</span></span>
<span data-ttu-id="5459b-144">tooremove une carte réseau à partir d’un ordinateur virtuel existant, d’abord libérer hello machine virtuelle avec [az vm désallouer](/cli/azure/vm#deallocate).</span><span class="sxs-lookup"><span data-stu-id="5459b-144">tooremove a NIC from an existing VM, first deallocate hello VM with [az vm deallocate](/cli/azure/vm#deallocate).</span></span> <span data-ttu-id="5459b-145">exemple Hello désalloue hello ordinateur virtuel nommé *myVM*:</span><span class="sxs-lookup"><span data-stu-id="5459b-145">hello following example deallocates hello VM named *myVM*:</span></span>

```azurecli
az vm deallocate --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="5459b-146">Supprimer hello carte réseau avec [supprimer de la carte réseau de machine virtuelle az](/cli/azure/vm/nic#remove).</span><span class="sxs-lookup"><span data-stu-id="5459b-146">Remove hello NIC with [az vm nic remove](/cli/azure/vm/nic#remove).</span></span> <span data-ttu-id="5459b-147">Hello exemple suivant supprime *myNic3* de *myVM*:</span><span class="sxs-lookup"><span data-stu-id="5459b-147">hello following example removes *myNic3* from *myVM*:</span></span>

```azurecli
az vm nic remove \
    --resource-group myResourceGroup \
    --vm-name myVM 
    --nics myNic3
```

<span data-ttu-id="5459b-148">Démarrer hello machine virtuelle avec [début de machine virtuelle az](/cli/azure/vm#start):</span><span class="sxs-lookup"><span data-stu-id="5459b-148">Start hello VM with [az vm start](/cli/azure/vm#start):</span></span>

```azurecli
az vm start --resource-group myResourceGroup --name myVM
```


## <a name="create-multiple-nics-using-resource-manager-templates"></a><span data-ttu-id="5459b-149">Créer plusieurs cartes réseau à l’aide de modèles Resource Manager</span><span class="sxs-lookup"><span data-stu-id="5459b-149">Create multiple NICs using Resource Manager templates</span></span>
<span data-ttu-id="5459b-150">Les modèles de gestionnaire de ressources Azure utilisent déclarative toodefine de fichiers JSON de votre environnement.</span><span class="sxs-lookup"><span data-stu-id="5459b-150">Azure Resource Manager templates use declarative JSON files toodefine your environment.</span></span> <span data-ttu-id="5459b-151">Vous pouvez consulter une [vue d’ensemble d’Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5459b-151">You can read an [overview of Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="5459b-152">Les modèles de gestionnaire de ressources fournissent une toocreate de façon plusieurs instances d’une ressource pendant le déploiement, telles que la création de plusieurs cartes réseau.</span><span class="sxs-lookup"><span data-stu-id="5459b-152">Resource Manager templates provide a way toocreate multiple instances of a resource during deployment, such as creating multiple NICs.</span></span> <span data-ttu-id="5459b-153">Vous utilisez *copie* nombre de hello toospecify de toocreate d’instances :</span><span class="sxs-lookup"><span data-stu-id="5459b-153">You use *copy* toospecify hello number of instances toocreate:</span></span>

```json
"copy": {
    "name": "multiplenics"
    "count": "[parameters('count')]"
}
```

<span data-ttu-id="5459b-154">En savoir plus sur la [création de plusieurs instances à l’aide de *copy*](../../resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="5459b-154">Read more about [creating multiple instances using *copy*](../../resource-group-create-multiple.md).</span></span> 

<span data-ttu-id="5459b-155">Vous pouvez également utiliser un `copyIndex()` toothen ajouter un nom de ressource tooa nombre, qui vous permet de toocreate `myNic1`, `myNic2`, etc. hello Voici un exemple d’ajout de valeur d’index hello :</span><span class="sxs-lookup"><span data-stu-id="5459b-155">You can also use a `copyIndex()` toothen append a number tooa resource name, which allows you toocreate `myNic1`, `myNic2`, etc. hello following shows an example of appending hello index value:</span></span>

```json
"name": "[concat('myNic', copyIndex())]", 
```

<span data-ttu-id="5459b-156">Vous pouvez consulter un exemple complet de la [création de plusieurs cartes réseau à l’aide de modèles Resource Manager](../../virtual-network/virtual-network-deploy-multinic-arm-template.md).</span><span class="sxs-lookup"><span data-stu-id="5459b-156">You can read a complete example of [creating multiple NICs using Resource Manager templates](../../virtual-network/virtual-network-deploy-multinic-arm-template.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="5459b-157">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="5459b-157">Next steps</span></span>
<span data-ttu-id="5459b-158">Révision [tailles de Linux VM](sizes.md) lors de la tentative de toocreating une machine virtuelle avec plusieurs cartes réseau.</span><span class="sxs-lookup"><span data-stu-id="5459b-158">Review [Linux VM sizes](sizes.md) when trying toocreating a VM with multiple NICs.</span></span> <span data-ttu-id="5459b-159">Payer une attention toohello nombre de cartes réseau prend en charge la taille de chaque machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="5459b-159">Pay attention toohello maximum number of NICs each VM size supports.</span></span> 
